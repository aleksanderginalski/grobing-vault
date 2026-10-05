---
title: "ISSUE-001 — Materialize the rest of the backlog from PROJECT_BRIEF"
type: issue
status: ready
priority: MUST
scope: docs
ideal_days: 1.0
created: 2026-10-05
updated: 2026-10-05
---

# ISSUE-001 — Materialize the rest of the backlog from PROJECT_BRIEF

> Jedyny meta-issue z kick-offu. Sesja postawiła minimalny start, mechanizmy jako pozycje i
> eksperymenty; to zadanie zamienia resztę `PROJECT_BRIEF.md` w pełny backlog. Wykonuje `docs`.
> Struktura wg hierarchii **COMPONENT** i reguły `doc-growth.md` — folder powstaje dopiero, gdy ma treść.

## Description

`00_START_HERE/kickoff/PROJECT_BRIEF.md` niesie każdą decyzję z kick-offu: wartość (§2), MoSCoW
M1-M11 (§5), personę (§4), ścieżkę wizyty (§4a), meta-decyzje, §Security i §Architecture (model
danych, ADR-y). To zadanie wyciąga je do osobnych artefaktów.

**Zakres:** wyłącznie dokumentacja. Bez kodu. Bez nowych decyzji produktowych — niejasność w briefie
→ `⚠️ OPEN` w wytworzonym pliku. **Bez danych rodziny.**

## Inputs (read first)

- `00_START_HERE/kickoff/PROJECT_BRIEF.md` — jedyne źródło
- `00_START_HERE/glossary.md` · `DEFINITION_OF_DONE.md` · `DOC_MAP.md` · `TRACEABILITY.md`
- `grobing-agents/.claude/rules/doc-growth.md` — który folder na jaki sygnał

### Correction from the author (2026-10-05) — the brief assumed otherwise

**Notatki nie zawierają adresów kwater** — są w nich adresy cmentarzy, pochowane osoby, informacje o
nich i ich powiązania. Brief zakładał adres kwatery z notatek: §1 („per cemetery plot"), §4a krok 2
(„each with its plot address") i gałąź *„Grave with no pin yet (only a plot address from the notes)"*.
Przy AC-3b: gałąź UJ-001 to **grób bez pinezki i bez adresu kwatery** — położenie i adres powstają
dopiero na miejscu (krok 6). Jeśli to wymaga zmiany kroku albo nowego EPIC-a/US → `## Open gaps`,
nie po cichu. Wpływ na SPIKE-001 krok 4 — oznaczony w samym spike'u.

## Acceptance Criteria

- [ ] **AC-1 — Vision.** Brief §1-3 wystarcza jako wizja — zapisz to jednym zdaniem w DOC_MAP albo,
      jeśli rozwijasz, `02_PRODUCT/vision/`.
- [ ] **AC-2 — Persona.** Brief §4 → `02_PRODUCT/personas/P1-zbierajacy.md` (Zbierający) + notka o
      babci jako **Źródle**, nie personie.
- [ ] **AC-3 — EPICs.** Z MoSCoW i kanonu (etapy procesu genealoga) → `03_REQUIREMENTS/epics/`, po
      pliku na EPIC, cel w jednym zdaniu, `status: draft`. Proponowany podział do potwierdzenia z
      autorem: *Zabezpiecz i przepisz* (M1, M8) · *Wizyta* (M2-M7) · *Zrozumienie* (M9-M11).
      **Bez US** — rozpisanie na US to osobny krok.
- [ ] **AC-3b — Journey coverage checked, not assumed.** Przejdź zasiane wiersze `TRACEABILITY.md` i
      przypisz każdy krok UJ-001 oraz każdy wiersz `n/a` do EPIC-a. **Krok bez EPIC-a trafia do
      `## Open gaps` z nazwy** — nie poszerzaj EPIC-a po cichu.
- [ ] **AC-3c — FR and NFR.** Z briefu (Step 0, model danych, §Security, sufficiency A1/A2) →
      `03_REQUIREMENTS/`: FR provenance (źródło + status), FR rodzina jako rekord, FR wiele osób w
      grobie, FR data z dopiskiem, FR nazwisko rodowe · NFR offline (każdy krok UJ-001 w trybie
      samolotowym), NFR odtworzenie na nowym telefonie, NFR migracje schematu, NFR czytelność w słońcu,
      NFR brak danych opuszczających telefon poza kopią.
- [ ] **AC-4 — ADRs.** Z §Architecture → `04_ARCHITECTURE/decisions/`: **ADR-001 local-first** i
      **ADR-002 Flutter z przypiętą wersją** jako `accepted` (decyzje zapadły w kick-offie, ≥3 opcje
      każda); ADR-003 (mapy) i ADR-004 (kopia) jako `proposed` — zamykają je SPIKE-001 i SPIKE-003;
      ADR-005 (dystrybucja) — przy NT-005. Model danych → `04_ARCHITECTURE/data-model.md` (diagram z
      briefu).
- [ ] **AC-5 — Non-technical items.** Sprawdź, że każdy wiersz §6 (N1-N7) ma pozycję w
      `backlog/non-tech/` albo jawnie wskazany dom (N5 → SPIKE-001). Kick-off postawił je — tu tylko
      weryfikacja.
- [ ] **AC-6 — Deferred requirements.** Sprawdź, że każdy wiersz §Security „Deferred" ma pozycję w
      `backlog/deferred/`. Kick-off postawił je — tu tylko weryfikacja.
- [ ] **AC-7 — DOC_MAP.** Każdy folder utworzony w tym zadaniu ma wiersz.
- [ ] **AC-8 — Closed.** `status: done`; `CURRENT_STATE.md` zaktualizowany.

## Manual Verification

```powershell
# w katalogu grobing-vault
Get-ChildItem 03_REQUIREMENTS/epics/*.md          # EPIC-i istnieją
Select-String -Path 00_START_HERE/TRACEABILITY.md -Pattern "^\| UJ-001" | Measure-Object   # 7 kroków ścieżki
Get-ChildItem 04_ARCHITECTURE/decisions/*.md      # ADR-001..004
```

## Next steps after this closes

1. Rozpisanie EPIC-a *Zabezpiecz i przepisz* na US (z kroków / funkcji) — najpierw kopia i odtwarzanie.
2. Normalny łańcuch: `pm` → `planning` → `dev` → `qa` → `docs`.
