---
title: "US-003 — Enter a whole family at once (przepisanie rodziny)"
type: user-story
status: done
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M1]
journey-steps: "n/a — poza ścieżką (M1, warunek kroku 1 UJ-001)"
FR: ["[[FR-001-provenance]]", "[[FR-002-rodzina-jako-rekord]]", "[[FR-004-data-z-dopiskiem]]"]
NFR: ["[[NFR-003-migracje-schematu]]"]
issues: ["[[ISSUE-019-family-relations]]"]
quality-verdict: APPROVED
verdict-date: 2026-10-08
verdict-reviewer: self-check
source: "PROJECT_BRIEF §5 M1 · §5a G6 · Step 0 (family group sheet) · data-model.md (Family)"
created: 2026-10-05
updated: 2026-10-08
---

# US-003 — Przepisanie rodziny naraz

## Story
**Jako** Zbierający **chcę** wpisać parę i jej dzieci jednym formularzem, **żeby** przepisanie ok. 100
osób z notatek było szybkie (G6), a relacje wynikały z rodzin, nie z pojedynczych powiązań.

## Acceptance Criteria
- **AC-1 — rodzina jednym formularzem.** *When* wpisuję rodzinę *Then* w jednym przebiegu podaję 1-2
  partnerów i dzieci, a nowe osoby powstają przy okazji ([[FR-002-rodzina-jako-rekord]]).
- **AC-2 — powtórne małżeństwo.** *Given* osoba jest już partnerem w jednej rodzinie *When* dodaję drugą
  rodzinę z tą samą osobą *Then* obie rodziny istnieją, a dzieci należą do właściwej pary.
- **AC-3 — małżeństwo z datą z dopiskiem.** *When* wpisuję datę małżeństwa albo końca rodziny *Then* mogę
  użyć kwalifikatora ([[FR-004-data-z-dopiskiem]]).
