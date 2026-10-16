---
title: "ISSUE-041 — Google Play internal testing and a safe update path (store, signing, version code, backup before update)"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-16
verdict-reviewer: self-check
source: "`/pm` 2026-10-16 — pytanie autora „czy nie stracę swoich danych przy aktualizacji?” i decyzja „tak zróbmy to” (Google Play, testy wewnętrzne, klucz od Google) · [[NT-005-distribution-decision]] · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-16
---

# ISSUE-041 — Google Play i bezpieczna aktualizacja

> Autor w `/pm`: *„Będę je chciał wprowadzić do mojej istniejącej na telefonie aplikacji — jak to zadziała? Czy nie stracę swoich danych?
> (…) We Friendsheet podoba mi się to, że mogę po prostu zaktualizować to z poziomu sklepu”*. Decyzja: **Google Play, ścieżka testów
> wewnętrznych, autor jedynym testerem, klucz podpisu generuje Google** — jak w Friendsheet. **Pierwsza pozycja kolejki** przed instalacją
> (najpóźniej 2026-10-29): każda następna funkcja przyjdzie na telefon tą drogą.

## Why
Android zachowuje dane przy aktualizacji, gdy zgadzają się trzy rzeczy: **nazwa pakietu** (`com.grobing.app`, niezmienna —
`project-config.example.md`), **klucz podpisu** i **wyższy numer wersji** (`versionCode`). Pierwsza instalacja z prawdziwymi danymi ustala
je na stałe; zmiana kanału po fakcie = odinstalowanie, czyli skasowana baza i odtworzenie z kopii. Trzecie ryzyko to zła migracja — przed
nią chronią testy (NFR-003) i kopia, która dziś jest **jedna i nadpisywana** (`backup-format.md` → *Known limits*).

## What to build
1. **Wpis aplikacji w Play Console** (konto autora, to samo co Friendsheet), ścieżka testów wewnętrznych, autor jedynym testerem. **Play App
   Signing z kluczem wygenerowanym przez Google**; obecny klucz wydania (`release_keystore_dir`) zostaje **kluczem przesyłania**. Czynności w
   konsoli wykonuje **autor** — agent podaje kroki, nie klika w zewnętrznych serwisach. Formularze konsoli (np. bezpieczeństwo danych, polityka
   prywatności) — sprawdzić przy planie, co wymaga ścieżka testów wewnętrznych.
2. **Paczka `flutter build appbundle`** zamiast APK `--split-per-abi` i **numeracja wersji**: `version` w `pubspec.yaml` rośnie przy każdym
   wydaniu. Pułapka: APK `--split-per-abi` dostaje na arm64 numer 2001 (na emulatorze x86_64 widać 4001), paczka sklepu 1, 2, 3… — **kanałów
   się nie miesza**.
3. **Kopia sprzed aktualizacji.** Najpierw najtańszy sprawdzian: czy Dysk trzyma poprzednią wersję nadpisanego pliku (`backup-format.md` →
   *Known limits*, „niesprawdzone”). Jeśli nie — mechanizm, który przy pierwszym starcie nowej wersji, przed migracją, zachowuje kopię
   poprzedniej (kształt do decyzji przy planie; odtworzenie musi ją przyjąć — ADR-004 pkt 5).
4. **Opis wydania w README `grobing-code`** (jedno miejsce): podbicie numeru → paczka → sprawdzenie w „Stanie danych”, że kopia jest świeża →
   wysyłka przez autora w Play Console → po aktualizacji: migracja, kopia.
5. **Próba generalna na telefonie autora** (Motorola moto g82 5G, Android 13 — [[2026-10-16-retro-04]] → fakt 1): wersja N ze sklepu na
   **wymyślonych** danych → wersja N+1 ze sklepu → dane i kopia bez zmian. To pierwszy wiersz listy A w [[ISSUE-032-mvp-install]] →
   *Hand checks*.
