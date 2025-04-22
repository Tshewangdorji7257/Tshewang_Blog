---
title: DNS
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

# DNS: The Internet's GPS

The **Domain Name System (DNS)** acts as the internet's GPS, guiding your online journey from memorable landmarks (domain names) to precise numerical coordinates (IP addresses). Like a GPS translates a destination name into latitude and longitude, DNS translates human-readable domain names (like `www.example.com`) into numerical IP addresses (like `192.0.2.1`).

Without DNS, navigating the online world would be like driving without a map or GPS – a frustrating and error-prone endeavour.

---

## How DNS Works

### 1. Your Computer Asks for Directions (DNS Query)
- Checks its cache for the IP address.
- If not found, it contacts a **DNS Resolver** (usually provided by your ISP).

### 2. DNS Resolver Checks Its Map (Recursive Lookup)
- Resolver checks its own cache.
- If still not found, it performs a recursive lookup starting from the **Root Name Server**.

### 3. Root Name Server Points the Way
- Doesn’t know the IP, but directs the resolver to a **TLD Name Server** (e.g., for `.com`).

### 4. TLD Name Server Narrows It Down
- Directs the resolver to the **Authoritative Name Server** for the domain.

### 5. Authoritative Name Server Delivers the Address
- Holds and returns the correct IP address to the resolver.

### 6. DNS Resolver Returns the Information
- Sends the IP back to your computer and caches it.

### 7. Your Computer Connects
- With the IP address in hand, it connects to the website.

---

## The Hosts File

A manual method of resolving domain names to IP addresses.

- **Windows**: `C:\Windows\System32\drivers\etc\hosts`
- **Linux/macOS**: `/etc/hosts`

### Format
```txt
<IP Address> <Hostname> [<Alias> ...]
```

### Examples
```txt
127.0.0.1 localhost
192.168.1.10 devserver.local
127.0.0.1 myapp.local      # Development
192.168.1.20 testserver.local # Connectivity Test
0.0.0.0 unwanted-site.com   # Block Site
```

---

## DNS is Like a Relay Race

Your computer passes the domain request to the resolver → root server → TLD server → authoritative server → IP returned.

---

## Key DNS Concepts

| Concept                    | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| Domain Name               | Human-readable label (e.g., `www.example.com`)                              |
| IP Address                | Numerical address (e.g., `192.0.2.1`)                                       |
| DNS Resolver              | Translates domain names (e.g., Google DNS `8.8.8.8`)                        |
| Root Name Server          | Top-level DNS server (e.g., `a.root-servers.net`)                           |
| TLD Name Server           | Handles top-level domains like `.com`, `.org`                               |
| Authoritative Name Server | Final source for IP address for a domain                                    |
| DNS Record Types          | Stores domain-related info: A, AAAA, MX, CNAME, TXT, etc.                   |

---

## Zone Files & DNS Records

A **zone** represents a portion of the domain namespace managed by an entity.

### Example Zone File
```zone
$TTL 3600 ; Default TTL
@ IN SOA ns1.example.com. admin.example.com. (
    2024060401 ; Serial
    3600       ; Refresh
    900        ; Retry
    604800     ; Expire
    86400      ; Minimum TTL
)
@ IN NS ns1.example.com.
@ IN NS ns2.example.com.
@ IN MX 10 mail.example.com.
www IN A 192.0.2.1
mail IN A 198.51.100.1
ftp IN CNAME www.example.com.
```

---

## Common DNS Record Types

| Type  | Full Name             | Description                                                             | Example |
|-------|------------------------|-------------------------------------------------------------------------|---------|
| A     | Address Record         | Maps hostname to IPv4 address                                           | `www.example.com. IN A 192.0.2.1` |
| AAAA  | IPv6 Address Record    | Maps hostname to IPv6 address                                           | `www.example.com. IN AAAA 2001:db8::7334` |
| CNAME | Canonical Name Record | Alias to another hostname                                               | `blog.example.com. IN CNAME webserver.example.net.` |
| MX    | Mail Exchange Record   | Specifies mail server                                                   | `example.com. IN MX 10 mail.example.com.` |
| NS    | Name Server Record     | Delegates zone to authoritative server                                  | `example.com. IN NS ns1.example.com.` |
| TXT   | Text Record            | Arbitrary text (used for SPF, domain verification)                      | `example.com. IN TXT "v=spf1 mx -all"` |
| SOA   | Start of Authority     | Administrative details about the DNS zone                               | `example.com. IN SOA ns1.example.com. admin.example.com. ...` |
| SRV   | Service Record         | Defines services, ports, and hosts                                      | `_sip._udp.example.com. IN SRV 10 5 5060 sipserver.example.com.` |
| PTR   | Pointer Record         | Reverse DNS: IP to hostname                                             | `1.2.0.192.in-addr.arpa. IN PTR www.example.com.` |

> `IN` stands for "Internet" – the most common DNS class used.

---

## Why DNS Matters for Web Recon

DNS is a treasure trove for pentesters and security analysts:

### Uncovering Assets
- Discover subdomains, outdated servers, or test environments through records like CNAME.

### Mapping Infrastructure
- Analyze A, NS, MX records to understand network layout and identify weaknesses.

### Monitoring Changes
- Watch for new subdomains (e.g., `vpn.example.com`) or revealing TXT records.

---

**Cheat Sheet Summary**: DNS resolves names to IPs, enabling internet communication. It includes multiple layers and record types. It’s also a vital tool in development, security, and infrastructure mapping.
