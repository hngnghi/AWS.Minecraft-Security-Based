---
title: "Worklog Tuần 2"
date: 2026-04-24
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:
* Thực hành quản lý chi phí chuyên sâu với AWS Budgets, thiết lập các ngưỡng cảnh báo sử dụng thực tế.
* Phân biệt rõ các loại ngân sách: chi phí, sử dụng, RI và Savings Plans.
* Tiếp cận kiến trúc mạng nâng cao và các giải pháp xử lý, phân tích dữ liệu không máy chủ.
* Xây dựng và thực thi quy trình dọn dẹp tài nguyên định kỳ bảo vệ tài khoản.

### Các công việc triển khai và Tiến độ thực tế:

| Thứ | Công việc theo kế hoạch | Ngày bắt đầu | Ngày hoàn thành | Công cụ & Tài liệu | Kết quả thực tế đạt được |
| :---: | :--- | :---: | :---: | :--- | :--- |
| **2** | - Ôn tập ngân sách chi phí (Cost Budget).<br>- Tạo budget theo tháng & thiết lập ngưỡng cảnh báo.<br>- Ôn tập mạng đám mây và lỗi phân quyền IAM. | 24/04/2026 | 24/04/2026 | AWS Budgets, Amazon VPC, AWS IAM | - Tạo thành công Cost Budget theo tháng, cấu hình ngưỡng cảnh báo tự động qua email.<br>- Ôn tập VPC và IAM: hiểu rõ luồng đi của dữ liệu qua các lớp bảo mật vào máy chủ EC2. |
| **3** | - Tạo ngân sách sử dụng để theo dõi Free Tier.<br>- Xác định dịch vụ tiêu tốn nhiều nhất.<br>- Tìm hiểu điện toán không máy chủ. | 25/04/2026 | 25/04/2026 | AWS Cost Explorer, AWS Lambda, S3, Python | - Tạo thành công Usage Budget theo dõi mức tiêu thụ tài nguyên.<br>- Khởi tạo thành công Lambda Function, tích hợp trigger tự động thực thi mã khi có file upload lên S3 Bucket. |
| **4** | - Tìm hiểu khái niệm Reserved Instance (RI).<br>- Ghi nhận trường hợp thực tế nên áp dụng RI.<br>- Tìm hiểu mô hình Hồ dữ liệu (Data Lake). | 26/04/2026 | 26/04/2026 | Tài liệu AWS RI, Amazon Athena, AWS Glue | - Nắm vững trường hợp tối ưu chi phí bằng RI.<br>- Xây dựng kiến trúc Data Lake cơ bản: Dùng Glue Data Catalog tạo bảng, viết truy vấn SQL trên Athena để phân tích dữ liệu trực tiếp từ file CSV lưu ở S3. |
| **5** | - Tổng hợp Savings Plans và ngân sách liên quan.<br>- So sánh budget với chi phí thực tế.<br>- Ôn tập và chuyển đổi tư duy thiết kế NoSQL. | 27/04/2026 | 28/04/2026 | AWS Billing, Amazon DynamoDB | - Nắm cách theo dõi budget trên Billing Dashboard.<br>- Lập bảng so sánh đối chiếu hệ CSDL quan hệ với DynamoDB: Hiểu thêm về việc chuyển từ thiết kế theo thực thể sang hướng truy vấn. |
| **6** | - Sử dụng công cụ kiểm tra tài nguyên bị bỏ quên.<br>- Thực hiện dọn dẹp hệ thống để tránh phát sinh chi phí. | 28/04/2026 | 28/04/2026 | AWS Trusted Advisor, AWS Console | - Đối chiếu hệ thống với các khuyến nghị từ Trusted Advisor.<br>- Thực thi checklist dọn dẹp tài nguyên hàng tuần, đảm bảo tài khoản an toàn chi phí 100%. |

---

### Kết quả cốt lõi đạt được trong tuần:

* Cấu hình Cost/Usage Budget; tự động hóa cảnh báo chi phí qua email.
* Dùng Lambda xử lý file từ S3; truy vấn SQL dữ liệu thô bằng Athena.
* Dọn dẹp tài nguyên thừa hàng tuần theo Trusted Advisor, bảo toàn 100% chi phí.

---
