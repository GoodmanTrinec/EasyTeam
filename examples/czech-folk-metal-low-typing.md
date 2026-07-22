# Example: Czech folk metal — AUTO se 3 plnými koly

Ukázka zkráceného transcriptu. Každý výstup BÁSNÍK v reálné session obsahuje celý aktuální text; zde jsou dlouhé verze označeny názvem verze a finální text je uveden celý na konci.

## Vstup

```text
UŽIVATEL: tema rytir metal cz 3
EasyTeam: Brief: rytíř, metal, česky, 3 kola. `total_rounds: 3`.
UŽIVATEL: GO
```

AUTO se mezi koly neptá na pokračování.

## Kolo 1/3

```text
MODERÁTOR: Kolo 1/3. TITLE zatím chybí, Lyrics a Style jsou prázdné. Cíl: vytvořit základ příběhu, refrén, hudební směr a první TITLE.
HUDEBNÍK: Epic folk metal, 140 BPM, těžké kytary, housle, hluboký mužský vokál, temný les. BÁSNÍK: krátké osmislabičné páry. PROMPTER: zdůraznit temnou cestu a sbor v refrénu.
BÁSNÍK: TITLE `Rytíř v plamenech`; odevzdává celý Lyrics verze 1 s Verse 1 a Chorus.
PROMPTER: Epic folk metal with heavy guitars, violins, deep male vocals and a steady 140 BPM pulse. Dark forest atmosphere with restrained choir harmonies in the chorus.
KRITIK: FAIL | ODPOVĚDNÁ ROLE: BÁSNÍK | CHYBA: Chorus, řádky 1–2, `ruce / duše` není přesvědčivý rým | NÁVRH OPRAVY: přepsat celý pár bez gramatického násilí.
MODERÁTOR: Ukládám TITLE, Lyrics verze 1 a Style verze 1. Slabý rým je prioritou kola 2.
```

## Kolo 2/3

```text
MODERÁTOR: Kolo 2/3. TITLE `Rytíř v plamenech`; příběh vede rytíře temným lesem, Style je folk metal 140 BPM. Cíl: opravit refrén, přidat druhou sloku a zpřesnit vokál.
HUDEBNÍK: Zachovat 140 BPM, přidat odpovědi sboru a širší housle. BÁSNÍK: sjednotit délku řádků. PROMPTER: popsat sbor bez technických poznámek v Lyrics.
BÁSNÍK: Aktualizuje TITLE na `Poslední hlídka` a odevzdává celý Lyrics verze 2: Verse 1, nový Chorus, Verse 2 a opakovaný Chorus.
PROMPTER: Epic folk metal at 140 BPM with heavy rhythm guitars, sweeping violins and deep male lead vocals. Restrained choir responses widen the chorus while the verses retain a dark forest tension.
KRITIK: PASS
MODERÁTOR: Ukládám TITLE `Poslední hlídka`, celý Lyrics verze 2 a Style verze 2. Bez nevyřešených chyb.
```

## Kolo 3/3

```text
MODERÁTOR: Kolo 3/3. TITLE `Poslední hlídka`; příběh nyní směřuje k tichému smíření. Cíl: doplnit bridge a outro, upravit TITLE podle skutečného konce a uzavřít hudební oblouk.
HUDEBNÍK: Přidat pomalé crescendo, sborové harmonie a ztišené finále. BÁSNÍK: konec nesmí působit vítězně. PROMPTER: zachovat temnou, slavnostní atmosféru.
BÁSNÍK: Aktualizuje TITLE na `Rytířův věčný pokoj` a odevzdává celý finální Lyrics včetně Verse 1, Chorus, Verse 2, Bridge a Outro.
PROMPTER: Epic folk metal at 140 BPM with heavy guitars, violins, deep male vocals and solemn choir harmonies. A dark forest atmosphere builds toward a restrained crescendo, then resolves into a quiet, non-triumphant ending.
KRITIK: PASS
MODERÁTOR: Ukládám finální TITLE, celý Lyrics a Style. Všechna 3 kola jsou dokončena.
```

## Finální kontrola a gate

```text
MODERÁTOR: TITLE odpovídá tichému konci, Lyrics je úplný a čistý, Style je anglicky a brief `rytir metal cz 3` je splněn. Spouštím final gate.
KRITIK: PASS
MODERÁTOR: `final_gate: pass`. Teprve nyní aktivuji COVERMASTER.
COVERMASTER: Připravuji specifikaci podle schváleného TITLE, příběhu, skutečného konce, stylu, emocí a symbolů.
```

## Finální výstup

```text
--- TITLE ---

Rytířův věčný pokoj

--- LYRICS ---

[Verse 1]
Rytíř v brnění z ocele
Kráčí tmou v lese směle
Měsíc kreslí cestu na štít
Osud šeptá: musíš dál jít

[Chorus]
Oheň hasne, chladne štít
Teď už nemusí dál jít
Noc mu sklání černý šál
Poslední boj tiše vzdal

[Verse 2]
Vítr válí suché listí
Úzká stezka kroky čistí
Stín se plíží mezi stromy
Nad ním mlčí dávné hromy

[Bridge]
Až se ráno dotkne skal
Odloží, co v bitvách znal
Poslední boj ztratil hlas
Pokoj našel právě včas

[Outro]
Oheň v srdci tiše spí
Les už jeho jméno ví

--- STYLE PROMPT ---

Epic folk metal at 140 BPM with heavy guitars, violins, deep male vocals and solemn choir harmonies. A dark forest atmosphere builds toward a restrained crescendo, then resolves into a quiet, non-triumphant ending.

--- COVERMASTER ---

COVERMASTER vychází z názvu `Rytířův věčný pokoj`, temného lesního příběhu, folk metalu, symbolů ohně, meče a štítu a z tichého konce bez falešného triumfu.

--- S-COVER ---

Size: 543 × 807 px
Aspect ratio: 543:807
Simplified ratio: 181:269
Text: Rytířův věčný pokoj
Prompt: Vertical Suno song cover, an armored knight at the edge of a dark forest at dawn, dim embers on a lowered sword, solemn folk metal atmosphere, cinematic shadows, no triumphant battle pose, no happy-ending rewrite.
```

## Ověřené vlastnosti

- Brief s číslem `3` způsobil přesně 3 plná kola.
- Každé kolo obsahovalo MODERÁTOR → HUDEBNÍK → BÁSNÍK → PROMPTER → KRITIK → MODERÁTOR.
- AUTO se mezi koly neptalo.
- TITLE se změnil spolu s příběhem.
- COVERMASTER se aktivoval až po samostatném finalním `PASS`.
