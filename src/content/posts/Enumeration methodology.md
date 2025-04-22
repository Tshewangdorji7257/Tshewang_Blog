---
title: Enumeration Methodology
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Footprinting
draft: false
---

# Enumeration Methodology - Simplified Notes

## Why Methodology Matters

- Enumeration is a **dynamic** process, but a **static, layered methodology** helps ensure thoroughness.
- Avoids skipping critical steps and adapts to various environments.
- Not a strict checklist — it's a flexible structure for approaching enumeration systematically.

---

## Enumeration Levels

1. **Infrastructure-Based Enumeration**
2. **Host-Based Enumeration**
3. **OS-Based Enumeration**

---

## Metaphor: Walls in a Labyrinth

Each layer is like a wall — instead of smashing through, we look for gaps, entrances, or ways around.  
The goal is to **navigate efficiently** through the system's defenses.

---

## The 6 Enumeration Layers

| Layer | Description | Key Information |
|-------|-------------|-----------------|
| **1. Internet Presence** | Identify external presence and infrastructure | Domains, Subdomains, IPs, ASN, Netblocks, vHosts, Cloud instances |
| **2. Gateway** | Identify external/internal protective measures | Firewalls, DMZ, IDS/IPS, EDR, VPN, Cloudflare, NAC, Proxies |
| **3. Accessible Services** | Identify exposed/internal services and interfaces | Ports, Service type, Version, Configuration, Interface |
| **4. Processes** | Understand internal system processes | Process IDs, Tasks, Source/Destination, Data processed |
| **5. Privileges** | Identify permissions and privileges on services | Users, Groups, Roles, Restrictions, Environment |
| **6. OS Setup** | Explore internal system configuration | OS type, Patch level, Network setup, Config & sensitive files |

> Note: Layers 1 & 2 are mainly relevant for **external** infrastructure (e.g., public internet).  
> Internal infrastructure like Active Directory will be covered elsewhere.

---

## Enumeration Mindset

- Every service exists for a **reason** — understand that reason.
- Think about **functionality** and how to interact or exploit it.
- Just because you find a gap doesn't mean it leads somewhere useful.
- Time is limited in tests — efficiency is key.
- There's **almost always a way in** — but we may not find it within the test window.

---

## Example: External Black Box Pentest

1. **Start with Layer 1: Internet Presence**
   - Map domains, subdomains, IP ranges, cloud assets.
2. **Proceed to Layer 2: Gateway**
   - Identify protections (firewalls, VPNs, proxies).
3. **Move to Layer 3: Accessible Services**
   - Scan for open ports, detect service versions.
4. **Layer 4-6**
   - Dive deeper internally (requires access or exploit paths).

---

## Important Considerations

- Enumeration methodology ≠ toolset.
- Tools are **supporting resources** (like a cheat sheet).
- The methodology is **how** we think and approach each situation systematically.
- OSINT from humans/employees is excluded from Layer 1 for simplicity.

---

## Summary

- Use methodology to **structure** your approach.
- Be flexible and adaptive — it's not about following steps blindly.
- Keep the goal in mind: **Understand and map the environment thoroughly**.

