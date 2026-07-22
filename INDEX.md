# EasyTeam — Index projektu

EasyTeam je **markdown prompt-pack pro ChatGPT Pro**, ne aplikace.
Cílem je tvorba písní pro Suno pomocí multi-agentního workflow s minimem psaní.

## Struktura

| Cesta | Obsah |
|---|---|
| README.md | Úvod, koncept, historie projektu |
| INDEX.md | **Tento soubor** — mapa celého projektu |
| DZIENNIK.md | Oficiální chronologický deník průběhu a stavu projektu |
| prompts/ | Hlavní prompt pro ChatGPT Project Instructions a definice rolí |
| prompts/roles/ | Modulární definice rolí (MODERÁTOR, BÁSNÍK, HUDEBNÍK, KRITIK, PROMPTER, COVERMASTER, UŽIVATEL) |
| workflows/ | Protokoly a pravidla interakce |
| examples/ | Ukázkové session s minimálním psaním |
| qa/ | Kritéria kvality, regresní checklisty |
| docs/ | Dokumentace workflow s ChatGPT a GitHubem |

## Interakce

- **Low-typing**: stačí krátký brief a samostatné `GO`.
- `GO` = AUTO start po načtení briefu; velikost písmen se neřeší.
- `?` = stručná nápověda.
- Čísla `0`–`9`, `ano` a `ne` nejsou globální příkazy hlavního projektu.

## Pravidla

- **Žádné placené API ani modely** nad rámec stávajícího ChatGPT Pro.
- Pokud by něco vyžadovalo platbu, EasyTeam pouze varuje a nepřipojí to.
- GitHub je primární zdroj pravdy; do repozitáře patří jen oficiální markdown, příklady, QA a konfigurace.
- Počet kol v AUTO pochází pouze z výslovného údaje o kolech nebo z koncového čísla kompaktního briefu; `94 BPM`, roky a čísla v Lyrics se ignorují. Chybějící počet znamená 3 kola.
- Samotný brief pouze inicializuje stav a čeká na samostatný příkaz `GO`; bez něj AUTO nezačne.
- Plné kolo je **MODERÁTOR → HUDEBNÍK → BÁSNÍK → PROMPTER → KRITIK → MODERÁTOR** a AUTO se mezi koly neptá.
- Stav obsahuje `current_title`, `current_lyrics` a `current_style`; TITLE vznikne nejpozději v prvním kole a sleduje změny příběhu.
- Po všech kolech následuje samostatný final gate KRITIK; COVERMASTER se aktivuje pouze po `PASS`.
- Výstupem je vždy **TITLE → Lyrics → Style Prompt → COVERMASTER → S-cover**.
- S-cover používá přesnou velikost **543 × 807 px**, poměr **543:807** a zjednodušený poměr **181:269**.
- Vstup toleruje mix PL/CZ/EN a nářečí po naszymu.
- Český výstup je standardní čeština, pokud brief výslovně nepožaduje nářečí nebo hovorový styl.
- Jediný `prompts/chatgpt-project-instructions.md` se vkládá přímo do Project Instructions a musí zůstat pod limitem 8000 znaků.

## Plánované artefakty

- prompts/chatgpt-project-instructions.md — hlavní prompt vkládaný přímo do Project Instructions
- prompts/roles/moderator.md — role MODERÁTOR
- prompts/roles/poet.md — role BÁSNÍK
- prompts/roles/musician.md — role HUDEBNÍK
- prompts/roles/prompter.md — role PROMPTER
- prompts/roles/critic.md — role KRITIK
- prompts/roles/covermaster.md — role COVERMASTER
- prompts/roles/user.md — role UŽIVATEL
- workflows/short-commands.md — protokol krátkých příkazů
- examples/czech-folk-metal-low-typing.md — ukázka low-typing session
- examples/pop-ballad-auto.md — ukázka plného AUTO bez mezikroků
- examples/empty-go-recovery.md — ukázka `GO` bez briefu
- qa/critic-rubric.md — kritéria hodnocení kvality
- qa/prompt-regression-checklist.md — regresní checklist
- qa/regression-test-results.md — poslední výsledky logických regresních testů
- docs/github-workflow.md — workflow s GitHubem
- docs/decision-log.md — rozhodovací deník
- DZIENNIK.md — chronologický průběh, stav implementace a odkazy na releasové commity
