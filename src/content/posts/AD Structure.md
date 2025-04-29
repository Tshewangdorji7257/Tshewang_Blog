---
title: AD Structure
published: 2025-04-29
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Active Directory
draft: false
---

# Active Directory Structure

Active Directory (AD) is a directory service for Windows network environments. It is a distributed, hierarchical structure that allows for centralized management of an organization's resources, including:

- Users  
- Computers  
- Groups  
- Network devices and file shares  
- Group policies  
- Servers and workstations  
- Trusts  

AD provides authentication and authorization functions within a Windows domain environment.

A directory service such as **Active Directory Domain Services (AD DS)** gives an organization ways to store directory data and make it available to both standard users and administrators on the same network. AD DS stores information such as usernames and passwords and manages the rights needed for authorized users to access this information.

AD was first shipped with Windows Server 2000. While it provides critical capabilities, it has come under increasing attack in recent years. AD is designed to be backward-compatible, and many features are arguably not "secure by default." It is difficult to manage properly, especially in large environments where it can be easily misconfigured.

## Why It Matters

Flaws and misconfigurations in Active Directory can be used to:

- Obtain a foothold (internal access)
- Move laterally and vertically within a network
- Gain unauthorized access to protected resources (databases, file shares, source code, etc.)

AD is essentially a large database accessible to all users within the domain, regardless of their privilege level. A basic AD user account with no added privileges can be used to enumerate most AD objects, including:

- Domain Computers  
- Domain Users  
- Domain Group Information  
- Organizational Units (OUs)  
- Default Domain Policy  
- Functional Domain Levels  
- Password Policy  
- Group Policy Objects (GPOs)  
- Domain Trusts  
- Access Control Lists (ACLs)  

> **Important:** Understanding how Active Directory is set up and administered is crucial before attempting to secure or attack it.

## Hierarchical Structure

Active Directory is arranged in a hierarchical **tree** structure. Here's a breakdown:

- **Forest:** The top-level security boundary that contains one or more domains.
- **Domain:** A structure containing users, computers, and groups.
- **Organizational Units (OUs):** Containers within domains that help organize users and apply group policies.
- **Objects:** Users, groups, computers, etc., within domains and OUs.

### Example Structure

```
INLANEFREIGHT.LOCAL/
├── ADMIN.INLANEFREIGHT.LOCAL
│   ├── GPOs
│   └── OU
│       └── EMPLOYEES
│           ├── COMPUTERS
│           │   └── FILE01
│           ├── GROUPS
│           │   └── HQ Staff
│           └── USERS
│               └── barbara.jones
├── CORP.INLANEFREIGHT.LOCAL
└── DEV.INLANEFREIGHT.LOCAL
```

In this example:
- `INLANEFREIGHT.LOCAL` is the **root domain**
- `ADMIN`, `CORP`, and `DEV` are **subdomains**
- Subdomains contain OUs, users, computers, and GPOs

## Domain Trusts

Organizations that acquire other companies often link domains or forests using **trust relationships**, rather than re-creating all user accounts.

Trust relationships can introduce **security issues** if not properly configured.

### Example: Two Forests

- `INLANEFREIGHT.LOCAL`
- `FREIGHTLOGISTICS.LOCAL`

A **bidirectional trust** exists between the two. This means:

- Users in `INLANEFREIGHT.LOCAL` can access `FREIGHTLOGISTICS.LOCAL`
- Users in `FREIGHTLOGISTICS.LOCAL` can access `INLANEFREIGHT.LOCAL`

However, **child domains do not automatically trust each other across forests**. For example:

- `admin.dev.freightlogistics.local` users cannot access resources in `wh.corp.inlanefreight.local` by default.
- A **new trust** would need to be set up for direct communication between these two child domains.

---

> This knowledge forms the foundation for secure administration, penetration testing, and defense of Active Directory environments.
