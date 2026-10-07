---
title: "ISSUE-017 — Person photos: each person's photo collection, photos shared between people, a chosen profile photo (schema v4)"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-005-zdjecia]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-07
verdict-reviewer: self-check
source: "stop #1 ISSUE-016, rundy 1–2 (decyzje autora 2026-10-07: D1 — baza zdjęć osoby, dzielona, z „profilowym”; D6' — podział na ISSUE-016 i ISSUE-017; D2' — 2048 px, JPEG 85) · GEDCOM 7.0 (OBJE, CROP, „the first is the most-preferred value”)"
created: 2026-10-07
updated: 2026-10-07
---

# ISSUE-017 — Zdjęcia osoby

> Z rozpisania [[US-005-zdjecia]] na stopie #1 [[ISSUE-016-photos-grave-and-person]] (decyzja autora 2026-10-07):
> ISSUE-016 robi zdjęcie nagrobka i fundament zdjęć (zmniejszanie, podgląd, spójność kopii), a ta pozycja —
> **zdjęcia osób**. Słowa autora: *„osoby chciałbym, aby miały «swoją bazę zdjęć» (lub dzieloną, jeżeli na zdjęciu
> jest kilka osób) i możliwość wybierania z nich «profilowego»”*. To **zmiana schematu**, więc pozycja zaczyna się
> od kanonu i modelu, nie od ekranu.

## What to build
1. **Baza zdjęć osoby:** osoba ma dowolnie wiele zdjęć, z galerii albo aparatem (ta sama droga co w ISSUE-016:
   arkusz źródła, zmniejszanie do 2048 px, JPEG 85).
2. **Zdjęcie dzielone:** jedno zdjęcie (np. ślubne) należy do kilku osób, bez kopii pliku.
3. **Profilowe:** autor wybiera, które zdjęcie osoby jest jej zdjęciem profilowym. Profilowe widać w formularzu
   osoby (miejsce wskazane w [[wpis-osoby]] v3, element 1a) i jako miniaturę w karcie osoby w [[grob]].
4. **Schemat v4:** zdjęcie jako osobny rekord, łącze osoba–zdjęcie z kolejnością (jak `OBJE` w GEDCOM 7), migracja
   v3→v4 z testem; istniejące zdjęcia osób z v3 przechodzą do łączy.

## Acceptance Criteria
- [ ] US-005 AC-1 (osoba): zdjęcie wybrane z galerii albo zrobione aparatem jest widoczne przy osobie.
- [ ] US-005 AC-2: aplikacja trzyma własną kopię pliku w prywatnym magazynie (jak w ISSUE-016).
- [ ] US-005 AC-3: zdjęcia osób i ich łącza są w kopii i wracają po odtworzeniu, z odciskiem zgodnym.
- [ ] Osoba może mieć kilka zdjęć; jedno z nich autor wybiera jako profilowe.
- [ ] To samo zdjęcie można przypisać kilku osobom; plik jest jeden.
- [ ] Usunięcie zdjęcia z jednej osoby nie usuwa go innym osobom, które je mają.
- [ ] Na zdjęciu da się zaznaczyć każdą osobę z aplikacji (najpierw osoby z tego grobu), **także później** — z bazy
      każdej osoby, która już jest na zdjęciu (decyzja autora, stop #1, D2).
- [ ] Migracja v3→v4 zachowuje wszystkie dane; kopia v3 odtwarza się w aplikacji v4; po migracji kopia w tle
      zamawia się od razu (retro 1, R6).
- [ ] Ekran stosuje wytyczne stylu B ([[style-b]], reguła 14).

## Out of Scope
- **Wycinek twarzy z grupowego zdjęcia** (`CROP` z GEDCOM 7) — osobna pozycja po tej: [[ISSUE-018-profile-photo-crop]]
  (decyzja autora na stopie #2: następna). Schemat v4 go nie przewiduje z góry: kolumny dojdą migracją (`addColumn`),
  gdy powstanie ekran wycinania.
- Widok osoby (M5, R4 prawy) z pełną galerią — ta pozycja pokazuje bazę zdjęć tam, gdzie zdecyduje `ui`.
- ~~**Przypisanie zdjęcia osobie z innego grobu**~~ — **rozstrzygnięte na stopie #1 (D2): wchodzi.** Wybór spośród
  wszystkich osób z filtrem, osoby z tego grobu na górze; filtr działa tylko w tym oknie, to nie jest S5.
- Zdjęcie nagrobka → [[ISSUE-016-photos-grave-and-person]].

## Technical Notes
- **Kanon** (odczyt 2026-10-07, cytaty: ISSUE-016 → *Stop #1 — round 1*): w GEDCOM 7 zdjęcie to rekord
  `MULTIMEDIA_RECORD`, a osoba ma do niego łącze `OBJE`; przy łączu może stać `CROP`; *„the first is the
  most-preferred value”* — profilowe = pierwsze łącze. Ta sama zasada „pierwszej wartości” co [[ADR-006-claimed-value-separate-structures]] D3.
- Dziś `Media` ma jednego właściciela (`CHECK ((person_id IS NULL) <> (grave_id IS NULL))`). Grób w ISSUE-016 zostaje
  przy `grave_id` (najwyżej jedno zdjęcie). Model v4 rozstrzyga ADR (następny wolny numer) z ≥ 3 opcjami.
- Usunięcie zdjęcia z osoby usuwa **łącze**; plik bez żadnego łącza i bez grobu sprząta mechanizm z ISSUE-016 (D3).
- Fundament z ISSUE-016: arkusz źródła, zmniejszanie, podgląd, spójność kopii.
- Dane do testów i weryfikacji wyłącznie wymyślone; obrazy generowane (strażnik danych rodziny).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-016-photos-grave-and-person]] (fundament zdjęć) | technical | `done` (2026-10-07) — [[ADR-008-photos-access-copy-and-backup-consistency]] |
| specyfikacja `ui`: baza zdjęć osoby, profilowe, dzielenie | design | do zrobienia przed planem ([[wpis-osoby]] v3 to kierunek z jednym zdjęciem — do przeprojektowania) |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP):
- test happy-path dla każdego AC;
- ręczna weryfikacja na emulatorze;
- zmiana schematu, więc test migracji v3→v4;
- próbne odtworzenie z kopii przechodzi;
- zero danych rodziny w zmianach.

Po przyjęciu tego ISSUE US-005 idzie do werdyktu US.

## Implementation plan
> `planning`, 2026-10-07. **DoR:** jasny zakres ✅ · powiązana US: [[US-005-zdjecia]] (AC-1…AC-3) ✅ · krok ścieżki:
> n/a — M1 ✅ · `task-level` ✅.
>
> **Ekrany** — specyfikacje `ui` z 2026-10-07:
> - [[zdjecia-osoby]] v1 — **nowy ekran**, baza zdjęć osoby;
> - [[zdjecie]] v1.3 — tryb osoby: arkusz z wyborem kilku zdjęć, podgląd z „Na zdjęciu” i „Ustaw jako profilowe”,
>   okno usunięcia z jednej osoby, nowa część D „Kto jest na zdjęciu?”;
> - [[wpis-osoby]] v4 — element 1a: profilowe i liczba zdjęć;
> - [[grob]] v4 — profilowe w kartach osób;
> - wytyczne [[style-b]] v1.9.
>
> **Makieta:** `makieta-zdjecia-osoby.html` w katalogu tymczasowym sesji, 9 ramek. Obowiązują specyfikacje.
>
> **Warstwa danych:** zmiana schematu (v3→v4) z testem migracji, odtworzenie kopii v3 w aplikacji v4, próbne
> odtworzenie kopii ze zdjęciem dzielonym, kopia w tle zaraz po migracji (mechanizm z ISSUE-012, R6).
>
> **Źródło faktu:** n/a. Zdjęcie i to, kto jest na zdjęciu, nie są twierdzeniem o dacie, relacji ani miejscu pochówku
> ([[FR-001-provenance]] → *Cost decision*), a łącze w GEDCOM 7 nie ma źródła (D5).

