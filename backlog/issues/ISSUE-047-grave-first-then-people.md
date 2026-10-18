---
title: "ISSUE-047 — Grave first, then people: add an empty grave, attach a person already in the app, add a person from the People tab"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-18
verdict-reviewer: self-check
source: "`/pm` 2026-10-18 — autor przeszedł cały przepływ na emulatorze (dane demo), punkty 1–3 z 7; podział na pozycje — `pm` (autor: „Do twojej decyzji ile tych zadań”)"
created: 2026-10-18
updated: 2026-10-18
---

# ISSUE-047 — Najpierw grób, potem osoby

> Autor, przed instalacją MVP: *„gdy próbuję dodać nowy grób, to nagle pokazuje się „Osoba w grobie” — a chciałbym dodać po prostu grób, a
> następnie osobę (lub osoby, które tam leżą)”* · *„gdy na grobie klikam „Dodaj osobę”, powinienem móc albo wybrać z istniejącej listy, albo dodać
> nową osobę do rodziny”* · *„w zakładce Osoby nie widzę możliwości dodania nowej osoby”*.
>
> **Dlaczego przed instalacją:** dziś nie ma drogi, by osobę już wpisaną (np. rodzica dodanego arkuszem rodziny, [[rodzina]]) przypiąć do grobu
> znalezionego później — zostaje wpisać ją drugi raz. Na prawdziwych danych z wyjazdu to duplikaty, a scalania osób w aplikacji nie ma. To jakość
> danych, nie wygoda.

## What to build
- **„Dodaj grób” otwiera grób, nie osobę** ([[cmentarz]] el. 6 i 9): okno grobu — te same pola co „Popraw grób” ([[grob]] 3a: nazwa, kwatera, rząd,
  miejsce) w trybie nowego grobu; po zapisie widok grobu w stanie „pusty” (jest już w [[grob]] *States*: „W tym grobie nie ma jeszcze wpisanych osób.”
  + „Dodaj osobę”). Zmienia decyzję [[wpis-osoby]] *Decisions* → „Grób powstaje z pierwszą osobą” — jej *Obali* („potrzeba grobu bez osób”) trafione.
- **„Dodaj osobę” w grobie → wybór osoby** ([[grob]] el. 6): najpierw szukaj, potem nowa — wzór z arkusza [[rodzina]] B2–B5 (szukaj · „Nowa osoba” ·
  „W tym grobie” · „Inne osoby”; D3). Wybrana osoba dostaje pochówek w tym grobie; „Nowa osoba” → [[wpis-osoby]] „kolejna osoba”, jak dziś.
- **„Dodaj osobę” w zakładce Osoby** ([[osoby]] — dziś bez dodawania): osoba bez grobu (np. żyjący krewny). Kształt i miejsce przycisku — `ui`.
- Projekt: `ui` przed `planning` — zmiana [[cmentarz]], [[grob]], [[osoby]], [[wpis-osoby]]; makieta, bo zmienia się przepływ wpisywania
  (retro 1, R5).

## Acceptance Criteria
- **AC-1** *Given* cmentarz *When* dotykam „Dodaj grób” i zapisuję nazwę „Grób rodzinny Wymyślonych” *Then* widzę ten grób pusty, z „Dodaj osobę”;
  formularz osoby nie otwiera się sam.
- **AC-2** *Given* Jan Wymyślony jest w aplikacji bez grobu (dodany w arkuszu rodziny jako rodzic) *When* w grobie dotykam „Dodaj osobę” i wybieram
  Jana *Then* Jan jest w tym grobie, a w aplikacji nadal jest jeden Jan — jego daty, zdjęcia i rodzina bez zmian.
- **AC-3** *Given* grób *When* „Dodaj osobę” → nowa osoba *Then* formularz jak dziś w trybie „kolejna osoba” (nazwisko podpowiedziane z grobu).
- **AC-4** *Given* zakładka Osoby *When* dodaję osobę Marię Zmyśloną *Then* Maria jest na liście, bez grobu, a jej wpis da się poprawić jak każdej
  osoby bez grobu ([[wpis-osoby]] v5).
- **AC-5** *Given* kopia sprzed tej pozycji *When* odtwarzam ją w nowej wersji *Then* dane są kompletne (DoD — przy zmianie schematu także test
  migracji).

