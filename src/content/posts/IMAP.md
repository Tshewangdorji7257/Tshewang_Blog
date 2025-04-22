---
title: IMAP
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

### **IMAP vs POP3 - Key Differences**
| Feature | IMAP | POP3 |
|--------|------|------|
| Access | Online access to emails directly on the server | Downloads and deletes emails from the server |
| Folder Support | Yes (supports folders & subfolders) | No |
| Synchronization | Two-way sync across multiple devices | One-way download to client |
| Storage | Emails stay on server | Emails stored locally after download |
| Port | 143 (unencrypted), 993 (SSL/TLS) | 110 (unencrypted), 995 (SSL/TLS) |
| Use Case | Multi-device, always-connected email access | Offline, single-device email access |

---

### **Common IMAP Commands**
| Command | Description |
|---------|-------------|
| `LOGIN username password` | Authenticates the user |
| `LIST "" *` | Lists all mailboxes |
| `SELECT INBOX` | Access specific mailbox |
| `FETCH <ID> all` | Retrieve message data |
| `LOGOUT` | Ends session |

---

### **Common POP3 Commands**
| Command | Description |
|---------|-------------|
| `USER <username>` | Identify user |
| `PASS <password>` | Authenticate user |
| `LIST` | Lists messages and sizes |
| `RETR <id>` | Retrieve specific message |
| `DELE <id>` | Delete specific message |
| `QUIT` | Ends session |

---

### **Security Concerns & Misconfigurations**
| Setting | Risk |
|--------|------|
| `auth_debug`, `auth_debug_passwords` | Exposes sensitive info in logs |
| `auth_verbose_passwords` | Logs cleartext passwords |
| `auth_anonymous_username` | Allows anonymous access (risky!) |
| **Unencrypted connections** | Usernames & passwords sent in plain text unless SSL/TLS is used |

---

### **Enumeration Tips**
- Use **Nmap** to scan common ports:  
  `nmap -sV -p 110,143,993,995 -sC <ip>`
- Look at **certificate details** for domain info (e.g. `mail1.inlanefreight.htb`)
- Use **curl** or **openssl s_client** to test login and capabilities:
  ```bash
  curl -k 'imaps://<ip>' --user <user>:<pass> -v
  openssl s_client -connect <ip>:993
  ```

---

### **Practical Testing Tips**
1. Set up a VM and install Dovecot:
   ```bash
   sudo apt install dovecot-imapd dovecot-pop3d
   ```
2. Test commands manually with telnet or openssl.
3. Explore `dovecot.conf` for authentication and logging configurations.

