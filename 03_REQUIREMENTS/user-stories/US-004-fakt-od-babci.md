---
title: "US-004 — Record what grandmother says, even against the notes (fakt od babci)"
type: user-story
status: withdrawn
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M1]
journey-steps: "n/a — poza ścieżką (M1, źródło „babcia")"
FR: ["[[FR-001-provenance]]"]
NFR: []
issues: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §2 („every conversation with grandmother ends with new facts in the app") · §5 M1 · Step 0 (WZ-036) · DoD PRODUCT"
created: 2026-10-05
updated: 2026-10-05
---

# US-004 — Fakt od babci obok notatek

> **Wycofana decyzją autora 2026-10-08 ([[SPIKE-004-mvp-flow-prototype]] D28, D27).** Autor: *„Babcia to po prostu jedna z osób które dadzą mi wkład
> do tego co później wrzucę do notatek o danej osobie - nie ma potrzeby mieć tam źródła. Po rozmowie z babią normalnie
> wszedłbym na edycje danej osoby i dodał o niej informacje.”* oraz *„a to jakiś błąd się wkradł w takim razie - moje notatki to moje notatki, nie potrzeba żadnych potwierdzeń skąd pochodzą”*. **Wiedza od babci wchodzi zwykłą poprawą
> wpisu** ([[wpis-osoby]], ✎ w [[osoba]]). Linia DoD produktu „co najmniej jedna rozmowa z babcią dodała fakty spoza
> notatek” zostaje — mierzy ją autor, nie aplikacja. Treść niżej — historia.

## Story
**Jako** Zbierający **chcę** w trakcie rozmowy z babcią dopisać, co pamięta, także gdy przeczy notatkom,
**żeby** każda rozmowa kończyła się nowymi faktami w aplikacji, a żadne źródło nie nadpisywało drugiego.

## Acceptance Criteria
- **AC-1 — drugie twierdzenie obok pierwszego.** *Given* osoba ma datę ze źródłem „notatki" *When*
  dopisuję inną datę ze źródłem „babcia" *Then* oba twierdzenia istnieją, mają status `CONTRADICTED` i
  żadne nie jest usunięte ([[FR-001-provenance]] → *Rules*).
- **AC-2 — potwierdzenie.** *Given* twierdzenie `CLAIMED` *When* drugie, niezależne źródło mówi to samo
  *Then* status zmienia się na `CONFIRMED`.
- **AC-3 — „nie wiem" jest daną.** *When* babcia nie pamięta *Then* mogę zapisać `UNKNOWN` przy tym fakcie.
- **AC-4 — źródło widać przy fakcie.** *When* oglądam osobę *Then* przy datach, relacjach i miejscu
  pochówku widzę źródło i status.

## Out of scope
- Przegląd statusów „czy to nadal prawda?" → ⚠️ OPEN w [[FR-001-provenance]] (kto, kiedy i jak).
- Nagrania rozmów, transkrypcja — poza briefem.

## Notes
- Ta US czyni sprawdzalną linię DoD produktu: *„co najmniej jedna rozmowa z babcią dodała fakty spoza
  notatek"* (`DEFINITION_OF_DONE.md` → *PRODUCT*).
- W vaulcie tylko pytania do babci **bez danych rodziny**; odpowiedzi trafiają do aplikacji
  (`family-data.md`, `CURRENT_STATE.md` → *Parked*).
