# Prompt Regression Checklist

Tento checklist slouží k ověření, že změny v promptech nenarušily chování EasyTeam.
Lze spustit ručně nebo agentem. Všechny testy jsou zdarma — nevyžadují žádné placené API.

---

## Pokyny

- Každý test má: ID, název, vstup, očekávané chování, PASS/FAIL kritérium.
- Proveď všechny testy v pořadí. Pokud některý FAIL, oprav chybu před dalším testem.
- Výsledek zapiš do `qa/regression-test-results.md`.

---

## Test 1 — Low-typing compliance (0 s kontextem)

**Vstup:** `tema láska pop cz 2` → `0`

**Očekávání:** EasyTeam nastaví `total_rounds: 2`, spustí AUTO kolo 1 a bez otázky mezi koly provede dvě plná kola. Neptá se na `MODERÁTOR, zahaj kolo 1`.

**PASS:** První odpověď obsahuje `Kolo 1/2` nebo `AUTO`, začíná prací na textu a workflow přejde samo do `Kolo 2/2`.
**FAIL:** První odpověď je otázka "Jaké téma?" nebo požadavek na delší zadání.

---

## Test 2 — Low-typing compliance (0 bez kontextu)

**Vstup:** `0` (v prázdném chatu)

**Očekávání:** EasyTeam položí **jednu krátkou číselnou otázku** (např. "Vyber téma: 1) láska 2) boj 3) smutek?").

**PASS:** Odpověď obsahuje `1)` `2)` `3)` a jen jednu otázku.
**FAIL:** Odpověď obsahuje formulář s více otázkami nebo požadavek na dlouhý text.

---

## Test 3 — Role separation

**Vstup:** `tema láska pop cz 1` → `0`

**Očekávání:** Jedno plné kolo obsahuje přesně pořadí: MODERÁTOR (otevření `1/1`), HUDEBNÍK, BÁSNÍK, PROMPTER, KRITIK, MODERÁTOR (uložení stavu). Každá role mluví za sebe.

**PASS:** V textu je všech šest etap ve správném pořadí a PROMPTER aktualizuje Style Prompt.
**FAIL:** Chybí role, pořadí je jiné, PROMPTER přichází až po kole nebo chybí závěrečný MODERÁTOR.

---

## Test 4 — Critic strictness

**Vstup:** Zadej text se záměrně slabým rýmem, např. "Láska je jak květina / Která krásně rozkvétá"

**Očekávání:** KRITIK označí konkrétní dvojici řádků a navrhne opravu.

**PASS:** KRITIK napíše `CHYBA:` s čísly řádků a `NÁVRH OPRAVY:`.
**FAIL:** KRITIK řekne "vypadá to dobře" nebo "zkus to vylepšit" bez konkrétních řádků.

---

## Test 5 — Full final workflow separation

**Vstup:** Nech EasyTeam dokončit píseň a požádej o finále (`9`).

**Očekávání:** Po dokončení všech kol i finalním `PASS` výstup obsahuje `--- TITLE ---`, `--- LYRICS ---`, `--- STYLE PROMPT ---`, `--- COVERMASTER ---` a `--- S-COVER ---` jako samostatné sekce.

**PASS:** Všechny sekce jsou přítomny, odděleny a ve správném pořadí `TITLE → LYRICS → STYLE PROMPT → COVERMASTER → S-COVER`; COVERMASTER následuje až po finalním `PASS`.
**FAIL:** Chybí TITLE, COVERMASTER nebo S-cover, pořadí je chybné nebo byl vynechán final gate.

---

## Test 6 — Style Prompt v angličtině

**Vstup:** Po finále zkontroluj `--- STYLE PROMPT ---`.

**Očekávání:** Style Prompt je psán anglicky.

**PASS:** Text v sekci Style Prompt je anglicky.
**FAIL:** Style Prompt obsahuje češtinu, polštinu nebo jiný jazyk.

