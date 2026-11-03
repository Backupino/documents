# 2. Package Management, Live Logs, and Disk Cleanup

> **Section:** User Guide • **Stable Version:** 1.0.1 Official • **Last Updated:** November 2026  
> **Audience:** Website Administrators and Technical Operators

---

## 📋 Recent Backups Table

Beneath the backup creation form in the Backupino dashboard, the **Recent Backups** table displays all existing archive packages stored on the server with complete operational metadata:

| Column | Content & Functionality |
|---|---|
| **Created At** | Timestamp of backup completion, localized to Gregorian or Jalali (Solar Hijri) calendars based on site language settings. |
| **Status** | Standardized status badges (`Green = Complete`, `Blue = Running`, `Red = Failed`, `Gray = Cancelled`). Clicking a badge opens the execution log modal. |
| **Package Name** | Descriptive package identifier including timestamp, custom label, and scope type (omitting redundant domain prefixes for visual clarity). |
| **File Size** | Exact final archive size formatted cleanly in MB or GB (e.g., `337.19 MB`). |
| **Actions** | Quick action controls for downloading, inspecting logs, and secure deletion. |

---

## 📥 Download Options

The Actions column for each record provides flexible, convenient download options:

1. **Download Both Package & Installer (`Both`):**  
   Triggers a dual download in your browser, saving both essential migration files (`backupino-xxx.zip` and `installer.php`) simultaneously.
2. **Download Backup Package (`.zip`):**  
   Downloads only the primary archive file containing website code, media, and SQL dump.
3. **Download Installer (`installer.php`):**  
   Downloads only the standalone installer script.

> [!NOTE]
> The `installer.php` file is generated as a self-contained, universal deployment script engineered to run directly at the web root of any hosting environment without needing recompilation.

---

## 🔍 Live System Execution Log

For full operational transparency, Backupino records every file read, chunk boundary, error condition, start time, and completion timestamp:

1. In the Recent Backups table, click any badge in the **Status** column (e.g., `Complete` or `Running`).
2. A terminal-styled modal window appears.
3. The modal displays real-time, line-by-line event logs with precise timestamps:
   * Total scanned files and directories
   * Processed database tables and row counts
   * Peak PHP memory allocation
   * Archive package name and absolute storage path
4. Click the **Copy Log** button to copy the entire trace for diagnostic review or technical support submission.

---

## 🛑 Instant Backup Cancellation

If you need to halt an active backup process at any point:
1. In the active progress card at the top of the dashboard, click the red **Cancel Process** button.
2. Confirm the prompt when dialog appears.
3. The execution pipeline terminates immediately.
4. **Guaranteed Disk Cleanup:** Upon cancellation, all temporary chunks and scratch files in the `jobs` working directory are immediately purged, and the job status transitions to `Cancelled`. No orphaned files or wasted disk space remain on your hosting account.

---

## 🗑️ Safe Deletion of Obsolete Backups

1. Click the trash icon (Delete) in the Actions column for the desired backup package.
2. Confirm the prompt.
3. Backupino permanently removes the `.zip` archive, associated standalone installer file, and the corresponding database registry record safely and completely.

---

## 🧭 Next Step

To discover how to automate offsite downloads and integrations with persistent URLs, read the next chapter:  
👉 [**Permanent Latest-Backup Download Link**](03-permanent-download-link.md)
