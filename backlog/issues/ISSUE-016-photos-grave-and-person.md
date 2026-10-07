---
title: "ISSUE-016 — Gravestone photo and the photo foundation: one photo per grave (add, change, delete), full-screen view, 2048 px JPEG, backup consistency"
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
source: "rozpisanie US-005 (decyzja autora 2026-10-07 w `pm`) · stop #1, rundy 1–2 (decyzje autora 2026-10-07: jedno zdjęcie nagrobka, zdjęcia osób → ISSUE-017, 2048 px JPEG 85, D3–D5) · US-005 AC-1..3 i *Notes* · ISSUE-012 → *Input from the author* 2–3 · 05_DESIGN: zdjecie.md v1.1, grob.md v3, cmentarz.md v3"
created: 2026-10-07
updated: 2026-10-07
---

# ISSUE-016 — Zdjęcie nagrobka i fundament zdjęć

> Z rozpisania [[US-005-zdjecia]] (decyzja autora 2026-10-07, po `pm`). Najpierw jedna pozycja na zdjęcia grobu i
> osoby; **na stopie #1 autor rozdzielił je** (rundy 1–2 niżej): ta pozycja robi **jedno zdjęcie nagrobka** i
> fundament wspólny dla wszystkich zdjęć — wybór źródła, zmniejszanie do 2048 px, podgląd z przybliżeniem i
> spójność kopii. Zdjęcia osób (baza zdjęć, dzielenie, „profilowe”, schemat v4) → [[ISSUE-017-person-photos]].

