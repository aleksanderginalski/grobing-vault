---
title: "ISSUE-007 — Data layer: SQLite package (ADR-005), schema v1, \"Stan danych\" screen"
type: issue
status: in-progress
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-001-kopia-z-odtworzeniem]]"
ideal_days: 1
quality-verdict: APPROVED
verdict-date: 2026-10-05
verdict-reviewer: self-check
created: 2026-10-05
updated: 2026-10-05
---

# ISSUE-007 — Warstwa danych

> Z rozpisania [[EPIC-001-zabezpiecz-i-przepisz]] (decyzja autora 2026-10-05, po `pm`): **najpierw baza,
> potem kopia.** Każdy punkt mechanizmu z [[ADR-004-backup-format-encryption-destination]] korzysta z
> funkcji SQLite (`VACUUM INTO`, `user_version`, `integrity_check`, migracje przy odtworzeniu), a w
> `grobing-code` nie ma dziś żadnej bazy. Wybór paczki SQLite był poza zakresem
> [[SPIKE-003-backup-and-restore]] (*Out of scope*).

## What to build
1. **ADR-005: wybór paczki SQLite** (≥ 3 opcje, źródła zamiast pamięci). Kandydaci do porównania, nie
   rozstrzygnięcie: `drift` · `sqflite` · `sqlite3` z `sqlite3_flutter_libs`. Brief wymienia
   „SQLite (np. `drift`)" jako przykład, nie decyzję (§Stack).
2. **Schemat v1** według `04_ARCHITECTURE/data-model.md`, z `PRAGMA user_version` = 1.
3. **Ekran „Stan danych"**, który da się kliknąć: wersja schematu, liczba rekordów w każdej tabeli i
   **odcisk danych** (SHA-256 treści tabel i zdjęć). To miara z [[NFR-002-odtworzenie-na-nowym-telefonie]]
   → *Method*, potrzebna w [[ISSUE-008-backup-write]] i [[ISSUE-009-restore]]. Wzorzec z
   [[SPIKE-003-backup-and-restore]]: ekran „2c Stan danych" w eksperymencie.

