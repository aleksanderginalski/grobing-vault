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
updated: 2026-10-08
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
  decyzji autora: `TRACEABILITY.md` → *Open gaps* 2 (SPIKE-001 zamknięty 2026-10-08 bez rozstrzygnięcia tej funkcji). Plan
  zarządcy jako trzecie źródło położenia odpadł, bo nie wolno go kopiować ([[ADR-003-map-source-offline]]).
  Kwatery zaznacza autor (sekcja niżej).

## Prior art
Przegląd z kick-offu (`kickoff/SESSION_STATE.md` → *Prior-art scan*, 2026-10-05): każdy widok istnieje
osobno. Widoki 1–2: **Grobonet** (mapa cmentarza, adres sektor/rząd/miejsce) i **BillionGraves** (zdjęcia
nagrobków z GPS na mapie). Widok 3: **Graveyard Navigator** (linie do grobów rodziny w jednym
cmentarzu). Widok 4: dowolne narzędzie do drzewa i **Geneteka** (indeksy akt PTG). Planując US tego
EPIC-a, zacznij od nich. Dopisane przy przeglądzie `kickoff/` (retro 1, R4, 2026-10-06).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[SPIKE-001-map-source-offline]] → [[ADR-003-map-source-offline]] | technical | ✅ `accepted` 2026-10-08 — plan schematyczny OSM offline, ortofotomapa GUGiK online, kwatery i pinezki autora |
| [[NT-004-grobonet-link-terms]] | legal | ✅ `done` 2026-10-08 — regulamin nie zakazuje linku, zakazuje kopiowania: link, nigdy kopia |
| [[NT-006-visual-guidelines]] | visual | `open` — styl B + czytelność w słońcu |
| [[EPIC-001-zabezpiecz-i-przepisz]] | product | krok 1 jest pusty bez przepisanych danych |

## Input from SPIKE-001 (2026-10-08) — for the first US of this EPIC
Decyzje autora po szkicu na emulatorze ([[SPIKE-001-map-source-offline]] → *Verification*,
[[ADR-003-map-source-offline]]):
- **Mapa cmentarza (widok 2) to plan schematyczny** w stylu B, *„jak Grobonet, w naszych kolorach”*: obrys i
  alejki z OSM, offline, pobrane przy dodaniu cmentarza; bez sieci zaślepka. Zdjęcie z góry (ortofotomapa)
  jest tylko online, jako warstwa;
- **kwatera** to nazwana strefa, którą autor zaznacza sam według planu zarządcy, i tylko tam, gdzie leży rodzina.
  Autor wcześniej myślał o kwaterze jak o miejscu jednego grobowca; w danych to sektor z wieloma grobami
  (`glossary.md` → *kwatera*);
- **grób** ma pinezkę w kwaterze i adres zarządcy (kwatera, rząd, miejsce). **Siatki grobów nie ma** (to dane
  zarządców);
- pomysł autora z 2026-10-08: *„można tam dodać kwatery ale ich lokalizacja będzie dostępna dopiero gdy będziemy
  mieć plan cmentarza”*, czyli kwatera może istnieć bez strefy, a strefę dostaje później;
- pole „link do wyszukiwarki zarządcy” zamiast „link do Grobonetu” (*Findings* → rekomendacja 6) czeka na
  decyzję autora przy tej US.

Wygląd projektuje `ui` (makieta przed kodem, retro 1 R5). [[cmentarz]] D1 zakładał zdjęcie nad listą, więc jest
do zmiany.

## Open questions
- ✅ **Kierunek dla gałęzi „grób bez pinezki” (autor, 2026-10-08, stop #2 [[SPIKE-001-map-source-offline]]):**
  1. w domu autor szuka grobu po nazwisku w **wyszukiwarce zarządcy**, którą ma każdy z jego cmentarzy (*Findings*
     → M1–M3), i przepisuje adres;
  2. z **planu zarządcy** wie, w której kwaterze jest grób, i zaznacza tę kwaterę w aplikacji;
  3. na miejscu idzie do kwatery planem offline i GPS-em i **stawia pinezkę** przy grobie (krok 6).

  Autor: *„mając plan cmentarza — wiem w której kwaterze jest mój grób a potem … zaznaczyłbym pinezką gdzie jest
  grób”*. Czy to wystarcza w terenie, sprawdzi wizyta (`CURRENT_STATE.md` → §Parked). Niżej zostaje
  pierwotny opis luki:
- ⚠️ **OPEN — gałąź „grób bez pinezki".** Brief §4a: *„Grave with no pin yet (only a plot address from
  the notes) → step 2 shows the address and the Grobonet link"*. **Po korekcie autora (2026-10-05)
  notatki nie mają adresów kwater**, więc przy pierwszej wizycie taki grób nie ma ani pinezki, ani
  adresu — krok 2 może pokazać co najwyżej link do Grobonetu (jeśli cmentarz jest pokryty). **Jak
  Zbierający znajduje go na miejscu?** Decyzja autora — `00_START_HERE/TRACEABILITY.md` → *Open gaps* 1.
  Brief się nie zmienia (`kickoff/` = zapis decyzji); poprawiona gałąź żyje tutaj do czasu decyzji.
- Krok 3 („porównanie z zapisanym zdjęciem nagrobka") przy pierwszej wizycie nie ma zdjęcia do
  porównania — notatki nie niosą zdjęć (brief §1); zdjęcie powstaje dopiero w kroku 6. Brief nie mówi, co
  krok 3 robi wtedy — ta sama sytuacja pierwszej wizyty co wyżej, część *Open gaps* 1.
