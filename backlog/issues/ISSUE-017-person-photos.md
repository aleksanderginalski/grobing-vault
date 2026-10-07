---
title: "ISSUE-017 — Person photos: each person's photo collection, photos shared between people, a chosen profile photo (schema v4)"
type: issue
status: ready
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-005-zdjecia]]"
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "stop #1 ISSUE-016, rundy 1–2 (decyzje autora 2026-10-07: D1 — baza zdjęć osoby, dzielona, z „profilowym”; D6' — podział na ISSUE-016 i ISSUE-017; D2' — 2048 px, JPEG 85) · GEDCOM 7.0 (OBJE, CROP, „the first is the most-preferred value”)"
created: 2026-10-07
updated: 2026-10-07
---

# ISSUE-017 — Zdjęcia osoby

> Z rozpisania [[US-005-zdjecia]] na stopie #1 [[ISSUE-016-photos-grave-and-person]] (decyzja autora 2026-10-07):
> ISSUE-016 robi zdjęcie nagrobka i fundament zdjęć (zmniejszanie, podgląd, spójność kopii), a ta pozycja —
> **zdjęcia osób**. Słowa autora: *„osoby chciałbym, aby miały «swoją bazę zdjęć» (lub dzieloną, jeżeli na zdjęciu
> jest kilka osób) i możliwość wybierania z nich «profilowego»”*. To **zmiana schematu**, więc pozycja zaczyna się
> od kanonu i modelu, nie od ekranu.

## What to build
1. **Baza zdjęć osoby:** osoba ma dowolnie wiele zdjęć, z galerii albo aparatem (ta sama droga co w ISSUE-016:
   arkusz źródła, zmniejszanie do 2048 px, JPEG 85).
2. **Zdjęcie dzielone:** jedno zdjęcie (np. ślubne) należy do kilku osób, bez kopii pliku.
3. **Profilowe:** autor wybiera, które zdjęcie osoby jest jej zdjęciem profilowym. Profilowe widać w formularzu
   osoby (miejsce wskazane w [[wpis-osoby]] v3, element 1a) i jako miniaturę w karcie osoby w [[grob]].
4. **Schemat v4:** zdjęcie jako osobny rekord, łącze osoba–zdjęcie z kolejnością (jak `OBJE` w GEDCOM 7), migracja
   v3→v4 z testem; istniejące zdjęcia osób z v3 przechodzą do łączy.

## Acceptance Criteria
- [ ] US-005 AC-1 (osoba): zdjęcie wybrane z galerii albo zrobione aparatem jest widoczne przy osobie.
- [ ] US-005 AC-2: aplikacja trzyma własną kopię pliku w prywatnym magazynie (jak w ISSUE-016).
- [ ] US-005 AC-3: zdjęcia osób i ich łącza są w kopii i wracają po odtworzeniu, z odciskiem zgodnym.
- [ ] Osoba może mieć kilka zdjęć; jedno z nich autor wybiera jako profilowe.
- [ ] To samo zdjęcie można przypisać kilku osobom; plik jest jeden.
- [ ] Usunięcie zdjęcia z jednej osoby nie usuwa go innym osobom, które je mają.
- [ ] Migracja v3→v4 zachowuje wszystkie dane; kopia v3 odtwarza się w aplikacji v4; po migracji kopia w tle
      zamawia się od razu (retro 1, R6).
- [ ] Ekran stosuje wytyczne stylu B ([[style-b]], reguła 14).

## Out of Scope
- **Wycinek twarzy z grupowego zdjęcia** (`CROP` z GEDCOM 7) — osobna pozycja po tej. Schemat v4 go nie przewiduje
  z góry: kolumny dojdą migracją (`addColumn`), gdy powstanie ekran wycinania.
- Widok osoby (M5, R4 prawy) z pełną galerią — ta pozycja pokazuje bazę zdjęć tam, gdzie zdecyduje `ui`.
- **Przypisanie zdjęcia osobie z innego grobu:** wymaga wyboru spośród wszystkich osób, a wyszukiwania osób (S5)
  jeszcze nie ma. `ui` i `planning` ustalają, czy wystarczy wybór spośród osób z tego samego grobu, i mówią to na
  stopie #1.
- Zdjęcie nagrobka → [[ISSUE-016-photos-grave-and-person]].

## Technical Notes
- **Kanon** (odczyt 2026-10-07, cytaty: ISSUE-016 → *Stop #1 — round 1*): w GEDCOM 7 zdjęcie to rekord
  `MULTIMEDIA_RECORD`, a osoba ma do niego łącze `OBJE`; przy łączu może stać `CROP`; *„the first is the
  most-preferred value”* — profilowe = pierwsze łącze. Ta sama zasada „pierwszej wartości” co [[ADR-006-claimed-value-separate-structures]] D3.
- Dziś `Media` ma jednego właściciela (`CHECK ((person_id IS NULL) <> (grave_id IS NULL))`). Grób w ISSUE-016 zostaje
  przy `grave_id` (najwyżej jedno zdjęcie). Model v4 rozstrzyga ADR (następny wolny numer) z ≥ 3 opcjami.
- Usunięcie zdjęcia z osoby usuwa **łącze**; plik bez żadnego łącza i bez grobu sprząta mechanizm z ISSUE-016 (D3).
- Fundament z ISSUE-016: arkusz źródła, zmniejszanie, podgląd, spójność kopii.
- Dane do testów i weryfikacji wyłącznie wymyślone; obrazy generowane (strażnik danych rodziny).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-016-photos-grave-and-person]] (fundament zdjęć) | technical | `done` (2026-10-07) — [[ADR-008-photos-access-copy-and-backup-consistency]] |
| specyfikacja `ui`: baza zdjęć osoby, profilowe, dzielenie | design | do zrobienia przed planem ([[wpis-osoby]] v3 to kierunek z jednym zdjęciem — do przeprojektowania) |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP):
- test happy-path dla każdego AC;
- ręczna weryfikacja na emulatorze;
- zmiana schematu, więc test migracji v3→v4;
- próbne odtworzenie z kopii przechodzi;
- zero danych rodziny w zmianach.

Po przyjęciu tego ISSUE US-005 idzie do werdyktu US.
