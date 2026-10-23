---
title: "ISSUE-055 — „Połącz dwie osoby” from the person on the tree, a path that stays until × or back and shows only the tree; a portrait / landscape button on the tree and the migration map"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-011-polacz-dwie-osoby]]"
depends-on: "[[ISSUE-039-connect-two-people]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-23
verdict-reviewer: self-check
source: "`/pm` 2026-10-22 — pierwsze użycie MVP z prawdziwą rodziną (drzewo *„działało bardzo płynnie”*); uwagi autora w `CURRENT_STATE.md` → *In progress*, pozycja 4 kolejki (*„to nie bug, tylko feature”*); kolejka autora 2026-10-23: 4 → 5 → 6; rozpisanie `docs` w auto-flow po `pm`, 2026-10-23"
created: 2026-10-23
updated: 2026-10-23
---

# ISSUE-055 — „Połącz dwie osoby” od osoby z drzewa i obrót ekranu

> Uwagi autora po pierwszym pokazie drzewa rodzinie (`/pm` 2026-10-22): „Od” to osoba zaznaczona na drzewie; przybliżanie dwoma palcami nie kończy
> ścieżki; ścieżka zostaje do „×” albo gestu wstecz; w trakcie ścieżki samo drzewo, bez suwaka czasu; przycisk pion/poziom w drzewie i na mapie
> migracji — *„cała aplikacja idzie na telewizor”*, *„to nie bug, tylko feature”*.
>
> Rozpisanie przed `ui` (retro 4, R2). **Pozycja zmienia ekran drzewa i część „Mapa” → `ui` przed `planning`.** Bez zmiany bazy (v15) — aktualizacja
> ze sklepu przed wyjazdem na Wszystkie Święte (`CURRENT_STATE.md` → *In progress*, „Zasady terminu”).

## Why one item, not two
Ścieżka i obrót to dwa miejsca w kodzie, ale jeden cel: autor pokazuje drzewo rodzinie, przy telefonie i na telewizorze przez przesyłanie całego
ekranu. Autor postawił je w kolejce jednym punktem. Gdyby `ui` pokazał, że obrót to osobny temat (np. dotyka wszystkich ekranów — *Open* 5), podział
proponuje łańcuch, a decyduje autor na stopie #1. Każda pozycja to osobna sesja (`autonomous-flow.md` → *One item per session*).

## Decisions this changes — on purpose
1. **[[drzewo]] D49 — „Każde otwarcie zaczyna od „Ja”** (element 7) → „Od” = osoba zaznaczona na drzewie.
2. **[[drzewo]] D49 — koniec podświetlenia: „każde działanie, które zmienia drzewo (dotknięcie, wstecz, poziom, rok, ▶, przesyłanie)”**, a w kodzie także
   dwa palce (`tree_screen.dart`: `pointerCount > 1 && _path != null` → `_endPath`) → ścieżka zostaje do „×” albo wstecz. *Obali* D49 — *„autor chce
   kończyć podświetlenie tylko przez wstecz”* — **trafione**, z dodanym „×”.
3. **[[drzewo]] D48 i elementy 5–6 w trakcie ścieżki** — dziś wybór „Do” ustawia rok na „dziś”, a karta i suwak czasu zostają na ekranie → samo drzewo,
   bez suwaka.
4. **Orientacja** — dziś poza trybem prezentacji aplikacja idzie za ustawieniem obracania w telefonie (`presentation_mode.dart` → `leavePresentation`),
   a poziomo staje sama tylko w trybie prezentacji ([[drzewo]] element 11, [[mapa-migracji]] element 13) → przycisk pion/poziom w drzewie i na mapie.

## What to build (kierunek — szczegóły `ui`)
### 1. Ścieżka
- **„Od” = osoba zaznaczona na drzewie** — osoba w środku ([[drzewo]] element 4); kafel „Od” w oknie (element 7) pokazuje ją od razu;
- **dwa palce nie kończą ścieżki** — przybliżanie i oddalanie zostawiają wyszarzenie, linię w akcencie i pierścienie;
- **ścieżka zostaje do „×” albo gestu wstecz** — bez limitu czasu;
- **w trakcie ścieżki samo drzewo**, bez suwaka czasu (element 6); po końcu suwak wraca.

### 2. Obrót
- **przycisk pion/poziom w drzewie i w części „Mapa”** ([[mapa-migracji]]) — działa także przy zablokowanym obracaniu w telefonie;
- drzewo i mapa w poziomie poza trybem prezentacji — układ do sprawdzenia: przy włączonym obracaniu w telefonie już dziś się obracają, ale tego nikt
  nie oglądał (lista B w [[ISSUE-032-mvp-install]] → *Hand checks* ma „telefon trzymany poziomo” tylko dla mapy Polski).

## Acceptance Criteria (runda 2 — `planning` po decyzjach autora na prototypie, 2026-10-23)
- [ ] **AC-1 — „Od” z drzewa** ([[drzewo]] D78). *Given* w środku drzewa jest Piotr Wymyślony *When* dotykam „Połącz dwie osoby” *Then* kafel „Od” pokazuje
      Piotra, a „Do” jest pusty; ikona jest także na drzewie bez wybranego „ja” (wejście z „Pokaż w drzewie”).
