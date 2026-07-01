---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# [PROJECT IN PROGRESS] CYBER SECURITY ON AWS: FROM AUTOMATED WAF TO A MACHINE LEARNING-BASED NETWORK INTRUSION DETECTION SYSTEM

While exploring Cyber Security on AWS, I had the opportunity to study and implement the **Security Automations for AWS WAF** solution. It is an interesting solution because it automatically detects, analyzes, and responds to attacks targeting web applications without requiring excessive manual intervention from the operations team.

What I appreciate most about this solution is its ability to integrate multiple AWS services into a complete security workflow. After studying and implementing this architecture, I realized that it is an excellent example of how AWS builds security solutions with automation and scalability in mind. However, what excites me even more is the next step beyond this solution.

---

## THE PROBLEM

Traditional Web Application Firewalls (WAFs) primarily rely on **Rule-Based Detection**. This approach is highly effective against known attack patterns, but it has significant limitations when dealing with new attack techniques, hybrid attacks, spoofed attacks, or abnormal behaviors that have never been seen before.

This led me to ask myself:

> **"Is it possible to build a system that can learn from network traffic and detect threats without having to predefine every single rule?"**

---

## THE SOLUTION

That is exactly why I am currently working on a project called **"Network Intrusion Detection System (NIDS) on AWS using Machine Learning."**

Instead of relying solely on predefined attack signatures, the system learns from network traffic data to distinguish between **normal** and **abnormal** behavior.

To achieve this, I am using the **CSE-CIC-IDS2018 on AWS** dataset, one of the most widely used datasets in network intrusion detection research.

This dataset was generated in an AWS environment and simulates a wide variety of real-world attacks, including:

- DDoS Attack
- DoS Attack
- Brute Force Attack
- Botnet Traffic
- Web Attacks
- Infiltration Attacks
- Reconnaissance Activities
- Other types of normal and malicious network traffic

Using this dataset, I will perform:

- Data preprocessing and cleaning.
- Feature extraction from network traffic.
- Machine Learning model training to classify normal and malicious traffic.
- Model evaluation using metrics such as Accuracy, Precision, Recall, and F1-Score.
- Deploying the model on AWS for real-time intrusion detection.

The architecture I am aiming for can be described as follows:

```text
Network Traffic
        ↓
Feature Extraction
        ↓
ML Model
        ↓
Threat Detection
        ↓
AWS Lambda
        ↓
AWS WAF / Security Group / SNS
```

In this architecture:

- Network traffic is collected and transformed into input features.
- The Machine Learning model evaluates the threat level of each network session or traffic flow.
- Once an attack is detected, AWS Lambda can automatically trigger response actions.
- These actions may include updating AWS WAF, blocking IP addresses through Security Groups, or sending notifications via Amazon SNS.

What I find particularly interesting is the combination of two different approaches:

### Rule-Based Detection

- Effective against known threats.
- Easy to implement and explain.
- Suitable for traditional security policies.

### Machine Learning-Based Detection

- Capable of detecting anomalous behavior.
- Better adaptability to emerging attack patterns.
- Reduces dependence on manually updating detection rules.

---

## CONCLUSION & FUTURE WORK

I believe that future network defense systems will no longer rely solely on static rules. Instead, they will increasingly integrate **Machine Learning** to improve their ability to detect and respond to increasingly sophisticated cyber threats.

For me, studying **Security Automations for AWS WAF** was the first step toward understanding how to build automated security mechanisms on AWS. The **Machine Learning-based NIDS project using the CSE-CIC-IDS2018 on AWS dataset** is the next step toward building intelligent intrusion detection systems that can continuously learn and adapt to real-world environments.

This is a research direction that I have been pursuing and will continue exploring in the future.

If you're interested in learning more, I'll be sharing the details at the upcoming **[HCM] Mini Meetup – First Cloud AI Journey | 06/06/2026**. See you there!

## Architecture Diagram

![Architecture Diagram](/images/3-BlogsPosted/3.2-Blog2/ArchitectureBlog2.png)

## RELATED RESOURCES

Repository GitHub: https://github.com/PeterHovng/HUTECH_DACN.CyberSecurity.AWS

Slide & Report: https://drive.google.com/.../1IA7GSU3iP9iwe09...

Video Demo: https://drive.google.com/.../1meqhF7-d0B_zZeQrG4mJTcT...

Source Code: https://drive.google.com/.../1qeoT3BBTsU3Tm8rSQ6Y4AXH83C7...

Dataset gốc: https://www.unb.ca/cic/datasets/ids-2018.html

![Blog2](/images/3-BlogsPosted/3.2-Blog2/Blog2.png)

---