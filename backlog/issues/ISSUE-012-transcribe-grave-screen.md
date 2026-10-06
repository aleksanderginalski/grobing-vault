---
title: "ISSUE-012 — Screen: transcribe a grave from the notes (cemetery → grave → persons)"
type: issue
status: ready
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-002-przepisanie-grobu]]"
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
created: 2026-10-06
updated: 2026-10-06
---

# ISSUE-012 — Ekran przepisania grobu

> Z rozpisania [[US-002-przepisanie-grobu]] (decyzja autora 2026-10-06, po `pm`): ekran po schemacie
> ([[ISSUE-011-schema-v2-assertions]]). To **pierwszy ekran do wpisywania danych**, czyli sygnał dla
> agenta `ui` (`CLAUDE.md` → *Na sygnał*) i warunek obudzenia [[NT-006-visual-guidelines]].

## What to build
1. **Cmentarz:** wybór i dodanie zrobiła [[ISSUE-014-home-map-of-poland]] (mapa, wyszukiwarka, dodanie
   ręczne), a dodanie z bazy robi [[ISSUE-015-add-cemetery-from-database]]. **Tu: „Otwórz cmentarz” w arkuszu
   mapy** ([[cmentarze]] element 7) prowadzi do ekranu cmentarza — przeniesione z ISSUE-014 decyzją autora
   (ISSUE-014 → *Decisions for stop #1* D5, 2026-10-06).
2. **Grób na cmentarzu**, zapisywany bez adresu kwatery, pinezki i zdjęcia. Brak adresu i pinezki widać
   przy grobie ([[US-002-przepisanie-grobu]] AC-5).
3. **Osoby w grobie, jedna po drugiej:** imiona, nazwisko, nazwisko rodowe, „kim była” z jedną linią
   źródła; daty urodzenia, zgonu i pochówku z dopiskiem (dokładnie / około / przed / po / między).
4. **Źródło przy datach i pochówku**, domyślnie „notatki”, status `CLAIMED`. Bez pytania o źródło przy
   każdym polu (decyzja kosztowa z [[FR-001-provenance]]).
5. **Widok grobu:** wszyscy pochowani z datami z dopiskiem.

## Acceptance Criteria
- [ ] US-002 AC-1: grób pokazuje wszystkie wpisane do niego osoby.
- [ ] US-002 AC-2: osoba ma imiona, nazwisko, osobno nazwisko rodowe i „kim była”.
- [ ] US-002 AC-3: data z każdym z pięciu dopisków zapisuje się i wyświetla z dopiskiem.
- [ ] US-002 AC-4: daty i pochówek zapisane z ekranu mają źródło (domyślnie „notatki”) i status
      `CLAIMED`; „kim była” ma jedną linię źródła.
- [ ] US-002 AC-5: grób z samym cmentarzem i osobami się zapisuje, a brak adresu i pinezki jest widoczny.
- [ ] Arkusz cmentarza na mapie ma „Otwórz cmentarz”, który otwiera ekran cmentarza (przeniesione z
      ISSUE-014 AC-4, D5).
- [ ] Ekran stosuje wytyczne stylu B z [[NT-006-visual-guidelines]].
- [ ] Zapis z ekranu zamawia kopię w tle tak samo jak każdy zapis danych ([[ISSUE-010-background-backup]]).

## Out of Scope
- Rodzice, małżeństwa, dzieci → [[US-003-przepisanie-rodziny]].
- Drugie, sprzeczne twierdzenie → [[US-004-fakt-od-babci]].
- Zdjęcia nagrobka i osoby → [[US-005-zdjecia]].
- Pinezka i jej poprawa na miejscu → [[EPIC-002-wizyta]] (M6).
- **Poprawianie i usuwanie wpisu:** US-002 ich nie wymienia. `planning` ustala, czy wchodzi minimum
  (poprawa literówki przy przepisywaniu), i mówi to na stopie #1. Bez tego zakres się nie poszerza.

## Input from the author (2026-10-06, po makiecie z [[ISSUE-013-setup-ui-agent]])
Autor ocenił pierwsze specyfikacje `ui` (`05_DESIGN/`) obok obrazów z kick-offu
(`05_DESIGN/brand/references.md`, R1–R4). Uwagi, blisko słów autora:
1. **Ekran główny = mapa Polski od startu**, także pusta, bez cmentarzy. Cmentarz dodaje się z pola
   **„Szukaj osoby lub cmentarza”**: gdy nic nie ma, można dodać nowy — *„lub znaleźć go w bazie cmentarzy,
   żeby potem zaimportować jego mapę?”* (pytanie autora, nowy pomysł). Każdy zapisany cmentarz jest na
   mapie Polski **zniczem**, jak w R1.
2. **Cmentarz jak R2:** po wejściu widać groby (kwatery) zaznaczone zniczami. Po wybraniu znicza arkusz
   pokazuje: miejsce na zdjęcie, lokalizację, ile osób tam leży i **nazwę grobowca**. Przycisk „Pokaż
   grób”.
3. **Grób jak R4:** zdjęcie grobu, nazwa, kto tam leży (zdjęcie, imię i nazwisko, daty urodzenia i
   śmierci), dodawanie zdjęć i nowych osób, wejście w szczegóły osoby.
4. **Formularz osoby** (ramki 5–6 makiety) może zostać jako dodawanie i poprawa osoby, ale brakuje mu:
   **zdjęcia, krótkiej biografii i informacji, z kim osoba jest związana (pokrewieństwo, powinowactwo).**

**Co to dotyka poza tą pozycją:**
- mapy → [[EPIC-002-wizyta]] (M2, M3) i [[SPIKE-001-map-source-offline]] / [[ADR-003-map-source-offline]];
- zdjęcia → [[US-005-zdjecia]];
- relacje → [[US-003-przepisanie-rodziny]];
- szczegóły osoby → M5;
- nazwa grobu → zmiana schematu (`05_DESIGN/grob.md` → *Open* 1);
- „baza cmentarzy z importem mapy” → pomysł spoza backlogu, obok `01_INBOX/2026-10-05-plany-cmentarzy.md`.

**Decyzja autora (2026-10-06, *„ok plan brzmi dobrze”*) — kolejność:**
1. [[ISSUE-014-home-map-of-poland]]: mapa Polski z wbudowanego konturu, znicze cmentarzy, dodanie
   cmentarza. **Przejmuje punkt 1 *What to build* tej pozycji;**
2. **ta pozycja:**
   - cmentarz jak R2, ale bez zdjęcia satelitarnego — arkusz z grobami, z pinezką i bez;
   - **grób jak R4 z nazwą grobu** (opcjonalne pole, czyli zmiana schematu: migracja v2→v3 z testem,
     NFR-003);
   - formularz osoby z biografią — dzisiejsze „kim była” z linią źródła;
3. [[US-005-zdjecia]] — zdjęcia grobu i osoby (formularz i R4);
4. [[US-003-przepisanie-rodziny]] — relacje w formularzu osoby;
5. [[SPIKE-001-map-source-offline]] — zdjęcie satelitarne cmentarza i znicze na grobach.

Groby z notatek nie mają położenia, więc znicze na mapie cmentarza pojawią się dopiero po postawieniu
pinezki. Specyfikacje w `05_DESIGN/` (`cmentarze.md`, `cmentarz.md`, `grob.md`) przebuduje `ui` przed
planem każdej z tych pozycji.

## Technical Notes
- **Tempo przepisywania** to miara ekranu: około 100 osób i 50 grobów całymi wpisami
  ([[NT-002-transcribe-the-notes]], G6). Każde dodatkowe pytanie na osobę mnoży się przez 100.
- **Czytelność w słońcu** ([[NT-006-visual-guidelines]]) do MVP sprawdza się na emulatorze. Słońce to
  wyjątek z `DEFINITION_OF_DONE.md`, sprawdzany na telefonie w buildzie release.
- Folder `05_DESIGN/` (oraz `05_DESIGN/brand/` dla stylu B) powstaje na ten sygnał według `doc-growth.md`,
  z wierszem w DOC_MAP. Zakłada go `docs`, kiedy praca nad ekranem albo NT-006 go potrzebuje.
- Sprawdzić, czy zamówienie kopii przy zapisie (ISSUE-010) obejmuje zapisy z nowego ekranu, a nie tylko
  drogi istniejące w chwili ISSUE-010.
- **Kopia zaraz po migracji v2→v3** (retro 1, R6): po udanej migracji schematu aplikacja zamawia kopię w
  tle od razu, a nie dopiero przy wyjściu albo następnym starcie ([[ISSUE-011-schema-v2-assertions]] →
  *Verification*, uwaga 2).
- Dane do pokazania i testów są wymyślone i istnieją tylko w buildzie debug ([[ISSUE-007-data-layer]]).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-011-schema-v2-assertions]] (twierdzenia w schemacie) | technical | `done` |
| [[NT-006-visual-guidelines]] (wytyczne stylu B) | design | `open` — ten ekran go budzi. Wytyczne v1 powstają w [[ISSUE-013-setup-ui-agent]] |
| agent `ui` w `grobing-agents` | process | [[ISSUE-013-setup-ui-agent]] (`done`). Pierwsze uruchomienie dało specyfikacje i uwagi autora (*Input from the author*) |
| [[ISSUE-014-home-map-of-poland]] (ekran główny, wybór i dodanie cmentarza) | product | `ready` — najpierw ona (decyzja autora 2026-10-06) |
| [[ISSUE-010-background-backup]] (kopia zamawiana przy zapisie) | technical | `done` |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC · ręczna weryfikacja na
emulatorze · fakt o rodzinie → źródło i status zapisane · dotyka warstwy danych → próbne odtworzenie z
kopii przechodzi (wpisy z ekranu wracają z odciskiem zgodnym) · zero danych rodziny w zmianach · INVEST
self-check. Po przyjęciu tego ISSUE US-002 idzie do werdyktu US.
