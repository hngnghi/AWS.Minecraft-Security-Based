---
title: "Worklog Week 7"
date: 2026-05-29
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:
* Understand and configure IAM Roles for EC2 to replace long-term access keys.
* Practice system migration solutions, disaster recovery (Disaster Recovery), and cost management (FinOps).

### Tasks & Progress:

| Day | Task | Date | Tools | Results Achieved |
| :---: | :--- | :---: | :--- | :--- |
| **Mon** | Research Access Key risks & virtual machine (VM) migration. | 01/06/2026 | AWS VM Import/Export, AWS CLI | Clearly distinguished the risks of static keys and the benefits of Roles. Successfully converted a local virtual machine into an AMI to run on EC2. |
| **Tue** | Create IAM Role for EC2 & migrate database. | 02/06/2026 | AWS DMS, AWS SCT, SQL Server | Attached S3 access permissions and configured trust policy for the Role. Used SCT and DMS to convert table structures and migrate data to RDS. |
| **Wed** | Attach Role to EC2 & set up continuous backup. | 03/06/2026 | AWS Elastic DR, Instance Metadata | Successfully verified temporary credentials via instance metadata. The system automatically configured disaster recovery to another Region. |
| **Thu** | Test S3 read/write permissions & create cost optimization plan. | 04/06/2026 | AWS Cost Explorer, AWS Billing | EC2 accessed S3 smoothly without using hardcoded keys. Proposed Savings Plans and Reserved Instances packages to reduce server costs. |
| **Fri** | Aggregate IAM best practices & analyze raw billing data. | 05/06/2026 | AWS Glue, Amazon Athena, SQL | Mastered the safe cleanup and management process for Roles. Used Glue and Athena to create a serverless pipeline to write SQL for separating costs by tags. |

---

### Core Achievements:
* Clearly understood why IAM roles should be used instead of long-term access keys.
* Successfully created and attached IAM roles to EC2.
* Accessed AWS resources from EC2 without using hardcoded credentials.
* Verified temporary credential behavior via instance metadata.
* Documented best practices when using roles for EC2.