# eJPTv2 Cheatsheet by joules18 — “La Biblia” (Community Edition)

Bienvenido/a 👋  
Este repo es una **ruta guiada** para aprobar **eJPTv2** con enfoque **100% práctico**, **metódico** y **orientado a labs/CTFs** (entornos autorizados).  
La idea es simple: **menos teoría suelta, más ejecución reproducible**.

> ✅ Úsalo **solo** en laboratorios/CTFs y sistemas donde tengas permiso explícito.

---

## ✨ ¿Qué hace diferente a este repo?

La mayoría de cheatsheets son listas gigantes de comandos. Este repo es otra cosa:

- **Metodología de examen** (de IP → servicios → enum → exploit → post → flags) :contentReference[oaicite:4]{index=4}  
- **Mini-playbooks paso a paso** (cuando estás bajo presión, no quieres “pensar”, quieres ejecutar) :contentReference[oaicite:5]{index=5}  
- **Checklists + plantillas** para que documentes “como pro” y no pierdas puntos por desorden :contentReference[oaicite:6]{index=6} :contentReference[oaicite:7]{index=7}  
- **Comandos limpios, sin duplicados** (lo mínimo necesario para llegar al objetivo)

Este repositorio fue construido **cruzando y unificando** cheatsheets públicos de la comunidad, y se mantiene con una regla clara:

> **Este repo es nuestra “biblia”: primero agotamos aquí; recién después usamos cosas externas.**

---

## 👤 ¿Quién soy / qué rol cumplo aquí?

Soy el/la mantenedor(a) de este repo y lo uso como guía para:
- practicar laboratorios de eJPTv2 de forma repetible,
- registrar evidencia rápido,
- y llegar a flags/credenciales con la menor fricción posible.

Si tú también estás en el camino eJPT: **este repo es para ti**.  
Si quieres contribuir: mejor aún. 🤝

---

## 🚀 Quick Start (en 60 segundos)

### 1) Crea tu workspace por target
```bash
mkdir -p ~/ejpt/{nmap,loot,web,notes}
cd ~/ejpt
nano notes/notes.md
Esto se repite en toda la metodología del repo 

CHEATSHEET

.

2) Escaneo base “modo examen”
nmap -Pn -p- -sS -T4 --open <IP> -oA nmap/tcp_all
# luego:
nmap -Pn -sC -sV -p <PORTS> <IP> -oA nmap/svc

(Exactamente como lo guía el flujo principal) 

CHEATSHEET

.

3) Elige tu “superficie primaria”

SMB → PB-02

HTTP → PB-03

FTP → PB-04

DB → PB-05

Con shell → PB-06 

PB-01-Recon-to-Services

🧭 Quick Navigation (por si estás apurado/a)
📌 Lectura principal (empieza aquí)

Main Cheat Sheet (Workflow completo): docs/CHEATSHEET.md 

CHEATSHEET

🔎 Por servicio (cuando ya viste el puerto)

docs/SERVICE_ENUM.md 

SERVICE_ENUM

💥 Metasploit “modo examen”

docs/MSF_WORKFLOW.md 

MSF_WORKFLOW

🧩 Mini-playbooks (mis favoritos)

playbooks/PB-01-Recon-to-Services.md 

PB-01-Recon-to-Services

playbooks/PB-02-SMB-to-Loot.md 

COMMAND_LOG_TEMPLATE

playbooks/PB-03-HTTP-to-RCE.md 

PB-03-HTTP-to-RCE

playbooks/PB-04-FTP-to-Creds.md 

PB-04-FTP-to-Creds

playbooks/PB-05-DB-to-Config-Flags.md 

PB-05-DB-to-Config-Flags

playbooks/PB-06-PostEx-FlagHunt.md 

PB-06-PostEx-FlagHunt

✅ Checklists + Templates (para no perderte)

checklists/TARGET_CHECKLIST.md 

TARGET_CHECKLIST

checklists/COMMAND_LOG_TEMPLATE.md 

PB-02-SMB-to-Loot

templates/NOTES_TEMPLATE.md 

NOTES_TEMPLATE

🧠 Cómo usar esto como si fuese un “sistema” (no solo un PDF)
🔁 Loop por target (la receta real)

Recon → puertos → servicios

Enumeración por servicio

Triage (¿hay exploit obvio?)

Explotación

Post-explotación

Flags / credenciales / pivots

Documentar y pasar al siguiente target

Este loop es exactamente el índice del CHEATSHEET 

CHEATSHEET

.

📸 Evidencia = velocidad + puntos

Usa -oA siempre (nmap), guarda loot/, y pega lo importante en notes.md.

Si un examen se trata de ejecutar bajo presión, tu organización te da puntos.

🏆 “Modo examen”: checklist rápido

Antes de pasar a otra máquina, confirma:

 nmap -p- guardado (-oA)

 nmap -sC -sV -p <ports> guardado

 Enumeración por servicio hecha

 Elegiste 1 vector principal (sin dispersarte)

 Guardaste loot + rutas + creds

 Actualizaste notas y dejaste comandos ganadores

(Está también en TARGET_CHECKLIST.md) 

TARGET_CHECKLIST

.

🤝 Contribuciones (sí, por favor)

Si quieres mejorar este repo, aquí tienes ideas que aportan muchísimo:

Mejorar comandos (typos, rutas de wordlists, flags de nmap)

Agregar “rutas de decisión” (si SMB null falla → ¿qué sigue?)

Playbooks para escenarios comunes (WordPress configs → DB → flags)

Mejorar redacción / orden / “anti-duplicados”

Agregar “common pitfalls” por herramienta

Formato de contribución

Mantén comandos reproducibles

Evita “spam de herramientas”

Aporta el por qué (1 línea) y el qué hacer después (2–3 líneas)

🧩 Roadmap (lo que viene)

 Versión “GitBook style” (navegación lateral + badges + index por temas)

 Tablas de “Decisión rápida” (si veo X, hago Y)

 Sección de “Errores comunes” (nmap/ffuf/gobuster/msf)

 One-liners para parsing de outputs (solo si aportan claridad)

⚠️ Disclaimer (importante)

Este repositorio es para educación y práctica autorizada.
No promueve el uso indebido de herramientas ni acciones fuera de alcance.

⭐ Si te sirvió…

Dale star, compártelo con tu grupo, y si alguien aprueba gracias a esto:
abre un issue con tu feedback (qué te faltó, qué te sobró, qué harías distinto).

Nos vemos en la meta. 🥷🔥


Si quieres, también puedo:
- meterte un **banner ASCII** pro,
- agregar badges (eJPTv2 / Lab-only / Community),
- y crear un `CONTRIBUTING.md` + `CODE_OF_CONDUCT.md` + `LICENSE` para que quede “open-source ready”.
Fuentes
