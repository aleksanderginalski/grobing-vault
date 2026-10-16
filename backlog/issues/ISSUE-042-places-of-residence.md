---
title: "ISSUE-042 — Places of residence: where and when a person lived, from a country down to an address"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "`/pm` 2026-10-16 — pomysł autora (miejsca zamieszkania i mapa migracji) i doprecyzowanie „od ogółu do szczegółu”; przed instalacją decyzją autora · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-16
---

# ISSUE-042 — Gdzie kto mieszkał i kiedy

> Autor w `/pm`: *„gdzie dana osoba mieszkała w którym momencie swojego życia, aby zrobić taką mapę, jak kto się przemieszczał po mapie
> świata”*, a o dokładności: **od ogółu do szczegółu** — kraj (punkt w środku kraju) → miasto (środek miasta) → adres; *„w ramach
> lokalizacji powinno to wystarczyć (…), ale można dodać miasto (centrum miasta) albo wręcz dokładną ulicę”*. Ta pozycja to **dane i
> formularz**; widok mapy to [[ISSUE-045-migration-map]]. **Przed instalacją**, bo zmienia bazę ([[2026-10-16-retro-04]] → zasady terminu).

## Prior art
- Kanon genealogii ma na to gotowy fakt: **zamieszkanie z datą i miejscem** — [GEDCOM 7 `INDI-RESI`](https://gedcom.io/terms/v7/INDI-RESI)
  (miejsce w `PLAC` i/lub `ADDR`, data w `DATE`); Gramps traktuje zamieszkanie jako zdarzenie
  ([dyskusja](https://gramps.discourse.group/t/residence-as-an-event/7277)).
- **Miejsce jako lista jednostek od najmniejszej do największej** (ulica, miasto, kraj) — konwencja `PLAC`
  ([Ancestris — Places](https://docs.ancestris.org/books/user-guide/page/places)); współrzędne dopisuje się z najdokładniejszej znanej
  jednostki (np. [GeoFinder](https://pypi.org/project/geofinder/0.2.4/) — gazeter geonames.org).
- U nas: `events` ma już daty z dopiskiem, także „między” (lata od–do, [[FR-004-data-z-dopiskiem]]), i miejsce — **tylko jako tekst**
  ([[data-model]]). Nowa wartość `EventType` na końcu nie wymaga migracji (`database.dart`), ale **miejsce ze współrzędnymi i poziomem
  dokładności** to nowa tabela — zmiana schematu, która tylko dokłada.

## What to build
- W widoku osoby sekcja „Gdzie mieszkał(a)”: lista zamieszkań w kolejności lat; dodanie, poprawa, usunięcie (z potwierdzeniem).
- Zamieszkanie: **lata** (od–do z dopiskiem: około, przed, po, między; może być bez daty) i **miejsce** na jednym z poziomów: **kraj · miasto ·
  adres** — punkt z poziomu (środek kraju, środek miasta, punkt adresu) i nazwa.
- Projekt: `ui` — specyfikacja i makieta przed planem (nowy ekran wyboru miejsca). **Kandydaci na makiecie, przed rekomendacją** (retro 2, R6):
  - **skąd współrzędne bez sieci:** lista krajów i miast w aplikacji (otwarte dane, np. Natural Earth — już w [[ADR-007-poland-map-bundled-data]] —
    i GeoNames) · dotknięcie mapy · wyszukiwarka online (wtedy nazwa miejscowości wychodzi z telefonu — [[NFR-005-dane-nie-opuszczaja-telefonu]]);
  - **granice się zmieniały:** nazwa z czasu zamieszkania, dzisiejsza czy obie — w polskiej rodzinie to reguła, nie wyjątek;
  - czy miejsce urodzenia i zgonu (dziś tekst) dostają ten sam wybór miejsca — `⚠️ OPEN`, decyzja autora na stopie #1.

## Acceptance Criteria
- **AC-1** *Given* osoba *When* dodaję zamieszkanie z samym krajem i latami „ok. 1930 – ok. 1945” *Then* zapis ma poziom „kraj”, punkt w środku
  kraju i te lata.
- **AC-2** *Given* to zamieszkanie *When* doprecyzowuję miasto, a potem adres *Then* poziom i punkt się zmieniają, a zamieszkanie zostaje jedno.
- **AC-3** *Given* brak sieci *When* wybieram kraj albo miasto *Then* wybór działa.
- **AC-4** *Given* kopia z wersji sprzed tej pozycji *When* odtwarzam ją w nowej *Then* dane są kompletne (test migracji z poprzedniej wersji,
  próbne odtworzenie — DoD), a kopia z nowej wersji niesie zamieszkania i miejsca.

## Notes
- Przykłady w specyfikacji, makiecie i testach tylko z rdzeni wymyślonych (`family-data.md`, retro 3 R7) — także nazwy miejscowości.
- Zależna: [[ISSUE-045-migration-map]] (widok na tych danych).
