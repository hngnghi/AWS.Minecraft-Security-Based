---
title: "Worklog Tuần 5"
date: 2026-05-15
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:
* Xây dựng và bảo mật hạ tầng mạng VPC hoàn chỉnh.
* Quản trị hệ thống bằng dòng lệnh, tối ưu cơ sở dữ liệu và kết nối mạng nâng cao.

### Công việc & Tiến độ:

| Thứ | Công việc | Ngày chạy | Công cụ | Kết quả đạt được |
| :---: | :--- | :---: | :--- | :--- |
| **2** | Học VPC, bảo mật mạng & cài đặt dòng lệnh quản trị. | 18/05/2026 | AWS CLI, Amazon VPC | Cấu hình thành công AWS CLI trên máy cá nhân; viết script tự động hóa khởi tạo/xóa nhanh tài nguyên. |
| **3** | Phân chia lớp mạng Public/Private & thiết kế CSDL NoSQL. | 19/05/2026 | VPC Console, DynamoDB | Thiết lập cụm VPC gắn Internet Gateway; tạo bảng DynamoDB chuẩn cấu trúc Partition Key và Sort Key để truy vấn. |
| **4** | Cấu hình định tuyến Route Table & triển khai Bộ nhớ đệm. | 20/05/2026 | NAT Gateway, ElastiCache (Redis) | Cấu hình NAT Gateway cho mạng Private; khởi tạo thành công cụm Redis giúp tăng tốc độ phản hồi dữ liệu xuống mức micro-giây. |
| **5** | Thiết lập Security Group, NACL & xem Workshop mạng. | 21/05/2026 | Security Group, NACL, VPC Flow Logs | Kích hoạt VPC Flow Logs và Reachability Analyzer để kiểm tra mạng; trực quan hóa toàn bộ kiến trúc mạng phức tạp. |
| **6** | Tạo EC2 kiểm tra kết nối & làm bài thực hành mạng nâng cao. | 22/05/2026 | Systems Manager, VPC Peering, CLI | Kết nối EC2 qua Session Manager (không cần SSH); cấu hình thành công kết nối liên vùng; chạy script tự động dọn sạch tài nguyên. |

---

### Kết quả cốt lõi:
* Triển khai hệ thống mạng **VPC** gồm Public/Private Subnet, NAT Gateway, NACL, SG và kiểm tra đường đi luồng dữ liệu bằng **Reachability Analyzer**.
* Sử dụng **AWS CLI** để chạy script tự động hóa; thiết kế bảng **DynamoDB** tối ưu cho phân tích dữ liệu và tích hợp bộ nhớ đệm.
* Kết nối máy chủ EC2 an toàn qua **Session Manager** và dọn dẹp 100% tài nguyên thừa tự động bằng script CLI để tránh mất tiền.

---
