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

## Exit criterion
Wybrane podejście → notatka/ADR; albo „nie da się czytelnie" → decyzja autora (np. widok wycinkowy
zamiast pełnego drzewa).

## Definition of Done
- [ ] Odpowiedź zapisana · kod eksperymentu usunięty · status H4 zaktualizowany.
