---
title: Network Configuration
published: 2025-04-16
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Linux
draft: false
---
# Network Configuration

As a penetration tester, one of the essential skills is configuring and managing network settings on Linux systems. Mastering this allows us to efficiently set up testing environments, manipulate network traffic, and identify or exploit vulnerabilities. A solid understanding of Linux network configuration gives us the ability to tailor our testing approach to suit specific needs, helping optimize both our testing procedures and results.

## Network Access Control

Another vital component of network configuration is network access control (NAC). As penetration testers, we need to be well-versed in how NAC can enhance network security and the various technologies available. Key NAC models include:

| Type | Description |
| --- | --- |
| Discretionary Access Control (DAC) | Allows the owner of the resource to set permissions for who can access it |
| Mandatory Access Control (MAC) | Permissions are enforced by the operating system, not the owner of the resource, making it more secure but less flexible |
| Role-Based Access Control (RBAC) | Permissions are assigned based on roles within an organization, making it easier to manage user privileges |

## Configuring Network Interfaces

When working with Ubuntu, you can configure local network interfaces using the `ifconfig` or the `ip` command. These powerful commands allow us to view and configure our system's network interfaces. Whether we're looking to make changes to our existing network setup or need to check on the status of our interfaces, these commands can greatly simplify the process.

### Network Settings

```bash
cry0l1t3@htb:~$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
inet 178.62.32.126 netmask 255.255.192.0 broadcast 178.62.63.255
inet6 fe80::88d9:faff:fecf:797a prefixlen 64 scopeid 0x20<link>
ether 8a:d9:fa:cf:79:7a txqueuelen 1000 (Ethernet)
RX packets 7910 bytes 717102 (700.2 KiB)
RX errors 0 dropped 0 overruns 0 frame 0
TX packets 7072 bytes 24215666 (23.0 MiB)
TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
inet 10.106.0.66 netmask 255.255.240.0 broadcast 10.106.15.255
inet6 fe80::b8ab:52ff:fe32:1f33 prefixlen 64 scopeid 0x20<link>
ether ba:ab:52:32:1f:33 txqueuelen 1000 (Ethernet)
RX packets 14 bytes 1574 (1.5 KiB)
RX errors 0 dropped 0 overruns 0 frame 0
TX packets 15 bytes 1700 (1.6 KiB)
TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING> mtu 65536
inet 127.0.0.1 netmask 255.0.0.0
inet6 ::1 prefixlen 128 scopeid 0x10<host>
loop txqueuelen 1000 (Local Loopback)
RX packets 15948 bytes 24561302 (23.4 MiB)
RX errors 0 dropped 0 overruns 0 frame 0
TX packets 15948 bytes 24561302 (23.4 MiB)
TX errors 0 dropped 0 carrier 0 collisions 0

cry0l1t3@htb:~$ ip addr

Network Configuration

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6 ::1/128 scope host
valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default q
link/ether 8a:d9:fa:cf:79:7a brd ff:ff:ff:ff:ff:ff
altname enp0s3
altname ens3
inet 178.62.32.126/18 brd 178.62.63.255 scope global dynamic eth0
valid_lft 85274sec preferred_lft 85274sec
inet6 fe80::88d9:faff:fecf:797a/64 scope link
valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default q
link/ether ba:ab:52:32:1f:33 brd ff:ff:ff:ff:ff:ff
altname enp0s4
altname ens4
inet 10.106.0.66/20 brd 10.106.15.255 scope global dynamic eth1
valid_lft 85274sec preferred_lft 85274sec
inet6 fe80::b8ab:52ff:fe32:1f33/64 scope link
valid_lft forever preferred_lft forever
```

### Activating Network Interfaces

```bash
K4y0x13@htb[/htb]$ sudo ifconfig eth0 up # OR
K4y0x13@htb[/htb]$ sudo ip link set eth0 up
```

### Assigning IP Addresses

```bash
K4y0x13@htb[/htb]$ sudo ifconfig eth0 192.168.1.2
```

### Setting Netmask

```bash
K4y0x13@htb[/htb]$ sudo ifconfig eth0 netmask 255.255.255.0
```

### Setting Default Gateway

```bash
K4y0x13@htb[/htb]$ sudo route add default gw 192.168.1.1 eth0
```

## DNS Configuration

Domain Name System (DNS) servers are responsible for translating domain names into IP addresses. Proper DNS configuration is crucial for enabling devices to access websites and online services. On Linux systems, this can be achieved by updating the `/etc/resolv.conf` file:

```bash
nameserver 8.8.8.8
nameserver 8.8.4.4
```

## Network Monitoring

Network monitoring involves capturing, analyzing, and interpreting network traffic to identify security threats and suspicious behavior. Common tools include:

- syslog/rsyslog
- ss (socket statistics)
- lsof (list open files)
- ELK stack (Elasticsearch, Logstash, Kibana)

## Troubleshooting

Common network issues during penetration tests include:

1. Connectivity problems
2. DNS resolution issues
3. Loss of data packets
4. Network performance issues

Common causes:

- Incorrectly configured firewalls or routers
- Damaged network cables or connections
- Incorrect network settings
- Hardware failures
- Incorrect DNS server settings or DNS server failures
- Network congestion
- Outdated network hardware
- Unpatched software or firmware

## Hardening

Several mechanisms are highly effective in securing Linux systems:

1. SELinux (Security-Enhanced Linux)
  - Mandatory access control (MAC) system integrated into the Linux kernel
  - Provides fine-grained control over access to system resources
  - Enforces security policies defining permissions for each process and file


2. AppArmor
  - MAC system controlling access to system resources
  - Operates using application profiles
  - Simpler and more user-friendly than SELinux


3. TCP Wrappers
  - Host-based network access control tool
  - Restricts access to network services based on IP address
  - Simple yet effective for basic network-level protection



Think of network configuration in Linux like building and securing a large office building. Configuring network interfaces is like setting up the wiring and infrastructure, ensuring that each room (network device) has a working connection. NAC is like managing the building's security where some rooms are open to everyone (DAC), while others are only accessible to certain people based on strict rules (MAC or RBAC). Monitoring network traffic is similar to installing surveillance cameras and alarms, keeping an eye on who is moving through the building, and troubleshooting is like having a toolkit on hand to fix any issues—whether a broken connection (ping), a faulty lock (nslookup), or a vulnerable entrance (nmap).