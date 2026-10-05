---
title: "NFR-003 — A schema change ships with a migration tested from the previous version"
type: non-functional-requirement
status: draft
epic: ["[[EPIC-001-zabezpiecz-i-przepisz]]", "[[EPIC-002-wizyta]]", "[[EPIC-003-zrozumienie]]"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §Architecture → Sufficiency pass A1 · DoD ISSUE"
created: 2026-10-05
updated: 2026-10-05
---

# NFR-003 — Migracje schematu

## Requirement
Każda zmiana schematu bazy wychodzi **z migracją przetestowaną z poprzedniej wersji**. Dane są
niezastępowalne i będą żyć latami — aktualizacja aplikacji ze złą migracją **jest** utratą danych (A1).

| | |
|---|---|
| **Metric** | zmiany schematu bez testu migracji z poprzedniej wersji |
| **Target** | **zero** |
| **Method** | test migracji (`qa`): baza poprzedniej wersji z **wymyślonymi** danymi → migracja → dane kompletne |
| **Verification trigger** | każda pozycja zmieniająca schemat (linia DoD ISSUE) |

## Notes
- Dotyczy każdego EPIC-a, który dokłada pole albo encję — stąd trzy EPIC-i w `epic:`.
- Razem z [[NFR-002-odtworzenie-na-nowym-telefonie]]: kopia sprzed migracji musi dać się odtworzyć w
  nowej wersji. ✅ **Rozstrzygnięte 2026-10-05** ([[ADR-004-backup-format-encryption-destination]], pkt 5;
  zmierzone w [[SPIKE-003-backup-and-restore]], krok 5): odtworzenie przepuszcza starszą kopię przez
  **zwykłe migracje** aplikacji, a kopię z nowszego schematu odrzuca. Wynika z tego, że **test migracji
  z tej NFR obejmuje też odtworzenie kopii**: ta sama ścieżka kodu.
