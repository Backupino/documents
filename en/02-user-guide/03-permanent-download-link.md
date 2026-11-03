# 3. Permanent Latest-Backup Download Link

> **Section:** User Guide • **Stable Version:** 1.0.1 Official • **Last Updated:** November 2026  
> **Audience:** WordPress Administrators, Automation Engineers, and Server Script Developers

---

## 🔗 What Is the Permanent Download Link?

In conventional backup solutions, generating a new backup creates a dynamically named archive timestamped with random characters. Consequently, administrators utilizing external automation scripts (such as Bash, Python, or remote server cron jobs) to download the latest backup to offsite storage or secondary cold storage must continually poll and extract the newest filename manually.

Backupino resolves this operational friction with the **Permanent Latest-Backup Download Link**:
```text
https://yourdomain.com/?backupino_download=latest&backupino_key=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

This persistent URL endpoint:
* **Never expires.**
* Always resolves to the **latest verified, successful backup package**.
* Directly streams the zip archive utilizing standard `Content-Disposition: attachment` response headers.

---

## 🔒 Multi-Layer Security Architecture

To guarantee strict defense against unauthorized data exfiltration, access to this endpoint is guarded by multi-layer security controls:

1. **High-Entropy 32-Byte Secret Key with Constant-Time Verification:**  
   Only requests bearing the valid secret key parameter are processed. The cryptographic token is generated with high entropy, and token validation is enforced using PHP's constant-time comparison `hash_equals()` to prevent timing-attack side-channel vulnerabilities.
2. **Brute-Force Rate Limiting:**  
   If an unauthorized client attempts to brute-force the secret key, any 5 consecutive failed attempts will trigger an automatic 10-minute IP block, returning HTTP status `429 Too Many Requests`.
3. **Mandatory Administrative Session Validation:**  
   Even if the secret key is leaked, Backupino enforces WordPress administrative session checks:
   * **Unauthenticated Requests (Guests):** The request is immediately redirected to the WordPress login screen (`wp-login.php`). Upon successful authentication, the file download begins instantly.
   * **Authenticated Non-Administrators:** Users lacking the `manage_options` capability are denied access with an HTTP `403 Forbidden` response.
4. **Web Server Directory Protection (`.htaccess` & `index.php`):**  
   Direct directory browsing or raw file downloads from `/wp-content/backupino/` are blocked at the web server level (`Options -Indexes` and strict deny rules). File retrieval is exclusively handled via the authenticated PHP streaming pipeline.
5. **Instant Key Regeneration:**  
   If you suspect your key has been compromised, simply regenerate or update the token in the plugin settings. The previous download URL becomes invalid immediately.

---

## 🤖 Integration with Remote Automation Scripts

To pull the latest backup automatically via remote automation scripts or external servers, provide the authenticated WordPress administrator cookie with the request:

```bash
# Example: Automated download via cURL using authenticated admin cookies:
curl -b "wordpress_cookie_file.txt" -L -o "latest-backup.zip" \
  "https://yourdomain.com/?backupino_download=latest&backupino_key=YOUR_SECRET_KEY"
```

---

## 🧭 Next Step

To set up recurring automatic backup schedules and storage retention rules, proceed to:  
👉 [**Automated Scheduling and Retention Policies**](04-scheduling-and-retention.md)
