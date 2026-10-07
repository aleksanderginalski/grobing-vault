---
title: "SPIKE-001 — Map source: offline satellite for 10 cemetery-sized areas, cost, Grobonet coverage"
type: spike
status: ready
priority: MUST
time-box: "1 day of work + the on-site check on the next cemetery visit"
hypotheses: [H3]
covers-non-tech: [N5]
created: 2026-10-05
updated: 2026-10-07
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
   > ⚠️ **Pytanie poszerzone przez pomysł autora (2026-10-05), do decyzji przy planowaniu:** przy okazji
   > policz też, ile z 10 cmentarzy ma **plan z kwaterami** (Grobonet, strona zarządcy, tablica przy
   > bramie). Taki plan to kandydat na trzecie źródło położenia obok satelity i GPS →
   > `01_INBOX/2026-10-05-plany-cmentarzy.md`.
   > **Nazwy cmentarzy autora w vaulcie — rozstrzygnięte 2026-10-07:** autor wybrał w
   > [[NT-008-publication-review]] publiczny vault, więc nazwa cmentarza autora mówiłaby publicznie, gdzie
   > leży jego rodzina. W vaulcie **tylko liczba** (tak jak falsyfikator w [[ISSUE-015-add-cemetery-from-database]]).
   > Nazwy zostają w odpowiedzi agenta i w aplikacji.
2. 2-3 kandydatów na źródło satelitarne z prawem offline: warunki, limity, koszt dla 1 użytkownika i
   10 małych obszarów; zgodność licencji z Flutterem (uwaga: popularna wtyczka bulk-download do
   `flutter_map` jest GPL).
   > **Z briefu (§Security), dopisane przy przeglądzie `kickoff/` (retro 1, R4, 2026-10-06):**
   > - **klucz API dostawcy**, jeśli jest potrzebny: poza repo (lokalna, gitignorowana konfiguracja),
   >   ograniczony do pakietu `com.grobing.app` i certyfikatu podpisu (*Hard floors* → *No secrets in
   >   the repo*);
   > - **sieć:** pobranie regionu offline wymaga sieci, a APK release **nie ma dziś uprawnienia
   >   `INTERNET`** ([[NFR-005-dane-nie-opuszczaja-telefonu]], [[ISSUE-008-backup-write]]). Dodanie go
   >   wchodzi do ADR-003 razem z tym, co aplikacja wysyła i dokąd (tylko HTTPS — *Hard floors*).
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
