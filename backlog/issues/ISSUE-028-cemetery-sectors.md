---
title: "ISSUE-028 — The author's sectors (kwatery): mark a named zone on the plan or the photo from above, shown as a dashed line with its name"
type: issue
status: ready
delivery-style: task-level
priority: MUST
epic: "[[EPIC-002-wizyta]]"
user-story: "[[US-007-mapa-cmentarza]]"
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "rozpisanie US-007 (`docs` w auto-flow po `pm`, autor: „tak”, 2026-10-12) · US-007 AC-4 i *Notes* („do zaprojektowania przed planem”) · [[ADR-003-map-source-offline]] pkt 3 · [[cmentarz]] element 4, D13 · [[EPIC-002-wizyta]] → *Open questions* (kierunek autora 2026-10-08)"
created: 2026-10-12
updated: 2026-10-12
---

# ISSUE-028 — Kwatery autora

> Z rozpisania [[US-007-mapa-cmentarza]] (`docs` w auto-flow, 2026-10-12, po `pm`). Druga z dwóch pozycji, po
> [[ISSUE-027-cemetery-map-plan-photo-states]], bo kwatery rysuje się na planie. Podział zaproponował łańcuch, nie
> autor.

## What to build
1. **Zaznaczenie kwatery** na planie albo na zdjęciu z góry: nazwa i strefa. Autor robi to w domu, według planu
   zarządcy, i zaznacza tylko kwatery, w których leży rodzina ([[ADR-003-map-source-offline]] pkt 3; kierunek autora:
   [[EPIC-002-wizyta]] → *Open questions*). **Jak to wygląda, SPIKE-004 nie pokazał.** Projektuje to `ui` przed
   planem: specyfikacja i makieta, a na stopie #1 kandydaci, gdzie się dotyka (retro 2, R6).
2. **Kwatera na planie** ([[cmentarz]] element 4, D13): przerywana linia, nazwa w dolnym lewym rogu strefy. Kwatera
   bez strefy jest tylko w adresach grobów.
3. **Poprawa i usunięcie kwatery**, bo autor może się pomylić.
4. **Kwatery w kopii i po odtworzeniu**, bo to dane autora, a nie dane z zewnątrz.

## Acceptance Criteria
- [ ] **US-007 AC-4 — kwatery autora.** *Given* kwatera zaznaczona przez autora *Then* plan pokazuje ją przerywaną
      linią z nazwą; kwatera bez strefy jest tylko w adresach.
- [ ] Kwatera wraca po odtworzeniu z kopii (odcisk danych zgodny — [[NFR-002-odtworzenie-na-nowym-telefonie]]).

## Out of scope
- Plan, zdjęcie z góry, stany ekranu → [[ISSUE-027-cemetery-map-plan-photo-states]].
- Pinezki grobów → [[US-008-pinezka-na-miejscu]].

## Notes
- **Zmiana schematu:** strefa kwatery to nowe dane (nazwa, obrys, cmentarz), z migracją, testem migracji i próbnym
  odtworzeniem. Model jest w ADR-003 → *Follow-ups* („model kwatery: nazwa + strefa”). To kandydat na ADR.
- **Kwatera w adresie grobu to dziś wolny tekst** (`graves.sector`). Do ustalenia: czy strefa łączy się z grobami po
  nazwie, czy przez odnośnik. Od tego zależy, czy zmiana nazwy strefy zmienia adresy.
- OSM ma kwatery tylko na 1 z 8 obszarów autora (SPIKE-001 M10), więc ich źródłem jest autor.
