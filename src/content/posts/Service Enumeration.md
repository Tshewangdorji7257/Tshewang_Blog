---
title: Service Enumeration
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Nmap
draft: false
---

# Nmap Service Enumeration

## Why Service Enumeration Matters
- Identifies exact application versions
- Helps find known vulnerabilities
- Allows targeted exploit research

## Basic Service Scan
```bash
sudo nmap 10.129.2.28 -p- -sV
```

### Key Options:
- `-p-`: Scan all ports
- `-sV`: Service version detection

## Monitoring Scan Progress
1. **During scan**: Press [Space Bar] to see status
2. **Automatic updates**: 
   ```bash
   --stats-every=5s  # Updates every 5 seconds
   ```
3. **Verbose output**:
   ```bash
   -v  # Basic verbosity
   -vv # Higher verbosity (shows open ports immediately)
   ```

## Understanding Results
Example output:
```
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 7.6p1 Ubuntu 4ubuntu0.3
80/tcp  open  http     Apache httpd 2.4.29 ((Ubuntu))
```

## Banner Grabbing
Nmap reads service banners, but sometimes misses details. For manual verification:
```bash
nc -nv 10.129.2.28 25
```

## Advanced Scanning Options
```bash
sudo nmap 10.129.2.28 -p- -sV -Pn -n --disable-arp-ping --packet-trace
```
- `-Pn`: Skip host discovery (treat all hosts as online)
- `-n`: No DNS resolution
- `--disable-arp-ping`: Disable ARP ping
- `--packet-trace`: Show all packets sent/received

## Network Traffic Analysis
Three-way handshake visible in tcpdump:
1. [SYN] → Client initiates connection
2. [SYN-ACK] ← Server acknowledges
3. [ACK] → Client confirms
4. [PSH-ACK] ← Server sends banner/data
5. [ACK] → Client acknowledges receipt

## Best Practices
1. Start with quick scans before comprehensive version detection
2. Combine with output saving (`-oA`) for documentation
3. Verify critical findings manually
4. Check filtered ports for potential firewall evasion opportunities
```

This condensed version keeps all the essential information while making it more scannable and organized. The markdown formatting allows for easy reading and can be directly used in documentation or note-taking apps.