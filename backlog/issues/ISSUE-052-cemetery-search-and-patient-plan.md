---
title: "ISSUE-052 — Cemetery: a search result says which place it was found through, and the plan downloads patiently, in the background, until it comes"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-23
verdict-reviewer: self-check
source: "`/pm` 2026-10-22 — pierwsze użycie MVP z prawdziwymi danymi; autor: *„ta funkcjonalność zadziałała najgorzej (w ogóle nie zadziałała)”*; zakres A z `/pm`, autor: *„ok jestem ok z tym co piszesz, wprowadźmy te rozwiązanie dla cmentarzy”*"
created: 2026-10-22
updated: 2026-10-23
---

# ISSUE-052 — Cmentarz: wynik mówi „przy: …”, a plan pobiera się cierpliwie

> Autor 2026-10-22 w `/pm`, po pierwszym użyciu MVP: cmentarza parafialnego we wsi *„mimo wpisywania adresu, nazwy … nic się nie wyszukiwało”*
> (Grobonet go ma), a dużego cmentarza miejskiego *„po około minucie pojawiała się informacja, że nie można pobrać, bo serwer nie odpowiada. No
> niestety to jest no-go, jeżeli miałbym tego próbować na żywo na cmentarzu”*. Pytanie autora: *„skąd pobieramy te cmentarze … czy korzystamy z
> grobonetu?”* — nie: lista to wbudowany wyciąg OSM ([[ISSUE-015-add-cemetery-from-database]]), plan to Overpass przy dodaniu cmentarza
> ([[ADR-003-map-source-offline]] pkt 1, [[ISSUE-027-cemetery-map-plan-photo-states]]), zdjęcie z góry to GUGiK online; Grobonet tylko linkiem
> ([[NT-004-grobonet-link-terms]]).

## Why — measured 2026-10-22 (`pm`, z PC, te same zapytania co aplikacja)
**Wyszukiwanie — cmentarz jest w bazie, ale nie da się go rozpoznać.** OSM nazywa cmentarz parafialny we wsi tylko „Cmentarz parafialny” i
przypisuje go do przysiółka tej wsi; nazwa wsi jest tylko na liście okolicznych miejscowości (`nearby`). Symulacja wyszukiwarki aplikacji na
wbudowanej bazie:

| Wpisane | Wyników | Ten cmentarz | Karta mówi |
|---|---|---|---|
| nazwa wsi (mianownik) | 51 | 25. | „Cmentarz parafialny · <przysiółek>” — nazwy wsi nie ma |
| nazwa wsi w miejscowniku (jak w nazwie z Grobonetu) | 855 | 402. — poza 30 pokazanymi | |
| wezwanie parafii z nazwy z Grobonetu | 0 | — | OSM nie zna tej nazwy |
| „parafialny” + nazwa wsi | 22 | 4. | |

To temat z [[ISSUE-015-add-cemetery-from-database]] → *Notes* („wynik znaleziony przez okoliczną miejscowość nie mówi, dlaczego trafił”,
propozycja `ui`: „· przy: …”), który przy prawdziwym cmentarzu przeszkodził naprawdę.

**Pobieranie planu — aplikacja poddaje się, zanim serwer odpowie.**

| Zapytanie | Główna instancja (`overpass-api.de`) | Druga instancja aplikacji i dwie inne |
|---|---|---|
| obrys, duży cmentarz miejski | 37,5 s, 17 KB | brak odpowiedzi w 90 s (dwie) · 504 po 0,6 s (jedna) |
| alejki, duży cmentarz miejski | 43,3 s, 437 KB | — |
| obrys, mały cmentarz wiejski | 30,5 s, 1,4 KB | — |
| alejki, mały cmentarz wiejski | 30,1 s, 5,8 KB | — |

**Cmentarze autora na wyjazd (8 pozycji listy autora, 13 obrysów z kandydatami — pomiar `pm` 2026-10-22 wieczorem, te same zapytania co
aplikacja, nazwy tylko w czacie):** wszystkie 13 mają obrys w OSM (żaden nie kończy się na (d)); 26 zapytań trwało **22–47 s**, 4 razy przyszło
502 i następna próba po 5 s przeszła. **Ze starymi granicami (30 s / 60 s) obie odpowiedzi zmieściłyby się przy 1–2 z 13, z nowymi (pkt 2
planu) — przy 13 z 13.** Cała lista jeden po drugim: ok. 15 min. Plany od kilku alejek (cmentarze wiejskie, 3–5 odcinków) do gęstej sieci
(duży cmentarz miejski, 180 odcinków); jeden zespół cmentarzy w mieście to w OSM kilka osobnych obrysów, więc w aplikacji — kilka cmentarzy.

Czas nie zależy od rozmiaru — serwer ma kolejkę. Aplikacja (`OverpassPlanSource`) czeka **30 s na zapytanie** i **60 s łącznie**, więc przy dzisiejszym
serwerze trafia w granicę: stąd „po około minucie”. Granice ustawiła [[ISSUE-027-cemetery-map-plan-photo-states]], gdy obrys przychodził w 3 s.
Do tego pobiera **tylko przy otwartej aplikacji** (D3 tamtej pozycji): przy starcie, powrocie, otwarciu cmentarza i „Pobierz teraz”.

