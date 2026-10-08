---
title: "ISSUE-021 — Small fixes after retro 2: Polish system strings, debug seed names, two buttons without a tap action, tests README"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
ideal_days: 0.5
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[2026-10-08-retro-02]] R3 i R9"
created: 2026-10-08
updated: 2026-10-08
---

# ISSUE-021 — Drobne poprawki po retro 2

> Decyzja autora w [[2026-10-08-retro-02]] (R9, R3): jedna mała pozycja, **przed pierwszymi prawdziwymi danymi**.
> Poprawki do ekranów z [[US-002-przepisanie-grobu]] ([[ISSUE-012-transcribe-grave-screen]],
> [[ISSUE-015-add-cemetery-from-database]]) i [[US-005-zdjecia]] ([[ISSUE-016-photos-grave-and-person]]).
> Kolumnę Issue(s) w `TRACEABILITY.md` wpisuje `planning`.

## What to fix
1. **Polskie teksty systemowe** — `MaterialLocalizations` są po angielsku (przegląd `ui`, uwaga 11): podpowiedzi
   i etykiety widżetów Fluttera (np. okno daty, „wklej”, opisy przycisku wstecz) w aplikacji po polsku.
2. **Wstępne dane debug** ([[ISSUE-012-transcribe-grave-screen]] → *Notes*): wszyscy wymyśleni z
   [[ISSUE-007-data-layer]] mają nazwisko „Wymyślona”, także „Ojciec” — na ekranach wygląda to jak błąd odmiany.
   Tylko build debug; wymyślone osoby zostają wymyślone.
3. **Semantyka dwóch przycisków** (przegląd `ui` przy [[ISSUE-017-person-photos]], MAJOR tego samego wzorca):
   „Dodaj zdjęcie nagrobka” ([[ISSUE-016-photos-grave-and-person]]) i podgląd cmentarza z bazy
   ([[ISSUE-015-add-cemetery-from-database]]) mają opis dla czytnika, ale bez akcji dotknięcia, więc Switch Access
   i Voice Access ich nie naciśną. Poprawka i test na każdy ekran.
4. **README `grobing-code` → testy** (R3, pisze `qa`): krótka sekcja o zawieszonych przebiegach — strumień drift i
   timer fałszywego czasu ([[ISSUE-014-home-map-of-poland]] → *Verification*), zapis albo odczyt bazy w
   `tester.runAsync` przy podpiętym ekranie ([[ISSUE-012-transcribe-grave-screen]] → *Verification*), wzorzec
   `leaveScreen`, zablokowany `sqlite3.dll` i `flutter_01.log` w korzeniu repo po zawieszonym przebiegu.

## Acceptance Criteria
- [ ] **AC-1** — widżety systemowe w aplikacji mówią po polsku (test: `MaterialLocalizations.of(context)` w
      aplikacji zwraca polskie teksty).
- [ ] **AC-2** — wymyśleni w buildzie debug mają nazwiska, które na ekranach nie wyglądają jak błąd odmiany.
- [ ] **AC-3** — oba przyciski mają akcję dotknięcia w drzewie semantyki (test na każdy ekran).
- [ ] **AC-4** — sekcja w README `grobing-code` → testy.

## Notes
- Specyfikacje ekranów się nie zmieniają (semantyka wynika z wzorca przeglądu ISSUE-017), więc `pm` może
  skierować pozycję od razu do `planning`. Jeśli plan pokaże zmianę na ekranie → najpierw `ui`.
- Bez zmiany schematu, bez warstwy danych.
