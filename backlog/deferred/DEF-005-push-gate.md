---
title: "DEF-005 — Push-triggered drift gate (CI-T1) — deferred requirement"
type: issue
status: deferred
deferred-until: PRODUKCJA
trigger: "the first push of any Grobing repo to a remote"
category: maturity
priority: SHOULD
created: 2026-10-05
updated: 2026-10-08
---

# DEF-005 — Bramka dryfu na pushu

## What
Czwarty trigger mechanizmu z Meta-decyzji 3g: check uruchamiany na push/PR, z filtrem ścieżek
wyprowadzonym z tego, **co agenci faktycznie czytają** (nie z tego, co wygląda na konfigurację) — łącznie
z plikiem samego filtra.

## Why deferred
Nie ma jeszcze zdalnego repo ani CI. Do tego czasu działają trzy pozostałe triggery
([[ISSUE-004-setup-freshness-gate]]).

## Activation condition
Wdrożyć, gdy: **którekolwiek repo Grobing dostaje pierwszy push na zdalne repo.**

**Czego NIE da:** niczego między pushami — agent może zaplanować całą sesję na fałszywym dokumencie,
który ta bramka poprawnie odrzuci godzinę później.

## Wake — 2026-10-07
Warunek aktywacji spełniony: trzy repo Grobing dostały pierwszy push na publiczny GitHub (za „go” autora,
`CURRENT_STATE.md` → *Recently done*). Obudzenie nie jest zgodą na budowę. Co z tego wynika:
- bramka to check w pipelinie CI na push/PR, a pipeline'u nie ma. Agent `ci` powstaje na sygnał „pierwszy
  pipeline” (`grobing-agents/CLAUDE.md`), a ten sam pipeline budzi [[DEF-003-dependency-scanning]];
- filtr ścieżek ma wynikać z tego, co agenci czytają — to samo pytanie co w
  [[ISSUE-004-setup-freshness-gate]] (trzy pozostałe triggery, jeszcze niezbudowane);
- **decyzja autora:** wdrożyć teraz (pozycja + `ci`) albo zostawić do `deferred-until: PRODUKCJA`. Do tej
  decyzji status zostaje `deferred`.

## Decision — 2026-10-08 ([[2026-10-08-retro-02]], R8)
Autor: **zostaje `deferred-until: PRODUKCJA`**. Powody:
- pipeline CI na GitHubie nie zna imion z notatek (lista nie może tam trafić), więc danych rodziny nie złapie. Treść
  przed `git add` sprawdza lokalnie [[ISSUE-020-content-guard]];
- dryf dokumentów łapią lokalne triggery z [[ISSUE-004-setup-freshness-gate]] (jeszcze niezbudowane).

Warunek ponownego obudzenia: wejście w etap PRODUKCJA albo pierwszy pipeline CI z innego powodu.
