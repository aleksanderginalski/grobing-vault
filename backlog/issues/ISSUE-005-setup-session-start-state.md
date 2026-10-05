---
title: "ISSUE-005 — Compute session state at start (in progress, parked, next) instead of remembering it"
type: issue
status: ready
priority: SHOULD
created: 2026-10-05
updated: 2026-10-05
---

# ISSUE-005 — Session state computed at start (SC-02 via T-03)

> Meta-decyzja 3h. **Dziś działa w wersji ręcznej** — `pm` czyta `CURRENT_STATE.md` i backlog
> (poziom MANUAL). To zadanie robi wersję liczoną: hook `SessionStart` **wylicza** stan z backlogu i
> wstrzykuje go, zanim padnie pierwsze pytanie — nic nie zależy od pamięci.

## What to build
Skrypt czytający frontmatter pozycji w `{vault}/backlog/` i `CURRENT_STATE.md`, wypisujący na starcie:
co jest `in-progress` · ile spraw zaparkowanych i ich warunki obudzenia · licznik do retro (≥10 →
przypomnienie o retro i pytaniu o fakty) · propozycja następnej pozycji (SC-12) wyprowadzona z tego
stanu.

**Czego NIE daje:** precyzyjnie policzony nieaktualny backlog to precyzyjna fikcja — liczenie gwarantuje,
że liczba jest **wyprowadzona**, nie że jest **sensowna**.

## Acceptance Criteria
- [ ] Skrypt istnieje i działa ręcznie; dopiero potem hook `SessionStart` w `.claude/settings.json`.
- [ ] Brak skryptu → `exit 2`; zero ścieżek absolutnych (vault z `project-config.md`).
- [ ] Może współdzielić hook startu sesji z [[ISSUE-004-setup-freshness-gate]] — jeden hook, dwa
      raporty, milczący, gdy nie ma nic do powiedzenia poza stanem.
- [ ] Uruchomiony raz naprawdę: pokazał zaparkowaną sprawę dodaną testowo (bez danych rodziny).
