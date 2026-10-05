---
title: "NFR-004 — Visit screens readable in direct sunlight"
type: non-functional-requirement
status: draft
epic: ["[[EPIC-002-wizyta]]"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §Architecture → Sufficiency pass A2 · §6a (Style B) · §6 N7"
created: 2026-10-05
updated: 2026-10-05
---

# NFR-004 — Czytelność w słońcu

## Requirement
Ekrany wizyty są **czytelne w pełnym słońcu**. Styl B jest ciemny (prawie czarne tło, szary tekst,
bursztynowy akcent), a wizyta odbywa się w dzień, na cmentarzu — ciemny interfejs w słońcu to klasyczna
porażka na zewnątrz (A2).

| | |
|---|---|
| **Metric** | ⚠️ **OPEN** — brief nie podaje miary (np. progu kontrastu); do ustalenia w [[NT-006-visual-guidelines]] |
| **Target** | ⚠️ **OPEN** — j.w. |
| **Method** | ręczna weryfikacja **na miejscu**, w słońcu (stop #2 przy ekranach wizyty) |
| **Verification trigger** | pierwszy ekran wizyty · każda wizyta na cmentarzu w dzień |

## Notes
- Jeśli nie przechodzi → **wariant wysokokontrastowy** (brief A2) — nie rezygnacja ze stylu B.
- Ekrany widoku 5 ([[EPIC-003-zrozumienie]]) nie są używane na cmentarzu — poza tym NFR.
