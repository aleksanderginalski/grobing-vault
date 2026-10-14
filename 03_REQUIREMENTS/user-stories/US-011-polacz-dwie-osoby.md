---
title: "US-011 — See how any two people are related, on the tree (połącz dwie osoby)"
type: user-story
status: done
epic: "[[EPIC-003-zrozumienie]]"
persona: "[[P1-zbierajacy]]"
moscow: [M11]
journey-steps: "n/a — funkcja widoku 5 (PROJECT_BRIEF §4a)"
FR: ["[[FR-002-rodzina-jako-rekord]]"]
NFR: []
issues: ["[[ISSUE-039-connect-two-people]]"]
quality-verdict: APPROVED
verdict-date: 2026-10-14
verdict-reviewer: self-check
source: "[[drzewo]] v1.4 (elementy 1, 7–10, D5, D6) · [[SPIKE-004-mvp-flow-prototype]] D21, D26 · [[ISSUE-024-person-view]] (`KinGraph.path`) · [[SPIKE-002-tree-on-a-phone]]"
created: 2026-10-13
updated: 2026-10-14
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
- **Zamknięta 2026-10-14** przez [[ISSUE-039-connect-two-people]] (AC-1–AC-4; decyzje autora na stopie #1: A1, W2, F2, O2, Y1 — [[drzewo]] v1.16–v1.17, D44–D49).
  Przy „Od” innym niż Ty baner mówi w dwóch liniach bez zaimka (O2): „Piotr Przykładowy → Zofia Wymyślona” / „Wnuczka”; przykład AC-3 („…mojej żony”) dotyczy
  „Od” = Ty. Ścieżka szersza niż ekran — drzewo maleje, aż się zmieści (F2), więc brzmienie AC-2 bez zmian.
- Ścieżka już jest: `grobing-code/lib/data/kinship.dart` (`KinGraph.path` — najkrótsza, mniej „para”) z testami ([[ISSUE-024-person-view]]).
- Zależy od [[US-009-drzewo-od-osoby]] (drzewo, poziomy, słownik).
