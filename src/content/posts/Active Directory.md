---
title: Active Directory
published: 2025-04-29
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Active Directory
draft: false
---

# Why Active Directory?

Active Directory (AD) is a directory service for Windows network environments. It is a distributed, hierarchical structure that allows for centralized management of an organization's resources, including users, computers, groups, network devices, file shares, group policies, devices, and trusts.

AD provides authentication and authorization functions within a Windows domain environment. It has come under increasing attack in recent years. It is designed to be backward-compatible, and many features are arguably not "secure by default," and it can be easily misconfigured. This weakness can be leveraged to move laterally and vertically within a network and gain unauthorized access.

AD is essentially a sizeable read-only database accessible to all users within the domain, regardless of their privilege level. A basic AD user account with no added privileges can enumerate most objects within AD. This fact makes it extremely important to properly secure an AD implementation because **any user account**, regardless of their privilege level, can be used to enumerate the domain and hunt for misconfigurations and flaws thoroughly.

Also, multiple attacks can be performed with only a standard domain user account, showing the importance of a **defense-in-depth strategy** and careful planning focusing on **security and hardening AD**, **network segmentation**, and **least privilege**. One example is the **noPac** attack that was first released in December of 2021.

Active Directory makes information easy to find and use for administrators and users. AD is **highly scalable**, supports **millions of objects per domain**, and allows the creation of additional domains as an organization grows.

## Why It Matters

It is estimated that around **95% of Fortune 500 companies run Active Directory**, making AD a key focus for attackers. A successful attack such as a phish that lands an attacker within the AD environment as a standard domain user would give them enough access to begin mapping out the domain and looking for avenues of attack.

As security professionals, we will encounter AD environments of all sizes throughout our careers. It is essential to understand the **structure and function of AD** to become better informed as both an attacker and a defender.

**Ransomware operators** have been increasingly targeting Active Directory as a key part of their attack paths. The **Conti Ransomware**, which has been used in more than 400 attacks around the world, has been shown to leverage recent critical Active Directory flaws such as:

- **PrintNightmare** (CVE-2021-34527)
- **Zerologon** (CVE-2020-1472)

These flaws are used to escalate privileges and move laterally in a target network.

Understanding the structure and function of Active Directory is the first step in a career path to find and prevent these types of flaws before attackers do. Researchers are continually finding new, **extremely high-risk attacks** that affect Active Directory environments, that often require no more than a standard domain user to obtain complete administrative control over the entire domain.

There are many great open-source tools for penetration testers to enumerate and attack Active Directory. Still, to use these most effectively, we must understand how Active Directory works to identify obvious and nuanced flaws. **Tools are only as effective as their operator is knowledgeable**.

So let's take the time to understand the structure and function of Active Directory before moving into later modules that will focus on:

- In-depth manual and tool-based enumeration
- Attacks
- Lateral movement
- Post-exploitation
- Persistence

## History of Active Directory

LDAP, the foundation of Active Directory, was first introduced in RFCs as early as 1971. Active Directory was predated by the **X.500 organizational unit concept**, which was the earliest version of all directory systems created by **Novell and Lotus** and released in 1993 as **Novell Directory Services**.

Active Directory was first introduced in the mid-'90s but did not become part of the Windows operating system until the release of **Windows Server 2000**. Microsoft first attempted to provide directory services in 1990 with the release of **Windows NT 3.0**. This operating system combined features of the **LAN Manager** protocol and the **OS/2** operating systems, which Microsoft created initially along with IBM, led by **Ed Iacobucci**, who also led the design of **IBM DOS** and later co-founded **Citrix Systems**.

The NT operating system evolved throughout the 90s, adapting protocols such as **LDAP** and **Kerberos** with Microsoft's proprietary elements. The first beta release of Active Directory was in **1997**.

### Major Milestones

- **Windows Server 2003**: Introduced the **Forest** feature, allowing sysadmins to create "containers" of separate domains, users, computers, and other objects all under the same umbrella.
- **Windows Server 2008**: Introduced **Active Directory Federation Services (ADFS)** to provide **Single Sign-On (SSO)** for users on Windows Server operating systems.
  - ADFS uses the **claims-based Access Control Authorization** model.
- **Windows Server 2016**: Introduced the ability to **migrate AD environments to the cloud** and added security enhancements such as:
  - **User access monitoring**
  - **Group Managed Service Accounts (gMSA)** — a mitigation against **Kerberoasting** attacks.
- **Azure AD Connect**: Released to enable **SSO for Office 365** environments and support hybrid cloud adoption.

## Importance of Active Directory Security

Active Directory has suffered from various **misconfigurations** from 2000 to the present day. New vulnerabilities are discovered regularly that affect AD and technologies that interface with it (e.g., Microsoft Exchange).

As penetration testers, we are tasked with finding these flaws for our clients before attackers do.

We must have a solid foundation in:

- Active Directory fundamentals
- AD structure and function
- Protocols used by AD
- User rights and privilege management
- Admin tools and practices
- Vulnerabilities and misconfigurations

Managing AD is no easy task — one fix can introduce issues elsewhere.

## Conclusion

As said before, **95% of Fortune 500 companies run Active Directory**, and Microsoft has a near-complete monopoly in the directory services space.

Even though many companies are transitioning to cloud and hybrid environments, **on-prem AD is not going away** for many organizations.

If you are performing **network penetration testing engagements**, you can be nearly sure to encounter AD in some form on almost all of them.

This fundamental knowledge will make us **better attackers and defenders** and give us insight into AD that will be extremely useful when providing **remediation advice** to clients.

A **deep understanding** of AD will make even large and complex environments feel manageable — whether you're dealing with **10,000 hosts** or just **20**.

