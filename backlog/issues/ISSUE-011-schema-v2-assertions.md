---
title: "ISSUE-011 — Schema v2: assertions (provenance) and the first real migration v1→v2"
type: issue
status: in-progress
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-002-przepisanie-grobu]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-06
verdict-reviewer: self-check
created: 2026-10-06
updated: 2026-10-06
---

# ISSUE-011 — Schemat v2: twierdzenia

> Z rozpisania [[US-002-przepisanie-grobu]] (decyzja autora 2026-10-06, po `pm`): **najpierw schemat,
> potem ekran**, tak jak w US-001 ([[ISSUE-007-data-layer]] przed kopią). Schemat v1 celowo pominął
> *Assertion* (`04_ARCHITECTURE/data-model.md` → *In code*), bo model nie mówi, **gdzie żyje wartość
> spornej daty: w *Event* czy w *Assertion***. Na v2 staną dane około 100 osób, więc to decyzja trudna do
> cofnięcia. Pozycja zaczyna się od kanonu i falsyfikatora, nie od projektu.

## What to build
1. **ADR-006: gdzie żyje wartość twierdzenia** (≥ 3 opcje, źródła zamiast pamięci). Wymienione opcje są
   kandydatami do porównania, a nie rozstrzygnięciem:
   - wartość w *Event* (jak w v1), a *Assertion* niesie tylko źródło i status przy nim;
   - wartość w *Event*, ale osoba może mieć kilka zdarzeń tego samego typu, każde ze swoim twierdzeniem;
   - wartość w *Assertion*, a *Event* bez własnej daty.

   ADR obejmuje całą ziarnistość z [[FR-001-provenance]] (daty, relacje, miejsce pochówku), nawet jeśli
   v2 wdroży tylko część. `planning` ustala, czy relacje wchodzą do v2, czy dojdą migracją przy
   [[US-003-przepisanie-rodziny]], i zapisuje to w planie.
2. **Schemat v2** z twierdzeniami według ADR-006, `PRAGMA user_version` = 2.
3. **Migracja v1→v2:** pierwsza prawdziwa ([[NFR-003-migracje-schematu]]). ISSUE-009 sprawdził tę drogę
   tylko na syntetycznej v2 z dodaną kolumną.
4. **Odtworzenie kopii v1 w aplikacji v2.** To ta sama ścieżka kodu co migracja (NFR-003 → *Notes*,
   [[ADR-004-backup-format-encryption-destination]] pkt 5).
5. **„Stan danych” i odcisk danych** obejmują tabelę twierdzeń.

## Acceptance Criteria
- [ ] ADR-006 `accepted` z ≥ 3 opcjami i z sekcją *Prior art*, która cytuje specyfikację GEDCOM 7 (link
      i rozdział), a nie pamięć. Przed wyborem zmierzony falsyfikator: przypadek z
      [[US-004-fakt-od-babci]] AC-1 zapisany w każdej opcji jako jednorazowy SQL na **wymyślonych**
      danych. Ta sama osoba ma tę samą datę z dwóch źródeł („notatki”, „babcia”) z różnymi wartościami.
      Oba twierdzenia zostają, status `CONTRADICTED`. Ten sam przypadek sprawdzić dla miejsca pochówku.
      Odpada opcja, w której drugie twierdzenie nie ma gdzie się zmieścić albo wymaga usunięcia
      pierwszego.
- [ ] Baza v2: `user_version` = 2, `integrity_check` = `ok`. Datę z dopiskiem i pochówek da się zapisać
      z twierdzeniem: źródło (domyślnie „notatki”), status `CLAIMED`, kiedy i kto
      ([[US-002-przepisanie-grobu]] AC-4, na poziomie danych).
- [ ] Test migracji v1→v2 (NFR-003): baza v1 z punktu odniesienia ISSUE-007 z wymyślonymi danymi →
      migracja → wszystkie rekordy v1 są obecne. ADR-006 zapisuje, co dostają daty z v1, które nie mają
      źródła.
- [ ] Kopia v1 odtwarza się w aplikacji v2: migracja przy odtworzeniu, liczby rekordów zgodne, odcisk
      zgodny przed migracją (tak sprawdza ISSUE-009 → *Implementation plan*).
- [ ] „Stan danych” i odcisk danych obejmują tabelę twierdzeń, a `tool/fingerprint.dart` liczy to samo.
- [ ] `data-model.md` → *In code* ma linię o v2 i odpowiedź na pytanie „Event czy Assertion” (link do
      ADR-006). Tabela encji zmienia się tylko wtedy, gdy ADR-006 zmienia model.

## Out of Scope
- Ekran przepisania grobu → [[ISSUE-012-transcribe-grave-screen]].
- Dopisywanie drugiego twierdzenia i przejścia `CONFIRMED` / `CONTRADICTED` jako funkcja →
  [[US-004-fakt-od-babci]]. Tutaj schemat **nie może** ich wykluczać; to falsyfikator, nie funkcja.
- Wprowadzanie relacji → [[US-003-przepisanie-rodziny]].
- Przegląd statusów „czy to nadal prawda?” → ⚠️ OPEN w [[FR-001-provenance]].

