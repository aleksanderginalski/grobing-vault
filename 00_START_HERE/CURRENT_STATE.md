---
title: "Grobing — Current State"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-06
---

# Grobing — Current State

> Żywy obraz tego, gdzie produkt jest teraz. Krótszy i bardziej zmienny niż `SESSION_STATE.md`.

> 📍 **Ten plik jest jedynym licznikiem stanu produktu** — etap dojrzałości, co w toku, licznik do
> retro, sprawy zaparkowane. **Żaden inny plik ich nie powtarza; wszystkie linkują tutaj.** Wolisz
> *„patrz `backlog/issues/`"* niż *„12 zadań"* — wskaźnik się nie zestarzeje.

## Maturity stage
MVP — od startu, cały produkt (Meta-decyzja 4).

## In progress
- Nic w toku. [[US-001-kopia-z-odtworzeniem]] **zamknięta** (2026-10-06): kopia na przycisk i w tle,
  odtworzenie także przez Dysk na drugim urządzeniu; format v1: `04_ARCHITECTURE/backup-format.md`.
- Następne kroki:
  - [[NT-001-photograph-the-notes]]: poza kodem, nadal najtańsze zabezpieczenie;
  - **przed planowaniem [[US-002-przepisanie-grobu]] — pytanie do autora:** czy grób z notatek to
    cmentarz + osoby, z adresem, pinezką i zdjęciem opcjonalnymi (⚠️ OPEN w US-002);
  - pozostałe spike'i: [[SPIKE-001-map-source-offline]] i [[SPIKE-002-tree-on-a-phone]], przed widokami,
    których dotyczą;
  - przed pierwszym pushem musi być zamknięte [[NT-008-publication-review]]. Zostały w nim wybór dla
    vaulta i przegląd `git log -p`; strażnik danych rodziny już działa.
- **Przed pierwszymi prawdziwymi danymi w aplikacji:** kopia jest gotowa (US-001 ✅). Zostały hasło i
  miejsce pliku klucza w notce przekazania ([[NT-007-hand-over-note]]): utrata któregoś z nich = utrata
  kopii. Notkę sprawdzić raz jej własną drogą (`age -d -i …` z hasłem w terminalu — NT-007 → *Input from
  US-001 closure*).
- **Budowa bez terminu** (decyzja autora 2026-10-05). 1 listopada niczego nie wyznacza; przy wizytach
  autor robi zdjęcia nagrobków z lokalizacją → `TRACEABILITY.md` → *Open gaps* 2.
- **Weryfikacja na emulatorze do MVP** (decyzja autora 2026-10-05). Na telefon trafi dopiero MVP, jako
  build release; wyjątki są w `DEFINITION_OF_DONE.md`.
- **Autor, poza sesją:**
  - kopia klucza wydania (`.jks` + hasła) w zaszyfrowanym miejscu przed pierwszymi danymi;
  - opcjonalnie zmiana hasła klucza (README `grobing-code` → *Podpis wydania*);
  - po SPIKE-003: usunąć folder `Grobing-spike` na Dysku i dwa pliki `grobing-*.age` z Pobranych na PC
    (wymyślone dane, zaszyfrowane);
  - po ISSUE-009: usunąć foldery `Grobing-dev-009` i `Grobing-proba` na Dysku (wymyślone dane, hasła
    testowe). Pliki o tej samej nazwie w kilku folderach mylą wyszukiwarkę okna przy odtworzeniu.
- **Przed rozpisaniem [[EPIC-002-wizyta]] na US — pytanie do autora:** jak znaleźć przy pierwszej wizycie
  grób bez pinezki, adresu kwatery i zdjęcia → `TRACEABILITY.md` → *Open gaps* 1. Kandydat: plany
  cmentarzy z kwaterami → `01_INBOX/2026-10-05-plany-cmentarzy.md` (rozstrzyga SPIKE-001).

