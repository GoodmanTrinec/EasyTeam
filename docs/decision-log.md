﻿# Decision Log — rozhodovací deník

Tento deník zaznamenává klíčová rozhodnutí o směřování EasyTeam projektu.

## Princip

- **GitHub je primární zdroj pravdy.** Všechna projektová rozhodnutí, verze promptů a dokumentace patří do committed markdown souborů.
- **`.omo/` je lokální scratch stav** — session deník, plány, drafty. NENÍ oficiálním zdrojem pravdy.
- Projektová rozhodnutí, changelog a release notes patří do normálních committed docs.

---

## Rozhodnutí

### 2026-07-19 — EasyTeam jako ChatGPT Pro prompt-pack

**Rozhodnutí:** EasyTeam bude markdown prompt-pack pro ChatGPT Pro, ne aplikace.

**Důvody:**
- UŽIVATEL má ChatGPT Pro s GitHub integrací
- Prompt-pack je rychlejší cesta k užitečnému výsledku než UI
- Hlavní mezera je kvalita workflow, ne tlačítka

**Dopad:** Všechny soubory jsou markdown, žádný backend, žádná databáze.

---

### 2026-07-19 — Low-typing interakce

**Rozhodnutí:** UŽIVATEL píše jen `0`-`9`, `ano`/`ne`, nebo krátký brief. Žádné dlouhé věty.

**Důvody:** UŽIVATEL píše pomalu a chce minimum psaní.

**Dopad:** Všechny prompty musí podporovat číselné příkazy a `ano`/`ne`. Nikdy nevyžadovat `MODERÁTOR, zahaj kolo 1`.

---

### 2026-07-19 — Žádná placená API

**Rozhodnutí:** Projekt nepoužívá žádná placená API ani modely nad rámec stávajícího ChatGPT Pro.

**Důvody:** UŽIVATEL výslovně odmítl placené služby.

**Dopad:** Všechny prompty obsahují guardrail. Pokud by něco vyžadovalo platbu, pouze varovat a nepřipojit.

---

### 2026-07-19 — Tolerance vstupního jazyka

**Rozhodnutí:** EasyTeam akceptuje mix PL/CZ/EN a nářečí `po naszymu`. Nikdy neopravuje UŽIVATEL.

**Důvody:** UŽIVATEL přirozeně míchá jazyky včetně lokálního nářečí.

**Dopad:** Všechny prompty musí tolerovat smíšený vstup a v případě potřeby se zeptat na výstupní jazyk jednou krátkou otázkou.

---

### 2026-07-20 — GitHub primární, `.omo/` scratch

**Rozhodnutí:** GitHub committed markdown je zdroj pravdy. `.omo/` je lokální plánovací scratch.

**Důvody:** UŽIVATEL chce GitHub jako primární úložiště. Session deník a plány v `.omo/` jsou dočasné.

**Dopad:** Všechna důležitá rozhodnutí, changelog a dokumentace jdou do committed souborů.