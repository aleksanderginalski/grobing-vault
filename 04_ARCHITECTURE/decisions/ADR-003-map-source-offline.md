---
title: "ADR-003 — Map and satellite source with offline use for 10 cemetery-sized areas"
type: adr
status: proposed
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[SPIKE-001-map-source-offline]]"
source: "PROJECT_BRIEF §Architecture → Stack (S-MAP) · §6 N5 · §3b H3, H9, H10 · MoSCoW W3"
created: 2026-10-05
updated: 2026-10-05
---

# ADR-003 — Źródło map offline

> Architecture Decision Record. `proposed` — **zamyka go [[SPIKE-001-map-source-offline]]** (warunek
> wyjścia spike'a: wybrane źródło z uzasadnieniem i kosztem → ten ADR `accepted`).

## Status
proposed — 2026-10-05.

## Context
- Widoki 1-2 (mapa Polski, mapa cmentarza) i krok 6 ścieżki (pinezka tam, gdzie stoję) stoją na mapie.
- Mapa musi działać **bez zasięgu** ([[NFR-001-offline]], M7).
- **Ograniczeniem są warunki dostawców, nie framework:** [polityka kafelków OSM Foundation](https://operations.osmfoundation.org/policies/tiles/)
  zabrania użycia offline na `tile.openstreetmap.org` (zweryfikowane 2026-10-05, brief §6 N5); inni
  dostawcy pobierają opłaty ponad darmowe progi (H10).
- Groby: Grobonet ma mapy grobów tylko dla cmentarzy, których zarządcy używają jego systemu, bez
  publicznego API → **link do strony grobu, nigdy kopia danych** (W3, [[NT-004-grobonet-link-terms]]).

## Decision
**Do podjęcia po SPIKE-001.** Kierunek ustalony w kick-offie: źródło map + zdjęć satelitarnych, którego
warunki **pozwalają** jednej osobie trzymać offline ok. 10 małych obszarów; koszt zapisany w
`06_NON_TECH/external-costs.md` (folder na sygnał); Grobonet — wyłącznie link.

## Options considered

| Option | Pros | Cons | Why (not) chosen |
|---|---|---|---|
| `flutter_map` + cache kafelków od dostawcy, który pozwala na offline | natywne dla Fluttera | popularna wtyczka bulk-download jest **GPL**; [warunki dostawców ograniczają masowe pobieranie](https://docs.fleaflet.dev/v7/tile-servers/offline-mapping) | do sprawdzenia w SPIKE-001 |
| Wtyczka MapLibre dla Fluttera z [regionami offline](https://maplibre.org/flutter-maplibre-gl/advanced/offline-regions/) | regiony offline wbudowane | warunki dostawcy kafelków nadal obowiązują | do sprawdzenia w SPIKE-001 |
| Własne kafelki (self-hosted) | brak warunków dostawcy co do offline (brief §6 N5) | hosting i utrzymanie; źródło zdjęć satelitarnych nadal potrzebne | do sprawdzenia w SPIKE-001 |
| Mapy tylko online (status quo) | zero pracy | łamie M7 / [[NFR-001-offline]] — ścieżka zawodzi tam, gdzie jest używana | rejected |

## Consequences
- **Positive:** po decyzji widoki 1-2 mogą ruszyć (spike'i przed widokami, których dotyczą — A5).
- **Negative / trade-offs:** możliwy koszt zewnętrzny; ewentualna licencja wtyczki (GPL) do oceny.
- **Follow-ups:** ⚠️ **OPEN — mapa Polski (krok 1) offline czy nie** — pytanie spike'a obejmuje tylko
  obszary cmentarzy; [[NFR-001-offline]] → *Notes*. · [[SPIKE-001-map-source-offline]] krok 4 (pinezki ze zdjęcia satelitarnego) jest podważony
  korektą autora — notatki nie mają adresów kwater; do przeformułowania przy planowaniu spike'a.
