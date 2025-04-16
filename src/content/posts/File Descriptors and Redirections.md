---
title: File Descriptors and Redirections
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Linux
draft: false
---
Understanding **file descriptors** and **redirections** in Linux is essential for effective command-line usage, as it allows us to control how input and output are handled. Let's go over the key concepts in detail:

### 1. **File Descriptors (FD)**
File descriptors are integer references maintained by the kernel that track open files or resources. The first three file descriptors are predefined:
- **STDIN (0)**: Standard Input - used for input operations.
- **STDOUT (1)**: Standard Output - used for output operations.
- **STDERR (2)**: Standard Error - used for error messages.

These file descriptors allow programs to interact with files or streams. For example, when you run a program, the system knows where to send output, errors, or where to get input based on these file descriptors.

### 2. **STDIN, STDOUT, and STDERR Examples**

#### STDIN (Input)
The `cat` command, when used with input, reads from STDIN:
```bash
cat
SOME INPUT
```
Here, `cat` reads the input from STDIN and outputs it to STDOUT.

#### STDOUT and STDERR (Output and Errors)
When using the `find` command, you can see both STDOUT and STDERR:
```bash
find /etc/ -name shadow
```
- **STDOUT**: Files that match the search criteria.
- **STDERR**: Error messages, such as "Permission denied."

You can suppress the error messages by redirecting STDERR to `/dev/null`, which discards the errors:
```bash
find /etc/ -name shadow 2>/dev/null
```

### 3. **Redirection Examples**

#### Redirect STDOUT to a File
You can redirect standard output (STDOUT) to a file:
```bash
find /etc/ -name shadow 2>/dev/null > results.txt
```
This redirects the results to `results.txt` and suppresses any errors.

#### Redirect STDOUT and STDERR to Separate Files
You can redirect both STDOUT and STDERR to different files:
```bash
find /etc/ -name shadow 2> stderr.txt 1> stdout.txt
```
Here:
- STDERR is redirected to `stderr.txt`.
- STDOUT is redirected to `stdout.txt`.

#### Redirect STDIN from a File
You can use the `<` symbol to redirect a file to be used as input (STDIN) by a command:
```bash
cat < stdout.txt
```
This reads from `stdout.txt` as if it were standard input.

#### Append STDOUT to an Existing File
To append STDOUT to an existing file without overwriting it, use `>>`:
```bash
find /etc/ -name passwd >> stdout.txt 2>/dev/null
```
This appends the output of the `find` command to `stdout.txt` and suppresses errors.

#### Redirect STDIN Stream to a File
You can use `<<` to take multiple lines of input and redirect it to a file:
```bash
cat << EOF > stream.txt
This is the input
that will be saved
in the stream.txt file.
EOF
```
This will create a `stream.txt` file with the input provided between `EOF` markers.

### 4. **Pipes (`|`)**

Pipes allow you to take the STDOUT of one command and use it as input (STDIN) for another command. This is useful for chaining commands together.

#### Example: Filtering with `grep`
You can use `grep` to filter output:
```bash
find /etc/ -name *.conf 2>/dev/null | grep systemd
```
This command finds all `.conf` files and then filters the results for those containing the pattern "systemd".

#### Example: Counting Results with `wc`
You can count the number of results using `wc -l`:
```bash
find /etc/ -name *.conf 2>/dev/null | grep systemd | wc -l
```
This counts the number of `.conf` files related to `systemd` in the `/etc/` directory.

### 5. **Summary of Redirection Symbols**
- `>`: Redirects STDOUT to a file, overwriting it.
- `>>`: Appends STDOUT to a file.
- `<`: Redirects a file to be used as STDIN.
- `2>`: Redirects STDERR to a file.
- `2>/dev/null`: Discards STDERR.
- `<<`: Used for taking multiline input and redirecting it to a file.
- `|`: Pipes STDOUT of one command to the input of another.

### Conclusion
Understanding file descriptors and redirections helps you control how data flows between commands, files, and processes. By utilizing redirections, you can suppress errors, filter outputs, and structure your commands in a more efficient and organized manner. Mastering these concepts significantly enhances your command-line productivity in Linux environments.