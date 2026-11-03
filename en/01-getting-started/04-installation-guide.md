# 4. Step-by-Step Installation & Setup Guide

> **Section:** Getting Started • **Stable Version:** 1.0.1 GA • **Last Updated:** November 2026  
> **Methods:** WordPress Directory, Zip Upload, Manual FTP / File Manager, WP-CLI

---

## Method 1: Automatic Installation from WordPress Directory (Recommended)

The quickest and simplest installation method directly within your WordPress administration dashboard:

1. Log into your WordPress administrative dashboard.
2. In the sidebar menu, navigate to **Plugins → Add New Plugin**.
3. In the search box at the top right, enter **Backupino**.
4. In the plugin card, click **Install Now**.
5. Once installation finishes, click the blue **Activate** button.
6. The dedicated **Backupino** menu item will appear in your admin dashboard navigation.

---

## Method 2: Uploading Archive (.zip) via WordPress Admin

If you acquired the distribution package directly from GitHub or the official website:

1. Download the latest release package (e.g., `backupino-1.0.1.zip`).
2. In your WordPress admin dashboard, go to **Plugins → Add New Plugin**.
3. At the top of the screen, click the **Upload Plugin** button.
4. Click **Choose File** and select the downloaded `backupino-1.0.1.zip` file.
5. Click **Install Now**, and once extracted, click **Activate Plugin**.

---

## Method 3: Manual Installation via FTP or Hosting File Manager

For production environments where web-based plugin uploads are disabled for security reasons:

1. Extract the `backupino-1.0.1.zip` file on your local workstation to uncover the `backupino` directory.
2. Connect to your web server using an SFTP/FTP client (such as FileZilla) or your hosting control panel's File Manager.
3. Browse to the WordPress plugins directory:  
   `wp-content/plugins/`
4. Upload the extracted `backupino` directory into this location.
5. Log into your WordPress admin dashboard, navigate to **Plugins → Installed Plugins**, and click **Activate** under **Backupino**.

---

## Method 4: Rapid Deployment via Command Line (WP-CLI)

Ideal for DevOps engineers, headless Linux servers, and automated CI/CD workflows:

```bash
# Install and activate directly from the official WordPress directory:
wp plugin install backupino --activate

# Or install from a local zip package:
wp plugin install /path/to/backupino-1.0.1.zip --activate

# Verify plugin installation status and system health:
wp backupino status
```

---

## ✅ Initial Setup & Compatibility Check

After activating Backupino:
1. Click **Backupino** in the WordPress admin sidebar.
2. Navigate to **Settings → System Status** tab.
3. Verify that all prerequisite indicators (PHP version, PDO and Zip extensions, storage directory write permissions) display green **Pass** checkmarks.

---

## 🔄 Automatic Updates & Maintenance

Backupino strictly complies with official WordPress core repository standards and operates independently with zero third-party license servers:

* **Official Update Notifications:** Whenever a new version is released, standard WordPress update alerts appear under **Dashboard → Updates** as well as on the **Plugins** screen.
* **One-Click Updates:** Click **Update Now** to allow WordPress core to securely fetch and update files in place.
* **Background Auto-Updates (Optional):** In the **Installed Plugins** table, you can click **Enable auto-updates** to guarantee prompt deployment of future security enhancements and engine optimizations.

---

## 🧭 Next Step

With Backupino installed and verified, proceed to configure and generate your first backup archive:  
👉 [**Manual & Custom Backup Guide**](../02-user-guide/01-creating-backups.md)
