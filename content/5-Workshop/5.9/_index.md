---
title: "Safe Server Shutdown Procedure"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

When the demo or lab session ends, shut down the server cleanly to avoid world corruption or stuck background processes.

### Step 1: Send a Safe Stop Command

From the terminal `$`, paste this command and press **Enter**:

```bash
# Send 'stop' directly into the detached screen so the game saves safely
screen -S minecraft-server -X stuff "stop^M"
```

Wait about **5 seconds** for PaperMC to finish saving the world.

### Step 2: Clean Up Background Resources

Paste the following commands to fully clean the system:

```bash
sudo killall -9 java 2>/dev/null
screen -wipe >/dev/null 2>&1
```

### Step 3: Stop the EC2 Instance from the Console

1. Return to the **AWS Web Console**.
2. Select `Minecraft-Secure-Server`.
3. Click **Instance state** → choose **Stop instance**.

{{% notice warning %}}
Use **Stop instance** only when you plan to restart the server later. Use **Terminate instance** only during final cleanup in section 5.11.
{{% /notice %}}

This improved shutdown flow uses detached-screen remote command injection (`-dmS` and `-X stuff`) to avoid stuck key sequences or manual screen attach errors during presentations.
