---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# MINECRAFT CYBER SECURITY ON AWS: DON'T JUST OPEN SECURITY GROUPS — AUTOMATE INCIDENT RESPONSE (SOAR FOR GAME SERVERS)

When deploying service hosts such as a Minecraft Server on AWS, many teams usually start by creating a few Security Groups to allow inbound connections (such as TCP port 25565) and restrict access by IP address.

However, the real challenge is not getting the server online—it is maintaining and protecting the infrastructure against Layer 3/4 DDoS attacks, brute-force attempts, and continuous port-scanning activities from attackers once the server's public IP address is exposed to the Internet.

To address this challenge, my project goes beyond static security configurations by implementing an automated Security Orchestration, Automation, and Response (SOAR) solution that combines multiple layers of protection from AWS Edge Locations all the way down to the EC2 instance.

---

## KEY FEATURES OF THE SOLUTION

### Hide the Origin IP and Mitigate DDoS with AWS Global Accelerator & AWS Shield

Minecraft uses a custom Layer 4 TCP protocol, meaning AWS WAF cannot be used to protect the game server.

Instead, the solution provisions two global Anycast static IP addresses through **AWS Global Accelerator**, which is integrated with **AWS Shield Standard** at AWS edge locations. This architecture absorbs and filters Layer 3/4 DDoS traffic such as SYN Floods and UDP Amplification attacks before forwarding only clean traffic to the **Network Load Balancer (NLB)**.

As a result, the real public IP address of the EC2 instance remains completely hidden.

### Zero-Trust Management by Completely Closing SSH Access

To eliminate the risk of unauthorized administrative access, **SSH (Port 22)** is completely closed to the public Internet.

Administrators connect securely through **AWS Systems Manager (SSM) Session Manager**, which provides an encrypted management channel without exposing any management ports.

### Amazon GuardDuty Intrusion Detection

Instead of relying on manual monitoring, **Amazon GuardDuty** continuously analyzes **VPC Flow Logs** from the EC2 instance to identify suspicious activities such as:

- Port scanning
- Brute-force attempts
- Other anomalous behaviors

### Automated Response with AWS Lambda and Amazon EventBridge (SOAR Loop)

As soon as GuardDuty detects a security finding, **Amazon EventBridge** immediately captures the event in real time and invokes an **AWS Lambda (Python)** function.

The Lambda function automatically extracts the attacker's source IP address.

### Real-Time Network Isolation Using Network ACL

Instead of requiring manual intervention, Lambda writes a **DENY /32 rule** directly into the **VPC Network ACL** at the subnet boundary.

The attacker is completely isolated from the infrastructure within seconds.

### "Ting Ting" Alert Notifications via Amazon SNS

At the same time the attacker is blocked, Lambda calls **Amazon SNS** to send an emergency email notification containing:

- Source IP
- Attack type
- Severity level

The notification is delivered directly to the administrator's mobile device, enabling immediate visibility into the incident.

### Automated Disaster Recovery with AWS Backup

Independent of the network security workflow, an **AWS Backup Plan** automatically creates encrypted **Amazon EBS snapshots every hour** and stores them securely inside an isolated **Backup Vault**.

If the server experiences data destruction or griefing, the system can be restored with an hourly **Recovery Point Objective (RPO)**, depending on the backup configuration.

---

## CONCLUSION

What I find most interesting about this architecture is that it demonstrates an important approach to cloud security:

**System security should not be treated as a collection of Security Group rules that are configured once and then forgotten.**

An effective security architecture should continuously provide:

- Continuous Monitoring
- Real-time Threat Detection
- Automated Incident Response and Attacker Isolation
- Cyber Resilience through Automated Backup and Disaster Recovery

---

## FUTURE WORK

In my next blog, I will dive deeper into **Cost Optimization** for this architecture, because keeping **AWS Global Accelerator** and **Network Load Balancer** running 24/7 introduces a relatively high fixed operational cost for small and medium-sized projects.

Finding the right balance between **cost efficiency** and **security posture** will be the primary focus of the next article.

In my opinion, this topic has strong potential to generate discussion because many developers running systems or game servers on AWS still expose their EC2 public IP addresses directly and configure overly permissive Security Groups. Few have adopted an **event-driven security architecture** that combines **Amazon GuardDuty, EventBridge, AWS Lambda, and Network ACLs** to automatically isolate attackers in real time.

## Architecture Diagram:

![Architecture Diagram](/images/3-BlogsPosted/3.3-Blog3/ArchitectureBlog3.png)

## Related resources:

Report: https://docs.google.com/document/d/1gLwVqTCD2lwx72q6pu60ZA4vUM945DOM860uvY6uNTI/edit?usp=sharing

![Blog3](/images/3-BlogsPosted/3.3-Blog3/Blog3.png)