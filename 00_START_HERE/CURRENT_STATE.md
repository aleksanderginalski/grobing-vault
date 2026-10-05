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
- nic. Następne kroki:
  - [[NT-001-photograph-the-notes]]: poza kodem, nadal najtańsze zabezpieczenie;
  - rozpisanie [[EPIC-001-zabezpiecz-i-przepisz]] na US. **Produkcyjna kopia jest pierwsza**: mechanizm
    jest już rozstrzygnięty w [[ADR-004-backup-format-encryption-destination]], a musi działać przed
    pierwszymi danymi;
  - pozostałe spike'i: [[SPIKE-001-map-source-offline]] i [[SPIKE-002-tree-on-a-phone]], przed widokami,
    których dotyczą;
  - przed pierwszym pushem musi być zamknięte [[NT-008-publication-review]]. Zostały w nim wybór dla
    vaulta i przegląd `git log -p`; strażnik danych rodziny już działa.
- ⚠️ **Przed pierwszymi prawdziwymi danymi w aplikacji:** `grobing-code` ma dziś domyślne
  `allowBackup=true`. Android skopiowałby dane do swojej kopii w chmurze i przy transferze na nowy
  telefon, co zmierzył [[SPIKE-003-backup-and-restore]] (M7). Poprawka należy do pozycji produkcyjnej
  kopii (ADR-004 → *Follow-ups*).
- **Budowa bez terminu** (decyzja autora 2026-10-05). 1 listopada niczego nie wyznacza; przy wizytach
  autor robi zdjęcia nagrobków z lokalizacją → `TRACEABILITY.md` → *Open gaps* 2.
- **Weryfikacja na emulatorze do MVP** (decyzja autora 2026-10-05). Na telefon trafi dopiero MVP, jako
  build release; wyjątki są w `DEFINITION_OF_DONE.md`.
- **Autor, poza sesją:**
  - kopia klucza wydania (`.jks` + hasła) w zaszyfrowanym miejscu przed pierwszymi danymi;
  - opcjonalnie zmiana hasła klucza (README `grobing-code` → *Podpis wydania*);
  - po SPIKE-003: usunąć folder `Grobing-spike` na Dysku i dwa pliki `grobing-*.age` z Pobranych na PC
    (wymyślone dane, zaszyfrowane).
- **Przed rozpisaniem [[EPIC-002-wizyta]] na US — pytanie do autora:** jak znaleźć przy pierwszej wizycie
  grób bez pinezki, adresu kwatery i zdjęcia → `TRACEABILITY.md` → *Open gaps* 1. Kandydat: plany
  cmentarzy z kwaterami → `01_INBOX/2026-10-05-plany-cmentarzy.md` (rozstrzyga SPIKE-001).

## Backlog at a glance
- Zadania: *patrz `backlog/issues/`*.
- Spike'i: *patrz `backlog/spikes/`* — trzy niewiadome, na których stoi architektura.
- Poza kodem: *patrz `backlog/non-tech/`*.
- Odłożone: *patrz `backlog/deferred/`*.
- Wymagania: *patrz `03_REQUIREMENTS/`* (EPIC-i, FR, NFR); architektura i ADR-y: *patrz `04_ARCHITECTURE/`*.
- **Przed pierwszym pushem (repo publiczne):** [[NT-008-publication-review]] — twardy warunek z
  `family-data.md` ([[ISSUE-006-setup-family-data-guard]] już zamknięte).

## Retro / fact-confirmation counter
- Zamknięte pozycje od ostatniego retro: **4**. Co **10** → retro + pytanie o 3-5 nośnych faktów
  (Meta-dec. 3g, 3h SC-16, A3). Licznik żyje **tylko tutaj**; podbija go `docs` przy zamknięciu.

## Parked (waiting on someone outside the session)
- brak. Format wpisu: `źródło (babcia / cmentarz X) · pytanie bez danych rodziny · warunek obudzenia
  (zdarzenie) · data zapytania`. **Odpowiedź z faktami o rodzinie trafia do aplikacji, nie tutaj.**

## Recently done
- 2026-10-05 — [[ISSUE-006-setup-family-data-guard]] zamknięte. Strażnik danych rodziny działa:
  - hook `PreToolUse` w `grobing-agents` odmawia zapisu baz, kopii `age`/`tar`, eksportów HTML/PDF,
    zdjęć i filmów w trzech repo. Odmawia też `git add`/`commit`, gdy taki plik mógłby wejść do commita;
  - przy własnym błędzie blokuje;
  - ten sam blok jest w `.gitignore` trzech repo, bo to jedyna ochrona commitów autora z VS Code;
  - nie widzi treści: nazwisko w tekście to sprawa [[ISSUE-003-setup-quality-critic]].

  **Dla autora:** obraz albo PDF wklejony w Obsidianie **nie wejdzie do commita** vaulta (ignorowany po
  cichu). Wyjątek dopisuje pozycja, przy której pojawi się pierwszy taki plik, np. `05_DESIGN/`. Hook
  dokłada czas do każdego wywołania narzędzia (pomiar: ISSUE-006 → *Verification*). Werdykt `qa`:
  APPROVED (self-check, z uwagami); kroki stopu #2 autor oddał agentowi.
- 2026-10-05 — [[SPIKE-003-backup-and-restore]] zamknięty, [[ADR-004-backup-format-encryption-destination]]
  `accepted`:
  - kopia to jeden plik `age` w Dysku autora, zapisany przez systemowe okno zapisu pliku. Dysk nie działa
    w oknie wyboru folderu, więc każda kopia wysyła całość;
  - kopia w tle nie potrzebuje hasła, bo w telefonie jest tylko klucz publiczny;
  - kopię da się otworzyć bez aplikacji (`age` + `tar` + SQLite);
  - odtworzenie przez Dysk na drugim emulatorze (`Grobing_Restore`, zostaje do próbnych odtworzeń) dało
    zgodny odcisk danych.

  Werdykt `qa`: APPROVED (self-check, z uwagami); stop #2 autor pominął.
- 2026-10-05 — [[ISSUE-002-bootstrap-code-repo]] zamknięte. Projekt Flutter w `grobing-code`:
  - Flutter przypięty na 3.41.1 przez `pubspec`;
  - pakiet `com.grobing.app`;
  - ciemny ekran startowy w stylu B;
  - podpis wydania kluczem spoza drzewa projektu.

  Na emulatorze działa build release. Werdykt `qa`: APPROVED (self-check).
- 2026-10-05 — [[ISSUE-001-materialize-backlog]] zamknięte: persona P1, EPIC-i, FR i NFR w <!-- placeholder-ok: real wikilink -->
  `03_REQUIREMENTS/`, ADR-001…004 i model danych w `04_ARCHITECTURE/`, EPIC przypisany w każdym wierszu
  macierzy. Werdykt `qa`: APPROVED (self-check, po poprawkach).
- 2026-10-05 — [[NT-008-publication-review]] pkt 2-3: zapis kick-offu przeredagowany przed pierwszym
  commitem (pozycja otwarta — czeka na ISSUE-006 i wybór dla vaulta).
- 2026-10-05 — kick-off NPG zamknięty; przestrzeń zmaterializowana (3 repo).
