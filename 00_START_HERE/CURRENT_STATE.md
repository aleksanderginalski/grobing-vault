---
title: "Grobing — Current State"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-13
---

# Grobing — Current State

> Żywy obraz tego, gdzie produkt jest teraz. Krótszy i bardziej zmienny niż `SESSION_STATE.md`.

> 📍 **Ten plik jest jedynym licznikiem stanu produktu** — etap dojrzałości, co w toku, licznik do
> retro, sprawy zaparkowane. **Żaden inny plik ich nie powtarza; wszystkie linkują tutaj.** Wolisz
> *„patrz `backlog/issues/`"* niż *„12 zadań"* — wskaźnik się nie zestarzeje.

## Maturity stage
MVP — od startu, cały produkt (Meta-decyzja 4).

## In progress
- **Po [[2026-10-13-retro-03]] (R1–R10, decyzja autora 2026-10-13):** ~~[[ISSUE-031-command-guard]]~~ i ~~[[SPIKE-002-tree-on-a-phone]]~~ —
  zamknięte 2026-10-13 (*Recently done*). Dalej droga do instalacji MVP — **następna: [[US-009-drzewo-od-osoby]]** (punkt 7 niżej);
  pierwszy krok pozycji: wymyślona rodzina o kształcie prawdziwej w `lib/dev/` (SPIKE-002 D6).
- **Prawdziwe dane rodziny dopiero po instalacji MVP** (decyzja autora 2026-10-08 w `/pm`): budujemy produkt gotowy do
  instalacji na telefonie (MVP = brief §5, M1–M11); do tego czasu autor ocenia aplikację na wymyślonych danych. Rozmowa z babcią
  (~2026-11-02) jest na kartce, a odpowiedzi trafią do aplikacji po instalacji.
