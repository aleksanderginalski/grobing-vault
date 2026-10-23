---
screen: "Mapa migracji — gdzie kto mieszkał w danym roku i jak się przemieszczał (część „Mapa” zakładki Drzewo, w telefonie i na telewizorze)"
items: ["[[ISSUE-045-migration-map]]", "[[ISSUE-050-next-event]]", "[[ISSUE-055-connect-from-the-tree-and-rotate]]"]
us: "n/a — pozycja z `/pm` 2026-10-16 ([[2026-10-16-retro-04]] → *Product decisions*), bez US; [[EPIC-003-zrozumienie]] (widok 5 — czas, M10)"
journey-step: "widok 5 (M10 — czas); dane z [[zamieszkanie]]"
mockup: "2026-10-19: mapa-050.html (ISSUE-050: ⏭ i podpis przeprowadzki, M1–M2; mapa z makiety ISSUE-045 w stanie po v1.4 — bez nazw, bez śladu, K2, kadr z gestów; z mapa-045.js, mapa-050-add.js i world.js obok) — katalog tymczasowy sesji `ef3f4405-…\\scratchpad`, obok drzewo-050.html; 2026-10-17: mapa-045.html (z mapa-045.js i world.js obok) — katalog tymczasowy sesji `40086651-…\\scratchpad`; link file:/// w ISSUE-045 → Implementation plan; zrzuty `shots\\`. Kandydaci v1: W1–W2, K1–K2, O1–O2, D1–D2, R1–R3 na wymyślonej rodzinie (16 osób). Wybrane O3 i R4 (v1.1) są tylko w tej specyfikacji — makieta pokazuje W2, K2 i D2"
updated: 2026-10-23
---

