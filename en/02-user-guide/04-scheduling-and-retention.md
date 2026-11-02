# 4. Automated Scheduling and Retention Policies

> **Section:** User Guide • **Stable Version:** 1.0.0 Official • **Last Updated:** November 2026  
> **Audience:** Website Administrators and System Architects

---

## ⏰ Automated Monthly Scheduling

A robust backup strategy must operate autonomously without requiring continual manual intervention. Backupino features an intelligent monthly scheduling engine built on top of WordPress's native `wp_cron` subsystem.

### Enabling the Schedule:
1. In your WordPress dashboard, navigate to **Backupino → Settings → Scheduling** tab.
2. Toggle the switch to **Enable Automatic Backups**.
3. In the interval selection, choose **Monthly**.
4. Click **Save Changes**.

---

## 📅 Native Jalali (Solar Hijri) and Gregorian Calendar Support

A distinct capability of Backupino is its calendar-aware localization:

* **For Persian-language sites (`fa_IR`):**  
  Automated scheduling computes recurring execution targeting the **1st day of every Jalali solar month** (1 Farvardin, 1 Ordibehesht, 1 Khordad, etc.) at 00:00 midnight. Dynamic leap years and month lengths (31, 30, and 29 days) are resolved using pure mathematical conversion algorithms without external calendar dependencies.
* **For international and English-language environments:**  
  Automated execution triggers predictably at 00:00 midnight on the first day of every Gregorian calendar month (January 1st, February 1st, March 1st, etc.).

---

## 🗃️ Intelligent Retention Policy (Storage Pruning)

The most common operational hazard with automated backups is server disk exhaustion caused by the accumulation of legacy archive files.

Backupino incorporates an automated storage pruning system:
* **Retention Count Configuration:**  
  In the Settings tab, define the maximum number of backup archives allowed to persist on the server (default: **3 archives**).
* **Pruning Lifecycle:**  
  Upon the successful completion of each new backup, Backupino inspects the total inventory of stored packages. When the count exceeds your configured retention threshold, the oldest archive—along with its metadata records and associated standalone installer files—is safely and permanently pruned from disk.
* This proactive cleanup ensures your server never encounters `Disk Full` errors or hosting account suspensions due to storage overages.

---

## 🧭 Next Step

To learn how to restore your website or migrate it seamlessly to a new domain or host, consult:  
👉 [**Comprehensive Restoration and Migration Guide**](05-restoration-and-migration.md)
