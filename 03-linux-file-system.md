# Linux File System

## Introduction

The Linux File System is the way Linux organizes, stores, and manages files and directories.

Unlike Windows, which uses multiple drives like **C:\**, **D:\**, and **E:\**, Linux has **only one root directory**.

Everything starts from the root directory:

```
/
```

Every file, folder, hard disk, USB drive, CD/DVD, and even hardware devices become part of this single directory tree.

Example:

```
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

This is known as the **Linux Directory Structure** or **Filesystem Hierarchy Standard (FHS).**

---

# Root Directory (/)

The root directory is the top-most directory.

Everything exists under it.

Do not confuse:

```
/
```

with

```
/root
```

They are completely different.

Example:

```
/
```

contains

```
home
etc
bin
usr
```

whereas

```
/root
```

is the home directory of the **root user** (system administrator).

---

# Absolute Path

An absolute path always starts from the root directory.

Example:

```
/home/user/Documents/file.txt
```

No matter where you currently are, this path always points to the same location.

Examples:

```
/etc/passwd

/usr/bin/python

/home/user/Desktop
```

---

# Relative Path

A relative path starts from your current working directory.

Suppose the current directory is

```
/home/user
```

Then

```
Documents/file.txt
```

means

```
/home/user/Documents/file.txt
```

Relative paths do not begin with "/".

---

# Difference Between Absolute and Relative Path

| Absolute Path | Relative Path |
|---------------|---------------|
| Starts with "/" | Doesn't start with "/" |
| Complete location | Depends on the current directory |
| Works from anywhere | Works only relative to the current location |

Example:

Absolute

```
/home/user/Desktop/test.txt
```

Relative

```
Desktop/test.txt
```

---

# Important Linux Directories

## 1. /bin

Contains essential command binaries.

Examples:

```
ls
cp
mv
cat
pwd
echo
rm
```

Check:

```
ls /bin
```

---

## 2. /sbin

Contains system administration commands.

Mostly used by the root user.

Examples:

```
fdisk
mkfs
shutdown
reboot
ifconfig
```

---

## 3. /boot

Contains files needed to boot Linux.

Examples:

- Linux Kernel
- GRUB Bootloader
- Boot Configuration Files

Example:

```
ls /boot
```

---

## 4. /dev

Contains device files.

Linux treats hardware devices as files.

Examples:

Hard Disk

```
/dev/sda
```

USB Drive

```
/dev/sdb
```

Terminal

```
/dev/tty
```

Random Number Generator

```
/dev/random
```

Null Device

```
/dev/null
```

---

### Interesting Device Files

#### /dev/null

Anything sent here disappears permanently.

Example:

```
echo "Hello" > /dev/null
```

Nothing gets stored.

---

#### /dev/zero

Produces an unlimited stream of zeros.

Useful while creating files.

Example:

```
cat /dev/zero
```

---

#### /dev/random

Generates random numbers.

---

# 5. /etc

Contains system configuration files.

This is one of the most important directories in Linux.

Examples:

```
/etc/passwd
/etc/group
/etc/hosts
/etc/fstab
/etc/hostname
```

Avoid storing personal files inside `/etc`.

---

# 6. /home

Contains the home directories of normal users.

Example:

```
/home/user1
/home/user2
/home/example
```

Personal files are usually stored here.

---

# 7. /root

The home directory of the root user.

Normal users generally cannot access it.

Example:

```
/root
```

---

# 8. /lib

Contains essential shared libraries.

Programs inside `/bin` depend on these libraries.

Comparable to DLL files in Windows.

---

# 9. /media

Automatically mounts removable storage devices.

Examples:

- USB Drives
- DVDs
- External Hard Drives

Example:

```
/media/user/USB_DRIVE
```

---

# 10. /mnt

Used for manually mounting filesystems temporarily.

Example:

```
sudo mount /dev/sdb1 /mnt
```

---

# 11. /opt

Stores optional third-party software.

Examples:

- Google Chrome
- Android Studio
- Visual Studio Code
- Oracle Software

---

# 12. /proc

A virtual filesystem.

Contains information about running processes and the kernel.

Nothing is physically stored here.

Useful commands:

```
ls /proc
```

CPU Information

```
cat /proc/cpuinfo
```

Memory Information

```
cat /proc/meminfo
```

Kernel Version

```
cat /proc/version
```

---

# 13. /run

Stores runtime information.

Contains temporary data created after the system boots.

Deleted after every restart.

---

# 14. /srv

Stores data served by system services.

Examples:

- Web Server Data
- FTP Server Data

---

# 15. /sys

A virtual filesystem containing information about hardware and the Linux kernel.

Often used for hardware configuration and system tuning.

---

# 16. /tmp

Stores temporary files.

Accessible by all users.

Files may be deleted automatically.

Example:

```
cd /tmp
```

---

# 17. /usr

One of the largest directories in Linux.

Contains installed applications and user utilities.

Common subdirectories:

```
/usr/bin
/usr/lib
/usr/share
/usr/local
```

Examples of programs found in `/usr/bin`:

```
python
java
gcc
vim
```

---

# 18. /var

Stores variable data.

Examples:

- Log Files
- Cache Files
- Databases
- Mail
- Print Queues

Examples:

```
/var/log
/var/cache
/var/spool
```

---

# Linux File Types

Linux supports several file types.

## Regular File

Contains user data.

Example:

```
notes.txt
```

---

## Directory

Contains files and subdirectories.

Example:

```
Documents
```

---

## Symbolic Link

A shortcut pointing to another file or directory.

Example:

```
ln -s file.txt shortcut
```

---

## Block Device

Represents storage devices.

Example:

```
/dev/sda
```

---

## Character Device

Represents devices that transfer data character by character.

Examples:

- Keyboard
- Mouse
- Terminal

---

## Socket

Used for communication between processes.

---

## Named Pipe (FIFO)

Used for inter-process communication.

---

# Identifying File Types

Use:

```
ls -l
```

The first character indicates the file type.

Examples:

Regular File

```
-rw-r--r--
```

Directory

```
drwxr-xr-x
```

Symbolic Link

```
lrwxrwxrwx
```

Block Device

```
brw-------
```

Character Device

```
crw-------
```

---

# Mounting

Linux does not use drive letters.

Instead, storage devices are mounted to directories.

Example:

```
sudo mount /dev/sdb1 /mnt
```

After mounting,

```
/mnt
```

becomes the access point for that device.

Unmount using:

```
sudo umount /mnt
```

---

# Common Filesystem Types

### ext4

The default filesystem for most Linux distributions.

### XFS

High-performance filesystem commonly used on enterprise servers.

### Btrfs

Supports advanced features like snapshots and checksums.

### FAT32

Compatible with Linux, Windows, and macOS.

### NTFS

The default filesystem used by Windows.

Linux can read and write NTFS partitions.

---

# Check Disk Usage

Display filesystem usage:

```
df -h
```

Display directory size:

```
du -sh Documents
```

---

# Useful Commands

Show current directory

```
pwd
```

List root directories

```
ls /
```

Show mounted filesystems

```
mount
```

Display filesystem usage

```
df -h
```

Display directory sizes

```
du -sh *
```

Identify a file type

```
file filename
```

---

# Quick Revision

- Linux has a single directory tree.
- The root directory is `/`.
- `/home` stores user home directories.
- `/root` is the home directory of the root user.
- `/etc` stores configuration files.
- `/bin` contains essential system commands.
- `/usr` stores installed applications and utilities.
- `/var` stores logs and other changing data.
- `/tmp` stores temporary files.
- `/dev` represents hardware as files.
- `/proc` and `/sys` are virtual filesystems.
- Linux uses mount points instead of drive letters.
- Use `df -h` to check disk usage.
- Use `du -sh` to check directory size.

---

# Interview Questions

1. What is the Linux File System?

2. What is the root directory?

3. What is the difference between `/` and `/root`?

4. What is the difference between an absolute path and a relative path?

5. What is stored inside `/etc`?

6. Why is `/proc` called a virtual filesystem?

7. What is the purpose of the `/var` directory?

8. What is `/dev/null`?

9. What is mounting in Linux?

10. What is the difference between ext4 and NTFS?