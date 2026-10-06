---
title: "ISSUE-008 — Production backup: encrypted on the phone, one age file in the author's Drive"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-001-kopia-z-odtworzeniem]]"
ideal_days: 1
quality-verdict: APPROVED
verdict-date: 2026-10-06
verdict-reviewer: self-check
created: 2026-10-05
updated: 2026-10-06
---

# ISSUE-008 — Kopia: zapis

> Mechanizm jest rozstrzygnięty w [[ADR-004-backup-format-encryption-destination]] (pkt 1-4) i zmierzony w
> [[SPIKE-003-backup-and-restore]] → *Findings*. Kod spike'a został usunięty, więc to jest budowa od
> nowa, na pomiarach. Musi działać **przed pierwszymi prawdziwymi danymi** (ADR-004 → *Follow-ups*).

## What to build
1. **Konfiguracja kopii (raz):**
   - tożsamość X25519 i plik tożsamości zaszyfrowany hasłem (scrypt, work factor 18), zapisany przez
     systemowe okno zapisu pliku;
   - w aplikacji zostaje tylko klucz publiczny;
   - plik kopii w Dysku wskazany oknem zapisu pliku (`ACTION_CREATE_DOCUMENT`) z trwałym uprawnieniem
     do odczytu i zapisu.

   Hasło autor wpisuje w aplikacji. Żaden plik z hasłem nie powstaje.
2. **Format (ADR-004 pkt 2):** własny moduł `age` v1 na `cryptography` i `pointycastle`; `tar` z
   `manifest.json` (`format_version`, `schema_version`, liczby rekordów, SHA-256 każdego pliku),
   migawką `VACUUM INTO` i `media/*`.
3. **Zapis:** nadpisanie pliku kopii w trybie `"wt"`. „Zrób kopię teraz" oraz kopia w tle bez hasła.
   Kiedy kopia w tle się uruchamia, wybiera `planning`; termin wykonania wyznacza Android.
4. **„Ostatnia udana kopia: kiedy"** na ekranie „Stan danych" (uwaga `qa` ze SPIKE-003). Uczciwie:
   aplikacja wie, że Dysk przyjął plik, nie że go wysłał (ADR-004, *Consequences*).
5. **`allowBackup="false"` i `dataExtractionRules`** wykluczające wszystko w `<cloud-backup>` i
   `<device-transfer>` (ADR-004 pkt 4).

## Acceptance Criteria
- [ ] Po jednorazowej konfiguracji „Zrób kopię teraz" zapisuje w Dysku jeden plik `age`, a ekran
      „Stan danych" pokazuje czas ostatniej udanej kopii.
- [ ] Kopia w tle powstaje po zmianie danych bez pytania o hasło (zmierzone na emulatorze; termin
      zapisany, nie obiecany).
- [ ] **Bramka zgodności (`qa`):** plik kopii + plik klucza + hasło otwierają się na PC oficjalnym
      `age` (`age -d`, potem `age -d -i`) i zwykłym `tar`. Wszystkie SHA-256 zgadzają się z manifestem,
      `integrity_check` = `ok`, a odcisk danych zgadza się z ekranem „Stan danych".
- [ ] Kopia Androida i transfer D2D nie obejmują danych `com.grobing.app`, sprawdzone tak samo jak M7
      w spike'u.
- [ ] Bez kluczy API, sekretów OAuth i uprawnienia `INTERNET` dla kopii; nowe zależności przejrzane
      ([[NFR-005-dane-nie-opuszczaja-telefonu]]).

## Out of Scope
- Odtworzenie w aplikacji → [[ISSUE-009-restore]].
- Eksport HTML + PDF → [[US-006-eksport-dla-rodziny]].
- Treść notki przekazania (hasło, miejsce pliku klucza) → [[NT-007-hand-over-note]].
- Kopia przyrostowa (ADR-004, *Options*: niewykonalna przez okno systemowe).

## Technical Notes
- Pomiary do wykorzystania (SPIKE-003 → *Findings*): czyste szyfrowanie w Darcie ~8 MB/s
  (`cryptography_flutter` jako opcja); scrypt tylko przy konfiguracji i odtworzeniu, nigdy przy kopii w
  tle; Dysk w oknie zapisu pliku działa w tle i przeżywa restart; termin kopii w tle od ~1 min do > 44 min.
- Próbne odtworzenie z DoD, zanim powstanie [[ISSUE-009-restore]]: oficjalne CLI na PC (bramka zgodności
  wyżej), tak jak M5 w spike'u.
- Dane do pokazania: wymyślone, mechanizmem z [[ISSUE-007-data-layer]] (nigdy w buildzie release).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-007-data-layer]] | technical | `done` |
| [[ADR-004-backup-format-encryption-destination]] | technical | `accepted` |
| emulator `Grobing_Restore` z kontem Google autora | technical | istnieje (SPIKE-003) |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC · ręczna weryfikacja na
emulatorze · próbne odtworzenie (tu: oficjalnym CLI) · zero danych rodziny w zmianach (pliki `*.age` w
żadnym repo — strażnik [[ISSUE-006-setup-family-data-guard]]) · INVEST self-check.

