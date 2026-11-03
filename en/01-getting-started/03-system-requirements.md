# 3. System Requirements & Server Compatibility

> **Section:** Getting Started • **Stable Version:** 1.0.1 GA • **Last Updated:** November 2026  
> **Target Audience:** System Administrators, Hosting Buyers, and WordPress Developers

---

## 💻 Hardware & Runtime Specifications

Backupino is engineered to operate efficiently with minimal server resources without requiring external server binaries or privileged system access. The table below outlines the minimum and recommended environments:

| Component | Minimum Required | Recommended |
|---|---|---|
| **PHP Version** | PHP 7.4 | PHP 8.1 / 8.2 / 8.3 / 8.4 |
| **WordPress Core** | WordPress 6.0 | WordPress 6.5 / 6.7+ |
| **MySQL / MariaDB** | MySQL 5.7 / MariaDB 10.2 | MySQL 8.0+ / MariaDB 10.6+ |
| **PHP Memory Limit** | 64 MB | 128 MB or 256 MB |
| **Max Execution Time (`max_execution_time`)** | 30 seconds | 60+ seconds (or 300s on shared hosting) |
| **Database Packet Size (`max_allowed_packet`)** | 16 MB | 64 MB or higher |

---

## 🧩 Required & Recommended PHP Extensions

During plugin activation and within the **System Health** tab of the Backupino settings panel, the following extensions are verified:

### Required Extensions:
1. **`pdo_mysql` or `mysqli`:** Used for secure database connections and row-by-row table streaming.
2. **`json`:** Required for serializing, parsing, and verifying package manifests and job state payloads.
3. **`zip` or internal `PclZip`:** Used for creating, appending, and extracting standard `.zip` archives.

### Recommended Extensions:
* **`mbstring`:** Ensures byte-accurate calculations during search-and-replace routines for non-ASCII, UTF-8, and multibyte character strings, preventing corrupted post slugs and broken layouts.
* **`openssl`:** Required for establishing secure HTTPS connections to dispatch webhook notifications (such as Telegram and Bale) and perform encrypted cloud transfers.
* **`curl`:** Enables reliable, high-performance HTTP requests within WordPress core APIs.

---

## 🌐 Web Server & Operating System Compatibility

Backupino is continuously tested and verified across a wide spectrum of production and development platforms:

* **Web Servers:**
  * Apache 2.4+ (with `mod_rewrite` enabled)
  * LiteSpeed and OpenLiteSpeed
  * Nginx (with PHP-FPM)
  * Microsoft IIS 8.5+
* **Server Operating Systems:**
  * Linux distributions (Ubuntu, Debian, CentOS, AlmaLinux, Rocky Linux, CloudLinux)
  * Windows Server and Windows 10/11 (for local development environments)
  * macOS (via Homebrew, Laravel Herd, or MAMP)
* **Hosting Control Panels:**
  * cPanel & WHM
  * DirectAdmin
  * Plesk
  * CyberPanel & aaPanel
  * Cloudways & RunCloud

---

## 🔒 File System Permissions

To ensure smooth archiving and standalone installer generation:
* The `wp-content/` directory must have standard write permissions: **`755`** (`drwxr-xr-x`) for directories and **`644`** for files.
* The internal storage directory `wp-content/backupino/` is automatically created with hardened security measures:
  * A `.htaccess` file containing `Deny from all` to block direct HTTP access to backup archives on Apache and LiteSpeed servers.
  * A blank `index.php` file to prevent web directory listing and index browsing across all web server environments.

---

## 🧭 Next Step

To proceed with installing and activating Backupino on your WordPress site:  
👉 [**Step-by-Step Installation & Setup Guide**](04-installation-guide.md)
