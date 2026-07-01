---
title: "Demo phòng thủ (Sample Findings)"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

Vì **GuardDuty** đôi khi mất 5 đến 15 phút để phân tích log thật, hãy dùng tính năng **Sample Findings** để demo mượt mà mà không có "thời gian chết".

1. Trên **AWS Console**, vào **GuardDuty** → **Settings**.
2. Cuộn xuống tìm **Generate sample findings** và nhấp vào đó. AWS sẽ tự động tạo log tấn công giả lập như SSH brute force và port sweep.

![Tạo sample findings](/images/5-Workshop/5.10/10.a.GD.png)

3. Ngay lập tức:
   - **EventBridge** bắt được sự kiện.
   - **Lambda** chạy code chặn IP.
   - Mở **CloudWatch Logs** của Lambda để xem dòng log: `"Phát hiện mối đe dọa... Đã thực thi chặn IP thành công"`.

![Log CloudWatch](/images/5-Workshop/5.10/10.b.GD.png)

4. **Lambda** cũng kích hoạt **Amazon SNS** và gửi email cảnh báo trực tiếp đến điện thoại hoặc hộp thư của người quản trị.

![Cảnh báo email/SMS](/images/5-Workshop/5.10/10.c.SMS.png)

{{% notice info %}}
**Mẹo demo:** Trình diễn đồng thời **CloudWatch Logs** và **email notification** để chứng minh chu trình SOAR hoàn chỉnh: Phát hiện → Tự động chặn IP → Thông báo.
{{% /notice %}}
