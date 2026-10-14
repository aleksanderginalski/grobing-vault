---
title: "ISSUE-038 — History on the TV and its tempo: ▶ in presentation mode with the year large enough for the room, and a choice of the slider's speed"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-010-czas-na-drzewie]]"
depends-on: "[[ISSUE-037-time-on-the-tree]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-14
verdict-reviewer: self-check
source: "prośba autora na stopie #2 [[ISSUE-037-time-on-the-tree]] (2026-10-14: *„Czy play również zadziała podczas prezentowania?”*, potem *„a) Można było tą historie odtwarzać na telewizorze, b) dostosowanie prędkości tych lat”*) · [[drzewo]] v1.13 (element 6, element 11, D37)"
created: 2026-10-14
updated: 2026-10-14
---

# ISSUE-038 — Historia na telewizorze i tempo lat

> Z prośby autora na stopie #2 [[ISSUE-037-time-on-the-tree]] (`docs`, 2026-10-14). Dziś tryb prezentacji nie ma suwaka ani roku i zawsze pokazuje „dziś”
> ([[drzewo]] D37), a ▶ biegnie stałym tempem ok. 21 lat na sekundę (D34). Punkty c) i d) z tej samej prośby — animacje połączeń i zbliżenia na zdarzenia, wieniec
> przy portrecie według nazwiska — są w [[2026-10-14-opowiesc-rodziny-i-wieniec]] (INBOX): mają za dużo niewiadomych na pozycję. **Pozycja zmienia ekran → `ui`
> przed `planning`.**

## What to build
1. **▶ w trybie prezentacji** (element 11): historia rodziny odtwarzana na telewizorze — drzewo w roku, osoby pojawiają się i łączą jak w elemencie 6.
2. **Rok widoczny na telewizorze** — czytelny z odległości pokoju (karty w prezentacji nie ma).
3. **Sterowanie na telefonie w prezentacji** — gdzie dotknąć ▶ / ❚❚ i suwak (dziś pusty dotyk pokazuje na 3 s tylko „Zakończ prezentację”, D25).
4. **Tempo lat** — wybór prędkości odtwarzania (np. wolniej / jak dziś / szybciej) w karcie i w prezentacji.

## Acceptance Criteria
> `planning` 2026-10-14, z [[drzewo]] v1.14 według rekomendacji `ui` (L1, B2, V2, Z2) — **do potwierdzenia na stopie #1**. Szkic sprzed `ui` miał tempa 14 · 7 · 4 s, czyli
> dzisiejsze tempo jako środkowe; po *„dla mnie za szybko”* dzisiejsze to najszybsze.

- [ ] **AC-1 — historia w prezentacji.** *Given* tryb prezentacji *When* dotykam pustego miejsca *Then* na dole listwa (▶ / ❚❚, rok początku, suwak, tempo), a u góry „Zakończ
  prezentację”; chowają się po 5 s od ostatniego dotyku albo po drugim pustym dotyku. *When* ▶ *Then* historia biegnie od początku suwaka (albo od bieżącego roku) do „dziś”, ❚❚
  zatrzymuje, a rok widać w lewym górnym rogu (36 sp, 48 dp od lewej krawędzi) także przy schowanej listwie; na „dziś” napis „dziś” zostaje 3 s ([[drzewo]] element 11, D39, D40).
- [ ] **AC-2 — tempo.** Przycisk tempa w karcie i w listwie przełącza „Wolno” → „Średnio” → „Szybko” (5 · 10 · 20 lat na sekundę; od 1880 do dziś ok. 29 · 15 · 7 s), domyślnie
  „Średnio”. Tempo jest to samo w karcie i w trybie i zostaje do zamknięcia aplikacji; zmiana w trakcie ▶ nie zatrzymuje odtwarzania (element 6, D41).
- [ ] **AC-3 — ograniczenie animacji.** Przy „Usuń animacje” zostaje R2 (dekada naraz, bez przenikania), a tempo zmienia odstęp skoków: co ok. 2 · 1 · 0,5 s (D36, D41).
- [ ] **AC-4 — prezentacja z roku Y.** *Given* karta na roku 1950 *When* „Przesyłaj na telewizor” → wstecz *Then* tryb pokazuje rok 1950, ▶ stoi; po „Zakończ prezentację” karta
  jest dalej w roku 1950 (Z2 — D42, zmienia D37).
- [ ] **AC-5 — tekst 200%.** Na 360 dp tempo stoi w górnym rzędzie karty, między latami, i nic nie jest ucięte; w trybie listwa mieści się w jednym rzędzie, a rok w rogu rośnie
  najwyżej do 1,3× (element 6, element 11, [[style-b]] *Thresholds* → tekst dla telewizora).
- [ ] **AC-6 — czas na sterowanie.** Z czytnikiem ekranu sterowanie w trybie nie chowa się samo; przy dłuższym „Czasie na działanie” w ułatwieniach dostępu chowa się po tym czasie,
  a nie po 5 s (D40).

## Open for `ui` (kandydaci na makiecie — retro 2, R6)
1. Wielkość i miejsce roku na telewizorze (prior art: napisy i liczniki w telewizji — pomiar przy odległości z kanapy).
2. Sterowanie w prezentacji: obok „Zakończ prezentację”, osobna listwa, czy gest.
3. Tempo: ile prędkości, jak je nazwać, gdzie stoi przełącznik (karta jest ciasna przy tekście 200%).
4. Czy prezentacja otwarta z roku Y zaczyna od Y (dziś D37: zawsze „dziś”) — zmiana D37 do decyzji autora.

## Out of scope
- Animacje związków, zbliżenia na zdarzenia, wieniec przy portrecie → [[2026-10-14-opowiesc-rodziny-i-wieniec]].
- Google Cast i odbiornik na telewizorze — obraz dalej przesyła system ([[drzewo]] D11, D29).

