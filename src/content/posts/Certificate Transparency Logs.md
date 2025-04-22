---
title: Certificate Transparency Logs
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

## Certificate Transparency Logs — Summary

### What are CT Logs?
- **Public, append-only logs** of SSL/TLS certificates.
- Managed by independent organizations.
- CAs must log every certificate they issue.

### Why They Matter
- **Early detection** of rogue or mis-issued certificates.
- **Holds Certificate Authorities accountable.**
- **Strengthens Web PKI** (Public Key Infrastructure).
- Allows **anyone** to monitor, audit, and verify SSL/TLS certificates.

---

## 🔍 Recon with CT Logs

### Benefits for Subdomain Enumeration
- **Accurate & historical**: Lists **all** subdomains that ever had a certificate.
- **Bypasses brute-force & wordlist limits**.
- Can reveal:
  - Expired/unused subdomains
  - Development/staging environments
  - Misconfigured or forgotten services

---

## Tools to Search CT Logs

| Tool     | Features | Pros | Cons |
|----------|----------|------|------|
| `crt.sh` | Simple UI, API access, shows SAN entries | No registration, fast | Limited filters |
| `Censys` | Advanced filters, broader data | Deep analysis, API access | Needs account |

---

## Practical Usage: `crt.sh` API + `jq`

```bash
curl -s "https://crt.sh/?q=facebook.com&output=json" \
| jq -r '.[] | select(.name_value | contains("dev")) | .name_value' \
| sort -u
```

### What this does:
- Pulls **certificate data for facebook.com** from `crt.sh`.
- Filters only those that **include "dev"** in the domain/subdomain.
- **Sorts** and removes **duplicates**.

### Real-World Examples Output
```
*.dev.facebook.com
dev.facebook.com
secure.dev.facebook.com
newdev.facebook.com
facebook-amex-dev.facebook.com
```

---

## Pro Tips
- Look for subdomains like `admin`, `staging`, `dev`, `test`, etc.
- Use in **combo with DNS zone transfers, subdomain brute-forcing**, and **Nmap scanning** for a complete recon.


