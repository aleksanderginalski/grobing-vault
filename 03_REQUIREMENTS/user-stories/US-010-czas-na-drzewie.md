---
title: "US-010 — See how the family changed over time on the tree (czas na drzewie)"
type: user-story
status: ready
epic: "[[EPIC-003-zrozumienie]]"
persona: "[[P1-zbierajacy]]"
moscow: [M10]
journey-steps: "n/a — funkcja widoku 5 (PROJECT_BRIEF §4a)"
FR: ["[[FR-004-data-z-dopiskiem]]", "[[FR-002-rodzina-jako-rekord]]"]
NFR: []
issues: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[drzewo]] v1.4 (element 6, D4) · [[SPIKE-004-mvp-flow-prototype]] D20, D25 · [[rodzina]] v1.4 (dwa tryby związku) · [[SPIKE-002-tree-on-a-phone]]"
created: 2026-10-13
updated: 2026-10-13
---

# US-010 — Czas na drzewie

## Story
**Jako** Zbierający **chcę** przesunąć suwak czasu na drzewie i zobaczyć, kto już żył, kto z kim był razem i kto zmarł, **żeby**
zrozumieć historię rodziny, a nie tylko jej kształt.

## Acceptance Criteria
- **AC-1 — rok na suwaku.** *Given* suwak na roku Y *Then* osoba urodzona po Y znika (jej miejsce zostaje, drzewo nie skacze), a osoba
  zmarła do Y ma znicz ([[drzewo]] element 6).
- **AC-2 — związki w czasie.** *Given* para „razem” od roku A i ze ślubem w roku B *Then* do A nie ma linii, od A jest linia „razem”
  (przerywana), od B — ciągła ([[rodzina]] v1.4, [[drzewo]] D4).
- **AC-3 — odtwarzanie.** *When* dotykam ▶ *Then* czas biegnie od 1880 do dziś w ok. 7 s; ❚❚ zatrzymuje; przy ograniczeniu animacji w
  systemie suwak przeskakuje bez animacji (SC 2.3.3).

## Out of scope
- Drzewo, poziomy, przestawianie środka → [[US-009-drzewo-od-osoby]].

## Notes
- ⚠️ OPEN — **data z dopiskiem i brak daty** ([[FR-004-data-z-dopiskiem]]): jak suwak pokazuje „ok. 1890”, „przed 1920” i osobę bez daty
  urodzenia. Decyzja `ui` przy pozycji (kandydaci na makiecie albo emulatorze, retro 2 R6).
- Kształt M10 rozstrzygnięty: czas jest **na drzewie**, nie na osobnej osi (SPIKE-004 D20; [[EPIC-003-zrozumienie]] → *Open questions*).
- Zależy od [[US-009-drzewo-od-osoby]] (drzewo, układ, wymyślona rodzina w `lib/dev/`).