## Notes
- **Autor na stopie #2 ISSUE-037:** *„dla mnie za szybko”* — obecne ok. 20 lat/s (1880 → dziś w ok. 7 s) to dla niego za szybko; tempo domyślne do przemyślenia razem
  z wyborem tempa (np. wolniejsze domyślne).
- Logika czasu jest gotowa (`lib/app/tree/tree_time.dart`, ISSUE-037): ta pozycja to widok i zegar ▶ (`_nextLater` w `tree_screen.dart`).
- Płynność ▶ zmierzona na emulatorze: 7–9% wolnych klatek przy tempie ok. 20 lat/s (ISSUE-037 → *Dev report*). Szybsze tempo = częstsze zmiany roku — pomiar przy
  najszybszym wariancie.

## Implementation plan
> `planning`, 2026-10-14. Specyfikacja (`ui`, przed planem): [[drzewo]] v1.14 — element 6 (tempo), element 11 (rok, sterowanie, wejście z roku Y), *Navigation*, *States*
> (tryb prezentacji — sterowanie, historia), *Sketch*, *AC → element*, *Candidates — ISSUE-038*, D38–D42, *Open* 9; [[style-b]] v1.30 (*Thresholds* → tekst dla telewizora).
> Makieta: `drzewo-038.html` w katalogu tymczasowym sesji `baf00b7b-…` (sekcje 1–5, podgląd „z kanapy” 32–65″, self-test `#test=1` i `#playtest=1`, zrzuty `shots-038\`).
> **Kandydaci tego, co widać** (retro 2, R6): L1–L3, B1–B3, V1–V3 i Z1–Z2 działają na makiecie (przełączniki w sekcjach 1–4), przed rekomendacją. *Open for `ui`* 1–4 z tej
> pozycji rozstrzyga specyfikacja: 1 → D39 (L), 2 → D40 (B), 3 → D41 (V), 4 → D42 (Z). Wszystko według rekomendacji, do potwierdzenia na stopie #1.

### Prior art (źródła, nie pamięć)
- **Tekst na telewizorze:** [[drzewo]] D38 — skala TV Androida (display small 36 sp dla liczb), margines 5% (48 dp z boków), wysokość znaku w kącie widzenia (ISO 9241-3xx: zwykle
  20–22′, minimum 16′, za listą CSS W3C). Telefon poziomo wypełnia szerokość telewizora 16:9, więc 36 sp ma z 3 m 23–46′ (32–65″), a imię 13 sp — 8–17′.
- **Sterowanie odtwarzacza:** Media3 `PlayerControlView` — `DEFAULT_SHOW_TIMEOUT_MS = 5_000`, `controllerHideOnTouch = true`, prędkości w menu (siedem). **Czas na sterowanie:**
  `AccessibilityManager.getRecommendedTimeoutMillis` (Android 10+, źródła SDK 36): *„Controls should remain on the screen for at least this long”*; ustawienie
  `accessibility_interactive_ui_timeout_ms` (`Settings.Secure`, `@hide`, ale `@Readable`).
- **Z kodu** (ankieta 2026-10-14):
  - zegar ▶ to `_nextLater` w `tree_screen.dart`: krok `7000000 ~/ (time.now - latestSliderStart)` µs (ok. 21 lat/s), przy `disableAnimations` — dekada co 1 s. Tempo zmienia
    tylko ten krok i odstęp R2;
  - `_present` zatrzymuje ▶ i ustawia `_setYear(null)` (D37) — tu zostaje rok (Z2); `_leave` roku nie rusza;
  - pusty dotyk w trybie: `_showExit` z `_exitTimer` na 3 s i `_exitButton` w `Positioned(top: 12, right: 12)`; pigułka poziomu i podpowiedź D26 to `_levelPill` u góry na środku —
    rok w lewym rogu z nimi nie koliduje;
  - rząd czasu to `TreeTimeBar` (`tree_time_bar.dart`): `start`, `now`, `year`, `playing`, `onPlay`, `onYear`; przy tekście ≥ 150% dwa rzędy. Ten sam widżet może stanąć w listwie
    w wariancie jednego rzędu bez roku na końcu;
  - kanał `grobing/external` (`external_link.dart` ↔ `ExternalLinks.kt`) już otwiera ekran przesyłania; `ExternalLinks` dostaje dziś tylko lambdę `start`, a do
    `AccessibilityManager` potrzebuje `Context`. `minSdk` = 24, więc metoda z Androida 10 za warunkiem wersji;
  - `tree_screen.dart` ma 1815 linii — sterowanie trybu (rok, listwa) do osobnego pliku;
  - testy, które zmienią oczekiwania: `tree_screen_test.dart` („the empty space shows „Zakończ prezentację” for 3 s” → 5 s) i `tree_time_screen_test.dart` („▶ from 1860 about 21
    years a second” → tempo „Średnio”, 10 lat/s). Test R2 („about a second each”) przy „Średnio” zostaje.

### Stop #1 (2026-10-14) — autor: „Ok”
Rekomendacja przyjęta w całości: D1 = **L1, B2, V2, Z2**, D2 (US-010 AC-3 przy zamknięciu), D3 („Zakończ prezentację” 5 s), D4 („Czas na działanie” przez kanał), D5 (tempo w
pamięci aplikacji), D6 (pomiar przy „Szybko” z buildem odniesienia). Uwagi do tempa „Średnio” autor nie zgłosił — zostaje domyślne. AC-1–AC-6 potwierdzone. Specyfikacja →
[[drzewo]] *Open* 9 rozstrzygnięte.

### Decisions for stop #1 (rekomendacja → „tak” przyjmuje wszystkie)
- **D1 — wygląd: L1, B2, V2, Z2** ([[drzewo]] *Candidates — ISSUE-038*, *Open* 9; makieta, sekcje 1–4):
  - **L1** — rok w lewym górnym rogu, 36 sp w akcencie na tabliczce, 48 dp od lewej. L2 — pas u góry (drzewo 86% wielkości w każdym pokazie); L3 — wielki rok w tle (1,20:1, poniżej
    3:1);
  - **B2** — listwa na dole jak w odtwarzaczu (▶, suwak, tempo) i „Zakończ prezentację”, 5 s. B1 — ▶ i tempo obok „Zakończ”, bez suwaka; B3 — gest dwoma palcami;
  - **V2** — „Wolno” · „Średnio” · „Szybko” = 5 · 10 · 20 lat/s, domyślnie „Średnio”; przycisk przełącza. V1 — dwa tempa; V3 — „0,5×” · „1×” · „2×”;
  - **Z2** — tryb z rokiem z karty (zmienia D37). Z1 — zawsze „dziś”.
  *Obali* każdego — D39–D42 w specyfikacji.
- **D2 — US-010 AC-3 zmienia brzmienie** (V2): „od 1880 w ok. 7 s” → „w wybranym tempie — domyślnie „Średnio”, od 1880 ok. 15 s; „Szybko” ok. 7 s”. Zmienia to `docs` przy zamknięciu,
  jak T2 w ISSUE-037. Szkic AC tej pozycji (14 · 7 · 4 s) jest już zastąpiony przez AC-2 wyżej.
- **D3 — „Zakończ prezentację” na 5 s zamiast 3 s** (D40): pusty dotyk pokazuje teraz listwę razem z przyciskiem, a jeden czas dla obu jest prostszy niż dwa. Zmienia zachowanie z
  [[ISSUE-034-tree-presentation-mode]] (D25) i jego test.
- **D4 — „Czas na działanie” przez kanał `grobing/external`** (D40 zostawia to planowi): jedna metoda, np. `recommendedTimeout(ms)` → `getRecommendedTimeoutMillis(ms,
  FLAG_CONTENT_CONTROLS | FLAG_CONTENT_TEXT)` na Androidzie 10+, a niżej i przy błędzie kanału — 5 s. Czytane przy wejściu w tryb. Koszt: kilka linii w Kotlinie i `Context` dla
  `ExternalLinks`. Z czytnikiem (`MediaQuery.accessibleNavigation`) sterowanie nie chowa się wcale. **Alternatywa:** sam czytnik bez kanału — wtedy AC-6 tylko w pierwszej części, a
  osoba z dłuższym „Czasem na działanie”, ale bez czytnika, dostaje 5 s.
- **D5 — tempo w pamięci aplikacji, bez zapisu** (D41): jedna wartość na czas działania procesu (np. pole statyczne albo `ValueNotifier` poza stanem ekranu drzewa, bo zakładka
  buduje drzewo od nowa). **Schemat bez zmian**, więc bez testu migracji i bez próbnego odtworzenia z kopii.
- **D6 — pomiar klatki przy „Szybko” w trybie prezentacji, naprzemiennie z buildem odniesienia** (*Do retro* z ISSUE-037: szum hosta na `Grobing_Restore`). „Szybko” to dzisiejsze
  tempo, więc nowe są tylko rok w rogu i listwa. Próg jak w ISSUE-037: wolnych klatek ≤ 10% albo nie więcej niż w buildzie odniesienia w tym samym przebiegu.

### Scope — files (`{code}`)
| Plik | Zmiana |
|---|---|
| `lib/app/tree/tree_time.dart` | tempo: trzy wartości z nazwą („Wolno”, „Średnio”, „Szybko”), lat na sekundę (5 · 10 · 20), krok zegara i odstęp R2 (10 / tempo s); następne tempo po kolei. Czysty Dart |
| `lib/app/tree/tree_time_bar.dart` | przycisk tempa (element 6: 14 sp, waga 500, kolor tekstu, cel 48 dp, `tooltip` i czytnik „Tempo historii: średnio — zmień”) na końcu rzędu, a przy tekście ≥ 150% w górnym rzędzie między latami; wariant **listwy** — jeden rząd, bez roku na końcu, także przy 200% |
| `lib/app/tree/tree_presentation.dart` (nowy) | sterowanie trybu: rok w rogu (L1 — 36 sp × skala tekstu najwyżej 1,3, półgruby, akcent, cyfry o stałej szerokości, tabliczka w kolorze tła 8 dp / 6 dp z boków, `left: 48`, `top: 24`; czytnik „Rok 1950” / „dziś”), listwa (B2 — powierzchnia, promień 16 dp, 24 dp od krawędzi) i „Zakończ prezentację” — przeniesione z `tree_screen.dart` |
| `lib/app/tree/tree_screen.dart` | tempo w `_nextLater` i w R2; zmiana tempa w trakcie ▶ — dalej od bieżącego roku; tryb: pusty dotyk pokazuje albo chowa sterowanie, 5 s (albo czas z D4) od ostatniego dotyku w sterowaniu, bez chowania przy czytniku; rok w rogu, gdy rok nie jest „dziś”, i zawsze ze sterowaniem; „dziś” 3 s po końcu ▶; `_present` bez `_setYear(null)` (Z2), ▶ stoi; wyjście zostawia rok |
| `lib/app/external_link.dart` · `android/…/ExternalLinks.kt` · `MainActivity.kt` | D4: `recommendedTimeout` — Android 10+, inaczej podany czas; `Context` dla `ExternalLinks` |
| `test/…` | `qa` — niżej |

**Bez nowej zależności, sieci i uprawnień** ([[NFR-005-dane-nie-opuszczaja-telefonu]]). **Warstwa danych bez zmian:** bez testu migracji i bez próbnego odtworzenia z kopii.

### Steps for `dev`
0. **Krok 0, przed budową, na emulatorze `Grobing_Restore`:** (a) czy `adb shell settings put secure accessibility_interactive_ui_timeout_ms 10000` zmienia wynik
   `getRecommendedTimeoutMillis` w aplikacji (D4) — jeśli ustawienia nie da się zmienić z adb, AC-6 w drugiej części pokrywa test z kanałem udawanym, nazwany wprost; (b) co dostaje
   `MediaQuery.accessibleNavigation` przy włączonym TalkBack na Androidzie 16 (adb: `settings put secure enabled_accessibility_services …`). Wynik w *Dev report*.
1. `tree_time.dart`: tempo (D41). Zegar ▶ i R2 w `tree_screen.dart` z tempa; przycisk w `TreeTimeBar`, 100% i 200%.
2. Tryb prezentacji: `tree_presentation.dart` — rok (L1), listwa (B2) z tym samym `TreeTimeBar` w wariancie jednego rzędu, „Zakończ prezentację”; czasy 5 s (D3) i z kanału (D4);
   czytnik; Z2.
3. **Przejście AC na emulatorze przed `qa`** (retro 3, R3): stany z *States* (tryb prezentacji — sterowanie, historia), tekst 200% w karcie na 360 dp i w trybie poziomo,
   semantyka (czytnik: tempo, rok w rogu, listwa) i **pomiar klatki** (D6). *Obali:* więcej wolnych klatek niż w buildzie odniesienia — rok w rogu i listwa w osobnych warstwach
   (`RepaintBoundary`), tak jak karta w ISSUE-037.

### Acceptance → tests (`qa`)
| AC | Test (happy path) |
|---|---|
| AC-1 | widget: tryb prezentacji → pusty dotyk → listwa i „Zakończ prezentację”; po 5 s obu nie ma; drugi pusty dotyk chowa od razu; ▶ w listwie → rok w rogu rośnie, ❚❚ zatrzymuje; rok w rogu przy schowanej listwie; na „dziś” „dziś” widać jeszcze 3 s; rok 48 dp od lewej krawędzi i 24 dp od góry |
| AC-2 | `tree_time`: kolejność i wartości temp (5 · 10 · 20, „Średnio” pierwsze); widget: na sztucznym zegarze ▶ od 1860 przy „Średnio” po 3,5 s ok. 1895, przy „Wolno” ok. 1877, przy „Szybko” ok. 1930 (jak `#playtest` makiety); przycisk przełącza w karcie i w listwie to samo tempo; zmiana w trakcie ▶ nie zatrzymuje; po nowym drzewie z zakładki tempo zostaje |
| AC-3 | `disableAnimations`: dekada co ok. 2 · 1 · 0,5 s według tempa, bez przenikania |
| AC-4 | karta na 1950 → tryb (ekran przesyłania udawany jak w teście ISSUE-036) → rok 1950, ▶ stoi → „Zakończ prezentację” → karta na 1950 |
| AC-5 | tekst 200% na 360 dp: tempo w górnym rzędzie, nic nie ucięte; tryb poziomo przy 200%: listwa w jednym rzędzie, rok w rogu ≤ 1,3 × 36 sp; `meetsGuideline` (`androidTapTargetGuideline`, `labeledTapTargetGuideline`, `textContrastGuideline`) na karcie z tempem i na trybie ze sterowaniem (retro 3, R2) |
| AC-6 | `accessibleNavigation: true` → sterowanie po 5 s dalej widać; kanał udawany z 10 000 ms → po 5 s jest, po 10 s nie ma |
| Regresja | test „Zakończ prezentację” z ISSUE-034 na 5 s; test tempa z ISSUE-037 na „Średnio”; wejście z paska i „Pokaż w drzewie” dalej „dziś” (D37); podpowiedź D26 bez zmian |

### Manual verification — agent na emulatorze (`Grobing_Restore`, build profile; przed stopem #2, ze zrzutami)
1. Karta: przycisk tempa po kolei przez trzy tempa; ▶ od początku przy każdym — czas do „dziś” zmierzony (AC-2); zmiana tempa w trakcie ▶.
2. „Przesyłaj na telewizor” → ekran systemu → wstecz → tryb; pusty dotyk → listwa i „Zakończ”; ▶; rok w rogu; po 5 s sterowanie znika; drugi pusty dotyk chowa; koniec ▶ → „dziś”
   3 s (AC-1).
3. Karta na 1950 → tryb → 1950 → „Zakończ prezentację” → karta na 1950 (AC-4).
4. „Usuń animacje” → ▶ przy każdym tempie, odstęp skoków (AC-3); po kroku ustawienie z powrotem.
5. Tekst 200% na 360 dp: karta i tryb poziomo (AC-5); czytnik przez `uiautomator dump`: tempo, rok w rogu, listwa.
6. „Czas na działanie” 10 s przez adb (krok 0) → sterowanie znika po ok. 10 s; ustawienie z powrotem (AC-6).
7. `FRAME_LOG` przy „Szybko” w trybie, naprzemiennie z buildem odniesienia (D6).

### Manual verification — autor: odczucie (najwyżej 3)
1. **Emulator:** w karcie dotknij ▶ przy „Średnio”, potem przełącz na „Wolno” — czy któreś tempo pasuje do oglądania historii z rodziną.
2. **Emulator, poziomo:** „Przesyłaj na telewizor” → wstecz, dotknij pustego miejsca i ▶ — czy rok w rogu i listwa na chwilę wyglądają jak coś, co chcesz pokazać na telewizorze.
3. **Emulator:** ustaw w karcie rok 1950 i wejdź w tryb — czy to, że tryb zaczyna od 1950, a nie od „dziś”, jest naturalne.

### Out of Scope (plan)
- **Imiona na telewizorze** — 13 sp to z kanapy 8–17′, poniżej minimum 16′ na telewizorach do 55″ ([[drzewo]] *Candidates — ISSUE-038* → *Zauważone*). To I2 (D27), osobna decyzja;
  przy zamknięciu wiersz na [[ISSUE-032-mvp-install]] → *Hand checks* (telewizor autora) i wejście do [[2026-10-14-opowiesc-rodziny-i-wieniec]].
- Tempo zapamiętane po zamknięciu aplikacji (D41 → *Obali*: osobna pozycja, zmiana tabeli `Settings`).
- Animacje związków, zbliżenia na zdarzenia, wieniec przy portrecie → [[2026-10-14-opowiesc-rodziny-i-wieniec]].
- Google Cast i odbiornik na telewizorze — obraz dalej przesyła system ([[drzewo]] D11, D29).
- Czytelność roku na prawdziwym telewizorze autora (proporcje obrazu po przesłaniu, D38 → *Obali*) → [[ISSUE-032-mvp-install]] → *Hand checks*.

### Risks
- **`tree_screen.dart` (1815 linii) i trzy timery w trybie** (`_pillTimer`, `_exitTimer`, zegar ▶): łatwo o timer, który chowa sterowanie w trakcie przeciągania suwaka. Dotknięcie
  w listwie odnawia 5 s, a przeciąganie trzyma sterowanie (test AC-1).
- **Czytnik w trybie:** do dziś tryb nie miał nic poza osobami i „Zakończ”; listwa wraca do drzewa semantyki tylko wtedy, gdy ją widać. Krok 0 (b) mówi, jak to sprawdzić na emulatorze.
- **Kanał D4 na innych telefonach:** metoda z Androida 10, `minSdk` 24 — warunek wersji i 5 s przy błędzie, jak `openCastSettings` przy braku ekranu.

## Dev report
> `dev`, 2026-10-14. Flutter 3.41.1 (przypięty). `dart format` i `flutter analyze` — bez uwag. Nowych testów nie pisałem (`qa`). Obecne testy drzewa: 33 zielone, 6
> czerwonych — wszystkie przez zmiany zapisane w planie (lista dla `qa` niżej).

### Krok 0
- **(a) „Czas na działanie” przez adb:** `settings put secure accessibility_interactive_ui_timeout_ms 10000` → `dumpsys accessibility` pokazuje `interactiveUiTimeout=10000`, a
  aplikacja trzyma sterowanie ok. 10 s (przejście, krok 6). `settings delete …` przywraca 0. Klucz jest `@hide`, ale `@Readable` (źródła SDK 36, `Settings.java`).
- **(b) `accessibleNavigation`:** silnik Fluttera (`AccessibilityBridge.java` w SDK 3.41.1) ustawia go, gdy usługa ułatwień dostępu poprosi o węzeł semantyki
  (`createAccessibilityNodeInfo` → `setAccessibleNavigation(true)`), a zdejmuje, gdy dostępność albo eksploracja dotykiem się wyłączy. Obejmuje więc TalkBack, Switch Access i Voice
  Access. **`uiautomator dump` go nie zostawia:** po odczycie sterowanie schowało się normalnie po 5 s (zrzut `19-after-7s`), więc przejście z odczytem semantyki nie fałszuje
  pomiaru chowania. TalkBack na `Grobing_Restore` przy pierwszym włączeniu pokazał systemowe okno zgody na powiadomienia i zabrał na nie fokus — krok nierozstrzygnięty (*Not
  checked live* dla `qa`; pokrywa go test widżetu z `accessibleNavigation: true`).

### Files (`{code}`)
| Plik | Zmiana |
|---|---|
| `lib/app/tree/tree_time.dart` | `TreeTempo` (`slow` 5, `medium` 10, `fast` 20 lat/s; `label`, `spoken`, `yearStep`, `decadeStep`, `next`) i `treeTempo` — tempo na czas działania aplikacji, domyślnie „Średnio” (D41) |
| `lib/app/tree/tree_time_bar.dart` | przycisk tempa (14 sp, waga 500, kolor tekstu, cel 48 dp, `Tooltip` i czytnik „Tempo historii: średnio — zmień”), szerokość najszerszego słowa; przy ≥ 150% w górnym rzędzie między latami (`Wrap`); `oneRow` — listwa trybu bez roku na końcu; `onSlide` — palec na suwaku |
| `lib/app/tree/tree_presentation.dart` (nowy) | `PresentationYear` (L1: 36 sp × skala tekstu najwyżej 1,3, akcent, tabliczka 8 dp / 6 dp, czytnik „Rok 1950” / „dziś”), `PresentationBar` (powierzchnia, 16 dp, 24 dp od krawędzi), `PresentationExit` (przeniesione z `tree_screen.dart`) |
| `lib/app/tree/tree_screen.dart` | zegar ▶ z tempa (`yearStep`, przy `disableAnimations` — `decadeStep`); `_nextTempo` — zmiana w trakcie ▶ od bieżącego roku; tryb: `_toggleControls` (pusty dotyk pokazuje i chowa), `_armControls` (5 s albo czas z kanału; bez timera przy czytniku i palcu na suwaku), rok w rogu (gdy nie „dziś”, ze sterowaniem i 3 s po końcu ▶), listwa i „Zakończ prezentację”; `_present` bez `_setYear(null)` (Z2), ▶ stoi; `_leave` zostawia rok |
| `lib/app/external_link.dart` | `recommendedTimeout(Duration)` — nigdy nie rzuca: odpowiedź inna niż liczba, błąd kanału albo brak wtyczki → podany czas |
| `android/…/ExternalLinks.kt` · `MainActivity.kt` | metoda `recommendedTimeout` — `getRecommendedTimeoutMillis(ms, FLAG_CONTENT_CONTROLS or FLAG_CONTENT_TEXT)` od Androida 10, niżej `ms`; `ExternalLinks` dostaje `applicationContext` |

Bez nowej zależności, sieci i uprawnień; schemat bez zmian.

### Found on the emulator and in the tests (poprawione przed `qa`)
- **a) Kanał rzucał błąd typu:** udawany kanał w testach ISSUE-036 odpowiada `true` na każdą metodę, a `invokeMethod<int>` rzucał `_TypeError`, którego nie łapała ani
  `PlatformException`, ani `MissingPluginException` — wejście w tryb kończyło się błędem w teście. Odczyt jako `Object?` i sprawdzenie `is int` — funkcja nie rzuca nigdy (D4).
