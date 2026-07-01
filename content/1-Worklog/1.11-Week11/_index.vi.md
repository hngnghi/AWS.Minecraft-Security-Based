---
title: "Worklog Tuần 11"
date: 2026-06-26
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Thiết kế kiến trúc AWS cho dự án tốt nghiệp: AWS + Minecraft + Cyber Security.
* Triển khai nền tảng: VPC, EC2, GuardDuty, Lambda, Backup, NLB và Global Accelerator.
* Đưa server Minecraft vào chế độ giám sát bảo mật cơ bản.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2 | - Xác định chi phí dự kiến<br>- Vẽ sơ đồ kiến trúc<br>- Liệt kê dịch vụ AWS cần dùng | 26/06/2026 | 26/06/2026 | Architecture design notes |
| 3 | - Tạo VPC `Minecraft-Security-Lab`<br>- Tạo subnet và route table<br>- Tạo SG chỉ mở port 25565 | 27/06/2026 | 27/06/2026 | Tài liệu AWS VPC |
| 4 | - Launch EC2 Ubuntu<br>- Cài Minecraft server qua Session Manager<br>- Chạy Minecraft bằng user `minecraft` | 28/06/2026 | 28/06/2026 | AWS Systems Manager docs |
| 5 | - Bật GuardDuty<br>- Xem findings, settings và logic cảnh báo<br>- Ghi nhận hành vi cần tự động chặn | 29/06/2026 | 30/06/2026 | Hướng dẫn AWS GuardDuty |
| 6 | - Tạo Lambda `Minecraft-Automated-Block-IP`<br>- Cấp quyền EC2<br>- Tạo EventBridge rule nối GuardDuty sang Lambda | 30/06/2026 | 30/06/2026 | Tài liệu AWS Lambda và EventBridge |

### Kết quả đạt được tuần 11:

* Thiết kế kiến trúc rõ ràng cho dự án tốt nghiệp.
* Triển khai VPC, EC2 và Minecraft server theo hướng bảo mật trước.
* Bật GuardDuty và nối với Lambda để chuẩn bị tự động hóa phản ứng.
* Tạo backup plan hàng giờ cho EC2.
* Mở khả năng truy cập qua Global Accelerator.