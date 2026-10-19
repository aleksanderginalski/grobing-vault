---
title: "Grobing — Current State"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-19
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
     aktualizacja na telefonie) — decyzją autora przed samą instalacją: [[ISSUE-032-mvp-install]] → *Before install* 0 (ikona 512 do karty sklepu gotowa —
     [[ISSUE-046-icons]]);
  2. ~~[[ISSUE-042-places-of-residence]]~~ — **zamknięte 2026-10-16**: miejsca zamieszkania od kraju do adresu (schemat v13,
     [[ADR-020-residences-place-in-the-row]]), lista miejsc w aplikacji poza gitem, pusty koniec z następnego miejsca (D12 — decyzja autora na stopie #2);
     wejście dla [[ISSUE-045-migration-map]] → *Notes*;
  3. ~~[[ISSUE-043-grave-paid-until]]~~ — **zamknięte 2026-10-16**: sama data „opłacone do” na dole widoku grobu (wariant B, schemat v14); przypomnienie
     — później aktualizacją, przed najwcześniejszą zapisaną datą;
  4. ~~[[ISSUE-044-family-wreaths]]~~ — **zamknięte 2026-10-17**: wieńce rodów przy portrecie, na drzewie i w trybie prezentacji (schemat v15,
     [[ADR-021-clans-choice-at-the-person]]); kobieta po ślubie pół na pół (D14), ród odróżnia para wzór + kolor (D20 — decyzja autora na stopie #2);
     **wszystko, co zmienia bazę przed instalacją, jest zrobione**;
  5. ~~[[ISSUE-045-migration-map]]~~ — **zamknięte 2026-10-17**: mapa migracji w części „Mapa” zakładki Drzewo — świat z Natural Earth bez sieci, osoby
     w swoich miejscach w roku suwaka, przejazd przy przeprowadzce, kadr z Twoich gestów, tryb prezentacji na telewizor; bez nazw, bez śladu, awatary
     (decyzje autora D18, D25, D26);
  6. ~~[[ISSUE-046-icons]]~~ — **zamknięte 2026-10-18**: ikona aplikacji — znicz L1 autora (adaptacyjna z jednobarwną); w aplikacji własny font ikon —
     9 ikon z arkusza DALL-E autora i znicz autora przerysowane do wektora, reszta Material Symbols Rounded 300 w dwóch tonach; ikona obok tekstu rośnie
     z tekstem (decyzje autora 1', 2–4); bez zmiany bazy;
  7. ~~[[ISSUE-047-grave-first-then-people]]~~ — **zamknięte 2026-10-18**: „Dodaj grób” otwiera okno „Nowy grób”, grób może być pusty; „Dodaj osobę” w grobie
     najpierw szuka — osoba bez grobu (np. z drzewa) dołącza jednym dotknięciem, osoba z grobem jest wyszarzona z powodem (D23); „Dodaj osobę” w Osobach;
     bez zmiany bazy;
  8. ~~[[ISSUE-048-portrait-photos]]~~ — **zamknięte 2026-10-19**: portret → „Zdjęcie profilowe” (zmiana profilowego, „Obejrzyj zdjęcie”, „Dodaj zdjęcia”),
     okrąg z inicjałami z plakietką, zapis od razu z widoku (D24), nowy ekran „Zdjęcia w aplikacji” (wchłonięta [[ISSUE-026-link-existing-photo-to-person]]);
     bez zmiany bazy;
  9. ~~[[ISSUE-049-tree-levels-and-zoom]]~~ — **zamknięte 2026-10-19**: poziomy według związków („Linia krwi”, „Przez 1 związek”…) niezależne od przybliżania;
     poziom na prostych + / − w rogu drzewa i na listwie trybu prezentacji, przycisków przybliżania nie ma (D58 — decyzja autora na stopie #2); oddalanie do
     całego poziomu, także na telewizorze; bez zmiany bazy;
  10. [[ISSUE-050-next-event]] — „Następne” obok ▶ na drzewie i mapie: rok i co się w nim stało;

     pozycje 7–10 — **przegląd przepływu przez autora 2026-10-18 w `/pm`** (7 punktów, podział na 4 pozycje — `pm`, autor: *„Do twojej decyzji ile tych
     zadań”*); wszystkie z ekranem (`ui` → `planning`), prawdopodobnie bez zmiany bazy, a **przed instalacją**, bo w trakcie wyjazdu aktualizacji nie ma.
     Gdy zabraknie czasu, `pm` pyta autora, co odpada, zanim cokolwiek odpadnie;
  11. [[NT-007-hand-over-note]] (warunek obudzenia spełniony: kopia jest i jest eksportem) i [[ISSUE-032-mvp-install]] — audyt, małe poprawki „przed
     instalacją”, lista A *Hand checks*, instalacja ze sklepu.

  **Zasady terminu:** przed instalacją wszystko, co zmienia bazę; widoki bez zmiany bazy (5, 6) mogą przyjść później jako aktualizacja ze sklepu; **w trakcie
  wyjazdu żadnych aktualizacji** — dlatego 7–10, potrzebne na wyjeździe, idą przed instalacją. Wszystkie US [[EPIC-001-zabezpiecz-i-przepisz]] i [[EPIC-003-zrozumienie]] zamknięte (EPIC-i zostają `draft` do instalacji —
  ich NFR i rzeczy w ręce sprawdza [[ISSUE-032-mvp-install]]).
- **Agent `architect` — nie teraz** (retro 4, R7): sygnał „pierwszy ADR zastąpiony” ([[ADR-018-export-is-the-backup]]) rozliczony; nowy warunek w `CLAUDE.md` →
  *Na sygnał*.

  Specyfikacja: [[drzewo]] v1.25, [[osoba]] v2.9, [[wpis-osoby]] v6, [[wieniec]] v1.2, [[zamieszkanie]] v1.4, [[mapa-migracji]] v1.4, [[grob]] v9.1,
  [[cmentarz]] v8, [[osoby]] v3.1, [[rodzina]] v2.2, [[zdjecia-osoby]] v1.6, [[zdjecie]] v1.7, [[kadr-profilowego]] v1.3, [[zdjecia-w-aplikacji]] v1.2,
  [[style-b]] v1.46.
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
  - **[[ISSUE-051-wedding-changes-wreath-and-surname]]** (`draft`, z `/pm` 2026-10-19) — ślub i koniec związku zmieniają wieniec (przed ślubem swój ród,
    po ślubie pół na pół, po rozwodzie znowu swój — odwraca [[wieniec]] B7) i nazwisko (pytanie przy ślubie i przy końcu związku, na suwaku nazwisko z
    danego roku); bez zmiany bazy. Rekomendacja `pm`: pierwsza aktualizacja po instalacji — **miejsce w kolejce czeka na autora** (⚠️ OPEN w pozycji);
  - **opowieść rodziny na drzewie** — pomysł autora ze stopu #2 ISSUE-037 (c) w [[2026-10-14-opowiesc-rodziny-i-wieniec]] (INBOX): najpierw prototyp `ui`
    w trybie discovery, potem pozycje. **Po instalacji MVP** (decyzja autora 2026-10-14). Wieniec (d) przeszedł 2026-10-16 do kolejki jako
    [[ISSUE-044-family-wreaths]] (zamknięte 2026-10-17); „następne zdarzenie” z c) — 2026-10-18 jako [[ISSUE-050-next-event]]; animacje i zbliżenia zostają;
  - ~~[[ISSUE-026-link-existing-photo-to-person]]~~ — **wchłonięta 2026-10-18 przez [[ISSUE-048-portrait-photos]]** (AC-4, AC-5 tam) — zbudowane 2026-10-19;
  - **usuwanie pustego grobu i pochówku** — w aplikacji nie ma usuwania grobów, osób ani pochówków (brief G7/C5). Od [[ISSUE-047-grave-first-then-people]]
    pusty grób z pomyłki zostaje na liście, a osoby z grobem nie da się dodać do drugiego (napis symboliczny). Kandydat na małą pozycję, gdy któreś zacznie
    przeszkadzać przy prawdziwych danych ([[cmentarz]] D38 *Obali* 2, [[grob]] D23 *Obali*);
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
    `makieta-042.html` i jej zrzut, `chr042\`, `emu041\`, wiadomości commitów — do kosza (także prompty `dalle-prompts-046.md` — [[ISSUE-046-icons]] zamknięte). Z sesji
    ISSUE-042 (`574c5666-…\scratchpad\`): `dl\` i `src\` — pobrane pliki GeoNames i Natural Earth (ok. 1 GB, dane publiczne; potrzebne tylko do
    ponownej budowy listy miejsc — README `grobing-code` → *Lista miejsc*), `emu042\` (zrzuty, kopia `files/` sprzed pozycji z `Grobing_Restore` —
    **wymyślone dane** i cmentarz dodany poza agentem — oraz APK odniesienia), `ui042\`, `tools\`, logi testów — do kosza. Z sesji ISSUE-043
    (`6983a70d-…\scratchpad\`): `emu043\` (zrzuty `01`–`21`, kopia danych `Grobing_Restore` sprzed pozycji i kopie bazy do liczenia — **wymyślone dane** i
    cmentarz dodany poza agentem), `fonts043\` i skrypty pomiaru przeglądu `ui`, `ui.py`, `counts.py`, logi testów — do kosza. Z sesji ISSUE-044:
    `2aa5d062-…\scratchpad\` (prototyp `wience-044.html`, panele 1–6) — do kosza; `3c71c787-…\scratchpad\` — **`src044\` zachowaj**: 19 oryginałów z DALL-E
    nazwanych kluczami wzorów (`<klucz>.png`), czyli dokładnie wejście do przebudowy wzorów (README `grobing-code` → *Wieńce*; te same obrazy leżą w
    Pobranych pod nazwami z ChatGPT) — przenieś je w swoje stałe miejsce; reszta do kosza: prototyp `wience-044-b.html` i jego obrazy, zrzuty `emu044\`
    (wymyślone dane), APK odniesienia `base-043.apk`, logi klatek i testów, skrypty. Z sesji ISSUE-046 (`1f978d57-…\scratchpad\`): makieta `makieta-046\`,
    zrzuty `emu046\` (wymyślone osoby, demo i jeden wpis autora), `stan-przed-046.tar` (dane pokazu — zwyczajne nazwiska, kopia jest w `_pokaz`) i
    `stan-po-046.tar` (stan sprzed pokazu z wpisami autora), `dl-symbols\` (fonty Google — wejście do przebudowy fontu, do pobrania z README), `fonttest\`,
    `review046\`, `lib-before-046\` (kopia `lib/` sprzed podmiany), `chr*\`, logi i skrypty — do kosza; poza katalogiem sesji `%TEMP%\gsonda`, `%TEMP%\gcmp`
    i `%TEMP%\gvenv` (środowisko Pythona z fontTools i potracer) — do kosza. **`C:\Programowanie\Grobing\_ikony-dalle\` zachowaj** (poza repo): arkusz,
    `L1-znicz.png`, `Z-znicz.png`, `Z-znicz-pelny.png` to wejście do przebudowy fontu i ikony aplikacji (README `grobing-code` → *Ikony*), a
    `sklep-ikona-512.png` idzie do Play Console; `L2-drzewo.png` i `P-pinezka.png` — niepotrzebne;
  - **katalog sesji ISSUE-047** (`%TEMP%\claude\c--Programowanie-Grobing-grobing-agents\cce9fe30-…\scratchpad\`): makieta `makieta-047.html` i `makieta-047.png`,
    `emu047\` — zrzuty `01`–`20` (na 05, 08, 09 i 17a jest Twój wpis z emulatora), kopia demo sprzed pozycji `stan-przed-047.tar` + `stan-przed-047-base.apk`
    (już wgrana z powrotem), `chr047\` (profil Chrome bez okna), skrypty `*.py` — wszystko do kosza;
  - **katalog sesji ISSUE-048** (`%TEMP%\claude\c--Programowanie-Grobing-grobing-agents\92e37203-…\scratchpad\`): makieta `makieta-048.html` i jej zrzuty
    `shots048\`, `fotki.html` i `fotki048\` (wymyślone rysunki — zdjęcia testowe; z galerii emulatora już usunięte), `emu048\` — zrzuty `01`–`19` (na 09 i 10
    jest Twój wpis z emulatora) i kopia demo sprzed pozycji `stan-przed-048.tar` + `stan-przed-048-base.apk` (już wgrana z powrotem), `chr048\` (profil Chrome
    bez okna), `tools\` (skrypty), logi testów — wszystko do kosza;
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
  zastąpić. **Po ISSUE-044:** build profile v15 z wieńcami (`--split-per-abi`, **bez** `FRAME_LOG` — ostatnia instalacja po D20; do pomiaru klatek zbudować z
  `--dart-define=FRAME_LOG=true`), baza v15 nad danymi (migawki v11–v14 w `files/pre-update/`); **13 rodów u wymyślonych osób** (nazwy ASCII z wymyślonych
  rdzeni): ród Antoniego „Wymyslonowie” w kolorze Miedź, Marianna „Przykladowscy” (kłosy, rubin — założony przez autora na stopie #2), Wiktoria pół na pół.
  Wpisy autora (cmentarz i grób) nietknięte; tekst, gęstość i animacje domyślne. **2026-10-18 (pokaz dla znajomych, poza pozycją):** autor pokazał demo — oba
  stany są w `C:\Programowanie\Grobing\_pokaz\` (poza repo; README ze sposobem zamiany): **demo** (41 wymyślonych osób o zwyczajnych nazwiskach — nigdy do repo,
  build `demo-profile.apk`) i **sprzed demo** (stan opisany wyżej). **Po ISSUE-046:** `Grobing_Restore` ma z powrotem **demo** (build demo, stara ikona
  Fluttera; ikona Grobing dodana na ekran główny, „Themed icons” wyłączone); przed testami na nim — wgrać stan sprzed demo z `_pokaz`, nigdy `pm clear` bez
  zapisanego tar. `Medium_Phone` — release HEAD 6f4f2fb nad danymi testowymi autora (v12 → v15, 2026-10-18, dane zachowane). **Po ISSUE-047:**
  `Grobing_Restore` — z powrotem **demo** (APK i dane zapisane przed pozycją, razem z Twoimi zmianami z 2026-10-18: 41 osób); na czas pozycji był tam stan
  sprzed demo z `_pokaz` z buildem ISSUE-047 — wpisy z testów i ze stopu #2 przepadły razem z nim, plik w `_pokaz` bez zmian. **Po ISSUE-048:**
  `Grobing_Restore` — z powrotem **demo** (41 osób, APK i dane zapisane przed pozycją); na czas pozycji stan sprzed demo z `_pokaz` z buildem ISSUE-048, a w
  nim zmiany z przejścia i ze stopu #2 (nowe profilowe Mateusza, zdjęcia Zofii i Ignacego) — przepadły razem z nim, plik w `_pokaz` bez zmian. Tekst i gęstość
  domyślne. **Emulator zawiesił się raz** (wątki QEMU bez odpowiedzi): po buildzie zostało ok. 0,9 GB wolnej pamięci — po każdym `flutter build` zatrzymać demony
  Gradle (`android\gradlew --stop`), zanim emulator dostanie zadania.
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
- Zamknięte pozycje od ostatniego retro: **9** (ostatnie retro: [[2026-10-16-retro-04]]). Co **10** → retro + pytanie o 3–5
  nośnych faktów (Meta-dec. 3g, 3h SC-16, A3). Licznik żyje **tylko tutaj**; podbija go `docs` przy zamknięciu, a zeruje go retro.
- Do retro (zebrane po drodze, bez decyzji):
  - Poprzednią listę rozliczyło [[2026-10-16-retro-04]] → *The "Do retro" list*.
  - **Nazwa opcji opisana kierunkiem, nie źródłem rysunku** ([[ISSUE-046-icons]] → *Stop #2 — runda 1*): opcja B na stopie #1 nazwana „Twój kierunek
    narysowany kreską” — autor wybrał ją, myśląc o swoich ikonach z arkusza; w aplikacji B to ikony Google w jego kolorach. Wyszło dopiero na emulatorze po
    całej budowie (dwie rundy `dev`). Kandydat: przy wyborze wariantu nazwa mówi, **skąd jest to, co autor zobaczy** („ikony Google w Twoich kolorach” vs
    „Twoje obrazki z arkusza”), a stop #1 pokazuje telefon z tym wariantem obok jego źródła.
  - **Wiersz macierzy ISSUE-044 bez Issue(s)/Issue Status** — `TRACEABILITY.md`, wiersz „wieńce rodzin”: pozycja zamknięta, kolumny `planning` puste
    (zauważone przy planie ISSUE-046). Do uzupełnienia przez `planning`/`docs` przy najbliższej okazji.
  - **Wycinanie ikon przez Fluttera gubi glify Material Symbols z podmianą wzdłuż FILL** ([[ISSUE-046-icons]] → *Probes*) — sonda przed masową podmianą
    złapała to, zanim poszło do przodu; wiedza w README `grobing-code` → *Ikony*.
  - **Zapis od razu z widoku → wyścig dwóch szkiców** ([[ISSUE-048-portrait-photos]] → *Verification*, przegląd `ui` MAJOR): przejście `dev` na emulatorze i testy
    były zielone, a drugie dotknięcie okręgu w trakcie przygotowania zdjęć otwierało drugi szkic, którego zapis całej listy zdejmował zdjęcia pierwszego. Ten
    sam mechanizm co D25 (otwarta poprawa). Kandydat: przy każdym zapisie „od razu” w specyfikacji stan „w toku” i pytanie o drugie wejście, zanim przyjdzie
    przegląd.
  - **„ok” na stopie #2 bez śladu dla jednego kroku** — po [[ISSUE-045-migration-map]] (krok 2) znów w [[ISSUE-048-portrait-photos]] (krok 3); pozostałe kroki ze
    śladem. Zapisane jak „pomiń” → lista B.
  - **Zmiana sterowania na stopie #2 po „tak” na klikalnej makiecie** ([[ISSUE-049-tree-levels-and-zoom]] → *Stop #2 — runda 1*): P2 (etykieta „Linia krwi ▾” z
    listą) przyjęte na stopie #1; zbudowane, na emulatorze autor zamienił je na proste + / − i usunął przyciski przybliżania — runda `ui`, `dev`, `qa`.
    Specyfikacja omijała + / −, bo autor nazwał nieestetycznym „− Poziom 2 +” ([[SPIKE-004-mvp-flow-prototype]] D25), a chodziło mu chyba o napis, nie o
    przyciski. Kandydat: gdy wcześniejsze odrzucenie jest powodem wyboru, jedno pytanie, co dokładnie było nie tak, zanim wypadnie cała rodzina wariantów.
  - **Pomiar w specyfikacji z innego ekranu niż zapisany** (przegląd `ui` rundy 2 [[ISSUE-049-tree-levels-and-zoom]]): *States* mówiły „emulator 360 dp” przy
    zrzucie z ekranu 411 dp (bez `wm size` / `wm density`). Kandydat: przy pomiarze „200% na 360 dp” zapis podaje `wm size` i gęstość z tej samej chwili.

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

- 2026-10-19 — [[ISSUE-049-tree-levels-and-zoom]] zamknięte. **Poziomy pokrewieństwa niezależne od przybliżania** (trzecia z 4 pozycji z przeglądu
  przepływu przez autora):
  - stop #1 na klikalnej makiecie — *„tak”*: **M2** (na „Linii krwi” krewni z mężami, żonami i partnerami, ich rodziny poziom wyżej — D50, zastępuje D2), **N2**
    („Linia krwi”, „Przez 1 związek”, „Przez 2 związki”), **K1** (po zmianie poziomu skala i środek zostają), **T2** (poziom i dwa palce także w trybie
    prezentacji, zmienia D16); przybliżanie to sam widok, aż do całego poziomu na środku (D51, zastępuje S2); przy bardzo małym drzewie dotknięcie przybliża
    (D52); „Połącz dwie osoby” podnosi poziom, nie obniża go;
  - stop #2 runda 1 — **zmiana autora (D58)**: zamiast etykiety z listą (P2) proste **+ / −** poziomu w rogu drzewa i na listwie; przycisków przybliżania nie ma —
    oddalanie tylko dwoma palcami (wyjątek od SC 2.5.1, [[style-b]] v1.46); pigułka poziomu także na telewizorze; runda 2 *„ok”* — kroki 1–3 ze śladem w logcat;
  - [[drzewo]] v1.25 (D50–D58), [[style-b]] v1.44–v1.46; wymyślona rodzina +10 osób (117, od „Ja” 91 → 113 → 116); **bez zmiany bazy** (v15);
  - przegląd `ui`: runda 1 — 3 MINOR, runda 2 — 7 MINOR (cel 48 dp na listwie, nieaktywny bez obrysu, szerokość pigułki, pigułka przy roku), poprawione przed
    stopem. `Grobing_Restore` — demo z powrotem (stan z pozycji zapisany w katalogu sesji).

  Lista B w [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 964 zielone. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 8 → 9.

- 2026-10-19 — [[ISSUE-048-portrait-photos]] zamknięte. **Portret jako miejsce na zdjęcia** (druga z 4 pozycji z przeglądu przepływu przez autora; wchłonięta
  [[ISSUE-026-link-existing-photo-to-person]]):
  - stop #1 na klikalnej makiecie — *„tak”*: **P2** — portret otwiera „Zdjęcie profilowe” jak „Zdjęcie w tle” (obecne profilowe, „Obejrzyj zdjęcie”, siatka,
    „Dodaj zdjęcia”); P1 (arkusz z działaniami) odrzucony; AC-4, AC-5 zostały; okrąg z inicjałami z plakietką prowadzi do dodania zdjęcia (D20 *Obali* trafione);
  - **zapis od razu z widoku** dla profilowego, kadru i dodanych zdjęć (D24), także „Dodaj zdjęcie” w pustej sekcji; poprawa tej osoby w stosie → wejścia
    zdjęć wracają do niej (D25, ochrona przed nadpisaniem — także tło); nowy ekran **„Zdjęcia w aplikacji”** — zdjęcia innych osób według osób, „Najbliżsi”,
    szukanie, zaznaczenie kilku, jeden plik i nowe łącze; [[osoba]] v2.9, [[zdjecia-osoby]] v1.6, [[zdjecie]] v1.7, [[kadr-profilowego]] v1.3,
    [[zdjecia-w-aplikacji]] v1.2, [[style-b]] v1.43 (wyjątek „wybór zdjęć w widoku”); **bez zmiany bazy** (v15);
  - przegląd `ui`: 1 MAJOR (drugi szkic w trakcie zapisu zdejmował zdjęcia — stan „w toku”) i 4 MINOR poprawione przed stopem, „z d.” poza zakresem;
    stop #2 *„ok”* — kroki 1–2 ze śladem, krok 3 bez śladu.

  Lista A i B w [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 956 zielonych. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 7 → 8.

- 2026-10-18 — [[ISSUE-047-grave-first-then-people]] zamknięte. **Najpierw grób, potem osoby** (pierwsza z 4 pozycji z przeglądu przepływu przez autora w `/pm`;
  [[ISSUE-048-portrait-photos]], [[ISSUE-049-tree-levels-and-zoom]], [[ISSUE-050-next-event]] rozpisane tego samego dnia, ISSUE-026 wchłonięta przez ISSUE-048):
  - stop #1 na makiecie — *„Tak”*: okno „Nowy grób” (to samo co „Popraw grób”), pusty grób, wybór „Kto leży w tym grobie?” („Bez grobu” do wyboru, „W grobach”
    wyszarzone z powodem — D23, bo pochówku nie da się cofnąć), „Dodaj osobę” w Osobach z imieniem z szukania; koszt: nowy grób z pierwszą osobą 1 → 4 dotknięcia;
  - decyzja „Grób powstaje z pierwszą osobą” obalona (*Obali* trafione); [[cmentarz]] v8 (D38), [[grob]] v9.1 (D22–D26), [[osoby]] v3.1, [[wpis-osoby]] v6 (tryb
    „nowa osoba”), [[rodzina]] v2.2; **bez zmiany bazy** (`burials` to osobna tabela);
  - przegląd `ui`: 1 MAJOR (pusty tytuł arkusza grobu bez nazwy i osób, z pinezką) i 2 MINOR — poprawione przed stopem; stop #2 *„Ok”* ze śladem na urządzeniu.

  Lista A i B w [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 946 zielonych. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 6 → 7.

- 2026-10-18 — [[ISSUE-046-icons]] zamknięte. **Ikony** (autor: obecne „wyglądają tak mało ciekawie”):
  - makieta A · B · C i ikony aplikacji; kierunek autora — arkusz DALL-E (bursztyn, dwa tony, charakter); stop #1: B, rośnie z tekstem, drzewo liściaste,
    ikona aplikacji **L1** (znicz); na stopie #2 autor zobaczył B na emulatorze i wskazał, że chciał **swoje rysunki** (decyzja 1') — opis opcji był myląco nazwany
    (*Do retro*);
  - sonda: wycinanie ikon przez Fluttera gubiło glify Material Symbols (`group`, `settings` puste) → **własny font ikon** (`assets/fonts/grobing-symbols.ttf`,
    `tool/icons/build_symbols.py`): Material Symbols Rounded 300 w dwóch tonach, **9 ikon z arkusza autora** i **znicz autora** (logo, przyciski, pinezki,
    drzewo) przerysowane do wektora; bez nowej zależności, bez zmiany bazy;
  - ikona aplikacji adaptacyjna z warstwą jednobarwną (motywy Androida 13), ikona 512 do sklepu poza repo; przeglądy `ui` (trzy): 3 MAJOR (ikona w `WidgetSpan`
    skalowana dwa razy, znicz w ikonie aplikacji poniżej 48 dp, dwie grubości kreski) i MINOR — poprawione lub przyjęte; [[style-b]] v1.37 → v1.42.

  Lista B w [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 936 zielonych. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 5 → 6.

- 2026-10-17 — [[ISSUE-045-migration-map]] zamknięte. **Mapa migracji** (cel autora „na wyjazd” — pokaz rodzinie na telewizorze):
  - stop #1 na makiecie: **W2 · K2 · O3 · D2 · R4** — przełącznik „Drzewo | Mapa”, bez cmentarzy, kraj w punkcie nazwy bez obszaru, droga tylko w ruchu,
    kadr tylko z Twoich gestów (O3 i R4 — warianty autora); [[mapa-migracji]] v1.1;
  - mapa świata wbudowana (Natural Earth, 182 kraje, 508 KB), bez sieci; **bez zmiany bazy** (schemat v15); skupienia miejsc z przybliżeniem; ląd rysowany
    do obrazu, gdy kamera stoi — klatki w zakresie drzewa z wieńcami;
  - decyzje autora w trakcie: **D18** — bez nazw krajów i miejsc („wystarczą awatary i kontury krajów”), **D25** — przeprowadzka bez śladu, **D26** —
    zdjęcie profilowe także u „ja” na mapie (drzewo i lista przy „Ja”); imiona w rozsunięciu i linia karty zostają (stop #2);
  - przeglądy `ui` (dwa): 1 MAJOR (przejazd ucinany co rok) i 13 MINOR — poprawione; testy `qa` znalazły przełącznik pod „Zakończ prezentację” przy 200%
    (D24); [[drzewo]] v1.22, [[osoba]] v2.8, [[zamieszkanie]] v1.4, [[style-b]] v1.36; przycisk „Wymyślone miejsca zamieszkania i portrety” w „Stanie danych”.

  Lista B w [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 923 zielonych. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 4 → 5.

- 2026-10-17 — [[ISSUE-044-family-wreaths]] zamknięte. **Wieńce rodów:**
  - discovery `ui` (dwa prototypy, 20 decyzji w [[wieniec]]): K2 — dwie gałązki otwarte u góry, 19 wzorów z DALL-E od autora (bez maku), paleta 12
    kolorów z cieniowaniem C3, cały wieniec po ojcu, ród wybierany raz u szczytu linii, **kobieta po ślubie pół panieński, pół po mężu** (D14 — pomysł
    autora), widok osoby, drzewo i telewizor;
  - stop #1 *„tak”* — **droga R**: obrazy w `grobing-code/assets/wreaths/`, wąski wyjątek w `.gitignore` i strażniku (tylko szary PNG z przezroczystością
    640 × 640); schemat **v15** (`clans`, `persons.clan_id`, `persons.no_wreath`, [[ADR-021-clans-choice-at-the-person]]) — zapisany tylko wybór, wieniec
    liczony z drzewa;
  - przejście `dev`: migracja nad danymi bez zmian liczb, przerwana migracja zostawiła v14 całe; klatki drzewa z wieńcami nie gorsze od buildu
    odniesienia; 200% na 360 dp wymusiło układ dużego tekstu (D19); przegląd `ui`: 1 MAJOR i 4 MINOR — poprawione, 10 odstępstw przyjętych ([[wieniec]] v1.1);
  - **na stopie #2 decyzja autora D20:** ród odróżnia para wzór + kolor — „też: …” tylko dla tej samej pary ([[wieniec]] v1.2).

  Lista A i B w [[ISSUE-032-mvp-install]] → *Hand checks*. Testy: 891 zielonych (strażnik 164). Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik
  retro: 3 → 4.

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
