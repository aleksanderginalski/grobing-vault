---
title: "ADR-016 — A sector is a record of its cemetery; a grave points at its sector (schema v11)"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-028-cemetery-sectors]]"
source: "ISSUE-028 → Implementation plan (Prior art, D2, D3), stop #1 („tak”: D2 = A — W-a), stop #2 („pomiń”) · 05_DESIGN/cmentarz.md v6.1 (*Open* W-a/W-b), grob.md v6 · data-model.md (Sector, planowana encja) · ADR-003 pkt 3, ADR-015 · grobing-code restore_service.dart (liczby wierszy przed migracją), cemeteries.dart (nowy punkt kasuje plan)"
created: 2026-10-12
updated: 2026-10-12
---

# ADR-016 — Kwatera jako rekord cmentarza, grób wskazuje kwaterę (schemat v11)

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-12 (stop #1 [[ISSUE-028-cemetery-sectors]]: D2 = A, wariant W-a — „tak”), wdrożone i sprawdzone w tej samej
pozycji:
- migracja v10→v11 z danymi (tekst kwatery → wiersze, „B” i „b” jedna kwatera);
- odtworzenie kopii v10 w v11 — kwatera z tekstu staje się rekordem, adres czyta się tak samo;
- kopia v11 z kwaterą, strefą i adresem — test, a na drugim emulatorze odcisk zgodny i strefa na planie w trybie samolotowym;
- stop #2 „pomiń”.

Zamknięte 2026-10-12.

**To nie zastępuje [[ADR-003-map-source-offline]]** — wykonuje jego pkt 3 („kwatera to nazwana strefa, którą autor zaznacza … według
planu zarządcy”) i jego *Follow-up* „model kwatery: nazwa + strefa”. Nie zastępuje też [[ADR-015-cemetery-plan-in-database]]. Sygnał
dla `architect` („pierwszy ADR zastąpiony po akceptacji”, retro 2, R7) się nie zapala.

## Context
- **Adres zarządcy jest prawdą, pinezka pomocą** ([[data-model]] → Grave). Systemy zarządców podają adres jako *sektor / rząd / numer*
  (SPIKE-001, M1–M3), a autor przepisuje go z wyszukiwarki zarządcy ([[EPIC-002-wizyta]] → *Open questions*, krok 1).
- **Kwatera ma dwie role:** jest częścią adresu grobu i strefą na planie, którą zaznacza autor (US-007 AC-4). Kwatera bez strefy żyje
  tylko w adresach. [[data-model]] planował **Sector** jako encję (nazwa, cmentarz, strefa opcjonalna) i zostawił wybór „encja czy
  tekst” pierwszej US mapy cmentarza.
- **Do v10 kwatera była tekstem** `graves.sector`. Zapisywały go tylko wymyślone dane w buildzie debug, bo żaden ekran nie miał pola
  adresu (luka M1, znaleziona przy specyfikacji ISSUE-028). Prawdziwe dane rodziny wejdą do aplikacji dopiero po instalacji MVP.
- **Z kodu** (ISSUE-028 → *Prior art*):
  - plan cmentarza (ADR-015) kasuje się przy zmianie punktu cmentarza, więc strefy w `cemetery_plans` zniknęłyby razem z nim;
  - odtworzenie liczy wiersze tabel kopii w jej wersji, więc migracja może przebudować tabelę i dodać nową, ale nie może zgubić wiersza.

## Decision
1. **Tabela `sectors`:**
   - `id`, `cemetery_id` → `cemeteries`;
   - `name` — jak wpisał autor, bez słowa „Kwatera” na początku;
   - `name_key` — nazwa bez wielkości liter i polskich znaków, **unikalna razem z `cemetery_id`**, więc „b” i „B” to jedna kwatera;
   - `zone` — JSON pierścienia współrzędnych w tym samym formacie co plan (6 miejsc po przecinku); `NULL` oznacza kwaterę bez strefy.
2. **Grób wskazuje kwaterę:** `graves.sector_id` → `sectors` zamiast tekstu `sector`. Rząd i miejsce zostają tekstem w grobie, bo
   zarządcy piszą „12a” i „IV”.
3. **Zmiana nazwy kwatery to jeden wiersz** — adresy wszystkich jej grobów mówią nową nazwę od razu.
4. **Kwatera bez strefy i bez grobów znika** w tej samej transakcji, w której straciła ostatni grób albo strefę. „Usuń z planu” zdejmuje
   tylko strefę, a adresy grobów zostają ([[cmentarz]] D27).
5. **Normalizacja nazwy jest w jednym miejscu** (`grobing-code` `lib/data/address_text.dart`), wspólnym dla okien, zapisu i migracji.
6. **Kwatery to dane autora** — wchodzą do kopii i odcisku jak każda tabela bazy. Nie są faktami o rodzinie w rozumieniu
   [[FR-001-provenance]] (to dane miejsca), bez twierdzeń.
7. **Migracja v10→v11:** `createTable(sectors)` → kwatera dla każdego różnego `name_key` z tekstu na cmentarzu (pisownia pierwszego
   grobu) → przebudowa `graves` bez kolumny tekstu (`TableMigration`, wiersze i `id` bez zmian) → `sector_id` → `PRAGMA
   foreign_key_check`. Liczba grobów się nie zmienia, a `sectors` jest nowa, więc kopie v10 odtwarzają się bez zmian w kodzie
   odtworzenia.

## Options considered
| Option | For | Against | Status |
|---|---|---|---|
| **(A) rekord `sectors`, grób wskazuje kwaterę (W-a)** | jedna nazwa w jednym wierszu: zmiana nazwy poprawia wszystkie adresy; „b” = „B”, więc literówka nie robi drugiej kwatery; lista kwater cmentarza (także bez strefy) do wyboru w adresie; teraz bez kosztu danych, bo żaden prawdziwy grób nie ma adresu | przebudowa `graves` w migracji; adres to złączenie, nie sam wiersz grobu | **chosen** |
| (B) tekst w grobie, strefa osobno po nazwie (W-b) | migracja to sam `createTable`; adres dowolnym tekstem | zmiana nazwy strefy nie rusza adresów, więc groby przestają pasować do strefy; „b” i „B” to dwie kwatery; przejście na A po instalacji MVP byłoby migracją prawdziwych adresów rodziny | rejected (stop #1) |
| (C) strefy w `cemetery_plans` | bez nowej tabeli | plan kasuje się przy zmianie punktu (ADR-015) — kwatery autora by zniknęły; plan to dane OSM, kwatery to dane autora | rejected |

## Consequences
- **Positive:**
  - US-007 AC-4 (strefa z nazwą, kwatera bez strefy tylko w adresach) i adres grobu (luka M1) na jednym modelu;
  - kwatery i adresy w kopii, odcisku i „Stanie danych” („Kwatery”) bez zmian w kodzie kopii.
- **Negative / trade-offs:**
  - odciski sprzed v11 i po v11 nie są porównywalne (zmieniły się kolumny `graves`), jak przy każdej zmianie schematu;
  - migracja scala „b” i „B” — pisownia pierwszego grobu wygrywa dla wszystkich (dziś dotyczy tylko danych debug);
  - testy odtworzenia v4–v10 porównują pustą `sectors` wprost.
- **Follow-ups:**
  - kwatera w eksporcie dla rodziny ([[US-006-eksport-dla-rodziny]]): adres tak, strefa prawdopodobnie nie — decyzja przy eksporcie;
  - na miejscu „Pokaż kwaterę” przy grobie bez pinezki i lista grobów kwatery — kandydaci dla [[US-008-pinezka-na-miejscu]] ([[cmentarz]] D29);
  - edytor pojedynczego rogu strefy — gdy autor będzie wiele razy poprawiał jeden róg ([[cmentarz]] D26).
