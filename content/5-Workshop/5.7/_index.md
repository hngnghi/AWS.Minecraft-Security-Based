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
   - Important: replace the sample ARN placeholder on line 11 with your actual SNS Topic ARN.
6. Click **Deploy**.

### Result

When GuardDuty finds a threat, Lambda now blocks the attacker IP and immediately sends an email alert via SNS.