### Prior art (sources, not memory)
- **[GEDCOM 7.0](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html)**, odczyt 2026-10-07. Cytaty
  `OBJE` i *„the first is the most-preferred value”* są w [[ISSUE-016-photos-grave-and-person]] → *Stop #1 — round 1*.
  Gramatyka łącza, przepisana dosłownie:
  ```
  MULTIMEDIA_LINK :=
  n OBJE @<XREF:OBJE>@                       {1:1}  g7:OBJE
    +1 CROP                                  {0:1}  g7:CROP
       +2 TOP <Integer>  · +2 LEFT <Integer>  · +2 HEIGHT <Integer>  · +2 WIDTH <Integer>
    +1 TITL <Text>                           {0:1}  g7:TITL
  ```
  Wnioski:
  - zdjęcie to rekord, a osoba ma do niego łącze;
  - łącza mają kolejność, a pierwsze to profilowe;
  - `CROP` i podpis `TITL` należą do **łącza**, nie do zdjęcia, więc przyszły wycinek twarzy dojdzie kolumnami
    łącza;
  - **łącze nie ma źródła (`SOUR`)** — D5.

  Uwaga: pierwsze streszczenie strony podało, że `SOUR` jest przy łączu. Blok gramatyki temu przeczy, a liczy się
  blok.
- **Kod `grobing-code`, odczyt 2026-10-07 — ograniczenie dla modelu:**
  - `restore_service.dart` → `_migrate`: po migracji starszej kopii **każda tabela z manifestu musi istnieć z tą samą
    liczbą wierszy** (README → *Baza danych*). Migracja v3→v4 może więc dodać tabelę i przebudować `media`, ale nie
    może usunąć jej wierszy ani jej samej. Dlatego `media` zostaje rekordem zdjęcia, a łącze to nowa tabela;
  - `data_state.dart`: odcisk danych sam znajduje tabele z `sqlite_master`, więc nowa tabela wchodzi do odcisku bez
    zmian w kodzie;
  - `_from1To2` (ISSUE-011) już przebudował tabelę przez `TableMigration`: ten sam wzorzec dla `media`. SQLite nie
    zmieni `CHECK` bez przebudowy, a dzisiejszy `CHECK` (osoba albo grób) w v4 przestaje obowiązywać.
- **[[ADR-008-photos-access-copy-and-backup-consistency]] pkt 3:** plik powstaje przed wierszem, usunięcie kasuje
  wiersz, a pliki bez wiersza starsze niż 1 h usuwa sprzątanie. **Nowe ryzyko z D3 (zapis z „Zapisz”):**
  - przygotowane zdjęcie czeka w katalogu roboczym, dopóki formularz jest otwarty, także godzinę i dłużej (u babci);
  - przeniesienie pliku (`rename`) **zachowuje stary czas modyfikacji**;
  - sprzątanie uruchomione między przeniesieniem a zatwierdzeniem transakcji usunęłoby więc plik, którego wiersz
    zaraz powstanie.

  Plan: czas modyfikacji ustawiony na „teraz” przy przeniesieniu (krok 2c) i test.

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego · co ją obali |
|---|---|---|---|
| **D1** | **Model zdjęć osób, schemat v4** (→ ADR-009 przy zamknięciu) | **(a)** `media` zostaje rekordem zdjęcia (bez `person_id`), nowa tabela łączy **`person_media` (osoba, zdjęcie, pozycja)**, a grób zostaje przy `media.grave_id` (najwyżej jedno, z ISSUE-016). Profilowe = najniższa pozycja | Odwzorowanie `OBJE` 1:1 i zgodne z ograniczeniem odtwarzania (wiersze `media` zostają). Kod nagrobka z ISSUE-016 się nie zmienia. *Obali:* trzeci właściciel zdjęć (np. cmentarz) — wtedy łącza ogólne jak w (b) |
| | opcja (b) | jedna tabela łączy dla osób i grobów | jednolita, ale przebudowuje dopiero co sprawdzony kod nagrobka, a grób i tak ma jedno zdjęcie — **odrzucona** |
| | opcja (c) | wiersz `media` na każde łącze (ta sama ścieżka pliku u kilku osób, kolumna pozycji, bez `UNIQUE` na ścieżce) | najmniejsza migracja, ale zdjęcie przestaje być rekordem: „kto jest na zdjęciu” to porównywanie ścieżek, a przyszłe dane zdjęcia (podpis, data) powtarzają się w każdym wierszu — **odrzucona** |
| | opcja (d) | profilowe jako znacznik `is_profile` przy łączu zamiast kolejności | wymaga warunku „dokładnie jeden na osobę”, a kolejność i tak jest potrzebna do siatki; rozjazd z GEDCOM — **odrzucona** |
| **D2** | **Kogo da się zaznaczyć na zdjęciu** ([[zdjecie]] D7; *Out of Scope* tej pozycji oddał to `ui` i `planning`) | **wszystkie osoby**, osoby z tego grobu na górze, filtr bez polskich znaków (`matchesQuery`, `polishCompare` — istniejący kod) | Zdjęcie grupowe z albumu łączy osoby z różnych grobów. Wariant „tylko ten grób” wymuszałby drugi plik tego samego zdjęcia. **Koszt:** jedna lista ok. 100 osób z polem filtra — **to nie jest S5.** **Tańszy wariant:** sama sekcja „W tym grobie” |
| **D3** | **Zmiany zdjęć osoby zapisują się z „Zapisz” formularza** ([[zdjecia-osoby]] D1, [[wpis-osoby]] D-zdjęcie-2) | tak — także łącza innych osób, w jednej transakcji z wpisem; „Odrzuć” cofa wszystko | „Zapis jest całością” i ten sam przepływ działa przy nowej osobie. **Inaczej niż nagrobek** (zapis od razu). Koszt: +1 dotknięcie przy zmianie samych zdjęć. *Obali:* na stopie #2 dwie zasady przeszkadzają — wtedy zapis od razu, a nowa osoba dostaje zdjęcia dopiero po pierwszym zapisie |
| **D4** | **Decyzje projektowe `ui` (pakiet)** | przyjąć | baza zdjęć na osobnym ekranie z 1a · zdjęcia w siatce jako kwadraty, okrąg tylko dla profilowego · nagłówek z profilowym 96 dp · kilka zdjęć naraz z galerii · kafelek „Dodaj zdjęcie” na końcu siatki · dzielenie od strony zdjęcia („Kto jest na zdjęciu?”) · profilowe osobne dla każdej osoby · bez przestawiania zdjęć poza profilowym |
| **D5** | **Kto jest na zdjęciu — bez źródła** | tak, bez źródła i statusu | FR-001 obejmuje daty, relacje i miejsce pochówku (*Cost decision*: „reszta bez osobnego źródła”), a GEDCOM 7 nie ma `SOUR` przy łączu (gramatyka wyżej). *Obali:* autor chce wiedzieć, kto rozpoznał osobę na zdjęciu (np. „babcia”) — wtedy źródło przy łączu, osobna pozycja |

### Stop #1 — odpowiedź autora (2026-10-07)
- **D1, D3, D4, D5:** „ok”.
- **D2:** *„Może być tak, że na 4-osobowym zdjęciu zaznaczę tylko dwie osoby, które znam, ale w przyszłości wrócę do
  tego zdjęcia i zaznaczę kolejną osobę (bo się dowiedziałem, że to rodzina i jak się łączy)”*. Przyjęte:
  **wszystkie osoby z filtrem**. Powrót działa z bazy każdej osoby już zaznaczonej na zdjęciu: zdjęcie → „Zmień”
  przy „Na zdjęciu” → zaznaczenie → „Gotowe” → „Zapisz”. Nowo poznany krewny leży zwykle w innym grobie, więc
  wariant „tylko ten grób” by go nie pokazał. Nowe AC w *Acceptance Criteria*, nowy test i krok 3b.
