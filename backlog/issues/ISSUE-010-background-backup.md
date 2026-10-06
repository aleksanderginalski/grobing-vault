---
title: "ISSUE-010 — Background backup: after data changes, without the passphrase"
type: issue
status: ready
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-001-kopia-z-odtworzeniem]]"
ideal_days: 1
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
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
