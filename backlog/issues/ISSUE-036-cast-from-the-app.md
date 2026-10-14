---
title: "ISSUE-036 — Cast from the app: a button on the tree opens the system's screen-cast list, then presentation mode — one touch, as „Przesyłaj” in Google Photos"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-009-drzewo-od-osoby]]"
depends-on: "[[ISSUE-034-tree-presentation-mode]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-14
verdict-reviewer: self-check
source: "decyzja autora na stopie #2 [[ISSUE-034-tree-presentation-mode]] (2026-10-14: *„chciałem aby ten tryb telewizora streamował obraz do smart TV … jak w Youtube”*; rekomendacja `qa` przyjęta „tak”) · [[drzewo]] D11, D26"
created: 2026-10-14
updated: 2026-10-14
---

# ISSUE-036 — Przesyłaj z aplikacji

> Z zamknięcia [[ISSUE-034-tree-presentation-mode]] (`docs`, 2026-10-14). Autor chce wybierać telewizor z poziomu aplikacji, tak jak „Przesyłaj” w
> Zdjęciach Google. Tryb prezentacji (ISSUE-034) układa obraz, ale do przesyłania trzeba dziś szukać kafelka w szybkich ustawieniach.
> **Pozycja zmienia ekran → `ui` przed `planning`.**

## What to build
1. **Przycisk „Przesyłaj”** w drzewie (miejsce i ikona — `ui`; np. `cast` przy ikonie telewizora albo w trybie prezentacji), który otwiera
   **systemową listę przesyłania ekranu**. Zmierzone na emulatorze (Android 16, 2026-10-14): `Settings.ACTION_CAST_SETTINGS` otwiera ekran
   „Google Cast” z listą urządzeń w pobliżu (`com.android.settings/.Settings$WifiDisplaySettingsActivity`).
2. Po wyborze telewizora — tryb prezentacji (kolejność i to, czy przycisk sam włącza tryb, rozstrzyga `ui`).
3. **Bez kodu sieciowego:** obraz ekranu wysyła system ([[NFR-005-dane-nie-opuszczaja-telefonu]]); bez Google Cast SDK i bez odbiornika.

## Acceptance Criteria
- [ ] *When* dotykam „Przesyłaj” *Then* otwiera się systemowa lista urządzeń do przesyłania ekranu.
- [ ] Telefon bez tej listy (inny producent) *Then* aplikacja nie pada, a podpowiedź z trybu prezentacji mówi, gdzie szukać przesyłania ([[drzewo]] D26).