## Backlog at a glance
- Zadania: *patrz `backlog/issues/`*.
- Spike'i: *patrz `backlog/spikes/`* — trzy niewiadome, na których stoi architektura.
- Poza kodem: *patrz `backlog/non-tech/`*.
- Odłożone: *patrz `backlog/deferred/`*.
- Wymagania: *patrz `03_REQUIREMENTS/`* (EPIC-i, US, FR, NFR); architektura i ADR-y: *patrz `04_ARCHITECTURE/`*.
- **Przed pierwszym pushem (repo publiczne):** [[NT-008-publication-review]] — twardy warunek z
  `family-data.md` ([[ISSUE-006-setup-family-data-guard]] już zamknięte).

## Retro / fact-confirmation counter
- Zamknięte pozycje od ostatniego retro: **8**. Co **10** → retro + pytanie o 3-5 nośnych faktów
  (Meta-dec. 3g, 3h SC-16, A3). Licznik żyje **tylko tutaj**; podbija go `docs` przy zamknięciu.
- Do retro (zebrane po drodze, bez decyzji):
  - kopia w tle po wyczerpaniu ponowień (np. Dysk wylogowany) czeka na następne użycie aplikacji, a błąd
    widać tylko na „Stanie danych” — czy to wystarcza przy rzadkim używaniu? ([[ISSUE-010-background-backup]]);
  - czy kopia AC-2 potrzebuje stałego testu z oficjalnym `age`/`tar` ([[US-001-kopia-z-odtworzeniem]] →
    *Verification*, uwaga 1)?

## Parked (waiting on someone outside the session)
- brak. Format wpisu: `źródło (babcia / cmentarz X) · pytanie bez danych rodziny · warunek obudzenia
  (zdarzenie) · data zapytania`. **Odpowiedź z faktami o rodzinie trafia do aplikacji, nie tutaj.**

## Recently done
- 2026-10-06 — [[ISSUE-010-background-backup]] zamknięte, a z nim **[[US-001-kopia-z-odtworzeniem]]**
  (werdykt US: APPROVED, niezależny przegląd, z uwagami). Kopia w tle w `grobing-code`:
  - kopię zamawia **zapis danych**; robi się **raz po sesji** — po 10 min bez zmian, najpóźniej godzinę od
    pierwszej zmiany; bez hasła, do tego samego pliku w Dysku;
  - gdy aplikacji nikt nie używa, nic się nie dzieje (bez cyklicznych sprawdzeń — decyzja autora);
  - przycisk, konfiguracja, odtworzenie i kopia w tle nigdy nie biegną naraz;
  - na „Stanie danych”: „Ostatnia udana kopia … (w tle)”.

  Stop #2 w pierwszym podejściu znalazł błąd: wyjście z aplikacji jako jedyny wyzwalacz przegrywało z
  wyrzuceniem aplikacji z ostatnich. Poprawione (zamówienie przy zapisie) i sprawdzone tym samym gestem.
  Werdykt `qa`: APPROVED (self-check, z uwagami); stop #2 „ok” w podejściu 2.

  **Dla autora:**
  - przy zamkniętej aplikacji termin kopii wyznacza Android — zmierzone: gotowe zadanie czekało ponad
    3,5 min (wcześniej bywało > 44 min). Kopia się spóźnia, nie ginie;
  - przy pierwszym buildzie release na telefon sprawdzić, że po zmianie danych pojawia się „(w tle)” — w
    AOT sprawdzał to tylko build profile;
  - folder `Grobing-proba` w Dysku dostał w tej sesji kilka kopii (wymyślone dane, hasło testowe) — do
    usunięcia jak wcześniej.
