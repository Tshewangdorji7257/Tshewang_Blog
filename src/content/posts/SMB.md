---
title: SMB
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

# SMB (Server Message Block) Notes

## Basics
- Client-server protocol for file/print sharing
- Mainly used in Windows networks
- Cross-platform via Samba (Linux/Unix)
- Operates over:
  - TCP ports 139 (NetBIOS) 
  - TCP port 445 (direct)

## SMB Versions
| Version | Introduced In | Key Features |
|---------|--------------|-------------|
| CIFS (SMB1) | Windows NT 4.0 | Original version |
| SMB 2.0 | Windows Vista | Performance improvements |
| SMB 3.0 | Windows 8 | Encryption, multichannel |
| SMB 3.1.1 | Windows 10 | AES-128 encryption |

## Samba
- Open-source SMB implementation for Unix/Linux
- Key components:
  - `smbd`: SMB service daemon
  - `nmbd`: NetBIOS name service
- Config file: `/etc/samba/smb.conf`

## Common Configurations
```ini
[global]
workgroup = WORKGROUP
server string = Samba Server
security = user

[sharename]
path = /path/to/share
browseable = yes
read only = no
guest ok = yes
```

## Enumeration Tools

### smbclient
```bash
smbclient -L //<IP>          # List shares
smbclient //<IP>/<share>     # Connect to share
```

### rpcclient
```bash
rpcclient -U "" <IP>         # Null session
# Commands:
srvinfo                      # Server info
enumdomusers                 # List users
queryuser <RID>              # User details
netshareenumall              # List shares
```

### Other Tools
```bash
nmap -p139,445 --script smb-* <IP>
smbmap -H <IP>               # Share permissions
crackmapexec smb <IP>        # Automated enum
enum4linux-ng.py <IP> -A     # Comprehensive enum
```

## Common Findings
- Anonymous access (guest ok = yes)
- Writable shares
- User enumeration via RID brute-forcing
- Outdated SMB versions (SMB1 vulnerabilities)
- Sensitive data in shares

## Security Considerations
- Disable SMB1 if possible
- Require SMB signing
- Restrict anonymous access
- Set proper share permissions
- Monitor for unusual SMB activity
```

This covers the key points about SMB protocol, Samba configuration, enumeration techniques, and security considerations in a concise markdown format.
