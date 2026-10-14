---
title: "ISSUE-036 — Cast from the app: a button on the tree opens the system's screen-cast list, then presentation mode — one touch, as „Przesyłaj” in Google Photos"
type: issue
status: ready
delivery-style: task-level
priority: MUST
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-009-drzewo-od-osoby]]"
depends-on: "[[ISSUE-034-tree-presentation-mode]]"
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "decyzja autora na stopie #2 [[ISSUE-034-tree-presentation-mode]] (2026-10-14: *„chciałem aby ten tryb telewizora streamował obraz do smart TV … jak w Youtube”*; rekomendacja `qa` przyjęta „tak”) · [[drzewo]] D11, D26"
created: 2026-10-14
updated: 2026-10-14
---

# ISSUE-036 — Przesyłaj z aplikacji

> Z zamknięcia [[ISSUE-034-tree-presentation-mode]] (`docs`, 2026-10-14). Autor chce wybierać telewizor z poziomu aplikacji, tak jak „Przesyłaj” w
> Zdjęciach Google. Tryb prezentacji (ISSUE-034) układa obraz, ale do przesyłania trzeba dziś szukać kafelka w szybkich ustawieniach.
> **Pozycja zmienia ekran → `ui` przed `planning`.**

## What to build
1. **Przycisk „Przesyłaj”** w drzewie (miejsce i ikona — `ui`; np. `cast` przy ikonie telewizora albo w trybie prezentacji), który otwiera
   **systemową listę przesyłania ekranu**. Zmierzone na emulatorze (Android 16, 2026-10-14): `Settings.ACTION_CAST_SETTINGS` otwiera ekran
   „Google Cast” z listą urządzeń w pobliżu (`com.android.settings/.Settings$WifiDisplaySettingsActivity`).
2. Po wyborze telewizora — tryb prezentacji (kolejność i to, czy przycisk sam włącza tryb, rozstrzyga `ui`).
3. **Bez kodu sieciowego:** obraz ekranu wysyła system ([[NFR-005-dane-nie-opuszczaja-telefonu]]); bez Google Cast SDK i bez odbiornika.

## Acceptance Criteria
- [ ] *When* dotykam „Przesyłaj” *Then* otwiera się systemowa lista urządzeń do przesyłania ekranu.
- [ ] Telefon bez tej listy (inny producent) *Then* aplikacja nie pada, a podpowiedź z trybu prezentacji mówi, gdzie szukać przesyłania ([[drzewo]] D26).

## Out of scope
- **Casting** — odbiornik Google Cast na telewizorze rysuje drzewo, telefon jest pilotem (jak YouTube, Zdjęcia): po MVP i tylko gdy przesyłanie
  ekranu nie wystarczy; wymaga ADR zmieniającego NFR-005, odbiornika na HTTPS i rejestracji Google Cast ([[ISSUE-034-tree-presentation-mode]] →
  *Verification* → *Stop #2*).
- Sprawdzenie z telewizorem autora → [[ISSUE-032-mvp-install]] → *Hand checks*.

## Notes
- Telewizor autora jest odbiornikiem Google Cast w tej samej sieci Wi-Fi (zrzut autora z Zdjęć, stop #2 ISSUE-034).
- Prior art do sprawdzenia przy planie: dokumentacja `Settings.ACTION_CAST_SETTINGS` (Android) i zachowanie na telefonach bez Google Cast (np. Samsung
  „Smart View”) — przy planie, ze źródłem.
- Kanał natywny: wzorzec `ExternalLinks` w `MainActivity.kt` (otwiera intencję z aktywności).
