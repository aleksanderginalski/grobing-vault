---
title: "ADR-007 — Map of Poland (view 1) from bundled public data, drawn with flutter_map without tiles"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-014-home-map-of-poland]]"
source: "ISSUE-014 → Implementation plan (Prior art, Falsifier, D1–D3) · ADR-003 Follow-ups (⚠️ OPEN: mapa Polski offline) · NFR-001 · NFR-005 · ADR-002 (pinned Flutter) · brief §Architecture → Stack, §6 N5"
created: 2026-10-06
updated: 2026-10-07
---

# ADR-007 — Mapa Polski z wbudowanych danych

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-06. Autor przyjął plan na stopie #1 [[ISSUE-014-home-map-of-poland]] (*„wygląda
dobrze”*). Falsyfikator zmierzono przed planem, a mapę wdrożono i sprawdzono na emulatorze (stop #2).
Pomiary są w pozycji (*Implementation plan* → *Prior art*, *Falsifier*; *Dev report*; *Verification*) i tam
zostają (jedna liczba, jeden dom).

## Context
- Widok 1 (M2, UJ-001 krok 1): mapa Polski ze zniczami cmentarzy rodziny, od decyzji autora (2026-10-06)
  **ekran główny od startu**, także pusty.
- [[NFR-001-offline]] chce bez zasięgu wszystkich kroków UJ-001, a [[ADR-003-map-source-offline]] pyta tylko
  o zdjęcie satelitarne ~10 obszarów cmentarzy. Krok 1 był `⚠️ OPEN`.
- Publiczne kafelki OpenStreetMap zabraniają użycia offline (brief §6 N5), a aplikacja **nie ma uprawnienia
  `INTERNET`** ([[NFR-005-dane-nie-opuszczaja-telefonu]], [[ADR-004-backup-format-encryption-destination]]).
- Flutter jest przypięty na 3.41.1 ([[ADR-002-flutter-pinned]]); każda paczka musi się na nim rozwiązać.

## Decision
1. **Dane:** kontur Polski, rzeki i 9 miast z [Natural Earth](https://www.naturalearthdata.com/about/terms-of-use/)
   1:10m (domena publiczna) jako zasób aplikacji `assets/map/poland.json`, odtwarzany skryptem
   `tool/map/extract_poland.dart`. Mapa działa offline od pierwszego uruchomienia i nie zależy od dostawcy.
2. **Rysowanie:** `flutter_map` 8.3.2 (BSD 3-Clause) i `latlong2` 0.10.1, przypięte dokładnie — **wielokąt,
   linie i znaczniki, bez warstwy kafelków**.
3. **Ruch kamery:** `CameraConstraint.containCenter`, **nie `contain`** (zmierzone: `contain` na pionowym
   ekranie daje pustą mapę). Z własnym `MapController` trzeba też ustawić `initialCenter` i `initialZoom`
   na Polskę (wartości domyślne leżą poza nią i łamią ograniczenie — wyszło na emulatorze).
4. **Odpowiedź na `⚠️ OPEN` z ADR-003:** krok 1 działa offline. ADR-003 zostaje przy zdjęciu satelitarnym
   cmentarzy (R2), które dalej czeka na [[SPIKE-001-map-source-offline]].

## Options considered
| Option | For | Against | Status |
|---|---|---|---|
| **`flutter_map` bez kafelków + wbudowany kontur Natural Earth** | gesty, odwzorowanie Merkatora, ograniczenie ruchu, znaczniki o stałej wielkości i dotknięcie → współrzędne gotowe (zmierzone); offline bez dostawcy; ta sama biblioteka jest kandydatem dla SPIKE-001 | nowa zależność (14 paczek, w tym nieużywane `http`); pułapki `contain` i domyślnego środka | **chosen** |
| `CustomPainter` + `InteractiveViewer` + ten sam kontur | bez zależności | odwzorowanie, odwrócenie dotknięcia, znaczniki o stałej wielkości i ograniczenie ruchu trzeba napisać i przetestować samemu | rejected |
| Kafelki offline Polski (rastrowe albo wektorowe, np. MBTiles) | mapa z detalami (drogi, wsie) | rozmiar APK, warunki dostawcy (N5), koszt; nadmiar dla wyboru, dokąd jechać | rejected |
| Kafelki z sieci | detale, zero pracy z danymi | łamie [[NFR-001-offline]] i wymaga uprawnienia `INTERNET`, którego aplikacja świadomie nie ma | rejected |

## Consequences
- **Positive:** ekran główny działa w trybie samolotowym od startu (stop #2); APK bez `INTERNET`; dane mapy to
  ok. 37 KB, a cała zmiana dokłada ok. 1,4 MB do APK release (trzy architektury).
- **Negative / trade-offs:** kontur 1:10m przy dużym przybliżeniu nie pokazuje nic poza punktem i rzeką, więc
  maksymalne przybliżenie jest ograniczone (64× całej Polski). Wybór konkretnego cmentarza „na oko” jest
  niedokładny — stąd baza cmentarzy w [[ISSUE-015-add-cemetery-from-database]].
- **Follow-ups:**
  - Jeśli SPIKE-001 wybierze inną bibliotekę dla mapy cmentarza (np. MapLibre), aplikacja będzie miała dwie
    biblioteki map. Decyzja wtedy, w ADR-003.
  - Zmiana wersji `flutter_map` / `latlong2` to przegląd, a nie `pub upgrade` (komentarz w `pubspec.yaml`).
  - **Baza cmentarzy Polski (2026-10-07, [[ISSUE-015-add-cemetery-from-database]]):** drugi wbudowany zbiór
    danych, tym razem z OpenStreetMap: `assets/cemeteries/poland_cemeteries.json`, ok. 1,9 MB (+0,62 MB w
    APK). Licencja ODbL: baza pochodna w repo na tej samej licencji, podpis „© autorzy OpenStreetMap
    (ODbL)” w aplikacji. Ta sama zasada co mapa — nic się nie pobiera, nowy wyciąg to nowa wersja aplikacji
    ze skryptu `tool/cemeteries/`. Decyzja tego ADR-a bez zmian.
