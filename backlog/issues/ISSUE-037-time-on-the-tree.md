---
title: "ISSUE-037 — Time on the tree: a year slider with ▶ / ❚❚ in the tree card — people appear when born, couples join with „razem” and then with the wedding, the dead get a candle; uncertain dates and missing dates on the slider"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-010-czas-na-drzewie]]"
depends-on: "[[ISSUE-033-tree-from-a-person]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-14
verdict-reviewer: self-check
source: "rozpisanie US-010 (`docs` w auto-flow po `pm`, autor: „ok”, 2026-10-14) · US-010 AC-1–AC-3 · [[drzewo]] v1.11 (element 6, D4, D23 *Obali*, *States* „rok w przeszłości”, *AC → element* M10) · [[FR-004-data-z-dopiskiem]] · [[rodzina]] v1.4 (dwa tryby związku) · [[SPIKE-004-mvp-flow-prototype]] D20"
created: 2026-10-14
updated: 2026-10-14
---

# ISSUE-037 — Czas na drzewie

> Z rozpisania [[US-010-czas-na-drzewie]] (`docs` w auto-flow, 2026-10-14, **przed** `ui` — żeby plan miał plik; lekcja z
> [[ISSUE-033-tree-from-a-person]], `CURRENT_STATE.md` → *Do retro*). **Jedna pozycja na całą US** — trzy AC na jednym elemencie
> ([[drzewo]] element 6). Podział zaproponował łańcuch, nie autor, więc na stopie #1 autor może go zmienić.
> **Pozycja zmienia ekran → `ui` przed `planning`.**

## What to build
1. **Wymyślona rodzina z datami niepewnymi** — **pierwszy krok pozycji**. Dziś `lib/dev/fictional_family.dart` ma same daty dokładne
   (`DateQualifier.exact`), więc ⚠️ OPEN z US-010 nie dałoby się sprawdzić na emulatorze. Dołożyć do istniejących wymyślonych osób (bez
   zmiany kształtu rodziny ze SPIKE-002: 106 osób, 38 związków) daty „ok.”, „przed”, „po”, „między”, kilka osób bez daty urodzenia i co
   najmniej jednego zmarłego bez daty zgonu (zmarły = zgon albo pochówek, z datą albo bez — [[drzewo]] D22). Liczby — plan. Nazwiska tylko
   z wymyślonych rdzeni (`family-data.md`, retro 3 R7).
2. **Suwak czasu w karcie drzewa** ([[drzewo]] element 6, szkic): ▶ / ❚❚ 36 dp w akcencie, „1880”, suwak w akcencie, rok w akcencie, „dziś”
   na końcu. Przeciągnięcie ustawia rok Y.
3. **Drzewo w roku Y** (AC-1, AC-2; [[drzewo]] *States* „rok w przeszłości”): osoba urodzona po Y znika, a jej miejsce zostaje (układ się
   nie przelicza); zmarły do Y ma znicz; para — bez linii przed początkiem związku, przerywana „razem” od początku, ciągła od ślubu.
4. **Odtwarzanie** (AC-3): ▶ biegnie od 1880 do dziś w ok. 7 s, ❚❚ zatrzymuje; przy ograniczeniu animacji w systemie suwak przeskakuje
   bez animacji (SC 2.3.3, jak [[drzewo]] D5).
5. **Daty niepewne i brak daty na suwaku** ([[FR-004-data-z-dopiskiem]] → *Rules*: „Suwak czasu musi umieć ustawić zdarzenie z datą
   niepewną”) — według decyzji z *Open for `ui`* 1.
6. **Tekst 200% na 360 dp, czytnik, cel dotyku** — karta z suwakiem rośnie z tekstem ([[drzewo]] D20); suwak i ▶ z opisem dla czytnika
   (rok, „odtwórz” / „zatrzymaj”); testy `meetsGuideline` (retro 3, R2).
7. **Płynność odtwarzania:** 7 s na ok. 140 lat to zmiana roku co ok. 50 ms przy 106 osobach — pomiar klatki na buildzie profile
   (`FRAME_LOG`, retro 3 R3), jak przy [[ISSUE-033-tree-from-a-person]]. Zmiana roku nie przelicza układu, tylko widoczność osób, linii i zniczy.

## Acceptance Criteria
- [ ] **US-010 AC-1 — rok na suwaku.** *Given* suwak na roku Y *Then* osoba urodzona po Y znika (jej miejsce zostaje, drzewo nie skacze), a
      osoba zmarła do Y ma znicz ([[drzewo]] element 6).
- [ ] **US-010 AC-2 — związki w czasie.** *Given* para „razem” od roku A i ze ślubem w roku B *Then* do A nie ma linii, od A jest linia
      „razem” (przerywana), od B — ciągła ([[rodzina]] v1.4, [[drzewo]] D4).
- [ ] **US-010 AC-3 — odtwarzanie.** *When* dotykam ▶ *Then* czas biegnie od 1880 do dziś w ok. 7 s; ❚❚ zatrzymuje; przy ograniczeniu
      animacji w systemie suwak przeskakuje bez animacji (SC 2.3.3).
- [ ] **Data niepewna i brak daty** — zachowanie według decyzji z *Open for `ui`* 1, sprawdzone na wymyślonych osobach z kroku 1.
- [ ] **Tekst 200% na 360 dp** — suwak, rok, ▶ i „dziś” nie są ucięte ani nie nachodzą na siebie; cele dotyku przechodzą `meetsGuideline`.

