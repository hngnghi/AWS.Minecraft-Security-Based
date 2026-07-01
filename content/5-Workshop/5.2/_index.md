---
title: "Deploy Minecraft Server & SSM Administration"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### Step 1: Launch EC2 (Ubuntu)

1. Go to **EC2** → **Launch instances**.
   - **Name:** `Minecraft-Secure-Server`
   - **Application and OS Images:** Choose **Ubuntu** (latest LTS).

![EC2 launch](/images/5-Workshop/5.2/2.a.EC2.png)

   - **Instance type:** `t3.medium` (2 vCPU, 4GB RAM) as the minimum for smooth Minecraft play. For Free Tier testing, `t2.micro` or `t3.micro` can be used but may lag under load.

![Instance type](/images/5-Workshop/5.2/2.b.EC2.png)

   - **Key pair (login):** Choose **Proceed without a key pair** (Not recommended for general use, but acceptable here because administration will go through **AWS Systems Manager (SSM)** rather than SSH).

![Key pair skipped](/images/5-Workshop/5.2/2.c.EC2.png)

   - **Network settings:** Click **Edit**.
     - **VPC:** `Minecraft-Security-Lab`
     - **Firewall (Security groups):** Select existing security group → choose `sg-minecraft-server`.

![Network settings](/images/5-Workshop/5.2/2.e.EC2.png)

   - **Advanced details:** Scroll to **IAM instance profile** and create or select a role with the `AmazonSSMManagedInstanceCore` policy attached. This allows AWS to manage the instance through **SSM Session Manager** without opening SSH.

![IAM instance profile](/images/5-Workshop/5.2/2.f.EC2.png)

2. Click **Launch instance**.

![Launching instance](/images/5-Workshop/5.2/2.g.EC2.png)

### Step 2: Install Minecraft Server via AWS SSM Session Manager

1. Wait until the instance shows **Running**. Select the instance → click **Connect**.
2. Choose the **Session Manager** tab → click **Connect**.

![Connect via SSM](/images/5-Workshop/5.2/2.h.EC2.png)

3. A browser-based terminal appears.

![Browser terminal](/images/5-Workshop/5.2/2.i.EC2.png)

4. Switch to root and update the system:

```bash
sudo su -
apt-get update && apt-get upgrade -y
```

5. Install Java:

```bash
apt-get install openjdk-17-jre-headless -y
```

6. Create a directory and download Minecraft Server:

```bash
cd /opt/minecraft
wget https://api.papermc.io/v2/projects/paper/versions/1.20.4/builds/496/downloads/paper-1.20.4-496.jar -O server.jar
```

7. Run once to generate config files:

```bash
java -Xmx2G -Xms2G -jar server.jar nogui
```

The server will stop and prompt EULA acceptance.

8. Open `eula.txt` with `nano eula.txt`, change `eula=false` to `eula=true`, and change `online-mode=true` to `online-mode=false`. Save and exit.

9. Start the server in the background using `screen`:

```bash
apt-get install screen -y
screen -S minecraft
java -Xmx2G -Xms2G -jar server.jar nogui
```

Detach with `Ctrl + A`, then press `D`.

{{% notice warning %}}
**Critical security warning:** You may see a yellow warning in the logs:
**YOU ARE RUNNING THIS SERVER AS AN ADMINISTRATIVE OR ROOT USER. THIS IS NOT ADVISED.**
Continue below to reconfigure the server to run as a restricted non-root user.
{{% /notice %}}

### Step 3: Reconfigure to Run as a Restricted User

**Step 3.1:** Stop the current server safely:

```bash
stop
```

Wait for the world save to complete.

**Step 3.2:** Create a dedicated non-root Minecraft user:

```bash
useradd -r -m -U -d /opt/minecraft -s /bin/false minecraft
```

**Step 3.3:** Reassign ownership of the game directory:

```bash
chown -R minecraft:minecraft /opt/minecraft
```

**Step 3.4:** Clean stale Java processes and remove the stuck lock file:

```bash
sudo killall -9 java
sudo rm -f /opt/minecraft/world/session.lock
```

**Step 3.5:** Ensure directory ownership again:

```bash
sudo chown -R minecraft:minecraft /opt/minecraft
```

**Step 3.6:** Run the server as the restricted user inside `screen`:

```bash
screen -S minecraft-server
sudo -u minecraft java -Xmx2G -Xms2G -jar /opt/minecraft/server.jar nogui
```

Wait for `Done!` to appear. The yellow root-user warning should disappear.

Detach with `Ctrl + A`, then press `D`.

**Step 3.7:** Connect in Minecraft using the EC2 public IP.

![Server ready](/images/5-Workshop/5.2/2.j.EC2.png)
