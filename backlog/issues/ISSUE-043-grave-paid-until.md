---
title: "ISSUE-043 — Grave fee „paid until” at the bottom of the grave view (brief S4)"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "brief §5 S4 (G4) · propozycja `pm` w `/pm` 2026-10-16, autor: „to jest dobre — można dodać na samym dole profilu grobu” · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-16
---

# ISSUE-043 — „Opłacone do” przy grobie

> Brief §5 S4: *grave fee „paid until” date + reminder* — grób ziemny bez odnowionej opłaty (co 20 lat) zarządca może zlikwidować; to jedyny
> sposób, żeby stracić **sam grób**, a nie wiedzę o nim. Warunek z briefu („przed najwcześniejszą zapisaną datą”) da się spełnić tylko, gdy daty
> są zapisane — Wszystkie Święte to okazja: naklejki z opłatą na grobach, otwarte biuro zarządcy. Autor: *„można dodać na samym dole profilu
> grobu”*. **Przed instalacją**, bo zmienia bazę.

## What to build
- W widoku grobu, **na samym dole**: „Opłacone do” — data (zwykle sam rok) albo „nie wiadomo”; poprawa tam, gdzie dziś „Popraw grób”
  (projekt: `ui`, zmiana specyfikacji [[grob]]).
- Kolumna w `graves` — dziś jej nie ma (`database.dart`: „still without the grave fee (S4)”), choć [[data-model]] wymienia ją w *Grave*.
- `⚠️ OPEN` na stop #1:
  1. **przypomnienie** (brief: „+ reminder”) — powiadomienie wymaga na Androidzie 13 uprawnienia `POST_NOTIFICATIONS`; z nim czy bez?
  2. **kto płaci** — brief: „who pays is recorded, not managed”; pole tekstowe czy bez?

## Acceptance Criteria
- **AC-1** *Given* grób *When* wpisuję „opłacone do 2031” *Then* na dole profilu grobu widać „Opłacone do 2031”.
- **AC-2** *Given* grób bez wpisu *Then* dół profilu nie udaje daty (stan „nie wiadomo” albo brak wiersza — decyzja `ui`).
- **AC-3** *Given* kopia z wersji sprzed tej pozycji *When* odtwarzam ją w nowej *Then* dane są kompletne (test migracji, próbne odtworzenie).

## Notes
- [[EPIC-002-wizyta]] (UJ-001 krok 4 — grób). Przypomnienie, jeśli wejdzie: dopiero po decyzji o uprawnieniu.
