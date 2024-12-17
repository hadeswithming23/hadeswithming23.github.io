---
title: Bash
date: 2024-12-13 23:50:00 +0800
categories: [Linux]
tags: [linux, knowledge]
---

# 8.0 Bash (Bourne Again Shell)
Bash is the default command-line shell on most Linux distributions. It is an enhanced version of the original Bourne shell (sh). It provides improved scripting capabilities, command-line editing, and job control.

## 8.1 First Bash Program: Hello World
**Step 1: Open a Text Editor**
- Use any text editor to create the script. Common choices:
  - Nano: nano script_name.sh
  - Vim: vim script_name.sh
  - Gedit: gedit script_name.sh

**Step 2: Add the Shebang Line**
```bash
#!/bin/bash
```
- #!/bin/bash: Use Bash shell.
- #!/bin/zsh: Use Zsh shell.
- #!/usr/bin/env bash: Dynamic interpreter lookup.

**Step 3: Write Your Commands**
- Add the commands you want to execute. Example:
```bash
#!/bin/bash
echo "Hello, World!"
current_date=$(date)
echo "The current date is: $current_date"
```

**Step 4: Save the File**
- Save the file with a .sh extension, e.g., my_script.sh.

**Step 5: Make the Script Executable**
- Grant execute permissions to the script using chmod:
```bash
chmod +x script_name.sh
```

**Step 6: Run the Script**
- Execute the script by specifying its path:
```bash
./script_name.sh
```
- If the script is in a directory included in your PATH, you can run it without ./

## 8.2 Read Input From User 

**Example Bash Script**
This script will:
1. Prompt the user to input their name.
2. Ask for their favorite programming language.
3. Print a customized message based on the inputs.

```bash
#!/bin/bash

# Prompt user for their name
echo "What is your name?"
read name

# Prompt user for their favorite programming language
echo "Hello, $name! What is your favorite programming language?"
read language

# Display the personalized message
echo "Great choice, $name! $language is an excellent programming language."

# End of script
```

**Example Workflow**

![read](assets/posts/chapter8linux2024/read.png)


## 8.3 Script to Scan Open Ports Using Nmap
**Nmap (Network Mapper)** is an open-source tool used for network discovery, security auditing, and port scanning. It helps administrators and security professionals understand the devices and services running on a network.

**Nmap Syntax**:
`nmap <target of scan> <target IP> <optionally, target port>`

**Basic Nmap Commands**

| **Command**                            | **Description**                                          |
| -------------------------------------- | -------------------------------------------------------- |
| `nmap <target>`                        | Basic scan to check open ports on the target.            |
| `nmap -sS <target>`                    | SYN scan (stealthier and faster).                        |
| `nmap -sT <target>`                    | TCP connect scan (requires no root privileges).          |
| `nmap -O <target>`                     | Detect the operating system of the target.               |
| `nmap -sV <target>`                    | Detect versions of services running on open ports.       |
| `nmap -A <target>`                     | Perform OS detection, version detection, and traceroute. |
| `nmap -Pn <target>`                    | Skip host discovery; assumes host is up.                 |
| `nmap -p <port_range> <target>`        | Scan specific ports (e.g., `nmap -p 22,80 192.168.1.1`). |
| `nmap -T<0-5> <target>`                | Set timing template (0 for slowest, 5 for fastest).      |
| `nmap -v <target>`                     | Enable verbose output for detailed scan information.     |
| `nmap --script <script_name> <target>` | Run a specific NSE script for vulnerabilities.           |
| `nmap --top-ports <number> <target>`   | Scan the top `<number>` most common ports.               |


8.3.1 Simple Bash script for scanning a target for MySQL services running on port 3306 using nmap

```bash
#!/bin/bash

# Target IP or hostname
TARGET="192.168.1.100"

# Check if nmap is installed
if ! command -v nmap &> /dev/null
then
    echo "nmap could not be found, please install it."
    exit 1
fi

# Basic port scan for MySQL (port 3306)
echo "Scanning for MySQL service on port 3306..."
nmap -p 3306 $TARGET

# Detect MySQL version
echo "Detecting MySQL version..."
nmap -sV -p 3306 $TARGET

# Aggressive scan for detailed information
echo "Performing aggressive scan for detailed information..."
nmap -A -p 3306 $TARGET

# Running MySQL-specific NSE scripts
echo "Running MySQL-specific NSE scripts for vulnerabilities..."
nmap --script mysql* -p 3306 $TARGET

# End of script
echo "MySQL scan completed."
```


