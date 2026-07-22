# Dziennik projektów

## 2026-07-20 — EasyTeam: plan finalnego workflow

### Status

Plan projektu. Zrealizowany 2026-07-22 — szczegóły w następnym wpisie.

### Cel

Zbudować wieloagentowy system tworzenia kompletnych utworów dla Suno. Wynik końcowy ma zawierać:

1. TITLE,
2. LYRICS,
3. STYLE PROMPT,
4. analizę COVERMASTER,
5. finalną specyfikację S-COVER.

### Role

- MODERATOR — prowadzi stan, rundy, konflikty wymagań i finalizację.
- MUZYK — odpowiada za konstrukcję muzyczną, tempo, instrumentację, dynamikę i wokal.
- POETA — tworzy i poprawia Lyrics, fabułę, rytm, gramatykę oraz prawdziwe rymy.
- PROMPTCISTA — w każdej rundzie tworzy zwięzły angielski Style Prompt dla Suno.
- KRYTYK — kontroluje tytuł, Lyrics, Style Prompt i wszystkie wymagania użytkownika.
- COVERMASTER — po FINAL PASS projektuje specyfikację okładki.
- UŻYTKOWNIK — dostarcza brief i steruje procesem w trybie MANUAL.

### Dane wejściowe

System przyjmuje: temat, liczbę rund, tryb AUTO/MANUAL, styl, język, dodatkowe wymagania oraz opcjonalnie tytuł, artystę, autora i własny tekst okładki. Brakujące dane mają otrzymywać bezpieczne wartości domyślne bez wymagania długiego formularza.

### Stan roboczy Moderatora

Przez cały proces należy utrzymywać:

- brief,
- mandatory_requirements,
- contradictions,
- current_title,
- current_lyrics,
- current_style,
- current_cover_specification,
- current_round,
- total_rounds,
- unresolved_errors,
- status.

Statusy: `initialization`, `active_round`, `final_check`, `finalization`, `cover_creation`, `final`.

### Przebieg jednej rundy

Każda runda musi mieć pełny przebieg:

```text
MODERATOR — OTWARCIE
→ MUZYK
→ POETA
→ PROMPTCISTA
→ KRYTYK
→ MODERATOR — ZAMKNIĘCIE
```

System wykonuje dokładnie liczbę rund podaną przez użytkownika. Poprawki po ocenie Krytyka należą do bieżącej rundy i nie zwiększają jej numeru.

### Kontrola jakości

Krytyk sprawdza:

- prawdziwość i konsekwencję rymów,
- rytm, długość wersów, sylaby i śpiewność,
- gramatykę i naturalność języka,
- spójność fabuły i zakończenia,
- siłę oraz zapamiętywalność refrenu,
- zgodność Style Promptu z utworem,
- każde wymaganie użytkownika jako `SPEŁNIONE` albo `NIESPEŁNIONE`.

Wynik rundy: `PASS` albo `FAIL`. Przy `FAIL` trzeba wskazać konkretny problem, miejsce, odpowiedzialną rolę i wymaganą poprawkę. Błąd poprawia właściwa rola, a zależne elementy są następnie aktualizowane i ponownie kontrolowane.

### Lyrics i Style Prompt

- Lyrics używa tagów Suno, np. `[Verse]`, `[Chorus]`, `[Bridge]`, `[Outro]`.
- Lyrics nie może zawierać instrukcji technicznych, tempa, instrumentacji ani sposobu wokalu.
- Style Prompt ma być po angielsku, zwięzły i opisywać gatunek, tempo, instrumenty, wokal, rytm, atmosferę, dynamikę i wykonanie.
- Nie wolno polecać bezpośredniego kopiowania stylu konkretnego artysty; należy opisywać cechy muzyczne.

### Kontrola finalna

Po wszystkich rundach Krytyk wykonuje osobną kontrolę końcową, która nie jest dodatkową rundą. Proces może przejść dalej dopiero po `FINAL PASS`. Przy `FINAL FAIL` właściwa rola wykonuje obowiązkową poprawkę, zależne elementy są aktualizowane, a Krytyk sprawdza wynik ponownie.

