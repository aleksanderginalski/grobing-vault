---
title: "ADR-004 — Backup: format, phone-side encryption, destination; export formats"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[SPIKE-003-backup-and-restore]]"
source: "PROJECT_BRIEF §Security → The off-phone copy · §Architecture → shape · Sufficiency A4 · §5 M8"
created: 2026-10-05
updated: 2026-10-05
---

# ADR-004 — Kopia: format, szyfrowanie, miejsce

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-05. Kierunek wybrał autor (§Security). Mechanizm zamknął
[[SPIKE-003-backup-and-restore]]: odtworzenie wykonane naprawdę, przez Dysk, na drugim emulatorze.
Pomiary M1-M7 i liczby są w sekcji *Findings* spike'a i tam zostają (jedna liczba, jeden dom).

## Context
- „Przeżywa autora i aplikację” (brief §2) → kopia poza telefonem **ze sprawdzonym odtworzeniem** (M8, G1)
  i eksport czytelny bez aplikacji.
- **Dwa artefakty o przeciwnych własnościach** (§Security): kopia — pełna, automatyczna, **zaszyfrowana**,
  sprawdzona odtworzeniem; eksport — **jawny** (czytelność jest celem), trwały, offline u rodziny.
- Hipoteza prawna: wyłączenie domowe RODO jest najmocniejsze, gdy dostawca chmury trzyma tylko szyfrogram
  ([[NT-003-verify-household-exemption]]).
