---
title: SMB - 139/445
layout: default
nav_order: 7
parent: Active Recon

---

# SMB Enumeration
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---

## SMB NSE Script Enumeration

NSE script to enumerate SMB OS version
```bash
sudo nmap -v -p 139, 445 --script=smb-os-discovery $IP
```

Runs NSE SMB vuln scripts that won't crash the target machine
```bash
nmap -v -p 139,445 --script=smb-vuln-* --script-args=safe=1 $IP
```

Runs NSE SMB vuln scripts that **WILL** crash the target machine
```bash
nmap -v -p 139,445 --script=smb-vuln-* --script-args $IP
```
Runs all NSE SMB Scripts against 139/445 regardless of safety
```bash
nmap -v -p 139,445 --script=smb-* $IP
```

List SMB Shares
```bash
nmap --script smb-enum-shares -p139,445 $IP
```

Toggle safety argument and look for Vulnerability **MS08-067**. Unsafe means that it may crash the host.
```bash
sudo nmap -v -p 139,445, --script=smb-vuln-ms08-067 --script-args=unsage=1 $IP
```


## SMBClient 

List shares compatible with NT1 protocol 

```bash
smbclient --option='client min protocol=NT1' -L $IP  
```

List shares compatible with LANMAN1 protocol
```bash
smbclient --option='client min protocol=LANMAN1' -L $IP
```

List available SMB Shares 
```bash
smbclient -L $IP
```

List available SMB Shares (Authenticated)
```bash
smbclient -L $IP -U user%pass
```

Connect to existing SMB Share
```bash
smbclient \\\\<ip>\\<sharename>

smbclient //$IP/<sharename>
```

Connect to existing SMB Share (Authenticated)
```bash
smbclient //$IP/<sharename> -U user%pass
```

Login to SMB as user
```bash
smbclient --user=$user//$IP/$sharename
```

Download files within smbclient
```bash
smb: \> get file.txt
```

Download all files within SMB share:
```bash
smb: \> mget 
```


## SMBMap

List SMB Shares
```bash
smbmap -H $IP
```

List share with username and password
```bash
smbmap -H $IP -u $USER -p $PASSWORD
```

List SMB Shares recursively
```bash
smbmap -H $IP -R
```


## RPClient

Running null session on rpcclient:
```bash
rpclient -u "" $IP
```

Getting server info:
```bash
rpclient> srvinfo
```

Enumerating users:
```bash
rpclient> enumdomusers
```



## Enum4Linux
Scan machine for SMB information: 
```bash
enum4linux $IP
```

## Enum4Linux-ng

1. Install enum4linux-ng
```bash
git clone https://github.com/cddmp/enum4linux-ng.git
```

2. Install python3 dependencies
```bash
cd /path/to/enum4linux-ng && pip3 install -r requirements.txt
```

3. Move enum4linux-ng binary to /usr/local/bin
```bash
sudo mv /path/to/enum4linux-ng.py /usr/local/bin/enum4linux-ng
```

4. Confirm that enum4linux-ng is working properly
```bash
enum4linux-ng -h
```

5. Run enum4linux-ng
```bash
enum4linux-ng -A $IP | tee enum4linux-ng.txt
```




## CrackMapExec

List SMB Shares (Unauthenticated)
```bash
crackmapexec smb $IP -u '' -p '' --shares
```

List SMB Shares (Authenticated)
```bash
crackmapexec smb $IP -u 'admin' -p 'password' --shares
```


## NBTScan - Enumerating NetBIOS

Scan host for NetBIOS:
```bash
sudo nbtscan -r $IP
```

Scan entire subnet for NetBIOS
```bash
sudo nbtscan -r $IP/24
```


## NMBLookup - Enumerating NetBIOS

Scan host:
```bash
nmblookup -A $IP
```


## Metasploit - SMB Shares Scanner

SMB Shares Scanner (Unauthenticated)
```bash
msfconsole -q -x 'use auxiliary/scanner/smb/smb_enumshares; set rhost $IP; exploit'
```

SMB Shares Scanner (Authenticated)
```bash
msfconsole -q -x 'use auxiliary/scanner/smb/smb_enumshares; set rhost $IP; exploit; set smbuser $USER; set smbpass $PASS'
```



## Finding Samba Version
Script to find Samba server version:
```bash
#!/bin/sh
#Author: rewardone
#Description:
# Requires root or enough permissions to use tcpdump
# Will listen for the first 7 packets of a null login
# and grab the SMB Version
#Notes:
# Will sometimes not capture or will print multiple
# lines. May need to run a second time for success.
if [ -z $1 ]; then echo "Usage: ./smbver.sh RHOST {RPORT}" && exit; else rhost=$1; fi
if [ ! -z $2 ]; then rport=$2; else rport=139; fi
tcpdump -s0 -n -i tap0 src $rhost and port $rport -A -c 7 2>/dev/null | grep -i "samba\|s.a.m" | tr -d '.' | grep -oP 'UnixSamba.*[0-9a-z]' | tr -d '\n' & echo -n "$rhost: " &
echo "exit" | smbclient -L $rhost 1>/dev/null 2>/dev/null
echo "" && sleep .1
```

Script Usage: 
```bash
./samba_ver.sh $IP $PORT
```



## Mounting SMB shares to attack machine
1. Make sure cifs  and cifs-helper  are installed:
```bash
sudo apt install cifs cifs-utils
```

2. Create a directory in /mnt :
```bash
sudo mkdir -p /mnt/user
```

3. Mount the Samba share:
```bash
sudo mount -t cifs //$IP/<share name> /mnt/user
```


## Unmount SMB Share
```bash
sudo umount -a -t cifs -l
```
