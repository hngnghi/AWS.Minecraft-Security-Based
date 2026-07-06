---
title: "Worklog Tuần 1"
date: 2026-04-17
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:
* Nắm vững các chính sách của gói Free Tier, chương trình nhận $200 credit và quy trình đăng ký tài khoản thành công.
* Chủ động kiểm soát và bảo vệ chi phí tài khoản ngay từ tuần đầu tiên.
* Ghi chép lại bài học cá nhân về các hành vi cấu hình sai dễ gây mất credit hoặc phát sinh chi phí ngoài ý muốn.

### Các công việc triển khai và Tiến độ thực tế:

| Thứ | Công việc theo kế hoạch | Ngày bắt đầu | Ngày hoàn thành | Công cụ & Tài liệu | Kết quả thực tế đạt được |
| :---: | :--- | :---: | :---: | :--- | :--- |
| **2** | - Tìm hiểu gói Free Tier và thay đổi chính<br>- So sánh gói miễn phí với trả phí<br>- Xác định các lỗi gây mất credit | 17/04/2026 | 17/04/2026 | Tài liệu AWS Free Tier, AWS Support | - Khám phá và định hướng hệ sinh thái dịch vụ AWS.<br>- Phân biệt rõ các loại ưu đãi: Always-free, 12-month free và short-term trial.<br>- Hoàn thành chương trình “Explore AWS” ngay trên giao diện AWS Console Home. |
| **3** | - Tạo tài khoản AWS<br>- Bật Multi-Factor Authentication (MFA)<br>- Ghi nhận nguyên tắc bảo vệ tài khoản root | 18/04/2026 | 18/04/2026 | Hướng dẫn AWS beginner, AWS IAM | - Đăng ký thành công tài khoản AWS cá nhân.<br>- Nắm vững luồng phân quyền và nguyên tắc bảo mật đặc quyền tối thiểu (Least Privilege).<br>- Thực hành gán thành công IAM Roles cho máy chủ EC2 thay vì sử dụng access key trực tiếp. |
| **4** | - Liệt kê 5 nhiệm vụ để nhận đủ $200<br>- Ghi nhận tiến độ hoàn thành nhiệm vụ<br>- Lập checklist bảo vệ chi phí | 19/04/2026 | 19/04/2026 | Trang promotions AWS, S3, DynamoDB | - Triển khai kiến trúc hạ tầng cơ bản: khởi tạo mạng ảo Amazon VPC và máy chủ ảo Amazon EC2.<br>- Cấu hình thành công S3 Bucket, phân quyền Public Read và host thành công một trang Website tĩnh (Static Website).<br>- Xây dựng cơ sở dữ liệu NoSQL cơ bản trên nền tảng Amazon DynamoDB. |
| **5** | - Xác định các hành vi khiến credit bị khóa<br>- Tìm hiểu cách bật cảnh báo chi phí | 20/04/2026 | 21/04/2026 | Tài liệu AWS Billing, AWS Budgets | - Thiết lập thành công công cụ AWS Budgets để kiểm soát tài chính thực hành.<br>- Cấu hình các hạn mức cảnh báo ngân sách tự động nhằm giải tỏa tâm lý lo ngại việc quên tắt tài nguyên gây phát sinh chi phí. |
| **6** | - Tìm hiểu mẫu kiến trúc phù hợp mức $200<br>- Nắm khái niệm giám sát/tối ưu chi phí<br>- Ôn FAQ và lộ trình học tiếp theo | 21/04/2026 | 21/04/2026 | Well-Architected Framework, AWS Cloud9, CLI | - Khởi tạo và cấu hình hoàn chỉnh môi trường lập trình trực tuyến AWS Cloud9 (Cloud IDE) trên trình duyệt.<br>- Sử dụng công cụ AWS CLI để tương tác, kiểm tra trạng thái tài nguyên S3 và DynamoDB. |

---

### Kết quả đạt được trong tuần:

* **Quản lý tài chính & An toàn tài khoản:** Thiết lập hệ thống bảo vệ tài khoản thông qua **AWS Budgets**, cấu hình các mốc cảnh báo chi phí tự động qua Email. Nắm rõ định nghĩa và phân biệt được các thuật ngữ quản trị: *budget, usage report, billing alarm, service quota*.
* **Triển khai hạ tầng đám mây cơ bản:** Thực hành khởi tạo thành công máy chủ ảo **EC2** nằm trong phân lớp mạng **VPC**, hiểu rõ sự khác biệt giữa mô hình máy chủ On-premise truyền thống và hạ tầng Cloud (IaaS, PaaS).
* **Lưu trữ & Cơ sở dữ liệu:** Cấu hình và vận hành thành công dịch vụ lưu trữ đối tượng **Amazon S3** để phục vụ hosting website. Tạo lập bảng và thực thi các câu lệnh tương tác dữ liệu cơ bản trên cơ sở dữ liệu NoSQL **Amazon DynamoDB**.
* **Bảo mật & Tự động hóa:** Ứng dụng thành thạo môi trường **AWS Cloud9** kết hợp công cụ **AWS CLI** để quản trị tài nguyên bằng dòng lệnh. Tuân thủ nguyên tắc bảo mật thông qua **AWS IAM**, thực hiện gán Role an toàn cho EC2 để loại bỏ rủi ro lộ lọt Access Key.

---

### Khó khăn & Bài học kinh nghiệm:
* **Khó khăn:** Khái niệm cơ sở dữ liệu phi quan hệ (NoSQL) của DynamoDB với cấu trúc cặp khóa *Partition Key / Sort Key* hoàn toàn mới và khác với tư duy thiết kế, chuẩn hóa dữ liệu của hệ quản trị CSDL quan hệ truyền thống học ở trường.
* **Cách giải quyết:** Hệ thống hóa lại các dịch vụ bằng cách liên hệ thực tế gần gũi (EC2 tương tự máy tính ảo cá nhân, S3 đóng vai trò như Google Drive) để nhanh chóng tiếp thu. Dành thời gian nghiên cứu các tài liệu thiết kế Use Case của DynamoDB để hiểu tư duy lưu trữ dữ liệu tập trung theo hướng tối ưu hóa mẫu truy vấn.
