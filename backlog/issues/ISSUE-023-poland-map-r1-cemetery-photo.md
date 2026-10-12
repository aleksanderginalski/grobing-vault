---
title: "ISSUE-023 — Map of Poland like R1 (neighbours, Baltic, lakes, centred) and the cemetery photo in the sheet"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-12
verdict-reviewer: self-check
source: "[[SPIKE-004-mvp-flow-prototype]] D5, D6, D7 (decyzje autora na prototypie, 2026-10-08)"
created: 2026-10-08
updated: 2026-10-12
---

# ISSUE-023 — Mapa Polski jak R1 i zdjęcie cmentarza

> Z zamknięcia [[SPIKE-004-mvp-flow-prototype]]. Specyfikacja: [[cmentarze]] v2.4 (elementy 3, 6a; D28–D30),
> [[style-b]] v1.13 (rola wody, reguła 13 i 14).

## What to build
- **Mapa jak R1** (D6, [[cmentarze]] element 3, D29): sąsiednie kraje w kolorze tła, Bałtyk i jeziora w kolorze wody,
  rzeki linią wody, granica Polski w kolorze tekstu pomocniczego, napis „Polska”, 11 miast (+ Bydgoszcz, Katowice).
  Dane: Natural Earth 1:10m — rozszerzenie `tool/map/extract_poland.dart` i `assets/map/poland.json` (plus
  `ne_10m_lakes`, `ne_10m_lakes_europe`). Tokeny `water` i `waterLine` w `theme.dart`. Bez faktury terenu.
- **Wyśrodkowanie** (D7, D30): bez arkusza Polska na środku obszaru mapy; po otwarciu arkusza mapa przesuwa się płynnie
  nad arkusz.
- **Zdjęcie cmentarza w arkuszu** (D5, [[cmentarze]] element 6a, D28): miniatura 96 × 80 dp z lewej; bez zdjęcia pole
  „Dodaj zdjęcie”; podgląd ze „Zmień zdjęcie” i „Usuń zdjęcie” jak przy nagrobku ([[zdjecie]]). **Zmiana schematu:**
  zdjęcie cmentarza (jak zdjęcie grobu — wiersz `Media` z odwołaniem do cmentarza), migracja z testem, kopia po migracji.

## Acceptance Criteria
- **AC-1** *Given* ekran główny *Then* widać sąsiednie kraje, Bałtyk, jeziora, napis „Polska” i 11 miast; bez sieci.
- **AC-2** *When* dotykam znicza *Then* mapa przesuwa się nad arkusz; *When* zamykam arkusz *Then* Polska wraca na środek.
- **AC-3** *Given* cmentarz bez zdjęcia *When* dodaję zdjęcie *Then* arkusz pokazuje miniaturę; podgląd pozwala ją zmienić
  i usunąć.
- **AC-4** *Given* kopia sprzed zmiany schematu *When* odtwarzam ją *Then* dane są pełne, a cmentarze bez zdjęć.

## Notes
- **Zmiana zakresu:** zdjęcie cmentarza nie było w briefie (M1 ma zdjęcie nagrobka) — decyzja autora (D5).

## Implementation plan
> `planning`, 2026-10-12. Specyfikacja (`ui`, przed planem — bez zmian w tej pozycji): [[cmentarze]] v2.5, elementy 3, 4, 6, 6a, 9;
> D28–D30, *Open*: brak — oraz [[zdjecie]] (B, C1), [[grob]] D12 (wzór pola „Dodaj zdjęcie”), [[style-b]] v1.19 (rola wody,
> reguły 13 i 14). **Kandydaci tego, co widać** (retro 2, R6) byli na prototypie [[SPIKE-004-mvp-flow-prototype]]: mapa A albo B →
> autor wybrał B (D29), więc ten stop nie pokazuje nowych wariantów. Zbudowaną mapę autor ocenia na stopie #2 (krok odczucia 1);
> *obali:* brakuje faktury terenu → wariant C na prototypie (D29).

### Prior art
- **Z kodu** (ankieta 2026-10-12):
  - `assets/map/poland.json` (37 KB) ma kontur Polski, rzeki i 9 miast; `tool/map/extract_poland.dart` czyta trzy pliki Natural
    Earth 1:10m. **Jedyne nazwy w pliku to nazwy miast** — kraje, jeziora i rzeki idą bez nazw i tak ma zostać;
  - `PolandMap` rysuje to samo w trzech miejscach: ekran główny, podgląd z bazy (14) i tryb wskazania (16) — nowy wygląd wejdzie
    do wszystkich trzech bez osobnej pracy;
  - ekran główny trzyma Polskę nad stałym miejscem na arkusz (`_sheetRoom = 150`, `fitPadding` dołu) — dlatego dziś bez arkusza
    stoi za wysoko (D30); `_reveal` przesuwa mapę skokiem, gdy znicz stoi pod arkuszem;
  - zdjęcie nagrobka to wiersz `media` z `grave_id` (`setGravePhoto`, `deleteGravePhoto` w `photos.dart`): plik przed wierszem,
    usunięcie zdejmuje tylko wiersz, plik idzie przy sprzątaniu (ADR-008). Podgląd `PhotoViewerScreen` i okno „Usunąć zdjęcie?”
    są ogólne — wejdą bez zmian;
  - **pułapka:** `applyPersonPhotoEdits` na końcu kasuje każdy wiersz `media` bez `grave_id` i bez łącza osoby. Wiersz zdjęcia
    cmentarza nie ma ani jednego, ani drugiego, więc **każde „Zapisz” przy zdjęciach dowolnej osoby skasowałoby zdjęcia
    cmentarzy**. Warunek musi dostać `cemetery_id IS NULL` (*Data layer*, test wprost);
  - `_AddPhotoField` w `grave_screen.dart` ma już poprawną semantykę (`Semantics` z `onTap` przy `excludeSemantics` — trzy
    wcześniejsze pozycje miały tu błąd, *Do retro* w `CURRENT_STATE`). Pole w arkuszu ma powstać z tego samego widżetu, a nie od nowa.
