---
title: "ISSUE-004 — Set up the drift check (\"the dump\"): on file write + on session start"
type: issue
status: deferred
deferred-until: signal
trigger: "first DOC_MAP ↔ disk mismatch or dead link found after the fact (not by the writer in the same change)"
level: enforced
priority: SHOULD
created: 2026-10-05
updated: 2026-10-13
---

# ISSUE-004 — Drift check: on file write + on session start

> Zmaterializowane z Meta-decyzji 3g, wybór **(c) mechanizm, który sam się odzywa** — odpowiedź na
> pytanie autora o śmietnik. Wzorzec źródłowy: check sprzężenia przy każdej edycji z NPG (WZ-015).
> **Zaczynamy od triggera, nie od checku.**

## What to build

| Trigger | Co sprawdza | Poziom | Czego NIE łapie |
|---|---|---|---|
| **przy zapisie pliku** (hook `PostToolUse`) | martwe odwołania · reguły nieładowane z `CLAUDE.md` · **DOC_MAP ↔ dysk** (folder bez wiersza, wiersz bez folderu) | ostrzeżenie w tej samej turze | **upływu czasu** — wszystkiego, czego nikt nie edytował |
| **na starcie sesji** (hook `SessionStart`) | ten sam podzbiór + **co się zestarzało**: sprawy zaparkowane, odłożone pozycje, których trigger mógł nastąpić. **Milczy, gdy czysto.** | raport, nigdy blokada | zmian w dalszej części tej samej sesji |
| **na żądanie** | pełny przebieg — `npg-linkcheck` na `grobing-agents` + `grobing-vault` | ręczny | siebie: nieuruchomiony check wygląda jak czysty |

**Trzy zasady, bez których to bramka bez zębów:**
1. **Bramka = czujnik + próg** — sprawdź oba.
2. **Check, który nie umie się uruchomić, pada GŁOŚNO** (stderr + `exit 2`), nigdy nie milknie.
3. **Ostrzeżenie, nie blokada** — check czerwony na naturalnym stanie repo zostanie wyłączony w tydzień.

**Ścieżki:** skrypt w `grobing-agents/.claude/scripts/`; korzeń z `$env:CLAUDE_PROJECT_DIR`, vault z
`project-config.md` — **zero ścieżek absolutnych** (rozdział tożsamości i ścieżki, T-14/T-15).

## The half no mechanism covers
Każdy check porównuje plik z nim samym. **Zdarzenia, które nie trafiło do dokumentów, nie zobaczy
żaden.** Para: co **10** zamkniętych pozycji `pm` pyta o 3-5 nośnych faktów (licznik w
`CURRENT_STATE.md`) — działa od dnia 1.

## Acceptance Criteria
- [ ] Skrypt istnieje; **dopiero potem** hooki w `.claude/settings.json` (hook bez skryptu to najcichsza
      awaria platformy).
- [ ] Hook przy zapisie i hook startu sesji wpięte; brak skryptu → `exit 2` z komunikatem.
- [ ] **Uruchomiony raz naprawdę** na celowo zepsutym przypadku (folder bez wiersza w DOC_MAP) —
      ostrzeżenie padło.
- [ ] Ostrzega, nie blokuje rutynowych edycji.
- [ ] Granica („nie widzi zdarzeń, których nikt nie zapisał") opisana tam, gdzie przeczyta ją następna
      osoba.

## Notes / references
- `PROJECT_BRIEF.md` §How we build → 3g · NPG `agentic-ci-patterns.md` (CI-T2, CI-T3, CI-T4) ·
  trigger bramki na pushu: [[DEF-005-push-gate]].

## Deferred — 2026-10-13 ([[2026-10-13-retro-03]], R10)
Decyzja autora: **`deferred` do sygnału** (`trigger:` wyżej). Pozycja stała w `ready` od kick-offu i przez 20 zamkniętych pozycji
nikt jej nie wziął. Do obudzenia DOC_MAP ↔ dysk pilnuje self-check `docs` (`doc-growth.md`), a zestarzały stan — `pm` na starcie
sesji. Retro 3 (R5) zmniejszyło `CURRENT_STATE.md`, bo odczyt obcinał go w połowie — to inna strona tego samego problemu.

**Warunek obudzenia:** pierwszy rozjazd DOC_MAP ↔ dysk albo martwe odwołanie znalezione po fakcie, a nie przez piszącego w tej
samej zmianie. Obudzenie nie jest zgodą na budowę — `pm` pokazuje je autorowi.
