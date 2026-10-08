---
title: "US-007 — Cemetery as a map: schematic plan offline, photo from above online, the author's quarters, candles (mapa cmentarza)"
type: user-story
status: ready
epic: "[[EPIC-002-wizyta]]"
persona: "[[P1-zbierajacy]]"
moscow: [M3, M7]
journey-steps: "UJ-001 · 2, 7 (widok 2, R2)"
FR: []
NFR: ["[[NFR-001-offline]]", "[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
issues: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[SPIKE-004-mvp-flow-prototype]] D8–D12 · [[ADR-003-map-source-offline]] · [[cmentarz]] v4.1 · EPIC-002 → Input from SPIKE-001"
created: 2026-10-08
updated: 2026-10-08
---

# US-007 — Mapa cmentarza

## Story
**Jako** Zbierający **chcę** widzieć cmentarz jako plan z kwaterami i zniczami grobów, także bez zasięgu, **żeby** znaleźć
grób rodziny bez papierowych notatek i bez planu przy bramie.

## Acceptance Criteria
- **AC-1 — plan offline.** *Given* cmentarz dodany z siecią *When* otwieram go w trybie samolotowym *Then* widzę plan
  schematyczny (obrys, alejki z OSM) z „Plan offline” i „© OpenStreetMap” ([[ADR-003-map-source-offline]] pkt 1).
- **AC-2 — zdjęcie z góry online.** *When* przełączam na „Zdjęcie” z siecią *Then* widzę ortofotomapę GUGiK; bez sieci —
  „bez internetu”, a plan działa; nic nie zapisuje się w telefonie (pkt 2).
- **AC-3 — sama mapa, jeden grób, lista.** *Given* groby z pinezką i bez *Then* na starcie jest sama mapa i pasek grobów
  z liczbą grobów bez pinezki; znicz → arkusz grobu z „Pokaż grób”; przeciągnięcie → lista wszystkich grobów
  ([[cmentarz]] stany A, B, C; D11, D14).
- **AC-4 — kwatery autora.** *Given* kwatera zaznaczona przez autora *Then* plan pokazuje ją przerywaną linią z nazwą;
  kwatera bez strefy jest tylko w adresach ([[cmentarz]] D13).
- **AC-5 — bez planu.** *Given* cmentarz dodany bez sieci *Then* jest zaślepka „pobierze się, gdy będzie internet” i
  „Pobierz teraz”, a lista grobów działa.

## Out of scope
- Pinezka z GPS na miejscu, „gdzie jestem” → [[US-008-pinezka-na-miejscu]].
- Link do Grobonetu i wyszukiwarki zarządcy — wycofany (SPIKE-004 D10).

## Notes
- **Do zaprojektowania przed planem (`ui`):** jak autor **zaznacza kwaterę** na planie albo zdjęciu z góry — SPIKE-004
  tego nie pokazał ([[cmentarz]] → *Navigation*).
- **Uprawnienie `INTERNET`** wchodzi z tą US — tylko do pobrania planu i zdjęcia z góry ([[ADR-003-map-source-offline]]
  pkt 4).
