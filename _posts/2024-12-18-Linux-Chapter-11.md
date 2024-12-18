---
title: Log System
date: 2024-12-18 23:25:30 +0800
categories: [Linux]
tags: [linux, knowledge]
---

# 11.0 Log System in Linux
The Linux log system is essential for recording system activities, debugging issues, and auditing events. It provides insights into system performance, errors, and security-related activities.


## 11.1 rsyslog
- **`rsyslog`** is a powerful and versatile logging daemon in Linux, used to collect and forward log messages.
- It is configured through the file `/etc/rsyslog.conf` and additional configuration files in `/etc/rsyslog.d/`.

**Key Features of rsyslog**:
- Supports remote logging.
- Provides filtering and templating for log messages.
- High performance for handling a large volume of logs.

**Common Commands**:
- Restart rsyslog service:
  ```bash
  sudo systemctl restart rsyslog
  ```
- View logs collected by rsyslog:
  ```bash
  less /var/log/syslog
  ```

### 11.1.1 rsyslog Configuration File
The **rsyslog** daemon in Linux uses configuration files to define how logs are collected, processed, and forwarded. These configuration files allow administrators to customize logging behavior for various system components.

### 11.1.2 Main Configuration File
- The main configuration file for rsyslog is **`/etc/rsyslog.conf`**.
- Additional configuration files can be found in the **`/etc/rsyslog.d/`** directory.

**Structure of `/etc/rsyslog.conf`**:

1. **Modules Section**:
   - Enables specific modules for functionality like remote logging or message parsing.
   - Example:
  
    ![rsyslog_conf](assets/posts/Linux/chapter11linux2024/modules.png)


2. **Global Directives**:
   - Configure global settings for rsyslog.
   - Example:
  
      ![rsyslog_conf](assets/posts/Linux/chapter11linux2024/global_directives.png)


3. **Rules Section**:
   - Defines filters and actions for log messages.
   - Example:
  
    ![rsyslog_conf](assets/posts/Linux/chapter11linux2024/rules.png)
 
## 11.2 Filters

**Filters**:
- Filters determine which log messages are processed based on their facility and severity.

### 11.2.1 Facilities
Facilities in syslogs are used to categorize log messages based on their sources or purposes. They provide a way to differentiate between various components of a Linux system

![facility](assets/posts/Linux/chapter11linux2024/facility.png)

### 11.2.2 Levels
Syslog levels indicate the severity or importance of log messages. They help prioritize and filter log entries based on their significance.

![level](assets/posts/Linux/chapter11linux2024/levels.png)

- Emergency will be the highest priority
- The log will be taken same as the level or higher only
- if put `*`, all messages for each level will be recorded


## 11.3 Use `logrotate` to Automatically Manage the Logs
**Logrotate** is a system utility in Linux designed to manage the growth of log files. It automates the rotation, compression, and deletion of log files to ensure that log files do not consume excessive disk space and remain manageable.


### 11.3.1 Features of Logrotate

- Automatically rotates log files based on size, time, or specific criteria.
- Compresses old log files to save space (e.g., gzip or bzip2).
- Removes or archives logs after a certain number of rotations.
- Allows custom post-rotation actions, like restarting services.
- Configurable on a system-wide and per-application basis.


### 11.3.2 Configuration Files

**Global Configuration**
  - Located at **`/etc/logrotate.conf`**.
  - Defines default behavior for all logs unless overridden by specific configurations.
  
**Per-Application Configuration**
  - Individual configuration files are stored in **`/etc/logrotate.d/`**.
  - Applications like Apache or MySQL may have their own logrotate files.

### 11.3.3 Common Configuration Directives

| **Directive**            | **Description**                                |
| ------------------------ | ---------------------------------------------- |
| **daily/weekly/monthly** | Specifies the frequency of rotation.           |
| **rotate [count]**       | Number of log rotations to keep.               |
| **size [value]**         | Rotates logs when they exceed a specific size. |
| **compress**             | Compresses logs after rotation.                |
| **delaycompress**        | Delays compression for one rotation cycle.     |
| **missingok**            | Ignores errors if the log file is missing.     |
| **notifempty**           | Skips rotation for empty logs.                 |
| **postrotate/endscript** | Executes commands after rotation.              |

Example `/etc/logrotate.conf`:
```plaintext
/var/log/syslog {
    daily
    rotate 7
    compress
    missingok
    notifempty
    postrotate
        /usr/bin/systemctl reload rsyslog > /dev/null
    endscript
}
```

![logrotate](assets/posts/Linux/chapter11linux2024/logrotate.png)


## 11.4 Keep Anonymous
Keeping anonymous while performing pentesting in Linux is crucial to protect your identity and prevent detection.

### 11.4.1 Shred Command in Linux
The **`shred`** command is a Linux utility used to securely delete files by overwriting their content multiple times, making it difficult to recover the data.

**Common Options**

| **Option** | **Description**                                   |
| ---------- | ------------------------------------------------- |
| `-u`       | Remove the file after overwriting it.             |
| `-n [N]`   | Overwrite the file N times (default is 3).        |
| `-z`       | Add a final overwrite with zeros for concealment. |
| `-v`       | Show verbose output while shreddi                 |


**Features of Shred**
- Overwrites file content multiple times with random data.
- Can delete the file after overwriting.
- Adds a final overwrite with zeros for concealment.

**Limitations**
- Effective only for traditional HDDs.
- Not reliable for SSDs or flash storage due to wear leveling.
- May not securely delete files on journaled file systems (e.g., ext3, ext4) if the data is logged elsewhere.


### 11.4.2 Managing the Rsyslog Service

The `rsyslog` service manages system logs in Linux. It can be stopped, restarted, or configured for maintenance.

**Stop the Service**
To stop the `rsyslog` service:
```bash
sudo systemctl stop rsyslog
```
**Common Options**

| **Option** | **Description**                                      |
| ---------- | ---------------------------------------------------- |
| `start`    | Start the service.                                   |
| `stop`     | Stop the service.                                    |
| `restart`  | Restart the service.                                 |
| `status`   | Check the current status of the service.             |
| `enable`   | Enable the service to start on boot.                 |
| `disable`  | Disable the service from starting on boot.           |
| `reload`   | Reload the service configuration without restarting. |
| `status`   | Display the service status.                          |
