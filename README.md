# EasyTeam

EasyTeam je markdown prompt-pack pro ChatGPT Project. Slouží k tvorbě písní pro Suno pomocí více specializovaných rolí a low-typing workflow.

## Stručná historie projektu

EasyTeam vznikl jako praktický způsob tvorby písní pro Suno. Původně šlo o jednoduchý postup: UŽIVATEL zadal téma, hudební styl a jazyk a AI vytvořila text písně.

Brzy se však ukázalo, že jedna odpověď často nestačí. Text mohl mít slabé rýmy, nevyrovnaný rytmus, příliš obecné obraty nebo hudební styl, který přesně neodpovídal zamýšlené atmosféře.

Proto se práce rozdělila mezi několik specializovaných rolí:

- **HUDEBNÍK** navrhuje žánr, tempo, nástroje, náladu, strukturu skladby a způsob vedení vokálu.
- **BÁSNÍK** píše text a soustředí se na rýmy, rytmus, emoce a zpěvnost.
- **PROMPTER** připravuje hudební zadání pro Suno.
- **KRITIK** hledá slabá místa, kontroluje rýmy, rytmus, zpěvnost a gramatickou správnost.
- **MODERÁTOR** řídí jednotlivá kola a hlídá, aby každá nová verze byla skutečně lepší.
- **COVERMASTER** připravuje specifikaci finálního S-coveru až po schválení Lyrics, Style Promptu a názvu písně ve finalním gate.
- **UŽIVATEL** určuje téma, počet kol, jazyk, styl, název a konečný směr skladby.

Tak vznikl systém tvůrčích kol. Každé plné kolo má přesně šest etap: MODERÁTOR otevře kolo a shrne TITLE, LYRICS a STYLE; HUDEBNÍK předá hudební doporučení; BÁSNÍK aktualizuje celý text i pracovní název; PROMPTER aktualizuje anglický Style Prompt; KRITIK vrátí `PASS` nebo konkrétní `FAIL`; MODERÁTOR sloučí změny a uloží nový stav. COVERMASTER se těchto kol neúčastní a aktivuje se až po samostatném final gate KRITIK ukončeném výsledkem `PASS`.

Finální workflow je:

**TITLE → LYRICS → STYLE PROMPT → final KRITIK PASS → COVERMASTER → S-COVER**

## AUTO a počet kol

- Počet kol pochází z posledního samostatného kladného celého čísla v briefu: `tema rytir metal cz 3` spustí 3 plná kola, `tema reggae pl 5` spustí 5.
- Když brief počet kol neobsahuje, EasyTeam použije bezpečný default 2 kola.
- AUTO provede všechna kola bez otázek mezi nimi.
- Jedno plné kolo vždy obsahuje MODERÁTOR → HUDEBNÍK → BÁSNÍK → PROMPTER → KRITIK → MODERÁTOR.
- PROMPTER se účastní každého kola; Style Prompt se vyvíjí souběžně s Lyrics.
- TITLE je navržen nejpozději v prvním kole a mění se, pokud se změní příběh.
- Po posledním kole následuje samostatný final gate KRITIK. Při `FAIL` odpovědná role opravuje a KRITIK kontroluje znovu až do `PASS`.
- COVERMASTER je zakázán před finalním `PASS`.

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
- Interpret se uvádí pouze tehdy, pokud ho UŽIVATEL zadal.
- Autor se uvádí pouze tehdy, pokud ho UŽIVATEL zadal.
- Pokud UŽIVATEL dodá vlastní text pro cover, tento text nahradí celou výchozí sadu textů.
- Při vlastním textu použij přesně dodaný text a nepřidávej nic dalšího.

## Role KRITIK

KRITIK je hlavním kontrolorem rýmů, rytmu, zpěvnosti a jazykové správnosti. Nesmí schválit text se slabými, falešnými nebo násilnými rýmy.

### Kontrola rýmů

KRITIK musí v každém kole samostatně zkontrolovat kvalitu rýmů. Nehodnotí pouze to, zda se poslední slova podobají. Ověřuje také:

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

Pokud je rým slabý, přibližný, opakovaný nebo vytvořený na úkor významu, KRITIK musí označit konkrétní dvojici řádků a požadovat její přepracování.

Text nemůže být schválen pouze proto, že obsahuje správnou myšlenku. Musí zároveň fungovat rytmicky, zvukově a při zpěvu.

### Kontrola skloňování a časování

KRITIK kontroluje také správné skloňování a časování slov. Nesmí schválit rým, který vznikl použitím:

- nesprávného pádu,
- nesprávného rodu,
- nesprávného čísla,
- nesprávné osoby,
- chybného slovesného času,
- umělé nebo nepřirozené koncovky.

Musí kontrolovat shodu mezi podmětem a přísudkem, správné vazby mezi slovy a přirozené znění věty v daném jazyce.

