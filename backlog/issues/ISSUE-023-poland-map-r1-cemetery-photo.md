---
title: "ISSUE-023 — Map of Poland like R1 (neighbours, Baltic, lakes, centred) and the cemetery photo in the sheet"
type: issue
status: ready
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[SPIKE-004-mvp-flow-prototype]] D5, D6, D7 (decyzje autora na prototypie, 2026-10-08)"
created: 2026-10-08
updated: 2026-10-08
---

# ISSUE-023 — Mapa Polski jak R1 i zdjęcie cmentarza

> Z zamknięcia [[SPIKE-004-mvp-flow-prototype]]. Specyfikacja: [[cmentarze]] v2.4 (elementy 3, 6a; D28–D30),
> [[style-b]] v1.13 (rola wody, reguła 13 i 14).

## What to build
- **Mapa jak R1** (D6, [[cmentarze]] element 3, D29): sąsiednie kraje w kolorze tła, Bałtyk i jeziora w kolorze wody,
  rzeki linią wody, granica Polski w kolorze tekstu pomocniczego, napis „Polska”, 11 miast (+ Bydgoszcz, Katowice).
  Dane: Natural Earth 1:10m — rozszerzenie `tool/map/extract_poland.dart` i `assets/map/poland.json` (plus
  `ne_10m_lakes`, `ne_10m_lakes_europe`). Tokeny `water` i `waterLine` w `theme.dart`. Bez faktury terenu.
- **Wyśrodkowanie** (D7, D30): bez arkusza Polska na środku obszaru mapy; po otwarciu arkusza mapa przesuwa się płynnie
  nad arkusz.
- **Zdjęcie cmentarza w arkuszu** (D5, [[cmentarze]] element 6a, D28): miniatura 96 × 80 dp z lewej; bez zdjęcia pole
  „Dodaj zdjęcie”; podgląd ze „Zmień zdjęcie” i „Usuń zdjęcie” jak przy nagrobku ([[zdjecie]]). **Zmiana schematu:**
  zdjęcie cmentarza (jak zdjęcie grobu — wiersz `Media` z odwołaniem do cmentarza), migracja z testem, kopia po migracji.

## Acceptance Criteria
- **AC-1** *Given* ekran główny *Then* widać sąsiednie kraje, Bałtyk, jeziora, napis „Polska” i 11 miast; bez sieci.
- **AC-2** *When* dotykam znicza *Then* mapa przesuwa się nad arkusz; *When* zamykam arkusz *Then* Polska wraca na środek.
- **AC-3** *Given* cmentarz bez zdjęcia *When* dodaję zdjęcie *Then* arkusz pokazuje miniaturę; podgląd pozwala ją zmienić
  i usunąć.
- **AC-4** *Given* kopia sprzed zmiany schematu *When* odtwarzam ją *Then* dane są pełne, a cmentarze bez zdjęć.

## Notes
- **Zmiana zakresu:** zdjęcie cmentarza nie było w briefie (M1 ma zdjęcie nagrobka) — decyzja autora (D5).
