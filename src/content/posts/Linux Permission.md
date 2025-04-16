---
title: Linux Permission
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Linux
draft: false
---

This is a great overview of permission management in Linux, especially when it comes to understanding how access is granted to files and directories and the special permission bits that can be applied. To summarize and clarify the key points:

### File and Directory Permissions:
In Linux, permissions control the actions that users can perform on files and directories. The permissions are divided into three categories:
- **Read (r)**: Permission to view the contents of the file or list the contents of the directory.
- **Write (w)**: Permission to modify the contents of the file or add/delete files in the directory.
- **Execute (x)**: Permission to run a file as a program or to traverse into a directory.

The permissions are represented for:
- **Owner**: The user who owns the file.
- **Group**: Users who belong to the group associated with the file.
- **Others**: All other users on the system.

The permission format is displayed as a string of 10 characters:
- The first character indicates the file type (`d` for directory, `-` for regular file, `l` for symbolic link, etc.).
- The next three characters represent the owner's permissions.
- The following three represent the group's permissions.
- The last three characters represent the permissions for others.

For example:
```bash
-rwxr-xr-- 1 cry0l1t3 htbteam 0 May 4 22:12 shell
```
This means:
- **Owner (cry0l1t3)** has **read (r)**, **write (w)**, and **execute (x)** permissions.
- **Group (htbteam)** has **read (r)** and **execute (x)** permissions.
- **Others** have **read (r)** permissions only.

### Changing Permissions with `chmod`:
The `chmod` command is used to change file permissions. Permissions can be added (`+`), removed (`-`), or set explicitly (`=`) for the owner, group, and others. You can use either symbolic notation (e.g., `r`, `w`, `x`) or octal notation (e.g., `755`).

Example:
```bash
chmod a+r shell      # Add read permission for all users
chmod 754 shell      # Set permissions: Owner: rwx, Group: rx, Others: r
```

### Octal Representation:
Permissions are calculated in octal values (base 8), where:
- `r = 4`
- `w = 2`
- `x = 1`

These are summed up for each user category:
- **Owner**: `rwx = 4+2+1 = 7`
- **Group**: `rw- = 4+2 = 6`
- **Others**: `r-- = 4`

Thus, `rwxr-xr--` corresponds to the octal value `754`.

### Changing Ownership with `chown`:
The `chown` command allows you to change the owner and/or the group of a file or directory:
```bash
chown user:group file
```

Example:
```bash
chown root:root shell  # Change the owner to root and the group to root
```

### Special Permissions:
Linux also supports special permissions, which give more control over how files and directories are accessed and executed.

#### SUID (Set User ID):
When the SUID bit is set on an executable file, it runs with the permissions of the file's owner, rather than the user who executes it. This is indicated by an `s` in the execute position for the owner.

Example:
```bash
-rwsr-xr-x 1 root root 12345 /usr/bin/someprogram
```

#### SGID (Set Group ID):
When the SGID bit is set, the file or directory runs with the permissions of the file's group, instead of the user's group. For directories, files created within will inherit the group of the directory, not the user's current group. This is indicated by an `s` in the execute position for the group.

Example:
```bash
-rwxr-sr-x 1 root staff 12345 /usr/bin/someprogram
```

#### Sticky Bit:
The sticky bit is primarily used on directories. When set, only the owner of a file can delete or rename it within the directory, even if others have write access. This is indicated by a lowercase `t` in the execute position for others.

Example:
```bash
drwxrwxrwt 2 root root 4096 Jan 12 12:30 /tmp
```
If the sticky bit is set but the directory lacks execute permissions for others, it’s represented by an uppercase `T`.

#### SUID, SGID, and Sticky Bit Risks:
While these special permissions can be useful for specific tasks, they can also pose security risks if misused. For instance, the SUID bit on a program like `journalctl` could allow unauthorized users to execute a shell as root, which is a significant security vulnerability.

### Summary:
Linux permissions are essential for controlling access to files and directories. By using commands like `chmod`, `chown`, and `ls`, users can manage who has access to what resources and modify the access rights as needed. Special permissions like SUID, SGID, and the sticky bit allow for more complex permission handling, but they must be used carefully to avoid introducing security risks.

Let me know if you'd like more details or if you'd like to dive into specific scenarios!