---
title: "Grobing — Current State"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-16
---

# Grobing — Current State

> Żywy obraz tego, gdzie produkt jest teraz. Krótszy i bardziej zmienny niż `SESSION_STATE.md`.

> 📍 **Ten plik jest jedynym licznikiem stanu produktu** — etap dojrzałości, co w toku, licznik do
> retro, sprawy zaparkowane. **Żaden inny plik ich nie powtarza; wszystkie linkują tutaj.** Wolisz
> *„patrz `backlog/issues/`"* niż *„12 zadań"* — wskaźnik się nie zestarzeje.

## Maturity stage
MVP — od startu, cały produkt (Meta-decyzja 4).

## In progress
- **Po [[2026-10-16-retro-04]] (R1–R7, decyzja autora 2026-10-16) — kolejka przed instalacją MVP**, ustalona w `/pm` tego dnia (retro 4 →
  *Product decisions*). **Instalacja ze sklepu najpóźniej 2026-10-29**; prawdziwe dane autor wpisuje w trakcie wyjazdu na Wszystkie Święte:
  1. ~~[[ISSUE-041-google-play-and-safe-update]]~~ — **zamknięte 2026-10-16** w części kodu: migawka bazy przed migracją, numer wersji, README *Wydanie*,
     [[ADR-019-distribution-play-internal-testing]] (zamyka [[NT-005-distribution-decision]]). **Część w sklepie** (Play Console, instalacja z odtworzeniem,
     aktualizacja na telefonie) — decyzją autora przed samą instalacją: [[ISSUE-032-mvp-install]] → *Before install* 0. Prompty do DALL-E z
     [[ISSUE-046-icons]] gotowe (katalog tymczasowy sesji `b20ca21c-…\scratchpad\dalle-prompts-046.md`);
  2. ~~[[ISSUE-042-places-of-residence]]~~ — **zamknięte 2026-10-16**: miejsca zamieszkania od kraju do adresu (schemat v13,
     [[ADR-020-residences-place-in-the-row]]), lista miejsc w aplikacji poza gitem, pusty koniec z następnego miejsca (D12 — decyzja autora na stopie #2);
     wejście dla [[ISSUE-045-migration-map]] → *Notes*;
  3. ~~[[ISSUE-043-grave-paid-until]]~~ — **zamknięte 2026-10-16**: sama data „opłacone do” na dole widoku grobu (wariant B, schemat v14); przypomnienie
     — później aktualizacją, przed najwcześniejszą zapisaną datą;
  4. [[ISSUE-044-family-wreaths]] — wieńce rodzin; prototyp `ui` (discovery) może iść równolegle z 1–3 (zmiana bazy);
  5. [[ISSUE-045-migration-map]] — mapa migracji na suwaku czasu i na telewizorze (bez zmiany bazy);
  6. [[ISSUE-046-icons]] — ikona aplikacji i ikony w aplikacji, wybór na makiecie (bez zmiany bazy);
  7. [[NT-007-hand-over-note]] (warunek obudzenia spełniony: kopia jest i jest eksportem) i [[ISSUE-032-mvp-install]] — audyt, małe poprawki „przed
     instalacją”, lista A *Hand checks*, instalacja ze sklepu.

  **Zasady terminu:** przed instalacją wszystko, co zmienia bazę; widoki bez zmiany bazy (5, 6) mogą przyjść później jako aktualizacja ze sklepu; **w trakcie
  wyjazdu żadnych aktualizacji**. Wszystkie US [[EPIC-001-zabezpiecz-i-przepisz]] i [[EPIC-003-zrozumienie]] zamknięte (EPIC-i zostają `draft` do instalacji —
  ich NFR i rzeczy w ręce sprawdza [[ISSUE-032-mvp-install]]).
- **Agent `architect` — nie teraz** (retro 4, R7): sygnał „pierwszy ADR zastąpiony” ([[ADR-018-export-is-the-backup]]) rozliczony; nowy warunek w `CLAUDE.md` →
  *Na sygnał*.

  Specyfikacja: [[drzewo]] v1.17, [[osoba]] v2.5, [[wpis-osoby]] v5.9, [[zamieszkanie]] v1.2, [[grob]] v8.1, [[style-b]] v1.32.
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
  8. ~~[[US-006-eksport-dla-rodziny]]~~ — zamknięta 2026-10-16 (~~ISSUE-040~~; eksport = kopia, [[ADR-018-export-is-the-backup]]);
  → dalej kolejka z retro 4 (wyżej) → **[[ISSUE-032-mvp-install]]** (`draft`): audyt pól modelu ↔ ekrany (R9), lista A *Hand checks*, warunki
  przed pierwszymi danymi → **instalacja ze sklepu** ([[ISSUE-041-google-play-and-safe-update]]) → prawdziwe dane ([[NT-002-transcribe-the-notes]]) w trakcie wyjazdu.
  Wpisy o zamkniętych pozycjach: retro 3 i retro 4 → *Archive*.

  **EPIC-001:** [[US-004-fakt-od-babci]] **wycofana** (SPIKE-004 D28 — bez źródeł; wiedza od babci przez zwykłą
  poprawę); [[US-006-eksport-dla-rodziny]] zamknięta (eksportem jest kopia).
- **[[SPIKE-001-map-source-offline]] zamknięty 2026-10-08** → [[ADR-003-map-source-offline]] `accepted`: mapa
  cmentarza to **plan schematyczny z OSM offline** + ortofotomapa GUGiK online + kwatery i pinezki autora.
- **Każda pozycja z ekranem: `ui` → `planning`** (`autonomous-flow.md`). Wygląd: `05_DESIGN/brand/` (wytyczne i
  referencje R1–R4 z kick-offu). Kolejność autora z 2026-10-06 (ISSUE-014 → SPIKE-001) wyczerpana — retro 2 → *Archive*.
- Poza tą kolejnością:
  - **opowieść rodziny na drzewie** — pomysł autora ze stopu #2 ISSUE-037 (c) w [[2026-10-14-opowiesc-rodziny-i-wieniec]] (INBOX): najpierw prototyp `ui`
    w trybie discovery, potem pozycje. **Po instalacji MVP** (decyzja autora 2026-10-14). Wieniec (d) przeszedł 2026-10-16 do kolejki jako
    [[ISSUE-044-family-wreaths]];
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
  - **komunikat błędu pod polem nie jest ogłaszany przez czytnik ekranu** ([[ISSUE-043-grave-paid-until]] → *Verification*, przegląd `ui`): `ErrorLine` nie
    jest regionem na żywo — ten sam wzorzec w bloku daty osoby i w oknie „Popraw grób”. Kandydat na drobną pozycję dla całej aplikacji (TalkBack);
  - **imiona przy ścieżce przy tekście 200%** ([[ISSUE-039-connect-two-people]] → *Verification*, obserwacja): przy długiej ścieżce w skali ok. 0,17 imiona dwóch osób
    ścieżki chowają się (nachodzą na inne imiona ścieżki), a wyszarzone imię spoza ścieżki, które na nic nie nachodzi, zostaje. Do oceny autora — np. bez imion
    wyszarzonych w trakcie podświetlenia.
- **Przed pierwszymi prawdziwymi danymi w aplikacji:** kopia jest gotowa (US-001 ✅), poprawki z retro 2 też
  ([[ISSUE-021-small-fixes-after-retro-2]] ✅). Zostały hasło i
  miejsce pliku klucza w notce przekazania ([[NT-007-hand-over-note]]): utrata któregoś z nich = utrata
  kopii. Notkę sprawdzić raz jej własną drogą (`age -d -i …` z hasłem w terminalu — NT-007 → *Input from
  US-001 closure*). Wszystkie warunki przed instalacją zbiera [[ISSUE-032-mvp-install]] → *Before install*.
- **Termin instalacji: najpóźniej 2026-10-29** (decyzja autora 2026-10-16 — retro 4 → *Product decisions*): prawdziwe dane autor wpisuje w trakcie
  wyjazdu na Wszystkie Święte. Do 2026-10-16 obowiązywało „budowa bez terminu” (2026-10-05); przy wizytach autor robi zdjęcia nagrobków z lokalizacją →
  `TRACEABILITY.md` → *Open gaps* 2.
- **Weryfikacja na emulatorze do MVP** (decyzja autora 2026-10-05). Na telefon trafi dopiero MVP, jako build **ze sklepu** (Google Play, testy
  wewnętrzne — [[ISSUE-041-google-play-and-safe-update]]); wyjątki są w `DEFINITION_OF_DONE.md`.
- **Autor, poza sesją:**
  - kopia klucza wydania (`.jks` + oba hasła) w zaszyfrowanym miejscu — **po [[ISSUE-041-google-play-and-safe-update]] nie blokuje** (retro 4): klucz
    podpisu aplikacji ze sklepu trzyma Google, a klucz z `release_keystore_dir` zostaje kluczem przesyłania, który da się zresetować (jak w Friendsheet).
    To **nie** klucz kopii z testów;
  - **notatki rodziny na PC** leżą w `family_data_dir` (`project-config.md`), poza repo. Docelowo
    zdjęcia stron trafiają do zaszyfrowanego miejsca (NT-001);
  - **lista rdzeni strażnika** (`rdzenie-straznika.txt` w `family_data_dir`, spisana przez agenta z notatek 2026-10-08):
    4 nazwiska mają niepewny odczyt pisma (oznaczone na liście). Poprawki — w pliku albo w czacie z agentem. Każde nowe
    nazwisko z przepisywania warto dopisać: rdzeń działa od następnego `git add`;
  - opcjonalnie zmiana hasła klucza (README `grobing-code` → *Podpis wydania*);
  - ~~build release na telefon przez `adb` przed wizytą~~ — **zastąpione 2026-10-16** (retro 4): na telefon (Motorola moto g82 5G, Android 13) trafia MVP
    **ze sklepu**, najpierw na wymyślonych danych do próby aktualizacji ([[ISSUE-041-google-play-and-safe-update]]), potem **wyczyść dane aplikacji**
    (Ustawienia → Aplikacje → Grobing → Pamięć) i prawdziwe dane. **Nie instaluj APK przez `adb` na telefon** — inny podpis i numer wersji niż w sklepie;
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
    ok. 80 MB), `chr\` (profil Chrome bez okna), wyniki testów i skrypty — do kosza. Z sesji ISSUE-040 (`cbd907af-…\scratchpad\`): wycofana makieta `eksport-040.html`,
    zrzuty `shots\`, `gate\` (kopia `grobing-*-040.age`, odszyfrowany plik klucza i `tar` z bazą — **wymyślone dane, hasło testowe**), `agebin\` (oficjalne `age` v1.3.2 —
    można zachować do notki NT-007), obraz testowy, `chr\` i skrypty — do kosza. Z sesji ISSUE-041/042 (`b20ca21c-…\scratchpad\`): makieta
    `makieta-042.html` i jej zrzut, `chr042\`, `emu041\`, wiadomości commitów — do kosza po [[ISSUE-046-icons]] (tam leżą prompty `dalle-prompts-046.md`). Z sesji
    ISSUE-042 (`574c5666-…\scratchpad\`): `dl\` i `src\` — pobrane pliki GeoNames i Natural Earth (ok. 1 GB, dane publiczne; potrzebne tylko do
    ponownej budowy listy miejsc — README `grobing-code` → *Lista miejsc*), `emu042\` (zrzuty, kopia `files/` sprzed pozycji z `Grobing_Restore` —
    **wymyślone dane** i cmentarz dodany poza agentem — oraz APK odniesienia), `ui042\`, `tools\`, logi testów — do kosza. Z sesji ISSUE-043
    (`6983a70d-…\scratchpad\`): `emu043\` (zrzuty `01`–`21`, kopia danych `Grobing_Restore` sprzed pozycji i kopie bazy do liczenia — **wymyślone dane** i
    cmentarz dodany poza agentem), `fonts043\` i skrypty pomiaru przeglądu `ui`, `ui.py`, `counts.py`, logi testów — do kosza;
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
  przestawienie środka 52–57% wolnych w obu buildach (przy ISSUE-033 2–8%) — porównanie tylko naprzemienne. **Po ISSUE-040:** build profile bez wiersza eksportu; Mateusz
  („ja”) ma profilowe z obrazu testowego (`testowy-obraz-040.jpg` w Zdjęciach emulatora); **kopia skonfigurowana z nowym hasłem testowym** (z sesji ISSUE-040) do
  `grobing-klucz-040.age` i `grobing-kopia-040.age` w Pobranych — kopia w tle nadpisuje ten plik. **Po ISSUE-041:** build profile `0.9.0` z migawką
  sprzed aktualizacji; baza przeszła v11 → v12 z wstrzykniętej kopii v11 (te same wymyślone dane), w `files/pre-update/` migawka v11. **Po 13:19 (czas
  emulatora) ktoś poza agentem dodał w aplikacji cmentarz** (publiczny, z bazy OSM) — agent wstrzymał odtworzenie, żeby go nie zastąpić; przed następnym
  użyciem emulatora pytanie do autora, czy jego dane można zastąpić. **Po ISSUE-042:** build profile z miejscami zamieszkania (`FRAME_LOG`), baza v13
  (migawki v11 i v12 w `files/pre-update/`), lista miejsc w `files/places/`; zamieszkania u wymyślonych osób (Bronisława — 2, Mateusz — 2 z samym „Od”,
  nowa osoba w nowym grobie na cmentarzu dodanym poza agentem — 1); ustawienia zmienione do przejścia: `stylus_handwriting_enabled 0` (nakładka rysika
  Gboard), `show_ime_with_hard_keyboard 1` (klawiatura ekranowa przy sprzętowej); kopia w tle v13 z 17:00 UTC przeszła. **Po ISSUE-043:** build profile v14
  z „Opłacone do” (`FRAME_LOG`, `--split-per-abi`), baza v14 (migawki v11–v13 w `files/pre-update/`), tekst i ekran domyślne. **Na stopie #2 autor dodał
  własny grób z datą opłaty** (nazwy nie zapisujemy) — przed następnym użyciem emulatora pytanie do autora, czy jego wpisy (cmentarz i ten grób) można
  zastąpić.
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
- Zamknięte pozycje od ostatniego retro: **3** (ostatnie retro: [[2026-10-16-retro-04]]). Co **10** → retro + pytanie o 3–5
  nośnych faktów (Meta-dec. 3g, 3h SC-16, A3). Licznik żyje **tylko tutaj**; podbija go `docs` przy zamknięciu, a zeruje go retro.
- Do retro (zebrane po drodze, bez decyzji):
  - Poprzednią listę rozliczyło [[2026-10-16-retro-04]] → *The "Do retro" list*.

## Parked (waiting on someone outside the session)
- **cmentarz (którykolwiek z cmentarzy autora)** · przy 3 grobach, które autor zna: (a) dokładność GPS telefonu
  przy grobie w metrach (dowolna mapa z niebieską kropką); (b) czy kropka trafia we właściwą kwaterę, rząd albo
  aleję; (c) czy przy bramie wisi plan z kwaterami. Odpowiedź w czacie: **same liczby i tak/nie**, bez nazw i
  położeń · warunek obudzenia: **najbliższa wizyta na cmentarzu** · 2026-10-08 ([[SPIKE-001-map-source-offline]] D5;
  mierzy H3 i H9 przed budową pinezek w [[EPIC-002-wizyta]]). Prawdopodobna okazja: wyjazd autora na zaduszki
  (~2026-11-02, ten sam co rozmowa z babcią — *In progress*). **Krok w terenie [[ISSUE-029-pin-on-site-gps]] (D4, 2026-10-12):** z MVP
  **ze sklepu** na telefonie (instalacja najpóźniej 2026-10-29, prawdziwe dane wpisywane w trakcie wyjazdu — retro 4) — kropka i jej dokładność przy
  3 grobach, pinezka postawiona i poprawiona, tryb samolotowy, czytelność w słońcu ([[NFR-004-czytelnosc-w-sloncu]]); wynik ustawia próg „słaby
  sygnał” (`weakSignalM`, dziś tymczasowo 15 m) i decyduje o [[ISSUE-030-sector-on-a-visit]]. Odpowiedź w czacie: same liczby i tak/nie. **Ta sama
  wizyta** sprawdzi w terenie [[ISSUE-029-pin-on-site-gps]] — cel autora z 2026-10-12.

Format wpisu: `źródło (babcia / cmentarz X) · pytanie bez danych rodziny · warunek obudzenia
(zdarzenie) · data zapytania`. **Odpowiedź z faktami o rodzinie trafia do aplikacji, nie tutaj.**

## Recently done
> Tylko wpisy od ostatniego retro ([[2026-10-16-retro-04]]; zasada R5 z retro 3). Starsze są w plikach retro → *Archive*:
> [[2026-10-16-retro-04]] · [[2026-10-13-retro-03]] · [[2026-10-08-retro-02]] · [[2026-10-06-retro-01]].

- 2026-10-16 — [[ISSUE-043-grave-paid-until]] zamknięte. **„Opłacone do” przy grobie:**
  - zakres B z `/pm` (decyzja autora): **sama data**, bez „kto płaci” i bez przypomnienia — przypomnienie bazy nie zmienia, więc przyjdzie aktualizacją ze
    sklepu przed najwcześniejszą zapisaną datą; na stopie #1 **W1** — grób bez daty ma wiersz „nie wiadomo” i „Wpisz” ([[grob]] v8, D15–D19);
  - schemat **v14** (`graves.paid_until_*`, [[data-model]]); pole przyjmuje lata do bieżącego + 50, daty osoby dalej bez przyszłości; zapis okna „wszystko
    albo nic”;
  - przejście `dev` znalazło okno, które nie przewijało się do pola przy 200% z klawiaturą; test `qa` pokazał, że poprawka zależała od tempa klawiatury —
    teraz przewija przy zmianie wysokości okna; przegląd `ui`: 0 BLOCKER / 0 MAJOR, 1 MINOR poprawiony, odstępstwa przyjęte ([[grob]] v8.1).

  Dwa wiersze listy A na [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 844 zielonych. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 2 → 3.

- 2026-10-16 — [[ISSUE-042-places-of-residence]] zamknięte. **Gdzie kto mieszkał i kiedy:**
  - stop #1 potwierdzony w `/pm`: **A1** (adres tekstem, punkt w środku miejscowości) i **N2** (nazwa z tamtego czasu obok miejsca z listy);
  - **lista miejsc w aplikacji** (11,7 MB, 239 krajów, ok. 188 tys. miejscowości — 4 kraje w całości, świat `cities5000`; `cities1000` przekroczył próg 15 MB),
    **poza gitem i poza kopią** (G1), wyszukiwanie ≤ 13 ms na emulatorze; schemat **v13** (`residences`, [[ADR-020-residences-place-in-the-row]]);
  - przegląd `ui`: 1 MAJOR (kraje pod 30 miejscowościami — błąd specyfikacji v1, D8) i 3 MINOR — poprawione; [[zamieszkanie]] v1.1, [[style-b]] v1.32;
  - **na stopie #2 decyzja autora D12:** pusty „Do” kończy się początkiem następnego miejsca, wyliczone przy odczycie, nie zapisane ([[zamieszkanie]] v1.2).

  Lista A i B w [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 820 zielonych. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 1 → 2.

- 2026-10-16 — [[ISSUE-041-google-play-and-safe-update]] zamknięte (w części kodu). **Aktualizacja bez utraty danych:**
  - decyzja autora: **Google Play, testy wewnętrzne, klucz od Google** → [[ADR-019-distribution-play-internal-testing]] (zamyka [[NT-005-distribution-decision]]);
    na telefon nic poza sklepem;
  - **migawka bazy przed migracją** (K3, stop #1 *„tak”*): `pre-update/grobing-v<stara>.db`, 3 najnowsze; sonda i test pokazały, że po przerwanym zapisie
    (gorący dziennik 1,4 MB) migawka ma zatwierdzone dane i wersję; na emulatorze v11 → v12, 750 wierszy przed i po; numer wersji `0.9.0+1`; README →
    *Wydanie* z drogą powrotu przy złej migracji;
  - **na stopie #2 autor wolał najpierw funkcje z kolejki** — część w sklepie (AC-1) przeszła do [[ISSUE-032-mvp-install]] → *Before install* 0.

  Trzy wiersze listy A na [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 777 zielonych. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 0 → 1.

- 2026-10-16 — **retro 4** ([[2026-10-16-retro-04]]): licznik 10 → 0. Decyzja autora: „wszystko ok” dla R1–R7:
  - `pm`: jedno pytanie o cel przed `ui` przy US z kick-offu i nowych pomysłach (R1); US bez ISSUE → `docs` rozpisuje przed `ui` (R2);
  - `ui`, `planning`: makieta jako `file:///`, wybór techniki opisany tym, co autor widzi i robi, zmiana decyzji potwierdzona na makiecie przed
    specyfikacją (R1);
  - `dev`: „mieści się” = liczba i najgorszy przypadek, pomiar klatek naprzemiennie z buildem odniesienia, przenikanie grupy = jedna warstwa (R3);
  - **Hand checks w dwóch listach:** A — dane, bramka przed prawdziwymi danymi; B — odczucie, w trakcie używania, bez bramki (R4, zmienia R8 z retro 3);
  - `qa`: `flutter test --timeout 120s`, szukanie w trasie (R5); przy otwartym stopie jedno pytanie na raz (R6); `architect` nie teraz, nowy warunek (R7).

  Fakty: telefon Motorola moto g82 5G, Android 13; konto Play to samo co przy Friendsheet; zdjęcia notatek przy autorze — pytanie zamknięte decyzją autora.
  **W tej samej sesji** decyzje produktowe: Google Play (testy wewnętrzne, klucz od Google), instalacja najpóźniej 2026-10-29, kolejka
  [[ISSUE-041-google-play-and-safe-update]] … [[ISSUE-046-icons]] → [[ISSUE-032-mvp-install]], odrzucone propozycje — *In progress* i retro 4 →
  *Product decisions*.
