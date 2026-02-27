# eJPTv2 Unified Cheat Sheet (Community Edition)

A **single, highly-ordered**, exam-aligned cheat sheet for **eJPTv2** labs/CTFs and authorized practice.
Built by **cross-unifying** multiple public community cheat sheets into one clean, repeatable workflow.

> ✅ Use **only** on systems you own or have explicit permission to test (labs/CTFs/training ranges).

---

## Quick Start

### 1) Create a working folder per target
```bash
mkdir -p ~/ejpt/{nmap,loot,web,notes}
cd ~/ejpt
```

### 2) Recommended “evidence” outputs
- `nmap/` → all scan outputs (`-oA` / `-oN`)
- `loot/` → downloaded configs, flags, DB dumps, etc.
- `web/` → requests, dir bust outputs, screenshots
- `notes/notes.md` → credentials, paths, commands, findings

---

## Repository Structure

- `docs/`
  - `CHEATSHEET.md` → **Main** unified cheat sheet (index + commands + mini playbooks)
  - `SERVICE_ENUM.md` → service-by-service enumeration recipes
  - `MSF_WORKFLOW.md` → metasploit workflow (exam-speed)
- `playbooks/`
  - `PB-01-Recon-to-Services.md`
  - `PB-02-SMB-to-Loot.md`
  - `PB-03-HTTP-to-RCE.md`
  - `PB-04-FTP-to-Creds.md`
  - `PB-05-DB-to-Config-Flags.md`
  - `PB-06-PostEx-FlagHunt.md`
- `checklists/`
  - `TARGET_CHECKLIST.md` → per-target exam checklist
  - `COMMAND_LOG_TEMPLATE.md` → paste commands + outputs quickly
- `templates/`
  - `NOTES_TEMPLATE.md`

---

## Contents

1. **Main cheat sheet**: `docs/CHEATSHEET.md`
2. Service enum recipes: `docs/SERVICE_ENUM.md`
3. Metasploit workflow: `docs/MSF_WORKFLOW.md`
4. Mini-playbooks: `playbooks/`
5. Checklists & templates: `checklists/`, `templates/`

---

## License & Sharing

This repo is intended for **learning and exam preparation**. If you share it, keep attribution and the authorized-use note.
