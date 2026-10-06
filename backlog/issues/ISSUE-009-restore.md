---
title: "ISSUE-009 — Restore from the backup file on a fresh install, validated before any overwrite"
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
created: 2026-10-05
updated: 2026-10-06
---

# ISSUE-009 — Kopia: odtworzenie

> [[ADR-004-backup-format-encryption-destination]] pkt 5-6 i uwagi `qa` ze
> [[SPIKE-003-backup-and-restore]] → *Verification*. **Odtworzenie = plik klucza + hasło + plik kopii.**

## What to build
1. **Odtworzenie na świeżej instalacji:** wybór pliku kopii i pliku klucza systemowym oknem otwarcia
   pliku, hasło, potem walidacja, migracje i podmiana danych.
2. **Walidacja przed nadpisaniem czegokolwiek (ADR-004 pkt 6):**
   - odszyfrowanie do katalogu tymczasowego;
   - `tar` tylko ze zwykłymi plikami i bezpiecznymi ścieżkami;
   - lista plików i SHA-256 zgodne z manifestem;
   - `PRAGMA integrity_check`;
   - `user_version` = manifest;
   - liczby rekordów zgodne, także po migracji.
3. **Kopia ze starszego schematu** przechodzi zwykłe migracje aplikacji, a z nowszego jest odrzucana z
   prośbą o aktualizację (ADR-004 pkt 5, [[NFR-003-migracje-schematu]]).
4. **Z uwag `qa` (SPIKE-003):**
   - odzyskanie stanu po awarii w trakcie podmiany (dwa `rename` nie są atomowe) przy następnym starcie;
   - limit rozmiaru i sprawdzenie wolnego miejsca **przed** rozpakowaniem;
   - instrukcja w aplikacji: na świeżym telefonie folder Dysku w oknie systemowym bywa pusty, a pliki
     znajduje wyszukiwarka okna.

## Acceptance Criteria
- [ ] Na `Grobing_Restore` odtworzenie kopii z Dysku daje odcisk danych identyczny ze źródłem
      ([[NFR-002-odtworzenie-na-nowym-telefonie]]).
- [ ] Złe hasło, uszkodzony plik, `tar` z niebezpieczną ścieżką, niezgodny manifest i kopia z nowszego
      schematu kończą się odmową z czytelnym komunikatem, a dane w telefonie zostają nietknięte.
- [ ] Ścieżka kopii ze starszego schematu sprawdzona testem (jak krok 5 spike'a: syntetyczna v2).
- [ ] Przerwanie w trakcie podmiany → przy następnym starcie aplikacja ma spójne dane: stare albo
      nowe, nigdy żadnych.
- [ ] Kopia większa niż limit albo brak miejsca → odmowa przed rozpakowaniem.

## Out of Scope
- Zapis kopii → [[ISSUE-008-backup-write]].
- Scalanie kopii z danymi już obecnymi w telefonie. Odtworzenie zastępuje dane. Jak chronić telefon,
  który już ma dane (np. wyraźne ostrzeżenie), ustala `planning`.

## Technical Notes
- **Stop #2 tym razem nie pomijać** (uwaga `qa` ze SPIKE-003): pierwsze odtworzenie, które obejrzy
  człowiek, wypada tutaj. W spike'u złe hasło na drugim urządzeniu nie było sprawdzone.
- **2026-10-06, z zamknięcia [[ISSUE-008-backup-write]]:**
  - **Dysk z kodem produkcyjnym nie był jeszcze sprawdzony** (stop #2 ISSUE-008 pominięty; kanał
    działał z Pobranymi emulatora, Dysk tylko z kodem spike'a). Tutaj kopia powstaje w Dysku na
    `Medium_Phone` i jest czytana z Dysku na `Grobing_Restore` — pierwszy raz kodem produkcyjnym. To
    drugi powód, żeby stopu #2 nie pomijać.
  - **Limit work factor przy odtwarzaniu w telefonie:** `ScryptIdentity` domyślnie przyjmuje do 22, jak
    oficjalne CLI, a 22 to ~4 GB pamięci. Nasze pliki klucza mają 18 — warto przekazać niższy limit.
  - **`backup.json` leży obok bazy** (stan kopii: klucz publiczny, plik w Dysku, czasy). Odtworzenie musi
    zdecydować, czy go zachowuje (ten sam telefon) i czym jest na świeżym telefonie (brak konfiguracji).
  - **Gotowe do użycia:** odszyfrowanie w module `age` (92 oficjalne wektory) · `BackupManifest.fromJson` ·
    w manifeście `size` (wolne miejsce przed rozpakowaniem) i `data_fingerprint` (sprawdzenie wyniku jedną
    liczbą) · `tool/fingerprint.dart` na PC. Format: `04_ARCHITECTURE/backup-format.md`.

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-008-backup-write]] | technical | `done` |
| emulator `Grobing_Restore` | technical | istnieje (SPIKE-003) |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC · ręczna weryfikacja na
emulatorze (dwa urządzenia) · próbne odtworzenie przechodzi · zero danych rodziny w zmianach · INVEST
self-check. Po przyjęciu tego ISSUE [[US-001-kopia-z-odtworzeniem]] może przejść do zamknięcia.