- 2026-10-06 — [[ISSUE-009-restore]] zamknięte. Odtworzenie w `grobing-code`:
  - „Stan danych” → „Odtwórz z kopii”: plik kopii i plik klucza z systemowego okna otwarcia pliku, hasło;
  - **nic w telefonie nie zmienia się przed sprawdzeniem całej kopii** (hasło, ścisły `tar`, manifest,
    SHA-256, `integrity_check`, liczby, odcisk danych); starsza kopia przechodzi migracje, nowsza jest
    odrzucana;
  - podmiana ze znacznikiem: przerwanie w dowolnym miejscu daje przy starcie stare albo nowe dane;
  - limit = wolne miejsce (2 × rozmiar kopii + 200 MB), bez sufitu w GB (D2);
  - telefon z danymi dostaje ostrzeżenie i „Zastąp dane” (D4).

  **Pierwszy zapis do Dysku i pierwsze odtworzenie z Dysku kodem produkcyjnym obejrzał człowiek**: odcisk
  zgodny na `Medium_Phone` i `Grobing_Restore` (release). Werdykt `qa`: APPROVED (self-check, z uwagami);
  stop #2 „ok”, sprawdzony na emulatorach.

  **Dla autora:** po zmianie telefonu kopia idzie dalej **tym samym kluczem** do tego samego pliku (D3),
  więc notka przekazania zostaje ważna. Stary telefon trzeba wtedy wyłączyć z kopii: dwa telefony
  nadpisują jeden plik. Plik w Dysku jest jeden i nadpisywany — historii kopii nie ma poza (niesprawdzoną)
  historią wersji Dysku.
- 2026-10-06 — [[ISSUE-008-backup-write]] zamknięte. Kopia w `grobing-code`:
  - konfiguracja raz: hasło, plik klucza i plik kopii zapisane przez systemowe okno zapisu (do Dysku);
    w telefonie zostaje tylko klucz publiczny;
  - „Zrób kopię teraz” i „Ostatnia udana kopia” na ekranie „Stan danych”;
  - własny moduł `age`: 92 oficjalne wektory C2SP i zgodność z oficjalnym CLI w obie strony; kopię z
    emulatora otworzył na PC oficjalny `age`, z odciskiem zgodnym z ekranem;
  - kopia Androida i transfer D2D wyłączone; aplikacja bez uprawnienia `INTERNET`.

  Kopia w tle wyszła do [[ISSUE-010-background-backup]] (decyzja autora, stop #1). Werdykt `qa`: APPROVED
  (self-check, z uwagami); stop #2 autor pominął.

  **Dla autora:** zapisu do Dysku kodem produkcyjnym nikt jeszcze nie wykonał (sprawdzony był zapis do
  Pobranych emulatora i Dysk z kodem spike'a). „Skonfiguruj kopię od nowa” tworzy **nowy** klucz: stary
  plik klucza nie otworzy nowych kopii. Kopię da się otworzyć bez Grobing:
  `04_ARCHITECTURE/backup-format.md` → *Opening a backup without Grobing*.
- 2026-10-05 — [[ISSUE-007-data-layer]] zamknięte. Warstwa danych w `grobing-code`:
  - `drift` na `sqlite3` z dołączonym SQLite 3.53.4, więc `VACUUM INTO` działa niezależnie od wersji
    Androida ([[ADR-005-sqlite-package]]);
  - schemat v1 bez *Assertion*, która przyjdzie jako v2 przy [[US-002-przepisanie-grobu]];
  - ekran „Stan danych" z odciskiem danych, czyli miarą dla kopii i odtworzenia;
  - wymyślone dane tylko w buildzie debug.

  **Dla autora:** przypięty Flutter zamraża parę `drift`/`drift_dev` na 2.34.0, więc zmiana SDK rusza też
  je ([[ADR-002-flutter-pinned]] → *Follow-ups*). Pierwszy build na nowej maszynie potrzebuje sieci (hook
  pobiera SQLite). Werdykt `qa`: APPROVED (self-check, z uwagami); stop #2 „ok”.
- 2026-10-05 — [[EPIC-001-zabezpiecz-i-przepisz]] rozpisany na US (`docs`). Nowy folder
  `03_REQUIREMENTS/user-stories/`, ISSUE-007…009 pod US-001. Każde FR EPIC-a ma US. To rozpisanie, nie
  zamknięta pozycja, więc licznik retro bez zmian.
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
