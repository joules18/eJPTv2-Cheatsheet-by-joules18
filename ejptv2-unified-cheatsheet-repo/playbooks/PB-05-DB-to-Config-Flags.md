\
# PB-05 — DB Access → Configs → Flags

## Goal
Use DB creds to find app configs, tables, and anything that points to flags or further access.

## MySQL
1) Nmap scripts
```bash
nmap -p 3306 -sV --script mysql-info,mysql-empty-password <IP> -oN nmap/mysql.txt
```

2) Login
```bash
mysql -h <IP> -u <USER> -p
```

3) Useful queries (start small)
```sql
show databases;
use <db>;
show tables;
select * from <table> limit 5;
```

4) If this is a web app DB:
- Look for tables like `users`, `config`, `settings`, `admin`, `wp_users`
- Check app configs on the target filesystem if you gain shell later (`wp-config.php`, `.env`)
