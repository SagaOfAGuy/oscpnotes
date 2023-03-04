---
title: DNS - 53
layout: default
nav_order: 3
parent: Active Recon

---

# DNS Enumeration
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---


## **Resolve IP address of Domain**
```bash
host www.google.com
```

```bash
nslookup google.com
```

## **Find Mail Record Entries**
Mail records are **names of servers responsible for handling mail for a domain**
```bash
host -t mx google.com
```
## **Find Nameserver Entries**
Nameserver entries contain names of the servers that host DNS records for a domain
```bash
host -t ns google.com
```

## **Find 'A' Record (IP Address of hostname)**
'A Records' contain the IP addresses of a hostname
```bash
host -t a google.com
```

## **Find Pointer records**
Pointer records are used to find records associated with an **IP Address**
```bash
host -t ptr $IP
```
## **Find Canonical Name records**
Canonical names are aliases for other hosts
```bash
host -t -cname $IP
```

## **Find Text records**
Text records are arbitrary data that can be used for domain ownership verification
```bash
host -t txt $IP
```

## **DNS Nmap Scan**
```bash
sudo nmap -A -p 53 -sV --script=dns* $IP -v | tee nmap-dns.txt
```

## **Zone Transfer**
```bash
dig axfr @$IP  
```