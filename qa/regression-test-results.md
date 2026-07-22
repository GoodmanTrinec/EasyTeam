# Prompt Regression Results — v1.1 — 2026-07-22

## Aktuální live Test 29 — přepracování staré písně 2+1

- Výsledek: **PASS**
- Metoda: živý test v projektu ChatGPT `Suno EasyTeam`
- Materiál: starší český text `MUŽ, KTERÝ PRODÁVAL VČEREJŠEK`
- Styl obsahoval `94 BPM` a zdrojové značky `[Verse 1]`, `[Verse 2]`
- Průběh: dvě původní kola + jedna dodatečná úplná revize `Kolo 3/3` bez nápovědy o konkrétní chybě

| Kontrola | Výsledek |
|---|:---:|
| Původní dvě kola obsahovala všech šest povinných etap | PASS |
| PROMPTER aktualizoval Style Prompt v obou původních kolech | PASS |
| Po dvou kolech workflow provedl samostatný final gate | PASS |
| Externí kontrola odhalila přehlédnutý chybný řádek `její tvář vybledne, jako by nebylo` | FAIL po 2 kolech |
| Dodatečné `Kolo 3/3` bylo spuštěno bez označení chybného řádku | PASS |
| Třetí kolo samo našlo uvedený řádek i další jazykové a významové slabiny | PASS |
| Třetí kolo obsahovalo MODERÁTOR → HUDEBNÍK → BÁSNÍK → PROMPTER → KRITIK → MODERÁTOR | PASS |
| BÁSNÍK aktualizoval celý text a PROMPTER celý anglický Style Prompt | PASS |
| Nový samostatný final gate skončil `PASS` | PASS |
| COVERMASTER následoval až po novém finalním `PASS` | PASS |
| Session skončila bez tuningového menu | PASS |

### Závěr UŽIVATELE a rozhodnutí

Live Test 2+1 potvrdil, že třetí plné kolo výsledek skutečně zlepšuje, místo aby pouze opakovalo předchozí hodnocení. UŽIVATEL schválil výsledek testu jako `PASS` a rozhodl o změně bezpečného defaultu ze 2 na 3 kola.

Test ještě použil výslovné `Počet kol: 2 kola`, aby starý parser nezaměnil `94 BPM` za počet kol; třetí kolo bylo spuštěno samostatně. Nová pravidla pro ignorování BPM a čísel v Lyrics byla doplněna až po testu a vyžadují další live spuštění bez výslovného počtu kol.

## Předchozí live Test 28 s `GO`

- Výsledek aktuálního live Testu 28 s `GO`: **1 PASS / 0 FAIL**
- Metoda: jeden nový živý end-to-end acceptance test v projektu ChatGPT `Suno EasyTeam`
- Scénář: Test 28 z `qa/prompt-regression-checklist.md`
- Brief: `Michal opět hraje Old School RuneScape, punk, česky, 3 rundy`

## Výsledek aktuálního Testu 28 s `GO`

| Kontrola | Výsledek |
|---|:---:|
| Project Instructions obsahují aktuální prompt o 6126 znacích | PASS |
| Samotný brief nevytvořil artefakty a vyžádal samostatné `GO` | PASS |
| Po `GO` proběhla přesně kola `1/3`, `2/3`, `3/3` | PASS |
| Každé kolo obsahovalo MODERÁTOR → HUDEBNÍK → BÁSNÍK → PROMPTER → KRITIK → MODERÁTOR | PASS |
| PROMPTER vystoupil právě jednou v každém kole | PASS |
| `FAIL` z kol 1 a 2 byl přenesen do dalšího kola | PASS |
| Samostatný final gate skončil `PASS` | PASS |
| TITLE, LYRICS, STYLE PROMPT, COVERMASTER a S-COVER vznikly ve správném pořadí | PASS |
| COVERMASTER následoval až po finalním `PASS` | PASS |
| Rozměr S-coveru zůstal `543 × 807 px`, `543:807`, `181:269` | PASS |
| Výstup neobsahoval chybný tvar `Nový hry` | PASS |
| Session skončila bez tuningového menu | PASS |
| UŽIVATEL ověřil výsledek v Suno a zpracoval S-cover | PASS |
| UŽIVATEL označil praktický výsledek za povedený | PASS |

### Akceptované tvůrčí posouzení

KRITIK v závěrečném kole označil dvojici `dnes / quest` za funkční rým. UŽIVATEL potvrdil, že ve svižném českém punkovém podání zní dostatečně podobně; výsledek je proto přijat jako záměrný přibližný rým, nikoli jako chyba workflow.

### Praktická akceptace

UŽIVATEL otestoval finální TITLE, Lyrics a Style Prompt v Suno a podle specifikace vytvořil S-cover. Výsledný song i celkový výstup vyhodnotil pozitivně. Test proto prošel nejen strukturální kontrolou, ale také praktickou uživatelskou akceptací.

## Historický baseline před změnou `0` → `GO`

### Výsledek historického testu 28

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
- Výsledek nového live Testu 28: **PASS**. Rým `dnes / quest` byl po poslechu UŽIVATELEM přijat jako funkční pro svižný punkový kontext.
