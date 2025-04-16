---
title: Regular Expressions
published: 2025-04-16
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Linux
draft: false
---
Regular expressions (RegEx) are indeed a powerful tool for text searching, replacing, and manipulating. The exercises you provided are great for practicing how to use RegEx in real-world scenarios. Let's go over each one:

1. **Show all lines that do not contain the `#` character.**

   In this case, we can use the negation operator (`^`) combined with the `grep` command to exclude lines containing `#`.

   ```bash
   grep -v "#" /etc/ssh/sshd_config
   ```

   The `-v` option inverts the match, meaning it will show lines that do **not** contain `#`.

2. **Search for all lines that contain a word that starts with `Permit`.**

   To find lines with words starting with "Permit", you can use the following command with the `^` and `\b` anchors:

   ```bash
   grep -E "\bPermit\w*" /etc/ssh/sshd_config
   ```

   Here, `\b` denotes a word boundary, and `\w*` allows any number of word characters (letters, digits, or underscores) following "Permit".

3. **Search for all lines that contain a word ending with `Authentication`.**

   For this, use the `\b` anchor to indicate a word boundary and a `*` quantifier to match any number of characters before "Authentication":

   ```bash
   grep -E "\w*Authentication\b" /etc/ssh/sshd_config
   ```

   This matches any word that ends with "Authentication".

4. **Search for all lines containing the word `Key`.**

   You can simply search for the word `Key` in the file:

   ```bash
   grep "Key" /etc/ssh/sshd_config
   ```

   This will display all lines containing the word "Key" (case-sensitive).

5. **Search for all lines beginning with `Password` and containing `yes`.**

   You can combine the beginning of the line anchor (`^`) with the `grep` command to match lines starting with `Password` and containing `yes` somewhere:

   ```bash
   grep -E "^Password.*yes" /etc/ssh/sshd_config
   ```

   The `^Password` ensures the line begins with `Password`, and `.*yes` allows `yes` to appear later in the line.

6. **Search for all lines that end with `yes`.**

   To find lines ending with `yes`, use the `$` anchor to indicate the end of the line:

   ```bash
   grep -E "yes$" /etc/ssh/sshd_config
   ```

   The `$` symbol ensures the line ends with `yes`.

These exercises give you a solid foundation in using RegEx for practical tasks like configuration file parsing and text manipulation. Let me know if you'd like further explanations or more practice!