## What to build
1. **Wynik w bazie cmentarzy mówi, przez co trafił** — „przy: <miejscowość>”, gdy słowa pasują do okolicznej miejscowości, a nie do nazwy ani
   miejscowości karty; **trafienia po nazwie i po miejscowości karty stoją wyżej niż po okolicy**. Odmiana nazwy miejscowości (miejscownik jak w
   nazwach parafii) — do `ui`, z liczbą wyników przed i po.
2. **Plan pobiera się cierpliwie, aż zejdzie:**
   - granice czasu z pomiaru wyżej, z zapasem na gorszy dzień (minuty, nie 60 s) — liczby wybiera `planning` z pomiaru, nie z pamięci;
   - nieudane pobranie **ponawia się samo** z przerwami, póki plan nie zejdzie albo OSM nie powie „brak obrysu” (2a (d)) — także po wyjściu z
     ekranu cmentarza; czy **przy zamkniętej aplikacji** (WorkManager — zmienia D3 z ISSUE-027) — do `ui` i `planning`, z kosztem;
   - komunikat mówi prawdę: serwer map jest przeciążony i aplikacja spróbuje znowu sama; widać, że pobieranie trwa (2a (a), (c)).
3. **Zasada na wyjazd:** cmentarze dodaje się **w domu, na Wi-Fi**, a plan zostaje w telefonie ([[ADR-003-map-source-offline]] pkt 1). Gdzie to
   powiedzieć w aplikacji (karta cmentarza bez planu? podpowiedź przy dodaniu?) — do `ui`.

**Bez zmiany bazy** (plan zapisuje się jak dziś — [[ADR-015-cemetery-plan-in-database]]). **Aktualizacja ze sklepu przed wyjazdem na Wszystkie Święte**
— w trakcie wyjazdu aktualizacji nie ma (`CURRENT_STATE.md` → *In progress*, „Zasady terminu”).

## What this will not give
- **Czytelności planu zarządcy.** Dla cmentarza parafialnego we wsi OSM ma obrys i kilka alejek (5,8 KB), bez grobów i kwater — jak w
  [[SPIKE-001-map-source-offline]] M10, M11. Plan „jak Grobonet” to osobna decyzja (niżej).
- **Planu w 5 minut, gdy serwer leży godzinami** — ponowi się sam, ale później.
- **Planów bez żadnego serwera** — opcja C niżej.

## Out of scope — decided after the visit (autor, 2026-10-22)
- **Plan zarządcy jako obraz:** zrzut ekranu autora (aplikacja nic z Grobonetu nie pobiera) przy cmentarzu, offline, bez GPS — „najgorszy wypadek”
  autora; dalej ewentualnie **dopasowanie obrazu dwoma punktami** do zdjęcia z góry, żeby niebieska kropka trafiała na zrzut (prior art: aplikacje do
  map szlaków, np. Custom Maps, Avenza — zdjęcie mapy przy wejściu + 2 punkty). Przesuwa granicę [[ADR-003-map-source-offline]] pkt 3 („siatki grobów
  nie ma”) i W3 — decyzja autora. **Najtańszy falsyfikator, bez kodu:** przed wyjazdem zrzut mapy zarządcy (po wyszukaniu grobu) w galerii telefonu
  i otwarcie go na cmentarzu bez sieci. Wystarczył → „obraz przy cmentarzu”; brakowało kropki → dopasowanie. Zaparkowany pomiar GPS (`CURRENT_STATE.md`
  → *Parked*) z tej samej wizyty mówi, czy kropka jest dość dokładna.
- **Opcja C — plany wszystkich cmentarzy wbudowane w aplikację** (jak baza cmentarzy), bez serwera. Rozmiar do policzenia z wyciągu Polski na PC.

## Acceptance Criteria (propozycja `docs` z `/pm` — do potwierdzenia przez `ui` i `planning`)
- **AC-1** *Given* w bazie „Cmentarz parafialny” z miejscowością „Zmyślonka”, a „Wymyślów” jest tylko wśród okolicznych *When* wpisuję „Wymyślów”
  *Then* karta mówi „przy: Wymyślów”, a cmentarze z miejscowością „Wymyślów” stoją nad nią.
- **AC-2** *Given* serwer odpowiada na każde z dwóch zapytań po 45 s *When* dodaję cmentarz *Then* plan zapisuje się bez błędu, a ekran przez cały
  czas mówi, że pobieranie trwa.
- **AC-3** *Given* serwer nie odpowiada *When* minie granica *Then* ekran mówi, że serwer map jest przeciążony i aplikacja spróbuje znowu sama;
  *When* serwer wróci *Then* plan schodzi bez dotknięcia, także gdy w tym czasie wyszedłem z ekranu cmentarza.
- **AC-4** *Given* plan zapisany *When* włączam tryb samolotowy i otwieram cmentarz *Then* plan jest (bez zmian względem dziś — regresja).

