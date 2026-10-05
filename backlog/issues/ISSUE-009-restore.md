---
title: "ISSUE-009 — Restore from the backup file on a fresh install, validated before any overwrite"
type: issue
status: ready
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-001-kopia-z-odtworzeniem]]"
ideal_days: 1
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
created: 2026-10-05
updated: 2026-10-05
---

# ISSUE-009 — Kopia: odtworzenie

> [[ADR-004-backup-format-encryption-destination]] pkt 5-6 i uwagi `qa` ze
> [[SPIKE-003-backup-and-restore]] → *Verification*. **Odtworzenie = plik klucza + hasło + plik kopii.**

## What to build
1. **Odtworzenie na świeżej instalacji:** wybór pliku kopii i pliku klucza systemowym oknem otwarcia
   pliku, hasło, potem walidacja, migracje i podmiana danych.
2. **Walidacja przed nadpisaniem czegokolwiek (ADR-004 pkt 6):**
   - odszyfrowanie do katalogu tymczasowego;
   - `tar` tylko ze zwykłymi plikami i bezpiecznymi ścieżkami;
   - lista plików i SHA-256 zgodne z manifestem;
   - `PRAGMA integrity_check`;
   - `user_version` = manifest;
   - liczby rekordów zgodne, także po migracji.
3. **Kopia ze starszego schematu** przechodzi zwykłe migracje aplikacji, a z nowszego jest odrzucana z
   prośbą o aktualizację (ADR-004 pkt 5, [[NFR-003-migracje-schematu]]).
4. **Z uwag `qa` (SPIKE-003):**
   - odzyskanie stanu po awarii w trakcie podmiany (dwa `rename` nie są atomowe) przy następnym starcie;
   - limit rozmiaru i sprawdzenie wolnego miejsca **przed** rozpakowaniem;
   - instrukcja w aplikacji: na świeżym telefonie folder Dysku w oknie systemowym bywa pusty, a pliki
     znajduje wyszukiwarka okna.

## Acceptance Criteria
- [ ] Na `Grobing_Restore` odtworzenie kopii z Dysku daje odcisk danych identyczny ze źródłem
      ([[NFR-002-odtworzenie-na-nowym-telefonie]]).
- [ ] Złe hasło, uszkodzony plik, `tar` z niebezpieczną ścieżką, niezgodny manifest i kopia z nowszego
      schematu kończą się odmową z czytelnym komunikatem, a dane w telefonie zostają nietknięte.
- [ ] Ścieżka kopii ze starszego schematu sprawdzona testem (jak krok 5 spike'a: syntetyczna v2).
- [ ] Przerwanie w trakcie podmiany → przy następnym starcie aplikacja ma spójne dane: stare albo
      nowe, nigdy żadnych.
- [ ] Kopia większa niż limit albo brak miejsca → odmowa przed rozpakowaniem.

## Out of Scope
- Zapis kopii → [[ISSUE-008-backup-write]].
- Scalanie kopii z danymi już obecnymi w telefonie. Odtworzenie zastępuje dane. Jak chronić telefon,
  który już ma dane (np. wyraźne ostrzeżenie), ustala `planning`.

## Technical Notes
- **Stop #2 tym razem nie pomijać** (uwaga `qa` ze SPIKE-003): pierwsze odtworzenie, które obejrzy
  człowiek, wypada tutaj. W spike'u złe hasło na drugim urządzeniu nie było sprawdzone.

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-008-backup-write]] | technical | `ready` |
| emulator `Grobing_Restore` | technical | istnieje (SPIKE-003) |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC · ręczna weryfikacja na
emulatorze (dwa urządzenia) · próbne odtworzenie przechodzi · zero danych rodziny w zmianach · INVEST
self-check. Po przyjęciu tego ISSUE [[US-001-kopia-z-odtworzeniem]] może przejść do zamknięcia.
