# 4. cPanel and DirectAdmin Hosting Troubleshooting Guide

> **Section:** Troubleshooting • **Stable Version:** 1.0.1 GA • **Last Updated:** November 2026  
> **Target Audience:** Site Builders and Shared Hosting Customers

---

## 🛠️ 1. Database Connection Errors (`Access Denied` or `Unknown Database`)

### Most Common Causes in cPanel & DirectAdmin:

#### 1. Missing Database or Username Prefix
In cPanel and DirectAdmin, database names and user accounts are almost always prefixed with your hosting account's username:
* If your hosting cPanel username is `royal` and you create a database named `site`, the actual full database name is **`royal_site`**, not merely `site`!
* When entering connection parameters in Step 2 of the Standalone Installer (`installer.php`), always supply the full identifier including prefix and underscore.

#### 2. User Not Assigned to the Database ("Add User to Database")
Creating a database and a user independently is not sufficient; the user must be explicitly granted privileges on the database:
1. In cPanel, navigate to the **MySQL Databases** section.
2. Scroll down to the **Add User To Database** module.
3. Select the created database user from the **User** dropdown and the target database from the **Database** dropdown, then click **Add**.
4. On the subsequent permissions screen, check **ALL PRIVILEGES** and click **Make Changes**.

#### 3. Database Host Name
In 99% of cPanel and DirectAdmin installations, the database host string is **`localhost`**. Avoid entering domain names or server IPs in the Host field unless your hosting provider explicitly specifies a remote/isolated MySQL cluster.

---

## 🛠️ 2. cPanel File Manager Upload Size Limits

If your backup archive is large (e.g., above 500 MB) and the web-based cPanel File Manager aborts or truncates the upload:
* Use an FTP/SFTP client such as FileZilla, which supports stream resuming and persistent socket connections.
* Alternatively, in Backupino settings, exclude bulky media files or video archives to reduce package weight.

---

## 🛠️ 3. LiteSpeed & Apache Internal Server Error (HTTP 500)

### Symptom:
During archive extraction in Step 4 of the standalone installer on cPanel/DirectAdmin servers powered by LiteSpeed Web Server or CloudLinux CageFS, an AJAX extraction request abruptly terminates with:
```text
CRITICAL: Extraction failed: Internal Server Error (HTTP 500)
```

### Root Cause:
WordPress backup archives contain sensitive web server configuration files from the source server, specifically `.htaccess`, `.user.ini`, `php.ini`, and `wp-config.php`. These files frequently contain environment-specific directives—such as custom PHP binary handlers (`AddHandler application/x-httpd-ea-php81`), absolute cache paths for LiteSpeed Cache, security module rules (e.g. Wordfence WAF auto-prepend), or custom rewrite rules tied to the old filesystem layout.  
If these files are directly extracted into the live document root during Step 4, the destination web server (especially LiteSpeed) parses the incompatible directives immediately, causing all subsequent incoming PHP requests—including the installer's own AJAX extraction chunks—to abort with HTTP 500.

### Backupino Safe Quarantine Extraction:
Backupino prevents this crash entirely through its **Safe Quarantine Extraction Architecture**:
1. During Step 4 extraction, environment-sensitive configuration files from the archive are automatically quarantined with a safe suffix:
   * `.htaccess` $\to$ `.htaccess.backupino-orig`
   * `.user.ini` $\to$ `.user.ini.backupino-orig`
   * `php.ini` $\to$ `php.ini.backupino-orig`
   * `wp-config.php` $\to$ `wp-config.php.backupino-orig`
2. Because these legacy directives remain quarantined, the installer completes all chunked AJAX extraction operations cleanly without triggering LiteSpeed or Apache 500 errors.
3. In Step 5, the installer writes a brand new, clean `wp-config.php` specifically configured for the target database and generates a standard WordPress `.htaccess` file.
4. If your source site had custom redirects or custom rewrite rules, `.htaccess.backupino-orig` is preserved on disk for manual inspection and verification.

---

## 🧭 Next Steps

To troubleshoot local development environments (XAMPP, Laragon, Docker), proceed to the following guide:  
👉 [**Local Development Environments Guide (Localhost)**](05-local-development.md)
