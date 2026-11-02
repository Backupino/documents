# 1. Database and SQL Troubleshooting Guide

> **Section:** Troubleshooting • **Stable Version:** 1.0.0 GA • **Last Updated:** November 2026  
> **Target Audience:** Developers, Host Administrators, and Debuggers

---

## 🛠️ 1. `Got a packet bigger than 'max_allowed_packet' bytes` Error

### Symptom:
During database import in Step 3 of the Standalone Installer (`installer.php`), you encounter a connection loss or maximum packet size exceeded error. This error typically occurs on tables such as `wp_options` (with heavy transient records or Elementor cache).

### Root Cause:
The target MySQL server has a low threshold for the `max_allowed_packet` variable (for example, 1 MB or 4 MB), and a single database row containing large payloads exceeds this ceiling.

### Solutions:
1. **Backupino Automatic Mechanism:** Backupino's SQL streamer intelligently breaks down multi-row statements and batches them into safe packets.
2. **Increase the value on the MySQL server:**
   * In the MySQL configuration file (`my.ini` on Windows/Localhost or `/etc/mysql/my.cnf` on Linux) under the `[mysqld]` section, add the following line and restart the database server:
     ```ini
     max_allowed_packet = 64M
     ```
   * Or execute the following SQL query in phpMyAdmin with root privileges:
     ```sql
     SET GLOBAL max_allowed_packet = 67108864;
     ```

---

## 🛠️ 2. `Tablespace for table '...' exists. Please DISCARD the tablespace` Error

### Symptom:
While creating a new table in MariaDB or MySQL, you encounter the following error:
```text
Tablespace for table '`backupino_test`.`wp_backupino_jobs`' exists. Please DISCARD the tablespace before IMPORT
```

### Root Cause:
During previous import attempts, the process was abruptly aborted, or the table was dropped in the database metadata while the physical table file (`.ibd`) remained locked on the server disk and was not purged.

### Solutions:
1. **Backupino Automatic Recovery:** Upon encountering this error, Backupino's import engine automatically issues an `ALTER TABLE ... DISCARD TABLESPACE` command to clean up orphaned tablespace before re-importing.
2. **Manual Solution in phpMyAdmin:**
   * Run the following query:
     ```sql
     DROP TABLE IF EXISTS `wp_backupino_jobs`;
     ```
   * Or if needed, drop and recreate the test database entirely (`CREATE DATABASE ...`).

---

## 🛠️ 3. Foreign Key Error `errno: 121 Duplicate key on write or update`

### Symptom:
While creating a table with foreign key constraints, MySQL error code 121 is returned.

### Root Cause:
In MySQL, foreign key constraint names must be globally unique across the entire database server. If a previously existing database or another table uses the same constraint name, table creation fails.

### Solutions:
* Before initiating the database import, Backupino issues `SET FOREIGN_KEY_CHECKS = 0;` to temporarily disable constraint validation.
* If error 121 is encountered, the installer automatically rewrites the constraint identifier with a unique hash and retries the query.

---

## 🛠️ 4. `Duplicate entry '...' for key 'PRIMARY'` Error

### Symptom:
When resuming an import following a network disconnection or timeout, a primary key duplication error occurs on an already populated table.

### Solution:
* The Backupino importer detects the collision and intelligently converts the `INSERT INTO` statements into `INSERT IGNORE INTO` queries, preserving existing records and continuing to import the remaining data without interruption.

---

## 🧭 Next Steps

To troubleshoot 504 errors, request timeouts, and memory constraints, refer to the following guide:  
👉 [**Timeout, 504 Gateway, and Memory Limit Troubleshooting**](02-timeout-and-memory.md)
