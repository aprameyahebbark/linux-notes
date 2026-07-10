# File and Directory Management

## Introduction

Everything in Linux is organized in the form of files and directories. Unlike Windows, where drives such as `C:` or `D:` are used, Linux organizes everything under a single root directory (`/`).

Efficient file and directory management is one of the most fundamental Linux skills and is essential for Cloud Computing, DevOps, System Administration, Software Development, and Shell Scripting.

This chapter covers the most commonly used commands for navigating the Linux file system, creating files and directories, copying, moving, renaming, deleting, and searching files.

---

# Understanding the Linux File System

Before learning commands, it is important to understand how Linux organizes files.

```
/
├── bin
├── boot
├── dev
├── etc
├── home
│   └── username
│       ├── Documents
│       ├── Downloads
│       └── Desktop
├── lib
├── media
├── opt
├── root
├── tmp
├── usr
└── var
```

The slash (`/`) represents the **root directory**, which is the top-most directory in Linux.

Every file and directory exists somewhere under this root.

---

# Absolute vs Relative Paths

## Absolute Path

An absolute path always starts from the root directory.

Example

```bash
/home/username/Documents/LinuxNotes
```

Absolute paths always begin with `/`.

---

## Relative Path

A relative path starts from your current working directory.

Example

```bash
Documents/LinuxNotes
```

or

```bash
../Downloads
```

---

## Interview Tip

Absolute paths never depend on your current location.

Relative paths always depend on your current directory.

---

# 1. cd

## Purpose

The `cd` command stands for **Change Directory**.

It is used to move from one directory to another.

---

## Syntax

```bash
cd directory_name
```

---

## Example

```bash
cd Documents
```

Moves into the Documents folder.

---

## Move to Home Directory

```bash
cd
```

or

```bash
cd ~
```

---

## Move One Directory Back

```bash
cd ..
```

Suppose you are here

```
/home/username/Documents/LinuxNotes
```

After running

```bash
cd ..
```

You move to

```
/home/username/Documents
```

---

## Move Two Directories Back

```bash
cd ../..
```

---

## Go to Previous Directory

```bash
cd -
```

---

## Go to Root Directory

```bash
cd /
```

---

## Common Use Cases

- Navigate between folders
- Move to project directories
- Return to home directory
- Access system folders

---

# 2. mkdir

## Purpose

Creates a new directory.

---

## Syntax

```bash
mkdir directory_name
```

---

## Example

```bash
mkdir LinuxNotes
```

Creates

```
LinuxNotes/
```

---

## Create Multiple Directories

```bash
mkdir Notes Projects Downloads
```

---

## Create Nested Directories

```bash
mkdir -p Projects/Linux/Basics
```

Creates

```
Projects
└── Linux
    └── Basics
```

without errors.

---

## Common Use Cases

- Organize projects
- Create folder structures
- Prepare application directories

---

# 3. rmdir

## Purpose

Removes an **empty** directory.

---

## Syntax

```bash
rmdir directory_name
```

---

## Example

```bash
rmdir Test
```

---

## Important

`rmdir` only removes empty directories.

If the directory contains files, it will fail.

---

# 4. touch

## Purpose

Creates an empty file.

---

## Syntax

```bash
touch filename
```

---

## Example

```bash
touch notes.txt
```

Creates

```
notes.txt
```

---

## Create Multiple Files

```bash
touch file1.txt file2.txt file3.txt
```

---

## Common Use Cases

- Create text files
- Create configuration files
- Test file permissions

---

# 5. cp

## Purpose

Copies files and directories.

---

## Syntax

```bash
cp source destination
```

---

## Example

```bash
cp notes.txt Backup/
```

Copies

```
notes.txt
```

to

```
Backup/
```

---

## Copy Directory

```bash
cp -r Projects Backup
```

The `-r` option copies directories recursively.

---

## Common Use Cases

- Backup files
- Duplicate folders
- Copy configuration files

---

# 6. mv

## Purpose

Moves or renames files and directories.

---

## Syntax

```bash
mv source destination
```

---

## Move File

```bash
mv notes.txt Documents/
```

---

## Rename File

```bash
mv notes.txt linux_notes.txt
```

---

## Rename Directory

```bash
mv Projects LinuxProjects
```

---

## Common Use Cases

- Organize files
- Rename files
- Move directories

---

# 7. rm

## Purpose

Deletes files.

---

## Syntax

```bash
rm filename
```

---

## Example

```bash
rm notes.txt
```

Deletes the file permanently.

---

## Delete Multiple Files

```bash
rm file1 file2 file3
```

---

## Delete Directory Recursively

```bash
rm -r FolderName
```

---

## Force Delete

```bash
rm -rf FolderName
```

### Warning

`rm -rf` permanently deletes files and directories without confirmation.

Use this command carefully.

---

## Interview Tip

One of the most dangerous Linux commands is

```bash
rm -rf
```

because deleted files usually cannot be recovered.

---

# 8. find

## Purpose

Searches for files and directories.

---

## Syntax

```bash
find path options
```

---

## Find File

```bash
find . -name notes.txt
```

Searches from the current directory.

---

## Find Directory

```bash
find . -type d
```

---

## Find Files Only

```bash
find . -type f
```

---

## Common Use Cases

- Locate files
- Search logs
- Find configuration files

---

# 9. locate

## Purpose

Searches files quickly using a database.

---

## Syntax

```bash
locate filename
```

---

## Example

```bash
locate bashrc
```

---

## Note

If the database is outdated, update it using

```bash
sudo updatedb
```

---

# 10. tree

## Purpose

Displays directories in a tree-like structure.

---

## Syntax

```bash
tree
```

---

## Example

```
LinuxNotes
├── README.md
├── 01-basic-linux-commands.md
└── 02-file-directory-management.md
```

---

## Install Tree

Ubuntu

```bash
sudo apt install tree
```

---

# Special Directory Symbols

| Symbol | Meaning |
|----------|---------|
| . | Current directory |
| .. | Parent directory |
| ~ | Home directory |
| / | Root directory |

---

# Summary Table

| Command | Purpose |
|----------|---------|
| cd | Change directory |
| mkdir | Create directory |
| rmdir | Remove empty directory |
| touch | Create file |
| cp | Copy files/directories |
| mv | Move or rename |
| rm | Delete files/directories |
| find | Search files |
| locate | Fast file search |
| tree | Display directory structure |

---

# Common Interview Questions

### Q1. What is the difference between `cp` and `mv`?

- `cp` creates a copy.
- `mv` moves or renames the original.

---

### Q2. Why is `rm -rf` considered dangerous?

Because it permanently deletes files and directories recursively without confirmation.

---

### Q3. What is the difference between `rmdir` and `rm -r`?

- `rmdir` removes only empty directories.
- `rm -r` removes directories along with their contents.

---

### Q4. What is the difference between an absolute path and a relative path?

An absolute path starts from the root (`/`), whereas a relative path starts from the current working directory.

---

# Conclusion

File and directory management forms the backbone of Linux administration. Mastering these commands allows you to efficiently navigate the file system, organize data, manage projects, and perform daily administrative tasks. These commands are heavily used in Cloud Computing, DevOps, Docker, Kubernetes, Shell Scripting, and Linux system administration.