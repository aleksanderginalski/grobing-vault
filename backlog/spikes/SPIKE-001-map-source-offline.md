---
title: "SPIKE-001 — Map source: offline satellite for 10 cemetery-sized areas, cost, Grobonet coverage"
type: spike
status: done
priority: MUST
time-box: "1 day of work + the on-site check on the next cemetery visit"
hypotheses: [H3]
covers-non-tech: [N5]
quality-verdict: APPROVED
verdict-date: 2026-10-08
verdict-reviewer: self-check
created: 2026-10-05
updated: 2026-10-08
---

# SPIKE-001 — Map source + offline (S-MAP)

## The question
**Które źródło map + zdjęć satelitarnych pozwala jednej osobie trzymać offline 10 obszarów wielkości
cmentarza — na jakich warunkach i za ile — i ile z 10 cmentarzy autora pokrywa Grobonet?**

## Why it matters
Widoki 1-2 i krok 6 ścieżki stoją na tej odpowiedzi (H3). Framework nie jest ograniczeniem — oba
stosy umieją regiony offline; ograniczeniem są **warunki dostawców**: np. publiczne serwery
OpenStreetMap wprost zabraniają użycia offline (§6 N5).

## Steps
1. Grobonet: wyszukaj 10 cmentarzy autora — które mają mapę grobów (tylko liczba i nazwy cmentarzy w
   notatce; **żadnych nazwisk**). Dla pokrytych: czy da się linkować do strony grobu (→ NT-004).
   > ⚠️ **Pytanie poszerzone przez pomysł autora (2026-10-05), do decyzji przy planowaniu:** przy okazji
   > policz też, ile z 10 cmentarzy ma **plan z kwaterami** (Grobonet, strona zarządcy, tablica przy
   > bramie). Taki plan to kandydat na trzecie źródło położenia obok satelity i GPS →
   > `01_INBOX/2026-10-05-plany-cmentarzy.md`.
   > **Nazwy cmentarzy autora w vaulcie — rozstrzygnięte 2026-10-07:** autor wybrał w
   > [[NT-008-publication-review]] publiczny vault, więc nazwa cmentarza autora mówiłaby publicznie, gdzie
   > leży jego rodzina. W vaulcie **tylko liczba** (tak jak falsyfikator w [[ISSUE-015-add-cemetery-from-database]]).
   > Nazwy zostają w odpowiedzi agenta i w aplikacji.
2. 2-3 kandydatów na źródło satelitarne z prawem offline: warunki, limity, koszt dla 1 użytkownika i
   10 małych obszarów; zgodność licencji z Flutterem (uwaga: popularna wtyczka bulk-download do
   `flutter_map` jest GPL).
   > **Z briefu (§Security), dopisane przy przeglądzie `kickoff/` (retro 1, R4, 2026-10-06):**
   > - **klucz API dostawcy**, jeśli jest potrzebny: poza repo (lokalna, gitignorowana konfiguracja),
   >   ograniczony do pakietu `com.grobing.app` i certyfikatu podpisu (*Hard floors* → *No secrets in
   >   the repo*);
   > - **sieć:** pobranie regionu offline wymaga sieci, a APK release **nie ma dziś uprawnienia
   >   `INTERNET`** ([[NFR-005-dane-nie-opuszczaja-telefonu]], [[ISSUE-008-backup-write]]). Dodanie go
   >   wchodzi do ADR-003 razem z tym, co aplikacja wysyła i dokąd (tylko HTTPS — *Hard floors*).
3. Prototyp jednorazowy: jeden cmentarz offline w trybie samolotowym.
4. **Na miejscu (zaparkowane do najbliższej wizyty, np. 1 listopada):** 3 pinezki postawione wcześniej
   ze zdjęcia satelitarnego — czy prowadzą do właściwego grobu?
   > ⚠️ **Założenie podważone (autor, 2026-10-05):** notatki **nie zawierają adresów kwater** — bez
   > wiedzy, gdzie grób leży, pinezki ze zdjęcia satelitarnego postawić się nie da. Pierwsze położenie
   > powstaje na miejscu (GPS). Krok 4 do przeformułowania przy planowaniu tego spike'a — decyzja
   > autora, nie poprawka po cichu.

## Exit criterion
Wybrane źródło z uzasadnieniem i kosztem → **ADR-003** `accepted`; koszt → `06_NON_TECH/external-costs.md`
(folder na sygnał). Albo: „żadne źródło nie spełnia" → decyzja autora o kompromisie.

## Definition of Done
- [x] Odpowiedź zapisana (ADR-003) · kod prototypu usunięty · status H3 zaktualizowany w notatce spike'a.
      *(`docs`, 2026-10-08:*
      - *odpowiedź w *Findings* i w [[ADR-003-map-source-offline]] `accepted`, z kierunkiem z decyzji autora na
        stopie #2;*
      - *H3 i H10 w *Findings*;*
      - *prototyp odinstalowany z emulatora, a pliki pomiarów usunięte ze scratchpada. **Folder
        `_throwaway/spike-001/` poza repo** najpierw zablokowała ochrona Claude Code (był katalogiem roboczym
        sesji), a potem agent go usunął na wyraźną prośbę autora, 2026-10-08;*
      - *krok 4 → §Parked.)*

## Implementation plan
> `planning`, 2026-10-08. **DoR (SPIKE):** pytanie ✓ · limit czasu ✓ (1 dzień + sprawdzenie na miejscu) ·
> warunek wyjścia ✓. Spike **nie zmienia `grobing-code`** (czyta z niego tylko wbudowaną bazę cmentarzy) ani
> warstwy danych, więc test migracji i próbne odtworzenie nie mają zastosowania. Faktów o rodzinie nie
> zapisuje. Testów automatycznych nie ma, bo kod nie zostaje (DoD SPIKE). Dowodem są pomiary M1–M9 i
> prototyp, który działa w trybie samolotowym. **Danymi rodziny są tu nazwy cmentarzy autora:** zostają w
> odpowiedziach agenta, a do vaulta trafiają tylko liczby (krok 1 → *Nazwy cmentarzy autora w vaulcie*).

