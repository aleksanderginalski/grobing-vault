---
title: "ISSUE-050 — „Next” beside ▶ on the tree and the migration map: the year and what happened in it"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "`/pm` 2026-10-18 — autor przeszedł cały przepływ na emulatorze (dane demo), punkt 7 z 7, z doprecyzowaniem w tej samej sesji; część c) z [[2026-10-14-opowiesc-rodziny-i-wieniec]] (INBOX) przeniesiona przed instalację"
created: 2026-10-18
updated: 2026-10-18
---

# ISSUE-050 — „Następne”: rok i co się w nim stało

> Autor: *„opcja przechodzenia do next event (obok przycisku play), aby pokazać, co się działo, i aby dawało krótki komentarz: a) w drzewie — ktoś się
> urodził, ktoś się ożenił, ktoś zmarł; b) na mapie — zmiana miejsca zamieszkania”*. Doprecyzowanie: *„zróbmy tylko „następne” — tak chciałbym, aby
> było na ekranie: data i co się w tym roku stało”*.
>
> 2026-10-14 autor odłożył opowieść rodziny (INBOX c) po instalację; 2026-10-18 „następne zdarzenie” przechodzi przed instalację. Animacje połączeń i
> zbliżenia zostają w INBOX, po instalacji.

## What to build
- **Przycisk „Następne” obok ▶** w listwie czasu — drzewo ([[drzewo]] el. 6 i 11) i mapa migracji ([[mapa-migracji]]): suwak przeskakuje do
  najbliższego późniejszego roku, w którym coś się stało.
- **Na ekranie rok i co się w nim stało:**
  - drzewo — urodziny, śluby (i „razem od”?), zgony;
  - mapa — przeprowadzki.
- **Tylko „następne”**, bez „poprzedniego” (autor).
- Także w trybie prezentacji — podpis czytany z kanapy ([[drzewo]] D38: minimum 16′ — dziś imię 13 sp go nie spełnia, INBOX c pytanie 6).
- Projekt: `ui` przed `planning` — zmiana [[drzewo]] i [[mapa-migracji]].

## Acceptance Criteria
- **AC-1** *Given* drzewo z suwakiem na 1940 *When* dotykam „Następne” *Then* suwak staje na najbliższym późniejszym roku ze zdarzeniem, np. 1952, a na
  ekranie jest „1952” i lista: „urodził się Jan Wymyślony”, „ślub: Maria Zmyślona i Piotr Wymyślony”.
- **AC-2** *Given* mapa migracji *When* „Następne” *Then* najbliższy rok z przeprowadzką i podpis, kto się przeprowadził.
- **AC-3** *Given* tryb prezentacji *When* „Następne” *Then* to samo na telewizorze, czytelne z kanapy.
- **AC-4** *Given* ostatnie zdarzenie za nami *When* „Następne” *Then* widać, że dalej nic nie ma (np. „dziś”), bez błędu.

## Notes
- **Przy starcie pozycji `pm` zada jedno pytanie o cel** (retro 4, R1) — zmienia decyzję z 2026-10-14.
- `⚠️ OPEN` (na makietę, stop #1):
  1. **czyje zdarzenia** — domyślnie osób widocznych na ekranie, na bieżącym poziomie ([[ISSUE-049-tree-levels-and-zoom]]);
  2. **daty niepewne** (ok., między, przed, po — [[drzewo]] D32): w którym roku i jak podpisane;
  3. **forma podpisu** — „urodził się” / „urodziła się” z płci; osoba bez płci; śluby bez daty (są w danych testowych);
  4. **mapa: nazwa miejsca w podpisie** — [[mapa-migracji]] D18 zdecydowało „bez nazw krajów i miejsc” na mapie; podpis to co innego, do decyzji;
  5. **zachowanie ▶ po „Następne”** — stoi czy jedzie dalej; ograniczenie animacji (SC 2.3.3).
- Zależy od [[ISSUE-049-tree-levels-and-zoom]] (poziomy). Bez zmiany bazy (zdarzenia z dat osób, związków i zamieszkań).
- [[EPIC-003-zrozumienie]] ([[US-010-czas-na-drzewie]]). Z tego samego przeglądu autora: [[ISSUE-047-grave-first-then-people]] ·
  [[ISSUE-048-portrait-photos]].