## Technical Notes
- **Co v1 już przesądza** (`grobing-code/lib/data/database.dart`): *Events* trzyma datę (`year` /
  `month` / `day`, zakres `…To`, `qualifier`), a *Burials* ma `person_id` UNIQUE, czyli co najwyżej jeden
  pochówek na osobę. Drugi, sprzeczny pochówek nie ma dziś gdzie się zmieścić, więc falsyfikator
  obejmuje pochówek, a nie tylko daty.
- **Kanon:** brief wskazuje GEDCOM jako punkt odniesienia dla własnego modelu, bez importu i eksportu
  (`kickoff/PROJECT_BRIEF.md` → wpis o GEDCOM, zmieniony 2026-10-05). Wersja przy kick-offie: GEDCOM 7
  (`kickoff/SESSION_STATE.md`). Źródło FR-001: Genealogical Proof Standard, wzorzec WZ-036.
- **„Kim była”** ma już jedną linię źródła w v1 (`bio_source`), zgodnie z decyzją kosztową FR-001.
- Statusy zapisywane po nazwie, nie po indeksie (zasada z komentarza w `database.dart`).
- **Odcisk po migracji z definicji się zmienia.** Odtworzenie porównuje go przed migracją, a liczby
  rekordów także po niej (ISSUE-009). Jeśli migracja tworzy twierdzenia dla dat z v1, liczby po migracji
  się różnią. `planning` ustala, co dokładnie sprawdza test.
- Wymyślone dane w buildzie debug dostają twierdzenia. **Nigdy w buildzie release** (ISSUE-007).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-007-data-layer]] (schemat v1, punkt odniesienia) | technical | `done` |
| [[ISSUE-009-restore]] (migracja przy odtworzeniu) | technical | `done` |
| `04_ARCHITECTURE/data-model.md` | technical | przyjęty w kick-offie; v2 dopisuje *In code* |
| [[ADR-005-sqlite-package]] | technical | `accepted` |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC · ręczna weryfikacja na
emulatorze · **test migracji z poprzedniej wersji (v1)** · próbne odtworzenie z kopii (kopia v1 →
aplikacja v2) · fakt o rodzinie → źródło i status zapisane (na poziomie danych; pierwsza pozycja, w
której ta linia DoD nie jest n/a) · zero danych rodziny w zmianach · INVEST self-check. Pozycja dotyka
warstwy danych, więc to kluczowa pozycja dla krytyka; do [[ISSUE-003-setup-quality-critic]] werdykt
daje self-check.

## Implementation plan
> `planning`, 2026-10-06. **DoR:** jasny zakres ✅ · powiązana US: [[US-002-przepisanie-grobu]] ✅ (AC-4 na
> poziomie danych; AC-1 i AC-3 schemat niesie od v1) · krok ścieżki: n/a, poza ścieżką (M1), tak jak wiersz
> w `TRACEABILITY.md` ✅ · `task-level` ✅. **Warstwa danych:** test migracji — **pierwszy prawdziwy** (v1→v2)
> · próbne odtworzenie — kopia v1 w aplikacji v2 · źródło faktu — **to jest ta pozycja**, na poziomie danych
> (dane wymyślone, tylko w buildzie debug).

### Prior art (sources, not memory)
[FamilySearch GEDCOM 7.0.18](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html) (17.02.2026),
odczyt 2026-10-06:
- **§3.2.3 EVENT_DETAIL:** *„Conflicting event information should be represented by placing them in
  separate event structures (with appropriate source citations) rather than by placing them under the same
  enclosing event.”*
- **§3.1:** *„Unless otherwise specified, the first is the most-preferred value. If an application needs to
  display just 1 of several NAMEs, BIRTs, etc, they should show the first such structure unless more
  specific selection criteria are available.”* Zdarzenia osoby, także `BURI`, mają krotność `{0:M}`.
- **§3.2.3 SOURCE_CITATION:** *„A source citation identifies a source and the relevant portion thereof. It
  connects a claim with the source documenting that claim.”* Na zdarzeniu `{0:M}`. `QUAY` 0-3 ocenia dowód
  (0 *„Unreliable evidence or estimated data”* … 3 *„Direct and primary evidence used, by itself”*).
- **§2.4 Date:** `ABT` · `BEF` · `AFT` · `BET … AND` odpowiadają dopiskom z [[FR-004-data-z-dopiskiem]].
  `CAL` i `EST` nie mają odpowiednika i zostają poza zakresem.

**Co mówi kanon:** wartość żyje w zdarzeniu. Sprzeczne wartości to osobne zdarzenia, a źródło to cytowanie
przy zdarzeniu (może ich być kilka). **Gdzie Grobing się różni:** `QUAY` ocenia siłę dowodu, a status z
[[FR-001-provenance]] opisuje relację między źródłami (`CLAIMED` · `CONFIRMED` · `CONTRADICTED` ·
`UNKNOWN`). Statusy zostają z FR-001, a `QUAY` nie wchodzi.

