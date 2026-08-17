# Linux Users and Groups

> "Everything in Linux happens through users and permissions."

---

# Table of Contents

1. Introduction
2. Why Linux is Multi-user
3. Types of Users
4. Understanding UID & GID
5. Linux User Architecture
6. /etc/passwd Explained
7. /etc/shadow Explained
8. /etc/group Explained
9. /etc/gshadow Explained
10. Home Directories
11. Login Shells
12. Creating Users
13. Managing Passwords
14. Modifying Users
15. Deleting Users
16. Groups
17. Group Management
18. User & Group Commands
19. Sudo and Root
20. visudo and sudoers
21. su vs sudo
22. Environment Variables
23. User Configuration Files
24. Enterprise User Management
25. AWS IAM vs Linux Users
26. Docker & Kubernetes Users
27. Security Best Practices
28. Troubleshooting
29. Practical Labs
30. Interview Questions
31. Command Cheat Sheet
32. Summary

---

# 1. Introduction

Linux was designed from the beginning to support multiple users working on the same computer simultaneously.

Every action performed in Linux belongs to a user.

Examples:

- Creating files
- Installing software
- Running programs
- Managing services
- Starting processes

Linux identifies every user uniquely and controls what they are allowed to do.

Without users and permissions, Linux would not be secure.

---

# 2. Why Linux is Multi-user

Unlike Windows Personal editions that originally focused on one person using one computer, Unix and Linux were designed for servers.

Imagine a university server.

- 300 students
- 20 professors
- Administrators

Everyone logs into the same machine.

Each person gets:

- Separate files
- Separate password
- Separate home directory
- Separate permissions

No user should access another user's private files.

This is why Linux is called a Multi-user Operating System.

Advantages

✔ Security

✔ Isolation

✔ Resource sharing

✔ Easier administration

✔ Better auditing

---

# 3. Types of Users

Linux mainly has three user types.

## 1. Root User

Username:

```
root
```

UID

```
0
```

Characteristics

- Superuser
- Unlimited permissions
- Can modify anything
- Can delete system files
- Can install software
- Can create users

Example

```
sudo rm -rf /
```

Root can even destroy the operating system.

Be careful.

---

## 2. System Users

Used by services.

Examples

```
mysql
nginx
apache
daemon
nobody
postfix
```

These users usually

- cannot login
- don't have home directories
- run background services

Example

Apache web server runs as

```
www-data
```

instead of root.

---

## 3. Normal Users

Created for humans.

Example

```
john
alice
ubuntu
developer
```

Characteristics

- Limited permissions
- Own home directory
- Login shell
- Can only modify their own files

---

# 4. Understanding UID & GID

Linux does NOT internally identify users by username.

It uses numbers.

## UID

User ID

Example

```
john → UID 1001
```

## GID

Group ID

Example

```
developers → GID 1002
```

Commands

```
id
```

Output

```
uid=1000(john)
gid=1000(john)
groups=1000(john),27(sudo)
```

---

Common UID Ranges

| UID | Meaning |
|------|----------|
|0|Root|
|1-999|System users|
|1000+|Normal users|

---

# 5. Linux User Architecture

```
              User

                │

        Username

                │

         /etc/passwd

                │

            UID

                │

         Authentication

                │

         /etc/shadow

                │

          Home Directory

                │

       /home/username

                │

          Login Shell

```

---

# 6. /etc/passwd Explained

Stores user account information.

View

```
cat /etc/passwd
```

Example

```
john:x:1000:1000:John Doe:/home/john:/bin/bash
```

Fields

```
username

password placeholder

UID

GID

comment

home directory

login shell
```

Meaning

```
john
```

Username

```
x
```

Password stored elsewhere

```
1000
```

UID

```
1000
```

Primary group

```
John Doe
```

Description

```
/home/john
```

Home

```
/bin/bash
```

Shell

---

# 7. /etc/shadow Explained

Stores encrypted passwords.

Only root can read.

View

```
sudo cat /etc/shadow
```

Example

```
john:$6$ABC123.....:19820:0:99999:7:::
```

Fields

```
Username

Encrypted password

Last password change

Minimum days

Maximum days

Warning days

Inactive days

Expiration
```

Why separate?

Earlier Linux stored passwords inside

```
/etc/passwd
```

Everyone could read it.

Huge security problem.

Modern Linux separates passwords into

```
/etc/shadow
```

---

# 8. /etc/group Explained

Contains group information.

Example

```
developers:x:1001:john,alice,bob
```

Fields

```
Group name

Password placeholder

GID

Members
```

---

# 9. /etc/gshadow Explained

Secure version of

```
/etc/group
```

Contains

- encrypted group password
- administrators
- members

Normally accessed only by root.

---

# 10. Home Directories

Every normal user gets

```
/home/username
```

Example

```
/home/john
```

