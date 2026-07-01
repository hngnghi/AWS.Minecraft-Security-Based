---
title: "Worklog Tuần 12"
date: 2026-07-03
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12:

* Hoàn thiện tự động hóa cảnh báo và phản ứng bảo mật cho dự án tốt nghiệp.
* Hoàn thành startup và shutdown script an toàn cho Minecraft.
* Chạy demo SOAR, dọn dẹp tài nguyên AWS và hoàn thiện tài liệu báo cáo.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2 | - Tạo SNS topic `Minecraft-Attack-Alerts`<br>- Xác thực email subscription<br>- Cấp quyền Lambda publish SNS | 03/07/2026 | 03/07/2026 | Tài liệu AWS SNS |
| 3 | - Cập nhật ARN SNS vào code Lambda<br>- Deploy lại hàm Lambda<br>- Kiểm tra định dạng thông báo gửi đi | 04/07/2026 | 04/07/2026 | Ghi chú deploy Lambda |
| 4 | - Viết startup script an toàn cho Minecraft<br>- Kiểm tra `screen -ls` và log<br>- Test hành vi restart | 05/07/2026 | 05/07/2026 | Ghi chú vận hành Minecraft |
| 5 | - Viết shutdown script an toàn<br>- Kiểm tra lưu world<br>- Ghi nhận các bước dừng an toàn | 06/07/2026 | 07/07/2026 | Linux service best practices |
| 6 | - Chạy GuardDuty sample findings<br>- Kiểm tra CloudWatch Logs và email cảnh báo<br>- Thực hiện dọn dẹp theo đúng thứ tự<br>- Kiểm tra AWS Billing Dashboard | 07/07/2026 | 10/07/2026 | Project cleanup checklist |

### Kết quả đạt được tuần 12:

* Hoàn thành luồng cảnh báo: GuardDuty finding, Lambda tự động hóa và SNS email notification.
* Kiểm tra startup và shutdown script cho Minecraft server.
* Demo thành công chu trình SOAR: phát hiện tấn công, chặn IP và gửi cảnh báo.
* Dọn dẹp tài nguyên AWS theo đúng thứ tự dependency.
* Xác nhận không còn chi phí bất ngờ trên AWS Billing.
* Hoàn thiện tài liệu Markdown song ngữ và báo cáo cuối kỳ.