## Acceptance Criteria
- [ ] ADR-005 `accepted` z ≥ 3 opcjami. Przed wyborem zmierzony falsyfikator: `VACUUM INTO` (od SQLite
      3.27.0, [release log](https://www.sqlite.org/releaselog/3_27_0.html)) działa na emulatorze z
      najniższym obsługiwanym API. Aplikacja ma dziś `minSdk` 24, domyślne Fluttera. Jeśli wybrana paczka
      tego nie spełnia, podniesienie `minSdk` jest decyzją zapisaną w ADR, nie skutkiem ubocznym.
- [ ] Przy pierwszym uruchomieniu powstaje baza ze schematem v1: `user_version` = 1,
      `PRAGMA integrity_check` = `ok`.
- [ ] Ekran „Stan danych" pokazuje wersję schematu, liczby rekordów i odcisk. Na tych samych wymyślonych
      danych odcisk jest ten sam przy dwóch odczytach i zmienia się po zmianie jednego rekordu.
- [ ] Schemat v1 jest zapisany jako punkt odniesienia dla testów migracji następnych wersji
      ([[NFR-003-migracje-schematu]]). Przy v1 nie ma z czego migrować; `planning` ustala, jak pokazać,
      że mechanizm migracji jest gotowy.
- [ ] Nowe zależności przejrzane pod [[NFR-005-dane-nie-opuszczaja-telefonu]] (żadnych wysyłających
      danych z telefonu); `no_cloud_sdk_test` przechodzi.

## Out of Scope
- Kopia → [[ISSUE-008-backup-write]]; odtworzenie → [[ISSUE-009-restore]].
- Ekrany wprowadzania danych → [[US-002-przepisanie-grobu]], [[US-003-przepisanie-rodziny]].
- Zdjęcia jako funkcja → [[US-005-zdjecia]]. Tutaj tylko tabela *Media* i katalog na pliki, bo odcisk
  danych musi je obejmować.
- Rozstrzygnięcie ⚠️ OPEN „grób bez adresu" ([[US-002-przepisanie-grobu]]). Schemat v1 nie przesądza go:
  kwatera, rząd, miejsce i pinezka grobu są opcjonalne.

## Technical Notes
- **Lekcja ze SPIKE-003:** `dartage` odpadł, bo wymagał nowszego Darta niż przypięty Flutter 3.41.1
  ([[ADR-002-flutter-pinned]]). Ograniczenie SDK każdej kandydującej paczki sprawdza się **przed**
  porównaniem czegokolwiek innego (`pubspec.yaml` → `sdk: ^3.11.0`).
- ADR-005 porównuje co najmniej: wersję SQLite (systemowa czy dołączona), kontrolę nad
  `user_version`, wsparcie testów migracji, otwarcie bazy z obcego pliku (odtworzenie), licencję,
  zgodność z przypiętym Dartem.
- ⚠️ **Wymyślone dane do pokazania i testów — nigdy w buildzie release.** Na telefon trafi build release
  z prawdziwymi danymi (`DEFINITION_OF_DONE.md`), więc funkcja wgrywająca wymyślone osoby nie może w nim
  istnieć: zmieszałaby się z danymi rodziny. `planning` wybiera mechanizm (np. tylko debug, tylko testy).
- `{code}` nie zawiera dziś warstwy danych: `pubspec.yaml` ma tylko `flutter` i `cupertino_icons`.

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-002-bootstrap-code-repo]] | technical | `done` |
| `04_ARCHITECTURE/data-model.md` | technical | przyjęty w kick-offie |
| [[ADR-002-flutter-pinned]] | technical | `accepted` |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC · ręczna weryfikacja na
emulatorze · próbne odtworzenie z kopii — **n/a do czasu [[ISSUE-008-backup-write]]**, bo kopii jeszcze nie
ma (`planning` potwierdza to w planie) · zero danych rodziny w zmianach · INVEST self-check.

## Implementation plan
> `planning`, 2026-10-05. **DoR:** jasny zakres ✅ · powiązana US: [[US-001-kopia-z-odtworzeniem]] ✅ ·
> krok ścieżki: n/a, poza ścieżką (M8), tak jak wiersz w `TRACEABILITY.md` ✅ · `task-level` ✅.
> **Warstwa danych:** test migracji — przy v1 nie ma poprzedniej wersji, więc zamiast niego zapisany
> schemat v1 i test zgodności z nim (AC-4) · próbne odtworzenie z kopii — **n/a**, kopia powstaje w
> [[ISSUE-008-backup-write]] · źródło faktu — **n/a**, pozycja nie zapisuje faktów o rodzinie (dane
> wymyślone, tylko w buildzie debug).

### Prior art (sources, not memory)
Pomiar z API pub.dev, 2026-10-05; Dart w przypiętym Flutterze 3.41.1 = **3.11.0**
(`bin/cache/dart-sdk/version`):

