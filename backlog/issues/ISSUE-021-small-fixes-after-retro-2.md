---
title: "ISSUE-021 — Small fixes after retro 2: Polish system strings, debug seed names, two buttons without a tap action, tests README"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
ideal_days: 0.5
quality-verdict: APPROVED
verdict-date: 2026-10-08
verdict-reviewer: self-check
source: "[[2026-10-08-retro-02]] R3 i R9"
created: 2026-10-08
updated: 2026-10-08
---

# ISSUE-021 — Drobne poprawki po retro 2

> Decyzja autora w [[2026-10-08-retro-02]] (R9, R3): jedna mała pozycja, **przed pierwszymi prawdziwymi danymi**.
> Poprawki do ekranów z [[US-002-przepisanie-grobu]] ([[ISSUE-012-transcribe-grave-screen]],
> [[ISSUE-015-add-cemetery-from-database]]) i [[US-005-zdjecia]] ([[ISSUE-016-photos-grave-and-person]]).
> Kolumnę Issue(s) w `TRACEABILITY.md` wpisuje `planning`.

## What to fix
1. **Polskie teksty systemowe** — `MaterialLocalizations` są po angielsku (przegląd `ui`, uwaga 11): podpowiedzi
   i etykiety widżetów Fluttera (np. okno daty, „wklej”, opisy przycisku wstecz) w aplikacji po polsku.
2. **Wstępne dane debug** ([[ISSUE-012-transcribe-grave-screen]] → *Notes*): wszyscy wymyśleni z
   [[ISSUE-007-data-layer]] mają nazwisko „Wymyślona”, także „Ojciec” — na ekranach wygląda to jak błąd odmiany.
   Tylko build debug; wymyślone osoby zostają wymyślone.
3. **Semantyka dwóch przycisków** (przegląd `ui` przy [[ISSUE-017-person-photos]], MAJOR tego samego wzorca):
   „Dodaj zdjęcie nagrobka” ([[ISSUE-016-photos-grave-and-person]]) i podgląd cmentarza z bazy
   ([[ISSUE-015-add-cemetery-from-database]]) mają opis dla czytnika, ale bez akcji dotknięcia, więc Switch Access
   i Voice Access ich nie naciśną. Poprawka i test na każdy ekran.
4. **README `grobing-code` → testy** (R3, pisze `qa`): krótka sekcja o zawieszonych przebiegach — strumień drift i
   timer fałszywego czasu ([[ISSUE-014-home-map-of-poland]] → *Verification*), zapis albo odczyt bazy w
   `tester.runAsync` przy podpiętym ekranie ([[ISSUE-012-transcribe-grave-screen]] → *Verification*), wzorzec
   `leaveScreen`, zablokowany `sqlite3.dll` i `flutter_01.log` w korzeniu repo po zawieszonym przebiegu.

## Acceptance Criteria
- [ ] **AC-1** — widżety systemowe w aplikacji mówią po polsku (test: `MaterialLocalizations.of(context)` w
      aplikacji zwraca polskie teksty).
- [ ] **AC-2** — wymyśleni w buildzie debug mają nazwiska, które na ekranach nie wyglądają jak błąd odmiany.
- [ ] **AC-3** — oba przyciski mają akcję dotknięcia w drzewie semantyki (test na każdy ekran).
- [ ] **AC-4** — sekcja w README `grobing-code` → testy.

## Notes
- Specyfikacje ekranów się nie zmieniają (semantyka wynika z wzorca przeglądu ISSUE-017), więc `pm` może
  skierować pozycję od razu do `planning`. Jeśli plan pokaże zmianę na ekranie → najpierw `ui`.
- Bez zmiany schematu, bez warstwy danych.

## Implementation plan
> `planning`, 2026-10-08 (wybór autora w `/pm`). **DoR:** zakres jasny, `delivery-style: task-level`, pod
> [[US-002-przepisanie-grobu]] i [[US-005-zdjecia]] (poprawki ich ekranów po zamknięciu), poza krokami ścieżki.
> **Bez `ui`:** żadna specyfikacja w `05_DESIGN/` się nie zmienia — teksty systemowe Fluttera nie są w
> specyfikacjach, a akcja dotknięcia jest niewidoczna. **Bez warstwy danych:** bez schematu, migracji i próbnego
> odtworzenia; wymyślone dane zmieniają się tylko w buildzie debug, a fakty o rodzinie nie są zapisywane.

