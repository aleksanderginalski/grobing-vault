---
title: "ISSUE-018 — Profile photo crop: the author frames a person's face on a group photo, each person their own crop (schema v5)"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: null
related: "[[US-005-zdjecia]] (rozwinięcie po jej werdykcie — AC US-005 spełnione bez tej pozycji)"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-07
verdict-reviewer: self-check
source: "stop #2 ISSUE-017 (2026-10-07): uwaga autora o zdjęciu grupowym i decyzja „tak zróbmy” — następna pozycja, przed US-003 · GEDCOM 7.0 MULTIMEDIA_LINK → CROP (TOP, LEFT, HEIGHT, WIDTH) · ADR-009 → Follow-ups"
created: 2026-10-07
updated: 2026-10-07
---

# ISSUE-018 — Kadr profilowego

> Z uwagi autora na stopie #2 [[ISSUE-017-person-photos]]: *„co z sytuacją, gdy jest to zdjęcie «grupowe» — zakładałem,
> że gdy wybieram dane zdjęcie, to mogę ustalić jego «kadr» z liniami pomocniczymi, aby na profilowym była właśnie ta
> osoba, a nie całe zdjęcie”*. Decyzja autora: *„tak zróbmy”* — **następna pozycja, przed
> [[US-003-przepisanie-rodziny]]**. To spełnia warunek obalający [[wpis-osoby]] D-zdjęcie-3 („bez kadrowania — obali:
> środek zdjęcia nie trafia w twarz”).

## What to build
1. **Kadr profilowego:** ekran z całym zdjęciem i okręgiem z liniami pomocniczymi, który pokazuje, co zobaczy się w
   profilowym. Okrąg da się przesunąć i powiększyć, a potem „Gotowe”. Wejście (kierunek z ISSUE-017, kształt ustala
   `ui`): przy „Ustaw jako profilowe” i z podglądu zdjęcia osoby.
2. **Kadr należy do łącza osoba–zdjęcie**, nie do zdjęcia (`CROP` przy `OBJE` w GEDCOM 7). Na jednym zdjęciu grupowym
   każda osoba ma własny kadr, a plik zdjęcia się nie zmienia.
3. **Profilowe pokazuje kadr** wszędzie, gdzie jest okręgiem: formularz osoby (1a), karta osoby w [[grob]], nagłówek
   [[zdjecia-osoby]].
4. **Schemat v5:** kolumny kadru w `person_media` (`addColumn`), migracja v4→v5 z testem; kopia po migracji (R6).

## Acceptance Criteria
- [ ] Na zdjęciu grupowym autor ustawia kadr profilowego jednej osoby; okrąg profilowego pokazuje ten kadr w
      formularzu, w karcie grobu i w nagłówku zdjęć osoby.
- [ ] Dwie osoby na tym samym zdjęciu mają różne kadry; plik zdjęcia jest jeden i się nie zmienia.
- [ ] Kadr da się poprawić.
- [ ] Kadr jest w kopii i wraca po odtworzeniu, z odciskiem zgodnym.
- [ ] Migracja v4→v5 zachowuje wszystkie dane; kopia v4 odtwarza się w aplikacji v5; kopia w tle zamawia się po
      migracji.
- [ ] Ekran stosuje wytyczne stylu B ([[style-b]], reguła 14; gesty z alternatywą jednym dotknięciem — SC 2.5.1).

## Out of Scope
- Automatyczne wykrywanie twarzy.
- Kadr miniatur w siatce zdjęć osoby (siatka zostaje wycinana ze środka — [[zdjecia-osoby]] D3), chyba że `ui`
  zaproponuje inaczej na stopie #1.
- Podpis zdjęcia (`TITL`) i źródło rozpoznania osoby na zdjęciu ([[ADR-009-person-photos-record-and-link]] →
  *Follow-ups*).
- Semantyka starszych ekranów (kandydat z przeglądu `ui` ISSUE-017 → `CURRENT_STATE.md`).

## Technical Notes
- **Kanon:** GEDCOM 7.0 `MULTIMEDIA_LINK` → `CROP` z `TOP`, `LEFT`, `HEIGHT`, `WIDTH` (liczby całkowite, piksele) —
  gramatyka przepisana w [[ISSUE-017-person-photos]] → *Prior art*. Zdjęcie w aplikacji to kopia dostępowa 2048 px
  ([[ADR-008-photos-access-copy-and-backup-consistency]]); czy kadr zapisywać w pikselach (jak GEDCOM), czy w ułamkach
  boków — do ADR przy planowaniu (≥ 3 opcje).
- Model: [[ADR-009-person-photos-record-and-link]] — łącze ma miejsce na kolumny kadru; zapis zmian z „Zapisz”
  formularza osoby, w jednej transakcji.
- Okrąg profilowego dekoduje dziś zdjęcie w szerokości 2 × pole (`coverDecodeWidth`); kadr zmieni, co i w jakim
  rozmiarze się dekoduje.
- Dane do testów i weryfikacji wyłącznie wymyślone; obrazy generowane (strażnik danych rodziny).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-017-person-photos]] (baza zdjęć, łącza, profilowe) | technical | `done` (2026-10-07) — [[ADR-009-person-photos-record-and-link]] |
| specyfikacja `ui`: ekran kadru, wejście, linie pomocnicze | design | **gotowa** (2026-10-07) — [[kadr-profilowego]] v1, [[zdjecie]] v1.4 |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC; ręczna weryfikacja na emulatorze; zmiana
schematu, więc test migracji v4→v5; próbne odtworzenie z kopii przechodzi; zero danych rodziny w zmianach.

## Implementation plan
> `planning`, 2026-10-07. **DoR:**
> - jasny zakres ✅;
> - US: [[US-005-zdjecia]] jako `related` — jej AC są spełnione, a pozycja to rozwinięcie z decyzji autora (stop #2
>   ISSUE-017). Pozycja niesie własne AC ✅;
> - krok ścieżki: n/a — M1 ✅;
> - `task-level` ✅.
>
> **Ekrany** — specyfikacje `ui` z 2026-10-07:
> - [[kadr-profilowego]] v1 — **nowy ekran** (K1–K5, decyzje D1–D10);
> - [[zdjecie]] v1.4 — B4': „Ustaw jako profilowe” → kadr; na profilowym „Popraw kadr”, a stan w podtytule paska;
> - [[zdjecia-osoby]] v1.1, [[wpis-osoby]] v4.1, [[grob]] v4.1 — okrąg profilowego pokazuje kadr;
> - wytyczne [[style-b]] v1.10 (reguła 14: ramka kadru jako jedyny wyjątek od „nic na zdjęciu”).
>
> **Makieta:** `makieta-kadr-profilowego.html` w katalogu tymczasowym sesji, ramki 1–6 i wariant odrzucony. Obowiązują
> specyfikacje.
>
> **Warstwa danych:**
> - zmiana schematu v4→v5 (`addColumn`) z testem migracji;
> - odtworzenie kopii v4 w aplikacji v5;
> - próbne odtworzenie kopii z kadrami, także na drugim emulatorze — zaległe z [[US-005-zdjecia]], uwaga 2;
> - kopia w tle zaraz po migracji (R6).
>
> **Źródło faktu:** n/a. Kadr mówi, gdzie na zdjęciu jest twarz, a nie podaje daty, relacji ani miejsca pochówku
> ([[FR-001-provenance]]). Łącze w GEDCOM 7 nie ma `SOUR` ([[ADR-009-person-photos-record-and-link]] pkt 7).

