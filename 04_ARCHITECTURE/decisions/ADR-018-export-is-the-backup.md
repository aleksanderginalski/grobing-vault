---
title: "ADR-018 — Export is the backup's open inside (SQLite + photos + manifest), opened with the official age; no HTML/PDF export"
type: adr
status: accepted
supersedes: ["[[ADR-004-backup-format-encryption-destination]] — tylko *Eksport (A4)*", "[[ADR-001-local-first]] — tylko „eksport czytelny bez aplikacji (HTML + PDF)”"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-040-export-is-the-backup]]"
source: "decyzja autora 2026-10-16 (łańcuch `/pm` → US-006, stop #1 ISSUE-040: „tak naprawdę nie potrzebuję HTML i PDF-a, wystarczy mi możliwość eksportowania. Gdybym kiedyś chciał wykorzystać tę bazę w innym produkcie. W skrócie — nie zależy mi na estetyce, a na zachowaniu danych” → „tak, wystarczy”) · Library of Congress Recommended Formats Statement → Datasets · FamilySearch GEDCOM 7 · 04_ARCHITECTURE/backup-format.md"
created: 2026-10-16
updated: 2026-10-16
---

# ADR-018 — Eksport to otwarte wnętrze kopii

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-16, decyzja autora w łańcuchu [[US-006-eksport-dla-rodziny]] (stop #1 [[ISSUE-040-export-is-the-backup]]).

**Pierwszy ADR, który zastępuje zaakceptowaną decyzję** (część [[ADR-004-backup-format-encryption-destination]] i
[[ADR-001-local-first]]) — to sygnał dla agenta `architect` z `CLAUDE.md` („pierwszy ADR zastąpiony po akceptacji”, retro 2, R7).

## Context
Kick-off zapisał dwa artefakty poza telefonem: **kopię** (zaszyfrowaną, do odtworzenia) i **eksport** (HTML + PDF czytelny bez
aplikacji, dla rodziny — brief §5 M8, G2, §Security; ADR-001; ADR-004 → *Eksport (A4)*). Przy planowaniu eksportu (ISSUE-040, makieta
pliku dla rodziny) autor powiedział, czego naprawdę chce: **zachować dane i móc je kiedyś użyć w innym produkcie**, a nie mieć ładny
plik. Kopia już jest w otwartym, opisanym formacie:
- `age` v1 → `tar` (ustar) → `grobing.db` (SQLite, migawka `VACUUM INTO`), `media/…` (zdjęcia), `manifest.json` (wersje, liczby
  rekordów, SHA-256 każdego pliku) — `04_ARCHITECTURE/backup-format.md`, pisane z myślą o kimś, *„kto nie ma Grobing”*;
- otwarcie oficjalnym `age` sprawdziła bramka zgodności [[ISSUE-008-backup-write]] (age v1.3.2, Python `sqlite3`, SHA-256 = manifest).

**Kanon:** Library of Congress, Recommended Formats Statement → Datasets ([źródło](https://www.loc.gov/preservation/resources/rfs/data.html),
odczyt 2026-10-16) — *Preferred*: *„Platform-independent open formats, e.g. .db, .db3, .sqlite, .sqlite3”*; tar jako opakowanie —
*Acceptable* *„with no encryption, password or other protection mechanisms”*. Do wymiany między programami genealogicznymi służy
FamilySearch GEDCOM 7 ([spec](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html), odczyt 2026-10-16): *„Its first purpose is to
foster sharing genealogical information”*.

## Decision
**Eksportem danych jest kopia.** Dane wychodzą poza aplikację jako odszyfrowane wnętrze kopii: baza SQLite, zdjęcia i manifest, opisane
w `backup-format.md` i `data-model.md`, otwierane oficjalnym `age` bez Grobing. **Osobnego eksportu HTML ani PDF nie ma**, a wiersz
„Eksport dla rodziny” znika z ustawień. Format wymiany (GEDCOM 7) powstaje dopiero pod konkretny produkt docelowy.

## Options considered

| Option | Pros | Cons | Why (not) chosen |
|---|---|---|---|
| Czytelny eksport HTML + PDF/A dla rodziny (ADR-001, ADR-004 A4; makieta ISSUE-040) | rodzina czyta bez aplikacji i bez techniki; druk | nowa zależność (`pdf` 3.12.0 — ostatnia zgodna z Dartem 3.11; 8 pakietów), ok. 10 nowych plików, osobny model treści do utrzymania przy każdej zmianie schematu; nie daje danych do innego produktu | rejected — autor nie potrzebuje wyglądu, tylko danych |
| **Kopia jako eksport** (SQLite + zdjęcia + manifest w `tar`, `age`) | już istnieje i działa co ~10 min; SQLite — format *Preferred* LoC; opisany schemat i sumy kontrolne; zero nowego kodu | do odczytu potrzebne `age`, plik klucza i hasło; schemat własny aplikacji (inny produkt potrzebuje konwertera) | **chosen** |
| Jawny eksport — ten sam `tar` bez szyfrowania, przyciskiem w aplikacji | bez `age` i hasła | kopia zrobiona drugi raz; jawny plik z danymi żyjących poza telefonem (NFR-005, §6 N3) — a autor i tak ma hasło | rejected |
| GEDCOM 7 / GEDZIP | standard wymiany; import do Gramps, FamilySearch, MyHeritage | największy koszt (mapowanie modelu, walidacja); część danych Grobing (pinezki, kwatery, kadry) idzie w rozszerzenia; **docelowego produktu dziś nie ma** | deferred — buduje się pod konkretny produkt (C2), model już się mapuje (ADR-006, ADR-010, ADR-012) |

## Consequences
- **Positive:**
  - dane przeżywają aplikację w formacie, który LoC zaleca dla zbiorów danych, bez nowego kodu i zależności;
  - [[NFR-005-dane-nie-opuszczaja-telefonu]]: znika drugi kanał (jawny eksport) — poza telefon wychodzi tylko szyfrogram;
  - `persons.is_living` nie steruje już niczym (sterował prywatnością eksportu) — pole zostaje w schemacie bez zmian, bez migracji.
- **Negative / trade-offs:**
  - **rodzina bez autora nie przeczyta danych bez aplikacji** bez `age`, pliku klucza, hasła i odrobiny techniki (osłabia G2 z briefu);
    [[NT-007-hand-over-note]] traci punkt „gdzie leży eksport” i opisuje tylko kopię;
  - inny produkt dostaje własny schemat Grobing — import wymaga konwertera albo GEDCOM 7 później;
  - zapis kick-offu (`kickoff/PROJECT_BRIEF.md` §5 M8, G2, §Security „a periodic plain export”) zostaje bez zmian jako historia; obowiązuje
    ten ADR.
- **Follow-ups:**
  - [[ISSUE-040-export-is-the-backup]]: kopia z dzisiejszym schematem otwarta na PC oficjalnym `age`, baza niezależnie od naszego kodu
    (liczby = manifest); wiersz eksportu i punkt 5 notki usunięte z aplikacji;
  - GEDCOM 7 — gdy pojawi się konkretny produkt docelowy (nowa pozycja, C2);
  - sygnał dla agenta `architect` → `pm`.
