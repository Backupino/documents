# 3. Migration, Unicode & Non-Latin Slugs FAQ

> **Section:** Frequently Asked Questions • **Stable Version:** 1.0.1 Official • **Last Updated:** November 2026  
> **Target Audience:** Web Designers, SEO Specialists, and Site Operators

---

### Are Persian, Arabic, and non-Latin post slugs (`/مقاله-تستی/`) safely preserved during migration?
**Yes, 100% guaranteed.** Unlike legacy tools that corrupt non-Latin UTF-8 strings or replace multibyte Persian/Arabic characters with question marks (`???`), Backupino's database streaming engine operates directly with standard MySQL character encoding pipelines. It preserves percent-encoded characters, UTF-8/UTF8MB4 multibyte strings, and permalink structures without data corruption.

### What should I do if pages return a 404 Not Found error after migration?
This is a standard WordPress post-migration routing behavior when web server rewrite rules need regeneration:
1. Log in to your WordPress dashboard on the destination site.
2. Navigate to **Settings → Permalinks**.
3. Without modifying any settings, simply click the blue **Save Changes** button. This flushes rewrite rules and rebuilds the `.htaccess` / web server rewrite configuration. All pages will immediately resolve correctly.

### Will Elementor page layouts or serialized container designs break?
**No.** Elementor stores page layouts, styles, and builder settings inside serialized PHP strings and JSON payloads. Backupino's smart search-and-replace engine accurately recalculates serialized string byte lengths when updating site URLs and paths. Container hierarchies, sections, typography, and widget configurations remain 100% intact.

---

## 🧭 Next Steps

To explore the product roadmap and upcoming development milestones, proceed to:  
👉 [**Version 1.0.1 Official (Free) Feature Overview**](../07-roadmap/01-features-overview.md)
