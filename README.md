# EasyTeam

EasyTeam je markdown prompt-pack pro ChatGPT Project. Slouží k tvorbě písní pro Suno pomocí více specializovaných rolí a low-typing workflow.

## Stručná historie projektu

EasyTeam vznikl jako praktický způsob tvorby písní pro Suno. Původně šlo o jednoduchý postup: uživatel zadal téma, hudební styl a jazyk a AI vytvořila text písně.

Brzy se však ukázalo, že jedna odpověď často nestačí. Text mohl mít slabé rýmy, nevyrovnaný rytmus, příliš obecné obraty nebo hudební styl, který přesně neodpovídal zamýšlené atmosféře.

Proto se práce rozdělila mezi několik specializovaných rolí:

- **Hudebník** navrhuje žánr, tempo, nástroje, náladu, strukturu skladby a způsob vedení vokálu.
- **Básník** píše text a soustředí se na rýmy, rytmus, emoce a zpěvnost.
- **Prompt specialista** připravuje hudební zadání pro Suno.
- **Kritik** hledá slabá místa, kontroluje rýmy, rytmus, zpěvnost a gramatickou správnost.
- **Moderátor** řídí jednotlivá kola a hlídá, aby každá nová verze byla skutečně lepší.
- **COVERMASTER** vytváří finální S-cover až po schválení Lyrics, Style Promptu a názvu písně.
- **Uživatel** určuje téma, počet kol, jazyk, styl, název a konečný směr skladby.

Tak vznikl systém tvůrčích kol. Na začátku každého kola Moderátor shrne aktuální text a hudební styl. Hudebník, Básník a Kritik spolupracují na lepší verzi. COVERMASTER se těchto skladatelských kol neúčastní; aktivuje se až po finálním schválení písně.

Finální workflow je:

**LYRICS → STYLE PROMPT → COVERMASTER → S-COVER**

## S-cover

S-cover je vertikální Suno song cover vytvořený podle názvu písně, lyrics a příběhu, jazyka, hudebního stylu, emocí, symbolů a konce příběhu.

- Přesná referenční velikost: **543 × 807 px**
- Přesný poměr stran: **543:807**
- Zjednodušený poměr stran: **181:269**
- Staré poměry **443:591** a obecný **3:4** jsou neplatné

COVERMASTER nesmí měnit význam příběhu ani vytvářet falešně pozitivní konec. Pokud je dodaný obrázek pouze referencí velikosti nebo poměru stran, COVERMASTER ho nesmí kopírovat jako vizuální obsah.

### Text na S-coveru

- Výchozí text: `TITLE AND ARTIST_IF_EXISTS AND AUTHOR_IF_EXISTS`
- Název písně je vždy zahrnut.
- Interpret se uvádí pouze tehdy, pokud ho uživatel zadal.
- Autor se uvádí pouze tehdy, pokud ho uživatel zadal.
- Pokud uživatel dodá vlastní text pro cover, tento text nahradí celou výchozí sadu textů.
- Při vlastním textu použij přesně dodaný text a nepřidávej nic dalšího.

## Role Kritika

Kritik je hlavním kontrolorem rýmů, rytmu, zpěvnosti a jazykové správnosti. Nesmí schválit text se slabými, falešnými nebo násilnými rýmy.

### Kontrola rýmů

Kritik musí v každém kole samostatně zkontrolovat kvalitu rýmů. Nehodnotí pouze to, zda se poslední slova podobají. Ověřuje také:

- zda jsou rýmy skutečné a zvukově přesvědčivé,
- zda nejsou násilné, gramaticky nepřirozené nebo vytvořené pouze kvůli koncovce,
- zda se neopakují stále stejná slova a stejné přípony,
- zda rým odpovídá významu verše,
- zda mají rýmující se řádky podobnou délku a rytmus,
- zda přízvuk při zpěvu nepadá na nesprávné místo,
- zda zvolená rýmová struktura zůstává v celé části skladby konzistentní.

Doporučené struktury jsou například:

- **AABB**
- **ABAB**
- **ABBA**
- složitější struktury, pokud zůstávají čitelné a zpěvné

Volný verš nesmí být vydáván za rýmovaný text.

Pokud je rým slabý, přibližný, opakovaný nebo vytvořený na úkor významu, Kritik musí označit konkrétní dvojici řádků a požadovat její přepracování.

Text nemůže být schválen pouze proto, že obsahuje správnou myšlenku. Musí zároveň fungovat rytmicky, zvukově a při zpěvu.

