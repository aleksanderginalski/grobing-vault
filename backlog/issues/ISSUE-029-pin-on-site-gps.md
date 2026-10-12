---
title: "ISSUE-029 — Pin a grave on site: „gdzie jestem” with the blue dot and accuracy circle, pin mode starting at the GPS dot and moved by a tap on the plan, „Postaw pinezkę” and „Popraw pinezkę”, the pin saved with source, accuracy and date"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-002-wizyta]]"
user-story: "[[US-008-pinezka-na-miejscu]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-12
verdict-reviewer: self-check
source: "rozpisanie US-008 (`docs` w auto-flow po `pm`, autor: „Tak”, 2026-10-12) · US-008 AC-1–AC-4 · [[cmentarz]] elementy 10–14, stan D, D15, D16 · [[grob]] v5.1 · [[SPIKE-004-mvp-flow-prototype]] D22 · H3"
created: 2026-10-12
updated: 2026-10-12
---

# ISSUE-029 — Pinezka na miejscu

> Z rozpisania [[US-008-pinezka-na-miejscu]] (`docs` w auto-flow, 2026-10-12, po `pm`). **Jedna pozycja na całą US.** Wszystkie
> cztery AC dzieją się w jednym trybie mapy (stan D) i sprawdza je jedna wizyta z telefonem. Prototyp SPIKE-004 ten przepływ
> pokazał (panel 7, D22, autor: *„5. ok”*), więc nie ma części, której nikt nie widział, jak kwatery przy US-007. Podział
> zaproponował łańcuch, nie autor, więc na stopie #1 autor może go zmienić.
>
> **Cel autora (2026-10-12, `/pm`: „Tak”):** build release na telefonie autora **przed zaduszkami (~2026-11-02)**. Jedna wizyta
> da wtedy dwie rzeczy: pomiar z `CURRENT_STATE.md` → *Parked* (H3, H9) i sprawdzenie AC-1 oraz AC-4 w terenie.

## What to build
1. **„Gdzie jestem”** ([[cmentarz]] element 10, D15): przycisk na planie, niebieska kropka, koło dokładności, plakietka
   „tu jesteś · ±N m”. Lokalizacja działa tylko po dotknięciu. Pierwsze użycie → systemowe pytanie o uprawnienie, a odmowa →
   komunikat i ręczne stawianie pinezki.
2. **Tryb stawiania pinezki** (stan D, element 12, D16): karta „Stań przy grobie…”, znicz w obrysie w kropce, dotknięcie planu
   przesuwa znicz, „Anuluj” · „Zapisz pinezkę”. Bez uprawnienia albo bez sygnału znicz stawia się dotknięciem planu.
3. **Wejścia do trybu D:** „Postaw pinezkę” w [[grob]] (grób bez pinezki, v5.1) i „Popraw pinezkę” w stanie B ([[cmentarz]]
   element 11).
4. **Pinezka zapisana ze źródłem, dokładnością i datą** (element 14). [[grob]] v5.1 pokazuje to pod adresem: „Pinezka: GPS ±4 m ·
   08.10.2026”. Pozycja, źródło i dokładność mają kolumny od v1 (`graves.lat`/`lon`/`position_source`/`position_accuracy_m`).
   **Daty pinezki w schemacie nie ma**, więc potrzebna jest zmiana schematu.
5. **Próg „słaby sygnał”** (element 12, dziś „gorsza niż 15 m”) wchodzi **tymczasowo**, jako jedna stała. Poprawimy go po pomiarze
   na cmentarzu (decyzja autora 2026-10-12).
6. **Bez internetu** (AC-4): kropka i stawianie pinezki działają na planie offline, a „Zdjęcie” bez sieci zachowuje się jak w
   [[US-007-mapa-cmentarza]].

## Acceptance Criteria
- [ ] **US-008 AC-1 — gdzie jestem.** *When* dotykam „gdzie jestem” na planie *Then* widzę niebieską kropkę i koło dokładności.
      Pierwsze użycie pyta o uprawnienie lokalizacji, a odmowa zostawia ręczne stawianie.
- [ ] **US-008 AC-2 — postaw pinezkę.** *Given* grób bez pinezki *When* w widoku grobu dotykam „Postaw pinezkę” *Then* mapa pokazuje
      pinezkę w kropce, dotknięcie planu ją przesuwa, a „Zapisz pinezkę” zapisuje ją z dokładnością i datą.
- [ ] **US-008 AC-3 — popraw pinezkę.** *Given* grób z pinezką *When* w arkuszu grobu dotykam „Popraw pinezkę” *Then* wchodzę w ten
      sam tryb dla tego grobu.
- [ ] **US-008 AC-4 — bez internetu.** *Given* tryb samolotowy *Then* „gdzie jestem” i stawianie pinezki działają na planie offline.
- [ ] Pinezka z datą wraca po odtworzeniu z kopii (odcisk danych zgodny, [[NFR-002-odtworzenie-na-nowym-telefonie]]).

