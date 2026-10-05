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
updated: 2026-10-05
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
- ⚠️ **OPEN — krok 1 offline:** cel „wszystkie kroki" obejmuje mapę Polski (krok 1), a
  [[SPIKE-001-map-source-offline]] / [[ADR-003-map-source-offline]] pytają tylko o ~10 obszarów wielkości
  cmentarza. Brief §4a wymaga bez zasięgu kroków 2-7; czy krok 1 musi działać offline (wybór, dokąd jechać)
  — do rozstrzygnięcia przy planowaniu SPIKE-001.
- Link do Grobonetu (krok 2) z natury wymaga sieci — to zewnętrzna strona w przeglądarce; brak zasięgu
  nie może blokować reszty kroku.
