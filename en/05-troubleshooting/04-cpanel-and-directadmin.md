# 4. cPanel and DirectAdmin Hosting Troubleshooting Guide

> **Section:** Troubleshooting • **Stable Version:** 1.0.0 GA • **Last Updated:** November 2026  
> **Target Audience:** Site Builders and Shared Hosting Customers

---

## 🛠️ 1. Database Connection Errors (`Access Denied` or `Unknown Database`)

### Most Common Causes in cPanel & DirectAdmin:

#### 1. Missing Database or Username Prefix
In cPanel and DirectAdmin, database names and user accounts are almost always prefixed with your hosting account's username:
* If your hosting cPanel username is `royal` and you create a database named `site`, the actual full database name is **`royal_site`**, not merely `site`!
* When entering connection parameters in Step 2 of the Standalone Installer (`installer.php`), always supply the full identifier including prefix and underscore.

#### 2. User Not Assigned to the Database ("Add User to Database")
Creating a database and a user independently is not sufficient; the user must be explicitly granted privileges on the database:
1. In cPanel, navigate to the **MySQL Databases** section.
2. Scroll down to the **Add User To Database** module.
3. Select the created database user from the **User** dropdown and the target database from the **Database** dropdown, then click **Add**.
4. On the subsequent permissions screen, check **ALL PRIVILEGES** and click **Make Changes**.

#### 3. Database Host Name
In 99% of cPanel and DirectAdmin installations, the database host string is **`localhost`**. Avoid entering domain names or server IPs in the Host field unless your hosting provider explicitly specifies a remote/isolated MySQL cluster.

---

## 🛠️ 2. cPanel File Manager Upload Size Limits

If your backup archive is large (e.g., above 500 MB) and the web-based cPanel File Manager aborts or truncates the upload:
* Use an FTP/SFTP client such as FileZilla, which supports stream resuming and persistent socket connections.
* Alternatively, in Backupino settings, exclude bulky media files or video archives to reduce package weight.

---

## 🧭 Next Steps

To troubleshoot local development environments (XAMPP, Laragon, Docker), proceed to the following guide:  
👉 [**Local Development Environments Guide (Localhost)**](05-local-development.md)
