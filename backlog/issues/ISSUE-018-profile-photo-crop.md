---
title: "ISSUE-018 — Profile photo crop: the author frames a person's face on a group photo, each person their own crop (schema v5)"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: null
related: "[[US-005-zdjecia]] (rozwinięcie po jej werdykcie — AC US-005 spełnione bez tej pozycji)"
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "stop #2 ISSUE-017 (2026-10-07): uwaga autora o zdjęciu grupowym i decyzja „tak zróbmy” — następna pozycja, przed US-003 · GEDCOM 7.0 MULTIMEDIA_LINK → CROP (TOP, LEFT, HEIGHT, WIDTH) · ADR-009 → Follow-ups"
created: 2026-10-07
updated: 2026-10-07
---

# ISSUE-018 — Kadr profilowego

> Z uwagi autora na stopie #2 [[ISSUE-017-person-photos]]: *„co z sytuacją, gdy jest to zdjęcie «grupowe» — zakładałem,
> że gdy wybieram dane zdjęcie, to mogę ustalić jego «kadr» z liniami pomocniczymi, aby na profilowym była właśnie ta
> osoba, a nie całe zdjęcie”*. Decyzja autora: *„tak zróbmy”* — **następna pozycja, przed
> [[US-003-przepisanie-rodziny]]**. To spełnia warunek obalający [[wpis-osoby]] D-zdjęcie-3 („bez kadrowania — obali:
> środek zdjęcia nie trafia w twarz”).

## What to build
1. **Kadr profilowego:** ekran z całym zdjęciem i okręgiem z liniami pomocniczymi, który pokazuje, co zobaczy się w
   profilowym. Okrąg da się przesunąć i powiększyć, a potem „Gotowe”. Wejście (kierunek z ISSUE-017, kształt ustala
   `ui`): przy „Ustaw jako profilowe” i z podglądu zdjęcia osoby.
2. **Kadr należy do łącza osoba–zdjęcie**, nie do zdjęcia (`CROP` przy `OBJE` w GEDCOM 7). Na jednym zdjęciu grupowym
   każda osoba ma własny kadr, a plik zdjęcia się nie zmienia.
3. **Profilowe pokazuje kadr** wszędzie, gdzie jest okręgiem: formularz osoby (1a), karta osoby w [[grob]], nagłówek
   [[zdjecia-osoby]].
4. **Schemat v5:** kolumny kadru w `person_media` (`addColumn`), migracja v4→v5 z testem; kopia po migracji (R6).

## Acceptance Criteria
- [ ] Na zdjęciu grupowym autor ustawia kadr profilowego jednej osoby; okrąg profilowego pokazuje ten kadr w
      formularzu, w karcie grobu i w nagłówku zdjęć osoby.
- [ ] Dwie osoby na tym samym zdjęciu mają różne kadry; plik zdjęcia jest jeden i się nie zmienia.
- [ ] Kadr da się poprawić.
- [ ] Kadr jest w kopii i wraca po odtworzeniu, z odciskiem zgodnym.
- [ ] Migracja v4→v5 zachowuje wszystkie dane; kopia v4 odtwarza się w aplikacji v5; kopia w tle zamawia się po
      migracji.
- [ ] Ekran stosuje wytyczne stylu B ([[style-b]], reguła 14; gesty z alternatywą jednym dotknięciem — SC 2.5.1).

## Out of Scope
- Automatyczne wykrywanie twarzy.
- Kadr miniatur w siatce zdjęć osoby (siatka zostaje wycinana ze środka — [[zdjecia-osoby]] D3), chyba że `ui`
  zaproponuje inaczej na stopie #1.
- Podpis zdjęcia (`TITL`) i źródło rozpoznania osoby na zdjęciu ([[ADR-009-person-photos-record-and-link]] →
  *Follow-ups*).
- Semantyka starszych ekranów (kandydat z przeglądu `ui` ISSUE-017 → `CURRENT_STATE.md`).

## Technical Notes
- **Kanon:** GEDCOM 7.0 `MULTIMEDIA_LINK` → `CROP` z `TOP`, `LEFT`, `HEIGHT`, `WIDTH` (liczby całkowite, piksele) —
  gramatyka przepisana w [[ISSUE-017-person-photos]] → *Prior art*. Zdjęcie w aplikacji to kopia dostępowa 2048 px
  ([[ADR-008-photos-access-copy-and-backup-consistency]]); czy kadr zapisywać w pikselach (jak GEDCOM), czy w ułamkach
  boków — do ADR przy planowaniu (≥ 3 opcje).
- Model: [[ADR-009-person-photos-record-and-link]] — łącze ma miejsce na kolumny kadru; zapis zmian z „Zapisz”
  formularza osoby, w jednej transakcji.
- Okrąg profilowego dekoduje dziś zdjęcie w szerokości 2 × pole (`coverDecodeWidth`); kadr zmieni, co i w jakim
  rozmiarze się dekoduje.
- Dane do testów i weryfikacji wyłącznie wymyślone; obrazy generowane (strażnik danych rodziny).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-017-person-photos]] (baza zdjęć, łącza, profilowe) | technical | `done` (2026-10-07) — [[ADR-009-person-photos-record-and-link]] |
| specyfikacja `ui`: ekran kadru, wejście, linie pomocnicze | design | do zrobienia przed planem |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC; ręczna weryfikacja na emulatorze; zmiana
schematu, więc test migracji v4→v5; próbne odtworzenie z kopii przechodzi; zero danych rodziny w zmianach.
