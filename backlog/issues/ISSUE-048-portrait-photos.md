---
title: "ISSUE-048 — The portrait is the place for photos: tap to change the profile photo or add photos (absorbs ISSUE-026)"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-19
verdict-reviewer: self-check
source: "`/pm` 2026-10-18 — autor przeszedł cały przepływ na emulatorze (dane demo), punkt 4 z 7; wchłania [[ISSUE-026-link-existing-photo-to-person]] (decyzja `pm`, autor: „Do twojej decyzji ile tych zadań”)"
created: 2026-10-18
updated: 2026-10-19
---

# ISSUE-048 — Portret jako miejsce na zdjęcia

> Autor: *„gdy klikam na kogoś „zdjęcie profilowe”, chciałbym od razu widzieć tam możliwość jego zmiany (lub dodania dla tej osoby nowych zdjęć —
> podobnie jak działa zdjęcie w tle)”*.

## What to build
- **Dotknięcie portretu** w widoku osoby ([[osoba]] el. 3) — dziś podgląd w trybie oglądania, a profilowe zmienia się pod ✎ — prowadzi od razu do:
  obejrzyj · zmień profilowe · dodaj zdjęcia. Wzór: tło ([[osoba]] D21 — dotknięcie → wybór, zapis od razu, jak zdjęcie nagrobka w [[grob]]).
- **Okrąg z inicjałami** (osoba bez zdjęć) — dziś bez akcji ([[osoba]] D20) — prowadzi do dodania zdjęcia; pierwsze zdjęcie jest profilowym
  ([[ADR-009-person-photos-record-and-link]]). *Obali* D20 („autor szuka dodania zdjęcia w okręgu portretu”) — trafione.
- **Z [[ISSUE-026-link-existing-photo-to-person]]:** trzecie źródło „Ze zdjęć w aplikacji” (zdjęcie, które już jest u innej osoby, np. grupowe) i
  wybór spośród zdjęć wszystkich osób — szczegóły w ISSUE-026 → *What to build*.
- Projekt: `ui` przed `planning` — zmiana [[osoba]], [[zdjecia-osoby]], [[zdjecie]], [[kadr-profilowego]].

## Acceptance Criteria
- **AC-1** *Given* Jan Wymyślony z profilowym *When* dotykam portretu *Then* od razu widzę, że mogę obejrzeć zdjęcie, zmienić profilowe albo dodać
  zdjęcia — bez ✎.
- **AC-2** *Given* nowe profilowe wybrane z portretu *Then* zapisuje się od razu, jak tło (D21), a widok pokazuje je bez wracania.
- **AC-3** *Given* Maria Zmyślona bez zdjęć *When* dotykam okręgu z inicjałami i dodaję zdjęcie *Then* jest ono jej profilowym.
- **AC-4** (ISSUE-026 AC-1) *Given* zdjęcie grupowe u Marii *When* u Jana wybieram „Ze zdjęć w aplikacji” i to zdjęcie *Then* jest ono u Jana i u
  Marii, a plik jest jeden.
- **AC-5** (ISSUE-026 AC-2) *Given* kilkaset zdjęć w aplikacji *Then* zdjęcie konkretnej osoby da się znaleźć bez przewijania wszystkiego.

## Notes
- **Rozmiar:** AC-4 i AC-5 wnoszą nowy ekran wyboru zdjęć. Gdy przy terminie instalacji (2026-10-29) zabraknie na nie czasu, `planning` pyta autora
  na stopie #1, czy zostają; jeśli wypadną — ISSUE-026 wraca do `ready` (nie giną).
- Bez zmiany schematu (łącze osoba–zdjęcie istnieje od v4, profilowe i kadr — [[kadr-profilowego]]) — do potwierdzenia przez `planning`.
- Z tego samego przeglądu autora: [[ISSUE-047-grave-first-then-people]] · [[ISSUE-049-tree-levels-and-zoom]] · [[ISSUE-050-next-event]].

## Implementation plan
> `planning`, 2026-10-19. **Pozycja z ekranem: zmiana istniejących i jeden nowy.** Specyfikacje — propozycja `ui` na stop #1: [[osoba]] **v2.9**
> (portret → „Zdjęcie profilowe”, okrąg z inicjałami z plakietką, D23–D25, **⚠️ OPEN 7: P2 albo P1**), [[zdjecia-osoby]] **v1.5** (tryb „Zdjęcie
> profilowe” P1–P6, D7), [[zdjecie]] **v1.7** (A4 „Ze zdjęć w aplikacji”, A z widoku zapisuje od razu, D10), [[kadr-profilowego]] **v1.3** (wejście z
> „Zdjęcia profilowego”), **nowy** [[zdjecia-w-aplikacji]] **v1** (AC-4, AC-5, D1–D8), [[style-b]] **v1.43** (wyjątek „wybór zdjęć w widoku”, bez nowych
> tokenów). **Makieta (klikalna, przełącznik P2 / P1 u góry, osoby Jan i Zofia):**
> `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/92e37203-2f58-4915-b7d9-04fe69e7e014/scratchpad/makieta-048.html`.
> Bez US (task-level, pod [[US-005-zdjecia]]); UJ-001 krok 5 (widok osoby, M5) i M1 (zbieranie zdjęć u babci).

