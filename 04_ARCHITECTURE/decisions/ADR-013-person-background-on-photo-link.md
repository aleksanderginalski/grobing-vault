---
title: "ADR-013 — A person's background photo: a mark on the person–photo link (schema v8)"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-024-person-view]]"
source: "ISSUE-024 → Implementation plan (Prior art, D3), stop #1 („2 ok / 3 ok / 4 ok”), stop #2 (runda 1: tło z pasma — D21; runda 2: „ok”) · GEDCOM 7.0 (MULTIMEDIA_LINK: CROP, TITL) · grobing-code photos.dart (applyPersonPhotoEdits przepisuje łącza) · restore_service.dart (liczniki wierszy po migracji) · ADR-009, ADR-010"
created: 2026-10-12
updated: 2026-10-12
---

# ADR-013 — Tło osoby: znacznik przy łączu osoba–zdjęcie (schemat v8)

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-09 (stop #1 [[ISSUE-024-person-view]]: D3 „ok” — wariant A), wdrożone i sprawdzone w tej samej pozycji:
migracja v7→v8 z danymi, odtworzenie kopii v7 w v8 (bez tła), kopia v8 z tłem na drugim emulatorze (odcisk zgodny), stop #2
„ok”. Zamknięte 2026-10-12.

**To nie zastępuje [[ADR-009-person-photos-record-and-link]] ani [[ADR-010-profile-photo-crop-pixels]]** — dokłada kolumnę przy
łączu, tak jak ADR-010 dołożył kadr. Sygnał dla `architect` („pierwszy ADR zastąpiony po akceptacji”, retro 2, R7) się nie
zapala (ISSUE-024 D3).

## Context
- **Zdjęcie w tle widoku osoby** ([[SPIKE-004-mvp-flow-prototype]] D17, [[osoba]] D3): autor wybiera je spośród zdjęć osoby
  (dom, wieś, zdjęcie grupowe). Każda osoba ma własne tło, także na wspólnym zdjęciu.
- **Kanon — [GEDCOM 7.0](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html)** (odczyt kopii z 2026-10-07):
  `MULTIMEDIA_LINK` ma tylko `CROP` i `TITL`. **Tła ani „okładki” standard nie zna** — to rozszerzenie aplikacji. Kolejność
  łączy (*„the first is the most-preferred value”*) niesie profilowe.
- **Z kodu:**
  - `applyPersonPhotoEdits` (`photos.dart`) przy każdym zapisie **przepisuje łącza osoby od zera** i czyta kadry przed
    skasowaniem, żeby je oddać (ISSUE-018, plan F1);
  - odtworzenie kopii po migracji porównuje liczbę wierszy każdej tabeli z manifestu (`restore_service.dart` → `_migrate`), więc
    migracja nie może dopisywać wierszy;
  - drift 2.34.0 ma `@TableIndex.sql`, więc częściowy indeks unikalny da się zapisać w schemacie.

## Decision
1. **Tło to znacznik przy łączu:** `person_media.is_background` (`boolean`, domyślnie `false`). Usunięcie łącza („Usuń z tej
   osoby”, odznaczenie w „Kto jest na zdjęciu?”) samo zdejmuje tło.
2. **Jedno tło na osobę:** częściowy indeks unikalny `person_media_background` na `person_id` `WHERE is_background`; ustawienie
   nowego tła przenosi znacznik.
3. **Zapis jedną drogą:** `applyPersonPhotoEdits` — jak kadr: tło zapisanego łącza, którego edycja nie dotyka, czyta przed
   przepisaniem i oddaje; jawna zmiana (`backgroundChanged`) ustawia albo zdejmuje. Z formularza zapisuje się z „Zapisz”, z
   pasma w widoku osoby — od razu, tą samą funkcją, we własnej transakcji ([[osoba]] D21).
4. **Tło nie jest faktem o rodzinie** — bez twierdzenia, jak profilowe i kadr ([[FR-001-provenance]]).
5. **Migracja v7→v8:** `addColumn` + `createIndex`. Żadnego wiersza nie przybywa, więc kopie v7 odtwarzają się bez tła i bez
   zmian w kodzie odtworzenia.

## Options considered
| Option | For | Against | Status |
|---|---|---|---|
| **(A) kolumna `is_background` przy łączu + częściowy indeks unikalny** | wzór jak kadr przy łączu (ADR-010); usunięcie łącza samo zdejmuje tło; każda osoba na wspólnym zdjęciu ma własne; migracja bez wierszy | tło musi przejść przez przepisywanie łączy (jak kadr) — jedna droga zapisu to pilnuje | **chosen** |
| (B) `persons.background_media_id` → `media` | przeżywa przepisanie łączy bez pracy | przy usunięciu łącza trzeba czyścić osobno; klucz do `media` blokuje sprzątanie wiersza zdjęcia bez łączy; dwa miejsca opisują jedno | rejected |
| (C) osobna tabela „tło osoby” | rozdział od łączy | jak B, z jedną tabelą więcej w kopii i w liczeniu wierszy przy odtworzeniu | rejected |

## Consequences
- **Positive:**
  - widok osoby ma tło nad portretem (AC-5); kopia i odtworzenie niosą je bez zmian w kodzie kopii (odcisk obejmuje kolumnę);
  - tło na wspólnym zdjęciu jest osobne dla każdej osoby; zdjęcie usunięte z osoby nie zostawia „wiszącego” tła.
- **Negative / trade-offs:**
  - każdy, kto przepisuje łącza osoby, musi oddać znacznik (dziś jedna droga: `applyPersonPhotoEdits`, z testem);
  - odciski sprzed v8 i po v8 nie są porównywalne, jak przy każdej zmianie schematu.
- **Follow-ups:**
  - eksport ([[US-006-eksport-dla-rodziny]]): tło jako rozszerzenie (np. tag z podkreśleniem) albo pominięte — decyzja przy
    eksporcie;
  - zdjęcie dodane jako tło osobie bez zdjęć staje się też jej profilowym (pierwsze łącze, ADR-009) — tak zostaje, profilowe
    zmienia się pod ✎ ([[osoba]] D21).
