---
title: Oracle TNS
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

This provides a thorough overview of Oracle TNS (Transparent Network Substrate), its configuration, usage, and its role in Oracle database communication. Oracle TNS enables client applications to connect to Oracle databases, often used with Oracle Net Services for efficient network communication.

Key points of the content:

### Overview of Oracle TNS:
- **TNS Protocol**: It supports network protocols like TCP/IP and others, providing flexibility for database communication. It ensures encryption and secure data transfer between clients and servers.
- **Security Features**: Built-in encryption (SSL/TLS) ensures secure database communication, reducing vulnerabilities from unauthorized access or attacks.
- **TNS Files**: Configuration files like `tnsnames.ora` (client-side) and `listener.ora` (server-side) define the database connections and listener behavior.

### Default Configuration:
- **Listener Port**: The Oracle TNS listener typically listens on TCP/1521, but it can be reconfigured.
- **Authentication**: Basic authentication is performed using hostnames, IP addresses, and user credentials.
- **Network Protocols Supported**: Includes TCP/IP, UDP, IPX/SPX, and AppleTalk, with flexible configurations allowing multiple network interfaces.

### Common Tools:
1. **ODAT (Oracle Database Attacking Tool)**: A Python tool for penetration testing Oracle databases, which helps enumerate vulnerabilities, misconfigurations, and services.
2. **Nmap**: A popular tool to scan for open ports and services. It can be used to identify Oracle TNS listeners and attempt SID brute forcing.

### Example Workflow:
1. **Enumerating Oracle TNS Listener**:
   - Using tools like Nmap and ODAT to detect open ports and gather information on Oracle database services.
   - Nmap can brute-force SIDs with the `oracle-sid-brute` script, while ODAT offers more advanced enumeration techniques.
2. **Connecting to the Database**:
   - Tools like SQLPlus can be used to interact with the Oracle database once valid credentials are found.
   - Common tasks include retrieving user roles, checking privileges, and attempting privileged access as `sysdba`.

3. **Extracting Password Hashes**:
   - Extract password hashes from system tables (e.g., `sys.user$`) to attempt offline cracking.
   - This is a common step for escalating privileges or further penetration testing.

### Sample Commands:
1. **Nmap Scan**:
   ```bash
   sudo nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute
   ```
   - Scans for Oracle TNS listener and attempts SID brute forcing.

2. **ODAT Command**:
   ```bash
   ./odat.py all -s 10.129.204.235
   ```
   - Runs all available modules of ODAT to gather information on the Oracle database.

3. **SQLPlus**:
   ```bash
   sqlplus scott/tiger@10.129.204.235/XE
   ```
   - Connects to the Oracle database using found credentials.

4. **Extracting Password Hashes**:
   ```sql
   select name, password from sys.user$;
   ```

### Conclusion:
The document effectively walks through various aspects of interacting with Oracle TNS, from initial configuration and enumeration using tools like Nmap and ODAT, to connecting to the database and extracting sensitive data. The example commands and configurations provided offer a detailed guide for penetration testing and Oracle database administration tasks.