### Prior art (sources, not memory)
- **[GEDCOM 7.0](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html) `CROP`**, odczyt 2026-10-07:
  - `TOP` / `LEFT` — *„a number of pixels to not display from the top/left side of the image”*; domyślnie 0;
  - `HEIGHT` / `WIDTH` — w pikselach, domyślnie wysokość albo szerokość obrazu minus `TOP` albo `LEFT`;
  - błąd: `LEFT + WIDTH` większe niż szerokość obrazu, `TOP + HEIGHT` większe niż wysokość albo `CROP` przy obrazie
    bez zdefiniowanej jednostki piksela.

  Gramatykę łącza (`CROP` przy `OBJE`) przepisał [[ISSUE-017-person-photos]] → *Prior art*.
- **Gramps:** region przy `MediaRef` to narożniki **w procentach** obrazu, liczby całkowite, np.
  `<region corner1_x="51" corner1_y="19" corner2_x="59" corner2_y="33"/>` — źródła w [[kadr-profilowego]] → *Prior art*
  (wątki forum Gramps; wiki zwróciło 403).
- **Kod `grobing-code`, odczyt 2026-10-07:**
  - `PhotoPreparation.kt`: kopia dostępowa jest **obrócona według EXIF przed zapisem i bez EXIF**. Siatka pikseli
    pliku to więc dokładnie to, co widać, a piksele kadru znaczą to samo na każdym ekranie;
  - [[ADR-008-photos-access-copy-and-backup-consistency]]: zdjęcia osoby nie podmienia się w miejscu (w bazie się
    dodaje i usuwa). Plik łącza się nie zmienia, więc piksele kadru się nie starzeją;
  - **`photos.dart` → `applyPersonPhotoEdits` usuwa wszystkie łącza osoby i wstawia je od nowa** (pozycje 0…n−1).
    Kolumny kadru zniknęłyby przy każdej zmianie zdjęć osoby (F1);
  - `data_state.dart`: odcisk danych czyta wszystkie kolumny każdej tabeli z `sqlite_master`, więc kadr wchodzi do
    odcisku bez zmian w kodzie;
  - `_from2To3` (ISSUE-012): `addColumn` bez przebudowy tabeli — ten sam wzorzec dla v5;
  - trzy okręgi profilowego to dziś trzy kopie tego samego `ClipOval` + `Image.file` + `coverDecodeWidth` (formularz
    80 dp, karta 40 dp, nagłówek 96 dp). Kadr zmienia wszystkie trzy, więc powstaje jeden wspólny widżet.

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego · co ją obali |
|---|---|---|---|
| **D1** | **Jednostka zapisu kadru, schemat v5** (→ ADR-010 przy zamknięciu) | **(a) piksele kopii dostępowej, cztery kolumny jak GEDCOM `CROP`**: `crop_left`, `crop_top`, `crop_width`, `crop_height` (liczby całkowite, opcjonalne) w `person_media`; wszystkie puste = bez kadru (środek). Ekran zapisuje kwadrat | Plik łącza się nie zmienia, a jego piksele są wyprostowane (*Prior art*), więc piksele są stabilne. Eksport do GEDCOM 1:1. Liczby całkowite w odcisku danych, bez zaokrągleń. Wymiary zdjęcia potrzebne do rysowania czyta się z nagłówka pliku (każda opcja poza (e) i tak ich potrzebuje). *Obali:* ten sam plik łącza w innej rozdzielczości (np. przyszła kopia z oryginału) — wtedy migracja przelicza kadr proporcjonalnie, bo wymiary obu plików są znane |
| | opcja (b) | ułamki boków (`REAL` 0…1) | niezależne od rozdzielczości, ale plik się nie zmienia, więc nic na tym nie zyskujemy. Kwadrat w pikselach wymaga zaokrągleń, a eksport i tak liczy piksele z wymiarów — **odrzucona** |
| | opcja (c) | środek i promień okręgu w ułamkach | zapisuje okrąg, a GEDCOM i każdy przyszły kadr prostokątny (np. węzeł drzewa, podpis) potrzebują prostokąta — **odrzucona** |
| | opcja (d) | procenty całkowite jak region w Gramps | za grube: 1% to ok. 20 px zdjęcia 2048 px, a przy najmniejszym kadrze (128 px, [[kadr-profilowego]] D5) krok to ok. 16% kadru — twarz „skacze” — **odrzucona** |
| | opcja (e) | osobny plik wycinka (mały JPEG twarzy) przy każdym łączu | rysowanie najprostsze, ale to dodatkowe pliki w kopii i w sprzątaniu (ADR-008 pkt 3), a każda poprawka kadru oznacza nowy plik. AC mówi „plik zdjęcia jest jeden” — **odrzucona**; wraca tylko, gdyby F6 wypadł źle |
| **D2** | **Nieruchomy okrąg, pod nim przesuwa się zdjęcie** ([[kadr-profilowego]] D1) — inaczej niż w opisie pozycji („okrąg da się przesunąć i powiększyć”) | tak | Twarz na zdjęciu grupowym ma na ekranie ok. 20 dp, więc ruchomy okrąg tej wielkości trudno ustawić palcem. Pod nieruchomym okręgiem twarz przybliża się do ok. 300 dp. Zapis jest ten sam (D1), więc zmiana dotyczy tylko gestów. **Porównanie na makiecie:** ramka 3 i ramka „wariant”. *Obali:* autor woli widzieć całe zdjęcie i przesuwać okrąg |
| **D3** | **„Ustaw jako profilowe” prowadzi przez kadr** ([[kadr-profilowego]] D2) | tak, +1 dotknięcie („Gotowe”) | Profilowe to okrąg, więc autor widzi wycinek, zanim zdjęcie zostanie profilowym. *Obali:* autor ustawia profilowe głównie z portretów i „Gotowe” go spowalnia — wtedy kadr tylko przez „Popraw kadr” |
| **D4** | **Pozostałe decyzje projektowe `ui` (pakiet)** | przyjąć | bez kadru = środek, a kadr nie otwiera się sam po pierwszym zdjęciu (D3) · okrąg zawsze cały na zdjęciu (D4) · największe przybliżenie: okrąg obejmuje 128 px (D5) · linie trójpodziału zawsze widoczne (D6) · dotknięcie twarzy i „Pomniejsz”/„Powiększ” zamiast gestów (D7, SC 2.5.1) · „Popraw kadr” i podtytuł „Zdjęcie profilowe” w podglądzie (D8) · wstecz bez okna (D9) · pierścień w akcencie między liniami w kolorze tła (D10) |

### Stop #1 — odpowiedź autora (2026-10-07)
- **D1:** „ok” — piksele kopii dostępowej, cztery kolumny `CROP` przy łączu.
- **D2:** *„zróbmy według Twojej rekomendacji”* — nieruchomy okrąg, pod nim przesuwa się zdjęcie.
- **D3:** „ok” — „Ustaw jako profilowe” przez kadr.
- **D4:** „ok” — pakiet decyzji `ui`.

