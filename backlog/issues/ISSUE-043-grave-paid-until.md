---
title: "ISSUE-043 — Grave fee „paid until” at the bottom of the grave view (brief S4)"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-16
verdict-reviewer: self-check
source: "brief §5 S4 (G4) · propozycja `pm` w `/pm` 2026-10-16, autor: „to jest dobre — można dodać na samym dole profilu grobu” · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-16
---

# ISSUE-043 — „Opłacone do” przy grobie

> Brief §5 S4: *grave fee „paid until” date + reminder* — grób ziemny bez odnowionej opłaty (co 20 lat) zarządca może zlikwidować; to jedyny
> sposób, żeby stracić **sam grób**, a nie wiedzę o nim. Warunek z briefu („przed najwcześniejszą zapisaną datą”) da się spełnić tylko, gdy daty
> są zapisane — Wszystkie Święte to okazja: naklejki z opłatą na grobach, otwarte biuro zarządcy. Autor: *„można dodać na samym dole profilu
> grobu”*. **Przed instalacją**, bo zmienia bazę.

## What to build
- W widoku grobu, **na samym dole**: „Opłacone do” — data (zwykle sam rok) albo „nie wiadomo”; poprawa tam, gdzie dziś „Popraw grób”
  (projekt: `ui`, zmiana specyfikacji [[grob]]).
- Kolumna w `graves` — dziś jej nie ma (`database.dart`: „still without the grave fee (S4)”), choć [[data-model]] wymienia ją w *Grave*.
- ~~`⚠️ OPEN` na stop #1~~ — **✅ rozstrzygnięte przez autora w `/pm` 2026-10-16: wariant B — sama data** (*Implementation plan* → *Scope decided*):
  1. **przypomnienie** (brief: „+ reminder”) — powiadomienie wymaga na Androidzie 13 uprawnienia `POST_NOTIFICATIONS`; z nim czy bez? → **nie teraz**;
  2. **kto płaci** — brief: „who pays is recorded, not managed”; pole tekstowe czy bez? → **bez pola**.

## Acceptance Criteria
- **AC-1** *Given* grób *When* wpisuję „opłacone do 2031” *Then* na dole profilu grobu widać „Opłacone do 2031”.
- **AC-2** *Given* grób bez wpisu *Then* dół profilu nie udaje daty (stan „nie wiadomo” albo brak wiersza — decyzja `ui`).
- **AC-3** *Given* kopia z wersji sprzed tej pozycji *When* odtwarzam ją w nowej *Then* dane są kompletne (test migracji, próbne odtworzenie).

## Notes
- [[EPIC-002-wizyta]] (UJ-001 krok 4 — grób). Przypomnienie, jeśli wejdzie: dopiero po decyzji o uprawnieniu.

## Implementation plan
> `planning`, 2026-10-16. **Pozycja z ekranem (zmiana istniejącego):** specyfikacja [[grob]] **v8**: element 7 (wiersz „Opłacone do” na dole
> widoku), 3c (pole w oknie „Popraw grób”), D15–D19, szkic v8 z wariantami W1/W2. Wytyczne [[style-b]] v1.32, bez nowych tokenów. Makiety nie ma,
> bo ekran nie jest nowy. Warianty pokazuje szkic ASCII w specyfikacji (*Sketch* → v8). Bez US (task-level, jak ISSUE-023/024/025), krok
> UJ-001 · 4, brief §5 S4 · G4.

> **Stop #1 — 2026-10-16, autor: *„Tak”*** na pytanie „W1 czy W2? („tak” = W1)”. **W1:** grób bez daty ma wiersz „nie wiadomo” i „Wpisz”.
> Decyzje z planu przyjęte.

### Scope decided (author, `/pm` 2026-10-16)
**Wariant B — sama data „opłacone do”.** Bez pola „kto płaci”. Bez przypomnienia: nie zmienia bazy, więc przyjdzie później aktualizacją ze sklepu,
przed najwcześniejszą zapisaną datą (brief S4: *„before the earliest recorded fee expiry”*). Oba `⚠️ OPEN` z *What to build* zamknięte.

### Decision for stop #1 (author) — jedno pytanie
- **W — grób bez daty** ([[grob]] D16, AC-2): **W1 (rekomendacja `ui`)** — wiersz zawsze, bez daty „nie wiadomo” i przycisk „Wpisz” (skrót do okna z
  fokusem w polu). Widać, przy których grobach daty jeszcze nie ma. Koszt: jedna szara linia na ok. 50 grobach do czasu wpisania · **W2** —
  wiersz tylko z datą, a wpis wyłącznie pod ✎ przy tytule. Na grobie bez daty nic nie mówi, że takie pole jest.

