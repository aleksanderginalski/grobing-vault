---
title: "US-002 — Transcribe a grave from the notes (przepisanie grobu)"
type: user-story
status: draft
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M1]
journey-steps: "n/a — poza ścieżką (M1, warunek kroku 1 UJ-001)"
FR: ["[[FR-001-provenance]]", "[[FR-003-wiele-osob-w-grobie]]", "[[FR-004-data-z-dopiskiem]]", "[[FR-005-nazwisko-rodowe]]"]
NFR: ["[[NFR-003-migracje-schematu]]"]
issues: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §5 M1 · data-model.md (Cemetery, Grave, Burial, Person, Event, Assertion)"
created: 2026-10-05
updated: 2026-10-05
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
  (⚠️ OPEN niżej).

## Out of scope
- Rodzice, małżeństwa, dzieci → [[US-003-przepisanie-rodziny]].
- Drugie, sprzeczne twierdzenie (babcia vs notatki) → [[US-004-fakt-od-babci]].
- Zdjęcia nagrobka i osoby → [[US-005-zdjecia]].
- Pinezka i jej poprawa na miejscu → [[EPIC-002-wizyta]] (M6).

## Open questions
- ⚠️ **OPEN — grób bez adresu kwatery, pinezki i zdjęcia** ([[EPIC-001-zabezpiecz-i-przepisz]] →
  *Open questions*, `TRACEABILITY.md` → *Open gaps* 1). AC-5 to **propozycja do potwierdzenia przez
  autora**: grób z notatek to cmentarz + osoby, a reszta jest opcjonalna i uzupełniana przy wizycie.
  Pytanie, jak taki grób znaleźć na miejscu, należy do EPIC-002 i tej US nie blokuje. **Decyzja autora
  przed planowaniem pierwszego ISSUE tej US** — dlatego `status: draft`.
