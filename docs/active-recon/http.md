---
title: HTTP - 80
layout: default
nav_order: 3
parent: Active Recon

---

# HTTP Enumeration
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

### Grabbing Banner
```bash
nc -nv $IP $PORT | tee banner.txt
```
### Nikto
```bash
nikto -h $IP | tee nikto.txt
```
### Check for robots.txt
```bash
curl http://$IP/robots.txt | tee robots.txt
```
### Check for sitemap.xml
```bash
curl http://$IP/sitemap.xml
```

### Dirsearch
Bruteforce with common list
```bash
dirsearch -w /usr/share/wordlists/dirb/common.txt -u http://$IP:$PORT -o $PWD/dirsearch.txt
```
Bruteforce with common list (recursive)
```bash
dirsearch -r -w /usr/share/wordlists/dirb/common.txt -u http://$IP:$PORT -o $PWD/dirsearch.txt
```
Bruteforce with big.txt list
```bash
dirsearch -w /usr/share/wordlists/dirb/big.txt -u http://$IP:$PORT -o $PWD/dirsearch.txt
```
Bruteforce with big.txt list (recursive)
```bash
dirsearch -r -w /usr/share/wordlists/dirb/big.txt -u http://$IP:$PORT -o $PWD/dirsearch.txt
```
### Gobuster
```bash
gobuster dir -e -u http://$IP -k -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -o gobuster.txt
```

### HTTP Nmap Scan
```bash
sudo nmap -p <PORT> -A --script=http* --script=vuln $IP -v | tee nmap-http.txt
```

