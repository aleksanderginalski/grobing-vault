---
title: "DEF-004 — Security event logging — deferred requirement"
type: issue
status: deferred
deferred-until: PRODUKCJA
trigger: "same as DEF-002: a second person installs the app, OR store distribution"
category: security
priority: COULD
created: 2026-10-05
updated: 2026-10-05
---

# DEF-004 — Logowanie zdarzeń bezpieczeństwa

## What
Zapis zdarzeń istotnych dla bezpieczeństwa (np. nieudane odtworzenie kopii, odrzucony plik kopii).

## Why deferred
Dla jednego użytkownika na jednym urządzeniu bez sensu. **Już teraz obowiązuje (MVP): zero danych
rodziny w logach.**

## Activation condition
Wdrożyć, gdy: **aplikację instaluje druga osoba albo trafia do sklepu.**