### Prior art (sources, not memory)
- **Flutter 3.41.1 (przypięty), `packages/flutter_localizations`**: `material_pl.arb` ma `backButtonTooltip`
  „Wstecz”, `pasteButtonLabel` „Wklej”, `selectAllButtonLabel` „Zaznacz wszystko”, `closeButtonTooltip` i
  `modalBarrierDismissLabel` „Zamknij” (sprawdzone w SDK na tej maszynie). Pakiet jest częścią SDK
  (`sdk: flutter`), a nie z pub.dev, więc nie zmienia wersji Fluttera (ADR-002). Jego `intl: 0.20.2` jest już
  w `pubspec.lock` jako zależność przechodnia, więc w locku nic się nie przesuwa.
- **Wzorzec semantyki z [[ISSUE-017-person-photos]]** (MAJOR z przeglądu `ui`, `person_photos_screen.dart:226`):
  `Semantics(button: true, label: …, onTap: onTap, excludeSemantics: true)`. `excludeSemantics` wycina akcję
  dotknięcia `InkWell`, więc `Semantics` musi mieć własne `onTap`. Test: `isSemantics(isButton: true,
  hasTapAction: true)` w `person_photos_screens_test.dart:245`.
- **Przegląd kodu:** w `lib/` jest 5 miejsc z `excludeSemantics: true`, a bez `onTap` są dokładnie 2 z pozycji:
  `grave_screen.dart:400` (`_AddPhotoField`) i `base_preview_screen.dart:219` (`_satelliteLink`). Innych nie ma.

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego |
|---|---|---|---|
| D1 | **Język tekstów systemowych** | **zawsze polski**, niezależnie od języka telefonu (`locale: Locale('pl')`, tylko `pl` w `supportedLocales`) | cała aplikacja jest po polsku (`language: pl`). Gdyby telefon był po angielsku, „podążanie za telefonem” dałoby z powrotem angielskie „Back” obok polskich ekranów |
| D2 | **Nazwiska wymyślonych w buildzie debug** | według formy, jak w testach (`restore_service_test.dart:197`): Ojciec → „Wymyślony”, Matka → „Wymyślona” (z d. „Zmyślona” bez zmian), Dziecko → „Wymyślone”. Partnerka „Zmyślona” i dziecko z drugiego związku bez nazwiska — bez zmian | to już konwencja repo, a słowa są w repo, więc strażnik treści nie ma tu nic nowego. Model jest bez płci (decyzja przy US-003), a nazwisko to zwykły tekst |

### Scope diff vs the item (to accept at stop #1)
- **„okno daty” z pozycji nie istnieje:** aplikacja nie używa `showDatePicker`, daty się wpisuje. Pkt 1 dotyczy
  więc: podpowiedzi przycisku wstecz, menu tekstu (Wytnij / Kopiuj / Wklej / Zaznacz wszystko) i etykiet
  zamykania arkuszy i okien dla czytnika ekranu;
- **dochodzi poprawka jednego testu:** `restore_screen_test.dart:213` szuka podpowiedzi „Back” → „Wstecz”;
- **dochodzi pomiar APK** przed zmianą i po niej: `flutter_localizations` wnosi teksty wszystkich języków, a
  ostatni release ma 61,2 MB (`build/…/app-release.apk`, 2026-10-08).

### Steps (dev)
1. **Pomiar przed:** `flutter build apk --release` na obecnym `main` → rozmiar APK zapisany w *Dev report*.
2. **AC-1** — `pubspec.yaml`: `flutter_localizations: sdk: flutter` z komentarzem (D1, SDK, bez wersji).
   `lib/app/grobing_app.dart` → `MaterialApp`: `locale: Locale('pl')`, `supportedLocales: [Locale('pl')]`,
   `localizationsDelegates: GlobalMaterialLocalizations.delegates`. Po `flutter pub get` diff `pubspec.lock`
   zawiera **tylko** `flutter_localizations`; inna zmiana w locku → STOP i powiedz.
