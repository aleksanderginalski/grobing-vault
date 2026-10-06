---
title: "FR-003 — Several people per grave (burial as a link)"
type: functional-requirement
status: draft
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
used-by: ["[[EPIC-002-wizyta]]"]
user-stories: ["[[US-002-przepisanie-grobu]]"]
NFR: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF Step 0 · §4a step 4 · Data model → Burial"
created: 2026-10-05
updated: 2026-10-06
---

# FR-003 — Wiele osób w grobie

## Requirement
**Pochówek** to powiązanie osoba ↔ grób. **Jeden grób może mieć wiele pochówków**; osoba ma co najwyżej
jeden pochówek.

## Rules
- Grób ≠ osoba: grób to miejsce na cmentarzu (adres kwatery, pinezka, zdjęcia nagrobka); osoby są
  powiązane z nim przez pochówek (`glossary.md` → *grób*, *pochówek*).
- Data pochówku jest zdarzeniem (Event), nie cechą powiązania.
- Miejsce pochówku jest twierdzeniem ze źródłem ([[FR-001-provenance]]).
- **Doprecyzowanie 2026-10-06 (decyzja autora, [[ADR-006-claimed-value-separate-structures]] D2):**
  „co najwyżej jeden pochówek” dotyczy **faktu** — człowiek leży w jednym miejscu — a nie zapisu. Gdy
  źródła podają różne groby, każdy jest osobnym pochówkiem z własnym twierdzeniem; oba zostają
  (`CONTRADICTED`), a pokazuje się pierwszy. Ten sam grób dla tej samej osoby nie występuje dwa razy:
  drugie źródło dla niego to drugie twierdzenie.

## Why durable
Grób rodzinny z kilkoma osobami to norma, nie wyjątek — widok grobu (M4, krok 4 UJ-001) pokazuje
**wszystkich** pochowanych.
