---
title: "ISSUE-044 — Family wreaths at the portrait: the families a person comes from, inherited from the father by default"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-17
verdict-reviewer: self-check
source: "[[2026-10-14-opowiesc-rodziny-i-wieniec]] → d) · `/pm` 2026-10-16: autor przenosi wieńce przed instalację („tak róbmy to”) i podaje definicję · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-17
---

# ISSUE-044 — Wieńce rodzin przy portrecie

> Autor 2026-10-14 (stop #2 ISSUE-037): *„chciałbym móc w wyborze portretu dla niej customowy wieniec, który byłby związany z danym
> nazwiskiem”*. 2026-10-16 w `/pm`: wieńce **symbolizujące rodziny, z których wywodzi się dana osoba (domyślnie dzieci przejmują po ojcu)** —
> i *„tak róbmy to”*: teraz, a nie po instalacji MVP.

## Two earlier decisions this changes — on purpose
1. **[[style-b]] reguła 8 i [[osoba]] D3 — „bez gałązek” wokół portretu** (choć referencja R4 je miała). Wraca do decyzji na prototypie.
2. **Kolejność z 2026-10-14** („c) i d) po instalacji MVP”) — d) idzie teraz; c) (opowieść na drzewie) zostaje po instalacji.

## What to build
1. **Najpierw `ui` w trybie discovery** — klikalny prototyp panel po panelu (retro 3, R4), link `file:///` (retro 4, R1). Pytania (z INBOX d i
   z nowej definicji):
   - czym jest wieniec (gałązki jak w R4, liście, ramka z motywem) i czy jest symbolem religijnym (reguła 8);
   - **jedna linia czy obie** — „rodziny, z których się wywodzi” może znaczyć linię ojca i matki;
   - kobieta z nazwiskiem rodowym („z d.”, [[FR-005-nazwisko-rodowe]]): wieniec rodu ojca, czy po ślubie inny;
   - wyjątek ręczny: kiedy dziecko nie przejmuje po ojcu (np. ojciec nieznany);
   - gdzie widać: portret w widoku osoby, węzły drzewa, karta, tryb prezentacji;
   - grafika: `ui` pisze prompty do DALL-E, autor generuje i odsyła (jak przy [[ISSUE-046-icons]]) — motywy wieńców to nie dane rodziny.
2. Potem plan i budowa: **wieniec wyliczany z drzewa po linii ojca**, zapisane tylko: wieńce rodów (nazwa, motyw) i wyjątki przy osobie — nowa
   tabela, zmiana schematu (test migracji, kopia ją niesie).

## Acceptance Criteria
> AC-1…AC-3 z pozycji; AC-4…AC-6 dopisane po discovery (propozycje `ui`, [[wieniec]] *AC → element*), przyjęte „tak” na stopie #1 (2026-10-17).
- **AC-1** *Given* ojciec z wieńcem rodu *When* dodaję mu dziecko *Then* dziecko ma ten wieniec bez dodatkowego kroku.
- **AC-2** *Given* osoba z wieńcem po ojcu *When* zmieniam jej wieniec ręcznie *Then* zmiana dotyczy tej osoby (i jej linii), a reszta rodu zostaje.
- **AC-3** *Given* kopia z wersji sprzed tej pozycji *When* odtwarzam ją w nowej *Then* dane są kompletne (test migracji, próbne odtworzenie).
- **AC-4** *Given* kobieta z małżeństwem *When* otwieram jej widok *Then* lewa połowa wieńca to jej ród, prawa — ród męża z ostatniego małżeństwa; brakująca
  połowa wypełnia całość.
- **AC-5** *Given* rody w rodzinie *When* oglądam drzewo albo tryb prezentacji *Then* osoby mają wieńce, a wieńce pary się nie nakładają.
- **AC-6** *Given* ród *When* zmieniam jego kolor albo wzór *Then* wieniec zmienia się u wszystkich osób z tym rodem (także w połowie).

## Notes
- Prototyp to tylko decyzje autora, więc może iść równolegle z budową [[ISSUE-041-google-play-and-safe-update]]…[[ISSUE-043-grave-paid-until]];
  budowa przed instalacją, jeśli zmieści się w terminie — inaczej po wyjeździe (zmiana bazy na prawdziwych danych, z testem migracji).

## Implementation plan
> `planning`, 2026-10-17. **Pozycja z ekranem (zmiana trzech istniejących, jeden nowy):** specyfikacja [[wieniec]] **v1.0** (A–F, reguły liczenia
> B1–B7, D1–D17) oraz [[osoba]] v2.6 (3, 4a), [[wpis-osoby]] v5.10 (4b), [[drzewo]] v1.18 (4, 11); wytyczne [[style-b]] **v1.33** (reguły 1, 2, 8,
> 14, nowa rola: kolory rodu). Bez US (task-level, z pomysłu autora), krok UJ-001 · 5 i widok 5.
> **Prototyp (discovery, decyzje autora):**
> `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/2aa5d062-71fb-4ca0-b949-aea0dc7465d8/scratchpad/wience-044.html`
> (panele 1–6; panel 3 — Ś1 — zastąpiony przez D14) i
> `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/3c71c787-79b5-42e3-bf37-7b9aec487ca0/scratchpad/wience-044-b.html`
> (panele 7–9: 19 wzorów, Ś3, kolor C3).
> **Decyzje autora z discovery** (2026-10-16/17, [[wieniec]] *Decisions*): DALL-E (D1), ok. 20 wzorów (D2; jest 19, bez maku — D12), kolor do
> zmiany (D3), K2 (D5), paleta 12 (D6), L1 — cały wieniec po ojcu (D7), raz u szczytu linii, O1 (D9), G2 — widok osoby, drzewo i telewizor (D10),
> podpis „Ród: …” (D11), **Ś3 — pół panieński, pół po mężu (D14)**, **C3 — tłoczenie i przejście tonu (D15)**.

> **Stop #1 — 2026-10-17, autor: *„tak”*** na pytanie o obrazy („tak” = R). **R:** 19 obrazów w `grobing-code/assets/wreaths/`, wąski wyjątek w
> `.gitignore` i w strażniku (tylko szare `wieniec-*.png`). AC-4…AC-6 przyjęte, decyzje z planu przyjęte.

