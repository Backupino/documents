# 3. File and Directory Permissions Troubleshooting

> **Section:** Troubleshooting • **Stable Version:** 1.0.1 GA • **Last Updated:** November 2026  
> **Target Audience:** Linux Administrators, Webmasters, and Server Support Teams

---

## 🔒 1. `Root directory is not writable` Error in Installer

### Symptom:
In Step 1 of the Standalone Installer (`installer.php`), the requirements check fails with a red warning indicating that the web server root directory is not writable.

### Root Cause:
The web server execution user (such as `nobody`, `www-data`, or `cpanel_user`) lacks write permissions to create files and directories in the document root directory.

### Solutions:
1. **Verify Directory Permissions:**  
   In your hosting File Manager, inspect the permissions of the `public_html` directory. It must be set to **`755`** (or `775` on certain group-managed setups).
2. **Correct Ownership on Linux / VPS / Dedicated Servers:**
   ```bash
   # For cPanel / DirectAdmin shared environments:
   chown -R cpaneluser:cpaneluser /home/cpaneluser/public_html
   chmod 755 /home/cpaneluser/public_html

   # For raw Apache / Nginx setups:
   chown -R www-data:www-data /var/www/html
   chmod -R 755 /var/www/html
   ```

---

## 🔒 2. Archive Write Failure (`Could not write the package file`)

### Symptom:
During the archive compression step in the WordPress dashboard, the job halts reporting that writing to the disk storage failed.

### Solutions:
1. Ensure `wp-content/` permissions are set to `755` so that the `wp-content/backupino/` storage directory can be created automatically without errors.
2. Verify that your hosting account has not exceeded its disk quota (`Disk Space 100% Full`).
3. In the Backupino settings panel under the Server Health tab, check the available free disk space.

---

## 🧭 Next Steps

For panel-specific configurations for cPanel and DirectAdmin, consult the following guide:  
👉 [**cPanel and DirectAdmin Hosting Configuration Guide**](04-cpanel-and-directadmin.md)
