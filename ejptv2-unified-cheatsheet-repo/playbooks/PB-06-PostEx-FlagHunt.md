\
# PB-06 — Post-Exploitation Flag Hunt (Win/Linux)

## Goal
Stabilize access, collect system info, and find flags/creds fast.

## Windows (CMD quick)
```bat
whoami
hostname
systeminfo
ipconfig /all
net users
net localgroup administrators
dir /b/s "*flag*"
dir /b/s "*.txt"
dir /b/s "*pass*"
type C:\path\file.txt
```

## Linux (quick)
```bash
whoami; id
uname -a; cat /etc/*release
ip a; ip route; ss -tulpn
find / -maxdepth 4 -type f -iname "*flag*" 2>/dev/null
grep -RniE "pass|password|apikey|token|secret|user" /etc /var/www 2>/dev/null | head
```

## Stabilize TTY (Linux)
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
# CTRL+Z
stty raw -echo && fg
reset
export TERM=xterm
```