### Decisions taken in the plan (visible at stop #1, no question)
- **Model — trzy kolumny w `graves`:** `paid_until_year`, `paid_until_month`, `paid_until_day`, wszystkie opcjonalne. To ten sam kształt co daty
  zamieszkań (`residences.from_*`) i `PartialDate` w kodzie. Odrzucone:
  - tekst ISO (`2031-03`) — drugi sposób zapisu dat w bazie;
  - wiersz w `events` — `events` to zdarzenia osoby i rodziny (`EventType`: urodzenie, zgon, pochówek, ślub…), a opłata dotyczy grobu.

  **Bez ADR**, bo to jedna opcjonalna wartość istniejącego rekordu, jak data pinezki w v12 ([[ISSUE-029-pin-on-site-gps]]). [[data-model]] wymienia ją
  w *Grave* od kick-offu. Bez twierdzeń (D28). Schemat **v13 → v14** (`addColumn` ×3).
- **Walidacja:** `parsePartialDate` dostaje opcjonalną górną granicę roku. **Domyślna zostaje: daty osoby dalej nie przyjmują przyszłości** (test
  regresji). Pole opłaty przyjmuje lata od 1500 do bieżącego + 50 i ma dwa komunikaty: zły zapis i rok dalej niż za 50 lat ([[grob]] 3c, D18).
- **Zapis w oknie: wszystko albo nic.** Zła data w 3c → nic się nie zapisuje (ani nazwa, ani adres), a okno zostaje. Dobra → nazwa, adres i data
  w jednej transakcji `setGraveDetails`. Zapis zamawia kopię w tle jak każdy.
- **Emulator `Grobing_Restore`:** tak jak w [[ISSUE-042-places-of-residence]]. Przed instalacją robimy kopię obecnych danych, a cmentarz dodany
  tam 2026-10-16 poza agentem zostaje. Po instalacji nad v13 sprawdzamy migawkę `pre-update/grobing-v13.db` ([[ISSUE-041-google-play-and-safe-update]]).

### Steps (`dev`)
1. **Schemat v14** w `lib/data/database.dart`:
   - trzy kolumny w `Graves` i krok `_from13To14` (`addColumn` ×3, bez zmiany wierszy);
   - `currentSchemaVersion = 14`, komentarz nagłówka (bez „still without the grave fee”);
   - `make-migrations` (schemat v14, testy generowane), `build_runner`.
2. **Dane** — `lib/data/graves.dart`:
   - `GraveDetail.paidUntil` (`PartialDate?`) z `loadGrave`;
   - `setGraveDetails(…, paidUntil:)` — `null` czyści datę, zapis w tej samej transakcji co nazwa i adres.
3. **Data** — `lib/app/dates.dart`: górna granica roku w `parsePartialDate` (domyślnie bieżący rok) i rozróżnienie „zły zapis” / „za daleko” dla
   pola opłaty.
4. **Ekran** — `lib/app/grave/grave_screen.dart` według [[grob]] v8:
   - element 7 pod „Dodaj osobę” — W1 albo W2 według stopu #1;
   - wiersz faktu jak „Daty” w [[osoba]] 8, etykieta nad wartością przy dużym tekście;
   - „Wpisz” pod wartość, gdy się nie mieści;
   - semantyka wiersza i przycisku („Wpisz datę opłaty”).

   `GraveDialog`:
   - pole 3c, klawiatura `TextInputType.datetime`;
   - Miejsce `next` → 3c `done` = „Zapisz”;
   - wejście z „Wpisz” — fokus w 3c i przewinięcie do pola (dziś `focusAddress: bool`, będzie cel fokusu: nazwa · kwatera · opłata);
   - błąd pod polem (`ErrorLine`).
5. **Dane wymyślone** — `lib/dev/fictional_data.dart`: kilka grobów z datą (przyszła, miniona, `mm.rrrr`) i reszta bez daty. Wszystkie stany
   [[grob]] v8 da się wtedy pokazać na emulatorze.