- **Strażnik treści — najtańszy falsyfikator zrobiony przed planem** (2026-10-12): suchy przebieg strażnika na nazwach z mapy
  („Polska” i 11 miast, w tym nowe Bydgoszcz i Katowice) — **przechodzi**. Wygenerowany plik i tak idzie przez suchy przebieg
  `qa` przed `docs` (pamięć sesji: *dry-run the content guard*).

### Stop #1 (2026-10-12) — autor: „tak”
D1 = A (ADR-014, `media.cemetery_id`), D2 i D3 przyjęte, decyzje projektowe ze specyfikacji potwierdzone.

### Decisions for stop #1 (rekomendacja → „tak” przyjmuje wszystkie)
- **D1 — ADR-014 „Zdjęcie cmentarza — wiersz `media` z odwołaniem do cmentarza (schemat v9)”** (pisze łańcuch, `docs` przy
  zamknięciu):
  - **A (rekomendacja):** kolumna `media.cemetery_id` (pusta, klucz do `cemeteries`), lustro `grave_id`. Jedno zdjęcie na cmentarz
    trzyma jedna droga zapisu (jak przy nagrobku — [[grob]] D9; przy kilku wierszach pokazuje się pierwszy według `id`). Krok
    `_from8To9` to sam `addColumn`: żadnego wiersza nie dodaje i nie przebudowuje tabeli;
  - **B:** `cemeteries.photo_media_id` → `media`. Klucz z cmentarza do zdjęcia blokuje sprzątanie wiersza zdjęcia, a zmiana
    zdjęcia to dwa zapisy w dwóch tabelach;
  - **C:** osobna tabela `cemetery_media`. Gotowa na kilka zdjęć cmentarza, których D28 nie chce; jedna tabela więcej w kopii i w
    liczeniu wierszy przy odtworzeniu.

  A **nie zastępuje** [[ADR-008-photos-access-copy-and-backup-consistency]] (rozszerza wzór nagrobka) — sygnał dla `architect` się
  nie zapala.
- **D2 — kiedy mapa jedzie (D30).** Bez arkusza Polska stoi na środku obszaru mapy, a zoom zostaje taki jak dziś (cała Polska
  mieści się też nad arkuszem — zoom nie skacze przy otwarciu). Otwarcie arkusza **przy całej Polsce** → płynne przesunięcie
  (ok. 300 ms) tak, że Polska stoi nad zmierzonym arkuszem; zamknięcie (dotknięcie mapy, przeciągnięcie, wstecz) → płynnie z
  powrotem na środek. **Przy przybliżonej mapie** zostaje dzisiejsza reguła: znicz nie stoi pod arkuszem, mapa nie wraca na
  środek. Ustawienie systemu „Usuń animacje” → przesunięcie bez ruchu. *Inaczej:* jazda także przy przybliżeniu (wtedy po
  zamknięciu arkusza mapa wraca tam, gdzie była).
- **D3 — zdjęcie cmentarza jak zdjęcie nagrobka:** zapis od razu, bez formularza; podgląd z tytułem = nazwa cmentarza i podtytułem
  „Zdjęcie cmentarza”, „Zmień zdjęcie”, „Usuń zdjęcie” → okno C1 bez zmian; po usunięciu arkusz z polem „Dodaj zdjęcie”; w czasie
  zapisu w miejscu pola wskaźnik, przy błędzie linia „Nie udało się zapisać zdjęcia. Spróbuj jeszcze raz.” pod wierszem nazwy (jak
  w [[grob]]). Ścieżka pliku `cmentarze/<id>/<czas>-<losowe>.jpg` — z `id`, nigdy z treści zdjęcia.
- **Decyzje projektowe ze specyfikacji** (do potwierdzenia tym samym „tak”): sąsiedzi w kolorze tła, Bałtyk i jeziora `water`
  `#101C25`, rzeki `waterLine` `#3A5E74` 1 dp, granica Polski w kolorze tekstu pomocniczego 1,4 dp, granice sąsiadów obrys 0,7 dp
  45%, „Polska” 22 sp półgruby, 11 miast z obwódką, bez faktury terenu (D29); miniatura 96 × 80 dp z lewej, ✎ w prawym górnym rogu
  (6a); arkusz grupy i karty wyszukiwarki **bez miniatur** (reguła 11; D28 → *obali*).
- *Obali „jedną pozycję”:* dane mapy (przycięcie, rozmiar, sklejenie warstw) zjadają sesję `dev` — wtedy zdjęcie cmentarza
  (schemat v9) jako ISSUE-027, a tu sama mapa i D30.