## Notes
- **Dane:** `burials` to osobna tabela osoba ↔ grób ([[data-model]]), więc grób bez osób i pochówek osoby, która już jest, mieszczą się
  prawdopodobnie w schemacie v15 — **do potwierdzenia przez `planning`**.
- ~~`⚠️ OPEN`~~ **✅ rozstrzygnięte projektem `ui`** ([[grob]] D23, D24; [[cmentarz]] D38) — na stop #1 razem z makietą (*Implementation plan*):
  1. **osoba, która ma już grób** — na liście wyboru: nieaktywna z powodem, drugi pochówek czy przeniesienie? (pierwszy pochówek liczy się w
     [[ADR-006-claimed-value-separate-structures]] D3);
  2. **pusty grób porzucony** — autor tworzy grób i wychodzi bez osób: zostaje jako „Grób bez wpisanych osób” ([[cmentarz]] *States*) czy
     znika? Czy da się go usunąć?
- Miejsce w kolejce: [[CURRENT_STATE]] → *In progress* (kolejka przed instalacją). Następne z tego samego przeglądu autora:
  [[ISSUE-048-portrait-photos]] · [[ISSUE-049-tree-levels-and-zoom]] · [[ISSUE-050-next-event]].
- [[EPIC-001-zabezpiecz-i-przepisz]] ([[US-002-przepisanie-grobu]], [[US-003-przepisanie-rodziny]]).

## Implementation plan
> `planning`, 2026-10-18. **Pozycja z ekranem (zmiana istniejących).** Specyfikacje — propozycja `ui` na stop #1: [[cmentarz]] **v8** (okno „Nowy grób”
> 9a, D38), [[grob]] **v9** (pusty grób, wybór osoby 8–12, D22–D24), [[osoby]] **v3** („Dodaj osobę” 8, D10), [[wpis-osoby]] **v6** (tryb „nowy grób”
> usunięty, tryb „nowa osoba”, imiona z szukania). Wytyczne [[style-b]] bez zmian, bez nowych tokenów. **Makieta:**
> `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/cce9fe30-7f70-4c38-a4b5-07fd72c0b003/scratchpad/makieta-047.html`
> (7 ekranów, miejsca dotknięć zaznaczone). Bez US (task-level, pod US-002 / US-003), krok: warunek kroku 1 UJ-001 (M1).

> **Stop #1 — 2026-10-18, autor: *„Tak”*** na pytanie „Czy przepływ z makiety zostaje?”. Przyjęte razem z decyzjami projektowymi: [[grob]] D22–D24,
> [[cmentarz]] D38, [[osoby]] D10 i koszt dotknięć (nowy grób z pierwszą osobą 1 → 4, kolejna nowa osoba 1 → 2). Specyfikacje przestają być propozycją.

### Scope — diff
**Dane (`lib/data/graves.dart`) — bez zmiany schematu** (sprawdzone: `graves` wymaga tylko `cemetery_id`, `burials` to osobna tabela osoba ↔ grób):
1. `addGrave(db, cemeteryId, {name, sector, row, plot, paidUntil})` → id grobu. Jedna transakcja: wiersz grobu + to samo, co zapisuje `setGraveDetails`
   (kwatera przez `sectorForAddress`, słowo pola usunięte, opłata). Wspólny kawałek wydzielony, żeby oba zapisy nie rozjechały się przy następnej zmianie.
2. `addExistingPersonToGrave(db, graveId, personId)` → pochówek przez `addBurialWithClaim` (źródło po cichu, jak każdy pochówek). **Odmowa (`StateError`), gdy
   osoba ma już jakikolwiek pochówek** — reguła D23 także w danych, nie tylko w wyglądzie.
3. `addPersonWithoutGrave(db, {entry, alsoWrite})` → osoba z datami, bez pochówku; „wszystko albo nic” jak `addPersonToGrave` (`_addPerson` rozdzielony na
   wpis osoby i opcjonalny pochówek).
4. `loadPersonChoices` — bez zmian w kształcie: `graveName`/`cemeteryName` = null znaczy „bez grobu”; plus `inGrave` dla „już w tym grobie”.
   `addPersonToNewGrave` **zostaje** w danych (25 plików testów używa go jako przygotowania), ale żaden ekran go już nie woła.