### Prior art (źródła, nie pamięć; odczyt 2026-10-08)
- **Ortofotomapa GUGiK** ([geoportal.gov.pl → Ortofotomapa](https://www.geoportal.gov.pl/pl/dane/ortofotomapa-orto/)):
  *„dostępna bezpłatnie do pobrania i możliwa do dowolnego wykorzystania”*. To zdjęcie **lotnicze**, a nie
  satelitarne: piksel standardowy > 10 cm, wysoka rozdzielczość ≤ 10 cm. Miasta odświeżane są co 2 lata,
  reszta kraju co 5 lat. **`GetCapabilities` usługi WMTS, pobrane w planowaniu:**
  - `StandardResolution`: warstwa `ORTOFOTOMAPA`, `image/jpeg`, macierze **EPSG:3857 0–19** (na poziomie 19
    mianownik skali 1066 ≈ 0,30 m/px w 3857, czyli ok. 0,18 m w terenie na 52° N), a także EPSG:2180 i 4326.
    `AccessConstraints`: *„brak ograniczeń”*. `Fees`: korzystanie oznacza akceptację regulaminu geoportalu;
  - `HighResolution`: **tylko EPSG:2180 i EPSG:4326**, poziomy 0–16 (≈ 0,07 m/px). **EPSG:3857 nie ma.**
    `flutter_map` rysuje domyślnie w 3857, więc tej warstwy **nie zakładamy**, tylko ją mierzymy (M9). Taką
    lekcję zapłaciło już Ankh-Morpork: fundament na założonej projekcji, a potem ADR-017/018 do korekty
    (globalny `CLAUDE.md` → *Skąd ta reguła*).
- **Regulamin geoportalu** ([geoportal.gov.pl/pl/o-geoportalu/regulamin](https://www.geoportal.gov.pl/pl/o-geoportalu/regulamin/),
  w życie od 2024-07-08), § 3 ust. 2: *„Publikacja materiałów z Serwisu jest dozwolona pod warunkiem
  umieszczenia informacji o źródle pochodzenia”*. Narzędzie, które streszczało stronę, nie znalazło zapisów o
  masowym pobieraniu, pamięci podręcznej ani limitach zapytań. **`dev` czyta regulamin w całości** (krok 2), bo
  streszczenie nie jest kanonem.
- **Google Map Tiles API** ([Map Tiles API Policies](https://developers.google.com/maps/documentation/tile/policies)):
  *„you must not pre-fetch, index, store, or cache any Content except under the limited conditions”*. Do tego
  zakaz użyć „non-visualization… such as offline uses”. Treść pochodzi z wyniku wyszukiwania, więc `dev`
  potwierdza ją na stronie. **Odpada.**
- **Esri World Imagery (for Export)** ([ArcGIS Blog — Wayback Export](https://www.esri.com/arcgis-blog/products/arcgis-living-atlas/imagery/wayback-export)):
  eksport *„small volumes of basemap tiles for offline use in ArcGIS applications and other applications built
  with an ArcGIS Maps SDK”*; wymaga konta organizacji, domyślny limit to 100 000 kafelków. Offline działa więc
  tylko w SDK Esri, a nie w `flutter_map`. Odczyt z wyniku wyszukiwania.
- **Mapbox Raster Tiles API** ([docs.mapbox.com/api/maps/raster-tiles](https://docs.mapbox.com/api/maps/raster-tiles/)):
  Mapbox Satellite można pobierać w każdym kliencie XYZ. Rozliczenie idzie za zapytanie o kafelek (darmowy próg
  podaje cennik), a `Cache-Control` daje 12 h w urządzeniu. **Zapisu o offline poza SDK Mapboksa w
  [ToS](https://www.mapbox.com/legal/tos) nie znaleziono** → `dev` szuka go w *Product Terms* (krok 2).
- **Kafelki OSM:** offline zabronione (brief §6 N5, sprawdzone 2026-10-05). Zdjęć lotniczych OSM i tak nie ma.
- **`flutter_map` — offline** ([docs.fleaflet.dev/tile-servers/offline-mapping](https://docs.fleaflet.dev/tile-servers/offline-mapping)):
  trzy drogi, czyli pamięć podręczna, masowe pobranie i dołączenie plików. *„Many tile servers will forbid or
  restrict bulk downloading”*. `flutter_map_tile_caching` ma licencję **GPL** (odpada), `flutter_map_cache`
  **MIT**, a `flutter_map_mbtiles` i `flutter_map_pmtiles` są paczkami społeczności (licencje sprawdza
  `dev`). `flutter_map` 8.3.2 jest już w aplikacji (ADR-007), bez warstwy kafelków.
- **Grobonet** ([antyweb](https://antyweb.pl/jak-znalezc-zmarlego-na-cmentarzu-grobonet-i-inne-wyszukiwarki-grobow),
  [spidersweb](https://spidersweb.pl/2021/10/wyszukiwarka-cmentarna-jak-znalezc-grob-zmarlego-aplikacje.html)):
  szuka się w nim **po imieniu i nazwisku** zmarłego. Wynik pokazuje mapę i adres kwatery. Wiele cmentarzy ma
  też **własną wyszukiwarkę zarządcy** (np. [Wrocław](https://www.wroclaw.pl/wyszukiwarka-grobow)). Liczby z
  prasy (ok. 1,4 tys. cmentarzy) są niesprawdzone. **Wniosek dla planu:** sprawdzać da się tylko
  **cmentarz**. Szukanie osoby wysłałoby nazwisko z rodziny do zewnętrznej usługi, więc agent go nie robi (D2).
- **W tym repo:** jednorazowy projekt poza repo i `Grobing_Restore` ([[SPIKE-003-backup-and-restore]] D3) ·
  wczytanie pliku systemowym oknem bez `INTERNET` ([[ISSUE-009-restore]]), czyli transport drogi (b) w D6 jest
  już sprawdzony · wbudowana baza cmentarzy z punktem każdego cmentarza, **bez obrysów**
  ([[ISSUE-015-add-cemetery-from-database]], `{code}/assets/cemeteries/`) · granica „punkt cmentarza autora =
  gdzie leży rodzina” ([[NFR-005-dane-nie-opuszczaja-telefonu]] → *Notes*, link satelitarny).

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego / czego to nie da |
|---|---|---|---|
| D1 | **Skąd lista cmentarzy autora i ile ich jest** (spike mówi o 10, a pomiar w [[ISSUE-014-home-map-of-poland]] o 8 z 8) | **Autor wpisuje w czacie** nazwę i miejscowość każdego cmentarza i potwierdza liczbę N. Agent nie czyta `family_data_dir` | Odczyt `family_data_dir` zablokował klasyfikator mimo zgody autora (2026-10-07), a nazwy w czacie nie trafiają do żadnego pliku w repo. **Koszt:** kilka minut autora. **Obali:** autor woli zgodę na odczyt notatek, a wtedy przy blokadzie i tak wracamy do czatu |
| D2 | **Krok 1 poszerzony** (⚠️ pierwszy w krokach) | Dla każdego z N cmentarzy agent liczy: **M1** Grobonet ma ten cmentarz · **M2** zarządca ma własną wyszukiwarkę grobów · **M3** w sieci jest plan z kwaterami (Grobonet, strona zarządcy). **Tylko cmentarz, nigdy osoba** | Wyszukiwarki szukają po nazwisku, więc szukanie osób z rodziny wysłałoby dane rodziny na zewnątrz. Robi to autor, jeśli chce, we własnej przeglądarce. **Nie da:** liczby grobów autora, które Grobonet zna. Plan na tablicy przy bramie sprawdzi się dopiero na miejscu (D5) |
| D3 | **Kandydaci i kolejność** | **1. ortofotomapa GUGiK** (bez opłat, bez klucza, „dowolne wykorzystanie”, EPSG:3857 do z19) jako falsyfikator · **2. Mapbox Satellite** i **3. Esri World Imagery** tylko na papierze (warunki, koszt) · Google i OSM odpadają z cytatem | GUGiK jest kanonem dla Polski, a cmentarze autora są w Polsce. Prototyp innego dostawcy wymaga konta i klucza autora. **Bramka A:** jeśli regulamin GUGiK zabrania pobrania offline, to STOP i decyzja autora o koncie u drugiego kandydata |
| D4 | **Gdzie żyje prototyp** | `{code}/../_throwaway/spike-001/` (poza trzema repo), `applicationId` `com.grobing.spike001`, z uprawnieniem `INTERNET` **tylko tam**. Obszar testowy to **publiczny cmentarz spoza listy autora** (domyślnie Stare Powązki, już w testach) | `com.grobing.app` zostaje bez `INTERNET`. Cmentarz spoza listy nie mówi nic o rodzinie, więc jego nazwa może trafić do *Findings*. Jeśli Powązki są na liście autora, `dev` bierze inny duży cmentarz i w vaulcie pisze tylko „publiczny cmentarz testowy” |
| D5 | **Krok 4 — przeformułowany** (⚠️ drugi w krokach) | **Sprawdzenie na miejscu bez aplikacji, zaparkowane** (`cmentarz`, warunek: najbliższa wizyta). Przy 3 grobach, które autor zna: (a) dokładność GPS telefonu przy grobie w metrach (dowolna mapa z niebieską kropką); (b) czy kropka na ortofotomapie trafia we właściwy rząd albo aleję; (c) czy zdjęcie da się czytać w słońcu; (d) czy przy bramie wisi plan z kwaterami. Odpowiedź w czacie: **same liczby i tak/nie**. **Spike zamyka się po krokach 1–3** (ADR-003 `accepted`), a krok 4 zostaje w §Parked | Pinezki ze zdjęcia przed wizytą odpadają, bo notatki nie mają adresów kwater. Sprawdzenie na miejscu mierzy H3 (ręczna pinezka wystarczy, żeby dojść) i H9 i nie potrzebuje kodu, który i tak zostałby usunięty. **Nie da:** pomiaru pinezki postawionej w aplikacji, bo takiej funkcji jeszcze nie ma (M6 w [[EPIC-002-wizyta]]) |
| D6 | **Jak zdjęcie trafia do telefonu** — decyzja dla ADR-003 **na stopie #2, z pomiarami**, nie teraz | Wstępnie **(b): aplikacja zostaje bez `INTERNET`**, a obszar cmentarza przygotowuje się na PC jako plik i wczytuje systemowym oknem. Alternatywa **(a):** `INTERNET` w aplikacji, pobieranie z jednego hosta po HTTPS, tylko na dotknięcie. **(c)** zdjęcia wbudowane w APK odpadają, bo publiczne repo zdradziłoby listę cmentarzy autora | Dziś [[NFR-005-dane-nie-opuszczaja-telefonu]] pilnuje system, bo aplikacja nie ma jak czegokolwiek wysłać. Przy (a) pilnuje tego już tylko kod. **Koszt (b):** krok na PC przy każdym nowym cmentarzu i przy odświeżeniu ortofotomapy (co 2–5 lat). **W obu drogach** GUGiK widzi zapytania o obszar cmentarza z adresu IP autora; to granica z NFR-005 → *Notes*. **Obali (b):** M8 pokaże dużą objętość albo autor uzna krok na PC za zbyt ciężki |

### Scope diff vs the item (to accept at stop #1)
- **„zdjęcie satelitarne” → „zdjęcie z góry”:** jeśli wygra GUGiK, źródłem będzie ortofotomapa lotnicza. Podpis
  linku „Zobacz zdjęcie satelitarne ↗” z ISSUE-015 zostaje bez zmian, bo prowadzi do Map Google.
- **+ M2 i M3** (wyszukiwarka zarządcy, plan z kwaterami): to kandydaci na luku 1 w `TRACEABILITY.md`, czyli jak
  znaleźć grób bez pinezki. Adres kwatery z wyszukiwarki zarządcy pozwala znaleźć grób **za pierwszym razem**.
- **+ M6 (widoczność):** czy na ortofotomapie widać aleje i rzędy na **cmentarzach autora**, czy tylko korony
  drzew. Stare cmentarze parafialne bywają całe pod drzewami.
- **+ D6** jako jawne pytanie ADR-003. Brief (§Security) wymaga, żeby decyzja o `INTERNET` weszła do ADR-003.
- **Koszt 0 zł → bez folderu `06_NON_TECH/`:** wynik trafia do ADR-003 i do H10 w *Findings*. Folder powstaje,
  gdy pojawi się pierwszy koszt większy od zera (`doc-growth.md`).
- **Spike zamyka się bez kroku 4** (D5). Krok 4 przechodzi do §Parked jako sprawdzenie na cmentarzu.
- **− Out of scope:**
  - ekran mapy cmentarza, pinezki, pobieranie i wczytywanie obszaru w `com.grobing.app`, czyli dalsze pozycje
    [[EPIC-002-wizyta]];
  - `INTERNET` w aplikacji;
  - zmiany w modelu danych i w glosariuszu. *Findings* daje tylko propozycje, a `docs` je stosuje po decyzji
    autora;
  - zamknięcie [[NT-004-grobonet-link-terms]] (spike daje tylko wejście);
  - szukanie osób w Grobonecie i wyszukiwarkach zarządców;
  - wysoka rozdzielczość w aplikacji (M9 tylko mierzy);
  - zdjęcie w kopii zapasowej (propozycja w *Findings*).

### Steps (dev) — w kolejności falsyfikatora, z limitem czasu
**Przed krokiem 1 (autor, czat):** lista N cmentarzy (D1).

1. **Krok 1 — cmentarze (≤ 1,5 h).** M1–M3 dla każdego z N, tylko po nazwie cmentarza i miejscowości (D2). **M4:**
   zapis regulaminu Grobonetu o linkowaniu do strony grobu, cytat z datą, jako wejście do NT-004. W
   odpowiedzi agenta: tabela z nazwami. W *Findings*: same liczby (np. „M1: 3 z N”).
2. **Warunki i koszt (≤ 1,5 h). M5:** tabela dla GUGiK, Mapbox i Esri plus odrzuconych (Google, OSM):
   - czy wolno trzymać obszar offline;
   - czy potrzebny jest klucz albo konto;
   - koszt dla 1 osoby i N obszarów;
   - zgodność z `flutter_map`;
   - cytat i data odczytu każdego warunku.

   Regulamin geoportalu czytany w całości, a podstawa prawna bezpłatności z ustawy. Licencje paczek do
   zapisu kafelków: bez GPL. **Bramka A** (D3).
3. **Widoczność (≤ 1 h). M6:** dla każdego z N cmentarzy kilka kafelków z18–z19 `StandardResolution` wokół
   punktu z wbudowanej bazy (`{code}/assets/cemeteries/`) do scratchpada. Ocena: widać aleje, rzędy, czy tylko
   drzewa? W *Findings* tylko liczby. Kafelki usunięte w kroku 6. **Bramka B:** jeśli rzędy widać na mniej niż
   połowie, przed prototypem idzie **M9** (≤ 1 h): `HighResolution` w EPSG:2180 albo 4326 w `flutter_map`
   (`Proj4Crs` / `Epsg4326`). Czy kafelki trafiają w siatkę, a obraz w punkt z bazy? Zmierzone, nie założone.
4. **Prototyp (≤ 2,5 h). M7:** w `_throwaway/spike-001/` pobranie obszaru publicznego cmentarza testowego (D4)
   w z16–z19:
   - obszar to obrys z Overpass, a gdy ten nie odpowiada, kwadrat ±300 m wokół punktu;
   - pobieranie po kolei, z własnym `User-Agent`, najwyżej 2 zapytania na sekundę;
   - kafelki zapisane jako pliki, mapa `flutter_map` z kafelkami z plików i podpisem „Ortofotomapa: GUGiK”.

   Build release na `Medium_Phone`, a potem **tryb samolotowy, zimny start i przesuwanie**. Pomiary: liczba
   kafelków, MB, czas pobrania, czas pierwszego obrazu offline.
5. **Objętość (≤ 0,5 h). M8:** dla N cmentarzy autora liczba kafelków i MB w z16–z19, wyliczona z obrysów
   (Overpass) albo z kwadratu ±300 m, **bez pobierania**. W *Findings*: suma i największy obszar.
6. ***Findings* + sprzątanie:**
   - tabela M1–M9;
   - rekomendacja do ADR-003: źródło, droga (a) albo (b) z kosztem, format zapisu, czy zdjęcie wchodzi do
     kopii (dane publiczne, do ponownego pobrania);
   - status H3 i H10;
   - wejście do NT-004;
   - propozycja dla modelu danych: plan zarządcy jako trzecie źródło pozycji, tylko jeśli M3 > 0.

   Usuwane: `_throwaway/spike-001/`, kafelki i `GetCapabilities` ze scratchpada, aplikacja `com.grobing.spike001`
   z emulatora.

**Limit czasu:** po ok. 4 h bez zamkniętych kroków 1–3 → stop i raport, bez dociągania na siłę.
**Dane:** nazwy cmentarzy autora tylko w odpowiedziach. **Przed `git add`:** grep zmian po każdej nazwie
cmentarza i każdej miejscowości z D1 (pamięć: przegląd po odczycie danych rodziny). Prototyp nie zawiera
żadnych osób.

### Exit → evidence
| Warunek | Dowód |
|---|---|
| Źródło z prawem offline, z uzasadnieniem | M5 z cytatami; bramka A przeszła |
| Koszt | M5 (spodziewane 0 zł dla GUGiK) → ADR-003 i H10 |
| Działa bez zasięgu | M7: zimny start w trybie samolotowym na `Medium_Phone` |
| Widać to, czego potrzebuje autor | M6 na N cmentarzach autora (+ M9, gdy zadziała bramka B) + krok autora na stopie #2 |
| Ile z N ma Grobonet, wyszukiwarkę zarządcy, plan z kwaterami | M1–M3 (liczby) |
| Status H3 | *Findings*; część na miejscu → §Parked (D5) |

### Manual verification (stop #2, po polsku, według miejsca)
Kroki dla autora dotyczą tylko odczucia (`DEFINITION_OF_DONE.md` → *Kto sprawdza*). Działanie offline, czas i
objętość sprawdza agent i zapisuje jako „kroki oddane agentowi”.
- **Emulator `Medium_Phone`** (tryb samolotowy włączy agent):
  1. Otwórz aplikację „spike 001”. Przybliż cmentarz testowy najmocniej, jak się da. **Czy rozpoznajesz aleje i
     rzędy grobów** na tyle, żeby wiedzieć, w którą stronę iść?
  2. Przesuń mapę palcem po całym cmentarzu. Czy obraz nadąża, czy widać puste kwadraty?
- **Napisz tutaj:**
  - „ok” · „pomiń” · opis tego, co nie gra;
  - **wybór drogi (D6): (a) czy (b)**. Agent poda go razem z pomiarami M7 i M8.

### Closing checklist (docs)
- [[ADR-003-map-source-offline]]:
  - *Decision* z *Findings* (źródło, droga z D6 i koszt);
  - *Options considered* ≥ 3, w tym odrzucone z cytatem;
  - tytuł i treść poprawione „10” → N z D1;
  - status `accepted`.

  Albo, przy bramce A: `proposed` + decyzja autora.
- [[NFR-001-offline]] → *Notes*: kroki 2–7 mają już źródło. Na miejscu sprawdza to §Parked (D5).
- [[NFR-005-dane-nie-opuszczaja-telefonu]] → *Notes*: droga z D6 i zapytania o obszar cmentarza (granica).
- `CURRENT_STATE.md` → §Parked: wpis kroku 4 (`cmentarz` · pytanie bez danych rodziny · warunek: najbliższa
  wizyta · 2026-10-08).
- `01_INBOX/2026-10-05-plany-cmentarzy.md`: wynik M3. Model danych i glosariusz (*pinezka*) zmieniają się tylko po
  decyzji autora o planie zarządcy jako źródle. Notatka znika z INBOX, gdy ta decyzja zapadnie.
- [[NT-004-grobonet-link-terms]]: wejście z M4. Zamknięcie, jeśli cytat odpowiada na pytanie.
- `TRACEABILITY.md` → *Open gaps* 1: odsyłacz do M2 i M3.
- Sprzątanie z kroku 6 potwierdzone. Paczka: **vault** (i `grobing-agents`, jeśli coś się zmieni), **bez
  `grobing-code`**. Przed `git add` grep po nazwach z D1.

## Findings
> `dev`, 2026-10-08. Kolejność kroków zmieniona po stopie #1, bo listy cmentarzy autora (D1) jeszcze nie ma.
> Najpierw idą krok 2 (M5) i krok 4 (M7), które jej nie potrzebują. Kroki 1, 3 i 5 (M1–M3, M6, M8) czekają na
> listę. Prototyp: `com.grobing.spike001` w `_throwaway/spike-001/` (poza repo), Flutter 3.41.1, `flutter_map`
> 8.3.2, build release, emulator `Medium_Phone` (Android 16, x86_64).

### M5 — warunki i koszt (krok 2; odczyt 2026-10-08)
| Źródło | Offline dla 1 osoby? | Klucz / konto | Koszt dla N obszarów | Z `flutter_map` | Werdykt |
|---|---|---|---|---|---|
| **Ortofotomapa GUGiK** (WMTS `StandardResolution`) | **tak**. Operator: *„dostępna bezpłatnie do pobrania i możliwa do dowolnego wykorzystania”* ([geoportal](https://www.geoportal.gov.pl/pl/dane/ortofotomapa-orto/)). [Regulamin geoportalu](https://www.geoportal.gov.pl/pl/o-geoportalu/regulamin/) (w życie 2024-07-08, przeczytany w całości) nie zawiera ani jednego zapisu o pobieraniu, pamięci podręcznej czy limitach. § 3 ust. 1: informacje z serwisu *„nie podlegają ochronie”* prawa autorskiego (art. 4 ustawy). § 3 ust. 2: publikacja *„pod warunkiem umieszczenia informacji o źródle pochodzenia”*. `GetCapabilities`: `AccessConstraints` *„brak ograniczeń”* | **brak** | **0 zł**. Opłaty za ortofotomapę zawieszone od 24.06.2020 (art. 15zzzia ustawy covidowej; [pismo Głównego Geodety Kraju z 30.06.2020](https://geoforum.pl/upload2/files/200703-ggk.pdf)), a dane GUGiK wystawił do pobrania usługami sieciowymi | **tak**: macierz EPSG:3857 to standardowa siatka WebMercator (narożnik −20037508,34 / 20037508,34, kafelek 256 px, skala z0 5,59 · 10⁸), więc x/y/z są te same co w `flutter_map`. Sprawdzone na kafelku i na obrysie OSM (M7) | **wybrany** (bramka A ✅) |
| Archiwum ortofotomap GUGiK (WMS `StandardResolutionTime`) | tak, te same warunki | brak | 0 zł | tak: WMS `GetMap` w `CRS=EPSG:3857` z ramką kafelka; wymiar `time` 1995-01 … 2025-11, krok co miesiąc | **zapas** na korony drzew (zdjęcie z wiosny bez liści) — patrz M6 |
| Ortofotomapa GUGiK, wysoka rozdzielczość (`HighResolution`, ≤ 10 cm) | tak | brak | 0 zł | **nie wprost**: tylko EPSG:2180 i 4326, poziomy 0–16; potrzebny inny układ w mapie | M9 tylko przy bramce B |
| Mapbox Satellite | **tylko przez Maps SDK Mapboksa**: *„Users of the SDK must retrieve Mapbox data intended for offline use from Mapbox servers--the data may not be preloaded, bundled or otherwise redistributed”*; limit 750 paczek kafelków ([Offline: concepts](https://docs.mapbox.com/android/maps/guides/offline/concepts/)). Raster Tiles API w kliencie XYZ: `Cache-Control` 12 h, a zapisu o offline poza SDK nie ma ([Raster Tiles API](https://docs.mapbox.com/api/maps/raster-tiles/), [ToS](https://www.mapbox.com/legal/tos)) | konto + klucz | za zapytanie, ponad darmowy próg (cennika nie czytano, bo kandydat odpadł) | **nie**: offline wymaga drugiego silnika mapy (SDK Mapboksa) | odrzucony |
| Esri World Imagery (for Export) | tylko *„in ArcGIS applications and other applications built with an ArcGIS Maps SDK”*; konto organizacji; domyślnie do 100 000 kafelków (wynik wyszukiwania; strona bloga Esri zwróciła 403) | konto + licencja (dla ArcGIS Maps SDK for Flutter: *„license your app for deployment using either user authentication or a license string”*, poziom Lite bezpłatny — [FAQ](https://developers.arcgis.com/flutter/faq/)) | nieustalony | **nie**: offline tylko w SDK Esri (drugi silnik mapy) | odrzucony |
| Google Map Tiles API | **nie**: *„you must not pre-fetch, index, store, or cache any Content”*, a wśród zakazanych użyć *„Offline uses”* ([Map Tiles API Policies](https://developers.google.com/maps/documentation/tile/policies)) | — | — | — | odrzucony |
| Kafelki OSM | **nie** (brief §6 N5, 2026-10-05); zdjęć lotniczych OSM nie ma | — | — | — | odrzucony |

**Paczki do zapisu kafelków (bez GPL):**
- `flutter_map` 8.3.2 ma wbudowany `FileTileProvider`, czyli kafelki z plików `z/x/y.jpg`. Prototyp nie
  potrzebuje żadnej paczki;
- [`flutter_map_mbtiles`](https://pub.dev/packages/flutter_map_mbtiles) 1.0.4: MIT, `flutter_map` < 9, ale ciągnie
  `sqlite3_flutter_libs` 0.5, a aplikacja ma własny, dołączony SQLite przez `sqlite3` 3.x
  ([[ADR-005-sqlite-package]]). **Konflikt do rozważenia**: jeśli kafelki mają być w jednym pliku MBTiles,
  prościej czytać go istniejącym `sqlite3`;
- [`flutter_map_cache`](https://pub.dev/packages/flutter_map_cache) 2.1.0: MIT, ale *„does not provide support to
  download tiles automatically”*, więc się nie nadaje;
- `flutter_map_tile_caching`: GPL, odpada (plan).

**H10** (darmowe progi wystarczą): **potwierdzona mocniej, niż zakładano.** Kanoniczne źródło dla Polski
kosztuje 0 zł bez żadnego progu, więc `06_NON_TECH/` nie powstaje (plan → *Scope diff*).

### M7 — prototyp offline (krok 4)
**Obszar:** publiczny cmentarz testowy Stare Powązki. Obrys z Nominatim (OSM way 93811398, 42,6 ha), bo
Overpass zwracał 504/500 na trzech instancjach. Ramka obrysu w z16–z19 to 642 kafelki.

| Pomiar | Wynik |
|---|---|
| Pobranie (po kolei, ≤ 2 zapytania/s, własny `User-Agent`) | **628 z 642 w porządku, 14 błędów (2,2%), 5,35 MB, 355 s.** Odpowiedź serwera na jeden kafelek zajmuje ok. 0,25 s, więc czas wyznacza tempo grzecznościowe, a nie serwer. Przyczyn 14 błędów build release nie pokazuje (bez `run-as`). Produkcyjne pobieranie potrzebuje ponowienia nieudanych kafelków |
| Objętość według zoomu | z16: 112 KB · z17: 268 KB · z18: 1070 KB · **z19: 4033 KB (75%)**. Kafelek z19 ma średnio ok. 8–10 KB, bo korony drzew dobrze się kompresują |
| **Offline** | tryb samolotowy włączony (`airplane_mode_on` = 1, `ping` do geoportalu nie przechodzi) → zimny start (`am start -W`: 5,3 s, cała aplikacja na emulatorze) → **obraz cmentarza w z16 widoczny na zrzucie 1 s po starcie**. Przybliżanie do z19 i przesuwanie bez sieci działa, bez pustych kafelków wewnątrz ramki |
| Dopasowanie (GUGiK vs obrys OSM) | północna granica obrysu biegnie wzdłuż muru i krawędzi ulicy na zdjęciu, z rozbieżnością kilku metrów (ocena wzrokowa w z19). Siatka 3857 GUGiK = siatka `flutter_map` (M5) — **bez przeliczania układów** |
| Czego nie ma w paczce | `flutter_map` 8.3.2 i jego wbudowany `FileTileProvider` (kafelki `z/x/y.jpg` z katalogu aplikacji). Żadnej paczki do kafelków, żadnego klucza. Prototyp ma `INTERNET` wyłącznie do pobrania; wyświetlanie nie dotyka sieci |
| Pułapka prototypu | `CameraConstraint.contain` z ramką mniejszą od ekranu rzucał kamerę w inne miejsce (kafelki z Ukrainy w logu); `containCenter` i `minZoom 16` to naprawiają. Do zapamiętania przy ekranie mapy cmentarza |

**Widoczność na cmentarzu testowym (wstęp do M6):** w z19 tam, gdzie korony drzew się rozstępują, widać
aleje, rzędy nagrobków (jasne prostokąty) i kaplice. Pod zwartym drzewostanem widać same korony, a tak
wygląda większość Starych Powązek, czyli przypadek skrajny. **Archiwum z wiosny** (WMS `StandardResolutionTime`,
`TIME`=2016-04-30, 2019-04-30, 2022-04-30, 2025-11-01) na kafelku ze środka cmentarza: w 2016 są gałęzie bez
liści, ale grobów dalej nie widać. Na zwartym starodrzewie archiwum nie pomaga. Rozstrzyga M6 na cmentarzach
autora.

### M4 — regulamin Grobonetu (wejście do NT-004)
[Regulamin Grobonetu](https://grobonet.com/index.php?page=regulamin) (odczyt 2026-10-08, bez daty i wersji; operator:
*„Firma Artlook Gallery s.c.”*):
- **o linkowaniu nic nie mówi**, ani o linkach do konkretnych stron, ani o dostępie automatycznym;
- *„Dane zawarte w wyszukiwarce nie mogą być kopiowane lub wykorzystywane do celów innych niż informacji o
  osobach pochowanych”*;
- *„Właścicielami baz danych są urzędy miast, gmin i parafie”*.

**Wniosek:** regulamin nie zabrania linku do strony grobu i potwierdza zasadę **„link, nigdy kopia”** (W3).
Czy link do strony grobu jest trwały (adres z identyfikatorem), sprawdzi się dopiero na grobie z cmentarza
pokrytego Grobonetem, gdy autor sam go wyszuka (D2).

### Lista cmentarzy autora (D1)
Autor podał listę w czacie 2026-10-08: **N = 8 pozycji**. Jedna z nich to zespół czterech sąsiadujących
cmentarzy, więc razem **11 cmentarzy na 8 obszarach**. Liczba zgadza się z pomiarem z
[[ISSUE-014-home-map-of-poland]] (8 z 8); „10” z briefu było szacunkiem. Wszystkie 11 są we wbudowanej bazie
cmentarzy (punkt do pomiarów poniżej). Nazwy zostają w czacie.

### M6 — widoczność na cmentarzach autora (krok 3)
Dla każdego z 11 punktów 3×3 kafelki w z17 (przegląd) i w z19 (szczegół) z `StandardResolution`, w
scratchpadzie (usunięte w kroku 6), ocenione wzrokowo.

| Wynik | Obszary |
|---|---|
| **Rzędy grobów, pojedyncze nagrobki i aleje widoczne w z19** | **7 z 8** (10 z 11 cmentarzy). W tym zespół czterech cmentarzy ze starodrzewem, bo zdjęcie zrobiono wczesną wiosną, przed rozwinięciem liści |
| Zwarty drzewostan: groby tylko w prześwitach wzdłuż głównej alei | 1 z 8 |

- Zdjęcia różnych obszarów pochodzą z różnych nalotów (pora roku widać po liściach). Dla obszaru pod
  drzewostanem zapasem jest archiwum z wiosny (M5). Na Starych Powązkach archiwum nie pomogło, więc to
  sprawdzenie na przyszłość, a nie obietnica.
- **Bramka B nie zadziałała** (rzędy widać na więcej niż połowie obszarów), więc **M9 nie był potrzebny**.
  Wysoka rozdzielczość w EPSG:2180 zostaje niezmierzona.
- Zapytania o kafelki: 3 zerwane połączenia na ok. 220 (ok. 1,4%), co zgadza się z M7 (2,2%). Ponawianie jest
  konieczne.

### M8 — objętość dla cmentarzy autora (krok 5)
Obszar to ramka cmentarzy OSM z Nominatim (`boundingbox`; obrysów Nominatim w tych wynikach nie zwrócił, a
Overpass nie odpowiadał). Dla zespołu czterech cmentarzy to suma ich ramek. Rozmiar kafelka to średnia z19 z
M6 dla danego obszaru (7–11 KB).

| | z16–z19 |
|---|---|
| **Razem, 8 obszarów** | **ok. 1150 kafelków, ok. 10,5 MB** |
| Największy obszar | ok. 560 kafelków, ok. 5,3 MB |
| Najmniejszy obszar | ok. 40 kafelków, ok. 0,3 MB |
| Górna granica (kwadrat ±300 m na obszar) | ok. 260–290 kafelków i 2–2,8 MB na obszar |

Przy 2 zapytaniach na sekundę całość pobiera się w ok. 10 minut, a największy obszar w ok. 5 minut.

### M1–M3 — Grobonet, wyszukiwarka zarządcy, plan z kwaterami (krok 1)
Sprawdzane **tylko po nazwie cmentarza** (D2), bez szukania żadnej osoby. Robił to subagent; trzy kluczowe
twierdzenia `dev` sprawdził sam: strony map Grobonetu odpowiadają, strony parafii linkują do systemu zarządcy,
plan PDF istnieje.

| | 8 pozycji listy | 11 cmentarzy |
|---|---|---|
| **M1** — cmentarz w Grobonecie (także Grobonet PRO na domenie zarządcy) | 4 z 8 | 6 z 11 |
| **M2** — wyszukiwarka zarządcy poza Grobonetem | 5 z 8 | 5 z 11; zarządca linkuje ją w 3, a 2 znaleziono tylko w katalogu systemu |
| **Jakakolwiek wyszukiwarka grobów (M1 albo M2)** | **8 z 8** | **11 z 11** |
| **M3** — plan z oznaczonymi kwaterami w sieci | 5 z 8 | 8 z 11; pozostałe 3 mają tylko mapę ze zdjęcia z drona, bez oznaczeń kwater |

- Systemy, które znaleziono: Grobonet (i Grobonet PRO), [cmentarz.app](https://cmentarz.app) i
  [eCmentarze](https://www.ecmentarze.pl). Wszystkie **szukają po imieniu i nazwisku**.
- Wynik pokazuje adres grobu (sektor / rząd / numer albo numer grobu) i miejsce na mapie zarządcy. W cmentarz.app
  jest to zdjęcie z drona z obrysem grobu.
- Kanał offline to tylko ortofotomapa z M5. Wyszukiwarki i plany wymagają sieci.

**Co to zmienia dla luki 1** (`TRACEABILITY.md` → *Open gaps* 1, „jak znaleźć grób bez pinezki”): adres
zarządcy da się zdobyć **dla każdego cmentarza autora**. Autor sam szuka po nazwisku we własnej przeglądarce i
przepisuje sektor, rząd i miejsce do pól, które aplikacja już ma (`sector` / `row` / `plot`). Regulamin Grobonetu
dopuszcza użycie danych *„do celów… informacji o osobach pochowanych”* (M4). Aplikacja niczego nie kopiuje
(W3). Na miejscu do kwatery prowadzi plan (8 z 11), a ortofotomapa offline pokazuje rzędy (7 z 8 obszarów).

### M10 — kwatery w OpenStreetMap (po pytaniu autora na stopie #2)
Autor zapytał, czy da się pobrać *„plan tego cmentarza z zaznaczonymi prostokątami symbolizującymi kwatery (coś
ala geoportal tylko dla cmentarzy)”*. Najtańszy falsyfikator: OSM, jedyne publiczne źródło wektorowe z prawem
użycia offline (ODbL). Ma znacznik [`cemetery=sector`](https://wiki.openstreetmap.org/wiki/Tag:cemetery%3Dsector).
Zapytanie Overpass w ramkach 8 obszarów z M8:

| | 8 obszarów |
|---|---|
| kwatery (`cemetery=sector`) | **1 kwatera na 1 obszarze**; na 7 z 8 — **zero** |
| groby (`cemetery=grave`) | 2 (na 1 obszarze) |
| alejki i drogi (`highway=*` w ramce, razem z ulicami wokół) | są na każdym obszarze |

**Wniosek:** w OSM nie ma kwater na cmentarzach autora. Plany z kwaterami mają tylko zarządcy (M3: 8 z 11 w
sieci) w swoich systemach, a te nie pozwalają ich kopiować (M4) i nie działają offline.

### M11 — szkic planu schematycznego i alejki w OSM (po stopie #2)
Na prośbę autora (*„czy mógłbym to najpierw zobaczyć w tym emulatorze”*) prototyp dostał trzy tryby, wszystkie
offline:
- **„Jak u Ciebie”**: obrys i alejki z OSM w tokenach stylu B, czyli teren w kolorze powierzchni, alejki szerokie
  na 3 m w terenie, obrys w kolorze obrysu. Do tego trzy kwatery jako dane autora, z etykietą „Kwatera N”, i dwa
  wymyślone groby jako bursztynowe znicze;
- **„Pełny (OSM)”**: wszystkie 477 kwater cmentarza testowego z OSM;
- **„Zdjęcie”**: ortofotomapa z tymi samymi warstwami na wierzchu.

Dane cmentarza testowego pobrane z Overpass: obrys, 86 alejek, 477 kwater.

**Alejki w OSM wewnątrz ramek cmentarzy autora** (`highway` = footway, path, pedestrian, service, track, steps; środek
odcinka w ramce):

| | obszary |
|---|---|
| gęsta sieć alejek (83–220 odcinków) | 4 z 8 |
| pojedyncze alejki (3–7 odcinków) | 4 z 8 |

Na połowie cmentarzy autora plan będzie więc wyglądał jak szkic. Na drugiej połowie będzie to obrys z
pojedynczymi alejkami oraz kwatery i znicze autora.

**Overpass jako źródło w aplikacji:** w tej sesji publiczne instancje zwracały 504, 429 i 500, a w każdej serii
zapytań odpowiadała co najwyżej jedna instancja. Pobranie planu przy dodaniu cmentarza musi więc ponawiać i
pokazywać zaślepkę.

### H3 — status
**Częściowo potwierdzona, w innej postaci niż w briefie.**
- **Pozycji grobu z istniejących map nie da się przejąć**, bo map zarządców nie wolno kopiować i nie są offline.
- **Adres zarządcy jest osiągalny dla 11 z 11 cmentarzy**, plan z kwaterami dla 8 z 11, a zdjęcie z widocznymi
  rzędami dla 7 z 8 obszarów.
- Czy ręczna pinezka albo adres z planem wystarczy, żeby dojść do grobu, rozstrzygnie sprawdzenie na miejscu (D5 →
  §Parked).

**H10:** potwierdzona (M5, 0 zł).

### Rekomendacja do ADR-003
1. **Źródło:** ortofotomapa GUGiK, WMTS `StandardResolution`, EPSG:3857, z16–z19, z podpisem „Ortofotomapa: GUGiK”.
   Koszt 0 zł. Zapas na drzewostan: archiwum WMS `StandardResolutionTime`. Odrzucone z cytatem: Mapbox, Esri,
   Google, kafelki OSM (M5).
2. **Droga do telefonu (D6) — rekomendacja (b): aplikacja zostaje bez `INTERNET`.**
   - Obszary cmentarzy pobiera **narzędzie na PC** w `grobing-code/tool/`, tak jak wyciąg bazy cmentarzy z
     ISSUE-015. Narzędzie zapisuje **jeden plik** (ok. 10,5 MB dla 8 obszarów, ok. 10 minut pobierania, z
     ponawianiem nieudanych kafelków).
   - Aplikacja wczytuje ten plik systemowym oknem, tak jak kopię w [[ISSUE-009-restore]].
   - [[NFR-005-dane-nie-opuszczaja-telefonu]] dalej pilnuje system, a nie kod.
   - **Koszt:** krok na PC przy nowym cmentarzu i przy odświeżeniu ortofotomapy (co 2–5 lat).

   Alternatywa (a): `INTERNET` i pobieranie w aplikacji na dotknięcie. Jest wygodniejsza w drodze, ale od tej chwili
   NFR-005 pilnuje już tylko kod. **Wybór należy do autora** na stopie #2.
3. **Format pliku:** MBTiles (standard; to plik SQLite, który aplikacja odczyta istniejącym `sqlite3`, bez
   `flutter_map_mbtiles` i jego `sqlite3_flutter_libs` — M5). Wyświetlanie przez własny `TileProvider`.
   Prototyp potwierdził tylko wariant z plikami `z/x/y.jpg` (`FileTileProvider`).
4. **Plik obszarów to dane rodziny co do miejsca**, bo mówi, na których cmentarzach leży rodzina. Trzymany jest
   poza repo (`family_data_dir`, Dysk autora). **Pozycja, która go wprowadzi, dopisuje `*.mbtiles` do `.gitignore`
   trzech repo i do strażnika** (dziś go nie łapie: rozpoznaje `*.db` i `*.sqlite*`).
5. **Zdjęcia obszarów nie wchodzą do kopii.** Są publiczne i da się je pobrać albo wczytać ponownie, a kopia
   zostaje mała.
6. **Propozycja dla modelu danych** (`data-model.md`, *Cemetery*): pole „link do Grobonetu (jeśli jest)” →
   **„link do wyszukiwarki zarządcy”**, bo 5 z 11 cmentarzy autora ma wyszukiwarkę poza Grobonetem. Plan zarządcy
   jako źródło **pozycji** (`01_INBOX` → plany cmentarzy) się nie sprawdził, bo planów nie wolno przejąć do
   aplikacji. Plan służy na miejscu do odnalezienia kwatery z adresu. Decyzja autora.
7. **Pułapka dla ekranu mapy cmentarza:** `CameraConstraint.contain` przy ramce mniejszej od ekranu (M7).

## Verification
> `qa`, 2026-10-08. **DoD SPIKE:** odpowiedź zapisana · kod eksperymentu usunięty · status hipotezy
> zaktualizowany. Testów automatycznych nie ma, bo kod nie zostaje. Dowodem są pomiary, które `qa` sprawdzał
> sam, a nie na podstawie raportu `dev`.

### Exit → evidence, sprawdzone przez `qa`
| Warunek | Sprawdzenie `qa` | Wynik |
|---|---|---|
| Źródło z prawem offline | regulamin geoportalu i strona ortofotomapy przeczytane u źródła; pismo GGK otwarte (PDF) | ✅ (M5) |
| Koszt | jw. | ✅ 0 zł |
| **Działa bez zasięgu** | sam powtórzył na `Medium_Phone`: `airplane_mode_on` = 1, `ping 8.8.8.8` nie przechodzi, `force-stop` → zimny start (`TotalTime` 4,9 s) → obraz cmentarza testowego na zrzucie 1 s po starcie. Build z 2026-10-08 07:54, jedyne uprawnienie to `INTERNET` | ✅ (M7) |
| Widać to, czego potrzebuje autor | panele M6 obejrzane: rzędy widoczne na 7 z 8 obszarów + krok autora na stopie #2 | ✅ / czeka na autora |
| M1–M3 | raport subagenta; trzy twierdzenia sprawdzone ręcznie (`dev`) | ✅ (liczby) |
| Status H3, H10 | *Findings* → *H3 — status* | ✅ |

### Dane rodziny
- **Grep dodanych linii vaulta** (`git diff -U0`) po nazwach i miejscowościach z listy autora, po wezwaniach parafii,
  identyfikatorach i subdomenach systemów cmentarnych z raportu subagenta oraz po współrzędnych: **0 trafień**.
  Jedno fałszywe: „prze**świta**ch”.
- Pliki z nazwami i punktami cmentarzy autora (skrypty M6/M8, kafelki, panele) są **wyłącznie w scratchpadzie
  sesji**, poza repo, i do usunięcia w sprzątaniu. W repo nie ma nowych plików: `grobing-agents` i `grobing-code`
  są czyste, a w vaulcie zmieniły się 2 pliki pozycji.
- Prototyp zawiera tylko publiczny cmentarz testowy (obrys OSM, ODbL) i żadnych osób.

### Stop #2 — odpowiedź autora (2026-10-08)
- **D6 — decyzja autora: droga (a), z zasadą „offline najpierw”.** Cytat: *„chciałbym aby aplikacja mogła działać
  bez internetu ale jestem z tym ok że jak dodaje nowy cmentarz to do mapy potrzebny jest internet (a jeżeli go
  nie ma to jest tylko placeholder z informacją żeby go pobrać gdy internet będzie)”*. Wynika z tego:
  - aplikacja dostaje `INTERNET` **tylko do pobrania zdjęcia obszaru cmentarza**, przy dodaniu cmentarza;
  - bez sieci w tym miejscu jest zaślepka z informacją, żeby pobrać, gdy będzie internet;
  - cała reszta działa offline.

  Rekomendacja `dev` (b) odrzucona przez autora; jej koszt (krok na PC) autor uznał za większy niż koszt (a).
- **Nowy pomysł autora (poza zakresem spike'a):** *„można tam dodać kwatery ale ich lokalizacja będzie dostępna
  dopiero gdy będziemy mieć plan cmentarza”*. Kwatery jako rzecz w cmentarzu, wpisywane od razu, z położeniem
  dopiero po planie. To wejście do [[EPIC-002-wizyta]] i do `01_INBOX/2026-10-05-plany-cmentarzy.md` (siatka
  kwater); dopisuje je `docs`.
- **Kroki 1–2 (emulator):** stan urządzenia po pierwszej odpowiedzi bez zmian (ten sam widok, brak zapytań o
  z18–z19 w logu), więc niewykonane. Odczucie z19 sprawdził agent (M7, zrzuty).
- **Odczucie autora zamiast kroków 1 i 3:** *„zastanawiam się czy fotografia satelitarna to dobry plan, niestety
  mało co jest widoczne tutaj”*. Autor pokazał zrzut **planu pokazowego z Grobonetu**: obrys cmentarza, alejki,
  kwatery I–VIII z podpisami, każdy grób jako prostokąt, wejście główne. Komentarz: *„coś podobnego (tyle że w
  naszych kolorach) chciałbym mieć w aplikacji”*. Wynik: M10 (OSM nie ma kwater) i kierunek niżej. **Krok 2**
  (płynność przesuwania) bez odpowiedzi; pokrył go agent (M7: przesuwanie i przybliżanie offline bez pustych
  kafelków w ramce).
- **Wniosek dla ADR-003 i [[EPIC-002-wizyta]]:** autor chce **planu schematycznego**, a nie zdjęcia jako głównego
  widoku. Z czego da się go zbudować:
  - obrys cmentarza z OSM (ODbL, offline, jak baza w ISSUE-015);
  - alejki z OSM tam, gdzie są;
  - kwatery i groby autora jako **jego dane**, z położeniem zaznaczonym na zdjęciu.

  Zdjęcie GUGiK służy jako podkład do zaznaczania i jako warstwa do włączenia. **Wszystkich grobów jak w Grobonecie
  nie będzie**, bo to dane zarządców (M4).
- **Po szkicu na emulatorze (M11)** autor przybliżył tryb „Zdjęcie” do kwatery i przysłał zrzut, więc obejrzał
  prototyp. Jego odpowiedzi:
  - *„tak ten widok "jak u Ciebie" jest tym co chciałbym mieć”*;
  - *„widzę że źle myślałem o kwaterach”*: kwatera to sektor z kilkunastoma albo kilkudziesięcioma grobami
    (`glossary.md` → *kwatera* już to mówi);
  - *„mając plan cmentarza — wiem w której kwaterze jest mój grób a potem (jeżeli nie ma tam podziału na siatkę
    grobów) to zaznaczyłbym pinezką gdzie jest grób”*;
  - *„Myślę aby mieć tylko ten widok "jak u Ciebie" w wersji offline a zdjęcie żeby mieć tylko gdy jest internet”*,
    z obawą, że zdjęcia zrobią aplikację *„zbyt ciężką”*.

  **Siatki grobów** nie da się mieć z publicznych danych: w OSM są 2 groby na 8 obszarach (M10), a zarządcy nie
  pozwalają kopiować (M4). Odpowiedź agenta na „ciężar”: zdjęcia wszystkich 8 obszarów to ok. 10,5 MB (M8), czyli
  ciężaru nie robią. Podział autora jest jednak spójny z jego przepływem:
  - kwatery i pinezki zaznacza w domu, przy sieci, ze zdjęciem i planem zarządcy;
  - na miejscu wystarczą plan offline i GPS.

  Decyzja jest odwracalna: zapis zdjęcia w telefonie da się dołożyć później, bo M7 pokazał, że działa.
- **Kierunek do ADR-003 — decyzje autora na stopie #2:**
  1. **plan schematyczny offline** z OSM: obrys i alejki pobierane przy dodaniu cmentarza (`INTERNET`), z
     podpisem „© OpenStreetMap”. Bez sieci zaślepka „pobierz, gdy będzie internet”;
  2. **ortofotomapa GUGiK tylko online**, jako warstwa do włączenia, bez zapisu w telefonie;
  3. **kwatery i groby to dane autora:** kwatera jako nazwana strefa zaznaczona przez autora, a grób jako pinezka w
     kwaterze, z adresem zarządcy (kwatera, rząd, miejsce). Siatki grobów nie ma.

  Rekomendacja `dev` z *Findings* (zdjęcie offline, droga (b)) jest przez to nieaktualna; zostaje jako historia.
- **Pole „link do wyszukiwarki zarządcy”** (propozycja 6) zostało bez odpowiedzi. Przechodzi do pozycji z ekranem
  cmentarza, bo to pole cmentarza.

### Werdykt `qa`: APPROVED (self-check, z uwagami)
Warunek wyjścia jest spełniony: źródło z uzasadnieniem i kosztem dla ADR-003, zmienione decyzją autora na stopie
#2 (plan OSM offline + ortofotomapa online), oraz status H3 i H10. Uwagi:
1. Kierunek ADR-003 różni się od pytania spike'a („zdjęcie offline dla 10 obszarów”). To decyzja autora, a
   pomiary M5–M8 zostają jako uzasadnienie odrzuconej i odwracalnej opcji;
2. Overpass jako źródło planu w aplikacji jest zawodny (M11), więc ponawianie i zaślepka są warunkiem, a nie
   ozdobą;
3. przegląd `ui` niepotrzebny: spike nie zmienia ekranów aplikacji. Wygląd planu projektuje `ui` w pozycji
   EPIC-002.

### Czego nie sprawdzono
- przyczyny 14 błędów pobrania w prototypie (build release bez `run-as`), choć skala zgadza się z M6;
- formatu MBTiles i wczytania pliku systemowym oknem: rekomendacja (pkt 3) stoi na kanonie i na
  [[ISSUE-009-restore]], nie na pomiarze;
- wysokiej rozdzielczości w EPSG:2180 (M9, bramka B się nie uruchomiła);
- czy adresy z wyszukiwarek prowadzą do grobu na miejscu (D5 → §Parked).
