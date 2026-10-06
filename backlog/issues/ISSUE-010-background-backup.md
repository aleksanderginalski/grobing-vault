---
title: "ISSUE-010 — Background backup: after data changes, without the passphrase"
type: issue
status: in-progress
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-001-kopia-z-odtworzeniem]]"
ideal_days: 1
quality-verdict: APPROVED
verdict-date: 2026-10-06
verdict-reviewer: self-check
created: 2026-10-06
updated: 2026-10-06
---

# ISSUE-010 — Kopia: w tle

> Wydzielone z [[ISSUE-008-backup-write]] decyzją autora na stopie #1 (D1, 2026-10-06): pkt 3 „kopia w
> tle" i AC-2. Konfiguracja, format, zapis do Dysku i „Ostatnia udana kopia" już są w ISSUE-008. Tutaj
> dochodzi tylko uruchamianie kopii bez użytkownika.

## What to build
1. **Kopia w tle po zmianie danych, bez hasła.** W telefonie jest tylko klucz publiczny
   ([[ADR-004-backup-format-encryption-destination]] pkt 3), więc kopia w tle nie potrzebuje sekretu.
2. **Kiedy się uruchamia, wybiera `planning`.** Termin wykonania wyznacza Android: od ~1 min do > 44 min
   ([[SPIKE-003-backup-and-restore]], M2a). Każda kopia wysyła całość (ADR-004, *Consequences*), więc
   częstotliwość waży przy zdjęciach.
3. Wynik trafia tam, gdzie wynik „Zrób kopię teraz": stan kopii poza bazą i „Ostatnia udana kopia" na
   ekranie „Stan danych" (ISSUE-008, krok 5).

## Acceptance Criteria
- [ ] Kopia w tle powstaje po zmianie danych bez pytania o hasło (zmierzone na emulatorze; termin
      zapisany, nie obiecany). *(AC-2 z ISSUE-008.)*
- [ ] Nowe zależności przejrzane, APK release nadal bez uprawnienia `INTERNET`
      ([[NFR-005-dane-nie-opuszczaja-telefonu]] → *Verification trigger*: każda nowa zależność).

## Unknowns — not measured by the spike
SPIKE-003 sprawdził natywny zapis do Dysku w tle, a nie szyfrowanie w tle (*Follow-ups*):
- **Dart w tle:** `workmanager` 0.10.10 (Dart ≥ 3.5, Flutter ≥ 3.38) działa z przypiętym SDK
  (ISSUE-008 → *Prior art*, API pub.dev 2026-10-06). WorkManager dokłada `WAKE_LOCK`,
  `ACCESS_NETWORK_STATE`, `RECEIVE_BOOT_COMPLETED` i `FOREGROUND_SERVICE` (SPIKE-003, M3), ale nie
  `INTERNET`.
- **Kanał do Dysku w silniku bez Activity:** `BackupDocuments.kt` zapisuje przez samo `Context`, ale kanał
  rejestruje `MainActivity`, więc silnik Fluttera uruchomiony w tle go nie zobaczy bez osobnej rejestracji.
- **Dwa połączenia z bazą naraz:** otwarta aplikacja i kopia w tle (`VACUUM INTO` z drugiego połączenia).

## Input from ISSUE-009 (2026-10-06)
- **Kopia w tle a odtworzenie:** odtworzenie zamyka bazę aplikacji tuż przed podmianą, a podmianę
  zatwierdza znacznik `restore.json` w katalogu danych (`lib/backup/restore_swap.dart`). Silnik w tle,
  który sam otwiera bazę, musi **najpierw** wywołać `completePendingRestore` (jak `main.dart`) albo nie
  ruszać bazy, dopóki znacznik istnieje. Kopia w tle nie może też biec w trakcie odtworzenia — dziś pilnuje
  tego tylko ekran (jedna operacja naraz).
- **Trzecie połączenie z bazą:** w trakcie odtworzenia aplikacja otwiera dodatkowo migawkę w katalogu
  tymczasowym (tylko do odczytu) — nie dotyczy żywej bazy, ale warto o nim wiedzieć przy „dwóch
  połączeniach naraz” wyżej.
- **Po odtworzeniu na świeżym telefonie** kopia jest już skonfigurowana (ten sam klucz, ten sam plik —
  D3). Pierwsza kopia w tle nadpisze plik w Dysku danymi odtworzonymi, czyli tymi samymi.
- `RestoreService.databaseClosed` i nowy klucz `GrobingApp` po odtworzeniu: wszystko, co trzyma
  `GrobingDatabase` (także przyszły harmonogram kopii w tle), musi się otworzyć od nowa po przeładowaniu.

## Out of Scope
- Odtworzenie → [[ISSUE-009-restore]].
- Kopia przyrostowa (ADR-004, *Options*: niewykonalna przez okno systemowe) · powiadomienia.

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-008-backup-write]] | technical | `done` |
| [[ISSUE-009-restore]] | kolejność w US-001 | `done` (2026-10-06) — najpierw domknięta pętla „kopia → odtworzenie" (G1: kopia, której nikt nie odtworzył, nie jest kopią), potem automatyzacja |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC · ręczna weryfikacja na
emulatorze · próbne odtworzenie kopii zrobionej w tle · zero danych rodziny w zmianach · INVEST self-check.

## Implementation plan
> **Stop #1 (autor, 2026-10-06): „tak” z poprawką D2.** Pierwsza wersja D2 („zadanie co 1 h”) odrzucona:
> *„takie częste checki to będzie za dużo jak na aplikację, z której korzysta się tak rzadko”*. Wariant
> „tylko przycisk” omówiony i odrzucony, bo kopia ma być automatyczna (ADR-004, brief §Security,
> `glossary.md`), a przycisk „Zrób kopię teraz” zostaje. Przyjęte: kopia wyzwalana **wyjściem z
> aplikacji, gdy coś się zmieniło**, bez cyklicznych sprawdzeń. D1, D3 i D4 bez zmian co do kierunku; D3
> dostosowane do D2 (ponowienie zamiast pominięcia, konfiguracja pod zamkiem).
>
> **Stop #2, podejście 1 (autor, 2026-10-06): wyzwalacz D2 poprawiony — „jedna kopia po sesji”.**
> Wyjście z aplikacji jako jedyny wyzwalacz przegrywa wyścig z wyrzuceniem aplikacji z ostatnich
> (*Verification* → podejście 1). Autor wybrał wariant „jedna kopia po sesji” zamiast „kopia co ~10 min w
> trakcie sesji”. Teraz **kopię zamawia sam zapis danych** (obserwator zapisów do bazy w korzeniu
> aplikacji). Start i wyjście zostają jako dodatkowe wyzwalacze. **Przebieg w tle czeka na ciszę:**
> kopia powstaje dopiero po 10 min bez zmian, a przy dłuższej, ciągłej pracy co najwyżej 60 min od
> pierwszej niezapisanej zmiany. Limit 60 min wybrał `dev`; autor poprosił o „górny limit” bez liczby.
> Niezmienniki (ii)-(iv) bez zmian.
>
> `planning`, 2026-10-06. **DoR:** jasny zakres ✅ (pkt 1-3 + *Input from ISSUE-009*) · powiązana US:
> [[US-001-kopia-z-odtworzeniem]] ✅ (AC-1, ostatnia brakująca) · krok ścieżki: n/a, poza ścieżką (M8) ✅ ·
> `task-level` ✅. Bez `⚠️ OPEN`; SPIKE-003 `done`. **Warstwa danych:** schemat się **nie** zmienia (v1),
> więc testu migracji nie ma. Stan kopii nadal żyje w `backup.json`, poza bazą. Dochodzi drugie połączenie
> z bazą (D3). Próbne odtworzenie **kopii zrobionej w tle**: test na hoście + stop #2. Źródło faktu:
> **n/a**, pozycja nie zapisuje faktów o rodzinie (dane wymyślone, tylko w buildzie debug).

