---
title: "EPIC-002 — Wizyta (the visit)"
type: epic
status: draft
moscow: [M2, M3, M4, M5, M6, M7]
persona: "[[P1-zbierajacy]]"
journey: "UJ-001 (PROJECT_BRIEF §4a) — steps 1-7"
FR: ["[[FR-001-provenance]]", "[[FR-002-rodzina-jako-rekord]]", "[[FR-003-wiele-osob-w-grobie]]"]
NFR: ["[[NFR-001-offline]]", "[[NFR-003-migracje-schematu]]", "[[NFR-004-czytelnosc-w-sloncu]]", "[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
user-stories: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §4a · §5 M2-M7 · §3b H3, H9"
created: 2026-10-05
updated: 2026-10-05
---

# EPIC-002 — Wizyta

## Goal
W okolicach 1 listopada Zbierający znajduje każdy grób rodziny na odwiedzanym cmentarzu, widzi, kto w
nim leży i jak łączy się z nim — bez otwierania papierowych notatek, także bez zasięgu — i poprawia
zapis na miejscu.

## Stage of the genealogist's process
**Weryfikacja na miejscu** — po zabezpieczeniu, przepisaniu i rozmowie ze Źródłem (brief, Step 0). Ten
EPIC niesie **główną ścieżkę produktu** (UJ-001, wybór autora w §4a) — US wyprowadza się z jej kroków.

## In scope
| M | Co | Krok UJ-001 |
|---|---|---|
| M2 | mapa Polski z cmentarzami rodziny (widok 1) | 1 |
| M3 | mapa cmentarza z pinezkami grobów, adresem kwatery, linkiem do Grobonetu tam, gdzie cmentarz jest pokryty (widok 2) | 2, 7 |
| M4 | widok grobu — wszyscy pochowani, zdjęcie + imię (widok 3) | 3, 4 |
| M5 | widok osoby — kim była, relacje, **ścieżka do „ja"** (widok 4) | 5 |
| M6 | poprawa na miejscu — pinezka tam, gdzie stoję; nowe zdjęcie nagrobka; imię z tablicy | 6 |
| M7 | działa bez zasięgu ([[NFR-001-offline]]) | 2-7 (gałąź) |

Krok 6 to **jedyne miejsce, gdzie powstają ręczne pinezki** (H3) — każda zapisana ze źródłem i
dokładnością ([[FR-001-provenance]]).

## Out of scope
- Wprowadzanie danych z notatek i od babci (M1) i kopia (M8) → [[EPIC-001-zabezpiecz-i-przepisz]].
- Widok 5 (M9-M11) → [[EPIC-003-zrozumienie]].
- C1 „odwiedzony w tym roku" · C4 wskazówki dojścia do grobu · S5 wyszukiwanie · W3 kopiowanie danych
  Grobonetu · W6 rocznice śmierci.
- **Grób ze zdjęcia z galerii (pinezka z lokalizacji zdjęcia)** — nierozstrzygnięte, poza zakresem do
  decyzji autora: `01_INBOX/2026-10-05-1-listopada-zbieranie.md`.

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[SPIKE-001-map-source-offline]] → [[ADR-003-map-source-offline]] | technical | ADR `proposed` — **widoki 1-2 czekają na spike** |
| [[NT-004-grobonet-link-terms]] | legal (hipoteza) | `open` — link, nigdy kopia |
| [[NT-006-visual-guidelines]] | visual | `open` — styl B + czytelność w słońcu |
| [[EPIC-001-zabezpiecz-i-przepisz]] | product | krok 1 jest pusty bez przepisanych danych |

## Open questions
- ⚠️ **OPEN — gałąź „grób bez pinezki".** Brief §4a: *„Grave with no pin yet (only a plot address from
  the notes) → step 2 shows the address and the Grobonet link"*. **Po korekcie autora (2026-10-05)
  notatki nie mają adresów kwater**, więc przy pierwszej wizycie taki grób nie ma ani pinezki, ani
  adresu — krok 2 może pokazać co najwyżej link do Grobonetu (jeśli cmentarz jest pokryty). **Jak
  Zbierający znajduje go na miejscu?** Decyzja autora — `00_START_HERE/TRACEABILITY.md` → *Open gaps* 1.
  Brief się nie zmienia (`kickoff/` = zapis decyzji); poprawiona gałąź żyje tutaj do czasu decyzji.
- Krok 3 („porównanie z zapisanym zdjęciem nagrobka") przy pierwszej wizycie nie ma zdjęcia do
  porównania — notatki nie niosą zdjęć (brief §1); zdjęcie powstaje dopiero w kroku 6. Brief nie mówi, co
  krok 3 robi wtedy — ta sama sytuacja pierwszej wizyty co wyżej, część *Open gaps* 1.
