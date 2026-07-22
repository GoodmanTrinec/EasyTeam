# Prompt Regression Results — v1.1 baseline — 2026-07-22

## Souhrn

- Výsledek baseline: **1 PASS / 0 FAIL**
- Metoda: jeden živý end-to-end acceptance test před změnou startu z `0` na `GO` v projektu ChatGPT `Suno EasyTeam`
- Scénář: Test 28 z `qa/prompt-regression-checklist.md`
- Brief: `Michal opět hraje Old School RuneScape, punk, česky, 3 rundy`

Tento záznam dokumentuje poslední skutečně provedený live test. Nová varianta s příkazem `GO` vyžaduje nový live acceptance test po vložení aktuálního promptu do Project Instructions; níže uvedené výsledky se proto nepřepisují ani nevydávají za test nové varianty.

## Výsledek testu 28

| Kontrola | Výsledek |
|---|:---:|
| Hlavní prompt má 5973 znaků a je přímo v Project Instructions | PASS |
| Project Sources neobsahují druhou kopii promptu ani loader | PASS |
| Samotný brief čekal na tehdejší samostatné `0` | PASS |
| Po tehdejším `0` proběhla přesně kola `1/3`, `2/3`, `3/3` | PASS |
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

## Stav změny `GO`

- Dokumentace, role, workflow, příklady a checklist byly převedeny z `0` na samostatné `GO`.
- `GO` má fungovat bez ohledu na velikost písmen, ale pouze jako celá zpráva po oříznutí.
- Hlavní projekt nabízí pouze `GO` a `?`; dřívější `0`–`9`, `ano` a `ne` již nejsou globálními příkazy.
- Aktuální hlavní prompt má 6126 znaků a 6616 bajtů v UTF-8, tedy zůstává pod limitem 8000 znaků.
- Výsledek nového live testu: **NESPUŠTĚNO**. Variantu `GO` nelze označit jako `PASS` před skutečným provedením Testu 28.
