---
title: "ISSUE-030 — Sectors on a visit (candidates): „Pokaż kwaterę” for a grave without a pin, the graves of a sector, overlapping candles opening a list"
type: issue
status: draft
delivery-style: task-level
priority: SHOULD
epic: "[[EPIC-002-wizyta]]"
user-story: "[[US-008-pinezka-na-miejscu]]"
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "rozpisanie US-008 (`docs` w auto-flow po `pm`, 2026-10-12) · [[cmentarz]] D29 i *Open* (znicze nachodzą na siebie) · [[EPIC-002-wizyta]] → *Open questions* (kierunek autora, krok 3)"
created: 2026-10-12
updated: 2026-10-12
---

# ISSUE-030 — Kwatera na wizycie (kandydaci)

> **`draft`: to propozycja łańcucha, nie decyzja autora.** Autor rozstrzyga ją na stopie #1 [[ISSUE-029-pin-on-site-gps]]: wchodzi
> przed zaduszkami, czeka na wizytę albo zostaje wycofana. Do tego czasu nie ma jej w kolejności drogi do MVP.

## Why
Kierunek autora dla grobu bez pinezki ([[EPIC-002-wizyta]] → *Open questions*): adres z wyszukiwarki zarządcy → kwatera zaznaczona
według planu zarządcy → **na miejscu idzie do kwatery planem offline i GPS-em** i stawia pinezkę. Kroki 1 i 2 mają ekrany od
[[ISSUE-028-cemetery-sectors]], a pinezkę z kroku 3 stawia [[ISSUE-029-pin-on-site-gps]]. Między nimi zostaje jedna rzecz: trzeba
**znaleźć na planie kwaterę grobu**. Dziś autor czyta adres w liście grobów i szuka strefy z tą nazwą na planie.

## Candidates
1. **„Pokaż kwaterę”** przy grobie bez pinezki, którego kwatera ma strefę: plan z tą strefą wybraną (akcent, jak w trybie E).
   *Obali:* nazwy stref na planie (element 4) wystarczą, żeby trafić — sprawdzi wizyta.
2. **Lista grobów kwatery** po dotknięciu strefy na wizycie ([[cmentarz]] D29). **Warunek obalenia D29 jeszcze nie zaszedł**: D29
   mówi „autor na wizycie chce dotknąć kwatery, żeby zobaczyć jej groby”, a wizyty z planem jeszcze nie było. Uczciwie: ten kandydat
   czeka na wizytę.
3. **Znicze sąsiednich grobów nachodzą na siebie** ([[cmentarz]] *Open*): przy największym przybliżeniu cel 48 dp ma ok. 9 m, a groby
   obok siebie są bliżej. Kandydat: znicz z liczbą otwiera arkusz z listą tych grobów. Problem pojawi się przy pierwszych pinezkach
   stawianych obok siebie.

## Acceptance Criteria
Powstaną po decyzji autora, z kandydatów, które wejdą.

## Notes
- Ekran się zmienia, więc gdy pozycja wejdzie: `ui` → `planning`.
- Kandydaci 2 i 3 mają warunek z terenu. Taniej sprawdzić je na wizycie z [[ISSUE-029-pin-on-site-gps]] niż zbudować wcześniej.
