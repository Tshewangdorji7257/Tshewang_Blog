---
title: Domain Information
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

This content you've shared is a **comprehensive walkthrough of passive reconnaissance techniques** in a penetration testing context, specifically focusing on **domain information enumeration** using Open Source Intelligence (OSINT) methods. Here's a breakdown and summary of the core ideas and tools mentioned, along with some insights to help digest and use the information effectively:

---

## **Key Concepts and Workflow**

### 1. **Passive Information Gathering**
- The goal is to **stay undetected** by acting like a regular user.
- You analyze the **public-facing assets** and **metadata** without directly interacting with the target's systems in a suspicious way.

---

## **Process Breakdown**

### 🔹 **Initial Website Recon**
- Understand the company's:
  - Offered services (e.g., app development, IoT, etc.)
  - Target industry
  - Underlying infrastructure and tech stack
- Use the **developer's mindset** to imagine what backend tech is likely supporting the services.

---

### **SSL Certificate Analysis**
- SSL certificates often list multiple subdomains.
- **Tool: [crt.sh](https://crt.sh)**
  - Useful for exploring **Certificate Transparency Logs**
  - Reveals all certificates ever issued for a domain

Example command:
```bash
curl -s "https://crt.sh/?q=inlanefreight.com&output=json" | jq .
```

You can grep subdomains like this:
```bash
curl -s "https://crt.sh/?q=inlanefreight.com&output=json" | jq . | grep name
```

---

### **Resolve Subdomains to IPs**
- Use `host` or `dig` to resolve subdomains
- Filter only company-hosted (non-third-party) IPs:
```bash
for i in $(cat subdomainlist); do host $i | grep "has address" | grep inlanefreight; done
```

---

### **Use Shodan for External Exposure**
- Input IPs into **Shodan** to analyze:
  - Open ports
  - Services running (e.g., nginx, SSH, Apache)
  - SSL versions
  - Geographic location
  - Organization info

```bash
for i in $(cat ip-addresses.txt); do shodan host $i; done
```

---

### **DNS Records Discovery**
- `dig any inlanefreight.com` reveals:
  - **A Records** → direct IPs of domains
  - **MX Records** → mail servers (Google in this example)
  - **NS Records** → name servers (hints at hosting provider)
  - **TXT Records** → verification tokens, SPF/DMARC settings
  - **SOA Record** → authority info about the zone

---

## **Key Takeaways**

| Type           | Usefulness                                        |
|----------------|---------------------------------------------------|
| `crt.sh`       | Discovering **subdomains via SSL certs**          |
| `host`, `dig`  | Mapping **subdomains to IP addresses**            |
| `Shodan`       | Identifying **publicly exposed services**         |
| `DNS Records`  | Understanding **email, name servers, verification** |
| `TXT Records`  | Useful for finding **3rd-party integrations**     |

---

## **Useful Tools Summary**
- `curl`, `jq` → parsing JSON from crt.sh
- `host`, `dig` → DNS queries
- `Shodan` CLI → external scanning via known IPs
- `grep`, `cut` → parsing output




