---
title: "Grobing — Current State"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-08
---

# Grobing — Current State

> Żywy obraz tego, gdzie produkt jest teraz. Krótszy i bardziej zmienny niż `SESSION_STATE.md`.

> 📍 **Ten plik jest jedynym licznikiem stanu produktu** — etap dojrzałości, co w toku, licznik do
> retro, sprawy zaparkowane. **Żaden inny plik ich nie powtarza; wszystkie linkują tutaj.** Wolisz
> *„patrz `backlog/issues/`"* niż *„12 zadań"* — wskaźnik się nie zestarzeje.

## Maturity stage
MVP — od startu, cały produkt (Meta-decyzja 4).

## In progress
- **[[SPIKE-001-map-source-offline]] zamknięty 2026-10-08** → [[ADR-003-map-source-offline]] `accepted`: mapa
  cmentarza to **plan schematyczny z OSM offline** + ortofotomapa GUGiK online + kwatery i pinezki autora. Kolejność
  autora z 2026-10-06 jest wyczerpana, więc następną pozycję proponuje `pm`. **Najpierw retro** (licznik niżej).
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
  - [[NT-001-photograph-the-notes]]: zdjęcia zrobione (33). Zostało: zaszyfrowane miejsce, sprawdzenie
    kopii w WhatsAppie i otwarcie kopii — *Resolution*;
  - [[SPIKE-002-tree-on-a-phone]]: przed drzewem (widok 5);
  - **wyszukiwanie w bazie cmentarzy — tematy do decyzji autora** ([[ISSUE-015-add-cemetery-from-database]] →
    *Notes*): literówki z OSM zajmują pierwsze miejsca, skracanie słów łapie podobne nazwy („krakow” →
    „…Krakowskie”), w bazie są cmentarze dla zwierząt, a wynik znaleziony przez okoliczną miejscowość nie
    mówi, przez którą. Kandydat na małą pozycję, gdy zacznie przeszkadzać przy prawdziwych cmentarzach;
  - **semantyka przycisków w dwóch starszych ekranach** (przegląd `ui` [[ISSUE-017-person-photos]], MAJOR tego samego
    wzorca): „Dodaj zdjęcie nagrobka” ([[ISSUE-016-photos-grave-and-person]]) i podgląd cmentarza z bazy
    ([[ISSUE-015-add-cemetery-from-database]]) mają opis dla czytnika, ale bez akcji dotknięcia. Switch Access i
    Voice Access ich nie naciśną. Poprawka: dwie linie i test na ekran. Autor nie zdecydował (pytanie na stopie #2
    ISSUE-017) — kandydat na małą pozycję;
  - **kontrola cykli w rodzinie** ([[ISSUE-019-family-relations]] → *Manual*): aplikacja pozwala, by osoba była w parze ze
    swoim dzieckiem albo była swoim przodkiem — zobaczone w danych testowych autora na stopie #2. Poza zakresem ISSUE-019
    ([[ADR-011-relation-claims-family-and-child-link]] → *Follow-ups*). Kandydat na małą pozycję, gdy zdarzy się przy
    prawdziwym przepisywaniu;
  - **data początku związku bez ślubu** (przegląd US-003, uwaga 4): arkusz ma „Ślub” i „Koniec związku”, a uwaga autora do
    O1 mówiła o związkach „w danym okresie”. Związek bez ślubu da się zapisać, ale bez daty początku. **Decyzja autora**,
    gdy pojawi się w notatkach: osobne pole „Początek związku” albo „Ślub” z innym podpisem;
  - **[[DEF-005-push-gate]] obudzony** pierwszym pushem (2026-10-07). Bramka potrzebuje pipeline'u CI,
    którego nie ma (`ci` na sygnał), a pipeline budzi też [[DEF-003-dependency-scanning]]. **Decyzja autora:**
    wdrożyć teraz albo zostawić do PRODUKCJA (DEF-005 → *Wake*). Do tego czasu status `deferred`.
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
    testowe). Pliki o tej samej nazwie w kilku folderach mylą wyszukiwarkę okna przy odtworzeniu;
  - po SPIKE-001: **usunąć folder `C:\Programowanie\Grobing\_throwaway\`** (prototyp poza repo; publiczny cmentarz
    testowy, bez danych rodziny). Ochrona Claude Code zablokowała usunięcie agentowi, bo był katalogiem roboczym
    sesji.
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
  paczki (decyzja autora 2026-10-07); przegląd imion na wychodzących zmianach czeka na retro (*Do retro*).

## Retro / fact-confirmation counter
- Zamknięte pozycje od ostatniego retro: **10** (ostatnie retro: [[2026-10-06-retro-01]]). Co **10** →
  retro + pytanie o 3–5 nośnych faktów (Meta-dec. 3g, 3h SC-16, A3). Licznik żyje **tylko tutaj**;
  podbija go `docs` przy zamknięciu, a zeruje go retro. **⏰ Sygnał dla `pm`: licznik osiągnął 10 (SPIKE-001 i
  NT-004, 2026-10-08) — retro przed następną pozycją.**
- Do retro (zebrane po drodze, bez decyzji):
  - **przegląd imion przy każdym pushu** ([[NT-008-publication-review]] → *Progress* 2026-10-07): przegląd
    historii objął commity do 2026-10-07. Każdy kolejny push publikuje nowe commity, a treść pilnuje tylko
    uwaga agenta, dopóki nie ma [[ISSUE-003-setup-quality-critic]]. Od 2026-10-07 push idzie sam, więc
    nie ma już momentu „go”, w którym człowiek patrzy na wychodzące zmiany. Kandydat: ten sam przegląd
    imion na zmianach przed `git add`. Dziś to niemożliwe bez prośby autora w sesji, bo agent nie czyta
    `family_data_dir` sam. Do decyzji: zmiana w `family-data.md` (np. lista rdzeni imion w `family_data_dir`,
    czytana tylko przy „go”) albo prośba autora przy każdym pushu. **Pierwszy push (2026-10-07) pokazał, że
    sama prośba nie wystarcza:** odczyt `family_data_dir` zablokował klasyfikator uprawnień Claude Code (dane
    osobowe), choć autor zgodził się w sesji. Każda z opcji wymaga więc reguły uprawnień w ustawieniach albo
    przeglądu, który robi sam autor;
  - **po czytaniu `family_data_dir` grep obowiązkowy** ([[ISSUE-014-home-map-of-poland]] → *Self-check*):
    `ui` wpisał do specyfikacji trzy prawdziwe przykłady zaraz po porównaniu z listą autora. Złapane przed
    commitem, bo strażnik nie widzi treści. Do decyzji: krok w regule `family-data.md` albo w checkliście R1;
  - **`git rm --cached` przez `dev`** (ISSUE-014 → *Dev report* → *Deviations* 5): zmiana indeksu poza commitem
    po checkliście. Zgłoszone od razu, skutek bez znaczenia (ta sama zmiana weszła do commita). Do decyzji:
    czy reguła ma wprost wymieniać `git rm` i `git restore`;
  - **zawieszony przebieg testów** (ISSUE-014 → *Verification*): drift zamyka strumień na timerze fałszywego
    czasu testu. Wzorzec sprzątania jest w testach; czy dopisać go do README `grobing-code` → testy.
    **Drugi przypadek w ISSUE-012** (→ *Verification*): zapis albo odczyt bazy w `tester.runAsync` przy podpiętym
    ekranie ze strumieniem drift wisi bez końca (zakleszczenie na blokadzie bazy), a limit czasu testu go nie
    przerywa. Wzorzec `leaveScreen` jest w `grave_screens_test.dart`. Po zawieszonym przebiegu `flutter test` padł
    na zablokowanym `sqlite3.dll` i zapisał `flutter_01.log` w korzeniu repo (usunięty przed commitem). Są już
    dwie instancje, więc kandydat na krótką sekcję README → testy;
  - **wstępne dane debug** (ISSUE-012 → *Notes*): wszyscy wymyśleni z ISSUE-007 mają nazwisko „Wymyślona”, także
    „Ojciec” — na ekranach wygląda to jak błąd odmiany;
  - **polskie `MaterialLocalizations`** (przegląd `ui`, uwaga 11): systemowe podpowiedzi są po angielsku —
    kandydat na małą pozycję;
  - **stop #2 w praktyce: autor robi część kroków** ([[ISSUE-017-person-photos]] → *Manual*): z 7 kroków autor wykonał
    2 (stan urządzenia), odpowiedział „względnie ok” z nową prośbą, a kroki funkcjonalne zrobił agent. To kolejna
    instancja po ISSUE-008, ISSUE-009, ISSUE-012 i ISSUE-014 (stop #2 tamtych pozycji: kroki pominięte albo „ok” bez
    śladu w stanie urządzenia). **Kolejna w [[ISSUE-018-profile-photo-crop]]:** autor wykonał krok 1 (bez „Gotowe”), dał
    odczucie z prośbą o zmianę i napisał *„nie planowałem więcej testować”*; kroki 2–3 zrobił agent. Kandydat: stop #2 z 2–3 krokami
    odczucia, a resztę od razu robi agent. **[[ISSUE-019-family-relations]] przeszła już tak (3 kroki):** autor zrobił krok 1 z
    nadmiarem (rodzice, koniec związku), krok 2 pominął i odpowiedział „ok” bez uwag — stan sprawdził agent na urządzeniu;
  - **emulator przed testami łapie to, czego testy nie widzą** ([[ISSUE-019-family-relations]] → *Dev report* → *Deviations*):
    przejście `dev` przez ekrany znalazło dwa błędy przy zielonych testach — współdzielony strumień drift (uśpiony też w widoku
    grobu od ISSUE-012) i „dalej” przeskakujące pole. Oba mają teraz testy. Do decyzji: czy przejście `dev` na emulatorze
    przed `qa` ma być krokiem reguły;
  - **agent `architect`** — kick-off (MD3c) dał mu sygnał „decyzja wymagająca ADR-a poza kick-offem”. Ten
    sygnał już był: [[ADR-005-sqlite-package]] i [[ADR-006-claimed-value-separate-structures]] powstały w
    łańcuchu (`planning` → `docs`), bez osobnego agenta, i [[ISSUE-014-home-map-of-poland]] doda kolejny.
    Według R9 sygnał z kick-offu wygrywa. **Decyzja autora:** zbudować `architect` albo zapisać, że ADR-y
    zostają w łańcuchu. Wykrył to przegląd `kickoff/` (R4); do tego czasu ADR-y robi łańcuch jak dotąd.
  
  - **szkic na emulatorze zmienił decyzję ADR** ([[SPIKE-001-map-source-offline]] → *Verification*): na stopie #2 autor
    zakwestionował zdjęcie („mało co widoczne”), pokazał plan z Grobonetu i poprosił o szkic na emulatorze. Po szkicu
    wybrał plan schematyczny zamiast zdjęcia offline, które rekomendował `dev`. Stop #2 autor znów przeszedł nie
    krokami, tylko odczuciem i pytaniem o kierunek. Kandydat: przy pozycjach z decyzją widoczną dla użytkownika szkic
    na emulatorze przed stopem #1, a nie po pomiarach;
  - **narzędzia pod presją** (SPIKE-001): agent dwa razy zawiesił powłokę `python -I -`, choć pamięć to opisuje, a
    ochrona Claude Code zablokowała usunięcie folderu prototypu, który był katalogiem roboczym sesji. Kandydat:
    prototyp w katalogu, który nie staje się katalogiem roboczym (`cd` tylko w komendzie), i pamięć sprawdzana
    przed pierwszym wywołaniem Pythona.

  Tematy z poprzedniego okresu rozliczyło [[2026-10-06-retro-01]] (R1–R10).

## Parked (waiting on someone outside the session)
- **cmentarz (którykolwiek z cmentarzy autora)** · przy 3 grobach, które autor zna: (a) dokładność GPS telefonu
  przy grobie w metrach (dowolna mapa z niebieską kropką); (b) czy kropka trafia we właściwą kwaterę, rząd albo
  aleję; (c) czy przy bramie wisi plan z kwaterami. Odpowiedź w czacie: **same liczby i tak/nie**, bez nazw i
  położeń · warunek obudzenia: **najbliższa wizyta na cmentarzu** · 2026-10-08 ([[SPIKE-001-map-source-offline]] D5;
  mierzy H3 i H9 przed budową pinezek w [[EPIC-002-wizyta]]).

Format wpisu: `źródło (babcia / cmentarz X) · pytanie bez danych rodziny · warunek obudzenia
(zdarzenie) · data zapytania`. **Odpowiedź z faktami o rodzinie trafia do aplikacji, nie tutaj.**

## Recently done
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
  - folder `_throwaway` do usunięcia (*Autor, poza sesją*);
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
