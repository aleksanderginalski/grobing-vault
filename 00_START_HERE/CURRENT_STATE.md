---
title: "Grobing — Current State"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-05
---

# Grobing — Current State

> Żywy obraz tego, gdzie produkt jest teraz. Krótszy i bardziej zmienny niż `SESSION_STATE.md`.

> 📍 **Ten plik jest jedynym licznikiem stanu produktu** — etap dojrzałości, co w toku, licznik do
> retro, sprawy zaparkowane. **Żaden inny plik ich nie powtarza; wszystkie linkują tutaj.** Wolisz
> *„patrz `backlog/issues/`"* niż *„12 zadań"* — wskaźnik się nie zestarzeje.

## Maturity stage
MVP — od startu, cały produkt (Meta-decyzja 4).

## In progress
- nic. Następne kroki: [[NT-008-publication-review]] przed pierwszym pushem (repo publiczne),
  [[NT-001-photograph-the-notes]] (dziś, poza kodem), [[ISSUE-002-bootstrap-code-repo]], potem
  spike'i z `backlog/spikes/` i rozpisanie [[EPIC-001-zabezpiecz-i-przepisz]] na US (najpierw kopia i
  odtwarzanie).
- **Budowa bez terminu** (decyzja autora 2026-10-05). 1 listopada niczego nie wyznacza; przy wizytach
  autor robi zdjęcia nagrobków z lokalizacją → `TRACEABILITY.md` → *Open gaps* 2.
- **Przed rozpisaniem [[EPIC-002-wizyta]] na US — pytanie do autora:** jak znaleźć przy pierwszej wizycie
  grób bez pinezki, adresu kwatery i zdjęcia → `TRACEABILITY.md` → *Open gaps* 1. Kandydat: plany
  cmentarzy z kwaterami → `01_INBOX/2026-10-05-plany-cmentarzy.md` (rozstrzyga SPIKE-001).

## Backlog at a glance
- Zadania: *patrz `backlog/issues/`*.
- Spike'i: *patrz `backlog/spikes/`* — trzy niewiadome, na których stoi architektura.
- Poza kodem: *patrz `backlog/non-tech/`*.
- Odłożone: *patrz `backlog/deferred/`*.
- Wymagania: *patrz `03_REQUIREMENTS/`* (EPIC-i, FR, NFR); architektura i ADR-y: *patrz `04_ARCHITECTURE/`*.
- **Przed pierwszym pushem (repo publiczne):** [[ISSUE-006-setup-family-data-guard]] +
  [[NT-008-publication-review]] — twardy warunek z `family-data.md`.

## Retro / fact-confirmation counter
- Zamknięte pozycje od ostatniego retro: **1**. Co **10** → retro + pytanie o 3-5 nośnych faktów
  (Meta-dec. 3g, 3h SC-16, A3). Licznik żyje **tylko tutaj**; podbija go `docs` przy zamknięciu.

## Parked (waiting on someone outside the session)
- brak. Format wpisu: `źródło (babcia / cmentarz X) · pytanie bez danych rodziny · warunek obudzenia
  (zdarzenie) · data zapytania`. **Odpowiedź z faktami o rodzinie trafia do aplikacji, nie tutaj.**

## Recently done
- 2026-10-05 — [[ISSUE-001-materialize-backlog]] zamknięte: persona P1, EPIC-i, FR i NFR w <!-- placeholder-ok: real wikilink -->
  `03_REQUIREMENTS/`, ADR-001…004 i model danych w `04_ARCHITECTURE/`, EPIC przypisany w każdym wierszu
  macierzy. Werdykt `qa`: APPROVED (self-check, po poprawkach).
- 2026-10-05 — [[NT-008-publication-review]] pkt 2-3: zapis kick-offu przeredagowany przed pierwszym
  commitem (pozycja otwarta — czeka na ISSUE-006 i wybór dla vaulta).
- 2026-10-05 — kick-off NPG zamknięty; przestrzeń zmaterializowana (3 repo).
