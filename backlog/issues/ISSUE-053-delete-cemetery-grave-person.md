---
title: "ISSUE-053 — Delete everything that can be added: cemetery, grave, person, burial, pin, clan — with an undo"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-23
verdict-reviewer: self-check
source: "`/pm` 2026-10-23 — pytanie autora po stopie #2 [[ISSUE-052-cemetery-search-and-patient-plan]]: *„gdzie ja mogę teraz usuwać cmentarze lub osoby? (jeżeli się okaże, że się pomyliłem)”*; cel (R1): A — pusty cmentarz i pusty grób (*„oba”*), C — osoba, której nie powinno być, z powiązaniami (*„tak”*), B — osoba, która nie istnieje (*„ktoś się pomylił — zdarza się”*); duplikat osoby → [[ISSUE-054-merge-two-people]]. Stop #1 runda 1 → zasada autora *„wszystko, co można dodać, można też usunąć”*, w drugiej sesji: *„zrobiłbym od razu wszystko”*"
created: 2026-10-23
updated: 2026-10-23
---

# ISSUE-053 — Usuń wszystko, co można dodać: cmentarz, grób, osoba, pochówek, pinezka, ród — z „Cofnij”

> Autor 2026-10-23 w `/pm`, w trakcie wpisywania prawdziwych danych: *„gdzie ja mogę teraz usuwać cmentarze lub osoby? Jest taka funkcjonalność?
> (jeżeli się okaże, że się pomyliłem i chciałbym tę osobę lub cmentarz usunąć)”*. Dziś usunąć się nie da (brief G7/C5 — *„a mis-tap at the cemetery
> must not erase a person”*, Could; [[wpis-osoby]] „Bez usuwania osoby” czekało na osobną decyzję). Kandydat był w `CURRENT_STATE.md` → *Poza tą
> kolejnością* („usuwanie pustego grobu i pochówku … gdy zacznie przeszkadzać przy prawdziwych danych”) — zaczęło.

## What the author wants (cel przed projektem, R1 — odpowiedź autora)
- **A — pusty cmentarz i pusty grób** dodane przez pomyłkę: *„oba”*.
- **C — osoba, której nie powinno być**, razem z jej powiązaniami (np. pomylona rodzina): *„tak”*.
- **B — osoba, która nie istnieje** (*„ktoś się pomylił — zdarza się”*) — to C. **Ta sama osoba wpisana dwa razy** to nie usuwanie, tylko scalenie —
  [[ISSUE-054-merge-two-people]] (usunięcie kopii skasowałoby to, co przy niej uzupełniono).
