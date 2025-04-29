---
title: AD Terminology
published: 2025-04-29
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Active Directory
draft: false
---

# Active Directory Terminology

Before we go any further, let's take a step back and define some key terminology that will be used throughout this module and in general when dealing with Active Directory in any capacity.

---

## Object
An object can be defined as **ANY resource** present within an Active Directory environment such as OUs, printers, users, domain controllers, etc.

## Attributes
Every object in Active Directory has an associated set of attributes used to define characteristics of the given object. A computer object contains attributes such as the hostname and DNS name. All attributes in AD have an associated LDAP name that can be used when performing LDAP queries, such as `displayName` for Full Name and `givenName` for First Name.

## Schema
The Active Directory schema is essentially the blueprint of any enterprise environment. It defines what types of objects can exist in the AD database and their associated attributes.  
Example:
- Users belong to the class `user`
- Computers belong to the class `computer`

When an object is created from a class, it is called **instantiation**. The object is then an **instance** of that class.

## Domain
A domain is a logical group of objects such as computers, users, OUs, groups, etc. Domains can operate independently or be connected via **trust relationships**.

## Forest
A forest is a **collection of Active Directory domains**. It is the topmost container and can include:
- Domains
- Users
- Groups
- Computers
- Group Policy objects

## Tree
A tree is a collection of Active Directory domains that begins at a single root domain. Domains in a tree:
- Share a namespace
- Have a parent-child trust relationship

Example:
- Tree 1: `inlanefreight.local`
  - Child: `corp.inlanefreight.local`
- Tree 2: `ilfreight.local`
  - Child: `corp.ilfreight.local`

## Container
Container objects hold other objects and have a defined place in the directory subtree hierarchy.

## Leaf
Leaf objects do not contain other objects and are found at the end of the subtree hierarchy.

## Global Unique Identifier (GUID)
A **GUID** is a 128-bit unique identifier assigned when a domain object (e.g., user or group) is created. Stored in the `ObjectGUID` attribute.

- Never changes once assigned
- Unique across the enterprise
- Used in PowerShell or LDAP queries

## Security Principals
Security principals are entities that the OS can authenticate:
- Users
- Computer accounts
- Threads/processes

In AD, they manage access to domain resources. Local accounts are managed by **Security Accounts Manager (SAM)**.

## Security Identifier (SID)
A **SID** uniquely identifies a security principal or group. Issued by the Domain Controller.  
When a user logs in:
- An access token is generated
- Token includes: User's SID + SIDs of all groups they belong to

Well-known SIDs exist, e.g., `Everyone`.

## Distinguished Name (DN)
Describes the **full path** to an object in AD.  
Example:  
`cn=bjones, ou=IT, ou=Employees, dc=inlanefreight, dc=local`

## Relative Distinguished Name (RDN)
A **single component** of the Distinguished Name that identifies the object uniquely at its level.  
Example: `bjones` is the RDN in the DN above.

## sAMAccountName
User's logon name, must be:
- Unique
- ≤ 20 characters  
Example: `bjones`

## userPrincipalName (UPN)
An alternative identifier for users. Format:  
`[user]@[domain]`  
Example: `bjones@inlanefreight.local`  
This attribute is **optional**.

## FSMO Roles
To prevent replication conflicts, Microsoft introduced **Flexible Single Master Operations (FSMO)** roles:

- **Schema Master** *(1 per forest)*
- **Domain Naming Master** *(1 per forest)*
- **RID Master** *(1 per domain)*
- **PDC Emulator** *(1 per domain)*
- **Infrastructure Master** *(1 per domain)*

These roles are set when DCs are created but can be transferred.

## Global Catalog (GC)
A **domain controller feature** that stores:
- Full copy of current domain objects
- Partial copy of objects from other domains

Functions:
- Authentication (for access tokens)
- Object search across all domains

## Read-Only Domain Controller (RODC)
An RODC contains:
- Read-only AD database
- Read-only DNS
- No password caching (except its own)
- Reduced replication traffic
- Administrator role separation

## Replication
Replication occurs when AD objects are updated and synchronized across DCs. Managed by:
- **Knowledge Consistency Checker (KCC)**

Ensures fault tolerance.

## Service Principal Name (SPN)
Used in **Kerberos authentication** to associate a service instance with a logon account.  
Allows clients to authenticate to services without knowing the account name.

## Group Policy Object (GPO)
Virtual collection of policy settings. Each GPO:
- Has a unique GUID
- Can contain AD or local file system settings
- Applies to users or computers (domain-wide or at the OU level)

## Access Control List (ACL)
Ordered collection of **Access Control Entries (ACEs)** that apply to an object.

## Access Control Entry (ACE)
Specifies:
- A trustee (user, group, session)
- Access rights (allow, deny, audit)

## Discretionary Access Control List (DACL)
Defines which security principals are allowed or denied access.  
If:
- No DACL exists → full access to everyone
- Empty DACL → no access to anyone

ACEs are evaluated in sequence.

## System Access Control List (SACL)
Specifies which access attempts are **logged** in the security event log.

## Fully Qualified Domain Name (FQDN)
Complete name for a computer or host. Format:  
`[host].[domain].[tld]`  
Example:  
`DC01.INLANEFREIGHT.LOCAL`

## Tombstone
A **deleted object placeholder** in AD.  
Attributes:
- Marked with `isDeleted = TRUE`
- Stored in "Deleted Objects" container
- Retained for the **Tombstone Lifetime** (default: 60–180 days)

Once expired, the object is permanently removed.

## AD Recycle Bin
Introduced in **Windows Server 2008 R2**, allows:
- Easy recovery of deleted AD objects
- Retains most attributes

Default retention period: 60 days  
Must be **enabled** to use.

## SYSVOL
A shared folder on each DC containing:
- Group Policy settings
- Scripts (logon/logoff)
- Public domain files

Replicated using **File Replication Services (FRS)**.

## AdminSDHolder
Used to manage ACLs for **privileged AD groups**.  
Works with:
- **SDProp (Security Descriptor Propagator)**  
- SDProp runs on the **PDC Emulator**, periodically resetting ACLs on protected accounts to match AdminSDHolder.

