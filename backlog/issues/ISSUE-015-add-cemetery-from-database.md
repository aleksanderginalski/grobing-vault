---
title: "ISSUE-015 — Add a cemetery from a bundled cemetery database (OpenStreetMap, offline): search section, preview, satellite link"
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
source: "decyzja autora 2026-10-06 na stopie #1 ISSUE-014 (*„miałem nadzieję, że będziemy to dodawać z jakiejś bazy cmentarzy”*; podział — *„wygląda dobrze”*) · ISSUE-014 → Stop #1 — round 1, D8–D10 · 05_DESIGN/cmentarze.md v2 · 01_INBOX/2026-10-05-plany-cmentarzy.md → Related idea"
created: 2026-10-06
updated: 2026-10-06
---

# ISSUE-015 — Dodanie cmentarza z bazy cmentarzy

> **Decyzja autora 2026-10-06** (stop #1 [[ISSUE-014-home-map-of-poland]]): cmentarz dodaje się z bazy
> cmentarzy, *„aby mieć pewność, że dodajemy odpowiedni cmentarz w odpowiedniej lokalizacji”*. Autor przyjął
> podział: ISSUE-014 robi mapę i ręczne dodanie, a ta pozycja dokłada bazę zaraz po niej (kolejność w
> `CURRENT_STATE.md`). Pomiary, na których stoi: ISSUE-014 → *Stop #1 — round 1* (falsyfikator: 8 z 8
> cmentarzy autora jest w bazie) i *Decisions for stop #1 — round 2* (D8–D10).

## What to build
1. **Wyciąg cmentarzy Polski z OpenStreetMap** jako zasób aplikacji (ok. 16 tys. cmentarzy, ok. 2 MB),
   z odtwarzającym go skryptem w `tool/`. Każdy cmentarz ma: nazwę (także nazwy dodatkowe: potoczne,
   oficjalne), środek, wyznanie (jeśli jest), **miejscowość do wyświetlenia** (najbliższa z uwzględnieniem
   rangi), **miejscowości w zasięgu jako słowa do szukania** i **województwo** z Natural Earth admin-1
   (ISSUE-014 D9). Duplikaty scalone.
2. **Sekcja „Z bazy cmentarzy”** w wyszukiwarce ([[cmentarze]] element 12): wyniki z województwem i
   wyznaniem, oznaczenie „Dodany” przy cmentarzu, który już jest u autora, podpis „© współtwórcy
   OpenStreetMap (ODbL)” i „Nie ma go w bazie — dodaj ręcznie”.
3. **Podgląd cmentarza z bazy** ([[cmentarze]] element 14): mapa przybliżona do punktu, znicz w obrysie, link
   **„Zobacz zdjęcie satelitarne ↗”** (intencja `geo:`, tylko po dotknięciu — ISSUE-014 D10) i „Dodaj ten
   cmentarz”.
4. **Okno z danymi z bazy** ([[cmentarze]] element 15): nazwa i miejscowość do poprawy przed zapisem, punkt z
   bazy, „Zapisz” bez kroku wskazania.

## Acceptance Criteria
- [ ] Bez sieci wyszukiwarka znajduje cmentarz z bazy po nazwie, po nazwie dodatkowej (potocznej) i po
      miejscowości. Polskie znaki i końcówki odmiany nie są potrzebne ([[cmentarze]] D3).
- [ ] Każdy wynik z bazy pokazuje miejscowość i województwo; ta sama nazwa w dwóch województwach to dwa
      rozróżnialne wyniki.
- [ ] Podgląd pokazuje cmentarz na mapie przed dodaniem. Link otwiera zewnętrzną aplikację map w tym punkcie,
      a bez dotknięcia aplikacja niczego nie wysyła.
- [ ] Dodanie z bazy zapisuje nazwę (poprawioną albo z bazy), miejscowość i punkt z bazy. Na mapie pojawia
      się znicz, a cmentarz w wynikach dostaje „Dodany”.
- [ ] Podpis ODbL jest widoczny przy wynikach z bazy; wyciąg w repo ma licencję ODbL i opis pochodzenia.
- [ ] APK release dalej **nie ma uprawnienia `INTERNET`**.
- [ ] Ekran według specyfikacji `ui` ([[cmentarze]] v2) i wytycznych stylu B.

## Out of Scope
- Kwatery, plany cmentarzy z kwaterami, zdjęcie satelitarne **w aplikacji** i granice cmentarza →
  [[SPIKE-001-map-source-offline]].
- Aktualizacja bazy w aplikacji (z sieci). Nowy wyciąg = nowa wersja aplikacji ze skryptu.
- Identyfikator obiektu OSM w schemacie (zmiana schematu) — punkt wystarcza do „Dodany” i do późniejszego
  dopasowania. Wraca, gdy SPIKE-001 będzie importować granice.
- Granice gmin (PRG / relacje OSM) — zbędne według pomiaru (ISSUE-014 D9).

## Technical Notes
- **Źródło i licencja:** OpenStreetMap (Overpass API, `landuse=cemetery` + `amenity=grave_yard` w granicach
  Polski, miejscowości `place=city|town|village|hamlet|suburb`), [ODbL](https://www.openstreetmap.org/copyright):
  podpis w aplikacji, wyciąg w publicznym repo na ODbL. Województwa: Natural Earth (domena publiczna).
- **Wyniki falsyfikatora** (ISSUE-014): 16 532 obiekty → 16 043 cmentarze po scaleniu, 60% z nazwą, 2,1 MB
  JSON (0,43 MB po kompresji). Potoczna nazwa bywa w `loc_name`; odmiana psuje dopasowanie całych słów; w
  danych są błędy. Stąd podgląd i link.
- **Miejscowość (D9):** najbliższa z uwzględnieniem rangi (zasięg: miasto 12 km, miasteczko 5 km, wieś 2,5 km,
  przysiółek 1,5 km), a do szukania wszystkie w zasięgu. Zmierzone na 8 cmentarzach autora: 7 z 8 do
  wyświetlenia, 8 z 8 do znalezienia, 8 z 8 województw.
- **Testy tylko na publicznych przykładach**, nigdy na cmentarzach autora (`family-data.md`): np.
  „powazki” → Cmentarz Powązkowski (Warszawa), „krakow rakowicki” → Cmentarz Rakowicki (Kraków). Sprawdzenie na
  cmentarzach autora robi agent w pamięci i zapisuje tylko liczbę.
- **Link `geo:`** — sposób wywołania (paczka `url_launcher` albo kilka linii w `MainActivity`) wybiera plan;
  nowa zależność wymaga zgodności z przypiętym Flutterem (ADR-002) i braku wysyłania danych (NFR-005).
- **Wczytanie bazy:** ok. 2 MB przy pierwszym wejściu w wyszukiwarkę; specyfikacja dopuszcza pasek postępu
  powyżej ok. 0,3 s. Do zmierzenia na emulatorze.

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-014-home-map-of-poland]] (mapa, wyszukiwarka z sekcjami, okno, tryb wskazania) | technical | `in-progress` |
| specyfikacja `ui` — [[cmentarze]] v2 (elementy 12–15, D16–D20) | design | gotowa (2026-10-06) |
| [[US-002-przepisanie-grobu]] | product | `in-progress` |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP):
- test happy-path dla każdego AC;
- ręczna weryfikacja na emulatorze, w tym tryb samolotowy;
- zapis cmentarza przez API danych z ISSUE-014 (kopia w tle zamawia się sama);
- zero danych rodziny w zmianach — w testach i przykładach wyłącznie publiczne albo wymyślone cmentarze.
