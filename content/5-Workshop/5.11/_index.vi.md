---
title: "Dọn dẹp tài nguyên"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---

Việc dọn dẹp tài nguyên AWS sau khi hoàn thành đồ án là bước cực kỳ quan trọng để tránh phát sinh chi phí ngoài ý muốn sau khi hết Free Tier.

Do các dịch vụ liên kết với nhau, bạn cần xóa theo đúng thứ tự ngược từ ngoài vào trong để tránh lỗi ràng buộc hệ thống.

### Bước 1: Xóa AWS Global Accelerator & Network Load Balancer

Hai dịch vụ này nằm ở rìa ngoài cùng và tính tiền theo giờ, cần xóa đầu tiên:

1. Vào **AWS Global Accelerator** → chọn `Minecraft-Accelerator` → bấm **Edit** → chuyển sang **Disabled**. Chờ khoảng 1 phút, tích chọn và bấm **Delete**.

![Tắt accelerator](/images/5-Workshop/5.11/11.a.Delete.png)

![Xóa accelerator](/images/5-Workshop/5.11/11.b.Delete.png)

2. Vào **EC2** → **Load Balancers** → chọn `Minecraft-NLB` → **Actions** → **Delete**.

![Xóa NLB](/images/5-Workshop/5.11/11.c.Delete.png)

3. Ở menu EC2 bên trái, chọn **Target Groups** → chọn `Minecraft-TG` → **Actions** → **Delete**.

![Xóa target group](/images/5-Workshop/5.11/11.d.Delete.png)

### Bước 2: Xóa vĩnh viễn máy chủ EC2

1. Vào **EC2** → **Instances**.
2. Chọn `Minecraft-Secure-Server`.
3. Bấm **Instance state** → chọn **Terminate instance**. Thao tác này sẽ xóa vĩnh viễn máy chủ và ổ đĩa EBS đi kèm.

{{% notice warning %}}
Ở bước này, **không** chọn **Stop instance**. Bắt buộc chọn **Terminate instance** để xóa bỏ hoàn toàn máy chủ.
{{% /notice %}}

![Terminate instance](/images/5-Workshop/5.11/11.e.Delete.png)

### Bước 3: Xóa Lambda & EventBridge Rule

1. Vào **Lambda** → chọn `Minecraft-Automated-Block-IP` → **Actions** → **Delete**.

![Xóa Lambda](/images/5-Workshop/5.11/11.f.Delete.png)

2. Vào **Amazon EventBridge** → **Rules** → chọn rule kết nối GuardDuty → **Delete**.

![Xóa EventBridge rule](/images/5-Workshop/5.11/11.g.Delete.png)

### Bước 4: Xóa Topic SNS

1. Vào **Simple Notification Service (SNS)** → **Subscriptions** → chọn subscription email của bạn → **Delete**.
2. Chọn **Topics** → chọn `Minecraft-Attack-Alerts` → **Delete**.

![Xóa topic SNS](/images/5-Workshop/5.11/11.h.Delete.png)

### Bước 5: Tắt Amazon GuardDuty

GuardDuty tính phí theo dung lượng log phân tích, nên cần tắt hoàn toàn khi không dùng:

1. Vào **Amazon GuardDuty**.
2. Ở menu bên trái, chọn **Settings**.

![Cài đặt GuardDuty](/images/5-Workshop/5.11/11.i.Delete.png)

3. Cuộn xuống phần **Disable GuardDuty** và bấm **Disable** để hủy toàn bộ dữ liệu cấu hình và dừng dịch vụ.

### Bước 6: Xóa các bản sao lưu trong AWS Backup

1. Vào **AWS Backup** → **Backup vaults**.
2. Mở `Minecraft-Secure-Vault`.
3. Tích chọn tất cả recovery points → **Actions** → **Delete** từng bản.

![Xóa recovery points](/images/5-Workshop/5.11/11.j.Delete.png)

4. Sau khi két sắt trống, quay lại **Backup vaults**, chọn vault đó → **Delete**.
5. Ở menu bên trái, chọn **Backup plans** → chọn plan sao lưu mỗi giờ → **Delete**.

![Xóa backup plan](/images/5-Workshop/5.11/11.k.Delete.png)

### Bước 7: Khôi phục lại Network ACL

Nếu cần, đưa VPC Network ACL về trạng thái mặc định:

1. Vào **VPC** → **Network ACLs**.
2. Chọn ACL của VPC → **Inbound rules** → **Edit inbound rules**.
3. Xóa rule số `50` do Lambda đã tạo tự động → **Save changes**.

![Reset NACL](/images/5-Workshop/5.11/11.l.Delete.png)

### Kiểm tra cuối cùng

Sau khi xóa xong, vào **AWS Billing** → **Dashboard** để kiểm tra xem còn dịch vụ nào đang chạy ngầm hay không. Nếu thực hiện đủ 7 bước trên, tài khoản AWS đã trở về trạng thái an toàn và không còn phát sinh chi phí.
