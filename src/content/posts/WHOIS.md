---
title: WHOIS
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

# WHOIS Protocol

## Overview
WHOIS is a widely used query and response protocol designed to access databases that store information about registered internet resources. Primarily associated with domain names, WHOIS can also provide details about IP address blocks and autonomous systems. Think of it as a giant phonebook for the internet, letting you look up who owns or is responsible for various online assets.

```bash
k4y0x13@htb[/htb]$ whois inlanefreight.com
[...]
Domain Name: inlanefreight.com
Registry Domain ID: 2420436757_DOMAIN_
Registrar WHOIS Server: whois.registrar.amazon.com
Registrar URL: https://registrar.amazon.com
Updated Date: 2023-07-03T01:11:15Z
Creation Date: 2019-08-05T22:43:09Z
[...]
```

## Typical WHOIS Record Contents
| Field                  | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| **Domain Name**        | The registered domain (e.g., `example.com`)                                 |
| **Registrar**          | Company where domain was registered (e.g., GoDaddy, Namecheap)              |
| **Registrant Contact** | Person/organization that registered the domain                              |
| **Administrative Contact** | Manager of the domain                                                   |
| **Technical Contact**   | Person handling technical issues                                           |
| **Creation/Expiration Dates** | When domain was registered and expiry date                            |
| **Name Servers**       | DNS servers translating domain to IP                                        |

## Historical Context
The WHOIS protocol traces back to **Elizabeth Feinler** and her team at Stanford Research Institute's Network Information Center (NIC) in the 1970s. It was created to track ARPANET (early internet) resources.

> **Fun Fact**: The original WHOIS was a simple text file before evolving into a distributed database system.

## Why WHOIS Matters in Web Recon
WHOIS provides critical reconnaissance data for penetration testers:

1. **Identifying Key Personnel**  
   - Reveals names, emails, phone numbers  
   - Useful for social engineering/phishing campaigns  

2. **Discovering Network Infrastructure**  
   - Name servers and IP addresses expose network architecture  
   - Helps identify misconfigurations/entry points  

3. **Historical Analysis**  
   - Services like [WhoisFreaks](https://whoisfreaks.com/) track changes over time  
   - Reveals ownership shifts or technical changes  

---

### WHOIS Cheat Sheet

| Command/Tool          | Description                                  | Example Usage                          |
|-----------------------|----------------------------------------------|----------------------------------------|
| `whois` (CLI)        | Query WHOIS databases directly              | `whois example.com`                   |
| `dig` + `whois`      | Combine DNS and WHOIS lookup                | `dig ns example.com && whois example.com` |
| **Online Tools**     |                                              |                                        |
| [ICANN Lookup](https://lookup.icann.org/) | Official ICANN WHOIS tool            |                                        |
| [WhoisFreaks](https://whoisfreaks.com/) | Historical WHOIS data              |                                        |
| **Advanced**         |                                              |                                        |
| `jwhois`            | Configurable WHOIS client                   | `jwhois -c /etc/jwhois.conf example.com` |
| Bulk WHOIS          | For mass domain lookups                     | Tools like DomainIQ or WhoisXMLAPI     |

---

**Next Steps**: Use WHOIS data to map organizational assets before proceeding to [DNS Enumeration](#).  
**Previous**: [Web Recon Basics](#) | **Next**: [DNS Enumeration](#)  
``` 

### Key Features:
1. **Structured Format**: Clear sections with headers and tables for easy reference
2. **Command Examples**: Ready-to-use CLI snippets
3. **Tool Recommendations**: Includes both CLI and web-based tools
4. **Historical Context**: Background on Elizabeth Feinler's contribution
5. **Cheat Sheet Table**: Quick-reference table for common tasks