### Falsifier — what is measured and what is not
| # | Pytanie | Wynik |
|---|---|---|
| F1 | Czy zmiana zdjęć osoby (dodanie, kolejność, usunięcie innego zdjęcia) zachowa kadr łączy, których nie dotyka? | ❌ **z kodu:** `applyPersonPhotoEdits` przepisuje łącza osoby od zera. Plan: edycje niosą kadr każdego łącza osoby (krok 2c). **Zmierzy** test: osoba z kadrem na profilowym dostaje nowe zdjęcie i traci inne → kadr profilowego bez zmian |
| F2 | Czy migracja v4→v5 zachowuje wszystkie dane? | **Zmierzy** test migracji: wymyślona baza v4 ze zdjęciem nagrobka, zdjęciem dzielonym przez dwie osoby i drugim zdjęciem jednej z nich → w v5 te same wiersze, pozycje i liczby; kolumny kadru puste; `PRAGMA foreign_key_check` pusty |
| F3 | Czy kopia v4 odtwarza się w aplikacji v5? | **Zmierzy** test odtworzenia na kopii v4 zrobionej kodem testowym (wzorzec F3 z ISSUE-017) |
| F4 | Czy kadr jest w kopii i wraca z odciskiem zgodnym? | **Zmierzy** test „end to end” (kopia v5 z dwoma różnymi kadrami na jednym zdjęciu → odtworzenie → kadry i odcisk równe) i **agent** na emulatorach: nowe hasło testowe, kopia z `Medium_Phone` → odtworzenie na `Grobing_Restore` |
| F5 | Czy piksele kadru znaczą to samo co na ekranie (obrót)? | ✅ **z kodu:** `PhotoPreparation.kt` obraca według EXIF przed zapisem i usuwa EXIF |
| F6 | Ile kosztuje okrąg z małym kadrem? Wycinek 128 px w okręgu 40 dp (ok. 104 px ekranu) wymaga dekodowania prawie całego zdjęcia (do 2048 px, ok. 12 MB w pamięci na plik) | **Zmierzy** `dev` na emulatorze: grób z 6 wymyślonymi osobami, każda z kadrem 128–300 px z innego obrazu → przewijanie bez szarpnięć i `adb shell dumpsys meminfo` przed i po. Źle → dekodowanie z limitem 1× zamiast 2× dla okręgów ≤ 40 dp, a jeśli to za mało — wraca D1 (e) |
| F7 | Odczucie kadru (D2, D3, D6, D8) | **Nie zmierzone** — autor na stopie #2 |

### Scope diff vs the item
- **zakres według pozycji:** kadr, kadr przy łączu, okręgi z kadrem, schemat v5 — bez zmian.
- **± kształt ekranu (D2):** nieruchomy okrąg zamiast ruchomego. Pozycja zostawiła kształt `ui` i wymieniła ruchomy
  okrąg jako kierunek.
- **+ „Popraw kadr” i podtytuł „Zdjęcie profilowe”** w podglądzie — kształt wejścia „z podglądu zdjęcia osoby” z
  pozycji.
- **+ wspólny widżet okręgu profilowego** w miejsce trzech kopii — kadr zmienia wszystkie trzy naraz.
- **+ poprawka przepisywania łączy (F1)** — konsekwencja kolumn przy łączu.
- **bez zmian:** siatka bazy zdjęć (środek), podgląd poza paskiem, nagrobek, brak `INTERNET`, styl B.

### Steps (dev)
0. **Przed zmianą:** na `Medium_Phone` jest build release v4 z wymyślonymi osobami i zdjęciami (stan po stopie #2
   ISSUE-017). **Nie odinstalowuj** — aktualizacja na tych danych to sprawdzenie migracji na urządzeniu (`qa`).
1. **Schemat v5** — `lib/data/database.dart`:
   - a. `PersonMedia`: `cropLeft`, `cropTop`, `cropWidth`, `cropHeight` — `IntColumn` opcjonalne. Komentarz: GEDCOM 7
     `CROP` przy `OBJE`, piksele kopii dostępowej, wszystkie puste = środek, kadr w obrębie obrazu (granicy SQL nie
     sprawdzi, bo wymiary zdjęcia nie są w bazie — pilnuje jedna funkcja zapisu, krok 2d). Komentarz przy tabeli
     („would be columns here, added when a screen needs them”) zaktualizuj;
   - b. `currentSchemaVersion = 5`, `dart run drift_dev make-migrations` (schemat v5 w `drift_schemas/grobing/`, testy w
     `test/drift/grobing/generated/`);
   - c. `_from4To5`: cztery `addColumn` — bez zmiany wierszy i bez przebudowy (wzorzec `_from2To3`);
   - d. `build_runner build`.
2. **Dane** — `lib/data/photos.dart`:
   - a. **`PhotoCrop`** — wartość (`left`, `top`, `width`, `height`, liczby całkowite, piksele) z `==`;
   - b. odczyt: `PersonPhoto.crop`; `profilePhotoPaths` → **`profilePhotos`**: ścieżka i kadr pierwszego łącza każdej
     osoby;
   - c. **`PersonPhotoEdits.crops`** — kadr każdego łącza tej osoby po edycji (brak = bez kadru).
     `applyPersonPhotoEdits` zapisuje je przy przepisywaniu łączy, więc kadr łącza, którego edycja nie zmienia,
     zostaje (**F1**). Łącza **innych** osób (część D) zachowują swój kadr, bo edycja ich nie przepisuje — tylko
     dodaje na końcu albo usuwa;
   - d. niezmiennik w jednym miejscu: zapis kadru = cztery wartości albo żadna, `width`, `height` > 0, przesunięcia
     ≥ 0. Granicę obrazu pilnuje ekran (krok 4), a rysowanie i tak przycina kadr do obrazu (krok 5).
3. **Grób** — `lib/data/graves.dart`: `BuriedPerson.profilePhotoPath` → także `profileCrop`; `_watch` czyta przez
   `profilePhotos`.
4. **Geometria** — nowy `lib/app/photo/crop_geometry.dart`, czyste funkcje (testowalne bez ekranu):
   - kadr domyślny: największy kwadrat ze środka;
   - przycięcie kadru do obrazu i do granic przybliżenia: od krótszego boku do `min(128, krótszy bok)` px;
   - przejście kadr ↔ widok (skala i przesunięcie zdjęcia pod okręgiem o danej średnicy);
   - dotknięcie punktu → ten punkt na środku okręgu; „Powiększ”/„Pomniejsz” ×1,5 wokół środka okręgu;
   - szerokość dekodowania okręgu: `min(szerokość obrazu, 2 × px okręgu × szerokość obrazu / szerokość kadru)`.
5. **Wspólny okrąg profilowego** — nowy `lib/app/photo/profile_circle.dart`:
   - plik + kadr (albo brak) + średnica, opcjonalnie wygląd błędu (karta: tło, 20 dp; formularz i nagłówek:
     powierzchnia);
   - wymiary zdjęcia z nagłówka pliku (`ImageDescriptor`), zapamiętane na ścieżkę;
   - dekodowanie w szerokości z kroku 4 (F6), wycinek rysowany w okręgu; bez kadru — środek, jak dziś.

   Używają go `_PhotoField` (`person_form_screen.dart`, 80 dp), `_ProfileThumbnail` (`grave_screen.dart`, 40 dp) i
   `_ProfileHeader` (`person_photos_screen.dart`, 96 dp).
