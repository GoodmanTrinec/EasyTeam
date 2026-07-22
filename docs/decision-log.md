# Decision Log — rozhodovací deník

Tento deník zaznamenává klíčová rozhodnutí o směřování EasyTeam projektu.

## Princip

- **GitHub je primární zdroj pravdy.** Všechna projektová rozhodnutí, verze promptů a dokumentace patří do committed markdown souborů.
- **Dočasné agentní scratch soubory nejsou zdroj pravdy** — session poznámky, plány a drafty patří mimo oficiální dokumentaci, dokud nejsou přepsané do committed markdown souborů.
- Projektová rozhodnutí, changelog a release notes patří do normálních committed docs.

---

## Rozhodnutí

### 2026-07-19 — EasyTeam jako ChatGPT Pro prompt-pack

**Rozhodnutí:** EasyTeam bude markdown prompt-pack pro ChatGPT Pro, ne aplikace.

**Důvody:**
- UŽIVATEL má ChatGPT Pro s GitHub integrací
- Prompt-pack je rychlejší cesta k užitečnému výsledku než UI
- Hlavní mezera je kvalita workflow, ne tlačítka

**Dopad:** Všechny soubory jsou markdown, žádný backend, žádná databáze.

---

### 2026-07-19 — Low-typing interakce

**Rozhodnutí (nahrazeno 2026-07-22):** UŽIVATEL píše jen `0`-`9`, `ano`/`ne`, nebo krátký brief. Žádné dlouhé věty.

**Důvody:** UŽIVATEL píše pomalu a chce minimum psaní.

**Historický dopad:** Prompty podporovaly číselné příkazy a `ano`/`ne`. Toto rozhraní později nahradily samostatné příkazy `GO` a `?`.

---

### 2026-07-19 — Žádná placená API

**Rozhodnutí:** Projekt nepoužívá žádná placená API ani modely nad rámec stávajícího ChatGPT Pro.

**Důvody:** UŽIVATEL výslovně odmítl placené služby.

**Dopad:** Všechny prompty obsahují guardrail. Pokud by něco vyžadovalo platbu, pouze varovat a nepřipojit.

---

### 2026-07-19 — Tolerance vstupního jazyka

**Rozhodnutí:** EasyTeam akceptuje mix PL/CZ/EN a nářečí `po naszymu`. Nikdy neopravuje UŽIVATEL.

**Důvody:** UŽIVATEL přirozeně míchá jazyky včetně lokálního nářečí.

**Dopad:** Všechny prompty musí tolerovat smíšený vstup a v případě potřeby se zeptat na výstupní jazyk jednou krátkou otázkou.

---

### 2026-07-20 — GitHub primární, scratch mimo dokumentaci

**Rozhodnutí:** GitHub committed markdown je zdroj pravdy. Dočasné agentní scratch soubory nejsou součást oficiální dokumentace.

**Důvody:** UŽIVATEL chce GitHub jako primární úložiště. Session deníky a pracovní plány jsou dočasné.

**Dopad:** Všechna důležitá rozhodnutí, changelog a dokumentace jdou do committed souborů.

---

### 2026-07-22 — Počet plných kol, TITLE a final gate

**Rozhodnutí (výchozí počet aktualizován níže):** AUTO používá počet kol z briefu. Každé plné kolo má přesně pořadí MODERÁTOR → HUDEBNÍK → BÁSNÍK → PROMPTER → KRITIK → MODERÁTOR. Stav obsahuje `current_title`, `current_lyrics` a `current_style`. Po všech kolech proběhne samostatný final gate KRITIK a COVERMASTER se aktivuje pouze po `PASS`.

**Důvody:** Style Prompt musí vznikat souběžně s Lyrics, TITLE musí odpovídat aktuálnímu příběhu a žádný krátký příkaz nesmí obejít kontrolu kvality.

**Dopad:**

- `tema rytir metal cz 3` nastaví 3 plná kola a `tema reggae pl 5` nastaví 5. Původní default 2 byl po live Testu 2+1 nahrazen třemi koly. Původně spuštění AUTO vyžadovalo příkaz `0`; aktuální příkaz je `GO`.
- AUTO se mezi koly neptá na pokračování.
- PROMPTER je povinný v každém kole.
- BÁSNÍK navrhne TITLE nejpozději v prvním kole a aktualizuje ho po změně příběhu.
- Finalní `FAIL` vrací práci odpovědné roli a KRITIK kontrolu opakuje až do `PASS`.
- COVERMASTER pouze připravuje specifikaci S-coveru po finalním `PASS`; rozměr zůstává `543 × 807 px`.

---

### 2026-07-22 — Dva oficiální deníky s rozdílnými úlohami

