# 2. Timeout, 504 Gateway, and Memory Limit Troubleshooting

> **Section:** Troubleshooting • **Stable Version:** 1.0.1 GA • **Last Updated:** November 2026  
> **Target Audience:** Shared Hosting Users and Server Administrators

---

## 🛑 1. `504 Gateway Timeout` Error or Frozen Progress Bar

### Symptom:
During backup generation, the progress bar halts at a specific percentage, or the browser's Network tab reports a `504 Gateway Timeout` status returned by the web server.

### Root Cause:
Web servers such as LiteSpeed or Nginx enforce request execution timeouts (typically 30 to 60 seconds). If a single continuous PHP process exceeds this window, the web server terminates the gateway connection.

### Solutions:
1. **Automated Design and Intelligent Browser Heartbeat:**  
   Modern browsers throttle or freeze background tabs. Backupino features a dedicated `visibilitychange` listener; as soon as you refocus on the plugin tab, the connection actively resumes and dispatches the subsequent step. Even if a connection terminates abruptly, Backupino's resumable chunk-based engine continues processing tasks via segmented AJAX requests, and refreshing the page accurately reflects real-time job status.
2. **Reduce File Batch Size (Chunk Size):**  
   If your hosting environment has strict resource throttling, navigate to **Backupino → Settings → Archiving & Exclusions tab** and reduce the "Files per request batch" setting from 300 down to **100 or 150 files**.
3. **Increase Timeout Directives in `.htaccess`:**
   ```apache
   php_value max_execution_time 300
   php_value max_input_time 300
   ```

---

## 🛑 2. Memory Exhaustion Error `Allowed memory size of ... bytes exhausted`

### Symptom:
The standard PHP fatal error: `Fatal error: Allowed memory size of X bytes exhausted`.

### Prevention & Solutions:
1. **Built-in Memory Auto-Boost Mechanism:**  
   At the start of each scanning, archiving, and database extraction step, Backupino invokes WordPress's native `wp_raise_memory_limit('admin')` function to elevate the memory ceiling dynamically up to the maximum server threshold. This ensures out-of-memory errors are eliminated across 95% of hosting environments.
2. **Increase Memory in `wp-config.php` (for restricted environments):**  
   Add the following directives above the `/* That's all, stop editing! Happy publishing. */` line in your `wp-config.php`:
   ```php
   define( 'WP_MEMORY_LIMIT', '256M' );
   define( 'WP_MAX_MEMORY_LIMIT', '512M' );
   ```
3. **Increase Limits via `.htaccess` or `php.ini`:**
   ```ini
   memory_limit = 256M
   ```
4. **Exclude Large Files:**  
   In Backupino settings, enable the option to exclude media or archive files larger than 50 MB or 100 MB.

---

## 🧭 Next Steps

To resolve directory and file permission issues, see the next guide:  
👉 [**File and Directory Permissions Guide**](03-file-permissions.md)