### Scope — files (`{code}`)
| Plik | Co |
|---|---|
| `tool/map/extract_poland.dart` | + **woda**: `ne_10m_ocean` przycięty do prostokąta (wyspy jako dziury — Bornholm) i jeziora z `ne_10m_lakes` + `ne_10m_lakes_europe` w tym prostokącie, bez drobin niewidocznych przy całej Polsce (próg pola — `dev` mierzy); + **granice sąsiadów**: `ne_10m_admin_0_boundary_lines_land` w prostokącie, uproszczone; + **11 miast** (Bydgoszcz, Katowice). Prostokąt danych większy niż wszystko, co kamera może pokazać (środek w granicach Polski, pół widoku dookoła przy najmniejszym zoomie) — **brzeg danych nigdy nie jest widoczny**. Tło mapy zostaje w kolorze tła = kolor sąsiadów, więc szczeliny między uproszczonymi granicami a pełnym konturem Polski nie wychodzą. **Żadnych nazw poza miastami.** Nagłówek: lista plików źródłowych. Budżet: `poland.json` ≤ 300 KB (dziś 37 KB); więcej → mocniejsze uproszczenie sąsiadów i oceanu |
| `assets/map/poland.json` | wygenerowany na nowo (klucze `water`, `lakes`, `borders` obok `outline`, `rivers`, `cities`) |
| `lib/app/home/poland_map_data.dart` | odczyt nowych kluczy (wielokąty z dziurami, linie) |
| `lib/app/home/poland_map.dart` | warstwy od dołu: woda → ląd Polski → jeziora → rzeki (`waterLine` 1 dp) → granice sąsiadów (obrys 0,7 dp, 45%) → granica Polski (tekst pomocniczy 1,4 dp) → „Polska” (stały punkt w wolnym miejscu północy, bez kolizji z podpisami) → miasta → znicze. Strony podpisów nowych miast (Katowice obok Krakowa — podpis nie może wejść na kropkę Krakowa). Bez zmian zachowania w podglądzie (14) i wskazaniu (16) |
| `lib/app/theme.dart` | `GrobingColors.water` `#101C25`, `GrobingColors.waterLine` `#3A5E74` — z komentarzem roli ([[style-b]] → woda: tylko mapa, dekoracja) |
| `lib/app/home/home_screen.dart` | **D30/D2:** środek bez arkusza; płynna jazda kamery (własna animacja `MapController.move` — flutter_map 8.3.2 nie ma ruchu animowanego) przy otwarciu i zamknięciu arkusza przy całej Polsce; `MediaQuery.disableAnimations` → bez ruchu; `_sheetRoom` = zmierzona wysokość arkusza z miniaturą. **6a:** wiersz: miniatura 96 × 80 dp (promień 12, przycięta ze środka) albo pole „Dodaj zdjęcie” → obok nazwa, miejscowość, liczby → ✎; dodanie (arkusz źródła → wybór → zapis), podgląd ze „Zmień” i „Usuń” (D3), stan zapisu i błędu |
| `lib/app/photo/add_photo_field.dart` (nowy) | `_AddPhotoField` z `grave_screen.dart` jako wspólny widżet: podpis, rozmiar i wielkość podpisu z parametrów (nagrobek: 120 dp, 16 sp; cmentarz: 96 × 80 dp, 12 sp półgruby), ta sama semantyka z `onTap` |
| `lib/app/grave/grave_screen.dart` | pole nagrobka przez wspólny widżet — bez zmian w wyglądzie |
| `lib/data/database.dart` | `Media.cemeteryId` — `integer().nullable().references(Cemeteries, #id)()`; komentarz tabeli; **schemat v9**, `_from8To9`: `addColumn` |
| `drift_schemas/grobing/drift_schema_v9.json`, `database.steps.dart`, `test/drift/grobing/generated/*` | `dart run drift_dev make-migrations` (README → *Baza danych*) |
| `lib/data/photos.dart` | `newCemeteryPhotoPath`, `cemeteryPhotoPath`, `setCemeteryPhoto`, `deleteCemeteryPhoto` — **jedna implementacja dla nagrobka i cmentarza** (właściciel jako parametr), żeby kolejność „plik przed wierszem” nie żyła w dwóch kopiach; **`applyPersonPhotoEdits`: sierota = bez grobu, bez cmentarza i bez łącza** |
| `lib/app/photo/photos.dart` | `setCemeteryPhoto`, `deleteCemeteryPhoto` (przygotowanie → warstwa danych, jak nagrobek) |
| `lib/data/cemeteries.dart` | `CemeterySummary.photoPath` (pierwszy wiersz `media` cmentarza według `id`); `watchCemeteries` czyta też `media` |
| `README.md` (`grobing-code`) | *Baza danych*: wpis v9; *Mapa*: pliki Natural Earth do pobrania (siedem zamiast trzech) |

Bez zmian: `restore_service.dart` (liczy wiersze — v9 ich nie dodaje), `backup_archive.dart` (bierze cały katalog `media/`, więc
`cmentarze/` wchodzi sam), `sweepOrphanMedia` (sierotą jest plik bez wiersza — wiersz cmentarza go chroni), arkusz grupy,
wyszukiwarka, [[cmentarz]].

### AC → implementation → test (testy pisze `qa`)
| AC | Gdzie | Test happy-path |
|---|---|---|
| AC-1 | `extract_poland.dart`, `poland.json`, `poland_map_data.dart`, `poland_map.dart`, `theme.dart` | danych (z zasobu, bez sieci): woda, jeziora, granice sąsiadów są; 11 miast z polskimi nazwami; w pliku nie ma innych nazw; brzeg danych poza zasięgiem kamery przy 360 i 411 dp; widżet: „Polska” i 11 podpisów na ekranie głównym; podpisy miast nie nachodzą na siebie przy całej Polsce (360 i 411 dp) |
| AC-2 | `home_screen.dart` | widżet: bez arkusza środek Polski w środku obszaru mapy; znicz → po animacji dół Polski nad arkuszem; dotknięcie mapy → znów środek; przy `disableAnimations` od razu; przybliżona mapa — znicz nad arkuszem, bez powrotu na środek (D2) |
| AC-3 | `home_screen.dart`, `add_photo_field.dart`, `photos.dart` (oba) | widżet: arkusz bez zdjęcia — „Dodaj zdjęcie” (przycisk z akcją dotknięcia dla czytnika) → atrapa galerii → miniatura w arkuszu; miniatura → podgląd „Zdjęcie cmentarza” → „Zmień zdjęcie” → nowa miniatura; „Usuń zdjęcie” → „Usuń” → arkusz z „Dodaj zdjęcie”; danych: plik przed wierszem, jedno zdjęcie na cmentarz, usunięcie zostawia plik do sprzątania; **„Zapisz” zdjęć osoby nie kasuje zdjęcia cmentarza**; sprzątanie nie rusza pliku cmentarza |
| AC-4 | `database.dart` (v9) | migracja v8→v9 na danych (`testWithDataIntegrity`): wiersze bez zmian, `cemetery_id` wszędzie puste; **odtworzenie kopii v8 w v9** — liczniki zgodne, cmentarze bez zdjęć; kopia v9 ze zdjęciem cmentarza → odtworzenie → zdjęcie jest, odcisk zgodny |