- **b) Górny rząd karty przy 200% przepełniał się w czcionce testowej** (kwadraty: „1860 · Średnio · 8888” > 336 dp). Na emulatorze w Roboto mieści się (zrzut `16`), ale `Row` ze
  `Spacer` nie ma wyjścia na węższy telefon — `Wrap(spaceBetween)`: w jednej linii wygląda tak samo, a gdy się nie mieści, rok przechodzi do następnej zamiast się ucinać.

### Measurements (emulator `Grobing_Restore`, build profile, `FRAME_LOG`; naprzemiennie z buildem ISSUE-037 z emulatora — D6)
| Runda | Odniesienie — ▶ w karcie (~21 lat/s) | Nowy — ▶ w karcie, „Szybko” (20 lat/s) | Nowy — ▶ w trybie, „Szybko”, rok w rogu |
|---|---|---|---|
| 1 | 15,4% wolnych klatek (260) | 8,9% (282) | 8,8% (284) |
| 2 | 8,8% (262) | 11,1% (261) — runda powtórzona osobno | 5,3% (281) |
| 3 | 14,6% (261) | 5,2% (288) | 8,2% (280) |

Nowy build w szumie odniesienia (8,8–15,4%): w karcie 5,2–11,1%, w trybie 5,3–8,8% — **D6 spełnione** (≤ 10% albo nie gorzej niż odniesienie w tym samym przebiegu; jedno 11,1%
z rundy bez pary). Rok w rogu i listwa mają własne warstwy (`RepaintBoundary`). Odniesienie: APK zainstalowany na emulatorze z ISSUE-037 (`base-037.apk` w katalogu sesji).

