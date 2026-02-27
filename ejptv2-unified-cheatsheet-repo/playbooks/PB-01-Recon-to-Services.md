\
# PB-01 — Recon → Services (repeatable)

## Goal
Turn an IP into a list of confirmed open ports + service versions + next actions.

## Steps
1) Create workspace folders
```bash
mkdir -p ~/ejpt/{nmap,loot,web,notes}
cd ~/ejpt
```

2) Quick TCP scan
```bash
nmap -Pn -sS -T4 --open <IP> -oN nmap/tcp_quick.txt
```

3) Full TCP scan
```bash
nmap -Pn -p- -sS -T4 --open <IP> -oA nmap/tcp_all
```

4) Service enumeration (only open ports)
```bash
nmap -Pn -sC -sV -p <PORTS> <IP> -oA nmap/svc
```

5) Decide “primary attack surface”
- SMB? → PB-02
- HTTP? → PB-03
- FTP? → PB-04
- DB? → PB-05
- Got shell? → PB-06
