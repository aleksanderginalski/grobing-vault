---
title: "Grobing — Current State"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-14
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
  zamknięte 2026-10-13 (*Recently done*). Dalej droga do instalacji MVP: ~~[[US-009-drzewo-od-osoby]]~~ **zamknięta 2026-10-14** (~~ISSUE-033~~,
  ~~ISSUE-034~~, ~~ISSUE-035~~, ~~ISSUE-036~~); ~~[[US-010-czas-na-drzewie]]~~ **zamknięta 2026-10-14** (~~ISSUE-037~~, ~~ISSUE-038~~ — historia na telewizorze i
  tempo, zamknięte 2026-10-14); ~~[[US-011-polacz-dwie-osoby]]~~ **zamknięta 2026-10-14** (~~ISSUE-039~~). **Wszystkie US
  [[EPIC-003-zrozumienie]] zamknięte** (EPIC zostaje `draft` do instalacji — jego rzeczy w ręce są na [[ISSUE-032-mvp-install]] → *Hand checks*). **Następna:
  [[US-006-eksport-dla-rodziny]]** (punkt 8 drogi niżej; `ready`, bez ISSUE — rozpisanie `docs` przed `ui`, jak przy US-011; nowy ekran eksportu → `ui` z
  makietą), potem [[NT-007-hand-over-note]].

  Specyfikacja: [[drzewo]] v1.17, [[osoba]] v2.4, [[style-b]] v1.31.
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
  7. ~~[[SPIKE-002-tree-on-a-phone]]~~ — zamknięty 2026-10-13 → ~~[[US-009-drzewo-od-osoby]]~~ — zamknięta 2026-10-14 (~~ISSUE-033~~, ~~ISSUE-034~~,
     ~~ISSUE-035~~, ~~ISSUE-036~~; drzewo od osoby, S2, ślad dalszej rodziny, słownik nazw złożonych, „Pokaż w drzewie”, tryb prezentacji, „Przesyłaj na
     telewizor”) → ~~[[US-010-czas-na-drzewie]]~~ — zamknięta 2026-10-14 (~~ISSUE-037~~; suwak czasu, daty niepewne, „//”; ~~ISSUE-038~~ — historia na telewizorze i
     tempo) → ~~[[US-011-polacz-dwie-osoby]]~~ — zamknięta 2026-10-14 (~~ISSUE-039~~; okno „Połącz dwie osoby”, ścieżka na drzewie, baner);
  8. **[[US-006-eksport-dla-rodziny]]** (następna) i [[NT-007-hand-over-note]];
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
  - **opowieść rodziny na drzewie i wieniec przy portrecie według nazwiska** — pomysły autora ze stopu #2 ISSUE-037 (c, d) w
    [[2026-10-14-opowiesc-rodziny-i-wieniec]] (INBOX): najpierw prototyp `ui` w trybie discovery, potem pozycje. Wieniec zmienia decyzję „bez gałązek”
    ([[style-b]] reguła 8, [[osoba]] D3) i schemat (nowa tabela). **Po instalacji MVP** (decyzja autora 2026-10-14);
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
    ISSUE-029);
  - **tabliczka imienia zasłania ślad dalszej rodziny w dół przy oddaleniu** ([[ISSUE-035-tree-names-shrink-my-voice]] → *Verification*, przegląd
    `ui`, MINOR od [[ISSUE-033-tree-from-a-person]]): przy I2 tabliczka rośnie o 1/skala, a kreska „dzieci poza widokiem” (D9) zaczyna się w stałym
    miejscu pod imieniem — przy tekście 100% znika od skali ok. 0,48, przy 200% od ok. 0,65; na poziomie 2 zostaje. Poprawka: kreska od dolnej
    krawędzi tabliczki na ekranie. Kandydat na małą pozycję. Przegląd `ui` [[ISSUE-039-connect-two-people]] dorzucił obok: linia od pary do dzieci biegnie
    tuż przy końcu tabliczki długiego imienia („Agnieszka”) — przy ścieżce w akcencie bardziej to widać;
  - **rodzeństwo przyrodnie w słowniku** ([[ISSUE-039-connect-two-people]] → *Dev report* → *Found, poza pozycją*): przyrodni brat dziadka to „Syn mojej
    prababci” — w karcie i na banerze „Połącz dwie osoby”. `KinGraph` łączy rodzeństwem tylko dzieci tej samej rodziny, a słownik
    ([[ISSUE-025-gender-kinship-together-since]] D2) nie ma „przyrodni”. Kandydat na małą pozycję, przed prawdziwymi danymi (powtórne związki są w notatkach);
  - **imiona przy ścieżce przy tekście 200%** ([[ISSUE-039-connect-two-people]] → *Verification*, obserwacja): przy długiej ścieżce w skali ok. 0,17 imiona dwóch osób
    ścieżki chowają się (nachodzą na inne imiona ścieżki), a wyszarzone imię spoza ścieżki, które na nic nie nachodzi, zostaje. Do oceny autora — np. bez imion
    wyszarzonych w trakcie podświetlenia.
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
    prototypy, zrzuty, pliki Natural Earth i kopie `-0NN` z wymyślonymi danymi — do kosza. Z drzewa zostały: `220a9b6c-…\scratchpad\drzewo-spike002.html`
    (makieta kandydatów SPIKE-002) i `c3868f5f-…\scratchpad\` — makieta `drzewo-us009.html`, zrzuty `shots-033\`, kopia bazy testowej
    `test-grobing.db` i kopia konfiguracji AVD (wszystko wymyślone) — po [[ISSUE-035-tree-names-shrink-my-voice]] do kosza (I1/G2 rozstrzygnięte; gdyby
    wrócił temat imion przy oddalaniu, kandydaci są opisani w [[drzewo]] *Candidates — US-009*). Z sesji ISSUE-034 (`940e38e7-…\scratchpad\`): zrzuty
    `shots-034\`, kopie bazy testowej `test-034*.db` (wymyślone), APK SystemUI z emulatora (`sysui\`, ok. 45 MB, do odczytu nazwy kafelka) i skrypty — do
    kosza. Z sesji ISSUE-035 (`da0c23f6-…\scratchpad\`): zrzuty `shots-035\`, kopia bazy testowej `test-035.db` (wymyślone), pliki planu i raportów,
    skrypty, powiększenia z przeglądu `ui` — do kosza. Z sesji ISSUE-036 (`fa865b36-…\scratchpad\`): makieta `drzewo-036.html`, zrzuty i nagrania ekranu `shots-036\`
    (wymyślone dane), logi testów i klatek — do kosza. Z sesji ISSUE-037 (`555909c3-…\scratchpad\`): cały katalog do kosza — makieta `drzewo-037.html`, zrzuty
    `shots-037\`, `shots-emu\` (wymyślone; makieta ISSUE-038 już z nich powstała), `base\` (kopia drzewa roboczego `grobing-code` z buildem, ok. 0,5 GB, **bez**
    `key.properties`), `fjar\`, `ref\` (PDF-y TimeNets i genogramu), logi klatek i skrypty. Z sesji ISSUE-038 (`baf00b7b-…\scratchpad\`): makieta `drzewo-038.html`, zrzuty
    `shots-038\` i `shots-emu\` (wymyślone), `base\` (dwa APK profile, ok. 80 MB), `chr\` (profil Chrome bez okna), źródła Media3, skrypty — do kosza. Z sesji ISSUE-039
    (`0558e715-…\scratchpad\`): makieta `drzewo-039.html` z częściami (`parts\`), zrzuty `shots-039\` i `emu\shots\` (wymyślone), `emu\base\` (APK profile ISSUE-038 i ISSUE-039,
    ok. 80 MB), `chr\` (profil Chrome bez okna), wyniki testów i skrypty — do kosza;
  - **repo nie mają pliku `LICENSE`** — kod można oglądać, ale nie wolno go używać. Licencję można dodać później.
- **Emulatory (po ISSUE-033):** `Medium_Phone` — release v12 na danych testowych autora, kopia skonfigurowana od nowa z hasłem
  testowym (wymyślone, z sesji ISSUE-029), pliki `grobing-klucz-029.age` i `grobing-kopia-029.age` w Pobranych; grób „Jozef” ma
  pinezkę z poprawki autora; **wyłączony** na czas ISSUE-033, dane nietknięte. `Grobing_Restore` — **build profile** (podpis debug,
  `--dart-define=FRAME_LOG=true` — czasy klatek w logcat `GROBING_FRAME`; od ISSUE-034 z trybem prezentacji, od ISSUE-035 z kartą w G2, od ISSUE-036 z ikoną
  „Przesyłaj na telewizor”; system po angielsku, ekran „Google Cast” bez urządzeń; systemowe okno „Viewing full screen” już potwierdzone, ustawienia ekranu i nawigacja gestami jak przed testami) z wymyśloną rodziną do drzewa (106 osób, „ja” = Mateusz); release z
  danymi kopii `-029` odinstalowany (D5 ISSUE-033); **`hw.gpu.enabled=yes`** (było `no` — rysowanie programowe zawyżało czasy klatek). Release na
  `Grobing_Restore` wymaga odinstalowania profile (inny podpis). Następna pozycja z kopią: nowe hasło testowe. **Po ISSUE-037:** build profile z suwakiem czasu, dane
  aplikacji wyczyszczone (`pm clear`, D4) i wymyślona rodzina dodana od nowa — z datami niepewnymi (ok., między, przed, po, bez daty) i trzema ślubami bez daty; skale
  animacji i tekstu z powrotem na 1. **Pomiar klatek na nim jest dziś zaszumiony** (przesuwanie 10–26% wolnych klatek także na buildzie sprzed ISSUE-037) — porównanie
  tylko naprzemienne z buildem odniesienia (ISSUE-037 → *Dev report* → *Measurements*). **Po ISSUE-038:** build profile z tempem i historią w trybie prezentacji (`FRAME_LOG`);
  tekst, gęstość i animacje domyślne, „Czas na działanie” usunięty, TalkBack wyłączony (okno zgody TalkBack na powiadomienia zamknięte „Nie zezwalaj”). Build odniesienia
  do pomiaru klatek: APK zainstalowany na emulatorze, ściągnięty przed instalacją nowego (`adb shell pm path com.grobing.app`, `adb pull`; sposób z ISSUE-038) — kopia drzewa
  roboczego niepotrzebna. **Po ISSUE-039:** build profile z „Połącz dwie osoby” (`FRAME_LOG`, `--split-per-abi`, bo zainstalowany ma `versionCode` 4001); dane aplikacji
  wyczyszczone (`pm clear`) i wymyślona rodzina dodana od nowa — **107 osób, z Teofilem bez rodziny**; tekst, gęstość, animacje i „Czas na działanie” domyślne. Klatki tego dnia:
  przestawienie środka 52–57% wolnych w obu buildach (przy ISSUE-033 2–8%) — porównanie tylko naprzemienne.
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
- Zamknięte pozycje od ostatniego retro: **9** (ostatnie retro: [[2026-10-13-retro-03]]). Co **10** → retro + pytanie o 3–5
  nośnych faktów (Meta-dec. 3g, 3h SC-16, A3). Licznik żyje **tylko tutaj**; podbija go `docs` przy zamknięciu, a zeruje go retro.
- Do retro (zebrane po drodze, bez decyzji):
  - **US bez ISSUE na starcie łańcucha** ([[ISSUE-033-tree-from-a-person]]): `pm` skierował [[US-009-drzewo-od-osoby]] prosto do `ui`, a plan nie miał
    pliku, w którym mógłby stanąć — `planning` zawołał `docs` do rozpisania w środku łańcucha. Przy US-007 i US-008 rozpisanie (`docs`) szło przed
    `ui`; tabela *Routing* w `pm` tego kroku nie zna.
  - **Makieta podana jako ścieżka z `%TEMP%` się nie otwiera** ([[ISSUE-034-tree-presentation-mode]], stop #1): przeglądarka nie rozwija `%TEMP%`.
    Autor otworzył `drzewo-us009.html` dopiero z adresem `file:///` i zmienił dwie decyzje ze stopu #1 ISSUE-033 (I2 → I1, G1 → G2) — tamto „Tak”
    zapadło najpewniej bez makiety. Koszt: jedna pozycja ([[ISSUE-035-tree-names-shrink-my-voice]]).
  - **Słowa techniczne przy wyborze techniki** ([[ISSUE-034-tree-presentation-mode]], stop #2): D11 („Przesyłaj ekran” + tryb, bez Google Cast)
    przyjęte na stopie #1 SPIKE-002, a autor rozumiał „tryb telewizora” jak przesyłanie w YouTube. Różnica *casting* / *przesyłanie ekranu* wyszła
    dopiero na stopie #2, po budowie.
  - **Ta sama decyzja zmieniona dwa razy** ([[ISSUE-035-tree-names-shrink-my-voice]], stop #1): imiona przy oddalaniu I2 (stop #1 ISSUE-033) → I1
    (stop #1 ISSUE-034) → I2 (stop #1 ISSUE-035). `ui` i `planning` rozpisali I1 (specyfikacja, wyjątek w [[style-b]], plan), a autor przy
    odpowiedzi na sekcje makiety wybrał I2 — zapis cofnięty przed budową. Pozycja założona na zmianie decyzji ruszyła bez potwierdzenia jej na
    makiecie przed `ui`.
  - **Kanon dał zły sygnał, pomiar go złapał** ([[ISSUE-036-cast-from-the-app]], krok 0 `dev`): plan oparł powrót z ekranu systemu na `hidden` → `resumed`
    (stany Fluttera), a na emulatorze szybki powrót wstecz w ogóle nie chowa aplikacji — Android zatrzymuje ją dopiero po chwili. Pierwsza wersja `dev` miała
    też bezpiecznik 2 s, który zwalniał czekanie, zanim przyszło `hidden`. Krok 0 przed budową znalazł oba w jednej rundzie; bez niego wyszłoby to na stopie #2.
  - **Pełny `flutter test` zawisł raz** ([[ISSUE-036-cast-from-the-app]] → *Verification*): jeden proces `flutter_tester` stał 13 min bez wskazania testu; drugi
    przebieg z `--timeout 120s` — 728 zielonych w 1:25. Kandydat: `--timeout` na stałe w rytuale WZ-024, żeby zawieszenie nazwało test.
  - **Lekcja z ISSUE-033 powtórzona w kodzie, który ją cytuje** ([[ISSUE-037-time-on-the-tree]] → *Dev report* → *Found* a): komentarz w `tree_screen.dart` mówił
    „one layer for all who appear … an Opacity on each person was a layer each”, a pierwsza wersja suwaka dała `AnimatedOpacity` każdej osobie — 14,6% wolnych klatek przy
    ▶. Złapał to pomiar klatki z listy przejścia AC (retro 3, R3), nie przegląd. Kandydat: zasada „przenikanie grupy — jedna warstwa” w `dev`, nie tylko w komentarzu.
  - **Punkt odniesienia dla pomiaru klatek** ([[ISSUE-037-time-on-the-tree]] → *Measurements*): przesuwanie na emulatorze dało dziś 20–30% wolnych klatek i wyglądało na
    regres; dopiero build z ostatniego commita (kopia drzewa roboczego z `git show HEAD:…`, bo `git archive` jest poza listą strażnika) pokazał 10–25% — szum hosta (ok. 46%
    obciążenia). Kandydat: pomiar klatek zawsze naprzemiennie z buildem odniesienia.
  - **Dwa pytania w jednej odpowiedzi przy otwartym stopie #2** ([[ISSUE-037-time-on-the-tree]]): pytanie o nowe zadania i otwarte kroki stopu #2 w jednej wiadomości — autor
    odpisał „ok” i nie było wiadomo, na co. Rozstrzygnął stan emulatora (bez śladu kroków) i ponowne pytanie. Kandydat: przy otwartym stopie każde inne pytanie osobno albo
    z jawnym „na które odpowiadasz?”.
  - **Przegląd `ui` ze zrzutów znalazł usterkę z poprzedniej pozycji** ([[ISSUE-038-history-on-tv-and-tempo]] → *Dev report* → Found d): dopasowanie poziomu 2 w trybie
    prezentacji przegrywało porównanie przez zaokrąglenie (z ISSUE-034). `dev` uznał, że „drzewo jest szersze niż ekran”, a test w czcionce testowej granicy nie trafia — przyczynę
    wyliczył przegląd z geometrii zrzutu (skala, szerokość, położenie środka). Kandydat: przy „nie mieści się” w *Dev report* — liczba, nie opis.
  - **Strażnik komend złapał pomyłkę agenta** ([[ISSUE-038-history-on-tv-and-tempo]], `ui`): do komendy z `sed` trafiło przez pomyłkę `python -I -` — odmowa przy próbie, nic się
    nie wykonało ([[ISSUE-031-command-guard]] działa). Kandydat: nic do zmiany, wpis jako dowód mechanizmu.
  - **Stop #2 „pomiń” we wszystkich krokach** ([[ISSUE-038-history-on-tv-and-tempo]]): trzy kroki odczucia na emulatorze, a odpowiedź jedna. Lista [[ISSUE-032-mvp-install]] →
    *Hand checks* rośnie o pozycję (siedem wierszy). Kandydat: pytanie na retro, czy kroki odczucia przy pozycjach z telewizorem odkładać od razu do telefonu z telewizorem.
    **Drugi raz z rzędu** w [[ISSUE-039-connect-two-people]] (bez telewizora): trzy kroki, „Pomiń”. Lista *Hand checks* ma już ponad 40 wierszy.
  - **Pomiar makiety dołożył pytanie przed stopem #1** ([[ISSUE-039-connect-two-people]], `ui`): AC-2 „ustawia ścieżkę w kadrze” na 360 dp nie zawsze się da (10 ze 105 ścieżek
    nawet przy 0,4) — stąd F1/F2. Dowód, że kandydaci z pomiarem przed rekomendacją (retro 2, R6) łapią rzeczy, których AC nie widziało; test układu potwierdził liczbę makiety (9
    ścieżek „4 +”).
  - **Przegląd `ui` znalazł MAJOR po zielonym przejściu i testach** ([[ISSUE-039-connect-two-people]]): imiona przy kadrze F2 przy 200% — przejście `dev` przy 200% szło krótką
    ścieżką (Piotr → Zofia), a najszersza ścieżka (Zdzisław) tylko przy 100%. Kandydat: przy regule „mieści się / kadr” przejście 200% na **najgorszym** przypadku z pomiaru, nie na przykładzie.
  - **Test trafiał w kartę pod listą** ([[ISSUE-039-connect-two-people]], `qa`): `find.text('Wanda …')` znajdował kartę drzewa pod ekranem wyboru, więc dotknięcie szło w inną osobę
    i siedem testów padło z mylącymi powodami. Kandydat: w testach z kilkoma trasami na ekranie szukać w trasie (`find.descendant(of: ekran)`).
  - **Strażnik komend złapał `python -I -` drugi raz** ([[ISSUE-039-connect-two-people]], `qa`) — odmowa przy próbie, nic się nie wykonało; dowód mechanizmu jak w ISSUE-038.
  - Poprzednią listę rozliczyło [[2026-10-13-retro-03]] → *The "Do retro" list*.

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

- 2026-10-14 — [[ISSUE-039-connect-two-people]] zamknięte — **[[US-011-polacz-dwie-osoby]] zamknięta** (AC-1–AC-4), **wszystkie US [[EPIC-003-zrozumienie]] zamknięte**.
  **„Połącz dwie osoby” na drzewie:**
  - rozpisanie `docs` przed `ui` (lekcja z *Do retro*); prior art ([[drzewo]] D43): FamilySearch — ścieżka tylko od „mnie”; Snackbar Androida bierze czas z „Czasu na działanie”
    (flaga treści, bez sterowania); WCAG SC 4.1.3. Pomiar makiety: 10 ze 105 ścieżek od „Ja” nie mieści się na 360 dp nawet przy 0,4 → pytanie F;
  - **decyzje autora na stopie #1 (*„Tak”*):** A1 — ikona `link_outlined` · W2 — „Do” w środku, karta trzyma nazwę · F2 — drzewo maleje, aż cała ścieżka się zmieści ·
    O2 — przy „Od” innym niż Ty dwie linie bez odmiany imion („Piotr Przykładowy → Zofia Wymyślona” / „Wnuczka”) · Y1 — ścieżka ustawia „dziś”; bez „ja” ikony nie ma;
    Teofil Przykładowski (bez rodziny) w wymyślonej rodzinie;
  - linia w akcencie po liniach rodziny, 0,7 s na krok, reszta przy 30% i poza czytnikiem; baner po dojściu linii, 4 s albo dłużej z ustawienia; koniec podświetlenia na każde
    działanie z D49;
  - **złapane przed stopem:** kadr za wysoko przy klawiaturze, baner zasłaniający ścieżkę przy 200% (`dev`), węzeł baneru dla czytnika (test `qa`), imiona poza kadrem F2 przy 200%
    (MAJOR przeglądu `ui`) i 5 MINOR → [[drzewo]] v1.17.

  Stop #2 „pomiń”; pięć wierszy na [[ISSUE-032-mvp-install]] → *Hand checks*. Rodzeństwo przyrodnie w słowniku → *Poza tą kolejnością*. Testy: 773 zielone. Werdykt `qa`:
  APPROVED (self-check, z uwagami). Licznik retro: 8 → 9.

- 2026-10-14 — [[ISSUE-038-history-on-tv-and-tempo]] zamknięte ([[US-010-czas-na-drzewie]] AC-3 — nowe brzmienie). **Historia na telewizorze i tempo lat:**
  - prior art ([[drzewo]] D38): skala TV Androida (36 sp dla liczb), margines 5% (48 dp), wysokość znaku w kącie widzenia (ISO 9241: min. 16′); rok w 36 sp ma z 3 m 23–46′
    (32–65″); odtwarzacz Media3 — sterowanie chowa się po 5 s, dotknięcie chowa;
  - **decyzje autora na stopie #1 (*„Ok”*):** L1 — rok w lewym górnym rogu · B2 — listwa na dole jak w odtwarzaczu (▶, suwak, tempo) i „Zakończ prezentację”, 5 s · V2 — „Wolno” ·
    „Średnio” · „Szybko” = 5 · 10 · 20 lat/s, domyślnie „Średnio” (od 1880 ok. 15 s) · Z2 — tryb z rokiem z karty (zmienia D37); kandydaci na makiecie `drzewo-038.html` z
    podglądem „z kanapy”;
  - „Czas na działanie” z ułatwień dostępu wydłuża sterowanie (kanał `grobing/external`, Android 10+); z czytnikiem sterowanie jest od wejścia i nie znika;
  - przegląd `ui`: 2 MAJOR poprawione przed stopem — tabliczka roku przechwytywała dotyk, a dopasowanie poziomu przy 200% przegrywało przez zaokrąglenie (usterka z ISSUE-034,
    poprawka poza pierwotnym zakresem, zgłoszona na stopie #2); 3 odstępstwa `dev` przyjęte → [[drzewo]] v1.15, [[style-b]] v1.31; płynność w szumie buildu odniesienia.

  Stop #2 „pomiń” we wszystkich krokach; siedem wierszy na [[ISSUE-032-mvp-install]] → *Hand checks*. Imiona na telewizorze poniżej progu czytelności → wejście do
  [[2026-10-14-opowiesc-rodziny-i-wieniec]]. Testy: 754 zielone. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 7 → 8.

- 2026-10-14 — [[ISSUE-037-time-on-the-tree]] zamknięte — **[[US-010-czas-na-drzewie]] zamknięta** (AC-1–AC-3). **Czas na drzewie — suwak w karcie:**
  - prior art ([[drzewo]] D31): TimeNets szacuje brakujące daty z rodziny i pokazuje niepewność; liczby okna z Gramps (20 lat między pokoleniami, 110 lat życia);
    „//” rozwodu z genogramu (D35); [[FR-004-data-z-dopiskiem]] pokryte w części suwaka;
  - **decyzje autora na stopie #1 (*„tak”*):** N3 — przerywany obrys „nie wiadomo, czy w tym roku żyje”, znicz dopiero na pewno · C1 — pusty pierścień „Ja” przed
    narodzinami · T2 — suwak od dekady przed najwcześniejszą datą (tu 1860), AC-3 przeredagowane · E3 — „//” od końca związku, także na „dziś” · R2 — przy
    „Usuń animacje” dekada co sekundę; kandydaci na makiecie `drzewo-037.html`;
  - wymyślona rodzina z datami jak w notatkach (ok., między, przed, po, bez daty, zgon bez daty, trzy śluby bez daty) — układ drzewa bez zmian (D3);
  - **złapane na emulatorze:** warstwa przezroczystości na każdej osobie (▶: 14,6% → 7–9% wolnych klatek po wspólnych warstwach i timerze na rok) i suwak skaczący pod
    palcem; przegląd `ui`: 0 BLOCKER, 0 MAJOR, 3 MINOR poprawione przed stopem → [[drzewo]] v1.13, [[style-b]] v1.29.

  Stop #2 „ok” ze śladem na urządzeniu; autor: *„dla mnie za szybko”* → tempo w [[ISSUE-038-history-on-tv-and-tempo]] (następna); animacje związków, zbliżenia i wieniec
  przy portrecie → [[2026-10-14-opowiesc-rodziny-i-wieniec]] (po instalacji MVP). Trzy wiersze na [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 742 zielone.
  Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 6 → 7.

- 2026-10-14 — [[ISSUE-036-cast-from-the-app]] zamknięte — **[[US-009-drzewo-od-osoby]] zamknięta** (AC-8). **„Przesyłaj na telewizor” w drzewie:**
  - prior art ([[drzewo]] D29, źródła SDK Androida): aplikacja bez Google Cast może tylko **otworzyć systemowy ekran przesyłania** („Google Cast”, ustawienia
    telefonu) — okienka z listą nad treścią jak w Zdjęciach nie da się zrobić, a samo przesyłanie włącza system;
  - **decyzja autora na stopie #1 (*„tak”*): P2** — jedna ikona `cast_outlined` zamiast ikony telewizora: ekran systemu → wstecz → tryb prezentacji bez podpowiedzi;
    telefon bez tego ekranu → od razu tryb z podpowiedzią ([[drzewo]] D30); kandydaci P1–P3 na makiecie ze zrzutów z emulatora;
  - krok 0 `dev`: powrót rozpoznawany po `inactive` → `resumed`, bo szybki powrót nie chowa aplikacji (*Do retro*); AC-2 sprawdzone jednorazową sondą bez ekranu
    przesyłania; przejście po powrocie ok. 1,1 s z chwilą niedopasowanego drzewa (pamięć grafiki zwolniona po zatrzymaniu) — obserwacja, na telefon;
  - przegląd `ui`: 0 BLOCKER, 0 MAJOR, 2 MINOR zamknięte; odstępstwa `dev` przyjęte → [[drzewo]] v1.11. Bez sieci, uprawnień i zależności (NFR-005).

  Stop #2 „ok” — oba kroki ze śladem na urządzeniu; pięć wierszy na [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 728 zielonych. Werdykt `qa`: APPROVED
  (self-check, z uwagami). Licznik retro: 5 → 6.

- 2026-10-14 — [[ISSUE-035-tree-names-shrink-my-voice]] zamknięte ([[US-009-drzewo-od-osoby]] AC-5). **Karta drzewa mówi Twoim głosem:**
  - „Moja babcia”, „Mój stryj (brat taty)”, „Babcia mojej żony”, „Brat wujeczny mojego taty”, „to ja”, „nie wiadomo jeszcze, kim jest dla mnie”; opis dla
    czytnika ten sam. Zdania aplikacji („Wybierz, która osoba to Ty”, „Twoje cmentarze”) zostają w drugiej osobie — [[drzewo]] D28, nowa zasada „kto
    mówi” w [[style-b]] reguła 7 (źródło: Microsoft Writing Style Guide → Person; FamilySearch „My Grandmother”);
  - **imiona przy oddalaniu zostają I2** — na stopie #1 autor odpowiedział na sekcje makiety „1 I2” (wcześniej I1 na stopie #1 ISSUE-034); zapis I1 w
    specyfikacji i wytycznych cofnięty przed budową ([[drzewo]] D27). Skutek: tryb prezentacji przy tekście 200% pokazuje 13 z 20 imion;
  - 2 pliki kodu, bez zmian w rysowaniu; przegląd `ui`: 0 BLOCKER, 0 MAJOR, 1 MINOR spoza pozycji (ślad w dół pod tabliczką — *In progress* → *Poza tą
    kolejnością*).

  Stop #2 „ok” bez śladu na urządzeniu (autor: „zapisz bez śladu”); trzy wiersze na [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 727 zielonych.
  Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 4 → 5.

- 2026-10-14 — [[ISSUE-034-tree-presentation-mode]] zamknięte ([[US-009-drzewo-od-osoby]] AC-8). **Tryb prezentacji drzewa — obraz na telewizor
  przez systemowe przesyłanie ekranu:**
  - ikona telewizora w pasku drzewa → poziomo, bez pasków systemu i przycisków, poziom 2 dopasowany do ekranu; dotknięcie osoby — ona w środku;
    pusty dotyk → na 3 s „Zakończ prezentację”; wstecz też kończy; po wyjściu pion, ta sama osoba, karta. Bez sieci i nowych uprawnień;
  - krok 0: `immersiveSticky` działa przy `targetSdk 36` (dokumentacja Fluttera w SDK twierdziła, że nie) — kanał natywny niepotrzebny;
  - **błąd złapany na emulatorze:** paski chowane w trakcie obrotu zostawiały aplikację w pionowym rozmiarze w poziomym oknie (6 z 8 wejść przy
    200%) — paski dopiero po obrocie, 16 z 16; przeciągnięcie od krawędzi przesuwało drzewo — pasy 24 dp przy czterech krawędziach;
  - przegląd `ui`: 0 BLOCKER, 0 MAJOR, 2 MINOR poprawione; 6 odstępstw przyjętych → [[drzewo]] v1.8 (D25, D26 — podpowiedź mówi o funkcji, bo
    kafelek to „Przesyłanie” na Pixelu, „Smart View” u Samsunga);
  - **decyzje autora:** stop #1 — I1 i „Moja” (osobna pozycja [[ISSUE-035-tree-names-shrink-my-voice]]); stop #2 — chciał „jak w YouTube”:
    zostaje przesyłanie ekranu (jego telewizor to odbiornik Google Cast), wejście z aplikacji → [[ISSUE-036-cast-from-the-app]], casting — po MVP.

  Stop #2 „ok” — krok 1 ze śladem, krok 2 częściowo; sześć wierszy na [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 727 zielonych. Werdykt
  `qa`: APPROVED (self-check, z uwagami). Licznik retro: 3 → 4.

- 2026-10-13 — [[ISSUE-033-tree-from-a-person]] zamknięte ([[US-009-drzewo-od-osoby]] AC-1–AC-7). **Zakładka Drzewo działa — od „Ja”, z poziomami:**
  - wymyślona rodzina o kształcie prawdziwej (106 osób, debug i profile — przycisk w „Stanie danych”); układ = port makiety SPIKE-002, liczby
    6 / 20 / 66 / 99 identyczne z M1; bez nowej zależności;
  - dotknięcie stawia osobę w środku, oddalanie i + / − dokładają poziomy (pigułka „Poziom 3 · 66 osób”), podwójne dotknięcie przybliża,
    ślad dalszej rodziny na zewnątrz od środka; drzewo wraca do kadru, gdy ucieknie;
  - karta: „Twoja ciotka (siostra taty)”, „Siostra cioteczna babci Twojej żony” — słownik ISSUE-025 z odcinkami liczonymi od drugiej osoby
    ([[drzewo]] D12); „Pokaż w drzewie” w widoku osoby; tekst 200%;
  - **decyzje autora na stopie #1 (*„Tak”*):** I2 (imiona czytelne, nakładające się chowają), G1 („Twoja babcia”), dwie pozycje ([[ISSUE-034-tree-presentation-mode]]
    następna), wymyślone dane za `!kReleaseMode`;
  - przejścia między poziomami: 2–8% wolnych klatek na emulatorze z GPU (SPIKE-002: do 55%) — po zamianie cieni pod imionami na tabliczkę i
    jednej warstwie przezroczystości;
  - przegląd `ui`: 1 MAJOR (poświata nad okręgiem zabarwiała „Ja” i zdjęcia) + 3 MINOR — poprawione przed stopem; poświata poprawiona też w
    mini-drzewie i portrecie osoby („ok” autora na stopie #2) — [[style-b]] v1.27; [[drzewo]] v1.7.

  Stop #2 „ok” — kroki 1–2 ze śladem na emulatorze, krok 3 bez śladu; dwa wiersze na [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 721
  zielonych. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 2 → 3.

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
