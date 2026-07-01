---
title: "Thông báo Email (SNS)"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

Để nâng cao điểm báo cáo SOAR, chúng ta sẽ nâng cấp hàm Lambda ở phần 5.4 để tự động gửi email cảnh báo chi tiết ngay khi phát hiện tấn công.

Chúng ta dùng **Amazon SNS (Simple Notification Service)** vì nó cực kỳ ổn định, bảo mật và hoàn toàn miễn phí ở quy mô này.

### Bước 1: Tạo Topic Amazon SNS

1. Tìm **Simple Notification Service (SNS)** trên thanh tìm kiếm AWS.

![Tìm SNS](/images/5-Workshop/5.7/7.a.SNS.png)

2. Tại màn hình chính, nhập tên Topic:
   - **Topic name:** `Minecraft-Attack-Alerts` → bấm **Next step**.

![Tạo topic](/images/5-Workshop/5.7/7.b.SNS.png)

3. Chọn **Standard** → cuộn xuống bấm **Create topic**.

4. Sau khi tạo xong, bấm **Create subscription** để đăng ký nhận email:
   - **Protocol:** `Email`
   - **Endpoint:** địa chỉ email của bạn
   - Bấm **Create subscription**.

![Tạo subscription](/images/5-Workshop/5.7/7.c.SNS.png)

5. Kích hoạt email:
   - Mở hộp thư, tìm thư xác nhận từ AWS.
   - Bấm **Confirm Subscription**.
   - Khi màn hình hiện `Subscription confirmed!` là thành công.

![Đã xác nhận subscription](/images/5-Workshop/5.7/7.d.SNS.png)

6. Quay lại SNS, copy ARN của Topic. ARN có dạng:

```text
arn:aws:sns:us-east-1:845242191085:Minecraft-Attack-Alerts:5902fe45-b63f-494c-9668-e7bdc655690e
```

### Bước 2: Nâng cấp Lambda gửi Email

1. Vào **Lambda** → mở hàm `Minecraft-Automated-Block-IP`.
2. Mở **Configuration** → **Permissions** → bấm link tên Role để sang trang **IAM**.
3. Trong IAM, bấm **Add permissions** → **Attach policies**.
4. Tìm `AmazonSNSFullAccess`, tích chọn và bấm **Add permissions**.
5. Quay lại tab **Code** của Lambda, thay thế code bằng phiên bản nâng cấp từ Colab.
   - Lưu ý: thay thế ARN mẫu ở dòng số 11 bằng ARN thực tế của SNS Topic.
6. Bấm **Deploy**.

### Kết quả

Khi GuardDuty phát hiện tấn công, Lambda sẽ vừa chặn IP, vừa gửi email cảnh báo qua SNS.
