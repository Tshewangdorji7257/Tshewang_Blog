---
title: Nmap Firewall/IDS Evasion
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Nmap
draft: false
---

# Nmap Firewall & IDS/IPS Evasion

## Detection Methods
- **Filtered Ports**: May indicate firewall presence (dropped or rejected packets)
- **Rejected Packets**: Return RST flag with ICMP errors:
  - Net/Host Unreachable
  - Net/Host Prohibited
  - Port/Proto Unreachable

## Evasion Techniques

### Scan Types
```bash
# ACK Scan (harder to filter)
nmap -sA -p 21,22,25 10.129.2.28

# SYN Scan (standard stealth)
nmap -sS -p 21,22,25 10.129.2.28
```

### Decoy Scanning
```bash
# Random decoys (position 2 is real IP)
nmap -D RND:5 -p 80 -sS 10.129.2.28

# Manual decoys
nmap -D decoy1,decoy2,ME,decoy3 -p 80 10.129.2.28
```

### Source Manipulation
```bash
# Spoof source IP
nmap -S 10.129.2.200 -e tun0 10.129.2.28

# Use specific source port
nmap --source-port 53 -p 50000 -sS 10.129.2.28
```

### DNS Tricks
```bash
# Specify DNS servers
nmap --dns-servers 8.8.8.8,1.1.1.1

# DNS tunneling (when TCP/53 is open)
ncat -nv --source-port 53 10.129.2.28 50000
```

## IDS/IPS Detection
1. Use multiple VPS with different IPs
2. Start with aggressive scans to test monitoring
3. If blocked, switch to stealthier approaches:
   - Slower timing (`-T2`)
   - Fragmented packets (`-f`)
   - IP spoofing

## Timing & Performance
| Option | Effect |
|--------|--------|
| `-T0` | Paranoid (slowest) |
| `-T3` | Normal (default) |
| `-T5` | Insane (fastest) |
| `--max-rtt-timeout` | Adjust round-trip timeout |
| `--scan-delay` | Add delay between probes |

## Best Practices
1. Always start with stealth scans (`-sS`)
2. Use decoys when scanning sensitive networks
3. Try alternative source ports (53, 80, 443)
4. Fragment packets (`-f`) to evade simple filters
5. Combine techniques for better evasion
6. Have multiple scanning hosts ready

> Warning: Aggressive scans may trigger blocks - always have fallback options.
``` 

This version keeps all key information while being much more concise and organized for quick reference. The markdown formatting makes it easy to read and use as a cheat sheet.