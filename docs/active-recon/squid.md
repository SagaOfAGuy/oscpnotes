---
title: Squid - 3128
layout: default
nav_order: 10
parent: Active Recon

---

# Squid Enumeration
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

### Spose.py
Scanning via `spose.py`
Download link - https://github.com/aancw/spose

#### Download 
```bash
git clone https://github.com/aancw/spose.git
```

#### Scan 
```bash
python spose.py --proxy http://$IP:3128 --target $IP
```




