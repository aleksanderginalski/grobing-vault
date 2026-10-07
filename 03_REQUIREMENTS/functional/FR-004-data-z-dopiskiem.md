---
title: "FR-004 — Dates with a qualifier (exact / about / before / after / between)"
type: functional-requirement
status: draft
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
used-by: ["[[EPIC-003-zrozumienie]]"]
user-stories: ["[[US-002-przepisanie-grobu]]", "[[US-003-przepisanie-rodziny]]"]
NFR: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF Step 0 · Data model → Event · §5 M10"
created: 2026-10-05
updated: 2026-10-07
---

# FR-004 — Data z dopiskiem

## Requirement
Każda data zdarzenia (urodzenie, zgon, małżeństwo, koniec rodziny, pochówek) to **data + kwalifikator**:
**dokładnie · około · przed · po · między** (dla „między" — dwie granice).

## Rules
- „ok. 1890" i „przed 1920" to **normalne dane**, nie błędy — aplikacja je przyjmuje, zapisuje i pokazuje
  z dopiskiem.
- Data jest twierdzeniem ze źródłem ([[FR-001-provenance]]) — dwie różne daty z dwóch źródeł to
  `CONTRADICTED`, nie nadpisanie.
- Suwak czasu (M10) musi umieć ustawić zdarzenie z datą niepewną.

## Coverage notes
- **2026-10-07 — data pochówku nie ma pola w formularzu** (decyzja autora, [[ISSUE-012-transcribe-grave-screen]] D7).
  Model przechowuje ją jak każde zdarzenie, a widok grobu pokazuje ją z dopiskiem, ale żadna zamknięta US nie daje
  dziś drogi jej wpisania. Przy werdykcie [[EPIC-001-zabezpiecz-i-przepisz]] ta część FR **nie liczy się jako
  pokryta**. Wraca z pierwszym wpisem z datą pochówku przy przepisywaniu albo ze źródłem innym niż notatki
  ([[US-004-fakt-od-babci]]).

## Why durable
Daty ślubów prawie nigdy nie są na nagrobkach (brief §1); źródła podają daty przybliżone. Model, który
wymaga daty dokładnej, wymusza zmyślanie.
