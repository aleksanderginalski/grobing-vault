---
title: "NT-005 — Distribution: direct install vs a store track (ADR — next free number)"
type: non-code-item
status: open
category: decision
priority: COULD
source: "PROJECT_BRIEF §6 N6"
wake-condition: "the first build worth installing on the author's own phone for daily use"
created: 2026-10-05
updated: 2026-10-06
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
[decyzja → ADR-NNN + data]
