---
title: "EPIC-003 — Zrozumienie (understand: tree, time slider, path)"
type: epic
status: draft
moscow: [M9, M10, M11]
persona: "[[P1-zbierajacy]]"
journey: "n/a — view 5 is a feature set, not a flow (PROJECT_BRIEF §4a)"
FR: ["[[FR-002-rodzina-jako-rekord]]", "[[FR-004-data-z-dopiskiem]]"]
NFR: ["[[NFR-003-migracje-schematu]]", "[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
user-stories: ["[[US-009-drzewo-od-osoby]]", "[[US-010-czas-na-drzewie]]", "[[US-011-polacz-dwie-osoby]]"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §5 M9-M11 · §3b H4, H5, H7 · MD4"
created: 2026-10-05
updated: 2026-10-13
---

# EPIC-003 — Zrozumienie

## Goal
Zbierający widzi całą rodzinę naraz — drzewo z powinowatymi i powtórnymi małżeństwami, zdarzenia na osi
czasu i ścieżkę między dowolnymi dwiema osobami — na ekranie telefonu.

## Stage of the genealogist's process
**Wizualizacja — ostatni etap kanonu** (brief, Step 0; MD4): model etapów opisuje dojrzałość **danych**,
nie oprogramowania, więc ten EPIC jest **ostatni w kolejności pracy**, choć należy do MVP.

> W MVP **z wyboru autora, ponad minimum wartości** (brief §2, back-loop MD4): widok 5 sprawia, że
> wiedza jest *bogatsza do oglądania*, nie *możliwa do zachowania*. Konsekwencja powiedziana na głos:
> **„MVP done" zależy od [[SPIKE-002-tree-on-a-phone]] (H4)**; korzystanie z widoków 1-4 — nie.

## In scope
- **M9 — drzewo rodziny** (widok 5) — budowane na końcu, po odpowiedzi SPIKE-002, czy drzewo z
  powinowatymi jest czytelne na telefonie.
- **M10 — suwak czasu** — urodzenia, małżeństwa, zgony (daty są: H5 KNOWN); na M9 albo jako własna oś.
- **M11 — ścieżka między dowolnymi dwiema osobami** — uogólnienie M5 (ścieżka do „ja"); najkrótsza
  droga po rodzinach, liczona, nigdy zapisywana (H7 — rozwiązany problem grafowy).

User stories wyprowadza się z **tych trzech funkcji**, nie ze ścieżki wizyty (brief §4a). **Rozpisane 2026-10-13** przy zamknięciu
[[SPIKE-002-tree-on-a-phone]] (*Findings* → *Rekomendacja*): [[US-009-drzewo-od-osoby]] (M9) → [[US-010-czas-na-drzewie]] (M10) →
[[US-011-polacz-dwie-osoby]] (M11), w tej kolejności.

- **C3 — nazwy pokrewieństwa złożone z odcinków** („siostra cioteczna babci mojej żony”) — **w zakresie** od decyzji autora na stopie #1
  [[ISSUE-024-person-view]] (2026-10-09: *„przypadki np. Brat stryjeczny prababki lub podobne zrobimy w widoku drzewa przy łączeniu różnych
  osób”*); słownik → [[US-009-drzewo-od-osoby]] AC-5. Pojedyncze nazwy jednego kroku są już w widoku osoby ([[ISSUE-025-gender-kinship-together-since]]).

## Out of scope
- M5 ścieżka do „ja" → [[EPIC-002-wizyta]] (widok osoby).
- ~~C3 nazwanie ścieżki polskimi terminami pokrewieństwa (teść, szwagier…) — H8, DEFER.~~ → w zakresie (wyżej, decyzja autora 2026-10-09).
- Całe drzewo naraz — nie w MVP ([[drzewo]] D1, stop #1 SPIKE-002, 2026-10-13).
- A6 podwójne datowanie sprzed 1918 r. (juliański / gregoriański) — Won't (now); kwalifikator daty +
  źródło uniosą to, jeśli się pojawi.

## Prior art
Przegląd z kick-offu (`kickoff/SESSION_STATE.md` → *Prior-art scan*, 2026-10-05): **ścieżka między
dwiema osobami (M11)** jest w **Gramps** (filtr „Relationship path between…”; gramplet Deep Connections,
który według użytkowników się zawiesza albo idzie drzewem w złą stronę), w **FamilySearch** i w
**MyHeritage**. Drzewa te narzędzia rysują na komputerze albo w przeglądarce i zwykle tylko w liniach
krwi (brief §3b H4). [[SPIKE-002-tree-on-a-phone]] i US tego EPIC-a zaczynają od nich. Dopisane przy
przeglądzie `kickoff/` (retro 1, R4, 2026-10-06).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[SPIKE-002-tree-on-a-phone]] (H4) | technical | `done` (2026-10-13) — czytelnie od osoby, z przesuwaniem; własny układ. Zadanie na czas na telefonie → [[ISSUE-032-mvp-install]] → *Hand checks* |
| [[FR-002-rodzina-jako-rekord]] | functional | rodzina jako rekord — bez tego powtórne małżeństwo psuje drzewo |
| [[FR-004-data-z-dopiskiem]] | functional | suwak musi umieć „ok. 1890" i „przed 1920" |
| [[EPIC-001-zabezpiecz-i-przepisz]] | product | drzewo z ~100 osób wymaga przepisanych danych |

## Open questions
- brak `⚠️ OPEN` w zakresie z briefu. ~~Kształt M10 (na drzewie czy osobna oś) rozstrzyga się po SPIKE-002.~~ → **na drzewie**
  (SPIKE-004 D20, [[drzewo]] element 6; [[US-010-czas-na-drzewie]]). Otwarte w US: data z dopiskiem na suwaku ([[US-010-czas-na-drzewie]]
  → *Notes*), imiona przy oddalaniu ([[drzewo]] *Open* 5).
