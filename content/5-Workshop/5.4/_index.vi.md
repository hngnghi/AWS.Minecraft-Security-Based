---
title: "Tự động phản ứng (Lambda & EventBridge)"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### Kịch bản

Khi **Amazon GuardDuty** phát hiện IP tấn công/quét port máy chủ, **Amazon EventBridge** bắt tín hiệu và gọi **AWS Lambda** để tự động thêm IP đó vào danh sách chặn của **Security Group**.

### Bước 1: Tạo hàm AWS Lambda

1. Truy cập **Lambda** → **Create function**.
   - **Function name:** `Minecraft-Automated-Block-IP`
   - **Runtime:** **Python 3.13**

![Tạo hàm Lambda](/images/5-Workshop/5.4/4.a.LBD.png)

![Chọn Python runtime](/images/5-Workshop/5.4/4.b.LBD.png)

2. Sau khi tạo xong, cuộn xuống **Configuration** → **Permissions** → bấm tên Role của Lambda để mở trang **IAM**.

![Quyền Lambda](/images/5-Workshop/5.4/4.c.LBD.png)

3. Trong IAM, bấm **Add permissions** → **Attach policies**.

![Thêm quyền](/images/5-Workshop/5.4/4.d.LBD.png)

![Gắn policies](/images/5-Workshop/5.4/4.e.LBD.IAM.png)

4. Tìm `AmazonEC2FullAccess`, tích chọn và bấm **Add permissions**.

![Gắn policy EC2](/images/5-Workshop/5.4/4.f.LBD.IAM.png)

5. Quay lại tab **Code** của Lambda, thay toàn bộ code bằng script Python từ Colab. Bấm **Deploy**.

![Code đã deploy](/images/5-Workshop/5.4/4.h.LBD.png)

> **Lưu ý:** PDF tham chiếu một notebook Colab cho code Lambda. Ở dòng số 11, thay thế placeholder ARN bằng ARN thực tế của SNS topic ở phần 5.7.

### Bước 2: Tạo EventBridge Rule

1. Mở **Amazon EventBridge** → **Rules** → **Create rule**.
   - **Name:** `GuardDuty-To-Lambda-Block`
   - **Rule type:** **Rule with an event pattern**

![Tạo EventBridge rule](/images/5-Workshop/5.4/4.i.LBD.EB.png)

![Loại rule](/images/5-Workshop/5.4/4.j.LBD.EB.png)

2. Bấm **Next**. Ở phần **Event source**, chọn **AWS services**.
   - **AWS service:** **GuardDuty**

![Nguồn GuardDuty](/images/5-Workshop/5.4/4.k.LBD.EB.png)

   - **Event type:** **GuardDuty Finding**

3. Bấm **Next**. Ở phần **Select target(s)**:
   - **Target:** **Lambda function**
   - **Function:** `Minecraft-Automated-Block-IP`

![Chọn target Lambda](/images/5-Workshop/5.4/4.l.LBD.EB.png)

4. Bấm **Next** qua các bước còn lại và **Create rule**.

![Rule đã tạo](/images/5-Workshop/5.4/4.m.LBD.EB.png)

### Kết quả

Khi GuardDuty phát hiện mối đe dọa, EventBridge kích hoạt Lambda. Lambda sẽ tự động chặn IP tấn công trong Security Group và gửi cảnh báo.
