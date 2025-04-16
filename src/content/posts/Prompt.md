---
title: Prompt Stucture
published: 2025-04-16
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Linux
draft: false
---
# Bash Prompt Notes

## Basic Prompt Structure

The bash prompt displays essential information like username, hostname, and current directory. Default format:

- Home directory is marked with a tilde `~`
- `$` indicates a regular user
- `#` indicates root user

### Examples:
- Regular user: `username@hostname[~]$`
- Root user: `root@htb[/htb]#`
- Basic unprivileged shell: `$`
- Basic privileged shell: `#`

---

## PS1 Variable

The `PS1` variable controls how your command prompt appears. It can be customized to show:

- Basic information (username, hostname, current directory)
- System details (IP address, date, time)
- Status of previous commands
- Colors and special characters

---

## Special Characters for Customization

| Character      | Description                          |
|----------------|--------------------------------------|
| `\d`           | Date (Mon Feb 6)                     |
| `\D{%Y-%m-%d}` | Date (YYYY-MM-DD)                    |
| `\H`           | Full hostname                        |
| `\j`           | Number of jobs managed by the shell  |
| `\n`           | Newline                              |
| `\r`           | Carriage return                      |
| `\s`           | Name of the shell                    |
| `\t`           | Current time 24-hour (HH:MM)         |
| `\T`           | Current time 12-hour (HH:MM)         |
| `@`            | Current time                         |
| `\u`           | Current username                     |
| `\w`           | Full path of current working directory |

---

## Benefits of Customization

- Makes terminal experience more personalized and efficient  
- Helps with troubleshooting and problem-solving  
- Provides important system state information  
- Particularly useful during penetration tests for tracking actions  

---

## Further Customization Options

- Different color schemes  
- Custom fonts  
- Other visual settings  
- Tools like `bash-prompt-generator` and `powerline`  
