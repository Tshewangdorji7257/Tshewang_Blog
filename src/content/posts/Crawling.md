---
title: Crawling
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

## **Web Crawling (Spidering) — Summary**

### What is Crawling?
- Automated **systematic browsing** of the web.
- Bots (crawlers/spiders) **follow links**, collect and index web content.
- Used by **search engines**, **data scrapers**, and **security researchers**.

---

## How Web Crawlers Work

1. **Start with a seed URL** (homepage).
2. **Fetch page content**, extract links.
3. Add new links to the **queue**.
4. **Iterate** the process across all discovered links.

Difference from **fuzzing**:  
Crawling follows *actual* links; fuzzing guesses possible paths.

---

## Crawling Strategies

### 1️**Breadth-First Crawling**
- Explores all links on the **current page first** before going deeper.
- Ideal for a **broad view** of a website’s structure.

### 2️**Depth-First Crawling**
- Follows **one link chain as deep as possible**, then backtracks.
- Good for **digging into deeply nested content**.

---

## Data Extracted by Crawlers

| Type              | Description |
|-------------------|-------------|
| **Links**         | Internal/external links to map site structure. |
| **Comments**     | May reveal sensitive info or vulnerabilities. |
| **Metadata**     | Titles, descriptions, authors, software versions, etc. |
| **Sensitive Files** | Backups (`.bak`, `.old`), config files (`.env`, `.php`), logs, etc. |

---

## The Power of Context in Recon

A single data point might seem harmless, but **combining multiple findings** can reveal vulnerabilities. For example:

**Example 1**  
- Crawled metadata shows old software version.  
- Comment mentions same version having issues.  
- A vulnerable endpoint is likely.

**Example 2**  
- Multiple links point to `/files/`.  
- Crawling reveals **directory listing enabled**.  
- Manually checking shows exposed **backups & documents**.

Always **connect the dots** for full context.

---

## Use in Web Recon

- **Mapping website structure**
- **Finding hidden endpoints or admin panels**
- **Identifying potentially vulnerable configurations**
- **Spotting exposed secrets (API keys, credentials, etc.)**

---

## Cheat Sheet

### Common Crawling Tools

| Tool        | Usage                            | Notes |
|-------------|----------------------------------|-------|
| `wget`      | `wget -r -l 2 <url>`             | Simple recursive crawl |
| `curl` + `grep` | For manual link extraction    | Good for quick checks |
| `gobuster`  | `gobuster dir -u <url> -w wordlist` | Fuzzing + directory discovery |
| `Burp Suite`| Passive/Active crawling during scan | Full-featured recon |
| `SpiderFoot`| Automated OSINT + crawling       | Excellent recon automation |

### Example: Get All Links
```bash
curl -s https://target.com | grep -oP 'href="\K[^"]+'
```

