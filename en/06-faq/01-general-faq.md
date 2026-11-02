# 1. General FAQ

> **Section:** Frequently Asked Questions • **Stable Version:** 1.0.0 Official • **Last Updated:** November 2026  
> **Target Audience:** All Users and Site Administrators

---

### Does the free version impose size limits, database size caps, or file count quotas?
**No, absolutely not.** Backupino Free does not impose any artificial size limits (such as 2 MB or 512 MB) or restrictions on the number of files or database records. The system operates reliably and without paywalls for everything from small business websites to massive, product-heavy WooCommerce online stores.

### Is there any charge for restoring or migrating a package?
**No, restore and site cloning are 100% free forever.** One of the primary motivations behind creating Backupino was to put an end to the unfair business model of offering free exports while demanding payment to restore your own site.

### Do I need WordPress pre-installed on the destination host to restore with `installer.php`?
**No.** `installer.php` is a standalone, lightweight, self-contained installer script. You can place it alongside your backup ZIP archive into a completely empty directory on the destination server and run it; the standalone installer extracts files, sets up the database, and generates `wp-config.php` entirely from scratch.

### Is Backupino compatible with WooCommerce stores?
**Yes, 100% compatible.** Orders, customer accounts, product metadata, and custom WooCommerce database tables are packaged and restored flawlessly without data loss.

### Will hosting disk space fill up if a backup is cancelled or interrupted?
**No.** Backupino features a Zero-Leftover Guarantee. All temporary files in the `jobs/` directory are immediately purged and cleaned up upon job completion or cancellation.

---

## 🧭 Next Steps

For security and privacy inquiries, proceed to:  
👉 [**Security & Privacy FAQ**](02-security-and-privacy.md)