- [ ] **AC-2 — gesty nie kończą ścieżki** (D79). *Given* ścieżka na drzewie *When* przybliżam i oddalam dwoma palcami, przeciągam, dotykam dwa razy albo
      dotykam osoby *Then* wyszarzenie, linia w akcencie, pierścienie i baner zostają.
- [ ] **AC-3 — koniec przez wstecz** (D79, D81; **bez „×” — decyzja autora na panelu 2**). *Given* ścieżka uruchomiona przy suwaku na 1950 *When* robię gest
      wstecz *Then* podświetlenie się kończy, karta i suwak wracają z rokiem 1950, „Od” stoi w środku, skala zostaje.
- [ ] **AC-4 — samo drzewo** (D80). *Given* ścieżka na drzewie *Then* nie widać karty z suwakiem ani + / − poziomu, a baner z nazwą stoi do wyjścia.
- [ ] **AC-5 — pion / poziom** (D76, D77, D82; mapa — [[mapa-migracji]] D31). *Given* drzewo albo mapa migracji, obracanie w telefonie zablokowane *When*
      dotykam „Obróć” *Then* ekran staje poziomo w układzie L4 — bez zakładek, przełącznik i ikony nad drzewem, karta z czasem w dolnym pasku — a drugie
      dotknięcie wraca do pionu; ścieżka po obrocie zostaje.
- [ ] Nowe przyciski czytane przez czytnik, cel dotyku `meetsGuideline` w pionie i w poziomie (retro 3, R2). Tekst 200% — bez sprawdzania (decyzja autora
      2026-10-23, [[style-b]] v1.53).

## Open for `ui` (przed planem; kandydaci na prototypie — retro 2, R6)
> **Rozstrzygnięte 2026-10-23** przez `ui` z autorem na prototypie `prototyp-055.html` — [[drzewo]] v1.29 (D76–D82), [[mapa-migracji]] v1.7 (D31),
> [[style-b]] v1.54. Pytanie 4 (obrót a tryb prezentacji) — odpowiedź autora w D76.

1. **Kto jest „zaznaczony”.** Osoba w środku — ale po ścieżce w środku staje „Do” ([[drzewo]] D45), więc następne otwarcie zaczyna od poprzedniego „Do”.
   Czy to chciał autor, i czy kafel „Od” dalej da się zmienić na liście.
2. **Co jeszcze kończy ścieżkę.** Autor powiedział „×” albo wstecz. Dziś kończą też: dotknięcie osoby (pierwsze tylko kończy podświetlenie), + / −
   poziomu, rok, ▶, ⏭, „Przesyłaj na telewizor”, przełącznik „Drzewo · Mapa” i zmiana danych drzewa (v1.17 — linia biegłaby po starym układzie). Co z
   nich zostaje. Przy suwaku schowanym rok, ▶ i ⏭ odpadają same.
3. **„Samo drzewo” — ile znika.** Suwak na pewno. Karta (element 5) mówi, kim jest „Do” dla mnie, także po zniknięciu baneru (D45); + / − poziomu w
   rogu; pasek z ikonami. Gdzie stoi „×” — baner znika po ok. 4 s (element 9), więc „×” nie może żyć tylko w nim.
4. **Obrót a tryb prezentacji.** Tryb prezentacji już stawia drzewo i mapę poziomo i chowa sterowanie dla telewizora. Uwaga *„cała aplikacja idzie na
   telewizor”* mówi, że autor przesyła cały ekran, nie tylko tryb. **Najpierw jedno pytanie do autora, czego tryb prezentacji mu nie dał** (np. ścieżki
   — w trybie jej nie ma, D49), zanim powstanie drugi przycisk „poziomo” obok pierwszego. Wariant opisany tym, co autor zobaczy na telewizorze
   (pamięć: nazwa opcji po źródle; „co widać na telewizorze” — telefon i telewizor obok siebie na makiecie, *Do retro* ISSUE-050).
5. **Zasięg obrotu.** Tylko drzewo i mapa, czy cała aplikacja — co się dzieje po wyjściu z drzewa poziomo do osoby, cmentarzy, grobu; czy przycisk
   pamięta wybór; jak wejście i wyjście z trybu prezentacji wraca do orientacji z przycisku.
6. **Prior art:** Android 9+ przy zablokowanym obracaniu sam pokazuje przycisk obrotu przy krawędzi ekranu, gdy telefon się przekręci (*rotation
   suggestions*) — `ui` sprawdza w dokumentacji Androida i na telefonie autora (nawigacja gestami), czy to nie wystarcza albo czy przycisk aplikacji z
   nim nie koliduje.
7. **Prototyp.** Zmiana zachowania na istniejącym ekranie i nowe przyciski → klikalny prototyp albo makieta na stop #1 (retro 1, R5), link `file:///`.