6. **Ekran kadru** — nowy `lib/app/photo/profile_crop_screen.dart`, [[kadr-profilowego]] K1–K5 i *States*:
   - wejście: plik, imiona i nazwisko osoby, kadr początkowy (łącza albo domyślny);
   - wynik: `PhotoCrop` po „Gotowe”, `null` po wstecz;
   - gesty: przesunięcie i rozsunięcie palców (`onScale*`), dotknięcie = środek (animacja 250 ms), przyciski K4 z
     `tooltip`; zdjęcie zatrzymuje się na krawędzi, bez odbicia;
   - warstwa okręgu (`CustomPainter`): przyciemnienie tłem 72% poza okręgiem, pierścień 2 dp w akcencie między liniami
     1 dp w kolorze tła, linie trójpodziału — wartości ze specyfikacji, kolory z `theme.dart`;
   - stan „błąd odczytu” (K4, K5 nieaktywne).
7. **Zmiany w formularzu** — `lib/app/photo/person_photos_draft.dart`:
   - kadr każdego zdjęcia w kolejności (z zapisu przy `load()`);
   - `setProfile(photo, crop)` (pierwsze miejsce i kadr), `setCrop(photo, crop)`, `cropOf(photo)`;
   - `hasChanges` widzi zmianę kadru (linia 6 w [[zdjecia-osoby]], okno „Odrzucić wpis?”);
   - `edits()` niesie kadry wszystkich łączy osoby (F1).
8. **Podgląd** — `lib/app/photo/person_photo_viewer_screen.dart` ([[zdjecie]] v1.4):
   - podtytuł paska: „Zdjęcie profilowe” na pierwszym zdjęciu, inaczej „Zdjęcie osoby”;
   - „Ustaw jako profilowe” → ekran kadru (kadr łącza albo domyślny) → wynik → `setProfile` → pierwsze zdjęcie;
     wstecz z kadru niczego nie zmienia;
   - na profilowym zamiast „✓ Profilowe” **„Popraw kadr”** (`Icons.crop_outlined`, akcent) → ekran kadru → `setCrop`.
     Dwa stałe miejsca w dolnym pasku zostają.
9. **Dane debug** — `lib/dev/fictional_data.dart` (obrazy rysowane w kodzie, `fictional_photo.dart`): zdjęcie grupowe
   z ISSUE-017 dostaje u dwóch osób **różne kadry** na rysowanych twarzach, żeby kadr było widać od pierwszego
   uruchomienia buildu debug.
10. **README** → *Baza danych*: akapit „Kadr profilowego (schemat v5)”:
    - kolumny `CROP` przy łączu, piksele kopii dostępowej;
    - brak kadru = środek;
    - kadr przeżywa każdą edycję zdjęć osoby (F1).
11. `dart format` · `flutter analyze` · `flutter test`. Build release i instalacja **na** buildzie v4 z kroku 0, bez
    odinstalowania. Pomiar F6, wynik w *Dev report*.

### Files likely touched
- **Kod danych:**
  - `lib/data/database.dart`, `database.g.dart`, `database.steps.dart`;
  - `drift_schemas/grobing/drift_schema_v5.json`;
  - `lib/data/photos.dart`, `lib/data/graves.dart`.
- **Kod ekranów:**
  - nowe: `lib/app/photo/crop_geometry.dart`, `profile_circle.dart`, `profile_crop_screen.dart`;
  - `lib/app/photo/person_photos_draft.dart`, `person_photo_viewer_screen.dart`, `person_photos_screen.dart`;
  - `lib/app/grave/person_form_screen.dart`, `grave_screen.dart`.
- **Debug i dokumentacja:** `lib/dev/fictional_data.dart`, `README.md`.
- **Testy (`qa`):**
  - `test/drift/grobing/migration_test.dart` i `generated/` (v5);
  - `test/data/photos_test.dart`, `graves_test.dart`, `data_state_test.dart`;
  - `test/backup/restore_service_test.dart`;
  - nowe: `test/app/photo/crop_geometry_test.dart`, `profile_crop_screen_test.dart`;
  - `test/app/photo/person_photos_screens_test.dart`, `test/app/grave/`.

### AC → tests (`qa`)
| AC | Test |
|---|---|
| kadr na zdjęciu grupowym; okrąg w formularzu, karcie i nagłówku | widget: podgląd zdjęcia grupowego → „Ustaw jako profilowe” → ekran kadru → dotknięcie punktu i „Powiększ” → „Gotowe” → podtytuł „Zdjęcie profilowe” → nagłówek, 1a i (po „Zapisz”) karta dostają ten kadr (`ProfileCircle.crop`); dane: kadr przy łączu |
| dwie osoby, różne kadry, jeden plik bez zmian | dane: dwa łącza do jednego `media` z różnymi kadrami; plik w `media/zdjecia/` bajt w bajt ten sam przed zapisem kadru i po nim |
| kadr da się poprawić | widget: „Popraw kadr” otwiera ekran na zapisanym kadrze → zmiana → „Gotowe” → „Zapisz” → nowy kadr w danych |
| kadr w kopii i po odtworzeniu, odcisk zgodny | F4: kopia v5 z kadrami → odtworzenie → kadry i odcisk równe; `data_state_test`: zmiana samego kadru zmienia odcisk |
| migracja v4→v5; kopia v4 w v5; kopia po migracji | F2 + wygenerowane testy schematu; F3; istniejący test startu (R6) dalej zielony |
| styl B, gesty z alternatywą (SC 2.5.1) | widget: dotknięcie przenosi punkt na środek; „Powiększ” nieaktywny przy 128 px, „Pomniejsz” przy krótszym boku; przegląd `ui` (subagent) ze zrzutów |
| F1 | dane: osoba z kadrem na profilowym → dodanie zdjęcia i usunięcie innego w jednej edycji → kadr profilowego bez zmian; łącze innej osoby do tego zdjęcia zachowuje jej kadr |
| geometria | jednostkowe: kadr domyślny (poziome, pionowe, kwadratowe zdjęcie), przycięcie do obrazu i granic, kadr ↔ widok w obie strony, dotknięcie, krok ×1,5, szerokość dekodowania |
| wstecz z kadru | widget: wstecz → `null`, profilowe i kadr bez zmian, bez okna |
| błąd odczytu | widget: plik nieczytelny → komunikat, „Gotowe” nieaktywne |

### Manual verification (stop #2) — kroki według miejsca
**Emulator `Medium_Phone`, build release (autor — UI/UX).** Wymyślone osoby i obrazy są na emulatorze od ISSUE-017;
`qa` dogra wymyślone zdjęcie grupowe przez `adb`, jeśli trzeba.
1. Grób z wymyślonymi osobami → osoba ze zdjęciem grupowym → okrąg → baza zdjęć → zdjęcie grupowe → **„Ustaw jako
   profilowe”** → ekran „Kadr profilowego”: przesuń zdjęcie palcem, rozsuń palce (albo „Powiększ”), dotknij twarzy →
   „Gotowe”. W pasku „Zdjęcie profilowe”, w dolnym pasku „Popraw kadr” → wstecz: nagłówek pokazuje twarz → wstecz:
   okrąg formularza pokazuje twarz → „Zapisz” → karta w grobie pokazuje twarz.
2. Druga osoba na tym samym zdjęciu → ten sam przepływ, **inna twarz** → w widoku grobu dwie karty z dwiema różnymi
   twarzami z jednego zdjęcia.
3. Pierwsza osoba → okrąg → nagłówek → **„Popraw kadr”** → ekran otwiera się na zapisanym kadrze → przesuń → „Gotowe” →
   wstecz → „Zapisz” → karta pokazuje nowy kadr.
