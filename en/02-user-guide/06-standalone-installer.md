# 6. Detailed Anatomy of the 5-Stage Standalone Installer (`installer.php`)

> **Section:** User Guide • **Stable Version:** 1.0.0 Official • **Last Updated:** November 2026  
> **Audience:** Developers, DevOps Engineers, and Website Administrators Performing Restorations

---

## 🧭 Modern Site Restoration Stepper Wizard

The `installer.php` file is an ultra-lightweight (~80 KB), standalone engineering script that requires zero existing WordPress footprint on the destination host. It delivers an intuitive user experience featuring a 5-stage interactive stepper wizard with bidirectional navigation:

---

### Step 1: Environment & Archive Verification

* **Core Prerequisites Audit:** Checks PHP version, ZipArchive/PclZip extensions, PDO/mysqli database drivers, and active memory allocation limits.
* **Filesystem Write Permissions:** Validates that the current target directory is writable (`is_writable`).
* **Automatic Archive Discovery:** The installer automatically scans the local directory for the matching `.zip` backup package, displaying its file size and metadata manifest attributes immediately.

---

### Step 2: Database Connection & Verification

* **Connection Parameters:**
  * Hostname (Database Host — typically `localhost` or custom port/socket)
  * Database Name
  * Database Username
  * Database Password
* **Test Connection Feature:**  
  Before continuing, click **Test Connection** to verify database connectivity, retrieve server engine versions (MySQL / MariaDB), and inspect existing table counts.
* **Clean Install Mode:**  
  If the destination database already contains existing tables, an explicit safety prompt allows you to empty or safely overwrite conflicting tables.

---

### Step 3: Archive Extraction & Database Streaming

* **Resumable Chunk-Based Archive Extraction:** Instead of attempting to extract tens of thousands of files in a single synchronous call, extraction is processed in manageable chunks (e.g., 300 files per cycle) with a live progress log, entirely preventing web server execution timeouts.
* **Chunked SQL Import Engine:**  
  * Executes `SET FOREIGN_KEY_CHECKS = 0` to eliminate foreign key constraint locks during batch restoration.
  * Streams database statements in 250-row chunks using an optimized 256 KB memory buffer with duplicate key handling (`INSERT IGNORE`).
  * **Comprehensive MySQL Views Compatibility:** Automatically strips incompatible `DEFINER` clauses and prepends `DROP VIEW IF EXISTS`, ensuring seamless import across servers with differing database users.
  * Dynamically resolves `Tablespace exists` conflicts on MariaDB and modern MySQL 8+.

---

### Step 4: Search & Replace and Domain Transformation

* **Automated URL & Path Detection:**  
  The source site URL/path from the archive manifest and the target host URL/path are automatically detected and populated in the input fields.
* **Deep Serializer Engine:**  
  Complex nested arrays stored within database options and metadata tables (particularly Elementor page builder data, sliders, widgets, and block settings) are recursively parsed, string occurrences replaced, and byte lengths re-serialized with mathematical precision.
* **Slug & Unicode Preservation:** Full support for non-Latin characters, UTF-8 multibyte strings, and URL-encoded slugs without corruption.
* **Cryptographic Salt Generation:** Generates a clean, cryptographically hardened `wp-config.php` file with fresh security authentication keys and salts.

---

### Step 5: Final Verification & Automated Security Cleanup

* Comprehensive summary report detailing restored file tallies, database records, and processing duration.
* Optional instant dispatch of restoration success alerts to Bale or Telegram bots (if configured in source settings).
* **Direct WordPress Admin Login:**  
  Clicking **Admin Login** securely launches your WordPress dashboard while automatically purging `installer.php` and runtime temporary deployment artifacts to maintain airtight server security.

---

## 🧭 Next Step

To explore the visual design and layout of the Backupino administrative dashboard, proceed to:  
👉 [**Visual Tour and UI Architecture Guide**](07-ui-tour.md)
