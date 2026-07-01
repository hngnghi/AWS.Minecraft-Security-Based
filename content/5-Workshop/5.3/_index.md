---
title: "Intrusion Detection (GuardDuty)"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

### Step 1: Enable Amazon GuardDuty

1. Search for **Amazon GuardDuty** in the AWS Console search bar.

![GuardDuty search](/images/5-Workshop/5.3/3.a.GD.png)

2. If this is your first time using it, simply click **Enable GuardDuty**.

3. GuardDuty immediately starts scanning and analyzing system logs and **VPC Flow Logs** to detect anomalies without slowing down your server.

![GuardDuty enabled](/images/5-Workshop/5.3/3.b.GD.png)

### Understanding GuardDuty

After enabling GuardDuty, you enter its management console. Pay attention to the left menu:

- **Findings:** Displays detected attacks or risky behavior, such as port scanning or password guessing. When the server is newly created, this list will be empty (`No findings`).
- **Lists:** Define trusted IPs or known malicious IP lists.
- **Settings:** Advanced configuration, and the most important area for live demos.