## Notes
- **Ekrany (`ui` → `planning`):** [[cmentarze]] (karta wyniku z bazy, kolejność, element 12–14) · [[cmentarz]] (2a — stany pobierania). Kod:
  `lib/app/home/cemetery_base.dart`, `lib/net/overpass_plan_source.dart`, `lib/app/map/plan_downloads.dart`, `lib/net/hosts.dart`.
- **Dane rodziny:** cmentarze autora tylko jako liczby i opisy („cmentarz parafialny we wsi”, „duży cmentarz miejski”). W testach i przykładach —
  wymyślone rdzenie (`family-data.md`).
- **`TRACEABILITY.md`** — wiersz przy starcie pozycji (`planning`).

## Stop #1 (2026-10-22)
- Autor: **„B1”** — plan pobiera się także przy zamkniętej aplikacji (pkt 6 wchodzi; [[cmentarz]] *Open* rozstrzygnięte); to też „tak” dla reszty
  planu (wiadomość stopu).
- Ta sama wiadomość: autor nie znalazł w obecnej wersji jednego z cmentarzy we wsi i zapytał, co wpisać dla cmentarza we wsi z Grobonetu. `pm`
  podał w czacie słowa, które dziś dają 2 wyniki (nazwa miejscowości + sąsiednia wieś albo gmina) — bez zmiany zakresu: po tej pozycji wystarczy
  sama nazwa (pomiar D36: 102. → 4. i 25. → 2.). Pomysł „łatwiej ustalić, który to cmentarz” poza nazwą (np. zdjęcie z góry w podglądzie
  zamiast linku do Map Google) — **nie dodany po cichu**: wraca, jeśli po tej pozycji wybór dalej będzie trudny.

## Implementation plan (`planning`, 2026-10-22)
> Specyfikacje: [[cmentarze]] v2.8 (D35–D37) · [[cmentarz]] v9 (D39–D41, ⚠️ OPEN B1/B2). Bez makiety: zmiany to teksty i jedna linia w
> istniejących elementach, a jedyny wybór (B1/B2) dotyczy zachowania, nie wyglądu. **Bez zmiany schematu** (v15) — migracji nie ma.

### Scope diff
1. **Kolejność i „przy:” w bazie cmentarzy** ([[cmentarze]] 12, D35, D36). `CemeteryBase.search` zwraca przy każdym wyniku okoliczną
   miejscowość, przez którą trafił (albo nic), i sortuje kluczem D36: (1) więcej słów zapytania jako całe słowa w polach, (2) najdalsze pole,
   którego wymaga któreś słowo (nazwa · miejscowość/dzielnica · okolica · środek słowa), (3) mniej pól na wszystkie słowa, (4) kolejność pliku
   (alfabet). Zbiór wyników bez zmian (D3). Słowa pól dzielone na znakach innych niż litery i cyfry (myślnik, nawias, kropka).
   `BaseCemeteryCard` wstawia „przy: <miejscowość>” po miejscu, przed województwem (`joinPlaceLine`).
   *Pomiar przed planem* ([[cmentarze]] D36): 8 z 8 cmentarzy autora w 30 pokazanych (dziś 6 z 8); koszt wyszukiwania — `dev` mierzy czas
   jednego zapytania na emulatorze przed i po (dziś liczone przy ISSUE-015; klucz liczy się tylko dla trafień, nie dla 16 tys. wierszy).
2. **Cierpliwe pobieranie** (`OverpassPlanSource`, [[cmentarz]] D39): `requestTimeout` 30 s → **120 s** (najwolniejsza odpowiedź z pomiaru
   43 s, prawie 3× zapasu), `deadline` 60 s → **5 min** na jedną próbę obu zapytań (obrys + alejki to 60–81 s w pomiarze, z jednym ponowieniem
   się mieści), `connectionTimeout` 15 s bez zmian. `[timeout:25]` w zapytaniu **zostaje**: z nim przeszły wszystkie pomiary, a to czas
   wykonania na serwerze, nie kolejki. Kolejność instancji bez zmian (druga nie odpowiedziała w 90 s — nie przeszkadza, bo pierwsza idzie
   pierwsza).
3. **Ponawianie w aplikacji** (`PlanDownloads`, [[cmentarz]] D40): po (c) kolejna próba sama po **2, 5, 10 min, potem co 15 min**, póki
   aplikacja działa; w czasie próby stan wraca do (a); „Pobierz teraz” — od razu, jak dziś. Bez internetu (b) czeka na start/powrót jak dziś
   (w B1 — na zadanie w tle niżej). `PlanDownloads` wystawia chwilę startu bieżącej próby, żeby zaślepka po 15 s dołożyła linię „odpowiada dziś
   wolno” (D39).
4. **Teksty zaślepki** (`plan_placeholder.dart`, [[cmentarz]] 2a v9): (a) dwie linie + trzecia po 15 s; (c) „Serwer map jest teraz
   przeciążony.” + droga naprzód; warianty B1/B2; bez grobów — bez „Groby są na liście.” (jak dziś).
