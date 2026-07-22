# Prompt Regression Results — 2026-07-22

## Souhrn

- Výsledek: **27 PASS / 0 FAIL**
- Metoda: statická logická kontrola committed promptů, rolí, workflow, příkladů a QA pravidel
- Rozsah: všech 27 testů z `qa/prompt-regression-checklist.md`
- Doplňkové kontroly: žádné staré pravidlo pevně vynucující 2 kola, žádný UTF-8 BOM ve sledovaných souborech, `git diff --check` bez chyb

Tato kontrola ověřuje, že dokumentovaná choreografie a stavová pravidla jsou vzájemně konzistentní. Nejde o živé spuštění promptu v externím ChatGPT Project; takové end-to-end ověření vyžaduje ruční vložení hlavního promptu do projektu.

## Výsledky

| Test | Scénář | Výsledek |
|---:|---|:---:|
| 1 | `0` s briefem a 2 koly | PASS |
| 2 | `0` bez kontextu | PASS |
| 3 | Šestietapové oddělení rolí | PASS |
| 4 | Přísnost KRITIK a konkrétní chyby | PASS |
| 5 | Finální oddělení TITLE / Lyrics / Style / COVERMASTER / S-cover | PASS |
| 6 | Style Prompt vždy anglicky | PASS |
| 7 | Žádná placená API nebo modely | PASS |
| 8 | Žádné klonování žijících umělců | PASS |
| 9 | Jedna otázka najednou | PASS |
| 10 | Smíšený vstup PL/CZ/EN/po naszymu | PASS |
| 11 | Číselná precedence | PASS |
| 12 | Příkaz `ano` | PASS |
| 13 | Časování aktivace COVERMASTER | PASS |
| 14 | Rozměr a poměr S-coveru | PASS |
| 15 | Vlastní text S-coveru nahrazuje default | PASS |
| 16 | S-cover zachovává skutečný konec | PASS |
| 17 | Size-only reference se nekopíruje obsahově | PASS |
| 18 | Brief s 1 kolem | PASS |
| 19 | Brief se 3 koly | PASS |
| 20 | Brief s 5 koly | PASS |
| 21 | Brief bez počtu kol používá default 2 | PASS |
| 22 | KRITIK vrací `FAIL` uvnitř kola | PASS |
| 23 | Final KRITIK vrací `FAIL` a kontrolu opakuje | PASS |
| 24 | PROMPTER je v každém kole | PASS |
| 25 | COVERMASTER nezačne před finalním `PASS` | PASS |
| 26 | TITLE se změní po změně příběhu | PASS |
| 27 | Příkazy `0`, `8`, `9`, `ano`, `ne` | PASS |

## Důkazy logické kontroly

- Hlavní prompt načítá `total_rounds` z briefu a při chybějícím počtu používá `2`.
- Plné kolo je ve všech hlavních dokumentech definováno jako MODERÁTOR → HUDEBNÍK → BÁSNÍK → PROMPTER → KRITIK → MODERÁTOR.
- `current_title`, `current_lyrics` a `current_style` jsou povinnou součástí stavu.
- PROMPTER aktualizuje celý anglický Style Prompt v každém kole.
- Finalní `FAIL` nemá pevný limit oprav a blokuje COVERMASTER.
- Příkazy `0`, `9` ani `ano` nemohou obejít chybějící kola nebo final gate; `8` stav pouze zobrazuje a `ne` nabízí alternativy.
- COVERMASTER připravuje specifikaci S-coveru až při `final_gate: pass`.
- Rozměr S-coveru zůstává `543 × 807 px`, poměr `543:807`, zjednodušený poměr `181:269`.