### Falsifier — measured 2026-10-06 (throwaway SQL)
Python `sqlite3` (SQLite 3.50.4), baza w pamięci, przycięty schemat v1, wymyślone osoby. Skrypt leżał w
katalogu tymczasowym sesji, a nie w repo. Przypadki: **T1** sprzeczna data, **T2** sprzeczne miejsce
pochówku (oba z [[US-004-fakt-od-babci]] AC-1) · **T3** potwierdzenie (US-004 AC-2) · **T4** `UNKNOWN`
(US-004 AC-3) · **T5** widok grobu (US-002 AC-1) · **T6** migracja z v1 bez utraty wierszy.

| Wariant | T1 | T2 | T3 | T4 | T5 | T6 | Werdykt |
|---|---|---|---|---|---|---|---|
| **A** — jedno zdarzenie danego typu na osobę, twierdzenie 1:1 przy nim | ❌ UNIQUE `events(person_id, type)` | ❌ UNIQUE `burials.person_id` | ❌ UNIQUE `assertions.event_id` | ✅ | ✅ | ✅ | **odpada** |
| **B** — osobne struktury (GEDCOM): wartość w *Event* / *Burial*, sprzeczna = nowy wiersz, twierdzenia 1..N przy wierszu | ✅ | ✅ (po zdjęciu UNIQUE) | ✅ | ✅ | ✅ | ✅ | przechodzi |
| **C** — wartość w twierdzeniu: jedna tabela faktów (`fact` = `birth_date`, `burial_grave`…) zamiast dat w *Event* i grobu w *Burial* | ✅ | ✅ | ✅ | ✅ | ✅ | ✅, ale kasuje `events` i `burials` | **odpada na odtworzeniu** (niżej) |
| **D** — wniosek + dowody: *Event* trzyma jedną wartość preferowaną, każde twierdzenie własną kopię wartości | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | przechodzi, ale schemat przyjmuje wartość bez źródła: *Event* = 1777, zgodnych twierdzeń 0 |

**Drugi pomiar, w kodzie:** po migracji starszej kopii odtworzenie sprawdza, że **każda tabela z manifestu
kopii istnieje i ma tę samą liczbę wierszy** (`grobing-code/lib/backup/restore_service.dart:254-264`).
Wariant C kasuje `events` i `burials`, więc żadna kopia v1 by się nie odtworzyła. **To kontrakt dla każdej
migracji:** tabele i liczby wierszy z poprzedniej wersji zostają; nowa tabela nie jest w starym manifeście.

### Decisions for stop #1
**Problem:** schemat v1 nie ma gdzie zapisać źródła daty ani drugiej, sprzecznej wartości, a na v2 staną
prawdziwe dane. Zła decyzja ujawni się dopiero przy US-004 i trzeba ją będzie wtedy naprawiać migracją
prawdziwych danych.

| # | Decyzja | Rekomendacja | Dlaczego · co ją obali |
|---|---|---|---|
| D1 | **Gdzie żyje wartość (ADR-006)** | **B — osobne struktury, jak GEDCOM 7.** Data z dopiskiem zostaje w `events`, grób w `burials`. Wartość sprzeczna z innym źródłem to osobny wiersz. Nowa tabela `assertions` jest cytowaniem: 1..N twierdzeń na wiersz `events` albo `burials` | Tylko B zgadza się z kanonem 1:1 (§3.2.3). Nie daje wartości dwóch domów (D) i nie psuje odtworzenia kopii v1 (C). v1 już pozwala na kilka zdarzeń tego samego typu, więc dla dat migracja tylko dokłada tabelę. **Koszt:** lista wszystkich twierdzeń o osobie to suma po dwóch tabelach, a z relacjami po czterech. **Obali:** fakt z US-003 albo US-004, którego nie da się zapisać jako osobny wiersz z twierdzeniem. Sprawdzić tym samym falsyfikatorem na początku planu US-003 |
| D2 | **Pochówek a [[FR-003-wiele-osob-w-grobie]]** | FR-003 („osoba ma co najwyżej jeden pochówek”) czytać jako **fakt**: człowiek leży w jednym miejscu, ale twierdzeń o tym miejscu może być kilka. Sprzeczne twierdzenia to dwa wiersze `burials` tej samej osoby, oba `CONTRADICTED`. `burials` traci UNIQUE na `person_id` i dostaje własne `id`. `docs` dopisuje do FR-003 datowane doprecyzowanie | Dziś FR-003 i FR-001 („miejsce pochówku jest twierdzeniem”, a sprzeczne twierdzenia współistnieją) mówią co innego. GEDCOM: `BURI {0:M}`. **Alternatywa:** zostawić UNIQUE i odłożyć sprzeczne miejsce do US-004. Wtedy US-004 i tak zdejmie UNIQUE, tylko migracją prawdziwych danych. **Koszt:** osoba, o której źródła się spierają, pojawi się w widoku obu grobów; oznaczenie tego to US-004 |
| D3 | **Którą wartość pokazać** | Jak GEDCOM §3.1: **pierwszą**, czyli o najniższym `id` (wpisaną najwcześniej). Bez kolumny „preferowana” w v2 | US-002 wpisuje jedno twierdzenie na fakt. Wybranie innej wartości jako preferowanej należy do US-004 i wtedy dochodzi kolumna (migracją). Generalizujemy z instancji |
| D4 | **Jak zapisać źródło** | **rodzaj** z FR-001 (nagrobek · notatki · babcia · krewny · akt; enum zapisany po nazwie) + **szczegół** (tekst opcjonalny: który krewny, który akt, czyli „kto je podał”) + **kiedy zapisane** (`recorded_at`, UTC) + **status** (enum zapisany po nazwie). Bez tabeli źródeł (`SOURCE_RECORD` z GEDCOM) | Realne źródła są dziś dwa: notatki i babcia. Tabela źródeł byłaby generalizacją przed instancjami. Eksport GEDCOM (C2, nice-to-have) zamieni rodzaj i szczegół na rekordy `SOUR`. **Obali:** potrzeba wskazania tego samego dokumentu (np. jednego aktu) z wielu faktów i poprawiania go w jednym miejscu. Wtedy tabela źródeł migracją |
| D5 | **Wiersze z v1 przy migracji** | Każdy wiersz `events` i `burials` z v1 dostaje jedno twierdzenie: `notatki`, `CLAIMED`, szczegół „przeniesione z v1”, `recorded_at` = chwila migracji | Prawdziwych danych w v1 nie ma nigdzie: telefon dostanie dopiero MVP (`DEFINITION_OF_DONE.md`), a na emulatorach są dane wymyślone. Jedyną zaplanowaną drogą dat do v1 było przepisanie z notatek, a szczegół mówi otwarcie, że to założenie. Od v2 obowiązuje niezmiennik: **każdy wiersz `events` i `burials` ma ≥ 1 twierdzenie**. **Obali:** kopia v1 z prawdziwymi danymi, której DoD nie dopuszcza |
| D6 | **Relacje** (FR-001: rodzice, małżeństwa) | **Poza v2.** Dojdą migracją v3 przy [[US-003-przepisanie-rodziny]] w tym samym kształcie: twierdzenie przy wierszu powiązania (`family_partners`, `family_children` dostaną `id`). ADR-006 opisuje to jednym zdaniem | US-002 nie wpisuje relacji, a [[NFR-003-migracje-schematu]] robi z migracji rutynę z testem. **Obali:** to samo co D1 |

