---
title: "US-002 — Transcribe a grave from the notes (przepisanie grobu)"
type: user-story
status: done
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M1]
journey-steps: "n/a — poza ścieżką (M1, warunek kroku 1 UJ-001)"
FR: ["[[FR-001-provenance]]", "[[FR-003-wiele-osob-w-grobie]]", "[[FR-004-data-z-dopiskiem]]", "[[FR-005-nazwisko-rodowe]]"]
NFR: ["[[NFR-003-migracje-schematu]]"]
issues: ["[[ISSUE-011-schema-v2-assertions]]", "[[ISSUE-014-home-map-of-poland]]", "[[ISSUE-015-add-cemetery-from-database]]", "[[ISSUE-012-transcribe-grave-screen]]"]
quality-verdict: APPROVED
verdict-date: 2026-10-07
verdict-reviewer: self-check
source: "PROJECT_BRIEF §5 M1 · data-model.md (Cemetery, Grave, Burial, Person, Event, Assertion)"
created: 2026-10-05
updated: 2026-10-07
---

# US-002 — Przepisanie grobu z notatek

## Story
**Jako** Zbierający **chcę** wpisać cmentarz, grób na nim i wszystkie osoby w nim pochowane, z datami
takimi, jakie są w notatkach, **żeby** grób z papieru istniał w aplikacji razem ze źródłem każdej daty.

## Acceptance Criteria
- **AC-1 — grób z wieloma osobami.** *Given* cmentarz w aplikacji *When* dodaję grób i wpisuję do niego
  kilka osób *Then* grób pokazuje wszystkie pochowane osoby ([[FR-003-wiele-osob-w-grobie]]).
- **AC-2 — osoba z nazwiskiem rodowym.** *When* wpisuję osobę *Then* mogę podać imiona, nazwisko,
  osobno nazwisko rodowe ([[FR-005-nazwisko-rodowe]]) i „kim była".
- **AC-3 — data z dopiskiem.** *When* wpisuję datę urodzenia albo zgonu *Then* mogę wybrać dokładnie / około /
  przed / po / między, a aplikacja pokazuje datę z dopiskiem ([[FR-004-data-z-dopiskiem]]). Data pochówku nie
  jest polem formularza (decyzja autora 2026-10-07, [[ISSUE-012-transcribe-grave-screen]] D7): model ją
  przechowuje, a widok grobu pokazuje ją z dopiskiem („· poch. …”), gdy osoba ją ma. *Zmienione 2026-10-07;
  wcześniej: „urodzenia, zgonu albo pochówku”.*
