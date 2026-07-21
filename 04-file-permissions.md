# Linux File Permissions

## Introduction

Linux is a **multi-user operating system**, meaning multiple users can access and use the same system simultaneously. To prevent unauthorized users from accessing or modifying files, Linux provides a robust permission system.

Every file and directory in Linux has:

- An **owner (user)**
- A **group**
- A set of **permissions**

These permissions determine who can:

- Read the file
- Modify the file
- Execute the file

Understanding file permissions is one of the most important Linux concepts for **system administrators, DevOps engineers, cloud engineers, and security professionals**.

---

# Why File Permissions are Important

Imagine a Linux server running a banking application.

- The application should be able to read customer data.
- Developers should modify source code.
- Normal users should not access confidential files.
- Attackers should never gain permission to execute malicious scripts.

Linux permissions help achieve this.

Without permissions:

- Anyone could delete important files.
- Sensitive information could be leaked.
- Servers could be compromised.

---

# Viewing File Permissions

Use the following command:

```bash
ls -l
```

Example:

```bash
-rwxr-xr-- 1 karthik developers 2048 Jul 21 15:30 script.sh
```

Let's understand every part.

```
-rwxr-xr--
```

This single string describes everything about the file permissions.

---

# Understanding Each Character

```
-rwxr-xr--
```

|Position|Meaning|
|---------|-------|
|1|File type|
|2-4|Owner permissions|
|5-7|Group permissions|
|8-10|Others permissions|

---

## Character 1 : File Type

|Symbol|Meaning|
|-------|-------|
|-|Regular File|
|d|Directory|
|l|Symbolic Link|
|c|Character Device|
|b|Block Device|
|p|Named Pipe|
|s|Socket|

Example:

```
drwxr-xr-x
```

This is a directory.

Example:

```
-rw-r--r--
```

This is a regular file.

---

# Permission Symbols

Linux has only three permissions.

|Permission|Symbol|Meaning|
|-----------|------|-------|
|Read|r|View contents|
|Write|w|Modify contents|
|Execute|x|Run the file|

---

# Understanding Read Permission

For Files

Read means:

- Open the file
- View contents
- Copy contents

Example:

```bash
cat notes.txt
```

If you don't have read permission:

```
Permission denied
```

---

For Directories

Read means:

You can list the directory contents.

Example:

```bash
ls Documents
```

Without read permission:

You cannot see the files inside.

---

# Understanding Write Permission

For Files

Write means:

- Edit file
- Delete file contents
- Add new data

Example:

```bash
echo "Linux" >> notes.txt
```

Without write permission:

```
Permission denied
```

---

For Directories

Write permission means:

You can

- Create files
- Delete files
- Rename files

Example:

```bash
touch report.txt
```

Without write permission:

You cannot create new files.

---

# Understanding Execute Permission

For Files

Execute means:

The file can run like a program.

Example:

```bash
./script.sh
```

Without execute permission:

```
Permission denied
```

---

For Directories

Execute means:

You can enter the directory.

Example:

```bash
cd Documents
```

Without execute permission:

```
Permission denied
```

---

# Permission Categories

Linux divides users into three groups.

```
-rwxr-xr--
```

```
Owner
Group
Others
```

---

## Owner (User)

The person who created the file.

Example:

```
Owner = karthik
```

Permissions:

```
rwx
```

Meaning:

- Read
- Write
- Execute

---

## Group

Users belonging to the assigned group.

Example:

```
developers
```

Permissions:

```
r-x
```

Meaning:

- Read
- Execute

Cannot modify the file.

---

## Others

Everyone else.

Permissions:

```
r--
```

Meaning:

Can only read.

---

# Visual Representation

```
-rwxr-xr--
 │ │ │
 │ │ └── Others
 │ └──── Group
 └────── Owner
```

---

# Checking Owner and Group

Use

```bash
ls -l
```

Example

```bash
-rwxr-xr-- 1 karthik developers script.sh
```

Owner

```
karthik
```

Group

```
developers
```

---

# Changing Permissions

Linux provides the **chmod** command.

Syntax

```bash
chmod [permissions] filename
```

Example

```bash
chmod +x script.sh
```

Now the script becomes executable.

---

# Symbolic Method

Permissions can be modified using symbols.

## User Symbols

|Letter|Meaning|
|------|-------|
|u|Owner|
|g|Group|
|o|Others|
|a|All|

---

## Operators

|Operator|Meaning|
|---------|-------|
|+|Add permission|
|-|Remove permission|
|=|Assign exact permission|

---

Examples

Give execute permission to owner

```bash
chmod u+x script.sh
```

Remove write permission from group

```bash
chmod g-w report.txt
```

Give everyone read permission

