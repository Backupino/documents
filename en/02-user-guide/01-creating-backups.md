# 1. Backup Creation Guide (Manual & Custom)

> **Section:** User Guide • **Stable Version:** 1.0.0 Official • **Last Updated:** November 2026  
> **Audience:** General Users, Webmasters, and WordPress Administrators

---

## 🎯 Introduction and Backup Types

In Backupino, you can create three distinct backup types depending on your needs:
1. **Full Backup:** Includes all WordPress files (themes, plugins, media uploads, and core files) + Database + Standalone Installer (`installer.php`).
2. **Database Only:** An ultra-fast, lightweight package ideal before making configuration adjustments, publishing posts, or performing routine minor updates.
3. **Files Only:** Contains media and code assets without the database dump.

---

## 🚀 Step-by-Step Dashboard Backup Process

1. Log in to your WordPress dashboard.
2. In the left navigation menu, click **Backupino** to open the plugin's dashboard.
3. In the top card on the screen, configure the backup generation form:
   * **Include Files:** Checked by default.
   * **Include Database:** Checked by default for full backups.
   * **Optional Label:** Add a descriptive tag (e.g., `pre-woocommerce-update` or `autumn-stable-release`). This label is embedded in the archive filename for effortless future identification.
4. Click the blue **Create Backup** button.
5. The real-time progress card appears immediately, executing the following sequential stages with live percentages and status updates:
   * **Stage 1 — Scan:** High-speed recursive filesystem traversal and cataloging into an optimized manifest.
   * **Stage 2 — Database:** Pure PHP streaming dump utilizing a 256 KB memory buffer and 250-row batch inserts with zero performance degradation.
   * **Stage 3 — Files:** Adaptive chunk-based compression constrained by a dedicated execution time budget with accurate percentage reporting.
   * **Stage 4 — Finalize:** Archive sealing, manifest verification, and standalone installer injection.

> [!TIP]
> **Switch browser tabs without interruption!**  
> Backupino features an intelligent **Browser Heartbeat / Keep-Alive** mechanism. When you navigate to another browser tab, browsers typically throttle background JavaScript timers. Backupino immediately detects tab focus restoration, re-synchronizes communication, and seamlessly resumes processing without delay. Additionally, the PHP memory allocation is automatically elevated (`wp_raise_memory_limit`) during execution to prevent unexpected memory exhaustion.

---

## 🛑 Excluding Large Files and Directories

If your site contains heavy video folders, massive log files, or development directories like `node_modules`, you can easily exclude them to streamline package size and accelerate backup execution:

1. Navigate to **Backupino → Settings → Archive & Exclusions** tab.
2. Configure the following rules:
   * **Excluded Paths & Patterns (one per line):**
     * Directory example: `wp-content/uploads/videos/`
     * File pattern example: `*.mp4`, `*.zip`, `*.iso`, `*.tar.gz`
     * Diagnostic logs: `debug.log`, `error_log`
   * **Skip Files Larger Than (MB):**  
     Set a threshold such as `50` or `100` to automatically bypass files exceeding that size. (Set to `0` for unlimited).
   * **Batch File Processing Size:**  
     Default is 300 files per cycle. For resource-constrained shared hosting, reduce to 100; on high-performance dedicated servers, increase up to 1000.
3. Click **Save Changes**.

---

## 💻 Creating Backups via WP-CLI

For system administrators who prefer terminal or SSH automation:

```bash
# Create a full backup:
wp backupino create

# Create a full backup with a custom label:
wp backupino create --label="pre-release-v2"

# Create a fast database-only backup:
wp backupino create --db-only

# Create a files-only backup:
wp backupino create --files-only
```

---

## 🧭 Next Step

To learn how to manage existing backups, download archives, inspect real-time logs, and monitor disk quotas:  
👉 [**Backup Management, Live Logs, and Disk Cleanup**](02-backup-management.md)
