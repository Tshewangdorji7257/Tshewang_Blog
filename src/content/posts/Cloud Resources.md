---
title: Cloud Resources
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

#### 1. **Cloud Resource Centralization**
- **Cloud providers** like AWS, GCP, and Azure offer centralized management, allowing remote access and operations.
- While cloud infrastructure is **secure by default**, **misconfigurations by users/admins** often create vulnerabilities.

#### 2. **Common Cloud Storage Risks**
- Public exposure of:
  - **S3 buckets (AWS)**
  - **Blobs (Azure)**
  - **Cloud Storage (GCP)**
- Misconfigurations may lead to unauthenticated access—**a major data breach vector**.

#### 3. **Enumeration via Subdomain Discovery**
```bash
for i in $(cat subdomainlist); do host $i | grep "has address" | grep inlanefreight; done
```
- Example shows resolving multiple subdomains linked to `inlanefreight.com`, including one pointing to an AWS S3 endpoint (`s3-website-us-west-2.amazonaws.com`).

#### 4. **Reconnaissance Using Google Dorks**
- Example dorks:
  - `inurl:companyname filetype:pdf`
  - `intext:confidential filetype:docx`
- Goal: discover **publicly exposed files** like presentations, documents, source code.

#### 5. **Source Code & CDN Discovery**
- Source code may contain links to JS, CSS, or images stored on cloud (e.g., S3).
- Reduces server load but may accidentally expose sensitive paths.

#### 6. **Third-Party Recon Tools**
- **domain.glass**: Can reveal subdomains, DNS records, or CDN usage (e.g., Cloudflare status).
- **GrayHatWarfare**: Search and filter exposed files in public cloud buckets by type and storage provider.

#### 7. **Naming Patterns & Abbreviations**
- Companies often use **internal acronyms or short names** in bucket names or directories (e.g., `abc-bucket.s3.amazonaws.com`).
- Recognizing naming conventions aids in brute-forcing or educated guessing during enumeration.

#### 8. **Leaked Private SSH Keys**
- One of the most dangerous exposures.
- Private keys uploaded to public repos or buckets may allow attackers **unauthorized SSH access** to company infrastructure.
- Never store SSH private keys in unprotected public locations.

---

### **Security Implications**
- Even with secure infrastructure, **human error** is the biggest threat.
- Always enforce:
  - **Least privilege access**
  - **Proper IAM policies**
  - **Regular audits and penetration testing**
  - **Use of cloud-native security tools** (e.g., AWS Macie, Azure Defender)


