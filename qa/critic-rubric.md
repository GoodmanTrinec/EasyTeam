# KRITIK Rubric — hodnoticí kritéria kvality písně

Tento rubric definuje, jak KRITIK v každém kole a v samostatném final gate hodnotí TITLE, Lyrics, Style Prompt, požadavky briefu a připravenost vstupů pro COVERMASTER.
Každá kategorie obsahuje **PASS** a **FAIL** příklady. Při chybě KRITIK musí vždy uvést odpovědnou roli, konkrétní řádky nebo pole a způsob opravy.

Výsledek kontroly je jednoznačný:

- `PASS`
- `FAIL | ODPOVĚDNÁ ROLE: <role> | CHYBA: <řádky/pole a co> | NÁVRH OPRAVY: <jak>`

---

## 1. Kvalita rýmů (Rhyme quality)

**PASS:** Rýmy jsou skutečné, zvukově přesvědčivé, přirozené.
- `"Měsíc svítí nad lesy / Cestu nocí nevidíš"` — čistý rým `í` kmenový, nejen koncovka
- `"Plamen hoří v kamnech / Ozvěna zní v dálkách"` — rým `ech` × `ách`, funkční a znělý

**FAIL:** Rýmy jsou násilné, pouze koncovkové, nebo nesedí významem.
- `"Láska je jak květina / Která krásně rozkvétá"` — pouze koncovka `á`, slova se nerýmují zvukově
- `"Rytíř bojoval s drakem / Celým svým životem takým"` — `drakem` × `takým` je násilné, vynucené

**KRITIK musí:** Označit konkrétní dvojici řádků, např.:
> CHYBA: řádky 3-4 "drakem / takým" — násilný rým, pouze koncovka -em/-ým bez zvukové shody
> NÁVRH OPRAVY: "Rytíř bojoval s drakem / Posledním statečným krokem"

---

## 2. Rytmus a zpěvnost (Rhythm & singability)

**PASS:** Řádky v rýmujícím se páru mají podobnou délku a přízvučné slabiky padají přirozeně.
- `"Vítr válí suché listí / Cesta před námi se čistí"` — 8 + 8 slabik, stejný rytmus

**FAIL:** Řádky mají výrazně odlišnou délku nebo přízvuk padá na špatné místo.
- `"Měsíc svítí" (3 slabiky) / "Do temné noci, která všechno skrývá" (9 slabik)` — nelze zazpívat

**KRITIK musí:** Uvést počet slabik a označit nesoulad.

---

## 3. Gramatika a morfologie (Grammar & morphology)

**PASS:** Všechny tvary jsou gramaticky správné, přirozené.
- `" tys mi slíbila "` — správné časování, shoda
- `"Nové hry nabízejí svůj lesk"` — standardní česká shoda přídavného jména s podstatným jménem

**FAIL:** Rým vynutil nesprávný pád, rod, čas nebo nepřirozený tvar.
- `"Šel jsem do lesa / Kde rostla krása"` — `lesa` je 2. pád, ale `krása` je 1. pád; rým tlačí nesprávnou vazbu
- `"Chtěl jsem ti dát květinách"` — chybný pád kvůli rýmu
- `"Nový hry mu cpou svůj lesk"` — neodůvodněná obecná čeština v textu požadovaném jako standardní český výstup; oprava `"Nové hry mu nabízejí svůj lesk"`

**KRITIK musí:** Rozlišovat jazyk vstupu a výstupu. Smíšený nebo nářeční vstup UŽIVATELE neopravuje. Ve finálním TITLE a Lyrics však vyžaduje standardní češtinu, pokud brief výslovně nepožaduje nářečí, slang nebo hovorovou stylizaci postavy.

---

## 4. Emoční specifičnost (Emotional specificity)

**PASS:** Text vyvolává konkrétní emoci, používá obrazy a detaily.
- `"Déšť bubnuje do oken / Sám sedím, vypnul jsem telefon"` — konkrétní obraz, nálada

**FAIL:** Obecné fráze, klišé, nic neříkající výplně.
- `"Láska je krásná / Jako pohádka"` — klišé, nic konkrétního
- `"Cítím se tak skvěle / Nejkrásněji v celém světě"` — abstraktní, bez obrazu

---

## 5. Síla refrénu (Chorus strength)

**PASS:** Refrén je chytlavý, opakovatelný, emocionálně nabitý.
- `"Zvedni hlavu, nepadej / Sám svým pánem zůstávej"` — krátký, rytmický, snadno zapamatovatelný

