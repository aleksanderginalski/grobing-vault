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
- [[US-002-przepisanie-grobu]] w toku: [[ISSUE-011-schema-v2-assertions]] (schemat v2) i
  [[ISSUE-014-home-map-of-poland]] (mapa Polski jako ekran główny) zamknięte. Zostały
  [[ISSUE-015-add-cemetery-from-database]] i [[ISSUE-012-transcribe-grave-screen]].
- **Następne kroki, w tej kolejności (decyzja autora 2026-10-06, *„ok plan brzmi dobrze”*; ISSUE-015 dołożona
  na stopie #1 ISSUE-014, *„wygląda dobrze”*):**
  1. ~~[[ISSUE-014-home-map-of-poland]]~~ — zamknięte 2026-10-06;
  2. [[ISSUE-015-add-cemetery-from-database]] — dodanie cmentarza z wbudowanej bazy OpenStreetMap (offline),
     z podglądem i linkiem do zdjęcia satelitarnego. Ręczne dodanie zostaje zapasem;
  3. [[ISSUE-012-transcribe-grave-screen]] — „Otwórz cmentarz” w arkuszu mapy (z ISSUE-014, D5); cmentarz jak
     R2, ale bez zdjęcia satelitarnego; grób jak R4
     z nazwą grobu (migracja v2→v3); formularz osoby z biografią. Zapis faktów jest gotowy w
     `grobing-code/lib/data/claims.dart`;
  4. [[US-005-zdjecia]] — zdjęcia grobu i osoby;
  5. [[US-003-przepisanie-rodziny]] — relacje w formularzu osoby;
  6. [[SPIKE-001-map-source-offline]] — zdjęcie satelitarne cmentarza, znicze na grobach, plany z kwaterami
     (`01_INBOX/2026-10-05-plany-cmentarzy.md`). Baza cmentarzy przeszła do ISSUE-015.
  
  **Każda pozycja z ekranem: `ui` → `planning`** (`autonomous-flow.md`). Wygląd: `05_DESIGN/brand/`
  (wytyczne v1.4 i referencje R1–R4 z kick-offu).
- Poza tą kolejnością:
  - [[NT-001-photograph-the-notes]]: zdjęcia zrobione (33). Zostało: zaszyfrowane miejsce, sprawdzenie
    kopii w WhatsAppie i otwarcie kopii — *Resolution*;
  - [[SPIKE-002-tree-on-a-phone]]: przed drzewem (widok 5);
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
  - kopia klucza wydania (`.jks` + oba hasła) w zaszyfrowanym miejscu przed pierwszymi danymi. To **nie**
    klucz kopii z testów. Klucz wydania (`release_keystore_dir` w `project-config.md`) podpisuje build, a
    bez niego telefon z danymi nie przyjmie aktualizacji bez odinstalowania, które kasuje bazę (retro 1,
    fakt 4);
  - **notatki rodziny na PC** leżą w `family_data_dir` (`project-config.md`), poza repo. Docelowo
    zdjęcia stron trafiają do zaszyfrowanego miejsca (NT-001);
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
- Zamknięte pozycje od ostatniego retro: **1** (ostatnie retro: [[2026-10-06-retro-01]]). Co **10** →
  retro + pytanie o 3–5 nośnych faktów (Meta-dec. 3g, 3h SC-16, A3). Licznik żyje **tylko tutaj**;
  podbija go `docs` przy zamknięciu, a zeruje go retro.
- Do retro (zebrane po drodze, bez decyzji):
  - **po czytaniu `family_data_dir` grep obowiązkowy** ([[ISSUE-014-home-map-of-poland]] → *Self-check*):
    `ui` wpisał do specyfikacji trzy prawdziwe przykłady zaraz po porównaniu z listą autora. Złapane przed
    commitem, bo strażnik nie widzi treści. Do decyzji: krok w regule `family-data.md` albo w checkliście R1;
  - **`git rm --cached` przez `dev`** (ISSUE-014 → *Dev report* → *Deviations* 5): zmiana indeksu poza commitem
    po checkliście. Zgłoszone od razu, skutek bez znaczenia (ta sama zmiana weszła do commita). Do decyzji:
    czy reguła ma wprost wymieniać `git rm` i `git restore`;
  - **zawieszony przebieg testów** (ISSUE-014 → *Verification*): drift zamyka strumień na timerze fałszywego
    czasu testu. Wzorzec sprzątania jest w testach; czy dopisać go do README `grobing-code` → testy;
  - **polskie `MaterialLocalizations`** (przegląd `ui`, uwaga 11): systemowe podpowiedzi są po angielsku —
    kandydat na małą pozycję;
  - **agent `architect`** — kick-off (MD3c) dał mu sygnał „decyzja wymagająca ADR-a poza kick-offem”. Ten
    sygnał już był: [[ADR-005-sqlite-package]] i [[ADR-006-claimed-value-separate-structures]] powstały w
    łańcuchu (`planning` → `docs`), bez osobnego agenta, i [[ISSUE-014-home-map-of-poland]] doda kolejny.
    Według R9 sygnał z kick-offu wygrywa. **Decyzja autora:** zbudować `architect` albo zapisać, że ADR-y
    zostają w łańcuchu. Wykrył to przegląd `kickoff/` (R4); do tego czasu ADR-y robi łańcuch jak dotąd.
  
  Tematy z poprzedniego okresu rozliczyło [[2026-10-06-retro-01]] (R1–R10).

## Parked (waiting on someone outside the session)
- brak. Format wpisu: `źródło (babcia / cmentarz X) · pytanie bez danych rodziny · warunek obudzenia
  (zdarzenie) · data zapytania`. **Odpowiedź z faktami o rodzinie trafia do aplikacji, nie tutaj.**

## Recently done
- 2026-10-06 — [[ISSUE-014-home-map-of-poland]] zamknięte. **Ekran główny to mapa Polski**, działająca bez sieci
  od pierwszego uruchomienia:
  - kontur, rzeki i 9 miast z Natural Earth są w aplikacji; `flutter_map` rysuje bez kafelków
    ([[ADR-007-poland-map-bundled-data]]), aplikacja dalej bez `INTERNET`. Krok 1 UJ-001 offline — `⚠️ OPEN`
    w NFR-001 i ADR-003 zamknięty;
  - znicz na każdym cmentarzu z punktem, a nachodzące łączą się w znicz z liczbą; arkusz z liczbą grobów i
    osób i ikonką edycji; wyszukiwarka bez polskich znaków i końcówek; ręczne dodanie (okno → dotknięcie
    na mapie) i poprawa;
  - na stopie #1 autor dołożył **bazę cmentarzy** — falsyfikator na wyciągu OpenStreetMap: 8 z 8 jego
    cmentarzy jest w bazie → [[ISSUE-015-add-cemetery-from-database]] zaraz po tej pozycji;
  - „Otwórz cmentarz” przeszło do [[ISSUE-012-transcribe-grave-screen]] (decyzja autora, D5).
  
  Werdykt `qa`: APPROVED (self-check, z uwagami); przegląd `ui` (BLOCKER w krokach poprawiony); stop #2 „ok”
  — kroki 4–5 (znicz z liczbą, cmentarz bez punktu) autor pominął, pokryte testami i sprawdzeniem agenta.
  Testy: 286.

  **Dla autora:** emulator `Medium_Phone` ma teraz świeżą instalację buildu release — testowa konfiguracja
  kopii z wcześniejszych pozycji zniknęła; przy następnej pozycji z kopią trzeba ją ustawić od nowa.
- 2026-10-06 — **przegląd `kickoff/`** (retro 1, R4; `docs`): brief, stan sesji, manifest i profil
  porównane z vaultem. Decyzje kick-offu mają dom (ISSUE-001 zmaterializował je w EPIC-ach, FR, NFR,
  ADR-ach i backlogu). Rozjechały się albo zgubiły cztery rzeczy, poprawione:
  - **numer ADR dystrybucji:** brief rezerwował ADR-005, a zajął go ADR-005 (SQLite) → [[NT-005-distribution-decision]]
    dostanie następny wolny numer;
  - **minima bezpieczeństwa dla mapy:** klucz API poza repo i ograniczony do pakietu, a pobranie mapy
    offline wymaga uprawnienia `INTERNET`, którego APK dziś nie ma → [[SPIKE-001-map-source-offline]] krok 2;
  - **prior art sprzed kick-offu** (Grobonet, BillionGraves, Graveyard Navigator, Gramps…) był tylko w
    notatkach sesji → sekcje *Prior art* w [[EPIC-002-wizyta]] i [[EPIC-003-zrozumienie]];
  - **agent `architect` na sygnał** zgubił się z listy w `grobing-agents/CLAUDE.md` → dopisany; decyzja
    autora wyżej (*Do retro*).
  
  `kickoff/MANIFEST.yaml` wymienia 5 agentów, na dysku jest 6 (`ui` na sygnał MD3c). Manifest z zasady
  się nie zmienia. To nie zamknięcie pozycji, więc licznik retro bez zmian.
- 2026-10-06 — **retro 1** ([[2026-10-06-retro-01]], nowy folder `07_RETRO/`): licznik 10 → 0. Decyzje
  autora R1–R10:
  - **commit bez pytania, po checkliście; push tylko po „go”** (R1);
  - na końcu sesji: co dalej i „możesz kończyć” (R2);
  - dane rodziny na PC w `family_data_dir`, poza repo (R3);
  - stop #1 przy ekranach dokładny (R5);
  - kopia zaraz po migracji w ISSUE-012 (R6).
  
  Notatki rodziny, które autor położył w vaulcie, przeniesione poza repo, zanim trafiły do historii.
- 2026-10-06 — [[ISSUE-013-setup-ui-agent]] zamknięte. **Agent `ui` działa i jest w łańcuchu:**
  - `ui` → `planning` przy każdej pozycji z ekranem; specyfikacja ekranu idzie na stop #1, bez nowego
    punktu stopu;
  - przegląd zbudowanego ekranu robi subagent dla `qa` przed stopem #2;
  - `05_DESIGN/` należy do `ui`.
  
  Pierwsze uruchomienie (na ISSUE-012) dało:
  - wytyczne stylu B (v1.2) i referencje z kick-offu (`05_DESIGN/brand/`, obrazy R1–R4 tylko lokalnie);
  - cztery pierwsze specyfikacje i makietę;
  - przegląd ekranu startowego.
  
  Na makiecie autor zmienił strukturę ekranów, zanim powstał kod (mapa od startu, cmentarz jak R2, grób
  jak R4). Stąd nowa [[ISSUE-014-home-map-of-poland]] i kolejność wyżej. Werdykt `qa`: APPROVED
  (self-check, z uwagami); stop #2 w dwóch rundach.
- 2026-10-06 — założona [[ISSUE-013-setup-ui-agent]] (`docs`, decyzja autora w `/pm`): agent `ui` przed
  pierwszym ekranem, zamiast projektowania ekranu przez `planning`. To założenie pozycji, nie zamknięcie,
  więc licznik retro bez zmian.
- 2026-10-06 — [[ISSUE-011-schema-v2-assertions]] zamknięte. Schemat v2 w `grobing-code`:
  - **każda data i każdy pochówek ma źródło i status** (twierdzenie: rodzaj źródła, szczegół, status,
    kiedy). Sprzeczna wartość z innego źródła to osobny wiersz, a pokazuje się pierwszy — jak w GEDCOM 7
    ([[ADR-006-claimed-value-separate-structures]]);
  - pochówek: każdy grób podany przez jakieś źródło to osobny wiersz (FR-003 doprecyzowane decyzją
    autora);
  - pierwsza prawdziwa migracja (v1→v2) w jednej transakcji; dane z v1 dostały źródło „notatki,
    przeniesione z v1”.

  Aktualizację na emulatorze (nowa wersja wgrana na starą, bez odinstalowania) sprawdził agent: wszystkie
  dane v1 identyczne wiersz w wiersz. Werdykt `qa`: APPROVED (self-check, z uwagami); stop #2 autor oddał
  agentowi i zdecydował, że jego kroki mają dotyczyć UI/UX (`DEFINITION_OF_DONE.md` → *Kto sprawdza*).

  **Dla autora:** odtworzenia starej kopii (v1) w nowej wersji nie sprawdzono na emulatorze, bo wymaga
  hasła testowego. Pokrywa je test na prawdziwym archiwum v1.
- 2026-10-06 — [[US-002-przepisanie-grobu]] rozpisana na [[ISSUE-011-schema-v2-assertions]] i
  [[ISSUE-012-transcribe-grave-screen]] (`docs`). To rozpisanie, nie zamknięta pozycja, więc licznik retro
  bez zmian. Kolumnę Issue(s) w `TRACEABILITY.md` wpisuje `planning` przy planowaniu każdego ISSUE.
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
