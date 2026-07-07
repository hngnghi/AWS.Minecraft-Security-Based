---
title: "Worklog Tuần 11"
date: 2026-06-26
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Objectives Week 11:
* Cooperate in researching, analyzing documents, and sketching advanced cloud security solutions for the graduation project.
* Support deploying foundational infrastructure (VPC, EC2) and configuring the security monitoring subsystem (GuardDuty, Lambda).

### Tasks Deployment and Actual Progress:

| Day | Planned Task | Start Date | Tools | Actual Result Achieved |
| :---: | :--- | :---: | :--- | :--- |
| **2** | Support researching documents & participate in sketching the overall architecture. | 26/06/2026 | Architecture design notes, Draw.io | Collected specifications of cloud infrastructure components and participated in sketching the overall architecture diagram for the Minecraft Server Security System on AWS project. |
| **3** | Cooperate in setting up the foundational secure network infrastructure. | 27/06/2026 | AWS VPC, Security Group | Set up foundational network parameters for the `Minecraft-Security-Lab` subsystem (VPC, Subnet, Route Table) and reviewed port closing/opening rules in the Security Group. |
| **4** | Support installing & configuring the server environment. | 28/06/2026 | Amazon EC2, Systems Manager | Launched Linux server on Amazon EC2, performed installation, configuration, and secure operation of Minecraft Server under a restricted system user via Session Manager. |
| **5** | Support configuring & analyzing alerts from the intrusion detection system. | 29/06/2026 | Amazon GuardDuty, EventBridge | Activated and monitored the Amazon GuardDuty system; analyzed and classified security alert categories (Findings) obtained from the test environment. |
| **6** | Participate in programming the response function & configuring the automation flow. | 30/06/2026 | AWS Lambda, Amazon EventBridge | Cooperated in writing and debugging the processing script for the AWS Lambda function (`Minecraft-Automated-Block-IP`) and tested the automated response flow to block malicious IP addresses. |

---

### Results Achieved Week 11:
* Completed the supporting role in analyzing documents and clarifying the cloud security architecture diagram for the project.
* Cooperated in successfully deploying the isolated network environment and configuring services on the secure EC2 server.
* Mastered the operational process, error classification of GuardDuty, and the automated trigger mechanism via EventBridge.