## Implementation plan
> `planning`, 2026-10-06. **DoR:** jasny zakres ✅ (ADR-004 pkt 5-6 + uwagi `qa` ze SPIKE-003) · powiązana
> US: [[US-001-kopia-z-odtworzeniem]] ✅ (AC-3, AC-4) · krok ścieżki: n/a, poza ścieżką (M8) ✅ ·
> `task-level` ✅. **Warstwa danych:** schemat się **nie** zmienia (v1), ale ścieżka migracji przez
> odtworzenie dostaje test z syntetyczną v2 (AC-3) · próbne odtworzenie — **to jest ta pozycja**, przez
> Dysk na `Grobing_Restore` (stop #2) · źródło faktu — **n/a**, pozycja nie zapisuje faktów o rodzinie
> (dane wymyślone, tylko w buildzie debug).

### Prior art (sources, not memory)
- **Podmiana danych odporna na awarię:** SQLite, [*Atomic Commit*](https://www.sqlite.org/atomiccommit.html)
  — zamiar zapisany trwale **przed** zmianą, odzyskanie przy następnym otwarciu (*hot journal*). Ten sam
  wzorzec niżej: znacznik = punkt zatwierdzenia, przy starcie dokończenie w przód.
- **Baza zawsze z własnym dziennikiem:** SQLite, [*How To Corrupt*](https://www.sqlite.org/howtocorrupt.html)
  → 1.3 *Deleting a hot journal* i 1.4 *Mispairing database files and hot journals*: plik bazy
  przenosimy **razem** z `-journal`/`-wal`/`-shm`; nowa baza nigdy nie dostaje cudzego dziennika.
- **Okno otwarcia pliku:** Android, [*Access documents and other files*](https://developer.android.com/training/data-storage/shared/documents-files)
  (sprawdzone 2026-10-06): `ACTION_OPEN_DOCUMENT` + `takePersistableUriPermission(READ | WRITE)` daje
  trwały dostęp; o zapis pytać `FLAG_SUPPORTS_WRITE`, nie `canWrite()`; `OpenableColumns.SIZE` bywa
  **nieznany** dla plików zdalnych.
- **Pomiary ze SPIKE-003 (M6):** odtworzenie 10 MB z Dysku na `Grobing_Restore` — pobranie 3,4 s,
  odszyfrowanie 1,05 s, weryfikacja 0,45 s, scrypt ~14 s (release); na świeżym urządzeniu folder Dysku
  w oknie bywa pusty, pliki znajduje wyszukiwarka okna.
- **tar ustar** i **`age` v1**: źródła w [[ISSUE-008-backup-write]] → *Prior art*; format kopii:
  `04_ARCHITECTURE/backup-format.md`.

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego · czego to nie da · co obali |
|---|---|---|---|
| D1 | **Rozmiar** (`ideal_days: 1` przy 4 punktach budowy i 5 AC) | **Bez podziału, ~1,5 dnia.** | Wszystkie AC to jeden przepływ: walidacja, podmiana i odzyskanie po awarii nie mają sensu osobno. Odtworzenie bez odzyskania po awarii byłoby niebezpiecznym stanem pośrednim. Inaczej niż przy ISSUE-008, tu nie ma osobnej niewiadomej do wydzielenia. **Czego nie da:** pozycji w rozmiarze z `glossary.md`. **Alternatywa:** D3 → ISSUE-010 (−0,2 dnia) |
| D2 | **„Limit” z AC-5** — ISSUE nie podaje liczby | **Limitem jest to, co telefon pomieści:** odmowa, gdy wolne miejsce < 2 × rozmiar pliku kopii + 200 MB (lokalna kopia zaszyfrowana + rozpakowane pliki). **Do tego licznik bajtów w trakcie** — rozmiar od Dysku bywa nieznany (*Prior art*), więc przekroczenie budżetu przerywa kopiowanie. **Bez sztywnego sufitu w GB** | Sufit w GB obroni telefon przed niczym, przed czym nie broni wolne miejsce. Za to po latach, przy dużej kolekcji zdjęć, odmówi prawdziwego odtworzenia. **Czego nie da:** ochrony przed kopią, która mieści się w wolnym miejscu, ale zajmie je prawie całe. Na to jest zapas 200 MB. **Obali ją:** dostawca zawyża rozmiar albo go nie podaje i licznik nie zadziała (test AC-5 z „nieznanym rozmiarem”) |
| D3 | **`backup.json` po odtworzeniu** (pytanie z *Technical Notes*) | **Ten sam telefon (kopia skonfigurowana):** bez zmian — ten sam klucz, ten sam plik. **Świeży telefon:** kopia **zostaje przy kluczu z odtworzenia** (klucz publiczny z pliku klucza) i pisze do **tego samego pliku w Dysku**, jeśli Dysk da trwały zapis przez okno otwarcia. Jeśli nie da, kopia zostaje nieskonfigurowana, a ekran mówi, że nowa konfiguracja = nowy klucz = poprawka w notce przekazania | Odtworzenie zdarza się właśnie przy zmianie telefonu. Bez D3 każda zmiana telefonu tworzy nowy klucz, więc plik klucza z notki u rodziny **po cichu przestaje otwierać nowe kopie** (zamknięcie [[ISSUE-008-backup-write]]). **Czego nie da:** obsługi dwóch żywych telefonów piszących do jednego pliku (*Self-check*). **Obali ją:** krok 1 — Dysk nie daje `FLAG_SUPPORTS_WRITE` albo trwałego zapisu przez `ACTION_OPEN_DOCUMENT` → wariant zapasowy, raport |
| D4 | **Telefon, który już ma dane** (*Out of Scope*: ustala `planning`) | **Ostrzeżenie z liczbami ze „Stanu danych” + wyraźne „Zastąp dane”.** Bez kopii bezpieczeństwa starych danych po sukcesie. **Bez propozycji „najpierw zrób kopię”** | „Zrób kopię teraz” przed odtworzeniem **nadpisałoby w Dysku ten sam plik, z którego odtwarzamy** (jeden plik, nadpisywany: ADR-004 pkt 1). Taki przycisk w tym miejscu to pułapka. **Czego nie da:** cofnięcia po potwierdzeniu. **Alternatywa:** stare dane zostają w telefonie do następnej udanej kopii (+0,2 dnia) |

### Scope diff vs the item (to accept at stop #1)
- **+ D3:** po odtworzeniu na świeżym telefonie kopia działa dalej tym samym kluczem (pytanie zadane w
  *Technical Notes*, odpowiedź to nowe zachowanie).
- **+ przeładowanie aplikacji po odtworzeniu** bez restartu: ta sama funkcja podmiany działa po
  odtworzeniu i przy starcie po awarii, więc każde odtworzenie ćwiczy ścieżkę odzyskania.
- **= AC-5 doprecyzowane przez D2** (limit = wolne miejsce z zapasem, nie liczba w GB).
- **+ przycisk „Odtwórz z kopii”** na ekranie „Stan danych” — w trybie release też, bo to funkcja dla
  prawdziwego telefonu.

### Steps (dev)
1. **Falsyfikator: kanał otwarcia + Dysk kodem produkcyjnym (≤ 1 h), przed czymkolwiek innym.**
   `BackupDocuments.kt` + `documents.dart` dostają:
   - `openDocument` (`ACTION_OPEN_DOCUMENT`, prośba o odczyt, zapis i trwałość);
   - `documentInfo` (rozmiar albo „nieznany” i `FLAG_SUPPORTS_WRITE`);
   - `readFile(uri → ścieżka lokalna)` z budżetem bajtów;
   - `freeSpace` (`StatFs` katalogu danych aplikacji).

   Pomiar na emulatorach:
   - **(a)** na `Medium_Phone` konfiguracja kopii **do Dysku** — pierwszy zapis do Dysku kodem
     produkcyjnym;
   - **(b)** na `Grobing_Restore` okno otwarcia znajduje plik, `readFile` daje bajty, a SHA-256 zgadza
     się z plikiem z `Medium_Phone`;
   - **(c)** rozmiar jest znany;
   - **(d)** `FLAG_SUPPORTS_WRITE` jest ustawione, a trwały zapis przyjęty (D3).

   **(a) albo (b) nie przechodzi → STOP i raport** (to byłby błąd ISSUE-008, nie tej pozycji). (d) nie
   przechodzi → wariant zapasowy D3, zapisane w raporcie, praca idzie dalej.
2. **Czytnik tar** (`lib/backup/tar_reader.dart`), ścisły dla formatu v1:
   - suma kontrolna nagłówka;
   - tylko zwykłe pliki (`typeflag` `0` albo NUL);
   - ścieżki tą samą regułą co zapis (wspólna funkcja z `tar_writer.dart`) i tylko te z formatu:
     `grobing.db` raz, `media/…`, `manifest.json` jako ostatni;
   - bez duplikatów, potem dwa bloki zer i nic niezerowego za nimi;
   - zapis tylko w katalogu tymczasowym, z budżetem bajtów; SHA-256 liczone w trakcie zapisu.
3. **Odtworzenie do katalogu tymczasowego** (`lib/backup/restore_service.dart`). Katalog tymczasowy jest
   w katalogu danych aplikacji, nie w cache — ten sam system plików, więc `rename` zadziała, a system
   nie wyczyści go w trakcie:
   1. miejsce (D2) przed czymkolwiek;
   2. plik klucza (mały, z limitem rozmiaru), odszyfrowany hasłem w `Isolate.run` przez
      `ScryptIdentity(maxWorkFactor: 20)`, czyli ~1 GB pamięci, a nie 4 GB przy domyślnych 22. Pliki
      klucza Grobing i domyślne oficjalnego `age` mają 18;
   3. plik kopii skopiowany lokalnie, odszyfrowany strumieniowo do czytnika tar, a kopia zaszyfrowana
      usunięta zaraz po odszyfrowaniu;
   4. sprawdzenie manifestu:
      - `format_version` = 1;
      - `schema_version` ≤ wersja aplikacji, a nowszy → „Kopia z nowszej wersji Grobing — zaktualizuj
        aplikację”;
      - lista plików, rozmiary i SHA-256 = manifest;
   5. migawka otwarta tylko do odczytu:
      - `integrity_check` = `ok`;
      - `user_version` = manifest;
      - liczby rekordów = manifest;
      - **odcisk = `data_fingerprint`** (przed migracją; po migracji odcisk się zmienia z definicji);
   6. starszy schemat: otwarcie klasą bazy aplikacji, czyli **zwykłe migracje** (ADR-004 pkt 5). Potem
      liczby rekordów każdej tabeli z manifestu bez zmian i ponownie `integrity_check`.

   Każda odmowa ma polski komunikat bez ścieżek i treści oraz „Dane w telefonie są nietknięte”, a katalog
   tymczasowy jest usuwany. Tożsamość i hasło nigdy nie trafiają na dysk, do logów ani do komunikatów.
   Osobny komunikat: „Ten plik klucza nie otwiera tej kopii” (inny klucz, `age` *no match*).
4. **Podmiana z odzyskaniem** — jedna funkcja `completePendingRestore(katalog danych)`:
   - zapis znacznika `restore.json` (plik tymczasowy + `rename`) to **punkt zatwierdzenia**;
   - zamknięcie bazy;
   - obecne `grobing.db` (+ `-journal`/`-wal`/`-shm`) i `media/` → `restore-old/`;
   - nowe → na miejsce;
   - przy D3 `backup.json` ze znacznika;
   - usunięcie znacznika, potem `restore-old/`.

   Każdy krok idempotentny. Przy starcie (`main.dart`, **przed** otwarciem bazy):
   - znacznik jest → dokończenie w przód;
   - znacznika nie ma → usunięcie resztek katalogu tymczasowego i `restore-old/`.

   Stan „ani starych, ani nowych” nie istnieje na żadnym etapie (AC-4).
5. **Przeładowanie po odtworzeniu:** korzeń aplikacji umie zamknąć bazę, wywołać
   `completePendingRestore` i otworzyć nową bazę z nowym `BackupService` (szczegół należy do `dev`).
6. **Ekran „Odtwórz z kopii”** (`lib/app/restore_screen.dart`, wejście z „Stanu danych”):
   - akapit: trzy rzeczy (plik kopii, plik klucza, hasło) i co jest sprawdzane;
   - **„Na nowym telefonie folder Dysku w oknie bywa pusty — wpisz »grobing« w wyszukiwarkę okna”**;
   - D4: przy niepustych danych ostrzeżenie z liczbami i „Zastąp dane”;
   - wybór pliku kopii i pliku klucza, hasło ukryte;
   - postęp po etapach (scrypt ~15 s w release, ~40 s w debug);
   - wynik: „Odtworzono kopię z dnia <`created_at`>”, potem „Stan danych” z odciskiem.

   Ekran techniczny w istniejącym motywie, więc agent `ui` nie jest potrzebny (jak w ISSUE-007 i 008).
7. **README `grobing-code` → „Kopia” → Odtworzenie:** co jest sprawdzane i w jakiej kolejności, znacznik
   i odzyskanie przy starcie, D2, D3.

### Files likely touched
`grobing-code`:
- `android/app/src/main/kotlin/com/grobing/app/BackupDocuments.kt` · `MainActivity.kt` (drugi kod żądania);
- `lib/backup/documents.dart` · `lib/backup/tar_writer.dart` (wspólna reguła ścieżek);
- nowe w `lib/backup/`: `tar_reader.dart`, `restore_service.dart` i plik podmiany (nazwa należy do `dev`);
- `lib/main.dart` · `lib/app/grobing_app.dart` (przeładowanie) · `lib/app/data_state_screen.dart` ·
  `lib/app/restore_screen.dart` (nowy);
- `README.md`;
- testy (`qa`): `test/backup/restore_*`, `test/support/backup_fakes.dart` (`FakeDocumentStore` z
  otwarciem, rozmiarem i wolnym miejscem).

`grobing-vault`: ta pozycja · `TRACEABILITY.md`.

### AC → tests (`qa`)
| AC | Test happy-path (host) | Ręcznie (stop #2) |
|---|---|---|
| AC-1 odcisk = źródło | wymyślone dane → `BackupService` (sztuczny Dysk) → odtworzenie do pustego katalogu → odcisk = źródło, liczby = manifest. Też: odtworzenie na tym samym telefonie z innymi danymi → odcisk = kopia | `Medium_Phone` → Dysk → `Grobing_Restore`: odcisk zgodny |
| AC-2 odmowy | po jednym teście na: złe hasło · inny plik klucza · zmieniony bit · ucięty plik · tar z `../`, ścieżką absolutną, dowiązaniem, nieznanym plikiem, duplikatem · SHA-256 albo rozmiar ≠ manifest · `format_version` 2 · schemat nowszy · uszkodzona baza (`integrity_check`). **W każdym:** odcisk żywych danych bez zmian, katalog tymczasowy usunięty, komunikat bez ścieżek | złe hasło na `Grobing_Restore` (w spike'u niesprawdzone) |
| AC-3 starszy schemat | testowa klasa bazy v2 (dodana kolumna + krok migracji) odtwarza kopię v1: `user_version` 2, liczby = manifest, `integrity_check` `ok` | — |
| AC-4 awaria w trakcie podmiany | dla **każdego** punktu przerwania (po znaczniku, po każdym przeniesieniu, przed usunięciem `restore-old/`) → `completePendingRestore` → odcisk = stary **albo** nowy, nigdy brak bazy. Resztki bez znacznika usuwane. Dziennik starej bazy nie zostaje przy nowej | — (zabicie procesu w tej milisekundzie nie jest powtarzalne) |
| AC-5 limit i miejsce | sztuczny Dysk: rozmiar > budżet → odmowa **zanim** cokolwiek powstanie w katalogu tymczasowym. Rozmiar nieznany + strumień większy niż budżet → przerwanie i sprzątanie | — |

### Manual verification (stop #2) — kroki według miejsca
> **Nie pomijać** (*Technical Notes*): pierwszy zapis do Dysku i pierwsze odtworzenie kodem
> produkcyjnym, które obejrzy człowiek. `qa` porównuje odpowiedź ze stanem emulatorów.

- **Terminal VS Code** (`grobing-code`): `flutter run` na `Medium_Phone` (debug, bo potrzebne są wymyślone
  dane). Na `Grobing_Restore` czystą instalację robi `qa`.
- **Emulator `Medium_Phone`:**
  1. „Stan danych” → „Wgraj wymyślone dane”.
  2. „Skonfiguruj kopię”: hasło **testowe** (nie Twoje prawdziwe) dwa razy, ~40 s czekania; plik klucza
     i plik kopii zapisz **w Dysku** (Mój dysk, jeden folder).
  3. Zapisz pierwsze 16 znaków odcisku ze „Stanu danych”.
- **Przeglądarka na PC:** drive.google.com → dwa pliki ze świeżą godziną.
- **Emulator `Grobing_Restore`:**
  4. „Stan danych” → „Odtwórz z kopii”. Czy tekst jest jasny?
  5. Wybierz plik kopii i plik klucza (pusty folder → wyszukiwarka okna, „grobing”), wpisz **złe** hasło
     → odmowa, „Stan danych” bez zmian.
  6. To samo z dobrym hasłem → „Odtworzono kopię z dnia …”, **odcisk = ten z kroku 3**.
  7. (D3) Sekcja „Kopia” skonfigurowana → „Zrób kopię teraz” → w przeglądarce godzina pliku się zmienia.
- **Emulator `Medium_Phone`:**
  8. (D4) „Odtwórz z kopii” przy danych w telefonie → ostrzeżenie z liczbami → „Anuluj” → odcisk bez zmian.
- **Napisz tutaj:** „ok” · „pomiń” · opis błędu.

### Closing checklist (docs)
- [[ADR-004-backup-format-encryption-destination]] → *Follow-ups*: datowana linia — odzyskanie po awarii,
  limit (D2) i instrukcja z wyszukiwarką zamknięte w kodzie.
- [[NFR-002-odtworzenie-na-nowym-telefonie]] → *Notes*: pozycja produkcyjna przeszła odtworzenie na
  drugim urządzeniu (o ile stop #2 „ok”; inaczej zapisać, czego nie sprawdzono).
- [[US-001-kopia-z-odtworzeniem]]: AC-3 i AC-4 pokryte. US zostaje `in-progress` do ISSUE-010. Linia
  *Definition of Done* tej pozycji mówi „US-001 może przejść do zamknięcia”, a od podziału D1 w ISSUE-008
  czeka jeszcze ISSUE-010. Zastane, do poprawki.
- [[NT-007-hand-over-note]] → wkład: kroki odtworzenia (wyszukiwarka okna) i D3 — po zmianie telefonu
  klucz zostaje ten sam, więc notka jest nadal ważna.
- `04_ARCHITECTURE/backup-format.md` → *Known limits*: dwa telefony piszące do jednego pliku (D3).
- `ideal_days` tej pozycji według D1.
- Bez pusha do zamknięcia [[NT-008-publication-review]].

### Out of Scope (this plan)
- Scalanie kopii z danymi w telefonie — odtworzenie zastępuje (*Out of Scope* pozycji).
- Kopia w tle → [[ISSUE-010-background-backup]].
- Wybór starszej wersji pliku z historii wersji Dysku, zmiana hasła, odtwarzanie z eksportu.
- Odtwarzanie strumieniowe wprost z Dysku, bez lokalnej kopii zaszyfrowanej. Oszczędza 1 × rozmiar
  miejsca, ale wymaga strumienia przez kanał natywny — dopiero gdy D2 zacznie odmawiać.

### Self-check (planning) — said out loud
- **Dwa żywe telefony** (stary nadal działa) po D3 piszą naprzemiennie do jednego pliku. Ostatni zapis
  wygrywa, a dane z drugiego telefonu znikają z kopii. Do zapisania w *Known limits*, nie do rozwiązania tu.
- **Jeden nadpisywany plik = brak historii kopii.** Jeśli do kopii trafią zepsute dane, poprzednia dobra
  kopia istnieje najwyżej w historii wersji Dysku — **niesprawdzone**. Pytanie do retro, nie zakres.
- „Nowszy schemat” wychodzi dopiero po odszyfrowaniu całości, bo manifest jest na końcu. Format v1 jest
  zamrożony, więc tak zostaje; przy dużych kopiach odmowa przyjdzie po minucie, nie od razu.
- AC-4 sprawdzają tylko testy na hoście — każdy punkt przerwania, ale nie prawdziwe zabicie procesu.
- `maxWorkFactor: 20`: plik klucza zaszyfrowany na PC z wyższym work factor zostanie odrzucony z
  komunikatem. Notka przekazania nie każe go przeszyfrowywać, więc to tylko granica.

## Dev report
> `dev`, 2026-10-06. **Stop #1:** autor „tak” dla planu z D1–D4 (2026-10-06). Kod w `grobing-code`,
> niezacommitowany. Flutter 3.41.1 (przypięty). `flutter analyze lib tool` bez uwag.

### Step 1 — falsifier: ✅ passed (a), (b), (c), (d)
Kanał natywny (`BackupDocuments.kt`): `openDocument`, `documentInfo` (rozmiar, nazwa,
`FLAG_SUPPORTS_WRITE`), `readFile` z budżetem bajtów, `freeSpace`. Sonda: tymczasowy plik startowy,
usunięty po pomiarze.
- **(a) Dysk kodem produkcyjnym:** `Medium_Phone`, build debug, wymyślone dane (odcisk
  `cac13dcd1f3fb213`). „Skonfiguruj kopię” → plik klucza i plik kopii w **Dysku**, w nowym folderze
  `Grobing-dev-009` → „Ostatnia udana kopia 07:34”. „Zrób kopię teraz” → 07:35 bez okna. `backup.json`:
  klucz publiczny, URI Dysku, czasy.
- **(b) Odczyt przez okno otwarcia na `Grobing_Restore`:** plik kopii ze SPIKE-003 w Dysku, 10,6 MB w
  **3,9 s**. Plików z (a) Dysk jeszcze wtedy nie pokazywał: `Medium_Phone` wyłączyłem 30 s po zapisie,
  a „zapisane” ≠ „w chmurze” (ADR-004). Pojawiły się kilkanaście minut później, a odtworzenie z nich
  przeszło (*Smoke checks*).
- **(c)** Rozmiar znany. **(d)** `FLAG_SUPPORTS_WRITE` = tak, trwałe uprawnienie odczyt + zapis przyjęte,
  zapis tych samych bajtów przeszedł → **D3 w wariancie podstawowym**. Budżet: `too_large`, a
  niepełnego pliku nie zostaje. `freeSpace` zgadza się z `df`.

### Smoke checks (dev)
- **Host** (skrypt próbny w scratchpadzie, wymyślone dane, 9/9):
  - świeży telefon: odcisk = źródło, kopia działa dalej (D3), bez resztek;
  - złe hasło → odmowa, odcisk bez zmian, katalog tymczasowy usunięty;
  - plik kopii wybrany jako plik klucza → „To nie jest plik klucza Grobing”;
  - za mało miejsca → odmowa przed kopiowaniem;
  - ten sam telefon z innymi danymi → zastąpione, `backup.json` bez zmian;
  - syntetyczna v2 (dodana kolumna) → `user_version` 2, liczby = manifest;
  - schemat nowszy → „nowszej wersji”;
  - przerwanie po każdym kroku podmiany (znacznik, każde przeniesienie, zatwierdzenie) → zawsze nowe dane,
    a dziennik starej bazy (`-journal`) nie zostaje przy nowej;
  - tar z `../evil` → odmowa, nic poza katalogiem.
- **Emulator `Grobing_Restore`, build debug:**
  - z Pobranych (pliki z hosta, wymyślone dane): złe hasło → odmowa po ~18 s, „Dane w telefonie są
    nietknięte”. Dobre hasło → ~21 s → przeładowanie na „Stan danych” z komunikatem, **odcisk
    `ff6d4202e5b6c0a2` = źródło**. D3: „Zrób kopię teraz” nadpisuje ten sam plik;
  - **z Dysku, kopia z (a)**: D4 — ostrzeżenie „W telefonie są już dane”, potem okno z liczbami
    (osoby 6, groby 4, cmentarze 2, pliki zdjęć 2). „Anuluj” → nic się nie zaczęło. „Zastąp dane” →
    ~21 s → **odcisk `cac13dcd1f3fb213` = `Medium_Phone`**, „Kopia działa jak dotąd” (ten sam
    telefon);
  - po odtworzeniach w katalogu danych tylko `backup.json`, `grobing.db`, `media` — bez
    `restore-staging/`, `restore-old/` i znacznika.

### Deviations from the plan
- **Korzeń aplikacji:** `GrobingApp` jest teraz `StatefulWidget` z `reopen` (z `main.dart`). Po odtworzeniu
  dostaje nowy klucz, więc każdy ekran buduje się od nowa na nowych danych i nic nie trzyma zamkniętej
  bazy. Na starcie są dwie trasy: start + „Stan danych” z komunikatem. Pierwsza wersja z `home` i
  `onGenerateInitialRoutes` padła na asercji Fluttera w debug (zobaczone na emulatorze, poprawione).
- **Weryfikacja migawki bez klasy bazy aplikacji:** `_StagedDatabase` (drift bez tabel, w wersji pliku)
  tylko do odczytu. `GrobingDatabase` próbowałaby migrować plik otwarty tylko do odczytu.
- **Odcisk sprawdzany przed migracją**, liczby rekordów — także po niej (z definicji odcisk po migracji
  się zmienia). Komunikat po odtworzeniu z migracją mówi to wprost.
- **+ nazwa pliku z okna** (`DISPLAY_NAME`) na ekranie: widać, który plik wybrano jako który.
- `MainActivity.kt` bez zmian — drugi kod żądania obsługuje `BackupDocuments.kt`.
- Po błędzie **za** punktem zatwierdzenia (baza już zamknięta) ekran i tak przeładowuje aplikację z
  komunikatem „Odtworzenie zostało przerwane…”; które dane wczytać, rozstrzyga
  `completePendingRestore`.

### For qa
- **Nie kompiluje się `test/support/backup_fakes.dart`:** `FakeDocumentStore` nie ma `openDocument`,
  `documentInfo`, `readFile` (z `maxBytes`, `too_large`) i `freeSpace`. Pozostałe testy ISSUE-008 po tej
  poprawce powinny przejść bez zmian (nowe parametry `GrobingApp`/`StartScreen`/`DataStateScreen` są
  opcjonalne).
- **Haki do testów:** `RestoreService(openDatabase:, schemaVersion:)` (syntetyczna v2);
  `commitRestore` / `completePendingRestore(onStep:)` (`@visibleForTesting`) — rzucenie z `onStep`
  symuluje przerwanie po danym kroku. Nazwy kroków: `marker`, `aside:<item>`, `in:<item>`, `committed`.
- **Stan emulatorów:**
  - `Grobing_Restore` działa (`-no-snapshot-save`), build debug, dane z odtworzenia (wymyślone) i
    kopia skonfigurowana do pliku w `Grobing-dev-009` w Dysku. Na stop #2 potrzebna jest **czysta
    instalacja**;
  - `Medium_Phone` wyłączony (RAM komputera: dwa emulatory naraz to za dużo, wolne ~2,7 GB); build
    debug z kopią w `Grobing-dev-009`.
- **Dla autora (sprzątanie):** folder `Grobing-dev-009` w Dysku (wymyślone dane, zaszyfrowane, hasło
  testowe) do usunięcia po stopie #2, tak jak `Grobing-spike`.
- Hasło testowe na emulatorach: ASCII (`adb input text` nie wpisze polskich znaków). Polskie znaki w
  haśle sprawdza test na hoście.

## Verification
> `qa`, 2026-10-06. Dowody sprawdzone **niezależnie od deklaracji `dev`**: testy napisane od nowa, a nie
> przeniesione ze skryptu próbnego `dev`; złośliwe kopie budowane w testach z prawdziwej kopii (rozpakowanie →
> zmiana → szyfrowanie tym samym kluczem).

### Automated (`flutter test`: 212 passed · `flutter analyze`: no issues · `dart format`: clean)
| AC | Test | Wynik |
|---|---|---|
| AC-1 odcisk = źródło | `test/backup/restore_service_test.dart`: **pełna droga z prawdziwą konfiguracją** (`BackupService.setUp`, scrypt work factor 18) → odtworzenie na świeży telefon: odcisk i liczby = źródło, kroki w kolejności, w katalogu danych tylko `grobing.db`, `media`, `backup.json` (bez sekretu i hasła). Telefon z innymi danymi i zdjęciami ← kopia bez zdjęć: stare zdjęcia nie przeżywają | ✅ |
| AC-1 na ekranie | `test/app/restore_screen_test.dart`: `GrobingApp` → „Stan danych” → „Odtwórz z kopii”; „Odtwórz” nieaktywne do wyboru obu plików i hasła; po odtworzeniu aplikacja otwiera się od nowa na „Stanie danych” z komunikatem i odciskiem odtworzonych danych; „wstecz” prowadzi do startu | ✅ |
| AC-2 odmowy | `restore_service_test.dart`, po jednym teście: złe hasło · plik klucza z innej konfiguracji · „plik klucza” > 64 KiB · plik klucza z work factor 21 · zwykły tekst zamiast `age` · zmieniony bit · ucięty plik · tar z `../`, ze ścieżką absolutną, z dowiązaniem, z nieznanym plikiem · baza dwa razy · SHA-256 zdjęcia ≠ manifest · plik w manifeście, którego nie ma · odcisk ≠ baza · liczby ≠ baza · manifest nie na końcu · uszkodzona baza ze zgodnymi sumami (`integrity_check`) · nowszy schemat · nowszy format. **W każdym:** komunikat bez ścieżek i hasła, odcisk danych w telefonie bez zmian, baza nadal otwarta, bez katalogu tymczasowego i znacznika. Na ekranie: złe hasło → „…nietknięte” | ✅ 19 + 1 |
| AC-2 czytnik tar | `test/backup/tar_reader_test.dart`: zgodność z zapisem (także długa ścieżka z prefiksem, pusty plik, wypełnienie zerami po końcu); odmowa: `..`, ścieżka absolutna, `\`, spacja, znak spoza ASCII, dowiązanie symboliczne i twarde, katalog, nagłówek GNU, zła suma nagłówka, nagłówek nie-ustar, ta sama ścieżka dwa razy, plik i katalog o tej samej nazwie (w obu kolejnościach), archiwum ucięte, bez końca, z danymi po końcu, niezerowe wypełnienie, ścieżka spoza listy, przekroczony budżet — bez zapisu poza katalogiem | ✅ 18 |
| AC-3 starszy schemat | `restore_service_test.dart`: aplikacja w syntetycznej v2 (kolumna `nickname` + krok migracji) odtwarza kopię v1 → `user_version` 2, liczby = źródło, kolumna jest. Migracja, która nie dochodzi do v2 → odmowa „przenieść”, telefon nietknięty | ✅ |
| AC-4 awaria w trakcie podmiany | `test/backup/restore_swap_test.dart`: przerwanie po **każdym** z 8 kroków podmiany → przy następnym starcie nowe dane; przerwanie przed punktem zatwierdzenia (pół znacznika) → stare dane; **przerwanie samego odzyskiwania** po każdym kroku i ponowny start → nowe dane. Zawsze: `backup.json` idzie ze swoimi danymi, dziennik starej bazy (`-journal`, `-wal`) nie zostaje przy nowej, bez resztek. Kopia bez zdjęć czyści katalog zdjęć; zatwierdzenie bez przygotowania → odmowa | ✅ 14 |
| AC-5 limit i miejsce | `restore_service_test.dart`: wolne < 2 × rozmiar + 200 MB → odmowa **zanim przeczytano choćby plik klucza**; dokładnie tyle → odtworzone; rozmiar nieznany → budżet `(wolne − 200 MB) / 2`, plik o bajt większy → odmowa, bez resztek | ✅ |
| D3 | świeży telefon → klucz publiczny z pliku klucza, plik kopii, trwałe uprawnienie; dostawca bez zapisu → nieskonfigurowana, bez `backup.json`; telefon z konfiguracją → bez zmian | ✅ |
| D4 | `restore_screen_test.dart`: telefon z danymi → ostrzeżenie, okno z liczbami (osoby 6, groby 4, cmentarze 2); „Anuluj” → nic nie przeczytano, bez katalogu tymczasowego | ✅ |
| (dostosowane) | `test/support/backup_fakes.dart`: sztuczny Dysk z oknem otwarcia, rozmiarem, budżetem, wolnym miejscem; `restoreServiceIn` | ✅ |

### Release build (APK, `aapt`)
- Uprawnienia: tylko `DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION` (AndroidX), **bez `INTERNET`**.
- `allowBackup=false`, `dataExtractionRules` podpięte. Nowych zależności brak (`pubspec` bez zmian).

### DoD lines specific to Grobing
- **Próbne odtworzenie z kopii:** to jest ta pozycja — testy wyżej oraz stop #2 przez Dysk na
  `Grobing_Restore`.
- **Test migracji:** schemat się nie zmienił (v1). Ścieżka migracji przez odtworzenie sprawdzona
  syntetyczną v2 (AC-3).
- **Źródło faktu:** n/a — pozycja nie zapisuje faktów o rodzinie.
- **Dane rodziny w zmianach:** brak. W trzech repo nie ma `*.db`, `*.age`, `*.tar`, eksportów ani zdjęć;
  testy używają wyłącznie `lib/dev/fictional_data.dart` i bajtów generowanych w teście.

### Manual (stop #2) — **„ok”** (autor, 2026-10-06), sprawdzone na emulatorach
Dwa emulatory naraz nie mieszczą się w pamięci komputera (wolne ~2 GB), więc kroki szły w dwóch
częściach. Krok D4 przeniesiony z `Medium_Phone` na `Grobing_Restore`, który po odtworzeniu ma dane; to
ten sam test bez przełączania emulatorów.
- **Część A — `Medium_Phone`, build debug, czysta instalacja:** wymyślone dane → „Skonfiguruj kopię” z
  hasłem testowym → plik klucza i plik kopii w **Dysku**, folder `Grobing-proba`. Autor: „A gotowe”.
  Stan na emulatorze: `backup.json` wskazuje dostawcę Dysku, ostatnia udana kopia 08:42 UTC, odcisk
  **`cac13dcd1f3fb213`**. Pliki w Dysku autor sprawdził w przeglądarce (krok 6).
- **Część B — `Grobing_Restore`, build release, czysta instalacja** (pusta baza `b91fe9928cef859e`, bez
  przycisku danych wymyślonych): odtworzenie z `Grobing-proba` przez okno otwarcia. Autor: „ok”. Stan na
  emulatorze:
  - komunikat „Odtworzono kopię z dnia 2026-10-06 08:42”, **odcisk `cac13dcd1f3fb213` = `Medium_Phone`**;
  - kopia skonfigurowana (D3).

  **Rozjazd przy pierwszym „ok”:** „Ostatnia udana kopia: jeszcze nie było”, więc krok 6 („Zrób kopię
  teraz”) nie był wykonany, a krok 8 od niego zależy. `qa` zgłosił to i zaproponował dokończenie. Autor
  wykonał oba kroki i odpisał „ok”. Stan po tym: ostatnia udana kopia **08:58**, bez nieudanej próby,
  odcisk bez zmian. Nowa godzina pliku w Dysku: potwierdzenie autora w przeglądarce.
- **Co to dowodzi:** pierwszy zapis do Dysku i pierwsze odtworzenie z Dysku **kodem produkcyjnym** na
  drugim urządzeniu, obejrzane przez człowieka. Po zmianie telefonu kopia zapisuje dalej tym samym
  kluczem do tego samego pliku (D3). Zamyka to uwagę 1 z werdyktu [[ISSUE-008-backup-write]] i uwagę
  `qa` ze SPIKE-003.
- **Czego nie widać w stanie emulatora:** krok 4 (złe hasło) i krok 7 („Anuluj” przy D4). Oba pokrywają
  testy automatyczne (`restore_service_test`, `restore_screen_test`) i smoke check `dev` na emulatorze
  (*Dev report*).

### Verdict (self-check)
**APPROVED** z uwagami. Każde AC ma test happy-path, a AC-2 i AC-4 dodatkowo wszystkie wskazane w
pozycji przypadki. Odtworzenie przez Dysk na drugim urządzeniu obejrzał człowiek, z odciskiem zgodnym ze
źródłem.

**Czego szukałem i nie znalazłem:**
- zmiany danych w telefonie przy którejkolwiek z 20 odmów (odcisk, otwarta baza, brak katalogu
  tymczasowego i znacznika);
- zapisu poza katalogiem tymczasowym przy złośliwym tar (`../`, ścieżka absolutna, dowiązania);
- stanu „ani starych, ani nowych” po przerwaniu podmiany w dowolnym kroku, także w trakcie odzyskiwania;
- dziennika starej bazy obok nowej;
- ścieżek, hasła albo klucza prywatnego w komunikatach i w `backup.json`;
- uprawnienia `INTERNET`, `allowBackup=true` i nowych zależności w buildzie release;
- danych rodziny w zmianach trzech repo.

**Uwagi, które nie blokują:**
1. **Środowisko:** `Medium_Phone` wstał ze snapshotu z 2026-10-05, ze starym buildem sprzed ISSUE-008
   (`ALLOW_BACKUP` we flagach pakietu). Na `Grobing_Restore` menedżer pakietów zgubił aplikację
   zainstalowaną przed restartem. Przed stopem #2 zawsze sprawdzać, który build jest zainstalowany.
2. Dysk wysyła plik z opóźnieniem: pliki `dev` pojawiły się na drugim urządzeniu po kilkunastu
   minutach (ADR-004: „zapisane” ≠ „w chmurze”). Instrukcja w aplikacji mówi o pustym folderze, ale nie
   o tym, że świeżej kopii może jeszcze nie być w chmurze — do [[NT-007-hand-over-note]].
3. W `grobing-kopia.age` w trzech folderach Dysku (`Grobing-spike`, `Grobing-dev-009`,
   `Grobing-proba`) wyszukiwarka okna pokazuje kilka plików o tej samej nazwie. Data w komunikacie
   po odtworzeniu pozwala je odróżnić. Dwa ostatnie foldery są do usunięcia przez autora (wymyślone
   dane, hasła testowe).
4. `typedef DatabaseOpener` w `restore_service.dart` ma tę samą nazwę co typ z `drift`. Plik, który
   importuje oba, musi użyć `show`/`hide` (tak robi `test/support/backup_fakes.dart`). Kosmetyka dla `dev`.
5. Czasu odtworzenia w buildzie release (scrypt) nie mierzyłem; w debug ~21 s dla 70 KB.
6. Tekst „Zapisana w Dysku na telefonie” stoi także przy pliku w Pobranych (znane z ISSUE-008, uwaga 3).
