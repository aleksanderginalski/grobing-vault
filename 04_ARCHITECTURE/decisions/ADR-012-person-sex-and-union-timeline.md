---
title: "ADR-012 — A person's sex and the union as a timeline: together since, wedding, end (schema v7)"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-025-gender-kinship-together-since]]"
source: "ISSUE-025 → Implementation plan (Prior art, rundy 0–2), stop #1 (autor: ewolucja związku w kreatorze; „C1 / P1 / Jest dobrze”), stop #2 („ok”) · GEDCOM 7.0 (SEX, MARR, payload Y, FAM, EVEN+TYPE) · ISSUE-019 → Prior art (pomiar PESEL) · grobing-code restore_service.dart (liczniki wierszy po migracji) · ADR-011"
created: 2026-10-08
updated: 2026-10-08
---

# ADR-012 — Płeć osoby i związek jako oś czasu (schemat v7)

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-08. Autor przyjął plan na stopie #1 [[ISSUE-025-gender-kinship-together-since]] w dwóch rundach: w
pierwszej odrzucił oba warianty rodzaju związku (przełącznik albo same daty) i opisał trzeci — **związek, który
„ewoluuje”**, wpisywany kreatorem krok po kroku; w drugiej: *„C1 / P1 / Jest dobrze”*. Wdrożone i sprawdzone w tej samej
pozycji: migracja v6→v7 z danymi, odtworzenie kopii v6 w v7, próbne odtworzenie kopii v7 na drugim emulatorze (odcisk
zgodny), stop #2 „ok”.

**To nie zastępuje [[ADR-011-relation-claims-family-and-child-link]].** Jego decyzja — gdzie stoją twierdzenia o relacji —
zostaje. Pkt 5 ADR-011 („płci w modelu nie ma”) sam zapowiadał powrót płci w *Follow-ups*; ADR-011 dostaje datowany dopisek.
Sygnał dla `architect` („pierwszy ADR zastąpiony po akceptacji”, retro 2, R7) się nie zapala (ISSUE-025 D4).

## Context
- **Powrót płci** ([[SPIKE-004-mvp-flow-prototype]] D16): nazwy relacji przy osobie (Matka, Mąż, Córka) i pokrewieństwa w
  widoku osoby (stryj, wuj, siostra cioteczna — [[osoba]] D4) zależą od płci i od strony ścieżki.
- **Dwa tryby związku** (SPIKE-004 D20), w rundzie 1 stopu #1 doprecyzowane przez autora: *„związek może »ewoluować« w
  małżeństwo”* — razem od → ślub → koniec.
- **Kanon — [GEDCOM 7.0](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html)** (odczyt 2026-10-08):
  - `SEX` — *„the sex of the individual at birth”*: `M`, `F`, `X` (*„Does not fit the typical definition of only Male or only
    Female”*), `U` (*„Cannot be determined from available sources”*);
  - `MARR` — *„A legal, common-law, or customary event such as a wedding or marriage ceremony that joins 2 partners…”*;
  - payload `Y` — *„the event is known to have occurred without providing any additional information about it”*;
  - `FAM` *„may also be used for cultural parallels to this, including nuclear families, marriage, cohabitation…”*; tagu na
    początek związku bez ślubu nie ma, a `EVEN` *„must be classified by a subordinate use of the TYPE tag”*.
- **Z kodu:** odtworzenie kopii po migracji porównuje liczbę wierszy każdej tabeli z manifestu (`restore_service.dart` →
  `_migrate`), więc migracja nie może dopisywać wierszy. Typ zdarzenia jest zapisany nazwą (`textEnum`), bez `CHECK` na
  wartościach, a `CHECK` na `events` traktuje każdy typ spoza osoby jako zdarzenie rodziny.
- **Pomiar podpowiedzi płci z imienia** (rejestr PESEL, [[ISSUE-019-family-relations]] → *Prior art*): 0,066% pomyłek
  wśród zmarłych, z listą wyjątków.

## Decision
1. **Płeć stoi przy osobie:** `persons.sex` — tekst `female` / `male`, **pusty = nieznana** (`U`). `X` bez przypadku w
   notatkach — dojdzie jako nowa wartość na końcu enuma, bez migracji. Płeć nie ma twierdzenia, jak imiona
   ([[FR-001-provenance]]: twierdzenia na datach, relacjach, pochówku).
