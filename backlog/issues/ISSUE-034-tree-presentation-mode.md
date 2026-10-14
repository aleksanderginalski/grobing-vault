---
title: "ISSUE-034 — Tree presentation mode for a TV: landscape, full screen, level 2 fitted, no buttons; the TV icon in the tree's bar; the system „Przesyłaj ekran” sends the picture"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-009-drzewo-od-osoby]]"
depends-on: "[[ISSUE-033-tree-from-a-person]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-14
verdict-reviewer: self-check
source: "rozpisanie US-009 (`docs` w auto-flow po `pm` i `ui`, autor: „ok”, 2026-10-13) · US-009 AC-8 · [[drzewo]] v1.5 (element 1 — ikona, element 11; D11, D16)"
created: 2026-10-13
updated: 2026-10-14
---

# ISSUE-034 — Tryb prezentacji drzewa

> Z rozpisania [[US-009-drzewo-od-osoby]] (`docs` w auto-flow, 2026-10-13). Druga z dwóch pozycji US-009 — buduje się na drzewie z
> [[ISSUE-033-tree-from-a-person]]. Podział zaproponował łańcuch, nie autor, więc na stopie #1 ISSUE-033 autor może go zmienić.

## What to build
1. **Ikona „Tryb prezentacji”** w pasku drzewa ([[drzewo]] element 1): `tv_outlined`, akcent, `tooltip`, cel 48 dp; bez niej w stanach bez
   drzewa.
2. **Tryb prezentacji** ([[drzewo]] element 11, D11, D16): poziomo, pełny ekran, poziom 2 dopasowany do ekranu, bez przycisków;
   podpowiedź o „Przesyłaj ekran” przy wejściu; dotknięcie osoby — ona w środku; dotknięcie pustego miejsca — na 3 s „Zakończ
   prezentację”; wstecz też kończy; po wyjściu orientacja i paski systemu wracają.
3. **Bez Google Cast i bez kodu sieciowego** — obraz na telewizor daje systemowe „Przesyłaj ekran” ([[NFR-005-dane-nie-opuszczaja-telefonu]]).

## Acceptance Criteria
- [ ] **US-009 AC-8 — tryb prezentacji.** *When* włączam tryb prezentacji *Then* drzewo jest poziomo, na pełnym ekranie, na poziomie 2, bez
      przycisków; obraz na telewizor daje systemowe „Przesyłaj ekran”.
- [ ] Wyjście (dotknięcie pustego miejsca → „Zakończ prezentację”, albo wstecz) przywraca orientację pionową, paski systemu i tę samą osobę
      w środku.

## Out of scope
- Google Cast i odbiornik na telewizorze ([[drzewo]] D11 — kod sieciowy i dane rodziny w sieci lokalnej).
- Oddalanie w trybie prezentacji (D16: poziom stały).
- Sprawdzenie z telewizorem autora („Przesyłaj ekran”, D11 → *Obali*) — tylko na telefonie → [[ISSUE-032-mvp-install]] → *Hand checks*.

## Notes
- Zależy od [[ISSUE-033-tree-from-a-person]] (ekran drzewa, układ, dopasowanie poziomu do ekranu).
- Emulator nie przesyła obrazu na telewizor; orientację, pełny ekran i wyjście sprawdzi agent na emulatorze.

## Implementation plan
> `planning`, 2026-10-14. Specyfikacja: [[drzewo]] v1.7 — element 1 (ikona), element 11, *States* („tryb prezentacji”), D11, D16, *Style B
> rules applied* (tryb prezentacji); [[style-b]] v1.27. Makieta: `drzewo-us009.html` (katalog tymczasowy sesji `c3868f5f-…`, tryb
> prezentacji). Pozycja nie zmienia specyfikacji, więc `pm` skierował od razu do `planning`. Wygląd rozstrzygnęły D11 i D16, więc tym razem
> nie ma kandydatów do wyboru (retro 2, R6).

### Stop #1 (2026-10-14) — autor: „tak” dla planu, a przy okazji zmiana dwóch decyzji ISSUE-033
Autor otworzył makietę `drzewo-us009.html` (dopiero z adresem `file:///`, bo ścieżka z `%TEMP%` nie otwiera się w przeglądarce) i odpowiedział
na jej sekcję „Pytania do Ciebie”: **1 — I1** (imiona maleją razem z drzewem), **2 — „Moja babcia”** (G2), **3 — tak**. Odpowiedzi 1 i 2
zmieniają decyzje ze stopu #1 [[ISSUE-033-tree-from-a-person]] (I2, G1), które są już zbudowane i zamknięte. **Decyzja autora („tak”,
2026-10-14): osobna pozycja zaraz po tej.** Ta pozycja zostaje przy I2 i G1. **Dla `docs` przy zamknięciu:** założyć pozycję „drzewo: I1 i
„Moja”” — łańcuch `ui` ([[drzewo]] *Open* 5 i 6, [[style-b]] reguła 13 z odstępstwem od 13 sp, zdanie zamiast „to Ty” i „…dla Ciebie”, baner 9
US-011, przykład w AC-5 US-009) → `planning`. D1–D6 tego planu przyjęte, a nazwa kafelka (D6) zostaje według specyfikacji.
**Do retro (dla `docs`):** makieta podana jako ścieżka z `%TEMP%` się nie otwiera, więc „Tak” na stopie #1 ISSUE-033 mogło zapaść bez makiety.

