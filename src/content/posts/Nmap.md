---
title: Intro to Nmap
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Nmap
draft: false
---
# Introduction to Nmap

Nmap (Network Mapper) is a powerful open-source network analysis and security auditing tool that helps identify hosts, services, and operating systems on a network. It uses raw packets to scan networks and detect available hosts, services, and applications, making it an essential tool for network administrators and security specialists.

## Common Use Cases

- Network security auditing
- Penetration testing simulation
- Firewall and IDS configuration verification
- Network mapping and discovery
- Port scanning and service identification
- Vulnerability assessment

## Basic Usage Example

```bash
# Basic SYN scan
sudo nmap -sS localhost

# Output example:
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-11 22:50 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000010s latency).
Not shown: 996 closed ports
PORT STATE SERVICE
22/tcp open ssh
80/tcp open http
5432/tcp open postgresql
5901/tcp open vnc-1
Nmap done: 1 IP address (1 host up) scanned in 0.18 seconds
```

## Common Scan Types Explained

1. **TCP SYN Scan (-sS)**  - Sends SYN packet and waits for SYN-ACK
  - Never completes three-way handshake
  - Fast and stealthy
  - Default scan type for privileged users


2. **TCP Connect Scan (-sT)**  - Completes full TCP handshake
  - More reliable but slower
  - Works without root privileges
  - More detectable by firewalls


3. **UDP Scan (-sU)**  - Connectionless protocol scanning
  - Slower due to timeout waiting
  - Useful for firewall testing
  - Good for discovering hidden services


4. **Idle Scan (-sI)**  - Uses zombie host for scanning
  - Completely stealthy
  - Complex to set up
  - Requires suitable zombie host



## Port States

- **Open**: Service is accepting connections
- **Closed**: No service is listening
- **Filtered**: Packet is being blocked
- **Unfiltered**: Port is accessible but no service

## Best Practices

1. **Scan Selection**  - Use appropriate scan type for the situation
  - Consider network conditions
  - Think about detection avoidance needs


2. **Performance Optimization**  - Use appropriate timing options
  - Limit port ranges when possible
  - Consider using script scanning for specific tasks


3. **Output Management**  - Save results for later analysis
  - Use different output formats as needed
  - Filter results for specific information



Nmap is a powerful tool that requires understanding of network protocols and scanning techniques. Mastering its various scan types and options can significantly improve your network security assessment capabilities.