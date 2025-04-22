---
title: NFS
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

## **What is NFS?**
- **Network File System (NFS)** allows access to remote filesystems as if they were local.
- Primarily used between **Linux/Unix systems** (not compatible with SMB).
- Built on **ONC-RPC/SUN-RPC**, communicates over **TCP/UDP port 2049**, and uses **XDR** for data exchange.

---

## **NFS Versions and Features**

| Version | Features |
|--------|---------|
| **NFSv2** | Older, UDP-based, widely supported. |
| **NFSv3** | Adds variable file size, better error reporting, still authenticates computers (not users). |
| **NFSv4** | User-based auth (like SMB), supports ACLs, Kerberos, works over the Internet, stateful protocol. |
| **NFSv4.1** | Adds **pNFS** (parallel access), session trunking (multipathing), simplified firewall handling with single port (2049). |

---

## **Security & Authentication**
- **UID/GID-based authentication**: Clients and servers must match mappings.
- **No user-level checks** by NFS itself — risky on untrusted networks.
- Use **Kerberos** (NFSv4) for secure, user-based auth.

---

## **Important Config Files**
### `/etc/exports`
Defines which directories are shared and with what permissions.
Example:
```bash
/mnt/nfs 10.129.14.0/24(sync,no_subtree_check)
```

### Common Export Options
| Option            | Description                                                                 |
|-------------------|------------------------------------------------------------------------------|
| `rw`              | Read/write access                                                            |
| `ro`              | Read-only access                                                             |
| `sync`            | Writes data immediately                                                      |
| `async`           | Delays write for performance (risky)                                         |
| `secure`          | Only allows access from ports < 1024                                         |
| `insecure`        | Allows access from ports > 1024 (less secure)                                |
| `no_subtree_check`| Prevents subtree checking (faster)                                           |
| `root_squash`     | Maps root UID 0 to anonymous user — prevents remote root access              |
| `no_root_squash`  | Dangerous — keeps root UID 0 permissions (avoid!)                            |

---

## **Dangerous Export Settings**
- `rw`, `insecure`, `nohide`, and especially `no_root_squash` can be **very risky**.

---

## **NFS Enumeration & Exploitation**
### Nmap Scan
```bash
sudo nmap -p111,2049 -sV -sC <target-ip>
sudo nmap --script nfs* -p111,2049 -sV <target-ip>
```
- Use Nmap scripts like `nfs-ls`, `nfs-showmount`, and `rpcinfo`.

### Discover Shares
```bash
showmount -e <target-ip>
```

### Mounting Shares
```bash
mkdir target-NFS
sudo mount -t nfs <target-ip>:/ ./target-NFS/ -o nolock
```

---

## **Privilege Escalation Vector**
If you find files owned by specific UIDs/GIDs (e.g., root or another user), you can:
1. **Create a user on your local system** with the same UID/GID.
2. **Access or modify** those files via the mounted NFS share.

```bash
sudo adduser --uid 0 attacker
```

---

## **Hands-On Practice**
You’re encouraged to set up:
- A **local VM** with multiple exports.
- Vary **export options**.
- Explore **access levels** and **user mapping**.
- Try combining Nmap enumeration + UID matching for privilege gain.

