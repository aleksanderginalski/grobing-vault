---
title: "ADR-009 — People's photos: the photo as a record, a person's link to it with an order (schema v4)"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-017-person-photos]]"
source: "ISSUE-017 → Implementation plan (Prior art, D1, F2–F4), stop #1 (author: „D1 — ok”) · GEDCOM 7.0 (MULTIMEDIA_RECORD, MULTIMEDIA_LINK, „the first is the most-preferred value”) · grobing-code restore_service.dart (_migrate: every table and row count of the backup kept) · ADR-008"
created: 2026-10-07
updated: 2026-10-07
---

# ADR-009 — Zdjęcia osób: zdjęcie jako rekord, łącze osoby z kolejnością

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-07. Autor przyjął D1 na stopie #1 [[ISSUE-017-person-photos]] („D1 — ok”). Wdrożone i sprawdzone
w tej samej pozycji (test migracji z danymi F2, odtworzenie kopii v3 w v4 F3, migracja na emulatorze).

## Context
- **Decyzja autora (stop #1 ISSUE-016):** *„osoby chciałbym, aby miały «swoją bazę zdjęć» (lub dzieloną, jeżeli na
  zdjęciu jest kilka osób) i możliwość wybierania z nich «profilowego»”*.
- Schemat v3: wiersz `media` ma jednego właściciela, osobę albo grób (`CHECK`). Jedno zdjęcie u kilku osób znaczyłoby
  kilka plików albo kilka wierszy z tą samą ścieżką.
- **Kanon — [GEDCOM 7.0](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html)** (odczyt 2026-10-07):
  - zdjęcie to `MULTIMEDIA_RECORD`, a osoba ma do niego łącze `OBJE`;
  - *„the first is the most-preferred value”*, więc profilowe = pierwsze łącze osoby;
  - gramatyka łącza (`MULTIMEDIA_LINK`) ma tylko `CROP` (TOP, LEFT, HEIGHT, WIDTH) i `TITL`, **bez `SOUR`**. Wycinek
    twarzy i podpis należą do łącza, a nie do zdjęcia; łącze nie ma źródła.
- **Ograniczenie z kodu:** odtworzenie starszej kopii (`restore_service.dart` → `_migrate`) sprawdza po migracji
  każdą tabelę z manifestu kopii i jej liczbę wierszy. Migracja może dodać tabelę i przebudować istniejącą, ale nie
  może usunąć tabeli `media` ani jej wierszy.

## Decision
1. **`media` to rekord zdjęcia:** ścieżka pliku i, dla nagrobka, `grave_id` (najwyżej jedno zdjęcie na grób,
   [[ADR-008-photos-access-copy-and-backup-consistency]]). Kolumna `person_id` i warunek „osoba albo grób” znikają.
2. **`person_media` to łącze osoba–zdjęcie** (`person_id`, `media_id`, `position`; klucz `{person_id, media_id}`,
   indeks na `media_id`). Łącza osoby układają się według `position`, potem `media_id`.
3. **Profilowe = pierwsze łącze osoby, osobno dla każdej osoby.** „Ustaw jako profilowe” przenosi łącze na pierwsze
   miejsce tej osoby. Osoba dodana do zdjęcia dostaje łącze na końcu swojej kolejności, więc jej profilowe się nie
   zmienia, chyba że wcześniej nie miała zdjęć.
4. **Wiersz `media` bez grobu i bez łącza nie przeżywa transakcji, która go takim zostawiła.** Jego plik usuwa
   sprzątanie z ADR-008 pkt 3, po godzinie.
5. **Zmiany zdjęć osoby zapisują się w transakcji wpisu osoby** (z „Zapisz” formularza; [[zdjecia-osoby]] D1), także
   łącza innych osób. Nowe pliki przechodzą do `media/zdjecia/` przed transakcją i dostają czas „teraz”, bo zdjęcie
   może czekać w otwartym formularzu dłużej niż godzinę sprzątania (F4). Nieudany zapis odkłada pliki z powrotem.
6. **Migracja v3→v4:** utworzenie `person_media`; każde zdjęcie osoby z v3 staje się jej łączem w kolejności `id`;
   przebudowa `media` (`TableMigration`, te same wiersze i `id`); na końcu `PRAGMA foreign_key_check`.
7. **Kto jest na zdjęciu — bez źródła i statusu** ([[FR-001-provenance]] obejmuje daty, relacje i miejsce pochówku, a
   łącze w GEDCOM 7 nie ma `SOUR`).

## Options considered
| Option | For | Against | Status |
|---|---|---|---|
| **(a) `media` = rekord, nowa tabela łączy `person_media` z pozycją; grób zostaje przy `media.grave_id`** | odwzorowanie `OBJE` 1:1; ograniczenie odtwarzania spełnione (wiersze `media` zostają); kod nagrobka z ISSUE-016 bez zmian; `CROP` i `TITL` dojdą kolumnami łącza | jedna przebudowa tabeli w migracji | **chosen** |
| (b) jedna tabela łączy dla osób i grobów | jednolity model | przebudowuje dopiero co sprawdzony kod nagrobka, a grób i tak ma jedno zdjęcie | rejected |
| (c) wiersz `media` na każde łącze (ta sama ścieżka u kilku osób, kolumna pozycji, bez `UNIQUE` na ścieżce) | najmniejsza migracja | zdjęcie przestaje być rekordem: „kto jest na zdjęciu” to porównywanie ścieżek, a dane zdjęcia (podpis, data) powtarzają się w każdym wierszu | rejected |
| (d) profilowe jako znacznik `is_profile` przy łączu | jawny | wymaga warunku „dokładnie jeden na osobę”, a kolejność i tak jest potrzebna do siatki; rozjazd z GEDCOM | rejected |

## Consequences
- **Positive:**
  - jedno zdjęcie grupowe, jeden plik, łącza od wielu osób (test i emulator);
  - osoba z innego grobu dopisana później (decyzja autora D2 na stopie #1) to jedno nowe łącze;
  - kopia v3 odtwarza się w aplikacji v4 (F3);
  - migracja zachowuje wiersze i kolejność (F2, emulator).
- **Negative / trade-offs:**
  - zdjęcia osób zapisują się z „Zapisz”, a nagrobek od razu — dwie zasady (odczucie autora nieocenione na stopie #2);
  - odcisk danych zmienił się razem ze schematem, więc odciski sprzed v4 i po v4 nie są porównywalne (jak przy
    każdej zmianie schematu).
- **Follow-ups:**
  - **Kadr profilowego** (`CROP` przy łączu, kolumny w `person_media`, schemat v5 przez `addColumn`) — decyzja autora
    na stopie #2 ISSUE-017: następna pozycja, [[ISSUE-018-profile-photo-crop]].
  - Podpis zdjęcia (`TITL`, np. „Ślub, 1948”) i źródło rozpoznania osoby na zdjęciu — kolumny łącza, gdy pojawi się
    potrzeba.
