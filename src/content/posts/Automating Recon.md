---
title: Automating Recon
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---


###  **Why Automate Reconnaissance?**
- **Efficiency:** Fast execution of repetitive tasks.
- **Scalability:** Recon over many domains or targets.
- **Consistency:** Reduces human error; same logic every time.
- **Comprehensive Coverage:** DNS, subdomains, ports, crawling, etc.
- **Integration:** Can be used with other tools in a pipeline.

---

###  **Popular Recon Frameworks**
| Tool         | Purpose |
|--------------|---------|
| **FinalRecon** | All-in-one tool for headers, Whois, SSL, crawling, DNS, subdomains, dirs, Wayback |
| **Recon-ng**  | Modular Python framework; supports scanning, crawling, exploitation |
| **theHarvester** | Gathers OSINT (emails, domains, hosts, ports) |
| **SpiderFoot** | Collects OSINT from IPs, domains, emails, social profiles |
| **OSINT Framework** | Curated list of tools for gathering intelligence |

---

###  **FinalRecon Modules**
| Command | Description |
|---------|-------------|
| `--url` | Target URL |
| `--headers` | Grab HTTP headers |
| `--whois` | WHOIS info |
| `--sslinfo` | SSL cert details |
| `--crawl` | Crawl website (HTML, JS, links) |
| `--dns` | Enumerate DNS records |
| `--sub` | Subdomain discovery |
| `--dir` | Directory brute-force |
| `--wayback` | Pull historical URLs |
| `--ps` | Fast port scan |
| `--full` | Run full recon |

---

###  **Installation Steps**
```bash
git clone https://github.com/thewhiteh4t/FinalRecon.git
cd FinalRecon
pip3 install -r requirements.txt
chmod +x ./finalrecon.py
./finalrecon.py --help
```

---

###  **Sample Command**
Gather headers and WHOIS for a target:
```bash
./finalrecon.py --headers --whois --url http://inlanefreight.com
```

---

###  **Example Output Highlights**
- **Headers:**
  - Server: Apache/2.4.41 (Ubuntu)
  - Content-Type: text/html; charset=UTF-8
- **Whois Info:**
  - Registrar: Amazon Registrar, Inc.
  - Created: 2019-08-05
  - Expires: 2024-08-05
  - Status: clientTransferProhibited, clientUpdateProhibited
