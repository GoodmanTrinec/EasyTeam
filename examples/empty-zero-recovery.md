# Example: Empty context — `0` recovery

Ukázka, co se stane, když UŽIVATEL pošle `0` bez jakéhokoli předchozího kontextu.
EasyTeam se nezeptá dlouhým formulářem, ale položí jednu krátkou číselnou otázku.

## Vstupní transcript

```
UŽIVATEL: 0
```

## Očekávané chování

EasyTeam nemá brief, téma ani styl. Místo dlouhého formuláře položí **jednu krátkou otázku**:

```
EasyTeam: Vyber téma: 1) láska 2) boj 3) smutek?
```

## Možné pokračování

### Varianta A — UŽIVATEL vybere číslo
```
UŽIVATEL: 1
EasyTeam: Téma láska. Styl: 1) pop 2) rock 3) folk?
UŽIVATEL: 2
EasyTeam: Jazyk: 1) česky 2) polsky 3) anglicky 4) po naszymu?
UŽIVATEL: 1
EasyTeam: Brief: láska, rock, česky. Počet kol nebyl zadán, používám default 2. Spouštím AUTO. Kolo 1/2...
EasyTeam: [provede dvě plná kola bez otázky mezi nimi, potom final gate]
```

### Varianta B — UŽIVATEL napíše `ne`
```
EasyTeam: Vyber téma: 1) láska 2) boj 3) smutek?
UŽIVATEL: ne
EasyTeam: 1) vlastní téma 2) náhodné téma 3) zrušit
UŽIVATEL: 1
EasyTeam: Napiš své téma:
UŽIVATEL: měsíční krajina
EasyTeam: Téma měsíční krajina. Styl: 1) pop 2) rock 3) folk?
...
```

### Varianta C — UŽIVATEL napíše krátký brief rovnou
```
EasyTeam: Vyber téma: 1) láska 2) boj 3) smutek?
UŽIVATEL: tema more pop cz 2
EasyTeam: Rozumím: téma moře, pop, česky, 2 kola. Spouštím AUTO...
```

## Co se NESTANE

- EasyTeam **nepošle dlouhý formulář** s 10 otázkami
- EasyTeam **nevyžaduje** `MODERÁTOR, zahaj kolo 1`
- EasyTeam **neodmítne** `0` s tím, že nemá kontext

## Shrnutí

- `0` bez kontextu → jedna krátká číselná otázka
- UŽIVATEL vybere číslo nebo napíše `ne` pro vlastní vstup
- Chybějící počet kol → bezpečný default 2 bez další otázky
- Po doplnění minimálního briefu AUTO provede všechna kola bez dotazu mezi nimi