**Tempo zmierzone na emulatorze (od 1860):** „Średnio” — 1890 po 3,2 s, 1934 po 7,7 s (ok. 10 lat/s); „Szybko” → „Wolno” w trakcie ▶ — 1891 tuż po zmianie, 1909 po 3 s (ok. 6
lat/s z opóźnieniem zrzutu); „Usuń animacje” — „Średnio” 1950 → 1970 w 2,5 s, po zmianie na „Szybko” 1980 → 2010 w 1,6 s (dekada co ok. 0,5 s).

### Deviations
1. **Z czytnikiem sterowanie jest od wejścia w tryb i nie chowa się wcale** (spec D40: „nie chowa się samo — znika po pustym dotyku”). Pusty obszar nie ma węzła semantyki, więc
   TalkBack ani Switch Access nie umieją go dotknąć: schowane sterowanie byłoby dla nich nie do odzyskania. Wyjście: „Zakończ prezentację” albo wstecz.
2. **Górny rząd przy ≥ 150% to `Wrap`** (Found b) — na telefonie 360 dp przy 200% wygląda jak w specyfikacji; inaczej tylko wtedy, gdy trzy elementy się nie mieszczą.
3. **Przycisk tempa ma szerokość najszerszego słowa** („Średnio”) — nie było w specyfikacji; ten sam powód co rok w v1.13 (tor suwaka nie zmienia długości przy przełączaniu).

