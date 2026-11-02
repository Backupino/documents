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
   * Proceed through the 5-step deployment wizard (enter new database credentials and test the connection).
   * In Step 4, the source URL (`http://localhost/site`) is auto-detected and pre-populated for replacement with your target live domain (`https://yourdomain.com`).
   * In Step 5, click **Admin Login**. The deployment wizard automatically purges installer runtime assets, leaving the live site production-ready.

---

## Scenario 2: Changing Website Domain Names (Domain Rebranding)

### Objective:
Migrate an existing website from one domain to another (e.g., from `oldbrand.com` to `newbrand.com`) without causing 404 broken links, corrupt permalinks, or missing images.

### Execution Steps:
1. On the old domain, generate a full backup using Backupino and download both the archive file and `installer.php`.
2. On the new domain's hosting account, upload both files to the target web root directory.
3. Open `https://newbrand.com/installer.php` in your browser.
4. In Step 4 (URL & Path Replacement), the form automatically maps the old URL and new URL.
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

For an in-depth technical analysis of each of the 5 installer phases, consult:  
👉 [**Anatomy of the Standalone Installer (`installer.php`)**](06-standalone-installer.md)
