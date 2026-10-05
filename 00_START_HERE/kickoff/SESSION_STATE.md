---
title: "Grobing — Session State"
type: session-state
status: active
lifecycle: done             # discovery | build-design | materialization | done (kick-off pipeline)
track: 1                    # NPG track 1 — new product kick-off
created: 2026-10-05
updated: 2026-10-05
---

# Grobing — Session State

> Resumable state. Read FIRST when resuming work on this product. Updated at the end of every
> session. `lifecycle:` tracks where the kick-off pipeline is (the `kickoff` router reads it to route).

> 📍 **What this file owns:** `lifecycle:`, the pipeline coverage table, the decisions log, open
> questions. **What it does NOT own:** maturity stage, backlog counts, what is in flight — those will
> live in `CURRENT_STATE.md` after materialization and are **linked, never copied** here.

## Kick-off pipeline coverage (section status in PROJECT_BRIEF)
> Each section carries its own `status: draft | in-progress | approved`. The gate matrix
> (`kickoff-workflow.md`) reads these to allow the next phase.

| Phase | Specialist | Sections | Status |
|---|---|---|---|
| 1 discovery | npg-discover | §Profile | **approved** (2026-10-05) |
| 1 discovery | npg-discover | §1-6 | **approved** (2026-10-05; reopened + re-approved same day — view 5 → Must, D-005) |
| 2 build-design | npg-architect (+ security-advisor) | §How we build, §Security, §Architecture | **approved** (2026-10-05; §Security by security-advisor) |
| 3 materialization | npg-materializer | repo on disk | **done** (2026-10-05) — 3 repos, 5 agents, 6 rules, backlog, registry entry `grobing` (poufnosc: publiczna), schema-check clean |

## What we are building (one sentence — confirmed in discovery, 2026-10-05)
A private Android app in which every family grave leads to the people buried in it and to how they
connect to me — replacing single-copy paper notes, filled in while grandmother can still tell, and
outliving both its author and the app. Full value sentence: `PROJECT_BRIEF.md` §2.

## Work done before the pipeline (same session, 2026-10-05) — input to discovery, NOT a substitute

