---
title: "ISSUE-048 — The portrait is the place for photos: tap to change the profile photo or add photos (absorbs ISSUE-026)"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "`/pm` 2026-10-18 — autor przeszedł cały przepływ na emulatorze (dane demo), punkt 4 z 7; wchłania [[ISSUE-026-link-existing-photo-to-person]] (decyzja `pm`, autor: „Do twojej decyzji ile tych zadań”)"
created: 2026-10-18
updated: 2026-10-18
---

# ISSUE-048 — Portret jako miejsce na zdjęcia

> Autor: *„gdy klikam na kogoś „zdjęcie profilowe”, chciałbym od razu widzieć tam możliwość jego zmiany (lub dodania dla tej osoby nowych zdjęć —
> podobnie jak działa zdjęcie w tle)”*.

## What to build
- **Dotknięcie portretu** w widoku osoby ([[osoba]] el. 3) — dziś podgląd w trybie oglądania, a profilowe zmienia się pod ✎ — prowadzi od razu do:
  obejrzyj · zmień profilowe · dodaj zdjęcia. Wzór: tło ([[osoba]] D21 — dotknięcie → wybór, zapis od razu, jak zdjęcie nagrobka w [[grob]]).
- **Okrąg z inicjałami** (osoba bez zdjęć) — dziś bez akcji ([[osoba]] D20) — prowadzi do dodania zdjęcia; pierwsze zdjęcie jest profilowym
  ([[ADR-009-person-photos-record-and-link]]). *Obali* D20 („autor szuka dodania zdjęcia w okręgu portretu”) — trafione.
- **Z [[ISSUE-026-link-existing-photo-to-person]]:** trzecie źródło „Ze zdjęć w aplikacji” (zdjęcie, które już jest u innej osoby, np. grupowe) i
  wybór spośród zdjęć wszystkich osób — szczegóły w ISSUE-026 → *What to build*.
- Projekt: `ui` przed `planning` — zmiana [[osoba]], [[zdjecia-osoby]], [[zdjecie]], [[kadr-profilowego]].

## Acceptance Criteria
- **AC-1** *Given* Jan Wymyślony z profilowym *When* dotykam portretu *Then* od razu widzę, że mogę obejrzeć zdjęcie, zmienić profilowe albo dodać
  zdjęcia — bez ✎.
- **AC-2** *Given* nowe profilowe wybrane z portretu *Then* zapisuje się od razu, jak tło (D21), a widok pokazuje je bez wracania.
- **AC-3** *Given* Maria Zmyślona bez zdjęć *When* dotykam okręgu z inicjałami i dodaję zdjęcie *Then* jest ono jej profilowym.
- **AC-4** (ISSUE-026 AC-1) *Given* zdjęcie grupowe u Marii *When* u Jana wybieram „Ze zdjęć w aplikacji” i to zdjęcie *Then* jest ono u Jana i u
  Marii, a plik jest jeden.
- **AC-5** (ISSUE-026 AC-2) *Given* kilkaset zdjęć w aplikacji *Then* zdjęcie konkretnej osoby da się znaleźć bez przewijania wszystkiego.

## Notes
- **Rozmiar:** AC-4 i AC-5 wnoszą nowy ekran wyboru zdjęć. Gdy przy terminie instalacji (2026-10-29) zabraknie na nie czasu, `planning` pyta autora
  na stopie #1, czy zostają; jeśli wypadną — ISSUE-026 wraca do `ready` (nie giną).
- Bez zmiany schematu (łącze osoba–zdjęcie istnieje od v4, profilowe i kadr — [[kadr-profilowego]]) — do potwierdzenia przez `planning`.
- Z tego samego przeglądu autora: [[ISSUE-047-grave-first-then-people]] · [[ISSUE-049-tree-levels-and-zoom]] · [[ISSUE-050-next-event]].