### Emulator pass (AC, *States*, zrzuty w katalogu sesji `baf00b7b-…\scratchpad\shots-emu\`, same wymyślone osoby)
- **AC-2:** przycisk po kolei „Średnio” → „Szybko” → „Wolno” → „Średnio”, tor suwaka tej samej długości (`03-tempo`); tempo w karcie i w listwie to samo, zostaje po wyjściu z trybu i po
  nowym drzewie z zakładki (`16`); zmiana w trakcie ▶ nie zatrzymuje (`06`).
- **AC-1:** wstecz z ekranu „Google Cast” → tryb (`09`); pusty dotyk → listwa i „Zakończ prezentację” (`10`), przy 4,9 s są, przy 7,3 s nie ma; drugi pusty dotyk chowa od razu
  (`11-hidden`); ▶ z listwy → rok w rogu biegnie (1996, 2024), po końcu „dziś” (`12-dzis`) i znika (`12-gone`). Rok w rogu nie przykrył nikogo przy „Ja” w środku (`09`, `10`).
- **AC-4 (Z2):** karta na 1979 → tryb pokazuje 1979, ▶ stoi (`09`); w trybie suwak na 1950 → „Zakończ prezentację” → karta na 1950 (`13`).
- **AC-3:** „Usuń animacje” — dekadami, odstęp według tempa (`15`); ustawienia z powrotem na 1.
- **AC-5:** 200% na 360 dp — karta: „1860 · Szybko · 2020” w górnym rzędzie, ▶ i suwak pod nim, nic nie ucięte (`16`); tryb: listwa w jednym rzędzie, „Zakończ prezentację” rośnie, rok
  w rogu ok. 47 sp (`17`, `18`). **Do przeglądu `ui`:** przy 200% z Michałem w środku drzewo jest szersze niż ekran i tabliczka „2020” przykrywa okrąg Zofii (`18`) — przypadek z
  D39 → *Obali* (w makiecie przy 200%: 2 ze 106 środków).
