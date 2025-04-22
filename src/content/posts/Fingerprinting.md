---
title: Fingerprinting
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

# Web Fingerprinting

## What is Fingerprinting?
Fingerprinting extracts technical details about technologies powering a website, revealing digital signatures of web servers, operating systems, and software components. This information helps identify potential security weaknesses.

## Why Fingerprinting Matters
- **Targeted Attacks**: Focuses efforts on known vulnerabilities for specific technologies
- **Identifying Misconfigurations**: Exposes outdated software and default settings
- **Prioritizing Targets**: Helps identify systems more likely to be vulnerable
- **Building Comprehensive Profiles**: Creates holistic view of target infrastructure

## Fingerprinting Techniques

### 1. Banner Grabbing
Analyzing banners presented by web servers that often reveal software and version numbers.

### 2. HTTP Header Analysis
Examining headers like `Server` and `X-Powered-By` that disclose web server software and technologies.

### 3. Probing for Specific Responses
Sending crafted requests that elicit unique responses revealing specific technologies.

### 4. Page Content Analysis
Examining page structure, scripts, and copyright headers for technology clues.

## Fingerprinting Tools

| Tool | Description | Features |
|------|-------------|----------|
| Wappalyzer | Browser extension and online service | Identifies CMSs, frameworks, analytics tools |
| BuiltWith | Web technology profiler | Detailed reports with free and paid plans |
| WhatWeb | Command-line tool | Vast database of technology signatures |
| Nmap | Versatile network scanner | Service and OS fingerprinting, NSE scripts |
| Netcraft | Web security services | Reports on technology, hosting, security |
| wafw00f | Command-line tool | Identifies Web Application Firewalls (WAFs) |

## Practical Fingerprinting Example

### Banner Grabbing with curl
```bash
# Get HTTP headers
curl -I inlanefreight.com

# Sample output
HTTP/1.1 301 Moved Permanently
Date: Fri, 31 May 2024 12:07:44 GMT
Server: Apache/2.4.41 (Ubuntu)
Location: https://inlanefreight.com/
Content-Type: text/html; charset=iso-8859-1
```

### Following Redirects
```bash
# Follow HTTPS redirect
curl -I https://inlanefreight.com

# Sample output
HTTP/1.1 301 Moved Permanently
Date: Fri, 31 May 2024 12:12:12 GMT
Server: Apache/2.4.41 (Ubuntu)
X-Redirect-By: WordPress
Location: https://www.inlanefreight.com/
Content-Type: text/html; charset=UTF-8
```

```bash
# Final destination
curl -I https://www.inlanefreight.com

# Sample output
HTTP/1.1 200 OK
Date: Fri, 31 May 2024 12:12:26 GMT
Server: Apache/2.4.41 (Ubuntu)
Link: <https://www.inlanefreight.com/index.php/wp-json/>; rel="https://api.w.org/"
Link: <https://www.inlanefreight.com/index.php/wp-json/wp/v2/pages/7>; rel="alternate"; typ
Link: <https://www.inlanefreight.com/>; rel=shortlink
Content-Type: text/html; charset=UTF-8
```

### WAF Detection with wafw00f
```bash
# Install wafw00f
pip3 install git+https://github.com/EnableSecurity/wafw00f

# Check for WAF
wafw00f inlanefreight.com

# Sample output
[*] Checking https://inlanefreight.com
[+] The site https://inlanefreight.com is behind Wordfence (Defiant) WAF.
[~] Number of requests: 2
```

### Comprehensive Scanning with Nikto
```bash
# Install Nikto (if needed)
sudo apt update && sudo apt install -y perl
git clone https://github.com/sullo/nikto
cd nikto/program
chmod +x ./nikto.pl

# Run fingerprinting modules
nikto -h inlanefreight.com -Tuning b

# Sample output
+ Server: Apache/2.4.41 (Ubuntu)
+ /index.php?: Uncommon header 'x-redirect-by' found, with contents: WordPress.
+ Apache/2.4.41 appears to be outdated (current is at least 2.4.59)
+ /license.txt: License file found may identify site software.
+ /: A Wordpress installation was found.
+ /wp-login.php: Wordpress login found.
```

## Key Findings from Example
- **Server**: Apache/2.4.41 on Ubuntu (outdated version)
- **CMS**: WordPress installation
- **Security**: Wordfence WAF deployed
- **Infrastructure**: Multiple IPs (IPv4 and IPv6)
- **Access Points**: WordPress login page identified
- **Information Disclosure**: License file potentially revealing software details
- **Security Headers**: Missing or insecure headers identified
