---
title: "Grobing — Document Map"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-05
---

# Grobing — Document Map

> Żywa mapa folderów vaulta: co tu jest, po co i kiedy powstało. **Dopisz wiersz za każdym razem,
> gdy powstaje folder** — według reguły rozbudowy w `grobing-agents/.claude/rules/doc-growth.md`
> (tabela „sygnał → folder → co tam trafia"). Folder bez wiersza albo wiersz bez folderu to
> **zaczątek śmietnika** — wyłapie to check z Meta-decyzji 3g
> ([[ISSUE-004-setup-freshness-gate]]).
>
> ⚠️ **W tym vaulcie nie ma i nie będzie danych rodziny** — imion, dat, zdjęć ani pozycji grobów
> prawdziwych osób. Dane żyją wyłącznie w aplikacji na telefonie (+ zaszyfrowana kopia + eksport u
> rodziny). Reguła: `grobing-agents/.claude/rules/family-data.md`.

| Folder | Purpose | Added |
|---|---|---|
| `00_START_HERE/` | Orientacja, stan, kontrakty (słownik, DoR/DoD, macierz powiązań) | kickoff |
| `00_START_HERE/kickoff/` | Zapis sesji kick-off: brief, profil, stan sesji, manifest decyzji | kickoff |
| `00_START_HERE/TRACEABILITY.md` | Macierz powiązań brief → EPIC → US → ISSUE, zasiana krokami ścieżki wizyty | kickoff (COMPONENT) |
| `01_INBOX/` | Szybkie notatki i pomysły do rozdzielenia — **bez danych rodziny** | kickoff |
| `backlog/` | Pozycje pracy (hierarchia COMPONENT: EPIC → US → ISSUE) | kickoff |
| `backlog/issues/` | Zadania (ISSUE-NNN), w tym zadania konfiguracji mechanizmów | kickoff |
| `backlog/spikes/` | Eksperymenty z pytaniem, limitem czasu i warunkiem wyjścia (SPIKE-NNN) | kickoff — trzy niewiadome architektury (A5) |
| `backlog/non-tech/` | Sprawy poza kodem (NT-NNN): prawne, koszty, przekazanie rodzinie, przepisywanie | kickoff — §6 briefu |
| `backlog/deferred/` | Wymogi odłożone z triggerem-zdarzeniem (DEF-NNN) | kickoff — §Security + Meta-dec. 3g |