### Scope diff vs the item (to accept at stop #1)
- **AC-1 (falsyfikator przed wyborem) zmierzony już tutaj**, na 4 wariantach (wyżej). `dev` go nie powtarza.
  Plik ADR-006 pisze `docs` przy zamknięciu z *Prior art*, *Falsifier* i D1-D6, tak jak ADR-005 w
  ISSUE-007 (*Dev report* → *Deviations*).
- **+ doprecyzowanie FR-003** (D2), przez `docs` przy zamknięciu.
- **+ test z syntetyczną wersją z ISSUE-009 przechodzi z v2 na v3.** Dziś udaje v2
  (`test/backup/restore_service_test.dart:147`), a prawdziwa v2 zajmie ten numer. Mechanizm „starsza kopia
  → migracja” dalej ma test niezależny od prawdziwej v2 (`qa`).
- **+ `lib/data/claims.dart`**: zapis faktu z twierdzeniem w jednej transakcji. Bez tego nie da się
  sprawdzić AC-2, a ISSUE-012 dostaje gotowe API.
- **− relacje** (D6) · **− kolumna „preferowana”** (D3).

### Schema v2 (diff vs v1)
| Tabela | Zmiana |
|---|---|
| `assertions` (nowa) | `id` · `event_id` **albo** `burial_id` (dokładnie jedno, CHECK) · `source_kind` (enum po nazwie) · `source_detail` (tekst, opcjonalny) · `status` (enum po nazwie) · `recorded_at` (UTC) |
| `burials` | **+ `id`** (klucz) · **− UNIQUE na `person_id`** (D2). Przebudowa tabeli w migracji, wiersze 1:1 |
| `events` | bez zmian (v1 już dopuszcza kilka zdarzeń tego samego typu) |
| pozostałe | bez zmian; `persons.bio_source` zostaje jedną linią źródła „kim była” (FR-001) |

### Steps (dev)
0. **Najpierw, przed jakąkolwiek zmianą w kodzie:** zbudować APK v1 z obecnego `main` (`flutter build apk
   --debug`) i odłożyć go do katalogu tymczasowego sesji. To punkt startu testu aktualizacji na stopie #2.
   Później dałoby się do niego wrócić tylko przez `git checkout`, którego agent nie wykonuje
   (`git-autonomy-boundary.md`).
1. `lib/data/database.dart`: enumy `SourceKind` i `AssertionStatus` (po nazwie), tabela `Assertions`,
   `Burials` z `id` i bez UNIQUE, `currentSchemaVersion = 2`. Krok migracji 1→2 w jednej transakcji:
   utworzyć `assertions`, przebudować `burials` (drift `TableMigration`) z zachowaniem wierszy i dodać
   twierdzenia dla wierszy v1 (D5). Po zmianie `build_runner` i `make-migrations` → `drift_schemas/grobing/`
   v2, `test/drift/grobing/generated/schema_v2.dart` i scaffold testu v1→v2.
2. `lib/data/claims.dart` (nowy): zapis daty z dopiskiem razem z twierdzeniem oraz pochówku razem z
   twierdzeniem, w jednej transakcji. Domyślnie `notatki` + `CLAIMED`. Odczyt „pierwszej” wartości (D3).
