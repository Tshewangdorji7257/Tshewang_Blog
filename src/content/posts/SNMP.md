---
title: SNMP
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

## **What is SNMP?**
SNMP is a protocol used to **monitor and manage network devices** such as routers, switches, servers, and IoT devices.

- **Functions**:
  - Monitor device status
  - Configure devices remotely
  - Receive alerts (traps)

---

## **Key SNMP Components**

### **Versions**
- **SNMPv1**: Basic, no encryption or authentication
- **SNMPv2c**: Adds some improvements, still no encryption
- **SNMPv3**: Supports **authentication + encryption** via username/password and pre-shared keys

### **Community Strings**
- Work like passwords (e.g., `public` for read-only)
- Still widely used, even though insecure if not encrypted

### **MIB (Management Information Base)**
- Text files describing available data points (OIDs) in a **tree structure**
- Written in ASN.1 format
- Enable **cross-vendor compatibility**

### **OID (Object Identifier)**
- Uniquely identifies SNMP data (like `.1.3.6.1.2.1.1.5.0` for system name)
- Represented in dot notation

---

## **SNMP Daemon Configuration (Example)**
```bash
cat /etc/snmp/snmpd.conf | grep -v "#" | sed -r '/^\s*$/d'
```

### Sample config values:
- `agentaddress`: Interface SNMP listens on
- `rocommunity public`: Read-only access with community string `public`
- `view systemonly`: Restrict viewable OIDs
- `rouser authPrivUser authpriv`: SNMPv3 user with encrypted/authenticated access

---

## **Dangerous Configurations**
| Setting                | Risk                                                              |
|------------------------|-------------------------------------------------------------------|
| `rwuser noauth`        | Full access with no auth                                          |
| `rwcommunity public`   | Full access from any IP                                           |
| `rwcommunity6 public`  | Same as above, for IPv6                                           |

---

## **Footprinting SNMP**

### **`snmpwalk`**
- Queries a device for all available info using a community string

```bash
snmpwalk -v2c -c public 10.129.14.128
```

- Useful for:
  - Discovering hostnames, OS versions
  - Enumerating installed software
  - Grabbing interface info, services, etc.

### Other Tools
- **onesixtyone**: Brute-force SNMP community strings
- **braa**: Fast bulk SNMP scanning

---

## **From Your snmpwalk Output (Highlights)**

- Hostname: `htb`
- Location: `"Sitting on the Dock of the Bay"`
- Contact: `mrb3n@inlanefreight.htb`
- Installed packages: `printer-driver-*`
- Boot image path: Includes Linux kernel `5.11.0-34-generic`

These details are often critical in a pentesting context for:
- OS fingerprinting
- Identifying software vulnerabilities
- Lateral movement or privilege escalation

