---
title: "NT-006 — Visual guidelines for Style B + readability in direct sunlight"
type: non-code-item
status: open
category: visual
priority: SHOULD
source: "PROJECT_BRIEF §6 N7, §6a, sufficiency A2"
wake-condition: "the first screen to design (also the trigger to propose the `ui` agent)"
created: 2026-10-05
updated: 2026-10-06
---

# NT-006 — Wytyczne wizualne (styl B) + czytelność w słońcu

## The question / task
Spisać wytyczne stylu B: nowoczesny · minimalistyczny · godny; tło prawie czarne, miękka szarość,
**jeden akcent: ciepły bursztyn jak światło znicza**, cienkie ikony, czysty krój bezszeryfowy.
Rozstrzygnąć **czytelność w pełnym słońcu** — wizyta odbywa się w dzień, na cmentarzu; ciemny interfejs
to klasyczny problem na zewnątrz → wariant o wysokim kontraście, jeśli test na miejscu wypadnie źle.

## Why it matters
Ton aplikacji (zmarli, 1 listopada, obok rodziny) i używalność głównego przepływu w miejscu, gdzie jest
używany. Folder `05_DESIGN/brand/` powstaje na ten sygnał (`doc-growth.md`).

## Resolution (fill when done — this is the DoD)
- ✅ **Wytyczne:** `05_DESIGN/brand/style-b.md` v1.2 (2026-10-06), napisane przez agenta `ui`
  ([[ISSUE-013-setup-ui-agent]]) i wyrównane do obrazów z kick-offu (`05_DESIGN/brand/references.md`,
  R1–R4) po uwagach autora.
- ⏳ **Test w słońcu:** nie zrobiony. Wymaga telefonu, buildu release i pełnego słońca
  (`DEFINITION_OF_DONE.md` → wyjątki). Miara [[NFR-004-czytelnosc-w-sloncu]] nadal `⚠️ OPEN`; kandydat 7:1 i
  jego skutek dla tekstu pomocniczego są w `style-b.md` → *Measurement*. **Pozycja zostaje `open`** do
  testu na telefonie.
