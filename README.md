# 📦 Backupino Official Documentation
### Modern, Resumable & Self-Contained WordPress Backup, Cloning & Easy Migration Platform

<div align="center">

[![Version](https://img.shields.io/badge/version-1.0.1--stable-blue.svg?style=for-the-badge)](https://github.com/Backupino/plugin)
[![WordPress](https://img.shields.io/badge/WordPress-6.0%20--%207.1-21759b.svg?style=for-the-badge&logo=wordpress)](https://wordpress.org)
[![PHP](https://img.shields.io/badge/PHP-7.4%20--%208.4-777bb4.svg?style=for-the-badge&logo=php)](https://php.net)
[![License](https://img.shields.io/badge/License-GPL--2.0--or--later-green.svg?style=for-the-badge)](https://www.gnu.org/licenses/gpl-2.0.html)
[![Plugin Check](https://img.shields.io/badge/Plugin%20Check-100%25%20Passed-success.svg?style=for-the-badge)](https://wordpress.org)
[![Offline First](https://img.shields.io/badge/Architecture-100%25%20Offline--First-orange.svg?style=for-the-badge)](#100-offline-first-architecture)

[Plugin Source](https://github.com/Backupino/plugin) • [Documentation Portal](https://github.com/Backupino/documents) • [WordPress Profile](https://profiles.wordpress.org/backupino/)

**Language**: **English (Default)** | [راهنمای فارسی (Persian)](fa/README.md)

</div>

---

## 🌟 About Backupino Documentation

Welcome to the central technical documentation and knowledge base for **Backupino**.  
This repository serves as the official handbook, user guide, migration playbook, architectural specification, and troubleshooting encyclopedia for site owners, DevOps engineers, web agencies, and WordPress professionals worldwide.

Backupino was engineered around one core philosophy:  
**"Eliminating paywalls for site restoration, defeating timeout crashes on real-world shared hosting, and delivering an ultra-fast, 100% offline-first migration experience."**

---

## 🗂 Documentation Atlas & Table of Contents

All guides are organized into 6 structured sections:

### 1. Getting Started
* [**01. Introduction & Philosophy**](en/01-getting-started/01-introduction.md) — Why Backupino was built, design philosophy, and core advantages.
* [**02. Technical Architecture**](en/01-getting-started/02-architecture.md) — The resumable chunk engine, pure PHP SQL streamer, and checkpoint state machines.
* [**03. System Requirements & Compatibility**](en/01-getting-started/03-system-requirements.md) — PHP versions, required modules, database drivers, and server permissions.
* [**04. Installation & Setup Guide**](en/01-getting-started/04-installation-guide.md) — Dashboard upload, ZIP installation, FTP deployment, and WP-CLI commands.

### 2. User Guide & Core Features
* [**01. Creating Backups**](en/02-user-guide/01-creating-backups.md) — Full backup, database-only, files-only, and custom exclusion filters.
* [**02. Backup Management & Live Logs**](en/02-user-guide/02-backup-management.md) — Monitoring job stages, inspecting live runtime logs, and instant cancellation.
* [**03. Permanent Latest-Backup Download Link**](en/02-user-guide/03-permanent-download-link.md) — 32-byte secret key security, admin authentication, and automated off-site scripts.
* [**04. Automated Scheduling & Retention Policies**](en/02-user-guide/04-scheduling-and-retention.md) — Monthly automated cron routines, Jalali calendar alignment, and package pruning.
* [**05. Site Restoration & Migration Playbook**](en/02-user-guide/05-restoration-and-migration.md) — Moving from localhost to live server, domain switching, staging clones, and cross-host migration.
* [**06. Standalone Installer (`installer.php`) Guide**](en/02-user-guide/06-standalone-installer.md) — Deep dive into the 7-step installer wizard, URL rewriting, server config quarantine, and salt generation.
* [**07. Admin UI Tour**](en/02-user-guide/07-ui-tour.md) — Complete overview of dashboard cards, tab navigation, and settings switches.

### 3. Messenger Integrations & Alerts
* [**01. Telegram Bot Integration**](en/03-integrations/01-telegram-bot.md) — Creating bots via @BotFather, extracting Chat IDs, and secure message dispatch.
* [**02. Bale Messenger Integration**](en/03-integrations/02-bale-bot.md) — Configuring Bale bot tokens, local network delivery, and domestic intranet alerts.
* [**03. Notification Templates & Retry Queues**](en/03-integrations/03-notification-templates.md) — Customizing Markdown alerts, token placeholders, and the 3-attempt fallback queue.

### 4. Comparisons & Benchmarks
* [**01. Backupino vs. Duplicator Lite**](en/04-comparisons/01-vs-duplicator.md) — Comparison of database limits, background chunking, and memory handling.
* [**02. Backupino vs. UpdraftPlus Free**](en/04-comparisons/02-vs-updraftplus.md) — Comparison of standalone offline restoration versus core-dependent restores.
* [**03. Backupino vs. All-in-One WP Migration**](en/04-comparisons/03-vs-all-in-one-wp.md) — Comparison of free upload/restore limits and file size restrictions.
* [**04. Comprehensive Feature Matrix**](en/04-comparisons/04-comprehensive-matrix.md) — Head-to-head technical comparison across 25+ parameters.

### 5. Troubleshooting & Playbooks
* [**01. Database & SQL Issues**](en/05-troubleshooting/01-database-and-sql.md) — Resolving `max_allowed_packet`, foreign key constraints, character sets, and corrupted views.
* [**02. Timeouts & Memory Optimization**](en/05-troubleshooting/02-timeout-and-memory.md) — Dealing with 30s FastCGI timeouts, `memory_limit` exhaustion, and slice tuning.
* [**03. File Permissions & Directory Ownership**](en/05-troubleshooting/03-file-permissions.md) — Recommended 755/644 permissions, `wp-content` storage access, and read-only host fallbacks.
* [**04. cPanel, DirectAdmin & Shared Hosting**](en/05-troubleshooting/04-cpanel-and-directadmin.md) — Tuning LiteSpeed, CloudLinux CageFS, Nginx reverse proxies, and OPcache.
* [**05. Localhost Development (XAMPP, Laragon, Docker)**](en/05-troubleshooting/05-local-development.md) — Testing migrations locally, socket paths, and database users.

### 6. Frequently Asked Questions (FAQ)
* [**01. General FAQ**](en/06-faq/01-general-faq.md) — Common questions about limits, multisite support, and pricing.
* [**02. Security & Privacy FAQ**](en/06-faq/02-security-and-privacy.md) — Package folder protection, brute-force rate limiting, and zero-telemetry architecture.
* [**03. Migration & Unicode FAQ**](en/06-faq/03-migration-and-unicode.md) — Handling RTL text, emojis, Cyrillic/Persian/Arabic slugs, and serialized PHP structures.

---

## 🏷️ Custom Versioning Specification

Backupino adheres to a precise, customized versioning scheme across all source releases and official documentation:

$$\mathbf{Major} \,.\, \mathbf{Minor} \,.\, \mathbf{Patch}$$

1. **Patch Component (Rightmost — Bug Fixes & Refinements):**
   * Strictly bounded to single digits **0 through 9**.
   * Rolling over past `9` resets Patch to `0` and increments Minor:
     $$\mathbf{1.0.0} \to \mathbf{1.0.1} \to \dots \to \mathbf{1.0.9} \implies \mathbf{1.1.0}$$
2. **Minor Component (Middle — Feature Iterations & Enhancements):**
   * **Unbounded** ($0 \dots \infty$). Progresses seamlessly beyond single digits:
     $$\mathbf{1.9.9} \implies \mathbf{1.10.0} \implies \mathbf{1.10.1} \dots \implies \mathbf{1.25.0}$$
3. **Major Component (Leftmost — Foundational Architectural Overhauls):**
   * Bounded between **1 and 9**. Increments exclusively upon fundamental architectural redesigns.

---

## ⚡ Architectural Highlights

| Feature | Technical Implementation |
| :--- | :--- |
| **Anti-Timeout Engine** | Slices heavy jobs into incremental micro-batches, resuming seamlessly from exact database checkpoints. |
| **Browser Heartbeat** | Listens to `visibilitychange` to maintain background processing across inactive browser tabs. |
| **Multi-Layer Security** | Protected by Rate Limiting on permanent links (HTTP 429 after 5 failures), REST nonces, and `.htaccess`/`web.config` locks. |
| **Auto Memory Escalation** | Safely calls `wp_raise_memory_limit('admin')` during intensive scanning and compression stages. |
| **Standalone Installer** | Requires zero pre-installed WordPress core on destination hosts; `installer.php` rebuilds everything. |
| **Smart Permanent Link** | Static URL for fetching latest backups with strict administrator capability checks (`manage_options`). |
| **Dual Messenger Dispatch** | Instant alerts to Telegram and Bale with formatted file sizes, execution times, and download links. |
| **Dual Calendar Support** | Solar Hijri (Jalali) calculations for Persian locales and Gregorian for international setups. |
| **100% Offline-First** | Zero remote scripts, zero CDN dependencies, zero external fonts. Completely safe for intranets. |

---

## 🤝 Community & Support

* **WordPress.org Profile:** [profiles.wordpress.org/backupino](https://profiles.wordpress.org/backupino/)
* **Plugin Source Repository:** [github.com/Backupino/plugin](https://github.com/Backupino/plugin)
* **Documentation Repository:** [github.com/Backupino/documents](https://github.com/Backupino/documents)
* **Bug Reports & Issues:** [GitHub Issues](https://github.com/Backupino/plugin/issues)
* **Persian Documentation:** [راهنمای فارسی مستندات](fa/README.md)
