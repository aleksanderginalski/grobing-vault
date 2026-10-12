---
title: "ADR-015 — A cemetery's plan in the database, in the backup (schema v10)"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-027-cemetery-map-plan-photo-states]]"
source: "ISSUE-027 → Implementation plan (Prior art, D2, D3, D5), stop #1 („tak”), stop #2 („ok”) · grobing-code data_state.dart (tabele z sqlite_master), backup_archive.dart, photos.dart (sprzątanie plików bez wiersza) · ADR-003 pkt 1, ADR-004, ADR-008"
created: 2026-10-12
updated: 2026-10-12
---

# ADR-015 — Plan cmentarza w bazie, w kopii (schemat v10)

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-12 (stop #1 [[ISSUE-027-cemetery-map-plan-photo-states]]: D2 = A, „tak”), wdrożone i sprawdzone w tej samej
pozycji:
- migracja v9→v10 z danymi;
- odtworzenie kopii v9 w v10 — cmentarze czekają na plan;
- kopia v10 z planem — test, a na drugim emulatorze odcisk zgodny i plan na ekranie w trybie samolotowym;
- stop #2 „ok”.

Zamknięte 2026-10-12.

**To nie zastępuje [[ADR-003-map-source-offline]]** — wykonuje jego pkt 1 („plan pobiera się raz, przy dodaniu cmentarza, i zostaje
w telefonie”) i rozstrzyga, gdzie plan leży. Sygnał dla `architect` („pierwszy ADR zastąpiony po akceptacji”, retro 2, R7) się nie
zapala.

## Context
- **Plan schematyczny z OSM** — obrys cmentarza i alejki — ma działać bez zasięgu ([[NFR-001-offline]], ADR-003 pkt 1). Pobiera się
  przez Overpass, który bywa zawodny (SPIKE-001 M11; pomiary przy ISSUE-027: 504, „server is probably too busy”).
- **Rozmiar:** duży cmentarz to ok. 70 KB współrzędnych w ramce obrysu, a po odcięciu tego, co poza obrysem, publiczny cmentarz
  testowy ma 2,6 KB obrysu i 11 KB alejek. 11 cmentarzy autora to razem mniej niż 1 MB.
- **Z kodu** (ISSUE-027 → *Prior art*):
  - kopia to migawka całej bazy, a odcisk i „Stan danych” biorą tabele z `sqlite_master` — nowa tabela wchodzi do nich bez zmian w
    kodzie kopii;
  - sprzątanie (`sweepOrphanMedia`) usuwa każdy plik w `media/` bez wiersza, więc plik planu w `media/` by zniknął;
  - odtworzenie porównuje liczbę wierszy każdej tabeli z manifestu, więc migracja nie może dopisywać wierszy.
- **Nowy telefon** ([[NFR-002-odtworzenie-na-nowym-telefonie]]): po odtworzeniu kopii autor może jechać na cmentarz bez zasięgu.

## Decision
1. **Plan to wiersz tabeli `cemetery_plans`:**
   - jeden wiersz na cmentarz (`cemetery_id` jest kluczem głównym i odwołaniem do `cemeteries`);
   - `status`: `ok` albo `notInOsm` (OSM nie ma obrysu przy punkcie);
   - `outline` i `paths` jako JSON samych współrzędnych (6 miejsc, ok. 0,1 m), **bez nazw i znaczników OSM**;
   - `fetched_at` i `server` (host, który odpowiedział).
2. **Brak wiersza = plan jeszcze nie pobrany.** Brak sieci i błąd serwera niczego nie zapisują, więc następny start próbuje znowu.
   „Brak w OSM” się zapisuje i wraca tylko po zmianie punktu (ISSUE-027 D3).
3. **Nowy punkt cmentarza kasuje jego plan** w tej samej transakcji (`updateCemetery`): obrys wybiera punkt. Plan pobrany dla starego
   punktu nie zapisuje się (`savePlan` porównuje punkt).
4. **Plan wchodzi do kopii i do odcisku** — jak każda tabela bazy. Po odtworzeniu na nowym telefonie działa od razu, bez sieci.
5. **Plan nie jest faktem o rodzinie** — to kształt publicznego miejsca, bez twierdzenia. Położenie cmentarza i tak jest w bazie
   (punkt środka).
6. **Migracja v9→v10:** sam `createTable`. Bez nowych wierszy, więc kopie v9 odtwarzają się bez zmian w kodzie odtworzenia, a
   cmentarze z punktem czekają na plan.

## Options considered
| Option | For | Against | Status |
|---|---|---|---|
| **(A) tabela `cemetery_plans` w bazie, w kopii** | plan działa po odtworzeniu bez sieci; kopia, odcisk i „Stan danych” bez zmian w kodzie; status i czas pobrania | kopia rośnie (dla 11 cmentarzy < 1 MB); pobranie planu wywołuje kopię w tle (raz na cmentarz) | **chosen** |
| (B) plik planu poza bazą i poza kopią | kopia mniejsza | po odtworzeniu każdy plan trzeba pobrać ponownie — na cmentarzu bez zasięgu go nie ma; w `media/` sprzątanie by go usunęło | rejected |
| (C) kolumna w `cemeteries` | bez nowej tabeli | bez statusu i czasu pobrania; każdy plan powiększa wiersz czytany przez mapę Polski | rejected |

## Consequences
- **Positive:**
  - plan offline (US-007 AC-1) i po odtworzeniu na nowym telefonie;
  - kopia, odcisk i „Stan danych” („Plany cmentarzy”) bez zmian w kodzie kopii.
- **Negative / trade-offs:**
  - plan to dane publiczne pobrane z serwera — **odświeżenie, gdy OSM się zmieni, nie istnieje** (plan pobiera się raz);
  - odciski sprzed v10 i po v10 nie są porównywalne, jak przy każdej zmianie schematu;
  - kopie odtworzonych starszych wersji mają pustą `cemetery_plans` — testy odtworzenia v4–v8 porównują to wprost.
- **Follow-ups:**
  - kwatery autora ([[ISSUE-028-cemetery-sectors]]) to dane autora, nie OSM — osobna tabela albo kolumny, decyzja przy ISSUE-028;
  - odświeżenie planu (np. „Pobierz plan od nowa” w poprawie cmentarza) — kandydat, gdy autor zobaczy plan, który się zmienił;
  - eksport ([[US-006-eksport-dla-rodziny]]): plan nie jest danymi rodziny — prawdopodobnie poza eksportem, decyzja przy eksporcie.