**FAIL:** Refrén je stejně dlouhý jako sloky, bez výrazného háčku.
- `"Slunce svítí na oblohu / Já jdu svojí cestou dál"` — nijak nevyčnívá, snadno zapomenutelný

---

## 6. Vhodnost pro Suno (Suno suitability)

**PASS:** Text je čistý, bez metainstrukcí, má nejvýše 5000 znaků včetně mezer, odřádkování a značek sekcí a neobsahuje jména ani tagy skutečných umělců či producentů.
- Čistý text, sekce označené `[Verse 1]`, `[Chorus]`

**FAIL:** Text obsahuje instrukce pro AI, není rozdělený na sekce, překračuje 5000 znaků nebo obsahuje zakázané či dvojznačné artist/producer označení.
- `"[zpívat smutně]"` nebo `"tady přidat kytarové sólo"` v textu
- `fifty grand` může Suno chybně vyhodnotit jako producer tag; bezpečná oprava je např. `the payoff`

**KRITIK musí:** Před každým `PASS` uvnitř kola i ve final gate spočítat celý blok Lyrics. BÁSNÍK cílí na nejvýše 4500 znaků jako rezervu; 5000 je nepřekročitelný limit. Současně zkontrolovat TITLE, Lyrics, Style Prompt a Negative Prompt na skutečná jména, aliasy a rozpoznatelné tagy a převést hudební reference na vlastnosti.

---

## 7. Kvalita Style Promptu (Style prompt quality)

**PASS:** Anglický, max 3 věty, obsahuje žánr, nástroje, tempo, vokál, atmosféru.
- `"Epic folk metal, heavy guitars and violins, deep male vocals, 140 BPM, dark forest atmosphere."`

**FAIL:** Delší než 3 věty, obsahuje češtinu, nebo je příliš obecný.
- `"Je to taková pomalá smutná písnička s kytarou a zpěvem"` — česky, moc obecné, bez tempa
- `"A cinematic orchestral piece with a choir, then it breaks down into a dubstep drop..."` — příliš dlouhé a popisné

---

## 8. Originalita a vyhýbání se klišé (Originality)

**PASS:** Neotřelé obrazy, překvapivé obraty.
- `"Tvé jméno je tiché písmeno / Které nikdo nevysloví"`

**FAIL:** Opotřebované fráze.
- `"Láska jako trám / Nehne se ani o krok"` — okoukané

---

## 9. TITLE a COVERMASTER readiness

**PASS:** `current_title` je přítomný a odpovídá aktuálnímu příběhu. Finální stav obsahuje čitelný příběh, hudební styl, emoce, symboly a skutečný konec, takže COVERMASTER může po finalním `PASS` vytvořit věrnou specifikaci S-coveru.
- `Název: Poslední hlídka`, lyrics končí tichým smířením a S-cover používá tmavou noční stráž, ne oslavný vítězný motiv.

**FAIL:** TITLE chybí, zůstal po změně příběhu neaktuální nebo finální stav nedává roli COVERMASTER dost informací.
- Příběh se změnil z vítězství na ztrátu, ale TITLE stále slibuje triumf.
- Skutečný konec nebo klíčové symboly nejsou z TITLE a Lyrics jednoznačně určitelné.

**KRITIK musí před aktivací COVERMASTER:** Ověřit TITLE, jednoznačnost příběhu, stylu, emocí, symbolů a skutečného konce. Nehodnotí ještě neexistující S-cover.

**COVERMASTER musí po finalním `PASS`:** Zachovat příběh a skutečný konec, nepřidat slunečný triumf ke ztrátě, použít přesnou velikost `543 × 807 px`, poměr `543:807`, zjednodušený poměr `181:269` a správná pravidla textu. Poměry `443:591` a obecný `3:4` jsou neplatné.

---

## Obecné pravidlo

**Text nemůže projít jen proto, že obsahuje správnou myšlenku. Musí zároveň fungovat rytmicky, zvukově a při zpěvu.**

## Použití v kole a ve final gate

- Každé plné kolo obsahuje kontrolu KRITIK po aktualizaci Lyrics i Style Promptu.
- `FAIL` uvnitř kola se předá závěrečnému MODERÁTOR, který uloží kompatibilní opravy a nevyřešené chyby pro další kolo.
- Po všech kolech MODERÁTOR zkontroluje TITLE, Lyrics, Style Prompt a brief a spustí samostatný final gate KRITIK.
- Při finalním `FAIL` odpovědná role opraví celý dotčený artefakt a KRITIK kontrolu opakuje bez pevného limitu.
- COVERMASTER nesmí být aktivován, dokud final gate nevrátí `PASS`.
