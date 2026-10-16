---
title: "NT-005 — Distribution: direct install vs a store track (ADR — next free number)"
type: non-code-item
status: open
category: decision
priority: COULD
source: "PROJECT_BRIEF §6 N6"
wake-condition: "the first build worth installing on the author's own phone for daily use"
created: 2026-10-05
updated: 2026-10-16
---

# NT-005 — Dystrybucja

## The question / task
Aplikacja dla jednej osoby nie potrzebuje wpisu w sklepie. Instalacja bezpośrednia czy ścieżka testów
wewnętrznych w sklepie (konto deweloperskie autora już istnieje)? Koszt, aktualizacje, utrzymanie →
**ADR z następnym wolnym numerem**.

> Brief (§Architecture → *ADRs expected at MVP*) zarezerwował na dystrybucję numer ADR-005, ale ten
> numer zajął [[ADR-005-sqlite-package]] ([[ISSUE-007-data-layer]]). Wykrył to przegląd `kickoff/`
> (retro 1, R4, 2026-10-06).

## Why it matters
Dystrybucja przez sklep to też trigger [[DEF-002-full-l1-review]] (druga osoba / sklep → przegląd L1).

## Resolution (fill when done — this is the DoD)
- **2026-10-16 — decyzja autora w `/pm`** ([[2026-10-16-retro-04]] → *Product decisions*): **Google Play, ścieżka testów wewnętrznych**,
  autor jedynym testerem, **klucz podpisu wygenerowany przez Google** (Play App Signing), konto to samo co przy Friendsheet — *„tak zróbmy
  to”*. Powód autora: aktualizacja ze sklepu jak we Friendsheet, bez obawy o dane. Warunek obudzenia („pierwszy build wart codziennego
  używania”) — instalacja MVP najpóźniej 2026-10-29.
- ⏳ **ADR-019** (≥3 opcje) pisze łańcuch [[ISSUE-041-google-play-and-safe-update]]; ta pozycja zamyka się razem z nim.
- [[DEF-002-full-l1-review]]: ścieżka testów wewnętrznych z jednym testerem to nie „druga osoba / sklep publiczny” — warunek obudzenia
  nie zachodzi (do potwierdzenia w ADR-019).
