---
title: "Sao lưu thảm họa (AWS Backup)"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

### Bước 1: Tạo Backup Vault

1. Tìm **AWS Backup** và mở dịch vụ.
2. Ở menu bên trái, chọn **Backup vaults** → bấm **Create Backup vault**.

![Tạo backup vault](/images/5-Workshop/5.5/5.a.Backup.png)

3. Cấu hình két sắt:
   - **Backup vault name:** `Minecraft-Secure-Vault`
   - **Encryption key:** Giữ mặc định `aws/backup` để AWS tự động mã hóa.

![Cấu hình vault](/images/5-Workshop/5.5/5.b.Backup.png)

4. Bấm **Create Backup vault**.

![Vault đã tạo](/images/5-Workshop/5.5/5.d.Backup.png)

### Bước 2: Tạo Backup Plan

1. Ở menu bên trái, chọn **Backup plans** → bấm **Create Backup plan**.

![Tạo backup plan](/images/5-Workshop/5.5/5.e.Backup.png)

2. Chọn **Build a new plan**.

3. **Backup plan details**:
   - **Backup plan name:** `Minecraft-DR-Plan`

![Chi tiết plan](/images/5-Workshop/5.5/5.f.Backup.png)

4. **Backup rule configuration**:
   - **Backup rule name:** `Hourly-Backup-Rule`
   - **Backup vault:** `Minecraft-Secure-Vault`
   - **Backup frequency:** `Hourly` để chứng minh RPO dưới 1 tiếng
   - **Retention period:** `7` ngày

![Cấu hình rule](/images/5-Workshop/5.5/5.g.Backup.png)

![Thời gian lưu trữ](/images/5-Workshop/5.5/5.h.Backup.png)

5. Bấm **Create plan**.

### Bước 3: Gắn máy chủ Minecraft vào kế hoạch

1. Sau khi tạo plan, bấm **Assign resources**.

![Gán tài nguyên](/images/5-Workshop/5.5/5.i.Backup.png)

2. Cấu hình gán tài nguyên:
   - **Resource assignment name:** `Assign-Minecraft-EC2`
   - **IAM role:** Giữ mặc định **Default role**
   - **Resource selection:** Chọn **Include specific resource types**
   - **Select specific resource types:** Chọn **EC2**, sau đó chọn đúng instance `Minecraft-Secure-Server`

![Gán EC2](/images/5-Workshop/5.5/5.j.Backup.png)

3. Bấm **Assign resources**.

![Hoàn tất gán](/images/5-Workshop/5.5/5.m.EC2.Minecraft.png)

![Tổng quan backup](/images/5-Workshop/5.5/5.n.EC2.Minecraft.png)

![Trạng thái backup](/images/5-Workshop/5.5/5.o.EC2.Minecraft.png)

{{% notice info %}}
**Tại sao quan trọng:** Sao lưu mỗi giờ giúp giảm mất dữ liệu tối đa xuống dưới 1 tiếng. Backup được mã hóa trong vault, nên ngay cả khi EC2 bị xâm phạm, bản sao lưu vẫn được bảo vệ.
{{% /notice %}}
