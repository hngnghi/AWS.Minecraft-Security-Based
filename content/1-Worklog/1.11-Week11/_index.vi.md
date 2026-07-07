---
title: "Worklog Tuần 11"
date: 2026-06-26
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:
* Phối hợp nghiên cứu, phân tích tài liệu và phác thảo giải pháp bảo mật đám mây chuyên sâu cho dự án tốt nghiệp.
* Hỗ trợ triển khai hạ tầng nền tảng (VPC, EC2) và cấu hình phân hệ giám sát an ninh (GuardDuty, Lambda).

### Các công việc triển khai và Tiến độ thực tế:

| Thứ | Công việc | Ngày chạy | Công cụ | Kết quả đạt được |
| :---: | :--- | :---: | :--- | :--- |
| **2** | Hỗ trợ nghiên cứu tài liệu & tham gia phác thảo kiến trúc tổng thể. | 26/06/2026 | Architecture design notes, Draw.io | Thu thập thông số cấu phần hạ tầng đám mây và tham gia phác thảo sơ đồ kiến trúc tổng thể cho dự án Hệ thống bảo mật máy chủ Minecraft trên AWS. |
| **3** | Phối hợp thiết lập hạ tầng mạng nền tảng bảo mật. | 27/06/2026 | AWS VPC, Security Group | Thiết lập các thông số mạng nền tảng cho phân hệ `Minecraft-Security-Lab` (VPC, Subnet, Route Table) và rà soát cấu hình luật đóng/mở cổng dịch vụ tại Security Group. |
| **4** | Hỗ trợ cài đặt & cấu hình môi trường máy chủ. | 28/06/2026 | Amazon EC2, Systems Manager | Khởi chạy máy chủ Linux trên Amazon EC2, thực hiện cài đặt, cấu hình và vận hành an toàn Minecraft Server dưới quyền user giới hạn hệ thống qua Session Manager. |
| **5** | Hỗ trợ cấu hình & phân tích cảnh báo hệ thống phát hiện xâm nhập. | 29/06/2026 | Amazon GuardDuty, EventBridge | Kích hoạt, theo dõi hệ thống Amazon GuardDuty; tiến hành phân tích và phân loại các danh mục cảnh báo an ninh (Findings) thu được từ môi trường thử nghiệm. |
| **6** | Tham gia lập trình hàm phản ứng & cấu hình luồng tự động hóa. | 30/06/2026 | AWS Lambda, Amazon EventBridge | Phối hợp viết kịch bản gỡ lỗi cho hàm AWS Lambda (`Minecraft-Automated-Block-IP`) và kiểm thử luồng tự động hóa phản ứng, ngăn chặn địa chỉ IP độc hại. |

---

### Kết quả đạt được tuần 11:
* Hoàn thành vai trò hỗ trợ phân tích tài liệu và làm rõ sơ đồ kiến trúc bảo mật đám mây cho dự án.
* Phối hợp triển khai thành công môi trường mạng cô lập và cấu hình dịch vụ trên máy chủ EC2 an toàn.
* Nắm quy trình vận hành, phân loại lỗi của GuardDuty và cơ chế kích hoạt tự động qua EventBridge.
