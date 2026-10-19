---
title: "ISSUE-050 — „Next” beside ▶ on the tree and the migration map: the year and what happened in it"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-19
verdict-reviewer: self-check
source: "`/pm` 2026-10-18 — autor przeszedł cały przepływ na emulatorze (dane demo), punkt 7 z 7, z doprecyzowaniem w tej samej sesji; część c) z [[2026-10-14-opowiesc-rodziny-i-wieniec]] (INBOX) przeniesiona przed instalację"
created: 2026-10-18
updated: 2026-10-19
---

# ISSUE-050 — „Następne”: rok i co się w nim stało

> Autor: *„opcja przechodzenia do next event (obok przycisku play), aby pokazać, co się działo, i aby dawało krótki komentarz: a) w drzewie — ktoś się
> urodził, ktoś się ożenił, ktoś zmarł; b) na mapie — zmiana miejsca zamieszkania”*. Doprecyzowanie: *„zróbmy tylko „następne” — tak chciałbym, aby
> było na ekranie: data i co się w tym roku stało”*.
>
> 2026-10-14 autor odłożył opowieść rodziny (INBOX c) po instalację; 2026-10-18 „następne zdarzenie” przechodzi przed instalację. Animacje połączeń i
> zbliżenia zostają w INBOX, po instalacji.

## What to build
- **Przycisk „Następne” obok ▶** w listwie czasu — drzewo ([[drzewo]] el. 6 i 11) i mapa migracji ([[mapa-migracji]]): suwak przeskakuje do
  najbliższego późniejszego roku, w którym coś się stało.
- **Na ekranie rok i co się w nim stało:**
  - drzewo — urodziny, śluby (i „razem od”?), zgony;
  - mapa — przeprowadzki.
- **Tylko „następne”**, bez „poprzedniego” (autor).
- Także w trybie prezentacji — podpis czytany z kanapy ([[drzewo]] D38: minimum 16′ — dziś imię 13 sp go nie spełnia, INBOX c pytanie 6).
- Projekt: `ui` przed `planning` — zmiana [[drzewo]] i [[mapa-migracji]].

## Acceptance Criteria
- **AC-1** *Given* drzewo z suwakiem na 1940 *When* dotykam „Następne” *Then* suwak staje na najbliższym późniejszym roku ze zdarzeniem, np. 1952, a na
  ekranie jest „1952” i lista: „Urodził się Jan Wymyślony”, „Ślub: Maria Zmyślona i Piotr Wymyślony” (zmienione na stopie #1, F1 — [[drzewo]] D61: linie
  wielką literą; do 2026-10-19 małą).
- **AC-2** *Given* mapa migracji *When* „Następne” *Then* najbliższy rok z przeprowadzką i podpis, kto się przeprowadził.
- **AC-3** *Given* tryb prezentacji *When* „Następne” *Then* to samo na telewizorze, czytelne z kanapy.
- **AC-4** *Given* ostatnie zdarzenie za nami *When* „Następne” *Then* widać, że dalej nic nie ma (np. „dziś”), bez błędu.

## Notes
- **Przy starcie pozycji `pm` zada jedno pytanie o cel** (retro 4, R1) — zmienia decyzję z 2026-10-14.
- ~~`⚠️ OPEN` (na makietę, stop #1)~~ — **rozstrzygnięte 2026-10-19, stop #1 *„tak”*:** 1 → K1, 2 → N1, 3 → F1, 4 → M2, 5 → Z1; z makiety także V2, P1, U3 ([[drzewo]]
  *Open* 12, [[mapa-migracji]] *Open* 6). Zapis pytań:
  1. **czyje zdarzenia** — domyślnie osób widocznych na ekranie, na bieżącym poziomie ([[ISSUE-049-tree-levels-and-zoom]]);
  2. **daty niepewne** (ok., między, przed, po — [[drzewo]] D32): w którym roku i jak podpisane;
  3. **forma podpisu** — „urodził się” / „urodziła się” z płci; osoba bez płci; śluby bez daty (są w danych testowych);
  4. **mapa: nazwa miejsca w podpisie** — [[mapa-migracji]] D18 zdecydowało „bez nazw krajów i miejsc” na mapie; podpis to co innego, do decyzji;
  5. **zachowanie ▶ po „Następne”** — stoi czy jedzie dalej; ograniczenie animacji (SC 2.3.3).
- Zależy od [[ISSUE-049-tree-levels-and-zoom]] (poziomy). Bez zmiany bazy (zdarzenia z dat osób, związków i zamieszkań).
- [[EPIC-003-zrozumienie]] ([[US-010-czas-na-drzewie]]). Z tego samego przeglądu autora: [[ISSUE-047-grave-first-then-people]] ·
  [[ISSUE-048-portrait-photos]].

## Implementation plan
> `planning`, 2026-10-19. **Cel autora** (pytanie R1 w `/pm` tego dnia): **(a) opowiadanie rodzinie przy telewizorze** — autor dotyka ⏭, rodzina czyta rok i podpis z kanapy;
> telewizor pierwszy, telefon drugi. **Pozycja z ekranem: zmiana istniejących** (drzewo, tryb prezentacji, mapa migracji). Specyfikacja — propozycja `ui` na stop #1: [[drzewo]] **v1.26**
> (element 6 — ⏭ i U3, nowy **6a** — „Następne” i podpis roku, 11 — ⏭ na listwie i podpis pod rokiem; D59–D71; **⚠️ OPEN 12: K, N, F, Z, V, P, U**), [[mapa-migracji]] **v1.5** (12, 13,
> nowy **15** — przeprowadzki i podpis; D27–D29; **⚠️ OPEN 6: M**), [[style-b]] **v1.47** (zdania na telewizorze od 28 sp; bez nowych tokenów). **Makiety (klikalne, na starcie
> rekomendacje):** drzewo i telewizor —
> `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/ef3f4405-6267-49f8-9af6-4889988c7d90/scratchpad/drzewo-050.html` (117 wymyślonych
> osób, przełączniki w sekcjach 1–8, podgląd „z kanapy” 32–65″); mapa —
> `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/ef3f4405-6267-49f8-9af6-4889988c7d90/scratchpad/mapa-050.html`. Task-level pod
> [[US-010-czas-na-drzewie]]; widok 5 (M10). **Bez zmiany bazy** (zdarzenia z dat osób, związków i zamieszkań, liczone przy otwarciu jak `TreeTime`).

> **Stop #1 — 2026-10-19, autor: *„tak”*** na pytanie „Budujemy według rekomendacji: K1 N1 F1 M2 Z1 V2 P1 U3?”. Przyjęte: **K1, N1, F1, M2, Z1, V2, P1, U3** ([[drzewo]] *Open* 12 i
> [[mapa-migracji]] *Open* 6 zamknięte), decyzje projektowe [[drzewo]] D66–D71 i [[mapa-migracji]] D28–D29 oraz brzmienie AC-1 przy F1 (AC-1 poprawione). Specyfikacje [[drzewo]] v1.26,
> [[mapa-migracji]] v1.5 i [[style-b]] v1.47 przestają być propozycją.

