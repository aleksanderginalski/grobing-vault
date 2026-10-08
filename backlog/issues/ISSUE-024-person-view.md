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
> [[grob]] v5, [[wpis-osoby]] v5.3, [[style-b]] reguła 15. Wymaga [[ISSUE-025-gender-kinship-together-since]] (płeć — zrobione)
> i [[ISSUE-022-app-skeleton-tabs-people-settings]] (pasek, „ja”). **Od zamknięcia ISSUE-025 ta pozycja buduje też słownik
> nazw pokrewieństwa i ścieżkę do „ja”** (decyzja autora na stopie #1 ISSUE-025, R2-D3 — *Input from ISSUE-025* niżej).

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
- **AC-6** (z ISSUE-025, dawne AC-2) *Given* ścieżka Ja → rodzic (mężczyzna) → jego rodzic → jego córka *Then* nazwa to
  „ciotka”; brat ojca — „stryj”, brat matki — „wuj”; dziecko siostry ojca — „brat/siostra cioteczna” (słownik ze źródłem).

## Notes
- Mini-drzewo dzieli układ i kolory linii z [[drzewo]] (D3) — w tej pozycji tylko jeden poziom (rodzice, partnerzy,
  dzieci).

## Input from ISSUE-025 (2026-10-08, `docs` przy zamknięciu)
- **Słownik i ścieżka** („Jak łączy się ze mną”, [[osoba]] element 7): kanon zacytowany w [[ISSUE-025-gender-kinship-together-since]]
  → *Prior art* (SJPD przez Frąckiewicz 2013, SJP PWN, GEDCOM 7), a zakres nazw, nawias ze ścieżką, opis z odcinków w
  dopełniaczu i odcinki neutralne przy braku płci — tabela D2 w *Decisions for stop #1 — runda 0*. Reguły nawiasu i opisu
  neutralnego (dawne [[osoby]] D8, D9) przechodzą tu; lista Osoby pokrewieństwa nie pokazuje (decyzja autora, [[osoby]] v2.2).
- **Uwaga autora ze stopu #2 ISSUE-025:** *„po wybraniu osoby najpierw wejść w jej »profil« z najważniejszymi informacjami a
  dopiero potem w edycję (aby oglądanie danej osoby nie mieszało się z edycją tej osoby)”* — to AC-1 i reguła 15: także
  **karta partnera i chipy w sekcji „Rodzina”** ([[wpis-osoby]] 9a v5.6) mają prowadzić do widoku osoby, a nie do poprawy.
- **Karta partnera:** dziś inicjały (ISSUE-025, odstępstwo 1 przyjęte w przeglądzie `ui`) — tu profilowe, skoro widok i tak
  czyta zdjęcia; chevron przy karcie, gdy zacznie prowadzić do widoku osoby (przegląd `ui`, znalezisko 6).
- **Stare `⚠️ OPEN` w [[osoba]]** (3 — źródło przy relacjach, 4 — ustawienie „ja”) są rozstrzygnięte (SPIKE-004 D28,
  ISSUE-022) — `ui` sprząta je przed planem.
