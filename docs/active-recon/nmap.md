---
title: Nmap
layout: default
nav_order: 1
parent: Active Recon

---

# Nmap Scanning
{: .no_toc }

# Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---


## **TCP Scans**
Quick Scan
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
sudo nmap -Pn -T5 -p- $IP -v | grep Discovered | awk -F " " '{print substr($4,1,length($4)-4)}' | tee ports.txt && sudo nmap -p $(tr '\n' , < ports.txt) -A -Pn $IP -v | tee nmap-depth.txt
```

Scan if ICMP ping is blocked
```bash
sudo nmap -Pn -T5 -p- $IP -v | tee nmap-probe-tcp.txt
sudo nmap -Pn -T5 -p <PORTS> $IP -v | tee nmap-probe-depth.txt
```
<br>

## **Vulnerability Scan**
Vuln Scan
```bash
sudo nmap --script=vuln -A -p <PORT> $IP -v | tee nmap-vuln.txt
```

## **UDP Scans**

Scan top 50 and 100 UDP ports
```bash
sudo nmap -T5 --top-ports=50 -sU $IP -v | tee nmap-quick-udp.txt
sudo nmap -T5 --top-ports=100 -sU $IP -v | tee nmap-quick-udp.txt
```
In-depth scan
```bash
sudo nmap -p <PORT> -A -sU $IP -v | tee nmap-depth-udp.txt
```

## **Scanning behind proxies**
Nmap scan behind a proxy
```bash
sudo nmap --proxies http://$IP:80 -A $IP -v | tee nmap-proxied.txt
```

Nmap scan behind proxy - Proxychains
1. Download proxychains if not installed
```bash
sudo apt install proxychains4 -y 
```
<br>
2. Edit `/etc/proxychains4.conf` by adding the IP and port:
```bash
echo 'http $IP $PORT' >> /etc/proxychains4.conf
```
<br>
3. Scan target through `proxychains`
```bash
sudo proxychains nmap -T5 -sS $IP -v | tee nmap-proxied.txt
```

