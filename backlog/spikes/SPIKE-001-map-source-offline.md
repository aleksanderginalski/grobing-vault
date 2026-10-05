---
title: "SPIKE-001 — Map source: offline satellite for 10 cemetery-sized areas, cost, Grobonet coverage"
type: spike
status: ready
priority: MUST
time-box: "1 day of work + the on-site check on the next cemetery visit"
hypotheses: [H3]
covers-non-tech: [N5]
created: 2026-10-05
updated: 2026-10-05
---

# SPIKE-001 — Map source + offline (S-MAP)

## The question
**Które źródło map + zdjęć satelitarnych pozwala jednej osobie trzymać offline 10 obszarów wielkości
cmentarza — na jakich warunkach i za ile — i ile z 10 cmentarzy autora pokrywa Grobonet?**

## Why it matters
Widoki 1-2 i krok 6 ścieżki stoją na tej odpowiedzi (H3). Framework nie jest ograniczeniem — oba
stosy umieją regiony offline; ograniczeniem są **warunki dostawców**: np. publiczne serwery
OpenStreetMap wprost zabraniają użycia offline (§6 N5).

## Steps
1. Grobonet: wyszukaj 10 cmentarzy autora — które mają mapę grobów (tylko liczba i nazwy cmentarzy w
   notatce; **żadnych nazwisk**). Dla pokrytych: czy da się linkować do strony grobu (→ NT-004).
2. 2-3 kandydatów na źródło satelitarne z prawem offline: warunki, limity, koszt dla 1 użytkownika i
   10 małych obszarów; zgodność licencji z Flutterem (uwaga: popularna wtyczka bulk-download do
   `flutter_map` jest GPL).
3. Prototyp jednorazowy: jeden cmentarz offline w trybie samolotowym.
4. **Na miejscu (zaparkowane do najbliższej wizyty, np. 1 listopada):** 3 pinezki postawione wcześniej
   ze zdjęcia satelitarnego — czy prowadzą do właściwego grobu?
   > ⚠️ **Założenie podważone (autor, 2026-10-05):** notatki **nie zawierają adresów kwater** — bez
   > wiedzy, gdzie grób leży, pinezki ze zdjęcia satelitarnego postawić się nie da. Pierwsze położenie
   > powstaje na miejscu (GPS). Krok 4 do przeformułowania przy planowaniu tego spike'a — decyzja
   > autora, nie poprawka po cichu.

## Exit criterion
Wybrane źródło z uzasadnieniem i kosztem → **ADR-003** `accepted`; koszt → `06_NON_TECH/external-costs.md`
(folder na sygnał). Albo: „żadne źródło nie spełnia" → decyzja autora o kompromisie.

## Definition of Done
- [ ] Odpowiedź zapisana (ADR-003) · kod prototypu usunięty · status H3 zaktualizowany w notatce spike'a.