### Okładka

COVERMASTER uruchamia się dopiero po `FINAL PASS` i zatwierdzeniu TITLE, LYRICS oraz STYLE PROMPT. Przygotowuje scenę, postać lub obiekt, tło, symbolikę, kompozycję, światło, kolorystykę, typografię, tekst i elementy zabronione.

Obowiązujący format S-COVER:

```text
543 × 807 px
Aspect ratio: 543:807
Simplified ratio: 181:269
```

Domyślnie okładka zawiera TITLE. Jeśli podano artystę lub autora, tekst jest rozszerzany zgodnie ze specyfikacją. Jeżeli użytkownik poda własny tekst okładki, należy użyć dokładnie jego treści bez dodatkowych napisów.

Sekcja S-COVER zawiera finalną specyfikację/prompt okładki, a nie wygenerowany plik graficzny. Specyfikacja nie może zmieniać fabuły, zakończenia, tytułu, symboliki ani zatwierdzonego tekstu.

### Tryby

- AUTO — pełny proces bez pytań między rundami, poza nierozwiązywalnymi sprzecznościami lub brakiem kluczowych danych.
- MANUAL — zatrzymanie po inicjalizacji, każdej pełnej rundzie, FINAL CHECK i specyfikacji COVERMASTER.

### Zasady bezwzględne

- Dokładnie podana liczba pełnych rund.
- PROMPTCISTA obecny w każdej rundzie.
- Każda runda zamknięta przez MODERATORA.
- Poprawki kierowane do właściwych ról.
- Osobna kontrola finalna.
- Brak finalizacji po `FAIL` lub `FINAL FAIL`.
- COVERMASTER dopiero po `FINAL PASS`.
- Zachowanie prawdziwego zakończenia historii.
- Rozdzielenie analizy COVERMASTER od finalnej specyfikacji S-COVER.

### Docelowy format odpowiedzi

```text
--- TITLE ---
<zatwierdzony tytuł>

--- LYRICS ---
<czysty finalny tekst>

--- STYLE PROMPT ---
<finalny prompt dla Suno>

--- COVERMASTER ---
<finalna specyfikacja okładki>

--- S-COVER ---
<finalna specyfikacja/prompt okładki>
```

## 2026-07-22 — EasyTeam: workflow wdrożony

### Status

Zakończone i połączone z gałęzią `main`.

### Zakres wdrożenia

- AUTO pobiera liczbę pełnych rund z ostatniej samodzielnej dodatniej liczby całkowitej w briefie; bez liczby używa 2 rund.
- Każda pełna runda ma sześć obowiązkowych etapów: MODERATOR → MUZYK → POETA → PROMPTCISTA → KRYTYK → MODERATOR.
- PROMPTCISTA uczestniczy w każdej rundzie, a Style Prompt rozwija się równolegle z Lyrics.
- Stan zawiera `current_title`, `current_lyrics` i `current_style`; TITLE powstaje najpóźniej w pierwszej rundzie i zmienia się razem z historią.
- Po wszystkich rundach działa osobny finalny gate KRYTYKA. `FAIL` blokuje dalszy proces aż do poprawki i ponownego `PASS`.
- COVERMASTER uruchamia się wyłącznie po finalnym `PASS` i przygotowuje analizę oraz finalną specyfikację S-COVER w rozmiarze `543 × 807 px`.
- Usunięto UTF-8 BOM ze wszystkich plików tekstowych w repozytorium.

### Weryfikacja i publikacja

- Testy regresyjne: **27/27 PASS**.
- Commit wdrożeniowy: `90e3aff` (`Fix EasyTeam round workflow and final validation`).
- Pull request: `#1`.
- Merge do `main`: `f4ae0f0`.

### Granice projektu

EasyTeam pozostaje zestawem promptów Markdown dla ChatGPT Project. Nie zawiera aplikacji, backendu, bazy danych ani osobnej roli generującej gotowy plik graficzny.

## 2026-07-22 — EasyTeam v1.1: poprawki po teście live

### Status

Kandydat lokalny v1.1 gotowy do przeglądu diffu przed commitem.

