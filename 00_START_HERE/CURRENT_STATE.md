---
title: "Grobing — Current State"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-12
---

# Grobing — Current State

> Żywy obraz tego, gdzie produkt jest teraz. Krótszy i bardziej zmienny niż `SESSION_STATE.md`.

> 📍 **Ten plik jest jedynym licznikiem stanu produktu** — etap dojrzałości, co w toku, licznik do
> retro, sprawy zaparkowane. **Żaden inny plik ich nie powtarza; wszystkie linkują tutaj.** Wolisz
> *„patrz `backlog/issues/`"* niż *„12 zadań"* — wskaźnik się nie zestarzeje.

## Maturity stage
MVP — od startu, cały produkt (Meta-decyzja 4).

## In progress
- **Po [[2026-10-08-retro-02]] (R1–R10, decyzja autora 2026-10-08):**
  1. ~~[[ISSUE-020-content-guard]]~~ — zamknięte 2026-10-08 (*Recently done*);
  2. ~~[[ISSUE-021-small-fixes-after-retro-2]]~~ — zamknięte 2026-10-08 (*Recently done*);
  3. ~~US-004 przed rozmową z babcią~~ — **rozstrzygnięte przez autora 2026-10-08 w `/pm`:** budujemy produkt
     gotowy do instalacji na telefonie (MVP = brief §5, M1–M11). **Wszystkie prawdziwe dane rodziny trafią do
     aplikacji dopiero po instalacji**, a do tego czasu autor ocenia aplikację na wymyślonych danych, żeby mieć
     „feeling”. Rozmowa z babcią (~2026-11-02) jest więc na kartce, a odpowiedzi trafią do aplikacji po instalacji.
     US-004 nie ma terminu;
  4. ~~[[SPIKE-004-mvp-flow-prototype]]~~ — zamknięty 2026-10-08 (*Recently done*).
