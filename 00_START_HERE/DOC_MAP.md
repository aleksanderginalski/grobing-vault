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

> **Wizja = `kickoff/PROJECT_BRIEF.md` §1-3** (zdanie wartości w §2) — wystarcza jako wizja produktu;
> `02_PRODUCT/vision/` powstaje dopiero, gdy wizja albo canvas wyjdą poza brief (`doc-growth.md`).
> Ustalone w [[ISSUE-001-materialize-backlog]] AC-1. <!-- placeholder-ok: real wikilink -->

| Folder | Purpose | Added |
|---|---|---|
| `00_START_HERE/` | Orientacja, stan, kontrakty (słownik, DoR/DoD, macierz powiązań) | kickoff |
| `00_START_HERE/kickoff/` | Zapis sesji kick-off: brief, profil, stan sesji, manifest decyzji | kickoff |
| `00_START_HERE/TRACEABILITY.md` | Macierz powiązań brief → EPIC → US → ISSUE, zasiana krokami ścieżki wizyty | kickoff (COMPONENT) |
| `01_INBOX/` | Szybkie notatki i pomysły do rozdzielenia — **bez danych rodziny** | kickoff |
| `02_PRODUCT/` | Produkt poza briefem: persony (wizja — patrz zdanie nad tabelą) | ISSUE-001 — pierwsza persona poza briefem |
| `02_PRODUCT/personas/` | Persony (P1 Zbierający; babcia to Źródło, nie persona) | ISSUE-001 AC-2 |
| `03_REQUIREMENTS/` | Wymagania kanoniczne: EPIC · US · AC · FR · NFR | ISSUE-001 — pierwsze wymaganie do spisania |
| `03_REQUIREMENTS/epics/` | EPIC-NNN — jeden etap procesu genealoga; **EPIC-i żyją tylko tutaj**, nie w `backlog/` | ISSUE-001 AC-3 |
| `03_REQUIREMENTS/functional/` | FR-NNN — trwałe reguły systemu (przeżywają każdą US), jeden `epic:` | ISSUE-001 AC-3c |
| `03_REQUIREMENTS/user-stories/` | US-NNN — jedna rzecz, którą Zbierający robi od początku do końca; **AC w pliku US** (Given/When/Then), lista ISSUE we frontmatterze | rozpisanie EPIC-001 (2026-10-05) — pierwsza US |
| `03_REQUIREMENTS/non-functional/` | NFR-NNN — miara · cel · metoda · trigger weryfikacji; `epic:` jako lista | ISSUE-001 AC-3c |
| `04_ARCHITECTURE/` | Architektura: model danych (`data-model.md` — żywy dom modelu), formaty kopii i eksportu | ISSUE-001 — pierwszy model danych |
| `04_ARCHITECTURE/decisions/` | ADR-NNN — ≥3 opcje, append-only po akceptacji | ISSUE-001 AC-4 — pierwsza decyzja architektoniczna |
| `backlog/` | Pozycje pracy: ISSUE · SPIKE · NT · DEF (EPIC-i — w `03_REQUIREMENTS/epics/`) | kickoff |
| `backlog/issues/` | Zadania (ISSUE-NNN), w tym zadania konfiguracji mechanizmów | kickoff |
| `backlog/spikes/` | Eksperymenty z pytaniem, limitem czasu i warunkiem wyjścia (SPIKE-NNN) | kickoff — trzy niewiadome architektury (A5) |
| `backlog/non-tech/` | Sprawy poza kodem (NT-NNN): prawne, koszty, przekazanie rodzinie, przepisywanie | kickoff — §6 briefu |
| `backlog/deferred/` | Wymogi odłożone z triggerem-zdarzeniem (DEF-NNN) | kickoff — §Security + Meta-dec. 3g |
