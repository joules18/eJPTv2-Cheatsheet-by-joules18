\
# PB-02 — SMB → Loot (Null/Guest first)

## Goal
Enumerate shares/users quickly, download interesting files, extract creds/paths.

## Steps
1) Baseline SMB enum
```bash
nmap -p 139,445 -sV -sC <IP> -oN nmap/smb_base.txt
nmap -p 445 --script smb-os-discovery,smb-protocols,smb-security-mode <IP> -oN nmap/smb_info.txt
```

2) Null/guest discovery
```bash
enum4linux -a <IP>
smbclient -L //<IP> -N
smbmap -H <IP> -u guest -p "" -d .
rpcclient -U "" -N <IP>
```

3) Enter share and download
```bash
smbclient //<IP>/<SHARE> -N
# ls
# get <file>
```

4) Parse loot for creds
```bash
grep -RniE "pass|password|user|username|apikey|token|secret" loot/ notes/ 2>/dev/null
```
