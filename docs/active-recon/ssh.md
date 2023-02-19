---
title: SSH - 22
layout: default
nav_order: 1
parent: Active Recon

---

# SSH Enumeration
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

## **<ins>Default Credentials Check</ins>**
1. Login with the following usernames/passwords
```bash
Username: root
Password: toor
Username: root
Password: root
```

2. Attempt login
```bash
ssh root@$IP
```



## **<ins>SSH Nmap Scan</ins>**
```bash
sudo nmap -p 22 -A --script=ssh* --script=vuln $IP -v | tee nmap-ssh.txt
```

## **<ins>SSH Key errors</ins>**
Try this method if SSH key algorithm errors surface: 

```bash
# ssh root@10.5.21.113
Unable to negotiate with 10.5.21.113 port 22: no matching host key type found. Their offer: ssh-dss
```

Reference: https://www.infosecmatter.com/solution-for-ssh-unable-to-negotiate-errors/

Ultimate solution, but it's not safe for overall security. To find out more, please visit the link above. 

```bash
{
echo -n 'Ciphers '
ssh -Q cipher | tr '\n' ',' | sed -e 's/,$//'; echo

echo -n 'MACs '
ssh -Q mac | tr '\n' ',' | sed -e 's/,$//'; echo

echo -n 'HostKeyAlgorithms '
ssh -Q key | tr '\n' ',' | sed -e 's/,$//'; echo

echo -n 'KexAlgorithms '
ssh -Q kex | tr '\n' ',' | sed -e 's/,$//'; echo

} >> ~/.ssh/config
```