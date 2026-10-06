---
title: "ISSUE-014 — Home screen: map of Poland (bundled outline) with the family's cemeteries as candles + add a cemetery"
type: issue
status: ready
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
used-by: "[[EPIC-002-wizyta]] (M2 — widok 1)"
user-story: "[[US-002-przepisanie-grobu]]"
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "decyzja autora 2026-10-06 (po makiecie z ISSUE-013) · references.md R1 · ISSUE-012 What to build 1 · ADR-003 Follow-ups (⚠️ OPEN: mapa Polski offline)"
created: 2026-10-06
updated: 2026-10-06
---

# ISSUE-014 — Ekran główny: mapa Polski ze zniczami cmentarzy

> **Decyzja autora 2026-10-06** (*„ok plan brzmi dobrze”*): ekran główny to od startu mapa Polski, jak
> na obrazie R1 (`05_DESIGN/brand/references.md`), a nie lista cmentarzy. Ta pozycja przejmuje punkt 1
> *What to build* z [[ISSUE-012-transcribe-grave-screen]] (wybór i dodanie cmentarza). Uwagi autora, z
> których wynika: ISSUE-012 → *Input from the author (2026-10-06)*.

## What to build
1. **Ekran główny = mapa Polski** jak w R1: kontur kraju, kilka dużych miast, subtelne rzeki. Dane z
   [Natural Earth](https://www.naturalearthdata.com/about/terms-of-use/) (domena publiczna, bez wymogu
   podpisu) są wbudowane w aplikację, więc mapa działa **offline od startu** i nie zależy od dostawcy
   kafelków. Pusta mapa, bez cmentarzy, to stan początkowy.
2. **Cmentarze rodziny jako znicze-pinezki** w punkcie cmentarza. Pola `centerLat` / `centerLon` są w
   schemacie od v1. Cmentarz bez punktu nie ma znicza, ale znajduje go wyszukiwarka.
3. **„Szukaj osoby lub cmentarza”** przeszukuje zapisane cmentarze po nazwie i miejscowości. Gdy nic nie
   znajdzie, proponuje **„Dodaj cmentarz”**: nazwa, miejscowość i opcjonalny punkt (dotknięcie na mapie).
4. **Wybór znicza** → arkusz jak w R1: nazwa, „6 grobów · 14 osób” i „Otwórz cmentarz” → ekran cmentarza
   ([[ISSUE-012-transcribe-grave-screen]]).
5. **Koło zębate → „Stan danych”.** Ekran startowy z [[ISSUE-002-bootstrap-code-repo]] znika (znak
   marki: znicz + „Grobing”, `05_DESIGN/brand/style-b.md` reguła 8).

## Acceptance Criteria
- [ ] Po starcie bez sieci (tryb samolotowy) widać mapę Polski — także pustą, bez żadnego cmentarza.
- [ ] Cmentarz dodany z punktem jest na mapie jako znicz; cmentarz bez punktu znajduje wyszukiwarka.
- [ ] Wyszukiwarka znajduje zapisany cmentarz po nazwie albo miejscowości; brak wyników → „Dodaj
      cmentarz”.
- [ ] Arkusz wybranego cmentarza pokazuje liczbę grobów i osób i otwiera ekran cmentarza.
- [ ] „Stan danych” jest pod kołem zębatym; ekranu startowego nie ma.
- [ ] Ekran według specyfikacji `ui` (`05_DESIGN/`) i wytycznych stylu B.

## Out of Scope
- Zdjęcie satelitarne cmentarza i znicze na grobach → [[SPIKE-001-map-source-offline]], potem
  [[EPIC-002-wizyta]] (M3).
- **„Baza cmentarzy z importem mapy”** (pytanie autora) → `01_INBOX/2026-10-05-plany-cmentarzy.md`;
  rozstrzyga ją SPIKE-001.
- Dolna nawigacja Mapa · Osoby · Drzewo → gdy istnieje drugi cel (`style-b.md` reguła 12).
- **Wyszukiwanie osób** (S5, Should): czy wchodzi minimum (po imieniu i nazwisku), mówi `planning` na
  stopie #1. Bez tego zakres się nie poszerza.

## Technical Notes
- **Najtańszy falsyfikator, przed planem kodu:** czy kontur Polski z Natural Earth rysuje się offline na
  przypiętym Flutterze 3.41.1. Kandydaci: `flutter_map` (BSD-3) z warstwami wielokątów i znaczników bez
  warstwy kafelków, albo własny `CustomPainter`. Do zmierzenia też: skala danych (1:10m czy 1:50m) wobec
  rozmiaru APK i wyglądu.
- **Decyzja architektoniczna:** mapa bazowa z wbudowanych danych publicznych odpowiada na `⚠️ OPEN` z
  [[ADR-003-map-source-offline]] → *Follow-ups* („mapa Polski offline czy nie”) dla widoku 1. Zapis jako
  nowy ADR albo dopisek do ADR-003 — rozstrzyga `planning`.
- Nowa zależność (pakiet mapy) wymaga sprawdzenia zgodności z przypiętym Flutterem (ADR-002) i braku
  wysyłania danych (§Security, NFR-005).
- Znicz: własna, cienka ikona wektorowa — nie ma jej w Material Icons (`style-b.md` → *Known gaps*).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-013-setup-ui-agent]] (agent `ui`) | process | `done` |
| specyfikacja ekranu od `ui` (`05_DESIGN/`) | design | do napisania przed planem (`ui` → `planning`) |
| [[US-002-przepisanie-grobu]] | product | `in-progress` |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP):
- test happy-path dla każdego AC;
- ręczna weryfikacja na emulatorze, w tym tryb samolotowy;
- zapis cmentarza idzie przez API danych (kopia w tle zamawia się sama, ISSUE-010);
- zero danych rodziny w zmianach — także nazwy i punkty cmentarzy w testach są wymyślone.