# Mapa migracji — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.36 — reguła 13, mapa świata) · referencja: [[references]] → **R1** (ciemny ląd) i **R3**
> (suwak lat, przełącznik segmentowy u góry).
>
> **Wersja 1 (2026-10-17, `ui` przed planem [[ISSUE-045-migration-map]]).** Cel autora — odpowiedź na pytanie „po co dziś” (retro 4, R1) w `/pm`
> 2026-10-17: **„na wyjazd”**. Mapa ma pokazać rodzinie na telewizorze w trakcie wyjazdu na Wszystkich Świętych, kto gdzie mieszkał i jak się
> przemieszczał, więc wchodzi przed instalacją ze sklepu (najpóźniej 2026-10-29). Pięć wyborów na makiecie (W, K, O, D, R) z rekomendacją W2 K1 O1 D1 R3.
>
> **Wersja 1.1 (2026-10-17, stop #1 — decyzja autora).** Autor: *„W 2 · K 2 · O tutaj tylko środek tego kraju, bez okręgu lub zaznaczonych krawędzi ·
> D 2 · R Tutaj Kadr wybrany przez usera, jeżeli tylko polskę sobie przybliże to widzę tylko to co się dzieje w polsce a ludzie którzy migrują wpadają
> „zza kadru””*. Przyjęte: **W2** (przełącznik „Drzewo | Mapa”), **K2** (osoba po śmierci znika — mapa bez cmentarzy), **O3** — nowy wariant autora
> (osoba w punkcie nazwy kraju, bez obszaru i bez zaznaczonej granicy), **D2** (drogę widać tylko w ruchu), **R4** — nowy wariant autora (kadr tylko z
> Twoich gestów, bez dopasowywania i bez plakietek przy krawędzi). Mapa jest przez to prostsza niż v1: z elementów v1 odpadają znicze (5), obszar kraju (6),
> linia drogi (7) i plakietki (10). Numery elementów zostają, żeby plan i testy dalej się zgadzały.
>
> **Wersja 1.2 (2026-10-17, przegląd `ui` zbudowanego ekranu [[ISSUE-045-migration-map]]).** Dwa źródła zmian:
> - **Decyzja autora w trakcie przeglądu** (D18): *„Tak naprawdę nie potrzebuje żadnych nazw krajów ani miejscowości, wystarczą awatary i kontury
>   krajów”*. Z mapy znikają nazwy krajów (2), podpisy miejsc pod stosami (4), podpis skupienia („5 miejsc”) i podpis „Francja · cały kraj” (6). Plakietka
>   „+N” zostaje. Czytnik dalej słyszy miejsce. **Imiona w rozsunięciu (9) i linia karty (12) zostają — do potwierdzenia na stopie #2** (`qa` pyta autora).
> - **Przyjęte odstępstwa `dev`** (*Dev report* → *Deviations*): 1 — skupienia miejsc (D19), 4 — podwójne dotknięcie o jeden poziom mapy (D23), 5 — przełącznik
>   tego samego kształtu w obu częściach (D20), 6 — dotknięcie osoby w środku otwiera jej widok (D21), 7 — pierwszy kadr najwyżej do poziomu 5 (D22).
>   Odstępstwo 3 (ląd rysowany raz do obrazu, gdy kamera stoi) to technika bez zmiany wyglądu, więc nie wchodzi do specyfikacji (dom: README `grobing-code` →
>   *Mapa*). Odstępstwo 2 (podpisy bez nakładania) jest nieaktualne po D18. Odstępstwo 8 („+N” przy nowym miejscu przed okręgami) to usterka, nie zmiana
>   specyfikacji.
> - **Z przeglądu, poza listą `dev`:** inicjały w kolorze tekstu jak w węźle drzewa (4), osoba w środku z niepewną datą — przerywany pierścień w akcencie
>   (4), ślad osoby w środku w akcencie przy kryciu 90% (8). **Poprawka specyfikacji:** ikona „Mapa” i „Pokaż na mapie” to `public_outlined`, a nie
>   `public` (v1–v1.1) — [[style-b]] reguła 3, cienkie ikony.
>
> **Wersja 1.3 (2026-10-17, ponowny przegląd `ui` zbudowanej [[ISSUE-045-migration-map]] — odstępstwo 9 `dev` przyjęte, D24):** przełącznik „Drzewo ·
> Mapa” w sterowaniu trybu prezentacji (13) stoi **na środku miejsca między rokiem w rogu a „Zakończ prezentację”**, a nie na środku ekranu; gdy napisy się tam
> nie mieszczą — same ikony. Powód: przy tekście 200% na telefonie trzymanym poziomo przełącznik na środku ekranu wchodził pod „Zakończ” (test `qa`, runda 4).
> Ta sama zmiana w [[drzewo]] v1.22 (element 11). [[style-b]] bez zmian.
>
> **Wersja 1.4 (2026-10-17, stop #2 [[ISSUE-045-migration-map]] — decyzja autora, D25):** *„Dodatkowo chciałbym aby po prostu się te avatary przemieszczały płynnie po mapie bez tych linii szarych (nie ma potrzeby żadnego dodatkowego efektu)”*. Przeprowadzka to sam
> przejazd okręgu — **bez śladu** (8). Z tabeli kontrastu schodzą dwa wiersze śladu, z reguły 1 — ślad osoby w środku. **Awatary (D26):** *„Dlaczego zamiast Avatar jest "Ja" chciałbym żeby były tam avatary zamiast inicjałów”* →
> na mapie zdjęcie profilowe u każdego, kto je ma, także u „ja” zamiast znaku „Ja”; bez zdjęcia inicjały (4). Drzewo i lista osób bez zmian (D14, [[osoby]] D4).
>
> **Wersja 1.5 (2026-10-19, `ui` przed planem [[ISSUE-050-next-event]]; decyzja autora na stopie #1 tego dnia — *„tak”*: M2, zapis bez zmian).** Cel autora z `/pm` tego dnia: **(a) opowiadanie rodzinie przy telewizorze**. ⏭ „Następne” zaraz za
> ▶ — ten sam co w drzewie ([[drzewo]] v1.26, element 6a) — na mapie przeskakuje do najbliższego roku z **przeprowadzką** (nowy element 15); okręgi jadą jak przy ▶, kadr stoi (R4). Na stop #1
> (*Open* 6, makieta `mapa-050.html`): **M2** — podpis mówi, kto, skąd i dokąd („Kazimierz Wymyślony: Zmyślin → Francja”), choć na samej mapie nazw dalej nie ma (D18). Element 15, 12, 13,
> *States* i *AC → element* są zapisane według rekomendacji; przy M1 `ui` zmienia je przed planem.
>
> **Wersja 1.6 (2026-10-19, stop #2 [[ISSUE-050-next-event]], runda 1 — prośba autora i decyzja *„B”*):** autor na emulatorze: *„Niech zostaną te informacje (z wyjątkiem pokazywania na
> telewizorze) i tak samo aby te avatary "lśniały" gdy coś się zmienia”*. Jak w drzewie ([[drzewo]] v1.28): **w trybie prezentacji podpis to drobna linia na listwie** nad rzędem ▶ ⏭,
> znika z listwą po 5 s ([[drzewo]] D72 — pod rokiem nic nie stoi); na telefonie dymek bez zmian. **Przeprowadzający się świecą** — pierścień w akcencie i poświata pod okręgiem, trzy pulsy,
> potem stała, dopóki stoi podpis; w stosie idą na przód, więc świecą ich własne okręgi, a „+N” świeci tylko przy więcej niż trzech (D30). Elementy 13 i 15, *States*, *Style B rules applied*, *AC → element*.

> **Wersja 1.7 (2026-10-23, `ui` przed planem [[ISSUE-055-connect-from-the-tree-and-rotate]]; decyzja autora na prototypie — panel 5, *„tak”*):** część „Mapa” dostaje
> przycisk **„Obróć”** w pasku i ten sam **układ poziomy L4 „bez zakładek”** co drzewo ([[drzewo]] 12, D76, D77, D82): przełącznik i ikony w górnym rzędzie nad mapą, karta
> z linią „gdzie” i czasem w dolnym pasku, bez zakładek (D31). Zmienione: element 1, *States*. Tryb prezentacji (13) bez zmian.

## Purpose
Zbierający pokazuje rodzinie, **gdzie kto mieszkał w wybranym roku** i **jak się przemieszczał**: przeprowadzki i wyjazdy za granicę. Robi to tym samym
suwakiem lat, tempem i trybem prezentacji co historia na drzewie ([[US-010-czas-na-drzewie]], [[ISSUE-038-history-on-tv-and-tempo]]). Przybliża to,
co chce pokazać (np. samą Polskę), a kto wyjeżdża albo przyjeżdża, wylatuje poza kadr albo wpada zza niego. Na co dzień widzi też, komu brakuje miejsca
w danym roku, czyli o co zapytać babcię.

## Prior art
- **Jedna osoba, miejsce po miejscu:** Legacy Family Tree, „Migration Mapping”, animuje drogę przodka: *„Legacy animates the ancestor's movement
  through time. Watch how they migrated from place to place.”* Pokaz idzie *„one place at a time at 1 second intervals”*
  ([Genea-Musings, 2013](https://www.geneamusings.com/2013/12/first-look-at-legacy-family-tree_18.html), odczyt 2026-10-17). Odpowiednik: osoba w środku
  i ▶ — droga widoczna w ruchu (D2 autora).
- **Cała rodzina w czasie:** Heredis, „Family Tree Mapping — By period”: *„A timeline will be displayed above the map”*, *„Click on the Play button and watch
  the events appear on the map through each time period”*, a powiększanie jest w rękach użytkownika: *„Press the Pause button to be able to zoom in and zoom out
  as you please”* ([Heredis Help](https://help.heredis.com/en/wp-json/wp/v2/posts/13419), odczyt 2026-10-17). Odpowiednik: suwak drzewa i kadr z Twoich
  gestów (R4 autora).
- **Kilka znaczników w jednym miejscu:** Leaflet.markercluster: *„When you click a cluster at the bottom zoom level we spiderfy it so you can see all
  of its markers.”* ([README](https://github.com/Leaflet/Leaflet.markercluster), odczyt 2026-10-17). Odpowiednik: rozsunięcie stosu (9). Osoby z
  jednej miejscowości mają ten sam punkt, więc przybliżanie ich nie rozdzieli.
- **Własne konwencje aplikacji:** mapa z wbudowanych danych Natural Earth bez kafelków ([[ADR-007-poland-map-bundled-data]], [[cmentarze]]).
  Niepewność daty niesie przerywany obrys, a nie krycie ([[drzewo]] D32, N3). Pusty koniec pobytu bierze się z następnego miejsca ([[zamieszkanie]] D12).

## Navigation
- **Przełącznik „Drzewo | Mapa”** (W2) u góry zakładki Drzewo zastępuje tytuł „Drzewo” (R3 ma taki przełącznik u góry). **Wspólne dla obu części:**
  osoba w środku, karta (12), rok, tempo, ▶. Przełączenie nie zmienia żadnej z tych rzeczy, a ▶ biegnie dalej.
- **Wejście z dolnego paska** — część „Drzewo”, „Ja” w środku, rok „dziś” (bez zmian, [[drzewo]] D15).
- **„Pokaż na mapie”** w widoku osoby ([[osoba]] 9a, v2.7) → zakładka Drzewo, część „Mapa”, ta osoba w środku, rok „dziś”. Działa jak „Pokaż
  w drzewie”: stos widoku osoby znika ([[drzewo]] D15). **Kadr się nie zmienia** (R4, 10).
- **Dotknięcie osoby na mapie** → ona w środku (karta, pierścień). **Dotknięcie osoby, która już jest w środku** → jej widok, jak w drzewie (v1.2, D21);
  w trybie prezentacji nic. Dotknięcie stosu kilku osób najpierw je rozsuwa (9), a **skupienia kilku miejsc — przybliża do nich** (4a, D19). **„Pokaż ›” w
  karcie** → [[osoba]], a wstecz wraca na mapę z tym samym środkiem, rokiem i kadrem.
- **„Przesyłaj na telewizor”** → systemowy ekran przesyłania → po powrocie **tryb prezentacji tej części, która była widoczna** (13). W trybie przełącznik
  jest w sterowaniu, więc z drzewa na mapę przechodzi się jednym dotknięciem, bez nowego przesyłania.
- **„Połącz dwie osoby”** zostaje tylko przy części „Drzewo” (D11).
- **Wstecz** z mapy — jak z drzewa: mapa Polski ([[style-b]] reguła 12).
- **⏭ „Następne”** (v1.5, ISSUE-050 — element 15): w części „Mapa” przeskakuje do najbliższego roku z przeprowadzką; reguły jak w drzewie ([[drzewo]] *Navigation*): z „dziś” — pierwsza
  przeprowadzka, po ostatniej — „dziś” i od nowa, zatrzymuje ▶. Przełączenie części zabiera podpis (rok zostaje): przeprowadzki to zdarzenia mapy, a drzewo ma swoje.

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** przełącznik segmentowy **„Drzewo” · „Mapa”** (`account_tree_outlined` · `public_outlined` — v1.2, reguła 3; wysokość 40 dp, cel 48 dp; aktywna część z obrysem 2 dp i ikoną w akcencie, jak segment z R3; czytnik: „Drzewo, zaznaczone” / „Mapa”) · po prawej **„Przesyłaj na telewizor”** jak w [[drzewo]] 1. Przy części „Mapa” bez „Połącz dwie osoby”. **Od v1.7 (D31):** na lewo od „Przesyłaj” — **„Obróć”** jak w [[drzewo]] 1 (D82); w poziomie przełącznik i ikony stoją w górnym rzędzie nad mapą ([[drzewo]] 12). **Tekst ≥ 150%:** przełącznik same ikony z `tooltip` i czytnikiem, gdy napisy nie mieszczą się w pasku części „Drzewo” (z „Połącz dwie osoby” i „Przesyłaj”). **Ten sam kształt w obu częściach** (v1.2, D20): część „Mapa” liczy miejsce tak jak „Drzewo”, więc przełącznik nie zmienia się pod palcem, który właśnie zmienił część | pasek + przełącznik + przycisk-ikona | część → zmiana części · cast → [[drzewo]] *Navigation* | część z wejścia | — | R3 · W2 (autor) |
| 2 | **Mapa świata bez sieci:** Natural Earth, kraje (dzisiejsze granice), rzut jak mapa Polski (Web Mercator `flutter_map`, bez kafelków). **Ląd** — powierzchnia, **morze** — woda, **granice i brzegi** — obrys przy kryciu 70%, 0,7 dp (dekoracja). ~~Nazwy krajów z danymi~~ — **v1.2 (D18, autor): bez nazw krajów** — kraj rozpoznaje się po konturze. Przeciąganie przesuwa, dwa palce przybliżają, **podwójne dotknięcie pustego miejsca przybliża o jeden poziom mapy (×2), jak mapa Polski i plan cmentarza** (v1.2, D23; + / − zostają ×1,45 — 11) | mapa | gesty · + / − (11) | kadr (10) | — | ISSUE-045 AC-4 · [[style-b]] reguła 13 · D1, D14, D18, D23 |
| 3 | **Pigułka u góry mapy:** „W 1950 na mapie: 9 osób · 3 bez miejsca” · „Dziś na mapie: 6 osób” (13 sp, tekst, powierzchnia, 12 dp od góry; bez działania). „Na mapie” to osoby żyjące w tym roku i mające miejsce (także poza kadrem). „Bez miejsca” to osoby żyjące bez miejsca na ten rok; ta część znika przy zerze. Odmiana liczby jak w [[style-b]] reguła 6. Czytnik czyta ją jako region na żywo po zatrzymaniu ▶ i po zmianie roku palcem, jak rok. **Nie ma jej na telewizorze** (13). **v1.5:** gdy stoi podpis roku po ⏭ (15), pigułki nie ma — podpis stoi w jej miejscu, a pigułka wraca, gdy podpis znika | tekst | — | — | — | D7 |
| 4 | **Osoba żyjąca w roku Y w swoim miejscu:** okrąg 32 dp na powierzchni z obrysem 1,5 dp, z profilowym w kadrze albo inicjałami (12 sp, półgrube, **tekst** — v1.2: kolor jak w węźle drzewa, 10,02:1; najwyżej 1,3×); **„Ja”** — jak każdy: profilowe albo inicjały (v1.4, D26 — decyzja autora; ~~znak „Ja” jak w drzewie, [[drzewo]] D14~~); kim jest „ja”, mówi karta („to ja”) i czytnik, a w rozsunięciu imię „Ja” pod okręgiem (9). **Osoba w środku** — pierścień 2,5 dp w akcencie i delikatna poświata ([[style-b]] reguła 2), zawsze na wierzchu. **Okno niepewnej daty** urodzenia albo śmierci (jak N3 w drzewie): przerywany obrys (kreska 4/3); **u osoby w środku przerywany pierścień w akcencie** (v1.2, jak w drzewie). Punkt to środek miejscowości albo, przy samym kraju, punkt jego nazwy (6) — z [[zamieszkanie]], `residences.lat/lon`. ~~Podpis miejsca pod okręgiem~~ — **v1.2 (D18, autor): bez podpisu miejsca**; gdzie osoba jest, mówi karta (12) i czytnik. **Kilka osób w jednym miejscu — stos:** do 3 okręgów co 22 dp (osoba w środku pierwsza, dalej według roku urodzenia) i plakietka „+N” (11 sp, powierzchnia z obrysem). **Cel dotyku:** okrąg 48 dp; stos to jeden cel na całą szerokość. **Dotknięcie osoby w środku** → jej widok (v1.2, D21; nie w trybie prezentacji). Czytnik: „Zofia Wymyślona, Moja prababcia, w 1930 Zmyślin, Polska, dziś Ukraina — w środek” (osoba w środku: „— otwórz”); stos: „Zmyślin: 4 osoby — rozsuń”; kolejność według położenia, z góry i od lewej | znacznik | dotknięcie → osoba w środek · osoba w środku → jej widok · stos → rozsunięcie (9) | — | — | AC-1 · D2, D3, D4, D18, D21 |
| 4a | **Skupienie miejsc** (v1.2, odstępstwo 1 `dev`, D19): miejsca, których stosy (okręgi z „+N”) leżałyby na ekranie na sobie, łączą się w **jeden stos** — do 3 twarzy (najpierw miejsce osoby w środku, potem miejsce z największą liczbą osób) i „+N” z liczbą pozostałych osób; **bez podpisu** (D18). **Dotknięcie przybliża** do jego miejsc (margines 72 dp), a przy największym przybliżeniu (poziom regionu, D1) rozsuwa jak stos (9). Cel dotyku jak stos. Czytnik: „Wymyślowo, Zmyślice i 2 więcej: 12 osób — przybliż” | znacznik | dotknięcie → przybliżenie · przy największym przybliżeniu → rozsunięcie (9) | — | — | Leaflet.markercluster · D19 |
| 5 | ~~Znicz na cmentarzu po śmierci (K1)~~ — **K2 (autor):** osoba **po śmierci znika** z mapy (koniec okna daty śmierci, jak znicz w drzewie), przenikaniem jak w drzewie. Cmentarzy na tej mapie nie ma | — | — | — | — | K2 (autor) · D16 |
| 6 | **Miejsce „cały kraj”** — **O3 (autor):** okrąg osoby **w punkcie nazwy kraju** (ten sam punkt, który zapisało zamieszkanie, `residences.lat/lon`), **bez obszaru, bez koła i bez zaznaczonej granicy**. To, że miejscowość nie jest znana, mówi linia karty (12) i czytnik („Francja, cały kraj”); ~~podpis „Francja · cały kraj”~~ — v1.2, D18: bez podpisu. Obrys okręgu zwykły — przerywany tylko przy niepewnej dacie (4) | znacznik | jak 4 | — | — | O3 (autor) · D15, D18 |
| 7 | ~~Linia drogi osoby w środku (D1)~~ — **D2 (autor):** **drogę widać tylko w ruchu** — okrąg osoby w środku jedzie przy przeprowadzce (8; ~~ślad w akcencie~~ — v1.4, D25). Kolejne miejsca w kolejności lat: ▶ albo suwak, a gdzie osoba jest w danym roku — karta (12) | — | — | — | — | D2 (autor) · D17 |
| 8 | **Przeprowadzka** w roku Y: okrąg **jedzie ze starego miejsca do nowego** (ok. 0,6 s, wolniej na starcie i końcu) — **sam przejazd, bez śladu i bez innego efektu** (v1.4, D25; ~~ślad — linia 2 dp gasnąca w ok. 1,8 s~~). Przejazd startuje z miejsca, w którym okrąg stał (w stosie, w rozsunięciu albo w drodze), a następny rok go nie przerywa. Także z miejsca poza kadrem i poza kadr: okrąg wpada zza krawędzi albo za nią wylatuje (R4). Przy przesuwaniu suwaka palcem — przejście 150 ms. Przy ▶ ruch nie czeka na rok (przy „Szybko” rok ma 50 ms, a przejazd trwa). **Ograniczenie animacji** — od razu (jak [[drzewo]] D36). Pojawienie się i zniknięcie (narodziny, śmierć, miejsce od zera) — przenikanie jak w drzewie | animacja | — | — | — | AC-1, AC-2 · D5, D25 |
| 9 | **Rozsunięcie:** dotknięcie stosu (4) rozkłada osoby na okręgu wokół punktu (promień 34 + 5 × liczba dp, a środki sąsiadów co najmniej 48 dp od siebie). Od punktu idą nóżki w kolorze obrysu, a pod każdym okręgiem jest imię (13 sp, tekst, obwódka w kolorze tła; najwyżej 1,3×) — **v1.2: imiona zostają, do potwierdzenia przez autora na stopie #2** (D18 — to nie nazwy miejsc). Dotknięcie osoby → w środek i złożenie. Dotknięcie pustego miejsca, zmiana roku albo ▶ → złożenie. Czytnik: osoby jak w 4 | rozsunięcie | dotknięcie osoby / pustego | — | — | Leaflet.markercluster · D3 |
| 10 | **Kadr — R4 (autor): wybrany przez Ciebie.** Zmieniają go tylko Twoje gesty i + / −; **ani rok, ani ▶, ani zmiana osoby w środku, ani „Pokaż na mapie” go nie przestawiają**. Kto przeprowadza się poza kadr albo zza niego, wylatuje za krawędź albo wpada zza niej (8). **Pierwszy kadr** po uruchomieniu aplikacji: wszystkie miejsca z danych (wszystkie lata) w kadrze, margines u góry 88 dp (pod pigułką), z boków 64 dp, na dole 52 dp; **przybliżony najwyżej do poziomu 5** (ok. jeden kraj na ekranie telefonu — v1.2, D22), gdy wszystkie miejsca leżą blisko siebie. **Kadr zostaje, dopóki aplikacja działa** (jak tempo, [[drzewo]] D41) — także po przejściu na drzewo i z powrotem; po zamknięciu aplikacji znowu wszystkie miejsca. Bez plakietek przy krawędzi (v1 R3). Gdy nie ma żadnego miejsca — kadr Polski (stan „pusta mapa”) | kadr | gesty · + / − | wszystkie miejsca | — | R4 (autor) · Heredis · D6 |
| 11 | **+ / −** w prawym dolnym rogu mapy (48 dp, powierzchnia z obrysem; ×1,45) — jak w [[drzewo]] 3: alternatywa jednym dotknięciem dla dwóch palców (SC 2.5.1). Przybliżenie najwyżej do poziomu regionu (D1) | przycisk-ikona ×2 | + przybliża · − oddala | — | — | [[style-b]] *Thresholds* → gesty |
| 12 | **Karta osoby w środku** — ta sama co w drzewie ([[drzewo]] 5 i 6: okrąg, imię, „lata · kim jest dla mnie”, „Pokaż ›”, ▶, ⏭ — v1.5, [[drzewo]] 6a, rok początku — przy tekście ≥ 150%, U3, suwak, rok, tempo). **Nowa linia pod „lata · kim jest dla mnie”, tylko w części „Mapa”** (14 sp, tekst, zawija się): „W 1930: Zmyślin, Polska · dziś Ukraina” (z nazwą z tamtego czasu — jak karta zamieszkania, [[zamieszkanie]] 6) · „W 1925: Francja · cały kraj” · „Dziś: Zmyślice, Polska” · „W 1950: nie wiadomo, gdzie mieszka” · „W 1900: przed narodzinami”. **Po śmierci linii nie ma** — lata życia w karcie już to mówią (D16). Twarda spacja po „W” i przed „·” ([[style-b]] reguła 6). Karta jest jedna dla obu części, więc linia pojawia się i znika z przełącznikiem. **v1.2 (D18):** na mapie bez podpisów to jedyne miejsce w telefonie, które mówi słowami, gdzie osoba jest — **linia zostaje, do potwierdzenia przez autora na stopie #2** | karta | „Pokaż ›” → [[osoba]] · ▶ · suwak · tempo | jak w drzewie | — | AC-1, AC-2 · D8 |
| 13 | **Tryb prezentacji mapy** (AC-3) — jak [[drzewo]] 11: poziomo, pełny ekran, bez pigułki (3), + / − i karty. **Rok w lewym górnym rogu** (36 sp, akcent, 48 dp od lewej, L1) — **podpis roku po ⏭ — linia na listwie** (v1.6, 15; B — [[drzewo]] D72; v1.5: pod rokiem, P1 — D64), **listwa** na pusty dotyk (B2, 5 s), „Zakończ prezentację”, tempo, ▶, **⏭** (v1.5), czytnik i „Czas na działanie” bez zmian. **W sterowaniu, u góry, przełącznik „Drzewo · Mapa”** (jak w 1, na powierzchni) — **na środku miejsca między rokiem w rogu a „Zakończ prezentację”** (v1.3, D24): miejsce zaczyna się 12 dp za prawą krawędzią roku w jego najszerszym zapisie przy danym tekście („dziś” albo cztery cyfry, więc przełącznik nie przesuwa się z rokiem) i kończy 12 dp przed „Zakończ”, które stoi po prawej we własnej szerokości. Gdy napisy się tam nie mieszczą — same ikony z `tooltip` (jak w 1); nigdy węższy niż same ikony. W obu częściach ten sam kształt (w trybie nie ma „Połącz dwie osoby”). Przełączenie zostawia rok, ▶ i tempo, a sterowanie zostaje na 5 s. **Kadr:** przy wejściu ten sam obszar co w telefonie, dopasowany do poziomego ekranu (środek bez zmian, cały widoczny wcześniej obszar w kadrze); **przeciąganie i dwa palce działają** (mapa nie ma poziomów, jak drzewo w trybie — [[drzewo]] D16); przy wyjściu kadr wraca do telefonu tak samo. Dotknięcie osoby → ona w środku (jak w drzewie, bez widoku osoby). **v1.2 (D18):** na telewizorze nie ma karty ani podpisów, więc miejsca rozpoznaje się wyłącznie po konturach krajów i twarzach | tryb | jak [[drzewo]] 11 + przełącznik + gesty mapy | część z telefonu | — | AC-3 · [[drzewo]] D38–D42 · W2 (autor) |
| 14 | **„Pokaż na mapie”** w widoku osoby — [[osoba]] 9a (v2.7): przycisk tekstowy w akcencie z ikoną `public_outlined` (v1.2, reguła 3), pod wierszami zamieszkań, do lewej, cel 48 dp. Jest, gdy osoba ma co najmniej jedno zamieszkanie | przycisk tekstowy | → mapa z tą osobą w środku (*Navigation*) | — | — | D10 |
| 15 | **ISSUE-050. „Następne” na mapie — przeprowadzki i podpis (v1.5):** ⏭ ten sam co w drzewie ([[drzewo]] 6a): w karcie i na listwie zaraz za ▶; zatrzymuje ▶ (Z1); z „dziś” — pierwsza przeprowadzka, po ostatniej — „dziś” i podpis „To wszystkie przeprowadzki z datą.”, potem od nowa; najwyżej 4 linie naraz, dalej „Jeszcze 2 w tym roku” i dalszy ciąg tym samym ⏭; podpis zostaje, dopóki rok stoi. **Zdarzenia mapy — tylko przeprowadzki** (D28): rok, w którym osoba żyjąca przechodzi z jednego zapisanego miejsca do innego (D4 — z dwóch pobytów w roku wygrywa późniejszy początek), **całej rodziny**, także poza kadrem — jak pigułka (3). Pierwsze miejsce, zniknięcie po śmierci (K2) i zamieszkanie bez lat to nie przeprowadzka. Data „ok.” na początku pobytu — dopisek „(ok. 1912)”. **Linia (M2 — D27):** „**Kazimierz Wymyślony**: Zmyślin → Francja”; kto jechał tą samą drogą w tym samym roku, stoi w jednej linii: „**Kazimierz Wymyślony**, **Zofia Wymyślona**, **Stanisław Wymyślony** i **Józef Wymyślony**: Zmyślin → Wymyślowo” (D29). Miejsce — nazwa z tamtego czasu, gdy jest zapisana (`Residence.nameThen`, N2 w [[zamieszkanie]]), inaczej nazwa miejscowości; przy „cały kraj” — nazwa kraju; bez „· dziś Ukraina” (to mówi karta, 12). Imiona bez „z d.”, jak w drzewie ([[drzewo]] D61); imię z nazwiskiem trzyma się razem, a strzałka — miejsca docelowego ([[style-b]] reguła 6). **Telefon:** podpis w miejscu pigułki (3), 14 sp, nagłówek „W 1946”. **Tryb prezentacji:** drobna linia na listwie nad rzędem ▶ ⏭ — nagłówek „W 1946” (13 sp, tekst pomocniczy), drogi rozdzielone „ · ” (14 sp, imiona półgrube); znika z listwą po 5 s, pusty dotyk pokazuje ją znowu, dopóki stoi podpis (v1.6, B — [[drzewo]] D72; v1.5: pod rokiem w rogu, 28 sp — D64). **Przeprowadzający się świecą** (v1.6, D30): okręgi osób z linii bieżącej strony dostają pierścień w akcencie 2,5 dp (jak osoba w środku, 4) i poświatę pod okręgiem — trzy pulsy po 1,2 s (krycie 0,30 → 0,65 → 0,30), potem stała 0,30, dopóki stoi podpis ([[drzewo]] D73); świecą w drodze i na nowym miejscu; poświata leży na jednej warstwie pod okręgami, jak w drzewie ([[style-b]] reguła 2 — przegląd `ui` rundy 2: cień w każdym okręgu przerysowywany w każdej klatce pulsu). W stosie (także w skupieniu, 4a) osoby z podpisu idą **na przód**, więc ich okręgi są wśród trzech widocznych i świecą; reszta stosu zachowuje kolejność. Gdy w jednym stosie jest ich więcej niż trzy, świeci też znak „+N” (pierścień w akcencie i poświata), który pojawia się, gdy stos stanie. Rozsunięty stos (9) — świecą okręgi osób z podpisu. Przy ograniczeniu animacji — od razu stała poświata ([[drzewo]] D75). Na telefonie i w trybie prezentacji tak samo ([[drzewo]] D74). **Ruch:** po ⏭ okręgi jadą ze starego miejsca do nowego jak przy ▶ (8, ok. 0,6 s), także zza kadru i poza kadr; **kadr się nie zmienia** (R4 — D29); przy ograniczeniu animacji od razu. Rozsunięcie (9) się składa. Na mapie bez żadnej przeprowadzki z datą ⏭ nie ma ([[drzewo]] D71). **Czytnik:** podpis — region na żywo, jak w drzewie | przycisk-ikona + podpis | ⏭ → następny rok z przeprowadzką (albo dalszy ciąg roku) | — | — | ISSUE-050 AC-2, AC-3 · [[drzewo]] 6a · D27–D29 |

**Dane, których ekran potrzebuje** (dla `planning`, bez zmiany bazy):
- osoby z datą urodzenia i zgonu z dopiskiem, czyli okna życia jak na suwaku drzewa (`tree_time.dart`); „ja”; nazwy pokrewieństwa jak w karcie;
- **wszystkie zamieszkania** z pustym końcem z następnego (`impliedEnds` w `lib/data/residences.dart` — mapa liczy ten sam koniec, nie własny);
- **mapa świata w aplikacji:** Natural Earth admin-0 (domena publiczna; plik 1:10m jest już źródłem mapy Polski i listy miejsc). Uproszczenie i rozmiar zmierzył
  `planning` (ISSUE-045 → *Implementation plan*). Kod kraju `ISO_A2_EH` (w Natural Earth `ISO_A2` bywa `-99`, np. przy Francji i Norwegii) i polska nazwa —
  do nazw krajów (2); **od v1.2 nazw krajów na mapie nie ma (D18)**, więc mapa potrzebuje tylko konturów. Wielokąta „głównego” nie trzeba (O3 nie ma obszaru).

## States
| Stan | Co widać |
|---|---|
| dziś (start) | 1–4, 10–12; rok „dziś”, „Ja” w środku (z „Pokaż na mapie” — ta osoba); pierwszy kadr — wszystkie miejsca |
| rok w przeszłości | 4, 6 według roku: żyjący w swoich miejscach, przy samym kraju w punkcie nazwy; bez podpisów (D18); pigułka z liczbami (3); w karcie „W 1930: …” |
| skupienie (v1.2) | 4a: stosy miejsc leżących na ekranie blisko siebie jako jeden stos z „+N”, bez podpisu; dotknięcie przybliża do nich, przy największym przybliżeniu rozsuwa (9). Typowo w pierwszym kadrze, gdy rodzina mieszka na dwóch kontynentach |
| odtwarzanie (▶) | 8 — okręgi jadą, także zza kadru i poza kadr (bez śladu, D25); rozsunięcie złożone; kadr stoi; pigułka i karta zmieniają się z rokiem, czytnik ogłasza rok dopiero po zatrzymaniu |
| następne — przeprowadzka (v1.5, ISSUE-050) | 15: suwak na roku przeprowadzki, okręgi jadą (8), kadr stoi (R4); w miejscu pigułki dymek „W 1946 / Kazimierz Wymyślony, Zofia Wymyślona, Stanisław Wymyślony i Józef Wymyślony: Zmyślin → Wymyślowo / Bronisława Wymyślona: Litwa → Wymyślowo (ok. 1946)” (makieta) |
| następne — koniec (v1.5, ISSUE-050) | „dziś”, dymek „Dziś / To wszystkie przeprowadzki z datą.”; ⏭ jeszcze raz → pierwsza przeprowadzka |
| następne — świecą (v1.6, ISSUE-050) | 15: okręgi z podpisu — pierścień w akcencie i poświata, trzy pulsy w drodze i na miejscu, potem stała; w stosie na przodzie, a „+N” świeci przy więcej niż trzech (D30); przy ograniczeniu animacji stała poświata od razu |
| tryb prezentacji — podpis (v1.6) | 13: rok w rogu, pod nim nic; na listwie nad rzędem ▶ ⏭ linia „W 1946  Kazimierz Wymyślony, Zofia Wymyślona …: Zmyślin → Wymyślowo · …” 14 sp, 5 s jak po każdym dotknięciu, znika z listwą; przeprowadzający się świecą (D30). Do v1.5 — podpis 28 sp pod rokiem (P1) |
| ograniczenie animacji | ▶ skacze o dekadę jak w drzewie (R2, D36); okręgi przeskakują |
| rozsunięcie | 9 nad stosem; reszta bez zmian |
| osoba w środku bez miejsca w tym roku | 4 bez niej; w karcie „W 1950: nie wiadomo, gdzie mieszka”; pigułka liczy ją w „bez miejsca” |
| osoba w środku przed narodzinami | 4 bez niej; w karcie „W 1900: przed narodzinami” |
| osoba w środku po śmierci | 4 bez niej (przeniknęła); w karcie bez linii miejsca |
| osoba w środku poza kadrem | jej okrąg za krawędzią; karta mówi, gdzie jest; kadr bez zmian (R4) |
| nikt w tym roku | mapa w kadrze, pigułka „W 1880 na mapie: 0 osób · 2 bez miejsca” |
| **pusta mapa** (nikt nie ma zamieszkania) | 1, 2 w kadrze Polski (jak mapa Polski), na środku „Tu pojawią się miejsca, w których mieszkała rodzina. Dodasz je w widoku osoby.” (16 sp, tekst pomocniczy) — bez działania, bo miejsce dodaje się przy konkretnej osobie ([[style-b]] reguła 9 — jak „pusta baza” drzewa); karta (12) bez zmian |
| „ja” niewybrane | jak [[drzewo]] *States*: „Wybierz, która osoba to Ty” w obu częściach; z „Pokaż na mapie” działa, karta bez pokrewieństwa (D19 drzewa) |
| tekst 200% / 360 dp | 1 — przełącznik same ikony, gdy napisy nie mieszczą się w części „Drzewo”, i tak samo w części „Mapa” (D20); 4 — inicjały i „+N” najwyżej 1,3×, 9 — imiona najwyżej 1,3×; 3 zawija się do dwóch linii, łamie się przed „·”; 12 — jak karta drzewa przy 200% ([[drzewo]] D20) |
| tryb prezentacji | 13; rok w rogu, gdy nie jest „dziś”, i zawsze ze sterowaniem; przełącznik na środku miejsca między rokiem a „Zakończ prezentację” (D24) — przy 100% na 914 dp ok. 40 dp na lewo od środka ekranu, przy 200% na 800 dp z napisami (267 dp), 29 dp przed „Zakończ” |
| wczytywanie · błąd odczytu | jak w [[drzewo]] (mapa świata jest w aplikacji, więc zwykle niewidoczne) |
| poziomo (v1.7) | jak [[drzewo]] *States* „poziomo” — mapa w miejscu drzewa, górny rząd nad mapą, dolny pasek z kartą (linia „gdzie”) i czasem, bez zakładek (D31) |

## Sketch
```
TELEFON — rok 1930, w środku Kazimierz, kadr przybliżony na Polskę (R4); v1.2 — bez podpisów (D18)
┌──────────────────────────────────┐
│ [⌘ Drzewo|(◍ Mapa)]          [⌔] │  ← przełącznik (1) · „Przesyłaj na telewizor”
│     ╭─ W 1930 na mapie: 8 osób ─╮│  ← pigułka (3) — liczy też osoby poza kadrem
│                  (BW)            │  ← przy samym kraju: okrąg w punkcie nazwy kraju (6)
│                                  │
│                  (MP)(HP)        │
│                                  │
│                                  │
│                     ((KW))(ZW)(SW)  ← osoba w środku na wierzchu, pierścień w akcencie (4)
│                                  │
│                           [+]    │  ← + / − (11)
│                           [−]    │
│ ╭──────────────────────────────╮ │
│ │(KW) Kazimierz Wymyślony Pokaż›│ │
│ │     ok. 1890 – 1958 · Mój pra… │ │
│ │     W 1930: Zmyślin, Polska ·  │ │  ← nowa linia karty (12)
│ │     dziś Ukraina               │ │
│ │(▶) 1850 ━━━━━━●━━━ 1930 Średnio│ │  ← suwak drzewa bez zmian
│ ╰──────────────────────────────╯ │
│  Mapa      Osoby      Drzewo     │
└──────────────────────────────────┘
  1946 (▶): (KW)(ZW)(SW) jadą z Zmyślina do Wymyślowa, bez śladu (8, D25);
  Józef w 1951 wylatuje za lewą krawędź (do Stanów) — kadr stoi (R4).

TELEWIZOR — tryb prezentacji, 1925, ze sterowaniem (13)
┌────────────────────────────────────────────────────────────────────────┐
│ ┌────┐                 [⌘ Drzewo|(◍ Mapa)]        ┌──────────────────┐ │
│ │1925│                                            │ ✕ Zakończ prezent.│ │
│ └────┘                                (MP)        └──────────────────┘ │
│              (KW)                                                      │
│                                                  (ZW)(SW)              │
│                                                                        │
│  ╭──────────────────────────────────────────────────────────────────╮  │
│  │ (▶) 1850 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━●━━━━━━━━━━━━━━━━━━  Średnio │  │
│  ╰──────────────────────────────────────────────────────────────────╯  │
└────────────────────────────────────────────────────────────────────────┘
```

## Tempo
n/a — ekran do oglądania.

## Style B rules applied
- **Reguła 13 (mapy) — mapa świata** ([[style-b]] v1.35): tylko tokeny, bez własnej palety. Ląd — powierzchnia, morze — woda (1,00:1, więc brzeg niesie
  linia). Granice i brzegi — obrys przy kryciu 70% (2,17:1 na lądzie i na wodzie): **dekoracja**, jak granice sąsiadów na mapie Polski. Znaczenie niosą osoby
  i ich ruch. ~~Podpisy z obwódką w kolorze lądu~~ — **v1.2 (D18, autor): bez podpisów miejsc i nazw krajów**; na mapie z tekstu zostają tylko „+N”, pigułka i
  imiona w rozsunięciu (do potwierdzenia na stopie #2). Stosy, które leżałyby na sobie, łączą się w skupienie (4a, D19) — jak znicze z liczbą na mapie Polski.
- **Reguła 1 (akcent):** pierścień osoby w środku i aktywna część przełącznika — wybór, nie dekoracja (~~ślad przy przeprowadzce~~ — v1.4, D25).
- **Reguła 2:** poświata pod osobą w środku i pod przeprowadzającymi się z podpisu po ⏭ (v1.6, D30 — trzy pulsy, potem stała; [[style-b]] v1.48).
- **Reguła 14:** okrąg to profilowe osoby w kadrze, bez zdjęcia — inicjały.
- **„Następne” (v1.5):** ⏭ i podpis jak w [[drzewo]] v1.26 (*Style B rules applied* → „Następne”): ⏭ w akcencie 8,04:1 na powierzchni, dymek — tekst 10,02:1 i tekst pomocniczy 5,01:1,
  linia podpisu na listwie (v1.6) — tekst 10,02:1 i tekst pomocniczy 5,01:1 na powierzchni, 14 sp ([[drzewo]] D72); pierścień świecących okręgów i „+N” — akcent 8,04:1 na lądzie, który ma kolor powierzchni (8,07:1 na wodzie; SC 1.4.11; przegląd `ui` rundy 2 — w v1.6 było omyłkowo „8,81:1 na lądzie w kolorze tła”), a wobec poświaty tuż przy okręgu ok. 6:1 w stałej i ok. 4:1 w szczycie pulsu (szacunek: na krawędzi okręgu rozmycie ma ok. połowę krycia), puls jak w drzewie (SC 2.2.2, SC 2.3.1 — [[drzewo]] D73). Strzałka „→” w kolorze tekstu. Bez nowych tokenów.
- **Niepewność daty niesie kształt:** przerywany obrys okręgu w oknie daty, jak w drzewie (N3). Niepewność miejsca („cały kraj”) niesie słowo ~~w podpisie i~~ w
  karcie i w czytniku (O3 — decyzja autora; od v1.2 bez podpisu — D18).
- **Reguła 5 i progi:** cele dotyku 48 dp (okrąg, stos, + / −, przełącznik), osoby w rozsunięciu co najmniej 48 dp od siebie. Gest dwoma palcami ma + / − i
  podwójne dotknięcie (SC 2.5.1). Rok na telewizorze 36 sp i 48 dp od krawędzi ([[style-b]] *Thresholds* → tekst dla telewizora).
- **Tokeny:** bez nowych. Pomiar według wzoru WCAG z `theme.dart` (2026-10-17; v1.2 — przeliczony z `theme.dart` przy przeglądzie, ten sam dzień):

| Para | Kontrast | Próg | Wynik |
|---|---|---|---|
| obrys okręgu osoby — na lądzie · na wodzie | 3,10 · 3,11 | 3 (SC 1.4.11) | ✅ |
| inicjały — ~~tekst pomocniczy (5,01)~~ **tekst na powierzchni** (v1.2, jak węzeł drzewa) | 10,02 | 4,5 | ✅ |
| pigułka, „+N”, linia karty — tekst na powierzchni | 10,02 | 4,5 | ✅ |
| ~~„Ja” — akcent na powierzchni~~ | — | — | v1.4: na mapie bez znaku „Ja” (D26) |
| imię w rozsunięciu — tekst z obwódką w kolorze tła | 10,98 | 4,5 | ✅ |
| nóżki rozsunięcia — obrys na lądzie · na wodzie | 3,10 · 3,11 | 3 | ✅ |
| ~~podpis miejsca — tekst na powierzchni (10,02) · nazwa kraju — tekst pomocniczy na lądzie (5,01)~~ | — | — | v1.2: bez podpisów (D18) |
| pierścień osoby w środku — akcent na lądzie · na wodzie | 8,04 · 8,07 | 3 | ✅ |
| ~~ślad osoby w środku — akcent 90% · ślad przeprowadzki — tekst 50%~~ | — | — | v1.4: bez śladu (D25) |
| granice i brzegi — obrys 70% | 2,17 | — | dekoracja (poza SC 1.4.11) |
| *v1, odrzucone:* obszar O1 — tekst 75% (6,18) · koło O2 — tekst 10% (1,23) · droga po Y — akcent 55% (3,34) | — | — | nie budujemy (O3, D2) |

## AC → element
| AC ([[ISSUE-045-migration-map]]) | Element(y) | Jak widać spełnienie |
|---|---|---|
| AC-1 — przesuwam suwak lat → gdzie kto mieszkał w tym roku | 3, 4, 6, 8, 12 | suwak na 1930 (makieta): Kazimierz, Zofia, Stanisław i Józef w Zmyślinie, Marian i Helena w Testowicach, Bronisława w punkcie nazwy Litwy („Litwa · cały kraj” — od v1.2 w karcie i czytniku, bez podpisu na mapie, D18); pigułka „W 1930 na mapie: 8 osób”; przesunięcie na 1946 — okręgi jadą do Wymyślowa (bez śladu, D25) |
| AC-2 — wybieram osobę → jej kolejne miejsca w kolejności lat (**D2: w ruchu**) | 4, 8, 12 | dotknięcie Kazimierza → w środku, pierścień; ▶ od 1880: jego okrąg jedzie Zmyślin → Francja → Zmyślin → Wymyślowo (pierścień w akcencie, bez śladu — D25), a karta mówi miejsce w każdym roku. `docs` przepisuje AC-2 przy zamknięciu: *„Given osoba w środku When odtwarzam ▶ albo przesuwam suwak Then widzę, jak przechodzi przez kolejne miejsca w kolejności lat, a karta mówi, gdzie jest w danym roku”* |
| AC-3 — tryb prezentacji na telewizorze: mapa z rokiem i tempem czytelna jak historia na drzewie | 13 | „Przesyłaj na telewizor” → wstecz: mapa poziomo, rok 36 sp w rogu, pusty dotyk → listwa z ▶ i tempem, przełącznik „Drzewo · Mapa” (zrzut `05-tv-1925` — makieta v1) |
| AC-4 — brak sieci → mapa i punkty działają | 2, 4, 6 | mapa świata w aplikacji (Natural Earth), punkty z bazy (zamieszkania) — tryb samolotowy, ten sam widok |
| [[ISSUE-050-next-event]] AC-2 — ⏭ na mapie: rok z przeprowadzką i kto | 15, 8 | makieta `mapa-050.html`: z „dziś” ⏭ → 1912 „Jan Wymyślony: Zmyślin → Stany Zjednoczone (ok. 1912)”; … → 1923 „Kazimierz Wymyślony: Zmyślin → Francja” — jego okrąg jedzie do punktu nazwy Francji; 1946 — dwie linie (cztery osoby jedną drogą i Bronisława z Litwy) |
| ISSUE-050 AC-3 — to samo na telewizorze | 13, 15 | tryb prezentacji: rok 1946 w rogu, okręgi jadą do Wymyślowa i świecą (D30), kadr stoi; linia podpisu 5 s na listwie — dla autora z telefonu (v1.6, B — [[drzewo]] D72; v1.5: podpis 28 sp pod rokiem, zrzut `m2-tv-1946`) |

## Decisions
- **D1 — mapa świata z wbudowanych danych Natural Earth, dzisiejsze granice, rzut jak mapa Polski.** Pozycja tak ustaliła (AC-4,
  [[ADR-007-poland-map-bundled-data]]), a lista miejsc i punkt kraju już są z Natural Earth ([[zamieszkanie]] D7). Nazwy z tamtego czasu niesie karta
  („Zmyślin, Polska · dziś Ukraina” — N2), a nie granice. Przybliżenie najwyżej do poziomu regionu, bo uproszczona linia robi się kanciasta. *Obali:* autor
  chce na mapie granic sprzed 1945 — wtedy osobne dane granic historycznych (Natural Earth ich nie ma) i osobna pozycja.
- **D2 — osoby, a nie punkty miejscowości.** Na telewizorze rodzina pyta „kto”, więc okrąg z twarzą albo inicjałami, jak węzeł drzewa. Prior art pokazuje
  punkty, bo zaczyna od zdarzeń, a tu zaczynamy od osób. *Obali:* przy prawdziwych danych w jednym miejscu stoi kilkanaście osób, a stos „+12” nic nie
  mówi — wtedy przy miejscu liczba i imiona w rozsunięciu.
- **D3 — stos do 3 + „+N” i rozsunięcie po dotknięciu** (Leaflet.markercluster *spiderfy*). Osoby z jednej miejscowości mają ten sam punkt, więc
  przybliżanie ich nie rozdzieli, a lista w arkuszu zasłoniłaby mapę na telewizorze. *Obali:* autor szuka listy osób z miejsca.
- **D4 — kto gdzie w roku Y:** żyje jak na suwaku drzewa (okno daty niepewnej, N3). Wpisane „Do” obejmuje swój rok, więc „do 1945” i „od 1946” nie
  zostawiają dziury. Puste „Do” kończy się początkiem następnego miejsca ([[zamieszkanie]] D12), a ostatnie — śmiercią. Pobyt z samym „Do” zaczyna się z
  urodzeniem. Z dwóch pobytów w tym samym roku wygrywa późniejszy początek. **Zamieszkanie bez lat nie ma miejsca na osi czasu** — nie stoi na mapie w
  żadnym roku; widać je w widoku osoby ([[ISSUE-045-migration-map]] → *Notes*: „do decyzji przy projekcie mapy”). *Obali:* autor ma wiele zamieszkań bez
  lat i chce je widzieć — wtedy przez całe życie osoby, z przerywanym obrysem.
- **D5 — przeprowadzka widoczna jako ruch:** przejazd ok. 0,6 s i ślad gasnący ok. 1,8 s; przy D2 to jedyny nośnik drogi. Legacy pokazuje miejsce po miejscu z
  przerwą, a tu rok biegnie dalej, więc ruch musi trwać dłużej niż rok przy „Szybko” (50 ms). *Obali:* przy „Szybko” ślady wielu osób naraz robią z mapy
  pajęczynę — wtedy ślad tylko osoby w środku.
- **D6 — kadr z Twoich gestów (R4, decyzja autora; zastępuje rekomendację R3 z v1).** Autor przybliża to, co chce pokazać, a migracje widać jako wylot i wlot
  za krawędź. Pierwszy kadr to wszystkie miejsca, żeby było od czego zacząć; kadr zostaje, dopóki aplikacja działa, bo wieczór z rodziną to jedno ustawienie
  (jak tempo). *Obali:* przy prawdziwych danych autor gubi osoby poza kadrem — wtedy wracają plakietki przy krawędzi z v1 (R3).
- **D7 — pigułka z liczbą osób i „bez miejsca”.** Przy przepisywaniu to lista pytań do babci bez szukania; liczy też osoby poza kadrem, więc mówi o całej
  rodzinie, a nie o tym, co widać. Na telewizorze jej nie ma. *Obali:* autor odbiera to jako wyrzut albo szum — wtedy tylko „na mapie: N osób”.
- **D8 — miejsce w karcie słowami.** Karta mówi, gdzie osoba w środku jest w roku Y — dla czytnika ekranu (mapa jest obrazem), dla osoby poza kadrem (R4) i dla
  AC-2 bez linii drogi (D2). *Obali:* linia powtarza podpis z mapy i autor jej nie czyta. **v1.2:** po D18 podpisów na mapie nie ma, więc linia jest jedynymi
  słowami o miejscu w telefonie — zostaje do potwierdzenia na stopie #2.
- ~~**D9 — znicz obok okręgów**~~ — odpada z K2 (v1.1).
- **D10 — „Pokaż na mapie” w widoku osoby,** jak „Pokaż w drzewie” pod mini-drzewem ([[osoba]] D11), tylko gdy osoba ma zamieszkanie. *Obali:* autor szuka mapy
  przy osobie bez miejsc.
- **D11 — „Połącz dwie osoby” tylko przy drzewie.** Ścieżka pokrewieństwa to linie rodziny, których mapa nie ma. *Obali:* autor chce na mapie zobaczyć dwie
  osoby naraz (np. „czy mogli się spotkać” — jak widok Gramps „Have they been able to meet?”) — osobna pozycja.
- **D12 — miejsce urodzenia i zgonu nie w tej pozycji** ([[zamieszkanie]] *Open* 3 — decyzja przy projekcie mapy). `events.place` to sam tekst, bez
  punktu, więc punkt na mapie wymagałby zmiany bazy. Pozycja jest „bez zmiany bazy”, a termin nie daje miejsca na drugą migrację przed instalacją.
  Pierwsze zamieszkanie z pustym „Od” zaczyna się z urodzeniem (D4), więc dom rodzinny już stoi na mapie od narodzin. Kandydat po wyjeździe — migracja
  przyjdzie aktualizacją ze sklepu z migawką ([[ADR-019-distribution-play-internal-testing]]). Autor na stopie #1 tego nie zmienił. *Obali:* przy
  przepisywaniu notatek miejsca urodzenia są częste, a zamieszkań brak — wtedy ta pozycja wraca przed następną aktualizacją.
- ~~**D13 — obszar „cały kraj” jako część kraju z punktem nazwy**~~ — odpada z O3 (v1.1): obszaru nie ma.
- **D14 — granice i brzegi jako dekoracja (70%).** Ląd i woda mają tę samą jasność (1,00:1), a pełny obrys (3,40:1) przy ok. 180 krajach zagłuszyłby
  osoby. *Obali:* na telewizorze z kanapy nie widać, gdzie jest ląd — wtedy brzegi pełnym obrysem, granice bez zmian (lista B).
- **D15 — „cały kraj” w punkcie nazwy kraju, bez obszaru (O3, decyzja autora, v1.1):** *„tutaj tylko środek tego kraju, bez okręgu lub zaznaczonych
  krawędzi”*. Zmienia zapis pozycji („obszar, nie pinezka” — *What to build*). Niepewność miejsca mówią słowa „cały kraj” ~~w podpisie i~~ w karcie (od v1.2
  także czytnik; podpisu nie ma — D18), a obrys okręgu zostaje zwykły, żeby przerywany znaczył tylko niepewną datę (jak w drzewie). *Obali:* rodzina przy
  telewizorze bierze punkt nazwy kraju za konkretne miasto (po D18 bardziej prawdopodobne — na telewizorze nie ma ani podpisu, ani karty).
- **D16 — osoba po śmierci znika (K2, decyzja autora, v1.1).** Mapa pokazuje życie i ruch; groby ma mapa Polski i cmentarze. Linia karty po śmierci znika, bo
  lata życia już ją mówią. *Obali:* autor chce na telewizorze pokazać, gdzie kto spoczywa — wtedy K1 z v1 (znicz na cmentarzu).
- **D17 — droga tylko w ruchu (D2, decyzja autora, v1.1).** Mapa bez linii jest spokojniejsza, a kolejność miejsc pokazuje ▶ i suwak; jej ruch wśród innych
  wyróżnia pierścień w akcencie (~~ślad w akcencie~~ — v1.4, D25). *Obali:* autor chce zobaczyć całą drogę osoby naraz — wtedy D1 z v1 (linia z numerami).
- **D18 — bez podpisów miejsc i nazw krajów (decyzja autora, 2026-10-17, w trakcie przeglądu `ui` zbudowanego ekranu, v1.2):** *„Tak naprawdę nie
  potrzebuje żadnych nazw krajów ani miejscowości, wystarczą awatary i kontury krajów”*. Z mapy znikają nazwy krajów (2), podpis miejsca pod stosem (4), podpis
  skupienia („5 miejsc” — 4a) i „Francja · cały kraj” (6); zostaje plakietka „+N”. Czytnik dalej słyszy miejsce („Testowo: 4 osoby — rozsuń”), bo to nie napis na
  ekranie, a mapa jest dla niego obrazem. Dlaczego: autor pokazuje rodzinie ludzi i ich ruch, a kraj rozpoznaje się po konturze — mapa jest spokojniejsza, a
  znika cała klasa kolizji podpisów przy krawędzi i pod + / − (zrzuty przeglądu). Czego to nie da: na telewizorze nie ma karty, więc nic nie mówi słowami, gdzie
  kto jest — kraj tylko z konturu, a miejscowości w jednym kraju się nie rozróżni. **Imiona w rozsunięciu (9) i linia karty (12) zostają — do potwierdzenia przez
  autora na stopie #2** (to nie nazwy miejsc; `qa` pyta). Odstępstwo 2 `dev` (podpisy bez nakładania) nie wchodzi jako reguła. *Obali:* przy telewizorze rodzina
  pyta „gdzie to jest?” albo myli dwa sąsiednie kraje — wtedy wracają najpierw nazwy krajów (tylko z danymi, bez nakładania, jak odstępstwo 2), dopiero potem
  miejscowości.
- **D19 — skupienie miejsc (odstępstwo 1 `dev`, przyjęte w v1.2):** stosy, które leżałyby na ekranie na sobie, łączą się w jeden stos z „+N”; dotknięcie
  przybliża do ich miejsc, a przy największym przybliżeniu rozsuwa. Dlaczego: pierwszy kadr przy rodzinie w Polsce i w USA to cały świat, a stosy miejscowości
  jednego kraju leżały na sobie (zrzut `02` przejścia `dev`). To kanon Leaflet.markercluster: *„When you click a cluster we zoom to its bounds.”* i *„When you
  click a cluster at the bottom zoom level we spiderfy it so you can see all of its markers.”*, a promień łączenia liczy się od wielkości znacznika (*„The maximum
  radius that a cluster will cover from the central marker (in pixels). Default 80.”* — [README](https://github.com/Leaflet/Leaflet.markercluster), odczyt
  2026-10-17). W aplikacji to druga instancja po zniczach z liczbą na mapie Polski ([[style-b]] reguła 13). Po D18 skupienie wygląda jak stos — różnicę mówi
  czytnik („przybliż” / „rozsuń”) i to, co się dzieje po dotknięciu. *Obali:* autor na stopie #2 nie rozumie, dlaczego jedno dotknięcie przybliża, a drugie
  rozsuwa — wtedy przy skupieniu liczba miejsc w plakietce.
- **D20 — przełącznik ma ten sam kształt w obu częściach (odstępstwo 5 `dev`, przyjęte w v1.2):** napisy albo same ikony liczone względem miejsca w części
  „Drzewo” (z „Połącz dwie osoby”). Dlaczego: przy 200% na 360 dp w części „Mapa” napisy by się zmieściły (292 dp), a w „Drzewie” nie (ok. 244 dp) — przełącznik
  zmieniałby szerokość pod palcem, który właśnie zmienił część. *Obali:* autor przy dużym tekście nie poznaje części po samych ikonach — wtedy przełącznik pod
  paskiem, nad mapą (*Obali* planu).
- **D21 — dotknięcie osoby w środku otwiera jej widok (odstępstwo 6 `dev`, przyjęte w v1.2),** poza trybem prezentacji; czytnik „— otwórz”. Dlaczego: obie
  części to ta sama zakładka, a w drzewie drugie dotknięcie osoby w środku otwiera jej widok — ten sam gest nie może znaczyć dwóch rzeczy. „Pokaż ›” w karcie
  zostaje. *Obali:* autor otwiera widok przypadkiem, celując w stos obok — wtedy na mapie dotknięcie osoby w środku nic nie robi.
- **D22 — pierwszy kadr najwyżej do poziomu 5 (odstępstwo 7 `dev`, przyjęte w v1.2).** Dlaczego: gdy wszystkie miejsca leżą blisko siebie (albo jest jedno),
  dopasowanie do nich dałoby poziom regionu (7, D1) — kanciaste brzegi i brak kraju wokół, a poziom 5 to mniej więcej jeden kraj na ekranie telefonu. *Obali:*
  rodzina mieszka w jednej okolicy i autor po każdym uruchomieniu przybliża — wtedy pierwszy kadr bliżej.
- **D23 — podwójne dotknięcie przybliża o jeden poziom mapy (×2) (odstępstwo 4 `dev`, przyjęte w v1.2);** + / − zostają ×1,45 (11). Dlaczego: na mapie Polski i
  na planie cmentarza podwójne dotknięcie to też jeden poziom (domyślne zachowanie `flutter_map`), więc mapy aplikacji zachowują się tak samo; ×1,45 to krok
  drzewa, które nie jest mapą. *Obali:* autor na stopie #2 odczuwa skok jako za duży — wtedy ×1,45 także przy podwójnym dotknięciu.
- **D24 — przełącznik w sterowaniu trybu prezentacji na środku miejsca między rokiem a „Zakończ prezentację” (odstępstwo 9 `dev`, przyjęte w v1.3,
  2026-10-17).** Do v1.2: „u góry pośrodku”, czyli na środku ekranu. Dlaczego: przy tekście 200% przełącznik na środku ekranu wchodził pod „Zakończ” — na
  914 dp o ok. 56 dp, a na 800 dp (telefon 360 dp poziomo) nawet same ikony o ok. 29 dp; dotknięcie „Mapa” trafiało w wyjście (test `qa`, *Round 4* pozycji).
  Teraz przy 200% na 800 dp przełącznik ma napisy (267 dp), 47 dp od roku i 29 dp przed „Zakończ”, bez nachodzenia (zrzut `r18`, granice węzłów z
  `uiautomator`); przy 100% na 914 dp stoi ok. 40 dp na lewo od środka ekranu, w równych odstępach od roku i od „Zakończ” (`r16`). Jedna reguła przy każdym
  rozmiarze tekstu, a położenie liczone z najszerszego zapisu roku — jak [[style-b]] reguła 5, przełącznik nie przesuwa się z rokiem przy ▶. Prior art: pasek
  narzędzi Fluttera (`NavigationToolbar`, Flutter 3.41.1, `widgets/navigation_toolbar.dart`) też daje środkowi tylko miejsce między elementami po bokach
  (*„maxWidth: size.width - leadingWidth - trailingWidth - middleSpacing * 2.0”*), ale stawia go na środku ekranu i przesuwa dopiero przy kolizji (*„If the
  centered middle will not fit between the leading and trailing widgets, then align its left or right edge with the adjacent boundary.”*, odczyt
  2026-10-17). Przyjęte tu „zawsze na środku miejsca”, bo w rzędzie są trzy rzeczy różnej szerokości (rok ok. 70 dp, „Zakończ” ok. 170 dp), a równe odstępy
  czytają się spokojniej niż równa odległość od brzegów ekranu, a sterowanie jest dla osoby z telefonem, nie dla rodziny przed telewizorem ([[style-b]]
  *Thresholds* → tekst dla telewizora). Czego to nie da: przy 100% przełącznik nie leży nad środkiem listwy. *Obali:* autor na stopie #2 albo przy telewizorze
  widzi przełącznik jako przesunięty w lewo — wtedy reguła `NavigationToolbar` (środek ekranu, przesunięcie tylko przy kolizji).
- **D25 — przeprowadzka bez śladu (decyzja autora, 2026-10-17, stop #2 [[ISSUE-045-migration-map]], v1.4):** *„Dodatkowo chciałbym aby po prostu się te avatary przemieszczały płynnie po mapie bez tych linii szarych (nie ma potrzeby żadnego dodatkowego efektu)”*.
  Do v1.3: za okręgiem linia gasnąca w ok. 1,8 s, u osoby w środku w akcencie (D5). Teraz przeprowadzkę niesie sam przejazd okręgu (0,6 s, wolniej
  na starcie i końcu). Dlaczego autor tak chce: na telewizorze przy ▶ ślady wielu osób naraz to szare linie, które nic nie mówią rodzinie, a ruch
  twarzy wystarcza — *Obali* z D5 („pajęczyna przy »Szybko«”) zaszło w odczuciu autora już przy „Średnio”. Czego to nie da: po przejeździe nie widać,
  skąd ktoś przyjechał — mówi to tylko ruch w chwili przeprowadzki, ▶ wstecz albo suwak (D2). *Obali:* rodzina przy telewizorze gubi, kto dokąd
  pojechał — wtedy ślad tylko osoby w środku, jak *Obali* w D5.
- **D26 — na mapie awatar także u „ja” (decyzja autora, 2026-10-17, stop #2 [[ISSUE-045-migration-map]], v1.4):** *„Dlaczego zamiast Avatar jest "Ja" chciałbym żeby były tam avatary zamiast inicjałów”*. Na pytanie, co ma być w
  okręgu, autor wybrał: zdjęcie profilowe u każdego, kto je ma, także u siebie zamiast znaku „Ja”; bez zdjęcia inicjały — także u „ja”. Do v1.3: znak „Ja”
  jak w drzewie (D14), także przy zdjęciu. Dlaczego: na mapie rodzina rozpoznaje ludzi po twarzach (D18 — bez nazw), a „Ja” zakrywało twarz autora. Kim jest
  „ja”, mówi karta („to ja”), czytnik i imię „Ja” w rozsunięciu. Drzewo i lista osób zostają przy „Ja” (to inna decyzja — D14, [[osoby]] D4; autor wybrał
  wariant bez drzewa). Odrzucone: sylwetka zamiast inicjałów (wiele okręgów wyglądałoby tak samo; [[osoby]] reguła 11 — litery, nie zastępczy obrazek).
  Na emulatorze: przycisk „Wymyślone miejsca zamieszkania i portrety” daje 7 osobom wymyślonej rodziny, także „ja”, narysowane portrety. *Obali:* autor
  albo rodzina przy telewizorze nie wie, która twarz to autor — wtedy znak „Ja” obok okręgu, nie zamiast twarzy.
- **D27 — podpis przeprowadzki: kto, skąd i dokąd (M2)** (v1.5, [[ISSUE-050-next-event]]; *Open* 6; **decyzja autora na stopie #1 — „tak”, 2026-10-19**). „Kazimierz Wymyślony: Zmyślin →
  Francja” — nazwa z tamtego czasu, gdy jest zapisana; przy „cały kraj” nazwa kraju; nazwy w mianowniku, ze strzałką, bo „do Zmyślina” wymagałoby odmiany dowolnej nazwy. Dlaczego: cel (a) —
  opowieść („z Zmyślina do Wymyślowa”), a na telewizorze nie ma karty (12), która mówi, gdzie kto jest; D18 zabrało nazwy z mapy, nie z podpisu, a sam autor napisał „zmiana miejsca
  zamieszkania” jako komentarz na mapie (ISSUE-050). M1 — „Przeprowadził się Kazimierz Wymyślony” — trzyma się D18 i mówi tylko „kto”. **Nie da:** ekranu bez nazw — wracają, choć tylko w
  podpisie. *Obali:* autor przy telewizorze woli same twarze („wystarczą awatary i kontury krajów” — D18) — wtedy M1.
- **D28 — zdarzenia mapy to tylko przeprowadzki, całej rodziny** (v1.5, decyzja projektowa). Przeprowadzka = osoba żyjąca w roku Y ma inne zapisane miejsce niż w roku Y−1 (D4). Narodziny,
  śmierć, pierwsze miejsce i zamieszkanie bez lat nie — na mapie osoba się wtedy pojawia albo znika przenikaniem (8), a narodziny i śmierć ma podpis drzewa. Całej rodziny, także poza
  kadrem, jak pigułka (3, D7) — mapa nie ma poziomów. **Nie da:** „pojawił się w Wymyślowie” przy pierwszym znanym miejscu. *Obali:* przy prawdziwych danych pierwsze miejsce jest często dopiero
  w dorosłości (np. wyjazd za granicę bez wcześniejszego adresu) i rodzina nie widzi wyjazdu — wtedy także „→ Francja” od pierwszego miejsca po latach bez miejsca.
- **D29 — po ⏭ kadr stoi; jedna linia na drogę** (v1.5, decyzja projektowa). Kadr zmieniają tylko Twoje gesty (R4 — D6): wyjazd poza kadr widać jako wylot za krawędź, przyjazd — jako wlot,
  jak przy ▶; dlatego na mapie nie ma podjazdu z drzewa ([[drzewo]] D63 — tam osoby poza ekranem nie widać). Kto jechał tą samą drogą w tym samym roku, stoi w jednej linii (M2): przy
  powojennej przeprowadzce rodziny cztery linie „Zmyślin → Wymyślowo” mówiłyby to samo. **Nie da:** osobnej linii dla każdej osoby przy wspólnej drodze. *Obali:* rodzina przy telewizorze
  gubi, kto dokąd pojechał, bo kadr obejmuje tylko Polskę — wtedy po ⏭ kadr na drogę (jak R2 z v1).
- **D30 — przeprowadzający się świecą** (v1.6; stop #2 [[ISSUE-050-next-event]], runda 1; **prośba autora** — *„tak samo aby te avatary "lśniały" gdy coś się zmienia”*; **decyzja *„B”***).
  Okręgi osób z linii bieżącej strony: pierścień w akcencie 2,5 dp (jak osoba w środku, 4) i poświata pod okręgiem, trzy pulsy, potem stała, dopóki stoi podpis — ten sam rytm co w drzewie
  ([[drzewo]] D73, D75). Świecą w drodze, więc oko idzie za nimi z miejsca na miejsce, także zza kadru (R4 — D29). **W stosie idą na przód** — gdy któraś z nich byłaby schowana w
  „+N”, osoby z podpisu stają pierwsze, reszta stosu zachowuje kolejność; przy więcej niż trzech świeci też „+N”. Dlaczego: na telewizorze nie ma nazw (D18) ani karty (12), a światło
  pokazuje z kanapy, kto się przeprowadził. Najpierw (v1.6, przed przejściem `dev`) kolejność miała zostać, a świecić miał sam „+N” — na emulatorze przy kadrze rodziny na dwóch kontynentach
  przeprowadzka z Litwy skończyła się w skupieniu 14 osób i świecił tylko „+11”, czyli żadna twarz. **Nie da:** spokojnego stosu — przy ⏭ i przy zmianie roku pozostałe okręgi
  przesuwają się o jedno miejsce. *Obali:* rodzina gubi, kto jest w stosie, bo kolejność skacze — wtedy na przód tylko przy ⏭, a po zmianie roku zostaje.
- **D31 — mapa poziomo: układ L4 jak drzewo** (v1.7, [[ISSUE-055-connect-from-the-tree-and-rotate]]; **decyzja autora na prototypie — panel 5, *„tak”***). Gdy ekran stoi
  poziomo — z „Obróć” albo z obracania telefonu — część „Mapa” ma ten sam układ co drzewo ([[drzewo]] 12, D77): bez dolnego paska zakładek, przełącznik i ikony („Obróć”,
  „Przesyłaj na telewizor”) w górnym rzędzie nad mapą, karta (12) z linią „gdzie” i czasem w dolnym pasku. Przełącznik „Drzewo · Mapa” zostawia obrót. **Nie da:** zakładek
  w poziomie. *Obali:* jak [[drzewo]] D77.

## Open
> **v1.1 — rozstrzygnięte na stopie #1 (2026-10-17, autor):** W2, K2, O3, D2, R4. Zapis kandydatów v1:

1. ~~⚠️ OPEN — W: skąd wchodzisz na mapę~~ → **W2** (przełącznik „Drzewo | Mapa”). W1 — osobny ekran z ikony globusa w pasku drzewa; na telewizorze
   z drzewa na mapę trzeba by zakończyć prezentację i przesłać jeszcze raz.
2. ~~⚠️ OPEN — K: osoba po śmierci~~ → **K2** (znika; D16). K1 — znicz na jej cmentarzu.
3. ~~⚠️ OPEN — O: miejsce znane tylko do kraju~~ → **O3, wariant autora** (punkt nazwy kraju, bez obszaru; D15). O1 — przerywana granica kraju (6,18:1);
   O2 — miękkie koło (1,23:1, poniżej SC 1.4.11).
4. ~~⚠️ OPEN — D: droga osoby w środku~~ → **D2** (tylko w ruchu; D17). D1 — linia w akcencie z numerami przystanków.
5. ~~⚠️ OPEN — R: kadr~~ → **R4, wariant autora** (kadr z Twoich gestów; D6). R1 — cała rodzina zawsze; R2 — droga osoby w środku; R3 — większość rodziny i
   osoba w środku, plakietki przy krawędzi.
6. ~~⚠️ OPEN — M: miejsce w podpisie przeprowadzki~~ — **rozstrzygnięte 2026-10-19: M2** (stop #1, *„tak”*; D27). Zapis sprzed decyzji: na stop #1 [[ISSUE-050-next-event]] (v1.5, makieta `mapa-050.html`; pytanie 4 z pozycji). **M1** — kto, bez miejsca
   („Przeprowadził się Kazimierz Wymyślony”); **M2** — kto, skąd i dokąd („Kazimierz Wymyślony: Zmyślin → Francja”). **Rekomendacja: M2** (D27). Pozostałe wybory „Następne” — [[drzewo]]
   *Open* 12.
