---
title: Firewall Setup
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Linux
draft: false
---

# Firewall Setup

Firewalls serve as crucial security mechanisms for controlling and monitoring network traffic between different network segments. They filter incoming and outgoing traffic based on predefined rules, protocols, ports, and other criteria to prevent unauthorized access and mitigate security threats.

## Linux Firewall Evolution

Linux firewall capabilities have evolved significantly, with iptables becoming the standard firewall solution since its introduction in Linux 2.4 kernel in 2000. Modern alternatives include nftables, ufw, and firewalld, each offering different advantages:

- **iptables**: Traditional, widely-used solution
- **nftables**: Modern syntax with improved performance
- **ufw**: User-friendly interface built on iptables
- **firewalld**: Dynamic solution with zone-based configuration


- **Filter Table**: Handles basic packet filtering (ACCEPT/DROP/REJECT)
- **NAT Table**: Manages Network Address Translation
- **Mangle Table**: Modifies packet headers and marks packets
- **Raw Table**: Handles special packet processing

When a packet enters the system, it passes through these tables in a specific order:

1. Raw table (PREROUTING)
2. Mangle table (PREROUTING)
3. NAT table (PREROUTING)
4. Routing decision
5. Filter table (INPUT/FORWARD)
6. Mangle table (OUTPUT)
7. NAT table (POSTROUTING)
8. Raw table (OUTPUT)

## Basic Iptables Commands

Here are the essential commands for managing your firewall:

```bash
# Block incoming traffic on TCP/8080
sudo iptables -A INPUT -p tcp --dport 8080 -j DROP

# Allow incoming traffic on TCP/8080
sudo iptables -A INPUT -p tcp --dport 8080 -j ACCEPT

# Block traffic from specific IP
sudo iptables -A INPUT -s 192.168.1.100 -j DROP

# Allow traffic from specific IP
sudo iptables -A INPUT -s 192.168.1.100 -j ACCEPT

# Block traffic based on protocol
sudo iptables -A INPUT -p tcp -j DROP

# Allow traffic based on protocol
sudo iptables -A INPUT -p tcp -j ACCEPT

# Create new chain
sudo iptables -N mychain

# Forward traffic to chain
sudo iptables -A INPUT -j mychain

# Delete specific rule
sudo iptables -D INPUT -p tcp --dport 8080 -j DROP

# List all rules
sudo iptables -L -v -n
```

## Common Matches

Use these matches to specify traffic criteria:

```bash
# Protocol match
-p tcp/udp/icmp

# Port matches
--dport 80    # destination port
--sport 1024  # source port

# IP address matches
-s 192.168.1.100    # source IP
-d 10.0.0.1         # destination IP

# Connection state
-m state --state NEW,ESTABLISHED

# Multiple ports
-m multiport --dports 80,443

# Rate limiting
-m limit --limit 5/min
```

## Best Practices

1. **Rule Organization**  - Place most specific rules first
  - Use chain names that describe their purpose
  - Comment important rules


2. **Security Measures**  - Default to DROP policy
  - Allow only necessary services
  - Regularly audit rules
  - Keep rules documented


3. **Performance**  - Use appropriate table for each task
  - Avoid unnecessary rule complexity
  - Consider using nftables for high-traffic systems



Remember that firewall rules are processed in order, so the first matching rule determines the packet's fate. Always test new rules carefully and maintain a backup of your configuration before making significant changes.