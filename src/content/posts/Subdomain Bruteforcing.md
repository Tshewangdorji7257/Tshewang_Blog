---
title: Subdomain Bruteforcing
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

# Subdomain Bruteforcing

## What is Subdomain Brute-Force Enumeration?
An active discovery technique that tests predefined lists of potential subdomain names against a target domain to identify valid subdomains.

## The Process

### 1. Wordlist Selection
Choose a list containing potential subdomain names:
- **General-Purpose**: Common names like dev, staging, blog, mail, admin, test
- **Targeted**: Industry or technology-specific names
- **Custom**: Self-created lists based on gathered intelligence

### 2. Iteration and Querying
- A tool appends each word from the wordlist to the main domain
- Example: "dev" + "example.com" = "dev.example.com"

### 3. DNS Lookup
- Performs DNS queries for each potential subdomain
- Typically uses A or AAAA record lookups

### 4. Filtering and Validation
- Valid subdomains that resolve to IP addresses are recorded
- Further validation may include attempting to access the subdomain

## Popular Tools

| Tool | Description |
|------|-------------|
| dnsenum | Comprehensive DNS enumeration with dictionary and brute-force capabilities |
| fierce | User-friendly tool with wildcard detection and recursive discovery |
| dnsrecon | Versatile tool combining multiple techniques with customizable output |
| amass | Actively maintained tool with extensive data source integration |
| assetfinder | Simple, lightweight tool for quick subdomain discovery |
| puredns | Powerful DNS brute-forcing with effective resolving and filtering |

## Tool Spotlight: DNSEnum

### Key Features
- DNS Record Enumeration (A, AAAA, NS, MX, TXT)
- Zone Transfer Attempts
- Subdomain Brute-Forcing
- Google Scraping for additional subdomains
- Reverse DNS Lookups
- WHOIS Lookups

### Example Usage
```bash
dnsenum --enum inlanefreight.com -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

#### Command Breakdown:
- `--enum inlanefreight.com`: Specifies the target domain
- `-f /path/to/wordlist`: Indicates the wordlist path for brute-forcing
- `-r`: (Optional) Enables recursive subdomain brute-forcing

### Sample Output
```
dnsenum VERSION:1.2.6
----- inlanefreight.com -----

Host's addresses:
__________________
inlanefreight.com. 300 IN A 134.209.24.248
[...]
Brute forcing with /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt:
_______________________________________________________________________________________
www.inlanefreight.com. 300 IN A 134.209.24.248
support.inlanefreight.com. 300 IN A 134.209.24.248
[...]

done.