> **Stop #1 — 2026-10-19, autor: *„tak”*** na pytanie „Budujemy wariant P2 w pełnym zakresie (AC-1–AC-5)?”. Przyjęte: **P2** ([[osoba]] *Open* 7
> zamknięte), AC-4 i AC-5 zostają w tej pozycji, decyzje projektowe z listy niżej (D24, D25, plakietka, A4 tylko tam, gdzie jest co wybrać, i bez „Zdjęcia
> w tle”). Specyfikacje przestają być propozycją.

### Scope — diff
**Dane — bez zmiany schematu (v15).** Sprawdzone w kodzie: `applyPersonPhotoEdits` przepisuje łącza osoby z listy `PhotoRef`, a `SavedPhoto` zdjęcia
innej osoby daje nowe łącze tej osoby; łącza innych osób, plik i wiersz `media` się nie zmieniają. Zapis od razu już działa przy tle
(`_chooseBackground` → `Photos.writeWithPersonPhotos`).
1. `lib/data/photos.dart` — **`allPersonPhotoLinks(db)`**: jedno zapytanie `person_media` ⋈ `media`, dla każdej osoby jej zdjęcia w kolejności łączy
   (`PersonPhoto`). Dla ekranu „Zdjęcia w aplikacji”; dziś łącza czyta się tylko po jednej osobie.
2. `lib/app/photo/person_photos_draft.dart` — **`addSaved(mediaId, relativePath)`**: dołącza zapisane zdjęcie innej osoby na końcu (bez duplikatu);
   `hasChanges` i `edits()` działają bez zmian (kolejność różni się od zapisanej). Po zapisie od razu szkic **wczytuje się od nowa** (`load`), żeby
   ekran, który zostaje otwarty, pracował na zapisanym stanie (nowe zdjęcia mają już swoje `mediaId`).

**Zapis od razu — jedna funkcja:**
3. Z `_chooseBackground` (`lib/app/person/person_screen.dart`) wydzielić **wspólny zapis zdjęć osoby od razu** (szkic → `edits()` →
   `writeWithPersonPhotos` w transakcji). Wołają go: wybór tła (jak dziś), wybór profilowego, dodanie zdjęć z widoku. Błąd → wyjątek dla wołającego (ten pokazuje komunikat).

**Ekrany:**
4. `lib/app/person/person_screen.dart` ([[osoba]] v2.9):
   - **portret ze zdjęciem** → „Zdjęcie profilowe” (`PersonPhotosScreen` w trybie profilowego); opis „Zdjęcie profilowe”, podpowiedź „zmień albo obejrzyj”;
   - **okrąg z inicjałami** → plakietka 32 dp (okrąg w kolorze tła, obrys 1 dp, `Glyphs.addPhotoAlternate` 20 dp w akcencie, pod 45°, nad wieńcem),
     cały okrąg jednym celem, `tooltip` „Dodaj zdjęcie”, opis „Zdjęcie profilowe: brak — dodaj zdjęcie”; dotknięcie → arkusz źródła → zapis od razu
     (pierwsze zdjęcie = profilowe);
   - **„Dodaj zdjęcie” w pustej sekcji 10** → to samo co okrąg, zamiast `_correct(pickPhotos: true)` (D24). `pickPhotosAtStart` w `openPersonEntry`
     usunąć, jeśli nikt go już nie woła;
   - **D25:** portret, okrąg, „Dodaj zdjęcie” i pasmo tła zaczynają od `PersonFormScreen.isCorrecting(personId)` → wtedy `_correct()` (wraca do poprawy w
     stosie, jak ✎);
   - błąd zapisu → komunikat u dołu „Nie udało się zapisać zdjęć. Spróbuj jeszcze raz.”.
5. `lib/app/photo/person_photos_screen.dart` — **tryb „Zdjęcie profilowe”** ([[zdjecia-osoby]] P1–P6) obok `chooseBackground`: pasek; okrąg 96 dp i
   **„Obejrzyj zdjęcie”** → `PersonPhotoViewerScreen(readOnly: true, initialIndex: 0)`; linia „Dotknij zdjęcia, które ma być profilowym.”; siatka z ramką na
   pierwszym; dotknięcie → `ProfileCropScreen(initial: draft.cropOf(photo))` → „Gotowe” → `setProfile(photo, crop)` → zapis od razu → `pop` do widoku;
   błąd → linia błędu pod siatką, ekran zostaje. Kafelek **„Dodaj zdjęcia”** → `addPersonPhotos` → zapis od razu → szkic od nowa, ekran zostaje.
   Wszystkie elementy rosną z tekstem jak tryb tła.
