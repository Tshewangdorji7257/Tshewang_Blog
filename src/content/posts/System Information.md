---
title: System Information
published: 2025-04-16
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Linux
draft: false
---
# System Information in Linux

Now, let’s dive into some hands-on practice to get comfortable using the terminal and shell. Remember:  
You can always use `-h`, `--help`, or `man` commands for guidance.

Understanding system structure — including system details, processes, network configurations, users, and directories — is essential not only for everyday Linux tasks but also for security assessments, vulnerability identification, and mitigation of potential risks.

---

## Essential System Information Commands

| **Command** | **Description** |
|-------------|-----------------|
| `whoami` | Displays current username |
| `id` | Returns user identity and group memberships |
| `hostname` | Displays or sets the system’s hostname |
| `uname` | Prints basic info about OS and system hardware |
| `pwd` | Prints the current working directory |
| `ifconfig` | Configures and views network interfaces |
| `ip` | Manages network interfaces, routing, etc. |
| `netstat` | Displays network status |
| `ss` | Investigates sockets (replacement for `netstat`) |
| `ps` | Displays process status |
| `who` | Shows who is logged in |
| `env` | Prints environment variables |
| `lsblk` | Lists block devices |
| `lsusb` | Lists USB devices |
| `lsof` | Lists open files |
| `lspci` | Lists PCI devices |

---

## Logging in via SSH

SSH (Secure Shell) is a protocol used to remotely access and manage Unix-like systems.

### SSH Command Example:
```bash
ssh htb-student@[IP address]
