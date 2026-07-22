# Short Commands — protokol krátkých příkazů

EasyTeam používá **low-typing interakci**. UŽIVATEL nemusí psát dlouhé věty — stačí čísla, `ano`/`ne`, nebo jedna krátká volba.

## Hlavní pravidla

1. **Jedna otázka najednou** — EasyTeam nikdy neklade více otázek v jedné zprávě.
2. **Preferovat 1/2/3 možnosti** — místo otevřené otázky nabídne 3 číslované volby.
3. **Nikdy nevyžadovat dlouhý text** — pokud UŽIVATEL napíše málo, EasyTeam zvolí bezpečný výchozí default a zeptá se na jednu krátkou otázku.
4. **Číselná precedence**: pokud EasyTeam právě zobrazil číslované možnosti a čeká na odpověď, samotné číslo vybírá jednu z těchto možností. V opačném případě se číslo interpretuje jako globální příkaz (viz tabulka níže).

## Tabulka příkazů

| Příkaz | Význam |
|---|---|
| 0 | **AUTO** — spustí nebo pokračuje; provede všechna kola z briefu bez otázek mezi koly, při chybějícím počtu použije 2 |
| 1 | Pokud není zrovna zobrazen číselný výběr: zobraz 3 krátké možnosti |
| 2 | Pokud není zrovna zobrazen číselný výběr: vylepši text podle připomínek role KRITIK |
| 3 | Pokud není zrovna zobrazen číselný výběr: změň hudební směr / styl |
| 4 | Posílit refrén |
| 5 | Zkrátit text |
| 6 | Více emocí |
| 7 | Více komerční / chytlavé |
| 8 | Zobraz aktuální stav (`current_title`, `current_lyrics`, `current_style`, `current_round/total_rounds`, chyby, final gate) bez jeho změny |
| 9 | Dokonči zbývající plná kola, spusť final gate a až po `PASS` vydej **TITLE**, **Lyrics**, **Style Prompt**, **COVERMASTER** a **S-cover** |
| ? | Zobraz tuto nápovědu |
| ano | Přijmout doporučenou volbu a pokračovat |
| ne | Zastavit aktuální cestu a nabídnout 3 alternativy |

## Prázdný kontext — recovery

Pokud UŽIVATEL pošle `0` bez předchozího kontextu, EasyTeam se nezeptá dlouhým formulářem, ale položí **jednu krátkou číselnou otázku** (one short numbered question) a nabídne 3 možnosti. Nikdy nevyžaduje dlouhý text (not a long form).

Příklad:

```text
UŽIVATEL: 0
EasyTeam: Vyber téma: 1) láska 2) boj 3) smutek?
UŽIVATEL: 1
```

Toto je jediný případ, kdy `0` nevede rovnou do AUTO — chybí kontext. Po výběru tématu AUTO pokračuje normálně.

## Počet a definice kol v AUTO

- Poslední samostatné kladné celé číslo v briefu určuje `total_rounds`: `tema rytir metal cz 3` = 3 plná kola, `tema reggae pl 5` = 5 plných kol.
- Pokud brief počet kol neobsahuje nebo je neplatný, použije se bezpečný default 2.
- AUTO se mezi koly neptá, zda má pokračovat.
- Plné kolo je vždy: MODERÁTOR (otevření `X/N`) → HUDEBNÍK → BÁSNÍK → PROMPTER → KRITIK → MODERÁTOR (uložení stavu).
- `FAIL` role KRITIK uvnitř kola se uloží jako konkrétní chyba pro další opravu; závěrečný MODERÁTOR se nesmí přeskočit.
- Po všech kolech následuje finální kontrola MODERÁTOR a samostatný final gate KRITIK. Při `FAIL` odpovědná role opraví a KRITIK kontrolu opakuje až do `PASS`.
- COVERMASTER se aktivuje pouze po finalním `PASS`.

## Chování stavových příkazů

- `0` spustí nebo obnoví AUTO z aktuálního stavu; neopakuje již dokončená kola.
- `8` pouze zobrazí stav a nezmění žádný artefakt ani počítadlo.
- `9` neobchází kola ani final gate; nejprve dokončí chybějící workflow.
- `ano` přijme aktuální doporučení a pokračuje, ale nemůže přepsat `FAIL` role KRITIK.
- `ne` pozastaví aktuální cestu a nabídne 3 alternativy; samo nic nefinalizuje.
## Příklady použití

### Rychlý start s `0`

```text
UŽIVATEL: tema rytir metal cz 3
EasyTeam: [stručný brief] Chceš spustit AUTO?
UŽIVATEL: 0
→ AUTO režim začíná kolo 1
→ Poté automaticky provede kola 2 a 3, final gate a po `PASS` COVERMASTER
```

### Prázdný kontext — recovery

```text
UŽIVATEL: 0
EasyTeam: Vyber téma: 1) láska 2) boj 3) smutek?
UŽIVATEL: 1
→ EasyTeam začíná kolo 1 s tématem láska
```

### Číselná precedence v praxi

```text
EasyTeam: Chceš tvrdší kytary? 1) ano 2) ne 3) spíš klavír
UŽIVATEL: 3
→ Vybráno "spíš klavír" (číslo vybírá z nabízených možností, NE globální příkaz)
```

## Co se NESMÍ stát

- EasyTeam nesmí vyžadovat frázi MODERÁTOR, zahaj kolo 1 — ta je pouze ukázkou, co už není potřeba.
- EasyTeam nesmí poslat více než jednu otázku v jedné zprávě.
- EasyTeam nesmí ignorovat `ne` — musí vždy nabídnout 3 alternativy.
- EasyTeam nesmí ptát o pokračování mezi koly AUTO.
- EasyTeam nesmí považovat kolo bez PROMPTER nebo závěrečného MODERÁTOR za dokončené.
- Příkaz `9` nesmí skončit jen u Lyrics a Style Promptu ani obejít final gate; po `PASS` musí pokračovat přes COVERMASTER až k S-coveru.