**Requested views (user's own words, condensed):**
1. Map of Poland with cemeteries where family members are buried.
2. Cemetery map with the burial place marked.
3. Grave → who is buried there (photo, first and last name).
4. Person detail → who they were, blood and in-law relations.
5. Family tree + time slider (births, marriages, deaths) + path between any two chosen people
   (e.g. me → my wife → her father → his sister → her husband → …).

**Prior-art scan (web, 2026-10-05) — every view exists, separately:**

| View | Existing tool |
|---|---|
| 1-2 map → cemetery → grave | Grobonet (1300+ Polish cemeteries, cemetery map, sector/row/plot address) · BillionGraves (GPS-tagged headstone photos on a map) |
| 3 who lies in the grave | as above · Graveyard Navigator (lines to family members' graves within one cemetery) |
| 4 person detail | any family-tree tool · Geneteka (Polish Genealogical Society, 46M+ vital-record indexes) |
| 5 relationship path | Gramps ("Relationship path between…" filter, Deep Connections gramplet — users report it crashes / walks the tree in the wrong direction) · FamilySearch, MyHeritage |
| data model under all of it | GEDCOM 7 (current 7.0.17) |

**Value hypothesis to test in discovery:** nothing found combines grave + tree + "how does this
connect to me" in one private place. That combination — not any single view — is the candidate value.

**Data-model traps named (for `npg-architect` Step 0 — canon of the domain):** marriage modelled as an
edge between two people instead of a family record (breaks at the first remarriage) · one grave = one
person (family graves hold several) · dates without uncertainty ("c. 1890", "before 1920") · no maiden
name (Geneteka search runs on it) · "kwatera" means a cemetery **sector** to administrators, while the
user uses it for a single grave.

**Observation from the same scan:** views 1 and 2 are one map at two zoom levels (satellite imagery
shows cemetery paths well enough to drop a pin); dedicated digital cemetery plans mostly do not exist.

## Decisions log
- **D-001 (2026-10-05):** Start building now rather than use 1 November as a capture-only day.
  The recommendation was capture-first; the user chose to build now because notes from previous
  years exist and should suffice for the first versions. 1 November is **not** a hard deadline —
  "whatever gets done is fine".
- **D-002 (2026-10-05):** Working space: `C:\Programowanie\Grobing` (working name "Grobing").
- **D-003 (2026-10-05):** Process appetite **heavy** (option B), chosen over the recommended "light
  process, durable data". The relaxed tone of the request is about the deadline, not the process.
  Profile approved.
- **D-004 (2026-10-05):** Discovery approved. Load-bearing outcomes: **sole user, multi-generational
  data** (the family inherits data, not app access) · main flow = **visit** · first version = views
  1-4 + capture + on-the-spot correction + offline + durable copy with restore and hand-over ·
  **view 5 (tree, slider, any-two path) → second version** · GEDCOM → nice-to-have (own database;
  canon compatibility flagged for the architect) · Style B (dark, minimal, candle-amber) · Android
  only, for now. Details: `PROJECT_BRIEF.md` §2, §5, §5a, §6a.
- **D-005 (2026-10-05):** MD4 — **MVP from the start** for the whole product (over the recommended
  PROTOTYP + data override). Same answer moved **view 5 (tree, slider, any-two path) into the MVP**
  (option B over A) → back-loop: §Discovery reopened, §5 Must gains M9-M11, "MVP done" now depends on
  spike H4.
- **D-006 (2026-10-05):** Build-design approved. Load-bearing outcomes: domain canon = genealogy
  (provenance, family group, oldest relatives first) + local-first · MD1 numbered, grow-as-you-go,
  PL content / EN headings, no family data in any repo, growth rule shipped as a loaded rule · MD2
  COMPONENT + task-level, spikes for unknowns, FR/NFR/AC/UJ/traceability · MD3 type A, pm/planning/
  dev/qa/docs, critic now (closed BLOCK list), auto-flow with 3 stops + parked items, write-time +
  session-start drift checks, family-data `PreToolUse` guard · MD4 MVP (all five views) · MD5
  ASVS-lite translated to mobile, encrypted own-cloud backup + offline family export · MD6 product DoD
  = §2 signal · **three repos** (vault/agents/code, over the recommended one) · **Flutter** (SDK
  pinned per project; no Firebase, own keystore outside the tree) · data model per the canon.
  Sufficiency A1-A6 accepted (migrations, sunlight readability, retro every 10, durable export
  formats, three spikes first, Julian dates named as Won't).
- **D-007 (2026-10-05):** Materialized at `C:\Programowanie\Grobing\` as three repos. Repos will be
  **public on GitHub** as a portfolio (registry `poufnosc: publiczna`); family data stays only on the
  phone, in the encrypted backup and in the family's export. **No repo is pushed before ISSUE-006
  (family-data guard) and NT-008 (publication review) are closed** — hard stop in `family-data.md`.

## Open questions
- [x] **Notes from previous years** — handwritten paper; ~50 graves · 10 cemeteries · ~100 people;
      dates present (D-004).
- [ ] **Privacy** — living people in the tree; where the off-phone copy lives → `security-advisor`
      (brief §6 N3).
- [ ] **Language of artefacts** — NPG default EN; content and user are Polish → `npg-architect` MD1.
- [ ] **Data model canon** — GEDCOM as the reference the own model is checked against; sources of
      facts (G3); fast entry for transcription (G6) → `npg-architect` Step 0 / Phase 3.
- [ ] **Data capture on 1 November 2026** — fits hypothesis H3 (pin 3 graves, check on site);
      becomes an early non-code item at materialization.

## Next step (to resume)
Kick-off closed. The author runs the printed `git init` commands, opens `grobing-agents` → `/pm`.
First items: ISSUE-001 (rest of the backlog) and NT-001 (photograph the notes).

## How to resume
**Product work:** open `C:\Programowanie\Grobing\Grobing.code-workspace` (agents first, vault + code as extra folders) → `/pm`. State lives in
`../00_START_HERE/CURRENT_STATE.md` (single counter), not here.
**Kick-off record:** this file + `PROJECT_BRIEF.md` + `PROFILE.md` + `MANIFEST.yaml` in this folder.
Moved here from `C:\Programowanie\Grobing\00_START_HERE\kickoff\` at materialization (2026-10-05).