- **AC-6:** „Czas na działanie” 10 s → listwa jest przy 6,7 s, znika przed 10,9 s (`14`); bez ustawienia — 5 s. Czytnik — nierozstrzygnięty na emulatorze (krok 0 b).
- **Semantyka** (`uiautomator dump`): karta — ▶ 48 × 48 dp, suwak „dziś, Rok”, „Tempo historii: szybko — zmień” 65 × 48 dp, wszystkie `clickable`; tryb — „Rok 2020” (bez akcji),
  „Zakończ prezentację”, „Odtwórz historię”, suwak „2020, Rok”, tempo (`19-pres.xml`, `23-card.xml`).

### Dla `qa` — testy, które zmieniają oczekiwania (według planu)
- `tree_time_screen_test.dart` — „▶ from 1860 about 21 years a second” i „❚❚: the reader hears the year once” liczą lata przy ~21 lat/s; domyślne tempo to teraz „Średnio” (10 lat/s).
  Test 200% („the two years in a row”): w czcionce testowej rok przechodzi do drugiej linii (`Wrap`, Found b).
- `tree_screen_test.dart` — „the empty space shows „Zakończ prezentację” for 3 s” → 5 s (D3); trzy testy ISSUE-036 oczekują wywołań kanału `['openCastSettings']`, a teraz jest też
  `recommendedTimeout`.