### Scope — diff
Plan według rekomendacji **K1 N1 F1 M2 Z1 V2 P1 U3**; inny wybór na stopie #1 zmienia odpowiednie punkty, zanim ruszy `dev`.

**Dane — bez zmiany schematu (v15), bez zmiany kopii.**
1. `lib/app/tree/tree_events.dart` (nowy, czysty Dart, jak `tree_time.dart`) — zdarzenia drzewa z `FamilyTreeData` ([[drzewo]] 6a, D59–D61, D68): narodziny i śmierć z `TreePerson.birth/death`,
   „razem” z `TreeUnion.together` (gdy nie ma ślubu albo „razem” jest wcześniej niż ślub) i ślub z `marriage` (przy `married`); **rok = `from.year` daty**, także przy „ok.”, „przed”,
   „po”, „między” (N1); **data bez roku — nie ma zdarzenia** (okna D31, D32 zostają tylko obrysowi). Pytania: lata ze zdarzeniem dla zbioru osób (bieżący poziom — K1; związek, gdy obie
   osoby w zbiorze), najbliższy późniejszy rok, zdarzenia roku w kolejności: śluby i „razem”, narodziny, śmierć; w grupie miesiąc i dzień, potem imię (`polishCompare`).
   **Linia (F1):** „Urodził się / Urodziła się / Urodził(a) się”, „Zmarł / Zmarła / Zmarł(a)” według `Sex` (null — „(a)”), „Ślub: … i …”, „Razem: … i …”; imię
   `personName(givenNames, surname)` **bez „z d.”**; w parze kobieta pierwsza, inaczej kolejność zapisu; data niepewna — dopisek „(ok. 1870)” z `formatDate` (`lib/app/dates.dart`). Twarde
   spacje: wewnątrz imienia z nazwiskiem, po „i”, w dopisku ([[style-b]] reguła 6). Wynik jako części (słowa i imiona osobno), żeby ekran pogrubił imiona.
2. `lib/app/tree/migration_year.dart` — **przeprowadzki** ([[mapa-migracji]] 15, D27–D29): rok Y, w którym osoba żyjąca ma inne zapisane miejsce niż w Y−1 (ta sama reguła co `person()` —
   D4), raz policzone dla rodziny; pierwsze miejsce, zniknięcie po śmierci i zamieszkanie bez lat — nie. **Linia (M2):** grupa po drodze w tym samym roku — imiona (jak w pkt 1, „, ” i „ i ”),
   „: ”, skąd „ → ” dokąd; miejsce `Residence.nameThen ?? place.name`, przy „cały kraj” `countryName`; dopisek „(ok. 1912)”, gdy początek pobytu ma „ok.”; strzałka z twardą spacją przed
   miejscem docelowym.

**Ekran** ([[drzewo]] v1.26, [[mapa-migracji]] v1.5):
3. `lib/app/tree/tree_time_bar.dart` — `onNext` (null → bez ⏭, D71): przycisk z `Glyphs.skipNext` w akcencie, 24 dp, `applyTextScaling: false`, cel 48 dp, `tooltip` i semantyka „Następne
   zdarzenie”, **zaraz za ▶** we wszystkich trzech układach (rząd, `large`, `oneRow`). **U3:** rok początku tylko w układzie `large` i w `oneRow` (listwa); w zwykłym rzędzie karty go nie ma.
4. `lib/app/tree/tree_screen.dart` — **`_nextEvent()`** (6a, *Navigation*): kończy ścieżkę (`_endPath`), zatrzymuje ▶ (Z1 — D62); gdy podpis ma dalszą stronę roku (> 4 zdarzenia —
   D66) — następna strona; inaczej rok → najbliższy późniejszy ze zdarzeniem (z „dziś” — pierwszy od `time.start`); po ostatnim — `_setYear(null)` i podpis końca, następne dotknięcie od
   początku (D67). Część „Drzewo” — osoby z `layout.positions` (bieżący poziom, K1); część „Mapa” — przeprowadzki z pkt 2. ⏭ jest, gdy zbiór ma choć jedno zdarzenie (D71). Czytnik: po ⏭
   podpis jako region na żywo, bez osobnego `_announceYear`.
5. **Podpis roku:** telefon — dymek w `Positioned(top: 10, left: 16, right: 16)` jak `_levelPill` (powierzchnia, zaokrąglony 12 dp; nagłówek „W 1952” / „W 1955 · 1 z 2” / „Dziś” 13 sp w600
   tekst pomocniczy; linie 14 sp, imiona w600, `Text.rich`; najwyżej 4 linie i „Jeszcze N w tym roku”); w części „Mapa” w miejscu pigułki — `MigrationMap` dostaje podpis i chowa `_Pill`.
   **Telewizor (P1):** pod `PresentationYear` — tekst 48 dp od lewej, 8 dp pod tabliczką, ≤ 62% szerokości, tabliczka w kolorze tła (8 dp), 28 sp, wysokość wiersza 1,25,
   `TextScaler.clamp(maxScaleFactor: 1.3)`, `IgnorePointer` + `RepaintBoundary`; rok w rogu widoczny, dopóki stoi podpis (także „dziś” na końcu). Listwa podpisu nie przesuwa.
6. **Trwanie** (D69): podpis znika w `_chooseYear`, przy starcie ▶, `_setLevel`, `_setPart` i przy ścieżce „Połącz dwie osoby”; zostaje przy dotknięciu osoby, przybliżaniu, przesuwaniu, wejściu
   w tryb i wyjściu z niego.
7. **V2** (D63): po ⏭ w części „Drzewo”, gdy któraś osoba z bieżącej strony leży poza obszarem drzewa bez podpisu (telefon — pod dymkiem; telewizor — pod podpisem i nad listwą, gdy jest)
   — widok jedzie do środka grupy, a gdy się nie mieści — do pierwszej osoby (ok. 0,45 s, ta sama krzywa co przestawienie środka; przy `_noMotion` od razu); skala i `_focus` bez zmian. Mapa
   — nic (R4).