3. `lib/dev/fictional_data.dart`: wymyślone dane dostają twierdzenia, plus jeden wymyślony spór (data z
   „notatki” i z „babcia”, oba `CONTRADICTED`). Tylko debug, jak dotąd.
4. `lib/data/data_state.dart` i `tool/fingerprint.dart`: sprawdzić, że nowa tabela liczy się sama (tabele
   z `sqlite_master`, ISSUE-007 krok 4). Jeśli tak, kod się nie zmienia, a potwierdza to test `qa`.
5. README `grobing-code` → *Baza danych*: v2, niezmiennik z D5, zasada „pierwsza wartość” (D3) i kontrakt
   migracji (tabele i liczby wierszy z poprzedniej wersji zostają).
6. Do `docs` przy zamknięciu: ADR-006, linia w `data-model.md` → *In code*, doprecyzowanie FR-003.

### Files likely touched
`grobing-code`: `lib/data/database.dart` + `database.g.dart` · `lib/data/claims.dart` (nowy) ·
`lib/dev/fictional_data.dart` · `drift_schemas/grobing/` (v2) · `test/drift/grobing/generated/` (v2) ·
`README.md` · testy (`qa`): migracja v1→v2, `test/data/claims_test.dart` (nowy),
`test/backup/restore_service_test.dart`, `test/data/data_state_test.dart`.
`grobing-vault`: ta pozycja · `TRACEABILITY.md` · przy zamknięciu: ADR-006 (nowy), `data-model.md`, FR-003.

