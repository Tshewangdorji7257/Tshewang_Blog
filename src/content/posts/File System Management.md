---
title: File System Management
published: 2025-04-16
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Linux
draft: false
---

### File System Types in Linux:
1. **ext2, ext3, ext4**:
   - **ext2**: An older file system without journaling, good for low-overhead scenarios.
   - **ext3**: Adds journaling for data integrity.
   - **ext4**: Default choice for most Linux systems, offering improved performance, reliability, and support for large files.
   
2. **Btrfs**:
   - Features like snapshotting, data integrity checks, and compression make it suitable for complex storage systems.
   
3. **XFS**:
   - High performance and good for large files and systems with high I/O demands.

4. **NTFS**:
   - Mainly used for compatibility with Windows systems.

### Inodes:
- Inodes store metadata (e.g., file permissions, size) but not the file content or name.
- The **inode table** acts like an index for managing files in Linux, ensuring efficient access to stored data.
- **Analogy**: Think of inodes as catalog cards in a library—each card gives detailed info about a book, but the card doesn’t contain the actual book.

### File Types:
1. **Regular Files**: Store data (text, images, executables).
2. **Directories**: Special files that contain other files or directories.
3. **Symbolic Links (Symlinks)**: Shortcuts to files or directories.

### Disk Management:
- **fdisk** and **gparted** are commonly used to manage partitions and disk space.
- Each partition can be formatted with a different file system.

### Mounting and Unmounting:
- **Mounting**: Linking a partition to a directory so it can be accessed. This is done using the `mount` command.
- **Unmounting**: Disconnecting a mounted partition. The `umount` command is used to safely unmount.
- To ensure drives are automatically mounted at boot, configure the `/etc/fstab` file.

### Swap Space:
- **Swap space** is used when the system runs out of RAM. It temporarily stores data that is not in active use.
- It can be created using the `mkswap` command and activated with `swapon`.
- Swap space is also critical for **hibernation**, saving the system's state to resume later.

