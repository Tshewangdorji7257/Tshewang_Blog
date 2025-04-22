---
title: Using WHOIS
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

# Utilising WHOIS in Security Operations

## Practical Scenarios

### Scenario 1: Phishing Investigation
**Situation**:  
Email security gateway flags suspicious emails impersonating a bank.

**WHOIS Findings**:
- **Registration Date**: Domain registered days ago
- **Registrant**: Privacy-protected (red flag)
- **Name Servers**: Bulletproof hosting provider

**Action Taken**:
1. Immediate domain blocking
2. Employee awareness alert
3. Infrastructure mapping for related malicious domains

### Scenario 2: Malware Analysis
**Situation**:  
Analysis of new malware strain with C2 communication.

**WHOIS Findings**:
- **Registrant**: Anonymous free email account
- **Location**: High-cybercrime jurisdiction
- **Registrar**: Known for lax abuse policies

**Conclusion**:  
Likely compromised/bulletproof server → Report to hosting provider

### Scenario 3: Threat Intelligence
**Patterns Discovered**:
- **Registration Timing**: Domain clusters before attacks
- **Registrants**: Fake identities/aliases
- **Infrastructure**: Shared name servers
- **History**: Previous takedowns

**Outcome**:  
Created TTP profile with WHOIS-based IOCs for threat sharing

---

## WHOIS Command-Line Usage

### Installation
```bash
sudo apt update
sudo apt install whois -y
```

### Basic Lookup Example
```bash
whois facebook.com
```

### Sample Output Analysis (facebook.com)
| Field | Value | Significance |
|-------|-------|--------------|
| **Registrar** | RegistrarSafe, LLC | Trusted registrar |
| **Creation Date** | 1997-03-29 | Established legitimacy |
| **Expiry Date** | 2033-03-30 | Long-term commitment |
| **Organization** | Meta Platforms, Inc. | Parent company verification |
| **Domain Status** | Multiple prohibitions | Strong security controls |
| **Name Servers** | A.NS.FACEBOOK.COM, etc. | Self-managed DNS infrastructure |

---

## Key WHOIS Indicators for Threat Hunting

### Red Flags
**New Domains** (<30 days old)  
**Privacy Protection Services**  
**Free Email Registrants** (e.g., @gmail.com)  
**High-Risk Jurisdictions**  
**Bulletproof Hosting Providers**  

### Defensive Patterns
**Long Registration Periods** (5+ years)  
**Corporate Email Contacts** (e.g., @company.com)  
**Registrar-Lock Status**  
**Enterprise DNS Providers** (AWS, Cloudflare, etc.)  

---

## Advanced WHOIS Techniques

### Bulk WHOIS Lookups
```bash
for domain in $(cat domains.txt); do whois $domain >> results.txt; done
```

### Historical WHOIS Analysis
Tools:  
- [WhoisFreaks](https://whoisfreaks.com/)  
- [WhoisHistory](https://whoishistory.org/)  

### RDAP Protocol (WHOIS Replacement)
```bash
curl -s https://rdap.verisign.com/com/v1/domain/example.com | jq
```

---

## Limitations & Complementary Tools

**WHOIS Shortcomings**:
- GDPR-masked data in EU regions
- Incomplete historical records
- Potential false registrant info

**Combine With**:
- `dig` for DNS verification
- `nslookup` for IP/host correlation
- [SecurityTrails](https://securitytrails.com/) for comprehensive historical data

> **Pro Tip**: Always correlate WHOIS data with passive DNS records and SSL certificate info for full infrastructure mapping.

---

**Next**: [DNS Enumeration Techniques](#) | **Previous**: [WHOIS Fundamentals](#)  
```

This markdown features:
1. **Real-world scenarios** with actionable insights
2. **Command-line examples** ready for copy-paste
3. **Analysis tables** for quick reference
4. **Threat indicators** checklist
5. **Advanced techniques** for deeper investigation
6. **Tool recommendations** for extended analysis