## Out of scope
- **Casting** — odbiornik Google Cast na telewizorze rysuje drzewo, telefon jest pilotem (jak YouTube, Zdjęcia): po MVP i tylko gdy przesyłanie
  ekranu nie wystarczy; wymaga ADR zmieniającego NFR-005, odbiornika na HTTPS i rejestracji Google Cast ([[ISSUE-034-tree-presentation-mode]] →
  *Verification* → *Stop #2*).
- Sprawdzenie z telewizorem autora → [[ISSUE-032-mvp-install]] → *Hand checks*.

## Notes
- Telewizor autora jest odbiornikiem Google Cast w tej samej sieci Wi-Fi (zrzut autora z Zdjęć, stop #2 ISSUE-034).
- Prior art do sprawdzenia przy planie: dokumentacja `Settings.ACTION_CAST_SETTINGS` (Android) i zachowanie na telefonach bez Google Cast (np. Samsung
  „Smart View”) — przy planie, ze źródłem.
- Kanał natywny: wzorzec `ExternalLinks` w `MainActivity.kt` (otwiera intencję z aktywności).

## Implementation plan
> `planning`, 2026-10-14. Specyfikacja: [[drzewo]] v1.10 — element 1 (ikona), element 11 (wejście, podpowiedź), *Navigation*, *States*, *AC → element*,
> *Candidates — ISSUE-036*, D29, **⚠️ *Open* 7 (P1 / P2 / P3 — na ten stop)**; [[style-b]] v1.28 (reguły 1, 3). Makieta wariantów ze zrzutami z emulatora:
> `drzewo-036.html` (katalog tymczasowy sesji `fa865b36-…\scratchpad`, zrzuty w `shots-036\`). **Plan jest pisany pod rekomendację P2**; co się zmienia przy
> P1 i P3 — na końcu sekcji.

### Stop #1 (2026-10-14) — autor: „tak”
P2 i D0–D4 przyjęte ([[drzewo]] D30, *Open* 7 zamknięte). Sekcja *If the author picks P1 or P3* zostaje jako zapis odrzuconych wariantów.

### Prior art (źródła, nie pamięć)
- **Co aplikacja może otworzyć** — [[drzewo]] D29: `Settings.ACTION_CAST_SETTINGS` (źródła SDK 36, `Settings.java`: *„In some cases, a matching Activity
  may not exist, so ensure you safeguard against this”*); samo przesyłanie włącza system (`MediaRouter.java`: trasa „remote display” jest `@hide`, uprawnienie
  systemowe `CONFIGURE_WIFI_DISPLAY`). Pomiar 2026-10-14: na `Grobing_Restore` akcja otwiera `com.android.settings/.Settings$WifiDisplaySettingsActivity`.
- **Jak aplikacja wie, że użytkownik wrócił** — `Activity.java` (źródła SDK 36) przy `startActivityForResult`: *„this method should only be used with Intent
  protocols that are defined to return a result … if the activity you are launching uses FLAG_ACTIVITY_NEW_TASK, it will not run in your task and thus you
  will immediately receive a cancel result”*. Ekran ustawień przesyłania nie oddaje wyniku, a ma `taskAffinity=com.android.settings`. Wynik z
  `onActivityResult` mógłby więc przyjść od razu, a tryb prezentacji włączyłby się pod ekranem ustawień. Dlatego D1 korzysta z cyklu życia aplikacji.
- **Z kodu:** `ExternalLinks.kt` + `lib/app/external_link.dart` (kanał `grobing/external`: otwiera inną aplikację po dotknięciu, `ActivityNotFoundException` →
  `false`), `TreeScreen._present()` / `_leave()` / `_flash()` i `presentation_mode.dart` ([[ISSUE-034-tree-presentation-mode]]), wzorzec wyniku okna systemu w
  `BackupDocuments.kt` (tu odrzucony — wyżej).

### Decisions for stop #1 (rekomendacja → „tak” przyjmuje wszystkie)
- **D0 — wariant wejścia: P2** ([[drzewo]] *Open* 7). Jedna ikona `cast_outlined` „Przesyłaj na telewizor” **zamiast** `tv_outlined` „Tryb prezentacji”: ekran
  systemu, a po powrocie tryb prezentacji bez podpowiedzi. **Nie da:** trybu bez telewizora jednym dotknięciem (ikona i wstecz).
- **D1 — powrót z ekranu systemu po cyklu życia aplikacji, nie po wyniku okna.** Dotknięcie otwiera ekran przez `startActivity` (jak link). Gdy aplikacja
  po schowaniu znów jest na wierzchu (`AppLifecycleListener`: `onHide`, a potem `onResume`), drzewo włącza tryb prezentacji. Czekanie kończy się po jednym
  wejściu albo po zamknięciu ekranu drzewa. **Krok 0 `dev` (przed resztą):** pomiar na `Grobing_Restore`, czy ekran ustawień staje w zadaniu aplikacji, jaka
  jest kolejność stanów cyklu życia i czy po wstecz tryb włącza się dokładnie raz. Wynik idzie do *Dev report*. Gdy cykl życia zawiedzie, `dev` mierzy
  `startActivityForResult` i bierze to, co działa. Zakres się nie zmienia. **Nie da:** rozróżnienia „wybrałem telewizor” i „wróciłem bez wyboru” (D29). Kto z
  ekranu systemu przejdzie do innej aplikacji i wróci do Grobinga z ostatnich, też trafi do trybu prezentacji.
- **D2 — telefon bez ekranu przesyłania** (AC-2): `ActivityNotFoundException`, brak kanału albo błąd → od razu tryb z podpowiedzią D26 (tekst bez zmian).
  Aplikacja nie pada.
- **D3 — drugie dotknięcie w trakcie otwierania** nie otwiera drugiego ekranu: flaga czekania w `TreeScreen`, ikona nieaktywna do powrotu.
- **D4 — czytnik:** `tooltip` „Przesyłaj na telewizor”, opis dla czytnika „Przesyłaj na telewizor — w ustawieniach telefonu” (jak „…, w innej aplikacji” w
  `base_preview_screen.dart`). Ikona się nie zmienia w czasie przesyłania (D29).

### Scope — files (`{code}`)
| Plik | Zmiana |
|---|---|
| `android/app/src/main/kotlin/com/grobing/app/ExternalLinks.kt` | metoda `openCastSettings` na istniejącym kanale: `start(Intent(Settings.ACTION_CAST_SETTINGS))`, `ActivityNotFoundException` → `false`. Bez nowego kanału, uprawnienia i `<queries>` (sam `startActivity` ich nie potrzebuje, jak przy linku) |
| `lib/app/external_link.dart` | `Future<bool> openCastSettings()` — `PlatformException` / `MissingPluginException` → `false` (jak `openExternalUrl`) |
| `lib/app/tree/tree_screen.dart` | w pasku `cast_outlined` zamiast `tv_outlined` (akcent, 48 dp, `tooltip`, opis D4), tylko gdy jest drzewo; `_cast()`: otwarcie (D3) → czekanie na powrót (D1) → `_present(hint: false)`; `false` → `_present(hint: true)` (D2). `_present` dostaje parametr podpowiedzi; komentarz „the hint … on every entry” poprawiony. Tryb prezentacji, wyjście i wstecz bez zmian (ISSUE-034) |
| `lib/app/tree/presentation_mode.dart` | tylko komentarz („Przesyłaj ekran” → ekran przesyłania systemu), jeśli `dev` uzna za potrzebny |

`AndroidManifest.xml`, `pubspec.yaml`, schemat — bez zmian. Testy (pisze `qa`): `test/app/tree/tree_screen_test.dart` (rozszerzony; testy, które dziś
dotykają „Tryb prezentacji”, przechodzą na nową ikonę), `test/app/external_link_test.dart` (nowy albo rozszerzony).

### AC → implementation → test (testy pisze `qa`)
| AC | Implementacja | Test happy-path |
|---|---|---|
| AC-1 — „Przesyłaj” otwiera systemową listę | ikona → `openCastSettings` → powrót → `_present(hint: false)` | wymyślona rodzina: dotknięcie ikony → kanał `grobing/external` dostaje `openCastSettings`; przed powrotem drzewo bez zmian; cykl życia `hidden` → `resumed` → tryb prezentacji (bez paska „Drzewo”, karty, + / −), **bez** tekstu podpowiedzi; drugie dotknięcie przed powrotem → jedno wywołanie (D3) |
| AC-2 — telefon bez listy | `false` z kanału albo wyjątek → `_present(hint: true)` | kanał odpowiada `false` → od razu tryb z podpowiedzią „Obraz na telewizor: …”, po 4 s jej nie ma; `MissingPluginException` → to samo, bez wyjątku w teście |
| Element 1 — ikona | `_bar` | pusta baza i brak „ja” → ikony nie ma; `meetsGuideline(androidTapTargetGuideline)` i `labeledTapTargetGuideline` na ikonie (retro 3, R2); opis dla czytnika z D4; ikony `tv_outlined` już nie ma |
| AC-8 US-009 — tryb bez zmian | — | regresja: wyjście pustym dotykiem i wstecz jak w ISSUE-034 (istniejące testy, wejście przez nową ikonę) |

### Data layer
- **Bez zmian:** ekran tylko czyta, schemat zostaje. Nie ma migracji ani próbnego odtworzenia z kopii.
- **Bez sieci** ([[NFR-005-dane-nie-opuszczaja-telefonu]], D11): aplikacja otwiera ekran ustawień, a obraz wysyła system. Tę drogę autor przyjął w D11. Bez nowej
  zależności i uprawnienia. `qa` sprawdza, że `AndroidManifest.xml` i `pubspec.lock` się nie zmieniły (`aapt` na APK bez nowych uprawnień).

### Manual verification
**Agent na emulatorze** — przed stopem #2, ze zrzutami (`Grobing_Restore`, build profile, wymyślona rodzina ze stanu po ISSUE-035):
0. (`dev`, przed budową) pomiar D1: zadanie ekranu ustawień (`dumpsys activity activities`), kolejność cyklu życia, jedno wejście w tryb po wstecz.
1. AC-1: ikona → na wierzchu `WifiDisplaySettingsActivity` (zrzut); wstecz → poziomo, bez podpowiedzi (zrzut).
2. D3: dwa szybkie dotknięcia ikony → jeden ekran ustawień, po wstecz jedno wejście w tryb.
3. AC-2: wyłączenie komponentu ustawień poleceniem `pm disable-user --user 0 com.android.settings/.Settings\$WifiDisplaySettingsActivity`, a po kroku
   `pm enable`. Wtedy dotknięcie → od razu tryb z podpowiedzią, aplikacja żyje. Gdy powłoka nie może wyłączyć komponentu, krok pokrywa test widgetu z AC-2.
   Ta luka będzie nazwana wprost w *Verification*.
4. D1, „nie da”: ekran ustawień → Home → powrót do Grobinga z ostatnich → tryb prezentacji (zapisane, jak się zachowuje).
5. Tekst 200% na 360 dp: ikona 48 dp w pasku, `uiautomator dump` — opis z D4; regresja wyjścia z trybu (pusty dotyk, wstecz).
6. Logcat procesu aplikacji bez nowych wpisów; `aapt` — uprawnienia bez zmian.

**Autor: odczucie** (najwyżej 3 kroki, emulator `Grobing_Restore`):
1. W zakładce Drzewo dotknij ikonę przesyłania. Otworzy się ekran telefonu „Google Cast”, pusty, bo emulator nie widzi telewizora. Wróć wstecz, a drzewo
   przejdzie w tryb prezentacji. Czy ta droga jest dla Ciebie oczywista jako „pokaż na telewizorze”, a ikona w pasku czytelna?

### Out of Scope
- **Casting** (telewizor sam rysuje drzewo, telefon jako pilot) — po MVP, ADR zmieniający NFR-005 (*Out of scope* wyżej).
- Okienko z listą telewizorów nad drzewem jak w Zdjęciach — wymaga Google Cast (D29).
- Ikona „przesyłanie trwa” (`cast_connected`) — aplikacja nie wie, czy przesyłanie trwa (D29).
- Ekran przesyłania na telefonie innego producenta (np. Samsung) i to, co system pokaże po wyborze telewizora (zgoda, „cały ekran / jedna aplikacja”) →
  [[ISSUE-032-mvp-install]] → *Hand checks* (`docs` przy zamknięciu: telewizor autora na liście ekranu systemu · co system pyta po wyborze · drzewo poziomo na
  telewizorze · jednorazowe okno systemu „pełny ekran” na telewizorze, D16).
- „Połącz dwie osoby” w pasku → [[US-011-polacz-dwie-osoby]].

### If the author picks P1 or P3 (stop #1)
- **P1** (dwie ikony): `tv_outlined` zostaje z `_present(hint: true)`, a `cast_outlined` dochodzi na lewo od niej. Reszta planu bez zmian, plus test, że obie ikony
  działają. `ui` zmienia element 1 i *Navigation* w [[drzewo]] przed `dev`.
- **P3** (przesyłanie z trybu): ikona telewizora zostaje, a w trybie podpowiedź staje się przyciskiem „Przesyłaj ›” i „Przesyłaj” stoi obok „Zakończ prezentację”.
  Dochodzi powrót z ekranu ustawień do trybu poziomego, czyli obrót w trakcie (pomiar jak D1 w ISSUE-034), oraz cel dotyku w pigułce, która dziś go nie ma (D26).
  To ok. 1,5 raza więcej pracy. `ui` przepisuje element 11 przed `dev`.

## Dev report
> `dev`, 2026-10-14. Flutter 3.41.1. Build profile z `--dart-define=FRAME_LOG=true` na `Grobing_Restore` (Android 16, system po angielsku), wymyślona
> rodzina ze stanu po ISSUE-035. `flutter analyze` — czysto; `dart format` — zrobione; `flutter test` — **724 zielone, 3 czerwone**. Czerwone to trzy
> testy AC-8 w `tree_screen_test.dart`, które dotykają ikony „Tryb prezentacji” (`tv_outlined`), a tej już nie ma (D0). Przepina je `qa`.

### Krok 0 — pomiar D1 (przed resztą)
- **Ekran ustawień staje w zadaniu aplikacji:** po dotknięciu `dumpsys activity`: zadanie #76 — `Hist #1 com.android.settings/.Settings$WifiDisplaySettingsActivity`,
  `Hist #0 com.grobing.app/.MainActivity` (`STOPPED`). Ostrzeżenie z `Activity.java` (wynik „cancelled” od razu) na emulatorze się nie spełnia, ale cykl
  życia i tak zostaje: nie zależy od tego, czy ekran ustawień jakiegoś producenta otworzy się w innym zadaniu.
- **Kolejność stanów Fluttera** (tymczasowy log, usunięty):
  - zostajesz na ekranie ustawień: `inactive` → po ok. 1,2 s `hidden` → `paused` · wstecz: `hidden` → `inactive` → `resumed`;
  - **wstecz po ok. 1 s: `inactive` → `resumed`, bez `hidden`.** Android zatrzymuje aplikację pod nowym ekranem dopiero po chwili.
  - Dlatego sygnałem jest `inactive` → `resumed`, a nie `hidden` → `resumed` z planu (odstępstwo 1).
- **Powrót z ekranu głównego:** ekran ustawień → Home → Grobing z ikony pokazuje znowu ekran ustawień (to samo zadanie). Dopiero wstecz włącza tryb. „Nie da” z
  D1 („kto przejdzie do innej aplikacji i wróci, trafi do trybu”) jest więc łagodniejsze: wraca najpierw do ekranu ustawień.

### What was built (`{code}`)
- **`android/.../ExternalLinks.kt`** — metoda `openCastSettings` na kanale `grobing/external`: `startActivity(Intent(Settings.ACTION_CAST_SETTINGS))`,
  `ActivityNotFoundException` → `false`. Bez nowego kanału, uprawnienia i `<queries>`.
- **`lib/app/external_link.dart`** — `openCastSettings()`; `PlatformException` / `MissingPluginException` → `false`.
- **`lib/app/tree/tree_screen.dart`:**
  - w pasku `cast_outlined` (akcent, `tooltip` „Przesyłaj na telewizor”) zamiast `tv_outlined`. Czytnik słyszy „Przesyłaj na telewizor — w ustawieniach
    telefonu”, a węzeł ma własne dotknięcie (wzorzec linku zewnętrznego, ISSUE-021);
  - `_cast()`: `AppLifecycleListener` założony przed otwarciem → `inactive`, potem `resumed` → `_present(hint: false)`. `false` z kanału →
    `_present(hint: true)` (AC-2). Drugie dotknięcie w trakcie czekania nic nie robi (D3);
  - `_present({required bool hint})` — podpowiedź D26 tylko przy `hint`. Słuchacz zwalniany po powrocie albo w `dispose`. Tryb, wyjście i wstecz bez zmian.
- `AndroidManifest.xml`, `pubspec.yaml`, `pubspec.lock`, schemat — bez zmian.

### Deviations (do przeglądu `ui`)
1. **Powrót rozpoznawany po `inactive` → `resumed`, nie po `hidden` → `resumed`** (D1, krok 0). Skutek uboczny: gdyby ekran ustawień otworzył się obok aplikacji
   (podzielony ekran), tryb włączy się, gdy wrócisz palcem do Grobinga. Nie ma już bezpiecznika 2 s, który był w pierwszej wersji (znalezisko a).
2. **D3 bez wyszarzenia ikony:** drugie dotknięcie jest pomijane w kodzie, a ikona wygląda tak samo. Wyszarzenie mignęłoby na ułamek sekundy przed ekranem
   ustawień.

### Found on the emulator (przejście AC przed `qa`, R5) — poprawione
- (a) **Pierwsza wersja miała bezpiecznik 2 s na podzielony ekran** (bez `hidden` w 2 s → koniec czekania). Na emulatorze `hidden` przyszło dopiero po ponad 2 s,
  więc słuchacz był już zwolniony i po wstecz trybu nie było (zrzut `12`). Poprawka: odstępstwo 1, bez bezpiecznika.

### AC pass on the emulator (zrzuty: katalog tymczasowy sesji `fa865b36-…\scratchpad\shots-036\`)
| Co | Wynik | Zrzut |
|---|---|---|
| Ikona w pasku, 100% | `cast_outlined` w akcencie; `uiautomator`: „Przesyłaj na telewizor — w ustawieniach telefonu”, `clickable=true`, 127 × 126 px = 48 dp | `10`, `16` |
| AC-1: ikona → ekran systemu | na wierzchu `WifiDisplaySettingsActivity` w zadaniu aplikacji | `11` |
| AC-1: długo na ekranie → wstecz | poziomo, tryb bez podpowiedzi | `13` |
| AC-1: wstecz po ok. 1 s | poziomo (2400 × 1080), tryb bez podpowiedzi | `14` |
| D3: dwa dotknięcia co 0,15 s | jeden ekran ustawień w zadaniu, po wstecz jedno wejście w tryb | — |
| AC-2: brak ekranu przesyłania | powłoka nie może wyłączyć komponentu ustawień (`SecurityException`; `adb root` — „cannot run as root in production builds”). Zamiast tego **jednorazowa sonda**: build z nieistniejącą akcją → aplikacja żyje, tryb od razu z podpowiedzią. Sonda cofnięta przed buildem końcowym | `15` |
| Tekst 200%, 360 dp | ikona 96 × 96 px przy gęstości 2,0 = 48 dp; ekran systemu → wstecz → tryb bez podpowiedzi; wyjście przyciskiem „Zakończ prezentację” i wstecz → pion | `17`–`21` |
| Home w trakcie | powrót do aplikacji pokazuje ekran ustawień, wstecz → tryb | `22` |
| Log procesu aplikacji | tylko wpisy systemu (`ImeTracker`, `BLASTBufferQueue` przy obrocie), nic z aplikacji | — |

Pomiar klatek — nie dotyczy (bez nowej warstwy ani danych). Stany „pusta baza” i „„ja” niewybrane” — warunek ikony bez zmian (`_treeShown`), do testu `qa`.

### Manual verification — for `qa`
Kroki agenta z planu (0–6) zrobione wyżej, poza `aapt` na APK — to zostaje dla `qa`. Krok autora bez zmian: ikona przesyłania → ekran „Google Cast” → wstecz → tryb
prezentacji; czy droga jest oczywista jako „pokaż na telewizorze”.

## Verification
> `qa`, 2026-10-14. Rytuał WZ-024: `dart format --set-exit-if-changed lib test` — bez zmian · `flutter analyze` — czysto · `flutter test` — **728 zielonych**
> (pierwszy pełny przebieg zawisł raz na jednym procesie `flutter_tester` po 13 min, bez wskazania testu; drugi z `--timeout 120s` przeszedł w 1:25 —
> zapisane jako obserwacja, nie usterka).

### Tests (`{code}/test/app/tree/tree_screen_test.dart`)
| AC | Test | Wynik |
|---|---|---|
| AC-1 + AC-8 | „Przesyłaj na telewizor” → kanał `grobing/external` dostaje `openCastSettings` raz, także po drugim dotknięciu (D3); dopóki aplikacja nie wróci, drzewo bez zmian i bez obrotu; cykl życia `inactive` → `resumed` → poziomo, bez paska, karty, + / −, 20 osób w kadrze **bez podpowiedzi**; ikona `cast_outlined`, brak `tv_outlined`; czytnik „Przesyłaj na telewizor — w ustawieniach telefonu” z akcją dotknięcia; `meetsGuideline` (oba) i `expectEveryButtonTappable` w trybie | ✅ |
| AC-2 | kanał odpowiada `false` → od razu tryb z podpowiedzią, po 4 s jej nie ma; wstecz → pion; błąd po stronie natywnej (`PlatformException`) → to samo, nic nie wyjątkuje | ✅ |
| Element 1 — stany | pusta baza i brak „ja” → ikony nie ma | ✅ |
| AC-8 — regresja | wyjście „Zakończ prezentację” i wstecz → pion, ta sama osoba; drugie wejście przez ekran systemu z pełnym cyklem (`hidden` / `paused`) | ✅ |
| Tap targets (R2) | AC-1 ISSUE-033 (pion, pasek z nową ikoną) i AC-1 tej pozycji (tryb) | ✅ |

Plan wymieniał `test/app/external_link_test.dart` — niepotrzebny: `openCastSettings()` (odpowiedź, `false`, `PlatformException`) pokrywają testy ekranu przez ten
sam kanał.

### Emulator (`Grobing_Restore`, build profile; zrzuty w katalogu tymczasowym sesji `fa865b36-…\scratchpad\shots-036\`)
- Przejście `dev` (*Dev report* → *AC pass*) sprawdzone na urządzeniu. Dodatkowo:
  - **brak podpowiedzi zaraz po powrocie:** `uiautomator dump` ok. 1,5 s po wstecz — 0 wystąpień „Obraz na telewizor”, zrzut `23` (przegląd `ui`, MINOR 1: zrzuty `13`
    i `14` nie odróżniały „nie było” od „zgasła”);
  - **przejście po powrocie** (nagranie `r036.mp4`, log klatek `FRAME_LOG`): ekran ustawień znika ok. 1 s (animacja systemu), obrót, a przez chwilę widać poziomy ekran
    z drzewem jeszcze niedopasowanym. Log: od wstecz do dopasowanego trybu ok. 1,1 s. Pierwsze klatki po powrocie rasteryzują się 64–100 ms (zwykle kilka ms): po
    zatrzymaniu aplikacji Android każe zwolnić pamięć grafiki (`onTrimMemory`), więc drzewo odbudowuje się w trakcie obrotu. Wejście bezpośrednie (sonda AC-2,
    nagranie `r036b.mp4`) dopasowuje się po obrocie w ok. 0,8 s, bez tej chwili. **Obserwacja, nie usterka:** koszt powrotu z innej aplikacji, na emulatorze bez
    sprzętowego GPU telefonu; na telefonie → *Hand checks*.
- **NFR-005:** `AndroidManifest.xml`, `pubspec.yaml`, `pubspec.lock` — bez zmian (`git diff`), więc `aapt` niepotrzebny; kod sieciowy nie doszedł (`ExternalLinks.kt` otwiera
  tylko ekran ustawień). Log procesu aplikacji: tylko wpisy systemu.
- **Dane rodziny w zmianach:** w kodzie i testach tylko wymyślona rodzina (`Wymyślony`, `Wymyślona`, `Przykładowa` — rdzenie jawnie wymyślone); w vaulcie bez imion i
  nazwisk spoza przykładów; zrzuty, nagrania i log poza repo.

### `ui` review (subagent, 2026-10-14)
0 BLOCKER, 0 MAJOR, 2 MINOR:
1. Zrzuty `13`/`14` bajtowo równe `04` (sprzed budowy) — nie dowodzą braku podpowiedzi → **zamknięte:** zrzut `23` i `uiautomator` (wyżej) oraz test AC-1.
2. Komentarze w kodzie z nazwą „Przesyłaj ekran” (`tree_screen.dart`, `presentation_mode.dart`) → **poprawione** (`dev`): „casting from the quick settings — only on a phone
   without the system's cast screen (D26, D30)” i „the system's own screen cast (D29)”.

Odstępstwa `dev` 1 (`inactive` → `resumed`) i 2 (D3 bez wyszarzenia) **przyjęte** → [[drzewo]] v1.11 (*Navigation*, element 1, D30 a/b).
Zgodne: element 1 (akcent, `tooltip`, opis, 48 dp przy 100% i 200%), stany, regresja elementu 11, kontrast z `theme.dart` (8,81 · 8,04 · 10,02 · 3,40 · 10,98:1), role
koloru, ton, brak danych rodziny na zrzutach.

### Stop #2 (2026-10-14) — autor: „ok”
Dwa kroki odczucia na `Grobing_Restore`: (1) ikona przesyłania → ekran „Google Cast” → wstecz → tryb prezentacji, z pytaniem o oczywistość drogi, czytelność ikony
i chwilę przejścia; (2) wyjście z trybu. **Ślad na urządzeniu dla obu** (logcat, czas emulatora): `START … CAST_SETTINGS` 13:53:17 → obrót do poziomu 13:53:20 → powrót
do pionu 13:53:25.

**Werdykt `qa`: APPROVED (self-check, z uwagami)** — uwagi: przejście po powrocie z ekranu systemu (ok. 1,1 s, chwila niedopasowanego drzewa) i jednorazowe zawieszenie
pełnego przebiegu testów (wyżej); wszystko, czego emulator nie sprawdzi, na liście niżej.

### Not tested live — for [[ISSUE-032-mvp-install]] → *Hand checks*
- telewizor autora na liście systemowego ekranu przesyłania (emulator nie widzi żadnego);
- co system pokazuje po wyborze telewizora (zgoda, „cały ekran / jedna aplikacja”) i czy drzewo staje poziomo na telewizorze;
- jednorazowe okno systemu o pełnym ekranie — czy trafia na telewizor przy pierwszym pokazie (D16);
- ekran przesyłania na telefonie innego producenta (np. Samsung — czy jest i czy widzi telewizor Google Cast; D29 *Obali*);
- przejście po powrocie z ekranu systemu na telefonie (na emulatorze ok. 1,1 s z chwilą niedopasowanego drzewa).
