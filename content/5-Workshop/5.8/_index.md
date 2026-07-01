---
title: "Complete Server Startup Procedure"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

### Step 1: Start the Server from AWS Console

1. Sign in to the **AWS Console** → open **EC2**.
2. Select `Minecraft-Secure-Server` → click **Instance state** → choose **Start instance**.
3. Wait until the instance shows **Running**. Click **Connect** → choose **SSM Session Manager** → click **Connect** to open the terminal `$`.

### Step 2: Run the Safe Startup Script

Copy and paste the entire command block below directly into the terminal. The system will clean up stale processes and start the server safely:

```bash
# 1. Clean up stuck processes from previous runs
sudo killall -9 java 2>/dev/null
sudo killall -9 screen 2>/dev/null
screen -wipe >/dev/null 2>&1

# 2. Remove stale lock file to prevent WorldConflict
sudo rm -f /opt/minecraft/world/session.lock

# 3. Ensure correct ownership for the game directory
sudo chown -R minecraft:minecraft /opt/minecraft

# 4. Move into the game directory
cd /opt/minecraft

# 5. Start the server in detached screen mode using the restricted user
screen -dmS minecraft-server sudo -u minecraft java -Xmx2G -Xms2G -jar server.jar nogui
```

After the script finishes:
- The server is running fully in the background.
- Wait about **15 seconds**, then open Minecraft and connect to play.

### Verify the Server

To check the server status, run:

```bash
screen -ls
```

Or:

```bash
screen -r minecraft-server
```

Or view the latest logs:

```bash
tail -n 20 /opt/minecraft/logs/latest.log
```
