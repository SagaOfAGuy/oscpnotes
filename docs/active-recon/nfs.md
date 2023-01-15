---
title: NFS - 111
layout: default
nav_order: 4
parent: Active Recon

---

# NFS Enumeration
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---



### NFS Nmap Scans
```bash
sudo nmap -sV -p 111 --script=rpcinfo $IP | tee nmap-nfs-rpcinfo.txt
```

```bash
sudo nmap -sV -p 111 --script nfs* $IP | tee nmap-nfs.txt
```

### Mount NFS share
1. Mount NFS share
```bash
sudo mount -o nolock $IP:/$SHARE_PATH
```

2. If we still can't view the path mounted, create user that has the same UID as specified in the permissions output via `ls -aril`
```bash
sudo useradd -u $UID $USER
```

3. Become created user, and see if you can view the restricted file:
```bash
su $USER
```

### Unmount NFS share
```bash
sudo umount -f -l $SHARE_PATH
```