- **Zasada (stop #1 runda 1, komentarz do makiety):** *„wszystko, co można dodać, można też usunąć”* — **w całości w tej pozycji, przed wyjazdem**
  (`/pm` 2026-10-23, druga sesja: *„zrobiłbym od razu wszystko”*). Spis z kodu, co dziś da się usunąć, a co nie: [[style-b]] reguła 16 → *mapa usuwania*.
- **Grób z osobami** (`/pm` 2026-10-23, druga sesja): *„gdy usuwamy grób to te osoby nie są usuwane a raczej tracą przypisany grób”* — tak samo cmentarz
  z grobami ([[cmentarze]] D40).

## What a deletion takes with it (schemat v15, klucze obce włączone, bez kaskad)
- **Cmentarz:** jego groby — każdy jak niżej — plan (`cemetery_plans`), kwatery (`sectors`), zdjęcie cmentarza (`media` z `cemetery_id` + plik). Osoby z
  grobów zostają.
- **Grób:** pochówki w nim (`burials` + ich `assertions`) — osoby zostają, bez grobu; zdjęcia nagrobka (`media` z `grave_id` + pliki), pinezka i adres
  (w wierszu grobu); kwatera, która zostaje bez strefy i bez grobów, znika jak dziś (`dropSectorIfUnused`).
- **Osoba z grobu (pochówek):** wiersz `burials` i jego `assertions`. Data pochówku (`events` typu `burial`) to fakt o osobie — zostaje.
- **Osoba:** jej udział w związkach (`family_partners`) i bycie dzieckiem (`family_children`) — związek, w którym nie zostaje nikt, znika razem ze swoimi
  zdarzeniami (ślub, „razem od”, koniec); zdarzenia osoby (`events`: urodziny, śmierć, pochówek); pochówki (`burials` — grób zostaje, może stać się pusty);
  „źródła” (`assertions`) tych zdarzeń, pochówków i więzi; zamieszkania (`residences`); powiązania ze zdjęciami (`person_media`) — zdjęcie, na którym
  nie zostaje nikt (ani grób, ani cmentarz), znika z plikiem. „Ja” (`settings.me_person_id`) się nie usuwa ([[wpis-osoby]] 12). Ród (`clans`) zostaje.
- **Pinezka:** `lat`, `lon`, `position_source`, `position_accuracy_m`, `position_recorded_at` w wierszu grobu → puste. Adres zostaje.
- **Ród:** `persons.clan_id` → puste u osób, które go wybrały (`no_wreath` bez zmian), potem wiersz `clans`. Wieniec liczy się z drzewa
  ([[ADR-021-clans-choice-at-the-person]]), więc osoby dostają to, co daje reguła bez tego rodu.

## Prior art and the decision under it (Pierwszy ruch — zmiana trudna do cofnięcia)
- **Wzorce usuwania:** przy działaniu niszczącym, które da się odwrócić, **„Cofnij” w pasku komunikatu** (np. Gmail, Zdjęcia Google) — okno „Czy na
  pewno?” klika się z przyzwyczajenia; okno — gdy znika więcej, niż widać. W aplikacji dziś: okno „Usunąć związek?” mówi, co zostaje
  (`union_summary_sheet.dart`). Źródło wzorca do potwierdzenia przez `planning` (cytat, nie pamięć). Programy
  genealogiczne (Gramps „Remove person”) usuwają osobę **razem z odniesieniami** w rodzinach i mówią przedtem, co zniknie.
- **Mechanizm — do `planning` (kandydat na ADR):** (H) usunięcie wierszy + „Cofnij” przez kilka sekund z zapamiętanych wierszy (bez zmiany schematu;
  pliki zdjęć kasowane dopiero po upływie „Cofnij”); (S) kosz — `deleted_at` w trzech tabelach, filtr w każdym zapytaniu i ekran kosza (zmiana schematu,
  każde zapytanie, które zapomni filtra, pokaże usuniętą osobę). Rekomendacja `pm`: **H** — kopia na Dysku trzyma stan sprzed usunięcia jako dalsza siatka;
  *Obali:* autor chce odzyskać usuniętą osobę po dniu → kosz (S).
- **Najtańszy falsyfikator:** odtworzenie z kopii już dziś przywraca usunięte dane (do następnej kopii) — sprawdza, czy H wystarcza bez kosza.

## What to build (zakres — szczegóły `ui` i `planning`; runda 2 po decyzjach autora)
1. **„Usuń cmentarz”** w oknie „Popraw cmentarz” — **przy każdym cmentarzu**; okno mówi, ile grobów znika i że osoby zostają bez grobu ([[cmentarze]] 15a).
2. **„Usuń grób”** w oknie „Popraw grób” — **przy każdym grobie**; okno wymienia osoby, które zostają bez grobu ([[grob]] 3d).
3. **„Usuń z grobu”** w poprawie wpisu osoby z grobem — osoba zostaje, bez grobu; przeniesienie = to + „Dodaj osobę” w dobrym grobie ([[wpis-osoby]] 12a).
4. **„Usuń osobę”** w poprawie wpisu — z oknem, które **mówi, co zniknie** (liczby: związki, zdjęcia, pochówek…), potem usunięcie ([[wpis-osoby]] 12).
5. **„Usuń pinezkę”** w trybie pinezki przy poprawie ([[cmentarz]] 12b).
6. **„Usuń ród”** na ekranie „Ród” ([[wieniec]] F7).
7. **„Cofnij”** po każdym usunięciu (pasek komunikatu) — **K2, przez 4 s** (stop #1 runda 2, decyzja autora); po jego upływie pliki zdjęć bez nikogo idą do kosza aplikacji.
8. Kopia w tle po usunięciu i po „Cofnij” jak po każdym zapisie.

**Bez zmiany bazy przy H.** Aktualizacja ze sklepu przed wyjazdem na Wszystkie Święte (`CURRENT_STATE.md` → *In progress*).

## Acceptance Criteria (propozycja `docs` z `/pm`; runda 2 — `ui` i `planning` po decyzjach autora)
- **AC-1** *Given* cmentarz „Cmentarz Wymyślony” bez grobów, z planem i zdjęciem *When* „Popraw cmentarz” → „Usuń cmentarz” *Then* znicza nie ma na mapie,
  cmentarza nie ma w wyszukiwarce, plan i zdjęcie zniknęły; *When* „Cofnij” *Then* wszystko wraca z tym samym planem i zdjęciem.
- ~~**AC-2** *Given* cmentarz z grobem *When* „Popraw cmentarz” *Then* zamiast „Usuń cmentarz” jest powód~~ — **zastąpione w rundzie 2:**
  **AC-2** *Given* „Cmentarz Testowy” z 2 grobami i 3 osobami w nich *When* „Usuń cmentarz” *Then* okno mówi „2 grobami…” i „Osoby z tych grobów (3)
  zostają w aplikacji — bez grobu.”; po „Usuń” trzy osoby są w Osobach „bez grobu” z datami, rodziną i zdjęciami; „Cofnij” przywraca cmentarz z grobami
  i osobami w nich.
- **AC-3** *Given* pusty grób ze zdjęciem nagrobka *When* „Usuń grób” *Then* znika z listy cmentarza; „Cofnij” przywraca go ze zdjęciem. **Runda 2:**
  *Given* grób z Janem Wymyślonym i Anną Testową *When* „Usuń grób” *Then* okno wymienia ich jako osoby, które zostają bez grobu; po „Usuń” oboje są w
  Osobach „bez grobu”; „Cofnij” przywraca grób z obojgiem.
- **AC-4** *Given* Jan Wymyślony z żoną Anną Testową, synem Piotrem, pochówkiem w grobie, zdjęciem z Anną i miejscem zamieszkania *When* „Usuń osobę” *Then*
  okno mówi, co zniknie; po potwierdzeniu Jana nie ma w Osobach i na drzewie, Anna i Piotr zostają (rodzina Anny z Piotrem), grób zostaje bez Jana,
  zdjęcie zostaje przy Annie; „Cofnij” przywraca Jana z wszystkimi powiązaniami.
- **AC-5** *Given* usunięcie *When* minie czas „Cofnij” i kopia w tle się zrobi *Then* odtworzenie kopii nie ma usuniętego wpisu, a odcisk danych się zgadza.
- **AC-6** (runda 2) *Given* Jan Wymyślony w złym grobie *When* jego poprawa → „Usuń z grobu” *Then* Jan zostaje w aplikacji „bez grobu” z datami,
  rodziną i zdjęciami, a w dobrym grobie „Dodaj osobę” → „Jan” pokazuje go w „Bez grobu” i dodaje jednym dotknięciem; „Cofnij” wkłada go z powrotem
  do pierwszego grobu.
- **AC-7** (runda 2) *Given* grób z pinezką „GPS ±4 m” *When* „Popraw pinezkę” → „Usuń pinezkę” *Then* na planie nie ma znicza grobu, a widok grobu mówi
  „bez pinezki”; „Cofnij” przywraca tę samą pinezkę (miejsce, źródło, dokładność, data).
- **AC-8** (runda 2) *Given* ród „Przykładowscy” wybrany u Antoniego, z wieńcem u 3 osób *When* ekran „Ród” → „Usuń ród” *Then* okno mówi „…zniknie u 3
  osób”, a po „Usuń” rodu nie ma na liście, Antoni i jego dzieci mają wieniec po ojcu Antoniego albo żaden; „Cofnij” przywraca ród i te same wieńce.

## Notes
- **Ekrany (`ui` → `planning`):** [[cmentarze]] (okno 15 „Popraw cmentarz”, 15a), [[grob]] („Popraw grób”, 3d), [[wpis-osoby]] (poprawa wpisu, 12a i 12),
  [[cmentarz]] (tryb D, 12b), [[wieniec]] (ekran „Ród”, F7) — bez nowego ekranu; okna, pasek „Cofnij” i mapa usuwania — [[style-b]] reguła 16.
- **Dane rodziny:** przykłady tylko z wymyślonych rdzeni (`family-data.md`).
- **`TRACEABILITY.md`** — wiersz przy starcie pozycji (`planning`).

## Stop #1 — runda 1 (2026-10-23, pierwsza sesja — rozliczona w drugiej)
- **K1 czy K2 — bez odpowiedzi.** Autor zamiast tego zapytał o zasadę „jedna sesja — jedno zadanie” (przeniesiona do Grobing: `autonomous-flow.md`
  → *One item per session*, `grobing-agents` 2944667). Pozycja zostaje `in-progress` na stopie #1; vault tej pozycji (ta pozycja,
  [[ISSUE-054-merge-two-people]], specyfikacje, kolejka w `CURRENT_STATE.md`, wiersz w `TRACEABILITY.md`) — niezacommitowany do zamknięcia paczki.
- **Komentarz autora do makiety:** *„Przy okazji powinniśmy też móc mieć możliwość usuwania grobów (ergo wszystko, co można dodać, można też
  usunąć)”*. Plan ma usuwanie grobu (3d), ale **tylko pustego**, a makieta pokazywała grób tylko przez analogię do cmentarza. Zasada autora
  poszerza zakres: **grób z osobami** (osoby zostają w aplikacji bez pochówku w tym grobie?), **cmentarz z grobami** (groby i pochówki znikają?) i
  inne rzeczy, które da się dodać (pinezka, ród, kwatera — część ma już „Usuń”). **Do nowej sesji (`ui` → `planning`):** spis „co można dodać ↔ czy
  można usunąć” z kodu, specyfikacje i makieta z panelami grobu, potem stop #1 od nowa — razem z K1/K2.
- **Rozliczenie (druga sesja, `/pm` 2026-10-23):** `pm` polecał przed wyjazdem tylko cmentarz, grób i osobę, a resztę po powrocie — autor: *„zrobiłbym od
  razu wszystko”* i *„gdy usuwamy grób to te osoby nie są usuwane a raczej tracą przypisany grób”*. `ui`: spis z kodu (dziś nie da się usunąć osoby z
  grobu, pinezki ani rodu; reszta ma „Usuń”) → [[style-b]] v1.50 reguła 16, [[cmentarze]] v3.1, [[grob]] v10.1, [[wpis-osoby]] v7.1, [[cmentarz]] v9.2,
  [[wieniec]] v1.3, makieta z panelami 1–18. Stop #1 od nowa — runda 2 niżej.

## Stop #1 — runda 2 (2026-10-23) — ✅ „tak”
- **Decyzja autora: *„tak K2 4s”*** — plan przyjęty; **K2, pasek „Cofnij” przez 4 s** (nie ok. 8 s z propozycji; 4 s to też
  domyślny czas paska we Flutterze). Przy czytniku ekranu i „Czasie na działanie” pasek nie znika sam ([[style-b]] v1.51 reguła 16).
- ~~**⚠️ OPEN K1/K2**~~ — pytanie było: po „Usuń” rzecz znika od razu (K1), czy przez ok. 8 s jest na dole pasek „Cofnij” (K2). Rekomendacja `ui` i
  `planning`: **K2** — kopia w tle po ok. 10 min ciszy nadpisuje plik na Dysku stanem już bez usuniętego, więc przy K1 po pomyłce zostaje kilka minut na
  odtworzenie całej kopii.
- **Decyzje projektowe do wglądu** (bez pytania): D40 cmentarz z grobami, D28 grób z osobami, **D29 „Usuń z grobu” w poprawie osoby, nad „Usuń
  osobę”** (*Obali:* autor szuka go w „Popraw grób” — krok 2 stopu #2), D43 pinezka w trybie pinezki, D21 ród, tytuły okien bez odmiany imion.

## Implementation plan (`planning`, 2026-10-23 — runda 2)
> Specyfikacje: [[cmentarze]] v3.1 (15a, D40) · [[grob]] v10.1 (3d, D28, D29) · [[wpis-osoby]] v7.1 (12a, 12) · [[cmentarz]] v9.2 (12b, D43) ·
> [[wieniec]] v1.3 (F7, D21) · [[style-b]] v1.50 (reguła 16, mapa usuwania).
> Makieta: `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/caa33748-6f1f-42bc-affe-bd98bc77539c/scratchpad/makieta-053.html`
> (spis na górze, panele 1–18; K1 i K2). Runda 1: makieta `9a0adb1f-…\scratchpad\makieta-053.html` — zastąpiona. **Bez zmiany schematu** (v15) — migracji nie ma.

### Mechanism — H (kandydat na ADR, zapisze `docs` przy zamknięciu)
**Usunięcie wierszy + „Cofnij” z zapamiętanych wierszy** (H), bez kosza. Przed usunięciem warstwa danych zbiera **migawkę** wszystkich wierszy, które
znikną albo się zmienią, potem usuwa je w jednej transakcji; „Cofnij” wstawia migawkę z powrotem w jednej transakcji (te same `id`, w kolejności kluczy
obcych — rodzice przed dziećmi) i przywraca zmienione kolumny (pinezka, `persons.clan_id`). Pliki zdjęć zostają na dysku do najbliższego sprzątania
(dziś: przy kopii i przy starcie — `sweepOrphanMedia`), więc „Cofnij” przywraca zdjęcia razem z wierszami. Dalsza siatka to kopia na Dysku (stan sprzed
usunięcia do następnej kopii — kopia w tle rusza po 10 min ciszy, `backupQuiet`).
- **Dlaczego nie kosz (S):** `deleted_at` w sześciu tabelach i filtr w każdym zapytaniu — każde zapytanie, które go zapomni, pokaże usuniętą osobę na
  drzewie albo w nazwie pokrewieństwa; plus migracja schematu przed wyjazdem. *Obali:* autor chce odzyskać rzecz po dniu.
- **Okno ryzyka:** „Zrób kopię teraz” w czasie paska „Cofnij” sprząta pliki usuniętych zdjęć — „Cofnij” przywróci wiersze bez pliku. Pasek trwa
  sekundy, kopia w tle czeka 10 min; przyjęte, w README.
- **Przy K1** mechanizm zostaje ten sam (migawka jest tania), tylko bez paska — „Cofnij” można dodać później bez zmiany warstwy danych.

### Scope diff
1. **`lib/data/deletion.dart` (nowy)** — każda funkcja w jednej transakcji, zwraca `DeletionSnapshot` (wiersze do wstawienia w kolejności kluczy obcych +
   kolumny do przywrócenia); każdy zapis przez drift, więc ekrany i kopia w tle słyszą zmianę:
   - `deleteGrave(db, id)` — **każdy grób:** `assertions` jego pochówków, `burials` grobu, `media` grobu (wiersze), wiersz grobu, potem
     `dropSectorIfUnused` dla jego kwatery (usunięta kwatera też w migawce); `previewGraveDeletion` — imiona osób (do 3 + „i N innych”), czy są zdjęcia,
     pinezka, adres;
   - `deleteCemetery(db, id)` — **każdy cmentarz:** jego groby jak `deleteGrave`, potem `cemetery_plans`, `sectors`, `media` cmentarza, wiersz;
     `previewCemeteryDeletion` — liczba grobów, liczba osób w nich (różnych), czy jest plan, kwatery, zdjęcie;
   - `removeFromGrave(db, personId)` — `assertions` pochówku i wiersz `burials` (osoba ma najwyżej jeden pochówek — D23); `events` typu `burial` zostaje;
   - `previewPersonDeletion(db, id)` i `deletePerson(db, id)` — jak w rundzie 1: nie dla „ja” (`StateError`); `assertions` jej zdarzeń, pochówków i więzi;
     `events`; `burials`; udział w związkach — związek bez nikogo przez `deleteFamily`; bycie dzieckiem; `residences`; `person_media`, a `media` bez nikogo
     (bez osoby, grobu i cmentarza) — wiersz; wiersz osoby;
   - `deleteGravePin(db, graveId)` — pięć kolumn pinezki → `null`; migawka: ich stare wartości;
   - `deleteClan(db, clanId)` — `persons.clan_id = null` u osób z tym rodem (`no_wreath` bez zmian), wiersz `clans`; migawka: wiersz rodu i lista osób;
     liczba do okna z `wreaths.countWith(clanId)` (jak F5);
   - `restoreDeletion(db, snapshot)` — wstawia wiersze (`InsertMode.insertOrAbort`, te same `id`) i przywraca kolumny w jednej transakcji.
2. **Wspólne elementy UI — `lib/app/widgets/deletion.dart` (nowy):** przycisk „Usuń …” (tekstowy, ikona `delete`, kolor tekstu, cel ≥ 48 dp — reguła 16),
   okno „Usunąć …?” (tytuł, treść, opcjonalna lista, „Anuluj” · „Usuń” w kolorze tekstu, błąd `ErrorLine`) i **pasek „Cofnij”** (K2: `SnackBar` z akcją
   na `ScaffoldMessenger` aplikacji, **4 s** — decyzja autora; przy czytniku ekranu albo „Czasie na działanie” nie znika sam — `dev` sprawdza zachowanie `SnackBar` z akcją
   w Flutter 3.41.1). Teksty z twardymi spacjami (reguła 6); tytuły bez odmiany imion.
3. **Sześć wejść** według specyfikacji: `cemetery_form.dart` / `cemetery_edit.dart` (15a) · okno „Popraw grób” w `grave_screen.dart` (3d) ·
   `person_form_screen.dart` (12a nad 12; 12a tylko przy osobie z grobem, 12 bez „ja”) · `pin_screen.dart` (12b — tylko przy poprawie pinezki, osobna
   linia nad „Anuluj” · „Zapisz pinezkę”) · `clan_screen.dart` (F7 — tylko ekran „Ród”, nie „Nowy ród”).
4. **Powrót i pasek:** cmentarz → mapa bez arkusza; grób → ekran cmentarza; osoba → ekran pod widokiem osoby (zamyka poprawę i widok); z grobu → tam, skąd
   otwarto poprawę (zwykle widok osoby, już „bez grobu”); pinezka → mapa cmentarza; ród → arkusz „Wieniec rodu”. Pasek na ekranie, na który się wraca;
   „Cofnij” → `restoreDeletion`; po przywróceniu cmentarza plan jest z migawki (bez pobierania).
5. **Pobieranie planów:** usunięty cmentarz w trakcie pobierania — `savePlan` sprawdza, że cmentarz istnieje (bez zmian); kolejka `PlanDownloads` go
   pomija przy następnej próbie (czyta brakujące od nowa — bez zmian).
6. **Bez zmian:** „Dodaj osobę” w grobie dalej wyszarza osobę z grobem (D23); `addExistingPersonToGrave` dalej odmawia osobie z pochówkiem — przeniesienie
   idzie przez „Usuń z grobu”.
7. **Wydanie:** `1.0.2+5`; README → akapit „Usuwanie i „Cofnij”” (mechanizm H, okno ryzyka, mapa usuwania jako link do [[style-b]] reguła 16).

### Files (likely)
`grobing-code`: `lib/data/deletion.dart` (nowy) · `lib/app/widgets/deletion.dart` (nowy) · `lib/app/home/cemetery_form.dart` · `lib/app/home/cemetery_edit.dart` ·
`lib/app/home/home_screen.dart` (pasek) · `lib/app/grave/grave_screen.dart` · `lib/app/grave/cemetery_screen.dart` (pasek) ·
`lib/app/grave/person_form_screen.dart` · `lib/app/person/person_screen.dart` (pasek po „Usuń z grobu”, odświeżenie) · ekran pod widokiem osoby (pasek
— przez wynik nawigacji) · `lib/app/grave/pin_screen.dart` · `lib/app/person/clan_screen.dart` · `pubspec.yaml`, `settings_screen.dart` (wersja) ·
`README.md`. Testy (`qa`): `test/data/deletion_test.dart`, widżety sześciu wejść i paska.

### AC → test / check
| AC | Test (`qa`) | Na emulatorze (agent) |
|---|---|---|
| AC-1 pusty cmentarz | `deletion_test` — plan, kwatery, zdjęcie znikają; migawka przywraca to samo (porównanie wierszy); okno w widżecie | pusty cmentarz → usunięcie → „Cofnij” |
| AC-2 cmentarz z grobami | `deletion_test` — groby, pochówki, zdjęcia nagrobków znikają, osoby z datami i rodziną zostają; po `restoreDeletion` **odcisk danych identyczny**; podgląd — liczby | cmentarz z 2 grobami → okno z liczbami → Osoby „bez grobu” → „Cofnij” |
| AC-3 grób | `deletion_test` — pusty i z osobami; kwatera bez strefy i grobów znika i wraca; widżet — imiona w oknie (do 3 + reszta) | grób z dwiema osobami → usunięcie → „Cofnij” |
| AC-4 osoba | `deletion_test` na wymyślonej rodzinie: Jan z żoną, synem, pochówkiem, zdjęciem wspólnym i własnym, zamieszkaniem, „źródłami” — po usunięciu Anna i Piotr w rodzinie, grób bez Jana, wspólne zdjęcie przy Annie, własne zniknęło; po `restoreDeletion` odcisk identyczny; „ja” — `StateError`; podgląd — liczby | drzewo przed i po, „Cofnij” |
| AC-5 kopia | odtworzenie kopii po usunięciu (test kopii) — wpisu nie ma, odcisk zgodny | — |
| AC-6 z grobu | `deletion_test` — pochówek i jego „źródło” znikają, data pochówku zostaje, osoba w `loadPeople` „bez grobu”; `addExistingPersonToGrave` do innego grobu przechodzi; widżet — 12a tylko przy osobie z grobem, nad 12 | Jan ze złego grobu → „Usuń z grobu” → „Dodaj osobę” w dobrym |
| AC-7 pinezka | `deletion_test` — kolumny puste, migawka przywraca te same wartości; widżet — 12b tylko przy poprawie | „Popraw pinezkę” → usunięcie → „Cofnij” |
| AC-8 ród | `deletion_test` — `clan_id` puste u wybierających, `no_wreath` bez zmian, wieńce z `wreaths` jak bez rodu; restore — te same wieńce; widżet — F7 tylko na „Ród” | ród u 3 osób → usunięcie → drzewo → „Cofnij” |

**Warstwa danych:** schematu nie zmienia (test migracji — nie); **próbne odtworzenie z kopii** — w AC-5 (test). Dostępność: `meetsGuideline` i
`expectEveryButtonTappable` w sześciu oknach i na pasku.

### Manual verification (stop #2)
**Agent na emulatorze** (przed stopem, zrzuty; `Grobing_Restore` — stan sprzed demo z `_pokaz`, demo z powrotem po pozycji): wiersze kolumny „Na
emulatorze”; tekst 200% na 360 dp (`wm size` i gęstość w zapisie) — okno cmentarza z grobami, okno osoby z pięcioma pozycjami, panel pinezki z „Usuń
pinezkę”; pasek przy TalkBack — nie znika sam; przegląd `ui` (subagent).
**Autor — odczucie (emulator, najwyżej 3):**
1. usuń osobę z powiązaniami z wymyślonej rodziny — czy okno mówi wystarczająco, żeby wiedzieć, co zniknie?
2. przenieś osobę do innego grobu, nie wiedząc z góry, gdzie to jest — czy znajdziesz „Usuń z grobu” (D29 *Obali*)?
3. (K2) usuń cmentarz z grobami i „Cofnij” — czy wszystko wróciło tak, jak było?

### Out of scope
- scalanie duplikatów — [[ISSUE-054-merge-two-people]];
- przeniesienie grobów do innego cmentarza, scalanie cmentarzy, scalanie rodów — [[cmentarze]] D40 / [[wieniec]] D21 *Obali*;
- „Cofnij” dla usunięć, które już są (związek, zamieszkanie, zdjęcia) — zamieszkanie i zdjęcia cofa „Odrzuć” poprawy, związek ma okno; kandydat na
  spójność po pozycji;
- kosz z odzyskiwaniem po czasie (S);
- usunięcie „ja”.

## Dev report (`dev`, 2026-10-23)

### Built
- **`lib/data/deletion.dart`** (nowy): `deleteCemetery` (każdy — groby jak `deleteGrave`, potem plan, kwatery, zdjęcie), `deleteGrave` (każdy — pochówki z
  „źródłami”, zdjęcie nagrobka, wiersz; kwatera bez strefy i grobów znika jak przy zmianie adresu), `removeFromGrave`, `deletePerson` (nie „ja”; związek,
  któremu brakuje partnera albo dwóch osób, znika cały — jak „Usuń związek”, reguła z `saveFamily`), `deleteGravePin`, `deleteClan`; podglądy do okien
  (`preview…`, `graveLabel`); `DeletionSnapshot` + `restoreDeletion` — wiersze wstawiane z tymi samymi `id` w kolejności kluczy obcych, wiersze zmienione w
  miejscu (pinezka, `persons.clan_id`, zdjęcie, na którym ktoś jest, a znika jego grób albo cmentarz — zostaje bez grobu) zapisywane z powrotem. Zdjęcie
  grobu/cmentarza, na którym ktoś jest, zostaje przy osobie (bez grobu), reszta znika.
- **`lib/app/widgets/deletion.dart`** (nowy): `DeleteButton`, `DeletionActions`, `confirmDeletion` (okno z błędem w środku), `DeletionText`/`Note`/`List`,
  `andList`/`withWord` („z”/„ze”, twarde spacje), `showUndoBar` (K2: 4 s albo „Czas na działanie”; przy czytniku ekranu nie znika sam).
- Wejścia: [[cmentarze]] 15a (`cemetery_form.dart`, `cemetery_edit.dart`; ekran główny zamyka arkusz, „Cofnij” go otwiera; ekran cmentarza się zamyka),
  [[grob]] 3d (`GraveDialog.onDelete`, widok grobu się zamyka), [[wpis-osoby]] 12a/12 (`person_form_screen.dart`; „ja” z faktem; trasy widoku osoby mają
  nazwę `PersonScreen.viewRoute`, żeby „Usuń osobę” zamknęło poprawę i widok), [[cmentarz]] 12b (`pin_screen.dart`, tylko przy poprawie), [[wieniec]] F7
  (`clan_screen.dart`, `ClanDeleted`). Wersja **1.0.2+5**; README → *Baza danych* → „Usuwanie i „Cofnij””. **Bez zmiany schematu** (v15).

### Found on the emulator (fixed before qa)
1. **`SnackBar` z akcją we Flutterze 3.41.1 nie znika wcale** — `persist` domyślnie `true`, gdy jest akcja (opis klasy o TalkBack jest nieaktualny); pasek
   wisiał ponad minutę. Teraz `persist` tylko przy czytniku ekranu (`MediaQuery.accessibleNavigation`), a czas z `recommendedTimeout` — zmierzone na
   urządzeniu: 4 s, a z „Czasem na działanie” 30 s — 30 s (próbki `uiautomator` co ok. 2 s: jest do 30 s, nie ma od 32 s).
2. **Przyciski okna nie mieszczą się w jednym wierszu już przy 100% na 411 dp**; `OverflowBar` stawiał wtedy „Usuń cmentarz” z prawej, nad „Dalej” →
   `DeletionActions` zawsze w dwóch liniach (odstępstwo 2).
3. **Pusty cmentarz bez planu w OSM: „zniknie z mapy razem z planem”** — wiersz „W OpenStreetMap nie ma planu” liczył się jako plan; podgląd liczy tylko
   `PlanStatus.ok`.

### Deviations (do przeglądu `ui`)
1. **Pasek „Cofnij”: pływający, na powierzchni z obrysem** — specyfikacja podaje tekst w kolorze tekstu i „Cofnij” w akcencie, a domyślne paski aplikacji
   są jasne (`inverseSurface` = kolor tekstu), na których bursztyn nie ma kontrastu.
2. **„Usuń …” zawsze w pierwszej linii z lewej, „Anuluj · Dalej/Zapisz” pod spodem z prawej** ([[cmentarze]] 15a, [[grob]] 3d: „w wierszu… z lewej”,
   zawija się przy 200%) — trzy przyciski nie mieszczą się w jednym wierszu na telefonie (znalezisko 2).
3. **„Usuń ród” zamyka też arkusz „Wieniec rodu”**, a pasek jest na poprawie wpisu ([[wieniec]] F7: „w arkuszu pasek”) — arkusz jest modalny i
   zasłaniałby pasek pokazany pod nim.
4. **Nazwa grobu bez nazwy w oknach osoby:** „pochówkiem w grobie „<nazwa>”” albo „…w grobie na cmentarzu „<cmentarz>”” (spec: „pochówkiem w „<grób>””
   — tytuł grobu bez nazwy to nazwa cmentarza, a nazw nie odmieniamy).

### Known edges
- „Cofnij” wyjęcia z grobu **po** dodaniu tej osoby do innego grobu wkłada ją z powrotem do pierwszego — osoba w dwóch grobach (D23). Okno to 4 s, przy
  czytniku — do dotknięcia.
- Pasek przez swój czas przykrywa dolny przycisk ekranu („Dodaj grób”, „Dodaj osobę”, przypięte „Zapisz” poprawy).
- Przy 200% na 360 dp okno cmentarza z grobami przewija się, a notka „Osoby z tych grobów (N) zostają…” jest pod krawędzią.
- Długa nazwa cmentarza w pasku łamie się przed liczbą: „…Wymyślony / 2”.” (twarda spacja w nazwie — dane, nie tekst aplikacji).
- **Poza pozycją:** ✎ „Popraw cmentarz” w arkuszu mapy przy 200% na 360 dp ma węzeł 48 × 96 px (24 dp wysokości).

### Emulator pass (`Grobing_Restore`, build profile 1.0.2+5, zrzuty w katalogu sesji `caa33748-…\scratchpad\emu053\shots\`)
| AC | Wynik |
|---|---|
| AC-1 | pusty cmentarz: „„Cmentarz Wymyślony 2” zniknie z mapy.” → brak znicza → „Cofnij” → wraca z wierszem planu (*nie ma w OSM*) |
| AC-2 | cmentarz z 2 grobami: okno z „2 grobami, z ich zdjęciami i adresami”, „kwaterami”, „Osoby z tych grobów (3)…” → mapa bez znicza → „Cofnij” → **odcisk danych identyczny** (`1c29…dac0b` przed i po), arkusz otwarty |
| AC-3 | grób z dwiema osobami: okno z imionami → grób znika z listy, osoby w „Bez grobu”; pasek znika sam po 4 s. „Cofnij” grobu sprawdzone pośrednio (AC-2 przywraca groby tą samą drogą) |
| AC-4 | osoba z 1 związkiem, dziećmi i 2 zdjęciami tylko jej: okno → lista Osób bez niej → „Cofnij” → **odcisk identyczny** (`fdec…7b77`, z plikami zdjęć); osoba z 2 związkami i pochówkiem — okno z obu związkami i notką o wspólnych zdjęciach |
| AC-5 | nie na urządzeniu — test kopii (`qa`) |
| AC-6 | osoba z usuniętego grobu w „Bez grobu” → jednym dotknięciem do innego grobu; „Usuń z grobu” → widok osoby z paskiem → „Cofnij” → „Pochówek: …” wraca |
| AC-7 | pinezka GPS ±5 m: „Usuń pinezkę” w osobnej linii → okno → bez znicza, „bez pinezki” → „Cofnij” → ta sama pinezka („Teraz: GPS ±5 m · 23.10.2026”) |
| AC-8 | ród u 4 osób: okno → arkusz się zamyka, wieniec osoby „Brak” (reguła bez rodu); pasek 30 s przy „Czasie na działanie”. „Cofnij” rodu na urządzeniu nie dotknięte |
| „ja” | brak „Usuń osobę”, fakt „To Ty („ja”)…”; osoba bez grobu — bez „Usuń z grobu” |
| 200% / 360 dp | `font_scale 2.0`, `wm size 720x1280`, `wm density 320`: okno cmentarza i okno osoby przewijają się, przyciski 48 dp; **panel pinezki przy 200% nie sprawdzony** (cmentarz bez punktu) — do testu widżetu |
| semantyka | każdy „Usuń …”, „Usuń”, „Anuluj”, „Cofnij” — `clickable` w `uiautomator`; „Cofnij” 70 × 48 dp |
| TalkBack | nie na urządzeniu — `persist` przy `accessibleNavigation` do testu widżetu (`qa`) |

**Stan emulatora:** `Grobing_Restore` ma teraz stan sprzed demo z `_pokaz` z buildem 1.0.2 i wymyślonymi partiami 2–3, zmienionymi testami (usunięte: grób,
dwie osoby, ród); „Czas na działanie”, tekst i ekran z powrotem domyślne. **Demo zapisane przed pozycją** w `emu053\stan-przed-053.tar` +
`stan-przed-053-base.apk` (to samo co `_pokaz\…\demo-app-data-2026-10-21.tar`) — wgrać z powrotem po `qa`. Pliki zdjęć usuniętych bez „Cofnij” czekają na
sprzątanie (kopia albo start po godzinie).

### Fixed after the ui review (`dev`, 2026-10-23)
- **MAJOR — „Popraw cmentarz” przy 200% z klawiaturą:** przyciski rysowały się na polach („Usuń cmentarz” na „Nazwie”) — okno nie miało `scrollable`
  (`cemetery_form.dart`). Teraz tytuł i pola się przewijają, przyciski pod nimi; na emulatorze przy 200% / 360 dp z klawiaturą bez nakładania (zrzut 71).
- **MINOR 3 — okno „Usunąć …?”:** treść pod tytułem przewija się z paskiem zawsze widocznym (`Scrollbar(thumbVisibility: true)`, zrzut 72).
- **MINOR 4, 5 — grób bez nazwy:** „Ten grób zostanie bez pinezki.” / „Ten grób zniknie z cmentarza…” zamiast imion albo „Grób” w cudzysłowie.
- **MINOR 6 — nieudane „Cofnij”:** pasek tej samej postaci z „Cofnij” jeszcze raz („Nie udało się cofnąć.”).
- **D23 — „Cofnij” nie kładzie osoby w dwóch grobach:** `restoreDeletion` odmawia (`RestoreRefused`), gdy osoba z migawki leży już w innym grobie, i nic
  nie zapisuje; pasek: „Nie da się cofnąć — ta osoba leży już w innym grobie.” (przypadek z *Known edges*).
- **MINOR 2 — pasek nad przypiętym przyciskiem ekranu — nie poprawione:** dolny odstęp zależałby od każdego ekranu powrotu (lista grobów, arkusz grobu,
  Osoby, poprawa wpisu); do oceny autora na stopie #2 (krok 3) — kandydat na drobną pozycję.

## Verification (`qa`, 2026-10-23)

### Tests — 1044 → zielone, `flutter analyze` i `dart format` czyste
- **`test/data/deletion_test.dart`** (nowy, 15 testów): AC-1 (pusty cmentarz z planem, kwaterą i zdjęciem; „nie ma w OSM” to nie plan), AC-2 (cmentarz z
  grobami — osoby, zdarzenia i rodziny zostają), AC-3 (grób z osobami; kwatera bez strefy wraca z tym samym `id`; zdjęcie nagrobka z osobą zostaje przy niej),
  AC-4 (podgląd; ojciec z dwoma związkami — związki matki i partnerki zostają; portret tylko matki znika, ślubne zostaje; związek bez dwóch osób znika cały;
  „ja” — `StateError`, nic nie zmienione), AC-6 (pochówek i jego „źródło”, data pochówku zostaje, przeniesienie do innego grobu; „Cofnij” po przeniesieniu —
  `RestoreRefused`, nic nie zapisane), AC-7 (pinezka z datą i dokładnością), AC-8 (wieńce wracają do reguły; „Bez wieńca” zostaje), dwa usunięcia cofnięte
  w odwrotnej kolejności. **Po każdym „Cofnij” odcisk danych identyczny** (`readDataState`, z plikami zdjęć).
- **AC-5** — `test/backup/restore_service_test.dart`: kopia zrobiona po usunięciu osoby i grobu odtwarza się bez nich, z odciskiem telefonu po usunięciu;
  dziecko z usuniętego grobu jest w aplikacji bez grobu, matka ma związek z dzieckiem.
- **`test/app/deletion_screens_test.dart`** (nowy, 10 testów): „Nowy grób” bez „Usuń grób”, w poprawie — pierwsza linia z lewej; AC-3 na ekranie — okno z
  imionami, powrót pod widok grobu, **pasek znika po 4 s**; 12a nad 12, osoba bez grobu bez 12a, „ja” z faktem; AC-4 i AC-6 na ekranie z „Cofnij”; F7 tylko na
  „Ród”, z arkusza — ekran i arkusz zamknięte, pasek pod nimi; 15a z wywołaniami `onDeleted`/`onRestored`; **czytnik ekranu — pasek po 10 s dalej jest**;
  **„Czas na działanie” 10 s** (kanał `recommendedTimeout`, pytanie jak o przyciski) — pasek 10 s, nie 4; okno i pasek — `androidTapTargetGuideline`,
  `labeledTapTargetGuideline`, `expectEveryButtonTappable`.
- **`test/app/grave/pin_screens_test.dart`** (+2): AC-7 na ekranie — „Usuń pinezkę” w osobnej linii nad „Zapisz pinezkę”, okno, pasek, „Cofnij” daje tę samą
  pinezkę; nowa pinezka bez „Usuń pinezkę”; **panel przy 200% na 360 × 640 dp** — cały, bez przepełnienia, każdy przycisk z akcją (luka z przejścia `dev`).
- **`test/app/person/residence_screens_test.dart`** (zmieniony test retro 3 R2): koniec formularza się wydłużył — przeciągnięcie o 6 dp zaczynało się na
  „Dodaj partnera” i otwierało jego arkusz jak dotknięcie. Poprawa sprawdzana teraz na wysokim ekranie, cała naraz — wytyczne dotyku obejmują przy tym
  „Usuń z grobu” i „Usuń osobę”.

### ui review (subagent, 2026-10-23)
0 BLOCKER · 1 MAJOR · 5 MINOR. MAJOR (okno cmentarza przy 200% z klawiaturą) i MINOR 3–6 poprawione przed stopem (*Fixed after the ui review*), MINOR 2 —
na stop #2. Wszystkie 4 odstępstwa `dev` przyjęte i zapisane: [[style-b]] v1.52 (reguła 16, *Token roles*, *Measurement* — pasek: tekst 10,02:1, „Cofnij”
8,04:1, obrys 3,40:1), [[cmentarze]] v3.2 (D41), [[grob]] v10.2 (D30), [[wieniec]] v1.4 (D22), [[wpis-osoby]] v7.2, [[cmentarz]] v9.3. Kandydaci spoza pozycji:
twarda spacja przed „—” w całej aplikacji; ✎ arkusza cmentarza przy 200% na 360 dp chowa się pod wyszukiwarką (arkusz wyższy niż miejsce — zrzut 70).

### Family data
Zmiany w trzech repo bez plików danych (`*.db`, kopie, eksporty, zdjęcia); w dodanych liniach kodu i testów tylko rdzenie wymyślone (Wymyśl-, Zmyśl-, Testow-,
Przykład-, „Próbny”, „Wymyślin”) i role („Ojciec”, „Matka”, „Rodzic”). Na emulatorze jest wpis autora z jego stanu sprzed demo i miasta z wymyślonych zamieszkań
— zrzuty z nimi (10, 30, 34, 35, 54) nie poszły do przeglądu ani do vaulta. Pozycja bez sieci — logcat bez sprawdzania współrzędnych (3b nie dotyczy).

### Stop #2 (2026-10-23) — autor: *„ok (przy czym zapomniałem żeby kliknąć cofnij)”*
Emulator `Grobing_Restore`, build 1.0.2, wymyślona partia 4. Sprawdzone na urządzeniu (kopia bazy z `run-as`, tylko wiersze partii 4, kopia usunięta):
- **krok 1 (usuń osobę) — ok, ze śladem:** „Ojciec 4” usunięty;
- **krok 2 (przenieś osobę, D29 *Obali*) — ok, bez śladu:** stanu nie da się rozróżnić — krok 3 usunął cmentarz z oboma grobami, więc „Dziecko 4” i tak jest
  bez grobu. Autor nie zgłosił, że szukał „Usuń z grobu” w „Popraw grób” — D29 zostaje;
- **krok 3 (usuń cmentarz z grobami) — ok, ze śladem:** „Cmentarz Wymyślony 4” usunięty, jego cztery osoby w aplikacji bez grobu (D40). **„Cofnij” autor nie
  dotknął** — sprawdzone przez agenta na emulatorze (AC-1, AC-2, AC-4, AC-6, AC-7) i w testach (odcisk identyczny). Do paska nad przyciskiem (MINOR 2) autor
  bez uwag.

**Do [[ISSUE-032-mvp-install]] → *Hand checks*:**
- **B** — krok 2: przeniesienie osoby do innego grobu — „ok” bez śladu na urządzeniu.
- **B** — „Cofnij” w ręce autora — nie dotknięte na stopie #2 (agent i testy — tak).
- **B** — pasek „Cofnij” przy TalkBack (nie znika sam) — nieprzetestowane na żywo, tylko test widżetu.
- **B** — pasek przez 4 s nad przypiętym przyciskiem ekranu (MINOR 2 przeglądu `ui`) — w używaniu; kandydat na drobną pozycję, gdy przeszkodzi.

**Werdykt `qa`: APPROVED (self-check, z uwagami)** — każde AC z testem (AC-5 kopią), przejście `dev` i agenta na emulatorze, przegląd `ui` z MAJOR poprawionym
przed stopem, stop #2 „ok”. Uwagi: MINOR 2 nie poprawiony; panel pinezki i TalkBack przy 200% / czytniku — tylko testy; „Cofnij” po przeniesieniu osoby
odmawia (D23) zamiast kłaść ją w dwóch grobach. Stan emulatora: demo z powrotem (`stan-przed-053.*`), stan z testów w `emu053\stan-po-053.tar` (wymyślone
partie i wpisy autora sprzed demo — do kosza z katalogiem sesji).
