---
title: "ISSUE-035 — Tree: names shrink with the tree when zooming out (I1) and the card speaks in my voice („Moja babcia”, G2)"
type: issue
status: ready
delivery-style: task-level
priority: MUST
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-009-drzewo-od-osoby]]"
depends-on: "[[ISSUE-034-tree-presentation-mode]]"
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "decyzja autora na stopie #1 [[ISSUE-034-tree-presentation-mode]] (2026-10-14: „1 — I1, 2 — Moja babcia”, potem „tak” dla osobnej pozycji) · [[drzewo]] v1.8 *Open* 5 i 6 · *Candidates — US-009* (I1, G2)"
created: 2026-10-14
updated: 2026-10-14
---

# ISSUE-035 — Drzewo: I1 i „Moja”

> Z zamknięcia [[ISSUE-034-tree-presentation-mode]] (`docs`, 2026-10-14). Autor pierwszy raz otworzył makietę `drzewo-us009.html` na stopie #1
> ISSUE-034 (adres `file:///`) i wybrał inaczej niż na stopie #1 [[ISSUE-033-tree-from-a-person]], gdzie „Tak” przyjęło rekomendacje I2 i G1.
> W kodzie są dziś I2 i G1. **Pozycja zmienia ekran → `ui` przed `planning`.**

## What to build
1. **I1 — imiona maleją razem z drzewem** ([[drzewo]] *Candidates — US-009*, I1): przy oddalaniu imię ma wielkość skali drzewa (poziom 3 ok.
   9 sp, poziom 4 ok. 6 sp), zamiast stałych 13 sp z chowaniem nakładających się (I2).
2. **G2 — karta mówi Twoim głosem:** „Moja babcia”, „Siostra cioteczna babci mojej żony” (zamiast „Twoja babcia”, „…Twojej żony”).

## Acceptance Criteria
- [ ] **US-009 AC-3 / [[drzewo]] *Open* 5 — I1.** *When* oddalam drzewo do poziomu 3 i 4 *Then* imiona maleją razem z drzewem i żadne się nie
      chowa.
- [ ] **US-009 AC-5 — G2.** *Given* ścieżka Ja → żona → jej mama → jej mama → jej rodzic → jego rodzeństwo → jego dziecko *Then* karta mówi
      „Siostra cioteczna babci mojej żony”; *Given* mama taty *Then* „Moja babcia”.
- [ ] Przykład w US-009 AC-5 i w [[drzewo]] wraca do „mojej żony”.

## Out of scope
- Mini-drzewo w [[osoba]] (nie ma oddalania).
- Inne miejsca aplikacji, które mówią do Ciebie („Wybierz, która osoba to Ty”, „…łączy się z Tobą”) — czy też się zmieniają, rozstrzyga `ui`
  (pytania niżej); bez decyzji `ui` nic poza kartą drzewa.

## Notes
- **Pytania dla `ui` przed planem:** (a) co zamiast „to Ty” na karcie „ja” i zamiast „nie wiadomo jeszcze, kim jest dla Ciebie”; (b) czy G2 obejmuje
  baner „Połącz dwie osoby” ([[drzewo]] element 9, US-011) i opisy dla czytnika; (c) odstępstwo od progu 13 sp w [[style-b]] reguła 13 przy I1;
  (d) pomiar trybu prezentacji przy tekście 200% na 360 dp (zrzut `18b` ISSUE-034 — [[drzewo]] *Open* 5, v1.8).
- Makieta z kandydatami I1–I3 i G1–G2: `drzewo-us009.html` w katalogu tymczasowym sesji `c3868f5f-…\scratchpad` — podawać autorowi jako
  adres `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/c3868f5f-084e-4101-9b20-5d98d098ca56/scratchpad/drzewo-us009.html`.
- Kod: `lib/app/tree/tree_labels.dart`, `tree_screen.dart` (`_labelScale`, `_visibleNames`), `lib/app/person/kinship_names.dart` (zaimek).
