---
title: "ADR-011 — Relation claims: on the family (the union) and on each child's link (schema v6)"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-019-family-relations]]"
source: "ISSUE-019 → Implementation plan (Prior art, D1, D3, F1–F7), stop #1 (author: „D1 — ok”, „D3 — na razie to dummy data”, no sex) · GEDCOM 7.0.18 (FAMILY_RECORD, INDIVIDUAL_RECORD → FAMC/FAMS, SEX) · Gramps source (ChildRef, Family, Person) · grobing-code restore_service.dart (row counts after migration) · ADR-006"
created: 2026-10-08
updated: 2026-10-08
---

# ADR-011 — Twierdzenie o relacji: przy rodzinie (związek pary) i przy łączu każdego dziecka

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-08. Autor przyjął D1 i D3 na stopie #1 [[ISSUE-019-family-relations]] („D1 — ok”; D3: *„na razie
to dummy data, więc nic się nie dzieje”*). Wdrożone i sprawdzone w tej samej pozycji:
- test migracji v5→v6 z danymi (F1);
- kopia v5 z rodzinami odtwarza się w v6 (F2);
- kopia z rodzinami i twierdzeniami odtworzona w teście i na drugim emulatorze, z odciskiem zgodnym (F3);
- zapis rodziny jest całością (F4), a reguły trzyma warstwa danych (F5).

## Context
- **FR-001:** relacja to fakt o rodzinie, więc ma źródło i status, jak daty i pochówek (ziarnistość: twierdzenia na
  datach, relacjach i pochówku). [[ADR-006-claimed-value-separate-structures]] D6 zapowiedział: *„relacje dojdą w tym
  samym kształcie (twierdzenie przy wierszu powiązania) migracją przy US-003”*.
- **Kanon — [GEDCOM 7.0.18](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html)** (odczyt 2026-10-07):
  - pod `HUSB`, `WIFE` i `CHIL` w `FAMILY_RECORD` stoi tylko `PHRASE` — **nie ma cytowania przy samym łączu**; cytowanie
    (`SOURCE_CITATION`) stoi przy całym rekordzie `FAM`;
  - pod `FAMC` i `FAMS` osoby też nie ma `SOUR`. `FAMC` ma `STAT` (*„assessing of the state or condition of a researcher's
    belief in a family connection”*: `CHALLENGED` · `DISPROVEN` · `PROVEN`);
  - *„Source citations and notes related to the start of a specific child relationship should be placed under the child's
    BIRT, CHR, or ADOP event, rather than under the FAM record”*;
  - *„The order of the CHIL (children) pointers within a FAM (family) structure should be chronological by birth”*;
  - *„Sex, gender, titles, and roles of partners should not be inferred based on the partner that the HUSB or WIFE
    structure points to”*;
  - sama specyfikacja: *„The structures for representing the strength of and confidence in various claims are known to be
    inadequate and are likely to change in a future version”*.
- **Gramps** (kod źródłowy `gramps-project/gramps`, gałąź `master` 6.1.0-dev, odczyt 2026-10-07; wiki i dokumentacja
  zwróciły 403): `ChildRef` ma **własne cytowania** i osobny rodzaj relacji do ojca i do matki; `Family` ma cytowania;
  partnerzy (`father_handle`, `mother_handle`) — bez własnych.
- **Z kodu:** odtworzenie kopii sprawdza po migracji, że **każda tabela z manifestu ma tę samą liczbę wierszy**
  (`restore_service.dart` → `_migrate`). Przed v6 rodziny pisały tylko wymyślone dane debug — formularza rodziny nie
  było (na dwóch emulatorach w buildzie release: 0 rodzin).
- **Decyzja autora na stopie #1:** bez płci w modelu („nie czuję potrzeby”); rodzina to **związek**, nie tylko
  małżeństwo (uwaga autora o rozstaniach, owdowieniach i nowych związkach).

## Decision
1. **Twierdzenie o parze stoi przy rodzinie:** `assertions.family_id`. Para to jeden fakt („byli parą”), jak cytowanie
   `FAM` w GEDCOM 7 i cytowania `Family` w Gramps. Inny partner to inna rodzina — osobny wiersz, jak sprzeczna wartość w
   [[ADR-006-claimed-value-separate-structures]] D1.
2. **Twierdzenie o dziecku stoi przy jego łączu:** `family_children` dostaje `id` (stary `rowid`) i UNIQUE (rodzina,
   osoba), a `assertions.family_child_id` cytuje łącze — jak `ChildRef` w Gramps i `FAMC.STAT` w GEDCOM. Spór „to nie
   było ich dziecko” ([[US-004-fakt-od-babci]]) dotyczy jednego dziecka.
