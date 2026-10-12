---
title: "ISSUE-027 — Cemetery as a map: OSM schematic plan downloaded on add and kept offline, GUGiK orthophoto online, three screen states (map · one grave · list), INTERNET permission"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-002-wizyta]]"
user-story: "[[US-007-mapa-cmentarza]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-12
verdict-reviewer: self-check
source: "rozpisanie US-007 (`docs` w auto-flow po `pm`, autor: „tak”, 2026-10-12) · US-007 AC-1, AC-2, AC-3, AC-5 · [[ADR-003-map-source-offline]] pkt 1, 2, 4 i *Follow-ups* · [[cmentarz]] v5 (stany A, B, C, element 2a; D10–D23) · [[SPIKE-004-mvp-flow-prototype]] D8–D12"
created: 2026-10-12
updated: 2026-10-12
---

# ISSUE-027 — Mapa cmentarza: plan, zdjęcie z góry, trzy stany

> Z rozpisania [[US-007-mapa-cmentarza]] (`docs` w auto-flow, 2026-10-12, po `pm`). **Dwie pozycje:** ta buduje
> ekran cmentarza jako mapę, a [[ISSUE-028-cemetery-sectors]] dokłada kwatery autora (AC-4), bo ich zaznaczanie
> trzeba dopiero zaprojektować. Podział zaproponował łańcuch, nie autor, więc na stopie #1 autor może go zmienić.

## What to build
1. **Plan schematyczny offline** ([[ADR-003-map-source-offline]] pkt 1): obrys cmentarza i alejki z OSM, pobrane
   **przy dodaniu cmentarza** i zapisane w telefonie, w tokenach stylu B, z podpisem „© OpenStreetMap”.
   - Pobieranie z ponawianiem, bo publiczny Overpass był w SPIKE-001 zawodny (M11). Ponawianie i zaślepka są
     warunkiem ADR-003.
   - **Zaślepka bez planu** (AC-5): „Plan tego cmentarza pobierze się, gdy będzie internet.” i „Pobierz teraz”.
     Dotyczy też cmentarzy dodanych przed tą pozycją, bo żaden z nich nie ma planu.
2. **Zdjęcie z góry tylko online** (pkt 2): przełącznik **Plan · Zdjęcie**, ortofotomapa GUGiK (WMTS
   `StandardResolution`, EPSG:3857, do z19), podpis „Ortofotomapa: GUGiK”, nic nie zapisuje się w telefonie. Bez
   sieci: „bez internetu”, a plan działa ([[cmentarz]] element 13).
3. **Ekran cmentarza w trzech stanach** ([[cmentarz]] v4.1):
   - **A, mapa:** plan i pasek grobów z liczbą grobów bez pinezki i z „Dodaj grób”;
   - **B, jeden grób:** znicz otwiera arkusz grobu z „Pokaż grób”;
   - **C, lista:** wszystkie groby po przeciągnięciu, bez mapy.
   Dzisiejszy ekran (lista z ISSUE-012/016) to stan C.
4. **Znicze grobów z pinezką** z kolumn `lat`/`lon` grobu (są w schemacie od v1, razem z `positionSource` i
   `positionAccuracyM`).
5. **Uprawnienie `INTERNET`** (pkt 4) wyłącznie do pobrania planu i do zdjęcia z góry. Dziś manifest mówi wprost, że
   wydanie go nie ma. Od tej pozycji [[NFR-005-dane-nie-opuszczaja-telefonu]] pilnuje kod, a nie system.

## Acceptance Criteria
- [ ] **US-007 AC-1 — plan offline.** *Given* cmentarz dodany z siecią *When* otwieram go w trybie samolotowym
      *Then* widzę plan schematyczny (obrys, alejki z OSM) z „Plan offline” i „© OpenStreetMap”.
- [ ] **US-007 AC-2 — zdjęcie z góry online.** *When* przełączam na „Zdjęcie” z siecią *Then* widzę ortofotomapę
      GUGiK; bez sieci „bez internetu”, a plan działa; nic nie zapisuje się w telefonie.
- [ ] **US-007 AC-3 — sama mapa, jeden grób, lista.** *Given* groby z pinezką i bez *Then* na starcie jest sama mapa
      i pasek grobów z liczbą grobów bez pinezki; znicz → arkusz grobu z „Pokaż grób”; przeciągnięcie → lista
      wszystkich grobów.
- [ ] **US-007 AC-5 — bez planu.** *Given* cmentarz dodany bez sieci *Then* jest zaślepka „pobierze się, gdy będzie
      internet” i „Pobierz teraz”, a lista grobów działa.

## Out of scope
- Kwatery autora: zaznaczanie i rysowanie stref (US-007 AC-4) → [[ISSUE-028-cemetery-sectors]].
- Stawianie i poprawianie pinezki, „gdzie jestem”, stan D → [[US-008-pinezka-na-miejscu]]. Pinezki do sprawdzenia
  AC-3 pochodzą z danych testowych.
- Link do Grobonetu i pole „link do wyszukiwarki zarządcy”: wycofane ([[cmentarz]] D12, SPIKE-004 D10). To zamyka
  ten punkt w ADR-003 → *Follow-ups*.

## Notes
- **Do rozstrzygnięcia przed planem albo w planie:**
  - **gdzie leży plan** (baza czy plik) i **czy wchodzi do kopii**. To dane publiczne, które da się pobrać ponownie,
    ale po odtworzeniu na nowym telefonie bez sieci planu by nie było ([[NFR-002-odtworzenie-na-nowym-telefonie]]).
    To kandydat na ADR;
  - **pobieranie przy dodaniu cmentarza** zmienia przepływ z [[ISSUE-015-add-cemetery-from-database]] ([[cmentarze]]).
    Trzeba ustalić, co widać, gdy pobieranie trwa albo się nie udaje (`ui`);
  - **[[NFR-004-czytelnosc-w-sloncu]]:** [[cmentarz]] D8 przesunęło miarę na „pierwszy ekran wizyty: mapę cmentarza
    z pinezkami”, a US-008 ma NFR-004 na liście. Trzeba ustalić, czy miara zapada tutaj, czy w US-008 (`ui`).
- **Wejście z widoku osoby** ([[cmentarz]] v4.3): „Pochówek” otwiera grób z pinezką w stanie B, a grób bez pinezki w
  stanie C z komunikatem ([[osoba]] D9). Ta pozycja zastępuje rozwiązanie „do czasu mapy” ([[osoba]] D17).
- **Prior art w repo:**
  - `flutter_map` 8.3.2 już jest (SPIKE-001, mapa Polski);
  - pułapka `CameraConstraint.contain` przy ramce mniejszej od ekranu ([[ADR-003-map-source-offline]] *Follow-ups*,
    M7);
  - płynne przesunięcie mapy nad arkusz jak [[cmentarze]] D30 (ISSUE-023).
- **Koszt rysowania:** w ISSUE-023 morze rysowane co klatkę dało ANR, a winę zrzucono najpierw na emulator. Przy nowej
  warstwie mapy pomiar czasu klatki należy do przejścia AC.
- **Prywatność:** zapytania o plan i o zdjęcie mówią serwerom OSM i GUGiK, którym obszarem interesuje się telefon
  (adres IP) — znany koszt z ADR-003 → *Consequences*.

## Implementation plan
> `planning`, 2026-10-12. Specyfikacja (`ui`, przed planem): [[cmentarz]] v5 — stany A, B, C, element 2a (zaślepki planu), D17–D23,
> *Open*; [[cmentarze]] v2.7 (D34); [[osoba]] D17 v2.4; [[style-b]] v1.20 (reguły 7, 13, 14). Makieta stanów i wariantów:
> `issue-027-mapa-cmentarza.html` (katalog tymczasowy sesji `1d9348ed-…`). Stany A, B, C autor widział i przyjął na prototypie
> [[SPIKE-004-mvp-flow-prototype]] (panel 2). **Kandydaci tego, co widać** (retro 2, R6): W1 i W2 na makiecie (D1).

