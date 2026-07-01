---
title: "Tự động phản ứng (Lambda & EventBridge)"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### Kịch bản

Khi **Amazon GuardDuty** phát hiện IP tấn công/quét port máy chủ, **Amazon EventBridge** bắt tín hiệu và gọi **AWS Lambda** để tự động thêm IP đó vào danh sách chặn của **Security Group**.

### Bước 1: Tạo hàm AWS Lambda

1. Truy cập **Lambda** → **Create function**.
   - **Function name:** `Minecraft-Automated-Block-IP`
   - **Runtime:** **Python 3.13**

![Tạo hàm Lambda](/images/5-Workshop/5.4/4.a.LBD.png)

![Chọn Python runtime](/images/5-Workshop/5.4/4.b.LBD.png)

2. Sau khi tạo xong, cuộn xuống **Configuration** → **Permissions** → bấm tên Role của Lambda để mở trang **IAM**.

![Quyền Lambda](/images/5-Workshop/5.4/4.c.LBD.png)

3. Trong IAM, bấm **Add permissions** → **Attach policies**.

![Thêm quyền](/images/5-Workshop/5.4/4.d.LBD.png)

![Gắn policies](/images/5-Workshop/5.4/4.e.LBD.IAM.png)

4. Tìm `AmazonEC2FullAccess`, tích chọn và bấm **Add permissions**.

![Gắn policy EC2](/images/5-Workshop/5.4/4.f.LBD.IAM.png)

5. Quay lại tab **Code** của Lambda, thay toàn bộ code bằng script Python từ Colab. Bấm **Deploy**.

```python
import boto3
import json
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

ec2 = boto3.client('ec2')

def lambda_handler(event, context):
    try:
        # 1. Bóc tách log từ GuardDuty gửi sang để tìm IP kẻ tấn công
        detail = event.get('detail', {})
        finding_type = detail.get('type', 'Unknown Threat')

        connection_details = detail.get('service', {}).get('action', {}).get('networkConnectionAction', {})
        attacker_ip = connection_details.get('remoteIpDetails', {}).get('ipAddressV4')

        if not attacker_ip:
            logger.info("Không tìm thấy IP tấn công hợp lệ trong bản ghi này (Bản ghi có thể không liên quan đến Network).")
            return {'statusCode': 200, 'body': 'No attacker IP found.'}

        logger.info(f"🚨 PHÁT HIỆN CUỘC TẤN CÔNG: '{finding_type}' từ IP: {attacker_ip}")

        # 2. Tìm ID của Network ACL (Tường lửa tầng mạng của VPC)
        network_acls = ec2.describe_network_acls()
        target_nacl_id = network_acls['NetworkAcls'][0]['NetworkAclId']

        # Đặt số thứ tự cho luật chặn (Rule Number).
        # Trong NACL, số càng nhỏ càng ưu tiên tối cao. Số 50 sẽ đứng trước các luật mặc định (thường là 100).
        rule_number = 50

        # 3. Tạo một luật "DENY" (Chặn đứng) ngay lập tức tại cửa ngõ VPC
        ec2.create_network_acl_entry(
            NetworkAclId=target_nacl_id,
            RuleNumber=rule_number,
            Protocol='-1', # Chặn toàn bộ các giao thức (TCP, UDP, ICMP...)
            RuleAction='deny', # Hành động: Từ chối / Chặn hoàn toàn
            Egress=False, # Áp dụng cho chiều dữ liệu đi VÀO (Inbound)
            CidrBlock=f"{attacker_ip}/32" # Chặn chính xác duy nhất IP này
        )

        logger.info(f"🛡️ SOAR ACTION SUCCESS: Đã tự động tạo luật BLOCK IP {attacker_ip} tại Network ACL ({target_nacl_id}). Kẻ tấn công đã bị cô lập hoàn toàn!")

        return {
            'statusCode': 200,
            'body': json.dumps(f"Successfully blocked {attacker_ip}")
        }

    except Exception as e:
        # Nếu rule_number 50 đã tồn tại (đã chặn 1 IP trước đó), ta sẽ bắt lỗi và ghi đè/tăng số rule lên để tránh lỗi trùng lặp khi demo
        if "NetworkAclEntryAlreadyExists" in str(e):
            logger.info(f"IP {attacker_ip} đã nằm trong danh sách chặn hoặc Rule ID bị trùng. Đang cập nhật lại...")
            try:
                ec2.replace_network_acl_entry(
                    NetworkAclId=target_nacl_id,
                    RuleNumber=rule_number,
                    Protocol='-1',
                    RuleAction='deny',
                    Egress=False,
                    CidrBlock=f"{attacker_ip}/32"
                )
                logger.info(f"🛡️ Đã cập nhật đè Rule chặn thành công cho IP: {attacker_ip}")
                return {'statusCode': 200, 'body': 'Updated block rule.'}
            except Exception as re:
                logger.error(f"Lỗi khi cố gắng thay thế Entry: {str(re)}")

        logger.error(f"❌ Lỗi thực thi hệ thống SOAR: {str(e)}")
        return {'statusCode': 500, 'body': json.dumps("Internal Error")}
```

![Code đã deploy](/images/5-Workshop/5.4/4.h.LBD.png)

> **Lưu ý:** PDF tham chiếu một notebook Colab cho code Lambda. Ở dòng số 11, thay thế placeholder ARN bằng ARN thực tế của SNS topic ở phần 5.7.

### Bước 2: Tạo EventBridge Rule

1. Mở **Amazon EventBridge** → **Rules** → **Create rule**.
   - **Name:** `GuardDuty-To-Lambda-Block`
   - **Rule type:** **Rule with an event pattern**

![Tạo EventBridge rule](/images/5-Workshop/5.4/4.i.LBD.EB.png)

![Loại rule](/images/5-Workshop/5.4/4.j.LBD.EB.png)

2. Bấm **Next**. Ở phần **Event source**, chọn **AWS services**.
   - **AWS service:** **GuardDuty**

![Nguồn GuardDuty](/images/5-Workshop/5.4/4.k.LBD.EB.png)

   - **Event type:** **GuardDuty Finding**

3. Bấm **Next**. Ở phần **Select target(s)**:
   - **Target:** **Lambda function**
   - **Function:** `Minecraft-Automated-Block-IP`

![Chọn target Lambda](/images/5-Workshop/5.4/4.l.LBD.EB.png)

4. Bấm **Next** qua các bước còn lại và **Create rule**.

![Rule đã tạo](/images/5-Workshop/5.4/4.m.LBD.EB.png)

### Kết quả

Khi GuardDuty phát hiện mối đe dọa, EventBridge kích hoạt Lambda. Lambda sẽ tự động chặn IP tấn công trong Security Group và gửi cảnh báo.
