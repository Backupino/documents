# 1. Database and SQL Troubleshooting Guide

> **Section:** Troubleshooting • **Stable Version:** 1.0.0 GA • **Last Updated:** November 2026  
> **Target Audience:** Developers, Host Administrators, and Debuggers

---

## 🛠️ 1. `Got a packet bigger than 'max_allowed_packet' bytes` Error

### Symptom:
During database import in Step 4 of the Standalone Installer (`installer.php`), you encounter a connection loss or maximum packet size exceeded error. This error typically occurs on tables such as `wp_options` (with heavy transient records or Elementor cache).

### Root Cause:
The target MySQL server has a low threshold for the `max_allowed_packet` variable (for example, 1 MB or 4 MB), and a single database row containing large payloads exceeds this ceiling.

### Solutions:
1. **Backupino Automatic Mechanism:** Backupino's SQL streamer intelligently breaks down large multi-row `INSERT` statements into micro-chunks and batches them into safe packets to prevent exceeding buffer limits.
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

## 🛠️ 2. `Tablespace for table '...' exists. Please DISCARD the tablespace` (InnoDB Error 1813)

### Symptom:
While creating a new table in MariaDB or MySQL during Step 4 of the installer, you encounter:
```text
❌ [ERROR]: Tablespace for table '`db_name`.`wp_table`' exists. Please DISCARD the tablespace before IMPORT
```

### Technical Cause:
InnoDB and XtraDB engines store individual tables in dedicated physical `.ibd` files. If previous test attempts were interrupted, or if tables were dropped in the database metadata while the physical files remained locked on disk, the MySQL engine refuses to create a new table under that name because an orphaned `.ibd` file exists on the filesystem without a dictionary catalog entry.

### Solutions:
1. **Backupino Automatic Recovery:** Upon detecting this condition, Backupino's import engine automatically issues an unblock sequence to discard the orphaned tablespace and re-attempt table creation:
   ```sql
   DROP TABLE IF EXISTS `wp_table`;
   ALTER TABLE `wp_table` DISCARD TABLESPACE;
   ```
2. **Control Panel / phpMyAdmin Solution:**
   * If you are performing test migrations into a temporary database, dropping the database completely and creating a fresh database with the same name clears all locked physical files.
   * On local development stacks (XAMPP/Laragon), ensure no stray background `mysqld.exe` processes hold open locks on the data directory.

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