## Open for `ui` (przed planem; kandydaci na makiecie albo emulatorze — retro 2, R6)
1. **⚠️ OPEN (z US-010) — data z dopiskiem i brak daty na suwaku:** kiedy pojawia się osoba „ok. 1890”, „przed 1920”, „po 1900”, „między
   1885 a 1890”; co z osobą bez daty urodzenia (zawsze widoczna? widoczna inaczej?); kiedy znicz ma zmarły bez daty zgonu. To samo dla dat
   związku i ślubu.
2. **Osoba w środku przed swoimi narodzinami** — „Ja” (ur. 1983 w wymyślonej rodzinie) w roku 1900: co pokazuje pierścień, karta i czytnik.
3. **Początek suwaka 1880 a osoby urodzone wcześniej** — wymyślona rodzina zaczyna się w 1868 (SPIKE-002 → *Rekomendacja*); czy suwak
   zaczyna się od 1880 zawsze, czy od najstarszej daty.
4. **Koniec związku** (rozwód, wdowieństwo — model ma datę końca rodziny; w wymyślonej rodzinie 3 osoby w dwóch związkach): czy linia pary
   po końcu się zmienia. AC-2 tego nie mówi.
5. **Suwak a poziomy (S2) i przestawianie środka** — czy rok zostaje przy zmianie środka i poziomu; czy dotknięcie osoby w czasie ▶
   zatrzymuje odtwarzanie.
6. **Tabliczka imion na tle** — [[drzewo]] D23 *Obali*: „pod węzłami pojawi się tło niejednolite (… pasmo czasu z US-010)”. Czy element 6 to
   zmienia.

## Out of scope
- Drzewo, poziomy, przestawianie środka, karta → [[US-009-drzewo-od-osoby]] (zrobione).
- Suwak w trybie prezentacji (element 11) — nie ma go w US-010 ani w elemencie 6. Jeśli `ui` albo autor go chce, to decyzja na stopie #1, nie
  po cichu w tej pozycji.
- „Połącz dwie osoby” → [[US-011-polacz-dwie-osoby]].
- Kontrola cykli w rodzinie ([[ISSUE-019-family-relations]] → *Manual*) — suwak musi się przy cyklu nie zawiesić, ale go nie zgłasza.

## Notes
- **Dziś w kodzie:** daty to `QualifiedDate` (`DateQualifier`: exact, about, before, after, between; `PartialDate` — rok, opcjonalnie miesiąc i
  dzień) w `lib/data/graves.dart` i `lib/data/database.dart`. Związek ma `together`, `marriage` i `end` (`lib/dev/fictional_data.dart` ma
  już przykłady „ok.” i „przed” — poza rodziną drzewa). Odczyt drzewa: `lib/data/family_tree.dart`; układ: `lib/app/tree/tree_layout.dart`
  ([[ISSUE-033-tree-from-a-person]] → *Implementation plan*).
- **Emulatory** (`CURRENT_STATE.md` → *In progress*): `Grobing_Restore` — build profile z wymyśloną rodziną i `FRAME_LOG`; `Medium_Phone` —
  release v12 z danymi testowymi autora, nietknięty.
- **Makieta** — link jako adres `file:///`, nie ścieżka z `%TEMP%` (`CURRENT_STATE.md` → *Do retro*, ISSUE-034).
- Przy tej pozycji: pozycja z ekranem, więc przegląd `ui` przed stopem #2 i testy `meetsGuideline` (retro 3, R2).

