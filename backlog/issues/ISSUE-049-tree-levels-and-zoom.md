---
title: "ISSUE-049 — Tree: kinship levels (blood, then each marriage) independent of zooming, zoom also on the TV"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "`/pm` 2026-10-18 — autor przeszedł cały przepływ na emulatorze (dane demo), punkty 5–6 z 7, z doprecyzowaniem w tej samej sesji; podział — `pm`"
created: 2026-10-18
updated: 2026-10-18
---

# ISSUE-049 — Poziomy pokrewieństwa niezależne od przybliżania

> Autor: *„dlaczego zoom-in/out nie działa w wersji drzewa genealogicznego, gdy jest na telewizorze”* · *„chciałbym, aby poziomy rodziny nie
> zmieniały się, gdy robię zoom-in zoom-out (chciałbym widzieć „big picture” i przybliżać sobie szczegóły bez znikania członków mojej rodziny)”*.
> Doprecyzowanie: *„chciałbym, aby to były niezależne względem siebie funkcjonalności: a) poziomy do pokazywania linii pokrewieństwa /
> powinowactwa (np. poziom pierwszy to tylko „nasza linia krwi”, a w kolejnych poziomach dodawana jest np. rodzina żony brata itd., na jeszcze
> kolejnym rodzina męża siostry żony brata itd.); b) zoom-in zoom-out do poruszania się po widoku naszego drzewa”*.

## What to build
- **a) Nowa reguła poziomów** — zastępuje [[drzewo]] D2 (reguła autora ze SPIKE-002: poziom 1 — rodzice, partnerzy, dzieci; kolejne dokładają rodzinę
  każdej osoby). Reguła zrozumiana przez `pm` (autor nie zaprzeczył): **poziom = 1 + liczba małżeństw na drodze od osoby w środku**:
  - poziom 1 — sama krew: przodkowie, potomkowie, rodzeństwo, kuzyni;
  - poziom 2 — przez jedno małżeństwo: np. rodzina żony, rodzina żony brata;
  - poziom 3 — przez kolejne: np. rodzina męża siostry żony brata.
  Rama: to nadal DOI z [[drzewo]] D8 (TimeNets), z innymi wagami — krok po krwi nic nie kosztuje, krok przez małżeństwo kosztuje poziom.
- **Osobny przełącznik poziomu** — poziom nie zmienia się gestem. Stary „− Poziom 2 +” autor nazwał nieestetycznym ([[drzewo]] D25, S1) → nowy
  kształt na makiecie.
- **b) Przybliżanie i oddalanie to sam widok** — dwa palce, + / −, podwójne dotknięcie; skład osób się nie zmienia. Zastępuje [[drzewo]] el. 3 / S2
  (oddalanie dokłada poziom, przybliżanie zabiera).
- **Tryb prezentacji** ([[drzewo]] el. 11, D16 „poziom 2 stały”, „bez szczypania”) — przybliżanie i oddalanie także na telewizorze; *Obali* D16
  („autor chce oddalać na telewizorze”) — trafione.
- Dotyka: ścieżka „Połącz dwie osoby” ([[drzewo]] el. 8 — „najniższy poziom, na którym widać całą ścieżkę”), ślad dalszej rodziny (D9), imiona przy
  oddalaniu (I2, D27), „Pokaż w drzewie” (D15 — poziom 2), stany i czytnik.
- Projekt: `ui` przed `planning`; **kandydaci na emulatorze albo makiecie przed rekomendacją** (retro 2, R6 — pozycja wybiera to, co widać).

## Acceptance Criteria
- **AC-1** *Given* drzewo na dowolnym poziomie *When* przybliżam i oddalam (dwa palce, + / −, podwójne dotknięcie) *Then* na drzewie są te same
  osoby — zmienia się tylko widok.
- **AC-2** *Given* „Ja” w środku, brat Piotr Wymyślony z żoną Ewą z d. Zmyśloną *When* poziom 1 *Then* widać krewnych z krwi (rodziców, dziadków,
  Piotra i jego dzieci), a rodziców Ewy nie; *When* poziom 2 *Then* widać też rodziców Ewy.
- **AC-3** *Given* poziom 2 *When* poziom 3 *Then* dochodzi rodzina, do której prowadzi kolejne małżeństwo (np. mąż siostry Ewy i jego rodzice).
- **AC-4** *Given* tryb prezentacji na telewizorze *When* szczypię na telefonie *Then* obraz przybliża się i oddala, a skład osób się nie zmienia.
- **AC-5** *Given* „Połącz dwie osoby” *Then* cała ścieżka jest dalej widoczna na drzewie (regresja [[US-011-polacz-dwie-osoby]]).

## Notes
- `⚠️ OPEN` (na makietę, stop #1):
  1. **małżonkowie krewnych na poziomie 1** — np. żona brata jako matka jego dzieci (dzieci są z krwi, ona nie): widać ją na poziomie 1 czy
     dopiero na 2?
  2. **przełącznik poziomu w trybie prezentacji** — jest, czy poziom zmienia się tylko przed wejściem w tryb?
  3. **skala po zmianie poziomu** — zostaje, czy drzewo dopasowuje się do ekranu?
  4. **nazwy poziomów** — słowa z pytania autora („linia krwi”, „pokrewieństwo / powinowactwo”) czy liczby.
- Bez zmiany bazy (poziom liczony z relacji przy otwarciu, jak dziś).
- Wejście dla [[ISSUE-050-next-event]] (zdarzenia osób na bieżącym poziomie).
- [[EPIC-003-zrozumienie]] ([[US-009-drzewo-od-osoby]], [[US-011-polacz-dwie-osoby]]). Z tego samego przeglądu autora:
  [[ISSUE-047-grave-first-then-people]] · [[ISSUE-048-portrait-photos]].
