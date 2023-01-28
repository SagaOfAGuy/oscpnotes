---
title: Listeners / Servers
layout: default
nav_order: 10
parent: File Transfers

---

# Certutil
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---

### Python Server 
#### Python2 web server
```bash
python -m SimpleHTTPServer 7331
```

#### Python3 web server
```bash
python3 -m http.server 7331
```

### PHP Web Server
```bash
php -S 0.0.0.0:8000
```

### Ruby Web Server
```bash
ruby -run -e httpd . -p 9000
```

### Busybox Web Server
```bash
busybox httpd -f -p 10000
```

