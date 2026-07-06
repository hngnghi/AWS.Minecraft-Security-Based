---
title: "Worklog Week 3"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:
* Understand the AWS Support case management process and severity classification.
* Practice cloud data deployment with Amazon RDS and container deployment with Amazon Lightsail.

### Tasks & Progress:

| Day | Task | Date | Tools | Results Achieved |
| :---: | :--- | :---: | :--- | :--- |
| **Mon** | Compare AWS Support plans & research RDS. | 04/05/2026 | AWS Docs, Amazon RDS | Distinguished Developer/Business/Enterprise. Understood automated backup and Multi-AZ mechanisms of RDS. |
| **Tue** | Learn case severity classification & create RDS Instance. | 05/05/2026 | Support Center, RDS, Security Group | Successfully initialized RDS MySQL/SQL Server; configured Security Group to allow connections from local machine. |
| **Wed** | Open a sample support case & research Lightsail. | 06/05/2026 | Support Console, Lightsail | Successfully created a standard sample case. Quickly deployed a Lightsail virtual server using available templates. |
| **Thu** | Track, close sample case & learn Container concepts. | 07/05/2026 | Support Console, Docker | Learned about the case handling lifecycle. Understood the lightweight advantages of Containers compared to virtual machines. |
| **Fri** | Aggregate best practices & run Containerized application. | 08/05/2026 | Lightsail Containers, Billing | Successfully packaged and ran a public Containerized application on Lightsail; safely controlled budget and expenses. |

---

### Core Achievements:
* Mastered the workflow of opening, replying to, and closing support cases, and monitoring the system via AWS Health.
* Successfully deployed **Amazon RDS**, mastering the operational mindset of High Availability (Multi-AZ).
* Packaged applications into **Docker Containers** and ran them directly on the **Lightsail Containers** environment.

---

### Challenges & Lessons Learned:
* Encountered a *Connection Timeout* error when connecting to the Amazon RDS database from the outside.
* Correctly configured Inbound rules (opened ports 3306/1433) on the **VPC Security Group** and restricted IP access.