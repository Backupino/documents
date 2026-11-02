# 1. Introduction to Backupino & Why It Was Created

> **Section:** Getting Started • **Stable Version:** 1.0.0 GA • **Last Updated:** November 2026  
> **Target Audience:** Web Designers, WordPress Administrators, and PHP Developers

---

## 🎯 Why Was Backupino Created?

Backing up, cloning, and migrating WordPress websites have historically been among the most high-risk, stressful tasks for website administrators and developers. Legacy backup tools designed years ago routinely suffer from structural limitations and frustrating pitfalls:

### 1. Ransomware-Style Paywalls for Restores and Artificial Size Limits
Many third-party plugins allow you to export or back up your website for free. However, at the most critical juncture—when your website is down or when you are migrating to a new host—you are blocked by an artificial error: *"Your backup file exceeds the maximum import size of 2MB or 512MB"*, forcing you to purchase $69 to $99 paid extensions just to restore your own data.  
**In Backupino:** Restore and migration are 100% free forever, with no artificial file size caps. Multi-gigabyte websites are backed up and restored seamlessly without paywalls.

### 2. Crashes and 504 Gateway Timeout Errors on Shared Hosting
Budget-friendly shared hosting environments typically enforce strict script execution limits (`max_execution_time`) of 30 to 60 seconds and RAM caps of 128MB or 256MB. Most legacy plugins attempt to compress all files or heavy database tables in a single execution pass. When the server hits these limits, the process crashes with a 504 Gateway Timeout or memory exhaustion error.  
**In Backupino:** A Resumable Chunk-Based Engine processes tasks in controlled, multi-megabyte chunks across successive AJAX/background iterations. Even if a timeout or temporary network disconnection occurs, the engine resumes precisely where it left off.

### 3. Corruption of Unicode Slugs and Multibyte Data
During domain migration, search-and-replace routines must update serialized PHP strings. Many legacy plugins calculate string lengths using single-byte string functions rather than multibyte-aware logic. This breaks serialized arrays, destroys Elementor layouts, breaks theme widgets, and corrupts non-Latin / UTF-8 post slugs (`%d8%...`).  
**In Backupino:** The deep search-and-replace engine natively handles multibyte character encodings, nested serialized objects, and JSON strings, guaranteeing 100% data integrity.

### 4. Zero Requirement for Pre-Installing WordPress on Destination Hosts
Conventional workflows often force administrators to manually configure a database on the destination host, install WordPress, log into wp-admin, reinstall the backup plugin, and only then attempt an import.  
**In Backupino:** A self-contained Standalone Installer (`installer.php`) is packaged alongside your backup archive. Simply upload the archive package and `installer.php` into an empty server directory. The standalone wizard automatically handles archive extraction, database creation/import, and wp-config generation without requiring WordPress to exist beforehand.

### 5. Native Jalali Calendar and Messaging Integrations
Standard tools restrict notifications to standard email, which frequently lands in spam folders. Furthermore, native support for the Jalali (Solar Hijri) calendar is absent in international tools.  
**In Backupino:** Comprehensive support for both Gregorian and Jalali (Solar Hijri) calendars is built in, alongside instant notification delivery—featuring direct download links—to platforms like **Bale** and **Telegram**.

---

## 💎 Core Values & Commitments of Backupino

| Principle | Software Commitment |
|---|---|
| **Truly Free & Unlocked** | Backup, download, restore, and migration workflows remain 100% free forever with no file size restrictions. |
| **100% Offline-First Architecture** | Zero dependencies on external CDNs or third-party servers. Built for intranets, firewalled environments, and air-gapped systems. |
| **Automatic Disk Cleanup (Zero Garbage)** | Whether an operation completes successfully or is aborted, temporary files and staging chunks are immediately purged from the host. |
| **Enterprise-Grade Security** | Direct HTTP access to backup archives is blocked via `.htaccess` and `index.php`. The permanent latest-backup download link strictly enforces administrator privileges. |

---

## 🧭 Next Step

To explore how the chunking engine, pure PHP streamer, and storage layers operate under the hood, proceed to:  
👉 [**Technical Architecture & Core Engine Breakdown**](02-architecture.md)
