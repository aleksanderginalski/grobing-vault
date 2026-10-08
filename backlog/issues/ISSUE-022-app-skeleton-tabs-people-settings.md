---
title: "ISSUE-022 — App skeleton: bottom bar Mapa · Osoby · Drzewo, the Osoby tab, settings under the gear"
type: issue
status: ready
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[SPIKE-004-mvp-flow-prototype]] D1, D2, D3, D19, D23 (decyzje autora na prototypie, 2026-10-08)"
created: 2026-10-08
updated: 2026-10-08
---

# ISSUE-022 — Szkielet aplikacji: dolny pasek, zakładka Osoby, ustawienia

> Z zamknięcia [[SPIKE-004-mvp-flow-prototype]]. Pierwsza pozycja w drodze do instalacji MVP: na tym szkielecie stoją
> wszystkie ekrany, które przyjdą później.

## What to build
- **Dolny pasek Mapa · Osoby · Drzewo** ([[style-b]] reguła 12, v1.12; [[cmentarze]] element 18): widoczny na ekranach do
  oglądania, ukryty w formularzach, oknach, trybach wyboru i na zdjęciu na pełnym ekranie; zakładka, z której autor
  przyszedł, zostaje aktywna na całym stosie (SPIKE-004 D1, D2).
- **Zakładka Osoby** ([[osoby]] v1): wyszukiwarka osób, „Ja” na górze, lista A–Z po nazwisku. Pokrewieństwo pod imieniem
  przyjdzie z [[ISSUE-025-gender-kinship-together-since]] — do tego czasu sam rok życia (D19).
- **Koło zębate → ustawienia** ([[ustawienia]] v1, elementy 1–7): „Ja” (wybór osoby — ustawienie „ja” z [[data-model]]),
  kopia (dzisiejsze informacje i działania z „Stanu danych”), „Eksport dla rodziny” (ekran eksportu przyjdzie z
  [[US-006-eksport-dla-rodziny]]), notka przekazania, „Stan danych” o poziom niżej (D23).
- **Wyszukiwarka na mapie zostaje „Szukaj cmentarza”** (D3, [[cmentarze]] D27) — bez zmian w kodzie.

## Acceptance Criteria
- **AC-1** *Given* ekran główny *Then* na dole są zakładki Mapa · Osoby · Drzewo, aktywna Mapa; w formularzu osoby paska
  nie ma.
- **AC-2** *When* dotykam „Osoby” *Then* widzę „Ja” i wszystkie osoby A–Z po nazwisku; wpisanie „wymys” zostawia osoby
  o nazwisku Wymyślony/Wymyślona (bez polskich znaków, od początku słowa).
- **AC-3** *When* dotykam koło zębate *Then* widzę ustawienia; „Stan danych” otwiera dzisiejszy ekran.
- **AC-4** *When* wybieram w ustawieniach „Ja” *Then* wybrana osoba jest zapisana jako „ja” i stoi na górze zakładki Osoby.

## Notes
- **Zakładka Drzewo przed zbudowaniem drzewa** — do decyzji na stopie #1: zaślepka „Drzewo powstanie po SPIKE-002”
  albo dwie zakładki do czasu drzewa (reguła 12: pasek pojawia się przy dwóch celach).
- **Zmiana zakresu** zapisana w [[osoby]]: wyszukiwanie osób (brief §5a G5, Should) wchodzi do MVP decyzją autora.
