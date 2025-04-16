---
title: Saving the Results
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Nmap
draft: false
---

# Nmap Output Formats

Nmap allows saving scan results in different formats for later analysis.

## Saving Results

Use `-oA` to save in all formats at once:
```bash
sudo nmap 10.129.2.28 -p- -oA target
```

This creates three files:
- `target.nmap` (Normal output)
- `target.gnmap` (Grepable output)
- `target.xml` (XML output)

## Format Details

### 1. Normal Output (`-oN`)
- File extension: `.nmap`
- Human-readable format
- Shows:
  - Scan metadata (time, command)
  - Host status
  - Open ports with services
  - Scan summary

### 2. Grepable Output (`-oG`)
- File extension: `.gnmap`
- Machine-parsable format
- Useful for scripting/automation
- Condenses information into single lines

### 3. XML Output (`-oX`)
- File extension: `.xml`
- Structured data format
- Can be converted to HTML reports:
  ```bash
  xsltproc target.xml -o target.html
  ```

## Key Options
- `-p-`: Scan all ports
- `-oA [name]`: Save in all formats with given filename prefix
- Without full path, files save to current directory

## Use Cases
- Normal: Quick human review
- Grepable: Scripting/automation
- XML: Reporting/documentation