- **Droga do instalacji MVP** — propozycja łańcucha przy zamknięciu SPIKE-004 (autor może zmienić kolejność):
  1. ~~[[ISSUE-022-app-skeleton-tabs-people-settings]]~~ — zamknięte 2026-10-08 (*Recently done*);
  2. ~~[[ISSUE-025-gender-kinship-together-since]]~~ — zamknięte 2026-10-08 (*Recently done*);
  3. ~~[[ISSUE-024-person-view]]~~ — zamknięte 2026-10-12 (*Recently done*);
  4. ~~[[ISSUE-023-poland-map-r1-cemetery-photo]]~~ — zamknięte 2026-10-12 (*Recently done*);
  5. ~~[[US-007-mapa-cmentarza]]~~ — zamknięta 2026-10-12 (~~ISSUE-027~~, ~~ISSUE-028~~; *Recently done*);
  6. ~~[[US-008-pinezka-na-miejscu]]~~ — zamknięta 2026-10-12 (~~ISSUE-029~~; *Recently done*). **Teren czeka:** build release na
     telefonie przed zaduszkami (~2026-11-02) → *Parked* (cel autora z `/pm`: jedna wizyta da pomiar i sprawdzenie AC-1, AC-4).
     Kandydaci z [[cmentarz]] D29 i nachodzące znicze → [[ISSUE-030-sector-on-a-visit]] (`draft`, **czeka na wizytę** — D5, stop #1);
  7. **następna (po retro — licznik niżej): [[SPIKE-002-tree-on-a-phone]]** → drzewo, czas, „Połącz dwie osoby” ([[drzewo]], EPIC-003) — od ISSUE-024 także **słownik nazw
     złożonych i dawne AC-6** („ciotka”, „stryj”, „siostra cioteczna babci żony”) i „Pokaż w drzewie” w widoku osoby (SPIKE-002 →
     *Input from ISSUE-024*);
  8. [[US-006-eksport-dla-rodziny]] i [[NT-007-hand-over-note]];
  → **instalacja MVP na telefonie** (build release) → prawdziwe dane ([[NT-002-transcribe-the-notes]]).

  **EPIC-001:** [[US-004-fakt-od-babci]] **wycofana** (SPIKE-004 D28 — bez źródeł; wiedza od babci przez zwykłą
  poprawę); [[US-006-eksport-dla-rodziny]] `ready`.
- **[[SPIKE-001-map-source-offline]] zamknięty 2026-10-08** → [[ADR-003-map-source-offline]] `accepted`: mapa
  cmentarza to **plan schematyczny z OSM offline** + ortofotomapa GUGiK online + kwatery i pinezki autora.
- **Kolejność autora (2026-10-06, *„ok plan brzmi dobrze”*; ISSUE-015 dołożona
  na stopie #1 ISSUE-014, *„wygląda dobrze”*) — wyczerpana:**
  1. ~~[[ISSUE-014-home-map-of-poland]]~~ — zamknięte 2026-10-06;
  2. ~~[[ISSUE-015-add-cemetery-from-database]]~~ — zamknięte 2026-10-07;
  3. ~~[[ISSUE-012-transcribe-grave-screen]]~~ — zamknięte 2026-10-07;
  4. ~~[[US-005-zdjecia]]~~ — zamknięta 2026-10-07 (~~ISSUE-016~~, ~~ISSUE-017~~);
     ~~4a. [[ISSUE-018-profile-photo-crop]]~~ — zamknięte 2026-10-07;
  5. ~~[[US-003-przepisanie-rodziny]]~~ — zamknięta 2026-10-08 (~~ISSUE-019~~);
  6. ~~[[SPIKE-001-map-source-offline]]~~ — zamknięty 2026-10-08 (*Recently done*).
  
  **Każda pozycja z ekranem: `ui` → `planning`** (`autonomous-flow.md`). Wygląd: `05_DESIGN/brand/`
  (wytyczne v1.6 i referencje R1–R4 z kick-offu).
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
    testowe). Pliki o tej samej nazwie w kilku folderach mylą wyszukiwarkę okna przy odtworzeniu.
- **[[EPIC-002-wizyta]] gotowy do rozpisania na US** — pytanie „jak znaleźć grób bez pinezki” ma kierunek autora
  (2026-10-08): adres z wyszukiwarki zarządcy → kwatera zaznaczona według planu zarządcy → na miejscu plan offline i
  GPS → pinezka. Wejście do pierwszej US (mapa cmentarza): EPIC-002 → *Input from SPIKE-001*. Ekran: `ui` →
  makieta przed kodem; [[cmentarz]] D1 (zdjęcie nad listą) do zmiany.

## Backlog at a glance
- Zadania: *patrz `backlog/issues/`*.
- Spike'i: *patrz `backlog/spikes/`* — trzy niewiadome, na których stoi architektura.
- Poza kodem: *patrz `backlog/non-tech/`*.
- Odłożone: *patrz `backlog/deferred/`*.
- Wymagania: *patrz `03_REQUIREMENTS/`* (EPIC-i, US, FR, NFR); architektura i ADR-y: *patrz `04_ARCHITECTURE/`*.
- **Repo są publiczne na GitHubie** od 2026-10-07 (*Recently done*). Push idzie sam zaraz po commicie
  paczki (decyzja autora 2026-10-07); treść wychodzących zmian sprawdza strażnik treści ([[ISSUE-020-content-guard]]) przy każdym `git add`/`commit`.

## Retro / fact-confirmation counter
- Zamknięte pozycje od ostatniego retro: **10** (ostatnie retro: [[2026-10-08-retro-02]]) — **🔔 sygnał dla `pm`: retro i pytanie o
  3–5 nośnych faktów przed następną pozycją** (po ISSUE-029, 2026-10-12). Co **10** →
  retro + pytanie o 3–5 nośnych faktów (Meta-dec. 3g, 3h SC-16, A3). Licznik żyje **tylko tutaj**;
  podbija go `docs` przy zamknięciu, a zeruje go retro.
- Do retro (zebrane po drodze, bez decyzji):
  - **model zagrożenia przyjęty, a nie zapytany** ([[ISSUE-020-content-guard]] → *Decision at stop #2*): plan i retro 2
    zakładały, że nazwiska nie mogą trafić do rozmowy z agentem, więc listę miał pisać autor. Autor na stopie #2: chroni
    tylko publikację na GitHubie. Kosztowało to rundę i edycję reguły, którą klasyfikator zablokował agentowi.
    Kandydat: przy pozycjach o danych rodziny pytanie „przed czym chronimy?” na stopie #1, zanim plan je założy;
  - **trzecia instancja tego samego błędu semantyki** ([[ISSUE-021-small-fixes-after-retro-2]] → *Verification*, uwaga
    5): `Semantics` z `excludeSemantics` bez `onTap` — przycisk czytany, ale nienaciskany przez Switch Access i Voice
    Access (ISSUE-017 + dwa ekrany z ISSUE-021). Kandydat: test na źródłach albo punkt przeglądu `ui`;
  - **discovery na klikalnym prototypie zadziałał** ([[SPIKE-004-mvp-flow-prototype]]): 10 paneli w jednej sesji, 28
    decyzji, 4 nowe specyfikacje, a przed kodem wyszły: inny układ cmentarza, płeć, zdjęcie w tle, bez Grobonetu, bez
    źródeł. Kandydat: tryb „discovery” w skillu `ui` (druga instancja potrzebna przed frameworkiem);
  - **wymaganie z kick-offu obalone dopiero na ekranie** (źródła, brief §5a G3 → FR-001 → US-004): przez trzy dni stało
    w specyfikacjach i w `qa`, a autor odrzucił je, gdy zobaczył je na prototypie. Kandydat: wymagania z kick-offu,
    których autor nie widział na ekranie, pokazać na makiecie wcześnie;
  - **twardy stop „fakt o rodzinie bez źródła”** w `grobing-agents/.claude/rules/autonomous-flow.md` (*Hard stops*) jest po
    D28 nieaktualny. Proponowane brzmienie: „…ryzyko utraty danych rodziny, dane rodziny w repo, niespełnione AC, zmiana
    bez odbicia w vaulcie”. Agent nie zmienia listy twardych stopów sam — decyzja autora (skill `qa` już poprawiony);
  - **agent uruchomił `python -I -`** (czytanie skryptu z wejścia), choć pamięć sesji mówi „nigdy” — komenda zawisła i
    trzeba ją było zatrzymać; bez szkody dla plików;
  - **strażnik treści złapał przykład agenta** ([[ISSUE-022-app-skeleton-tabs-people-settings]] → *Verification*): zwykłe
    polskie nazwisko, użyte jako przykład w komentarzu i teście, trafiło na listę rdzeni. Strażnik zadziałał przed `git add`
    (suchy przebieg `qa`). Kandydat: przykłady tylko z rdzeni jawnie wymyślonych („Wymyśl-”, „Zmyśl-”, „Testow-”,
    „Przykład-”), nigdy z prawdziwych nazwisk, nawet popularnych;
  - **`python -I -` jeszcze dwa razy** ([[ISSUE-025-gender-kinship-together-since]]) — po zapisie w pamięci „nigdy”
    (SPIKE-001, dwa razy). Wola nie działa: token wraca z nawyku, raz jako „szablon” komendy, raz doklejony do łańcucha.
    Kandydat: hook `PreToolUse`, który odmawia komendy z `python -I -` (mechanizm zamiast pamięci, jak strażnik danych);
  - **discovery na klikalnym prototypie — druga instancja** ([[ISSUE-025-gender-kinship-together-since]], stop #1): autor
    odrzucił oba warianty z makiety (przełącznik albo same daty) i opisał trzeci kształt — związek, który „ewoluuje”,
    w kreatorze; po prototypie panel po panelu: *„C1 / P1 / Jest dobrze”*. Z SPIKE-004 to już dwie instancje — warunek dla
    trybu „discovery” w skillu `ui` spełniony (doc-growth: generalizacja z instancji). Przy okazji: decyzja z prototypu
    SPIKE-004 (pokrewieństwo w liście Osób, D19) odwrócona na stopie #1 — *„to jest funkcja łączenia osób w drzewie”*;
  - **przegląd `ui` zmienił decyzję zapisaną w specyfikacji z prototypu** (ISSUE-022, MAJOR: „Odtwórz z kopii” przez
    „Stan danych”): prototyp nie pokazał drugiego przycisku pod „Skonfiguruj kopię od nowa”. Na tę lukę prototypu odpowiedział
    przegląd zbudowanego ekranu.

  - **przegląd `ui` znalazł 4 MAJOR po zielonych testach i przejściu AC na emulatorze** ([[ISSUE-024-person-view]] → *Verification*):
    pierścień w akcencie przykryty przez okrąg w trzech miejscach, ucięta rola i łamane słowo przy tekście 200%, ramka zaznaczenia na
    krawędzi zdjęcia. `dev` nie sprawdzał tekstu 200% ani zdjęć w sepii. Kandydat: punkt „tekst 200% i zdjęcie w sepii” w przejściu AC
    przez `dev` (R5) przy każdym nowym ekranie;
  - **wybór z makiety odwrócony na stopie #2** (ISSUE-024): autor wybrał W2 („widok tylko pokazuje”), a przy tle na emulatorze chciał
    trzeciej drogi — dotknąć pasma i wybrać. Makieta pokazała W1 i W2 jako całości, a nie miejsce działania. Kandydat: przy pozycji
    z działaniem na ekranie pokazać na makiecie **gdzie się dotyka**, nie tylko co widać;
  - **„ok” na stopie #2 bez sprawdzenia na urządzeniu — autor przerwał sprawdzenie: „pomiń”** (ISSUE-024, krok 3 rundy 2). Pamięć mówi,
    że „ok” bez śladu agent sprawdza; tu autor zdecydował inaczej. Kandydat: zapytać, czy sprawdzanie „ok” na urządzeniu ma zostać.
  - **`dev` przypisał wolne klatki emulatorowi, a był to błąd wydajności ok. 600×** ([[ISSUE-023-poland-map-r1-cemetery-photo]] →
    *After `qa`* pkt 1): morze rysowane przez `Path.combine` co klatkę, ANR przy starcie. Złapał to dopiero ANR i pomiar `qa` (stara vs
    nowa mapa). Kandydat: przy nowej warstwie mapy albo dużych danych — test kosztu w przejściu AC, zanim padnie słowo „emulator”;
  - **`python -` jeszcze raz** (ISSUE-023, `qa`) — trzecia sesja z rzędu mimo pamięci „nigdy”; zawisło, bez szkody. Wzmacnia kandydata
    na hook `PreToolUse` wyżej;
  - **czwarta instancja błędu semantyki** (ISSUE-023): `Semantics` bez `container` zlał „Dodaj zdjęcie” z całym arkuszem — przycisk
    niedostępny dla Switch Access jako osobny. Złapane w przejściu AC (`uiautomator`). Przy okazji z ISSUE-024: węzeł „Dodaj zdjęcie
    osoby” w „Zdjęcie w tle” jest szerszy niż kafelek (ramka TalkBack). Kandydat: punkt „semantyka” w przejściu AC i w przeglądzie `ui`;
  - **skill `ui` w trybie przeglądu mówi „nic nie zapisujesz”**, a przeglądy zapisują przyjęte odstępstwa w specyfikacji (ISSUE-023:
    cmentarze v2.6, style-b v1.20, zdjecie v1.6; wcześniej v2.2, v1.4–v1.8, v1.17). Kandydat: wyrównać skill z praktyką. ISSUE-027:
    jeszcze raz (cmentarz v5.1, style-b v1.21);
  - **współrzędna z pamięci w planowaniu** ([[ISSUE-027-cemetery-map-plan-photo-states]] → *Dev report*, Found 1): sonda przed planem
    użyła punktu cmentarza testowego „z głowy” (ok. 80 m za krawędzią), więc *Prior art* zapisał błędny wniosek. Odwrócił go dopiero
    punkt z bazy aplikacji w `dev`. Globalne „cytuję źródło, nie pamięć” dotyczy też danych wejściowych sondy;
  - **pakiet zewnętrzny pisał lokalizację do logu** (ISSUE-027 F5): `flutter_map` wypisywał adres nieudanego kafelka (miejsce
    cmentarza) do logcat także w release — znalezione przypadkiem przy sprawdzaniu „ok” ze stopu #2. Kandydat: krok `qa` „logcat bez
    adresów i współrzędnych” przy każdej pozycji z siecią;
  - **piąta instancja błędu semantyki** (ISSUE-027 F4): węzeł „Pokaż listę grobów” bez `container` brał granice całego panelu razem
    z „Dodaj grób”. Wzmacnia kandydata „semantyka” w przejściu AC i w przeglądzie `ui`;
  - **Overpass ma limit zapytań na adres IP**, a emulator wychodzi przez adres PC (ISSUE-027): sondy z PC w tym samym czasie
    psuły pobieranie na emulatorze. Kandydat: zakaz sond z PC w czasie przejścia AC na emulatorze (zapisany w README);
  - **`adb input text` zgubił pierwszy znak hasła** (ISSUE-027, próbne odtworzenie): pierwsza próba „Złe hasło”. Kandydat do
    pamięci emulatora: dotknąć pola, odczekać, wpisać, policzyć kropki.
  - **wymaganie M1 bez ekranu przez cały MVP** ([[ISSUE-028-cemetery-sectors]] → *Do retro*): adres kwatery z brief §5 M1 miał kolumny od
    v1, ale żaden ekran go nie zapisywał — wyszło dopiero przy specyfikacji `ui` piątej pozycji drogi do MVP. Kandydat: przy rozpisywaniu
    EPIC-u porównać pola modelu danych z ekranami, które je zapisują;
  - **szósta instancja błędu dostępności dotyku** (ISSUE-028, MAJOR przeglądu): pigułka „Kwatery” w polu 48 dp przyjmowała dotyk tylko na
    40 dp i nie była przyciskiem dla czytnika — wzorzec `TapHandle`/`LayerSwitch` leżał w pliku obok. Wzmacnia kandydata „semantyka i cel
    dotyku” w przejściu AC `dev`;
  - **granica git złamana komendą „tylko do liczenia”** (ISSUE-028, `dev`): `git add -N .` i `git reset -q` — bez skutku, ale zakazane.
    Kandydat: hook, który odmawia komend git zmieniających indeks poza commitem `docs`;
  - **`python -` jeszcze trzy razy** (ISSUE-028, `dev` i `qa`) — razem już co najmniej siedem razy mimo pamięci „nigdy”; hook `PreToolUse`
    z tej listy coraz pilniejszy;
  - **stop #2 pominięty w całości** (ISSUE-028) — drugi raz z rzędu bez sprawdzenia w ręce (ISSUE-024 krok 3). Kandydat: zapytać, czy stop
    #2 przy pozycji z nowym gestem ma zostać obowiązkowy.
  - **`python -I -` ósmy raz** ([[ISSUE-029-pin-on-site-gps]], `qa`) — doklejone do komendy poprawiającej test; zawisło, zatrzymane od razu,
    bez skutku. Hook `PreToolUse` z tej listy — najpilniejszy kandydat retro 3;
  - **przegląd `ui` znalazł 3 MAJOR w stanach, których przejście AC `dev` nie pokazało** (ISSUE-029: brak kropki, brak mapy, „Zdjęcie” bez
    sieci) — przejście szło główną drogą. Kandydat: w przejściu AC `dev` stany z *States* specyfikacji, każdy ze zrzutem;
  - **testy widżetów z udawaną lokalizacją złapały dwa błędy, których nie złapał emulator** (◎ bez wyjścia przy „Przybliżonej”, kontroler
    animacji tworzony w `dispose()`) — emulator i testy uzupełniają się;
  - **`adb emu geo fix` bez wysokości i satelitów nie zmieniał pozycji** — kosztowało rundę; zapisane w README i w pamięci emulatora;
  - **stop #2: autor przeszedł inną drogą niż krok** (poprawił pinezkę zamiast postawić nową) — ten sam mechanizm, „ok” sprawdzone na
    urządzeniu; krok 2 (◎) znów bez śladu.

  Tematy z poprzedniego okresu rozliczyło [[2026-10-08-retro-02]] (R1–R10); wcześniejsze [[2026-10-06-retro-01]].

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
- 2026-10-12 — [[ISSUE-029-pin-on-site-gps]] zamknięte, a z nim **[[US-008-pinezka-na-miejscu]]** (werdykt US = werdykt jedynej pozycji:
  APPROVED, self-check, z uwagami). **Pinezkę da się postawić przy grobie:**
  - **„gdzie jestem”** na planie: niebieska kropka z kołem dokładności i „tu jesteś · ±5 m”, trzy stany przycisku (włącz i do kropki ·
    wyłącz · wróć do kropki), poza cmentarzem plakietka z odległością, zgoda „Przybliżona” bez kropki, odmowa i blokada z drogą przez
    ustawienia ([[cmentarz]] v7.1, 10, 10a);
  - **tryb „Pinezka grobu”** w wariancie **P2** (celownik, plan pod zniczem — decyzja autora na stopie #1): z grobu „Postaw pinezkę”, z
    arkusza „Popraw pinezkę”; z GPS plan idzie za kropką, przesunięcie albo dotknięcie robi pinezkę ręczną; słaby sygnał od 15 m
    (tymczasowo); bez internetu działa; po zapisie mapa z nowym zniczem;
  - **źródło pinezki = skąd pozycja** (D33): „Pinezka: GPS ±5 m · 12.10.2026”, „postawiona na planie · …”, „postawiona na zdjęciu z
    góry · …” w widoku grobu ([[grob]] v7);
  - **schemat v12:** data pinezki i źródło `plan` ([[data-model]]); migracja v11→v12 z testem, na Twoich danych testowych liczby bez
    zmian; próbne odtworzenie kopii v12 na drugim emulatorze — odcisk zgodny, pinezka z datą bez sieci;
  - **pozycja tylko z satelitów**, własnym kanałem, bez usług Google i bez nowej zależności, nigdy w logu
    ([[ADR-017-location-from-gnss-only]], [[NFR-005-dane-nie-opuszczaja-telefonu]]); komunikat [[osoba]] D9 przy „Pochówku” grobu bez
    pinezki wrócił.

  Przegląd `ui`: 0 BLOCKER, 3 MAJOR (karta „Stań przy grobie” bez kropki, zapis poprawki bez ruchu, zapis pinezki, której nie widać), 9
  MINOR — MAJOR i 7 MINOR poprawione przed stopem #2; testy `qa` znalazły dwa błędy aplikacji (◎ nie dawał się wyłączyć przy „Przybliżonej”,
  wyjątek przy zamknięciu trybu bez mapy) — poprawione. Stop #2 „ok”: poprawa pinezki sprawdzona na urządzeniu, trzy stany ◎ bez śladu.
  Werdykt `qa`: APPROVED (self-check, z uwagami). Testy: 692. Licznik retro: 9 → 10.

  **Dla autora:**
  - **teren** — build release na telefonie przed ~2026-11-02 (*Autor, poza sesją*) i krok przy grobach (*Parked*);
  - `Medium_Phone`: release v12 na Twoich danych testowych, kopia skonfigurowana od nowa — **nowe hasło testowe** (wymyślone, w tej
    sesji), pliki `grobing-klucz-029.age` i `grobing-kopia-029.age` w Pobranych; grób „Jozef” ma pinezkę z Twojej poprawki, „Grob
    wymyslonych” — bez pinezki;
  - `Grobing_Restore`: release v12 z danymi z kopii `-029`;
  - znana luka: przy tekście 200% na 360 × 640 dp plan w A jest bardzo niski, a „Kwatery” przykrywa plakietki (z ISSUE-027/028; *Poza tą
    kolejnością*);
  - prototyp `issue-029-pinezka.html`, zrzuty i kopie `-029` leżą poza repo (katalog tymczasowy sesji `8b388e89-…`) — do kosza.
- 2026-10-12 — [[US-008-pinezka-na-miejscu]] rozpisana na **[[ISSUE-029-pin-on-site-gps]]** (AC-1–AC-4: „gdzie jestem”, tryb D,
  „Postaw pinezkę”, „Popraw pinezkę”, data pinezki, offline) i **[[ISSUE-030-sector-on-a-visit]]** (`draft`: „Pokaż kwaterę”, lista
  grobów kwatery, nachodzące znicze — do decyzji autora) (`docs`, auto-flow po `pm`). Jedna pozycja, bo cztery AC dzieją się w
  jednym trybie mapy, który prototyp pokazał. Podział zaproponował łańcuch, więc na stopie #1 autor może go zmienić. To rozpisanie,
  nie zamknięta pozycja, więc licznik retro bez zmian. Rozpisanie wejdzie do commita paczki ISSUE-029.
- 2026-10-12 — [[ISSUE-028-cemetery-sectors]] zamknięte, a z nim **[[US-007-mapa-cmentarza]]** (werdykt US: APPROVED, niezależny
  przegląd, z uwagami). **Kwatery autora są na planie, a adres grobu da się wpisać:**
  - **tryb „Kwatery”** (pigułka na planie): lista kwater cmentarza → „Zaznacz kwaterę” → nazwa → rogi **celownikiem i „Dodaj róg”**
    (K1 — decyzja autora na stopie #1) → strefa na planie i na zdjęciu z góry, przerywana linia z nazwą. Dalej: zmiana nazwy,
    „Narysuj strefę od nowa”, „Usuń z planu” — adresy grobów zostają ([[cmentarz]] v6.1);
  - **adres zarządcy** w oknie „Popraw grób”: kwatera z chipów kwater cmentarza, rząd, miejsce; „Wpisz adres” pod brakiem adresu
    ([[grob]] v6). To była **luka M1**: kolumny istniały od v1, ale żaden ekran ich nie zapisywał (zmiana zakresu przyjęta na stopie #1);
  - **schemat v11:** kwatera jako rekord cmentarza, grób na nią wskazuje. Zmiana nazwy poprawia wszystkie adresy, „b” = „B”
    ([[ADR-016-sector-record-and-grave-link]]). Migracja v10→v11 z testem; próbne odtworzenie na drugim emulatorze — odcisk zgodny,
    strefa i adres widać bez sieci.

  Przegląd `ui`: 0 BLOCKER, 1 MAJOR (pigułka 40 dp zamiast 48), 9 MINOR — poprawione przed stopem #2. Stop #2: „pomiń” dla trzech
  kroków. Werdykt `qa`: APPROVED (self-check, z uwagami). Testy: 661. Licznik retro: 8 → 9.

  **Incydent:** `dev` uruchomił `git add -N .` i `git reset -q` — komendy zakazane; bez skutku, zgłoszone w sesji (*Do retro*).

  **Dla autora:**
  - **nieprzetestowane w ręce:** rysowanie K1 i okno adresu (stop #2 „pomiń”) — wracają przy pierwszym prawdziwym przepisywaniu
    adresów po instalacji MVP; do tego TalkBack i prawdziwy telefon;
  - `Medium_Phone`: release v11 na Twoich danych testowych, kopia skonfigurowana od nowa — **nowe hasło testowe** (wymyślone, w tej
    sesji), pliki `grobing-klucz-028.age` i `grobing-kopia-028.age` w Pobranych. Grób „Grob wymyslonych” ma adres „Kwatera B1 ·
    Rząd 4 · Miejsce 12”, a kwatera B1 — strefę;
  - `Grobing_Restore`: release v11 z danymi z tej kopii (build debug z ISSUE-027 odinstalowany);
  - znana luka: okno „Popraw grób” na małym ekranie przy tekście 200% i otwartej klawiaturze pokazuje naraz ok. dwie linie ([[grob]]
    *Open*);
  - prototyp `issue-028-kwatery.html`, zrzuty i kopie kopii leżą poza repo (katalog tymczasowy sesji `9f87c8cf-…`) — do kosza.
- 2026-10-12 — [[ISSUE-027-cemetery-map-plan-photo-states]] zamknięte (pierwsza z dwóch pozycji [[US-007-mapa-cmentarza]]). **Cmentarz
  jest mapą:**
  - **plan offline** z OpenStreetMap — obrys i alejki pobierane raz (przy zapisie cmentarza z punktem, przy zmianie punktu, przy
    starcie i powrocie do aplikacji, przy otwarciu cmentarza, „Pobierz teraz”), trzymane w bazie i w kopii
    ([[ADR-015-cemetery-plan-in-database]], schemat v10); **zdjęcie z góry GUGiK** tylko online, nic nie zostaje w telefonie;
  - **trzy stany** ([[cmentarz]] v5.1): A — sama mapa i pasek grobów, B — jeden grób ze znicza, C — lista; uchwyty działają
    dotknięciem; z „Pochówku” grób z pinezką → B, bez → lista; ✎ w pasku cmentarza;
  - **pięć zaślepek planu** (2a): pobieram · bez internetu · serwer nie odpowiada · brak w OSM · bez punktu — każda z faktem i drogą
    naprzód;
  - **W2 — miara [[NFR-004-czytelnosc-w-sloncu]] przyjęta** (decyzja autora na stopie #1): tekst czytany przy grobie ≥ 7:1;
  - **`INTERNET` w aplikacji**, wszystkie adresy w jednym pliku (`lib/net/hosts.dart`), tylko `https`, bez pamięci kafelków i bez
    adresów kafelków w logu ([[NFR-005-dane-nie-opuszczaja-telefonu]]); serwery planu bez `maps.mail.ru` (D4).

  Znalezione po drodze:
  - `around` w Overpass nie łapie środka dużego cmentarza → zapytanie łączy `is_in` i `around`;
  - kadr nie dopasowywał się przy tekście 200% → poprawione;
  - `flutter_map` domyślnie zapisuje kafelki na dysk i wypisuje ich adresy do logu → oba wyłączone.

  Przegląd `ui`: 0 BLOCKER, 2 MAJOR (uchwyt 28 dp, zaślepka bez grobów odsyłała do listy), 7 MINOR — poprawione przed stopem #2;
  odstępstwo „karty listy w kolorze tła” odrzucone (lista na tle, karty na powierzchni). Próbne odtworzenie na drugim emulatorze:
  odcisk zgodny, plan z kopii bez sieci. Stop #2 „ok” (kroki 1–2 sprawdzone na urządzeniu, krok 3 bez śladu). Werdykt `qa`: APPROVED
  (self-check, z uwagami). Testy: 632. Licznik retro: 7 → 8.

  **Dla autora:**
  - **po tej pozycji na Twoich danych plan jest bez zniczy** — pinezki postawisz od [[US-008-pinezka-na-miejscu]]; znicze widać tylko na
    wymyślonych pinezkach (przycisk „Wymyślone pinezki na planach” w „Stanie danych”, tylko debug);
  - `Medium_Phone`: release v10 na Twoich danych testowych, kopia skonfigurowana od nowa — **nowe hasło testowe** (wymyślone, w
    tej sesji), pliki `grobing-klucz-027.age` i `grobing-kopia-027.age` w Pobranych;
  - `Grobing_Restore`: **build debug** z danymi z tej kopii i wymyślonymi pinezkami (do kroku 3 stopu #2) — przed następnym próbnym
    odtworzeniem w release trzeba go odinstalować;
  - nieprzetestowane na żywo: stan „brak w OSM” (serwer był przeciążony), koszt rysowania na prawdziwym telefonie, TalkBack na
    planie, test w słońcu (W2) — przy instalacji MVP;
  - do decyzji, gdy zobaczysz plany swoich cmentarzy: grubość alejek (w OSM prawie wszystkie są „boczne”) i znicze sąsiednich
    grobów, które nachodzą na siebie ([[cmentarz]] → *Open*);
  - zrzuty, makieta (`issue-027-mapa-cmentarza.html`), kopie `-027` i wyciąg planu leżą poza repo (katalog tymczasowy sesji
    `1d9348ed-…`) — do kosza.
- 2026-10-12 — [[US-007-mapa-cmentarza]] rozpisana na [[ISSUE-027-cemetery-map-plan-photo-states]] (AC-1, AC-2, AC-3, AC-5:
  plan, zdjęcie z góry, stany ekranu, `INTERNET`) i [[ISSUE-028-cemetery-sectors]] (AC-4: kwatery autora) (`docs`, auto-flow
  po `pm`). Kwatery są osobno, bo ich zaznaczania prototyp nie pokazał, a zmieniają schemat. Ten podział zaproponował
  łańcuch, nie autor, więc na stopie #1 autor może go zmienić. To rozpisanie, nie zamknięta pozycja, więc licznik retro
  bez zmian. Rozpisanie wejdzie do commita paczki ISSUE-027.
- 2026-10-12 — [[ISSUE-023-poland-map-r1-cemetery-photo]] zamknięte. **Mapa Polski wygląda jak R1, a cmentarz ma zdjęcie:**
  - **mapa jak R1** ([[cmentarze]] v2.6, D29, D32): sąsiedzi w kolorze tła z granicami, Bałtyk i jeziora w kolorze wody, rzeki linią
    wody, granica Polski w kolorze tekstu pomocniczego, „Polska” (tylko przy najmniejszych przybliżeniach), 11 miast (+ Bydgoszcz,
    Katowice); podpisy mapy rosną z tekstem systemu najwyżej do 1,3×. Dane Natural Earth, bez sieci, `poland.json` ok. 300 KB, brzeg
    danych nigdy na ekranie; ten sam wygląd w podglądzie z bazy i w trybie wskazania;
  - **Polska na środku** (D30, D26 v2.6): bez arkusza na środku, na całą szerokość na każdym telefonie; przy otwarciu arkusza mapa
    płynnie podjeżdża (ok. 300 ms), przy zamknięciu wraca; na krótkim ekranie arkusz zasłania południe (reguła znicza);
  - **zdjęcie cmentarza w arkuszu** (6a, D33): miniatura 96 × 80 z lewej albo „Dodaj zdjęcie”, podgląd ze „Zmień” i „Usuń” jak przy
    nagrobku;
  - **schemat v9:** `media.cemetery_id` — [[ADR-014-cemetery-photo-on-media]]; migracja v8→v9 z testem, kopia v8 odtwarza się z
    cmentarzami bez zdjęć; próbne odtworzenie kopii v9 ze zdjęciem cmentarza na drugim emulatorze — odcisk zgodny.

  Znalezione po drodze: **błąd wydajności** — morze rysowane przez `Path.combine` co klatkę (2–3 s na klatkę, ANR przy starcie) →
  `evenOdd`, start 2,3 s; pułapka sieroty (zapis zdjęć osoby kasowałby zdjęcia cmentarzy) zamknięta przed kodem; arkusz liczył margines
  paska gestów dwa razy (od ISSUE-022) — poprawione. Dwa przeglądy `ui`: 0 BLOCKER, 2 MAJOR, 3 MINOR — wszystkie poprawione przed
  stopem #2. Stop #2 „ok”, sprawdzone na urządzeniu. Werdykt `qa`: APPROVED (self-check, z uwagami). Testy: 579. Licznik retro: 6 → 7.

  **Dla autora:**
  - na `Medium_Phone` kopia skonfigurowana od nowa — hasło testowe, do Pobranych (`grobing-klucz-023.age`, `grobing-kopia-023.age`,
    wymyślone dane); `Grobing_Restore` ma dane z tej kopii. Powązki mają wymyślone zdjęcie z Twojego kroku 3, Kuba Testowy — wymyślone
    profilowe i tło (z kroków agenta);
  - nieprzetestowane na żywo: wydajność mapy na słabym telefonie (pierwszy prawdziwy telefon przy MVP), TalkBack w arkuszu, telefon
    trzymany poziomo;
  - zrzuty, pliki Natural Earth (ok. 43 MB) i kopie kopii leżą poza repo (katalog tymczasowy sesji `a8d4bcfd-…`) — do kosza.
- 2026-10-12 — [[ISSUE-024-person-view]] zamknięte. **Osoba ma swój widok, a poprawa jest pod ✎:**
  - **widok osoby** ([[osoba]] v2.3): pasmo tła, portret na jego krawędzi, imię i lata, „kim była” w całości, **mini-drzewo** (rodzice,
    partnerzy — dwa związki po obu stronach, „razem” przerywaną linią — dzieci pod swoim związkiem, przewijanie w bok), **„Jak łączy
    się ze mną”** — łańcuch od „Ja” po imionach z relacją kroku (Ja → Mama Anna → Jej mama Maria; decyzja autora: nazwy złożone w
    drzewie), daty, **pochówek** → cmentarz z zaznaczonym grobem (do czasu mapy), zdjęcia;
  - **każde dotknięcie osoby otwiera widok**: karta w grobie, w Osobach, „Ja”, chipy i karta partnera w formularzu (uwaga autora
    *„najpierw profil, potem edycja”*); jedna poprawa osoby naraz w stosie;
  - **zdjęcia w widoku tylko do oglądania** (W2), z dwoma wyjątkami: „Dodaj zdjęcie” u osoby bez zdjęć (→ poprawa z arkuszem) i
    **pasmo tła → „Zdjęcie w tle”** — wybór albo nowe zdjęcie zapisuje tło od razu (decyzja autora na stopie #2, D21);
  - **schemat v8:** tło jako znacznik przy łączu osoba–zdjęcie, jedno na osobę — [[ADR-013-person-background-on-photo-link]]; migracja
    v7→v8 z testem, kopia v7 odtwarza się bez tła; próbne odtworzenie kopii v8 z tłem na drugim emulatorze — odcisk zgodny;
  - słownik nazw złożonych i dawne AC-6 → [[SPIKE-002-tree-on-a-phone]]; „połączyć z istniejącymi” → [[ISSUE-026-link-existing-photo-to-person]].

  Stop #1 w dwóch rundach (W2; łańcuch po imionach; sekcja „Zdjęcia” także bez zdjęć). Dwa przeglądy `ui`: 0 BLOCKER, 4 MAJOR,
  10 MINOR — wszystkie poprawione przed stopem #2. Stop #2: kroki 1–2 „ok”, krok 3 w drugiej rundzie (tło z pasma) „ok”, bez
  sprawdzenia na urządzeniu (autor: „pomiń”). Werdykt `qa`: APPROVED (self-check, z uwagami). Testy: 544. Licznik retro: 5 → 6.

  **Dla autora:**
  - na `Medium_Phone` kopia skonfigurowana od nowa — hasło testowe, do Pobranych (`grobing-klucz-024.age`, `grobing-kopia-024.age`,
    wymyślone dane); `Grobing_Restore` ma dane z tej kopii. Zofia Testowa ma wymyślone zdjęcie jako profilowe i tło (z kroków agenta);
  - nieprzetestowane na żywo: TalkBack w widoku osoby i ekran 360 dp (emulator ma 411 dp; układ dla 360 dp sprawdzają testy);
  - Ewa i Jozef z danych testowych nie mają płci (sprzed v7) — w łańcuchu „Rodzeństwo”, „Małżonek”; zaznacz ♀ ♂ w ich poprawie;
  - makieta (`issue-024-widok-osoby.html`), zrzuty i pliki kopii leżą poza repo (katalog tymczasowy sesji `8adf85b2-…`) — do kosza.
- 2026-10-08 — [[ISSUE-025-gender-kinship-together-since]] zamknięte. **Płeć wraca, związek to oś czasu, formularz bez
  źródeł:**
  - **płeć ♀ ♂ obok „Imiona”** w formularzu osoby i przy każdej nowej osobie, podpowiadana z imienia (wyjątki z pomiaru
    PESEL: Kuba, Barnaba…), zmiana jednym dotknięciem; zapisanej płci formularz sam nie zmienia ([[wpis-osoby]] v5.6);
  - **związek „ewoluuje”** (decyzja autora na stopie #1, zamiast przełącznika albo samych dat): **kreator w arkuszu od
    dołu** — z kim → „Razem” albo „Małżeństwo” (z datą albo „Nie znam daty”) → co było dalej (ślub · koniec · nic więcej);
    przy osobie **karta na każdy związek** z osią czasu („razem od 1980 · ślub 1985”) i ✎ do podsumowania, w którym każdą
    datę zmienia się osobno; **dzieci pod kartą związku** (C1) i **„Dodaj rodziców”** tym samym kreatorem („Kto jest
    mamą?”, „Kto jest tatą?” — P1); arkusz zawsze tej samej wysokości (uwaga autora na stopie #2) ([[rodzina]] v2.1);
  - nazwy ról z płci i ślubu: Matka, Ojciec, Mąż, Żona, Partner, Partnerka, Syn, Córka; bez płci — neutralne;
  - **bez źródeł w formularzu** (D28) — dane dalej zapisują się z domyślnym źródłem;
  - **schemat v7:** `persons.sex`, zdarzenie „Razem od”, ślub i koniec bez daty jako zdarzenia bez daty (`MARR Y` w GEDCOM 7)
    — [[ADR-012-person-sex-and-union-timeline]] (nie zastępuje ADR-011, sygnał dla `architect` się nie zapala); migracja
    v6→v7 z testem, kopia v6 odtwarza się w v7; próbne odtworzenie kopii v7 na drugim emulatorze — odcisk zgodny;
  - **zmiana wymagań** (decyzja autora, C1): [[FR-002-rodzina-jako-rekord]] i [[US-003-przepisanie-rodziny]] AC-1 — rodzina
    to jeden rekord, dzieci dodaje się przy parze; **bez pokrewieństwa w zakładce Osoby** ([[osoby]] v2.2); **słownik
    pokrewieństwa i AC-2 → [[ISSUE-024-person-view]]** (kanon zapisany w ISSUE-025 → *Prior art*).

  Stop #1 w trzech rundach (makieta wariantów → prototyp klikalny → „Jest dobrze”). Przegląd `ui`: 0 BLOCKER, 2 MAJOR, 7 MINOR —
  wszystkie poprawione przed stopem #2. Werdykt `qa`: APPROVED (self-check, z uwagami); stop #2 „ok” w dwóch rundach,
  sprawdzone na urządzeniu. Testy: 504. Licznik retro: 4 → 5.

  **Dla autora:**
  - **pytanie bez odpowiedzi:** czy kreator rodziców ma wpisywać płeć z odpowiedzi „mama”/„tata” osobie, która jej nie ma
    (tylko puste pole, nigdy nadpisanie)? Dziś nie wpisuje — chip mówi „Rodzic” ([[ADR-012-person-sex-and-union-timeline]]
    → *Follow-ups*). Tanie, jeśli tak;
  - podpowiadane nazwisko nowej osoby ma formę osoby z wpisu („Testowy” dla mamy) — znany punkt „do odczucia”
    ([[wpis-osoby]] *Open*);
  - nieprzetestowane na żywo: TalkBack i tekst 200% w kreatorze;
  - emulatory: na `Medium_Phone` kopia skonfigurowana od nowa z hasłem testowym do Pobranych (`grobing-klucz-025.age`,
    `grobing-kopia-025.age`, wymyślone dane); `Grobing_Restore` ma dane z tej kopii i Twoje usunięcia związków ze stopu #2;
  - makieta i prototyp leżą poza repo (katalog tymczasowy sesji: `issue-025-warianty.html`, `issue-025-prototyp.html`) — do
    kosza.
- 2026-10-08 — [[ISSUE-022-app-skeleton-tabs-people-settings]] zamknięte. **Aplikacja ma szkielet z prototypu:**
  - **dolny pasek Mapa · Osoby · Drzewo** na mapie, cmentarzu i grobie; mapa zawsze na dole stosu, więc „wstecz” z Osób
    wraca na mapę; zakładka z głębi stosu wraca do swojego ekranu głównego. Drzewo to na razie zapowiedź (D1 = A);
  - **zakładka Osoby:** „Ja” na górze, wszyscy A–Z po nazwisku (gdy brak — po rodowym), wyszukiwanie od początku słowa
    bez polskich znaków, karta → „Poprawa wpisu” do czasu widoku osoby (D2);
  - **koło zębate → ustawienia:** „Ja” (wybór „Która osoba to Ty?” — pierwszy zapis ustawienia „ja” z [[data-model]],
    bez zmiany schematu), kopia (ostatnia udana, „Zrób kopię teraz”, „Odtwórz z kopii” od razu do odtworzenia), notka
    przekazania (lista z NT-007), zaślepka eksportu, „Stan danych” piętro niżej, „O aplikacji”;
  - wyszukiwanie osób (brief §5a G5, Should) weszło do MVP decyzją autora na prototypie.

  `dev` znalazł na emulatorze, że po powrocie z wpisu wraca klawiatura (pole odzyskiwało fokus) — poprawione. Przegląd `ui`:
  0 BLOCKER, 1 MAJOR (droga odtworzenia), 13 MINOR — MAJOR i 9 MINOR poprawione przed stopem; specyfikacje [[osoby]] v2,
  [[ustawienia]] v2, [[cmentarze]] v2.5, [[style-b]] v1.17. Strażnik treści złapał przykładowe nazwiska w teście przed
  `git add` — zamienione na wymyślone. Próbne odtworzenie z „ja” na drugim emulatorze: odcisk zgodny. Werdykt `qa`:
  APPROVED (self-check, z uwagami); stop #2 „ok” (krok 3 sprawdzony na urządzeniu). Testy: 481. Licznik retro: 3 → 4.

  **Dla autora:**
  - na `Medium_Phone` kopia skonfigurowana od nowa — hasło testowe, do Pobranych (`grobing-klucz-022.age`,
    `grobing-kopia-022.age`, wymyślone dane); `Grobing_Restore` ma dane z tej kopii; „Ja” na `Medium_Phone` to Twój wybór
    ze stopu #2;
  - rozpoznanie „Dysk Google” w wierszu kopii sprawdzone tylko testem — pierwszy prawdziwy telefon przy MVP;
  - nieprzetestowane przez nikogo na żywo: TalkBack i duże powiększenie tekstu na Osobach i ustawieniach;
  - makieta wariantów paska ze stopu #1 leży poza repo (katalog tymczasowy tej sesji) — do kosza.
- 2026-10-08 — [[SPIKE-004-mvp-flow-prototype]] zamknięty. **Cały przepływ MVP przeszedł przez klikalny prototyp**, panel po
  panelu, z decyzjami autora zapisanymi od razu w specyfikacjach (D1–D28):
  - **szkielet:** dolny pasek Mapa · Osoby · Drzewo, widok przed poprawą (✎), ustawienia pod kołem zębatym;
  - **mapa Polski jak R1** (sąsiedzi, Bałtyk, wyśrodkowanie) i **zdjęcie cmentarza** w arkuszu;
  - **cmentarz to mapa**: plan offline, zdjęcie z góry online, kwatery autora; znicz → jeden grób, przeciągnięcie → lista;
    **bez linku do Grobonetu**;
  - **widok osoby** (nowy): zdjęcie w tle, portret, mini-drzewo, „jak łączy się ze mną”, pochówek → mapa z pinezką;
  - **płeć wraca** (babcia, stryj, siostra cioteczna); związek „razem” i „małżeństwo”;
  - **drzewo od osoby** z poziomami, kolorami linii i czasem; „Połącz dwie osoby” z animacją na drzewie;
  - **wizyta:** „gdzie jestem”, pinezka z GPS, praca bez internetu;
  - **bez źródeł w aplikacji** — *„a to jakiś błąd się wkradł w takim razie - moje notatki to moje notatki, nie potrzeba żadnych potwierdzeń skąd pochodzą”*: FR-001 i US-004 wycofane, schemat bez zmian.

  Nowe specyfikacje: [[osoba]], [[osoby]], [[drzewo]], [[ustawienia]]. Nowe pozycje: ISSUE-022…025, [[US-007-mapa-cmentarza]],
  [[US-008-pinezka-na-miejscu]] (*In progress* → droga do instalacji MVP). Zmiany zakresu nazwane w SPIKE-004 →
  *Verification*. Werdykt: APPROVED (self-check). Licznik retro: 2 → 3.

  **Dla autora:** prototyp leży poza repo (`%TEMP%\claude\c--Programowanie-Grobing-grobing-agents\e2987d63-950d-4e55-b9fb-24429bf1ed09\scratchpad\grobing-prototyp.html`) — do obejrzenia albo do kosza. Sprawa „data początku związku bez
  ślubu” rozstrzygnięta (*Poza tą kolejnością*).
- 2026-10-08 — [[ISSUE-021-small-fixes-after-retro-2]] zamknięte (retro 2, R3 i R9). **Poprawki przed pierwszymi
  prawdziwymi danymi:**
  - teksty widżetów Fluttera **zawsze po polsku**, niezależnie od języka telefonu (D1): „Wstecz”, menu tekstu
    „Wytnij · Kopiuj · Wklej”, „Zamknij” przy arkuszach. Pakiet `flutter_localizations` z SDK; `intl` cofnięty do
    0.20.2 (decyzja autora; [[ADR-002-flutter-pinned]] → *Follow-ups*). APK +0,8 MB;
  - „Dodaj zdjęcie nagrobka” i link „Zobacz zdjęcie satelitarne” mają akcję dotknięcia — Switch Access i Voice
    Access je naciśną (na emulatorze `clickable` false → true);
  - wymyśleni w buildzie debug: „Wymyślony”, „Wymyślona”, „Wymyślone” (D2);
  - README `grobing-code` → **Testy**: trzy pułapki, przez które przebieg testów wisi, i co zrobić po nim.

  Bez nowego ekranu: kroki na emulatorze zrobił agent (aktualizacja na danych testowych, dane bez zmian). Werdykt `qa`:
  APPROVED (self-check, z uwagami). Testy: 462. Licznik retro: 1 → 2.

  **Fakt 5 z retro 2 ma odpowiedź** (rozmowa z babcią ~2026-11-02) → następna [[US-004-fakt-od-babci]] (*In progress*).

  **Dla autora:**
  - czytnik ekranu czyta teraz tłumaczenia Fluttera, także niezgrabne: tło pod arkuszem to „Siatka”, arkusz to
    „Plansza dolna” (wcześniej „Scrim”, „Bottom Sheet”);
  - `Medium_Phone` ma build release z ISSUE-021, wgrany na Twoje dane testowe (bez odinstalowania).
- 2026-10-08 — [[ISSUE-020-content-guard]] zamknięte. **Strażnik danych rodziny sprawdza też treść**, nie tylko typ pliku:
  - przy każdym `git add`/`commit` porównuje z listą rdzeni (`rdzenie-straznika.txt` w `family_data_dir`): linie
    dodane, pliki nowe, ścieżki, opis commita, plik `-F`. Bez polskich znaków i wielkości liter, rdzeń na początku
    słowa (także camelCase). Odmowa podaje plik, linię i numer linii listy, **nigdy słowo**;
  - brak listy, pusta lista albo rdzeń krótszy niż 3 znaki → blokada. Ręcznie: `-ScanTracked` przeszukuje treść
    trzech repo;
  - **decyzja autora na stopie #2:** nazwiska w rozmowie z agentem są w porządku, chronimy publikację na GitHubie,
    więc listę spisał agent z notatek. Regułę w `family-data.md` poprawił autor (klasyfikator zablokował agentowi);
  - **skan treści trzech repo: 0 nazwisk z notatek** — trafienia tylko w danych publicznych (wyciąg OSM, jedno duże miasto
    mapy Polski, które wypadło z listy).

  Koszt: ok. +0,2–0,3 s na `git add`/`commit`. Testy strażnika: 150. Werdykt `qa`: APPROVED (self-check, z uwagami).
  Licznik retro: 0 → 1.

  **Dla autora:** 4 niepewne odczyty nazwisk na liście (*Autor, poza sesją*); odświeżenie bazy cmentarzy OSM zostanie
  odrzucone (*In progress*).
- 2026-10-08 — **retro 2** ([[2026-10-08-retro-02]]): licznik 10 → 0. Decyzje autora R1–R10 („ok idźmy z twoją
  rekomendacją”):
  - **strażnik treści** — lista rdzeni w `family_data_dir`, czyta ją skrypt strażnika, odmowa bez słowa → [[ISSUE-020-content-guard]] (R1);
  - **stop #2: najwyżej 3 kroki odczucia**, resztę agent robi na emulatorze przed stopem (R4);
  - `dev` przechodzi AC na emulatorze przed `qa` przy ekranach (R5); kandydaci na emulatorze albo makiecie na
    stopie #1, gdy pozycja wybiera to, co widać (R6);
  - ADR-y zostają w łańcuchu, `architect` na sygnał „pierwszy ADR zastąpiony” (R7); DEF-005 do PRODUKCJA (R8);
  - drobne poprawki → [[ISSUE-021-small-fixes-after-retro-2]] (R3, R9); `git rm`/`restore`/`stash` wprost zakazane (R2).

  Na pięć pytań o fakty autor nie odpowiedział — zapisane jako „bez odpowiedzi”, wracają tam, gdzie od nich coś
  zależy (retro 2 → *Load-bearing facts*).
- 2026-10-08 — [[SPIKE-001-map-source-offline]] zamknięty → **[[ADR-003-map-source-offline]] `accepted`**, a z nim
  [[NT-004-grobonet-link-terms]] (regulamin Grobonetu nie zakazuje linku i zakazuje kopiowania). **Mapa cmentarza:**
  - **plan schematyczny offline**: obrys i alejki z OSM, pobrane przy dodaniu cmentarza; bez sieci zaślepka;
  - **ortofotomapa GUGiK tylko online**, za 0 zł (H10). Mapbox, Esri i Google odpadły na warunkach offline;
  - **kwatery i pinezki to dane autora**. Siatki grobów nie ma, bo plany zarządców nie są do kopiowania;
  - aplikacja dostanie `INTERNET` tylko do pobrania planu i zdjęcia online ([[NFR-005-dane-nie-opuszczaja-telefonu]]).

  Pomiary (bez nazw cmentarzy):
  - lista autora to 8 pozycji, czyli 11 cmentarzy;
  - wyszukiwarka grobów zarządcy: 11 z 11, plan z kwaterami w sieci: 8 z 11, Grobonet: 6 z 11;
  - rzędy grobów na zdjęciu widać w 7 z 8 obszarów;
  - kwatery w OSM: 1 na 8 obszarów; gęste alejki w OSM: 4 z 8;
  - prototyp pokazał w trybie samolotowym plan i zdjęcie z plików.

  Autor zakwestionował zdjęcie na stopie #2. Na jego prośbę agent zrobił szkic planu na emulatorze, a autor
  wybrał kierunek „Jak u Ciebie”. Werdykt `qa`: APPROVED (self-check, z uwagami). Licznik retro: 8 → 10.

  **Dla autora:**
  - sprawdzenie na cmentarzu przy najbliższej wizycie → §Parked;
  - folder prototypu `_throwaway` usunięty 2026-10-08 na Twoją prośbę;
  - pole „link do wyszukiwarki zarządcy” zamiast „link do Grobonetu” czeka na Twoją decyzję przy pierwszej US mapy
    cmentarza.
- 2026-10-08 — [[ISSUE-019-family-relations]] zamknięte, a z nim **[[US-003-przepisanie-rodziny]]** (werdykt US: APPROVED,
  niezależny przegląd, z uwagami). **Rodzinę wpisuje się naraz, a relacje widać przy osobie:**
  - w formularzu osoby (poprawa) sekcja **„Rodzina”** ([[wpis-osoby]] v5.2): rodzice i każdy **związek** z dziećmi jako
    chipy „Rodzic”, „Partner”, „Dziecko”, które otwierają wpis krewnego, także osoby bez grobu; „Dodaj rodziców”,
    „Dodaj związek”, ✎;
  - **arkusz rodziny** ([[rodzina]] v1.2): para, ślub, koniec związku (rozwód albo rozstanie; owdowienie to zgon), dzieci
    według daty urodzenia; nowa osoba wpisana w arkuszu albo wybrana — **najpierw szukaj, potem twórz**; „Usuń rodzinę”;
  - **schemat v6:** twierdzenie o parze przy rodzinie, o dziecku przy jego łączu — [[ADR-011-relation-claims-family-and-child-link]];
    migracja v5→v6 z testem, bez dopisywania wierszy (kopie v5 odtwarzają się bez zmian); kopia z rodzinami odtworzona na
    drugim emulatorze z odciskiem zgodnym;
  - **decyzje autora na stopie #1:** bez płci (nazwy neutralne), bez rodzeństwa przy osobie, „związek” zamiast
    „małżeństwo” (rozstania, owdowienia, nowe związki), dzieci według urodzenia.

  Przegląd `ui`: 0 BLOCKER, 1 MAJOR (komunikat błędu daty pod „Zapisz” przy otwartej klawiaturze — także w formularzu
  osoby, wspólny blok daty) poprawiony przed stopem #2, 4 MINOR poprawione. `dev` znalazł na emulatorze dwa błędy przy
  zielonych testach (współdzielony strumień drift, uśpiony też w widoku grobu; „dalej” przeskakujące pole) — poprawione, z
  testami. Werdykt `qa`: APPROVED (self-check, z uwagami); stop #2 „ok” (krok 2 pominięty, sprawdzony przez agenta).
  Testy: 458.

  **Dla autora:**
  - u Ewy Wymyslonej na `Medium_Phone` są Twoje dane testowe ze stopu #2 (rodzice Stefan i Anna, związek z Janem), a w nich
    cykl: Stefan jest dzieckiem Anny i jednocześnie rodzicem z nią Ewy — aplikacja na to pozwala (kandydat wyżej);
  - kopia na `Medium_Phone` skonfigurowana od nowa z hasłem testowym do Pobranych (`grobing-klucz-019.age`,
    `grobing-kopia-019.age`, wymyślone dane); `Grobing_Restore` ma dane z tej kopii;
  - pomiar podpowiedzi płci z imienia (rejestr PESEL: 0,066% pomyłek wśród zmarłych) czeka w ISSUE-019 → *Prior art*,
    gdyby płeć wróciła z drzewem.
- 2026-10-07 — [[US-003-przepisanie-rodziny]] rozpisana na **jedną** pozycję, [[ISSUE-019-family-relations]] (`docs`,
  auto-flow po `pm`). Schemat v6 (źródło i status przy przynależności partnerów i dzieci, AC-4) idzie razem z ekranem,
  jak w ISSUE-016…018. Ten podział zaproponował łańcuch, nie autor, więc na stopie #1 autor może pozycję podzielić.
  Tabele rodzin są od v1, a zdarzenia rodziny z twierdzeniami od v2, więc daty małżeństwa nie zmieniają schematu. To
  rozpisanie, nie zamknięcie, więc licznik retro bez zmian. Rozpisanie wejdzie do commita paczki ISSUE-019.
- 2026-10-07 — [[ISSUE-018-profile-photo-crop]] zamknięte. **Profilowe pokazuje twarz osoby, a nie środek zdjęcia
  grupowego:**
  - ekran „Kadr profilowego” ([[kadr-profilowego]] v1.2): okrąg stoi, pod nim przesuwa się i przybliża zdjęcie (decyzja
    autora D2 na stopie #1), linie trójpodziału, samo „Gotowe”. Przybliżenie: dwa palce albo **podwójne dotknięcie**, a
    dotknięcie twarzy stawia ją na środku. Wejście: „Ustaw jako profilowe” (przez kadr, D3) i „Popraw kadr” na
    profilowym; w podglądzie stan „Zdjęcie profilowe” w pasku ([[zdjecie]] v1.4);
  - **kadr należy do łącza osoby**, więc każda osoba na zdjęciu grupowym ma własny, a plik się nie zmienia. Pokazują go
    okrąg w formularzu, karta w widoku grobu i nagłówek zdjęć osoby;
  - **schemat v5:** `CROP` z GEDCOM 7 w pikselach kopii dostępowej, cztery kolumny przy łączu —
    [[ADR-010-profile-photo-crop-pixels]]; migracja v4→v5 z testem, kopia v4 odtwarza się w v5. Kadr przeżywa każdą
    późniejszą edycję zdjęć osoby;
  - **odtworzenie zdjęć osób na drugim emulatorze — wykonane** (zaległe z US-005): kopia z kadrami, nowe hasło testowe,
    odcisk zgodny.

  Stop #1: D1–D4 „ok”. Przegląd `ui`: 0 BLOCKER, 0 MAJOR, 6 MINOR — poprawione; test znalazł błąd zamykania ekranu
  kadru (poprawiony). Stop #2: autor ustawił kadr na zdjęciu grupowym i poprosił o ekran **bez lup i podpowiedzi** →
  opcja A: przybliżanie podwójnym dotknięciem (próg SC 2.5.1 zostaje). Kroki 2–3 zrobił agent. Werdykt `qa`: APPROVED
  (self-check, z uwagami). Testy: 429.

  **Dla autora:**
  - nieocenione: odczucie podwójnego dotknięcia i ok. 0,3 s, które czeka pojedyncze dotknięcie;
  - czytnikiem ekranu nie da się przesunąć ani przybliżyć zdjęcia na ekranie kadru — nazwana luka ([[kadr-profilowego]]
    K2);
  - pamięć okręgów z małym kadrem zmierzyć na telefonie przy MVP (emulator nie pokazuje pamięci grafiki —
    ADR-010 → *Follow-ups*);
  - na `Medium_Phone` (release v5) kopia jest skonfigurowana od nowa z hasłem testowym do Pobranych emulatora
    (`grobing-klucz-018.age`, `grobing-kopia-018.age`, wymyślone dane); w galerii wymyślone obrazy `wymyslone-duze-1…4.jpg`
    i `wymyslone-grupowe.jpg`; Ewa i Zofia mają profilowe z kadrem ze zdjęcia grupowego. `Grobing_Restore` ma dane z tej
    kopii.
- 2026-10-07 — [[ISSUE-017-person-photos]] zamknięte, a z nim **[[US-005-zdjecia]]** (werdykt US: APPROVED, niezależny
  przegląd, z uwagami). **Osoba ma bazę zdjęć z „profilowym”, a jedno zdjęcie może należeć do kilku osób:**
  - w formularzu osoby okrąg z profilowym i liczbą zdjęć → ekran „Zdjęcia” ([[zdjecia-osoby]]): profilowe, siatka,
    „Dodaj zdjęcie” (kilka z galerii naraz albo aparat);
  - podgląd: „Ustaw jako profilowe”, „Na zdjęciu: …” z „Kto jest na zdjęciu?” (wszystkie osoby, ten grób na górze,
    filtr — decyzja autora D2 na stopie #1, także zaznaczenie później), „Usuń z tej osoby”;
  - profilowe w kartach osób w widoku grobu;
  - zmiany zdjęć zapisują się z „Zapisz” formularza, w jednej transakcji z wpisem (D3);
  - **schemat v4:** zdjęcie jako rekord, łącze osoba–zdjęcie z kolejnością (`OBJE` w GEDCOM 7) —
    [[ADR-009-person-photos-record-and-link]]; migracja v3→v4 z testem, kopia v3 odtwarza się w v4.

  Przegląd `ui`: 0 BLOCKER, 1 MAJOR (semantyka), 5 MINOR — poprawione przed stopem #2. Werdykt `qa`: APPROVED
  (self-check, z uwagami). Stop #2: autor wykonał dodanie z galerii i zdjęcie wspólne, kroki 4–7 zrobił agent. Testy:
  391.

  **Decyzja autora na stopie #2:** kadr profilowego ze zdjęcia grupowego — **następna pozycja**,
  [[ISSUE-018-profile-photo-crop]].

  **Dla autora:**
  - **próbnego odtworzenia na drugim emulatorze nie było** (w sesji nie było hasła testowego z ISSUE-016). Pokrywają je
    testy na prawdziwych archiwach. Przy następnej pozycji z kopią — nowe hasło testowe i odtworzenie na
    `Grobing_Restore`;
  - nieocenione przez ciebie: „Ustaw jako profilowe”, odczucie siatki i okręgu, zapis zdjęć przez „Zapisz” (D3 — inaczej
    niż nagrobek, który zapisuje się od razu) i lista „Kto jest na zdjęciu?”;
  - okno wyboru oddaje zdjęcia w kolejności zaznaczania — sprawdzone tylko na Androidzie 16;
  - na `Medium_Phone` (release v4) są wymyślone osoby ze zdjęciami. Dwie osoby „as Wymyslona” z ISSUE-016 mają teraz
    imiona Ewa i Zofia, a w drugim grobie jest „Jozef z d. Testowy” (do kroków stopu #2). W galerii emulatora leżą
    `wymyslone-1…3.png`.
- 2026-10-07 — [[ISSUE-016-photos-grave-and-person]] zamknięte. **Grób ma zdjęcie nagrobka:**
  - pole „Dodaj zdjęcie nagrobka” w miejscu zdjęcia, nad tytułem (decyzja autora na stopie #2, [[grob]] v3.2 D12) →
    galeria albo aparat → zdjęcie nad tytułem; podgląd na pełnym ekranie z przybliżeniem; „Zmień zdjęcie” i „Usuń
    zdjęcie” (z oknem); miniatura nagrobka na liście grobów;
  - zdjęcie w aplikacji to **kopia dostępowa: JPEG 2048 px, bez EXIF** (decyzja autora D2'), oryginał zostaje w galerii
    albo na papierze — [[ADR-008-photos-access-copy-and-backup-consistency]];
  - **naprawiona luka w kopii z ISSUE-008:** zdjęcie dodane w trakcie kopii dawało kopię, której żadne odtworzenie by
    nie przyjęło (dziś nieosiągalne, ta pozycja by ją otworzyła) — jedna lista plików i sprzątanie (ADR-008 pkt 3);
  - bez nowych uprawnień; APK 57,1 MB (+0,8 MB).

  Stop #1 w dwóch rundach: autor rozdzielił zdjęcia — nagrobek jedno zdjęcie, a osoby **baza zdjęć, dzielona, z
  „profilowym”** → [[ISSUE-017-person-photos]] (schemat v4). Przegląd `ui`: 0 BLOCKER, 1 MAJOR poprawiony przed stopem.
  Werdykt `qa`: APPROVED (self-check, z uwagami); stop #2 „ok”. Testy: 367.

  **Dla autora:**
  - okno wyboru zdjęć na Androidzie 16 wymaga „Done” także przy jednym zdjęciu — to system, nie aplikacja;
  - zdjęć HEIF nie sprawdzono (emulator ich nie zrobi) — pierwsze prawdziwe zdjęcie z Twojego telefonu przy MVP;
  - „Stan danych” przez godzinę po zmianie albo usunięciu zdjęcia pokazuje więcej plików niż wpisów — sprzątanie, nie
    błąd;
  - na `Medium_Phone` kopia jest skonfigurowana **do Pobranych** emulatora (hasło testowe), a `Grobing_Restore` ma dane
    z tej kopii; jego stare ustawienia kopii wskazują folder `Grobing-proba` w Twoim Dysku (wymyślone dane).
- 2026-10-07 — [[US-005-zdjecia]] rozpisana na [[ISSUE-016-photos-grave-and-person]] i [[ISSUE-017-person-photos]]
  (`docs`). Najpierw jedna pozycja (decyzja autora w `pm`), a na stopie #1 autor chciał dla osób **bazy zdjęć,
  dzielonej między osoby, z „profilowym”**, a nagrobkowi wystarczy jedno zdjęcie. To zmiana schematu, więc podział:
  016 — nagrobek i fundament (bez zmiany schematu), 017 — zdjęcia osób (schemat v4, model jak `OBJE` w GEDCOM 7).
  Zdjęcia w aplikacji: **2048 px, JPEG 85** („raczej podglądowe”), oryginał zostaje w galerii albo na papierze. To
  rozpisanie, nie zamknięta pozycja, więc licznik retro bez zmian.
- 2026-10-07 — [[ISSUE-012-transcribe-grave-screen]] zamknięte, a z nim **[[US-002-przepisanie-grobu]]** (werdykt US:
  APPROVED, niezależny przegląd, z uwagami). **Grób z notatek da się przepisać w aplikacji:**
  - arkusz cmentarza na mapie → „Otwórz cmentarz” → lista grobów ([[cmentarz]] v2.1: „R2 bez satelity”, bez pola
    mapy, dopóki groby nie mają pinezek) → „Dodaj grób” → formularz pierwszej osoby → widok grobu jak R4 bez
    zdjęć ([[grob]] v2.1) → „Dodaj osobę”;
  - formularz osoby ([[wpis-osoby]] v2.2): imiona, nazwisko (w grobie podpowiedziane), z domu, urodzenie i zgon z
    dopiskiem i podglądem, „kim była” jako krótka biografia z linią źródła; daty i pochówek zawsze ze źródłem
    „notatki”, `CLAIMED`; zapis całością albo wcale;
  - **nazwa grobu** z ✎ w widoku grobu — schemat v3 (migracja v2→v3 z testem; kopia v2 odtwarza się w v3);
  - **poprawa wpisu** (D1): wartości poprawiane w miejscu, data z kilku źródeł tylko do odczytu;
  - **kopia zamawia się zaraz po migracji** (retro 1, R6 dowiezione): start pyta o kopię dopiero po otwarciu bazy.

  Na stopie #2 autor zdecydował (D7): **bez pola „Pochówek”** w formularzu — model danych zachowuje datę pochówku,
  [[FR-004-data-z-dopiskiem]] ma linię o pokryciu. Na stopie #1 autor zapytał o siatkę kwater (→
  `01_INBOX/2026-10-05-plany-cmentarzy.md`), relacje (→ US-003) i zdjęcia (→ US-005). Przegląd `ui`: 0 BLOCKER,
  0 MAJOR, 5 MINOR poprawione przed stopem; wytyczne [[style-b]] v1.6. Werdykt `qa`: APPROVED (self-check, z
  uwagami); stop #2 „ok”. Testy: 341.

  **Dla autora:**
  - **czy notatki podają daty pochówku — niesprawdzone.** Pierwszy taki wpis przy przepisywaniu
    ([[NT-002-transcribe-the-notes]]) to sygnał, żeby pole wróciło (bez migracji);
  - na emulatorze `Medium_Phone` jest build release z publicznym cmentarzem (Powązki) i grobem z kroku stopu #2
    (wymyślone osoby). Kopia w tle po aktualizacji zadziałała na starym buildzie debug z konfiguracją testową
    z ISSUE-010, a na obecnym release kopia nie jest skonfigurowana.
- 2026-10-07 — **push bez pytania** (decyzja autora, po pierwszym pushu): `docs` wypycha paczkę zaraz po
  commicie. W retro 1 autor chciał automatu dla commitu i pushu, a zapis R1 („push tylko po „go””) tego nie
  oddał. „go” zostaje tylko tam, gdzie odpowiedź może brzmieć „nie”: commit spoza łańcucha (np. z VS Code),
  odrzucony push, nowe repo albo remote, ustawienia GitHuba. Nigdy force, pull ani rebase. Reguły:
  `grobing-agents` → `git-autonomy-boundary.md` → *push*. To nie zamknięcie pozycji, więc licznik retro bez
  zmian.
- 2026-10-07 — **pierwszy push: trzy repo publiczne na GitHubie** (za „go” autora, stop #3):
  [grobing-agents](https://github.com/aleksanderginalski/grobing-agents) ·
  [grobing-vault](https://github.com/aleksanderginalski/grobing-vault) ·
  [grobing-code](https://github.com/aleksanderginalski/grobing-code). Repo założone puste (bez README,
  licencji i `.gitignore`), `main` śledzi `origin/main`.
  - **przed pushem:** 3 commity powstałe po przeglądzie historii z [[NT-008-publication-review]] (zamknięcie
    NT-008 i ISSUE-015) przeszukane **bez notatek rodziny**. Kody pocztowe, PESEL, adresy, numery kwater i
    sekrety: 0. Współrzędne i miejscowości: tylko publiczne (znane cmentarze w testach, wynik z bazy OSM) albo
    wymyślone. Nazwiska osób: 0;
  - odczyt `family_data_dir` zablokował klasyfikator uprawnień Claude Code mimo zgody autora (*Do retro*).
    Nazwy z notatek w zmianach ISSUE-015 pokrywa grep `qa` przed commitem (ISSUE-015 → *Verification*);
  - **granica:** tekstu dopisanego przy zamknięciu ISSUE-015 nikt nie przeszukał nazwami z notatek;
  - obudził się [[DEF-005-push-gate]] → *In progress*.
  
  To nie zamknięcie pozycji, więc licznik retro bez zmian.

  **Dla autora:** repo nie mają pliku `LICENSE` — kod można oglądać, ale nie wolno go używać. Licencję można
  dodać później.
- 2026-10-07 — [[ISSUE-015-add-cemetery-from-database]] zamknięte. **Cmentarz dodaje się z wbudowanej bazy
  cmentarzy Polski**, bez sieci:
  - wyciąg z OpenStreetMap: ok. 16 tys. cmentarzy z miejscowością (z dzielnicą w mieście), województwem i
    wyznaniem, licencja ODbL, podpis „Dane: © autorzy OpenStreetMap (ODbL)”;
  - wyniki z bazy pod twoimi cmentarzami; „Dodany” przy tym, który już masz; najwyżej 30 wyników z
    podpowiedzią, żeby dopisać miejscowość;
  - podgląd na mapie ze zniczem w obrysie. Link „Zobacz zdjęcie satelitarne ↗” otwiera Mapy Google w widoku
    satelitarnym, tylko po dotknięciu (`geo:` nie umie wybrać warstwy — D1). Okno z nazwą do poprawy i
    „Zapisz”;
  - aplikacja dalej bez `INTERNET`, APK +0,62 MB; pierwsze wczytanie bazy ok. 0,5 s.

  Przegląd `ui` w 2 rundach (MAJOR: przybliżenie podglądu), specyfikacja [[cmentarze]] v2.2, [[style-b]] v1.5.
  Werdykt `qa`: APPROVED (self-check, z uwagami); stop #2: 8 z 8 „tak”. Testy: 309.

  **Dla autora:**
  - zapytań Overpass w README `grobing-code` nie wykonano ponownie (serwery 2026-10-07 nie odpowiadały).
    Plik bazy pochodzi z wyciągu z 2026-10-06;
  - emulator `Medium_Phone` wrócił ze starego snapshotu z buildem debug — teraz jest na nim build release z
    jednym publicznym cmentarzem z kroku 4 stopu #2.
- 2026-10-07 — [[NT-008-publication-review]] zamknięte. **Push na GitHuba odblokowany**, choć jeszcze się nie
  odbył:
  - agent przeszukał historię trzech repo (41 commitów, razem z opisami) imionami, nazwiskami i miejscami z
    notatek rodziny, za zgodą autora w sesji. Przegląd nie znalazł w historii danych rodziny. Liczby i granice przeglądu są w
    NT-008 → *Progress*, bez żadnego imienia;
  - jedną linię (prompt R3 w `05_DESIGN/brand/references.md`) autor potwierdził jako wymyśloną;
  - wybór autora: **wszystkie trzy repo publiczne**. Skutek dla [[SPIKE-001-map-source-offline]]: nazwy
    cmentarzy autora nigdy nie trafiają do vaulta, tylko liczby.
  
  Push odbył się tego samego dnia (wpis wyżej). Przegląd imion przy kolejnych pushach czeka na retro.
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