## What to build
1. **Zdjęcie nagrobka przy grobie — jedno:** dodaj (z galerii albo aparatem), zmień, usuń (po potwierdzeniu).
2. **Zdjęcie w aplikacji = własna kopia, zmniejszona:** JPEG, najwyżej 2048 px po dłuższym boku, jakość 85,
   orientacja zapisana w pikselach, bez danych EXIF (decyzja autora D2'). Oryginał zostaje w galerii.
3. **Gdzie widać:** nad tytułem w [[grob]] (element 1a), miniatura w karcie grobu w [[cmentarz]] (3 (d)), podgląd
   na pełnym ekranie z przybliżeniem ([[zdjecie]] B).
4. **Zdjęcie w kopii i po odtworzeniu**, z odciskiem danych zgodnym — także gdy zdjęcie dodano albo usunięto w
   trakcie kopii (D3).

## Acceptance Criteria
- [ ] US-005 AC-1 (grób): zdjęcie wybrane z galerii albo zrobione aparatem jest widoczne przy grobie.
- [ ] US-005 AC-2: aplikacja trzyma własną kopię pliku w prywatnym magazynie. Usunięcie oryginału z galerii nie
      zmienia niczego w aplikacji.
- [ ] US-005 AC-3: zdjęcie jest w kopii i wraca po odtworzeniu (odcisk danych obejmuje zdjęcia —
      [[NFR-002-odtworzenie-na-nowym-telefonie]]).
- [ ] **Zmniejszanie (D2'):** zapisane zdjęcie to JPEG, najwyżej 2048 px po dłuższym boku, w poprawnej orientacji;
      mniejsze zdjęcie nie jest powiększane.
- [ ] **Zmiana i usunięcie (D1'):** zdjęcie nagrobka da się zmienić na inne i usunąć po potwierdzeniu; grób ma
      najwyżej jedno zdjęcie.
- [ ] **Spójność kopii (D3):** kopia ze zdjęciem dodanym albo usuniętym w trakcie kopii odtwarza się z odciskiem
      zgodnym.
- [ ] Dodanie, zmiana i usunięcie zdjęcia zamawiają kopię w tle tak samo jak każdy zapis danych
      ([[ISSUE-010-background-backup]]).
- [ ] Aplikacja dalej bez uprawnienia `INTERNET`. Każde nowe uprawnienie ma w planie powód
      ([[NFR-005-dane-nie-opuszczaja-telefonu]]).
- [ ] Ekran stosuje wytyczne stylu B ([[style-b]], reguła 14).

## Out of Scope
- **Zdjęcia osób** — baza zdjęć osoby, zdjęcia dzielone, „profilowe”, schemat v4 → [[ISSUE-017-person-photos]].
- Kilka zdjęć nagrobka (decyzja autora: jedno wystarczy).
- Pinezka z lokalizacji zdjęcia → `TRACEABILITY.md` → *Open gaps* 2 (EXIF nie trafia do aplikacji — D2').
- Nowe zdjęcie robione na miejscu z widoku wizyty → [[EPIC-002-wizyta]] (M6).
- Wstrzymanie kopii w Zdjęciach Google dla zdjęć nagrobków — ustawienie telefonu autora
  (`TRACEABILITY.md` → *Open gaps* 2).

## Technical Notes
- **Co już jest w `grobing-code`** (ISSUE-007, ISSUE-008): tabela `Media` (ścieżka względna, osoba albo grób —
  dokładnie jedno), pliki w `mediaDir`, kopia pakuje je jako `media/<path>` ([[backup-format]]), odcisk danych liczy
  SHA-256 każdego pliku, stempel zmian widzi rozmiar i czas pliku. Dziś zdjęcie dodaje tylko przycisk debug.
- **Rozmiar (D2'):** ok. 50 zdjęć nagrobków × ok. 0,4–0,7 MB (**szacunek, do zmierzenia**) ≈ 20–35 MB. Razem z
  bazą zdjęć osób z ISSUE-017 (ok. 350 zdjęć) ok. 0,15–0,25 GB na kopię — szyfrowanie ~8 MB/s (ADR-004) to ok.
  20–30 s, daleko od ~10 min zadania w tle. Liczby kopii w tle (10 min ciszy, najpóźniej 60 min) zostają.
- **Spójność kopii:** migawka bazy (`VACUUM INTO`) i odczyt plików zdjęć nie są jedną transakcją
  ([[backup-format]] → *Known limits*) — D3.
- **Dane do testów i weryfikacji — wyłącznie wymyślone:** strażnik danych rodziny odmawia zapisu plików
  graficznych w trzech repo (poza `android/app/src/main/res/`), więc obrazy do testów `qa` generuje w kodzie; do
  galerii emulatora trafiają obrazy wygenerowane poza repo. Nigdy zdjęcia notatek rodziny.

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-012-transcribe-grave-screen]] (widok grobu) | product | `done` |
| [[ISSUE-008-backup-write]] · [[ISSUE-009-restore]] · [[ISSUE-010-background-backup]] (kopia zabiera zdjęcia, odtworzenie, kopia w tle) | technical | `done` |
| specyfikacje `ui`: [[zdjecie]] v1.1 (nowy) · [[grob]] v3 · [[cmentarz]] v3 | design | gotowe 2026-10-07, po stopie #1 |
| [[style-b]] (wytyczne stylu B) | design | v1.7 — reguła 14 (zdjęcia), próg SC 2.5.1 |
| paczka `image_picker` (oficjalna, flutter.dev) | technical | nowa zależność — D5 |
| [[ISSUE-017-person-photos]] | product | czeka na tę pozycję (fundament) |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP):
- test happy-path dla każdego AC;
- ręczna weryfikacja na emulatorze;
- dotyka warstwy danych, więc próbne odtworzenie z kopii przechodzi: zdjęcie wraca z odciskiem zgodnym;
- zero danych rodziny w zmianach;
- INVEST self-check.

US-005 idzie do werdyktu US po [[ISSUE-017-person-photos]].

## Implementation plan
> `planning`, 2026-10-07. **DoR:** jasny zakres ✅ · powiązana US: [[US-005-zdjecia]] (AC-1…AC-3) ✅ · krok ścieżki:
> n/a — M1 ✅ · `task-level` ✅.
> **Ekrany:** specyfikacje `ui` z 2026-10-07 — [[zdjecie]] v1.1 (nowy: arkusz źródła A, podgląd B, okno usunięcia C),
> [[grob]] v3 (jedno zdjęcie), [[cmentarz]] v3; wytyczne [[style-b]] v1.7 (reguła 14). Makieta
> `makieta-zdjecia.html` w katalogu tymczasowym sesji pokazuje wersję sprzed stopu #1 (kilka zdjęć, portrety) —
> obowiązują specyfikacje. **Warstwa danych:** bez zmiany schematu (grób ma najwyżej jeden wiersz `Media`),
> poprawka spójności kopii (D3), próbne odtworzenie kopii ze zdjęciem. **Źródło faktu:** zdjęcie nie jest
> twierdzeniem o dacie ani relacji — FR-001 go nie obejmuje (US-005 nie ma FR).

### Prior art (sources, not memory)
- **Library of Congress, *Personal Archiving: Digital Photographs*** ([digitalpreservation.gov](https://www.digitalpreservation.gov/personalarchiving/photos.html)),
  odczyt 2026-10-07: *„If there are multiple versions of an important photo, save the one with highest quality.”* ·
  *„Make at least two copies of your selected photos”*. Rama „oryginał + kopia dostępowa”: autor wybrał trzymać w
  aplikacji **kopię dostępową** (podgląd), a oryginał zostaje w galerii albo na papierze (D2'). To świadomy wybór, z
  kosztem nazwanym na stopie #1.
- **`image_picker`** (oficjalna paczka zespołu Fluttera; [pub.dev](https://pub.dev/packages/image_picker), wersja
  1.2.4), odczyt 2026-10-07:
  - *„On Android 13 and above this package uses the Android Photo Picker. On Android 12 and below use of Android
    Photo Picker is optional.”* — systemowe okno wyboru, bez uprawnienia do całej galerii;
  - `pickImage` bez parametrów: *„the image will be returned at it's original width and height”*;
    *„Compression is only supported for certain image types such as JPEG and on Android PNG and WebP”* — **paczka
    nie zmniejszy HEIF**, więc zmniejszanie robi aplikacja (D2', krok 3 `dev`);
  - *„When under high memory pressure the Android system may kill the MainActivity … use the
    `ImagePicker.retrieveLostData()` method to retrieve the lost data.”*
- **Silnik Fluttera:** `shell/platform/android/android_image_generator.cc` dekoduje obrazy przez Androida
  (`FlutterJNI.decodeImage`). Plik nie podaje formatów ani minimalnego API — F3.
- **Kod `grobing-code`, odczyt 2026-10-07 — luka w kopii, istniejąca już dziś:**
  - `backup_archive.dart` → `writeEncryptedBackup` liczy odcisk danych z `readDataState(…, mediaDir)`, który sam
    listuje pliki zdjęć, a **potem drugi raz** woła `listMediaFiles(mediaDir)` dla archiwum;
  - `restore_service.dart` odrzuca kopię, gdy odcisk danych z rozpakowanych plików ≠ odcisk z manifestu.

  Wniosek: zdjęcie dodane między tymi dwiema listami trafia do archiwum, ale nie do odcisku, więc **takiej kopii nie
  da się odtworzyć**, a kopia jest jedna i nadpisywana. Dziś zdjęcia dodaje tylko przycisk debug, więc luka jest
  nieosiągalna; ta pozycja ją otwiera (kopia w tle startuje po 10 min ciszy, a autor może wrócić i dodać zdjęcie).
  Usunięcie pliku w tym samym oknie wywraca samą kopię (pliku nie da się otworzyć) — kopia się nie zapisze.

### Falsifier — what is measured and what is not
| # | Pytanie | Wynik |
|---|---|---|
| F1 | Czy zapisane zdjęcie to JPEG ≤ 2048 px, w dobrej orientacji, i ile waży? | **Zmierzy** `dev` na emulatorze: zdjęcie z aparatu emulatora (pionowe i poziome) i wymyślone obrazy większe niż 2048 px → wymiary, orientacja na ekranie, rozmiar pliku. *Obali D2':* > 1 MB przy 2048 px na typowym zdjęciu → 1600 px (decyzja autora) |
| F2 | Czy kopia z ok. 350 zdjęciami mieści się w zadaniu w tle i ile trwa odcisk danych? | z rachunku: ~0,2 GB → szyfrowanie ~25 s. **Nie zmierzono** SHA-256 odcisku w Darcie na telefonie. **Zmierzy** `qa` na emulatorze: 350 wygenerowanych plików po ~0,6 MB → czas kopii, rozmiar, czas „Stanu danych” |
| F3 | Czy zdjęcie HEIF da się dodać? | **nie zmierzone.** `dev` próbuje z wymyślonym plikiem HEIF, jeśli da się go wygenerować na PC; bez pliku — „niesprawdzone” w *Dev report*. Plik, którego nie da się zdekodować, kończy się komunikatem „Nie udało się zapisać zdjęcia” (stan ze specyfikacji). Telefon autora — przy MVP |
| F4 | Czy kopia ze zdjęciem dodanym w trakcie kopii daje się odtworzyć? | ❌ dziś (z kodu, wyżej). **Zmierzy** test `qa`: najpierw pokazuje lukę, potem jej zamknięcie (D3) |
| F5 | Tempo: zdjęcie nagrobka 3 dotknięcia z galerii | ze specyfikacji. **Nie zmierzone na ekranie** — odczucie autora na stopie #2 |

### Decisions for stop #1 — round 1 (przedstawione 2026-10-07)
| # | Decyzja | Rekomendacja `planning` | Wynik |
|---|---|---|---|
| D1 | Usuwanie i podmiana zdjęcia | wchodzi minimum (nagrobek z oknem; osoba — zmiana z „Zapisz”) | **zmienione przez autora** → round 2 (D1', D6') |
| D2 | Rozdzielczość | oryginał bajt w bajt | **odrzucone przez autora** („raczej podglądowe”) → D2' |
| D3 | Spójność kopii: jedna lista plików; plik przed wierszem; usunięcie = wiersz + sprzątanie plików bez wiersza (> 1 h, pod zamkiem kopii, przed znacznikiem i migawką, też przy starcie); zdjęcie z formularza w katalogu tymczasowym | — | **przyjęte** |
| D4 | Decyzje projektowe `ui`: (a) kilka zdjęć naraz, (b) miniatury na liście grobów, (c) proporcja zdjęcia najwyżej kwadrat, (d) jedno zdjęcie osoby, (e) „Dodaj osobę” z lewej, (f) karta bez wcięcia | — | **przyjęte**; (a) i (d) zdezaktualizowane decyzją D1' (jedno zdjęcie nagrobka; osoby → ISSUE-017), (f) → ISSUE-017 |
| D5 | `image_picker`, przypięty dokładnie, bez nowych uprawnień; bez obsługi `retrieveLostData` | — | **przyjęte** + przypadek autora: zdjęcie zrobione dawno, dodane z galerii później — pokrywa systemowe okno wyboru (wszystkie zdjęcia i albumy) |
| D6 | Jedna pozycja | — | autor: „jak uważasz” → D6' |

### Stop #1 — round 1 (2026-10-07, odpowiedź autora)
Blisko słów autora:
- **D1:** *„nagrobek — wystarczy mi jedno zdjęcie, ale osoby chciałbym, aby miały «swoją bazę zdjęć» (lub dzieloną,
  jeżeli na zdjęciu jest kilka osób) i możliwość wybierania z nich «profilowego»”*;
- **D2:** *„zastanawiam się nad jakąś optymalizacją — to mają być raczej zdjęcia podglądowe niż takie najwyższej
  jakości — jakie mamy opcje?”*;
- **D3, D4:** ok; **D6:** *„jak uważasz”*;
- **D5:** ok, z przypadkiem do pokrycia: zdjęcie zrobione kiedyś (np. zdjęcie zdjęcia z albumu), a dopiero później
  wiadomo, że ta osoba leży w tym grobie — autor szuka zdjęcia w galerii i je dodaje.

**Kanon dla D1 (odczyt 2026-10-07, [GEDCOM 7.0](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html)):**
- `OBJE` (łącze) — *„Links the superstructure to the MULTIMEDIA_RECORD with the given pointer.”* Zdjęcie to osobny
  rekord, a osoba ma do niego łącze, więc jedno zdjęcie może mieć łącza od kilku osób;
- `CROP` — *„A subregion of an image to display”* (LEFT, TOP, WIDTH, HEIGHT w pikselach), osobno przy każdym
  łączu: twarz jednej osoby z grupowego zdjęcia;
- *„Unless otherwise specified, the first is the most-preferred value”* — „profilowe” = pierwsze łącze.

Dzisiejsza tabela `Media` ma **jednego** właściciela (osoba albo grób, `CHECK`), więc „baza zdjęć osoby, dzielona
między osoby” to **zmiana schematu** → [[ISSUE-017-person-photos]].

### Decisions for stop #1 — round 2 (przyjęte przez autora 2026-10-07: „tak”)
| # | Decyzja | Przyjęte | Dlaczego · co ją obali |
|---|---|---|---|
| D6' | **Podział** | **ISSUE-016 — zdjęcie nagrobka i fundament:** jedno zdjęcie przy grobie (dodaj, zmień, usuń), podgląd z przybliżeniem, miniatura na liście grobów, zmniejszanie (D2'), spójność kopii (D3); bez zmiany schematu. **ISSUE-017 — zdjęcia osoby:** schemat v4 (zdjęcie jako rekord + łącze osoba–zdjęcie w kolejności, jak `OBJE`), baza zdjęć, „profilowe”, dzielenie, ADR o modelu | Każda połowa ma własny przepływ do sprawdzenia na stopie #2; zmiana schematu idzie razem z ekranem, który jej potrzebuje |
| D1' | **Zdjęcie nagrobka: jedno; zmiana i usunięcie** | „Zmień zdjęcie” (bez okna — wymaga wybrania nowego) i „Usuń zdjęcie” (z oknem „Usunąć zdjęcie?”, „Zostaw” w akcencie) w podglądzie; „Dodaj zdjęcie” tylko bez zdjęcia ([[zdjecie]] B4, C, D5; [[grob]] D9) | *Obali:* autor zmienia zdjęcie przez pomyłkę — wtedy okno także przy zmianie |
| D2' | **Rozmiar zdjęcia w aplikacji** | **2048 px po dłuższym boku, JPEG 85**, orientacja w pikselach, bez EXIF; mniejszych nie powiększamy. Ok. 0,4–0,7 MB na zdjęcie (szacunek). Opcje przedstawione: oryginał (3–5 MB) · 2560 px · **2048 px** · 1600 px · 1280 px | Ok. 2× przybliżenia na ekranie ~1080 px: napis na tablicy i twarz z grupowego zdjęcia (przyszłe `CROP`). **Tracimy:** oryginał nie trafia do aplikacji; w kopii nie ma EXIF z lokalizacją. *Obali:* F1 > 1 MB na typowym zdjęciu → 1600 px |

### Scope diff vs the item (accepted at stop #1)
- **zakres:** zdjęcie osoby, portret w formularzu i miniatury osób **wychodzą** do [[ISSUE-017-person-photos]]; grób
  ma **jedno** zdjęcie.
- **+ AC — zmniejszanie (D2'):** JPEG ≤ 2048 px, poprawna orientacja.
- **+ AC — zmiana i usunięcie (D1').**
- **+ AC — spójność kopii (D3):** poprawka luki w kodzie ISSUE-008, bez której AC-3 nie jest prawdą.
- **+ ekran podglądu** ([[zdjecie]] B) i **miniatura na liście grobów** ([[cmentarz]] D9) — decyzje projektowe (D4).
- **bez zmian:** AC-1…AC-3 (w części o grobie), kopia zamawiana przy zapisie, brak `INTERNET`, styl B. **Bez zmiany
  schematu.**

### Steps (dev)
0. **Przed zmianą:** na `Medium_Phone` jest build release z publicznym cmentarzem i grobem z wymyślonymi osobami
   (stop #2 ISSUE-012). **Nie odinstalowuj** — te dane posłużą do kroków stopu #2.
1. **Zależność** — `pubspec.yaml`: `image_picker` przypięty dokładnie, z komentarzem w stylu pozostałych przypięć
   (oficjalna paczka, Photo Picker, bez sieci); zgodny z przypiętym Flutterem 3.41.1 (`flutter pub get` bez zmiany
   SDK, [[ADR-002-flutter-pinned]]). `test/no_cloud_sdk_test.dart` dalej zielony.
2. **Spójność kopii (D3 pkt 1)** — `lib/data/data_state.dart` i `lib/backup/backup_archive.dart`: lista plików
   zdjęć powstaje **raz** i służy i odciskowi, i archiwum (np. `readDataState` przyjmuje listę albo zwraca tę, którą
   policzył). Definicja odcisku się nie zmienia — odciski zapisane wcześniej zostają ważne.
3. **Zmniejszanie (D2')** — metoda natywna w istniejącym wzorcu kanałów Kotlin (`MainActivity`, jak kanał Dysku),
   poza wątkiem głównym: plik źródłowy → JPEG jakość 85, dłuższy bok ≤ 2048 px (mniejszy bez zmian rozmiaru), orientacja
   z EXIF zapisana w pikselach, bez EXIF w wyniku. Android 9+: `ImageDecoder` z docelowym rozmiarem (sam uwzględnia
   orientację; HEIF — F3); Android 7–8 (`minSdk` 24): `BitmapFactory` z `inSampleSize` + obrót z
   `android.media.ExifInterface` (bez nowej zależności). Wynik **w katalogu tymczasowym poza `mediaDir`** (niedokończony
   plik nie może trafić do kopii). Po stronie Darta interfejs `PhotoPreparer`, **podmienialny w testach** (atrapa kopiuje
   bajty). `image_picker` wywołany bez `maxWidth`/`imageQuality` — paczka nie zmniejsza HEIF i zostawia EXIF.
4. **API zdjęć** — nowy `lib/data/photos.dart` (czysty Dart; zapisy przez `drift`, więc `tableUpdates` zamawia kopię):
   - nazwa pliku: unikalna, bez danych z treści (np. `groby/<graveId>/<znacznik czasu>-<losowe>.jpg`), nigdy
     nadpisanie istniejącego;
   - `setGravePhoto(db, mediaDir, graveId, File prepared)`: przeniesienie gotowego pliku do `mediaDir` (**plik przed
     wierszem**), potem w jednej transakcji: usunięcie wierszy `Media` tego grobu i wstawienie nowego (dodanie i zmiana
     to ta sama operacja; grób ma najwyżej jedno zdjęcie);
   - `gravePhoto(db, graveId)`: wiersz o najniższym `id` (odporność na dane z kilkoma wierszami, np. z debug);
   - `deleteGravePhoto(db, graveId)` (D1'): **tylko wiersze** (D3 pkt 3);
   - `sweepOrphanMedia(db, mediaDir, {olderThan: 1 h})`: usuwa pliki bez wiersza starsze niż próg; pliki z wierszem
     i świeże zostają; puste katalogi też.
5. **Sprzątanie w kopii (D3 pkt 3)** — `lib/backup/backup_service.dart` → `backUpWhileLocked`: `sweepOrphanMedia`
   pod zamkiem, **przed** `dataStamp` i migawką. Także raz przy starcie (`main.dart`, w tle, pod tym samym zamkiem).
   Katalog tymczasowy zmniejszania czyszczony przy starcie.
6. **Dane dla ekranów** — `lib/data/graves.dart`: `GraveDetail` i `GraveSummary` dostają zdjęcie grobu (ścieżka albo
   brak).
7. **Wybór zdjęcia** — nowy `lib/app/photo/photo_picker.dart`: cienka warstwa nad `image_picker` (galeria — jedno
   zdjęcie, aparat), **podmienialna w testach**. Arkusz źródła `photo_source_sheet.dart` według [[zdjecie]] A.
8. **Podgląd** — nowy `lib/app/photo/photo_viewer_screen.dart` według [[zdjecie]] B i C: zdjęcie w całości na tle,
   `InteractiveViewer` do 4×, podwójne dotknięcie 2,5× w miejscu dotknięcia (SC 2.5.1); pasek z nazwą grobu i
   „Zdjęcie nagrobka”; „Zmień zdjęcie” (→ A, stany „zmiana w toku” i „nieudana zmiana”) i „Usuń zdjęcie” (→ okno C);
   stan błędu odczytu.
9. **Widok grobu** — `grave_screen.dart` według [[grob]] v3: element 1a (proporcja zdjęcia, najwyżej kwadrat,
   dotknięcie → podgląd), „Dodaj zdjęcie” obok „Dodaj osobę” tylko bez zdjęcia (`Wrap`), stany: zapisywanie, nieudany
   zapis, błąd odczytu. Obraz dekodowany w rozmiarze wyświetlania (`cacheWidth`/`ResizeImage`).
10. **Ekran cmentarza** — `cemetery_screen.dart` według [[cmentarz]] v3: miniatura 56 dp (kwadrat, promień 8 dp) w
    karcie grobu ze zdjęciem.
11. **Dane debug** — `lib/dev/fictional_data.dart`: plik zastępczy `.txt` przy grobie zastąp **obrazem wygenerowanym
    w kodzie** (np. przez `dart:ui` albo mały PNG składany w Darcie, z napisem „Wymyślony nagrobek”), bo widok grobu
    teraz go pokazuje. Nigdy zdjęcie z dysku ani z sieci.
12. **README** `grobing-code`: sekcja o zdjęciach — 2048 px JPEG 85 bez EXIF (D2'), nazwy plików, sprzątanie (D3),
    obrazy w testach tylko generowane w kodzie (strażnik danych rodziny).
13. **Sprawdzenia:** `dart format`, `flutter analyze`, `flutter test`, APK release; **scalony manifest wydania bez
    `INTERNET` i bez nowych uprawnień** (`aapt dump permissions`) — lista do *Dev report*. Na `Medium_Phone` build
    release wgrany na obecny, bez odinstalowania. F1 i F3 → *Dev report*.

### Files likely touched
- **Nowe:** `lib/data/photos.dart` · `lib/app/photo/photo_picker.dart` · `lib/app/photo/photo_preparer.dart` ·
  `lib/app/photo/photo_source_sheet.dart` · `lib/app/photo/photo_viewer_screen.dart`.
- **Zmienione:** `pubspec.yaml` · `pubspec.lock` · `android/app/src/main/kotlin/…/MainActivity.kt` (albo osobny plik
  kanału) · `lib/data/data_state.dart` · `lib/backup/backup_archive.dart` · `lib/backup/backup_service.dart` ·
  `lib/main.dart` · `lib/data/graves.dart` · `lib/app/grave/grave_screen.dart` · `lib/app/grave/cemetery_screen.dart` ·
  `lib/dev/fictional_data.dart` · `README.md`.
- **Testy (`qa`):** `test/data/photos_test.dart` (nowy) · `test/backup/backup_archive_test.dart` ·
  `test/backup/backup_service_test.dart` · `test/backup/restore_service_test.dart` · `test/data/graves_test.dart` ·
  `test/app/grave/*_test.dart` · `test/app/photo/*_test.dart` (nowe). **Obrazy w testach wyłącznie generowane w
  kodzie** — strażnik odmawia plików graficznych w repo.

### AC → tests (`qa`)
| AC | Test (happy-path) | Ręcznie |
|---|---|---|
| US-005 AC-1 (grób) | dane: `setGravePhoto` → wiersz z `graveId`, plik w `mediaDir`; widżet z atrapą wyboru: „Dodaj zdjęcie” → arkusz → galeria → zdjęcie nad tytułem, „Dodaj zdjęcie” znika; cmentarz → miniatura w karcie | kroki 1, 6 |
| US-005 AC-2 własna kopia pliku | dane: po dodaniu plik źródłowy usunięty → plik w `mediaDir` jest | agent: oryginał usunięty z galerii emulatora (`adb`) → zdjęcie dalej widać |
| US-005 AC-3 w kopii i po odtworzeniu | grób ze zdjęciem → kopia → odtworzenie → ten sam plik i wiersz, odcisk zgodny (istniejące atrapy) | agent: kopia na `Medium_Phone`, odtworzenie na `Grobing_Restore` (jeden emulator naraz), odcisk zgodny |
| **+ zmniejszanie (D2')** | widżet/dane: do API trafia plik z `PhotoPreparer` (atrapa); jednostkowo — obliczenie docelowego rozmiaru (dłuższy bok 2048, mniejszy bez zmian) | agent: F1 na emulatorze (wymiary, orientacja, rozmiar) |
| **+ zmiana i usunięcie (D1')** | dane: `setGravePhoto` drugi raz → jeden wiersz, nowy plik; `deleteGravePhoto` → wiersza nie ma, plik do sprzątania; widżet: „Usuń zdjęcie” → okno → „Zostaw” nic nie zmienia, „Usuń” → grób bez zdjęcia, „Dodaj zdjęcie” wraca; „Zmień zdjęcie” → nowe zdjęcie w podglądzie | kroki 3, 4 |
| **+ spójność kopii (D3)** | F4: plik dodany między odciskiem a archiwum → odtworzenie **przechodzi** (przed krokiem 2 `dev` — odrzucone); wiersz usunięty w trakcie kopii → kopia się zapisuje i odtwarza; `sweepOrphanMedia`: plik bez wiersza starszy niż 1 h znika, świeży i z wierszem zostają; sprzątanie przed znacznikiem — kopia nie powtarza się bez zmian | — |
| Zdjęcie zamawia kopię | widżet z atrapą: dodanie, zmiana, usunięcie → zamówienie kopii | — |
| Bez `INTERNET`, bez nowych uprawnień | istniejący test manifestu + `aapt dump permissions` na APK release (krok 13 `dev`) | — |
| Styl B, SC 2.5.1 | przegląd `ui` (subagent) ze zrzutów przed stopem #2; widżet: podwójne dotknięcie przybliża | całość |
| F2 — rozmiar i czas kopii | — | agent: 350 wygenerowanych plików po ~0,6 MB (build debug, po pomiarze sprzątnięte) → czas kopii, rozmiar, czas „Stanu danych” → *Verification* |
| DoD: zero danych rodziny | obrazy tylko generowane; grep zmian przed commitem | — |

### Manual verification (stop #2) — kroki według miejsca
**Agent przed stopem:** build release na `Medium_Phone` (wgrany na obecny, `dumpsys` potwierdza nowy build). W
galerii emulatora album **„Wymyślone”**: kilka obrazów **wygenerowanych na PC poza repo** (szare „nagrobki” z
napisem „Wymyślony”, poziome i pionowe). Agent sprawdza sam AC-2, AC-3, F1–F3 (*Verification*).

**Emulator `Medium_Phone`:**
1. Mapa → cmentarz → grób z wymyślonymi osobami → **„Dodaj zdjęcie”** → arkusz → „Wybierz z galerii” → poziomy
   „nagrobek” z albumu „Wymyślone”. Zdjęcie nad tytułem, „Dodaj zdjęcie” zniknęło.
2. **Dotknij zdjęcia** → podgląd: całe zdjęcie, w pasku nazwa grobu i „Zdjęcie nagrobka”. Podwójne dotknięcie
   przybliża w tym miejscu, drugie oddala. Wstecz.
3. Zdjęcie → **„Zmień zdjęcie”** → „Zrób zdjęcie” → aparat emulatora (wirtualna scena) → zatwierdź → podgląd pokazuje
   nowe zdjęcie. Wstecz → grób z nowym zdjęciem.
4. Zdjęcie → **„Usuń zdjęcie”** → okno → „Zostaw” → nic się nie zmienia → „Usuń zdjęcie” → „Usuń” → grób bez zdjęcia,
   „Dodaj zdjęcie” wróciło.
5. „Dodaj zdjęcie” → **pionowy** „nagrobek” z galerii → zdjęcie przycięte do kwadratu nad tytułem; w podglądzie całe.
6. Wstecz → **cmentarz:** karta grobu z miniaturą; karty innych grobów bez zmian.
7. **Odczucie:** czy zdjęcie nad tytułem nie spycha „Dodaj osobę” za daleko (D4 c)? Czy miniatury na liście grobów
   pomagają (D4 b)? Czy podgląd jest dość ostry jak na „zdjęcie podglądowe” (D2')?

**Napisz tutaj:** „ok” · „pomiń” · opis błędu przy numerze kroku.

### Out of Scope (this plan)
- Zdjęcia osób, portret w formularzu, miniatury osób w kartach, dzielenie zdjęć, „profilowe”, schemat v4 →
  [[ISSUE-017-person-photos]]. Wycinek twarzy (`CROP`) → po ISSUE-017.
- Kilka zdjęć nagrobka. Pinezka z lokalizacji zdjęcia (EXIF nie trafia do aplikacji — D2').
- Obsługa `retrieveLostData` (D5). Zdjęcie cmentarza (tabela `Media` zna tylko osobę i grób).
- Eksport zdjęć dla rodziny → [[US-006-eksport-dla-rodziny]]. Wstrzymanie kopii w Zdjęciach Google — ustawienie
  telefonu autora.

### For docs at closure
- **ADR-008 — zdjęcia w aplikacji: kopia dostępowa 2048 px i spójność kopii** z D2' i D3 (≥ 3 opcje z rundy 2:
  oryginał · 2560 · 2048 · 1600 · 1280 px; spójność: jedna lista + sprzątanie vs usunięcie pod zamkiem kopii).
- `04_ARCHITECTURE/backup-format.md` → *Known limits*: punkt „migawka a zdjęcia” zamknięty przez D3 (jedna lista,
  sprzątanie); rozmiar kopii ze zdjęciami z F2.
- `04_ARCHITECTURE/data-model.md` → *Media*: zdjęcie 2048 px JPEG bez EXIF, grób — najwyżej jedno zdjęcie, usuwanie
  przez sprzątanie; kierunek dla osób → ISSUE-017.
- [[US-005-zdjecia]] → *Notes*: rozdzielczość rozstrzygnięta (D2'); liczby kopii w tle zostają według F2.
- [[ISSUE-017-person-photos]] → *Dependencies*: ISSUE-016 `done`.
- [[NFR-002-odtworzenie-na-nowym-telefonie]]: odtworzenie ze zdjęciem sprawdzone (AC-3).

### Self-check (planning) — said out loud
1. **Kompletność:** zakres, pliki, AC → testy, kroki ręczne według miejsca, *Out of Scope* ✅.
2. **Spójność:** plan idzie za decyzjami autora ze stopu #1 (rundy 1–2) i specyfikacjami `ui` po stopie
   ([[zdjecie]] v1.1, [[grob]] v3). Wszystko spoza AC US-005 (D1', D2', D3, D4) jest przyjęte na stopie, nie po cichu.
3. **Własność:** zapisałem *What to build*, *Acceptance Criteria*, *Out of Scope* i *Technical Notes* po stopie (jak
   „Scope diff accepted” w ISSUE-012), tę sekcję, `status: in-progress`, *Dependencies* i swoje kolumny macierzy.
   Specyfikacje zmieniał `ui`, a ISSUE-017 założył `docs`.
4. **Warstwa danych:** bez zmiany schematu, więc bez testu migracji ✅ · odtworzenie kopii ze zdjęciem + spójność w
   trakcie kopii ✅ · źródło faktu: n/a — zdjęcie nie jest twierdzeniem (FR-001) ✅.
5. **Wystarczalność — czego plan nie ma:**
   - **rozmiar 0,4–0,7 MB to szacunek** — F1 mierzy na zdjęciach z emulatora i wymyślonych obrazach, prawdziwe zdjęcia
     z telefonu autora dopiero przy MVP;
   - **HEIF** (F3) — jeśli emulator nie da pliku, pierwsze prawdziwe sprawdzenie będzie na telefonie;
   - **kod natywny (Kotlin) nie ma testu automatycznego** — zmniejszanie sprawdza agent na emulatorze (F1); testy Darta
     idą przez atrapę.

## Dev report
> `dev`, 2026-10-07. Flutter 3.41.1 (przypięty) ✅. Bez zmiany schematu.

### What was built
- **Zależność:** `image_picker` 1.2.4, przypięty dokładnie, z komentarzem. `pubspec.lock`: tylko dopisane paczki
  (`image_picker_*`, `file_selector_*`, `cross_file`, `flutter_plugin_android_lifecycle`), żadna istniejąca nie
  zmieniła wersji.
- **D3 pkt 1 — jedna lista plików:** `readDataState(…, mediaFiles:)` przyjmuje listę; `writeEncryptedBackup` listuje
  pliki raz, po migawce, i tę samą listę daje odciskowi i archiwum. Definicja odcisku bez zmian.
- **Zmniejszanie (D2'):** `PhotoPreparation.kt` (kanał `com.grobing.app/photos`, osobny wątek): próbkowanie potęgą
  dwójki, potem skalowanie według wymiarów **zdekodowanej** bitmapy, więc wynik nie zależy od tego, czy dekoder podaje
  wymiar przed obrotem, czy po nim. Android 9+ `ImageDecoder` (sam obraca według EXIF), Android 7–8 `BitmapFactory` +
  `android.media.ExifInterface`. Zapis `*.part` i zmiana nazwy na końcu. Po stronie Darta `PhotoPreparer` (atrapa w
  testach), stałe `photoMaxEdge` = 2048 i `photoJpegQuality` = 85.
- **API zdjęć** `lib/data/photos.dart`: `newGravePhotoPath`, `gravePhotoPath` (najniższe `id`), `setGravePhoto`
  (przeniesienie pliku do `media/groby/<id>/…`, potem jedna transakcja: usunięcie wierszy grobu i wstawienie nowego),
  `deleteGravePhoto` (tylko wiersze), `sweepOrphanMedia` (pliki bez wiersza starsze niż 1 h, potem puste katalogi).
- **Sprzątanie (D3 pkt 3):** w `backUpWhileLocked` przed `dataStamp`; przy starcie w `requestBackgroundOnStart` pod
  `lock.tryAcquire()` (gdy zamek trzyma kopia, sprząta ona). Błąd sprzątania nigdy nie psuje kopii.
- **Ekrany:** `lib/app/photo/` — `photo_picker.dart` (`SystemPhotoPicker`; `discard` usuwa tylko kopię w cache
  aplikacji), `photo_preparer.dart`, `photos.dart` (`Photos`: `mediaDir`, `photo-work/` obok `media/`, wybór i
  przygotowanie; `clearWork` przy starcie), `photo_source_sheet.dart` (A), `photo_viewer_screen.dart` (B: całe
  zdjęcie, `InteractiveViewer` do 4×, podwójne dotknięcie 2,5× w miejscu dotknięcia; B4 „Zmień” / „Usuń”; C — okno
  usunięcia; wspólny `PhotoErrorLine`). Widok grobu (1a, stany zapisywania, błędu i nieczytelnego pliku, „Dodaj
  zdjęcie” w `Wrap` tylko bez zdjęcia), miniatura 56 dp na ekranie cmentarza. `Photos` idzie przez `GrobingApp` →
  `HomeScreen` → `CemeteryScreen` → `GraveScreen` / `PersonFormScreen`.
- **Dane debug:** `lib/dev/fictional_photo.dart` rysuje w Darcie „nagrobek” (PNG 480 × 360, własny mały koder PNG,
  `zlib` + CRC32); `fictional_data.dart` zapisuje `wymyslone/nagrobek-<partia>.png` zamiast `nota-<partia>.txt`.
- **README** → nowa sekcja *Zdjęcia*.

### Checks (dev, host Windows + emulator `Medium_Phone_API_36.1`)
- `dart format` ✅ · `flutter analyze` (cały projekt): **czyste**.
- `flutter test`: **340 ✅, 1 ❌ — oczekiwany:** `backup_archive_test.dart` → „backup of made-up data…” sprawdza
  nazwy `media/wymyslone/nota-1.txt`, a dane debug mają teraz `nagrobek-1.png` (krok 11 planu). Do poprawy przez `qa`.
- **APK release:** 57,1 MB (było 56,3 MB, +0,8 MB). **`aapt dump permissions`:** `WAKE_LOCK`, `ACCESS_NETWORK_STATE`,
  `RECEIVE_BOOT_COMPLETED`, `FOREGROUND_SERVICE` (od ISSUE-010) — **bez `INTERNET`, bez `CAMERA`, bez dostępu do
  pamięci; nowych uprawnień 0**. `image_picker` dokłada tylko `ImagePickerFileProvider` (plik dla aparatu).
- **Emulator:** build release wgrany na obecny (`adb install -r`; `firstInstallTime` 12:44 bez zmian, dane z ISSUE-012
  są). Galeria: album `Pictures/Wymyslone` — 4 obrazy wygenerowane na PC (Pillow) poza repo. Przejście (zrzuty w
  katalogu tymczasowym sesji): grób bez zdjęcia → „Dodaj zdjęcie” → arkusz → „Wybierz z galerii” → poziomy „nagrobek”
  → zdjęcie 4:3 nad tytułem, „Dodaj zdjęcie” znika ✅ · podgląd: całe zdjęcie, podwójne dotknięcie przybliża w miejscu
  i oddala ✅ · „Zmień zdjęcie” → obraz z EXIF 6 → stoi pionowo, w widoku grobu przycięty do kwadratu ze środka ✅ ·
  „Usuń zdjęcie” → okno → „Zostaw” nic nie zmienia → „Usuń” → grób bez zdjęcia, „Dodaj zdjęcie” wraca ✅ · „Zrób
  zdjęcie” → aparat emulatora → „Done” → zdjęcie ✅ · cmentarz: miniatura w karcie ✅.

**F1 — zmierzone** (kopia z emulatora rozszyfrowana na PC niezależnym dekoderem `age` v1 w Pythonie, odcisk w
manifeście = ekran „Stan danych” `ba2e4cb185501718`):

| Wejście (wymyślone) | Zapisane | Rozmiar | EXIF |
|---|---|---|---|
| JPEG 4000 × 3000 | JPEG **2048 × 1536** | 236 KB | brak (zostaje profil kolorów ICC) |
| JPEG 4000 × 3000 z EXIF orientation 6 | JPEG **1536 × 2048**, w pionie | 234 KB | brak |
| zdjęcie z aparatu emulatora 1440 × 1920 | **1440 × 1920** — bez powiększania | 28 KB | brak |

Rozmiar dotyczy obrazów syntetycznych z szumem. Prawdziwe zdjęcia mają więcej szczegółów, więc 0,4–0,7 MB z planu
dalej jest szacunkiem, nie pomiarem. Próg z D2' (> 1 MB) nie padł.

**F3 — niesprawdzone:** lokalny `ffmpeg` nie ma muksera HEIF, a Pillow bez `pillow-heif`. Pierwsze sprawdzenie —
telefon autora przy MVP.

### Deviations from the plan
1. **Okno wyboru zdjęć wymaga „Done”** (Android 16, `image_picker` 1.2.4): po dotknięciu zdjęcia trzeba jeszcze
   potwierdzić. Z galerii **4 dotknięcia, nie 3** ([[zdjecie]] → *Tempo*, [[grob]] → *Tempo*) — do poprawy przez `ui`
   przy przeglądzie. Około 50 dotknięć więcej na całe notatki.
2. **`photos` opcjonalne w ekranach** (null tylko w testach innych funkcji — jak `restore` w `GrobingApp`), a nie
   wymagane. Istniejące testy ekranów kompilują się bez zmian; bez `Photos` ekran nie ma zdjęcia ani „Dodaj zdjęcie”.
3. **Reguła rozmiaru tylko w Kotlinie** — bez jednostkowego testu w Darcie (plan: „jednostkowo — obliczenie
   docelowego rozmiaru”). Sprawdzona na emulatorze (F1).
4. **Katalog roboczy `photo-work/`** obok `media/` w pamięci aplikacji (nie w cache) — przeniesienie do `media/` to
   zmiana nazwy na tym samym systemie plików.
5. **Profil kolorów ICC zostaje w JPEG** (Android go dopisuje). EXIF, w tym lokalizacji, nie ma.
6. **PNG z przezroczystością** zamieni przezroczyste piksele na czerne (JPEG nie ma kanału alfa). Zdjęcia z aparatu i
   galerii przezroczystości nie mają; nieobsłużone.
7. **Pliki po zmianie i usunięciu widać na „Stanie danych” do sprzątania** (godzina): „Zdjęcia (wpisy) 1” przy „Pliki
   zdjęć 3”. Tak działa D3; kopia zawiera te pliki, a odcisk je liczy spójnie. Może dziwić — uwaga dla `ui`/autora.

### For qa
- Testy według *AC → tests*; popraw `backup_archive_test.dart` (nazwy plików debug: `nagrobek-<partia>.png`).
- **AC-3 na urządzeniu:** na `Medium_Phone` kopia jest skonfigurowana **do Pobranych** emulatora (nie do Dysku autora
  — okno otworzyło się w jego Dysku, w folderze `Grobing-proba`, i agent go nie użył): `grobing-klucz-016.age`,
  `grobing-kopia-016.age`. Hasło testowe jest w katalogu tymczasowym sesji (`haslo-testowe-016.txt`), poza repo.
  Pobrane mają też stare pliki ze SPIKE-003 (wymyślone dane).
- Dekoder `age_decrypt.py` i obrazy testowe leżą w katalogu tymczasowym sesji.
- **F2** (350 plików po ~0,6 MB) — do zrobienia przez `qa`.

### Fixes after the ui review (dev, 2026-10-07)
1. **MAJOR — „Zapisuję zdjęcie…” przy otwartym arkuszu:** `PhotoViewerScreen` dostał dwa kroki — `pickReplacement`
   (arkusz i okno systemowe, `File?`) i `replace(File)` (zapis). Stan „zmiana w toku” włącza się dopiero po wyborze.
   Sprawdzone na emulatorze (zrzut z arkuszem nad podglądem: widać obecne zdjęcie) i testem widżetu.
2. **Okno C:** treść 16 sp w kolorze tekstu (jak „Odrzucić wpis?”).
3. **Wczytywanie zdjęcia w grobie:** `frameBuilder` — do pierwszej klatki puste pole 4:3, bez przeskoku tytułu i osób.
4. **Android Photo Picker:** `image_picker_android` 0.8.13+17 domyślnie (`useAndroidPhotoPicker = false`) wysyła
   `ACTION_GET_CONTENT`. Teraz `SystemPhotoPicker` włącza Photo Picker (`image_picker_android` i
   `image_picker_platform_interface` jako bezpośrednie zależności, przypięte na wersjach już rozwiązanych — lockfile
   bez zmian wersji). Logcat: `act=android.provider.action.PICK_IMAGES … com.android.photopicker.MainActivity`.
   **„Gotowe” zostaje** — Photo Picker na Androidzie 16 wymaga go także przy jednym zdjęciu. Specyfikacja liczy 4
   dotknięcia ([[zdjecie]] v1.2).

## Verification
> `qa`, 2026-10-07. Werdykt — po stopie #2.

### Automated — `flutter test`: 367 ✅ (było 341) · `flutter analyze`: czyste · `dart format`: ✅
| AC / decyzja | Testy |
|---|---|
| US-005 AC-1 (grób) | `test/app/photo/grave_photo_screens_test.dart`: „Dodaj zdjęcie” → arkusz (galeria nad aparatem) → zdjęcie nad tytułem, „Dodaj zdjęcie” znika; zamknięcie arkusza i anulowanie wyboru nic nie zmienia · `test/data/photos_test.dart`: plik do `groby/<id>/`, jeden wiersz, `loadGrave`/`loadCemeteryGraves` widzą zdjęcie · `test/app/photo/photos_test.dart`: przygotowanie raz, kopia wyboru i plik roboczy usunięte |
| US-005 AC-2 | `photos_test` (dane): przekazany plik przeniesiony, zapisany zostaje, bajty te same |
| US-005 AC-3 | `test/backup/restore_service_test.dart`: grób ze zdjęciem → kopia → odtworzenie → ten sam plik, wiersz i odcisk |
| D2' zmniejszanie | atrapa w testach; prawdziwy kod natywny — F1 na emulatorze (*Dev report*) |
| D1' zmiana i usunięcie | dane: po zmianie jeden wiersz z nowym plikiem, stary plik do sprzątania; po usunięciu brak wiersza, plik zostaje · widżet: „Zmień zdjęcie” (przy otwartym arkuszu brak „Zapisuję zdjęcie…” — MAJOR) → nowe zdjęcie w podglądzie; „Usuń zdjęcie” → okno (tekst słowo w słowo) → „Zostaw” nic nie zmienia → „Usuń” → grób bez zdjęcia, „Dodaj zdjęcie” wraca |
| D3 spójność kopii | `backup_archive_test.dart` **F4**: katalog zdjęć podmieniony tak, że zaraz po listowaniu pojawia się nowe zdjęcie → katalog listowany **raz**, archiwum bez spóźnionego pliku, odcisk z rozpakowanej kopii = odcisk w manifeście. **Falsyfikator sprawdzony:** ten sam test na kodzie sprzed poprawki (`git show HEAD:…backup_archive.dart` w drzewie roboczym, potem przywrócone) — **czerwony** (2 listowania) · usunięcie w trakcie kopii: kopia ma plik, odcisk zgodny · `backup_service_test.dart`: sprzątanie przy starcie pod zamkiem (stary sierota znika, świeży zostaje; przy zajętym zamku nic) i w kopii przed znacznikiem (kopia nie powtarza się bez zmian) · `photos_test`: sprzątanie > 1 h, puste katalogi, brak katalogu |
| Kopia zamawiana przy zapisie | `photos_test`: dodanie, zmiana i usunięcie powiadamiają tabelę `media` (`tableUpdates` — droga zamawiania kopii z ISSUE-010) |
| Podgląd, SC 2.5.1 | widżet: nazwa grobu i „Zdjęcie nagrobka” w pasku, podwójne dotknięcie → 2,5×, drugie → 1× |
| Cmentarz D9 | widżet: miniatura 56 × 56 tylko przy grobie ze zdjęciem |
| Dane debug | `backup_archive_test` z nowymi nazwami `nagrobek-<partia>.png` |

Obrazy w testach rysuje kod (`fictional_photo.dart`, `test/support/photo_fakes.dart`); żadnego pliku graficznego w repo.

### Agent checks on the emulators (release, wymyślone dane i obrazy wygenerowane poza repo)
- **AC-1 (`Medium_Phone`):** galeria → zdjęcie poziome 4:3 nad tytułem; „Zmień” → obraz z EXIF 6 stoi pionowo, w grobie
  przycięty do kwadratu; „Usuń” z oknem; aparat emulatora; miniatura na cmentarzu.
- **AC-2:** oryginał (`wymyslony-nagrobek-maly.jpg`) usunięty z galerii i z MediaStore (`adb`), aplikacja zatrzymana i
  uruchomiona — zdjęcie dalej w grobie.
- **AC-3:** kopia 15:11 z `Medium_Phone` (do Pobranych, hasło testowe) → **niezależny dekoder `age` w Pythonie** na PC:
  manifest = ekran „Stan danych” (`ba2e4cb185501718`), pliki 2048 px bez EXIF (F1) → **odtworzenie na
  `Grobing_Restore`** (build zaktualizowany z wersji z 2026-10-06, migracja v2→v3 przy okazji przeszła): „Odtworzono
  kopię… odcisk `ba2e4cb185501718` — ten sam co niżej”, grób pokazuje zdjęcie.
- **F2 (host, `flutter test`, JIT):** 350 plików × 600 KB (205 MB) — odcisk danych 4,9 s, cała kopia 21,8 s
  (~9,4 MB/s). Progi D2' (kopia > 5 min, „Stan danych” > 30 s) daleko. Telefon wolniejszy niż host — przy pełnej bazie
  zdjęć osób (ISSUE-017) „Stan danych” może liczyć kilka sekund (uwaga dla ISSUE-017).
- **F3 (HEIF):** niesprawdzone (*Dev report*).
- **Uprawnienia:** bez nowych (*Dev report*); APK 57,1 MB.

### ui review (subagent bez historii, ze zrzutów emulatora i kodu)
0 BLOCKER · 1 MAJOR (poprawiony, *Fixes after the ui review* 1) · MINOR:
- treść okna C (poprawione w kodzie);
- przeskok przy wczytywaniu zdjęcia (poprawione w kodzie, stan w [[grob]] v3.1);
- „Gotowe” w oknie wyboru (falsyfikator wykonany — zostaje; [[zdjecie]] v1.2, [[grob]] v3.1: 4 dotknięcia);
- „B — wczytywanie” bez wskaźnika (specyfikacja);
- zmierzone, ile osób mieści się nad zgięciem: poziome do 4, pionowe do 3 ([[grob]] *Tempo*, D8);
- wskaźnik postępu w roli akcentu ([[style-b]] v1.8);
- „Stan danych”: przez godzinę „Zdjęcia (wpisy) 1” przy „Pliki zdjęć 3” — opis do ADR-008 i README; linia na ekranie
  tylko, jeśli autora to zdziwi.

Zgodne: kolejność elementów, proporcje (4:3 i kwadrat), promienie, cele dotyku, role kolorów, kontrast z tokenów
(bez zmian), reguła 14, teksty. **Niesprawdzone:** duża czcionka (200 %) i TalkBack — tylko z kodu.

### Corrections
- *Prior art* cytował README `image_picker` („On Android 13 and above this package uses the Android Photo Picker”).
  Kod `image_picker_android` 0.8.13+17 robi to tylko z `useAndroidPhotoPicker = true` — poprawione w kodzie
  (*Fixes* 4).
- Na `Medium_Phone` przez pomyłkę agent wybrał raz w oknie wyboru stary zrzut ekranu z emulatora (okno Dysku z 5.10,
  bez danych rodziny) jako zdjęcie nagrobka i od razu je zmienił. Plik zostaje tylko w pamięci aplikacji na emulatorze,
  do sprzątania po godzinie; poza emulatorem go nie ma.

### State left on the emulators (dla autora)
- `Medium_Phone`: kopia skonfigurowana **do Pobranych** emulatora (`grobing-kopia-016.age`) z hasłem testowym — dalsze
  kopie w tle idą tam. Grób „Grob wymyslonych” bez zdjęcia; w galerii album „Wymyslone” (3 wymyślone obrazy).
- `Grobing_Restore`: nowy build, dane z kopii 016. Jego ustawienia kopii nadal wskazują stary plik testowy w Dysku
  (`Grobing-proba`, ISSUE-009) — kopia w tle może tam pisać (wymyślone dane).

### Package list for docs
- **grobing-code:** `README.md` · `pubspec.yaml` · `pubspec.lock` ·
  `android/app/src/main/kotlin/com/grobing/app/MainActivity.kt` · `…/PhotoPreparation.kt` (nowy) ·
  `lib/main.dart` · `lib/app/grobing_app.dart` · `lib/app/home/home_screen.dart` ·
  `lib/app/grave/cemetery_screen.dart` · `lib/app/grave/grave_screen.dart` · `lib/app/grave/person_form_screen.dart` ·
  `lib/app/photo/photo_picker.dart` · `photo_preparer.dart` · `photos.dart` · `photo_source_sheet.dart` ·
  `photo_viewer_screen.dart` (nowe) · `lib/backup/backup_archive.dart` · `lib/backup/backup_service.dart` ·
  `lib/data/data_state.dart` · `lib/data/graves.dart` · `lib/data/photos.dart` (nowy) · `lib/dev/fictional_data.dart` ·
  `lib/dev/fictional_photo.dart` (nowy) · `test/backup/backup_archive_test.dart` · `backup_service_test.dart` ·
  `restore_service_test.dart` · `test/data/photos_test.dart` (nowy) · `test/support/photo_fakes.dart` (nowy) ·
  `test/app/photo/photos_test.dart` · `grave_photo_screens_test.dart` (nowe).
- **grobing-vault:** `00_START_HERE/CURRENT_STATE.md` · `00_START_HERE/TRACEABILITY.md` ·
  `03_REQUIREMENTS/user-stories/US-005-zdjecia.md` · `05_DESIGN/zdjecie.md` (nowy) · `05_DESIGN/grob.md` ·
  `05_DESIGN/wpis-osoby.md` · `05_DESIGN/cmentarz.md` · `05_DESIGN/brand/style-b.md` ·
  `backlog/issues/ISSUE-016-photos-grave-and-person.md` (nowy) · `backlog/issues/ISSUE-017-person-photos.md` (nowy)
  — plus pliki zamknięcia `docs` (ADR-008 i *For docs at closure*).
- **Kontrola danych rodziny w zmianach (przed `git add`):** brak plików `*.db`, `*.age`, `*.tar`, eksportów, zdjęć;
  brak adresów e-mail, kodów pocztowych i numerów PESEL; osoby wyłącznie wymyślone („Wymyślony”, „Zmyślona”,
  „Testowa”). `family_data_dir` w tej pozycji nie był czytany.

### Manual (stop #2) — autor, emulator `Medium_Phone`, 2026-10-07
- **Kroki 1–6: „ok”.** Sprawdzone na urządzeniu po odpowiedzi: grób ma zdjęcie nad tytułem, a autor dopisał dwie
  wymyślone osoby (czyli sprawdzał też przewijanie przy zdjęciu).
- **Krok 7 (odczucie): „jest dobrze”** — wysokość zdjęcia, miniatury na liście, „Done” w oknie wyboru.
- **Zmiana od autora** (ze zrzutem, strzałka z przycisku w miejsce zdjęcia): *„dodaj zdjęcie powinno być domyślnie na
  polu przeznaczonym dla zdjęcia”*. Wprowadzone tym samym łańcuchem: `ui` → [[grob]] v3.2 (D12: pole „Dodaj zdjęcie
  nagrobka” 120 dp w miejscu zdjęcia, rząd działań tylko z „Dodaj osobę”, komunikat błędu pod polem); [[zdjecie]] (nawigacja
  i *Tempo*) · `dev` → `_AddPhotoField` w `grave_screen.dart` · `qa` → test widżetu (pole nad tytułem, brak „Dodaj
  zdjęcie” w rzędzie), `flutter analyze` czyste, **367 ✅**, build release na emulatorze, zrzut pola zgodny z v3.2.
- **Krok kontrolny 8** (pole „Dodaj zdjęcie nagrobka”): autor **„ok”** — według logcat bez otwarcia okna wyboru po
  16:03, czyli ocena wyglądu pola, a nie przejście. Przejście (pole → arkusz → galeria → „Done” → zdjęcie w miejscu
  pola) wykonał agent na emulatorze — ✅.

### Verdict — APPROVED (self-check, z uwagami)
Każde AC ma test happy-path i sprawdzenie na urządzeniu (AC-1 na `Medium_Phone`, AC-2 z usunięciem oryginału z
galerii, AC-3 z odtworzeniem na drugim emulatorze i niezależnym rozszyfrowaniem na PC). D3 ma falsyfikator, który na
starym kodzie jest czerwony. Przegląd `ui`: MAJOR poprawiony przed stopem; stop #2 „ok” z jedną zmianą (D12), wprowadzoną
i sprawdzoną.

**Uwagi (czego nie sprawdzono albo co zostaje):**
- HEIF (F3) — niesprawdzone; pierwszy raz na telefonie autora przy MVP;
- rozmiar 0,4–0,7 MB na prawdziwym zdjęciu — szacunek; zmierzone tylko obrazy syntetyczne (F1);
- F2 tylko na hoście (JIT); telefon wolniejszy — „Stan danych” przy pełnej bazie zdjęć osób (ISSUE-017) może liczyć
  kilka sekund;
- „Done” w oknie wyboru (Android 16) — 4 dotknięcia, poza kontrolą aplikacji;
- duża czcionka i TalkBack — tylko z kodu;
- kod natywny zmniejszania bez testu automatycznego (sprawdzony na emulatorze);
- „Stan danych” przez godzinę pokazuje więcej plików niż wpisów (sprzątanie D3) — do opisania w ADR-008 i README;
  autora to na stopie #2 nie zdziwiło.
