---
title: "ISSUE-046 — Icons: the launcher icon and the in-app icons, options compared on a mockup"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-18
verdict-reviewer: self-check
source: "`/pm` 2026-10-16 — autor: obecne ikony „wyglądają tak mało ciekawie”; DALL-E (prompty od agenta, grafiki od autora); „w ramach wizualizacji w html pokażesz mi, jak to może wyglądać i jakie mamy opcje” · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-18
---

# ISSUE-046 — Ikony

> Dwie różne rzeczy: **ikona aplikacji** na ekranie telefonu (dziś domyślna ikona Fluttera — `mipmap-*` bez zmian od
> [[ISSUE-002-bootstrap-code-repo]]; sklep chce ikony 512 × 512) i **ikony w aplikacji** (ok. 70 różnych, Material Icons „outlined” — [[style-b]]
> reguła 3). Autor chce spróbować DALL-E dla obu i wybrać na makiecie. **Bez zmiany bazy.** Prompty idą od razu, żeby autor generował,
> kiedy łańcuch pracuje nad wcześniejszymi pozycjami.

## What to build
1. **`ui`: prompty do DALL-E** w stylu B — ikona aplikacji jako ikona adaptacyjna Androida (symbol na środku w strefie bezpiecznej, płaskie
   tło, wersja jednobarwna do motywów Androida 13+) i próbka ikon w aplikacji (najczęściej widoczne: zakładki, dodaj zdjęcie, pinezka,
   edycja, przesyłanie na telewizor).