## Out of scope
- „Połącz dwie osoby” w trybie prezentacji (D49) i animacje ścieżki na telewizorze → opowieść rodziny, pozycja 6 kolejki
  ([[2026-10-14-opowiesc-rodziny-i-wieniec]]) — chyba że odpowiedź na *Open* 4 to zmieni; decyzja na stopie #1.
- Czytelność linii przy dużej rodzinie → pozycja 5 kolejki.
- Tabliczka imienia zasłaniająca ślad dalszej rodziny (MINOR z [[ISSUE-035-tree-names-shrink-my-voice]]) → *Poza tą kolejnością*.
- Słownik i baner (D47, „przyrodni”) — bez zmian; rodzeństwo przyrodnie → *Poza tą kolejnością*.

## What this will not give
- **Obraz na telewizorze to kopia ekranu telefonu** ([[drzewo]] D29, NFR-005). Poziomo z przycisku pokaże na telewizorze także pasek, kartę i przyciski
  aplikacji — tryb prezentacji istnieje, żeby ich tam nie było. Czysty telewizor ze ścieżką to dalej pozycja 6.
- Przy „Od” ≠ „Ja” — teraz częściej — baner ma dwie linie (D47); *Obali* D47 („Wnuczka” — czyja?) dostaje więcej okazji.

## Notes
- Kod: `lib/app/tree/tree_screen.dart` (`_endPath`, `_clearPath`, gest dwóch palców), `lib/app/tree/presentation_mode.dart` (orientacja).
- Uwaga *„cała aplikacja idzie na telewizor”* częściowo odpowiada na wiersz listy B w [[ISSUE-032-mvp-install]] → *Hand checks* („co system pokazuje po
  wyborze telewizora — cały ekran / jedna aplikacja”) — przy zamknięciu `docs` aktualizuje ten wiersz tym, co autor potwierdzi.
- Odwraca decyzje [[ISSUE-039-connect-two-people]] (D48, D49) — `ui` zapisuje nowe wersje w [[drzewo]] i [[mapa-migracji]], stare zostają z adnotacją.

## Stop #1 (2026-10-23) — ✅ „tak”
Prototyp `prototyp-055.html` (decyzje autora na panelach 1–5: D76–D81, D31) i plan niżej z decyzjami projektowymi (D78 bez „ja”, D79 co jeszcze kończy
ścieżkę, D80 + / − schowane, D82 „Obróć”, pigułka i dymek ⏭ pod górnym rzędem, jedna pozycja) — autor: *„tak”*.

## Implementation plan (`planning`, 2026-10-23)
> Specyfikacje: [[drzewo]] v1.29 (elementy 1, 7–10, nowy 12; D76–D82) · [[mapa-migracji]] v1.7 (element 1, D31) · [[style-b]] v1.54 (reguła 12).
> Prototyp: `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/8d325e2e-0b12-4ac8-b0cf-028478b1a72b/scratchpad/prototyp-055.html`
> (panele 1–6, decyzje autora na panelach 1–5). **Bez zmiany schematu** (v15) — migracji nie ma, kopia i odtworzenie bez zmian.

### Scope diff
1. **„Od” z drzewa (D78)** — `connect_dialog.dart`: `showConnectDialog` dostaje osobę ze środka i od niej zaczyna kafel „Od” (dziś `meId`); `tree_screen.dart`
   `_connect` bez warunku `family.meId == null`, a ikona „Połącz dwie osoby” w `_bar()` jest przy każdym drzewie. Baner bez „ja” ma dwie linie —
   `pathBannerText` już to robi (`fromMe` fałszywe).
2. **Ścieżka zostaje do wstecz (D79)** — `_endPath` zostaje w: `PopScope` (wstecz), `_setPart` (przełącznik), `_cast` (przesyłanie), `_connect` (nowa
   ścieżka zastępuje starą) i przy zmianie danych drzewa (`_listen`, v1.17). Znika z: gestu dwóch palców (`onInteractionUpdate`, `pointerCount > 1`),
   `_zoom` (podwójne dotknięcie), `_zoomIn` (dotknięcie miejsca < 24 dp dalej przybliża), `_tap` i `_pointerUp` przy `_lit` (dotknięcie osoby i pustego
   miejsca — nic). W `_setLevel`, `_chooseYear`, `_togglePlay`, `_nextEvent`, `_open` zostaje jako zabezpieczenie — w trakcie ścieżki ich elementów nie
   widać. Osoby w trakcie ścieżki bez akcji dotknięcia w semantyce (czytnik nie mówi „otwórz”).
3. **Samo drzewo i baner do końca (D80)** — `_content`: karta (`_TreeCard` z `TreeTimeBar`) i `_levelButtons` tylko przy `_path == null`; baner bez
   timera przy ścieżce — `_bannerTime` (D43) zostaje tylko dla „bez ścieżki” (element 10). Obszar drzewa rośnie, gdy karta znika — kadr ścieżki liczy się
   w nowym rozmiarze (dziś „nowy rozmiar przed następnym dotknięciem kadruje ścieżkę od nowa”).
