---
title: "ISSUE-006 — PreToolUse guard that refuses family-data files in any repo"
type: issue
status: ready
priority: MUST
created: 2026-10-05
updated: 2026-10-05
---

# ISSUE-006 — Family-data guard (T-05: the only real veto)

> Meta-decyzja 3h. Uzasadnione, bo w tym projekcie jest **jedna nieodwracalna akcja: wypchnięcie danych
> rodziny** do repo, które może dostać remote. Do czasu zbudowania chronią: reguła `family-data.md`
> (ładowana) i `.gitignore` w trzech repo.

## What to build
Hook `PreToolUse` w `grobing-agents/.claude/settings.json`, który **odmawia** (`deny`) zapisu i
`git add` plików: `*.db`, `*.sqlite*`, kopii (`*.grobing-backup`), eksportów, zdjęć spoza zasobów UI —
w **każdym z trzech repo**, rozpoznając je po typie i lokalizacji.

**Czego NIE daje — powiedziane uczciwie:** rozpoznaje plik, **nie treść**. Prawdziwego nazwiska
wpisanego w kod albo dokumentację nie zauważy — tę połowę pilnuje krytyk (powód BLOCK „dane rodziny w
repo", [[ISSUE-003-setup-quality-critic]]).

## Acceptance Criteria
- [ ] Skrypt istnieje; dopiero potem hook. Brak skryptu → `exit 2`, nigdy cisza.
- [ ] Zero ścieżek absolutnych; repo rozpoznawane z `project-config.md`.
- [ ] **Uruchomiony raz naprawdę:** próba zapisu `test.db` w `grobing-code` została odrzucona z
      czytelnym komunikatem.
- [ ] Granica (plik, nie treść) zapisana w `family-data.md` — status mechanizmu z „plan" na „działa".
