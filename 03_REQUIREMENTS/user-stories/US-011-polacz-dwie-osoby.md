---
title: "US-011 — See how any two people are related, on the tree (połącz dwie osoby)"
type: user-story
status: ready
epic: "[[EPIC-003-zrozumienie]]"
persona: "[[P1-zbierajacy]]"
moscow: [M11]
journey-steps: "n/a — funkcja widoku 5 (PROJECT_BRIEF §4a)"
FR: ["[[FR-002-rodzina-jako-rekord]]"]
NFR: []
issues: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[drzewo]] v1.4 (elementy 1, 7–10, D5, D6) · [[SPIKE-004-mvp-flow-prototype]] D21, D26 · [[ISSUE-024-person-view]] (`KinGraph.path`) · [[SPIKE-002-tree-on-a-phone]]"
created: 2026-10-13
updated: 2026-10-13
---

# US-011 — Połącz dwie osoby

## Story
**Jako** Zbierający **chcę** wybrać dowolne dwie osoby i zobaczyć na drzewie, jak się łączą, z nazwą pokrewieństwa, **żeby** od razu
wiedzieć, kim ktoś z grobu jest dla mnie albo dla kogoś z rodziny.

## Acceptance Criteria
- **AC-1 — wybór osób.** *When* dotykam ikony „Połącz dwie osoby” *Then* otwiera się okno z kaflami „Od” (domyślnie „Ja”) i „Do”; kafel
  prowadzi do listy jak [[osoby]] (wyszukiwarka i A–Z); wybór drugiej osoby zamyka okno ([[drzewo]] element 7).
- **AC-2 — ścieżka na drzewie.** *Then* drzewo przechodzi na najniższy poziom, na którym widać obie osoby, ustawia ścieżkę w kadrze,
  wyszarza osoby spoza ścieżki, a linia w akcencie biegnie od osoby do osoby (ok. 0,7 s na krok); przy ograniczeniu animacji w systemie —
  od razu cała ścieżka ([[drzewo]] element 8, D5).
- **AC-3 — baner z nazwą.** *Then* na ok. 4 s u góry drzewa jest baner z opisem pokrewieństwa ze słownika z [[US-009-drzewo-od-osoby]] AC-5,
  np. „Siostra cioteczna babci mojej żony”; dotknięcie drzewa albo wstecz kończy podświetlenie ([[drzewo]] element 9, D6).
- **AC-4 — bez ścieżki.** *Given* osoby, które się nie łączą *Then* baner „Te osoby nie łączą się — w drzewie brakuje rodziny między
  nimi.”, drzewo bez zmian ([[drzewo]] element 10).

## Out of scope
- Słownik nazw złożonych → [[US-009-drzewo-od-osoby]] AC-5 (pierwsza potrzebuje go karta osoby w środku).

## Notes
- Ścieżka już jest: `grobing-code/lib/data/kinship.dart` (`KinGraph.path` — najkrótsza, mniej „para”) z testami ([[ISSUE-024-person-view]]).
- Zależy od [[US-009-drzewo-od-osoby]] (drzewo, poziomy, słownik).
