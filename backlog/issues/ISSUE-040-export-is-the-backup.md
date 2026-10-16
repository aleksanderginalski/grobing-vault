---
title: "ISSUE-040 — Export is the backup: a backup with today's schema opens on the PC with the official age and plain tar, and the database checks out against the manifest without Grobing's code; the „Eksport dla rodziny” row and the export line of the hand-over note leave the app"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-006-eksport-dla-rodziny]]"
depends-on: "[[ISSUE-008-backup-write]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-16
verdict-reviewer: self-check
source: "rozpisanie US-006 (`docs` w auto-flow po `pm`, 2026-10-16) · decyzja autora na stopie #1 pierwszego planu (2026-10-16): eksport = kopia, bez HTML i PDF → [[ADR-018-export-is-the-backup]] · bramka zgodności [[ISSUE-008-backup-write]] → *Compatibility gate (AC-3)* · `04_ARCHITECTURE/backup-format.md`"
created: 2026-10-16
updated: 2026-10-16
---

# ISSUE-040 — Eksport to kopia

> Z rozpisania [[US-006-eksport-dla-rodziny]] (`docs` w auto-flow, 2026-10-16, przed `ui`). **Pierwszy plan tej pozycji — eksport HTML + PDF/A dla
> rodziny — autor wycofał na stopie #1:** *„tak naprawdę nie potrzebuję HTML i PDF-a, wystarczy mi możliwość eksportowania. Gdybym kiedyś chciał
> wykorzystać tę bazę w innym produkcie. W skrócie — nie zależy mi na estetyce, a na zachowaniu danych”*; na rekomendację „kopia jako eksport” —
> *„tak, wystarczy”*. Decyzja: [[ADR-018-export-is-the-backup]]. US-006 przepisana pod tę decyzję.
> **Pozycja zmienia ekran** (usuwa wiersz z ustawień i zdanie z notki) → `ui` aktualizuje [[ustawienia]]; nowego ekranu nie ma.

## What to build
1. **Sprawdzenie, że dane wychodzą poza aplikację** (US-006 AC-1): kopia zrobiona aplikacją z dzisiejszym schematem, na wymyślonych danych → PC →
   oficjalne `age` → zwykły `tar` → baza i zdjęcia sprawdzone **narzędziem niezależnym od kodu Grobing** — jak bramka [[ISSUE-008-backup-write]], która
   była na schemacie v1, a dziś jest v12.
2. **Opis wystarcza bez Grobing** (US-006 AC-2): każda tabela w `grobing.db` z kopii ma opis w `data-model.md` albo `backup-format.md`; braki dopisane.
3. **Eksport znika z aplikacji** (US-006 AC-3): wiersz „Eksport dla rodziny” i zaślepka w ustawieniach; punkt (5) „gdzie leży eksport dla rodziny” w
   ekranie notki przekazania ([[ustawienia]] 6a).

## Acceptance Criteria
- [ ] **US-006 AC-1 — dane poza aplikacją.** *Given* kopia zrobiona aplikacją z dzisiejszym schematem *When* odszyfrowana na PC oficjalnym `age` i
      rozpakowana zwykłym `tar` *Then* są `grobing.db`, `media/…` i `manifest.json`; baza przechodzi `PRAGMA integrity_check`, `user_version` i liczba
      wierszy każdej tabeli = manifest, rozmiar i SHA-256 każdego pliku = manifest — sprawdzone bez kodu Grobing.
- [ ] **US-006 AC-2 — opis bez Grobing.** *Then* każda tabela bazy z kopii ma opis w `04_ARCHITECTURE/` (`data-model.md` albo `backup-format.md`).
- [ ] **US-006 AC-3 — bez osobnego eksportu.** *When* otwieram ustawienia *Then* nie ma wiersza „Eksport dla rodziny”, a notka przekazania nie mówi o
      eksporcie.

## Out of scope
- Eksport HTML i PDF dla rodziny — wycofany ([[ADR-018-export-is-the-backup]]).
- GEDCOM 7 (C2) — gdy pojawi się konkretny produkt docelowy (ADR-018 → *Follow-ups*).
- Jawny eksport bez szyfrowania — odrzucony w ADR-018.
- Treść papierowej notki przekazania — [[NT-007-hand-over-note]] (poza kodem; autor przechodzi drogę `age` z hasłem w terminalu sam, przy notce).
- Usunięcie kolumny `persons.is_living` — zostaje w schemacie nieużywana, bez migracji (ADR-018 → *Consequences*).