- **Granica (powiedziana autorowi):**
  - zaznaczyć można tylko osobę, która już jest w aplikacji. Dziś osoba powstaje tylko w grobie, a krewny bez znanego
    grobu albo żyjący dojdzie z [[US-003-przepisanie-rodziny]];
  - zdjęcie nie pamięta, że są na nim osoby jeszcze nierozpoznane (np. „2 z 4”). Kandydat: podpis zdjęcia (`TITL`
    przy łączu), poza zakresem.

### Falsifier — what is measured and what is not
| # | Pytanie | Wynik |
|---|---|---|
| F1 | Czy Photo Picker zwraca kilka zdjęć w kolejności zaznaczania? ([[zdjecie]] D8) | **Zmierzy** `dev` na emulatorze: 3 wymyślone obrazy zaznaczone w odwrotnej kolejności niż w galerii → kolejność w siatce. Nie → zapis w *Dev report* i notka dla autora („profilowe ustawisz 2 dotknięciami”); bez zmiany kodu |
| F2 | Czy migracja v3→v4 zachowuje wszystkie dane i przenosi zdjęcia osób z v3 do łączy w kolejności? | **Zmierzy** test migracji: wymyślona baza v3 ze zdjęciem grobu i dwoma zdjęciami osoby → w v4 ten sam `media` (bez `person_id`), dwa łącza w kolejności `id`, `PRAGMA foreign_key_check` pusty, liczby wierszy v3 równe |
| F3 | Czy kopia v3 z wierszami zdjęć osób odtwarza się w aplikacji v4? | **Zmierzy** test odtworzenia na kopii v3 zrobionej kodem testowym (jak archiwum v1 w ISSUE-011): przechodzi `_migrate` i sprawdzenie liczb wierszy |
| F4 | Czy sprzątanie może usunąć zdjęcie w trakcie zapisu formularza otwartego dłużej niż 1 h? | ❌ bez kroku 2c (wniosek z kodu, *Prior art*). **Zmierzy** test: przygotowany plik ze starym czasem → zapis z zatrzymaniem przed transakcją → sprzątanie → plik zostaje |
| F5 | Tempo bazy zdjęć i „Zapisz” po zmianie zdjęć | ze specyfikacji ([[zdjecia-osoby]] → *Tempo*). **Nie zmierzone na ekranie** — odczucie autora na stopie #2 |

### Scope diff vs the item
- **zakres według pozycji:** baza zdjęć, dzielenie, profilowe, schemat v4 — bez zmian.
- **kształt ekranów (D4):** nowy ekran [[zdjecia-osoby]] i część D w [[zdjecie]]. Pozycja zostawiała miejsce na
  bazę zdjęć do decyzji `ui`.
- **+ kilka zdjęć naraz z galerii** — decyzja projektowa, obiecana w [[zdjecie]] D2.
- **± wybór wszystkich osób na zdjęciu (D2)** — *Out of Scope* pozycji zostawiało to pytanie otwarte. Rekomendacja
  je poszerza; tańszy wariant zostaje przy pozycji.
- **+ zapis zdjęć z „Zapisz” (D3)** i **odświeżenie czasu pliku (F4)** — konsekwencja D3.
- **bez zmian:** AC 1–8, brak `INTERNET`, styl B, `CROP` poza zakresem.

### Steps (dev)
0. **Przed zmianą:** na `Medium_Phone` jest build release v3 z wymyślonymi danymi i zdjęciem nagrobka (stop #2
   ISSUE-016). **Nie odinstalowuj** — aktualizacja na tych danych to sprawdzenie migracji na urządzeniu (`qa`).
1. **Schemat v4** — `lib/data/database.dart`:
   - a. `Media`: bez `personId` i bez `CHECK` (osoba albo grób); `graveId` opcjonalne jak dotąd. Komentarz: wiersz bez
     grobu i bez łącza nie istnieje po zapisie (krok 2d);
   - b. nowa tabela **`PersonMedia`** (`person_media`): `personId` → `Persons`, `mediaId` → `Media`, `position` (int).
     Klucz `{personId, mediaId}`, indeks na `mediaId` (pytanie „kto jest na zdjęciu”). Kolejność = `position`, potem
     `mediaId`;
   - c. `currentSchemaVersion = 4`, `dart run drift_dev make-migrations` (schemat v4 w `drift_schemas/grobing/`, testy w
     `test/drift/grobing/generated/`);
   - d. `_from3To4`, w tej kolejności:
     1. `createTable(person_media)`;
     2. łącza z v3: `INSERT … SELECT person_id, id, row_number() OVER (PARTITION BY person_id ORDER BY id) - 1 FROM
        media WHERE person_id IS NOT NULL`;
     3. `alterTable(TableMigration(schema.media))` — przebudowa bez `person_id`, wiersze i `id` zostają;
     4. `PRAGMA foreign_key_check` musi być pusty, inaczej wyjątek, a transakcja całej aktualizacji wraca (wzorzec
        `onUpgrade`).

     Sprawdź, że w `onUpgrade` klucze obce są wyłączone: `PRAGMA foreign_keys = ON` jest w `beforeOpen`, czyli po
     migracji. Zapisz to w komentarzu;
   - e. `build_runner build`.
2. **Dane** — `lib/data/photos.dart`:
   - a. odczyt:
     - `personPhotos(db, personId)` → zdjęcia osoby w kolejności łączy (id, ścieżka);
     - `photoPeople(db, mediaId)` → osoby z łączem (dla B5);
     - `profilePhotoPaths(db, personIds)` → ścieżka pierwszego łącza każdej osoby;
   - b. `newPersonPhotoPath()` → `zdjecia/<czas>-<losowe>.jpg`, bez id osoby (zdjęcie bywa wspólne) i nigdy z treści
     zdjęcia. Stare ścieżki z v3 zostają;
   - c. **`PersonPhotoEdits`** (wartość: kolejna lista zdjęć tej osoby — istniejące po id, nowe po przygotowanym pliku;
     zmiany osób na każdym zdjęciu; usunięte) i **`moveNewPersonPhotos(mediaDir, edits)`**:
     - przenosi przygotowane pliki do `media/` **przed** transakcją (ADR-008);
     - **ustawia czas modyfikacji na teraz** (F4);
     - zwraca ścieżki;
   - d. **`applyPersonPhotoEdits(db, personId, edits, paths)`** — wywoływane **wewnątrz** transakcji zapisu osoby:
     - wiersze `media` dla nowych zdjęć;
     - łącza tej osoby przepisane w kolejności (pozycje 0…n−1);
     - innym osobom łącze dodane na końcu (max + 1) albo usunięte;
     - na końcu **usuwa wiersze `media` bez grobu i bez łącza** (plik zostaje do sprzątania, ADR-008 pkt 3).

     Sprzątanie plików się nie zmienia, bo dalej patrzy na wiersze `media`.
3. **Zapis osoby** — `lib/data/graves.dart`:
   - `addPersonToNewGrave`, `addPersonToGrave` i `updatePersonEntry` przyjmują opcjonalne edycje zdjęć i stosują je
     w **tej samej transakcji**, gdy id osoby jest już znane. Błąd transakcji → przeniesione pliki usuwane od razu
     (wzorzec `setGravePhoto`);
   - `BuriedPerson.profilePhotoPath`; `_watch` widoku grobu czyta też `person_media`;
   - **`loadPhotoPeopleChoices(db, graveId)`** dla części D:
     - osoby z tego grobu w kolejności wpisania;
     - pozostałe według `polishCompare` (nazwisko, imiona), z latami i nazwą grobu albo cmentarza pierwszego pochówku
       (ADR-006 D3);
     - osoby bez pochówku — same lata.