- Androidowa automatyczna kopia jest **domyślnie włączona** i ma limit **25 MB na aplikację**
  ([Android docs](https://developer.android.com/identity/data/autobackup)). Od Androida 12
  `allowBackup="false"` **nie** wyłącza transferu między urządzeniami (D2D)
  ([Behavior changes: Android 12](https://developer.android.com/about/versions/12/behavior-changes-12)).
- **Zmierzone w spike'u (dowody: SPIKE-003 → *Findings*):**
  - Dysk Google **nie** pojawia się w systemowym oknie wyboru *folderu*, tylko w oknie zapisu i otwarcia
    *pliku*. Przyjmuje trwałe uprawnienie do odczytu i zapisu, które działa w tle i przeżywa restart.
  - Obie implementacje `age` w Darcie odpadły: `dartage` wymaga nowszego Darta niż przypięty (ADR-002),
    a `dage` ma dwa błędy zgodności, z których jeden robi kopie nie do odtworzenia.
  - Scrypt (koszt hasła) jest drogi w czystym Darcie; szyfrowanie samego pliku tanie.

## Decision
**Kierunek (autor, 2026-10-05):** automatyczna kopia **szyfrowana w telefonie** przed wysłaniem do
folderu we własnej chmurze autora **+** okresowy jawny eksport przechowywany offline przez rodzinę.

**Mechanizm (SPIKE-003, 2026-10-05):**
1. **Miejsce — jeden plik w Dysku autora przez systemowe okno zapisu pliku** (`ACTION_CREATE_DOCUMENT`),
   z trwałym uprawnieniem do odczytu i zapisu. Każda kopia nadpisuje ten plik w trybie `"wt"`.
   **Bez kluczy API i sekretów OAuth w aplikacji**, a aplikacja sama nie potrzebuje dostępu do sieci,
   bo wysyła aplikacja Dysku.
2. **Format — `age` v1** (standard, [age-encryption.org](https://age-encryption.org)) z archiwum `tar`
   zawierającym:
   - `manifest.json`: `format_version`, `schema_version`, liczby rekordów i SHA-256 każdego pliku;
   - migawkę SQLite (`VACUUM INTO`);
   - `media/*`.

   Kopię da się otworzyć **bez Grobing**: oficjalnym `age` + zwykłym `tar` + dowolnym SQLite.
   **Implementacja: własny moduł formatu** na prymitywach z `cryptography` i `pointycastle`, z testem
   zgodności z oficjalnym CLI jako bramką `qa` (`dage` i `dartage` odrzucone, *Context*).
3. **Klucz — odbiorca X25519 (klucz publiczny w aplikacji), tożsamość zaszyfrowana hasłem.** Klucz
   publiczny nie jest sekretem, więc **kopia w tle nie potrzebuje hasła ani bezpiecznego magazynu**
   (`flutter_secure_storage` niepotrzebne). Tożsamość (klucz prywatny) jest zaszyfrowana hasłem (scrypt,
   work factor 18) w osobnym pliku obok kopii. To wzorzec, który zaleca dokumentacja oficjalnego `age`
   (*passphrase-encrypted identity files*). **Odtworzenie = plik klucza + hasło + plik kopii.**
4. **`allowBackup="false"` i `dataExtractionRules`** wykluczające wszystko w `<cloud-backup>` oraz
   `<device-transfer>`. Jedna droga na nowy telefon: nasza sprawdzona kopia.
5. **Kopia sprzed migracji schematu:** odtworzenie przepuszcza starszą kopię przez **zwykłe migracje
   aplikacji** ([[NFR-003-migracje-schematu]]). Kopię z nowszego schematu odrzuca z prośbą o
   aktualizację.
6. **Walidacja przed nadpisaniem czegokolwiek** (floor: walidacja wejścia na granicy zaufania):
   - odszyfrowanie do katalogu tymczasowego;
   - tar tylko ze zwykłymi plikami i bezpiecznymi ścieżkami;
   - lista plików i SHA-256 zgodne z manifestem;
   - `PRAGMA integrity_check`;
   - `user_version` = manifest;
   - liczby rekordów zgodne, także po migracji.

   Dopiero wtedy podmiana danych.

**Eksport (A4):** samodzielny HTML + PDF, bez formatu specyficznego dla aplikacji; nazwy ze znakami
specjalnymi escapowane (§Security, output encoding). *Nie był przedmiotem spike'a; decyzja z kick-offu
bez zmian.*

## Options considered

| Option | Pros | Cons | Why (not) chosen |
|---|---|---|---|
| **Jeden plik w Dysku przez okno zapisu pliku + `age` do klucza publicznego, tożsamość zaszyfrowana hasłem** | automatyczna bez sekretu w telefonie; chmura trzyma tylko szyfrogram; czytelna bez aplikacji (standard); bez OAuth | **każda kopia wysyła całość**; utracony plik klucza albo hasło = utracona kopia | **wybrane** (SPIKE-003) |
| Folder w Dysku przez okno wyboru folderu (kopia przyrostowa: tylko nowe zdjęcia) | mniej wysyłania | **Dysk nie pojawia się w tym oknie** (zmierzone, M1) | niewykonalne |
| Ten sam plik, ale hasło w bezpiecznym magazynie (`age` scrypt przy każdej kopii) | odtworzenie z samego hasła, bez pliku klucza | sekret w telefonie; scrypt przy **każdej** kopii w tle kosztuje sekundy i setki MB pamięci (zmierzone, M4) | rejected |
| Dysk przez REST API z logowaniem Google (OAuth) | kopia przyrostowa możliwa | konfiguracja OAuth, uprawnienia do Dysku w aplikacji, zależność od API Google; spike pokazał, że nie jest potrzebne | rejected |
| Własna koperta szyfrująca (np. Argon2id + AES-GCM) zamiast `age` | pełna kontrola | format znany tylko Grobing — odtworzenie zależy od aplikacji, która umiera pierwsza | rejected (był fallbackiem D2, niepotrzebny) |
| Tylko plik eksportu kopiowany ręcznie na PC / USB | brak strony trzeciej | zależy od pamiętania — ręczne umiera, gdy brak czasu | rejected |
| Sama androidowa automatyczna kopia | automatyczna, szyfrowana end-to-end od Androida 9 | limit 25 MB → **cicho niepełna** ze zdjęciami | rejected |

## Consequences
- **Positive:**
  - [[NFR-002-odtworzenie-na-nowym-telefonie]] ma mechanizm sprawdzony odtworzeniem na drugim urządzeniu;
  - [[NFR-005-dane-nie-opuszczaja-telefonu]]: jedyny kanał wychodzący z danymi rodziny jest zaszyfrowany,
    a kanały Androida (kopia w chmurze, D2D) są zamknięte świadomie;
  - kopia przeżywa aplikację, bo jest w standardowym formacie.
- **Negative / trade-offs:**
  - **dwa pojedyncze punkty awarii:** hasło **i** plik klucza. Oba muszą żyć poza tą samą chmurą,
    fizycznie ([[NT-007-hand-over-note]]);
  - pełna kopia przy każdym zapisie (rośnie ze zdjęciami);
  - **„zapisane” ≠ „w chmurze”:** aplikacja widzi tylko, że Dysk przyjął plik, nie że go wysłał;
  - termin kopii w tle wyznacza Android, nie aplikacja (zmierzone: od ~1 min do > 44 min);
  - własny moduł kryptograficzny do utrzymania (mały, za bramką zgodności z oficjalnym CLI).
- **Follow-ups:**
  - [[SPIKE-003-backup-and-restore]] **poprzedza masowe przepisywanie** (MD2) — ✅ spike zamknięty
    2026-10-05; produkcyjna funkcja kopii to pozycja z rozpisania [[EPIC-001-zabezpiecz-i-przepisz]].
  - ✅ **2026-10-05 — kopia sprzed migracji schematu** (było ⚠️ OPEN): zmierzone w spike'u, krok 5. Kopia
    v1 odtworzona w aplikacji v2 przeszła migrację z identycznym odciskiem danych; kopia v2 w aplikacji v1
    odrzucona. Decyzja w pkt 5 wyżej.
  - ✅ **2026-10-06 — zamknięte w kodzie** ([[ISSUE-008-backup-write]]; M7 powtórzone na buildzie release:
    kopia Androida *„Backup is not allowed"*, D2D odrzucone). Było: ⚠️ **Przed pierwszymi prawdziwymi
    danymi:** `grobing-code` ma dziś **domyślne `allowBackup=true`**
    i brak `dataExtractionRules`. Zmierzone na `com.grobing.app`: kopia Androida i D2D przechodzą.
    Pozycja produkcyjna kopii wprowadza pkt 4.
  - Pozycja produkcyjna dostaje z uwag `qa` (SPIKE-003 → *Verification*):
    - odzyskanie stanu po awarii w trakcie podmiany danych (dwa `rename` nie są atomowe);
    - limit rozmiaru i sprawdzenie wolnego miejsca przed rozpakowaniem kopii;
    - widoczne w aplikacji „ostatnia udana kopia: kiedy” — ✅ 2026-10-06, [[ISSUE-008-backup-write]];
    - instrukcję odtworzenia: na świeżym telefonie folder Dysku w oknie systemowym bywa pusty, a pliki
      znajduje wyszukiwarka okna.
  - **2026-10-05 — pozycja produkcyjna kopii** to [[US-001-kopia-z-odtworzeniem]]:
    [[ISSUE-007-data-layer]] (baza, której kopia potrzebuje) → [[ISSUE-008-backup-write]] (pkt 1-4) →
    [[ISSUE-009-restore]] (pkt 5-6 i uwagi `qa`).
  - **2026-10-06 — format v1 przypięty** w `04_ARCHITECTURE/backup-format.md` ([[ISSUE-008-backup-write]],
    D2). Pkt 2 bez zmian; doszły szczegóły: manifest na końcu archiwum (sumy w tym samym przebiegu co
    zapis) i trzy pola ponad listę z pkt 2 — `created_at`, `data_fingerprint`, `size` każdego pliku.
    Własny moduł `age` przeszedł 92 oficjalne wektory C2SP i bramkę zgodności z CLI w obie strony.
  - **2026-10-06 — kopia w tle** wydzielona do [[ISSUE-010-background-backup]] (D1 ISSUE-008).
