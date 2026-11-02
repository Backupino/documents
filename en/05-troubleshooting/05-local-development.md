# 5. Local Development Environments Troubleshooting Guide (XAMPP, Laragon, Docker)

> **Section:** Troubleshooting • **Stable Version:** 1.0.0 GA • **Last Updated:** November 2026  
> **Target Audience:** Web Designers and Local Developers

---

## 💻 1. Restoring on Localhost: XAMPP and Laragon

When migrating or restoring a backup archive from live cPanel hosting to XAMPP or Laragon on Windows or macOS:

### 1. Default Database Credentials in XAMPP and Laragon:
* **Host:** `localhost` or `127.0.0.1`
* **Username:** `root`
* **Password:** *empty* (leave the password field completely blank).
* **Database Name:** The database name you created in your local phpMyAdmin (e.g., `backupino_test`).

### 2. Custom Web Server Ports:
If your local Apache or Nginx server runs on a non-standard port (such as 8080, 8081, or 8888):
* In Step 4 of the Standalone Installer (`installer.php`), provide the complete URL including port number:  
  `http://localhost:8080/myproject`
* The installer's search-and-replace engine accurately preserves and applies the port across serialized PHP metadata, option strings, and internal links.

---

## 🐳 2. Working in Docker and LocalWP Environments

* When utilizing Docker Compose stacks, the database host is typically the container service name (such as `db`, `mysql`, or `mariadb`), not `localhost`.
* Verify that the containerized PHP service has write permissions to the mounted web root volume.

---

## 🧭 Next Steps

To review common questions and answers, proceed to the FAQ section:  
👉 [**General Frequently Asked Questions (FAQ)**](../06-faq/01-general-faq.md)
