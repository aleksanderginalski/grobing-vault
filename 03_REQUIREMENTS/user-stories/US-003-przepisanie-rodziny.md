---
title: "US-003 — Enter a whole family at once (przepisanie rodziny)"
type: user-story
status: ready
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M1]
journey-steps: "n/a — poza ścieżką (M1, warunek kroku 1 UJ-001)"
FR: ["[[FR-001-provenance]]", "[[FR-002-rodzina-jako-rekord]]", "[[FR-004-data-z-dopiskiem]]"]
NFR: ["[[NFR-003-migracje-schematu]]"]
issues: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §5 M1 · §5a G6 · Step 0 (family group sheet) · data-model.md (Family)"
created: 2026-10-05
updated: 2026-10-05
---

# US-003 — Przepisanie rodziny naraz

## Story
**Jako** Zbierający **chcę** wpisać parę i jej dzieci jednym formularzem, **żeby** przepisanie ok. 100
osób z notatek było szybkie (G6), a relacje wynikały z rodzin, nie z pojedynczych powiązań.

## Acceptance Criteria
- **AC-1 — rodzina jednym formularzem.** *When* wpisuję rodzinę *Then* w jednym przebiegu podaję 1-2
  partnerów i dzieci, a nowe osoby powstają przy okazji ([[FR-002-rodzina-jako-rekord]]).
- **AC-2 — powtórne małżeństwo.** *Given* osoba jest już partnerem w jednej rodzinie *When* dodaję drugą
  rodzinę z tą samą osobą *Then* obie rodziny istnieją, a dzieci należą do właściwej pary.
- **AC-3 — małżeństwo z datą z dopiskiem.** *When* wpisuję datę małżeństwa albo końca rodziny *Then* mogę
  użyć kwalifikatora ([[FR-004-data-z-dopiskiem]]).
- **AC-4 — źródło przy relacjach.** *When* zapisuję rodzinę *Then* przynależność partnerów i dzieci ma
  źródło (domyślnie „notatki") i status ([[FR-001-provenance]]).
- **AC-5 — osoba z grobu w rodzinie.** *Given* osoba wpisana przy grobie ([[US-002-przepisanie-grobu]])
  *When* tworzę rodzinę *Then* mogę wskazać tę osobę zamiast tworzyć ją drugi raz.

## Out of scope
- Widok drzewa i ścieżka pokrewieństwa → [[EPIC-003-zrozumienie]] (kształt po [[SPIKE-002-tree-on-a-phone]]).
- Wskazanie „ja" → widok osoby, [[EPIC-002-wizyta]] (M5).
- Sprzeczne twierdzenia o relacji → [[US-004-fakt-od-babci]].

## Notes
- Szybkość wprowadzania (G6) brief zostawił projektowi wprowadzania. Formularz zaprojektuje agent `ui`
  przy pierwszym ekranie (trigger z `CLAUDE.md`; styl B potrzebuje wytycznych [[NT-006-visual-guidelines]]).
