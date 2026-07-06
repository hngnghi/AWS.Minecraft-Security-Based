---
title: "Worklog Week 1"
date: 2026-04-17
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:
* Master the AWS Free Tier policies, the $200 credit promotional program, and successfully complete the account registration process.
* Proactively establish a cost control and protection strategy for the account starting from day one.
* Document personal lessons learned regarding common misconfigurations that can lead to credit depletion or unexpected charges.

### Planned Tasks & Actual Progress:

| Day | Planned Task | Start Date | Completion Date | Tools & Documentation | Actual Results Achieved |
| :---: | :--- | :---: | :---: | :--- | :--- |
| **Mon** | - Explore the Free Tier package and its key updates<br>- Compare free tier vs. paid services<br>- Identify common mistakes that cause credit loss | 17/04/2026 | 17/04/2026 | AWS Free Tier Documentation, AWS Support | - Explored and oriented with the AWS service ecosystem.<br>- Clearly distinguished among the three types of offers: Always-free, 12-month free, and short-term trials.<br>- Successfully completed the “Explore AWS” program directly on the AWS Console Home interface. |
| **Tue** | - Create an AWS account<br>- Enable Multi-Factor Authentication (MFA)<br>- Document best practices for securing the root account | 18/04/2026 | 18/04/2026 | AWS Beginner Guide, AWS IAM | - Successfully registered a personal AWS account.<br>- Mastered the access management workflow and the principle of Least Privilege.<br>- Hand-on practice: Successfully assigned IAM Roles to an EC2 instance instead of using hardcoded access keys. |
| **Wed** | - List 5 milestone tasks to claim the full $200 credit<br>- Track task completion progress<br>- Establish a cost protection checklist | 19/04/2026 | 19/04/2026 | AWS Promotions Page, S3, DynamoDB | - Deployed foundational infrastructure: initialized an Amazon VPC virtual network and launched an Amazon EC2 virtual server.<br>- Configured an S3 Bucket, set up Public Read permissions, and successfully hosted a static website.<br>- Built a basic NoSQL database utilizing Amazon DynamoDB. |
| **Thu** | - Identify behaviors that could trigger credit suspension<br>- Learn how to enable cost alerts | 20/04/2026 | 21/04/2026 | AWS Billing Documentation, AWS Budgets | - Successfully configured the AWS Budgets tool to manage and control hands-on lab expenses.<br>- Set up automated budget alert thresholds to alleviate worries about forgetting to terminate resources. |
| **Fri** | - Research architecture patterns optimized for a $200 budget<br>- Understand cost monitoring and optimization concepts<br>- Review FAQs and chart the upcoming learning roadmap | 21/04/2026 | 21/04/2026 | Well-Architected Framework, AWS Cloud9, CLI | - Initialized and fully configured an AWS Cloud9 online development environment (Cloud IDE) via the browser.<br>- Attained proficiency in using the AWS CLI tool to interact with and inspect the resource status of S3 and DynamoDB. |

---

### Core Achievements of the Week:

* **Financial Management & Account Security:** Established an account protection guardrail using **AWS Budgets** and configured automated threshold alerts sent via Email. Gained a clear understanding of and distinguished among core administrative terms: *budget, usage report, billing alarm, and service quota*.
* **Foundational Cloud Infrastructure Deployment:** Successfully initialized an **EC2** virtual machine inside an **Amazon VPC** network subsystem, clarifying the structural differences between traditional on-premises servers and Cloud deployment models (IaaS, PaaS).
* **Storage & Databases:** Configured and operated **Amazon S3** object storage to handle static web hosting. Created tables and executed foundational data interaction actions (CRUD) on the NoSQL database engine **Amazon DynamoDB**.
* **Security & Automation:** Developed proficiency in leveraging the **AWS Cloud9** workspace combined with the **AWS CLI** to manage cloud resources via the command line. Maintained rigorous compliance with security standards via **AWS IAM** by attaching secure roles to EC2 instances, eliminating credential leak risks.

---

### Challenges & Lessons Learned:
* **The Challenge:** Transitioning to the NoSQL paradigm in DynamoDB—with its unique *Partition Key / Sort Key* structural mechanics—proved highly unfamiliar and contrasted sharply with the traditional relational database design and normalization patterns taught in university courses.
* **The Solution:** Conceptualized and mapped cloud services to familiar real-world comparisons (viewing EC2 as a personal virtual computer and S3 acting like Google Drive) to accelerate learning. Dedicated additional time to studying DynamoDB data modeling use cases to master data storage layouts optimized primarily around specific Query Patterns rather than multi-table joins.