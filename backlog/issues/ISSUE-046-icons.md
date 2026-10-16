---
title: "ISSUE-046 — Icons: the launcher icon and the in-app icons, options compared on a mockup"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "`/pm` 2026-10-16 — autor: obecne ikony „wyglądają tak mało ciekawie”; DALL-E (prompty od agenta, grafiki od autora); „w ramach wizualizacji w html pokażesz mi, jak to może wyglądać i jakie mamy opcje” · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-16
---

# ISSUE-046 — Ikony

> Dwie różne rzeczy: **ikona aplikacji** na ekranie telefonu (dziś domyślna ikona Fluttera — `mipmap-*` bez zmian od
> [[ISSUE-002-bootstrap-code-repo]]; sklep chce ikony 512 × 512) i **ikony w aplikacji** (ok. 70 różnych, Material Icons „outlined” — [[style-b]]
> reguła 3). Autor chce spróbować DALL-E dla obu i wybrać na makiecie. **Bez zmiany bazy.** Prompty idą od razu, żeby autor generował,
> kiedy łańcuch pracuje nad wcześniejszymi pozycjami.

## What to build
1. **`ui`: prompty do DALL-E** w stylu B — ikona aplikacji jako ikona adaptacyjna Androida (symbol na środku w strefie bezpiecznej, płaskie
   tło, wersja jednobarwna do motywów Androida 13+) i próbka ikon w aplikacji (najczęściej widoczne: zakładki, dodaj zdjęcie, pinezka,
   edycja, przesyłanie na telewizor).
2. **`ui`: makieta HTML z opcjami** (link `file:///`, retro 4 R1): **A** — obecne · **B** — Material Symbols z cieńszą kreską (grubość jednym
   parametrem, [`Icon.weight`](https://api.flutter.dev/flutter/widgets/Icon/weight.html), pakiet
   [`material_symbols_icons`](https://pub-web.flutter-io.cn/packages/material_symbols_icons/example)) · **C** — z DALL-E. Każda w prawdziwym
   rozmiarze (24 dp), w bursztynie i w kolorze tekstu pomocniczego, przy tekście 200%. Autor wybiera.
3. Plan i budowa według wyboru: ikona aplikacji (adaptacyjna + jednobarwna) i ikony w aplikacji; zmiana reguły 3 w [[style-b]], jeśli wybór
   ją zmienia. Nowa zależność → sprawdzenie, że nie wysyła danych ([[NFR-005-dane-nie-opuszczaja-telefonu]]).

## Acceptance Criteria
- **AC-1** *Given* telefon autora *Then* na ekranie głównym jest ikona Grobing w stylu B (także w motywie jednobarwnym), nie ikona Fluttera.
- **AC-2** *Given* wybrana opcja *Then* ikony w aplikacji są z jednej rodziny, mają kontrast ≥ 3:1 (WCAG 2.2 SC 1.4.11), rosną z tekstem, a cele
  dotyku zostają ≥ 48 dp.

## Notes
- Ryzyka opcji C (do pokazania na makiecie, nie do zgadywania): obraz rastrowy przy 24 dp, kolor zależny od stanu, spójność kilkudziesięciu
  ikon.
