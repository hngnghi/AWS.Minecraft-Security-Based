---
title: "Thông báo Email (SNS)"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

Để nâng cao điểm báo cáo SOAR, chúng ta sẽ nâng cấp hàm Lambda ở phần 5.4 để tự động gửi email cảnh báo chi tiết ngay khi phát hiện tấn công.

Chúng ta dùng **Amazon SNS (Simple Notification Service)** vì nó cực kỳ ổn định, bảo mật và hoàn toàn miễn phí ở quy mô này.

### Bước 1: Tạo Topic Amazon SNS

1. Tìm **Simple Notification Service (SNS)** trên thanh tìm kiếm AWS.

![Tìm SNS](/images/5-Workshop/5.7/7.a.SNS.png)

2. Tại màn hình chính, nhập tên Topic:
   - **Topic name:** `Minecraft-Attack-Alerts` → bấm **Next step**.

![Tạo topic](/images/5-Workshop/5.7/7.b.SNS.png)

3. Chọn **Standard** → cuộn xuống bấm **Create topic**.

4. Sau khi tạo xong, bấm **Create subscription** để đăng ký nhận email:
   - **Protocol:** `Email`
   - **Endpoint:** địa chỉ email của bạn
   - Bấm **Create subscription**.

![Tạo subscription](/images/5-Workshop/5.7/7.c.SNS.png)

5. Kích hoạt email:
   - Mở hộp thư, tìm thư xác nhận từ AWS.
   - Bấm **Confirm Subscription**.
   - Khi màn hình hiện `Subscription confirmed!` là thành công.

![Đã xác nhận subscription](/images/5-Workshop/5.7/7.d.SNS.png)

6. Quay lại SNS, copy ARN của Topic. ARN có dạng:

```text
arn:aws:sns:us-east-1:845242191085:Minecraft-Attack-Alerts:5902fe45-b63f-494c-9668-e7bdc655690e
```

### Bước 2: Nâng cấp Lambda gửi Email

1. Vào **Lambda** → mở hàm `Minecraft-Automated-Block-IP`.
2. Mở **Configuration** → **Permissions** → bấm link tên Role để sang trang **IAM**.
3. Trong IAM, bấm **Add permissions** → **Attach policies**.
4. Tìm `AmazonSNSFullAccess`, tích chọn và bấm **Add permissions**.
5. Quay lại tab **Code** của Lambda, thay thế code bằng phiên bản nâng cấp từ Colab.

```python
import boto3
import json
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

ec2 = boto3.client('ec2')
sns = boto3.client('sns')

# ⚠️ HÃY THAY MÃ ARN TOPIC SNS CỦA BẠN VÀO ĐÂY:
SNS_TOPIC_ARN = "arn:aws:sns:us-east-1:845242191085:Minecraft-Attack-Alerts:5902fe45-b63f-494c-9668-e7bdc655690e"

def lambda_handler(event, context):
    try:
        detail = event.get('detail', {})
        finding_type = detail.get('type', 'Unknown Threat')
        severity = detail.get('severity', 'High')

        connection_details = detail.get('service', {}).get('action', {}).get('networkConnectionAction', {})
        attacker_ip = connection_details.get('remoteIpDetails', {}).get('ipAddressV4')

        if not attacker_ip:
            logger.info("Bản ghi không chứa IP tấn công mạng.")
            return {'statusCode': 200, 'body': 'No attacker IP found.'}

        logger.info(f"🚨 PHÁT HIỆN CUỘC TẤN CÔNG: '{finding_type}' từ IP: {attacker_ip}")

        # 1. Thực hiện lệnh chặn tại Network ACL
        network_acls = ec2.describe_network_acls()
        target_nacl_id = network_acls['NetworkAcls'][0]['NetworkAclId']
        rule_number = 50

        ec2.create_network_acl_entry(
            NetworkAclId=target_nacl_id,
            RuleNumber=rule_number,
            Protocol='-1',
            RuleAction='deny',
            Egress=False,
            CidrBlock=f"{attacker_ip}/32"
        )

        action_msg = f"🛡️ SOAR ACTION SUCCESS: Đã chặn đứng IP {attacker_ip} tại Network ACL ({target_nacl_id})."
        logger.info(action_msg)

        # 2. BẮN EMAIL CẢNH BÁO TING TING QUA SNS
        email_subject = f"🚨 [AWS SOAR ALERT] Phát hiện & Chặn đứng tấn công máy chủ Minecraft!"
        email_body = (
            f"Hệ thống tự động phát hiện xâm nhập (SOAR) báo cáo:\n\n"
            f"- Loại tấn công: {finding_type}\n"
            f"- Mức độ nguy hiểm (Severity): {severity}/8\n"
            f"- IP kẻ tấn công: {attacker_ip}\n"
            f"- Hành động phản ứng: {action_msg}\n\n"
            f"Trạng thái hệ thống: ĐÃ AN TOÀN. Kẻ tấn công đã bị cô lập hoàn toàn."
        )

        sns.publish(
            TopicArn=SNS_TOPIC_ARN,
            Message=email_body,
            Subject=email_subject
        )
        logger.info("📩 Đã gửi email thông báo thành công qua Amazon SNS!")

        return {
            'statusCode': 200,
            'body': 'Successfully blocked and notified.'
        }

    except Exception as e:
        if "NetworkAclEntryAlreadyExists" in str(e):
            logger.info(f"IP {attacker_ip} đã bị chặn từ trước.")
            return {
                'statusCode': 200,
                'body': 'IP already blocked.'
            }

        logger.error(f"❌ Lỗi hệ thống SOAR: {str(e)}")
        return {
            'statusCode': 500,
            'body': 'Internal Error'
        }
```

   - Lưu ý: thay thế ARN mẫu ở dòng số 11 bằng ARN thực tế của SNS Topic.
6. Bấm **Deploy**.

### Kết quả

Khi GuardDuty phát hiện tấn công, Lambda sẽ vừa chặn IP, vừa gửi email cảnh báo qua SNS.
