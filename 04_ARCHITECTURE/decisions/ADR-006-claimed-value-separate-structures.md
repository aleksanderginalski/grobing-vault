---
title: "ADR-006 — Where a claimed value lives: separate rows with citations, as in GEDCOM 7"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-011-schema-v2-assertions]]"
source: "FR-001 (provenance) · FR-003 · FR-004 · US-004 AC-1 · data-model.md → In code (ISSUE-007 D2) · GEDCOM 7.0.18 · ADR-004 pkt 5 (restore migrates older backups)"
created: 2026-10-06
updated: 2026-10-08
---

# ADR-006 — Gdzie żyje wartość twierdzenia

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-06. Kierunek i D2 zaakceptował autor na stopie #1 [[ISSUE-011-schema-v2-assertions]].
Falsyfikator zmierzono przed wyborem, a schemat v2 wdrożono i sprawdzono w tej pozycji (migracja na
emulatorze). Pomiary są w pozycji (*Implementation plan* → *Prior art*, *Falsifier*; *Verification*) i
tam zostają (jedna liczba, jeden dom).

## Context
- [[FR-001-provenance]]: każde twierdzenie o **datach, relacjach i miejscu pochówku** ma źródło, status,
  czas i to, kto je podał. **Dwa sprzeczne twierdzenia współistnieją**, a `CONTRADICTED` się nie usuwa.
- Schemat v1 ([[ISSUE-007-data-layer]], D2) pominął *Assertion*, bo model nie mówił, **gdzie żyje
  wartość spornej daty: w *Event* czy w *Assertion***. W v1 *Event* już trzyma datę z dopiskiem
  ([[FR-004-data-z-dopiskiem]]), a *Burial* miał `person_id` UNIQUE.
- Na tym schemacie staną dane około 100 osób. Zła decyzja wyszłaby przy [[US-004-fakt-od-babci]], kiedy
  da się ją naprawić już tylko migracją prawdziwych danych.
- **Kanon:** brief wskazuje GEDCOM jako punkt odniesienia dla własnego modelu, bez importu i eksportu.
  [GEDCOM 7.0.18](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html):
  - §3.2.3 *EVENT_DETAIL*: *„Conflicting event information should be represented by placing them in
    separate event structures (with appropriate source citations) rather than by placing them under the
    same enclosing event.”*
  - §3.1: *„the first is the most-preferred value”*;
  - §3.2.3 *SOURCE_CITATION* (`{0:M}` na zdarzeniu): *„connects a claim with the source documenting that
    claim”*.
- **Kontrakt odtworzenia:** po migracji starszej kopii każda tabela z jej manifestu musi istnieć z tą
  samą liczbą wierszy ([[ADR-004-backup-format-encryption-destination]] pkt 5, `restore_service.dart`).

## Decision
**Wartość żyje w wierszu, a twierdzenie jest cytowaniem przy nim, jak w GEDCOM 7.**
- **D1:** data z dopiskiem zostaje w `events`, grób w `burials`. **Wartość sprzeczna** z innym źródłem to
  **osobny wiersz**. Tabela `assertions` to 1..N twierdzeń na wiersz `events` **albo** `burials`. Drugie
  źródło dla tej samej wartości to drugie twierdzenie, nie drugi wiersz.
- **D2 (decyzja autora):** „osoba ma co najwyżej jeden pochówek” ([[FR-003-wiele-osob-w-grobie]]) to
  **fakt**, nie wiersz: człowiek leży w jednym miejscu, ale źródła mogą się co do niego różnić.
  `burials` traci UNIQUE na `person_id`, dostaje `id` i UNIQUE (`person_id`, `grave_id`).
- **D3:** pokazuje się **pierwszy** wiersz (najniższe `id`), jak w GEDCOM §3.1. W v2 nie ma kolumny
  „preferowana”.
- **D4:** źródło = **rodzaj** z FR-001 (nagrobek · notatki · babcia · krewny · akt) + opcjonalny
  **szczegół** (który krewny, który akt) + **kiedy zapisane**; do tego status. Bez tabeli źródeł.
- **D5:** każdy wiersz `events` i `burials` ma ≥ 1 twierdzenie (niezmiennik pilnowany przez kod zapisu
  i testy). Wiersze z v1 dostały przy migracji twierdzenie „notatki, `CLAIMED`, przeniesione z v1”:
  prawdziwych danych w v1 nie było, a jedyną zaplanowaną drogą dat do v1 było przepisanie notatek.
- **D6:** relacje dojdą w tym samym kształcie (twierdzenie przy wierszu powiązania) migracją przy
  [[US-003-przepisanie-rodziny]].

Status z FR-001 (`CLAIMED` · `CONFIRMED` · `CONTRADICTED` · `UNKNOWN`) zostaje własny Grobing. GEDCOM-owe
`QUAY` ocenia siłę dowodu, a nie relację między źródłami, więc nie wchodzi.

## Options considered

