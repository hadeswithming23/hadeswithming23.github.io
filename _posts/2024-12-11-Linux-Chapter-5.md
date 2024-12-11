---
title: Linux File Permissions and Ownership
date: 2024-12-11 21:47:00 +0800
categories: [Linux]
tags: [knowledge, linux]
---

# Linux File Permissions and Ownership

File permissions and ownership are critical in Linux to ensure security and proper access control. This guide covers the essentials for understanding and managing permissions and ownership.

## 5.1 Basics of File Permissions
Linux uses a permission model with three access categories:
- **Owner**: The user who owns the file.
- **Group**: The group that owns the file.
- **Others**: All other users.

### 5.1.1 Permission Types
Each file or directory has three types of permissions:
1. **Read (r)**: Allows reading the contents of a file or listing a directory's contents.
2. **Write (w)**: Allows modifying the contents of a file or adding/removing files in a directory.
3. **Execute (x)**: Allows executing a file or accessing a directory.

### 5.1.2 Representation
- **Symbolic (ls -l output)**: `-rwxr-xr--`
- First character: File type (`-` for file, `d` for directory, etc.).
- Next three: Owner permissions.
- Next three: Group permissions.
- Last three: Other permissions.

- **Octal (Numeric)**:
Each permission is represented by a digit:
- `4` = Read
- `2` = Write
- `1` = Execute
Combine these to calculate permissions (e.g., `7` = `4+2+1` = `rwx`).


## 5.2 Viewing Permissions
To check permissions:
```bash
ls -l <file_or_directory>
```

**Example output:**
> -rw-r--r--  1 user group  12345 Dec 11 12:00 example.txt
- `-rw-r--r--`: Permissions
- `user`: Owner
- `group`: Group

## 5.3 Changing Permissions
**Using `chmod`**
Modify file permissions:
```bash
chmod <mode> <file>
```

**Symbolic Mode**
- Add (+), remove (-), or set (=) permissions. Example:
```bash
chmod u+x example.sh  # Add execute for owner
chmod g-w example.txt # Remove write for group
chmod o=r file.txt    # Set read-only for others
```

**Numeric Mode**
- Set permissions using octal values. Example:
```bash
chmod 755 example.sh  # rwx for owner, rx for group/others
chmod 644 example.txt # rw for owner, r for group/others
```

## 5.4 Chaning Ownership
**Using `chown`**
Change file owner and/or group:
```bash
chown <owner>:<group> <file>
```

- Change only the owner
```bash
chown user example.txt
```

- Change only the group
```bash
chown :group example.txt
``` 

**Recursive Change**
To apply changes to all files and subdirectories:
```bash
chown -R <owner>:<group> <directory>
```

## 5.5 Special Permissions
**Setuid**
- **Purpose**: Run a file with the permission of its owner.
- Command:
```bash
chmod u+s <file>
```

**Setgid**
- **Purpose**: Run a file with the permissions of its group or ensure files created in a directory inherit the group.
- Command:
```bash
chmod g+s <file_or_directory>
```

**Sticky Bit**
- **Purpose**: Prevent deletion of files in a directory by users other than the owner.
- Command:
```bash
chmod +t <directory>
```

## 5.6 Examples 
**Example 1: Restrict Access**
- Task: Allow the owner full access (`rwx`), the group read-only (`r--`), and others no access (`---`).
- Command:
```bash
chmod 740 file.txt
```

**Example 2: Shared Directory**
- Task: Allow a group to collaboratively modify files, but restrict others.
- Command:
```bash
mkdir shared_folder
chmod 2770 shared_folder
chown :shared_group shared_folder
```

**Example 3: Setuid and Sticky Bit**
- Task: Enable a script to run with its owner's permissions and protect a directory.
- Commands:
```bash
chmod u+s script.sh
chmod +t /tmp
```

## 5.7 Summary Table

| **Command** | **Description**                          | **Example**                 |
| ----------- | ---------------------------------------- | --------------------------- |
| `ls -l`     | View file permissions                    | `ls -l file.txt`            |
| `chmod`     | Change permissions (symbolic or numeric) | `chmod 644 file.txt`        |
| `chown`     | Change ownership (owner or group)        | `chown user:group file.txt` |
| `chmod u+s` | Add Setuid bit                           | `chmod u+s script.sh`       |
| `chmod g+s` | Add Setgid bit                           | `chmod g+s folder/`         |
| `chmod +t`  | Add sticky bit                           | `chmod +t /tmp`             |

**When to Use a Four-Digit Mode**
- **Setuid (4)**: Applies to executable files and allows the file to be run as the file owner, not the executor.
- **Setgid (2)**: Common for shared directories to maintain group consistency.
- **Sticky Bit (1)**: Used on directories like `/tmp` to restrict deletion to the file owner.