6. `lib/app/photo/photo_source_sheet.dart` — **A4 „Ze zdjęć w aplikacji”** ([[zdjecie]] v1.7): opcjonalny wiersz z `Glyphs.group` i drugą linią; arkusz
   zwraca osobną wartość (nie nową wartość `PhotoSource` — ta trafia do systemowego wybieracza). Wiersz tylko na prośbę wołającego.
7. `addPersonPhotos` (`person_photos_screen.dart`, wspólne dla formularza 1a, kafelka w bazie, kafelka „Zdjęcia profilowego”, okręgu i sekcji 10) —
   pokazuje A4, gdy jest choć jedno zdjęcie innej osoby, którego szkic nie ma; A4 → nowy ekran (8) → `addSaved` dla każdego wybranego, w kolejności
   zaznaczania. **Bez A4 w „Zdjęciu w tle”** (`_addBackground` ma własne wywołanie arkusza — [[zdjecia-w-aplikacji]] D7).
8. **Nowy plik** `lib/app/photo/app_photos_screen.dart` — „Zdjęcia w aplikacji” ([[zdjecia-w-aplikacji]] 1–7): pole szukania przypięte (`matchesQuery`
   jak w „Kto jest na zdjęciu?”); grupy osób z `allPersonPhotoLinks`, bez tej osoby i bez zdjęć, które szkic już ma; „Najbliżsi” (rodzice, partnerzy i
   dzieci z mini-drzewa i osoby z jej grobu), potem „Inne osoby” (`polishCompare`); wiersz osoby (okrąg 40 dp z profilowym w kadrze, imię z „z d.”, lata ·
   liczba z odmianą); siatka 3 kolumn, leniwa (`CustomScrollView` z gridami), miniatury w rozmiarze komórki; zaznaczenie należy do zdjęcia — ramka we
   wszystkich grupach; plik bez odczytu — komórka nieaktywna; „Dodaj” nieaktywny → „Dodaj 2 zdjęcia” → `pop` listy zdjęć. Bez dolnego paska.
   **Wariant tańszy** (gdy zabraknie czasu w `dev`): bez sekcji „Najbliżsi”, wszystko alfabetycznie ([[zdjecia-w-aplikacji]] D4) — zgłosić w *Dev report*.

### AC → test happy-path (`qa`)
| AC | Test |
|---|---|
| AC-1 | ekran: widok Jana Wymyślonego z trzema zdjęciami → portret → „Zdjęcie profilowe”: „Obejrzyj zdjęcie”, „Dotknij zdjęcia, które ma być profilowym.”, siatka z ramką na pierwszym, kafelek „Dodaj zdjęcia”; „Obejrzyj zdjęcie” → podgląd bez działań (B4'') |
| AC-2 | ekran: portret → drugie zdjęcie → kadr → „Gotowe” → widok Jana; dane: pierwsze łącze to to zdjęcie z kadrem, bez „Zapisz”; widok pokazuje nowe profilowe (strumień widoku) |
| AC-3 | ekran: Maria Zmyślona bez zdjęć → okrąg z inicjałami (opis „Zdjęcie profilowe: brak”) → „Wybierz z galerii” (wybieracz testowy) → widok z portretem; dane: jedno łącze, pozycja 0. To samo z „Dodaj zdjęcie” w sekcji 10 |
| AC-4 | dane: zdjęcie grupowe Marii; szkic Jana `addSaved` → zapis → Jan ma łącze na końcu, łącze Marii bez zmian, liczba wierszy `media` i plików bez zmian. Ekran: portret Jana → „Dodaj zdjęcia” → „Ze zdjęć w aplikacji” → grupa Marii → zdjęcie → „Dodaj 1 zdjęcie” → zdjęcie w siatce „Zdjęcia profilowego” |
| AC-5 | ekran: ok. 300 zdjęć u ok. 60 wymyślonych osób (rdzenie Wymyśl-, Zmyśl-, Testow-, Przykład-) → „zmysl” w polu → tylko pasujące grupy; zaznaczenie zostaje po zmianie filtra; przycisk liczy zdjęcia, nie ramki (zdjęcie grupowe w dwóch grupach = 1) |

Dodatkowo (decyzje projektowe): **D25** — poprawa Jana w stosie → portret i pasmo wracają do niej, bez zapisu; **A4** — ukryty bez zdjęć innych osób i
w „Zdjęciu w tle”; **kopia** — zdjęcie dołączone z aplikacji i nowe profilowe z kadrem → kopia → odtworzenie → te same łącza, kolejność i kadr, jeden
plik (jak `backup_archive_test.dart`). **Bez testu migracji** — schemat się nie zmienia. Testy, które zakładają „portret → podgląd” i „Dodaj zdjęcie → poprawa”
(`person_screen_test.dart` i pokrewne), przechodzą na nowy przepływ. Rytuał WZ-024: `dart format` → `flutter analyze` → `flutter test --timeout 120s`.