## Implementation plan
> `planning`, 2026-10-06. **DoR:** jasny zakres ✅ (ADR-004 pkt 1-4) · powiązana US:
> [[US-001-kopia-z-odtworzeniem]] ✅ · krok ścieżki: n/a, poza ścieżką (M8) ✅ · `task-level` ✅.
> **Warstwa danych:** schemat się **nie** zmienia (stan kopii żyje poza bazą, krok 5), więc testu migracji
> nie ma · próbne odtworzenie — oficjalnym CLI na PC (bramka AC-3), bo odtworzenie w aplikacji to
> [[ISSUE-009-restore]] · źródło faktu — **n/a**, pozycja nie zapisuje faktów o rodzinie (dane wymyślone,
> tylko w buildzie debug).

### Prior art (sources, not memory)
- **Format `age` v1:** specyfikacja [C2SP age](https://c2sp.org/age). Oficjalne wektory testowe:
  [C2SP/CCTV `age/testdata`](https://github.com/C2SP/CCTV/tree/main/age) (147 plików, sprawdzone
  2026-10-06). README: implementacja może *„just attempt to decrypt the test files, check the operation
  only succeeds if `expect` is `success`, and compare the decrypted payload"*; kopia wektorów w projekcie
  jest dozwolona *„without attribution"*. **Granica:** wektory *„can't be used to test the encryption
  direction end-to-end"*, więc szyfrowanie sprawdza round-trip i oficjalne CLI (bramka AC-3).
- **Plik tożsamości chroniony hasłem:** README `age` →
  [*Passphrase-protected key files*](https://github.com/FiloSottile/age#passphrase-protected-key-files):
  `age -d -i key.age` sam pyta o hasło. Zmierzone w SPIKE-003, M5.
- **tar:** format ustar, POSIX `pax` →
  [*ustar Interchange Format*](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/pax.html#tag_20_92_13_06):
  nagłówki po 512 B, nazwa do 100 znaków + prefiks do 155.
- **Paczki z przypiętym Dartem 3.11.0** (API pub.dev, 2026-10-06): `cryptography` 2.9.0 (Dart ≥ 3.3) ✅ ·
  `pointycastle` 4.0.0 (^3.2) ✅, spike użył 3.9.1 · `workmanager` 0.10.10 (Dart ≥ 3.5, Flutter ≥ 3.38) ✅,
  potrzebny dopiero do kopii w tle (D1).
- **Kopia Androida i D2D:** ADR-004 pkt 4 i SPIKE-003 M7 (źródła tam).

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego · czego to nie da · co obali |
|---|---|---|---|
| D1 | **Rozmiar** (`ideal_days: 1` przy 5 punktach budowy) | **Kopia w tle (pkt 3, AC-2) → nowa pozycja `ISSUE-010`.** ISSUE-008 = konfiguracja, format, „Zrób kopię teraz", „ostatnia udana kopia", `allowBackup` | ISSUE to ~0,5-1 dnia (`glossary.md`), a całość to ~1,5-2 dni. Kopia w tle ma własną niewiadomą, której spike nie zmierzył (*Follow-ups*: „sprawdził natywny zapis w tle, nie szyfrowanie w tle"): Dart w tle, kanał do Dysku w silniku bez Activity, dwa połączenia z bazą naraz. Ma też własną decyzję: kiedy się uruchamia. **Czego nie da:** do ISSUE-010 kopia powstaje tylko na przycisk. Prawdziwych danych i tak jeszcze nie ma, bo masowe przepisywanie czeka na całą US-001. **Alternatywa:** całość tutaj, `ideal_days: 2` |
| D2 | **Format kopii v1** — kontrakt, który zamraża pierwsza prawdziwa kopia | `age` v1 do jednego odbiorcy X25519. W środku `tar` ustar (tylko zwykłe pliki, ścieżki ASCII): `grobing.db` (migawka `VACUUM INTO`), `media/…`, **`manifest.json` na końcu**. Manifest: `format_version: 1`, `created_at` (UTC), `schema_version`, `record_counts`, **`data_fingerprint`**, `files[]` (`path`, **`size`**, `sha256`). Plik klucza: tekst tożsamości (jak z `age-keygen`) zaszyfrowany `age` scrypt, work factor 18 | Odtworzenie musi czytać v1 zawsze, więc zmiana to `format_version: 2`. Trzy pola ponad ADR-004, każde dla ISSUE-009: data (pokazać „kopia z dnia…"), odcisk (sprawdzić wynik odtworzenia jedną liczbą — NFR-002 → *Method*), rozmiary (wolne miejsce przed rozpakowaniem — uwaga `qa` ze SPIKE-003). Manifest na końcu: suma liczona w tym samym przebiegu, w którym plik trafia do archiwum, nie rozjedzie się z treścią, a pliki czytamy raz zamiast dwóch. **Obali go:** bramka AC-3 — oficjalne `age` + `tar` nie otworzą |
| D3 | **Moduł `age`** | **Od razu w obie strony** (szyfrowanie + odszyfrowanie), sprawdzany oficjalnymi wektorami C2SP w `flutter test` | Wektory testują tylko odszyfrowanie, więc bez niego moduł nie ma stałej bramki, tylko jednorazowe CLI. Odszyfrowanie i tak jest potrzebne w ISSUE-009 (przesuwa ~0,2 dnia z 009 do 008). **Czego nie da:** szyfrowania wektory nie sprawdzą; to robi round-trip i CLI. **Obali go:** wektory nie przechodzą po ~2 h → STOP (krok 1) |

### Scope diff vs the item (to accept at stop #1)
- **− pkt 3 „kopia w tle" i AC-2** → `ISSUE-010` (D1), pozycję zakłada `docs`.
- **+ odszyfrowanie** w module `age` i wektory C2SP (D3).
- **+ trzy pola manifestu ponad ADR-004** (D2) i specyfikacja formatu v1 w vaulcie (checklista `docs`).
- **+ konfiguracja kończy się pierwszą kopią:** pusty plik w Dysku niczego nie chroni.
- **+ `tool/fingerprint.dart`:** odcisk danych z rozpakowanej kopii na PC, **tą samą funkcją** co ekran.
  Bez niego bramka AC-3 nie ma jak porównać odcisku.

### Steps (dev)
1. **Falsyfikator: moduł `age` (≤ 2 h), przed czymkolwiek innym.** `lib/backup/age/`:
   - nagłówek (stanze X25519 i scrypt, HMAC), strumień ChaCha20-Poly1305 w kawałkach 64 KiB, Bech32
     (`age1…`, `AGE-SECRET-KEY-1…`);
   - scrypt z `pointycastle`, reszta z `cryptography`;
   - strumieniowo w obie strony (spike, 157 MB: szczyt pamięci 195 MB).

   Sprawdzenie skryptem próbnym w scratchpadzie (jak smoke check w ISSUE-007): wektory C2SP poza `armor_*`
   i `hybrid_*` (tych funkcji nie używamy) + round-trip 0 B, 1 B, 64 KiB ± 1, 128 KiB, hasło z polskimi
   znakami. Stały test pisze `qa`. **Wektory nie przechodzą → STOP i raport.**
2. **Archiwum** (`lib/backup/backup_archive.dart`):
   - `VACUUM INTO` do pliku tymczasowego w katalogu cache;
   - liczby rekordów i odcisk z migawki (`readDataState`, ta sama definicja co ekran);
   - tar ustar strumieniowo: `grobing.db`, `media/…` po ścieżce, `manifest.json` na końcu; SHA-256 i
     rozmiar liczone w tym samym przebiegu;
   - szyfrowanie `age` → plik tymczasowy.

   Migawka i plik tymczasowy znikają w `finally`; resztki po przerwanej kopii — na starcie następnej.
   Ścieżka spoza ASCII albo za długa dla ustar → błąd, nie cicha zmiana nazwy.
3. **Kanał natywny** (`MainActivity.kt` + nowy plik Kotlin, bez paczki pośredniej, jak w spike'u):
   - utworzenie dokumentu (`ACTION_CREATE_DOCUMENT`);
   - trwałe uprawnienie odczyt + zapis;
   - kopiowanie pliku lokalnego do URI w trybie `"wt"`;
   - sprawdzenie, czy uprawnienie żyje.

   Zapis potrzebuje tylko `Context`, nie Activity — z tego skorzysta ISSUE-010.
4. **Konfiguracja** (`lib/backup/backup_setup.dart` + ekran):
   - akapit: „hasło + plik klucza + plik kopii = odtworzenie; utrata hasła albo pliku klucza = utrata
     kopii" (brief §Security);
   - hasło dwa razy, ukryte;
   - nowa tożsamość X25519;
   - plik klucza: scrypt (work factor 18) w `Isolate.run` z widocznym postępem (~15 s, M4);
   - okno zapisu `grobing-klucz.age` (zapis raz, bez trwałego uprawnienia);
   - okno zapisu `grobing-kopia.age` (trwałe uprawnienie);
   - pierwsza kopia.

   W aplikacji zostaje tylko klucz publiczny `age1…`. Hasło i tożsamość nigdy nie trafiają na dysk, do
   logów ani do komunikatów błędów. Przerwanie w dowolnym kroku → konfiguracja nie powstaje.
5. **Stan kopii poza bazą:** `backup.json` w katalogu wsparcia (klucz publiczny, URI pliku kopii, czas
   ostatniej udanej kopii, ostatni błąd). **Dlaczego nie w bazie:** czas kopii w bazie zmieniałby odcisk
   przy każdej kopii i wymagałby migracji v2.
6. **„Stan danych" → sekcja „Kopia":**
   - „Skonfiguruj kopię" albo „Zrób kopię teraz";
   - „Ostatnia udana kopia: <data, godzina>" z dopiskiem, że plik przyjął Dysk, a wysyła go aplikacja
     Dysk (ADR-004, *Consequences*);
   - ostatni błąd, jeśli był.

   Ekran techniczny w istniejącym motywie — trigger agenta `ui` nie pada (jak w ISSUE-007).
7. **Android:** `allowBackup="false"` + `dataExtractionRules` → `res/xml/data_extraction_rules.xml`,
   wykluczenie wszystkiego w `<cloud-backup>` i `<device-transfer>` (jak M7).
8. **`tool/fingerprint.dart`:** wersja schematu, liczby i odcisk z katalogu z `grobing.db` + `media/`, na PC.
9. **README `grobing-code` → „Kopia":** format v1 (link do vaulta) · otwarcie bez Grobing
   (`age -d -i grobing-klucz.age grobing-kopia.age | tar -x`) · skąd wektory C2SP · gdzie leży stan
   kopii i dlaczego poza bazą.

### Files likely touched
`grobing-code`: `pubspec.yaml` · `pubspec.lock` (`cryptography`, `pointycastle`) · `lib/backup/` (nowy:
`age/`, `backup_archive.dart`, `backup_setup.dart`, stan kopii) · `lib/app/data_state_screen.dart` · ekran
konfiguracji (nowy) · `android/app/src/main/AndroidManifest.xml` ·
`android/app/src/main/res/xml/data_extraction_rules.xml` (nowy) ·
`android/app/src/main/kotlin/com/grobing/app/` (`MainActivity.kt` + nowy) · `tool/fingerprint.dart` (nowy)
· `README.md` · testy i wektory w `test/backup/` (`qa`).
`grobing-vault`: ta pozycja · `TRACEABILITY.md` · przy zamknięciu (`docs`): ISSUE-010, specyfikacja
formatu, ADR-004.

### AC → tests (`qa`)
| AC | Test happy-path | Ręcznie (stop #2) |
|---|---|---|
| AC-1 konfiguracja, „Zrób kopię teraz", czas kopii | na hoście: wymyślone dane → kopia do pliku lokalnego → odszyfrowanie własnym modułem → w tar `grobing.db`, `media/…`, `manifest.json`; SHA-256 i rozmiary = manifest; `integrity_check` = `ok`; `data_fingerprint` = odcisk żywej bazy. Widget: „Stan danych" pokazuje „Ostatnia udana kopia" ze stanu kopii | konfiguracja do Dysku; czas po „Zrób kopię teraz"; plik w Dysku w przeglądarce |
| ~~AC-2~~ kopia w tle | → ISSUE-010 (D1) | — |
| AC-3 bramka zgodności | wektory C2SP (odszyfrowanie) + round-trip w `flutter test`. **`qa` na PC:** oficjalne CLI `age` — `age -d` (klucz), `age -d -i` (kopia) → `tar` → `integrity_check` → `tool/fingerprint.dart` = ekran | — (hasło testowe, nie autora) |
| AC-4 kopia Androida i D2D | test czyta `AndroidManifest.xml` i `data_extraction_rules.xml`: `allowBackup="false"`, oba bloki wykluczają wszystko. **`qa`:** M7 powtórzone na buildzie release (`bmgr`, D2D) | — |
| AC-5 bez sieci i sekretów | `no_cloud_sdk_test` · test: główny manifest bez `INTERNET`. **`qa`:** `aapt dump permissions` na APK release · przegląd `cryptography` i `pointycastle` (czysty Dart, bez sieci) | — |

**Pliki do bramki AC-3:** druga konfiguracja na emulatorze z zapisem do pamięci urządzenia (Pobrane),
potem `adb pull` do scratchpada — nigdy do repo. Plik w Dysku ogląda autor na stopie #2; że Dysk nie
zmienia bajtów, pokazał SPIKE-003 (M5).

### Manual verification (stop #2) — kroki według miejsca
- **Terminal VS Code** (`grobing-code`): `flutter run` na `Medium_Phone` (debug, bo potrzebne są wymyślone
  dane).
- **Emulator `Medium_Phone`:**
  1. „Stan danych" → „Wgraj wymyślone dane".
  2. „Skonfiguruj kopię": czy tekst o haśle i pliku klucza jest jasny? Hasło **testowe** (nie Twoje
     prawdziwe) dwa razy, potem ~15 s czekania.
  3. Zapisz plik klucza w Dysku, potem plik kopii w tym samym folderze.
  4. Po powrocie na „Stan danych" „Ostatnia udana kopia" ma bieżącą godzinę.
  5. „Wgraj wymyślone dane" jeszcze raz → „Zrób kopię teraz" → godzina się zmienia.
- **Przeglądarka na PC:** drive.google.com → dwa pliki. Kopia ma świeżą godzinę modyfikacji, a jej treści
  nie da się odczytać.
- **Emulator, build release (instaluje `qa`):** sekcja „Kopia" jest, przycisku „Wgraj wymyślone dane" nie ma.
- **Napisz tutaj:** „ok" · „pomiń" · opis błędu.

### Closing checklist (docs)
- Założyć **ISSUE-010 — kopia w tle** (D1): pkt 3 i AC-2 tej pozycji. Niewiadome: Dart w tle (`workmanager`
  0.10.10 działa z przypiętym Flutterem, *Prior art*), kanał do Dysku w silniku bez Activity, dwa
  połączenia z bazą naraz. Decyzja: kiedy kopia się uruchamia. Zależy od ISSUE-008. Wpisy w US-001 →
  *Issues* i w `TRACEABILITY.md`.
- `04_ARCHITECTURE/backup-format.md`: format v1 (D2) i jak otworzyć kopię bez Grobing. Będzie do niego
  linkować [[NT-007-hand-over-note]]. ADR-004 → *Follow-ups*: datowana linia z linkiem.
- *Dependencies* tej pozycji: wiersz ISSUE-007 ma `ready`, a pozycja jest `done` (zastane; jak wiersz
  ISSUE-002 w EPIC-001 przy SPIKE-003).
- [[NFR-005-dane-nie-opuszczaja-telefonu]] → *Notes* i `CURRENT_STATE.md`: kanał kopii Androida zamknięty
  w kodzie (zdjąć ⚠️ o `allowBackup=true`).
- Bez pusha do zamknięcia [[NT-008-publication-review]].

### Out of Scope (this plan)
- Kopia w tle → ISSUE-010 (D1).
- Odtworzenie w aplikacji i walidacja przy odtwarzaniu → [[ISSUE-009-restore]]. Moduł `age` umie już
  odszyfrować, ale to tylko fundament.
- Zmiana hasła · zmiana pliku kopii bez nowego klucza · pokazywanie klucza prywatnego w aplikacji. Do notki
  przekazania wystarczy `age -d` pliku klucza na PC ([[NT-007-hand-over-note]]).
- `cryptography_flutter`: dopiero gdy pomiar pokaże potrzebę (czysty Dart ~8 MB/s, M4).
- Eksport, powiadomienia, zmniejszanie zdjęć.

### Self-check (planning) — said out loud
- Każda kopia potrzebuje chwilowo ~2× rozmiaru danych w cache (migawka + plik zaszyfrowany). Brak miejsca
  kończy się widocznym błędem, bez sprawdzania z góry. Sprawdzenie z góry jest potrzebne przy odtworzeniu
  (ISSUE-009).
- Migawka bazy i odczyt zdjęć to nie jedna transakcja. Dziś zdjęcia dodaje tylko przycisk debug, ale przy
  [[US-005-zdjecia]] usunięcie zdjęcia w trakcie kopii zostawi wpis bez pliku. Do zapisania przy US-005.
- `backup.json` leży obok bazy, więc ISSUE-009 musi zdecydować, czy odtworzenie go zachowuje.
- Scrypt z work factor 18 sprawdza tylko konfiguracja na emulatorze i bramka CLI; wektory C2SP mają niski
  koszt.
- Nie wiem, czy `tool/fingerprint.dart` ruszy przez `dart run` z dołączonym SQLite na Windows. Jeśli nie,
  `dev` robi to samo jako test uruchamiany ręcznie — ważne, żeby liczył tą samą funkcją co ekran.

## Dev report
> `dev`, 2026-10-06. **Stop #1:** autor „tak” dla planu z podziałem (D1), D2 i D3 (2026-10-06). Kod w
> `grobing-code`, niezacommitowany. Flutter 3.41.1 (przypięty). `flutter analyze lib tool` bez uwag.

### Step 1 — falsifier (age module): ✅ passed on the first run
Skrypt próbny w scratchpadzie (`flutter test` na pliku spoza repo), moduł `lib/backup/age/`:
- **Wektory C2SP/CCTV, commit `50a8ecf2a220f4c8bdc4f085789b8e85c26829e7`: 92 / 92 zgodne z `expect`**, a
  dla wektorów z `payload` także SHA-256 odszyfrowanej treści (również tej wydanej przed błędem). To
  wszystkie wektory poza `armor_*` i `hybrid_*`: 15 × success · 51 × header failure · 18 × payload failure ·
  7 × no match · 1 × HMAC failure. Wśród nich `stream_last_chunk_empty` — dokładnie ten błąd `dage`, który
  robił kopie nie do odtworzenia.
- Round-trip X25519: 0 B, 1 B, 65 535, 65 536, 65 537, 131 072, 131 073, 200 000 B, wejście podawane
  kawałkami po 1000 B. Scrypt z hasłem z polskimi znakami + plik tożsamości (`encodeIdentityFile` →
  `parseIdentityFile`); złe hasło → *no match*; jeden zmieniony bit → *payload failure*.
- Przykład ze specyfikacji: `AGE-SECRET-KEY-1GFPYY…` daje `age1zvkyg2lq…` (X25519 + Bech32).

### Smoke checks (dev)
- **Cała ścieżka na hoście** (Windows, wymyślone dane, dwie partie): migawka → kopia (~70 KB, 99 ms) →
  odszyfrowanie → **systemowy `tar` z Windows czyta archiwum** (`grobing.db`, `media/…`, `manifest.json`
  na końcu) → `dart run tool/fingerprint.dart`: `integrity_check ok`, odcisk, liczby, rozmiary i SHA-256
  zgodne z manifestem. **`dart run` z dołączonym SQLite działa** (pierwsze pytanie z *Self-check*).
- **Emulator `Medium_Phone`, build debug**, zapis do Pobranych emulatora (nie Dysk):
  - konfiguracja: hasło testowe → okno zapisu klucza po **42 s** (debug, niezoptymalizowany Dart; spike
    zmierzył ~14 s w release) → okno zapisu kopii → pierwsza kopia → „Ostatnia udana kopia" z godziną;
  - plik klucza: `age` scrypt, work factor 18; po `adb pull` otwarty własnym modułem hasłem, kopia jego
    kluczem → **odcisk `cac13dcd1f3fb213` = ekran**, manifest zgodny;
  - „Zrób kopię teraz" po nowych danych i po restarcie aplikacji: plik nadpisany (zachowane uprawnienie,
    bez okna); katalog roboczy w cache pusty po kopii; `backup.json` = klucz publiczny, URI, czasy — bez
    sekretu.
- **APK release** (`aapt`): uprawnień `INTERNET` brak (jedyne: `DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION`
  z AndroidX), `allowBackup=false`, `dataExtractionRules` podpięte.

### Deviations from the plan
- **`DataLocation.appDefault()` → `DataLocation.inDirectory()`**, a `path_provider` przeniesione do
  `main.dart`. Inaczej `tool/fingerprint.dart` nie uruchomi się przez `dart run` (`path_provider` ciągnie
  Fluttera).
- **`listMediaFiles` i `mediaRelativePath` w `data_state.dart` stały się publiczne**, żeby archiwum
  zawierało dokładnie te pliki, które liczy odcisk. Definicja odcisku bez zmian.
- **Pliki:** `backup_service.dart` (konfiguracja i kopia; w planie `backup_setup.dart`),
  `backup_settings.dart` (stan kopii), `documents.dart` (kanał), `tar_writer.dart`; ekran
  `lib/app/backup_setup_screen.dart`; Kotlin `BackupDocuments.kt`.
- **+ „Skonfiguruj kopię od nowa"** (ten sam przepływ, nowy klucz, z ostrzeżeniem o notce przekazania).
  To jedyne wyjście, gdy aplikacja straci dostęp do pliku kopii (komunikat błędu tak mówi). **Do
  potwierdzenia przez autora na stopie #2.**
- **+ `tool/fingerprint.dart` sprawdza też manifest** (rozmiary, SHA-256, liczby, odcisk): bramka AC-3
  to jedno polecenie.
- `cryptography` 2.9.0 i `pointycastle` **4.0.0** (spike: 3.9.1), przypięte dokładnie (komentarz w
  `pubspec.yaml`).
- `ScryptIdentity` odrzuca work factor > 22, jak oficjalne CLI (wektor `scrypt_work_factor_23`).

### For qa
- **Dwa testy się nie kompilują:** `test/app_start_test.dart` i `test/app/data_state_screen_test.dart`
  (wymagany parametr `backup`). Potrzebny `BackupService` z bazą w pamięci, katalogami tymczasowymi i
  sztucznym `DocumentStore` (interfejs w `lib/backup/documents.dart`).
- **Wektory C2SP:** commit wyżej. Pliki nie mają rozszerzenia, więc ani `.gitignore`, ani strażnik ich
  nie blokują. Harness próbny: scratchpad sesji, `probe008/age_probe_test.dart`.
- **Bramka AC-3:** pliki z emulatora przez `adb pull` (Pobrane), oficjalne CLI `age`, potem
  `tool/fingerprint.dart`. Zrób własną konfigurację, bez moich plików próbnych.
- **Stop #2:** w buildzie debug konfiguracja czeka ~40 s, nie ~15 s — popraw krok 2 kroków ręcznych.
- **Stan emulatora:** `Medium_Phone` działa z `-no-snapshot-save` (po zamknięciu zmiany znikną).
  Zainstalowany build debug z konfiguracją do Pobranych. W Pobranych leżą też pliki ze SPIKE-003
  (`grobing-kopia.age` 157 MB, `grobing-klucz.age`, 2026-10-05; wymyślone dane, zaszyfrowane) i dwa moje
  `(1)`. `com.grobing.spike003` nadal zainstalowane (snapshot, jak przy ISSUE-007).
- Tekst „Zapisana w Dysku na telefonie" stoi także wtedy, gdy plik jest gdzie indziej (smoke check:
  Pobrane). Konfiguracja każe wybrać Dysk.
- **Dla ISSUE-009:** `ScryptIdentity(maxWorkFactor: …)` — przy odtwarzaniu w telefonie warto przekazać
  niższy limit (22 to ~4 GB pamięci).

## Verification
> `qa`, 2026-10-06. Dowody sprawdzone **niezależnie od deklaracji `dev`**: powtórzone albo zmierzone na
> nowo, z własną konfiguracją na emulatorze i oficjalnym CLI, którego `dev` nie użył.

### Automated (`flutter test`: 147 passed · `flutter analyze`: no issues · `dart format`: clean)
| AC | Test | Wynik |
|---|---|---|
| AC-1 zawartość kopii | `test/backup/backup_archive_test.dart`: wymyślone dane → `VACUUM INTO` → kopia → odszyfrowanie → własny czytnik ustar: kolejność `grobing.db`, `media/…`, `manifest.json` na końcu; sumy kontrolne nagłówków, tryb 0644; rozmiary i SHA-256 = manifest; `integrity_check` `ok`; `data_fingerprint` = odcisk żywej bazy; pusta baza też; ścieżka > 100 znaków dzielona na prefiks; ścieżki spoza bezpiecznego zbioru (`..`, `/`, polskie znaki, spacja, `\`) odrzucane | ✅ |
| AC-1 konfiguracja i „Zrób kopię teraz" | `test/backup/backup_service_test.dart` (sztuczne okno zapisu i Dysk): kroki w kolejności; plik klucza = `age` scrypt, otwierany hasłem, jego klucz publiczny = zapisany; kopia otwierana tym kluczem ma odcisk żywej bazy; `backup.json` bez hasła i bez `AGE-SECRET-KEY`; uprawnienie trwałe tylko do pliku kopii; katalog roboczy usunięty. Zamknięcie okna klucza albo kopii → nic nie skonfigurowane. Ponowna kopia nadpisuje plik i zapisuje czas; błąd zapisu i utrata dostępu → zapisana porażka, ostatni sukces zostaje; kopia bez konfiguracji → odmowa | ✅ |
| AC-1 ekran | `test/app/data_state_screen_test.dart`: bez kopii — „Skonfiguruj kopię"; z kopią — „Ostatnia udana kopia" z datą, uczciwa notka, ostatnia porażka, oba przyciski | ✅ |
| AC-3 (odszyfrowanie) | `test/backup/age_testkit_test.dart`: **92 oficjalne wektory C2SP** (commit w `age_testkit/README.md`), wynik + SHA-256 treści | ✅ 92/92 |
| AC-3 (szyfrowanie) | `test/backup/age_test.dart`: round-trip 8 rozmiarów na granicach 64 KiB; n × 64 KiB kończy się pełnym kawałkiem końcowym (rozmiar pliku); przykład klucza ze specyfikacji; plik tożsamości w formacie `age-keygen`; domyślny work factor 18; hasło z polskimi znakami; złe hasło, zmieniony bit, ucięcie na granicy kawałka; scrypt nie miesza się z innymi odbiorcami | ✅ |
| AC-4 | `test/repo_invariants_test.dart`: `allowBackup="false"`, `dataExtractionRules`; oba bloki wykluczają wszystkie 9 domen, żadnego `<include>` | ✅ |
| AC-5 | `test/repo_invariants_test.dart`: główny manifest bez `INTERNET`; `no_cloud_sdk_test` | ✅ |
| (dostosowane) | `app_start_test`, `data_state_screen_test` — nowy parametr `backup` | ✅ |

`test/backup/age_testkit/` ma `.gitattributes` (`-text`): `core.autocrlf=true` zamieniłby LF na CRLF w
wektorach bez bajtów zerowych i je zepsuł.

### Compatibility gate (AC-3) — official CLI `age` v1.3.2, on the PC
- **Pliki z emulatora** (`qa`, własna konfiguracja przez „Skonfiguruj kopię od nowa", build debug,
  zapis do Pobranych, hasło testowe, `adb pull` do scratchpada):
  - plik klucza → oficjalne `age -d` (scrypt przez `age-plugin-batchpass` z tej samej dystrybucji, bo
    sesja nie ma terminala do wpisania hasła) → `# created`, `# public key`, jeden `AGE-SECRET-KEY-1`; złe
    hasło → *incorrect passphrase*;
  - kopia → `age -d -i klucz.txt` → `tar` (Windows) → `grobing.db`, 2 pliki `media/`, `manifest.json`;
  - **niezależnie od naszego kodu** (Python `sqlite3` + `hashlib`): `integrity_check` `ok`, `user_version`
    1 = manifest, liczby rekordów = manifest, rozmiary i SHA-256 wszystkich 3 plików = manifest;
  - `tool/fingerprint.dart`: **odcisk `ff6d4202e5b6c0a2` = ekran „Stan danych"** na emulatorze; wszystkie
    sprawdzenia OK.
- **Macierz w obie strony na hoście:** nasz moduł → CLI: X25519 dla 0, 1, 65 535, **65 536**, 65 537,
  **131 072**, 131 073, 200 000 B — 8 × PASS; scrypt (work factor 18) z hasłem ASCII i z polskimi znakami
  — PASS. CLI → nasz moduł: te same 8 rozmiarów i oba hasła — PASS.

### AC-4 — Android backup, repeated like M7 (release build on `Medium_Phone`)
Transport lokalny (`bmgr`), potem ustawienia emulatora przywrócone (transport GMS, Backup Manager
wyłączony):
- kopia w chmurze (`is_encrypted=true`): `com.grobing.app` → **„Backup is not allowed"**;
- D2D (`is_device_transfer=true`): `com.grobing.app` → **„Transport rejected package"**;
- kontrola pozytywna, ten sam transport D2D: `com.android.providers.settings` → *Success*.

### AC-5 — no network, no secrets
- `aapt dump permissions` (APK release, przebudowany po `dart format`): tylko
  `DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION` (AndroidX), **bez `INTERNET`**.
- Nowe paczki: `cryptography` 2.9.0 (zależności: collection, crypto, ffi, meta, typed_data) i
  `pointycastle` 4.0.0 (collection, convert) — wszystkie już były w `pubspec.lock`. W `lib/` obu paczek
  brak `HttpClient`, `package:http`, gniazd i `dart:html`. Kod kopii niczego nie loguje.
- Kluczy API i sekretów OAuth brak; `key.properties` nieczytany.

### DoD lines specific to Grobing
- **Próbne odtworzenie z kopii:** oficjalnym CLI na PC (bramka wyżej), jak zakłada plan; odtworzenie w
  aplikacji to ISSUE-009.
- **Test migracji:** n/a — schemat się nie zmienił (`schemaVersion` 1, stan kopii poza bazą).
- **Źródło faktu:** n/a — pozycja nie zapisuje faktów o rodzinie.
- **Dane rodziny w zmianach:** brak. W 3 repo nie ma `*.db`, `*.age`, `*.tar`, eksportów ani zdjęć.
  W testach tylko wymyślone osoby z `lib/dev/fictional_data.dart` („Wymyślona"). `test/backup/age_testkit/` to
  **publiczne wektory testowe** w formacie `age` (bez rozszerzenia, więc strażnik ich nie blokuje). Nie
  ma w nich niczego o rodzinie. Odszyfrowane pliki z bramki leżą tylko w scratchpadzie sesji.

### Manual (stop #2)
- Kroki 1-5 (emulator, build release) i sprawdzenie w przeglądarce: **„pomiń"**. Autor najpierw napisał
  „ok”, ale emulator po tej odpowiedzi pokazywał „Kopia nie jest skonfigurowana” i odcisk pustej bazy, a
  innego urządzenia nie było podłączonego. `qa` zgłosił rozjazd i zaproponował konfigurację przez `adb` z
  potwierdzeniem w przeglądarce. Autor wybrał „pomiń” (2026-10-06). Zapisane jako pominięte, **nie** jako
  „ok”.
- **Co to znaczy dla dowodu:** zapis do **Dysku Google kodem produkcyjnym nie był wykonany**. Kanał
  natywny (okno zapisu, trwałe uprawnienie, `"wt"`, zapis bez okna po restarcie) działał z dostawcą
  Pobranych emulatora (`dev`, `qa`). Z Dyskiem działał tylko kod spike'a (SPIKE-003, M2-M3). Nikt nie
  obejrzał też tekstów ekranu konfiguracji.
- **Decyzja autora:** dodatek `dev` „Skonfiguruj kopię od nowa” zostaje (zgoda z góry przy „ok”,
  potwierdzona przy „pomiń”).

### Verdict (self-check)
**APPROVED** z uwagami. Każde AC po podziale D1 ma test happy-path (AC-2 przeszło do ISSUE-010).
Bramka zgodności przeszła na plikach z emulatora, M7 powtórzone, APK release bez `INTERNET`.

**Czego szukałem i nie znalazłem:**
- niezgodności z oficjalnym `age` w którąkolwiek stronę, także na granicach 64 KiB i przy polskim haśle;
- rozjazdu odcisku między emulatorem a PC;
- sekretu w telefonie (`backup.json`: klucz publiczny, URI, czasy) i migawki bazy po kopii (cache pusty);
- uprawnienia `INTERNET` i kodu sieciowego w nowych paczkach;
- danych rodziny w zmianach trzech repo.

**Uwagi, które nie blokują:**
1. **Dysk z kodem produkcyjnym niesprawdzony** (stop #2 pominięty). Pierwsza okazja: konfiguracja do Dysku
   na emulatorze w [[ISSUE-009-restore]] — odtworzenie i tak czyta plik z Dysku. **Warto jej tam nie
   pomijać**: to drugi pominięty stop #2 w US-001 po SPIKE-003.
2. Plik klucza otworzyło oficjalne CLI przez `age-plugin-batchpass` (ten sam kod scrypt, hasło ze zmiennej
   środowiskowej), a nie przez interaktywne `age -d -i grobing-klucz.age` z README. Ścieżki z
   terminalem nikt nie wykonał.
3. Tekst „Zapisana w Dysku na telefonie” stoi także przy pliku zapisanym gdzie indziej (`dev`, *For qa*).
4. W buildzie debug konfiguracja trwa ~40 s (scrypt w niezoptymalizowanym Darcie). W release spike
   zmierzył ~14 s; tu release niezmierzony, bo konfiguracja w release nie powstała.

## Closure
`docs`, 2026-10-06. Commity: `grobing-code` e28aabf (kod + testy) · `grobing-vault` a3863f0 (plan, raport
dev, weryfikacja) + commit zamknięcia.

**Checklista zamknięcia (z planu):**
- ✅ [[ISSUE-010-background-backup]] założone: pkt 3 i AC-2 tej pozycji, trzy niewiadome, nowa zależność
  do przeglądu. W [[US-001-kopia-z-odtworzeniem]] jako czwarte, po [[ISSUE-009-restore]].
- ✅ `04_ARCHITECTURE/backup-format.md`: format v1 (D2) i otwarcie kopii bez Grobing; do niego ma linkować
  [[NT-007-hand-over-note]]. [[ADR-004-backup-format-encryption-destination]] → *Follow-ups*: datowane linie.
- ✅ *Dependencies* tej pozycji: wiersz ISSUE-007 poprawiony na `done`.
- ✅ [[NFR-005-dane-nie-opuszczaja-telefonu]] → *Notes* i `CURRENT_STATE.md`: kanał kopii Androida
  zamknięty w kodzie, ⚠️ o `allowBackup=true` zdjęte.
- ✅ Bez pusha: [[NT-008-publication-review]] otwarte.

**Uwagi z werdyktu — gdzie trafiły:**
- Dysk z kodem produkcyjnym niesprawdzony (stop #2 pominięty) → [[ISSUE-009-restore]] → *Technical Notes*
  i `CURRENT_STATE.md`.
- Limit work factor przy odtwarzaniu w telefonie i los `backup.json` przy odtworzeniu → ISSUE-009 →
  *Technical Notes*.
- Migawka bazy a zdjęcia (nie jedna transakcja) → [[US-005-zdjecia]] → *Notes* i `backup-format.md` →
  *Known limits*.
- `tool/fingerprint.dart` jako metoda na PC → [[NFR-002-odtworzenie-na-nowym-telefonie]] → *Notes*.

**Poza checklistą:** [[NT-007-hand-over-note]] → *Input from ISSUE-008*: nazwy plików, link do
`backup-format.md`, wyjęcie klucza prywatnego na PC oraz to, że ponowna konfiguracja unieważnia notkę.

**INVEST / DoD ISSUE:** jeden komponent (kopia: zapis), po podziale D1 w rozmiarze ISSUE. Test happy-path
dla każdego AC (147 testów). Ręczna weryfikacja: „pomiń”, zapisana z tym, czego przez to nie sprawdzono.
Próbne odtworzenie: oficjalnym CLI na PC, odcisk zgodny z ekranem. Test migracji i źródło faktu: n/a
(*Verification*). README `grobing-code` → *Kopia*. Folder nie powstał, więc DOC_MAP bez nowego wiersza (w
wierszu `04_ARCHITECTURE/` dopisany plik formatu). Zero danych rodziny.