Contains

- Documents
- Downloads
- Hidden configuration
- Desktop
- Projects

Display

```
echo $HOME
```

Example

```
/home/john
```

---

# 11. Login Shells

A shell interprets commands.

Common shells

```
/bin/bash
```

```
/bin/zsh
```

```
/bin/sh
```

```
/bin/dash
```

```
/usr/bin/fish
```

View current shell

```
echo $SHELL
```

List available shells

```
cat /etc/shells
```

Disable login

```
/usr/sbin/nologin
```

---

# 12. Creating Users

Using useradd

```
sudo useradd john
```

Create with home directory

```
sudo useradd -m john
```

Specify shell

```
sudo useradd -m -s /bin/bash john
```

Create using adduser (Ubuntu)

```
sudo adduser john
```

Difference

useradd

Low-level

adduser

Interactive

---

# 13. Managing Passwords

Set password

```
sudo passwd john
```

Change own password

```
passwd
```

Lock account

```
sudo passwd -l john
```

Unlock

```
sudo passwd -u john
```

Force password reset

```
sudo passwd -e john
```

---

# 14. Modifying Users

Rename

```
sudo usermod -l newname oldname
```

Change home

```
sudo usermod -d /home/newhome john
```

Move home

```
sudo usermod -m -d /home/newhome john
```

Change shell

```
sudo usermod -s /bin/zsh john
```

Add supplementary group

```
sudo usermod -aG docker john
```

Never forget

```
-aG
```

Using only

```
-G
```

removes previous supplementary groups.

---

# 15. Deleting Users

Delete account

```
sudo userdel john
```

Delete account and home

```
sudo userdel -r john
```

---

# 16. Groups

Groups simplify permission management.

Instead of assigning permissions to 100 users individually,

assign permissions to one group.

Example

```
developers
```

Members

```
John

Alice

Bob

David
```

Grant access to group once.

Everyone benefits.

---

Primary Group

Every user has one.

Secondary Groups

A user may belong to many.

Check

```
groups
```

or

```
id
```

---

# 17. Group Management

Create

```
sudo groupadd developers
```

Delete

```
sudo groupdel developers
```

Rename

```
sudo groupmod -n dev developers
```

Add user

```
sudo usermod -aG developers john
```

Remove user

```
sudo gpasswd -d john developers
```

View groups

```
cat /etc/group
```

---

# 18. User & Group Commands

Current user

```
whoami
```

Current UID

```
id
```

Current groups

```
groups
```

Logged-in users

```
who
```

Detailed login

```
w
```

Last logins

```
last
```

Current session

```
logname
```

---

# 19. Sudo and Root

Root

Unlimited access.

Instead of logging in as root,

Linux recommends

```
sudo
```

Example

```
sudo apt update
```

Advantages

- Audit trail
- Safer
- Temporary privileges
- Better security

---

# 20. visudo and sudoers

Configuration file

```
/etc/sudoers
```

Never edit directly.

Use

```
sudo visudo
```

Grant sudo

```
john ALL=(ALL:ALL) ALL
```

Group-based

```
%sudo ALL=(ALL:ALL) ALL
```

---

# 21. su vs sudo

su

```
su
```

Changes to another user.

Usually root.

Requires root password.

sudo

```
sudo command
```

Runs only one command as root.

Requires your own password.

Comparison

| Feature | su | sudo |
|---------|------|------|
|Switch user|Yes|No|
|Runs one command|No|Yes|
|Uses root password|Usually|No|
|Audited|Less|Yes|

---

# 22. Environment Variables

Variables storing user environment.

View

```
env
```

Important

```
HOME
```

```
USER
```

```
PATH
```

```
SHELL
```

Example

```
echo $USER
```

```
echo $PATH
```

---

# 23. User Configuration Files

Hidden files begin with

```
.
```

Examples

```
.bashrc
```

```
.profile
```

```
.bash_logout
```

```
.gitconfig
```

These customize

- aliases
- prompt
- environment variables
- startup commands

---

# 24. Enterprise User Management

Large companies rarely create local users manually.

Instead they use centralized authentication.

Examples

LDAP

Lightweight Directory Access Protocol

Microsoft Active Directory

FreeIPA

SSSD

Benefits

- One login
- Central password policy
- Single Sign-On
- Easier management

---

# 25. AWS IAM vs Linux Users

Linux User

Exists on one machine.

AWS IAM User

Exists in AWS account.

Linux

```
john
```

AWS

```
Developer-IAM
```

Comparison

| Linux | AWS IAM |
|--------|----------|
|Machine|Cloud|
|UID|IAM Identity|
|Password|Console Password|
|Groups|IAM Groups|
|Permissions|IAM Policies|

Cloud engineers manage both.

---

# 26. Docker & Kubernetes Users

Docker

Containers often run as

```
root
```

