---
title: "Defense Demo (Sample Findings)"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

Because **GuardDuty** may take 5 to 15 minutes to analyze real logs, use **Sample Findings** for a smooth live demo without downtime.

1. In the **AWS Console**, go to **GuardDuty** → **Settings**.
2. Scroll down to **Generate sample findings** and click it. AWS will generate simulated attack logs, such as SSH brute force and port sweep.

![Generate sample findings](/images/5-Workshop/5.10/10.a.GD.png)

3. Immediately:
   - **EventBridge** captures the event.
   - **Lambda** runs the block-IP code.
   - Open the **CloudWatch Logs** of the Lambda function to show the log line: `"Phát hiện mối đe dọa... Đã thực thi chặn IP thành công"`.

![CloudWatch log](/images/5-Workshop/5.10/10.b.GD.png)

4. **Lambda** also invokes **Amazon SNS** and sends an email alert directly to the administrator's phone or inbox.

![Email/SMS alert](/images/5-Workshop/5.10/10.c.SMS.png)

{{% notice info %}}
**Demo tip:** Show the **CloudWatch Logs** and **email notification** together to prove the full SOAR loop: Detect → Auto block IP → Notify.
{{% /notice %}}
