---
title: "Worklog Tuần 7"
date: 2026-05-29
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:
* Hiểu và cấu hình IAM Role cho EC2 để thay thế access key dài hạn.
* Thực hành các giải pháp dịch chuyển hệ thống (Migration), sao lưu dự phòng (Disaster Recovery) và quản lý chi phí (FinOps).

### Công việc & Tiến độ:

| Thứ | Công việc | Ngày chạy | Công cụ | Kết quả đạt được |
| :---: | :--- | :---: | :--- | :--- |
| **2** | Nghiên cứu rủi ro Access Key & dịch chuyển máy ảo (VM). | 01/06/2026 | AWS VM Import/Export, AWS CLI | Phân biệt rõ rủi ro của key cố định và lợi ích của Role. Chuyển đổi thành công máy ảo cục bộ thành AMI để chạy trên EC2. |
| **3** | Tạo IAM Role cho EC2 & dịch chuyển cơ sở dữ liệu. | 02/06/2026 | AWS DMS, AWS SCT, SQL Server | Gắn quyền truy cập S3 và cấu hình trust policy cho Role. Dùng SCT và DMS chuyển đổi cấu trúc bảng, dịch chuyển dữ liệu sang RDS. |
| **4** | Gắn Role vào EC2 & thiết lập sao lưu liên tục. | 03/06/2026 | AWS Elastic DR, Instance Metadata | Kiểm tra temporary credentials thành công qua instance metadata. Hệ thống tự động cấu hình dự phòng sang Region khác. |
| **5** | Kiểm tra quyền đọc/ghi S3 & lập phương án tối ưu chi phí. | 04/06/2026 | AWS Cost Explorer, AWS Billing | EC2 truy cập S3 mượt mà không cần dùng key hardcode. Đề xuất gói Savings Plans và Reserved Instances giúp giảm chi phí máy chủ. |
| **6** | Tổng hợp best practices IAM & phân tích dữ liệu hóa đơn thô. | 05/06/2026 | AWS Glue, Amazon Athena, SQL | Nắm quy trình dọn dẹp và quản lý an toàn cho Role. Dùng Glue và Athena tạo pipeline không máy chủ để viết SQL tách chi phí theo thẻ. |

---

### Kết quả:
* Hiểu rõ tại sao nên dùng IAM role thay vì access key dài hạn.
* Tạo và gắn IAM role vào EC2 thành công.
* Truy cập tài nguyên AWS từ EC2 mà không dùng credential hardcode.
* Kiểm tra hành vi temporary credential qua instance metadata.
* Ghi nhận best practices khi dùng role cho EC2.
