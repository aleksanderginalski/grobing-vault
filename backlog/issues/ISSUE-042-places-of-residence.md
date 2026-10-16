---
title: "ISSUE-042 — Places of residence: where and when a person lived, from a country down to an address"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-16
verdict-reviewer: self-check
source: "`/pm` 2026-10-16 — pomysł autora (miejsca zamieszkania i mapa migracji) i doprecyzowanie „od ogółu do szczegółu”; przed instalacją decyzją autora · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-16
---

# ISSUE-042 — Gdzie kto mieszkał i kiedy

> Autor w `/pm`: *„gdzie dana osoba mieszkała w którym momencie swojego życia, aby zrobić taką mapę, jak kto się przemieszczał po mapie
> świata”*, a o dokładności: **od ogółu do szczegółu** — kraj (punkt w środku kraju) → miasto (środek miasta) → adres; *„w ramach
> lokalizacji powinno to wystarczyć (…), ale można dodać miasto (centrum miasta) albo wręcz dokładną ulicę”*. Ta pozycja to **dane i
> formularz**; widok mapy to [[ISSUE-045-migration-map]]. **Przed instalacją**, bo zmienia bazę ([[2026-10-16-retro-04]] → zasady terminu).

## Prior art
- Kanon genealogii ma na to gotowy fakt: **zamieszkanie z datą i miejscem** — [GEDCOM 7 `INDI-RESI`](https://gedcom.io/terms/v7/INDI-RESI)
  (miejsce w `PLAC` i/lub `ADDR`, data w `DATE`); Gramps traktuje zamieszkanie jako zdarzenie
  ([dyskusja](https://gramps.discourse.group/t/residence-as-an-event/7277)).
- **Miejsce jako lista jednostek od najmniejszej do największej** (ulica, miasto, kraj) — konwencja `PLAC`
  ([Ancestris — Places](https://docs.ancestris.org/books/user-guide/page/places)); współrzędne dopisuje się z najdokładniejszej znanej
  jednostki (np. [GeoFinder](https://pypi.org/project/geofinder/0.2.4/) — gazeter geonames.org).
- U nas: `events` ma już daty z dopiskiem, także „między” (lata od–do, [[FR-004-data-z-dopiskiem]]), i miejsce — **tylko jako tekst**
  ([[data-model]]). Nowa wartość `EventType` na końcu nie wymaga migracji (`database.dart`), ale **miejsce ze współrzędnymi i poziomem
  dokładności** to nowa tabela — zmiana schematu, która tylko dokłada.

## What to build
- W widoku osoby sekcja „Gdzie mieszkał(a)”: lista zamieszkań w kolejności lat; dodanie, poprawa, usunięcie (z potwierdzeniem).
- Zamieszkanie: **lata** (od–do z dopiskiem: około, przed, po, między; może być bez daty) i **miejsce** na jednym z poziomów: **kraj · miasto ·
  adres** — punkt z poziomu (środek kraju, środek miasta, punkt adresu) i nazwa.
- Projekt: `ui` — specyfikacja i makieta przed planem (nowy ekran wyboru miejsca). **Kandydaci na makiecie, przed rekomendacją** (retro 2, R6):
  - **skąd współrzędne bez sieci:** lista krajów i miast w aplikacji (otwarte dane, np. Natural Earth — już w [[ADR-007-poland-map-bundled-data]] —
    i GeoNames) · dotknięcie mapy · wyszukiwarka online (wtedy nazwa miejscowości wychodzi z telefonu — [[NFR-005-dane-nie-opuszczaja-telefonu]]);
  - **granice się zmieniały:** nazwa z czasu zamieszkania, dzisiejsza czy obie — w polskiej rodzinie to reguła, nie wyjątek;
  - czy miejsce urodzenia i zgonu (dziś tekst) dostają ten sam wybór miejsca — `⚠️ OPEN`, decyzja autora na stopie #1.

## Acceptance Criteria
- **AC-1** *Given* osoba *When* dodaję zamieszkanie z samym krajem i latami „ok. 1930 – ok. 1945” *Then* zapis ma poziom „kraj”, punkt w środku
  kraju i te lata.
- **AC-2** *Given* to zamieszkanie *When* doprecyzowuję miasto, a potem adres *Then* poziom i punkt się zmieniają, a zamieszkanie zostaje jedno.
- **AC-3** *Given* brak sieci *When* wybieram kraj albo miasto *Then* wybór działa.
- **AC-4** *Given* kopia z wersji sprzed tej pozycji *When* odtwarzam ją w nowej *Then* dane są kompletne (test migracji z poprzedniej wersji,
  próbne odtworzenie — DoD), a kopia z nowej wersji niesie zamieszkania i miejsca.

## Notes
- Przykłady w specyfikacji, makiecie i testach tylko z rdzeni wymyślonych (`family-data.md`, retro 3 R7) — także nazwy miejscowości.
- Zależna: [[ISSUE-045-migration-map]] (widok na tych danych).

## Implementation plan
> `planning`, 2026-10-16. **Pozycja z ekranem:** specyfikacja [[zamieszkanie]] v1 (nowa), [[osoba]] v2.5 (element 9a), [[wpis-osoby]] v5.9 (element
> 9b). **Makieta:** `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/b20ca21c-7265-44c6-afbf-089c44ba2555/scratchpad/makieta-042.html`
> (ramki 1–5, kandydaci A i N; wymyślone osoby i miejscowości).

> **Stop #1 — 2026-10-16, autor: *„jest ok, ale skończmy tutaj sesję … i kontynuujmy w nowej”*.** Zapisane jako przyjęcie rekomendacji **A1** (adres
> jako tekst) i **N2** (nazwa z tamtego czasu + miejsce dziś) oraz decyzji z planu. Odpowiedź nie nazwała A i N wprost, więc `pm` **potwierdza A1 i N2
> jednym pytaniem na starcie następnej sesji**, zanim ruszy `dev` (krok 0).

### Decisions for stop #1 (author)
- **A — adres** ([[zamieszkanie]] *Open* 1): **A1 (rekomendacja)** adres jako tekst, punkt w środku miejscowości · A2 + „Popraw punkt na mapie” przy
  sieci · A3 wyszukiwarka adresów w sieci (wpisany adres wychodzi z telefonu).
- **N — nazwa sprzed zmiany granic** ([[zamieszkanie]] *Open* 2): N1 tylko dzisiejsza nazwa z listy · **N2 (rekomendacja, FamilySearch)** miejsce z
  listy + opcjonalna „Nazwa z tamtego czasu”.

### Decisions taken in the plan (visible at stop #1, no question)
- **Lista miejsc budowana na komputerze, poza gitem** (G1): `assets/places/places.db` (SQLite) robi narzędzie `tool/places/` z pobranych plików
  (GeoNames, Natural Earth), jak `tool/cemeteries/`. `*.db` jest w `.gitignore` (blok danych rodziny), a strażnik treści sprawdza tylko pliki, których
  `.gitignore` nie ukrywa (`family-data-guard.ps1`: *„untracked files .gitignore does not hide”*) — lista nazw wszystkich miejscowości (także tych z listy
  rdzeni) nie trafia do repo i **strażnik zostaje bez zmian**. Koszt: przed buildem z czystego klonu krok „zbuduj listę” (README); pliki źródłowe
  z datą pobrania w README. Odrzucone G2 (plik w repo + wyjątek strażnika dla jego ścieżki) — dziura w jedynej ochronie publikacji.
- **Zakres listy** (krok 0 `dev`, pomiar): kraje — Natural Earth admin-0 (nazwa polska `NAME_PL`, punkt etykiety); miejscowości — GeoNames: **wszystkie
  miejscowości Polski, Ukrainy, Białorusi i Litwy** (granice sprzed 1945) + **świat: miasta > 1000 mieszkańców** (`cities1000`); polskie nazwy z
  `alternateNames` (`pl`). Próg: lista ≤ 15 MB, wyszukiwanie 3 liter < 100 ms na emulatorze. Za duża → świat do `cities5000`, potem `cities15000`.
- **Model (ADR-020, ≥3 opcje — pisze łańcuch `planning` → `docs`):** **R1 (wybrane)** — jedna nowa tabela `residences`: osoba · od (dopisek
  `exact`/`about` + rok/miesiąc/dzień, puste dozwolone) · do (jak od) · miejsce **w wierszu** (poziom `country`/`locality`/`address`, nazwa dziś,
  jednostka, kraj — kod i nazwa polska, punkt, id z listy) · nazwa z tamtego czasu (N2) · adres (A1). Nazwy zapisane słowami, nie tylko jako id z
  listy — kopia (= eksport, [[ADR-018-export-is-the-backup]]) czyta się bez listy z aplikacji. Odrzucone: R2 (`residences` + tabela `places` — miejsce
  współdzielone; jedna instancja użycia, generalizacja przed drugą — wróci przy miejscu urodzenia, *Open* 3) · R3 (`events` z typem `residence` — jeden
  dopisek na parę dat i „między” = `BET`, a okres to `FROM … TO …`). Bez twierdzeń (`assertions`) — D28. Schemat **v12 → v13** (`createTable`).
- Osoby nie da się dziś usunąć (brak takiej ścieżki w `lib/data`), więc bez kaskady; klucz obcy do `persons`.

### Steps (`dev`)
0. **Krok 0 — lista miejsc i pomiar:** `tool/places/build_places.dart` (wejście: pliki GeoNames `PL`, `UA`, `BY`, `LT`, `cities1000`, `alternatenames`
   tych krajów; Natural Earth admin-0 10m) → `assets/places/places.db`: tabele `countries` (ISO, nazwa PL, punkt etykiety) i `places` (id GeoNames,
   nazwa wyświetlana — polska, jeśli jest, klucz wyszukiwania bez polskich znaków i wielkości liter, kraj, jednostka 1. rzędu słowami, punkt), indeks
   na kluczu. W *Dev report*: liczba wierszy, rozmiar pliku i paczki, czas wyszukiwania (najgorszy przypadek: 1 litera i 3 litery). **Suchy przebieg
   strażnika** (`echo … git add -- assets/places/places.db`) — plik ignorowany, nic do sprawdzenia. README → *Lista miejsc* (źródła, data, licencje, komenda).
1. **Schemat v13:** tabela `residences` (R1) w `lib/data/database.dart`, krok `_from12To13` (`createTable`), `make-migrations` (schemat v13, testy
   generowane), `build_runner`.
2. **Dane:** `lib/data/residences.dart` — odczyt zamieszkań osoby w kolejności D4 ([[zamieszkanie]]), zapis listy zamieszkań **w transakcji zapisu
   osoby** (D5: wstaw / zmień / usuń razem z „Zapisz”), „ostatnio wybrane” (do 5 różnych miejsc z `residences`, najnowsze); `lib/data/places.dart` —
   otwarcie listy z assetu (kopia do katalogu aplikacji przy pierwszym użyciu albo odczyt w pamięci — decyzja `dev` z pomiarem), wyszukiwanie od
   początku słów, kraje osobno.
3. **Ekrany według [[zamieszkanie]]:** sekcja 9a w `lib/app/person/person_screen.dart`; sekcja 9b w `lib/app/grave/person_form_screen.dart` (lista
   w stanie formularza, okno „Odrzucić wpis?” liczy zmiany zamieszkań jako wpisane dane); nowe `lib/app/person/residence_screen.dart` (okno A —
   blok daty z dopiskiem `dokładnie`/`około` przez `lib/app/widgets/date_block.dart`) i `lib/app/person/place_picker_screen.dart` (wybór B z podpisem
   źródła); format lat okresu w `lib/app/dates.dart` (`1946–1978`, `ok. 1925 – 1945`, `od 1946`, `do ok. 1925`).
4. **Przejście AC na emulatorze** (stała lista `dev`): każdy stan z *States* [[zamieszkanie]] ze zrzutem, tekst 200% na 360 dp, semantyka i cel dotyku,
   tryb samolotowy przy wyborze (AC-3). Przed pierwszą instalacją na `Grobing_Restore`: **kopia obecnych danych** (cmentarz dodany tam 2026-10-16 poza
   agentem zostaje — odtworzenie przywraca ten sam stan); po instalacji nad v12 — migawka `pre-update/grobing-v12.db` z [[ISSUE-041-google-play-and-safe-update]].

### Files likely touched
`grobing-code`: `tool/places/build_places.dart` (nowy) · `assets/places/places.db` (generowany, **poza gitem**) · `pubspec.yaml` (asset) ·
`lib/data/database.dart`, `database.g.dart`, `database.steps.dart`, `drift_schemas/grobing/drift_schema_v13.json`, `test/drift/grobing/generated/*`
(generowane) · `lib/data/residences.dart`, `lib/data/places.dart` (nowe) · `lib/app/person/person_screen.dart`, `residence_screen.dart`,
`place_picker_screen.dart` (nowe) · `lib/app/grave/person_form_screen.dart` · `lib/app/dates.dart` · `README.md` (*Lista miejsc*, *Baza danych* — v13).
`grobing-vault` (`docs` przy zamknięciu): ADR-020 · `04_ARCHITECTURE/data-model.md` (tabela `residences`) · `backup-format.md` (v13 w kopii).

### AC mapping
| AC | Kroki | Dowód |
|---|---|---|
| AC-1 — kraj + „ok. 1930 – ok. 1945” | 0, 1–3 | test zapisu (poziom `country`, punkt etykiety kraju), test widżetu wiersza; zrzut |
| AC-2 — miasto, potem adres → jedno zamieszkanie | 2, 3 | test: zmiana zamieszkania nie dokłada wiersza; zrzut karty i widoku |
| AC-3 — kraj i miasto bez sieci | 0, 2 | test wyszukiwania na assecie bez sieci; przejście w trybie samolotowym |
| AC-4 — kopia sprzed pozycji odtwarza się | 1 | test migracji v12 → v13 z danymi; próbne odtworzenie kopii v12 w v13 |

### Tests (`qa`)
- Migracja v12 → v13 z wymyślonymi danymi (wszystkie tabele bez zmian, `residences` pusta); wygenerowane v1…v12 → v13; odtworzenie kopii v12 w v13.
- `residences.dart`: zapis w transakcji osoby (nieudany zapis osoby nie zostawia zamieszkań), kolejność D4, „ostatnio wybrane”, walidacja „Do” ≥ „Od”.
- `places.dart`: polska nazwa przed miejscową, bez polskich znaków i wielkości liter, od początku słów, kraje osobno, brak wyników; na **wymyślonej**
  mini-liście w teście (nie na prawdziwym assecie).
- Widżety: sekcja 9a (pełna, pusta, kraj, N2 z „dziś”), 9b (karty, „Dodaj miejsce”), okno A (błędy, kraj chowa adres, usunięcie z potwierdzeniem),
  wybór B (ostatnie, wyniki, brak, podpis źródła); `meetsGuideline` (retro 3, R2); tekst 200%.
- Pełny `flutter test --timeout 120s`, `flutter analyze`, `dart format`.

### Manual verification
**Agent na emulatorze (przed stopem #2):** krok 4 z *Steps* — zrzuty wszystkich stanów, 200%, tryb samolotowy; migracja v12 → v13 nad danymi
(liczby wierszy bez zmian, migawka v12); próbne odtworzenie na drugim emulatorze z odciskiem zgodnym.

**Autor — odczucie (najwyżej 3, na emulatorze):**
1. U wymyślonej osoby w widoku „Dodaj miejsce”: sam kraj z „ok.” i miejscowość z listy — czy wiersze w widoku czytają się jak notatka?
2. Wybór miejsca: znajdź kilka dowolnych miejscowości (polskich i za granicą) — czy łatwo trafić we właściwą przy tej samej nazwie?
3. (przy N2) Wpisz nazwę z tamtego czasu — czy „dziś: …” w drugiej linii jest jasne?

### Out of scope
Mapa migracji ([[ISSUE-045-migration-map]]) · miejsce urodzenia i zgonu ([[zamieszkanie]] *Open* 3) · A2/A3, jeśli nie wybrane · „do dziś” jako osobny
znak (D3) · eksport GEDCOM (`RESI` z `FROM`/`TO`, `PLAC` + `MAP`, `ADDR` — mapa pól zapisana w ADR-020 na później) · tabela `places` współdzielona (R2).

### Obali (falsifiers)
- Lista za duża albo wyszukiwanie za wolne po zawężeniu do `cities15000` → STOP, decyzja o zakresie.
- Zbyt wiele miejscowości z notatek nie ma na liście (autor zobaczy przy przepisywaniu) → wtedy pozycja na rozszerzenie zakresu (dodatkowe kraje).
- Strażnik w suchym przebiegu widzi `places.db` → STOP przed jakimkolwiek `git add`.

### Sources
[GEDCOM 7 `INDI-RESI`](https://gedcom.io/terms/v7/INDI-RESI) · [GEDCOM 7 — type Date](https://gedcom.io/terms/v7/type-Date) (okres `FROM`/`TO` vs `BET`/`AND`) ·
[Family Locket — historical place names in FamilySearch](https://familylocket.com/adding-historical-place-names-in-familysearch) ·
[GeoNames — Creative Commons](https://wiki.creativecommons.org/wiki/GeoNames) (CC BY 4.0) · [[ADR-007-poland-map-bundled-data]] (Natural Earth).

## Dev report
> `dev`, 2026-10-16. **Stop #1 potwierdzony:** w `/pm` na pytanie „Czy potwierdzasz A1 i N2?” autor: *„Tak”* — adres jako tekst (A1), nazwa z tamtego
> czasu obok miejsca z listy (N2). Flutter 3.41.1 (przypięty) · `flutter analyze` czyste · `dart format` czyste. Testów nie pisałem (`qa`).

### Changed
- **Krok 0 — lista miejsc:** `tool/places/build_places.dart` (nowy) → `assets/places/places.db` (**poza gitem**, `*.db`). Tabele `meta`, `countries`
  (ISO, nazwa PL, punkt etykiety), `units` (jednostka 1. rzędu słowami), `places` (id = kolejność wyników, `geonames_id`, nazwa, kraj, jednostka, punkt
  w dziesięciotysięcznych stopnia), `words` (klucz bez polskich i innych łacińskich znaków, miejsce, „od początku nazwy”), `short_keys` (gotowe pierwsze
  wyniki dla 1–2 liter). `pubspec.yaml` — asset; README → nowa sekcja **Lista miejsc** (zakres, licencje, budowa, źródła z datą) i *Baza danych* → v13.
- **Krok 1 — schemat v13:** tabela `residences` (R1: okres od–do z dopiskiem, poziom `country`/`locality`/`address`, miejsce słowami w wierszu, punkt,
  `geonames_id`, `name_then`, `address`; dwa `CHECK`: adres ⇔ poziom `address`, kraj ⇔ brak `geonames_id`), indeks `residences_person`, krok
  `_from12To13` (`createTable` + `createIndex`), `drift_schema_v13.json` i wygenerowane `schema_v13.dart` (`make-migrations`), `build_runner`.
- **Krok 2 — dane:** `lib/data/residences.dart` (nowy) — `residencesOf` (kolejność D4), `inStayOrder`, `writeResidences` (różnica: usuwa, zmienia tylko
  zmienione, dokłada; sprawdza dopiski, „Do” ≥ „Od” — `notBefore` — i adres tylko w miejscowości), `recentPlaces`, `stayQualifiers`;
  `lib/data/places.dart` (nowy) — `PlaceList` (otwarcie tylko do odczytu przez mmap, `search`, `searchCountries`), `placeWords`/`placeKey` (wspólne z
  narzędziem); `lib/data/person_view.dart` — `PersonView.residences` i tabela w obserwowanych.
- **Krok 3 — ekrany według [[zamieszkanie]]:** `lib/app/person/residence_screen.dart` (nowy — okno A, teksty wierszy i kart, sekcja 9b
  `ResidencesFormSection`); `lib/app/person/place_picker_screen.dart` (nowy — wybór B); `lib/app/person/place_list_asset.dart` (nowy — kopia assetu do
  `places/` w katalogu aplikacji); `person_screen.dart` — sekcja 9a po „Datach”, „Dodaj miejsce” → poprawa z oknem od razu; `person_form_screen.dart` —
  lista w stanie formularza, zapis przez `AlsoWrite` razem ze zdjęciami (D5), zmiany zamieszkań liczą się do „Odrzucić wpis?”, parametr
  `addResidenceAtStart`; `widgets/date_block.dart` — trzy opcje (lista dopisków, bez podglądu pojedynczej daty, `onNext` z ostatniego pola);
  `dates.dart` — `stayYears`; `dev/frame_log.dart` — `measureLog` (tylko z `FRAME_LOG`, nigdy w release).

### Step 0 — the list (measured)
| Wariant | Miejscowości | Słowa | Plik | Wynik |
|---|---|---|---|---|
| 4 kraje całe + świat `cities1000`, wszystkie zapisy łacińskie wsi | 280 322 | 573 466 | 21,6 MB | ponad próg |
| jw., ale z zapisów wsi tylko te z polską literą | 280 322 | 385 848 | 17,9 MB | ponad próg — **falsyfikator planu**: świat do `cities5000` |
| **4 kraje całe (125 567) + świat `cities5000` (62 675)** | **188 242** | **243 747** | **11,7 MB** | **w progu 15 MB** — przyjęty |

239 krajów (Natural Earth z kodem ISO), 3705 jednostek. Pominięte: 105 miejscowości terytoriów bez własnego kraju w Natural Earth (departamenty
zamorskie Francji i podobne). Budowa ok. 25 s. **Suchy przebieg strażnika** (`echo … git add -- assets/places/places.db`) przeszedł, `git check-ignore`
→ `.gitignore:7 *.db`.

**Czas wyszukiwania** (najgorszy przypadek = najczęstszy początek w liście):
| | 1 litera | 2 litery | 3 litery (7,6 tys. słów) |
|---|---|---|---|
| PC | 0,2–0,3 ms (`short_keys`) | 0,2 ms | 2,1 ms |
| emulator, pierwsze zapytanie po starcie (zimny dysk) | 6,4–11 ms | ≤ 3,7 ms | **10,7–13,1 ms** |
| emulator, kolejne | ok. 1 ms | ok. 1 ms | ok. 1 ms |

Pierwsza wersja zapytania łączyła każde pasujące miejsce przed sortowaniem: **89 ms** dla 3 liter na zimnym dysku emulatora (próg 100 ms, ale w wątku
interfejsu). Po zmianie (sortowanie i obcięcie do 30 na samym indeksie słów, potem 30 miejsc) — 10,7 ms. **Otwarcie listy:** pierwsze po instalacji
(kopia 11,7 MB) 504 ms; w każdym kolejnym uruchomieniu 152–179 ms (wczytanie assetu do porównania rozmiaru), asynchronicznie — klatki pierwszego i
drugiego otwarcia wyboru te same (6 vs 7 i 3 vs 4 wolnych na ok. 25, przejście z klawiaturą). **Klatki przy pisaniu** w wyborze: 4% wolnych (2/46),
najdłuższy build 18,6 ms — tyle samo co pisanie w wyszukiwaniu cmentarzy na tym samym buildzie (4%, 34,5 ms); szum emulatora tego dnia jak w
ISSUE-039, więc porównanie obok siebie, nie liczba sama.

**Paczka:** lista w APK po kompresji **6,9 MB** (41% z 11,7 MB); APK x86_64 profile 41,3 MB vs build odniesienia sprzed pozycji 34,3 MB (świeży build).

### Emulator pass (`Grobing_Restore`, build profile `0.9.0`, `FRAME_LOG`)
- **Przed instalacją:** kopia `files/` aplikacji do katalogu tymczasowego sesji (`574c5666-…\scratchpad\emu042\before-042-files.tar`; wymyślone dane i
  cmentarz dodany 2026-10-16 poza agentem) i APK odniesienia (`ref-0.9.0-profile.apk`).
- **Migracja v12 → v13 nad danymi:** 751 wierszy, **te same liczby w każdej tabeli**, `residences` 0, `user_version` 13; migawka
  `pre-update/grobing-v12.db` (v12) obok `grobing-v11.db`.
- **Stany z *States*** (zrzuty w `emu042\shots\`): widok bez miejsc (1 + 4) · okno nowe (fokus i klawiatura numeryczna w „Od”, „Gotowe” nad
  klawiaturą) · menu dopisku tylko „dokładnie · około” · podgląd „→ ok. 1930 – ok. 1945” · `next` z „Do” otwiera wybór · wybór pusty bez ostatnich
  (sama podpowiedź) · wybór z „Ostatnio wybrane” · wyniki (miejscowości, potem „Kraje”) · brak wyników (element 21) · okno „kraj” bez pola „Adres” ·
  okno z karty (wartości, „Usuń to miejsce”) · okno błąd („Koniec nie może być przed początkiem.” i „Wybierz miejsce.”, kolor + ikona, fokus na
  pierwszym) · formularz bez miejsc i z miejscami (także w trybie **nowy grób**) · widok z miejscami (kolejność D4, wiersz bez lat na końcu z pustą
  kolumną) · N2 („…, Polska” / „dziś: …, Litwa”; karta „· dziś Litwa”).
- **AC-1:** kraj + „około 1930 – około 1945” → jeden wiersz `level = country`, `UA`, punkt etykiety 49,72 / 32,14, oba dopiski `about`.
- **AC-2:** ten sam wiersz (`id` 1) → miejscowość z listy → adres „ul. Testowa 3” → `level = address`, `geonames_id` i punkt miejscowości, **wciąż jeden
  wiersz**.
- **AC-3:** tryb samolotowy (`Active default network: none`) — wyszukiwanie i wybór miejscowości działają.
- **D5:** „Usuń to miejsce” → potwierdzenie → karta znika; „Odrzucić wpis?” → „Odrzuć” → w bazie dalej 2 wiersze. Okno: ✕ ze zmianą → „Odrzucić
  zmiany?”. Nowy grób: grób, pochówek, osoba i jej zamieszkanie w jednym „Zapisz”.
- **Tekst 200% / 360 dp** (`font_scale 2.0`, `wm density 480`): lata nad miejscem, wiersz bez lat bez pustej linii, karty rosną, okno — dopisek obok daty
  się mieści, pola poniżej przewijają się nad przyciskami; wybór — wiersze rosną.
- **Semantyka i cel dotyku** (`uiautomator dump`): wiersze widoku bez akcji (`clickable=false`, opis „ok. 1930 – ok. 1945: …”); „Dodaj miejsce”, ✎ karty
  (48 dp, „Popraw miejsce”), pole „Miejsce” (56 dp, „Miejsce: …, zmień”), wiersze wyboru (59 dp) — granice elementu.
- **Błędy znalezione i poprawione w przejściu:** (1) w kolumnie lat 112 dp „ok.” zostawało na końcu linii, a rok spadał niżej → twarde spacje po „ok.”, „od”,
  „do” i przed myślnikiem (łamie się tylko za „–”); (2) przy 200% linia w wyborze kończyła się na „·” → `joinPlaceLine` (twarda spacja za „·”, jak w bazie
  cmentarzy), to samo w linii karty i w polu miejsca; (3) zapytanie 89 ms (wyżej).

### Deviations
- **D-dev 1 — kolejność wyników** (specyfikacja jej nie mówi): dopasowanie od początku nazwy przed dopasowaniem w środku, potem liczba mieszkańców z
  wagą (Polska ×10, Ukraina, Białoruś, Litwa ×3), stolica i siedziby jednostek, alfabet. Bez wagi 3 litery dawały najpierw duże miasto dalekiego kraju, a
  dopiero potem polskie miasto o tym samym początku.
- **D-dev 2 — szukanie także po innych nazwach:** polskie nazwy historyczne z GeoNames i polskie zapisy wsi z czterech krajów (tylko te z polską literą) są
  słowami do szukania; wiersz pokazuje nazwę z listy (jak inne nazwy cmentarzy w bazie cmentarzy). Kto szuka nazwy sprzed 1945, trafia na dzisiejszą
  miejscowość i wpisuje starą w „Nazwa z tamtego czasu”.
- **D-dev 3 — nazwy jednostek:** polskie z GeoNames, skróty „woj.” i „obw.” jak w specyfikacji; 6 jednostek bez polskiej nazwy w GeoNames (4 obwody
  Białorusi, 2 miasta wydzielone Ukrainy) — wpisane w narzędziu; jednostki spoza czterech krajów często po angielsku albo w języku kraju.
- **D-dev 4 — wiersze dla połączeń, których specyfikacja nie pokazuje:** adres + N2 → „{adres}, {nazwa z tamtego czasu}” / „dziś: {miejscowość}, {kraj}”;
  kraj + N2 → „{nazwa z tamtego czasu}” / „dziś: {kraj} — cały kraj”. Karta skraca „dziś …” do samego kraju, gdy nazwa z tamtego czasu zaczyna się
  dzisiejszą nazwą (makieta: „Zmyślin, Polska · dziś Ukraina”).
- **D-dev 5 — „Ostatnio wybrane”** biorą najpierw miejsca z kart tego formularza (jeszcze niezapisane), potem z bazy — przy przepisywaniu kilku
  zamieszkań jednej osoby drugie ma już pierwsze miejsce pod ręką (D6). Nagłówek „Ostatnio wybrane”, w drugiej linii jednostka i kraj.
- **D-dev 6 — teksty spoza specyfikacji:** treść okien „Usunąć to miejsce zamieszkania?” — „Zniknie z wpisu po „Zapisz”.” i „Odrzucić zmiany?” —
  „Zmiany w tym miejscu nie zostaną zapisane.”; podpowiedź pola wyboru „Kraj albo miejscowość”; opis ✕ „Zamknij”.
- **D-dev 7 — pliki spoza listy planu:** `lib/app/person/place_list_asset.dart` (warstwa danych zostaje bez Fluttera, bo `tool/` dzieli z nią słowa),
  `lib/data/person_view.dart`, `lib/dev/frame_log.dart` (pomiar).
- **D-dev 8 — lista otwierana w wątku interfejsu** (synchronicznie, `sqlite3`): przy zmierzonych ≤ 13 ms bez osobnego wątku. Gdyby na telefonie było
  wolniej — przenieść wyszukiwanie do `Isolate`.

### Found, outside the item
- **Kraje pod 30 miejscowościami przy krótkim zapytaniu** (element 20 — „pod miejscowościami”): 3 litery nazwy kraju dają 30 miejscowości i kraj
  dopiero pod nimi (trzeba przewinąć); przy pełnej nazwie kraj stoi pod kilkoma wierszami i mieści się nad klawiaturą. Do przeglądu `ui` — np. kraj
  przed miejscowościami, gdy nazwa kraju pasuje od początku.
- **Pierwsze uruchomienie wyboru w każdym starcie wczytuje 11,7 MB assetu** do porównania rozmiaru (150–180 ms, asynchronicznie). Tańsza droga
  (znacznik wersji listy obok kopii) — gdyby kiedyś przeszkadzało.

### For `qa`
- **12 testów czerwonych z 777 po v13 — wszystkie do aktualizacji, nie regresje:** 10 przypina schemat 12 albo dokładny zestaw tabel (`database_test`,
  `data_state_test`, `data_state_screen_test` — „12”, siedem testów `restore_service_test` — tabela `residences` w zestawie po migracji), 2 w
  `person_screen_test` przewijają o stały krok i nowa sekcja niżej zdejmuje nagłówek „Jak łączy się ze mną” z leniwej listy (widok na emulatorze
  pokazuje go jak przedtem).
- Testy z planu (*Tests*). Teksty lat mają **twarde spacje** (` `) po „ok.”, „od”, „do” i przed „–”, a linie miejsca — za „·”.
  `writeResidences` rzuca `ArgumentError` dla dopisku spoza „dokładnie · około”, „Do” przed „Od” i adresu przy kraju.
- Próbne odtworzenie kopii v12 w v13 i kopii v13 z zamieszkaniami (*Manual verification*).
- **Stan emulatora `Grobing_Restore`:** build profile z `FRAME_LOG` (baza v13, migawki v11 i v12); zamieszkania: 2 u wymyślonej osoby z kroku AC-1/AC-2
  i 1 u nowej, wymyślonej osoby w nowym grobie na cmentarzu dodanym tam poza agentem (sam cmentarz bez zmian); kopia sprzed pozycji — wyżej. Ustawienia
  zmienione do przejścia: `stylus_handwriting_enabled 0` (nakładka rysika Gboard), `show_ime_with_hard_keyboard 1` (klawiatura ekranowa przy sprzętowej);
  tekst i gęstość z powrotem domyślne, tryb samolotowy wyłączony.

### Round 2 — after the `ui` review (specification v1.1)
- **MAJOR → D8:** `PlaceList.searchCountries` oddaje dwie grupy (`CountryMatches`: nazwa zaczyna się od tekstu · dalsze słowo); wybór od 3 liter stawia
  pierwszą grupę **na górze, bez nagłówka**, pod miejscowościami zostaje druga (przy 1–2 literach — wszystkie) pod „Kraje”. Emulator: 3 litery nazwy
  kraju → kraj w pierwszym wierszu (wcześniej pod 30 miejscowościami).
- **MINOR:** karta skraca „dziś …” do kraju tylko, gdy **cała** część nazwy z tamtego czasu przed pierwszym przecinkiem równa się dzisiejszej nazwie
  (bez polskich znaków i wielkości liter); twarda spacja po „dziś” (karta) i „dziś:” (wiersz widoku); twarde spacje po „i”, „w”, „z” w elemencie 21, w
  treści obu okien i w etykiecie „Nazwa z tamtego czasu”, a za „·” w podpisie źródła. Emulator, 200%: linia karty łamie się przed „·”, „dziś” zostaje
  przy nazwie.
- `flutter analyze` czyste, `dart format` bez zmian.

### Round 3 — the end from the next residence (specification v1.2, D12 — the author at stop #2)
- `lib/data/residences.dart` — `impliedEnds(inOrder)`: zamieszkanie z „Od” i bez „Do” kończy się „Od” najbliższego o późniejszym początku (z jego dopiskiem
  i dokładnością); wpisane „Do” wygrywa; bez „Od”, ten sam początek albo ostatnie — bez końca. **Tylko przy odczycie** — `writeResidences` bez zmian, w bazie
  zostaje to, co wpisane.
- Widok (9a) i karta (9b) pokazują lata z tym końcem (`stayYears(from, to ?? implied)`), opis dla czytnika też; okno — pod „Do” linia „Puste — do początku
  następnego miejsca.” (`DateBlock.note`).
- **Dla [[ISSUE-045-migration-map]]:** mapa bierze ten sam koniec z `impliedEnds`. **Dla `docs`:** ADR-020 — koniec wyliczony, nie zapisany (D12).
- Emulator: Mateusz — „od 2024” (kraj) i „od 2026” (miejscowość) przez okno → karty i widok „2024–2026” / „od 2026”, czytnik „2024–2026: …”; w bazie oba
  wiersze z pustym „Do”.

## Verification
> `qa`, 2026-10-16. **Stop #2 — odpowiedzi autora** (emulator `Grobing_Restore`):
> 1. sekcja w widoku po „Dodaj miejsce” (kraj z „około”, miejscowość) — **„ok”**; zrzut autora pokazuje karty w formularzu, a wpis został **niezapisany**
>    (baza bez zmian) — widok po „Zapisz” sprawdził agent (wyżej), od autora: ocena kart;
> 2. wybór miejsca — **„ok”** (przed poprawką D8 z przeglądu `ui`; kraj na górze po 3 literach autor zobaczy w użyciu — lista B);
> 3. „Nazwa z tamtego czasu” i „dziś: …” — **„ok” bez śladu na urządzeniu** (w niezapisanym wpisie autora nie było nazwy z tamtego czasu);
> 4. pytanie autora przy kroku 1 → **decyzja D12** (*„tak, zróbmy to jak rekomendujesz”*): pobyt bez „Do” kończy się początkiem następnego, wyliczone przy
>    odczycie (*Round 3*); krok domykający D12 — **„pomiń”**.
>
> **Werdykt: APPROVED (self-check, z uwagami)** — AC-1…AC-4 spełnione dowodami niżej (testy od dotknięcia do wiersza w bazie, migracja i odtworzenie w testach,
> przejście na emulatorze). Uwagi: próbne odtworzenie na urządzeniu niezrobione (powód niżej) → lista A; trzy odpowiedzi bez śladu na urządzeniu → lista B;
> zakres poszerzony decyzją autora o D12 (bez zmiany bazy).

### `ui` review (subagent, 2026-10-16)
Spec v1 + style B v1.31, 33 zrzuty, kod pięciu plików, kontrast z `theme.dart`. **1 MAJOR, 3 MINOR — wszystkie poprawione w rundzie 2** (wyżej) i sprawdzone
przez `qa` na emulatorze i w testach:
- **MAJOR** — kraje zawsze pod miejscowościami (błąd specyfikacji v1, nie `dev`): kraj, jedyna droga do „sam kraj” (AC-1), poza widokiem nad klawiaturą →
  [[zamieszkanie]] v1.1 D8;
- **MINOR** — karta porównywała początek nazwy (ukrywała zmianę nazwy) → D10; „dziś” na końcu linii przy 200%; brak twardych spacji po jednoliterowych
  słowach w nowych tekstach ([[style-b]] reguła 6, v1.32).

Zgodne: elementy i kolejność 1–22, każdy stan z *States* (tryb „nowy grób” — z *Dev report*), role kolorów (akcent tylko w nagłówkach, ✎, ikonie „Dodaj
miejsce”, jedynym wypełnionym przycisku, fokusie, wyborze w menu, „Wróć”), kontrast (tekst 10,98/10,02; pomocniczy 5,50/5,01; obrys 3,40/3,10; błąd 6,45),
cele dotyku (48–59 dp), kolor nie jest jedynym nośnikiem (błąd: ramka + ikona + tekst; wybór w menu: znacznik), 200% na 360 dp, ton. **Przyjęte
odstępstwa:** D-dev 1–6 → [[zamieszkanie]] **v1.1** (D9 kolejność i inne nazwy, D10 wiersze N2, D11 „Ostatnio wybrane”, teksty okien), oba stany zbudowane
poza specyfikacją (lista się otwiera / nie otworzyła); [[style-b]] **v1.32** — reguła 6: linia nie kończy się „·” ani dopiskiem („ok.”, „od”, „do”,
„dziś”), lata okresu łamią się za „–” (druga instancja po [[cmentarze]] D25). D-dev 7–8 poza oceną `ui`.

### Automated
`dart format` → `flutter analyze` (czyste) → `flutter test --timeout 120s`: **820 zielonych** po rundzie 3 (przed pozycją 777; 12 czerwonych po v13 poprawione, 43 nowe — w tym D12: `impliedEnds` w `residences_test` i widok, karta, okno w `residence_screens_test`).
- **Poprawione pod v13 (12):** wersja 13 i tabela `residences` w `database_test`, `data_state_test`, `data_state_screen_test` (16 zer na ekranie „Stan
  danych”); `'residences': 0` w siedmiu testach odtworzenia starszych kopii (`restore_service_test`); dwa testy `person_screen_test` przewijały o stały krok
  przez nagłówek, który nowa sekcja niżej zdejmowała z leniwej listy — teraz przewijają do nagłówka, a wiersz łańcucha dotykają po `ensureVisible`.
- **Nowe — warstwa danych:**
  - `test/drift/grobing/migration_test.dart` — **AC-4** v12 → v13 z danymi (osoby, zdarzenie, grób z pinezką, pochówek, twierdzenia): wszystko jak było,
    `residences` pusta z indeksem, przyjmuje wiersz osoby sprzed migracji; oba `CHECK` (adres ⇔ poziom `address`, kraj ⇔ brak id GeoNames) odmawiają;
    `foreign_key_check` pusty. Migracje bez danych v1…v12 → v13 z `make-migrations` — zielone;
  - `test/backup/restore_service_test.dart` — **AC-4** kopia **v12** (wygenerowany schemat v12) odtwarza się w v13: każda tabela i liczba jak w kopii,
    `residences` = 0, osoba bez miejsc; kopia **v13** z dwoma zamieszkaniami (kraj z „około”, adres z nazwą z tamtego czasu) odtwarza się z tym samym
    odciskiem i każdym polem;
  - `test/data/residences_test.dart` (8) — **AC-1** kraj + „ok. 1930 – ok. 1945” → poziom `country`, punkt kraju; **AC-2** to samo zamieszkanie → miejscowość
    → adres: jeden wiersz, ten sam `id`; **D5** nieudany zapis osoby nie zostawia ani osoby, ani zamieszkań; lista formularza staje się zapisaną (usunięte
    znika, zmienione się zmienia, niezmienione zostaje, nowe dochodzi, cudze zostają); **D4** kolejność; **D6** „ostatnio wybrane” (5 różnych, najnowsze);
    **D3** odmowa „przed”/„między”, końca przed początkiem i adresu przy kraju; `notBefore`;
  - `test/data/places_test.dart` (7) — **AC-3** na wymyślonej mini-liście w układzie narzędzia (`test/support/place_fakes.dart`, nigdy prawdziwy asset):
    od początku słów, nie w środku słowa; bez wielkości liter, polskich i innych łacińskich znaków; nazwa z listy pokazana, inna nazwa (miejscowa,
    historyczna) znajduje; te same nazwy rozróżnione jednostką i krajem; 1–2 litery z `short_keys` = wynik zakresu; brak wyników; kraje osobno.
- **Nowe — ekrany** `test/app/person/residence_screens_test.dart` (10, wymyślona lista przez `places:`): linia karty według D10 i kraje według D8 (3 litery — na górze, 2 — pod „Kraje”); **AC-1** i **AC-2** od dotknięcia do wiersza w bazie
  (menu dopisku tylko „dokładnie · około”, podgląd lat, kraj na górze wyników bez nagłówka, „Ostatnio wybrane”, pole „Adres” tylko przy miejscowości, zapis dopiero
  z „Zapisz”); błędy okna z ikoną; ✕ → „Odrzucić zmiany?”; „Usuń to miejsce” z potwierdzeniem + „Odrzucić wpis?” → w bazie bez zmian; wybór bez ostatnich,
  brak wyników, podpis źródła, wstecz bez wyniku; 9a — kolejność, „cały kraj — miejscowość nieznana”, N2 „dziś: …”, adres nad krajem, opisy dla czytnika;
  9a bez miejsc → poprawa z oknem od razu; **retro 3 R2** — `androidTapTargetGuideline`, `labeledTapTargetGuideline` i „każdy przycisk ma akcję dotknięcia”
  w widoku, formularzu, oknie i wyborze; **tekst 200% na 360 dp** bez przepełnienia w wierszach, kartach, oknie i wyborze (pasek zakładek przepełnia się w
  czcionce testowej, każda litera 1 em — na emulatorze przy 200% mieści się; test go odfiltrowuje, każde inne przepełnienie jest błędem).
- `test/app/dates_test.dart` — `stayYears`: `1946–1978`, `ok. 1925 – 1945`, `od 1946`, `do ok. 1925`, twarde spacje.

### Agent on the emulator
Przejście `dev` (*Dev report* → *Emulator pass*) — stany, AC-1…AC-3, D5, 200%, semantyka — i do tego:
- **Migracja nad danymi:** v12 → v13, 751 wierszy bez zmian, migawka `pre-update/grobing-v12.db`.
- **Kopia w tle po migracji:** `backup.json` — ostatnia udana **17:00:39 UTC, w tle, bez błędu**, po ostatniej zmianie bazy (16:50, trzy zamieszkania);
  `grobing-kopia-040.age` w Pobranych z tą godziną.
- **Próbne odtworzenie na urządzeniu — nie zrobione:** hasła testowego kopii z sesji ISSUE-040 nie ma (nie zapisuje się haseł), na `Grobing_Restore` jest
  cmentarz dodany poza agentem, a `Medium_Phone` ma dane testowe autora — odtworzenie zastąpiłoby jedne albo drugie. Ścieżkę odtworzenia v12 → v13 i kopii
  z zamieszkaniami pokrywają testy wyżej; na urządzeniu — lista A w [[ISSUE-032-mvp-install]] (już jest od ISSUE-041).

### Family data in the changes
31 plików paczki kodu: żadnych `*.db`, kopii, eksportów ani zdjęć; `assets/places/places.db` ignorowany (`.gitignore:7 *.db`). Przykłady w kodzie, testach i
README tylko z rdzeni wymyślonych („Zmyślin”, „Wymyślowo”, „Kraj Przykładowy”, „ul. Przykładowa 3”); prawdziwe nazwy jednostek tylko jako dane narzędzia
(`_unitPolish`). **Suchy przebieg strażnika treści** na 31 plikach kodu i na tej pozycji — przeszedł. Pozycja bez sieci (lista w aplikacji) — logcat z
adresami nie dotyczy.

### For ISSUE-032 → Hand checks
- **A** — odtworzenie kopii **v13 z zamieszkaniami** na urządzeniu, z odciskiem zgodnym: na emulatorze niezrobione — hasła testowego kopii z sesji ISSUE-040 nie
  ma, a odtworzenie zastąpiłoby dane, których agent nie stworzył (cmentarz na `Grobing_Restore`, dane testowe autora na `Medium_Phone`); kopia w tle v13 na
  emulatorze przeszła;
- **A** — pierwsza aktualizacja ze sklepu nad v12: migracja v12 → v13 i migawka `pre-update/grobing-v12.db` na telefonie (na emulatorze — przeszła);
- **B** — sekcja „Miejsca zamieszkania” w widoku osoby po „Zapisz” — autor ocenił karty w formularzu (wpis niezapisany);
- **B** — „Nazwa z tamtego czasu” i „dziś: …” w widoku — „ok” bez śladu na urządzeniu;
- **B** — koniec z następnego miejsca (D12: „od 2024” + „od 2026” → „2024–2026”) — „pomiń”;
- **B** — wybór miejsca na telefonie: kraj na górze po 3 literach (D8, po poprawce z przeglądu `ui`), płynność pisania i czas wyszukiwania (emulator: ≤ 13 ms
  na zimnym dysku; D-dev 8 — przy wolniejszym telefonie wyszukiwanie do `Isolate`).

### Package for `docs`
**`grobing-code`** (31): `README.md` · `pubspec.yaml` · `drift_schemas/grobing/drift_schema_v13.json` · `tool/places/build_places.dart` · `lib/app/dates.dart` ·
`lib/app/grave/person_form_screen.dart` · `lib/app/person/person_screen.dart` · `lib/app/person/place_list_asset.dart` · `lib/app/person/place_picker_screen.dart` ·
`lib/app/person/residence_screen.dart` · `lib/app/widgets/date_block.dart` · `lib/data/database.dart` · `lib/data/database.g.dart` · `lib/data/database.steps.dart` ·
`lib/data/person_view.dart` · `lib/data/places.dart` · `lib/data/residences.dart` · `lib/dev/frame_log.dart` · `test/app/data_state_screen_test.dart` ·
`test/app/dates_test.dart` · `test/app/person/person_screen_test.dart` · `test/app/person/residence_screens_test.dart` · `test/backup/restore_service_test.dart` ·
`test/data/data_state_test.dart` · `test/data/database_test.dart` · `test/data/places_test.dart` · `test/data/residences_test.dart` ·
`test/drift/grobing/generated/schema.dart` · `test/drift/grobing/generated/schema_v13.dart` · `test/drift/grobing/migration_test.dart` ·
`test/support/place_fakes.dart`. **Nie wchodzi:** `assets/places/places.db` (ignorowany, `*.db` — celowo, README → *Lista miejsc*).

**`grobing-vault`** (tej pozycji, przed zamknięciem `docs`): `backlog/issues/ISSUE-042-places-of-residence.md` · `05_DESIGN/zamieszkanie.md` (nowy, v1.2) ·
`05_DESIGN/osoba.md` (v2.5) · `05_DESIGN/wpis-osoby.md` (v5.9) · `05_DESIGN/brand/style-b.md` (v1.32) · `00_START_HERE/TRACEABILITY.md` ·
`00_START_HERE/CURRENT_STATE.md` — plus pliki zamknięcia `docs` (ADR-020 z D12 — koniec wyliczony, nie zapisany; `04_ARCHITECTURE/data-model.md`;
`backup-format.md`; DOC_MAP, jeśli dochodzi wiersz).

**`grobing-agents`** — bez zmian.
