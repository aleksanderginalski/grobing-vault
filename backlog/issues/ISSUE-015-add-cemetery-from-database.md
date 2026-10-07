---
title: "ISSUE-015 — Add a cemetery from a bundled cemetery database (OpenStreetMap, offline): search section, preview, satellite link"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
used-by: "[[EPIC-002-wizyta]] (M2 — widok 1)"
user-story: "[[US-002-przepisanie-grobu]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-07
verdict-reviewer: self-check
source: "decyzja autora 2026-10-06 na stopie #1 ISSUE-014 (*„miałem nadzieję, że będziemy to dodawać z jakiejś bazy cmentarzy”*; podział — *„wygląda dobrze”*) · ISSUE-014 → Stop #1 — round 1, D8–D10 · 05_DESIGN/cmentarze.md v2 · 01_INBOX/2026-10-05-plany-cmentarzy.md → Related idea"
created: 2026-10-06
updated: 2026-10-07
---

# ISSUE-015 — Dodanie cmentarza z bazy cmentarzy

> **Decyzja autora 2026-10-06** (stop #1 [[ISSUE-014-home-map-of-poland]]): cmentarz dodaje się z bazy
> cmentarzy, *„aby mieć pewność, że dodajemy odpowiedni cmentarz w odpowiedniej lokalizacji”*. Autor przyjął
> podział: ISSUE-014 robi mapę i ręczne dodanie, a ta pozycja dokłada bazę zaraz po niej (kolejność w
> `CURRENT_STATE.md`). Pomiary, na których stoi: ISSUE-014 → *Stop #1 — round 1* (falsyfikator: 8 z 8
> cmentarzy autora jest w bazie) i *Decisions for stop #1 — round 2* (D8–D10).

## What to build
1. **Wyciąg cmentarzy Polski z OpenStreetMap** jako zasób aplikacji (ok. 16 tys. cmentarzy, ok. 2 MB),
   z odtwarzającym go skryptem w `tool/`. Każdy cmentarz ma: nazwę (także nazwy dodatkowe: potoczne,
   oficjalne), środek, wyznanie (jeśli jest), **miejscowość do wyświetlenia** (najbliższa z uwzględnieniem
   rangi), **miejscowości w zasięgu jako słowa do szukania** i **województwo** z Natural Earth admin-1
   (ISSUE-014 D9). Duplikaty scalone.
2. **Sekcja „Z bazy cmentarzy”** w wyszukiwarce ([[cmentarze]] element 12): wyniki z województwem i
   wyznaniem, oznaczenie „Dodany” przy cmentarzu, który już jest u autora, podpis „© współtwórcy
   OpenStreetMap (ODbL)” i „Nie ma go w bazie — dodaj ręcznie”.
3. **Podgląd cmentarza z bazy** ([[cmentarze]] element 14): mapa przybliżona do punktu, znicz w obrysie, link
   **„Zobacz zdjęcie satelitarne ↗”** (intencja `geo:`, tylko po dotknięciu — ISSUE-014 D10) i „Dodaj ten
   cmentarz”.
4. **Okno z danymi z bazy** ([[cmentarze]] element 15): nazwa i miejscowość do poprawy przed zapisem, punkt z
   bazy, „Zapisz” bez kroku wskazania.

## Acceptance Criteria
- [ ] Bez sieci wyszukiwarka znajduje cmentarz z bazy po nazwie, po nazwie dodatkowej (potocznej) i po
      miejscowości. Polskie znaki i końcówki odmiany nie są potrzebne ([[cmentarze]] D3).
- [ ] Każdy wynik z bazy pokazuje miejscowość i województwo; ta sama nazwa w dwóch województwach to dwa
      rozróżnialne wyniki.
- [ ] Podgląd pokazuje cmentarz na mapie przed dodaniem. Link otwiera zewnętrzną aplikację map w tym punkcie,
      a bez dotknięcia aplikacja niczego nie wysyła.
- [ ] Dodanie z bazy zapisuje nazwę (poprawioną albo z bazy), miejscowość i punkt z bazy. Na mapie pojawia
      się znicz, a cmentarz w wynikach dostaje „Dodany”.
- [ ] Podpis ODbL jest widoczny przy wynikach z bazy; wyciąg w repo ma licencję ODbL i opis pochodzenia.
- [ ] APK release dalej **nie ma uprawnienia `INTERNET`**.
- [ ] Ekran według specyfikacji `ui` ([[cmentarze]] v2) i wytycznych stylu B.

## Out of Scope
- Kwatery, plany cmentarzy z kwaterami, zdjęcie satelitarne **w aplikacji** i granice cmentarza →
  [[SPIKE-001-map-source-offline]].
- Aktualizacja bazy w aplikacji (z sieci). Nowy wyciąg = nowa wersja aplikacji ze skryptu.
- Identyfikator obiektu OSM w schemacie (zmiana schematu) — punkt wystarcza do „Dodany” i do późniejszego
  dopasowania. Wraca, gdy SPIKE-001 będzie importować granice.
- Granice gmin (PRG / relacje OSM) — zbędne według pomiaru (ISSUE-014 D9).

## Technical Notes
- **Źródło i licencja:** OpenStreetMap (Overpass API, `landuse=cemetery` + `amenity=grave_yard` w granicach
  Polski, miejscowości `place=city|town|village|hamlet|suburb`), [ODbL](https://www.openstreetmap.org/copyright):
  podpis w aplikacji, wyciąg w publicznym repo na ODbL. Województwa: Natural Earth (domena publiczna).
- **Wyniki falsyfikatora** (ISSUE-014): 16 532 obiekty → 16 043 cmentarze po scaleniu, 60% z nazwą, 2,1 MB
  JSON (0,43 MB po kompresji). Potoczna nazwa bywa w `loc_name`; odmiana psuje dopasowanie całych słów; w
  danych są błędy. Stąd podgląd i link.
- **Miejscowość (D9):** najbliższa z uwzględnieniem rangi (zasięg: miasto 12 km, miasteczko 5 km, wieś 2,5 km,
  przysiółek 1,5 km), a do szukania wszystkie w zasięgu. Zmierzone na 8 cmentarzach autora: 7 z 8 do
  wyświetlenia, 8 z 8 do znalezienia, 8 z 8 województw.
- **Testy tylko na publicznych przykładach**, nigdy na cmentarzach autora (`family-data.md`): np.
  „powazki” → Cmentarz Powązkowski (Warszawa), „krakow rakowicki” → Cmentarz Rakowicki (Kraków). Sprawdzenie na
  cmentarzach autora robi agent w pamięci i zapisuje tylko liczbę.
- **Link `geo:`** — sposób wywołania (paczka `url_launcher` albo kilka linii w `MainActivity`) wybiera plan;
  nowa zależność wymaga zgodności z przypiętym Flutterem (ADR-002) i braku wysyłania danych (NFR-005).
- **Wczytanie bazy:** ok. 2 MB przy pierwszym wejściu w wyszukiwarkę; specyfikacja dopuszcza pasek postępu
  powyżej ok. 0,3 s. Do zmierzenia na emulatorze.

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-014-home-map-of-poland]] (mapa, wyszukiwarka z sekcjami, okno, tryb wskazania) | technical | `done` (2026-10-06) |
| specyfikacja `ui` — [[cmentarze]] v2 (elementy 12–15, D16–D20) | design | gotowa (2026-10-06) |
| [[US-002-przepisanie-grobu]] | product | `in-progress` |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP):
- test happy-path dla każdego AC;
- ręczna weryfikacja na emulatorze, w tym tryb samolotowy;
- zapis cmentarza przez API danych z ISSUE-014 (kopia w tle zamawia się sama);
- zero danych rodziny w zmianach — w testach i przykładach wyłącznie publiczne albo wymyślone cmentarze.