**Ekrany:**
5. `lib/app/grave/cemetery_screen.dart` — `_addGrave`: zamiast `PersonFormScreen(NewGrave…)` okno `GraveDialog` w trybie nowego grobu (tytuł „Nowy grób”, puste
   pola, chipy kwater cmentarza) → `addGrave` → `GraveScreen` nowego grobu. Pasek grobów (6) i lista (9) — ten sam przycisk. Karta grobu bez osób: z nazwą —
   linia (b) „bez wpisanych osób”; bez nazwy — „Grób bez wpisanych osób” (jest), podsumowanie liczy groby bez osób (cmentarz *States*).
6. `lib/app/grave/grave_screen.dart` — `GraveDialog` z trybem nowego grobu (tytuł, zapis przez `addGrave` zamiast `setGraveDetails`; walidacja, przewijanie
   D20 i błędy bez zmian); `_addPerson` → nowy ekran wyboru (7); stan „pusty” według [[grob]] *States* v9.
7. **Nowy plik** `lib/app/grave/grave_person_choice_screen.dart` — „Kto leży w tym grobie?” ([[grob]] 8–12): `PersonChoiceList` z trybem sekcji grobu
   (`lib/app/family/person_choice_list.dart`: „Bez grobu” / „W grobach” zamiast „W tym grobie” / „Inne osoby”; w „W grobach” wszyscy nieaktywni z powodem
   „już w tym grobie” albo „w grobie: <grób albo cmentarz>”). Wiersz „Bez grobu” → `addExistingPersonToGrave` → `pop` do grobu; błąd → pasek komunikatu.
   „Nowa osoba” → `PersonFormScreen(NextPerson(…, givenNames: tekst))`, który zastępuje wybór na stosie (zapis → grób, jak dziś). Arkusz rodziny używa
   `PersonChoiceList` jak dotąd — jego sekcje się nie zmieniają.
8. `lib/app/grave/person_form_screen.dart` — `NewGrave` usunięty; `NextPerson` z `givenNames` (fokus, kursor na końcu) i bez liczby osób w podtytule przy
   pustym grobie; nowy tryb **`NewPerson`** („Nowa osoba” · „bez grobu w aplikacji”, `addPersonWithoutGrave`, zapis → `openPersonView` zamiast formularza na
   stosie). Miejsca zamieszkania (9b) w nowym trybie jak w każdym; „Rodzina” i wieniec — dalej tylko w poprawie.
9. `lib/app/people/people_screen.dart` — wypełniony „Dodaj osobę” przypięty na dole listy ([[osoby]] 8): przy tekście w szukaniu „Dodaj osobę: „Ewa””; odstęp
   pod ostatnią kartą; pusta baza — zdanie i przycisk. Wzór przycisku — ten sam co „Dodaj grób” (`cemetery_screen.dart`).

### AC → test happy-path (`qa`)
| AC | Test |
|---|---|
| AC-1 | ekran: „Dodaj grób” → okno „Nowy grób” → „Grób rodzinny Wymyślonych” → „Zapisz” → widok grobu z „W tym grobie nie ma jeszcze wpisanych osób.”, bez formularza osoby; wstecz → karta z nazwą i „bez wpisanych osób”. Dane: `addGrave` z adresem i opłatą |
| AC-2 | dane: `addExistingPersonToGrave` — Jan Wymyślony (dodany arkuszem rodziny, bez grobu) w grobie, liczba osób w bazie bez zmian, jego daty, zdjęcia i rodzina bez zmian; odmowa dla osoby z pochówkiem. Ekran: wybór → „Jan” → wiersz w „Bez grobu” → grób z kartą Jana; osoba z innego grobu nieaktywna z powodem |
| AC-3 | ekran: „Nowa osoba: „Anna”” → formularz „Osoba w grobie” z „Anna” w Imionach, nazwisko podpowiedziane z poprzedniej osoby; zapis → grób z dwiema kartami |
| AC-4 | ekran: Osoby → „Maria” → „Dodaj osobę: „Maria”” → formularz „Nowa osoba” → „Zmyślona” → „Zapisz” → widok Marii; wstecz → Maria na liście. Dane: `addPersonWithoutGrave` bez pochówku |
| AC-5 | kopia z pustym grobem, osobą bez grobu i pochówkiem dodanym z wyboru → odtworzenie → ten sam stan (test kopii, jak `backup_archive_test.dart`). **Bez testu migracji** — schemat się nie zmienia |