## Notes — z pierwszego planu (HTML + PDF/A), na wypadek powrotu tematu
- `persons.is_living` ma domyślnie „nie żyje”, żaden ekran go nie ustawia, a kod czyta je tylko w `person_view.dart` — każdy eksport dla innych musi
  liczyć, kto może żyć (kanon: Gramps `probably_alive`, zasada 110 lat FamilySearch), a nie czytać to pole.
- Biblioteka `pdf` 3.13.x wymaga Darta ≥ 3.12; przypięty Flutter 3.41.1 ma Darta 3.11.0 — ostatnia zgodna to 3.12.0 (PDF/A-3b bez adnotacji).
- Makieta pliku dla rodziny (`eksport-040.html`) została w katalogu tymczasowym sesji `cbd907af-…` — do kosza razem z resztą katalogów sesji.

## Implementation plan
> `planning`, 2026-10-16. Specyfikacja (`ui`, przed planem): [[ustawienia]] v3 — element 5 usunięty, 6a z listą 1–4, D10. Decyzja: [[ADR-018-export-is-the-backup]].

### Stop #1 (2026-10-16) — autor: „tak, wystarczy”
Na rekomendację „kopia jest eksportem; jedno sprawdzenie odszyfrowania na PC; wiersz „Eksport dla rodziny” z zaślepką znika z ustawień”. **Skutek
tej samej decyzji, nazwany tu wprost:** punkt (5) notki przekazania w aplikacji („Gdzie leży eksport dla rodziny…”) też znika — inaczej aplikacja
wskazywałaby rodzinie plik, którego nie ma. Nowego ekranu nie ma, więc stop #2 dla autora jest pusty (kroki oddane agentowi, `DEFINITION_OF_DONE.md`).

### Prior art
- Bramka zgodności [[ISSUE-008-backup-write]] → *Compatibility gate (AC-3)*: oficjalne `age` v1.3.2 z `age-plugin-batchpass` z tej samej dystrybucji
  (hasło bez terminala), `tar` Windows, Python `sqlite3` + `hashlib` niezależnie od kodu Grobing. Wtedy: schemat v1, 2 pliki `media/`. Dziś: schemat v12.
- README `grobing-code` → *Otwarcie bez Grobing* (trzy polecenia) i `04_ARCHITECTURE/backup-format.md` — opis dla kogoś bez Grobing.
- Kanon formatu: LoC RFS → Datasets — SQLite *Preferred* ([[ADR-018-export-is-the-backup]]).
- Z kodu: wiersz — `lib/app/settings/settings_screen.dart` (sekcja „Dla rodziny”); zaślepka — `export_placeholder_screen.dart`; notka —
  `hand_over_note_screen.dart` (`_points`, 5 pozycji); test — `test/app/skeleton_test.dart` (lista nagłówków i wierszy, przejście do zaślepki).
  Na PC nie ma `age` ani `sqlite3` w `PATH`; jest `tar`, Python z `sqlite3` 3.50.4 i Java.

### Scope — files (`{code}`)
| Plik | Zmiana |
|---|---|
| `lib/app/settings/settings_screen.dart` | bez wiersza „Eksport dla rodziny” i importu zaślepki; sekcja „Dla rodziny” z jednym wierszem „Notka przekazania” |
| `lib/app/settings/export_placeholder_screen.dart` | usunięty |
| `lib/app/settings/hand_over_note_screen.dart` | `_points` bez punktu o eksporcie (4 punkty); komentarz z odsyłaczem do ADR-018 |
| `README.md` | jeśli gdzieś mówi o eksporcie HTML/PDF — zdanie, że eksportem jest kopia (ADR-018) |
| `test/app/skeleton_test.dart` | `qa` — niżej |

**Bez nowej zależności, sieci i uprawnień. Warstwa danych bez zmian** (schemat ten sam, `is_living` zostaje): bez testu migracji; próbne otwarcie kopii
**jest** treścią pozycji (AC-1).

### Steps for `dev`
1. Wiersz, zaślepka, notka — jak w tabeli; `dart format`, `flutter analyze`.
2. **Przejście AC-3 na emulatorze** (`Grobing_Restore`, build profile): ustawienia bez wiersza, notka z czterema punktami, tekst 200% na 360 dp (zrzuty).