5. **Stan planu przed wejściem w cmentarz** ([[cmentarze]] 6, 11, D37 — decyzja projektowa): `CemeterySummary` dostaje stan zapisanego planu
   (brak · plan · brak w OSM) z `LEFT JOIN cemetery_plans` w zapytaniu podsumowań (`lib/data/cemeteries.dart`, odczyt, bez zmiany schematu);
   `cemeteryLine` dopisuje „bez planu” / „bez planu w OSM” na liście „Twoje cmentarze”; arkusz (`home_screen.dart`) — linia planu z ikoną
   (`Glyphs.offlinePin`, `cloudDownload`, `cloudOff`, `notListedLocation` — są w foncie ikon, bez przebudowy fontu) ze stanem z pamięci
   `PlanDownloads`, gdy pobieranie trwa w tym uruchomieniu.
6. **B1 — pobieranie przy zamkniętej aplikacji** (tylko po „B1” na tym stopie; [[cmentarz]] *Open*). Wzorzec kopii w tle (`BackupWorker`,
   ISSUE-010):
   - `PlanWorker.kt` (nowy): WorkManager, unikalne zadanie `grobing-plans` (`KEEP`), warunek **sieć** (`NetworkType.CONNECTED`), ponawianie
     wykładnicze od 5 min, granica przebiegu 9 min (pod ~10 min WorkManagera, jak kopia); bezgłowy silnik Fluttera z wejściem
     `backgroundPlansMain`;
   - `lib/net/background_plans.dart` (nowy): otwiera bazę jak kopia w tle, przechodzi `cemeteriesWithoutPlan` (czytane od nowa przed każdym
     cmentarzem — co aplikacja zdążyła pobrać, pomija), `OverpassPlanSource` z granicami z pkt 2, `savePlan`/`saveNotInOsm`; wynik `done`
     (nic nie zostało) albo `retry`;
   - prośba o zadanie: przy wyjściu z aplikacji (`paused`), gdy są cmentarze z punktem bez planu, i po zapisie cmentarza z punktem;
     `BackgroundChannel` dostaje metodę `requestPlans`;
   - aplikacja i zadanie mogą pobrać ten sam cmentarz naraz — `savePlan` nadpisuje wiersz (upsert, sprawdza punkt), więc szkody nie ma, a
     koszt to jedno zapytanie więcej; **bez** `DataLock` (to zwykły zapis jak edycja w aplikacji, nie kopia ani odtworzenie);
   - plan zapisany w tle wchodzi do kopii ([[ADR-015-cemetery-plan-in-database]]) — `dev` sprawdza, czy zapis w tle zamawia kopię tak jak zapis
     w aplikacji; jeśli nie — `BackupWorker.request` po zapisanym planie;
   - **`am force-stop` zatrzymuje zadania WorkManagera** — na emulatorze „zamknięcie aplikacji” = wyjście do ekranu głównego i usunięcie z
     ostatnich, nie `force-stop`.
   Koszt B1: ok. 0,5 dnia ponad resztę (pozycja ok. 1,5 dnia zamiast 1). Przy liście autora (ok. 15 min pobierania, *Why*) granica 9 min na
   przebieg znaczy dwa–trzy przebiegi: gdy przebieg zapisał plany, a coś zostało — od razu następny (jak `again` w kopii); gdy serwer nic nie
   dał — `retry` i ponawianie wykładnicze. Uprawnienia: bez nowych (`INTERNET` jest; WorkManager już w aplikacji).
7. **Wydanie:** `1.0.1+4` (README `grobing-code` → *Wydanie*: następna wysyłka ≥ 4), paczka `.aab` poza repo; wgranie w Play Console — autor.
   README → nowy akapit o granicach czasu i ponawianiu (sieć: [[NFR-005-dane-nie-opuszczaja-telefonu]] — adresy bez zmian).

### Files (likely)
`grobing-code`: `lib/app/home/cemetery_base.dart` · `lib/app/home/cemetery_card.dart` · `lib/app/home/cemetery_search.dart` ·
`lib/app/home/home_screen.dart` · `lib/data/cemeteries.dart` · `lib/net/overpass_plan_source.dart` · `lib/app/map/plan_downloads.dart` ·
`lib/app/grave/plan_placeholder.dart` · `lib/app/grave/cemetery_screen.dart` · `lib/app/grobing_app.dart` · `pubspec.yaml` (wersja) ·
`README.md`; **B1:** `android/app/src/main/kotlin/com/grobing/app/PlanWorker.kt` (nowy) · `BackgroundBackup.kt` (metoda kanału) ·
`lib/net/background_plans.dart` (nowy) · `lib/main.dart` (wejście `backgroundPlansMain`) · `lib/backup/background.dart` (prośba).
Testy (`qa`): `test/` — wyszukiwanie na małej wymyślonej bazie, zaślepka, ponawianie z podstawionym zegarem i źródłem, zapytanie podsumowań,
przebieg w tle z podstawionym źródłem.