### Prior art (źródła, nie pamięć)
- **Pełny ekran na Androidzie:** [Android — Hide system bars for immersive mode](https://developer.android.com/develop/ui/views/layout/immersive):
  *„Some examples are videos, games, image galleries, books, and presentation slides”*. Paski chowa `WindowInsetsControllerCompat.hide(systemBars())`,
  a `BEHAVIOR_SHOW_TRANSIENT_BARS_BY_SWIPE` pokazuje je na chwilę po przeciągnięciu od krawędzi i sam je chowa. We Flutterze to
  `SystemUiMode.immersiveSticky`. `leanBack` odpada: tam dotknięcie ekranu pokazuje paski i nie trafia do aplikacji, a w trybie dotknięcia
  przestawiają osoby.
- **Ryzyko — źródła się nie zgadzają (sprawdzone 2026-10-14):** Flutter 3.41.1 buduje z `targetSdkVersion = 36`
  (`flutter_tools/gradle/.../FlutterExtension.kt`). Dokumentacja `SystemUiMode` w SDK (`services/system_chrome.dart`) mówi przy `immersive`,
  `immersiveSticky` i `leanBack`: *„If your app targets Android SDK 16 (API 36) or later, then the Android system will ignore this value”*.
  Silnik (`PlatformPlugin.java`, tag 3.41.1) chowa paski starymi flagami `View.setSystemUiVisibility` (`SYSTEM_UI_FLAG_IMMERSIVE_STICKY`), a nie
  przez `WindowInsetsControllerCompat`. Dokumentacja Androida nie wspomina o takim ograniczeniu, a strona Fluttera o edge-to-edge
  ([breaking change](https://docs.flutter.dev/release/breaking-changes/default-systemuimode-edge-to-edge)) dotyczy tylko rezygnacji z rysowania pod
  paskami. Rozstrzyga pomiar: krok 0 `dev`, D1. Emulatory mają Androida 36.1, więc to ten sam przypadek.
- **Orientacja:** `SystemChrome.setPreferredOrientations`. Aplikacja dziś nigdzie nie ustawia orientacji ani trybu pasków (`grep` w `lib/`).
  `MainActivity` ma w manifeście `configChanges` z `orientation|screenSize`, więc obrót nie tworzy aktywności od nowa, tylko Flutter dostaje nowy rozmiar.
- **Z kodu** ([[ISSUE-033-tree-from-a-person]]): `TreeScreen` (`lib/app/tree/tree_screen.dart`) — `_relayout`, `_centreOn`, `_keepInView` (D21),
  poziom ze skali w `_onView` (S2), podwójne dotknięcie z surowych zdarzeń (`_pointerUp`), pigułka `_levelPill` z `liveRegion`. Nowy rozmiar
  przed pierwszym dotknięciem ustawia środek od nowa (`_touched`). Wstecz przechwytuje `PopScope` (wzorzec: `home_screen.dart`), a kanały
  natywne są w `android/app/src/main/kotlin/com/grobing/app/` (`ExternalLinks`, `HereLocation`).

### Decisions for stop #1 (rekomendacja → „tak” przyjmuje wszystkie)
- **D1 — jak schować paski (krok 0 `dev`, przed resztą):** najpierw `SystemChrome.setEnabledSystemUIMode(SystemUiMode.immersiveSticky)` na
  `Grobing_Restore`. Jeśli paski znikają, tak zostaje. **Jeśli zostają** — mały kanał natywny `SystemBars.kt`
  (`WindowInsetsControllerCompat.hide(systemBars())` z `BEHAVIOR_SHOW_TRANSIENT_BARS_BY_SWIPE`, jak w dokumentacji Androida), bez nowej
  zależności (`androidx.core` przychodzi z `androidx.work`). Wynik pomiaru `dev` zapisuje w *Dev report*. Zakres się nie zmienia, tylko droga
  do niego.
- **D2 — orientacja po wyjściu:** wraca **ustawienie systemu** (`setPreferredOrientations([])`), poprzedzone na chwilę pionem, bo bez tego
  ekran może zostać poziomo do najbliższego obrotu (do sprawdzenia w kroku 0). Przy wyłączonym autoobracaniu drzewo wraca pionowo, jak mówi
  AC. **Nie** blokujemy całej aplikacji w pionie: to zmiana wszystkich ekranów i osobna decyzja. *Obali:* po wyjściu przy wyłączonym
  autoobracaniu ekran zostaje poziomo.
- **D3 — tryb w tym samym ekranie, nie osobny:** flaga w `_TreeScreenState`. Ten sam układ, węzły, animacja przestawienia i nazwy, a „ta sama
  osoba w środku” po wyjściu przychodzi sama. Osobny ekran wymagałby wyjęcia rysowania (ok. 400 linii) z `tree_screen.dart`. *Obali:*
  `tree_screen.dart` z trybem przestaje się dać czytać — wtedy wyjęcie rysowania jako osobna pozycja.
- **D4 — „dopasowany do ekranu”:** cały poziom 2 mieści się w obszarze bezpiecznym (poza wycięciem aparatu) z marginesem 24 dp, a skala
  mieści się w granicach drzewa 0,4–2,0 (D17, D18). Gdy poziom 2 przy 0,4 jest szerszy niż ekran (tekst 200%, duża rodzina), resztę
  odsłania przeciąganie, a drzewo wraca, gdy ucieknie (D21). Na `Grobing_Restore` poziomo (914 × 411 dp) od „Ja” wychodzi ok. 0,9, czyli
  wszyscy z imionami.
- **D5 — dotknięcie osoby, która już jest w środku:** w prezentacji nic się nie dzieje. Poza prezentacją drugie dotknięcie otwiera widok
  osoby, ale tryb nie ma karty ani „Pokaż” (element 11), a widok osoby w pionie przerwałby pokaz. Specyfikacja nie mówi tego wprost; wynika
  to z „bez przycisków”.
- **D6 — nazwa kafelka w podpowiedzi:** tekst ze specyfikacji („Obraz na telewizor: „Przesyłaj ekran” w szybkich ustawieniach Androida”).
  Nazwa kafelka zależy od telefonu (np. u Samsunga „Smart View”). Agent sprawdzi polską nazwę na emulatorze. Inna nazwa na telefonie autora
  → `ui` poprawia jedną linię w [[drzewo]] (element 11).

### Scope — files (`{code}`)
| Plik | Zmiana |
|---|---|
| `lib/app/tree/tree_screen.dart` | **ikona „Tryb prezentacji”** w pasku (`tv_outlined`, akcent, `tooltip`, 48 dp) tylko wtedy, gdy jest drzewo (`_layout != null`). **Tryb** (D3): bez paska „Drzewo”, paska zakładek, karty, + / − i pigułki poziomu; poziom 2 stały — `_onView` nie zmienia poziomu ze skali, szczypanie i podwójne dotknięcie wyłączone; dopasowanie z D4 przy wejściu, po obrocie, po przestawieniu środka i w `_keepInView` zamiast `_centreOn`; pigułka podpowiedzi ok. 4 s przy każdym wejściu (`liveRegion`); dotknięcie pustego miejsca → „Zakończ prezentację” na 3 s w prawym górnym rogu (`close` w akcencie, napis w kolorze tekstu, powierzchnia z obrysem, 48 dp); osoba w środku — nic (D5); `PopScope` — wstecz kończy tryb. **Wyjście:** poziom 2, skala 1, ta sama osoba w środku. `dispose` w trybie przywraca orientację i paski |
| `lib/app/tree/presentation_mode.dart` (nowy) | `enterPresentation()` / `leavePresentation()` — orientacja (D2) i paski (D1) w jednym miejscu; w ekranie nie ma nic platformowego |
| `android/app/src/main/kotlin/com/grobing/app/SystemBars.kt` (nowy) + `MainActivity.kt` | **tylko gdy krok 0 pokaże, że `immersiveSticky` nie działa** (D1): kanał `hide` / `show` |

Testy (pisze `qa`): `test/app/tree/tree_screen_test.dart` (rozszerzony), `test/app/tree/presentation_mode_test.dart` (nowy).

### AC → implementation → test (testy pisze `qa`)
| AC | Implementacja | Test happy-path |
|---|---|---|
| AC-8 — tryb prezentacji | ikona → `enterPresentation`, tryb w `TreeScreen` | wymyślona rodzina, widok 914 × 411: dotknięcie ikony → kanał platformy dostaje orientację `landscapeLeft` + `landscapeRight` i schowanie pasków (przechwycony `SystemChannels.platform` albo kanał z D1); nie ma „Drzewo”, + / −, karty ani paska zakładek; 20 osób (poziom 2), cały układ w kadrze; podpowiedź jest, po 4 s jej nie ma |
| AC-8 — przestawianie w trybie | dotknięcie osoby: ona w środku, dopasowanie od nowa, poziom 2 | dotknięcie żony → ona w środku, dalej bez karty; dotknięcie osoby w środku → widok osoby się nie otwiera (D5) |
| Wyjście | pusty dotyk → „Zakończ prezentację” → `leavePresentation`; wstecz to samo | pusty dotyk → przycisk, po 3 s go nie ma; dotknięcie przycisku → orientacja (D2) i paski (`edgeToEdge`) wracają, pasek „Drzewo”, karta i + / − wracają, ta sama osoba w środku, poziom 2; to samo przez wstecz (`handlePopRoute`) |
| Element 1 — ikona tylko z drzewem | `_bar` | pusta baza i brak „ja” — ikony nie ma; `meetsGuideline(androidTapTargetGuideline)` i `labeledTapTargetGuideline` na ikonie i na „Zakończ prezentację” (retro 3, R2) |

### Data layer
- **Bez zmian:** ekran tylko czyta (jak ISSUE-033), schemat v12 zostaje. Nie ma migracji ani próbnego odtworzenia z kopii.
- **Bez sieci** (D11, [[NFR-005-dane-nie-opuszczaja-telefonu]]): bez Google Cast i bez nowego uprawnienia. `qa` sprawdza, że `AndroidManifest.xml` i
  `pubspec.yaml` się nie zmieniły.

### Manual verification
**Agent na emulatorze** — przed stopem #2, ze zrzutami (`Grobing_Restore`, build profile, wymyślona rodzina ze stanu po ISSUE-033):
0. (`dev`, przed budową) pomiar D1 i D2: czy paski znikają, czy orientacja wraca do pionu.
1. AC-8: ikona → zrzut poziomo, bez pasków systemu i bez przycisków; podpowiedź, a po 4 s jej brak; `uiautomator dump` — poza osobami nie ma
   nic do dotknięcia.
2. Dotknięcie kilku osób: każda staje w środku, poziom 2 dopasowany; dotknięcie osoby w środku nic nie robi (D5).
3. Wyjście: pusty dotyk → „Zakończ prezentację” (zrzut), po 3 s go nie ma; dotknięcie → pion, paski, ta sama osoba w środku. Drugi raz
   wstecz (`keyevent 4`).
4. Przeciągnięcie od krawędzi w trybie → paski na chwilę i same znikają. Home i powrót do aplikacji → tryb trwa (poziomo, bez pasków).
5. Tekst 200% w trybie: dopasowanie przy skali 0,4, a przeciąganie odsłania resztę.
6. Ograniczenie animacji: przestawienie w trybie odbywa się od razu.
7. Nazwa kafelka przesyłania ekranu w szybkich ustawieniach emulatora po polsku (D6) — zrzut.

**Autor: odczucie** (najwyżej 3 kroki, emulator `Grobing_Restore`):
1. Dotknij ikonę telewizora i przejdź po rodzinie, dotykając osoby. Czy obraz poziomo wygląda tak, jak chcesz go pokazać rodzinie na
   telewizorze (wielkość osób, imiona)?
2. Zakończ prezentację dotknięciem pustego miejsca, a drugi raz przyciskiem wstecz. Czy wyjście jest oczywiste i drzewo wraca tam, gdzie było?

### Out of Scope
- Google Cast i odbiornik na telewizorze (D11).
- Szczypanie i + / − w trybie (D16 — poziom stały).
- „Przesyłaj ekran” z telewizorem autora i tryb na fizycznym telefonie (producent może inaczej chować paski) → [[ISSUE-032-mvp-install]] → *Hand checks*.
- Blokada całej aplikacji w pionie (D2).
- „Połącz dwie osoby” w pasku → [[US-011-polacz-dwie-osoby]]; czas → [[US-010-czas-na-drzewie]].
- Powiadomienia innych aplikacji w czasie przesyłania obrazu — aplikacja ich nie kontroluje (w telefonie: „Nie przeszkadzać”).

## Dev report
> `dev`, 2026-10-14. Flutter 3.41.1. Build profile z `--dart-define=FRAME_LOG=true` na `Grobing_Restore` (Android 36.1), wymyślona
> rodzina ze stanu po ISSUE-033. `flutter analyze` — czysto; `dart format` — zrobione; `flutter test` — 721 zielonych (bez nowych testów — to `qa`).

### Krok 0 — pomiar D1 i D2 (przed resztą)
- **D1: `SystemUiMode.immersiveSticky` działa przy `targetSdk 36` na Androidzie 36.1.** Po wejściu `dumpsys window`: `statusBars visible=false`,
  `navigationBars visible=false`, `mCurrentRotation=ROTATION_90`. Zdanie z dokumentacji Fluttera („the Android system will ignore this value”)
  się nie potwierdziło. **Kanał natywny `SystemBars.kt` nie powstał.**
- **D2: orientacja wraca do pionu** — przy włączonym i wyłączonym autoobracaniu, wyjście przez „Zakończ prezentację” i przez wstecz
  (`ROTATION_0`, oba paski `visible=true`). Krok „najpierw pion” jest potrzebny: przy zablokowanym obrocie emulator zapamiętał poziom
  (`user_rotation=1`), a wyjście z trybu wyzerowało go do `0`.

### What was built (`{code}`)
- **`lib/app/tree/presentation_mode.dart`** (nowy) — `enterPresentation()`: poziomo, potem paski schowane (`immersiveSticky`), dopiero gdy
  aplikacja ma już poziomy rozmiar (najwyżej 2 s — znalezisko a); `leavePresentation()`: paski (`edgeToEdge`), na chwilę pion, potem ustawienie
  telefonu (D2).
- **`lib/app/tree/tree_screen.dart`** — ikona „Tryb prezentacji” w pasku (`tv_outlined`, akcent, `tooltip`, 48 dp) tylko z drzewem; tryb w tym
  samym ekranie (D3): bez paska „Drzewo”, paska zakładek, karty, + / − i pigułki poziomu; poziom 2 stały (poziom ze skali wyłączony, bez
  szczypania i podwójnego dotknięcia); dopasowanie D4 (`_fitted`) przy wejściu, po obrocie, po przestawieniu środka i przy powrocie drzewa do
  kadru; pigułka podpowiedzi 4 s przy każdym wejściu; pusty dotyk → „Zakończ prezentację” na 3 s (prawy górny róg, styl przycisku z obrysem
  na powierzchni, 48 dp); `PopScope` — wstecz kończy; wyjście: poziom 2, skala 1, ta sama osoba w środku; `dispose` w trybie oddaje paski i
  orientację. Podpowiedź czytnika węzła przychodzi z ekranu (`hint`), żeby osoba w środku pokazu nie mówiła „otwórz”.
- `AndroidManifest.xml`, `pubspec.yaml`, Kotlin — bez zmian (bez sieci i uprawnień, NFR-005).

### Deviations (do przeglądu `ui`)
1. **Osoba w środku w prezentacji: dotknięcie dopasowuje poziom od nowa** (płynnie, jak powrót drzewa do kadru), a nie „nic” z D5. Element 11
   mówi „dotknięcie osoby → … poziom 2 dopasowany na nowo”, a po przesunięciu palcem to jedyna droga z powrotem bez wychodzenia. Widok osoby
   się nie otwiera (D5); czytnik: bez podpowiedzi.
2. **Pasy 24 dp przy górnej i dolnej krawędzi nie przyjmują dotyku w trybie** (znalezisko b). Dopasowany poziom i tak trzyma od nich 24 dp (D4).
3. **„Zakończ prezentację” chowa podpowiedź**, gdy pusty dotyk przyjdzie w ciągu 4 s od wejścia — specyfikacja nie mówi, co z obiema naraz.
4. **Podpowiedź przy wejściu przykrywa na 4 s górny rząd osób** (zrzut `02`) — pigułka stoi tam, gdzie pigułka poziomu. Do oceny `ui`.
5. **Tekst 200%, ekran 360 dp, poziomo:** poziom 2 mieści się przy skali 0,45 — kółka ok. 20 dp, imiona 26 sp (I2 — imię nie maleje), 6 z 20
   imion schowanych (zrzut `18b`). Do oceny `ui`, także pod pozycję „I1 i „Moja””.
6. **Nazwa kafelka (D6):** w polskim interfejsie emulatora (SystemUI Google, Android 16) kafelek nazywa się **„Przesyłanie”**, nie „Przesyłaj
   ekran” — `quick_settings_cast_title` (pl) w zasobach SystemUI z emulatora. W kodzie tekst ze specyfikacji; poprawka tekstu to `ui` / autor.

### Found on the emulator (przejście AC przed `qa`, R5) — poprawione
- (a) **Paski chowane w trakcie obrotu zostawiały aplikację przy pionowym rozmiarze w poziomym oknie** — drzewo ucięte na 360 dp i
  dopasowane do pionu. Log rozmiarów (tymczasowy, usunięty): 6 z 8 wejść przy tekście 200% dostawało tylko pionowy rozmiar (360 × 800 dp),
  choć `dumpsys` mówił `ROTATION_90`. Poprawka: paski dopiero po poziomym rozmiarze — **10 z 10** przy 200%, **6 z 6** przy 100%.
- (b) **Systemowe przeciągnięcie od krawędzi przesuwało drzewo** — w `immersiveSticky` gest, który pokazuje paski, trafia też do aplikacji
  (dokumentacja `SystemUiMode`). Poprawka: pasy z odstępstwa 2. Po niej przeciągnięcie od góry i od dołu pokazuje paski na chwilę, drzewo stoi.
- (c) **Dotknięcie osoby w środku nic nie robiło** — w trybie węzeł nie miał `onTap`. Poprawka: odstępstwo 1.

### Observations (nie błędy aplikacji)
- **Systemowe okno „Viewing full screen — To exit, swipe down from the top of your screen — Got it”** przy pierwszym pełnym ekranie aplikacji;
  po „Got it” nie wraca. Na telefonie pokaże się raz — także na telewizorze, jeśli przesyłanie już trwa.
- **Zablokowany obrót może zostać poziomo**, gdy aplikacja zginie w trakcie pokazu i zostanie uruchomiona wprost (`adb am start`). Z ikony w
  launcherze — pionowo (ekran główny zeruje `user_rotation`). Ekran główny i powrót w trakcie pokazu: tryb trwa, poziomo, bez pasków.

### Sprawdzone przez `dev` (zrzuty w katalogu tymczasowym sesji, `shots-034\`)
- AC-8: ikona w pasku (`01`, 48 dp), wejście z podpowiedzią (`02`), poziom 2 dopasowany, 20 osób, poza osobami nic do dotknięcia (`uiautomator dump`);
  dotknięcie Kasi → ona w środku, 17 osób, dopasowane od nowa (`04`); pusty dotyk → „Zakończ prezentację”, 48 dp (`05`), po 3 s znika.
- Wyjście: przyciskiem (`06` — pion, paski, Kasia w środku, karta i + / −) i wstecz (`07`), przy autoobracaniu włączonym i wyłączonym.
- Przeciągnięcie od krawędzi i ekran główny z powrotem (`12`); przesunięcie i dotknięcie osoby w środku (`15`); tekst 200% na 360 dp (`18b`,
  `18c`); bez animacji (`19`); stany bez ikony: bez „ja” (`20`) i pusta baza (`21`) — na kopii bazy testowej przez `run-as`, potem baza
  przywrócona; ostateczny build: trzy wejścia i wyjścia (`22`).
- **Nie sprawdzone:** czytnik TalkBack na głos; fizyczny telefon i telewizor (→ [[ISSUE-032-mvp-install]] → *Hand checks*).

### For `qa`
- Kroki — *Implementation plan* → *Manual verification* (agent: kroki 0–7, z czego 0–6 przeszedł już `dev`, wyżej; autor: 2 kroki odczucia).
- **Testy widżetów:** `enterPresentation` czeka na poziomy rozmiar widoku do 2 s (co 50 ms) — w teście ustaw `tester.view.physicalSize` poziomo
  przed dotknięciem ikony albo przewiń czas o ≥ 2 s; wywołania platformy: `SystemChrome.setPreferredOrientations` i
  `SystemChrome.setEnabledSystemUIMode` na `SystemChannels.platform`.
- **Stan emulatora:** `Grobing_Restore` — build profile (FRAME_LOG) z tej pozycji, wymyślona rodzina, „ja” = Mateusz; ustawienia ekranu jak przed
  testami (autoobracanie włączone, tekst 100%, gęstość i rozmiar domyślne, animacje 1); okno „Viewing full screen” już potwierdzone.

### Poprawki po `qa` i przeglądzie `ui` (2026-10-14)
- **Testowalność:** `_untilLandscape` czyta widok przez `WidgetsBinding.instance.platformDispatcher`, a nie `ui.PlatformDispatcher.instance` —
  na telefonie to ten sam widok, a test widżetu może go obrócić (bez tego test kolejności „obrót → paski” nie miał czego sprawdzić).
- **MINOR-2 `ui`:** pasy bez dotyku przy **wszystkich czterech** krawędziach. Na emulatorze przy nawigacji trzema przyciskami pasek w poziomie
  stoi z prawej (`frame=[2274,0][2400,1080]`), a przeciągnięcie od niej przesuwało drzewo („Ja” z x 1311 na 665); po poprawce zostaje (`23c`).
  Emulator wrócił do nawigacji gestami.
- **MINOR-1 `ui`:** podpowiedź według [[drzewo]] v1.8 (D26): „Obraz na telewizor: przesyłanie ekranu w szybkich ustawieniach telefonu”, z twardą
  spacją po „w” (`r07`).

## Verification
> `qa`, 2026-10-14. DoD ISSUE (MVP): test happy-path dla każdego AC · ręczna weryfikacja na emulatorze · dokumentacja · zero danych rodziny.
> Warstwa danych bez zmian (ekran tylko czyta, schemat v12) — bez testu migracji i bez próbnego odtworzenia (plan → *Data layer*). Sieci w pozycji
> nie ma: `AndroidManifest.xml` i `pubspec.yaml` bez zmian, więc logcat pod kątem współrzędnych nie dotyczy (retro 3, R7).

### Tests (happy path per AC, `{code}/test/`)
- `test/app/tree/presentation_mode_test.dart` (nowy, 3): wejście — najpierw `setPreferredOrientations` (poziomo), paski (`immersiveSticky`) dopiero
  po obrocie widoku; ekran, który się nie obraca — paski po 2 s; wyjście — `edgeToEdge`, `[portraitUp]`, `[]` (D2).
- `test/app/tree/tree_screen_test.dart` (+3, 1 rozszerzony):
  - **AC-8 — wejście:** wywołania platformy w kolejności; nie ma paska „Drzewo”, paska zakładek, karty, „Pokaż”, + / − ani ikony; 20 osób, wszystkie
    na ekranie 800 × 360 dp; podpowiedź widoczna, po 4 s nie; `meetsGuideline(androidTapTargetGuideline)`, `labeledTapTargetGuideline`, każdy
    przycisk z akcją dotknięcia (retro 3, R2);
  - **AC-8 — w trybie:** dotknięcie Kasi → 17 osób, nadal bez karty, ona w środku bez podpowiedzi czytnika, inni „w środek”; osoba w środku nie
    otwiera widoku; przeciągnięcie od górnej i od bocznej krawędzi nie rusza drzewa, ze środka — rusza; dotknięcie osoby w środku dopasowuje od
    nowa; pusty dotyk → „Zakończ prezentację”, po 3 s znika;
  - **wyjście:** „Zakończ prezentację” i wstecz (`handlePopRoute`) — wywołania wyjścia, karta „ur. 1985 · Twoja żona”, 17 osób, ikona, + / −, pasek
    zakładek, Kasia na środku ekranu 360 dp; po wstecz drzewo zostaje;
  - **stany:** pusta baza i brak „ja” — bez ikony (test stanów rozszerzony).
- **Czy testy umieją się wywrócić:** pasy przy krawędziach na chwilę wyłączone (wysokość 0) → test „w trybie” padł (Kasia przesunięta o 200 dp);
  przywrócone. Test kolejności „obrót → paski” nie przeszedłby z wcześniejszym `ui.PlatformDispatcher.instance` (widok testu nieobrócony).
- `dart format` bez zmian · `flutter analyze` czysto · `flutter test`: **727 zielonych** (było 721).

### Agent na emulatorze (przed stopem #2)
Kroki 0–7 z planu przeszedł `dev` (*Dev report* → *Krok 0*, *Sprawdzone przez `dev`*), a `qa` powtórzył kluczowe na ostatecznym buildzie (zrzuty
`r01`–`r07`, `23c` w `shots-034\`): ikona, wejście z podpowiedzią, dopasowanie, „Zakończ prezentację”, dotknięcie Kasi, wyjście wstecz, nowa
podpowiedź, boczna krawędź przy trzech przyciskach. Tekst 200% (`18b`), ograniczenie animacji (`19`), stany bez ikony (`20`, `21`) — z przebiegu `dev`.

### UI review (`ui`, subagent bez historii) — 0 BLOCKER, 0 MAJOR, 2 MINOR — oba poprawione przed stopem #2
- **Odstępstwa 1–6 przyjęte** → [[drzewo]] v1.8: D25 (dotyk w trybie: osoba w środku dopasowuje, pasy przy krawędziach, „Zakończ” chowa podpowiedź),
  D26 (podpowiedź mówi o funkcji, nie o nazwie kafelka; jej miejsce), D16 v1.8 (systemowe okno pełnego ekranu), *Open* 5 i 6 — zmiana decyzji autora
  (I1, G2) jako wejście do osobnej pozycji; 200% w trybie mierzy jej `ui`.
- **MINOR-1** — tekst podpowiedzi według D26 → poprawione (`r07`).
- **MINOR-2** — boczna krawędź przy nawigacji trzema przyciskami → sprawdzone na emulatorze: drzewo jechało; poprawione (pasy przy czterech
  krawędziach, `23c`, test).
- Korekta liczby w *Dev report*: na `18b` widać 13 z 20 imion (7 schowanych), nie 14.

### Dane rodziny
- Zmiany: 4 pliki kodu i testów; żadnych baz, kopii, eksportów ani zdjęć (zrzuty i kopie bazy testowej tylko w katalogu tymczasowym sesji).
- Słowa z wielkiej litery w dodanych liniach: wyłącznie wymyślona rodzina (Kasia, Mateusz, Wymyślon-) i nazwy produktów (Pixel, Samsung, Smart View).

### Not verified here (po jednym w linii — dla [[ISSUE-032-mvp-install]] → *Hand checks*)
- „Przesyłanie” obrazu z trybu prezentacji na telewizor autora (emulator nie przesyła).
- Nazwa kafelka przesyłania ekranu na telefonie autora (podpowiedź mówi o funkcji — D26).
- Tryb na fizycznym telefonie: paski, obrót i przeciągnięcie od krawędzi przy nawigacji, której używa autor.
- Systemowe okno „pełny ekran” przy pierwszym wejściu — przed pierwszym pokazem wejść w tryb raz bez przesyłania.
- Czytnik TalkBack na głos w trybie prezentacji.

### Stop #2 (2026-10-14) — wstrzymany przez autora, czeka na decyzję
Autor, przed krokami: *„chciałem aby ten tryb telewizora streamował obraz do smart TV, który jest w tej samej sieci wifi co mój telefon (tak jak
robię to np. w Youtube)”*. To rozwidlenie decyzji z [[drzewo]] D11 (przyjętej na stopie #1 [[SPIKE-002-tree-on-a-phone]]: systemowe przesyłanie
ekranu + tryb prezentacji, **bez Google Cast**). Różnica: YouTube to *casting* — aplikacja-odbiornik na telewizorze sama ładuje treść, telefon
steruje ([Google Cast — overview](https://developers.google.com/cast/docs/overview)); zbudowany tryb to *mirroring* — telefon wysyła przez Wi-Fi
obraz ekranu, telewizor wybiera się z listy jak w YouTube. Casting dla Grobing = odbiornik na publicznym adresie HTTPS, rejestracja Google Cast
($5, [registration](https://developers.google.com/cast/docs/registration)) i dane rodziny wysyłane do aplikacji na telewizorze — wbrew
[[NFR-005-dane-nie-opuszczaja-telefonu]]; tylko telewizory z Google Cast. Rekomendacja `qa`: najpierw sprawdzić przesyłanie ekranu z telefonu
autora na jego telewizor (bez Grobing, np. ze Zdjęć) — czeka na odpowiedź autora.

**Odpowiedź autora (2026-10-14): „tak”** — ze zrzutem z Zdjęć Google: telewizor autora jest na liście „Przesyłaj na”, czyli to odbiornik Google Cast
w tej samej sieci Wi-Fi. Samego przesyłania ekranu z kafelka szybkich ustawień zrzut nie pokazuje → zostaje na liście *Hand checks* (wyżej).
**Decyzja (rekomendacja `qa` przyjęta „tak”):**
- ISSUE-034 zostaje przy przesyłaniu ekranu (D11) i zamyka się po krokach autora na emulatorze;
- **zaraz potem mała pozycja „Przesyłaj z aplikacji”:** przycisk w drzewie otwiera systemową listę przesyłania ekranu — jedno dotknięcie jak
  „Przesyłaj” w Zdjęciach. Zmierzone na emulatorze (Android 16): `Settings.ACTION_CAST_SETTINGS` otwiera ekran „Google Cast” z listą urządzeń w
  pobliżu (`com.android.settings/.Settings$WifiDisplaySettingsActivity`). Bez kodu sieciowego — obraz ekranu wysyła system. Łańcuch `ui` → `planning`;
- **casting jak w Zdjęciach/YouTube** (odbiornik Google Cast rysuje drzewo, telefon wolny) — dopiero po MVP i tylko gdy przesyłanie ekranu nie
  wystarczy: ADR zmieniający NFR-005, odbiornik na HTTPS, rejestracja Google Cast.
**Dla `docs` przy zamknięciu:** założyć pozycję „Przesyłaj z aplikacji” (obok pozycji „drzewo: I1 i „Moja”” — kolejność ustala `pm` z autorem).

### Stop #2 (2026-10-14, po decyzji) — autor: „ok”
Ślad na emulatorze (`logcat`: zmiany orientacji okna Grobing i klatki `GROBING_FRAME`):
- **krok 1 — ze śladem:** wejście w tryb 09:44:41, przestawienie w trybie (klatki 09:44:45–47), ok. 8 s pokazu;
- **krok 2 — częściowo:** jedno wyjście do pionu 09:44:49 ze śladem; drugiego wejścia i wyjścia przyciskiem Wstecz nie widać (wstecz sprawdzone
  przez agenta — zrzut `07` — i w teście `handlePopRoute`).
- Pytanie 3 (nazwa kafelka) — zbędne po decyzji wyżej; zostaje na liście niżej.

### Na listę ISSUE-032 → *Hand checks* (po jednym w linii)
- Przesyłanie ekranu z trybu prezentacji na telewizor autora z kafelka szybkich ustawień (telewizor jest odbiornikiem Google Cast — zrzut autora z Zdjęć).
- Nazwa kafelka przesyłania ekranu na telefonie autora (podpowiedź mówi o funkcji — [[drzewo]] D26).
- Tryb na fizycznym telefonie: paski, obrót i przeciągnięcie od krawędzi przy nawigacji, której używa autor.
- Systemowe okno „pełny ekran” przy pierwszym wejściu — przed pierwszym pokazem wejść w tryb raz bez przesyłania.
- Czytnik TalkBack na głos w trybie prezentacji.
- Wyjście z trybu przyciskiem Wstecz — „ok” autora bez śladu na urządzeniu (stop #2, krok 2).

### Werdykt `qa`: APPROVED (self-check, z uwagami)
- AC-8 i AC wyjścia: test happy-path dla każdego, przejście na emulatorze ze zrzutami, przegląd `ui` (0 BLOCKER, 0 MAJOR, 2 MINOR poprawione).
- **Uwagi:** (1) obraz na prawdziwym telewizorze i fizyczny telefon niesprawdzone (lista wyżej); (2) autor chce wejścia „jak w Zdjęciach” → pozycja
  „Przesyłaj z aplikacji”; (3) przy tekście 200% w trybie imiona 26 sp przy okręgach ok. 20 dp (I2) — mierzy pozycja „drzewo: I1 i „Moja””;
  (4) błąd „paski w trakcie obrotu” (6 z 8 wejść) złapany dopiero przez przejście na emulatorze przy 200% — przy 100% nie był widoczny.
- **Czego szukałem i nie znalazłem:** danych rodziny w zmianach; nowych zależności, uprawnień i kodu sieciowego (`pubspec.yaml`, manifest, Kotlin bez
  zmian); przycisku bez akcji dotknięcia; celu dotyku < 48 dp w trybie; regresji w 721 dotychczasowych testach.

### Paczka dla `docs` (jedna pozycja = jeden commit na repo)
- **`grobing-code`:** `lib/app/tree/tree_screen.dart` · `lib/app/tree/presentation_mode.dart` (nowy) · `test/app/tree/tree_screen_test.dart` ·
  `test/app/tree/presentation_mode_test.dart` (nowy).
- **`grobing-vault`:** `backlog/issues/ISSUE-034-tree-presentation-mode.md` · `05_DESIGN/drzewo.md` (v1.8, `ui`) · `00_START_HERE/TRACEABILITY.md` ·
  pliki zamknięcia `docs` (m.in. `CURRENT_STATE.md`, [[ISSUE-032-mvp-install]] → *Hand checks*, dwie nowe pozycje).
- **`grobing-agents`:** bez zmian.