4. **Wybór i przygotowanie zdjęć**:
   - `lib/app/photo/photo_picker.dart`: `pickMany()` przez `pickMultiImage(requestFullMetadata: false)` z Photo
     Pickerem, a aparat jak dotąd jedno zdjęcie. Przy okazji F1;
   - `lib/app/photo/photos.dart`: `preparePersonPhoto(picked)` → plik w katalogu roboczym, bez zapisu danych; kopia
     z paczki usuwana od razu po przygotowaniu.
5. **Ekrany:**
   - a. `lib/app/photo/person_photos_draft.dart` (`ChangeNotifier`) — stan zmian formularza:
     - zdjęcia w kolejności, osoby na każdym zdjęciu, usunięte;
     - `hasChanges`, profilowe, liczba;
     - przy porzuceniu kasuje swoje przygotowane pliki;
   - b. `lib/app/photo/person_photos_screen.dart` — [[zdjecia-osoby]], elementy 1–6 i stany;
   - c. `photo_viewer_screen.dart` — tryb osoby:
     - B3: przesunięcie tylko bez przybliżenia, przyciski ‹ › z `tooltip`;
     - B5 „Na zdjęciu” z „Zmień”;
     - B4' „Ustaw jako profilowe” albo stan „✓ Profilowe”, „Usuń z tej osoby”;
     - okno C1' z trzema treściami.

     Tryb grobu bez zmian;
   - d. `lib/app/photo/photo_people_screen.dart` — część D: zdjęcie 160 dp, filtr, dwie sekcje, „ta osoba”
     nieaktywna, „Gotowe”;
   - e. `photo_source_sheet.dart`: tytuł z parametru, w trybie osoby galeria z wyborem kilku zdjęć;
   - f. `lib/app/grave/person_form_screen.dart`:
     - 1a v4: bez zdjęć → arkusz źródła; ze zdjęciami → baza zdjęć (profilowe + „3 zdjęcia”, `plural`);
     - treść okna „Odrzucić wpis?” przy zmianach zdjęć;
     - „Zapisz” przekazuje edycje;
   - g. `lib/app/grave/grave_screen.dart` → `_PersonCard`:
     - profilowe 40 dp z lewej, dekodowane w rozmiarze (`cacheWidth`);
     - bez zdjęcia bez wcięcia (D11);
     - plik bez odczytu → `broken_image_outlined`.
6. **Dane debug** — `lib/dev/fictional_data.dart` i `fictional_photo.dart`:
   - dwa rysowane obrazy: „portret” i „zdjęcie grupowe” (jak nagrobek z ISSUE-016: rysowane w kodzie, nigdy plik z
     dysku);
   - jedna osoba z dwoma zdjęciami, a zdjęcie grupowe wspólne dla dwóch osób z tego samego grobu.
7. **README** → *Baza danych*:
   - akapit „Zdjęcia osób (schemat v4)”: rekord + łącze, profilowe = pierwsze łącze, zapis z „Zapisz”;
   - wiersz `media` bez grobu i łącza usuwany w transakcji;
   - czas pliku odświeżany przy przeniesieniu.
8. `dart format` · `flutter analyze` · `flutter test`; build release i instalacja **na** buildzie v3 z kroku 0, bez
   odinstalowania.

### Files likely touched
- **Kod danych:**
  - `lib/data/database.dart`, `database.g.dart`, `database.steps.dart`;
  - `drift_schemas/grobing/drift_schema_v4.json`;
  - `lib/data/photos.dart`, `lib/data/graves.dart`.
- **Kod ekranów:**
  - `lib/app/photo/` — `photo_picker.dart`, `photos.dart`, `photo_source_sheet.dart`, `photo_viewer_screen.dart`;
    nowe: `person_photos_draft.dart`, `person_photos_screen.dart`, `photo_people_screen.dart`;
  - `lib/app/grave/person_form_screen.dart`, `grave_screen.dart`.
- **Debug i dokumentacja:** `lib/dev/fictional_data.dart`, `fictional_photo.dart`, `README.md`.
- **Testy (`qa`):**
  - `test/drift/grobing/migration_test.dart` i `generated/` (v4);
  - `test/data/photos_test.dart`, `graves_test.dart`, `data_state_test.dart`;
  - `test/backup/restore_service_test.dart` (kopia v3 → v4, kopia ze zdjęciem dzielonym);
  - `test/app/photo/`, `test/app/grave/`;
  - `test/support/photo_fakes.dart` (`pickMany`).

### AC → tests (`qa`)
| AC | Test |
|---|---|
| US-005 AC-1 (osoba) | widget: formularz → 1a → arkusz → atrapa zwraca 2 pliki → 1a pokazuje profilowe i „2 zdjęcia” → „Zapisz” → karta w grobie ma miniaturę; dane: 2 łącza w kolejności |
| US-005 AC-2 | po zapisie pliki są w `media/zdjecia/`; kopia z paczki i plik roboczy usunięte |
| US-005 AC-3 | kopia → odtworzenie: zdjęcie dzielone (dwa łącza, jeden plik) i profilowe wracają, odcisk zgodny (F3 dla kopii v3) |
| kilka zdjęć, jedno profilowe | „Ustaw jako profilowe” → po zapisie to zdjęcie ma pozycję 0; karta i 1a pokazują je |
| jedno zdjęcie u kilku osób, jeden plik | zaznaczenie drugiej osoby w D → po zapisie jeden wiersz `media`, jeden plik, dwa łącza; druga osoba bez zdjęć dostaje je jako profilowe |
| usunięcie u jednej osoby nie usuwa innym | usunięcie łącza osoby A → osoba B ma zdjęcie, wiersz i plik zostają; usunięcie u ostatniej osoby → wiersz `media` usunięty, plik usuwa sprzątanie po 1 h (zegar w teście) |
| migracja v3→v4 | F2 (dane) + wygenerowane testy schematu; kopia zaraz po migracji — istniejący test startu (R6) dalej zielony |
| styl B | przegląd `ui` (subagent) ze zrzutów |
| D3: „Odrzuć” | baza bez zmian, pliki robocze usunięte |
| F4 | stary czas pliku → zapis → sprzątanie w środku → plik zostaje |
| D2: filtr | „wym” znajduje „Wymyślony” w obu sekcjach; zaznaczenia ukrytych wierszy zostają |
| D2: zaznaczenie później (nowe AC) | zdjęcie z dwiema osobami z jednego grobu, zapisane → w nowej edycji formularza jednej z nich dodana trzecia osoba **z innego grobu** → po zapisie trzy łącza, plik jeden, a trzecia osoba (bez zdjęć) ma je jako profilowe |

### Manual verification (stop #2) — kroki według miejsca
**Emulator `Medium_Phone`, build release (autor — UI/UX).** W galerii emulatora są wymyślone obrazy, które `qa`
wgra przez `adb`.
1. Grób z wymyślonymi osobami → osoba → **„Dodaj zdjęcie”** nad imionami → „Wybierz z galerii” → zaznacz 3 obrazy →
   „Gotowe”. Okrąg pokazuje zdjęcie i „3 zdjęcia”, a imiona i fokus się nie zmieniają. „Zapisz” → w karcie osoby
   jest okrąg ze zdjęciem.
2. Ta osoba → okrąg → baza zdjęć → drugie zdjęcie → **„Ustaw jako profilowe”** (pojawia się „✓ Profilowe”) → wstecz:
   nagłówek bazy pokazuje nowe profilowe → wstecz → „Zapisz” → karta pokazuje nowe zdjęcie.
