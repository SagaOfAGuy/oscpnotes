---
title: FTP - 21
layout: default
nav_order: 2
parent: Active Recon

---

# FTP Enumeration
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

## Anonymous Login
```bash
ftp $IP 

USER anonymous
PASS anonymous
```

## Passive Mode - Issue 
Issue when the `ftp` keeps giving a ``

Relevant Issue - https://www.youtube.com/watch?v=i5furEJlySY
```bash
ftp $IP

ftp>passive
Passive mode: off
```

## Banner Grabbing
```bash
nc -nvC $IP 21
```

```bash
nc -nv $IP 21
```

Search for banner in `searchsploit`: 
```bash
searchsploit $BANNER_VERSION 
```


## Nmap Scan - Vulnerability 
```bash
sudo nmap -T5 -p 21 -A --script=vuln --script=ftp* $IP -v 
```

## Nmap Scan
```bash
sudo nmap -T5 -p 21 -A --script=ftp* $IP -v 
```