8. `lib/app/tree/migration_map.dart` — po ⏭ przejazd jak przy ▶ (ok. 0,6 s, nie 150 ms suwaka), kadr bez zmian, rozsunięcie się składa; podpis zamiast pigułki (pkt 5).
9. **Glif ⏭:** `skip_next` do `tool/icons/glyphs.txt`, przebudowa fontu według README → *Ikony* (`build_symbols.py`; font Material z commita w README, rysunki autora z
   `C:\Programowanie\Grobing\_ikony-dalle\` — poza repo, bez danych rodziny) → `assets/fonts/grobing-symbols.ttf` i `lib/app/widgets/glyphs.dart` (`Glyphs.skipNext`). Reszta glifów bez
   zmian — porównać listę przed i po.

**Dane testowe:** wymyślona rodzina z `lib/dev/` ma daty niepewne, śluby bez daty i zamieszkania (przycisk „Wymyślone miejsca zamieszkania i portrety”) — bez zmian; osoba bez płci
tylko w teście jednostkowym.

**Brzmienie AC-1 przy F1** (poprawione po „tak”): *… a na ekranie jest „1952” i lista: „Urodził się Jan Wymyślony”, „Ślub: Maria Zmyślona i Piotr Wymyślony”* (linie wielką literą).

### AC → test happy-path (`qa`)
| AC | Test |
|---|---|
| AC-1 | jednostka `tree_events` (wymyślona rodzina): najbliższy rok po 1940, linie roku z narodzinami i ślubem, „ok.”, osoba bez płci „(a)”, kolejność w roku, data bez roku pominięta; ekran: suwak 1940 → ⏭ → rok w karcie i dymek z liniami; rok z > 4 zdarzeniami — strona 1 z „Jeszcze N w tym roku”, ⏭ → strona 2 tego roku |
| AC-2 | jednostka `migration_year`: przeprowadzki i linie M2 (grupa po drodze, kraj, „ok.”, nazwa z tamtego czasu); ekran mapy: ⏭ → rok przeprowadzki, podpis zamiast pigułki, kadr bez zmian |
| AC-3 | ekran w trybie prezentacji: ⏭ na listwie → rok w rogu i podpis pod nim (28 sp, skala tekstu najwyżej 1,3); sterowanie znika po 5 s, podpis stoi |
| AC-4 | ekran: ostatnie zdarzenie → ⏭ → „dziś” i „To wszystkie zdarzenia z datą.”; ⏭ → pierwsze zdarzenie; zbiór bez zdarzeń z datą → bez ⏭ |

Dodatkowo (decyzje projektowe): Z1 — ⏭ przy biegnącym ▶ zatrzymuje je; D69 — podpis znika przy suwaku, ▶, zmianie poziomu i części, zostaje przy dotknięciu osoby; V2 — osoba z podpisu
poza obszarem trafia po ⏭ do obszaru, skala bez zmian; U3 — przy 100% bez roku początku w karcie, przy 200% z nim; `meetsGuideline` (cel ⏭ 48 dp) i „przycisk ma akcję dotknięcia”;
tekst 200% na 360 dp bez przepełnienia. **Bez testu migracji i odtworzenia** — schemat i kopia się nie zmieniają. Rytuał WZ-024: `dart format` → `flutter analyze` →
`flutter test --timeout 120s`.

### Manual checks (stop #2)
**Agent na emulatorze — przed stopem, ze zrzutami.** `Grobing_Restore` ma **demo**: najpierw zapisać obecny stan i wgrać stan sprzed demo z `C:\Programowanie\Grobing\_pokaz`
(README tam), **nigdy `pm clear` bez zapisanego tar**; po pozycji — demo z powrotem (jak w ISSUE-047–049).
1. Drzewo, „Ja”, „Linia krwi”: ⏭ z „dziś” → pierwsze zdarzenie, potem kilka ⏭ — rok w karcie, dymek, widok podjeżdża do osób z podpisu; rok z więcej niż 4 zdarzeniami — strona 2.
2. Koniec: ostatnie zdarzenie → ⏭ → „dziś” i podpis końca → ⏭ → pierwsze zdarzenie.
3. ▶ biegnie → ⏭ zatrzymuje; suwak, ▶ i + zabierają podpis, dotknięcie osoby — nie.
4. Mapa (przycisk wymyślonych zamieszkań w „Stanie danych”): ⏭ → przeprowadzki, podpis w miejscu pigułki, okręgi jadą, kadr stoi.
5. Tryb prezentacji (poziomo): ⏭ na listwie, rok w rogu i podpis pod nim; po 5 s listwa znika, podpis stoi; to samo na mapie.
6. Tekst 200% na 360 dp: rząd czasu z ⏭, dymek; TalkBack — opisy ⏭ i podpisu (`uiautomator dump`); „Usuń animacje” — rok i widok przeskakują.
7. **Klatki** (retro 4, R3): build profile z `FRAME_LOG`, naprzemiennie z buildem odniesienia — ⏭ z podjazdem widoku; po każdym `flutter build` — `android\gradlew --stop`.

**Autor: odczucie — najwyżej 3 kroki** (emulator, tryb prezentacji):
1. Opowiedz kilka lat, dotykając ⏭ na listwie — czy tak będziesz opowiadać rodzinie? (*Obali* [[drzewo]] D62, D66, D69)
2. Patrz na podpis pod rokiem, gdy drzewo podjeżdża do osób — czy wiesz, o kim mowa, i czy nic ważnego nie jest zasłonięte? (*Obali* D63, D64)
3. Przełącz na mapę i dotknij ⏭ kilka razy — czy „skąd → dokąd” w podpisie jest Ci potrzebne? (*Obali* [[mapa-migracji]] D27)

Na telefonie i telewizorze (lista **B** w [[ISSUE-032-mvp-install]] → *Hand checks*): podpis 28 sp z kanapy na Twoim telewizorze; ⏭ na telefonie z obrazem na telewizorze.

### Out of Scope
- zbliżenia i efekty na zdarzeniach, wyróżnianie osób z podpisu — [[2026-10-14-opowiesc-rodziny-i-wieniec]] c), po instalacji ([[drzewo]] D70);
- „Poprzednie” (autor: tylko „Następne”);
- koniec związku i pochówek w podpisie ([[drzewo]] D68); miejsca urodzenia i zgonu na mapie ([[mapa-migracji]] D12);
- jedna linia dla kilku narodzin („Urodzili się: …”) — w drzewie linia na zdarzenie, łączenie tylko na mapie (wspólna droga);
- ⏭ w mini-drzewie w [[osoba]]; zapamiętanie roku albo podpisu po zamknięciu aplikacji;
- znane drobne usterki drzewa z *CURRENT_STATE* — osobne kandydatki.

### Decision for stop #1 (author) — jedno pytanie
**Budujemy według rekomendacji: K1 N1 F1 M2 Z1 V2 P1 U3?** „tak” = obie makiety tak, jak otwierają się na starcie + decyzje projektowe niżej + brzmienie AC-1 przy F1. Inna odpowiedź:
litery wariantów, np. „P2, U2” (reszta zostaje).
- **K1** — podpis mówi o osobach z wybranego poziomu; + dokłada rodziny razem z ich zdarzeniami (K2: cała rodzina, także osoby, których na drzewie nie widać);
- **N1** — „ok. 1870” stoi w 1870 z dopiskiem „(ok. 1870)” (N2: daty niepewne pomijane — w makiecie 6 ze 147 zdarzeń);
- **F1** — „Urodził się Jan …”, „Urodziła się Maria …”, osoba bez płci „Urodził(a) się …” (F2: „Narodziny: …”, „Śmierć: …”);
- **M2** — na mapie „Kazimierz Wymyślony: Zmyślin → Francja” (M1: „Przeprowadził się Kazimierz Wymyślony”, bez miejsca — jak sama mapa);
- **Z1** — ⏭ zatrzymuje biegnącą historię, podpis stoi (Z2: jak w odtwarzaczu — historia biegnie, podpis znika po 0,1 s);
- **V2** — gdy osoby z podpisu nie widać, drzewo podjeżdża do niej bez zmiany przybliżenia (V1: widok stoi — od „Ja” w pierwszych 12 podpisach 0 z 16 osób na ekranie);
- **P1** — na telewizorze podpis pod rokiem w lewym górnym rogu (P2: na dole na środku, jak napisy — skacze nad listwę po każdym ⏭);
- **U3** — w karcie telefonu ▶ ⏭, suwak, rok, tempo; rok początku znika (U1: zostaje, suwak prawie bez toru; U2: dwa rzędy, drzewo niższe o 48 dp).

Decyzje projektowe, które przechodzą na „tak” (widać je na makietach): ⏭ z „dziś” zaczyna od pierwszego zdarzenia, po ostatnim — „dziś”, „To wszystkie zdarzenia z datą.” i od nowa; najwyżej
4 zdarzenia naraz, dalszy ciąg roku tym samym ⏭; podpis stoi, dopóki stoi rok, bez odliczania; imiona bez „z d.”; koniec związku nie jest zdarzeniem; ⏭ nie ma, gdy na poziomie nie ma żadnej
daty; na mapie jedna linia na wspólną drogę i kadr się nie rusza; na telewizorze podpis 28 sp.

**Czego to nie da:** odpowiedzi „który to?” na drzewie bez zbliżeń — imiona pod węzłami czyta się z bliska, a podpis mówi imieniem; i wolnego lewego górnego rogu telewizora przy kilku
zdarzeniach (do ok. 190 dp z 411). Termin: ok. 1–1,5 dnia (z przebudową fontu ikon); po zamknięciu licznik retro dojdzie do 10 → retro 5, potem NT-007 i ISSUE-032 — mieści się do 2026-10-29.

## Dev report
> `dev`, 2026-10-19. Flutter 3.41.1 (przypięty). `flutter analyze` — czysto. Bez zmiany schematu (v15) i kopii. Wymyślone dane z `lib/dev/` bez zmian.

### Done
1. `lib/app/tree/tree_events.dart` (nowy) — zdarzenia drzewa z `FamilyTreeData` (D59–D61, D68): narodziny, śmierć, „razem” (bez ślubu albo wcześniej niż ślub), ślub; rok z
   `from.year` także przy „ok.”, „przed”, „po”, „między”; data bez roku — brak zdarzenia. `yearsOf(people, start, now)`, `inYear(year, people)` (śluby i „razem”, narodziny, śmierć; miesiąc,
   dzień, imię), `line(event)` — F1 według `Sex` (null → „(a)”), imię bez „z d.”, w parze kobieta pierwsza, dopisek z `formatDate`. Twarde spacje w imieniu z nazwiskiem, po „i”, w
   dopisku i między czasownikiem a „się”. `captionPage = 4`.
2. `lib/app/tree/migration_year.dart` — `MapMove`, `moves` (raz na rodzinę; lata początków i końców pobytów, porównanie `person(y−1)` i `person(y)`), `moveYears(start)`,
   `moveLines(year, people)` — M2: grupa po drodze w tym samym roku, imiona w kolejności urodzenia (początek okna), `nameThen ?? name`, przy kraju nazwa kraju, „(ok. 1912)” przy
   niepewnym początku pobytu, strzałka z twardą spacją przed miejscem docelowym.
3. `lib/app/tree/tree_time_bar.dart` — `onNext` (null → bez ⏭, D71): `IconButton` z `Glyphs.skipNext` w akcencie, 24 dp, `tooltip` „Następne zdarzenie”, zaraz za ▶ we wszystkich trzech
   układach. **U3:** w zwykłym rzędzie karty z ⏭ nie ma roku początku; w układzie ≥ 150% i na listwie jest.
4. `lib/app/tree/tree_screen.dart` — `_nextEvent()` (Z1, D66, D67), `_Caption` (rok, linie z chwili ⏭, strona, część), dymek na telefonie (`_captionBubble`, w części „Mapa” zamiast
   pigułki) i podpis pod rokiem na telewizorze (`_captionTv`, 28 sp, ≤ 62% szerokości, skala tekstu ≤ 1,3), oba regionami na żywo; podpis znika w `_chooseYear`, przy starcie ▶,
   `_setLevel`, `_setPart`, `_showPath` i nowych danych, zostaje przy dotknięciu osoby i w trybie prezentacji (D69); rok w rogu widoczny, dopóki stoi podpis; ⏭ w karcie i na listwie,
   gdy jest choć jedno zdarzenie; **V2** — `_frameCaption()` po klatce (D63; zob. *Deviations* 2).
5. `lib/app/tree/tree_presentation.dart` — `PresentationYear.bottom(context)` (dolna krawędź tabliczki roku przy danej skali tekstu).
6. `lib/app/tree/migration_map.dart` — `showPill` (pigułka znika pod podpisem) i `ride` (po ⏭ przejazd 0,6 s jak przy ▶).
7. **Glif ⏭:** `skip_next` w `tool/icons/glyphs.txt`, font przebudowany (`build_symbols.py`; font Material z katalogu sesji ISSUE-046, rysunki autora z `_ikony-dalle`) →
   `assets/fonts/grobing-symbols.ttf` (244 048 → 246 304 B), `Glyphs.skipNext = Glyph(0xe044)`. **Sonda przed zmianą:** przebudowa z listą sprzed zmiany dała plik różny od
   zacommitowanego tylko w 9 bajtach (znacznik czasu `head.modified` i sumy kontrolne) — źródło fontu to samo. W `glyphs.dart` doszła jedna linia, kody glifów z arkusza bez zmian.

### Deviations
1. **Podpis na telewizorze — tabliczka 48 dp od lewej, tekst 54 dp** ([[drzewo]] 6a: „tekst 48 dp od lewej”): tabliczka podpisu stoi tam, gdzie tabliczka roku, z tym samym wcięciem 6 dp,
   więc tekst podpisu zaczyna się równo z cyframi roku. Margines z D38 (≥ 48 dp) zachowany.
2. **V2 — grupa pod podpisem, nie na środku obszaru** (D63: „na środku tego obszaru”): na emulatorze przy 200% na 360 dp środek obszaru drzewa wypadał na wysokości + / − poziomu w rogu
   i „Tomasz” stał pod „+” (zrzut `t200-next`); wyłączenie całej kolumny przycisków zwęziło obszar tak, że para się nie mieściła i było gorzej (zrzut `t200-fixed`). Teraz: grupa 8 dp pod
   podpisem (ludzie stoją przy słowach o nich), w poziomie na środku; za szeroka — pierwsza osoba zawsze w obszarze; ktoś na + / − — grupa przesuwa się w lewo, dopóki pierwsza osoba się mieści.
   Za wysoka — rząd pierwszej osoby u góry. Po zmianie przy 200% para stoi pod dymkiem, z dala od „+” (zrzut `t200-v2c`).
3. **„Urodził się”, „Urodziła się” z twardą spacją przed „się”** — poza regułą 6 (ta mówi o jednoliterowych słowach); linia nie zaczyna się od „się Jan…”.

### Found on the emulator (poprawione przed oddaniem `qa`)
- V2 przy 200% — imię pod „+” (*Deviations* 2).

### Measurements (`Grobing_Restore`, build profile z `FRAME_LOG`, 1080 × 2400, gęstość 420; zrzuty i skrypty w `emu050\` katalogu sesji)
- **⏭ w karcie:** cel 126 × 126 px = 48 dp, klikalny, opis „Następne zdarzenie”; roku początku w karcie nie ma (U3). Suwak przy 100% — 497 px = 189 dp (tor Fluttera ok. 141 dp);
  przy 200% na 360 dp (gęstość 480) — dwa rzędy, suwak 240 dp, ⏭ obok ▶.
- **Całe przejście ⏭ od „Ja”, „Linia krwi”:** 83 lata ze zdarzeniem + koniec = 84 dotknięcia do „dziś”, pięć lat w dwóch stronach (1955, 1958, 1960, 1983, 2010 — jak pomiar makiety), potem
  1868 od nowa (AC-4). Mapa: 16 lat przeprowadzek (1914–2024) do „dziś” i „To wszystkie przeprowadzki z datą.” (poprawione przez `qa`: było „15” — liczone od 1914).
- **V2 (po *Deviations* 2), całe koło od „Ja” w skali 1:** po każdym ⏭ co najmniej jedna osoba z podpisu na ekranie; razem 123 ze 178 osób z podpisów (69%) — reszta to grupy szersze niż
  ekran (np. ślub i trzy narodziny w różnych gałęziach).
- **Telewizor (914 × 411 dp):** tabliczka podpisu 48 dp od lewej, 75 dp od góry (8 dp pod rokiem); 4 zdarzenia — 146 dp wysokości, 447 dp szerokości (49% ekranu), dół ok. 221 dp.
  Listwa po ⏭ znika po 5 s, rok i podpis zostają.
- **„Usuń animacje”:** ekran 0,15 s po ⏭ równy ekranowi po 1,35 s w 3 z 4 dotknięć (z animacjami — w 1 z 4).
- **Klatki, naprzemiennie z buildem odniesienia** (`new-049f-profile.apk` — ostatni build ISSUE-049 z sesji `92dbd968-…`; `git archive` blokuje strażnik komend): przestawienie środka
  dotknięciem — odniesienie 42,6% i 27,1% wolnych klatek, nowy 37,3% i 21,7%; ▶ przez całą historię — odniesienie 18,5% i 15,7%, nowy 19,1% i 13,4%; **⏭ z podjazdem** (12 dotknięć) —
  19,2%, 16,4%, 23,1%, raster p50 ok. 14,7 ms, p90 ok. 18 ms. **Pojedyncze klatki rastra 130–175 ms** przy niektórych ⏭ (np. 1898, 1920), także w drugim kole tej samej sesji — ten sam
  rząd co przy ▶ w buildzie odniesienia (85–127 ms, 3 klatki > 50 ms na przebieg w obu buildach), czyli koszt zmiany roku na emulatorze, a nie ⏭. Do sprawdzenia na telefonie — lista B.

### Dla `qa`
- **Dwa testy padają z powodu U3** (`test/app/tree/tree_time_screen_test.dart`): „element 6 — ▶, 1860, the slider…” i „ISSUE-038 AC-3 — … a decade at once” szukają „1860” w karcie przy
  tekście 100%. Po U3 rok początku jest w karcie tylko przy ≥ 150% i na listwie trybu prezentacji — oczekiwanie do poprawy, nie usterka.
- `uiautomator dump` w trakcie ▶ zwraca stary plik (ekran nigdy nie jest bezczynny) — stan sprawdzać po zatrzymaniu albo zrzutem.
- Testy według planu (*AC → test happy-path*); jednostkowo także osoba bez płci („Urodził(a) się”) i rok z > 4 zdarzeniami.

## Verification
> `qa`, 2026-10-19. Rytuał WZ-024: `dart format` → `flutter analyze` (czysto) → `flutter test --timeout 120s` — **985 zielonych** (przed pozycją 964; po poprawkach z przeglądu
> przebieg powtórzony). Bez zmiany schematu i kopii — bez testu migracji i próbnego odtworzenia (plan).

### AC → test (happy path)
| AC | Test |
|---|---|
| AC-1 | `tree_events_test.dart` — lata od 1868, „ok. 1870” w 1870, ślub i narodziny bez daty nie są zdarzeniem, słowa F1 z dopiskami, kolejność 1955 na „Linii krwi”, bez płci „Urodził(a) się”; `tree_next_test.dart` — „AC-1 — ⏭ right after ▶”: 1940 → ⏭ → 1944 „Zmarł Leon Wymyślony (ok. 1944)”, → 1946 „Ślub: Helena Wymyślona i Józef Wymyślony”, region na żywo, cele dotyku |
| AC-2 | `migration_year_test.dart` (grupa „ISSUE-050 — moves”) — przeprowadzki (pierwsze miejsce, śmierć i miejsce bez lat nie), powrót po zagnieżdżonym pobycie, linie M2 (wspólna droga, kraj, „ok.”, nazwa z tamtego czasu, twarde spacje); `tree_next_test.dart` — „AC-2” na mapie: podpis zamiast pigułki, kadr bez zmian, koniec „To wszystkie przeprowadzki z datą.” |
| AC-3 | `tree_next_test.dart` — „AC-3 (P1)”: ⏭ na listwie zaraz za ▶, rok w rogu i podpis pod nim (8–12 dp, 28 sp, równo z cyframi roku), czytnik „W 1868. Urodził się Antoni Wymyślony”, listwa znika po 5 s, podpis zostaje i wraca na telefon |
| AC-4 | `tree_next_test.dart` — „AC-4, D67”: z „dziś” → 1868; po 2019 → „dziś”, „Dziś”, „To wszystkie zdarzenia z datą.”; → 1868 bez błędu; „D71, U3” — bez zdarzeń nie ma ⏭ |

Dodatkowo: **D66** (1955: 4 + „Jeszcze 1 w tym roku”, strona 2, potem 1956) · **Z1** (▶ od 1860, przy 1870 ⏭ → 1893, ▶ stoi) · **D69** (podpis znika z suwakiem, ▶, poziomem; zostaje
po dotknięciu osoby) · **V2** (Antoni po ⏭ na ekranie pod podpisem, skala bez zmian) · **SC 2.3.3** (przy wyłączonych animacjach widok od razu w miejscu docelowym) · **U3** przy 200% na
360 dp (dwa rzędy, rok początku, bez przepełnienia — poza znanym artefaktem czcionki testowej w dolnym pasku `tabs.dart`) · dwa testy `tree_time_screen_test.dart` poprawione pod U3
(„1860” w karcie przy 100% → brak; w teście „animations off” jeden napis zamiast dwóch).

### Przegląd `ui` (subagent bez historii; 23 zrzuty z `emu050\shots\`, kod, `theme.dart`)
- **MAJOR — ślub i „razem” z niepewną datą bez dopisku** (`tree_events.dart` → `line()`): narodziny i śmierć miały „(ok. …)”, związek nie — przy „ślub przed 1920” podpis wyglądałby na pewną
  datę. **Poprawione przed stopem** (w roli `dev`): dopisek także po drugim imieniu; test „D60 — a union with an uncertain date”.
- **MINOR — podpis na telewizorze czytany bez roku** (rok stoi w rogu): **poprawione** — semantyka podpisu „W 1868. Urodził się …”, wspólne `_captionHead` z dymkiem telefonu; test w AC-3.
- Odstępstwa `dev` 1–3 **przyjęte** i wpisane do [[drzewo]] **v1.27** (6a, 11, *States*, D61, D63, D64). Zgodne: kolejność elementów i stany, role kolorów (▶ jedyny wypełniony, ⏭ akcent
  bez wypełnienia), kontrasty z `theme.dart` (⏭ 8,04, dymek 10,02 / 5,01, telewizor 10,98 / 5,50, rok 8,81), cel ⏭ 48 dp, reguła 6, podpis 28 sp i 8 dp pod rokiem, ton, tylko wymyślone osoby.
- **Uwagi bez poprawki (obserwacje):** (a) długie imię z nazwiskiem przy 200% albo na telewizorze przy 1,3× — twarde spacje nie dają łamania, więc wiersz złamie się w środku słowa (dane
  demo tego nie mają); (b) telewizor przy tekście 130% i roku z czterema długimi liniami — podpis może przez 5 s sięgać pod listwę (z wyliczenia: ok. 361 dp przy górze listwy ok. 331 dp);
  (c) przy V2 rodzice nowo narodzonych bywają pod dymkiem (koszt zapisany w D63).

### Family data
Zmiany w kodzie, testach i vaulcie bez danych rodziny: przykłady tylko z rdzeni Wymyśl-, Zmyśl-, Testow-, Przykład-; bez plików `*.db`, kopii, eksportów i zdjęć (font ikon to zasób aplikacji).
Strażnik przepuścił próbne `git add` obu paczek (kod — 13 plików, vault — 5). Pozycja bez sieci (3b nie dotyczy).

### Emulator (agent, przed stopem)
`Grobing_Restore`, stan sprzed demo z `_pokaz`; kroki 1–7 z planu zrobione przez `dev` (zrzuty `emu050\shots\`: całe koło drzewa i mapy, telewizor, 200%, „Usuń animacje”, klatki) — liczby
w *Dev report* → *Measurements*. Na stop #2 zainstalowany build z poprawkami przeglądu (`new-050d-profile.apk`).

### Stop #2 — runda 1 (2026-10-19, autor na emulatorze)
Autor napisał „ok”, przerwał i podał zmiany (traktowane jako opis zmian, nie „ok”):
1. *„dobrze by było gdyby rzeczy które się dzieją były podświetlone na telewizorze (obwódka wokół osoby i/lub podświetlona relacja) natomiast sama informacja kto się urodził itd. niech
   zostanie na telefonie (aby nie przysłaniała drzewa na telewizorze)”*;
2. *„jak wyżej - chciałbym aby ich obwódka / laur "lśniały"”*;
3. *„Niech zostaną te informacje (z wyjątkiem pokazywania na telewizorze) i tak samo aby te avatary "lśniały" gdy coś się zmienia”* (mapa).

**Ograniczenie techniczne, przed rundą 2 — pytanie do autora:** w trybie prezentacji telewizor dostaje kopię ekranu telefonu (przesyłanie ekranu — [[drzewo]] D11, D29, [[ISSUE-036-cast-from-the-app]]),
więc telefon i telewizor pokazują ten sam obraz; „tylko na telefonie” w trakcie prezentacji nie istnieje bez drugiego ekranu. Warianty: **A** — w trybie prezentacji żadnego podpisu, samo
lśnienie; **B** — po ⏭ krótka linia na listwie sterowania (mały druk przy ⏭), znika z listwą po 5 s; na drzewie lśnią osoby zdarzenia (obwódka / wieniec, przy związku obie osoby i linia
między nimi), na mapie lśnią przeprowadzające się awatary; poza prezentacją dymek bez zmian. **Decyzja autora: *„B”*** (2026-10-19). Runda 2: `ui` ([[drzewo]] v1.28, [[mapa-migracji]] v1.6,
[[style-b]] v1.48) → `dev` → `qa` → stop #2, runda 2.

### Runda 2 — plan (2026-10-19, `planning` po „B”)
Specyfikacje: [[drzewo]] v1.28 (6a, 11, D72–D75), [[mapa-migracji]] v1.6 (13, 15, D30), [[style-b]] v1.48 (reguła 2). Bez nowego stopu #1 — zakres to decyzja autora „B” na stopie #2,
sprawdzana w rundzie 2 stopu #2.
- **Diff zakresu:** − podpis 28 sp pod rokiem (P1, D64) · + linia podpisu na listwie nad ▶ ⏭, 14 sp, znika z listwą (D72) · + osoby z podpisu świecą: pierścień, poświata pod okręgiem i
  wieńcem, trzy pulsy, potem stała; przy ślubie i „razem” linia pary (D73–D75) · + na mapie świecą przeprowadzający się, schowani w „+N” — „+N” (D30) · V2 w trybie prezentacji — obszar od
  tabliczki roku do listwy.
- **AC-3 po „B”:** z kanapy czyta się rok (36 sp) i widać, kogo dotyczy (świecenie); słowa czyta autor z listwy w ręce (D72).
- **Pliki:** `lib/app/tree/tree_screen.dart` (`_Caption` z osobami linii, `_shine`, warstwa poświaty, linie par, linia na listwie, `_frameCaption`), `lib/app/tree/migration_year.dart`
  (osoby linii przeprowadzki), `lib/app/tree/migration_map.dart` (`_PersonCircle`, `_PlusBadge`); testy `test/app/tree/tree_next_test.dart`, `test/app/tree/migration_year_test.dart`.
- **AC → test:** AC-3 — linia na listwie (czytnik „W 1868. Urodził się …”), pod rokiem nic, linia znika z listwą po 5 s, osoby z podpisu świecą · AC-1 — świecą osoby strony, przy ślubie
  linia pary · SC 2.3.3 — przy ograniczeniu animacji poświata stała od razu · AC-2 — na mapie świecą przeprowadzający się.
- **Agent na emulatorze:** linia na listwie przy 100% i 200% (najdłuższa strona — 1955), świecenie przy skali 1 i przy całym poziomie, ślub z linią pary, wieniec, „+N” na mapie, pomiar
  klatek pulsu naprzemiennie z buildem odniesienia (`new-050d-profile.apk`).
- **Autor — odczucie (≤ 3):** czy świecenie widać i czy nie męczy · czy linia na listwie wystarcza jako ściąga · mapa: czy świecące awatary prowadzą oko.

### Dev report — runda 2 (2026-10-19)
**Done**
1. **Linia podpisu na listwie** (D72): `_captionLine` w `PresentationBar` nad rzędem ▶ ⏭ — nagłówek 13 sp (tekst pomocniczy), 12 dp odstępu, zdarzenia „ · ” z twardą
   spacją po kropce, 14 sp, imiona półgrube, „Jeszcze N w tym roku”; region na żywo z etykietą „W 1868. Urodził się …”. Podpis 28 sp pod rokiem (`_captionTv`) usunięty;
   `_captionEnd` wspólny dla dymka i listwy.
2. **Świecenie** (D73–D75): `_Caption.who` — osoby każdej linii (drzewo: `TreeEvent.people`, związek = para; mapa: `MigrationYear.movePeople`); `_shining` — osoby strony.
   `_shine` (3,6 s) i `_ShineLevel`: do 0,30 w 0,3 s, trzy pulsy po 1,2 s do 0,65, potem 0,30. Warstwa `_ShinePainter` pod osobami, nad liniami rodziny: gradient
   promienisty pod okręgiem albo pod wieńcem (0,4 pudełka wieńca), przy oddaleniu stała wielkość na ekranie (`_labelScale`), przesuwa się z przestawieniem środka.
   Pierścień — `lit` węzła. Linia pary — `layout.pathRoute` krokiem „partner”, `PathLinePainter(together: true)`, rośnie w 0,45 s, czeka z liniami rodziny przy przestawieniu.
   Przy ograniczeniu animacji `_shine.value = 1` od razu.
3. **V2 w trybie prezentacji:** obszar od dołu tabliczki roku (bez podpisu pod nim) do listwy.
4. **Mapa** (D30): `shine` / `shineLevel` do `MigrationMap`; `_PersonCircle` — pierścień 2,5 dp i pulsująca poświata; `_PlusBadge` — pierścień i poświata, gdy ktoś z
   podpisu jest w „+N”.

**Deviations** (wszystkie wpisane przez `ui` w tej samej rundzie — [[drzewo]] v1.28, [[mapa-migracji]] v1.6)
1. **Na mapie osoby z podpisu idą w stosie na przód** — v1.6 przed przejściem mówiła „kolejność zostaje, świeci „+N””; na emulatorze przy kadrze rodziny na dwóch
   kontynentach przeprowadzka z Litwy skończyła się w skupieniu 14 osób i świecił tylko „+11” (zrzut `r2-map01-peak`). Teraz Bronisława stoi pierwsza i świeci (`r2-map03-front`);
   „+N” świeci tylko przy więcej niż trzech. D30 przepisane.
2. **Wejście w tryb prezentacji (i powrót) z podpisem podjeżdża do jego osób** — przed poprawką telewizor pokazywał tylko pusty pierścień „Ja” (zrzut `r2-tv01-enter`),
   a świecące osoby były poza ekranem; po — para z 1921 na ekranie (`r2-tv04-enter-framed`). [[drzewo]] 6a (*Trwanie*).
3. **Gradient zamiast rozmycia** pod osobami — ten sam wygląd; rozmycie było podejrzane o wolne klatki, pomiar tego nie potwierdził (niżej), gradient został jako tańszy.

**Found**
- **Telefon, tekst 200% na 360 dp — dymek 4 zdarzeń (1955) zakrywa całe drzewo** (`r2-200-01-phone-1955`): świecących osób nie widać pod dymkiem. To dymek z rundy 1
  (D66 — 4 zdarzenia), nie zmiana rundy 2; najgorszy przypadek, do decyzji autora, jeśli przeszkadza.
- **Tryb prezentacji, 200% na 360 dp — linia 1955 ma 4 wiersze, listwa zajmuje ok. 53% wysokości** (191 z 360 dp) na 5 s (`r2-200-03-tv-bar`); bez ucinania, łamanie
  zgodne z regułą 6 („· Urodziła się …” na początku wiersza). Przy 100% na 411 dp — 1–2 wiersze. Zapisane w D72 (*Nie da*).

**Measurements** (`Grobing_Restore`, 1080 × 2400, gęstość 420; zrzuty `emu050\shots\r2-*`)
- Telefon: 1868 — Antoni z pierścieniem, poświata za wieńcem, puls (`r2-01`) i stała (`r2-02`); 1921 — ślub, obie osoby i linia pary (`r2-03`).
- Tryb prezentacji: 1922 — linia na listwie „W 1922  Ślub: Wiktoria Zmyślicka i Ignacy Zmyślicki”, para świeci (`r2-tv02`); po 5 s — rok i świecące osoby, bez słów (`r2-tv03`).
  Węzeł czytnika: „W 1921. Ślub: Jadwiga Wymyślona i Franciszek Wymyślony” na listwie, nieklikalny.
- Ograniczenie animacji (`transition_animation_scale 0`): ekran 0,15 s po ⏭ = ekran 1,35 s po ⏭ w 4 z 4 dotknięć; z animacjami 0 z 4; poświata stała (`r2-nomotion`).
- **Klatki, naprzemiennie z buildem odniesienia** (`new-050c-profile.apk`, runda 1, `FRAME_LOG`; `new-050d` jest bez `FRAME_LOG`), 12 × ⏭ od „dziś”: nowy build 873–970
  klatek (puls rysuje ciągle), wolnych 23–36%, raster p50 14,0–15,3 ms, p90 19–24 ms, > 50 ms: 5–15; odniesienie 361–413 klatek, wolnych 23–38%, raster p50 14,2–15,1,
  p90 19–23, > 50 ms: 1–6. Na klatkę bez zmiany (p50, p90, udział > 50 ms ok. 1,0% vs 0,8%); więcej klatek, bo puls trwa 3,6 s po każdym ⏭. Po pulsie klatek nie ma:
  69 w pierwszych 1,5 s po ⏭, 0 między 4 a 7 s.
- Nie przeszedłem: świecenia przy oddaleniu (skala < 1) — `adb input` nie ma dwóch palców; do testu widżetu (`qa`).

**Dla qa**
- Test AC-3 (P1) do przepisania: linia na listwie, pod rokiem nic, linia znika z listwą, czytnik „W 1868. Urodził się Antoni Wymyślony”.
- Nowe: świecą osoby strony (`_TreeNode.lit` / warstwa `_ShinePainter`), przy ślubie linia pary, przy ograniczeniu animacji poziom stały od razu, przy oddaleniu wielkość
  na ekranie stała; mapa — `movePeople`, przód stosu, „+N”.
- Build na emulatorze: `new-050h-profile.apk` (z `FRAME_LOG`).

**Po przeglądzie `ui` (w roli `dev`):** poświata na mapie z cienia w każdym okręgu i w „+N” (przerysowywanego w każdej klatce pulsu) na **jedną warstwę gradientu** pod osobami
(`_ShineLayer`), jak w drzewie; okrąg i „+N” mają już tylko pierścień. Klatki mapy, 12 × ⏭, naprzemiennie z `new-050c`: przed poprawką 25,8–37,3% wolnych, raster p90 20–30 ms, > 50 ms:
8–27 (odniesienie 21,6–23,3%, p90 18–19, 4–5); po — 25,3–25,5%, p90 19,4–19,8 ms, > 50 ms: 6–10 (odniesienie 27,6–28,5%, p90 21,2–21,3, 3–6). Zrzuty `r2-map04` (puls) i `r2-map05`
(stała). Build na stop #2: `new-050k-profile.apk` (bez `FRAME_LOG`).

### Verification — runda 2
> `qa`, 2026-10-19. Rytuał WZ-024: `dart format` → `flutter analyze` (czysto) → `flutter test --timeout 120s` — **989 zielonych** (po rundzie 1: 985). Bez zmiany schematu i kopii.

| Co | Test |
|---|---|
| AC-3 (B — D72) | `tree_next_test.dart` — „AC-3 (B — D72)”: ⏭ na listwie zaraz za ▶; rok w rogu, pod nim nic (żadnego tekstu 28 sp); linia na listwie nad ▶ ⏭ „W 1868 … Urodził się Antoni Wymyślony”, 14 sp, czytnik „W 1868. Urodził się Antoni Wymyślony”; po 5 s linia znika z listwą, rok i świecenie zostają; pusty dotyk — listwa z tą samą linią; z powrotem na telefonie dymek |
| D73 | „D73 — after ⏭ the people of the page glow”: 1868 — pierścień Antoniego, jedna poświata, szczyt pulsu 0,65 po 0,6 s, po 4 s stała 0,30 i **żadnej animacji** (SC 2.2.2); 1946 — Helena i Józef z pierścieniem, dwie poświaty, linia pary (jeden odcinek); po suwaku — nic nie świeci |
| D73 (oddalenie) | „zoomed out”: przy skali 0,5 zasięg poświaty × 2 (stała wielkość na ekranie, I2) |
| D75, SC 2.3.3 | „with the system's animations off”: 0,30 od razu i po 0,6 s, pierścień jest |
| AC-2, D30 | „AC-2” na mapie: warstwa poświaty mapy z osobami i w pulsie (> 0,45); `migration_year_test.dart` — „D30 — whose each line is”: osoby linii w jej kolejności, rok bez przeprowadzki — pusto |

**Przegląd `ui` rundy 2** (subagent bez historii; 14 zrzutów `r2-*`, kod, `theme.dart`): **bez MAJOR.**
- **MINOR — poświata na mapie jako cień w każdym okręgu**, przerysowywany w każdej klatce pulsu, wbrew [[style-b]] regule 2 v1.48 („jedna warstwa”): **poprawione** (wyżej, z pomiarem).
- **MINOR — specyfikacja mapy: kontrast pierścienia** „8,81:1 na lądzie” → 8,04:1 (ląd ma kolor powierzchni): poprawione przez `ui` w [[mapa-migracji]].
- Odstępstwa `dev` rundy 2 (przód stosu, podjazd przy wejściu w tryb prezentacji, gradient) — w specyfikacjach (v1.28, v1.6) zgodnie z kodem.
- Zgodne: elementy i stany 6a, 11, 13, 15; puls (0,3 s do 0,30, szczyty 0,65 co 1,2 s, koniec 3,6 s bez skoku); SC 2.2.2, 2.3.1 (mniej niż 3 na sekundę, mała powierzchnia), 2.3.3;
  kontrasty — linia na listwie 10,02 / 5,01, pierścień 8,81 na tle i 8,04 na lądzie, wyróżnienie ≥ 3:1 w każdej chwili pulsu; linia podpisu bez akcji, cele ▶ ⏭ − + 48 dp; region na żywo;
  reguła 6 przy 200%; V2 w trybie prezentacji zgodne z D63; na zrzutach tylko wymyślone osoby.
- **Uwagi bez poprawki:** (a) osoba w środku po pulsie (pierścień i poświata 0,35) różni się od osób z podpisu tylko siłą poświaty — do obserwacji na stopie #2; (b) przy „Razem” ciągła linia
  pary przykrywa przerywaną linię „razem”, dopóki stoi podpis (jak ścieżka, element 8; słowo „Razem:” jest w podpisie); (c) dymek 1955 przy 200% na telefonie zakrywa świecące osoby (runda 1,
  D66); (d) tryb prezentacji przy 200% na 360 dp — między rokiem a listwą ok. 19 dp, rząd tuż nad listwą (D72 → *Nie da*).

**Family data:** zmiany rundy 2 w kodzie, testach i vaulcie bez danych rodziny — przykłady z rdzeni Wymyśl-, Zmyśl-, Testow-, Przykład-; nazwa prawdziwego miasta z bazy demo emulatora,
przepisana z podpisu mapy do *Dev report* i D30, **usunięta przed `git add`** (zostaje „przeprowadzka z Litwy”, kraj z wymyślonych danych `lib/dev`). Bez plików `*.db`, kopii, eksportów,
zdjęć. Pozycja bez sieci.

### Stop #2 — runda 2 (2026-10-19, autor na emulatorze)
Kroki: (1) drzewo, ⏭ do ślubu — świecenie, puls, linia pary, osoba w środku a osoby zdarzenia; (2) tryb prezentacji, ⏭ na listwie — linia jako ściąga, po 5 s sam rok i świecące
osoby; (3) mapa w trybie prezentacji, ⏭ — świecący awatar. **Odpowiedź autora: *„ok”*.** Ślad na urządzeniu: po restarcie aplikacja stała na mapie cmentarzy, po „ok” — tryb prezentacji
(ekran poziomo), część „Mapa”, rok „dziś” (`uiautomator`, zrzut `r2-after-ok`). Uwaga (a) z przeglądu (osoba w środku a osoby zdarzenia) — bez zgłoszenia.

**Werdykt (`self-check`): APPROVED, z uwagami** — AC-1–AC-4 mają testy (AC-3 po decyzji autora „B”: z kanapy rok i świecenie, słowa na listwie dla autora); przegląd `ui` runda 1:
1 MAJOR i 1 MINOR poprawione, runda 2: 0 MAJOR, 1 MINOR poprawiony (z pomiarem); uwagi bez poprawki (a)–(d) wyżej; stop #2 runda 2 — „ok” ze śladem. Szukałem i nie znalazłem: tekstu pod
rokiem w trybie prezentacji, ruchu po 4 s od ⏭, klatek po pulsie, przycisku bez akcji dotknięcia, danych rodziny w zmianach (poza nazwą miasta, usuniętą przed `git add`). Do listy B
w [[ISSUE-032-mvp-install]] → *Hand checks* (`docs`): trzy wiersze niżej.

### For ISSUE-032 → Hand checks
- **B** — z kanapy na Twoim telewizorze po ⏭: czy widać, kogo dotyczy zdarzenie (pierścień, poświata za wieńcem, linia pary przy ślubie) i czy rok 36 sp wystarcza, a słowa mówisz Ty
  (runda 2, D72–D73; do rundy 1 tu był podpis 28 sp pod rokiem).
- **B** — ⏭ na telefonie z obrazem na telewizorze: płynność podjazdu drzewa do osób z podpisu, pulsu poświaty (3,6 s) i pojedyncze wolne klatki przy zmianie roku (na emulatorze 130–175 ms,
  tak samo przy ▶ w buildzie sprzed pozycji; puls na emulatorze bez zmiany kosztu klatki).
- **B** — TalkBack: po ⏭ słychać rok i zdarzenia („W 1868. Urodził się …”) — na telefonie i w trybie prezentacji.