### Acceptance → tests (`qa`)
| AC | Test / sprawdzenie |
|---|---|
| AC-1 | **Na emulatorze i PC, bez kodu Grobing w sprawdzeniu:** `Grobing_Restore` — wymyślona rodzina (107 osób) + jedno wymyślone zdjęcie osoby (rysunek wgrany przez `adb`, żeby `media/` nie było puste); „Skonfiguruj kopię” z **nowym hasłem testowym**, zapis do Pobranych → `adb pull` do katalogu tymczasowego sesji → oficjalne `age` v1.3.2 i `age-plugin-batchpass` (pobrane z wydania na GitHubie do katalogu tymczasowego, nie do repo) → `tar -xf` → skrypt Pythona (plik w katalogu tymczasowym, `python -I`): `integrity_check` = `ok`, `user_version` = `schema_version`, liczba wierszy każdej tabeli = `record_counts`, rozmiar i SHA-256 każdego pliku = `files[]`. Dodatkowo `dart run tool/fingerprint.dart` = odcisk z ekranu „Stan danych” |
| AC-2 | lista tabel z `sqlite_master` kopii ↔ `data-model.md` i `backup-format.md`: każda tabela ma opis; brak → `docs` dopisuje przy zamknięciu |
| AC-3 | widget (`skeleton_test.dart`): w ustawieniach są „Dla rodziny” i „Notka przekazania”, **nie ma** „Eksport dla rodziny”; notka ma cztery punkty i nie ma słowa „eksport”; reszta listy i przejścia bez zmian. Pełny `flutter test` zielony |
| Regresja | ustawienia, notka, „Stan danych”, kopia — dotychczasowe testy bez zmian poza usuniętym przejściem do zaślepki |

### Manual verification — agent na emulatorze (`Grobing_Restore`; kroki oddane agentowi — bez nowego ekranu)
1. Ustawienia: bez „Eksport dla rodziny”, sekcja „Dla rodziny” z notką; notka — 4 punkty (zrzut; tekst 200% na 360 dp).
2. AC-1 jak w tabeli — wynik skryptu i odcisk w *Verification*.
3. Pliki kopii i klucza z wymyślonymi danymi zostają tylko w katalogu tymczasowym sesji (`*.age`, `*.tar`, `*.db` — strażnik i `.gitignore` i tak blokują repo).

### Manual verification — autor: odczucie
Brak (bez nowego ekranu). Droga z hasłem wpisanym w terminalu (`age -d -i …`) zostaje przy [[NT-007-hand-over-note]] → *Input from US-001 closure* — przy
pisaniu notki.

## Dev report
- `settings_screen.dart`: bez wiersza „Eksport dla rodziny” i importu zaślepki, komentarz z odsyłaczem do ADR-018; `export_placeholder_screen.dart` usunięty;
  `hand_over_note_screen.dart`: cztery punkty, komentarz o ADR-018. README bez zmian — nie mówił o eksporcie HTML/PDF (tylko „ani eksportów” w zakazie
  danych rodziny i „eksport jako `EVEN`” przy GEDCOM).
- **Przejście AC-3 na emulatorze** (`Grobing_Restore`, build profile `x86_64`, `FRAME_LOG`): ustawienia bez wiersza, sekcja „Dla rodziny” z notką; notka z
  czterema punktami; tekst 200% na 360 dp — lista i notka przewijają się, nic nie ucięte (zrzuty `shots\settings-100`, `note-100`, `settings-200`,
  `note-200` w katalogu tymczasowym sesji `cbd907af-…`).
- **Found:** `home_screen_test.dart` (AC-5 ISSUE-022) przestał trafiać w „Stan danych” — o jeden wiersz krótsza lista ustawień zbudowała wiersz w pamięci
  listy, ale poza ekranem, więc `scrollUntilVisible` nie przewinął, a dotknięcie poszło obok. Poprawka w teście: `ensureVisible` przed dotknięciem.

## Verification
> `qa`, 2026-10-16. Kroki oddane agentowi (pozycja bez nowego ekranu — `DEFINITION_OF_DONE.md`).