Better practice

```
USER appuser
```

inside Dockerfile.

Kubernetes

Security Context

```
runAsUser
```

Example

```yaml
securityContext:
  runAsUser: 1001
```

Never run containers as root unless necessary.

---

# 27. Security Best Practices

✔ Disable root SSH login

✔ Use sudo

✔ Strong passwords

✔ MFA where available

✔ Least privilege

✔ Remove unused accounts

✔ Lock inactive users

✔ Audit logins

✔ Update software regularly

✔ Review sudo permissions

---

# 28. Troubleshooting

Cannot login

Check

```
/etc/passwd
```

Account locked

```
passwd -S username
```

Permission denied

```
ls -l
```

Check groups

```
groups
```

Check ownership

```
ls -ld file
```

---

# 29. Practical Labs

## Lab 1

Create user

```
sudo adduser student1
```

---

## Lab 2

Set password

```
sudo passwd student1
```

---

## Lab 3

Create group

```
sudo groupadd developers
```

---

## Lab 4

Add user

```
sudo usermod -aG developers student1
```

---

## Lab 5

Verify

```
groups student1
```

---

## Lab 6

Change shell

```
sudo usermod -s /bin/bash student1
```

---

## Lab 7

Delete user

```
sudo userdel -r student1
```

---

# 30. Interview Questions

### Beginner

Why is Linux called multi-user?

Difference between root and normal user?

What is UID?

What is GID?

What is sudo?

Difference between su and sudo?

---

### Intermediate

Explain /etc/passwd.

Explain /etc/shadow.

Difference between primary and secondary groups.

How do you lock a user?

Difference between useradd and adduser?

---

### Advanced

How does LDAP work?

Explain Active Directory integration.

How does sudo logging improve security?

Why should Docker avoid root containers?

Explain Linux authentication flow.

---

# 31. Command Cheat Sheet

| Command | Purpose |
|----------|----------|
|whoami|Current user|
|id|UID and GID|
|groups|Groups|
|who|Logged users|
|w|Detailed users|
|last|Login history|
|useradd|Create user|
|adduser|Interactive create|
|passwd|Change password|
|usermod|Modify user|
|userdel|Delete user|
|groupadd|Create group|
|groupdel|Delete group|
|groupmod|Modify group|
|gpasswd|Manage groups|
|visudo|Edit sudoers|
|su|Switch user|
|sudo|Run privileged command|
|env|Environment variables|
|echo $PATH|View PATH|
|echo $HOME|Home directory|

---

# 32. Summary

Linux is fundamentally a multi-user operating system built around the concepts of users, groups, identities, and permissions. Every action performed on the system is associated with a specific user and controlled through ownership, group membership, and access rights.

Key takeaways:

- Every user has a unique **UID (User ID)**.
- Every group has a unique **GID (Group ID)**.
- User account details are stored in **`/etc/passwd`**, while encrypted passwords are stored securely in **`/etc/shadow`**.
- Group information resides in **`/etc/group`** and secure group data in **`/etc/gshadow`**.
- Each normal user typically has a dedicated home directory under **`/home`** and a default login shell such as Bash.
- Administrative tasks should be performed with **`sudo`** instead of logging in directly as the root user.
- Proper group management simplifies permission administration across teams.
- Enterprise environments often integrate Linux with centralized identity systems like **LDAP**, **Active Directory**, or **FreeIPA**.
- In cloud-native environments, Linux user concepts extend into services such as **AWS IAM**, **Docker**, and **Kubernetes**, where identity and least-privilege principles remain critical.

---

# Real-World DevOps Perspective

Understanding Linux users and groups is essential because almost every DevOps tool relies on these concepts:

- Jenkins agents run as dedicated service users.
- Docker containers should avoid running as the root user.
- Kubernetes Pods can be configured with specific user IDs (`runAsUser`).
- CI/CD pipelines require controlled access through service accounts.
- Cloud virtual machines (EC2, Azure VMs, GCP Compute Engine) authenticate administrators using Linux users and SSH keys.
- Production servers use groups to control access to application files, logs, and deployment directories.

A strong understanding of Linux identity management forms the foundation for system administration, cybersecurity, cloud engineering, DevOps, and Site Reliability Engineering (SRE).

---

# What's Next?

After mastering **Linux Users and Groups**, the recommended learning sequence is:

1. Linux File Permissions
2. chmod, chown, and chgrp
3. ACL (Access Control Lists)
4. Linux Processes and Process Management
5. Systemd and Services
6. Package Management (APT, DNF, YUM)
7. SSH and Remote Access
8. Networking Fundamentals
9. Shell Scripting
10. Cron Jobs and Automations

These topics build directly on the concepts introduced in this guide and are core skills expected from Linux administrators, cloud engineers, and DevOps professionals and also used in different pipeline implementations and deployment as commands.