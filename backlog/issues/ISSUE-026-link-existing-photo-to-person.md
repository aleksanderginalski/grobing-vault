---
title: "ISSUE-026 — Add a photo already in the app to a person (from the person's side)"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[ISSUE-024-person-view]] — uwaga autora na stopie #1, runda 1 („…lub połączyć z istniejącymi”), osobna pozycja decyzją autora w rundzie 2 („jest dobrze”), [[osoba]] *Open* 6"
created: 2026-10-12
updated: 2026-10-12
---

# ISSUE-026 — Zdjęcie z aplikacji dla osoby

> Z zamknięcia [[ISSUE-024-person-view]]. Autor o sekcji „Zdjęcia” w widoku osoby: *„chciałbym mieć dla osoby bez zdjęć również
> miejsce na »zdjęcia« abym wiedział że mogę tutaj je dodać na dole (lub połączyć z istniejącymi)”*. Pierwszą część zbudowała
> ISSUE-024 (D20); „połączyć z istniejącymi” to osobna pozycja (decyzja autora, stop #1 ISSUE-024, runda 2).

## What to build
- **Trzecie źródło w arkuszu zdjęć osoby** ([[zdjecie]] A, tryb osoby): obok „Wybierz z galerii” i „Zrób zdjęcie” — **„Ze zdjęć w
  aplikacji”** (zdjęcie, które już jest u innej osoby, np. grupowe).
- **Ekran wyboru** spośród zdjęć wszystkich osób: jak znaleźć jedno wśród kilkuset (siatka według osób, wyszukiwarka imion),
  zaznaczenie kilku, „Gotowe”. Projekt: `ui` — specyfikacja i makieta przed planem (nowy ekran).
- Wybrane zdjęcia dostają łącze do tej osoby (na końcu jej kolejności), plik zostaje jeden ([[ADR-009-person-photos-record-and-link]]);
  zapis jak reszta zmian zdjęć osoby. Także w wyborze tła ([[zdjecia-osoby]] v1.4) — do decyzji przy projekcie.

## Acceptance Criteria
- **AC-1** *Given* zdjęcie grupowe u Marii *When* w zdjęciach Jana wybieram „Ze zdjęć w aplikacji” i to zdjęcie *Then* po
  zapisie jest ono u Jana i u Marii, a plik jest jeden.
- **AC-2** *Given* kilkaset zdjęć w aplikacji *Then* zdjęcie konkretnej osoby da się znaleźć bez przewijania wszystkiego (np. po
  imieniu osoby na zdjęciu).

## Notes
- Dziś to samo da się zrobić od strony zdjęcia: podgląd u osoby, która je ma → „Na zdjęciu · Zmień” → zaznaczyć drugą osobę
  ([[zdjecie]] D).
- Bez zmiany schematu (łącze osoba–zdjęcie istnieje od v4).
