---
title: "Email Notifications (SNS)"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

To maximize the SOAR demo impact, upgrade the Lambda function from section 5.4 so it sends detailed email alerts automatically when an attack is detected.

We use **Amazon SNS (Simple Notification Service)** because it is stable, secure, and free at this scale.

### Step 1: Create SNS Topic

1. Search for **Simple Notification Service (SNS)** in AWS Console.

![SNS search](/images/5-Workshop/5.7/7.a.SNS.png)

2. On the main screen, enter the Topic name:
   - **Topic name:** `Minecraft-Attack-Alerts` → click **Next step**.

![Create topic](/images/5-Workshop/5.7/7.b.SNS.png)

3. Choose **Standard** → scroll down and click **Create topic**.

4. After creation, scroll down and click **Create subscription** to register an email recipient:
   - **Protocol:** `Email`
   - **Endpoint:** your email address
   - Click **Create subscription**.

![Create subscription](/images/5-Workshop/5.7/7.c.SNS.png)

5. Confirm the email subscription:
   - Open the confirmation email from AWS.
   - Click **Confirm Subscription**.
   - When the screen shows `Subscription confirmed!`, the setup is successful.

![Subscription confirmed](/images/5-Workshop/5.7/7.d.SNS.png)

6. Return to the SNS console and copy the Topic **ARN**. It looks like:

```text
arn:aws:sns:us-east-1:845242191085:Minecraft-Attack-Alerts:5902fe45-b63f-494c-9668-e7bdc655690e
```

### Step 2: Upgrade Lambda to Send Email

1. Go to **Lambda** → open `Minecraft-Automated-Block-IP`.
2. Open **Configuration** → **Permissions** → click the Role name link to open **IAM**.
3. In IAM, click **Add permissions** → **Attach policies**.
4. Search for `AmazonSNSFullAccess`, select it, and click **Add permissions**.
5. Return to the Lambda **Code** tab and replace the code with the upgraded version from the Colab notebook.

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

   - Important: replace the sample ARN placeholder on line 11 with your actual SNS Topic ARN.
6. Click **Deploy**.

### Result

When GuardDuty finds a threat, Lambda now blocks the attacker IP and immediately sends an email alert via SNS.
