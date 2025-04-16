---
title: Navigation
published: 2025-04-16
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Linux
draft: false
---
# Linux Navigation Basics

## Finding Your Location

- Use `pwd` to see your current directory location:

  ```bash
  pwd
  ```

  Example Output:
  ```bash
  /home/username
  ```

## Listing Directory Contents

- **Basic listing**: `ls`

  ```bash
  ls
  ```

- **Detailed listing**: `ls -l`

  ```bash
  ls -l
  ```

- **Show hidden files**: `ls -la`

  ```bash
  ls -la
  ```

- **List specific directory**: `ls -l /path/to/directory`

  ```bash
  ls -l /path/to/directory
  ```

## Understanding Directory Listings

When using `ls -l`, you will see the following information:

- **Permissions** (e.g., `drwxr-xr-x`)
- **Number of links**
- **Owner and group**
- **File size**
- **Last modified date/time**
- **Name**

## Moving Between Directories

- **Change directory**: `cd /path/to/directory`

  ```bash
  cd /path/to/directory
  ```

- **Go to the previous directory**: `cd -`

  ```bash
  cd -
  ```

- **Go up one directory**: `cd ..`

  ```bash
  cd ..
  ```

## Helpful Tips

- Use the `TAB` key twice to see available options when typing paths.
- In directory listings:
  - `.` means current directory.
  - `..` means parent directory.
- Clean terminal: `clear` or `Ctrl+L`.
- Browse command history: Up/Down arrow keys.
- Search command history: `Ctrl+R`.
