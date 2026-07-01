---
title: "Hide Real IP & DDoS Protection (Global Accelerator + NLB)"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

Minecraft runs on TCP port **25565** (Layer 4), so **AWS WAF** and **CloudFront** cannot be used here. The standard AWS approach is **AWS Global Accelerator** combined with **Network Load Balancer (NLB)** to hide the EC2 origin IP and mitigate DDoS.

Players connect through a static Global Accelerator IP, which is protected by **AWS Shield Standard**. The real EC2 IP stays hidden.

### Step 1: Create Network Load Balancer (NLB)

1. Go to **EC2** → **Load Balancing** → **Target Groups** → **Create target group**.
   - **Choose a target type:** `Instances`
   - **Target group name:** `Minecraft-TG`
   - **Protocol / Port:** `TCP` and `25565`

![Create target group](/images/5-Workshop/5.6/6.a.TG.png)

![Target group settings](/images/5-Workshop/5.6/6.b.TG.png)

   - Select `Minecraft-Secure-Server` → **Include as pending below** → **Create target group**.

![Target group created](/images/5-Workshop/5.6/6.c.TG.png)

2. In the left menu, choose **Load Balancers** → **Create load balancer** → **Network Load Balancer**.
   - **Load balancer name:** `Minecraft-NLB`
   - **Scheme:** `Internet-facing`

![Create NLB](/images/5-Workshop/5.6/6.d.TG.png)

   - **Network mapping:** Choose the workshop VPC and select all Availability Zones / Subnets.

![Network mapping](/images/5-Workshop/5.6/6.e.TG.png)

   - **Listeners and routing:** Protocol `TCP`, Port `25565`, Default action = `Minecraft-TG`.

![Listener configuration](/images/5-Workshop/5.6/6.f.TG.png)

   - Click **Create load balancer**.

### Step 2: Configure AWS Global Accelerator

1. Search for **AWS Global Accelerator** → click **Create accelerator**.
   - **Accelerator name:** `Minecraft-Accelerator`
   - **Type:** `Standard` → click **Next**.

![Create accelerator](/images/5-Workshop/5.6/6.g.GA.png)

![Accelerator type](/images/5-Workshop/5.6/6.h.GA.png)

2. **Listeners:** Configure Port `25565`, Protocol `TCP` → **Next**.

![Listener config](/images/5-Workshop/5.6/6.i.GA.png)

3. **Endpoint groups:** Select your Region, for example `ap-southeast-1` → **Next**.

![Endpoint group](/images/5-Workshop/5.6/6.j.GA.png)

4. **Endpoints:** Choose **Network Load Balancer** and select `Minecraft-NLB` → **Create accelerator**.

![Endpoint selection](/images/5-Workshop/5.6/6.l.GA.png)

![Accelerator ready](/images/5-Workshop/5.6/6.l.GA.png)

### Result

AWS provides two static global IP addresses. From now on, share these addresses with players instead of the EC2 public IP.