**Rozhodnutí:** `DZIENNIK.md` je commitnutou součástí dokumentace a zaznamenává chronologický průběh a stav realizace. `docs/decision-log.md` uchovává architektonická rozhodnutí a jejich odůvodnění.

**Důvody:** Historie provedené práce má být viditelná na GitHubu, ale stavy implementace se nemají míchat s projektovými rozhodnutími.

**Dopad:** Každá významná změna workflow dostane stavový zápis v `DZIENNIK.md`; rozhodnutí měnící pravidla EasyTeam se nadále zapisují zde.

---

### 2026-07-22 — Jednosouborové nasazení v1.1

**Rozhodnutí:** Jediný `prompts/chatgpt-project-instructions.md` musí zůstat pod limitem 8000 znaků a vkládá se přímo do pole ChatGPT Project Instructions. Samotný brief pouze inicializuje stav; původní start `0` byl později nahrazen příkazem `GO`.

**Důvody:** Živý test odhalil limit 8000 znaků v Project Instructions, automatický start bez `0` a příliš mírnou kontrolu standardní češtiny.

**Dopad:** Není potřeba loader ani duplicitní project source. Prompt je stručnější, protokol krátkých příkazů je jednoznačný a KRITIK rozlišuje tolerantní vstup UŽIVATELE od jazykově správného finálního výstupu.

---

### 2026-07-22 — Jednoznačný start `GO`

**Rozhodnutí:** Hlavní EasyTeam používá pouze samostatné příkazy `GO` a `?`. `GO` po načtení briefu spustí celé AUTO; `?` zobrazí stručnou nápovědu. Původní globální příkazy `0`–`9`, `ano` a `ne` jsou z hlavního projektu odstraněny.

**Důvody:** Číselné příkazy řídily interní role místo skutečného uživatelského workflow a nedávaly smysl před poslechem výsledku v Suno. `GO` je krátké, srozumitelné napříč jazyky a méně nejednoznačné než `R`.

**Dopad:** Brief vždy čeká na `GO`, AUTO proběhne bez uživatelských voleb až do finálního výstupu a session skončí. Tuning není součástí hlavního projektu; později vznikne jako samostatný projekt.

---

### 2026-07-22 — Tři výchozí kola a bezpečné rozpoznání počtu

**Rozhodnutí:** Brief bez výslovného počtu používá `total_rounds: 3`. Počet se načítá přednostně z označení `počet kol: N`, `N kol/kola`, `N rund/rundy` nebo `N rounds`; koncové samostatné číslo je platné jen v kompaktním briefu. Čísla patřící k tempu, roku, datu, značkám sekcí nebo dodaným Lyrics se ignorují.

**Důvody:** Live Test 2+1 přepracování staré písně ukázal, že po dvou kolech zůstal gramaticky vadný řádek a několik slabších formulací. Dodatečné třetí kolo bez nápovědy UŽIVATELE samo našlo chyby, opravilo je a prošlo finalním gate. Současně styl `94 BPM` odhalil riziko záměny tempa za počet kol.

**Dopad:** Tři kola jsou bezpečným minimem pro nový brief bez počtu. UŽIVATEL může nadále výslovně vyžádat 1, 2, 5 nebo jiný kladný počet kol, ale `94 BPM`, `[Verse 2]` ani čísla ve vloženém textu počet kol nemění.

---

### 2026-07-22 — Tvrdé Suno brány pro Lyrics a artist/producer tagy

**Rozhodnutí:** BÁSNÍK cílí na nejvýše 4500 znaků a absolutní limit Lyrics je 5000 znaků včetně mezer, odřádkování a značek sekcí. KRITIK počet ověřuje před každým `PASS` a ve final gate. TITLE, Lyrics, Style Prompt a Negative Prompt nesmí obsahovat jména, aliasy ani rozpoznatelné tagy skutečných umělců, skupin či producentů; odmítají se také dvojznačné fráze, které Suno takto vyhodnocuje.

**Důvody:** Live Test 3 vytvořil strukturálně správný anglický old-school hip-hop příběh, ale praktické vložení do Suno nejprve selhalo kvůli překročení 5000 znaků a podruhé kvůli frázi `fifty grand`, kterou Suno označilo jako producer tag. Původní final gate obě vady chybně schválil.

**Dopad:** Překročení limitu vždy vrací práci BÁSNÍKOVI. Odkazy na konkrétní umělce se převádějí na hudební vlastnosti a rizikové výrazy se nahrazují bezpečným významovým ekvivalentem, např. `fifty grand` → `the payoff`. COVERMASTER zůstává zablokován až do opakovaného finalního `PASS`.
