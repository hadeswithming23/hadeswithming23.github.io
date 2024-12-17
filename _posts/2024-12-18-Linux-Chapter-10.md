---
title: File System and Storage Device Management
date: 2024-12-18 00:43:30 +0800
categories: [Linux]
tags: [linux, knowledge]
---

# 10.0 File System and Storage Device Management
 Managing storage devices and file systems in Linux begins with the `/dev` directory, which represents all devices as files. 

## 10.1 Understanding `/dev`
- **`/dev`** is a special directory that contains device files, representing hardware devices like hard drives, partitions, USB drives, and more.
- Devices are accessed as files, e.g., `/dev/sda`, `/dev/sdb1`, etc.
- Types of device files:
  - **Block devices**: Represent storage devices (e.g., `/dev/sda`).
  - **Character devices**: Represent input/output devices (e.g., `/dev/tty`).

## 10.2 Device Representation in `/dev`
![example](assets/posts/chapter10linux2024/ls.png)
- the first character that is `b` represents block devices, while `c` belongs to character devices

**Block Devices**
- Block devices handle data in fixed-size blocks, used for storage devices where data is read and written in chunks.
  - Example: 
    - `/dev/sda` – First hard drive.
    - `/dev/sdb1` – First partition on the second hard drive.


**Character Devices**
- Character devices handle data as streams and transfer data one character at a time.
  - Example:
    -  `/dev/tty` – Represents terminal input/output.
    - `/dev/null` – Discards all data written to it.
    - `/dev/urandom` – Provides random bytes.

## 10.3 Structure of Device Files

**Path Format**: `/dev/` followed by a unique identifier:
- `/dev/sdX` – Represents block devices, where `X` denotes the device letter.
- `/dev/tty` – Represents character devices.

**Partitions**: Block devices can have multiple partitions:
- `/dev/sda1`, `/dev/sda2` – First, second partitions on the first disk.

## 10.4 Accessing Storage Devices

**Listing Devices**
Use `lsblk` or `fdisk` to view available devices:
- `lsblk` – Displays block devices and their partitions.
  ![lsblk](assets/posts/chapter10linux2024/lsblk.png)

- `fdisk -l` – Provides detailed partition information.
  ![fdisk](assets/posts/chapter10linux2024/fsdisk.png)

## 10.5 Mount and Unmount in Linux

1. Mount
**Mount** is used to **attach a file system** (or block device) to a directory, making it accessible for read/write operations.

```bash
mount /dev/sdb1 /mnt
```

This attaches the first partition of the second hard drive (`/dev/sdb1`) to the /mnt directory.

2. Unmount
**Unmount** is used to **detach the file system** or block device from a directory, preventing further access.

```bash
umount /dev/sdb1
```

This detaches the mounted partition `/dev/sdb1` from the directory. 
> The syntax for unmount command would without the **n** - `umount`
{: .prompt-warning }


## 10.6 Monitoring the File System in Linux
Monitoring and managing the file system in Linux is crucial for maintaining system stability and performance. Below are some important tools and commands used for this purpose:

### 10.6.1 Using `df` Command

- **`df`** (Disk Free) is used to display disk space usage of file systems.

  - Syntax:
    ```bash
    df [options] [file_or_directory]
    ```

  - Common Options:
    - `-h` : Human-readable format (e.g., KB, MB, GB).
    - `-T` : Display file system types.
    - `-a` : Include all file systems, even those with 0 usage.

  - Example:
    ```bash
    df -h /home
    ```

    Output:
    ```
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/sda1       50G   20G   28G  42%  /
    ```

### 10.6.2 Using `fsck` Command

- **`fsck`** (File System Consistency Check) is used to check and repair file systems.

  - Syntax:
    ```bash
    fsck [options] [device]
    ```

  - Common Options:
    - `-y` : Automatically respond "yes" to all prompts.
    - `-v` : Verbose mode (more detailed output).
    - `-t` : Check specific file system type (e.g., `ext4`, `xfs`).

  - Example:
    ```bash
    fsck /dev/sda1
    ```

    This will check and repair the file system on `/dev/sda1`.
