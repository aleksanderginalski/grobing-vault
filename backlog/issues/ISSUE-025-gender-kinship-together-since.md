---
title: "ISSUE-025 — Gender back in the person form, Polish kinship names, union 'together since', no sources in the form"
type: issue
status: ready
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[SPIKE-004-mvp-flow-prototype]] D16, D20, D28 (decyzje autora na prototypie, 2026-10-08)"
created: 2026-10-08
updated: 2026-10-08
---

# ISSUE-025 — Płeć, nazwy pokrewieństwa, „Razem od”, formularz bez źródeł

> Z zamknięcia [[SPIKE-004-mvp-flow-prototype]]. Jedna zmiana schematu dla trzech rzeczy w danych osoby i rodziny.
> Specyfikacja: [[wpis-osoby]] v5.4 (4a; elementy 9–10 bez źródła), [[rodzina]] v1.4, [[osoba]] D4, [[drzewo]] D4, D6.

## What to build
- **Płeć** (D16): pole „Płeć” (Kobieta · Mężczyzna) w formularzu osoby, podpowiadane z imienia, poza `next`
  ([[wpis-osoby]] 4a, kształt z v5). **Zmiana schematu:** kolumna płci, migracja z testem (bez wartości dla istniejących
  osób; formularz podpowie przy pierwszej poprawie).
- **Nazwy pokrewieństwa po polsku** (D16): z płci i strony ścieżki do „ja” — mama/tata, babcia/dziadek, stryj/wuj/ciotka,
  rodzeństwo stryjeczne/wujeczne/cioteczne, teść/teściowa, szwagier/szwagierka… oraz **opis złożony z odcinków** w
  dopełniaczu („siostra cioteczna babci mojej żony”, [[drzewo]] D6). **Słownik ze źródłem** (kanon polskiej terminologii
  pokrewieństwa), nie z pamięci; test na tabeli przypadków. Chipy i role w arkuszu rodziny z płci ([[rodzina]] v1.3).
- **„Razem od”** (D20, [[rodzina]] v1.4): w arkuszu rodziny obok „Ślubu” data początku związku; zdarzenie rodziny jak
  ślub. Związek bez ślubu: „Partner/Partnerka”.
- **Formularz bez źródeł** (D28): bez linii „Źródło: notatki · Zmień” przy „kim była” i bez tekstu „Daty i miejsce
  pochówku zapiszą się ze źródłem: notatki”. Dane dalej zapisują się z domyślnym źródłem w schemacie — bez migracji.

## Acceptance Criteria
- **AC-1** *Given* osoba „Maria” *When* otwieram formularz *Then* „Płeć” jest podpowiedziana jako Kobieta; zapis ją
  utrwala.
- **AC-2** *Given* ścieżka Ja → rodzic (mężczyzna) → jego rodzic → jego córka *Then* nazwa to „ciotka”; brat ojca —
  „stryj”, brat matki — „wuj”; dziecko siostry ojca — „brat/siostra cioteczna”.
- **AC-3** *Given* para z „Razem od” 1980 i „Ślubem” 1985 *Then* obie daty są zapisane, a chip po ślubie mówi „Mąż/Żona”.
- **AC-4** *Given* kopia sprzed migracji *When* odtwarzam ją *Then* dane są pełne, osoby bez płci, związki bez „Razem od”.
- **AC-5** formularz nie pokazuje źródła ani przy „kim była”, ani przy datach.
