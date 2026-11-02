# 2. Security & Privacy FAQ

> **Section:** Frequently Asked Questions • **Stable Version:** 1.0.0 Official • **Last Updated:** November 2026  
> **Target Audience:** Security Specialists, Network Administrators, and DPOs

---

### Are backup files publicly accessible via the web or a browser?
**No.** Backup archives are stored in `wp-content/backupino/packages/`. This path is automatically hardened by multiple strict security layers:
1. **`.htaccess` file** configured with `Options -Indexes` and `Require all denied` (completely blocks HTTP web requests and directory browsing on Apache and LiteSpeed).
2. **Dedicated `web.config` file** with `<deny users="*" />` rules for Windows and IIS servers.
3. **Execution blocking** for all executable extensions (`.php`, `.py`, `.cgi`, etc.) inside the backup directory, preventing remote code execution even if unauthorized server access occurs.
4. **Blank `index.php` file** to prevent directory listing fallthrough.
5. **Smart fallback mechanism**: If `wp-content/` is read-only on restrictive shared hosting environments, storage automatically and securely falls back to `uploads/backupino/` to ensure operations succeed seamlessly.

### Can attackers invoke the plugin's PHP source files directly via a browser?
**No.** Every single PHP source file in `src/` enforces a strict guard clause: `defined( 'ABSPATH' ) || exit;`. Direct web requests terminate execution immediately with a blank response. Standalone installer component files are likewise protected with a dedicated `defined( 'BACKUPINO_INSTALLER' )` guard.

### Can the permanent download link secret token be brute-forced?
**No.** The download security token is generated as a cryptographically secure 32-byte high-entropy string and compared using the timing-attack-safe `hash_equals()` function. Furthermore, the built-in rate limiter blocks client IPs after 5 consecutive failed attempts within a 10-minute window, returning an HTTP `429 Too Many Requests` response.

### Are REST API endpoints and admin panel actions protected against CSRF?
**Yes.** All sensitive AJAX and REST API endpoints verify WordPress admin capabilities (`manage_options`) and validate standard WordPress security nonces (`X-WP-Nonce: wp_rest`) to eliminate Cross-Site Request Forgery (CSRF) vectors.

### Does the plugin transmit telemetry, statistics, or site metadata to external servers?
**No, never.** Backupino is engineered on a 100% Offline-First Architecture. No telemetry data, email addresses, database statistics, or analytics are sent to any remote server without your explicit consent.

### Are external CDNs used for frontend styles, fonts, or scripts?
**No.** All CSS files, JavaScript bundles, fonts, and icons are bundled locally within the plugin package. The plugin never requests external CDNs that could be blocked, censored, or throttled by regional networks or firewalls, ensuring full compatibility in restricted intranet and national network environments.

### How are Telegram and Bale bot tokens secured?
Bot tokens are securely stored in the WordPress database and are never printed in public debug logs or exposed in API responses. They are strictly transmitted as authorization headers directly to the messaging provider's API during notification dispatch.

---

## 🧭 Next Steps

For questions regarding Unicode character sets, multibyte strings, and non-Latin slugs, proceed to:  
👉 [**Migration, Unicode & Non-Latin Slugs FAQ**](03-migration-and-unicode.md)
