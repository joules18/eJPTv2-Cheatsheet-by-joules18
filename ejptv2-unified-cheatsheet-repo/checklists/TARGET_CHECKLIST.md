\
# TARGET_CHECKLIST — eJPTv2 (Per Target)

## A) Discovery
- [ ] Create folders (`nmap/ loot/ web/ notes/`)
- [ ] Run full TCP scan (`nmap -p- ... -oA`)
- [ ] Run service scan (`nmap -sC -sV -p <ports> ... -oA`)

## B) Enumeration (pick what exists)
- [ ] SMB: shares/users/null session
- [ ] FTP: anonymous/files
- [ ] HTTP: dirs/files/robots/sitemap
- [ ] SQL: login/dbs/tables
- [ ] SMTP/SSH: basics

## C) Exploitation
- [ ] Choose 1 main path
- [ ] Gain stable session/shell
- [ ] Save loot + outputs

## D) Post & Goal
- [ ] Find configs → creds → flags
- [ ] Quick privesc checks (if needed)
- [ ] Note the exact “winning commands”

## E) Notes
- [ ] Update `notes/notes.md` with:
  - IP, ports, creds
  - paths
  - exploit module / steps
  - flags
