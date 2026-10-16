---
title: "US-006 — Data that outlives the app: the backup's open inside is the export (dane do wyjęcia poza aplikację)"
type: user-story
status: done
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M8]
journey-steps: "n/a — poza ścieżką (M8)"
FR: []
NFR: ["[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
ADR: ["[[ADR-018-export-is-the-backup]]", "[[ADR-004-backup-format-encryption-destination]]"]
issues: ["[[ISSUE-040-export-is-the-backup]]"]
quality-verdict: APPROVED
verdict-date: 2026-10-16
verdict-reviewer: self-check
source: "PROJECT_BRIEF §5 M8 · decyzja autora 2026-10-16 ([[ADR-018-export-is-the-backup]]) · `04_ARCHITECTURE/backup-format.md`"
created: 2026-10-05
updated: 2026-10-16
---

# US-006 — Dane do wyjęcia poza aplikację

> **Przepisana 2026-10-16** (decyzja autora, [[ADR-018-export-is-the-backup]]). Do tego dnia: „Eksport dla rodziny” — HTML i PDF czytelne bez
> aplikacji, ze znakami specjalnymi jako tekst i zapisem tylko tam, gdzie autor wskaże (AC-1–AC-3 z kick-offu). Autor przy planowaniu: *„nie
> zależy mi na estetyce, a na zachowaniu danych”* — eksportem jest kopia.

## Story
**Jako** Zbierający **chcę** móc wyjąć wszystkie dane poza aplikację w otwartym, opisanym formacie, **żeby** przeżyły aplikację i żebym mógł
kiedyś użyć ich w innym produkcie.

## Acceptance Criteria
- **AC-1 — dane poza aplikacją.** *Given* kopia zrobiona aplikacją *When* odszyfrowana na PC oficjalnym `age` i rozpakowana zwykłym `tar` *Then*
  są baza SQLite, zdjęcia i manifest; baza jest spójna, a liczby rekordów, rozmiary i sumy SHA-256 zgadzają się z manifestem — sprawdzone bez
  kodu Grobing.
- **AC-2 — opis bez Grobing.** *Then* każda tabela bazy z kopii ma opis w `04_ARCHITECTURE/` (`data-model.md`, `backup-format.md`).
- **AC-3 — bez osobnego eksportu.** Aplikacja nie ma drugiej drogi wyjścia danych poza kopią ([[NFR-005-dane-nie-opuszczaja-telefonu]]).

## Out of scope
- Eksport HTML i PDF dla rodziny — wycofany ([[ADR-018-export-is-the-backup]]).
- GEDCOM 7 (C2) — gdy pojawi się konkretny produkt docelowy.
- Notka przekazania dla rodziny → [[NT-007-hand-over-note]] (poza kodem).

## Notes
- `persons.is_living` niczym już nie steruje (sterowało prywatnością eksportu) — zostaje w schemacie bez zmian ([[ADR-018-export-is-the-backup]]).
- Rodzina bez autora otwiera dane drogą kopii: plik kopii + plik klucza + hasło + `age` ([[NT-007-hand-over-note]], `backup-format.md`).
