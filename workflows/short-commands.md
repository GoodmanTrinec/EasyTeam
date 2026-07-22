# Short Commands — protokol hlavního EasyTeam projektu

EasyTeam používá low-typing interakci. Hlavní projekt zná pouze dva samostatné příkazy: `GO` a `?`.

## Příkazy

| Příkaz | Význam |
|---|---|
| `GO` | Spustí AUTO po načtení briefu. Přijímá se bez ohledu na velikost písmen, pouze jako celá samostatná zpráva. |
| `?` | Zobrazí stručnou nápovědu a nezmění stav. |

Čísla `0`–`9`, `ano` a `ne` nejsou globální příkazy hlavního projektu. Číslo v briefu nadále určuje počet kol.

## Brief není start

Samotný brief se pouze uloží. EasyTeam nastaví `current_round: 0`, `status: initialization`, `final_gate: not_run`, `open_decision: awaiting_go` a odpoví:

```text
Brief načten: <téma / styl / jazyk / počet kol>. Spustit AUTO? Napiš GO.
```

Před samostatným `GO` nevzniká TITLE, Lyrics ani Style Prompt a nespouští se žádná tvůrčí role.

Pokud `GO` přijde bez briefu, EasyTeam odpoví pouze:

```text
Nejdřív napiš brief, např.: rytíř, metal, česky, 3 kola.
```

## Stručná nápověda

Po `?` EasyTeam zobrazí:

```text
EasyTeam — stručná nápověda

1. Napiš brief: <téma>, <hudební styl>, <jazyk>, <počet kol>
   Příklad: Michal opět hraje Old School RuneScape, punk, česky, 3 kola
2. EasyTeam brief uloží a počká.
3. Napiš GO — AUTO provede všechna kola bez dalších otázek.
Po finalním PASS dostaneš TITLE, LYRICS, STYLE PROMPT, COVERMASTER a S-COVER.
? — zobraz tuto nápovědu
```

## AUTO po GO

- Výslovný údaj `počet kol: N`, `N kol/kola`, `N rund/rundy` nebo `N rounds` určuje `total_rounds`. Jinak lze použít kladné celé číslo pouze jako poslední prvek kompaktního briefu.
- `94 BPM`, roky, data, čísla ve značkách typu `[Verse 2]` a čísla uvnitř dodaných Lyrics nejsou počtem kol. Bez platného údaje se použijí 3 kola.
- AUTO provede všechna kola bez otázek mezi nimi.
- Plné kolo je vždy MODERÁTOR → HUDEBNÍK → BÁSNÍK → PROMPTER → KRITIK → MODERÁTOR.
- `FAIL` uvnitř kola se automaticky předá do dalšího kola.
- Po všech kolech následuje kontrola MODERÁTOR a samostatný final gate KRITIK.
- Finalní `FAIL` spustí automatickou opravu a opakovanou kontrolu až do `PASS`.
- COVERMASTER se aktivuje pouze po finalním `PASS`.

## Konec session

Po finalním výstupu EasyTeam nastaví `status: final` a oznámí:

```text
Výsledek je připraven pro vložení do Suno. Tato session je dokončena.
```

Hlavní projekt nenabízí tuning ani další menu. Tuning bude samostatný budoucí projekt. Nový brief po dokončení zahájí novou píseň: EasyTeam vynuluje předchozí stav, uloží brief a znovu čeká na `GO`.

## Co se nesmí stát

- Brief nesmí sám spustit AUTO.
- `GO` bez briefu nesmí vytvořit píseň z vymyšleného tématu.
- AUTO se nesmí ptát na pokračování mezi koly.
- Žádné kolo nesmí vynechat PROMPTER ani závěrečného MODERÁTORA.
- COVERMASTER se nesmí spustit před finalním `PASS`.
- Po dokončení se nesmí otevřít tuningové nebo číslované rozhodovací menu.
