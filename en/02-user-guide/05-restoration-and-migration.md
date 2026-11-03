# 5. Comprehensive Restoration and Website Migration Guide

> **Section:** User Guide • **Stable Version:** 1.0.0 Official • **Last Updated:** November 2026  
> **Audience:** Web Designers, Freelancers, and Hosting System Administrators

---

## 🎯 Common Migration Scenarios

Backupino streamlines WordPress website migration into a straightforward 2-minute workflow. Below are three primary real-world deployment scenarios explained step-by-step:

---

## Scenario 1: Moving from Localhost (XAMPP / Laragon / LocalWP) to Live Hosting

### Objective:
You designed a client's website in a local development environment (e.g., LocalWP, Laragon, XAMPP, or WampServer) and need to deploy it to production cPanel, DirectAdmin, or a cloud VPS without breaking layouts, serialized database options, or asset URLs.

### Execution Steps:
1. **On your local environment:**
   * Open the local WordPress admin dashboard.
   * Generate a fresh full backup using Backupino.
   * Click **Download Both** to save both deployment files (`backupino-xxx.zip` and `installer.php`).
2. **On the production server (cPanel / DirectAdmin / VPS):**
   * Access the server File Manager or use SFTP.
   * Navigate to the target web root directory (e.g., `public_html`). Ensure the directory is empty.
   * Upload both files (`backupino-xxx.zip` and `installer.php`) into `public_html`.
   * In your hosting control panel, open **MySQL Databases**:
     * Create a new database (e.g., `mybrand_db`).
     * Create a dedicated database user with a secure password (e.g., `mybrand_usr`).
     * Assign the user to the database and grant **ALL PRIVILEGES**.
3. **Running the Standalone Installer:**
   * Open your browser and navigate to the standalone installer endpoint:  
     `https://yourdomain.com/installer.php`
   * Proceed through the 7-step deployment wizard:
     * **Step 1 (System Validation):** Automatic pre-flight verification of PHP version, ZipArchive extension, and directory write permissions.
     * **Step 2 (Database Connection):** Enter MySQL connection parameters (host, user, password, database) and click **Test Connection**.
     * **Step 3 (Database Options):** Configure character set and custom table prefix (e.g. `jvd_` or maintain source prefix). Backupino synchronizes all user capabilities and option prefix keys (`usermeta` / `options`), ensuring administrators are never locked out.
     * **Step 4 (Extraction & Import):** Progressively extracts files with automatic server configuration quarantine (`.htaccess.backupino-orig`) and streams the SQL dump without memory spikes.
     * **Step 5 (Search & Replace):** Automatically maps source URL (`http://localhost/site`) to the target URL (`https://yourdomain.com`). Deep search-and-replace parses JSON objects, preserves Elementor dynamic tags, and updates raw/encoded UTF-8 Persian slugs with string length corrections.
     * **Step 6 (Administrator Account):** Verify existing administrator credentials or optionally provision a fresh admin account with a custom password.
     * **Step 7 (Final Verification & Cleanup):** Click the green **Admin Login & Remove Installer Files** button. All temporary runtime files and archive packages are purged securely.

---

## Scenario 2: Changing Website Domain Names (Domain Rebranding)

### Objective:
Migrate an existing website from one domain to another (e.g., from `oldbrand.com` to `newbrand.com`) without causing 404 broken links, corrupt permalinks, or missing images.

### Execution Steps:
1. On the old domain, generate a full backup using Backupino and download both the archive file and `installer.php`.
2. On the new domain's hosting account, upload both files to the target web root directory.
3. Open `https://newbrand.com/installer.php` in your browser.
4. In Step 5 (URL & Path Replacement), the form automatically maps the old URL and new URL.
5. Click Next. Backupino's deep search-and-replace engine updates all database tables—correctly recalculating string length offsets in serialized PHP arrays and JSON payloads.

---

## Scenario 3: Creating a Staging Environment on a Subdomain

### Objective:
Establish an isolated, exact replica of your production website on a testing subdomain (e.g., `dev.mybrand.com`) to safely test updates and custom code before rolling them out live.

### Execution Steps:
1. In your hosting control panel, configure a subdomain named `dev.mybrand.com` (document root: `public_html/dev`).
2. Create an independent, empty MySQL database for the staging environment.
3. Upload the production backup archive and `installer.php` into the `public_html/dev` directory.
4. Navigate to `https://dev.mybrand.com/installer.php` and complete deployment pointing to the staging database.

---

## 🧭 Next Step

For an in-depth technical analysis of each of the 7 installer phases and quarantine safeguards, consult:  
👉 [**Anatomy of the Standalone Installer (`installer.php`)**](06-standalone-installer.md)
