---
title: "Grobing — Requirements Traceability"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-05
---

# Grobing — Requirements Traceability

> Jedna macierz dla całego łańcucha: brief → EPIC → US → ISSUE. **Zasiana w dniu materializacji
> krokami ścieżki wizyty (UJ-001, brief §4a) z PUSTYMI kolumnami US i Issue** — US mają wynikać z
> kroków, więc krok bez US jest luką, którą WIDAĆ. Zasiane też: funkcje widoku 5 (zestaw funkcji, nie
> przepływ) i pozycje Must spoza ścieżki — żeby nic z Must nie było niewidoczne.

## Column ownership (so agents don't clobber each other's lanes)
> Kolumny edytuje wyłącznie ich właściciel.

| Columns | Owner |
|---|---|
| Journey step, Brief §, EPIC, US, Story Status | `docs` (strażnik vaulta; pierwsze EPIC/US wpisuje ISSUE-001, wykonywane przez `docs`) |
| Issue(s), Issue Status | `planning` |
| Quality Verdict | krytyk `quality`, gdy powstanie ([[ISSUE-003-setup-quality-critic]]); do tego czasu `qa` z `verdict-reviewer: self-check` |

## Matrix

| Journey step | Brief § | EPIC | US | Issue(s) | Story Status | Issue Status | Quality Verdict |
|---|---|---|---|---|---|---|---|
| UJ-001 · 1 — mapa Polski z cmentarzami rodziny; wybór, dokąd jechać | §4a · §5 M2 | | | | | | |
| UJ-001 · 2 — na miejscu: mapa cmentarza, pinezki, adres zarządcy, link do Grobonetu | §4a · §5 M3 | | | | | | |
| UJ-001 · 3 — dojście do pinezki; porównanie ze zdjęciem nagrobka | §4a · §5 M3/M4 | | | | | | |
| UJ-001 · 4 — grób: wszyscy pochowani, zdjęcie + imię | §4a · §5 M4 | | | | | | |
| UJ-001 · 5 — osoba: kim była, pokrewieństwa, ścieżka do „ja" | §4a · §5 M5 | | | | | | |
| UJ-001 · 6 — poprawa na miejscu: pinezka, nowe zdjęcie, imię z tablicy | §4a · §5 M6 | | | | | | |
| UJ-001 · 7 — powrót na mapę cmentarza → następny grób | §4a · §5 M3 | | | | | | |
| n/a — widok 5 (zestaw funkcji): drzewo | §5 M9 | | | | | | |
| n/a — widok 5: suwak czasu | §5 M10 | | | | | | |
| n/a — widok 5: ścieżka między dowolnymi dwiema osobami | §5 M11 | | | | | | |
| n/a — poza ścieżką (warunek kroku 1): wprowadzanie danych całymi rodzinami | §5 M1 | | | | | | |
| n/a — poza ścieżką (NFR): działa bez zasięgu | §5 M7 | | | | | | |
| n/a — poza ścieżką: kopia z odtworzeniem + eksport + notka przekazania | §5 M8 | | | | | | |

> Jedna US może pokrywać 1-3 kolejne kroki — wpisz ją raz i zaznacz zakres. Każda US musi mieć brief §
> w górę i ≥1 issue w dół. Pusta komórka „Brief §" albo „Issue(s)" to luka.

## Open gaps
- W dniu materializacji żaden wiersz nie ma US ani Issue — **tak ma być**.
  [[ISSUE-001-materialize-backlog]] AC-3b przypisuje każdy krok do EPIC-a; krok bez EPIC-a trafia <!-- placeholder-ok: real wikilink -->
  tutaj z nazwy.