4. **Po wyjściu (D81)** — `_showPath`: bez `_focus = to`; gdy „Od” ≠ osoba w środku (kafel zmieniony w oknie) — przestawienie środka na „Od” jak po
   dotknięciu; poziom liczony od „Od” (`pathLevel(graph, from, …)`). Rok sprzed ścieżki zapamiętany przy pierwszej ścieżce z rzędu (nowa ścieżka go nie
   nadpisuje); `_endPath` go przywraca (▶ stoi). Skala, poziom i środek zostają.
5. **„Obróć” (D82)** — glif `screen_rotation` dołożony do fontu ikon (`tool/icons/glyphs.txt`, `tool/icons/build_symbols.py` → `assets/fonts/grobing-symbols.ttf`,
   `Glyphs.rotate` w `lib/app/widgets/glyphs.dart`; README → *Ikony*). Przycisk w `_bar()` na lewo od „Połącz dwie osoby” (w „Mapie” — na lewo od
   „Przesyłaj”), `tooltip` i czytnik „Obróć poziomo” / „Obróć pionowo”. Orientacja w nowym `lib/app/tree/tree_orientation.dart`: wybór na czas działania
   aplikacji (jak `treeTempo`), `SystemChrome.setPreferredOrientations` — poziomo `[landscapeLeft, landscapeRight]`, pionowo `[portraitUp]`, bez wyboru
   `[]`. Drzewo stosuje wybór przy wejściu i po powrocie z widoku osoby; zwalnia go przed otwarciem widoku osoby i przy wyjściu z zakładki (`dispose`);
   `leavePresentation` wraca do wyboru, a nie do `[]`. Ścieżki nie kończy.
6. **Układ poziomy L4 (D77, D31; element 12)** — `tree_screen.dart` `build`: przy `MediaQuery.orientationOf(context) == Orientation.landscape` i poza trybem
   prezentacji — bez `GrobingTabBar` i bez wiersza `_bar()`; nad obszarem drzewa nakładki: przełącznik (12 dp od lewej i od góry) i pigułka ikon (8 dp od
   prawej i od góry), na powierzchni z obrysem; **dolny pasek** — karta w jednym rzędzie (wariant poziomy `_TreeCard`: okrąg 40 dp, imię 15 sp, opis 13 sp,
   w „Mapie” linia „gdzie”, tekst do 300 dp, zawija się bez ucinania; `TreeTimeBar` w tym samym rzędzie; „Pokaż ›”); + / − nad paskiem; baner ścieżki w
   górnym rzędzie między nakładkami; kadr ścieżki pod górnym rzędem (64 dp zamiast wysokości baneru). Ta sama budowa dla części „Mapa” (ten sam ekran).
   **Decyzja `planning`** (z reguły trybu prezentacji, element 11): pigułka poziomu (3) i dymek ⏭ (6a), które w pionie stoją u góry drzewa, w poziomie stoją
   **pod górnym rzędem**, 68 dp od góry — na stop #1.
7. **Wydanie:** `1.0.3+6` (`pubspec.yaml`, `appVersion` w `settings_screen.dart`) — aktualizacja ze sklepu przed wyjazdem.

### Files (likely)
`grobing-code`: `lib/app/tree/tree_screen.dart` · `lib/app/tree/connect_dialog.dart` · `lib/app/tree/tree_orientation.dart` (nowy) · `lib/app/tree/presentation_mode.dart` ·
`lib/app/tree/tree_time_bar.dart` (jeśli rząd w pasku poziomym wymaga wariantu) · `lib/app/widgets/glyphs.dart` · `tool/icons/glyphs.txt` ·
`tool/icons/build_symbols.py` · `assets/fonts/grobing-symbols.ttf` · `pubspec.yaml` · `lib/app/settings/settings_screen.dart` · `README.md` (*Ikony*, akapit o
orientacji drzewa). Testy (`qa`): `test/app/tree/tree_connect_test.dart`, `tree_screen_test.dart`, `presentation_mode_test.dart`, `migration_map_test.dart`.