4. **Odczucie** (napisz tutaj): nieruchomy okrąg i linie trójpodziału (D2, D6), „Gotowe” przy każdym profilowym (D3),
   czy „Zdjęcie profilowe” w pasku wystarcza, żeby wiedzieć, które zdjęcie jest profilowe (D8).

**Agent (bez autora):**
- aktualizacja na buildzie v4 z kroku 0: liczby wierszy, łącza i pozycje bez zmian, kolumny kadru są, kopia zamówiona
  po starcie;
- wstecz z ekranu kadru bez „Gotowe” → bez zmian;
- **F4 na urządzeniu:** nowa konfiguracja kopii z nowym hasłem testowym (wymyślone dane), kopia do Pobranych →
  odtworzenie na `Grobing_Restore` → odcisk zgodny, kadry w bazie równe;
- F6 (pamięć i przewijanie);
- „Stan danych” bez błędów po migracji.

### Out of Scope (this plan)
- Automatyczne wykrywanie twarzy; kadr miniatur w siatce; kadr zdjęcia nagrobka.
- Kadr z oryginału w wyższej rozdzielczości (oryginał zostaje w galerii — ADR-008).
- Otwieranie kadru samo po pierwszym zdjęciu osoby i kadr dla innych osób zaznaczanych w „Kto jest na zdjęciu?”
  ([[kadr-profilowego]] D3 — falsyfikator tam).
- Kadr prostokątny (model go przyjmie, ekran zapisuje kwadrat), podpis `TITL`, źródło rozpoznania osoby.
- Semantyka starszych ekranów (kandydat w `CURRENT_STATE.md`).

### For docs at closure
- **ADR-010 — kadr profilowego: piksele kopii dostępowej przy łączu (schemat v5)** z D1: opcje (a)–(e), GEDCOM 7
  `CROP` (cytaty wyżej), region w Gramps, F5 (obrót przed zapisem) i F6 (koszt dekodowania).
- [[ADR-009-person-photos-record-and-link]] → *Follow-ups*: datowany dopisek „kadr → ADR-010”.
- `04_ARCHITECTURE/data-model.md` → *Media*: kolumny kadru przy łączu, brak = środek.
- `04_ARCHITECTURE/backup-format.md`: bez zmiany formatu; kadr w bazie i w odcisku.
- `glossary.md`: **kadr profilowego** (wycinek zdjęcia przy łączu osoba–zdjęcie, osobny dla każdej osoby).
- [[NFR-003-migracje-schematu]]: migracja v4→v5. [[US-005-zdjecia]] → *Notes*: uwaga 2 (odtworzenie na urządzeniu)
  zamknięta przez F4, jeśli przejdzie.

### Self-check (planning) — said out loud
1. **Kompletność:** zakres, decyzje, falsyfikatory, kroki, pliki, AC → testy, kroki ręczne według miejsca, *Out of
   Scope* ✅.
2. **Spójność:** plan idzie za specyfikacjami `ui` (2026-10-07) i pozycją. Zmiana kształtu ekranu względem opisu
   pozycji (D2) i +1 dotknięcie (D3) idą na stop #1 jawnie.
3. **Własność:** ta sekcja, `status: in-progress`, kolumny Issue(s) i Issue Status w `TRACEABILITY.md`. ADR-010 pisze
   `docs` przy zamknięciu, jak ADR-009. Specyfikacje zmieniał `ui`.
4. **Warstwa danych:**
   - test migracji v4→v5 z danymi (F2) ✅;
   - odtworzenie kopii v4 w v5 (F3) i kopii z kadrami (F4), także na urządzeniu ✅;
   - kopia po migracji (R6) ✅;
   - źródło faktu: n/a z uzasadnieniem ✅.
5. **Wystarczalność — czego plan nie ma:**
   - **prawdziwego zdjęcia grupowego** — kadr sprawdzą wymyślone obrazy; czy 128 px wystarcza na twarz ze starego
     zdjęcia, pokaże dopiero przepisywanie ([[kadr-profilowego]] D5);
   - **dużej czcionki i TalkBacka na ekranie kadru** — tylko z kodu i przeglądu `ui`;
   - **F6 na telefonie** — emulator ma inną pamięć niż telefon autora; pomiar to sygnał, nie dowód.

## Dev report
> `dev`, 2026-10-07. Flutter 3.41.1 (przypięty) ✅. Kroki planu 0–11 zrobione; odstępstwa niżej.

### What was built
- **Schemat v5** (`database.dart`): `person_media` + `crop_left`, `crop_top`, `crop_width`, `crop_height` (opcjonalne);
  `_from4To5` — cztery `addColumn`. `drift_schema_v5.json`, `database.steps.dart`, `database.g.dart` wygenerowane.
- **Dane** (`photos.dart`): `PhotoCrop` (z `PhotoCrop.of(link)`: cztery wartości z dodatnim rozmiarem albo brak),
  `PersonPhoto.crop`, `profilePhotos` (ścieżka + kadr; **zastępuje `profilePhotoPaths`**), `PersonPhotoEdits.crops`.
  `applyPersonPhotoEdits` czyta kadry łączy osoby przed przepisaniem i zapisuje je z powrotem, chyba że edycja ustawiła
  nowy (**F1**). `graves.dart`: `BuriedPerson.profileCrop`.
- **Geometria** (`lib/app/photo/crop_geometry.dart`, czyste funkcje): `middleSquare`, `squareOf`, `clampSquare`,
  `moveAndScale`, `centreOn`, `zoomed` (×1,5), `canZoomIn`/`canZoomOut`, `cropDecodeWidth`; granica 128 px.
- **Wspólny okrąg** (`profile_circle.dart`): `ProfileCircle` (plik, kadr, średnica, wygląd błędu) i `imageSizeOf`
  (wymiary z nagłówka pliku, zapamiętane na ścieżkę). Używają go formularz (80), karta grobu (40) i nagłówek bazy (96).
- **Ekran kadru** (`profile_crop_screen.dart`): K1–K5 i stany ze specyfikacji; gesty `onScale*`, dotknięcie =
  środek, przyciski z `tooltip`; warstwa `_CropFramePainter` (przyciemnienie 72 %, trójpodział 60 % z cieniem,
  pierścień 2 dp w akcencie między liniami tła). Kolory tylko z `theme.dart`.
- **Formularz** (`person_photos_draft.dart`): `cropOf`, `setCrop`, `setProfile(photo, crop:)`; `hasChanges` widzi kadr.
- **Podgląd** (`person_photo_viewer_screen.dart`): podtytuł „Zdjęcie profilowe” na pierwszym zdjęciu; „Ustaw jako
  profilowe” → kadr → profilowe z kadrem; na profilowym „Popraw kadr” (`crop_outlined`).
- **Dane debug** (`fictional_data.dart`): „zdjęcie ślubne” ma u matki i ojca różne kadry na rysowanych głowach.
- **README** → *Baza danych*: akapit „Kadr profilowego (schemat v5)”.

### Checks (dev, host Windows + emulator `Medium_Phone_API_36.1`, build release)
- `dart format` ✅ · `flutter analyze lib` — czyste. `flutter analyze` całości: 2 błędy w
  `test/data/person_photos_test.dart` (`profilePhotoPaths` → `profilePhotos`) — dla `qa`.