6. **README** `grobing-code` → *Baza danych*: v14.
7. **Przejście AC na emulatorze** (stała lista `dev`, retro 3):
   - każdy stan v8 ze zrzutem: z datą, bez daty, okno z „Wpisz”, zła data (oba komunikaty);
   - tekst 200% na 360 dp: wiersz 7 i „Wpisz”, okno z klawiaturą przewinięte do 3c;
   - semantyka i cel dotyku 48 dp;
   - migracja nad danymi: liczby wierszy przed i po, migawka v13.

### Files likely touched
`grobing-code`:
- schemat: `lib/data/database.dart`, `database.g.dart`, `database.steps.dart`, `drift_schemas/grobing/drift_schema_v14.json`,
  `test/drift/grobing/generated/*` (generowane);
- kod: `lib/data/graves.dart`, `lib/app/dates.dart`, `lib/app/grave/grave_screen.dart`, `lib/dev/fictional_data.dart`, `README.md`;
- testy (`qa`): `test/drift/grobing/migration_test.dart`, `test/data/graves_test.dart`, `test/app/dates_test.dart`,
  `test/app/grave/grave_screens_test.dart`, `test/backup/restore_service_test.dart`.

`grobing-vault` (`docs` przy zamknięciu):
- `04_ARCHITECTURE/data-model.md` — *Grave*: kolumny opłaty, v14;
- `04_ARCHITECTURE/backup-format.md` — od schematu v14 data opłaty w `graves`; format v1 bez zmian.

### AC mapping
| AC | Kroki | Dowód |
|---|---|---|
| AC-1 — „opłacone do 2031” widać na dole | 1–4 | test zapisu i odczytu `paidUntil` (rok, `mm.rrrr`, `dd.mm.rrrr`, czyszczenie); test widżetu: „Wpisz” (W1) albo ✎ → „2031” → `done` → wiersz „2031”; poprawa na „03.2031”; zrzut |
| AC-2 — bez wpisu dół nie udaje daty | 4 | test widżetu: grób bez daty — „nie wiadomo” i „Wpisz” (W1) albo brak wiersza (W2), żadnej daty; zrzut |
| AC-3 — kopia sprzed pozycji odtwarza się kompletna | 1 | test migracji v13 → v14 z wymyślonymi danymi (każdy wiersz każdej tabeli bez zmian, kolumny opłaty puste); generowane v1…v13 → v14; odtworzenie kopii v13 w v14 (`restore_service_test`, wzór v12 z ISSUE-042); próbne odtworzenie kopii v14 z datą na drugim emulatorze, odcisk zgodny (odcisk liczy wszystkie kolumny — `data_state.dart`) |

### Tests (`qa`)
- **Migracja:** v13 → v14 z danymi (graves z nazwą, adresem i pinezką bez zmian, opłata pusta). Wygenerowane testy z każdej wersji do v14.
- **Odtworzenie:** kopia v13 w aplikacji v14 przechodzi przez migrację. Kopia v14 z datą wraca z tą samą datą.
- **`graves.dart`:** zapis, poprawa i czyszczenie daty. Data w tej samej transakcji co nazwa i adres.
- **`dates.dart`:**
  - pole opłaty przyjmuje „2031”, „03.2031”, „31.12.2031” i rok bieżący + 50;
  - „2301” → komunikat „za daleko”, „13.2031” → „Nie rozumiem tej daty…”;
  - **regresja:** data osoby z przyszłości dalej odrzucona.
- **Widżety:**
  - element 7 z datą (także miniona — bez koloru błędu) i bez daty (W1/W2);
  - okno: Miejsce `next` → 3c, „Wpisz” → fokus w 3c;
  - zła data → okno zostaje, nic się nie zapisuje;
  - semantyka „Opłacone do 2031” i „Wpisz datę opłaty”;
  - `meetsGuideline` (retro 3, R2), tekst 200%.
- **Pełny przebieg:** `flutter test --timeout 120s`, `flutter analyze`, `dart format`.
- **Przegląd `ui`** (subagent) przed stopem #2.

