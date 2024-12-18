---
title: Introduction to Linux
date: 2024-12-09 02:30:00 +0800
categories: [Linux]
tags: [knowledge, linux]
---


This is a site for introducing Linux!

## Before Starting to Know About Linux
> Prepare a virtual machine like Kali Linux before you get started to read this !!
{: .prompt-info }

Please navigate through below link to install your VM under the tab Pre-built VMs and select the VM based on your preferration. (if you haven't done it yet)


<a href="https://www.kali.org/get-kali/#kali-virtual-machines" target="_blank">Kali Linux VM</a>

## 1.1 Introduction to Terms and Concepts
  - Binary programs are usually stored in the /usr/bin or /usr/sbin directory.
    - ps
    - cat
    - ls
    - cd

  - Case-sensitive (Not like Windows)
  
  - Directory (To store different files)
  
  - Root User (superadmin)

  - Shell (A shell is an environment and interpreter for executing commands on a Linux system.)
    - bash (Bourne-again shell)
    - C shell
    - Z shell 

## 1.2 Linux File System
The Linux file system structure differs significantly from that of Windows. Unlike Windows, which organizes files under physical drives such as the C: drive, Linux employs a logical filesystem. At the top of this hierarchy is the root directory (/), which serves as the foundation of an inverted tree-like structure, as illustrated in the figure below.

![linux1](assets/posts/Linux/chapter1linux2024/linux-directory-structure.png)

- /bin (User Binaries)
  - Contains essential binary executables for system operation and user commands, such as `ls`, `cp`, and `cat`, which are available to all users.
  
- /sbin (System Binaries)
  - Stores administrative commands and system utilities, like `fsck`, `reboot`, and `iptables`, typically used by the root user.  
  
- /etc (Configuration Files)
  - Houses configuration files for system and application settings, such as `passwd`, `hosts`, and service configuration files.
 
- /dev (Device Files)
  - Contains special device files representing hardware and virtual devices, like /`dev/sda` for disks and `/dev/null` for the null device.

- /proc (Process Information)
  - A virtual filesystem providing real-time system information, including process details (e.g., `/proc/1` for process 1) and kernel parameters.

- /var (Variable Files)
  - Stores variable data that changes frequently during operation, such as logs (`/var/log`), mail, and cache files.

- /tmp (Temporary Files)
  - A space for temporary files created by programs. Files here are usually cleared upon reboot.
 
- /usr (User Programs)
  - Contains user-installed software, libraries, and documentation. It includes subdirectories like `/usr/bin` for binaries and `/usr/lib` for libraries.
   
- /home (Home Directories)
  - Holds personal directories for each user (e.g., `/home/user1`), where they can store their files, configurations, and documents.
   
- /boot (Boot Loader Files)
  - Contains files needed for the boot process, such as the kernel and boot loader configuration files (e.g., `grub.cfg`).
   
- /lib (System Libraries)
- Stores essential libraries required by binaries in `/bin` and `/sbin`, such as `libc.so.6`.

- /opt (Optional Applications)
  - Reserved for optional third-party applications and software packages that are not part of the default Linux distribution.

- /mnt (Mount Directory)
  - Provides a temporary mount point for filesystems, such as when mounting external drives or network shares.
   
- /media (Removable Devices)
  - Automatically mounts removable devices, like USB drives and CDs, under this directory.
   
- /srv (Service Data)
  - Stores data for services provided by the system, such as web server content or FTP files.


## 1.3 File and Direcory Operations Commands

### Listing Files and Directories

`ls` - List files and directories.
![ls](assets/posts/Linux/chapter1linux2024/ls.png)
   - -l: Long format listing
  
![ls-l](assets/posts/Linux/chapter1linux2024/ls-l.png)
   - -a: Include hidden files (starting with a dot `.`)
  ![ls-a](assets/posts/Linux/chapter1linux2024/ls-a.png)
   - -la: List files and directories in a detailed, long format including hidden files.
  ![ls-la](assets/posts/Linux/chapter1linux2024/ls-la.png) 
  
  In this example:
  - . represents the current directory.
  - .. represents the parent directory.
  - -rw-r--r-- shows the file permissions. (the first letter indicates whether it is a directory `d`, the remaining 9 chars indicate the read, write execute permission)
  - 1 is the number of hard links to the file.
  - kali kali shows the file's owner and group.
  - 4096 and 220 are the file sizes.
  - Dec 9 10:34 shows the last modification date and time.

### Change Directory 

- `cd /path/to/directory`: changes the current directory to the specified path
![cd](assets/posts/Linux/chapter1linux2024/cd.png)

### Print Current Working Directory
`pwd`: displays the current working directory

![pwd](assets/posts/Linux/chapter1linux2024/pwd.png)

### Create a New Directory

`mkdir` - Create a new directory

![mkdir](assets/posts/Linux/chapter1linux2024/mkdir.png)

### Remove Files and Directories

`rm`: deletes file

- `-r`: remove direcrories recursively
  - `rm -r` deletes the directory "directory_name" and its contents directly
  - `rmdir` cannot delete non-empty dir
  
- `-f`: force removal without confirmation
  - `rm -f file.txt` deletes the file `test.txt` without confirmation 
  
- `rm -rf`: remove directory and all of its contents without prompting for confirmation (irreversible!!)

### Copy Files and Directories

`cp`: copy file
- `cp filename.txt destination`: copies the file to the specified destination

- `cp -r directoryname destination`: copiest the directory and its contents to the specified destination

### Move/Rename Files and Directories

`mv`: move/rename files
- `mv file.txt new_name.txt`: renames the file "file.txt" to "new_name.txt".
- `mv file.txt directory`: moves the file "file.txt" to the specified directory

### Create an Empty File or Update File Timestamps

- `touch file.txt`: creates an empty file named "file.txt"

### View the Contents of a File

- `cat file.txt`: displays the contents of the file

### Displays the First/Last Few Lines of a File

- `head file.txt`: shows the first 10 lines of the file

- `n`: specifies the number of lines to display
  - `head -n 5 file.txt`: display the first 5 lines of the file

-`tail`: same as head just show the last 10 lines of the file

### Locate File Path
`locate filename`: shows all matched results in terms of file path

### Search for Files and Directories
`find /path/to/search -name "*.txt"`: searches for all files with the extension ".txt" in the specified directory

![find](assets/posts/Linux/chapter1linux2024/find.png)


## 1.4 File Permission Commands

| Command | Description                   | Options                                                                                                                                                                               | Examples                                                                                                           |
| ------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `chmod` | Change file permissions.      | `u`: User/owner permissions. <br> `g`: Group permissions. <br> `o`: Other permissions. <br> `+`: Add permissions. <br> `–`: Remove permissions. <br> `=`: Set permissions explicitly. | `chmod u+rwx file.txt` grants read, write, and execute permissions to the owner of the file.                       |
| `chown` | Change file ownership.        | N/A                                                                                                                                                                                   | `chown user file.txt` changes the owner of `file.txt` to the specified user.                                       |
| `chgrp` | Change group ownership.       | N/A                                                                                                                                                                                   | `chgrp group file.txt` changes the group ownership of `file.txt` to the specified group.                           |
| `umask` | Set default file permissions. | N/A                                                                                                                                                                                   | `umask 022` sets the default file permissions to read and write for the owner, and read-only for group and others. |

## 1.5 File Compression and Archiving Commands

| Command | Description                      | Options                                                                                                                                                                                                                         | Examples                                                                                                                                  |
| ------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `tar`   | Create or extract archive files. | `-c`: Create a new archive. <br> `-x`: Extract files from an archive. <br> `-f`: Specify the archive file name. <br> `-v`: Verbose mode. <br> `-z`: Compress the archive with gzip. <br> `-j`: Compress the archive with bzip2. | `tar -czvf archive.tar.gz files/` creates a compressed tar archive named `archive.tar.gz` containing the files in the `files/` directory. |
| `gzip`  | Compress files.                  | `-d`: Decompress files.                                                                                                                                                                                                         | `gzip file.txt` compresses the file `file.txt` and renames it as `file.txt.gz`.                                                           |
| `zip`   | Create compressed zip archives.  | `-r`: Recursively include directories.                                                                                                                                                                                          | `zip archive.zip file1.txt file2.txt` creates a zip archive named `archive.zip` containing `file1.txt` and `file2.txt`.                   |


## 1.6 Process Management Commands

| Command | Description                                                                                                      | Options                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Examples                                                                                                                                                                                                                                   |
| ------- | ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `ps`    | Display running processes.                                                                                       | `-aux`: Show all processes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | `ps aux` shows all running processes with detailed information.                                                                                                                                                                            |
| `top`   | Monitor system processes in real-time.                                                                           | None                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | `top` displays a dynamic view of system processes and their resource usage.                                                                                                                                                                |
| `kill`  | Terminate a process.                                                                                             | `-9`: Forcefully kill a process.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | `kill PID` terminates the process with the specified process ID.                                                                                                                                                                           |
| `pkill` | Terminate processes based on their name.                                                                         | None                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | `pkill process_name` terminates all processes with the specified name.                                                                                                                                                                     |
| `pgrep` | List processes based on their name.                                                                              | None                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | `pgrep process_name` lists all processes with the specified name.                                                                                                                                                                          |
| `grep`  | Used to search for specific patterns or regular expressions in text files or streams and display matching lines. | `-i`: Ignore case distinctions while searching. <br> `-v`: Invert the match, displaying non-matching lines. <br> `-r` or `-R`: Recursively search directories for matching patterns. <br> `-l`: Print only the names of files containing matches. <br> `-n`: Display line numbers alongside matching lines. <br> `-w`: Match whole words only, rather than partial matches. <br> `-c`: Count the number of matching lines instead of displaying them. <br> `-e`: Specify multiple patterns to search for. <br> `-A`: Display lines after the matching line. <br> `-B`: Display lines before the matching line. <br> `-C`: Display lines both before and after the matching line. | `grep -i “hello” file.txt` <br> `grep -v “error” file.txt` <br> `grep -r “pattern” directory/` <br> `grep -l “keyword” file.txt` <br> `grep -n “pattern” file.txt` In these examples we are extracting our desired output from `file.txt`. |

## 1.7 System Information Commands

| Command  | Description                        | Options                                                         | Examples                                                                |
| -------- | ---------------------------------- | --------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `uname`  | Print system information.          | `-a`: All system information.                                   | `uname -a` displays all system information.                             |
| `whoami` | Display current username.          | None                                                            | `whoami` shows the current username.                                    |
| `df`     | Show disk space usage.             | `-h`: Human-readable sizes.                                     | `df -h` displays disk space usage in a human-readable format.           |
| `du`     | Estimate file and directory sizes. | `-h`: Human-readable sizes. <br> `-s`: Display total size only. | `du -sh directory/` provides the total size of the specified directory. |
| `free`   | Display memory usage information.  | `-h`: Human-readable sizes.                                     | `free -h` displays memory usage in a human-readable format.             |
| `uptime` | Show system uptime.                | None                                                            | `uptime` shows the current system uptime.                               |
| `lscpu`  | Display CPU information.           | None                                                            | `lscpu` provides detailed CPU information.                              |
| `lspci`  | List PCI devices.                  | None                                                            | `lspci` lists PCI devices.                                              |
| `lsusb`  | List USB devices.                  | None                                                            | `lsusb` lists all connected USB devices.                                |

## 1.8 Networking Commands

| Command    | Description                                 | Examples                                                                                                   |
| ---------- | ------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `ifconfig` | Display network interface information.      | `ifconfig` shows the details of all network interfaces.                                                    |
| `ping`     | Send ICMP echo requests to a host.          | `ping google.com` sends ICMP echo requests to “google.com” to check connectivity.                          |
| `netstat`  | Display network connections and statistics. | `netstat -tuln` shows all listening TCP and UDP connections.                                               |
| `ss`       | Display network socket information.         | `ss -tuln` shows all listening TCP and UDP connections.                                                    |
| `ssh`      | Securely connect to a remote server.        | `ssh user@hostname` initiates an SSH connection to the specified hostname.                                 |
| `scp`      | Securely copy files between hosts.          | `scp file.txt user@hostname:/path/to/destination` securely copies “file.txt” to the specified remote host. |
| `wget`     | Download files from the web.                | `wget http://example.com/file.txt` downloads “file.txt” from the specified URL.                            |
| `curl`     | Transfer data to or from a server.          | `curl http://example.com` retrieves the content of a webpage from the specified URL.                       |



## 1.9 IO Redirection Commands

| Command           | Description                                                    | Examples                                                                               |
| ----------------- | -------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| `cmd < file`      | Input of `cmd` is taken from `file`.                           | `cmd < file` takes the input for `cmd` from `file`.                                    |
| `cmd > file`      | Standard output (stdout) of `cmd` is redirected to `file`.     | `cmd > file` redirects the standard output of `cmd` to `file`.                         |
| `cmd 2> file`     | Error output (stderr) of `cmd` is redirected to `file`.        | `cmd 2> file` redirects the error output of `cmd` to `file`.                           |
| `cmd 2>&1`        | Stderr is redirected to the same place as stdout.              | `cmd 2>&1` redirects both stderr and stdout to the same location.                      |
| `cmd1 <(cmd2)`    | Output of `cmd2` is used as the input file for `cmd1`.         | `cmd1 <(cmd2)` runs `cmd2` and passes its output to `cmd1` as if it were a file.       |
| `cmd > /dev/null` | Discards the stdout of `cmd` by sending it to the null device. | `cmd > /dev/null` sends the output of `cmd` to `/dev/null`, effectively discarding it. |
| `cmd &> file`     | Every output of `cmd` is redirected to `file`.                 | `cmd &> file` redirects both stdout and stderr of `cmd` to `file`.                     |
| `cmd 1>&2`        | Stdout is redirected to the same place as stderr.              | `cmd 1>&2` redirects stdout to the same location as stderr.                            |
| `cmd >> file`     | Appends the stdout of `cmd` to `file`.                         | `cmd >> file` appends the standard output of `cmd` to `file`.                          |

## 1.10 Environment Variable Commands

| Command                      | Description                                                       | Examples                                                                                    |
| ---------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `export VARIABLE_NAME=value` | Sets the value of an environment variable.                        | `export PATH=/usr/local/bin` sets the `PATH` environment variable to `/usr/local/bin`.      |
| `echo $VARIABLE_NAME`        | Displays the value of a specific environment variable.            | `echo $PATH` displays the value of the `PATH` environment variable.                         |
| `env`                        | Lists all environment variables currently set in the system.      | `env` lists all the environment variables along with their current values.                  |
| `unset VARIABLE_NAME`        | Unsets or removes an environment variable.                        | `unset PATH` removes the `PATH` environment variable.                                       |
| `export -p`                  | Shows a list of all currently exported environment variables.     | `export -p` lists all environment variables that have been exported in the current session. |
| `env VAR1=value COMMAND`     | Sets the value of an environment variable for a specific command. | `env VAR1=value ls` runs the `ls` command with `VAR1=value` as an environment variable.     |
| `printenv`                   | Displays the values of all environment variables.                 | `printenv` displays all environment variables in the current environment.                   |

## 1.11 User Management Commands

| Command                                 | Description                                                                                                                                                       | Examples                                                                                                                  |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `who`                                   | Shows who is currently logged in.                                                                                                                                 | `who` displays the list of users currently logged into the system.                                                        |
| `sudo adduser username`                 | Creates a new user account on the system with the specified username.                                                                                             | `sudo adduser john` creates a new user account for "john" on the system.                                                  |
| `finger`                                | Displays information about all the users currently logged into the system, including their usernames, login time, and terminal.                                   | `finger` provides information about all users currently logged in, including usernames and login times.                   |
| `sudo deluser USER GROUPNAME`           | Removes the specified user from the specified group.                                                                                                              | `sudo deluser john users` removes "john" from the "users" group.                                                          |
| `last`                                  | Shows the recent login history of users.                                                                                                                          | `last` shows the login history, including the time, duration, and the terminal used.                                      |
| `finger username`                       | Provides information about the specified user, including their username, real name, terminal, idle time, and login time.                                          | `finger john` displays detailed information about the user "john", such as their real name, idle time, and login details. |
| `sudo userdel -r username`              | Deletes the specified user account from the system, including their home directory and associated files. The `-r` option ensures the removal of the user’s files. | `sudo userdel -r john` deletes the "john" user and their home directory.                                                  |
| `sudo passwd -l username`               | Locks the password of the specified user account, preventing the user from logging in.                                                                            | `sudo passwd -l john` locks the password of the user "john".                                                              |
| `su – username`                         | Switches to another user account with the user’s environment.                                                                                                     | `su - john` switches to the user "john" with their environment.                                                           |
| `sudo usermod -a -G GROUPNAME USERNAME` | Adds an existing user to the specified group. The user is added to the group without removing them from their current groups.                                     | `sudo usermod -a -G admins john` adds "john" to the "admins" group without removing them from other groups.               |


## 1.12 Shortcuts Commands

### 1.12.1 Bash Shortcuts Commands

| Navigation | Description                        | Editing    | Description                                                       | History    | Description                              |
| ---------- | ---------------------------------- | ---------- | ----------------------------------------------------------------- | ---------- | ---------------------------------------- |
| `Ctrl + A` | Move to the beginning of the line. | `Ctrl + U` | Cut/delete from the cursor position to the beginning of the line. | `Ctrl + R` | Search command history (reverse search). |
| `Ctrl + E` | Move to the end of the line.       | `Ctrl + K` | Cut/delete from the cursor position to the end of the line.       | `Ctrl + G` | Escape from history search mode.         |
| `Ctrl + B` | Move back one character.           | `Ctrl + W` | Cut/delete the word before the cursor.                            | `Ctrl + P` | Go to the previous command in history.   |
| `Ctrl + F` | Move forward one character.        | `Ctrl + Y` | Paste the last cut text.                                          | `Ctrl + N` | Go to the next command in history.       |
| `Alt + B`  | Move back one word.                | `Ctrl + L` | Clear the screen.                                                 | `Ctrl + C` | Terminate the current command.           |
| `Alt + F`  | Move forward one word.             |            |                                                                   |            |                                          |

### 1.12.2 Nano Shortcuts Commands

| File Operations | Description                             | Navigation | Description                              | Editing    | Description                                                 | Search and Replace | Description                              |
| --------------- | --------------------------------------- | ---------- | ---------------------------------------- | ---------- | ----------------------------------------------------------- | ------------------ | ---------------------------------------- |
| `Ctrl + O`      | Save the file.                          | `Ctrl + Y` | Scroll up one page.                      | `Ctrl + K` | Cut/delete from the cursor position to the end of the line. | `Ctrl + W`         | Search for a string in the text.         |
| `Ctrl + X`      | Exit Nano (prompt to save if modified). | `Ctrl + V` | Scroll down one page.                    | `Ctrl + U` | Uncut/restore the last cut text.                            | `Alt + W`          | Search and replace a string in the text. |
| `Ctrl + R`      | Read a file into the current buffer.    | `Alt + \`  | Go to a specific line number.            | `Ctrl + 6` | Mark a block of text for copying or cutting.                | `Alt + R`          | Repeat the last search.                  |
| `Ctrl + J`      | Justify the current paragraph.          | `Alt + ,`  | Go to the beginning of the current line. | `Ctrl + K` | Cut/delete the marked block of text.                        |                    |                                          |
|                 |                                         | `Alt + .`  | Go to the end of the current line.       | `Alt + 6`  | Copy the marked block of text.                              |                    |                                          |

### 1.12.3 VI Shortcuts Commands

| Command | Description                                                                                                           |
| ------- | --------------------------------------------------------------------------------------------------------------------- |
| `cw`    | Change the current word. Deletes from the cursor position to the end of the current word and switches to insert mode. |
| `dd`    | Delete the current line.                                                                                              |
| `x`     | Delete the character under the cursor.                                                                                |
| `R`     | Enter replace mode. Overwrites characters starting from the cursor position until you press the Escape key.           |
| `o`     | Insert a new line below the current line and switch to insert mode.                                                   |
| `u`     | Undo the last change.                                                                                                 |
| `s`     | Substitute the character under the cursor and switch to insert mode.                                                  |
| `dw`    | Delete from the cursor position to the beginning of the next word.                                                    |
| `D`     | Delete from the cursor position to the end of the line.                                                               |
| `4dw`   | Delete the next four words from the cursor position.                                                                  |
| `A`     | Switch to insert mode at the end of the current line.                                                                 |
| `S`     | Delete the current line and switch to insert mode.                                                                    |
| `r`     | Replace the character under the cursor with a new character entered from the keyboard.                                |
| `i`     | Switch to insert mode before the cursor.                                                                              |
| `3dd`   | Delete the current line and the two lines below it.                                                                   |
| `ESC`   | Exit from insert or command-line mode and return to command mode.                                                     |
| `U`     | Restore the current line to its original state before any changes were made.                                          |
| `~`     | Switch the case of the character under the cursor.                                                                    |
| `a`     | Switch to insert mode after the cursor.                                                                               |
| `C`     | Delete from the cursor position to the end of the line and switch to insert mode.                                     |

### 1.12.4 Vim Shortcuts Commands

| Normal Mode | Description                                              | Command Mode               | Description                                              | Visual Mode | Description                       |
| ----------- | -------------------------------------------------------- | -------------------------- | -------------------------------------------------------- | ----------- | --------------------------------- |
| `i`         | Enter insert mode at the current cursor position.        | `:w`                       | Save the file.                                           | `v`         | Enter visual mode to select text. |
| `x`         | Delete the character under the cursor.                   | `:q`                       | Quit Vim.                                                | `y`         | Copy the selected text.           |
| `dd`        | Delete the current line.                                 | `:q!`                      | Quit Vim without saving changes.                         | `d`         | Delete the selected text.         |
| `yy`        | Copy the current line.                                   | `:wq` or `:x`              | Save and quit Vim.                                       | `p`         | Paste the copied or deleted text. |
| `p`         | Paste the copied or deleted text below the current line. | `:s/old/new/g`             | Replace all occurrences of “old” with “new” in the file. |             |                                   |
| `u`         | Undo the last change.                                    | `:set nu` or `:set number` | Display line numbers.                                    |             |                                   |
| `Ctrl + R`  | Redo the last undo.                                      |                            |                                                          |             |                                   |
