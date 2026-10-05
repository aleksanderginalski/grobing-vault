---
title: "FR-005 — Birth (maiden) surname next to the married surname"
type: functional-requirement
status: draft
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
used-by: []
user-stories: []
NFR: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF Step 0 · Data model → Person"
created: 2026-10-05
updated: 2026-10-05
---

# FR-005 — Nazwisko rodowe

## Requirement
Osoba ma **nazwisko** i osobno **nazwisko rodowe** (z urodzenia, panieńskie).

## Rules
- Nazwisko rodowe ≠ nazwisko po ślubie (`glossary.md` → *nazwisko rodowe*).

## Why durable
Po nazwisku rodowym przeszukuje się polskie zapisy (model danych → *Person*). Odpowiednik w kanonie
GEDCOM — eksport (C2) zostaje tani.