### Rytuał (WZ-024)
`dart format` — bez zmian · `flutter analyze` — 0 problemów · `flutter test --timeout 120s` — **773 zielone**.

### AC-1 — dane poza aplikacją: oficjalne `age` v1.3.2 na PC, bez kodu Grobing
- **Kopia z aplikacji:** `Grobing_Restore`, wymyślona rodzina (107 osób) + jedno wymyślone zdjęcie osoby (obraz testowy `ffmpeg testsrc`, wgrany przez `adb`,
  wybrany systemowym oknem zdjęć — profilowe Mateusza); „Skonfiguruj kopię” z **nowym hasłem testowym** (15 znaków, oba pola po 15 kropek), zapis do Pobranych
  jako `grobing-klucz-040.age` (366 B) i `grobing-kopia-040.age` (185 064 B); ustawienia: „Ostatnia udana kopia · dziś, 11:11 · Pobrane”; „Stan danych”:
  schemat 12, odcisk **`d425b2b3242343c7`**.
- **PC:** `age-v1.3.2-windows-amd64.zip` z wydania na GitHubie (katalog tymczasowy sesji): plik klucza → `age -d -j batchpass` (hasło ze zmiennej
  `AGE_PASSPHRASE`, bo sesja nie ma terminala — jak bramka [[ISSUE-008-backup-write]]) → `# created`, `# public key`, jedna linia `AGE-SECRET-KEY-1`; kopia →
  `age -d -i` → `tar -xf` (Git Bash): `grobing.db` (139 264 B), `media/zdjecia/…jpg` (41 953 B), `manifest.json`.
- **Python `sqlite3` + `hashlib`, niezależnie od kodu Grobing** (skrypt w katalogu tymczasowym): `integrity_check` = `ok`; `user_version` 12 = `schema_version`;
  14 tabel = `record_counts` i liczba wierszy każdej = manifest (m.in. `persons` 107, `families` 38, `family_partners` 76, `family_children` 67, `events` 177,
  `assertions` 282, `media` 1, `person_media` 1 — te same liczby co ekran „Stan danych”); rozmiar i SHA-256 obu plików = `files[]`; na dysku nie ma plików spoza
  manifestu. **Wynik: OK.**
- `dart run tool/fingerprint.dart` na rozpakowanym katalogu: odcisk **`d425b2b3242343c7` = ekran** i = manifest; schemat, liczby, pliki — OK.
- **Czego to nie sprawdza:** drogi z hasłem wpisanym w terminalu (`age -d -i grobing-klucz.age …` pyta o hasło) — zostaje przy [[NT-007-hand-over-note]];
  cmentarzy, grobów, pinezek i kwater w kopii — wymyślona rodzina ich nie ma (0 wierszy; ich odtworzenie z kopii sprawdziły [[ISSUE-027-cemetery-map-plan-photo-states]],
  [[ISSUE-028-cemetery-sectors]] i [[ISSUE-029-pin-on-site-gps]] z identycznym odciskiem).

### AC-2 — opis bez Grobing
Lista 14 tabel z `sqlite_master` ↔ `04_ARCHITECTURE/`: encje były opisane pojęciowo, ale **`events`, `family_partners` i `family_children` nie miały swoich nazw
nigdzie**, a pozostałe tylko w historii schematu. Dopisane: `data-model.md` → *Tables in `grobing.db` — schema v12* — tabela → encja → kolumny; sprawdzone z
`PRAGMA table_info` bazy z kopii (14 z 14).

### AC-3 — bez osobnego eksportu
Widget (`skeleton_test.dart`): „Dla rodziny” i „Notka przekazania” są, „Eksport dla rodziny” i „HTML i PDF” — nie; notka ma „4.”, nie ma „5.” ani słowa
„eksport”. Emulator — *Dev report*. Kod: nic nie importuje `export_placeholder_screen.dart`.

### Zero danych rodziny w zmianach
Kod: usunięte linie i jeden komentarz; testy — teksty interfejsu. Vault: wymyślone przykłady („Ewa Wymyślona”). Pliki `*.age`, `*.tar`, `*.db`, obraz testowy i
zrzuty tylko w katalogu tymczasowym sesji.

### Werdykt
**APPROVED** (self-check). Uwaga: droga z hasłem w terminalu — przy NT-007; reszta kopii z grobami i pinezkami sprawdzona w poprzednich pozycjach.