### Decision for stop #1 (author) — jedno pytanie
**Skąd aplikacja weźmie obrazy wieńców?** 19 obrazów z DALL-E to pliki PNG, a ochrona danych rodziny (`.gitignore` w `grobing-code` i strażnik
Claude'a) nie wpuszcza do repo żadnego PNG poza ikonami aplikacji (`android/app/src/main/res/`). To Twoja ochrona, więc decyzja jest Twoja:
- **R (rekomendacja) — obrazy w repo, w jednym katalogu.** `assets/wreaths/` w `grobing-code`, tylko pliki `wieniec-<wzór>.png`. To drugi wąski
  wyjątek obok ikon. Strażnik Claude'a przepuszcza tam **tylko szare obrazy** 640 × 640, więc kolorowego zdjęcia nie wpuści. Ty nic nie robisz,
  a aplikacja buduje się z czystej kopii repo. Koszt: wyjątek w ochronie; gdyby klasyfikator nie pozwolił mi zmienić strażnika, dostaniesz kilka
  linii do wklejenia.
- **P — obrazy poza repo, jak lista miejsc.** Aplikacja buduje się z Twoich plików, które trzymasz u siebie (np. na Dysku). Ochrona bez zmian.
  Koszt: bez tych plików wieńców nie zbuduje nikt — ani agent na nowym komputerze, ani ktoś z publicznego repo.
- **S — wieńce przerysowane na krzywe (SVG w repo).** Ochrona bez zmian, wszystko w repo. Koszt: nowa biblioteka do rysowania SVG, cieniowanie C3
  liczone w aplikacji i ok. 1–2 dni więcej przy terminie 29.10, a przerysowanie drobnych żyłek może zmienić wygląd.

**„tak” = plan jak niżej z R.**

### Decisions taken in the plan (visible at stop #1, no question)
- **Model — ADR-021 (≥3 opcje, pisze łańcuch `planning` → `docs`):** **M1 (wybrane)** — nowa tabela `clans` (nazwa, klucz wzoru, klucz koloru) i
  dwie kolumny w `persons`: `clan_id` (ród wybrany przy osobie, opcjonalny) i `no_wreath` (wybrane „bez wieńca”). **Zapisany jest tylko wybór**, a
  wieniec każdej osoby liczy się z drzewa przy odczycie (B1–B7), jak ścieżka „Jak łączy się ze mną”. Odrzucone:
  - **M2 — ród przy rodzinie (`families`)** — rodzina to związek, a wieniec dziedziczy się po osobie (ojcu); przy Ś3 jedna rodzina miałaby dwa rody;
  - **M3 — ród z nazwiska** (bez zapisu wyboru) — nazwisko zmienia się po ślubie, ma literówki, a jedno nazwisko może mieć dwa rody;
  - **M4 — wieniec zapisany przy każdej osobie** — zmiana u szczytu linii to dziesiątki zapisów, a po zmianie drzewa wieniec rozjeżdża się z rodziną.

  Schemat **v14 → v15** (`createTable` + `addColumn` ×2, bez zmiany wierszy). Kopia i eksport niosą tabelę same, bo kopią jest cała baza
  ([[ADR-018-export-is-the-backup]]).
- **Nazwa rodu jest unikalna bez wielkości liter i polskich znaków** — sprawdza to kod (`fold` z `lib/data/folding.dart`, jak wyszukiwarka), a nie
  indeks SQLite, bo `NOCASE` nie zna polskich liter.
- **Wybór rodu i ród zapisują się od razu** ([[wieniec]] D16), jak „Rodzina” w tym samym formularzu; „Zapisz” formularza ich nie dotyczy. Każdy
  zapis zamawia kopię w tle, jak każdy.
- **Obrazy wzorów:** narzędzie `tool/wreaths/` (Python z Pillow i numpy — algorytm C3 sprawdzony w discovery, skrypty `wreathlib.py` i
  `build_colour.py` w katalogu tymczasowym sesji `3c71c787-…`; `dev` może je przenieść albo przepisać na Darta) robi z 19 obrazów autora po jednym
  pliku 640 × 640: kształt liści, mapa cieniowania C3 (najciemniej 80%) i obwódka w kolorze tła (0,75% płótna). **Kolor nakłada aplikacja raz na
  parę wzór–kolor** i zapamiętuje gotowy obraz; Ś3 składa dwie połówki z dwóch takich obrazów. W klatce drzewa — tylko rysowanie gotowych obrazów,
  bez rozmycia i bez warstwy krycia na węzeł (retro 4, R3).
- **Kolejność budowy:** dane i liczenie → widok osoby → formularz i ród → drzewo i tryb prezentacji. Drzewo idzie w tej pozycji, bo rodzina będzie
  je oglądać na telewizorze w czasie wyjazdu, a w trakcie wyjazdu aktualizacji nie ma (retro 4 → *Product decisions*).
- **Emulator `Grobing_Restore`:** instalacja nad v14, bez czyszczenia danych. Wpisów dodanych przez autora (cmentarz i grób z 2026-10-16) nie
  zastępujemy, więc pytanie o ich zastąpienie nie jest potrzebne. Rody nadaje `dev` wymyślonym osobom przez aplikację — to zarazem przejście
  formularza. Po instalacji sprawdzamy migawkę `pre-update/grobing-v14.db`.

### Steps (`dev`)
1. **Schemat v15** — `lib/data/database.dart`: tabela `Clans` (`id`, `name`, `motif` — klucz wzoru, `colour` — klucz koloru; klucze z [[wieniec]]
   A) · `Persons.clanId` (FK, opcjonalny) · `Persons.noWreath` (bool, domyślnie fałsz) · krok `_from14To15` · `currentSchemaVersion = 15` ·
   `make-migrations`, `build_runner`.
2. **Dane:**
   - `lib/data/clans.dart` — rody: lista z liczbą osób, nowy (z wyborem dla osoby w jednej transakcji), poprawa (nazwa, kolor, wzór), unikalna
     nazwa (`fold`); wybór dla osoby: ród · „bez wieńca” · dziedziczy (czyści oba);
   - `lib/data/wreaths.dart` — **czysta funkcja** liczenia B1–B7: z osób (płeć, wybór), rodzin (rodzice, dzieci), związków (małżeństwo, kolejność
     jak `TreeUnion.startKey`) i rodów → wieniec osoby (lewa, prawa) i źródło (po ojcu · wybrane tutaj · wyjątek · bez · Ś3 z mężem). Pętla →
     brak (pamięć odwiedzonych). Potomkowie po linii ojca do F5 i E1;
   - `family_tree.dart` (`TreePerson`, `loadFamilyTree`, `watchTables` + `clans`) i `person_view.dart` niosą wybór i rody.
3. **Obrazy (R):** `tool/wreaths/` + 19 plików w `assets/wreaths/` + `pubspec.yaml` (`assets`); `.gitignore` — wyjątek
   `!/assets/wreaths/wieniec-*.png`; strażnik `grobing-agents/.claude/hooks/family-data-guard.ps1` — drugi katalog wyjątku z warunkiem „szary obraz
   640 × 640”, z testami w `.claude/hooks/tests/`; `family-data.md` → tabela *Mechanisms* (wyjątek). Klasyfikator odmówi zmiany strażnika → linie
   dla autora, nie obejście.
4. **Kolory** — `lib/app/theme.dart`: 12 kolorów rodu ([[wieniec]] → *Style B rules applied*) z kluczami.
5. **Rysowanie wieńca** — `lib/app/widgets/wreath.dart`: obraz wzoru → kolor rodu (C3, obwódka) raz na parę i pamięć podręczna; Ś3 — dwie połówki;
   wieniec bez dotyku i poza czytnikiem; obraz bez odczytu → bez wieńca.
6. **Widok osoby** — `lib/app/person/person_screen.dart`: [[wieniec]] C1–C3 (płótno 208 dp, portret w (0,50; 0,434), imię 8 dp pod wieńcem, „Ród:
   …” z twardą spacją po „·”).
7. **Formularz i ród** — `lib/app/grave/person_form_screen.dart` (wiersz 4b, tylko w poprawie, stany E1, E1a) i nowy
   `lib/app/person/clan_screen.dart` (arkusz E2, ekran „Nowy ród” / „Ród” F: kolor domyślnie pierwszy wolny, wzór pierwszy wolny, F5, błąd
   nazwy).
8. **Drzewo** — `tree_layout.dart` (`TreeMetrics.slot = max(96, 80 × skala tekstu)`, gdy ktoś ma wieniec; ślad w bok od 43 dp), `tree_screen.dart`
   (wieniec pod węzłem, kolejność D1, wyszarzenie z osobą), `tree_painter.dart` (ślad), tryb prezentacji (`tree_presentation.dart`) — to samo.
9. **Dane wymyślone** — `lib/dev/fictional_data.dart`: 4 rody (wymyślone nazwy z rdzeni „Wymyśl-”, „Zmyśl-”, „Testow-”, „Przykład-”) u szczytów linii,
   jeden wyjątek, jedno „bez wieńca”, kobiety po ślubie z mężem z rodem i bez.
10. **README** `grobing-code` → *Baza danych* (v15) i nowa sekcja *Wieńce* (skąd obrazy, jak przebudować, licencja: obrazy wygenerowane przez autora).
11. **Przejście AC na emulatorze** (stała lista `dev`, retro 3 i 4):
    - każdy stan z [[wieniec]] *States* ze zrzutem: widok osoby (po ojcu, Ś3, B5, bez rodu, portret bez zdjęcia, pasmo ze zdjęciem i bez), wiersz
      E1 w każdym stanie, arkusz E2 (pusty i z rodami), F nowy i poprawa, błąd nazwy;
    - tekst 200% na 360 dp: widok osoby, wiersz, arkusz, F (siatka 3 kolumn i koła kolorów), drzewo (`max(96, 160)`);
    - semantyka i cel dotyku 48 dp (koła kolorów, kafle wzorów, ✎ w arkuszu);
    - **klatki drzewa** z wieńcami u ok. 100 osób: przesuwanie i przestawienie środka, naprzemiennie z buildem odniesienia (APK sprzed pozycji);
    - migracja nad danymi: liczby wierszy przed i po, migawka v14;
    - **„mieści się” liczbą** (retro 4, R3): wieniec w widoku osoby na 360 dp, najgorszy przypadek (lipa, kasztanowiec) przy 100% i 200%.

### Files likely touched
`grobing-code`:
- schemat: `lib/data/database.dart`, `database.g.dart`, `database.steps.dart`, `drift_schemas/grobing/drift_schema_v15.json`,
  `test/drift/grobing/generated/*` (generowane);
- kod: `lib/data/clans.dart` (nowy), `lib/data/wreaths.dart` (nowy), `lib/data/family_tree.dart`, `lib/data/person_view.dart`, `lib/app/theme.dart`,
  `lib/app/widgets/wreath.dart` (nowy), `lib/app/person/person_screen.dart`, `lib/app/person/clan_screen.dart` (nowy),
  `lib/app/grave/person_form_screen.dart`, `lib/app/tree/tree_layout.dart`, `tree_screen.dart`, `tree_painter.dart`, `tree_presentation.dart`,
  `lib/dev/fictional_data.dart`, `pubspec.yaml`, `.gitignore`, `README.md`;
- obrazy i narzędzie: `assets/wreaths/wieniec-*.png` (19), `tool/wreaths/*`;
- testy (`qa`): `test/drift/grobing/migration_test.dart`, `test/data/clans_test.dart` (nowy), `test/data/wreaths_test.dart` (nowy),
  `test/data/family_tree_test.dart`, `test/app/person/person_screen_test.dart`, `test/app/person/clan_screen_test.dart` (nowy),
  `test/app/grave/*` (formularz), `test/app/tree/tree_layout_test.dart`, `tree_screen_test.dart`, `tree_presentation_test.dart`,
  `test/backup/restore_service_test.dart`, `test/repo_invariants_test.dart` (wyjątek w `.gitignore`).

`grobing-agents` (R): `.claude/hooks/family-data-guard.ps1`, `.claude/hooks/tests/*`, `.claude/rules/family-data.md`.

`grobing-vault` (`docs` przy zamknięciu): ADR-021 · `04_ARCHITECTURE/data-model.md` (`clans`, `persons.clan_id`, `persons.no_wreath`, v15) ·
`backup-format.md` (v15 w kopii) · specyfikacje `05_DESIGN/` z discovery (już napisane przez `ui`: [[wieniec]], [[osoba]], [[wpis-osoby]],
[[drzewo]], [[style-b]]) · AC pozycji przepisane według tabeli niżej.

### AC mapping
AC-1…AC-3 z pozycji; **AC-4…AC-6 dopisane po discovery** (propozycje `ui`, [[wieniec]] *AC → element*) — „tak” na stopie #1 je przyjmuje, a `docs`
przepisuje sekcję *Acceptance Criteria* przy zamknięciu.

| AC | Kroki | Dowód |
|---|---|---|
| AC-1 — ojciec z wieńcem, dziecko dostaje go bez kroku | 2, 6, 7 | test `wreaths`: syn, wnuk, córka po ojcu; test widżetu: widok syna z wieńcem i „Ród: Wymyślscy”, wiersz „Po ojcu: …”; zrzut |
| AC-2 — zmiana ręczna dotyczy tej osoby (i jej linii), reszta rodu zostaje | 2, 7 | test `wreaths`: wyjątek u syna → jego dzieci po nim, ojciec i siostra bez zmian; „Wróć do wieńca po ojcu”; „bez wieńca”; test widżetu E1/E1a; zrzut |
| AC-3 — kopia sprzed pozycji odtwarza się kompletna | 1 | test migracji v14 → v15 (każdy wiersz każdej tabeli bez zmian, rodów brak); generowane v1…v14 → v15; odtworzenie kopii v14 w v15; próbne odtworzenie kopii v15 z rodami na drugim emulatorze |
| AC-4 — kobieta po ślubie: pół panieński, pół po mężu | 2, 5, 6 | test `wreaths`: B4 (ostatnie małżeństwo, „razem” się nie liczy), B5 (mąż bez rodu, ona bez rodu), B6 (dzieci cały wieniec ojca), osoba bez płci; widok z „Ród: X · po mężu Y”; zrzut |
| AC-5 — wieńce na drzewie i w trybie prezentacji, pary się nie nakładają | 8 | test `tree_layout`: 96 dp z wieńcem, 80 dp bez, `max(96, 80 × skala)` przy 200%; ślad w bok od 43 dp; test widżetu: wieniec pod węzłem, znicz nad nim; zrzuty drzewa i trybu prezentacji |
| AC-6 — zmiana koloru albo wzoru rodu zmienia go u wszystkich | 2, 7 | test `clans`: poprawa koloru → wieniec wszystkich osób rodu (także połowa Ś3); F5 „Zmiana dotyczy N osób”; zrzut |

### Tests (`qa`)
- **Migracja:** v14 → v15 z danymi (wszystkie tabele bez zmian, `clans` pusta, `clan_id` puste, `no_wreath` fałsz); wygenerowane testy z każdej wersji.
- **Odtworzenie:** kopia v14 w aplikacji v15 przez migrację; kopia v15 z rodami i wyborami wraca taka sama.
- **`wreaths.dart` (czysta funkcja):** B1–B7 każda osobno — ojciec bez płci, dziecko w dwóch rodzinach, wybór · „bez” · dziedziczenie, O1, wyjątek
  dziedziczony przez dzieci, Ś3 (ostatnie małżeństwo według daty i bez dat, „razem” pominięte, mąż bez rodu, ona bez rodu, obie połowy brak),
  koniec związku nie zmienia, **pętla w drzewie nie zawiesza**; potomkowie po linii ojca (F5, E1).
- **`clans.dart`:** nowy ród z wyborem w jednej transakcji; unikalna nazwa („Wymyślscy” = „wymyslscy”); poprawa; liczba osób.
- **Widżety:** widok osoby (wieniec, podpis, odstęp imienia); wiersz E1 w każdym stanie, E1a; arkusz E2 (zaznaczenie z `check` i stanem „zaznaczone”,
  ✎, „Bez wieńca” tylko gdy ma sens); F (domyślne pierwsze wolne, błąd nazwy, F5); drzewo (slot, kolejność warstw, ślad); tryb prezentacji;
  `meetsGuideline` (retro 3, R2), tekst 200%.
- **Repo:** `repo_invariants_test` — wyjątek `assets/wreaths/wieniec-*.png` nie wpuszcza innych typów (np. `*.db`) ani innych nazw; testy strażnika
  (kolorowy PNG w katalogu → odmowa, szary 640 × 640 → przepuszcza, inny katalog → odmowa).
- **Pełny przebieg:** `flutter test --timeout 120s`, `flutter analyze`, `dart format`.
- **Przegląd `ui`** (subagent) przed stopem #2.

### Manual verification
**Agent na emulatorze (przed stopem #2):** krok 11 z *Steps* — zrzuty stanów, 200% na 360 dp, klatki drzewa naprzemiennie z buildem odniesienia,
migracja v14 → v15 nad danymi (liczby wierszy, migawka v14), próbne odtworzenie kopii v15 na drugim emulatorze (po kolei, nie równolegle — RAM).

**Autor — odczucie (najwyżej 3, na emulatorze):**
1. Otwórz wymyśloną osobę z wieńcem, a potem kobietę po ślubie. Czy wieniec wokół portretu wygląda godnie i czy pół na pół czyta się od razu?
2. W poprawie osoby u szczytu linii załóż nowy ród (nazwa, kolor, wzór). Czy to zrozumiałe i dość szybkie przy kilkunastu liniach?
3. Drzewo i tryb prezentacji z wieńcami: czy drzewo nie jest za gęste i czy rody widać?

**Lista B — odczucie na telewizorze** ([[ISSUE-032-mvp-install]] → *Hand checks*, retro 4 R4): wieńce w trybie prezentacji z kanapy.

### Out of scope
- usuwanie rodu ([[wieniec]] D16 → *Obali*);
- mak (D12) — może dojść aktualizacją, bez zmiany schematu;
- L2 — ród matki w drugiej połowie (D7);
- wieniec zmieniany suwakiem czasu albo dniem ślubu (B7);
- wieniec w okręgach 40 dp i mniejszych: lista osób, karta grobu, mini-drzewo, łańcuch, karta drzewa, kafle okna (D10);
- wybór rodu przy dodawaniu nowej osoby („nowy grób”, „kolejna osoba”) — tylko w poprawie (D9);
- dowolny kolor spoza palety (D6);
- rody w eksporcie GEDCOM (eksportem jest kopia, [[ADR-018-export-is-the-backup]]).

### Obali (falsifiers)
- Klatki drzewa z ok. 100 wieńcami wyraźnie gorsze od buildu odniesienia → mniej szczegółu na drzewie (obraz mniejszej rozdzielczości dla węzła) przed
  stopem #2; gdyby nie wystarczyło — decyzja autora o wieńcach na drzewie (G1/G3 z prototypu).
- Przy 96 dp tryb prezentacji nie mieści rodziny na poziomie 2 w kadrze telewizora → [[wieniec]] D17 → *Obali* (mniejszy wieniec na drzewie).
- Na stopie #2 C3 wygląda ciężko na małym węźle → C1 na drzewie (mniej cienia), C3 w widoku osoby.

### Sources
[[wieniec]] v1.0 (pomiar 19 wzorów, kontrast C3) · [[style-b]] v1.33 · WCAG 2.2 SC 1.4.1, 1.4.11 · obrazy autora (Pobrane, 2026-10-17, poza repo) ·
[[ADR-018-export-is-the-backup]] · [[ADR-012-person-sex-and-union-timeline]] (płeć, związek) · retro 4 R3 (pomiar klatek, „mieści się” liczbą).

## Dev report
> `dev`, 2026-10-17. Flutter 3.41.1 (przypięty). `flutter analyze` czyste, `dart format` bez zmian. Testy: 844 zielonych, 14 czerwonych — wszystkie
> do aktualizacji przez `qa` (*For `qa`*), żaden nie pokazuje błędu w kodzie pozycji.

### Changed (`grobing-code`)
- **Schemat v15** (krok 1): `Clans` (`name`, `motif`, `colour` — klucze), `Persons.clanId`, `Persons.noWreath`; `_from14To15` (`createTable` + `addColumn` ×2);
  `drift_schema_v15.json`, `schema_v15.dart` (generowane).
- **Dane** (krok 2): `lib/data/clans.dart` — `WreathMotif` (19 kluczy, plik `assets/wreaths/wieniec-<klucz>.png`), `ClanColour` (12 kluczy), `Clan`,
  `WreathChoice`, `loadClans`/`watchClans`, `createClan` (z wyborem dla osoby w jednej transakcji), `updateClan`, `setWreathChoice`, nazwa unikalna przez
  `fold` (`ClanNameException`). `lib/data/wreaths.dart` — `WreathGraph` (czysta funkcja B1–B7: ojciec, ród własny z pamięcią i ochroną przed pętlą, mąż
  z ostatniego małżeństwa, połówki, `heirs`, `countWith`), `PersonWreath` (`left`, `right`, `origin`, `overridesFather`). `FamilyTreeData.wreaths`
  (`family_tree.dart`, czyta też `clans`), `PersonView.wreath` (`person_view.dart`).
- **Obrazy** (krok 3, R): `tool/wreaths/build_wreaths.py` (Python, Pillow, numpy — algorytm C3 z discovery) → 19 plików `assets/wreaths/wieniec-*.png`
  (szare z przezroczystością, 640 × 640, razem 3,5 MB); `pubspec.yaml`; `.gitignore` — `!/assets/wreaths/wieniec-*.png`.
  `grobing-agents`: `family-data-guard.ps1` — `Test-WreathImage` (nagłówek PNG: 640 × 640, typ koloru 4 — szary z przezroczystością) i drugi wyjątek w
  `Get-FamilyCategory`; `family-data.md` — wyjątek i to, czego nie łapie. **Klasyfikator nie zablokował zmian.** Próba na sucho: 19 obrazów przechodzi;
  kolorowy PNG `wieniec-proba.png` 640 × 640 — **odmowa** strażnika (plik usunięty po próbie).
- **Kolory** (krok 4): `GrobingColors.clan(ClanColour)` w `theme.dart`.
- **Rysowanie** (krok 5): `lib/app/widgets/wreath.dart` — `WreathFrame` (kadr A2), `WreathImages` (kolor rodu × cieniowanie z obrazu, obwódka w kolorze tła,
  połówki Ś3; raz na parę i rozmiar, w pamięci), `WreathView` (bez dotyku, poza czytnikiem), `WreathSign` (znak z okręgiem portretu; bez wieńca — okrąg
  przerywany), `clanLine` („Ród: X · po mężu Y”, twarda spacja ` `).
- **Widok osoby** (krok 6): wieniec pod portretem (płótno 208 dp), imię 8 dp pod wieńcem, podpis 4a.
- **Formularz i ród** (krok 7): `lib/app/person/clan_screen.dart` — `WreathFormRow` (E1, E1a), `showWreathSheet` (E2), `ClanScreen` (F: nazwa, 12 kół, wzory,
  F5, „Zapisz ród” / „Zapisz”); wiersz 4b w `person_form_screen.dart` tylko w poprawie.
- **Drzewo** (krok 8): `TreeMetrics.wreaths`, `traceSide` (43 dp), miejsce `max(96, 80 × skala)` (`tree_screen.dart` → `_metricsFor`), wieniec w `_TreeNode`
  pod imieniem i okręgiem (płótno 88 dp, `oversample` 1,5); osoba w środku przed narodzinami — bez wieńca. Tryb prezentacji — ten sam węzeł.
- **Dane wymyślone** (krok 9): `fictional_data.dart` — ojciec u szczytu linii (dąb), matka u szczytu swojej (laur, Ś3 z mężem), partnerka bez rodu (B5),
  dziecko drugiego związku „bez wieńca”.
- **README** (krok 10): *Baza danych* (v15) i nowa sekcja *Wieńce*.

### Emulator pass (`Grobing_Restore`, build profile, `--split-per-abi`, `FRAME_LOG`)
- **Migracja nad danymi:** przed: v14, `persons` 109, `families` 38, `family_children` 67, `family_partners` 76, `events` 180, `assertions` 287, `graves` 2,
  `burials` 2, `residences` 5, `media` 3, `person_media` 3, `cemeteries` 1, `sectors` 1, `settings` 1. Po: v15, **każda liczba bez zmian**, `clans` 0,
  `clan_id` i `no_wreath` puste. Migawka `pre-update/grobing-v14.db` jest. **Przy okazji:** pierwsze zatrzymanie aplikacji wypadło w trakcie migracji —
  przy bazie został gorący `grobing.db-journal`, a kopia pokazała v14 bez zmian; następne uruchomienie przeszło do v15. Przerwana migracja zostawia starą
  wersję całą (NFR-003). Kopie bazy do liczenia usunięte (był w nich wpis autora).
- **Stany ([[wieniec]] *States*), zrzuty `emu044\` w katalogu tymczasowym sesji `3c71c787-…`:** E1 „Brak” + „Wybierz ród” (`01`); arkusz pusty (`02`); „Nowy
  ród” (`03`, `04`); „Wybrane tutaj. Po tej osobie wieniec mają: Franciszek, Wiktoria, Stanisław i 21 innych osób.” (`05`); widok osoby z wieńcem i „Ród:
  Wymyslonowie” (`06`); Ś3 u Wiktorii — pół dębu, pół lauru, „Ród: Wymyslonowie · po mężu Zmyslickowie” (`09`); arkusz z zaznaczeniem i „po ojcu” (`12`);
  wyjątek z „Wróć do wieńca po ojcu” (`13`); „Bez wieńca” (`14`); poprawa rodu — kolor Miedź, „Zmiana dotyczy 35 osób.”, wszystkie wieńce linii w miedzi
  (`15`, `17` — AC-6); drzewo (`10`, `18`, `19`) i tryb prezentacji (`20`) z wieńcami; 200% na 360 dp (`21`–`30`).
- **Nazwy w przejściu** — ASCII z wymyślonych rdzeni („Wymyslonowie”, „Zmyslickowie” i 14 innych): `adb input text` nie pisze polskich liter.
- **Klatki** (retro 4, R3) — scenariusz: z „Ja” trzy kroki „−”, sześć przesunięć, trzy kroki „+”, dwa przestawienia środka; 12 rodów u szczytów linii (poprawione przez `qa` z bazy; „16” to były próby — u czterech osób ojciec miał już ród), wieńce
  u większości osób. **Naprzemiennie z buildem odniesienia** (APK ISSUE-043 na migawce v14 — stara aplikacja nie otwiera v15; skrypty `swap.sh`,
  `measure.sh`):

  | Przebieg | Klatki | Wolne (> 16,7 ms) | Rysowanie p50 / p90 | Budowanie p90 |
  |---|---|---|---|---|
  | nowy 1 | 462 | 14,5% | 14,7 / 17,1 ms | 4,9 ms |
  | odniesienie 1 | 471 | 17,4% | 14,9 / 17,2 ms | 4,1 ms |
  | nowy 2 | 449 | 12,5% | 14,4 / 16,9 ms | 4,8 ms |
  | odniesienie 2 | 464 | 18,1% | 15,0 / 17,2 ms | 4,6 ms |
  | nowy 3 | 427 | 15,0% | 14,5 / 16,9 ms | 4,6 ms |

  **Wieńce nie pogarszają ruchu drzewa** — różnice w szumie hosta (*Obali* planu się nie spełnia).
- **„Mieści się” liczbą** (retro 4, R3): widok osoby na 360 dp przy 100% i 200% — liście wieńca ok. 194 dp szerokości, najszerszy wzór (kasztanowiec, krawędzie
  1,3% od brzegu płótna) ok. 202 dp z 208 dp płótna: mieści się z ok. 79 dp z każdej strony. Drzewo przy 96 dp: między wieńcami pary ok. 11 dp, kreska pary
  widoczna (`10`, `18`).
- **Semantyka i cele dotyku** (`uiautomator dump`): koła kolorów 126 × 126 px = 48 dp, `clickable`, z nazwą koloru; kafle wzorów `clickable`; ✎ w arkuszu
  „Popraw ród”; „Zmień” z opisem „Zmień wieniec rodu”; wiersz E1 czytany jako „Wieniec rodu / … / …”.
- **Znalezione w przejściu i poprawione przed `qa`:**
  1. przycisk „Wybierz ród” leżał w `MergeSemantics` wiersza — czytnik scalał go z tekstem w jeden węzeł o wysokości 46 dp (test retro 3 R2) → przycisk
     poza scaleniem;
  2. ekran F miał pasek `AppBar` na powierzchni i pole podkreślone zamiast obramowanego → `BackTitleBar` i motyw pól formularza;
  3. kafle wzorów w `GridView` o stałej proporcji — przy „też: …” i dużym tekście przepełnienie → rzędy z `IntrinsicHeight`;
  4. **200% na 360 dp:** nazwa rodu łamała się w środku słowa w wierszu E1 („Wymyslono / wie”) i w arkuszu („Przykladowiczowi / e”) → przy tekście ≥ 150%
     znak i przyciski nad tekstem, tekst na całą szerokość; w F nazwy wzorów („Kasztan / owiec”) i rodów w „też:” → dwie kolumny przy ≥ 150%, nazwa
     w jednej linii (`FittedBox` w dół);
  5. koła kolorów po 7 w rzędzie przy 411 dp → odstęp 8 dp, 6 w rzędzie (F3).

### Deviations
1. **96 dp na osobę, gdy ktoś w całej rodzinie ma wieniec**, a nie „w pokazanym drzewie” ([[drzewo]] v1.18): miejsce nie może się zmieniać przy przestawianiu
   środka (drzewo by skakało). Bez rodów — 80 dp jak dziś.
2. **Układ przy tekście ≥ 150%** (wiersz E1, wiersze arkusza E2, dwie kolumny wzorów w F, nazwa w jednej linii) — specyfikacja go nie opisuje; ten sam próg co
   „Pokaż ›” w karcie drzewa ([[drzewo]] D20). Przyczyna: słowa łamane w środku (*Znalezione* 4).
3. **Obwódka (A5) liczona w aplikacji, nie w pliku:** plik niesie kształt i cieniowanie, a obwódkę dokłada `WreathImages` — kształt w kolorze tła rysowany 12 razy
   wokół, raz na parę i rozmiar. Grubość obwódki zależy wtedy od rozmiaru na ekranie (0,75% płótna), jak w A5.
4. **Jasne miejsca C3** (mnożnik > 1): kolor × mnożnik z obcięciem do bieli (`ColorFilter.matrix`), a nie „w stronę bieli” jak w skrypcie discovery. Na zrzutach
   różnicy nie widać; najciemniejsze miejsca (≥ 80%) bez zmian, więc kontrast z [[wieniec]] obowiązuje.
5. **Wieniec w węźle drzewa, nie na osobnej warstwie** pod wszystkimi węzłami ([[wieniec]] D1 w *Elements* D): w węźle wygasa i wyszarza się razem z osobą,
   bez warstwy na węzeł. Kolejność w obrębie węzła jest jak w D1; między węzłami wieńce się nie nakładają (połowa wieńca 43 dp < połowa miejsca 48 dp).

### Found, outside the item
- Nic nowego. Wpisy autora na `Grobing_Restore` (cmentarz i grób) nietknięte; wymyślonym osobom dodano 12 rodów (nazwy ASCII; liczba z bazy, `qa`), kolor „Wymyslonowie” zmieniony
  na Miedź (AC-6).

### For `qa`
- **14 czerwonych testów do aktualizacji:**
  - wersja i lista tabel (13): `test/data/database_test.dart` („user_version 14…”), `test/data/data_state_test.dart` („schema 14…”),
    `test/app/data_state_screen_test.dart`, `test/backup/restore_service_test.dart` — 10 testów odtworzenia v4…v14, które sprawdzają dokładną mapę tabel i
    wersję (dochodzi `clans`, wersja 15);
  - `test/app/person/residence_screens_test.dart` → „retro 3 R2 …”: po `ensureVisible('Dodaj miejsce')` przycisk „Wybierz ród” jest u góry ucięty przewijaniem
    (widać 46 z 48 dp) i `androidTapTargetGuideline` go łapie. Przycisk ma `minimumSize` 48 dp — to geometria przewinięcia w teście, nie rozmiar. Osoba w
    tym teście nie ma ojca w drzewie, więc wiersz jest w stanie „Brak”.
- **Nowe testy według planu** (*Tests*): `clans_test`, `wreaths_test` (B1–B7, pętla), `clan_screen_test`, migracja v14 → v15, odtworzenie v14 → v15 i v15 z
  rodami, drzewo (96 / 80 dp, `max(96, 160)` przy 200%, ślad od 43 dp), `repo_invariants_test` (wyjątek w `.gitignore`), testy strażnika w
  `grobing-agents/.claude/hooks/tests/family-data-guard.tests.ps1` (szary 640 × 640 z przezroczystością przechodzi; kolorowy, inny rozmiar, bez
  przezroczystości, inna nazwa, inny katalog — odmowa).
- **Kroki ręczne:** jak w *Manual verification* planu; agent zrobił krok 11 (wyżej). Dla autora — 3 kroki odczucia na `Grobing_Restore`: widok Wiktorii (Ś3) i
  Antoniego; nowy ród u Marianny Wymyślonej (żona Antoniego, bez ojca w drzewie — dziś nosi cały dąb męża, po założeniu rodu dostanie pół na pół); drzewo
  i tryb prezentacji.

### Round 2 — po przeglądzie `ui` (2026-10-17)
- **MAJOR — kafle wzorów (F4):** znak, nazwa i „też: …” stały u góry kafla, a wyższy sąsiad w rzędzie zostawiał pod nimi pustkę → treść kafla wyśrodkowana w
  pionie i w poziomie (`37-F-kafle-wysrodkowane.png`).
- **MINOR — ślad w bok:** 43 dp od środka dostawali wszyscy, gdy ktoś w rodzinie miał wieniec → tylko osoba z wieńcem (`TreeGraph.hasWreath`), reszta przy okręgu
  ([[wieniec]] D3, v1.1).
- **MINOR — twarde spacje:** „po mężu” w podpisie 4a i w wierszu E1; „ · ”, „7 osób” i „po ojcu” w opisie rodu w arkuszu ([[style-b]] reguła 6).
- **MINOR — brakujące zrzuty stanów** (a)–(e): `31`–`36` (B5 u Marianny, E1 z ojcem bez rodu, błąd nazwy w F, osoba z tłem i profilowym, drzewo przy 200%).
- **Znalezione przez `qa`:** ekran „Stan danych” pokazywał surowe nazwy tabel `clans` i `residences` (tej drugiej brakowało od [[ISSUE-042-places-of-residence]]) →
  „Rody” i „Miejsca zamieszkania” (`data_state_screen.dart`).

### Round 3 — po stopie #2 (2026-10-17, [[wieniec]] D20)
- **Ród odróżnia para wzór + kolor** (uwaga autora na stopie #2): „też: …” na kaflu wzoru tylko dla rodów z tym wzorem **w wybranym kolorze**; zmiana koloru
  przelicza „też”. Domyślny wybór nowego rodu: kolor i wzór, których nie ma nikt (jak dotąd), a gdy każdy wzór ma już ród — pierwszy wzór wolny w tym kolorze.
  `lib/data/clans.dart` — `firstFreeColour`, `firstFreeMotif`; `clan_screen.dart` — `usedBy` po parze. Tej samej pary aplikacja nie blokuje (D20).

## Verification
> `qa`, 2026-10-17. **Werdykt: APPROVED (self-check, z uwagami).** AC-1…AC-6 mają dowody w testach i w przejściu na emulatorze; przegląd `ui` — usterki
> poprawione przed stopem; stop #2 „ok” ze śladem na urządzeniu, a uwaga autora (D20) wdrożona i przyjęta w rundzie 2. Uwagi:
> - próbne odtworzenie kopii v15 na urządzeniu niezrobione (powód niżej) → lista A;
> - tryb prezentacji bez osobnego testu widżetu — ten sam węzeł co drzewo (test `tree_screen`), sprawdzony zrzutem `20`.

### Stop #2 — 2026-10-17, autor: „ok” (runda 1) i uwaga → D20
- **Ślad na urządzeniu (sprawdzony po odpowiedzi):** krok 3 — aplikacja na drzewie oddalonym do dalszej rodziny; krok 2 — za pierwszym sprawdzeniem bez śladu
  (Marianna dalej „po mężu”, w bazie 12 rodów), po pytaniu `qa` autor go zrobił: Marianna ma ród z kłosami w kolorze rubin, podpis „Ród: Przykladowscy · po
  mężu Wymyslonowie” (13 rodów). Krok 1 nie zostawia śladu — „ok” autora.
- **Uwaga autora przy kroku 2:** kafel kłosów pokazał „też: …” z rodem, który ma kłosy w innym kolorze — *„każdy kolor chciałbym traktować osobno”* →
  [[wieniec]] D20, *Dev report* → *Round 3*.
- Kopie bazy do sprawdzenia (tylko liczba rodów, wzór i kolor) usunięte z katalogu tymczasowego sesji.
- **D20 na emulatorze** (nowy build, `qa`): „Ród” Marianny w rubinie — kłosy bez „też”, „też: …” tylko przy rumianku (ród z rumiankiem w rubinie) (`40`); po
  dotknięciu „Stare złoto” — „też: …” przy kłosach (ród z kłosami w starym złocie) (`41`); wstecz bez zapisu. Zmiana bez nowego wyglądu (ten sam napis, inny
  warunek), więc bez drugiego przeglądu `ui`.
- **Runda 2 — 2026-10-17, autor: „teraz jest dobrze”** (D20 na zrzutach `40`, `41` i na emulatorze).

### `ui` review (subagent, 2026-10-17)
**0 BLOCKER · 1 MAJOR · 4 MINOR — wszystkie poprawione przed stopem** (*Dev report* → *Round 2*).
- **Pięć odstępstw `dev` przyjętych** (*Deviations* 1–5) i pięć, których *Deviations* nie wymienia: wiersz E1 w czytniku jako dwa węzły (słowa i przycisk); okrąg
  w znaku bez wieńca 28 dp przerywany (było 40 dp); linia B5 „Po ślubie wieniec męża: …”; `check` przy „Bez wieńca”, gdy wybrane; wysokość kafla wzoru z treści
  (ok. 100 dp zamiast ≥ 120). Zapis: [[wieniec]] **v1.1** (D18, D19), [[drzewo]] **v1.19**.
- **Zgodne:** kadr wspólny (A2, portret 50% płótna), kolejność elementów osoby 3 → 4 → 4a, wiersz 4b tylko w poprawie, stany E1 z *States*, arkusz E2 (A–Z,
  „po ojcu”, ✎, „Bez wieńca” tylko gdy ma sens), F (12 kolorów, 19 wzorów, pierwsze wolne, F5), drzewo 96 dp z kreską pary w przerwie; akcent tylko na
  działaniach i wyborze; kontrast C3 z [[wieniec]] (najciemniej 80% koloru, obwódka w kolorze tła); wybór niesiony też `check` i stanem „zaznaczone”, nie samym
  kolorem (SC 1.4.1); cel dotyku ≥ 48 dp; ton tekstów; na zrzutach tylko wymyślone osoby.

### Automated
- **Pełny przebieg `flutter test --timeout 120s`: 891 zielonych** (po rundzie 3). `flutter analyze` czyste, `dart format` bez zmian. **Testy strażnika**
  (`grobing-agents`): 164 z 164.
- **Runda 3 (D20):** `clans_test` — `firstFreeColour` i `firstFreeMotif` (nikt nie ma; każdy wzór zajęty → pierwszy wolny w kolorze; każda para zajęta →
  pierwszy); `clan_screen_test` — w brązie żaden kafel nie mówi „też”, w starym złocie „też” przy laurze (ród z laurem w tym kolorze), z powrotem w brązie
  znowu nic. Test widżetu pada na kodzie sprzed D20 („też” przy laurze w brązie).
- **Poprawione pod v15 (14):** wersja 15 i tabela `clans` w `database_test`, `data_state_test`, `data_state_screen_test` (także „Rody” i „Miejsca
  zamieszkania”) i w 10 testach odtworzenia v4…v14 (`restore_service_test`); `residence_screens_test` → „retro 3 R2”: przewinięcie do końca formularza i
  o 6 dp z powrotem — przycisk „Wybierz ród” był ucięty krawędzią przewijania w teście, nie rozmiarem (48 dp).
- **Nowe — warstwa danych:**
  - `test/drift/grobing/migration_test.dart` — **AC-3** v14 → v15 z danymi: każdy wiersz każdej tabeli bez zmian, `clans` pusta, `clan_id` puste, `no_wreath`
    fałsz, potem ród i wybór się zapisują; wygenerowane testy z każdej wersji do v15 też przechodzą;
  - `test/backup/restore_service_test.dart` (2) — **AC-3** kopia **v14** odtwarza się w v15 przez migrację (wszystkie tabele i liczby, rodów brak, wieńców
    brak); kopia **v15** z rodami wraca z tym samym odciskiem i wyborami, a wieńce liczą się jak przed kopią (ojciec → dziecko, pół na pół u żony — **AC-4**);
  - `test/data/wreaths_test.dart` (12) — **B1–B7** każda osobno: rodzic bez płci nie jest ojcem, dziecko w dwóch rodzinach bierze pierwszą; ród u szczytu
    przechodzi na dzieci i wnuki (**AC-1**); wyjątek u syna i „bez wieńca” — on i jego dzieci, ojciec i siostra bez zmian, powrót do ojca czyści (**AC-2**,
    E1a); Ś3 — ostatnie małżeństwo według początku, bez dat po nich, „razem” bez połowy, brakująca połowa wypełnia całość (**AC-4**); dzieci córki po ojcu
    (B6); O1; **pętla w drzewie nie zawiesza**; `heirs` i `countWith` (E1, F5); osoba spoza grafu i ród usunięty — bez wieńca, bez błędu;
  - `test/data/clans_test.dart` (7) — nowy ród z wyborem w jednej transakcji (F6); nazwa pusta i zajęta bez wielkości liter i polskich znaków — nic się nie
    zapisuje (F2); poprawa nazwy, wzoru i koloru dla wszystkich (**AC-6**); wybór, „bez wieńca”, powrót; ojciec → dziecko przez drzewo (**AC-1**, **AC-2**);
    A–Z; nieznany klucz z nowszej kopii.
- **Nowe — ekran** (`test/app/person/clan_screen_test.dart`, 6): E1 „Brak” (O1 i ojciec bez rodu) z „Wybierz ród”; „Nowy ród” — pierwszy wolny kolor i wzór,
  pusta nazwa odrzucona, F5, „Zapisz ród” zapisuje wybór u osoby, a syn ma ród po niej (**AC-1**); arkusz z `check` i „po ojcu”, wyjątek, „Bez wieńca”, powrót
  (**AC-2**); kobieta bez rodu z rodem męża (**AC-4**); ✎ → „Zmiana dotyczy 3 osób.”, nowy kolor u wszystkich (**AC-6**); tekst 200% na 360 dp. W każdym:
  `meetsGuideline` (`androidTapTargetGuideline`, `labeledTapTargetGuideline`) i każdy przycisk z akcją dotknięcia (retro 3, R2).
- **Nowe — widok osoby i drzewo:** `person_screen_test` — wieniec pod portretem, „Ród: … · po mężu …” (**AC-1**, **AC-4**); `tree_screen_test` — miejsce 96 dp
  zamiast 80, wieniec pierwszy w węźle, 88 dp (**AC-5**); `tree_layout_test` — ślad w bok od 43 dp przy osobie z wieńcem, 22 dp bez.
- **Nowe — repo:** `repo_invariants_test` — w bloku danych rodziny jeden wyjątek `!/assets/wreaths/wieniec-*.png`, w `assets/wreaths/` tylko pliki wzorów z
  `WreathMotif`, każdy szary z przezroczystością 640 × 640. Strażnik (14 nowych): szary 640 × 640 przechodzi; kolorowy z przezroczystością, kolorowy, szary bez
  przezroczystości, 512 × 512, nie-PNG pod tą nazwą — odmowa; inna nazwa, inny katalog, vault — odmowa; `.gitignore` w prawdziwym repo ukrywa `wieniec-x.db` i
  wzór w innym katalogu.

### Agent on the emulator
`Grobing_Restore`, build profile v15. Zrzuty `01`–`37` w `C:\Users\user\AppData\Local\Temp\claude\c--Programowanie-Grobing-grobing-agents\3c71c787-79b5-42e3-bf37-7b9aec487ca0\scratchpad\emu044\`.

- **Migracja nad danymi v14 → v15:** liczby w każdej tabeli bez zmian, migawka `pre-update/grobing-v14.db` jest; przerwana migracja zostawiła v14 całe
  (*Dev report*).
- **Stany z [[wieniec]] *States*, 200% na 360 dp, semantyka i cele dotyku, klatki drzewa naprzemiennie z buildem odniesienia** — *Dev report* → *Emulator pass*;
  po rundzie 2 zrzuty `31`–`37`.
- **Próbne odtworzenie kopii v15 na urządzeniu — niezrobione** (jak w [[ISSUE-042-places-of-residence]] i [[ISSUE-043-grave-paid-until]]): hasła testowego kopii
  nie ma, a odtworzenie zastąpiłoby dane, których agent nie stworzył (cmentarz i grób autora na `Grobing_Restore`, dane testowe autora na `Medium_Phone`).
  Ścieżkę pokrywają oba testy odtworzenia wyżej, na prawdziwym formacie kopii z szyfrowaniem → lista A.
- Pozycja bez sieci, więc logcat bez sprawdzania (retro 3, R7 dotyczy pozycji z siecią).

### Family data in the changes
- Bez plików baz, kopii, eksportów i zdjęć w trzech repo. Jedyne obrazy: 19 wzorów `assets/wreaths/wieniec-*.png` — liście i kwiaty z obrazów DALL-E autora,
  szare z przezroczystością, bez osób; strażnik sprawdza nagłówek każdego.
- Nazwiska w kodzie i testach tylko z rdzeni wymyślonych (Wymyśl-, Zmyśl-, Testow-, Przykład-); `clans_test` po poprawce `qa` (dwie nazwy spoza rdzeni).
  Rody na emulatorze — ASCII z tych samych rdzeni, poza repo.
- Zrzuty, build odniesienia, skrypty pomiaru i obrazy źródłowe autora leżą poza repo (katalog tymczasowy sesji, Pobrane). Kopie bazy do liczenia usunięte.
- **Strażnik na sucho na całej paczce** (`echo dry-run: git add -- <lista>` w każdym repo): przeszedł — 55 plików kodu, 8 vaulta, 3 agentów.

### For ISSUE-032 → Hand checks
- **A** — próbne odtworzenie kopii **v15 z rodami** na urządzeniu, z odciskiem zgodnym: na emulatorze niezrobione (hasło testowe nieznane, dane spoza agenta);
  testy odtworzenia v14 → v15 i v15 przeszły;
- **A** — pierwsza aktualizacja ze sklepu nad v14: migracja v14 → v15 i migawka `pre-update/grobing-v14.db` na telefonie (na emulatorze przeszła);
- **B** — wpisane przez `qa` od razu (retro 4, R4): wieńce w trybie prezentacji na telewizorze z kanapy; płynność drzewa z wieńcami na telefonie; TalkBack przy
  wierszu „Wieniec rodu” i arkuszu.

### Package for `docs`
- **`grobing-code` (55):**
  - kod: `.gitignore` · `README.md` · `pubspec.yaml` · `lib/app/data_state_screen.dart` · `lib/app/grave/person_form_screen.dart` · `lib/app/person/clan_screen.dart` ·
    `lib/app/person/person_screen.dart` · `lib/app/theme.dart` · `lib/app/tree/tree_layout.dart` · `lib/app/tree/tree_screen.dart` · `lib/app/widgets/wreath.dart` ·
    `lib/data/clans.dart` · `lib/data/database.dart` · `lib/data/database.g.dart` · `lib/data/database.steps.dart` · `lib/data/family_tree.dart` ·
    `lib/data/person_view.dart` · `lib/data/wreaths.dart` · `lib/dev/fictional_data.dart` · `tool/wreaths/build_wreaths.py`;
  - obrazy (19, każdy po nazwie): `assets/wreaths/wieniec-{bluszcz,brzoza,chaber,chmiel,dab,dzika_roza,jablon,jarzebina,kalina,kasztanowiec,klon,klosy,konwalia,laur,leszczyna,lipa,paproc,rumianek,wrzos}.png`;
  - schemat: `drift_schemas/grobing/drift_schema_v15.json`;
  - testy: `test/app/data_state_screen_test.dart` · `test/app/person/clan_screen_test.dart` · `test/app/person/person_screen_test.dart` ·
    `test/app/person/residence_screens_test.dart` · `test/app/tree/tree_layout_test.dart` · `test/app/tree/tree_screen_test.dart` ·
    `test/backup/restore_service_test.dart` · `test/data/clans_test.dart` · `test/data/data_state_test.dart` · `test/data/database_test.dart` ·
    `test/data/wreaths_test.dart` · `test/drift/grobing/generated/schema.dart` · `test/drift/grobing/generated/schema_v15.dart` ·
    `test/drift/grobing/migration_test.dart` · `test/repo_invariants_test.dart`.
- **`grobing-vault`:** `backlog/issues/ISSUE-044-family-wreaths.md` · `backlog/issues/ISSUE-032-mvp-install.md` · `05_DESIGN/wieniec.md` · `05_DESIGN/osoba.md` ·
  `05_DESIGN/wpis-osoby.md` · `05_DESIGN/drzewo.md` · `05_DESIGN/brand/style-b.md` · `00_START_HERE/TRACEABILITY.md` + zamknięcie `docs` (ADR-021,
  `CURRENT_STATE.md`, `04_ARCHITECTURE/data-model.md`, `04_ARCHITECTURE/backup-format.md`, [[ISSUE-032-mvp-install]] → lista A).
- **`grobing-agents`:** `.claude/hooks/family-data-guard.ps1` · `.claude/hooks/tests/family-data-guard.tests.ps1` · `.claude/rules/family-data.md`.
