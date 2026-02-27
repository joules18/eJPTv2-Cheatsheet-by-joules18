\
# PB-04 — FTP → Files → Creds

## Goal
Use FTP to download files/configs and pivot into another service (DB/SSH/SMB/HTTP).

## Steps
1) Check anonymous + system
```bash
nmap -p 21 -sV -sC --script ftp-anon,ftp-syst <IP> -oN nmap/ftp.txt
```

2) Browse + download
```bash
ftp <IP>
# ls, cd, get <file>
```

3) Search downloaded files for creds
```bash
grep -RniE "user|username|pass|password|host|db|mysql|ssh|smb" loot/ 2>/dev/null
```
