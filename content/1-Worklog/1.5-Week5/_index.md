---
title: "Worklog Week 5"
date: 2026-05-15
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:
* Build and secure a complete VPC network infrastructure.
* System administration via command line, database optimization, and advanced network connectivity.

### Tasks & Progress:

| Day | Task | Date | Tools | Results Achieved |
| :---: | :--- | :---: | :--- | :--- |
| **Mon** | Learn VPC, network security & install command line administration. | 18/05/2026 | AWS CLI, Amazon VPC | Successfully configured AWS CLI on local machine; wrote automation scripts to quickly create/delete resources. |
| **Tue** | Divide Public/Private network layers & design NoSQL database. | 19/05/2026 | VPC Console, DynamoDB | Established VPC cluster with Internet Gateway attached; created DynamoDB tables with standard Partition Key and Sort Key structures for querying. |
| **Wed** | Configure Route Table routing & deploy Cache system. | 20/05/2026 | NAT Gateway, ElastiCache (Redis) | Configured NAT Gateway for the Private network; successfully initialized a Redis cluster to accelerate data response times down to microseconds. |
| **Thu** | Set up Security Group, NACL & view network Workshop. | 21/05/2026 | Security Group, NACL, VPC Flow Logs | Activated VPC Flow Logs and Reachability Analyzer to inspect the network; visualized the entire complex network architecture. |
| **Fri** | Create EC2 to test connectivity & perform advanced network lab. | 22/05/2026 | Systems Manager, VPC Peering, CLI | Connected to EC2 via Session Manager (without SSH); successfully configured cross-region peering; ran scripts to automatically clean up all resources. |

---

### Core Achievements:
* Deployed a **VPC** network system including Public/Private Subnet, NAT Gateway, NACL, SG, and verified data flow paths using **Reachability Analyzer**.
* Leveraged **AWS CLI** to execute automation scripts; designed **DynamoDB** tables optimized for data analysis and integrated data caching.
* Connected to EC2 servers securely via **Session Manager** and cleaned up 100% of redundant resources automatically using CLI scripts to avoid costs.

---