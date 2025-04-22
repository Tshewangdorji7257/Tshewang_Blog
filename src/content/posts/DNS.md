---
title: DNS
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

### **DNS**
- **DNS (Domain Name System)**: Translates human-readable domain names (e.g., `example.com`) into IP addresses (e.g., `93.184.216.34`).
- **Not centralized**: Info is distributed globally across many name servers.

---

### **Types of DNS Servers**
| **Type**                 | **Role** |
|--------------------------|----------|
| **Root Server**          | Top of the DNS hierarchy, knows where to find TLD (.com, .org) info |
| **Authoritative Server** | Final source of truth for a zone, answers DNS queries for that domain |
| **Non-authoritative**    | Gets answers from other servers (not authoritative for the data) |
| **Caching Server**       | Stores results of past queries to speed up response |
| **Forwarding Server**    | Forwards queries to another DNS server |
| **Resolver**             | Usually client-side (OS/router); initiates DNS queries |

---

### **DNS Security**
- DNS traffic is usually **unencrypted** (privacy risk).
- Encryption standards:
  - **DoT (DNS over TLS)**
  - **DoH (DNS over HTTPS)**
  - **DNSCrypt**

---

### 📄 **DNS Records**
| **Record** | **Function** |
|------------|---------------|
| `A`        | IPv4 address |
| `AAAA`     | IPv6 address |
| `MX`       | Mail server |
| `NS`       | Name servers |
| `TXT`      | Misc text (e.g., SPF, DMARC, domain verification) |
| `CNAME`    | Alias of another domain |
| `PTR`      | Reverse lookup (IP → domain) |
| `SOA`      | Start of Authority (zone management info) |

---

### **BIND DNS Configuration**
- Key config files:
  - `/etc/bind/named.conf`
  - `/etc/bind/named.conf.local`
  - `/etc/bind/named.conf.options`
- **Zone files** (e.g. `/etc/bind/db.domain.com`): Define DNS records for a domain.
- **Reverse lookup zone files** (e.g. `/etc/bind/db.10.129.14`): Map IPs to hostnames.

---

### **Common Dangerous Settings**
| **Option**       | **Risk if misconfigured** |
|------------------|---------------------------|
| `allow-query`    | Anyone can query sensitive DNS data |
| `allow-recursion`| Opens recursive queries to public—can be abused |
| `allow-transfer` | Can allow zone transfers (AXFR) to attackers |
| `zone-statistics`| May reveal internal structure or usage stats |

---

### **DNS Enumeration Techniques**
- `dig` tool examples:
  - `dig ns domain.com`: Get nameservers
  - `dig soa domain.com`: Get SOA record
  - `dig any domain.com`: Get all available records
  - `dig CH TXT version.bind`: Get DNS version info (if exposed)

