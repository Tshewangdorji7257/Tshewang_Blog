---
title: Security AD 
published: 2025-04-29
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Active Directory
draft: false
---

### **Key Active Directory Hardening Measures**

#### **1. Microsoft LAPS (Local Administrator Password Solution)**
- Randomizes and rotates local admin passwords on endpoints.
- Helps prevent **lateral movement** by attackers.

#### **2. Logging & Monitoring (Audit Policies)**
- Detects unusual or malicious activity like:
  - Unauthorized account changes.
  - Password spray or Kerberos-based attacks.
- Use **Advanced Audit Policies** to track sensitive actions.

#### **3. Group Policy Security Settings**
- Use GPOs to apply security configurations:
  - **Account policies** (e.g., password length, lockouts, Kerberos settings).
  - **Local policies** (e.g., user rights, security options).
  - **Software/Application Restrictions** (via AppLocker or SRP).
  - **Audit policies** for access, logon, and privilege use.

#### **4. Update Management (WSUS/SCCM)**
- Automate and centralize Windows patching.
- Reduce risk from unpatched systems.

#### **5. Group Managed Service Accounts (gMSA)**
- Secure service accounts with:
  - Auto-managed long passwords.
  - Non-interactive logins.
  - Cross-host usage with minimal risk.

#### **6. Security Groups Usage**
- Use role-based access via groups rather than individual permissions.
- Limit and regularly audit group memberships.

#### **7. Account Separation**
- Admins should have two accounts:
  - Regular account (daily work).
  - Admin account (admin tasks only).
- Prevents high-privilege exposure in case of compromise.

#### **8. Password Complexity + MFA**
- Use long **passphrases** or random passwords (≥12 chars).
- Avoid seasonal/company names.
- **Enforce MFA**, especially for RDP and administrative access.

#### **9. Domain Admin Account Restrictions**
- Limit Domain Admin logins to **Domain Controllers only**.
- Avoid using admin accounts on standard or internet-facing systems.

#### **10. Regular Audit of Users & Permissions**
- Identify and remove:
  - **Stale accounts**, unused service accounts.
  - **Excessive privileges**.
- Monitor sensitive groups like **Domain Admins, Enterprise Admins**.

#### **11. Logging & Threat Detection**
- Implement:
  - **Anomaly detection** (failed logins, enumeration).
  - **SIEM tools** to monitor logs.
  - Microsoft’s audit policy recommendations.

#### **12. Restricted Groups**
- Use Group Policy to tightly control:
  - Membership of local admins.
  - High-privilege groups (e.g., Enterprise Admins).

#### **13. Limit Server Roles**
- Avoid "role bloat":
  - Do not install extra roles like IIS on Domain Controllers.
  - Separate web/database/mail services onto different hosts.

#### **14. Local Admin & RDP Access Control**
- Avoid making Domain Users local admins.
- Restrict who can RDP into systems.
- Limit exposure of privileged sessions to reduce credential theft.

---

### **Summary**
Active Directory is powerful but vulnerable if left in its default state. Proper hardening requires:
- **Minimizing attack surfaces**,
- **Using principle of least privilege**, and
- **Monitoring for abuse**.

These best practices create **defense-in-depth** against modern threats.




