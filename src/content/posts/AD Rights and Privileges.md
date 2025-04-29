---
title: AD Rights and Privileges
published: 2025-04-29
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Active Directory
draft: false
---

### **Difference Between Rights and Privileges**

- **Rights**: Permissions to access *objects* (e.g., files, folders).
- **Privileges**: Permissions to *perform actions* (e.g., shut down a system, debug processes).
- **User Rights Assignment** (via GPO): Assigns **privileges**, though often called “rights.”

---

### **Key Built-in AD Groups and Their Security Impact**

| Group Name              | Description & Risk                                                                 |
|------------------------|-------------------------------------------------------------------------------------|
| **Administrators**      | Full control over a system or domain; compromising this = full domain takeover.   |
| **Domain Admins**       | Full domain-wide privileges; highly sensitive.                                    |
| **Enterprise Admins**   | Forest-level privileges; can create domains/trusts.                               |
| **Backup Operators**    | Can back up sensitive files (SAM, NTDS.dit) → extract credentials.                |
| **DnsAdmins**           | Can load DLLs via DNS service exploitation.                                       |
| **Server Operators**    | Can manage services, SMB shares, and local access on DCs.                         |
| **Print Operators**     | Can potentially load malicious drivers.                                           |
| **Hyper-V Admins**      | Can control virtual DCs → full domain control possible.                           |
| **Schema Admins**       | Can modify AD schema → irreversible and dangerous.                               |
| **Pre-Windows 2000 Compatible Access** | Often misconfigured, can allow unauthorized reads of AD info.      |

---

### **Privilege Escalation via User Rights Assignment**

Certain **privileges** can be leveraged by attackers for lateral movement or privilege escalation:

| Privilege | Abuse Potential |
|-----------|-----------------|
| **SeBackupPrivilege** | Read sensitive files like NTDS.dit or SAM. |
| **SeDebugPrivilege** | Hook into LSASS memory (e.g., Mimikatz) to extract creds. |
| **SeImpersonatePrivilege** | Token impersonation (e.g., *JuicyPotato*). |
| **SeLoadDriverPrivilege** | Load malicious drivers. |
| **SeTakeOwnershipPrivilege** | Take ownership of restricted objects. |
| **SeRemoteInteractiveLogonRight** | RDP access; potential lateral movement. |

---

### **Checking User Privileges**

Use:

```powershell
whoami /priv
```

- **Standard users** have minimal rights.
- **Domain Admins** show limited rights in non-elevated shells (due to **UAC**).
- **Elevated shell** (`Run as Administrator`) reveals full privileges.

Example rights seen **only in elevated contexts**:
- `SeDebugPrivilege`
- `SeBackupPrivilege`
- `SeTakeOwnershipPrivilege`
- `SeLoadDriverPrivilege`
- `SeImpersonatePrivilege`

---

### **Best Practices**

- **Limit membership** in high-privilege groups (e.g., Domain Admins, Backup Operators).
- **Monitor changes** in group memberships using auditing tools.
- **Regularly audit** rights assigned through GPOs.
- **Avoid assigning powerful privileges** to unnecessary service accounts or legacy accounts.
- **Disable or remove** unused built-in groups like "Pre–Windows 2000 Compatible Access".