### AC → tests (`qa`)
| AC | Test happy-path | Ręcznie (stop #2) |
|---|---|---|
| AC-1 ADR-006 + falsyfikator | pomiar w *Falsifier* (skrypt jednorazowy, nie test stały) | — |
| AC-2 baza v2 + zapis z twierdzeniem | świeża baza: `user_version` 2, `integrity_check` `ok`. „około 1890” → zdarzenie + 1 twierdzenie `notatki`/`claimed`; pochówek → wiersz + twierdzenie. **Przypadek US-004 AC-1 na v2:** druga data i drugi pochówek tej samej osoby ze źródłem „babcia” zapisują się, a pierwsze zostają | „Stan danych”: schemat 2, tabela twierdzeń w liczbach |
| AC-3 migracja v1→v2 | test `drift` (wygenerowany): v1 z wymyślonymi danymi → v2. Każdy wiersz v1 jest obecny, każdy wiersz `events`/`burials` ma dokładnie 1 twierdzenie (D5), schemat zgodny z eksportem v2 | aktualizacja na emulatorze bez odinstalowania (niżej) |
| AC-4 kopia v1 → aplikacja v2 | kopia v1 → aplikacja v2: `user_version` 2, liczby = manifest, odcisk zgodny przed migracją. Syntetyczna v3 dalej przechodzi | odtworzenie kopii zrobionej przed aktualizacją |
| AC-5 odcisk + „Stan danych” | odcisk obejmuje `assertions`: zmiana statusu jednego twierdzenia zmienia odcisk; `tool/fingerprint.dart` = ekran | — |
| AC-6 `data-model.md` | — (`docs` przy zamknięciu) | — |
| niezmiennik D5 | po migracji i po każdym zapisie przez `claims.dart`: żaden wiersz `events`/`burials` bez twierdzenia | — |

### Manual verification (stop #2) — kroki według miejsca
Sprawdzamy drogę, którą przejdzie każda przyszła aktualizacja na telefonie: **stara wersja z danymi → nowa
wersja wgrana na wierzch → dane są**. Przygotowanie (agent, przez `adb`): `Medium_Phone` z APK v1 z kroku 0
i wymyślonymi danymi. Przed krokami agent sprawdza `dumpsys package com.grobing.app`, bo emulator potrafi
wrócić ze starej migawki.
- **Emulator (v1):**
  1. „Stan danych” → zanotuj: schemat **1**, liczby, odcisk.
  2. „Zrób kopię teraz”. Jeśli kopia nie jest skonfigurowana, skonfiguruj ją hasłem testowym. Miejsce
     może być w Pobranych emulatora.
- **Terminal VS Code** (`grobing-code`): agent wgrywa APK v2 **na wierzch** (`adb install -r`, ten sam klucz
  debug, bez odinstalowania).
- **Emulator (v2):**
  3. „Stan danych” → schemat **2**, liczby tabel z kroku 1 **bez zmian**, nowa tabela twierdzeń z liczbą =
     zdarzenia + pochówki. Odcisk inny niż w kroku 1, bo przybyła tabela.
  4. „Odtwórz z kopii” → kopia z kroku 2 → po odtworzeniu schemat **2** i te same liczby co w kroku 3.
- **Napisz tutaj:** „ok” · „pomiń” · opis błędu.

### Out of Scope (this plan)
- Ekran i jakikolwiek widok twierdzeń → [[ISSUE-012-transcribe-grave-screen]].
- Przejścia statusów jako funkcja, wybór wartości preferowanej → [[US-004-fakt-od-babci]].
- Relacje (D6) · tabela źródeł (D4) · `QUAY` · daty `CAL`/`EST` · usuwanie wierszy.

### Self-check (planning) — said out loud
- **Falsyfikator sprawdził kształty, nie kod drift.** Przebudowa `burials` przez `TableMigration` na
  przypiętym `drift` 2.34.0 nie jest zmierzona. Jeśli generator nie przejdzie, STOP.
- **D2 zmienia czytanie wymagania**, nie tylko schemat. Dlatego to decyzja autora, a nie `dev`.
- Niezmiennika „każdy wiersz ma twierdzenie” SQLite nie wymusi bez wyzwalaczy. W v2 pilnuje go kod
  (`claims.dart`) i test. Wyzwalacz byłby generalizacją przed drugim piszącym kodem.
- Status `CONTRADICTED` przy drugim twierdzeniu ustawia dziś tylko test. Kod, który ustawia go sam, to
  US-004.

## Dev report
> `dev`, 2026-10-06. Stop #1: „tak”, D2 według rekomendacji. Flutter 3.41.1 zgodny z przypiętym.

### Step 0 — APK v1 before any change: ✅
`flutter build apk --debug` z `e13e94b` (repo czyste) → `grobing-v1-e13e94b-debug.apk` w katalogu
tymczasowym sesji. Punkt startu testu aktualizacji na stopie #2.

### What was built
- `lib/data/database.dart`: enumy `SourceKind` (`gravestone` · `notes` · `grandmother` · `relative` ·
  `record`) i `AssertionStatus` (`claimed` · `confirmed` · `contradicted` · `unknown`), oba zapisywane po
  nazwie; tabela `Assertions` (CHECK: zdarzenie **albo** pochówek); `Burials` z `id`, bez UNIQUE na osobie;
  `currentSchemaVersion = 2`. Krok `_from1To2`: `alterTable` na `burials` (dawny `rowid` → `id`),
  `createTable(assertions)`, potem twierdzenia `notes` / `claimed` / „przeniesione z v1” dla wierszy v1 (D5).
- **Wszystkie kroki migracji i `user_version` w jednej transakcji** (wzorzec z dokumentacji `drift`,
  `Migrator.runMigrationSteps`). `drift` zapisuje wersję dopiero po migracji. Bez tego aplikacja zabita
  między krokiem a zapisem wersji przy następnym starcie zaczęłaby migrację drugi raz na w połowie
  zmienionej bazie i by się nie otworzyła.
- `lib/data/claims.dart` (nowy): `addEventWithClaim`, `addBurialWithClaim` (jedna transakcja, typowane API
  `drift`, więc zapis budzi `tableUpdates` i zamawia kopię w tle — ISSUE-010), `firstEvent`, `firstBurial`
  (D3), `ClaimSource` z domyślnym „notatki, `claimed`”.
- `lib/dev/fictional_data.dart`: zdarzenia i pochówki przez `claims.dart`, plus jeden wymyślony spór (rok
  urodzenia ojca: notatki „około 1890” i babcia „1892”, oba `contradicted`). Partia ma teraz 5 zdarzeń,
  3 pochówki i 8 twierdzeń.
- Wygenerowane: `database.g.dart`, `database.steps.dart` (nowy), `drift_schemas/grobing/drift_schema_v2.json`,
  `test/drift/grobing/generated/schema_v2.dart` (+ `schema.dart`, `schema_v1.dart` z klasami danych do
  testów integralności), szkielet `test/drift/grobing/migration_test.dart`.
- README `grobing-code` → *Baza danych*: jedna transakcja, kontrakt „nie usuwa tabel ani wierszy”,
  twierdzenia (D1, D3, D5).
- Krok 4 planu: **bez zmian w kodzie.** `readDataState` bierze tabele z `sqlite_master`, a
  `tool/fingerprint.dart` woła tę samą funkcję.

### Checks (dev, host Windows)
- **Weryfikator `drift`** (wygenerowany `migration_test.dart`, część „simple”): schemat po migracji 1→2 =
  świeży v2 ✅. Część z danymi to pusty szablon dla `qa`.
- **Test dymny** (jednorazowy, w katalogu tymczasowym, poza repo; baza v1 z wygenerowanej klasy
  `DatabaseAtV1`, wymyślone osoby):
  - po migracji: v2, liczby tabel v1 bez zmian (`events` 3, `burials` 3), `assertions` 6;
  - `id` pochówków = dawny `rowid` (kolejność wierszy zachowana);
  - pierwsze twierdzenie:
    `{event_id: 1, source_kind: notes, source_detail: przeniesione z v1, status: claimed, recorded_at: 1791295807}`;
  - zero wierszy `events` / `burials` bez twierdzenia; `integrity_check` = `ok`; `foreign_key_check` pusty.
  - **US-004 AC-1 na v2:** druga data (babcia, 1892) i drugi grób tej samej osoby zapisują się, pierwsze
    zostają. `firstEvent` = 1890, `firstBurial` = pierwszy grób. Ta sama para osoba + grób drugi raz →
    odmowa.
  - Partia wymyślonych danych na zmigrowanej bazie: `events` 9 · `burials` 7 · `assertions` 16 (zgodne z
    rachunkiem).
- `flutter analyze lib`: czyste. W całym repo jedna uwaga `info` (`directives_ordering`) w wygenerowanym
  szkielecie `migration_test.dart`, czyli w pliku `qa`.

### Deviations from the plan
- **+ UNIQUE (`person_id`, `grave_id`) na `burials`.** Wynika z D1: ta sama osoba w tym samym grobie to ta
  sama wartość, a drugie źródło dla niej to drugie twierdzenie, nie drugi wiersz. Bez tego potwierdzenie
  dałoby się zapisać na dwa sposoby.
- **+ etykieta „Twierdzenia (źródła)” na „Stanie danych”** (`lib/app/data_state_screen.dart`). Bez niej
  nowa tabela pojawiałaby się na końcu jako surowe `assertions`.
- `carriedOverFromV1` jest publiczną stałą, żeby test migracji nie powtarzał tekstu.
- ADR-006, linia w `data-model.md` i doprecyzowanie FR-003 → `docs` przy zamknięciu (jak w ISSUE-007).

### For qa
- **`flutter test`: 227 ✅ / 23 ❌.** Przyczyną nie jest kod, tylko testy, które zakładają v1:
  - `test/support/backup_fakes.dart:173` — `restoreServiceIn(… schemaVersion = 1)`: kopia z bazy v2 jest
    dla nich „z nowszej wersji” (stąd większość `restore_service_test` i `restore_screen_test`). Błędy
    `PathAccessException` przy usuwaniu katalogów to skutek uboczny: test rzucił wyjątek, zanim zamknął
    bazę;
  - syntetyczna v2 z ISSUE-009 (`restore_service_test.dart:147, 799, 843`) i „inna wersja” = 2 w
    `background_backup_test.dart:371` → przesunąć na 3 (scope diff planu);
  - `data_state_test`, `database_test` (AC-2: „schemat v1, dokładnie tabele v1”), `data_state_screen_test`
    (szuka „1”), `backup_archive_test` (4 zdarzenia w partii → teraz 5).
- Do wypełnienia: szablon integralności w `migration_test.dart` (AC-3, D5).
- **Z kodu, niezmierzone:** kroki migracji idą przez `customStatement`, a to nie budzi `tableUpdates`.
  Kopia v2 po aktualizacji zostanie więc zamówiona przy wyjściu z aplikacji albo przy następnym starcie
  (stempel danych się zmienił), a nie w chwili migracji.

### Manual verification (stop #2) — kroki według miejsca
Bez zmian względem planu, z jednym doprecyzowaniem: nowa tabela na „Stanie danych” nazywa się
**„Twierdzenia (źródła)”**. Na jedną partię wymyślonych danych z v1 (4 zdarzenia, 3 pochówki) po
aktualizacji powinno ich być **7**.

## Verification
> `qa`, 2026-10-06. Werdykt: **APPROVED (self-check, z uwagami)**. Krytyka jeszcze nie ma
> ([[ISSUE-003-setup-quality-critic]]).

### Automated — `flutter test`: 258 ✅ · `flutter analyze`: czyste
| AC | Dowód | Wynik |
|---|---|---|
| AC-1 ADR-006 + falsyfikator | *Implementation plan* → *Falsifier* (4 warianty, jednorazowy SQL) | ✅ pomiar · ⏳ **plik ADR-006 pisze `docs` przy zamknięciu** |
| AC-2 baza v2 + zapis z twierdzeniem | `test/data/claims_test.dart`: data „około 1890” → zdarzenie + twierdzenie `notes`/`claimed`/czas; pochówek + twierdzenie; nieudany zapis nie zostawia ani wiersza, ani twierdzenia; CHECK „zdarzenie albo pochówek”. **US-004 AC-1 na v2:** druga data i drugi grób od babci zapisują się obok notatek, nic nie jest zastąpione, pokazywany jest pierwszy wiersz, ten sam grób drugi raz → odmowa. `test/data/database_test.dart`: świeża baza = v2, 11 tabel; drugi grób tej samej osoby dozwolony (D2) | ✅ |
| AC-3 migracja v1→v2 | `test/drift/grobing/migration_test.dart`: weryfikator `drift` (schemat po migracji = świeży v2) i test z danymi: wiersze v1 wartość w wartość, `burials` z `id` = dawny `rowid` (kolejność zachowana), 6 twierdzeń `notes` / „przeniesione z v1” / `claimed` z czasem migracji | ✅ |
| AC-4 kopia v1 → aplikacja v2 | `restore_service_test.dart` → *ISSUE-011 AC-4*: archiwum v1 złożone z bazy tworzonej eksportem schematu v1 (`DatabaseAtV1`) → odtworzenie na świeżym telefonie: `(1, 2)`, liczby tabel v1 = manifest, 4 twierdzenia „przeniesione z v1”. Mechanizm „starsza kopia → nowsza aplikacja” ma dalej test syntetyczny, teraz „bieżąca + 1” | ✅ |
| AC-5 odcisk + „Stan danych” | `claims_test`: zmiana statusu jednego twierdzenia zmienia odcisk przy tych samych liczbach; `data_state_screen_test`: wiersz „Twierdzenia (źródła)”; `tool/fingerprint.dart` woła tę samą `readDataState` | ✅ |
| AC-6 `data-model.md` | — | ⏳ `docs` przy zamknięciu |
| niezmiennik D5 | `claims_test`: po zapisach przez `claims.dart` i po partii wymyślonych danych żaden wiersz `events`/`burials` nie jest bez twierdzenia | ✅ |

**23 testy z założeniem v1 poprawione, nie wyłączone.** Wersja schematu w testach wynika teraz z
`GrobingDatabase.currentSchemaVersion` (`restoreServiceIn`, „nowsza kopia”, „inna wersja” w kopii w tle,
`VACUUM INTO`, manifest), więc następne podbicie nie zepsuje ich znowu. Liczby wymyślonych danych: 5
zdarzeń i 8 twierdzeń na partię.

### Manual (stop #2) — kroki oddane agentowi
**Autor, 2026-10-06:** *„Tutaj Ci ufam, że to działa. Najbardziej zależało mi, żeby testy użytkownika
dotyczyły elementów UI/UX, gdzie faktycznie mogę poczuć domyślny flow finalnego usera.”* Pozycja nie ma
nowego ekranu, więc kroki wykonał agent na emulatorze `Medium_Phone_API_36.1` (build debug, wymyślone
dane), a nie autor:
1. APK v1 z `e13e94b` wgrany przez `adb install -r` na zainstalowaną aplikację. Baza: `user_version` 1,
   8 partii wymyślonych danych (zdarzenia 32, pochówki 24).
2. APK v2 wgrany **na wierzch**, bez odinstalowania; „Stan danych” otwarty dotknięciem
   (`uiautomator`). Ekran: schemat **2**, wszystkie liczby jak w v1, „Twierdzenia (źródła)” **56** (32 + 24).
3. Baza zdjęta z telefonu (`run-as`) i porównana z kopią sprzed aktualizacji: `integrity_check` `ok`,
   **wszystkie tabele v1 identyczne wiersz w wiersz**, `id` pochówków = dawny `rowid`, 56 twierdzeń
   `notes` / „przeniesione z v1” / `claimed`, 0 wierszy bez twierdzenia.
4. „Wgraj wymyślone dane” na v2: +5 zdarzeń, +3 pochówki, +8 twierdzeń, w tym para sprzeczna
   (notatki i babcia, `contradicted`); 0 wierszy bez twierdzenia.

**Nie zrobione na urządzeniu:** odtworzenie kopii v1 w aplikacji v2. Wymaga hasła testowego wpisanego w
oknie odtworzenia, a hasło zna tylko autor. Pokrywa je test na hoście (AC-4) z prawdziwym archiwum v1.
Ścieżka odtworzenia przez Dysk na Androidzie była sprawdzona przy [[ISSUE-009-restore]].

### DoD lines specific to Grobing
- **Test migracji z poprzedniej wersji:** ✅ (AC-3, na hoście i na emulatorze).
- **Próbne odtworzenie z kopii:** ✅ na hoście z kopią v1 (AC-4) i z kopią v2 (dotychczasowe testy
  ISSUE-009 na v2); na urządzeniu nie (wyżej).
- **Fakt o rodzinie → źródło i status:** ✅ na poziomie danych. Każdy zapis zdarzenia i pochówku idzie z
  twierdzeniem; ekranu, który to zapisuje, jeszcze nie ma ([[ISSUE-012-transcribe-grave-screen]]).
- **Zero danych rodziny w zmianach:** ✅. W `git status` nie ma baz, kopii, eksportów ani zdjęć; w
  testach i danych debug tylko wymyślone osoby („Ojciec 1”, „Wymyślona”, „Cmentarz Wymyślony”). Bazy
  zdjęte z emulatora leżą tylko w katalogu tymczasowym sesji.
- **INVEST:** jeden komponent (warstwa danych), sprawdzalny bez ekranu.

### What I looked for and did not find
- utraty wiersza albo zmiany wartości przy migracji (porównanie wiersz w wiersz na urządzeniu);
- naruszeń kluczy obcych po migracji (`foreign_key_check` pusty — test dymny `dev`);
- wiersza `events`/`burials` bez twierdzenia (host i urządzenie);
- testu wyłączonego albo osłabionego, żeby przeszedł (każdy z 23 poprawionych sprawdza to samo co
  wcześniej, tylko przy v2);
- kodu migracji, który kasuje albo tworzy bazę od nowa.

### Notes (do not block)
1. **Zapis kopii czyta migawkę przez `GrobingDatabase` tylko do odczytu** (`backup_archive.dart`), więc
   migawka musi mieć wersję aplikacji. Dziś tak jest: kopia w tle pomija bazę w innej wersji, a przycisk
   działa na otwartej, zmigrowanej bazie. Dlatego kopię v1 do testu AC-4 trzeba było złożyć ręcznie.
2. **Kopia v2 po aktualizacji** zostanie zamówiona przy wyjściu z aplikacji albo przy następnym starcie,
   a nie w chwili migracji, bo kroki migracji nie budzą `tableUpdates`. Wniosek z kodu, niezmierzony.
3. Status `contradicted` ustawiają dziś tylko testy i dane debug. Aplikacja będzie to robić w
   [[US-004-fakt-od-babci]].
4. Build release (AOT) nie był uruchamiany; migracja nie ma kodu zależnego od `vm:entry-point`. Telefon
   dostanie dopiero MVP.