### Prior art
- **Pomiar przed planem** (2026-10-12, zapytania z PC o publiczny cmentarz testowy z danych testowych):
  - obrys (`landuse=cemetery`, `amenity=grave_yard`, `around:300` od punktu, `out geom`) z `overpass-api.de` w 3 s, 7 KB;
  - ⚠️ *(poprawka `dev` → Dev report, Found 1: punkt w tym pomiarze był błędny)* **zwrócony obrys nie zawierał punktu.** To sąsiedni cmentarz w promieniu 300 m, więc wybór obrysu musi sprawdzać, czy
    punkt jest w środku;
  - alejki w ramce obrysu dużego cmentarza: `overpass-api.de` dwa razy **504**, `overpass.private.coffee` bez odpowiedzi
    w 40 s, `maps.mail.ru` 200 w 20 s. Wynik: 482 drogi i 3319 punktów (`service` 132, `footway` 337, `path` 10, `steps` 2,
    `track` 1), czyli **ok. 70 KB** jako współrzędne bez nazw, przed odcięciem tego, co poza obrysem;
  - wniosek: ponawianie, kilka instancji i stan (c) „serwer nie odpowiada” to nie ostrożność, tylko norma (jak SPIKE-001 M11).
- **Zasady `overpass-api.de`** ([Overpass API — commons](https://dev.overpass-api.de/overpass-doc/en/preface/commons.html)): *„a
  maximum of about 10000 requests per day”*, *„below about 1 GB per day”*, a odmowa za tempo to HTTP 429. Za problem uznają
  *„setting up an app for more than just OSM mappers and relying on the public instances as backend”*. Grobing ma **jednego
  użytkownika** i 11 cmentarzy, a plan pobiera się raz na cmentarz, więc to kilkadziesiąt zapytań w ogóle. Gdyby aplikacja
  kiedyś trafiła do innych rodzin, potrzebna będzie własna instancja albo inne źródło — [[NT-005-distribution-decision]].
- **`flutter_map` 8.3.2 domyślnie zapisuje kafelki na dysk.** Źródło pakietu
  (`lib/src/layer/tile_layer/tile_provider/network/tile_provider.dart`): *„Caching provider used to get cached tiles. … Defaults
  to [BuiltInMapCachingProvider]. Set to [DisabledMapCachingProvider] to disable.”*. Wbudowany zapis idzie do
  `getApplicationCacheDirectory()`. Bez `cachingProvider: const DisabledMapCachingProvider()` zdjęcie z góry zostawałoby w
  telefonie wbrew [[ADR-003-map-source-offline]] pkt 2. Domyślny klient kafelków to `RetryClient(Client())` z pakietu `http`
  (już w drzewie zależności `flutter_map`), więc **żadna nowa zależność nie jest potrzebna**. Zapytanie o plan robi
  `dart:io` `HttpClient`.
- **Z kodu** (ankieta 2026-10-12):
  - **kopia i odcisk biorą tabele z `sqlite_master`** (`data_state.dart`: *„a table added by a later schema counts without code
    changes”*), a kopia to migawka całej bazy. Plan w bazie wchodzi więc do kopii, odcisku i „Stanu danych” bez zmian w
    `backup_*`;
  - groby mają `lat`, `lon`, `positionSource`, `positionAccuracyM` od v1. `GraveSummary` niesie dziś samo `hasPin`;
  - każdy zapis prosi o kopię w tle (`watchChanges` w `grobing_app.dart`), więc pobrany plan też ją wywoła — raz na
    cmentarz. To jest w porządku;
  - `grobing_app.dart` ma już `WidgetsBindingObserver` (`paused` → kopia); `resumed` jest wolne;
  - poprawa cmentarza (okno → wskazanie) żyje prywatnie w `home_screen.dart` (`_edit`), a ekran cmentarza nie ma ✎;
  - `CemeteryScreen(highlightGraveId:)` to dziś lista z zaznaczeniem (v4.3);
  - debug ma wymyślone dane z punktami w okrągłych, wymyślonych miejscach (`fictional_data.dart`), gdzie OSM nie ma
    cmentarza, czyli gotowy przypadek (d) „brak obrysu”, a co trzecia partia jest bez punktu (e);
  - emulatory to obrazy Play Store (`google_apis_playstore`): bez `adb root`, a release bez `run-as`. **Groby z pinezką na
    emulatorze da tylko build debug**, bo pinezek nie da się postawić do US-008.
- **Pułapki z poprzednich pozycji:**
  - `CameraConstraint.contain` przy ramce mniejszej od ekranu (ADR-003 → *Follow-ups*, M7) — a tu najmniejsze przybliżenie to
    właśnie cały cmentarz w ekranie;
  - koszt rysowania sprawdzony dopiero ANR-em (ISSUE-023, *Do retro*);
  - semantyka przycisków w arkuszach (`Semantics` z `onTap`, `container`; cztery wcześniejsze pozycje).

### Stop #1 (2026-10-12) — autor: „tak”
D1 = **W2** (7:1 dla tekstu czytanego przy grobie), D2 = **A** (ADR-015, plan w bazie i w kopii, schemat v10), D3 (pobieranie w
aplikacji), D4 (`overpass-api.de` → `overpass.private.coffee`, bez `maps.mail.ru`), D5, D6 (jedna pozycja) przyjęte; decyzje projektowe
[[cmentarz]] D17–D23 potwierdzone. Miarę NFR-004 (W2) `docs` wpisze przy zamknięciu.

### Decisions for stop #1 (rekomendacja → „tak” przyjmuje wszystkie)
- **D1 — miara [[NFR-004-czytelnosc-w-sloncu]] na tym ekranie** (⚠️ OPEN ze specyfikacji, makieta ramki B1 i B2):
  - **W1:** jak dziś — adres, „3 osoby”, linia grobów bez pinezki i druga linia zaślepek w tekście pomocniczym (5,01:1, AA);
  - **W2 (rekomendacja `ui`):** 7:1 (SC 1.4.6) dla tekstu, który czyta się przy grobie — te linie w kolorze tekstu (10,02:1).
    W tekście pomocniczym zostają tylko podpisy źródeł. Bez nowych tokenów. Test w słońcu na telefonie przy instalacji MVP.

  Po decyzji `docs` wpisze miarę do NFR-004, [[style-b]] (*Thresholds*) i [[grob]] (*Known gaps*).
- **D2 — ADR-015 „Plan cmentarza w bazie (schemat v10), w kopii”** (pisze łańcuch, `docs` przy zamknięciu):
  - **A (rekomendacja):** tabela `cemetery_plans` — jeden wiersz na cmentarz (`cemetery_id` klucz główny), status (`ok` ·
    `notInOsm`), obrys i alejki jako zwarty JSON samych współrzędnych (bez nazw i znaczników), czas pobrania i serwer.
    Plan wchodzi do kopii, więc po odtworzeniu na nowym telefonie działa bez sieci od razu ([[NFR-002-odtworzenie-na-nowym-telefonie]]).
    Duży cmentarz to ok. 70 KB na plan, a 11 cmentarzy to razem mniej niż 1 MB. Krok `_from9To10` to sam `createTable`;
  - **B:** plik planu poza bazą i poza kopią. Kopia jest mniejsza, ale po odtworzeniu każdy plan trzeba pobrać ponownie, a
    na cmentarzu bez zasięgu go nie ma. Pliki w `media/` odpadają, bo sprzątanie usuwa każdy plik bez wiersza;
  - **C:** kolumna w `cemeteries`. Bez statusu i czasu pobrania, a każdy plan powiększa wiersz czytany przez mapę Polski.

  A **nie zastępuje** żadnego ADR — sygnał dla `architect` się nie zapala.
- **D3 — kiedy plan się pobiera** ([[cmentarz]] D18):
  - **rekomendacja:** w aplikacji, bez zadania w tle. Pobieranie rusza przy zapisie cmentarza z punktem, przy zmianie
    punktu, przy starcie aplikacji, przy powrocie do niej, przy otwarciu cmentarza bez planu i po „Pobierz teraz”;
  - plany idą po kolei, najwyżej 1 zapytanie na sekundę;
  - (b) i (c) nie zapisują się w bazie, a (d) „brak obrysu” tak. (d) wraca do pobierania tylko po zmianie punktu, żeby nie
    pytać serwera przy każdym starcie;
  - tekst (b) zostaje, bo plan pobierze się przy pierwszym otwarciu aplikacji z internetem;
  - *Inaczej:* zadanie WorkManagera z warunkiem sieci, na wzór kopii. Wymaga kodu natywnego, drugiego silnika Darta i
    blokady danych (zapis w czasie odtwarzania), czyli kosztu wielkości osobnej pozycji. Pobranie w tle z zamkniętą aplikacją
    nic tu nie daje.
- **D4 — serwery planu** (prywatność, ADR-003 → *Consequences*):
  - **rekomendacja:** `overpass-api.de`, a po nim `overpass.private.coffee`. Oba działają w Niemczech, w społeczności OSM;
  - **bez `maps.mail.ru`.** W pomiarze odpowiedział tylko on, ale prowadzi go VK (Rosja), a nie OSM, a ADR-003 przyjął, że
    obszar cmentarza poznają serwery OSM i GUGiK. Nie wychodzą dane rodziny, tylko ramka publicznego cmentarza i adres IP
    telefonu;
  - koszt: częściej stan (c) i plan dzień później;
  - *obali:* (c) trzyma się na którymś cmentarzu dłużej niż tydzień startów → dokładamy trzecią instancję Twoją decyzją;
  - **GUGiK:** wyłącznie `mapy.geoportal.gov.pl`, adres kafelka z `GetCapabilities` `StandardResolution`, macierz EPSG:3857
    (jak SPIKE-001 M7);
  - wszystko tylko HTTPS, z `User-Agent` aplikacji bez danych osobowych.
- **D5 — wybór obrysu i alejek:**
  - obrys to wielokąt `landuse=cemetery` albo `amenity=grave_yard` (droga albo relacja), który **zawiera punkt** cmentarza;
  - bez takiego: najbliższy w odległości do 100 m, bo ręczny punkt bywa przy bramie;
  - bez obu: (d);
  - alejki to `highway` = `footway`, `path`, `steps` (boczne, 2 dp) oraz `pedestrian`, `service`, `track` (główne, 4 dp), jak w
    SPIKE-001 M11. Odcinek zostaje, gdy jego środek leży w obrysie;
  - współrzędne zaokrąglone do 6 miejsc (ok. 0,1 m), bez nazw i znaczników;
  - **budżet:** plan ≤ 150 KB, rysowanie mieści się w czasie klatki na dużym cmentarzu (pomiar w przejściu AC).
- **D6 — jedna pozycja.** Warstwa danych, sieć, plan, zdjęcie, stany A, B, C, zaślepki i ✎ idą razem, bo żadna część nie daje
  się ocenić osobno.
  *Obali:* `dev` nie zamknie tego w jednej sesji → podział na 027 (dane, sieć, plan i zdjęcie w stanie A, zaślepki) i 027b
  (stany B i C, uchwyt, ✎, wejście z widoku osoby). Decyzja przy pierwszej oznace, a nie po fakcie.
- **Decyzje projektowe ze specyfikacji** (do potwierdzenia tym samym „tak”): [[cmentarz]] D17 (sześć stanów planu, element
  2a), D19 (brak obrysu → zdjęcie z góry, a nie kwadrat wokół punktu), D20 / [[cmentarze]] D34 (pobieranie bez śladu na mapie
  Polski), D21 (uchwyt dotknięciem), D22 (plakietki przy dużym tekście), D23 (z widoku osoby: grób z pinezką → B, bez → lista,
  bez komunikatu do US-008).
- **Co zobaczysz po tej pozycji na prawdziwych danych:** plan bez zniczy. Pinezki przychodzą z [[US-008-pinezka-na-miejscu]],
  a znicze widać na razie tylko w danych testowych.

### Scope — files (`{code}`)
| Plik | Co |
|---|---|
| `android/app/src/main/AndroidManifest.xml` | `android.permission.INTERNET` z komentarzem: tylko plan (OSM) i zdjęcie z góry (GUGiK), lista hostów w `lib/net/hosts.dart`, NFR-005 pilnuje kod. Komentarz „No INTERNET in release” → przepisany (kopia dalej idzie przez okno „zapisz jako”). `usesCleartextTraffic="false"` jawnie |
| `lib/net/hosts.dart` (nowy) | **jedyne miejsce z adresami sieci:** Overpass (D4, w kolejności), szablon kafelka GUGiK, `User-Agent` (nazwa i wersja aplikacji, adres repo, bez danych osobowych); `https` jedynym schematem |
| `lib/net/overpass_plan_source.dart` (nowy) | `PlanSource` (interfejs — testy go podmieniają) i wersja Overpass: zapytanie o obrys od punktu, wybór obrysu i alejek (D5), parsowanie `out geom` (droga i relacja z dziurami), ponawianie po hostach z przerwą (429/5xx/czas → następny host, najwyżej 2 próby na host, cała próba ≤ ok. 60 s), wynik: plan · `notInOsm` · `offline` (brak sieci: nieudane rozwiązanie nazwy albo połączenie) · `serverError`. Odpowiedź czytana strumieniem z limitem rozmiaru |
| `lib/data/database.dart` | tabela `CemeteryPlans` (D2 A): `cemeteryId` klucz główny → `cemeteries`, `status` (`textEnum` `PlanStatus { ok, notInOsm }`), `outline`/`paths` (tekst JSON, puste przy `notInOsm`), `fetchedAt`, `server`. **Schemat v10**, `_from9To10`: `createTable` |
| `drift_schemas/grobing/drift_schema_v10.json`, `database.steps.dart`, `test/drift/grobing/generated/*` | `dart run drift_dev make-migrations` (README → *Baza danych*) |
| `lib/data/cemetery_plans.dart` (nowy) | model planu (pierścienie obrysu, alejki z klasą główna/boczna), JSON w obie strony, `watchCemeteryPlan`, `savePlan`, `saveNotInOsm`, `cemeteriesNeedingPlan` (z punktem, bez wiersza) |
| `lib/data/cemeteries.dart` | `updateCemetery`: **zmiana punktu kasuje wiersz planu w tej samej transakcji** (D3, [[cmentarz]] D18) |
| `lib/data/graves.dart` | `GraveSummary.pin` (`GeoPoint?`) obok `hasPin`; zapytanie czyta `lat`/`lon` |
| `lib/app/map/plan_downloads.dart` (nowy) | stan pobierania w pamięci per cmentarz (pobieram · offline · serverError) jako strumień dla ekranu; `download(id)`, `ensureAll()` (po kolei, jedno naraz, ≤ 1 zapytanie/s); zapis wyniku przez `cemetery_plans.dart` |
| `lib/app/grobing_app.dart` | tworzy `PlanDownloads` (podmienialne w testach jak `photos`); `ensureAll()` po starcie i przy `resumed`; nowa generacja po odtworzeniu → nowe `PlanDownloads` |
| `lib/app/grave/cemetery_plan_map.dart` (nowy) | `FlutterMap`: obrys (`PolygonLayer`, powierzchnia + obrys 1,5), alejki (`PolylineLayer`, obrys 4/2 dp), znicze (`MarkerLayer`, cel 48 dp, przycisk dla czytnika „Grób: <tytuł>”), warstwa zdjęcia (`TileLayer` z `NetworkTileProvider(cachingProvider: const DisabledMapCachingProvider(), headers: User-Agent)`, `maxNativeZoom` 19). Kadr: obrys z marginesem 16 dp w wolnym miejscu, najmniejsze przybliżenie = ten kadr, największe z19, ruch w ramce obrysu z marginesem — **bez `CameraConstraint.contain`** (pułapka M7). Płynny przesuw nad arkusz B jak `home_screen` (D30 z ISSUE-023), `disableAnimations` → bez ruchu. Plan dla czytnika jednym węzłem „Plan cmentarza” |
| `lib/app/grave/plan_placeholder.dart` (nowy) | element 2a: warianty (a)–(e), teksty dosłownie ze specyfikacji, przyciski tekstowe z semantyką; „Pobierz teraz” bez sieci → pasek komunikatu |
| `lib/app/grave/cemetery_screen.dart` | przebudowa na stany **A · B · C** ([[cmentarz]] v5): pasek z ✎, plakietki (zawijanie przy dużym tekście, D22), pasek grobów (6), arkusz grobu (7) z uchwytem dotykowym (D21), lista (8–9) jak dziś; wstecz według *Navigation*; wejście `highlightGraveId` → B przy pinezce, C bez (D23); W1/W2 według D1; „Pokaż zdjęcie z góry” (d), „Wskaż na mapie” (e) |
| `lib/app/home/cemetery_edit.dart` (nowy) | `_edit` z `home_screen.dart` jako wspólna droga (okno 15 → wskazanie 16) dla ✎ w arkuszu mapy Polski, ✎ w pasku cmentarza i „Wskaż na mapie”; po zapisie z punktem → `download(id)` |
| `lib/app/home/home_screen.dart` | poprawa przez `cemetery_edit.dart`; zapis z bazy (okno 15 „Zapisz”) → `download(id)`. Wygląd bez zmian (D34) |
| `lib/app/person/person_screen.dart` | „Pochówek” bez zmian w wywołaniu; decyzję B/C podejmuje ekran cmentarza (D23) |
| `lib/app/data_state_screen.dart` | etykieta `cemetery_plans` → „Plany cmentarzy” |
| `lib/dev/fictional_data.dart` | **tylko debug:** wymyślone pinezki (`positionSource: satellite`) dla grobów bez pinezki na cmentarzach z planem `ok`, w punktach wewnątrz obrysu, deterministycznie. Wywołanie obok dzisiejszego „wymyślonych danych” |
| `README.md` (`grobing-code`) | *Baza danych*: v10; nowa sekcja *Sieć*: po co `INTERNET`, lista hostów, `aapt` na APK, bez pamięci kafelków |

Bez zmian: `backup_*`, `restore_*`, `data_stamp.dart` (tabele z `sqlite_master`), `theme.dart` (W2 bez nowych tokenów), [[cmentarze]]
poza wywołaniem pobierania.

### AC → implementation → test (testy pisze `qa`)
| AC | Gdzie | Test happy-path |
|---|---|---|
| US-007 AC-1 | `overpass_plan_source.dart`, `cemetery_plans.dart`, `plan_downloads.dart`, `cemetery_plan_map.dart` | danych (atrapa odpowiedzi Overpass z **wymyśloną geometrią, bez nazw**): z dwóch obrysów wybrany ten z punktem; alejki poza obrysem odcięte; klasy główna/boczna; JSON w obie strony; widżet: cmentarz z planem przy atrapie sieci bez połączenia → plan, „Plan offline”, „© OpenStreetMap” |
| US-007 AC-2 | `cemetery_plan_map.dart`, `cemetery_screen.dart`, `hosts.dart` | widżet: „Zdjęcie” → warstwa kafelków z szablonem GUGiK i `DisabledMapCachingProvider`, „tylko z internetem”, „Ortofotomapa: GUGiK”; bez sieci → „bez internetu”, „Wróć do planu” → plan |
| US-007 AC-3 | `cemetery_screen.dart`, `graves.dart` | widżet: 4 groby z pinezką i 2 bez → 4 znicze, „2 groby bez pinezki — na liście”; znicz → arkusz z tytułem, adresem i „Pokaż grób” → [[grob]]; dotknięcie uchwytu → lista 6 kart; przeciągnięcie → lista; wstecz → B → A; z „Pochówku” grób z pinezką → B, bez → C z zaznaczeniem |
| US-007 AC-5 | `plan_placeholder.dart`, `plan_downloads.dart` | widżet: cmentarz bez planu przy atrapie „offline” → (b) z tekstami i „Pobierz teraz”; pasek → lista działa; „Pobierz teraz” bez sieci → pasek komunikatu; z siecią → (a) → plan |
| stany 2a, D3, D4 | `plan_placeholder.dart`, `plan_downloads.dart`, `hosts.dart`, `cemeteries.dart` | (c) po błędach serwera na obu hostach (kolejność hostów, ponowienia); (d) zapisane i bez ponownego zapytania przy następnym `ensureAll`; (e) bez przełącznika; zmiana punktu kasuje plan i rusza pobieranie; **test na źródłach:** w `lib/` żaden adres `http(s)://` poza `hosts.dart`, każdy adres w `hosts.dart` to `https` |

Testy do przepisania: `cemetery_screen_test.dart` (lista → stany A/B/C), `database_test.dart` i `data_state_screen_test.dart` (wersja 9
→ 10), testy wejścia z `person_screen` (D23), `home_screen_test.dart` (poprawa przez `cemetery_edit.dart`).

### Data layer
- **Schemat v10** (D2) z testem migracji v9→v10 na danych (`testWithDataIntegrity`, NFR-003) i plikiem schematu z `make-migrations`.
- **Próbne odtworzenie:** test — kopia v9 odtwarza się w v10 bez planów (cmentarze dostają (a)/(b), aż będzie sieć); kopia v10 z planem
  → odtworzenie → plan jest, odcisk zgodny. Na emulatorze: kopia z `Medium_Phone` (nowe hasło testowe) → `Grobing_Restore`, tryb
  samolotowy → plan jest (agent).
- **Źródło i status faktu:** ta pozycja **nie zapisuje faktów o rodzinie**. Plan to publiczne dane OSM, a pinezki w debug są
  wymyślone.
- **Dane rodziny:** w testach i atrapach tylko wymyślona geometria bez nazw; na emulatorze publiczny cmentarz z danych testowych i
  wymyślone dane debug. Plan z OSM nie zapisuje nazw (D5), więc nazwy alejek ani okolicy nie trafiają do bazy.
- **ADR-015** (D2), wpis v10 w [[data-model]], uwaga w [[NFR-005-dane-nie-opuszczaja-telefonu]] → *Notes* (hosty, HTTPS, bez pamięci
  kafelków, `aapt`) i miara NFR-004 (D1) → `docs` przy zamknięciu.

### Network — NFR-005 (DoD tej pozycji)
- Lista hostów w kodzie, tylko HTTPS (test na źródłach wyżej).
- `aapt dump permissions` na APK release: dochodzi **tylko** `INTERNET`.
- Przegląd zależności: **bez nowych pakietów** (`pubspec.lock` bez zmian poza ewentualnym `http` jako zależność bezpośrednia — wtedy
  ta sama wersja co w locku).
- `qa`: w kodzie nie ma innego wywołania sieciowego niż `PlanSource` i warstwa kafelków (`HttpClient`, `http`, `Socket` — grep).
- Brak plików kafelków w pamięci aplikacji po oglądaniu zdjęcia (build debug, `run-as ls cache`).

### Manual verification
**Agent na emulatorze** (zrzuty przed stopem #2):
1. `Medium_Phone`, build release jako aktualizacja na danych testowych v9: dane całe, „Stan danych” — v10, „Plany cmentarzy”;
   `aapt` — `INTERNET`.
2. Z siecią: start → plan publicznego cmentarza z danych testowych pobiera się sam (D3); otwarcie → plan, „Plan offline”,
   „© OpenStreetMap”; czas pobrania i rozmiar planu zapisane.
3. Tryb samolotowy, zimny start → ten sam cmentarz: plan jest; „Zdjęcie” → „bez internetu” → „Wróć do planu”. Sieć → „Zdjęcie” →
   ortofotomapa, „Ortofotomapa: GUGiK”.
4. Tryb samolotowy → dodanie cmentarza z bazy → (b) → „Pobierz teraz” → pasek komunikatu; sieć → powrót do aplikacji → plan
   pobiera się sam.
5. `Grobing_Restore`, **build debug** (dane z kopii `Medium_Phone` + wymyślone): wymyślony cmentarz → (d) → „Pokaż zdjęcie z góry”;
   cmentarz bez punktu → (e) → „Wskaż na mapie” → wskazanie → (a)/(d); wymyślone pinezki → A ze zniczami → B → uchwyt → C →
   wstecz; z widoku osoby „Pochówek” → B (grób z pinezką) i C (bez); brak plików kafelków w `cache` po oglądaniu zdjęcia.
6. `uiautomator`: znicze, uchwyt, przełącznik, przyciski zaślepek `clickable` z opisami; **tekst 200%** (plakietki D22, arkusz,
   pasek); **360 × 640 dp**.
7. **Koszt rysowania:** build profile, duży cmentarz z planem — czas klatki przy przesuwaniu i przybliżaniu (60 ruchów kamery;
   lekcja ISSUE-023).
8. Próbne odtworzenie: kopia z `Medium_Phone` → `Grobing_Restore`, tryb samolotowy → plan jest, odcisk zgodny.

(c) „serwer nie odpowiada” sprawdzają tylko testy — na emulatorze nie da się go wywołać na żądanie.

**Autor: odczucie** (najwyżej 3):
1. `Medium_Phone`: otwórz cmentarz z planem — czy plan czyta się jak plan przy bramie; przełącz na „Zdjęcie” i z powrotem.
2. W trybie samolotowym otwórz ten sam cmentarz — czy plan jest i czy jasne jest, że zdjęcie potrzebuje internetu.
3. `Grobing_Restore` (wymyślone pinezki): znicz → arkusz → uchwyt → lista → wstecz — czy przejścia między mapą, grobem i
   listą są oczywiste, a adres w arkuszu czyta się dobrze (wariant z D1).

Przegląd ekranów `ui` (subagent `qa`) przed stopem #2; `dev` przechodzi AC na emulatorze przed `qa` (retro 2, R5), z tekstem 200% i
pomiarem kosztu rysowania.

### Out of Scope
- Kwatery autora (US-007 AC-4) → [[ISSUE-028-cemetery-sectors]].
- Stawianie i poprawianie pinezek, „gdzie jestem”, stan D → [[US-008-pinezka-na-miejscu]].
- Zdjęcie z góry offline (ADR-003 → *Options*: odwracalne, gdy na miejscu go zabraknie); archiwum wiosenne GUGiK.
- Pobieranie w tle przy zamkniętej aplikacji (D3 → *Inaczej*); odświeżanie planu, gdy OSM się zmieni.
- Przycisk „cały cmentarz” (*Open* specyfikacji — znana luka SC 2.5.7); budynki (kaplica) na planie.
- Test w słońcu (NFR-004) — telefon przy instalacji MVP.

## Dev report
> `dev`, 2026-10-12. Flutter 3.41.1 (przypięty). `flutter analyze` czyste, `dart format` bez zmian. Testów nie ruszałem (`qa`),
> poza plikami wygenerowanymi przez `make-migrations` (`test/drift/grobing/generated/schema.dart`, `schema_v10.dart`) — tak jak
> README każe przy zmianie schematu. Żadnej nowej zależności (`pubspec.yaml` i `pubspec.lock` bez zmian).

### What was built (`{code}`)
- **Dane:** `CemeteryPlans` (`@DataClassName('CemeteryPlanRow')`, `PlanStatus { ok, notInOsm }`), **schemat v10**, krok `_from9To10`
  (`createTable`), `drift_schema_v10.json`; `lib/data/cemetery_plans.dart` — model planu, JSON (płaskie listy współrzędnych, 6 miejsc),
  `watchCemeteryPlan`, `cemeteriesWithoutPlan`, `savePlan`/`saveNotInOsm` (zapis tylko, gdy punkt cmentarza nie zmienił się w trakcie
  pobierania); `updateCemetery` — nowy punkt kasuje plan w tej samej transakcji; `GraveSummary.pin` (`hasPin` to teraz getter),
  `CemeteryGraves.point`.
- **Sieć:** `lib/net/hosts.dart` (jedyne adresy, D4); `lib/net/osm_plan.dart` (zapytania, wybór obrysu i alejek — czyste funkcje,
  D5); `lib/net/overpass_plan_source.dart` (`PlanSource`, ponowienia po hostach, limit ok. 60 s, rozróżnienie „brak internetu” /
  „serwer”); manifest: `INTERNET` + `usesCleartextTraffic="false"`.
- **Pobieranie:** `lib/app/map/plan_downloads.dart` — kolejka, stany (a)/(b)/(c) w pamięci, `downloadAll` przy starcie i przy
  `resumed`, `download(id)` na przedzie kolejki; `MapNetwork` nad nawigatorem (`MaterialApp.builder`) — plany, „czy zdjęcie
  osiągalne”, dostawca kafelków z `DisabledMapCachingProvider`; nowa instancja po odtworzeniu kopii.
- **Ekran:** `cemetery_screen.dart` przebudowany na A/B/C (*Navigation* v5, D21, D23), `cemetery_plan_map.dart` (plan, zdjęcie,
  znicze 28 × 35 / 38 × 47 z celem 48 dp, `containCenter`, `evenOdd`), `plan_placeholder.dart` (2a (a)–(e)), plakietki według D22,
  element 13; W2 w elementach 2a, 6, 7, 8 (c).
- **Poprawa cmentarza:** `lib/app/home/cemetery_edit.dart` — wspólna droga dla ✎ na mapie Polski, ✎ w pasku cmentarza i „Wskaż na
  mapie”; po zapisie z punktem rusza pobieranie planu. Mapa Polski: cmentarz z bazy → pobieranie od razu (D34).
- **Debug:** `addFictionalPins` i przycisk „Wymyślone pinezki na planach” w „Stanie danych” (tylko `kDebugMode`).
- „Stan danych”: etykieta „Plany cmentarzy”. README: schemat v10, wymyślone pinezki, nowa sekcja *Mapa cmentarza i sieć*.

### Deviations (do przeglądu `ui`)
1. **Karty listy (C) w kolorze tła**, nie powierzchni: lista leży teraz na arkuszu w kolorze powierzchni z uchwytem (element 8 „na
   powierzchni z uchwytem”), więc karty w kolorze powierzchni byłyby niewidoczne.
2. **„Ortofotomapa: GUGiK” jako mała plakietka na powierzchni**, a nie sam tekst — na zdjęciu nic poza zniczami i plakietkami
   (reguła 14).
3. **Arkusz grobu (B) przeciągnięty w dół → A.** Specyfikacja mówi tylko o przeciągnięciu w górę; w dół zamyka arkusz tak jak
   dotknięcie planu.
4. **Znicze grobów się nie łączą** (inaczej niż znicze cmentarzy w [[cmentarze]] element 4) — specyfikacja milczy. Na całym
   cmentarzu dwa groby obok siebie mogą się zasłonić; wtedy wybór przez listę. Kandydat do decyzji `ui`.
5. **Plan ma zawsze co najmniej 35% wysokości mapy** (`fitRoom`): na 360 × 640 dp z tekstem 200% nazwa, plakietki i pasek zajmują
   prawie cały ekran — wtedy pasek zasłania południe planu ([[cmentarz]] D14 → *Obali*).
6. **Element 1:** nazwa 18 sp, miejscowość 13 sp — jak w specyfikacji (zbudowany ekran miał 20 i 14).
7. **„Pokaż zdjęcie z góry” (2a (d))** pojawia się dopiero po sprawdzeniu, że serwer zdjęcia jest osiągalny (nazwa hosta). Bez sieci
   przycisku nie ma, jak w specyfikacji.
8. **Stan „bez internetu” przy zdjęciu** trwa, aż autor przełączy warstwę (wtedy sieć jest sprawdzana jeszcze raz); ekran sam nie
   wykrywa powrotu sieci.
9. Ikona `group_outlined` w arkuszu B ma stałe 18 dp przy tekście 200% (jak ikony w arkuszu cmentarza na mapie Polski).

### Found on the emulator (AC przed `qa`, R5) — `Medium_Phone` (release jako aktualizacja na danych testowych v9) i `Grobing_Restore` (debug)
1. **`around:300` nie łapie środka dużego cmentarza** (mierzy do krawędzi obrysu): pierwsze uruchomienie źródła na publicznym
   cmentarzu testowym dało „brak w OSM”. Zapytanie łączy teraz `is_in` (obrys zawierający punkt) z `around:300`. **Poprawka do
   *Prior art*:** wniosek „zwrócony obrys nie zawierał punktu — sąsiedni cmentarz” stał na błędnej współrzędnej podanej w planowaniu
   z pamięci (ok. 80 m za krawędzią). Punkt z bazy aplikacji leży w obrysie (`is_in`), a `around:300` zwraca ten obrys razem z
   sąsiednim — reguła D5 („największy obrys zawierający punkt”) wybiera właściwy. D5 zostaje.
2. **Kadr nie dopasowywał się po zmianie wysokości plakietek i paska** (tekst 200%: plan wchodził pod plakietki i pod pasek). Teraz
   dopasowuje się ponownie, dopóki palec nie ruszy mapy. Sprawdzone przy 200% (zrzut `b16-200-A`).
3. **Overpass:** limit kilku zapytań naraz na adres IP, a emulator wychodzi przez adres PC — moje sondy z PC w tym samym czasie dały
   na emulatorze (c). Później serwer odpowiadał „server is probably too busy” (504), więc **stanu (d) nie dało się wywołać na żywo**
   (pokrywają go testy z atrapą źródła). Ekran pokazał wtedy (c), zgodnie z prawdą.
4. **`TileLayer` dopisuje `User-Agent` przez `putIfAbsent`** do nagłówków dostawcy, więc stała mapa by się wywróciła. Nagłówki są
   zwykłą mapą (wyczytane ze źródła `flutter_map` przed pierwszym uruchomieniem).
5. **Build release:** zwykły `flutter build apk --release` ma kod wersji 1, a zainstalowany ma 4001 (`--split-per-abi`), więc Android
   odrzucił go jako „downgrade”. Zapisane w README → *Mapa cmentarza i sieć*.

Przejście AC:
- **AC-1:** z siecią plan pobrał się sam (raz po ok. 2 min przez 504, raz po ok. 30 s); tryb samolotowy, zimny start → plan, „Plan
  offline”, „© OpenStreetMap” (`a07`).
- **AC-2:** „Zdjęcie” z siecią → ortofotomapa, „tylko z internetem”, „Ortofotomapa: GUGiK” (`a06`); w trybie samolotowym → „bez
  internetu”, „Zdjęcie z góry potrzebuje internetu. Plan działa bez niego.”, „Wróć do planu” → plan (`a08`). Po oglądaniu zdjęcia
  (debug, `run-as`) w `cache` aplikacji nie ma plików kafelków.
- **AC-3** (debug, wymyślone pinezki): A ze zniczami i „1 grób bez pinezki — na liście” (`b06`); znicz → B (`b07`); uchwyt → C z
  zaznaczoną kartą (`b08`); wstecz → B → A. Z widoku osoby: grób z pinezką → B (`b09`), bez → C z zaznaczeniem (`b10`); wstecz →
  osoba.
- **AC-5:** tryb samolotowy → cmentarz z bazy → (b) (`b01`); „Pobierz teraz” → „Bez internetu. Plan pobierze się, gdy będzie
  zasięg.” (`b02`); sieć + powrót do aplikacji → plan pobrał się sam (`b03`, D3).
- **(e):** cmentarz bez punktu → zaślepka bez przełącznika (`b13`) → „Wskaż na mapie” → wskazanie → „Zapisz” → ekran w (a) (`b14`).
- **`uiautomator`:** znicze („Grób: …”), uchwyty („Pokaż listę grobów”, „Pokaż mapę”), połówki przełącznika (stan „wybrany”),
  przyciski zaślepek — `clickable`, z opisem.
- **Tekst 200%:** plakietki według D22 (`a09`), kadr po poprawce (`b16`), arkusz B (`b17`); **360 × 640 dp przy 200%** — odstępstwo 5
  (`a10`, zrzut sprzed poprawki).
- **Koszt rysowania** (jednorazowy test na PC, poza repo; plan publicznego cmentarza testowego z bazy emulatora): 60 ruchów kamery —
  ok. 5 ms na klatkę przy 112 alejkach i tyle samo przy 448 (plan ×4). Dla porównania błąd z ISSUE-023: 2–3 s na klatkę. Na
  urządzeniu nie mierzone (pierwszy prawdziwy telefon przy MVP).
- **Pomiary:** plan publicznego cmentarza testowego w bazie — obrys 2,6 KB, alejki 11 KB; `aapt` — z nowych uprawnień tylko
  `INTERNET`; APK x86_64 23,1 MB.

Zrzuty: katalog tymczasowy sesji `1d9348ed-…/scratchpad/shots/`.

### For `qa` — kroki ręczne
- **Stan emulatorów:**
  - **`Medium_Phone`** — release v10 jako aktualizacja na danych testowych autora, plan cmentarza testowego pobrany, tryb samolotowy
    wyłączony, tekst 100%;
  - **`Grobing_Restore`** — **build debug** (release odinstalowany, dane z kopii po ISSUE-023 skasowane): cmentarz testowy z bazy,
    3 wymyślone groby (2 z wymyślonymi pinezkami), dwa wymyślone cmentarze. Do próbnego odtworzenia potrzebny release, czyli znów
    odinstalowanie.
- Kroki z *Manual verification* bez zmian; (c) i (d) sprawdzają tylko testy, bo serwera nie da się zmusić ani do błędu, ani do
  odpowiedzi.

## Verification
> `qa`, 2026-10-12. Flutter 3.41.1. Rytuał WZ-024: `dart format` bez zmian → `flutter analyze` czyste → **`flutter test`: 632, wszystkie
> zielone** (przed pozycją 579) → kroki ręczne → stop #2.

### Tests (happy path per AC)
| AC / punkt | Test |
|---|---|
| US-007 AC-1 | `test/app/grave/cemetery_map_screen_test.dart` (plan z bazy: obrys, „Plan offline”, „© OpenStreetMap”, przełącznik „Plan” wybrany, sieć nie pytana); `test/net/osm_plan_test.dart` (wybór obrysu: największy z punktem, najbliższy ≤ 100 m, brak; relacja z pierścieniem z kilku dróg i dziurą; alejki przycięte do obrysu, główne/boczne); `test/net/overpass_plan_source_test.dart` (lokalny serwer: obrys → alejki, User-Agent, 504 i „runtime error” → ponowienie → następny host, alejki od hosta, który dał obrys, „brak w OSM”, serwery zajęte → (c), brak nazwy hosta → (b)); `test/data/cemetery_plans_test.dart` (JSON w obie strony, 6 miejsc, bez nazw; zapis i odczyt; nie zapisuje dla starego punktu) |
| US-007 AC-2 | ekran: „Zdjęcie” → `TileLayer` z szablonem GUGiK i dostawcą z `MapNetwork`, „tylko z internetem”, „Ortofotomapa: GUGiK”; bez sieci → „bez internetu”, tekst el. 13, „Wróć do planu” → plan; `test/net/hosts_test.dart` (dostawca kafelków z `DisabledMapCachingProvider`, nagłówki do `putIfAbsent`) |
| US-007 AC-3 | ekran: znicze z etykietą „Grób: …” tylko dla grobów z pinezką, „1 grób bez pinezki — na liście”, znicz → arkusz z „Pokaż grób”, uchwyt → lista z ramką, wstecz → B → A, pasek i „Pokaż mapę” jednym dotknięciem (D21); D23: z „Pochówku” grób z pinezką → B, bez → C z zaznaczeniem; `test/dev/fictional_pins_test.dart` |
| US-007 AC-5 | ekran: (b) z tekstami, „Pobierz teraz” bez sieci → pasek komunikatu, lista działa; (a) → (c) → „Pobierz teraz” → plan; (d) z „Pokaż zdjęcie z góry” → zdjęcie; (e) bez przełącznika; bez grobów (b) i (c) nie odsyłają do listy |
| D3 kolejka | `test/app/map/plan_downloads_test.dart` (stan „pobieram”, brak sieci → (b) dla wszystkich czekających, nic nie zapisane, potem wszystkie; (c); (d) zapisane i nie pytane drugi raz; otwarty cmentarz na przedzie; plan już jest → bez zapytania) |
| D3 zmiana punktu | `test/data/cemetery_plans_test.dart` (nowy punkt kasuje plan, ten sam punkt albo nazwa — nie; „bez punktu” kasuje) |
| W2, D22 | ekran: kolory linii czytanych przy grobie = tekst, podpis źródła = pomocniczy; 360 dp przy 160% — „Plan offline” pod przełącznikiem, bez przepełnień |
| NFR-005 | `test/net/hosts_test.dart` (w `lib/` żaden adres w stringu poza `hosts.dart` — wyjątek `external_link.dart`, adres oddawany innej aplikacji; wszystkie `https`; hosty D4; User-Agent bez danych osoby); `test/repo_invariants_test.dart` (manifest: tylko `INTERNET`, `usesCleartextTraffic="false"`, wskazanie na `hosts.dart`) |
| Schemat v10 | `test/drift/grobing/migration_test.dart` (v9 → v10 na danych: cmentarze, groby z pinezką, zdjęcie cmentarza bez zmian, plany puste, zapis planu po migracji, klucze obce całe); `test/backup/restore_service_test.dart` (**kopia v9 → v10**: liczby wierszy, zdjęcie cmentarza, cmentarz z punktem czeka na plan; **kopia v10 z planem**: ten sam odcisk, plan wraca cały); `database_test`, `data_state_test`, `data_state_screen_test` (wersja 10, 13 tabel, „Plany cmentarzy”) |

Testy przepisane: `grave_screens_test.dart`, `grave_photo_screens_test.dart` (lista za paskiem grobów), testy odtworzenia v4–v8
(nowa pusta tabela `cemetery_plans` po odtworzeniu), niezmiennik manifestu (był „bez `INTERNET`”, ISSUE-008 AC-5).

### Agent na emulatorze (przed stopem #2)
1. ✅ `Medium_Phone`, release jako aktualizacja na danych testowych v9: dane całe, „Stan danych” v10, „Plany cmentarzy”; `aapt` — z
   nowych uprawnień tylko `INTERNET` (zrzuty `a02`).
2. ✅ Z siecią plan publicznego cmentarza testowego pobrał się sam (D3; raz po ok. 2 min przez 504 Overpass, raz po ok. 30 s).
3. ✅ Tryb samolotowy, zimny start → plan, „Plan offline”, „© OpenStreetMap” (`a07`, po poprawkach `q01` — margines 16 dp nad paskiem);
   „Zdjęcie” → el. 13 (`a08`); z siecią ortofotomapa (`a06`).
4. ✅ Tryb samolotowy → cmentarz z bazy → (b) → „Pobierz teraz” → pasek komunikatu → sieć i powrót do aplikacji → plan sam (`b01`–`b03`).
5. ✅ `Grobing_Restore`, debug: (e) → „Wskaż na mapie” → (a) (`b13`, `b14`); A ze zniczami → B → uchwyt → C → wstecz (`b06`–`b08`);
   „Pochówek” → B / C (`b09`, `b10`); po oglądaniu zdjęcia w `cache` aplikacji nie ma plików kafelków (`run-as`). **(d) nie dało się
   wywołać na żywo** — Overpass odpowiadał „server is probably too busy” (504); pokrywają je testy.
6. ✅ `uiautomator`: znicze, uchwyty, połówki przełącznika, przyciski zaślepek — `clickable` z opisem; tekst 200% (`a09`, `b16`, `b17`);
   360 × 640 dp przy 200% (`a10`) → odstępstwo 5, przyjęte.
7. ✅ Koszt rysowania (test jednorazowy na PC): ok. 5 ms na klatkę przy 112 i przy 448 alejkach (błąd z ISSUE-023: 2–3 s). Na
   urządzeniu nie mierzone.
8. ✅ **Próbne odtworzenie:** na `Medium_Phone` kopia skonfigurowana od nowa z nowym hasłem testowym (wymyślonym) → `grobing-klucz-027.age`,
   `grobing-kopia-027.age` w Pobranych → `Grobing_Restore` (release, czysta instalacja), tryb samolotowy → odtworzenie: **odcisk
   `3bddd5a84974c83a` zgodny ze źródłem**, schemat 10, „Plany cmentarzy: 1”, plan na ekranie bez sieci (`r09`, `r10`). Pierwsza
   próba: „Złe hasło…”, bo `adb input` zgubił pierwszy znak (24 kropki zamiast 25) — powtórzone, przeszło; komunikat i „Dane w
   telefonie są nietknięte” zachowały się poprawnie.

### `ui` review (subagent, bez historii)
0 BLOCKER, 2 MAJOR, 7 MINOR (zrzuty `a03`–`b17`):
- **MAJOR 1** — uchwyt B/C miał cel 28 dp → **48 dp** (poprawione, test).
- **MAJOR 2** — (b)/(c) na cmentarzu bez grobów odsyłały do listy, której nie ma → **`hasGraves`**, bez tej linii (poprawione, test).
- MINOR: znicz 48 × 47 → 48 × 48; ikony `outlined`; zdjęcie ładuje się na powierzchni; „© OpenStreetMap” jako plakietka jak GUGiK
  (poprawione); margines po zimnym starcie — sprawdzony po poprawce kadru (`q01`, 16 dp); 11 sp — wyjątek w [[style-b]] v1.21; alejki
  prawie wszystkie 2 dp — to dane OSM (`footway`), nie błąd → *Open* w [[cmentarz]].
- **Odstępstwo 1 odrzucone:** karty listy w kolorze tła → **lista na tle, karty na powierzchni** (reguły 2, 11; `q02`). Odstępstwa 2–9
  przyjęte i zapisane w [[cmentarz]] v5.1.

`qa` → `dev` (poprawione przed stopem):
- **F1** — alejki pytane najpierw u hosta, który dał obrys (wcześniej znów od zajętego, z przerwami);
- **F2** — nieaktualne komentarze „aplikacja nie ma `INTERNET`” (`external_link.dart`, `pubspec.yaml`);
- **F3** — przełącznik przy dwóch rzędach zmniejsza się zamiast wychodzić za ekran;
- **F4** — „Pokaż listę grobów” to osobny węzeł (`container`): wcześniej węzeł brał granice całego panelu razem z „Dodaj grób” (piąta
  instancja błędu semantyki z *Do retro*).

### Family data
- Suchy przebieg strażnika treści na 42 plikach kodu i 9 plikach vaulta paczki — **przechodzi**.
- Fixture'y: wymyślona geometria bez nazw, wymyślone osoby („Wymyślony”, „Testowa”, „Zmyślony”), serwery w testach lokalne albo
  `*.example`/`*.invalid`.
- Bez plików `*.db`, kopii, eksportów ani zdjęć w zmianach. Na emulatorach i w zrzutach — wymyślone osoby i publiczny cmentarz z OSM.
- Kopie `-027` w Pobranych obu emulatorów i w katalogu tymczasowym sesji — dane testowe, hasło wymyślone.

### Not covered (named)
- (d) na żywo (serwer przeciążony); (c) tylko testami.
- Koszt rysowania i odczucie płynności na prawdziwym telefonie; TalkBack na planie; telefon poziomo.
- Test w słońcu (NFR-004, W2) — telefon przy instalacji MVP.
- Pobranie planu cmentarzy autora — dopiero po instalacji MVP (pamięć: dane wymyślone do instalacji).

### Stop #2 (2026-10-12) — autor: „okok”
Emulator `Grobing_Restore` (debug, dane testowe autora odtworzone z kopii `-027`, wymyślone pinezki). Odpowiedź sprawdzona na urządzeniu
(pamięć sesji: „ok” bez śladu się sprawdza):
1. **Plan i „Zdjęcie” — ok.** Ślad: ekran po stopie na warstwie „Zdjęcie”.
2. **Tryb samolotowy — ok.** Ślad w logu: 13:24:53 kafelki zdjęcia nie pobrały się z braku sieci, 13:25:00 tryb samolotowy wyłączony.
3. **Znicz → arkusz → uchwyt → lista → wstecz — ok, bez śladu na urządzeniu** (przejścia go nie zostawiają).

**Po stopie, przy sprawdzaniu śladów (F5, `qa` → `dev`):** `flutter_map` 8.3.2 przy nieudanym kafelku wypisuje błąd z **pełnym adresem
kafelka** do logu systemu (`TileLayer._onTileLoadError` → `debugPrint`, także w release) — numery kafelków to miejsce, które oglądał
telefon; na telefonie z danymi rodziny to położenie jej cmentarza (NFR-005: nic o rodzinie w logach). Poprawka:
`NetworkTileProvider(silenceExceptions: true)`, martwe wywołanie zwrotne błędu kafelka usunięte; „bez internetu” przy zdjęciu dalej
z pytania o host przy wyborze „Zdjęcia” (tak przeszedł krok 2). Test (`hosts_test`), a na emulatorze: zdjęcie, tryb samolotowy,
przesunięcie mapy → **0 linii z adresem GUGiK w logu**. Zmiana bez wpływu na wygląd, więc bez nowej rundy kroków autora. Testy po
poprawce: 632, zielone.

### Verdict
**APPROVED** (self-check, z uwagami):
- AC-1, AC-2, AC-3, AC-5 — test happy-path na każde, przejście na emulatorze, stop #2 „ok”; AC-4 → [[ISSUE-028-cemetery-sectors]];
- schemat v10 z testem migracji v9→v10; próbne odtworzenie na drugim emulatorze — odcisk zgodny, plan z kopii bez sieci;
- NFR-005: hosty tylko w `lib/net/hosts.dart`, `https`, bez pamięci kafelków (sprawdzone `run-as`), bez adresów kafelków w logu (F5),
  `aapt` — z nowych tylko `INTERNET`, bez nowych zależności;
- **uwagi:** (d) „brak w OSM” i (c) tylko testami (Overpass przeciążony); koszt rysowania mierzony na PC, nie na telefonie; test w
  słońcu (W2) i TalkBack na planie — przy instalacji MVP; znicze sąsiednich grobów nachodzą na siebie → *Open* dla US-008; alejki
  według rodzaju z OSM prawie wszystkie „boczne” → *Open* w [[cmentarz]]; krok 3 stopu #2 bez śladu na urządzeniu.

Szukałem i nie znalazłem: danych rodziny w zmianach i fixture'ach (strażnik: 41 plików kodu, 9 vaulta), innych wywołań sieci niż
`PlanSource` i warstwa kafelków (`HttpClient`, `http`, `Socket` — grep `lib/`), plików kafelków w pamięci aplikacji, przepełnień przy
tekście 200% na 411 dp, regresji w 579 wcześniejszych testach.

### Package for `docs` (lista jawna, R1)
**`grobing-code`** (41):
`README.md` · `pubspec.yaml` · `android/app/src/main/AndroidManifest.xml` · `lib/app/data_state_screen.dart` · `lib/app/external_link.dart` ·
`lib/app/grave/cemetery_screen.dart` · `lib/app/grave/cemetery_plan_map.dart` · `lib/app/grave/plan_placeholder.dart` ·
`lib/app/grobing_app.dart` · `lib/app/home/home_screen.dart` · `lib/app/home/cemetery_edit.dart` · `lib/app/map/plan_downloads.dart` ·
`lib/app/person/person_screen.dart` · `lib/data/cemeteries.dart` · `lib/data/cemetery_plans.dart` · `lib/data/database.dart` ·
`lib/data/database.g.dart` · `lib/data/database.steps.dart` · `lib/data/graves.dart` · `lib/dev/fictional_data.dart` · `lib/net/hosts.dart` ·
`lib/net/osm_plan.dart` · `lib/net/overpass_plan_source.dart` · `drift_schemas/grobing/drift_schema_v10.json` ·
`test/drift/grobing/generated/schema.dart` · `test/drift/grobing/generated/schema_v10.dart` · `test/drift/grobing/migration_test.dart` ·
`test/net/osm_plan_test.dart` · `test/net/overpass_plan_source_test.dart` · `test/net/hosts_test.dart` · `test/data/cemetery_plans_test.dart` ·
`test/app/map/plan_downloads_test.dart` · `test/app/grave/cemetery_map_screen_test.dart` · `test/app/grave/grave_screens_test.dart` ·
`test/app/photo/grave_photo_screens_test.dart` · `test/backup/restore_service_test.dart` · `test/repo_invariants_test.dart` ·
`test/data/database_test.dart` · `test/data/data_state_test.dart` · `test/app/data_state_screen_test.dart` · `test/dev/fictional_pins_test.dart`

**`grobing-vault`** (zapisane w łańcuchu): `00_START_HERE/CURRENT_STATE.md` · `00_START_HERE/TRACEABILITY.md` ·
`03_REQUIREMENTS/user-stories/US-007-mapa-cmentarza.md` · `backlog/issues/ISSUE-027-cemetery-map-plan-photo-states.md` ·
`backlog/issues/ISSUE-028-cemetery-sectors.md` · `05_DESIGN/cmentarz.md` · `05_DESIGN/cmentarze.md` · `05_DESIGN/osoba.md` ·
`05_DESIGN/brand/style-b.md` — plus to, co dopisze `docs` przy zamknięciu (ADR-015, model danych v10, NFR-004 miara W2, NFR-005
*Notes*, [[grob]] *Known gaps*).

**`grobing-agents`:** nic.

### Do retro (zebrane w tej pozycji)
- **Współrzędna z pamięci w planowaniu** dała błędny wniosek w *Prior art* („obrys nie zawierał punktu”); prawdziwy punkt z bazy
  aplikacji odwrócił go dopiero w `dev`. Lekcja z globalnego `CLAUDE.md` („cytuję źródło, nie pamięć”) dotyczy też danych do sondy.
- **`around` mierzy do krawędzi obrysu** — falsyfikator na prawdziwym cmentarzu w `dev` złapał to przed kodem ekranu.
- **Pakiet zewnętrzny pisze lokalizację do logu** (F5) — znalezione przypadkiem przy sprawdzaniu „ok”. Kandydat: przy każdej pozycji z
  siecią krok `qa` „logcat bez adresów i współrzędnych”.
- **Piąta instancja błędu semantyki** (F4: węzeł paska zlany z panelem) — wzmacnia kandydata na punkt „semantyka” w przejściu AC.
- **Overpass ma limit na IP**, a emulator wychodzi przez adres PC — sondy z PC psuły pobieranie na emulatorze.
- **`adb input text` zgubił pierwszy znak hasła** (pole bez fokusu) — pierwsza próba odtworzenia „Złe hasło”.
- **Build release na emulator:** kod wersji 4001 (`--split-per-abi`) vs 1 — zapisane w README.