### Problemy wykryte w teście live

- pełny prompt ma więcej niż 8000 znaków i nie mieści się w polu ChatGPT Project Instructions,
- sam brief uruchomił AUTO bez oczekiwania na komendę `0`,
- KRYTYK zaakceptował nieuzasadnioną formę `Nový hry` w czeskim tekście.

### Poprawki v1.1

- skrócono pojedynczy `prompts/chatgpt-project-instructions.md` do mniej niż 8000 znaków; loader i drugi project source nie są potrzebne,
- sam brief ustawia stan inicjalizacji i czeka na osobne `0`,
- rozdzielono tolerancję mieszanego wejścia użytkownika od obowiązku standardowego czeskiego wyjścia,
- POETA i KRYTYK otrzymali jednoznaczne reguły dla form `Nový hry` → `Nové hry`,
- dokumentację instalacji ujednolicono z rzeczywistym limitem ChatGPT Project.

### Weryfikacja

- główny prompt: **5973 znaki**, poniżej limitu 8000,
- wykonano dokładnie jeden test akceptacyjny live: **1 PASS / 0 FAIL**,
- sam brief poprawnie czekał na osobne `0`,
- po `0` wykonano dokładnie trzy pełne rundy, a PROMPTER, KRYTYK i końcowy MODERATOR wystąpili w każdej,
- błędy z rund 1 i 2 zostały przekazane do kolejnych rund; TITLE zmienił się z `Ještě jeden level` na `Ještě jeden quest`,
- osobny final gate zwrócił `FINAL GATE: PASS`, a COVERMASTER i S-COVER pojawiły się dopiero potem,
- po teście poprawiono wyłącznie czeskie sformułowanie `celé číslice` na precyzyjne `celého čísla`; zgodnie z decyzją użytkownika nie uruchamiano drugiego testu,
- drugi prompt/source i loader zostały usunięte z projektu ChatGPT; obowiązuje jedno Project Instructions.

## 2026-07-22 — EasyTeam Main: start `GO`

### Status

Wariant `GO` został opublikowany na `main`, wstawiony do Project Instructions i sprawdzony jednym testem live. Wynik dokumentacyjny testu jest lokalnie gotowy do przeglądu przed kolejnym commitem.

### Decyzja

- komendę startową `0` zastąpiono jednoznacznym `GO`, akceptowanym niezależnie od wielkości liter,
- w głównym projekcie pozostają tylko `GO` i `?`,
- usunięto globalne komendy `1–9`, `ano` i `ne`,
- po finalnym wyniku session kończy się bez menu tuningu,
- tuning zostanie zaprojektowany później jako osobny projekt ChatGPT.

### Docelowy przebieg

`brief → GO → wszystkie pełne rundy → finalny PASS → TITLE + LYRICS + STYLE PROMPT + COVERMASTER + S-COVER → koniec session`.

### Weryfikacja statyczna

- główny prompt ma **6126 znaków** i mieści się w limicie 8000,
- repozytorium nie zawiera plików z UTF-8 BOM,
- wszystkie sprawdzane reguły `GO`, rund, final gate i COVERMASTER przeszły kontrolę statyczną,
- nowy live Test 28 z `GO`: **PASS** dla struktury workflow — brief czekał na `GO`, wykonano dokładnie 3 pełne rundy, PROMPTER wystąpił 3 razy, finalny gate zakończył się `PASS`, a COVERMASTER uruchomił się dopiero potem,
- sesja zakończyła się komunikatem o gotowości dla Suno bez menu tuningu,
- decyzja artystyczna użytkownika: `dnes / quest` brzmi wystarczająco podobnie w szybkim czeskim punku i zostaje zaakceptowane jako funkcjonalny rym przybliżony,
- użytkownik przetestował finalny utwór w Suno i samodzielnie przygotował S-cover według wygenerowanej specyfikacji,
- praktyczny rezultat utworu oraz coveru został przez użytkownika oceniony pozytywnie; live acceptance EasyTeam v1.1 zakończył się pełnym `PASS`,
- historyczny live test z komendą `0` pozostaje opisany jako baseline.
