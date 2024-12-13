---
title: User Environment Variable Management
date: 2024-12-13 21:52:00 +0800
categories: [Linux]
tags: [linux, knowledge]
---

# 7.0 User Environment Variable Management in Linux

**Overview**
Environment variables are dynamic values in Linux that affect the behavior of processes and applications. They store information like user preferences, system paths, and configuration details.

**Common Environment Variables**
- **`PATH`**: Directories to search for executable files.
- **`HOME`**: Path to the user's home directory.
- **`USER`**: The currently logged-in user's name.
- **`SHELL`**: The default shell for the user.
- **`EDITOR`**: Default text editor for the user.
- **`LANG`**: System language and localization settings.

## 7.1 View and Modify Environment Variables
1. **List All Variables**:
  ```bash
  printenv
  # or using env
  env
  ``` 
  - Use `printenv` to view environment variables and their values.
  - Use `env` to display all variables or run a command in a modified environment.

### 7.1.1 Checking All Environment Variables Using `set`
The `set` command in Linux is used to display and modify shell settings, functions, and environment variables. Unlike `env` or `printenv`, it shows **all shell variables**, including environment variables and shell-specific variables.

- **Command**:
  ```bash
  set
  ```
- **Output**:
  - Displays a comprehensive list of:
    - Environment variables (exported to child processes).
    - Shell variables (local to the shell session).
    - Shell functions.

2. **Display a Specific Vaariable**:
  ```bash
  echo $VARIABLE_NAME
  ```

### 7.1.2 Setting Environment Variables
1. Temporarily (for the current session)

  ```bash
  export VARIABLE_NAME=value
  # or directly type 
  VARIABLE_NAME=value
  ```
  
2. Permanently (persist across sessions):
- Add the variable to one of the following configuration files:
  - use `echo $SHELL` to check which shell is using 
  - ~/.bashrc or ~/.bash_profile (for Bash shell).
  - ~/.zshrc (for Zsh shell).
  - Example:
    ```bash
    echo 'export EDITOR=vim' >> ~/.bashrc
    source ~/.bashrc
    ```

### 7.1.3 Unsetting Environment Variables
- Remove a variable temporarily:
```bash
unset VARIABLE_NAME
```

### 7.1.4 Modifying `PATH`
1. Add a Directory to `PATH` Temporarily:
```bash
export PATH=$PATH:/new/directory
```

2. Add a Directory to PATH Permanently:
```bash
echo 'export PATH=$PATH:/new/directory' >> ~/.bashrc
source ~/.bashrc
```

> Bear in mind, 
Directly typing `PATH=/root/mydirectory` in your terminal will overwrite the current `PATH` environment variable, causing significant issues with command execution. 
{: .prompt-warning }