## Implementation plan
> `planning`, 2026-10-14. Specyfikacja (`ui`, przed planem): [[drzewo]] v1.12 — element 6 (cały), element 4 (koniec związku „//”), *Navigation* (rok), *States*
> (rok w przeszłości, osoba w środku przed narodzinami, odtwarzanie, ograniczenie animacji), *AC → element*, *Candidates — ISSUE-037*, D31–D37, *Open* 8;
> [[style-b]] v1.28 bez zmian (przerywany obrys jako znak niepewności dopisze `ui` po decyzji). Makieta: `drzewo-037.html` w katalogu tymczasowym sesji `555909c3-…`
> (sekcje 1–6, self-test `#test=1` i `#playtest=1`, zrzuty `shots-037\`). **Kandydaci tego, co widać** (retro 2, R6): N1–N3, C1–C2, T1–T2, E1–E3 i R1–R2 działają na
> makiecie (przełączniki w sekcjach 1–5), przed rekomendacją. *Open for `ui`* 1–6 z tej pozycji rozstrzyga specyfikacja: 1 → D32, 2 → D33, 3 → D34, 4 → D35, 5 → D37,
> 6 → *Style B rules applied* (D23 bez zmian); doszło R (D36). Wszystko według rekomendacji, do potwierdzenia na stopie #1.

### Prior art (źródła, nie pamięć)
- **Daty niepewne i brakujące:** [[drzewo]] D31 — TimeNets (*Missing Data Estimation*, *Uncertainty*: szacowanie z rodziny, ślub z urodzenia najstarszego dziecka,
  niepewność widoczna na rysunku) i liczby z Gramps (`AVG_GENERATION_GAP = 20`, `MAX_SIB_AGE_DIFF = 20`, `MAX_AGE_PROB_ALIVE = 110`). Okno daty — D32.
- **Koniec związku:** genogram — jedna kreska przez linię pary to separacja, dwie to rozwód (D35, ND CFS QA *Genogram Resource*).
- **Ograniczenie animacji:** WCAG 2.2 SC 2.3.3 (AAA) dotyczy animacji ruchu (D36). We Flutterze `MediaQuery.disableAnimationsOf` — ten sam warunek, którego drzewo
  już używa przy przestawianiu środka (element 4).
- **Z kodu** (ankieta 2026-10-14):
  - `FamilyTreeData` (`lib/data/family_tree.dart`) ma `TreePerson.birth` / `death` (`QualifiedDate`) i `dead` (zgon albo pochówek, D22), a `TreeUnion` — tylko
    `married` i `startKey` („razem”, a bez niego ślub). **Nie czyta** osobnej daty ślubu, końca związku (`EventType.end`) ani daty pochówku (`EventType.burial`).
    Związek bez daty ma `startKey == null` i sortuje się **na koniec** (`_byKey`). U wdowy z dwoma związkami zamieniłoby to ich kolejność i przestawiło drzewo (D3);
  - `TreeGraph` sortuje rodzeństwo po roku urodzenia, osoby bez daty na koniec (`tree_layout.dart`, `_birthYear ?? 99999`);
  - `layoutTree` liczy pozycje **i** linie razem (`_lines`, `_traces`; `TreeLineKind`: `married`, `together`, `parentChild`, `trace*`). Układ przy 106 osobach to do
    15 ms (SPIKE-002 M1), więc **pozycji nie liczymy co rok**: rok zmienia tylko to, kto jest, linie i ślad;
  - węzeł `_TreeNode` (`tree_screen.dart`): `InitialsCircle` z ciągłym obrysem albo `ProfileCircle`, pierścień w akcencie przy osobie w środku, `_CandleBadge` przy
    `person.dead`. Przerywanego okręgu Flutter nie ma (`Border` nie ma kreski) — potrzebny własny `CustomPainter`;
  - wymyślona rodzina (`lib/dev/fictional_family.dart`) ma same daty dokładne (`year()` → `DateQualifier.exact`). `addFictionalFamily` drugi raz nic nie dodaje
    (znacznik partii), więc na `Grobing_Restore` została by stara rodzina bez dat niepewnych (D4);
  - na tej rodzinie stoją `tree_layout_test.dart` (liczby 6 / 20 / 66 / 99, skrzyżowania) i `tree_screen_test.dart`.

### Stop #1 (2026-10-14) — autor: „tak”
Rekomendacja przyjęta w całości: D1 = **N3, C1, T2, E3, R2**, D2 (jedna pozycja), D3 (związek bez daty po najstarszym dziecku), D4 (`pm clear` na `Grobing_Restore`),
D5 (czytnik co 10 lat, krok 0). Decyzje projektowe [[drzewo]] D37 potwierdzone. Specyfikacja → [[drzewo]] *Open* 8 rozstrzygnięte; [[style-b]] — przerywany obrys
jako znak niepewności. Przy zamknięciu `docs` zmienia US-010 AC-3 („od początku suwaka, najpóźniej 1880” — T2).

### Decisions for stop #1 (rekomendacja → „tak” przyjmuje wszystkie)
- **D1 — wygląd czasu: N3, C1, T2, E3, R2** ([[drzewo]] *Candidates — ISSUE-037*, *Open* 8; makieta, sekcje 1–5):
  - **N3** — przerywany obrys „nie wiadomo, czy w tym roku żyje”. N1 — jeden rok z daty; N2 — blada osoba (odrzucona pomiarem: imię poniżej 4,5:1 aż do krycia 60%);
  - **C1** — pusty pierścień w miejscu osoby w środku przed jej narodzinami. C2 — osoba zostaje, wyszarzona;
  - **T2** — suwak od pełnej dekady przed najwcześniejszą datą (najpóźniej 1880), stała prędkość ok. 21 lat/s. T1 — zawsze 1880. **Przy T2 `docs` przy zamknięciu zmienia
    US-010 AC-3:** „od 1880” → „od początku suwaka (najpóźniej 1880)”;
  - **E3** — „//” na linii pary od roku końca związku, **także na „dziś”**, czyli zmienia drzewo z US-009 (decyzja projektowa, nie z AC). E1 — bez zmian; E2 — linia znika;
  - **R2** — przy „Usuń animacje” ▶ skacze dekadami co ok. 1 s. R1 — od razu „dziś”.
  *Obali* każdego — D32–D36 w specyfikacji.
- **D2 — jedna pozycja.** E3 zmienia drzewo także bez suwaka, ale to jedna linia malowania i ten sam odczyt końca związku, którego potrzebuje suwak. Alternatywa: E3
  osobno — wtedy tutaj E1, a koniec związku pomijany jak dziś.
- **D3 — związek bez daty sortuje się po najstarszym wspólnym dziecku** (D31: TimeNets, „ślub ← urodzenie najstarszego dziecka”), a nie na koniec. Ten sam rok rysuje
  linię pary na suwaku. Po co: wymyślona rodzina dostaje trzy związki bez daty (jak w notatkach), a u wdowy z dwoma związkami kolejność by się odwróciła. **Test układu
  (6 / 20 / 66 / 99, skrzyżowania) bez zmian** pokazuje, że nowe daty nie przestawiły drzewa.
- **D4 — `Grobing_Restore`: wyczyszczenie danych aplikacji** (`pm clear com.grobing.app` na buildzie profile) i rodzina dodana od nowa przyciskiem w „Stanie danych”. Są
  tam tylko wymyślone dane, a `addFictionalFamily` nie nadpisuje istniejącej rodziny. `Medium_Phone` z Twoimi danymi testowymi zostaje nietknięty. Alternatywa: przycisk
  „zastąp wymyśloną rodzinę” w debug i profile — więcej kodu dla jednej pozycji.
- **D5 — czytnik: suwak zmienia rok o 10 lat** na gest zwiększania i zmniejszania (element 6). Krok 0 `dev` sprawdza, czy da się to zrobić `semanticFormatterCallback` i
  `Semantics(onIncrease/onDecrease)`; jeśli nie — krok 1 rok i zapis w *Dev report*.

### Scope — files (`{code}`)
| Plik | Zmiana |
|---|---|
| `lib/dev/fictional_family.dart` | **pierwszy krok.** Daty jak w makiecie, te same osoby i rdzenie: Marianna (`a2`) ur. „ok. 1870”; Tadeusz (`td`) ur. „między 1895 a 1900”; Kazimierz (`kz`) ur. „przed 1900”, zm. „po 1960”; Leokadia (`le`) ur. „po 1905”; Stanisław (`f3`) i Lech (`lh`) bez daty urodzenia; Leon (`L`) zm. „ok. 1944”; Władysław (`wl`) — zgon bez daty; związki Antoni–Marianna, Kazimierz–Bronisława, Władysław–Genowefa bez daty (dalej małżeństwa); rozstanie Andrzej–Bożena 1995 już jest. Kształt rodziny bez zmian (106 osób, 38 związków) |
| `lib/data/family_tree.dart` | **tylko odczyt, schemat bez zmian:** `TreePerson.burial` (data pochówku — koniec okna śmierci, D32); `TreeUnion.together`, `.marriage`, `.end` (`QualifiedDate?`); `startKey` związku bez daty = rok najstarszego wspólnego dziecka (D3) |
| `lib/app/tree/tree_time.dart` (nowy) | czysty Dart, bez Fluttera: okno urodzenia i śmierci (D32 — „dokładnie / ok. / między / przed / po / brak” i granice z rodziny), stan osoby w roku Y (nie ma / żyje / niepewne — urodzenie albo śmierć / nie żyje), linia pary w roku Y (brak / razem / ślub, koniec), początek suwaka (D34). Liczony raz na dane, nie co rok |
| `lib/app/tree/tree_layout.dart` | linie i ślad **dla roku, bez liczenia pozycji od nowa** (np. `TreeLayout.linesAt(...)` z tym, czego potrzebuje `_lines`); nowy `TreeLineKind.ended` („//”); ślad tylko od osób, które w roku Y już są (D37) |
| `lib/app/tree/tree_painter.dart` | „//” w kolorze partnerów, 2 dp, ok. 12 × 12 dp przez środek linii pary |
| `lib/app/tree/tree_screen.dart` | rok jako stan widoku (D37: zostaje przy środku, poziomie i wstecz; „dziś” przy wejściu z paska, z „Pokaż w drzewie” i w trybie prezentacji); rząd czasu w karcie (element 6; przy tekście ≥ 150% dwa rzędy); ▶ / ❚❚ z zegarem ok. 21 lat/s i R2 przy `disableAnimations`; węzeł: nie ma (poza dotykiem i czytnikiem), przerywany obrys, pusty pierścień (C1), znicz według roku; przenikanie 150 ms; pigułka poziomu liczy osoby w roku; czytnik według elementu 6 |
| `lib/app/tree/tree_time_bar.dart` (nowy, gdy `tree_screen.dart` za bardzo urośnie) | rząd ▶ · rok początku · suwak · rok |
| przerywany okrąg | `CustomPainter` (kreska 4/3, 2 dp) nad `InitialsCircle` i `ProfileCircle`; w akcencie przy osobie w środku |
| `test/…` | `qa` — niżej |

**Bez nowej zależności, sieci i uprawnień** ([[NFR-005-dane-nie-opuszczaja-telefonu]]). **Warstwa danych:** tylko odczyt, schemat bez zmian, więc bez testu migracji i bez
próbnego odtworzenia z kopii. Fixture w `lib/dev/` jest za `!kReleaseMode` (ISSUE-033 D6).

### Steps for `dev`
0. **Krok 0, przed budową, na emulatorze:** (a) czy czytnik dostaje „Rok, 1923” i krok 10 lat (D5); (b) co Flutter czyta jako `disableAnimations` na Androidzie 16 i
   jak to włączyć przez adb na `Grobing_Restore`. Wynik w *Dev report*.
1. Fixture (`fictional_family.dart`) i odczyt (`family_tree.dart`, D3). Test układu z ISSUE-033 musi dać te same liczby.
2. `tree_time.dart` według D32–D34. Oczekiwane okna z makiety (`#test=1`): `a2` 1865–1875; `td` 1895–1900; `kz` 1882–1900, śmierć 1960–2010; `le` 1905–1930; `f3`
   1890–1920; `lh` 1916–1958; `L` śmierć 1939–1949; `wl` śmierć 1930–2010.
3. Linie i ślad dla roku, „//” (E3).
4. Ekran: rząd czasu, stan roku, węzły, ▶ / ❚❚, R2, tekst 200%, czytnik.
5. **Przejście AC na emulatorze przed `qa`** (retro 3, R3): stany z *States* (rok w przeszłości, przed narodzinami, odtwarzanie, ograniczenie animacji), tekst 200% na
   360 dp, semantyka i **pomiar klatki w trakcie ▶** na buildzie profile (`FRAME_LOG`). Próg jak przy przejściach w ISSUE-033: wolnych klatek ≤ 10%. *Obali:* więcej —
   wtedy linie dla roku z pamięci podręcznej (zmieniają się tylko w latach zdarzeń) i węzły bez przebudowy całego drzewa.

### Acceptance → tests (`qa`)
| AC | Test (happy path) |
|---|---|
| US-010 AC-1 | `tree_time`: osoba ur. 1983 w roku 1950 — „nie ma”, w 1984 — „żyje”; zm. 2010 — w 2010 „nie żyje”. Widget: rok 1950 od „Ja” → 5 z 20 osób na poziomie 2, pusty pierścień (C1), osoby nieurodzone poza drzewem semantyki |
| US-010 AC-2 | rodzice „Ja” (razem 1982, ślub 1985): 1981 — bez linii, 1984 — `together`, 1986 — `married`; związek bez daty — od najstarszego dziecka |
| US-010 AC-3 | ▶ od początku suwaka: na sztucznym zegarze rok rośnie ok. 21 na sekundę, na końcu „dziś” i znów ▶; ❚❚ zatrzymuje; przeciągnięcie zatrzymuje; `disableAnimations` → dekada co ok. 1 s (R2) |
| Data niepewna i brak daty | `tree_time`: okna z kroku 2 (wszystkie przypadki D32); widget: przerywany obrys przy `kz` w 1890, przy `wl` w 1960 bez znicza, w 2011 ze zniczem |
| Koniec związku (E3) | linie dla roku: Andrzej–Bożena w 1990 bez „//”, w 2000 i na „dziś” z „//” |
| Tekst 200% na 360 dp | rząd czasu w dwóch rzędach, nic nie ucięte; `meetsGuideline` (`androidTapTargetGuideline`, `labeledTapTargetGuideline`, `textContrastGuideline`) na ekranie z suwakiem (retro 3, R2) |
| D37 | rok zostaje po dotknięciu osoby; wejście z paska i „Pokaż w drzewie” → „dziś”; pigułka liczy osoby w roku |
| Regresja | test układu z ISSUE-033 bez zmian (D3); drzewo na „dziś” jak dotąd, poza „//” |

### Manual verification — agent na emulatorze (`Grobing_Restore`, build profile; przed stopem #2, ze zrzutami)
1. Rodzice „Ja” w latach 1981, 1984 i 1986: brak linii, przerywana, ciągła (AC-2).
2. „Ja” w roku 1950: pusty pierścień, 5 osób na poziomie 2, karta bez zmian (AC-1, C1).
3. Kazimierz w 1890 i 1970, Władysław w 1960 i 2011, Leon w 1944: przerywany obrys i znicz według okien (N3).
4. Andrzej w 2000 i na „dziś”: „//” (E3).
5. ▶ od początku do „dziś” (czas mierzony), ❚❚, przeciągnięcie i dotknięcie osoby w trakcie; `FRAME_LOG` w trakcie ▶.
6. „Usuń animacje” → ▶ dekadami (R2); po kroku ustawienie z powrotem.
7. Tekst 200% na 360 dp — rząd czasu; czytnik przez `uiautomator dump`: etykiety suwaka, ▶, osoby z przerywanym obrysem i pustego pierścienia.
8. Wejście z paska, „Pokaż w drzewie”, tryb prezentacji → „dziś”; wstecz z widoku osoby → ten sam rok (D37).

### Manual verification — autor: odczucie (najwyżej 3)
1. **Emulator:** na drzewie od „Ja” dotknij ▶ i obejrzyj całą historię — czy tempo i pojawianie się osób mówią, jak zmieniała się rodzina.
2. **Emulator:** postaw w środku Kazimierza i przesuń suwak przez lata 1880–1910 — czy przerywany obrys bez wyjaśnienia mówi „nie wiadomo, czy już żył”.
3. **Emulator:** Andrzej w środku, „dziś” — czy „//” na linii z Bożeną pasuje do drzewa.

### Out of Scope (plan)
- Suwak w trybie prezentacji (element 11) — D37: tryb pokazuje „dziś”.
- Wpisywanie dat z dopiskiem i końca związku — formularze już to mają ([[FR-004-data-z-dopiskiem]], [[rodzina]] A6); tu tylko odczyt.
- Rozróżnienie rozwodu i rozstania („/” i „//”) — model ma jeden koniec związku (D35 → *Nie da*).
- „Połącz dwie osoby” i jego wyszarzenie w przeszłym roku → [[US-011-polacz-dwie-osoby]].
- Płynność na fizycznym telefonie → [[ISSUE-032-mvp-install]] → *Hand checks* (wiersz przy zamknięciu, jeśli krok 1 autora będzie bez śladu na urządzeniu).

### Risks
- **Klatki w trakcie ▶:** rok zmienia się co ok. 48 ms, a każda zmiana to widoczność do 106 węzłów i nowe linie. Pomiar w kroku 5, *Obali* tam.
- **Fixture a testy:** nowe daty mogą zmienić teksty lat w testach karty (`tree_screen_test.dart`) i mini-drzewa. `qa` poprawia oczekiwania, a nie dane — chyba że test
  sprawdza układ: wtedy D3 jest błędne i wraca do planu.

## Dev report
> `dev`, 2026-10-14. Flutter 3.41.1 (przypięty). `flutter analyze` — bez uwag; dotychczasowe testy drzewa i widoku osoby (`test/app/tree`, `test/app/person`) — 47 zielonych,
> w tym test układu z ISSUE-033 (6 / 20 / 66 / 99, skrzyżowania) bez zmian, czyli D3 nie przestawiło drzewa. Nowych testów nie pisałem (`qa`).

### Krok 0
- **(a) Czytnik, krok 10 lat (D5):** `Slider` daje czytnikowi krok jednego podziału albo 10% zakresu (`_semanticActionUnit`, `slider.dart`). Rozwiązanie: własne
  `Semantics(slider: true, label: 'Rok', value, increasedValue, decreasedValue, onIncrease / onDecrease ± 10 lat, excludeSemantics: true)` nad suwakiem; palec dalej
  przeciąga co rok. W `uiautomator dump` suwak to „dziś, Rok” / „1950, Rok”, klikalny, 48 dp wysokości. Samego gestu TalkBack na emulatorze nie sprawdzałem — test semantyki `qa`.
- **(b) „Usuń animacje”:** silnik Fluttera (`io/flutter/view/AccessibilityBridge`) czyta `Settings.Global.TRANSITION_ANIMATION_SCALE`; zero → `disableAnimations`. Na
  emulatorze: `settings put global transition_animation_scale 0` (i `animator_duration_scale`, `window_animation_scale` — jak przełącznik w ułatwieniach dostępu).

### Files (`{code}`)
| Plik | Co |
|---|---|
| `lib/dev/fictional_family.dart` | daty jak w makiecie: `a2` ok. 1870, `td` między 1895 a 1900, `kz` przed 1900 i zm. po 1960, `le` po 1905, `f3` i `lh` bez daty urodzenia, `L` zm. ok. 1944, `wl` zgon bez daty; trzy małżeństwa bez daty (`married: true` bez `marriage`) |
| `lib/data/family_tree.dart` | odczyt pochówku (`TreePerson.burial`), „razem”, ślubu i końca związku (`TreeUnion.together`, `.marriage`, `.ended`, `.end`); `startKey` związku bez daty = najstarsze dziecko (D3). Tylko odczyt, schemat bez zmian |
| `lib/app/tree/tree_time.dart` (nowy) | `TreeTime`: okna urodzenia i śmierci (D32), stan osoby w roku (`InYear`: `notYet`, `maybeBorn`, `alive`, `maybeDead`, `dead`), linia pary w roku (`PairInYear`), początek suwaka (D34). Okna z kodu = okna makiety (`#test=1`) dla wszystkich ośmiu osób — sprawdzone w aplikacji na emulatorze dla `kz`, `wl` i par |
| `lib/app/tree/tree_layout.dart` | `TreeLayout.linesAt(time, year)` — linie i ślad dla roku bez liczenia pozycji; `lines` = „dziś”; `TreeLineKind.ended` („//”, 12 × 12 dp) |
| `lib/app/tree/tree_painter.dart` | „//” w kolorze partnerów; pędzel bierze listę linii; `TreeLinesPainter.same` — te same linie zostawiają stare ścieżki i warstwę |
| `lib/app/tree/tree_time_bar.dart` (nowy) | rząd czasu: ▶ / ❚❚ (okrąg 36 dp, cel 48 dp, `tooltip`), rok początku, suwak, rok; przy tekście ≥ 150% dwa rzędy; semantyka z kroku 0 |
| `lib/app/tree/tree_screen.dart` | rok jako stan widoku (D37), ▶ i R2, węzły według roku (przerywany obrys — `_DashedRing`, pusty pierścień C1, znicz), przenikanie 150 ms, pigułka liczy osoby w roku, karta z rzędem czasu, prezentacja → „dziś” |
| `lib/app/people/people_list.dart` | `InitialsCircle(outline: false)` — drzewo rysuje wtedy własny, przerywany obrys |

### Found on the emulator (poprawione przed `qa`)
- **(a) Warstwa na każdej osobie.** Pierwsza wersja dawała każdemu węzłowi `AnimatedOpacity` (przenikanie 150 ms). `RenderOpacity` przy kryciu > 0 zawsze tworzy warstwę
  (`proxy_box.dart`: `alwaysNeedsCompositing => child != null && _alpha > 0`), więc 106 warstw w każdej klatce, a do tego `Ticker` wymuszał klatkę 60 razy na sekundę.
  Pomiar ▶ (`FRAME_LOG`, od „Ja”, poziom 2): **14,6% wolnych klatek**, raster mediana 14,5 ms — ponad próg planu (10%). Poprawka jak przy przestawianiu środka w ISSUE-033:
  osoby, które się pojawiają albo znikają w danym roku, w **dwóch wspólnych warstwach** (jeden kontroler 150 ms); osób spoza drzewa w tym roku nie ma w drzewie widżetów; zegar
  ▶ to **timer na kolejny rok** zamiast `Ticker` (klatka tylko przy zmianie roku); linie przemalowane tylko wtedy, gdy się zmieniły. Po poprawce ▶: **7,3% i 9,2%** wolnych
  klatek w dwóch przebiegach, raster mediana 6,5–7,2 ms.
- **(b) Suwak skakał pod palcem.** Napis roku „dziś” jest szerszy niż „1984”, więc tor zmieniał długość przy pierwszym ruchu i uchwyt przesuwał się pod palcem. Napis ma teraz
  stałe miejsce (najszerszy z „dziś” i „8888”).

### Measurements (emulator `Grobing_Restore`, build profile, `FRAME_LOG`)
- **▶ od 1860 do „dziś”: 8,4 s** (oczekiwane 7,96 s; timery na rok spóźniają się łącznie o ok. 0,45 s); od 1880 to ok. 7,3 s — „ok. 7 s” z AC-3 trzymane.
- **R2:** przy zerowej skali animacji rok skacze co dekadę mniej więcej co sekundę (po ok. 5 s — 1910), klatki pojedyncze, bez przenikania; na końcu „dziś” i ▶.
- **Przesuwanie drzewa na „dziś” — punkt odniesienia:** ten sam pomiar na buildzie z ostatniego commita (kopia drzewa roboczego z plikami z `git show HEAD:…`, w katalogu
  sesji) daje dziś **10–25% wolnych klatek** (średnio 16%), ta pozycja **10–26%** (średnio 20%), naprzemiennie, po 6 przesunięć. Zakresy się pokrywają: na tym emulatorze i
  przy obciążeniu komputera ok. 46% (zdalny pulpit, VS Code, przeglądarki) różnicy nie da się wykazać. ISSUE-033 mierzyło przesuwanie płynniej — emulator jest dziś
  wolniejszy niż wtedy. Karta ma własną warstwę (`RepaintBoundary`), żeby przesuwanie nie przemalowywało suwaka. **Płynność na telefonie → ISSUE-032 → *Hand checks*.**

### Deviations
1. **Tempo ▶ ok. 19,7 lat/s zamiast 21** (spóźnianie timerów, wyżej) — od 1880 nadal ok. 7 s. Dokładniej się da (zegar zamiast liczenia kroków), ale zegar nie przesuwa się
   w testach na sztucznym czasie.
2. **Napis roku ma stałą szerokość** (Found b) — specyfikacja tego nie mówi.
3. **Karta w osobnej warstwie** — techniczne, bez zmiany wyglądu.
4. **Osoba przechodząca w „przed narodzinami” w trakcie ▶** gaśnie razem z innymi w jednej warstwie; gdy rok zmienia się co 48 ms, przenikanie 150 ms przerywa następny rok i osoba
   staje się w pełni widoczna wcześniej — przy ręcznym przesuwaniu suwaka przenikanie widać w całości.

### Emulator pass (AC, *States*, zrzuty w katalogu sesji `555909c3-…\scratchpad\shots-emu\`, same wymyślone osoby)
- **AC-2:** rodzice „Ja” w 1981 — bez linii, 1984 — przerywana, 1986 — ciągła (`m-ac2.png`). Para bez daty ślubu (Władysław–Genowefa) — ciągła od 1928, najstarszego dziecka.
- **AC-1 / C1:** „Ja” w 1981 i 1950 — pusty pierścień, karta bez zmian, czytnik „…, to ja — przed narodzinami”; pigułka w 1950: „Poziom 2 · 5 osób”, poziom 3 — 25 (`m-pill.png`).
- **N3:** Kazimierz 1890 — przerywany pierścień w akcencie, bez żony; 1970 — przerywany, bez znicza; 2015 — znicz (`m-kz.png`); czytnik „nie wiadomo, czy już żyje” /
  „…czy jeszcze żyje”. Władysław 1929 — żyje, 1960 — przerywany, 2011 — znicz, czytnik „nie żyje” (`m-wl.png`). Leon (zm. ok. 1944) — niesprawdzany na emulatorze, okno w
  teście `qa`.
- **E3:** Andrzej — 1990 bez „//”, 2000 i „dziś” z „//” na linii z Bożeną; linia do dzieci zostaje (`m-adr.png`).
- **D37:** dotknięcie osoby zostawia rok (1950 → Zofia → Kazimierz); wstecz z widoku osoby — ten sam rok; zakładka Drzewo i „Pokaż w drzewie” — „dziś”; prezentacja z roku 1950 —
  „dziś” (20 osób, znicze — `08c-state.png`), po wyjściu „dziś”.
- **Tekst 200% na 360 dp:** „1860” i rok nad suwakiem, ▶ i suwak pod nimi, nic nie ucięte (`m-200.png`); ▶ 48 × 48 dp, suwak 48 dp wysokości.
- **Emulator po przejściu:** `Grobing_Restore` — build profile tej pozycji z `FRAME_LOG`, dane wyczyszczone (D4) i wymyślona rodzina z datami niepewnymi; skale animacji i
  tekstu z powrotem na 1, gęstość domyślna. `Medium_Phone` nietknięty.

### Dla `qa` — kroki ręczne
Agent na emulatorze — zrobione wyżej (kroki 1–8 planu poza czytnikiem przez TalkBack i Leonem). Autor: odczucie — trzy kroki z planu (▶ od „Ja”, Kazimierz 1880–1910, „//” u
Andrzeja), na `Grobing_Restore`.

## Verification
> `qa`, 2026-10-14. Rytuał WZ-024: `dart format` (bez zmian) → `flutter analyze` (bez uwag) → `flutter test --timeout 120s` — **742 zielone** (było 728; +14) → kroki ręczne.

### Tests (`{code}/test/`)
| AC | Test |
|---|---|
| US-010 AC-1, C1 | `tree_time_test.dart` — osoba w roku: `notYet` / `maybeBorn` / `alive` / `maybeDead` / `dead`, „dziś” jak bez suwaka · `tree_time_screen_test.dart` — rok 1950: 5 z 20 osób na drzewie, „Ja” jako pusty pierścień z czytnikiem „… — przed narodzinami”, karta bez zmian |
| US-010 AC-2, E3 | `tree_time_test.dart` — rodzice „Ja”: 1981 brak, 1984 „razem”, 1986 ślub; ślub bez daty od najstarszego dziecka (1895); Andrzej–Bożena: 1990 bez końca, 2000 i „dziś” z końcem; „razem” bez ślubu zostaje przerywana; „//” w liniach roku (4 punkty) |
| US-010 AC-3, R2 | `tree_time_screen_test.dart` — ▶ od 1860: po 2 s rok 1901, ❚❚ zatrzymuje, dalej do „dziś” i ▶; przeciągnięcie zatrzymuje; dotknięcie osoby w trakcie ▶ nie zatrzymuje; przy `disableAnimations` — 1870, 1880 co sekundę, potem „dziś” |
| D32 (N3) | `tree_time_test.dart` — okna z makiety dla ośmiu osób (ok., między, przed, po, brak; śmierć ok., po, bez daty) i osoba bez dat i rodziny, śmierć ograniczona pochówkiem · `tree_time_screen_test.dart` — czytnik „nie wiadomo, czy już żyje” (1890) i „…czy jeszcze żyje” (1970) |
| D34 (T2) | `tree_time_test.dart` — start 1860; rodzina od 1912 — 1880 |
| D37 | pigułka „Poziom 3 · 25 osób” / „Poziom 2 · 5 osób” w 1950; dotknięcie osoby zostawia rok; „Pokaż w drzewie” — nowe drzewo od „dziś”; widok osoby zatrzymuje ▶, wstecz — ten sam rok; ślad w bok dopiero od początku związku (Teresa 1984 / 1987); linie w roku bez nikogo — puste |
| D3 | test układu ISSUE-033 bez zmian; związek bez daty ma `startKey` (najstarsze dziecko) |
| element 6, D5 | suwak „Rok”, wartość „dziś”, krok czytnika 10 lat (2016 / 2006); po ❚❚ ogłoszenie „Rok 1901” (kanał `accessibility`), w trakcie ▶ żadnego |
| Tekst 200% na 360 dp | lata w rzędzie nad ▶ i suwakiem; cel ▶ 48 × 48 dp (wyjątek tylko na znane przelanie paska zakładek w czcionce testowej — `lib/app/tabs.dart`, jak AC-7 ISSUE-033) |
| Dostępność (retro 3, R2) | `meetsGuideline(androidTapTargetGuideline)`, `labeledTapTargetGuideline`, `textContrastGuideline`; `expectEveryButtonTappable` |
| Fixture | `fictional_family_test.dart` — kształt rodziny bez zmian (106, 38, 31 zmarłych, 39 bez rodziców, 3 w dwóch związkach, 1868–2019, 6 pokoleń) + 2 urodzenia bez daty, 4 z dopiskiem, 1 zgon bez daty, 3 śluby bez daty |

### Review `ui` (subagent, przed stopem #2)
0 BLOCKER, 0 MAJOR, 3 MINOR — **wszystkie poprawione przed stopem** (`dev` w łańcuchu, z testami):
1. ślad partnera przed początkiem związku (Teresa 1981–1985) — teraz od początku związku, jak linia pary (zrzut `m-trace.png`: 1984 bez, 1987 ze śladem);
2. ▶ biegł pod otwartym widokiem osoby — widok zatrzymuje ▶ na bieżącym roku;
3. po zatrzymaniu czytnik nie słyszał roku — jedno ogłoszenie („Rok 1923” / „dziś”) po ❚❚, na końcu i przy otwarciu widoku osoby.
Odstępstwa `dev` 1, 2, 4 przyjęte do [[drzewo]] v1.13; 3 — techniczne. Kontrast z `theme.dart` zgodny (m.in. rok 8,04:1, „1860” 5,01:1, tor 3,10:1, przerywany obrys 3,40:1).

### Family data
Zmiany bez baz, kopii, eksportów i zdjęć; w kodzie, testach i vaulcie tylko wymyślone osoby (rdzenie Wymyśl-, Zmyśl-, Testow-, Przykład-). Próba strażnika treści na obu paczkach
(`echo git add -- …`) — przechodzi. Kopia drzewa roboczego do pomiaru odniesienia leży w katalogu sesji, bez `key.properties` (usunięty przed buildem).

### Not checked live
- czytnik przez TalkBack na emulatorze (gest zwiększania o 10 lat, ogłoszenie po ❚❚) — tylko testem semantyki;
- Leon (zm. ok. 1944) na emulatorze — tylko testem okna;
- płynność ▶ i przesuwania na fizycznym telefonie (emulator dziś zaszumiony: przesuwanie 10–26% wolnych klatek także na buildzie z ostatniego commita).

### Stop #2 (2026-10-14) — autor: *„jest ok ale dla mnie za szybko niemniej w ramach tego issue jest wystarczające”*
- **„ok” — ze śladem na urządzeniu:** po krokach na `Grobing_Restore` w środku drzewa stoi Bożena (krok 3 — drzewo Andrzeja), a log `FRAME_LOG` ma 1255 klatek z
  odtwarzania i przesuwania od chwili, gdy agent zostawił emulator (krok 1). Krok 2 (Kazimierz) — bez osobnego śladu.
- **Tempo ▶ za szybkie dla autora** (ok. 20 lat/s) — w tej pozycji wystarczające, wybór tempa buduje [[ISSUE-038-history-on-tv-and-tempo]] (wejście: autor chce wolniej).
- **Prośba autora przy stopie:** historia na telewizorze i tempo → [[ISSUE-038-history-on-tv-and-tempo]]; animacje związków, zbliżenia i wieniec przy portrecie →
  [[2026-10-14-opowiesc-rodziny-i-wieniec]] (po instalacji MVP — decyzja autora).

### For ISSUE-032 → Hand checks (po jednym w linii)
- ISSUE-037 — krok 2 autora (przerywany obrys u Kazimierza, lata 1880–1910): „ok” bez osobnego śladu na urządzeniu.
- ISSUE-037 — czytnik TalkBack: suwak „Rok” co 10 lat i ogłoszenie roku po ❚❚ — nieprzetestowane na żywo (tylko test semantyki).
- ISSUE-037 — płynność ▶ i przesuwania drzewa na telefonie (emulator zaszumiony: przesuwanie 10–26% wolnych klatek także przed tą pozycją).

### Verdict
**APPROVED** (self-check, z uwagami): wszystkie AC US-010 i decyzje stopu #1 mają testy (742 zielone) i przejście na emulatorze; przegląd `ui` — 0 BLOCKER, 0 MAJOR, 3 MINOR
poprawione przed stopem. Uwagi: tempo ▶ za szybkie dla autora (→ ISSUE-038); czytnika i płynności na telefonie nie sprawdzono na żywo (→ ISSUE-032). Szukałem też i nie
znalazłem: danych rodziny w zmianach (strażnik treści — próba przechodzi), nowych zależności, sieci i uprawnień, zmiany schematu (tylko odczyt).

