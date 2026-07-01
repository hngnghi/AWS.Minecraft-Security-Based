---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# AWS + Minecraft + Cyber Security

**Minecraft Cyber Threat Detection & Automated Response** — Securing a Minecraft Server on AWS.

#### Overview

This workshop transforms a standard Minecraft server into a security-hardened environment using core **AWS** services. The focus is on **Monitoring** and **Automated Incident Response** when the server is under attack.

#### How It Works

- Host a Minecraft server on **Amazon EC2** (or **AWS Fargate/ECS** for advanced architecture).
- Design security layers to defend against common game-server attacks (DDoS, data griefing, SSH brute force).
- When simulated attacks occur (port scanning, brute force, or crash exploits), the **AWS** system automatically detects and blocks them.

#### AWS Services Used

| Service | Purpose |
|---------|---------|
| **Amazon EC2** / **ECS Fargate** | Run the Minecraft server |
| **AWS Global Accelerator** + **Network Load Balancer (NLB)** | Hide the EC2 origin IP and mitigate DDoS |
| **Amazon VPC**, **Security Groups**, **NACLs** | Open only port **25565**; block SSH port **22** — admin access via **AWS Systems Manager (SSM) Session Manager** only |
| **AWS IAM** | Strict permissions for server administrators |
| **Amazon CloudWatch** & **AWS CloudTrail** | Monitor logs and detect abnormal behavior |
| **Amazon GuardDuty** | Detect threats against the AWS account and EC2 instance |
| **Amazon EventBridge** | Receive alerts from **GuardDuty** or **CloudWatch Logs** |
| **AWS Lambda** | Auto-modify security rules to block attacker IPs; send alerts via **Amazon SNS** |
| **Amazon S3** & **AWS Backup** | Hourly world-data backups for disaster recovery |

{{% notice info %}}
**Note:** This lab intentionally does **not** use **AWS Shield Advanced** or **AWS WAF** (or **CloudFront**) for application-layer protection. **Global Accelerator** + **NLB** is the standard TCP (Layer 4) approach for Minecraft port **25565**.
{{% /notice %}}

#### Security Highlights

- DDoS mitigation and real IP concealment via **Global Accelerator** / **Load Balancer**
- Server administration without key pairs or public SSH
- Mini **SOAR** (Security Orchestration, Automation, and Response) demo: Attack → Auto block IP → Email alert

#### Content

1. [Project Overview & Cost](5.0/)
2. [Secure Network Setup (VPC & Security Group)](5.1/)
3. [Deploy Minecraft Server & SSM Administration](5.2/)
4. [Intrusion Detection (GuardDuty)](5.3/)
5. [Automated Response (Lambda & EventBridge)](5.4/)
6. [Disaster Recovery Backup (AWS Backup)](5.5/)
7. [Hide Real IP & DDoS Protection (Global Accelerator + NLB)](5.6/)
8. [Email Notifications (SNS)](5.7/)
9. [Complete Server Startup Procedure](5.8/)
10. [Safe Server Shutdown Procedure](5.9/)
11. [Defense Demo (Sample Findings)](5.10/)
12. [Resource Cleanup](5.11/)
