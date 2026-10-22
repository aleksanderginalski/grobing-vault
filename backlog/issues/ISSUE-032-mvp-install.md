---
title: "ISSUE-032 — MVP install on the author's phone: data-model audit, hand checks, conditions before the first real data"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-22
verdict-reviewer: self-check
source: "[[2026-10-13-retro-03]] R8, R9 · `CURRENT_STATE.md` → *Droga do instalacji MVP* (ostatni krok bez pozycji)"
created: 2026-10-13
updated: 2026-10-21
---

# ISSUE-032 — Instalacja MVP na telefonie autora

> **`draft`: dom dla dwóch decyzji retro 3, a nie plan.** Droga do instalacji MVP kończyła się krokiem bez pozycji; retro 3
> dało mu dwie rzeczy — audyt (R9) i jedną listę rzeczy niesprawdzonych w ręce (R8). Plan pisze `planning`, gdy droga dojdzie
> do tego kroku (po [[ISSUE-041-google-play-and-safe-update]] … [[ISSUE-046-icons]] i [[NT-007-hand-over-note]] — kolejka w `CURRENT_STATE.md`).
>
> **2026-10-16 ([[2026-10-16-retro-04]]):** instalacja **ze sklepu** (Google Play, testy wewnętrzne — [[ISSUE-041-google-play-and-safe-update]]), nie
> `adb install`; **najpóźniej 2026-10-29** — prawdziwe dane autor wpisuje w trakcie wyjazdu na Wszystkie Święte. Telefon: Motorola moto g82 5G,
> Android 13. *Hand checks* w dwóch listach (R4).

## Why
Po instalacji na telefon trafiają **prawdziwe dane rodziny** (decyzja autora 2026-10-08) — od tej chwili błąd kosztuje dane, a nie
rundę. Wszystko, co do tej pory sprawdzał tylko emulator, test albo nikt, ma być sprawdzone albo świadomie przyjęte przed
pierwszym prawdziwym wpisem.

## Before install
Warunki — każdy ma swój dom, tutaj tylko lista:
0. ✅ (2026-10-22, *Verification*) **Sklep — przeniesione z [[ISSUE-041-google-play-and-safe-update]] (AC-1, decyzja autora 2026-10-16: najpierw funkcje z kolejki, potem sklep).**
   Kod jest gotowy (migawka sprzed aktualizacji, numer wersji, README → *Wydanie*); zostały kroki z ISSUE-041 → *Implementation plan* → *Steps*:
   A1 — paczka (`flutter build appbundle --release`, numer z `pubspec.yaml`) i wpis w Play Console przez autora (aplikacja, testerzy, pierwsza
   wersja z **kluczem wygenerowanym przez Google**; **nazwa `com.grobing.app` zajęta → STOP**); A2 — telefon: zaproszenie testera, instalacja ze
   sklepu (Grobing z APK wcześniej → odinstalować); C6 — wymyślona rodzina z kopii zrobionej na emulatorze z nowym hasłem testowym, „Odtwórz z
   kopii”, odcisk w „Stanie danych”; C7 — następny numer wersji, wysyłka, aktualizacja ze sklepu, **ten sam odcisk**. Wynik → lista A niżej.
   Ikona do karty w Play Console (512 × 512, znicz L1) jest gotowa poza repo: `C:\Programowanie\Grobing\_ikony-dalle\sklep-ikona-512.png`
   ([[ISSUE-046-icons]]; przebudowa — README `grobing-code` → *Ikony*);
1. ✅ (2026-10-21, *Audit*) **Audyt pól modelu ↔ ekrany** (retro 3, R9): każde pole [[data-model]] ma ekran, który je zapisuje, albo jawne „nie zapisuje go
   żaden ekran, bo…”. Powód: adres kwatery (M1) miał kolumny od v1, a ekran dopiero w [[ISSUE-028-cemetery-sectors]]. Robi agent;
   wynik to tabela w tej pozycji. Znani kandydaci: `is_living` ([[ISSUE-040-export-is-the-backup]] → *Notes*) i `grobonetUrl` (link wycofany —
   [[cmentarz]] D12; zauważone w `/pm` 2026-10-16);
2. ~~**klucz wydania** (`.jks` i oba hasła) w zaszyfrowanym miejscu~~ — **po [[ISSUE-041-google-play-and-safe-update]] nie blokuje** ([[2026-10-16-retro-04]]):
   klucz podpisu trzyma Google, a obecny klucz wydania zostaje kluczem przesyłania, który da się zresetować. Kopia dalej wskazana;
3. ⏸ odłożone decyzją autora 2026-10-22 do [[NT-007-hand-over-note]] (*Verification*, krok 12) — **notka przekazania** sprawdzona jej własną drogą — [[NT-007-hand-over-note]];
4. ✅ (2026-10-22) **dane aplikacji wyczyszczone** po próbie aktualizacji z [[ISSUE-041-google-play-and-safe-update]] (wymyślone dane) — Ustawienia → Aplikacje →
   Grobing → Pamięć;
5. kandydaci na małe pozycje „przed instalacją MVP” — `CURRENT_STATE.md` → *Poza tą kolejnością* (np. mapa cmentarza przy
   tekście 200%);
6. *kandydat, nie decyzja retro:* testy dostępności dotyku z R2 (`meetsGuideline`) na ekranach zbudowanych przed retro 3 — decyzja
   przy planowaniu.

## Hand checks — rzeczy niesprawdzone w ręce
> **Jedno miejsce, dwie listy** (retro 3, R8; podział — [[2026-10-16-retro-04]], R4). Pisze `docs` przy zamknięciu każdej pozycji: każde
> „pomiń”, „ok” bez śladu na urządzeniu i „nieprzetestowane na żywo” z *Verification* → jeden wiersz ze źródłem, w liście A albo B.
> - **A — dane** (kopia, odtworzenie, aktualizacja ze sklepu, migracja): na telefonie z buildem ze sklepu, na wymyślonych danych, **przed**
>   pierwszymi prawdziwymi. To jest bramka.
> - **B — odczucie** (telewizor, TalkBack, płynność, wygląd, przepływ): **w trakcie używania, bez bramki** — R4 zmienia tu R8 z retro 3, bo lista
>   urosła ponad 40 wierszy, a stop #2 „pomiń” dwa razy z rzędu (ISSUE-038, ISSUE-039). Kroki stopu #2, które wymagają telewizora albo telefonu,
>   trafiają tu od razu.
>
> Krok w terenie (GPS przy grobach, słońce, tryb samolotowy) jest w `CURRENT_STATE.md` → *Parked*, nie tutaj.

### A — dane (przed pierwszymi prawdziwymi danymi)
> **2026-10-22:** wiersze sprawdzone na telefonie autora z wersjami ze sklepu — [[ISSUE-032-mvp-install]] → *Verification*. Dane z kopii v13 i v14
> odtworzone jako kopia v15, która je zawiera; odtworzenie starszych kopii pokrywają testy. Został jeden wiersz (⏸) — droga z notki.
- ✅ 2026-10-22 — instalacja ze sklepu i aktualizacja tą samą drogą — wymyślone dane i kopia bez zmian (AC-1 z [[ISSUE-041-google-play-and-safe-update]], krok
  *Before install* 0);
- ✅ 2026-10-22 — odtworzenie kopii na telefonie po starcie z migawką — na emulatorze wstrzymane (emulator był w użyciu poza agentem), w kroku C6 na telefonie
  ([[ISSUE-041-google-play-and-safe-update]] → *Verification*);
