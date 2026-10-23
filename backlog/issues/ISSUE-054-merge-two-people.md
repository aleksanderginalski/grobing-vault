---
title: "ISSUE-054 — Merge two entries of the same person into one, keeping what was filled in at each"
type: issue
status: withdrawn
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "`/pm` 2026-10-23 — odpowiedź autora B na pytanie o cel usuwania: osoba wpisana dwa razy (*„to co piszesz”*) — scalenie zamiast usunięcia kopii; obok [[ISSUE-053-delete-cemetery-grave-person]]"
created: 2026-10-23
updated: 2026-10-23
---

# ISSUE-054 — Scal dwa wpisy tej samej osoby

> **Wycofana 2026-10-23 decyzją autora** — na panelu 1 prototypu `ui` (discovery, start z `/pm` tego dnia): *„nie nie robimy scalania - nie potrzebuje
> tego”*. Nic nie zbudowano; specyfikację i prototyp `ui` usunął przed zapisem. Źródłem pozycji była zgoda autora na opcję zaproponowaną przez `pm`
> (*„to co piszesz”*), nie potrzeba z używania — `CURRENT_STATE.md` → *Do retro*. **Wraca, gdy** duplikat osoby przeszkodzi przy prawdziwych danych
> albo autor zacznie usuwać kopię osoby, żeby się jej pozbyć ([[wpis-osoby]] → *Decisions* → „Usuwanie osoby”, *Obali*). Treść niżej bez zmian.

> Ta sama osoba wpisana dwa razy (np. raz z notatek, raz z drzewa przy rodzinie) — usunięcie jednej kopii ([[ISSUE-053-delete-cemetery-grave-person]])
> skasowałoby to, co przy niej uzupełniono. Autor 2026-10-23: B — *„to co piszesz”*.

## What to build (kierunek — `ui` w trybie discovery przed planem)
- wybór dwóch osób (wzorzec okna „Połącz dwie osoby” — [[ISSUE-039-connect-two-people]]) albo wejście z wpisu osoby;
- **porównanie obok siebie** i wybór wartości pole po polu tam, gdzie się różnią (imiona, nazwisko, daty, płeć, „kim była”, profilowe);
- powiązania **sumują się**: związki, dzieci, rodzice, pochówki, zdjęcia, zamieszkania, ród; konflikt (np. dwa różne pochówki, dwie różne pary rodziców)
  — do decyzji `ui`;
- „Cofnij” jak w [[ISSUE-053-delete-cemetery-grave-person]].

## Prior art
- **Gramps „Merge People”** i **FamilySearch „possible duplicates”**: dwie kolumny, wybór wpisu głównego i wartości pole po polu; zdarzenia i rodziny obu
  osób przechodzą na osobę wynikową.

## Notes
- Po [[ISSUE-053-delete-cemetery-grave-person]] — wspólny mechanizm „Cofnij” i wiedza, co wisi na osobie.
- Rozpisanie AC — przy starcie pozycji (`pm` → `ui` discovery → `planning`).
