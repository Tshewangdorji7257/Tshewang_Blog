---
title: robots.txt
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

# Robots.txt

## What is robots.txt?
A simple text file placed in the root directory of a website (e.g., `www.example.com/robots.txt`) that follows the Robots Exclusion Standard. It contains instructions (directives) that tell web crawlers which parts of a website they can and cannot access.

## How robots.txt Works
- The file targets specific user-agents (identifiers for different types of bots)
- Contains directives that allow or disallow access to specific paths
- Lives in the website's root directory
- Is publicly accessible to anyone who knows to look for it

Example:
```txt
User-agent: *
Disallow: /private/
```
This tells all user-agents (the * is a wildcard) not to access URLs starting with `/private/`.

## Structure of robots.txt

A robots.txt file consists of "records" separated by blank lines. Each record has:

1. **User-agent specification**: Identifies which crawler the rules apply to
   - `*` targets all bots
   - Specific agents can be targeted (e.g., "Googlebot", "Bingbot")

2. **Directives**: Instructions for the specified user-agent

### Common Directives

| Directive | Description | Example |
|-----------|-------------|---------|
| Disallow | Paths that should not be crawled | `Disallow: /admin/` |
| Allow | Explicitly permitted paths (even if under a Disallow) | `Allow: /public/` |
| Crawl-delay | Delay (seconds) between bot requests | `Crawl-delay: 10` |
| Sitemap | URL to an XML sitemap | `Sitemap: https://www.example.com/sitemap.xml` |

## Why Most Bots Respect robots.txt
- Prevents server overload from excessive crawler traffic
- Protects sensitive information from being indexed
- Legal and ethical compliance with website terms of service
- Standard practice among legitimate search engines and crawlers

## robots.txt in Web Reconnaissance

For security professionals, robots.txt can provide valuable intelligence:

- **Uncovers Hidden Directories**: Disallowed paths often reveal sensitive areas like admin panels, backup files, or private content
- **Maps Website Structure**: Helps create a map of the website including sections not linked from the main navigation
- **Detects Crawler Traps**: May reveal "honeypot" directories intended to catch malicious bots

## Example Analysis

```txt
User-agent: *
Disallow: /admin/
Disallow: /private/
Allow: /public/

User-agent: Googlebot
Crawl-delay: 10

Sitemap: https://www.example.com/sitemap.xml
```

From this example, we can infer:
- The website likely has an admin panel at `/admin/`
- There's sensitive content in the `/private/` directory
- Public content is explicitly allowed at `/public/`
- The site owner wants Google to crawl slowly (10 second delay)
- A sitemap is available for more efficient crawling