- ✅ 2026-10-22 (v14 → v15 na telefonie) — pierwsza aktualizacja **ze zmianą schematu** przez sklep: migawka `pre-update/grobing-v<stara>.db` powstaje na telefonie (AC-2 z ISSUE-041 —
  sprawdzone testami i na emulatorze, na telefonie jeszcze nie; [[ADR-019-distribution-play-internal-testing]]) — także v12 → v13 z migawką
  `grobing-v12.db` ([[ISSUE-042-places-of-residence]]: na emulatorze przeszła, liczby wierszy bez zmian), v13 → v14 z migawką `grobing-v13.db`
  ([[ISSUE-043-grave-paid-until]]: na emulatorze przeszła, liczby wierszy bez zmian) i v14 → v15 z migawką `grobing-v14.db`
  ([[ISSUE-044-family-wreaths]]: na emulatorze przeszła, liczby wierszy bez zmian, przerwana migracja zostawiła v14 całe);
- ✅ 2026-10-22 — odtworzenie kopii z **pustym grobem, osobą bez grobu i pochówkiem dodanym z wyboru** „Kto leży w tym grobie?” — na urządzeniu niezrobione (jeden
  emulator na raz, a na `Grobing_Restore` jest demo); test kopii przeszedł ([[ISSUE-047-grave-first-then-people]] → *Verification*, AC-5);
- ✅ 2026-10-22 — odtworzenie kopii ze **zdjęciem dołączonym z „Zdjęć w aplikacji”** (jedno zdjęcie u dwóch osób) i **profilowym z kadrem ustawionym z portretu** — na
  urządzeniu niezrobione; test kopii przeszedł ([[ISSUE-048-portrait-photos]] → *Verification*, `backup_archive_test.dart` „ISSUE-048”);
- ✅ 2026-10-22 — odtworzenie kopii **v15 z rodami** z odciskiem zgodnym — na emulatorze niezrobione z tego samego powodu co v13 niżej; testy odtworzenia v14 → v15 i
  v15 z rodami przeszły ([[ISSUE-044-family-wreaths]] → *Verification*);
- ✅ 2026-10-22 (dane v14 w kopii v15) — odtworzenie kopii **v14 z datą opłaty grobu** z odciskiem zgodnym — na emulatorze niezrobione z tego samego powodu co v13 niżej; testy odtworzenia
  v13 → v14 i v14 przeszły ([[ISSUE-043-grave-paid-until]] → *Verification*);
- ✅ 2026-10-22 (dane v13 w kopii v15) — odtworzenie kopii **v13 z zamieszkaniami** z odciskiem zgodnym — na emulatorze niezrobione (hasła testowego kopii nie ma, a odtworzenie zastąpiłoby
  dane spoza agenta na obu emulatorach); testy odtworzenia v12 → v13 i v13 przeszły, kopia w tle v13 na emulatorze też
  ([[ISSUE-042-places-of-residence]] → *Verification*);
- ✅ 2026-10-22 (przed i po aktualizacji do 1.0.0) — po zmianie danych pojawia się „(w tle)” — w AOT sprawdzał to tylko build profile ([[ISSUE-010-background-backup]]);
- ✅ 2026-10-22 („· Dysk Google” w Ustawieniach) — rozpoznanie „Dysk Google” w wierszu kopii — tylko test ([[ISSUE-022-app-skeleton-tabs-people-settings]]);
- ⏸ odłożone decyzją autora 2026-10-22 ([[NT-007-hand-over-note]] → *Input from ISSUE-032*) — kopia z telefonu otwiera się drogą z notki przekazania ([[NT-007-hand-over-note]]) albo odtwarza na emulatorze ([[NFR-002-odtworzenie-na-nowym-telefonie]]).

### B — odczucie (w trakcie używania, bez bramki)

**Zdjęcia**
- zdjęcie HEIF z telefonu — emulator ich nie robi ([[ISSUE-016-photos-grave-and-person]]);
- okno wyboru oddaje zdjęcia w kolejności zaznaczania — sprawdzone tylko na Androidzie 16 ([[ISSUE-017-person-photos]]);
- nieocenione w ręce: „Ustaw jako profilowe”, siatka i okrąg, zapis zdjęć przez „Zapisz”, lista „Kto jest na zdjęciu?”
  ([[ISSUE-017-person-photos]]);
- kadr profilowego: podwójne dotknięcie i ok. 0,3 s czekania przy pojedynczym; pamięć okręgów z małym kadrem
  ([[ISSUE-018-profile-photo-crop]], [[ADR-010-profile-photo-crop-pixels]] → *Follow-ups*);
- „Zdjęcia w aplikacji”: czy szukanie po osobie wystarcza przy prawdziwych zdjęciach — stop #2, krok 3: **ok bez śladu na urządzeniu**
  ([[ISSUE-048-portrait-photos]]);
- TalkBack: portret i okrąg z inicjałami (także stan „zapisuję zdjęcia”), „Zdjęcie profilowe”, „Zdjęcia w aplikacji” z nagłówkami osób — sprawdzone w
  drzewie semantyki i testach, nie na żywo ([[ISSUE-048-portrait-photos]]);
- płynność przewijania „Zdjęć w aplikacji” przy kilkuset zdjęciach na telefonie — nieprzetestowane na żywo (siatka leniwa, test z 300 zdjęciami;
  [[ISSUE-048-portrait-photos]]).

**Osoby i rodzina**
- tło z pasma w widoku osoby — „pomiń” ([[ISSUE-024-person-view]], krok 3 rundy 2); TalkBack w widoku osoby, ekran 360 dp;
- TalkBack i tekst 200% w kreatorze związku ([[ISSUE-025-gender-kinship-together-since]]);
- TalkBack i duże powiększenie tekstu na Osobach i w ustawieniach ([[ISSUE-022-app-skeleton-tabs-people-settings]]);
- TalkBack na wyborze „Kto leży w tym grobie?”: wiersze „W grobach” czytane jako niedostępne, z powodem — sprawdzone w semantyce i testach, nie na żywo
  ([[ISSUE-047-grave-first-then-people]]).

**Mapa Polski**
- znicz z liczbą i cmentarz bez punktu — kroki pominięte, pokryte testami i agentem ([[ISSUE-014-home-map-of-poland]]);
- wydajność na słabym telefonie, TalkBack w arkuszu, telefon trzymany poziomo ([[ISSUE-023-poland-map-r1-cemetery-photo]]).

**Mapa cmentarza i pinezka**
- znicz → arkusz → uchwyt → lista → wstecz — „ok” bez śladu ([[ISSUE-027-cemetery-map-plan-photo-states]], krok 3); stan „brak w
  OSM”, koszt rysowania, TalkBack na planie;
- rysowanie kwatery celownikiem (K1), zmiana nazwy i „Usuń z planu”, „Wpisz adres” — „pomiń” ([[ISSUE-028-cemetery-sectors]]);
  okno „Popraw grób” przy tekście 200% z otwartą klawiaturą ([[grob]] → *Open*);
- trzy stany ◎ — „ok” bez śladu ([[ISSUE-029-pin-on-site-gps]], krok 2); słaby sygnał i „Włącz” tylko w testach; TalkBack.

**Drzewo** (decyzja autora w `/pm` 2026-10-13: ocena na emulatorze, telefon tutaj)
- zadanie na czas „kim jest X dla mnie” < 30 s przy ok. 100 osobach — „pomiń” na stopie #2 ([[SPIKE-002-tree-on-a-phone]], krok 3; kryterium
  spike'a niezmierzone);
- płynność przesuwania i przejścia między poziomami na fizycznym telefonie — nieprzetestowane na żywo, emulator to tylko wskazówka
  ([[SPIKE-002-tree-on-a-phone]] → *Findings* M3);
- ~~progi S2 (oddalanie odsłania dalszą rodzinę) przy szczypaniu palcami — nieprzetestowane na żywo, na emulatorze tylko przyciski i mysz
  ([[SPIKE-002-tree-on-a-phone]]);~~ — nieaktualne: S2 zastąpione przez [[ISSUE-049-tree-levels-and-zoom]] (poziom na + / −, przybliżanie to sam widok);
