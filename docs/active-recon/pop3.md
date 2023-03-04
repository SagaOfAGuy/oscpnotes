---
title: POP3 - 110
layout: default
nav_order: 3
parent: Active Recon

---

# POP3 Enumeration
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

## Nmap Scan
```bash
sudo nmap -A -p 110 --script=vuln --script=pop3* $IP -v | tee nmap-pop3.txt
```

## Banner Grab
```bash
telnet $IP 110
```

```bash
nc -nv $IP 110
```

Reference - https://book.hacktricks.xyz/network-services-pentesting/pentesting-pop