3. **AC-2** — `lib/dev/fictional_data.dart`: `person()` dostaje nazwisko (D2). Nazwa grobu „Grób rodzinny
   Wymyślonych” zostaje.
4. **AC-3** — `onTap: onTap` w `Semantics` `_AddPhotoField` i `onTap: _openSatellite` w `Semantics` linku
   satelitarnego; komentarz przy każdym, jak w ISSUE-017 (Switch Access, Voice Access, WCAG 2.2 SC 4.1.2).
5. **Pomiar po:** ten sam build release, rozmiar i różnica w *Dev report*.
6. Przejście na emulatorze (R5 — teksty systemowe są na ekranach): `Medium_Phone`, build release na istniejących
   danych (aktualizacja, bez odinstalowania): przycisk wstecz, menu tekstu w polu „Nazwisko”, arkusz źródła
   zdjęcia nagrobka. Zrzuty w scratchpadzie.

### Files likely touched
- `grobing-code`: `pubspec.yaml`, `pubspec.lock`, `lib/app/grobing_app.dart`, `lib/dev/fictional_data.dart`,
  `lib/app/grave/grave_screen.dart`, `lib/app/home/base_preview_screen.dart` — `dev`;
- testy — `qa`: nowy test lokalizacji (np. `test/app/localizations_test.dart`), `test/app/restore_screen_test.dart`
  („Back” → „Wstecz”), `test/app/photo/grave_photo_screens_test.dart`, `test/app/home/home_screen_test.dart`, nowy
  `test/dev/fictional_data_test.dart`;
- `grobing-code/README.md` → nowa sekcja **„Testy”** — `qa` (AC-4, R3);
- `grobing-vault`: ta pozycja (plan — `planning`, *Dev report* — `dev`, *Verification* — `qa`), `TRACEABILITY.md`
  (Issue(s) i Issue Status — `planning`), `CURRENT_STATE.md` — `docs`.

### AC → checks (`qa`)
| AC | Sprawdzenie |
|---|---|
| AC-1 | test na `GrobingApp`: `MaterialLocalizations.of(context)` → `backButtonTooltip` „Wstecz”, `pasteButtonLabel` „Wklej”; `Localizations.localeOf` = `pl`. Pełny zestaw testów zielony po zmianie „Back” → „Wstecz” |
| AC-2 | `addFictionalData` na bazie w pamięci → Ojciec „Wymyślony”, Matka „Wymyślona” z d. „Zmyślona”, Dziecko „Wymyślone” |
| AC-3 | `tester.getSemantics(find.bySemanticsLabel('Dodaj zdjęcie nagrobka'))` → `isSemantics(isButton: true, hasTapAction: true)`; link satelitarny → `isSemantics(isLink: true, hasTapAction: true)`; na każdym akcja z drzewa semantyki (`SemanticsAction.tap`) otwiera to samo co dotknięcie (arkusz źródła zdjęcia / wywołanie linku) |
| AC-4 | sekcja „Testy” w README: strumień drift i timer fałszywego czasu ([[ISSUE-014-home-map-of-poland]] → *Verification*), zapis albo odczyt bazy w `tester.runAsync` przy podpiętym ekranie ([[ISSUE-012-transcribe-grave-screen]] → *Verification*), wzorzec `leaveScreen`, zablokowany `sqlite3.dll` i `flutter_01.log` w korzeniu repo po zawieszonym przebiegu |
| — | `dart format`, `flutter analyze`, `flutter test` zielone; dane w zmianach tylko wymyślone (strażnik przy `git add`) |

### Manual verification (stop #2) — kroki według miejsca
**Agent — emulator `Medium_Phone`, build release, przed stopem #2 (R4):**
1. `uiautomator dump` na grobie bez zdjęcia: węzeł „Dodaj zdjęcie nagrobka” ma `clickable="true"`; to samo dla
   „Zobacz zdjęcie satelitarne” w podglądzie cmentarza z bazy. Porównanie z dumpem sprzed zmiany (`clickable="false"`).
2. Przycisk wstecz: `content-desc` „Wstecz”; długie przytrzymanie w polu z tekstem → menu „Wklej” / „Zaznacz
   wszystko” — zrzut.