### AC → test / check
| AC | Test (`qa`) | Na emulatorze (agent) |
|---|---|---|
| AC-1 „Od” z drzewa | widżet: środek — wymyślona osoba (nie „ja”) → okno, kafel „Od” z nią; drzewo z „Pokaż w drzewie” bez „ja” — ikona jest, baner w dwóch liniach | dotknięcie osoby → ⛓ → kafel „Od” (zrzut) |
| AC-2 gesty | widżet: ścieżka → skalowanie dwoma palcami, podwójne dotknięcie, dotknięcie osoby i pustego miejsca — ścieżka, wyszarzenie i baner zostają | podwójne dotknięcie i dotknięcie osoby w trakcie ścieżki (dwóch palców `adb` nie zrobi — pokrywa test) |
| AC-3 wstecz | widżet: wstecz → koniec, karta i suwak wracają z rokiem sprzed ścieżki, „Od” w środku, skala bez zmian; przełącznik „Mapa” i „Przesyłaj” też kończą; nowe „Do” zastępuje ścieżkę i nie nadpisuje roku | ścieżka przy 1950 → `keyevent 4` → suwak na 1950 (zrzut) |
| AC-4 samo drzewo | widżet: w trakcie ścieżki nie ma karty, `TreeTimeBar` ani + / −; baner stoi po 10 s; „bez ścieżki” — baner znika po 4 s jak dziś | ścieżka → zrzut po 10 s |
| AC-5 pion / poziom | widżet: „Obróć” → `setPreferredOrientations` z poziomymi (kanał platformy w teście), drugie — z pionową; przy rozmiarze poziomym brak `GrobingTabBar`, są nakładki i dolny pasek, w „Mapie” linia „gdzie”; ścieżka po zmianie rozmiaru zostaje; wyjście z trybu prezentacji wraca do wyboru | autoobracanie wyłączone (`settings put system accelerometer_rotation 0`) → „Obróć” → L4 na drzewie i mapie, ścieżka poziomo; widok osoby → pion, powrót → poziomo; tryb prezentacji → wyjście → poziomo |

**Dostępność:** `meetsGuideline` i `expectEveryButtonTappable` w pionie, w poziomie i w trakcie ścieżki. **Warstwa danych:** nie dotyka (bez schematu, bez
kopii) — testu migracji i próbnego odtworzenia nie ma.

### Manual verification (stop #2)
**Agent na emulatorze** (przed stopem, zrzuty; `Grobing_Restore` — stan sprzed demo z `_pokaz`, demo z powrotem po pozycji; ekran ustawiony na 412 × 915 dp
jak telefon autora, `wm size` i gęstość w zapisie): kolumna „Na emulatorze” wyżej; przegląd `ui` (subagent) w pionie i w poziomie.
**Autor — odczucie (emulator, najwyżej 3):**
1. połącz kogoś ze środka drzewa z kimś dalekim, przybliż, poprzesuwaj i wyjdź gestem wstecz — czy ścieżka trzyma się tak, jak chciałeś?
2. „Obróć” na drzewie i na mapie — czy w poziomie jest dość miejsca na drzewo?

**Lista B** ([[ISSUE-032-mvp-install]] → *Hand checks*, od razu — krok z telewizorem, retro 4 R4): przesyłanie z szybkich ustawień, drzewo poziomo ze ścieżką
na telewizorze — czy rodzina widzi drzewo i nazwę pokrewieństwa.

### Decisions for stop #1 (projektowe — „tak” przyjmuje je z planem)
- **D78:** ikona „Połącz dwie osoby” także na drzewie bez wybranego „ja”.
- **D79:** ścieżkę kończą też przełącznik „Mapa”, „Przesyłaj na telewizor”, nowe „Do” i zmiana danych; dotknięcie osoby nic nie robi.
- **D80:** + / − poziomu schowane w trakcie ścieżki.
- **D82:** „Obróć” trzyma wybór w zakładce Drzewo do zamknięcia aplikacji; widok osoby i inne zakładki idą za ustawieniem telefonu — przy telewizorze
  wyjście z drzewa obróci obraz do pionu.
- **`planning`:** pigułka poziomu i dymek ⏭ w poziomie pod górnym rzędem.
- **Jedna pozycja, nie dwie:** ścieżka (mała zmiana) i układ poziomy (większa) w jednej paczce `1.0.3+6`; podział to druga sesja przed wyjazdem.

### Out of scope
- ścieżka w trybie prezentacji i animacje opowieści → pozycja 6 kolejki ([[2026-10-14-opowiesc-rodziny-i-wieniec]]);
- poziomo na innych ekranach (osoba, grób, cmentarze) — autor nie wybrał „cała aplikacja poziomo” (D76);
- „×” albo „Zakończ” na banerze — [[drzewo]] D79 *Obali*;
- czytelność linii przy dużej rodzinie → pozycja 5 kolejki;
- tekst 200% (decyzja autora 2026-10-23).

## Dev report (`dev`, 2026-10-23)
Flutter 3.41.1 (przypięty). `flutter analyze` — czysto; `dart format` — bez zmian. Bez zmiany schematu (v15). Wersja `1.0.3+6`.

### Built
1. **„Od” z drzewa (D78)** — `connect_dialog.dart`: `showConnectDialog(from:)`, kafel „Od” od osoby w środku; ikona „Połącz dwie osoby” przy
   każdym drzewie (także bez „ja”); okno nie kończy ścieżki przy otwarciu — „Anuluj” ją zostawia, nowe „Do” ją zastępuje.
2. **Ścieżka do wstecz (D79)** — `_endPath` znika z gestu dwóch palców, podwójnego dotknięcia, dotknięcia < 24 dp i dotknięć osoby / pustego
   miejsca; zostaje: wstecz, przełącznik części, przesyłanie, nowe „Do”, zmiana danych. Osoby w trakcie ścieżki bez akcji dotknięcia i bez podpowiedzi
   dla czytnika (poza „przybliż” przy miejscu < 24 dp). Baner samego elementu 10 dalej kończy pierwszy dotyk (D49).