### Manual checks (stop #2)
**Agent na emulatorze — przed stopem, ze zrzutami.** `Grobing_Restore` ma dziś **demo**: najpierw zapisać obecny stan i wgrać stan sprzed demo z
`C:\Programowanie\Grobing\_pokaz` (README tam), **nigdy `pm clear` bez zapisanego tar**; po pozycji — demo z powrotem (jak w ISSUE-047).
1. Osoba ze zdjęciami → portret → „Zdjęcie profilowe” → „Obejrzyj zdjęcie” (podgląd bez działań) → wstecz → inne zdjęcie → kadr → „Gotowe” → widok z nowym
   portretem; zamknięcie aplikacji i powrót — to samo profilowe.
2. Osoba bez zdjęć → plakietka na okręgu → arkusz (z A4, gdy inni mają zdjęcia) → galeria → widok z portretem; „Dodaj zdjęcie” w sekcji 10 — to samo.
3. „Ze zdjęć w aplikacji” → szukanie po kilku literach → zdjęcie grupowe zaznaczone w dwóch grupach → „Dodaj 1 zdjęcie”; w bazie (`run-as` na buildzie
   profile) jeden wiersz `media`, łącze u obu osób.
4. D25: poprawa osoby A → chip partnera → jego mini-drzewo → A → portret → powrót do poprawy A.
5. Tekst 200% na 360 dp: „Zdjęcie profilowe”, „Zdjęcia w aplikacji” (wiersz osoby, przycisk), plakietka; TalkBack — opisy portretu, okręgu i komórek.
6. Kopia w tle po zapisach i próbne odtworzenie na drugim emulatorze (jeden emulator naraz) — profilowe, kadr i dołączone zdjęcie są po odtworzeniu.

**Autor: odczucie — najwyżej 3 kroki** (emulator):
1. Portret → zmień profilowe na inne zdjęcie: czy tak to sobie wyobrażałeś? (*Obali* [[osoba]] D23)
2. Osoba bez zdjęć: czy plakietka na okręgu mówi, że tu dodasz zdjęcie? Dodaj jedno.
3. „Ze zdjęć w aplikacji”: znajdź zdjęcie grupowe innej osoby i dodaj — czy szukanie po osobie wystarcza? (*Obali* [[zdjecia-w-aplikacji]] D1, D6)

### Out of Scope
- usuwanie zdjęć i „Kto jest na zdjęciu?” z widoku — zostają pod ✎ ([[osoba]] D24); „Cofnij” po dodaniu (D24 *Obali*);
- „Zdjęcia · N” w widoku dalej tylko do oglądania (W2);
- A4 w „Zdjęciu w tle” ([[zdjecia-w-aplikacji]] D7); podgląd na pełnym ekranie z „Zdjęć w aplikacji” (D6);
- opis i data zdjęcia, porządkowanie zdjęć ([[zdjecia-osoby]] D3);
- okręgi profilowego poza widokiem osoby (karta grobu, drzewo, Osoby) — bez zmian.

### Decision for stop #1 (author) — jedno pytanie
**Budujemy wariant P2 w pełnym zakresie (AC-1–AC-5)?** „tak” = P2 + nowy ekran „Zdjęcia w aplikacji” + decyzje niżej. Inna odpowiedź: **„P1”** (arkusz z
czterema działaniami zamiast ekranu) albo **„bez zdjęć z aplikacji”** (AC-4 i AC-5 wracają do [[ISSUE-026-link-existing-photo-to-person]]).
Decyzje projektowe, które przechodzą na „tak” (widać je na makiecie):
- zmiany zdjęć z widoku zapisują się od razu, także „Dodaj zdjęcie” w pustej sekcji „Zdjęcia” (dziś przez formularz i „Zapisz”) — D24;
- gdy poprawa tej osoby jest otwarta niżej, portret i pasmo tła wracają do niej — ochrona przed nadpisaniem zdjęć, także przy tle — D25;
- okrąg z inicjałami dostaje plakietkę z ikoną, bo stał się przyciskiem;
- „Ze zdjęć w aplikacji” tylko tam, gdzie jest co wybrać, i nie w „Zdjęciu w tle”; najpierw „Najbliżsi”; zdjęć, które osoba już ma, nie ma na liście.

Koszt i zysk: zmiana profilowego 8 → 3 dotknięcia; zdjęcie innej osoby 8+ → 5. Termin: pozycja to ok. dnia pracy; kolejka (ISSUE-049, ISSUE-050, ISSUE-032)
mieści się do 2026-10-29 także z AC-4 i AC-5.

