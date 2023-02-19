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


## **<ins>Resolve IP address of Domain</ins>**
```bash
host www.google.com
```
**OR**

```bash
nslookup google.com
```

## **<ins>Find Mail Record Entries</ins>**
Mail records are **names of servers responsible for handling mail for a domain**
```bash
host -t mx google.com
```
## **<ins>Find Nameserver Entries</ins>**
Nameserver entries contain names of the servers that host DNS records for a domain
```bash
host -t ns google.com
```

## **<ins>Find 'A' Record (IP Address of hostname)</ins>**
'A Records' contain the IP addresses of a hostname
```bash
host -t a google.com
```

## **<ins>Find Pointer records</ins>**
Pointer records are used to find records associated with an **IP Address**
```bash
host -t ptr $IP
```
## **<ins>Find Canonical Name records</ins>**
Canonical names are aliases for other hosts
```bash
host -t -cname $IP
```

## **<ins>Find Text records</ins>**
Text records are arbitrary data that can be used for domain ownership verification
```bash
host -t txt $IP
```

## **<ins>DNS Nmap Scan</ins>**
```bash
sudo nmap -A -p 53 -sV --script=dns* $IP -v | tee nmap-dns.txt
```

## **<ins>Zone Transfer</ins>**
```bash
dig axfr @$IP  
```