Testy, które dziś zakładają „Dodaj grób” → formularz (np. `cemetery_map_screen_test.dart`, `grave_screens_test.dart`, `skeleton_test.dart`), przechodzą na
nowy przepływ — wskaże je `flutter test`. Rytuał WZ-024: `dart format` → `flutter analyze` → `flutter test --timeout 120s`.

### Manual checks (stop #2)
**Agent na emulatorze — przed stopem, ze zrzutami.** `Grobing_Restore` ma dziś **demo**: najpierw zapisać obecny stan i wgrać stan sprzed demo z
`C:\Programowanie\Grobing\_pokaz` (README tam), **nigdy `pm clear` bez zapisanego tar**; po pozycji — demo z powrotem.
1. Cmentarz → „Dodaj grób” → „Zapisz” przy pustych polach → widok „Grób”, pusty; wstecz → karta „Grób bez wpisanych osób”. To samo z nazwą i kwaterą.
2. Osoba z drzewa bez grobu → w grobie „Dodaj osobę” → kilka liter → wiersz w „Bez grobu” → karta w grobie; w Osobach ta osoba raz.
3. Osoba z innego grobu i osoba z tego grobu — wyszarzone z powodem, dotknięcie nic nie zmienia; TalkBack czyta „niedostępne” i powód.
4. „Nowa osoba: „…”” → formularz z imieniem → zapis → grób; Osoby → „Dodaj osobę: „…”” → „Nowa osoba” → zapis → widok osoby → wstecz → lista.
5. Tekst 200% na 360 dp: okno „Nowy grób”, wybór osoby, przycisk w Osobach (nie zasłania ostatniej karty).
6. Kopia w tle po zapisach i próbne odtworzenie na drugim emulatorze — pusty grób, osoba bez grobu i nowy pochówek są po odtworzeniu.

**Autor: odczucie — najwyżej 3 kroki** (emulator):
1. Dodaj grób → pusty grób → „Dodaj osobę” → wybierz kogoś z drzewa: czy „najpierw grób, potem osoby” jest takie, jak chciałeś?
2. Wpisz jeden grób z dwiema nowymi osobami (wymyślonymi): czy 4 dotknięcia do pierwszej osoby przeszkadzają? (*Obali* [[cmentarz]] D38)
3. Osoby → „Dodaj osobę”: czy przycisk na dole przeszkadza w przeglądaniu listy? (*Obali* [[osoby]] D10)

### Out of Scope
- **Usuwanie** grobów, osób i pochówków (brief G7/C5 — osobna decyzja; [[grob]] D24, [[cmentarz]] D38 *Obali* 2);
- **ta sama osoba w dwóch grobach** (napis symboliczny) — [[grob]] D23 *Obali*; scalanie duplikatów, które już są;
- przeniesienie osoby do innego grobu; „Zapisz i dodaj następną” ([[wpis-osoby]] *Decisions*);
- portret i zdjęcia osoby — [[ISSUE-048-portrait-photos]].

### Decision for stop #1 (author) — jedno pytanie
Czy przepływ z makiety zostaje (**„tak” = budujemy**)? Na „tak” przechodzą też decyzje projektowe pokazane w makiecie (*Decyzje w projekcie*):
- osoba, która ma już grób, jest w wyborze wyszarzona z powodem — nie trafi do drugiego grobu, bo pochówku nie da się cofnąć (D23);
- pusty grób zostaje, bez usuwania (D24, D38);
- wybór osoby zapisuje od razu, bez okienka (D22);
- „Dodaj osobę” w Osobach na dole listy (D10);
- koszt: nowy grób z pierwszą osobą 1 → 4 dotknięcia, kolejna nowa osoba 1 → 2.

## Dev report
> `dev`, 2026-10-18. Flutter 3.41.1 (przypięty). `dart format` i `flutter analyze lib` — czyste. **Bez zmiany schematu** (v15).

