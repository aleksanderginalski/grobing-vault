---
title: "ADR-003 — Cemetery map: schematic plan from OpenStreetMap offline, GUGiK orthophoto online, sectors and pins as the author's data"
type: adr
status: accepted
supersedes: []
quality-verdict: APPROVED
verdict-date: 2026-10-08
verdict-reviewer: self-check
decided-by: "[[SPIKE-001-map-source-offline]] + decyzja autora na stopie #2 (2026-10-08)"
source: "PROJECT_BRIEF §Architecture → Stack (S-MAP) · §6 N5 · §3b H3, H9, H10 · MoSCoW W3"
created: 2026-10-05
updated: 2026-10-08
---

# ADR-003 — Mapa cmentarza: plan offline, zdjęcie online

> Architecture Decision Record. **`accepted` 2026-10-08** — zamknął go [[SPIKE-001-map-source-offline]].
> Pomiary są w *Findings* spike'a (M1–M11), a decyzja autora w *Verification* → *Stop #2*.

## Status
accepted — 2026-10-08.

## Context
- Widok 2 (mapa cmentarza) i krok 6 ścieżki (pinezka tam, gdzie stoję) stoją na mapie. Widok 1 (mapa Polski)
  rozstrzygnął osobno [[ADR-007-poland-map-bundled-data]].
- Mapa ma działać **bez zasięgu** ([[NFR-001-offline]], M7). Warunki dostawców, a nie framework, decydują, co
  wolno trzymać offline (brief §6 N5).
- Cmentarze autora: 8 pozycji (11 cmentarzy). Liczby z pomiarów są w *Findings* spike'a, bez nazw (vault
  publiczny, [[NT-008-publication-review]]).
- **Co wolno, a czego nie** (SPIKE-001):
  - ortofotomapę GUGiK wolno pobrać i używać dowolnie, za 0 zł (M5);
  - Mapbox i Esri pozwalają na offline tylko we własnych SDK, a Google wcale (M5);
  - plany z kwaterami i mapy grobów mają tylko zarządcy (plany w sieci: 8 z 11, wyszukiwarka grobów: 11 z 11),
    bez prawa kopiowania i bez offline (M1–M4);
  - OSM nie ma kwater na cmentarzach autora: 1 kwatera na 8 obszarów (M10), ale ma obrysy i, na połowie
    obszarów, gęstą sieć alejek (M11).
- **Autor obejrzał szkic na emulatorze (M11)** i wybrał plan schematyczny w stylu B, „jak Grobonet, w naszych
  kolorach”, z kwaterami i pinezkami, które zaznacza sam. Zdjęcie ma być **tylko online**.

## Decision
1. **Plan schematyczny offline z OpenStreetMap (ODbL).**
   - Plan to obrys cmentarza i alejki, w tokenach stylu B: teren w kolorze powierzchni, alejki, obrys.
   - Pobiera się raz, **przy dodaniu cmentarza**, i zostaje w telefonie.
   - Bez sieci w tym miejscu jest **zaślepka „pobierz, gdy będzie internet”** (decyzja autora).
   - Podpis: „© OpenStreetMap”.
   - Źródło zapytania (Overpass albo inne) wybiera pozycja, która to buduje. Publiczny Overpass był w tej sesji
     zawodny (M11), więc **ponawianie i zaślepka są warunkiem**.
2. **Ortofotomapa GUGiK tylko online**, jako warstwa do włączenia: WMTS `StandardResolution`, EPSG:3857, do z19,
   podpis „Ortofotomapa: GUGiK”. Nic nie jest zapisywane w telefonie. Służy do zaznaczania kwater i pinezek w domu,
   przy sieci.
3. **Kwatery i groby to dane autora**, a nie dane z zewnątrz.
   - **Kwatera** to nazwana strefa, którą autor zaznacza na planie albo na zdjęciu według planu zarządcy. Zaznacza
     tylko kwatery, w których leży rodzina.
   - **Grób** ma pinezkę (ze źródłem: zaznaczona w domu albo z GPS na miejscu) i adres zarządcy (kwatera, rząd,
     miejsce), który autor znajduje sam, szukając po nazwisku w wyszukiwarce zarządcy, i przepisuje.
   - **Siatki wszystkich grobów nie ma**, bo to dane zarządców ([[NT-004-grobonet-link-terms]], W3).