Testy do przepisania: `database_test.dart` i `data_state_screen_test.dart` (wersja 8 → 9), `poland_map_data_test.dart` (9 → 11
miast, nowe klucze), `home_screen_test.dart` (położenie mapy przy starcie, jeśli je sprawdza).

### Data layer
- **Schemat v9** (D1) z testem migracji v8→v9 na danych (NFR-003) i plikiem schematu z `make-migrations`.
- **Próbne odtworzenie:** testy kopii v8 → v9 i kopii v9 ze zdjęciem cmentarza; na emulatorze kopia z `Medium_Phone` z nowym
  hasłem testowym → `Grobing_Restore` (agent).
- **Źródło i status faktu:** ta pozycja **nie zapisuje faktów o rodzinie** — zdjęcie cmentarza to zdjęcie miejsca, bez twierdzenia
  (jak nagrobek).
- **Dane rodziny:** zdjęcia w testach i na emulatorze tylko wymyślone (`photo_fakes.dart`, `wymyslone-*.jpg`); mapa ma wyłącznie
  dane publiczne Natural Earth.
- **ADR-014** (D1) i wpis v9 w [[data-model]] → `docs` przy zamknięciu.

### Manual verification
**Agent na emulatorze** (`Medium_Phone`, build release jako aktualizacja na danych testowych v8), zrzuty przed stopem #2:
1. Po aktualizacji: dane całe, `user_version` 9, `media.cemetery_id` wszędzie puste.
2. Tryb samolotowy → start: sąsiedzi, Bałtyk, jeziora, rzeki w kolorze wody, „Polska”, 11 miast; Katowice i Kraków czytelne;
   największe przybliżenie i przeciąganie do każdej krawędzi — nigdzie brzegu danych (morza tam, gdzie go nie ma).
3. Znicz → arkusz: mapa jedzie płynnie, Polska nad arkuszem; zamknięcie dotknięciem, przeciągnięciem i wstecz → z powrotem na
   środku; przy przybliżeniu znicz nad arkuszem; „Usuń animacje” w systemie → bez ruchu.
4. „Dodaj zdjęcie” → galeria (wymyślony obraz) → miniatura; podgląd → „Zmień zdjęcie” → „Usuń zdjęcie” → okno → arkusz z „Dodaj
   zdjęcie”; potem „Zapisz” przy zdjęciach osoby w innym grobie → zdjęcie cmentarza dalej w bazie i w arkuszu.
5. `uiautomator`: „Dodaj zdjęcie” i miniatura `clickable` z opisem; **tekst 200%** — arkusz bez ucięć, podpisy miast i „Polska”
   bez kolizji; **ekran 360 × 640 dp** (`wm size` + `wm density`) — Polska nad arkuszem z miniaturą ([[cmentarze]] D26 → *obali*).
6. Próbne odtworzenie na `Grobing_Restore`: odcisk zgodny, zdjęcie cmentarza w arkuszu.

**Autor: odczucie** (najwyżej 3):
1. Otwórz aplikację: czy mapa wygląda jak R1 (sąsiedzi, morze, jeziora) i czy Polska stoi na środku.
2. Otwórz i zamknij kilka razy arkusz cmentarza: czy jazda mapy jest płynna i nie męczy.
3. Dodaj cmentarzowi zdjęcie (dowolny wymyślony obraz z galerii): czy miniatura w arkuszu wygląda dobrze, a droga dodaj → podgląd →
   zmień albo usuń jest jasna.

Przegląd ekranów `ui` (subagent `qa`) przed stopem #2; zmieniony ekran → `dev` przechodzi AC na emulatorze przed `qa` (retro 2, R5),
**z tekstem 200%** (kandydat z ISSUE-024 w *Do retro*).

### Out of Scope
- **Faktura terenu** z R1 (lasy, rzeźba) — D29; wariant C, gdy po zbudowaniu jej brakuje.
- Zdjęcie cmentarza na ekranie [[cmentarz]], w arkuszu grupy i w kartach wyszukiwarki (reguła 11; D28 → *obali*); kilka zdjęć
  cmentarza (D28: jedno).
- Mapa cmentarza — plan offline, ortofotomapa, kwatery → [[US-007-mapa-cmentarza]].
- Eksport zdjęcia cmentarza → [[US-006-eksport-dla-rodziny]].
- Odświeżenie bazy cmentarzy OSM (wyjątek strażnika — osobna decyzja), twarde spacje (reguła 6), „Stan danych” B6 — osobne pozycje.

## Dev report
> `dev`, 2026-10-12. Flutter 3.41.1 (przypięty). `flutter analyze` czyste, `dart format` bez zmian. Testów nie ruszałem
> (`qa`) — poza wygenerowanymi przez `make-migrations` (`test/drift/grobing/generated/schema.dart`, `schema_v9.dart`).

### What was built (`{code}`)
- **Mapa jak R1** — `tool/map/extract_poland.dart` czyta siedem plików Natural Earth: morze (ocean przycięty
  Sutherlandem–Hodgmanem do prostokąta 7–31,5° E × 42,5–60° N, wyspy jako dziury), jeziora (w Polsce od 8 km², za granicą od
  40 km²), granice sąsiadów (bez granic Polski), 11 miast. Upraszczanie Douglasem–Peuckerem zależne od miejsca: ok. 50 m przy
  Polsce, ok. 600 m dalej; kontur Polski bez uproszczenia. **`poland.json`: 281 KB** (budżet 300 KB; pierwsza wersja z
  prostokątem 2–38° × 40–63° i stałą tolerancją miała 1 MB). Nazwy w pliku: tylko 11 miast.
- `poland_map.dart`: warstwy woda → ląd Polski → jeziora → rzeki (`waterLine` 1 dp) i granice sąsiadów (obrys 0,7 dp, 45%) →
  granica Polski (tekst pomocniczy 1,4 dp) → „Polska” → miasta → znicze. Katowice z podpisem po lewej. Tokeny `water`, `waterLine`
  w `theme.dart`. Podgląd z bazy (14) i tryb wskazania (16) dostały nowy wygląd z tego samego widżetu.
