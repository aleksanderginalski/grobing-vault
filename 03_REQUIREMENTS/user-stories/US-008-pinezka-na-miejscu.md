---
title: "US-008 — Pin a grave where I stand, fix it on the spot, see where I am (pinezka na miejscu)"
type: user-story
status: done
epic: "[[EPIC-002-wizyta]]"
persona: "[[P1-zbierajacy]]"
moscow: [M6, M7]
journey-steps: "UJ-001 · 6 (poprawa na miejscu)"
FR: []
NFR: ["[[NFR-001-offline]]", "[[NFR-004-czytelnosc-w-sloncu]]"]
issues: ["[[ISSUE-029-pin-on-site-gps]]"]
quality-verdict: APPROVED
verdict-date: 2026-10-12
verdict-reviewer: self-check
source: "[[SPIKE-004-mvp-flow-prototype]] D22 · [[cmentarz]] v4.2 (elementy 10–14) · [[grob]] v5.1 · H3"
created: 2026-10-08
updated: 2026-10-12
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
- **Rozpisana 2026-10-12** (`docs` w auto-flow po `pm`) na jedną pozycję, [[ISSUE-029-pin-on-site-gps]] (AC-1–AC-4).
  **Cel autora:** build release na telefonie przed zaduszkami (~2026-11-02), żeby jedna wizyta dała pomiar z *Parked* i
  sprawdzenie AC-1 i AC-4 w terenie. Do tego czasu próg „słaby sygnał” jest tymczasowy. Kandydaci z [[cmentarz]] D29 →
  [[ISSUE-030-sector-on-a-visit]] (`draft`, decyzja autora).

## Closure
> `docs`, 2026-10-12. **Zamknięta** z [[ISSUE-029-pin-on-site-gps]] — jedyną pozycją, która pokrywa AC-1–AC-4. Werdykt US to werdykt tej
> pozycji (`qa`: APPROVED, self-check, z uwagami — ISSUE-029 → *Verification*); osobnego przeglądu na poziomie US nie było, bo US = jedna
> pozycja (inaczej niż [[US-007-mapa-cmentarza]]).

- AC-1–AC-4: testy happy-path i przejście na emulatorze; stop #2 „ok” (poprawa pinezki sprawdzona na urządzeniu).
- **Otwarte, nie blokuje (decyzja autora na stopie #1 ISSUE-029, D4):** AC-1 i AC-4 na prawdziwym GPS i w terenie — wizyta na cmentarzu,
  `CURRENT_STATE.md` → *Parked*; tam też próg „słaby sygnał” (tymczasowo 15 m).
- Źródło lokalizacji: [[ADR-017-location-from-gnss-only]]; dane: [[data-model]] → schemat v12.
