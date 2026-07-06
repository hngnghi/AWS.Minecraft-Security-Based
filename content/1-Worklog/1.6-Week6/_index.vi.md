---
title: "Worklog Tuần 6"
date: 2026-05-22
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:
* Tìm hiểu về máy chủ EC2, lưu trữ EBS và AMI.
* Thực hành CloudFront, Lambda@Edge và Microsoft AD.

### Công việc & Tiến độ:

| Thứ | Công việc | Ngày chạy | Công cụ | Kết quả đạt được |
| :---: | :--- | :---: | :--- | :--- |
| **2** | Nghiên cứu instance types, EBS & cấu hình mạng phân phối nội dung. | 25/05/2026 | CloudFront, Amazon S3 | Phân biệt các loại volume phù hợp từng workload. Khởi tạo CloudFront Distribution, giảm đáng kể độ trễ tải trang tĩnh từ S3. |
| **3** | Khởi chạy máy chủ EC2 & nâng cấp giải pháp điện toán biên. | 26/05/2026 | EC2 (Linux/Windows), Lambda@Edge | Chạy máy chủ Linux/Windows; viết và tích hợp mã Lambda@Edge (Node.js/Python) xử lý request tại biên mạng để giảm tải cho máy chủ gốc. |
| **4** | Quản lý vòng đời máy chủ & triển khai Windows Server. | 27/05/2026 | EC2 lifecycle, AMI, RDP | Thay đổi instance type, tạo EBS snapshot/custom AMI. Kết nối thành công Windows Server qua RDP; hiểu quy trình chạy ứng dụng ASP.NET Core MVC. |
| **5** | Thực hành phục hồi quyền máy chủ & thiết lập dịch vụ thư mục. | 28/05/2026 | AWS Managed Microsoft AD | Phục hồi quyền truy cập Linux/Windows và cấu hình RDP. Khởi tạo thành công miền Active Directory, quản lý định danh tập trung cho máy chủ. |
| **6** | Deploy ứng dụng Web & tổng hợp báo cáo kiểm soát chi phí. | 29/05/2026 | IAM, AWS Billing | Triển khai thành công ứng dụng web (LAMP/Node.js) trên Linux. Hiểu rõ các chính sách IAM giới hạn loại instance family, type và EBS để tối ưu chi phí. |

---

### Kết quả đạt được tuần 6:

* Quản lý thành công EC2 Linux và Windows.
* Tạo snapshot, AMI và sử dụng lại tài nguyên đã chuẩn bị.
* Thực hành thay đổi loại instance và phục hồi quyền truy cập.
* Triển khai ứng dụng web trên Linux.
* Hiểu các chính sách IAM giới hạn instance family, type và EBS.