3. Zdjęcie grupowe: baza → zdjęcie → „Zmień” przy „Na zdjęciu” → zaznacz drugą osobę z grobu → „Gotowe” → linia
   „Na zdjęciu” ma obie osoby → wstecz → „Zapisz”. Druga osoba → okrąg → zdjęcie jest w jej bazie.
   **3b. Później:** osoba z innego grobu (wymyślona, z danych debug) → wróć do pierwszej osoby → okrąg → to samo
   zdjęcie → „Zmień” → filtr: pierwsze litery nazwiska → zaznacz → „Gotowe” → „Zapisz”. Osoba z innego grobu ma to
   zdjęcie w swojej bazie, a w jej grobie jest w karcie.
4. U drugiej osoby: zdjęcie → **„Usuń z tej osoby”** → okno mówi, u kogo zdjęcie zostaje → „Usuń” → „Zapisz”.
   Pierwsza osoba dalej ma to zdjęcie.
5. Dodaj zdjęcie, a potem wstecz bez „Zapisz” → okno „Wpisane dane i zmiany zdjęć nie zostaną zapisane.” → „Odrzuć”
   → zdjęcia nie ma.
6. „Zrób zdjęcie” aparatem emulatora → zdjęcie w bazie.
7. **Odczucie** (napisz tutaj): siatka i okrąg profilowego (przycięcie ze środka), „Zapisz” po zmianie samych zdjęć
   (D3), lista „Kto jest na zdjęciu?” (D2).

**Agent (bez autora):**
- aktualizacja na buildzie v3 z kroku 0 — liczby wierszy i zdjęcie nagrobka bez zmian, `person_media` jest, kopia
  zamówiona po starcie;
- F1 na emulatorze;
- odcisk przed i po kopii z odtworzeniem na `Grobing_Restore`;
- „Stan danych” pokazuje `person_media`.

### Out of Scope (this plan)
- Wycinek twarzy (`CROP`) → osobna pozycja po tej. Kolumny łącza dojdą przez `addColumn` (D1).
- Podpis zdjęcia (`TITL`), data zdjęcia, przestawianie zdjęć, widok osoby (M5), wybór „ze zdjęć w aplikacji”
  ([[zdjecia-osoby]] D6), źródło rozpoznania osoby na zdjęciu (D5).
- Wyszukiwanie S5. Filtr w D działa tylko w tym oknie.
- Usuwanie osoby, eksport ([[US-006-eksport-dla-rodziny]]), HEIF z telefonu autora (dalej niesprawdzony —
  ADR-008).

### For docs at closure
- **ADR-009 — zdjęcia osób: rekord + łącze z kolejnością (schemat v4)** z D1: opcje (a)–(d), ograniczenie
  odtwarzania, GEDCOM 7 `MULTIMEDIA_LINK` (bez `SOUR`, `CROP` i `TITL` przy łączu).
- `04_ARCHITECTURE/data-model.md` → *Media*:
  - rekord zdjęcia, `person_media` z pozycją, profilowe = pierwsze łącze;
  - ścieżki `media/zdjecia/…`;
  - wiersz bez grobu i bez łącza usuwany w transakcji.
- `04_ARCHITECTURE/backup-format.md`: nowa tabela w kopii (bez zmiany formatu); odświeżanie czasu pliku (F4) przy
  *Known limits* → spójność.
- `glossary.md`: **profilowe** (pierwsze łącze osoby do zdjęcia, osobne dla każdej osoby) i **łącze zdjęcia** —
  zgłoszone przez `ui`.
- [[US-005-zdjecia]] → werdykt US (ostatni ISSUE). [[NFR-003-migracje-schematu]]: migracja v3→v4.
- [[ISSUE-017-person-photos]] → *Out of Scope*: pytanie o przypisanie osobie z innego grobu rozstrzygnięte (D2).

### Self-check (planning) — said out loud
1. **Kompletność:** zakres, decyzje, falsyfikatory, kroki, pliki, AC → testy, kroki ręczne według miejsca, *Out
   of Scope* ✅.
2. **Spójność:** plan idzie za specyfikacjami `ui` (2026-10-07) i pozycją. Poszerzenie (D2) i zmiana zasady zapisu
   (D3) są nazwane i idą na stop #1, nie po cichu.
3. **Własność:**
   - ta sekcja, `status: in-progress` i kolumny Issue(s) i Issue Status w `TRACEABILITY.md`;
   - ADR-009 pisze `docs` przy zamknięciu, jak ADR-008;
   - specyfikacje zmieniał `ui`.
4. **Warstwa danych:**
   - test migracji v3→v4 z danymi (F2) ✅;
   - odtworzenie kopii v3 w v4 (F3) i kopii ze zdjęciem dzielonym ✅;
   - kopia po migracji (R6) ✅;
   - źródło faktu: n/a z uzasadnieniem (D5) ✅.
5. **Wystarczalność — czego plan nie ma:**
   - **przeglądu migracji na prawdziwym telefonie** — autor nie ma jeszcze danych w aplikacji, więc pierwsza
     prawdziwa aktualizacja v3→v4 zdarzy się co najwyżej na emulatorach. Build v3 nie dodawał zdjęć osób, więc na
     urządzeniu migracja przenosi zero łączy, a łącza z v3 sprawdza tylko test;
   - **liczby zdjęć osób** — założenie ok. 50 ([[zdjecia-osoby]] → *Tempo*); czas odcisku przy setkach zdjęć —
     ADR-008 *Follow-ups*;
   - **zapis wielu zdjęć naraz** trwa dłużej (przenoszenie plików przed transakcją); wskaźnik w „Zapisz” jest w
     specyfikacji, czas — do zmierzenia przez `dev`.

## Dev report
> `dev`, 2026-10-07. Flutter 3.41.1 (przypięty) ✅.

### What was built
- **Schemat v4** (`lib/data/database.dart`):
  - `media` bez `person_id` i bez `CHECK`;
  - nowa tabela `person_media` (osoba, zdjęcie, pozycja; klucz `{person_id, media_id}`, indeks `person_media_media`);
  - `_from3To4`: utworzenie tabeli, łącza z v3 przez `row_number() OVER (PARTITION BY person_id ORDER BY id) - 1`,
    przebudowa `media` (`TableMigration`), na końcu `PRAGMA foreign_key_check`.

  Wygenerowane: `drift_schema_v4.json`, `database.steps.dart`, `test/drift/grobing/generated/schema_v4.dart` i
  `schema.dart` (`make-migrations`).
- **Dane** (`lib/data/photos.dart`):
  - odczyt: `personPhotos`, `photoPeopleIds`, `profilePhotoPaths`, `newPersonPhotoPath` (`zdjecia/<czas>-<losowe>.jpg`);
  - edycja: `PhotoRef` (`SavedPhoto` | `NewPhoto`), `PersonPhotoEdits`;
  - zapis: `moveNewPersonPhotos` (czas pliku = teraz, F4), `returnMovedPhotos`, `applyPersonPhotoEdits` (łącza tej
    osoby od nowa w kolejności, innym na końcu, wiersz bez grobu i łącza usuwany).
- **Zapis osoby** (`lib/data/graves.dart`):
  - `AlsoWrite` w `addPersonToNewGrave`, `addPersonToGrave` i `updatePersonEntry` — w tej samej transakcji;
  - `BuriedPerson.profilePhotoPath`;
  - `watchGrave` czyta `person_media`;
  - `loadPersonChoices` (wszyscy + kto leży w grobie; pierwszy pochówek według ADR-006 D3).
- **Ekrany:**
  - `person_photos_draft.dart` — stan zdjęć w otwartym formularzu;
  - `person_photos_screen.dart` — [[zdjecia-osoby]] i wspólne `addPersonPhotos`;
  - `person_photo_viewer_screen.dart` — [[zdjecie]] B w trybie osoby i okno C1';
  - `photo_people_screen.dart` — część D;
  - `person_form_screen.dart` — 1a v4, okno „Odrzucić wpis?” przy zmianach zdjęć, zapis ze zdjęciami, wskaźnik w
    „Zapisz”;
  - `grave_screen.dart` — profilowe 40 dp w kartach, `graveId` przy poprawie;
  - `data_state_screen.dart` — etykieta „Zdjęcia osób (łącza)”.