- `flutter test`: **372 ✅, 7 ❌** — wszystkie z planowanej zmiany, do dostosowania przez `qa`:
  - `data_state_screen_test` („schema version…”), `database_test` (AC-2, `user_version 4`), `data_state_test` („schema
    4”), `restore_service_test` (ISSUE-017 F3: oczekuje `(3, 4)`, jest `(3, 5)`) — wersja schematu 5;
  - `person_photos_screens_test` („Ustaw jako profilowe” → „✓ Profilowe”) — teraz przez ekran kadru, a na profilowym
    „Popraw kadr” ([[zdjecie]] v1.4);
  - `person_photos_screens_test` („Zrób zdjęcie” z bazy) — **sam przechodzi**; w pełnym przebiegu pada za poprzednim
    testem z tego pliku;
  - `person_photos_test.dart` — nie kompiluje się (`profilePhotoPaths`).
- **Migracja v4→v5 na urządzeniu** (release zainstalowany na buildzie v4 z 17:50, bez odinstalowania; zrzuty „Stan
  danych” przed i po w katalogu tymczasowym sesji, `shots/00…`, `01…`): wersja schematu 4 → **5**; liczby wierszy
  **równe** (osoby 5 · zdarzenia 4 · cmentarze 1 · groby 2 · pochówki 5 · twierdzenia 9 · zdjęcia 8 · łącza 9 · pliki
  8). Odcisk `a31a18867b14952e` → `1953bf47d3119e50` — zmiana oczekiwana, bo kolumny weszły do odcisku (ADR-009 →
  *Consequences*). Kopia w tle po migracji: jeszcze nie widziana (ostatnia 18:25, sprzed instalacji) — dla `qa` (R6).
- **Przepływ na urządzeniu (wymyślone dane):**
  - Jan → baza → profilowe → **„Popraw kadr”** → ekran kadru (środek, „Pomniejsz” nieaktywny) → dotknięcie,
    „Powiększ” → „Gotowe” → podgląd: „Zdjęcie profilowe”, „Popraw kadr”; nagłówek, okrąg formularza i — po „Zapisz” —
    karta w grobie pokazują kadr; siatka zostaje ze środka; linia zapisu widoczna;
  - Anna → to samo zdjęcie (wspólne z Janem) → **„Ustaw jako profilowe”** → kadr startuje ze środka (jej łącze nie ma
    kadru) → inny wycinek → „Gotowe” → „1 z 3” → „Zapisz”: **dwie karty, dwa różne wycinki jednego zdjęcia** (AC 2).
- **F6 — pomiar (sygnał, nie dowód):** cztery osoby w grobie z profilowym z innego wymyślonego obrazu 2048 × 1536
  (`Pictures/wymyslone-duze-1…4.jpg`), każde przy największym przybliżeniu (kadr 128 px), więc okrąg 40 dp dekoduje
  cały plik (2048 px). `dumpsys meminfo` po świeżym starcie: mapa — PSS 81,6 MB, natywna sterta 24,2 MB; widok grobu —
  PSS 76,8 MB, natywna sterta 29,1 MB. **Emulator nie pokazuje pamięci grafiki** („Graphics: 0”), a tekstury czterech
  zdjęć to ok. 4 × 12,6 MB. Widok otworzył się bez widocznego opóźnienia. `gfxinfo` nie mierzy klatek Fluttera. Wniosek:
  **bez zmiany kodu**; prawdziwy pomiar na telefonie przy MVP. Gdyby zabrakło pamięci, plan ma odpowiedź (limit 1× dla
  okręgów ≤ 40 dp, potem D1 (e)).

### Deviations from the plan
1. **Krok 2c:** edycja niesie tylko kadry ustawione w tej edycji (`crops`), a kadr łącza, którego edycja nie nazywa,
   zostaje w danych — zamiast „edycja niesie kadr każdego łącza”. Ten sam skutek (F1), ale niezależnie od tego, czy
   wywołujący zna kadry.
2. **`profilePhotoPaths` → `profilePhotos`** (ścieżka + kadr) zamiast drugiej funkcji obok — testy używające starej
   nazwy dostosuje `qa`.
3. **Okrąg z kadrem przez pierwszą chwilę pokazuje środek**, dopóki nie przeczyta wymiarów z nagłówka pliku (ułamek
   sekundy). Specyfikacja tego stanu nie opisuje.
4. **Przyciski „Pomniejsz”/„Powiększ” też przesuwają płynnie (250 ms)**, jak dotknięcie — specyfikacja mówi o animacji
   tylko przy dotknięciu.
5. `make-migrations` wygenerował `test/drift/grobing/generated/schema_v5.dart` i zmienił `schema.dart` — pliki
   wygenerowane w katalogu `qa`, jak w ISSUE-017.
6. **Obserwacja dla przeglądu `ui`, zgodna z D4:** przy najmniejszym przybliżeniu okrąg obejmuje cały krótszy bok, więc
   zdjęcie 4:3 przesuwa się w bok tylko o 1/8 szerokości. Dotknięcie twarzy przy krawędzi stawia ją na środku dopiero po
   „Powiększ”. Zobaczone na emulatorze (obraz 800 × 600: przesunięcie zatrzymane na krawędzi).

### For qa
- Testy do dostosowania i nowe — *AC → tests* w planie; lista padających wyżej.
- **Stan emulatora `Medium_Phone` (release v5, wymyślone dane):** Jan, Anna, Ewa i Zofia mają jako profilowe nowe obrazy
  `wymyslone-duze-*` z najmniejszym kadrem (pomiar F6). Jan i Anna mają też wspólne zdjęcie w paski z różnymi kadrami
  (Jana — jego wcześniejsze profilowe). Do kroków stopu #2 wystarczy wspólne zdjęcie Jana i Anny: obie osoby mają już
  inne profilowe, więc „Ustaw jako profilowe” na nim zadziała u obu.
- F4 na urządzeniu (nowe hasło testowe, `Grobing_Restore`) i R6 — przed tobą. Dwa emulatory naraz nie mieszczą się w
  pamięci PC: po kolei.

## Verification
> `qa`, 2026-10-07. Testy napisał `qa`; jedną usterkę znalazł test, cztery przegląd `ui`, a poprawił je `dev` (niżej).
> Dane w testach i na emulatorach wyłącznie wymyślone; obrazy generowane (paski, koła, rysowane postacie).

