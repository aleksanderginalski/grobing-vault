---
title: "ISSUE-003 — Set up adversarial quality critic (`quality`)"
type: issue
status: ready
deferred-until: null
trigger: null
priority: SHOULD
created: 2026-10-05
updated: 2026-10-05
---

# ISSUE-003 — Set up adversarial quality critic (`quality`)

> Zmaterializowane z `PROJECT_BRIEF.md` §How we build, Meta-decyzja 3d: **włączony od razu, poziom
> lekki** (kluczowe pozycje: każda dotykająca warstwy danych + zamknięcie każdej US) — **ale z
> czterema mechanizmami, bez których krytyk jest dekoracją.** NPG nie dostarcza gotowego krytyka —
> zapisuje decyzję i wzorzec.

## What to build
Niezależny agent **tylko do odczytu** (`quality`), który ocenia pozycję **przed** przyjęciem i może ją
zablokować.

- **Werdykt:** `APPROVED` / `CONDITIONAL` / `BLOCK`; tabela `Location | Problem | Severity | Fix`;
  znaleziska kierowane do właściciela (`dev` / `qa` / `docs`) — krytyk nie naprawia.
- **1. Zamknięta lista powodów BLOCK — tylko te:**
  - **ryzyko utraty danych** — ścieżka usuwająca/nadpisująca dane rodziny bez potwierdzenia albo
    przed istnieniem kopii i odtwarzania;
  - **dane rodziny w repo** — prawdziwe imię, data, zdjęcie, pozycja w kodzie, fixture'ach,
    dokumentacji;
  - **fakt o rodzinie zapisany bez źródła/statusu** (FR provenance);
  - **niespełnione kryterium akceptacji**;
  - **Vault-Doc-Sync** — dowieziona zmiana, której nie odbija vault.
  Coś innego „powinno" blokować → krytyk proponuje rozszerzenie listy, **decyduje autor**.
- **2. Obejście zostawia ślad** — autor może zawsze iść dalej, nigdy po cichu; obejście nazywa
  znalezisko, które pomija. Samo „ok, dalej" nie jest obejściem.
- **3. Ocenia subagent bez historii rozmowy** (narzędzie Agent); gdy niemożliwe — raport mówi
  `⚠️ review not independent`.
- **4. Nieprawdziwy self-check to BLOCK**; `APPROVED` bez żadnej uwagi zawiera listę tego, czego
  szukał i nie znalazł.

## Acceptance Criteria
- [ ] `grobing-agents/.claude/skills/quality/SKILL.md` z `SKILL.template.md` NPG; deklaruje: pisze nic
      poza werdyktem w pozycji.
- [ ] Wpięty jako bramka (subagent) w łańcuchu `autonomous-flow.md` przed punktem stopu #3.
- [ ] Lista BLOCK z tego pliku, dosłownie; kolumna Quality Verdict w `TRACEABILITY.md` przechodzi z
      `qa` na `quality`.
- [ ] **Uruchomiony raz naprawdę** na prawdziwej pozycji — ścieżka BLOCK zadziałała albo wykazano, że
      by zadziałała. Krytyk nigdy nieuruchomiony jest nieodróżnialny od niedziałającego.

## Notes / references
- `PROJECT_BRIEF.md` §How we build → 3d · NPG `workflow-library.md` §Review.
