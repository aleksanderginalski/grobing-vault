---
title: "ISSUE-032 — MVP install on the author's phone: data-model audit, hand checks, conditions before the first real data"
type: issue
status: draft
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[2026-10-13-retro-03]] R8, R9 · `CURRENT_STATE.md` → *Droga do instalacji MVP* (ostatni krok bez pozycji)"
created: 2026-10-13
updated: 2026-10-16
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
0. **[[ISSUE-041-google-play-and-safe-update]] zamknięte** — aplikacja w sklepie, próba aktualizacji na wymyślonych danych przeszła (lista A niżej);
1. **Audyt pól modelu ↔ ekrany** (retro 3, R9): każde pole [[data-model]] ma ekran, który je zapisuje, albo jawne „nie zapisuje go
   żaden ekran, bo…”. Powód: adres kwatery (M1) miał kolumny od v1, a ekran dopiero w [[ISSUE-028-cemetery-sectors]]. Robi agent;
   wynik to tabela w tej pozycji. Znani kandydaci: `is_living` ([[ISSUE-040-export-is-the-backup]] → *Notes*) i `grobonetUrl` (link wycofany —
   [[cmentarz]] D12; zauważone w `/pm` 2026-10-16);
2. ~~**klucz wydania** (`.jks` i oba hasła) w zaszyfrowanym miejscu~~ — **po [[ISSUE-041-google-play-and-safe-update]] nie blokuje** ([[2026-10-16-retro-04]]):
   klucz podpisu trzyma Google, a obecny klucz wydania zostaje kluczem przesyłania, który da się zresetować. Kopia dalej wskazana;
3. **notka przekazania** sprawdzona jej własną drogą — [[NT-007-hand-over-note]];
4. **dane aplikacji wyczyszczone** po próbie aktualizacji z [[ISSUE-041-google-play-and-safe-update]] (wymyślone dane) — Ustawienia → Aplikacje →
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
- instalacja ze sklepu i aktualizacja tą samą drogą — wymyślone dane i kopia bez zmian ([[ISSUE-041-google-play-and-safe-update]] AC-1, próba
  generalna);
- kopia sprzed aktualizacji istnieje i odtworzenie ją przyjmuje ([[ISSUE-041-google-play-and-safe-update]] AC-2);
- po zmianie danych pojawia się „(w tle)” — w AOT sprawdzał to tylko build profile ([[ISSUE-010-background-backup]]);
- rozpoznanie „Dysk Google” w wierszu kopii — tylko test ([[ISSUE-022-app-skeleton-tabs-people-settings]]);
- kopia z telefonu otwiera się drogą z notki przekazania ([[NT-007-hand-over-note]]) albo odtwarza na emulatorze ([[NFR-002-odtworzenie-na-nowym-telefonie]]).

### B — odczucie (w trakcie używania, bez bramki)

**Zdjęcia**
- zdjęcie HEIF z telefonu — emulator ich nie robi ([[ISSUE-016-photos-grave-and-person]]);
- okno wyboru oddaje zdjęcia w kolejności zaznaczania — sprawdzone tylko na Androidzie 16 ([[ISSUE-017-person-photos]]);
- nieocenione w ręce: „Ustaw jako profilowe”, siatka i okrąg, zapis zdjęć przez „Zapisz”, lista „Kto jest na zdjęciu?”
  ([[ISSUE-017-person-photos]]);
- kadr profilowego: podwójne dotknięcie i ok. 0,3 s czekania przy pojedynczym; pamięć okręgów z małym kadrem
  ([[ISSUE-018-profile-photo-crop]], [[ADR-010-profile-photo-crop-pixels]] → *Follow-ups*).

**Osoby i rodzina**
- tło z pasma w widoku osoby — „pomiń” ([[ISSUE-024-person-view]], krok 3 rundy 2); TalkBack w widoku osoby, ekran 360 dp;
- TalkBack i tekst 200% w kreatorze związku ([[ISSUE-025-gender-kinship-together-since]]);
- TalkBack i duże powiększenie tekstu na Osobach i w ustawieniach ([[ISSUE-022-app-skeleton-tabs-people-settings]]).

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
- progi S2 (oddalanie odsłania dalszą rodzinę) przy szczypaniu palcami — nieprzetestowane na żywo, na emulatorze tylko przyciski i mysz
  ([[SPIKE-002-tree-on-a-phone]]);
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

**Do decyzji autora, gdy zobaczy swoje cmentarze** (nie sprawdzenie, tylko wybór): grubość alejek i znicze, które nachodzą na
siebie ([[cmentarz]] → *Open*, [[ISSUE-030-sector-on-a-visit]]).

## Notes / references
- [[2026-10-13-retro-03]] R8, R9 · `DEFINITION_OF_DONE.md` → *Kto sprawdza* · wyjątki „na telefonie” w DoD (GPS, słońce,
  offline — build release).
