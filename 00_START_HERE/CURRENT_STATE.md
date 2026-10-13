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
- **Po [[2026-10-13-retro-03]] (R1–R10, decyzja autora 2026-10-13): następna [[ISSUE-031-command-guard]]** — hook, który
  odmawia Pythona ze skryptem z wejścia i komend git spoza listy (R1). Potem dalej droga do instalacji MVP.
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
  7. **po ISSUE-031: [[SPIKE-002-tree-on-a-phone]]** → drzewo, czas, „Połącz dwie osoby” ([[drzewo]], EPIC-003) — od ISSUE-024 także **słownik nazw
     złożonych i dawne AC-6** („ciotka”, „stryj”, „siostra cioteczna babci żony”) i „Pokaż w drzewie” w widoku osoby (SPIKE-002 →
     *Input from ISSUE-024*);
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
  - [[SPIKE-002-tree-on-a-phone]]: przed drzewem (widok 5);
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
    prototypy, zrzuty, pliki Natural Earth i kopie `-0NN` z wymyślonymi danymi — do kosza;
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
- Zamknięte pozycje od ostatniego retro: **0** (ostatnie retro: [[2026-10-13-retro-03]]). Co **10** → retro + pytanie o 3–5
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
