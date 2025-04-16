---
title: Editing Files
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Linux
draft: false
---

This section covers editing files in Linux using two different text editors: **Nano** and **Vim**.

### Nano Editor
- **Nano** is a simple, command-line-based text editor, which is ideal for beginners. It provides an easy-to-navigate interface, where commands are listed at the bottom of the screen.
- To start editing a file, use the `nano` command followed by the file name:
  ```bash
  nano notes.txt
  ```
  In the editor, you can type your content directly. Nano's shortcuts are displayed at the bottom of the screen. For example:
  - `CTRL + O`: Save the file.
  - `CTRL + X`: Exit Nano.
  - `CTRL + W`: Search for a word in the file.

Once you're done editing, you can save and exit with `CTRL + O` and `CTRL + X`, respectively. To view the contents of the file from the shell, you can use `cat`:
```bash
cat notes.txt
```

### Vim Editor
- **Vim** is a more advanced text editor and is modal. This means it has different modes for navigating, editing, and executing commands.
  - **Normal mode**: Where you issue commands.
  - **Insert mode**: Where you can type text.
  - **Command mode**: Allows you to enter commands like `:q` (quit), `:w` (save), etc.

To open Vim, simply type:
```bash
vim
```
Once inside Vim, you start in **Normal mode**. To start editing, press `i` to enter **Insert mode**. After typing your text, press `ESC` to return to Normal mode. From there, you can issue commands, such as:
- `:q`: Quit Vim.
- `:w`: Save the file.
- `:wq`: Save and quit.
- `:q!`: Quit without saving.

Vim also has a built-in tutor that you can access by running:
```bash
vimtutor
```
This provides a guided tutorial to get you up to speed with Vim's commands and functionality.

### Optional Exercise:
To get comfortable with Vim, open the Vim tutor with `vimtutor` and follow the lessons. It will guide you through essential Vim commands and help you become more efficient in editing text files.

By practicing and becoming familiar with these editors, you’ll be able to quickly and effectively edit and manage files in Linux.
