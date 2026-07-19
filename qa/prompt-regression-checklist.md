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

**Očekávání:** EasyTeam spustí AUTO kolo 1, neptá se na `Moderátore, zahaj kolo 1`.

**PASS:** První odpověď obsahuje "Kolo 1" nebo "AUTO" a začíná prací na textu.  
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

**Očekávání:** V odpovědi se objeví role: Moderátor, Hudebník, Básník, Kritik. Každá role mluví za sebe.

**PASS:** V textu jsou jasně oddělené sekce pro jednotlivé role.  
**FAIL:** Vše píše jedna entita bez rozlišení rolí.

---

## Test 4 — Critic strictness

**Vstup:** Zadej text se záměrně slabým rýmem, např. "Láska je jak květina / Která krásně rozkvétá"

**Očekávání:** Kritik označí konkrétní dvojici řádků a navrhne opravu.

**PASS:** Kritik napíše `CHYBA:` s čísly řádků a `NÁVRH OPRAVY:`.  
**FAIL:** Kritik řekne "vypadá to dobře" nebo "zkus to vylepšit" bez konkrétních řádků.

---

## Test 5 — Lyrics / Style Prompt separation

**Vstup:** Nech EasyTeam dokončit píseň a požádej o finále (`9`).

**Očekávání:** Výstup obsahuje `--- LYRICS ---` a `--- STYLE PROMPT ---` jako samostatné sekce.

**PASS:** Obě sekce jsou přítomny a odděleny.  
**FAIL:** Chybí jedna ze sekcí nebo jsou smíchané.

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

## Test 12 — Ekvivalenty `ano`

**Vstup:** V odpověď na nabídku napiš `jo`.

**Očekávání:** EasyTeam to bere jako `ano` a pokračuje.

**PASS:** EasyTeam přijme `jo` jako souhlas a pokračuje.  
**FAIL:** EasyTeam nerozumí nebo se ptá, co `jo` znamená.