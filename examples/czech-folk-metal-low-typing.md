﻿# Example: Czech folk metal — low typing

Ukázka, jak uživatel zadá krátký brief a pak už jen mačká `0` a `ano`.

## Vstupní transcript

```
Uživatel: tema rytir metal cz 3

EasyTeam: Rozumím: téma rytíř, metal, česky, 3 kola. Spustit AUTO? (0 = ano, 1 = změnit téma, 2 = změnit styl)
Uživatel: 0
```

## Průběh (AUTO režim)

### Kolo 1
```
Moderátor: Kolo 1/3. Téma: rytíř, metal, česky.
Hudebník: Folk metal, 140 BPM, kytary, housle, houslový klíč, temný lesní motiv.
Básník:
[Verse 1]
Rytíř v brnění z ocele
Kráčí tmou v lese cele
Měsíc svítí na jeho štít
Osud už mu káže jít

[Chorus]
Oheň v srdci, meč v ruce
Statečnost je v jeho duše
Noc je dlouhá, cesta tmavá
Rytíř ví, co ho čekává

Kritik: CHYBA: řádek 6 "duše" — měl by být "duši" (6. pád). NÁVRH OPRAVY: "Statečnost je v jeho duši"
Básník: Opraveno.

Kritik: SCHVÁLENO (s opravou)
```

### Kolo 2
```
Moderátor: Kolo 2/3. Vylepšujeme refrén a přidáváme sloku 2.
Hudebník: Přidat sborové vokály, zrychlit na 150 BPM v refrénu.
Básník:
[Verse 2]
Vítr válí suché listí
Cesta před ním se mi čistí
Stín se plíží mezi stromy
Rytíř jde dál, je nezlomný

[Chorus]
Oheň v srdci, meč v ruce (vylepšený)
Statečnost je v jeho duši
Noc je dlouhá, cesta tmavá
Rytíř ví, co ho čeká (zkráceno pro lepší rytmus)

Kritik: SCHVÁLENO
```

### Kolo 3
```
Moderátor: Kolo 3/3. Finální doladění.
Hudebník: Přidat crescendo na konci, fade-out.
Básník: Bridge:
[Bridge]
Až svitne den
Složí svůj sen
Rytířův boj
Dokončil svůj stroj

Kritik: CHYBA: řádek 4 "stroj" — rým násilný, "svůj sen" / "svůj stroj" — sen × stroj se nerýmuje.
NÁVRH OPRAVY: "Rytířův boj / Skončil jako dávný hrdina boj"
Kritik: nebo lépe zachovat strukturu: "Rytířův boj / Přinesl mu věčný pokoj"
Básník: Opraveno na:
[Bridge]
Až svitne den
Složí svůj sen
Rytířův boj
Přinesl mu věčný pokoj

Kritik: SCHVÁLENO
```

## Finální výstup

```
--- TITLE ---

Rytířův věčný pokoj

--- LYRICS ---

[Verse 1]
Rytíř v brnění z ocele
Kráčí tmou v lese cele
Měsíc svítí na jeho štít
Osud už mu káže jít

[Chorus]
Oheň v srdci, meč v ruce
Statečnost je v jeho duši
Noc je dlouhá, cesta tmavá
Rytíř ví, co ho čeká

[Verse 2]
Vítr válí suché listí
Cesta před ním se mi čistí
Stín se plíží mezi stromy
Rytíř jde dál, je nezlomný

[Chorus]
Oheň v srdci, meč v ruce
Statečnost je v jeho duši
Noc je dlouhá, cesta tmavá
Rytíř ví, co ho čeká

[Bridge]
Až svitne den
Složí svůj sen
Rytířův boj
Přinesl mu věčný pokoj

[Outro]
Oheň v srdci hasne již
Rytíř došel, našel klid

--- STYLE PROMPT ---

Epic folk metal, heavy guitars and violins, deep male vocals, 140 BPM, dark forest atmosphere, building to a crescendo with choir-like harmonies.

--- AVOID / NEGATIVE PROMPT ---

No modern synthesizers, no electronic drums, no pop elements.

--- COVERMASTER ---

COVERMASTER vychází z názvu "Rytířův věčný pokoj", temného lesního příběhu, češtiny, folk metalu, symbolů ohně, meče, štítu a klidného konce. Cover nesmí změnit konec na triumfální vítězství; rytíř nachází tichý pokoj po boji.

--- S-COVER ---

Size: 543 × 807 px
Aspect ratio: 543:807
Simplified ratio: 181:269
Text: Rytířův věčný pokoj
Prompt: Vertical Suno song cover, an armored knight standing at the edge of a dark forest at dawn, dim ember glow on a lowered sword, quiet solemn folk metal mood, cinematic shadows, no triumphant battle pose, no happy ending rewrite.
```

## Shrnutí

- Uživatel napsal jen `tema rytir metal cz 3` a poté `0`
- Vše ostatní bylo `ano` / `0` / číselné volby
- Výstupem jsou Lyrics, Style Prompt, COVERMASTER a S-cover připravené pro Suno workflow