2. **Podpowiedź płci tylko na ekranie, nigdy w bazie:** formularz i kreator podpowiadają z pierwszego imienia (reguła
   z pomiaru), a zapisuje się to, co widać po dotknięciu „Zapisz”. Osoby sprzed v7 dostają płeć przy pierwszej poprawie.
3. **Związek to oś czasu z trzech zdarzeń rodziny:** `together` („Razem od”, nowy typ — eksport jako `EVEN` z `TYPE`),
   `marriage`, `end`. **Ślub albo koniec, o których wiadomo, że były, a daty nie ma, to zdarzenie bez daty** (jak `MARR Y`),
   z twierdzeniem jak każde inne. „Mąż/Żona” zamiast „Partner/Partnerka” wynika z istnienia zdarzenia ślubu, nie z daty.
4. **Zapis jedną drogą:** `saveFamily` dostaje `together`, `married`, `ended` obok dat; bez flag decyduje sama data, jak
   przed v7. Kreator, podsumowanie i „Dodaj dziecko” budują szkic z obecnej rodziny i jednej zmiany.
5. **Migracja v6→v7 tylko dodaje kolumnę** (`addColumn(persons.sex)`); nowy typ zdarzenia nie potrzebuje kroku. Żadnego
   wiersza nie przybywa, więc kopie v6 odtwarzają się bez zmian w kodzie odtworzenia.

## Options considered
| Option | For | Against | Status |
|---|---|---|---|
| **(a) płeć przy osobie + oś czasu ze zdarzeń; ślub/koniec bez daty = zdarzenie bez daty** | kanon GEDCOM 1:1 (`SEX`, `MARR Y`, `EVEN`+`TYPE`); „ewolucja” związku to zwykłe zdarzenia z datami (oś czasu dla drzewa, M10); migracja bez nowych wierszy | „Razem” bez daty nie zostawia śladu w danych (związek bez zdarzeń) — wystarcza, bo brak ślubu i tak znaczy „razem” | **chosen** |
| (b) kolumna „rodzaj związku” przy rodzinie (razem / małżeństwo) | rodzaj zapisany wprost, także bez dat | dubluje zdarzenie ślubu — dwa źródła prawdy o tym samym (rodzaj „razem” przy ślubie z datą?); przebudowa `families` | rejected |
| (c) same daty (wariant V z rundy 0) — małżeństwo tylko przy dacie ślubu | najprostsze, bez flag | para „żona Jana” z notatek bez daty staje się „Partnerem” — nieprawda; autor odrzucił na stopie #1 | rejected |
| (d) płeć wyliczana z imienia przy odczycie, bez kolumny | zero migracji | niewidoczna zgadywanka w danych i w eksporcie; nie da się poprawić wyjątku ani zapisać „nieznana” | rejected |

## Consequences
- **Positive:**
  - nazwy ról z płci i ślubu (Matka, Mąż, Partnerka, Syn) przy osobie; nazwy pokrewieństwa w widoku osoby mają dane
    ([[ISSUE-024-person-view]]);
  - oś czasu związku jest gotowa dla drzewa (linia przerywana od „Razem od”, ciągła od ślubu — [[drzewo]] D4);
  - kopie v6 odtwarzają się w v7 (test i liczniki); odcisk danych obejmuje nową kolumnę sam.
- **Negative / trade-offs:**
  - osoby sprzed v7 nie mają płci, dopóki ktoś ich nie poprawi — nazwy neutralne („Rodzic”, „Małżonek”, „Dziecko”); do
    instalacji MVP to tylko dane wymyślone;
  - zdarzenie bez daty to nowy przypadek dla każdego, kto czyta `events` (eksport, drzewo): „było, data nieznana”, a nie
    „brak zdarzenia”;
  - odciski sprzed v7 i po v7 nie są porównywalne, jak przy każdej zmianie schematu.
- **Follow-ups:**
  - eksport ([[US-006-eksport-dla-rodziny]]): `together` → `EVEN` + `TYPE`, ślub/koniec bez daty → `MARR Y` / `DIV Y`;
  - płeć `X` — gdy pojawi się przypadek;
  - **do decyzji autora:** wpisywać płeć z odpowiedzi „mama”/„tata” w kreatorze rodziców osobie, która jej nie ma (tylko
    puste pole, nigdy nadpisanie) — pytanie z przeglądu `ui`, na stopie #2 bez odpowiedzi;
  - kontrola cykli w rodzinie — nadal poza zakresem ([[ADR-011-relation-claims-family-and-child-link]] → *Follow-ups*).
