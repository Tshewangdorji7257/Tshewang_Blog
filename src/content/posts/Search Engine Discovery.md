---
title: Search Engine Discovery
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

##  **Search Engine Discovery (OSINT via Search Engines)**

###  Why Use It?

-  **Open Source**: Legal and ethical
-  **Broad Coverage**: Public data across the web
-  **Easy to Use**: Just need a search engine
-  **Free**: No cost, no access restrictions

###  Use Cases

-  Security Assessments (find exposed files, endpoints)
-  Threat Intelligence
-  Competitive Research
-  Investigative Journalism

---

##  **Essential Search Operators**

| Operator        | Description                                            | Example                                      |
|-----------------|--------------------------------------------------------|----------------------------------------------|
| `site:`         | Limits results to a specific site                      | `site:example.com`                            |
| `inurl:`        | Finds pages with a keyword in the URL                  | `inurl:login`                                 |
| `filetype:`     | Searches for files with a specific extension           | `filetype:pdf`                                |
| `intitle:`      | Finds keywords in the title                            | `intitle:"confidential report"`               |
| `intext:`       | Finds keywords in the body text                        | `intext:"password reset"`                     |
| `cache:`        | Shows cached page version                              | `cache:example.com`                           |
| `link:`         | Finds pages linking to a URL                           | `link:example.com`                            |
| `related:`      | Finds sites similar to a URL                           | `related:example.com`                         |
| `info:`         | Displays summary info about a URL                      | `info:example.com`                            |
| `define:`       | Definition of a term                                   | `define:phishing`                             |
| `numrange:`     | Searches for numbers within a range                    | `1000..2000`                                  |
| `allintext:`    | All specified words must appear in body text           | `allintext:admin password reset`              |
| `allinurl:`     | All specified words must be in the URL                 | `allinurl:admin panel`                        |
| `allintitle:`   | All specified words must be in the title               | `allintitle:confidential report 2023`         |
| `AND`           | Require both terms                                     | `site:example.com AND inurl:admin`            |
| `OR`            | Either term can be present                             | `"linux" OR "ubuntu"`                         |
| `NOT` / `-`     | Exclude term                                           | `site:example.com -inurl:login`               |
| `"` (quotes)    | Exact phrase match                                     | `"information security policy"`               |
| `*`             | Wildcard (any word or character)                       | `"user * manual"`                             |

---

##  **Google Dorking Cheat Sheet**

Google Dorking = Advanced recon using search operators to find sensitive/exposed content.

###  Login Pages
```bash
site:example.com inurl:login
site:example.com (inurl:login OR inurl:admin)
```

###  Exposed Files
```bash
site:example.com filetype:pdf
site:example.com (filetype:xls OR filetype:docx)
```

###  Configuration Files
```bash
site:example.com inurl:config.php
site:example.com (ext:conf OR ext:cnf)
```

###  Database Backups
```bash
site:example.com inurl:backup
site:example.com filetype:sql
```

---

##  Pro Tips

- Use **DuckDuckGo**, **Bing**, or **Yandex** for additional results—each indexes the web differently.
- Combine operators for more specific targeting:
  ```bash
  site:gov.bt filetype:pdf intitle:"budget report"
  ```

- Explore the [Google Hacking Database (GHDB)](https://www.exploit-db.com/google-hacking-database/) for real-world dorks.



