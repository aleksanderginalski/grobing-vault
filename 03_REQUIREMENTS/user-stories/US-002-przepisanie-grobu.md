---
title: "US-002 — Transcribe a grave from the notes (przepisanie grobu)"
type: user-story
status: in-progress
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M1]
journey-steps: "n/a — poza ścieżką (M1, warunek kroku 1 UJ-001)"
FR: ["[[FR-001-provenance]]", "[[FR-003-wiele-osob-w-grobie]]", "[[FR-004-data-z-dopiskiem]]", "[[FR-005-nazwisko-rodowe]]"]
NFR: ["[[NFR-003-migracje-schematu]]"]
issues: ["[[ISSUE-011-schema-v2-assertions]]", "[[ISSUE-014-home-map-of-poland]]", "[[ISSUE-015-add-cemetery-from-database]]", "[[ISSUE-012-transcribe-grave-screen]]"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §5 M1 · data-model.md (Cemetery, Grave, Burial, Person, Event, Assertion)"
created: 2026-10-05
updated: 2026-10-06
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
- **AC-3 — data z dopiskiem.** *When* wpisuję datę urodzenia, zgonu albo pochówku *Then* mogę wybrać
  dokładnie / około / przed / po / między, a aplikacja pokazuje datę z dopiskiem
  ([[FR-004-data-z-dopiskiem]]).
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