3. Aktualizacja na istniejących danych: wpisy z wcześniejszych stopów są na miejscu (aplikacja wgrana bez
   odinstalowania).

**AC-2 bez emulatora (nazwane):** wymyślone dane są tylko w buildzie debug, a build debug na `Medium_Phone`
wymagałby odinstalowania release (inny podpis), co kasuje dane testowe autora. Pokrywa to test AC-2.

**Autor — odczucie:** brak (pozycja bez nowego ekranu; DoD → *Kto sprawdza*). Stop #2 = „kroki oddane agentowi”
ze zrzutami.

### Out of Scope (this plan)
- własne teksty aplikacji (już po polsku) i formaty dat (`dates.dart`, `polish.dart` zostają);
- teksty systemowe w języku telefonu (D1);
- sprawdzenie w całym repo, że żadne `Semantics` z `excludeSemantics` nie gubi akcji (test na źródłach) — to
  trzecia instancja tego samego wzorca (ISSUE-017 + te dwie), więc kandydat na retro, nie tu;
- dane wymyślone już zapisane na emulatorach — zostają ze starymi nazwiskami (seed dodaje nową paczkę);
- specyfikacje w `05_DESIGN/`.

### Falsifier — what will show this shape is wrong
- diff `pubspec.lock` pokazuje coś poza `flutter_localizations` → zależność rusza wersje przy przypiętym SDK;
  STOP przed dalszymi krokami;
- APK rośnie o więcej niż ~2 MB → teksty wszystkich języków kosztują za dużo; wtedy własny delegat tylko dla `pl`
  (decyzja autora);
- dump na emulatorze dalej pokazuje `clickable="false"` przy zielonym teście → test semantyki nie mierzy tego,
  co widzi Android, a wzorzec z ISSUE-017 trzeba sprawdzić także tam.

### Self-check (planning) — said out loud
- **Wystarczalność:** pozycja nie sprawdza Switch Access ani Voice Access „w ręce” — dowodem jest drzewo semantyki
  i `clickable` w dumpie Androida, a nie przełącznik na emulatorze.
- **Ryzyko:** jedyna zmiana z zależnością to `flutter_localizations`; reszta to dwie linie semantyki, nazwiska w
  seedzie i README.
- **Własność:** `planning` napisał tę sekcję, `status: in-progress` i kolumny Issue(s) / Issue Status w
  `TRACEABILITY.md` (wiersze US-002 i US-005).

## Dev report
> `dev`, 2026-10-08. Stop #1: „tak” (D1, D2 z rekomendacjami). Flutter 3.41.1 zgodny z przypiętym.

### What was built
- **AC-1:** `flutter_localizations` (`sdk: flutter`) w `pubspec.yaml`; `MaterialApp` w `grobing_app.dart`:
  `locale: Locale('pl')`, `supportedLocales: [Locale('pl')]`,
  `localizationsDelegates: GlobalMaterialLocalizations.delegates` (D1).
- **AC-2:** `fictional_data.dart` → `person(given, surname)`: Ojciec „Wymyślony”, Matka „Wymyślona” z d. „Zmyślona”,
  Dziecko „Wymyślone” (D2).
- **AC-3:** `onTap` w `Semantics` pola „Dodaj zdjęcie nagrobka” (`grave_screen.dart`) i linku „Zobacz zdjęcie
  satelitarne” (`base_preview_screen.dart`).
- `dart format` i `flutter analyze`: czyste.

### Measured
- **APK release:** przed 61 205 420 B · po 62 024 620 B → **+819 200 B (~0,8 MB)**, poniżej progu ~2 MB z planu.

### Falsifier hit — `pubspec.lock` (waiting for the author)
- Diff locka to nie tylko `flutter_localizations`: **`intl` 0.20.3 → 0.20.2** (cofnięcie o poprawkę).
  `flutter_localizations` z przypiętego SDK wymaga dokładnie `intl: 0.20.2`, więc innej wersji się nie da.
