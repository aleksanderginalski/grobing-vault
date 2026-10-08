---
title: "US-008 — Pin a grave where I stand, fix it on the spot, see where I am (pinezka na miejscu)"
type: user-story
status: ready
epic: "[[EPIC-002-wizyta]]"
persona: "[[P1-zbierajacy]]"
moscow: [M6, M7]
journey-steps: "UJ-001 · 6 (poprawa na miejscu)"
FR: []
NFR: ["[[NFR-001-offline]]", "[[NFR-004-czytelnosc-w-sloncu]]"]
issues: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[SPIKE-004-mvp-flow-prototype]] D22 · [[cmentarz]] v4.2 (elementy 10–14) · [[grob]] v5.1 · H3"
created: 2026-10-08
updated: 2026-10-08
---

# US-008 — Pinezka na miejscu

## Story
**Jako** Zbierający **chcę** stojąc przy grobie postawić albo poprawić jego pinezkę jednym dotknięciem, **żeby** następnym
razem trafić do grobu bez szukania.

## Acceptance Criteria
- **AC-1 — gdzie jestem.** *When* dotykam „gdzie jestem” na planie *Then* widzę niebieską kropkę i koło dokładności;
  pierwsze użycie pyta o uprawnienie lokalizacji, a odmowa zostawia ręczne stawianie.
- **AC-2 — postaw pinezkę.** *Given* grób bez pinezki *When* w widoku grobu dotykam „Postaw pinezkę” *Then* mapa pokazuje
  pinezkę w kropce; dotknięcie planu ją przesuwa; „Zapisz pinezkę” zapisuje ją z dokładnością i datą.
- **AC-3 — popraw pinezkę.** *Given* grób z pinezką *When* w arkuszu grobu dotykam „Popraw pinezkę” *Then* wchodzę w ten sam
  tryb dla tego grobu.
- **AC-4 — bez internetu.** *Given* tryb samolotowy *Then* „gdzie jestem” i stawianie pinezki działają na planie offline.

## Out of scope
- Plan, kwatery, stany mapy → [[US-007-mapa-cmentarza]].

## Notes
- **Dokładność GPS przy grobie** mierzy wizyta (`CURRENT_STATE.md` → *Parked*). Próg „słaby sygnał” ([[cmentarz]]
  element 12) ustala ten pomiar.
- Wymaga telefonu w terenie (wyjątek w `DEFINITION_OF_DONE.md`: GPS na miejscu, build release).
