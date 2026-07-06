---
title: "Worklog Week 2"
date: 2026-04-24
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:
* Practice advanced cost management with AWS Budgets, setting up practical usage alert thresholds.
* Clearly distinguish among different budget types: cost, usage, RI, and Savings Plans.
* Approach advanced networking architecture and serverless data processing and analytics solutions.
* Build and execute a routine resource cleanup workflow to safeguard the account.

### Planned Tasks & Actual Progress:

| Day | Planned Task | Start Date | Completion Date | Tools & Documentation | Actual Results Achieved |
| :---: | :--- | :---: | :---: | :--- | :--- |
| **Mon** | - Review Cost Budget concepts.<br>- Create a monthly budget & configure alert thresholds.<br>- Review cloud networking and basic IAM permission errors. | 24/04/2026 | 24/04/2026 | AWS Budgets, Amazon VPC, AWS IAM | - Successfully created a monthly Cost Budget and configured automated email alerts.<br>- Reviewed VPC and IAM: mastered the data flow through security layers into EC2 instances. |
| **Tue** | - Create a Usage Budget to track Free Tier usage.<br>- Identify the top cost-consuming services.<br>- Explore Serverless Computing. | 25/04/2026 | 25/04/2026 | AWS Cost Explorer, AWS Lambda, S3, Python | - Successfully created a Usage Budget to monitor resource consumption limits.<br>- Built a Lambda Function and integrated an automated trigger to execute code upon file uploads to an S3 Bucket. |
| **Wed** | - Research Reserved Instance (RI) concepts.<br>- Document real-world use cases for RIs.<br>- Study Data Lake architectures. | 26/04/2026 | 26/04/2026 | AWS RI Documentation, Amazon Athena, AWS Glue | - Mastered cost optimization strategies using RIs.<br>- Built a basic Data Lake: leveraged Glue Data Catalog to define tables and ran SQL queries in Athena to analyze raw CSV data in S3. |
| **Thu** | - Aggregate Savings Plans and corresponding budgets.<br>- Compare budget thresholds against actual spending.<br>- Review and transition to NoSQL design principles. | 27/04/2026 | 28/04/2026 | AWS Billing, Amazon DynamoDB | - Learned to track budgets on the Billing Dashboard.<br>- Mapped relational databases against DynamoDB: understood shifting from entity normalization to query-driven access patterns. |
| **Fri** | - Use tools to inspect forgotten or idle cloud resources.<br>- Execute system cleanup routines to eliminate unexpected charges. | 28/04/2026 | 28/04/2026 | AWS Trusted Advisor, AWS Console | - Evaluated the infrastructure against Trusted Advisor recommendations.<br>- Executed the weekly resource cleanup checklist, keeping the account 100% cost-safe. |

---

### Core Achievements:
* Configured Cost/Usage Budgets; automated cost alerts via email.
* Handled files from S3 using Lambda; queried raw data directly with SQL via Athena.
* Automated weekly cleanup of idle resources using Trusted Advisor, securing 100% budget efficiency.

---