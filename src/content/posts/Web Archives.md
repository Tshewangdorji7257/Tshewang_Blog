---
title: Web Archives
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---


##  **Web Archives & The Wayback Machine**

###  What is the Wayback Machine?

- Created by the **Internet Archive** (non-profit)
- Started in **1996**
- Lets you **view old versions of websites** (HTML, CSS, JS, images, etc.)
- Each snapshot is called a **capture** or **archive**

---

###  **How It Works (3 Steps)**

| Step         | Description                                                                 |
|--------------|-----------------------------------------------------------------------------|
| **1. Crawling**   | Bots visit and download webpages + resources (like search engine crawlers)  |
| **2. Archiving**  | Stores captured content and timestamps it (daily/weekly/monthly based on site activity) |
| **3. Accessing**  | Users enter a URL and pick a date to view the old version of the site         |

---

###  **Why It's Useful for Web Recon**

| Use Case                             | Description                                                                                   |
|--------------------------------------|-----------------------------------------------------------------------------------------------|
|  Hidden Assets                   | Find old paths, subdomains, files, or admin panels that no longer appear on the live site     |
|  Vulnerabilities                   | Spot older, less secure implementations or exposed sensitive data                            |
|  Track Changes                     | Observe how site content, structure, or tech stack has evolved                                |
|  Gather Intel                      | Find legacy pages revealing names, emails, internal projects, etc.                           |
|  Stealthy Recon                    | Passive info gathering — no interaction with target servers                                  |

---

###  **Example Recon Usage**

**Scenario**: You're gathering recon on a company site.

```bash
1. Go to: https://web.archive.org
2. Enter: https://targetsite.com
3. Click on earliest capture (e.g., 2015-04-12)
4. Look for: 
   - `/admin/`
   - `/config/`
   - Exposed file names: `.bak`, `.zip`, `.old`
   - Emails, phone numbers, and internal project references
```

You can also pair this with **Google Dorking**:
```bash
site:web.archive.org targetsite.com
```

---

### Real-World Example (HTB)

- **Hack The Box (HTB)** earliest capture:
  ```
  https://web.archive.org/web/20170610042301/https://hackthebox.eu/
  ```

- Find changes to login forms, sign-up methods, retired lab names, early team members, etc.

---

### Limitations

- Not **all** websites/pages are archived
- Some sites **block** crawlers (`robots.txt`)
- Owners can **request exclusion**
- Dynamic content (e.g., JavaScript-heavy apps) may not always render properly