## Out of scope
- Plan, kwatery i stany A, B, C → [[US-007-mapa-cmentarza]] (zrobione).
- „Pokaż kwaterę” przy grobie bez pinezki i lista grobów kwatery ([[cmentarz]] D29) → [[ISSUE-030-sector-on-a-visit]] (`draft`,
  decyzja autora na stopie #1 tej pozycji).
- Znicze sąsiednich grobów, które nachodzą na siebie ([[cmentarz]] *Open*: znicz z liczbą otwiera arkusz z listą) → kandydat w
  [[ISSUE-030-sector-on-a-visit]].
- Wysyłanie pozycji poza telefon w jakiejkolwiek postaci ([[NFR-005-dane-nie-opuszczaja-telefonu]]).

## Notes
- **Data pinezki to zmiana schematu (v12)**: migracja, test migracji i próbne odtworzenie. Jeśli zmiana wyjdzie poza jedną kolumnę,
  to kandydat na ADR.
- **Źródło pinezki to nie źródło faktu.** Elementy 12 i 14 w [[cmentarz]] linkują [[FR-001-provenance]], wycofane w SPIKE-004 D28.
  Źródło pinezki (`PositionSource`: `gps`, `satellite`) jest osobnym polem grobu ([[data-model]] → Grave), więc D28 go nie dotyczy.
  Link w specyfikacji poprawia `ui`.
- **Do ustalenia przed planem (`ui`):**
  - (a) pinezka z GPS przesunięta dotknięciem — jakie źródło i jaka dokładność zostają w zapisie?
  - (b) jakie źródło ma pinezka postawiona ręcznie na planie? Enum zna `gps` i `satellite`, a [[cmentarz]] 14 mówi „zaznaczona w
    domu (z planu lub zdjęcia z góry)”;
  - (c) gdzie się dotyka w trybie D — na makiecie, nie tylko co widać (kandydat z *Do retro*, ISSUE-024).
- **Do sprawdzenia w źródłach przez `planning` (*Prior art*):**
  - czym jest liczba z `Location.getAccuracy()` na Androidzie (promień przy jakiej pewności), bo od tego zależy, co znaczy koło
    dokładności i próg;
  - pakiet lokalizacji zgodny z przypiętym Flutterem 3.41.1 ([[ADR-002-flutter-pinned]]);
  - uprawnienia lokalizacji na Androidzie 12+ (lokalizacja dokładna albo przybliżona) i co aplikacja robi przy „przybliżonej”;
  - czy dostawca lokalizacji (Google Play Services albo systemowy `LocationManager`) wysyła coś poza telefon
    ([[NFR-005-dane-nie-opuszczaja-telefonu]]).
- **Emulator:** pozycję podaje się komendą `adb emu geo fix <lon> <lat>`. Punkt bierzemy z bazy aplikacji, nie z pamięci (*Do retro*,
  ISSUE-027). Przejście AC-1–AC-4 na emulatorze robi agent przed stopem #2.
- **Krok w terenie (propozycja łańcucha, do przyjęcia na stopie #1):** GPS na miejscu i offline na cmentarzu sprawdzi tylko telefon
  (wyjątek w `DEFINITION_OF_DONE.md`, wyłącznie build release). Krok w terenie **nie blokuje zamknięcia**, tak jak test w słońcu w
  ISSUE-027. `qa` zapisuje go w *Parked* z warunkiem obudzenia „wizyta na cmentarzu”, razem z pomiarem H3 i H9.
- **Telefon przed MVP:** build release podpisany kluczem wydania, tym samym co MVP, więc MVP wejdzie później jako aktualizacja.
  Na telefonie są tylko wymyślone dane. Przed prawdziwymi danymi trzeba je wyczyścić (prawdziwe dane dopiero po instalacji MVP —
  decyzja autora 2026-10-08).

## Implementation plan
> `planning`, 2026-10-12. Specyfikacja (`ui`, przed planem): [[cmentarz]] v7 — elementy 10, 10a, 11, 12, 12a, 14, *States* v7, D31–D37,
> *Open* (P1/P2); [[grob]] v7 — element 4, D14; [[style-b]] *State colours* (kropka „tu jesteś”, v1.16). Klikalny prototyp:
> `issue-029-pinezka.html` (katalog tymczasowy sesji `8b388e89-…`), panele 1–4. **Kandydaci tego, co widać** (retro 2, R6): P1 i P2
> działają na prototypie (panele 2–4, przełącznik).

### Prior art
- **Co znaczy liczba dokładności** — `Location.getAccuracy()` (AOSP, `core/java/android/location/Location.java`): *„Returns the
  estimated horizontal accuracy radius in meters of this location at the 68th percentile confidence level. This means that there is a
  68% chance that the true location of the device is within a distance of this uncertainty of the reported location.”* Koło dokładności
  to więc „zwykle”, a nie „na pewno”: przy „±5 m” prawdziwa pozycja w co trzecim odczycie leży dalej. Dlatego próg słabego sygnału
  (D37) ustawi pomiar, a nie specyfikacja.
- **Uprawnienia** ([Android — Request location access at runtime](https://developer.android.com/develop/sensors-and-location/location/permissions/runtime)):
  - na Androidzie 12+ *„request both the `ACCESS_FINE_LOCATION` permission and the `ACCESS_COARSE_LOCATION` permission in a single
    runtime request”*; okno systemu daje do wyboru „Precise” albo „Approximate” i „While using the app” · „Only this time” · „Deny”;
  - *„If the user downgrades your app's location access from precise to approximate […] the system restarts your app's process”*;
  - przybliżona: *„accurate to within about 3 square kilometers”* ([Location permissions](https://developer.android.com/develop/sensors-and-location/location/permissions)),
    czyli na cmentarzu bezużyteczna — stąd stan 10a (c) bez kropki;
  - od Androida 11 druga odmowa działa jak „nie pytaj więcej” i okno się już nie pokazuje ([Android 11 — permission updates](https://developer.android.com/about/versions/11/privacy/permissions)).
    Droga dalej prowadzi wtedy przez ustawienia aplikacji.
- **Skąd pozycja** (AOSP, `LocationManager.java`): `GPS_PROVIDER` *„determines location using GNSS satellites”*; `NETWORK_PROVIDER`
  *„based on nearby of cell tower and WiFi access points. Operation of this provider may require a data connection”*; `FUSED_PROVIDER`
  *„may combine inputs from several other location providers”*. „Dokładność lokalizacji Google” (ustawienie telefonu): *„Google
  periodically collects information about sensors and wireless signals near you”* ([Pomoc Androida](https://support.google.com/android/answer/3467281)).
- **Pakiety:** [`geolocator`](https://pub.dev/packages/geolocator) 14.1.1 korzysta z *„FusedLocationProviderClient or if not available
  the LocationManager”* i ma opcję `forceLocationManager`. Ciągnie sześć pakietów platform (android, apple, linux, web, windows,
  interfejs), a `geolocator_android` dokłada `com.google.android.gms:play-services-location:21.2.0` (jego `build.gradle`). Dziś
  aplikacja nie ma żadnej zależności od usług Google (`pubspec.yaml`: „No Firebase, analytics…”).
- **Z kodu** (ankieta 2026-10-12):
  - `graves.lat`/`lon`/`position_source`/`position_accuracy_m` są od v1, `PositionSource { satellite, gps }`, **daty pinezki nie ma**.
    Pozycję zapisuje dziś tylko `lib/dev/fictional_data.dart` (debug), więc na danych autora żaden grób nie ma pinezki;
  - schemat **v11** (`currentSchemaVersion`); kopia, odcisk i „Stan danych” biorą kolumny z `sqlite_master` — nowa kolumna wchodzi do
    kopii bez zmian w `backup_*`;
  - **własne kanały Kotlin** (`ExternalLinks.kt`, `PhotoPreparation.kt`, `BackupDocuments.kt`) z cienką nakładką w Dart
    (`external_link.dart`) — wzorzec dla lokalizacji; `minSdk` 24, więc `LocationManager.isLocationEnabled()` (API 28) potrzebuje
    drogi dla 24–27 (`isProviderEnabled(GPS_PROVIDER)`);
  - tryb F (`sectors_screen.dart`) ma celownik i `_toCrosshair` (dotknięcie planu → płynny przesuw pod celownik) — P2 to ten sam
    mechanizm; `CemeteryPlanMap` ma `onMapTapAt`, `candlesDimmed`, nakładki;
  - `GraveScreen` otwiera się zawsze z ekranu cmentarza (`_openGrave`), więc wynik „pinezka zapisana” może wrócić przez dwa ekrany.
- **Emulator:** pozycję podaje `adb emu geo fix <lon> <lat>`. **Dokładności ta komenda nie ustawia**, więc słaby sygnał sprawdzają
  testy widżetów, a nie emulator. Punkty bierzemy z bazy aplikacji, nie z pamięci (*Do retro*, ISSUE-027).
- **Pułapki z poprzednich pozycji:** semantyka przycisków (`Semantics` z `onTap` i `container`; sześć instancji), cel dotyku 48 dp
  pigułek (ISSUE-028, MAJOR), tekst 200% i 360 dp przed `qa` (R5), logcat bez współrzędnych (ISSUE-027 F5), `python -` w Bashu wisi.
  **Komendy git tylko do odczytu** — rozmiar zmian: `git diff --stat` i `git status --short` (incydent ISSUE-028).

### Stop #1 (2026-10-12) — autor: „ok”
Rekomendacja przyjęta w całości: D1 = **P2** (celownik, plan pod zniczem), D2 = **A** (własny kanał na `GPS_PROVIDER`, bez nowej
zależności; ADR-017 pisze łańcuch), D3 (schemat v12: data pinezki, źródło `plan`), D4 (krok w terenie nie blokuje zamknięcia; build
release na telefon przed ~2026-11-02 osobnym krokiem), D5 ([[ISSUE-030-sector-on-a-visit]] czeka na wizytę), D6 (jedna pozycja).
Decyzje projektowe [[cmentarz]] D31–D33, D35–D37, [[grob]] D14 i komunikat [[osoba]] D9 potwierdzone. Wariant rekomendowany w
*Scope — files* obowiązuje bez zmian.

### Decisions for stop #1 (rekomendacja → „tak” przyjmuje wszystkie)
- **D1 — gdzie się dotyka w trybie D** ([[cmentarz]] *Open*, D34; prototyp, panele 2–4):
  - **P2 — celownik, plan pod zniczem (rekomendacja `ui`):** ten sam ruch co rysowanie kwatery (K1, Twój wybór), palec nie zasłania
    miejsca, idąc z telefonem nie przestawisz pinezki przypadkiem, plan idzie za kropką; dotknięcie miejsca przesuwa je pod znicz.
    Koszt: przy dużej poprawce przesuwasz plan zamiast dotknąć;
  - **P1 — dotknięcie przesuwa znicz** (prototyp SPIKE-004, wskazanie cmentarza): jedno dotknięcie na poprawkę. Koszt: opuszka przy
    z19 zasłania ok. 8–9 m planu — tyle, ile sama poprawka GPS.
- **D2 — skąd aplikacja bierze pozycję** → **[[ADR-017-location-from-gnss-only]]** (pisze łańcuch, `docs` przy zamknięciu; nowa decyzja, nie zastępuje żadnej):
  - **A — własny kanał na `LocationManager.GPS_PROVIDER` (rekomendacja):** sam GNSS, bez nowej zależności i bez usług Google, wzorzec
    istniejących kanałów. Koszt: ok. 150–250 linii Kotlin i Dart (uprawnienia, strumień, ustawienia). W budynku pozycji zwykle nie
    będzie („Szukam pozycji…”) — na cmentarzu to bez znaczenia, a w domu i tak stawia się ręcznie;
  - **B — `geolocator` z `forceLocationManager`:** mniej własnego kodu. Koszt: `play-services-location` w APK i sześć pakietów do
    przypięcia i przeglądu (NFR-005), zgodność z Flutterem 3.41.1 do sprawdzenia;
  - **C — `geolocator` z Fused (usługi Google):** pierwsza pozycja szybciej (Wi-Fi, maszty). Koszt: jak B, a pozycja zależy od usług
    Google i ich ustawienia „Dokładność lokalizacji”. Na otwartym cmentarzu przewaga znika, bo i tak liczy GNSS.
- **D3 — schemat v12:** kolumna `graves.position_recorded_at` (data i czas, `NULL` = bez daty) i wartość `plan` dopisana na końcu
  `PositionSource` (zapis po nazwie, więc stare wiersze bez zmian). `_from11To12` to sam `addColumn`. Pinezki sprzed v12 (tylko debug)
  zostają bez daty, a linia źródła pokazuje je bez „· data” ([[cmentarz]] 14). Bez ADR — wiersz w [[data-model]] (`docs`).
- **D4 — krok w terenie nie blokuje zamknięcia** (propozycja z rozpisania): `qa` zapisuje go w `CURRENT_STATE.md` → *Parked* z
  warunkiem „wizyta na cmentarzu”, razem z pomiarem H3/H9. **Build release na Twoim telefonie przed ~2026-11-02** to osobny krok
  po zamknięciu: README dostaje instrukcję, a instalację robisz Ty albo agent przez `adb`, gdy podłączysz telefon. Na telefonie są
  wtedy tylko wymyślone dane, a przed prawdziwymi trzeba je wyczyścić.
- **D5 — [[ISSUE-030-sector-on-a-visit]] (`draft`):** rekomendacja — **czeka na wizytę**. Kandydaci 2 i 3 mają warunek z terenu, a
  kandydata 1 („Pokaż kwaterę”) zastępuje na razie D32 (pinezka bez kropki startuje w strefie kwatery grobu) i nazwy stref na planie.
  Wizyta pokaże, czy to wystarcza. *Inaczej:* „Pokaż kwaterę” jako mała pozycja zaraz po tej.
- **D6 — jedna pozycja.** *Obali:* `dev` nie zamknie jej w jednej sesji → podział na **029** (kanał, kropka, „gdzie jestem”, 10a) i
  **029b** (tryb D, v12, zapis). Decyzja przy pierwszej oznace.
- **Decyzje projektowe ze specyfikacji** (do potwierdzenia tym samym „tak”): [[cmentarz]] D31 (trzy stany ◎, plan jedzie do kropki),
  D32 (D włącza lokalizację, start w strefie kwatery), D33 (źródło = skąd pozycja), D35 (poprawa od zapisanej), D36 (D jak F; po
  zapisie mapa z grobem), D37 (próg tymczasowy 15 m); [[grob]] D14 („Postaw” tak, „Popraw” nie). **Spoza AC US-008, zapisane
  wcześniej:** komunikat z [[osoba]] D9 przy „Pochówku” grobu bez pinezki.

### Scope — files (`{code}`, wariant rekomendowany: P2, D2 A)
| Plik | Co |
|---|---|
| `android/app/src/main/AndroidManifest.xml` | `ACCESS_FINE_LOCATION` i `ACCESS_COARSE_LOCATION` z komentarzem (tylko na ekranie cmentarza, tylko GNSS, nic nie wychodzi) |
| `android/.../HereLocation.kt` (nowy) | `MethodChannel` `grobing/location`: `access` (dokładna · przybliżona · odmowa · zablokowana — po odmowie bez `shouldShowRequestPermissionRationale` · plus „lokalizacja w telefonie włączona”), `request` (FINE i COARSE w jednym żądaniu, wynik z `onRequestPermissionsResult`), `openAppSettings`, `openLocationSettings`; `EventChannel` `grobing/location/fixes`: `GPS_PROVIDER`, `requestLocationUpdates` co ok. 1 s **tylko przy subskrypcji**, `removeUpdates` przy anulowaniu, wysyła szerokość, długość, dokładność (gdy `hasAccuracy`). **Bez logowania pozycji** |
| `MainActivity.kt` | rejestracja kanału; `onRequestPermissionsResult` → `HereLocation` |
| `lib/app/grave/here_location.dart` (nowy) | nakładka na kanał (`HereLocation`, `HereFix`, `HereAccess`) z wersją do podmiany w testach (jak `photo_preparer.dart`); `const double weakSignalM = 15` — **jedna stała**, z komentarzem „tymczasowa do pomiaru (cmentarz D37)”; „w obrysie z marginesem” i odległość do środka obrysu (bez planu — punkt cmentarza) |
| `lib/data/database.dart` | `PositionSource.plan` (na końcu); `Graves.positionRecordedAt`; **schemat v12**, `_from11To12` z komentarzem w stylu poprzednich kroków |
| `drift_schemas/grobing/drift_schema_v12.json`, `database.steps.dart`, `test/drift/grobing/generated/*` | `dart run drift_dev make-migrations` (README → *Baza danych*) |
| `lib/data/graves.dart` | `GravePin` (punkt, źródło, dokładność, data) w `GraveSummary` i `GraveDetail` zamiast samego punktu; `setGravePin(graveId, point, source, accuracyM)` — data zapisu z zegara w tej samej transakcji, dokładność tylko przy `gps` |
| `lib/app/polish.dart` | `pinSourceText` — „GPS ±4 m · 12.10.2026”, „postawiona na planie · …”, „postawiona na zdjęciu z góry · …” (metry całkowite; bez daty bez „· data”) |
| `lib/app/theme.dart` | `GrobingColors.here` (`#5EA2E6`) z rolą z [[style-b]] |
| `lib/app/grave/cemetery_plan_map.dart` | warstwa „tu jesteś”: koło w metrach (krycie 18%), kropka 16 dp z obwódką 2 dp w kolorze tła, plakietka 12 sp do 1,3× (bez niej w D) — poza czytnikiem; znicz w obrysie jako znacznik (P1) |
| `lib/app/grave/map_chrome.dart` | przycisk „gdzie jestem” (trzy stany, opis ze stanem), plakietka 10a, pasek komunikatu z akcją |
| `lib/app/grave/pin_screen.dart` (nowy) | **tryb D** (12, 12a) jako trasa, jak `SectorsScreen`: pasek z ✕, karta, plan w warstwie z poprzedniego stanu, przygaszone znicze, kropka, ◎ nad panelem, panel ze źródłem, słabym sygnałem, „Anuluj” · „Zapisz pinezkę”; P2 — znicz w obrysie na środku wolnego miejsca, plan idzie za kropką, przesunięcie albo dotknięcie (płynny przesuw jak `_toCrosshair`) → ręcznie; start (D32), poprawa (D35); błąd zapisu; wynik `PinSaved(graveId)`. Teksty dosłownie ze specyfikacji |
| `lib/app/grave/cemetery_screen.dart` | ◎ i kropka w A i B, 10a; pigułka „Popraw pinezkę” w B (pole dotyku 48 dp, jak „Kwatery”) → `PinScreen`; wynik z `_openGrave` i z `PinScreen` → B z tym grobem i kadrem na zniczu; komunikat z [[osoba]] D9; subskrypcja lokalizacji kończy się przy wyjściu |
| `lib/app/grave/grave_screen.dart` | element 4: „Postaw pinezkę” (z obrysem, 48 dp) albo linia „Pinezka: …”; po `PinSaved` → `pop` z wynikiem |
| `lib/dev/fictional_data.dart` | tylko debug: pinezki z datą, jedna `plan` |
| `README.md` (`grobing-code`) | *Baza danych*: v12; *Lokalizacja*: kanał, `adb emu geo fix`, brak dokładności na emulatorze; **build release na telefon przed wizytą** i czyszczenie danych przed prawdziwymi |

Bez zmian: `backup_*`, `restore_*`, `data_stamp.dart` (kolumny z `sqlite_master`), `lib/net/*` (żadnego nowego adresu), `pubspec.yaml`
(wariant A).

**Gdy autor wybierze inaczej:** P1 — znicz w obrysie jako znacznik w miejscu dotknięcia (`onMapTapAt`), bez nakładki i bez
podążania planu; przeciągnięcie przesuwa tylko plan. D2 B albo C — `geolocator` przypięty dokładnie (z pakietami platform) w
`pubspec.yaml`, przegląd zależności w NFR-005, bez `HereLocation.kt`.

### AC → implementation → test (testy pisze `qa`)
| AC | Gdzie | Test happy-path |
|---|---|---|
| US-008 AC-1 — gdzie jestem | `here_location.dart`, `HereLocation.kt`, `map_chrome.dart`, `cemetery_plan_map.dart`, `cemetery_screen.dart` | widżet z udawaną lokalizacją: ◎ → prośba o zgodę → zgoda → kropka, koło, „tu jesteś · ±5 m”, plan na kropce, ◎ w kolorze kropki; przesunięcie → `location_searching`; ◎ → wraca; ◎ → wyłącza; pozycja poza obrysem → „poza cmentarzem · 2,5 km”, kadr bez zmian; odmowa → „Bez zgody na lokalizację pinezki postawisz tylko ręcznie.”; przybliżona → 10a (c), bez kropki |
| US-008 AC-2 — postaw pinezkę | `pin_screen.dart`, `graves.dart`, `grave_screen.dart` | danych: `setGravePin` z GPS → pozycja, `gps`, dokładność, data; z ręki → `plan` / `satellite`, bez dokładności; widżet: grób bez pinezki → „Postaw pinezkę” → D z GPS (znicz w kropce, „Pinezka: GPS ±5 m”) → nowa pozycja → pinezka idzie za nią → przesunięcie planu → „postawiona na planie” → „Zapisz pinezkę” → stan B z nowym zniczem; w [[grob]] linia źródła z datą; dokładność 25 m → „Słaby sygnał: ±25 m…”, zapis możliwy |
| US-008 AC-3 — popraw pinezkę | `cemetery_screen.dart`, `pin_screen.dart` | widżet: znicz → B → „Popraw pinezkę” → D w zapisanym miejscu, „Teraz: …”, „Zapisz pinezkę” nieaktywny → ◎ → kropka, „Po zapisie: GPS…” → zapis → B |
| US-008 AC-4 — bez internetu | `cemetery_screen.dart`, `pin_screen.dart` | widżet: sieć niedostępna, plan z bazy → ◎ i D działają, zapis bez sieci; „Zdjęcie” → 13 |
| ISSUE-029 — pinezka z datą po odtworzeniu | `database.dart`, kopia bez zmian | odtworzenie: kopia v12 z pinezką GPS i datą → odtworzenie → ta sama pinezka, źródło, dokładność, data; odcisk zgodny |
| [[osoba]] D9 (spoza AC) | `cemetery_screen.dart` | widżet: „Pochówek” grobu bez pinezki → C z zaznaczonym grobem i komunikatem |

Testy do przepisania: `database_test.dart` i `data_state_screen_test.dart` (wersja 11 → 12), testy, które budują `GraveSummary` z
`pin` (nowy `GravePin`), `cemetery_screen_test.dart` (◎, pigułka w B). Test na źródłach: `HereLocation.kt` bez `Log.` z pozycją.

### Data layer
- **Schemat v12** (D3) z **testem migracji v11→v12 na danych** (`testWithDataIntegrity`, NFR-003): groby z pinezką `gps` i
  `satellite` oraz bez pinezki → po migracji te same pozycje, źródła i dokładności, data `NULL`, liczba grobów bez zmian.
- **Próbne odtworzenie:** test — kopia v11 z pinezką odtwarza się w v12 (data `NULL`); kopia v12 z pinezką i datą → to samo, odcisk
  zgodny. Na emulatorze: kopia z `Medium_Phone` (nowe hasło testowe) → `Grobing_Restore` — pinezka, linia źródła i data są (agent).
- **Źródło i status faktu:** ta pozycja **nie zapisuje faktów o rodzinie**. Pinezka to dane miejsca, a jej źródło (`PositionSource`)
  to pole grobu, nie [[FR-001-provenance]] (wycofane, SPIKE-004 D28).
- **Dane rodziny:** pinezki tylko na wymyślonych grobach; pozycje dla `adb emu geo fix` z punktu publicznego cmentarza testowego w
  bazie aplikacji. **Pozycja telefonu nigdy w logu** — przy prawdziwym użyciu to miejsce, gdzie leży rodzina (NFR-005, ISSUE-027 F5).
- **NFR-005:** wariant A bez nowej zależności; `aapt` na APK release: nowe uprawnienia tylko `ACCESS_FINE_LOCATION` i
  `ACCESS_COARSE_LOCATION`; logcat po przejściu: 0 linii ze współrzędnymi podanymi emulatorowi.
- **ADR-017** (D2), wiersz *Grave* w [[data-model]] (v12: data pinezki, źródło `plan`), słowniczek → *pinezka* (trzy źródła i data) →
  `docs` przy zamknięciu.

### Manual verification
**Agent na emulatorze** (zrzuty przed stopem #2):
1. `Medium_Phone`, build release jako aktualizacja na danych testowych v11: dane całe, „Stan danych” — v12.
2. Cmentarz z planem, `adb emu geo fix` w środku jego obrysu: ◎ → okno systemu → „Dokładna”, „Podczas korzystania z aplikacji” →
   kropka, koło, plakietka, plan jedzie; przesunięcie → ikona „plan odsunięty”; ◎ → wraca; ◎ → wyłącza. Punkt kilka km dalej →
   „poza cmentarzem · N km”. Zgoda „Przybliżona” → 10a (c). Dwie odmowy → komunikat i ustawienia aplikacji. Lokalizacja wyłączona w
   systemie → pasek z „Włącz”.
3. Grób bez pinezki → „Postaw pinezkę” → D (P1 albo P2 wg D1): pinezka w kropce, zmiana `geo fix` → idzie za nią; poprawka ręką →
   „postawiona na planie”; „Zapisz pinezkę” → B z nowym zniczem → „Pokaż grób” → „Pinezka: … · data”. To samo na „Zdjęciu” →
   „postawiona na zdjęciu z góry”. W domu (punkt daleko) → start w strefie kwatery grobu.
4. B → „Popraw pinezkę” → start w zapisanym miejscu, „Zapisz pinezkę” nieaktywny → ◎ → kropka → zapis.
5. Tryb samolotowy: kropka i D działają, „Zdjęcie” → „bez internetu”. Z osoby → „Pochówek” grobu bez pinezki → komunikat D9.
6. `uiautomator`: ◎ (opis ze stanem), „Popraw pinezkę”, „Postaw pinezkę”, ✕, „Anuluj”, „Zapisz pinezkę” — `clickable`, osobne węzły,
   cel 48 dp; **tekst 200%** (karta i panel D, pigułka B) i **360 × 640 dp**.
7. logcat: brak współrzędnych z `geo fix`; `aapt` na APK release — uprawnienia.
8. Próbne odtworzenie: kopia z `Medium_Phone` → `Grobing_Restore` → pinezki z datą są, odcisk zgodny.

**Autor: odczucie** (najwyżej 3):
1. `Medium_Phone`: grób bez pinezki → „Postaw pinezkę” (agent prowadzi kropkę po planie) → popraw pinezkę ręką → „Zapisz pinezkę”.
   Czy wariant z D1 jest naturalny i czy pinezka staje tam, gdzie celujesz?
2. Na planie ◎: włącz, przesuń plan, wróć, wyłącz. Czy trzy stany przycisku są jasne bez tłumaczenia?

**W terenie** (wyjątek DoD: GPS na miejscu, offline na cmentarzu — build release na telefonie, D4): przy 3 grobach — kropka i jej
dokładność, pinezka postawiona i poprawiona, tryb samolotowy. **Nie blokuje zamknięcia** — *Parked* z pomiarem H3/H9.

Przegląd ekranów `ui` (subagent `qa`) przed stopem #2; `dev` przechodzi AC na emulatorze przed `qa` (retro 2, R5) — z tekstem 200%,
360 dp i semantyką.

### Out of Scope
- „Pokaż kwaterę”, lista grobów kwatery, znicze nachodzące na siebie → [[ISSUE-030-sector-on-a-visit]] (D5).
- Lokalizacja w trybach kwater (E, F) — rysowanie kwatery na miejscu; kompas, kierunek i odległość do pinezki; lokalizacja w tle.
- Pinezki w eksporcie dla rodziny → [[US-006-eksport-dla-rodziny]].
- Zmiana progu słabego sygnału — po pomiarze (*Parked*), jedna stała.
- Twarde spacje w „±5 m” i „Kwatera B” — pozycja z regułą 6 [[style-b]] (*CURRENT_STATE* → poza kolejnością).

## Dev report
> `dev`, 2026-10-12. Flutter 3.41.1 (przypięty). `flutter analyze` czyste na `lib/` i `test/`, `dart format` na `lib/`. Testów `dev` nie
> pisze; żaden istniejący test nie przestał się kompilować. `pubspec.yaml` i `pubspec.lock` bez zmian (D2 A).

### What was built (`{code}`)
- **Dane, schemat v12** (D3): `graves.position_recorded_at`, `PositionSource.plan` (na końcu, zapis po nazwie), `_from11To12` (`addColumn`).
  Pliki schematu z `make-migrations` (`drift_schema_v12.json`, `database.steps.dart`, `test/drift/grobing/generated/schema_v12.dart`).
  `graves.dart`: `GravePin` (punkt, źródło, dokładność, data) w `GraveSummary.pinned` i `GraveDetail.pin` (gettery `pin` i `hasPin`
  zostają), `setGravePin` — dokładność tylko przy `gps`, data z zegara.
- **Lokalizacja** (D2 A): `HereLocation.kt` — `GPS_PROVIDER`, `requestLocationUpdates` co 1 s tylko przy subskrypcji, `removeUpdates`
  przy anulowaniu; FINE i COARSE w jednym żądaniu; „blocked” po odmowie bez `shouldShowRequestPermissionRationale`; ustawienia
  aplikacji i lokalizacji; **bez `Log.`**. `MainActivity` — rejestracja i `onRequestPermissionsResult`. Manifest — dwa uprawnienia i
  `uses-feature gps required=false`. Dart: `here_location.dart` — `HereLocation` (kanał; jeden wspólny strumień), `MapHereLocation`
  nad nawigatorem (`grobing_app.dart`), `HereTracker` na ekran, `weakSignalM = 15` (jedna stała, tymczasowa), `atCemetery`,
  `distanceText`.
- **Ekrany:**
  - `map_chrome.dart` — `MapPill` (wspólna pigułka „Kwatery” / „Popraw pinezkę”, zamiast prywatnej `_SectorsPill`), `HereButton`
    (trzy stany, opis ze stanem i dokładnością), `HereStatus` (10a), `MapBadges.hereStatus`;
  - `cemetery_plan_map.dart` — warstwa „tu jesteś” (koło w metrach 18%, kropka 16 dp z obwódką, plakietka 12 sp do 1,3×), `onMapEvent`;
  - `cemetery_screen.dart` — ◎ w A i B (D31: włącz i do kropki z z18 · na kropce → wyłącz · odsunięty → wróć; kropka poza cmentarzem →
    10a z odległością, plan stoi), plakietka 10a, pasek „Lokalizacja w telefonie jest wyłączona.” z „Włącz”, „Popraw pinezkę” w B,
    po `PinSaved` stan B z grobem, komunikat [[osoba]] D9;
  - `pin_screen.dart` (nowy) — **tryb D w wariancie P2**: pasek z ✕, karta (teksty ze *States* v7), znicz w obrysie z cieniem na
    środku wolnego miejsca, plan za kropką, przeciągnięcie albo dotknięcie (płynny przesuw pod znicz) → ręcznie, ◎ → do kropki,
    przygaszone znicze, warstwa z poprzedniego stanu; panel 12a (adres, „Pinezka: …” / „Teraz: …” / „Po zapisie: …”, „Szukam
    pozycji…”, „Jesteś poza cmentarzem (…)”, lokalizacja wyłączona z „Włącz”, słaby sygnał, błąd zapisu); start (D32), poprawa (D35);
  - `grave_screen.dart` — element 4: „Postaw pinezkę” albo „Pinezka: GPS ±4 m · 12.10.2026”; po zapisie zamyka się z wynikiem;
  - `polish.dart` — `pinSourceText`, `pinLine`; `theme.dart` — `GrobingColors.here`.
- `fictional_data.dart` (debug) — wymyślone pinezki przez `setGravePin`, po kolei z każdym źródłem. README: *Baza danych* (v12),
  nowa sekcja *Lokalizacja* (kanał, emulator, build na telefon przed wizytą, czyszczenie danych).

### Deviations (do przeglądu `ui`)
1. **Odległość od 10 km w pełnych kilometrach** („9446 km”, nie „9445,6 km”; od 1 do 10 km z jedną cyfrą po przecinku — 10a (a)).
2. **Komunikat [[osoba]] D9 jako pasek komunikatu na dole** (`SnackBar`, jak każdy pasek komunikatu w aplikacji), a nie „pod paskiem
   (1)”.
3. **Grób dodany przez formularz** („Dodaj grób” → formularz zastępuje się widokiem grobu): po „Zapisz pinezkę” wraca na mapę w stanie,
   z którego przyszedł (A, z nowym zniczem), a nie do B — wynik nie przechodzi przez `pushReplacement`. Z listy i z B — stan B, jak D36.
4. **Tryb D bez planu i bez zdjęcia** (cmentarz bez obrysu w OSM): „Planu tego cmentarza nie ma w telefonie. Pinezkę postawisz tu tylko z
   GPS.” — zapis tylko z kropki. Specyfikacja tego stanu nie opisuje.
5. **Szczypanie w trybie D nie zmienia pinezki na ręczną** — zmienia przybliżenie, a plan wraca pod kropkę. Ręczna jest po przeciągnięciu
   albo dotknięciu (element 12: „przeciągnięcie planu albo dotknięcie miejsca”). Po pierwszym szczypaniu ekran nie zmienia już
   przybliżenia sam.
6. **◎ w A i B nie ma przy zaślepce planu (2a) i przy „Zdjęciu” bez sieci** — jak „Kwatery”; kropka nie ma na czym stanąć.
7. **Przy tekście 200% na 360 × 640 dp** plan w A jest bardzo niski, a „Kwatery” i ◎ stoją na wysokości plakietek (zrzut `24-200-B`).
   To znana luka z [[ISSUE-027-cemetery-map-plan-photo-states]] (kadr, D14 → *Obali*), ◎ jej nie pogarsza; tryb D w tych warunkach mieści się
   (zrzut `23-200-D`).

### Found on the emulator (AC przed `qa`, R5) — `Grobing_Restore`, release jako aktualizacja na danych z kopii 028
- **Migracja na danych testowych autora:** v11 → v12, „Stan danych”: wersja schematu 12, dane i kopia całe.
- **Przeszło:**
  - A: ◎ → okno systemu (Precise / Approximate; While using · Only this time · Don't allow) → „Don't allow” → „Bez zgody na lokalizację
    pinezki postawisz tylko ręcznie.” → ◎ → zgoda → kropka, koło, „tu jesteś · ±5 m”, plan przy kropce w z18; ◎ na kropce → wyłącza; plan
    przesunięty → `location_searching` → ◎ → wraca; pozycja domyślna emulatora (Kalifornia) → „poza cmentarzem · …”, plan stoi;
  - grób z kwaterą → „Postaw pinezkę” → D z GPS (karta „Stań przy grobie…”, „Pinezka: GPS ±5 m”) → przeciągnięcie → „Pinezka: postawiona na
    planie”, karta ręczna z ◎ → dotknięcie miejsca w kwaterze → pod znicz → „Zapisz pinezkę” → B z nowym zniczem, „Popraw pinezkę” i ◎ nad
    arkuszem → „Pokaż grób” → „Pinezka: postawiona na planie · 12.10.2026”;
  - B → „Popraw pinezkę” → „Teraz: postawiona na planie · 12.10.2026”, „Zapisz pinezkę” nieaktywne → ◎ → „Po zapisie: GPS ±5 m” → zapis →
    „Pinezka: GPS ±5 m · 12.10.2026”;
  - **tryb samolotowy:** „Zdjęcie” → „bez internetu”, „Wróć do planu”; D, ◎ i zapis z GPS działają;
  - z widoku osoby „Pochówek” grobu bez pinezki → lista z zaznaczonym grobem i „Ten grób nie ma jeszcze pinezki — jest zaznaczony na liście.”;
  - grób bez adresu → „Wpisz adres” i pod nim „Postaw pinezkę” → D bez strefy kwatery, przybliżenie z18;
  - zgoda „Przybliżona” (`pm revoke` FINE) → „tylko przybliżona lokalizacja”, bez kropki; dwie odmowy → trzecie dotknięcie bez okna, pasek z
    „Ustawienia”;
  - **tekst 200% i 360 × 640 dp:** tryb D — karta przewijana z paskiem, ◎ nad panelem, „Anuluj” i „Zapisz pinezkę” w jednym rzędzie;
  - `uiautomator`: ◎ („Gdzie jestem, włączone, ±5 m” / „wyłączone”; w D „Pinezka w Twojej pozycji…”), „Popraw pinezkę” (48 dp), „Postaw
    pinezkę” (48 dp), ✕, „Anuluj”, „Zapisz pinezkę” (52 dp) — `clickable`, osobne węzły; nieaktywne „Zapisz” — `clickable=false`;
  - **logcat procesu aplikacji: 0 linii ze współrzędnymi** podanymi emulatorowi; `aapt` na APK release — nowe uprawnienia tylko
    `ACCESS_FINE_LOCATION` i `ACCESS_COARSE_LOCATION`.
- **Poprawione w przejściu:**
  - plan w A wracał do najmniejszego przybliżenia, gdy pojawiała się albo znikała plakietka 10a (ekran od nowa dopasowywał cały cmentarz)
    → kropka przejmuje kadr jak palec;
  - tryb D startował przy całym cmentarzu (pierwsze dopasowanie mapy przychodziło po ruchu startu) → każde ustawienie pinezki przez ekran
    przybliża do z18, dopóki autor sam nie zmieni przybliżenia;
  - „9445,6 km” → pełne kilometry od 10 km (odstępstwo 1).
- **Emulator:** `adb emu geo fix <dł> <szer>` bez wysokości i satelitów zostawiał domyślną pozycję emulatora; działa `… 100 8` (README).
- **Nie sprawdzone tutaj (dla `qa`):** słaby sygnał (emulator nie ustawia dokładności — test widżetu); lokalizacja wyłączona w telefonie
  („Włącz”); warstwa „Zdjęcie” z siecią w trybie D („postawiona na zdjęciu z góry”); próbne odtworzenie kopii v12; TalkBack.
- **Stan emulatora po przejściu:** `Grobing_Restore` — build release z tej pozycji; dwa groby z danych 028 mają pinezki (GPS ±5 m i z
  planu), zgoda na lokalizację cofnięta do „nie pytano”, tekst 100%, rozmiar ekranu przywrócony. Zrzuty w katalogu tymczasowym sesji
  (`8b388e89-…/scratchpad/shots/`).

### For `qa`
- Testy do napisania według *AC → implementation → test*; udawana lokalizacja przez `MapHereLocation` z własnym `HereLocation` (strumień
  `HereSignal`). `HereTracker` łapie błędy strumienia.
- Test na źródłach: `HereLocation.kt` bez `Log.`.
- Kroki autora bez zmian względem planu (*Manual verification* → „Autor: odczucie”, 1–2) — na `Medium_Phone` po aktualizacji.

## Verification
> `qa`, 2026-10-12. Rytuał WZ-024: `dart format` (0 zmian w 174 plikach) → `flutter analyze` (czyste, `lib/` i `test/`) → `flutter test`
> **692/692** (było 661; +31) → kroki agenta na emulatorze → stop #2. Werdykt: self-check (krytyk — ISSUE-003).

### Tests (happy path per AC, `{code}/test/`)
| AC | Test |
|---|---|
| US-008 AC-1 — gdzie jestem | `app/grave/pin_screens_test.dart` „US-008 AC-1 — "gdzie jestem": off, the system's question, then the blue dot…” · „…a refusal… refused twice… only "Przybliżona"… a position far away” |
| US-008 AC-2 — postaw pinezkę | `pin_screens_test.dart` „US-008 AC-2 — a grave without a pin → "Postaw pinezkę" → mode D…” (GPS z dokładnością i datą) · „…a finger moves the plan: the pin becomes "postawiona na planie"…” (ręczna, bez dokładności, `PinSaved`) · `data/grave_pins_test.dart` (zapis, D33, linia źródła) |
| US-008 AC-3 — popraw pinezkę | `pin_screens_test.dart` „US-008 AC-3 — a candle → B → "Popraw pinezkę"…” („Teraz: …”, zapis nieaktywny, ◎ bez pozycji go nie uaktywnia — M2, ◎ → „Po zapisie: GPS ±5 m” → B) |
| US-008 AC-4 — bez internetu | `pin_screens_test.dart` „US-008 AC-4 — without the internet…” · „ui review M3 — a cemetery without a plan and without the photo…” |
| ISSUE-029 — pinezka z datą po odtworzeniu | `backup/restore_service_test.dart` „ISSUE-029 — a v12 backup with pins restores with them…” (odcisk zgodny, oba źródła) |
| D37 — słaby sygnał | `pin_screens_test.dart` „D37 — a GPS position worse than 15 m…” · `grave_pins_test.dart` (próg 15 m) |
| [[grob]] 4, D14 · [[osoba]] D9 · 200% | `pin_screens_test.dart` „grob.md v7 element 4, D14…”, „osoba.md D9…”, „element 12 at 200% on 360 × 640 dp…” |
| 10a, element 14 | `grave_pins_test.dart` (w obrysie, odległość, linia „GPS ±4 m · 12.10.2026”) |
| NFR-005 | `grave_pins_test.dart` — `HereLocation.kt` bez `Log.`, bez `NETWORK_PROVIDER`, bez usług Google; `repo_invariants_test.dart` — w manifeście tylko `INTERNET`, FINE, COARSE, bez `ACCESS_BACKGROUND_LOCATION`, GPS niewymagany |

Przepisane (zmiana celowa): wersja schematu 11 → 12 (`database_test`, `data_state_test`, `data_state_screen_test`), wymyślone pinezki z każdym
źródłem (`dev/fictional_pins_test`), manifest (`repo_invariants_test`).

### Data layer (DoD)
- **Migracja v11→v12 na danych** (`migration_test.dart`, `testWithDataIntegrity`): pinezki `gps` i `satellite` oraz grób bez pinezki —
  pozycje, źródła i dokładności bez zmian, data `NULL`, kwatery i odnośniki całe.
- **Na urządzeniu:** `Medium_Phone` (Twoje dane testowe) v11 → v12 jako aktualizacja — wszystkie liczby w „Stanie danych” bez zmian,
  zmienił się tylko odcisk (`19061c02…` → `b334e4fa…`, nowa kolumna — oczekiwane).
- **Próbne odtworzenie:** kopia skonfigurowana od nowa na `Medium_Phone` (wymyślone hasło testowe, `grobing-klucz-029.age`,
  `grobing-kopia-029.age` w Pobranych) → `Grobing_Restore`: „Odtworzono kopię z dnia 2026-10-12 18:54. Odcisk danych w kopii:
  6af0474033244a3e — ten sam co niżej.” W trybie samolotowym znicz na planie i „Pinezka: GPS ±5 m · 12.10.2026”.
- **Źródło i status faktu:** nie dotyczy — pinezka to dane miejsca, a jej źródło to pole grobu (FR-001 wycofane, D28).
- **Dane rodziny:** w zmianach brak baz, kopii, eksportów, zdjęć; w testach i kodzie tylko rdzenie wymyślone (Wymyśl-, Zmyśl-, Testow-);
  suchy przebieg strażnika treści na 30 plikach kodu i 8 plikach vaulta — przeszedł. Logcat procesu aplikacji: 0 linii ze
  współrzędnymi; `aapt` — nowe uprawnienia tylko FINE i COARSE.

### UI review (`ui`, subagent bez historii) — 0 BLOCKER, 3 MAJOR, 9 MINOR
- **MAJOR, poprawione przez `dev` przed stopem #2:** M1 karta „Stań przy grobie” przy braku kropki (przeczyła panelowi) → tekst GPS tylko
  przy pinezce w kropce (zrzut `45-D-outside-after-review`); M2 ◎ bez pozycji uaktywniał zapis poprawki i gubił „GPS ±N m” → zapis dopiero
  po ruchu pinezki (test); M3 zapis pinezki, której nie widać (bez mapy; „Zdjęcie” bez sieci) → bez mapy tylko GPS, D na planie bez sieci,
  „Popraw pinezkę” z regułą ◎ (test).
- **MINOR poprawione:** m1 cień w kolorze tła i nie na kropce, m2 stany lokalizacji w kolorze tekstu (W2), m3 ◎ w D „Gdzie jestem”, m4
  mała litera po dwukropku, m5 po podwójnym dotknięciu znicz wraca do kropki, m7 rola koloru „tu jesteś” w `style-b` v1.23 i w `theme.dart`.
- **MINOR przyjęte bez zmiany kodu:** m6 pierwsze przybliżenie skokiem (zapisane w [[cmentarz]] v7.1), m8 luka 200% / 360 dp z ISSUE-027/028
  (zrzut `46-200-B`: „Popraw pinezkę” i ◎ całe, 48 dp; plan niski) — kandydat na osobną pozycję, m9 ◎ bez kropki do powrotu wyłącza (v7.1).
- **Odstępstwa `dev` 1–7:** przyjęte (4 i 6 z poprawką M3); wpisane w [[cmentarz]] v7.1.
- **Znalezione testami `qa` i poprawione w `dev`:** przy zgodzie „Przybliżona” (i bez pozycji) ◎ nie dawał się wyłączyć; tryb D bez mapy tworzył
  kontroler animacji dopiero w `dispose()` (wyjątek przy zamknięciu ekranu).

### Not verified here
- Słaby sygnał na urządzeniu (emulator nie ustawia dokładności — tylko test); lokalizacja wyłączona w telefonie („Włącz”) — tylko kod;
  „Zdjęcie” z siecią w trybie D na jasnym zdjęciu (reguła 14); TalkBack.
- **Krok w terenie** (D4): GPS przy 3 grobach, pinezka postawiona i poprawiona, tryb samolotowy, czytelność w słońcu (NFR-004) — build
  release na telefonie autora przed ~2026-11-02; nie blokuje zamknięcia → `CURRENT_STATE.md` → *Parked* razem z pomiarem H3/H9.

### Do retro
- **`python -I -` jeszcze raz** (`qa`, w komendzie poprawiającej test) — zawisło, zatrzymane od razu, bez skutku. Ósmy raz mimo pamięci
  „nigdy”: hook `PreToolUse` z *Do retro* coraz pilniejszy.

### Stop #2 (2026-10-12) — autor: „działa - poprawiłem pinezkę jest ok”
- **Krok 1 (pinezka ręką, celownik P2) — „ok”, sprawdzone na urządzeniu:** zgoda na lokalizację nadana przez autora (`USER_SET`, Precise);
  autor **poprawił** pinezkę grobu „Jozef” (postawioną przez agenta z GPS) — w widoku grobu „Pinezka: postawiona na planie ·
  12.10.2026”. Nowej pinezki na „Grob wymyslonych” nie postawił — droga poprawy (B → „Popraw pinezkę” → D) używa tego samego celownika.
- **Krok 2 (trzy stany ◎) — ogólne „działa”, bez śladu na urządzeniu** (◎ nie zostawia stanu).
- **Krok w terenie** (D4) — nie teraz; *Parked* przy zamknięciu (`docs`).

**Werdykt: APPROVED** (self-check, z uwagami):
- AC-1–AC-4 mają testy happy-path i przeszły na emulatorze; AC-1 i AC-4 na prawdziwym GPS i w terenie — dopiero przy wizycie (D4);
- krok 2 autora bez śladu; słaby sygnał i „Włącz” tylko w testach; TalkBack niesprawdzony;
- luka 200% / 360 dp z ISSUE-027/028 zostaje (kandydat na pozycję przed MVP).

**Czego szukano i nie znaleziono:** AC bez testu; testy czerwone albo pominięte; współrzędne w logu; nowa zależność albo usługi Google
(`pubspec.lock` bez zmian); uprawnienia inne niż FINE i COARSE (także `ACCESS_BACKGROUND_LOCATION`); dane rodziny w zmianach (strażnik —
suchy przebieg); zgubiony wiersz po migracji (liczby „Stanu danych” na danych autora bez zmian); różny odcisk po odtworzeniu.

### Package for `docs` (jedna pozycja = jeden commit na repo)
- **`grobing-code` (30):** `README.md` · `android/app/src/main/AndroidManifest.xml` · `android/app/src/main/kotlin/com/grobing/app/MainActivity.kt` ·
  `android/app/src/main/kotlin/com/grobing/app/HereLocation.kt` · `drift_schemas/grobing/drift_schema_v12.json` ·
  `lib/app/grave/{cemetery_plan_map,cemetery_screen,grave_screen,here_location,map_chrome,pin_screen}.dart` · `lib/app/{grobing_app,polish,theme}.dart` ·
  `lib/data/{database,database.g,database.steps,graves}.dart` · `lib/dev/fictional_data.dart` ·
  `test/app/data_state_screen_test.dart` · `test/app/grave/pin_screens_test.dart` · `test/backup/restore_service_test.dart` ·
  `test/data/{data_state_test,database_test,grave_pins_test}.dart` · `test/dev/fictional_pins_test.dart` ·
  `test/drift/grobing/generated/{schema,schema_v12}.dart` · `test/drift/grobing/migration_test.dart` · `test/repo_invariants_test.dart`.
- **`grobing-vault`:** `00_START_HERE/CURRENT_STATE.md` · `00_START_HERE/TRACEABILITY.md` · `03_REQUIREMENTS/user-stories/US-008-pinezka-na-miejscu.md` ·
  `05_DESIGN/cmentarz.md` · `05_DESIGN/grob.md` · `05_DESIGN/brand/style-b.md` · `backlog/issues/ISSUE-029-pin-on-site-gps.md` ·
  `backlog/issues/ISSUE-030-sector-on-a-visit.md` + pliki zamknięcia `docs` (ADR-017, [[data-model]], słowniczek, US-008, EPIC-002…).
- **`grobing-agents`:** brak zmian.
