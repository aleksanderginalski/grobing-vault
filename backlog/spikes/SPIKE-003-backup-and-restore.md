---
title: "SPIKE-003 — Encrypted backup to the author's cloud via the system picker, and a real restore"
type: spike
status: in-progress
priority: MUST
time-box: "1 day"
precedes: "mass transcription (NT-002) — backup + restore must exist first (MD2)"
quality-verdict: APPROVED
verdict-date: 2026-10-05
verdict-reviewer: self-check
created: 2026-10-05
updated: 2026-10-05
---

# SPIKE-003 — Backup + restore (S-BACKUP)

## The question
**Czy aplikacja może automatycznie zapisywać kopię zaszyfrowaną w telefonie (hasłem) do folderu w
chmurze autora, wskazanego w systemowym oknie wyboru — bez kluczy API i sekretów OAuth w aplikacji — i
czy z tej kopii da się naprawdę odtworzyć wszystko na drugim urządzeniu?**

## Why it matters
§Security: kopia (zaszyfrowana, automatyczna, sprawdzona odtworzeniem) i eksport (czytelny, u rodziny)
to dwie różne rzeczy. Od pierwszej przepisanej osoby telefon jest **jedyną** cyfrową kopią — więc ten
spike poprzedza masowe przepisywanie.

## Steps
1. Zapis pliku do folderu z chmury wybranego w systemowym oknie; trwałe uprawnienie do zapisu w tle.
2. Szyfrowanie po stronie telefonu (hasło → klucz); gdzie trzymać klucz do kopii automatycznej
   (kandydat: bezpieczny magazyn, sprawdzony we wcześniejszej aplikacji autora).
3. **Androidowa automatyczna kopia (`allowBackup`)** — decyzja świadoma: limit 25 MB na aplikację
   oznacza **cicho niepełną** kopię ze zdjęciami.
4. Odtworzenie na emulatorze/drugim urządzeniu z wymyślonymi danymi; walidacja pliku przed nadpisaniem
   czegokolwiek (floor: walidacja wejścia na granicy).

## Exit criterion
**ADR-004** (format, szyfrowanie, miejsce, `allowBackup`) `accepted`; albo „okno systemowe nie wystarcza"
→ decyzja autora o alternatywie.

## Definition of Done
- [ ] Odpowiedź zapisana · kod eksperymentu usunięty · **odtworzenie wykonane naprawdę**, nie tylko
      zaprojektowane.

## Implementation plan
> `planning`, 2026-10-05. **DoR (SPIKE):** pytanie ✓ · limit czasu ✓ (1 dzień) · warunek wyjścia ✓.
> Spike dotyka warstwy danych, ale **niczego nie zapisuje w `grobing-code`**: test migracji i próbne
> odtworzenie są tu samym przedmiotem pomiaru (kroki 4-5), a źródło faktów nie ma zastosowania, bo dane
> są wymyślone. Testów automatycznych nie ma, bo kod nie zostaje (DoD SPIKE). Dowodem są pomiary i
> odtworzenie wykonane naprawdę.