Rým nesmí být vytvořen za cenu gramatické chyby nebo nepřirozené formulace.

## Základní pravidla EasyTeam

- Stav obsahuje `current_title`, `current_lyrics`, `current_style`, `current_round` a `total_rounds`.
- MODERÁTOR zahajuje každé kolo číslem `X/N`, shrnutím aktuálního TITLE, LYRICS a STYLE a konkrétním cílem kola.
- Každé další kolo musí přinést skutečné zlepšení.
- HUDEBNÍK v každém kole analyzuje žánr, tempo, atmosféru, nástroje, strukturu a vokál.
- BÁSNÍK v každém kole odevzdává celý aktualizovaný text.
- PROMPTER v každém kole aktualizuje anglický Style Prompt a přesouvá do něj technické instrukce z Lyrics.
- KRITIK uvádí konkrétní chyby a konkrétní místa k opravě.
- MODERÁTOR uzavírá každé kolo uložením nového stavu a přenesením nevyřešených chyb do dalšího kola.
- Rýmy musí být skutečné, přirozené a zpěvné.
- Gramatika a správné tvary slov mají stejnou váhu jako samotný rým.
- Text a hudební styl se odevzdávají odděleně.
- COVERMASTER se aktivuje až po dokončení všech kol a finalním `PASS` pro TITLE, Lyrics, Style Prompt a požadavky briefu.
- Finální výstup musí obsahovat **TITLE**, čisté **Lyrics**, samostatný **Style Prompt**, sekci **COVERMASTER** a finální **S-cover**.
- UŽIVATEL má konečné slovo a určuje směr skladby.

## Rychlý start

1. Otevři ChatGPT Project a do **Project Instructions** vlož obsah souboru `prompts/chatgpt-project-instructions.md`.
2. Napiš krátký brief, např.:

   ```text
   tema rytir metal cz 3
   ```

3. Poté napiš `0` pro AUTO režim.
4. AUTO provede všechna 3 plná kola bez dotazů mezi koly.
5. Po finalním `PASS` dostaneš `--- TITLE ---`, `--- LYRICS ---`, `--- STYLE PROMPT ---`, `--- COVERMASTER ---` a `--- S-COVER ---`.

## Struktura projektu

| Cesta | Obsah |
|---|---|
| `prompts/chatgpt-project-instructions.md` | **Hlavní prompt** — vlož do ChatGPT Project Instructions |
| `prompts/roles/moderator.md` | Role MODERÁTOR |
| `prompts/roles/poet.md` | Role BÁSNÍK |
| `prompts/roles/musician.md` | Role HUDEBNÍK |
| `prompts/roles/prompter.md` | Role PROMPTER |
| `prompts/roles/critic.md` | Role KRITIK |
| `prompts/roles/covermaster.md` | Role COVERMASTER |
| `prompts/roles/user.md` | Role UŽIVATEL |
| `workflows/short-commands.md` | Protokol krátkých příkazů (0-9, ano/ne) |
| `examples/*.md` | Ukázkové session |
| `qa/critic-rubric.md` | Kritéria hodnocení kvality |
| `qa/prompt-regression-checklist.md` | Regresní checklist pro změny v promptech |
| `qa/regression-test-results.md` | Poslední výsledky logických regresních testů |
| `docs/github-workflow.md` | Workflow s ChatGPT + GitHub |
| `docs/decision-log.md` | Rozhodovací deník |
| `DZIENNIK.md` | Oficiální chronologický deník průběhu a stavu projektu |

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
| `8` | Zobraz stav včetně TITLE, Lyrics, Style, čísla kola a chyb; nic neměň |
| `9` | Dokonči zbývající kola a final gate; COVERMASTER spusť jen po `PASS` |
| `ano` | Souhlas |
| `ne` | Zastavit, nabídnout alternativy |
| `?` | Nápověda |

## Cenová politika

- **Žádná placená API ani modely** nad rámec stávajícího ChatGPT Pro.
- Pokud by něco vyžadovalo platbu, EasyTeam pouze **varuje** a nepřipojí to.
- Všechny nástroje jsou zdarma: ChatGPT Pro, GitHub, markdown.

## Odkazy

- [Hlavní prompt](prompts/chatgpt-project-instructions.md)
- [Seznam příkazů](workflows/short-commands.md)
- [KRITIK rubric](qa/critic-rubric.md)
- [Regresní checklist](qa/prompt-regression-checklist.md)
- [Výsledky regresních testů](qa/regression-test-results.md)
- [Ukázkové session](examples/czech-folk-metal-low-typing.md)
- [GitHub workflow](docs/github-workflow.md)
- [Rozhodovací deník](docs/decision-log.md)
- [Dziennik projektu](DZIENNIK.md)
