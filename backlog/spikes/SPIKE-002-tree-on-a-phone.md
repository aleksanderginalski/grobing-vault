---
title: "SPIKE-002 — Is a family tree with in-laws and remarriages readable on a phone?"
type: spike
status: ready
priority: MUST
time-box: "1-2 days"
hypotheses: [H4]
blocks: "MVP done (view 5, M9-M11) — not the use of views 1-4"
created: 2026-10-05
updated: 2026-10-05
---

# SPIKE-002 — Tree on a phone (S-TREE)

## The question
**Czy graf rodziny ~100 osób z powinowatymi i powtórnymi małżeństwami da się czytelnie pokazać na
ekranie telefonu — i jakim układem?**

## Why it matters
To główne ryzyko budowy (H4) i jedyna rzecz, od której zależy **ogłoszenie gotowego MVP** (widok 5
trafił do Must z wyboru autora). Narzędzia genealogiczne pokazują zwykle przodków albo potomków, a nie
„wszystkich" — nie bez powodu.

## Steps
1. Wygeneruj **wymyślony** zbiór ~100 osób o strukturze podobnej do realnej (powinowaci, 2-3 powtórne
   małżeństwa, kilka pokoleń) — **żadnych prawdziwych danych**.
2. 2-3 podejścia: biblioteka układu grafu we Flutterze · widok wycinkowy (rodzina + 1 pokolenie w górę
   i w dół, przewijany) · widok „od osoby" z rozwijaniem.
3. Oceń na prawdziwym telefonie autora: czy da się odpowiedzieć na „kim jest X dla Y" w < 30 s.

## Input from SPIKE-004 (2026-10-08)
- **Kierunek autora na prototypie** ([[drzewo]] v1.1): drzewo **od osoby** z przestawianiem środka (kandydat 3 z kroku 2),
  poziomy połączeń, kolory linii rodzic–dziecko i partnerzy, czas (pojawianie przy narodzinach, łączenie przy związku),
  „Połącz dwie osoby” na drzewie z animacją. Spike sprawdza teraz **czytelność tego kierunku przy ok. 100 osobach**.
- **Do pokazania jako kandydaci** (retro 2, R6): sterowanie poziomami bez przycisków − / + (np. oddalanie odsłania dalszą
  rodzinę — [[drzewo]] *Open* 1) i tryb prezentacji na telewizor (*Open* 2).
- **Dane do spike'a:** wymyślona rodzina o kształcie prawdziwej (ok. 100 osób, powinowaci, związki „razem” i małżeństwa),
  zostaje w buildzie debug jako dane do oceny „feelingu” (propozycja z sesji `/pm` 2026-10-08).

## Exit criterion
Wybrane podejście → notatka/ADR; albo „nie da się czytelnie" → decyzja autora (np. widok wycinkowy
zamiast pełnego drzewa).

## Definition of Done
- [ ] Odpowiedź zapisana · kod eksperymentu usunięty · status H4 zaktualizowany.
