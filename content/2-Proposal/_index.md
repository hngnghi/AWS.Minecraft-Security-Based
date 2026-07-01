# Project Proposal
## Minecraft Server Security Platform on AWS
### Automated Intrusion Detection and Incident Response Using AWS Services

---

# 1. Executive Summary

The **Minecraft Server Security Platform on AWS** is designed to demonstrate how Amazon Web Services (AWS) security services can be integrated to deploy a secure game server capable of detecting cyber threats and automatically responding to security incidents.

Rather than simply hosting a Minecraft server on Amazon EC2, the platform implements multiple layers of cloud-native security to protect against common attacks such as port scanning, SSH brute-force attempts, Distributed Denial-of-Service (DDoS) attacks, unauthorized access, and data loss.

The architecture follows the principles of **Cloud-native Security** and **Security Automation**, combining services including Amazon GuardDuty, Amazon EventBridge, AWS Lambda, AWS Backup, Amazon SNS, AWS Systems Manager Session Manager, and AWS Global Accelerator to build a lightweight Security Orchestration, Automation, and Response (SOAR) solution.

Beyond protecting a Minecraft server, this project also serves as an educational platform for students and cloud engineers to gain hands-on experience with AWS security services in a real-world environment.

---

# 2. Problem Statement

## Background

Public Minecraft servers are frequently targeted by various cyberattacks, including:

- Port scanning
- SSH brute-force attacks
- Distributed Denial-of-Service (DDoS)
- Server exploitation
- World data corruption
- Unauthorized administrative access

In addition, many administrators still rely on traditional SSH access using Key Pairs, increasing the risk of credential leakage and unauthorized access.

Without an automated monitoring and response mechanism, these attacks may lead to service disruption, data loss, and poor player experience.

## Proposed Solution

The proposed solution deploys a multi-layered security architecture on AWS with the following capabilities:

- Host the Minecraft server on Amazon EC2.
- Eliminate public SSH access by using AWS Systems Manager Session Manager.
- Continuously monitor suspicious activities with Amazon GuardDuty.
- Route security findings through Amazon EventBridge.
- Automatically trigger AWS Lambda to update Security Groups and block malicious IP addresses.
- Send real-time security notifications through Amazon SNS.
- Protect game data with scheduled backups using AWS Backup.
- Improve availability and hide the server's public IP using AWS Global Accelerator and Network Load Balancer.

---

# 3. Project Objectives

## Primary Objectives

- Deploy a secure Minecraft server on AWS.
- Build an automated intrusion detection and response system.
- Minimize manual intervention during security incidents.
- Protect game data while maximizing service availability.

## Secondary Objectives

- Gain practical experience with AWS security services.
- Demonstrate a lightweight SOAR architecture.
- Apply Zero Trust principles to cloud infrastructure.
- Develop a reusable cloud security reference architecture.

---

# 4. Solution Architecture

The platform adopts a multi-layered cloud architecture designed to maximize security, scalability, and automation.

![Architecture](/images/2-Proposal/Architecture.png)

## Architecture Overview

The architecture consists of three major functional workflows:

### 1. Traffic Routing & DDoS Mitigation

- Players connect to the Minecraft server through **AWS Global Accelerator** using TCP port 25565.
- **AWS Shield Standard** filters Layer 3 and Layer 4 network attacks.
- Clean traffic is forwarded to a **Network Load Balancer (NLB)** inside the VPC.
- The NLB routes traffic to the **Amazon EC2 Minecraft Server** running PaperMC.
- Administrative access is provided through **AWS Systems Manager Session Manager**, while SSH port 22 remains completely closed.

### 2. Security Automation (SOAR Workflow)

- VPC Flow Logs are analyzed by **Amazon GuardDuty**.
- GuardDuty generates security findings whenever suspicious activities are detected.
- Findings are forwarded to **Amazon EventBridge**.
- EventBridge triggers an **AWS Lambda** function.
- Lambda automatically updates the VPC Network ACL to block malicious IP addresses.
- Lambda also publishes emergency notifications through **Amazon SNS**, immediately alerting the administrator via email.

### 3. Disaster Recovery & Backup

- **AWS Backup** automatically creates hourly snapshots of the EC2 EBS volume.
- Backups are securely stored in an encrypted **Backup Vault**.
- Recovery points can be restored whenever data loss or server failures occur.

---

# AWS Services Used

| AWS Service | Purpose |
|--------------|----------|
| Amazon EC2 | Host the Minecraft server |
| Amazon VPC | Network isolation |
| Security Groups | Traffic filtering |
| Network ACL | Network-level protection |
| AWS IAM | Identity and access management |
| AWS Systems Manager Session Manager | Secure server administration without SSH |
| Amazon GuardDuty | Threat detection |
| Amazon EventBridge | Event routing |
| AWS Lambda | Automated incident response |
| Amazon SNS | Email notifications |
| AWS Backup | Automated backup |
| Backup Vault | Secure backup storage |
| AWS Global Accelerator | Hide public IP and improve availability |
| Network Load Balancer | TCP load balancing |
| Amazon CloudWatch | Monitoring and logging |
| AWS CloudTrail | Audit logging |

---

# 5. Technical Design

## Zero Trust Administration