- „Pokaż w drzewie” z widoku osoby otwiera drzewo tam, gdzie się go spodziewasz — „ok” bez śladu ([[ISSUE-033-tree-from-a-person]], krok 3);
- TalkBack na drzewie: opisy węzłów („…, Moja babcia, w środek” — od [[ISSUE-035-tree-names-shrink-my-voice]], wcześniej „Twoja”) i pigułka poziomu —
  nieprzetestowane na żywo, tylko `uiautomator` i testy ([[ISSUE-033-tree-from-a-person]]).

**Drzewo — tryb prezentacji** ([[ISSUE-034-tree-presentation-mode]] → *Verification*)
- przesyłanie ekranu z trybu prezentacji na telewizor autora z kafelka szybkich ustawień — nieprzetestowane na żywo (emulator nie przesyła;
  telewizor autora jest odbiornikiem Google Cast — zrzut autora z Zdjęć);
- nazwa kafelka przesyłania ekranu na telefonie autora — podpowiedź mówi o funkcji ([[drzewo]] D26); telefon to **Motorola moto g82 5G, Android 13**
  ([[2026-10-16-retro-04]] → fakt 1) — ani Pixel, ani Samsung;
- paski, obrót i przeciągnięcie od krawędzi na fizycznym telefonie, przy nawigacji, której używa autor — nieprzetestowane na żywo;
- systemowe okno „pełny ekran” przy pierwszym wejściu — przed pierwszym pokazem wejść w tryb raz bez przesyłania;
- TalkBack w trybie prezentacji — nieprzetestowane na żywo;
- wyjście z trybu przyciskiem Wstecz — „ok” bez śladu (stop #2, krok 2; sprawdzone przez agenta i w teście).

**Drzewo — karta Twoim głosem** ([[ISSUE-035-tree-names-shrink-my-voice]] → *Verification*)
- karta w G2 („Moja babcia”, „…babci mojej żony”, „to ja”) brzmi tak, jak autor mówi o rodzinie — „ok” bez śladu na urządzeniu (stop #2, krok 1; autor:
  „zapisz bez śladu”);
- stan „osoba bez rodziny” („nie wiadomo jeszcze, kim jest dla mnie”) — tylko test widżetu, w bazie testowej nie ma takiej osoby;
- opis z trzech odcinków („Siostra cioteczna babci mojej żony”) — tylko test jednostkowy, na emulatorze widać opisy z dwóch odcinków.

**Drzewo — „Przesyłaj na telewizor”** ([[ISSUE-036-cast-from-the-app]] → *Verification* → *Not tested live*)
- telewizor autora na liście systemowego ekranu przesyłania — emulator nie widzi żadnego, nieprzetestowane na żywo;
- co system pokazuje po wyborze telewizora (zgoda, „cały ekran / jedna aplikacja”) i czy drzewo staje poziomo na telewizorze — nieprzetestowane na żywo;
- jednorazowe okno systemu o pełnym ekranie — czy trafia na telewizor przy pierwszym pokazie ([[drzewo]] D16);
- telefon innego producenta (np. Samsung): czy ma ekran przesyłania i czy widzi telewizor Google Cast ([[drzewo]] D29 *Obali*) — nieprzetestowane;
- przejście po powrocie z ekranu systemu na telefonie — na emulatorze ok. 1,1 s z chwilą niedopasowanego drzewa (pierwsze klatki po powrocie 64–100 ms).

**Drzewo — czas na suwaku** ([[ISSUE-037-time-on-the-tree]] → *Verification* → *For ISSUE-032 → Hand checks*)
- przerywany obrys u osoby z datą „przed” (Kazimierz, lata 1880–1910) mówi „nie wiadomo, czy już żył” — „ok” bez osobnego śladu na urządzeniu (stop #2, krok 2);
- czytnik TalkBack: suwak „Rok” zmienia rok co 10 lat, po ❚❚ pada rok — nieprzetestowane na żywo (tylko test semantyki);
- płynność ▶ i przesuwania drzewa na telefonie — emulator zaszumiony (przesuwanie 10–26% wolnych klatek także przed ISSUE-037), ▶ 7–9%.

**Drzewo — historia na telewizorze i tempo** ([[ISSUE-038-history-on-tv-and-tempo]] → *Verification* → *For ISSUE-032 → Hand checks*)
- tempo „Średnio” / „Wolno” przy oglądaniu historii z rodziną; czy przycisk tempa obok „dziś” wygląda na dotykalny (MINOR przeglądu `ui`) — stop #2 „pomiń” (krok 1);
- rok w rogu i listwa w trybie prezentacji na prawdziwym telewizorze — czy to obraz do pokazania — stop #2 „pomiń” (krok 2);
- tryb prezentacji otwarty z roku z karty (Z2) — czy start od 1950, a nie od „dziś”, jest naturalny — stop #2 „pomiń” (krok 3);
- TalkBack w trybie prezentacji — sterowanie od wejścia, rok w rogu bez ogłaszania w trakcie ▶ — nieprzetestowane na żywo (okno zgody TalkBack na emulatorze);
- czytelność roku z kanapy na telewizorze autora i czy obraz telefonu wypełnia szerokość telewizora ([[drzewo]] D38 → *Obali*) — nieprzetestowane na żywo;
- imiona w trybie prezentacji z kanapy — 13 sp ≈ 14′ z 3 m na 55″, poniżej 16′ (I2, [[drzewo]] D27) — nieprzetestowane na żywo;
- „Czas na działanie” z ustawień telefonu wydłuża sterowanie w trybie (Android 10+) — nieprzetestowane na żywo (na emulatorze przez adb).

**Drzewo — „Połącz dwie osoby”** ([[ISSUE-039-connect-two-people]] → *Verification* → *For ISSUE-032 → Hand checks*)
- Ja → Wanda: czy linia (0,7 s na krok) i baner na końcu dobrze opowiadają, kim ktoś jest — stop #2 „pomiń” (krok 1);
- długa ścieżka (np. Ja → Zdzisław): czy pomniejszone drzewo z całą ścieżką (F2) jest czytelne, czy lepszy byłby widok jadący za linią (F1) — stop #2 „pomiń” (krok 2);
- „Od” inne niż Ty (Piotr → Zofia): czy baner w dwóch liniach jasno mówi, kto kim jest dla kogo (O2) — stop #2 „pomiń” (krok 3);
- TalkBack czyta baner raz, gdy się pokaże (region na żywo) — nieprzetestowane na żywo;
- płynność ścieżki na telefonie — linia, wyszarzenie, poziom 4 — nieprzetestowane na żywo (emulator w szumie: przestawienie środka 52–57% wolnych klatek w obu buildach).

**Drzewo — poziomy i przybliżanie** ([[ISSUE-049-tree-levels-and-zoom]] → *Verification* → *For ISSUE-032 → Hand checks*)
- szczypanie na telefonie w trybie prezentacji z obrazem na telewizorze — czy przybliżanie i oddalanie płynie na telewizorze (emulator przez `adb` nie szczypie;
  w teście ekranu dwa wskaźniki);
- cały obraz z kanapy: drzewo oddalone do całego poziomu na telewizorze — czy widać, kto jest kim (okręgi ok. 15 dp, ok. połowa imion);
- płynność oddalania do całego drzewa na telefonie — nieprzetestowane na żywo (emulator: ok. 4 pp więcej wolnych klatek niż build odniesienia, w jego rozrzucie);
- oddalanie tylko dwoma palcami ([[drzewo]] D58): czy ktoś z rodziny nie radzi sobie bez przycisku — *Obali* wyjątku [[style-b]] v1.46;
- TalkBack na żywo: „Dalsza rodzina” / „Bliższa rodzina”, słowo stanu nieaktywnego i pigułka poziomu po zmianie — sprawdzone w drzewie semantyki i testach.

**„Następne” — rok i co się w nim stało** ([[ISSUE-050-next-event]] → *Verification — runda 2* → *For ISSUE-032 → Hand checks*)
- z kanapy na Twoim telewizorze po ⏭: czy widać, kogo dotyczy zdarzenie (pierścień, poświata za wieńcem, linia pary przy ślubie) i czy rok 36 sp wystarcza, a słowa
  mówisz Ty ([[drzewo]] D72–D73) — krok z telewizorem, poza stopem #2;
- ⏭ na telefonie z obrazem na telewizorze: płynność podjazdu drzewa do osób z podpisu, pulsu poświaty (3,6 s) i pojedyncze wolne klatki przy zmianie roku —
  nieprzetestowane na żywo (emulator: 130–175 ms, tak samo przy ▶ w buildzie sprzed pozycji; puls bez zmiany kosztu klatki);
- TalkBack: po ⏭ słychać rok i zdarzenia („W 1868. Urodził się …”) na telefonie i w trybie prezentacji — sprawdzone w drzewie semantyki i testach, nie na żywo.

**Miejsca zamieszkania** ([[ISSUE-042-places-of-residence]] → *Verification* → *For ISSUE-032 → Hand checks*)
- sekcja w widoku osoby po „Zapisz” — autor ocenił karty w formularzu, wpis został niezapisany (stop #2, krok 1);
- „Nazwa z tamtego czasu” i druga linia „dziś: …” w widoku — „ok” bez śladu na urządzeniu (krok 3);
- koniec z następnego miejsca („od 2024” + „od 2026” → „2024–2026”, [[zamieszkanie]] D12) — „pomiń” (krok domykający);
- wybór miejsca na telefonie: kraj na górze po 3 literach (D8), płynność pisania i czas wyszukiwania (emulator ≤ 13 ms na zimnym dysku) —
  nieprzetestowane na żywo; przy wolnym telefonie — wyszukiwanie do `Isolate` (D-dev 8).

**Wieńce rodów** ([[ISSUE-044-family-wreaths]] → *Verification* → *For ISSUE-032 → Hand checks*)
- wieńce w trybie prezentacji na telewizorze z kanapy: czy rody widać i czy drzewo nie jest za gęste (96 dp na osobę) — krok z telewizorem, poza stopem #2;
- płynność drzewa z wieńcami na telefonie — nieprzetestowane na żywo (emulator: bez regresji wobec buildu odniesienia, 12,5–15,0% wolnych klatek wobec
  17,4–18,1%);
- TalkBack przy wierszu „Wieniec rodu” (dwa węzły: słowa i przycisk) i w arkuszu (stan „zaznaczone”) — sprawdzone w drzewie semantyki, nie na żywo.

**Mapa migracji** ([[ISSUE-045-migration-map]] → *Verification* → *Manual verification*)
- mapa z kanapy na telewizorze: kontury krajów, okręgi 32 dp z twarzami albo inicjałami, rok w rogu — czy rodzina rozpoznaje, kto gdzie jest — krok z
  telewizorem, poza stopem #2;
- płynność ▶ na mapie na telefonie — nieprzetestowane na żywo (emulator: 9–20% wolnych klatek, bez regresji wobec wcześniejszego buildu);
- TalkBack na mapie: okrąg, stos, skupienie, przełącznik — sprawdzone w drzewie semantyki i testach, nie na żywo;
- tryb prezentacji mapy z przełącznikiem „Drzewo · Mapa” w sterowaniu ([[mapa-migracji]] D24) — stop #2, krok 3: **pomiń**;
- „Pokaż na mapie” z widoku osoby i rozsunięcie stosu z imionami — stop #2, krok 2: **ok bez śladu na urządzeniu**.

**Ikony** ([[ISSUE-046-icons]] → *Verification* → *Hand checks*)
- kreska ikon w kolorze tekstu pomocniczego w pełnym słońcu (NFR-004) — nieprzetestowane na żywo; przy słabej widoczności: ikony Material —
  `GrobingIcon.weight` 300 → 400; 9 ikon z arkusza autora (w tym trzy zakładki) i znicz — `THICKEN` w `tool/icons/build_symbols.py` i przebudowa fontu;
- ikona aplikacji (znicz L1) na Motoroli — launcher producenta (maska, motyw) może różnić się od Pixel Launchera na emulatorze — nieprzetestowane na żywo.

**Do decyzji autora, gdy zobaczy swoje cmentarze** (nie sprawdzenie, tylko wybór): grubość alejek i znicze, które nachodzą na
siebie ([[cmentarz]] → *Open*, [[ISSUE-030-sector-on-a-visit]]).

## Notes / references
- [[2026-10-13-retro-03]] R8, R9 · `DEFINITION_OF_DONE.md` → *Kto sprawdza* · wyjątki „na telefonie” w DoD (GPS, słońce,
  offline — build release).

## Implementation plan
> `planning`, 2026-10-21 — start z `/pm` tego dnia (autor pominął retro 5, licznik zostaje 10). Pozycja **bez nowego ekranu** — bez `ui`.
> Kod: jedna linia dziennika przy migawce i numery wersji; reszta to sklep, telefon i kopia. **Termin instalacji: najpóźniej 2026-10-29.**
> Kandydaci „przed wyjazdem” bez zmiany bazy (rodzeństwo przyrodnie, [[ISSUE-051-wedding-changes-wreath-and-surname]], mapa cmentarza przy 200%)
> **poza tą pozycją** — `pm` pyta o nie, gdy sklep zadziała; przyjdą jako aktualizacja ze sklepu przed wyjazdem.
>
> **Stop #1 — 2026-10-21, autor: *„tak”*:** D1 (najpierw wersja ze schematem v14), D2–D4 jak niżej, cztery zagrożenia (a)–(d) bez zmian.

### Acceptance (z *Before install* i listy A — bez nowych decyzji)
- **AC-1** (z [[ISSUE-041-google-play-and-safe-update]]) *Given* aplikacja ze sklepu z wymyślonymi danymi *When* aktualizacja ze sklepu bez zmiany
  schematu *Then* odcisk i liczby w „Stanie danych” jak przed, a kopia w tle po aktualizacji przechodzi.
- **AC-2** (lista A, wiersz 3) *Given* wersja ze sklepu ze starszym schematem i wpisanymi danymi *When* aktualizacja ze sklepu ze zmianą schematu *Then* na
  telefonie powstaje migawka `pre-update/grobing-v<stara>.db`, baza ma nowy schemat, liczby wierszy bez zmian (D1).
- **AC-3** (lista A, wiersze 2, 4–8) *Given* kopia v15 z emulatora z przypadkami z listy A *When* „Odtwórz z kopii” na telefonie *Then* odcisk jak na
  emulatorze.
- **AC-4** (*Before install* 1, R9) każde pole [[data-model]] ma ekran, który je zapisuje, albo jawny powód — tabela *Audit* niżej.
- **AC-5** (*Before install* 3, 4; lista A, wiersze 9–11) przed pierwszymi prawdziwymi danymi: dane aplikacji wyczyszczone, kopia skonfigurowana od nowa
  na Dysku („Zapisana w Dysku”), a jej plik otwiera się drogą z notki (`age` → `tar` → odcisk równy „Stanowi danych”) — [[NT-007-hand-over-note]].

### Audit — pola modelu ↔ ekrany (R9, odczyt 2026-10-21)
> Schemat v15, 16 tabel (`lib/data/database.dart`). Odczyt kodu przez subagenta `planning`, dwie tezy (`events.place`, D12) sprawdzone ręcznie.
> Kopia i odtworzenie podmieniają cały plik bazy — żadna kolumna nie jest pisana tylko przy odtworzeniu. **Wynik: każde pole ma ekran albo zapisany
> powód; luki, która wymaga ekranu przed instalacją, nie ma.** Do poprawy w vaulcie (krok F): trzy zdania w [[data-model]] i jedno w `backup-format.md`.

**Pola, których żaden ekran nie zapisuje albo nie pokazuje — z powodem:**

| Pole | Stan | Powód (dom decyzji) | Przed prawdziwymi danymi |
|---|---|---|---|
| `events.place` (miejsce urodzenia i zgonu) | nikt nie zapisuje ani nie czyta (`database.dart:149`) | **kandydat po wyjeździe** — punkt na mapie wymaga zmiany bazy, bo pole to sam tekst ([[mapa-migracji]] D12, [[zamieszkanie]] *Open* 3; pokazane na stopie #1 ISSUE-045). Obejście z D12: pierwsze zamieszkanie z pustym „Od” zaczyna się z urodzeniem | miejsca z notatek po wyjeździe trzeba będzie dopisać — koszt znany |
| `persons.is_living` | nikt nie zapisuje (domyślnie 0), czyta tylko `PersonView` (`person_view.dart:187`), żaden ekran | „nie żyje” wynika z daty śmierci albo pochówku ([[drzewo]] D22) | **kopia = eksport** ([[ADR-018-export-is-the-backup]]): kto czyta bazę bez aplikacji, zobaczy `0` także przy żyjących → zdanie „pomiń `is_living`” w `backup-format.md` → *Opening a backup without Grobing* |
| `cemeteries.grobonet_url` | nikt nie zapisuje ani nie czyta (`database.dart:165`) | link wycofany ([[cmentarz]] D12, [[SPIKE-004-mvp-flow-prototype]] D10) | brak skutku; [[data-model]] (wiersze o Grobonecie) opisuje go jak żywy → oznaczyć jako wycofany |
| `events` typu `burial` (data pochówku) | ekrany czytają (`grave_screen.dart:613`, drzewo), żaden nie tworzy | pole „Pochówek” usunięte decyzją autora ([[ISSUE-012-transcribe-grave-screen]] D7) | tylko gdy notatki podają datę pochówku inną niż śmierci |
| `assertions.source_kind`, `source_detail`, `status`; `persons.bio_source` | zawsze wartości domyślne („notatki”, puste, „claimed”), nigdzie niepokazane | źródła i statusy wycofane ([[SPIKE-004-mvp-flow-prototype]] D28) | gdyby źródła wróciły, wpisy sprzed tego mają domyślne „notatki”; [[data-model]] nazywa `bio_source` „nieużywanym”, a ekrany je zapisują → poprawić zdanie |
| `cemetery_plans.fetched_at`, `server` · `residences.place_unit`, `country_code`, `geonames_id` · kadr na nie-pierwszym zdjęciu osoby | zapisywane, niepokazane | techniczne: pochodzenie planu, rozróżnianie i sortowanie miejsc, kadr czeka, aż zdjęcie zostanie profilowym | — |

**Pola zapisywane przez ekrany (w skrócie):** osoba (imiona, nazwisko, z domu, płeć, „kim była”, ród, bez wieńca) — formularz osoby, kreator
związku, „Dodaj dziecko”, okno rodu · rodzina i dzieci — kreator i podsumowanie związku · zdarzenia (narodziny, śmierć, „razem”, ślub, koniec; daty
z niepewnością i „między”) — formularz osoby, kreator związku · cmentarz (nazwa, miejscowość, punkt) — ✎, „Wskaż na mapie”, baza cmentarzy · plan
cmentarza — pobierany sam z OSM · kwatery — ekran kwater, adres grobu · grób (nazwa, kwatera, rząd, miejsce, opłacone do, pinezka z dokładnością i
czasem) — „Popraw grób”, „Nowy grób”, ekran pinezki · pochówek — formularz osoby, „Kto leży w tym grobie?” · zdjęcia (grób, cmentarz, osoba,
kolejność, kadr, tło) — ekrany zdjęć · zamieszkania — okno miejsca · „ja” — wybór „ja”. Pozostałe kolumny to identyfikatory, klucze obce i
kolejność. **Usuwania nie ma:** pochówku, rodu, grobu ani osoby nie da się usunąć (D23, D16; `CURRENT_STATE.md` → *Poza tą kolejnością*).

### Decisions for stop #1
- **D1 — aktualizacja ze zmianą schematu przez sklep na telefonie, zanim pojawią się prawdziwe dane. Rekomendacja: tak.** Pierwsza wysyłka to
  wersja ze schematem v14 (kod z [[ISSUE-043-grave-paid-until]]), druga — obecna z v15. Na telefonie wpisujesz w v14 jeden grób z dwiema wymyślonymi
  osobami (ok. 3 min), aktualizujesz ze sklepu i agent sprawdza migawkę i liczby. Powód: README → *Wydanie* mówi, że kopia na Dysku po migracji
  nadpisuje się zaraz po starcie, więc **przy złej migracji jedyną siatką jest migawka** — a na telefonie, w buildzie ze sklepu, nie uruchomiła się
  nigdy. Koszt: jedna wysyłka więcej (3 zamiast 2) i ok. 1 h agenta. **Czego nie da:** nie sprawdza drogi powrotu z migawki (to kod z przyszłej
  poprawki — README → *Wydanie*). **D1-b:** bez starej wersji — wiersz listy A przyjęty na testach i emulatorze, a pierwsza zmiana schematu po
  wyjeździe uruchomi migawkę na telefonie pierwszy raz, już z prawdziwymi danymi.
- **D2 — telefon na kablu z debugowaniem USB** (domyślnie, jak D3 w ISSUE-041 i przy Friendsheet): agent wgrywa pliki kopii do Pobranych
  (`adb push`), czyta „Stan danych” (zrzut, `uiautomator dump`) i dziennik migawki (`adb logcat`). **Agent nigdy nie instaluje niczego przez `adb`
  na telefonie** — tylko sklep. Przy dwóch urządzeniach każda komenda `adb` z `-s`. Bez kabla: pliki kopiujesz przez USB sam, a odcisk (16 znaków)
  czytasz z ekranu.
- **D3 — dane próby odtworzenia** (domyślnie): stan sprzed demo z `_pokaz` (wymyślona rodzina — rody, zamieszkania, zdjęcia) plus dopisane z
  wymyślonych rdzeni przypadki z listy A, których tam nie ma. W tym stanie są też **Twoje wpisy z emulatora** (cmentarz, grób z datą opłaty): trafią
  na telefon i znikną przy wyczyszczeniu danych (krok 10); do repo nie trafia nic, a kopie na PC agent usuwa po pozycji.
- **D4 — numery** (domyślnie, README → *Wydanie*): +1 = `0.9.0+1` (v14, numer z tamtego kodu), +2 = `0.9.1+2` (obecny kod z dziennikiem migawki),
  +3 = `1.0.0+3` (tylko numer) — **na tej wersji zaczną się prawdziwe dane**.
- **Przed czym chronimy?** (retro 3, R7) Plan zakłada cztery zagrożenia: (a) aktualizacja wymusza odinstalowanie (podpis, kanał, numer) → tylko sklep,
  AC-1; (b) zła migracja po wyjeździe → migawka sprawdzona na telefonie, AC-2; (c) kopii nie da się otworzyć — zgubione hasło albo plik klucza,
  albo droga z notki nie działa → AC-5 przed prawdziwymi danymi, kiedy kopia ma jeszcze pustą bazę; (d) dane z próby zostają w telefonie obok
  prawdziwych → wyczyszczenie danych i nowa konfiguracja kopii (nowy klucz, więc notka dopiero po niej). Dane rodziny na GitHubie: z tej pozycji
  do repo idzie tylko plan, tabela, linia dziennika i numery.

### Steps
**A — paczki (`dev`)**
1. **Paczka +1 ze schematem v14:** drzewo z commita `208ba9b` (ISSUE-043 — ostatni ze schematem v14, `version: 0.9.0+1`) odtworzone **wyłącznie
   odczytem gita** (`git ls-tree -r` + `git cat-file blob`, skrypt z pliku; bez `checkout`, `worktree`, `archive`) do katalogu poza repo i
   workspace'em o krótkiej ścieżce (np. `C:\Programowanie\Grobing\_v14\` — w katalogu tymczasowym build łapie MAX_PATH). Pliki spoza gita z obecnego
   drzewa: `android/key.properties`, `android/local.properties`, `assets/places/`, wrapper Gradle. `flutter build appbundle --release`; podpis =
   klucz przesyłania (SHA-1 `36:CE:…:7E` — ISSUE-041 → *Bundle*). Starego kodu nie poprawiamy: nie buduje się → **D1-b**, bez rundy naprawy. Po
   pozycji katalog do kosza (jest w nim `key.properties`).
2. **Dziennik migawki** w obecnym kodzie: `lib/data/pre_update_snapshot.dart` — po udanej migawce jedna linia `debugPrint` (jak `GROBING_FRAME`),
   np. `GROBING_SNAPSHOT v14 -> v15 139264 B`: same wersje i rozmiar, bez ścieżki i treści. Numer `0.9.1+2` (`pubspec.yaml` i `appVersion`). Przed
   wysyłką — linia widoczna w logcat na emulatorze (build profile, baza v14 wstrzyknięta przez `run-as`, sposób z ISSUE-041 → *Emulator pass*).
   `android\gradlew --stop` po każdym buildzie.
3. Po kroku 8: numer `1.0.0+3` (tylko numer) → paczka +3. README → *Wydanie* bez zmian w treści kroków.

**B — sklep i telefon (autor; agent podaje kroki i odpowiedzi do formularzy)**
4. **Play Console** (konto Friendsheet): *Utwórz aplikację* (Grobing, polski, aplikacja, bezpłatna) → *Testy wewnętrzne* → testerzy (Twój adres) →
   *Utwórz wersję* → klucz podpisu **wygenerowany przez Google** → paczka +1 → *Rozpocznij wdrażanie*. Nazwa `com.grobing.app` zajęta → **STOP**.
   Potem *Weryfikacja deweloperów Androida*: `com.grobing.app` zarejestrowany (Friendsheet `docs/BACKLOG.md` TASK-133.3 — aplikacje ze sklepu
   rejestrują się same; klucz przesyłania rejestrować nie trzeba, bo nic nie idzie poza sklepem).
5. **Telefon:** link testera → „Zostań testerem” → instalacja +1 (Grobing z APK wcześniej → najpierw odinstalować) → 1 cmentarz z bazy, 1 grób, 2
   wymyślone osoby (rdzenie „Wymyśl-”, „Testow-”) → debugowanie USB, kabel (D2). Agent: liczby i schemat 14 w „Stanie danych”.
6. **Aktualizacja ze zmianą schematu:** paczka +2 w konsoli → *Aktualizuj* w Sklepie Play → otwarcie Grobing. Agent: `GROBING_SNAPSHOT v14 -> v15`
   w logcat, „Stan danych” — schemat 15, liczby jak w kroku 5, obie osoby na ekranie — **AC-2**.

**C — odtworzenie na telefonie**
7. Agent na `Grobing_Restore`: demo zapisane do tar (jak w ISSUE-047/048) → stan sprzed demo z `_pokaz` → build profile obecnego kodu → dopisane z
   wymyślonych rdzeni: pusty grób; osoba bez grobu z pochówkiem z „Kto leży w tym grobie?”; zdjęcie z „Zdjęć w aplikacji” u drugiej osoby; profilowe
   z kadrem ustawionym z portretu → kopia skonfigurowana z **nowym hasłem testowym** do Pobranych → odcisk i liczby zapisane → oba pliki na PC
   (katalog sesji) → demo z powrotem.
8. Agent: `adb -s <telefon> push` obu plików do Pobranych. Autor: „Stan danych” → „Odtwórz z kopii” → plik kopii, plik klucza → hasło testowe (od
   agenta). Agent: odcisk = emulator — **AC-3**. Autor poprawia jedno pole dowolnej osoby; agent po ok. 10 min: „(w tle)” w „Stanie danych” (lista A,
   wiersz 9).

**D — aktualizacja bez zmiany schematu**
9. Paczka +3 w konsoli → *Aktualizuj* → agent: odcisk i liczby jak przed aktualizacją, kopia w tle po niej przechodzi — **AC-1**.

**E — przed prawdziwymi danymi (autor; agent podaje komendy)**
10. Ustawienia → Aplikacje → Grobing → Pamięć → *Wyczyść dane*; pliki próby z Pobranych telefonu usunięte (agent przez `adb` za Twoją zgodą albo
    Ty).
11. Grobing → kopia → **Dysk Google** → **docelowe hasło — nigdy w czacie** → „Stan danych”: „Zapisana w Dysku” (lista A, wiersz 10) → pierwsza kopia
    (pusta baza albo samo „ja”).
12. **Droga z notki** (terminal VS Code, katalog poza repo; hasło wpisujesz Ty): oba pliki z Dysku → `age -d -i grobing-klucz.age grobing-kopia.age >
    kopia.tar` → `tar -xf kopia.tar -C kopia` → `dart run tool/fingerprint.dart <katalog>` w `grobing-code` → odcisk = „Stan danych” (lista A,
    wiersz 11; `backup-format.md` → *Opening a backup without Grobing*) → `age -d grobing-klucz.age` → klucz prywatny do notki → notka
    [[NT-007-hand-over-note]] na papierze → rozpakowane pliki do kosza. `age` v1.3.2 leży w katalogu sesji ISSUE-040 (`…\cbd907af-…\scratchpad\agebin\age\age.exe`).

**F — vault (`docs` przy zamknięciu):** tabela *Audit* zostaje tutaj; poprawki z audytu — [[data-model]] (Grobonet wycofany, `bio_source`
zapisywane, `is_living` nieużywane) i `backup-format.md` → *Opening a backup without Grobing* („pomiń `is_living`”); wiersze listy A — sprawdzone albo przyjęte; `CURRENT_STATE.md` (instalacja,
emulatory, katalogi do kosza, **retro 5 odłożone decyzją autora 2026-10-21**); NT-007 → *Resolution* dopiero po przekazaniu notki rodzinie (może na
wyjeździe).

### AC mapping
| AC | Jak spełnione | Dowód |
|---|---|---|
| AC-1 | kroki 4, 5, 9 | odcisk i liczby przed i po aktualizacji +2 → +3; kopia w tle po aktualizacji („Stan danych”) |
| AC-2 | kroki 1, 2, 5, 6 | logcat `GROBING_SNAPSHOT v14 -> v15`; schemat 15 i liczby jak przed |
| AC-3 | kroki 7, 8 | odcisk na telefonie = odcisk kopii z emulatora |
| AC-4 | *Audit* | tabela w tej pozycji |
| AC-5 | kroki 10–12 | „Zapisana w Dysku”; odcisk z `tool/fingerprint.dart` = „Stan danych” |

### Tests (`qa`)
- Dziennik migawki: test w `test/data/pre_update_snapshot_test.dart` — po migawce dokładnie jedna linia `GROBING_SNAPSHOT` z wersjami i rozmiarem, bez
  ścieżki (podmieniony `debugPrint`); brak migawki → brak linii.
- `settings_words_test.dart` — `appVersion` = nazwa z `pubspec.yaml` po zmianie numeru.
- Pełny `flutter test --timeout 120s`, `flutter analyze`, `dart format` (retro 4, R5).
- **Próbne odtworzenie** (DoD — warstwa danych): kroki 7–8, emulator → telefon, odcisk zgodny.
- Paczki: podpis każdej (`keytool -printcert -jarfile`) = klucz przesyłania; numer wersji w paczce 1, 2, 3.

### Manual verification
**Agent (emulator, telefon przez `adb`):** kroki 1–3 (paczki, podpis, linia dziennika na emulatorze), 5–6 (liczby, schemat, logcat), 7–9 (odcisk,
„(w tle)”, kopia po aktualizacji) — zrzuty i odczyty w *Verification*.

**Autor — kroki w ręce (lista A, nie odczucie; AC bez nich niespełnione, więc „pomiń” zostawia pozycję otwartą):**
- **przeglądarka, Play Console:** krok 4; wysyłka w krokach 6 i 9;
- **telefon:** kroki 5, 6 (aktualizacja), 8 (odtworzenie, jedna poprawka), 9 (aktualizacja), 10, 11;
- **terminal VS Code:** krok 12;
- **napisz tutaj:** po każdym kroku na telefonie — „zrobione” albo co widzisz.

**Autor — odczucie:** brak (pozycja bez nowego ekranu).

### Out of scope
Kandydaci bez zmiany bazy (wyżej) · *Before install* 6 — testy `meetsGuideline` na ekranach sprzed retro 3 (dostępność, nie dane — lista B) · lista B
*Hand checks* (w trakcie używania) · K1 — historia wersji Dysku (opcjonalne, ISSUE-041 D1) · droga powrotu z migawki (kod przyszłej poprawki) ·
ścieżka produkcyjna i wpis w sklepie (ikona 512 gotowa, gdyby konsola o nią poprosiła) · przepisywanie prawdziwych danych ([[NT-002-transcribe-the-notes]])
· przekazanie notki rodzinie (NT-007 → *Resolution*).

### Obali (falsifiers)
- `com.grobing.app` zajęta w Google Play → STOP (krok 4).
- Konsola nie wdroży testów wewnętrznych bez formularzy → lista dla autora z odpowiedziami, plan bez zmian.
- Stary kod (`208ba9b`) nie buduje się → D1-b, bez naprawy starego kodu.
- Brak `GROBING_SNAPSHOT` po kroku 6 przy linii widocznej na emulatorze (krok 2) → STOP: migawka na telefonie nie powstaje — przed prawdziwymi danymi.
- Odcisk po odtworzeniu albo po aktualizacji inny niż przed → STOP, nic prawdziwego na telefon.
- `tool/fingerprint.dart` na pliku z Dysku daje inny odcisk niż „Stan danych” albo `age` nie otwiera klucza hasłem → STOP: notka nie może powstać.

## Dev report
> `dev`, 2026-10-21. Flutter 3.41.1 (przypięty) · `flutter analyze` czyste · `dart format` bez zmian. Testów nie pisałem (`qa`). Kroki 1, 2 i 7 zrobione;
> krok 3 (`1.0.0+3`) czeka na krok 8.

### Changed (`grobing-code`)
- `lib/data/pre_update_snapshot.dart` — po udanej migawce jedna linia `debugPrint`: `GROBING_SNAPSHOT v<stara> -> v<nowa> <bajty> B` (same wersje i
  rozmiar, bez ścieżki i treści); komentarz mówi, po co (AC-2 na telefonie, gdzie prywatny katalog aplikacji jest niedostępny).
- `pubspec.yaml` — `version: 0.9.1+2`; `lib/app/settings/settings_screen.dart` — `appVersion = '0.9.1'` (D4).

### Step 1 — paczka +1 ze schematem v14
- Drzewo commita `208ba9b` (schemat 14, `version: 0.9.0+1`) w `C:\Programowanie\Grobing\_v14\` — **358 plików** z `git ls-tree -r -z` + `git cat-file blob`
  (skrypt z pliku w katalogu sesji; bez `checkout`, `worktree`, `archive`). Spoza gita skopiowane z obecnego drzewa: `android/key.properties` (ścieżka
  klucza bezwzględna, więc działa z kopii), `android/local.properties`, `android/gradlew`, `gradlew.bat`, `gradle-wrapper.jar`, `assets/places/` (Gradle
  8.14 ten sam co dziś).
- `flutter build appbundle --release` (177 s) → **56,5 MB**, podpis SHA-1 `36:CE:ED:57:…:06:7E` = klucz przesyłania. Paczka:
  **`C:\Programowanie\Grobing\_paczki\grobing-1-schemat-v14.aab`**. `gradlew --stop` po buildzie.
- `_v14\` ma w sobie `key.properties` — do kosza po pozycji (krok F).

### Step 2 — paczka +2 i linia dziennika na emulatorze
- `flutter build appbundle --release` → **60,6 MB**, ten sam podpis → **`C:\Programowanie\Grobing\_paczki\grobing-2-schemat-v15.aab`**.
- `Grobing_Restore`: demo zapisane (APK i tar danych w katalogu sesji, `emu032\`) → build profile `0.9.1` (`versionCode` 4002) → dane sprzed demo z `_pokaz`
  → `files/grobing.db` zastąpiona migawką v14, którą ten stan już miał (`files/pre-update/grobing-v14.db`, z migracji ISSUE-044) → start →
  **`I flutter : GROBING_SNAPSHOT v14 -> v15 147456 B`** w logcat; `pre-update/grobing-v14.db` zapisana na nowo w chwili startu. Build profile jest AOT
  jak release, więc linia przejdzie i w paczce ze sklepu.

### Step 7 — kopia wymyślonej rodziny do odtworzenia na telefonie
- Stan sprzed demo z `_pokaz` (czysty, v15) + build profile `0.9.1`. Dopisane przez interfejs, z wymyślonych rdzeni:
  - pusty grób „Pusty grob Testowy” („Nowy grób”, bez osób);
  - grób „Grob Testowy z wyboru” z osobą bez grobu dołączoną z „Kto leży w tym grobie?”;
  - zdjęcie innej wymyślonej osoby dołączone z „Zdjęć w aplikacji” — jedno zdjęcie u dwóch osób;
  - kadr profilowego zmieniony z portretu (podwójne dotknięcie i przesunięcie) — kadr leży na łączu tego wspólnego zdjęcia.
- Liczby w bazie (kopia na hoście, potem usunięta): schemat 15 · osoby 109 (106 bez pochówku) · groby 4 (1 bez osób) · pochówki 3 · zdjęcia 9, łącza 10 (1
  zdjęcie u 2 osób, 1 łącze z kadrem) · rody 13 (13 osób z rodem) · zamieszkania 61 · groby z datą opłaty 1 · cmentarze 1. W tym stanie są wpisy
  autora z emulatora (D3) — tu tylko liczby.
- „Skonfiguruj kopię od nowa” z **nowym hasłem testowym** (13 znaków, kropki policzone na zrzucie; hasło dostaje autor na stopie #2, w vaulcie go nie ma)
  → Pobrane: `grobing-klucz-032.age` (366 B) i `grobing-kopia-032.age` (363 800 B), kopia 15:13 UTC. **Odcisk `c52cb50f42471378`**, schemat 15.
- Sprawdzone na PC przed telefonem: `age` + `age-plugin-batchpass` (hasło testowe) → klucz → `age -d -i` → `tar` → `dart run tool/fingerprint.dart` —
  odcisk, schemat, liczby i 10 plików zgodne z manifestem. Rozpakowane pliki usunięte. Oba pliki `.age` w katalogu sesji (`emu032\`), do `adb push` w kroku 8.
- `Grobing_Restore` — **demo z powrotem** (APK `0.9.0`, 4001, i dane zapisane przed pozycją; 41 osób na liście). Emulator wyłączony.

### Step 3 — paczka +3 (2026-10-22, po kroku 8)
- `pubspec.yaml` — `version: 1.0.0+3`; `appVersion = '1.0.0'` (`settings_words_test.dart` zielony). `flutter build appbundle --release` → 60,6 MB, ten sam
  podpis → `C:\Programowanie\Grobing\_paczki\grobing-3-wersja-1.0.0.aab`. **Na tej wersji zaczynają się prawdziwe dane.**

### Deviations
- Brak w kodzie. **Uwaga do listy A, wiersz 10** („rozpoznanie Dysk Google”): „Stan danych” pisze „Zapisana w Dysku na telefonie” także przy kopii w
  Pobranych (znane, `CURRENT_STATE.md` → ISSUE-022 B6 — widać to na emulatorze w tym przejściu). Dowodem jest wiersz w Ustawieniach: „Ostatnia udana kopia
  … · **Dysk Google**” (`settings_screen.dart:43` rozpoznaje dostawcę po adresie pliku; przy Pobranych pisze „· Pobrane”).

### For `qa`
- Testy z planu (*Tests*): linia `GROBING_SNAPSHOT` (podmieniony `debugPrint`), `settings_words_test.dart` przy `0.9.1`, pełny przebieg.
- Stop #2: kroki 4–12 z autorem według planu. Telefon i emulator naraz → każda komenda `adb` z `-s <numer telefonu>`; **żadnego `adb install` na
  telefon**. Krok 8: `adb -s <telefon> push` obu plików `*-032.age` do `/sdcard/Download/`, hasło testowe autorowi w czacie, oczekiwany odcisk
  `c52cb50f42471378`. Krok 3 (`1.0.0+3` w `pubspec.yaml` i `appVersion`, paczka) — dopiero po kroku 8.
- Release na telefonie nie daje `run-as`: liczby i odcisk z „Stanu danych” (`uiautomator dump`, zrzut), migawka z logcat.

## Verification
> `qa`, 2026-10-21 – 2026-10-22. Pozycja bez nowego ekranu — bez przeglądu `ui`. Stop #2 = kroki autora 4–12 (lista A) w pięciu częściach, telefon
> autora na kablu (D2), odczyt przez `uiautomator dump`, zrzuty i logcat; **żadnej instalacji przez `adb`** — każda wersja ze Sklepu Play
> (`installerPackageName=com.android.vending`).
>
> **Werdykt: APPROVED (self-check, z uwagami)** — AC-1, AC-2, AC-3, AC-4 spełnione dowodami niżej; AC-5 w części: dane wyczyszczone i kopia na Dysku tak,
> droga z notki **odłożona decyzją autora** do [[NT-007-hand-over-note]] (autor: *„na razie nie chcę tego robić — tamte działały, więc dlaczego to nowe ma
> nie działać”*). Uwagi niżej.

### Stop #2 — on the phone (Motorola moto g82 5G, Android 13)
| Krok | Wynik | Dowód |
|---|---|---|
| 4 — Play Console | aplikacja utworzona, **`com.grobing.app` wolna i zarezerwowana**; testy wewnętrzne, klucz od Google; wersja 1 (0.9.0) „Dostępna dla testerów wewnętrznych” 2026-10-21 22:58 | zrzuty konsoli od autora |
| 5 — instalacja +1 | link testera dał „nie znaleziono elementu” przez ok. 30 min (pierwsze wdrożenie nowej aplikacji — Pomoc Play: link może działać po kilku godzinach); potem instalacja; `versionCode` 1, ze sklepu. Autor wpisał wymyślone osoby: schemat **14**, osoby 3, groby 2, pochówki 3, cmentarze 2, zdarzenia 6 | `dumpsys package`, „Stan danych” |
| 6 — aktualizacja +2 (v14 → v15) | **`I flutter : GROBING_SNAPSHOT v14 -> v15 135168 B`** 2026-10-22 10:51:19; „Stan danych”: schemat **15**, osoby 3, zdarzenia 6, cmentarze 2, plany 2, groby 2, pochówki 3, twierdzenia 9 — bez zmian; rody 0 (nowa tabela) — **AC-2** | logcat, „Stan danych” |
| 8 — odtworzenie kopii z emulatora | pliki `*-032.age` przez `adb push`; „Odtwórz z kopii” z hasłem testowym → odcisk **`c52cb50f42471378`** = emulator; osoby 109, rodziny 38, zdarzenia 180, groby 4, pochówki 3, zdjęcia 9, łącza 10, zamieszkania 61, rody 13 — **AC-3** (lista A: odtworzenie po starcie z migawką, pusty grób i pochówek z wyboru, zdjęcie u dwóch osób z kadrem, v15 z rodami, data opłaty, zamieszkania) | „Stan danych” |
| 8 — kopia w tle | po zmianie jednego pola: „Ostatnia udana kopia 2026-10-22 11:13 **(w tle)**” | „Stan danych”, czas pliku w Pobranych |
| 9 — aktualizacja +3 (1.0.0) | przed: odcisk `1c8700b3f6ed931e` (autor dodał cmentarz); po: **ten sam odcisk**, te same liczby, „Grobing 1.0.0”; zmiana po aktualizacji (zamieszkanie) → plik kopii nadpisany sam o 12:38 — **AC-1** | „Stan danych”, `dumpsys package`, czas pliku |
| 10 — wyczyszczenie | dane aplikacji wyczyszczone (osoby 0, bez „ja”); pliki próby `*-032.age` usunięte z Pobranych telefonu przez `adb` | „Stan danych”, `ls` |
| 11 — kopia docelowa | „Ostatnia udana kopia — dziś, 13:31 · **Dysk Google**” (wiersz w Ustawieniach; „Stan danych” pisze „Zapisana w Dysku” zawsze — znane B6); pusta baza: odcisk `dff49ae6db482714`, schemat 15 | Ustawienia, „Stan danych” |
| 12 — droga z notki | **nie wykonane — decyzja autora**: mechanizm (age → tar → odcisk) przeszedł dziś na kopii próbnej z emulatora, a odtworzenie na telefonie tą samą drogą; niesprawdzone zostaje, czy hasło na kartce = hasło wpisane w telefonie i czy oba pliki są na Dysku. Przeniesione do [[NT-007-hand-over-note]] razem z komendami (*Steps* 12); `age.exe` czeka w `C:\Programowanie\Grobing\_notka\` | — |

### Notes
- **D1 zadziałało:** migawka na telefonie z wersji ze sklepu jest udowodniona, nie przyjęta.
- **Pierwsze wdrożenie** w testach wewnętrznych potrzebowało ok. 30 min, zanim sklep dał instalację; kolejne wersje — kilka minut (wersja 3 po „Rozpocznij
  wdrażanie” także po kilku minutach i „Sprawdź dostępność aktualizacji”).
- **„Stan danych” pisze „Zapisana w Dysku na telefonie” przy kopii w Pobranych** — potwierdzone na telefonie (B6 w `CURRENT_STATE.md`); Ustawienia mówią
  prawdę („· Pobrane” / „· Dysk Google”).
- Na telefonie jest teraz wersja **1.0.0** z pustą bazą i kopią na Dysku — gotowa na prawdziwe dane. Debugowanie USB autor może wyłączyć.

### For ISSUE-032 → Hand checks (A)
- **A** — kopia docelowa otwiera się hasłem z kartki i plikiem klucza z Dysku (krok 12) — **odłożone decyzją autora** do [[NT-007-hand-over-note]]; do
  czasu sprawdzenia: zgubione albo źle zapisane hasło = kopia, której nie da się otworzyć.
- Pozostałe wiersze listy A — sprawdzone wyżej (kroki 5–11).

### Automated
- **Nowy test** w `test/data/pre_update_snapshot_test.dart` (ISSUE-032, AC-2 na telefonie): po migawce dokładnie jedna linia
  `GROBING_SNAPSHOT v11 -> v15 <rozmiar migawki> B`, bez ścieżki katalogu i bez `pre-update`; brak migawki (brak bazy) → brak linii.
- `settings_words_test.dart` zielony przy `0.9.1` (nazwa w `pubspec.yaml` = `appVersion`).
- **Pełny `flutter test --timeout 120s`: 990 zielonych** (989 + 1), bez zawieszenia; `flutter analyze` czyste; `dart format` — 0 zmian.

### Family data in the changes
- Kod i test: przykłady tylko z rdzeni wymyślonych („Wymyślony”, „Zmyślonych”, „Testowy”); linia dziennika ma same wersje i rozmiar. Vault: tabela
  audytu, plan i raport bez imion, miejsc i nazw cmentarzy — wpisy autora z emulatora opisane liczbami. Strażnik treści (próba `git add` na sucho):
  `grobing-code` (4 pliki) i `grobing-vault` (pozycja, macierz) — przechodzą.
- Kopie `*-032.age`, zrzuty i stan emulatora tylko w katalogu sesji; paczki `.aab` i drzewo `_v14\` w `C:\Programowanie\Grobing\` poza repo.
