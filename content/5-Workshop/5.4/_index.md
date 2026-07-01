---
title: "Automated Response (Lambda & EventBridge)"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### Scenario

When **Amazon GuardDuty** detects an attacker scanning or brute-forcing the server, **Amazon EventBridge** captures the alert and invokes **AWS Lambda** to automatically add the attacker IP to the **Security Group** block list.

### Step 1: Create AWS Lambda Function

1. Go to **Lambda** → **Create function**.
   - **Function name:** `Minecraft-Automated-Block-IP`
   - **Runtime:** **Python 3.13**

![Create Lambda function](/images/5-Workshop/5.4/4.a.LBD.png)

![Select Python runtime](/images/5-Workshop/5.4/4.b.LBD.png)

2. After creation, scroll to **Configuration** → **Permissions** → click the Lambda role name to open **IAM**.

![Lambda permissions](/images/5-Workshop/5.4/4.c.LBD.png)

3. In IAM, click **Add permissions** → **Attach policies**.

![Add permissions](/images/5-Workshop/5.4/4.d.LBD.png)

![Attach policies](/images/5-Workshop/5.4/4.e.LBD.IAM.png)

4. Search for `AmazonEC2FullAccess`, select it, and click **Add permissions**.

![Attach EC2 policy](/images/5-Workshop/5.4/4.f.LBD.IAM.png)

5. Return to the Lambda **Code** tab and replace the default code with the Python script from the Colab notebook. Click **Deploy**.

![Lambda code deployed](/images/5-Workshop/5.4/4.h.LBD.png)

> **Note:** The PDF references a Colab notebook for the Lambda code. Replace the sample ARN placeholder on line 11 with your actual SNS topic ARN in section 5.7.

### Step 2: Create EventBridge Rule

1. Open **Amazon EventBridge** → **Rules** → **Create rule**.
   - **Name:** `GuardDuty-To-Lambda-Block`
   - **Rule type:** **Rule with an event pattern**

![Create EventBridge rule](/images/5-Workshop/5.4/4.i.LBD.EB.png)

![Rule type](/images/5-Workshop/5.4/4.j.LBD.EB.png)

2. Click **Next**. Under **Event source**, choose **AWS services**.
   - **AWS service:** **GuardDuty**

![Event source GuardDuty](/images/5-Workshop/5.4/4.k.LBD.EB.png)

   - **Event type:** **GuardDuty Finding**

3. Click **Next**. Under **Select target(s)**:
   - **Target:** **Lambda function**
   - **Function:** `Minecraft-Automated-Block-IP`

![Select Lambda target](/images/5-Workshop/5.4/4.l.LBD.EB.png)

4. Click **Next** through remaining steps and create the rule.

![Rule created](/images/5-Workshop/5.4/4.m.LBD.EB.png)

### Result

When GuardDuty detects a threat, EventBridge triggers Lambda, which automatically revokes access from the attacker IP in the Security Group and sends an alert notification.
