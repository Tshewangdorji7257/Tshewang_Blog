---
title: Auth LDAP Kerberos
published: 2025-04-29
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Active Directory
draft: false
---

## **Kerberos**
- **Purpose**: Default authentication protocol in AD since Windows 2000.
- **Key Concept**: Uses **tickets** (TGT, TGS) instead of transmitting passwords.
- **Process Overview**:
  1. User logs in → sends an encrypted timestamp to **KDC**.
  2. KDC verifies and issues a **TGT**.
  3. TGT is presented to request a **TGS** for accessing specific services.
  4. TGS is encrypted with the **service account’s NTLM hash**.
  5. Final access request is made using the TGS.
- **Ports**: TCP/UDP **88**
- **Security**: Stateless; password never transmitted over the network.

---

## **DNS**
- **Purpose**: Resolves domain names to IPs and helps clients locate **Domain Controllers (DCs)** using **SRV records**.
- **Key Features**:
  - Uses **Dynamic DNS (DDNS)** for automatic updates.
  - Supports both **forward** and **reverse** lookups via `nslookup`.
- **Ports**: UDP **53** (default), TCP **53** (for large messages).
- **Example**:
  - `nslookup INLANEFREIGHT.LOCAL` → Retrieves DC IP.
  - `nslookup 172.16.6.5` → Gets FQDN.

---

## **LDAP (Lightweight Directory Access Protocol)**
- **Purpose**: Used by AD to handle **directory lookups** and **authentication**.
- **Ports**:
  - **389** for plain LDAP.
  - **636** for LDAPS (encrypted).
- **Authentication Methods**:
  1. **Simple**: Username/password (in cleartext by default).
  2. **SASL**: Can use **Kerberos** or other services for secure authentication.
- **Security Note**: LDAP traffic should be encrypted to prevent sniffing.

---

## **MSRPC (Microsoft RPC)**
- **Purpose**: Interprocess communication for accessing AD functions remotely.
- **Key Interfaces**:
  - **lsarpc**: Interacts with Local Security Authority (LSA).
  - **netlogon**: Handles domain logins.
  - **samr**: Manages user and group info. Vulnerable to enumeration.
  - **drsuapi**: Handles directory replication; can be abused to extract the **NTDS.dit** file.

---

## Attacker/Defender Notes
- **Port Scans** (e.g., Nmap) can reveal open Kerberos and DNS ports to identify DCs.
- **LDAP & samr** interfaces are commonly used in enumeration tools (like **BloodHound**).
- **drsuapi** exploitation can lead to full domain compromise.