- `treeTempo` jest globalne na czas procesu (D5) — w testach `setUp` przywraca `TreeTempo.medium`.

**Emulator:** `Grobing_Restore` ma build profile ISSUE-038 (`FRAME_LOG`), tekst 100%, gęstość i animacje domyślne, „Czas na działanie” usunięty, TalkBack wyłączony; okno zgody TalkBack na
powiadomienia zamknięte „Nie zezwalaj”.

### Found by `qa` and the `ui` review (poprawione przed stopem #2)
- **c) Tabliczka roku przechwytywała dotyk** (test `qa` „L1 — the year in the corner takes no touch”, MAJOR w przeglądzie `ui`): `DecoratedBox` łapie trafienie, więc osoba i puste
  miejsce pod rokiem nie reagowały. `IgnorePointer` wokół tabliczki, jak pigułka poziomu; etykieta „Rok …” zostaje dla czytnika (test AC-5). Na emulatorze dotknięcie roku chowa
  sterowanie jak pusty dotyk (`27-tap-on-year`).
- **d) Poziom 2 w trybie nie był dopasowany przy 200% z Michałem w środku** (MAJOR w przeglądzie `ui`, zrzut `18`) — **usterka z [[ISSUE-034-tree-presentation-mode]], poprawka poza
  pierwotnym zakresem, zgłoszona na stopie #2.** W `_fitted()` porównanie `size × scale <= room − 2 × margin` na osi, z której wzięła się skala, przegrywało o ułamek przez zaokrąglenie
  liczb zmiennoprzecinkowych. Kod uznawał wtedy, że oś się nie mieści, i stawiał drzewo wokół osoby w środku: z lewej ucięci Józef, Halina i Jan, z prawej ok. 230 dp pustego. Dlatego
  tabliczka „2020” przykryła Zofię. Poprawka: 0,5 dp luzu w porównaniu (jedna linia). Po niej przy tym środku widać cały poziom, a rok kończy się przed Józefem (`26-michal-200`,
  `27-year`) — D39 → *Obali* nie zachodzi. Test „element 11, D16 — at 200 % each person put in the middle gets level 2 fitted” sprawdza trzy środki. Czcionka testowa tej granicy nie
  trafia, więc test chroni przed regresją dopasowania, a samą usterkę pokazał emulator.

## Verification
> `qa`, 2026-10-14. Rytuał WZ-024: `dart format --set-exit-if-changed lib test` — bez zmian · `flutter analyze` — bez uwag · `flutter test --timeout 120s` — **754 zielone**, 0
> czerwonych (przed pozycją 742; +12 nowych, 6 zmienionych oczekiwań).

### Tests (`{code}/test/`)
| AC | Test |
|---|---|
| AC-1 | `tree_presentation_test.dart` — pusty dotyk → listwa i „Zakończ prezentację”, przy 4,9 s są, przy 5,1 s nie; drugi pusty dotyk chowa; ▶ z listwy → rok w rogu 1880 po 2 s, 1900 po 4 s przy schowanej listwie; po „dziś” napis „dziś” 3 s; ❚❚ w listwie; rok 48 dp od lewej i 24 dp od góry. Ten sam plik: palec na suwaku trzyma sterowanie 8 s, dotknięcie tempa w listwie odnawia 5 s; dotknięcie tabliczki roku dochodzi do drzewa (L1) |
| AC-2 | `tree_time_test.dart` — wartości, kolejność i kroki `TreeTempo`, od 1880 ok. 29 · 15 · 7 s; `tree_time_screen_test.dart` — przycisk „Średnio” → „Szybko” → „Wolno” → „Średnio”, tor tej samej długości, ▶ od 1860 po 3,5 s 1895 · 1930 · 1877 (jak `#playtest` makiety), czytnik „Tempo historii: średnio — zmień”; zmiana w trakcie ▶ (1880 → 1890 w 2 s przy „Wolno”), tempo zostaje dla nowego drzewa |
| AC-3 | `tree_time_screen_test.dart` — „Usuń animacje”: dekada co 2 · 1 · 0,5 s według tempa; test R2 z ISSUE-037 bez zmian |
| AC-4 | `tree_presentation_test.dart` — karta na 1950 → tryb z rokiem 1950, ▶ stoi, 6 węzłów (5 osób i pierścień „Ja”); suwak w listwie na 1930 → „Zakończ prezentację” → karta na 1930 |
| AC-5 | `tree_time_screen_test.dart` — 200% na 360 dp: tempo w rzędzie lat, wszystko w karcie, ▶ i suwak pod spodem; `tree_presentation_test.dart` — listwa w jednym rzędzie przy 200%, rok `textScaler` = 1,3 × 36 sp, cele sterowania ≥ 48 dp; dopasowanie poziomu 2 przy 200% (Found d) |
| AC-6 | `tree_presentation_test.dart` — `accessibleNavigation: true`: sterowanie od wejścia, po 8 s i po pustym dotyku dalej jest; kanał udawany z 10 000 ms: przy 9,9 s jest, przy 10,1 s nie |
| Dostępność (retro 3, R2) | `meetsGuideline` (`androidTapTargetGuideline`, `labeledTapTargetGuideline`, `textContrastGuideline`) i „każdy przycisk ma akcję dotknięcia” na karcie z tempem i na trybie ze sterowaniem przy 100%. Przy 200% w trybie cel dotyku sprawdzony na sterowaniu, nie na całym ekranie: węzły dopasowanego drzewa przy skali ok. 0,44–0,55 schodzą poniżej 48 dp — wyjątek D17 ([[style-b]] *Thresholds*) |
| Regresja | `tree_screen_test.dart` — „Zakończ prezentację” i listwa 5 s (D3, było 3 s); testy ISSUE-036 z wywołaniami `openCastSettings` i `recommendedTimeout`; `tree_time_screen_test.dart` — test ▶ i czytnika przy ❚❚ na „Średnio” (1880 zamiast 1901); test 200% z nowym rzędem |

