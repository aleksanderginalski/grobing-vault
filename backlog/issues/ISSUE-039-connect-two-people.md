---
title: "ISSUE-039 — Connect two people on the tree: a „Połącz dwie osoby” icon opens a window with „Od” (default „Ja”) and „Do”; the tree goes to the level that shows the path, greys out the rest, draws the line person by person and names the kinship in a banner; a „no path” banner when nothing joins them"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-011-polacz-dwie-osoby]]"
depends-on: "[[ISSUE-033-tree-from-a-person]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-14
verdict-reviewer: self-check
source: "rozpisanie US-011 (`docs` w auto-flow po `pm`, 2026-10-14) · US-011 AC-1–AC-4 · [[drzewo]] v1.15 (elementy 1, 7–10, *States* „połącz — …”, *AC → element* M11, *Open* 1a, D5, D6, D21, D26, D28) · `KinGraph.path` ([[ISSUE-024-person-view]]) · słownik nazw ([[ISSUE-033-tree-from-a-person]] D12, [[ISSUE-035-tree-names-shrink-my-voice]] G2)"
created: 2026-10-14
updated: 2026-10-14
---

# ISSUE-039 — Połącz dwie osoby

> Z rozpisania [[US-011-polacz-dwie-osoby]] (`docs` w auto-flow, 2026-10-14, **przed** `ui` — żeby plan miał plik; lekcja z
> [[ISSUE-033-tree-from-a-person]], `CURRENT_STATE.md` → *Do retro*). **Jedna pozycja na całą US** — okno bez ścieżki nic nie daje, a cztery AC
> stoją na elementach 7–10 jednego ekranu ([[drzewo]]). Podział zaproponował łańcuch, nie autor, więc na stopie #1 autor może go zmienić.
> **Pozycja zmienia ekran → `ui` przed `planning`.**

## What to build
1. **Ikona „Połącz dwie osoby”** w pasku drzewa, na lewo od „Przesyłaj na telewizor” ([[drzewo]] element 1): bez podpisu, akcent, cel 48 dp,
   `tooltip`; w stanach bez drzewa (bez „ja”, pusta baza) jej nie ma. Glif — *Open for `ui`* 1.
2. **Okno z kaflami „Od” i „Do”** (AC-1, element 7): „Od” domyślnie „Ja”; kafel → lista osób jak [[osoby]] (wyszukiwarka i A–Z); wybór
   drugiej osoby zamyka okno i uruchamia ścieżkę. Lista — ta sama co w [[osoby]], nie druga.
3. **Ścieżka na drzewie** (AC-2, element 8): najniższy poziom, na którym widać obie osoby; ścieżka w kadrze; osoby spoza ścieżki wyszarzone
   (ok. 30%); linia w akcencie od osoby do osoby (ok. 0,7 s na krok), osiągnięta osoba dostaje pierścień; przy ograniczeniu animacji w systemie
   — od razu cała ścieżka (SC 2.3.3, [[drzewo]] D5). Dotknięcie drzewa albo wstecz kończy podświetlenie.
4. **Baner z nazwą** (AC-3, element 9): ok. 4 s u góry drzewa, opis ze słownika z [[US-009-drzewo-od-osoby]] AC-5. Dla „Od” = „Ja” — ten sam
   tekst co w karcie drzewa (G2: „Siostra cioteczna babci mojej żony”, [[drzewo]] D28). Dla „Od” ≠ „Ja” — *Open for `ui`* 2.
5. **Bez ścieżki** (AC-4, element 10): baner „Te osoby nie łączą się — w drzewie brakuje rodziny między nimi.”, drzewo bez zmian.
6. **Tekst 200% na 360 dp, czytnik, cel dotyku** — okno, kafle, lista i baner rosną z tekstem; baner i ścieżka są ogłaszane czytnikowi; testy
   `meetsGuideline` (retro 3, R2).
7. **Płynność** — przejście poziomu, kadr, wyszarzenie i linia na ok. 100 osobach: pomiar klatki na buildzie profile (`FRAME_LOG`, retro 3 R3),
   naprzemiennie z buildem odniesienia (`CURRENT_STATE.md` → *Do retro*, ISSUE-037). Wyszarzenie grupy jedną warstwą, nie przezroczystość na
   każdej osobie (lekcja z [[ISSUE-037-time-on-the-tree]] → *Dev report* → *Found* a).

## Acceptance Criteria
- [ ] **US-011 AC-1 — wybór osób.** *When* dotykam ikony „Połącz dwie osoby” *Then* otwiera się okno z kaflami „Od” (domyślnie „Ja”) i „Do”;
      kafel prowadzi do listy jak [[osoby]] (wyszukiwarka i A–Z); wybór drugiej osoby zamyka okno ([[drzewo]] element 7).
- [ ] **US-011 AC-2 — ścieżka na drzewie.** *Then* drzewo przechodzi na najniższy poziom, na którym widać obie osoby, ustawia ścieżkę w kadrze,
      wyszarza osoby spoza ścieżki, a linia w akcencie biegnie od osoby do osoby (ok. 0,7 s na krok); przy ograniczeniu animacji w systemie — od
      razu cała ścieżka ([[drzewo]] element 8, D5).
- [ ] **US-011 AC-3 — baner z nazwą.** *Then* na ok. 4 s u góry drzewa jest baner z opisem pokrewieństwa ze słownika z [[US-009-drzewo-od-osoby]]
      AC-5, np. „Siostra cioteczna babci mojej żony”; dotknięcie drzewa albo wstecz kończy podświetlenie ([[drzewo]] element 9, D6).
- [ ] **US-011 AC-4 — bez ścieżki.** *Given* osoby, które się nie łączą *Then* baner „Te osoby nie łączą się — w drzewie brakuje rodziny między
      nimi.”, drzewo bez zmian ([[drzewo]] element 10).
- [ ] **Tekst 200% na 360 dp** — okno, kafle i baner nie są ucięte ani nie nachodzą na siebie; cele dotyku przechodzą `meetsGuideline`.

## Open for `ui` (przed planem; kandydaci na makiecie albo emulatorze — retro 2, R6)
> Elementy 7–10 w [[drzewo]] są z v1.1 ([[SPIKE-004-mvp-flow-prototype]] D21, D26 — prototyp z ok. 30 osobami), czyli sprzed US-009 i US-010.
> Pytania wypisał `pm` przy starcie łańcucha; `docs` dołożył 5 i 6.

1. **Ikona** ([[drzewo]] *Open* 1a): `conversion_path` nie ma w `Icons` Fluttera 3.41.1. `Icons.link` stoi już przy „Jak łączy się ze mną” w
   widoku osoby ([[osoba]] element 7 — ta sama idea) albo własna ikona wektorowa.
2. **„Od” ≠ „Ja”.** AC-1 pozwala wybrać dowolne „Od”, a słownik mówi tylko od „ja”: `kinshipName` składa „Moja babcia”, „…mojej żony” (G2,
   [[drzewo]] D28). Jak brzmi baner, gdy żadna z dwóch osób to nie Ty — i czy „Od” inne niż „Ja” jest w MVP potrzebne. Do tego: od kogo
   liczony jest poziom i kadr, gdy „Od” nie stoi w środku drzewa.
