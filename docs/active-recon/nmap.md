---
title: Nmap
layout: default
nav_order: 1
parent: Active Recon

---

# Nmap Scanning
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---


### TCP Scans
Quickly scan all ports
```bash
sudo nmap -T5 -p- $IP -v | tee nmap-quick-tcp.txt
```
Scan **x** number of ports
```bash
sudo nmap --top-ports=100 $IP -v | tee nmap-top-50.txt
```

In-depth Scan
```bash
sudo nmap -A -p <PORTS> -sV $IP -v | tee nmap-tcp.txt
```

Quick Scan + In-depth Scan
```bash
sudo nmap -T5 -p- $IP -v | grep Discovered | awk -F " " '{print substr($4,1,length($4)-4)}' | tee ips.txt && sudo nmap -p `cat ips.txt` -A $IP -v | tee nmap-depth.txt 
```

Scan if ICMP ping is blocked
```bash
sudo nmap -Pn -T5 -p- $IP -v | tee nmap-probe-tcp.txt
```

```bash
sudo nmap -Pn -T5 -p <PORTS> $IP -v | tee nmap-probe-depth.txt
```

Vulnerability Scan
```bash
sudo nmap --script=vuln -A -p <PORT> $IP -v | tee nmap-vuln.txt
```

### UDP Scans
Scan top 50 and 100 UDP ports
```bash
sudo nmap -T5 --top-ports=50 -sU $IP -v | tee nmap-quick-udp.txt
```

```bash
sudo nmap -T5 --top-ports=100 -sU $IP -v | tee nmap-quick-udp.txt
```

In-depth scan
```bash
sudo nmap -p <PORT> -A -sU $IP -v | tee nmap-depth-udp.txt
```
