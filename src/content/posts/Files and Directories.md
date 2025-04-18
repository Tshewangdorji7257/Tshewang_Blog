---
title: Files and Directories
published: 2025-04-16
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Linux
draft: false
---

# Working with Files and Directories

The primary difference between working with files in Linux, as opposed to Windows, lies in how we access and manage those files. In Windows, we typically use graphical tools like Explorer to find, open, and edit files. However, in Linux, the terminal offers a powerful alternative where files can be accessed and edited directly using commands. This method is not only faster, but also more efficient, as it allows you to edit files interactively without even needing editors like vim or nano.

The terminal's efficiency stems from its ability to access files with just a few commands, and it allows you to modify files selectively using regular expressions (regex). Additionally, you can run multiple commands at once, redirecting output to files and automating batch editing tasks, which is a major time-saver when working with numerous files simultaneously. This command-line approach streamlines workflow, making it an invaluable tool for tasks that would be more time-consuming through a graphical interface.

Next, we will explore working with files and directories to effectively manage the content on our operating system.

## Create, Move, and Copy

Let us begin by learning how to perform key operations like creating, renaming, moving, copying, and deleting files. Before we execute the following commands, we first need to SSH into the target (using the connection instructions at the bottom of the section).

### Syntax - `touch`

To create an empty file:

```bash
K4y0x13@htb[/htb]$ touch <name>
```

### Syntax - `mkdir`

To create a directory:

```bash
K4y0x13@htb[/htb]$ mkdir <name>
```

In the next example, we will create a file called `info.txt` and a directory called `Storage`. To create these, we follow the commands and their syntax as shown above.

### Create an Empty File

```bash
K4y0x13@htb[/htb]$ touch info.txt
```

### Create a Directory

```bash
K4y0x13@htb[/htb]$ mkdir Storage
```

When organizing your system, you may need to create multiple directories within other directories. Manually running the `mkdir` command for each one would be time-consuming. Fortunately, the `mkdir` command has the `-p` (parents) option, which allows you to create parent directories automatically.

```bash
K4y0x13@htb[/htb]$ mkdir -p Storage/local/user/documents
```

We can look at the whole structure after creating the parent directories with the `tree` tool.

```bash
K4y0x13@htb[/htb]$ tree .
```

Example output:

```
.
├── info.txt
└── Storage
    ├── local
    └── user
        └── documents
```

You can create files directly within specific directories by specifying the path where the file should be stored, and you can use the single dot (`.`) to indicate that you want to start from the current directory. This is a convenient way to work within your current location, without needing to type the full path.

### Create `userinfo.txt`

```bash
K4y0x13@htb[/htb]$ touch ./Storage/local/user/userinfo.txt
```

We can check the updated structure again using the `tree` command:

```bash
K4y0x13@htb[/htb]$ tree .
```

Example output:

```
.
├── info.txt
└── Storage
    ├── local
    └── user
        ├── documents
        └── userinfo.txt
```

### Moving and Renaming Files

With the command `mv`, we can move and also rename files and directories. The syntax for this looks like this:

### Syntax - `mv`

```bash
K4y0x13@htb[/htb]$ mv <file/directory> <renamed file/directory>
```

First, let us rename the file `info.txt` to `information.txt` and then move it to the directory `Storage`.

### Rename File

```bash
K4y0x13@htb[/htb]$ mv info.txt information.txt
```

Now, let us create a file named `readme.txt` in the current directory and then copy the files `information.txt` and `readme.txt` into the `Storage/` directory.

### Create `readme.txt`

```bash
K4y0x13@htb[/htb]$ touch readme.txt
```

### Move Files to Specific Directory

```bash
K4y0x13@htb[/htb]$ mv information.txt readme.txt Storage/
```

Check the directory structure using `tree`:

```bash
K4y0x13@htb[/htb]$ tree .
```

Example output:

```
.
└── Storage
    ├── information.txt
    ├── local
    │   └── user
    │       ├── documents
    │       └── userinfo.txt
    └── readme.txt
```

Let us assume we want to have the `readme.txt` in the `local/` directory. Then we can copy them there with the paths specified.

### Copy `readme.txt`

```bash
K4y0x13@htb[/htb]$ cp Storage/readme.txt Storage/local/
```

Check the directory structure again:

```bash
K4y0x13@htb[/htb]$ tree .
```

Example output:

```
.
└── Storage
    ├── information.txt
    ├── local
    │   ├── readme.txt
    │   └── user
    │       ├── documents
    │       └── userinfo.txt
    └── readme.txt
```

## Additional Methods

In addition to basic file management commands, there are many other powerful ways to work with files in Linux, such as using redirection and text editors. Redirection allows you to manipulate the flow of input and output between commands and files, making tasks like creating or modifying files faster and more efficient. You can also use popular text editors like `vim` and `nano` for more interactive editing.

We will explore and discuss these methods in greater detail in later sections. As you become familiar with these techniques, you will gain more flexibility in how you create, edit, and manage files on your system.

## Optional Exercise

Use the tools we’ve already learned to figure out how to delete files and directories. Keep in mind that online research is a valuable part of the learning process—it’s not cheating. You’re not being tested right now, but rather building your knowledge. Searching for solutions online can expose you to different approaches and alternative methods, giving you a broader understanding of how things work.
