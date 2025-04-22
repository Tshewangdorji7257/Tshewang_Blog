---
title: Digging DNS
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

# DNS Reconnaissance Tools & Techniques

## Essential DNS Tools

| Tool | Key Features | Use Cases |
|------|-------------|-----------|
| **dig** | Supports all record types, detailed output | Manual queries, zone transfers, troubleshooting |
| **nslookup** | Basic A/AAAA/MX record lookup | Quick domain resolution checks |
| **host** | Simplified output for A/AAAA/MX | Rapid DNS verification |
| **dnsenum** | Automated enumeration + brute-forcing | Subdomain discovery, zone transfers |
| **fierce** | Recursive search + wildcard detection | Subdomain enumeration |
| **dnsrecon** | Multi-technique enumeration | Comprehensive DNS mapping |
| **theHarvester** | OSINT + DNS record collection | Email/employee discovery |

## Mastering `dig` (Domain Information Groper)

### Common Command Cheat Sheet

```bash
# Basic record queries
dig example.com A          # IPv4 address
dig example.com AAAA       # IPv6 address 
dig example.com MX         # Mail servers
dig example.com NS         # Name servers
dig example.com TXT        # Text records
dig example.com CNAME      # Canonical names
dig example.com SOA        # Start of Authority

# Advanced usage
dig @1.1.1.1 example.com   # Query specific DNS server
dig +trace example.com     # Full resolution path
dig -x 192.0.2.1          # Reverse DNS lookup
dig +short example.com     # Minimal output
dig +noall +answer example.com # Clean answer format
```

### Anatomy of a `dig` Output (google.com example)

```dns
;; HEADER SECTION
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16449
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION
;google.com. IN A

;; ANSWER SECTION
google.com. 0 IN A 142.251.47.142

;; FOOTER SECTION
;; Query time: 0 msec
;; SERVER: 172.23.176.1#53
;; WHEN: Thu Jun 13 10:45:58 SAST 2024
;; MSG SIZE rcvd: 54
```

**Key Sections Explained**:
1. **Header**: Shows query type (`QUERY`), success status (`NOERROR`), and response flags
   - `qr`: Query Response
   - `rd`: Recursion Desired
   - `ad`: Authentic Data (DNSSEC validated)

2. **Question**: The original query (A record for google.com)

3. **Answer**: Contains the resolved IP (142.251.47.142) with TTL (0=uncached)

4. **Footer**: Metadata including:
   - Query duration
   - Responding server (172.23.176.1 on port 53)
   - Timestamp
   - Response size

## Practical DNS Enumeration Flow

1. **Basic Recon**
   ```bash
   dig target.com ANY +noall +answer  # Try ANY query first
   dig target.com NS +short           # Identify nameservers
   ```

2. **Subdomain Discovery**
   ```bash
   dnsrecon -d target.com -t std     # Standard enumeration
   fierce --domain target.com        # Recursive search
   ```

3. **Mail Server Mapping**
   ```bash
   dig target.com MX +short
   for server in $(dig target.com MX +short | cut -d' ' -f2); do
     dig $server A +short
   done
   ```

4. **Reverse Lookups** (For found IPs)
   ```bash
   dig -x 192.0.2.1 +short
   ```

## Pro Tips & Warnings

**Caution**: 
- Some DNS servers rate-limit or block excessive queries
- Always obtain proper authorization before scanning
- Consider using Tor or VPN for sensitive investigations

**Enhancements**:
- Combine with WHOIS: `whois $(dig target.com NS +short \| head -1)`
- Use Cloudflare's 1.1.1.1 for reliable resolution: `dig @1.1.1.1 target.com`
- Store results for comparison: `dig target.com > baseline_dns.txt`

## Online DNS Tools
- [DNSDumpster](https://dnsdumpster.com/)
- [ViewDNS.info](https://viewdns.info/)
- [SecurityTrails](https://securitytrails.com/)

---

**Next**: [Subdomain Enumeration Techniques]()  
**Previous**: [WHOIS Deep Dive]()
```

This markdown features:
1. **Tool comparison table** for quick reference
2. **Ready-to-use command snippets** with annotations
3. **Visual breakdown** of `dig` output components
4. **Practical workflow** from basic to advanced techniques
5. **Warning boxes** for operational security
6. **Integration tips** with other recon methods

