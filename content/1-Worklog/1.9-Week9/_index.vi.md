---
title: "Worklog Tuần 9"
date: 2026-06-12
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* Triển khai website tĩnh trên Amazon S3.
* Hiểu cách kiểm soát public access, object permission và website routing.
* Tối ưu truy cập với Amazon CloudFront.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2 | - Tìm hiểu static website hosting trên S3<br>- Hiểu public access block và ACL | 12/06/2026 | 12/06/2026 | Tài liệu AWS S3 |
| 3 | - Tạo bucket S3 cho static website<br>- Upload file website<br>- Bật website endpoint | 13/06/2026 | 13/06/2026 | AWS S3 console |
| 4 | - Cấu hình public access và bucket policy cẩn trọng<br>- Kiểm tra website endpoint | 14/06/2026 | 14/06/2026 | AWS security best practices |
| 5 | - Tạo CloudFront distribution<br>- Đặt bucket S3 làm origin<br>- Cấu hình cache behavior và root object | 15/06/2026 | 16/06/2026 | Hướng dẫn AWS CloudFront |
| 6 | - Bật versioning cho bucket<br>- Cấu hình replication đa region<br>- Ghi chú cleanup | 16/06/2026 | 16/06/2026 | Tài liệu AWS S3 replication |

### Kết quả đạt được tuần 9:

* Triển khai thành công website tĩnh trên S3.
* Phân biệt rõ giữa public access block và permission cấp object.
* Tăng tốc truy cập bằng CloudFront kết hợp S3 origin.
* Bật versioning và cấu hình replication để tăng độ bền dữ liệu.
* Ghi nhận các bước dọn dẹp bucket và distribution.