---
title: "ADR-004 — Backup: format, phone-side encryption, destination; export formats"
type: adr
status: proposed
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

> Architecture Decision Record. `proposed` — **kierunek wybrał autor** (§Security, 2026-10-05);
> **mechanizm zamyka [[SPIKE-003-backup-and-restore]]** (warunek wyjścia: odtworzenie wykonane naprawdę →
> ten ADR `accepted`).

## Status
proposed — 2026-10-05.

## Context
- „Przeżywa autora i aplikację" (brief §2) → kopia poza telefonem **ze sprawdzonym odtworzeniem** (M8, G1)
  i eksport czytelny bez aplikacji.
- **Dwa artefakty o przeciwnych własnościach** (§Security): kopia — pełna, automatyczna, **zaszyfrowana**,
  sprawdzona odtworzeniem; eksport — **jawny** (czytelność jest celem), trwały, offline u rodziny.
- Hipoteza prawna: wyłączenie domowe RODO jest najmocniejsze, gdy dostawca chmury trzyma tylko szyfrogram
  ([[NT-003-verify-household-exemption]]).
- Androidowa automatyczna kopia jest **domyślnie włączona** i ma limit **25 MB na aplikację**
  ([Android docs](https://developer.android.com/identity/data/autobackup)).

## Decision
**Kierunek (autor, 2026-10-05):** automatyczna kopia **szyfrowana w telefonie** (hasłem) przed wysłaniem
do folderu we własnej chmurze autora **+** okresowy jawny eksport przechowywany offline przez rodzinę.

**Do rozstrzygnięcia w SPIKE-003:**
- miejsce przez **systemowe okno wyboru folderu** — *hipoteza*: bez kluczy API i sekretów OAuth w aplikacji;
- format pliku kopii i walidacja przed odtworzeniem (floor: walidacja wejścia na granicy zaufania);
- gdzie trzymać klucz do kopii automatycznej (kandydat: `flutter_secure_storage`);
- **`allowBackup` — decyzja świadoma**, nie dziedziczona.

**Eksport (A4):** samodzielny HTML + PDF, bez formatu specyficznego dla aplikacji; nazwy ze znakami
specjalnymi escapowane (§Security, output encoding).

## Options considered

| Option | Pros | Cons | Why (not) chosen |
|---|---|---|---|
| **Kopia szyfrowana w telefonie → folder w chmurze autora, automatycznie + jawny eksport offline** | pełna, automatyczna; chmura trzyma tylko szyfrogram | **utracone hasło = utracona kopia** → hasło w notce przekazania ([[NT-007-hand-over-note]]), fizycznie, nie w tej samej chmurze | **kierunek wybrany przez autora** |
| Tylko plik eksportu kopiowany ręcznie na PC / USB | brak strony trzeciej | zależy od pamiętania — ręczne umiera, gdy brak czasu | rejected |
| Sama androidowa automatyczna kopia | automatyczna, szyfrowana end-to-end od Androida 9 | limit 25 MB → **cicho niepełna** ze zdjęciami | rejected |

## Consequences
- **Positive:** [[NFR-002-odtworzenie-na-nowym-telefonie]] ma mechanizm; [[NFR-005-dane-nie-opuszczaja-telefonu]]
  — jedyny kanał wychodzący z danymi rodziny jest zaszyfrowany.
- **Negative / trade-offs:** hasło jest pojedynczym punktem awarii; eksport jest jawny — dlatego offline.
- **Follow-ups:**
  - [[SPIKE-003-backup-and-restore]] **poprzedza masowe przepisywanie** (MD2).
  - ⚠️ **OPEN — kopia sprzed migracji schematu:** czy kopię zrobioną w starszej wersji da się odtworzyć w
    nowszej ([[NFR-003-migracje-schematu]]) — do rozstrzygnięcia przy formacie kopii.
