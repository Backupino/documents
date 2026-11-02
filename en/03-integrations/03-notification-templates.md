# 3. Customizing Notification Templates & Variable Tags

> **Section:** Integrations • **Stable Release:** 1.0.0 Official • **Last Updated:** November 2026  
> **Audience:** Web Designers, Developers & Webmasters

---

## 📝 Default Notification Templates in Backupino

Backupino provides standardized, production-ready templates for two primary lifecycle events:
1. **Backup Finished Notification:** Dispatched upon package completion; includes archive metadata, package scope, and download links.
2. **Migration & Restore Completed Notification:** Automatically triggered by the Standalone Installer (`installer.php`) the moment the site is deployed and verified on the destination host.

---

## 🏷️ Available Template Variables

You can customize notification message templates from the **Notifications tab** in settings using the following dynamic variable tags. Backupino automatically replaces these tags with live runtime parameters during dispatch:

| Variable Tag | Technical Description | Sample Rendered Output |
|---|---|---|
| `{site_name}` | Site title configured in WordPress General Settings | Royal Brand Store |
| `{site_url}` | Source website root URL | `https://example.com` |
| `{contents}` | Backup package scope | Files & Database |
| `{size}` | Formatted archive file size | `348.25 MB` |
| `{date}` | Completion timestamp (Jalali / Gregorian) | `2026-11-02 16:30` |
| `{download_url}` | Protected direct download link for package & installer | Secure Download Link |
| `{new_site_url}` | Destination domain URL after migration | `https://newdomain.com` |
| `{admin_url}` | Direct WordPress admin dashboard URL on the destination host | `https://newdomain.com/wp-admin/` |

---

## 💬 Sample Template: Backup Completion

```text
🎉 Backupino — Backup Completed: {site_name}

📦 Contents: {contents}
💾 File Size: {size}
📅 Date: {date}

📥 Download Package & Standalone Installer:
{download_url}
```

---

## 🚀 Sample Template: Migration & Restore Completion

```text
🚀 Backupino — Your website has been successfully migrated and restored!

🌐 New Site URL: {new_site_url}
🔑 Admin Dashboard: {admin_url}
📅 Restore Date: {date}
```

---

## 🎨 Link Formatting Mechanism Across Messengers

* **In Bale Messenger:** Messages are rendered using standard Markdown formatting. Links formatted as `[Direct Package Download]({download_url})` are rendered as clickable inline text.
* **In Telegram Messenger:** Messages are dispatched using strict HTML mode (`parse_mode=HTML`), with URLs and dynamic data safely escaped to avoid malformed links or entity parsing errors with special characters.

---

## 🧭 Next Step

To review technical feature comparisons between Backupino and other market solutions, proceed to the next section:  
👉 [**Backupino vs. Duplicator: Comprehensive Comparison**](../04-comparisons/01-vs-duplicator.md)
