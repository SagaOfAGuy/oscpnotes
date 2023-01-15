---
title: Linux Privilege Escalation
layout: default
nav_order: 1
parent: Privilege Escalation

---

# Linux Privilege Escalation
{: .no_toc }
## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

### SUID/SGID Binary
### Automated Tools
### Kernel Exploits


### SSH - Authorized Keys Transfer
If you can upload files to the target, but have no shell, you may be able to export your public key as an `authorized_key` file and gain access to the target as root or other user

1. Generate SSH key 
<br>
```bash
ssh-keygen # generate key example.pub at /home/kali/.ssh/example.pub
```

2. Copy the **public** SSH key into a file called `authorized_keys` locally. 
```bash
cat /home/kali/.ssh/example.pub > authorized_key
```

3. Upload our local `authorized_key` file to the target which would be `/root/.ssh/authorized_keys` for the root user or `/home/$USER/.ssh/authorized_keys` for any other user.

4. Attempt to SSH into the target machine using the `example.pub` public key we created as the user we targeted on the target. We use the `-i` to specify the public key. Otherwise, this technique **WON'T** work. 
```bash
ssh -i /home/kali/.ssh/example.pub root@$IP
```

