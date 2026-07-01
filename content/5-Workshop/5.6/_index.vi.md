---
title: "Che giấu IP thật & chống DDoS (Global Accelerator + NLB)"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

Minecraft chạy trên giao thức TCP cổng **25565** (Tầng 4), nên không thể dùng **AWS WAF** hay **CloudFront**. Giải pháp chuẩn là **AWS Global Accelerator** kết hợp **Network Load Balancer (NLB)** để che giấu IP gốc của EC2 và chống DDoS.

Người chơi kết nối qua IP tĩnh của Global Accelerator, được bảo vệ mặc định bởi **AWS Shield Standard**. IP thật của EC2 được ẩn hoàn toàn.

### Bước 1: Tạo Network Load Balancer (NLB)

1. Vào **EC2** → **Load Balancing** → **Target Groups** → **Create target group**.
   - **Choose a target type:** `Instances`
   - **Target group name:** `Minecraft-TG`
   - **Protocol / Port:** `TCP` và `25565`

![Tạo target group](/images/5-Workshop/5.6/6.a.TG.png)

![Cấu hình target group](/images/5-Workshop/5.6/6.b.TG.png)

   - Chọn `Minecraft-Secure-Server` → **Include as pending below** → **Create target group**.

![Target group đã tạo](/images/5-Workshop/5.6/6.c.TG.png)

2. Ở menu bên trái, chọn **Load Balancers** → **Create load balancer** → **Network Load Balancer**.
   - **Load balancer name:** `Minecraft-NLB`
   - **Scheme:** `Internet-facing`

![Tạo NLB](/images/5-Workshop/5.6/6.d.TG.png)

   - **Network mapping:** Chọn VPC workshop và tích chọn tất cả Availability Zones / Subnets.

![Network mapping](/images/5-Workshop/5.6/6.e.TG.png)

   - **Listeners and routing:** Protocol `TCP`, Port `25565`, Default action = `Minecraft-TG`.

![Cấu hình listener](/images/5-Workshop/5.6/6.f.TG.png)

   - Bấm **Create load balancer**.

### Bước 2: Cấu hình AWS Global Accelerator

1. Tìm **AWS Global Accelerator** → bấm **Create accelerator**.
   - **Accelerator name:** `Minecraft-Accelerator`
   - **Type:** `Standard` → **Next**.

![Tạo accelerator](/images/5-Workshop/5.6/6.g.GA.png)

![Loại accelerator](/images/5-Workshop/5.6/6.h.GA.png)

2. **Listeners:** Cấu hình Port `25565`, Protocol `TCP` → **Next**.

![Cấu hình listener](/images/5-Workshop/5.6/6.i.GA.png)

3. **Endpoint groups:** Chọn Region, ví dụ `ap-southeast-1` → **Next**.

![Endpoint group](/images/5-Workshop/5.6/6.j.GA.png)

4. **Endpoints:** Chọn **Network Load Balancer** và chọn `Minecraft-NLB` → **Create accelerator**.

![Chọn endpoint](/images/5-Workshop/5.6/6.l.GA.png)

![Accelerator đã sẵn sàng](/images/5-Workshop/5.6/6.l.GA.png)

### Kết quả

AWS cấp 2 IP tĩnh toàn cầu. Từ giờ, hãy dùng các IP này để người chơi kết nối vào thay vì IP public của EC2.
