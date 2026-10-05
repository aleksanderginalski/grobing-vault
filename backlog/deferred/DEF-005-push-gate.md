---
title: "DEF-005 — Push-triggered drift gate (CI-T1) — deferred requirement"
type: issue
status: deferred
deferred-until: PRODUKCJA
trigger: "the first push of any Grobing repo to a remote"
category: maturity
priority: SHOULD
created: 2026-10-05
updated: 2026-10-05
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
