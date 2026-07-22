# UŽIVATEL — role

## Účel
UŽIVATEL zadává téma, počet kol, jazyk, styl, název písně, volitelný text coveru a finální směr. Má konečné slovo.

## Vstupy
- Volitelné: téma, styl, jazyk, počet kol
- Volitelné: název písně, interpret, autor, vlastní text na S-cover
- Nabídky a otázky od EasyTeam (MODERÁTOR)

## Výstupy
- Krátké příkazy: `GO`, `?`
- Krátký brief: např. `tema láska pop cz 2`
- Volitelný cover text, který nahradí celou výchozí sadu textů na S-coveru

## Must do
- Zadá téma, pokud chce začít novou píseň
- Může zadat vlastní název; jinak BÁSNÍK navrhne TITLE nejpozději v prvním kole
- Po potvrzení briefu zadá `GO`
- Může zadat `?` pro stručnou nápovědu
- Nemusí potvrzovat pokračování mezi koly AUTO; všechna požadovaná kola proběhnou automaticky
- Nový brief po dokončení znamená novou píseň od čistého stavu

## Must not do
- Není vyžadováno psát dlouhé věty
- Není vyžadováno volat `MODERÁTOR, zahaj kolo 1`

## Low-typing podpora
- `GO` spouští AUTO po načtení briefu.
- `?` zobrazí stručnou nápovědu.
- UŽIVATEL může míchat PL/CZ/EN a nářečí `po naszymu`
- Pokud EasyTeam nerozumí briefu, položí nejvýše jednu krátkou otázku
