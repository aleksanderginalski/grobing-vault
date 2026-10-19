---
title: "ISSUE-049 — Tree: kinship levels (blood, then each marriage) independent of zooming, zoom also on the TV"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-19
verdict-reviewer: self-check
source: "`/pm` 2026-10-18 — autor przeszedł cały przepływ na emulatorze (dane demo), punkty 5–6 z 7, z doprecyzowaniem w tej samej sesji; podział — `pm`"
created: 2026-10-18
updated: 2026-10-19
---

# ISSUE-049 — Poziomy pokrewieństwa niezależne od przybliżania

> Autor: *„dlaczego zoom-in/out nie działa w wersji drzewa genealogicznego, gdy jest na telewizorze”* · *„chciałbym, aby poziomy rodziny nie
> zmieniały się, gdy robię zoom-in zoom-out (chciałbym widzieć „big picture” i przybliżać sobie szczegóły bez znikania członków mojej rodziny)”*.
> Doprecyzowanie: *„chciałbym, aby to były niezależne względem siebie funkcjonalności: a) poziomy do pokazywania linii pokrewieństwa /
> powinowactwa (np. poziom pierwszy to tylko „nasza linia krwi”, a w kolejnych poziomach dodawana jest np. rodzina żony brata itd., na jeszcze
> kolejnym rodzina męża siostry żony brata itd.); b) zoom-in zoom-out do poruszania się po widoku naszego drzewa”*.

## What to build
- **a) Nowa reguła poziomów** — zastępuje [[drzewo]] D2 (reguła autora ze SPIKE-002: poziom 1 — rodzice, partnerzy, dzieci; kolejne dokładają rodzinę
  każdej osoby). Reguła zrozumiana przez `pm` (autor nie zaprzeczył): **poziom = 1 + liczba małżeństw na drodze od osoby w środku**:
  - poziom 1 — sama krew: przodkowie, potomkowie, rodzeństwo, kuzyni;
  - poziom 2 — przez jedno małżeństwo: np. rodzina żony, rodzina żony brata;
  - poziom 3 — przez kolejne: np. rodzina męża siostry żony brata.
  Rama: to nadal DOI z [[drzewo]] D8 (TimeNets), z innymi wagami — krok po krwi nic nie kosztuje, krok przez małżeństwo kosztuje poziom.
- **Osobny przełącznik poziomu** — poziom nie zmienia się gestem. Stary „− Poziom 2 +” autor nazwał nieestetycznym ([[drzewo]] D25, S1) → nowy
  kształt na makiecie.
- **b) Przybliżanie i oddalanie to sam widok** — dwa palce, + / −, podwójne dotknięcie; skład osób się nie zmienia. Zastępuje [[drzewo]] el. 3 / S2
  (oddalanie dokłada poziom, przybliżanie zabiera).
- **Tryb prezentacji** ([[drzewo]] el. 11, D16 „poziom 2 stały”, „bez szczypania”) — przybliżanie i oddalanie także na telewizorze; *Obali* D16
  („autor chce oddalać na telewizorze”) — trafione.
- Dotyka: ścieżka „Połącz dwie osoby” ([[drzewo]] el. 8 — „najniższy poziom, na którym widać całą ścieżkę”), ślad dalszej rodziny (D9), imiona przy
  oddalaniu (I2, D27), „Pokaż w drzewie” (D15 — poziom 2), stany i czytnik.
- Projekt: `ui` przed `planning`; **kandydaci na emulatorze albo makiecie przed rekomendacją** (retro 2, R6 — pozycja wybiera to, co widać).

## Acceptance Criteria
- **AC-1** *Given* drzewo na dowolnym poziomie *When* przybliżam i oddalam (dwa palce, podwójne dotknięcie) *Then* na drzewie są te same
  osoby — zmienia się tylko widok (zmienione na stopie #2 — [[drzewo]] D58: + / − zmieniają poziom, przybliżania nie ma na przyciskach; do 2026-10-19:
  „dwa palce, + / −, podwójne dotknięcie”).
- **AC-2** *Given* „Ja” w środku, brat Piotr Wymyślony z żoną Ewą z d. Zmyśloną *When* poziom 1 *Then* widać krewnych z krwi (rodziców, dziadków,
  Piotra i jego dzieci), a rodziców Ewy nie; *When* poziom 2 *Then* widać też rodziców Ewy.