### Prior art (źródła, nie pamięć)
- **Okno wyboru folderu (`ACTION_OPEN_DOCUMENT_TREE`) a chmura:** *„few cloud storage providers seem to
  support `ACTION_OPEN_DOCUMENT_TREE`"* ([CommonsWare, Scoped Storage Stories: Trees](https://commonsware.com/blog/2019/11/09/scoped-storage-stories-trees.html)).
  Dostawca musi mieć `FLAG_SUPPORTS_IS_CHILD` ([Create a custom document provider](https://developer.android.com/guide/topics/providers/create-document-provider)).
  **Hipoteza:** Dysk Google nie pojawi się w oknie wyboru *folderu*. Zostaje okno wyboru *pliku*
  (`ACTION_CREATE_DOCUMENT` / `ACTION_OPEN_DOCUMENT`) z trwałym uprawnieniem, czyli wzorzec KeePassDX:
  zaszyfrowany plik w Dysku przez systemowe okno, bez integracji z API chmury
  ([KeePassDX #342](https://github.com/Kunzisoft/KeePassDX/issues/342)).
- **`allowBackup` na Androidzie 12+:** *„specifying `android:allowBackup="false"` does disable backups
  to Google Drive, but doesn't disable D2D transfers for the app"*. Reguły transferu między urządzeniami
  trzeba podać osobno w `dataExtractionRules` → `<device-transfer>`
  ([Behavior changes: Android 12](https://developer.android.com/about/versions/12/behavior-changes-12)).
- **`flutter_secure_storage`** (Friendsheet: `^9.2.2`, opcje domyślne, bez konfiguracji `allowBackup`):
  README każe ustawić `android:allowBackup="false"`, bo kopia Androida odtwarza zaszyfrowane wartości
  bez klucza z Keystore → `InvalidKeyException: Failed to unwrap key`. Aktualna wersja to 11.x, min. SDK 23
  ([pub.dev](https://pub.dev/packages/flutter_secure_storage)).
- **Format zaszyfrowanego pliku:** standard [age](https://age-encryption.org) (hasło → scrypt, strumień
  ChaCha20-Poly1305 w kawałkach 64 KiB, więc duże archiwa nie muszą mieścić się w pamięci). Ma czyste
  implementacje w Dart: [`dartage`](https://pub.dev/packages/dartage) (0.2.0, strumieniowe) i
  [`dage`](https://pub.dev/packages/dage). Alternatywa to dojrzała biblioteka
  [`cryptography`](https://pub.dev/packages/cryptography) (2.9.0: Argon2id, AES-GCM, ChaCha20-Poly1305),
  ale z własnym formatem koperty.

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego / czego to nie da |
|---|---|---|---|
| D1 | **Która chmura** (brief mówi tylko „own cloud drive") | **Dysk Google**: konto Google i tak jest na każdym Androidzie, a aplikacja Dysku jest dostępna na emulatorze (obraz `google_apis_playstore`, sprawdzone) | Inny dostawca (OneDrive, Dropbox) = inny `DocumentsProvider`, więc pomiar kroku 1 trzeba powtórzyć dla niego. **Konto na emulatorze loguje autor sam**, żeby dane logowania nie przeszły przez sesję |
| D2 | **Format do sprawdzenia najpierw** | **`age` (hasło/scrypt) przez `dartage`**, sprawdzone interoperacyjnością z oficjalnym CLI `age` na PC. Fallback: `cryptography` (Argon2id + AES-GCM w kawałkach) z własnym, wersjonowanym nagłówkiem | `age` to standard ze specyfikacją: kopię da się odszyfrować **bez aplikacji**, gdy aplikacji już nie będzie (brief §2, „trwalsza niż aplikacja"). **Koszt:** młoda paczka Dart w roli kryptografii. Obala ją test interoperacyjności (krok 2), a jeśli nie przejdzie, przechodzimy na fallback |
| D3 | **Gdzie żyje eksperyment** | Osobny, jednorazowy projekt `{code}/../_throwaway/spike-003/` (poza trzema repo), `applicationId` `com.grobing.spike003` | Nie dotyka `grobing-code` ani zainstalowanego `com.grobing.app`; „kod eksperymentu usunięty” = usunięcie folderu. Zależności eksperymentu nie trafiają do `pubspec.lock` aplikacji |

### Scope diff vs the item (to accept at stop #1)
- **+ ⚠️ OPEN z [[ADR-004-backup-format-encryption-destination]] / [[NFR-003-migracje-schematu]]
  wchodzi w zakres:** kopia ze starszej wersji schematu odtwarza się w nowszej (krok 5). Format kopii i
  tak powstaje tutaj, a później zmiana kosztowałaby migrację wszystkich istniejących kopii.
- **+ `dataExtractionRules`** obok `allowBackup` (prior art: Android 12+). Bez tego decyzja o kopii
  Androida byłaby tylko pozorna.
- **+ drugi wirtualny telefon** (`Grobing_Restore`, ten sam obraz) jako „drugie urządzenie”. **Zostaje po
  spike'u** jako stałe narzędzie do próbnych odtworzeń (DoD ISSUE: każda pozycja z warstwą danych).
- **+ pomiar bez uprawnienia `INTERNET`:** czy kopia trafia do Dysku, gdy aplikacja w ogóle nie ma
  dostępu do sieci (wysyła aplikacja Dysku). Jeśli tak, [[NFR-005-dane-nie-opuszczaja-telefonu]] dostaje
  mocną własność: aplikacja sama nie może niczego wysłać. Mapy (SPIKE-001) mogą ją później zmienić.
- **+ sekcja *Findings* w tej pozycji.** Jej pisarzem jest `dev`, bo pomiary są produktem spike'a (tak
  jak kod w ISSUE). Tabela własności w `vault-as-sot.md` nie obejmuje wyników spike'a, więc **dopisanie
  wiersza to punkt dla `docs`**.
- **− Out of scope:** produkcyjna funkcja kopii (ekran, harmonogram okresowy, powiadomienia), eksport
  HTML + PDF (A4 w ADR-004), wybór paczki SQLite dla aplikacji, rozdzielczość zdjęć w aplikacji, treść
  notki przekazania z hasłem ([[NT-007-hand-over-note]]).

### Steps (dev) — w kolejności falsyfikatora, z limitem czasu
**Przed krokiem 1 (autor, emulator):** zaloguj konto Google na `Medium_Phone` i na nowym
`Grobing_Restore` (tworzy go dev przez `avdmanager`). Zaktualizuj Dysk Google ze Sklepu Play i utwórz w
Dysku folder `Grobing-spike`.

1. **Miejsce zapisu (falsyfikator, ≤ 2 h).** Minimalny kanał natywny w Kotlinie (bez paczki pośredniej):
   - `ACTION_OPEN_DOCUMENT_TREE`: czy Dysk jest na liście (**M1**);
   - `ACTION_CREATE_DOCUMENT` → plik w `Grobing-spike` → `takePersistableUriPermission` (odczyt + zapis);
   - nadpisanie tego samego pliku: po zimnym starcie, po restarcie emulatora i z jednorazowego zadania
     WorkManager przy zamkniętej aplikacji (**M2**). Tryb zapisu `"wt"` i sprawdzenie, że krótszy zapis
     obcina plik;
   - całość w buildzie release **bez** `INTERNET` (**M3**).

   **Bramka:** jeśli trwały zapis do Dysku nie działa w żadnym trybie, to **STOP**: „okno systemowe nie
   wystarcza” (warunek wyjścia) → decyzja autora o alternatywie. Dalszych kroków wtedy nie robimy.
2. **Szyfrowanie (≤ 2 h).** Archiwum (snapshot SQLite przez `VACUUM INTO` + katalog zdjęć + `manifest.json`)
   szyfrowane strumieniowo formatem `age` z hasłem testowym (D2). Pomiary (**M4**): czas KDF na emulatorze;
   czas i szczytowa pamięć dla ~150 MB syntetycznych zdjęć (szum JPEG, czyli rozmiar realny, bez
   kompresji). **Interoperacyjność (M5):** plik z emulatora otwiera się oficjalnym CLI `age` na PC
   (pobranym do scratchpada) i odwrotnie. **Klucz do kopii automatycznej:** porównaj dwa warianty:
   (a) hasło w `flutter_secure_storage`; (b) klucz publiczny `age` (X25519) w aplikacji, tak że kopia w tle
   **nie potrzebuje sekretu**, a tożsamość chroniona hasłem leży osobno. Zapisz wybór z uzasadnieniem.
3. **Kopia Androida (≤ 0,5 h).** `allowBackup="false"` + `dataExtractionRules` wykluczające wszystko z
   `<cloud-backup>` i `<device-transfer>`. Rekomendacja: **jedna droga na nowy telefon, czyli nasza
   sprawdzona kopia**. Dowód (**M7**): `adb shell bmgr backupnow com.grobing.spike003` nie przenosi danych.
4. **Odtworzenie na drugim urządzeniu (≤ 2,5 h).** Na `Grobing_Restore`: `ACTION_OPEN_DOCUMENT` → plik z
   Dysku → hasło. Walidacja **zanim cokolwiek zostanie nadpisane**:
   - odszyfrowanie do katalogu tymczasowego;
   - sumy SHA-256 z manifestu;
   - `PRAGMA integrity_check`;
   - wersja formatu i schematu;
   - liczby rekordów zgodne z manifestem.

   Dopiero wtedy następuje podmiana katalogu (rename), a poprzednie dane zostają do sukcesu. Przypadki
   negatywne (**M6**): złe hasło · plik ucięty · plik z obcym bajtem · kopia z nowszej wersji schematu →
   odmowa, **nic nie nadpisane**.
5. **Kopia sprzed migracji (≤ 0,5 h).** Kopia zrobiona w schemacie v1 (wymyślone osoby) → odtworzenie w
   buildzie ze schematem v2 (`user_version` 2, dodana kolumna) → zwykła migracja przy otwarciu → dane
   kompletne (**M6**). To zamyka ⚠️ OPEN.
6. **Findings + sprzątanie.** Tabela M1-M7 z wynikami i rekomendacją do ADR-004. Usuwane:
   `_throwaway/spike-003/`, CLI `age` ze scratchpada, plik testowy i folder `Grobing-spike` w Dysku (to
   ostatnie robi autor). `Grobing_Restore` zostaje.

**Limit czasu:** po ~4 h bez zamkniętych kroków 1-2 → stop i raport, nie dociąganie na siłę.
**Dane:** wyłącznie wymyślone osoby, np. „Jan Testowy”, „Zofia Żółć-Próbna” (znaki polskie testują
kodowanie) i syntetyczne zdjęcia. Prawdziwych zdjęć z galerii nie używamy.

### Exit → evidence
| Warunek | Dowód |
|---|---|
| Miejsce: okno systemowe + trwały zapis w tle | M1-M3 w *Findings* |
| Szyfrowanie: format, KDF, klucz do kopii automatycznej | M4-M5 + wybrany wariant (a/b) z uzasadnieniem |
| `allowBackup` świadomie | manifest + `dataExtractionRules` w *Findings*, M7 |
| **Odtworzenie naprawdę** | M6 na `Grobing_Restore`: liczby i sumy zgodne; przypadki negatywne odrzucone bez nadpisania |
| ⚠️ OPEN migracja kopii | krok 5 |

### Manual verification (stop #2, po polsku, według miejsca)
- **Emulator `Medium_Phone`:**
  1. W aplikacji spike'a „Wybierz folder”: czy na liście jest Dysk Google?
  2. „Utwórz plik kopii” → Dysk → `Grobing-spike`. Wpisz **testowe** hasło (nie swoje prawdziwe).
  3. „Dane testowe” → „Zrób kopię”: widać rozmiar i czas.
  4. Zamknij aplikację (przesuń z ostatnich). Dev uruchamia kopię w tle.
- **Przeglądarka na PC:** drive.google.com → `Grobing-spike`. Plik ma nową godzinę modyfikacji, a jego
  treści nie da się odczytać.
- **Terminal VS Code:** dev odszyfrowuje plik oficjalnym `age`. Hasło wpisujesz Ty, w okno terminala,
  nie do czatu.
- **Emulator `Grobing_Restore`:**
  1. „Odtwórz” → plik z Dysku → hasło. Liczby osób, grobów i zdjęć są takie jak na `Medium_Phone`.
  2. Złe hasło daje komunikat, a dane testowe zostają nietknięte.
- **Napisz tutaj:** „ok” · „pomiń” · opis błędu.

### Closing checklist (docs)
- [[ADR-004-backup-format-encryption-destination]]: *Decision* z *Findings*, *Options considered* (≥3, także
  odrzucony wariant, np. folder vs plik), status `accepted`. Albo, gdy okno systemowe nie wystarcza:
  `proposed` + decyzja autora o alternatywie.
- [[NFR-003-migracje-schematu]] i ADR-004: zdjąć ⚠️ OPEN o kopii sprzed migracji (link do kroku 5).
- [[NFR-002-odtworzenie-na-nowym-telefonie]]: *Method*. Stałe urządzenie do odtworzeń to `Grobing_Restore`.
- [[EPIC-001-zabezpiecz-i-przepisz]] → *Dependencies*: wiersz ISSUE-002 nadal ma `ready`, choć pozycja
  jest `done` (zastane, zauważone przy planowaniu); wiersz SPIKE-003 po zamknięciu.
- `vault-as-sot.md` (repo agentów): wiersz własności dla *Findings* w spike'ach (pisarz: `dev`).
- Kod eksperymentu usunięty (`_throwaway/spike-003/`). Paczka na stop #3: **vault** (i ewentualnie
  agenci), **bez** `grobing-code`. Bez pusha do zamknięcia [[ISSUE-006-setup-family-data-guard]] i
  [[NT-008-publication-review]].

## Findings
> `dev`, 2026-10-05. Pomiary w jednorazowym projekcie `com.grobing.spike003` (build release, bez
> uprawnienia `INTERNET`), emulator `Medium_Phone` (Android 16, x86_64, obraz z Google Play), Flutter 3.41.1.
> Dane wyłącznie wymyślone: 100 osób, 40 rodzin, 50 grobów, 80 pochówków i pliki losowe udające zdjęcia
> (nieściśliwe jak JPEG). Ten sam generator na każdym urządzeniu daje ten sam **odcisk danych**
> (SHA-256 kolumn v1 i zdjęć), więc zgodność po odtworzeniu sprawdza się porównaniem jednej liczby.

### Odstępstwo od planu (D2) — biblioteka `age`
- **`dartage` odpada:** każda wersja (0.1.0–0.3.0) wymaga Darta ≥ 3.12, a przypięty Flutter 3.41.1 ma
  Darta 3.11. Globalnego SDK nie ruszamy (ADR-002).
- **`dage` 1.0.10 odpada** (ostatnie wydanie 2024-02). Test zgodności z oficjalnym CLI `age` v1.3.2
  dał **22 × FAIL**:
  - **hasło z polskimi znakami** nie działa w żadną stronę, bo `dage` koduje hasło jako UTF-16
    `codeUnits` zamiast UTF-8;
  - **plik o rozmiarze dokładnie n × 64 KiB** dostaje pusty ostatni kawałek. Takiego pliku nie otworzy
    oficjalne CLI (*„last chunk is empty”*) **ani sam `dage`** (*„Last chunk can not be empty!”*). To byłaby
    kopia, której nie da się odtworzyć. Archiwum tar ma rozmiar będący wielokrotnością 512 B, więc
    trafiałoby to ~1 na 128 kopii; przy standardowym `tar` z rekordem 10 KiB ~1 na 32.
- **Zamiast tego: własny moduł formatu `age` v1** (~370 linii; scrypt + X25519 + strumień ChaCha20-Poly1305)
  na prymitywach z `cryptography` 2.9.0 i `pointycastle` 3.9.1. **Zgodność z oficjalnym CLI: wszystko PASS.**
  Sprawdzone w obie strony dla 8 rozmiarów (0 B, 1 B, 64 KiB ± 1, 128 KiB…), z hasłem ASCII i z polskimi
  znakami, z X25519 i z plikiem tożsamości. Moduł odrzuca złe hasło, ucięcie (także na granicy kawałka)
  i jeden zmieniony bit. Fallback z D2 (własna koperta) nie był potrzebny, a format zostaje standardem.

### Measurements
| # | Pytanie | Wynik |
|---|---|---|
| **M1** | Czy Dysk jest w oknie wyboru **folderu** (`ACTION_OPEN_DOCUMENT_TREE`)? | **NIE.** Z zalogowanym kontem i zainstalowanym Dyskiem okno folderu pokazuje tylko pamięć urządzenia i kartę SD. W oknie zapisu **pliku** (`ACTION_CREATE_DOCUMENT`) Dysk jest |
| **M2** | Trwałe uprawnienie i ponowny zapis | **Dysk przyjmuje `takePersistableUriPermission` (odczyt + zapis)** dla obu plików (kopia + klucz). Zapis `"wt"` po zimnym starcie, bez okna: OK. **W tle** (WorkManager, proces zabity, bez Activity): do pliku lokalnego 157 MB `SUCCESS`; **do Dysku 10,6 MB `SUCCESS`** (6,5 s z uruchomieniem dostawcy Dysku). **Po restarcie emulatora:** 4 trwałe uprawnienia nadal aktywne, kopia na Dysk bez okna wyboru: OK |
| **M2a** | Kiedy rusza zadanie w tle | **Nieprzewidywalnie.** Zadanie jednorazowe bez warunków: raz ruszyło ~50 s po terminie; drugim razem było `Ready` (wszystkie warunki spełnione, standby `ACTIVE`, bez Doze) **ponad 44 min i nie wystartowało**, choć stałe JobSchedulera (`min_ready_cpu_only_jobs_count=3`, `max_cpu_only_job_batch_delay_ms=1860000`) zapowiadają ≤ 31 min. Do testu dostępu w tle uruchomione ręcznie (`cmd jobscheduler run -f`). **Wniosek dla produkcji:** termin kopii w tle wyznacza system, nie aplikacja. Kopia okresowa musi mieć widoczny w aplikacji „ostatnia udana kopia: kiedy” i nie może zakładać godziny |
| **M3** | Bez `INTERNET` | APK release nie ma `INTERNET` (`aapt`). Zapis do Dysku działa, bo wysyła aplikacja Dysku. **Dostawca odpowiada natychmiast** (10 MB w 37 ms) i przez kilka sekund podaje `_size: 0`, potem pełny rozmiar. Wniosek: **„zapisane” ≠ „wysłane do chmury”**, a aplikacja nie widzi momentu wysłania. **Potwierdzenie w chmurze (autor, drive.google.com):** oba pliki w `Grobing-spike`, kopia 10,1 MB, „plik binarny”, dostęp prywatny. WorkManager dokłada uprawnienia `WAKE_LOCK`, `ACCESS_NETWORK_STATE`, `RECEIVE_BOOT_COMPLETED` i `FOREGROUND_SERVICE`; żadne nie jest widoczne dla użytkownika |
| **M4** | Koszt | **scrypt (work factor 18, domyślny w `age`): 14,2 s i ~430 MB RAM** (czysty Dart). Kopia **10 MB**: wariant A **16,2 s**, wariant B **2,4 s**. Kopia **~157 MB** (75 × 2 MB), wariant B: **28,6 s** (sumy 4,1 s · tar 4,5 s · szyfrowanie 20,0 s ≈ 8 MB/s), zapis przez okno 1,1 s, **szczyt pamięci 195 MB** (strumieniowo) |
| **M5** | Kopia bez aplikacji | Plik z telefonu → PC → **oficjalne `age -d` + zwykły `tar`** → `manifest.json`, `grobing.db` (Python `sqlite3`: `integrity_check = ok`, 100 osób) i zdjęcia. **Przez chmurę:** autor pobrał z Dysku przeglądarką klucz i kopię zapisane przez emulator. Oficjalne CLI otworzyło klucz hasłem testowym (`age -d`), a kopię tym kluczem (`age -d -i`). Wynik: 12 plików, **wszystkie SHA-256 zgodne z manifestem**, `integrity_check = ok`. **Kopia jest czytelna bez Grobing** |
| **M6** | Odtworzenie | Ten sam emulator, z pliku przez okno systemowe: **odcisk po odtworzeniu = odcisk przy kopii** (`fd91310b79f4d2c1`), 1,4 s dla 10 MB (+ 14 s scrypt na klucz). **Odmowa, dane nietknięte (odcisk bez zmian):** złe hasło · zmieniony 1 bit · ucięte 100 B · kopia ze schematu v2 w aplikacji v1 (*„zaktualizuj aplikację”*). **Kopia v1 w aplikacji v2:** odtworzona i zmigrowana (`v1 → v2`), odcisk identyczny. **Drugie urządzenie (`Grobing_Restore`, pusta aplikacja, świeżo zalogowane konto) z Dysku:** klucz + hasło + kopia → **odcisk `fd91310b79f4d2c1`, identyczny jak na `Medium_Phone`**. Pobranie 10,6 MB przez okno systemowe 3,4 s, odszyfrowanie 1,05 s, weryfikacja 0,45 s. **Uwaga z UI:** na świeżym urządzeniu folder Dysku w oknie systemowym był pusty jeszcze kilka minut po zalogowaniu, nawet po otwarciu aplikacji Dysk. Pliki znalazła dopiero **wyszukiwarka okna** („grobing”). Instrukcja odtworzenia w produkcji (i notka przekazania) musi to mówić |
| **M7** | Kopia Androida | `allowBackup="false"` + `dataExtractionRules` wykluczające wszystko: transport lokalny → *„Backup is not allowed”*; D2D → pakiet odrzucony. **Próba kontrolna — samo `allowBackup="false"` bez reguł: D2D → `Success`**, czyli potwierdzenie dokumentacji Androida 12+. **Obecna aplikacja `com.grobing.app` (szablon Fluttera, domyślnie `allowBackup=true`): kopia lokalna `Success`, D2D `Success`** |

### Recommendation for ADR-004 (dla `docs`)
1. **Miejsce:** **jeden plik** w folderze Dysku autora, wskazany raz oknem zapisu (`ACTION_CREATE_DOCUMENT`),
   z trwałym uprawnieniem; każda kopia nadpisuje go w trybie `"wt"`. Okno folderu nie działa z Dyskiem
   (M1), więc **kopia przyrostowa (tylko nowe zdjęcia) przez okno systemowe nie jest możliwa**. Każda
   kopia wysyła całość.
2. **Format:** `age` v1 (odbiorca X25519) z `tar`(`manifest.json` + migawka SQLite `VACUUM INTO` +
   `media/*`). Manifest niesie `format_version`, `schema_version`, liczby rekordów i SHA-256 każdego pliku.
   **Własny moduł `age`** z testem zgodności z oficjalnym CLI jako bramką, bez `dage` i bez `dartage`.
3. **Klucz — wariant B:** w aplikacji tylko **klucz publiczny** (nie jest sekretem), więc kopia w tle
   **nie potrzebuje hasła ani `flutter_secure_storage`**. Tożsamość jest zaszyfrowana hasłem (scrypt) w
   drugim pliku obok kopii. To ten sam wzorzec, który zaleca dokumentacja oficjalnego `age`
   („passphrase-encrypted identity files”). Odtworzenie = plik klucza + hasło + plik kopii.
   **Koszt:** utrata pliku klucza = utrata kopii nawet z hasłem. Dlatego tożsamość
   (`AGE-SECRET-KEY-1…`, 74 znaki) powinna trafić też do notki przekazania, fizycznie
   ([[NT-007-hand-over-note]]). Wariant A (hasło w magazynie kluczy) odrzucony: 14 s i ~430 MB przy
   każdej kopii w tle, a do tego sekret w telefonie.
4. **Kopia Androida:** `allowBackup="false"` **i** `dataExtractionRules` z wykluczeniem wszystkiego w
   `<cloud-backup>` oraz `<device-transfer>`. Jedna droga na nowy telefon: nasza sprawdzona kopia.
5. **Kopia sprzed migracji (zamyka ⚠️ OPEN):** odtworzenie przepuszcza starszą kopię przez **zwykłe
   migracje** aplikacji; kopię z nowszego schematu odrzuca z prośbą o aktualizację.
6. **Walidacja przed nadpisaniem:**
   - odszyfrowanie do katalogu tymczasowego;
   - tar tylko ze zwykłymi plikami i bezpiecznymi ścieżkami;
   - zgodność listy plików i SHA-256 z manifestem;
   - `PRAGMA integrity_check`;
   - `user_version` = manifest;
   - liczby rekordów (także po migracji).

   Dopiero potem podmiana katalogu przez `rename`.

### Follow-ups — not decided here
- ⚠️ **`grobing-code` dziś ma domyślne `allowBackup=true`** (M7). Pozycja produkcyjna kopii musi to
  zmienić **przed pierwszymi prawdziwymi danymi**.
- **Kopia w tle w produkcji** potrzebuje Darta w tle (np. `workmanager`) albo szyfrowania natywnego.
  Spike sprawdził natywny zapis w tle, nie szyfrowanie w tle. Wariant B to ułatwia, bo nie ma sekretu.
- **Pełna kopia przy każdym zapisie:** przy ~1 GB zdjęć w oryginale każda kopia wysyła ~1 GB.
  Częstotliwość (np. raz dziennie, po zmianach) i ewentualne zmniejszanie zdjęć w aplikacji to decyzje
  pozycji produkcyjnych.
- **„Zapisane” ≠ „w chmurze”** (M3): aplikacja może sprawdzić tylko, że plik przyjęto. Pytanie o fakty co
  10 pozycji (*„czy ostatnie odtworzenie naprawdę zadziałało?”*) pozostaje jedynym dowodem.
- Wydajność: szyfrowanie w czystym Darcie to ~8 MB/s; `cryptography_flutter` (natywne) jest opcją, jeśli
  zajdzie potrzeba.
- Środowisko: Gradle przy pierwszym buildzie doinstalował **Android SDK Platform 35** (wymaga go
  WorkManager). Dodatek obok, Friendsheet nietknięty.
- Środowisko: `Grobing_Restore` założony przez `avdmanager` miał `hw.keyboard=no`, więc klawiatura
  komputera nie działała przy logowaniu. Poprawione na `yes`. Do tego na obu emulatorach wyłączone pismo
  rysikiem (`stylus_handwriting_enabled 0`), bo samouczek Gboard przechwytywał wpisywany tekst.

### For `qa` — what is evidenced, what is left for stop #2
- **Już z dowodem** (zapis wyżej): M1-M7. Autor brał udział w M3 (przeglądarka) i M5 (pobranie z Dysku
  na PC).
- **Do stopu #2 zostaje to, co widzi tylko człowiek**, na `Grobing_Restore`, który jest uruchomiony z
  odtworzonymi danymi:
  - ekran aplikacji spike'a pokazuje „ODTWORZONO — odcisk fd91310b79f4d2c1”;
  - po wpisaniu złego hasła i „4b” widać odmowę, a odcisk się nie zmienia.
- **Sprzątanie celowo po stopie #2** (zmiana kolejności względem kroku 6 planu): `_throwaway/spike-003/`,
  APK spike'a w `_throwaway/`, CLI `age` w scratchpadzie oraz aplikacja `com.grobing.spike003` na obu
  emulatorach są potrzebne do ręcznej weryfikacji. Folder `Grobing-spike` na Dysku i dwa pliki w
  Pobranych usuwa autor.

## Verification
> `qa`, 2026-10-05. Spike: kod nie zostaje, więc testów w `grobing-code` nie ma (DoD SPIKE). Dowody
> sprawdzone **niezależnie od deklaracji `dev`**, czyli powtórzone albo odczytane na nowo.

### Automated / re-checked
| Co | Jak sprawdzone przez `qa` | Wynik |
|---|---|---|
| Zgodność własnego modułu `age` z oficjalnym CLI | macierz `tool/interop.dart` uruchomiona ponownie (CLI `age` v1.3.2) | ✅ moduł: 0 × FAIL (scrypt ASCII i z polskimi znakami, 8 rozmiarów, X25519, plik tożsamości, 4 przypadki odrzucenia) |
| Błędy `dage` (podstawa odstępstwa od D2) | ta sama macierz | ✅ powtórzone: 22 × FAIL `dage`, te same dwie przyczyny |
| Odtworzenie na drugim urządzeniu | „2c Stan danych” na `Grobing_Restore`, odczyt na nowo | ✅ `fd91310b79f4d2c1` = odcisk z `Medium_Phone` |
| M7, obecny stan aplikacji | `grobing-code/android/app/src/main/AndroidManifest.xml` | ✅ potwierdzone: brak `allowBackup` i `dataExtractionRules`, więc kopia Androida jest włączona domyślnie |
| Dane rodziny w zmianach | `git status` w 3 repo + przegląd diffu vaulta | ✅ zmienione tylko 2 pliki `.md` w vaulcie; `grobing-code` i `grobing-agents` czyste. W pozycji brak e-maila, identyfikatorów plików z Dysku i kluczy. Kod eksperymentu żyje poza repo (`_throwaway/`) |

### Manual (stop #2)
- Kroki 1-3 na `Grobing_Restore` (odcisk po odtworzeniu · złe hasło · odtworzenie rękami autora):
  **„pomiń”**. Autor (2026-10-05): *„dobra zakładam że działa”*. Kroków nie wykonał, więc zapisane jako
  pominięte, **nie** jako „ok”.
- Co to znaczy dla dowodu: odtworzenie przez Dysk na drugim emulatorze **było wykonane naprawdę**, ale
  sterował nim agent przez `adb`, a odcisk odczytał agent (dwa razy, `dev` i `qa`). Człowiek potwierdził
  własnymi oczami tylko M3 (pliki w chmurze, przeglądarka) i M5 (pobrał pliki, które CLI otworzyło na PC).
  **Złe hasło na drugim urządzeniu nie było sprawdzone.** Odmowę przy złym haśle mamy tylko z
  `Medium_Phone` i z macierzy na PC.

### Verdict (self-check)
**APPROVED** z uwagami. Wszystkie warunki z *Exit → evidence* mają dowód, a odtworzenie zostało wykonane
naprawdę (DoD pozycji).

**Czego szukałem i nie znalazłem:**
- danych rodziny w zmianach (tylko 2 pliki `.md` w vaulcie, dane w eksperymencie wymyślone);
- kluczy `AGE-SECRET-KEY`, e-maila i identyfikatorów plików z Dysku w pozycji;
- błędu zgodności własnego modułu `age` z oficjalnym CLI (macierz powtórzona);
- rozjazdu odcisku między urządzeniami;
- nadpisania danych przy odmowie;
- uprawnienia `INTERNET` w APK eksperymentu.

**Uwagi, które nie blokują spike'a** (do pozycji produkcyjnej kopii):
- **Podmiana katalogu przy odtworzeniu nie jest atomowa.** To dwa `rename`: `data` → `data.old`, potem
  staging → `data`. Awaria między nimi zostawia aplikację bez `data` (dane są w `data.old`). Produkcja
  potrzebuje odzyskania tego stanu przy starcie.
- **Rozpakowanie tar zapisuje pliki przed porównaniem rozmiarów z manifestem.** Złośliwa albo uszkodzona
  kopia może zapełnić pamięć telefonu. Produkcja: limit rozmiaru i sprawdzenie wolnego miejsca przed
  rozpakowaniem.
- Stop #2 pominięty (wyżej). Pierwsze odtworzenie, które człowiek obejrzy, wypadnie w pozycji
  produkcyjnej. Tam warto go nie pomijać.

### Cleanup (2026-10-05, po stopie #2)
- ✅ Kod eksperymentu usunięty: cały `_throwaway/` (projekt, build, oba APK). CLI `age` i pliki
  pomocnicze usunięte ze scratchpada sesji.
- ✅ `com.grobing.spike003` odinstalowane z `Medium_Phone` i z `Grobing_Restore`; `com.grobing.app` na
  `Medium_Phone` nietknięte.
- `Grobing_Restore` zostaje jako urządzenie do próbnych odtworzeń, z zalogowanym kontem Google autora.
- **Autor:** usuwa folder `Grobing-spike` na Dysku i dwa pliki `grobing-*.age` z Pobranych na PC.