### Done (plan → *Scope — diff*)
1. `lib/data/graves.dart` — `addGrave` (wiersz grobu + część okna w jednej transakcji; wspólny `_writeGraveDetails` z `setGraveDetails`),
   `addExistingPersonToGrave` (odmowa `StateError`, gdy osoba ma już pochówek albo jej nie ma — D23 w danych), `addPersonWithoutGrave`
   (`_addPerson` z opcjonalnym pochówkiem). `addPersonToNewGrave` zostaje dla testów; ekran go nie woła.
2. `lib/app/family/person_choice_list.dart` — parametr `forGrave`: sekcje „Bez grobu” (do wyboru) i „W grobach” (nieaktywne, powód „już w tym
   grobie” albo „w grobie: <grób albo cmentarz>”); bez linii „Nie ma osoby pasującej…” — przy braku wyników tylko pole i „Nowa osoba: „…””.
3. **Nowy plik** `lib/app/grave/grave_person_choice_screen.dart` — „Kto leży w tym grobie?”; wiersz „Bez grobu” → `addExistingPersonToGrave` → powrót
   do grobu; błąd → pasek „Nie udało się zapisać. Spróbuj jeszcze raz.”; „Nowa osoba” → formularz zastępuje wybór na stosie.
4. `lib/app/grave/grave_screen.dart` — `GraveDialog` z `grave: null` = „Nowy grób” (tytuł; reszta okna bez zmian); „Dodaj osobę” → wybór.
5. `lib/app/grave/person_form_screen.dart` — `NewGrave` usunięty; `NextPerson(givenNames:)` (kursor na końcu, płeć podpowiedziana z imienia, w pustym
   grobie podtytuł bez liczby); nowy `NewPerson` („Nowa osoba” · „bez grobu w aplikacji”, zapis → widok osoby zamiast formularza).
6. `lib/app/grave/cemetery_screen.dart` — „Dodaj grób” → okno „Nowy grób” → `addGrave` → widok nowego grobu; karta grobu z nazwą bez osób ma linię
   „bez wpisanych osób”.
7. `lib/app/people/people_screen.dart` — wypełniony „Dodaj osobę” pod listą (jak „Dodaj grób” na liście grobów), przy szukaniu „Dodaj osobę: „…””
   (jedna linia, „…”), → `NewPerson(givenNames:)`.

### Emulator pass (`Grobing_Restore`, build profile x86_64)
Stan demo zapisany przed zamianą: `scratchpad/emu047/stan-przed-047.tar` + `stan-przed-047-base.apk` (demo z dzisiejszymi zmianami autora — **przed
końcem pozycji wgrać z powrotem**); wgrany stan sprzed demo z `_pokaz`, na nim build ISSUE-047. Zrzuty `01`–`18` w `scratchpad/emu047/shots/`
(poza repo; na liście „W grobach” widać wpis autora z emulatora — zrzutów nie przenosić).
- AC-1: „Dodaj grób” → okno „Nowy grób” (fokus w nazwie) → „Zapisz” przy pustych polach → grób „Grób”, pusty, „Dodaj osobę”; „Anuluj” nie zostawia
  grobu (licznik bez zmian); grób z nazwą → karta „<nazwa> / bez wpisanych osób”. ✅
- AC-2: wybór → „Jan” → „Bez grobu” → Jan Wymyślony → grób z jego kartą, bez formularza. Wiersze „W grobach” nieaktywne (`enabled=false`), dotknięcie
  nic nie robi. ✅
- AC-3: „Nowa osoba: „Anna”” → „Osoba w grobie” z „Anna”, ♀ podpowiedziana, nazwisko z poprzedniej osoby → „Zapisz” → grób z dwiema kartami. ✅
- AC-4: Osoby → „Ksenia” → „Nie ma osoby „Ksenia”.” + „Dodaj osobę: „Ksenia”” → „Nowa osoba · bez grobu w aplikacji” → „Zapisz” → widok osoby; wstecz →
  Ksenia na liście, licznik +1. ✅
- 200% na 360 dp: Osoby — przycisk 52 dp, długie imię ucięte „…”; wybór osoby — wiersze się zawijają, nic nie ucięte; okno „Nowy grób” z klawiaturą
  przewija się jak „Popraw grób” (znana luka [[grob]] v6.1). Tekst i gęstość z powrotem domyślne.

