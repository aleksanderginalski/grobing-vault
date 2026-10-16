---
title: "ISSUE-045 — Migration map: where the family lived over the years, on the time slider and the TV"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "`/pm` 2026-10-16 — pomysł autora („mapa, jak kto się przemieszczał po mapie świata”) · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-16
---

# ISSUE-045 — Mapa migracji

> Widok na danych z [[ISSUE-042-places-of-residence]]: gdzie kto mieszkał w danym roku i jak się przemieszczał. **Bez zmiany bazy**, więc
> jeśli zabraknie czasu przed instalacją (2026-10-29), przychodzi później jako aktualizacja ze sklepu ([[2026-10-16-retro-04]] → zasady
> terminu).

## What to build
- Mapa świata (offline) z miejscami zamieszkania — **ten sam suwak lat, tempo i tryb prezentacji na telewizor**, które są w drzewie
  ([[US-010-czas-na-drzewie]], [[ISSUE-038-history-on-tv-and-tempo]], [[ISSUE-036-cast-from-the-app]]); nie nowa oś czasu.
- Punkty, które już są w danych: **cmentarz z pochówku** (ma współrzędne) i miejsca z [[ISSUE-042-places-of-residence]].
- Miejsce niepewne (poziom „kraj”) jako **obszar, nie pinezka** — jak koło dokładności GPS na mapie cmentarza (kandydat na makietę).
- Projekt: `ui` — specyfikacja i makieta (nowy ekran): skąd się wchodzi (zakładka, karta drzewa, widok osoby), droga jednej osoby vs cała
  rodzina w roku. Dane mapy świata: otwarte, wbudowane jak kontur Polski ([[ADR-007-poland-map-bundled-data]], Natural Earth).

## Acceptance Criteria
- **AC-1** *Given* osoby z zamieszkaniami *When* przesuwam suwak lat *Then* widzę, gdzie kto mieszkał w tym roku.
- **AC-2** *Given* osoba *When* ją wybieram *Then* widzę jej kolejne miejsca w kolejności lat.
- **AC-3** *Given* tryb prezentacji *When* przesyłam na telewizor *Then* mapa z rokiem i tempem jest czytelna jak historia na drzewie.
- **AC-4** *Given* brak sieci *Then* mapa i punkty działają.

## Notes
- Zależy od [[ISSUE-042-places-of-residence]]. Płynność: pomiar klatek naprzemiennie z buildem odniesienia (retro 4, R3).
- **Input from [[ISSUE-042-places-of-residence]]** (zamknięte 2026-10-16): dane w tabeli `residences` ([[ADR-020-residences-place-in-the-row]]) — punkt na
  każdym poziomie (kraj: punkt etykiety, miejscowość i adres: środek miejscowości), lata `od`/`do` z dopiskiem dokładnie/około. **Pusty koniec bierze się z
  następnego zamieszkania** — `impliedEnds` w `lib/data/residences.dart` ([[zamieszkanie]] D12, decyzja autora); mapa liczy ten sam koniec, nie własny.
  Bez lat — zamieszkanie bez miejsca na osi czasu (do decyzji przy projekcie mapy).