The platform completely disables public SSH access.

Administrators manage the EC2 instance through **AWS Systems Manager Session Manager**, authenticated using IAM Roles.

### Benefits

- No SSH Key Pairs required.
- No Bastion Host required.
- Eliminates SSH brute-force attacks.
- Follows the Principle of Least Privilege.

---

## Threat Detection

Amazon GuardDuty continuously analyzes:

- VPC Flow Logs
- AWS CloudTrail Logs
- DNS Logs

Whenever suspicious behavior is identified, GuardDuty generates a Security Finding for further processing.

---

## Automated Incident Response

After a threat is detected, the workflow proceeds automatically:

```
- [5] An arrow labeled 'VPC Flow Logs' connects EC2 to 'Amazon GuardDuty' (Intrusion Detection).
- [6] 'Amazon GuardDuty' sends threat findings to 'Amazon EventBridge' (Event router).
- [7] 'Amazon EventBridge' triggers an 'AWS Lambda' function (with a small Python logo).
- [8] 'AWS Lambda' executes a script to update the 'VPC Network ACL', adding a 'DENY Attacker IP' rule at the subnet gateway.
- [9] Concurrently, 'AWS Lambda' triggers 'Amazon SNS' to send an emergency email notification (Email/Bell icon) to the administrator.
```

The entire response process is fully automated without requiring manual administrator intervention.

---

## Backup and Disaster Recovery

Minecraft world data is periodically backed up using AWS Backup.

All recovery points are stored inside an encrypted Backup Vault and can be restored quickly whenever data corruption or server failures occur.

---

# 6. Security Features

## Infrastructure Security

- Zero Trust Architecture
- Public SSH Disabled
- IAM Least Privilege
- Security Groups
- Network ACL

## Threat Detection

- Amazon GuardDuty
- Amazon CloudWatch
- AWS CloudTrail

## Automated Response

- Amazon EventBridge
- AWS Lambda
- Automatic IP Blocking
- Email Notifications

## High Availability

- AWS Global Accelerator
- Network Load Balancer

## Disaster Recovery

- AWS Backup
- Backup Vault
- Scheduled Backups
- Rapid Recovery

---

# 7. Implementation Plan

## Phase 1 – Architecture Design

- Requirement analysis
- AWS infrastructure design
- Security architecture planning

---

## Phase 2 – Infrastructure Deployment

- Amazon VPC
- Security Groups
- IAM Roles
- Amazon EC2

---

## Phase 3 – Minecraft Server Deployment

- Ubuntu Server
- Java Runtime
- PaperMC Server
- Session Manager configuration

---

## Phase 4 – Security Deployment

- Amazon GuardDuty
- Amazon EventBridge
- AWS Lambda
- Amazon SNS

---

## Phase 5 – High Availability Deployment

- Network Load Balancer
- AWS Global Accelerator

---

## Phase 6 – Backup Deployment

- AWS Backup
- Backup Vault
- Backup Plan

---

## Phase 7 – Testing

- Simulate security attacks
- Verify automated response
- Test email notifications
- Validate backup and recovery

---

# 8. Budget Estimation

The platform primarily utilizes AWS Free Tier services.

Expected operational costs mainly come from:

- Amazon EC2
- AWS Global Accelerator
- Network Load Balancer
- Amazon GuardDuty
- AWS Backup

Actual monthly costs depend on:

- EC2 running hours
- Network traffic
- Number of GuardDuty findings
- Backup storage size

The AWS Pricing Calculator can be used to estimate deployment costs before implementation.

---

# 9. Risk Assessment

| Risk | Impact | Mitigation |
|------|--------|------------|
| DDoS Attack | High | AWS Global Accelerator & AWS Shield Standard |
| SSH Brute Force | High | Disable Public SSH |
| Data Loss | High | AWS Backup |
| Unauthorized Access | Medium | IAM & Session Manager |
| Budget Overrun | Medium | AWS Budgets & Cost Explorer |

---

# 10. Expected Outcomes

## Technical Outcomes

- Successfully deploy a secure Minecraft server on AWS.
- Implement automated intrusion detection.
- Automatically respond to security incidents.
- Send real-time email alerts.
- Enable automated backup and disaster recovery.

## Educational Outcomes

- Gain practical experience with AWS Security services.
- Understand SOAR architecture.
- Learn modern cloud security best practices.
- Apply cloud security concepts in real-world projects.

---

# 11. Future Enhancements

Future improvements may include:

- AWS Security Hub
- Amazon Inspector
- AWS Config
- AWS Firewall Manager
- Amazon Route 53
- Amazon CloudFront
- Infrastructure as Code using AWS CDK or Terraform
- Grafana monitoring dashboard
- Discord Bot or Telegram Bot for real-time security notifications

---

# 12. Conclusion

The **Minecraft Server Security Platform on AWS** demonstrates how cloud-native AWS security services can be integrated to build a secure, automated, and resilient hosting environment for a Minecraft server.

By applying Zero Trust principles, Security Automation, and Disaster Recovery strategies, the platform enhances infrastructure security, minimizes operational risks, and improves service availability. In addition to serving as a production-ready reference architecture, it provides an effective hands-on learning environment for cloud security, AWS services, and cybersecurity best practices.