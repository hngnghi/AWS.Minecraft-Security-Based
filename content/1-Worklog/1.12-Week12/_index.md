---
title: "Week 12 Worklog"
date: 2026-07-03
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objectives

* Complete security automation and alerting for the graduation project.
* Finalize safe startup and shutdown workflows for Minecraft.
* Run end-to-end validation, demo the SOAR flow, clean up AWS resources, and finalize report materials.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | ---------- | --------------- | ----------------------------------------- |
| 2 | - Create SNS topic `Minecraft-Attack-Alerts`<br>- Confirm email subscription<br>- Grant Lambda permission to publish to SNS | 03/07/2026 | 03/07/2026 | AWS SNS documentation |
| 3 | - Update Lambda code with SNS topic ARN<br>- Deploy the updated function<br>- Review published message format | 04/07/2026 | 04/07/2026 | Lambda deployment notes |
| 4 | - Write a safe Minecraft startup script<br>- Verify `screen -ls` and log files<br>- Test restart behavior | 05/07/2026 | 05/07/2026 | Minecraft operations notes |
| 5 | - Write a safe shutdown script<br>- Verify world save behavior<br>- Document graceful stop steps | 06/07/2026 | 07/07/2026 | Linux service best practices |
| 6 | - Run GuardDuty sample findings<br>- Check CloudWatch Logs and email alerts<br>- Execute the full cleanup sequence<br>- Review AWS Billing Dashboard | 07/07/2026 | 10/07/2026 | Project cleanup checklist |

### Week 12 Achievements

* Completed the alerting path: GuardDuty finding, Lambda automation, and SNS email notification.
* Validated startup and shutdown scripts for the Minecraft server.
* Demonstrated the end-to-end SOAR flow: attack detection, IP blocking, and alert notification.
* Cleaned up AWS resources in the correct dependency order.
* Confirmed no unexpected charges remain in AWS Billing.
* Prepared final bilingual Markdown documentation and graduation report.