- Kto używa `intl`: tylko `latlong2`, wyłącznie w `LatLng.toString()` (`NumberFormat` w tekście do debugowania).
  Kod aplikacji nie importuje `intl` i nie wywołuje `LatLng.toString()`. `flutter_localizations` nie ustawia
  `Intl.defaultLocale`.
- Co cofa 0.20.3 (CHANGELOG): symbole walut TRY i GHS, parsowanie locale ze skryptem (`zh-Hans-CN`), CLDR v48 → v46,
  pragma dla wasm. Nic z tego Grobing nie używa.
- Plan mówił „inna zmiana w locku → STOP” → **decyzja autora 2026-10-08: „tak”, `intl` 0.20.2 przyjęty.**

### Emulator pass (R5) — `Medium_Phone`, build release wgrany na istniejące dane (`install -r`)
| Sprawdzenie | Przed (release z ISSUE-019) | Po |
|---|---|---|
| „Dodaj zdjęcie nagrobka” w drzewie Androida (`uiautomator dump`) | `clickable="false"` | `clickable="true"`; dotknięcie otwiera arkusz „Zdjęcie nagrobka” |
| „Zobacz zdjęcie satelitarne, w innej aplikacji” w podglądzie cmentarza z bazy | `clickable="false"` | `clickable="true"` |
| przycisk wstecz (`content-desc`) | „Back” | „Wstecz” |
| menu tekstu w polu wyszukiwania (długie przytrzymanie) | — | „Wytnij · Kopiuj · Wklej · Udostępnij · Więcej” |
| dane po aktualizacji | 2 groby · 5 osób | 2 groby · 5 osób (te same groby i osoby) |

Zrzuty i dumpy w scratchpadzie sesji (`before-*`, `after-*`), nie w repo. Błędów nie znaleziono.

### For `qa`
- **Teksty Fluttera, które teraz brzmią po polsku dla czytnika ekranu:** tło pod arkuszem — „Siatka” z podpowiedzią
  „Zamknij: Plansza dolna” (po angielsku „Scrim”, „Close Bottom Sheet”). To oficjalne tłumaczenie z SDK
  (`material_pl.arb`); zmiana wymagałaby własnego delegata — poza zakresem, uwaga dla przeglądu.
- „Read aloud” w menu tekstu to akcja innej aplikacji Androida w języku systemu emulatora (angielski), nie Fluttera.
- Test `restore_screen_test.dart:213` (`find.byTooltip('Back')`) przestanie przechodzić → „Wstecz” (plan → *Scope diff*).
- AC-2 tylko testem: build debug na `Medium_Phone` wymagałby odinstalowania release (plan → *Manual verification*).

## Verification
> `qa`, 2026-10-08. Rytuał WZ-024: `dart format` (112 plików, 0 zmienionych) → `flutter analyze` (No issues found) →
> `flutter test` (**462 z 462**, wcześniej 458) → kroki ręczne.

### AC → tests
| AC | Test | Wynik |
|---|---|---|
| AC-1, D1 | `test/app_start_test.dart` → „ISSUE-021 AC-1, D1”: telefon po angielsku (`localesTestValue` en_US) → `Localizations.localeOf` = `pl`; `MaterialLocalizations`: „Wstecz”, „Wklej”, „Kopiuj”, „Zaznacz wszystko”, „Zamknij” | ✅ |
| AC-1 | `restore_screen_test.dart:213`: `byTooltip('Back')` → `'Wstecz'` (cała aplikacja, powrót ze „Stanu danych”) | ✅ |
| AC-2, D2 | nowy `test/dev/fictional_data_test.dart`: `addFictionalData` → Ojciec „Wymyślony”, Matka „Wymyślona” z d. „Zmyślona”, Dziecko „Wymyślone” | ✅ |
| AC-3 | `grave_photo_screens_test.dart` → „ISSUE-021 AC-3”: `isSemantics(isButton: true, hasTapAction: true)`; akcja z drzewa semantyki (`tester.semantics.tap`) otwiera arkusz „Zdjęcie nagrobka” | ✅ |
| AC-3 | `home_screen_test.dart` → „ISSUE-021 AC-3”: link `isSemantics(isLink: true, hasTapAction: true)`; akcja z drzewa otwiera ten sam adres (punkt, `basemap=satellite`) co dotknięcie | ✅ |
| AC-4 | README `grobing-code` → **Testy**: strumień drift i fałszywy zegar (ISSUE-014), zapis w `runAsync` przy podpiętym ekranie i `leaveScreen` (ISSUE-012), `_pumpUntil`, zablokowany `sqlite3.dll` i `flutter_01.log` | ✅ |

