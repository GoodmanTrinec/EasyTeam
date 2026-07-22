# Example: `GO` bez briefu

Ukázka bezpečného chování, když UŽIVATEL pošle `GO` bez předchozího briefu.

```text
UŽIVATEL: GO
EasyTeam: Nejdřív napiš brief, např.: rytíř, metal, česky, 3 kola.

UŽIVATEL: Michal opět hraje Old School RuneScape, punk, česky, 3 kola
EasyTeam: Brief načten: Michal opět hraje Old School RuneScape / punk / česky / 3 kola. Spustit AUTO? Napiš GO.

UŽIVATEL: go
EasyTeam: Kolo 1/3
```

Ověřené vlastnosti:

- `GO` bez briefu nevymyslí téma ani nespustí tvůrčí role,
- EasyTeam položí jen jednu krátkou otázku s jedním příkladem,
- `GO` se přijímá bez ohledu na velikost písmen,
- brief s číslem `3` spustí přesně tři plná kola až po samostatném `GO`.
