---
title: "ISSUE-034 — Tree presentation mode for a TV: landscape, full screen, level 2 fitted, no buttons; the TV icon in the tree's bar; the system „Przesyłaj ekran” sends the picture"
type: issue
status: ready
delivery-style: task-level
priority: MUST
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-009-drzewo-od-osoby]]"
depends-on: "[[ISSUE-033-tree-from-a-person]]"
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "rozpisanie US-009 (`docs` w auto-flow po `pm` i `ui`, autor: „ok”, 2026-10-13) · US-009 AC-8 · [[drzewo]] v1.5 (element 1 — ikona, element 11; D11, D16)"
created: 2026-10-13
updated: 2026-10-13
---

# ISSUE-034 — Tryb prezentacji drzewa

> Z rozpisania [[US-009-drzewo-od-osoby]] (`docs` w auto-flow, 2026-10-13). Druga z dwóch pozycji US-009 — buduje się na drzewie z
> [[ISSUE-033-tree-from-a-person]]. Podział zaproponował łańcuch, nie autor, więc na stopie #1 ISSUE-033 autor może go zmienić.

## What to build
1. **Ikona „Tryb prezentacji”** w pasku drzewa ([[drzewo]] element 1): `tv_outlined`, akcent, `tooltip`, cel 48 dp; bez niej w stanach bez
   drzewa.
2. **Tryb prezentacji** ([[drzewo]] element 11, D11, D16): poziomo, pełny ekran, poziom 2 dopasowany do ekranu, bez przycisków;
   podpowiedź o „Przesyłaj ekran” przy wejściu; dotknięcie osoby — ona w środku; dotknięcie pustego miejsca — na 3 s „Zakończ
   prezentację”; wstecz też kończy; po wyjściu orientacja i paski systemu wracają.
3. **Bez Google Cast i bez kodu sieciowego** — obraz na telewizor daje systemowe „Przesyłaj ekran” ([[NFR-005-dane-nie-opuszczaja-telefonu]]).

## Acceptance Criteria
- [ ] **US-009 AC-8 — tryb prezentacji.** *When* włączam tryb prezentacji *Then* drzewo jest poziomo, na pełnym ekranie, na poziomie 2, bez
      przycisków; obraz na telewizor daje systemowe „Przesyłaj ekran”.
- [ ] Wyjście (dotknięcie pustego miejsca → „Zakończ prezentację”, albo wstecz) przywraca orientację pionową, paski systemu i tę samą osobę
      w środku.

## Out of scope
- Google Cast i odbiornik na telewizorze ([[drzewo]] D11 — kod sieciowy i dane rodziny w sieci lokalnej).
- Oddalanie w trybie prezentacji (D16: poziom stały).
- Sprawdzenie z telewizorem autora („Przesyłaj ekran”, D11 → *Obali*) — tylko na telefonie → [[ISSUE-032-mvp-install]] → *Hand checks*.

## Notes
- Zależy od [[ISSUE-033-tree-from-a-person]] (ekran drzewa, układ, dopasowanie poziomu do ekranu).
- Emulator nie przesyła obrazu na telewizor; orientację, pełny ekran i wyjście sprawdzi agent na emulatorze.
