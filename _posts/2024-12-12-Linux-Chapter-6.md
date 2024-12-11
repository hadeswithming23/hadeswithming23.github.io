---
title: Process Management
date: 2024-12-12 02:33:00 +0800
categories: [Linux]
tags: [knowledge, linux]
---

# 6.0 Process Management in Linux
**What is a Process?**
- A **process** is a running instance of a program.
- It includes the program code, its current activity, resources like open files, and memory usage.
- Every process in Linux has a **unique Process ID (PID)**.

## 6.1 Types of Processes
1. **Foreground Processes**: 
   - Run in the foreground and take input from the user.
   - Example: Commands like `vim`, `cat`.
2. **Background Processes**:
   - Run in the background without user interaction.
   - Example: Services or daemons like `ssh`, `cron`.

## 6.2 Key Concepts in Process Management
- **Parent and Child Processes**:
  - A parent process spawns child processes using system calls like `fork()`.
  - The **init** process (PID 1) is the ancestor of all processes.
- **States of a Process**:
  1. **Running**: Actively executing.
  2. **Sleeping**: Waiting for an event or resource.
  3. **Stopped**: Halted, usually by a signal.
  4. **Zombie**: Completed execution but waiting for the parent process to read its exit status.

## 6.3 Viewing Processes
- `ps`: Displays running processes.

 ![ps](assets/posts/chapter6linux2024/ps.png)

  - Example: `ps aux` shows all processes with detailed info.
  ![psaux](assets/posts/chapter6linux2024/psaux.png)

  **Command Breakdown**:
  - `ps`: Process status.
  - `a`: Displays processes for all users.
  - `u`: Shows user-oriented format.
  - `x`: Includes processes without a terminal.
  
  **Columns Descriptions**:
  - `USER`: Owner of the process.
  - `PID`: Unique Process ID.
  - `%CPU` and `%MEM`: CPU and memory usage, respectively.
  - `STAT`: Process state (e.g., running, sleeping, idle).
    - `R`: Running.
    - `S`: Sleeping.
    - `I`: Idle.
    - `<`: High priority.
    - `N`: Low priority.
    - `T`: Stopped (e.g., by a signal or during debugging).
    - `Z`: Zombie process.
  - `VSZ`: Virtual memory size used by the process (in kilobytes).
  - `RSS`: Resident Set Size - the non-swapped physical memory used by the process (in kilobytes)
  - `TTY`: The terminal associated with the process. If the process is not attached to a terminal, it shows ?.
  - `START`: The time when the process started.
  - `TIME`: The total CPU time consumed by the process.
  - `COMMAND`: The command used to start the process.

  **Common Processes**:
    - `init`: The first system process (PID 1).
    - `kworker`: Handles kernel-related background tasks.
    - `sshd`, `nginx`, etc.: Services managed by the system.

**Real Time Monitoring**
- `top`: Interactive view of system processes and resource usage.
- `htop`: Similar to `top`, but more user-friendly.


## 6.4 Controlling Processes
- `kill`: Sends a signal to terminate a process.
  - Example: `kill -9 <PID>` forcibly kills a process.
- `pkill`: Kills processes by name.
  - Example: `pkill firefox`.
- `killall`: Kills processes by name too.
  - Example: `killall firefox` or `killall -I firefox` (ignore case while matching)
   
**Key Differences**

| Feature           | `pkill`                                        | `killall`                                        |
| ----------------- | ---------------------------------------------- | ------------------------------------------------ |
| **Name Matching** | Matches **partial names**                      | Matches **exact names**                          |
| **Scope**         | Can target based on user, session, or terminal | Targets all processes with exact names           |
| **Use Case**      | Flexible targeting                             | Bulk termination of processes with the same name |

- in `top`, type `k` to kill a process through providing the PID
- `jobs`: Lists background jobs for the current session.
- `fg`: Brings a background job to the foreground.
- `bg`: Sends a job to the background.

## 6.5 Starting and Managing Processes
- `&`: Starts a process in the background.
  - Example: `sleep 100 &`.
- `nice` and `renice`: Adjust the priority of a process.
  - Example: 
    - `nice -n 10 /bin/slowprocess` runs a command with a lower priority.
    - `renice 19 6996` runs a command command with lowest priority.

| Feature        | `nice`                              | `renice`                                     |
| -------------- | ----------------------------------- | -------------------------------------------- |
| **Purpose**    | Sets priority for a **new process** | Modifies priority of an **existing process** |
| **Scope**      | Works only at process creation      | Targets already running processes            |
| **Target**     | Command/program                     | Process by PID, user, or group               |
| **Permission** | Requires `sudo` for higher priority | Requires `sudo` for increasing priority      |


## 6.6 Process Scheduling
- The Linux kernel uses a **scheduler** to allocate CPU time to processes.
- Scheduling classes:
  - **CFS (Completely Fair Scheduler)**: Default for most processes.
  - **Real-Time Scheduling**: For high-priority tasks.
- Priorities range:
  ![priority](assets/posts/chapter6linux2024/priority.png)
  - `-20` (highest priority) to `19` (lowest priority).

## 6.7 Signals in Process Management
- Signals are used to communicate with processes.
  - Example signals:
    - `SIGTERM` (15): Terminate gracefully.
    - `SIGKILL` (9): Forcefully terminate.
    - `SIGHUP` (1): Restart a process.
- Use `kill -l` to list all signals.

## 6.8 Tools for Advanced Process Management
- `strace`: Traces system calls of a process.
- `lsof`: Lists open files for a process.
- `systemctl`: Manages system services and daemons.
