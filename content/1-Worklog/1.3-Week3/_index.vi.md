---
title: "Worklog Tuần 3"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:
* Nắm quy trình quản lý AWS Support case và phân loại mức độ nghiêm trọng.
* Thực hành triển khai dữ liệu đám mây với Amazon RDS và container với Amazon Lightsail.

### Công việc & Tiến độ:

| Thứ | Công việc | Ngày chạy | Công cụ | Kết quả đạt được |
| :---: | :--- | :---: | :--- | :--- |
| **2** | So sánh gói AWS Support & nghiên cứu RDS. | 04/05/2026 | AWS Docs, Amazon RDS | Phân biệt Developer/Business/Enterprise. Hiểu cơ chế sao lưu tự động và Multi-AZ của RDS. |
| **3** | Học phân loại mức độ lỗi & tạo RDS Instance. | 05/05/2026 | Support Center, RDS, Security Group | Khởi tạo thành công RDS MySQL/SQL Server; mở cấu hình Security Group để kết nối từ máy cục bộ. |
| **4** | Mở một support case mẫu & nghiên cứu Lightsail. | 06/05/2026 | Support Console, Lightsail | Tạo thành công case mẫu đúng chuẩn. Triển khai nhanh máy chủ ảo Lightsail bằng template có sẵn. |
| **5** | Theo dõi, đóng case mẫu & học khái niệm Container. | 07/05/2026 | Support Console, Docker | Học thêm về vòng đời xử lý case. Nắm rõ ưu điểm gọn nhẹ của Container so với máy ảo. |
| **6** | Tổng hợp best practices & chạy ứng dụng Container. | 08/05/2026 | Lightsail Containers, Billing | Đóng gói và chạy thành công ứng dụng Container hóa public lên Lightsail; kiểm soát ví tiền an toàn. |

---

### Kết quả cốt lõi:
* Làm chủ luồng mở, phản hồi, đóng support case và theo dõi hệ thống qua AWS Health.
* Triển khai thành công **Amazon RDS**, nắm vững tư duy vận hành High Availability (Multi-AZ).
* Đóng gói ứng dụng dạng **Docker Container** và chạy trực tiếp trên môi trường **Lightsail Containers**.

---

### Khó khăn & Bài học:
* Gặp lỗi *Connection Timeout* khi kết nối từ bên ngoài vào cơ sở dữ liệu Amazon RDS.
* Cấu hình chính xác luật Inbound (mở port 3306/1433) trên **VPC Security Group** và giới hạn IP truy cập.