### Manual verification
**Agent na emulatorze (przed stopem #2):**
- krok 7 z *Steps*: zrzuty stanów, 200% na 360 dp, migracja v13 → v14 nad danymi (liczby wierszy, migawka v13);
- próbne odtworzenie kopii v14 na drugim emulatorze, po kolei, nie równolegle (RAM). Odcisk musi być zgodny.

**Autor — odczucie (najwyżej 3, na emulatorze):**
1. Wymyślony grób bez daty, przewiń na dół. Czy wiersz „Opłacone do” jest na właściwym miejscu i nie przeszkadza (W1: z „nie wiadomo” i „Wpisz”)?
2. Wpisz rok z wyobrażonej naklejki („Wpisz” albo ✎). Czy to dość szybkie przy ok. 50 grobach?

### Out of scope
- przypomnienie: powiadomienie i oznaczenie opłaty, która minęła ([[grob]] D19) — później, aktualizacją;
- „kto płaci”;
- stan „bez terminu” (D19);
- data opłaty na karcie grobu w [[cmentarz]] i w [[osoba]];
- dopisek „ok.” przy dacie opłaty (D18);
- eksport GEDCOM (eksportem jest kopia, [[ADR-018-export-is-the-backup]]).

### Obali (falsifiers)
- Na stopie #2 wiersz przy każdym grobie wygląda jak upominanie → W2 ([[grob]] D16).
- Okno przy tekście 200% z klawiaturą nie pokazuje pola 3c po „Wpisz” → poprawka w `dev` przed stopem. Gdyby się nie dało, okno na cały ekran:
  decyzja przy drugim oknie z tym problemem ([[grob]] *Open*, luka v6.1).
- W trakcie wyjazdu część grobów okazuje się „bez terminu” → pozycja z nową kolumną i migracją na prawdziwych danych (D19).
- Migracja albo odtworzenie kopii v13 nie przechodzi → STOP przed jakimkolwiek commitem.

### Sources
brief §5 S4 i §5a G4 (opłata za grób ziemny co 20 lat; źródła w briefie: money.pl, Bankier) · [[grob]] v8 · [[data-model]] → *Grave* ·
wzór kolumn daty: `Residences` (`lib/data/database.dart`, [[ADR-020-residences-place-in-the-row]]).

## Dev report
> `dev`, 2026-10-16. Flutter 3.41.1 (przypięty). Kroki 1–7 z planu wykonane. `flutter analyze` czyste, `dart format` zrobiony. Istniejące testy
> migracji, grobów, kwater, dat i ekranów grobu zielone (139, w tym wygenerowane v1…v13 → v14). Testów nie pisałem — to `qa`.

### Changed (`grobing-code`)
- **Schemat v14:**
  - `lib/data/database.dart`: `Graves.paidUntilYear` / `paidUntilMonth` / `paidUntilDay` (opcjonalne), krok `_from13To14` (`addColumn` ×3),
    `currentSchemaVersion = 14`, komentarz nagłówka;
  - generowane: `database.g.dart`, `database.steps.dart`, `drift_schemas/grobing/drift_schema_v14.json`, `test/drift/grobing/generated/schema.dart`
    i `schema_v14.dart`.
- **Dane** — `lib/data/graves.dart`:
  - `GraveDetail.paidUntil` (`PartialDate?`) z `loadGrave` — dzień tylko z miesiącem;
  - `setGraveDetails(…, paidUntil:)` zapisuje całe okno w jednej transakcji, `null` czyści.
- **Daty** — `lib/app/dates.dart`:
  - `parsePartialDate(…, latestYear:)`, domyślnie bieżący rok, więc daty osoby bez zmian;
  - `readPaidUntil` — puste = brak daty; do bieżącego roku + 50 (`paidUntilYearsAhead`); dwa komunikaty;
  - `badDateMessage` przeniesione z `date_block.dart`, ten sam tekst.
- **Ekran** — `lib/app/grave/grave_screen.dart`:
  - element 7 `_PaidUntilRow` (W1), pod „Dodaj osobę” po 24 dp;
  - `GraveField { name, sector, paidUntil }` zamiast `focusAddress: bool`;
  - pole 3c w `GraveDialog`: `TextInputType.datetime`, filtr cyfr i separatorów, ≤ 10 znaków; Miejsce `next` → 3c `done` = „Zapisz”;
  - zła data → `ErrorLine` pod polem, nic się nie zapisuje.
- **Dane wymyślone** — `lib/dev/fictional_data.dart`: nazwany grób każdej paczki ma datę na zmianę `2031` · `03.2019` · `31.12.2045`, grób z adresem
  nie ma żadnej.
- **README** → *Baza danych*: wpis „Opłata za grób (schemat v14)”.

### Emulator pass (`Grobing_Restore`, build profile `0.9.0`, `--split-per-abi`, `FRAME_LOG`)
Zrzuty: `C:\Users\user\AppData\Local\Temp\claude\c--Programowanie-Grobing-grobing-agents\6983a70d-0d04-4682-9976-309892f41b6d\scratchpad\emu043\` (pliki `01`–`17`).

- **Przed instalacją:** kopia danych aplikacji `data-before.tar` i bazy `grobing-before.db` w tym samym katalogu. Na emulatorze są tylko wymyślone
  osoby oraz cmentarz dodany 2026-10-16 poza agentem (zostaje).
- **Migracja v13 → v14 nad danymi** (liczby z kopii bazy przed i po):
  - wszystkie tabele bez zmian: 108 osób, 177 zdarzeń, 283 twierdzenia, 38 rodzin, 5 zamieszkań, 1 cmentarz, 1 grób, 1 zdjęcie;
  - `graves` ma trzy nowe kolumny, puste;
  - `pre-update/grobing-v13.db` powstała, a jej liczby są równe kopii sprzed instalacji.
- **Stany [[grob]] v8:**
  - bez daty (`01`): „Opłacone do · nie wiadomo · Wpisz”, 24 dp pod „Dodaj osobę”, linia podziału;
  - okno z „Wpisz” (`02`): fokus w 3c;
  - z datą (`03`): „Opłacone do · 2031”, bez „Wpisz”;
  - poprawa przez ✎ na „2301” (`04`): „Tak odległa data…”, czerwona ramka i ikona, okno zostaje;
  - „13.2031” (`05`): „Nie rozumiem tej daty…”. Komunikat znika przy pisaniu;
  - **w bazie dalej `2031`** (nic się nie zapisało);
  - „03.2019” (`06`): zwykły tekst, bez koloru błędu (D19);
  - czyszczenie: znów „nie wiadomo”;
  - „31.12.2045” zapisane przez ✓ z `next` z „Miejsce” (`16`) — w bazie `(2045, 12, 31)`, nazwa i adres nietknięte.
- **Tekst 200% na 360 dp** (`720x1280`, gęstość 320):
  - bez daty (`07`): etykieta nad wartością, „Wpisz” na końcu wiersza. Wymiary: wartość z etykietą 162 dp + „Wpisz” 88 dp przy szerokości 328 dp,
    zapas 78 dp. To **najgorszy przypadek**, bo bez daty tekst jest zawsze ten sam („nie wiadomo”). Gałąź „Wpisz pod wartością” przy 360 dp się
    nie włącza; zostaje dla węższych ekranów;
  - z datą (`17`): „31.12.2045” pod etykietą.
- **Klawiatura ekranowa** (`show_ime_with_hard_keyboard 1`):
  - 200% (`12`, `13`): pole z etykietą u góry okna nad klawiaturą numeryczną; błąd widać z polem;
  - 100% (`14`): pole i podpowiedź nad klawiaturą;
  - „Wpisz adres” dalej daje fokus w „Kwatera” (`15`).
- **Semantyka i cel dotyku** (`uiautomator dump`):
  - wiersz — „Opłacone do: nie wiadomo” / „Opłacone do 2031”, nie `clickable`;
  - przycisk — „Wpisz datę opłaty”, `clickable`, 62 × 48 dp (100%) i 88 × 48 dp (200%).
- **Bez pomiaru klatek** — nie ma nowej warstwy mapy ani dużych danych.
- **Stan emulatora po przejściu:** build profile v14, grób ma wymyśloną datę `31.12.2045`, tekst i ekran domyślne.

### Deviations
- **Okno samo przewija się do 3c** (poza specyfikacją, która mówiła tylko „okno przewija się do pola nad klawiaturą”). **Znalezione w przejściu:**
  - przy 200% z klawiaturą „Wpisz” dawało fokus w 3c (klawiatura numeryczna), ale pole zostawało pod krawędzią okna. Widać było „Rząd” i
    „Miejsce” (`08`, `10`) — to falsyfikator z planu;
  - własne przewijanie pola tekstowego go nie wyciągało;
  - poprawka: przy fokusie w 3c, przy zmianie wysokości klawiatury i przy błędzie okno przewija pole z 16 dp nad nim na górę widocznej części
    (`Scrollable.ensureVisible`). Odstęp jest po to, żeby etykieta pływająca nie była ucięta — w pierwszej wersji była ucięta do połowy, `11`.
- **Podpowiedź pod 3c ma 3 linie przy 100%** (specyfikacja: „do 2 linii”) — tekst z 3c się nie mieści. `helperMaxLines: 6`, żeby przy 200% nic nie
  zostało ucięte (SC 1.4.4). Propozycja dla `ui`: zostawić albo skrócić tekst, np. „Rok albo data z naklejki lub pokwitowania. Puste — nie wiadomo.”

### Found, outside the item
- Ta sama przyczyna może dotyczyć innych długich okien z polem na końcu (np. „Popraw cmentarz” przy 200% z klawiaturą) — **nie sprawdzałem**,
  [[grob]] → *Open* (luka v6.1) już o tym mówi.

### For `qa`
- **Testy z planu** (*Tests*):
  - migracja v13 → v14 z danymi — w `migration_test.dart` brakuje importu `schema_v14.dart`; wygenerowane testy v1…v13 → v14 już przechodzą;
  - odtworzenie kopii v13 w v14 (wzór v12 w `restore_service_test.dart`);
  - `readPaidUntil` i regresja `parsePartialDate` (data osoby z przyszłości dalej odrzucona);
  - `setGraveDetails` z datą i czyszczeniem;
  - widżety elementu 7 i 3c, w tym przewinięcie do 3c, Miejsce `next` → 3c, „wszystko albo nic”, semantyka, `meetsGuideline`, tekst 200%;
  - istniejące wywołania `setGraveDetails` w testach podają część pól — przy pełnym zapisie okna czyszczą datę i tak ma być.
- **Ręcznie — autor, odczucie** (z planu): 1. grób bez daty — czy wiersz na dole jest na miejscu i nie przeszkadza; 2. wpis roku przez „Wpisz” — czy
  dość szybko przy ok. 50 grobach.
- **Próbne odtworzenie kopii v14** — kopia z datą na drugim emulatorze, po kolei (RAM), odcisk zgodny.

### Round 2 — after `qa` tests and the `ui` review (2026-10-16)
- **Przewijanie do 3c przez zmianę wysokości okna, nie przez zdarzenie klawiatury.**
  - Co znalazł `qa`: test widżetu z klawiaturą pokazaną od razu (jak na szybkim telefonie) zostawiał pole pod krawędzią okna. `Dialog` zmniejsza się
    po klawiaturze z animacją 100 ms, więc przewijanie po samym zdarzeniu klawiatury szło przy oknie jeszcze dużym i dochodziło do końca przewijania.
    Na emulatorze działało tylko dlatego, że klawiatura wysuwa się wieloma zdarzeniami.
  - Poprawka: `NotificationListener<ScrollMetricsNotification>` wokół okna. Przewija przy każdej zmianie wysokości widocznej części, gdy fokus jest
    w 3c. Nasłuch `WidgetsBindingObserver` usunięty.
  - Sprawdzone: test bez tej poprawki pada (pole 242 dp przy krawędzi 196 dp). Na emulatorze nowy build przy 200% z klawiaturą pokazuje pole z
    etykietą u góry (`19-v3-200-okno-wpisz.png`).
- **MINOR z przeglądu `ui` poprawiony.** Etykieta „Opłacone do” idzie nad wartość, gdy jej **zmierzona** szerokość (`TextPainter`) przekracza 96 dp, a
  nie od 18 sp. Na emulatorze: przy 115% stoi w kolumnie w jednej linii (`21-v3-115-wiersz.png`), przy 200% nad wartością (`20-v3-200-wiersz.png`),
  przy 100% bez zmian.

## Verification
> `qa`, 2026-10-16. **Werdykt: APPROVED (self-check, z uwagami).** AC-1…AC-3 mają dowody w testach i w przejściu na emulatorze, a stop #2 ma „ok” ze
> śladem na urządzeniu. Uwagi:
> - próbne odtworzenie na urządzeniu niezrobione (powód niżej) → lista A;
> - przegląd `ui` zgłosił sprawę spoza pozycji: komunikat błędu nie jest ogłaszany przez czytnik.

### Stop #2 — 2026-10-16, autor: „ok”
- **Ślad na urządzeniu (sprawdzony po odpowiedzi):** w bazie `Grobing_Restore` jest data opłaty `2041` (sam rok), wpisana przez autora w oknie. Oba kroki
  odczucia zrobione: wiersz na dole i wpis przez „Wpisz”/✎.
- Autor wpisał ją przy grobie, który dodał sam. Nazwa grobu nie jest zapisana nigdzie poza emulatorem, a kopię bazy z tym wpisem agent usunął z katalogu
  tymczasowego sesji.
- **Przed następnym użyciem `Grobing_Restore`:** zapytać autora, czy jego wpisy można zastąpić (cmentarz i ten grób).

### `ui` review (subagent, 2026-10-16)
**0 BLOCKER · 0 MAJOR · 1 MINOR (opcjonalny):**
- MINOR: etykieta „Opłacone do” zajmuje 95 z 96 dp przy tekście 115%, a próg 18 sp z [[osoba]] 8 dobrano do krótszych etykiet → **poprawione w rundzie 2**
  (pomiar szerokości).
- **Oba odstępstwa `dev` przyjęte:** D20 — okno samo przewija się do 3c; D21 — podpowiedź bez limitu linii, a tekst bez zmian. Krótszy tekst od `dev`
  odrzucony: na 360 dp też ma 3 linie, a „Puste — nie wiadomo” zmienia głos okna. Zapis: [[grob]] **v8.1**.
- **Zgodne:** kolejność 1–7, 7 ostatni, 24 dp i linia podziału; stany v8 (`01`–`07`, `17`); akcent tylko w „Wpisz”, w fokusie i w „Zapisz”; kontrast z
  `theme.dart` ≥ AA wszędzie; cel dotyku 62/88 × 48 dp; błąd z ikoną i tekstem; opis dla czytnika (SC 2.5.3); twarde spacje; ton; wzór „Daty”.
- **Spoza pozycji:** komunikat błędu pod polem nie jest ogłaszany przez czytnik (`ErrorLine` bez regionu na żywo). To ten sam wzorzec co w bloku daty
  osoby, więc kandydat na drobną pozycję dla całej aplikacji, nie poprawka tutaj.

### Automated
- **Pełny przebieg `flutter test --timeout 120s`: 844 zielonych.** `flutter analyze` czyste, `dart format` bez zmian.
- **Poprawione pod v14 (4):** wersja 14 i kolumny opłaty w `database_test`; wersja 14 w `data_state_test` i `data_state_screen_test`; `currentSchemaVersion`
  w teście odtworzenia v12 z ISSUE-042 (`restore_service_test`).
- **Nowe — warstwa danych:**
  - `test/drift/grobing/migration_test.dart` — **AC-3** v13 → v14 z danymi. Dwa groby: z nazwą, adresem i pinezką GPS oraz pusty. Do tego osoba,
    kwatera, pochówek, twierdzenie i zamieszkanie. Wszystko zostaje jak było, opłata jest pusta, a potem grób przyjmuje datę z dniem. Wygenerowane testy
    z każdej wersji do v14 też przechodzą;
  - `test/backup/restore_service_test.dart` (2) — **AC-3** kopia **v13** odtwarza się w v14 przez migrację: wszystkie tabele i liczby, groby z „nie
    wiadomo”. Kopia **v14** z datą `03.2031` wraca z tym samym odciskiem i tą samą datą, a drugi grób zostaje bez daty;
  - `test/data/graves_test.dart` (1) — **AC-1, AC-2** brak daty, potem rok, miesiąc i dzień razem z nazwą i adresem; strumień widoku się odświeża;
    zapis bez daty ją czyści (całe okno).
- **Nowe — daty** (`test/app/dates_test.dart`, 4): pole opłaty przyjmuje `2031`, `03.2031`, `31.12.2045`, rok +50 i datę minioną; puste znaczy brak
  daty. `2077` i dalej dostają komunikat „za daleko”, a `13.2031`, `31.02.2031`, `203`, `ok. 2031` — komunikat bloku daty. **Regresja: data osoby z
  przyszłości dalej odrzucona.**
- **Nowe — ekran** (`test/app/grave/grave_screens_test.dart`, 3):
  - **AC-1, AC-2, W1** — wiersz pod „Dodaj osobę” z „nie wiadomo” i „Wpisz”; opisy dla czytnika; `meetsGuideline` (`androidTapTargetGuideline`,
    `labeledTapTargetGuideline`); każdy przycisk z akcją dotknięcia (retro 3, R2). „Wpisz” daje fokus w 3c z klawiaturą `datetime`. „2031” i `done`
    → „Opłacone do 2031” bez „Wpisz”. ✎ → „03.2019” w kolorze tekstu (D19), w bazie `2019-03`;
  - **D18** — Miejsce `next` → 3c; „2301” i „13.2031” zostawiają okno z komunikatem i ikoną, komunikat znika przy zmianie. „Anuluj” → w bazie nie ma
    ani nazwy wpisanej w oknie, ani daty;
  - **D20, 200% na 360 dp** — okno z „Wpisz” i klawiatura 300 dp: etykieta i linia wpisu w widocznej części okna, nad klawiaturą. **Test pada bez
    poprawki z rundy 2** (sprawdzone). To, czy wiersz mieści się przy 200%, jest zmierzone na emulatorze: w czcionce testowej litera jest kwadratem, a
    pasek zakładek pod grobem przelewa się tylko w niej (tak jak w `map_r1_and_cemetery_photo_test`).

### Agent on the emulator
`Grobing_Restore`, build profile v14. Zrzuty `01`–`21` w `C:\Users\user\AppData\Local\Temp\claude\c--Programowanie-Grobing-grobing-agents\6983a70d-0d04-4682-9976-309892f41b6d\scratchpad\emu043\`.

- **Migracja nad danymi v13 → v14:** liczby w każdej tabeli bez zmian; migawka `pre-update/grobing-v13.db` równa kopii sprzed instalacji (*Dev report*).
- **Stany v8 przy 100%, 115% i 200%, z klawiaturą sprzętową i ekranową:** wszystkie przeszły, także po rundzie 2 (`18`–`21`).
- **„Wszystko albo nic” w bazie:** po dwóch złych datach w bazie dalej był poprzedni wpis `2031`.
- **Próbne odtworzenie na urządzeniu — niezrobione** (jak w [[ISSUE-042-places-of-residence]]): hasła testowego kopii z sesji ISSUE-040 nie ma, a
  odtworzenie zastąpiłoby dane, których agent nie stworzył (cmentarz na `Grobing_Restore`, dane testowe autora na `Medium_Phone`). Ścieżkę pokrywają oba
  testy odtworzenia wyżej, na prawdziwym formacie kopii z szyfrowaniem → lista A.
- Pozycja bez sieci, więc logcat bez sprawdzania (retro 3, R7 dotyczy pozycji z siecią).

### Family data in the changes
- Bez plików baz, kopii, eksportów i zdjęć w obu repo. Zrzuty, kopia danych emulatora i bazy do liczenia leżą w katalogu tymczasowym sesji.
- Nazwiska w kodzie i testach tylko z rdzeni wymyślonych (Wymyśl-, Zmyśl-, Testow-, Przykład-).
- „Grób rodzinny Nowaków” to istniejąca podpowiedź z referencji R4 — w diffie tylko przesunięta o wcięcie.
- Nazwa cmentarza z emulatora nie występuje w żadnej zmianie (grep: 0).

### For ISSUE-032 → Hand checks
- **A** — próbne odtworzenie kopii **v14 z datą opłaty** na urządzeniu, z odciskiem zgodnym: na emulatorze niezrobione (hasło testowe nieznane, dane
  spoza agenta); testy odtworzenia v13 → v14 i v14 przeszły;
- **A** — pierwsza aktualizacja ze sklepu nad v13: migracja v13 → v14 i migawka `pre-update/grobing-v13.db` na telefonie (na emulatorze przeszła).
- Lista B — nic (oba kroki odczucia „ok” ze śladem na urządzeniu).

### Package for `docs`
- **`grobing-code` (20):**
  - kod: `README.md` · `lib/app/dates.dart` · `lib/app/grave/grave_screen.dart` · `lib/app/widgets/date_block.dart` · `lib/data/database.dart` ·
    `lib/data/database.g.dart` · `lib/data/database.steps.dart` · `lib/data/graves.dart` · `lib/dev/fictional_data.dart`;
  - schemat: `drift_schemas/grobing/drift_schema_v14.json`;
  - testy: `test/drift/grobing/generated/schema.dart` · `test/drift/grobing/generated/schema_v14.dart` · `test/drift/grobing/migration_test.dart` ·
    `test/app/dates_test.dart` · `test/app/grave/grave_screens_test.dart` · `test/app/data_state_screen_test.dart` · `test/backup/restore_service_test.dart` ·
    `test/data/graves_test.dart` · `test/data/database_test.dart` · `test/data/data_state_test.dart`.
- **`grobing-vault`:** `backlog/issues/ISSUE-043-grave-paid-until.md` · `05_DESIGN/grob.md` · `00_START_HERE/TRACEABILITY.md` + zamknięcie `docs`
  (`CURRENT_STATE.md`, `04_ARCHITECTURE/data-model.md`, `04_ARCHITECTURE/backup-format.md`, [[ISSUE-032-mvp-install]] → *Hand checks*).
- **`grobing-agents`:** nic.