| Paczka | Najnowsza | Wymaga | Z przypiętym Flutterem |
|---|---|---|---|
| `drift` / `drift_dev` | 2.35.1 | Dart ≥ 3.10 · zależy od `sqlite3` ^3.4 | ✅ najnowsza |
| `sqlite3` | 3.7.0 | Dart ≥ 3.10 · SQLite **dołączony** przez build hooks ([README](https://pub.dev/packages/sqlite3): *„bundles SQLite with your application"*); od 3.6.0 można wskazać systemowy SQLite per platforma | ✅ najnowsza |
| `sqflite` | 2.4.4+1 | **Dart ^3.12, Flutter ≥ 3.44** | ⚠️ tylko do **2.4.2+1** (`sqflite_android` 2.4.2+3); każda nowsza wersja wymaga odpięcia Fluttera ([[ADR-002-flutter-pinned]]) |
| `sqlite3_flutter_libs` | 0.6.0+**eol** | — | ❌ wycofana |

- `VACUUM INTO` istnieje od SQLite **3.27.0** ([release log](https://www.sqlite.org/releaselog/3_27_0.html)).
  `sqflite` używa SQLite telefonu, więc wynik zależy od wersji Androida. Wersji systemowego SQLite dla
  API 24-29 **nie potwierdziłem w źródle**. Na tej maszynie są tylko obrazy API 36/36.1, więc pomiar na
  API 24 wymagałby pobrania obrazu systemu.
- Migracje w `drift` ([docs](https://drift.simonbinder.eu/migrations/)): `schemaVersion` +
  `MigrationStrategy`; `drift_dev make-migrations` zapisuje schemat każdej wersji i **generuje test
  migracji** (*„Drift will also generate a test file for your migrations"*). To jest metoda z
  [[NFR-003-migracje-schematu]], gotowa w narzędziu.
- Lekcja ze SPIKE-003: `dartage` odpadł na wymaganym Darcie. Tabela wyżej to ten sam test: **`sqflite`
  oblałby go w najnowszej wersji.**

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego · co ją obali |
|---|---|---|---|
| D1 | **Paczka SQLite (ADR-005)** | **`drift` na `sqlite3` z dołączonym SQLite.** `minSdk` zostaje 24 | `VACUUM INTO` nie zależy od wersji Androida, bo SQLite jest w aplikacji. Najnowsze wersje działają z przypiętym Dartem. Narzędzie generuje testy migracji (NFR-003). Brief wskazał `drift` jako przykład. **Koszt:** generowanie kodu (`build_runner`, pliki `*.g.dart`) i większa paczka niż czysty SQL. **Obali ją krok 1:** hooks nie budują się na Flutterze 3.41.1 albo `sqlite_version()` < 3.27 na emulatorze. Wtedy STOP i wracam z opcjami (`sqflite` 2.4.2+1 z decyzją o `minSdk` albo `sqlite3` z systemowym SQLite) |
| D2 | **Zakres schematu v1** | **Cały `data-model.md` oprócz *Assertion*** oraz pól, o których kształcie decyduje coś otwartego: opłata za grób (S4, poza Must) i status mapy offline cmentarza ([[SPIKE-001-map-source-offline]]) | Model nie mówi, **gdzie żyje wartość spornej daty**: w *Event* czy w *Assertion*. „Co twierdzimy" jest w *Assertion*, a data w *Event*, więc wartość miałaby dwa domy. FR-004 wymaga, żeby dwie daty z dwóch źródeł współistniały. Kształt *Assertion* powstanie przy planowaniu [[US-002-przepisanie-grobu]] (AC-4, pierwszy zapis źródła) jako **v2 z pierwszym prawdziwym testem migracji**. Generalizujemy z instancji, nie przed nią. **Obali go:** jeśli *Event* trzeba będzie przebudować pod *Assertion*, robi to migracja v2 na danych wymyślonych, zanim powstaną prawdziwe |
| D3 | **Wymyślone dane do pokazania** | Akcja „Wgraj wymyślone dane" w `lib/dev/`, wywoływana wyłącznie za `kDebugMode`; w buildzie release jej nie ma. Imiona oczywiście syntetyczne (np. „Wymyślona Osoba 7") | `kDebugMode` jest stałą `false` w release, więc kod nie wchodzi do buildu, który trafi na telefon z danymi rodziny. Testy używają bazy w pamięci, nie tej akcji |

### Scope diff vs the item (to accept at stop #1)
- **− *Assertion* w schemacie v1** (D2): AC-2 „schemat v1 według `data-model.md`" węższy o jedną encję i
  dwa pola.
- **+ poprawka znaleziona przy okazji:** `test/repo_invariants_test.dart` sprawdza wpis
  `*.grobing-backup` w `.gitignore`, który [[ISSUE-006-setup-family-data-guard]] usunęło. **`flutter test`
  w `grobing-code` nie przechodzi od ISSUE-006** (zmierzone 2026-10-05: 4 z 5, błąd na `*.grobing-backup`).
  Poprawka: `*.age` i `*.tar` zamiast `*.grobing-backup` (ADR-004).
- **+ akcja z wymyślonymi danymi tylko w debug** (D3). Potrzebna tutaj i w ISSUE-008.

### Schema v1 (from `data-model.md`)
| Tabela | Kluczowe kolumny | Uwagi |
|---|---|---|
| `persons` | imiona · nazwisko · `birth_surname` · „kim była" (tekst) + jedna linia źródła · `is_living` | [[FR-005-nazwisko-rodowe]] |
| `families` · `family_partners` · `family_children` | PK (rodzina, osoba) | „1-2 partnerów" pilnuje kod przy wprowadzaniu (US-003), nie schemat |
| `events` | typ (urodzenie · zgon · pochówek · małżeństwo · koniec) · osoba **albo** rodzina · kwalifikator (dokładnie · około · przed · po · między) · dwie granice daty jako rok + opcjonalny miesiąc i dzień · miejsce | [[FR-004-data-z-dopiskiem]]; rok osobno, bo suwak czasu (M10) liczy w latach |
| `cemeteries` | nazwa · miejscowość · środek (opcjonalny) · link do Grobonetu (opcjonalny) | bez statusu mapy offline (D2) |
| `graves` | cmentarz · `sector` / `row` / `plot` · pozycja + sposób uzyskania + dokładność — **wszystko opcjonalne** | nie przesądza ⚠️ OPEN z US-002 (`data-model.md` → *Known consequence*) |
| `burials` | osoba (unikalna) · grób | [[FR-003-wiele-osob-w-grobie]]: wiele na grób, osoba najwyżej raz |
| `media` | plik w prywatnym magazynie (ścieżka względna) · osoba **albo** grób | pliki w katalogu `media/` obok bazy |
| `settings` | wskazanie „ja" | — |

### Steps (dev)
1. **Falsyfikator D1 (≤ 1 h), przed czymkolwiek innym:** na przypiętym Flutterze dodać `drift`,
   `sqlite3`, `path_provider` oraz dev: `drift_dev`, `build_runner`. Następnie
   `flutter build apk --release`, a na `Medium_Phone`: `select sqlite_version()` ≥ 3.27, `VACUUM INTO` do
   pliku tymczasowego, `integrity_check` kopii = `ok`, `PRAGMA user_version` = `schemaVersion`. Zapisać,
   czy hook pobiera gotowy SQLite z sieci przy budowaniu (wpływa na build offline). **Porażka → STOP.**
2. **ADR-005** (`04_ARCHITECTURE/decisions/`): ≥ 3 opcje z tabeli *Prior art* plus wynik kroku 1;
   `accepted` po zdanym kroku 1 i „tak" na stopie #1.
3. `lib/data/database.dart`: tabele v1 z tabeli wyżej, `schemaVersion = 1`; plik `grobing.db` w
   katalogu wsparcia aplikacji (`path_provider`), zdjęcia w `media/` obok. `build.yaml` dla
   `make-migrations`; wygenerować `drift_schemas/…_v1.json` i scaffold testu migracji.
4. `lib/data/data_state.dart`: liczby rekordów i **odcisk danych** liczone po tabelach z `sqlite_master`
   (tabela dodana w v2 policzy się sama). Odcisk to SHA-256 treści: tabele po nazwie, wiersze po kluczu,
   wartości w stałej serializacji, potem zdjęcia po ścieżce (ścieżka + SHA-256 pliku). Pokazywane 16
   znaków hex, jak w SPIKE-003. **Liczony z treści, nie z pliku bazy**, więc `VACUUM INTO` i odtworzenie
   go nie zmieniają. Na tym opierają się ISSUE-008 i 009.
5. `lib/app/data_state_screen.dart` „Stan danych" (wersja schematu, liczby, odcisk) + wejście z
   `start_screen.dart`. Baza otwierana w `main.dart` i przekazana w dół, bez nowej paczki do zarządzania
   stanem. To ekran techniczny (lista liczb w istniejącym motywie), a nie widok produktu, więc trigger
   agenta `ui` jeszcze nie pada.
6. `lib/dev/fictional_data.dart` (D3) + przycisk widoczny tylko w debug.
7. README `grobing-code`: sekcja „Baza danych": gdzie leży plik, `build_runner` i
   `make-migrations` przy każdej zmianie schematu, pliki `*.g.dart` commitowane razem ze zmianą,
   definicja odcisku jako miary.
8. `data-model.md`: jedna datowana linia, że v1 wdrożony bez *Assertion* i dwóch pól (D2), z linkiem tutaj.

### Files likely touched
`grobing-code`: `pubspec.yaml` · `pubspec.lock` · `build.yaml` (nowy) · `lib/main.dart` ·
`lib/app/grobing_app.dart` · `lib/app/start_screen.dart` · `lib/app/data_state_screen.dart` (nowy) ·
`lib/data/database.dart` + `database.g.dart` (nowe) · `lib/data/data_state.dart` (nowy) ·
`lib/dev/fictional_data.dart` (nowy) · `drift_schemas/` (nowy) · `README.md` · testy (`qa`).
`grobing-vault`: `ADR-005-…` (nowy) · `data-model.md` (linia) · ta pozycja · `TRACEABILITY.md`.

### AC → tests (`qa`)
| AC | Test happy-path | Ręcznie (stop #2) |
|---|---|---|
| AC-1 ADR-005 + falsyfikator | test na hoście: baza v1 z wymyślonymi danymi → `VACUUM INTO` → kopia ma `integrity_check` = `ok`; `sqlite_version()` ≥ 3.27 | wynik kroku 1 z emulatora zapisany w ADR-005 |
| AC-2 baza v1 przy pierwszym starcie | świeża baza: `user_version` = 1, `integrity_check` = `ok`, komplet tabel v1 | ekran „Stan danych" po instalacji: schemat 1, zera |
| AC-3 ekran i odcisk | odcisk ten sam przy dwóch odczytach, inny po zmianie jednego rekordu i **ten sam po `VACUUM INTO`**; widget test ekranu | wgranie wymyślonych danych → liczby i odcisk się zmieniają; restart → ten sam odcisk |
| AC-4 schemat v1 jako punkt odniesienia | wygenerowany test `drift`: schemat tworzony przez aplikację = zapisany `…_v1.json` | — |
| AC-5 zależności | `no_cloud_sdk_test` przechodzi; lista nowych paczek przejrzana w *Verification* | — |
| (poprawka) | `repo_invariants_test` przechodzi z `*.age`/`*.tar` | — |

### Manual verification (stop #2) — kroki według miejsca
- **Terminal VS Code** (`grobing-code`): `flutter run` na emulatorze `Medium_Phone` (debug).
- **Emulator:**
  1. Ekran startowy → „Stan danych": schemat **1**, wszystkie liczby **0**, jest odcisk.
  2. „Wgraj wymyślone dane" → liczby rosną, odcisk inny niż w kroku 1.
  3. Zamknij aplikację całkiem i otwórz ponownie → te same liczby i ten sam odcisk.
- **Terminal VS Code:** `flutter build apk --release`, potem `flutter install`.
- **Emulator (release):** „Stan danych" działa, a przycisku „Wgraj wymyślone dane" **nie ma**.
- **Napisz tutaj:** „ok" · „pomiń" · opis błędu.

### Out of Scope (this plan)
- *Assertion* i każdy zapis źródła → v2 przy [[US-002-przepisanie-grobu]] (D2).
- Ekrany wprowadzania, kopia, odtworzenie (ISSUE-008/009), opłata za grób (S4), status mapy offline.
- Zmiana `minSdk` (tylko gdyby obalił ją krok 1 → STOP) · paczka do zarządzania stanem.

### Self-check (planning) — said out loud
- Nie wiem, czy hook `sqlite3` pobiera SQLite z sieci przy pierwszym budowaniu; krok 1 to zapisze.
- API 24 nie będzie zmierzone, bo nie ma obrazu. Przy dołączonym SQLite to bez znaczenia dla
  `VACUUM INTO`, ale ładowanie biblioteki na Androidzie 7 zostaje niesprawdzone; telefon dostanie dopiero
  MVP w buildzie release.
- Odcisk z kroku 4 staje się kontraktem dla ISSUE-008/009. Zmiana jego definicji później unieważnia
  porównania, dlatego README zapisuje go jako miarę (krok 7).

## Dev report
> `dev`, 2026-10-05. Kod w `grobing-code`, niezacommitowany. `flutter analyze lib` bez uwag.

### Step 1 — falsifier D1: ✅ passed
Program próbny poza repo (scratchpad, `com.grobing.probe.probe007`, potem odinstalowany), build
release na `Medium_Phone` (API 36, x86_64):

| Pomiar | Wynik |
|---|---|
| Build hooks `sqlite3` na Flutterze 3.41.1 | ✅ budują się; `libsqlite3.so` w APK dla `arm64-v8a`, `armeabi-v7a`, `x86_64` (~1,7 MB każda) |
| `select sqlite_version()` | **3.53.4** (dołączony; wymagane ≥ 3.27.0) |
| `VACUUM INTO` → kopia | ✅ plik powstał, `integrity_check` = `ok`, wiersze zgodne |
| `user_version` w kopii | **zachowany** (1). Ważne dla ADR-004 pkt 6 („`user_version` = manifest”) |
| `drift` a `user_version` | `drift` trzyma `schemaVersion` w `PRAGMA user_version` (źródło: `drift-2.34.x/lib/native.dart:85`); w teście dymnym świeża baza ma `user_version` = 1 |
| Skąd hook bierze SQLite | pobiera gotową bibliotekę z wydań `sqlite3.dart` na GitHubie i sprawdza SHA-256 zapisane w paczce (`lib/src/hook/asset_hashes.dart`); potem cache w `.dart_tool/`. **Pierwszy build potrzebuje sieci** |

### Versions — what the pinned SDK allows (new findings for ADR-005)
- **`sqlite3` 3.5.2, nie 3.7.0:** 3.6+ wymaga `hooks` ^2.2, a tego nie da się rozwiązać z przypiętym SDK.
- **`drift` 2.34.0 + `drift_dev` 2.34.0, przypięte parą.** Przypięty Flutter trzyma `analyzer` na 10.x, a
  `drift_dev` 2.34.2+ wymaga `analyzer` ^13. Zakres `drift_dev` 2.34.0 dopuszcza `drift` < 2.35, ale
  **`drift` 2.34.1 i 2.34.4 łamią go**: `schema dump` i weryfikator migracji się nie kompilują
  (`allSchemaEntities`, zmierzone). Komentarz w `pubspec.yaml`, sekcja w README. To ta sama klasa
  ryzyka co `dartage`: przypięty SDK ogranicza paczki, a zakres wersji w paczce tego nie widzi.

### Smoke check (dev, host Windows, throwaway test in the scratchpad)
Świeża baza: v1, 10 tabel, zera, odcisk `b91fe9928cef859e`. Po wymyślonych danych odcisk się zmienia i
jest powtarzalny. Kopia `VACUUM INTO` ma **ten sam odcisk**, `user_version` 1 i `integrity_check` `ok`.
Klucz obcy (pochówek nieistniejącej osoby) i CHECK (zdarzenie z osobą i rodziną naraz) są odrzucane.
**Ten sam odcisk pustej bazy na hoście i na emulatorze** (build release, zrzut ekranu): definicja nie
zależy od platformy.

### Deviations from the plan
- **Krok 2 (ADR-005) i krok 8 (linia w `data-model.md`) → `docs`.** Skill `dev` nie aktualizuje vaulta,
  a tabela własności w `vault-as-sot.md` nie daje `dev` ADR-ów. Treść jest gotowa: *Prior art*, D1 i
  dwie sekcje wyżej.
- `burials.person_id` jest `UNIQUE`, a nie kluczem głównym. Pojedynczy `INTEGER PRIMARY KEY` byłby
  aliasem `rowid` i SQLite wygenerowałby go, gdyby go pominąć.
- „Jeden wiersz” w `settings` przez `CHECK (id = 1)` w `customConstraints` (lint `recursive_getters`).
- Kolejność wierszy na ekranie: czytelna (osoby, rodziny…), a nie alfabetyczna po nazwach tabel.
  Odcisk dalej liczy po nazwach.

### For qa
- **`test/app_start_test.dart` się nie kompiluje:** `GrobingApp` wymaga teraz `database` i `location`
  (`flutter analyze` na całym repo zgłasza 2 błędy wyłącznie tam). Wystarczy baza w pamięci
  (`GrobingDatabase(NativeDatabase.memory())`) i katalog tymczasowy.
- Poprawka `repo_invariants_test`: `*.age`/`*.tar` zamiast `*.grobing-backup` (scope diff).
- `dart run drift_dev make-migrations` wygeneruje scaffold testów w `test/drift/grobing/`. Schemat v1
  już leży w `drift_schemas/grobing/drift_schema_v1.json` i jest identyczny z bieżącym zrzutem
  (sprawdzone `cmp`).
- Kroki stopu #2: sekcja *Manual verification* wyżej, bez zmian. Build debug na `Medium_Phone` wymaga
  najpierw **odinstalowania** `com.grobing.app` (jest tam build release, inny podpis). Na emulatorze
  nie ma prawdziwych danych.
- Obserwacja poza zakresem: na `Medium_Phone` jest zainstalowane `com.grobing.spike003`, choć
  SPIKE-003 → *Cleanup* mówi, że je odinstalowano. Emulator startuje ze snapshotu, więc odinstalowanie
  bez zapisu snapshotu mogło się cofnąć.

## Verification
> `qa`, 2026-10-05. Rytuał WZ-024: `dart format` (0 zmian) → `flutter analyze` (bez uwag, całe repo) →
> `flutter test` **21/21** → kroki ręczne (niżej).

### Automated
| AC | Dowód | Wynik |
|---|---|---|
| AC-1 ADR-005 + falsyfikator | emulator: *Dev report* → *Step 1*. Host: `test/data/database_test.dart` → SQLite ≥ 3.27.0, `VACUUM INTO` daje kopię z `integrity_check` `ok`, `user_version` 1 i kompletem wierszy | ✅ pomiar · ⏳ **plik ADR-005 pisze `docs` przy zamknięciu** (*Dev report* → *Deviations*) |
| AC-2 baza v1 | `database_test.dart`: `user_version` 1, `integrity_check` `ok`, `foreign_keys` 1, **dokładnie 10 tabel v1** (bez *Assertion*, D2). Do tego: grób z samym cmentarzem; wiele pochówków na grób, najwyżej jeden na osobę (FR-003); klucz obcy odrzuca pochówek nieistniejącej osoby; zdarzenie nie należy naraz do osoby i rodziny; data „między 1893 a 1895" zapisana tak, jak wpisana (FR-004) | ✅ |
| AC-3 ekran i odcisk | `test/data/data_state_test.dart`: pusta baza (schemat 1, zera); liczby idą za danymi; odcisk powtarzalny i zmienia się po zmianie jednej wartości oraz po zmianie pliku zdjęcia; **kopia `VACUUM INTO` ma ten sam odcisk**. `test/app/data_state_screen_test.dart`: ekran pokazuje wersję, odcisk i 11 liczb; przycisk debug wgrywa dane i odcisk się zmienia | ✅ |
| AC-4 schemat v1 jako punkt odniesienia | `test/drift/grobing/schema_v1_test.dart`: weryfikator `drift` porównuje schemat z `drift_schemas/grobing/drift_schema_v1.json` z oczekiwaniami kodu, a baza tworzona przez aplikację przechodzi `validateDatabaseSchema`. Plik celowo nie nazywa się `migration_test.dart`, żeby `make-migrations` utworzyło go przy v2 | ✅ |
| AC-5 zależności | `no_cloud_sdk_test` ✅. Nowe paczki runtime: `drift`, `sqlite3` (autor obu: simolus3; natywna biblioteka bez sieci w działaniu, przy budowaniu pobierana z przypiętym SHA-256), `path_provider` (flutter.dev; przechodnio `jni`/`jni_flutter`), `crypto` (dart.dev). Tylko dev: `drift_dev`, `build_runner`. **APK release bez uprawnienia `INTERNET`** (`aapt2 dump permissions`: tylko `DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION`) | ✅ |
| (poprawka) `repo_invariants_test` | `*.age`/`*.tar` zamiast `*.grobing-backup` → 5/5 | ✅ |

### DoD lines specific to Grobing
- **Test migracji:** v1 nie ma poprzedniej wersji, więc pierwszy prawdziwy test migracji przyjdzie z v2
  ([[US-002-przepisanie-grobu]]). Punkt odniesienia v1 jest zapisany i sprawdzany (AC-4).
- **Próbne odtworzenie z kopii:** n/a. Kopia powstaje w [[ISSUE-008-backup-write]] (plan, DoR). Najbliższy
  dowód: kopia `VACUUM INTO` ma ten sam odcisk danych (AC-3).
- **Źródło + status faktu:** n/a. Pozycja nie zapisuje faktów o rodzinie, a dane wymyślone są tylko w debug.
- **Zero danych rodziny w zmianach:** przegląd `git status --untracked-files=all` w trzech repo. Brak baz,
  kopii, eksportów i zdjęć. Imiona w `lib/dev/` i testach są syntetyczne („Wymyślona", „Ojciec 1",
  „Ktoś", „Cmentarz Wymyślony").

### Found by qa → fixed by dev
- **`setState` dostawał `Future`.** `_refresh()` miał postać `setState(() => _state = _read())`, a
  strzałka zwraca wynik przypisania. W buildzie debug odświeżenie i przycisk z wymyślonymi danymi
  kończyły się asercją. W release asercje są wyłączone, dlatego test dymny `dev` tego nie złapał.
  Poprawka: ciało blokowe (`lib/app/data_state_screen.dart`). Złapał to widget test AC-3 i teraz go pilnuje.

### Manual (stop #2)
Build debug na `Medium_Phone` (wcześniejszy build release odinstalowany: inny podpis, na emulatorze nie
ma prawdziwych danych). Kroki 1-4 (pusta baza z odciskiem `b91fe9928cef859e` → wymyślone dane → odświeżenie
→ ponowne uruchomienie): **„ok”**. Autor, 2026-10-05: *„działa”*. Brak przycisku w buildzie release
sprawdził `dev` (zrzut ekranu, *Dev report*); autor tego kroku nie powtarzał.

### Verdict (self-check)
**APPROVED** z uwagami:
- **AC-1 domyka `docs`:** pomiar jest, ale plik ADR-005 i linia w `data-model.md` powstają przy
  zamknięciu (własność vaulta). Bez nich pozycja nie jest `done`.
- `drift` i `drift_dev` są przypięte parą na 2.34.0 przez przypięty Flutter. Każda zmiana SDK
  (ADR-002) musi je ruszyć razem i powtórzyć `schema dump` oraz testy.
- Ładowanie dołączonego SQLite na Androidzie 7-10 nie jest zmierzone (brak obrazu; plan, *Self-check*).

**Czego szukałem i nie znalazłem:**
- danych rodziny w zmianach i prawdziwych imion w danych testowych;
- uprawnienia `INTERNET` i paczek wysyłających dane;
- kodu wymyślonych danych osiągalnego w release (`kDebugMode`, zrzut ekranu);
- rozjazdu `drift_schema_v1.json` ze schematem w kodzie (weryfikator + `cmp`);
- zmiany odcisku po `VACUUM INTO`;
- ścieżki „usuń i stwórz od nowa” w migracji (`onUpgrade` kończy się błędem).