### Review `ui` (subagent, przed stopem #2)
0 BLOCKER, **2 MAJOR — poprawione** (Found c, d), 1 MINOR: „dziś” i „Średnio” stoją ok. 8 dp od siebie, a przycisk w kolorze tekstu nie wygląda na dotykalny — zgodne ze specyfikacją i
regułą 1, bez zmiany; obserwacja w kroku 1 autora. Trzy odstępstwa `dev` przyjęte → [[drzewo]] v1.15, [[style-b]] v1.31 (reguła 5: stała szerokość zmiennego napisu). Sprawdzone i zgodne:
elementy i kolejność, stany, role kolorów, pary kontrastu z `theme.dart` (rok w rogu 8,81:1, akcent na powierzchni 8,04:1, tempo i „Zakończ” 10,02:1, rok początku 5,01:1, tor 3,10:1,
obrys 3,40:1), cele ≥ 48 dp, kolor nie jest jedynym nośnikiem, próg „tekst dla telewizora”, tylko wymyślone osoby na zrzutach.

### Family data
W zmianach kodu, testów i vaulta tylko wymyślone osoby z fixture'a (rdzenie Wymyśl-, Zmyśl-, Testow-, Przykład-); żadnych `*.db`, kopii, eksportów ani zdjęć. Zrzuty, makieta, APK i
dumpy w katalogu tymczasowym sesji, poza repo. Bez sieci (logcat bez współrzędnych — nie dotyczy).

### Not checked live
- TalkBack w trybie prezentacji (sterowanie od wejścia, rok w rogu bez ogłaszania w trakcie ▶) — na emulatorze okno zgody TalkBack zabrało fokus; pokrywa test z `accessibleNavigation`.
- Czytelność roku z kanapy na telewizorze autora i to, czy obraz telefonu wypełnia szerokość telewizora (D38 → *Obali*).
- Imiona w trybie prezentacji z kanapy — 13 sp to ok. 14′ z 3 m na 55″, poniżej 16′ (*Candidates — ISSUE-038* → *Zauważone*; I2, D27).
- „Czas na działanie” na telefonie autora (Android 10+, wartość z ustawień, nie z adb).

### Stop #2 (2026-10-14) — autor: *„Pomiń”*
Wszystkie trzy kroki odczucia „pomiń” (tempo w karcie i czy „Średnio” wygląda na przycisk · rok w rogu i listwa jako obraz na telewizor · tryb od roku 1950). Zapisane, nie blokuje
(`DEFINITION_OF_DONE.md`, R8). Kroki agenta zrobione przed stopem, ze zrzutami (*Dev report* → *Emulator pass*, Found c, d).

### For ISSUE-032 → Hand checks (po jednym w linii)
- ISSUE-038, krok 1 „pomiń”: tempo „Średnio” / „Wolno” przy oglądaniu historii z rodziną; czy przycisk tempa obok „dziś” wygląda na dotykalny (MINOR przeglądu `ui`).
- ISSUE-038, krok 2 „pomiń”: rok w rogu i listwa w trybie prezentacji na prawdziwym telewizorze — czy to obraz do pokazania.
- ISSUE-038, krok 3 „pomiń”: tryb prezentacji otwarty z roku z karty (Z2) — czy start od 1950, a nie od „dziś”, jest naturalny.
- ISSUE-038, nieprzetestowane na żywo: TalkBack w trybie prezentacji — sterowanie od wejścia, rok w rogu bez ogłaszania w trakcie ▶.
- ISSUE-038, nieprzetestowane na żywo: czytelność roku z kanapy na telewizorze autora i czy obraz telefonu wypełnia szerokość telewizora (D38 → *Obali*).
- ISSUE-038, nieprzetestowane na żywo: imiona w trybie prezentacji z kanapy (13 sp ≈ 14′ z 3 m na 55″, poniżej 16′; I2, D27).
- ISSUE-038, nieprzetestowane na żywo: „Czas na działanie” z ustawień telefonu wydłuża sterowanie w trybie (Android 10+).

### Verdict
**APPROVED** (self-check, z uwagami). AC-1–AC-6 mają testy happy-path i przejście na emulatorze; 754 testy zielone. Uwagi: dwie usterki z przeglądu `ui` poprawione przed stopem, w tym
jedna z ISSUE-034 poza pierwotnym zakresem (Found d, zgłoszona na stopie #2); stop #2 „pomiń” we wszystkich krokach — siedem wierszy na [[ISSUE-032-mvp-install]] → *Hand checks*.
Szukałem i nie znalazłem: danych rodziny w zmianach, nowej zależności, sieci i uprawnień, zmian schematu, przycisku bez akcji dotknięcia, pary kontrastu poniżej progu, celu sterowania
poniżej 48 dp.

### Package for `docs` (pliki, które ta pozycja zapisała)
- `grobing-code`: `android/app/src/main/kotlin/com/grobing/app/ExternalLinks.kt` · `android/app/src/main/kotlin/com/grobing/app/MainActivity.kt` · `lib/app/external_link.dart` ·
  `lib/app/tree/tree_presentation.dart` (nowy) · `lib/app/tree/tree_screen.dart` · `lib/app/tree/tree_time.dart` · `lib/app/tree/tree_time_bar.dart` ·
  `test/app/tree/tree_presentation_test.dart` (nowy) · `test/app/tree/tree_screen_test.dart` · `test/app/tree/tree_time_screen_test.dart` · `test/app/tree/tree_time_test.dart`.
- `grobing-vault`: `backlog/issues/ISSUE-038-history-on-tv-and-tempo.md` · `05_DESIGN/drzewo.md` · `05_DESIGN/brand/style-b.md` · `00_START_HERE/TRACEABILITY.md` — oraz to, co
  dopisze `docs` przy zamknięciu (`CURRENT_STATE.md`, US-010 AC-3, ISSUE-032 → *Hand checks*).
- `grobing-agents`: bez zmian.
