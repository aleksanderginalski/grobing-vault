---
title: "ADR-001 — Local-first: the phone's database is the single source of truth, no backend"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF Step 0 (local-first canon) · §Architecture → shape · §Security · §3a"
created: 2026-10-05
updated: 2026-10-05
---

# ADR-001 — Local-first

> Architecture Decision Record. **Append-only po akceptacji:** zmiana = nowy ADR, który ten zastępuje.

## Status
accepted — 2026-10-05 (kick-off, zatwierdzone przez autora na checkpoincie fazy 2).

## Context
- Zdanie wartości (brief §2): **prywatne** miejsce, które **przeżyje autora i aplikację**.
- Ścieżka wizyty odbywa się na cmentarzu — zasięg bywa słaby albo żaden (M7, H9).
- Jeden użytkownik (W1); rodzina dziedziczy **dane**, nie dostęp do aplikacji.
- Kanon: [Local-first software](https://inkandswitch.com/local-first/) (Ink & Switch, 2019) — cztery z
  siedmiu ideałów to niemal dosłownie zdanie wartości (offline, długowieczność, prywatność, kontrola
  użytkownika); [Android: offline-first](https://developer.android.com/topic/architecture/data-layer/offline-first)
  — lokalna baza jako jedyne źródło prawdy.
- Sprawdzony stos autora (wcześniejsza aplikacja) trzyma dane w chmurze — **reuse stosu nie jest reuse
  jego modelu przechowywania** (brief §3a, Conflict Check 3).

## Decision
**Lokalna baza SQLite + zdjęcia w prywatnym magazynie aplikacji są jedynym źródłem prawdy.** Bez serwera,
bez kont, bez analityki, bez crash reportingu poza telefon. Poza telefonem żyją dwa **różne** artefakty:
**kopia** (zaszyfrowana, automatyczna, do odtworzenia) i **eksport** (czytelny bez aplikacji, dla rodziny,
offline) — kopia nie jest bazą w chmurze, którą telefon odzwierciedla.

## Options considered

| Option | Pros | Cons | Why (not) chosen |
|---|---|---|---|
| **Baza w telefonie = SoT + zaszyfrowana kopia + czytelny eksport** | offline z konstrukcji; prywatność; dane żyją bez aplikacji (eksport); zero kosztów serwera | telefon jest jedyną kopią, dopóki kopia nie istnieje; brak wielu urządzeń | **chosen** |
| Backend w chmurze jako SoT (model wcześniejszej aplikacji autora) | sprawdzony stos; synchronizacja „za darmo" | chmura firmy trzyma dane żyjących krewnych — sprzeczne z „prywatne"; wymaga zasięgu na cmentarzu; dane umierają z usługą | rejected — prywatność, offline, długowieczność |
| Lokalna baza jako lustro bazy w chmurze (sync) | offline + automatyczna kopia | nadal baza w chmurze z danymi rodziny; złożoność synchronizacji dla jednego użytkownika | rejected — kanon: kopia to backup i eksport, nie lustro |
| Hostowany serwis genealogiczny (MyHeritage / FamilySearch) | drzewo, zdjęcia, przeżywa autora, zero budowy | nieprywatny; zakotwiczony w osobie — grób nie jest punktem wejścia | rejected — test zastępowalności (brief §2) |

## Consequences
- **Positive:** [[NFR-001-offline]] z konstrukcji · [[NFR-005-dane-nie-opuszczaja-telefonu]] da się
  utrzymać · długowieczność niesie eksport (HTML + PDF), nie format aplikacji.
- **Negative / trade-offs:** od pierwszej przepisanej osoby telefon jest **jedyną cyfrową kopią** —
  dlatego kopia + odtwarzanie **przed masowym przepisywaniem** (MD2, [[NFR-002-odtworzenie-na-nowym-telefonie]]);
  brak współdzielenia (W1) — świadomie.
- **Follow-ups:** [[ADR-004-backup-format-encryption-destination]] (kopia) ·
  [[SPIKE-003-backup-and-restore]] · [[NT-003-verify-household-exemption]] (miejsce kopii a RODO) ·
  model danych: `04_ARCHITECTURE/data-model.md`.