| Option | Pros | Cons | Why (not) chosen |
|---|---|---|---|
| **B — osobne wiersze z twierdzeniami (GEDCOM 7)** | zgodne z kanonem 1:1; wartość ma jeden dom; v1 już dopuszczał kilka zdarzeń tego samego typu, więc dla dat migracja tylko dokłada tabelę; tabele v1 zostają, więc kopie v1 się odtwarzają | lista wszystkich twierdzeń o osobie to suma po kilku tabelach; „która wartość pokazać” to osobna reguła (D3) | **wybrane** — przeszło wszystkie przypadki falsyfikatora |
| A — jedno zdarzenie danego typu na osobę, twierdzenie 1:1 przy nim | najprostsze; jedna wartość do pokazania | sprzeczna data i drugi grób nie mają się gdzie zmieścić (odmowa UNIQUE); potwierdzenie też nie | rejected — obalone falsyfikatorem (US-004 AC-1) |
| C — wartość w tabeli twierdzeń (jedna tabela faktów zamiast dat w *Event* i grobu w *Burial*) | wszystkie twierdzenia w jednym miejscu | polimorficzna tabela z wieloma pustymi kolumnami; odchodzi od encji modelu i od kanonu; **kasuje `events` i `burials`, więc żadna kopia v1 by się nie odtworzyła** | rejected — łamie kontrakt odtworzenia |
| D — wniosek + dowody: *Event* trzyma jedną wartość preferowaną, każde twierdzenie własną kopię wartości | rozdziela wniosek od dowodów (Genealogical Proof Standard) | wartość ma dwa domy; schemat przyjmuje wartość bez żadnego zgodnego twierdzenia (zmierzone) | rejected — wartość bez źródła to dokładnie to, czemu FR-001 ma zapobiec |

## Consequences
- **Positive:**
  - spór źródeł z US-004 jest zapisywalny już w v2; US-004 dokłada funkcję, nie migrację;
  - wybór wartości do pokazania jest odwracalny (D3 → kolumna przy US-004), a miejsce wartości nie musi
    się zmieniać;
  - eksport (US-006, GEDCOM jako nice-to-have) mapuje się wprost: wiersz → struktura zdarzenia,
    twierdzenie → `SOURCE_CITATION`, rodzaj i szczegół → rekord `SOUR`.
- **Negative / trade-offs:**
  - **osoba, o której źródła się spierają, pojawia się w widoku obu grobów.** Oznaczenie tego to US-004;
  - niezmiennika D5 nie wymusza SQLite (byłyby potrzebne wyzwalacze). Pilnuje go `claims.dart` i testy,
    więc każdy nowy kod zapisu musi przez nie przechodzić;
  - status `CONTRADICTED` przy drugim twierdzeniu ustawi dopiero US-004. Do tego czasu robią to tylko
    testy i dane debug.
- **Follow-ups:**
  - [[US-003-przepisanie-rodziny]]: przed planem ten sam falsyfikator dla sprzecznej relacji (rodzic według
    notatek i według babci) jako osobnego wiersza powiązania (D6).
  - [[US-004-fakt-od-babci]]: przejścia statusów, wybór wartości preferowanej (kolumna, migracja) i
    oznaczenie sporu w widokach.
  - Gdyby trzeba było wskazać ten sam dokument (np. jeden akt) z wielu faktów i poprawiać go w jednym
    miejscu, przyjdzie tabela źródeł migracją (D4).
  - **2026-10-08 — D6 doprecyzowany w [[ADR-011-relation-claims-family-and-child-link]]** ([[ISSUE-019-family-relations]]):
    twierdzenie o parze stoi przy rodzinie (para to jeden fakt, jak cytowanie `FAM` w GEDCOM 7), a o dziecku — przy jego
    łączu (jak `ChildRef` w Gramps). Sprzeczna relacja to osobny wiersz: inny partner — inna rodzina, inni rodzice —
    inne łącze dziecka (to drugie zostaje [[US-004-fakt-od-babci]]). Migracja v5→v6 nie dopisała twierdzeń rodzinom
    sprzed v6 — inaczej niż D5 przy v1→v2, bo `assertions` nie była już nową tabelą.

## Follow-ups — 2026-10-08 ([[SPIKE-004-mvp-flow-prototype]] D28)
**Wymaganie, które ta decyzja niosła ([[FR-001-provenance]]), autor wycofał:** *„a to jakiś błąd się wkradł w takim razie - moje notatki to moje notatki, nie potrzeba żadnych potwierdzeń skąd pochodzą”*. **Struktury zostają** — sprzeczna
wartość dalej mogłaby być osobnym wierszem — ale aplikacja nie pokazuje ani nie zbiera źródła i statusu: formularz zapisuje
domyślne źródło po cichu, a poprawa zastępuje wartość. Bez migracji i bez nowego ADR (struktura się nie zmienia; to nie jest
zastąpienie decyzji, więc nie jest to sygnał dla agenta `architect`).