8.3.2 Advanced Bash script for scanning a target for MySQL services running on port 3306 using nmap

```bash
#!/bin/bash

# Function to scan a range of IP addresses for a specific port
scan_ports() {
    local base_ip=$1
    local start_octet=$2
    local end_octet=$3
    local port=$4

    echo "Scanning IP range $base_ip.$start_octet to $base_ip.$end_octet for port $port..."

    # Loop through the IP addresses
    for ip in $(seq $start_octet $end_octet); do
        nmap -p $port $base_ip.$ip | grep "open"
    done
}

# Input for base IP address
echo -n "Enter the base IP (e.g., 192.168.1): "
read base_ip

# Starting last octet of the IP range
echo -n "Enter the starting last octet (e.g., 50): "
read start_octet

# Ending last octet of the IP range
echo -n "Enter the ending last octet (e.g., 100): "
read end_octet

# Single port number
echo -n "Enter the port number to scan (e.g., 3306): "
read port

# Scan IPs and ports
scan_ports $base_ip $start_octet $end_octet $port

echo "Scan completed for IP range $base_ip.$start_octet-$end_octet on port $port."
```

## 8.4 Common Bash Script Commands

| **Command**                        | **Description**                                                                                |
| ---------------------------------- | ---------------------------------------------------------------------------------------------- |
| `readonly <variable>`              | Marks a variable as read-only, preventing its modification.                                    |
| `eval <expression>`                | Evaluates the given expression as if it were typed in a new shell.                             |
| `exec <command>`                   | Terminates the current shell and starts a new one running the specified command.               |
| `exit <status>`                    | Exits the script with an optional exit status.                                                 |
| `export <variable>`                | Exports a variable to the environment, making it accessible to child processes.                |
| `getopts <options> <args>`         | Parses options and arguments passed to the script.                                             |
| `set <options>`                    | Sets or resets positional parameters to the specified values.                                  |
| `shift`                            | Shifts positional parameters to the left by one.                                               |
| `test <expression>`                | Evaluates a conditional expression.                                                            |
| `true`                             | Always returns true (exit status 0).                                                           |
| `false`                            | Always returns false (exit status 1).                                                          |
| `trap <command>`                   | Catches and executes a command when a signal is received.                                      |
| `wait <pid>`                       | Waits for a process with the specified process ID (`pid`) to complete execution.               |
| `if <condition>`                   | Conditionally executes commands if the condition is true.                                      |
| `else`                             | Specifies a block of commands if the `if` condition fails.                                     |
| `fi`                               | Ends an `if` block.                                                                            |
| `while <condition>`                | Repeats commands while the condition evaluates to true.                                        |
| `done`                             | Ends a `while` loop.                                                                           |
| `for <variable> in <list>`         | Iterates over a list, executing commands for each item.                                        |
| `do`                               | Begins a block of commands for a `for` loop.                                                   |
| `done`                             | Ends a `for` loop.                                                                             |
| `case <variable> in`               | Matches a variable against multiple patterns and executes the corresponding block of commands. |
| `esac`                             | Ends a `case` block.                                                                           |
| `mkdir <directory>`                | Creates a new directory `<directory>`.                                                         |
| `rm <file>`                        | Removes a file `<file>`.                                                                       |
| `cp <source> <destination>`        | Copies a file or directory from `<source>` to `<destination>`.                                 |
| `mv <source> <destination>`        | Moves or renames a file or directory.                                                          |
| `chmod <mode> <file>`              | Changes the permissions of a file or directory.                                                |
| `tar -xvzf <file>.tar.gz`          | Extracts a `.tar.gz` archive.                                                                  |
| `zip <file>.zip <file>`            | Compresses `<file>` into a `.zip` archive.                                                     |
| `echo <text>`                      | Prints `<text>` to the terminal.                                                               |
| `read <variable>`                  | Reads input from the user and assigns it to `<variable>`.                                      |
| `ps`                               | Lists currently running processes.                                                             |
| `kill <pid>`                       | Sends a termination signal to a process with process ID `<pid>`.                               |
| `grep <pattern> <file>`            | Searches for `<pattern>` in `<file>`.                                                          |
| `find <directory> -name <pattern>` | Searches for files matching `<pattern>` within `<directory>`.                                  |
| `awk <script>`                     | Processes text using Awk with a specified script.                                              |
| `sed <script>`                     | Stream editor for text manipulation.                                                           |
| `alias <name>='<command>'`         | Creates a custom command alias.                                                                |
| `which <command>`                  | Displays the full path of a command.                                                           |

