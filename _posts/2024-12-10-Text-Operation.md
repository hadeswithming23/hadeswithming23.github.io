---
title: Text Operation in Linux
time: 2024-12-10 01:47:00
categories: [Linux]
tags: [knowledge, linux]
---

This section uses some of the files in the Network Intrusion Detection System (NIDS) Snort. 

> If you are using Kali Linux without the snort system installed, please type `sudo apt-get install snort` to download it
{: .prompt-info }

## 2.1 Check The File Contents
`cat /etc/snort/snort.lua`: The new version of Snort 3.0 uses snort.lua instead of snort.conf

![cat_snort.lua](assets/posts/chapter2linux2024/catsnortlua.png)

### 2.1.1 Getting the Header of the File
`head /etc/snort/snort.lua`: The first 10 lines of the snort.lua file

![head_snort.lua](assets/posts/chapter2linux2024/headsnortlua.png)

### 2.1.2 Getting the End of the File
`tail /etc/snort/snort.lua`: The last 10 lines of the snort.lua file

![tail_snort.lua](assets/posts/chapter2linux2024/tailsnortlua.png)

### 2.1.3 Mark the Line Number
`nl /etc/snort/snort.lua`: Number the lines of a file and display the content with the added line numbers.

![nl_snort.lua](assets/posts/chapter2linux2024/nlsnortlua.png)


## 2.2 Filter the Contents Using Command 'grep'
`nl /etc/snort/snort.lua | grep log`:Show the number line and filter the word that matches log

![grep_snort.lua](assets/posts/chapter2linux2024/grepsnortlua.png)

## 2.3 Find and Replace With the 'sed' Command

The `sed` command (**Stream Editor**) is a powerful tool for processing and transforming text streams or files. It supports operations like search-and-replace, insertion, deletion, and line filtering.

### 2.3.2 Common Operation

| **Operation**            | **Command**                                  | **Description**                                     |
| ------------------------ | -------------------------------------------- | --------------------------------------------------- |
| **Substitution** (`s`)   | `sed 's/old/new/' file.txt`                  | Replace first occurrence of `old` with `new`.       |
|                          | `sed 's/old/new/g' file.txt`                 | Replace all occurrences of `old` with `new`.        |
| **Edit In-Place**        | `sed -i 's/old/new/g' file.txt`              | Edit file directly without printing to output.      |
| **Delete Lines** (`d`)   | `sed '/pattern/d' file.txt`                  | Delete lines matching `pattern`.                    |
|                          | `sed '3d' file.txt`                          | Delete the 3rd line.                                |
| **Insert Lines** (`i`)   | `sed '3i\This is a new line' file.txt`       | Insert "This is a new line" **before** line 3.      |
| **Append Lines** (`a`)   | `sed '3a\This is an appended line' file.txt` | Append "This is an appended line" **after** line 3. |
| **Replace in Specific**  | `sed '2,4s/old/new/' file.txt`               | Replace `old` with `new` in lines 2 to 4.           |
| **Print Matching Lines** | `sed -n '/pattern/p' file.txt`               | Print only lines matching `pattern`.                |
| **Remove Blank Lines**   | `sed '/^$/d' file.txt`                       | Remove all empty lines.                             |
| **Change Delimiters**    | `sed 's/,/                                   | /g' file.txt`                                       | Replace commas with pipes (` | `). |

### 2.3.3 Advanced Features

| **Feature**             | **Command**                                    | **Description**                                       |
| ----------------------- | ---------------------------------------------- | ----------------------------------------------------- |
| **Regular Expressions** | `sed -n '/^[A-Z]/p' file.txt`                  | Print lines starting with an uppercase letter.        |
| **Multiple Commands**   | `sed -e 's/old/new/' -e '/pattern/d' file.txt` | Use multiple commands in one `sed` invocation.        |
| **Backup Before Edit**  | `sed -i.bak 's/old/new/g' file.txt`            | Create a backup file (`file.txt.bak`) before editing. |

**Examples**

| **Command**                  | **Input File: `example.txt`**                         | **Output**                                           |
| ---------------------------- | ----------------------------------------------------- | ---------------------------------------------------- |
| Replace `Linux` with `Unix`  | `Hello World`<br>`This is Linux`<br>`sed is powerful` | `Hello World`<br>`This is Unix`<br>`sed is powerful` |
| Delete the 2nd Line          | `Hello World`<br>`This is Linux`<br>`sed is powerful` | `Hello World`<br>`sed is powerful`                   |
| Print Lines Containing `sed` | `Hello World`<br>`This is Linux`<br>`sed is powerful` | `sed is powerful`                                    |
| Remove Blank Lines           | `Line 1`<br>`<blank>`<br>`Line 2`                     | `Line 1`<br>`Line 2`                                 |


## 2.4 `more` and `less` Commands to Check the File Contents
The `more` and `less` commands are used to view files interactively in the terminal, allowing navigation through large files.

### 2.4.1 `more` Command
The `more` command lets you view file content one screen at a time. It's ideal for reading long files.

**Syntax**
```
more [options] [file] 
```

| **Option**  | **Description**                               |
| ----------- | --------------------------------------------- |
| `-d`        | Display help message when using invalid keys. |
| `-f`        | Count logical lines rather than screen lines. |
| `-p`        | Clear the screen before displaying content.   |
| `-s`        | Squeeze multiple blank lines into one.        |
| `+<number>` | Start displaying from a specific line number. |

### 2.4.2 `less` Command
The `less` command provides a more advanced way to navigate files compared to `more`. It allows backward navigation and searching within the file.

**Syntax**
```
less [options] [file]
```

| **Option**   | **Description**                            |
| ------------ | ------------------------------------------ |
| `-N`         | Display line numbers.                      |
| `-X`         | Disable terminal clearing after exit.      |
| `-S`         | Chop long lines rather than wrapping.      |
| `/<pattern>` | Search for a specific pattern in the file. |

**Comparison of `more` and `less`**

| Feature            | `more` Command                      | `less` Command                    |
| ------------------ | ----------------------------------- | --------------------------------- |
| **Navigation**     | Forward only.                       | Both forward and backward.        |
| **Search**         | Limited to `vi`-style navigation.   | Supports pattern-based searching. |
| **Line Wrapping**  | Automatically wraps lines.          | Can disable wrapping with `-S`.   |
| **Resource Usage** | Simpler and faster for small files. | Advanced, better for large files. |
