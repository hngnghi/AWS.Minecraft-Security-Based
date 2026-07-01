---
title: "Quy trình tắt server an toàn"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

Khi kết thúc buổi lab, hãy tắt server theo quy trình gọn gàng dưới đây để tránh lỗi dữ liệu thế giới hoặc tiến trình ngầm bị kẹt.

### Bước 1: Gửi lệnh tắt an toàn

Tại terminal `$`, dán lệnh này rồi bấm **Enter**:

```bash
# Gửi lệnh 'stop' trực tiếp vào cửa sổ ngầm để game lưu dữ liệu an toàn
screen -S minecraft-server -X stuff "stop^M"
```

Đợi khoảng **5 giây** để PaperMC lưu bản đồ xuống ổ đĩa.

### Bước 2: Dọn dẹp tài nguyên nền

Dán tiếp các lệnh dọn dẹp sau:

```bash
sudo killall -9 java 2>/dev/null
screen -wipe >/dev/null 2>&1
```

### Bước 3: Tắt EC2 từ Console

1. Quay lại **AWS Web Console**.
2. Chọn `Minecraft-Secure-Server`.
3. Bấm **Instance state** → chọn **Stop instance**.

{{% notice warning %}}
Chỉ dùng **Stop instance** khi bạn cần khởi động lại server sau này. Chỉ dùng **Terminate instance** ở bước dọn dẹp cuối cùng ở phần 5.11.
{{% /notice %}}

Quy trình này dùng cơ chế chạy ngầm chủ động (`-dmS`) và gửi lệnh từ xa (`-X stuff`), giúp loại bỏ hoàn toàn lỗi thao tác sai phím hay kẹt tiến trình khi báo cáo trước hội đồng.
