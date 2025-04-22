---
title: Introduction
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

# Web Reconnaissance

## Introduction

Web Reconnaissance is the foundation of a thorough security assessment. This process involves systematically and meticulously collecting information about a target website or web application. Think of it as the preparatory phase before delving into deeper analysis and potential exploitation. It forms a critical part of the "Information Gathering" phase of the Penetration Testing Process.

### Primary Goals of Web Reconnaissance

1. **Identifying Assets**: Uncovering all publicly accessible components of the target, such as web pages, subdomains, IP addresses, and technologies used. This step provides a comprehensive overview of the target's online presence.
2. **Discovering Hidden Information**: Locating sensitive information that might be inadvertently exposed, including backup files, configuration files, or internal documentation. These findings can reveal valuable insights and potential entry points for attacks.
3. **Analysing the Attack Surface**: Examining the target's attack surface to identify potential vulnerabilities and weaknesses. This involves assessing the technologies used, configurations, and possible entry points for exploitation.
4. **Gathering Intelligence**: Collecting information that can be leveraged for further exploitation or social engineering attacks. This includes identifying key personnel, email addresses, or patterns of behaviour that could be exploited.

Attackers leverage this information to tailor their attacks, allowing them to target specific weaknesses and bypass security measures. Conversely, defenders use recon to proactively identify and patch vulnerabilities before malicious actors can leverage them.

## Types of Reconnaissance

Web reconnaissance encompasses two fundamental methodologies: **active** and **passive reconnaissance**. Each approach offers distinct advantages and challenges, and understanding their differences is crucial for adequate information gathering.

### Active Reconnaissance

In active reconnaissance, the attacker directly interacts with the target system to gather information. This interaction can take various forms:

| Technique               | Description                                                                 | Example Tools                     | Risk of Detection                                                                 |
|-------------------------|-----------------------------------------------------------------------------|-----------------------------------|-----------------------------------------------------------------------------------|
| Port Scanning           | Identifying open ports and services running on the target.                  | Nmap, Masscan, Unicornscan        | High: Direct interaction with the target can trigger intrusion detection systems (IDS) and firewalls. |
| Vulnerability Scanning  | Probing the target for known vulnerabilities (e.g., outdated software).     | Nessus, OpenVAS, Nikto            | High: Vulnerability scanners send exploit payloads that security solutions can detect. |
| Network Mapping         | Mapping the target's network topology, including connected devices.         | Traceroute, Nmap                  | Medium to High: Excessive or unusual network traffic can raise suspicion. |
| Banner Grabbing         | Retrieving information from banners displayed by services.                  | Netcat, curl                      | Low: Banner grabbing typically involves minimal interaction but can still be logged. |
| OS Fingerprinting       | Identifying the operating system running on the target.                     | Nmap, Xprobe2                     | Low: OS fingerprinting is usually passive, but some advanced techniques can be detected. |
| Service Enumeration     | Determining the specific versions of services running on open ports.        | Nmap                              | Low: Similar to banner grabbing, service enumeration can be logged but is less likely to trigger alerts. |
| Web Spidering           | Crawling the target website to identify web pages, directories, and files.  | Burp Suite Spider, OWASP ZAP Spider, Scrapy | Low to Medium: Can be detected if the crawler's behaviour is not carefully configured. |

**Pros**: Direct and comprehensive view of the target's infrastructure.  
**Cons**: Higher risk of detection due to direct interaction.

---

### Passive Reconnaissance

In passive reconnaissance, information is gathered without directly interacting with the target. This relies on publicly available data:

| Technique               | Description                                                                 | Example Tools                     | Risk of Detection                                                                 |
|-------------------------|-----------------------------------------------------------------------------|-----------------------------------|-----------------------------------------------------------------------------------|
| Search Engine Queries   | Using search engines to uncover target information.                         | Google, DuckDuckGo, Shodan        | Very Low: Normal internet activity, unlikely to trigger alerts. |
| WHOIS Lookups           | Querying WHOIS databases for domain registration details.                   | `whois`, online WHOIS services    | Very Low: Legitimate queries, no suspicion. |
| DNS Analysis            | Analysing DNS records to identify subdomains and infrastructure.            | `dig`, `nslookup`, dnsrecon       | Very Low: Essential for internet browsing, not flagged. |
| Web Archive Analysis    | Examining historical snapshots of the target's website.                     | Wayback Machine                   | Very Low: Normal activity. |
| Social Media Analysis   | Gathering information from platforms like LinkedIn, Twitter.                | LinkedIn, Twitter, OSINT tools    | Very Low: Public profile access is not intrusive. |
| Code Repositories       | Analysing public code repositories (e.g., GitHub) for exposed data.         | GitHub, GitLab                    | Very Low: Publicly accessible repositories. |

**Pros**: Stealthy, low risk of detection.  
**Cons**: Less comprehensive, relies on publicly available data.

---

## Next Steps

In this module, we will delve into the essential tools and techniques used in web reconnaissance, starting with **WHOIS**. Understanding the WHOIS protocol provides a gateway to accessing vital information about domain registrations, ownership details, and the digital infrastructure of targets. This foundational knowledge sets the stage for more advanced recon methods we'll explore later.

> **Next**: Mark Complete & Continue
```

### Cheat Sheet
```markdown
### Active Recon Tools
- **Port Scanning**: `nmap -sV <target>`
- **Vulnerability Scanning**: `nikto -h <target>`
- **Banner Grabbing**: `nc <target> 80`  
  or `curl -I http://<target>`

### Passive Recon Tools
- **WHOIS Lookup**: `whois <domain>`
- **DNS Enumeration**: `dig <domain>`  
  or `dnsrecon -d <domain>`
- **Search Engines**: `site:<domain>` in 