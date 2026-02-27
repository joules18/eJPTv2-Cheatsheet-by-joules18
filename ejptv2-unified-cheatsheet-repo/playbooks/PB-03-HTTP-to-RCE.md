\
# PB-03 — HTTP → Discovery → RCE (fast path)

## Goal
Find hidden directories/files, identify the app, locate a low-effort exploit path.

## Steps
1) Fingerprint + headers
```bash
whatweb http://<IP>
curl -I http://<IP>/
```

2) Discovery
```bash
dirb http://<IP>/
gobuster dir -u http://<IP>/ -w /usr/share/wordlists/dirb/common.txt -x php,txt,html -t 50
```

3) Fast “interesting files”
- `/robots.txt`, `/sitemap.xml`
- `.env`, `wp-config.php`, `settings.php`
- backups: `.bak`, `.old`, `.zip`, `~`

4) Triage
```bash
searchsploit <APP> <VERSION>
```

5) If you get creds → try admin panels / DB login / SMB login
