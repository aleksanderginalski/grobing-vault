---
title: "ISSUE-033 — Tree from a person: an invented family of 106 in the debug build, own layout, levels by zooming out (S2), trace of the wider family, the centre card with kinship names, „Pokaż w drzewie”, text at 200%"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-009-drzewo-od-osoby]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-13
verdict-reviewer: self-check
source: "rozpisanie US-009 (`docs` w auto-flow po `pm` i `ui`, autor: „ok”, 2026-10-13) · US-009 AC-1–AC-7 · [[drzewo]] v1.5 (elementy 1, 3–5; D12–D15, D17–D20; *Open* 5, 6) · [[osoba]] v2.4 (element 6, D11) · [[SPIKE-002-tree-on-a-phone]] → *Findings*, *Rekomendacja* · [[ISSUE-025-gender-kinship-together-since]] D2"
created: 2026-10-13
updated: 2026-10-13
---

# ISSUE-033 — Drzewo od osoby

> Z rozpisania [[US-009-drzewo-od-osoby]] (`docs` w auto-flow, 2026-10-13, po `pm` i `ui`). **Dwie pozycje:** ta buduje drzewo
> (AC-1–AC-7), a [[ISSUE-034-tree-presentation-mode]] dokłada tryb prezentacji (AC-8). US na to pozwala (*„Może wyjść do osobnej pozycji
> przy planowaniu”*), a SPIKE-002 → *Rekomendacja* pkt 4 to przewidział: „w 1. albo osobno, gdy 1. urośnie”. Urosła: słownik z opisem z
> odcinków, imiona przy oddalaniu, tekst 200% i stany. Podział zaproponował łańcuch, nie autor, więc na stopie #1 autor może go zmienić.

## What to build
1. **Wymyślona rodzina o kształcie prawdziwej** w buildzie debug (`lib/dev/`, SPIKE-002 D6) — **pierwszy krok pozycji**. Kształt (same
   liczby, SPIKE-002 → *Rekomendacja*): 106 osób, 38 związków, 6 pokoleń (roczniki 1868–2019), 31 zmarłych i 75 żyjących, 39 osób bez
   rodziców w danych, 3 osoby w dwóch związkach (wdowiec, wdowa, rozwód), 2 pary „razem” (jedna potem ze ślubem), rodzina żony w 3
   pokoleniach z jej kuzynami. Nazwiska tylko z wymyślonych rdzeni (`family-data.md`, retro 3 R7).
2. **Układ drzewa** — własny, port algorytmu makiety (SPIKE-002 M1: liczby identyczne z makietą), bez nowej zależności: rzędy według
   pokolenia, para jako blok, rodzina partnera z boku, kolejność w rzędzie według środków ciężkości, położenie z regresji izotonicznej.
   **Poziomy** według [[drzewo]] D2.
3. **Ekran „Drzewo”** zamiast zaślepki zakładki ([[drzewo]] elementy 1, 3, 4, 5): S2 z wartościami z D18, ślad dalszej rodziny (D9),
   przestawianie środka z animacją, „Ja” ze znakiem „Ja” (D14), imiona przy oddalaniu (*Open* 5), czytnik.
4. **Nazwa pokrewieństwa w karcie** ([[drzewo]] element 5): słownik ze źródłem ([[ISSUE-025-gender-kinship-together-since]] D2) z
   nawiasem (D13), dalej opis z odcinków liczony od drugiej osoby (D12), z dopełniaczem; kto mówi — *Open* 6.
5. **„Pokaż w drzewie”** w widoku osoby ([[osoba]] v2.4, element 6, D11) → zakładka Drzewo z tą osobą w środku ([[drzewo]] D15).
6. **Tekst 200%** (AC-7, D20) i **stany** ([[drzewo]] *States*: bez „ja”, pusta baza, osoba bez rodziny, osoba spoza rodziny „ja”, błąd
   odczytu — D19).
7. **Przejście między poziomami bez szarpania** (SPIKE-002 M3: do 55% wolnych klatek na emulatorze) — wejścia z *Findings*: linie z pamięci
   podręcznej w czasie animacji, przerywane bez `computeMetrics` w każdej klatce, mniej cieni, przeliczenie poza klatką animacji.

## Acceptance Criteria
- [ ] **US-009 AC-1 — od „Ja”.** *When* otwieram zakładkę „Drzewo” *Then* w środku stoi „Ja” na poziomie 2: rodzice, partner, dzieci,
      rodzeństwo, dziadkowie, rodzina partnera po prawej; rzędy według pokolenia, linie według rodzaju relacji ([[drzewo]] element 4).
- [ ] **US-009 AC-2 — przestawianie środka.** *When* dotykam osobę *Then* ona staje w środku z animacją, a karta pokazuje imię, lata i kim
      jest dla mnie; dotknięcie osoby w środku albo „Pokaż” → [[osoba]].
- [ ] **US-009 AC-3 — dalsza rodzina (S2).** *When* oddalam (dwa palce albo przycisk −) *Then* drzewo dokłada kolejny poziom (4 progi) i na
      chwilę pokazuje „Poziom N · M osób”; przybliżanie (dwa palce, podwójne dotknięcie albo +) zabiera dalszą rodzinę.
- [ ] **US-009 AC-4 — ślad dalszej rodziny.** *Given* osoba ma rodzinę poza widokiem *Then* przy niej jest krótka, blada, przerywana
      kreska: w górę rodzice, w dół dzieci, w bok partner.
