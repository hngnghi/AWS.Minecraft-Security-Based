---
title: "Worklog Week 12"
date: 2026-07-03
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Objectives Week 12:
* Cooperate in finalizing the operational automation process, optimizing secure server management scripts, and cleaning up the test system.
* Comprehensively accept the attack detection cycle, complete bilingual technical documentation, and the final internship graduation report.

### Tasks Deployment and Actual Progress:

| Day | Planned Task | Start Date | Tools | Actual Result Achieved |
| :---: | :--- | :---: | :--- | :--- |
| **2** | Cooperate in setting up and authorizing the security alert infrastructure. | 03/07/2026 | Amazon SNS, AWS Lambda | Successfully configured SNS Topic (`Minecraft-Attack-Alerts`), verified email subscription list, and granted permissions for Lambda to publish alert notifications. |
| **3** | Update source code configuration and test message formatting. | 04/07/2026 | AWS Lambda, CloudWatch Logs | Integrated SNS ARN into Lambda source code, redeployed the function, and standardized the display data structure of notifications sent to email. |
| **4** | Support building a secure server startup script on Linux. | 05/07/2026 | Linux Screen, Amazon EC2 | Participated in writing and testing Startup Script for Minecraft Server, monitored session status (`screen -ls`) and system log files after activating restart mode. |
| **5** | Support building a secure server shutdown and data preservation script. | 06/07/2026 | Linux Bash Script, Minecraft Server | Participated in finalizing Shutdown Script, tested automated world save feature, and configured secure service stopping process. |
| **6** | Simulate attacks for SOAR cycle acceptance and resource decommissioning. | 07/07/2026 | Amazon GuardDuty, AWS Billing | Activated sample findings to test the automated malicious IP isolation flow; performed cleanup of all resources based on dependency order and verified 100% safe cost budget. |

---

### Results Achieved Week 12:
* Supported system operation optimization by completing secure startup and shutdown scripts, ensuring data integrity for Minecraft Server on Linux.
* Successfully accepted the SOAR cycle by activating simulated attack samples on GuardDuty to comprehensively test the detection, IP isolation, and automated alert sending flow.
* Completed technical documentation with bilingual Markdown files and finished the final graduation internship report on schedule.
* Decommissioned and cleanly wiped out all test resources on the AWS Console, confirming no unexpected costs incurred on the AWS Billing Dashboard.