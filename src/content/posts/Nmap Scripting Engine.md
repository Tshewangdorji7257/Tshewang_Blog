---
title: Nmap Scripting Engine
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Nmap
draft: false
---

# Nmap Scripting Engine (NSE)

## NSE Categories
| Category    | Description |
|-------------|-------------|
| auth        | Authentication credential detection |
| broadcast   | Host discovery via broadcasting |
| brute       | Brute-force login attempts |
| default     | Default scripts (`-sC`) |
| discovery   | Service discovery |
| dos         | Denial-of-service checks |
| exploit     | Vulnerability exploitation |
| external    | Uses external services |
| fuzzer      | Vulnerability fuzzing |
| intrusive   | Potentially harmful scripts |
| malware     | Malware infection checks |
| safe        | Non-intrusive scripts |
| version     | Service version detection |
| vuln        | Vulnerability identification |

## Using NSE Scripts
```bash
# Default scripts
nmap -sC <target>

# Specific category
nmap --script <category> <target>

# Defined scripts
nmap --script <script1>,<script2> <target>
```

## Practical Examples
### SMTP Service Scanning
```bash
nmap -p 25 --script banner,smtp-commands 10.129.2.28
```
**Output shows:**
- Server banner (reveals OS info)
- Supported SMTP commands (VRFY, ETRN, etc.)

### Aggressive Scan (-A)
```bash
nmap -p 80 -A 10.129.2.28
```
**Combines:**
- Service detection (-sV)
- OS detection (-O)
- Traceroute
- Default scripts (-sC)

### Vulnerability Assessment
```bash
nmap -p 80 -sV --script vuln 10.129.2.28
```
**Checks for:**
- Known vulnerabilities (CVE listings)
- Web application details (WordPress version)
- Admin interfaces
- Stored XSS vulnerabilities

## Key Findings Example
```
http-wordpress-users:
| Username found: admin
vulners:
| CVE-2019-0211 7.2 https://vulners.com/cve/CVE-2019-0211
| CVE-2018-1312 6.8 https://vulners.com/cve/CVE-2018-1312
```

## Best Practices
1. Start with default scripts (`-sC`)
2. Use specific categories for targeted enumeration
3. For web apps: combine `vuln` with `discovery` scripts
4. Always review script output carefully
5. Consider intrusiveness level before running scripts