3. **Samo drzewo, baner do końca (D80)** — karta z rzędem czasu i + / − tylko bez ścieżki; baner ścieżki bez timera (D43 tylko dla elementu 10).
   Kadr ścieżki bez omijania + / − (usunięte `_underControls`).
4. **Po wyjściu (D81)** — „Od” zostaje w środku (poziom liczony od niego, `pathLevel(graph, from, …)`), rok sprzed ścieżki w `_clearPath`
   (także przy zmianie danych), zapamiętany przy pierwszej ścieżce z rzędu.
5. **„Obróć” (D82)** — glif `screen_rotation` (font przebudowany skryptem z README → *Ikony*; przebudowa bez zmian odtworzyła font z repo tabela w
   tabelę, potem +2 glify — linia i wypełnienie); `lib/app/tree/tree_orientation.dart` (wybór na czas działania aplikacji; widok osoby i wybór „ja” —
   ustawienie telefonu, powrót — wybór; ostatnia karta drzewa zdjęta ze stosu — ustawienie telefonu, licznik kart na wypadek „Pokaż w drzewie”);
   `leavePresentation` wraca do wyboru.
6. **Układ poziomy L4 (D77, D31; element 12)** — w poziomie z drzewem: bez paska zakładek i paska ekranu; `_WideTop` (przełącznik, pigułka ikon na
   powierzchni z obrysem, baner w miejscu między nimi); karta w jednym rzędzie (`_TreeCard(row:)`, imię 15 sp, opis 13 sp, tekst do 300 dp, rząd
   czasu, „Pokaż”); pigułka poziomu, dymek ⏭ i pigułka mapy (`MigrationMap.pillTop`) pod górnym rzędem; kadr ścieżki i dymka pod górnym rzędem.
   Bez drzewa (pusta baza, bez „ja”) w poziomie zostaje zwykły pasek i zakładki.
7. README → *Drzewo — obrót i układ poziomy*.

### Found on the emulator (fixed before qa)
- **a) Aplikacja w starym rozmiarze w obróconym oknie** — po „Obróć” okno się obracało, a aplikacja rysowała się w rozmiarze sprzed obrotu (pion w
  poziomym oknie i odwrotnie), aż do wyjścia z aplikacji; w pętli 8 z 8 obrotów (po pierwszym). `dumpsys activity top`: `FlutterView` 1080×2400,
  jego `FlutterSurfaceView` 2400×1080. **Przyczyna w silniku Fluttera 3.41.1** (źródła w SDK): na początku każdej klatki silnik prosi o rozmiar
  powierzchni równy klatce (`external_view_embedder.cc` → `FlutterJNI.maybeResizeSurfaceView` → `FlutterView.resizeEngineView`) — klatka w starym
  rozmiarze, która dojdzie po obrocie, przypina powierzchni stary rozmiar w pikselach i ustawia `shouldSendViewportMetrics = false`, więc następny
  `onSizeChanged` (sam obrót) nie dochodzi do Fluttera. Sondy: „najpierw `[]`, potem poziomo” — nie pomogło; `requestLayout` przy
  `onConfigurationChanged` — nie pomogło (za wcześnie, a parametry powierzchni są sztywne). **Poprawka** w `MainActivity.kt`: nasłuch zmiany
  układu widoku Fluttera i jego powierzchni — powierzchnia, która nie wypełnia widoku, wraca do `MATCH_PARENT`, a `requestApplyInsets` wysyła
  rozmiar widoku do Fluttera (`onApplyWindowInsets` → `sendViewportMetricsToFlutter`). Po poprawce **12 z 12** obrotów dobrych; w logcat
  `GROBING_SURFACE … refitted` przy każdym. Ten sam wyścig najpewniej stał za „6 z 8” zawieszeniami trybu prezentacji w [[ISSUE-034-tree-presentation-mode]]
  (tam obejście `_untilLandscape` zostaje); poprawka działa dla każdego obrotu, także z czujnika telefonu.

### Deviations (do przeglądu `ui`)
1. **Lista „Od kogo?” / „Do kogo?” w poziomie z klawiaturą** — klawiatura zakrywa wszystkie wyniki (zrzut `12a`); po schowaniu klawiatury (⌄) wyniki
   są. Specyfikacja nie rozstrzyga (lista to tryb wyboru z drzewa, więc idzie za wyborem „Obróć”). Kandydaci: zostawić (A–Z bez szukania działa) ·
   lista w pionie jak widok osoby (dwa obroty obrazu na telewizorze) · wyniki nad polem w poziomie.
2. **Pasek dolny w poziomie: 64 dp rośnie** z linią „gdzie” (mapa) do ok. 78 dp — trzy linie tekstu; specyfikacja mówi „rośnie, gdy tekst się zawija”.