### AC → test / check
| AC | Test (`qa`) | Na emulatorze (agent) |
|---|---|---|
| AC-1 „przy:” i kolejność | baza: „Cmentarz parafialny” w „Zmyślonce” z „Wymyślów” w okolicy, cmentarz w „Wymyślowie”, cmentarz „…Wymyślowice”; „wymyslow” → kolejność i „przy: Wymyślów”; regresje z D36 („powazki”, „parafialny”) na wymyślonych odpowiednikach | wyszukanie cmentarza we wsi z pomiaru po nazwie wsi → karta z „przy:”, w pierwszych 30 (nazwy do vaulta nie trafiają) |
| AC-2 wolny serwer | źródło z podstawionym klientem, który odpowiada po czasie dłuższym niż stara granica (skalowane granice w teście) → `PlanFound`; zaślepka: linia po 15 s | dodanie dużego cmentarza miejskiego z prawdziwym serwerem → czas do planu, zrzut (a) z trzecią linią |
| AC-3 przeciążony i ponowienie | brak odpowiedzi → (c) z nowym tekstem; zegar +2 min → próba sama → plan; wyjście z ekranu nie przerywa; **B1:** przebieg w tle z podstawionym źródłem → plan zapisany, wynik `done`/`retry` | **B1:** tryb samolotowy → dodanie cmentarza → wyjście z aplikacji (bez `force-stop`) → sieć włączona → po kilku min plan jest bez otwierania (zrzut arkusza „Plan offline”) |
| AC-4 offline (regresja) | istniejące testy US-007 AC-1 | tryb samolotowy → cmentarz z planem → plan i „Plan offline” |
| D37 stan planu | zapytanie podsumowań: brak · plan · brak w OSM; `cemeteryLine` | lista „Twoje cmentarze” z pustym tekstem: „· bez planu” tylko przy cmentarzu bez planu |

**Warstwa danych:** schematu nie zmienia, więc testu migracji nie ma. **Odtworzenie z kopii:** kopia z cmentarzem bez planu → po odtworzeniu
plan schodzi sam (w B1 także w tle) — `qa` na emulatorze, bo to ścieżka nowego telefonu ([[cmentarz]] *Open*, „czy plan wchodzi do kopii”).
**Dane rodziny:** emulator `Grobing_Restore` trzyma demo dla znajomych — przed testami stan sprzed demo z `_pokaz`, nigdy `pm clear` bez
zapisanego tar; cmentarze dodawane na emulatorze to publiczne cmentarze z bazy, a do vaulta trafiają **opisy, nie nazwy**.

### Manual verification (stop #2)
**Agent na emulatorze** (przed stopem, ze zrzutami): wiersze kolumny „Na emulatorze” wyżej + przegląd `ui` (subagent) karty z „przy:”, linii
planu w arkuszu i zaślepki przy 200% na 360 dp.

**Autor — odczucie (emulator, najwyżej 3):**
1. *emulator* — wpisz nazwę wsi z Grobonetu, której dziś nie znalazłeś: czy rozpoznajesz swój cmentarz na karcie z „przy: …”?
2. *emulator* — otwórz cmentarz, którego plan właśnie się pobiera: czy tekst (a) mówi wystarczająco, żeby spokojnie wyjść?

