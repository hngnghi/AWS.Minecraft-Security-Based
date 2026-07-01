---
title: "Thiết lập mạng bảo mật (VPC & Security Group)"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

Trước khi triển khai máy chủ Minecraft, cần xây dựng một lớp bảo vệ mạng an toàn — giống như tạo "hào thành" bao quanh hệ thống để ngăn chặn các truy cập trái phép ngay từ bên ngoài.

### Bước 1: Tạo VPC và Public Subnet

1. Đăng nhập vào **AWS Management Console** và mở dịch vụ **VPC**.

![Dịch vụ VPC](/images/5-Workshop/5.1/1.a.VPC.png)

2. Chọn **Create VPC**.

![Tạo VPC](/images/5-Workshop/5.1/1.b.VPC.png)

- Chọn **VPC and more** để AWS tự động tạo Subnet và Internet Gateway.
- **Name tag auto-generation:** `Minecraft-Security-Lab`
- **IPv4 CIDR block:** `10.0.0.0/16`

![Cấu hình CIDR cho VPC](/images/5-Workshop/5.1/1.c.VPC.png)

- **Number of Availability Zones (AZs):** `1` (giúp tối ưu chi phí cho môi trường thực hành).
- **Number of Public subnets:** `1`
- **Number of Private subnets:** `0`

Trong phạm vi workshop, chỉ sử dụng một **Public Subnet** kết hợp với **Security Group** để đơn giản hóa kiến trúc nhưng vẫn đảm bảo tính bảo mật.

![Cấu hình Subnet](/images/5-Workshop/5.1/1.d.VPC.png)

3. Nhấn **Create VPC** để hoàn tất quá trình tạo.

![Tạo VPC thành công](/images/5-Workshop/5.1/1.e.VPC.png)

---

### Bước 2: Cấu hình Security Group theo mô hình Zero Trust

Một trong những cổng thường xuyên bị tin tặc dò quét là **SSH (Port 22)**. Trong workshop này, máy chủ sẽ **không mở cổng SSH**, chỉ cho phép người chơi truy cập thông qua cổng mặc định của Minecraft.

1. Trong dịch vụ **VPC**, chọn **Security Groups** → **Create security group**.

- **Security group name:** `sg-minecraft-server`
- **Description:** `Only allow Minecraft traffic.`
- **VPC:** Chọn `Minecraft-Security-Lab`

![Tạo Security Group](/images/5-Workshop/5.1/1.f.VPC.png)

2. Tại phần **Inbound rules**, chọn **Add rule** và cấu hình như sau:

- **Type:** Custom TCP
- **Port range:** `25565`
- **Source:** Anywhere-IPv4 (`0.0.0.0/0`) để cho phép người chơi kết nối từ Internet.

**Không thêm bất kỳ quy tắc nào cho cổng `22 (SSH)`**.

{{% notice warning %}}
**Lưu ý quan trọng về bảo mật**

Tuyệt đối **không mở cổng SSH (22)** ra Internet.

Toàn bộ quá trình quản trị máy chủ sẽ được thực hiện thông qua **AWS Systems Manager Session Manager**, giúp quản trị viên kết nối trực tiếp đến EC2 mà không cần SSH Key Pair hoặc Public IP dành cho SSH.
{{% /notice %}}

3. Giữ nguyên **Outbound rules** mặc định (**Allow all outbound**) để máy chủ có thể:

- Tải plugin Minecraft.
- Cập nhật hệ điều hành.
- Truy cập các dịch vụ cần thiết của AWS.

4. Nhấn **Create security group**.

![Cấu hình Inbound Rules](/images/5-Workshop/5.1/1.g.VPC.SG.png)

![Tạo Security Group thành công](/images/5-Workshop/5.1/1.h.VPC.SG.png)

---

### Bước 3: Bật tính năng tự động gán Public IP cho Subnet

Trước khi tạo máy chủ **Amazon EC2**, cần bật tính năng tự động gán địa chỉ IP công khai để tránh tình trạng EC2 không có Public IP sau khi khởi tạo.

Thực hiện theo các bước sau:

1. Truy cập **VPC** → **Subnets**.
2. Chọn Public Subnet vừa tạo.
3. Chọn **Actions** → **Edit subnet settings**.
4. Đánh dấu chọn **Enable auto-assign public IPv4 address**.
5. Nhấn **Save** để lưu cấu hình.
6. Sau đó tiến hành tạo máy chủ **EC2** trên Subnet này.

![Bật Auto-assign Public IP](/images/5-Workshop/5.1/1.i.VPC.SG.png)

---

### Kết quả

Sau khi hoàn thành các bước trên, hạ tầng mạng ban đầu đã sẵn sàng với các thành phần:

- Một **Amazon VPC** độc lập cho môi trường Minecraft.
- Một **Public Subnet** kết nối Internet.
- Một **Security Group** áp dụng nguyên tắc **Zero Trust**, chỉ cho phép truy cập cổng **25565** của Minecraft.
- Cổng **SSH (22)** hoàn toàn bị vô hiệu hóa để giảm thiểu nguy cơ bị tấn công Brute Force hoặc dò quét.
- Public Subnet được cấu hình tự động gán **Public IPv4 Address**, sẵn sàng cho bước triển khai máy chủ Amazon EC2 ở phần tiếp theo.