- **D30/D2** — `home_screen.dart`: zapas na arkusz rozdzielony góra/dół (ten sam zoom, Polska na środku bez arkusza); przy
  całej Polsce otwarcie arkusza → jazda ok. 300 ms (`AnimationController`, `easeOutCubic`) do pozycji „dół Polski 16 dp nad
  zmierzonym arkuszem” (albo „góra 16 dp pod wyszukiwarką”, gdy Polska się nie mieści), zamknięcie (dotknięcie mapy,
  przeciągnięcie, wstecz) → na środek. Przy przybliżeniu — dawna reguła znicza. „Usuń animacje” → skok. Palec na mapie
  zatrzymuje jazdę.
- **6a** — miniatura 96 × 80 (promień 12, ze środka) albo „Dodaj zdjęcie” z lewej, nazwa/miejscowość/liczby obok, ✎ w rogu;
  arkusz źródła „Zdjęcie cmentarza”, zapis od razu, podgląd „Zdjęcie cmentarza” ze „Zmień” i „Usuń” (okno C1), stan zapisu
  (wskaźnik w miejscu pola) i linia błędu. Wspólne pole `lib/app/photo/add_photo_field.dart` — nagrobek używa go bez zmiany
  wyglądu.
- **Schemat v9** (D1 = A): `media.cemetery_id`, `_from8To9` = `addColumn`; `drift_schema_v9.json`, kroki i schematy testowe z
  `make-migrations`. `photos.dart`: jedna implementacja zdjęcia miejsca (`_Place.grave` / `_Place.cemetery`) —
  `setCemeteryPhoto`, `deleteCemeteryPhoto`, `cemeteryPhotoPath`, ścieżki `cmentarze/<id>/…`; **sierota w
  `applyPersonPhotoEdits` = bez grobu, bez cmentarza i bez łącza**. `watchCemeteries` daje `photoPath` i czyta `media`.
- README `grobing-code`: *Baza danych* (v9, pułapka sieroty), *Mapa* (siedem plików, prostokąt, tło = kolor sąsiadów, jazda
  mapy i jak ją sprawdzać na emulatorze).

### Deviations (do przeglądu `ui`)
1. **Podpisy mapy rosną z tekstem systemu najwyżej do 1,3×** („Polska” i miasta; miasto przy 200% = 17 sp), a wysokość
   znacznika rośnie z nimi. Przy 200% podpisy były ucięte w pionie (stała wysokość 24 dp — **od ISSUE-014**) i „Bydgoszcz”
   wchodziła na „Białystok” (nowe). Specyfikacja nie mówi, czy podpis mapy skaluje się z tekstem.
2. **„Polska” znika powyżej +2 kroków przybliżenia** (nazwa kraju należy do najmniejszych przybliżeń); stoi w punkcie
   53,85° N, 21,0° E (Mazury, między podpisami Gdańska, Bydgoszczy, Warszawy i Białegostoku).
3. Brzegi sąsiadów bez linii — wodę od lądu sąsiada odróżnia sam odcień (dekoracja; brzeg Polski niesie jej granica).
4. Progi jezior: 8 km² w Polsce, 40 km² za granicą (drobiny przy całej Polsce poniżej 2 dp).
5. Stan zapisu w 6a: sam wskaźnik, bez „Zapisuję zdjęcie…” (nie ma miejsca w 96 × 80); tekst słyszy czytnik.
6. Kolumna nazwy obok miniatury zaczyna się 2 dp od góry (bez miniatury jak dotąd: 12 dp, w linii z ✎).
7. **Zapas na arkusz 150 → 214 dp** (zmierzony arkusz z miniaturą, plan). Na telefonach 20:9 i dłuższych bez zmiany (zoom
   wyznacza szerokość — sprawdzone na 411 × 914 i 360 × 780); na 360 × 640 Polska maleje do ok. 145 dp szerokości (Deviation →
   *Found on the emulator* 4).

### Found on the emulator (AC przed `qa`, R5) — `Medium_Phone`, build release jako aktualizacja na danych testowych v8
1. **„Dodaj zdjęcie” nie było osobnym przyciskiem dla czytnika** — `Semantics` bez `container` zlał etykietę i akcję z całym
   arkuszem (`uiautomator`: jeden węzeł „Dodaj zdjęcie / Cmentarz Powązkowski / …” na cały arkusz). W grobie to nie wychodziło,
   bo lista daje każdemu elementowi własny węzeł. Poprawione: `container: true` we wspólnym polu, w miniaturze i w stanie zapisu;
   po poprawce „Dodaj zdjęcie” i „Zdjęcie cmentarza — otwórz” to osobne węzły `clickable`. **Czwarta instancja tej rodziny błędów
   semantyki** (*Do retro*: ISSUE-017 + dwa ekrany ISSUE-021).
2. **Tekst 200%:** podpisy miast ucięte i nachodzące — poprawione (Deviation 1); zrzut po poprawce: całe, bez kolizji. Arkusz
   przy 200%: pole „Dodaj zdjęcie” rośnie w dwie linie, nic nie ucięte.
3. **Jazda mapy:** na zrzutach z emulatora (okno w tle) mapa stawała w pół drogi, a po zamknięciu potrafiła pokazać poprzednią
   pozycję. Sprawdzone, że to klatki, nie logika: (a) z „Usuń animacje” pozycje dokładne — otwarcie podnosi Polskę o 206 px
   (78 dp, jej południe 16 dp nad arkuszem), zamknięcie wraca co do piksela; (b) z animacją pozycja końcowa dochodzi (zrzut po
   ok. 1,5–4 s); (c) jednorazowy test widżetu (skasowany, nie w repo) — środek kamery przechodzi płynnie do celu w 300 ms.
   **Płynność ocenia oko autora** (krok odczucia 2).
   **⚠️ Ten wniosek był błędny** (sprostowane przez `qa`, 2026-10-12 — *After `qa` and the `ui` review*, pkt 1): to nie emulator,
   tylko koszt rysowania morza, 2–3 s na klatkę. Logika jazdy była dobra, ale klatek nie było.
