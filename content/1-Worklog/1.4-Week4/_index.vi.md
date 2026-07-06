---
title: "Worklog Tuần 4"
date: 2026-05-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:
* Quản trị phân quyền tài khoản theo nguyên tắc đặc quyền tối thiểu.
* Triển khai hệ thống Auto Scaling, CloudWatch và Hybrid DNS.

### Công việc & Tiến độ:

| Thứ | Công việc | Ngày chạy | Công cụ | Kết quả đạt được |
| :---: | :--- | :---: | :--- | :--- |
| **2** | Ôn tập IAM & nghiên cứu cơ chế mở rộng đàn hồi. | 11/05/2026 | AWS IAM, EC2 Launch Templates | Nắm rõ user/group/role/policy. Phân biệt Vertical và Horizontal Scaling; tạo thành công Launch Template chuẩn hóa cho máy chủ. |
| **3** | Cấu hình nhóm quản trị/vận hành & thiết lập Auto Scaling. | 12/05/2026 | IAM Console, EC2 Auto Scaling | Tạo user/group và phân quyền Least Privilege. Auto Scaling tự động sinh EC2 khi CPU > 70% và tự thu hồi khi tải giảm. |
| **4** | Kiểm tra quyền login & cấu hình giám sát hệ thống. | 13/05/2026 | AWS CLI, CloudWatch, Amazon SNS | Kiểm tra quyền truy cập Console/CLI; tạo Dashboard giám sát, nhận email cảnh báo thời gian thực khi ép tải CPU. |
| **5** | Tạo user vận hành đổi role & nghiên cứu kiến trúc mạng lai. | 14/05/2026 | IAM Role, Route 53, Amazon VPC | Thực hành đổi role kiểm soát phạm vi quyền. Hiểu cơ chế hoạt động của Route 53 Hosted Zones (Public/Private). |
| **6** | Kiểm tra dọn dẹp quyền IAM thừa & cấu hình Route 53 Resolver. | 15/05/2026 | Trusted Advisor, Route 53 Resolver, Draw.io | Thực thi checklist dọn dẹp IAM. Cấu hình Inbound/Outbound Endpoints nối thông DNS, phân giải tên miền chéo giữa mạng Local và VPC. |

---

### Kết quả đạt được tuần 4:

* Tạo được group và user cho vai trò quản trị, vận hành.
* Áp dụng phân quyền theo least privilege.
* Thực hành đổi role và xác định phạm quyền.
* Xây dựng checklist quản trị IAM.

---

