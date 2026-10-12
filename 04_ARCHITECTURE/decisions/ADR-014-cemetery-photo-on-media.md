---
title: "ADR-014 — A cemetery's photo: a media row pointing at the cemetery (schema v9)"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-023-poland-map-r1-cemetery-photo]]"
source: "ISSUE-023 → Implementation plan (Prior art, D1), stop #1 („tak”), stop #2 („ok”) · grobing-code photos.dart (setGravePhoto, applyPersonPhotoEdits, sweepOrphanMedia) · restore_service.dart (liczniki wierszy po migracji) · ADR-008, ADR-009"
created: 2026-10-12
updated: 2026-10-12
---

# ADR-014 — Zdjęcie cmentarza: wiersz `media` z odwołaniem do cmentarza (schemat v9)

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-12 (stop #1 [[ISSUE-023-poland-map-r1-cemetery-photo]]: D1 = A, „tak”), wdrożone i sprawdzone w tej samej
pozycji: migracja v8→v9 z danymi, odtworzenie kopii v8 w v9 (cmentarze bez zdjęć), kopia v9 ze zdjęciem cmentarza (test) i na
drugim emulatorze (odcisk zgodny), stop #2 „ok”. Zamknięte 2026-10-12.

**To nie zastępuje [[ADR-008-photos-access-copy-and-backup-consistency]] ani [[ADR-009-person-photos-record-and-link]]** —
rozszerza wzór zdjęcia nagrobka o drugie miejsce. Sygnał dla `architect` („pierwszy ADR zastąpiony po akceptacji”, retro 2, R7) się
nie zapala.

## Context
- **Zdjęcie cmentarza w arkuszu na mapie** ([[SPIKE-004-mvp-flow-prototype]] D5, [[cmentarze]] 6a, D28): jedno zdjęcie na
  cmentarz, zrobione przez autora — miniatura 96 × 80 dp, podgląd ze „Zmień” i „Usuń” jak przy nagrobku. Zmiana zakresu wobec
  briefu (M1 ma zdjęcie nagrobka) — decyzja autora.
- **Z kodu** (ISSUE-023 → *Prior art*):
  - zdjęcie nagrobka to wiersz `media` z `grave_id`; zapis: plik przed wierszem, usunięcie zdejmuje tylko wiersz, plik idzie przy
    sprzątaniu (ADR-008);
  - `applyPersonPhotoEdits` kasuje każdy wiersz `media` bez właściciela — przed v9 „bez grobu i bez łącza osoby”. Wiersz zdjęcia
    cmentarza nie ma ani jednego, ani drugiego: bez nowego warunku każde „Zapisz” przy zdjęciach osoby skasowałoby zdjęcia
    cmentarzy;
  - odtworzenie kopii po migracji porównuje liczbę wierszy każdej tabeli z manifestu (`restore_service.dart`), więc migracja nie
    może dopisywać wierszy.

## Decision
1. **Zdjęcie cmentarza to wiersz `media` z kolumną `cemetery_id`** (pusta, klucz do `cemeteries`) — lustro `grave_id`. Pliki w
   `media/cmentarze/<id>/<czas>-<losowe>.jpg`, nigdy z treści zdjęcia.
2. **Jedno zdjęcie na cmentarz** pilnuje jedna droga zapisu, wspólna z nagrobkiem (`photos.dart` → `_setPlacePhoto`); przy kilku
   wierszach pokazuje się pierwszy według `id` (jak [[grob]] D9). SQL tego nie wymusza — tak jak przy nagrobku.
3. **Sierota = wiersz bez grobu, bez cmentarza i bez łącza osoby** (`applyPersonPhotoEdits`); test z mutacją pilnuje warunku.
4. **Zdjęcie cmentarza nie jest faktem o rodzinie** — bez twierdzenia, jak nagrobek.
5. **Migracja v8→v9:** sam `addColumn`. Bez nowych wierszy i bez przebudowy tabeli, więc kopie v8 odtwarzają się bez zmian w kodzie
   odtworzenia, a cmentarze nie mają zdjęć.

## Options considered
| Option | For | Against | Status |
|---|---|---|---|
| **(A) `media.cemetery_id`, lustro `grave_id`** | wzór nagrobka: ta sama droga zapisu, sprzątanie i kopia; migracja jednym `addColumn` | „jedno na cmentarz” pilnuje kod, nie SQL; warunek sieroty trzeba rozszerzyć (zrobione, z testem) | **chosen** |
| (B) `cemeteries.photo_media_id` → `media` | jedno zdjęcie wymuszone kształtem | klucz z cmentarza blokuje sprzątanie wiersza zdjęcia; zmiana zdjęcia to dwa zapisy w dwóch tabelach | rejected |
| (C) osobna tabela `cemetery_media` | gotowa na kilka zdjęć cmentarza | D28 chce jednego; jedna tabela więcej w kopii i w liczeniu wierszy przy odtworzeniu | rejected |

## Consequences
- **Positive:**
  - arkusz cmentarza ma zdjęcie (AC-3); kopia i odtworzenie niosą je bez zmian w kodzie kopii — cały katalog `media/` wchodzi do
    kopii, a odcisk obejmuje kolumnę;
  - nagrobek i cmentarz mają jedną implementację zapisu, więc kolejność „plik przed wierszem” żyje w jednym miejscu.
- **Negative / trade-offs:**
  - każde nowe miejsce ze zdjęciem (np. kwatera) musi dopisać się do warunku sieroty — inaczej `applyPersonPhotoEdits` je skasuje;
  - odciski sprzed v9 i po v9 nie są porównywalne, jak przy każdej zmianie schematu.
- **Follow-ups:**
  - eksport ([[US-006-eksport-dla-rodziny]]): zdjęcie cmentarza jako `OBJE` przy miejscu albo pominięte — decyzja przy eksporcie;
  - zdjęcie cmentarza na ekranie [[cmentarz]] i miniatury w wyszukiwarce — poza ISSUE-023 ([[cmentarze]] D28 → *obali*).
