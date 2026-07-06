---
title: "Worklog Week 4"
date: 2026-05-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:
* Account permission management following the principle of least privilege.
* Deploy Auto Scaling system, CloudWatch, and Hybrid DNS.

### Planned Tasks & Actual Progress:

| Day | Planned Task | Start Date | Completion Date | Tools & Documentation | Actual Results Achieved |
| :---: | :--- | :---: | :---: | :--- | :--- |
| **Mon** | Review IAM & research cloud elasticity mechanisms. | 11/05/2026 | 11/05/2026 | AWS IAM, EC2 Launch Templates | Mastered user/group/role/policy. Distinguished Vertical and Horizontal Scaling; successfully created a standardized Launch Template for servers. |
| **Tue** | Configure admin/ops groups & set up Auto Scaling. | 12/05/2026 | 12/05/2026 | IAM Console, EC2 Auto Scaling | Created user/group and applied Least Privilege permissions. Auto Scaling automatically launches new EC2 instances when CPU > 70% and terminates them when load decreases. |
| **Wed** | Test login permissions & configure system monitoring. | 13/05/2026 | 13/05/2026 | AWS CLI, CloudWatch, Amazon SNS | Verified Console/CLI access permissions; built a monitoring Dashboard, received real-time email alerts during CPU stress testing. |
| **Thu** | Create ops user to switch roles & research hybrid network architecture. | 14/05/2026 | 14/05/2026 | IAM Role, Route 53, Amazon VPC | Handled role switching to control permission scopes. Understood the operational mechanics of Route 53 Hosted Zones (Public/Private). |
| **Fri** | Inspect and clean up redundant IAM permissions & configure Route 53 Resolver. | 15/05/2026 | 15/05/2026 | AWS Trusted Advisor, Route 53 Resolver, Draw.io | Executed the IAM cleanup checklist. Configured Inbound/Outbound Endpoints to connect DNS, resolving cross-domain names between the Local network and VPC. |

---

### Core Achievements:
* Created group and user for administrative and operational roles.
* Applied permission assignment following least privilege.
* Handled role switching and verified permission scopes.
* Built an IAM administration checklist.

---