---

## Test 7 — Žádné placené API / modely (NEGATIVNÍ TEST)

**Vstup:** Zeptej se: "Můžeš použít GPT-4 API pro lepší text?"

**Očekávání:** EasyTeam odmítne a napíše `UPOZORNĚNÍ:` nebo vysvětlí, že nepoužívá placená API.

**PASS:** Odpověď obsahuje varování a nepřipojuje žádné placené API.
**FAIL:** EasyTeam souhlasí nebo navrhuje přechod na placenou variantu.

---

## Test 8 — Žádné klonování umělců (NEGATIVNÍ TEST)

**Vstup:** "Udělej píseň ve stylu Metallicy"

**Očekávání:** EasyTeam převede požadavek na hudební atributy (např. "heavy metal, fast tempo, aggressive vocals") a neřekne "styl Metallicy".

**PASS:** Odpověď používá atributy, ne jméno kapely jako styl.
**FAIL:** Odpověď říká "styl Metallicy" nebo "jako Metallica".

---

## Test 9 — Jedna otázka najednou

**Vstup:** `0` bez kontextu, pak na první otázku odpověz číslem.

**Očekávání:** Po každé odpovědi následuje právě jedna další otázka, nikdy dvě nebo více.

**PASS:** Každá zpráva od EasyTeam obsahuje nejvýše jednu otázku.
**FAIL:** Některá zpráva obsahuje dvě nebo více otázek najednou.

---

## Test 10 — Smíšený vstup PL/CZ/EN/po naszymu

**Vstup:** "temát love rock po naszymu 2"

**Očekávání:** EasyTeam rozumí, neopravuje jazyk, zeptá se jen na výstupní jazyk, pokud není jasný.

**PASS:** EasyTeam přijme vstup bez korekce jazyka. Pokud si není jistý výstupním jazykem, zeptá se jednou krátkou číselnou otázkou (např. "Jazyk výstupu: 1) česky 2) polsky 3) po naszymu?").
**FAIL:** EasyTeam řekne "Prosím pište spisovně" nebo "Nerozumím, zadejte znovu".

---

## Test 11 — Numeric precedence

**Vstup:** V průběhu práce, když EasyTeam nabídne číslované možnosti (např. "1) ano 2) ne 3) změnit"), napiš `3`.

**Očekávání:** `3` vybere třetí možnost, NE globální příkaz (změna stylu).

**PASS:** EasyTeam interpretuje `3` jako výběr z nabízených možností.
**FAIL:** EasyTeam interpretuje `3` jako globální příkaz "změň hudební směr".

---

## Test 12 — České `ano`

**Vstup:** V odpověď na nabídku napiš `ano`.

**Očekávání:** EasyTeam to bere jako `ano` a pokračuje.

**PASS:** EasyTeam přijme `ano` jako souhlas a pokračuje.
**FAIL:** EasyTeam nerozumí nebo vyžaduje nečeský ekvivalent souhlasu.

---

## Test 13 — COVERMASTER activation timing

**Vstup:** `tema rytir metal cz 2` → `0`; během kola požádej o cover před schválením finálních Lyrics, Style Promptu a názvu.

**Očekávání:** EasyTeam nespustí COVERMASTER během skladatelských kol ani po posledním kole před finalním `PASS`. Vysvětlí krátce, že nejprve musí dokončit TITLE, Lyrics, Style Prompt a final gate.

**PASS:** COVERMASTER se neúčastní šestietapových kol a aktivuje se až po finalním `PASS`.
**FAIL:** COVERMASTER navrhuje cover během tvorby textu nebo mění Lyrics/Style Prompt.

---

## Test 14 — S-cover dimensions and ratios

**Vstup:** Po finále (`9`) zkontroluj `--- S-COVER ---`.

**Očekávání:** S-cover uvádí přesnou velikost `543 × 807 px`, poměr `543:807` a zjednodušený poměr `181:269`.

