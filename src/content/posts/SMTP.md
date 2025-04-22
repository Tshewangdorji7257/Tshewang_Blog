---
title: SMTP
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

### **SMTP Basics**
- **Purpose:** Sends email from client (MUA) to server (MTA), or between MTAs.
- **Default Port:** `25` (plaintext); **Secure alternatives:** 
  - `587` (STARTTLS – plaintext upgraded to TLS)
  - `465` (implicit SSL/TLS)

---

### **Email Transmission Path**
`MUA (Client)` → `MSA (Relay)` → `MTA` → `MDA` → `Mailbox (via POP3/IMAP)`

---

### **Common SMTP Issues & Attacks**
1. **Open Relay Misconfiguration**
   - If `mynetworks = 0.0.0.0/0`, anyone can send emails through the server (abused for spam/phishing).
2. **No Authentication or Encryption by Default**
   - SMTP transmits **everything in plaintext** unless encrypted via STARTTLS/SSL.
3. **Spoofing & Spam**
   - Since authentication is not required by default, sender identity can be faked (mail spoofing).
   - Tools like SPF, DKIM, DMARC help fight this.

---

### **Security Features**
- **STARTTLS:** Initiates TLS encryption.
- **SMTP AUTH (AUTH PLAIN):** Authenticates users to prevent unauthorized use.
- **ESMTP:** Extended SMTP, adds support for additional commands like `STARTTLS`, `AUTH`, etc.

---

### **Pentesting Techniques**
- **VRFY / EXPN:** Can be used for user enumeration (though not always reliable).
- **Manual Mail Sending via `telnet`:**
   - `EHLO`, `MAIL FROM:`, `RCPT TO:`, `DATA`, etc.
   - Useful for testing server behavior or spoofing attempts.
- **Nmap Scripts:**
   - `smtp-commands`: Lists supported commands.
   - `smtp-open-relay`: Tests if server allows unauthenticated mail relay.

---

### Practical Use Case (Pentesting)
You could combine enumeration and spoofing like this:
```bash
telnet <target> 25
EHLO attackdomain.com
MAIL FROM:<fake@trusted.com>
RCPT TO:<victim@target.com>
DATA
Subject: Urgent - Reset Your Password
...
.
QUIT
```
If the server accepts it and relays the message, **you’ve confirmed an open relay**.

