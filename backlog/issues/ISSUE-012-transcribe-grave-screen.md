---
title: "ISSUE-012 — Screen: transcribe a grave from the notes (cemetery → grave → persons)"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-002-przepisanie-grobu]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-07
verdict-reviewer: self-check
created: 2026-10-06
updated: 2026-10-07
---

# ISSUE-012 — Ekran przepisania grobu

> Z rozpisania [[US-002-przepisanie-grobu]] (decyzja autora 2026-10-06, po `pm`): ekran po schemacie
> ([[ISSUE-011-schema-v2-assertions]]). To **pierwszy ekran do wpisywania danych**, czyli sygnał dla
> agenta `ui` (`CLAUDE.md` → *Na sygnał*) i warunek obudzenia [[NT-006-visual-guidelines]].

## What to build
1. **Cmentarz:** wybór i dodanie zrobiła [[ISSUE-014-home-map-of-poland]] (mapa, wyszukiwarka, dodanie
   ręczne), a dodanie z bazy robi [[ISSUE-015-add-cemetery-from-database]]. **Tu: „Otwórz cmentarz” w arkuszu
   mapy** ([[cmentarze]] element 7) prowadzi do ekranu cmentarza — przeniesione z ISSUE-014 decyzją autora
   (ISSUE-014 → *Decisions for stop #1* D5, 2026-10-06).
2. **Grób na cmentarzu**, zapisywany bez adresu kwatery, pinezki i zdjęcia. Brak adresu i pinezki widać
   przy grobie ([[US-002-przepisanie-grobu]] AC-5).
3. **Osoby w grobie, jedna po drugiej:** imiona, nazwisko, nazwisko rodowe, „kim była” z jedną linią
   źródła; daty urodzenia, zgonu i pochówku z dopiskiem (dokładnie / około / przed / po / między).
4. **Źródło przy datach i pochówku**, domyślnie „notatki”, status `CLAIMED`. Bez pytania o źródło przy
   każdym polu (decyzja kosztowa z [[FR-001-provenance]]).
5. **Widok grobu:** wszyscy pochowani z datami z dopiskiem.

## Acceptance Criteria
- [ ] US-002 AC-1: grób pokazuje wszystkie wpisane do niego osoby.
- [ ] US-002 AC-2: osoba ma imiona, nazwisko, osobno nazwisko rodowe i „kim była”.
- [ ] US-002 AC-3: data z każdym z pięciu dopisków zapisuje się i wyświetla z dopiskiem.
- [ ] US-002 AC-4: daty i pochówek zapisane z ekranu mają źródło (domyślnie „notatki”) i status
      `CLAIMED`; „kim była” ma jedną linię źródła.
- [ ] US-002 AC-5: grób z samym cmentarzem i osobami się zapisuje, a brak adresu i pinezki jest widoczny.
- [ ] Arkusz cmentarza na mapie ma „Otwórz cmentarz”, który otwiera ekran cmentarza (przeniesione z
      ISSUE-014 AC-4, D5).
- [ ] Ekran stosuje wytyczne stylu B z [[NT-006-visual-guidelines]].
- [ ] Zapis z ekranu zamawia kopię w tle tak samo jak każdy zapis danych ([[ISSUE-010-background-backup]]).
- [ ] **Nazwa grobu** (stop #1, D4): grób można nazwać w widoku grobu; nazwa jest tytułem widoku i karty na
      cmentarzu; bez nazwy widok ma tytuł „Grób”, a karta — osoby.
- [ ] **Migracja v2→v3** (stop #1, D6): aktualizacja zachowuje wszystkie dane, kopia v2 odtwarza się w aplikacji
      v3, a po migracji kopia w tle zamawia się od razu (retro 1, R6).
- [ ] **Poprawa wpisu** (stop #1, D1): literówka poprawiona w formularzu zmienia wartość w miejscu; data z kilkoma
      twierdzeniami jest tylko do odczytu.

## Out of Scope
- Rodzice, małżeństwa, dzieci → [[US-003-przepisanie-rodziny]].
- Drugie, sprzeczne twierdzenie → [[US-004-fakt-od-babci]].
- Zdjęcia nagrobka i osoby → [[US-005-zdjecia]].
- Pinezka i jej poprawa na miejscu → [[EPIC-002-wizyta]] (M6).
- **Poprawianie i usuwanie wpisu:** US-002 ich nie wymienia. `planning` ustala, czy wchodzi minimum
  (poprawa literówki przy przepisywaniu), i mówi to na stopie #1. Bez tego zakres się nie poszerza.

## Input from the author (2026-10-06, po makiecie z [[ISSUE-013-setup-ui-agent]])
Autor ocenił pierwsze specyfikacje `ui` (`05_DESIGN/`) obok obrazów z kick-offu
(`05_DESIGN/brand/references.md`, R1–R4). Uwagi, blisko słów autora:
1. **Ekran główny = mapa Polski od startu**, także pusta, bez cmentarzy. Cmentarz dodaje się z pola
   **„Szukaj osoby lub cmentarza”**: gdy nic nie ma, można dodać nowy — *„lub znaleźć go w bazie cmentarzy,
   żeby potem zaimportować jego mapę?”* (pytanie autora, nowy pomysł). Każdy zapisany cmentarz jest na
   mapie Polski **zniczem**, jak w R1.
2. **Cmentarz jak R2:** po wejściu widać groby (kwatery) zaznaczone zniczami. Po wybraniu znicza arkusz
   pokazuje: miejsce na zdjęcie, lokalizację, ile osób tam leży i **nazwę grobowca**. Przycisk „Pokaż
   grób”.
3. **Grób jak R4:** zdjęcie grobu, nazwa, kto tam leży (zdjęcie, imię i nazwisko, daty urodzenia i
   śmierci), dodawanie zdjęć i nowych osób, wejście w szczegóły osoby.
4. **Formularz osoby** (ramki 5–6 makiety) może zostać jako dodawanie i poprawa osoby, ale brakuje mu:
   **zdjęcia, krótkiej biografii i informacji, z kim osoba jest związana (pokrewieństwo, powinowactwo).**

**Co to dotyka poza tą pozycją:**
- mapy → [[EPIC-002-wizyta]] (M2, M3) i [[SPIKE-001-map-source-offline]] / [[ADR-003-map-source-offline]];
- zdjęcia → [[US-005-zdjecia]];
- relacje → [[US-003-przepisanie-rodziny]];
- szczegóły osoby → M5;
- nazwa grobu → zmiana schematu (`05_DESIGN/grob.md` → *Open* 1);
- „baza cmentarzy z importem mapy” → pomysł spoza backlogu, obok `01_INBOX/2026-10-05-plany-cmentarzy.md`.

**Decyzja autora (2026-10-06, *„ok plan brzmi dobrze”*) — kolejność:**
1. [[ISSUE-014-home-map-of-poland]]: mapa Polski z wbudowanego konturu, znicze cmentarzy, dodanie
   cmentarza. **Przejmuje punkt 1 *What to build* tej pozycji;**
2. **ta pozycja:**
   - cmentarz jak R2, ale bez zdjęcia satelitarnego — arkusz z grobami, z pinezką i bez;
   - **grób jak R4 z nazwą grobu** (opcjonalne pole, czyli zmiana schematu: migracja v2→v3 z testem,
     NFR-003);
   - formularz osoby z biografią — dzisiejsze „kim była” z linią źródła;
3. [[US-005-zdjecia]] — zdjęcia grobu i osoby (formularz i R4);
4. [[US-003-przepisanie-rodziny]] — relacje w formularzu osoby;
5. [[SPIKE-001-map-source-offline]] — zdjęcie satelitarne cmentarza i znicze na grobach.

Groby z notatek nie mają położenia, więc znicze na mapie cmentarza pojawią się dopiero po postawieniu
pinezki. Specyfikacje w `05_DESIGN/` (`cmentarze.md`, `cmentarz.md`, `grob.md`) przebuduje `ui` przed
planem każdej z tych pozycji.

## Technical Notes
- **Tempo przepisywania** to miara ekranu: około 100 osób i 50 grobów całymi wpisami
  ([[NT-002-transcribe-the-notes]], G6). Każde dodatkowe pytanie na osobę mnoży się przez 100.
- **Czytelność w słońcu** ([[NT-006-visual-guidelines]]) do MVP sprawdza się na emulatorze. Słońce to
  wyjątek z `DEFINITION_OF_DONE.md`, sprawdzany na telefonie w buildzie release.
- Folder `05_DESIGN/` (oraz `05_DESIGN/brand/` dla stylu B) powstaje na ten sygnał według `doc-growth.md`,
  z wierszem w DOC_MAP. Zakłada go `docs`, kiedy praca nad ekranem albo NT-006 go potrzebuje.
- Sprawdzić, czy zamówienie kopii przy zapisie (ISSUE-010) obejmuje zapisy z nowego ekranu, a nie tylko
  drogi istniejące w chwili ISSUE-010.
- **Kopia zaraz po migracji v2→v3** (retro 1, R6): po udanej migracji schematu aplikacja zamawia kopię w
  tle od razu, a nie dopiero przy wyjściu albo następnym starcie ([[ISSUE-011-schema-v2-assertions]] →
  *Verification*, uwaga 2).
- Dane do pokazania i testów są wymyślone i istnieją tylko w buildzie debug ([[ISSUE-007-data-layer]]).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-011-schema-v2-assertions]] (twierdzenia w schemacie) | technical | `done` |
| [[NT-006-visual-guidelines]] (wytyczne stylu B) | design | `open` — ten ekran go budzi. Wytyczne v1 powstają w [[ISSUE-013-setup-ui-agent]] |
| agent `ui` w `grobing-agents` | process | [[ISSUE-013-setup-ui-agent]] (`done`). Pierwsze uruchomienie dało specyfikacje i uwagi autora (*Input from the author*) |
| [[ISSUE-014-home-map-of-poland]] (ekran główny, wybór i dodanie cmentarza) | product | `done` (2026-10-06) |
| [[ISSUE-015-add-cemetery-from-database]] (dodanie cmentarza z bazy) | product | `done` (2026-10-07) |
| [[ISSUE-010-background-backup]] (kopia zamawiana przy zapisie) | technical | `done` |
| specyfikacje `ui`: [[cmentarz]] v2 · [[grob]] v2 · [[wpis-osoby]] v2 · [[cmentarze]] element 7 | design | gotowe 2026-10-07 (przed planem) |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC · ręczna weryfikacja na
emulatorze · fakt o rodzinie → źródło i status zapisane · dotyka warstwy danych → próbne odtworzenie z
kopii przechodzi (wpisy z ekranu wracają z odciskiem zgodnym) · zero danych rodziny w zmianach · INVEST
self-check. Po przyjęciu tego ISSUE US-002 idzie do werdyktu US.

## Implementation plan
> `planning`, 2026-10-07. **DoR:** jasny zakres ✅ · powiązana US: [[US-002-przepisanie-grobu]] (AC-1…AC-5) ✅ ·
> krok ścieżki: n/a — M1, warunek kroku 1 UJ-001 ✅ · `task-level` ✅.
> **Ekrany:** specyfikacje `ui` z 2026-10-07 — [[cmentarz]] v2, [[grob]] v2, [[wpis-osoby]] v2, [[cmentarze]]
> element 7; wytyczne [[style-b]] v1.5. Makieta `makieta-cmentarz-grob-osoba.html` (ramki 0–8; ramka 8 to kierunek
> po SPIKE-001, nie ta pozycja) leży w katalogu tymczasowym sesji. Plan idzie za specyfikacjami i nie projektuje
> ekranów od nowa. **Warstwa danych:** zmiana schematu v2→v3 (nazwa grobu) z testem migracji, kopia zaraz po
> migracji (R6), próbne odtworzenie kopii z wpisami z ekranu. **Źródło faktu:** daty i pochówek z twierdzeniem
> „notatki” / `CLAIMED` przez `claims.dart`; „kim była” z jedną linią źródła (`persons.bio_source`).

### Prior art (sources, not memory)
- **drift 2.34.0, źródło w pamięci podręcznej pub** (wersja przypięta, [[ADR-002-flutter-pinned]]), odczyt
  2026-10-07:
  - `Migrator.addColumn(TableInfo table, GeneratedColumn column)` — *„Adds the given column to the specified
    table”* (`lib/src/runtime/query_builder/migration.dart`). Kolumna opcjonalna dochodzi bez przebudowy tabeli i
    bez ruszania wierszy, więc zasada README „krok dodaje, nie usuwa” jest spełniona z definicji;
  - `transaction` — *„Starting from drift version 2.0, nested transactions are supported on most database
    implementations (including `NativeDatabase` …) … When the outermost transaction completes, its changes
    (including changes from child transactions) are written to the database”*
    (`lib/src/runtime/api/connection_user.dart`). `addEventWithClaim` i `addBurialWithClaim` otwierają własne
    transakcje, więc zapis osoby owinięty w jedną zewnętrzną transakcję jest „całością albo niczym” bez zmiany
    `claims.dart`.
- **GEDCOM 7 §2.4, data z modyfikatorem** (`ABT` · `BEF` · `AFT` · `BET … AND`, dokładność od roku do dnia) —
  cytowane w [[ISSUE-011-schema-v2-assertions]] → *Prior art*; ten sam model co `events.qualifier` + rok, miesiąc,
  dzień.
- **Kod `grobing-code`, odczyt 2026-10-07 — skąd luka R6:**
  - `main.dart` → `_open` woła `backup.requestBackgroundIfChanged()` zaraz po utworzeniu bazy;
  - `data_stamp.dart` czyta licznik zmian **z nagłówka pliku, bez otwierania bazy**, a
    `NativeDatabase.createInBackground` otwiera bazę (i migruje) dopiero przy pierwszym zapytaniu;
  - kroki migracji (`customStatement`, `Migrator`) nie zgłaszają zmian w `tableUpdates()`.
  
  Wniosek: dziś start sprawdza znacznik **przed** migracją, a migracja nie zamawia kopii. Kopia zamówi się dopiero
  przy pierwszym zapisie albo wyjściu z aplikacji. To dokładnie przypadek z retro 1 (R6).

### Falsifier — what is measured and what is not
| Pytanie | Wynik |
|---|---|
| Czy dodanie kolumny przejdzie przez weryfikator migracji i odtworzenie starszej kopii? | ✅ z kanonu: `addColumn` nie usuwa tabel ani wierszy. **Zmierzy** test `make-migrations` (v2→v3 i v1→v3) oraz test odtworzenia kopii v2 w aplikacji v3 (`qa`) |
| Czy zapis osoby z datami i pochówkiem da się zrobić „całością albo niczym” na istniejącym `claims.dart`? | ✅ z kanonu drift (zagnieżdżone transakcje). **Zmierzy** test `qa`: błąd w środku zapisu → zero nowych wierszy |
| Czy start zamawia dziś kopię po migracji? | ❌ z kodu (wyżej), **nie zmierzone na urządzeniu**. Test `qa` najpierw pokazuje lukę, potem jej zamknięcie (krok 2 `dev`) |
| Który typ klawiatury daje cyfry i kropkę bez przełączania | **nie zmierzone** — `dev` mierzy na emulatorze ([[wpis-osoby]] → *Open* 2) |
| Tempo wpisu jednej osoby (G6) | specyfikacja liczy **8 akcji** na typową osobę. **Nie zmierzone na ekranie** — odczucie autora na stopie #2 (krok 9) |

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego · co ją obali |
|---|---|---|---|
| D1 | **Poprawa wpisu** (⚠️ OPEN z *Out of Scope* tej pozycji i [[wpis-osoby]] → *Open* 1) | **Wchodzi minimum:** dotknięcie osoby w [[grob]] otwiera ten sam formularz w trybie „Poprawa wpisu”. Poprawia się **w miejscu**: imiona, nazwiska, „kim była” i jego źródło, daty z jednym twierdzeniem. Wyczyszczona data znika razem ze swoim jedynym twierdzeniem. **Data z więcej niż jednym twierdzeniem jest tylko do odczytu**, z dopiskiem „Kilka źródeł — tej daty tu nie poprawisz.” Bez przenoszenia osoby do innego grobu i bez usuwania | Przy ok. 100 wpisach literówka jest pewna, a bez poprawy zostaje w niezastąpionych danych. Literówka to błąd tego samego źródła, a nie drugie źródło ([[ADR-006-claimed-value-separate-structures]] rozdziela wartości z **różnych** źródeł), więc poprawa w miejscu nie łamie FR-001. Bez tego biografii nie widać nigdzie poza bazą ([[grob]] D3). Koszt: tryb formularza, dwie funkcje danych, ok. 3 kroki stopu #2. **Obali:** chcesz mniejszej pozycji — wtedy poprawa staje się osobną małą pozycją zaraz po tej, a karta osoby w [[grob]] dostaje linię „kim była” |
| D2 | **Rozmiar pozycji:** trzy ekrany, migracja, okno nazwy, poprawa | **Jedna pozycja, bez podziału.** Szew na wypadek, gdyby `dev` utknął: D1 (poprawa) odcina się jako osobna pozycja | Wartość US-002 istnieje tylko w całości: pusty ekran cmentarza bez formularza nie zapisze grobu, a formularz bez ekranu grobu nie pokaże, co się zapisało. Każda połowa miałaby stop #2 bez przepływu do sprawdzenia. Migracja to jedna kolumna. **Koszt:** dłuższy stop #2 (ok. 9 kroków). **Obali:** wolisz krótsze stopy — wtedy podział: (a) migracja + cmentarz + formularz + grób, (b) poprawa |
| D3 | **Cmentarz „jak R2 bez satelity”** ([[cmentarz]] D1) | **Arkusz grobów na cały ekran, bez pola mapy.** Po [[SPIKE-001-map-source-offline]] i pinezkach (M6) mapa stanie nad listą, a lista stanie się arkuszem jak w R2 (makieta, ramka 8) | Groby z notatek nie mają pinezek, a ta pozycja nie daje sposobu ich postawienia. Pole mapy byłoby zawsze puste. **Obali:** chcesz już teraz widzieć miejsce na mapę |
| D4 | **Gdzie wpisuje się nazwę grobu** ([[grob]] D1, D2) | **Okno z ikonki ✎ w widoku grobu**, opcjonalnie. Bez nazwy tytułem jest „Grób”, a karta na cmentarzu pokazuje osoby. Nazwy nie wyliczamy z nazwisk | Formularz osoby to ok. 100 wpisów: pole nazwy kosztowałoby przy każdym nowym grobie i mieszało grób z osobą. Zła odmiana („Nowaków”, „Kowalskich”) na grobie rodziny razi. Zaraz po zapisie pierwszej osoby widok grobu jest na ekranie, więc nazwa to 2 dotknięcia. **Obali:** nazywasz prawie każdy grób i okno spowalnia — wtedy pole w trybie „nowy grób” |
| D5 | **Biografia** ([[wpis-osoby]] v2) | **„Kim była” = krótka biografia:** podpowiedź „Krótka biografia — np. zawód, miejsce, co warto zapamiętać”, pole na 3 linie od startu. Jedna linia źródła, domyślnie „notatki” | Twoja decyzja z 2026-10-06. Zdjęcie ([[US-005-zdjecia]]) i relacje ([[US-003-przepisanie-rodziny]]) mają już wskazane miejsce w formularzu, więc kolejne pozycje go nie przestawią. **Obali:** chcesz osobnych pól (zawód, miejsce) — wtedy osobna pozycja ze zmianą schematu |
| D6 | **Kopia zaraz po migracji** (R6, *Technical Notes*) | **Start sprawdza znacznik danych dopiero po otwarciu bazy**, czyli po migracji, bez czekania na nią z pierwszym ekranem. Migracja zmienia plik, więc znacznik różni się od ostatniej kopii i kopia w tle zamawia się od razu. Bez osobnej flagi „była migracja” | Jeden mechanizm dla migracji i dla każdej zmiany spoza `drift`, którą start i tak miał łapać (ISSUE-010, D2). Kopia biegnie dalej według zasad ISSUE-010 (cisza 10 min, najpóźniej godzina). **Obali:** test pokaże, że start bez migracji też zamawia kopię — wtedy znacznik łapie coś przy samym otwarciu i potrzebna jest flaga |

**Stop #1 — zatwierdzony przez autora 2026-10-07** (*„Wygląda dobrze … D1-9 ok”*): D1–D6 według rekomendacji,
kroki stopu #2 bez zmian. Nowe AC dopisane do *Acceptance Criteria*. Pytania autora przy stopie — żadne nie
zmienia zakresu:
1. **Siatka kwater do dotknięcia przy dodawaniu grobu** (*„jeżeli to temat na kolejny issue, to możemy teraz
   odpuścić”*). **Poza tą pozycją.** Notatki nie mają adresów kwater (decyzja autora przy US-002), więc siatka
   pomoże dopiero na cmentarzu, a nie przy biurku. Do tego potrzebny jest plan cmentarza z kwaterami, a ten jest w
   [[SPIKE-001-map-source-offline]] krok 1 (ile z 10 cmentarzy ma plan) i w `01_INBOX/2026-10-05-plany-cmentarzy.md`.
   Pomysł „kliknij kwaterę na planie, żeby wiedzieć, która to” dopisuje tam `docs` przy zamknięciu.
2. **Gdzie łączyć osoby (kto kim dla kogo)** → [[US-003-przepisanie-rodziny]], dwie pozycje po tej. Miejsce w
   formularzu osoby jest wskazane ([[wpis-osoby]] → *Decisions* → „Zdjęcie i relacje później”: sekcja „Rodzina” pod
   biografią). Czy relacje wpisuje się z formularza osoby, z formularza całej rodziny (US-003 AC-1, *family group
   sheet* z briefu), czy obiema drogami, rozstrzyga `ui` z autorem przed planem US-003.
3. **Zdjęcia: makieta wygląda inaczej niż R4.** Zdjęcia to [[US-005-zdjecia]], następna pozycja po tej. W
   ISSUE-012 ich miejsca **celowo nie są zarysowane** ([[style-b]] reguła 11: bez zastępczych obrazków). Po US-005
   widok grobu wraca do R4: zdjęcie nagrobka nad tytułem, portret z lewej w karcie osoby, „Dodaj zdjęcie” obok
   „Dodaj osobę”, portret na górze formularza osoby ([[grob]] D4). `ui` pokaże to na makiecie przed planem US-005.

### Scope diff vs the item (accepted at stop #1)
Nowe AC (dopisane do *Acceptance Criteria* po „tak”):
- **+ AC — nazwa grobu** (z *Input from the author*, decyzja 2026-10-06): grób można nazwać w widoku grobu;
  nazwa jest tytułem widoku i karty na cmentarzu; bez nazwy widok ma tytuł „Grób”, a karta — osoby (D4);
- **+ AC — migracja v2→v3**: aktualizacja zachowuje wszystkie dane (groby bez nazwy), kopia v2 odtwarza się w
  aplikacji v3, a **po migracji kopia w tle zamawia się od razu** (R6, D6);
- **+ AC — poprawa wpisu** (tylko przy „tak” dla D1): literówka poprawiona w formularzu zmienia wartość w
  miejscu; data z kilkoma twierdzeniami jest tylko do odczytu;
- **zmiana — „Otwórz cmentarz”**: wstecz z ekranu cmentarza wraca na mapę z otwartym arkuszem tego cmentarza i
  nowymi liczbami ([[cmentarz]] D7);
- **bez zmian w AC-1…AC-5 i pozostałych AC pozycji.** Źródło dat w tym ekranie to zawsze „notatki” (AC-4,
  „domyślnie”): zmiana źródła daty to [[US-004-fakt-od-babci]].

### Steps (dev)
0. **Przed zmianą:** na `Medium_Phone` jest build release v2 z jednym publicznym cmentarzem (ISSUE-015).
   **Nie odinstalowuj aplikacji** — ta baza v2 to dane do sprawdzenia aktualizacji v2→v3 (krok 10).
1. **Schemat v3** — `lib/data/database.dart`:
   - `Graves.name` (`text().nullable()`), komentarz: nazwa nadana przez autora, nie wyliczana z nazwisk;
   - `currentSchemaVersion = 3`; `build_runner`; `dart run drift_dev make-migrations` → `drift_schema_v3.json` i
     wygenerowane testy w `test/drift/grobing/`;
   - `_from2To3`: `m.addColumn(schema.graves, schema.graves.name)`; `migrationSteps(from1To2:, from2To3:)` w tej
     samej transakcji co `user_version`;
   - README `grobing-code` → *Baza danych*: v3 — nazwa grobu.
2. **R6 / D6** — `lib/main.dart` → `_open`: start pyta o kopię **po otwarciu bazy** (np. pierwsze zapytanie,
   które uruchamia migrację), w tle (`unawaited`), więc pierwszy ekran nie czeka. Błąd otwarcia nie zatrzymuje
   startu: pokaże go ekran, jak dziś.
3. **API danych** — nowy `lib/data/graves.dart` (czysty Dart, bez widżetów; zapisy przez API `drift`, więc
   `tableUpdates` zamawia kopię jak przy każdym zapisie):
   - `watchGraves(db, cemeteryId)` → groby w kolejności wpisania: nazwa, adres (kwatera, rząd, miejsce),
     czy ma pinezkę, osoby (imiona + nazwisko) w kolejności pochówków;
   - `watchGrave(db, graveId)` → grób z cmentarzem (nazwa, miejscowość) i osoby w kolejności pochówków; przy
     każdej osobie pierwsze zdarzenie urodzenia, zgonu i pochówku (`firstEvent`) oraz liczba twierdzeń
     każdej daty (do D1);
   - `PersonEntry` (imiona, nazwisko, nazwisko rodowe, „kim była”, źródło „kim była”, trzy daty z dopiskiem);
   - `addPersonToNewGrave(db, cemeteryId, entry)` i `addPersonToGrave(db, graveId, entry)`: jedna zewnętrzna
     transakcja — grób (dla nowego), osoba, pochówek z twierdzeniem, każda wpisana data z twierdzeniem
     („notatki”, `CLAIMED`). `bio_source` = „notatki”, gdy „kim była” jest wpisane bez zmiany źródła; puste
     „kim była” → oba pola puste;
   - `updatePersonEntry(db, personId, entry)` (D1): poprawa w miejscu według D1; data z > 1 twierdzeniem nie
     zmienia się nigdy (także gdy formularz przyśle inną wartość);
   - `setGraveName(db, graveId, String?)`: pusta albo z samych spacji → brak nazwy.
4. **Daty** — nowy `lib/app/dates.dart` (czysty Dart):
   - parser pola daty: `rrrr` · `mm.rrrr` · `dd.mm.rrrr`, separatory `.` `-` `/`, rok 1500…bieżący, dzień zgodny
     z miesiącem; „między”: druga data późniejsza od pierwszej;
   - formaty z [[style-b]] reguła 6 i [[grob]] element 5: podgląd („→ ok. 1890”, „→ między 1893 a 1895”), lata
     życia (`1921–1987`, `ok. 1890 – 14.03.1951`), `ur. …`, `zm. …`, „bez dat”, `· poch. …`.
5. **Ekran cmentarza** — nowy `lib/app/grave/cemetery_screen.dart` według [[cmentarz]] v2 (elementy 1–4, stany).
6. **Formularz osoby** — nowy `lib/app/grave/person_form_screen.dart` (+ blok daty w osobnym pliku, jeśli
   rośnie) według [[wpis-osoby]] v2:
   - tryby „nowy grób”, „kolejna osoba”, „poprawa” (D1); podtytuł według elementu 1;
   - fokus i klawiatura od razu w „Imiona”; nazwisko podpowiedziane i **zaznaczone** w „kolejnej osobie”;
   - `next` z pola do pola, dopisek poza kolejnością `next`, drugie pole przy „między”, podgląd pod datą;
   - „kim była” 3–6 linii z podpowiedzią; linia „Źródło: notatki · Zmień”; stały tekst o źródle dat;
   - „Zapisz” przypięty nad klawiaturą; błędy przy polach z ikoną, fokus na pierwszym błędzie;
   - wstecz z wpisanymi danymi → okno „Odrzucić wpis?” („Wróć do wpisu” w akcencie);
   - zapis → „nowy grób”: [[grob]] **zastępuje** formularz na stosie; „kolejna osoba” i „poprawa”: powrót do
     [[grob]];
   - **zmierz typ klawiatury** daty ([[wpis-osoby]] → *Open* 2), wynik do *Dev report*.
7. **Widok grobu** — nowy `lib/app/grave/grave_screen.dart` według [[grob]] v2: tytuł z ✎, okno „Popraw grób”,
   adres i pinezka, karty osób (chevron i dotknięcie tylko przy D1), „Dodaj osobę”.
8. **Ekran główny** — `home_screen.dart` → `_cemeterySheet`: element 7 „Otwórz cmentarz” (wypełniony, znicz w
   kolorze tła, `CandleIcon`), wypycha ekran cmentarza; arkusz zostaje otwarty pod spodem ([[cmentarz]] D7).
9. **Dane debug** — `lib/dev/fictional_data.dart`: jeden wymyślony grób w partii dostaje nazwę („Grób rodzinny
   Wymyślonych”), drugi zostaje bez, żeby oba stany było widać. Przykłady w kodzie i komentarzach tylko
   wymyślone.
10. **Sprawdzenia:** `dart format`, `flutter analyze`, `flutter test`, APK release. Na `Medium_Phone` — **build
    release v3 wgrany na v2, bez odinstalowania**: `user_version` = 3, publiczny cmentarz z ISSUE-015 jest, kolumna
    `name` pusta. Wynik w *Dev report*.

### Files likely touched
- **Nowe:** `lib/data/graves.dart` · `lib/app/dates.dart` · `lib/app/grave/cemetery_screen.dart` ·
  `lib/app/grave/person_form_screen.dart` (+ ew. `date_field.dart`) · `lib/app/grave/grave_screen.dart` ·
  `drift_schemas/grobing/drift_schema_v3.json` · `test/drift/grobing/generated/schema_v3.dart`.
- **Zmienione:** `lib/data/database.dart` · `database.g.dart` · `database.steps.dart` · `lib/main.dart` ·
  `lib/app/home/home_screen.dart` · `lib/dev/fictional_data.dart` · `test/drift/grobing/generated/schema.dart` ·
  `README.md`.
- **Testy (`qa`):** `test/drift/grobing/migration_test.dart` · `test/data/graves_test.dart` (nowy) ·
  `test/app/dates_test.dart` (nowy) · `test/app/grave/*_test.dart` (nowe) · `test/app/home/home_screen_test.dart` ·
  test startu (R6) · test kopii i odtworzenia z wpisami z ekranu.

### AC → tests (`qa`)
| AC | Test (happy-path) | Ręcznie |
|---|---|---|
| US-002 AC-1 grób z wieloma osobami | dane: dwie osoby do jednego grobu → `watchGrave` pokazuje obie w kolejności wpisania; widżet: „Dodaj grób” → zapis → „Dodaj osobę” → zapis → dwie karty | kroki 2–4 |
| US-002 AC-2 imiona, nazwisko, rodowe, „kim była” | widżet: wypełnienie czterech pól → wiersz `persons` z wartościami; karta „Imiona Nazwisko z d. Rodowe” | kroki 2, 4 |
| US-002 AC-3 pięć dopisków | jednostkowe `dates.dart`: każdy dopisek, trzy dokładności, „między”, błędy (`196`, 31.02, druga data wcześniejsza); widżet: „między” daje drugie pole, podgląd, karta grobu z dopiskiem | krok 4 |
| US-002 AC-4 źródło i status | dane: po zapisie każda data i pochówek mają dokładnie jedno twierdzenie `notes` / `claimed`; `bio_source` = „notatki”, a po „Zmień” — wpisany tekst; puste „kim była” → `bio_source` puste | krok 2 |
| US-002 AC-5 grób bez adresu i pinezki | widżet: grób z samym cmentarzem i osobą → „Bez adresu kwatery · bez pinezki” na karcie cmentarza i w widoku grobu | krok 3 |
| „Otwórz cmentarz” otwiera ekran cmentarza | widżet `home_screen`: arkusz → przycisk → ekran z nazwą cmentarza; wstecz → arkusz otwarty | krok 1, 6 |
| **+ nazwa grobu** (D4) | widżet: ✎ → nazwa → „Zapisz” → tytuł widoku i karty; pusta → „Grób” i osoby w karcie | krok 5 |
| **+ migracja v2→v3, kopia v2 w v3, kopia po migracji** (D6) | migracja: wygenerowane v1→v3 i v2→v3 + test z danymi (każdy wiersz zostaje, `name` puste); odtworzenie: kopia v2 w aplikacji v3 (liczby = manifest); start: plik v2 → po otwarciu **jedno** zamówienie kopii w tle (atrapa), plik bez zmian od kopii → zero | agent: krok 10 `dev` |
| **+ poprawa wpisu** (D1) | dane: poprawa roku zmienia wartość w tym samym wierszu, twierdzenie zostaje; wyczyszczona data znika z twierdzeniem; data z dwoma twierdzeniami (wymyślony spór z danych debug) nie zmienia się; widżet: dopisek „Kilka źródeł…” | krok 7 |
| Zapis z ekranu zamawia kopię w tle | widżet z atrapą: zapis osoby → zamówienie kopii | — |
| Styl B | przegląd `ui` (subagent) ze zrzutów przed stopem #2 | całość |
| DoD: całość albo nic | dane: błąd w środku zapisu (np. zła data przemycona do API) → zero nowych wierszy w `persons`, `graves`, `burials`, `events`, `assertions` | — |
| DoD: odtworzenie z kopii | grób z nazwą i dwiema osobami z ekranu → kopia → odtworzenie → te same wiersze, odcisk zgodny (istniejące atrapy) | — |
| DoD: zero danych rodziny | wszystkie przykłady wymyślone; grep zmian przed commitem | — |

### Manual verification (stop #2) — kroki według miejsca
**Agent przed stopem:** build release v3 na `Medium_Phone` (wgrany na v2, `dumpsys` potwierdza nowy build),
migracja sprawdzona (krok 10 `dev`). **Wpisuj wyłącznie wymyślone osoby** — przykłady niżej.

**Emulator `Medium_Phone`:**
1. Mapa → znicz cmentarza → arkusz → **„Otwórz cmentarz”**. Pusty cmentarz: tekst i „Dodaj grób”.
2. „Dodaj grób” → klawiatura od razu w „Imiona”. Wpisz: **Jan · Wymyślony**, urodzenie „około” **1890**, zgon
   **14.03.1951**, „kim była” dwa krótkie zdania. Czy `next` prowadzi pole po polu i klawiatura sama się zmienia?
   Czy podgląd pod datą pokazuje „→ ok. 1890”? „Zapisz”.
3. **Widok grobu:** „Grób”, „Bez adresu kwatery · bez pinezki”, karta „Jan Wymyślony · ok. 1890 – 14.03.1951”.
4. „Dodaj osobę” → nazwisko podpowiedziane i zaznaczone. Wpisz **Anna**, nazwisko **Wymyślona** (pisanie
   zastępuje podpowiedź), z domu **Zmyślona**, urodzenie „między” **1893** i **1895**, zgon „przed” — najpierw
   **196** (komunikat błędu), potem **1960**. „Zapisz” → dwie karty.
5. **✎** przy tytule → „Grób rodzinny Wymyślonych” → „Zapisz” → nowy tytuł.
6. Wstecz → cmentarz: karta z nazwą, osobami i „Bez adresu kwatery · bez pinezki”, „1 grób · 2 osoby”. Wstecz →
   mapa z otwartym arkuszem i „1 grób · 2 osoby”.
7. *(tylko przy D1)* Cmentarz → grób → karta Jana → „Poprawa wpisu” → zmień rok urodzenia na **1891** → „Zapisz” →
   karta pokazuje nową datę.
8. „Dodaj osobę” → wpisz imię → wstecz → okno „Odrzucić wpis?” → „Wróć do wpisu” → wstecz → „Odrzuć”. Osoby nie
   przybyło.
9. **Odczucie (G6):** czy wpis jednej osoby jest dość szybki na ok. 100 osób? Czy coś przeszkadza?

**Napisz tutaj:** „ok” · „pomiń” · opis błędu przy numerze kroku.

### Out of Scope (this plan)
- Zdjęcie grobu i portrety, „Dodaj zdjęcie” → [[US-005-zdjecia]]. Relacje w formularzu → [[US-003-przepisanie-rodziny]].
- Widok osoby (R4 prawy, M5); pole mapy na ekranie cmentarza, pinezki i ich stawianie, adres kwatery w oknie
  „Popraw grób” → [[SPIKE-001-map-source-offline]], [[EPIC-002-wizyta]].
- Usuwanie osoby albo grobu, przeniesienie osoby do innego grobu → osobna decyzja (brief G7/C5).
- Źródło inne niż „notatki” przy datach, sprzeczne twierdzenia i ich oznaczanie → [[US-004-fakt-od-babci]].
- Nazwa grobu wyliczana z nazwisk (D4). Wyszukiwanie osób (S5). [[NFR-004-czytelnosc-w-sloncu]] ([[cmentarz]] D8).

### For docs at closure
- `04_ARCHITECTURE/data-model.md` → *Grave*: opcjonalna **nazwa grobu** (v3).
- `glossary.md`: termin **nazwa grobu** — tytuł nadany przez autora, nie nazwisko osób.
- [[NFR-003-migracje-schematu]] → *Notes*: druga migracja (v2→v3, `addColumn`) i kopia zamawiana po migracji (R6).
- `07_RETRO`/`CURRENT_STATE` → R6 dowieziona.
- US-002: po zamknięciu tej pozycji wszystkie jej ISSUE są `done`, więc idzie do werdyktu US.
- `01_INBOX/2026-10-05-plany-cmentarzy.md` (albo [[SPIKE-001-map-source-offline]]): pomysł autora ze stopu #1 —
  siatka kwater na planie cmentarza do dotknięcia, żeby wiedzieć, która to kwatera (pytanie 1 wyżej).
- `ui` (przy przeglądzie dla `qa`): [[wpis-osoby]] → *Open* 1 rozstrzygnięte na stopie #1 (D1 — poprawa wchodzi),
  [[grob]] → chevron i dotknięcie karty osoby obowiązują.

### Self-check (planning) — said out loud
1. **Kompletność:** zakres, pliki, AC → testy, kroki ręczne według miejsca, *Out of Scope* ✅.
2. **Spójność:** plan idzie za pozycją, decyzjami autora z 2026-10-06 i specyfikacjami `ui` v2. Nowe AC (nazwa
   grobu, migracja, R6, poprawa) mają źródło i czekają na stop #1, a nie wchodzą po cichu.
3. **Własność:** zapisałem tę sekcję, `status: in-progress`, tabelę *Dependencies* (ISSUE-014 `done`, dopisane
   ISSUE-015 i specyfikacje) i swoje kolumny macierzy. Specyfikacji `ui` nie ruszałem.
4. **Warstwa danych:** migracja z testem (v1→v3, v2→v3, z danymi) ✅ · odtworzenie kopii v2 w v3 i kopii z wpisami
   z ekranu ✅ · źródło i status dat i pochówku, linia źródła „kim była” ✅ · kopia po migracji (R6) ✅.
5. **Wystarczalność — czego plan nie ma:**
   - **tempa nikt nie zmierzył na ekranie** — specyfikacja liczy 8 akcji, a odczucie autora (krok 9) jest jedyną
     miarą przed prawdziwym przepisywaniem;
   - **brak usuwania:** grób założony na złym cmentarzu albo osoba w złym grobie zostają do osobnej decyzji (G7).
     Przy prawdziwym przepisywaniu to się zdarzy; dziś ratuje to tylko poprawa nazw (D1);
   - pierwsze prawdziwe dane wejdą dopiero z MVP na telefonie, więc ta pozycja nie wymaga jeszcze notki
     przekazania ([[NT-007-hand-over-note]]).

## Dev report
> `dev`, 2026-10-07. Flutter 3.41.1 (przypięty) ✅. Kroki planu 0–10 zrobione. Odstępstwa niżej, każde z
> powodem. Testów `dev` nie pisał.

### What was built
- **Schemat v3** (`lib/data/database.dart`): `graves.name` (opcjonalna), `currentSchemaVersion = 3`,
  `_from2To3` = `addColumn` w tej samej transakcji co `user_version`. `make-migrations` dało
  `drift_schemas/grobing/drift_schema_v3.json` i `test/drift/grobing/generated/schema_v3.dart` (pliki narzędzia).
  README → *Baza danych*: v3, start po otwarciu bazy, zapis osoby jako jedna transakcja.
- **R6 / D6:** `BackupService.requestBackgroundOnStart()` — najpierw `SELECT 1` (otwarcie bazy = migracje),
  potem `requestBackgroundIfChanged()`. Błąd otwarcia → nic nie zamawia. `main.dart` woła ją w tle.
- **API danych** `lib/data/graves.dart`: `PartialDate`, `QualifiedDate`, `PersonEntry`; odczyty
  `watchCemeteryGraves` / `watchGrave` (i `load…`); zapisy `addPersonToNewGrave`, `addPersonToGrave`,
  `updatePersonEntry` (D1), `setGraveName`. Liczba twierdzeń daty = suma po wszystkich zdarzeniach tego typu
  osoby; > 1 → data tylko do odczytu, także w API.
- **Daty** `lib/app/dates.dart`: parser (`rrrr` · `mm.rrrr` · `dd.mm.rrrr`, separatory `.` `-` `/`, rok
  1500…bieżący, dzień zgodny z miesiącem), `isLater`, formaty z reguły 6, `lifeLine`.
- **Teksty** w `lib/app/polish.dart`: `personName` („z d.”), `graveAddress`, `addressLine`.
- **Ekrany** `lib/app/grave/`: `cemetery_screen.dart` (+ `NamesText` z „i jeszcze N”, mierzone),
  `grave_screen.dart` (+ `GraveNameDialog`), `person_form_screen.dart` (tryby `NewGrave`, `NextPerson`,
  `Correction`).
- **Ekran główny:** „Otwórz cmentarz” (element 7) z ikoną znicza w kolorze tła; arkusz zostaje pod spodem.
- **Dane debug:** jeden grób w partii ma nazwę „Grób rodzinny Wymyślonych”.

### Checks (dev, host Windows + emulator `Medium_Phone_API_36.1`)
- `dart format` ✅ · `flutter analyze` czyste ✅ · APK release zbudowany, `aapt dump permissions` **bez
  `INTERNET`** ✅ (rozmiar APK z wszystkimi ABI: 56,3 MB, jak przed zmianą).
- `flutter test`: **303 ✅, 4 ❌ — wszystkie przez podbicie schematu** (testy mają wpisaną wersję 2):
  `test/data/database_test.dart:46`, `test/data/data_state_test.dart:34`,
  `test/app/data_state_screen_test.dart:80` (tekst „2” na „Stanie danych”),
  `test/backup/restore_service_test.dart:969` (kopia v1 po odtworzeniu ma teraz `user_version` 3).
- **Migracja na urządzeniu (v1→v2→v3, build debug na debug, bez odinstalowania):** `user_version` 1 → 3,
  `integrity_check` ok, każda tabela z tą samą liczbą wierszy, `persons` identyczne wiersz w wiersz,
  7 twierdzeń „przeniesione z v1”, `graves.name` puste.
- **Kopia po starcie:** zaraz po starcie v3 w `dumpsys jobscheduler` jest zadanie WorkManagera z ciszą ok.
  10 min. **Granica:** `backup.json` na tym emulatorze pochodzi sprzed ISSUE-010 i nie ma znacznika danych,
  więc start zamówiłby kopię i bez migracji. Rozstrzyga test `qa` na hoście (plik v2 → jedno zamówienie,
  plik bez zmian → zero).
- **Przepływ na emulatorze (wymyślone osoby):** mapa → arkusz → „Otwórz cmentarz” → „Dodaj grób” → osoba z
  datami → widok grobu → „Dodaj osobę” (nazwisko podpowiedziane i zaznaczone) → „między” 1893–1895 i błąd
  „196” → zapis → ✎ nazwa → poprawa wpisu (otwiera się z wartościami, wstecz bez zmian nie pyta) → „Odrzucić
  wpis?” → „Odrzuć”. W bazie: osób przybyło 2 (odrzucona nie weszła), każda data i każdy pochówek ma
  dokładnie jedno twierdzenie `notes` / `claimed`.
- **Klawiatura daty ([[wpis-osoby]] → *Open* 2): `TextInputType.datetime`** — Gboard pokazuje klawiaturę
  numeryczną z `.`, `-`, `/` i klawiszem „dalej”. Bez przełączania. `numberWithOptions` niepotrzebne (przy
  polskim układzie dałoby przecinek).

### Deviations from the plan
1. **Krok 0 i 10 — emulator wrócił ze starego snapshotu** (pułapka znana z ISSUE-009/010): zamiast buildu release
   v2 z publicznym cmentarzem z ISSUE-015 był build **debug z 2026-10-06 08:21, baza v1**. Release na debug się
   nie zainstaluje (inny podpis), więc migrację sprawdziłem buildem debug v3 na debug v1 — łańcuch v1→v2→v3 zamiast
   samego v2→v3. Sam krok v2→v3 sprawdzają wygenerowane testy na hoście.
2. **Błąd znaleziony na emulatorze — formularz w `SingleChildScrollView`, nie w `ListView`.** `ListView`
   buduje tylko widoczne pola, więc `next` z „Pochówku” przeskakiwał niezbudowane „Kim była” i lądował na
   „Zapisz” (przy `adb` Enter nacisnął przycisk i zapisał osobę bez biografii). Teraz wszystkie pola są w
   kolejności `next`. **Dla `qa`:** test kolejności `next` od „Imiona” do „Kim była”.
3. **Błąd znaleziony na emulatorze — menu dopisku chowa klawiaturę przy otwarciu.** Menu nie omija klawiatury,
   która zasłaniała dolne pozycje („między” było prawie niewidoczne). Po wyborze fokus wraca do pola daty, a z
   nim klawiatura. Koszt: klawiatura mignie przy każdej zmianie dopisku.
4. **Teksty spoza specyfikacji** (do przeglądu `ui`):
   - „między” z jedną datą: „Podaj drugą datę.” albo „Podaj pierwszą datę.”;
   - podpowiedzi pola daty: „rok albo dd.mm.rrrr”, a przy „między” — „od” i „do”;
   - nieudany zapis formularza: `error_outline` + „Nie udało się zapisać. Spróbuj jeszcze raz.” nad „Zapisz” (stan
     nieopisany w specyfikacji, wzór z okna cmentarza).
5. **Element 10** („Daty i miejsce pochówku zapiszą się…”) stoi na końcu przewijanej treści, nad „Zapisz”, a nie
   przypięty z przyciskiem — żeby pas nad klawiaturą był najniższy.
6. **Fokus od razu w „Imiona” także w poprawie** (specyfikacja mówi o fokusie po wejściu bez wyróżnienia trybu).
7. **Błąd „Podaj imiona albo nazwisko.”** stoi tylko pod „Imiona”.
8. **„Dodaj osobę”** jest przyciskiem z obrysem w rzędzie wyrównanym do lewej (R4), nie na pełną szerokość.
9. **Wyzwalacz startowy w `BackupService`** (`requestBackgroundOnStart`), a nie w `main.dart`, żeby `qa` mógł go
   przetestować z atrapą.
10. **Data tylko do odczytu w poprawie** nie była widoczna na urządzeniu: stara baza v1 nie ma sporu źródeł.
    Pokrywa ją test (dane debug v3 mają spór o urodzenie ojca).

### For qa
- Testy do poprawy przez podbicie schematu: 4 pliki wyżej. Grupa „simple database migrations” sama obejmuje
  teraz v1→v3 i v2→v3.
- Punkty zaczepienia: `CemeteryScreen(database, cemeteryId)`, `GraveScreen(database, graveId)`,
  `PersonFormScreen(database, mode)`, `GraveNameDialog(name, save)`, `NamesText`,
  `BackupService.requestBackgroundOnStart()`; funkcje danych w `lib/data/graves.dart` i `lib/app/dates.dart`.
- **Stan emulatora:** `Medium_Phone` ma build **debug** v3 z danymi wymyślonymi i wpisami z mojego przejścia
  („Cmentarz Wymyślony 1”, grób „Grob rodzinny Wymyslonych” z Janem i Anną). Na stop #2 w buildzie release
  trzeba odinstalować debug (dane wymyślone przepadną) i zainstalować release. **Wtedy na mapie nie ma
  cmentarza:** krok 1 stopu #2 potrzebuje kroku 0 — dodać publiczny cmentarz z bazy (np. „powazki”).
- Kroki ręczne: plan → *Manual verification (stop #2)*, z krokiem 0 wyżej.

### Fixes after the ui review (dev, 2026-10-07)
Przegląd `ui` (niżej, *Verification*) dał 0 BLOCKER, 0 MAJOR, 5 MINOR. Wszystkie poprawione przed stopem #2:
1. **Poprawa wpisu, element 10:** w poprawie tekst „Poprawa nie zmienia źródła dat. Nowa data zapisze się ze źródłem:
   notatki.” (data zachowuje swoje twierdzenie, a grób się nie zmienia, więc poprzedni tekst mówił nieprawdę od US-004).
2. **Poprawa wpisu bez fokusu i klawiatury** od wejścia (odstępstwo 6 → poprawione).
3. **Przycisk dopisku:** rozmiar najmniejszy 116 × 56 dp, rośnie z tekstem, bez ucinania (SC 1.4.4).
4. **Menu dopisku:** wybrana pozycja z ikoną ✓ i stanem „zaznaczone” dla czytnika (SC 1.4.1).
5. **Odstępy 24 dp:** nagłówek grobu → lista; pasek formularza → pierwsze pole.

## Verification
> `qa`, 2026-10-07. `verdict-reviewer: self-check` (krytyk ISSUE-003 jeszcze nie istnieje).

### Automated — `flutter test`: 341 ✅ (było 309) · `flutter analyze`: czyste · `dart format`: ✅
| AC / DoD | Test |
|---|---|
| US-002 AC-1, AC-2, AC-5 | `test/data/graves_test.dart` (nowy grób z pierwszą osobą, druga osoba, brak adresu i pinezki, lista cmentarza z osobami) · `test/app/grave/grave_screens_test.dart` (ekran cmentarza pusty i wypełniony; przepływ „Dodaj grób” → zapis → grób → „Dodaj osobę” → dwie karty; wstecz z grobu do cmentarza) |
| US-002 AC-3 | `test/app/dates_test.dart` (parser: trzy dokładności, separatory, rok przestępny, odrzucane „196”, 31.02 i inne; `isLater`; pięć dopisków; linia lat życia) · widżet: „między” z drugim polem i podglądem, błąd „196” z ikoną |
| US-002 AC-4 | dane: każda data i każdy pochówek mają **dokładnie jedno** twierdzenie `notes`/`claimed`; `bio_source` „notatki” domyślnie, inne po „Zmień”, puste bez biografii · widżet: to samo po przejściu ekranami |
| „Otwórz cmentarz” | `test/app/home/home_screen_test.dart`: arkusz → przycisk ze zniczem → ekran cmentarza; wstecz → arkusz otwarty |
| + nazwa grobu (D4) | dane: nazwa, obcięcie spacji, pusta usuwa · widżet: ✎ → nazwa → tytuł; pusta → „Grób” |
| + migracja v2→v3 (D6) | `test/drift/grobing/migration_test.dart`: wygenerowane v1→v3, v2→v3 + test z danymi (każdy wiersz wartość w wartość, `graves.name` puste) · `test/backup/restore_service_test.dart`: kopia v2 odtworzona w v3 (liczby = v2, groby bez nazwy) |
| + kopia zaraz po migracji (R6) | `test/backup/background_backup_test.dart`: plik v2 z kopią sprzed aktualizacji → **pytanie przed otwarciem bazy: 0 zamówień (luka)**, `requestBackgroundOnStart`: 1; bez migracji i zmian: 0; baza, która się nie otwiera: 0 i bez wyjątku |
| + poprawa wpisu (D1) | dane: rok poprawiony w tym samym wierszu, twierdzenie bez zmian; wyczyszczona data znika ze swoim twierdzeniem; nowa data dostaje twierdzenie; **data z dwoma twierdzeniami nie zmienia się**, cokolwiek przyjdzie · widżet: „Poprawa wpisu” bez fokusu, z wartościami, tekst o źródle dat, data tylko do odczytu z dopiskiem, poprawiony rok w grobie |
| kolejność `next` | widżet: 6 × `next` od „Imiona” do „Kim była” (regresja błędu z emulatora) |
| okno „Odrzucić wpis?” | widżet: bez wpisu wstecz bez pytania; z wpisem okno; „Wróć do wpisu” zostaje; „Odrzuć” wychodzi, w bazie nic |
| zapis zamawia kopię w tle | `background_backup_test.dart`: zapis osoby przez API ekranów → zamówienie kopii |
| DoD: całość albo nic | dane: odmowa w środku zapisu → zero nowych wierszy w pięciu tabelach |
| DoD: odtworzenie z kopii | `restore_service_test.dart`: grób z nazwą i dwiema osobami z API ekranów → kopia → odtworzenie → **ten sam odcisk**, nazwa, osoby, dopiski, źródło biografii |
| testy podbite na schemat 3 | `database_test`, `data_state_test`, `data_state_screen_test`, odtworzenie kopii v1 (`schemaTo` = bieżąca) |

**Lekcja z testów (do retro):** zapis albo odczyt bazy w `tester.runAsync` przy podpiętym ekranie ze strumieniem
`drift` wisi bez końca: strumień ponawia zapytanie w strefie fałszywego zegara i trzyma blokadę bazy. W
`grave_screens_test.dart` jest na to `leaveScreen` (ekran zdjęty przed `runAsync`). To drugi przypadek po
„zawieszonym przebiegu testów” z ISSUE-014 → *Do retro*.

### Agent checks on the emulator (`Medium_Phone_API_36.1`)
- **Migracja na urządzeniu:** debug v3 wgrany na debug v1 (stary snapshot, *Dev report* → odstępstwo 1): v1 → 3,
  `integrity_check` ok, liczby wierszy i osoby bez zmian, 7 twierdzeń „przeniesione z v1”.
- **Kopia w tle po migracji, na v3:** „Stan danych” pokazał „Ostatnia udana kopia 2026-10-07 12:09 (w tle)” — kopia
  w tle (konfiguracja testowa z ISSUE-010, dane wymyślone) wykonała się po aktualizacji i po zapisach z nowych
  ekranów.
- **Przejście ekranów** (zrzuty w katalogu tymczasowym sesji, wymyślone osoby): wszystkie stany ze specyfikacji, w
  tym pusty cmentarz, data tylko do odczytu w poprawie (spór z danych debug), okno nazwy, okno odrzucenia.
- **Build release na stop #2:** debug odinstalowany (dane wymyślone), release zainstalowany 12:44, a po poprawkach z
  przeglądu wgrany na niego 12:55 (dane zostały). Krok 0: publiczny cmentarz z bazy (Cmentarz Powązkowski,
  Warszawa), zrobiony przez agenta. `aapt`: bez `INTERNET`.

### ui review (subagent bez historii, ze zrzutów emulatora)
**0 BLOCKER · 0 MAJOR · 5 MINOR** — wszystkie poprawione (*Fixes after the ui review*). Odstępstwa `dev` 1–5 i 7–10
przyjęte, 6 poprawione. Sprawdzone i zgodne: elementy i kolejność trzech ekranów i okien, stany, role kolorów (jeden
wypełniony przycisk, na grobie żaden; znicz tylko na „Otwórz cmentarz”), kontrast z `theme.dart` (najniższy: tekst na
zaznaczeniu 4,60:1 — nowa para w [[style-b]] v1.6), cele dotyku ≥ 48 dp, kolor nigdy sam, formaty (reguła 6), ton
(reguła 7), na zrzutach tylko wymyślone osoby. Specyfikacje po przeglądzie: [[wpis-osoby]] v2.1, [[grob]] v2.1,
[[cmentarz]] v2.1, [[style-b]] v1.6.

### DoD lines specific to Grobing
- **fakt o rodzinie → źródło i status:** ✅ testy AC-4 (dane i ekran).
- **zmiana schematu → test migracji z poprzedniej wersji:** ✅ v2→v3 z danymi + v1→v3; na urządzeniu v1→v3.
- **warstwa danych → próbne odtworzenie z kopii:** ✅ kopia z wpisami z ekranów odtwarza się z tym samym odciskiem;
  kopia v2 odtwarza się w v3.
- **zero danych rodziny w zmianach:** ✅ w zmianach brak baz, kopii, eksportów, zdjęć i logów; wszystkie osoby i
  miejsca wymyślone albo publiczne (Powązki z bazy OSM, „Nowaków” z R4 jako podpowiedź). `family_data_dir` w tej
  sesji nieczytany.
- **kopia w tle przy zapisie z nowych ekranów:** ✅ test + kopia „(w tle)” na emulatorze.

### Manual (stop #2) — autor, 2026-10-07, emulator `Medium_Phone` (build release)
**„a cała reszta ok”** — kroki 1–9. Agent sprawdził stan urządzenia po odpowiedzi: na Cmentarzu Powązkowskim jest
grób z nazwą nadaną przez autora i dwiema osobami („1 grób · 2 osoby”), więc kroki zostały wykonane.

**Uwaga autora (krok 9): *„pochówek jest informacją zbędną (imo to jest to samo co zgon)”*.** → **D7 (decyzja autora
na stopie #2): formularz bez pola „Pochówek”.**
- Każde pole mnoży się przez ok. 100 wpisów: tempo 7 akcji zamiast 8. **Czy notatki podają daty pochówku —
  niesprawdzone** (to założenie agenta, nie słowa autora; przegląd US). *Obali:* pierwszy wpis z datą pochówku przy
  przepisywaniu ([[NT-002-transcribe-the-notes]]) — wtedy pole wraca, bo inaczej data trafi do „kim była”, bez
  dopisku i bez twierdzenia.
- **Model danych bez zmian.** W genealogii data pochówku to osobne zdarzenie, nie to samo co zgon (GEDCOM `BURI` obok
  `DEAT`; dla starszych grobów księga pochowanych w parafii bywa jedyną datą). Pole może więc wrócić bez migracji, np.
  ze źródłem innym niż notatki ([[US-004-fakt-od-babci]]).
- Poprawa wpisu nie rusza daty pochówku, którą osoba już ma (test widżetu). Grób dalej pokazuje „· poch. …”, gdy data
  przyszła z innych danych.
- **Skutek dla AC:** US-002 AC-3 dotyczy teraz z tego ekranu dat urodzenia i zgonu; data pochówku zostaje w modelu
  i w FR-004. Zmianę w US zapisuje `docs` przy zamknięciu.
- Zmiana sprawdzona przez agenta (zakres zgodny z prośbą autora, bez nowego kroku dla autora): `flutter test` 341 ✅,
  release wgrany na emulator — formularz bez „Pochówku”, mieści się na jednym ekranie. Specyfikacja: [[wpis-osoby]]
  v2.2.

### Verdict
**APPROVED (self-check, z uwagami).** Każde AC pozycji (z nowymi: nazwa grobu, migracja i kopia po migracji, poprawa
wpisu) ma test happy-path i zostało przejrzane na emulatorze. Linie DoD specyficzne dla Grobing są spełnione. Uwagi:
- R6 na urządzeniu nie rozróżnia „przed i po poprawce” (stare ustawienia kopii bez znacznika). Rozróżnia to test na
  hoście, który pokazuje lukę i jej zamknięcie;
- krok v2→v3 sprawdzony tylko na hoście, a na urządzeniu łańcuch v1→v3 (stary snapshot emulatora);
- tempa przepisywania nikt jeszcze nie zmierzył na prawdziwych notatkach. Odczucie autora: ok.

Po przyjęciu tej pozycji **wszystkie ISSUE z [[US-002-przepisanie-grobu]] są zamknięte**, więc US-002 idzie do werdyktu
US (`docs`).

### Package for docs (one commit per repo, explicit list)
**`grobing-code`** — wszystko zapisała ta pozycja (`dev`, `qa`, `make-migrations`):
`README.md` · `lib/main.dart` · `lib/app/dates.dart` · `lib/app/polish.dart` · `lib/app/home/home_screen.dart` ·
`lib/app/grave/cemetery_screen.dart` · `lib/app/grave/grave_screen.dart` · `lib/app/grave/person_form_screen.dart` ·
`lib/backup/backup_service.dart` · `lib/data/database.dart` · `lib/data/database.g.dart` ·
`lib/data/database.steps.dart` · `lib/data/graves.dart` · `lib/dev/fictional_data.dart` ·
`drift_schemas/grobing/drift_schema_v3.json` · `test/app/dates_test.dart` · `test/app/data_state_screen_test.dart` ·
`test/app/grave/grave_screens_test.dart` · `test/app/home/home_screen_test.dart` ·
`test/backup/background_backup_test.dart` · `test/backup/restore_service_test.dart` · `test/data/data_state_test.dart`
· `test/data/database_test.dart` · `test/data/graves_test.dart` · `test/drift/grobing/generated/schema.dart` ·
`test/drift/grobing/generated/schema_v3.dart` · `test/drift/grobing/migration_test.dart`.
Poza listą: `build/`, raporty `flutter_*.log` (żadnego teraz nie ma).

**`grobing-vault`** — pliki tej pozycji: `backlog/issues/ISSUE-012-transcribe-grave-screen.md` ·
`00_START_HERE/TRACEABILITY.md` · `05_DESIGN/cmentarz.md` · `05_DESIGN/cmentarze.md` · `05_DESIGN/grob.md` ·
`05_DESIGN/wpis-osoby.md` · `05_DESIGN/brand/style-b.md`, plus pliki zamknięcia `docs`.

**`grobing-agents`** — bez zmian.

**Kontrola danych rodziny przed `git add` (`qa`):** w zmianach brak baz, kopii, eksportów, zdjęć i logów; osoby i
miejsca wymyślone albo publiczne. Zrzuty i bazy z emulatora leżą w katalogu tymczasowym sesji, poza repo.

### Notes (do not block)
- Dane debug z ISSUE-007: wszyscy wymyśleni mają nazwisko „Wymyślona”, także „Ojciec”. Na ekranach wygląda to jak
  błąd odmiany, ale to dane testowe, nie usterka ekranu (przegląd `ui`).
- `flutter test` padł raz na zablokowanym `sqlite3.dll` po zawieszonym przebiegu. Wtedy zapisuje `flutter_01.log` w
  korzeniu `grobing-code` — usunięty, nie wchodzi do paczki.