- **Droga do instalacji MVP** — propozycja łańcucha przy zamknięciu SPIKE-004 (autor może zmienić kolejność):
  1. ~~[[ISSUE-022-app-skeleton-tabs-people-settings]]~~ — zamknięte 2026-10-08;
  2. ~~[[ISSUE-025-gender-kinship-together-since]]~~ — zamknięte 2026-10-08;
  3. ~~[[ISSUE-024-person-view]]~~ — zamknięte 2026-10-12;
  4. ~~[[ISSUE-023-poland-map-r1-cemetery-photo]]~~ — zamknięte 2026-10-12;
  5. ~~[[US-007-mapa-cmentarza]]~~ — zamknięta 2026-10-12 (~~ISSUE-027~~, ~~ISSUE-028~~);
  6. ~~[[US-008-pinezka-na-miejscu]]~~ — zamknięta 2026-10-12 (~~ISSUE-029~~). **Teren czeka:** build release na
     telefonie przed zaduszkami (~2026-11-02) → *Parked* (cel autora z `/pm`: jedna wizyta da pomiar i sprawdzenie AC-1, AC-4).
     Kandydaci z [[cmentarz]] D29 i nachodzące znicze → [[ISSUE-030-sector-on-a-visit]] (`draft`, **czeka na wizytę** — D5, stop #1);
  7. ~~[[SPIKE-002-tree-on-a-phone]]~~ — zamknięty 2026-10-13 → **następna: [[US-009-drzewo-od-osoby]]** (drzewo od osoby, S2, ślad dalszej
     rodziny, słownik nazw złożonych — dawne AC-6 ISSUE-024, „Pokaż w drzewie”, tryb prezentacji) → [[US-010-czas-na-drzewie]] →
     [[US-011-polacz-dwie-osoby]] ([[drzewo]] v1.4, [[EPIC-003-zrozumienie]]);
  8. [[US-006-eksport-dla-rodziny]] i [[NT-007-hand-over-note]];
  → **[[ISSUE-032-mvp-install]]** (`draft`): audyt pól modelu ↔ ekrany (R9), lista rzeczy niesprawdzonych w ręce (R8), warunki
  przed pierwszymi danymi → build release na telefonie → prawdziwe dane ([[NT-002-transcribe-the-notes]]).
  Wpisy o zamkniętych pozycjach: retro 3 → *Archive*.

  **EPIC-001:** [[US-004-fakt-od-babci]] **wycofana** (SPIKE-004 D28 — bez źródeł; wiedza od babci przez zwykłą
  poprawę); [[US-006-eksport-dla-rodziny]] `ready`.
- **[[SPIKE-001-map-source-offline]] zamknięty 2026-10-08** → [[ADR-003-map-source-offline]] `accepted`: mapa
  cmentarza to **plan schematyczny z OSM offline** + ortofotomapa GUGiK online + kwatery i pinezki autora.
- **Każda pozycja z ekranem: `ui` → `planning`** (`autonomous-flow.md`). Wygląd: `05_DESIGN/brand/` (wytyczne i
  referencje R1–R4 z kick-offu). Kolejność autora z 2026-10-06 (ISSUE-014 → SPIKE-001) wyczerpana — retro 2 → *Archive*.
- Poza tą kolejnością:
  - [[ISSUE-026-link-existing-photo-to-person]] — zdjęcie, które już jest w aplikacji, dodane osobie od jej strony („połączyć z
    istniejącymi”, decyzja autora na stopie #1 ISSUE-024); nowy ekran wyboru, więc `ui` → `planning`. Dziś działa od strony zdjęcia;
  - [[NT-001-photograph-the-notes]]: zdjęcia zrobione (33). Zostało: zaszyfrowane miejsce, sprawdzenie
    kopii w WhatsAppie i otwarcie kopii — *Resolution*;
  - **wyszukiwanie w bazie cmentarzy — tematy do decyzji autora** ([[ISSUE-015-add-cemetery-from-database]] →
    *Notes*): literówki z OSM zajmują pierwsze miejsca, skracanie słów łapie podobne nazwy („krakow” →
    „…Krakowskie”), w bazie są cmentarze dla zwierząt, a wynik znaleziony przez okoliczną miejscowość nie
    mówi, przez którą. Kandydat na małą pozycję, gdy zacznie przeszkadzać przy prawdziwych cmentarzach;
  - **odświeżenie bazy cmentarzy OSM zostanie odrzucone przez strażnika treści** ([[ISSUE-020-content-guard]] →
    *Verification*): wyciąg to jeden wiersz JSON z nazwami miejscowości z listy rdzeni. Przy pierwszym odświeżeniu —
    wyjątek dla ścieżki tego pliku jako osobna pozycja, decyzja autora;
  - **kontrola cykli w rodzinie** ([[ISSUE-019-family-relations]] → *Manual*): aplikacja pozwala, by osoba była w parze ze
    swoim dzieckiem albo była swoim przodkiem — zobaczone w danych testowych autora na stopie #2. Poza zakresem ISSUE-019
    ([[ADR-011-relation-claims-family-and-child-link]] → *Follow-ups*). Kandydat na małą pozycję, gdy zdarzy się przy
    prawdziwym przepisywaniu;
  - ~~**data początku związku bez ślubu**~~ — **rozstrzygnięte 2026-10-08** ([[SPIKE-004-mvp-flow-prototype]] D20,
    [[rodzina]] v1.4): dwa tryby związku, osobne pole **„Razem od”** obok „Ślubu” (autor: *„czasami ludzie nie są
    małżeństwem, mają dziecko, i dopiero biorą ślub”*). Wejdzie z pozycją z zamknięcia SPIKE-004;
  - **[[DEF-005-push-gate]]** obudzony pierwszym pushem — **zostaje do PRODUKCJA** (retro 2, R8; DEF-005 →
    *Decision*);
  - **twarde spacje po jednoliterowych słowach i w „z d.”** w całej aplikacji ([[style-b]] v1.17 reguła 6 — kod jeszcze
    jej nie stosuje; przegląd `ui` w [[ISSUE-022-app-skeleton-tabs-people-settings]], B5). Dotyka `personName`, więc
    wszystkich ekranów z osobami i ich testów. Kandydat na małą pozycję;
  - **„Stan danych” mówi „Zapisana w Dysku na telefonie” także przy kopii w Pobranych** (ISSUE-022, B6) — jedna linia z
    `backupPlace`, poza zakresem ISSUE-022.
  - **mapa cmentarza przy tekście 200% na 360 × 640 dp** ([[ISSUE-029-pin-on-site-gps]] → *Verification*, przegląd `ui` m8): plan w A
    jest bardzo niski, „Kwatery” przykrywa „Plan offline” i „© OpenStreetMap” — z [[ISSUE-027-cemetery-map-plan-photo-states]] (D14 →
    *Obali*) i [[ISSUE-028-cemetery-sectors]]. Kandydat na małą pozycję **przed instalacją MVP**;
  - [[ISSUE-030-sector-on-a-visit]] (`draft`) — „Pokaż kwaterę”, lista grobów kwatery, nachodzące znicze; **czeka na wizytę** (D5 stopu #1
    ISSUE-029).
- **Przed pierwszymi prawdziwymi danymi w aplikacji:** kopia jest gotowa (US-001 ✅), poprawki z retro 2 też
  ([[ISSUE-021-small-fixes-after-retro-2]] ✅). Zostały hasło i
  miejsce pliku klucza w notce przekazania ([[NT-007-hand-over-note]]): utrata któregoś z nich = utrata
  kopii. Notkę sprawdzić raz jej własną drogą (`age -d -i …` z hasłem w terminalu — NT-007 → *Input from
  US-001 closure*). Wszystkie warunki przed instalacją zbiera [[ISSUE-032-mvp-install]] → *Before install*.
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
  - **lista rdzeni strażnika** (`rdzenie-straznika.txt` w `family_data_dir`, spisana przez agenta z notatek 2026-10-08):
    4 nazwiska mają niepewny odczyt pisma (oznaczone na liście). Poprawki — w pliku albo w czacie z agentem. Każde nowe
    nazwisko z przepisywania warto dopisać: rdzeń działa od następnego `git add`;
  - opcjonalnie zmiana hasła klucza (README `grobing-code` → *Podpis wydania*);
  - **build release na telefon przed wizytą na cmentarzu (~2026-11-02)** — README `grobing-code` → *Lokalizacja* (`flutter build apk
    --release --split-per-abi --target-platform android-arm64`, `adb install -r`), albo agent przez `adb`, gdy podłączysz telefon. Podpisany
    kluczem wydania, więc MVP wejdzie później jako aktualizacja. Na telefonie tylko wymyślone dane; **przed prawdziwymi danymi — wyczyść
    dane aplikacji** (Ustawienia → Aplikacje → Grobing → Pamięć);
  - po SPIKE-003: usunąć folder `Grobing-spike` na Dysku (wymyślone dane, zaszyfrowane). Dwa pliki `grobing-*.age`
    z Pobranych na PC agent przeniósł do Kosza Windows 2026-10-08, na prośbę autora. Folderów na Dysku agent nie
    usunął, bo podłączony do Claude Dysk Google to inne konto niż to na emulatorach;
  - po ISSUE-009: usunąć foldery `Grobing-dev-009` i `Grobing-proba` na Dysku (wymyślone dane, hasła
    testowe). Pliki o tej samej nazwie w kilku folderach mylą wyszukiwarkę okna przy odtworzeniu;
  - **katalogi tymczasowe sesji** w `%TEMP%\claude\c--Programowanie-Grobing-grobing-agents\` (poza bieżącą sesją): makiety,
    prototypy, zrzuty, pliki Natural Earth i kopie `-0NN` z wymyślonymi danymi — do kosza. Z SPIKE-002 zostało `220a9b6c-…\scratchpad\drzewo-spike002.html`
    (makieta kandydatów drzewa, 106 wymyślonych osób) — przyda się przy [[US-009-drzewo-od-osoby]], potem do kosza;
  - **repo nie mają pliku `LICENSE`** — kod można oglądać, ale nie wolno go używać. Licencję można dodać później.
- **Emulatory (po ISSUE-029):** `Medium_Phone` — release v12 na danych testowych autora, kopia skonfigurowana od nowa z hasłem
  testowym (wymyślone, z sesji ISSUE-029), pliki `grobing-klucz-029.age` i `grobing-kopia-029.age` w Pobranych; grób „Jozef” ma
  pinezkę z poprawki autora. `Grobing_Restore` — release v12 z danymi z kopii `-029`. Następna pozycja z kopią: nowe hasło testowe.
- **[[EPIC-002-wizyta]] gotowy do rozpisania na US** — pytanie „jak znaleźć grób bez pinezki” ma kierunek autora
  (2026-10-08): adres z wyszukiwarki zarządcy → kwatera zaznaczona według planu zarządcy → na miejscu plan offline i
  GPS → pinezka. Wejście do pierwszej US (mapa cmentarza): EPIC-002 → *Input from SPIKE-001*. Ekran: `ui` →
  makieta przed kodem; [[cmentarz]] D1 (zdjęcie nad listą) do zmiany.

## Backlog at a glance
- Zadania: *patrz `backlog/issues/`*.
- Spike'i: *patrz `backlog/spikes/`* — trzy niewiadome, na których stoi architektura.
- Poza kodem: *patrz `backlog/non-tech/`*.
- Odłożone: *patrz `backlog/deferred/`* oraz pozycje ze `status: deferred` w `backlog/issues/` (ISSUE-003…005, retro 3 R10 —
  warunek obudzenia w `trigger:`).
- Wymagania: *patrz `03_REQUIREMENTS/`* (EPIC-i, US, FR, NFR); architektura i ADR-y: *patrz `04_ARCHITECTURE/`*.
- **Repo są publiczne na GitHubie** od 2026-10-07 ([[2026-10-08-retro-02]] → *Archive*). Push idzie sam zaraz po commicie
  paczki (decyzja autora 2026-10-07); treść wychodzących zmian sprawdza strażnik treści ([[ISSUE-020-content-guard]]) przy każdym `git add`/`commit`.

## Retro / fact-confirmation counter
- Zamknięte pozycje od ostatniego retro: **2** (ostatnie retro: [[2026-10-13-retro-03]]). Co **10** → retro + pytanie o 3–5
  nośnych faktów (Meta-dec. 3g, 3h SC-16, A3). Licznik żyje **tylko tutaj**; podbija go `docs` przy zamknięciu, a zeruje go retro.
- Do retro (zebrane po drodze, bez decyzji): — pusto. Poprzednią listę rozliczyło [[2026-10-13-retro-03]] → *The "Do retro"
  list*.

## Parked (waiting on someone outside the session)
- **cmentarz (którykolwiek z cmentarzy autora)** · przy 3 grobach, które autor zna: (a) dokładność GPS telefonu
  przy grobie w metrach (dowolna mapa z niebieską kropką); (b) czy kropka trafia we właściwą kwaterę, rząd albo
  aleję; (c) czy przy bramie wisi plan z kwaterami. Odpowiedź w czacie: **same liczby i tak/nie**, bez nazw i
  położeń · warunek obudzenia: **najbliższa wizyta na cmentarzu** · 2026-10-08 ([[SPIKE-001-map-source-offline]] D5;
  mierzy H3 i H9 przed budową pinezek w [[EPIC-002-wizyta]]). Prawdopodobna okazja: wyjazd autora na zaduszki
  (~2026-11-02, ten sam co rozmowa z babcią — *In progress*). **Krok w terenie [[ISSUE-029-pin-on-site-gps]] (D4, 2026-10-12):** z buildem
  release na telefonie, na wymyślonym grobie — kropka i jej dokładność przy 3 grobach, pinezka postawiona i poprawiona, tryb samolotowy,
  czytelność w słońcu ([[NFR-004-czytelnosc-w-sloncu]]); wynik ustawia próg „słaby sygnał” (`weakSignalM`, dziś tymczasowo 15 m) i decyduje
  o [[ISSUE-030-sector-on-a-visit]]. Odpowiedź w czacie: same liczby i tak/nie. **Ta sama wizyta** sprawdzi w terenie
  [[ISSUE-029-pin-on-site-gps]] (build release na telefonie, wymyślony grób) — cel autora z 2026-10-12.

Format wpisu: `źródło (babcia / cmentarz X) · pytanie bez danych rodziny · warunek obudzenia
(zdarzenie) · data zapytania`. **Odpowiedź z faktami o rodzinie trafia do aplikacji, nie tutaj.**

## Recently done
> Tylko wpisy od ostatniego retro ([[2026-10-13-retro-03]], R5). Starsze są w plikach retro → *Archive*:
> [[2026-10-13-retro-03]] · [[2026-10-08-retro-02]] · [[2026-10-06-retro-01]].

- 2026-10-13 — [[SPIKE-002-tree-on-a-phone]] zamknięty (H4). **Drzewo ok. 100 osób czyta się od osoby, z przesuwaniem — całości naraz nie:**
  - prior art ze źródłami ([[drzewo]] D8: TimeNets, drzewa podwójne, FamilySearch) — rodzina to krata, pokazuje się wycinek według zainteresowania,
    czyli poziomy z D2;
  - makieta kandydatów na 106 wymyślonych osobach; pomiar: bez przesuwania mieści się tylko poziom 1, poziomy rosną 6 → 20 → 66 → 99 → 106;
  - **decyzje autora na stopie #1 (*„Tak”*):** K2 bez całego drzewa, S2 (oddalanie odsłania dalszą rodzinę, 4 progi), ślad dalszej rodziny,
    telewizor przez „Przesyłaj ekran” + tryb prezentacji ([[drzewo]] v1.3);
  - prototyp we Flutterze poza repo: własny układ wygrał z `graphview` w każdej mierze (bez ADR, bez nowej zależności); przesuwanie płynne,
    przejście między poziomami szarpie na emulatorze, tekst 200% wymaga reguły mini-drzewa (*Findings*);
  - EPIC-003 rozpisany: [[US-009-drzewo-od-osoby]] → [[US-010-czas-na-drzewie]] → [[US-011-polacz-dwie-osoby]]; słownik nazw złożonych w zakresie
    (decyzja autora 2026-10-09).

  Stop #2 „ok” — kroki 1–2 ze śladem na emulatorze, zadanie na czas „pomiń”; trzy wiersze na [[ISSUE-032-mvp-install]] → *Hand checks*.
  Werdykt `qa`: APPROVED (self-check, z uwagami). Prototyp usunięty, `grobing-code` bez zmian. Licznik retro: 1 → 2.

- 2026-10-13 — [[ISSUE-031-command-guard]] zamknięte (retro 3, R1). **Strażnik komend: mechanizm zamiast pamięci:**
  - hook `command-guard.ps1` przy każdej komendzie Bash i PowerShell — z gita przechodzi tylko **lista dozwolonych**: odczyt,
    `git add` jawnych plików, `git commit` bez `--amend`/`-a`/`--no-verify`, `git push origin main`. Reszta — także `reset`,
    `stash`, `fetch`, `revert`, `clean`, `gh` — dostaje odmowę przy próbie, również z `-C`/`-c`, w `&&`, `$(…)`, `bash -c`,
    `powershell -Command`;
  - **Python ze skryptem z wejścia** (`python -`, `python -I -`, REPL) — odmowa z podpowiedzią „zapisz skrypt i uruchom plik”;
  - tekst w cudzysłowach i heredoc to tekst: `grep 'git reset'` i opis commita przechodzą;
  - **komendy „po go”** (`git init`, `git remote`, `gh`) wykonuje autor w terminalu VS Code — agent podaje komendę
    (`git-autonomy-boundary.md`);
  - **luka w strażniku danych rodziny zamknięta:** przy przekroczeniu `timeout` przepuszczał po cichu — teraz oba hooki mają
    `"onFailure": "block"`.

  Testy: strażnik komend 369/369, strażnik danych rodziny 150/150 bez regresji; odmowy sprawdzone na żywo w Bash i PowerShell.
  Koszt ok. 0,4–0,5 s na komendę, równolegle ze strażnikiem danych rodziny. Kroki oddane agentowi (pozycja bez ekranu); nic na
  listę [[ISSUE-032-mvp-install]] → *Hand checks*. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 0 → 1.

  **Dla autora:** `claude` 2.1.238 w terminalu nie zna `onFailure` — sesje idą przez rozszerzenie VS Code 2.1.296, które go zna.

- 2026-10-13 — **retro 3** ([[2026-10-13-retro-03]]): licznik 10 → 0. Decyzja autora: „tak” dla R1–R10:
  - **hook na zakazane komendy** (Python ze skryptem z wejścia, komendy git spoza listy) → [[ISSUE-031-command-guard]], następna (R1);
  - `qa`: testy dostępności dotyku `meetsGuideline` przy każdym ekranie (R2), logcat bez współrzędnych i adresów przy pozycji z
    siecią (R7);
  - `dev`: przejście AC ze stanami z *States*, tekstem 200% na 360 dp i pomiarem klatki (R3); `ui`: tryb discovery, makieta „gdzie się
    dotyka”, przegląd zapisuje przyjęte odstępstwa (R4); `planning`: „przed czym chronimy?” (R7); przykłady tylko z wymyślonych
    rdzeni (R7);
  - twardy stop „fakt o rodzinie bez źródła” usunięty (R6);
  - **ten plik schudł** (R5): *Recently done* trzyma tylko wpisy od ostatniego retro;
  - **jedna lista rzeczy niesprawdzonych w ręce** i audyt pól modelu ↔ ekrany przed instalacją → [[ISSUE-032-mvp-install]]
    (`draft`; R8, R9);
  - [[ISSUE-003-setup-quality-critic]], [[ISSUE-004-setup-freshness-gate]], [[ISSUE-005-setup-session-start-state]] → `deferred` z
    warunkami obudzenia (R10).

  Na cztery pytania o fakty autor nie odpowiedział — zapisane jako „bez odpowiedzi”, wracają tam, gdzie od nich coś zależy
  (retro 3 → *Load-bearing facts*).