## Dev report
> `dev`, 2026-10-19. Flutter 3.41.1 (przypięty). `dart format` i `flutter analyze lib` — czyste. **Bez zmiany schematu** (v15). Pełny wariant
> (z sekcją „Najbliżsi”), nie tańszy.

### Changed
- `lib/data/photos.dart` — `allPersonPhotos(db)`: zdjęcia wszystkich osób jednym zapytaniem (osoba → zdjęcia w kolejności łączy).
- `lib/app/photo/person_photos_draft.dart` — `savedMediaIds`, `addSaved(mediaId, file)` (zdjęcie innej osoby na końcu, bez duplikatu), `reload()` (po zapisie od
  razu: zmiany szkicu wyczyszczone, przygotowane pliki, które nie przeszły do magazynu, usunięte, szkic wczytany od nowa).
- `lib/app/photo/photo_source_sheet.dart` — wspólny arkusz; `showPersonPhotoSourceSheet(fromApp:)` z A4 „Ze zdjęć w aplikacji” (`Glyphs.group`, druga linia)
  i osobnym wynikiem `PersonPhotoSource` (gallery · camera · app); `showPhotoSourceSheet` dla grobu, cmentarza i tła bez zmian w wyglądzie.
- `lib/app/photo/person_photos_screen.dart`:
  - `addPersonPhotos(context, draft, personName:, firstName:)` — A4 tylko, gdy `hasAppPhotos` (jedno zapytanie przed arkuszem); po A4 → `loadAppPhotos` →
    ekran „Zdjęcia w aplikacji” → `addSaved`;
  - `savePersonPhotosNow(draft)` — wspólny zapis od razu (wydzielony z wyboru tła);
  - tryb **`chooseProfile`** (P1–P6): okrąg 96 dp + „Obejrzyj zdjęcie” (podgląd tylko do oglądania), linia, siatka z ramką na pierwszym, zdjęcie → kadr →
    „Gotowe” → zapis od razu → powrót do widoku; kafelek „Dodaj zdjęcia” → zapis od razu, ekran zostaje; błąd zapisu → szkic wraca do zapisanego stanu i
    linia „Nie udało się zapisać zdjęć. Spróbuj jeszcze raz.”; w trakcie zapisu siatka i kafelek czekają.
- **Nowe pliki:** `lib/app/photo/app_photos_screen.dart` („Zdjęcia w aplikacji”: `hasAppPhotos`, `loadAppPhotos`, `AppPhotosScreen` — pole przypięte, grupy
  „Najbliżsi” / „Inne osoby”, `SliverGrid` leniwie, zaznaczenie należy do zdjęcia, plik bez odczytu nieaktywny, „Dodaj N zdjęć” z odmianą) ·
  `lib/app/photo/photo_cell.dart` (`PhotoCell`, `UnreadableCell` — wydzielone z bazy zdjęć, wspólne dla obu siatek).
- `lib/app/person/person_screen.dart` — portret → `_chooseProfile` (opis „Zdjęcie profilowe”, podpowiedź „zmień albo obejrzyj”); okrąg z inicjałami →
  przycisk z plakietką `_AddBadge` (32 dp, 45°, `tooltip` „Dodaj zdjęcie”, opis „Zdjęcie profilowe: brak”, podpowiedź „dodaj zdjęcie”) → `_addPhotosNow`; „Dodaj
  zdjęcie” w sekcji 10 → `_addPhotosNow`; **D25** — `_toOpenCorrection()` na początku tła, portretu, okręgu i „Dodaj zdjęcie”; „Zdjęcia · N” → baza do oglądania
  jak dotąd.
- `lib/app/grave/person_form_screen.dart` — `pickPhotosAtStart` usunięte (nikt go już nie woła — D24); formularz podaje imię do „Zdjęć w aplikacji”.
- `lib/app/polish.dart` — `firstGivenName` („Jan” z „Jan Józef”).

### Deviations
1. **Arkusz zwraca osobny typ `PersonPhotoSource`** zamiast nowej wartości `PhotoSource` — `PhotoSource` idzie do systemowego wybieracza (plan krok 6 tak
   zakładał; zapisuję, bo zmienia API).
2. **Po nieudanym zapisie w „Zdjęciu profilowym” szkic wraca do zapisanego stanu** — także zdjęcia dodane w tej próbie trzeba dodać jeszcze raz. Specyfikacja
   mówi „stare profilowe”; dla dodanych zdjęć nie mówi nic — tak jest prościej i nic nie wisi niezapisane.
3. **Plik bez odczytu w „Zdjęciach w aplikacji”** rozpoznaje sprawdzenie istnienia pliku przy wczytaniu ekranu. Plik, który istnieje, ale się nie dekoduje,
   pokazuje ikonę uszkodzenia, a da się go zaznaczyć (rzadki przypadek; łącze i tak wskaże ten sam plik).