- **AC-4 — źródło przy relacjach.** *When* zapisuję rodzinę *Then* przynależność partnerów i dzieci ma
  źródło (domyślnie „notatki") i status ([[FR-001-provenance]]).
- **AC-5 — osoba z grobu w rodzinie.** *Given* osoba wpisana przy grobie ([[US-002-przepisanie-grobu]])
  *When* tworzę rodzinę *Then* mogę wskazać tę osobę zamiast tworzyć ją drugi raz.

## Out of scope
- Widok drzewa i ścieżka pokrewieństwa → [[EPIC-003-zrozumienie]] (kształt po [[SPIKE-002-tree-on-a-phone]]).
- Wskazanie „ja" → widok osoby, [[EPIC-002-wizyta]] (M5).
- Sprzeczne twierdzenia o relacji → [[US-004-fakt-od-babci]].

## Notes
- Szybkość wprowadzania (G6) brief zostawił projektowi wprowadzania. Formularz projektuje agent `ui` w
  łańcuchu przed `planning` ([[ISSUE-013-setup-ui-agent]]), na wytycznych `05_DESIGN/brand/style-b.md`.
  Punkt wyjścia to formularz osoby z [[ISSUE-012-transcribe-grave-screen]] (`05_DESIGN/wpis-osoby.md`,
  tempo liczone w akcjach na rekord).
- **Uwaga autora (2026-10-06):** w formularzu osoby brakuje mu informacji, *„z kim osoba jest związana
  (pokrewieństwo, powinowactwo)”*. Kolejność: ta US zaraz po [[US-005-zdjecia]], przed przepisywaniem
  notatek (ISSUE-012 → *Input from the author*). Czy relacje wpisuje się z formularza osoby, czy
  formularzem rodziny (AC-1), czy obiema drogami, rozstrzyga `ui` z autorem przed planem.
- **Zamknięcie (2026-10-08, [[ISSUE-019-family-relations]]):**
  - **droga wejścia** (decyzja autora na stopie #1): relacje wpisuje się **arkuszem rodziny** ([[rodzina]]), a widać je w
    formularzu osoby jako chipy ([[wpis-osoby]] 9a);
  - **„związek”, nie tylko „małżeństwo”** — uwaga autora o rozstaniach, owdowieniach i nowych związkach. AC-2 i AC-3 mówią
    „małżeństwo”, a w aplikacji to „Związek” z datą „Ślub” i „Koniec związku”. Brzmienie AC zostaje jako zapis z kick-offu;
  - **AC-4 „przynależność partnerów”** spełnia twierdzenie przy rodzinie (para to jeden fakt), a przynależność dziecka —
    twierdzenie przy jego łączu ([[ADR-011-relation-claims-family-and-child-link]]). Zmiana partnera w poprawie zostawia
    rodzinie stare twierdzenie o parze — bez skutków, dopóki źródło jest zawsze „notatki”; wraca przy [[US-004-fakt-od-babci]];
  - **bez płci i bez rodzeństwa** przy osobie (decyzje autora); nazwy relacji neutralne;
  - **kandydaci na później:** data początku związku bez ślubu (uwaga autora: „był z kimś w danym okresie”) i kontrola
    cykli w rodzinie (`CURRENT_STATE.md`).

## Verification (US)
> `qa`, 2026-10-08. Werdykt na poziomie US wystawił **niezależny przegląd**: subagent bez udziału w budowie, tylko odczyt
> plików i przebieg testów rodzin (**20/20**). Po przeglądzie `qa` dopisał test z uwagi 1 (dopiski w arkuszu): pełny
> przebieg **458/458**. DoD US: każde AC z testem happy-path · pokazane w aplikacji na emulatorze · werdykt zapisany ·
> wiersz w `TRACEABILITY.md`.

| AC | Test happy-path | Pokazane człowiekowi (emulator) |
|---|---|---|
| AC-1 rodzina jednym formularzem | `families_test.dart` „AC-1, AC-4, AC-5 — one sheet…” · `family_screens_test.dart` „AC-1, AC-5 — "Dodaj związek" from the form…” | **Autor** (stop #2): związek z nowym dzieckiem u Ewy; stan urządzenia sprawdzony przez agenta. **Agent:** para z grobu i nowe dziecko „Stefan” |
| AC-2 powtórne małżeństwo | `families_test.dart` „AC-2 — a person in two unions…” · `family_screens_test.dart` „AC-2, AC-3, D4…” · F1 (`migration_test.dart`), F3 (`restore_service_test.dart`) | **Autor:** Jan w dwóch związkach (z Anną i z Ewą) w danych ze stopu #2 |
| AC-3 data z dopiskiem | `families_test.dart` „AC-3 — the dates are corrected in place…” · `family_screens_test.dart` „AC-3 on the sheet…” (**dopisany po przeglądzie**) | **Autor:** „ślub ok. 1993 · koniec 1995” |
| AC-4 źródło przy relacjach | `families_test.dart` (twierdzenia rodziny i łączy; usunięte dziecko zabiera twierdzenia; rodzina sprzed v6 dostaje je przy zapisie; `CHECK`) · `family_screens_test.dart` AC-1 (2 twierdzenia) · `data_state_test.dart` (twierdzenie w odcisku) | — (statusu nie pokazuje ekran — decyzja kosztowa FR-001) |
| AC-5 osoba z grobu w rodzinie | `families_test.dart` AC-1/4/5 · `family_screens_test.dart` AC-1/AC-5 (w bazie 3 osoby) | **Autor i agent:** wybór z „W tym grobie” |

**Werdykt: APPROVED** z uwagami: AC-1…AC-5 mają testy happy-path, które przechodzą, a autor widział AC-1, AC-2, AC-3 i
AC-5 na emulatorze. Uwagi: brzmienie „małżeństwo” w AC (wyżej, *Notes*), twierdzenie o parze przy rodzinie (ADR-011),
data początku związku bez ślubu i kontrola cykli — kandydaci.

**Czego szukano i nie znaleziono:** AC bez testu; testów czerwonych albo pominiętych; naruszenia *Out of scope* (drzewa,
ścieżki, „ja”, sprzecznych twierdzeń); decyzji autora sprzecznej z AC (płeć ani rodzeństwo nie są w AC).