3. **Ścieżka w roku innym niż „dziś”** (US-010, element 6, *States* „rok w przeszłości”): osoby ze ścieżki, która w tym roku się nie
   urodziła, nie widać (jej miejsce zostaje). Czy wybór ustawia „dziś”, czy linia idzie przez puste miejsca; co robi ▶ w trakcie podświetlenia.
4. **Ścieżka w trybie prezentacji** (element 11) — tam nie ma paska z ikonami, a AC tego nie mówi. Domyślnie *Out of scope*; zmiana — decyzja na
   stopie #1.
5. **Baner a czytnik i „Czas na działanie”** — baner znika po ok. 4 s. Sterowanie trybu prezentacji wydłuża się według „Czas na działanie”, a z
   czytnikiem w ogóle nie znika ([[drzewo]] D40, [[ISSUE-038-history-on-tv-and-tempo]]). Czy baner tak samo.
6. **Okno z kaflami to nowy element** → makieta na stop #1 (retro 1, R5); link jako adres `file:///`, nie ścieżka z `%TEMP%`.

## Out of scope
- Słownik nazw złożonych → [[US-009-drzewo-od-osoby]] AC-5 (zrobione: [[ISSUE-033-tree-from-a-person]], [[ISSUE-035-tree-names-shrink-my-voice]]).
- Drzewo, poziomy, karta, czas, tryb prezentacji → [[US-009-drzewo-od-osoby]], [[US-010-czas-na-drzewie]] (zrobione).
- Zdanie ścieżki w banerze i „Odtwórz jeszcze raz” — wykluczone w [[drzewo]] element 9 (D26).
- Kontrola cykli w rodzinie ([[ISSUE-019-family-relations]] → *Manual*) — `KinGraph.path` idzie wszerz i na cyklu się nie zawiesza, ale go nie
  zgłasza.
- Tabliczka imienia zasłaniająca ślad dalszej rodziny (MINOR z [[ISSUE-035-tree-names-shrink-my-voice]]) — osobna mała pozycja
  (`CURRENT_STATE.md` → *Poza tą kolejnością*); dołączenie tylko decyzją autora na stopie #1, nie po cichu.

## Notes
- **Dziś w kodzie:** ścieżka — `KinGraph.path(from, to)` w `lib/data/kinship.dart` (najmniej kroków, potem najmniej „para”, potem id, więc ta sama
  rodzina daje zawsze tę samą ścieżkę; `null`, gdy nic nie łączy) z testami ([[ISSUE-024-person-view]]); karta drzewa już jej używa
  (`lib/app/tree/tree_screen.dart`). Nazwa — `kinshipName` w `lib/app/person/kinship_names.dart`, tylko od „ja”. Drzewo — `lib/app/tree/`
  (`tree_screen.dart`, `tree_layout.dart`, `tree_painter.dart`, `tree_time.dart`, `presentation_mode.dart`). Lista do wyboru — ekran [[osoby]];
  czy da się go użyć jako wyboru, rozstrzyga plan.
- **AC-4 na emulatorze:** wymyślona rodzina drzewa (`lib/dev/fictional_family.dart`) musi mieć osobę, która z nikim się nie łączy — sprawdzić;
  jeśli nie ma, dołożyć (nazwisko tylko z wymyślonych rdzeni, `family-data.md`, retro 3 R7).
- **Emulatory** (`CURRENT_STATE.md` → *In progress*): `Grobing_Restore` — build profile z wymyśloną rodziną (106 osób, „ja” = Mateusz) i `FRAME_LOG`;
  `Medium_Phone` — release v12 z danymi testowymi autora, wyłączony, nietknięty.
- **Przy tej pozycji:** przejście AC na emulatorze przez `dev` ze stanami z *States* (retro 3, R3), przegląd `ui` przed stopem #2, testy
  `meetsGuideline` (retro 3, R2).
- **Kolumna Issue(s) w `TRACEABILITY.md`** należy do `planning` — wpis przy planie.

