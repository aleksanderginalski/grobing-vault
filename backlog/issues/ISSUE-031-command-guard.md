---
title: "ISSUE-031 — Command guard: refuse a Python script read from stdin and the git commands the boundary forbids"
type: issue
status: ready
delivery-style: task-level
priority: MUST
ideal_days: 0.5
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[2026-10-13-retro-03]] R1"
created: 2026-10-13
updated: 2026-10-13
---

# ISSUE-031 — Strażnik komend (mechanizm zamiast pamięci)

> Decyzja autora w [[2026-10-13-retro-03]] (R1). Pozycja startowa procesu, tak jak [[ISSUE-006-setup-family-data-guard]] i
> [[ISSUE-020-content-guard]]: bez kroku ścieżki i bez US, więc bez wiersza w `TRACEABILITY.md`.

## Problem
Dwie rzeczy wracają mimo zapisu w pamięci agenta i w regułach:
- **`python -` / `python -I -`** (skrypt czytany z wejścia) — **8 razy** od SPIKE-001, w czterech kolejnych pozycjach (ISSUE-025,
  023, 028, 029). W tym środowisku komenda wisi, aż ktoś ją zatrzyma. Pamięć mówi „nigdy”, a token wraca z nawyku: raz jako
  „szablon” komendy, raz doklejony do łańcucha. Bez szkody dla plików, ale za każdym razem tracona runda;
- **komendy git zmieniające indeks poza commitem `docs`** — `git rm --cached` w ISSUE-014 (retro 2, R2), `git add -N .` i `git reset -q`
  w ISSUE-028 („tylko do liczenia”). Reguła `git-autonomy-boundary.md` je zakazuje, a nic ich nie zatrzymuje.

Strażnik danych rodziny pokazał, że mechanizm działa tam, gdzie wola nie działa.

## What to build
Hook `PreToolUse` w `grobing-agents` (narzędzia `Bash` i `PowerShell`), który **odmawia** komendy z czytelnym powodem i
podpowiedzią:
- **Python ze skryptem z wejścia:** `python`, `python3`, `py` (także `.exe`) z argumentem `-` albo bez skryptu i bez `-c`/`-m`
  → odmowa z podpowiedzią „zapisz skrypt w katalogu tymczasowym sesji i uruchom plik”;
- **git z *Forbidden autonomously*** (`git-autonomy-boundary.md`): `reset`, `restore`, `stash`, `rm`, `checkout`, `switch`,
  `rebase`, `merge`, `pull`, `fetch`, `commit --amend`, `branch -D/-d`, `init`, `remote add/set-url/remove`, `push` inny niż
  `git push origin main` (`--force`, `-f`, `--force-with-lease`, inna gałąź, tagi), `add` z `-A`, `--all`, `.`, `-u`, `-N`,
  `--intent-to-add`, wzorcem katalogu, `--no-verify` przy każdej komendzie, `gh`;
- **przechodzi bez zmian:** komendy tylko do odczytu (`status`, `diff`, `log`, `branch -l`, `branch --show-current`,
  `remote get-url`, `check-ignore`, `show`, `rev-parse`), `git add -- <jawne pliki>`, `git commit` (bez `--amend`, bez
  `--no-verify`), `git push origin main`.

Strażnik danych rodziny dalej robi swoje przy `git add`/`commit` — ten hook go nie zastępuje.

## Czego NIE daje — powiedziane uczciwie
- Komendy złożonej w locie (`bash -c "$(…)"`, zmienna z nazwą komendy, alias), skryptu z pliku, który sam woła zakazaną komendę,
  i komend autora z VS Code.
- Pamięć agenta o komendach zostaje. Hook łapie nawyk przy próbie, ale nie usuwa go.
- Zmianę `.claude/settings.json` klasyfikator Claude Code może zablokować agentowi (tak było przy edycji reguł w ISSUE-020) — wtedy
  autor wpisuje podaną linię sam.

## Acceptance Criteria
- [ ] Każda zakazana forma z *What to build* w teście hooka → odmowa z powodem i podpowiedzią; **falsyfikator: test, w którym
      któraś z nich przechodzi**.
- [ ] Każda forma z listy „przechodzi” w teście → bez odmowy; komendy łączone (`&&`, `;`, `|`) sprawdzane w całości.
- [ ] Przy własnym błędzie albo braku skryptu hook **blokuje** (jak strażnik danych rodziny, ISSUE-006) i mówi dlaczego.
- [ ] Testy strażnika danych rodziny dalej zielone; koszt hooka na wywołanie zmierzony i zapisany.
- [ ] `git-autonomy-boundary.md` → *Forbidden autonomously* mówi, który mechanizm łapie te komendy, i czego nie łapie.

## Do decyzji na stopie #1
- Osobny skrypt (`command-guard.ps1`) czy gałąź istniejącego `family-data-guard.ps1`? Kandydat: osobny skrypt — inna
  odpowiedzialność, a strażnik danych rodziny ma już 635 linii i 150 testów.
- Czy `git fetch` (bez zapisu w gałęziach roboczych) ma przechodzić? Reguła mówi dziś „`git fetch` z zapisem”.

## Notes / references
- [[2026-10-13-retro-03]] R1 · `grobing-agents/.claude/rules/git-autonomy-boundary.md` → *Forbidden autonomously* ·
  `.claude/hooks/family-data-guard.ps1` (wzorzec: fail-closed, testy w `.claude/hooks/tests/`).
