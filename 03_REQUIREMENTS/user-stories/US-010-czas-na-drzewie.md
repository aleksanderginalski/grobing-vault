---
title: "US-010 — See how the family changed over time on the tree (czas na drzewie)"
type: user-story
status: done
epic: "[[EPIC-003-zrozumienie]]"
persona: "[[P1-zbierajacy]]"
moscow: [M10]
journey-steps: "n/a — funkcja widoku 5 (PROJECT_BRIEF §4a)"
FR: ["[[FR-004-data-z-dopiskiem]]", "[[FR-002-rodzina-jako-rekord]]"]
NFR: []
issues: ["[[ISSUE-037-time-on-the-tree]]", "[[ISSUE-038-history-on-tv-and-tempo]]"]
quality-verdict: APPROVED
verdict-date: 2026-10-14
verdict-reviewer: self-check
source: "[[drzewo]] v1.4 (element 6, D4) · [[SPIKE-004-mvp-flow-prototype]] D20, D25 · [[rodzina]] v1.4 (dwa tryby związku) · [[SPIKE-002-tree-on-a-phone]]"
created: 2026-10-13
updated: 2026-10-14
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
- **AC-3 — odtwarzanie.** *When* dotykam ▶ *Then* czas biegnie od początku suwaka (najpóźniej 1880) do dziś **w wybranym tempie — domyślnie „Średnio”, od 1880
  ok. 15 s; „Wolno” ok. 29 s, „Szybko” ok. 7 s**; ❚❚ zatrzymuje; przy ograniczeniu animacji w systemie suwak przeskakuje bez animacji (SC 2.3.3). *(2026-10-14:
  „od 1880” → „od początku suwaka” — T2, decyzja autora na stopie #1 [[ISSUE-037-time-on-the-tree]], [[drzewo]] D34; przeskok co dekadę — R2, D36. 2026-10-14:
  „od 1880 w ok. 7 s” → tempo — V2, decyzja autora na stopie #1 [[ISSUE-038-history-on-tv-and-tempo]], [[drzewo]] D41.)*

## Out of scope
- Drzewo, poziomy, przestawianie środka → [[US-009-drzewo-od-osoby]].

## Notes
- ~~⚠️ OPEN — data z dopiskiem i brak daty~~ — **rozstrzygnięte 2026-10-14: N3** (stop #1 [[ISSUE-037-time-on-the-tree]], *„tak”*; [[drzewo]] D32): okno daty
  i przerywany obrys „nie wiadomo, czy w tym roku żyje”, znicz dopiero na pewno. Zbudowane w [[ISSUE-037-time-on-the-tree]].
- Historia na telewizorze i wybór tempa (autor: *„dla mnie za szybko”*) → [[ISSUE-038-history-on-tv-and-tempo]] — zamknięta 2026-10-14 (L1, B2, V2, Z2).
- Kształt M10 rozstrzygnięty: czas jest **na drzewie**, nie na osobnej osi (SPIKE-004 D20; [[EPIC-003-zrozumienie]] → *Open questions*).
- Zależy od [[US-009-drzewo-od-osoby]] (drzewo, układ, wymyślona rodzina w `lib/dev/`).