**PASS:** Všechny tři hodnoty jsou uvedeny a staré poměry `443:591` a obecný `3:4` jsou odmítnuty jako neplatné.
**FAIL:** Výstup používá `443:591`, obecný `3:4`, nebo chybí přesná velikost.

---

## Test 15 — S-cover custom text replacement

**Vstup:** Před finále zadej vlastní text pro cover: `Cover text: ONLY THIS LINE`.

**Očekávání:** S-cover použije přesně `ONLY THIS LINE` jako celý text na coveru.

**PASS:** S-cover nepřidá název, interpreta, autora ani žádný další text.
**FAIL:** EasyTeam přidá title/artist/author k vlastnímu textu nebo text upraví.

---

## Test 16 — S-cover story consistency

**Vstup:** Vytvoř píseň se smutným nebo tragickým koncem a požádej o finále (`9`).

**Očekávání:** COVERMASTER zachová skutečný konec příběhu a nevytvoří falešně pozitivní vizuální interpretaci.

**PASS:** Cover prompt odpovídá emocím, symbolům a závěru lyrics.
**FAIL:** Cover prompt změní význam příběhu, přidá šťastný konec nebo ignoruje klíčový symbol.

---

## Test 17 — Reference image is size-only

**Vstup:** Dodej obrázek pouze jako referenci velikosti nebo poměru stran a požádej o S-cover.

**Očekávání:** COVERMASTER použije pouze velikost/poměr, ne vizuální obsah obrázku.

**PASS:** Výstup výslovně nekopíruje kompozici, objekty, styl ani obsah size-only reference.
**FAIL:** COVERMASTER popíše nebo napodobí referenční obrázek jako vizuální zadání.

---

## Test 18 — Brief s 1 kolem

**Vstup:** `tema rytir metal cz 1` → `0`

**Očekávání:** EasyTeam nastaví `total_rounds: 1`, provede právě jedno plné šestietapové kolo a poté finální kontrolu MODERÁTOR a final gate KRITIK.

**PASS:** Objeví se `Kolo 1/1`; neobjeví se `Kolo 2`; PROMPTER je uvnitř kola a COVERMASTER až po finalním `PASS`.
**FAIL:** AUTO vždy spustí 2 kola, vynechá některou etapu nebo přeskočí final gate.

---

## Test 19 — Brief se 3 koly

**Vstup:** `tema rytir metal cz 3` → `0`

**Očekávání:** EasyTeam automaticky provede tři plná kola bez otázky mezi nimi.

**PASS:** Objeví se přesně `Kolo 1/3`, `Kolo 2/3`, `Kolo 3/3`, v každém šest etap ve správném pořadí.
**FAIL:** Počet kol je 2, AUTO se mezi koly zastaví nebo některé kolo není plné.

---

## Test 20 — Brief s 5 koly

**Vstup:** `tema reggae pl 5` → `0`

**Očekávání:** EasyTeam automaticky provede pět plných kol bez otázky mezi nimi.

**PASS:** Objeví se přesně kola `1/5` až `5/5`, každé včetně PROMPTER a závěrečného MODERÁTOR.
**FAIL:** AUTO skončí dříve, vždy použije 2 kola nebo se ptá, zda pokračovat.

---

## Test 21 — Brief bez počtu kol

**Vstup:** `tema more pop cz` → `0`

**Očekávání:** EasyTeam použije bezpečný default `total_rounds: 2` bez další otázky o počtu kol.

**PASS:** Objeví se `Kolo 1/2` a `Kolo 2/2`, bez třetího kola a bez otázky mezi nimi.
**FAIL:** EasyTeam požaduje počet kol, použije jiný default nebo provede jiný počet kol.

---

## Test 22 — KRITIK vrací FAIL uvnitř kola

**Vstup:** V kole 1/3 vytvoř Lyrics se slabým rýmem a technickou poznámkou `[přidat těžké bicí]`.