- **AC-3** *Given* poziom 2 *When* poziom 3 *Then* dochodzi rodzina, do której prowadzi kolejny związek (np. rodzice męża siostry Ewy — sam mąż jest już na poziomie 2;
  zmienione na stopie #1, M2 — [[drzewo]] D50; do 2026-10-19: „mąż siostry Ewy i jego rodzice”).
- **AC-4** *Given* tryb prezentacji na telewizorze *When* szczypię na telefonie *Then* obraz przybliża się i oddala, a skład osób się nie zmienia.
- **AC-5** *Given* „Połącz dwie osoby” *Then* cała ścieżka jest dalej widoczna na drzewie (regresja [[US-011-polacz-dwie-osoby]]).

## Notes
- `⚠️ OPEN` (na makietę, stop #1):
  1. **małżonkowie krewnych na poziomie 1** — np. żona brata jako matka jego dzieci (dzieci są z krwi, ona nie): widać ją na poziomie 1 czy
     dopiero na 2?
  2. **przełącznik poziomu w trybie prezentacji** — jest, czy poziom zmienia się tylko przed wejściem w tryb?
  3. **skala po zmianie poziomu** — zostaje, czy drzewo dopasowuje się do ekranu?
  4. **nazwy poziomów** — słowa z pytania autora („linia krwi”, „pokrewieństwo / powinowactwo”) czy liczby.
- Bez zmiany bazy (poziom liczony z relacji przy otwarciu, jak dziś).
- Wejście dla [[ISSUE-050-next-event]] (zdarzenia osób na bieżącym poziomie).
- [[EPIC-003-zrozumienie]] ([[US-009-drzewo-od-osoby]], [[US-011-polacz-dwie-osoby]]). Z tego samego przeglądu autora:
  [[ISSUE-047-grave-first-then-people]] · [[ISSUE-048-portrait-photos]].

## Implementation plan
> `planning`, 2026-10-19. **Pozycja z ekranem: zmiana istniejącego (drzewo i tryb prezentacji).** Specyfikacja — propozycja `ui` na stop #1: [[drzewo]] **v1.23**
> (element 3 — poziom i jego przełącznik, nowy 3a — przybliżanie, zmiany w 4, 8, 11; D50–D57; **⚠️ OPEN 11: M, P, N, K, T**), [[style-b]] **v1.44** (wyjątek celu dotyku — D52;
> bez nowych tokenów). **Makieta (klikalna, 117 wymyślonych osób, przełączniki wariantów w sekcjach 1–5, na starcie rekomendacje):**
> `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/92dbd968-927f-472a-91ff-e3e4542b1b66/scratchpad/drzewo-049.html`.
> Bez US (task-level, pod [[US-009-drzewo-od-osoby]] i [[US-011-polacz-dwie-osoby]]); widok 5 (M9, M11). **Bez zmiany bazy** (poziom liczony z relacji przy otwarciu).

> **Stop #1 — 2026-10-19, autor: *„tak”*** na pytanie „Budujemy według rekomendacji: M2, P2, N2, K1, T2?”. Przyjęte: **M2, P2, N2, K1, T2** ([[drzewo]] *Open* 11
> zamknięte), decyzje projektowe D51, D52, D57 i brzmienie AC-3 przy M2 (AC-3 poprawione). Specyfikacja [[drzewo]] v1.23 i [[style-b]] v1.44 przestają być propozycją.

### Scope — diff
**Dane — bez zmiany schematu (v15), bez zmiany kopii.**
1. `lib/app/tree/tree_layout.dart` — **`TreeGraph.unionLevels(focus)`** (D50, M2): krewni = w górę, potem w dół (`parentsOf`, `childrenOf`); poziom 1 — krewni osoby w
   środku z ich partnerami (`partnersOf`, oba tryby związku, także zakończone); poziom k + 1 — krewni każdego partnera spoza krwi z poziomu k, z ich partnerami. Każdy raz, na
   najniższym poziomie, więc cykl w danych nie zawiesza (jak `levelsFrom`). `layoutTree(graph, focus, level)` bierze osoby z `unionLevels ≤ level`. **`levelsFrom` zostaje**
   jako odległość w krokach — kolejność w układzie i pierwszeństwo imion (I2, D57); nazwa do decyzji `dev` (np. `stepsFrom`), opis w komentarzu.
2. `lib/app/tree/tree_path.dart` — `pathLevel`: najwyższy `unionLevels` osób ścieżki (każda połączona osoba ma poziom, `also` zawsze puste); **usunąć `levelScales` i
   `pathMinScale`** — kadr ścieżki: największa skala, w której się mieści, najwyżej 1,3, najmniej dolna granica z pkt 3.

**Ekran — `lib/app/tree/tree_screen.dart`** ([[drzewo]] v1.23):
3. **Skala odpięta od poziomu** (3a, D51): usunąć `treeLevelAtScale` i zmianę poziomu w `_onView`; **dolna granica liczona** — cały pokazany poziom w obszarze drzewa (24 dp
   marginesu), `clamp(0.08, 0.4)`; liczona przy każdym `_relayout` i nowym rozmiarze obszaru, podana do `InteractiveViewer.minScale` i `_zoom`; gdy wypada nad bieżącą skalą —
   skala rośnie do niej. Górna 2,0 i krok 1,45 bez zmian.
4. **Dotknięcie przy małym drzewie** (D52): gdy `slot × skala < 24` — dotknięcie osoby albo pustego miejsca przybliża w to miejsce do 0,45 (animacja ok. 0,35 s, przy
   ograniczeniu animacji od razu), nie stawia w środku; semantyka węzła: działanie „przybliż” zamiast „w środek”. W trybie prezentacji pusty dotyk dalej pokazuje sterowanie.
5. **Poziom** (3, D53–D55, D57): **wybrany poziom zostaje, dopóki aplikacja działa** (jak `treeTempo` — zmienna na poziomie modułu), pierwszy raz 1; `curLevel = min(wybrany,
   najwyższy poziom osoby w środku)`. **Etykieta** `Positioned(left: 12, bottom: 12)` w obszarze drzewa (powierzchnia z obrysem, 48 dp, nazwa 14 sp w500 + `Glyphs.arrowDropDown`
   w akcencie, ucięcie „…” przed + / −; semantyka „Kogo pokazać: … — zmień”). **Lista** — dolny arkusz jak arkusz rodów (`clan_screen.dart`): tytuł „Kogo pokazać na drzewie”,
   wiersz poziomu (nazwa, opis z liczbą osób, `Glyphs.check` w akcencie przy wybranym, stan „zaznaczone”). **Nazwy** N2: „Linia krwi”, „Przez N związek/związki/związków”
   (odmiana z `polish.dart`). **Zmiana:** `_relayout(keep: focus, animate: true)` bez ruchu kamery (K1); pigułka „{nazwa} · {N osób} (+M)” ok. 1,8 s, liczba osób w roku suwaka
   (D37); kończy podświetlenie ścieżki.
6. **„Połącz dwie osoby”** (8, D57): poziom tylko w górę (`max(wybrany, pathLevel)`); kadr z pkt 2; **po końcu skala i poziom zostają** — usunąć powrót do 0,4 i poziom ze skali
   (`_clearPath` i okolice, dziś linie ok. 424, 432, 1113–1123). `_underZoomButtons` sprawdza też prostokąt etykiety poziomu w lewym dolnym rogu (osoba ze ścieżki nie może
   stać pod żadnym z nich).
7. **Tryb prezentacji** (11, D56): `_present` bez poziomu 2 i dopasowania — poziom i skala zostają, osoba w środku na środku ekranu; `scaleEnabled: true` (dwa palce);
   dotknięcie osoby w środku — przesunięcie do niej bez zmiany skali; `_leave` bez `_scale = 1`; `_fitted()` usunąć, jeśli nic go nie woła. **Listwa** (`PresentationBar`): za
   `TreeTimeBar` (jeden rząd) etykieta poziomu (ta sama lista) i − / + (44 dp w celu 48 dp); każde ich dotknięcie przedłuża sterowanie (`_armControls`).
8. **Start i „Pokaż w drzewie”:** skala 1, wybrany poziom (nie 2). Teksty i komentarze o S2, poziomie 2 i „Poziom N · …” — przepisać.

**Dane testowe:**
9. `lib/dev/fictional_family.dart` (debug i profile) — **+10 osób jak w makiecie** (rdzenie wymyślone): rodzice Natalii (Zbigniew i Alicja Zmyślewicz), jej siostra Patrycja z
   mężem Konradem Przykładniakiem i córką, rodzice i brat Konrada, rodzice Bartosza Testowicza. Komentarz i liczby w nagłówku pliku; `fictional_family_test.dart` liczy nowe.

**Brzmienie AC-3 przy M2** (zmiana na stopie #1): *Given* poziom 2 *When* poziom 3 *Then* dochodzi rodzina, do której prowadzi kolejny związek (np. **rodzice męża siostry
Ewy** — sam mąż jest już na poziomie 2). W danych testowych: Ewa → Natalia, mąż siostry → Konrad.

### AC → test happy-path (`qa`)
| AC | Test |
|---|---|
| AC-1 | ekran: „Ja”, „Linia krwi” — −, podwójne dotknięcie, + i gest dwóch palców (`TestGesture`): liczba węzłów osób stała, skala się zmienia; oddalenie do dolnej granicy = cały poziom w obszarze |
| AC-2 | jednostka (`unionLevels` na wymyślonej rodzinie): Michał, Leon, Natalia na 1, rodzice Natalii na 2; ekran: etykieta → lista → „Przez 1 związek” → węzeł rodziców Natalii jest, pigułka z „(+N)” |
| AC-3 | jednostka: Konrad na 2, jego rodzice na 3; ekran: „Przez 2 związki” — rodzice Konrada na drzewie |
| AC-4 | ekran w trybie prezentacji: dwa palce zmieniają skalę, liczba osób stała; − / + i etykieta na listwie; wejście i wyjście zachowują poziom i skalę |
| AC-5 | ekran: „Połącz dwie osoby” Ja → rodzic Konrada — wszystkie osoby ścieżki w kadrze, poziom podniesiony do 3; po końcu podświetlenia poziom i skala bez zmian; z poziomu 3 do ścieżki na 1 — poziom zostaje 3 |

Dodatkowo (decyzje projektowe): **D52** — przy skali, w której `slot × skala < 24`, dotknięcie osoby przybliża do 0,45, a środek się nie zmienia; **D57** — poziom po
przejściu na inną zakładkę i z powrotem zostaje, osoba bez rodziny („Teofil”) pokazuje jeden poziom, a po powrocie do „Ja” wraca wybrany; jednostka — cykl w danych
(osoba w parze ze swoim dzieckiem) nie zawiesza `unionLevels`. Testy S2 (US-009 AC-3: „− → Poziom 3”) i dopasowania poziomu 2 w prezentacji przechodzą na nowe zachowanie.
**Bez testu migracji i odtworzenia** — schemat i kopia się nie zmieniają. Rytuał WZ-024: `dart format` → `flutter analyze` → `flutter test --timeout 120s`.

### Manual checks (stop #2)
**Agent na emulatorze — przed stopem, ze zrzutami.** `Grobing_Restore` ma dziś **demo**: najpierw zapisać obecny stan i wgrać stan sprzed demo z
`C:\Programowanie\Grobing\_pokaz` (README tam), **nigdy `pm clear` bez zapisanego tar**; 10 osób z pkt 9 dopisać po swojemu (przycisk wymyślonej rodziny na pustej bazie albo
formularz); po pozycji — demo z powrotem (jak w ISSUE-047, ISSUE-048).
1. „Ja”, „Linia krwi”: − do całego drzewa i + z powrotem — liczba osób w zrzucie drzewa (`uiautomator dump`) ta sama; przy całości dotknięcie przybliża, dopiero potem osoba staje w środku.
2. Etykieta → lista → „Przez 1 związek” → „Przez 2 związki” → „Linia krwi”: rodzina Natalii i rodzice Konrada pojawiają się i znikają, pigułki z liczbą; osoba w środku nie skacze.
3. Tryb prezentacji: − / + i etykieta na listwie, zmiana poziomu; wyjście — ten sam poziom i skala. Gest dwóch palców — test ekranu (emulator przez `adb` nie szczypie) i lista B.
4. „Połącz dwie osoby” Ja → rodzic Konrada: cała ścieżka w kadrze, potem koniec podświetlenia — poziom i skala zostają.
5. Tekst 200% na 360 dp: etykieta, lista, listwa prezentacji (poziomo); TalkBack — opisy etykiety, wierszy listy i węzła przy małym drzewie (`uiautomator dump`).
6. **Klatki** (retro 4, R3): build profile z `FRAME_LOG`, naprzemiennie z buildem odniesienia — oddalanie do całego drzewa (116 osób na ekranie) i zmiana poziomu 1 → 2; po każdym
   `flutter build` — `android\gradlew --stop`.
7. Zamknięcie aplikacji i start — „Linia krwi” znowu; przejście na inną zakładkę i z powrotem — poziom zostaje.

**Autor: odczucie — najwyżej 3 kroki** (emulator):
1. Oddal do całego drzewa i przybliż z powrotem do siebie — czy to jest „big picture”, o które Ci chodziło? (*Obali* [[drzewo]] D51)
2. Etykietą „Linia krwi ▾” dołóż rodziny przez związki i wróć — czy przełącznik jest estetyczny i jasny? (*Obali* D53, D54)
3. W trybie prezentacji przybliż i zmień poziom na listwie — czy tak opowiesz rodzinie od linii krwi do rodzin przez związki? (*Obali* D56)

Na telefonie i telewizorze (lista **B** w [[ISSUE-032-mvp-install]] → *Hand checks*): szczypanie na telefonie w trybie prezentacji z obrazem na telewizorze; cały obraz z kanapy.

### Out of Scope
- mini-drzewo w [[osoba]] (bez poziomów) i mapa migracji ([[mapa-migracji]] — kto jest na mapie, bez zmian);
- „Następne” ([[ISSUE-050-next-event]]) — korzysta z poziomów tej pozycji, budowane osobno;
- „Połącz dwie osoby” w trybie prezentacji (D49) i opowieść rodziny ([[2026-10-14-opowiesc-rodziny-i-wieniec]]);
- drzewo poziomo na telefonie poza trybem prezentacji (cały obraz czytelny tylko na telewizorze — D51 *Nie da*);
- nowe ikony w foncie aplikacji (P2 ich nie potrzebuje; P3 by potrzebował);
- znane drobne usterki drzewa z *CURRENT_STATE* (ślad pod tabliczką imienia, imiona przy ścieżce przy 200%) — osobne kandydatki.

### Decision for stop #1 (author) — jedno pytanie
**Budujemy według rekomendacji: M2, P2, N2, K1, T2?** „tak” = makieta tak, jak otwiera się na starcie + decyzje projektowe niżej + brzmienie AC-3 przy M2. Inna odpowiedź: litery
wariantów, np. „M1, P1” (reszta zostaje), albo Twoje nazwy poziomów zamiast N2.
- **M2** — mąż, żona i partner krewnego już na „Linii krwi”, ich rodziny poziom wyżej (M1: na 1 sama krew — 67 zamiast 91 osób od Ciebie, dzieci brata bez mamy);
- **P2** — etykieta „Linia krwi ▾” w lewym dolnym rogu, dotknięcie otwiera listę z opisem i liczbą osób (P1: numery „1 · 2 · 3” u góry; P3: okrągły przycisk nad + / −);
- **N2** — „Linia krwi”, „Przez 1 związek”, „Przez 2 związki” (N1: „Poziom 1, 2, 3”);
- **K1** — po zmianie poziomu skala i osoba w środku zostają (K2: drzewo dopasowuje się do ekranu);
- **T2** — przełącznik poziomu także na listwie w trybie prezentacji (T1: tylko przed wejściem).

Decyzje projektowe, które przechodzą na „tak” (widać je na makiecie): oddalanie do całego drzewa; przy bardzo małym drzewie dotknięcie najpierw przybliża (cel ≥ 24 dp);
wybrany poziom zostaje, dopóki aplikacja działa, a pierwszy raz to „Linia krwi”; ścieżka „Połącz” podnosi poziom, ale go nie obniża, a po niej skala zostaje; imiona przy
oddalaniu według kroków w rodzinie; na telewizorze dwa palce i − / +.

**Czego to nie da:** czytelnego całego drzewa na telefonie pionowo — przy 91 osobach okręgi mają ok. 5 dp i widać ok. 10 imion; czytelny cały obraz jest na telewizorze (okręgi
15 dp, ok. połowa imion). Termin: pozycja to ok. 1–1,5 dnia pracy; kolejka (ISSUE-050, retro przy liczniku 10, ISSUE-032) mieści się do 2026-10-29.

## Dev report
> `dev`, 2026-10-19. Plan pkt 1–9 zrobione; `flutter analyze lib` czyste, `dart format` bez zmian. Flutter 3.41.1 (przypięty). **Bez zmiany schematu** (v15).
> Testy należą do `qa` — w `test/` są dziś 2 błędy analizy od usuniętych nazw (niżej, *Dla `qa`*).

### Done
- `lib/app/tree/tree_layout.dart` — `TreeGraph.bloodOf`, **`unionLevels`** (D50, M2), `unionLevelCount`, `unionLevelSize`; `layoutTree` pokazuje osoby z
  `unionLevels ≤ level`; `levelsFrom` zostaje jako odległość w krokach (kolejność w układzie, pierwszeństwo imion — D57), opisane w komentarzu.
- `lib/app/tree/tree_path.dart` — `pathLevel` = najwyższy poziom osób ścieżki (`also` puste); usunięte `levelScales` i `pathMinScale`, nowe `pathMaxScale` (1,3).
- `lib/app/tree/tree_screen.dart`:
  - skala odpięta od poziomu (3a): usunięte `treeLevelAtScale` i zmiana poziomu w `_onView`; dolna granica `_minScale` liczona z układu i obszaru
    (`treeMinScaleAtLeast` 0,08 … `treeMinScaleAtMost` 0,4), podawana do `InteractiveViewer` i `_zoomTo`; podniesienie skali po zmianie poziomu albo obszaru — po klatce;
  - D52: `slot × skala < 24` → dotknięcie osoby albo pustego miejsca przybliża do 0,45 (`_zoomIn`), podpowiedź czytnika „przybliż”;
  - poziom: `treeLevel` (zmienna modułu, jak `treeTempo`, start 1), `_level` = min(wybrany, poziomy osoby w środku); **`_LevelChip`** (lewy dolny róg,
    `Glyphs.arrowDropDown`, semantyka „Kogo pokazać: … — zmień”), **`showLevelSheet`** (wiersze z `check`, `selected`), `treeLevelName` / `treeLevelWho`
    (N2, twarde spacje jako escape), pigułka „{nazwa} · {N osób} (+M)” 1,8 s; K1 — `_relayout(keep, animate)` bez ruchu kamery;
  - „Połącz dwie osoby”: poziom tylko w górę, kadr `max(_minScale, min(fit, 1,3))`, po końcu skala i poziom zostają; `_underControls` liczy też etykietę;
  - tryb prezentacji: bez poziomu 2 i dopasowania (`_fitted` usunięte), `scaleEnabled: true`, środek na 50% wysokości, wyjście bez `_scale = 1`; na listwie
    etykieta poziomu i − / + (44 dp w 48 dp, tło z obrysem).
- `lib/dev/fictional_family.dart` — **+10 osób** i 4 związki jak w makiecie; `addFictionalFamily` dopisuje je do rodziny wgranej wcześniej (narzędzie, debug i profile).

### Deviations
1. **Oddalenie do końca stawia cały poziom na środku obszaru** (`_wholeView`) — przy − od razu, po geście dwóch palców po 0,4 s spokoju (jak D21). Specyfikacja (3a)
   mówi „od skali, w której cały poziom mieści się”, ale nie mówi, gdzie stoi: na emulatorze − od „Ja” zostawiało drzewo przesunięte w bok, z uciętą osobą (89 z 91
   na ekranie). Teraz 91 z 91. Ze ścieżką „Połącz” — bez centrowania (jej kadr). *Do przyjęcia przez `ui`.*
2. **Osoby z widocznym imieniem rysowane na wierzchu swojej grupy** (`steadyNamed`, klucz na `Positioned`): przy całym drzewie imię 13 sp jest szersze niż kilka
   okręgów, a okręgi rysowane po nim cięły litery („Wiktoria”, „Stanisław”). Tabliczka imienia zakrywa teraz okręgi pod sobą.
3. **W trybie prezentacji bez pigułki po zmianie poziomu** — u góry stoi sterowanie (rok, „Drzewo · Mapa”, „Zakończ”), a nazwę poziomu mówi etykieta na listwie.
4. Narzędzie: przycisk „Wymyślona rodzina do drzewa” w *Stanie danych* dopisuje 10 osób do rodziny, która już jest (wcześniej — nic).
5. **Poprawka liczby** w [[drzewo]] v1.23, planie i makiecie: dopisanych osób jest **10**, nie 11 (117 = 107 z makiet + 10) — błąd `ui` i `planning` w tej sesji.

### Found on the emulator
`Grobing_Restore`, build profile z `FRAME_LOG`, stan sprzed demo z `_pokaz` + 10 osób; zrzuty w `emu049\shots\` (katalog sesji).
- **AC-1:** „Ja”, „Linia krwi” — 8 × − → cały poziom (skala ok. 0,12), na ekranie 91 osób; + z powrotem; przy całym poziomie 3 — 116 osób.
- **AC-2:** start — Michał, Natalia, Leon na „Linii krwi”, nad Natalią i Kasią ślad (D9); „Przez 1 związek” → rodzice Natalii, Patrycja, Konrad, rodzice Bartosza;
  pigułka „Przez 1 związek · 113 osób (+22)”, „Ja” w tym samym miejscu ekranu (K1).
- **AC-3:** „Przez 2 związki” → rodzice i brat Konrada, pigułka „Przez 2 związki · 116 osób (+3)”. Z całego poziomu 3 na „Linię krwi” — skala rośnie do nowej granicy,
  cały poziom na środku.
- **D52:** przy całości cele ok. 11 dp, podpowiedź „przybliż”; dotknięcie → skala 0,45, środek bez zmian, cele 43 dp, „w środek”.
- **Lista:** 91 → 113 → 116 osób, wybrany z `check` i `selected`; przy tekście 200% na 360 dp lista się przewija, a etykieta (ok. 233 × 48 dp) stoi obok − bez nakładania.
- **AC-5:** Ja → Ryszard Przykładniak: cała ścieżka w kadrze (6 osób), poziom sam do „Przez 2 związki” (od Ryszarda w środku, W2), baner „Teść siostry partnerki
  mojego brata”; po końcu — te same granice węzłów i poziom.
- **AC-4:** tryb prezentacji przejął poziom; skala z telefonu była niższa niż granica na ekranie poziomym → podniesiona, cały poziom na środku (od Ryszarda na
  poziomie 3 to 99 osób — rodzina Kasi jest od niego na poziomie 4, zgodnie z regułą); − / + na listwie: 66 → 98 osób na ekranie, poziom bez zmian; lista na listwie
  (560 dp, 4 poziomy od Ryszarda: 6 → 11 → 99 → 116) → „Przez 3 związki”; wyjście — ten sam poziom i skala. Szczypania przez `adb` się nie da → test `qa` + lista B.
- **D57:** zakładka Osoby i z powrotem — „Ja”, skala 1, wybrany poziom (przycięty do 3 przy „Ja”); po ponownym uruchomieniu — „Linia krwi”; Teofil (bez rodziny) przez
  „Pokaż na mapie” → „Drzewo”: jeden poziom, „Linia krwi · 1 osoba”.
- **Klatki** (retro 4, R3 — naprzemiennie z buildem odniesienia z HEAD e8c404e, ta sama baza; 8 × −, 3 przeciągnięcia, 8 × +): nowy 23,7% i 26,9% klatek > 16,7 ms,
  raster p50 14,7–14,8 ms; odniesienie 17,4% i 24,3%, p50 13,9 ms. Nowy średnio ok. 4 pp gorzej przy rozrzucie odniesienia 7 pp — przy całym drzewie na ekranie
  jest naraz 91 osób z wieńcami, a stare drzewo kończyło na 0,4 z częścią poza ekranem. Płynność w ręce — lista B ([[ISSUE-032-mvp-install]]).

### Observations (dla przeglądu `ui`)
- Na „Przez 1 związek” od „Ja” rodzice Natalii stoją po drugiej stronie drzewa, a do niej biegnie długa linia nad Kasią — cecha kraty (D8), układ bez zmian.
- Opisy na liście mówią przykładami od „Ja” („np. rodzina żony brata”), także gdy w środku stoi ktoś inny.
- Na zrzutach z emulatora są wpisy autora z wcześniejszych stopów (osoba na liście „Do kogo?”) — zrzuty zostają poza repo, do kosza po pozycji.

### Dla `qa`
- **Usunięte:** `treeLevelAtScale`, `treeMinScale`, `levelScales`, `pathMinScale` — błędy analizy: `test/app/tree/tree_connect_test.dart:461`,
  `test/app/tree/tree_presentation_test.dart:501`. **Nowe:** `treeLevel` (zmienna modułu — ustawiać w `setUp` jak `treeTempo`), `treeLevelName`, `treeLevelWho`,
  `showLevelSheet`, `TreeGraph.bloodOf` / `unionLevels` / `unionLevelCount` / `unionLevelSize`, `pathMaxScale`, `treeMinScaleAtMost` / `treeMinScaleAtLeast`,
  `treeTargetMin`, `treeTapZoomScale`.
- Wymyślona rodzina: 117 osób, 42 związki, 32 zmarłych, 44 bez rodziców; od „Ja” 91 → 113 → 116.
- **Emulator:** `Grobing_Restore` ma stan sprzed demo + 10 osób + nowy build profile (`FRAME_LOG`); tekst i gęstość domyślne. **Demo zapisane** w katalogu sesji
  `emu049\` (`stan-przed-049.tar` + `stan-przed-049-base.apk`) — wgrać z powrotem po pozycji. APK odniesienia: `emu049\ref-head-profile.apk`; kopia repo do jego
  budowy: `%TEMP%\gref049` (bez `key.properties`) — do kosza.

### Runda 2 — po stopie #2 (decyzja autora, [[drzewo]] v1.25, D58)
> `dev`, 2026-10-19. `flutter analyze` czyste, `dart format` bez zmian. Bez zmiany schematu.
- `lib/app/tree/tree_screen.dart`: **usunięte** `_LevelChip`, `showLevelSheet`, `_LevelRow`, `_chooseLevel`, `treeLevelWho`, `_levelChipWidth`, `_levelChipBand`,
  `_zoomButton`, `_zoomButtons`; `_ZoomButton` → **`_RoundButton`** (`onPressed` może być `null` — ikona w kolorze tekstu pomocniczego, semantyka `button`, `enabled`,
  etykieta = `tooltip`). **Nowe:** `_levels` (liczba poziomów osoby w środku), `_levelButtons` (+ nad −, prawy dolny róg), `_further` / `_nearer` („Dalsza rodzina” /
  „Bliższa rodzina”, na krańcach `null`); `_setLevel` odrzuca poziom spoza 1…`_levels` i pokazuje pigułkę także w trybie prezentacji — 68 dp od góry, gdy widać
  sterowanie (górny rząd ma 48 dp przy każdym rozmiarze tekstu), inaczej 10 dp; listwa prezentacji: − / + poziomu od 560 dp; `_underControls` liczy już tylko
  kolumnę + / −, a kadr ścieżki pod nią — `v.width − 72`. `treeZoomStep` zostaje dla podwójnego dotknięcia.
- **Bez odstępstw** od [[drzewo]] v1.25. Klatek nie mierzyłem ponownie: drzewo, warstwy i gesty bez zmian, zmieniły się tylko przyciski i miejsce pigułki.
- **Emulator** (`Grobing_Restore`, nowy build profile; zrzuty `emu049\shots\` 24–30): start — „Dalsza rodzina” klikalne, „Bliższa rodzina” nie (`uiautomator`: 127 × 126 px,
  48 dp); + → „Przez 1 związek · 113 osób (+22)”, + → „Przez 2 związki · 116 osób (+3)” i + nieaktywne; tryb prezentacji: na listwie − / + (126 × 126 px), − →
  pigułka „(−3)” pod „Drzewo · Mapa” i „Zakończ prezentację”; tekst 200% poziomo — pigułka od ok. 267 dp, tabliczka roku do ok. 142 dp, pigułka 69 dp od góry, rząd
  sterowania do 59 dp; tekst 200% pionowo na 411 dp — pigułka w dwóch liniach, + / − bez zmian.
- **Po przeglądzie `ui` rundy 2** (4 MINOR na ekranie, poprawione przed stopem): cel 48 dp na listwie przyjmuje dotyk także w 2 dp wokół koła 44 dp (`GestureDetector`
  nieprzezroczysty na całym celu — koło z klipem łapało tylko siebie); nieaktywny + / − **bez obrysu** (sam kolor ikony dawał 2,00:1 między stanami); pigułka
  `textWidthBasis: longestLine` — w dwóch liniach szeroka jak dłuższa, nie jak cały rząd; w trybie prezentacji pigułka wcięta z obu stron o szerokość roku w rogu i 12 dp
  (jak przełącznik „Drzewo · Mapa”). Emulator po poprawkach (zrzuty 31–33): ekran **360 × 640 dp** przy 200% — pigułka ok. 214 dp w dwóch liniach; ten sam ekran poziomo
  (640 dp), tryb prezentacji — pigułka od ok. 220 dp, tabliczka roku do ok. 140 dp, nieaktywne − bez obrysu; cel na listwie 144 × 144 px = 48 dp.

## Verification
> `qa`, 2026-10-19. Rytuał WZ-024: `dart format lib test` — 0 zmian · `flutter analyze` — czysto · `flutter test --timeout 120s` — **964 zielone**
> (przed pozycją 956). Bez zmiany schematu (v15) — bez testu migracji i próbnego odtworzenia (kopia się nie zmienia).

### AC → test (happy path)
| AC | Test |
|---|---|
| AC-1 | `tree_screen_test`: „ISSUE-049 AC-1 (3a, D51, D58)” — gest dwóch palców razem (4 ×, do granicy) i osobno, podwójne dotknięcie: cały czas 91 osób; na końcu cały poziom w obszarze i na środku, bez pigułki; przycisków „Przybliż” / „Oddal” nie ma · `tree_layout_test` „AC-2, AC-3 (D50, M2)” — liczby i układ jak w makiecie (91 / 2568 dp / 3 skrzyżowania itd.) |
| AC-2 | `tree_layout_test`: Michał, Leon, Natalia na 1, rodzice Natalii na 2 · `tree_screen_test` „AC-2, AC-3 (3, D55, D58)”: + → „Przez 1 związek”: rodzice Natalii, Patrycja, Konrad; pigułka „Przez 1 związek · 113 osób (+22)”; „Ja” w tym samym miejscu, skala 1 (K1) |
| AC-3 | te same testy: Konrad na 2, jego rodzice i brat na 3; pigułka „(+3)”; + nieaktywne na 3 (dotknięcie nic nie zmienia); − dwa razy — „(−3)”, „(−22)” |
| AC-4 | `tree_presentation_test` „ISSUE-049 AC-4 (D56, T2)”: gest dwóch palców (dwa wskaźniki) — skala > 1,5, osób tyle samo; na listwie bez przybliżania, − nieaktywne na „Linii krwi”; + na listwie → 113 osób, skala bez zmian, pigułka pod „Zakończ prezentację”; po wyjściu ten sam poziom i skala · „element 11, D56” — przy 200% dotknięta osoba na środku w tej samej skali, dotknięcie środka po przeciągnięciu wraca |
| AC-5 | `tree_connect_test` „ISSUE-049 AC-5 (D57)”: Ja → Ryszard Przykładniak — poziom sam do 3, ścieżka w kadrze, po końcu poziom i skala zostają, ścieżka do Wandy go nie obniża · `tree_layout_test` „every path from Ja has its level” (115 ścieżek, `also` puste, poziom niżej nie mieści ścieżki) · F2 — imiona ścieżki w całości 24 dp od krawędzi |

Dodatkowo: **D52** — przy celu < 24 dp dotknięcie przybliża do 0,45, środek bez zmian, podpowiedź „przybliż” → „w środek” · **D57** — wybór zostaje dla nowego drzewa z zakładki, Teofil ma jeden poziom (+ i − nieaktywne, dotknięcie bez pigułki), wybór wraca przy „Ja” · **D50** — krew to przodkowie i ich potomkowie, nie partner; Teofil w niczyim poziomie; cykl w danych nie zawiesza `unionLevels` · ślad partnera i ślad z wieńcem — od Tadeusza (Genowefa ma pierwszego męża poziom wyżej), także według roku · pigułka w roku 1950 liczy 32 osoby (+ i − z powrotem).
**Dostępność** (retro 3, R2): start drzewa i poziom 3 — `androidTapTargetGuideline`, `labeledTapTargetGuideline`, każdy przycisk z akcją dotknięcia (nieaktywny — bez akcji, z `enabled: false`); „Dalsza rodzina” / „Bliższa rodzina” — przyciski z etykietą, na krańcach „niedostępne”. Runda 1 (do stopu #2): etykieta „Kogo pokazać: Linia krwi — zmień” i wiersze listy z `selected` — usunięte z ekranem (D58).
**Testy przeniesione na nowe zachowanie** (stare sprawdzały S2, poziom 2 i jego dopasowanie): `tree_layout_test` (liczby SPIKE-002 → poziomy według związków; `levelsFrom` zostaje z liczbami 6 → 20 → 66 → 104 → 113 → 116), `tree_time_test` (rok bez nikogo 1860), `tree_screen_test` (AC-1, S2 → 4 nowe testy, AC-5, AC-7, tryb prezentacji × 4), `tree_time_screen_test` (91 osób, 1950: 32), `tree_presentation_test` (1950: 33 węzły, dopasowanie → D56), `tree_connect_test` (F2 po końcu skala zostaje, D49 przez węzeł Agnieszki), `fictional_family_test` (117 osób, 42 związki, 44 bez rodziców, 91 → 113 → 116).

### Found by `qa` (poprawione przed stopem, w roli `dev`)
1. **Listwa trybu prezentacji przepełniała się** — z czytnikiem sterowanie jest od wejścia, zanim telefon się obróci: listwa 302 dp, etykieta i − / + o 6,5 dp za szerokie; przy 200% etykieta zabierała miejsce paskowi czasu. Teraz etykieta najwyżej 30% listwy, a etykieta i − / + dopiero od 560 dp (telefon poziomo ma zawsze więcej).
2. **Kadr ścieżki nie mieścił imienia** („Zdzisław” 0,4 dp za marginesem — powtórka MAJOR z przeglądu ISSUE-039): skala całego poziomu liczy same miejsca osób, a imiona przy oddaleniu nie maleją. Kadr ścieżki może zejść do 0,08.

### Runda 2 — po stopie #2 (D58)
Rytuał WZ-024 po zmianie i po poprawkach przeglądu: `dart format` — bez zmian · `flutter analyze` — czysto · `flutter test --timeout 120s` — **964 zielone** (testy etykiety
i listy zastąpione testami + / −; zoom przyciskami → gest dwóch palców, `test/support/gestures.dart` — `pinch`). Nowe sprawdzenia: + / − — przycisk, etykieta, `enabled`
na krańcach (start, poziom 3, osoba z jednym poziomem); nieaktywny bez obrysu; „Przybliż” / „Oddal” nie ma; na listwie − / + i dotknięcie 23 dp od środka celu 48 dp;
pigułka w trybie prezentacji pod „Zakończ prezentację”; kadr ścieżki F2 z dala od + / − poziomu; zmiana poziomu kończy podświetlenie ścieżki (D49).

**Przegląd `ui` rundy 2** (subagent bez historii, [[drzewo]] v1.25, zrzuty `emu049\shots\` 24–30): 0 BLOCKER, 0 MAJOR, 7 MINOR — **wszystkie poprawione przed stopem**:
4 na ekranie (*Dev report* → *Runda 2*) i 3 w dokumentacji — *States* podawały „emulator 360 dp” przy zrzucie 411 dp (teraz pomiar na 360 dp, zrzut 31), *Navigation*
mówiła o „+ / − (3a)”, [[style-b]] *Thresholds* — „przybliżenie (+) daje ≥ 48 dp” (przepisane). Zgodne: elementy i stany według v1.25, bursztyn tylko w dozwolonych rolach,
kontrast z `theme.dart` — róg: obrys 3,40, ikona 10,02, nieaktywna 5,01; listwa: obrys 3,10, ikona 10,98, nieaktywna 5,50; pigułka 10,02; semantyka `button` /
`enabled` / etykieta; twarde spacje w pigułce; na zrzutach tylko wymyślone osoby. Nie sprawdzone: słowo stanu w TalkBacku („niedostępne” mówi system).

### Przegląd `ui` (subagent, zrzuty `emu049\shots\` 01–08, 10–16, 18–22)
0 BLOCKER, 0 MAJOR, 3 MINOR — **wszystkie poprawione przed stopem**: strzałka etykiety rośnie z tekstem (reguła 3); twarde spacje po „·”, po „np.” i między liczbą a „osób” (reguła 6); lista liczy osoby w roku suwaka jak pigułka (D37). Odstępstwa `dev` 1–3 i poprawki `qa` 1–2 przyjęte → [[drzewo]] **v1.24**, [[style-b]] **v1.45** (reguła 13 — osoba z widocznym imieniem nad sąsiadami). Kontrast z `theme.dart`: etykieta — obrys 3,40:1, nazwa 10,02:1, strzałka 8,04:1 (na listwie 3,10 · 10,98 · 8,81); lista — 10,02 · 5,01 · `check` 8,04; pigułka 10,02.

### Family data
W zmianach tylko osoby z rdzeni wymyślonych (Wymyśl-, Zmyśl-, Testow-, Przykład-); bez baz, kopii, eksportów i zdjęć. Zrzuty i zrzuty drzewa leżą poza repo (katalog sesji). **Uwaga:** zrzut `emu049\shots\09-picker.png` pokazuje wpis autora z emulatora (z wcześniejszego stopu) — poza repo, do kosza, bez przepisywania. Pozycja bez sieci — logcat bez zmian.

### Emulator (agent, przed stopem)
Przejście AC — *Dev report → Found on the emulator*; po poprawkach `qa` i przeglądu: tryb prezentacji przy 200% (zrzut 22 — listwa w jednym rzędzie, suwak ok. 282 dp) i lista z twardymi spacjami (zrzut 23). Na `Grobing_Restore` ostateczny build profile.

### Stop #2
- **Runda 1 — 2026-10-19, autor (zrzut z emulatora, zakreślone + / − w rogu):** *„Mój feedback 1) jednak zamiast "kogo pokazać na drzewie" chciałbym mieć prosty
  "+" "-" 2) Obecny "+" "-" można zastąpić/usunąć bo wystarczy funkcja ręcznego zoom-in/out. Te komentarze odnoszą się tak samo do widoku w aplikacji i na
  telewizorze”* → `ui` [[drzewo]] v1.25 (D58), [[style-b]] v1.46 (wyjątek od SC 2.5.1 — oddalanie tylko dwoma palcami), `dev` i `qa` — runda 2 wyżej.
- **Runda 2 — 2026-10-19, autor: *„ok”*** (jedna odpowiedź na trzy kroki). Sprawdzone na urządzeniu (logcat emulatora, bez danych): po ostatnim przejściu agenta
  (12:27) aplikacja rysowała klatki o 12:56–12:57 (1243 klatki, `FRAME_LOG`), a o 12:57:17 otwarła systemowy ekran przesyłania (krok 3 — wejście w tryb prezentacji).
  1. **+ / − poziomu i pigułka** — ✅ **ok ze śladem** (klatki 12:56–12:57; kroku nie da się odróżnić od 2 w logu).
  2. **Oddalanie dwoma palcami, przybliżanie bez przycisków** — ✅ **ok ze śladem** (te same klatki).
  3. **Tryb prezentacji, − / + na listwie, pigułka pod sterowaniem** — ✅ **ok ze śladem** (ekran przesyłania 12:57:17, klatki po nim).

### For ISSUE-032 → Hand checks
- **B** — szczypanie na telefonie w trybie prezentacji z obrazem na telewizorze: czy przybliżanie i oddalanie płynie na telewizorze (emulator przez `adb` nie szczypie;
  w teście ekranu — dwa wskaźniki).
- **B** — cały obraz z kanapy: drzewo oddalone do całego poziomu na telewizorze — czy widać, kto jest kim (okręgi ok. 15 dp, ok. połowa imion).
- **B** — płynność oddalania do całego drzewa na telefonie (emulator: ok. 4 pp więcej wolnych klatek niż build odniesienia, w jego rozrzucie).
- **B** — oddalanie tylko dwoma palcami (D58): czy ktoś z rodziny nie radzi sobie bez przycisku — *Obali* wyjątku [[style-b]] v1.46.
- **B** — TalkBack na żywo: „Dalsza rodzina” / „Bliższa rodzina” i słowo stanu nieaktywnego, pigułka czytana po zmianie — nieprzetestowane na żywo (w testach semantyka).

### Verdict
**APPROVED** (self-check, 2026-10-19, z uwagami): każde AC z testem happy-path i przejściem na emulatorze; dwie rundy przeglądu `ui` — runda 1: 3 MINOR poprawione,
runda 2 (po zmianie autora na stopie #2, D58): 7 MINOR poprawione (4 na ekranie, 3 w dokumentacji); bez zmiany bazy (v15) — bez testu migracji i odtworzenia; 964
testy zielone. Uwagi: AC-1 zmienione na stopie #2 (bez + / − przybliżania); oddalanie tylko dwoma palcami — świadomy wyjątek od SC 2.5.1 (decyzja autora, *Obali*
w [[drzewo]] D58); klatki zmierzone w rundzie 1, w rundzie 2 bez nowego pomiaru (zmiana przycisków i pigułki, nie drzewa); szczypanie na żywo i TalkBack — lista B.
Szukałem i nie znalazłem: danych rodziny w zmianach (osoby tylko z rdzeni Wymyśl-, Zmyśl-, Testow-, Przykład-), przycisku bez akcji dotknięcia (poza nieaktywnymi z
`enabled: false`), celu < 48 dp, koloru jako jedynego nośnika stanu, literalnych twardych spacji w źródle, nakładania pigułki na rok i sterowanie przy 200%.