2. **`ui`: makieta HTML z opcjami** (link `file:///`, retro 4 R1): **A** — obecne · **B** — Material Symbols z cieńszą kreską (grubość jednym
   parametrem, [`Icon.weight`](https://api.flutter.dev/flutter/widgets/Icon/weight.html), pakiet
   [`material_symbols_icons`](https://pub-web.flutter-io.cn/packages/material_symbols_icons/example)) · **C** — z DALL-E. Każda w prawdziwym
   rozmiarze (24 dp), w bursztynie i w kolorze tekstu pomocniczego, przy tekście 200%. Autor wybiera.
3. Plan i budowa według wyboru: ikona aplikacji (adaptacyjna + jednobarwna) i ikony w aplikacji; zmiana reguły 3 w [[style-b]], jeśli wybór
   ją zmienia. Nowa zależność → sprawdzenie, że nie wysyła danych ([[NFR-005-dane-nie-opuszczaja-telefonu]]).

## Acceptance Criteria
- **AC-1** *Given* telefon autora *Then* na ekranie głównym jest ikona Grobing w stylu B (także w motywie jednobarwnym), nie ikona Fluttera.
- **AC-2** *Given* wybrana opcja *Then* ikony w aplikacji są z jednej rodziny, mają kontrast ≥ 3:1 (WCAG 2.2 SC 1.4.11), rosną z tekstem, a cele
  dotyku zostają ≥ 48 dp.

## Notes
- Ryzyka opcji C (do pokazania na makiecie, nie do zgadywania): obraz rastrowy przy 24 dp, kolor zależny od stanu, spójność kilkudziesięciu
  ikon.

## Implementation plan
> `planning`, 2026-10-18. **Pozycja wybiera to, co widać** (retro 2, R6): kandydaci, pomiary i rekomendacja `ui` — [[style-b]] v1.37 → *Candidates — ISSUE-046*
> (reguły bez zmian do wyboru). Makieta: `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/1f978d57-48d1-4755-8e05-34fca0f9c30d/scratchpad/makieta-046/ikony-046.html`.
> Bez US (task-level, jak ISSUE-043 i ISSUE-045), brief §6a · N7. **Bez zmiany bazy** — bez migracji i bez próbnego odtworzenia; jedyna granica danych to nowa
> zależność (NFR-005).

> **Stop #1 — w toku (2026-10-18).** Autor uznał pierwsze proste ikony z DALL-E za „zbyt proste”. Prompty przepisane: metafory Grobing (mapa z
> trasą, rodzina z dzieckiem, drzewo liściaste z kropkami, stare zdjęcie, pinezka ze zniczem, stalówka), detale, dwa tony. O arkuszu bursztynowym
> (`_ikony-dalle\C-arkusz-bursztyn.png`, poza repo) autor napisał: *„to jest kierunek, w który chcę iść”* → **kierunek ikon w aplikacji: bursztyn, dwa tony
> (linia + wypełnienie ok. 25%), charakter.** Otwarte zostaje: technika (C — obrazy z DALL-E jako maski · B z wypełnieniem 25%), pytania 2–3 i ikona
> aplikacji — autor generuje ją w tym samym kierunku. **Ikona aplikacji (autor, 2026-10-18):** dwie koncepcje z DALL-E — `L1-znicz.png` (znicz z
> perforowaną pokrywką, bez krzyża) i `L2-drzewo.png` (drzewo z kropkami i płomieniem) w `_ikony-dalle`; L3 nie powstała (*„chyba mamy już wszystko”*).
> Wersje jednobarwne wyprowadzone z kolorowych (same linie), nie generowane. Komplet na makiecie → pytania po kolei.
>
> **Decyzja 1 (autor, 2026-10-18: *„B”*) — ikony w aplikacji: B w kierunku arkusza:** Material Symbols, końce zaokrąglone, grubość 300, **wypełnienie 25%**
> (glif wypełniony pod glifem z kreską), **metafory z arkusza** — `ink_pen` zamiast `edit`, `add_photo_alternate` zamiast `add_a_photo`. C (obrazy z arkusza)
> odrzucone: detale znikają przy 24 dp, 9 z 77 ikon.
>
> **Decyzja 3 (autor, 2026-10-18: *„Zrób tak jak rekomendujesz”*) — zakładka „Drzewo” i „Pokaż w drzewie”: `nature` (drzewo liściaste)**, jak drzewo z
> arkusza i gałązka w R1. Rekomendacja `ui` zmieniona z `family_history` po wyborze arkusza; `park` (iglaste) odpada — reguła 8.
>
> **Decyzja 2 (autor, 2026-10-18: *„Rośnie”*) — ikona obok tekstu rośnie z tekstem** (przyciski, nagłówki sekcji, wiersze); pasek ekranu i dolne zakładki
> zostają 24 dp. AC-2 tak, jak je zapisano; krok 4 planu w mocy.
>
> **Decyzja 4 (autor, 2026-10-18: *„L1”*) — ikona aplikacji: L1, znicz z DALL-E** (`_ikony-dalle\L1-znicz.png`, poza repo). V i L2 odrzucone (L2 powtarzałoby
> ikonę zakładki „Drzewo”). **Stop #1 zamknięty decyzjami 1–4** → `dev`.

### Plan after stop #1 — zmiany względem kroków niżej
Kroki 1–7 zostają; decyzje 1–4 zmieniają w nich tyle:
- **Krok 2 + 3 — dwa tony:** nowy widżet `GrobingIcon` (`lib/app/widgets/grobing_icon.dart`): ten sam glif dwa razy w jednym pudełku — pod spodem `fill: 1` w
  kolorze ikony przy kryciu 25%, na wierzchu `fill: 0`; kolor i rozmiar z argumentów albo z `IconTheme` (żeby `NavigationBar`, `AppBar` i stany wybrane działały
  jak dziś); `semanticLabel` raz. Podmiana w kroku 3 to `Icon(Icons.x…)` → `GrobingIcon(Symbols.x_rounded…)`. Wypełnienie to dekoracja — znaczenie i kontrast
  ≥ 3:1 niesie kreska (SC 1.4.11).
- **Krok 3 — metafory:** `edit_outlined` → `Symbols.ink_pen_rounded`, `add_a_photo_outlined` → `Symbols.add_photo_alternate_rounded`; zakładka „Drzewo” i „Pokaż w
  drzewie” → `Symbols.nature_rounded`. Reszta według mapy `ui`.
- **Krok 4 — „rośnie”:** w mocy (decyzja 2).
- **Krok 5 — ikona aplikacji L1 zamiast V:** skrypt `tool/icons/` czyta `L1-znicz.png` spoza repo (ścieżka w argumencie, jak przy wieńcach), robi maskę z kanału
  czerwonego (tło → 0, linia → 1), barwi ją akcentem `#E3A646` i kładzie na `grobing_background`: pierwszy plan `mipmap-*/ic_launcher_foreground.png` (108 dp na
  gęstość, symbol dłuższym bokiem ok. 61% warstwy — w strefie 66 dp), warstwa jednobarwna `mipmap-*/ic_launcher_monochrome.png` (same linie, próg dobrany
  tak, żeby wnętrze znicza nie robiło się pełną plamą — na makiecie próg 0,55 dał ciemny pas w środku), stare `mipmap-*/ic_launcher.png` i 512 × 512 do sklepu
  poza repo. `ic_launcher.xml` w `mipmap-anydpi-v26` z tłem `@color/grobing_background`. Wektor V (`drawable/*.xml`) odpada. Źródło L1 nie wchodzi do repo.
- **Krok 6 (`ui`):** reguły 3 i 8 w [[style-b]] — robione od razu po stopie (v1.38).
- **Testy:** dochodzi test `GrobingIcon` — dwie warstwy (`fill` 1 przy 25% i `fill` 0), kolor z `IconTheme`, rozmiar ze skalą tekstu przy „rośnie”, jeden opis
  dla czytnika.

### Decisions for stop #1 (author) — jedno pytanie na raz
Pytania z [[style-b]] → *Candidates — ISSUE-046* → ⚠️ OPEN 1–4. **1 (A · B · C) i 4 (V · L1–L3) czekają na obrazy z DALL-E** — decyzja autora w `/pm`
2026-10-18: wybór przy komplecie. Pytania 2 (ikona obok tekstu przy 200%) i 3 (zakładka „Drzewo”) da się rozstrzygnąć na makiecie już teraz. Plan niżej
rozpisuje rekomendację `ui` (**B · zaokrąglone · 300 · rośnie obok tekstu · `family_history` · V**) i mówi, co się zmienia przy innym wyborze.

### Decisions taken in the plan (visible at stop #1, no question)
- **Najpierw sonda, potem masowa podmiana** (B): jedna ikona Symbols w buildzie release przy 300 i 400 obok siebie, zrzut z emulatora. Sonda `ui` pokazała, że
  wycinanie fontu zostawia oś grubości; czy silnik ją rysuje na telefonie, pokaże dopiero build. Nie rysuje → STOP, wracamy z tym na stop #1.
- **Pakiet przypięty dokładnie** (`material_symbols_icons: 4.2960.0`), z komentarzem jak przy kryptografii i mapie: same fonty, Apache-2.0, zależy tylko od
  `flutter`, wymaga Darta ≥ 3.0 (mamy 3.11 — Flutter 3.41.1 zostaje, ADR-002). `pubspec.lock` bez nowych zależności przechodnich, inaczej STOP.
- **Ikona aplikacji adaptacyjna z warstwą jednobarwną** (Android 8+ i motywy Androida 13+), a stare `mipmap-*/ic_launcher.png` przebudowane z tego samego
  źródła, bo `minSdk` = 24 (Android 7 nie zna ikon adaptacyjnych). Ikona do sklepu (512 × 512) powstaje tym samym skryptem **poza repo** — wgrywa ją autor w
  [[ISSUE-032-mvp-install]] → *Before install* 0.
- **Znicz (`CandleIcon`) bez zmian** — to on jest wzorcem grubości.

### Steps
1. **Sonda grubości (B):** `material_symbols_icons` w `pubspec.yaml`; jedno miejsce z `Symbols.edit_rounded` przy `weight` 300 i 400; build release na `Grobing_Restore`
   (przed tym zapis stanu emulatora do `C:\Programowanie\Grobing\_pokaz` i stan sprzed pokazu — dane pokazu autora zostają); zrzut. Różnica widoczna → dalej.
2. **Motyw** (`lib/app/theme.dart` → `GrobingTheme.dark`): `iconTheme: IconThemeData(weight: 300, opticalSize: 24, fill: 0, grade: 0)`; `actionIconTheme` —
   `backButtonIconBuilder` i `closeButtonIconBuilder` z `Symbols.arrow_back_rounded` / `Symbols.close_rounded` (wbudowane „wstecz” i „zamknij” rysują inaczej
   `Icons.*` ze starego fontu — 7 jawnych `BackButton` i strzałki w `AppBar`). Sprawdzić na zrzutach, że `NavigationBar` i `AppBar` dziedziczą grubość.
3. **Podmiana ikon:** 77 nazw w ok. 180 miejscach `lib/` → `Symbols.<nazwa>_rounded` według mapy `ui` (bez przyrostka `_outlined`/`_outline`; `people_outline` →
   `group`, `favorite_border` → `favorite`). Zakładka „Drzewo” (`lib/app/tabs.dart`) według pytania 3. Mechanicznie, bez zmiany rozmiarów, kolorów i układu.
4. **Ikona obok tekstu** (pytanie 2 — „rośnie”): `IconThemeData.applyTextScaling: true` w motywie, `false` dla ikon `AppBarTheme` i `NavigationBarThemeData`; usunąć
   ręczne skalowanie, które dziś to robi, bo inaczej skala liczy się dwa razy (`base_preview_screen.dart:248` — strzałka linku; `home_screen.dart:724` — sprawdzić);
   `CandleIcon` obok tekstu (np. „Otwórz cmentarz”) rośnie tak samo. Przejście 200% na 360 × 640 dp po ekranach z ikonami obok tekstu (stała lista AC z retro 3).
   **Przy „stała”** ten krok odpada.
5. **Ikona aplikacji (V):** `res/mipmap-anydpi-v26/ic_launcher.xml` (tło `@color/grobing_background`, pierwszy plan i warstwa jednobarwna);
   `res/drawable/ic_launcher_foreground.xml` — wektor z `_candlePath()` w siatce 108 dp, w strefie 66 dp, płomień wypełniony, kreska 1,9 (makieta `ui`);
   `res/drawable/ic_launcher_monochrome.xml` — ta sama ścieżka. Skrypt `tool/icons/` (wzorem `tool/wreaths/build_wreaths.py`) robi z tej samej ścieżki stare
   `mipmap-*/ic_launcher.png` (48–192 px) i ikonę do sklepu 512 × 512 poza repo. **Przy L1–L3:** pierwszy plan i warstwa jednobarwna jako PNG w `mipmap-*`
   (108 dp na gęstość: 108–432 px) z pliku autora w `_ikony-dalle` — ten sam skrypt; plik źródłowy nie wchodzi do repo.
6. **Wytyczne** (`ui`, po wyborze): reguła 3 w [[style-b]] — rodzina, końce, grubość, rośnięcie; reguła 8 — znicz jako ikona aplikacji; zmiana w *Changelog*.
7. README `grobing-code`: krótka sekcja *Ikony* — skąd ikony w aplikacji (pakiet, grubość w motywie) i jak przebudować ikonę aplikacji (`tool/icons/`).

**Przy A:** kroki 1–3 odpadają, zostają 4 (jeśli „rośnie”), 5, 6. **Przy C:** plan wraca na stop #1 — 9 ikon z arkusza trzeba przerysować do wektora (inaczej
nie zmienią koloru ze stanem i rozmyją się przy 24 dp), a pozostałe 68 zostaje z A albo B; to osobny koszt, którego dziś nie umiem uczciwie oszacować bez obrazów.

### Files likely touched
`pubspec.yaml`, `pubspec.lock` · `lib/app/theme.dart` · `lib/app/tabs.dart` · ok. 40 plików `lib/app/**` z `Icons.*` · `lib/app/widgets/candle.dart` (tylko przy
„rośnie”) · `lib/app/home/base_preview_screen.dart`, `lib/app/home/home_screen.dart` (ręczne skalowanie) · `android/app/src/main/res/mipmap-anydpi-v26/ic_launcher.xml`,
`res/drawable/ic_launcher_foreground.xml`, `res/drawable/ic_launcher_monochrome.xml`, `res/mipmap-*/ic_launcher.png` · `tool/icons/` · `README.md` · testy z
`Icons.*` (14 odwołań w 7 plikach) · vault: [[style-b]] (`ui`).

### AC mapping
- **AC-1** (ikona Grobing w stylu B, także w motywie jednobarwnym) → krok 5; sprawdzenie: zasoby w APK (`aapt dump badging` — ikona adaptacyjna z `monochrome`) i
  zrzut ekranu głównego emulatora z włączonymi ikonami tematycznymi.
- **AC-2** (jedna rodzina · kontrast ≥ 3:1 · rosną z tekstem · cele ≥ 48 dp) → kroki 2–4; kontrast już zmierzony przez `ui` (5,50 i 8,81:1 na tle); cele dotyku —
  przyciski się nie zmieniają, przy „rośnie” sprawdzone przy 200%.

### Tests (`qa`)
- **Jedna rodzina:** test czyta `lib/` i nie znajduje `Icons.` (poza wyjątkami z uzasadnieniem w teście) — strażnik, żeby nowa ikona nie wróciła do starego fontu.
- **Grubość z motywu:** widżet w `GrobingTheme.dark` → `IconTheme.of(context).weight == 300`; przycisk „wstecz” rysuje `Symbols.arrow_back_rounded`.
- **Przy „rośnie”:** przy `TextScaler.linear(2)` ikona w przycisku z podpisem ma 2 × rozmiar, ikona w `AppBar` i w dolnym pasku zostaje 24 dp; strzałka linku
  skalowana raz (32 dp przy 200%, nie 64); `meetsGuideline(androidTapTargetGuideline)` na widoku osoby i grobu przy 200%.
- Istniejące testy z `find.byIcon(Icons.…)` przepisane na `Symbols` — liczba testów nie spada.
- `flutter test --timeout 120s`, `flutter analyze`, `dart format` — zielone.

### Manual verification
**Agent na emulatorze** (przed stopem #2, zrzuty w odpowiedzi): sonda 300/400 (krok 1) · ekran główny Androida z ikoną Grobing — kolorowa i z ikonami
tematycznymi · widok osoby, grobu, mapa, drzewo i „Stan danych” przy 100% i 200% — grubość wszędzie ta sama, „wstecz” i zakładki też · rozmiar APK przed i po
(oczekiwane: + ok. 0,2 MB) · przegląd `ui` ze zrzutów.

**Autor: odczucie** (najwyżej 3, emulator):
1. Ekran główny Androida: ikona Grobing obok innych — czy to znak, który chcesz widzieć na telefonie.
2. Przejdź Mapa → cmentarz → grób → osoba → Drzewo: czy ikony są spokojne i czytelne, nic nie wygląda „z innej bajki”.

Słońce i kreska 300 na prawdziwym ekranie → od razu lista **B** w [[ISSUE-032-mvp-install]] → *Hand checks* (telefon, retro 4 R4).

### Out of scope
- Nowe ikony, nowe działania, zmiana układu ekranów — tylko podmiana kształtu i grubości.
- Znicz (`CandleIcon`) i pinezki — bez zmian.
- Inna rodzina ikon niż A · B · C (np. bliższa R1 rodzina w stylu Lucide) — nie pokazana, poza pozycją.
- Grafika i zrzuty do karty sklepu poza ikoną 512 × 512 — [[ISSUE-032-mvp-install]].

### Obali (falsifiers)
- Build release rysuje 300 tak samo jak 400 → B nie daje cieńszej kreski; STOP i decyzja autora (A albo inne źródło grubości).
- `NavigationBar` albo `AppBar` nie dziedziczy grubości z motywu i nie da się tego ustawić ich motywem → ikony w dwóch grubościach; STOP.
- Kreska 300 w tekście pomocniczym słabo widoczna w słońcu (telefon, lista B) → 400, jednym parametrem w motywie.

### Sources
[[style-b]] v1.37 → *Candidates — ISSUE-046* (pomiary, sonda `font-subset`, kontrast) · [pub.dev — material_symbols_icons](https://pub.dev/packages/material_symbols_icons)
(4.2960.0, Apache-2.0, Dart ≥ 3.0 — odczyt 2026-10-18) · Flutter 3.41.1 SDK: `widgets/icon.dart` (`weight`, `opticalSize`), `widgets/icon_theme_data.dart`
(`applyTextScaling`, domyślnie `false`), `material/action_icons_theme.dart` (`backButtonIconBuilder`, `closeButtonIconBuilder`) — sprawdzone 2026-10-18.

## Dev report
> `dev`, 2026-10-18. `flutter analyze` czyste, `dart format lib` zrobione. Flutter 3.41.1 (przypięty) bez zmian. **Bez zmiany bazy** (v15) i **bez nowej zależności**
> — `pubspec.lock` identyczny jak przed pozycją.

### Probes (krok 1)
- **Sonda 1** (osobna aplikacja w katalogu tymczasowym, build profile z wycinaniem ikon, `Grobing_Restore`): grubość 200 / 300 / 400 rysuje się różnie —
  oś `wght` przeżywa build. **Ale `group` i `settings` wyszły puste.** Bez wycinania (`--no-tree-shake-icons`) są — APK +17 MB (trzy pełne fonty pakietu).
  Przyczyna: Material Symbols podmienia część glifów wzdłuż osi FILL (GSUB, *feature variations*), a `font-subset` Fluttera nie zabiera tych podmian
  (w wyciętym foncie glif jest, ale Chrome rysuje go pełnym, a Flutter wcale). To nie było w falsyfikatorach planu.
- **Sonda 2:** ten sam font wycięty **fontTools z domknięciem układu** (8 ikon → 16 glifów: 7 podmian), zadeklarowany jako zwykły font i rysowany jak tekst —
  wszystkie ikony konturem, grubość działa, dwa tony leżą równo. Wycinacz Fluttera rusza tylko fonty, na które wskazuje `IconData`, więc tego nie tnie.

### Changed (`grobing-code`)
- **Ikony w aplikacji:** `lib/app/widgets/grobing_icon.dart` — `Glyph` (sam kod znaku, celowo nie `IconData`) i `GrobingIcon`: Material Symbols Rounded,
  grubość 300, dwie warstwy (`FILL` 1 przy kryciu 25% pod `FILL` 0), `opsz` = rysowany rozmiar (20–48), rozmiar i kolor z argumentów albo `IconTheme`, jeden
  opis dla czytnika; `applyTextScaling` domyślnie `true`. `lib/app/widgets/glyphs.dart` — 73 stałe (generowane). Font `assets/fonts/grobing-symbols.ttf`
  (211 KB, wersja 2.975, 116 glifów z podmianami) i jego licencja Apache-2.0 obok, w licencjach aplikacji (`main.dart` → `LicenseRegistry`).
- **Narzędzia:** `tool/icons/glyphs.txt` (lista nazw), `tool/icons/build_symbols.py` (fontTools: font + `glyphs.dart`), `tool/icons/build_launcher.py`
  (Pillow: ikona aplikacji). README → *Ikony* (źródło fontu przypięte do commita `49d4db3`, jak przebudować, dlaczego nie `Icon`).
- **Podmiana w kodzie** (skrypt jednorazowy, 40 plików `lib/app/**`): 137 wywołań `Icon(` → `GrobingIcon(`, 179 nazw `Icons.*` → `Glyphs.*`, 20 typów
  `IconData` → `Glyph`, importy. Metafory: `edit` → `inkPen`, `add_a_photo` → `addPhotoAlternate`, `account_tree` → `nature` (zakładka, „Pokaż w drzewie”, segment).
  W `lib/` nie ma ani jednego `Icons.` ani `Icon(`.
- **Rośnie z tekstem** (decyzja 2): domyślnie tak; **53 miejsca stałe** (`applyTextScaling: false`): 26 `IconButton`, dolne zakładki (`tabs.dart`), okrągłe
  przyciski drzewa i mapy migracji, przycisk z samą ikoną cofnięcia kwater, przełącznik płci, przełącznik „Drzewo | Mapa”, ikony w pudełkach o stałym rozmiarze
  (miniatury, portret, miejsce na zdjęcie, kafelek dodawania, kółko koloru rodu, strzałka między osobami w „Połącz dwie osoby”) i duże ikony zaślepek.
  `CandleIcon` dostał `applyTextScaling` (domyślnie `false`) — `true` w „Otwórz cmentarz” i „Pokaż grób”. Ręczne skalowanie strzałki linku
  (`base_preview_screen.dart`) usunięte, bo liczyłoby skalę dwa razy.
- **Motyw** (`theme.dart`): `actionIconTheme` — „wstecz” i „zamknij” Fluttera rysują `GrobingIcon` (stałe 24 dp).
- **Ikona aplikacji L1:** `res/mipmap-anydpi-v26/ic_launcher.xml` (tło `@color/grobing_background`, pierwszy plan, warstwa jednobarwna),
  `mipmap-*/ic_launcher_foreground.png` (108 dp na gęstość, akcent z dwoma tonami, symbol 44% warstwy), `mipmap-*/ic_launcher_monochrome.png` (same linie,
  próg 0,8 — bez ciemnej plamy z makiety), `mipmap-*/ic_launcher.png` przebudowane (Android 7, `minSdk` 24). Ikona sklepu 512 × 512 — **poza repo**:
  `C:\Programowanie\Grobing\_ikony-dalle\sklep-ikona-512.png` (do Play Console, [[ISSUE-032-mvp-install]] → *Before install* 0).

### Emulator pass (`Grobing_Restore`, build profile, `--split-per-abi`)
Stan pokazu autora zapisany (taki sam jak `_pokaz/stan-emulatora/demo-app-data.tar`); na czas pozycji wgrany stan sprzed pokazu (wymyślona rodzina,
109 osób, v15). Zrzuty w katalogu tymczasowym sesji `1f978d57-…\scratchpad\emu046\shots\`.
- **100%:** ekran główny (lupa, koło zębate, zakładki z drzewem liściastym), podgląd cmentarza („Dodaj zdjęcie”, pióro, znicz w „Otwórz cmentarz”), plan
  cmentarza (Plan offline w zieleni, segment Plan/Zdjęcie, Kwatery, gdzie jestem, „Dodaj grób”), widok osoby (pióro, nagłówki sekcji, „Pokaż w drzewie”,
  dodanie zdjęcia w tle, „wstecz”), drzewo (przełącznik, połącz, telewizor, +/−, odtwarzanie), mapa migracji, ustawienia i „Stan danych” (kolory ról: zieleń
  kopii, bursztyn działań, szarość informacji). Wszystko w dwóch tonach, grubość 300, nic nie puste.
- **200% na 360 dp** (`wm density 480`, `font_scale 2.0`): ikony obok tekstu rosną (lupa, nagłówki sekcji, „Pokaż w drzewie”, plakietki na planie, segment
  Plan/Zdjęcie, znicz i „+” w głównych przyciskach, „Pokaż ›”); stałe zostają 24 dp (koło zębate, „wstecz”, pióro, gdzie jestem, zakładki, przełącznik drzewa
  — przy dużym tekście jak dotąd same ikony). Nic na nic nie nachodzi bardziej niż przed pozycją: plakietki na planie cmentarza mają wysokość z tekstu, ikona
  mieści się w niej (znany temat mapy cmentarza przy 200% — `CURRENT_STATE` → *Poza tą kolejnością* — bez zmian).
- **Semantyka:** opisy przycisków bez zmian („Wstecz”, „Popraw wpis”, „Ustawienia”, „Gdzie jestem, wyłączone”); ikony nie dodały węzłów.
- **AC-1:** szuflada — znicz L1 na tle aplikacji w okrągłej masce; ekran główny z włączonymi „Themed icons” (Pixel Launcher) — linie znicza w kolorze z tapety.
- **Rozmiar:** zawartość APK +0,3 MB rozpakowana (font, licencja, kod); `MaterialIcons` wycięty do 1,5 KB (zostały ikony Fluttera, których nie rysujemy).

### Deviations (dla przeglądu `ui`)
1. **Technika:** własny wycięty font zamiast pakietu `material_symbols_icons` (sonda 1). Wygląd ten sam co na makiecie; plan → *Decisions taken in the plan*
   („pakiet przypięty dokładnie”) nieaktualne.
2. **Grubość 300 jako stała `GrobingIcon.weight`**, a nie `IconThemeData.weight` w motywie — jedno miejsce w kodzie; motyw zmienia tylko `actionIconTheme`.
3. **Przełącznik „Drzewo | Mapa” stały** (jak zakładki), choć ma podpis.
4. **Ta sama ikona dla dwóch „dodaj zdjęcie”** — przycisk „Dodaj zdjęcie” (było `add_a_photo`) i zdjęcie w tle (już było `add_photo_alternate`): po decyzji 1
   oba to zdjęcie z krajobrazem.
5. **Obserwacja, nie zmiana:** znicz w ikonie aplikacji wygląda obok innych ikon na mały — 47,5 dp wysokości z 72 widocznych (jak na makiecie); przy jego
   proporcjach strefa bezpieczna 66 dp mieści ok. 59 dp. Jedna stała `SYMBOL` w `build_launcher.py`.

### Found, outside the item
- Emulator: na czas weryfikacji włączone „Themed icons” w launcherze i ikona Grobing na ekranie głównym; stan sprzed pokazu wgrany. Po stopie #2 —
  z powrotem stan pokazu (`_pokaz`) i motyw wyłączony.

### For `qa`
- **Testy z `Icons.*`** (14 odwołań w 7 plikach) przestaną znajdować ikony: `find.byIcon` nie działa z `GrobingIcon` — szukaj
  `find.byWidgetPredicate((w) => w is GrobingIcon && w.icon == Glyphs.x)`; każda ikona to dwie warstwy tekstu, nie `Icon`.
- **Nowe testy z planu:** brak `Icons.` i `Icon(` w `lib/` (skan źródeł); `GrobingIcon` — dwie warstwy (`FILL` 1 przy 25% i `FILL` 0, `wght` 300), kolor z
  `IconTheme`, rozmiar ze skalą tekstu tylko przy `applyTextScaling`, jeden opis dla czytnika; „wstecz” w `AppBar` rysuje `Glyphs.arrowBack`; strzałka linku
  32 dp przy 200% (nie 64); `meetsGuideline(androidTapTargetGuideline)` na widoku osoby i grobu przy 200%. Propozycja: **każdy `Glyphs.*` jest w `cmap` fontu**
  (test czyta `assets/fonts/grobing-symbols.ttf`) — pilnuje zgodności listy i fontu po przebudowie.
- **Kroki odczucia dla autora** (emulator): z planu → *Manual verification*.

### Round 2 — co znalazły testy `qa` (2026-10-18)
- **Strzałka menu w dacie** (`date_block.dart`, przycisk „dokładnie/około…”) przy 200% na 360 dp rosła do 48 dp i rozpychała wiersz daty o 2 px w oknie
  „Miejsce zamieszkania” (328 dp) — test „text 200% at 360 dp … without an overflow”. Teraz stała 24 dp, jak strzałka pól Material (`applyTextScaling: false`).

### Round 3 — przegląd `ui` (2 MAJOR, 2 MINOR — wszystkie poprawione)
- **MAJOR 1 — ikona w `WidgetSpan` rosła dwa razy:** Flutter sam skaluje dziecko `WidgetSpan` skalą tekstu (`widgets/widget_span.dart`,
  `_AutoScaleInlineWidget`), a `GrobingIcon` skalował drugi raz — znacznik przy „Bez adresu kwatery” stał 3,2 × przy 200%. Oba `WidgetSpan` z ikoną
  (`grave_screen.dart`, `pin_screen.dart`) → `applyTextScaling: false`; test pilnuje, że żaden `WidgetSpan` z `GrobingIcon` nie skaluje go sam.
- **MAJOR 2 — znicz w ikonie aplikacji za mały:** 23 × 47,5 dp, poniżej Androida (*„at least 48x48 dp … must not exceed 66x66 dp”*). `SYMBOL` 0,44 → **0,54**:
  58 × 28 dp, najdalszy punkt 29,6 dp od środka — w strefie 66 dp. Przebudowane warstwy, stare ikony i ikona sklepu 512 (poza repo).
- **MINOR — `public` → `language`** (przełącznik „Mapa”, „Pokaż na mapie”, wiersz kraju): pełne kontynenty były najcięższym glifem; **`storage` →
  `database`** („Stan danych”). `glyphs.txt` → font przebudowany (73 glify, 216 KB).
- Odstępstwa 1–4 przyjęte przez `ui` → [[style-b]] v1.39 (reguła 3: stałe 24 dp także przełącznik i ikony w pudełkach, skąd glify; reguła 4: „bez własnych
  krojów tekstu” — font ikon nie jest krojem).

### Round 4 — decyzja 1' autora na stopie #2: 9 ikon z arkusza (2026-10-18)
- `tool/icons/build_symbols.py` dostał trzeci argument — arkusz autora (poza repo): każdy z 9 rysunków przerysowany potrace'em (3 × rozdzielczość, Cu2Qu do
  krzywych TrueType) na **dwa statyczne glify**: linie (alfa > 0,55) i wypełnienie (wnętrze zewnętrznego obrysu — tło zalane od brzegu; dziurą zostaje tylko
  zamknięty obszar > ~30 × 30 px i średnio ciemniejszy niż 0,06, np. środek koła zębatego). Próg samego wypełnienia (pierwsza próba) dawał plamy z tekstury
  DALL-E na kole zębatym. Glify w polu 800 z 960 jednostek, jak Material, na wolnych kodach z prywatnego obszaru BMP; `HVAR` usunięty (szerokości stałe).
  Font: 73 ikony (9 z arkusza), 118 glifów, 234 KB.
- `Glyph` ma opcjonalne `fill` (kod glifu wypełnienia); `GrobingIcon` rysuje je pod liniami przy 25%. Nazwy w kodzie bez zmian (`Glyphs.map`, `group`,
  `nature`, `search`, `settings`, `addPhotoAlternate`, `addLocationAlt`, `inkPen`, `cast`), więc ekrany się nie zmieniły.
- Testy: zgodność fontu rozumie pary glifów i pilnuje, że dokładnie te 9 ma wypełnienie; nowy test — ikona z arkusza rysuje glif wypełnienia pod glifem
  linii. `flutter test --timeout 120s` — **936 zielonych**. README → *Ikony* (arkusz, potrace, jak przebudować).

### Round 5 — przegląd `ui` rundy 4 (1 MAJOR, 4 MINOR)
- **MAJOR — dwie grubości kreski:** linie arkusza miały przy 24 dp 0,6–0,75 dp, Material przy 300 — 1,5 dp. `THICKEN = 12` jednostek z 960 (≈ +0,3 dp przy
  24 dp; sonda `ui`: +0,5 dp zlewa koronę drzewa, +0,8 dp niszczy rysunki) — linie poszerzone przed potrace'em, wypełnienie bez zmian. Próba z `LINE` 0,4
  (żeby wróciły warstwice mapy) wciągnęła wypełnienie liści do linii i zlała drzewo — `LINE` zostaje 0,55.
- MINOR (słońce — druga dźwignia): glify z arkusza są statyczne, `GrobingIcon.weight` ich nie pogrubi; dźwignią jest `THICKEN` + przebudowa fontu → wiersz
  listy B niżej i reguła 3 ([[style-b]] v1.41).
- MINOR (pinezka ze zniczem na wypełnionych przyciskach „Dodaj cmentarz”, „Dodaj ten cmentarz”, „Dodaj ręcznie” — reguła 8 „Dodaj nie ma znicza”):
  **przyjęte** — to pinezka aplikacji (reguła 8: znicz w pinezce), a dodanie cmentarza stawia nową pinezkę na mapie; [[style-b]] v1.41 doprecyzowuje regułę 8.
- MINOR (poświata płomienia w wypełnieniu pinezki, ~0,3 dp przy 24 dp; warstwice mapy przerwane) — **zostaje**: przy 24 dp niewidoczne, poprawa wymaga innej
  reguły wypełnienia; wraca, gdyby autor zobaczył to w dużym rozmiarze.
- MINOR (AC-2 „z jednej rodziny” po 1') — zapis w *Verification*.

### Round 6 — znicz aplikacji (stop #2, runda 2 — autor: *„Te trzy są jeszcze, które zastanawiam się, dlaczego nie zmieniłeś”*)
- Autor wskazał logo, pinezkę na mapie i znicz w „Otwórz cmentarz” (stara sylwetka z ISSUE-014, rysowana w kodzie, poza listą 9 ikon). Na prośbę autora
  prompty do DALL-E (wzór: L1 i arkusz); autor wygenerował `Z-znicz.png` (dwa tony), `Z-znicz-pelny.png` (pełny z wyciętymi detalami), `P-pinezka.png` (poza repo).
- `build_symbols.py` przyjmuje oba znicze (argumenty 4 i 5) → `Glyphs.candle` (linie + wypełnienie, `THICKEN` jak arkusz) i `Glyphs.candleSolid` (jeden glif).
  `CandleIcon` rysuje je z fontu (logo, „Otwórz cmentarz”, „Pokaż grób”, znacznik zmarłych w drzewie); `CandlePin` zostaje kroplą z kodu (czubek co do piksela,
  poświata wybranej, licznik grupy), a w środku pełny znicz w kolorze tła — czyli wygląd `P-pinezka` (samego `P-pinezka` nie trzeba śledzić). Pinezka „jeszcze
  nie zapisana” — znicz w dwóch tonach bursztynu. Stara ścieżka znicza usunięta z kodu.
- Emulator: logo, przycisk, pinezka (obok starej) i znacznik w drzewie — zrzuty 50–53. Testy: **936 zielonych** (zgodność fontu: + 2 glify znicza).
  [[style-b]] v1.42 (reguła 8, *Known gaps*).

## Verification
> `qa`, 2026-10-18. Bez zmiany bazy (v15) — bez testu migracji i bez próbnego odtworzenia (DoD: dotyczy warstwy danych). Bez sieci — bez kroku logcat.

### Tests (`grobing-code`)
- **Przepisane:** 14 odwołań `find.byIcon(Icons.…)` w 7 plikach → `findGlyph(Glyphs.…)` (`test/support/glyphs.dart`) — `find.byIcon` nie widzi `GrobingIcon`.
- **Nowe — `test/app/icons_test.dart` (10):** `GrobingIcon` — dwie warstwy (`FILL` 1 przy 25% pod `FILL` 0, `wght` 300, `GRAD` 0, font aplikacji), kolor i
  rozmiar z `IconTheme`, rośnie z tekstem obok słów (20 → 40 dp przy 200%), stała przy `applyTextScaling: false`, jeden opis dla czytnika; „wstecz” Fluttera
  rysuje `Glyphs.arrowBack`, 24 dp przy 200% · **jedna rodzina (AC-2):** w `lib/` nie ma `Icons.` ani `Icon(`; każdy `Glyphs.*` jest w `cmap` fontu, lista
  w `glyphs.txt` zgadza się ze stałymi, font ma osie `FILL`, `GRAD`, `opsz`, `wght`; żaden `WidgetSpan` z ikoną nie skaluje jej drugi raz · **AC-1:** ikona
  adaptacyjna z tłem `grobing_background`, pierwszym planem i warstwą jednobarwną; każda gęstość ma warstwy 108 dp i starą ikonę 48 dp.
- **Nowe w plikach ekranów:** strzałka linku w podglądzie z bazy przy 200% ma 32 dp (skala raz, nie 64 — `home_screen_test.dart`); widok osoby przy 200% na
  360 dp — nagłówek sekcji 22 → 44 dp, pióro i „wstecz” 24 dp, `meetsGuideline(androidTapTargetGuideline)` i `labeledTapTargetGuideline`, każdy przycisk z akcją
  dotknięcia (`person_screen_test.dart`). Przepełnienie dolnego paska w kwadratowym foncie testowym przepuszczone jak w teście drzewa (nie na telefonie).
- **Wycofane:** test widoku grobu przy 200% — kwadratowy font testowy przepełnia wiersz o 84 px, czego nie ma w Roboto (ten sam powód co komentarz przy
  teście okna opłaty). Widok grobu przy 200% sprawdzony na emulatorze (zrzuty 20–22). Przy 100% cele dotyku grobu sprawdza istniejący test (W1).
- `dart format` · `flutter analyze` — czyste · `flutter test --timeout 120s` — **935 zielonych** (przed pozycją 923).

### What the tests found (→ `dev`, runda 2)
- Strzałka menu w dacie przepełniała okno miejsca zamieszkania przy 200% — *Round 2*.

### `ui` review (subagent bez historii, 2026-10-18)
- 0 BLOCKER · **2 MAJOR** (ikona w `WidgetSpan` skalowana dwa razy; znicz w ikonie aplikacji poniżej 48 dp) · **2 MINOR** (`public`, `storage` za ciężkie) —
  wszystkie poprawione (*Round 3*). Sprawdzone i zgodne: jedna rodzina i grubość (73 glify wyrenderowane z fontu), dwa tony bez pustych ikon, metafory,
  role kolorów bez zmian, kontrast kreski ≥ 3:1 we wszystkich parach (także wobec własnego wypełnienia: najsłabsza 3,47:1), wypełnienie nie niesie znaczenia,
  rośnięcie i stałe 24 dp zgodnie z decyzją 2, cele dotyku bez zmian, AC-1 kolorowa i tematyczna. Odstępstwa 1–4 przyjęte → [[style-b]] v1.39.

### Re-check after round 3 (emulator, build profile)
- Ikona aplikacji ze zniczem przy `SYMBOL` 0,54: w szufladzie kolorowa i na ekranie głównym w motywie Androida 13 — tej samej wagi co ikony obok (zrzuty 23–24).
- Grób przy 200% na 360 dp: znacznik przy „Bez adresu kwatery” ma wysokość tekstu (zrzut 25; przed poprawką 21).
- Testy po rundzie 3: **935 zielonych**; analiza czysta.

### Re-check after rounds 4–5 (emulator, build profile)
- 9 ikon z arkusza na ekranach (zrzuty 30–35, 40–43): zakładki, koło zębate, lupa, „Dodaj zdjęcie”, pióro, „Postaw pinezkę”, telewizor, „Pokaż w drzewie”,
  przełącznik drzewa; pinezka ze zniczem na bursztynowym „Dodaj ten cmentarz” i mapa na wybranym segmencie „Plan” — czytelne w kolorze tła na akcencie.
- Testy: **936 zielonych**; analiza czysta.

### Stop #2 — runda 1 (autor, 2026-10-18)
- Krok 1 (ikona aplikacji): *„ikona samej aplikacji jest ok”*.
- Krok 2 (ikony w aplikacji): **błąd zrozumienia decyzji 1** — *„dalej widzę, że to są te stare ikonki zamiast nowych … ikona cmentarzy, Mapy, Osoby, Drzewa są
  tymi »uproszczonymi«, a ja chciałem te »odpicowane«”* (załączony arkusz `C-arkusz-bursztyn.png`). Opis opcji B na pytaniu („Twój kierunek narysowany
  kreską”) autor odczytał jako swoje ikony z arkusza; w aplikacji B to ikony Google w bursztynie i dwóch tonach. Decyzja 1 do potwierdzenia na makiecie
  (kolumna C) — retro 4, R1.
- **Decyzja 1' (autor, 2026-10-18: *„tak”*) — 9 ikon z arkusza autora w aplikacji:** zakładki Mapa, Osoby, Drzewo, lupa, ustawienia, dodaj zdjęcie,
  pinezka ze zniczem, pióro, telewizor — przerysowane do wektora (ostre, kolor ze stanu); drobne ikony spoza arkusza (strzałki, ✕, ✓, „›”, kalendarz …)
  zostają z B. Autor zna koszt: przy 24 dp najdrobniejsze detale się zlewają (makieta → punkt 2). Pokaz na emulatorze przed zamknięciem.
- **Do retro:** nazwa opcji opisana kierunkiem („Twój kierunek …”) zamiast tym, skąd jest rysunek („ikony Google w Twoich kolorach” vs „Twoje obrazki
  z arkusza”) — autor wybrał nie to, co chciał; wyszło dopiero na emulatorze po całej budowie.

### Stop #2 — runda 2 i 3 (autor, 2026-10-18)
- Runda 2 (9 ikon z arkusza): autor wskazał trzy miejsca ze starym zniczem (logo, pinezka, „Otwórz cmentarz”) → *Round 6*.
- **Runda 3 — krok 2: *„Ok”*** (ikony z arkusza, znicz autora w logo, przyciskach, pinezce i drzewie; emulator, build profile). Krok 1 (ikona aplikacji) —
  *„ok”* z rundy 1.
- Przegląd zmiany znicza (*Round 6*) — `qa` ze zrzutów 50–53, bez osobnego subagenta `ui` (mała zmiana na prośbę autora, oglądana przez autora na stopie).

### Hand checks → [[ISSUE-032-mvp-install]]
- **B** — kreska ikon w kolorze tekstu pomocniczego w pełnym słońcu na telefonie (NFR-004; przy słabej widoczności: ikony Material — `GrobingIcon.weight`
  300 → 400; 9 ikon z arkusza, w tym trzy zakładki — `THICKEN` w `tool/icons/build_symbols.py` i przebudowa fontu) — nieprzetestowane na żywo, wymaga telefonu.
- **AC-2 po decyzji 1'** — „z jednej rodziny” czytamy jako jeden font, te same role kolorów, rozmiary i dwa tony; rysunki mają dwa źródła (9 z arkusza autora,
  reszta Material) i bliską, ale nie identyczną grubość — skutek decyzji autora, nie usterka (przegląd `ui`, runda 4).
- **B** — ikona aplikacji na telefonie autora (Motorola, launcher producenta: maska i motyw mogą różnić się od Pixel Launchera na emulatorze) —
  nieprzetestowane na żywo, wymaga telefonu.