4. **360 × 640 dp** (`wm size 720x1280`, `wm density 320`): arkusz zajmuje ok. 60% wysokości mapy, Polska ok. 145 dp szerokości
   i nie mieści się nad arkuszem (działa reguła znicza); podpisy nachodzą (Bydgoszcz–Białystok, „Polska” na Gdańsku).
   **Falsyfikator [[cmentarze]] D26 („arkusz zasłania południe Polski na małym telefonie”) się zapalił** — decyzja `ui`.
   360 × 780 dp: bez problemu (Polska na całą szerokość, znicz nad arkuszem).
5. AC-3 na urządzeniu: dodanie z galerii (wymyślony obraz) → miniatura; podgląd → „Zmień zdjęcie” → nowa; „Usuń zdjęcie” → okno
   C1 → arkusz z „Dodaj zdjęcie”. **Pułapka sieroty sprawdzona:** zdjęcie w tle dla Kuby Testowego (droga
   `writeWithPersonPhotos` → `applyPersonPhotoEdits`) — zdjęcie cmentarza dalej w arkuszu.
6. „Stan danych”: wersja schematu 9; kopia w tle po aktualizacji udana (08:17).
7. Poza zakresem, z ISSUE-024: w „Zdjęcie w tle” (osoba bez zdjęć) węzeł „Dodaj zdjęcie osoby” ma granice na całą szerokość, a
   kafelek ok. 1/3 — dotknięcie w środku węzła trafia obok kafelka. Switch Access używa akcji, więc działa; ramka TalkBack jest za
   szeroka. Do notatek przeglądu `ui`.

### For `qa` — kroki ręczne
Plan → *Manual verification*. Zrobione przez `dev` (zrzuty w katalogu tymczasowym sesji, `shots/`): krok 2 (bez trybu
samolotowego — mapa nie ma sieci w ogóle), 3 (pozycje; płynność — autor), 4 i 5. Zostaje dla `qa`: krok 1 (wiersze — przez
odcisk, build release nie pozwala czytać bazy), 6 (próbne odtworzenie na `Grobing_Restore`), suchy przebieg strażnika na paczce.
Stan `Medium_Phone`: Powązki **bez** zdjęcia cmentarza (dodane, zmienione, usunięte — pliki pójdą przy sprzątaniu); Kuba Testowy ma
wymyślone zdjęcie profilowe i w tle (z kroku 5); tekst 100%, ekran 1080 × 2400, animacje włączone.

### After `qa` and the `ui` review (`dev`, 2026-10-12)
Poprawki po błędach z testów `qa`, po pomiarze `qa` i po przeglądzie `ui` (2 MAJOR, 3 MINOR — wszystkie przyjęte):
1. **Wydajność morza (znalazł `qa`, pomiar).** ANR przy zimnym starcie na `Grobing_Restore` („Input dispatching timed out”, główny
   wątek w kodzie aplikacji — od Fluttera 3.29 Dart działa na głównym wątku Androida). Jednorazowy test kosztu (skasowany) na tym
   samym ekranie: stara mapa — 60 ruchów 0,33 s; nowa — 60 ruchów **213 s**, pierwsza klatka 7,8 s. Rozbicie na warstwy: winne samo
   morze (jeziora i granice po kilkadziesiąt ms). Przyczyna: `flutter_map` domyślnie wycina dziury (wyspy) przez `Path.combine` przy
   każdej klatce. **Poprawka:** `painterFillMethod: PolygonPainterFillMethod.evenOdd` dla wody i jezior — wyspy się nie przecinają,
   rysunek ten sam. Po poprawce: 60 ruchów 0,42 s (jak stara mapa); na emulatorze zimny start 2,3 s, bez ANR, czas procesora
   aplikacji 2,45 s (wcześniej 19 s), jazda kończy się przed 0,4 s. README → *Mapa* (pułapka), test ekranu pilnuje `evenOdd`.
