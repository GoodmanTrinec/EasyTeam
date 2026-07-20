﻿﻿# EasyTeam — Index projektu

EasyTeam je **markdown prompt-pack pro ChatGPT Pro**, ne aplikace.  
Cílem je tvorba písní pro Suno pomocí multi-agentního workflow s minimem psaní.

## Struktura

| Cesta | Obsah |
|---|---|
| README.md | Úvod, koncept, historie projektu |
| INDEX.md | **Tento soubor** — mapa celého projektu |
| prompts/ | Hlavní prompt pro ChatGPT Project Instructions |
| prompts/roles/ | Modulární definice rolí (MODERÁTOR, BÁSNÍK, HUDEBNÍK, KRITIK, PROMPTER, COVERMASTER, UŽIVATEL) |
| workflows/ | Protokoly a pravidla interakce |
| examples/ | Ukázkové session s minimálním psaním |
| qa/ | Kritéria kvality, regresní checklisty |
| docs/ | Dokumentace workflow s ChatGPT a GitHubem |

## Interakce

- **Low-typing**: stačí `0`, `ano`/`ne`, nebo číselná volba.
- `0` = AUTO start nebo pokračování
- `ano` = přijmout doporučenou volbu
- `ne` = zastavit a nabídnout 3 alternativy
- 1/2/3 = výběr z nabízených možností
- ? = nápověda

## Pravidla

- **Žádné placené API ani modely** nad rámec stávajícího ChatGPT Pro.
- Pokud by něco vyžadovalo platbu, EasyTeam pouze varuje a nepřipojí to.
- GitHub je primární zdroj pravdy; do repozitáře patří jen oficiální markdown, příklady, QA a konfigurace.
- Výstupem je vždy **Lyrics → Style Prompt → COVERMASTER → S-cover**.
- S-cover používá přesnou velikost **543 × 807 px**, poměr **543:807** a zjednodušený poměr **181:269**.
- Vstup toleruje mix PL/CZ/EN a nářečí po naszymu.

## Plánované artefakty

- prompts/chatgpt-project-instructions.md — hlavní prompt pro ChatGPT
- prompts/roles/moderator.md — role MODERÁTOR
- prompts/roles/poet.md — role BÁSNÍK
- prompts/roles/musician.md — role HUDEBNÍK
- prompts/roles/prompter.md — role PROMPTER
- prompts/roles/critic.md — role KRITIK
- prompts/roles/covermaster.md — role COVERMASTER
- prompts/roles/user.md — role UŽIVATEL
- workflows/short-commands.md — protokol krátkých příkazů
- examples/czech-folk-metal-low-typing.md — ukázka low-typing session
- examples/pop-ballad-yes-no.md — ukázka s ano/ne
- examples/empty-zero-recovery.md — ukázka prázdného startu
- qa/critic-rubric.md — kritéria hodnocení kvality
- qa/prompt-regression-checklist.md — regresní checklist
- docs/github-workflow.md — workflow s GitHubem
- docs/decision-log.md — rozhodovací deník
