---
title: "ISSUE-020 — Content guard: refuse staged lines that match the author's stem list"
type: issue
status: ready
delivery-style: task-level
priority: MUST
ideal_days: 0.5
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[2026-10-08-retro-02]] R1"
created: 2026-10-08
updated: 2026-10-08
---

# ISSUE-020 — Strażnik treści (lista rdzeni autora)

> Decyzja autora w [[2026-10-08-retro-02]] (R1). Pozycja startowa procesu, tak jak
> [[ISSUE-006-setup-family-data-guard]]: bez kroku ścieżki i bez US, więc bez wiersza w `TRACEABILITY.md`.

## Problem
Od 2026-10-07 push idzie sam zaraz po commicie paczki, a repo są publiczne. Strażnik z ISSUE-006 rozpoznaje
**typ pliku, nie treść**: nazwisko wpisane w kod, test albo dokument przejdzie. Przegląd imion z
[[NT-008-publication-review]] objął historię do 2026-10-07, a przy następnych pushach treści pilnuje tylko uwaga
agenta. Agent nie może sam przeszukać zmian nazwami z notatek: odczytu `family_data_dir` klasyfikator Claude
Code nie przepuścił nawet za zgodą autora w sesji (pierwszy push, `CURRENT_STATE.md` → *Recently done*).

## What to build
Rozszerzenie `grobing-agents/.claude/hooks/family-data-guard.ps1` o **sprawdzenie treści** przy `git add` i
`git commit` w trzech repo:

- **lista rdzeni** w pliku w `family_data_dir` (nazwa ustalana w planie): nazwiska, nazwiska z domu, miejscowości,
  nazwy cmentarzy — po jednym w linii. **Pisze ją autor**, w Notatniku, poza VS Code. Agent jej nie tworzy, nie
  czyta i nie edytuje;
- czyta ją **wyłącznie skrypt strażnika** (uruchamiany przez harness, nie przez agenta);
- sprawdzane: **dodawane linie** w plikach, które mogą wejść do commita (ten sam zbiór co dziś przy typach plików),
  i **opis commita** z komendy;
- dopasowanie bez wielkości liter i bez polskich znaków, rdzeń jako początek słowa (np. rdzeń „Wymyslin” łapie
  „Wymyślina” i „WYMYSLINIE”);
- trafienie → **odmowa** z repo, plikiem i numerem linii, **bez trafionego słowa i bez treści linii** (komunikat
  strażnika trafia do kontekstu agenta, a stamtąd do zapisu sesji);
- zmiana w `family-data.md`: skrypt strażnika jako jedyny czytelnik listy; agenci dalej nie czytają
  `family_data_dir` bez prośby autora; nowy wiersz w tabeli *Mechanisms*.

## Czego NIE daje — powiedziane uczciwie
- **imion** — za częste, kolidowałyby z wymyślonymi danymi w testach; lista ma rdzenie rzadkie;
- **commitów autora z VS Code** — tam dalej chroni tylko `.gitignore`;
- **treści już wypchniętej** — historię do 2026-10-07 przejrzało NT-008, commity od tamtej pory nie były
  przeszukane nazwami z notatek;
- słowa z literówką albo odmienionego tak, że zmienia się rdzeń.

## Acceptance Criteria
- [ ] **AC-1 — odmowa bez echa.** *Given* na liście jest wymyślony rdzeń testowy *When* `git add` pliku, w którym
      to słowo stoi odmienione, wielkimi literami albo bez polskich znaków *Then* strażnik odmawia, a komunikat
      podaje repo, plik i linię i **nie zawiera** ani słowa, ani linii (test sprawdza stderr).
- [ ] **AC-2 — opis commita.** *Given* ten sam rdzeń *When* `git commit -m` z tym słowem w opisie *Then* odmowa
      bez słowa w komunikacie.
- [ ] **AC-3 — czysto przechodzi.** Zmiany bez trafień przechodzą; czas strażnika przy `git add`/`commit`
      zmierzony i zapisany (porównanie z pomiarem z ISSUE-006 → *Verification*).
- [ ] **AC-4 — uruchomiony raz naprawdę.** Autor wpisuje na listę wymyślony rdzeń testowy, agent dodaje w repo
      plik z tym słowem → odmowa; potem autor usuwa rdzeń, a agent plik.
- [ ] **AC-5 — reguła.** `family-data.md`: kto czyta listę, czego mechanizm nie łapie, status „działa”.

## Do decyzji na stopie #1
- brak pliku listy: blokada (jak brak `project-config.md`, fail-closed) czy ostrzeżenie;
- które linie sprawdzać przy `git add` pliku nieśledzonego (cały plik) i śledzonego (diff wobec `HEAD`);
- czy lista ma też kody i liczby (np. numery kwater), czy tylko słowa.

## Notes / references
- Wzorzec dziedziny: skaner przed commitem z listą zakazanych wzorców trzymaną **poza treścią repo** (np.
  git-secrets: wzorce w lokalnym `git config`). Źródło do sprawdzenia w planie, nie z pamięci.
- Edycje reguł i skryptu strażnika klasyfikator może zablokować jako zmianę własnych uprawnień agenta. Takie linie
  agent podaje autorowi do wpisania, nie obchodzi blokady.
- Lista leży w `family_data_dir`, poza trzema repo i workspace'em, jak inne robocze notatki rodziny
  (`family-data.md` → *Family data on this PC*).