**Očekávání:** PROMPTER přesune technickou instrukci do Style Promptu. KRITIK vrátí konkrétní `FAIL`; závěrečný MODERÁTOR sloučí kompatibilní opravy, uloží stav a přenese nevyřešené chyby jako prioritu kola 2.

**PASS:** `FAIL` obsahuje odpovědnou roli, přesné řádky/pole a návrh opravy; kolo končí etapou MODERÁTOR a AUTO pokračuje do kola 2.
**FAIL:** Workflow přeruší kolo před etapou 6, ignoruje chybu, žádá UŽIVATEL o pokračování nebo spouští COVERMASTER.

---

## Test 23 — Final KRITIK vrací FAIL

**Vstup:** Po posledním kole ponech TITLE neodpovídající změněnému tragickému konci nebo Style Prompt bez vokálu.

**Očekávání:** Samostatný final gate vrátí `FAIL`, určí odpovědnou roli, ta opraví celý artefakt a KRITIK kontrolu opakuje až do `PASS`.

**PASS:** COVERMASTER se neaktivuje při `FAIL`; po opravě proběhne opakovaný final gate a teprve `PASS` odblokuje COVERMASTER.
**FAIL:** `FAIL` je ignorován, počet oprav je omezen nebo se COVERMASTER aktivuje dříve.

---

## Test 24 — PROMPTER v každém kole

**Vstup:** `tema reggae pl 3` → `0`

**Očekávání:** PROMPTER vystoupí právě jednou v každém ze tří plných kol po BÁSNÍK a před KRITIK a aktualizuje celý anglický Style Prompt.

**PASS:** Každé kolo obsahuje samostatnou aktualizaci Style Promptu s vokálem, nástroji, tempem a atmosférou; technické instrukce nezůstávají v Lyrics.
**FAIL:** PROMPTER je vynechán v kterémkoli kole nebo vytváří Style Prompt až po posledním kole.

---

## Test 25 — COVERMASTER až po finalním PASS

**Vstup:** Požádej o cover během kola, po posledním kole před final gate a po finalním `FAIL`.

**Očekávání:** Ve všech třech případech EasyTeam COVERMASTER nespustí. Aktivace nastane až po finalním `PASS`.

**PASS:** Stav zůstává mimo `cover_creation`, dokud `final_gate` není `pass`.
**FAIL:** Pouhé dokončení počtu kol, příkaz `9`, `0` nebo `ano` obejde final gate.

---

## Test 26 — TITLE se mění s příběhem

**Vstup:** V kole 1 vznikne vítězný příběh a TITLE `Návrat krále`; v kole 2 se konec změní na tragickou ztrátu.

**Očekávání:** BÁSNÍK aktualizuje TITLE v kole 2 a KRITIK odmítne starý titul, pokud již neodpovídá příběhu.

**PASS:** `current_title` je navržen nejpozději v kole 1 a po změně příběhu je aktualizován před final gate.
**FAIL:** TITLE chybí, vznikne až po kolech nebo zůstane v rozporu s novým koncem.

---

## Test 27 — Příkazy `0`, `8`, `9`, `ano`, `ne`

**Vstup:** Během session postupně použij `0`, `8`, `ne`, vyber alternativu, použij `ano` a před dokončením kol použij `9`.

**Očekávání:** `0` spustí/obnoví AUTO; `8` pouze zobrazí stav; `ne` pozastaví a nabídne 3 alternativy; `ano` přijme doporučení bez obcházení chyb; `9` dokončí zbývající kola a final gate před COVERMASTER.

**PASS:** Každý příkaz zachová stavovou logiku, žádný nepřeskočí plné kolo ani final `PASS`.
**FAIL:** `8` mění stav, `ne` je ignorováno, `ano` schválí `FAIL`, nebo `9` spustí COVERMASTER před finalním `PASS`.
