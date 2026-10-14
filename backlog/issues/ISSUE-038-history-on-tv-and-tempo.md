---
title: "ISSUE-038 — History on the TV and its tempo: ▶ in presentation mode with the year large enough for the room, and a choice of the slider's speed"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-010-czas-na-drzewie]]"
depends-on: "[[ISSUE-037-time-on-the-tree]]"
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "prośba autora na stopie #2 [[ISSUE-037-time-on-the-tree]] (2026-10-14: *„Czy play również zadziała podczas prezentowania?”*, potem *„a) Można było tą historie odtwarzać na telewizorze, b) dostosowanie prędkości tych lat”*) · [[drzewo]] v1.13 (element 6, element 11, D37)"
created: 2026-10-14
updated: 2026-10-14
---

# ISSUE-038 — Historia na telewizorze i tempo lat

> Z prośby autora na stopie #2 [[ISSUE-037-time-on-the-tree]] (`docs`, 2026-10-14). Dziś tryb prezentacji nie ma suwaka ani roku i zawsze pokazuje „dziś”
> ([[drzewo]] D37), a ▶ biegnie stałym tempem ok. 21 lat na sekundę (D34). Punkty c) i d) z tej samej prośby — animacje połączeń i zbliżenia na zdarzenia, wieniec
> przy portrecie według nazwiska — są w [[2026-10-14-opowiesc-rodziny-i-wieniec]] (INBOX): mają za dużo niewiadomych na pozycję. **Pozycja zmienia ekran → `ui`
> przed `planning`.**

## What to build
1. **▶ w trybie prezentacji** (element 11): historia rodziny odtwarzana na telewizorze — drzewo w roku, osoby pojawiają się i łączą jak w elemencie 6.
2. **Rok widoczny na telewizorze** — czytelny z odległości pokoju (karty w prezentacji nie ma).
3. **Sterowanie na telefonie w prezentacji** — gdzie dotknąć ▶ / ❚❚ i suwak (dziś pusty dotyk pokazuje na 3 s tylko „Zakończ prezentację”, D25).
4. **Tempo lat** — wybór prędkości odtwarzania (np. wolniej / jak dziś / szybciej) w karcie i w prezentacji.

## Acceptance Criteria (szkic — dopisze `ui` i `planning`)
- [ ] W trybie prezentacji ▶ odtwarza historię od początku suwaka do „dziś”, ❚❚ zatrzymuje; rok widać na telewizorze.
- [ ] Wybrane tempo zmienia czas odtwarzania (np. 1880 → dziś w ok. 14 s / 7 s / 4 s) w karcie i w prezentacji.
- [ ] Przy ograniczeniu animacji w systemie zostaje R2 (dekada co ok. 1 s) — tempo zmienia tylko odstęp skoków.

## Open for `ui` (kandydaci na makiecie — retro 2, R6)
1. Wielkość i miejsce roku na telewizorze (prior art: napisy i liczniki w telewizji — pomiar przy odległości z kanapy).
2. Sterowanie w prezentacji: obok „Zakończ prezentację”, osobna listwa, czy gest.
3. Tempo: ile prędkości, jak je nazwać, gdzie stoi przełącznik (karta jest ciasna przy tekście 200%).
4. Czy prezentacja otwarta z roku Y zaczyna od Y (dziś D37: zawsze „dziś”) — zmiana D37 do decyzji autora.

## Out of scope
- Animacje związków, zbliżenia na zdarzenia, wieniec przy portrecie → [[2026-10-14-opowiesc-rodziny-i-wieniec]].
- Google Cast i odbiornik na telewizorze — obraz dalej przesyła system ([[drzewo]] D11, D29).

## Notes
- **Autor na stopie #2 ISSUE-037:** *„dla mnie za szybko”* — obecne ok. 20 lat/s (1880 → dziś w ok. 7 s) to dla niego za szybko; tempo domyślne do przemyślenia razem
  z wyborem tempa (np. wolniejsze domyślne).
- Logika czasu jest gotowa (`lib/app/tree/tree_time.dart`, ISSUE-037): ta pozycja to widok i zegar ▶ (`_nextLater` w `tree_screen.dart`).
- Płynność ▶ zmierzona na emulatorze: 7–9% wolnych klatek przy tempie ok. 20 lat/s (ISSUE-037 → *Dev report*). Szybsze tempo = częstsze zmiany roku — pomiar przy
  najszybszym wariancie.
