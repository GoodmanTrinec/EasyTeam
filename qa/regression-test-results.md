# Prompt Regression Results — v1.1 — 2026-07-22

## Souhrn

- Výsledek: **1 PASS / 0 FAIL**
- Metoda: jeden živý end-to-end acceptance test v projektu ChatGPT `Suno EasyTeam`
- Scénář: Test 28 z `qa/prompt-regression-checklist.md`
- Brief: `Michal opět hraje Old School RuneScape, punk, česky, 3 rundy`

## Výsledek testu 28

| Kontrola | Výsledek |
|---|:---:|
| Hlavní prompt má 5973 znaků a je přímo v Project Instructions | PASS |
| Project Sources neobsahují druhou kopii promptu ani loader | PASS |
| Samotný brief čeká na samostatné `0` | PASS |
| Po `0` proběhnou přesně kola `1/3`, `2/3`, `3/3` | PASS |
| Každé kolo obsahuje všech šest etap | PASS |
| PROMPTER vystoupí jednou v každém kole | PASS |
| `FAIL` z kol 1 a 2 se přenese k opravě v dalším kole | PASS |
| TITLE se po změně hlavního motivu změní z `Ještě jeden level` na `Ještě jeden quest` | PASS |
| Český výstup nepoužívá neodůvodněný tvar `Nový hry` | PASS |
| Samostatný final gate vrátí `FINAL GATE: PASS` | PASS |
| COVERMASTER a S-COVER následují až po finalním `PASS` | PASS |

## Doplňkové statické kontroly

- `prompts/chatgpt-project-instructions.md`: 5973 znaků, tedy pod limitem 8000.
- Očekávaná choreografie v testu: 3× PROMPTER, 3× KRITIK a 3× závěrečný MODERÁTOR; skutečný výstup odpovídal.
- Rozměr S-coveru zůstal `543 × 807 px`, poměr `543:807`, zjednodušený poměr `181:269`.
- Po live testu byla provedena pouze významově zpřesňující oprava formulace `celé číslice` na `celého čísla`; finální prompt tak vzrostl z 5967 na 5973 znaků. Podle rozhodnutí UŽIVATELE se druhý live test nespouštěl.
- Další scénáře checklistu nebyly v této iteraci spouštěny; podle rozhodnutí UŽIVATELE proběhl zatím pouze jeden test.