### Deviations
- **Pole szukania w wyborze** ma kształt z arkusza rodziny (linia pod polem, jak zbudowane [[rodzina]] B2), a nie ramkę — to ten sam `PersonChoiceList`.
- **Błąd odczytu osób** pokazuje teraz „Nowa osoba” i „Nie udało się odczytać osób.” także w arkuszu rodziny (do dziś pusty ekran) — ten sam widżet,
  zachowanie według [[grob]] v9 → *Stany wyboru*.
- Po powrocie do Osób z tym samym tekstem przycisk dalej mówi „Dodaj osobę: „Ksenia””, choć Ksenia jest już na liście nad nim — zgodnie z [[osoby]] 8.

### For `qa`
- **Nie kompilują się** (`NewGrave` usunięty): `test/app/family/family_screens_test.dart:1143`, `test/app/grave/grave_screens_test.dart:363, 402`.
- Stary przepływ „Dodaj grób” → formularz / „Dodaj osobę” → formularz zakładają też: `cemetery_map_screen_test.dart`, `grave_photo_screens_test.dart`,
  `skeleton_test.dart` (7 miejsc z tymi przyciskami).
- Testy z planu → *AC → test happy-path*; próbne odtworzenie (AC-5) i przywrócenie stanu demo na `Grobing_Restore` po stopie #2.

## Verification
> `qa`, 2026-10-18. Rytuał WZ-024: `dart format` czysty · `flutter analyze` — brak uwag · `flutter test --timeout 120s` — **946 zielonych** (było 936).

### Tests (happy-path per AC)
- **AC-1** — `test/app/grave/grave_first_screens_test.dart` („Dodaj grób” → „Nowy grób” z fokusem w nazwie, „Anuluj” bez grobu, „Zapisz” → pusty grób,
  karta „bez wpisanych osób”); `test/data/grave_first_test.dart` (`addGrave` z nazwą, kwaterą, rzędem, miejscem i opłatą; puste okno = sam cmentarz);
  `cemetery_map_screen_test.dart` — grób bez nazwy i osób z pinezką: arkusz „Grób bez wpisanych osób” / „bez wpisanych osób” (regresja MAJOR z przeglądu).
- **AC-2** — wybór „Kto leży w tym grobie?”: „Bez grobu” nad „W grobach”, powody „w grobie: …” i „już w tym grobie”, nieaktywny wiersz nic nie robi, Jan
  dołącza do grobu, w bazie nadal jedna osoba; dane: pochówek z twierdzeniem, odmowa dla osoby z grobem i dla nieistniejącej (D23).
- **AC-3** — `grave_screens_test.dart` (przepisany test przepisywania): „Nowa osoba: „Jan”” i „„Anna”” → formularz z imieniem, fokus, podtytuł pustego
  grobu bez liczby, nazwisko podpowiedziane; wstecz z grobu nie wraca do wyboru ani formularza.
- **AC-4** — Osoby: „Dodaj osobę: „Ksenia”” → „Nowa osoba” · „bez grobu w aplikacji” → widok osoby → lista; w bazie bez pochówku.
- **AC-5** — `backup_archive_test.dart`: kopia z pustym grobem (nazwa, kwatera, opłata), osobą bez grobu i pochówkiem z wyboru — po odszyfrowaniu ten sam
  odcisk danych i ten sam stan. **Bez testu migracji** — schemat bez zmian (v15).
- **Dostępność dotyku** (retro 3, R2): `androidTapTargetGuideline`, `labeledTapTargetGuideline` i „każdy przycisk ma akcję dotknięcia” na wyborze osoby i
  na Osobach. `test/support/a11y.dart`: przycisk **wyłączony** (`enabled: false`) nie musi mieć akcji — inaczej reguła odrzucała nieaktywne wiersze D23.
- Testy starego przepływu przepisane na nowy: `family_screens_test.dart` i dwa w `grave_screens_test.dart` (`NewGrave` → `NewPerson`).