4. **Uprawnienie `INTERNET`** wchodzi do aplikacji wyłącznie po to, żeby pobrać plan (pkt 1) i wyświetlić zdjęcie
   online (pkt 2). Wszystko inne działa bez sieci → [[NFR-005-dane-nie-opuszczaja-telefonu]] → *Notes*.
5. **Koszt: 0 zł.** H10 potwierdzona, więc folder `06_NON_TECH/` nie powstaje (`doc-growth.md`: folder powstaje przy
   pierwszym koszcie).

## Options considered

| Option | Pros | Cons | Why (not) chosen |
|---|---|---|---|
| **Plan OSM offline + ortofotomapa GUGiK online + kwatery i pinezki autora** | czytelny schemat, jak plan przy bramie; mały i offline; wolno go użyć; zdjęcie bez zajmowania pamięci | kwatery zaznacza autor; na połowie cmentarzy OSM ma tylko pojedyncze alejki (M11); zdjęcia nie ma na cmentarzu bez sieci | **wybrana** przez autora po szkicu na emulatorze |
| Ortofotomapa GUGiK offline (pobrana obszarami; narzędzie na PC albo pobieranie w aplikacji) | działa na cmentarzu bez sieci; ok. 10,5 MB dla 8 obszarów (M8); prototyp offline działa (M7) | na zdjęciu „mało co widoczne” pod drzewami (autor; M6: 1 z 8 obszarów pod drzewostanem); zajmuje miejsce | odrzucona przez autora; **odwracalna**: zapis w telefonie da się dołożyć do pkt 2, gdy na miejscu zabraknie zdjęcia |
| Mapbox Satellite / Esri World Imagery | globalne pokrycie | offline tylko w ich SDK (drugi silnik mapy), konto i klucz (M5) | rejected |
| Google Map Tiles API | — | offline zakazane (M5) | rejected |
| Plany zarządców (Grobonet, systemy parafii) jako mapa w aplikacji | wszystkie groby i kwatery | zakaz kopiowania, tylko online (M3, M4) | rejected — **link, nigdy kopia** (W3) |
| Mapy tylko online (status quo) | zero pracy | łamie M7 / [[NFR-001-offline]] | rejected |

## Consequences
- **Positive:**
  - widok 2 może ruszyć jako pozycja EPIC-002, z projektem `ui` i makietą przed kodem;
  - plan jest lekki i działa offline;
  - zdjęcie nie zajmuje miejsca;
  - luka 1 (grób bez pinezki) ma przepływ (`TRACEABILITY.md` → *Open gaps* 1).
- **Negative / trade-offs:**
  - aplikacja dostaje `INTERNET`, więc NFR-005 pilnuje od teraz kod, a nie system;
  - zapytania o plan i o zdjęcie mówią serwerom OSM i GUGiK, którym obszarem interesuje się telefon autora (adres
    IP);
  - kwatery to praca autora;
  - na cmentarzu bez sieci nie ma zdjęcia.
- **Follow-ups:**
  - ✅ Mapa Polski działa offline z Natural Earth ([[ADR-007-poland-map-bundled-data]], 2026-10-06);
  - pozycja EPIC-002 „mapa cmentarza”: model **kwatery** (nazwa + strefa) i **pinezki grobu** (źródło,
    dokładność), pobieranie planu z ponawianiem, warstwa zdjęcia, pole „link do wyszukiwarki zarządcy” (*Findings*
    → rekomendacja 6, bez decyzji autora), wygląd od `ui` ([[cmentarz]] D1 zakładał zdjęcie nad listą, więc do
    zmiany przez `ui`);
  - pułapka w `flutter_map`: `CameraConstraint.contain` przy ramce mniejszej od ekranu (M7);
  - sprawdzenie na miejscu (GPS przy grobie, plan przy bramie) → `CURRENT_STATE.md` → §Parked.
