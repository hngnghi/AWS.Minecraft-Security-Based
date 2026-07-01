---
title: "Disaster Recovery Backup (AWS Backup)"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

### Step 1: Create Backup Vault

1. Search for **AWS Backup** and open the service.
2. In the left menu, choose **Backup vaults** → click **Create Backup vault**.

![Create backup vault](/images/5-Workshop/5.5/5.a.Backup.png)

3. Configure the vault:
   - **Backup vault name:** `Minecraft-Secure-Vault`
   - **Encryption key:** Keep the default `aws/backup` so AWS encrypts your backups automatically.

![Vault configuration](/images/5-Workshop/5.5/5.b.Backup.png)

4. Click **Create Backup vault**.

![Vault created](/images/5-Workshop/5.5/5.d.Backup.png)

### Step 2: Create Backup Plan

1. In the left menu, select **Backup plans** → click **Create Backup plan**.

![Create backup plan](/images/5-Workshop/5.5/5.e.Backup.png)

2. Choose **Build a new plan**.

3. **Backup plan details**:
   - **Backup plan name:** `Minecraft-DR-Plan`

![Plan details](/images/5-Workshop/5.5/5.f.Backup.png)

4. **Backup rule configuration**:
   - **Backup rule name:** `Hourly-Backup-Rule`
   - **Backup vault:** `Minecraft-Secure-Vault`
   - **Backup frequency:** `Hourly` to demonstrate an RPO under one hour
   - **Retention period:** `7` days

![Rule configuration](/images/5-Workshop/5.5/5.g.Backup.png)

![Retention period](/images/5-Workshop/5.5/5.h.Backup.png)

5. Click **Create plan**.

### Step 3: Assign Minecraft EC2 to the Backup Plan

1. After creating the plan, click **Assign resources**.

![Assign resources](/images/5-Workshop/5.5/5.i.Backup.png)

2. Configure resource assignment:
   - **Resource assignment name:** `Assign-Minecraft-EC2`
   - **IAM role:** Keep the default **Default role**
   - **Resource selection:** Choose **Include specific resource types**
   - **Select specific resource types:** Choose **EC2**, then select the exact `Minecraft-Secure-Server` instance ID

![Assign EC2](/images/5-Workshop/5.5/5.j.Backup.png)

3. Click **Assign resources**.

![Assignment complete](/images/5-Workshop/5.5/5.m.EC2.Minecraft.png)

![Backup overview](/images/5-Workshop/5.5/5.n.EC2.Minecraft.png)

![Backup status](/images/5-Workshop/5.5/5.o.EC2.Minecraft.png)

{{% notice info %}}
**Why this matters:** Hourly backups reduce maximum data loss to under one hour. Backups are encrypted in the vault, so even if EC2 is compromised, the backup remains protected.
{{% /notice %}}
