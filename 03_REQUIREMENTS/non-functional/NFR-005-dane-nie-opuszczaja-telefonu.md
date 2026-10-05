---
title: "NFR-005 — No family data leaves the phone except the encrypted backup and the export"
type: non-functional-requirement
status: draft
epic: ["[[EPIC-001-zabezpiecz-i-przepisz]]", "[[EPIC-002-wizyta]]", "[[EPIC-003-zrozumienie]]"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §Security (ASVS-lite translated, off-phone copy) · Step 0 (local-first: privacy) · §2 value ('private')"
created: 2026-10-05
updated: 2026-10-05
---

# NFR-005 — Dane nie opuszczają telefonu poza kopią

## Requirement
Dane rodziny opuszczają telefon **wyłącznie** jako:
1. **kopia zaszyfrowana w telefonie** (hasłem) przed wysłaniem do folderu w chmurze autora;
2. **okresowy eksport** czytelny bez aplikacji, przechowywany offline u rodziny (§Security: *„a periodic
   plain export kept offline by the family"*).

Nic więcej: **bez analityki, bez crash reportingu wysyłającego dane, bez danych rodziny w logach**, bez
SDK wysyłających dane z telefonu (np. Firebase).

| | |
|---|---|
| **Metric** | kanały wychodzące z telefonu, które niosą dane rodziny, poza dwoma powyższymi |
| **Target** | **zero** |
| **Method** | przegląd zależności przy każdej pozycji dokładającej pakiet (`qa`); przegląd logów pod kątem danych rodziny |
| **Verification trigger** | każda nowa zależność · [[ISSUE-002-bootstrap-code-repo]] (AC: brak Firebase) · pełny przegląd L1 przy [[DEF-002-full-l1-review]] |

## Notes
- **Wchodzi, nie wychodzi:** kafelki map są pobierane, nie wysyłane; link do Grobonetu otwiera się w
  zewnętrznej przeglądarce (bez WebView z danymi użytkownika).
- **Androidowa automatyczna kopia (`allowBackup`)** domyślnie kopiuje dane aplikacji na Dysk Google — to
  też kanał wychodzący. **Decyzja świadoma, nie dziedziczona** → [[ADR-004-backup-format-encryption-destination]].
- Eksport nie jest szyfrowany z założenia (czytelność jest jego celem) — dlatego żyje offline, nie w chmurze
  (§Security).
- Hipoteza prawna (wyłączenie domowe RODO) jest najmocniejsza, gdy chmura trzyma tylko szyfrogram →
  [[NT-003-verify-household-exemption]].