**Falsyfikacja testów AC-3:** oba testy uruchomione na wersji ekranów z `HEAD` (bez `onTap`) → **oba padają**
(`Expected: has semantics with actions: [tap]`); po przywróceniu zmian przechodzą. Test łapie błąd, który poprawia.

### Manual verification — kroki oddane agentowi (pozycja bez nowego ekranu, DoD → *Kto sprawdza*)
Agent na emulatorze `Medium_Phone`, build release wgrany na istniejące dane: *Dev report* → *Emulator pass*
(przed/po `clickable`, „Wstecz”, menu tekstu, dane bez zmian). **Autor — odczucie: brak kroków.**

### Family data in the changes
- `grobing-code`: tylko wymyślone osoby („Wymyślony/-a/-e”, „Zmyślona”, już w repo) i publiczny cmentarz z
  testów ISSUE-015. Bez plików baz, kopii, eksportów i zdjęć. `family_data_dir` nieczytany.
- `grobing-vault`: bez nazw osób i miejsc. Miejscowość, którą autor podał w czacie przy fakcie 5, nie trafiła do
  pozycji ani do macierzy (sprawdzone grepem).
- Ostatnia kontrola treści: strażnik przy `git add` (`docs`).

### Szukane i nieznalezione
- inne `Semantics` z `excludeSemantics` bez `onTap` w `lib/` — 5 sprawdzonych, poprawione 2 z pozycji;
- inne testy, które szukają angielskich tekstów Fluttera (`'Back'`, `'Close'`, `'Paste'`, `'Copy'`…) — był jeden;
- pusta pierwsza klatka po dodaniu lokalizacji — test startu bez dodatkowego `pump` przechodzi (delegaty ładują
  się synchronicznie);
- zmiana w `pubspec.lock` poza `flutter_localizations` i `intl` 0.20.2 (przyjęte przez autora) — brak.

### Uwagi (nie blokują)
1. **Czytnik ekranu czyta teraz tłumaczenia Fluttera**: tło pod arkuszem — „Siatka”, podpowiedź „Zamknij: Plansza
   dolna” (wcześniej „Scrim”, „Close Bottom Sheet”). Oficjalne `material_pl.arb`; zmiana tylko własnym delegatem.
2. **AC-2 bez emulatora** — tylko test (build debug wymagałby odinstalowania release).
3. **Switch Access i Voice Access nieuruchomione „w ręce”** — dowodem jest drzewo semantyki i `clickable` w dumpie
   Androida.
4. README: przyczyna zablokowanego `sqlite3.dll` (proces `flutter_tester.exe`) opisana jako „najpewniej” —
   niezmierzona.
5. **Kandydat do retro:** trzecia instancja tego samego wzorca semantyki (ISSUE-017 + te dwie) — test na źródłach
   albo reguła przeglądu `ui`, żeby czwartej nie było.
6. APK release +0,8 MB (teksty wszystkich języków z `flutter_localizations`).

### Verdict
**APPROVED** (self-check, z uwagami 1–6), 2026-10-08.

### Package for `docs` (jawna lista plików tej pozycji)
- `grobing-code`: `README.md`, `pubspec.yaml`, `pubspec.lock`, `lib/app/grobing_app.dart`, `lib/dev/fictional_data.dart`,
  `lib/app/grave/grave_screen.dart`, `lib/app/home/base_preview_screen.dart`, `test/app_start_test.dart`,
  `test/app/restore_screen_test.dart`, `test/app/photo/grave_photo_screens_test.dart`,
  `test/app/home/home_screen_test.dart`, `test/dev/fictional_data_test.dart` (nowy);
- `grobing-vault`: `backlog/issues/ISSUE-021-small-fixes-after-retro-2.md`, `00_START_HERE/TRACEABILITY.md` + pliki
  zamknięcia `docs` (`CURRENT_STATE.md`).
