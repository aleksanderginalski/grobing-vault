---
title: "NFR-003 — A schema change ships with a migration tested from the previous version"
type: non-functional-requirement
status: draft
epic: ["[[EPIC-001-zabezpiecz-i-przepisz]]", "[[EPIC-002-wizyta]]", "[[EPIC-003-zrozumienie]]"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §Architecture → Sufficiency pass A1 · DoD ISSUE"
created: 2026-10-05
updated: 2026-10-08
---

# NFR-003 — Migracje schematu

## Requirement
Każda zmiana schematu bazy wychodzi **z migracją przetestowaną z poprzedniej wersji**. Dane są
niezastępowalne i będą żyć latami — aktualizacja aplikacji ze złą migracją **jest** utratą danych (A1).

| | |
|---|---|
| **Metric** | zmiany schematu bez testu migracji z poprzedniej wersji |
| **Target** | **zero** |
| **Method** | test migracji (`qa`): baza poprzedniej wersji z **wymyślonymi** danymi → migracja → dane kompletne |
| **Verification trigger** | każda pozycja zmieniająca schemat (linia DoD ISSUE) |

## Notes
- Dotyczy każdego EPIC-a, który dokłada pole albo encję — stąd trzy EPIC-i w `epic:`.
- Razem z [[NFR-002-odtworzenie-na-nowym-telefonie]]: kopia sprzed migracji musi dać się odtworzyć w
  nowej wersji. ✅ **Rozstrzygnięte 2026-10-05** ([[ADR-004-backup-format-encryption-destination]], pkt 5;
  zmierzone w [[SPIKE-003-backup-and-restore]], krok 5): odtworzenie przepuszcza starszą kopię przez
  **zwykłe migracje** aplikacji, a kopię z nowszego schematu odrzuca. Wynika z tego, że **test migracji
  z tej NFR obejmuje też odtworzenie kopii**: ta sama ścieżka kodu.
- **2026-10-06 — pierwsza prawdziwa migracja** (v1→v2, [[ISSUE-011-schema-v2-assertions]]). Z niej dwie
  zasady dla każdej następnej (README `grobing-code` → *Baza danych*):
  - **krok dodaje i przebudowuje, ale nie usuwa tabel ani wierszy**, bo odtworzenie starszej kopii
    sprawdza po migracji każdą tabelę z jej manifestu i liczbę wierszy;
  - **wszystkie kroki i `user_version` w jednej transakcji**: przerwana aktualizacja zostawia starą wersję
    całą.

  Sprawdzone na emulatorze: aktualizacja przez wgranie nowej wersji na starą, bez odinstalowania.
- **2026-10-07 — druga migracja** (v2→v3, [[ISSUE-012-transcribe-grave-screen]]): opcjonalna nazwa grobu, sam
  `addColumn`. Test z danymi v2→v3 i wygenerowane v1→v3; na emulatorze łańcuch v1→v3. Kopia v2 odtwarza się w
  aplikacji v3. **Kopia zamawia się zaraz po migracji** (retro 1, R6): start pyta o kopię dopiero po otwarciu bazy,
  bo migracja zmienia plik, ale nie zgłasza zmian. Test na hoście pokazuje lukę sprzed poprawki i jej zamknięcie.
- **2026-10-07 — trzecia migracja** (v3→v4, [[ISSUE-017-person-photos]], [[ADR-009-person-photos-record-and-link]]):
  - nowa tabela łączy `person_media`; zdjęcia osób z v3 stają się łączami w kolejności `id`;
  - przebudowa `media` bez `person_id` (`TableMigration`, te same wiersze i `id` — odtworzenie kopii v3 liczy wiersze);
  - na końcu `PRAGMA foreign_key_check`.

  Test z danymi v3→v4 i wygenerowane v1→v4, v2→v4. Kopia v3 ze zdjęciami osób odtwarza się w v4 (test na prawdziwym
  archiwum). Na emulatorze build v4 wgrany na v3 z danymi: liczby wierszy bez zmian, kopia w tle po migracji.
- **2026-10-07 — czwarta migracja** (v4→v5, [[ISSUE-018-profile-photo-crop]], [[ADR-010-profile-photo-crop-pixels]]): kadr
  profilowego przy łączu, cztery `addColumn` w `person_media` — bez zmiany wierszy i bez przebudowy. Test z danymi v4→v5
  (łącza i pozycje bez zmian, kolumny kadru puste) i wygenerowane v1…v4→v5. Kopia v4 odtwarza się w v5 (test). Na dwóch
  emulatorach build v5 wgrany na starsze dane: liczby wierszy bez zmian, kopia w tle przeszła na v5.
- **2026-10-08 — piąta migracja** (v5→v6, [[ISSUE-019-family-relations]], [[ADR-011-relation-claims-family-and-child-link]]):
  twierdzenia przy rodzinie i łączu dziecka. Przebudowa `family_children` (stary `rowid` to `id`) i `assertions` (nowy
  `CHECK`), `PRAGMA foreign_key_check` na końcu. **Pierwsza migracja, która świadomie nie dopisuje wierszy do istniejącej
  tabeli:** twierdzenia dla rodzin sprzed v6 zmieniłyby liczbę wierszy `assertions` i odtworzenie kopii v5 z rodzinami
  by odmówiło. Zasada dla kolejnych: **krok dopisuje wiersze tylko do tabeli, której starsza kopia nie ma.** Test z danymi
  v5→v6 i wygenerowane v1…v5→v6; kopia v5 z rodzinami odtwarza się w v6 (test). Na dwóch emulatorach build v6 wgrany na
  v5: liczby wierszy bez zmian.
