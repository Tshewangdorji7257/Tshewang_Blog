---
title: AD Objects
published: 2025-04-29
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Active Directory
draft: false
---

### **What Is an Active Directory Object?**
An **object** in AD refers to **any resource** stored in the AD environment, including users, groups, computers, printers, OUs, and more.

---

### **Types of Active Directory Objects**

| **Object**              | **Description**                                                                                                                                     | **Security Principal?** | **Container or Leaf?** |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|------------------------|
| **Users**               | Represent individuals in the AD environment. Contain many attributes (e.g., login times, email, etc.).                                              | Yes (has SID & GUID)  | Leaf                   |
| **Contacts**            | Represent external entities like vendors. Hold contact info only.                                                                                  | No (GUID only)        | Leaf                   |
| **Printers**            | Pointers to network-accessible printers.                                                                                                            | No (GUID only)        | Leaf                   |
| **Computers**           | Represent devices joined to the AD domain. Important for authentication and access control.                                                         | Yes (has SID & GUID)  | Leaf                   |
| **Shared Folders**      | Represent shared directories on networked systems. Access can be restricted via permissions.                                                        | No (GUID only)        | Leaf                   |
| **Groups**              | Contain users, computers, or other groups. Used to assign permissions collectively. Supports **nested groups**.                                     | Yes (has SID & GUID)  | Container              |
| **Organizational Units (OUs)** | Used for organizing objects. Enable **delegation** of administrative tasks and applying **Group Policy**.                                      | No (GUID only)        | Container              |
| **Domain**              | The top-level structure in AD. Contains all other objects and enforces policies.                                                                    |  Yes                   | Container              |
| **Domain Controllers**  | Servers that manage authentication, access control, and enforce policies. Central authority of the domain.                                          | Yes                   | Special role           |
| **Sites**               | Represent one or more IP subnets with fast interconnects. Used to optimize **replication** between domain controllers.                              | No                    | Container              |
| **Built-in**            | Contains default AD groups created during domain setup.                                                                                             | (groups inside)       | Container              |
| **Foreign Security Principals (FSPs)** | Represent users/groups from **trusted external forests**. Auto-created when such entities are added to groups in the current domain.       | Yes (has external SID) | Leaf                   |

---

### Key Terms:
- **Leaf Object**: Cannot contain other objects (e.g., user, printer).
- **Container Object**: Can hold other objects (e.g., group, OU).
- **Security Principal**: Objects that can be assigned permissions (have a **SID**).
- **SID**: Security Identifier.
- **GUID**: Global Unique Identifier.

