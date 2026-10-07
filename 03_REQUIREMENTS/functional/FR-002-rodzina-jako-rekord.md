---
title: "FR-002 — Family as a record (couple + children), entered as a whole"
type: functional-requirement
status: draft
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
used-by: ["[[EPIC-002-wizyta]]", "[[EPIC-003-zrozumienie]]"]
user-stories: ["[[US-003-przepisanie-rodziny]]"]
NFR: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF Step 0 (family group sheet) · §5a G6 · Data model → Family"
created: 2026-10-05
updated: 2026-10-08
---

# FR-002 — Rodzina jako rekord

## Requirement
**Rodzina** jest osobnym rekordem: **1-2 partnerów + dzieci**, z własnymi zdarzeniami (małżeństwo,
koniec). **Osoba może być partnerem w kilku rodzinach.** Relacje między osobami wynikają z rodzin, nie są
zapisywane jako krawędzie osoba ↔ osoba.

Dane wprowadza się **całymi rodzinami** (para + dzieci naraz), nie osoba po osobie.

## Rules
- Powtórne małżeństwo = druga rodzina z tą samą osobą jako partnerem — **działa z konstrukcji**.
- Dziecko należy do rodziny (pary), nie do pojedynczego rodzica.
- Ścieżka pokrewieństwa (M5, M11) = najkrótsza droga po rodzinach — liczona na bieżąco, nigdy
  zapisywana (model danych).

## Why durable
„Małżeństwo jako krawędź" psuje się przy pierwszym powtórnym małżeństwie (pułapka z rozpoznania przed
kick-offem). Rodzina jako rekord to też odpowiednik `FAM` z GEDCOM — dzięki temu eksport GEDCOM (C2)
zostaje tani, choć go nie budujemy.

## Why entry by family
Kanon: arkusz rodziny (*family group sheet*) — wprowadzanie rodziny naraz jest szybsze niż po osobie
(odpowiedź na G6 — szybkie przepisywanie ~100 osób) i strukturalnie zapobiega pułapce krawędzi.

## In the app (2026-10-08, [[ISSUE-019-family-relations]])
- **Wpisywanie arkuszem rodziny** ([[rodzina]] A): para, dzieci, ślub i koniec związku naraz; nowe osoby powstają przy
  okazji, a osobę już wpisaną wskazuje się z listy (najpierw szukaj, potem twórz). Arkusz otwiera się z sekcji „Rodzina”
  formularza osoby („Dodaj związek”, „Dodaj rodziców”, ✎).
- **Widok przy osobie** ([[wpis-osoby]] 9a): rodzice i każdy związek z dziećmi jako chipy „Rodzic”, „Partner”,
  „Dziecko”, które otwierają wpis krewnego — także osoby bez grobu.
- **Rodzina to związek, nie tylko małżeństwo** (uwaga autora na stopie #1): po rozstaniu albo owdowieniu kolejny związek
  to kolejna rodzina ze swoimi dziećmi; owdowienie to zgon partnera, bez osobnej daty końca.
- **Reguły w warstwie danych:** 1–2 osoby w parze, co najmniej dwie osoby, nikt dwa razy, dziecko w jednej rodzinie
  rodziców. Źródło relacji: [[ADR-011-relation-claims-family-and-child-link]].
- **Poza zakresem:** kontrola cykli (ktoś w parze ze swoim dzieckiem — obserwacja ze stopu #2), rodzaj więzi dziecka
  (przysposobienie), druga rodzina rodziców.