### Przegląd `ui` (subagent, zrzuty `01`–`18`)
0 BLOCKER · 1 MAJOR · 2 MINOR — **wszystkie poprawione przez `dev` przed stopem**, zrzuty `19`, `20`:
- MAJOR — arkusz grobu (stan B) bez nazwy i bez osób, z pinezką: pusty tytuł i „0 osób” → „Grób bez wpisanych osób” i „bez wpisanych osób” (zrzut 19, test);
- MINOR — pole szukania w wyborze bez ramki → ramka jak w arkuszu rodziny (`GrobingTheme.fields`, zrzut 20); odstępstwo 1 z *Deviations* nie przyjęte;
- MINOR — przewinięcie listy wyboru nie chowało klawiatury → chowa (sprawdzone: `mInputShown` true → false).
Przyjęte i zapisane przez `ui`: [[grob]] v9.1 (D25 nagłówki 14 sp, D26 odstępy pustego stanu), [[osoby]] v3.1 (D11), [[rodzina]] v2.2 (stan „błąd odczytu” —
odstępstwo 2). Poza zakresem (wcześniejsze): twarde spacje w „z d.” i „·” przy 200% ([[style-b]] reguła 6), nazwisko podpowiadane w formie poprzedniej osoby.

### Agent na emulatorze (plan → *Manual checks*)
1. ✅ „Dodaj grób” → „Zapisz” przy pustych polach → „Grób”, pusty; z nazwą → karta z nazwą i „bez wpisanych osób”; „Anuluj” — licznik bez zmian (zrzuty 02, 03, 08).
2. ✅ Osoba z drzewa bez grobu → w grobie, raz w Osobach (04, 06).
3. ✅ Wiersze „W grobach” nieaktywne z powodem (`enabled=false` w `uiautomator`, 05). TalkBack nie był włączony — czytanie „niedostępne” sprawdzone w semantyce.
4. ✅ „Nowa osoba: „…”” → formularz z imieniem → grób (07); Osoby → „Dodaj osobę: „…”” → widok → lista (10–13).
5. ✅ 200% na 360 dp (14–18): przycisk w Osobach 52 dp, długie imię „…”; wybór się zawija; okno „Nowy grób” przewija się jak „Popraw grób” (luka v6.1).
6. ⚠️ Kopia w tle i próbne odtworzenie **na urządzeniu** — nie robione (jeden emulator na raz); odtworzenie sprawdza test AC-5 → lista A.

### Dane rodziny
Zmiany w kodzie, testach i vaulcie: tylko wymyślone osoby (Wymyśl-, Zmyśl-, Testow-, Przykład-; imiona bez nazwisk z listy). Strażnik treści przepuścił
paczkę kodu i vaulta na próbie. Zrzuty leżą poza repo; na 05, 08, 09 i 17a jest wpis autora z emulatora — nie przenosić.

### Stop #2 — 2026-10-18, autor: *„Ok”*
Trzy kroki odczucia (plan → *Manual checks*, autor: odczucie 1–3) — **„ok” ze śladem na urządzeniu** (sprawdzone na `Grobing_Restore` przed zamknięciem,
bez zapisywania wpisanych nazw): nowy grób z nazwą, w nim osoba z drzewa wybrana z „Bez grobu” i nowa osoba z „Nowa osoba”; osoba dodana w zakładce Osoby
(licznik 111 → 113). Po stopie `Grobing_Restore` ma z powrotem **demo** (APK i dane zapisane przed pozycją: 41 osób) — wpisy z testów i ze stopu przepadły
razem ze stanem testowym; stan sprzed demo w `C:\Programowanie\Grobing\_pokaz` bez zmian.

### Hand checks for ISSUE-032
- **A** — próbne odtworzenie na urządzeniu kopii z pustym grobem, osobą bez grobu i pochówkiem dodanym z wyboru (w kodzie: test AC-5; na urządzeniu — nie).
- **B** — TalkBack na wyborze „Kto leży w tym grobie?”: wiersz „W grobach” czytany jako niedostępny z powodem (sprawdzone w semantyce, nie na żywo).

**Werdykt `qa`: APPROVED** (self-check, z uwagami: odtworzenie na urządzeniu i TalkBack → listy A i B; okno „Nowy grób” przy 200% z klawiaturą przewija
się jak „Popraw grób” — znana luka [[grob]] v6.1).
