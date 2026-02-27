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