## Implementation plan
> `planning`, 2026-10-07. **DoR:** jasny zakres ✅ · powiązana US: [[US-002-przepisanie-grobu]] (AC-1 *Given*
> „cmentarz w aplikacji”) ✅ · krok ścieżki: UJ-001 · 1 (M2) i jego warunek (M1) ✅ · `task-level` ✅.
> **Ekran:** specyfikacja `ui` — [[cmentarze]] v2, elementy 12–15, D16–D21; wytyczne [[style-b]] v1.4; makieta
> v2, ramki 6–8 (wyniki z bazy, podgląd, okno) w katalogu tymczasowym sesji 2026-10-06
> (`makieta-mapa-polski.html`). Pozycja nie zmienia struktury ekranu, więc bez nowej rundy `ui`; trzy
> poprawki tekstu specyfikacji są niżej (D1, D3, D4). **Warstwa danych:** bez zmiany schematu i bez migracji.
> Cmentarz z bazy zapisuje się przez `addCemetery` z ISSUE-014, więc kopia w tle zamawia się sama.
> Odtworzenie kopii z takim cmentarzem sprawdza test `qa`. **Źródło faktu:** cmentarz to miejsce, a nie fakt
> o osobie ([[FR-001-provenance]]), więc bez twierdzeń, jak w ISSUE-014.

