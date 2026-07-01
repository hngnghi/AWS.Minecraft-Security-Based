---
title: "Phát hiện xâm nhập (GuardDuty)"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

### Bước 1: Bật Amazon GuardDuty

1. Tìm dịch vụ **Amazon GuardDuty** trên thanh tìm kiếm AWS Console.

![Tìm kiếm GuardDuty](/images/5-Workshop/5.3/3.a.GD.png)

2. Nếu đây là lần đầu sử dụng, chỉ cần nhấn **Enable GuardDuty**.

3. GuardDuty sẽ tự động quét, phân tích các dòng log hệ thống và **VPC Flow Logs** để phát hiện hành vi bất thường mà không làm chậm server.

![GuardDuty đã bật](/images/5-Workshop/5.3/3.b.GD.png)

### Hiểu về GuardDuty

Sau khi bật GuardDuty, bạn sẽ vào giao diện quản trị. Chú ý các mục menu bên trái:

- **Findings:** Hiển thị danh sách tấn công hoặc hành vi nguy hiểm đang diễn ra, ví dụ quét port hoặc dò mật khẩu. Khi server mới lập, danh sách này sẽ trống (`No findings`).
- **Lists:** Nơi tự định nghĩa danh sách IP tin cậy hoặc IP độc hại đã biết trước.
- **Settings:** Cấu hình nâng cao và là nơi quan trọng nhất để demo trực tiếp.