3. **Twierdzenie cytuje dokładnie jeden wiersz:** zdarzenie, pochówek, rodzinę albo łącze dziecka — `CHECK` na sumie
   czterech kolumn. `family_partners` bez zmian.
4. **Migracja v5→v6 nie dodaje wierszy (D3):** przebudowuje `family_children` i `assertions` (`TableMigration`, te same
   wiersze i `id`). Dopisanie twierdzeń do rodzin sprzed v6 zmieniłoby liczbę wierszy `assertions` i odtworzenie każdej
   kopii v5 z rodzinami by odmówiło. Rodzina i łącza bez twierdzenia dostają je przy pierwszym zapisie w arkuszu
   rodziny (`families.dart` → `saveFamily`). Inaczej niż v1→v2 ([[ADR-006-claimed-value-separate-structures]] D5): tam
   `assertions` była nową tabelą.
5. **Płci w modelu nie ma** (decyzja autora). Nazwy relacji są neutralne („Rodzic”, „Partner”, „Dziecko”). Płeć, gdyby
   wróciła, stoi przy osobie — GEDCOM nie wyprowadza jej z miejsca w parze.

## Options considered
| Option | For | Against | Status |
|---|---|---|---|
| **(a) przy rodzinie (para) i przy łączu dziecka** | łączy oba kanony: GEDCOM cytuje `FAM`, Gramps — `ChildRef`; jedno dziecko da się zakwestionować; `family_partners` bez przebudowy | odchodzi od dosłownego brzmienia ADR-006 D6 przy parze; przypadek „jedno źródło potwierdza jednego partnera, a przeczy drugiemu w tej samej rodzinie” się nie zmieści | **chosen** |
| (b) przy każdym łączu — partnera i dziecka | dosłownie ADR-006 D6 | para to jeden fakt, a żaden kanon nie cytuje przy samym partnerze; druga przebudowa tabeli bez zysku | rejected — wraca, gdyby obalił (a) przypadek z kolumny wyżej |
| (c) tylko przy rodzinie (GEDCOM 1:1) | najprostsze | nie umie zakwestionować jednego dziecka (US-004) | rejected |
| (d) dziecko przez zdarzenie urodzenia z `FAMC` (zalecenie GEDCOM) | zgodne z zaleceniem GEDCOM | miesza źródło daty urodzenia ze źródłem rodziców; dziecko bez daty potrzebowałoby pustego zdarzenia; `events` ma `CHECK` „osoba albo rodzina” | rejected |
| (e) jedna tabela `family_members` zamiast dwóch | jedno miejsce na łącza | migracja usuwa tabele, a odtworzenie kopii v5 liczy wiersze każdej tabeli z manifestu ([[NFR-003-migracje-schematu]]) | rejected |

## Consequences
- **Positive:**
  - każda nowa rodzina ma twierdzenie „notatki”, `CLAIMED`, a każde łącze dziecka — swoje (AC-4 [[US-003-przepisanie-rodziny]]);
  - usunięcie dziecka z rodziny zabiera twierdzenia jego łącza; „Usuń rodzinę” — wszystko, co cytuje rodzinę, jej łącza i
    jej zdarzenia; osoby zostają;
  - kopie v5 odtwarzają się w v6 bez zmian w kodzie odtworzenia; odcisk danych obejmuje nowe kolumny sam.
- **Negative / trade-offs:**
  - **relacje sprzed v6 nie mają twierdzeń**, dopóki rodzina nie zostanie zapisana w arkuszu — w buildzie release takich
    rodzin nie ma, w bazach debug sprzed v6 są;
  - eksport do GEDCOM (C2) będzie musiał przełożyć twierdzenie łącza dziecka na `FAMC.STAT` albo cytowanie przy
    urodzeniu z `FAMC` — GEDCOM nie ma cytowania przy samym `CHIL`;
  - odciski sprzed v6 i po v6 nie są porównywalne, jak przy każdej zmianie schematu.
- **Follow-ups:**
  - kontrola cykli (osoba w parze ze swoim dzieckiem, ktoś swoim przodkiem) — poza zakresem ISSUE-019; aplikacja dziś na
    to pozwala (obserwacja ze stopu #2). Kandydat na małą pozycję;
  - rodzaj więzi dziecka (przysposobienie — `PEDI` w GEDCOM, rodzaje `ChildRef` w Gramps) i druga rodzina rodziców —
    [[US-004-fakt-od-babci]] albo osobna pozycja;
  - płeć — wraca jako pole osoby z migracją, gdyby nazwy ścieżki albo drzewa (EPIC-003) jej potrzebowały; pomiar
    podpowiedzi z imienia (PESEL) jest w [[ISSUE-019-family-relations]] → *Prior art*.