## Implementation plan
> `planning`, 2026-10-14. Specyfikacja (`ui`, przed planem): [[drzewo]] v1.16 — elementy 1, 7–10, *Navigation*, *States* (połącz — wybór, ścieżka, ścieżka przy 200%, bez ścieżki),
> *Sketch*, *Style B rules applied*, *AC → element*, *Candidates — ISSUE-039* (pomiar), D43–D49, *Open* 1a i 10; [[style-b]] v1.31 bez zmian. Makieta: `drzewo-039.html` w katalogu
> tymczasowym sesji `0558e715-…` (sekcje 1–7, przykłady u góry, self-test `#test=1`, zrzuty `shots-039\`). **Kandydaci tego, co widać** (retro 2, R6): A1–A4, W1–W2, F1–F2, O1–O3 i
> Y1–Y2 działają na makiecie, przed rekomendacją. *Open for `ui`* 1–6 rozstrzyga specyfikacja: 1 → D44 (A), 2 → D45 (W) i D47 (O), 3 → D48 (Y), 4 → D49 (tryb prezentacji poza MVP),
> 5 → D43 (czas jak Snackbar, komunikat stanu), 6 → makieta. Pytanie F (D46) doszło z pomiaru: 10 ze 105 ścieżek od „Ja” nie mieści się na 360 dp nawet przy skali 0,4.

### Prior art (źródła, nie pamięć)
- [[drzewo]] D43: FamilySearch pokazuje ścieżkę tylko od „mnie”; **Snackbar** Material Components bierze czas z `getRecommendedTimeoutMillis(czas, FLAG_CONTENT_ICONS |
  FLAG_CONTENT_TEXT)`, a `FLAG_CONTENT_CONTROLS` dokłada tylko przy działaniu; **WCAG 2.2 SC 4.1.3** — komunikat o wyniku działania czytnik czyta bez fokusu.
- **Z kodu** (ankieta 2026-10-14):
  - `KinGraph.path(from, to)` (`lib/data/kinship.dart`): najmniej kroków, potem najmniej „para”, potem id; `null`, gdy nic nie łączy; krawędzie parent · child · sibling · partner
    (`KinStep.married`). Działa z każdej osoby, nie tylko z „ja”;
  - `kinshipName(steps, sexOf)` (`lib/app/person/kinship_names.dart`) składa odcinki od drugiej osoby (D12) i zawsze dokłada „mój / moja / mojej / mojego” — O2 potrzebuje wariantu
    bez zaimka; odcinki i dopełniacz bez zmian;
  - `layoutTree(graph, focus, level, metrics)` (`tree_layout.dart`) widzi `levelsFrom(focus, level)` — „poziom 4 + osoby ścieżki” potrzebuje dodatkowego zbioru osób. `linesAt`
    liczy kreskę do dzieci z pasem — trasa linii ścieżki ma brać te same współrzędne, żeby leżała na liniach rodziny;
  - `_onView` zmienia poziom według skali (`treeLevelAtScale`), a `InteractiveViewer` ma `minScale: treeMinScale` (0,4) — F2 schodzi niżej tylko na czas podświetlenia;
  - `_visibleNames` — kolejność: środek, poziom, odległość; imiona ścieżki potrzebują pierwszeństwa;
  - koniec podświetlenia (D49) dotyka `_tap`, `_pointerUp`, `PopScope`, `_zoom` / `_onView` (szczypanie), `_togglePlay`, `_chooseYear` i `_cast`;
  - kanał `recommendedTimeout` (`external_link.dart` ↔ `ExternalLinks.kt`, ISSUE-038) ma na sztywno `FLAG_CONTENT_CONTROLS | FLAG_CONTENT_TEXT` — baner potrzebuje flag treści bez
    sterowania;
  - wybór osoby: `MePickerScreen` (`lib/app/people/me_picker_screen.dart`) od razu zapisuje „ja”; lista z `people_list.dart` (`PeopleSearchField`, `peopleListItems`, `PersonListCard`)
    da się użyć w ekranie, który tylko zwraca wybraną osobę;
  - `lib/dev/fictional_family.dart` (106 osób) nie ma osoby bez rodziny, a `addFictionalFamily` nie dokłada rodziny do niepustej bazy;
  - `tree_screen.dart` ma ok. 1940 linii — stan i rysowanie ścieżki do osobnego pliku.

### Stop #1 (2026-10-14) — autor: „Tak”
Rekomendacja przyjęta w całości: D1 = **A1, W2, F2, O2, Y1**, D2 (decyzje projektowe D49), D3 (bez „ja” ikony nie ma), D4 (Teofil Przykładowski w wymyślonej rodzinie), D5 (czas baneru
przez kanał z flagami treści), D6 (osoby wyszarzone poza semantyką), D7 (pomiar klatki). AC-1–AC-4 i tekst 200% potwierdzone. Specyfikacja → [[drzewo]] *Open* 1a i 10 rozstrzygnięte.

### Decisions for stop #1 (rekomendacja → „tak” przyjmuje wszystkie)
- **D1 — wygląd i zachowanie: A1, W2, F2, O2, Y1** ([[drzewo]] *Candidates — ISSUE-039*, *Open* 10, D44–D48; makieta, sekcje 1–5):
  - **A1** — ikona `link_outlined`, jak przy „Jak łączy się ze mną” w widoku osoby. A2 — trasa (`route_outlined`), A3 — punkty i linia, A4 — własna ikona;
  - **W2** — „Do” staje w środku, karta trzyma nazwę po zniknięciu baneru. W1 — „Od” w środku;
  - **F2** — drzewo maleje, aż cała ścieżka się zmieści (najmniej 0,15; po końcu skala 0,4). F1 — widok jedzie za linią (zmienia brzmienie AC-2);
  - **O2** — przy „Od” innym niż Ty dwie linie: „Piotr Przykładowy → Zofia Wymyślona” / „Wnuczka”. O1 — „Od” zawsze Ty (zmienia AC-1); O3 — „Wnuczka Piotra” (odmiana imion: 5 z 10
    trudnych imion źle);
  - **Y1** — ścieżka przestawia rok na „dziś” i zatrzymuje ▶ (zmienia D37). Y2 — rok zostaje, nieurodzeni na ścieżce jako puste pierścienie.

  *Obali* każdego — D44–D48 w specyfikacji.
- **D2 — decyzje projektowe ze specyfikacji (D49):** poziom najniższy z całą ścieżką, a dalej niż 4 — poziom 4 i osoby ścieżki; linia po liniach rodziny; baner po dojściu linii do
  „Do”; koniec podświetlenia: dotknięcie (pierwsze dotknięcie osoby tylko kończy), wstecz, przybliżanie i oddalanie, ▶, suwak, „Przesyłaj na telewizor” — przeciąganie nie kończy; okno
  od „Ja” przy każdym otwarciu, lista bez osoby z drugiego kafla; tryb prezentacji bez „Połącz dwie osoby”; bez pigułki poziomu przy wejściu w ścieżkę.
- **D3 — bez „ja” ikony nie ma** (luka w specyfikacji — decyzja planu). Drzewo z „Pokaż w drzewie” bez wybranego „ja” (D19) się pokazuje, ale okno zaczyna od „Ja”, a nazwa w banerze
  mówi od „ja”. Ikona „Połącz dwie osoby” jest więc tylko wtedy, gdy „ja” jest wybrane; „Przesyłaj na telewizor” zostaje. **Alternatywa:** ikona jest, a „Od” pusty — kolejny stan okna
  dla stanu, który trwa do pierwszego wyboru „ja”. Przy „tak” `ui` dopisuje to do [[drzewo]] element 1 w przeglądzie, jako przyjęte odstępstwo.
- **D4 — osoba bez rodziny w wymyślonej rodzinie** (`lib/dev/`, tylko debug i profile): **Teofil Przykładowski, 1910–1975**, bez rodziców i związków — jak w makietach ISSUE-038 i
  ISSUE-039 — żeby AC-4 dało się sprawdzić na emulatorze. Rodzina od „Ja” bez zmian (poziomy 6 · 20 · 66 · 99 · 106), ale test rodziny zmienia liczby: 106 → 107 osób, zmarli 31 → 32,
  bez rodziców 39 → 40 (`qa`). Na emulatorze: dane aplikacji `pm clear` i rodzina dodana od nowa, jak D4 w ISSUE-037. **Alternatywa:** agent dodaje osobę przez formularz w aplikacji
  — zostaje tylko na jednym emulatorze, bez testu.
- **D5 — czas baneru przez kanał z ISSUE-038, z flagami treści** (D43): `recommendedTimeout(time, controls: false)` → `FLAG_CONTENT_ICONS | FLAG_CONTENT_TEXT`; tryb prezentacji
  bez zmian (z `FLAG_CONTENT_CONTROLS`). Android poniżej 10 i błąd kanału — 4 s. Czytnik: `SemanticsService.announce` tekstu baneru (jak rok w `_announceYear`), bez fokusu.
- **D6 — osoby wyszarzone poza semantyką na czas podświetlenia** ([[drzewo]] *Style B rules applied*: tło bez działania). Czytnik słyszy osoby ścieżki i baner; dotknięcie
  gdziekolwiek kończy podświetlenie. Skutek dla testów: `textContrastGuideline` nie liczy imion przy 30% (2,04:1), które WCAG wyłącza jako nieaktywne.
- **D7 — pomiar klatki** przy najcięższym przypadku (ścieżka „4 +”: poziom 4, wyszarzenie, linia rosnąca co klatkę) i przy zwykłym przestawieniu środka, naprzemiennie z buildem
  odniesienia (sposób z ISSUE-038). Próg jak w ISSUE-037: wolnych klatek ≤ 10% albo nie więcej niż w buildzie odniesienia. Wyszarzenie grupy jedną warstwą, a linia ścieżki w osobnym
  `RepaintBoundary` (lekcja z ISSUE-037: przezroczystość na każdej osobie to warstwa na osobę).

### Scope — files (`{code}`)
| Plik | Zmiana |
|---|---|
| `lib/app/tree/tree_layout.dart` | `layoutTree(…, also: Set<int>)` — osoby spoza poziomu dołożone do układu („4 +”); trasa jednego kroku ścieżki z tych samych współrzędnych co `linesAt`: para — pozioma, rodzic–dziecko — przez kreskę do dzieci i jej pas, rodzeństwo — przez kreskę rodziców, bez kreski — prosto. Czysty Dart |
| `lib/app/tree/tree_path.dart` (nowy) | podświetlenie: osoby ścieżki, kroki co 0,7 s, osoby osiągnięte, koniec; malarz linii (akcent, 3 dp na ekranie przy każdej skali); baner (element 9 i 10: jedna albo dwie linie, 4 s albo czas z kanału, ogłoszenie dla czytnika) |
| `lib/app/tree/connect_dialog.dart` (nowy) | okno 7: tytuł, kafle „Od” / „Do” (obok siebie; przy tekście ≥ 150% jeden pod drugim, imię łamane tylko na spacjach), pusty kafel „Wybierz osobę”, „Anuluj”; zwraca parę osób albo nic |
| `lib/app/people/person_choice_screen.dart` (nowy) | lista „Od kogo?” / „Do kogo?”: wyszukiwarka, A–Z, karty z `people_list.dart`; bez dolnego paska; bez osoby z drugiego kafla; wybór zwraca osobę (`MePickerScreen` bez zmian) |
| `lib/app/tree/tree_screen.dart` | ikona `link_outlined` w pasku (D3); po wyborze: „Do” w środek z animacją, poziom najniższy z całą ścieżką, kadr ścieżki pod banerem (F2 — poniżej `treeMinScale` tylko w podświetleniu, `_onView` nie zmienia wtedy poziomu), Y1; wyszarzenie 30% jedną warstwą osób i linii, osoby wyszarzone poza semantyką (D6); pierwszeństwo imion ścieżki w `_visibleNames`; koniec podświetlenia we wszystkich wejściach z D2; po końcu skala < 0,4 → 0,4 z osobą w środku; bez pigułki poziomu przy wejściu w ścieżkę |
| `lib/app/person/kinship_names.dart` | nazwa bez zaimka (O2): „Wnuczka”, „Siostrzenica bratowej”, „Ciotka (siostra taty)” — te same odcinki |
| `lib/app/external_link.dart` · `android/…/ExternalLinks.kt` | `recommendedTimeout(time, controls: false)` — bez `FLAG_CONTENT_CONTROLS`, z `FLAG_CONTENT_ICONS` (D5) |
| `lib/dev/fictional_family.dart` | Teofil Przykładowski (D4) |
| `test/…` | `qa` — niżej |

**Bez nowej zależności, sieci i uprawnień** ([[NFR-005-dane-nie-opuszczaja-telefonu]]). **Warstwa danych bez zmian** — tylko odczyt (`KinGraph`), schemat ten sam: bez testu migracji i bez
próbnego odtworzenia z kopii. `lib/dev/` działa tylko w debug i profile.

### Steps for `dev`
0. **Krok 0, przed budową, na emulatorze `Grobing_Restore`:** (a) czy `TransformationController` utrzyma skalę poniżej `minScale` `InteractiveViewer` i czy pierwszy gest jej nie
   „poprawi” (F2) — jeśli poprawi, kadr podświetlenia w osobnym przekształceniu na jego czas; (b) czy TalkBack na Androidzie 16 czyta `SemanticsService.announce` baneru. Wynik w
   *Dev report*.
1. `tree_layout.dart`: `also` i trasa kroku — z testami bez ekranu.
2. `kinship_names.dart`: nazwa bez zaimka.
3. Okno, wybór osoby, ikona w pasku (D3).
4. Ścieżka: `tree_path.dart` i `tree_screen.dart` — środek, poziom, kadr, wyszarzenie, linia krok po kroku, baner, koniec, Y1, ograniczenie animacji.
5. Kanał (D5) i Teofil (D4).
6. **Przejście AC na emulatorze przed `qa`** (retro 3, R3): stany z *States* (połącz — wybór, ścieżka, ścieżka przy 200%, bez ścieżki), tekst 200% na 360 dp, semantyka (ikona, kafle,
   lista, baner) i **pomiar klatki** (D7). *Obali:* więcej wolnych klatek niż w buildzie odniesienia — warstwy według D7.

### Acceptance → tests (`qa`)
| AC | Test (happy path) |
|---|---|
| AC-1 | widget: ikona `link_outlined` z `tooltip` „Połącz dwie osoby”, gdy „ja” jest (bez „ja” — nie ma, D3) → okno: „Od” — „Ja” z imieniem, „Do” — „Wybierz osobę”; „Do” → „Do kogo?” bez osoby z „Od”, wyszukiwanie „wand” → Wanda; wybór zamyka okno; „Od” → wybór Piotra → okno z Piotrem w „Od”; „Anuluj” i wstecz zamykają okno bez zmian |
| AC-2 | `tree_layout`: trasa kroku para / rodzic–dziecko / rodzeństwo leży na punktach `linesAt`; `also` dokłada osobę spoza poziomu 4. widget: Ja → Wanda — Wanda w środku, poziom 3, osoby ścieżki w pełnym kryciu, reszta 30% w jednej warstwie; na sztucznym zegarze linia dochodzi do kolejnych osób co 0,7 s i daje im pierścień; `disableAnimations` → cała ścieżka od razu; ścieżka szersza niż ekran (Ja → Zdzisław) → skala poniżej 0,4, wszystkie osoby ścieżki w kadrze, po końcu 0,4; suwak na 1950 → po wyborze „dziś”, ▶ stoi (Y1) |
| AC-3 | widget: baner po dojściu linii, „Babcia mojej żony”, po 4 s go nie ma; kanał udawany z 10 000 ms → po 4 s jest, po 10 s nie ma; „Od” = Piotr, „Do” = Zofia (ur. 2012) → „Piotr Przykładowy → Zofia Wymyślona” / „Wnuczka”; ogłoszenie dla czytnika; dotknięcie drzewa i wstecz kończą podświetlenie i chowają baner, przeciąganie nie; `kinship_names`: nazwy bez zaimka dla przykładów z [[drzewo]] *AC → element* |
| AC-4 | widget: Teofil → baner „Te osoby nie łączą się — w drzewie brakuje rodziny między nimi.”; środek, poziom i rok bez zmian |
| Tekst 200% | 360 dp: okno — kafle jeden pod drugim, „Przykładowa” bez łamania w słowie; baner bez ucięcia; `meetsGuideline` (`androidTapTargetGuideline`, `labeledTapTargetGuideline`, `textContrastGuideline`) na oknie, liście i drzewie z banerem (retro 3, R2) |
| Regresja | dotknięcie osoby bez podświetlenia stawia ją w środku (US-009 AC-2); pigułka poziomu przy zwykłym oddalaniu; tryb prezentacji bez ikony „Połącz dwie osoby”; sterowanie w trybie dalej z czasem dla sterowania (ISSUE-038 AC-6); test wymyślonej rodziny — 107 osób (D4) |

### Manual verification — agent na emulatorze (`Grobing_Restore`, build profile; przed stopem #2, ze zrzutami)
1. Ikona → okno → „Do” → „wand” → Wanda: Wanda w środku, poziom 3, linia Ja → Kasia → Piotr → Wanda, baner „Babcia mojej żony”, karta Wandy (AC-1–AC-3).
2. „Od” → Piotr, „Do” → Zofia (ur. 2012): baner w dwóch liniach (O2).
3. „Do” → Teofil: baner „Te osoby nie łączą się…”, drzewo bez zmian (AC-4).
4. „Do” → Zdzisław („Stryj mojej mamy”): cała ścieżka w kadrze (F2); dotknięcie → skala 0,4.
5. Suwak na 1950 → ścieżka → „dziś” (Y1); ▶ w trakcie podświetlenia kończy podświetlenie.
6. „Usuń animacje” → cała ścieżka od razu; ustawienie z powrotem.
7. Tekst 200% na 360 dp: okno, lista, baner, ścieżka; semantyka przez `uiautomator dump` (ikona, kafle, lista, baner).
8. „Czas na działanie” 10 s przez adb (sposób z ISSUE-038, krok 0) → baner ok. 10 s; ustawienie z powrotem.
9. `FRAME_LOG`: ścieżka „4 +” i przestawienie środka, naprzemiennie z buildem odniesienia (D7).

### Manual verification — autor: odczucie (najwyżej 3)
1. **Emulator:** dotknij ikony, w „Do” wybierz Wandę — czy linia (0,7 s na krok) i baner na końcu dobrze opowiadają, kim jest.
2. **Emulator:** w „Do” wybierz Zdzisława — czy pomniejszone drzewo z całą ścieżką jest czytelne, czy wolałbyś widok jadący za linią (F1).
3. **Emulator:** zmień „Od” na Piotra, a „Do” na Zofię (ur. 2012) — czy baner w dwóch liniach jasno mówi, kto kim jest dla kogo.

### Out of Scope (plan)
- Ścieżka w trybie prezentacji i na telewizorze → [[2026-10-14-opowiesc-rodziny-i-wieniec]] (D49).
- Zapamiętane ostatnie „Od” w oknie (D49 → *Obali*).
- Odmiana imion — tylko przy wyborze O3; wtedy osobny zakres z tabelą odmiany i testami.
- Tabliczka imienia zasłaniająca ślad dalszej rodziny (MINOR z [[ISSUE-035-tree-names-shrink-my-voice]]) — osobna mała pozycja; dołączenie tylko na prośbę autora na tym stopie.
- Kontrola cykli w rodzinie — `KinGraph.path` idzie wszerz i się nie zawiesza, ale cyklu nie zgłasza.
- Zdanie ścieżki i „Odtwórz jeszcze raz” (D26).

### Risks
- **`tree_screen.dart` (ok. 1940 linii):** nowy stan ekranu obok prezentacji, czasu i przesyłania — łatwo o wejście, które nie kończy podświetlenia. Lista końców z D2 to lista testów.
- **F2 poniżej `treeMinScale`:** `InteractiveViewer` może poprawić skalę przy pierwszym geście, a `_onView` przeliczyć poziom w trakcie — krok 0 (a).
- **Imię na skraju przy 200%** ([[drzewo]] D46): kadr liczy miejsca osób, a imię rośnie o 1/skala — może wyjść poza ekran; `dev` mierzy i w razie potrzeby liczy kadr z szerokością imion
  ścieżki.
- **Płynność:** wyszarzenie i linia rosnąca co klatkę na poziomie 4 — D7.

## Dev report
> `dev`, 2026-10-14. Flutter 3.41.1 (przypięta). `flutter analyze` czyste, `dart format` bez zmian. Testy istniejące (`test/app/tree`, `test/dev`, `kinship_names_test`): 64
> zielone, 2 czerwone — oba w `fictional_family_test.dart` i oba zapowiedziane w D4 (107 osób zamiast 106). Bez nowej zależności, sieci i uprawnień; schemat bez zmian.

### Krok 0
- **(a) F2 poniżej `treeMinScale`** — ze źródła `InteractiveViewer` (Flutter 3.41.1, `interactive_viewer.dart`): `_matrixScale` przycina skalę do `[minScale, maxScale]` tylko w geście
  skalowania; przesuwanie skali nie dotyka, a wartość ustawiona w `TransformationController` nie jest poprawiana. Kadr 0,15–0,4 trzyma się więc przez całe podświetlenie, a szczypanie
  podciągnęłoby skalę do 0,4 — ale ono i tak kończy podświetlenie (D49), po którym widok wraca do 0,4 (D46). Osobne przekształcenie niepotrzebne. Na emulatorze: Ja → Zdzisław w skali ok.
  0,39 (zrzut `23`), po dotknięciu 0,4.
- **(b) Czytnik i baner** — ekran drzewa ogłasza już pigułkę poziomu jako `Semantics(liveRegion: true)`; baner robi to samo (*Deviations* 1). W `uiautomator dump` baner jest
  węzłem z tekstem, a osoby wyszarzone znikają z drzewa semantyki (D6): przy Ja → Wanda czytnik widzi 4 osoby ścieżki i baner, po końcu — znowu wszystkich. Mowy TalkBack agent nie
  słyszy → *Not checked live*.

### Files (`{code}`)
| Plik | Co |
|---|---|
| `lib/app/tree/tree_path.dart` (nowy) | `TreePath`, `pathLevel` (najniższy poziom z całą ścieżką, „4 +”), `levelScales`, `pathBannerText` (G2 od „ja”, O2 od kogoś innego, element 10), `PathLinePainter` (akcent, 3 dp na ekranie przy każdej skali, krok po kroku), `PathBanner` z pomiarem wysokości |
| `lib/app/tree/connect_dialog.dart` (nowy) | okno 7: kafle obok siebie, od 150% jeden pod drugim; pusty kafel z przerywanym okręgiem; „Od” od „Ja” przy każdym otwarciu; wybór „Do” zamyka okno z parą |
| `lib/app/people/person_choice_screen.dart` (nowy) | lista „Od kogo?” / „Do kogo?” — `PeopleSearchField`, `peopleListItems`, `PersonListCard`; bez osoby z drugiego kafla; zwraca id |
| `lib/app/tree/tree_layout.dart` | `layoutTree(…, also:)`; `pathRoute` — trasa kroku po liniach rodziny z tych samych pasów co `linesAt` (`_lines` oddaje pas każdej rodziny) |
| `lib/app/tree/tree_screen.dart` | ikona `link_outlined` (tylko z „ja” — D3); `_connect`, `_showPath` („Do” w środek, poziom, kadr F2, Y1), `_runPath` (0,7 s na krok, przy „Usuń animacje” od razu), baner (4 s albo czas z kanału), `_endPath` (D49; skala < 0,4 → 0,4); wyszarzenie 30% w grupach (osoby, linie), osoby wyszarzone poza semantyką; pierścień `lit` na osobach, do których doszła linia; pierwszeństwo imion ścieżki; `_onView` nie zmienia poziomu w podświetleniu |
| `lib/app/person/kinship_names.dart` | `kinshipName(…, mine: false)` — te same odcinki bez „mój / moja / mojej / mojego” |
| `lib/app/external_link.dart` · `android/…/ExternalLinks.kt` | `recommendedTimeout(time, controls: false)` → `FLAG_CONTENT_ICONS \| FLAG_CONTENT_TEXT` (D5); tryb prezentacji bez zmian |
| `lib/dev/fictional_family.dart` | Teofil Przykładowski, 1910–1975, bez rodziców i związków (D4) |

### Found on the emulator (poprawione przed `qa`)
- **(a) Kadr za wysoko po wyborze z klawiaturą na ekranie.** Wybór „Do” zaraz po wpisaniu w wyszukiwarkę: klawiatura jeszcze się chowała, obszar drzewa był mniejszy, a animacja widoku
  (0,45 s) jechała do celu zmierzonego dla małego obszaru — ścieżka u góry, pół ekranu pustego pod nią (zrzut `12`, ten sam wybór bez klawiatury — zrzut `16`). Poprawka: nowy rozmiar w
  trakcie ruchu przestawia cel animacji (`_viewMove.end`), a kadr ścieżki to nowe „ustawienie w środku” (`_touched = false`), więc kolejna zmiana rozmiaru kadruje od nowa. Po poprawce —
  zrzut `17`.
- **(b) Baner przy 200% zasłaniał górę ścieżki.** Pomiar wysokości baneru (`TextPainter`) nie znał wysokości wiersza z motywu (Material 3: 1,43) i zaniżał baner o ok. 13 dp. Poprawka:
  style baneru z jawną wysokością wiersza 1,3 — pomiar i rysunek liczą tak samo (zrzuty `36` → `38`).

### Measurements (emulator `Grobing_Restore`, build profile, `FRAME_LOG`; naprzemiennie z buildem ISSUE-038 z emulatora — D7)
| Przebieg | Klatki | Wolne (> 16,7 ms) | Raster — mediana · p90 |
|---|---|---|---|
| ISSUE-038 — przestawienie środka (dotknięcie Ewy) | 30 | 56,7% | 17,1 · 29,9 ms |
| ISSUE-039 — przestawienie środka | 27 | 51,9% | 18,7 · 24,1 ms |
| ISSUE-039 — ścieżka Ja → Ignacy Zmyślicki (5 kroków, ok. 4,4 s), runda 1 · 2 | 217 · 225 | 31,8% · 24,0% | 14,8 · 22,8 / 14,9 · 21,1 ms |

Dwa przebiegi bez klatek (dotknięcie przed gotowym drzewem) — odrzucone. **Emulator rysuje dziś wolniej niż przy ISSUE-033** (przestawienie środka tam 2–8% wolnych klatek, tu 52–57% w obu
buildach), host obciążony 9%. Nowy build nie jest gorszy od odniesienia, a ścieżka — wyszarzenie, linia rosnąca co klatkę, poziom 4 — wypada lżej niż samo przestawienie środka. Próg
D7 („nie więcej niż w buildzie odniesienia”) spełniony; wartość bezwzględna — w szumie emulatora, płynność na telefonie → [[ISSUE-032-mvp-install]].

**„Czas na działanie” (D5, D43):** `accessibility_non_interactive_ui_timeout_ms = 10000` → baner jest po ok. 6 s, po ok. 11 s go nie ma; sam klucz `interactive` → baner znika po 4 s (flaga
treści czyta klucz treści, jak Snackbar). Ustawienie z ułatwień dostępu zapisuje oba klucze naraz — AOSP `AccessibilityTimeoutController.onRadioButtonClicked`
([źródło](https://github.com/aosp-mirror/platform_packages_apps_settings/blob/main/src/com/android/settings/accessibility/AccessibilityTimeoutController.java)): *„save value to both
content and control timeout setting”*. Ustawienia emulatora usunięte po pomiarze.

### Deviations
1. **Ogłoszenie baneru przez `liveRegion`, a nie `SemanticsService.announce`** (plan D5): ten sam wzorzec co pigułka poziomu na tym ekranie — węzeł z tekstem, czytnik czyta zmianę bez
   fokusu (SC 4.1.3). Jedna droga na ekranie zamiast dwóch.
2. **Kadr na poziomie 1 w skali 1,3, nie do 2,0** (`levelScales`): krótka ścieżka (np. Ja → córka) nie jest przybliżana ponad próg poziomu 1 — jak w makiecie. Specyfikacja mówi „w skali
   swojego poziomu” (1,3–2,0).
3. **Zmiana danych w trakcie podświetlenia kończy je** (`_onData`): osoby ścieżki mogły zniknąć albo zmienić rodzinę. D49 tego wejścia nie wymienia.
4. **Wysokość wiersza baneru 1,3** zamiast domyślnej 1,43 z motywu (*Found* b) — baner o kilka dp niższy niż w makiecie przy tekście 100%.

### Emulator pass (AC, *States*, zrzuty w katalogu sesji `0558e715-…\scratchpad\emu\shots\`, same wymyślone osoby)
| Co | Wynik | Zrzut / dump |
|---|---|---|
| Ikona w pasku (A1), 48 dp, `clickable`, opis „Połącz dwie osoby” | ✓ | `07` |
| AC-1 — okno: „Od” — Ja (Mateusz Wymyślony), „Do” — „Wybierz osobę”; „Anuluj”; kafle 134 × 133 dp | ✓ | `08` |
| AC-1 — „Do kogo?” bez osoby z „Od”; „wand” → Wanda; wybór zamyka okno | ✓ | `09`, `10` |
| AC-1 — „Od” → „Od kogo?” → Piotr → okno z Piotrem w „Od” | ✓ | `19` |
| AC-2 — Ja → Wanda: Wanda w środku, poziom 3, linia przez Kasię i Piotra po liniach rodziny, reszta 30%, pierścienie po kolei | ✓ | `11`, `17` |
| AC-3 — baner „Babcia mojej żony” po dojściu linii, po ok. 4 s go nie ma, ścieżka zostaje; karta „Babcia mojej żony” | ✓ | `12`, `13` |
| O2 — Piotr → Zofia (ur. 2012): „Piotr Przykładowy → Zofia Wymyślona” / „Wnuczka”, poziom 2 | ✓ | `21` |
| AC-4 — Teofil: baner „Te osoby nie łączą się…”, drzewo bez zmian | ✓ | `22` |
| F2 — Ja → Zdzisław: cała ścieżka w kadrze w skali ok. 0,39 | ✓ | `23` |
| Y1 — suwak na 1921 → ścieżka → „dziś” | ✓ | dump `27`, `28` |
| „Usuń animacje” — cała ścieżka i baner od razu | ✓ | `29` |
| Koniec: dotknięcie drzewa · wstecz (zostaje zakładka Drzewo) · ▶ — wszyscy wracają do semantyki | ✓ | dump `14`, `40`, `43` |
| Tekst 200% na 360 dp: okno (kafle jeden pod drugim), O2 w czterech liniach, kadr pod banerem | ✓ (po *Found* b) | `31`, `38` |
| Semantyka: ikona, kafle, karty listy `clickable`; osoby wyszarzone poza drzewem semantyki | ✓ | dumpy `07`, `08`, `09`, `12` |
| Szczypanie w trakcie podświetlenia | — adb nie ma dotyku dwoma palcami → test widżetu `qa` | — |
| Bez „ja” ikony nie ma (D3) | — stanu nie da się ustawić bez zmiany danych → test widżetu `qa` | — |

**Emulator po przejściu:** `Grobing_Restore` — build profile ISSUE-039 (`FRAME_LOG`), dane aplikacji wyczyszczone (`pm clear`) i wymyślona rodzina dodana od nowa (107 osób z Teofilem); gęstość,
tekst, animacje i „Czas na działanie” z powrotem domyślne. Build odniesienia ISSUE-038 i nowy APK — `0558e715-…\scratchpad\emu\base\`.

### Found, poza pozycją
- **Rodzeństwo przyrodnie w słowniku** ([[ISSUE-025-gender-kinship-together-since]] D2): Zdzisław (syn prababci z drugiego związku, przyrodni brat dziadka) to „Syn mojej prababci” — w karcie
  tak samo. `KinGraph` łączy rodzeństwem tylko dzieci tej samej rodziny, więc ścieżka idzie przez matkę; makieta mówiła „Stryj mojej mamy”. Kandydat na małą pozycję (nazwa „przyrodni”).
- Przy tekście 200% przyciski + / − nachodzą na imiona przy prawej krawędzi drzewa (sprzed tej pozycji).

### Dla `qa` — testy, które zmieniają oczekiwania
- `test/dev/fictional_family_test.dart`: 106 → 107 osób, zmarli 31 → 32, bez rodziców 39 → 40 (D4) — dwa czerwone testy dziś.
- Kanał `recommendedTimeout` dostaje dodatkowy argument `controls` (D5) — testy udające kanał w `tree_screen_test` i `tree_presentation_test` przechodzą bez zmian.

### Found by `qa` and the `ui` review (poprawione przed stopem #2)
- **(c) Baner bez własnego węzła semantyki** (test `qa`): `Semantics(liveRegion: true)` bez `container` oddawał flagę węzłowi wyżej, a nie tekstowi baneru → `container: true`.
- **(d) MAJOR z przeglądu `ui` — kadr F2 nie liczył imion:** poniżej skali 1 imię nie maleje (I2), więc na 200% imię skrajnej osoby wyszłoby poza ekran. Kadr liczy teraz imiona ścieżki
  na ekranie (szerokość i wysokość) obok miejsc osób; ścieżka, która weszłaby pod + / −, kadruje się obok nich (`_pathFramed`, `_pathFrame`, `_underZoomButtons`). Na emulatorze przy
  200% na 360 dp Ja → Zdzisław: imiona ścieżki całe, „Zdzisław” ok. 32 dp od krawędzi, nic pod + / − (zrzut `50`).
- **(e) MINOR z przeglądu:** podpowiedź czytnika w trakcie podświetlenia „zakończ ścieżkę” (dotknięcie tylko kończy, D49) · baner O2 dla czytnika „Od: Piotr Przykładowy, do: Zofia Wymyślona —
  Wnuczka” (strzałka nie jest słowem) · twarda spacja w „w drzewie” ([[style-b]] reguła 6) · zmiana danych w trakcie podświetlenia kończy je jak `_endPath` — poziom ze skali co najmniej
  0,4 i widok na 0,4 (D46).

## Verification
> `qa`, 2026-10-14. Rytuał WZ-024: `dart format` — 199 plików bez zmian · `flutter analyze` — czyste · `flutter test --timeout 120s` — **773 zielone** (przed pozycją 754).

### Tests (`{code}/test/`)
| Plik | Co sprawdza |
|---|---|
| `test/app/tree/tree_connect_test.dart` (nowy, 15) | AC-1 okno: „Od: Mateusz Wymyślony”, „Do: wybierz osobę”, „Anuluj” i wstecz bez zmian, lista bez osoby z „Od”, „wand” → Wanda, wybór zamyka okno; „Od” → Piotr; AC-2/AC-3 Ja → Wanda: karta „ur. 1934 · Babcia mojej żony”, czytnik widzi 4 osoby ścieżki z podpowiedzią „zakończ ścieżkę”, linia rośnie o 1/3 co 0,7 s, baner dopiero po dojściu linii, węzeł z flagą „live region”, kadr pod banerem, po 4 s baneru nie ma, a ścieżka zostaje; koniec (D49): dotknięcie pustego miejsca, osoby spoza ścieżki (tylko kończy, Wanda zostaje), wstecz (zostaje drzewo), ▶, +, dwa palce — przeciąganie nie kończy; AC-4 Teofil: baner elementu 10, drzewo bez zmian; O2 Piotr → Zofia: dwie linie i etykieta dla czytnika; F2 Ja → Zdzisław: skala < 0,4, po końcu 0,4; imiona ścieżki całe 24 dp od krawędzi i poza + / −; Y1: rok 1950 → „dziś”; „Usuń animacje”: cała ścieżka i baner od razu; „Czas na działanie” 10 s przez kanał udawany, wywołanie z `controls: false`; D3: bez „ja” nie ma ikony; tekst 200%: kafle jeden pod drugim, pomiar wysokości baneru = rysunek; tryb prezentacji: przesyłanie kończy podświetlenie, w trybie nie ma ikony. `meetsGuideline` (`androidTapTargetGuideline`, `labeledTapTargetGuideline`, `textContrastGuideline`) i „każdy przycisk ma akcję dotknięcia” (retro 3, R2) na oknie, liście i drzewie ze ścieżką |
| `test/app/tree/tree_layout_test.dart` (+3) | `pathLevel`: Ja → Wanda od Wandy — poziom 3; „4 +”: 9 ze 105 ścieżek od „Ja” — **ta sama liczba co pomiar makiety** — każda w całości w układzie z `also`; trasa kroku: bez skosów, para pozioma, rodzic–dziecko przez pas, który drzewo rysuje |
| `test/app/person/kinship_names_test.dart` (+1) | `mine: false`: „Babcia żony”, „Siostra cioteczna babci żony”, „Ciotka (siostra taty)”, od dziadka do „ja” — „Wnuk” |
| `test/dev/fictional_family_test.dart` | 107 osób, 32 zmarłych, 40 bez rodziców; Teofil jedyny bez rodziców i związków; rodzina od „Ja” dalej 106 |

**W testach, nie w kodzie:** w czcionce testowej (każda litera to kwadrat) przy 200% pasek zakładek się przepełnia — przepuszczony jawnie, jak w AC-7 ISSUE-033; baner jest tam wyższy niż pół
obszaru drzewa, więc kadr celowo nie robi mu miejsca (próg z D46) — test 200% sprawdza sam pomiar baneru, a brak nakładania — test przy 100%. Przy 200% w skali 0,34 cel dotyku osoby jest
poniżej 48 dp — wyjątek D17, a dotknięcie i tak tylko kończy podświetlenie (`labeledTapTargetGuideline` zostaje).

### Review `ui` (subagent, przed stopem #2)
0 BLOCKER · 1 MAJOR (*Found* d) — poprawiony · 5 MINOR (*Found* e i + / −) — poprawione. Odstępstwa `dev` 1–4 przyjęte; **dwa przyjęte w przeglądzie, których *Dev report* nie wymieniał:**
(5) w trakcie podświetlenia przy 30% są wszystkie linie rodziny i ślady, także osób ze ścieżki — jedna warstwa (D7), drogę niesie linia w akcencie (4,81:1 na przyciemnionej linii); (6) znak „Ja”
w kaflu „Od” ma obrys w akcencie jak na liście [[osoby]], nie jak w drzewie (D14) — w oknie nie ma osoby w środku. Wszystkie sześć → [[drzewo]] v1.17. Pary kontrastu przeliczone z
`theme.dart`; na zrzutach tylko wymyślone osoby. **Spoza pozycji:** linia od pary do dzieci biegnie tuż przy końcu tabliczki długiego imienia (pasuje do małej pozycji o tabliczkach z
ISSUE-035); „Syn mojej prababci” zamiast „Stryj mojej mamy” (*Found, poza pozycją* — rodzeństwo przyrodnie).

**Obserwacja z emulatora po poprawkach (200%, Ja → Zdzisław, zrzut `50`):** imiona Henryka i Genowefy chowają się, bo przy skali ok. 0,17 nachodzą na imiona innych osób ścieżki (stan
„połącz — ścieżka, tekst 200%” to przewiduje), a w tym czasie widać wyszarzone imię „Feliks”, które na nic nie nachodzi. Do oceny autora — nie zmieniane po cichu.

### Family data
Próba strażnika treści na liście paczki (`echo git add -- …` w obu repo — 13 plików kodu i testów, 5 plików vaulta): przechodzi. Nazwiska tylko z rdzeni Wymyśl-, Zmyśl-, Przykład-, Testow-;
nowa osoba Teofil Przykładowski. Bez baz, kopii, eksportów i zdjęć w zmianach; zrzuty i makieta poza repo (`0558e715-…\scratchpad\`).

### Not checked live
- Mowa TalkBack przy banerze (region na żywo) — węzeł jest w drzewie semantyki, odsłuchu nie było.
- Płynność ścieżki na telefonie — emulator dziś w szumie (przestawienie środka 52–57% wolnych klatek w obu buildach).

### Stop #2 (2026-10-14) — autor: *„Pomiń”*
Jedna odpowiedź na wszystkie trzy kroki odczucia: zapisane jako „pomiń”, nie blokuje (`DEFINITION_OF_DONE.md`, retro 3 R8). Na emulatorze nie było śladu kroków autora do sprawdzenia —
przejście agenta i testy są wyżej.

### For ISSUE-032 → Hand checks (po jednym w linii)
- „Połącz dwie osoby” Ja → Wanda: czy linia (0,7 s na krok) i baner na końcu dobrze opowiadają, kim ktoś jest (stop #2 ISSUE-039, krok 1 — „pomiń”).
- Długa ścieżka (np. Ja → Zdzisław): czy pomniejszone drzewo z całą ścieżką (F2) jest czytelne, czy lepszy byłby widok jadący za linią (F1) (stop #2 ISSUE-039, krok 2 — „pomiń”).
- „Od” inne niż Ty (Piotr → Zofia): czy baner w dwóch liniach jasno mówi, kto kim jest dla kogo (O2; stop #2 ISSUE-039, krok 3 — „pomiń”).
- TalkBack czyta baner „Połącz dwie osoby” raz, gdy się pokaże (region na żywo; ISSUE-039 — nieprzetestowane na żywo).
- Płynność ścieżki „Połącz dwie osoby” na telefonie — linia, wyszarzenie, poziom 4 (ISSUE-039 — emulator w szumie).

### Verdict
**APPROVED** (self-check, z uwagami). Każde AC ma test happy-path i przejście na emulatorze ze zrzutami; przegląd `ui` — 0 BLOCKER, MAJOR i MINOR poprawione przed stopem; warstwa danych
bez zmian (tylko odczyt, bez migracji i odtworzenia kopii); dane rodziny — próba strażnika przechodzi. **Uwagi:** stop #2 „pomiń” we wszystkich krokach; odsłuch TalkBack i płynność na
telefonie nieprzetestowane na żywo; przy 200% imiona dwóch osób długiej ścieżki chowają się, a wyszarzone imię spoza ścieżki zostaje (obserwacja wyżej); „Syn mojej prababci” zamiast
nazwy z „przyrodni” — poza pozycją. **Szukałem i nie znalazłem:** wejścia, które nie kończy podświetlenia (lista D49 — testy); osoby ścieżki poza kadrem przy 100% (test F2 — imiona całe 24 dp
od krawędzi); ogłoszenia baneru poza jego węzłem (test „live region”); danych rodziny w zmianach.

### Package for `docs` (pliki, które ta pozycja zapisała)
- **`grobing-code`:** `android/app/src/main/kotlin/com/grobing/app/ExternalLinks.kt` · `lib/app/external_link.dart` · `lib/app/person/kinship_names.dart` · `lib/app/tree/tree_layout.dart` ·
  `lib/app/tree/tree_screen.dart` · `lib/app/tree/tree_path.dart` (nowy) · `lib/app/tree/connect_dialog.dart` (nowy) · `lib/app/people/person_choice_screen.dart` (nowy) ·
  `lib/dev/fictional_family.dart` · `test/app/tree/tree_connect_test.dart` (nowy) · `test/app/tree/tree_layout_test.dart` · `test/app/person/kinship_names_test.dart` ·
  `test/dev/fictional_family_test.dart`.
- **`grobing-vault`:** `backlog/issues/ISSUE-039-connect-two-people.md` (nowy) · `05_DESIGN/drzewo.md` · `03_REQUIREMENTS/user-stories/US-011-polacz-dwie-osoby.md` ·
  `00_START_HERE/CURRENT_STATE.md` · `00_START_HERE/TRACEABILITY.md` — oraz to, co dopisze zamknięcie `docs` (np. `backlog/issues/ISSUE-032-mvp-install.md`).
- **`grobing-agents`:** bez zmian.