2. **Kontroler jazdy w `initState`** (znalazł `qa` w testach): leniwy `AnimationController` powstawał w `dispose()`, gdy ekran
   zamknięto przed wczytaniem mapy (8 testów padało na „deactivated widget's ancestor”).
3. **Prostokąt danych `[3, 40, 35, 62]`** (znalazł test `qa`): na 411 dp południe widoku sięgało dokładnie 42,5°, a na 360 × 640 zachód
   wychodził poza 7°. Trzy progi uproszczenia (ok. 50 m przy Polsce, 600 m do 3,5° wokół, 2 km dalej) i jeziora daleko od 150 km²:
   **`poland.json` 298 KB** (budżet 300 KB; sam większy prostokąt dawał 462 KB).
4. **MAJOR 2 `ui`:** arkusz i karta pustego stanu nie dodają już marginesu paska gestów (liczony podwójnie od ISSUE-022); arkusz z
   miniaturą ma ok. 190 dp (było 214).
5. **MAJOR 1 `ui` (D26 v2.6):** najmniejsze przybliżenie = Polska na całą szerokość, 16 dp marginesu, na środku
   (`EdgeInsets.all(16)`) — formuła `min(zapas, luz pod Polską)` z D26 v2.6 nigdy nie zmienia tego przybliżenia, więc jest mu
   równoważna. Na 360 × 640 Polska ma ok. 328 dp szerokości (było ok. 145), a otwarty arkusz zasłania południe (reguła znicza).
6. **MINOR 3–5 `ui`:** ✎ w linii nazwy obok miniatury (`Transform.translate`, cel 48 × 48 bez zmian); miniatura dekodowana
   `coverDecodeWidth` (ostra przy zdjęciu poziomym); `PhotoErrorLine` ogłaszana przez czytnik (`liveRegion`) — także w grobie.
7. **Follow-up `ui` (p07):** podpis Białegostoku pod kropką — przy 360 dp i tekście 200% stał spację od „Bydgoszcz” w jednej linii
   i czytał się jak jeden napis ([[cmentarze]] D32).

## Verification
> `qa`, 2026-10-12. Rytuał WZ-024: `dart format` bez zmian · `flutter analyze` czyste · `flutter test` — **579 zielonych** (przed
> pozycją 544). Werdykt po stopie #2.

### Tests (happy path per AC)
| AC | Test |
|---|---|
| AC-1 | `poland_map_data_test.dart`: 11 miast z polskimi nazwami; morze (Zatoka Gdańska, okolice Kołobrzegu — woda; Warszawa, Berlin, Bornholm — nie); jeziora (zamknięte pierścienie, część w Polsce); granice sąsiadów bez granicy Polski; **w pliku tylko nazwy 11 miast i linia źródła**; plik < 300 KB; prostokąt morza większy niż Polska. `map_r1_and_cemetery_photo_test.dart`: kolejność i kolory warstw (woda, ląd, jeziora, rzeki `waterLine` 1 dp, granice sąsiadów obrys 45% 0,7 dp, granica Polski tekst pomocniczy 1,4 dp), **`evenOdd` dla wody i jezior**, „Polska” i 11 podpisów; podpisy mapy rosną do 1,3× przy tekście 200%, a tekst obok w pełni; **brzeg danych poza widokiem** w każdym rogu Polski na 411 × 914, 360 × 780 i 360 × 640 dp; **Polska na całą szerokość, na środku** na tych trzech ekranach |
| AC-2 | jazda (nie skok): w 100 ms pozycja pośrednia, po 400 ms dół Polski 16 dp nad arkuszem; dotknięcie mapy → środek co do 1e-6°; „Usuń animacje” → od razu; przy przybliżeniu znicz nad arkuszem, zamknięcie zostawia mapę |
| AC-3 | ekran: „Dodaj zdjęcie” to **osobny** węzeł-przycisk z akcją dotknięcia, z lewej od nazwy → arkusz „Zdjęcie cmentarza” → miniatura 96 × 80 → podgląd → „Zmień zdjęcie” → „Usuń zdjęcie” → okno → pole wraca, w bazie brak, pliki czekają na sprzątanie. Dane (`photos_test.dart`): plik przed wierszem w `cmentarze/<id>/`, jedno zdjęcie na cmentarz, usunięcie zdejmuje wiersz, sprzątanie zostawia plik cmentarza, strumień arkusza widzi zmianę, ścieżka bez treści zdjęcia. **Pułapka sieroty** (`person_photos_test.dart`): „Zapisz” zdjęć osoby zostawia zdjęcie cmentarza — test sprawdzony mutacją (bez warunku `cemetery_id` pada) |
| AC-4 | `migration_test.dart`: v8 → v9 na danych (cmentarze, grób z nagrobkiem, osoba z tłem) — wiersze bez zmian, `cemetery_id` puste, zdjęcie cmentarza zapisuje się po migracji, klucze całe; migracje bez danych 1…9. `restore_service_test.dart`: **kopia v8 → v9** (liczniki, nagrobek, tło, pliki; cmentarze bez zdjęć) i **kopia v9 ze zdjęciem cmentarza** (odcisk zgodny, wiersz i plik) |

Przepisane (zachowanie zmienione tą pozycją): wersja 8 → 9 (`database_test`, `data_state_test`, `data_state_screen_test`), 9 → 11
miast, warstwa lądu wśród trzech (`home_screen_test` AC-1 ISSUE-014).

### Agent na emulatorze (przed stopem #2)
Zrzuty w katalogu tymczasowym sesji (`review/`), poza repo.
1. **Aktualizacja** na danych testowych v8 (`Medium_Phone`, build release): „Stan danych” — wersja schematu 9, liczby całe; kopia w tle
   po aktualizacji udana.
2. **Mapa:** sąsiedzi, Bałtyk, jeziora, rzeki w kolorze wody, „Polska”, 11 miast; Katowice i Kraków osobno; przy przybliżeniu 2×
   Mazury i Zatoka Gdańska; na 360 × 640 przeciąganie do krawędzi — brzegu danych nie widać.
3. **Jazda mapy:** otwarcie przy całej Polsce — dół Polski ok. 16 dp nad arkuszem, koniec przed 0,4 s; zamknięcie — środek co do
   piksela; „Usuń animacje” — od razu.
4. **Zdjęcie cmentarza:** dodanie z galerii (wymyślony obraz), podgląd, „Zmień”, „Usuń” → okno → pole; po „Zapisz” zdjęć osoby
   zdjęcie cmentarza zostaje.
5. **Dostępność i ekrany:** „Dodaj zdjęcie” i miniatura to osobne węzły `clickable` z opisem (po poprawce); tekst 200% (411 i 360 dp)
   — arkusz bez ucięć, podpisy mapy całe i osobno; 360 × 640 i 360 × 780 — Polska na całą szerokość.
6. **Próbne odtworzenie:** kopia skonfigurowana od nowa na `Medium_Phone` (hasło testowe, do Pobranych: `grobing-klucz-023.age`,
   `grobing-kopia-023.age`, wymyślone dane) → `Grobing_Restore` (aktualizacja v8 → v9, potem odtworzenie): **odcisk
   `12aa563905347598` zgodny z kopią**, schemat 9, liczby te same, zdjęcie cmentarza w arkuszu.
7. **Wydajność** (znalezione tutaj, *After `qa`* pkt 1): ANR przy zimnym starcie → pomiar → `evenOdd`; po poprawce zimny start
   2,3 s, bez ANR.

### `ui` review (subagent, bez historii)
Runda 1 (r01–r14): 0 BLOCKER, **2 MAJOR** (zapas na arkusz zmniejszał Polskę na krótkich ekranach — D26; margines paska gestów
liczony dwa razy), **3 MINOR** (✎ poza linią nazwy, rozmyta miniatura, błąd zapisu nieogłaszany czytnikowi). Odstępstwa `dev` 1–6
przyjęte, 7 do poprawki. Runda 2 (p01–p07): wszystkie zamknięte; jedna poprawka podpisu (Białystok pod kropką), sprawdzona na
p07b i p01b. Specyfikacje zaktualizowane przez `ui`: [[cmentarze]] v2.6 (D26 nowa reguła, D30 jak zbudowano, D32 podpisy i
szczegóły R1, D33 arkusz z miniaturą, *States*, *AC → element*), [[style-b]] v1.20 (wyjątek SC 1.4.4 dla podpisów mapy, reguła
13), [[zdjecie]] v1.6 (tryb cmentarza).

### Family data
Zmiany bez danych rodziny: mapa to publiczne dane Natural Earth (nazwy tylko 11 miast; suchy przebieg strażnika na nazwach przed
planem i na całej paczce kodu — przechodzi); zdjęcia w testach rysowane w kodzie, na emulatorze — wymyślone obrazy; cmentarz w
danych testowych to publiczny cmentarz z bazy OSM.

### Not covered (named)
- **Wydajność na słabym telefonie** — zmierzona tylko względnie (test kosztu: nowa mapa jak stara) i na emulatorze; pierwszy
  prawdziwy telefon przy instalacji MVP.
- TalkBack na żywo w arkuszu (ogłoszenie błędu zapisu, kolejność czytania) — sprawdzone tylko drzewem dostępności i testem.
- Poziomo trzymany telefon: prostokąt danych liczony dla pionu (README → *Mapa*).
- Czy jeziora są widoczne przy całej Polsce (woda i ląd 1,00:1) — pytanie w kroku odczucia 1 (`ui`, D32 → *obali*).

### Stop #2 (2026-10-12) — autor: „ok”
Trzy kroki odczucia (mapa jak R1 i jeziora · jazda mapy · zdjęcie cmentarza): **„ok”**. Sprawdzone na urządzeniu (`Medium_Phone`):
w arkuszu Powązek stoi inne wymyślone zdjęcie niż zostawione przez agenta (usunięte i dodane na nowo), arkusz otwarty po kroku 2;
w logcat żadnego ANR od wgrania buildu z poprawką wydajności (wcześniejsze — 09:13–09:14, build sprzed poprawki).

### Verdict
**APPROVED** (self-check, 2026-10-12, z uwagami: *Not covered* — wydajność na słabym telefonie, TalkBack na żywo, układ poziomy).
Każde AC ma test happy-path; warstwa danych: migracja v8 → v9 z testem, odtworzenie kopii v8 i v9 (testy) i próbne odtworzenie na
drugim emulatorze z odciskiem zgodnym; zero danych rodziny w zmianach (suchy przebieg strażnika na kodzie i vaulcie).
Szukane i nieznalezione: utrata zdjęcia cmentarza przy zapisie zdjęć osoby (test z mutacją), sierota pliku po zmianie (D3 — plik czeka
na sprzątanie, wiersz nie), brzeg danych na ekranie (3 rozmiary), regres zdjęcia nagrobka po wydzieleniu `AddPhotoField` (testy
ISSUE-016 zielone), ANR po poprawce.

### Package for `docs` (lista jawna, R1)
**`grobing-code`** (29): `README.md` · `assets/map/poland.json` · `tool/map/extract_poland.dart` · `lib/app/theme.dart` ·
`lib/app/home/home_screen.dart` · `lib/app/home/poland_map.dart` · `lib/app/home/poland_map_data.dart` ·
`lib/app/grave/grave_screen.dart` · `lib/app/photo/add_photo_field.dart` (nowy) · `lib/app/photo/photos.dart` ·
`lib/app/photo/photo_viewer_screen.dart` · `lib/data/cemeteries.dart` · `lib/data/database.dart` · `lib/data/database.g.dart` ·
`lib/data/database.steps.dart` · `lib/data/photos.dart` · `drift_schemas/grobing/drift_schema_v9.json` (nowy) ·
`test/drift/grobing/generated/schema.dart` · `test/drift/grobing/generated/schema_v9.dart` (nowy) ·
`test/drift/grobing/migration_test.dart` · `test/app/home/map_r1_and_cemetery_photo_test.dart` (nowy) ·
`test/app/home/poland_map_data_test.dart` · `test/app/home/home_screen_test.dart` · `test/app/data_state_screen_test.dart` ·
`test/backup/restore_service_test.dart` · `test/data/data_state_test.dart` · `test/data/database_test.dart` ·
`test/data/person_photos_test.dart` · `test/data/photos_test.dart`.

**`grobing-vault`** (przed zamknięciem `docs`): `backlog/issues/ISSUE-023-poland-map-r1-cemetery-photo.md` ·
`00_START_HERE/TRACEABILITY.md` · `05_DESIGN/cmentarze.md` · `05_DESIGN/brand/style-b.md` · `05_DESIGN/zdjecie.md` — plus to, co
dopisze `docs` (ADR-014, [[data-model]] v9, `CURRENT_STATE.md`, DOC_MAP jeśli dotyczy).

**`grobing-agents`:** nic.

### Do retro (zebrane w tej pozycji)
- **`dev` przypisał wolne klatki emulatorowi** (*Found on the emulator* 3), choć był to błąd wydajności 600×; złapał go dopiero ANR i
  pomiar `qa`. Kandydat: przy nowej warstwie mapy albo dużych danych — test kosztu (stara vs nowa) w przejściu AC, zanim padnie
  słowo „emulator”.
- **`python -` (skrypt z wejścia) jeszcze raz** — `qa` w tej pozycji, mimo pamięci „nigdy”; zawisło, zatrzymane, bez szkody.
  Trzecia sesja z rzędu — za hookiem `PreToolUse` z *Do retro*.
- **Czwarta instancja błędu semantyki** (`Semantics` bez `container` zlał się z arkuszem) — za punktem „semantyka” w przejściu AC.
- Skill `ui` w trybie przeglądu mówi „nic nie zapisujesz”, a przegląd zapisuje przyjęte odstępstwa w specyfikacji (tu i wcześniej)
  — wyrównać skill z praktyką.