4. **Węzeł semantyki okręgu w P2** ma `container: true` — bez tego zrzut drzewa pokazał etykietę na całym nagłówku, także nad „Obejrzyj zdjęcie”.
   Poprawione po przejściu (build na emulatorze jest sprzed tej poprawki).

### AC walk on the emulator
`Grobing_Restore`, build profile (`--split-per-abi`, `FRAME_LOG`) na stanie **sprzed demo** z `_pokaz` (podmiana jak w ISSUE-047; demo zapisane wcześniej — niżej).
Zrzuty: `%TEMP%\claude\c--Programowanie-Grobing-grobing-agents\92e37203-…\scratchpad\emu048\shots\` (`01`–`17`), zdjęcia testowe — wymyślone rysunki
(`fotki048\`, w galerii emulatora w `Pictures/Grobing048`).
- **AC-1** ✅ portret Mateusza → „Zdjęcie profilowe”: okrąg, „Obejrzyj zdjęcie”, linia, siatka z ramką, kafelek „Dodaj zdjęcia” (`02`).
- **Dodanie z kafelka** ✅ galeria → 2 zdjęcia → „Done” → siatka z 3 zdjęciami, ekran został (`05`).
- **AC-2** ✅ zdjęcie 2 → kadr → „Gotowe” → widok z nowym portretem od razu (`06`, `07`); w kopii bazy: pierwsze łącze to to zdjęcie z kadrem, tło bez zmian.
- **AC-3 + AC-4** ✅ Zofia (bez zdjęć) — plakietka na okręgu nad wieńcem (`08`) → arkusz z A4 → „Zdjęcia w aplikacji”: „Najbliżsi” (matka, ojciec), „Inne osoby”
  (`09`) → zdjęcie grupowe ojca → ramka, „Dodaj 1 zdjęcie” (`10`) → widok Zofii z portretem (`11`); w kopii bazy: jeden wiersz `media`, łącze u dwóch osób, u
  Zofii pozycja 0. Kopia bazy usunięta po liczeniu (liczby, bez nazw).
- **AC-5** ✅ (na małej liczbie zdjęć) „przyk” → zostaje osoba z pasującym nazwiskiem rodowym i jedna z „Innych osób”, zaznaczenie zostaje (`17`).
- **D25** ✅ poprawa Zofii → chip ojca → jego mini-drzewo → Zofia → portret → powrót do „Poprawa wpisu” Zofii (`12`).
- **Tekst 200% na 360 dp** ✅ widok z plakietką (`13`), „Zdjęcie profilowe” (`14`), arkusz (`15`), „Zdjęcia w aplikacji” — pole przypięte, wiersz osoby zawija się,
  przycisk cały (`16`); potem tekst i gęstość z powrotem.
- **Semantyka** ✅ portret „Zdjęcie profilowe, zmień albo obejrzyj”; okrąg „Zdjęcie profilowe: brak, dodaj zdjęcie”; komórki „…, zaznaczone — odznacz”; kafelek
  „Dodaj zdjęcia osoby” — wszystkie `clickable` z granicami elementu (poza nagłówkiem P2 — odstępstwo 4).
- **Nie sprawdzone:** czas klatki przy kilkuset zdjęciach (na emulatorze jest ich kilkanaście; siatka buduje się leniwie, a 300 zdjęć ma pokryć test `qa`);
  TalkBack na żywo; kopia w tle i odtworzenie — przy `qa`.

**Emulator po przejściu:** zawiesił się raz (host bez pamięci po buildzie — demony Gradle zatrzymane, emulator uruchomiony od nowa, dane nietknięte).
`Grobing_Restore` ma teraz build ISSUE-048 na stanie sprzed demo + zmiany z przejścia (Mateusz: 2 nowe zdjęcia i nowe profilowe; Zofia: zdjęcie ojca).
**Demo z Twoimi zmianami z 2026-10-18** jest zapisane w `…\scratchpad\emu048\stan-przed-048.tar` + `stan-przed-048-base.apk` — wraca na emulator po `qa`.

### Tests (for `qa`)
`flutter test --timeout 120s` przed poprawką semantyki: **945 zielonych, 1 czerwony** — `person_screen_test.dart`: „D20 — without photos … „Dodaj zdjęcie” → the
correction with the sheet …” zakłada starą drogę przez formularz i „Zapisz”; po D24 „Dodaj zdjęcie” zapisuje od razu — test do przepisania przez `qa`.

### Manual checks for `qa`
Plan → *Manual checks* bez zmian; do dopisania: odstępstwo 4 (granice węzła okręgu w P2 po nowym buildzie) i 300 zdjęć w „Zdjęciach w aplikacji” (test widżetu). Gdyby
potrzebny był pomiar klatek: ekran jest nowy, więc nie ma buildu odniesienia z tym samym ekranem — porównaniem jest przewijanie bazy zdjęć osoby w tym samym
buildzie (`stan-przed-048-base.apk` to build demo, nie odniesienie).

## Verification
> `qa`, 2026-10-19. Rytuał WZ-024: `dart format` ✅ · `flutter analyze` (lib + test) ✅ · `flutter test --timeout 120s` — **956 zielonych** (było 946; +10 nowych, 1
> przepisany). Bez zmiany schematu — **bez testu migracji**; próbne odtworzenie z kopii — test niżej.

### Tests per AC (happy path)
| AC | Test |
|---|---|
| AC-1 | `person_screen_test.dart` „ISSUE-048 AC-1, AC-2” — portret → „Zdjęcie profilowe”: „Obejrzyj zdjęcie”, linia, siatka z ramką i `selected`, „Dodaj zdjęcia”, bez „Zapisz”; „Obejrzyj zdjęcie” → podgląd bez działań |
| AC-2 | ten sam test — zdjęcie 2 → kadr → „Gotowe” → widok; w bazie pierwsze łącze to to zdjęcie z kadrem, tło bez zmian · `person_photos_draft_test.dart` „ISSUE-048 AC-2” — `setProfile` z kadrem + `savePersonPhotosNow`, dodane zdjęcie zapisane razem, bez zmian — nic nie zapisane |
| AC-3 | `person_screen_test.dart` „ISSUE-048 AC-3, D24” — okrąg z plakietką („Zdjęcie profilowe: brak”, `tooltip`) → arkusz bez formularza, bez A4 (brak zdjęć w aplikacji) → galeria → portret i „Zdjęcia · 1” od razu; „Dodaj zdjęcie” u Jana — to samo, z A4 i aparatem (zastępuje dawny test D20 przez „Zapisz”) |
| AC-4 | `person_screen_test.dart` „ISSUE-048 AC-4” — Jan: okrąg → A4 → „Najbliżsi” z Marią → zaznaczenie → „Dodaj 1 zdjęcie” → portret; zdjęcie u Jana i u Marii, jeden wiersz `media` · `person_photos_draft_test.dart` „ISSUE-048 AC-4” — `addSaved` bez duplikatu, jeden plik, łącza Anny bez zmian, `allPersonPhotos` |
| AC-5 | `app_photos_screen_test.dart` (nowy) — 300 zdjęć u 60 wymyślonych osób: siatka leniwa (< 60 obrazów zbudowanych), „zmysl” zostawia grupy „Zmyśl-”, zdjęcie grupowe w ramce w obu grupach i liczone raz, zaznaczenie zostaje po filtrze, „Dodaj 2 zdjęcia” oddaje zdjęcia w kolejności zaznaczania; plik bez odczytu nieaktywny; „Dodaj” nieaktywny bez zaznaczenia; wstecz nic nie oddaje; pusty wynik |

**Dodatkowo:** **D25** (`person_screen_test.dart` „ISSUE-048 D25”) — portret Marii przy otwartej jej poprawie wraca do formularza; „Zdjęcie w tle” bez A4 ·
**przegląd `ui` MAJOR** („ISSUE-048, ui review MAJOR”) — w trakcie przygotowania okrąg ze wskaźnikiem, nieaktywny, „Dodaj zdjęcie” nieaktywne, drugie
dotknięcie nie otwiera arkusza, po zapisie oba zdjęcia · **kopia** (`backup_archive_test.dart` „ISSUE-048”) — zdjęcie dołączone z aplikacji i profilowe z
kadrem, zapisane od razu → kopia → odtworzona baza: ten sam odcisk, łącza, kolejność i kadr; zdjęcie wspólne w archiwum raz · **dostępność dotyku**
(`meetsGuideline(androidTapTargetGuideline)`, `labeledTapTargetGuideline`, `expectEveryButtonTappable`) na „Zdjęciu profilowym” i „Zdjęciach w aplikacji”.

### Family data
Zmiany w `grobing-code`: kod i testy — nazwiska tylko z rdzeni Wymyśl-, Zmyśl-, Testow-, Przykład-; bez baz, kopii, eksportów i plików zdjęć (obrazy w testach
rysowane w kodzie). Zrzuty i wymyślone „zdjęcia” (`fotki048\`) — tylko w katalogu tymczasowym sesji. **Na emulatorze jest wpis autora** (osoba spoza
wymyślonych rdzeni, z dwoma zdjęciami) — widoczny na zrzutach 09–10 dev; nie trafia nigdzie poza katalog tymczasowy.

### ui review (subagent, 2026-10-19)
0 BLOCKER · **1 MAJOR · 5 MINOR**:
1. **MAJOR — brak stanu „w toku” i ryzyko utraty zdjęć** (drugi szkic w trakcie przygotowania zapisuje całą listę i zdejmuje zdjęcia pierwszego; w „Zdjęciu
   profilowym” komórki nie czekały na przygotowanie) → **poprawione** (`dev` w tym przejściu): `_busy`/`_working` w widoku — wskaźnik w okręgu, wejścia
   nieaktywne także dla czytnika; komórki czekają na przygotowanie; [[osoba]] *States* „dodawanie w toku”, [[zdjecia-osoby]] *States*; test regresji.
2. MINOR — twarde spacje: „Ze zdjęć w aplikacji”, „u innych osób”, „Zdjęcia w aplikacji” → **poprawione** (` `; zrzut `19` przy 200%: „u innych osób” razem).
3. MINOR — „·” w linii wiersza osoby → **poprawione** (`· `).
4. MINOR — nagłówki sekcji i wiersze osób bez roli nagłówka dla czytnika → **poprawione** (`header: true` w `PeopleSectionHeader` — wspólny z „Kto jest na
   zdjęciu?” — i w wierszu osoby).
5. MINOR — stan „zapis — błąd” w specyfikacji ≠ kod → **specyfikacja według kodu** ([[zdjecia-w-aplikacji]] v1.2, D10; odstępstwo 5).
6. MINOR — „z d.” odrywa się od nazwiska rodowego przy 200% → **poza zakresem**: `personName` bez twardej spacji to znana luka z [[style-b]] reguła 6
   ([[CURRENT_STATE]] → *Poza tą kolejnością*, „twarde spacje … i w „z d.””).

Przyjęte odstępstwa `dev`: 2 → [[zdjecia-osoby]] v1.6 (D8), 3 → [[zdjecia-w-aplikacji]] v1.1 (D9); 4 — wykonanie P2, bez zapisu. Po poprawkach na emulatorze:
granice węzła okręgu w P2 = sam okrąg (96 dp), plakietka przy 200% (`18`), arkusz przy 200% (`19`). Uwaga do *Dev report*: zrzut `13` pokazuje Zofię już z
portretem — plakietkę przy 200% pokazuje `18`.

### Stop #2 — 2026-10-19, autor: *„ok”*
Sprawdzone na urządzeniu (kopia bazy z emulatora, same liczby, usunięta po liczeniu):
1. **Zmiana profilowego z portretu** — ✅ **ok ze śladem**: pierwsze łącze Mateusza to inne zdjęcie niż przed krokiem, z kadrem.
2. **Plakietka na okręgu z inicjałami, dodanie z galerii** — ✅ **ok ze śladem**: Ignacy ma nowe zdjęcie (nowy wiersz `media`), jest jego profilowym. Pytanie
   o dwie te same ikony (pasmo tła i plakietka) — bez uwag.
3. **„Ze zdjęć w aplikacji”, szukanie po osobie** — **„ok” bez śladu na urządzeniu** (żadne nowe łącze do zdjęcia innej osoby) → zapisane jak **„pomiń”**.
   AC-4 i AC-5 pokrywają testy i przejście `dev` na emulatorze (zrzuty `09`–`11`, `17`).

### For ISSUE-032 → Hand checks
- **A** — odtworzenie kopii na telefonie ze zdjęciem dołączonym z „Zdjęć w aplikacji” (jedno zdjęcie u dwóch osób) i profilowym z kadrem ustawionym z portretu (w
  testach — `backup_archive_test.dart` „ISSUE-048”; na urządzeniu nie sprawdzone).
- **B** — „Zdjęcia w aplikacji”: czy szukanie po osobie wystarcza przy prawdziwych zdjęciach (krok 3 stopu #2 — „ok” bez śladu, zapisane jak „pomiń”).
- **B** — TalkBack na żywo: portret i okrąg z inicjałami (stan „zapisuję zdjęcia”), „Zdjęcie profilowe”, „Zdjęcia w aplikacji” z nagłówkami osób — nieprzetestowane na żywo.
- **B** — płynność przewijania „Zdjęć w aplikacji” przy kilkuset zdjęciach na telefonie — nieprzetestowane (siatka leniwa, test widżetu z 300 zdjęciami).

### Verdict
**APPROVED** (self-check, 2026-10-19, z uwagami): każde AC z testem happy-path i przejściem na emulatorze; przegląd `ui` — 1 MAJOR (ryzyko utraty zdjęć przy
drugim dotknięciu w trakcie zapisu) i 4 MINOR poprawione przed stopem, 1 MINOR poza zakresem (znana luka „z d.”); bez zmiany bazy; odtworzenie z kopii w
teście. Uwagi: krok 3 stopu #2 bez śladu; czasu klatki przy kilkuset zdjęciach nie mierzono na urządzeniu; okrąg 96 dp w P2 przeszedł poprawkę semantyki po
przejściu `dev` (sprawdzona na emulatorze po nowym buildzie). Szukałem i nie znalazłem: danych rodziny w zmianach, przycisku bez akcji dotknięcia, celu < 48 dp,
koloru jako jedynego nośnika zaznaczenia, literalnych twardych spacji w źródle.
