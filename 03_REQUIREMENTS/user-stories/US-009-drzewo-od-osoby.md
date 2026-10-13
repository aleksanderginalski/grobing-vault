---
title: "US-009 — See the family around one person and how it connects (drzewo od osoby)"
type: user-story
status: in-progress
epic: "[[EPIC-003-zrozumienie]]"
persona: "[[P1-zbierajacy]]"
moscow: [M9]
journey-steps: "n/a — funkcja widoku 5 (PROJECT_BRIEF §4a)"
FR: ["[[FR-002-rodzina-jako-rekord]]"]
NFR: ["[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
issues: ["[[ISSUE-033-tree-from-a-person]]", "[[ISSUE-034-tree-presentation-mode]]"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[SPIKE-002-tree-on-a-phone]] → *Findings*, *Rekomendacja* · [[drzewo]] v1.4 (elementy 1–5, D1–D3, D6, D8–D11) · [[SPIKE-004-mvp-flow-prototype]] D20, D25 · [[ISSUE-024-person-view]] (dawne AC-6)"
created: 2026-10-13
updated: 2026-10-13
---

# US-009 — Drzewo od osoby

## Story
**Jako** Zbierający **chcę** zobaczyć rodzinę wokół wybranej osoby — z powinowatymi i powtórnymi związkami — i przestawiać środek
na kolejne osoby, **żeby** zrozumieć, jak łączą się ze sobą ludzie z grobów i ze mną.

## Acceptance Criteria
- **AC-1 — od „Ja”.** *When* otwieram zakładkę „Drzewo” *Then* w środku stoi „Ja” na poziomie 2: rodzice, partner, dzieci, rodzeństwo,
  dziadkowie, rodzina partnera po prawej; rzędy według pokolenia, linie według rodzaju relacji ([[drzewo]] element 4).
- **AC-2 — przestawianie środka.** *When* dotykam osobę *Then* ona staje w środku z animacją, a karta pokazuje imię, lata i kim jest
  dla mnie; dotknięcie osoby w środku albo „Pokaż” → [[osoba]].
- **AC-3 — dalsza rodzina (S2).** *When* oddalam (dwa palce albo przycisk −) *Then* drzewo dokłada kolejny poziom (4 progi) i na chwilę
  pokazuje „Poziom N · M osób”; przybliżanie (dwa palce, podwójne dotknięcie albo +) zabiera dalszą rodzinę ([[drzewo]] element 3).
- **AC-4 — ślad dalszej rodziny.** *Given* osoba ma rodzinę poza widokiem *Then* przy niej jest krótka, blada, przerywana kreska: w górę
  rodzice, w dół dzieci, w bok partner ([[drzewo]] D9).
- **AC-5 — nazwa pokrewieństwa w karcie** (dawne AC-6 [[ISSUE-024-person-view]]). *Given* ścieżka Ja → tata → jego rodzic → jego córka
  *Then* karta mówi „ciotka”; brat ojca — „stryj”, brat matki — „wuj”; dziecko siostry ojca — „brat/siostra cioteczna”; dalsze
  pokrewieństwo — opis z odcinków („Siostra cioteczna babci Twojej żony”, [[drzewo]] D6, D12; „Twojej” — decyzja autora G1 na stopie #1
  [[ISSUE-033-tree-from-a-person]], 2026-10-13). Słownik ze źródłem:
  [[ISSUE-025-gender-kinship-together-since]] → *Prior art* i D2.
- **AC-6 — „Pokaż w drzewie”.** *When* w widoku osoby dotykam „Pokaż w drzewie” *Then* drzewo otwiera się z tą osobą w środku
  ([[osoba]] D11).
- **AC-7 — tekst 200% na 360 dp.** Imiona nie są ucięte tak, że mylą osoby (miejsce osoby rośnie z tekstem jak w mini-drzewie, najwyżej
  160 dp — [[osoba]] v2.2), inicjały mieszczą się w okręgu.
- **AC-8 — tryb prezentacji** ([[drzewo]] D11). *When* włączam tryb prezentacji *Then* drzewo jest poziomo, na pełnym ekranie, na poziomie 2,
  bez przycisków; obraz na telewizor daje systemowe „Przesyłaj ekran”. *Może wyjść do osobnej pozycji przy planowaniu.*

## Out of scope
- Czas na drzewie → [[US-010-czas-na-drzewie]]; „Połącz dwie osoby” → [[US-011-polacz-dwie-osoby]].
- Całe drzewo naraz (K1) — nie w MVP ([[drzewo]] D1, stop #1 SPIKE-002).

## Notes
- **Pierwszy krok pozycji:** wymyślona rodzina o kształcie prawdziwej w buildzie debug (`lib/dev/fictional_data.dart`; SPIKE-002 D6) —
  kształt w [[SPIKE-002-tree-on-a-phone]] → *Rekomendacja* (same liczby).
- **Układ:** własny, port algorytmu makiety, z testami; bez nowej zależności (`graphview` odpadł w M2).
- **Wejścia z *Findings*:** optymalizacja rysowania przy przejściu między poziomami (M3), skala S2 z osi x, a nie z
  `getMaxScaleOnAxis()`, imiona przy oddalaniu ([[drzewo]] *Open* 5), ikona „Połącz dwie osoby” ([[drzewo]] *Open* 1a).
- Na fizycznym telefonie (czas „kim jest X dla mnie”, płynność, progi S2) → [[ISSUE-032-mvp-install]] → *Hand checks*.