### Prior art (sources, not memory)
- **`workmanager` (pub) a własny kanał:** silnik w tle tworzy `BackgroundWorker.kt` jako
  `engine = FlutterEngine(applicationContext)`
  ([źródło, fluttercommunity/flutter_workmanager](https://github.com/fluttercommunity/flutter_workmanager/blob/main/workmanager_android/android/src/main/kotlin/dev/fluttercommunity/workmanager/BackgroundWorker.kt),
  sprawdzone 2026-10-06). Taki silnik dostaje tylko wtyczki z `GeneratedPluginRegistrant`, czyli paczki z
  pub, a aplikacja **nie ma haka**, żeby dołożyć własny `MethodChannel`. Kanał `com.grobing.app/documents`
  rejestruje `MainActivity`, więc w tym silniku go nie ma. Z `workmanager` kanał musiałby się stać osobną
  paczką-wtyczką. Wersja: 0.10.10, wydana ~28 dni temu (pub.dev).
- **Dart w tle bez paczki:** Flutter, [*Background processes*](https://docs.flutter.dev/packages-and-plugins/background-processes):
  izolat w tle z wywołaniem zwrotnym albo WorkManager. Bezgłowy silnik uruchamia nazwaną funkcję przez
  [`DartExecutor.DartEntrypoint(pathToBundle, functionName)`](https://api.flutter.dev/javadoc/io/flutter/embedding/engine/dart/DartExecutor.DartEntrypoint.html).
  W buildzie release funkcja musi mieć `@pragma('vm:entry-point')`, inaczej kompilator AOT ją wytnie.
- **WorkManager (Android):** [*Define work*](https://developer.android.com/develop/background-work/background-tasks/persistent/getting-started/define-work):
  zadanie okresowe co **≥ 15 min**; warunki m.in. `StorageNotLow` i `BatteryNotLow`; ponawianie domyślnie
  wykładnicze od 30 s. [*Manage work*](https://developer.android.com/develop/background-work/background-tasks/persistent/how-to/manage-work):
  unikalne zadanie = jedno o danej nazwie (`KEEP` / `REPLACE`). Zadanie dostaje **~10 min**; od Androida
  12 system może je zatrzymać po 10 min, gdy potrzebuje zasobów
  ([`CoroutineWorker`](https://developer.android.com/reference/kotlin/androidx/work/CoroutineWorker)).
  `REPLACE` **anuluje** istniejące zadanie, także biegnące; `APPEND_OR_REPLACE` dokłada nowe za
  istniejącym.
- **Wyjście z aplikacji we Flutterze:** [`AppLifecycleState.paused`](https://api.flutter.dev/flutter/dart-ui/AppLifecycleState.html)
  — aplikacja *„not currently visible to the user”*. Przychodzi więc także wtedy, gdy aplikację zasłoni
  systemowe okno wyboru pliku (konfiguracja, odtworzenie) albo aparat (przyszłe US-005), nie tylko przy
  wyjściu na ekran główny.
- **Dwa połączenia z jedną bazą w jednym procesie:** SQLite, [*How To Corrupt*](https://www.sqlite.org/howtocorrupt.html)
  §2.2-2.3: *„perfectly safe for two or more threads to access the same SQLite database file using the
  SQLite library"*, ale **pod warunkiem jednej kopii biblioteki**. Druga kopia (np. `android.database.sqlite`
  w Kotlinie na `grobing.db`) nie zna cudzych blokad, a to grozi uszkodzeniem bazy.
- **Pomiary ze SPIKE-003:** M2 — natywne zadanie WorkManager przy zabitym procesie zapisało 10,6 MB do
  Dysku (`SUCCESS`); M2a — termin od ~1 min do > 44 min; M3 — uprawnienia dokładane przez WorkManager, bez
  `INTERNET`; M4 — szyfrowanie ~8 MB/s.

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego · czego to nie da · co obali |
|---|---|---|---|
| D1 | **Jak uruchomić Darta w tle** (pozycja: „`workmanager` działa z przypiętym SDK”) | **Własne zadanie na `androidx.work` w Kotlinie + bezgłowy silnik Fluttera.** Zadanie startuje silnik, rejestruje w nim **ten sam** `BackupDocuments` (bez okien) i kanał zakończenia, a potem uruchamia funkcję Darta `backgroundBackup` z `@pragma('vm:entry-point')`. **Bez paczki `workmanager`** | `workmanager` nie widzi naszego kanału (*Prior art*), więc kanał trzeba by i tak wyjąć do osobnej paczki-wtyczki. Natywne zadanie WorkManager piszące do Dysku przy zabitym procesie **już zmierzyliśmy** (M2). Nowa jest tylko druga połowa: silnik Fluttera w tym zadaniu. Do tego jedna zależność mniej do przeglądu (NFR-005): `androidx.work` to Jetpack Google, z którego `workmanager` i tak korzysta. **Koszt:** ~100 linii Kotlina (cykl życia silnika) do utrzymania. **Czego nie da:** gotowego API Darta do planowania, bo jest jedna metoda kanału. **Obali ją:** krok 1 — silnik w tle nie uruchamia funkcji albo nie zapisze do Dysku → wariant zapasowy `workmanager` + paczka-wtyczka z kanałem (+~0,5 dnia), raport |
| D2 | **Kiedy się uruchamia** (pkt 2: wybiera `planning`; **poprawione na stopie #1**) | **Zdarzenie, nie harmonogram.** Wyzwalacze: **wyjście z aplikacji** (`paused`) i **start aplikacji**, oba tylko wtedy, gdy **stempel danych** (metadane pliku bazy i plików zdjęć, nie treść) różni się od stempla zapisanego przy ostatniej udanej kopii. Wyzwolenie zakłada **jedno** unikalne zadanie z opóźnieniem **~10 min**, warunkiem `StorageNotLow` i bez warunku sieci (wysyła aplikacja Dysk). Niezmienniki: **(i)** kolejne wyzwolenia w czasie oczekiwania nic nie dokładają, bo jedna kopia obejmuje wszystkie zmiany; **(ii)** biegnąca kopia **nigdy** nie jest anulowana, więc nie `REPLACE`: anulowanie w trakcie zapisu `"wt"` zostawia w Dysku ucięty plik; **(iii)** zmiana w trakcie biegnącej kopii → kopia sprawdza stempel na końcu i zakłada jeszcze jedną; **(iv)** nieudana kopia → ponowienie z odstępem (WorkManager), ograniczona liczba prób, potem następne wyzwolenie. Stempel jest brany **przed** migawką. Zapisuje go też „Zrób kopię teraz” | **Gdy aplikacji nikt nie używa, nic się nie dzieje** (uwaga autora). Po sesji przepisywania powstaje jedna kopia, kilka minut po wyjściu. Opóźnienie łączy krótkie wyjścia (okno wyboru pliku, później aparat w US-005) w jedną pełną kopię. **Nie trzeba haka w każdym przyszłym ekranie:** jeden obserwator cyklu życia w korzeniu aplikacji, a stempel łapie każdy zapis, także spoza `drift`. Start aplikacji łapie wyjście, którego nie było (awaria, zabity proces). Stary telefon bez zmian **nie nadpisze** pliku w Dysku. **Czego nie da:** kopii „zaraz po zapisie”; okno utraty to ~10 min + opóźnienie Androida (M2a); po wyczerpaniu ponowień następna próba czeka na następne użycie aplikacji (błąd widać na „Stanie danych”). **Odrzucone:** zadanie co 1 h (pierwsza wersja D2 — sprawdzenia także bez użycia) i sam przycisk (kopia ręczna — ADR-004 *Options*). **Obali ją:** stempel zmienia się bez zmiany danych (np. samo otwarcie bazy) → zbędna kopia przy każdym wyjściu (test na hoście) |
| D3 | **Jedna operacja na danych naraz** (*Input from ISSUE-009*) | **Zamek w procesie, trzymany natywnie**, wspólny dla kopii w tle, „Zrób kopię teraz”, **konfiguracji kopii** i odtworzenia. Flaga w Darcie nie przechodzi między silnikami, a `File.lock` w Darcie to blokada `fcntl`, która działa na poziomie procesu, więc nie wyklucza dwóch izolatów w jednym procesie. Kopia w tle przy zajętym zamku **ponawia później** (odstęp WorkManagera), bo przy D2 pominięcie gubiłoby wyzwolenie. Odtworzenie, konfiguracja i „Zrób kopię teraz” dostają komunikat. **Kopia w tle nie dokańcza odtworzenia i nie migruje:** przy znaczniku `restore.json` albo przy `user_version` ≠ wersja aplikacji kończy bez kopii. Odtworzenie albo migrację dokończy start aplikacji, a ten sam start znów wyzwoli kopię (D2). `PRAGMA busy_timeout` na **obu** połączeniach | Odtworzenie zamyka bazę i podmienia pliki. Kopia w tle w tym momencie czytałaby pliki w połowie podmiany. **Konfiguracja pod zamkiem**, bo okno wyboru pliku wyzwala `paused` (*Prior art*), a kopia w tle zapisująca wynik ze starym kluczem nadpisałaby `backup.json` świeżo zapisany przez „Skonfiguruj kopię od nowa”. Dokańczanie odtworzenia i migracja w dwóch silnikach naraz to wyścig. `VACUUM INTO` trzyma blokadę odczytu, więc bez `busy_timeout` zapis w otwartej aplikacji dostałby `SQLITE_BUSY`. **Czego nie da:** obrony przed drugą kopią SQLite w procesie. To zakaz: Kotlin **nigdy** nie otwiera `grobing.db` (*Prior art*). **Obali ją:** test dwóch połączeń (zapis + `VACUUM INTO` naraz) daje `SQLITE_BUSY` albo `integrity_check` ≠ `ok` |
| D4 | **Rozmiar** (`ideal_days: 1`) | **Bez podziału, ~1,5 dnia** | Kopia w tle bez zamka (D3) to niebezpieczny stan pośredni, tak jak odtworzenie bez odzyskania po awarii w ISSUE-009, a D2 bez D1 nie ma czego uruchamiać. **Czego nie da:** pozycji w rozmiarze z `glossary.md` |

### Scope diff vs the item (to accept at stop #1)
- **= AC-1 doprecyzowane przez D2:** „po zmianie danych” znaczy ~10 min po wyjściu z aplikacji, jeśli coś
  się zmieniło (termin wyznacza Android). Bez zmian i bez używania aplikacji nic się nie dzieje.
- **+ D3:** zamek wspólny z odtworzeniem, konfiguracją i „Zrób kopię teraz” oraz `busy_timeout` na
  połączeniu aplikacji. To odpowiedź na *Input from ISSUE-009*, z testami.
- **+ stempel danych i źródło kopii w `backup.json`**, czyli poza bazą: bez migracji, bez zmiany odcisku.
- **+ ekran „Stan danych”:** przy ostatniej udanej kopii dopisek **„(w tle)”** i jedno zdanie o
  harmonogramie (*„Kopia w tle: kilka minut po wyjściu z aplikacji, jeśli coś się zmieniło; dokładny
  termin wyznacza Android.”*). Bez tego autor nie zobaczy w aplikacji dowodu na AC-1.
- **+ README `grobing-code` → „Kopia” → „Kopia w tle”.**

### Steps (dev)
1. **Falsyfikator: Dart w tle zapisuje do Dysku (≤ 2 h), przed czymkolwiek innym.** Zadanie
   `androidx.work` (Kotlin) startuje bezgłowy silnik i rejestruje w nim `BackupDocuments`. Okna w tle
   zwracają błąd, a nie wiszą. Potem silnik uruchamia funkcję Darta, która woła istniejące
   `BackupService.backUpNow()`. Pomiar na `Medium_Phone` z kopią skonfigurowaną do Dysku:
   - **(a)** aplikacja zamknięta (przesunięta z ostatnich), zadanie wymuszone
     `adb shell cmd jobscheduler run -f com.grobing.app <id>` (jak M2a) → nowa „Ostatnia udana kopia” w
     `backup.json`, nowa godzina pliku w Dysku;
   - **(b)** to samo przy **otwartej** aplikacji (dwa połączenia z bazą);
   - **(c)** to samo w **buildzie release**, gdzie `vm:entry-point` może zostać wycięty. Zmianę danych w
     release daje odtworzenie: świeża instalacja → konfiguracja → odtworzenie kopii z danymi.

   **(a) albo (c) nie przechodzi → STOP i raport:** wariant zapasowy D1 wymaga decyzji autora.
2. **Wyzwalanie (D2):** obserwator cyklu życia w korzeniu aplikacji (`GrobingApp`) przy `paused` oraz
   `_open` z `main.dart` przy starcie. Oba wyzwalają tylko przy kopii skonfigurowanej i stemplu ≠ stempel
   ostatniej udanej kopii. Decyzję „wyzwolić czy nie” podejmuje Dart, więc da się ją przetestować na
   hoście. Jedna metoda kanału (np. `requestBackgroundBackup`) zakłada unikalne zadanie jednorazowe z
   opóźnieniem ~10 min i `StorageNotLow`. Politykę WorkManagera dobiera `dev` pod niezmienniki (i)-(iv) z
   D2. Wyzwalanie nie trzyma `GrobingDatabase`, bo każdy przebieg otwiera własne połączenie, a po
   odtworzeniu obserwator czyta bieżące dane z korzenia. Warunek *Input from ISSUE-009* („otworzyć od nowa
   po przeładowaniu”) jest więc spełniony konstrukcyjnie. Wersję `androidx.work` zgodną z `compileSdk`
   wybiera i zapisuje `dev`.
3. **Przebieg w tle w Darcie** (np. `lib/backup/background_backup.dart`). Logika jest testowalna na
   hoście, a punkt wejścia to cienka funkcja z `@pragma('vm:entry-point')`. Kolejność:
   1. kopia nieskonfigurowana → koniec;
   2. zamek (D3); zajęty → ponów później;
   3. jest `restore.json` → koniec bez kopii (dokończy start aplikacji, który znów wyzwoli kopię);
   4. `user_version` ≠ wersja aplikacji → koniec bez kopii, jak wyżej. Odczyt bez otwierania klasą bazy,
      żeby nie ruszyć migracji;
   5. stempel = stempel ostatniej udanej kopii → koniec (D2);
   6. `backUpNow()` z tym samym archiwum i tym samym zapisem do Dysku, ze źródłem „w tle”. Nieudana →
      ponów później (D2 iv);
   7. stempel po kopii ≠ stempel zapisany przed migawką → jeszcze jedna kopia (D2 iii);
   8. zamknięcie bazy, zwolnienie zamka.

   Kotlin kończy zadanie po sygnale z Darta albo po limicie czasu i **zawsze** zwalnia zamek i niszczy
   silnik, także gdy system zatrzyma zadanie. Wynik i błąd trafiają do `backup.json` jak przy przycisku,
   bez ścieżek i treści. Kotlin nie otwiera `grobing.db` (D3).
4. **Zamek (D3) w odtworzeniu, w konfiguracji i w „Zrób kopię teraz”:** zajęty → *„Trwa kopia w tle —
   spróbuj za chwilę.”*, a dane i konfiguracja zostają nietknięte. Odtworzenie trzyma zamek od walidacji
   po przeładowanie, konfiguracja — od pierwszego okna po zapis `backup.json` i pierwszą kopię.
5. **`busy_timeout`** na połączeniu aplikacji (`GrobingDatabase.atFile`) i w przebiegu w tle (kilka
   sekund; wartość wybiera `dev`).
6. **`backup.json`:** stempel z ostatniej udanej kopii i jej źródło (przycisk / w tle). Stary plik bez tych
   pól czyta się jak „zmiana” (jedna kopia po aktualizacji).
7. **Ekran „Stan danych”:** dopisek „(w tle)” i zdanie o harmonogramie (*Scope diff*). Ekran techniczny w
   istniejącym motywie, więc agent `ui` nie jest potrzebny.
8. **Pomiar terminu (AC-1, „zapisany, nie obiecany”):** zadanie **bez wymuszania** na emulatorze. Ile
   minut od wyjścia z aplikacji do kopii — wynik w *Dev report*.
9. **README `grobing-code` → „Kopia” → „Kopia w tle”:** D1-D3, wyzwalacze i opóźnienie, limit ~10 min na
   zadanie, zakaz drugiej kopii SQLite, wymuszenie przez `adb` do testów.

### Files likely touched
`grobing-code`:
- `android/app/build.gradle.kts` (`androidx.work`);
- `android/app/src/main/kotlin/com/grobing/app/`: nowe zadanie w tle i kanał (harmonogram, zamek, koniec
  przebiegu); nazwy należą do `dev`. Do tego `MainActivity.kt` (rejestracja kanału) i `BackupDocuments.kt`
  (bez okien w tle);
- `lib/backup/background_backup.dart` (nowy) · `backup_service.dart` (zamek, stempel, źródło) ·
  `backup_settings.dart` · `restore_service.dart` (zamek);
- `lib/data/database.dart` (`busy_timeout`) · `lib/main.dart` (wyzwolenie przy starcie, punkt wejścia) ·
  `lib/app/grobing_app.dart` (obserwator cyklu życia) · `lib/app/data_state_screen.dart`;
- `README.md`;
- testy (`qa`): `test/backup/background_backup_test.dart`, test dwóch połączeń, `test/support/backup_fakes.dart`
  (sztuczny zamek i harmonogram).

`grobing-vault`: ta pozycja · `TRACEABILITY.md`.

### AC → tests (`qa`)
| AC | Test happy-path (host) | Ręcznie / emulator |
|---|---|---|
| AC-1 kopia w tle po zmianie, bez hasła | **wyzwalanie:** `paused` i start przy zmienionym stemplu → zadanie zamówione; przy niezmienionym albo kopii nieskonfigurowanej → nie. **Przebieg w tle** (sztuczny Dysk, zamek i harmonogram): zmiana danych → kopia **bez hasła** i bez okna, „w tle” i stempel w `backup.json`. **Bez zmiany → nic nie zapisane** (także po samym otwarciu i zamknięciu bazy). Zamek zajęty → „ponów”, a dane i `backup.json` bez zmian. Znacznik `restore.json` / `user_version` ≠ aplikacja → koniec bez kopii, dane nietknięte. Zmiana w trakcie kopii → jeszcze jedna kopia. Błąd Dysku → wynik zapisany jak przy przycisku i „ponów”. Konfiguracja przy zajętym zamku → odmowa, `backup.json` bez zmian. **Próbne odtworzenie:** kopia zrobiona przebiegiem w tle → odtworzenie do pustego katalogu → odcisk = źródło. Odtworzenie przy zajętym zamku → odmowa, dane nietknięte. Dwa połączenia: zapisy w jednym izolacie + `VACUUM INTO` w drugim → bez `SQLITE_BUSY`, `integrity_check` `ok` | stop #2 (niżej) · release (krok 1c) · termin bez wymuszania (krok 8) |
| AC-2 zależności, bez `INTERNET` | `test/no_cloud_sdk_test.dart` bez zmian (paczek pub nie przybywa) | `aapt` na APK release: lista uprawnień (oczekiwane z M3), **bez `INTERNET`**; przegląd `androidx.work` → NFR-005 |

### Manual verification (stop #2) — kroki według miejsca
> Jeden emulator naraz (RAM). `qa` przed krokami sprawdza, który build jest zainstalowany, i porównuje
> odpowiedź ze stanem emulatora.

- **Terminal VS Code** (`grobing-code`): `flutter run` na `Medium_Phone` (debug, bo potrzebne są wymyślone
  dane). Uruchamia `qa`.
- **Emulator `Medium_Phone`:**
  1. „Stan danych” → sekcja „Kopia” skonfigurowana. Jeśli nie jest: „Skonfiguruj kopię”, hasło
     **testowe**, oba pliki w Dysku. Czy zdanie o kopii w tle jest jasne?
  2. „Wgraj wymyślone dane” → zapisz pierwsze 16 znaków odcisku (**B**).
  3. Wyjdź z aplikacji i zamknij ją: przesuń ją z ostatnich.
- **Napisz tutaj:** „zamknięte” → `qa` wymusza zadanie przez `adb`. Możesz też zamiast tego odczekać
  ~10 min (zobaczysz zachowanie naturalne; Android bywa wolniejszy).
- **Emulator `Medium_Phone`:**
  4. Otwórz aplikację → „Stan danych”: „Ostatnia udana kopia” ma nową godzinę z dopiskiem **„(w tle)”**,
     bez komunikatu o błędzie.
- **Przeglądarka na PC:** drive.google.com → plik kopii ma nową godzinę. Dysk może się spóźnić o kilka
  minut.
- **Emulator `Medium_Phone`** — próbne odtworzenie kopii zrobionej w tle:
  5. „Wgraj wymyślone dane” jeszcze raz → odcisk się zmienia.
  6. „Odtwórz z kopii” → plik kopii z Dysku, plik klucza, hasło testowe → „Zastąp dane” → *„Odtworzono kopię
     z dnia …”* z godziną z kroku 4, a **odcisk = B**.
- **Napisz tutaj:** „ok” · „pomiń” · opis błędu.

### Closing checklist (docs)
- [[US-001-kopia-z-odtworzeniem]]: AC-1 pokryte, wszystkie cztery ISSUE przyjęte → zamknięcie US według
  DoD US (werdykt, *Story Status* w `TRACEABILITY.md`).
- [[ADR-004-backup-format-encryption-destination]] → *Follow-ups*: datowana linia — kopia w tle zamknięta
  w kodzie (D1-D3), zmierzony termin, limit ~10 min na zadanie (przy ~8 MB/s to kopia rzędu kilku GB).
- [[NFR-005-dane-nie-opuszczaja-telefonu]] → *Notes*: `androidx.work` przejrzane, uprawnienia z APK
  release, nadal bez `INTERNET`.
- [[US-005-zdjecia]] → *Notes*: opóźnienie D2 (~10 min) do ponownej decyzji przy pierwszych zdjęciach.
  Każda kopia wysyła całość, a każde zdjęcie z aparatu systemowego to wyjście z aplikacji (`paused`).
- `CURRENT_STATE.md`: przed pierwszymi prawdziwymi danymi zostaje [[NT-007-hand-over-note]] (+ kopia
  klucza wydania).
- `ideal_days` według D4.
- Bez pusha: [[NT-008-publication-review]] otwarte.

### Out of Scope (this plan)
- Powiadomienia (pozycja: *Out of Scope*) i kopia przyrostowa.
- Wyłączanie kopii w tle i wybór opóźnienia w aplikacji.
- Kopia okresowa (odrzucona na stopie #1).
- Zadanie na pierwszym planie (`setForeground`) dla kopii dłuższych niż ~10 min — dopiero gdy zdjęcia
  do tego dojdą (US-005).
- Historia kopii i rotacja plików (*Known limits* w `backup-format.md`).
- Spójność zdjęć dodanych albo usuniętych w trakcie kopii (migawka bazy a katalog zdjęć). To było już przy
  przycisku i dotyczy US-005.

### Self-check (planning) — said out loud
- **Wyzwalanie zdarzeniem ma jedną dziurę, której harmonogram nie miał:** po wyczerpaniu ponowień (np.
  Dysk wylogowany) kolejna próba czeka na następne użycie aplikacji, a przy rzadkim używaniu to mogą być
  tygodnie. Błąd widać na „Stanie danych”, ale tylko temu, kto tam zajrzy. Powiadomienia są poza zakresem;
  to kandydat na pytanie przy retro, nie na rozszerzenie teraz.
- **Android może odłożyć kopię dłużej niż ~10 min:** M2a (> 44 min), a po „Wymuś zatrzymanie” zadania
  czekają do następnego otwarcia. Dlatego AC mówi „termin zapisany, nie obiecany”, a ekran — „termin
  wyznacza Android”.
- **Zadanie przerwane przez system** (limit ~10 min, brak pamięci) nie zdąży zapisać błędu. W
  `backup.json` zostaje poprzednia udana kopia, a następne wyzwolenie (start aplikacji) próbuje od nowa.
- **Zamek zakłada, że zadanie biegnie w procesie aplikacji** (domyślne w WorkManager). Osobny proces
  złamałby D3.
- **Dwa telefony** (*Known limits*): po D2 stary telefon bez zmian nic nie zapisze. Telefon, na którym coś
  się zmieni, nadpisze plik.

## Dev report
> `dev`, 2026-10-06. **Stop #1:** autor „tak” z poprawką D2 (wyzwalanie wyjściem z aplikacji). Kod w
> `grobing-code`, niezacommitowany. Flutter 3.41.1 (przypięty). `flutter analyze lib tool` bez uwag.
> `androidx.work:work-runtime` **2.11.2**: dojrzała linia z poprawkami, `minSdk` 23 przy naszym 24.
> 2.12.0 ma dwa tygodnie i podnosi `minSdk` do 24.

### Step 1 — falsifier: ✅ passed (a), (b), (c)
Zadanie `BackupWorker` (Kotlin, `androidx.work`) startuje bezgłowy `FlutterEngine`, rejestruje w nim
`BackupDocuments` bez okien i kanał `com.grobing.app/background`, potem uruchamia `backgroundBackupMain`.
Wymuszenie: `cmd jobscheduler run -f -n androidx.work.systemjobscheduler com.grobing.app <id>`.
- **(a) bez ekranu aplikacji, `Medium_Phone`, debug:** proces aplikacji zabity (`am kill`), więc proces
  uruchomił JobScheduler bez `MainActivity`. Wynik: silnik Fluttera załadowany w ~0,9 s, `Worker result
  SUCCESS` ~7 s po starcie. `backup.json`: nowa „ostatnia udana kopia”, stempel,
  `last_success_in_background: true`. Zapis do pliku w Dysku (`Grobing-proba`) przyjęty bez błędu.
- **(b) przy otwartej aplikacji (dwa połączenia z bazą):** „Wgraj wymyślone dane” (odcisk
  `ff6d4202e5b6c0a2`, 6 osób) → wyjście z aplikacji → **zadanie zamówione przez `paused`** → powrót do
  aplikacji → wymuszenie przy aplikacji na pierwszym planie → `SUCCESS` po 5 s. Potem w aplikacji:
  „Odśwież” czyta bazę normalnie, a ekran pokazuje „2026-10-06 11:19 (w tle)”. „Zrób kopię teraz” działa
  od razu, więc zamek został zwolniony: 11:20, bez dopisku. Katalog roboczy kopii jest usunięty.
- **(c) build release (AOT), `Grobing_Restore`:** aktualizacja tym samym kluczem na buildzie z ISSUE-009
  (dane z odtworzenia, odcisk `cac13dcd1f3fb213`, `backup.json` bez stempla, więc start zamówił kopię) →
  wyjście, `am kill`, wymuszenie → `SUCCESS` po 2,3 s. Na ekranie „Ostatnia udana kopia 2026-10-06 11:24
  (w tle)”. **`vm:entry-point` przetrwał kompilację AOT.**

### Smoke checks (dev)
- **Wyjście bez zmian → zadania nie ma** (0 w `dumpsys jobscheduler`) po otwarciu, odczycie i odświeżeniu
  „Stanu danych”. Stempel nie zmienia się od samego otwarcia bazy (D2 *obali ją*: nie obaliło).
- **Wyjście po zmianie → jedno zadanie z opóźnieniem** `TIME=+9m58s`, warunek `STORENOTLOW`.
- **APK release (`aapt dump permissions`):** `WAKE_LOCK`, `ACCESS_NETWORK_STATE`, `RECEIVE_BOOT_COMPLETED`,
  `FOREGROUND_SERVICE` (to co M3) + `DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION`. **Bez `INTERNET`.**
  Paczek pub nie przybyło (`pubspec.yaml` bez zmian).
- **Termin bez wymuszania (krok 8):** `Medium_Phone`, debug, ekran wygaszony nie był, emulator na
  zasilaniu. Wyjście z aplikacji o 11:26:42 UTC → start zadania o 11:37:29 (**10 min 47 s**, czyli
  opóźnienie 10 min + 47 s JobSchedulera) → `SUCCESS` o 11:37:38 (9 s). Jeden pomiar na emulatorze, bez
  Doze. To termin zapisany, nie obiecany (M2a: bywało > 44 min).

### Deviations from the plan
- **Stempel ma jeszcze licznik zmian z nagłówka SQLite** (offset 24, *file change counter*, zwiększany
  przy każdym zatwierdzonym zapisie w trybie dziennika wycofania —
  [fileformat2](https://www.sqlite.org/fileformat2.html#file_change_counter)). Czas modyfikacji pliku w
  Linuksie ma ziarno kilku milisekund, więc dwa zapisy o tym samym rozmiarze w jednym „tyknięciu” po obu
  stronach migawki dałyby ten sam stempel. Licznik jest dokładny i czyta się go bez otwierania bazy.
- **Odtworzenie zwalnia zamek po podmianie, a nie po przeładowaniu.** Przeładowanie robi `GrobingApp`, już
  poza `RestoreService`. Bezpieczne, bo przebieg w tle, który wystartuje w tej chwili, widzi albo
  skończone dane, albo — po przerwanej podmianie — znacznik, którego nie rusza (D3).
- **Polityka zamawiania (D2 i-iii):** `request()` w Kotlinie nie robi nic, gdy zadanie czeka (`ENQUEUED`
  albo `BLOCKED`), a w przeciwnym razie `APPEND_OR_REPLACE`: biegnące zostaje, nowe idzie za nim.
  Przebieg, który po kopii widzi inny stempel, kończy się `again`, a Kotlin zamawia następne. Ponowienia
  (iv): 4 próby, odstęp wykładniczy od 1 min. Limit odpowiedzi Darta: 9 min, czyli poniżej limitu
  WorkManagera.
- **Brak pliku bazy → koniec bez kopii** (nic do kopiowania).
- `GrobingDatabase.currentSchemaVersion` jako stała: przebieg w tle porównuje `user_version` bez
  otwierania klasy bazy.
- `MainActivity.cleanUpFlutterEngine` zwalnia zamek: silnik zniszczony w trakcie odtworzenia albo kopii
  go nie zatrzyma. Zadanie w tle zwalnia go w `finally`, także gdy system je zatrzyma.

### For qa
- **Nie kompilują się trzy miejsca w testach** (wymagany `lock`): `test/support/backup_fakes.dart:120`
  (`backupServiceIn`), `:136` (`restoreServiceIn`) i `test/backup/restore_service_test.dart:266`.
  Reszta sygnatur bez zmian. Nowe parametry `GrobingApp` i ekranów nie doszły.
- **Haki do testów:**
  - `DataLock` i `BackgroundBackups` (`lib/backup/background.dart`) to interfejsy pod sztuczny zamek i
    harmonogram;
  - `runBackgroundBackup(dataDir:, workDir:, lock:, documents:, schemaVersion:, openDatabase:, clock:)`
    zwraca `BackgroundOutcome` (`done` / `again` / `retry`);
  - `BackupService.changedSinceLastBackup()` i `requestBackgroundIfChanged()` (z `background:`);
  - `dataStamp(DataLocation)`;
  - `configureConnection` (`busy_timeout`) do testu dwóch połączeń.
- **Stan emulatorów:**
  - `Medium_Phone` działa (`-no-snapshot-save`, więc restart wraca do snapshotu z buildem z 08:21).
    Zainstalowany build debug z 11:26, kopia skonfigurowana do `Grobing-proba` w Dysku, odcisk
    `cac13dcd1f3fb213`; trwa pomiar z kroku 8;
  - `Grobing_Restore` wyłączony; zainstalowany build release z tej pozycji.
- **Środowisko:** po `am kill` WorkManager uznaje zabicie za „wymuszone zatrzymanie” i przeplanowuje
  zadanie pod nowym numerem — przed wymuszeniem trzeba sprawdzić numer w `dumpsys jobscheduler`.
- **Plik `grobing-kopia.age` w `Grobing-proba`** nadpisały w tej sesji oba emulatory (wymyślone dane,
  hasło testowe z ISSUE-009). Na stopie #2 odtwarza się plik zapisany na stopie, więc to nie przeszkadza.

### Round 2 — after stop #2, attempt 1 (author: „jedna kopia po sesji”)
- **Wyzwalacz przy zapisie:** `BackupService.watchChanges()` (`tableUpdates` z `drift`), subskrypcja w
  `GrobingApp` (tworzona w `initState`, wymieniana przy przeładowaniu po odtworzeniu, anulowana w
  `dispose`). Seria zapisów daje najwyżej jedno zamówienie naraz i żadnego nie gubi. `paused` i start
  zostają.
- **Czekanie na ciszę:** przebieg w tle dostaje od Kotlina czas pierwszej zmiany (argument funkcji
  wejścia; `inputData` zadania). Gdy dane zmieniły się < 10 min temu, a od pierwszej zmiany minęło
  < 60 min, kończy się `later` z czasem do końca ciszy (nie dłuższym niż do limitu), a Kotlin zamawia
  kolejny przebieg z tym samym czasem pierwszej zmiany. Cofnięty zegar nie każe czekać. `lastDataChange`
  w `data_stamp.dart` czyta te same metadane co stempel.
- Ekran: *„Kopia w tle: ok. 10 minut po ostatniej zmianie, przy dłuższej pracy co godzinę; dokładny termin
  wyznacza Android.”* README → *Kopia w tle* przepisane.
- **Na urządzeniu (`Medium_Phone`, debug):**
  - zapis danych → **zadanie zapisane 1,5 s po zapisie, przy wciąż otwartej aplikacji** (opóźnienie
    9 min 58 s). Gest do ostatnich + wyrzucenie + zabicie procesu → zadanie nadal jest;
  - przebieg wymuszony 3 min po zmianie (12:03:25) → bez kopii, następny zamówiony na 12:10:34, czyli
    równo 10 min po zmianie. Ten ruszył sam o 12:10:37 → `SUCCESS`, kopia „w tle”;
  - **build profile (AOT, ten sam klucz debug co build debug)** — funkcja wejścia z argumentem: przebieg
    0,7 s → `later` → następny na 12:28:30 (= zmiana 12:18:27 + 10 min).
- **Pomiar, który zostaje:** gdy proces aplikacji żyje, WorkManager uruchamia czekające zadanie sam,
  punktualnie (12:10:37 przy terminie 12:10:34). Gdy proces jest zamrożony albo martwy, termin wyznacza
  JobScheduler: zadanie stało `READY` > 3,5 min i nie ruszyło (stan urządzenia `ACTIVE`, koszyk
  `ACTIVE`). To M2a ze SPIKE-003; zadanie wykonane potem wymuszeniem. Ekran mówi „dokładny termin
  wyznacza Android”.

## Verification
> `qa`, 2026-10-06. Dowody sprawdzone **niezależnie od deklaracji `dev`**: testy napisane przez `qa`,
> stan emulatora czytany po każdej odpowiedzi autora (`backup.json`, czasy plików, `dumpsys
> jobscheduler`, log WorkManagera), APK release zbudowany od nowa po rundzie 2.

### Automated (`flutter test`: 248 passed · `flutter analyze`: no issues · `dart format`: clean)
| AC | Test | Wynik |
|---|---|---|
| AC-1 przebieg w tle | `test/backup/background_backup_test.dart`: zmiana → kopia bez hasła, „w tle”, stempel; plik otwiera się kluczem, manifest = dane na dysku; bez resztek, zamek wolny. Bez zmiany → nic nie zapisane (bajty pliku i `backup.json` identyczne). Po kopii z przycisku → tło nic nie robi. Aplikacja otwarta (drugie połączenie) → kopia, aplikacja pisze dalej. Zmiana w trakcie → `again` z czekaniem 10 min. Dysk odmawia → `retry`, błąd zapisany, zamek wolny. Zamek zajęty → `retry`, nic nie ruszone. Znacznik `restore.json` → koniec bez kopii, znacznik zostaje. Inna wersja schematu → koniec bez kopii, baza nie otwarta klasą aplikacji (`user_version` 1). Brak konfiguracji → zamek nawet nie wzięty | ✅ 11 |
| AC-1 jedna kopia po sesji (D2) | ten sam plik: zmiana minutę temu → `later` 9 min, nic nie zapisane; 10 min ciszy → kopia; ciągła praca od godziny → kopia (limit); czekanie nigdy nie przekracza limitu (55 min → 5 min); cofnięty zegar → kopia od razu; bez zmian → `done` bez czekania | ✅ 6 |
| AC-1 stempel (D2) | otwarcie, odczyt, `VACUUM INTO`, zamknięcie → stempel bez zmian; zapis przy **tym samym rozmiarze i czasie pliku** → stempel inny (licznik zmian SQLite); zdjęcie dodane / usunięte → inny | ✅ 3 |
| AC-1 wyzwalacze | `requestBackgroundIfChanged`: zmiana → zamówienie; zaraz po kopii → nie, po zmianie → tak; brak konfiguracji → nie; błąd kanału nie dociera do aplikacji; `backup.json` sprzed ISSUE-010 → „zmienione”. **`watchChanges`:** seria zapisów → 1-2 zamówienia; po kopii zapis znów zamawia; po anulowaniu — cisza | ✅ 6 |
| AC-1 w aplikacji | `test/app/background_backup_screen_test.dart`: `paused` → jedno zamówienie, `inactive`/`hidden`/`resumed` → żadne; zapis w aplikacji → zamówienie (obserwator w korzeniu); „(w tle)” i zdanie o terminie na „Stanie danych” | ✅ 3 |
| Próbne odtworzenie (DoD) | kopia zrobiona przebiegiem w tle → odtworzenie na świeżym telefonie → odcisk i liczby = źródło | ✅ |
| D3 jedna operacja naraz | „Zrób kopię teraz”, konfiguracja (przed pierwszym oknem) i odtworzenie przy zajętym zamku → odmowa `dataBusyMessage`, nic nie ruszone; zamek zwolniony po sukcesie, błędzie, zamkniętym oknie i odmowie odtworzenia | ✅ 4 |
| D3 dwa połączenia | zapis w aplikacji czeka na blokadę odczytu kopii i przechodzi (`busy_timeout`); **kontrola: bez `busy_timeout` ten sam zapis → „database is locked”**; `VACUUM INTO` z drugiego połączenia przy ciągłych zapisach → wszystkie migawki i baza `integrity_check` `ok` | ✅ 3 |
| (dostosowane) | `test/support/backup_fakes.dart`: `FakeDataLock` (wspólny jak w procesie), `FakeBackgroundBackups`; `restore_service_test.dart`: `lock` | ✅ |

### AC-2 — release build (APK zbudowany od nowa po rundzie 2, `aapt`)
- Uprawnienia: `WAKE_LOCK`, `ACCESS_NETWORK_STATE`, `RECEIVE_BOOT_COMPLETED`, `FOREGROUND_SERVICE` (z
  `androidx.work`, jak SPIKE-003 M3) + `DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION`. **Bez `INTERNET`.**
- `allowBackup=false`, `dataExtractionRules` podpięte. `pubspec.yaml`, `pubspec.lock` i manifest bez zmian;
  `test/no_cloud_sdk_test.dart` przechodzi.
- **Przegląd `androidx.work:work-runtime:2.11.2`** (`gradlew app:dependencies`, release): dochodzi
  `androidx.room` 2.7.0, `androidx.sqlite` 2.5.0 (na systemowym SQLite) i `androidx.startup`. Bibliotek
  sieciowych brak. Room trzyma **własną** bazę WorkManagera (lista zadań, bez danych rodziny), wyłączoną
  z kopii Androida jak całe dane aplikacji. To druga kopia SQLite w procesie, ale **na innym pliku**, a
  `grobing.db` otwiera tylko Dart (§2.3 *How To Corrupt* dotyczy jednego pliku).

### DoD lines specific to Grobing
- **Próbne odtworzenie kopii zrobionej w tle:** test na hoście + stop #2 (podejście 2, krok 6).
- **Test migracji:** schemat bez zmian (v1). Przebieg w tle **nie migruje** — test z wersją 2.
- **Źródło faktu:** n/a.
- **Dane rodziny w zmianach:** brak. W trzech repo tylko pliki tekstowe (kod, testy, README, 2 pliki
  vaulta); żadnych `*.db`, `*.age`, `*.tar`, eksportów, zdjęć. Dane w testach i na emulatorach wymyślone
  (`fictional_data.dart`).

### Manual (stop #2), podejście 2 — **„ok”** (autor, 2026-10-06), sprawdzone na emulatorze
`Medium_Phone`, build debug z rundy 2, kopia do `Grobing-proba` (hasło testowe z ISSUE-009).
- Kroki 1-3: autor wgrał dane (baza zmieniona 12:35:06.08) i **zamknął aplikację tym samym gestem co w
  podejściu 1**. Stan: **zadanie zapisane 12:35:06.50** (0,4 s po zapisie, przy otwartej aplikacji);
  „remove task” 12:35:27; zadanie przetrwało.
- Po 10 min ciszy `qa` wymusił zadanie (12:45:12) → `SUCCESS` 12:45:15, `backup.json`: „w tle”, bez
  błędu. Krok 4: ekran „2026-10-06 12:45 (w tle)” (odczyt `qa`).
- Krok 5: zapis 12:46:49 → zadanie zamówione od razu (log WorkManagera). Krok 6: odtworzenie 12:47:44 →
  *„Odtworzono kopię z dnia 2026-10-06 12:45. Odcisk danych w kopii: c3eda4351a1c4271 — ten sam co
  niżej”*. Kopia z 12:45 niosła dane z kroku 2 (bez zmian między 12:35 a 12:45), więc odcisk = B.
- Krok w przeglądarce (godzina pliku w Dysku): tylko potwierdzenie autora, stąd niewidoczne.
- Po kroku 6 czeka zadanie z kroku 5: po ciszy zapisze do Dysku odtworzone dane, czyli te same (*Input
  from ISSUE-009*).

### Manual (stop #2), podejście 1 — **błąd znaleziony przez `qa` przy sprawdzeniu stanu emulatora**
- Autor: kroki 1-3, potem „zamknięte”. Stan emulatora: dane zmienione o 11:43:07 (doszedł plik
  `nota-2.txt`), ale **zadania w tle nie było**, a `backup.json` był bez zmian od 11:37.
- **Przyczyna — wyścig wyzwalacza `paused` z zamknięciem aplikacji gestem.** Log autora: aplikacja
  przesunięta do ostatnich (`TO_BACK`) o 11:43:31.24, wyrzucona z ostatnich i zabita („remove task”) o
  11:43:33.22, czyli po 2,0 s. Pomiar `qa` tym samym gestem: od `TO_BACK` do zapisania zadania w
  WorkManagerze mija **1,7 s** (Android wysyła `onStop` → `paused` po animacji gestu, potem stempel, kanał
  i zapis zadania). Kto szybko wyrzuca aplikację z ostatnich, przegrywa wyścig, a zmiana czeka na
  następne otwarcie aplikacji — przy rzadkim używaniu tygodnie. Wyjście przyciskiem ekranu głównego i
  gest bez wyrzucenia działają (zadanie zapisane po ~1-2 s).
- Fałszywy trop po drodze: `adb shell input keyevent KEYCODE_APP_SWITCH` nie chowa aplikacji na tym
  obrazie (aktywność zostaje `RESUMED`), więc nie nadaje się do odtwarzania gestu; gest to
  `input swipe 540 2395 540 1300 700`.
- Diagnoza zmieniała dane na `Medium_Phone` (wymyślone, kilka razy „Wgraj wymyślone dane”) i robiła kopie
  w tle do `Grobing-proba` — stop #2 trzeba powtórzyć od kroku 1 po poprawce.

### Verdict (self-check)
**APPROVED** z uwagami. AC-1: kopia powstaje po zmianie danych bez hasła, także gdy aplikację zamknie się
gestem zaraz po zmianie; jedna kopia po sesji (cisza 10 min, limit 60 min); kopię zrobioną w tle
odtworzył człowiek z odciskiem zgodnym. AC-2: bez `INTERNET`, zależność przejrzana. Stop #2 w podejściu 1
znalazł błąd (wyścig wyzwalacza), poprawiony w rundzie 2 i sprawdzony tym samym gestem.

**Czego szukałem i nie znalazłem:**
- kopii przy niezmienionych danych (bajty pliku identyczne; wyjście bez zmian nie zamawia zadania);
- zmiany stempla od samego otwarcia, odczytu i `VACUUM INTO`;
- przebiegu w tle, który rusza bazę przy znaczniku odtworzenia albo migruje;
- operacji na danych, która przechodzi przy zajętym zamku; zamka, który zostaje po błędzie;
- `SQLITE_BUSY` przy dwóch połączeniach (z kontrolą, że bez `busy_timeout` błąd jest);
- zadania zgubionego przez zabicie procesu po zapisie;
- wycięcia funkcji wejścia w kompilacji AOT (release w rundzie 1, profile w rundzie 2);
- `INTERNET`, bibliotek sieciowych, danych rodziny w zmianach.

**Uwagi, które nie blokują:**
1. **Przy zamkniętej aplikacji termin wyznacza JobScheduler:** zadanie gotowe stało > 3,5 min i nie
   ruszyło (M2a: bywało > 44 min). Gdy proces żyje, WorkManager uruchamia je punktualnie. Ekran mówi
   „dokładny termin wyznacza Android”. Kopia nie ginie, tylko się spóźnia.
2. **Po wyczerpaniu 4 ponowień** (np. Dysk wylogowany) kolejna próba czeka na następny zapis albo start
   aplikacji. Widać to tylko na „Stanie danych” (*Self-check* `planning`) — pytanie do retro.
3. Funkcję wejścia **z argumentem** w AOT sprawdził build profile (ten sam kompilator AOT, klucz debug), a
   release — wersję bez argumentu (runda 1). Następny build release na emulatorze potwierdzi to wprost.
4. Limit 60 min wybrał `dev`; autor poprosił o „górny limit” bez liczby.
5. Stempel nie widzi zdjęcia zmienionego „w miejscu” z tym samym rozmiarem i czasem pliku. Aplikacja
   zdjęć nie edytuje w miejscu — do pamiętania przy [[US-005-zdjecia]].
6. Środowisko: `am kill` i aktualizacja pakietu sprawiają, że WorkManager przeplanowuje zadanie pod nowym
   numerem; przed wymuszeniem trzeba sprawdzić numer (README → *Do testów*).
