---
title: "US-006 — Export readable without the app (eksport dla rodziny)"
type: user-story
status: ready
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M8]
journey-steps: "n/a — poza ścieżką (M8)"
FR: []
NFR: ["[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
ADR: ["[[ADR-004-backup-format-encryption-destination]]"]
issues: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §5 M8 · §Security (backup vs export, output encoding) · Sufficiency A4"
created: 2026-10-05
updated: 2026-10-05
---

# US-006 — Eksport dla rodziny

## Story
**Jako** Zbierający **chcę** wygenerować eksport, który rodzina otworzy bez aplikacji i za 30 lat,
**żeby** zapis przeżył i mnie, i aplikację.

## Acceptance Criteria
- **AC-1 — HTML i PDF bez aplikacji.** *When* generuję eksport *Then* powstaje samodzielny HTML i PDF z
  osobami, rodzinami, grobami i datami z dopiskiem (bez źródeł — [[SPIKE-004-mvp-flow-prototype]] D28), otwierany zwykłą przeglądarką
  ([[ADR-004-backup-format-encryption-destination]] → *Eksport (A4)*).
- **AC-2 — znaki specjalne bezpieczne.** *Given* imię albo „kim była" ze znakami specjalnymi HTML *Then*
  eksport pokazuje je jako tekst (§Security, output encoding).
- **AC-3 — eksport nie idzie do chmury sam.** *When* eksport powstaje *Then* zapisuję go tam, gdzie wskażę;
  aplikacja nie wysyła go nigdzie automatycznie ([[NFR-005-dane-nie-opuszczaja-telefonu]]).

## Out of scope
- Eksport GEDCOM (C2), szyfrowanie eksportu (czytelność jest jego celem — `glossary.md` → *eksport*).
- Notka przekazania dla rodziny → [[NT-007-hand-over-note]] (poza kodem).

## Notes
- Osoby żyjące: model ma `is_living`, które „steruje prywatnością w eksporcie" (data-model.md → *Person*).
  Co dokładnie ukrywać u żyjących, rozstrzyga planowanie pierwszego ISSUE tej US.
- Eksport żyje offline u rodziny (NFR-005 → *Notes*); kiedy i jak często go odświeżać — [[NT-007-hand-over-note]].
