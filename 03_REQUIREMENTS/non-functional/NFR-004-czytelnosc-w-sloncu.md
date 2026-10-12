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
updated: 2026-10-12
---

# NFR-004 — Czytelność w słońcu

## Requirement
Ekrany wizyty są **czytelne w pełnym słońcu**. Styl B jest ciemny (prawie czarne tło, szary tekst,
bursztynowy akcent), a wizyta odbywa się w dzień, na cmentarzu — ciemny interfejs w słońcu to klasyczna
porażka na zewnątrz (A2).

| | |
|---|---|
| **Metric** | kontrast tekstu, który czyta się przy grobie (adres, liczby, stan planu), na ekranach wizyty — WCAG 2.2 SC 1.4.6 (AAA); i ocena autora w pełnym słońcu na telefonie |
| **Target** | **≥ 7:1** dla tego tekstu (dziś kolor tekstu: 10,02:1 na powierzchni, 10,98:1 na tle); w tekście pomocniczym (5,01:1) zostaje tylko to, czego nie czyta się przy grobie (np. podpisy źródeł). **Decyzja autora 2026-10-12** — W2 na stopie #1 [[ISSUE-027-cemetery-map-plan-photo-states]] (pierwszy ekran wizyty: [[cmentarz]]) |
| **Method** | ręczna weryfikacja **na miejscu**, w słońcu (stop #2 przy ekranach wizyty) |
| **Verification trigger** | pierwszy ekran wizyty · każda wizyta na cmentarzu w dzień |

## Notes
- ✅ **Miara przyjęta 2026-10-12** (W2, ISSUE-027): stosuje ją [[cmentarz]] v5 (el. 2a, 6, 7, 8 (c)), dalsze ekrany wizyty — [[grob]]
  przy M4, pinezka (US-008) — przy swoich pozycjach. **Test w słońcu dalej nie zrobiony** — telefon, build release, przy instalacji
  MVP ([[NT-006-visual-guidelines]]).
- Jeśli nie przechodzi → **wariant wysokokontrastowy** (brief A2) — nie rezygnacja ze stylu B.
- Ekrany widoku 5 ([[EPIC-003-zrozumienie]]) nie są używane na cmentarzu — poza tym NFR.
