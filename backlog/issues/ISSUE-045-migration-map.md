---
title: "ISSUE-045 — Migration map: where the family lived over the years, on the time slider and the TV"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-17
verdict-reviewer: self-check
source: "`/pm` 2026-10-16 — pomysł autora („mapa, jak kto się przemieszczał po mapie świata”) · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-17
---

# ISSUE-045 — Mapa migracji

> Widok na danych z [[ISSUE-042-places-of-residence]]: gdzie kto mieszkał w danym roku i jak się przemieszczał. **Bez zmiany bazy**, więc
> jeśli zabraknie czasu przed instalacją (2026-10-29), przychodzi później jako aktualizacja ze sklepu ([[2026-10-16-retro-04]] → zasady
> terminu).

## What to build
- Mapa świata (offline) z miejscami zamieszkania — **ten sam suwak lat, tempo i tryb prezentacji na telewizor**, które są w drzewie
  ([[US-010-czas-na-drzewie]], [[ISSUE-038-history-on-tv-and-tempo]], [[ISSUE-036-cast-from-the-app]]); nie nowa oś czasu.
- ~~Punkty, które już są w danych: **cmentarz z pochówku** (ma współrzędne) i miejsca z [[ISSUE-042-places-of-residence]].~~ **K2 (decyzja autora, stop #1):**
  osoba po śmierci znika — mapa bez cmentarzy; punkty tylko z miejsc zamieszkania ([[mapa-migracji]] v1.1).
- ~~Miejsce niepewne (poziom „kraj”) jako **obszar, nie pinezka** — jak koło dokładności GPS na mapie cmentarza (kandydat na makietę).~~ **O3 (decyzja
  autora, stop #1):** osoba w punkcie nazwy kraju, bez obszaru i bez zaznaczonej granicy ([[mapa-migracji]] D15).
- Projekt: `ui` — specyfikacja i makieta (nowy ekran): skąd się wchodzi (zakładka, karta drzewa, widok osoby), droga jednej osoby vs cała
  rodzina w roku. Dane mapy świata: otwarte, wbudowane jak kontur Polski ([[ADR-007-poland-map-bundled-data]], Natural Earth).

## Acceptance Criteria
- **AC-1** *Given* osoby z zamieszkaniami *When* przesuwam suwak lat *Then* widzę, gdzie kto mieszkał w tym roku.
- **AC-2** *Given* osoba w środku *When* odtwarzam ▶ albo przesuwam suwak *Then* widzę, jak przechodzi przez kolejne miejsca w kolejności lat, a karta mówi,
  gdzie jest w danym roku. *(Przepisane przy zamknięciu — D2, stop #1: drogę widać tylko w ruchu; było: „Given osoba When ją wybieram Then widzę jej
  kolejne miejsca w kolejności lat”.)*
- **AC-3** *Given* tryb prezentacji *When* przesyłam na telewizor *Then* mapa z rokiem i tempem jest czytelna jak historia na drzewie.
- **AC-4** *Given* brak sieci *Then* mapa i punkty działają.

## Notes
- Zależy od [[ISSUE-042-places-of-residence]]. Płynność: pomiar klatek naprzemiennie z buildem odniesienia (retro 4, R3).
- **Input from [[ISSUE-042-places-of-residence]]** (zamknięte 2026-10-16): dane w tabeli `residences` ([[ADR-020-residences-place-in-the-row]]) — punkt na
  każdym poziomie (kraj: punkt etykiety, miejscowość i adres: środek miejscowości), lata `od`/`do` z dopiskiem dokładnie/około. **Pusty koniec bierze się z
  następnego zamieszkania** — `impliedEnds` w `lib/data/residences.dart` ([[zamieszkanie]] D12, decyzja autora); mapa liczy ten sam koniec, nie własny.
  Bez lat — zamieszkanie bez miejsca na osi czasu (do decyzji przy projekcie mapy).

## Implementation plan
> `planning`, 2026-10-17. **Pozycja z ekranem (nowy ekran i zmiana dwóch istniejących):** specyfikacja [[mapa-migracji]] **v1** (elementy 1–14,
> D1–D14, *Open* 1–5) oraz [[osoba]] v2.7 (9a, D22) i [[zamieszkanie]] v1.3 (4a); wytyczne [[style-b]] v1.33 (reguły 1, 2, 8, 13, 14; bez nowych
> tokenów). Bez US (task-level, z pomysłu autora), [[EPIC-003-zrozumienie]], widok 5 (M10). **Bez zmiany bazy.**
> **Cel autora** (`/pm` 2026-10-17, pytanie „po co dziś” — retro 4 R1): **„na wyjazd”** — pokaz rodzinie na telewizorze w trakcie wyjazdu na
> Wszystkich Świętych, więc pozycja wchodzi przed instalacją ze sklepu (najpóźniej 2026-10-29).
> **Makieta klikalna** (telefon i telewizor na żywo, przełączanie kandydatów, wymyślona rodzina 16 osób):
> `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/40086651-07c4-4037-a1ef-c81265e490b8/scratchpad/mapa-045.html`
> (obok `mapa-045.js` i `world.js`; zrzuty w `shots\`).

> **Stop #1 — 2026-10-17, autor:** *„W 2 · K 2 · O tutaj tylko środek tego kraju, bez okręgu lub zaznaczonych krawędzi · D 2 · R Tutaj Kadr wybrany przez
> usera, jeżeli tylko polskę sobie przybliże to widzę tylko to co się dzieje w polsce a ludzie którzy migrują wpadają „zza kadru””*. → **W2 · K2 · O3 · D2 ·
> R4** (O3 i R4 — warianty autora). Zapisane przez `ui` (krok 0): [[mapa-migracji]] **v1.1** (D6, D15–D17), [[drzewo]] v1.20 (1, 11, *Navigation*),
> [[style-b]] v1.34 (reguła 13 — mapa świata). Plan niżej już według tego wyboru: **bez zniczy i cmentarzy, bez obszaru kraju, bez linii drogi, bez
> plakietek i bez automatycznego kadru**. **AC-2 przepisane** (D2 — droga w ruchu; `docs` przy zamknięciu): *„Given osoba w środku When odtwarzam ▶ albo
> przesuwam suwak Then widzę, jak przechodzi przez kolejne miejsca w kolejności lat, a karta mówi, gdzie jest w danym roku”*. O3 zmienia też zdanie z *What to
> build* („obszar, nie pinezka”) — decyzja autora, [[mapa-migracji]] D15.

### Decision for stop #1 (author) — jedno pytanie, pięć liter
**Jak ma wyglądać mapa?** Na makiecie przełączasz pięć wyborów i od razu widzisz telefon i telewizor. Odpowiedz jednym ciągiem, np. **„W2 K1 O1 D1 R3”**
(moje rekomendacje), albo co zmienić:
- **W — skąd wchodzisz:** W1 — osobny ekran z ikony globusa w pasku drzewa; **W2** — przełącznik „Drzewo | Mapa” u góry zakładki Drzewo, a na
  telewizorze ten sam przełącznik w sterowaniu (z drzewa na mapę jednym dotknięciem, w tym samym roku).
- **K — osoba po śmierci:** **K1** — staje się zniczem na swoim cmentarzu; K2 — znika.
- **O — miejsce znane tylko do kraju:** **O1** — przerywana granica kraju; O2 — miękkie koło wokół środka kraju (za słabe kontrastowo: 1,23:1).
- **D — droga osoby w środku:** **D1** — bursztynowa linia z numerami miejsc; D2 — bez linii, droga widoczna tylko w ruchu.
- **R — kadr:** R1 — cała rodzina zawsze; R2 — droga osoby w środku; **R3** — większość rodziny, a kto dalej — plakietka przy krawędzi.

**„tak” = plan jak niżej z W2 K1 O1 D1 R3.** Inny wybór zmienia kroki 5–7 (W1: nowy ekran zamiast zmiany drzewa — mniej pracy w drzewie, prezentacja
bez przełącznika; K2, O2, D2, R1, R2 — mniej elementów, bez zmiany kolejności).

### Decisions taken in the plan (visible at stop #1, no question)
- **Bez zmiany bazy i bez ADR-u.** Mapa czyta to, co już jest: zamieszkania (v13), urodzenia i zgony (K2 — cmentarzy mapa nie czyta). Mapa świata to dane
  w aplikacji, jak kontur Polski ([[ADR-007-poland-map-bundled-data]]). Bez nowej zależności: `flutter_map` 8.3.2 i `latlong2` już są
  ([[NFR-005-dane-nie-opuszczaja-telefonu]] bez zmian — nic nie idzie do sieci).
- **Miejsce urodzenia i zgonu — nie w tej pozycji** ([[mapa-migracji]] D12): `events.place` to sam tekst bez punktu, więc to zmiana bazy, a pozycja ma
  być bez niej. Kandydat po wyjeździe, aktualizacją ze sklepu z migawką.
- **Mapa świata:** Natural Earth 1:10m admin-0 uproszczona (Douglas–Peucker) do pliku `assets/map/world.json` **w repo** (domena publiczna, jak
  `poland.json`). **Pomiar `planning`** na tym samym pliku źródłowym (2026-10-17, skrypt w katalogu tymczasowym sesji): 0,02° — 99,6 tys. punktów,
  1,6 MB · 0,04° — 55,2 tys., 0,9 MB · **0,06° — 37,8 tys., 615 KB (makieta)** · 0,10° — 22,8 tys., 372 KB. Start: **0,06°**, wyspy od 0,15 stopnia
  kwadratowego (183 kraje). Przybliżenie najwyżej do poziomu regionu (przy 0,06° ≈ 6,7 km linia robi się kanciasta). Kod kraju `ISO_A2_EH`, polska nazwa
  (`NAME_PL`) i punkt nazwy — do nazw krajów z danymi (O3: bez wielokąta „głównego”, obszaru nie ma). Plik źródłowy: README → *Mapa* (ten sam co do mapy
  Polski i listy miejsc).
- **Logika osobno od widoku:** „kto gdzie w roku Y” (D4), grupy, ruch (kto zmienił miejsce między latami), pierwszy kadr (wszystkie miejsca) i liczby pigułki
  to **czysta funkcja** w Darcie nad danymi drzewa (`TreeTime` — okna dat) i zamieszkaniami (`inStayOrder`, `impliedEnds` z `residences.dart` — mapa liczy ten
  sam koniec, nie własny). Testowalna bez ekranu.
- **Kadr (R4):** zmieniają go tylko gesty i + / −; trzymany w pamięci, dopóki aplikacja działa (jak `treeTempo`), a nie w bazie. Pierwszy — wszystkie miejsca.
- **W2 — mapa jako druga część zakładki Drzewo:** osoba w środku, karta, rok, tempo, ▶ i tryb prezentacji zostają w `TreeScreen`, a mapa to osobny
  widżet zamiast obszaru drzewa. Nowy widżet nie dokłada się do 2,4 tys. linii `tree_screen.dart` — ten dostaje tylko przełącznik, linię karty i wybór
  widoku.
- **Ruch na mapie bez warstwy na osobę** (retro 4, R3: jedno krycie na węzeł = jedna warstwa): okręgi i ślady rysowane w jednym malowaniu, przejazd
  liczony z jednego kontrolera animacji.
- **Dane do sprawdzenia:** w menu dewelopera „Stan danych” (tylko debug i profile, jak „Wymyślona rodzina do drzewa”) nowy przycisk **„Wymyślone miejsca
  zamieszkania”**. Dokłada zamieszkania wymyślonym osobom (wymyślone rdzenie, miejsca z listy), nic nie zastępując. Wpisy autora na `Grobing_Restore`
  (cmentarz i grób z 2026-10-16) zostają, więc pytanie o ich zastąpienie nie jest potrzebne.

### Steps
0. ~~**`ui` po stopie #1**~~ — **zrobione 2026-10-17**: [[mapa-migracji]] v1.1, [[drzewo]] v1.20, [[style-b]] v1.34.
1. **Mapa świata** — `tool/map/extract_world.dart` (Dart, jak `extract_poland.dart`; źródło `ne_10m_admin_0_countries.geojson`): uproszczenie, wyspy,
   kod, polska nazwa, punkt nazwy → `assets/map/world.json` + `pubspec.yaml` (`assets`); `lib/app/map/world_map_data.dart` — odczyt jak `PolandMapData`.
2. **Dane** — `lib/data/migration.dart` (nowy, tylko odczyt): wszystkie zamieszkania (z osobą); obserwacja tabel jak `watchFamilyTree`. Cmentarzy mapa nie
   czyta (K2).
3. **Logika** — `lib/app/tree/migration_year.dart` (nowy, czysty Dart): stan osoby w roku Y (żyje w miejscu · bez miejsca · przed narodzinami · po śmierci —
   D4, okna z `TreeTime`; przerywany obrys w oknie daty), grupy według miejsca (kolejność: osoba w środku, potem rok urodzenia), zmiana miejsca między dwoma
   latami (do przejazdu i śladu), wszystkie miejsca (pierwszy kadr), liczby pigułki (także poza kadrem), słowa linii karty („W 1930: Zmyślin, Polska · dziś
   Ukraina” — jak karta zamieszkania, [[zamieszkanie]] 6; po śmierci bez linii).
4. **Widżet mapy** — `lib/app/tree/migration_map.dart` (nowy): `flutter_map` z warstwą krajów (ląd, morze, granice 70% — D14; `evenOdd` jak mapa Polski),
   nazwy krajów z danych (bez nazwy, gdy ktoś stoi w jej punkcie — O3), okręgi osób ze stosem i „+N”, „cały kraj” w punkcie nazwy kraju bez obszaru (O3),
   rozsunięcie (9), pigułka (3), + / −, gesty i podwójne dotknięcie, przejazd i ślad — także zza kadru i poza kadr (8; u osoby w środku w akcencie),
   ograniczenie animacji, kadr tylko z gestów (R4), semantyka według [[mapa-migracji]] 4, 9; cele dotyku 48 dp.
5. **Drzewo (W2)** — `lib/app/tree/tree_screen.dart`: przełącznik „Drzewo | Mapa” w pasku (1, z ikonami przy ≥ 150% tekstu, gdy się nie mieści), wybór
   obszaru, „Połącz dwie osoby” tylko przy drzewie, linia karty (12) w `_TreeCard`, wejście z parametrem „mapa” (`TreeScreen`, `openTab` w
   `lib/app/tabs.dart`). Rok, osoba, tempo i ▶ wspólne.
6. **Tryb prezentacji** — `lib/app/tree/tree_presentation.dart` i `tree_screen.dart`: mapa poziomo (13), przełącznik w sterowaniu u góry pośrodku, bez
   pigułki; kadr przy wejściu — ten sam obszar co w telefonie, dopasowany do poziomego ekranu, a przy wyjściu z powrotem; przeciąganie i dwa palce działają;
   dotknięcie osoby → w środek.
7. **Widok osoby** — `lib/app/person/person_screen.dart`: „Pokaż na mapie” pod wierszami zamieszkań ([[osoba]] 9a, D22), tylko przy zamieszkaniu; → zakładka
   Drzewo, część „Mapa”, ta osoba w środku, rok „dziś”.
8. **Dane wymyślone** — `lib/dev/fictional_family.dart` (albo `fictional_data.dart`): zamieszkania dla ok. 30 wymyślonych osób w 4–5 pokoleniach — wyjazdy
   za granicę (kraj i miejscowość), przeprowadzka po 1945, „ok.” i daty bez końca, jedno zamieszkanie bez lat, miejsca z listy (np. „Ukraina — cały
   kraj”); przycisk w `lib/app/data_state_screen.dart`. Tylko debug i profile.
9. **README** `grobing-code` → *Mapa* (mapa świata: źródło, uproszczenie, `dart run tool/map/extract_world.dart <katalog>`).
10. **Przejście AC na emulatorze** (`Grobing_Restore`, build profile z `FRAME_LOG`, `--split-per-abi`; stała lista `dev`, retro 3 i 4):
    - każdy stan z [[mapa-migracji]] *States* ze zrzutem (dziś, rok w przeszłości, odtwarzanie — także wylot za krawędź przy przybliżonej Polsce,
      rozsunięcie stosu, osoba bez miejsca, przed narodzinami, po śmierci, osoba w środku poza kadrem, pusta mapa — na czystym drugim emulatorze albo w
      teście, „ja” niewybrane);
    - tekst 200% na 360 dp: pasek (przełącznik), pigułka, karta z nową linią, podpisy ≤ 1,3×;
    - semantyka i cele 48 dp (okrąg, stos, przełącznik, + / −); TalkBack — drzewo semantyki;
    - kadr: rok, ▶, zmiana osoby i „Pokaż na mapie” go nie przestawiają; zostaje po przejściu na drzewo i z powrotem;
    - **klatki** (retro 4, R3): ▶ na mapie od początku suwaka przy ok. 100 osobach z zamieszkaniami — porównanie z ▶ drzewa w tym samym buildzie;
      przesuwanie drzewa i ▶ drzewa naprzemiennie z buildem odniesienia (APK sprzed pozycji), bo pozycja zmienia `tree_screen.dart`;
    - **„mieści się” liczbą** (retro 4, R3): przełącznik i „Przesyłaj” w pasku 360 dp przy 100% i 200%; najgorszy przypadek — najdłuższa linia karty
      („W 1930: …, Polska · dziś Ukraina”) przy 200%;
    - tryb samolotowy — mapa i punkty (AC-4);
    - tryb prezentacji poziomo z rokiem, listwą i przełącznikiem (AC-3, zrzut).

### Files likely touched
`grobing-code`:
- nowe: `tool/map/extract_world.dart`, `assets/map/world.json`, `lib/app/map/world_map_data.dart`, `lib/data/migration.dart`,
  `lib/app/tree/migration_year.dart`, `lib/app/tree/migration_map.dart`;
- zmienione: `lib/app/tree/tree_screen.dart`, `lib/app/tree/tree_presentation.dart`, `lib/app/tabs.dart`, `lib/app/person/person_screen.dart`,
  `lib/dev/fictional_family.dart` (albo `fictional_data.dart`), `lib/app/data_state_screen.dart`, `pubspec.yaml`, `README.md`;
- testy (`qa`): `test/app/tree/migration_year_test.dart` (nowy), `test/app/tree/migration_map_test.dart` (nowy), `test/data/migration_test.dart` (nowy),
  `test/app/map/world_map_data_test.dart` (nowy), `test/app/tree/tree_screen_test.dart`, `tree_presentation_test.dart`, `presentation_mode_test.dart`,
  `test/app/person/person_screen_test.dart`, `test/dev/fictional_family_test.dart`.

`grobing-vault`: `ui` (krok 0) — [[mapa-migracji]], [[drzewo]], [[style-b]]; `docs` przy zamknięciu — stan, macierz, *Hand checks* w [[ISSUE-032-mvp-install]].
Bez zmian w `data-model.md` i `backup-format.md` (schemat bez zmian).

### AC mapping
| AC | Kroki | Dowód |
|---|---|---|
| AC-1 — przesuwam suwak lat → gdzie kto mieszkał w tym roku | 2, 3, 4, 5 | test `migration_year`: D4 (wpisane „Do” obejmuje swój rok, puste „Do” z następnego, ostatnie do śmierci, samo „Do” od urodzenia, dwa pobyty w roku — późniejszy, bez lat — poza osią, „ok.” jak okno drzewa, po śmierci — nie ma), grupy, pigułka (także poza kadrem); test widżetu: rok 1930 → okręgi w miejscach, przy kraju w punkcie nazwy bez obszaru; zrzuty |
| AC-2 (przepisane, D2) — osoba w środku: ▶ albo suwak → przechodzi przez kolejne miejsca w kolejności lat, karta mówi, gdzie jest | 3, 4, 5, 7 | test `migration_year`: zmiana miejsca między latami (kolejność `inStayOrder`, ten sam punkt dwa razy, kraj), słowa linii karty w każdym stanie; test widżetu: dotknięcie osoby → w środku, rok 1923 → 1929 → jej okrąg zmienia miejsce, ślad w akcencie, linia karty; „Pokaż na mapie” z widoku osoby → ta osoba w środku, kadr bez zmian; zrzut |
| AC-3 — tryb prezentacji: mapa z rokiem i tempem czytelna jak historia na drzewie | 6 | test widżetu: tryb prezentacji z mapą — rok w rogu (36 sp, 48 dp od lewej), listwa z ▶ i tempem, przełącznik zostawia rok i ▶; zrzut z emulatora; telewizor → lista B |
| AC-4 — brak sieci → mapa i punkty działają | 1, 2, 4 | test: mapa z samego `world.json` (bez warstwy kafelków, `no_cloud_sdk_test` bez zmian); emulator w trybie samolotowym — zrzut |

### Tests (`qa`)
- **`migration_year.dart` (czysta funkcja):** każda reguła D4 osobno, wymyślone osoby z wymyślonych rdzeni; okna „ok.” i daty bez dnia (przerywany obrys
  w oknie); osoba bez urodzenia; po śmierci — nie ma; grupy i kolejność w stosie; zmiana miejsca między latami (miejsce dwa razy, kraj); wszystkie miejsca
  (pierwszy kadr); pigułka (osoby poza kadrem też); słowa linii karty (N2, kraj, dziś, przed narodzinami, bez miejsca; po śmierci — brak) z twardymi spacjami.
- **`migration.dart`:** zamieszkania wszystkich osób, osoba bez zamieszkań.
- **`world_map_data`:** plik się wczytuje; Polska, Ukraina, Francja, Litwa mają kod `ISO_A2_EH` i polską nazwę; punkt nazwy kraju z pliku zgadza się z punktem
  kraju z listy miejsc (zamieszkanie „cały kraj” stoi w punkcie nazwy).
- **Widżety:** przełącznik (W2) — rok, osoba i tempo te same po zmianie części, ▶ biegnie dalej; „Połącz” tylko przy drzewie; pigułka; stos i
  rozsunięcie; „cały kraj” bez obszaru; **kadr (R4)** — rok, ▶, dotknięcie osoby i „Pokaż na mapie” go nie zmieniają, zostaje po przejściu na drzewo i z
  powrotem; linia karty; „Pokaż na mapie” tylko przy zamieszkaniu; tryb prezentacji z przełącznikiem i kadrem z telefonu; ograniczenie animacji — bez
  przejazdu; **`meetsGuideline`** (cele, kontrast tekstu — retro 3, R2), tekst 200%; semantyka (okrąg, stos).
- **Bez regresji drzewa:** obecne testy drzewa i trybu prezentacji zielone bez zmian oczekiwań (poza paskiem z przełącznikiem).
- **Pełny przebieg:** `flutter test --timeout 120s`, `flutter analyze`, `dart format`.
- **Przegląd `ui`** (subagent) przed stopem #2.
- **Warstwa danych:** tylko odczyt, schemat bez zmian — test migracji niepotrzebny; **próbne odtworzenie** kopii v15 z zamieszkaniami na drugim
  emulatorze nie jest wymagane przez DoD (pozycja nie zapisuje danych), ale kopia z wymyślonymi zamieszkaniami jest wejściem listy A w ISSUE-032.

### Manual verification
**Agent na emulatorze (przed stopem #2):** krok 10 z *Steps* — zrzuty stanów, 200% na 360 dp, cele i semantyka, klatki (mapa ▶ wobec drzewa ▶ w tym samym
buildzie; drzewo naprzemiennie z buildem odniesienia), tryb samolotowy, tryb prezentacji.

**Autor — odczucie (najwyżej 3, na emulatorze):**
1. Na mapie z wymyśloną rodziną dotknij ▶ od początku suwaka. Czy widać, kto się przeprowadza i dokąd, i czy kadr zachowuje się spokojnie?
2. Dotknij kilku osób (także stosu), potem w widoku osoby „Pokaż na mapie”, a na koniec przełącz „Drzewo | Mapa”. Czy osoba i rok zostają tam, gdzie się
   spodziewasz?
3. Tryb prezentacji na emulatorze (poziomo): mapa z rokiem w rogu i przełącznikiem w sterowaniu. Czy tak chcesz to pokazać rodzinie?

**Lista B — telewizor** ([[ISSUE-032-mvp-install]] → *Hand checks*, retro 4 R4): mapa z kanapy (brzegi lądu, podpisy 13 sp, okręgi 32 dp), płynność ▶ na
telefonie, TalkBack na mapie.

### Out of scope
- miejsce urodzenia i zgonu na mapie (D12) — zmiana bazy, kandydat po wyjeździe;
- granice historyczne (D1);
- „Połącz dwie osoby” i „czy mogli się spotkać” na mapie (D11);
- lista osób z miejsca w arkuszu, filtr według linii albo pokolenia, wyszukiwanie na mapie;
- poprawa zamieszkań z mapy (poprawa zostaje pod ✎ w widoku osoby — [[style-b]] reguła 15);
- inne zdarzenia z miejscem (ślub, chrzest), mini-mapa w widoku osoby;
- kafelki, zdjęcia satelitarne, przybliżenie poniżej poziomu regionu;
- zmiana wyglądu drzewa poza paskiem i trybem prezentacji.

### Obali (falsifiers)
- **▶ na mapie wyraźnie gorsze od ▶ drzewa w tym samym buildzie** → mniej punktów (0,10° — 22,8 tys.), kraje rysowane raz do obrazu i przesuwane, a nie
  przeliczane w każdej klatce; dopiero potem decyzja autora o mniejszym kadrze świata.
- **Przełącznik w pasku nie mieści się na 360 dp przy 200%** nawet z samymi ikonami → przełącznik pod paskiem, nad mapą (zmiana [[mapa-migracji]] 1 —
  `ui`).
- **Wbudowanie mapy w `TreeScreen` (W2) okazuje się splątane** (stan drzewa, ścieżka, animacje) → mapa jako osobna trasa ze wspólnym stanem roku i osoby,
  ten sam wygląd przełącznika; powiedziane na stopie #2, nie po cichu.
- **Na wymyślonej rodzinie stosy „+N” zasłaniają mapę** → [[mapa-migracji]] D2 → *Obali* (liczba przy miejscu) przed stopem #2.
- **Przy przybliżonej Polsce gubisz osoby poza kadrem** (stop #2) → [[mapa-migracji]] D6 → *Obali*: plakietki przy krawędzi z v1 (R3).

### Sources
[[mapa-migracji]] v1 (prior art: Legacy Family Tree, Heredis, Leaflet.markercluster; pomiar kontrastu) · [[zamieszkanie]] D4, D12 · [[drzewo]] 5, 6, 11, D32,
D36–D42 · [[style-b]] v1.34 reguła 13 · [[ADR-007-poland-map-bundled-data]] · [[ADR-020-residences-place-in-the-row]] · retro 4 R1, R3, R4 · pomiar mapy
świata (`planning`, 2026-10-17).

## Dev report
> `dev`, 2026-10-17. Flutter 3.41.1 (przypięty). Kroki 1–9 planu zrobione, krok 10 (przejście na emulatorze) niżej. `flutter analyze` czyste,
> `dart format` bez zmian. **Bez zmiany bazy** (schemat v15), bez nowej zależności. Testów nie dotykałem (`qa`).

### Changed (`grobing-code`)
- **Mapa świata:** `tool/map/extract_world.dart` (nowy) → `assets/map/world.json` (nowy, **508 KB, 182 kraje, 35 005 punktów** — Douglas–Peucker 0,06°,
  wyspy od 0,15 stopnia kw., bez Antarktydy, kod `ISO_A2_EH`, `NAME_PL`, punkt nazwy); `pubspec.yaml` (asset); `lib/app/map/world_map_data.dart` (nowy — odczyt
  raz na uruchomienie, w tle przez `compute`).
- **Dane:** `lib/data/residences.dart` — `allResidences` i `watchAllResidences` (zamieszkania wszystkich osób; w tym pliku, bo korzysta z prywatnego
  `_residence`, a nie w osobnym `migration.dart` z planu).
- **Logika:** `lib/app/tree/migration_year.dart` (nowy, czysty Dart) — `MigrationYear` (stan osoby w roku według D4, okna z `TreeTime`, grupy, liczby pigułki,
  wszystkie punkty, kody krajów), `mapWhereLine` (linia karty — z `residenceCardLine` karty zamieszkania), `mapPill`, `mapPlaceLabel`, `mapWhen` (twarde spacje).
- **Widżet mapy:** `lib/app/tree/migration_map.dart` (nowy) — `MigrationMap`: ląd (`_LandLayer`), osoby w stosach i skupieniach (`_PeopleLayer`), rozsunięcie,
  przejazd i ślad, przenikanie grupami (jedna warstwa na grupę), pigułka, + / −, kadr z gestów (`migrationArea`, w pamięci do zamknięcia aplikacji).
- **Drzewo (W2):** `lib/app/tree/tree_screen.dart` — `_PartSwitch` w pasku i w sterowaniu trybu prezentacji; część „Mapa” zamiast obszaru drzewa (te same
  warstwy prezentacji: rok w rogu, pasy przy krawędziach, listwa, „Zakończ”); linia karty `where`; dotknięcie osoby na mapie; „Połącz dwie osoby” tylko
  przy drzewie; `showMap` w `TreeScreen`; `lib/app/tabs.dart` — `openTab(…, treeMap:)`.
- **Widok osoby:** `lib/app/person/person_screen.dart` — „Pokaż na mapie” pod zamieszkaniami ([[osoba]] 9a, D22).
- **Dane wymyślone:** `lib/dev/fictional_residences.dart` (nowy) + przycisk „Wymyślone miejsca zamieszkania” w `lib/app/data_state_screen.dart` (debug i
  profile): 30 wymyślonych osób, 6 wymyślonych miejscowości (rdzenie Wymyśl-, Zmyśl-, Testow-, Przykład-) w przykładowych punktach, 5 krajów; wyjazd do Francji
  i z powrotem, przeprowadzka po 1945, Litwa „cały kraj”, emigranci do USA i Niemiec, „ok.”, puste „Do”, dwa zamieszkania bez lat. **Ponowne dotknięcie
  podmienia tylko własne zamieszkania** — wpisy z ręki (ISSUE-042) zostają.
- **README** → *Mapa* → *Mapa świata (mapa migracji)*: źródło, przebudowa, kadr, skupienia, pułapka wydajności.

### Emulator pass (`Grobing_Restore`, build profile, `--split-per-abi`, `FRAME_LOG`)
APK sprzed pozycji zapisany przed instalacją (`emu045\apk\installed-044-profile.apk`); build odniesienia z kodu `HEAD` w kopii drzewa roboczego poza repo (bez
`key.properties`). Instalacja nad v15 — bez migracji, migawki v12–v14 bez zmian. Dane: wymyślona rodzina (109 osób) + przycisk → **59 zamieszkań** (54 wymyślone
+ 5 z ISSUE-042). Wpisy autora (cmentarz i grób) nietknięte. Zrzuty: katalog tymczasowy sesji `40086651-…\scratchpad\emu045\shots\`.
- **Pasek (W2):** przełącznik „Drzewo | Mapa”, segmenty 48 dp wysokości (`uiautomator`: 126 px przy 420 dpi), stan „zaznaczone”; „Połącz dwie osoby” tylko przy
  drzewie (`01`, `02`).
- **Dziś, pierwszy kadr — wszystkie miejsca** (USA ↔ Litwa, czyli prawie cały świat; `03`): pigułka „Dziś na mapie: 13 osób · 61 bez miejsca”.
- **Rok 1927** (`06`): „Litwa · cały kraj” — dwie osoby w punkcie nazwy Litwy, bez obszaru (O3); Testowice 7 osób; karta „W 1927: przed narodzinami”.
- **Rozsunięcie** stosu Testowo (`05`): 4 osoby na okręgu, nóżki, imiona; dotknięcie Marka → w środek, karta „Dziś: Testowo, Polska”, **kadr bez zmian**.
- **„Pokaż na mapie”** z widoku Marka → część „Mapa”, Marek w środku, ten sam kadr; wstecz → mapa Polski (D15) (`14`, `15`).
- **Ruch** (`19`, ▶ „Wolno” od 1940): w 1946 okręgi jadą z Testowic i Zmyślina na zachód, ślady gasną, niepewne daty z przerywanym obrysem.
- **Tryb prezentacji** (`07`–`10`): poziomo, rok 36 sp w rogu, przełącznik u góry pośrodku, „Zakończ prezentację”, listwa; przełączenie na „Drzewo” — ten sam rok;
  kadr = obszar z telefonu dopasowany do poziomego ekranu.
- **Tryb samolotowy** (`18`): mapa, osoby i skupienia bez zmian (AC-4).
- **Tekst 200% na 360 dp** (`16`, `17`): **przełącznik z napisami potrzebuje ok. 267 dp**; w części „Drzewo” miejsca jest ok. 244 dp (obok dwóch ikon) → same ikony.
  Pigułka w dwóch liniach (84 dp), łamie się przed „·”; podpisy ≤ 1,3×; karta: „Pokaż ›” pod tekstem, linia „Dziś: …” zawinięta bez ucięcia.
- **Restart aplikacji** → pierwszy kadr znowu wszystkie miejsca (R4: kadr trwa, dopóki aplikacja działa).
- **Klatki** — ▶ od 1860 do „dziś”, „Średnio”, świeży start (skrypt `emu045\play.sh`; % klatek > 16,7 ms, p50 / p99 wolniejszego z build i raster):

  | Przebieg | Wolne | p50 | p99 | Uwagi |
  |---|---|---|---|---|
  | mapa, pierwsza wersja | 22,1% · 26,0% | 14,1 · 15,2 ms | 29,7 · 32,4 ms | raster p50 13,1 ms, build p90 16,5 ms |
  | **mapa, końcowa** (9 przebiegów) | **3,4 – 11,2%** | 4,3 – 15,0 ms | 18,0 – 29,1 ms | dwa tryby emulatora (p50 ok. 4–5 albo 13–15 ms) przy tym samym obrazie lądu w logu |
  | mapa bez obwódki podpisów (próba, kod przywrócony) | 6,6% | 12,8 ms | 19,9 ms | obwódka kosztuje ok. 2 ms rastra na klatkę |
  | drzewo, nowy build (4) | 2,7 · 3,0 · 4,2 · 4,8% | 4,3 – 4,5 ms | 18,2 – 29,2 ms | naprzemiennie z odniesieniem |
  | drzewo, build odniesienia (2) | 5,6 · 3,6% | 4,2 – 4,3 ms | 19,6 · 20,3 ms | **drzewo bez regresji** |

  Mapa przy ▶ rysuje każdą klatkę (przejazdy i ślady), drzewo — tylko przy zmianie roku (ok. 960 wobec ok. 335 klatek w przebiegu). Końcowa mapa mieści się w
  zakresie przyjętym dla drzewa z wieńcami w ISSUE-044 (12,5–15%) — **płynność na telefonie → lista B**.

### Deviations (dla przeglądu `ui`)
1. **Skupienia miejsc** (nie ma ich w [[mapa-migracji]]): miejsca bliżej niż 44 dp na ekranie łączą się w jeden stos — do 3 twarzy, „+N”, podpis „5 miejsc”;
   dotknięcie **przybliża** do ich miejsc, a przy największym przybliżeniu rozsuwa. Czytnik: „Wymyślowo, Zmyślice i 2 więcej: 12 osób — przybliż”. Powód: pierwszy
   kadr (wszystkie miejsca) przy rodzinie w Polsce i w USA to cały świat, a stosy miejscowości jednego kraju leżały na sobie (zrzut `02`). Wzorzec:
   Leaflet.markercluster (*zoom to bounds*, *spiderfy* na dole) — ten sam, który spec cytuje przy rozsunięciu, i ten sam co znicze z liczbą na mapie Polski.
2. **Podpisy nie nachodzą na siebie ani na okręgi innych miejsc** — kolejność: miejsce osoby w środku, potem najwięcej osób, na końcu nazwy krajów (zrzut `02`
   przed poprawką: „Polska”, „Testowo”, „Niemcy · cały kraj” na sobie). Jak I2 w drzewie: mniej podpisów, każdy czytelny.
3. **Ląd rysowany raz do obrazu**, gdy kamera stoi (technika, wygląd ten sam) — tabela klatek wyżej; to *Obali* z planu.
4. **Podwójne dotknięcie** przybliża o 1 poziom `flutter_map` (×2), a nie ×1,45 jak drzewo; + / − — ×1,45 jak w spec.
5. **Przełącznik ma ten sam kształt w obu częściach** — „mieści się” liczone względem miejsca w części „Drzewo” (z „Połącz”). Na 360 dp przy 200% w części „Mapa”
   napisy by się zmieściły (292 dp), ale przełącznik zmieniałby kształt pod palcem.
6. **Dotknięcie osoby w środku na mapie otwiera jej widok** (poza trybem prezentacji), jak drugie dotknięcie w drzewie; spec mówi tylko „w środek”.
7. **Pierwszy kadr przybliża najwyżej do poziomu 5**, gdy wszystkie miejsca leżą blisko siebie (bez tego jedno miejsce dawałoby przybliżenie do regionu).
8. **W trakcie przejazdu** (0,6 s) podpis i „+N” stoją już przy nowym miejscu, a okręgi jeszcze jadą (zrzut `19`) — chwilowe.
9. **Przełącznik w trybie prezentacji stoi na środku miejsca między rokiem a „Zakończ prezentację”**, a nie na środku ekranu (runda 4 niżej) — przy
   100% ok. 40 dp w lewo od środka. Gdy napisy się tam nie mieszczą, same ikony.

### Round 2 — decyzja autora w trakcie przeglądu (2026-10-17)
Autor: *„Tak naprawdę nie potrzebuje żadnych nazw krajów ani miejscowości, wystarczą awatary i kontury krajów”* ([[mapa-migracji]] D18, v1.2). Z mapy zeszły
podpisy miejsc, „· cały kraj” i nazwy krajów (z nimi kolejność podpisów — odstępstwo 2 nieaktualne); `world.json` nadal niesie nazwy, ale nic ich nie rysuje.
Zostały: „+N”, pigułka, imiona pod rozsuniętym stosem (to nie nazwy miejsc — do potwierdzenia na stopie #2) i linia karty „W 1930: …” (jedyne słowa o
miejscu — też do potwierdzenia). Czytnik mówi miejsce jak wcześniej.

### Round 3 — przegląd `ui` (1 MAJOR, 9 MINOR — wszystkie poprawione)
- **MAJOR — przejazd ucinany co rok:** przy „Średnio” rok trwa 100 ms, a przejazd 600 ms; jedna animacja na wszystkich ruszała od nowa z każdym rokiem i okrąg
  skakał po 1/6 drogi. Teraz **każdy przejazd ma własny start** (`_Glide`): następny rok zaczyna nowy przejazd z miejsca, do którego okrąg doszedł.
- **MINOR:** „+N” wraca, gdy osoby stosu dojechały (odstępstwo 8) · ślad rysowany za okręgiem, nie przed nim · stosy łączą się, gdy ich okręgi by się stykały
  (nie od stałej odległości) · obrys 1,5 dp na każdym okręgu, także ze zdjęciem · inicjały 12 sp w kolorze tekstu (jak węzeł drzewa, 10,02:1) · u osoby w środku
  przerywany pierścień w akcencie przy niepewnej dacie · pigułka mówi czytnikowi dopiero po zatrzymaniu ▶ · twarda spacja po „w” w „w których” (pusta mapa, reguła 6) ·
  ikona `public_outlined` (reguła 3) · miejsce na „Połącz dwie osoby” liczone tylko przy części „Drzewo”.
- Przyjęte odstępstwa 1, 4–7 zapisał `ui` w [[mapa-migracji]] v1.2 (D19–D23).

### Round 4 — co znalazły testy `qa` (2026-10-17)
- **Przełącznik pod „Zakończ prezentację” przy dużym tekście** (test prezentacji: dotknięcie „Mapa” trafiało w „Zakończ”). Pomiar ze zrzutu `r09` (420 dpi,
  ekran poziomo 914 dp): przy 100% między przełącznikiem a „Zakończ” jest 135 dp; **przy 200% przełącznik z napisami (ok. 280 dp) wchodzi pod „Zakończ” (ok.
  361 dp) o ok. 56 dp, a na 800 dp (360 dp przy gęstości 480, poziomo) nawet same ikony o ok. 29 dp**. Poprawka (`tree_screen.dart` → `_ControlsTop`,
  `tree_presentation.dart` → `PresentationYear.right`): „Zakończ” po prawej we własnej szerokości, przełącznik na środku miejsca między rokiem (jego
  najszerszy zapis przy danym tekście) a „Zakończ”, przy braku miejsca same ikony — odstępstwo 9. Najgorszy przypadek, 800 dp przy 200% — **pomiar na
  emulatorze** (`r18`, `uiautomator`): „Zakończ” 304 dp (szacunek wyżej, 361 dp, był za duży), miejsca na przełącznik ok. 301 dp, przełącznik z napisami 267 dp
  → **napisy**, 29 dp do „Zakończ”, nic nie nachodzi; same ikony zostają jako zabezpieczenie (węższe miejsce, inny krój). Stary układ (środek ekranu, 400 ± 133 dp)
  wszedłby pod „Zakończ” (od 484 dp) o ok. 49 dp. Pierwsza wersja (`Row`) przepełniała się w czcionce testów (każda litera to kwadrat: „Zakończ” przy 200% ok. 650 px na
  800) — `tree_presentation_test` AC-5 i AC-6; układ nie daje przełącznikowi mniej niż ikony i nie zgłasza przepełnienia, a poza tym zachowuje się jak dawniej.
- **Zegar przejazdu z klatek, nie ze stopera** (`migration_map.dart`): przejazd rodzi się i rysuje w czasie klatki (`currentSystemFrameTimeStamp`) — równo z
  klatkami i z zegarem testu (test MAJOR-a z rundy 3 był bez tego zależny od czasu ściany). Pusta linia `if (…) {}` w `didUpdateWidget` usunięta.

### Round 5 — drugi przegląd `ui` (0 MAJOR, 4 MINOR; odstępstwo 9 przyjęte — [[mapa-migracji]] v1.3 D24, [[drzewo]] v1.22)
- **Stos rysowany od ostatniego okręgu do pierwszego** (`migration_map.dart`): pierwszy — osoba w środku — na wierzchu i żaden okrąg nie traci obu brzegów.
  Wcześniej drugi okrąg stosu z osobą w środku był ucięty z obu stron (inicjały czytały się źle).
- **Przejazd startuje z miejsca, w którym okrąg był narysowany** w ostatniej klatce (w stosie, w skupieniu, w rozsunięciu albo w drodze — `_drawn`), a nie z
  punktu miejsca: wcześniej w pierwszej klatce okrąg z pozycji 0 stosu czterech skakał o 34 dp.
- **Przełącznik w sterowaniu prezentacji ma jedną krawędź:** powierzchnia w kształcie kapsuły pod obrysem (`Ink` na przezroczystym `Material`), bez `Material`
  48 dp pod spodem; cel dotyku 48 dp bez zmian. W pasku bez zmian.
- Liczby rundy 4 poprawione według pomiaru (wyżej).

### Round 6 — decyzje autora na stopie #2 (2026-10-17; [[mapa-migracji]] v1.4, [[style-b]] v1.36)
- **D25 — przeprowadzka bez śladu:** *„chciałbym aby po prostu się te avatary przemieszczały płynnie po mapie bez tych linii szarych (nie ma potrzeby
  żadnego dodatkowego efektu)”*. `migration_map.dart`: bez `_Trail` i `_TrailPainter`; zostaje sam przejazd (0,6 s przy ▶, 150 ms ręcznie), od miejsca, w
  którym okrąg był narysowany, nieprzerywany kolejnym rokiem.
- **D26 — awatar także u „ja”:** autor pytał, czemu zamiast awatara jest „Ja”; na pytanie (jedno, z wariantami) wybrał: zdjęcie profilowe u każdego, kto je
  ma, także u siebie; bez zdjęcia inicjały. `_PersonCircle` bez znaku „Ja”; imię „Ja” w rozsunięciu zostaje. Drzewo i lista bez zmian.
- **Portrety w danych wymyślonych** (żeby awatary było widać na emulatorze): `lib/dev/fictional_residences.dart` → `addFictionalPortraits` — 7 osób wymyślonej
  rodziny, także „ja”, dostaje portret rysowany w kodzie (`fictionalPeoplePng`, sepia, głowa i ramiona — nikt nie jest przedstawiony, plik tylko na urządzeniu),
  tylko osoba bez żadnego zdjęcia, bez dublowania. Przycisk w „Stanie danych”: „Wymyślone miejsca zamieszkania i portrety” (debug i profile).

### Found, outside the item
- Pigułka „bez miejsca” na wymyślonych danych jest duża (61 osób) — to dane, nie błąd; przy prawdziwych danych pokaże, ile zamieszkań brakuje.

### For `qa`
- **Testy:** `migration_year` (D4 — każda reguła, okna „ok.”, przed/po, grupy, pigułka, słowa linii karty z twardymi spacjami), `allResidences`, `world_map_data`
  (kody, polskie nazwy, punkt nazwy = punkt kraju z listy miejsc), widżet mapy (stos, rozsunięcie, skupienie → przybliżenie, kadr R4, „cały kraj” bez obszaru,
  ograniczenie animacji, semantyka), przełącznik w `TreeScreen` (rok, osoba, tempo, ▶ po zmianie części; „Połącz” tylko przy drzewie; tryb prezentacji),
  „Pokaż na mapie”, `fictional_residences` (ponownie — bez dublowania, wpisy z ręki zostają). Istniejące testy drzewa mogą szukać tytułu „Drzewo” w pasku —
  teraz to segment przełącznika.
- **Stany bez przejścia na emulatorze** (wymagają innych danych): pusta mapa (nikt bez zamieszkań), „ja” niewybrane — w testach widżetu.
- **Emulator:** zainstalowany końcowy build (profile, `FRAME_LOG`); dane z przycisku są na miejscu; tekst, gęstość i tryb samolotowy przywrócone.

## Verification
> `qa`, 2026-10-17. Flutter 3.41.1. Bez zmiany bazy (v15) — test migracji i próbne odtworzenie niepotrzebne (DoD: pozycja tylko czyta).

### Tests (`grobing-code`)
- **Pełny przebieg:** `flutter test --timeout 120s` — **923 zielonych** po rundzie 6 (921 po rundzie 5; przed pozycją 820 przy ISSUE-042); `flutter analyze` — czysto; `dart format` — bez zmian.
- **Nowe:** `migration_year_test` (12 — każda reguła D4, okna „ok.”, przed narodzinami i po śmierci, grupy i kolejność, pigułka, słowa linii karty z
  twardymi spacjami) · `all_residences_test` (2) · `world_map_data_test` + `fictional_residences_test` (6 — kody, polskie nazwy, punkt nazwy = punkt kraju z
  listy miejsc; ponowne dotknięcie bez dublowania, wpisy z ręki zostają; portrety D26 — 7 osób, także „ja”, plik pod `media/`, bez dublowania) ·
  `migration_map_test` (12):
  - W2 — przełącznik: rok, tempo i ▶ zostają przy zmianie części, „Połącz dwie osoby” tylko przy drzewie;
  - AC-1, AC-2, R4 — „dziś” w Polsce: stos się rozsuwa, imiona pod okręgami, dotknięcie → w środek, linia karty, **kadr bez zmian**, kraj sam w punkcie
    nazwy bez obszaru (O3), **żadnych nazw miejsc i krajów na mapie** (D18);
  - pierwszy kadr = wszystkie miejsca, skupienie przybliża do swoich miejsc;
  - AC-3 — tryb prezentacji z mapy: poziomo, bez pigułki, przełącznik w sterowaniu, „Drzewo” — ten sam rok, „Mapa” z powrotem, wyjście → pionowo;
  - „Pokaż na mapie” (osoba 9a) i jego brak bez zamieszkań; pusta mapa; „ja” niewybrane;
  - **element 8 — przejazd nie jest ucinany** przez następny rok (MAJOR rundy 3) i **startuje z miejsca okręgu w stosie** (MINOR rundy 5); oba testy
    sprawdzone mutacją — na starym kodzie padają (skok 92 px i 34 dp);
  - **D26 — awatary:** zdjęcie profilowe na mapie u każdego, kto je ma, także u „ja” (bez znaku „Ja”), inicjały u reszty;
  - tekst 200% na 360 dp (same ikony w obu częściach); `meetsGuideline(androidTapTargetGuideline)`, `labeledTapTargetGuideline`, każdy przycisk z akcją
    dotknięcia (retro 3, R2).
- **Zmienione:** `tree_presentation_test` — w trybie prezentacji nie ma paska zakładek ani „Połącz dwie osoby”.
- AC-4 (bez sieci): mapa z samego `world.json`, bez warstwy kafelków; `no_cloud_sdk_test` bez zmian; emulator w trybie samolotowym (`dev`, zrzut `18`).

### What the tests found (→ `dev`, runda 4)
- Przełącznik w sterowaniu prezentacji pod „Zakończ prezentację” przy dużym tekście — poprawione (odstępstwo 9, przyjęte przez `ui`: D24).
- Zegar przejazdu ze stopera — test zależny od czasu ściany; teraz czas klatki.

### `ui` review
- **Pierwszy przegląd** (zrzuty `r01`–`r11`): 1 MAJOR (przejazd ucinany co rok) i 9 MINOR — poprawione w rundzie 3; odstępstwa 1, 4–7 przyjęte ([[mapa-migracji]]
  v1.2, D19–D23). W jego trakcie decyzja autora D18 (bez nazw).
- **Drugi przegląd** (zrzuty `r12`–`r20` z buildu po rundzie 4): 0 MAJOR, 4 MINOR — stos ucięty z obu stron, start przejazdu z punktu miejsca, podwójna
  krawędź przełącznika w prezentacji, zła liczba w *Round 4* — poprawione w rundzie 5; odstępstwo 9 przyjęte ([[mapa-migracji]] v1.3 D24, [[drzewo]] v1.22).
- **Na emulatorze po rundzie 4** (`qa`): 200% przy 800 dp poziomo — przełącznik z napisami 267 dp, 29 dp do „Zakończ”, „Drzewo” → drzewo w tym samym roku,
  „Mapa” → z powrotem (`r18`–`r20`).

### Frames (build profile, `FRAME_LOG`, ▶ od 1860 do „dziś”, „Średnio”)
Pomiar naprzemienny z buildem `dev` sprzed rundy 3 (te same dane, rozgrzewka po instalacji w parach 3–4):

| Build | Wolne klatki (> 16,7 ms) | p50 |
|---|---|---|
| sprzed rundy 3 | 13,5 · 14,2 · 15,5 · 14,8% | 14,2 – 14,7 ms |
| po rundzie 4 | 19,8 · 16,1 · 12,8 · 14,1% (bez pary: 14,9 · 11,3 · 9,0%) | 13,1 – 14,7 ms |
| drzewo, ten sam build | 7,5 · 5,0% | 5,5 · 6,0 ms |

Emulator był w wolniejszym trybie niż przy pomiarze `dev` (drzewo 5–7,5% wobec 2,7–4,8%). **Bez regresji rund 3–4** — rozrzut mieści się w szumie hosta; mapa
w zakresie przyjętym dla drzewa z wieńcami w ISSUE-044 (12,5–15%). Płynność na telefonie → lista B.

### Family data
Zmiany w `grobing-code` (9 zmienionych, 11 nowych plików) i w vaulcie (6 zmienionych, 1 nowy) przejrzane przed `git add`: bez baz, kopii, eksportów i zdjęć;
`assets/map/world.json` — Natural Earth (domena publiczna), granice i nazwy krajów; osoby i miejscowości tylko z rdzeni wymyślonych, kraje — nazwy publiczne;
prawdziwych miejscowości ani nazwisk w dodanych liniach brak. Zrzuty emulatora tylko w katalogu tymczasowym sesji. Sieć: pozycja nie łączy się z siecią —
logcat bez sprawdzania współrzędnych (retro 3, R7 dotyczy pozycji z siecią).

### Found, outside the item (`qa`)
- Przykłady z prawdziwym, popularnym nazwiskiem sprzed tej pozycji: `grobing-code/README.md:94` („Grób rodzinny …ów”) i `grobing-vault/05_DESIGN/brand/style-b.md:143`
  (przykład nazwiska rodowego) — wbrew retro 3, R7 („nawet popularne”). Już w publicznej historii; do podmiany na wymyślone rdzenie przy najbliższej pozycji,
  która dotyka tych plików (`docs`).

### Manual verification (stop #2)
**Agent na emulatorze — zrobione** (zrzuty `r12`–`r22`, katalog tymczasowy sesji `40086651-…\scratchpad\emu045\review\`): stany ze specyfikacji, 200% na
360 dp pionowo i 800 dp poziomo, cele i semantyka (`uiautomator`), tryb prezentacji, klatki naprzemiennie (wyżej); tryb samolotowy — `dev` (`18`).

**Autor — odczucie** (2026-10-17, emulator `Grobing_Restore`, build po rundzie 5, wymyślona rodzina):
**Runda 1** (build po rundzie 5): autor zamiast odpowiedzi na kroki — dwie zmiany: *„Dlaczego zamiast Avatar jest "Ja" chciałbym żeby były tam avatary
zamiast inicjałów (no chyba że ktoś nie ma imienia. Dodatkowo chciałbym aby po prostu się te avatary przemieszczały płynnie po mapie bez tych linii szarych
(nie ma potrzeby żadnego dodatkowego efektu)”* → D25 (bez śladu) i — po jednym pytaniu z wariantami — D26 (zdjęcie u każdego, także u „ja”; bez zdjęcia
inicjały) → `dev` runda 6.

**Agent na emulatorze po rundzie 6** (`r23`–`r26`): przycisk „Wymyślone miejsca zamieszkania i portrety” → portrety u osób bez zdjęcia; „ja” miało już zdjęcie
z wcześniejszych testów (obraz kontrolny wirtualnej kamery emulatora), więc pokazuje je zamiast „Ja”; w rozsunięciu Ewa i Marek z portretem, reszta z
inicjałami; ▶ od 1934 — przejazdy bez linii (`r26`). Pełny przebieg: **923 zielonych**, analiza i format czyste. Karta pod mapą zostaje przy „Ja” — jest
wspólna z drzewem (D26: drzewo bez zmian).

**Runda 2** (build po rundzie 6, portrety z przycisku):
Odpowiedź autora (2026-10-17): **„Ok”** — jedna na trzy kroki; sprawdzona na emulatorze, każdy krok osobno:
1. ▶ w karcie — awatary jadą płynnie, bez linii — **ok** (ślad na urządzeniu: ok. 650 klatek mapy i dwa obrazy lądu po zmianie kadru o 20:10–20:11 —
   mapa była odtwarzana i przybliżana po instalacji buildu).
2. Stos → imiona → osoba w środku → „Pokaż na mapie” — **ok, bez śladu na urządzeniu** (nawigacja w aplikacji nie zostawia go w logu). **Decyzja z
   kroku: imiona pod rozsuniętym stosem i linia karty zostają** (w kroku: „„ok” znaczy, że zostają oba”) — [[mapa-migracji]] 9 i 12 bez zmian.
3. Tryb prezentacji z przełącznikiem — **pomiń** (po instalacji buildu z rundy 6 nikt nie otworzył ustawień przesyłania — ostatni `CAST_SETTINGS` w logu o
   19:21, przy zrzutach `qa`; zapisane, nie blokuje — tryb sprawdzony przez `qa` na emulatorze przy 100% i 200%, `r16`–`r22`).

**Lista B — telewizor i telefon** ([[ISSUE-032-mvp-install]] → *Hand checks*, retro 4 R4; `docs` przenosi):
- B — mapa migracji z kanapy: kontury krajów, okręgi 32 dp z inicjałami, rok w rogu — czytelne na telewizorze;
- B — płynność ▶ na mapie na telefonie (emulator: 9–20% wolnych klatek, zakres jak drzewo z wieńcami);
- B — TalkBack na mapie: okrąg, stos, skupienie, przełącznik;
- B — tryb prezentacji mapy z przełącznikiem „Drzewo · Mapa” w sterowaniu (D24) — stop #2 krok 3: **pomiń**;
- B — „Pokaż na mapie” z widoku osoby i rozsunięcie stosu z imionami — stop #2 krok 2: **ok bez śladu na urządzeniu**.

### Verdict (`qa`, self-check, 2026-10-17)
**APPROVED — z uwagami.** Każde AC ma test widżetu albo czystej funkcji i przejście na emulatorze (AC-2 w brzmieniu przepisanym przez D2); bez zmiany bazy;
923 testy zielone, analiza i format czyste; dwa przeglądy `ui` (MAJOR i wszystkie MINOR poprawione); dane rodziny w zmianach — brak; klatki bez regresji
rund 3–6 w pomiarze naprzemiennym. **Czego szukałem i nie znalazłem:** nachodzenia przy 200% w obu orientacjach (po rundzie 4), skoku okręgu przy
przejeździe (mutacje: 92 px i 34 dp na starym kodzie), nazw miejsc na mapie (D18), śladu po przejeździe (D25), znaku „Ja” zamiast zdjęcia (D26),
prawdziwych miejscowości i nazwisk w dodanych liniach. **Uwagi:** krok 3 stopu #2 — pomiń, krok 2 — ok bez śladu (lista B); płynność i czytelność na
telewizorze — lista B; dwa starsze przykłady z prawdziwym nazwiskiem poza tą pozycją (*Found, outside the item*).
