---
title: "ISSUE-024 — Person view (M5): cover photo, portrait, mini family tree, chain to me, dates, burial → cemetery map"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-12
verdict-reviewer: self-check
source: "[[SPIKE-004-mvp-flow-prototype]] D4, D13–D19, D24, D27, D28 (decyzje autora na prototypie, 2026-10-08)"
created: 2026-10-08
updated: 2026-10-12
---

# ISSUE-024 — Widok osoby

> Z zamknięcia [[SPIKE-004-mvp-flow-prototype]]. Nowy ekran (widok 4, M5, R4 prawy). Specyfikacja: [[osoba]] v1.3,
> [[grob]] v5, [[wpis-osoby]] v5.3, [[style-b]] reguła 15. Wymaga [[ISSUE-025-gender-kinship-together-since]] (płeć — zrobione)
> i [[ISSUE-022-app-skeleton-tabs-people-settings]] (pasek, „ja”). **Od zamknięcia ISSUE-025 ta pozycja buduje też słownik
> nazw pokrewieństwa i ścieżkę do „ja”** (decyzja autora na stopie #1 ISSUE-025, R2-D3 — *Input from ISSUE-025* niżej).

## What to build
- **Widok osoby** ([[osoba]] elementy 1–10): zdjęcie w tle, portret na jego krawędzi, imię, lata, „kim była”, **Rodzina
  jako mini-drzewo** (rodzice, partnerzy, dzieci), **„Jak łączy się ze mną”** (nazwa pokrewieństwa i łańcuch od „ja”),
  daty, **pochówek → mapa cmentarza z zaznaczoną pinezką** (bez pinezki — lista z zaznaczonym grobem), zdjęcia; ✎ →
  formularz poprawy.
- **Widok przed poprawą** ([[style-b]] reguła 15): karta osoby w [[grob]] i chipy krewnych prowadzą do widoku osoby, nie
  do formularza.
- **Zdjęcie w tle** (D17): „Ustaw jako tło” w podglądzie zdjęcia osoby. **Zmiana schematu:** wskazanie tła przy łączu
  osoba–zdjęcie (jak profilowe, [[ADR-009-person-photos-record-and-link]]), migracja z testem.
- **Bez źródeł na ekranie** (D28): daty bez „· notatki”, bez statusów.

## Acceptance Criteria
- **AC-1** *When* dotykam osoby w grobie *Then* otwiera się widok osoby, a nie formularz; ✎ otwiera poprawę.
- **AC-2** *Given* osoba z rodzicami, partnerem i dziećmi *Then* mini-drzewo pokazuje ich z nazwami („Matka”, „Mąż”,
  „Córka”), a dotknięcie przenosi do widoku krewnego.
- **AC-3** *(brzmienie ze stopu #1, runda 1 — decyzja autora)* *Given* ustawione „ja” i ścieżka do osoby *Then* widać łańcuch
  od „Ja” z imionami i relacją każdego kroku: Ja → Mama Anna → Jej mama Maria. ~~„Twoja babcia” i łańcuch Ja → Mama Anna → Babcia
  Maria~~.
- **AC-4** *(brzmienie ze stopu #1, D2 — do czasu mapy cmentarza)* *When* dotykam „Pochówek” *Then* otwiera się cmentarz tej
  osoby z jej grobem zaznaczonym na liście grobów (obrys w akcencie, lista przewinięta do grobu); mapa z pinezką — z
  [[US-007-mapa-cmentarza]]. ~~Mapa cmentarza z zaznaczoną pinezką tego grobu~~.
- **AC-5** *When* ustawiam zdjęcie jako tło *Then* widać je nad portretem; kopia sprzed zmiany odtwarza się bez tła.
- ~~**AC-6** (z ISSUE-025, dawne AC-2) *Given* ścieżka Ja → rodzic (mężczyzna) → jego rodzic → jego córka *Then* nazwa to
  „ciotka”; brat ojca — „stryj”, brat matki — „wuj”; dziecko siostry ojca — „brat/siostra cioteczna” (słownik ze źródłem).~~
  **→ drzewo** (decyzja autora na stopie #1, runda 1) — [[SPIKE-002-tree-on-a-phone]] → *Input from ISSUE-024*.

## Notes
- Mini-drzewo dzieli układ i kolory linii z [[drzewo]] (D3) — w tej pozycji tylko jeden poziom (rodzice, partnerzy,
  dzieci).

## Input from ISSUE-025 (2026-10-08, `docs` przy zamknięciu)
- **Słownik i ścieżka** („Jak łączy się ze mną”, [[osoba]] element 7): kanon zacytowany w [[ISSUE-025-gender-kinship-together-since]]
  → *Prior art* (SJPD przez Frąckiewicz 2013, SJP PWN, GEDCOM 7), a zakres nazw, nawias ze ścieżką, opis z odcinków w
  dopełniaczu i odcinki neutralne przy braku płci — tabela D2 w *Decisions for stop #1 — runda 0*. Reguły nawiasu i opisu
  neutralnego (dawne [[osoby]] D8, D9) przechodzą tu; lista Osoby pokrewieństwa nie pokazuje (decyzja autora, [[osoby]] v2.2).
- **Uwaga autora ze stopu #2 ISSUE-025:** *„po wybraniu osoby najpierw wejść w jej »profil« z najważniejszymi informacjami a
  dopiero potem w edycję (aby oglądanie danej osoby nie mieszało się z edycją tej osoby)”* — to AC-1 i reguła 15: także
  **karta partnera i chipy w sekcji „Rodzina”** ([[wpis-osoby]] 9a v5.6) mają prowadzić do widoku osoby, a nie do poprawy.
- **Karta partnera:** dziś inicjały (ISSUE-025, odstępstwo 1 przyjęte w przeglądzie `ui`) — tu profilowe, skoro widok i tak
  czyta zdjęcia; chevron przy karcie, gdy zacznie prowadzić do widoku osoby (przegląd `ui`, znalezisko 6).
- **Stare `⚠️ OPEN` w [[osoba]]** (3 — źródło przy relacjach, 4 — ustawienie „ja”) są rozstrzygnięte (SPIKE-004 D28,
  ISSUE-022) — `ui` sprząta je przed planem.

## Implementation plan
> `planning`, 2026-10-09. Specyfikacja (`ui`, przed planem): [[osoba]] v2 — oraz [[zdjecie]] v1.5, [[zdjecia-osoby]] v1.2,
> [[wpis-osoby]] v5.8, [[osoby]] v2.3, [[cmentarz]] v4.3, [[grob]], [[style-b]] v1.18. **Makieta** (10 ramek, warianty W1/W2):
> `issue-024-widok-osoby.html` w katalogu tymczasowym sesji `8adf85b2-…` (poza repo).

### Prior art
- **Słownik pokrewieństwa** — kanon zacytowany w [[ISSUE-025-gender-kinship-together-since]] → *Prior art* (SJPD przez
  Frąckiewicz 2013, SJP PWN) i tabela D2 (*Decisions for stop #1 — runda 0*): zakres nazw, nawias, opis z odcinków, odcinki
  neutralne, wybór ścieżki. Ta pozycja go **wykonuje**, nie projektuje od nowa.
- **[GEDCOM 7.0](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html)** (odczyt kopii z 2026-10-07): `MULTIMEDIA_LINK`
  ma tylko `CROP` i `TITL` — **tła ani „okładki” standard nie zna**, więc wskazanie tła to rozszerzenie aplikacji, a jego eksport
  rozstrzyga [[US-006-eksport-dla-rodziny]]. Kolejność łączy (*„the first is the most-preferred value”*) dalej niesie
  profilowe ([[ADR-009-person-photos-record-and-link]]).
- **Z kodu** (ankieta 2026-10-09):
  - `applyPersonPhotoEdits` (`photos.dart`) **przepisuje łącza osoby od zera** i czyta kadry przed skasowaniem, żeby je oddać
    (plan F1 z ISSUE-018) — znacznik tła musi przejść tę samą drogę, inaczej zniknie przy każdym „Zapisz”;
  - zmiany zdjęć osoby żyją w `PersonPhotosDraft` i zapisują się w transakcji wpisu (`Photos.writeWithPersonPhotos`) — **W2 nie
    potrzebuje nowej drogi zapisu**, W1 — tak (*Decisions* D1);
  - drift 2.34.0 ma `@TableIndex.sql`, więc **częściowy unikalny indeks** „jedno tło na osobę” da się zapisać w schemacie;
  - `loadRelations` daje wszystko do mini-drzewa (rodzice, ich związek, związki osoby z partnerem, `married`, dzieci według
    urodzenia); ścieżki ani grafu całej rodziny w kodzie nie ma (drzewo to zaślepka);
  - jedno wejście do poprawy: `openPersonEntry` (`person_form_screen.dart`) — wołają je Osoby i sekcja „Rodzina”; grób ma własne
    `_correct`;
  - `Icons.conversion_path` nie istnieje we Flutterze 3.41.1 → `Icons.link` ([[osoba]] D18).

### Stop #1, runda 2 (2026-10-09) — autor: „jest dobrze”
- Runda 2 przyjęta (łańcuch po imionach z relacją kroku, pusta sekcja „Zdjęcia” z „Dodaj zdjęcie”, zakres bez słownika).
- **„Połączyć z istniejącymi” — osobna pozycja po ISSUE-024** (rekomendacja przyjęta): źródło „Ze zdjęć w aplikacji” i ekran
  wyboru spośród zdjęć wszystkich osób. Pozycję zakłada `docs` przy zamknięciu ISSUE-024 (`ui` → specyfikacja i makieta przed
  planem).

### Stop #1, runda 1 (2026-10-09) — decyzje autora
> Autor: *„1 W2 jest dobry; łączenie ze sobą tylko po imionach oraz relacje miedzy tymi osobami (mama, córka, brat, mąż itd -
> przypadki np. Brat stryjeczny prababki lub podobne zrobimy w widoku drzewa przy łączeniu różnych osób); chciałbym mieć dla
> osoby bez zdjęć również miejsce na »zdjęcia« abym wiedział że mogę tutaj je dodać na dole (lub połączyć z istniejącymi) /
> 2 ok / 3 ok / 4 ok”*.

- **D1 = W2.** Widok tylko pokazuje zdjęcia; zmiany zdjęć — z formularza.
- **D2, D3, D4 przyjęte** (AC-4 do czasu mapy, ADR-013 wariant A, „Pokaż w drzewie” ukryte).
- **„Jak łączy się ze mną” — łańcuch po imionach z relacją jednego kroku** ([[osoba]] v2.1, D13'): „Ja” · „Mama Anna” · „Jej mama
  Maria” (forma karty ścieżki z R3). Bez pierwszej linii „Twoja babcia” i bez słownika nazw złożonych. **AC-3 dostaje nowe
  brzmienie**: *Given ustawione „ja” i ścieżka do osoby Then widać łańcuch od „Ja” z imionami i relacją każdego kroku: Ja → Mama
  Anna → Jej mama Maria*. **AC-6 → drzewo** ([[drzewo]] D6, razem ze słownikiem z ISSUE-025 D2). Oba zapisuje `docs` przy
  zamknięciu; AC-6 trafia do [[SPIKE-002-tree-on-a-phone]] → *Input from ISSUE-024* (pozycji drzewa jeszcze nie ma).
- **Sekcja „Zdjęcia” także bez zdjęć** ([[osoba]] v2.1, D20): „Ta osoba nie ma jeszcze zdjęć.” + „Dodaj zdjęcie” → poprawa wpisu z
  arkuszem źródła nad nią → „Zapisz”. Zapis zdjęć zostaje jeden (W2). Makieta: ramki 2, 3 (runda 2).
- **⚠️ OPEN — „połączyć z istniejącymi”** ([[osoba]] *Open* 6): nowe źródło „Ze zdjęć w aplikacji” i nowy ekran wyboru spośród
  zdjęć wszystkich osób. To zmiana zakresu — pytanie na stopie #1, runda 2. Rekomendacja: **osobna pozycja po ISSUE-024**.

Specyfikacje po rundzie 1: [[osoba]] v2.1, [[drzewo]] (D6 — słownik i dawne AC-6), [[zdjecie]] v1.5 (A z widoku, tryb
oglądania), [[zdjecia-osoby]] v1.2, [[wpis-osoby]] v5.8.

### Decisions for stop #1 — runda 0 (zapis; D1 = W2, D2–D4 przyjęte, D13 zastąpione przez D13')
- **D1 — zdjęcia w widoku: W2 czy W1** ([[osoba]] *Open* 1; makieta, ramki 2, 3, 9). **W2 (rekomendacja):** widok tylko pokazuje
  zdjęcia; bez tła — bez pasma, bez zdjęcia — okrąg z inicjałami; podgląd i baza z widoku w trybie oglądania. Tło, profilowe i
  nowe zdjęcia — pod ✎, zapis z „Zapisz” jak dziś. Koszt: flaga „tylko do oglądania” w dwóch ekranach zdjęć. **W1:** „Dodaj
  zdjęcie w tle” i „Dodaj zdjęcie” w widoku, zmiany zapisują się po powrocie do widoku. Koszt: **druga droga zapisu zdjęć
  osoby** poza formularzem (przeniesienie plików, transakcja, blokada danych przy kopii) i więcej stanów do testów. Za W2 Twoja
  uwaga ze stopu #2 ISSUE-025 („oglądanie nie miesza się z edycją”); za W1 — tło w 3 dotknięciach zamiast 6.
- **D2 — AC-4 do czasu mapy cmentarza** ([[osoba]] D17; makieta, ramka 6). Mapy ([[US-007-mapa-cmentarza]]) i pinezek
  ([[US-008-pinezka-na-miejscu]]) jeszcze nie ma, więc nowe brzmienie: *When dotykam „Pochówek” Then otwiera się cmentarz tej
  osoby z jej grobem zaznaczonym na liście grobów (obrys w akcencie, lista przewinięta do grobu); mapa z pinezką — z US-007.*
  Zapisuje `docs` przy zamknięciu. *Inaczej:* do czasu mapy „Pochówek” → od razu [[grob]] (jedno dotknięcie mniej).
- **D3 — ADR-013 „Tło osoby — znacznik przy łączu osoba–zdjęcie (schemat v8)”** (pisze łańcuch, `docs` przy zamknięciu):
  - **A (rekomendacja):** kolumna `is_background` przy łączu (`person_media`) + częściowy unikalny indeks „jedno tło na osobę”.
    Usunięcie łącza (z „Usuń z tej osoby” albo z „Kto jest na zdjęciu?”) samo zdejmuje tło; wzór jak kadr przy łączu
    ([[ADR-010-profile-photo-crop-pixels]]);
  - **B:** `persons.background_media_id` → `media`. Przeżywa przepisanie łączy bez pracy, ale przy usunięciu łącza trzeba je
    czyścić osobno, a klucz do `media` blokuje sprzątanie wiersza zdjęcia bez łączy;
  - **C:** osobna tabela „tło osoby”. Jak B, z jedną tabelą więcej w kopii i w liczeniu wierszy przy odtworzeniu.

  A **nie zastępuje** ADR-009 ani ADR-010 (dokłada kolumnę, jak ADR-010 dołożył kadr) — sygnał dla `architect` się nie zapala.
- **D4 — „Pokaż w drzewie” ukryte**, dopóki Drzewo jest zaślepką ([[osoba]] D11).
- **Decyzje projektowe ze specyfikacji** (do potwierdzenia tym samym „tak”): mini-drzewo — dwa związki po obu stronach, dzieci
  pod swoim związkiem, przewijanie w bok, etykiety 13 sp (D12; ramka 4); pierwsza linia „Jak łączy się ze mną” z zaimkiem przy
  odcinku najbliższym Ciebie (D13; ramka 5); chipy i karta partnera w formularzu → widok (D14; ramka 10); jedna poprawa osoby
  naraz (D15); „kim była” w całości (D16); podgląd zdjęcia z trzema działaniami i „Usuń z tła” (ramki 7, 8).
- *Obali „jedną pozycję”:* plan nie mieści się w jednej sesji `dev` — wtedy „Jak łączy się ze mną” (słownik, ścieżka, AC-3,
  AC-6) jako ISSUE-026, a tu widok, mini-drzewo, tło i wejścia.

### Scope — files (`{code}`)
| Plik | Co |
|---|---|
| `lib/data/database.dart` | `PersonMedia.isBackground` — `boolean().withDefault(const Constant(false))()`; `@TableIndex.sql` — częściowy unikalny indeks na `person_id` przy `is_background`. **Schemat v8**, krok `_from7To8`: `addColumn` + `createIndex` — żadnego wiersza nie dodaje (odtworzenie liczy wiersze, `restore_service.dart` → `_migrate`). Komentarz tabeli: tło jako rozszerzenie (GEDCOM 7 go nie zna) |
| `drift_schemas/grobing/drift_schema_v8.json`, `database.steps.dart`, `test/drift/grobing/generated/*` | `dart run drift_dev make-migrations` (README → *Baza danych*) |
| `lib/data/photos.dart` | `PersonPhoto.isBackground`; `backgroundPhotos(db, ids)` (jak `profilePhotos`); `PersonPhotoEdits.background` — **jak kadry**: tło zapisanego łącza, którego edycja nie dotyka, czytane przed przepisaniem i oddawane; jawne „ustaw na X” albo „bez tła”; łącze usunięte w edycji traci tło razem z sobą |
| `lib/app/photo/person_photos_draft.dart` | stan tła w szkicu: `background`, `setBackground(photo)`, `clearBackground()`; `remove` zdejmuje tło usuwanego zdjęcia; `hasChanges` widzi zmianę tła |
| `lib/app/photo/person_photo_viewer_screen.dart` | [[zdjecie]] B4'': trzy kolumny, ikona nad napisem; „Ustaw jako tło” (`wallpaper_outlined`) ↔ „Usuń z tła” (`hide_image_outlined`); podtytuł „Zdjęcie w tle” / „Zdjęcie profilowe i tło”; `RemovePersonPhotoDialog` — zdanie „Osoba zostanie bez zdjęcia w tle.”; **W2:** `readOnly` — bez B4'' i bez „Zmień” w B5 |
| `lib/app/photo/person_photos_screen.dart` | **W2:** `readOnly` — bez kafelka „Dodaj zdjęcie” i linii zapisu; opis komórki z „tło” ([[zdjecia-osoby]] v1.2) |
| `lib/data/person_view.dart` (nowy) | odczyt widoku: osoba (imiona, nazwisko, rodowe, płeć, „kim była”, żyjąca), urodzenie i zgon (pierwsza wartość), profilowe z kadrem, tło, liczba zdjęć i 4 pierwsze, pochówek (grób: tytuł, kwatera, rząd, miejsce, `id`; cmentarz: nazwa, `id`), relacje (`loadRelations`) z profilowymi krewnych, „ja”; `watchPersonView` przez `watchTables` (widok odświeża się po „Zapisz”) |
| `lib/data/kinship.dart` (nowy) | graf całej rodziny (osoby z płcią; rodziny: partnerzy, dzieci, `married`) i **ścieżka od „ja”**: krawędzie R, D, B (dzieci tej samej rodziny), P; najkrótsza, przy równej — mniej P, dalej stała kolejność `id` (ISSUE-025 D2); bez ścieżki — `null` |
| `lib/app/person/kinship_names.dart` (nowy) | **podpisy łańcucha** ([[osoba]] 7, D13', runda 1): relacja jednego kroku z płci osoby w wierszu — mama / tata, córka / syn, siostra / brat, żona / mąż (małżeństwo), partnerka / partner („razem”); bez płci — rodzic, dziecko, rodzeństwo, partner; zaimek „jej” / „jego” z rodzaju gramatycznego relacji w wierszu wyżej (rodzic, dziecko, rodzeństwo → „jego”); pierwszy krok bez zaimka. Czysta funkcja — testy jednostkowe. **Bez słownika nazw złożonych** (→ [[drzewo]]) |
| `lib/app/person/person_screen.dart` (nowy) | [[osoba]] elementy 1–10 i stany; pasek dolny z zakładką, z której przyszedł; `openPersonView(context, db, personId, photos:)` — **jedna funkcja wejścia**; pusta sekcja „Zdjęcia” z „Dodaj zdjęcie” → `openPersonEntry` z otwartym od razu arkuszem źródła (D20) |
| `lib/app/person/mini_tree.dart` (nowy) | układ (czysta funkcja: rzędy, miejsca 80 dp, dwa związki po bokach, grupy dzieci rozsunięte — [[osoba]] 6, D12) + linie (`CustomPainter`: kolor relacji, ciągła / przerywana 5/4) + węzły-przyciski z opisem dla czytnika; przewijanie w bok z osobą na środku |
| `lib/app/grave/grave_screen.dart` | karta osoby → `openPersonView` (zamiast `_correct`) |
| `lib/app/people/people_screen.dart` | karta osoby i karta „Ja” po wyborze → `openPersonView` |
| `lib/app/family/family_section.dart` | chipy i karta partnera → `openPersonView`; karta partnera: profilowe 40 dp w kadrze (bez zdjęcia — inicjały), chevron, opis „… — otwórz” ([[wpis-osoby]] v5.8) |
| `lib/app/grave/person_form_screen.dart` | `openPersonEntry` zostaje jako cel ✎ w widoku; parametr „otwórz arkusz źródła zdjęć od razu” dla „Dodaj zdjęcie” z widoku (D20 — ta sama droga co element 1a bez zdjęć); **D15**: poprawa osoby, której formularz już leży w stosie, wraca do niego (`popUntil` po nazwie trasy z `id` osoby) zamiast otwierać drugi |
| `lib/app/grave/cemetery_screen.dart` | `highlightGraveId`: lista przewinięta do karty (`Scrollable.ensureVisible`), karta z obrysem 2 dp w akcencie i `selected` dla czytnika ([[cmentarz]] v4.3) |
| `lib/app/theme.dart` | `GrobingColors.relParentChild` `#8FB3C9`, `GrobingColors.relPartners` `#D39BB0` ([[style-b]] v1.16; pomiar 8,50 i 8,16:1 na tle) |
| `README.md` (`grobing-code`) | *Baza danych*: wpis v8 (tło przy łączu, indeks) |

Bez zmian: `restore_service.dart` (liczy wiersze — v8 ich nie dodaje), zakładka Drzewo (zaślepka), lista Osoby poza wejściem,
`photo_people_screen.dart` (odznaczenie osoby usuwa łącze, a tło znika z nim w `applyPersonPhotoEdits`).

### AC → implementation → test (testy pisze `qa`)
| AC | Gdzie | Test happy-path |
|---|---|---|
| AC-1 | `grave_screen.dart`, `person_screen.dart`, `person_form_screen.dart` | widżet: karta osoby w grobie → widok (imię, lata), nie formularz; ✎ → „Poprawa wpisu”; „Zapisz” → widok z nowym imieniem |
| AC-2 | `mini_tree.dart`, `person_screen.dart` | jednostkowy układu: rodzice nad osobą, mąż po prawej, dzieci pod związkiem; dwa związki — po bokach, grupy dzieci rozłączne; widżet: „Matka”, „Mąż”, „Córka” z płci, neutralne bez płci; węzeł → widok krewnego, wstecz → poprzednia osoba |
| AC-3 (runda 1) | `kinship.dart`, `kinship_names.dart`, `person_screen.dart` | jednostkowy: ścieżka Ja → mama → jej matka = „Ja”, „Mama Anna”, „Jej mama Maria”; przez żonę — „Żona Kasia”, „Jej tata Marek”, „Jego siostra Ewa”; osoba bez płci — „Jego rodzic Aleksander”, „Jego córka Zofia”; przyrodnie — „Tata Jan”, „Jego syn Piotr”; najkrótsza ścieżka, przy równej mniej „para”; widżet: sekcja z łańcuchem; bez ścieżki i bez „ja” — teksty z [[osoba]] 7; dla „ja” sekcji nie ma |
| AC-4 (D2) | `person_screen.dart`, `cemetery_screen.dart` | widżet: „Pochówek” → cmentarz z zaznaczonym grobem (`selected`, obrys), wstecz → widok; osoba bez pochówku — bez wiersza |
| AC-5 | `database.dart` (v8), `photos.dart`, szkic, podgląd, `person_screen.dart` | danych: „ustaw jako tło” → `is_background` na jednym łączu; drugie ustawienie przenosi tło; zmiana kolejności i kadru nie gubi tła; usunięcie łącza je zdejmuje; indeks odrzuca drugie tło; migracja v7→v8 na danych (`testWithDataIntegrity`): wiersze bez zmian, wszystkie `false`; **odtworzenie kopii v7 w v8 — bez tła**, liczniki zgodne; widżet: tło nad portretem po „Zapisz” |
| ~~AC-6~~ → [[drzewo]] (runda 1) | — | — |
| D20 (runda 1) | `person_screen.dart`, `person_form_screen.dart` | widżet: osoba bez zdjęć — „Ta osoba nie ma jeszcze zdjęć.” i „Dodaj zdjęcie”; dotknięcie → „Poprawa wpisu” z arkuszem „Zdjęcia osoby”; zdjęcie z (atrapy) galerii → „Zapisz” → widok z portretem i „Zdjęcia · 1” |
| *Input from ISSUE-025* | `family_section.dart`, `people_screen.dart` | widżet: chip „Syn: Stanisław” w formularzu → widok Stanisława, wstecz → formularz z wpisanymi danymi; karta osoby w Osobach → widok; D15 — ✎ osoby, której poprawa leży niżej, wraca do niej |

Testy do przepisania (zachowanie się zmienia, a zamknięte pozycje muszą zostać zielone): w `grave_screens_test.dart`,
`skeleton_test.dart` (karta w Osobach) i `family_screens_test.dart` scenariusze „karta / chip → poprawa” przechodzą na „→ widok → ✎ →
poprawa”; `database_test.dart`, `data_state_screen_test.dart` (wersja 7 → 8); `person_photos_screens_test.dart` (układ trzech działań).

### Data layer
- **Schemat v8** z testem migracji v7→v8 na danych (NFR-003) i plikiem schematu z `make-migrations`.
- **Próbne odtworzenie:** test kopii v7 → v8 (bez tła, AC-5) i kopii v8 z tłem (odcisk zgodny). Na emulatorze: kopia z
  `Medium_Phone` z nowym hasłem testowym → `Grobing_Restore` (agent).
- **Źródło i status faktu:** ta pozycja **nie zapisuje faktów o rodzinie** — tło to wybór zdjęcia, nie fakt (bez twierdzenia,
  jak profilowe i kadr); ścieżka i nazwy pokrewieństwa są liczone, nie zapisywane ([[data-model]]).
- **ADR-013** (D3), wpis v8 w [[data-model]], nowe brzmienie AC-4 (D2) → `docs` przy zamknięciu.

### Manual verification
**Agent na emulatorze** (`Medium_Phone`, build release jako aktualizacja na danych testowych v7), zrzuty przed stopem #2:
1. Po aktualizacji: dane całe, `user_version` 8, `person_media.is_background` wszędzie 0.
2. Wejścia: karta osoby w grobie, karta w Osobach, karta „Ja” → widok (dla „ja” bez sekcji 7); chip i karta partnera w
   formularzu → widok, wstecz → formularz z wpisanymi danymi; ✎ → poprawa → „Zapisz” → widok z nową wartością; D15 (żona → mąż →
   żona → ✎ wraca do pierwszej poprawy).
3. Mini-drzewo: rodzice, partner, dzieci z nazwami ról; węzeł → krewny; osoba z dwoma związkami i kilkorgiem dzieci — przewijanie
   w bok, przerywana linia przy „razem”.
4. „Jak łączy się ze mną”: babcia (Ja → Mama → Jej mama), krewny z boku (Jej brat), droga przez żonę, osoba bez ścieżki.
5. „Pochówek” → lista grobów przewinięta do zaznaczonego grobu; wstecz → widok.
6. Tło (W2, przez ✎): ustawienie, „Usuń z tła”, usunięcie zdjęcia, które jest tłem (zdanie w oknie); kadr i kolejność po zmianie
   tła bez zmian. Z widoku zdjęcia tylko do oglądania (bez kafelka, bez działań); osoba bez zdjęć — „Dodaj zdjęcie” → poprawa z
   arkuszem → „Zapisz” → widok z portretem.
7. `uiautomator`: węzły mini-drzewa i wiersze łańcucha `clickable` z opisem; zaznaczona karta grobu `selected`; tekst 200% — nic
   nie ucięte poza imieniem w węźle („…”).
8. Próbne odtworzenie na `Grobing_Restore`: odcisk zgodny, tło to samo.

**Autor: odczucie** (najwyżej 3):
1. Otwórz osobę z grobu i przejdź po rodzinie mini-drzewem (rodzic → dziecko → wstecz): czy widok mówi, kim była i z kim.
2. „Jak łączy się ze mną” przy dziadku albo babci i przy kimś z boku: czy łańcuch z imionami mówi jasno, jak się łączycie.
3. Ustaw komuś zdjęcie w tle: czy droga jest do przyjęcia, a tło z portretem wygląda dobrze.

Przegląd ekranów `ui` (subagent `qa`) przed stopem #2; nowy ekran → `dev` przechodzi AC na emulatorze przed `qa` (retro 2, R5).

### Out of Scope
- **Mapa cmentarza i pinezka grobu** w AC-4, komunikat „Ten grób nie ma jeszcze pinezki” → [[US-007-mapa-cmentarza]],
  [[US-008-pinezka-na-miejscu]] ([[osoba]] D9).
- **„Pokaż w drzewie”**, pokrewieństwo w karcie i banerze drzewa → pozycja drzewa ([[SPIKE-002-tree-on-a-phone]]).
- **Nazwy złożone** („babcia”, „stryj”, „siostra cioteczna babci żony”), słownik z ISSUE-025 D2 i **dawne AC-6** → drzewo przy
  łączeniu dwóch osób ([[drzewo]] D6; decyzja autora na stopie #1, runda 1). Ścieżka (`kinship.dart`) z tej pozycji zostaje do
  użycia.
- **„Połączyć z istniejącymi”** (zdjęcie, które już jest w aplikacji, od strony osoby) — czeka na decyzję autora w rundzie 2
  ([[osoba]] *Open* 6); dziś działa od strony zdjęcia („Na zdjęciu · Zmień”).
- Eksport tła do GEDCOM → [[US-006-eksport-dla-rodziny]].
- Zapis zdjęć z widoku osoby (W1 — odrzucony na stopie #1).
- Twarde spacje w nazwach ([[style-b]] reguła 6 — osobna drobna pozycja); kontrola cykli w rodzinie; płeć z odpowiedzi
  „mama”/„tata” w kreatorze rodziców ([[ADR-012-person-sex-and-union-timeline]] → *Follow-ups*).
- Ojczym, pasierb, rodzeństwo przyrodnie — w łańcuchu jako kroki („Tata Jan” → „Jego syn Piotr”), nazwy — z drzewem.

## Dev report
> `dev`, 2026-10-09. Stop #1, runda 2: „jest dobrze”. Flutter 3.41.1 zgodny z przypiętym. `dart format` i `flutter analyze`
> czyste (cały projekt z testami). Testów nie pisałem (`qa`).

### What was built (`{code}`)
| Plik | Co |
|---|---|
| `lib/data/database.dart` | `PersonMedia.isBackground` (`boolean`, domyślnie `false`) + `@TableIndex.sql` `person_media_background` — częściowy indeks unikalny na `person_id` `WHERE is_background`. **Schemat v8**, krok `_from7To8`: `addColumn` + `createIndex`, bez nowych wierszy |
| `drift_schemas/grobing/drift_schema_v8.json`, `database.steps.dart`, `database.g.dart`, `test/drift/grobing/generated/schema.dart`, `schema_v8.dart` | `build_runner` + `drift_dev make-migrations` |
| `lib/data/photos.dart` | `PersonPhoto.isBackground`; `PersonPhotoEdits.backgroundChanged` + `background`; `applyPersonPhotoEdits` czyta tło przed przepisaniem łączy i oddaje je (jak kadr), jawna zmiana ustawia albo zdejmuje; łącze usunięte nie dostaje tła |
| `lib/app/photo/person_photos_draft.dart` | `background`, `isBackground`, `setBackground`, `clearBackground`; `remove` zdejmuje tło usuwanego zdjęcia; `hasChanges` i `edits()` widzą tło |
| `lib/app/photo/person_photo_viewer_screen.dart` | B4'': trzy kolumny, ikona nad napisem (`_StackedAction`, cel ≥ 48 × 64 dp); „Ustaw jako tło” (`wallpaper_outlined` w akcencie, napis w kolorze tekstu) ↔ „Usuń z tła” (`hide_image_outlined`, kolor tekstu); podtytuł „Zdjęcie w tle” / „Zdjęcie profilowe i tło”; okno C1' — „Osoba zostanie bez zdjęcia w tle.”; `readOnly` — bez B4'' i bez „Zmień” |
| `lib/app/photo/person_photos_screen.dart` | `readOnly` — bez kafelka „Dodaj zdjęcie” i linii zapisu; opis komórki „…, profilowe, tło — otwórz” |
| `lib/data/kinship.dart` (nowy) | `KinGraph` (z rodzin: partnerzy, dzieci, ślub) i `path(from, to)`: wszerz, najmniej kroków → najmniej „para” → najniższe `id` po kolei; krawędzie rodzic, dziecko, rodzeństwo (dzieci tej samej rodziny), para |
| `lib/data/person_view.dart` (nowy) | `PersonView` i `watchPersonView` (przez `watchTables`, odświeża się po każdym zapisie): osoba, daty, profilowe, tło, zdjęcia (liczba i 4 pierwsze), pochówek (`BurialPlace`), relacje, profilowe krewnych, „ja”, łańcuch (`ChainLink`) |
| `lib/app/person/kinship_names.dart` (nowy) | `stepWord` (relacja jednego kroku z płci) i `chainLabels` („Mama Anna”, „Jej mama Maria”); zaimek z rodzaju gramatycznego słowa w wierszu wyżej |
| `lib/app/person/mini_tree.dart` (nowy) | `layoutMiniTree` (czysta funkcja, [[osoba]] 6, D12) + `MiniTree` (przewijanie w bok z osobą na środku, linie `CustomPainter` — kolor relacji, przerywana 5/4 przy „razem”) |
| `lib/app/person/person_screen.dart` (nowy) | widok osoby, elementy 1–10, stany; `openPersonView` — jedno wejście |
| `lib/app/family/role_names.dart` (nowy) | `roleName` / `FamilyRole` przeniesione z `family_section.dart` — jedna lista ról dla formularza i mini-drzewa |
| `lib/app/family/family_section.dart` | chipy i karta partnera → `openPersonView`; karta partnera: profilowe 40 dp w kadrze (bez zdjęcia — `InitialsCircle`), chevron; opisy „… — otwórz”; strumień z profilowymi partnerów (czyta też `person_media`, `media`); `tab` |
| `lib/app/grave/person_form_screen.dart` | `openPersonEntry(tab, pickPhotosAtStart)`; **D15**: trasa `/correction/<id>` i rejestr otwartych poprawek — poprawa osoby, która już leży w stosie, wraca do niej (`popUntil`); `pickPhotosAtStart` otwiera arkusz zdjęć po wczytaniu szkicu (D20); `tab` dalej do sekcji „Rodzina” i do grobu po nowym grobie |
| `lib/app/grave/grave_screen.dart` | karta osoby → `openPersonView`; `tab` (pasek, formularz) |
| `lib/app/grave/cemetery_screen.dart` | `highlightGraveId`: karta z obrysem 2 dp w akcencie i `selected`, lista przewinięta do niej (`Scrollable.ensureVisible`); `tab` |
| `lib/app/people/people_screen.dart` | karta osoby i „Ja” → `openPersonView(tab: AppTab.people)` |
| `lib/app/theme.dart` | `relParentChild` `#8FB3C9`, `relPartners` `#D39BB0` |
| `README.md` | *Baza danych*: wpis v8 |

### Deviations (do przeglądu `ui`)
1. **`tab` przez cmentarz, grób i formularz** — plan wymieniał tylko widok osoby; [[osoby]] → *Navigation* mówi, że zakładka Osoby zostaje
   aktywna na całym stosie (osoba → cmentarz → grób), a cmentarz i grób miały „Mapa” na sztywno. Domyślnie `AppTab.map`, jak dotąd.
2. **Bez `backgroundPhotos(db, ids)`** z planu — widok czyta tło z `personPhotos` (jedna osoba), funkcja na wiele osób nie miała użytkownika.
3. **Neutralne nazwy w łańcuchu** według [[osoba]] 7: „rodzeństwo”, „partner” (także przy małżeństwie bez płci), a mini-drzewo — według
   [[rodzina]] *Role names*: „Małżonek”. Na emulatorze: „Rodzeństwo Ewa” (osoba sprzed v7, bez płci).
4. **Lista cmentarza z zaznaczonym grobem buduje wszystkie karty** (`cacheExtent`), żeby dało się przewinąć do grobu daleko na liście; bez
   zaznaczenia — jak dotąd.
5. **Portret bez czytelnego pliku** — kwadrat z `broken_image_outlined` w okręgu (jak w [[grob]]); tło bez pliku — pasmo na powierzchni z tą
   samą ikoną.
6. **Wiersz łańcucha ≥ 48 dp, linia 12 dp między wierszami** — spec mówiła wiersz ≥ 56 dp; cel dotyku ≥ 48 dp (próg Androida). Linia nie
   dotyka okręgów (4 dp przerwy nad i pod) — w R4 łączy je w całości.

### Found on the emulator (AC przed `qa`, R5)
`Medium_Phone`, build release jako aktualizacja na danych testowych v7 (Twoje dane z ISSUE-019…025): migracja przeszła, „Stan danych” —
wersja schematu 8.
- **Wiersze łańcucha zlewały się dla czytnika** w jeden węzeł („Ja / Rodzeństwo Ewa, otwórz”) — wiersz bez akcji nie był granicą
  semantyki. Poprawione (`container: true` we wszystkich nowych `Semantics`), sprawdzone `uiautomator`: „Ja, otwórz” i „Rodzeństwo Ewa” osobno.
- **„Dodaj zdjęcie” na całą szerokość** — wspólny styl drugorzędny ma `minimumSize: Size.fromHeight(52)`. Poprawione na szerokość treści.

Przeszło na emulatorze (zrzuty w katalogu tymczasowym sesji, `v1…v14`):
- AC-1 — karta Jana w grobie → widok Jana, nie formularz; ✎ → „Poprawa wpisu”;
- AC-2 — mini-drzewo Ewy: rodzice (ciągła — małżeństwo), Jan po lewej (przerywana — „razem”), Kuba po prawej („Mąż”), dzieci pod swoimi
  związkami; węzeł → widok krewnego;
- AC-3 — łańcuchy „Ja → Rodzic Stefan → Jego rodzic Jan”, „Ja → Żona Zofia”; dla „ja” sekcji nie ma;
- AC-4 — „Pochówek” → Cmentarz Powązkowski, „Grob wymyslonych” z obrysem w akcencie, `selected=true`; zakładka Osoby aktywna;
- AC-5 — ✎ → zdjęcia → podgląd → „Ustaw jako tło” (podtytuł „Zdjęcie profilowe i tło”, przycisk „Usuń z tła”) → „Zapisz” → widok z tłem;
- D20 — Zofia bez zdjęć: „Dodaj zdjęcie” → poprawa z arkuszem → zdjęcie z galerii → „Zapisz” → widok z portretem i „Zdjęcia · 1”;
- D15 — z poprawy Jana: karta Ewy → widok Ewy → węzeł „Jan” → ✎ wraca do tej samej poprawy Jana (ta sama pozycja przewinięcia);
- W2 — z widoku tło i „Zdjęcia” otwierają podgląd bez działań i bez „Zmień” i bazę bez kafelka.

**Zmiana danych testowych na `Medium_Phone`:** Zofia Testowa ma teraz zdjęcie z galerii emulatora (wymyślone) jako profilowe i tło.

### For `qa` — kroki ręczne
Kroki agenta i autora — *Manual verification* wyżej (z rundy 1). Do tego:
- **testy do przepisania** (zachowanie się zmienia): `grave_screens_test.dart` (karta osoby → widok, nie poprawa), `skeleton_test.dart`
  (karta w Osobach → widok), `family_screens_test.dart` (chip i karta partnera → widok; karta z chevronem), `person_photos_screens_test.dart`
  (trzy kolumny działań), `database_test.dart` i `data_state_screen_test.dart` (wersja 8); test migracji v7→v8 na danych w
  `test/drift/grobing/` (pliki pomocnicze schematu v8 wygenerowane);
- **niesprawdzone przeze mnie:** tekst 200% w mini-drzewie i łańcuchu, TalkBack na żywo, „Usuń z tła” i okno usunięcia zdjęcia, które jest
  tłem, próbne odtworzenie kopii v8 z tłem na `Grobing_Restore`.

### After `qa` and the `ui` review (`dev`, 2026-10-09)
- **Podpisy węzła mini-drzewa przepełniały swoje pudełko o 0,2 px** (złapał to test `family_screens_test.dart` — wyjątek
  renderowania): wysokość dwóch linii liczona bez zapasu na metryki fontu → +4 dp.
- **Przegląd `ui`, MAJOR:** pierścień w akcencie rysuje się nad zdjęciem (`DecorationPosition.foreground`) — portret, osoba w
  środku mini-drzewa, okręgi łańcucha; przy tekście 200% miejsce węzła rośnie ze skalą (do 160 dp, rozstaw rodziców w tej samej
  proporcji), więc rola nie jest ucinana; etykiety „Daty” idą nad wartość, gdy nie mieszczą się w 96 dp (kolumna wierszy dat
  na pełną szerokość — inaczej stały na środku, znalezione na emulatorze).
- **Przegląd `ui`, MINOR:** linia łańcucha przez okręgi bez przerw (`IntrinsicHeight`, odcinek nad i pod okręgiem); inicjały w
  `InitialsCircle` rosną najwyżej 1,3× (komponent wspólny — także lista Osoby i grób); chevron karty partnera otwiera widok
  partnera; „małżonek” w łańcuchu przy małżeństwie bez płci; w oknie C1' bez zdania o tle przy ostatnim zdjęciu.

## Verification
> `qa`, 2026-10-09. Rytuał WZ-024: `dart format` (0 zmian) → `flutter analyze` (czysto) → `flutter test` — **542 testy, wszystkie
> zielone** (było 504; +38 nowych i przepisanych).

### Tests (happy path per AC)
| AC | Test |
|---|---|
| AC-1 | `grave_screens_test.dart` — D1, ISSUE-024 AC-1: karta w grobie → widok (bez formularza), ✎ → „Poprawa wpisu”, „Zapisz” → widok z nowym rokiem, wstecz → grób z nowym rokiem; `skeleton_test.dart` — pasek na widoku osoby (zakładka Mapa), karta w Osobach → widok (zakładka Osoby), bez „Pochówek” dla osoby bez grobu |
| AC-2 | `person_screen_test.dart` — role „Ojciec”, „Matka”, „Mąż”, „Córka”, „Syn”, węzeł → widok krewnego, wstecz; bez „Pokaż w drzewie”; `mini_tree_test.dart` — układ: jeden związek, dwa związki po bokach z rozłącznymi grupami dzieci i przewijaniem, rodzina jednego rodzica, sama osoba |
| AC-3 (runda 1) | `person_screen_test.dart` — „Ja”, „Mama Anna”, „Jej mama Maria”, bez „babcia”/„Twoja”; dla „ja” bez sekcji; bez „ja” — tekst i „Wybierz…”; bez ścieżki — tekst; `kinship_test.dart` — ścieżka (babcia, rodzeństwo jako jeden krok, przyrodnie przez rodzica, mniej „para”, niższe `id`, graf z bazy); `kinship_names_test.dart` — podpisy z R3, zaimek z rodzaju słowa, neutralne i „małżonek” |
| AC-4 (D2) | `person_screen_test.dart` — „Pochówek” → cmentarz z `highlightGraveId`, zakładka Osoby, karta `selected`, wstecz → widok |
| AC-5 | `migration_test.dart` — v7→v8 na danych (`testWithDataIntegrity`): wiersze, łącza, kadry bez zmian, `is_background` = 0, indeks, drugie tło odrzucone; `restore_service_test.dart` — **kopia v7 w aplikacji v8: liczniki, łącza i kadry bez zmian, nikt nie ma tła**; kopia end-to-end ma tło matki z powrotem na jej łączu (ojciec na tym samym zdjęciu bez tła); `person_photos_test.dart` — ustaw / przenieś / zdejmij tło, tło przeżywa kolejność i kadr, znika z łączem, dwie osoby na jednym zdjęciu; `database_test.dart` — v8, indeks; `person_photos_screens_test.dart` — trzy działania, „Ustaw jako tło” → „Zdjęcie w tle” i „Usuń z tła” → zapis; okno usunięcia tła; `person_screen_test.dart` — tło nad portretem |
| D20 | `person_screen_test.dart` — „Ta osoba nie ma jeszcze zdjęć.” → „Dodaj zdjęcie” → poprawa z arkuszem „Zdjęcia osoby” → galeria → „Zapisz” → „Zdjęcia · 1” i portret |
| D15 | `person_screen_test.dart` — z poprawy Marii: karta Jana → widok Jana → węzeł Marii → ✎ wraca do tej samej poprawy z wpisanym „Maria Józefa” |
| W2 | `person_screen_test.dart` — tło i „Zdjęcia” z widoku: podgląd bez działań i bez „Zmień”, baza bez kafelka, opis komórki „tło” |
| *Input from ISSUE-025* | `family_screens_test.dart` — chip „Syn: Kuba” → widok Kuby (formularz Marii czeka pod spodem) → ✎ → jego wpis z „Ojciec: Jan”, „Matka: Maria” |

Przepisane, bo zachowanie się zmieniło: `grave_screens_test.dart` (D1), `skeleton_test.dart` (dwa testy), `family_screens_test.dart` (role),
`person_photos_screens_test.dart` (droga do poprawy przez widok — 7 testów przez `openJan`/`saveForm`), `database_test.dart`,
`data_state_test.dart`, `data_state_screen_test.dart` (wersja 8).

### Agent na emulatorze (przed stopem #2)
`Medium_Phone`, build release jako aktualizacja na danych testowych v7 (kroki 1–7 planu); zrzuty w katalogu tymczasowym sesji
(`v1…v14`, `review/r01…r15`, `review/f01…f07`):
1. Po aktualizacji: dane całe, „Stan danych” — wersja schematu 8 (`is_background` sprawdzone testem migracji; buildu release nie da się
   czytać `run-as`).
2. Wejścia: grób → widok Jana; Osoby → widok; „Ja” → widok bez sekcji 7; formularz → karta Ewy → widok Ewy; D15 — ✎ wraca do
   otwartej poprawy Jana.
3. Mini-drzewo Ewy: rodzice (ciągła), Jan „razem” po lewej (przerywana), Kuba „Mąż” po prawej, dzieci pod związkami; przy 200% role
   całe, inicjały w okręgach.
4. Łańcuchy: „Ja → Rodzic Stefan → Jego rodzic Jan”, „Ja → Rodzeństwo Ewa”, „Ja → Żona Zofia”.
5. „Pochówek” → Cmentarz Powązkowski, grób z obrysem, `selected=true`, zakładka Osoby.
6. Tło: ✎ → zdjęcia → „Ustaw jako tło” → „Zapisz” → widok z tłem (Zofia); „Dodaj zdjęcie” → poprawa z arkuszem → galeria →
   „Zapisz” → portret; z widoku zdjęcia tylko do oglądania.
7. `uiautomator`: węzły i wiersze łańcucha osobne i `clickable` z opisem (po poprawce `container`); zaznaczona karta `selected`;
   tekst 200% — daty z etykietą nad wartością, nic istotnego nieucięte.
8. **Próbne odtworzenie na `Grobing_Restore`:** kopia skonfigurowana od nowa na `Medium_Phone` z hasłem testowym do Pobranych
   (`grobing-klucz-024.age`, `grobing-kopia-024.age`, wymyślone dane), kopia v8 z tłem Zofii → `Grobing_Restore` → „Odtworzono kopię…
   Odcisk danych w kopii: c524e86930900532 — ten sam co niżej”, schemat 8; widok Zofii po odtworzeniu ma tło i profilowe.

### `ui` review (subagent, bez historii)
0 BLOCKER · 3 MAJOR · 5 MINOR — **wszystkie poprawione przed stopem #2** (*Dev report → After `qa` and the `ui` review*) i sprawdzone na
emulatorze (`review/f01…f06`). MAJOR: pierścień przykryty przez okrąg (portret, środek drzewa, łańcuch); rola ucięta w drzewie przy
200%; „Pochów / ek” łamane przy 200%. MINOR: przerwy w linii łańcucha; inicjały bez limitu skali; martwy chevron karty partnera;
„małżonek”/„partner” dla tej samej osoby; podwójne zdanie w oknie C1'. Odstępstwa z *Dev report* 1–6 przyjęte (6 — wysokość tak, linia
poprawiona). Specyfikacje po przeglądzie: [[osoba]] v2.2, [[zdjecie]] C1', [[zdjecia-osoby]] v1.3. Przegląd zauważył też, że zrzuty
mają gęstość 2,625 (411 dp), a nie 360 dp — ucinanie zależy od stałych szerokości w kodzie, więc wnioski obowiązują i dla 360 dp.

### Family data
- Zmiany kodu, testów i vaulta: tylko wymyślone osoby (Wymyślon-, Testow-, Przykładow-, Zmyślon-) i publiczna nazwa cmentarza z bazy OSM
  na zrzutach; żadnych baz, kopii, eksportów ani obrazów w repo (makieta, zrzuty, pliki kopii — w katalogu tymczasowym sesji).
- Suchy przebieg strażnika treści na liście plików kodu (`git add -- …` w `echo`) — **przechodzi**.

### Not covered (named)
- TalkBack na żywo (opisy sprawdzone `uiautomator` i testami semantyki).
- Ekran 360 dp na emulatorze (`Medium_Phone` ma 411 dp) — układ mini-drzewa przy 360 dp sprawdzają testy układu.
- Stany „bez ścieżki”, „bez ja”, „błąd odczytu” — tylko w testach widżetów, nie na zrzutach.
- Eksport tła do GEDCOM — [[US-006-eksport-dla-rodziny]].

### Stop #2 — runda 1 (2026-10-09)
- **Krok 1 (osoba i rodzina): „ok”. Krok 2 („Jak łączy się ze mną”): „ok”.**
- **Krok 3 (tło) — zmiana:** autor (zaznaczył na zrzucie widoku obszar nad imieniem, obok portretu): *„chciałbym móc kliknąć w ten
  obszar i od razu być przekierwany do listy zdjęć (domyślnie jest tam zwykłe tło) z tą osobą z możliwośią dodania zdjęcia
  powiązanego z tą osobą (aparatem lub z galerii) i po wybraniu ustawia się to tło”*. Pasmo tła jest zawsze (bez zdjęcia — zwykłe
  tło), a jego dotknięcie otwiera wybór tła: zdjęcia osoby i „Dodaj zdjęcie”; wybór ustawia tło od razu. Wraca do `ui` → `dev` →
  `qa` → stop #2, runda 2 ([[osoba]] v2.3, D21).

### Stop #2 — runda 1 → poprawki (2026-10-09)
- **`ui`:** [[osoba]] v2.3 (pasmo tła zawsze, D21; *States* — błąd zapisu tła; AC-5 — droga przez pasmo), [[zdjecia-osoby]] v1.4 (tryb
  „Zdjęcie w tle”), [[style-b]] v1.19 (reguła 14: tło z pasma, ramka zaznaczenia wokół zdjęcia, pasmo bez tła jako wyjątek).
- **`dev`:** `person_screen.dart` — pasmo 140 dp zawsze (bez tła: powierzchnia z ikoną `add_photo_alternate_outlined` w akcencie i
  `tooltip`, opis „Zdjęcie w tle: brak”), dotknięcie → `_chooseBackground`: szkic zdjęć → „Zdjęcie w tle” → wybór zapisuje się od razu
  (`writeWithPersonPhotos` w transakcji, bez wpisu osoby), błąd — komunikat u dołu; `person_photos_screen.dart` — tryb
  `chooseBackground` (podpowiedź, siatka z ramką obecnego tła wokół zdjęcia, kafelek: jedno zdjęcie z aparatu albo galerii, „Bez
  zdjęcia w tle”), `BackgroundChoice`; `selected` w semantyce tylko w trybie wyboru.
- **Przegląd `ui` zmiany** (subagent): 0 BLOCKER · 1 MAJOR (ramka zaznaczenia na krawędzi zdjęcia — na sepii ok. 1:1) · 5 MINOR
  (`tooltip` ikony, opis „brak”, stan błędu w specyfikacji, nieaktualne zdania w [[osoba]] i [[style-b]], `selected: false` poza wyborem)
  — wszystkie poprawione; ramka sprawdzona na emulatorze (`review/g04`).
- **`qa`:** `person_screen_test.dart` — AC-5/D21 (pasmo → wybór → inne zdjęcie zapisane od razu → „Bez zdjęcia w tle”), W2 osobno, D21
  dla osoby bez zdjęć (zwykłe pasmo → „Dodaj zdjęcie” → galeria → tło i profilowe); **544 testy, wszystkie zielone**; format i analiza
  czyste; strażnik treści przepuszcza paczkę. Emulator `Medium_Phone` (build release): pasmo bez tła (Kuba), pusty wybór, wybór z
  sześcioma zdjęciami (Ewa), zaznaczone tło (Zofia).

### Stop #2 — runda 2 (2026-10-12)
- **Krok 3 (tło z pasma): „ok”** (autor). **Sprawdzenia na urządzeniu nie było** — agent zaczął je uruchamiać, autor przerwał:
  *„pomiń”*. Wynik kroku stoi więc na słowie autora, bez śladu na `Medium_Phone` (pamięć: „ok” bez śladu agent zwykle sprawdza).
- Kroki 1 i 2 — „ok” z rundy 1.

### Verdict
**APPROVED (self-check, z uwagami)** — `qa`, 2026-10-12. Każde AC ma test happy-path (AC-3 i AC-4 w nowym brzmieniu, AC-6 → drzewo);
migracja v7→v8 z testem; odtworzenie: testy kopii v7 i v8 z tłem oraz próbne odtworzenie na `Grobing_Restore` (odcisk zgodny); dwa
przeglądy `ui` — wszystkie znaleziska poprawione; zero danych rodziny (strażnik treści przepuszcza paczkę). Uwagi: krok 3 rundy 2 bez
sprawdzenia na urządzeniu (wyżej); TalkBack i 360 dp nie na żywo (*Not covered*).
