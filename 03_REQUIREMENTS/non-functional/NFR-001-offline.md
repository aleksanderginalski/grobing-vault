---
title: "NFR-001 — Every visit-journey step works without signal"
type: non-functional-requirement
status: draft
epic: ["[[EPIC-002-wizyta]]"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §5 M7 · §4a branch 'weak or no signal' · §3b H9 · MD2 (NFR example) · Step 0 (local-first)"
created: 2026-10-05
updated: 2026-10-08
---

# NFR-001 — Offline

## Requirement
Każdy krok ścieżki wizyty (UJ-001, brief §4a) działa **w trybie samolotowym** — na cmentarzu zasięg bywa
słaby albo żaden, a ścieżka, która go potrzebuje, zawodzi dokładnie tam, gdzie jest używana.

| | |
|---|---|
| **Metric** | liczba kroków UJ-001, które przechodzą w trybie samolotowym |
| **Target** | **wszystkie kroki** UJ-001 (brief: kroki 2-7 muszą działać bez zasięgu; AC-3c ISSUE-001: każdy krok) |
| **Method** | ręczna weryfikacja w telefonie z włączonym trybem samolotowym (stop #2); na miejscu — przy wizycie na cmentarzu (H9 testowane razem z H3) |
| **Verification trigger** | każda pozycja dotykająca ekranu wizyty · każda wizyta na cmentarzu |

## Notes
- Baza w telefonie jest źródłem prawdy, sieć jest opcjonalna ([[ADR-001-local-first]]).
- **Mapy offline zależą od warunków dostawcy**, nie od frameworka — publiczne kafelki OSM zabraniają
  użycia offline (brief §6 N5) → [[SPIKE-001-map-source-offline]], [[ADR-003-map-source-offline]].
- ✅ **Krok 1 offline — rozstrzygnięte 2026-10-06** ([[ADR-007-poland-map-bundled-data]]): mapa Polski działa
  bez zasięgu z danych wbudowanych w aplikację (Natural Earth). Sprawdzone na emulatorze w trybie
  samolotowym ([[ISSUE-014-home-map-of-poland]], stop #2). Kroki 2–7 dalej czekają na
  [[SPIKE-001-map-source-offline]] / [[ADR-003-map-source-offline]].
- Link do Grobonetu (krok 2) z natury wymaga sieci — to zewnętrzna strona w przeglądarce; brak zasięgu
  nie może blokować reszty kroku.
- ✅ **Kroki 2–7 mają źródło mapy — 2026-10-08** ([[ADR-003-map-source-offline]], [[SPIKE-001-map-source-offline]]):
  - **plan schematyczny** cmentarza (obrys i alejki z OSM) pobiera się raz, przy dodaniu cmentarza, i działa
    offline. Kwatery i pinezki to dane autora w bazie. Prototyp pokazał plan i zdjęcie w trybie samolotowym
    na emulatorze (M7, M11);
  - **zdjęcie z góry (ortofotomapa)** jest świadomie tylko online (decyzja autora). Na cmentarzu bez zasięgu go nie
    ma, a plan i GPS działają.

  Sprawdzenie na miejscu (H9 razem z H3) → `CURRENT_STATE.md` → §Parked.