- **Picker:** `PhotoPicker.pickMany()` (`pickMultiImage`, Photo Picker); `Photos.preparePersonPhoto`, `discard`,
  `writeWithPersonPhotos`.
- **Dane debug:** rysowane „portret” i „zdjęcie ślubne” (`fictionalPeoplePng`). Matka ma oba zdjęcia (portret jako
  profilowe), a ojciec — ślubne, wspólne z nią.
- **README** → *Baza danych* (schemat v4) i *Zdjęcia* (model, zapis z „Zapisz”, czas pliku, ponowienie).

### Checks (dev, host Windows + emulator `Medium_Phone_API_36.1`, build release)
- `flutter analyze lib`: czyste. `dart format lib`: ✅.
- **`flutter test` — 12 czerwonych, wszystkie po stronie testów (dla `qa`, *For qa*).** Wygenerowane testy
  migracji przechodzą: 1→4, 2→4, 3→4 i stare testy danych v1→v2 oraz v2→v3.
- **Próbka logiki zapisu** (poza repo, katalog tymczasowy sesji — nie test `qa`). Zielona dla:
  - dwa nowe zdjęcia Anny, drugie dzielone z Janem → jeden wiersz `media` na wspólne zdjęcie, Jan bez zdjęć dostaje
    je jako profilowe;
  - **F4:** plik z czasem sprzed 3 h po przeniesieniu ma czas „teraz”, sprzątanie go nie bierze;
  - zmiana profilowego i usunięcie zdjęcia tylko Anny → wiersz `media` znika w transakcji, plik — dopiero po
    sprzątaniu (> 1 h);
  - usunięcie wspólnego u Anny → Jan je ma;
  - **D2 „później”:** Anna znów zaznaczona z formularza Jana;
  - nieudany zapis odkłada pliki z powrotem;
  - `foreign_key_check` pusty.
- **Migracja na urządzeniu:** release v4 zainstalowany **na** release v3 z ISSUE-016, bez odinstalowania. „Stan
  danych”:

  | | v3 | v4 |
  |---|---|---|
  | wersja schematu | 3 | 4 |
  | odcisk | `65f2257485182a63` | `96c0dce357b30cf5` (inny schemat) |
  | osoby · zdarzenia · cmentarze · groby · pochówki · twierdzenia | 4 · 4 · 1 · 1 · 4 · 8 | 4 · 4 · 1 · 1 · 4 · 8 |
  | zdjęcia (wpisy) · pliki | 1 · 1 | 1 · 1 |
  | zdjęcia osób (łącza) | — | 0 |

  Zdjęcie nagrobka jest. Kopię w tle po migracji (R6) sprawdza `qa`.
- **F1 — wynik:** Photo Picker na Androidzie 16 oddaje zdjęcia **w kolejności zaznaczania**:
  - 3 wymyślone obrazy zaznaczone w kolejności 2 → 3 → 1 (w galerii 3, 1, 2);
  - baza: 2, 3, 1;
  - profilowe: 2.

  Na Androidzie 13–15 nie sprawdzone.
- **Przegląd na emulatorze:** 1a → arkusz „Zdjęcia osoby” → wybór 3 → „Gotowe” → 1a „3 zdjęcia” → baza → podgląd
  „2 z 3” → „Zmień” → Jan → „Gotowe” → „Na zdjęciu: Anna Wymyslona, Jan Wymyslony” → „Zapisz”. Widok grobu: Anna z
  profilowym, Jan ze wspólnym zdjęciem jako profilowe, osoby bez zdjęć bez wcięcia. Zrzuty są w katalogu tymczasowym
  sesji (`f1-*.png`), tylko wymyślone obrazy.
- APK release: 57,7 MB (+0,6 MB). Bez nowych uprawnień.

### Deviations from the plan
1. **Podgląd osoby w osobnym pliku** `person_photo_viewer_screen.dart`, nie jako tryb w `photo_viewer_screen.dart`.
   Wspólne części wyjęte do publicznych `ZoomablePhoto`, `PhotoViewerBar` i `UnreadablePhoto`. Podgląd nagrobka
   działa jak dotąd: przybliżenie wraca po zmianie zdjęcia, bo nowy plik to nowy `ZoomablePhoto` (klucz).
2. **Nieudany zapis odkłada pliki, zamiast je usuwać** (`returnMovedPhotos`; plan krok 3: „usuwane od razu”). Inaczej
   „Spróbuj jeszcze raz” nie miałoby już pliku do przeniesienia. Pliku, którego nie da się odłożyć, nic nie
   ratuje, więc jest usuwany.
3. **`AlsoWrite` (wywołanie z id osoby) zamiast edycji zdjęć w parametrach `graves.dart`.** Warstwa grobów nie zna
   typów zdjęć, a transakcja jest ta sama.
4. **Dane debug rysują i zapisują obrazy przed transakcją.** Powód: `background_backup_test` („seria zapisów daje
   najwyżej 2 zgłoszenia”) dawał 3. Próbka pokazała, że drift zgłasza tabele zagnieżdżonych transakcji (pomocników
   twierdzeń) od razu. Dłuższa transakcja po nich, z zapisami plików z `flush`, rozciągała jedną serię na trzy
   zgłoszenia. Teraz test przechodzi trzy razy z rzędu. Kolejność „plik przed wierszem” zostaje.
5. **Etykieta „Zdjęcia osób (łącza)” na „Stanie danych”** — poza planem; bez niej ekran pokazałby `person_media`.
6. **Wskaźnik w „Zapisz” tylko przy zmianach zdjęć.** Bez zdjęć zapis trwa ułamek sekundy i napis zostaje, jak dotąd.
7. **Nowe zdjęcie usunięte z tej osoby, ale zaznaczone u innych, i tak zapisuje się u tamtych.** Tak mówi okno C1':
   „Zdjęcie zostaje u: …”.
8. **`Correction` dostał opcjonalne `graveId`**, żeby „W tym grobie” działało przy poprawie wpisu.

### For qa
- **Testy do poprawy** (zmiana interfejsu i schematu, nie błąd kodu):
  - `test/support/photo_fakes.dart` — `FakePhotoPicker` potrzebuje `pickMany` (przez to nie kompilują się
    `grave_photo_screens_test`, `photos_test` w `test/app/photo/` i `test/data/photos_test.dart`);
  - `test/data/photos_test.dart:68` — `MediaFile.personId` nie istnieje (łącza w `person_media`);
  - `data_state_test` (schemat 4, nowa tabela, liczby);
  - `database_test` (v4, lista tabel);
  - `data_state_screen_test` i `backup_archive_test` (dane debug mają teraz 3 pliki zdjęć i 3 łącza);
  - `restore_service_test` „v2 backup restores into the v3 app” (oczekuje `(2, 3)`, jest `(2, 4)`).
- **Testy nowe** — plan → *AC → tests*: F2 (migracja z danymi), F3 (kopia v3 → v4), F4 (czas pliku), D2 (filtr i
  „później”).
- **Stan emulatora `Medium_Phone`:**
  - release v4;
  - Anna Wymyslona ma 3 wymyślone zdjęcia (profilowe: zielony obraz), Jan Wymyslony ma wspólne zdjęcie (niebieski);
  - w galerii są `Pictures/wymyslone-1…3.png` (kolorowe paski, bez osób).

  Kroki stopu #2 zakładają osobę bez zdjęć: zostały dwie osoby „as Wymyslona” bez dat i zdjęć, albo trzeba dodać
  nową osobę.
