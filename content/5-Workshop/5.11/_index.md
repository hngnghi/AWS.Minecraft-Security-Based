---
title: "Resource Cleanup"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---

Cleaning up AWS resources after the lab is essential to avoid unexpected charges after the Free Tier period.

Because the services are linked together, delete them in the following reverse order to avoid dependency errors.

### Step 1: Delete AWS Global Accelerator & Network Load Balancer

These services are outermost and billed by the hour, so delete them first:

1. Go to **AWS Global Accelerator** → select `Minecraft-Accelerator` → click **Edit** → change status to **Disabled**. Wait about 1 minute, select it, and click **Delete**.

![Disable accelerator](/images/5-Workshop/5.11/11.a.Delete.png)

![Delete accelerator](/images/5-Workshop/5.11/11.b.Delete.png)

2. Go to **EC2** → **Load Balancers** → select `Minecraft-NLB` → **Actions** → **Delete**.

![Delete NLB](/images/5-Workshop/5.11/11.c.Delete.png)

3. In the EC2 left menu, choose **Target Groups** → select `Minecraft-TG` → **Actions** → **Delete**.

![Delete target group](/images/5-Workshop/5.11/11.d.Delete.png)

### Step 2: Terminate Minecraft EC2

1. Go to **EC2** → **Instances**.
2. Select `Minecraft-Secure-Server`.
3. Click **Instance state** → choose **Terminate instance**. This permanently deletes the instance and its EBS volumes.

{{% notice warning %}}
Do **not** choose **Stop instance** here. You must choose **Terminate instance** to fully remove the server.
{{% /notice %}}

![Terminate instance](/images/5-Workshop/5.11/11.e.Delete.png)

### Step 3: Delete Lambda & EventBridge Rule

1. Go to **Lambda** → select `Minecraft-Automated-Block-IP` → **Actions** → **Delete**.

![Delete Lambda](/images/5-Workshop/5.11/11.f.Delete.png)

2. Go to **Amazon EventBridge** → **Rules** → select the GuardDuty-to-Lambda rule → **Delete**.

![Delete EventBridge rule](/images/5-Workshop/5.11/11.g.Delete.png)

### Step 4: Delete SNS Topic

1. Go to **Simple Notification Service (SNS)** → **Subscriptions** → select your email subscription → **Delete**.
2. Choose **Topics** → select `Minecraft-Attack-Alerts` → **Delete**.

![Delete SNS topic](/images/5-Workshop/5.11/11.h.Delete.png)

### Step 5: Disable Amazon GuardDuty

GuardDuty charges for analyzed log volume, so disable it when no longer needed:

1. Go to **Amazon GuardDuty**.
2. In the left menu, choose **Settings**.

![GuardDuty settings](/images/5-Workshop/5.11/11.i.Delete.png)

3. Scroll to **Disable GuardDuty** and click **Disable** to remove all configuration data and stop billing.

### Step 6: Delete AWS Backup Recovery Points

1. Go to **AWS Backup** → **Backup vaults**.
2. Open `Minecraft-Secure-Vault`.
3. Select all recovery points → **Actions** → **Delete** each one.

![Delete recovery points](/images/5-Workshop/5.11/11.j.Delete.png)

4. After the vault is empty, return to **Backup vaults**, select the vault, and click **Delete**.
5. In the left menu, choose **Backup plans**, select the hourly plan, and click **Delete**.

![Delete backup plan](/images/5-Workshop/5.11/11.k.Delete.png)

### Step 7: Reset Network ACL Rules

If needed, restore the VPC Network ACL to its default state:

1. Go to **VPC** → **Network ACLs**.
2. Select the ACL used by your VPC → **Inbound rules** → **Edit inbound rules**.
3. Delete rule number `50`, which Lambda created automatically → **Save changes**.

![Reset NACL](/images/5-Workshop/5.11/11.l.Delete.png)

### Final Verification

After cleanup, open **AWS Billing** → **Dashboard** and verify that no services are still running. If you followed all 7 steps, your AWS account should return to a safe, idle state with no ongoing charges.