- [ ] **US-009 AC-5 — nazwa pokrewieństwa w karcie.** *Given* ścieżka Ja → tata → jego rodzic → jego córka *Then* karta mówi „ciotka”; brat
      ojca — „stryj”, brat matki — „wuj”; dziecko siostry ojca — „brat/siostra cioteczna”; dalsze pokrewieństwo — opis z odcinków
      („Siostra cioteczna babci Twojej żony” — G1, stop #1).
- [ ] **US-009 AC-6 — „Pokaż w drzewie”.** *When* w widoku osoby dotykam „Pokaż w drzewie” *Then* drzewo otwiera się z tą osobą w środku.
- [ ] **US-009 AC-7 — tekst 200% na 360 dp.** Imiona nie są ucięte tak, że mylą osoby (miejsce osoby rośnie z tekstem jak w mini-drzewie,
      najwyżej 160 dp), inicjały mieszczą się w okręgu.
- [ ] Zaślepka zakładki Drzewo (`tree_placeholder_screen.dart`) znika razem z prawdziwym ekranem ([[style-b]] reguła 12).

## Out of scope
- Tryb prezentacji (AC-8, [[drzewo]] element 11, D16) i ikona telewizora w pasku → [[ISSUE-034-tree-presentation-mode]].
- Czas na drzewie (element 6) → [[US-010-czas-na-drzewie]]; „Połącz dwie osoby” (elementy 7–10, ikona w pasku) → [[US-011-polacz-dwie-osoby]].
- Całe drzewo naraz (K1) — nie w MVP ([[drzewo]] D1).
- Kontrola cykli w rodzinie ([[ISSUE-019-family-relations]] → *Manual*) — drzewo musi się przy cyklu nie zawiesić, ale go nie zgłasza.
- Na fizycznym telefonie: zadanie „kim jest X dla mnie” < 30 s, płynność, progi S2 w ręce → [[ISSUE-032-mvp-install]] → *Hand checks*
  (wiersze ze SPIKE-002).

## Notes
- **D12 zmienia regułę z [[ISSUE-025-gender-kinship-together-since]] D2:** odcinki liczone od drugiej osoby, nie od „ja” — inaczej przykład z
  AC-5 wychodzi jako „Siostrzenica babci Twojej teściowej”. Słownik i nawiasy bez zmian. Przy G1 (*Open* 6) przykład w AC-5 US-009 („mojej
  żony”) do poprawy.
- **Dziś w kodzie:** ścieżka między osobami (`lib/data/kinship.dart`, `KinGraph`, ISSUE-024) i słowa jednego kroku (`lib/app/person/
  kinship_names.dart`). Nazw złożonych i dopełniacza nie ma. Mini-drzewo (`lib/app/person/mini_tree.dart`) ma regułę miejsca osoby przy
  tekście 200%, a `InitialsCircle` — limit 1,3×.
- **Wejścia z SPIKE-002 *Findings*:** skala S2 z osi x, a nie z `getMaxScaleOnAxis()` (oś z psuła zmianę poziomu); pierwsza klatka na
  Androidzie ma rozmiar bliski zeru, więc ustawienie środka czeka na prawdziwy rozmiar; przeliczenie układu przy 106 osobach do 15 ms.
- **Makiety:** `drzewo-us009.html` (kandydaci *Open* 5 i 6, karta, stany, tekst 200%; self-test `#test=1`) i `drzewo-spike002.html` (algorytm
  układu, rodzina) w katalogach tymczasowych sesji ([[drzewo]] → *mockup*).
- **Emulatory** (`CURRENT_STATE.md` → *In progress*): `Medium_Phone` ma release v12 z danymi testowymi autora. Wymyślona rodzina wchodzi
  tylko w buildzie debug — jak ją położyć obok, nie kasując danych autora, ustala plan.
- Przy tej pozycji: pozycja z ekranem, więc przegląd `ui` przed stopem #2 i testy `meetsGuideline` (retro 3, R2).

## Implementation plan
> `planning`, 2026-10-13. Specyfikacja (`ui`, przed planem): [[drzewo]] v1.5 — elementy 1, 3, 4, 5, *States*, D9, D12–D15, D17–D20,
> *Open* 5 i 6; [[osoba]] v2.4 — element 6, D11; [[style-b]] v1.24. Makieta: `drzewo-us009.html` (katalog tymczasowy sesji `c3868f5f-…`;
> sekcje 1–6, self-test `#test=1`). **Kandydaci tego, co widać** (retro 2, R6): I1–I3 i G1–G2 działają na makiecie (przełączniki w
> sekcjach 1 i 2), przed rekomendacją.

### Prior art (źródła, nie pamięć)
- **Układ i poziomy:** [[SPIKE-002-tree-on-a-phone]] → *Findings* M1 (port makiety daje te same liczby: 6 → 20 → 66 → 99 osób, 0/0/6/9
  skrzyżowań, przeliczenie do 15 ms przy 106 osobach) i M2 (`graphview` przegrywa w każdej mierze — bez nowej zależności, bez ADR).
  Kanon „rodzina to krata, pokazuje się wycinek według zainteresowania”: [[drzewo]] D8 (TimeNets, AVI 2010).
- **Płynność:** SPIKE-002 M3 — przesuwanie płynne (≤ 1,3% wolnych klatek), przejście między poziomami do 55% wolnych klatek; wąskie
  gardło to rasteryzacja (linie przerywane liczone co klatkę, cienie, wszystkie węzły na nowo).
- **Słownik:** [[ISSUE-025-gender-kinship-together-since]] → *Prior art* (SJPD przez Frąckiewicz 2013, SJP PWN) i D2 (tabela nazw, nawiasy,
  odcinki neutralne). Dopełniacz każdej nazwy `dev` sprawdza w [SJP PWN](https://sjp.pwn.pl) (odmiana), nie z pamięci — lista form w *Dev
  report*.
- **Z kodu** (ankieta 2026-10-13): `KinGraph` (`lib/data/kinship.dart`) zna krawędzie rodzic, dziecko, rodzeństwo (dzieci tej samej
  rodziny) i partner z flagą ślubu, a `path()` daje najkrótszą ścieżkę (ISSUE-025 D2). Słowa jednego kroku są w `kinship_names.dart`, a nazw
  złożonych i dopełniacza nie ma. Związki to `families` + `family_partners` + `family_children`, a ślub i „razem” to zdarzenia rodziny
  (`EventType.marriage`, `together`). „Ja” to `settings.mePersonId`. Zakładki przełącza `openTab` (`lib/app/tabs.dart`). Wymyślone dane
  dodają przyciski w „Stanie danych” za `kDebugMode`. Build profile dziedziczy podpis debug (`android/app/build.gradle.kts`: klucz wydania
  ma tylko `release`).

### Stop #1 (2026-10-13) — autor: „Tak”
Rekomendacja przyjęta w całości: D1 = **I2** (imiona zostają czytelne, nakładające się chowają), D2 = **G1** („Twoja babcia”), D3 (dwie
pozycje — ISSUE-034 po tej), D4 (odcinki od drugiej osoby), D5 (`Grobing_Restore` z buildem profile; `Medium_Phone` nietknięty), D6
(wymyślone dane za `!kReleaseMode`). Decyzje projektowe [[drzewo]] D13–D20 i [[osoba]] D11 v2.4 potwierdzone. Specyfikacja → [[drzewo]] v1.6,
[[style-b]] v1.25; przykład w AC-5 US-009 → „Twojej żony”.

### Decisions for stop #1 (rekomendacja → „tak” przyjmuje wszystkie)
- **D1 — imiona przy oddalaniu ([[drzewo]] *Open* 5):** I1 · **I2 (rekomendacja)** · I3 — makieta, sekcja 1, przyciski „Poziom 3” i
  „Poziom 4”. Przy I2 na poziomie 4 widać 63 z 99 imion w 13 sp, przy I1 — 99 imion w ok. 6 sp, przy I3 — jedno. *Obali I2:* miganie imion
  przy szczypaniu na emulatorze przeszkadza — wtedy I3 (zamiana jednej funkcji, układ bez zmian).
- **D2 — kto mówi w karcie ([[drzewo]] *Open* 6):** **G1 „Twoja babcia” (rekomendacja)** · G2 „Moja babcia” — makieta, sekcja 2. Przy G1
  `docs` poprawia przykład w AC-5 US-009 („…babci Twojej żony”).
- **D3 — dwie pozycje:** ta (AC-1–AC-7) i [[ISSUE-034-tree-presentation-mode]] (AC-8, po tej). Alternatywa: jedna pozycja na całą US — wtedy
  tryb prezentacji dochodzi tutaj jako krok 9 i ok. 1/6 więcej pracy przed stopem #2.
- **D4 — odcinki od drugiej osoby ([[drzewo]] D12)** zamiast „od „ja”” z ISSUE-025 D2 — tylko tak przykład z AC-5 wychodzi jako „Siostra
  cioteczna babci … żony”. Testy z obu przykładów (AC-5 i „Siostra cioteczna Twojego dziadka”).
- **D5 — gdzie stoi wymyślona rodzina:** build profile (AOT, płynność jak w release) na `Grobing_Restore`. **Odinstalowanie releasu na
  `Grobing_Restore` kasuje tam dane z kopii `-029`** — to kopia, nie nic unikalnego, a następna pozycja z kopią i tak bierze nowe hasło
  (`CURRENT_STATE.md` → *Emulatory*). `Medium_Phone` z Twoimi danymi testowymi i releasem v12 zostaje nietknięty. Alternatywa: nowy AVD
  (kilka GB na dysku, jeden emulator naraz — RAM).
- **D6 — wymyślone dane za `!kReleaseMode` zamiast `kDebugMode`** (przyciski w „Stanie danych”): widać je w debug i w profile, nigdy w
  release — `kReleaseMode` jest stałą, więc kod za nią wypada z buildu release jak dotąd. Po co: pomiar klatki i Twoje odczucie płynności na
  buildzie AOT, a nie na debug, który na emulatorze szarpie sam z siebie. Zmienia ISSUE-007 D3 tylko w tym, w którym buildzie widać przyciski.
- Decyzje projektowe ze specyfikacji, które „tak” też przyjmuje: [[drzewo]] D13 (nawias w karcie), D14 (znak „Ja”), D15 (zakładka zawsze od
  „Ja”, „Pokaż w drzewie” przełącza zakładkę, wstecz nie cofa środka), D17 (cel dotyku na poziomie 4: 38–32 dp, wyjątek w [[style-b]]), D18
  (progi S2 z prototypu), D19 (stany bez „ja” i pustej bazy), D20 (tekst 200% w karcie); [[osoba]] D11 v2.4.

### Scope — files (`{code}`)
| Plik | Zmiana |
|---|---|
| `lib/dev/fictional_family.dart` (nowy) | `addFictionalFamily(db)` — rodzina z makiety (106 osób, 38 związków; te same rdzenie), przez istniejące zapisy (`saveFamily`, zdarzenia ślubu i „razem” z datą). Ustawia „ja” tylko wtedy, gdy nie jest ustawione. Drugie wywołanie nie dubluje (sprawdza znacznik partii jak `addFictionalData`) |
| `lib/app/data_state_screen.dart` | przycisk „Dodaj wymyśloną rodzinę (drzewo)”; przyciski wymyślonych danych za `!kReleaseMode` (D6) |
| `lib/data/family_tree.dart` (nowy) | odczyt dla drzewa jednym strumieniem (`watchTables` jak `person_view`): osoby (imiona, nazwisko, z d., płeć, lata, zmarły), związki (partnerzy w kolejności pierwszej daty związku, dzieci według urodzenia, ślub / razem), „ja”, profilowe. **Tylko odczyt** |
| `lib/app/tree/tree_layout.dart` (nowy) | czysty Dart: poziomy według D2 (`levelsFrom`), port układu z makiety (rzędy, bloki par, środki ciężkości, regresja izotoniczna), linie (para, rodzic–dziecko z szynami), ślad (D9); miejsce osoby i wysokość rzędu z parametru (tekst systemu, D20) |
| `lib/app/tree/tree_labels.dart` (nowy) | imiona przy oddalaniu według D1 — przy I2: rozmiar ≥ 13 sp × skala tekstu, kolejność bliskości (poziom, potem odległość w poziomie od środka), chowanie nakładających się; czysta funkcja |
| `lib/app/tree/tree_screen.dart` (nowy) | ekran: pasek (element 1 bez ikon US-010/011 i bez telewizora — ISSUE-034), obszar drzewa z przesuwaniem i S2 (skala z osi x, D18; podwójne dotknięcie pustego miejsca; + / −; pigułka + ogłoszenie dla czytnika), przestawianie środka z animacją ok. 0,45 s (bez animacji przy `MediaQuery.disableAnimations`), karta (element 5), stany (D19), czytnik (element 4) |
| `lib/app/tree/tree_painter.dart` (nowy) | linie i ślad w `CustomPainter`; ścieżki liczone raz na układ (nie w każdej klatce), linie przerywane bez `computeMetrics` co klatkę, osobny `RepaintBoundary` dla linii i węzłów (SPIKE-002 M3) |
| `lib/app/person/kinship_names.dart` | `kinshipName(...)`: słownik ISSUE-025 D2 z nawiasem (D13), odcinki od drugiej osoby (D4/D12), dopełniacz, zaimek według D2 (G1/G2), odcinki neutralne bez płci |
| `lib/app/tabs.dart` | `openTab(..., AppTab.tree, focusPersonId:)`; zakładka zawsze od „ja” (D15); `TreeScreen` zamiast zaślepki |
| `lib/app/tree/tree_placeholder_screen.dart` | **usunięty** |
| `lib/app/person/person_screen.dart` | „Pokaż w drzewie” pod mini-drzewem, gdy osoba ma rodzinę ([[osoba]] element 6) |

Testy (pisze `qa`): `test/app/tree/tree_layout_test.dart`, `tree_labels_test.dart`, `tree_screen_test.dart`, `test/app/person/kinship_names_test.dart`
(rozszerzony), `test/dev/fictional_family_test.dart`, `test/data/family_tree_test.dart`.

### AC → implementation → test (testy pisze `qa`)
| AC | Implementacja | Test happy-path |
|---|---|---|
| AC-1 — od „Ja” | `tabs.dart` → `TreeScreen` od `mePersonId`, poziom 2, skala 1; `tree_layout` (poziomy D2, rodzina partnera z boku) | `tree_screen_test`: wymyślona rodzina → „Ja” w środku z pierścieniem, 20 osób; `tree_layout_test`: poziomy 6/20/66/99, każda para obok siebie, rodzina żony po prawej |
| AC-2 — przestawianie środka | dotknięcie węzła → nowy układ od tej osoby, animacja; drugie dotknięcie / „Pokaż” → widok osoby, zakładka Drzewo | dotknięcie żony → karta „ur. 1985 · Twoja żona”; „Pokaż” → `PersonScreen` z aktywną zakładką Drzewo |
| AC-3 — dalsza rodzina (S2) | progi 1,3 · 0,85 · 0,55, skala 0,4–2,0, krok 1,45 (D18) | − → „Poziom 3 · 66 osób” i 66 węzłów; + → poziom 2; podwójne dotknięcie pustego miejsca → przybliżenie |
| AC-4 — ślad | `tree_layout` → ślad dla osób z rodziną poza widokiem | układ poziomu 1: ślady w górę, w dół i w bok tam, gdzie rodzina jest poza widokiem; żadnego przy osobie bez dalszej rodziny |
| AC-5 — nazwa pokrewieństwa | `kinship_names.dart` | ciotka (siostra taty), stryj (brat taty), wuj (brat mamy), siostra cioteczna (córka siostry taty), „Siostra cioteczna babci Twojej żony” (D4), „Siostra cioteczna Twojego dziadka”, „Bratowa Twojej żony”, „Partnerka Twojego brata” („razem”), odcinek bez płci — neutralny |
| AC-6 — „Pokaż w drzewie” | `person_screen.dart` → `openTab(tree, focusPersonId)` | widok osoby z rodziną → przycisk → drzewo z tą osobą w środku; osoba bez rodziny — przycisku nie ma |
| AC-7 — tekst 200% na 360 dp | miejsce osoby 80 dp × skala tekstu (≤ 160 dp), rząd 104 → 124 dp, inicjały ≤ 1,3×, „Pokaż ›” pod tekstem przy ≥ 150% | `textScaler: 2.0`, ekran 360 dp: imię bez „…” w 160 dp, inicjały w okręgu; `meetsGuideline(androidTapTargetGuideline)` i `labeledTapTargetGuideline` na drzewie przy skali 1 (retro 3, R2) |
| zaślepka znika | `tree_placeholder_screen.dart` usunięty | `skeleton_test`: zakładka Drzewo otwiera `TreeScreen` |

### Data layer
- **Bez zmiany schematu** (v12 zostaje) — bez migracji i testu migracji. Ekran tylko czyta.
- **Próbne odtworzenie z kopii — nie dotyczy:** nic nowego nie trafia do bazy ani do kopii. Wymyślona rodzina (tylko debug i profile) zapisuje
  istniejącymi funkcjami, które mają swoje testy.
- `test/data/family_tree_test.dart`: odczyt na bazie testowej z wymyśloną rodziną — liczby osób i związków, kolejność partnerów, ślub i
  „razem”.

### Manual verification
**Agent na emulatorze** — przed stopem #2, ze zrzutami (`Grobing_Restore`, build profile, wymyślona rodzina; D5):
1. AC-1–AC-6 przejściem po ekranie: „Ja” w środku → żona → „Pokaż” → widok → wstecz → − dwa razy (poziom 3, 4) → + → „Pokaż w drzewie” z
   widoku dziadka.
2. Tekst 200% na 360 dp (`wm size` + `wm density` jak w poprzednich pozycjach) — drzewo, karta, + / −; zrzut przed i po.
3. Stany: bez „ja” (wyczyszczone ustawienie), osoba bez rodziny, pusta baza (świeża instalacja).
4. Ograniczenie animacji (`settings put global animator_duration_scale 0`) — przestawienie środka bez animacji.
5. Czytnik: `uiautomator dump` — opisy węzłów („… — w środek”, „… — otwórz”), przyciski + / − z opisem.
6. **Pomiar klatki** (`FrameTiming` w logu, build profile): przesuwanie na poziomie 3 i przejścia 2 → 3 → 4 → 2, przed i po optymalizacji z
   M3 — w *Dev report*. Emulator to wskazówka; telefon → [[ISSUE-032-mvp-install]].

**Autor: odczucie** (najwyżej 3 kroki, emulator `Grobing_Restore`):
1. Oddal i przybliż drzewo palcami (myszą z Ctrl) i przyciskami + / − — czy przy oddalaniu imiona czytają się i nie męczą (wybrany wariant
   z D1)?
2. Przejdź po rodzinie, dotykając kolejne osoby — czy łatwo się zorientować, gdzie jesteś, i czy nazwy w karcie brzmią tak, jak mówisz?
3. W widoku osoby dotknij „Pokaż w drzewie” — czy drzewo otwiera się tam, gdzie się spodziewasz?

### Out of Scope
- Tryb prezentacji i ikona telewizora → [[ISSUE-034-tree-presentation-mode]].
- Czas (element 6) → [[US-010-czas-na-drzewie]]; „Połącz dwie osoby” → [[US-011-polacz-dwie-osoby]]; K1 — nie w MVP.
- Twarde spacje w `personName` ([[style-b]] reguła 6 — osobna drobna pozycja z `CURRENT_STATE.md`); kontrola cykli (drzewo tylko się przy
  nich nie zawiesza: `levelsFrom` i układ odwiedzają osobę raz).
- Zdjęcia w węzłach poza tym, co daje `ProfileCircle` (kadr łącza jak w mini-drzewie) — bez nowych reguł zdjęć.
- Pomiar na telefonie (płynność, progi S2 w ręce, zadanie < 30 s) → ISSUE-032 → *Hand checks*.

## Dev report
> `dev`, 2026-10-13. Flutter 3.41.1. Build profile z `--dart-define=FRAME_LOG=true` na `Grobing_Restore` (D5), wymyślona rodzina z „Stanu
> danych”. `flutter analyze lib` — czysto; `dart format` — zrobione.

### What was built (`{code}`)
- **`lib/data/family_tree.dart`** (nowy) — cała rodzina naraz, tylko odczyt: osoby (imiona, nazwiska, płeć, lata, zmarły, profilowe), związki
  (partnerzy w kolejności zapisu, dzieci według urodzenia, ślub, początek związku), „ja”; `KinGraph` z tych samych danych. `watchFamilyTree`
  odświeża po każdym zapisie do czytanych tabel.
- **`lib/app/tree/tree_layout.dart`** (nowy) — poziomy D2 i port układu makiety 1:1, z sortowaniem stabilnym jak w JavaScripcie; linie
  (para, rodzic–dziecko z szynami na osobnych wysokościach) i ślad D9; rozmiary z parametru (tekst systemu).
- **`lib/app/tree/tree_labels.dart`** (nowy) — I2: imiona, które się mieszczą, najbliższe środka pierwsze.
- **`lib/app/tree/tree_painter.dart`** (nowy) — linie i ślad; ścieżki (także przerywane) budowane raz na układ.
- **`lib/app/tree/tree_screen.dart`** (nowy) — ekran: pasek, `InteractiveViewer` z S2 (progi 1,3 · 0,85 · 0,55, skala 0,4–2,0, krok 1,45,
  skala z osi x), + / −, podwójne dotknięcie pustego miejsca (z surowych zdarzeń, więc dotknięcie osoby nie czeka 300 ms), pigułka
  poziomu z `liveRegion`, przestawianie środka z animacją 0,45 s (bez niej przy ograniczeniu animacji), karta (D12, D13, G1, D20), stany
  (pusta baza, bez „ja”, błąd odczytu), opisy dla czytnika („…, Twoja babcia, w środek” / „otwórz”).
- **`lib/app/person/kinship_names.dart`** — `kinshipName`: słownik ISSUE-025 D2 z nawiasem, odcinki od drugiej osoby (D12), dopełniacz,
  „Twój / Twoja / Twoje” według rodzaju słowa, odcinki neutralne bez płci.
- **`lib/app/tabs.dart`** — `TreeScreen` zamiast zaślepki; `treeFocus` otwiera drzewo od nowa z daną osobą (D15).
- **`lib/app/person/person_screen.dart`** — „Pokaż w drzewie” pod mini-drzewem, gdy osoba ma rodzinę.
- **`lib/app/people/people_list.dart`** — `initialsOf`; `InitialsCircle.accentOutline` (znak „Ja” z obrysem w kolorze obrysu, D14).
- **`lib/dev/fictional_family.dart`** (nowy) — rodzina z makiety: 106 osób, 38 związków, raz; ustawia „ja”, gdy go nie ma.
- **`lib/app/data_state_screen.dart`** — przycisk „Wymyślona rodzina do drzewa”; przyciski wymyślonych danych za `!kReleaseMode` (D6).
- **`lib/dev/frame_log.dart`** (nowy) + `lib/main.dart` — czasy klatek do logu tylko z `--dart-define=FRAME_LOG=true`, nigdy w release.
- **`lib/app/tree/tree_placeholder_screen.dart`** — usunięty (z dysku; do indeksu wejdzie przy commicie paczki).

### Deviations (do przeglądu `ui`)
1. **Obwódka imion to tabliczka w kolorze tła** (zaokrąglona 4 dp, 3 dp z boków), a nie obrys liter jak na mapie Polski. Najpierw były
   rozmyte cienie, potem pomiar pokazał szarpanie na wątku rasteryzacji (niżej). Na jednolitym tle drzewa tabliczka działa jak obwódka:
   przerywa linie pod imieniem. [[style-b]] reguła 13 v1.25 mówi „obwódka w kolorze tła” — do przyjęcia albo poprawy przez `ui`.
2. **Drzewo nie ucieka z ekranu:** gdy po przesunięciu albo zmianie skali nie widać nikogo, widok wraca płynnie (0,35 s) do osoby w środku;
   palec na ekranie przerywa powrót. Specyfikacja tego nie mówi. Bez tego drzewo dało się zgubić na emulatorze: wstecz nie cofa środka
   (D15), a zakładka na swoim ekranie nic nie robi (reguła 12).
3. **Nowy rozmiar obszaru drzewa przed pierwszym dotknięciem** (klawiatura po wyborze „ja”, obrót) ustawia środek od nowa.
4. **Zmarły = zapisany zgon albo pochówek**, z datą albo bez (znicz w rogu węzła). Specyfikacja mówi „zmarły ma znicz”, nie mówi, skąd to
   wiadomo; `persons.is_living` ma wartość domyślną `false`, więc nic nie mówi.
5. **Imię przy tekście 100% ucina się przy ok. 10 literach** („Bronisła…”), tak jak w mini-drzewie (miejsce osoby 80 dp). AC-7 mówi o
   200%, a tam miejsce osoby rośnie do 160 dp i imiona mieszczą się w całości (zrzut 10b).
6. **„Pokaż w drzewie” zawsze otwiera drzewo od nowa** — także z widoku osoby otwartego z drzewa (stos drzewa znika, D15).
7. **Dopełniacz:** rzadsze formy sprawdzone w Wikisłowniku (tabele odmiany), a nie w SJP PWN, jak mówił plan — szwagra, siostrzeńca,
   zięcia, teścia, wuja (2026-10-13). Reszta to odmiana regularna (mamy, babci, dziadka…), objęta testami `qa`.
8. **Emulator `Grobing_Restore`: `hw.gpu.enabled=no` → `yes`** (kopia konfiguracji w katalogu tymczasowym sesji). Rysowanie programowe dawało
   inne liczby niż `Medium_Phone` w SPIKE-002 i zafałszowałoby odczucie płynności na stopie #2.

### Found on the emulator (przejście AC przed `qa`, R5) — poprawione
- (a) **Przejścia między poziomami szarpały:** 28–44% wolnych klatek, rasteryzacja p90 140–200 ms (rysowanie programowe). Przyczyny: osobny
  `Opacity` dla każdej pojawiającej się osoby i ok. 100 rozmytych cieni pod imionami w każdej klatce ruchu. Poprawka: jedna warstwa
  przezroczystości dla pojawiających się i jedna dla odchodzących, tabliczka zamiast cieni (odstępstwo 1).
- (b) **Drzewo dało się zgubić poza ekranem** po kilku przesunięciach i zmianach skali (odstępstwo 2).
- (c) **Tabliczka imienia „Ja” ucinała poświatę osoby w środku** (widać przy 200%) — teraz okrąg maluje się nad imieniem.
- (d) **Po wyborze „ja” z otwartą klawiaturą środek stał za wysoko** (odstępstwo 3).

### Pomiar klatek (`FrameTiming`, build profile, `Grobing_Restore` z GPU; od „Ja”)
| Co | Klatek | > 16,7 ms | Budowa p50 / p90 | Raster p50 / p90 | SPIKE-002 M3 (`Medium_Phone`) |
|---|---|---|---|---|---|
| przejście 2 → 3 (+ / −) | 41 | 7% | 1,1 / 4,1 ms | 4,2 / 7,3 ms | 55%, raster p90 65 ms |
| przejście 3 → 4 | 48 | 8% | 3,3 / 5,0 ms | 11,3 / 16,5 ms | 19% |
| przejście 4 → 3 · 3 → 2 | 54 · 58 | 2% · 5% | ok. 1–2 / 5–7 ms | 3,0–13,6 / 4,0–16,0 ms | 23% · 5% |
| przesuwanie, poziom 3 | 192 | 4% | 1,0 / 1,4 ms | 4,3 / 14,8 ms | 1%, raster p50 4,8 ms |
| przesuwanie, poziom 4 | 184 | 4% | 1,0 / 1,5 ms | 4,9 / 16,1 ms | 1,3% |

Pojedyncze klatki do ok. 150 ms raz na serię (pierwsza klatka po dłuższym spokoju). Emulator to wskazówka (dokumentacja Fluttera: *„generally
not indicative”*); telefon → [[ISSUE-032-mvp-install]] → *Hand checks* (wiersz ze SPIKE-002).

### Sprawdzone przez `dev` (zrzuty w katalogu tymczasowym sesji, `shots-033\`)
- **Liczby układu = SPIKE-002 M1:** od „Ja” 6 / 20 / 66 / 99 / 106 osób, szerokości 212 / 864 / 1960 / 2663 / 2960 dp, skrzyżowania 0 / 0 / 6 / 9 /
  10 (tymczasowy test, usunięty — testy pisze `qa`).
- **Nazwy dla wszystkich 105 osób wymyślonej rodziny** od „Ja” — m.in. „Twoja ciotka (siostra taty)”, „Twój wuj (brat mamy)”, „Twoja siostra
  stryjeczna (córka brata taty)”, „Twoja wujenka (żona brata mamy)”, „Twój wuj (mąż siostry taty)”, „Siostra cioteczna Twojego dziadka”,
  „Bratowa Twojej żony”, „Partnerka Twojego brata”, „Mąż Twojej prababci”. **Do oceny autora:** reguła D12 daje też „Synowa ciotki Twojego
  taty” (żona brata ciotecznego taty) i „Wnuk Twojej ciotki” — poprawne, ale można by powiedzieć inaczej (D12 → *Obali*).
- **Emulator:** AC-1 (02), AC-2 (03b, 04 — widok Kasi z aktywną zakładką Drzewo, wstecz wraca z tym samym środkiem), AC-3 (05b, 06,
  pigułka 05a, podwójne dotknięcie 13), AC-4 (ślady na 02 i 03b), AC-5 (07 — „Ciotka Twojej żony”), AC-6 (09a → 09b, z zakładki Osoby), AC-7
  (10b, 10c — 360 dp, tekst 200%), pusta baza (01), bez „ja” i wybór „ja” (12, 12b), ograniczenie animacji (11), opisy węzłów i + / − w
  `uiautomator dump` (`clickable=true`, „…, w środek” / „…, otwórz”).
- **Nie sprawdzone na emulatorze:** osoba bez rodziny i „Pokaż w drzewie” ukryte u osoby bez rodziny (w danych nie ma takiej osoby) i błąd
  odczytu — do testów `qa`; czytnik TalkBack na głos.

### For `qa`
- **`test/app/skeleton_test.dart` nie kompiluje się** — importuje usuniętą zaślepkę (`TreePlaceholderScreen`, 3 błędy analizy w `test/`).
  Reszta: 682 testy zielone (`flutter test`, 2026-10-13).
- **Stan emulatorów:** `Grobing_Restore` — build profile (FRAME_LOG), wymyślona rodzina (106 osób) i „ja” = Mateusz; release z danymi kopii
  `-029` odinstalowany (D5). `Medium_Phone` wyłączony, jego release v12 z danymi testowymi autora nietknięty.
- Kroki autora — *Implementation plan* → *Manual verification* (3 kroki odczucia, `Grobing_Restore`).

## Verification
> `qa`, 2026-10-13. DoD ISSUE (MVP): test happy-path dla każdego AC · ręczna weryfikacja na emulatorze · dokumentacja · zero danych rodziny.
> Warstwa danych tylko czyta, schemat v12 bez zmian — bez testu migracji i bez próbnego odtworzenia (plan → *Data layer*). Sieci w pozycji
> nie ma, więc logcat pod kątem współrzędnych nie dotyczy (retro 3, R7).

### Tests (happy path per AC, `{code}/test/`)
| AC | Test | Co sprawdza |
|---|---|---|
| AC-1 | `app/tree/tree_screen_test.dart` → *AC-1*; `app/tree/tree_layout_test.dart` → *AC-1* (dwa) | „Ja” w środku, 20 osób, karta „ur. 1983 · to Ty”, opisy dla czytnika; rodzice wyżej, dzieci niżej, każda para obok siebie (80 dp), rodzina żony po prawej |
| AC-2 | `tree_screen_test` → *AC-2* | dotknięcie Kasi → karta „ur. 1985 · Twoja żona”; „Pokaż” → widok osoby z aktywną zakładką Drzewo |
| AC-3 | `tree_screen_test` → *AC-3*; `tree_layout_test` → *AC-3* | − → „Poziom 3 · 66 osób” i 66 osób, − → „Poziom 4 · 99 osób”, + + → poziom 2; podwójne dotknięcie pustego miejsca → „Poziom 1 · 6 osób”; poziomy i układ = SPIKE-002 M1 liczba w liczbę |
| AC-4 | `tree_layout_test` → *AC-4* | ślad w górę przy tacie (poziom 1), w bok przy bracie, na zewnątrz od środka (poziom 2); żadnego śladu przy wszystkich osobach |
| AC-5 | `app/person/kinship_names_test.dart` → *kinshipName* (4); `tree_screen_test` → *AC-5* | słownik z nawiasami (ciotka, stryj, wuj, siostra cioteczna, wuj — mąż siostry taty, teść, szwagier), **„Siostra cioteczna babci Twojej żony”** (przykład AC-5, D12), „Partnerka Twojego brata”, słowa neutralne bez płci; w karcie „ur. 1961 · Ciotka Twojej żony” |
| AC-6 | `tree_screen_test` → *AC-6* | „Pokaż w drzewie” w widoku Józefa → Drzewo, „1925–2004 · Twój dziadek”; osoba bez rodziny — przycisku nie ma |
| AC-7 | `tree_screen_test` → *AC-7* | 360 dp, tekst 200%: miejsce osoby 160 dp, imię 26 sp w jednej linii, inicjały ≤ 44 dp, „Pokaż” pod tekstem karty. **Czy imiona są całe — tylko zrzut 10b** (czcionka testowa rysuje litery jako kwadraty, szersze niż Roboto; ten sam powód co w teście mapy przy 200%) |
| zaślepka znika | `app/skeleton_test.dart` (przepięty) | zakładka Drzewo otwiera `TreeScreen` |
| stany | `tree_screen_test` → *States* (dwa) | pusta baza; bez „ja” → „Wybierz, która osoba to Ty” → wybór „ja”; osoba bez rodziny — sama, „nie wiadomo jeszcze, kim jest dla Ciebie” |
| dane | `data/family_tree_test.dart` (3), `dev/fictional_family_test.dart` (4), `app/tree/tree_labels_test.dart` (5) | odczyt drzewa (kolejność partnerów i dzieci, ślub, „razem”, zmarły ze zgonu albo pochówku, „ja”, odświeżanie); kształt wymyślonej rodziny ze SPIKE-002 i nazwiska tylko z rdzeni; imiona I2 |

**Dostępność dotyku (retro 3, R2):** `meetsGuideline(androidTapTargetGuideline)` i `meetsGuideline(labeledTapTargetGuideline)` na drzewie przy
skali 1 oraz nowa reguła w `test/support/a11y.dart` — każdy węzeł semantyki z flagą przycisku ma akcję dotknięcia (pierwsze użycie; pomocnik do
kolejnych ekranów). **Wynik:** `flutter test` — **721 zielonych**, `flutter analyze` — czysto, `dart format` — bez zmian (2026-10-13).

### Agent na emulatorze (przed stopem #2)
Przejście `dev` (*Dev report*: AC-1–AC-7, stany, 200%, ograniczenie animacji, czytnik, pomiar klatek) powtórzone przez `qa` na buildzie po
poprawkach — zrzuty 20–24 i 30 w `shots-033\`. Poświata pod okręgiem sprawdzona w pikselach: wnętrze okręgu „Ja” `#1C1B19` (= powierzchnia),
przed poprawką `#594626`.

### UI review (`ui`, subagent bez historii) — 0 BLOCKER, 1 MAJOR, 3 MINOR — wszystkie poprawione przed stopem #2
| Waga | Problem | Poprawka (`dev`) |
|---|---|---|
| MAJOR | poświata osoby w środku leżała **na** okręgu: zabarwiała go na bursztynowo, znak „Ja” ok. 3,8–4,3:1 (< 4,5:1, SC 1.4.3), profilowe dostałoby odcień (reguła 14) | pierścień nad okręgiem, poświata pod nim (`tree_screen.dart`) |
| MINOR | cel dotyku węzła 80 × 65 dp × skala — wysokość < 48 dp już od skali 0,74 (poziom 3), a D17 zakładał tylko poziom 4 | cel tak wysoki jak miejsce osoby (80 dp, przy dużym tekście najwyżej rząd − 16 dp), wyśrodkowany na okręgu i imieniu; to samo w trafianiu podwójnego dotknięcia |
| MINOR | ślad partnera zawsze w prawo — u osób na lewo od środka celował w „Ja” (D9 → *Obali*); błąd z makiety `ui` | ślad na zewnątrz od środka, 14 dp jak w specyfikacji (`tree_layout.dart`); [[drzewo]] element 4 dopisany |
| MINOR | zmarły bez daty zgonu: znicz poza czytnikiem, a lata tego nie mówią | opis węzła dopisuje „nie żyje” |

**Znalezione przez `qa` w teście stanów:** kontrolery animacji tworzone leniwie powstawały dopiero w `dispose()` drzewa, które nikogo nie ułożyło
(pusta baza, bez „ja”) — ticker na odpiętym widżecie. Poprawka `dev`: kontrolery w `initState`.

**Odstępstwa `dev` — wszystkie 8 przyjęte przez `ui`** i zapisane: [[drzewo]] v1.7 (D21–D24, notki w D12, D15) i [[style-b]] v1.26 (reguła 13 —
tabliczka w drzewie). Zmiana `hw.gpu.enabled` na `Grobing_Restore` — dla `docs` do `CURRENT_STATE.md` → *Emulatory*.

**Poza zakresem, do decyzji na stopie #2:** ta sama przyczyna co MAJOR (poświata nad okręgiem) jest w mini-drzewie (`mini_tree.dart`) i w
portrecie widoku osoby (`person_screen.dart`) z [[ISSUE-024-person-view]].

### Dane rodziny
- Zmiany: kod Dart i testy, bez baz, kopii, eksportów i zdjęć. Wymyślona rodzina tylko z rdzeni Wymyśl-, Zmyśl-, Testow-, Przykład- — sprawdza
  to test (`fictional_family_test` → *surnames*); w testach pozostałe nazwiska też z tych rdzeni. Dry-run strażnika treści na plikach kodu i vaulta
  przeszedł (`dev`, 2026-10-13; powtórzy go `docs` przed `git add`).
- Zrzuty, makiety i kopia bazy testowej (`test-grobing.db`, wymyślone dane) leżą w katalogu tymczasowym sesji, poza repo.

### Not verified here (po jednym w linii — dla [[ISSUE-032-mvp-install]] → *Hand checks*)
- „nieprzetestowane na żywo”: czytnik TalkBack na głos na drzewie (opisy węzłów sprawdzone w `uiautomator dump` i w testach).

### Stop #2 (2026-10-13) — autor: „ok”
**Sprawdzone na urządzeniu** (pamięć: „ok” sprawdzać na urządzeniu): po wiadomości ze stopem `Grobing_Restore` narysował ok. 680 klatek
(19:31–19:32 w logu `GROBING_FRAME`), środek przestawiony na wnuczkę ciotki (Lena), skala zmieniona — **kroki 1 i 2 mają ślad**. Kroku 3 nie da
się odróżnić w stanie aplikacji od przestawiania środka — zapisany jako „ok” bez śladu.

- Krok 1 (oddalanie i imiona przy oddalaniu): **ok** (ślad na urządzeniu).
- Krok 2 (przejście po rodzinie, nazwy w karcie): **ok** (ślad na urządzeniu).
- Krok 3 („Pokaż w drzewie” z widoku osoby): **ok — bez śladu na urządzeniu** (AC-6 pokrywa test i przejście agenta, zrzuty 09a → 09b).
- **Decyzja o zakresie:** „ok” na wiadomość z rekomendacją → **tak**: poświata pod okręgiem także w mini-drzewie (`mini_tree.dart`) i w portrecie
  widoku osoby (`person_screen.dart`) z [[ISSUE-024-person-view]]. Zrobione w tej paczce (`dev`), falsyfikator `test/support/style_checks.dart` →
  `expectNoGlowOverContent` w testach drzewa i widoku osoby; [[style-b]] v1.27, reguła 2. W `person_screen_test` (AC-2 ISSUE-024) usunięte
  nieaktualne „«Pokaż w drzewie» nie ma, dopóki drzewo jest zaślepką” — przechodziło tylko dlatego, że lista buduje się leniwie.

**Po poprawce:** `flutter test` — 721 zielonych, `flutter analyze` — czysto; build profile z poprawką zainstalowany na `Grobing_Restore`.

### Na listę ISSUE-032 → *Hand checks* (po jednym w linii)
- „ok bez śladu”: „Pokaż w drzewie” z widoku osoby otwiera drzewo tam, gdzie autor się spodziewa (krok 3 stopu #2).
- „nieprzetestowane na żywo”: czytnik TalkBack na głos na drzewie (opisy węzłów, pigułka poziomu).
- (Płynność drzewa, progi S2 w ręce i zadanie < 30 s są już na liście ze SPIKE-002.)

### Werdykt `qa`: APPROVED (self-check, z uwagami)
Wszystkie AC-1–AC-7 mają test happy-path i przejście na emulatorze; przegląd `ui` — 1 MAJOR i 3 MINOR poprawione przed stopem, 8 odstępstw
przyjętych i zapisanych w [[drzewo]] v1.7 i [[style-b]] v1.26–v1.27. Uwagi:
1. czy imiona przy 200% są całe — sprawdza tylko zrzut z Roboto (10b); w teście czcionka testowa jest szersza;
2. reguła D12 daje czasem poprawne, ale nietypowe opisy („Synowa ciotki Twojego taty”) — autor nie zgłosił uwag w kroku 2; zostaje *Obali* D12;
3. przy 100% dłuższe imiona ucinają się („Bronisła…”, D24) — jak w mini-drzewie;
4. pomiar klatek tylko na emulatorze (z GPU) — telefon → ISSUE-032.

**Czego szukałem i nie znalazłem:** danych rodziny w zmianach (0 — tylko wymyślone rdzenie, test to pilnuje) · kodu sieciowego (0) · zmiany
schematu (0, v12) · przycisku bez akcji dotknięcia (0 — `expectEveryButtonTappable`) · celu dotyku < 48 dp przy skali 1 (0 — `meetsGuideline`) ·
poświaty nad okręgiem (0 po poprawce — `expectNoGlowOverContent`) · rozjazdu układu z SPIKE-002 M1 (0).

### Paczka dla `docs` (jedna pozycja = jeden commit na repo)
- **`grobing-code`:**
  - nowe: `lib/app/tree/tree_layout.dart`, `lib/app/tree/tree_labels.dart`, `lib/app/tree/tree_painter.dart`, `lib/app/tree/tree_screen.dart`,
    `lib/data/family_tree.dart`, `lib/dev/fictional_family.dart`, `lib/dev/frame_log.dart`, `test/app/tree/tree_layout_test.dart`,
    `test/app/tree/tree_labels_test.dart`, `test/app/tree/tree_screen_test.dart`, `test/data/family_tree_test.dart`,
    `test/dev/fictional_family_test.dart`, `test/support/a11y.dart`, `test/support/style_checks.dart`;
  - zmienione: `lib/app/data_state_screen.dart`, `lib/app/people/people_list.dart`, `lib/app/person/kinship_names.dart`,
    `lib/app/person/mini_tree.dart`, `lib/app/person/person_screen.dart`, `lib/app/tabs.dart`, `lib/main.dart`,
    `test/app/person/kinship_names_test.dart`, `test/app/person/person_screen_test.dart`, `test/app/skeleton_test.dart`;
  - usunięty: `lib/app/tree/tree_placeholder_screen.dart`.
- **`grobing-vault`:** `backlog/issues/ISSUE-033-tree-from-a-person.md`, `backlog/issues/ISSUE-034-tree-presentation-mode.md` (nowe),
  `03_REQUIREMENTS/user-stories/US-009-drzewo-od-osoby.md`, `05_DESIGN/drzewo.md`, `05_DESIGN/osoba.md`, `05_DESIGN/brand/style-b.md`,
  `00_START_HERE/TRACEABILITY.md`, `00_START_HERE/CURRENT_STATE.md` + pliki zamknięcia `docs`.
- **`grobing-agents`:** bez zmian.
- **Dla `docs` do `CURRENT_STATE.md` → *Emulatory*:** `Grobing_Restore` — build profile (FRAME_LOG) z wymyśloną rodziną (106 osób, „ja” = Mateusz),
  `hw.gpu.enabled=yes` (było `no`; kopia konfiguracji w katalogu tymczasowym sesji), release z danymi kopii `-029` odinstalowany (D5);
  `Medium_Phone` wyłączony, release v12 z danymi testowymi autora nietknięty.
