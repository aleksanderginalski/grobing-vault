---
title: "ADR-005 — SQLite package: drift on sqlite3 with a bundled SQLite"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-007-data-layer]]"
source: "ADR-001 (local SQLite = SoT) · ADR-004 (VACUUM INTO, user_version, migrations on restore) · NFR-003 · PROJECT_BRIEF §Stack („SQLite (e.g. drift)”)"
created: 2026-10-05
updated: 2026-10-05
---

# ADR-005 — Paczka SQLite

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-05. Kierunek zaakceptował autor na stopie #1 [[ISSUE-007-data-layer]], a falsyfikator
z kroku 1 przeszedł na emulatorze. Pomiary i liczby są w pozycji (*Implementation plan* → *Prior art*,
*Dev report*) i tam zostają (jedna liczba, jeden dom).

## Context
- [[ADR-004-backup-format-encryption-destination]] stoi na funkcjach samego SQLite: migawka
  `VACUUM INTO` (od SQLite 3.27.0, [release log](https://www.sqlite.org/releaselog/3_27_0.html)),
  `PRAGMA user_version` zgodne z manifestem, `integrity_check` i zwykłe migracje przy odtworzeniu kopii.
- Aplikacja ma `minSdk` 24. Paczka, która używa SQLite telefonu, dostaje wersję zależną od Androida.
  Wersji systemowego SQLite dla API 24-29 nie potwierdzono w źródle.
- **Flutter jest przypięty na 3.41.1 z Dartem 3.11.0** ([[ADR-002-flutter-pinned]]). Na tym ograniczeniu
  odpadł w [[SPIKE-003-backup-and-restore]] `dartage`. Zmierzone w pub.dev i w rozwiązywaniu zależności
  (2026-10-05):
  - najnowszy `sqflite` (2.4.4+1) wymaga Fluttera ≥ 3.44; z przypiętym działa najwyżej 2.4.2+1;
  - `sqlite3` rozwiązuje się najwyżej do 3.5.2, bo 3.6+ wymaga `hooks` ^2.2;
  - przypięty SDK trzyma `analyzer` na 10.x, więc `drift_dev` działa najwyżej w 2.34.0, a `drift` 2.34.1
    i 2.34.4 nie kompilują się z nim, choć zakres wersji je dopuszcza;
  - `sqlite3_flutter_libs` jest wycofany (EOL).
- [[NFR-003-migracje-schematu]] wymaga testu migracji z poprzedniej wersji przy każdej zmianie schematu.

## Decision
**`drift` 2.34.0 na `sqlite3` (^3.5.2), który dołącza własny SQLite przez build hooks.** `drift` i
`drift_dev` są przypięte **parą** na 2.34.0. `minSdk` zostaje 24.

Zmierzone w falsyfikatorze (build release, emulator API 36, x86_64):
- SQLite **3.53.4** w aplikacji, niezależny od wersji Androida;
- `VACUUM INTO` daje kopię z `integrity_check` = `ok`, która **zachowuje `user_version`**;
- `drift` trzyma `schemaVersion` w `PRAGMA user_version`;
- hooks budują się na Flutterze 3.41.1.

## Options considered

| Option | Pros | Cons | Why (not) chosen |
|---|---|---|---|
| **`drift` na `sqlite3` z dołączonym SQLite** | SQLite niezależny od telefonu, więc `VACUUM INTO` działa wszędzie; `make-migrations` i `SchemaVerifier` dają testy migracji (NFR-003); typowane zapytania; `user_version` = `schemaVersion` | generowanie kodu (`build_runner`, `*.g.dart`); para `drift`/`drift_dev` przypięta przez SDK; pierwszy build pobiera bibliotekę z sieci; APK większy o ~1,7 MB na ABI | **wybrane** |
| `sqflite` 2.4.2+1 (SQLite telefonu) | popularny, bez generowania kodu, mniejszy APK | zatrzymany na starej linii: każda nowsza wersja wymaga odpięcia Fluttera; `VACUUM INTO` zależy od Androida (API 24-29 niepotwierdzone, brak obrazu do pomiaru); migracje ręcznie w `onUpgrade`, bez generowanych testów | rejected — zależność od wersji SQLite telefonu i zamrożona wersja |
| sam `sqlite3` (czysty SQL, bez `drift`) | najmniej zależności, pełna kontrola, ten sam dołączony SQLite | własne narzędzie do testów migracji i własne mapowanie wierszy; więcej kodu do utrzymania przez jedną osobę | rejected — NFR-003 dostaje gotowe narzędzie w `drift` |
| `sqlite3` z systemowym SQLite (`source: {android: system}`, od 3.6.0) | mniejszy APK | 3.6+ nie rozwiązuje się z przypiętym SDK; wraca zależność od wersji Androida | niewykonalne teraz |
| `sqlite3_flutter_libs` | znany sposób dołączania SQLite | paczka wycofana (EOL) | rejected |

## Consequences
- **Positive:**
  - kopia z ADR-004 ma `VACUUM INTO` i `user_version` w każdej wersji Androida;
  - migracje mają narzędzie: zapis schematu każdej wersji (`drift_schemas/grobing/`) i weryfikator w
    testach; schemat v1 jest punktem odniesienia;
  - klucze obce włączone przy każdym otwarciu: usunięcie osoby z pochówkiem kończy się błędem, a nie
    cichym osieroceniem danych.
- **Negative / trade-offs:**
  - **para `drift`/`drift_dev` zamrożona przez przypięty Flutter.** Ruszenie jednej bez drugiej psuje
    generowanie kodu i weryfikator migracji (zmierzone);
  - **pierwszy build potrzebuje sieci:** hook pobiera bibliotekę z wydań `sqlite3.dart` na GitHubie i
    sprawdza SHA-256 zapisane w paczce; potem korzysta z cache;
  - ładowanie dołączonej biblioteki na Androidzie 7-10 nie jest zmierzone (brak obrazu emulatora);
  - generowanie kodu przy każdej zmianie tabel (README `grobing-code` → *Baza danych*).
- **Follow-ups:**
  - Zmiana wersji Fluttera ([[ADR-002-flutter-pinned]]) → `drift` i `drift_dev` razem, potem
    `drift_dev schema dump` (porównanie z zapisanym schematem) i pełne testy.
  - Encja *Assertion* przyjdzie jako schemat v2 przy [[US-002-przepisanie-grobu]], z pierwszym prawdziwym
    testem migracji (ISSUE-007, D2).
