---
title: "FR-001 — Provenance: every disputed fact carries its source and status"
type: functional-requirement
status: draft
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
used-by: ["[[EPIC-002-wizyta]]"]
user-stories: []
NFR: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF Step 0 (Genealogical Proof Standard, pattern WZ-036) · §5a G3 · Data model → Assertion"
created: 2026-10-05
updated: 2026-10-05
---

# FR-001 — Provenance

## Requirement
Każde **twierdzenie** o **datach, relacjach i miejscu pochówku** jest zapisane razem z:
- **źródłem** — nagrobek · notatki · babcia · krewny · akt;
- **statusem** — `CLAIMED` (jedno źródło) · `CONFIRMED` (drugie, niezależne) · `CONTRADICTED` (źródła się
  różnią) · `UNKNOWN` (wiem, że nie wiem);
- **kiedy** zostało zapisane i **kto** je podał.

Pole „kim była" (tekst wolny) niesie **jedną linię źródła** dla całego tekstu.

## Rules
- **Dwa sprzeczne twierdzenia współistnieją.** `CONTRADICTED` się nie usuwa — to wynik, nie błąd
  (kanon: rozstrzyganie sprzecznych dowodów; „babcia mówi" i „nagrobek mówi" to dwa źródła).
- Status mówi, **jak mocne** jest twierdzenie, nie **czy jest prawdziwe** (granica wzorca WZ-036) — wzorzec
  wymaga okresowego przeglądu „czy to nadal prawda?". ⚠️ **OPEN:** brief nie mówi, kto, kiedy i jak
  przegląda statusy twierdzeń **w aplikacji**. Pytanie o nośne fakty co 10 zamkniętych pozycji (3g) dotyczy
  faktów o **projekcie** w vaulcie — twierdzeń o rodzinie tam nie ma i nie będzie, więc tej luki nie pokrywa.
- Pinezka grobu to też twierdzenie o położeniu: **jak powstała** (zdjęcie satelitarne / GPS na miejscu)
  + dokładność (model danych → *Grave*).

## Why durable
Zapis ma przeżyć autora. Fakt bez źródła nie daje się później poprawić — rodzina po autorze nie będzie
wiedziała, czy „ok. 1890" pochodzi z nagrobka, czy z pamięci. To pierwsza zasada kanonu genealogii
(brief §5a G3, rozstrzygnięte przez Step 0).

## Cost decision (said out loud in the kick-off)
Źródło **na każdym polu** spowolniłoby przepisywanie ~100 osób (G6). Dlatego: twierdzenia na datach,
relacjach i miejscu pochówku — to, o co się spiera; reszta bez osobnego źródła.

## Verification
DoD ISSUE: *„zapisuje fakt o rodzinie → źródło + status zapisane"* — `qa` sprawdza przy każdej funkcji,
która zapisuje fakt o rodzinie (MD3).
