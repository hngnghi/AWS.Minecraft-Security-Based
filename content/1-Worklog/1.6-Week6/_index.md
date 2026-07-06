---
title: "Worklog Week 6"
date: 2026-05-22
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:
* Learn about EC2 servers, EBS storage, and AMIs.
* Practice CloudFront, Lambda@Edge, and Microsoft AD.

### Planned Tasks & Actual Progress:

| Day | Planned Task | Start Date | Completion Date | Tools & Documentation | Actual Results Achieved |
| :---: | :--- | :---: | :---: | :--- | :--- |
| **Mon** | Research instance types, EBS & configure content delivery network. | 25/05/2026 | 25/05/2026 | CloudFront, Amazon S3 | Distinguished volume types suitable for each workload. Initialized CloudFront Distribution, significantly reducing latency for static page loads from S3. |
| **Tue** | Launch EC2 servers & upgrade edge computing solution. | 26/05/2026 | 26/05/2026 | EC2 (Linux/Windows), Lambda@Edge | Ran Linux/Windows servers; wrote and integrated Lambda@Edge code (Node.js/Python) to process requests at the network edge to reduce load on the origin server. |
| **Wed** | Manage server lifecycle & deploy Windows Server. | 27/05/2026 | 27/05/2026 | EC2 lifecycle, AMI, RDP | Changed instance type, created EBS snapshots/custom AMIs. Successfully connected to Windows Server via RDP; understood the process of running ASP.NET Core MVC applications. |
| **Thu** | Practice server permission recovery & set up directory service. | 28/05/2026 | 28/05/2026 | AWS Managed Microsoft AD | Recovered Linux/Windows access permissions and configured RDP. Successfully initialized an Active Directory domain, managing centralized identity for servers. |
| **Fri** | Deploy Web application & aggregate cost control report. | 29/05/2026 | 29/05/2026 | IAM, AWS Billing | Successfully deployed web applications (LAMP/Node.js) on Linux. Understood IAM policies that restrict instance families, types, and EBS to optimize costs. |

---

### Core Achievements:

* Successfully managed EC2 Linux and Windows.
* Created snapshots, AMIs, and reused prepared resources.
* Practiced changing instance types and recovering access permissions.
* Deployed web applications on Linux.
* Understood IAM policies that restrict instance families, types, and EBS.

---