```bash
chmod a+r notes.txt
```

Remove execute permission from others

```bash
chmod o-x script.sh
```

Assign only read permission to owner

```bash
chmod u=r file.txt
```

---

# Numeric Method (Octal Method)

Every permission has a numeric value.

|Permission|Value|
|----------|-----|
|Read|4|
|Write|2|
|Execute|1|

Total values:

|Number|Permission|
|------|----------|
|0|---|
|1|--x|
|2|-w-|
|3|-wx|
|4|r--|
|5|r-x|
|6|rw-|
|7|rwx|

---

## Example: chmod 755

```
7 = 4+2+1 = rwx
5 = 4+1 = r-x
5 = 4+1 = r-x
```

Command

```bash
chmod 755 script.sh
```

Permissions become

```
rwxr-xr-x
```

---

## Example: chmod 644

```
6 = rw-
4 = r--
4 = r--
```

Command

```bash
chmod 644 notes.txt
```

Permissions become

```
rw-r--r--
```

---

## Common Permission Values

|Permission|Meaning|
|----------|-------|
|777|Everyone has full access|
|755|Owner full, others read & execute|
|700|Only owner has access|
|644|Owner read/write, others read|
|600|Only owner can read/write|
|666|Everyone can read/write (not recommended)|

---

# Recursive Permissions

Apply permissions to all files and directories.

```bash
chmod -R 755 project/
```

Be careful because recursive permission changes affect every file inside.

---

# Changing Owner

Use

```bash
sudo chown username filename
```

Example

```bash
sudo chown karthik notes.txt
```

---

# Changing Owner and Group

```bash
sudo chown karthik:developers project.txt
```

---

# Changing Group

Use

```bash
sudo chgrp developers project.txt
```

---

# Viewing Detailed Information

Use

```bash
stat notes.txt
```

Example output

```
Access: (0644/-rw-r--r--)
Uid: (1000/karthik)
Gid: (1000/developers)
```

---

# Default Permissions

Linux initially creates files and directories with default permissions.

Files

```
666
```

Directories

```
777
```

The **umask** removes permissions.

Example

```
666
-022
-----
644
```

Directories

```
777
-022
-----
755
```

Check current umask

```bash
umask
```

---

# Special Permissions

Linux also supports advanced permissions.

## SUID (Set User ID)

When an executable has the SUID bit set, it runs with the permissions of its owner instead of the user executing it.

Example:

```bash
chmod u+s program
```

Display:

```
-rwsr-xr-x
```

Common example:

```
/usr/bin/passwd
```

A normal user can change their password because `passwd` runs with root privileges.

---

## SGID (Set Group ID)

Files execute with the group's permissions.

Directories created inside inherit the parent directory's group.

Example

```bash
chmod g+s shared_folder
```

Display

```
drwxr-sr-x
```

Useful for team collaboration.

---

## Sticky Bit

Commonly used on shared directories.

Only the owner can delete their own files.

Example

```
/tmp
```

Set Sticky Bit

```bash
chmod +t directory
```

Display

```
drwxrwxrwt
```

---

# Practical Examples

## Example 1

Create a script

```bash
touch backup.sh
```

Give execute permission

```bash
chmod +x backup.sh
```

Run

```bash
./backup.sh
```

---

## Example 2

Make a private file

```bash
touch secrets.txt
chmod 600 secrets.txt
```

Only owner can access.

---

## Example 3

Shared project folder

```bash
mkdir project
sudo chgrp developers project
chmod 775 project
chmod g+s project
```

Every new file inherits the developers group.

---

# Best Practices

- Never use `chmod 777` unless absolutely necessary.
- Use the principle of least privilege.
- Use groups instead of giving permissions to everyone.
- Regularly audit file permissions.
- Use `stat` to verify permissions.
- Protect sensitive files with `600` or `640`.

---

# Interview Questions

### What does chmod 755 mean?

Owner has read, write, execute.

Group has read and execute.

Others have read and execute.

---

### Difference between 644 and 755?

644

- Cannot execute

755

- Executable

---

### What is the difference between chown and chmod?

`chmod`

Changes permissions.

`chown`

Changes owner.

---

### Why is chmod 777 dangerous?

It allows everyone to:

- Read
- Modify
- Execute

This creates serious security risks.

---

# Summary

- Linux permissions control access to files and directories.
- There are three permissions: Read (r), Write (w), and Execute (x).
- Permissions are assigned to Owner, Group, and Others.
- `chmod` changes permissions.
- `chown` changes file ownership.
- `chgrp` changes the group.
- Numeric permissions like 755 and 644 are widely used.
- Special permissions include SUID, SGID, and Sticky Bit.
- Proper permission management is essential for Linux security and administration.