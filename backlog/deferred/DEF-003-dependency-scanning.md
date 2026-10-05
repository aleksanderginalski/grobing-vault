---
title: "DEF-003 — Dependency / SCA scanning — deferred requirement"
type: issue
status: deferred
deferred-until: PRODUKCJA
trigger: "the first CI pipeline is set up (pairs with DEF-005)"
category: security
priority: COULD
created: 2026-10-05
updated: 2026-10-05
---

# DEF-003 — Skanowanie zależności

## What
Automatyczne skanowanie zależności pod znane podatności. Do tego czasu obowiązuje twarde minimum:
zależności wyłącznie z zaufanych rejestrów.

## Why deferred
Bez CI nie ma gdzie tego wpiąć; ręczne skanowanie raz na jakiś czas zostałoby zapomniane.

## Activation condition
Wdrożyć, gdy: **powstaje pierwszy pipeline CI.**
