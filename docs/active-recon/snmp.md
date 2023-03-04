---
title: SNMP - 161
layout: default
nav_order: 6
parent: Active Recon

---

# SNMP Enumeration
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

## Nmap scan
```
sudo nmap --script=snmp* --script=vuln -sU --open -p 161 $IP -v | tee nmap-snmp.txt
```
## SNMP enum for Linux Systems
```bash
snmp-check $IP -c public
```
## SNMP enum for Windows Systems

Enumerating entire MIB Database
```
snmpwalk -c public -v1 -t 10 $IP
```
`-c` is for community string

`-v` specifies SNMP version. Usually versions 1 & 2 are more likely to have vulns

`-t` timeout variable

## Enumerating Windows Users
```
snmpwalk -c public -v1 $IP 1.3.6.1.4.1.77.1.2.25
```

## Enumerating Running Processes in Windows
```
snmpwalk -c public -v1 $IP 1.3.6.1.2.1.25.4.2.1.2
```
## Enumerating open TCP ports
```
snmpwalk -c public -v1 $IP 1.3.6.1.2.1.6.13.1.3
```
## Enumerating installed softwares
```
snmpwalk -c public -v1 $IP 1.3.6.1.2.1.25.6.3.1.2
```
