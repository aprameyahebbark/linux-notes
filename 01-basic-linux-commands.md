# Basic Linux Commands

## Introduction

Linux is a command-line driven operating system where most tasks are performed through the terminal using commands. Learning these basic commands is the first step toward becoming comfortable with Linux and is essential for Cloud Computing, DevOps, System Administration, and Software Development.

This document covers some of the most frequently used Linux commands, their syntax, examples, and practical use cases.

---

# 1. pwd

## Purpose

The `pwd` command stands for **Print Working Directory**.

It displays the complete (absolute) path of the directory you are currently working in.

This command is useful whenever you are unsure of your current location in the Linux file system.

---

## Syntax

```bash
pwd
```

---

## Example

```bash
$ pwd
```

Output

```text
/home/karthik/Documents
```

---

## Explanation

Suppose your current folder is:

```
Home
 └── Documents
      └── LinuxNotes
```

Running

```bash
pwd
```

prints

```text
/home/karthik/Documents/LinuxNotes
```

This tells you exactly where you are.

---

## Common Use Cases

- Verify the current directory.
- Before creating or deleting files.
- Useful while writing shell scripts.
- Helpful during file navigation.

---

## Interview Tip

**Q:** What is the difference between an absolute path and a relative path?

- Absolute path starts from the root directory (`/`).
- Relative path starts from the current directory.

---

# 2. ls

## Purpose

The `ls` command lists the files and directories inside the current directory.

It is one of the most frequently used Linux commands.

---

## Syntax

```bash
ls
```

---

## Example

```bash
$ ls
Documents Downloads Pictures Music notes.txt
```

---

## Explanation

Instead of opening a graphical file manager, Linux allows you to see the contents of a directory directly from the terminal.

---

## Common Options

### `ls -l`

Displays files in **long listing format**.

```bash
ls -l
```

Example output

```text
drwxr-xr-x 2 user user 4096 Jul 8 Documents
-rw-r--r-- 1 user user  512 Jul 8 notes.txt
```

Information shown:

- File permissions
- Number of links
- Owner
- Group
- File size
- Last modified date
- File name

---

### `ls -a`

Shows hidden files.

```bash
ls -a
```

Output

```text
.  ..  .bashrc  .profile  Documents
```

Hidden files begin with a dot (`.`).

---

### `ls -lh`

Displays file sizes in a human-readable format.

```bash
ls -lh
```

Example

```text
1.5K
45M
2.3G
```

instead of

```
1536
47185920
2147483648
```

---

## Common Use Cases

- View directory contents
- Check hidden files
- Verify file permissions
- Check file sizes

---

## Interview Tip

`ls` only lists files.

It does **not** change directories.

---

# 3. clear

## Purpose

Clears everything currently displayed in the terminal screen.

---

## Syntax

```bash
clear
```

---

## Example

```bash
$ clear
```

After execution, the terminal appears empty, but previous commands are still stored in the terminal history.

---

## Common Use Cases

- Clean the terminal before running commands.
- Improve readability during demonstrations.

---

# 4. whoami

## Purpose

Displays the username of the currently logged-in user.

---

## Syntax

```bash
whoami
```

---

## Example

```bash
$ whoami
```

Output

```text
karthik
```

---

## Use Cases

- Verify the active user.
- Check permissions.
- Confirm the current account after switching users.

---

# 5. date

## Purpose

Displays the current system date and time.

---

## Syntax

```bash
date
```

---

## Example

```bash
$ date
```

Output

```text
Tue Jul 8 14:35:42 IST 2026
```

---

## Useful Options

Display only the year

```bash
date +%Y
```

Display only the current month

```bash
date +%m
```

Display only today's date

```bash
date +%d
```

---

## Common Use Cases

- Check system time.
- Timestamp logs.
- Use in shell scripts.

---

# 6. cal

## Purpose

Displays a calendar in the terminal.

---

## Syntax

```bash
cal
```

---

## Example

```bash
$ cal
```

Output

```text
     July 2026
Su Mo Tu We Th Fr Sa
         1  2  3  4
5  6  7  8  9 10 11
...
```

---

## Useful Options

Display an entire year

```bash
cal 2026
```

Display a specific month

```bash
cal 7 2026
```

---

# 7. history

## Purpose

Displays previously executed terminal commands.

---

## Syntax

```bash
history
```

---

## Example

```bash
history
```

Output

```text
1 pwd
2 ls
3 mkdir Linux
4 cd Linux
5 touch notes.txt
```

---

## Common Use Cases

- Recall previous commands.
- Repeat commands.
- Debug terminal activity.

---

# 8. man

## Purpose

Displays the official Linux manual page for a command.

---

## Syntax

```bash
man command_name
```

Example

```bash
man ls
```

---

## Navigation

| Key | Action |
|------|--------|
| Enter | Scroll one line |
| Space | Next page |
| b | Previous page |
| q | Quit |

---

## Common Use Cases

- Learn command options.
- Read official documentation.
- Troubleshoot unfamiliar commands.

---

# 9. echo

## Purpose

Prints text or variable values to the terminal.

---

## Syntax

```bash
echo "Hello Linux"
```

---

## Example

Output

```text
Hello Linux
```

---

## Common Use Cases

- Display messages.
- Print environment variables.
- Debug shell scripts.

---

# 10. uname

## Purpose

Displays information about the Linux operating system and kernel.

---

## Syntax

```bash
uname
```

---

## Useful Options

Display kernel name

```bash
uname
```

Display kernel version

```bash
uname -r
```

Display all available information

```bash
uname -a
```

---

## Example

```bash
$ uname -a
```

Output

```text
Linux ubuntu 6.8.0 x86_64 GNU/Linux
```

---

# Summary

These commands form the foundation of Linux terminal usage. Becoming comfortable with them will make it much easier to navigate the file system, manage files, understand the operating system, and progress to more advanced topics such as shell scripting, networking, Docker, and DevOps.