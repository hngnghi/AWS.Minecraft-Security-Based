---
title: "Triển khai Minecraft Server & Quản trị SSM"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### Bước 1: Khởi tạo máy chủ EC2 (Ubuntu)

1. Truy cập **EC2** → chọn **Launch instances**.
   - **Name:** `Minecraft-Secure-Server`
   - **Application and OS Images:** Chọn **Ubuntu** (bản LTS mới nhất).

![EC2 launch](/images/5-Workshop/5.2/2.a.EC2.png)

   - **Instance type:** `t3.medium` (2 vCPU, 4GB RAM) — cấu hình tối thiểu để chạy Minecraft mượt. Nếu dùng Free Tier, có thể chọn `t2.micro` hoặc `t3.micro`, nhưng game có thể bị lag.

![Instance type](/images/5-Workshop/5.2/2.b.EC2.png)

   - **Key pair (login):** Chọn **Proceed without a key pair**. Lý do bảo mật: chúng ta sẽ quản trị qua **AWS Systems Manager (SSM)**, không dùng SSH.

![Key pair skipped](/images/5-Workshop/5.2/2.c.EC2.png)

   - **Network settings:** Bấm **Edit**.
     - **VPC:** `Minecraft-Security-Lab`
     - **Firewall (Security groups):** Chọn security group đã tạo: `sg-minecraft-server`.

![Network settings](/images/5-Workshop/5.2/2.e.EC2.png)

   - **Advanced details:** Cuộn xuống mục **IAM instance profile**, tạo hoặc chọn Role có gắn policy `AmazonSSMManagedInstanceCore`. Role này cho phép AWS quản lý EC2 qua **SSM Session Manager** mà không cần mở port 22.

![IAM instance profile](/images/5-Workshop/5.2/2.f.EC2.png)

2. Bấm **Launch instance**.

![Launching instance](/images/5-Workshop/5.2/2.g.EC2.png)

### Bước 2: Cài đặt Minecraft Server qua AWS SSM Session Manager

1. Chờ instance chuyển sang trạng thái **Running**. Tích chọn instance → bấm **Connect**.
2. Chọn tab **Session Manager** → bấm **Connect**.

![Connect via SSM](/images/5-Workshop/5.2/2.h.EC2.png)

3. Một terminal dòng lệnh hiện ngay trên trình duyệt.

![Browser terminal](/images/5-Workshop/5.2/2.i.EC2.png)

4. Chuyển sang root và cập nhật hệ thống:

```bash
sudo su -
apt-get update && apt-get upgrade -y
```

5. Cài đặt Java:

```bash
apt-get install openjdk-17-jre-headless -y
```

6. Tạo thư mục và tải Minecraft Server:

```bash
cd /opt/minecraft
wget https://api.papermc.io/v2/projects/paper/versions/1.20.4/builds/496/downloads/paper-1.20.4-496.jar -O server.jar
```

7. Chạy thử lần đầu để tạo file cấu hình:

```bash
java -Xmx2G -Xms2G -jar server.jar nogui
```

Server sẽ dừng lại và yêu cầu đồng ý điều khoản.

8. Mở file `eula.txt` bằng `nano eula.txt`, sửa `eula=false` thành `eula=true`, và `online-mode=true` thành `online-mode=false`. Lưu lại.

9. Khởi chạy server chạy ngầm bằng `screen`:

```bash
apt-get install screen -y
screen -S minecraft
java -Xmx2G -Xms2G -jar server.jar nogui
```

Thoát màn hình `screen` bằng `Ctrl + A`, sau đó bấm `D`.

{{% notice warning %}}
**Cảnh báo bảo mật:** Trong log có thể xuất hiện thông báo màu vàng:
**YOU ARE RUNNING THIS SERVER AS AN ADMINISTRATIVE OR ROOT USER. THIS IS NOT ADVISED.**
Hãy làm theo các bước dưới đây để chuyển server sang chạy bằng tài khoản hạn chế quyền.
{{% /notice %}}

### Bước 3: Chuyển server sang chạy bằng tài khoản hạn chế quyền

**Bước 3.1:** Tắt server an toàn:

```bash
stop
```

**Bước 3.2:** Tạo user riêng cho Minecraft:

```bash
useradd -r -m -U -d /opt/minecraft -s /bin/false minecraft
```

**Bước 3.3:** Phân quyền lại thư mục game:

```bash
chown -R minecraft:minecraft /opt/minecraft
```

**Bước 3.4:** Dọn tiến trình cũ và xóa file lock:

```bash
sudo killall -9 java
sudo rm -f /opt/minecraft/world/session.lock
```

**Bước 3.5:** Đảm bảo phân quyền lại toàn bộ thư mục:

```bash
sudo chown -R minecraft:minecraft /opt/minecraft
```

**Bước 3.6:** Chạy server bằng user `minecraft` trong `screen`:

```bash
screen -S minecraft-server
sudo -u minecraft java -Xmx2G -Xms2G -jar /opt/minecraft/server.jar nogui
```

Đợi log hiện chữ `Done!`. Cảnh báo màu vàng sẽ biến mất.

Ẩn cửa sổ này bằng `Ctrl + A`, sau đó bấm `D`.

**Bước 3.7:** Kết nối vào game bằng Public IP của EC2.

![Server ready](/images/5-Workshop/5.2/2.j.EC2.png)
