# 1. Technical Comparison: Backupino vs. Duplicator

> **Section:** Comparisons • **Stable Version:** Official 1.0.0 • **Last Updated:** November 2026  
> **Target Audience:** Web Designers, Developers, and Hosting Administrators

---

## ⚖️ Overview

The **Duplicator** plugin is one of WordPress's oldest site cloning and package generation tools. However, because its core architecture was engineered over a decade ago, it encounters multiple technical bottlenecks and constraints on modern servers and shared hosting environments.

---

## 🥊 Key Differences

### 1. Stability on Budget and Shared Hosting (Timeout Resilience)
* **Duplicator:** Performs file archiving and compression in large, monolithic blocks. If the hosting server enforces strict 30- or 60-second PHP execution limits, it frequently hits 504 Gateway Timeout or server errors around 60%–70% progress and halts abruptly.
* **Backupino:** Features a proprietary **Resumable Chunk-Based Engine** that packages files in 300-item micro-batches while recording sequential checkpoints; consequently, it completes successfully without errors even on severely resource-constrained shared hosts.

### 2. Footprint and Architecture of the Standalone Installer (`installer.php`)
* **Duplicator:** Duplicator's installer package is relatively heavy (often several megabytes) and unpacks hundreds of temporary files and subdirectories into the hosting webroot.
* **Backupino:** Features an ultra-lightweight **Standalone Installer (`installer.php`)** (~80 KB), executes as a self-contained single file, and automatically purges all temporary installer artifacts and itself from the server upon deployment completion.

### 3. User Experience and Dashboard Advertising (No-Ads Policy)
* **Duplicator:** The free version dashboard is saturated with upgrade banners pushing "Duplicator Pro", Black Friday promotions, notices, and persistent upsell banners.
* **Backupino:** Delivers a modern, clutter-free, 100% ad-free interface fully compliant with official WordPress.org guidelines.

### 4. Instant Messaging Notifications & Jalali Calendar Support
* **Duplicator:** Does not provide mobile messenger notifications (limited strictly to standard email delivery) and lacks native Jalali (Solar Hijri) calendar support.
* **Backupino:** Features automated instant dispatch of backup and migration completion alerts via **Bale** and **Telegram**, alongside native Jalali calendar scheduling for precise automated backups on the first day of each Solar Hijri month.

---

## 🧭 Next Step

To review the detailed comparison against UpdraftPlus, proceed to the following guide:  
👉 [**Backupino vs. UpdraftPlus Side-by-Side Comparison**](02-vs-updraftplus.md)
