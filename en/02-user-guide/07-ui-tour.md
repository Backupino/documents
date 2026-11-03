# 7. Dashboard Tour and UI Architecture

> **Section:** User Guide • **Stable Version:** 1.0.1 Official • **Last Updated:** November 2026  
> **Audience:** General Users and System Administrators

---

## 🎨 UI/UX Design Philosophy

Backupino's user interface is crafted to modern design standards, emphasizing clean typography, high-contrast visual hierarchy, complete accessibility, and responsive layouts:
* **Zero Aggressive Promotional Banners:** Your WordPress dashboard will never be cluttered with annoying upsell popups, artificial feature locks, or promotional nag notices.
* **100% Offline-First Architecture:** All CSS styling, icons, and typography assets are bundled locally, ensuring lightning-fast loading with zero dependencies on external CDNs or Google Fonts.

---

## 🖥️ Primary Dashboard Layout

### 1. Brand Header and Top Navigation
* Distinctive Backupino brand logo
* Software release and stability badge (`1.0.1 Free`)
* Primary navigation tabs: **Backups** and **Settings**

### 2. Permanent Download Link Banner
* Prominent top alert card featuring the persistent latest-backup URL endpoint along with a one-click **Copy Link** action button.

### 3. Backup Configuration & Initiation Card
* Toggle checkboxes for including files and database
* Optional text label field for package customization
* High-visibility blue **Create Backup** action button

### 4. Live Progress and Processing Terminal
* Real-time operational card with an animated progress bar displaying precise completion percentages and stage descriptions across all 4 pipeline stages.
* High-visibility red **Cancel** button for instantaneous process abort and disk cleanup.

### 5. Recent Backups Table
* Granular display of latest job statuses, package filenames, archive sizes, triple-choice download buttons (`Both`, `.zip`, `installer.php`), and secure deletion controls.

---

## ⚙️ Six Dedicated Settings Tabs

1. **Archive & Exclusions Tab:** Configure directory/file exclusion rules, file size threshold limits, and batch file compression chunk sizes.
2. **Storage Tab:** Displays the absolute physical path of the backup directory on the host filesystem and provides a storage directory health check tool.
3. **Notifications Tab:** Configure Telegram or Bale notification bots with API token and Chat ID fields, plus a **Send Test Notification** button.
4. **Schedule Tab:** Enable automated monthly backup routines and define maximum storage retention thresholds.
5. **Installer Tab:** Configure default restoration preferences, security flags, and destination URL mapping defaults.
6. **Updates & Privacy Tab:** Check plugin version status, perform manual update checks, and verify Backupino's 100% telemetry-free zero data collection guarantee.

---

## 🧭 Next Step

To connect automated messaging bots for real-time backup notifications, proceed to:  
👉 [**Telegram Bot Setup Guide**](../03-integrations/01-telegram-bot.md)