**Po wydaniu, na telefonie (lista A — gotowość na wyjazd, nie stop #2):** w domu, na Wi-Fi — dodaj cmentarze z listy wyjazdowej; po ok. 15 min
lista „Twoje cmentarze” bez „· bez planu”; tryb samolotowy → dwa z nich → plan jest. Agent może to sprawdzić przez USB (tylko odczyt: zrzut
ekranu), jeśli podłączysz telefon.

### Out of scope
- plan zarządcy jako obraz i dopasowanie dwoma punktami; plany wbudowane (opcja C) — po wizycie (*Out of scope — decided after the visit*);
- odmiana nazw miejscowości w bazie (miejscownik z wyciągu) — [[cmentarze]] D36 *Obali*;
- pozostałe tematy wyszukiwania z [[ISSUE-015-add-cemetery-from-database]] → *Notes* (literówki z OSM, cmentarze dla zwierząt, próg 6 liter);
- trzecia instancja Overpass — w pomiarze 2026-10-22 żadna z dwóch dodatkowych nie odpowiedziała; nowy adres to decyzja autora (`hosts.dart`);
- zmiana wyglądu mapy cmentarza przy 200% (*Poza tą kolejnością* w `CURRENT_STATE.md`).

## Dev report (`dev`, 2026-10-22)
Flutter 3.41.1 (przypięty). `flutter analyze` — czysto; `dart format` — czysto. Istniejące testy: 987 zielonych, **3 czerwone — wszystkie
sprawdzają zachowanie, które pozycja zmienia celowo** (do poprawy przez `qa`): stary tekst (c) „Spróbuję znowu później” (2 testy w
`cemetery_map_screen_test.dart`) i stara kolejność D8 w `cemetery_base_test.dart` (zastąpiona przez D36). Bez zmiany schematu (v15).

### Done (plan pkt 1–7)
1. `CemeteryBase.search` — klucz D36 (całe słowa → najdalsze pole → mniej pól, zachłannie → alfabet), słowa pól liczone przy pierwszym trafieniu
   i trzymane; `foundThrough` + „· przy: …” w `BaseCemeteryCard`. Sonda w Pythonie odtwarzająca kod 1:1 daje pozycje z [[cmentarze]] D36 co do
   miejsca (wieś 25 → 2, miejscownik 402 → 27, „parafialny” + miejscownik 86 → 13, wieś z 3-literowym rdzeniem 102 → 4, miasto 47 → 14).
2. `OverpassPlanSource`: 120 s na zapytanie, 5 min na próbę.
3. `PlanDownloads`: stan `slow` po 15 s (dla wszystkich w kolejce, aż kolejka się opróżni), ponawianie po (c) po 2, 5, 10, potem co 15 min.
4. Zaślepka 2a v9 (B1).
5. `CemeterySummary.plan` (odczyt `cemetery_plans`), „· bez planu” / „· bez planu w OSM” na liście, linia planu w arkuszu.
6. **B1:** `PlanWorker.kt` (WorkManager, warunek sieć, `KEEP`, ponawianie od 5 min, 14 prób), `lib/net/background_plans.dart`, wejście
   `backgroundPlansMain`, metoda kanału `requestPlans`; prośba przy wyjściu z aplikacji, gdy brakuje planów; po powrocie — gdy brakuje mniej
   niż przy wyjściu — tabela planów oznaczona jako zmieniona (ekrany czytają od nowa, kopia w tle słyszy zmianę); przebieg w tle po zapisie
   planu prosi o kopię.
7. `1.0.1+4`, README → *Mapa cmentarza i sieć* (granice, ponawianie, praca w tle, pułapka `force-stop`).

### Found on the emulator (fixed)
- **Proces z pracą w tle zamrożony przez Androida → plan nigdy nie schodzi** (API 36, `Grobing_Restore`). Po zabiciu procesu (`am kill` =
  `USER REQUESTED`) następny start WorkManagera uznaje aplikację za wymuszenie zatrzymaną, przestawia zadania, systemowe zadanie się kończy, a
  pracę uruchamia planista WorkManagera **w procesie**, bez zadania systemu — `ActivityManager: freezing … com.grobing.app` po 10 s, w systemie
  nie ma już zadania, proces `isFrozen=true` do otwarcia aplikacji. Przesunięcie aplikacji z ostatnich na telefonie najpewniej daje ten sam
  powód wyjścia. **Poprawka:** `PlanWorker` sprawdza, kto go uruchomił — start systemu niesie sprawdzoną sieć (`network`), start w procesie nie;
  start w procesie oddaje pracę systemowi (`retry`). Do tego opóźnienie startu 60 s po wyjściu i 30 s między przebiegami, żeby od razu startował
  system, a nie planista w procesie opuszczanej aplikacji (bez tego każdy zwykły wyjazd z aplikacji kosztował 5 min i jedną próbę).
- **Dwuczłonowa nazwa po „przy:” łamała się w środku przy 200%** — nazwa okolicznej miejscowości spięta twardymi spacjami (jak separatory, D25).

### Measurements (emulator `Grobing_Restore`, profile, prawdziwy serwer Overpass, 2026-10-22 wieczorem)
| Przypadek | Wynik |
|---|---|
| AC-1 — nazwa wsi z Grobonetu | cmentarz wsi 2. z 51, karta „Cmentarz parafialny · <przysiółek> · przy: <wieś> · woj. …” |
| AC-2 — duży cmentarz miejski, otwarty ekran | po 15 s linia „odpowiada dziś wolno”; plan po ok. 75 s od zapisu (stara wersja: błąd po ok. 60 s) |
| AC-3 / B1 — dodany bez sieci, aplikacja zamknięta (wyjście + zabity proces), potem sieć | zadanie czeka w systemie na sieć; po włączeniu sieci start w procesie → `retry` (bramka) → systemowy start → `SUCCESS` po 60 s, baza 192 → 295 KB przy zamkniętej aplikacji; **gotowe zadanie po ponowieniu czekało w systemie 6+ min mimo spełnionych warunków** — uruchomione `cmd jobscheduler run` (kiedy, decyduje Android) |
| B1 — zwykły domowy przypadek: sieć jest, dodanie i od razu wyjście (bez zabijania) | wyjście 21:31:54 → proces zamrożony 21:33:05 → systemowy start `PlanWorker` 21:33:40 → `SUCCESS` 21:35:12; **3,5 min od zapisu do planu, bez otwierania aplikacji** |
| AC-4 — tryb samolotowy po pobraniu w tle | arkusz „Plan offline”, plan na ekranie, lista bez „· bez planu” |
| D37 | lista: „· bez planu” tylko przy cmentarzu bez planu; arkusz: „Pobieram plan…”, „Plan pobierze się, gdy będzie internet.”, „Plan offline” |
| 200% na 360 × 640 dp | karta z „przy:” — czytelna; zaślepka (a) — **mieści się tylko pierwsza linia**, reszta pod paskiem grobów (znana luka ekranu przy 200%, *Poza tą kolejnością* w `CURRENT_STATE.md`); arkusz i czytnik mówią całość |

Stan (c) („przeciążony”) tylko testami — na emulatorze bez roota nie da się wywołać odpowiedzi serwera inaczej niż jej brakiem.

### Deviations (dla przeglądu `ui`)
1. **(a) przy wolnym serwerze: jedna linia zamiast trzech** — „Serwer map odpowiada dziś wolno. Plan zapisze się sam i zostanie w telefonie —
   możesz zamknąć aplikację.” zastępuje zdanie D41, zamiast dochodzić jako trzecia (przy 200% na 360 dp trzecia nie miała gdzie stanąć).
2. **Ikona linii planu w arkuszu 18 dp**, jak linia liczb obok (specyfikacja: „jak linia liczb … ikona 20 dp” — sama sobie przeczy).
3. **Opóźnienie startu pracy w tle (60 s / 30 s) i bramka startu w procesie** — poza planem, z przejścia (*Found*).

### Found, poza pozycją
- **`BackupWorker` ma tę samą ekspozycję** (praca uruchomiona w procesie po przestawieniu zadań może zostać zamrożona). Kopia przeszła na
  telefonie ([[ISSUE-032-mvp-install]]), ale bez sprawdzenia po przesunięciu aplikacji z ostatnich. Kandydat na małą pozycję albo wiersz listy A.
- **APK profile rośnie przy buildach przyrostowych** (43,8 → 58,9 MB przy tych samych 45,8 MB wpisów) — dziury po pakowaniu Gradle; `appbundle`
  do sklepu pakuje się od zera.

### Manual steps for `qa`
Jak *Implementation plan* → *Manual verification*; emulator `Grobing_Restore` ma teraz stan sprzed demo z `_pokaz` + build ISSUE-052 i 5 dodanych
publicznych cmentarzy z bazy (opisy, nie nazwy — `family-data.md`); stan demo sprzed pozycji zapisany w katalogu sesji (`emu052/stan-przed-052.*`).
Na zakończenie łańcucha — wgrać demo z powrotem.

## Verification (`qa`, 2026-10-23)
**Rytuał:** `dart format` — czysto · `flutter analyze` — czysto · `flutter test --timeout 120s` — **1016 zielonych** (przed pozycją 990; 3 stare
testy poprawione na zmienione zachowanie, 26 nowych).

### AC → test
| AC | Testy | Wynik |
|---|---|---|
| AC-1 „przy:” i kolejność | `cemetery_base_test.dart` — D36 (zastępuje D8: całe słowo przed rdzeniem), kolejność nazwa → miejscowość karty → okolica → środek słowa, jedno pole przed rozrzuconymi, `foundThrough` (najwięcej słów, nie pierwszy rdzeń; nic, gdy karta mieści słowa; dzielnica liczy się jak karta), regresje na prawdziwym wyciągu (Powązki w Warszawie pierwsze, „krakow” — Kraków pierwszy); `plan_line_and_through_test.dart` — karta „· przy: …”, spięcie nazwy tylko gdy się mieści (D38) | zielone; na emulatorze cmentarz wsi z pomiaru 2. z 51 z „przy: <wieś>” |
| AC-2 wolny serwer | `overpass_plan_source_test.dart` — domyślne granice 120 s / 5 min; `plan_downloads_test.dart` — stan `slow` po `slowAfter` dla bieżącego i czekających, nowa kolejka znowu „downloading”; `cemetery_map_screen_test.dart` — (a) z linią „odpowiada dziś wolno” po 15 s, jedno zdanie zamiast trzech | zielone; emulator: plan po ok. 75 s |
| AC-3 przeciążony i ponowienie, B1 | `plan_downloads_test.dart` — ponowienie samo po pierwszej przerwie, przerwy rosną, plan zapisany w tle nie jest pytany drugi raz, `close()` kasuje czekające; `cemetery_map_screen_test.dart` — (c) „Serwer map jest teraz przeciążony.” + „Spróbuję sam…”; `background_plans_test.dart` — przebieg w tle: wszystkie, błąd jednego → `retry`, brak sieci → `retry`, `again` po czasie, brakujące czytane przed każdym cmentarzem, znacznik odtworzenia / inna wersja schematu → `done` bez pytania, kopia po zapisie; `background_plans_app_test.dart` — wyjście z aplikacji z brakującym planem prosi o pracę w tle, bez braków nie prosi; po powrocie plan zapisany innym połączeniem widać w arkuszu („Plan offline”) | zielone; emulator: dwa przebiegi z zamkniętą aplikacją (*Dev report* → *Measurements*) |
| AC-4 offline (regresja) | istniejące testy US-007 AC-1 | zielone; emulator: tryb samolotowy, plan z tła jest |
| D37 stan planu | `cemeteries_test.dart` — `CemeterySummary.plan` (nic · plan · brak w OSM, nowa wartość po zapisie), `cemeteryLine` („· bez planu”, „· bez planu w OSM”, arkusz grupy bez stanu); `plan_line_and_through_test.dart` — arkusz „Plan offline”, „W OpenStreetMap nie ma planu.”, „Pobieram plan…”, „Bez planu — pobierze się sam.”, lista „· bez planu” | zielone |

**Dostępność dotyku** (retro 3, R2): `meetsGuideline(androidTapTargetGuideline)`, `labeledTapTargetGuideline` i `expectEveryButtonTappable` na
wynikach wyszukiwania i w arkuszu — zielone. Zaślepka 2a — cele z ISSUE-027 bez zmian (`Pobierz teraz` 48 × 48).

**Warstwa danych:** schemat bez zmian (v15), więc testu migracji nie ma. Kopia i odtworzenie bez zmian (plan w kopii — [[ADR-015-cemetery-plan-in-database]]);
istniejące testy odtworzenia zielone. Po odtworzeniu brakujące plany pobiera start aplikacji (ISSUE-027), a po wyjściu z niej — praca w tle.

### Przegląd `ui` (subagent, 2026-10-23)
**0 BLOCKER · 0 MAJOR · 4 MINOR** — wszystkie reguła 6 (łamanie linii), **poprawione przed stopem**:
1. spięta twardymi spacjami długa nazwa po „przy:” łamałaby się w środku słowa → spięcie tylko gdy całe „· przy: <nazwa>” mieści się w linii
   (pomiar `TextPainter` w stylu i skali karty), inaczej zwykłe spacje ([[cmentarze]] D38);
2. „woj.” na końcu linii (od ISSUE-015) → twarda spacja po „woj.” na karcie z bazy (podgląd 14 bez zmian — poza zakresem);
3. „·” na końcu linii w linii liczb arkusza i na liście „Twoje cmentarze” → `·` + twarda spacja (jak `joinPlaceLine`); adres grobu (`polish.dart`) — poza zakresem;
4. brak twardych spacji po jednoliterowych słowach w nowych tekstach → „w telefonie”, „i zostanie”, „W OpenStreetMap” z twardą spacją.

Przyjęte odstępstwa `dev`: (a) przy wolnym serwerze jedno zdanie zamiast trzeciej linii ([[cmentarz]] v9.1, D42); ikona linii planu 18 dp
([[cmentarze]] v2.9, D38); opóźnienie i bramka pracy w tle (zachowanie, bez zmiany specyfikacji). Kontrast z `theme.dart`: linie pomocnicze 5,01:1 na
powierzchni, teksty 2a 10,98:1 na tle (W2). Znana luka zostaje: przy 200% na 360 × 640 dp w 2a widać tylko pierwszą linię (*Poza tą kolejnością*).

### Family data
- **Skan zmian przed `git add`** (nazwy z listy wyjazdowej autora z czatu, regex po rdzeniach): **trzy trafienia w komentarzach kodu `dev`**
  (`cemetery_base.dart` — przykłady podziału słów i pomiaru kolejności z nazwami miejsc autora) → zamienione na wymyślone rdzenie przed jakimkolwiek
  `git add`; po poprawce zero trafień w kodzie, testach i vaulcie. Testy i przykłady — tylko rdzenie Wymyśl-/Zmyśl-/Testow-/Przykład-; prawdziwy wyciąg
  testowany tylko na publicznych cmentarzach, których testy już używały.
- Logcat aplikacji na emulatorze (build profile, z pobieraniem w tle): **zero współrzędnych i adresów** Overpass / GUGiK (retro 3, R7).
- Uprawnienia APK (`aapt dump permissions`) — **bez zmian** względem wersji sprzed pozycji; adresy w `hosts.dart` bez zmian.
- Zrzuty i stan emulatora tylko w katalogu sesji; na zrzutach publiczne nazwy cmentarzy z bazy OSM.

### Stop #2 — kroki dla autora (emulator `Grobing_Restore`, build z pozycji)
1. *emulator* — „Szukaj cmentarza” → wpisz nazwę wsi z Grobonetu, której nie znalazłeś: czy rozpoznajesz swój cmentarz na karcie z „przy: …”?
2. *emulator* — dodaj dowolny duży cmentarz z bazy i od razu „Otwórz cmentarz”: czy to, co mówi ekran przez pierwsze sekundy i po ok. 15 s, pozwala
   spokojnie wyjść z aplikacji?

Wynik (2026-10-23): autor — **„ok”**, ze śladem na emulatorze: dodany z bazy cmentarz wsi z pomiaru (karta z „przy: …”) i otwarty; o 07:11:40
zadanie w tle `PlanWorker` → `SUCCESS`, baza 295 → 412 KB — plan zapisany przy wyjściu z aplikacji (krok 2). W tej samej wiadomości nowe pytanie
autora o usuwanie cmentarzy i osób → `pm` (poza pozycją).

### Hand checks (dla `docs` → [[ISSUE-032-mvp-install]])
- **A** — po wysłaniu `1.0.1+4` do sklepu: aktualizacja na telefonie, dane i odcisk bez zmian (bez zmiany schematu).
- **A** — gotowość na wyjazd: w domu, na Wi-Fi — cmentarze z listy wyjazdowej dodane, aplikacja zamknięta; po kilkunastu minutach lista „Twoje cmentarze”
  bez „· bez planu”; tryb samolotowy → dwa z nich → plan jest. (Agent może sprawdzić przez USB, tylko odczyt.)
- **B** — praca w tle po przesunięciu aplikacji z ostatnich na telefonie (na emulatorze sprawdzona po zabiciu procesu; czas uruchomienia gotowego zadania
  decyduje Android — raz 6+ min po ponowieniu).
