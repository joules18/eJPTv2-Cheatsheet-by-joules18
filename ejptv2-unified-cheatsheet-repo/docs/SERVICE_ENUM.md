\
# SERVICE_ENUM — Recipes by Service (eJPTv2)

> Use this when you know the port/service and want the fastest “what next?”.

## SMB (139/445)
### 1) Identify OS / protocols / signing
```bash
nmap -p 139,445 -sV -sC <IP> -oN nmap/smb_base.txt
nmap -p 445 --script smb-os-discovery,smb-protocols,smb-security-mode <IP> -oN nmap/smb_info.txt
```

### 2) Null session / shares / users
```bash
enum4linux -a <IP>
smbclient -L //<IP> -N
smbmap -H <IP> -u guest -p "" -d .
rpcclient -U "" -N <IP>
```

### 3) Enter share and loot
```bash
smbclient //<IP>/<SHARE> -N
# ls, cd, get <file>
```

---

## FTP (21)
### 1) Anonymous?
```bash
nmap -p 21 -sV -sC --script ftp-anon,ftp-syst <IP> -oN nmap/ftp.txt
```
### 2) Browse and download
```bash
ftp <IP>
# ls, cd, get <file>
```

---

## SSH (22)
```bash
nmap -p 22 -sV -sC <IP> -oN nmap/ssh.txt
ssh <USER>@<IP>
```

---

## HTTP/HTTPS
### 1) Fingerprint
```bash
whatweb http://<IP>
curl -I http://<IP>/
```

### 2) Discovery (dirs/files)
```bash
dirb http://<IP>/
gobuster dir -u http://<IP>/ -w /usr/share/wordlists/dirb/common.txt -x php,txt,html -t 50
```

### 3) Quick checks
- `robots.txt`, `sitemap.xml`
- backup extensions: `.bak`, `.old`, `.zip`, `~`
- configs: `.env`, `wp-config.php`, `settings.php`

---

## MySQL (3306)
```bash
nmap -p 3306 -sV --script mysql-info,mysql-empty-password <IP> -oN nmap/mysql.txt
mysql -h <IP> -u <USER> -p
```
Inside MySQL:
```sql
show databases;
use <db>;
show tables;
select * from <table> limit 5;
```

---

## MSSQL (1433)
```bash
nmap -p 1433 -sV -sC --script ms-sql-info,ms-sql-ntlm-info <IP> -oN nmap/mssql.txt
```

---

## SMTP (25)
```bash
nmap -p 25 -sV -sC <IP> -oN nmap/smtp.txt
nc <IP> 25
# EHLO test
```
