---
title: "EPIC-001 — Zabezpiecz i przepisz (secure & transcribe)"
type: epic
status: draft
moscow: [M1, M8]
persona: "[[P1-zbierajacy]]"
FR: ["[[FR-001-provenance]]", "[[FR-002-rodzina-jako-rekord]]", "[[FR-003-wiele-osob-w-grobie]]", "[[FR-004-data-z-dopiskiem]]", "[[FR-005-nazwisko-rodowe]]"]
NFR: ["[[NFR-002-odtworzenie-na-nowym-telefonie]]", "[[NFR-003-migracje-schematu]]", "[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
user-stories: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §5 M1, M8 · Step 0 (domain canon) · MD2"
created: 2026-10-05
updated: 2026-10-05
---

# EPIC-001 — Zabezpiecz i przepisz

## Goal
Wiedza z papierowych notatek i od babci trafia do aplikacji jako rodziny ze źródłami — i od pierwszej
przepisanej osoby ma kopię poza telefonem, którą da się naprawdę odtworzyć.

## Stage of the genealogist's process
**Pierwszy etap kanonu:** zabezpiecz notatki → przepisz je **rodzinami** (para + dzieci) → zapisz, co
pamięta najstarsze żyjące pokolenie (brief, Step 0 → *Genealogy*). Kolejność EPIC-ów idzie za tym
modelem (MD2): ten EPIC jest pierwszy.

> **Dlaczego rozmowa z babcią nie jest osobnym EPIC-iem** (brief MD2 szacuje „~4 EPICs"): wprowadzanie
> faktów od babci to ta sama funkcja M1 ze źródłem „babcia" ([[FR-001-provenance]]). Osobny EPIC nie
> miałby własnej pozycji Must. Ustalone z autorem przy planowaniu [[ISSUE-001-materialize-backlog]].

## In scope
- **M1 — minimum wprowadzania:** cmentarz · grób (adres kwatery, zdjęcie nagrobka, pinezka) · osoby w
  grobie (imię i nazwisko, daty, zdjęcie, kim była) · relacje (rodzice, małżeństwa, dzieci) — tyle, ile
  trzeba, żeby przepisać ok. 100 osób z notatek. Wprowadzanie **całymi rodzinami** (G6,
  [[FR-002-rodzina-jako-rekord]]).
- **M8 — przeżywa telefon i aplikację:** kopia poza telefonem **ze sprawdzonym odtworzeniem** (G1) ·
  eksport czytelny bez aplikacji · notka przekazania dla rodziny (G2 — poza kodem, [[NT-007-hand-over-note]]).
- ⚠️ **Kolejność wewnątrz EPIC-a (MD2):** kopia + odtwarzanie **przed masowym przepisywaniem** — od
  pierwszej przepisanej osoby telefon jest jedyną cyfrową kopią, czyli problem papieru od nowa.

## Out of scope
- Widoki wizyty (M2-M7) → [[EPIC-002-wizyta]]; widok 5 (M9-M11) → [[EPIC-003-zrozumienie]].
- S4 opłata za grób + przypomnienie · S5 wyszukiwanie · C2 eksport GEDCOM · C5 cofanie / brak cichego
  usuwania (albo jako własność architektury) · W2 import z innych drzew.
- Samo przepisywanie i fotografowanie notatek — praca autora poza kodem: [[NT-001-photograph-the-notes]],
  [[NT-002-transcribe-the-notes]].

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[SPIKE-003-backup-and-restore]] → [[ADR-004-backup-format-encryption-destination]] | technical | ✅ spike `done`, ADR `accepted` (2026-10-05). Produkcyjna funkcja kopii to US/ISSUE z rozpisania tego EPIC-a; **przed pierwszymi prawdziwymi danymi** (ADR-004 → *Follow-ups*) |
| [[ADR-001-local-first]] · [[ADR-002-flutter-pinned]] | technical | `accepted` |
| `04_ARCHITECTURE/data-model.md` | technical | przyjęty w kick-offie |
| [[ISSUE-002-bootstrap-code-repo]] | technical | `done` (2026-10-05) |
| [[NT-003-verify-household-exemption]] | legal (hipoteza) | `open` — wpływa na miejsce kopii |

## Open questions
- ⚠️ **OPEN — grób bez adresu kwatery i bez pinezki.** Korekta autora (2026-10-05): notatki **nie
  zawierają adresów kwater**. M1 zakłada „grób: adres kwatery, zdjęcie nagrobka, pinezka" — przy
  przepisywaniu nie ma żadnego z trzech. Grób przepisany z notatek to więc: cmentarz + osoby w nim.
  Patrz `00_START_HERE/TRACEABILITY.md` → *Open gaps* 1. Decyzja autora.
- Ziarnistość źródeł (twierdzenia na datach, relacjach i miejscu pochówku; „kim była" — jedna linia
  źródła) jest decyzją kosztową z kick-offu — patrz [[FR-001-provenance]].
