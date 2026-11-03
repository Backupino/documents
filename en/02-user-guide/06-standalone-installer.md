# 6. Detailed Anatomy of the Standalone Installer (`installer.php`)

> **Section:** User Guide • **Stable Version:** 1.0.1 Official • **Last Updated:** November 2026  
> **Audience:** Developers, DevOps Engineers, and Website Administrators Performing Restorations

---

## 🧭 Modern Self-Contained Site Restoration Wizard

Backupino's standalone installer script is an ultra-lightweight (~80 KB) engineering solution that requires zero existing WordPress footprint on the destination server. Built upon a resilient chunked-processing architecture (AJAX ticks), it eliminates PHP execution timeouts and memory exhaustion across large enterprise sites:

### 📦 Dual File Naming for User Convenience
1. **`installer.php`**: The file downloaded directly from the WordPress Admin Dashboard via the "Download Installer" button, or copied from the packages folder.
2. **`[site]_[timestamp]-installer.php`**: The timestamped file stored automatically in `wp-content/backupino/packages/` alongside the archive, ensuring multiple backup packages within a directory never collide.
> Both files are **100% byte-for-byte identical** in content and capability.

---

### Step 1: Environment & Archive Verification
* **System Prerequisites Audit:** Checks PHP version (PHP 7.4 through 8.4+), required extensions (`ZipArchive`/`PclZip`, `mysqli`, `pdo_mysql`), and memory limits.
* **Filesystem Write Permissions:** Validates that the current target directory is fully writable (`is_writable`).
* **Cryptographic Token & Hash Pairing:** Scans for the matching `.zip` archive, pairing the embedded 32-character security token and SHA-256 archive hash to eliminate package mismatch risks.

---

### Step 2: Database Connection & Prefix Customization
* **Database Parameters:** Hostname (including port/socket), Database Name, Username, and Password.
* **Custom Table Prefix:** Option to retain the existing prefix or set an entirely new prefix (e.g., changing from `wp_` to `custom_`); Backupino automatically updates table names, views, and prefix-dependent options (`wp_user_roles`, `wp_capabilities`).
* **Test Connection:** Live connectivity check reporting database engine version (MySQL / MariaDB) and table count.
* **Clean Install / Empty DB:** Safely drops pre-existing conflicting tables and views if clean installation is selected.

---

### Step 3: Chunked File Extraction & Web Server Quarantine
* **Slice-Based Extraction (300 files/tick):** Extracts tens of thousands of files across small synchronous requests, guaranteeing web server execution limits are respected.
* **🛡️ Smart Server Config Quarantine (Zero 500 Server Errors):**
  * On shared Linux servers running LiteSpeed or Apache (cPanel, DirectAdmin, CloudLinux), extracting the source site's `.htaccess`, `.user.ini`, `php.ini`, and `wp-config.php` immediately can trigger severe **500 Internal Server Errors** due to conflicting PHP handlers (`ea-php81`), LiteSpeed Cache directives, or outdated WAF prepend paths.
  * Backupino automatically quarantines these configuration files during extraction as `.backupino-orig`, guaranteeing that the web server remains 100% stable throughout the entire migration wizard.

---

### Step 4: Resilient SQL Import & InnoDB Tablespace Recovery
* **Packet Size Auto-Splitting:** Large multi-row `INSERT` statements exceeding the database's `max_allowed_packet` are dynamically split into micro-statements without corrupting data tuples.
* **MariaDB & MySQL 8+ Error Resilience:**
  * Automatically recovers from MariaDB orphan tablespace collisions (`Tablespace exists - Error 1813`).
  * Enforces `SET FOREIGN_KEY_CHECKS = 0` and unique check disabling.
  * Automatically sanitizes incompatible `DEFINER` clauses and handles views gracefully.

---

### Step 5: Deep Search & Replace, Elementor Tags & Persian Slugs
* **Automated URL Mapping:** Detects source site URL and target domain automatically.
* **Deep Serializer Engine:**
  * Recursively unpacks nested PHP serialized strings, updating URLs and recalculating byte-length descriptors accurately.
  * Traverses and rewrites JSON-encoded strings.
  * **Elementor Dynamic Tag Preservation:** Perfectly preserves URL-encoded JSON dynamic tag syntax (`settings="%7B%7D"`).
  * **Persian & Unicode Slug Preservation:** Preserves non-Latin UTF-8 slugs in `post_name` and URL paths without corruption or loss.

---

### Step 6: WordPress Configuration & Standard `.htaccess` Generation
* **Fresh `wp-config.php` Generation:** Synthesizes clean configuration with cryptographically secure random authentication salts while preserving custom user-defined constants from the source config.
* **Standard `.htaccess` Generation:** Dynamically writes a standard WordPress `.htaccess` rule set configured with the exact `RewriteBase` matching the target directory (root or subdirectory).
* **Custom Login Slug Detection:** Automatically detects customized login endpoints configured by security plugins (WPS Hide Login, AIOWPS, etc.).

---

### Step 7: Final Report, Security Cleanup & Direct Admin Login
* Comprehensive statistics display: extracted files, executed SQL queries, and updated database fields.
* Sends automated notification to Bale or Telegram bots if enabled.
* **Delete Installer Files & Login:** Safely purges the installer script, archive zip, SQL dump, state files, and all quarantined `.backupino-orig` files before redirecting to the WordPress login screen.

---

## 🧭 Next Step

To explore the visual design and layout of the Backupino administrative dashboard, proceed to:  
👉 [**Visual Tour and UI Architecture Guide**](07-ui-tour.md)