### Known edges
- Poprawka a) nie sprawdzona na prawdziwym telefonie (Android 13) — kandydat na listę B ([[ISSUE-032-mvp-install]] → *Hand checks*).
- `GROBING_SURFACE` loguje dwie linie na obrót (nasłuch na widoku i na powierzchni) — bez skutku dla działania.
- D78 bez „ja” i baner elementu 10 (4 s) — na emulatorze nie przechodzone (stan „bez ja” wymaga edycji bazy); pokrywają testy widżetów (`qa`).

### Emulator pass (`Grobing_Restore`, build profile `1.0.3+6`, 1080 × 2400 przy 420 dpi = 411 × 914 dp, autoobracanie wyłączone; zrzuty
`8d325e2e-…\scratchpad\emu055\shots\`)
- AC-1: Zofia w środek → ⛓ → „Od: Zofia Wymyślona” (`02`). AC-2: ścieżka Zofia → Henryk (pradziadek) — baner stoi po 10 s, podwójne dotknięcie
  i dotknięcie osoby nie kończą, karty i + / − nie ma (`03`–`06`). AC-3: wstecz → Zofia w środku, karta, + / −, „dziś”; Henryk na 1951 → ścieżka do
  wnuczki → wstecz → **1951** i Henryk w środku (`07`–`09`). AC-4: jw. AC-5: „Obróć poziomo” przy zablokowanym obracaniu → L4 (`10`); ścieżka w poziomie
  — baner w górnym rzędzie, 4 pokolenia pod nim (`12`); „Obróć” w trakcie ścieżki w obie strony — ścieżka zostaje (`13`); mapa w poziomie — pigułka
  pod górnym rzędem, „Obróć” i „Przesyłaj” (`19`); widok osoby → pion, wstecz → poziomo; prezentacja → wyjście → poziomo (`21`, `22`); pigułka
  poziomu i dymek ⏭ pod górnym rzędem (`23`, `24`); wyjście z zakładki → pion, powrót → poziomo (`25`).
- Semantyka: „Obróć poziomo / pionowo” `clickable`, granice 48 × 48 dp (126 × 126 px) w pasku i w pigułce; osoby ścieżki bez akcji.
- **Stan emulatora:** dane sprzed demo z `_pokaz` + build `1.0.3`, autoobracanie wyłączone (`accelerometer_rotation 0`) — dla stopu #2. Demo zapisane
  przed pozycją: `emu055\stan-przed-055-demo.apk` + `.tar` — **przywrócić po stopie #2** (i `accelerometer_rotation 1`).

### For `qa`
- `tree_connect_test.dart` — 10 testów sprawdza zachowanie zmienione celowo: „Do” w środku i karta „Do” (D45 → D81), koniec dotknięciem / palcami / + /
  ▶ (D49 → D79), baner 4 s (D43 → D80), brak ikony bez „ja” (D3 → D78), poziom od „Do” (→ od „Od”), `TreeTimeBar` w trakcie ścieżki (D80); F2 „ścieżka
  szersza niż ekran” — z „Od” w środku i bez karty Ja → Zdzisław mieści się w 0,71, potrzebna szersza para.
- Nowe: `tree_orientation.dart` (kanał `SystemChrome.setPreferredOrientations` w teście), układ poziomy (rozmiar widoku poziomy), `MigrationMap.pillTop`.
  Globalny `treeLandscape` — zerować między testami.

### Fixed after the ui review (`dev`, 2026-10-23)
- MINOR przeglądu: w poziomie dolny pasek kończył się 24 dp nad krawędzią ekranu (pas tła z uchwytem gestów pod nim, widoczny na telewizorze).
  Kolumna schodzi pod obszar gestów (`SafeArea(bottom:)` tylko w trybie prezentacji), karta w jednym rzędzie bierze go jako wewnętrzny dolny odstęp, a bez
  karty (ścieżka) drzewo zostaje nad nim. Na emulatorze piksele y 1000–1075 przy krawędzi = kolor powierzchni (zrzut `26`).

## Verification (`qa`, 2026-10-23)
### Tests — 1051 zielonych, `flutter analyze` i `dart format` czyste
- **`tree_connect_test.dart`** — 10 testów przepisanych na zachowanie z D78–D81 (powody w *Dev report* → *For `qa`*), 2 nowe:
  - AC-1 — Michał w środek → okno „Od: Michał Wymyślony”, „Do” pusty (D78);
  - D79 — „Anuluj” zostawia ścieżkę, nowe „Do” zastępuje ją, a rok sprzed pierwszej ścieżki zostaje;
  - bez „ja” ikona jest, okno od Wandy, baner w dwóch liniach (D78, D47; zastępuje test D3);
  - AC-2 — dotknięcie pustego miejsca, osoby spoza ścieżki, podwójne dotknięcie, jeden i dwa palce nie kończą ścieżki;
  - AC-3 — wstecz: karta, + / −, „Od” w środku; z suwakiem na 1950 → wstecz → 1950, ▶ stoi;
  - AC-4 — w trakcie ścieżki bez `TreeTimeBar` i + / −, baner po 10 s; baner elementu 10 dalej znika po czasie z „Czasu na działanie” (D43);
  - F2 na parze Ja → Ryszard Testowiak (skala ok. 0,19 — od „Ja” w środku Ja → Zdzisław mieści się w 0,71).
- **`tree_rotate_test.dart`** (nowy, 4) — AC-5:
  - „Obróć” prosi o poziom; w poziomie bez zakładek, rząd nad drzewem, karta w jednym rzędzie przy dolnej krawędzi; cele 48 dp, etykiety, kontrast;
  - „Obróć pionowo” → pion; widok osoby → ustawienie telefonu, powrót → wybór; wyjście z zakładki → ustawienie telefonu;
  - ścieżka w poziomie — baner w górnym rzędzie między przełącznikiem a ikonami, ścieżka pod nim, obrót jej nie kończy;
  - mapa w poziomie — pigułka 68 dp od góry, bez „Połącz dwie osoby”.
- **`presentation_mode_test.dart`** +1 — wyjście z prezentacji wraca do wyboru „Obróć”, a nie do ustawienia telefonu.
- **Dostępność:** `meetsGuideline` (cel, etykieta, kontrast) i `expectEveryButtonTappable` w pionie, w poziomie i w trakcie ścieżki. W kadrze ścieżki z „Ja”
  miejsca osób < 48 dp — przyjęty wyjątek oddalonego drzewa (D17, D52), tam tylko etykiety i kontrast.
- **Bez testu automatycznego:** obejście wyścigu silnika w `MainActivity.kt` (Kotlin) — przejście na emulatorze 12 z 12 obrotów, log `GROBING_SURFACE`.
- **Warstwa danych:** bez zmiany schematu i kopii — testu migracji i próbnego odtworzenia ta pozycja nie potrzebuje (pełny zestaw z testami kopii zielony).

### ui review (subagent, 2026-10-23)
0 BLOCKER / 0 MAJOR / 1 MINOR (dolny pasek w poziomie nad krawędzią — poprawione wyżej). Odstępstwa `dev` 1–2 przyjęte, [[drzewo]] v1.30 (element 7, element 12,
D77). Uwagi bez usterek: w poziomie górny rząd przykrywa rząd rodziców osoby w środku (D77, krok autora 2); szeroka ścieżka w pionie z pustym miejscem nad i pod
nią (kadr ograniczony szerokością — krok autora 1); linia w akcencie przez przygaszone imiona przy małej skali — pozycja 5 kolejki. Kontrast z tokenów: tekst
pomocniczy na powierzchni 5,01, akcent na powierzchni 8,04, obrys 3,10.

### Family data
W zmianach nie ma baz, kopii, eksportów ani zdjęć; nazwiska w testach i w pozycji tylko z wymyślonych rdzeni (fikcyjna rodzina buildu debug, rodzina sprzed
demo). Na zrzutach `19` i `22` w linii „gdzie” stoi nazwa prawdziwego miasta z danych demo emulatora i na liście „Do kogo?” wpis autora — **nieprzepisane**
do vaulta. Strażnik treści — przy `git add` (`docs`).

### Stop #2 (2026-10-23) — autor: *„ok”*
Emulator `Grobing_Restore`, build `1.0.3+6`, autoobracanie wyłączone, start: zakładka Drzewo, pion, „Ja” w środku.
- **Krok 2 (poziomo) — „ok” ze śladem:** po stopie aplikacja stoi poziomo z „Obróć pionowo” (`mCurrentRotation=ROTATION_90`, zrzut `27`) — przy
  wyłączonym autoobracaniu mógł to zrobić tylko przycisk; `GROBING_SURFACE` po restarcie bez wpisu (wyścig silnika tym razem nie wystąpił).
- **Krok 1 (ścieżka do wstecz) — „ok” bez śladu:** po stopie w środku „Ja”, poziom bez zmian — ścieżka od osoby postawionej w środku zostawiłaby ją w
  środku (D81). Zapisane jak „pomiń” → lista B.

### For ISSUE-032 → Hand checks (B)
- B — ścieżka do gestu wstecz na prawdziwych danych: przybliżanie, przesuwanie, dotknięcia w trakcie, wyjście wstecz (stop #2 krok 1 — „ok” bez śladu).
- B — telewizor: przesyłanie z szybkich ustawień, drzewo poziomo ze ścieżką — czy rodzina widzi drzewo i nazwę (krok z telewizorem, retro 4 R4).
- B — obrót „Obróć” kilka razy i z czujnika na telefonie autora (Android 13): aplikacja wypełnia ekran po obrocie (obejście wyścigu silnika w
  `MainActivity` — nieprzetestowane na żywo).
- B — TalkBack: ścieżka bez „×”, wyjście „wstecz” czytnika (nieprzetestowane na żywo).

**Werdykt `qa`: APPROVED (self-check, z uwagami)** — AC-1–AC-5 z testami; uwagi: obejście wyścigu silnika Fluttera 3.41.1 w `MainActivity` sprawdzone
tylko na emulatorze (12 z 12); krok 1 stopu #2 bez śladu; przegląd `ui` — 1 MINOR poprawiony.