### Automated — `flutter test`: 429 ✅ po zmianie ze stopu #2 (426 przed nią; było 379 + 7 ❌ po `dev`) · `flutter analyze`: czyste · `dart format`: ✅
| AC | Test |
|---|---|
| kadr na zdjęciu grupowym; okrąg w formularzu, karcie i nagłówku | `person_photos_screens_test.dart` „ISSUE-018 AC 1” (zdjęcie wspólne → „Ustaw jako profilowe” → dotknięcie z prawej i „Powiększ” → „Gotowe” → ten sam kadr w nagłówku 96 dp, w okręgu formularza i po „Zapisz” w karcie grobu; kadr na łączu Jana, łącze Anny bez kadru) · `person_photos_test.dart` „AC 1, 3” (dane: łącze, `profilePhotos`, `BuriedPerson.profileCrop`) |
| dwie osoby, różne kadry, jeden plik bez zmian | `person_photos_test.dart` „AC 2” (dwa kadry na jednym `media`, jeden plik, bajty pliku równe przed i po) |
| kadr da się poprawić | `person_photos_screens_test.dart` „ISSUE-018 AC 3” („Popraw kadr” otwiera zapisany kadr; „Gotowe” bez zmian = brak zmiany; „Powiększ” → „Gotowe” → „Zapisz” = nowy kadr wokół tego samego środka) · `profile_crop_screen_test.dart` (kadr łącza wraca bez zmian) |
| kadr w kopii i po odtworzeniu, odcisk zgodny | `restore_service_test.dart` „end to end” (kopia v5 danych debug: odcisk równy, kadry matki i ojca na wspólnym zdjęciu wracają różne, portret bez kadru) · `data_state_test.dart` (zmiana samego kadru zmienia odcisk) |
| migracja v4→v5; kopia v4 w v5; kopia po migracji | `migration_test.dart` „ISSUE-018 F2” (wiersze, łącza i pozycje bez zmian, kolumny kadru puste, `foreign_key_check` pusty) + wygenerowane `from 1…4 to 5` · `restore_service_test.dart` „ISSUE-018 F3” (kopia v4 → v5: liczby, łącza, pliki, kadry puste) · istniejący test startu (R6) zielony |
| styl B, gesty z alternatywą (SC 2.5.1) | `profile_crop_screen_test.dart`: K1–K5, `tooltip`, „Pomniejsz” nieaktywny od środka, 3 × „Powiększ” = 128 px i „Powiększ” nieaktywny, dotknięcie przesuwa kwadrat, wstecz zwraca nic bez okna, błąd odczytu (brak pliku i plik ucięty) · `crop_geometry_test.dart` (13: środek, granice, gesty, ×1,5, 7 kroków do 128 px, szerokość dekodowania) · przegląd `ui` niżej |
| F1 | `person_photos_test.dart` „F1” (dodanie, usunięcie i kolejność bez nazwanych kadrów → kadr Anny i łącze Jana bez zmian, Józef bez kadru) · `person_photos_draft_test.dart` „ISSUE-018 — the crop” |

Zmienione testy z planowanej zmiany: wersja schematu 5 (`database_test`, `data_state_test`, `data_state_screen_test` — wersja czytana z jej wiersza, bo jedna z liczb też wynosi 5), ISSUE-017 F3 na `currentSchemaVersion`, `profilePhotoPaths` → `profilePhotos`, „Ustaw jako profilowe” przez ekran kadru.

**Usterka znaleziona testem (→ `dev`, poprawiona):** `AnimationController` ekranu kadru był tworzony leniwie (`late final`), więc ekran zamknięty bez dotknięcia — czyli samo „Gotowe” albo samo wstecz, najczęstszy przypadek — tworzył go dopiero w `dispose()` i rzucał wyjątek. Teraz powstaje w `initState`.

### Agent checks on the emulators (release, wymyślone dane)
- **Migracja v4→v5 na `Medium_Phone`** (release na buildzie v4 z ISSUE-017, bez odinstalowania): liczby wierszy przed i po równe (5 osób · 8 zdjęć · 9 łączy · 8 plików i reszta), schemat 5; odcisk zmienił się razem z kolumnami, jak przy każdej zmianie schematu. `Grobing_Restore` też przeszedł aktualizację na v5 na swoich starych danych.
- **Przepływ:** „Popraw kadr” (Jan) i „Ustaw jako profilowe” na wspólnym zdjęciu (Anna, inny wycinek) → dwie karty, dwa różne wycinki jednego zdjęcia (AC 2 na urządzeniu); nagłówek, formularz i karta pokazują kadr; siatka ze środka.
- **F1 na urządzeniu:** po dwóch przepisaniach łączy Jana (nowe zdjęcie, zmiana profilowego) ekran kadru otworzył się na jego zapisanym wycinku z 19:06 — piksel w piksel (zrzuty 06 i 21).
- **F4 na urządzeniu (zaległe z US-005, uwaga 2):** nowa konfiguracja kopii z nowym hasłem testowym na `Medium_Phone` → kopia do Pobranych (odcisk `cbc66a72f520bea6`, 5 osób, 12 zdjęć, 13 łączy, 12 plików) → pliki przeniesione na `Grobing_Restore` → „Odtwórz z kopii” → „Zastąp dane” → **odcisk po odtworzeniu ten sam** (`cbc66a72f520bea6`, obejmuje kolumny kadru); karty grobu pokazują te same kadry co źródło.
- **R6:** kopia w tle na v5 przeszła o 19:30 (migracja 19:01). Zamówiły ją migracja albo zapisy z tej sesji — na urządzeniu nie da się ich rozdzielić; zamówienie po samej migracji pilnuje test startu.
- **F6:** wynik w *Dev report* (sygnał; emulator nie pokazuje pamięci grafiki).
- Czcionka 130 %: ekran kadru i podgląd bez ucięć (zrzuty 22, 23); przywrócona 100 %.

### ui review (subagent bez historii, ze zrzutów emulatora i kodu)
0 BLOCKER · 0 MAJOR · 6 MINOR:
1. okrąg z kadrem pokazywał przez chwilę środek, zanim przeczytał wymiary (na zdjęciu grupowym mógł mignąć ktoś inny) → **poprawione**: okrąg pusty do odczytu wymiarów;
2. obszar kadru miał dla TalkBacka „podwójne dotknięcie”, które trafiało w środek i nic nie robiło → **poprawione** (`excludeFromSemantics`); przesuwanie zdjęcia czytnikiem to **nazwana luka** w [[kadr-profilowego]] K2, przybliżenie działa przez K4;
3. plik z czytelnym nagłówkiem, którego nie da się zdekodować, dawał pusty okrąg z aktywnym „Gotowe” → **poprawione**: „błąd odczytu” (test z uciętym plikiem);
4. dotknięcie w trakcie płynnego „Powiększ” skracało krok → **poprawione** (test);
5. krycie cienia linii trójpodziału (50 %) i 6. płynny krok K4 — tylko w kodzie → **dopisane** w [[kadr-profilowego]] v1.1 i [[style-b]] reguła 14.

Zgodne według przeglądu: K1–K5 i kolejność, stany, decyzje D1–D10, role kolorów (akcent tylko pierścień i „Gotowe” na K), kontrast z `theme.dart` (pierścień akcent/tło 8,81:1, tekst pomocniczy 5,50:1, tekst 10,98:1), cele ≥ 48 dp, SC 1.4.1 (stan profilowego w podtytule), SC 2.5.1, SC 1.4.4 przy 130 %, okręgi 96/80/40 dp, na zrzutach wyłącznie wymyślone osoby.

**Obserwacje na stop #2 (nie usterki):** przy najmniejszym przybliżeniu zdjęcie 4:3 przesuwa się w bok tylko trochę, więc twarz przy krawędzi trafia na środek dopiero po „Powiększ” (D4); przy największym przybliżeniu widać piksele (128 px na ok. 950 px ekranu), a okręgi pokazują ten wycinek najwyżej ok. 2×.

### Family data
Zmiany w trzech repo: kod, testy, wygenerowany schemat, specyfikacje i pozycja — bez baz, kopii, eksportów i obrazów. Osoby w testach i danych debug wymyślone (Jan, Anna, Józef, „Wymyślony”, „Zmyślony”). Obrazy do sprawdzeń (paski, koła, rysowane postacie) leżą tylko w katalogu tymczasowym sesji i w galerii emulatorów. **Granica:** bez porównania z notatkami rodziny, bo `family_data_dir` nie był czytany.

