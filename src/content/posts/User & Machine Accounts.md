---
title: Users & Machine Accounts
published: 2025-04-29
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Active Directory
draft: false
---

### **User and Machine Accounts Overview**

#### **1. User Accounts**
- **Purpose**: Allow users (or services) to log in and access resources.
- **Location**: Can exist on local machines or within **Active Directory (AD)**.
- **Access Token**: Created upon login; contains the user’s identity and group memberships.
- **Group Memberships**: Used for easier privilege management and access control.
- **Multiple Accounts**: Some users (e.g., IT admins) may have multiple accounts for different roles.

#### **2. Common Types of User Accounts**
- **Standard User Accounts**: Tied to individuals.
- **Admin Accounts**: With elevated privileges (e.g., Domain Admins, Enterprise Admins).
- **Service Accounts**: Used by applications/services; often have persistent elevated access.
- **Deactivated Accounts**: Often stored in OUs like "FORMER EMPLOYEES" for audit purposes.

#### **3. Local Accounts (Non-domain joined)**
- Exist only on specific hosts and cannot access domain resources.
- **Default Accounts**:
  - `Administrator`: SID ends in 500; high privileges; disabled/renamed by default in newer Windows.
  - `Guest`: Very limited access; disabled by default.
  - `SYSTEM`: OS-level account with full local privileges; doesn’t appear in User Manager.
  - `Network Service` / `Local Service`: Used by Windows services; minimal privileges.

#### **4. Domain Users**
- Can log in and access domain-wide resources.
- Controlled centrally via the **Domain Controller (DC)** and Group Policies.
- **Special Domain Account**:
  - `KRBTGT`: Used for Kerberos ticket granting; target for "Golden Ticket" attacks.

#### **5. Key User Attributes in AD**
| Attribute         | Description                                                   |
|------------------|---------------------------------------------------------------|
| **UserPrincipalName (UPN)** | Usually the user's email; primary login ID          |
| **ObjectGUID**    | Unique and unchanging identifier                             |
| **SAMAccountName**| Legacy login name (pre-Windows 2000)                         |
| **objectSID**     | User’s unique security identifier                            |
| **sIDHistory**    | Previous SIDs (useful in domain migrations)                  |

#### **6. Domain-joined vs Non-domain-joined Machines**
| Type              | Characteristics                                               |
|------------------|---------------------------------------------------------------|
| **Domain-joined** | Central management (via DC), resource access, Group Policies |
| **Non-domain**    | Independent, local resource access only, user-managed         |

- **Machine (SYSTEM) Account in AD**: Can have **similar rights** to standard domain users.
  - Valuable for enumeration even without user credentials.
  - SYSTEM access via RCE or privilege escalation can be leveraged for domain reconnaissance.

