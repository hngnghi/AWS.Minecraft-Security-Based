---
title: "Secure Network Setup (VPC & Security Group)"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

Before starting the server, build a secure network perimeter — the "moat" around the castle.

### Step 1: Create VPC and Public Subnet

1. Sign in to the **AWS Console** and open **VPC**.

![VPC service](/images/5-Workshop/5.1/1.a.VPC.png)

2. Click **Create VPC**.

![Create VPC](/images/5-Workshop/5.1/1.b.VPC.png)

   - Select **VPC and more** (AWS auto-creates Subnet and Internet Gateway).
   - **Name tag auto-generation:** `Minecraft-Security-Lab`
   - **IPv4 CIDR block:** `10.0.0.0/16`

![VPC CIDR configuration](/images/5-Workshop/5.1/1.c.VPC.png)

   - **Number of Availability Zones (AZs):** `1` (cost saving).
   - **Number of Public subnets:** `1`
   - **Number of Private subnets:** `0` (for lab simplicity, use one Public Subnet locked down by **Security Group**).

![Subnet configuration](/images/5-Workshop/5.1/1.d.VPC.png)

3. Click **Create VPC**.

![VPC created](/images/5-Workshop/5.1/1.e.VPC.png)

### Step 2: Configure "Zero Trust" Security Group (Security Focus)

Attackers commonly scan port **22** (SSH). We will **not** open port **22** — only the game port.

1. In the **VPC** menu, select **Security Groups** → **Create security group**.
   - **Security group name:** `sg-minecraft-server`
   - **Description:** `Only allow Minecraft traffic.`
   - **VPC:** Select `Minecraft-Security-Lab`.

![Create security group](/images/5-Workshop/5.1/1.f.VPC.png)

2. **Inbound rules:** Click **Add rule**.
   - **Type:** Custom TCP | **Port range:** `25565` | **Source:** Anywhere-IPv4 (`0.0.0.0/0`) — allow players to connect.
   - **Do NOT** add a rule for port **22** (SSH).

{{% notice warning %}}
**Critical security rule:** Never open port **22** to the public Internet. All administration will use **AWS Systems Manager Session Manager** — no SSH key pair required.
{{% /notice %}}

3. **Outbound rules:** Keep default (Allow all outbound — needed for plugin downloads and OS updates).

4. Click **Create security group**.

![Inbound rules](/images/5-Workshop/5.1/1.g.VPC.SG.png)

![Security group created](/images/5-Workshop/5.1/1.h.VPC.SG.png)

### Step 3: Enable Auto-assign Public IP on Subnet

Before creating **EC2**, enable public IP auto-assignment to avoid missing Public IP errors:

1. Go to **VPC** → **Subnets** → select your subnet.
2. **Actions** → **Edit subnet settings**.
3. Check **Enable auto-assign public IPv4 address** → **Save**.
4. Then create **EC2** on this subnet.

![Auto-assign public IP](/images/5-Workshop/5.1/1.i.VPC.SG.png)
