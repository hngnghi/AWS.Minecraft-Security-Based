---
title: "Worklog Tuần 12"
date: 2026-07-03
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12:
* Phối hợp hoàn thiện quy trình tự động hóa vận hành, tối ưu hóa kịch bản quản trị máy chủ an toàn và dọn dẹp hệ thống thử nghiệm.
* Nghiệm thu toàn diện chu trình phát hiện tấn công, hoàn thiện tài liệu kỹ thuật song ngữ và báo cáo kết quả thực tập tốt nghiệp.

### Các công việc triển khai và Tiến độ thực tế:

| Thứ | Công việc | Ngày chạy | Công cụ | Kết quả đạt được |
| :---: | :--- | :---: | :--- | :--- |
| **2** | Phối hợp thiết lập và phân quyền hạ tầng cảnh báo bảo mật. | 03/07/2026 | Amazon SNS, AWS Lambda | Cấu hình thành công SNS Topic (`Minecraft-Attack-Alerts`), xác thực danh sách email subscription và cấp quyền cho Lambda thực hiện publish thông báo cảnh báo. |
| **3** | Cập nhật cấu hình mã nguồn và kiểm thử định dạng thông điệp. | 04/07/2026 | AWS Lambda, CloudWatch Logs | Tích hợp ARN của SNS vào mã nguồn Lambda, tiến hành tái triển khai hàm và chuẩn hóa cấu trúc dữ liệu hiển thị của thông báo gửi về email. |
| **4** | Hỗ trợ xây dựng kịch bản khởi động máy chủ an toàn trên Linux. | 05/07/2026 | Linux Screen, Amazon EC2 | Tham gia viết và kiểm thử Startup Script cho Minecraft Server, theo dõi trạng thái phiên làm việc (`screen -ls`) và tệp log hệ thống sau khi kích hoạt chế độ restart. |
| **5** | Hỗ trợ xây dựng kịch bản đóng máy chủ và bảo toàn dữ liệu. | 06/07/2026 | Linux Bash Script, Minecraft Server | Tham gia hoàn thiện Shutdown Script, thực hiện kiểm thử tính năng lưu trữ bản đồ thế giới (world save) tự động và cấu hình quy trình dừng dịch vụ an toàn. |
| **6** | Giả lập tấn công nghiệm thu chu trình SOAR và giải thể tài nguyên. | 07/07/2026 | Amazon GuardDuty, AWS Billing | Kích hoạt sample findings để kiểm tra luồng tự động cô lập IP độc hại; thực hiện dọn dẹp toàn bộ tài nguyên theo thứ tự phụ thuộc và đối soát ví tiền an toàn 100%. |

---

### Kết quả đạt được tuần 12:
* Hỗ trợ tối ưu hóa vận hành hệ thống thông qua việc hoàn thành các kịch bản khởi động và đóng máy chủ an toàn, đảm bảo toàn vẹn dữ liệu cho Minecraft Server trên Linux.
* Nghiệm thu thành công chu trình SOAR bằng cách kích hoạt mẫu tấn công giả lập trên GuardDuty để kiểm thử toàn diện luồng phát hiện, cô lập IP và gửi cảnh báo tự động.
* Hoàn thiện hệ thống tài liệu kỹ thuật bằng file Markdown song ngữ và hoàn thành báo cáo kết quả thực tập tốt nghiệp đúng tiến độ.
* Giải thể và dọn dẹp sạch sẽ toàn bộ tài nguyên thử nghiệm trên AWS Console, xác nhận không phát sinh chi phí ngoài ý muốn trên AWS Billing Dashboard.