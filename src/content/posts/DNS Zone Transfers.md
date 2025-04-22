---
title: DNS Zone Transfers
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

# DNS Zone Transfers

While brute-forcing subdomains can be effective, there's a less invasive and potentially more efficient method: **DNS zone transfers**. This mechanism, intended for replicating DNS records between name servers, can reveal sensitive information if misconfigured.

---

## What is a Zone Transfer?

A **DNS zone transfer** is a process where all DNS records within a domain's zone (including subdomains) are copied from a **primary** name server to a **secondary** name server. It ensures consistency and redundancy in DNS data across servers.

If not properly secured, an unauthorized user can initiate a zone transfer and download the **entire zone file**, exposing:

- All subdomains
- IP addresses
- Mail server details
- Name server configurations

---

### Zone Transfer Process (AXFR)

1. **AXFR Request**  
   The secondary DNS server sends a zone transfer request (AXFR) to the primary server.

2. **SOA Record Transfer**  
   The primary server responds with the **Start of Authority (SOA)** record, which includes key metadata like the zone's serial number.

3. **DNS Records Transmission**  
   The primary server then sends all DNS records in the zone (`A`, `AAAA`, `MX`, `CNAME`, `NS`, etc.).

4. **Zone Transfer Complete**  
   After all records are sent, the primary server signals completion.

5. **Acknowledgement (ACK)**  
   The secondary server confirms successful receipt of the zone data.

---

## The Zone Transfer Vulnerability

In the past, DNS servers were often configured to allow zone transfers from **any client**, making administration easy but leaving a major security hole. Today, while most servers restrict transfers to trusted sources, **misconfigurations still occur**.

### What Attackers Can Learn:
- **Subdomains**: Often hidden from the main website, possibly revealing development or admin environments.
- **IP Addresses**: Direct targets for scanning or exploitation.
- **NS Records**: May disclose hosting providers or misconfigurations.

---

## Remediation

To prevent unauthorized zone transfers:
- **Restrict AXFR access** to trusted secondary servers only.
- **Audit DNS configurations** regularly.
- **Use DNSSEC and firewalls** to further protect DNS infrastructure.

Despite modern protections, it's still valuable to attempt a zone transfer (with authorization) to assess DNS security posture.

---

## Exploiting Zone Transfers

You can use the `dig` command to attempt a zone transfer:

```bash
dig axfr @nsztm1.digi.ninja zonetransfer.me
```

### Example Output (truncated):

```bash
; <<>> DiG 9.18.12 <<>> axfr @nsztm1.digi.ninja zonetransfer.me
...
zonetransfer.me. 7200 IN A 5.196.105.14
zonetransfer.me. 7200 IN NS nsztm1.digi.ninja.
_acme-challenge.zonetransfer.me. 301 IN TXT "token"
canberra-office.zonetransfer.me. 7200 IN A 202.14.81.230
...
```

> **Note**: `zonetransfer.me` is a test domain provided by [Robin Wood (DigiNinja)](https://www.digininja.org) to safely demonstrate the risks of zone transfers.

---

## Summary

DNS zone transfers can be a powerful reconnaissance method when misconfigured. Always verify your DNS security settings and restrict AXFR access to prevent leakage of sensitive DNS data.
