# Example: Empty context — `0` recovery

Ukázka, co se stane, když uživatel pošle `0` bez jakéhokoli předchozího kontextu.
EasyTeam se nezeptá dlouhým formulářem, ale položí jednu krátkou číselnou otázku.

## Vstupní transcript

```
Uživatel: 0
```

## Očekávané chování

EasyTeam nemá brief, téma ani styl. Místo dlouhého formuláře položí **jednu krátkou otázku**:

```
EasyTeam: Vyber téma: 1) láska 2) boj 3) smutek?
```

## Možné pokračování

### Varianta A — uživatel vybere číslo
```
Uživatel: 1
EasyTeam: Téma láska. Styl: 1) pop 2) rock 3) folk?
Uživatel: 2
EasyTeam: Jazyk: 1) česky 2) polsky 3) anglicky 4) po naszymu?
Uživatel: 1
EasyTeam: Počet kol: 1) 2 kola 2) 3 kola 3) 5 kol?
Uživatel: 0 (nebo 1 pro výchozí 2 kola)

EasyTeam: Brief: láska, rock, česky, 2 kola. Spouštím AUTO. Kolo 1/2...
```

### Varianta B — uživatel napíše `ne`
```
EasyTeam: Vyber téma: 1) láska 2) boj 3) smutek?
Uživatel: ne
EasyTeam: 1) vlastní téma 2) náhodné téma 3) zrušit
Uživatel: 1
EasyTeam: Napiš své téma:
Uživatel: měsíční krajina
EasyTeam: Téma měsíční krajina. Styl: 1) pop 2) rock 3) folk?
...
```

### Varianta C — uživatel napíše krátký brief rovnou
```
EasyTeam: Vyber téma: 1) láska 2) boj 3) smutek?
Uživatel: tema more pop cz 2
EasyTeam: Rozumím: téma moře, pop, česky, 2 kola. Spouštím AUTO...
```

## Co se NESTANE

- EasyTeam **nepošle dlouhý formulář** s 10 otázkami
- EasyTeam **nevyžaduje** `Moderátore, zahaj kolo 1`
- EasyTeam **neodmítne** `0` s tím, že nemá kontext

## Shrnutí

- `0` bez kontextu → jedna krátká číselná otázka
- Uživatel vybere číslo nebo napíše `ne` pro vlastní vstup
- Během 3-4 krátkých interakcí je hotový brief a AUTO startuje