---
title: SMTP - 25
layout: default
nav_order: 2
parent: Active Recon

---

# SMTP Enumeration
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

## **Grabbing SMTP banner**
```bash
nc -nvC $IP 25
```
## **Search SMTP version in Searchsploit**
```bash
searchsploit <SMTP_VERSION>
```

## **Search Google for SMTP version**
```bash
https://www.google.com/search?q=<SMTP_VERSION>
```

## **Search Github for SMTP Version**
```bash
https://www.google.com/search?q=Github <SMTP_VERSION> Exploit
```

## **Enumerate Users via Python script**
Python code for verifying usernames in SMTP
```python
#!/usr/bin/python
import socket
import sys
if len(sys.argv) != 3:
        print "Usage: vrfy.py <ip> <username>"
        sys.exit(0)
# Create a Socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
# Connect to the Server
connect = s.connect((sys.argv[1],25))
# Receive the banner
banner = s.recv(1024)
print banner
# VRFY a user
s.send('VRFY ' + sys.argv[2] + '\r\n')
result = s.recv(1024)
print result
# Close the socket
s.close()
```

Executing above script: 
```bash
python smtpenum.py <IP> <USER>

python smtpenum.py $IP root
```


## **SMTP Nmap Scan**
```bash
sudo nmap -p 25 -sV -A --script=smtp* --script=vuln $IP -v | tee nmap-smtp.txt
```