- **Przegląd `ui`** (subagent): zrzuty z emulatora; ekrany [[zdjecia-osoby]], [[zdjecie]] (B osoby, C1', D),
  [[wpis-osoby]] 1a, [[grob]] 5.

### Fixes after the ui review (dev, 2026-10-07)
1. **MAJOR — akcja dotknięcia w semantyce:** `Semantics(excludeSemantics: true)` z etykietą „… — otwórz” chował akcję
   `InkWell`. Czytnik, Switch Access i Voice Access dostawały przycisk, którego nie da się nacisnąć. Poprawione:
   `onTap` (i `enabled`) w `Semantics` przy komórkach siatki, nagłówku profilowego, kafelku „Dodaj zdjęcie” i elemencie
   1a.
2. **MINOR:** podtytuł `PhotoViewerBar` ma jedną linię i jest ucinany.
3. **MINOR:** B4' to dwa stałe miejsca (`Row` z dwoma `Expanded`), więc „Usuń z tej osoby” nie przesuwa się przy
   przewijaniu. Na emulatorze te same współrzędne przy profilowym i przy kolejnym zdjęciu.
4. **MINOR:** miniatury przycinane ze środka (siatka, 96, 80 i 40 dp) dekodują się w szerokości 2 × pole
   (`coverDecodeWidth`), więc zdjęcie poziome do 2:1 nie jest powiększane.
5. **MINOR:** „Usuń z tej osoby” jest nieaktywne, dopóki osoby bieżącego zdjęcia się nie wczytają. Okno C1' nie może
   więc powiedzieć „Zdjęcia nie będzie…” przy zdjęciu dzielonym.
6. **MINOR:** kafelek „Dodaj zdjęcie” ma szerokość komórki i co najmniej jej wysokość, a przy dużej czcionce rośnie w
   dół.

## Verification
> `qa`, 2026-10-07. Do czasu krytyka (ISSUE-003) werdykt `self-check`.

### Automated — `flutter test`: 389 ✅ (było 367) · `flutter analyze`: czyste · `dart format`: ✅
- **Nowe testy:**
  - `test/data/person_photos_test.dart` (10): AC-1/AC-2, profilowe, zdjęcie dzielone (jeden wiersz, jeden plik),
    usunięcie u jednej osoby i u ostatniej (wiersz od razu, plik po sprzątaniu), D2 „później” z innego grobu,
    `loadPersonChoices`, **F4**, nieudany zapis odkłada pliki, nowe zdjęcie zostaje u innych (C1'), zapis zamawia
    kopię;
  - `test/app/photo/person_photos_draft_test.dart` (3): „Odrzuć” kasuje przygotowane pliki, zdjęcie nie do odczytania
    liczone („1 z 2”), zmiany w szkicu nie dotykają bazy, a cofnięcie zmian to „bez zmian”;
  - `test/app/photo/person_photos_screens_test.dart` (4):
    - AC-1 z elementu 1a do karty grobu;
    - baza zdjęć i podgląd: „Ustaw jako profilowe”, „Kto jest na zdjęciu?” (ten grób, filtr, osoba z innego grobu
      później);
    - „Odrzuć”;
    - okno C1'.

    Do tego semantyka: rola przycisku i akcja dotknięcia (MAJOR z przeglądu). **Falsyfikator wykonany:** bez
    poprawki test pada („flags: [isButton]”, bez akcji);
  - `migration_test.dart` **F2** (v3→v4 z danymi): łącza w kolejności `id`, wiersze `media` z tymi samymi `id`,
    `foreign_key_check` pusty;
  - `restore_service_test.dart` **F3**: kopia v3 ze zdjęciami osób odtwarza się w v4. Liczby wierszy v3 zostają, a
    łącza i pliki są.
- **Poprawione testy** (schemat 4, nowa tabela, dane debug z 3 zdjęciami):
  - `photo_fakes.dart` (`pickMany`);
  - `photos_test.dart`, `data_state_test.dart`, `database_test.dart`;
  - `data_state_screen_test.dart` (także etykieta „Zdjęcia osób (łącza)”);
  - `backup_archive_test.dart`;
  - `restore_service_test.dart` (kopia v2 → bieżąca wersja).
- **Odtworzenie kopii z v4** (zdjęcie dzielone, łącza, profilowe) pokrywa istniejący test „a fresh phone restores
  them with the fingerprint of the source” na danych debug, które mają teraz wspólne zdjęcie. Odcisk zgodny.
- **Granica testu „Odrzuć” na ekranie:** okrąg 1a wyświetla przygotowany plik, a loader obrazów w teście na Windows
  trzyma go otwartym. Skasowanie pliku sprawdza więc test szkicu, a test ekranu sprawdza okno i pustą bazę. Na
  Androidzie otwarty plik da się usunąć, a resztki i tak czyści `clearWork` przy starcie.

### Agent checks on the emulator `Medium_Phone` (release, wymyślone dane i obrazy wygenerowane poza repo)
- **Migracja na urządzeniu:** v4 zainstalowany na v3 z ISSUE-016 (tabela w *Dev report*). Liczby wierszy v3 bez zmian,
  „Zdjęcia osób (łącza)” 0, zdjęcie nagrobka jest.
- **Kopia po migracji (R6):** „Ostatnia udana kopia 17:30 (w tle)” po migracji o 17:16 i zmianach o 17:20, czyli
  10 min ciszy. Liczby po kopii: wpisy zdjęć 4, łącza 4, pliki 4.
- **F1:** kolejność zaznaczania (*Dev report*).
- **Filtr w D:** „test” zostawia tylko osobę z innego grobu (bez polskich znaków i końcówek). Pozostałe ekrany i
  zrzuty — przegląd `ui` niżej.
- **Próbne odtworzenie na drugim emulatorze — nie wykonane.** Kopia na `Medium_Phone` jest zaszyfrowana hasłem
  testowym z ISSUE-016, którego w tej sesji nie było. Pokrywają to F3 (kopia v3 → v4) i test odtworzenia danych debug
  z v4. Oba używają prawdziwego archiwum z kodu produkcyjnego.
- **Dane rodziny w zmianach:** w kodzie, testach i vaulcie tylko wymyślone osoby (Wymyślony, Zmyślony, Testowy);
  żadnych plików `*.png`, `*.jpg`, `*.db`, `*.age`, `*.html`, `*.pdf`. **Granica:** bez porównania z notatkami rodziny,
  bo `family_data_dir` nie był w tej sesji czytany (*Do retro* w `CURRENT_STATE.md`).

### ui review (subagent bez historii, ze zrzutów emulatora i kodu)
**0 BLOCKER · 1 MAJOR · 5 MINOR — wszystkie poprawione przed stopem #2** (*Dev report* → *Fixes after the ui
review*).

Zgodne:
- elementy i kolejność wszystkich ekranów;
- role akcentu, pary kontrastu z tokenów (bez nowych), cele dotyku ≥ 48 dp;
- kolor nigdy jedynym nośnikiem;
- profilowe 96, 80 i 40 dp, wysokość zdjęcia w D 160 dp (zmierzone ze zrzutów);
- karta osoby z miniaturą tej samej wysokości (pomiar z [[grob]] v3.1 dalej obowiązuje);
- na zrzutach tylko wymyślone osoby.

Nie sprawdzono ze zrzutów: TalkBack, Switch Access i Voice Access na urządzeniu; układ przy szerokości 360 dp i dużej
czcionce; stany przygotowania i błędu (są w testach).

**Poza zakresem — do decyzji autora:** ten sam wzorzec semantyki (przycisk bez akcji dotknięcia) jest w starszym
kodzie: „Dodaj zdjęcie nagrobka” (`grave_screen.dart`, ISSUE-016) i podgląd cmentarza z bazy
(`base_preview_screen.dart`, ISSUE-015).

### State left on the emulator (dla autora)
- **`Medium_Phone`:** release v4.
- **Grób „Grob wymyslonych”:**
  - Anna — 3 zdjęcia, profilowe zielone;
  - Jan — wspólne zdjęcie niebieskie;
  - **Ewa i Zofia** bez zdjęć. Imiona zmienił agent: w ISSUE-016 obie miały wpisane „as”, a na liście „Kto jest na
    zdjęciu?” dwie jednakowe osoby myliłyby się.
- **Drugi grób:** „Jozef z d. Testowy”.
- **Galeria:** `Pictures/wymyslone-1…3.png` (kolorowe paski, bez osób).
- **Kopia:** dalej do Pobranych emulatora, z hasłem testowym z ISSUE-016.

### Manual (stop #2) — autor i agent, emulator `Medium_Phone`, 2026-10-07
- **Autor, kroki 1 i 3 — wykonane.** Sprawdzone na urządzeniu, bo to odpowiedź „względnie ok”, a nie „ok”:
  - jedno okno wyboru zdjęć o 17:59 (`PICK_IMAGES` w logcacie);
  - Ewa ma 3 zdjęcia, a Zofia — wspólne zdjęcie Ewy jako profilowe.

  **Krok 2** nie zostawia śladu w stanie, więc jest nieoceniony.
- **Odpowiedź autora:** *„jest względnie ok, ale co z sytuacją, gdy jest to zdjęcie «grupowe» — zakładałem, że gdy
  wybieram dane zdjęcie, to mogę ustalić jego «kadr» z liniami pomocniczymi, aby na profilowym była właśnie ta osoba,
  a nie całe zdjęcie”*.
  - To spełnia warunek obalający [[wpis-osoby]] D-zdjęcie-3 („środek zdjęcia nie trafia w twarz → kadrowanie jako
    osobna pozycja”). Kadr był poza zakresem tej pozycji: *Out of Scope* i stop #1.
  - **Decyzja autora:** *„tak zróbmy”*. ISSUE-017 zamknąć tak, jak jest, a **kadr profilowego** zrobić jako **następną
    pozycję, przed [[US-003-przepisanie-rodziny]]**.
  - Kierunek: kadr (`CROP` z GEDCOM 7) przy łączu osoba–zdjęcie, osobny dla każdej osoby; ekran z okręgiem i liniami
    pomocniczymi; schemat v5 (`addColumn`).
- **Kroki 4–7 wykonał agent przez `adb`.** Autor zgodził się zamknąć pozycję „tak, jak jest”, a te kroki są
  funkcjonalne, nie dotyczą odczucia:
  - **krok 4 (D2 „później”):** u Ewy wspólne zdjęcie → „Zmień” → filtr „test” → „Jozef z d. Testowy” z innego grobu →
    „Na zdjęciu: Ewa Wymyslona, Zofia Wymyslona, Jozef” → „Zapisz”. Józef ma 1 zdjęcie ✅;
  - **krok 5:** u Zofii „Usuń z tej osoby” → okno „Usunąć zdjęcie z tej osoby?”, „Zdjęcie zostaje u: Ewa Wymyslona,
    Jozef. Osoba nie będzie miała zdjęcia.” → „Usuń” → „Ta osoba nie ma zdjęć.” → „Zapisz”. Ewa dalej ma 3 ✅;
  - **krok 6:** jedno zdjęcie dodane → wstecz → „Odrzucić wpis?” z treścią „Wpisane dane i zmiany zdjęć nie zostaną
    zapisane.” → „Odrzuć”. Ewa ma znów 3 ✅;
  - **krok 7:** aparat emulatora → „Done” → „Zdjęcie 4 z 4” → „Zapisz”. Ewa ma 4 ✅.

  **Stan końcowy na „Stanie danych”:** zdjęcia (wpisy) 8, łącza 9, pliki 8, odcisk `a31a18867b14952e`. Zgadza się z
  krokami: nagrobek 1, Anna 3 i Ewa 4 to wpisy; łącza to Anna 3, Jan 1, Ewa 4 i Józef 1, a Zofia 0.
- **Odczucie z kroku 7** (siatka, okrąg profilowego, „Zapisz” po zmianie samych zdjęć — D3, lista „Kto jest na
  zdjęciu?”): autor skomentował tylko kadr, więc reszta jest **nieoceniona**.
- **Poprawka semantyki w starszych ekranach** (ISSUE-015 i ISSUE-016, przegląd `ui`): bez odpowiedzi autora. **Poza
  paczką**, jako kandydat na małą pozycję.

**Po niezależnym przeglądzie US-005** (2026-10-07, [[US-005-zdjecia]] → *Verification (US)*) `qa` dopisał:
- test aparatu przy grobie i przy osobie (uwaga 1);
- odczyt łączy i profilowego po odtworzeniu kopii v4 w teście „end to end” (uwaga 2).

`flutter test`: **391 ✅**.

### Verdict — APPROVED (self-check, z uwagami)
Każde AC ma test i przechodzi; przegląd `ui` poprawiony; stop #2: kroki 1 i 3 autora, kroki 4–7 agenta. Uwagi:
1. **Kadr profilowego ze zdjęcia grupowego** — decyzja autora: następna pozycja (`docs` zakłada).
2. **Próbne odtworzenie na urządzeniu nie wykonane** (brak hasła testowego z ISSUE-016 w sesji). Pokrywają je testy
   odtworzenia na prawdziwych archiwach z kodu produkcyjnego: kopia v4 z danych debug (wspólne zdjęcie, łącza) i F3
   (kopia v3 → v4).
3. **Odczucie D3** (zapis zdjęć z „Zapisz”, inaczej niż przy nagrobku) — nieocenione przez autora.
4. **F1** (kolejność zaznaczania) sprawdzony tylko na Androidzie 16; **HEIF** dalej niesprawdzony (ADR-008).
5. **Semantyka starszych ekranów** (ISSUE-015 i ISSUE-016) — kandydat poza tą paczką.

### Package list for docs
**`grobing-code`** — wszystkie pliki, które zapisała ta pozycja:
- `README.md`;
- `drift_schemas/grobing/drift_schema_v4.json`;
- `lib/data/`: `database.dart`, `database.g.dart`, `database.steps.dart`, `graves.dart`, `photos.dart`;
- `lib/app/data_state_screen.dart`;
- `lib/app/grave/`: `grave_screen.dart`, `person_form_screen.dart`;
- `lib/app/photo/`: `photo_picker.dart`, `photo_source_sheet.dart`, `photo_viewer_screen.dart`, `photos.dart`,
  `person_photo_viewer_screen.dart`, `person_photos_draft.dart`, `person_photos_screen.dart`,
  `photo_people_screen.dart`;
- `lib/dev/`: `fictional_data.dart`, `fictional_photo.dart`;
- `test/app/data_state_screen_test.dart`;
- `test/app/photo/`: `grave_photo_screens_test.dart` (test aparatu po przeglądzie US-005), `person_photos_draft_test.dart`,
  `person_photos_screens_test.dart`;
- `test/backup/`: `backup_archive_test.dart`, `restore_service_test.dart`;
- `test/data/`: `data_state_test.dart`, `database_test.dart`, `photos_test.dart`, `person_photos_test.dart`;
- `test/drift/grobing/`: `migration_test.dart`, `generated/schema.dart`, `generated/schema_v4.dart`;
- `test/support/photo_fakes.dart`.

**`grobing-vault`:**
- `05_DESIGN/`: `zdjecia-osoby.md`, `zdjecie.md`, `wpis-osoby.md`, `grob.md`, `brand/style-b.md`;
- `backlog/issues/ISSUE-017-person-photos.md`;
- `00_START_HERE/TRACEABILITY.md`;
- pliki zamknięcia `docs` (*For docs at closure*, nowa pozycja kadru profilowego, `CURRENT_STATE.md`).

**`grobing-agents`:** brak zmian.

**Kontrola przed `git add`:** tylko wymyślone osoby; żadnych obrazów, baz, kopii ani eksportów. Granica: bez
porównania z notatkami rodziny (*Agent checks*).
