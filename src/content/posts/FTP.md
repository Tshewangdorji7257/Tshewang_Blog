---
title: FTP
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

# FTP (File Transfer Protocol) Notes

## Basics
- One of the oldest Internet protocols
- Operates in the application layer (same as HTTP/POP)
- Uses two channels:
  - Control channel (TCP port 21) for commands
  - Data channel (TCP port 20) for file transfers

## Connection Modes
1. **Active Mode**
   - Client opens control channel
   - Server connects back to client for data
   - Firewall issues possible

2. **Passive Mode**
   - Server provides port for data connection
   - Client initiates both channels
   - Better for firewalled clients

## Security
- Clear-text protocol (credentials can be sniffed)
- Supports anonymous access (no password)
- Some servers offer TLS/SSL encryption

## TFTP (Trivial File Transfer Protocol)
- Simpler than FTP
- No authentication
- Uses UDP instead of TCP
- Limited to local/protected networks

## vsFTPd (Common Linux FTP Server)
- Config file: `/etc/vsftpd.conf`
- Important settings:
  - `anonymous_enable` - Allow anonymous access
  - `local_enable` - Allow local user logins
  - `write_enable` - Allow file uploads
  - `chroot_local_user` - Restrict users to home dirs

## Common Commands
```bash
ftp <host>          # Connect to FTP server
ls                  # List files
get <file>          # Download file
put <file>          # Upload file
quit                # Exit
```

## Enumeration Tools
```bash
nmap -sV -p21 -sC -A <target>  # Scan FTP service
openssl s_client -connect <host>:21 -starttls ftp  # Check SSL
wget -m --no-passive ftp://anonymous@<host>  # Download all files
```

## Security Considerations
- Check for anonymous access
- Look for writable directories
- Check version for known vulnerabilities
- Try uploading files (potential web server access)
