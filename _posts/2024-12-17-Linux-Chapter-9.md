---
title: Compress Document
date: 2024-12-17 22:50:00 +0800
categories: [Linux]
tags: [linux, knowledge]
---

# 9.0 Compress Document
**Compression** is the process of reducing the size of data, files, or information to save storage space, optimize transmission, or improve processing speed. It works by encoding data in a more efficient way, often by eliminating redundancy or using mathematical algorithms to represent data more concisely.

## 9.1 Types of Compression

### 9.1.1 Lossless Compression
- Reduces file size **without any loss** of original data.  
- Decompressed data is **exactly** the same as the original.  
- **Examples**:  
  - ZIP, GZIP files  
  - PNG images  
  - FLAC audio files  
- **Algorithms**:  
  - Huffman Coding, LZW, RLE

### 9.1.2 Lossy Compression
- Reduces file size by **removing some data** permanently.  
- Decompressed data is **not identical** to the original but is close enough for human use.  
- **Examples**:  
  - JPEG images  
  - MP3 audio  
  - MP4 video  
- **Algorithms**:  
  - DCT, Wavelet Compression

## 9.2 How Compression Works
- **Pattern Recognition**: Replace repeated data with shorter representations.  
   - Example: `AAAABBB` → `4A3B` (Run-Length Encoding).  
- **Mathematical Models**: Approximate or encode data more efficiently.  
- **Entropy Encoding**: Assign shorter codes to frequent elements.

## 9.3 Archiving Documents Using the `tar` Command

The `tar` command (short for **tape archive**) is a popular utility in Linux and Unix systems for **archiving** and **compressing files**. It allows you to group multiple files and directories into a single archive file, which can optionally be compressed.


### 9.3.1 **Common Syntax**

```bash
tar [options] archive_name.tar file1 file2 directory/
```

- `options`: Specifies the operation (`-c`, `-x`, `-z`, etc.).
- `archive_name.tar`: The name of the archive file to create or extract.
- `file1`, `file2`, `directory/`: The files or directories to archive.

### 9.3.2 Creating an Archive Without Compression

```bash
tar -cvf archive_name.tar file1 file2 directory/
```

### 9.3.3 Creating an Archive with Compression
1. Using gzip for Compression

```bash
tar -czvf archive_name.tar.gz file1 file2 directory/
```

- `-c`: Create a new archive.
- `-z`: Compress the archive using gzip.
- `-v`: Verbose mode (lists archived files).
- `-f`: Specifies the archive file name with .tar.gz extension.

2. Using bzip2 for Compression

```bash
tar -cjvf archive_name.tar.bz2 file1 file2 directory/
```

- `-c`: Create a new archive.
- `-j`: Compress the archive using bzip2.
- `-v`: Verbose mode (lists archived files).
- `-f`: Specifies the archive file name with .tar.gz extension.

### 9.3.4 Basic Commands

| Option | Description                                    |
| ------ | ---------------------------------------------- |
| `-c`   | Create a new archive.                          |
| `-x`   | Extract files from an archive.                 |
| `-v`   | Verbosely list files being archived/extracted. |
| `-f`   | Specify the filename of the archive.           |
| `-z`   | Compress the archive using gzip.               |
| `-j`   | Compress the archive using bzip2.              |
| `-C`   | Change directory when extracting files.        |

## 9.4 Creating a Bit-by-Bit or Physical Copy of a Storage Device in Linux
Creating a **bit-by-bit or physical copy** of a storage device involves duplicating every byte of the source device to another destination device. This process is often used for **data recovery, backups, or forensic analysis**.

1. dd Command
- One of the most commonly used tools for creating a bit-by-bit copy.
- Captures the entire content of a storage device, including unallocated space.

```bash
dd if=/dev/source_device of=/dev/destination_device bs=4M status=progress
```
- `if`: Input file (source device).
- `of`: Output file (destination device).
- `bs`: Block size (adjust based on the size of the storage).
- `status=progress`: Shows progress during the operation.

2. ddrescue
- A more robust and error-tolerant tool for data recovery or copying devices with bad sectors.

```bash
ddrescue /dev/source_device /dev/destination_device
```

3. dcfldd
- Similar to `dd` but provides additional features like hash verification and logging.

```bash
dcfldd if=/dev/source_device of=/dev/destination_device hash=md5
```

## 9.5 Summary 
`tar` simplifies file organization, while compression tools like `compress`, `gzip` and `bzip2` reduce file size. However, they may struggle with data recovery, especially when files are overwritten or deleted. dd excels at creating bit-by-bit copies but can’t recover permanently lost data. For more robust data management, combining these tools with specialized recovery methods is recommended.


| Compression Method | Compression Ratio      | Speed            | Suitable For                          |
| ------------------ | ---------------------- | ---------------- | ------------------------------------- |
| **gzip**           | Good (balanced)        | Fast             | General-purpose file compression      |
| **bzip2**          | Better than gzip       | Slower           | Large text/data files                 |
| **XZ**             | High compression ratio | Slower           | Critical data or archival purposes    |
| **zstd**           | Very good compression  | Fast & Efficient | Balance between compression & speed   |
| **7-Zip**          | High compression       | Varies           | High compression with custom settings |