6. **ADR-019 — dystrybucja** (≥3 opcje: sklep + klucz Google · sklep + własny klucz przez PEPK · APK bezpośrednio) — zamyka
   [[NT-005-distribution-decision]]. Pisze łańcuch `planning` → `docs` (`CLAUDE.md` → *Na sygnał*).

## Acceptance Criteria
- **AC-1** *Given* aplikacja zainstalowana ze sklepu z wymyślonymi danymi *When* autor instaluje ze sklepu nowszą wersję *Then* dane są
  nienaruszone (liczby wierszy i odcisk kopii jak przed aktualizacją), a kopia w tle przechodzi. **→ przeniesione 2026-10-16 do
  [[ISSUE-032-mvp-install]] → *Before install* 0** (decyzja autora na stopie #2).
- **AC-2** *Given* nowa wersja zmienia schemat *When* migracja zepsuje dane albo aktualizacja się przerwie *Then* istnieje kopia sprzed
  aktualizacji i odtworzenie ją przyjmuje.
- **AC-3** *Given* README `grobing-code` *When* agent przygotowuje wydanie *Then* wszystkie kroki (numer, paczka, kopia, wysyłka, sprawdzenie
  po aktualizacji) są w jednym miejscu, a te w Play Console są opisane jako kroki autora.

## Notes
- Prior art: [Sign your app](https://developer.android.com/studio/publish/app-signing) — klucz podpisu nie zmienia się przez całe życie
  aplikacji; [Play App Signing](https://support.google.com/googleplay/android-developer/answer/9842756) — klucz od Google albo własny; Friendsheet
  (`Friendsheet-App/docs/BACKLOG.md`): Play App Signing, reset klucza przesyłania 2026-03-18, a APK zbudowany lokalnie ma inny podpis niż wersja
  ze sklepu (TASK-133). Limity testów wewnętrznych (do 100 testerów, bez przeglądu) — ze źródeł pobocznych, sprawdzić w Play Console.
- **Skutek dla [[ISSUE-032-mvp-install]]:** instalacja **ze sklepu**, nie `adb install`; pytanie o klucz wydania z retro 1–3 traci wagę
  (klucz przesyłania da się zresetować).
- **Dane rodziny:** sklep dostarcza kod, bazy nie widzi; [[NFR-005-dane-nie-opuszczaja-telefonu]] bez zmian.
- W trakcie wyjazdu na Wszystkie Święte **żadnych aktualizacji** ([[2026-10-16-retro-04]] → *Product decisions*).

## Implementation plan
> `planning`, 2026-10-16. Pozycja **bez nowego ekranu** (sklep, numer wersji, mechanizm przy starcie) — bez `ui`.
>
> **Stop #1 — 2026-10-16, autor: *„tak”*:** D1 = **K3** (migawka bazy przed migracją), D2 i D3 jak niżej, trzy zagrożenia (a)–(c) bez zmian;
> AC-2 w brzmieniu z *AC mapping*.

### What the code already does (read 2026-10-16)
- **Migrację robi tylko start aplikacji:** `lib/main.dart` → `_open()` → `GrobingDatabase.atFile` (`onUpgrade` w jednej transakcji z
  `user_version` — przerwana aktualizacja zostawia starą wersję całą). **Kopia w tle bazy w innej wersji nie dotyka**
  (`background_backup.dart`: `_userVersion(file) != schemaVersion` → koniec), więc po aktualizacji ze sklepu nic nie migruje, zanim autor
  otworzy aplikację.
- **Zaraz po migracji start zamawia kopię** (`requestBackgroundOnStart`, retro 1 R6) — nadpisuje jedyny plik kopii nowymi danymi. Tu jest luka
  AC-2.
- Baza w trybie **rollback-journal** (`data_stamp.dart`); towarzysze pliku: `-journal`, `-wal`, `-shm` (`restore_swap.dart`).
- Manifest po scaleniu: `INTERNET`, lokalizacja (tylko na pierwszym planie), `FOREGROUND_SERVICE` (z WorkManagera, bez typu usługi i bez
  `setForeground`), `WAKE_LOCK`, `RECEIVE_BOOT_COMPLETED`, `ACCESS_NETWORK_STATE`. **Bez** `FOREGROUND_SERVICE_<TYP>` i bez `READ_MEDIA_*` (okno
  wyboru zdjęć) — czyli bez uprawnień, które w Play Console wymagają osobnych formularzy (sprawdzi to i tak pierwsza wysyłka, krok A1).
- `build.gradle.kts`: każde zadanie „Release” bez `key.properties` kończy się błędem — obejmuje też `bundleRelease`. Paczka sklepu jest podpisana
  obecnym kluczem wydania, który w Play App Signing staje się **kluczem przesyłania**.

### Decisions for stop #1
- **D1 — kopia sprzed aktualizacji. Kandydaci opisani tym, co widzisz i robisz** (retro 4, R1):
  - **K1 — historia wersji Dysku:** nic nie budujemy. Gdy aktualizacja zepsuje dane, wchodzisz na drive.google.com → plik `grobing-kopia.age` →
    „Zarządzaj wersjami” → pobierasz wcześniejszą i odtwarzasz. **Niesprawdzone**, czy zapis przez okno plików Androida tworzy wersję; Dysk
    trzyma wersje ok. 30 dni; działa tylko przy kopii na Dysku.
  - **K2 — drugi plik kopii w Pobranych:** przy pierwszym starcie po aktualizacji aplikacja robi pełną zaszyfrowaną kopię „sprzed
    aktualizacji” do Pobranych (widać ją w „Odtwórz z kopii”). Koszt: start po aktualizacji dłuższy o czas pełnej kopii ze zdjęciami (rząd
    0,2 GB — `backup-format.md` → *Known limits*), drugi duży plik w telefonie.
  - **K3 — migawka samej bazy w prywatnym miejscu aplikacji (rekomendacja):** zanim aplikacja przerobi bazę na nową wersję, odkłada jej spójną
    migawkę (`pre-update/grobing-v<stara>.db`, obok bazy, poza Pobranymi). **Ty nic nie widzisz i nic nie robisz.** Zdjęć aktualizacje nie ruszają
    (migracje zmieniają wiersze), więc wystarczy baza — kilka MB, ułamek sekundy. Droga powrotu przy złej migracji: wersja z poprawką czyta
    migawkę zamiast zepsutej bazy (kod naprawczy w tej wersji — README → *Wydanie*). Trzymamy 3 ostatnie migawki. **Czego nie da:** nie chroni
    przed utratą telefonu w trakcie aktualizacji — przed tym chroni zwykła kopia (sprzed migracji leży na Dysku, dopóki start jej nie nadpisze).
  - K1 można sprawdzić **dodatkowo i za darmo** po instalacji, raz, na Twoim Dysku — wiersz listy A w [[ISSUE-032-mvp-install]] (opcjonalny).
- **D2 — numer wersji** (domyślnie, bez pytania): każda wysyłka do sklepu podbija numer kompilacji w `pubspec.yaml` (`+N` → `+N+1`); nazwa
  `0.9.x` do instalacji z prawdziwymi danymi, `1.0.0` na instalację. APK `--split-per-abi` zostają na emulatorach i **nigdy nie idą na telefon**.
- **D3 — dane do próby na telefonie** (domyślnie): wymyślona rodzina z kopii zrobionej na emulatorze z **nowym hasłem testowym**, odtworzona na
  telefonie przez „Odtwórz z kopii”. Ta sama próba sprawdza odtworzenie na prawdziwym telefonie ([[NFR-002-odtworzenie-na-nowym-telefonie]], lista A).
  Pliki kopii na telefon: `adb push` do Pobranych, gdy podłączysz telefon kablem z debugowaniem USB (jak przy Friendsheet); inaczej kilka osób
  wpisanych ręcznie.
- **Przed czym chronimy?** (retro 3, R7 — pozycja o danych rodziny). Plan zakłada trzy zagrożenia: (a) zła migracja w nowej wersji → D1;
  (b) pomyłka kanału, podpisu albo numeru wersji, która wymusza odinstalowanie → sklep jako jedyna droga na telefon i D2; (c) przerwana
  aktualizacja → już dziś jedna transakcja. Sklep nie widzi bazy (NFR-005).

### Steps
**A — sklep (autor w Play Console, agent podaje kroki i odpowiedzi do formularzy):**
1. **A1 — krok 0, najtańszy falsyfikator:** agent buduje `flutter build appbundle --release` (`build/app/outputs/bundle/release/app-release.aab`);
   autor: *Utwórz aplikację* (Grobing, polski, aplikacja, bezpłatna) → *Testy wewnętrzne* → testerzy: lista z adresem autora → *Utwórz
   wersję* → **klucz podpisu: wygenerowany przez Google** → wgranie paczki → wdrożenie. Pierwsza wysyłka **rezerwuje nazwę pakietu
   `com.grobing.app`** i pokazuje, o co konsola prosi (formularze z panelu). Nazwa zajęta → **STOP** (zmiana pakietu przed prawdziwymi danymi jest
   jeszcze możliwa, ale to decyzja autora — `project-config.example.md`).
2. **A2 — telefon:** link zaproszenia testera → „Zostań testerem” → instalacja ze sklepu. Grobing zainstalowany wcześniej z APK → najpierw
   odinstalować (inny podpis; na telefonie są tylko wymyślone dane albo nic).

**B — kod (`dev`):**
3. **Migawka sprzed aktualizacji (K3)** — nowy `lib/data/pre_update_snapshot.dart`, wołany w `_open()` w `lib/main.dart` **przed**
   `GrobingDatabase.atFile`: plik bazy istnieje i jego `user_version` < `currentSchemaVersion` → spójna migawka do
   `<support>/pre-update/grobing-v<stara>.db`, potem otwarcie i migracja jak dziś; zostają 3 najnowsze migawki. Odczyt `user_version` jednym
   pomocnikiem dla `main` i `background_backup.dart` (dziś prywatny `_userVersion`). **Krok 0 `dev`:** sposób migawki przy gorącym dzienniku
   (`-journal` po przerwanym zapisie) — `VACUUM INTO` z połączenia tylko do odczytu albo kopia pliku po odtworzeniu dziennika; wynik z pomiarem w
   *Dev report*. Migawka nie powstaje przy pierwszej instalacji (brak pliku) ani przy odtworzeniu z kopii (tam starszą wersją jest sam plik kopii).
4. **Numer wersji** — `pubspec.yaml`: `version: 0.9.0+1` (pierwsza wysyłka), dalej według D2.
5. **README `grobing-code`** — nowa sekcja *Wydanie*: numer → `flutter build appbundle --release` → „Stan danych”: kopia świeża → wysyłka
   (autor) → aktualizacja na telefonie → migracja i kopia; **droga powrotu przy złej migracji** (migawka z kroku 3); zakaz APK na telefonie;
   *Podpis wydania*: klucz wydania = klucz przesyłania, klucz podpisu trzyma Google, reset klucza przesyłania przez konsolę.

**C — próba generalna (autor na telefonie, agent przygotowuje):**
6. Agent: na emulatorze kopia wymyślonej rodziny z nowym hasłem testowym → pliki na telefon (D3). Autor: „Odtwórz z kopii” → odczyt odcisku w
   „Stanie danych”.
7. Agent: wersja N+1 (tylko podbity numer) → autor wysyła i aktualizuje ze sklepu → odcisk w „Stanie danych” ten sam (AC-1).

**D — vault (`docs` przy zamknięciu, z treści planu i *Dev report*):** ADR-019 (dystrybucja; opcje: sklep z kluczem Google · sklep z własnym
kluczem przez PEPK · APK bezpośrednio; decyzja autora 2026-10-16) → zamyka [[NT-005-distribution-decision]]; `backup-format.md` → *Known limits*
(migawka sprzed aktualizacji); wiersze listy A w [[ISSUE-032-mvp-install]].

### AC mapping
| AC | Jak spełnione | Dowód |
|---|---|---|
| AC-1 | kroki A1–A2, C6–C7 | odcisk w „Stanie danych” przed i po aktualizacji ze sklepu (autor); kopia w tle po aktualizacji |
| AC-2 (doprecyzowane do K3 — decyzja na tym stopie) | krok 3 — *Given* baza w starszej wersji *When* pierwszy start nowej wersji *Then* przed migracją powstaje migawka w starej wersji, a migracja z migawki daje te same dane | test `qa` + przejście na emulatorze |
| AC-3 | krok 5 | README → *Wydanie* |

### Tests (`qa`)
- Migawka: baza v11 z **wymyślonymi** danymi (schematy w `drift_schemas/grobing/`) → otwarcie przez ścieżkę startu → `pre-update/grobing-v11.db` ma
  `user_version` 11 i te same wiersze, baza główna ma v12; migracja z migawki przechodzi (ten sam test co NFR-003).
- Brak migawki: przy tej samej wersji, przy pierwszej instalacji, po odtworzeniu z kopii. Rotacja: zostają 3 najnowsze.
- Migawka przy gorącym dzienniku (wynik kroku 0 `dev`).
- Pełny `flutter test --timeout 120s`, `flutter analyze`, `dart format` (retro 4, R5).

### Manual verification
**Agent na emulatorze (przed stopem #2):**
- build profile; do katalogu danych aplikacji (`run-as`) baza v11 z wymyślonymi danymi → start → migawka v11 jest, baza v12, liczby wierszy bez
  zmian, kopia w tle po migracji (zrzuty);
- `flutter build appbundle --release` przechodzi; rozmiar paczki w *Dev report*;
- **próbne odtworzenie** (DoD — pozycja dotyka startu bazy): kopia z emulatora po migracji odtwarza się na drugim emulatorze, odcisk zgodny, a
  odtworzenie nie zostawia migawki.

**Autor — kroki w ręce (lista A, nie odczucie; AC-1 bez nich nie jest spełnione, więc „pomiń” zostawia pozycję otwartą):**
1. Play Console: utworzenie aplikacji, testerzy, pierwsza wersja z kluczem od Google (lista kroków od agenta).
2. Telefon: zaproszenie testera → instalacja → „Odtwórz z kopii” (pliki i hasło testowe od agenta) → odcisk w „Stanie danych” → napisz tutaj.
3. Druga wersja: wysyłka w konsoli → aktualizacja na telefonie → odcisk → napisz tutaj.

### Out of scope
Ścieżka produkcyjna i publiczny wpis w sklepie · grafiki wpisu (ikona — [[ISSUE-046-icons]]) · Firebase App Distribution · ekran odtwarzania
z migawki · kopia przyrostowa i historia kopii na Dysku (K1 tylko jako opcjonalne sprawdzenie) · zmiana schematu (pierwsza prawdziwa migracja przez
sklep przyjdzie z [[ISSUE-042-places-of-residence]] — wiersz listy A) · iPhone.

### Obali (falsifiers)
- Nazwa pakietu `com.grobing.app` zajęta w Google Play → STOP (krok A1).
- Konsola blokuje wdrożenie testów wewnętrznych bez formularzy (polityka prywatności, ocena treści) → lista dla autora, plan bez zmian.
- Migawka przy gorącym dzienniku nie daje spójnej bazy → krok 0 `dev` wybiera drugą drogę.
- Odcisk po aktualizacji ze sklepu inny niż przed → STOP, nic na telefon z prawdziwymi danymi.

### Sources
[Sign your app](https://developer.android.com/studio/publish/app-signing) · [Play App Signing](https://support.google.com/googleplay/android-developer/answer/9842756) ·
[Testy wewnętrzne, zamknięte i otwarte](https://support.google.com/googleplay/android-developer/answer/9845334) (pierwsza wersja dostępna od razu
z tymczasową nazwą do 48 h; ścieżka wewnętrzna zwolniona z sekcji „Bezpieczeństwo danych”) · [Foreground services — declare](https://developer.android.com/develop/background-work/services/fgs/declare)
(formularz dotyczy typów usług — u nas brak) · Friendsheet `docs/BACKLOG.md` (TASK-032/033, TASK-133).

## Dev report
> `dev`, 2026-10-16. Flutter 3.41.1 (przypięty) · `flutter analyze` czyste · `dart format` bez zmian. Testów nie pisałem (`qa`).

### Changed
- `lib/data/pre_update_snapshot.dart` (nowy) — `takePreUpdateSnapshot()`: istnieje plik bazy, `user_version` > 0 i < `currentSchemaVersion` →
  `VACUUM INTO` do `pre-update/grobing-v<stara>.db.partial`, potem zmiana nazwy na `grobing-v<stara>.db`; zostają 3 najwyższe wersje, pliki
  `.partial` po przerwanym biegu znikają. Zwraca migawkę albo `null`. Stałe i ścieżki publiczne dla testów (`preUpdateSnapshotDir`,
  `preUpdateSnapshotFile`, `preUpdateSnapshotsKept`).
- `lib/main.dart` — `_open()`: po `completePendingRestore`, **przed** `GrobingDatabase.atFile`, wywołanie migawki w `try`/`on Object` (D-dev 2).
- `pubspec.yaml` — `version: 0.9.0+1` (D2); `lib/app/settings/settings_screen.dart` — `appVersion = '0.9.0'` (drugi dom nazwy; test
  `settings_words_test.dart` trzyma je razem).
- `README.md` — *Lokalizacja* → *Telefon*: tylko ze sklepu, dlaczego APK nie (podpis, numer 2001); *Podpis wydania*: klucz wydania = klucz
  przesyłania, reset w Play Console; nowa sekcja **Wydanie** (numer, paczka, kopia przed wysyłką, wysyłka i aktualizacja przez autora, bez
  aktualizacji w trakcie wyjazdu, migawka, **droga powrotu przy złej migracji**) — AC-3.

### Step 0 — snapshot with a hot journal (measured)
Sonda (jednorazowy `tool/probe_hot_journal.dart`, usunięty; trzy osobne uruchomienia, bo na Windows proces potomny `dart run` nie może podmienić
`sqlite3.dll`, którą trzyma rodzic): baza 5000 wymyślonych wierszy, `user_version` 11 → proces w transakcji zmienia wszystkie wiersze i ustawia
`user_version` 12 przy `cache_size = 1` (strony trafiają do pliku) i ginie bez `COMMIT` — **gorący dziennik 1 426 960 B**. Potem
`takePreUpdateSnapshot(currentVersion: 12)`:
- dziennik cofnięty (po migawce go nie ma), odczytana wersja **11** (zatwierdzona, nie połowiczna 12);
- migawka i baza: 5000 wierszy, **0 zmienionych**, `integrity_check` ok; czas **68–89 ms** dla 1,1 MB.

Wniosek: połączenie do zapisu (nie tylko do odczytu) jest właściwą drogą — odczyt nagłówka pliku mógłby zobaczyć połowiczną migrację, a połączenie
tylko do odczytu przy gorącym dzienniku kończy się błędem (`SQLITE_READONLY_ROLLBACK`).

### Emulator pass (`Grobing_Restore`, build profile `0.9.0`, `FRAME_LOG`)
- Baza z emulatora (wymyślona rodzina: 107 osób, 14 tabel, 750 wierszy, bez cmentarzy) → kopia **v11** na hoście (usunięta kolumna
  `graves.position_recorded_at` — jedyny krok 11→12; `user_version` 11; grobów 0, więc żadna wartość nie zginęła) → `run-as` do `files/grobing.db`
  przy zatrzymanej aplikacji → `adb install -r` nowego buildu → start.
- **Po 5 s od uruchomienia** jest `files/pre-update/grobing-v11.db` (139 264 B). Porównanie (`python`, skrypt z pliku):
  migawka — `user_version` 11, `integrity_check` ok, 750 wierszy; baza główna — **v12**, kolumna `position_recorded_at` jest, `integrity_check` ok,
  **750 wierszy, te same liczby w każdej tabeli** co przed. Logcat bez błędów Fluttera. Zrzut: ekran główny po migracji jak przed (mapa Polski,
  „Tu pojawią się cmentarze rodziny” — ta rodzina nie ma cmentarzy).
- **Drugi start:** migawka bez zmian (czas zapisu 13:19:03 UTC, drugi start ok. 30 s później), żadnej nowej.
- Kopia w tle po migracji — nie czekałem na nią (okres ciszy); do sprawdzenia przez `qa` w „Stanie danych”.

### Bundle
`flutter build appbundle --release` → `build/app/outputs/bundle/release/app-release.aab`, **50,3 MB** (wszystkie architektury; sklep podaje
telefonowi tylko arm64). Podpis: certyfikat klucza wydania z 2026-10-05, ważny do 2054 — **SHA-1 `36:CE:ED:57:56:C6:F6:FF:0E:F5:39:D5:4A:90:CB:47:4F:AD:06:7E`**
(odcisk jawny; po pierwszej wysyłce to odcisk klucza przesyłania w Play Console → *Integralność aplikacji*).

### Deviations
- **D-dev 1 — bez wspólnego pomocnika `user_version`** (plan, krok 3): migawka potrzebuje połączenia **do zapisu**, które cofa gorący dziennik;
  kopia w tle zostaje przy swoim odczycie tylko do odczytu (przy gorącym dzienniku kończy się błędem → ponowienie, jak dziś). Jeden pomocnik
  ukryłby tę różnicę.
- **D-dev 2 — błąd migawki nie zatrzymuje startu:** brak migawki to nie powód, żeby zamknąć dane — migracja idzie w jednej transakcji, a kopia
  na Dysku trzyma dane sprzed niej, dopóki start jej nie zastąpi. Do oceny `qa` i autora.
- Migawka idzie **synchronicznie przed `runApp`** (pierwsza klatka czeka) — tylko przy pierwszym starcie po aktualizacji ze zmianą schematu; na
  hoście 1,1 MB w 68–89 ms, na emulatorze 139 KB (osobno nie mierzone).

### For `qa`
- Testy z planu (*Tests*): v11 → migawka + v12; brak migawki (ta sama wersja · brak pliku · `user_version` 0 · po odtworzeniu); rotacja 3;
  `.partial` po przerwanym biegu; gorący dziennik (powtórzenie sondy w teście: osobny proces albo `Isolate`, który ginie w transakcji — albo
  zapisany wcześniej plik z dziennikiem jako dane testu).
- Próbne odtworzenie na drugim emulatorze (*Manual verification*); kopia w tle po migracji w „Stanie danych”.
- **Stop #2 — kroki autora (lista A)** według planu; druga wersja (C7) = `0.9.0+2`, buduje agent po kroku 2 autora — w paczce pozycji zostaje
  numer, który poszedł do sklepu ostatni.
- Stan emulatora: `Grobing_Restore` ma build profile `0.9.0`, bazę po migracji z wstrzykniętej v11 (te same dane) i migawkę v11 w `files/pre-update/`.

## Verification
> `qa`, 2026-10-16. **Stop #2 — decyzja autora:** po kroku 1 (Play Console) autor: *„wait — ja najpierw chciałbym stworzyć te funkcjonalności,
> o których mówiliśmy wcześniej, zanim zainstaluję na telefonie”*, potem *„tak”* na podział: **ISSUE-041 zamyka się w części kodu (AC-2, AC-3); część w
> sklepie (AC-1 — kroki A1–A2, C6–C7) przechodzi do [[ISSUE-032-mvp-install]] → *Before install* 0.** To nie „pomiń”: kroków nikt nie zaczął, przeszły
> w całości do pozycji instalacji.
>
> **Werdykt: APPROVED (self-check, z uwagami)** — AC-2 i AC-3 spełnione dowodami niżej; AC-1 poza tą pozycją. Uwagi: D-dev 2 (błąd migawki nie
> zatrzymuje startu) przyjęte; próbne odtworzenie na urządzeniu — na telefonie w ISSUE-032; nazwa pakietu w sklepie niesprawdzona do pierwszej wysyłki.

### Automated
- **Nowe testy** `test/data/pre_update_snapshot_test.dart` (4, wymyślone cmentarze i groby, schemat v11 z `drift_schemas` przez `SchemaVerifier`):
  1. **AC-2** — baza v11: migawka v11 z każdym wierszem, sama baza bez zmian, obie po otwarciu w aplikacji przechodzą na bieżącą wersję z tymi samymi
     grobami;
  2. brak migawki: brak pliku (pierwsza instalacja), baza w bieżącej wersji (także każda po odtworzeniu — migruje we własnym katalogu), plik z
     `user_version` 0; katalog `pre-update/` wtedy nie powstaje;
  3. rotacja (zostają v9, v10, v11 z v8–v11), plik `.partial` po przerwanym biegu znika, drugi start w tej samej starej wersji zastępuje migawkę;
  4. **gorący dziennik**: zapis przerwany w transakcji (wszystkie groby zmienione, 3000 nowych cmentarzy, `user_version` 12, `cache_size` 1) — plik bez
     dziennika **różni się** od zatwierdzonej bazy (test łapie kopię pliku „jak leży”), a migawka i baza po migawce mają zatwierdzone dane i wersję 11,
     dziennik cofnięty.
- **Pełny `flutter test --timeout 120s`: 777 zielonych** (773 + 4), bez zawieszenia; `flutter analyze` czyste (jedna uwaga `prefer_const_declarations`
  w nowym teście poprawiona); `dart format --set-exit-if-changed lib test`: 0 zmian.

### Agent on the emulator
- Przejście `dev` (*Dev report* → *Emulator pass*) sprawdzone na danych: migawka v11 = wstrzyknięta baza v11, baza główna v12, 750 wierszy w 14 tabelach
  przed i po, `integrity_check` ok, drugi start bez nowej migawki.
- **Próbne odtworzenie na emulatorze — wstrzymane:** po 13:19 (czas emulatora) w aplikacji na `Grobing_Restore` pojawił się cmentarz dodany **poza agentem**
  (ktoś używa emulatora); odtworzenie zastąpiłoby te dane. Ścieżka odtworzenia nie zmieniła się w kodzie — testy `restore_service_test.dart` (w pełnym
  przebiegu) zielone, a odtworzenie między urządzeniami zrobi krok 2 autora na telefonie.

### For ISSUE-032 → Hand checks
- **A** — instalacja ze sklepu i aktualizacja tą samą drogą (AC-1, przeniesione — *Before install* 0);
- **A** — odtworzenie kopii na urządzeniu po starcie z migawką — na emulatorze wstrzymane, na telefonie w kroku C6;
- **A** — pierwsza aktualizacja ze zmianą schematu przez sklep: migawka powstaje na telefonie.

### Family data in the changes
Kod, testy i README: przykłady tylko z rdzeni wymyślonych („Wymyślony”, „Zmyślonych”, „Testowy”); żadnych `*.db`, kopii, eksportów ani zdjęć w zmianach
(`git status` `grobing-code`: README, `lib/main.dart`, `lib/app/settings/settings_screen.dart`, `pubspec.yaml`, `lib/data/pre_update_snapshot.dart`,
`test/data/pre_update_snapshot_test.dart`). Bazy z emulatora (wymyślona rodzina) leżą tylko w katalogu tymczasowym sesji.
