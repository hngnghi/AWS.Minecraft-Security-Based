---
title: "Quy trình bật server hoàn chỉnh"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

### Bước 1: Bật máy chủ trên AWS Console

1. Đăng nhập **AWS Console** → vào **EC2**.
2. Chọn `Minecraft-Secure-Server` → bấm **Instance state** → chọn **Start instance**.
3. Chờ máy chuyển sang trạng thái **Running**. Bấm **Connect** → chọn tab **SSM Session Manager** → bấm **Connect** để mở terminal `$`.

### Bước 2: Chạy chuỗi lệnh khởi động an toàn

Copy toàn bộ khối lệnh sau và dán trực tiếp vào terminal `$`. Hệ thống sẽ tự động dọn sạch tiến trình cũ và khởi động server một cách an toàn:

```bash
# 1. Quét sạch các tiến trình kẹt từ lần trước (nếu có)
sudo killall -9 java 2>/dev/null
sudo killall -9 screen 2>/dev/null
screen -wipe >/dev/null 2>&1

# 2. Xóa file lock bị kẹt để tránh lỗi WorldConflict
sudo rm -f /opt/minecraft/world/session.lock

# 3. Đảm bảo phân quyền chính xác cho thư mục game
sudo chown -R minecraft:minecraft /opt/minecraft

# 4. Di chuyển vào đúng thư mục chứa game
cd /opt/minecraft

# 5. Khởi chạy game ngầm trong screen tên 'minecraft-server' bằng user an toàn
screen -dmS minecraft-server sudo -u minecraft java -Xmx2G -Xms2G -jar server.jar nogui
```

Sau khi chạy xong:
- Server đã được bật ngầm hoàn toàn.
- Đợi khoảng **15 giây**, rồi mở Minecraft và kết nối vào chơi.

### Kiểm tra trạng thái Server

Để kiểm tra trạng thái, chạy:

```bash
screen -ls
```

Hoặc:

```bash
screen -r minecraft-server
```

Hoặc xem log mới nhất:

```bash
tail -n 20 /opt/minecraft/logs/latest.log
```
