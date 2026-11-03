# 1. Telegram Bot Integration & Setup Guide

> **Section:** Integrations • **Stable Release:** 1.0.1 Official • **Last Updated:** November 2026  
> **Audience:** General Users & System Administrators

---

## 🎯 Introduction & Benefits of Telegram Notifications

Backupino enables you to receive site backup and restore status reports directly in your Telegram account through a **dedicated personal bot**:
* **Direct Communication (No Intermediaries):** Messages are dispatched directly from your host to official Telegram servers without passing through any intermediate or centralized third-party servers.
* **Direct Download Buttons & Links:** Interactive download links embedded right within the message.
* **Comprehensive Metrics:** Reports backup archive size, file count, and Jalali (Solar Hijri) / Gregorian timestamps.
* **Resilient Retry Queue:** Built-in retry queue to handle momentary host network interruptions gracefully.

---

## 🤖 Step-by-Step Telegram Bot Creation

### Step 1: Create a Bot via BotFather
1. Open the Telegram app and search for the official verified bot [`@BotFather`](https://t.me/BotFather) (marked with a blue checkmark).
2. Click **Start** and send the command `/newbot`.
3. Enter a display name for your bot (e.g., `Royal Brand Site Backup`).
4. Enter a unique username ending with `bot` (e.g., `mybrand_backup_bot`).
5. BotFather will provide a long alphanumeric string known as the **HTTP API Token**:
   ```text
   7123456789:AAHk1_xyzabc1234567890abcdef
   ```
   Copy this token securely.

### Step 2: Start the Bot
1. Click the link to your newly created bot in Telegram to open the chat window.
2. Click **Start** to initiate the conversation and authorize the bot to send you messages (otherwise Telegram blocks inbound messages from the bot).

### Step 3: Retrieve Your Numeric User Chat ID
1. Search for the official bot [`@userinfobot`](https://t.me/userinfobot) in Telegram.
2. Click **Start**.
3. The bot will return your account information; the numeric value displayed next to **`Id:`** (e.g., `987654321`) is your personal Chat ID.

---

## ⚙️ Configuration in the Backupino Dashboard

1. In your WordPress admin dashboard, navigate to **Backupino → Settings → Notifications tab**.
2. Configure the Telegram section as follows:
   * **Enable Telegram Notifications:** Toggle the Telegram switch to the active position. (Backupino provides independent on/off switches for Telegram and Bale; enabling or disabling one has no effect on the other).
   * **Bot Token:** Paste the token received from BotFather.
   * **Chat ID:** Enter your numeric Chat ID.
3. Click **Save Settings**.
4. Click **Send Test Message**. Within seconds, a test notification featuring clickable links will arrive in your Telegram chat, verifying successful connectivity!
5. **Disabling Notifications:** Whenever you wish to suspend Telegram notifications, simply turn off the toggle switch. The saved token and Chat ID remain securely stored, but no network requests will be dispatched to Telegram.

---

## 🔒 Important Security Considerations

* Your bot token acts as your bot's secret password; never expose or share it with unauthorized parties.
* In Backupino, token values are never printed in public logs or exposed via public API endpoints; they are stored securely in the `wp_options` table.
* If your hosting server restricts or firewalls outbound traffic to Telegram domains, you can use the Bale messenger integration, which operates seamlessly across restricted or national networks.

---

## 🧭 Next Step

To set up notifications via the Bale messenger bot, proceed to the following guide:  
👉 [**Bale Bot Integration & Setup Guide**](02-bale-bot.md)