### Prior art (sources, not memory)
- **Android, intencje Map Google** ([developer.android.com/guide/components/google-maps-intents](https://developer.android.com/guide/components/google-maps-intents),
  odczyt 2026-10-07): `geo:latitude,longitude?z=zoom` i `geo:0,0?q=latitude,longitude(label)`. Dokumentacja
  zna tylko `z` (przybliżenie) i `q` (miejsce). **Parametru warstwy satelitarnej w `geo:` nie ma.**
- **Google Maps URLs** ([developers.google.com/maps/documentation/urls/get-started](https://developers.google.com/maps/documentation/urls/get-started),
  odczyt 2026-10-07): `map_action=map` z `center`, `zoom` (0–21) i `basemap`, *„The value can be either
  `roadmap` (default), `satellite`, or `terrain`”*. Na Androidzie: *„If Google Maps app for Android is
  installed and active, the URL launches Google Maps in the Maps app […] If the Google Maps app is not
  installed or is disabled, the URL launches Google Maps in a browser”*.
- **OSM, prawa autorskie** ([openstreetmap.org/copyright/pl](https://www.openstreetmap.org/copyright/pl),
  odczyt 2026-10-07):
  - polski podpis to **„© autorzy OpenStreetMap”**;
  - trzeba *„wyraźnie zaznaczyć, że dane dostępne są na licencji Open Database License”*;
  - wyciąg (baza pochodna) rozpowszechnia się *„tylko na podstawie tej samej licencji”*.
- **Falsyfikator z ISSUE-014** (→ *Stop #1 — round 1*), dane w katalogu tymczasowym sesji 2026-10-06:
  - wyciąg Overpass: `osm_cemeteries.json`, stan OSM 2026-10-06T20:13Z;
  - miejscowości: `osm_places.json`;
  - województwa: `ne_10m_admin_1.geojson`;
  - skrypt `gazetteer.py`: scalanie duplikatów, nazwy dodatkowe, wyznanie, dzielnica.
  
  Wyniki: 16 043 cmentarze po scaleniu, 60% z nazwą, 2,1 MB JSON. Miejscowość „najbliższa z uwzględnieniem
  rangi” przeszła 7 z 8, a województwo 8 z 8 (D9 ISSUE-014). **Strona falsyfikatora otwierała zdjęcie
  satelitarne adresem Map Google, nie `geo:`.**

### Falsifier — what is measured and what is not
| Pytanie | Wynik |
|---|---|
| Czy `geo:` pokaże „zdjęcie satelitarne”, jak obiecuje podpis linku? | ❌ **nie** — kanon Androida nie zna parametru warstwy. Mapy Google otworzą się na mapie drogowej albo na ostatnio używanej warstwie. Stąd D1 |
| Czy da się wymusić zdjęcie satelitarne? | ✅ Google Maps URLs, `basemap=satellite` (kanon wyżej). Ten sam rodzaj linku autor używał na stronie falsyfikatora |
| Brzmienie podpisu OSM | „© autorzy OpenStreetMap” (kanon) ≠ „© współtwórcy OpenStreetMap” (specyfikacja). Stąd D3 |
| Surowe dane do wyciągu | ✅ są w katalogu tymczasowym z 2026-10-06, z zapytaniem i stanem OSM. Nie trzeba ich pobierać od nowa (D9) |
| **Nie zmierzone:** czas pierwszego wczytania bazy (ok. 2 MB) na emulatorze | mierzy `dev`, krok 10. Próg obalenia w D5 |
| **Nie zmierzone:** przyrost APK | mierzy `dev`, kroki 0 i 10. Szacunek: ok. 0,45 MB (wyciąg po kompresji) |
| **Nie zmierzone:** czy na emulatorze są Mapy Google | `qa` sprawdza przed stopem #2. Bez nich link otworzy przeglądarkę, i to też jest zachowanie z kanonu |

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego · co ją obali |
|---|---|---|---|
| D1 | **Jaki link pod „Zobacz zdjęcie satelitarne ↗”** (zmienia D10 ISSUE-014 i D18 specyfikacji: tam był `geo:`) | **Adres Map Google** `https://www.google.com/maps/@?api=1&map_action=map&center=<lat>,<lon>&zoom=17&basemap=satellite`, tylko po dotknięciu. Podpis linku zostaje | `geo:` nie wybiera warstwy (kanon), więc podpis obiecywałby coś, czego link nie daje. Adres Map Google otwiera aplikację Mapy w widoku satelitarnym, a bez niej przeglądarkę. **Koszt jest taki sam jak przy `geo:`:** punkt cmentarza (publiczny obiekt z bazy, nie dane rodziny) idzie do Google po dotknięciu. Nowy koszt: link zależy od jednego dostawcy. **Alternatywa:** `geo:` z podpisem „Pokaż w aplikacji map ↗”; wtedy warstwę przełączasz sam, jednym dotknięciem w Mapach. **Obali:** nie chcesz linku do Google — wtedy alternatywa |
| D2 | **Jak otworzyć link** (ISSUE-014 D10 zostawiło to planowi) | **Kilkanaście linii w `MainActivity`**: kanał `grobing/external`, `ACTION_VIEW` z adresem. Brak aplikacji, która go otworzy → komunikat „Nie ma aplikacji, która to otworzy.” | Aplikacja ma już takie kanały (`BackupDocuments`, `BackgroundChannel`). `url_launcher` to nowa zależność przy przypiętym Flutterze ([[ADR-002-flutter-pinned]]): każda nowa paczka to przegląd zgodności. Dla jednego linku to za dużo. Na Androidzie 11+ samo `startActivity` nie wymaga wpisu `<queries>`; brak aplikacji łapie `ActivityNotFoundException`. **Obali:** linków przybędzie i każdy będzie potrzebował czegoś innego. Link do Grobonetu (EPIC-002) użyje tego samego kanału |
| D3 | **Podpis licencji** (poprawka tekstu elementu 12) | **„Dane: © autorzy OpenStreetMap (ODbL)”** | Brzmienie z polskiej strony praw autorskich OSM (kanon wyżej); „(ODbL)” spełnia wymóg wyraźnego oznaczenia licencji. Specyfikację poprawia `ui`. **Obali:** nic — to wymóg licencji |
| D4 | **Miejscowość w wyniku** (rozjazd: D16 specyfikacji mówi o „granicach administracyjnych”) | **Według D9 ISSUE-014, które zatwierdziłeś po D16:** do wyświetlenia najbliższa z uwzględnieniem rangi (zasięg: miasto 12 km, miasteczko 5 km, wieś 2,5 km, przysiółek 1,5 km). **Dzielnica** w nawiasie, gdy miejscowość to miasto albo miasteczko i dzielnica (`place=suburb`) leży bliżej niż 2,5 km. Do szukania wszystkie miejscowości w zasięgu. Województwo z Natural Earth | Pomiar: 7 z 8 do wyświetlenia, 8 z 8 do znalezienia, 8 z 8 województw, bez ciężkich granic gmin. D16 to zdanie sprzed drugiego pomiaru. Specyfikację poprawia `ui`. **Obali:** kolejne cmentarze z notatek z miejscowością, której nie da się znaleźć |
| D5 | **Format i wczytanie bazy** | Jeden plik `assets/cemeteries/poland_cemeteries.json` (nagłówek: źródło, licencja, stan OSM, lista województw; cmentarze jako krótkie tablice). Wczytany przy pierwszym wejściu w wyszukiwarkę: odczyt zasobu i parsowanie w osobnym izolacie (`compute`), wynik trzymany do końca sesji. Indeks szukania liczony od razu: tekst bez polskich znaków dla każdego cmentarza | Specyfikacja dopuszcza pasek postępu po ok. 0,3 s. Izolat nie zamraża klawiatury. **Obali:** pierwsze wczytanie na emulatorze w buildzie release trwa dłużej niż ok. 1,5 s — wtedy wczytanie w tle zaraz po starcie aplikacji albo lżejszy format (wraca na stop #2) |
| D6 | **Duplikaty i „zespół cmentarzy”** | Scalanie jak w falsyfikatorze: ta sama nazwa (albo obie bez nazwy) i ta sama miejscowość w promieniu 300 m. Różne obiekty przy jednej ulicy zostają osobno (D21 specyfikacji) | Zmierzone: 16 532 → 16 043. **Obali:** w wynikach widać pary tego samego cmentarza — wtedy szerszy promień |
| D7 | **„Dodany”** | Twój cmentarz z punktem bliżej niż 100 m od punktu z bazy. Liczone przy wyświetlaniu, bez zapisu identyfikatora OSM (*Out of Scope* pozycji) | Twoich cmentarzy jest ok. 10, a wyników najwyżej 30, więc to tanie. **Obali:** poprawisz punkt dalej niż 100 m — wtedy „Dodany” zniknie i ryzykujesz drugi wpis. Na to jest podgląd i lista twoich cmentarzy nad wynikami |
| D8 | **Kolejność i limit wyników z bazy** | Najpierw cmentarze, w których **każde słowo** zapytania trafia w nazwę albo nazwę dodatkową, potem reszta (trafienia przez miejscowość). W grupie alfabetycznie, według polskiego alfabetu. Najwyżej 30; więcej → „Pokazuję 30 z N — dopisz miejscowość.” | Element 12 specyfikacji. Zapytanie „krakow rakowicki” trafia raz w miejscowość, raz w nazwę, więc wpada do drugiej grupy. Przy 30 wynikach to bez znaczenia |
| D9 | **Skąd surowe dane** | Wyciąg z 2026-10-06 (katalog tymczasowy sesji): ten sam, na którym stoi pomiar 8 z 8. Zapytania Overpass i adresy plików Natural Earth trafiają do README, tak jak przy mapie | Plik w repo da się odtworzyć skryptem z nowego pobrania. Surowe pliki (ok. 75 MB) nie wchodzą do repo. **Obali:** katalog tymczasowy zniknie przed krokiem 1 — wtedy `dev` pobiera na nowo tymi samymi zapytaniami (ok. 2 min) |

**Stop #1 — zatwierdzony przez autora 2026-10-07** (*„D1-D9 - ok”*). Sprawdzenia bazy na cmentarzach autora
autor nie zamówił, więc `qa` go nie robi.

### Scope diff vs the item (to accept at stop #1)
- **zmiana linku:** adres Map Google z warstwą satelitarną zamiast `geo:` (D1). AC-3 („link otwiera
  zewnętrzną aplikację map w tym punkcie”) dalej obowiązuje: otwiera Mapy, a bez nich przeglądarkę;
- **zmiana podpisu:** „© autorzy OpenStreetMap” zamiast „© współtwórcy OpenStreetMap” (D3);
- **+ komunikat o braku aplikacji, która otworzy link** (D2). Specyfikacja tego stanu nie opisuje, więc
  sprawdza go przegląd `ui`;
- **teksty z elementów 12 i 13**, których ISSUE-014 jeszcze nie miało: „Nie ma go w bazie — dodaj
  ręcznie” i „Nie ma cmentarza „…” ani u Ciebie, ani w bazie.”;
- **poza zakresem, jak w pozycji:** identyfikator OSM w schemacie, aktualizacja bazy z sieci, kwatery,
  zdjęcie satelitarne w aplikacji, granice gmin.

### Steps (dev)
0. **Przed zmianą:** rozmiar APK release (arm64) i `aapt dump permissions` → *Dev report*.
1. **Wyciąg** — `tool/cemeteries/extract_cemeteries.dart`, w Dart, na wzór `tool/map/extract_poland.dart`.
   Wejście: katalog z `osm_cemeteries.json`, `osm_places.json` i `ne_10m_admin_1_states_provinces.geojson`
   (w katalogu tymczasowym leży jako `ne_10m_admin_1.geojson`). Logika z `gazetteer.py`, przeniesiona i
   uzupełniona:
   - punkt: środek (`center`) albo węzeł;
   - nazwa: `name` albo `name:pl`; nazwy dodatkowe: `alt_name`, `loc_name`, `official_name`, `short_name`,
     `old_name`, różne od nazwy;
   - wyznanie po polsku z `denomination` / `religion` (słownik z `gazetteer.py`);
   - miejscowość według D4, dzielnica według D4, miejscowości w zasięgu do szukania, województwo:
     punkt w wielokącie 16 województw Natural Earth. Punkt tuż za zgrubną granicą 1:10m → najbliższe
     województwo;
   - scalanie według D6.
   
   Wyjście: `assets/cemeteries/poland_cemeteries.json`. Skrypt wypisuje liczby: wszystkie, z nazwą, rozmiar.
   Porównaj je z falsyfikatorem (ok. 16 043, ok. 60%); każdą różnicę wyjaśnij w *Dev report*. Nagłówek
   pliku: `source` (Overpass, zapytanie, stan OSM), `license` („ODbL 1.0 — © autorzy OpenStreetMap”,
   adres strony praw autorskich), `voivodeships`.
2. **Zasób i licencja:** wpis w `pubspec.yaml` → `assets` z komentarzem o ODbL. README `grobing-code` →
   nowa sekcja „Baza cmentarzy”: pochodzenie, oba zapytania Overpass dosłownie, plik Natural Earth, jak
   odtworzyć, licencja ODbL (baza pochodna na tej samej licencji, podpis w aplikacji).
3. **`lib/data/cemetery_base.dart`** (czysty Dart, bez widżetów):
   - `BaseCemetery`: nazwa (może być pusta), nazwy dodatkowe, punkt `GeoPoint`, wyznanie, miejscowość,
     dzielnica, województwo, miejscowości do szukania;
   - `CemeteryBase.parse(String)`: liczy indeks od razu (`fold` z `lib/app/polish.dart`; jeśli import z
     `app/` do `data/` razi, `fold` i `searchStems` przechodzą do wspólnego pliku bez zmiany zachowania);
   - `search(query) → (wyniki ≤ 30, ile wszystkich)` według D8;
   - `addedAs(BaseCemetery, List<CemeterySummary>) → int?`: id twojego cmentarza bliżej niż 100 m (D7).
   
   Wczytanie zasobu: `rootBundle` + `compute`, raz na sesję, z możliwością podania bazy w testach (jak
   `mapData` w `HomeScreen`).
4. **Wyszukiwarka** (`cemetery_search.dart`), elementy 12–13:
   - sekcja „Z bazy cmentarzy” pod „Twoje cmentarze”: karta, „Cmentarz bez nazwy” w kolorze pomocniczym,
     „Miejscowość (dzielnica) · woj. …” i „· wyznanie”;
   - przy cmentarzu, który już masz, „Dodany” zamiast chevronu, a dotknięcie otwiera jego arkusz;
   - „Pokazuję 30 z N — dopisz miejscowość.”; podpis z D3 pod sekcją; „Nie ma go w bazie — dodaj ręcznie”;
   - element 13: „Nie ma cmentarza „<tekst>” ani u Ciebie, ani w bazie.” + „Dodaj ręcznie”;
   - stany: cienki pasek postępu pod polem, gdy wczytanie trwa dłużej niż ok. 0,3 s; błąd zasobu → zamiast
     sekcji „Baza cmentarzy jest niedostępna — dodaj ręcznie.” (twoje cmentarze i ręczne dodanie działają).
   
   Karta z bazy → podgląd (krok 5) wypchnięty nad wyszukiwarkę, więc wstecz wraca do wyników z tym samym
   tekstem. „Dodaj ten cmentarz” kończy wyszukiwanie nowym wynikiem `AddFromBase(BaseCemetery)`.
5. **Podgląd** — `lib/app/home/base_preview_screen.dart`, element 14:
   - pasek: wstecz + „Cmentarz z bazy”;
   - mapa przybliżona do punktu (+3 jak przy wyborze z wyszukiwarki) ze zniczem `PinLook.outlined`; twoje
     znicze widoczne, nieaktywne. `PolandMap` dostaje dwa parametry: wygląd postawionego znicza i
     początkowy środek z przybliżeniem;
   - karta: nazwa 18 sp, „Miejscowość · woj. …”, wyznanie;
   - link (akcent, podkreślony) przez kanał z kroku 7, z adresem z D1; „Dodaj ten cmentarz” wypełniony.
6. **Okno** (`cemetery_form.dart`), element 15 z bazy:
   - przyciski „Anuluj” · „Zapisz” zamiast „Dalej”;
   - nazwa i miejscowość z bazy; przy cmentarzu bez nazwy puste pole z podpowiedzią „np. Cmentarz
     parafialny”;
   - fokus w pierwszym pustym polu (jest).
7. **Kanał linku:** `ExternalLinks.kt` + rejestracja w `MainActivity` (`grobing/external`, `openUrl`),
   `ACTION_VIEW`; brak aplikacji → `false`. Dart: `lib/app/external_link.dart`; `false` → `SnackBar` „Nie ma
   aplikacji, która to otworzy.” **Bez nowej paczki, bez zmiany manifestu, bez `INTERNET`.**
8. **Ekran główny:** `AddFromBase` → okno z kroku 6 → `addCemetery(nazwa, miejscowość, punkt z bazy)` →
   mapa z nowym zniczem i arkuszem, tak jak po ręcznym zapisie (D11 specyfikacji). Anulowanie → mapa bez
   zmian.
9. **Testy `dev` nie pisze** (to `qa`), ale przykłady w kodzie i w komentarzach tylko publiczne (Powązki,
   Rakowicki) albo wymyślone (`Wymyślin`).
10. **Sprawdzenia:** `dart format`, `flutter analyze`, `flutter test`, APK release:
    - rozmiar po zmianie wobec kroku 0;
    - `aapt dump permissions` bez `INTERNET`;
    - na emulatorze, w buildzie release: czas od wejścia w wyszukiwarkę do wyników z bazy, 3 pomiary,
      próg w D5.

### Files likely touched
- **Nowe:** `tool/cemeteries/extract_cemeteries.dart` · `assets/cemeteries/poland_cemeteries.json` ·
  `lib/data/cemetery_base.dart` · `lib/app/home/base_preview_screen.dart` · `lib/app/external_link.dart` ·
  `android/app/src/main/kotlin/com/grobing/app/ExternalLinks.kt`.
- **Zmienione:** `lib/app/home/cemetery_search.dart` · `cemetery_form.dart` · `home_screen.dart` ·
  `poland_map.dart` · `lib/app/polish.dart` (tylko jeśli `fold` się przenosi) · `MainActivity.kt` ·
  `pubspec.yaml` · `README.md`.
- **Testy (`qa`):** `test/data/cemetery_base_test.dart` (nowy) · `test/app/home/home_screen_test.dart` ·
  `test/repo_invariants_test.dart` · test kopii i odtworzenia z cmentarzem z bazy.

### AC → tests (`qa`)
| AC | Test (happy-path) | Ręcznie |
|---|---|---|
| 1 szukanie bez sieci: nazwa, nazwa dodatkowa, miejscowość; bez polskich znaków i końcówek | jednostkowy na **prawdziwym zasobie**: „powazki” → Cmentarz Powązkowski (Warszawa); „stare powazki” → ten sam przez nazwę dodatkową; „krakow rakowicki” → Cmentarz Rakowicki (Kraków); po samej miejscowości | tryb samolotowy, krok 1 |
| 2 miejscowość i województwo; ta sama nazwa w dwóch województwach rozróżnialna | na zasobie: „powazkowski” daje ≥ 2 wyniki o różnych województwach (falsyfikator: drugi przy wsi w innym województwie); widżet: karta pokazuje „· woj. …” | krok 1 |
| 3 podgląd na mapie; link otwiera mapy w punkcie; bez dotknięcia nic nie wychodzi | widżet: podgląd ma znicz w obrysie i kartę; atrapa kanału: **zero wywołań przed dotknięciem**, po dotknięciu adres z `center=<lat>,<lon>` i `basemap=satellite`; `false` → komunikat | krok 3 |
| 4 dodanie z bazy: nazwa (poprawiona albo z bazy), miejscowość, punkt; znicz; „Dodany” | widżet na bazie w pamięci: wynik → podgląd → „Dodaj…” → poprawa nazwy → „Zapisz” → wiersz w bazie z punktem z bazy; znicz; drugie wyszukanie pokazuje „Dodany” i prowadzi do arkusza | kroki 4–5 |
| 5 podpis ODbL przy wynikach; wyciąg z licencją i pochodzeniem | widżet: tekst z D3 pod sekcją; repo: nagłówek zasobu ma `license` z ODbL i `source`, README ma sekcję „Baza cmentarzy” | krok 1 |
| 6 APK release bez `INTERNET` | istniejący test manifestu + `aapt` na APK release (agent) | — |
| 7 ekran według specyfikacji i stylu B | przegląd `ui` (subagent) ze zrzutów przed stopem #2 | całość |
| DoD: warstwa danych | cmentarz dodany z bazy → kopia → odtworzenie → ten sam wiersz z punktem (istniejące atrapy kopii) | — |
| DoD: zero danych rodziny | wszystkie przykłady publiczne albo wymyślone; grep zmian przed commitem | — |

**Sprawdzenie na Twoich cmentarzach** (ISSUE-014: 8 z 8 na wyciągu falsyfikatora) — na zbudowanym zasobie
powtarza je agent, w pamięci, **tylko jeśli poprosisz w tej sesji** (`family-data.md`). Do vaulta trafia
tylko liczba.

### Manual verification (stop #2) — kroki według miejsca
Emulator `Medium_Phone`, build release (agent instaluje go przed stopem i sprawdza `dumpsys`, czy to nowy
build).
1. **Emulator, tryb samolotowy:** wyszukiwarka → wpisz „powazki”. Pod „Z bazy cmentarzy” jest Cmentarz
   Powązkowski · Warszawa (dzielnica) · woj. mazowieckie, a pod sekcją podpis OSM. Wpisz „powazkowski”:
   czy dwa Powązkowskie da się odróżnić po województwie?
2. **Emulator:** dotknij wyniku → podgląd: mapa przybliżona, znicz w obrysie, karta. Wstecz → wyniki z tym
   samym tekstem.
3. **Emulator, z siecią:** „Zobacz zdjęcie satelitarne ↗” → czy otwiera się zdjęcie satelitarne tego
   miejsca (Mapy Google albo przeglądarka)? Wróć do Grobing.
4. **Emulator:** „Dodaj ten cmentarz” → okno z nazwą i miejscowością z bazy. Zmień nazwę → „Zapisz” →
   mapa z nowym zniczem i arkuszem z Twoją nazwą.
5. **Emulator:** wyszukaj go jeszcze raz → „Dodany”; dotknięcie → jego arkusz.
6. **Emulator:** wpisz coś, czego nie ma (np. „xyzq”) → komunikat i „Dodaj ręcznie”.
7. **Odczucie:** czy pierwsze wejście w wyszukiwarkę jest dość szybkie? Agent poda zmierzony czas.

**Napisz tutaj:** „ok” · „pomiń” · opis błędu przy numerze kroku.

### Out of Scope (this plan)
- Kwatery, plany cmentarzy, zdjęcie satelitarne **w aplikacji**, granice cmentarza →
  [[SPIKE-001-map-source-offline]].
- Aktualizacja bazy z sieci; identyfikator OSM w schemacie; granice gmin.
- Wyszukiwanie osób; „Otwórz cmentarz” → [[ISSUE-012-transcribe-grave-screen]].
- Link do strony praw autorskich OSM z podpisu: kanon mówi „najlepiej link”, ale podpis z „(ODbL)” spełnia
  wymóg. Dotknięcie podpisu byłoby drugim wyjściem z aplikacji.

### For docs at closure
- [[NFR-005-dane-nie-opuszczaja-telefonu]]: pierwsze wyjście z aplikacji, czyli link do Map Google, tylko po
  dotknięciu. Wychodzi punkt publicznego cmentarza z bazy, nie dane rodziny.
- [[ADR-007-poland-map-bundled-data]] → *Follow-ups*: baza cmentarzy z OSM (ODbL) jako drugi wbudowany zbiór
  danych (append-only, bez zmiany decyzji).
- [[cmentarze]] (przez `ui`): D16 według D4 · podpis według D3 · D18 według D1 · komunikat o braku aplikacji
  (D2) · `items` w nagłówku z ISSUE-015.

### Self-check (planning) — said out loud
1. **Kompletność:** zakres, pliki, AC → testy, kroki ręczne, *Out of Scope* ✅.
2. **Spójność:** plan idzie za pozycją, za D8–D10 ISSUE-014 i za specyfikacją. Odstępstwa od specyfikacji
   (D1, D3, D4) mają źródło i idą na stop #1, a nie po cichu do kodu.
3. **Własność:** zapisałem tylko tę sekcję, `status: in-progress`, poprawkę zależności (ISSUE-014 jest
   `done`) i swoje kolumny macierzy. `cmentarze.md` nie ruszałem, bo należy do `ui`.
4. **Warstwa danych:** bez schematu i bez migracji; zapis przez istniejące API; test kopii z odtworzeniem w
   planie `qa`; źródło faktu nie dotyczy (miejsce, nie osoba).
5. **Wystarczalność — czego plan nie ma:**
   - czasu wczytania bazy nikt nie zmierzył na telefonie, więc D5 ma próg i plan B;
   - błędów w danych OSM plan nie poprawia. Łagodzą je podgląd, link i poprawa nazwy;
   - **jakość miejscowości na kolejnych cmentarzach z notatek** jest znana tylko na 8. Obala ją D4.

## Dev report
> `dev`, 2026-10-07. Flutter 3.41.1 (przypięty) ✅. `flutter analyze` czyste, `dart format` ✅. Testy: 283 ✅,
> 3 ❌ — wszystkie trzy to istniejące testy ekranu głównego, które otwierają wyszukiwarkę bez bazy (→ *For qa*).

### Step 0 — APK release before any change: ✅
arm64 (`--target-platform android-arm64`): **23 585 339 B**. `aapt dump permissions`: bez `INTERNET`.

### What was built
- **Wyciąg:** `tool/cemeteries/extract_cemeteries.dart` → `assets/cemeteries/poland_cemeteries.json`:
  - stan OSM 2026-10-06T20:13Z; 16 532 obiekty → **16 040 cmentarzy**, 60% z nazwą, 1 907 305 B;
  - falsyfikator miał 16 043; różnica 3 bierze się ze scalania według miejscowości liczonej z rangą (D4), a nie
    najbliższej;
  - 50 cmentarzy tuż za zgrubną granicą Natural Earth 1:10m dostało najbliższe województwo; wszystkie mają
    miejscowość;
  - nagłówek: `source`, `license` (ODbL 1.0 — © autorzy OpenStreetMap), `osmBase`, `voivodeships`, `kinds`,
    `fields`;
  - wiersze posortowane jak wyniki (polski alfabet), więc aplikacja tylko to sprawdza.
- **Baza w aplikacji:** `lib/app/home/cemetery_base.dart`. Zawiera `BaseCemetery`,
  `CemeteryBase.fromJson`/`load` (izolat), `search` (D8, limit 30), `addedAs` (100 m, D7), `distanceMetres`.
- **Wyszukiwarka** (`cemetery_search.dart`):
  - sekcja „Z bazy cmentarzy”, „Dodany”, „Pokazuję 30 z N — dopisz miejscowość.”;
  - podpis „Dane: © autorzy OpenStreetMap (ODbL)”, „Nie ma go w bazie — dodaj ręcznie”, element 13;
  - pasek postępu po 0,3 s, błąd zasobu;
  - karta z bazy: `BaseCemeteryCard` w `cemetery_card.dart`.
- **Podgląd** (`base_preview_screen.dart`): mapa przybliżona (+3) ze zniczem w obrysie, karta, link, „Dodaj ten
  cmentarz”. `PolandMap` dostał `placedLook` i `focus`.
- **Okno** (`cemetery_form.dart`): tryb `fromBase` — „Zapisz” i podpowiedź „np. Cmentarz parafialny”.
- **Link:** `ExternalLinks.kt` (kanał `grobing/external`, `ACTION_VIEW`, tylko `https://`) i
  `lib/app/external_link.dart` (`openExternalUrl`, `satelliteUrl`). Bez nowej paczki i bez zmiany manifestu.
- **Ekran główny:** `AddFromBase` → okno → `addCemetery` z punktem z bazy → znicz i arkusz (`_showSaved`, wspólne
  z ręcznym zapisem).
- `pubspec.yaml` (zasób z komentarzem ODbL), README → „Baza cmentarzy”.

### Checks (dev, host Windows + emulator `Medium_Phone_API_36.1`, build release x64)
| Co | Wynik |
|---|---|
| **Czas pierwszego wczytania bazy** (log z buildu pomiarowego, 3 razy) | pierwsza wersja: **1 651 / 1 293 / 1 454 ms** — na progu D5. Po poprawce (niżej, *Deviations* 2): **550 / 434 / 476 ms**; sam odczyt pliku 63–89 ms. Pasek postępu mignie (> 0,3 s) |
| APK release arm64, ten sam sposób budowania co krok 0 | **24 207 027 B (+621 688 B ≈ +0,62 MB)** — to skompresowany zasób (1,9 MB → 0,62 MB w APK) |
| `aapt dump permissions` po zmianie | bez `INTERNET` (te same uprawnienia co w kroku 0) |
| **Link (D1) na emulatorze** | dotknięcie → aplikacja **Mapy Google**, **widok satelitarny**, Cmentarz Powązkowski z bliska (widać aleje). „Wstecz” wraca do Grobing |
| Przepływ na emulatorze | „powazki” → oba Powązkowskie (Warszawa (Żoliborz) · woj. mazowieckie; Marczów · woj. dolnośląskie) i Wojskowy; podpis OSM; podgląd; „Dodaj ten cmentarz” → okno z nazwą i miejscowością z bazy → „Zapisz” → znicz przy Warszawie i arkusz; ponowne „powazki” → „Dodany” |
| Grep zmian wzorcami z notatek rodziny (poza plikiem bazy, który ma wszystkie cmentarze Polski) | 0 |

### Deviations from the plan
1. **`cemetery_base.dart` leży w `lib/app/home/`, a nie w `lib/data/`** — obok `poland_map_data.dart`, bo to
   wbudowany zasób tylko do odczytu, jak mapa (`rootBundle`). Dzięki temu `fold` nie musiał się przenosić.
2. **Wydajność (D5):** pierwszy pomiar dał 1,3–1,65 s, czyli próg D5. Pomiar na hoście pokazał, że czas zjada
   sortowanie po polskim alfabecie i `fold`. Zmiany:
   - skrypt zapisuje bazę już posortowaną, a aplikacja sprawdza kolejność jednym przebiegiem i sortuje tylko
     wtedy, gdy ktoś poda listę nieposortowaną (testy);
   - `fold` przechodzi po kodach znaków zamiast tworzyć napis dla każdej litery. Zachowanie bez zmian
     (`polish_test` przechodzi).
   
   Wynik: 0,43–0,55 s. Plan B z D5 (wczytanie zaraz po starcie) nie był potrzebny.
3. **„↗” jako ikona `north_east`**, bo Android rysuje znak U+2197 jako kolorowe emoji (widać na emulatorze).
   Tekst linku jest podkreślony, ikona w akcencie. Czytnik ekranu czyta „Zobacz zdjęcie satelitarne, w innej
   aplikacji”.
4. **Błąd zapisu cmentarza z bazy** → pasek „Nie udało się zapisać. Spróbuj jeszcze raz.” (tekst z elementu 17).
   Specyfikacja opisuje ten błąd tylko w trybie wskazania. Do przeglądu `ui`.
5. **Błąd zasobu bazy:** tekst ze specyfikacji i przycisk „Dodaj ręcznie” (wypełniony, gdy nie ma twoich
   trafień). Specyfikacja podaje sam tekst.
6. **Podgląd:** mapa nad kartą (kolumna), a nie pod nią, więc znicz nigdy nie chowa się pod kartą.
7. **Miejscowość w oknie** = miejscowość z bazy bez dzielnicy („Warszawa”), bo to Twój zapis, a nie adres.
8. **Zapytania Overpass w README są odtworzone** z budowy plików z 2026-10-06 (te same filtry i tryb wyjścia),
   **nie wykonane ponownie**: oba serwery Overpass zwróciły 2026-10-07 błąd (504, błąd serwera). Plik w repo
   pochodzi z wyciągu z 2026-10-06.
9. **Emulator:** `Medium_Phone` wrócił ze starego snapshotu z buildem debug z 2026-10-06 (inny klucz), więc
   build release się nie instalował. Odinstalowałem go (na emulatorze były tylko wymyślone dane) i
   zainstalowałem release.

### For qa
- **3 testy w `home_screen_test.dart` do poprawy przez `qa`:** AC-2, AC-3 i „adding by hand”. Otwierają
  wyszukiwarkę bez `base:`, więc ekran czyta prawdziwy zasób. W czasie symulowanym testu to wczytanie się nie
  kończy, pasek postępu animuje się bez końca i `pumpAndSettle` przekracza limit. Podaj
  `base: Future.value(CemeteryBase([...]))` z publicznymi albo wymyślonymi cmentarzami.
- **Haki do testów:**
  - `HomeScreen(base:, openUrl:)`, `CemeterySearchScreen(base:, openUrl:)`, `BasePreviewScreen(openUrl:)`;
  - `CemeteryBase([...])`, `CemeteryBase.fromJson`, `search`, `addedAs`, `satelliteUrl`, stała `osmAttribution`;
  - testy na **prawdziwym zasobie** mogą czytać plik przez `File` i `CemeteryBase.fromJson`.
- **Publiczne przykłady na zasobie:**
  - „powazki” → Cmentarz Powązkowski · Warszawa (Żoliborz) · woj. mazowieckie, nazwa dodatkowa „Stare
    Powązki”;
  - drugi Cmentarz Powązkowski · Marczów · woj. dolnośląskie;
  - „krakow rakowicki” → Cmentarz Rakowicki · Kraków (Krowodrza) · woj. małopolskie.
- **Emulator:** zainstalowany build release x64 z 2026-10-07. Podczas sprawdzenia dodałem jeden cmentarz
  (Cmentarz Powązkowski). Przed stopem #2 wyczyść dane aplikacji, żeby autor zaczął od pustej mapy.
- **Kroki ręczne:** jak w planie (*Manual verification*), bez zmian.

### Fixes after the ui review and qa (dev, 2026-10-07)
- **qa:** tekst linku w podglądzie nie zawijał się i wychodził poza kartę przy dużej czcionce. Teraz tekst może
  się zawinąć.
- **ui MAJOR 1:** przybliżenie podglądu zmienione z +3 na **+1,5**. Według pomiaru recenzenta na zasobie miasto
  jest w kadrze przy 96% cmentarzy (przy +3 przy 29%). Przy wyborze własnego cmentarza z wyszukiwarki zostaje
  +3.
- **ui MINOR 2 i 5:** okno otwiera się **nad podglądem**, więc „Anuluj” wraca do podglądu. Podgląd zapisuje
  cmentarz przez `onSave`. Błąd zapisu pojawia się w karcie podglądu, w kolorze błędu i z `error_outline`, a
  okno wraca z wpisanymi wartościami. Wynik wyszukiwarki to teraz `AddedFromBase(id, punkt)`; zapis z ekranu
  głównego zniknął.
- **ui MINOR 3, 4 i 6:**
  - tytuł podglądu ma 20 sp, w600;
  - link ma co najmniej 48 dp i rośnie z czcionką;
  - „Pokazuję 30 z N…” stoi tuż pod nagłówkiem sekcji.
- **ui NIT 7–10:**
  - separator `' · '` (`joinPlaceLine`), więc linia nie kończy się kropką;
  - strzałka skaluje się z tekstem;
  - odstęp między grupami wynosi 24 dp;
  - „Dodany” jest wyrównany do kolumny strzałek.

## Verification
> `qa`, 2026-10-07 (`verdict-reviewer: self-check`, do czasu krytyka ISSUE-003).

### Automated — `flutter test`: 309 ✅ · `flutter analyze`: czyste · `dart format`: ✅
Nowe i zmienione testy, 23:
- **`test/app/home/cemetery_base_test.dart`** (nowy, 15):
  - na **prawdziwym zasobie**: licencja ODbL i podpis „© autorzy OpenStreetMap”, pochodzenie, 16 województw,
    > 15 tys. cmentarzy;
  - kolejność pliku = kolejność wyników (aplikacja nie sortuje);
  - AC-1: „powazki”, „stare powazki” (nazwa dodatkowa), „krakow rakowicki”, „marczow” (sama miejscowość);
  - AC-2: dwa Cmentarze Powązkowskie w różnych województwach; miejscowość i województwo niepuste;
  - dzielnica „Warszawa (Żoliborz)”, wyznanie;
  - na wymyślonych cmentarzach: kolejność D8 (nazwa, potem miejscowość, alfabetycznie), limit 30 z liczbą
    wszystkich, „Cmentarz bez nazwy” w kolejności i po miejscowości, puste zapytanie;
  - D7: „Dodany” poniżej 100 m (56 m tak, 167 m nie, bez punktu nie), `distanceMetres`;
  - D1: adres z `center`, `zoom=17`, `basemap=satellite`.
- **`test/app/home/home_screen_test.dart`** (+6, 3 poprawione: dostają bazę, element 13 ma nowy tekst):
  - AC-1, AC-2, AC-5: sekcja z bazy z miejscowością, dzielnicą, województwem i wyznaniem; podpis OSM; „Nie ma
    go w bazie — dodaj ręcznie”; nazwa dodatkowa; cmentarz bez nazwy;
  - AC-3: podgląd ze zniczem w obrysie i kartą; **zero wywołań linku przed dotknięciem**; po dotknięciu
    adres w punkcie z warstwą satelitarną; brak aplikacji → komunikat; wstecz → te same wyniki;
  - AC-4: okno z nazwą i miejscowością z bazy i „Zapisz” (bez „Dalej”); poprawiona nazwa zapisana z
    punktem z bazy; znicz i arkusz; „Dodany” prowadzi do arkusza;
  - D8: „Pokazuję 30 z 35 — dopisz miejscowość.”;
  - *States*: pasek postępu po 0,3 s; błąd zasobu → tekst, twoje cmentarze i „Dodaj ręcznie” działają;
  - przegląd `ui`: „Anuluj” zostaje w podglądzie; błąd zapisu z ikoną; okno wraca z wpisanymi wartościami.
- **`test/backup/restore_service_test.dart`** (+1, **DoD warstwy danych**): cmentarz dodany z prawdziwej bazy
  (Powązki), z poprawioną nazwą, wraca z kopii z punktem z bazy.
- **`test/repo_invariants_test.dart`** (+1, AC-5): zasób w `pubspec.yaml` z adnotacją ODbL, README → „Baza
  cmentarzy” z licencją i adresem strony praw autorskich, skrypt wyciągu w repo.

### Agent checks on the emulator (`Medium_Phone_API_36.1`, build release x64)
| Co | Wynik |
|---|---|
| AC-6: `aapt dump permissions` na APK release arm64 | bez `INTERNET` ✅ (te same uprawnienia co przed zmianą) |
| Rozmiar APK | +0,62 MB (*Dev report*) |
| Czas pierwszego wczytania bazy | 0,43–0,55 s (*Dev report*) |
| D1: link | Mapy Google, widok satelitarny cmentarza z bliska; „Wstecz” wraca do Grobing ✅ |
| Przepływ: wyniki → podgląd → okno → zapis → „Dodany” | ✅ (zrzuty w katalogu tymczasowym sesji) |
| Podgląd przy czcionce systemowej 130% | link mieści się, nic się nie ucina ✅ |
| Podgląd cmentarza z innego województwa (Marczów) po zmianie przybliżenia | widać Wrocław i Poznań, czyli jasne, gdzie leży ✅ |
| Dane aplikacji przed stopem #2 | wyczyszczone (`pm clear`), pusta mapa |

### ui review (subagent bez historii, ze zrzutów emulatora)
Runda 1: **CHANGES REQUESTED**, bez BLOCKER-ów: 1 MAJOR (przybliżenie podglądu), 5 MINOR, 7 NIT. Odstępstwa
z *Dev report* 3, 5, 6 i 7 przyjęte, a 4 przyjęte częściowo (dalej w MINOR 5). Poprawki → *Fixes after the ui review and
qa*.

Runda 2 (nowe zrzuty po poprawkach): **APPROVED**. MAJOR 1, MINOR 2–6 i NIT 7–10 są zamknięte. `ui` wpisał
ustalenia do [[cmentarze]] v2.2 (D22–D25) i do [[style-b]] v1.5 (strzałka linku zewnętrznego jako ikona). Zostają
tematy dla autora (*Notes*).

### DoD lines specific to Grobing
- Test happy-path dla każdego AC ✅ (tabela *AC → tests* wyżej).
- Warstwa danych: bez zmiany schematu i bez migracji. Zapis przez `addCemetery`, a odtworzenie z kopii
  sprawdza test ✅. Źródło faktu nie dotyczy, bo cmentarz to miejsce.
- **Zero danych rodziny w zmianach:** grep kodu, testów i vaulta wzorcami z notatek (nazwiska, miejsca) daje 0.
  Pomijam plik bazy, bo ma wszystkie cmentarze Polski i niczym nie wyróżnia cmentarzy rodziny. Przykłady w
  testach są publiczne (Powązki, Rakowicki, Marczów) albo wymyślone (Wymyślin) ✅.
- Kopia w tle: zapis idzie przez API danych, więc kopia zamawia się sama (test ISSUE-010 dalej przechodzi) ✅.

### Manual (stop #2) — autor, 2026-10-07, emulator `Medium_Phone` (build release, czysta instalacja)
| Krok | Odpowiedź autora |
|---|---|
| 1 wyniki z bazy w trybie samolotowym, dwa Powązkowskie po województwie, podpis OSM | „tak” |
| 2 podgląd, wstecz do tych samych wyników, drugi Powązkowski jako inne miejsce | „tak” |
| 3 zdjęcie satelitarne w Mapach Google, powrót | „tak” |
| 4 „Anuluj” zostaje w podglądzie; zapis z poprawioną nazwą → znicz i arkusz | „tak” |
| 5 „Dodany” prowadzi do arkusza | „tak” |
| 6 podpowiedź o limicie i zawężenie miejscowością | „tak” |
| 7 brak wyników → komunikat i „Dodaj ręcznie” | „tak” |
| 8 szybkość pierwszego wejścia w wyszukiwarkę | „jest dobrze” |

**Sprawdzone ze stanem urządzenia:** po krokach na ekranie emulatora zostało wyszukiwanie z kroku 6
(„parafialny krakow” → „Pokazuję 30 z 40”). Liczba wyników spadła z 3740 do 40.

### Verdict
**APPROVED** (self-check, z uwagami), 2026-10-07:
- każde AC ma test happy-path;
- przegląd `ui` w rundzie 2 dał APPROVED;
- stop #2: 8 z 8 kroków „tak”;
- zmiany bez danych rodziny;
- APK bez `INTERNET`.

Uwagi niżej (*Notes*) nie blokują pozycji.

### Package for docs (one commit per repo, explicit list)
- **`grobing-code`:**
  - nowe: `tool/cemeteries/extract_cemeteries.dart`, `assets/cemeteries/poland_cemeteries.json`,
    `lib/app/home/cemetery_base.dart`, `lib/app/home/base_preview_screen.dart`, `lib/app/external_link.dart`,
    `android/app/src/main/kotlin/com/grobing/app/ExternalLinks.kt`, `test/app/home/cemetery_base_test.dart`;
  - zmienione: `lib/app/home/cemetery_search.dart`, `lib/app/home/cemetery_card.dart`,
    `lib/app/home/cemetery_form.dart`, `lib/app/home/home_screen.dart`, `lib/app/home/poland_map.dart`,
    `lib/app/polish.dart`, `android/app/src/main/kotlin/com/grobing/app/MainActivity.kt`, `pubspec.yaml`,
    `README.md`, `test/app/home/home_screen_test.dart`, `test/backup/restore_service_test.dart`,
    `test/repo_invariants_test.dart`.
- **`grobing-vault`:** ta pozycja, `00_START_HERE/TRACEABILITY.md`, `05_DESIGN/cmentarze.md` (v2.1 i v2.2),
  `05_DESIGN/brand/style-b.md` (v1.5), oraz pliki zamknięcia `docs`.
- **`grobing-agents`:** brak zmian.

### Notes (do not block)
- **Skracanie słów daje szum przy nazwach miejscowości:** „krakow” → rdzeń „krak” trafia też w dzielnice
  „…Krakowskie” (Bielsko-Biała), widać to w kroku 6. To ta sama rodzina co literówki niżej. Specyfikacja D3
  przewiduje próg 6 liter, gdy trafień będzie za dużo — do decyzji autora.
- **Cmentarze dla zwierząt** są w bazie (OSM `landuse=cemetery`), np. „Psi Los”. Mogą trafić do wyników.
  Kandydat na filtr przy następnym wyciągu.
- **Literówki z OSM** („parafialany”) zapełniają 30 miejsc przy samym słowie „parafialny”. Podpowiedź o
  dopisaniu miejscowości stoi teraz u góry. Propozycja `ui`: najpierw całe słowa, potem rdzenie (do decyzji
  autora, poza zakresem).
- **Wynik znaleziony przez okoliczną miejscowość** nie mówi, dlaczego trafił. Propozycja `ui`: „· przy:
  Dębniki” (do decyzji autora, poza zakresem).
- **Pasek komunikatu** to już drugi taki w aplikacji, a style-b nie ma dla niego reguły. Temat dla `ui`.
