---
title: Virtual Hosts
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

# Virtual Hosts

## What are Virtual Hosts?
Virtual hosts allow web servers (like Apache, Nginx, or IIS) to host multiple websites or applications on a single server by differentiating between domains, subdomains, or separate websites.

## VHosts vs. Subdomains

### Subdomains
- Extensions of a main domain (e.g., `blog.example.com` is a subdomain of `example.com`)
- Typically have their own DNS records
- Can point to the same IP as the main domain or a different one
- Used to organize different sections or services of a website

### Virtual Hosts (VHosts)
- Server configurations that enable multiple websites on a single server
- Can be associated with domains or subdomains
- Each virtual host can have separate configurations
- Can be accessed even without DNS records by modifying the local hosts file

## How Virtual Hosts Work

1. **Browser Request**: User enters a domain name in their browser
2. **Host Header**: Browser sends HTTP request with the domain in the Host header
3. **Server Processing**: Web server examines the Host header and finds matching configuration
4. **Content Delivery**: Server retrieves files from the corresponding document root
5. **Response**: Server sends the appropriate content back to the browser

### Example Apache Configuration
```apache
<VirtualHost *:80>
    ServerName www.example1.com
    DocumentRoot /var/www/example1
</VirtualHost>

<VirtualHost *:80>
    ServerName www.example2.org
    DocumentRoot /var/www/example2
</VirtualHost>

<VirtualHost *:80>
    ServerName www.another-example.net
    DocumentRoot /var/www/another-example
</VirtualHost>
```

## Types of Virtual Hosting

### 1. Name-Based Virtual Hosting
- Uses HTTP Host header to distinguish between websites
- Most common and flexible method
- Doesn't require multiple IP addresses
- Limitations with certain protocols like SSL/TLS

### 2. IP-Based Virtual Hosting
- Assigns unique IP address to each website
- Doesn't rely on Host header
- Can be used with any protocol
- Better isolation between websites
- Requires multiple IP addresses (less scalable)

### 3. Port-Based Virtual Hosting
- Different websites use different ports on same IP
- Example: one site on port 80, another on port 8080
- Useful when IP addresses are limited
- Less user-friendly (requires port number in URL)

## Virtual Host Discovery Tools

| Tool | Description | Features |
|------|-------------|----------|
| gobuster | Multi-purpose tool for directory/file brute-forcing and vhost discovery | Fast, supports multiple HTTP methods, custom wordlists |
| Feroxbuster | Rust-based implementation similar to Gobuster | Supports recursion, wildcard discovery, various filters |
| ffuf | Fast web fuzzer that can fuzz Host headers | Customizable wordlist input and filtering options |

## Using Gobuster for VHost Discovery

### Prerequisites
1. Target web server's IP address
2. Wordlist with potential virtual host names

### Basic Command
```bash
gobuster vhost -u http://<target_IP_address> -w <wordlist_file> --append-domain
```

### Options
- `-u`: Target URL
- `-w`: Path to wordlist
- `--append-domain`: Appends base domain to each word in wordlist
- `-t`: Increase threads for faster scanning
- `-k`: Ignore SSL/TLS certificate errors
- `-o`: Save output to file

### Example Output
```
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url: http://inlanefreight.htb:81
[+] Method: GET
[+] Threads: 10
[+] Wordlist: /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt
[+] User Agent: gobuster/3.6
[+] Timeout: 10s
[+] Append Domain: true
===============================================================
Starting gobuster in VHOST enumeration mode
===============================================================
Found: forum.inlanefreight.htb:81 Status: 200 [Size: 100]
[...]
Progress: 114441 / 114442 (100.00%)
===============================================================
Finished
===============================================================
```

> **Note:** Virtual host discovery can generate significant traffic and might be detected by intrusion detection systems (IDS) or web application firewalls (WAF). Exercise caution and obtain proper authorization before scanning.