### State left on the emulators (dla autora)
- `Medium_Phone` (release v5): kopia skonfigurowana od nowa z hasłem testowym do Pobranych emulatora (`grobing-klucz-018.age`, `grobing-kopia-018.age` — wymyślone dane); w galerii obrazy `wymyslone-duze-1…4.jpg` i `wymyslone-grupowe.jpg`; Ewa i Zofia mają wspólne zdjęcie grupowe bez kadrów — do kroków stopu #2.
- `Grobing_Restore` (release v5): dane odtworzone z tej kopii.

### Manual (stop #2) — autor i agent, emulator `Medium_Phone`, 2026-10-07
- **Autor:** krok 1 — kadr na wymyślonym zdjęciu grupowym Ewy, ekran przybliżony na twarzy (zrzut autora); bez „Gotowe”
  (ekran został otwarty). Odpowiedź: *„Jest dobrze, ale tak naprawdę nie czuję, że potrzebowałbym tych lup — cała reszta
  działa wystarczająco dobrze”* (na zrzucie przekreślone podpowiedź i lupy) oraz *„reszta działa dobrze, nie planowałem
  więcej testować”*.
- **Decyzja autora (opcja A):** bez podpowiedzi K3 i lup K4; przybliżanie jednym palcem przez **podwójne dotknięcie**
  (×2 w miejscu dotknięcia, przy 128 px powrót do całości), żeby został próg SC 2.5.1 z wytycznych. Opcja B (bez
  zastępstwa, nazwana luka) odrzucona. → [[kadr-profilowego]] v1.2 (D7'), kod i testy w tej samej paczce:
  - `crop_geometry.dart`: `doubleTapped` zamiast `zoomed`/`zoomStep`/`canZoomOut`;
  - `profile_crop_screen.dart`: bez K3 i K4, `onDoubleTap`; pojedyncze dotknięcie czeka ok. 0,3 s na drugie;
  - testy: `profile_crop_screen_test.dart` od nowa (podwójne dotknięcie 360 → 180 → 128 → całość, w miejscu dotknięcia,
    dotknięcie po nim, wstecz, błędy), `crop_geometry_test.dart` (podwójne dotknięcie, 4 kroki do 128 px, powrót przy
    krawędzi), `person_photos_screens_test.dart` (AC 1, AC 3, D9 przez podwójne dotknięcie). **`flutter test`: 429 ✅**,
    `flutter analyze` czyste, `dart format` ✅.
- **Kroki oddane agentowi** (build release v1.2, wymyślone dane): Ewa → zdjęcie grupowe → „Ustaw jako profilowe” → ekran
  bez podpowiedzi i lup, tylko „Gotowe” → podwójne dotknięcie na twarzy przybliża ×2 → „Gotowe” → „Zdjęcie profilowe”
  i „Popraw kadr” → „Zapisz”; Zofia → to samo zdjęcie → podwójne dotknięcie na **innej** twarzy → „Zapisz”: w widoku grobu
  karty Ewy i Zofii mają dwie różne twarze z jednego zdjęcia (AC 2). Krok 3 („Popraw kadr”) — sprawdzony wcześniej na
  urządzeniu (Jan, ekran otwarty na zapisanym kadrze) i testem AC 3.
- **Granica:** `adb` nie umie wysłać podwójnego dotknięcia dwoma zwykłymi `input tap` (odstęp > 0,3 s daje dwa
  pojedyncze); działa przez dwa równoległe wywołania. Odczucia podwójnego dotknięcia i opóźnienia pojedynczego (0,3 s)
  autor **nie ocenił** — zmiana weszła na jego prośbę po stopie #2.

### Verdict — APPROVED (self-check, z uwagami)
Każde AC ma test happy-path, który przechodzi; AC 1 i AC 2 widziane na urządzeniu na zdjęciu grupowym, AC 3 na
urządzeniu (Jan) i w teście; AC 4 (kopia z kadrami, odcisk zgodny) **odtworzone na drugim emulatorze**; AC 5 — migracja
v4→v5 na dwóch emulatorach, kopia v4 w v5 i kopia po migracji testami; AC 6 — przegląd `ui` (0/0/6 MINOR, poprawione).

**Czego szukano i nie znaleziono:** AC bez testu; testów pominiętych albo czerwonych; utraty kadru przy późniejszej edycji
zdjęć (F1 — test i urządzenie); różnicy odcisku po odtworzeniu; łącza z kadrem poza obrazem (kod zapisuje tylko kwadrat w
obrazie, odczyt odrzuca niepełny); prawdziwych osób w testach i danych debug; baz, kopii, eksportów i obrazów w zmianach.

**Uwagi, które nie blokują:**
1. **Odczucie podwójnego dotknięcia** i 0,3 s opóźnienia pojedynczego — nieocenione przez autora (zmiana po stopie #2).
2. **TalkBack:** czytnikiem nie da się przesunąć ani przybliżyć zdjęcia — nazwana luka w [[kadr-profilowego]] K2;
   „Gotowe” zapisuje kadr, który jest.
3. **F6 (pamięć okręgów z małym kadrem)** — tylko sygnał z emulatora, który nie pokazuje pamięci grafiki; pomiar na
   telefonie przy MVP.
4. **Prawdziwe stare zdjęcie grupowe** — czy 128 px wystarcza na twarz, pokaże przepisywanie (D5).
5. **Twarz przy krawędzi zdjęcia** trafia na środek dopiero po przybliżeniu (D4) — autor tego nie zgłosił.
6. Werdykt obowiązuje dla commita obejmującego całą paczkę niżej.

### Package list for docs
- **`grobing-code`:**
  - `README.md`;
  - `lib/data/database.dart`, `database.g.dart`, `database.steps.dart`, `photos.dart`, `graves.dart`;
  - `drift_schemas/grobing/drift_schema_v5.json`;
  - `lib/app/photo/crop_geometry.dart`, `profile_circle.dart`, `profile_crop_screen.dart` (nowe),
    `person_photo_viewer_screen.dart`, `person_photos_draft.dart`, `person_photos_screen.dart`;
  - `lib/app/grave/grave_screen.dart`, `person_form_screen.dart`;
  - `lib/dev/fictional_data.dart`;
  - `test/drift/grobing/migration_test.dart`, `test/drift/grobing/generated/schema.dart`, `schema_v5.dart` (nowy);
  - `test/data/person_photos_test.dart`, `data_state_test.dart`, `database_test.dart`;
  - `test/backup/restore_service_test.dart`;
  - `test/app/data_state_screen_test.dart`;
  - `test/app/photo/person_photos_screens_test.dart`, `person_photos_draft_test.dart`, `crop_geometry_test.dart` (nowy),
    `profile_crop_screen_test.dart` (nowy).
- **`grobing-vault`:**
  - `backlog/issues/ISSUE-018-profile-photo-crop.md`;
  - `05_DESIGN/kadr-profilowego.md` (nowy), `zdjecie.md`, `zdjecia-osoby.md`, `wpis-osoby.md`, `grob.md`,
    `brand/style-b.md`;
  - `00_START_HERE/TRACEABILITY.md`;
  - pliki zamknięcia `docs` (*For docs at closure* w planie: ADR-010, `data-model.md`, `backup-format.md`, `glossary.md`,
    ADR-009 *Follow-ups*, NFR-003, US-005 *Notes*, `CURRENT_STATE.md`).
- **`grobing-agents`:** bez zmian.
- **Poza repo (nie do commita):** makieta, zrzuty, obrazy testowe i pliki kopii w katalogu tymczasowym sesji.
