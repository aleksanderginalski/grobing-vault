---
title: "ISSUE-024 — Person view (M5): cover photo, portrait, mini family tree, chain to me, dates, burial → cemetery map"
type: issue
status: ready
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[SPIKE-004-mvp-flow-prototype]] D4, D13–D19, D24, D27, D28 (decyzje autora na prototypie, 2026-10-08)"
created: 2026-10-08
updated: 2026-10-08
---

# ISSUE-024 — Widok osoby

> Z zamknięcia [[SPIKE-004-mvp-flow-prototype]]. Nowy ekran (widok 4, M5, R4 prawy). Specyfikacja: [[osoba]] v1.3,
> [[grob]] v5, [[wpis-osoby]] v5.3, [[style-b]] reguła 15. Wymaga [[ISSUE-025-gender-kinship-together-since]] (nazwy
> pokrewieństwa) i [[ISSUE-022-app-skeleton-tabs-people-settings]] (pasek, „ja”).

## What to build
- **Widok osoby** ([[osoba]] elementy 1–10): zdjęcie w tle, portret na jego krawędzi, imię, lata, „kim była”, **Rodzina
  jako mini-drzewo** (rodzice, partnerzy, dzieci), **„Jak łączy się ze mną”** (nazwa pokrewieństwa i łańcuch od „ja”),
  daty, **pochówek → mapa cmentarza z zaznaczoną pinezką** (bez pinezki — lista z zaznaczonym grobem), zdjęcia; ✎ →
  formularz poprawy.
- **Widok przed poprawą** ([[style-b]] reguła 15): karta osoby w [[grob]] i chipy krewnych prowadzą do widoku osoby, nie
  do formularza.
- **Zdjęcie w tle** (D17): „Ustaw jako tło” w podglądzie zdjęcia osoby. **Zmiana schematu:** wskazanie tła przy łączu
  osoba–zdjęcie (jak profilowe, [[ADR-009-person-photos-record-and-link]]), migracja z testem.
- **Bez źródeł na ekranie** (D28): daty bez „· notatki”, bez statusów.

## Acceptance Criteria
- **AC-1** *When* dotykam osoby w grobie *Then* otwiera się widok osoby, a nie formularz; ✎ otwiera poprawę.
- **AC-2** *Given* osoba z rodzicami, partnerem i dziećmi *Then* mini-drzewo pokazuje ich z nazwami („Matka”, „Mąż”,
  „Córka”), a dotknięcie przenosi do widoku krewnego.
- **AC-3** *Given* ustawione „ja” i ścieżka do osoby *Then* widać „Twoja babcia” i łańcuch Ja → Mama Anna → Babcia Maria.
- **AC-4** *When* dotykam „Pochówek” *Then* otwiera się mapa cmentarza z zaznaczoną pinezką tego grobu.
- **AC-5** *When* ustawiam zdjęcie jako tło *Then* widać je nad portretem; kopia sprzed zmiany odtwarza się bez tła.

## Notes
- Mini-drzewo dzieli układ i kolory linii z [[drzewo]] (D3) — w tej pozycji tylko jeden poziom (rodzice, partnerzy,
  dzieci).
