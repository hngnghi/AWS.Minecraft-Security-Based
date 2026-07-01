---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# AWS + Minecraft + Cyber Security

**Minecraft Cyber Threat Detection & Automated Response** — Bảo mật Máy chủ Minecraft trên AWS.

#### Tổng quan

Workshop này biến một máy chủ Minecraft thông thường thành "pháo đài" bảo mật bằng các dịch vụ cốt lõi của **AWS**, tập trung vào **Giám sát (Monitoring)** và **Tự động xử lý sự cố (Incident Response)** khi server bị tấn công.

#### Cách thức hoạt động

- Host Minecraft server trên **Amazon EC2** (hoặc **AWS Fargate/ECS** để nâng cao kiến trúc).
- Thiết kế các lớp bảo mật chống lại tấn công phổ biến vào game server (DDoS, phá hoại dữ liệu, bruteforce SSH).
- Khi có tấn công thử nghiệm (quét port, Brute Force, exploit crash server), hệ thống **AWS** tự động phát hiện và ngăn chặn.

#### Các dịch vụ AWS sử dụng

| Dịch vụ | Mục đích |
|---------|----------|
| **Amazon EC2** / **ECS Fargate** | Chạy Minecraft Server |
| **AWS Global Accelerator** + **Network Load Balancer (NLB)** | Che giấu IP gốc EC2 và chống DDoS |
| **Amazon VPC**, **Security Groups**, **NACLs** | Chỉ mở cổng **25565**; chặn SSH port **22** — quản trị qua **AWS Systems Manager (SSM) Session Manager** |
| **AWS IAM** | Phân quyền nghiêm ngặt cho quản trị viên |
| **Amazon CloudWatch** & **AWS CloudTrail** | Giám sát log, phát hiện hành vi bất thường |
| **Amazon GuardDuty** | Phát hiện mối đe dọa đối với tài khoản AWS và EC2 |
| **Amazon EventBridge** | Nhận cảnh báo từ **GuardDuty** hoặc **CloudWatch Logs** |
| **AWS Lambda** | Tự động block IP tấn công; gửi cảnh báo qua **Amazon SNS** |
| **Amazon S3** & **AWS Backup** | Sao lưu world Minecraft mỗi giờ — Disaster Recovery |

{{% notice info %}}
**Lưu ý:** Lab này **không dùng AWS Shield Advanced** hay **AWS WAF** (hoặc **CloudFront**). Giải pháp chuẩn cho Minecraft TCP cổng **25565** (Tầng 4) là **Global Accelerator** + **NLB**.
{{% /notice %}}

#### Điểm nhấn bảo mật

- Bảo vệ server khỏi DDoS, che giấu IP thật qua **Load Balancer**
- Quản trị server không cần keypair / mở port SSH công cộng
- Demo mô hình **SOAR** thu nhỏ: Tấn công → Tự động block IP → Email cảnh báo "Ting ting"

#### Nội dung

1. [Tổng quan dự án & Chi phí](5.0/)
2. [Thiết lập mạng an toàn (VPC & Security Group)](5.1/)
3. [Triển khai Minecraft Server & Quản trị SSM](5.2/)
4. [Phát hiện xâm nhập (GuardDuty)](5.3/)
5. [Tự động phản ứng (Lambda & EventBridge)](5.4/)
6. [Sao lưu thảm họa (AWS Backup)](5.5/)
7. [Che giấu IP & chống DDoS (Global Accelerator + NLB)](5.6/)
8. [Thông báo Email (SNS)](5.7/)
9. [Quy trình bật server hoàn chỉnh](5.8/)
10. [Quy trình tắt server an toàn](5.9/)
11. [Demo phòng thủ (Sample Findings)](5.10/)
12. [Dọn dẹp tài nguyên](5.11/)