- **AC-4 — źródło przy datach i miejscu pochówku.** *When* zapisuję daty i pochówek *Then* każde z tych
  twierdzeń ma źródło (domyślnie „notatki") i status `CLAIMED`; „kim była" ma jedną linię źródła
  ([[FR-001-provenance]]).
- **AC-5 — grób bez adresu, pinezki i zdjęcia.** *Given* notatki nie mają adresu kwatery *When* zapisuję
  grób tylko z cmentarzem i osobami *Then* grób się zapisuje, a brak adresu i pinezki jest widoczny
  (potwierdzone przez autora 2026-10-06 — *Open questions*).

## Out of scope
- Rodzice, małżeństwa, dzieci → [[US-003-przepisanie-rodziny]].
- Drugie, sprzeczne twierdzenie (babcia vs notatki) → [[US-004-fakt-od-babci]].
- Zdjęcia nagrobka i osoby → [[US-005-zdjecia]].
- Pinezka i jej poprawa na miejscu → [[EPIC-002-wizyta]] (M6).

## Open questions
- ✅ **Zamknięte — grób bez adresu kwatery, pinezki i zdjęcia.** **Decyzja autora (2026-10-06): jeden wpis w notatkach = jeden nagrobek i osoby w nim.** Grób z notatek
  to więc cmentarz + osoby; adres kwatery, pinezka i zdjęcie są opcjonalne i dochodzą przy wizycie.
  Model danych bez zmian (pochówek wymaga grobu).
  - **Rozważone opcje:** (A) grób = cmentarz + osoby — **wybrana**; (B) osobny poziom „miejsce rodziny”
    między cmentarzem a grobem — odrzucona, nic w notatkach go nie wymaga; (C) pochówek = osoba +
    cmentarz, grób opcjonalny (wzorzec Find a Grave: wpis osoby na cmentarzu, kwatera i GPS później) —
    niepotrzebna, bo notatki zawsze mówią, kto leży razem.
  - **Wraca do decyzji, gdy** przy przepisywaniu pojawi się wpis, który nie jest jednym nagrobkiem (kilka
    grobów rodziny obok siebie albo osoba przy cmentarzu bez grobu). Wtedy opcja C, migracją schematu.
  - Pytanie, jak taki grób znaleźć na miejscu, należy do [[EPIC-002-wizyta]] (`TRACEABILITY.md` → *Open
    gaps* 1) i tej US nie blokuje.

## Verification (US)
> `qa`, 2026-10-07. Werdykt na poziomie US wystawił **niezależny przegląd** (subagent bez udziału w budowie, tylko
> odczyt plików i jeden przebieg `flutter test`: **341/341**, ok. 37 s). DoD US: każde AC z testem happy-path ·
> pokazane w aplikacji na emulatorze · werdykt zapisany · wiersz w `TRACEABILITY.md`.

| AC | Test happy-path | Pokazane człowiekowi (emulator) |
|---|---|---|
| AC-1 grób z wieloma osobami | `graves_test.dart` (nowy grób z pierwszą osobą, potem druga) · `grave_screens_test.dart` (przejście „Dodaj grób” → … → obie osoby) · *Given*: `home_screen_test.dart` („Otwórz cmentarz”, dodanie z bazy) | ISSUE-012 stop #2 „ok” (stan urządzenia potwierdzony: grób z nazwą, dwie osoby) · *Given*: ISSUE-014 i ISSUE-015 stop #2 |
| AC-2 imiona, nazwisko, rodowe, „kim była” | `graves_test.dart` · `grave_screens_test.dart` (karta „Anna Wymyślona z d. Zmyślona”) | ISSUE-012 stop #2, kroki 2 i 4 |
| AC-3 data z dopiskiem (po D7) | `dates_test.dart` (pięć dopisków, linia lat życia) · `graves_test.dart` (zapis i odczyt z dopiskiem) · `grave_screens_test.dart` (około i między z menu, podgląd, „196” odrzucone, brak pola „Pochówek”; poprawa pokazuje datę pochówku z modelu) | ISSUE-012 stop #2, kroki 2, 4, 7; decyzja D7 |
| AC-4 źródło i status | `graves_test.dart` (dokładnie jedno twierdzenie `notes`/`claimed` na każdą datę i pochówek; linia źródła „kim była”) · `grave_screens_test.dart` · `claims_test.dart` (ISSUE-011) | ISSUE-012 stop #2, krok 2 (linia źródła); twierdzenia sprawdził agent (ISSUE-011 stop #2, ISSUE-012 *Dev report*) |
| AC-5 grób bez adresu i pinezki | `graves_test.dart` · `grave_screens_test.dart` („Bez adresu kwatery · bez pinezki” na cmentarzu i w grobie) | ISSUE-012 stop #2, kroki 3 i 6 |

**Werdykt: APPROVED** z uwagami — dla AC-3 w brzmieniu po D7 (wpisanym w tej samej paczce). Gdyby autor chciał pole
„Pochówek” z powrotem, werdykt zmienia się na CHANGES_REQUESTED; naprawa to jedno pole daty i test.

**Czego szukano i nie znaleziono:** AC bez testu happy-path; testów pominiętych i zawieszenia przebiegu; zapisu daty
albo pochówku bez twierdzenia; zapisu częściowego; pola „Pochówek” po D7 i utraty istniejącej daty pochówku przy
poprawie; baz, kopii, eksportów, zdjęć i logów w zmianach; prawdziwych osób w testach i danych debug (bez porównania z
notatkami — `family_data_dir` nieczytany).

**Uwagi, które nie blokują:**
1. Dopiski „przed” i „po” nie przechodzą przez formularz w żadnym teście (jest test formatu; zapis po nazwie
   `textEnum`). Tania poprawka: test widżetu z każdym z pięciu dopisków.
2. **Czy notatki podają daty pochówku — niesprawdzone.** D7 to decyzja autora („zbędne”), a nie wynik przeglądu
   notatek. *Obali:* pierwszy wpis z datą pochówku przy przepisywaniu ([[NT-002-transcribe-the-notes]]) — pole wraca.
3. [[FR-004-data-z-dopiskiem]] wymienia pochówek, a po D7 żadna US nie daje drogi wpisania tej daty — datowana linia
   w FR-004, żeby werdykt EPIC-001 nie liczył jej jako pokrytej.
4. Odpowiedź „a cała reszta ok”: stan urządzenia potwierdza kroki 2 i 4–6; dopiski i kroki 7–8 pokrywają testy.
5. Tempo (G6) znane tylko z odczucia autora na wymyślonych osobach (7 akcji na osobę); pomiar na notatkach — NT-002.
6. Na urządzeniu migracja v1→v3; krok v2→v3 i odtworzenie kopii v1 tylko na hoście.
