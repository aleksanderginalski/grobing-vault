---
title: "ISSUE-012 — Screen: transcribe a grave from the notes (cemetery → grave → persons)"
type: issue
status: ready
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-002-przepisanie-grobu]]"
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
created: 2026-10-06
updated: 2026-10-06
---

# ISSUE-012 — Ekran przepisania grobu

> Z rozpisania [[US-002-przepisanie-grobu]] (decyzja autora 2026-10-06, po `pm`): ekran po schemacie
> ([[ISSUE-011-schema-v2-assertions]]). To **pierwszy ekran do wpisywania danych**, czyli sygnał dla
> agenta `ui` (`CLAUDE.md` → *Na sygnał*) i warunek obudzenia [[NT-006-visual-guidelines]].

## What to build
1. **Cmentarz:** wybór istniejącego albo dodanie nowego (nazwa, miejscowość).
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
- [ ] Ekran stosuje wytyczne stylu B z [[NT-006-visual-guidelines]].
- [ ] Zapis z ekranu zamawia kopię w tle tak samo jak każdy zapis danych ([[ISSUE-010-background-backup]]).

## Out of Scope
- Rodzice, małżeństwa, dzieci → [[US-003-przepisanie-rodziny]].
- Drugie, sprzeczne twierdzenie → [[US-004-fakt-od-babci]].
- Zdjęcia nagrobka i osoby → [[US-005-zdjecia]].
- Pinezka i jej poprawa na miejscu → [[EPIC-002-wizyta]] (M6).
- **Poprawianie i usuwanie wpisu:** US-002 ich nie wymienia. `planning` ustala, czy wchodzi minimum
  (poprawa literówki przy przepisywaniu), i mówi to na stopie #1. Bez tego zakres się nie poszerza.

## Technical Notes
- **Tempo przepisywania** to miara ekranu: około 100 osób i 50 grobów całymi wpisami
  ([[NT-002-transcribe-the-notes]], G6). Każde dodatkowe pytanie na osobę mnoży się przez 100.
- **Czytelność w słońcu** ([[NT-006-visual-guidelines]]) do MVP sprawdza się na emulatorze. Słońce to
  wyjątek z `DEFINITION_OF_DONE.md`, sprawdzany na telefonie w buildzie release.
- Folder `05_DESIGN/` (oraz `05_DESIGN/brand/` dla stylu B) powstaje na ten sygnał według `doc-growth.md`,
  z wierszem w DOC_MAP. Zakłada go `docs`, kiedy praca nad ekranem albo NT-006 go potrzebuje.
- Sprawdzić, czy zamówienie kopii przy zapisie (ISSUE-010) obejmuje zapisy z nowego ekranu, a nie tylko
  drogi istniejące w chwili ISSUE-010.
- Dane do pokazania i testów są wymyślone i istnieją tylko w buildzie debug ([[ISSUE-007-data-layer]]).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-011-schema-v2-assertions]] (twierdzenia w schemacie) | technical | `ready` |
| [[NT-006-visual-guidelines]] (wytyczne stylu B) | design | `open` — ten ekran go budzi |
| agent `ui` w `grobing-agents` | process | nie istnieje — ten ekran to jego sygnał |
| [[ISSUE-010-background-backup]] (kopia zamawiana przy zapisie) | technical | `done` |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC · ręczna weryfikacja na
emulatorze · fakt o rodzinie → źródło i status zapisane · dotyka warstwy danych → próbne odtworzenie z
kopii przechodzi (wpisy z ekranu wracają z odciskiem zgodnym) · zero danych rodziny w zmianach · INVEST
self-check. Po przyjęciu tego ISSUE US-002 idzie do werdyktu US.
