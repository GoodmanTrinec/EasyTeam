# Decision Log — rozhodovací deník

Tento deník zaznamenává klíčová rozhodnutí o směřování EasyTeam projektu.

## Princip

- **GitHub je primární zdroj pravdy.** Všechna projektová rozhodnutí, verze promptů a dokumentace patří do committed markdown souborů.
- **Dočasné agentní scratch soubory nejsou zdroj pravdy** — session poznámky, plány a drafty patří mimo oficiální dokumentaci, dokud nejsou přepsané do committed markdown souborů.
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

### 2026-07-20 — GitHub primární, scratch mimo dokumentaci

**Rozhodnutí:** GitHub committed markdown je zdroj pravdy. Dočasné agentní scratch soubory nejsou součást oficiální dokumentace.

**Důvody:** UŽIVATEL chce GitHub jako primární úložiště. Session deníky a pracovní plány jsou dočasné.

**Dopad:** Všechna důležitá rozhodnutí, changelog a dokumentace jdou do committed souborů.

---

### 2026-07-22 — Počet plných kol, TITLE a final gate

**Rozhodnutí:** AUTO používá poslední samostatné kladné celé číslo z briefu jako počet kol; při chybějícím počtu použije 2. Každé plné kolo má přesně pořadí MODERÁTOR → HUDEBNÍK → BÁSNÍK → PROMPTER → KRITIK → MODERÁTOR. Stav obsahuje `current_title`, `current_lyrics` a `current_style`. Po všech kolech proběhne samostatný final gate KRITIK a COVERMASTER se aktivuje pouze po `PASS`.

**Důvody:** Style Prompt musí vznikat souběžně s Lyrics, TITLE musí odpovídat aktuálnímu příběhu a žádný krátký příkaz nesmí obejít kontrolu kvality.

**Dopad:**

- `tema rytir metal cz 3` nastaví 3 plná kola, `tema reggae pl 5` nastaví 5; brief bez počtu nastaví 2. Samotné spuštění AUTO vyžaduje příkaz `0`.
- AUTO se mezi koly neptá na pokračování.
- PROMPTER je povinný v každém kole.
- BÁSNÍK navrhne TITLE nejpozději v prvním kole a aktualizuje ho po změně příběhu.
- Finalní `FAIL` vrací práci odpovědné roli a KRITIK kontrolu opakuje až do `PASS`.
- COVERMASTER pouze připravuje specifikaci S-coveru po finalním `PASS`; rozměr zůstává `543 × 807 px`.

---

### 2026-07-22 — Dva oficiální deníky s rozdílnými úlohami

**Rozhodnutí:** `DZIENNIK.md` je commitnutou součástí dokumentace a zaznamenává chronologický průběh a stav realizace. `docs/decision-log.md` uchovává architektonická rozhodnutí a jejich odůvodnění.

**Důvody:** Historie provedené práce má být viditelná na GitHubu, ale stavy implementace se nemají míchat s projektovými rozhodnutími.

**Dopad:** Každá významná změna workflow dostane stavový zápis v `DZIENNIK.md`; rozhodnutí měnící pravidla EasyTeam se nadále zapisují zde.

---

### 2026-07-22 — Jednosouborové nasazení v1.1

**Rozhodnutí:** Jediný `prompts/chatgpt-project-instructions.md` musí zůstat pod limitem 8000 znaků a vkládá se přímo do pole ChatGPT Project Instructions. Samotný brief pouze inicializuje stav a AUTO spouští až samostatný příkaz `0`.

**Důvody:** Živý test odhalil limit 8000 znaků v Project Instructions, automatický start bez `0` a příliš mírnou kontrolu standardní češtiny.

**Dopad:** Není potřeba loader ani duplicitní project source. Prompt je stručnější, protokol krátkých příkazů je jednoznačný a KRITIK rozlišuje tolerantní vstup UŽIVATELE od jazykově správného finálního výstupu.