### Kontrola skloňování a časování

Kritik kontroluje také správné skloňování a časování slov. Nesmí schválit rým, který vznikl použitím:

- nesprávného pádu,
- nesprávného rodu,
- nesprávného čísla,
- nesprávné osoby,
- chybného slovesného času,
- umělé nebo nepřirozené koncovky.

Musí kontrolovat shodu mezi podmětem a přísudkem, správné vazby mezi slovy a přirozené znění věty v daném jazyce.

Rým nesmí být vytvořen za cenu gramatické chyby nebo nepřirozené formulace.

## Základní pravidla EasyTeam

- Moderátor zahajuje každé kolo shrnutím aktuálního textu a hudebního stylu.
- Každé další kolo musí přinést skutečné zlepšení.
- Kritik uvádí konkrétní chyby a konkrétní místa k opravě.
- Rýmy musí být skutečné, přirozené a zpěvné.
- Gramatika a správné tvary slov mají stejnou váhu jako samotný rým.
- Text a hudební styl se odevzdávají odděleně.
- COVERMASTER se aktivuje až po schválení Lyrics, Style Promptu a názvu písně.
- Finální výstup musí obsahovat čisté **Lyrics**, samostatný **Style Prompt**, sekci **COVERMASTER** a finální **S-cover**.
- Uživatel má konečné slovo a určuje směr skladby.

## Rychlý start

1. Otevři ChatGPT Project a do **Project Instructions** vlož obsah souboru `prompts/chatgpt-project-instructions.md`.
2. Napiš krátký brief, např.:

   ```text
   tema rytir metal cz 3
   ```

3. Poté napiš `0` pro AUTO režim.
4. Odpovídej `ano` / `ne` / čísly — EasyTeam udělá zbytek.
5. Po dokončení dostaneš `--- LYRICS ---`, `--- STYLE PROMPT ---`, `--- COVERMASTER ---` a `--- S-COVER ---`.

## Struktura projektu

| Cesta | Obsah |
|---|---|
| `prompts/chatgpt-project-instructions.md` | **Hlavní prompt** — vlož do ChatGPT Project Instructions |
| `prompts/roles/moderator.md` | Role Moderátora |
| `prompts/roles/poet.md` | Role Básníka |
| `prompts/roles/musician.md` | Role Hudebníka |
| `prompts/roles/prompt-specialist.md` | Role Prompt specialisty |
| `prompts/roles/critic.md` | Role Kritika |
| `prompts/roles/covermaster.md` | Role COVERMASTERa |
| `prompts/roles/user.md` | Role Uživatele |
| `workflows/short-commands.md` | Protokol krátkých příkazů (0-9, ano/ne) |
| `examples/*.md` | Ukázkové session |
| `qa/critic-rubric.md` | Kritéria hodnocení kvality |
| `qa/prompt-regression-checklist.md` | Regresní checklist pro změny v promptech |
| `docs/github-workflow.md` | Workflow s ChatGPT + GitHub |
| `docs/decision-log.md` | Rozhodovací deník |

## Krátké příkazy

| Příkaz | Význam |
|---|---|
| `0` | AUTO start / pokračování |
| `1` | Zobraz 3 možnosti |
| `2` | Vylepši text |
| `3` | Změň styl |
| `4` | Posílit refrén |
| `5` | Zkrátit |
| `6` | Více emocí |
| `7` | Více komerční |
| `8` | Zobraz stav |
| `9` | Finalizovat Lyrics, Style Prompt, COVERMASTER a S-cover |
| `ano`/`jo`/`tak`/`ok` | Souhlas |
| `ne` | Zastavit, nabídnout alternativy |
| `?` | Nápověda |

## Cenová politika

- **Žádná placená API ani modely** nad rámec stávajícího ChatGPT Pro.
- Pokud by něco vyžadovalo platbu, EasyTeam pouze **varuje** a nepřipojí to.
- Všechny nástroje jsou zdarma: ChatGPT Pro, GitHub, markdown.

## Odkazy

- [Hlavní prompt](prompts/chatgpt-project-instructions.md)
- [Seznam příkazů](workflows/short-commands.md)
- [Kritik rubric](qa/critic-rubric.md)
- [Regresní checklist](qa/prompt-regression-checklist.md)
- [Ukázkové session](examples/czech-folk-metal-low-typing.md)
- [GitHub workflow](docs/github-workflow.md)
- [Rozhodovací deník](docs/decision-log.md)
