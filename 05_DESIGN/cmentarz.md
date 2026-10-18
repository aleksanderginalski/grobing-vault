---
screen: "Cmentarz — groby na cmentarzu"
items: ["[[ISSUE-012-transcribe-grave-screen]]", "[[ISSUE-016-photos-grave-and-person]]", "[[SPIKE-004-mvp-flow-prototype]]", "[[ISSUE-024-person-view]]", "[[ISSUE-027-cemetery-map-plan-photo-states]]", "[[ISSUE-028-cemetery-sectors]]", "[[ISSUE-029-pin-on-site-gps]]", "[[ISSUE-047-grave-first-then-people]]"]
us: "[[US-002-przepisanie-grobu]] · [[US-005-zdjecia]] · [[US-007-mapa-cmentarza]] · [[US-008-pinezka-na-miejscu]]"
journey-step: "n/a — M1 (warunek kroku 1 UJ-001); docelowo mapa cmentarza z arkuszem grobu (R2, krok 2 UJ-001, M3)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-cmentarz-grob-osoba.html (ramki 1–2, 8, ISSUE-012) · makieta-zdjecia.html (ramka 9, ISSUE-016) · 2026-10-08: grobing-prototyp.html (SPIKE-004, panel 2) · 2026-10-12: issue-027-mapa-cmentarza.html (stany planu, warianty NFR-004) · 2026-10-12: issue-028-kwatery.html (klikalny: kwatery na planie, tryb „Kwatery”, kandydaci K1–K3, adres grobu W-a/W-b) · 2026-10-12: issue-029-pinezka.html (klikalny: „gdzie jestem”, tryb D, kandydaci P1/P2, poprawa, słaby sygnał; katalog tymczasowy sesji `8b388e89-…`) · 2026-10-18: makieta-047.html (ISSUE-047 — „Dodaj grób” → okno „Nowy grób”, ekrany 1–2)"
updated: 2026-10-18
---

# Cmentarz — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.8) · referencja: [[references]] → **R2**.
>
> **Wersja 2 (2026-10-07, przed planem ISSUE-012)** — przebudowa według decyzji autora z 2026-10-06
> ([[ISSUE-012-transcribe-grave-screen]] → *Input from the author*): **cmentarz jak R2, ale bez zdjęcia
> satelitarnego — arkusz z grobami, z pinezką i bez.** Wersja 1 była listą kart z „Grób nazwany osobami”;
> zmiany: układ R2 (nagłówek, arkusz grobów), **nazwa grobu** jako tytuł karty, wejście z „Otwórz cmentarz”
> ([[cmentarze]] element 7), kierunek po [[SPIKE-001-map-source-offline]] (D1).
>
> **Wersja 2.1 — przegląd `ui` zbudowanego ekranu (2026-10-07):** lista kończy się nad przypiętym „Dodaj grób”
> (zamiast przewijać się pod nim — skutek ten sam: ostatnia karta jest cała widoczna). Osoba bez imion i nazwiska
> (tylko z innych danych): „Osoba bez imienia”. Reszta zgodna ze zbudowanym ekranem.
>
> **Wersja 3 (2026-10-07, przed planem [[ISSUE-016-photos-grave-and-person]]):** karta grobu ze zdjęciem ma z
> lewej **miniaturę zdjęcia nagrobka** (element 3 (d)) — „miejsce na zdjęcie” z arkusza grobu, którego chciał
> autor (ISSUE-012 → *Input from the author* 2), i miniatura nagrobka z R2. Grób bez zdjęcia — karta bez zmian.
>
> **Wersja 4 — discovery na prototypie, panel 2 ([[SPIKE-004-mvp-flow-prototype]] D8–D11, 2026-10-08): cmentarz to
> mapa.** Kierunek z D1 („mapa nad listą, lista w dolnym arkuszu jak w R2”) autor zmienił na prototypie:
> - **na starcie sama mapa**: plan schematyczny z OSM (offline) albo zdjęcie z góry (online), kwatery, znicze grobów
>   z pinezką, bez listy (D10, D11);
> - **znicz → arkusz jednego grobu** z „Pokaż grób” (R2);
> - **arkusz przeciągnięty w górę → cała lista grobów bez mapy**, a karta na liście → [[grob]];
> - **bez linku do Grobonetu i do wyszukiwarki zarządcy** (D12);
> - kwatery jako nazwane strefy z przerywaną linią (D13).
>
>
> **Wersja 4.1 — panel 2, runda 2 (SPIKE-004 D12, 2026-10-08):** w stanie mapy pasek grobów na dole z liczbą grobów
> bez pinezki i **wypełnionym „Dodaj grób”, takim samym jak pod listą** (autor: *„1 ok, ale chciałbym aby wygląd
> przycisku »dodaj grób« był konsekwentny z tym co jest po rozwinięciu tego paska grobów”*; przepływ: *„2. tak”*).
> Purpose, Navigation, Elements, States, Sketch, Tempo i *Style B rules applied* przepisane na trzy stany ekranu
> (mapa · jeden grób · lista). **Zbudowany ekran (ISSUE-012/016) to dzisiejszy stan C bez planu i bez pasków.**
>
> **Wersja 4.2 — wizyta, panel 7 ([[SPIKE-004-mvp-flow-prototype]] D22, 2026-10-08):** autor: *„5. ok”*. Na planie
> przycisk **„gdzie jestem”** z niebieską kropką i kołem dokładności; w arkuszu grobu z pinezką **„Popraw pinezkę”** (R2);
> **tryb stawiania pinezki** (stan D) z GPS — pinezka w kropce, przesuwana dotknięciem planu, zapis ze źródłem „GPS ±N m,
> data”; **bez internetu** plan działa, a „Zdjęcie” mówi „bez internetu”. Wejście do trybu D także z [[grob]] („Postaw
> pinezkę”). Elementy 10–14, stan D i *States*.
>
> **Wersja 4.3 (2026-10-09, przed planem [[ISSUE-024-person-view]]) — zaznaczony grób z widoku osoby.** „Pochówek” w
> [[osoba]] (element 9) otwiera ten ekran **z zaznaczonym grobem**. Do czasu [[US-007-mapa-cmentarza]] zbudowany ekran to
> sama lista (dzisiejszy stan C), więc: lista przewija się tak, żeby karta grobu była cała widoczna, karta ma **obrys 2 dp w
> akcencie** (D11 — „na liście zaznaczony grób ma obrys w akcencie”) i stan „zaznaczone” dla czytnika (SC 1.4.1 — kolor
> nie jest jedynym nośnikiem). **Bez komunikatu o pinezce**, dopóki pinezek nie ma w aplikacji ([[osoba]] D17); wraca z
> mapą. Wstecz → widok osoby. Zaznaczenie trwa, dopóki ekran jest otwarty (powrót z grobu — dalej zaznaczony).
>
> **Wersja 5 (2026-10-12, przed planem [[ISSUE-027-cemetery-map-plan-photo-states]]) — stany planu, których prototyp nie
> pokazał.** Prototyp znał dwa stany planu: „jest” i „nie pobrany”. Plan pobierany z sieci ma ich sześć, bo cmentarz może
> nie mieć punktu albo obrysu w OSM, a serwer może nie odpowiadać (element 2a, D17–D19). Do tego:
> - pobieranie bez śladu na mapie Polski (D20);
> - uchwyt arkusza działa dotknięciem (D21);
> - plakietki przy dużym tekście (D22);
> - wejście z widoku osoby, gdy mapa już jest (D23).
>
> Kwatery (element 4) → [[ISSUE-028-cemetery-sectors]]. W ISSUE-027 plan jest bez kwater i bez sposobu ich zaznaczenia.
> **Pinezek nie da się postawić aż do [[US-008-pinezka-na-miejscu]]**, więc na prawdziwych danych mapa po ISSUE-027 pokazuje
> stan „bez pinezek”, a znicze widać tylko na danych testowych. Zbudowany ekran nie ma jeszcze ✎ w pasku (element 1). Wchodzi
> z tą pozycją tą samą drogą, co ✎ w arkuszu [[cmentarze]] (okno 15 → wskazanie 16).
> Miara [[NFR-004-czytelnosc-w-sloncu]] na tym ekranie: **W2** — adres, „3 osoby”, linia grobów bez pinezki i druga linia
> zaślepek w kolorze tekstu (decyzja autora na stopie #1 ISSUE-027, *Open*).

> **Wersja 5.1 (2026-10-12, przegląd `ui` zbudowanego ekranu [[ISSUE-027-cemetery-map-plan-photo-states]]):** odstępstwa `dev`
> przyjęte w przeglądzie i poprawki z przeglądu (0 BLOCKER, 2 MAJOR, 7 MINOR — poprawione przed stopem #2):
> - **2a bez grobów:** (b) bez drugiej linii, (c) tylko „Spróbuję znowu później.” — zaślepka nie odsyła do listy, której nie ma
>   (reguła 7). Ikony 2a w wariantach `outlined` (`cloud_download_outlined`, `cloud_off_outlined`, `not_listed_location_outlined`),
>   przełącznik `satellite_alt_outlined` — reguła 3 (błąd tej specyfikacji w v5);
> - **uchwyty arkuszy (B, C) — cel 48 dp**, znicz 48 × 48 dp (D21);
> - **podpisy źródła** („© OpenStreetMap”, „Ortofotomapa: GUGiK”) jako mała plakietka na powierzchni, 11 sp, tekst pomocniczy
>   (5,01:1) — alejki nie przecinają liter (reguła 13), na zdjęciu tylko plakietki (reguła 14); wyjątek 11 sp w [[style-b]]
>   *Thresholds* (v1.21). Zdjęcie ładuje się na tle w kolorze powierzchni;
> - **element 8 (C): lista na tle, karty na powierzchni** (reguły 2, 11 — jak Osoby i grób); w v5 omyłkowo „na powierzchni”;
> - **kadr (el. 2):** plan ma co najmniej 35% wysokości mapy; na 360 × 640 dp przy 200% pasek zasłania południe planu (D14 →
>   *Obali*; wyjście „Dodaj grób obok liczby” nie mieści się w 360 dp przy 200%). Przełącznik przy dwóch rzędach zmniejsza się,
>   zamiast wychodzić za ekran;
> - **B:** arkusz przeciągnięty w dół → A; ikona „osoby” w kolorze linii (W2), stałe 18 dp;
> - **el. 13:** „bez internetu” przy zdjęciu trwa do zmiany warstwy (sieć sprawdzana jeszcze raz przy wyborze „Zdjęcia”);
> - **pasek grobów (6):** „Pokaż listę grobów” to osobny węzeł dla czytnika (`container`), nie cały panel.

> **Wersja 6 (2026-10-12, przed planem [[ISSUE-028-cemetery-sectors]]) — kwatery autora.** Prototyp SPIKE-004 pokazał, jak
> kwatera wygląda (D13), a nie jak się ją zaznacza. Nowe:
> - przycisk **„Kwatery”** w stanie A (element 15) → **tryb E „Kwatery”** (16–17): lista kwater cmentarza, kwatera wybrana,
>   zmiana nazwy, „Narysuj strefę”, „Usuń z planu”;
> - **tryb F — zaznaczanie strefy** (18) i okna (19), D24–D29;
> - element 4 — kwatera wybrana, położenie nazwy, strefy bez dotyku poza trybem E.
>
> Na stop #1 idą dwie decyzje (*Open*): **gdzie się dotyka** przy rysowaniu (K1 celownik · K2 dotknięcie · K3 prostokąt) i
> **jak kwatera łączy się z adresem grobu** (W-a odnośnik · W-b tekst). Do tego **luka spoza tej specyfikacji**: adresu grobu
> (kwatera, rząd, miejsce) nie da się dziś wpisać na żadnym ekranie — propozycja w [[grob]] v6. Klikalny prototyp:
> `issue-028-kwatery.html` (katalog tymczasowy sesji `9f87c8cf-…`).

> **Wersja 6.1 (2026-10-12, przegląd `ui` zbudowanego ekranu [[ISSUE-028-cemetery-sectors]]):** 0 BLOCKER, 1 MAJOR, 9 MINOR —
> poprawione przed stopem #2. Odstępstwa `dev` przyjęte (7 — częściowo):
> - **15:** cel dotyku 48 dp to całe pole wokół pigułki 40 dp, dla czytnika przycisk „Kwatery” (MAJOR — było 40 dp); kadr planu w A
>   pigułki nie liczy;
> - **4:** nazwa po wewnętrznej stronie strefy — na lewo od rogu, gdy na prawo byłaby poza strefą; na zdjęciu z góry linia strefy na
>   linii w kolorze tła;
> - **16, 17b:** kadr nie przybliża bez potrzeby, a lista nie rusza planu, który już pokazuje strefy;
> - **17a:** cyfry przed literami (2, 10, A, B);
> - **18:** karta najwyżej ok. 22% mapy, z widocznym paskiem przewijania; podpis źródła mapy pod kartą; przy tekście > 130% „Cofnij”
>   jako ikona z `tooltip`; stara strefa w kolorze tekstu pomocniczego; komunikat przecięcia „…— cofnij ostatni róg.”;
> - **19b:** nazwa zajęta — „…już jest na tym cmentarzu — wpisz inną nazwę.” (zmiana nazwy nie łączy kwater).
>
> **Wersja 7 (2026-10-12, przed planem [[ISSUE-029-pin-on-site-gps]]) — pinezka na miejscu.** Prototyp SPIKE-004 (panel 7, D22)
> pokazał „gdzie jestem”, tryb D i „Popraw pinezkę”. Nie pokazał, co dzieje się poza zwykłą drogą. Na stopie #1 autor
> wybrał **P2** (*Open*). Nowe w tej wersji:
> - **„gdzie jestem” ma trzy stany** (10, D31): wyłączony, plan na kropce, plan odsunięty. Do tego plakietka stanu 10a: poza
>   cmentarzem, szukam pozycji, tylko przybliżona lokalizacja;
> - **tryb D włącza lokalizację sam** (D32). Poza cmentarzem pinezka zaczyna w strefie kwatery grobu;
> - **źródło pinezki to to, z czego wzięła się pozycja** (14, D33): GPS z dokładnością albo „postawiona na planie” / „na zdjęciu z
>   góry”. Link do wycofanego FR-001 zastąpiony słowniczkiem (*pinezka*) i [[data-model]] → Grave;
> - **poprawa zaczyna od zapisanej pinezki** (11, D35);
> - **słaby sygnał** z progiem tymczasowym 15 m, do pomiaru (12a, D37);
> - **tryb D jak tryb F** (D36): pasek z ✕, bez dolnego paska, warstwa z poprzedniego stanu.
>
> Na stop #1 idzie jedno pytanie (*Open*): **gdzie się dotyka** w trybie D — **P1** (dotknięcie przesuwa znicz, jak w prototypie
> SPIKE-004) albo **P2** (celownik jak przy kwaterach, K1). Klikalny prototyp: `issue-029-pinezka.html` (katalog tymczasowy sesji
> `8b388e89-…`). Poza AC US-008, ale zapisane wcześniej: z [[osoba]] → „Pochówek” grób bez pinezki → stan C **z komunikatem**
> [[osoba]] D9 (*Navigation*).
>
> **Wersja 7.1 (2026-10-12, przegląd `ui` zbudowanego ekranu [[ISSUE-029-pin-on-site-gps]]):** 0 BLOCKER, 3 MAJOR, 9 MINOR —
> MAJOR poprawione przed stopem #2. Ta wersja obowiązuje nad opisami elementów 10–12a wyżej, gdy się różnią:
> - **12 — karta GPS tylko wtedy, gdy znicz naprawdę stoi w kropce.** Gdy telefon szuka pozycji albo jest poza cmentarzem, karta
>   mówi o stawianiu ręcznym z „◎ wraca do Twojej pozycji.”, a panel mówi, czego brakuje (MAJOR — karta przeczyła panelowi);
> - **12a — „Zapisz pinezkę” przy poprawie** robi się aktywny dopiero, gdy pinezka się ruszy. Samo dotknięcie ◎ bez pozycji jej nie
>   rusza (MAJOR — zapis w tym samym miejscu gubił „GPS ±N m”);
> - **12 bez mapy (nowy stan):** cmentarz bez planu i bez zdjęcia — karta „Bez planu pinezkę postawisz tylko z GPS: stań przy
>   grobie, a znicz stanie w niebieskiej kropce.”, w miejscu planu „Planu tego cmentarza nie ma w telefonie. Pinezkę postawisz tu
>   tylko z GPS.”, „Zapisz pinezkę” czeka na kropkę. **Tryb D na „Zdjęciu” bez sieci startuje na planie**, a „Popraw pinezkę” (11)
>   ma tę samą regułę widoczności co ◎ (10): nie ma ich przy zaślepce planu (2a) i przy „Zdjęciu” bez sieci (MAJOR — zapisywała się
>   pinezka, której nie było widać);
> - **10, D31 — gdy nie ma kropki, do której można wrócić** (tylko przybliżona, szukam pozycji, poza cmentarzem), ◎ wygląda jak „na
>   kropce” i dotknięcie wyłącza — jest wyjście (znalezione testem `qa`: przy „Przybliżonej” ◎ nie dawał się wyłączyć). Pierwsze
>   włączenie z przybliżeniem do z18 to skok, nie przejazd (przyjęte);
> - **10a (a)** — od 10 km pełne kilometry („312 km”); od 1 do 10 km z jedną cyfrą po przecinku;
> - **12a — stany lokalizacji** („Szukam pozycji…”, „Jesteś poza cmentarzem (…)”, „Lokalizacja w telefonie jest wyłączona.”) w
>   **kolorze tekstu** (10,02:1, W2) — w v7 omyłkowo tekst pomocniczy;
> - **12 — ◎ w trybie D nazywa się „Gdzie jestem”** jak w A i B (opis ze stanem); karta „bez zgody” — po dwukropku mała litera;
>   cień pod czubkiem w kolorze tła (krycie 60%) i bez cienia, gdy znicz stoi w kropce; po podwójnym dotknięciu znicz wraca do kropki;
> - **12 — szczypanie nie zmienia pinezki na ręczną**, tylko przybliżenie; ręczną robi przeciągnięcie albo dotknięcie miejsca;
> - **D36 — wyjątek:** grób dodany przez formularz („Dodaj grób” → widok grobu zastępuje formularz) po „Zapisz pinezkę” wraca na mapę w
>   stanie A z nowym zniczem, a nie do B. *Obali:* autor nie znajduje nowego znicza — wtedy wynik przechodzi przez stos;
> - ***Navigation* — komunikat [[osoba]] D9 to pasek komunikatu na dole** (jeden wzorzec paska w aplikacji), nie „pod paskiem (1)”.
>
> Znana luka (przegląd, odstępstwo 7): przy tekście 200% na 360 × 640 dp „Kwatery” przykrywa „Plan offline” i „© OpenStreetMap”, a plan
> w A jest bardzo niski — z [[ISSUE-027-cemetery-map-plan-photo-states]] i [[ISSUE-028-cemetery-sectors]]; ◎ jej nie pogarsza. Kandydat
> na osobną pozycję przed MVP.
>
> **Wersja 8 (2026-10-18, przed planem [[ISSUE-047-grave-first-then-people]]) — przyjęte na stopie #1 (autor: „Tak”, 2026-10-18): najpierw grób, potem osoby.** Autor:
> *„gdy próbuję dodać nowy grób, to nagle pokazuje się „Osoba w grobie” — a chciałbym dodać po prostu grób, a następnie osobę”*. Obali decyzji
> [[wpis-osoby]] „Grób powstaje z pierwszą osobą” (*„potrzeba grobu bez osób”*) trafione. Zmiany:
> - **„Dodaj grób” (6, 9) otwiera okno „Nowy grób”** (9a) — to samo okno co „Popraw grób” ([[grob]] 3a–3c), wszystkie pola opcjonalne; „Zapisz”
>   tworzy grób i otwiera jego widok, pusty ([[grob]] v9). Tryb „nowy grób” formularza osoby znika;
> - **grób bez osób powstaje teraz z interfejsu** (*States*): karta ma tytuł — nazwę grobu, a pod nią „bez wpisanych osób”; bez nazwy — „Grób bez
>   wpisanych osób”, jak dotąd (D38);
> - *Tempo*: nowy grób z pierwszą osobą to 4 dotknięcia zamiast 1 (D38). Makieta: `makieta-047.html`, ekrany 1–2.
>
## Purpose
Cmentarz rodziny **jako mapa** (UJ-001 krok 2, M3, M7): plan schematyczny bez sieci albo zdjęcie z góry z siecią,
kwatery zaznaczone przez autora i znicze grobów z pinezką. Stąd autor idzie do **jednego grobu** (znicz) albo do
**listy wszystkich grobów**, także bez pinezki, i dodaje kolejny grób z notatek (M1). Lista mówi, czy grób ma adres
kwatery i pinezkę (US-002 AC-5), i pokazuje, dokąd doszło przepisywanie.

## Navigation
- **Z [[cmentarze]]:** arkusz cmentarza → **„Otwórz cmentarz”** (element 7). Ekran otwiera się zawsze w stanie A.
  Także dla cmentarza bez grobów, bez planu i bez punktu na mapie.
- **Trzy stany ekranu** ([[SPIKE-004-mvp-flow-prototype]] D9, D12):
  - **A — mapa:** plan (2–5) i pasek grobów na dole (6). Znicz → B. Pasek (dotknięcie albo przeciągnięcie w górę)
    → C. „Dodaj grób” → **okno „Nowy grób” (9a, v8)** → „Zapisz” → [[grob]] tego grobu, pusty; wstecz z grobu wraca tu, a nowy grób jest
    na liście (do v7: [[wpis-osoby]] w trybie „nowy grób” — grób powstawał z pierwszą osobą, przy jej zapisie);
  - **B — jeden grób:** arkusz grobu (7), a plan przesuwa się płynnie nad arkusz. „Pokaż grób” → [[grob]]. Arkusz
    przeciągnięty w górę albo **dotknięty uchwyt** → C (D21). Dotknięcie planu albo wstecz → A;
  - **C — lista:** wszystkie groby na cały ekran, bez planu (8–9). Karta → [[grob]]. Lista przeciągnięta w dół, **dotknięty
    uchwyt** albo wstecz → stan, z którego przyszła (B albo A).
- **Z [[osoba]] → „Pochówek”** (v5, D23): grób z pinezką → stan B z tym grobem; grób bez pinezki → stan C z zaznaczonym
  grobem, **bez komunikatu o pinezce aż do [[US-008-pinezka-na-miejscu]]** ([[osoba]] D17 trwa; komunikat z [[osoba]] D9
  wraca z US-008). Wstecz → widok osoby. **v7 ([[ISSUE-029-pin-on-site-gps]]):** komunikat wraca — pasek komunikatu pod
  paskiem (1): „Ten grób nie ma jeszcze pinezki — jest zaznaczony na liście.” ([[osoba]] D9), znika po ok. 4 s albo po
  dotknięciu.
- **Wstecz w stanie A → [[cmentarze]]** z tym samym cmentarzem wybranym i jego arkuszem (D7). Z [[grob]] wstecz →
  stan, w którym autor ekran opuścił.
- **✎ w pasku → okno „Popraw cmentarz”** ([[cmentarze]] 15), według [[style-b]] reguły 15. Zaznaczanie kwater i
  stawianie pinezek to osobne działania: kwatery — przycisk „Kwatery” (15, v6), pinezki — panel 7 (wizyta, [[US-008-pinezka-na-miejscu]]).
- **Pinezka (v7, [[ISSUE-029-pin-on-site-gps]]):**
  - **[[grob]] → „Postaw pinezkę”** (grób bez pinezki) → **tryb D** tego cmentarza dla tego grobu;
  - **B → „Popraw pinezkę”** (11) → tryb D dla grobu z arkusza;
  - **D → „Zapisz pinezkę”** → stan B z tym grobem, kadr na nowym zniczu — także gdy wejście było z [[grob]] (D22 z SPIKE-004,
    D36). Wstecz z B → A, jak zawsze;
  - **D → ✕, „Anuluj” albo wstecz** → tam, skąd przyszło ([[grob]] albo B), bez zapisu i bez okna (jedna pinezka to mało pracy
    do stracenia — inaczej niż rogi w F, 19d);
  - lokalizacja (10) gaśnie przy wyjściu z ekranu cmentarza. Nic nie działa w tle.
- **Kwatery (v6, [[ISSUE-028-cemetery-sectors]]):**
  - **A → „Kwatery” (15) → tryb E** (16–17): lista kwater. Kwatera dotknięta na liście albo na planie → kwatera wybrana (17b).
    ‹ albo wstecz → lista; ✕ albo wstecz z listy → A z tym samym kadrem co przed wejściem;
  - **„Zaznacz kwaterę” → okno „Nowa kwatera” (19a) → „Dalej” → tryb F** (18). „Gotowe” zapisuje kwaterę ze strefą → E z tą
    kwaterą wybraną. Z kwatery wybranej **„Narysuj strefę” / „Narysuj strefę od nowa” → F** bez okna nazwy;
  - **F → ✕ albo wstecz:** bez rogów → E; z rogami → okno „Porzucić zaznaczanie?” (19d);
  - **✎ przy kwaterze → okno „Nazwa kwatery”** (19b); **„Usuń z planu” → okno 19c** → E (lista).
- **Pasek dolny** Mapa · Osoby · Drzewo jest widoczny we wszystkich stanach, a aktywna jest Mapa ([[style-b]] reguła
  12, SPIKE-004 D2).

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** wstecz + **nazwa cmentarza** (18 sp, półgruby, do 2 linii), pod nią miejscowość (13 sp, tekst pomocniczy; bez miejscowości brak linii); po prawej ✎ (`edit_outlined`, akcent, `tooltip` „Popraw cmentarz”) | pasek | wstecz (*Navigation*); ✎ → okno | — | — | R2 (nagłówek) · [[style-b]] reguła 15 |
| 2 | **Plan schematyczny** na całą szerokość pod paskiem, także pod arkuszami: obrys cmentarza i alejki z OSM, pobrane przy dodaniu cmentarza ([[style-b]] reguła 13: teren — powierzchnia z obrysem, alejki — obrys 4 i 2 dp). Wyśrodkowany w wolnym miejscu między plakietkami (3) a paskiem grobów (6); w stanie B przesuwa się płynnie nad arkusz (jak [[cmentarze]] D30). Podpis „© OpenStreetMap” (11 sp, tekst pomocniczy) pod plakietką. **Kadr (v5):** na starcie cały obrys z marginesem 16 dp w wolnym miejscu; to też najmniejsze przybliżenie, a największe to z19 (granica zdjęcia z góry, [[ADR-003-map-source-offline]] pkt 2). Przesuwanie ograniczone do obrysu z marginesem, więc cmentarz nigdy nie znika z ekranu. Teren poza obrysem w kolorze tła. **Dla czytnika** plan to jeden węzeł „Plan cmentarza” (alejek nie czyta), a każdy znicz (5) to osobny przycisk. **Bez planu → 2a** | mapa | szczypanie, przeciąganie, podwójne dotknięcie; bez obrotu | cały cmentarz, północ u góry | — | [[ADR-003-map-source-offline]] pkt 1 · D10 |
| 2a | **Zaślepka planu (v5, D17)** w miejscu planu, wyśrodkowana w wolnym miejscu. Ikona 32 dp w kolorze tekstu pomocniczego, pod nią fakt i droga naprzód (oba 14 sp, kolor tekstu — W2, *Open*), niżej przycisk tekstowy w akcencie, cel ≥ 48 dp. Pięć wariantów: **(a) pobieranie** — wskaźnik postępu (kołowy, akcent) zamiast ikony, „Pobieram plan cmentarza…”, bez przycisku; **(b) bez internetu** — `cloud_download`, „Plan tego cmentarza pobierze się, gdy będzie internet.” · „Groby są na liście — pasek na dole.” · **„Pobierz teraz”**; **(c) serwer nie odpowiada** (po ponowieniach) — `cloud_off`, „Nie udało się pobrać planu — serwer map nie odpowiada.” · „Spróbuję znowu później. Groby są na liście.” · **„Pobierz teraz”**; **(d) brak obrysu w OSM** — `not_listed_location`, „W OpenStreetMap nie ma planu tego cmentarza.” · „Z internetem zobaczysz go na zdjęciu z góry.” · **„Pokaż zdjęcie z góry”** (tylko z siecią; bez sieci bez przycisku); **(e) bez punktu** — `location_off_outlined`, „Plan pobierze się, gdy wskażesz cmentarz na mapie.” · **„Wskaż na mapie”**. Plakietka „Plan offline” i podpis „© OpenStreetMap” znikają w każdym wariancie; przełącznik Plan · Zdjęcie (3) zostaje w (a)–(d), a w (e) znika, bo zdjęcie nie ma środka | stan planu | „Pobierz teraz” → (a); bez sieci zamiast tego pasek komunikatu „Bez internetu. Plan pobierze się, gdy będzie zasięg.” (zaślepka zostaje); „Pokaż zdjęcie z góry” → warstwa „Zdjęcie”, środek w punkcie cmentarza, z17; „Wskaż na mapie” → tryb wskazania ([[cmentarze]] 16) dla tego cmentarza; po „Zapisz” powrót tutaj w (a) | według stanu pobierania | — | [[ADR-003-map-source-offline]] pkt 1 („ponawianie i zaślepka są warunkiem”) · US-007 AC-5 · [[style-b]] reguła 7 · D17–D19 |
| 3 | **Plakietki na planie**, na powierzchni, wys. 32 dp, margines 12 dp. Z lewej **„Plan offline”** z ikoną `offline_pin` w zieleni stanu (propozycja `#8CC084`, [[style-b]] *State colours*). Z prawej przełącznik segmentowy **Plan · Zdjęcie** (ikony `map_outlined`, `satellite_alt`; aktywny segment w akcencie). „Zdjęcie” to ortofotomapa GUGiK, tylko online, nic nie zapisuje w telefonie; plakietka zmienia się na „tylko z internetem” z ikoną `wifi` (tekst pomocniczy), a podpis na „Ortofotomapa: GUGiK”. Kafelki zdjęcia ładują się na tle w kolorze powierzchni, bez wskaźnika; nic nie trafia do pamięci telefonu poza pamięcią podręczną w RAM (pkt 2). Wygląd „Zdjęcia” bez sieci → 13. **Duży tekst (v5, D22):** plakietki to kontrolki, więc rosną w pełni; gdy z przełącznikiem nie mieszczą się w jednym rzędzie, „Plan offline” schodzi pod przełącznik, z lewej. Przełącznik dla czytnika: dwa przyciski ze stanem „wybrany” | plakietka + przełącznik | segment → warstwa | Plan | — | [[ADR-003-map-source-offline]] pkt 2 · D10 |
| 4 | **Kwatery autora:** przerywana linia 1,5 dp (tekst, krycie 75% — 6,16:1 na powierzchni, kreska 5/4), **bez wypełnienia** (D28), i nazwa „Kwatera A” (12 sp, półgruba, kolor tekstu, obwódka 3 dp w kolorze powierzchni planu) w dolnym lewym rogu strefy: przy rogu strefy położonym najbardziej w lewo i w dół (największe „y − x” na ekranie), 6 dp nad rogiem, **w stronę wnętrza strefy** — na prawo od rogu, a na lewo, gdy na prawo byłaby poza strefą (v6.1); przy pochyłym boku litery mogą przeciąć linię — przykrywa ją obwódka; rośnie z tekstem najwyżej do 1,3× ([[style-b]] reguła 13). Na zdjęciu z góry tak samo, a pod linią strefy leży linia w kolorze tła 3,5 dp (pod wybraną 5 dp) — reguły 13, 14 (v6.1). Kwatera bez strefy jest tylko w adresach grobów (i na liście 17a). **W stanach A i B strefy nie reagują na dotyk** (D29), a dla czytnika są częścią węzła „Plan cmentarza”. **Kwatera wybrana (tryb E, v6):** linia 2,5 dp w akcencie, nazwa w akcencie (8,04:1) | strefy | w trybie E dotknięcie strefy → kwatera wybrana (17b) | — | — | [[ADR-003-map-source-offline]] pkt 3 · D13 · US-007 AC-4 |
| 5 | **Znicze grobów z pinezką:** znicz-pinezka 28 × 35 dp, cel dotyku ≥ 48 dp; wybrany 38 × 47 dp z poświatą ([[style-b]] reguła 13). Grób bez pinezki nie ma znicza | znaczniki | dotknięcie → stan B | — | — | R2 · D11 |
| 6 | **Pasek grobów** (stan A): dolny arkusz na powierzchni, promień 16 dp u góry, uchwyt. „6 grobów · 14 osób” (14 sp, tekst), pod spodem „2 groby bez pinezki — na liście” albo „wszystkie groby mają pinezki” (13 sp, kolor tekstu — W2). Pod nimi **wypełniony „Dodaj grób”** z ikoną `add`, ≥ 52 dp, na pełną szerokość — **ten sam przycisk co pod listą (9)** | dolny arkusz + przycisk główny | dotknięcie albo przeciągnięcie w górę → stan C; „Dodaj grób” → okno „Nowy grób” (9a, v8; do v7 — [[wpis-osoby]] „nowy grób”) | — | — | **decyzja autora** (SPIKE-004 D12) · D14 |
| 7 | **Arkusz grobu** (stan B), na powierzchni, z uchwytem: miniatura nagrobka 72 dp (promień 12 dp; bez zdjęcia brak miniatury), tytuł (16 sp, półgruby — jak 8 (a)), adres i ikona `group_outlined` + „3 osoby” (14 sp, kolor tekstu — W2, *Open*), **wypełniony „Pokaż grób” ze zniczem** (kolor tła na akcencie) | dolny arkusz + przycisk główny | „Pokaż grób” → [[grob]]; przeciągnięcie w górę albo dotknięcie uchwytu (cel 48 dp, czytnik: „Pokaż listę grobów”) → stan C | — | — | R2 (arkusz grobu) · D11 · D21 |
| 8 | **Lista grobów** (stan C), pod paskiem (1), na powierzchni z uchwytem: podsumowanie „6 grobów · 14 osób” (14 sp, tekst pomocniczy, margines 16 dp) i karty (promień 16 dp, odstęp 8 dp, margines 16 dp) w kolejności wpisania. Karta, od góry: **(a) tytuł** — nazwa grobu (16 sp, półgruby, kolor tekstu, do 2 linii); bez nazwy tytułem są **osoby w grobie**: imiona i nazwiska po przecinku, ten sam krój, do 2 linii, potem „i jeszcze 2”. **(b) osoby** — tylko gdy tytułem jest nazwa: imiona i nazwiska po przecinku (14 sp, tekst pomocniczy, do 2 linii, potem „i jeszcze 2”). **(c) adres** (14 sp, kolor tekstu — W2, ten sam adres co w arkuszu 7): „Kwatera B · Rząd 4 · Miejsce 12”, a bez pinezki dopisane „· bez pinezki”; bez adresu „Bez adresu kwatery · bez pinezki”. Chevron „›” po prawej. Karta ≥ 64 dp. **(d) miniatura** — tylko gdy grób ma zdjęcie: zdjęcie nagrobka ([[grob]] D9), kwadrat **56 dp** z zaokrągleniem 8 dp, przycięty ze środka, z lewej, wyśrodkowany w pionie, odstęp 12 dp do tekstu; poza czytnikiem. Bez zdjęcia bez miniatury i bez wcięcia ([[grob]] D11). **Grób wybrany w stanie B** ma obrys 1,5 dp w akcencie | lista kart | karta → [[grob]]; przeciągnięcie w dół albo dotknięcie uchwytu (czytnik: „Pokaż mapę”) → stan B albo A | kolejność wpisania | — | AC-1 · AC-5 · R2 · decyzja autora (nazwa grobu) · US-005 AC-1 · D6, D9, D11 |
| 9 | **„Dodaj grób”** pod listą — wypełniony, z ikoną `add`, ≥ 52 dp, przypięty na dole; lista przewija się nad nim, a ostatnia karta ma pod sobą odstęp na wysokość przycisku | przycisk główny | → okno „Nowy grób” (9a, v8; do v7 — [[wpis-osoby]] „nowy grób”) | — | — | *What to build* 2 · D14 |
| 9a | **Okno „Nowy grób”** (v8, [[ISSUE-047-grave-first-then-people]]) nad tym ekranem (stan A albo C): **to samo okno co „Popraw grób”** w [[grob]] — tytuł „Nowy grób”, pola 3a (Nazwa grobu), 3b (Adres zarządcy: Kwatera z chipami kwater tego cmentarza, Rząd, Miejsce) i 3c (Opłacone do), te same podpowiedzi, kolejność `next`, przewijanie (D20) i walidacja; przyciski „Anuluj” · **„Zapisz”** (akcent). **Wszystkie pola opcjonalne** — „Zapisz” przy pustych daje grób bez nazwy („Grób”, [[grob]] D1) | okno dialogowe | fokus i klawiatura od razu w „Nazwa grobu”; „Zapisz” → grób powstaje (zamawia kopię w tle jak każdy zapis) → [[grob]] tego grobu, pusty; „Anuluj” albo wstecz → bez grobu, okno znika (bez pytania „Odrzucić?”, bo przy pustym oknie nic nie przepada; z wpisanym tekstem — też bez pytania, jak „Popraw grób”) | pusto | jak [[grob]] 3a–3c; zła data w 3c → okno zostaje, grób nie powstaje. Błąd zapisu — jak 3a | **decyzja autora** (`/pm` 2026-10-18) · ISSUE-047 AC-1 · [[grob]] D2 · D38 |
| 10 | **„Gdzie jestem”** — okrągły przycisk 48 dp na powierzchni, z prawej nad paskiem grobów (A) albo arkuszem grobu (B), na wysokości „Kwater” (15) i „Popraw pinezkę” (11); w trybie D nad panelem 12a. **Trzy stany (v7, D31):** wyłączony — `my_location` w kolorze tekstu; **włączony, plan na kropce** — `my_location` w kolorze kropki „tu jesteś”; **włączony, plan odsunięty** (po przesunięciu planu) — `location_searching` w kolorze kropki. `tooltip` i opis dla czytnika „Gdzie jestem” ze stanem („włączone, ±5 m”). Na planie **niebieska kropka** 16 dp z obwódką 2 dp w kolorze tła i **kołem dokładności** (promień = dokładność podana przez telefon, w skali planu; kolor kropki, krycie 18%), obok plakietka „tu jesteś · ±5 m” (12 sp, tekst, na powierzchni, rośnie najwyżej do 1,3× — jak nazwa kwatery, reguła 13). Kropka i plakietka poza czytnikiem — stan mówi opis przycisku. Kropka przeskakuje do każdej nowej pozycji, bez animacji | przycisk-ikona | wyłączony → włącza i **jedzie planem do kropki** (płynnie, ok. 300 ms, przybliżenie co najmniej z18); plan na kropce → wyłącza; plan odsunięty → wraca do kropki. Kropka poza obrysem z marginesem (np. w domu) → plan się nie rusza, mówi o tym 10a. Pierwsze użycie → systemowe pytanie o lokalizację | wyłączony przy każdym wejściu na ekran | brak zgody → pasek komunikatu „Bez zgody na lokalizację pinezki postawisz tylko ręcznie.” (ok. 4 s); następne dotknięcie pyta jeszcze raz, jeśli system pozwala, a gdy nie — ten sam komunikat (czy otwierać ustawienia aplikacji — do sprawdzenia w planie) | R2 · [[style-b]] *State colours* · D15 · D31 |
| 10a | **Plakietka stanu lokalizacji (v7)** — tylko przy włączonej lokalizacji, gdy kropki nie widać albo nie warto jej ufać. Z prawej pod przełącznikiem (3), na powierzchni, wys. 32 dp, 13 sp, tekst, ikona w kolorze kropki: (a) **„poza cmentarzem · 2,5 km”** — kropka poza obrysem z marginesem; odległość od środka obrysu, z jedną cyfrą po przecinku, a poniżej 1 km w metrach, zaokrąglona do dziesiątek; (b) **„Szukam pozycji…”** — telefon nie podał jeszcze pozycji; (c) **„tylko przybliżona lokalizacja”** — zgoda „Przybliżona” (Android 12+), bez kropki i bez koła, bo koło przykryłoby cały plan. **Lokalizacja wyłączona w telefonie** → zamiast plakietki pasek komunikatu „Lokalizacja w telefonie jest wyłączona.” z akcją „Włącz” (okno systemu albo ustawienia — do sprawdzenia w planie) | plakietka | — | — | — | D31 |
| 11 | **„Popraw pinezkę”** (stan B, grób z pinezką) — pigułka jak „Kwatery” (15): wys. 40 dp w polu dotyku 48 dp (całe pole reaguje), na powierzchni, `edit_location_alt` w akcencie + „Popraw pinezkę” (14 sp, tekst), z lewej nad arkuszem grobu (R2), margines 12 dp; dla czytnika przycisk „Popraw pinezkę” | przycisk | → tryb D dla tego grobu; **pinezka startuje w zapisanym miejscu** (v7, D35) | — | — | R2 · M6 · D15 · D35 |
| 12 | **Tryb D — „Pinezka grobu” (v7; w v4.2 „stan D”):** pasek: `close` (`tooltip` „Anuluj”), „Pinezka grobu” (18 sp, półgruby) i pod spodem tytuł grobu ([[grob]] D1; 13 sp, tekst pomocniczy). **Bez dolnego paska** ([[style-b]] reguła 12 — tryb, jak F). **U góry karta** jak w 18 — `edit_location_alt` w akcencie i instrukcja (13 sp; teksty → *States*), najwyżej ok. 22% wysokości mapy, a pod nią podpis źródła mapy. **Warstwa (plan albo zdjęcie) z poprzedniego stanu, bez przełącznika** — jak F (D36). Na planie: kwatery jak w 4, znicze innych grobów przygaszone (krycie 55%) i nieaktywne, kropka i koło (10; bez plakietki — dokładność jest w 12a), „gdzie jestem” (10) nad panelem i **znicz w obrysie** ([[style-b]] reguła 13 — miejsce jeszcze niezapisane); czubek znicza to miejsce pinezki, pod czubkiem cień 10 × 4 dp. **Gdzie się dotyka — P1 albo P2, decyzja autora na stopie #1** (*Open*, D34): **P1** — znicz stoi w kropce i idzie za nią; dotknięcie planu przenosi znicz w to miejsce i od tej chwili pinezka jest ręczna; przeciągnięcie przesuwa tylko plan. **P2** — znicz stoi na środku wolnego miejsca między kartą a panelem, a plan idzie za kropką (kropka pod czubkiem). Przeciągnięcie planu albo dotknięcie miejsca (miejsce płynnie podjeżdża pod znicz, ok. 220 ms, jak w F — droga bez przeciągania, SC 2.5.7) przechodzi na ręczne. W obu: **„gdzie jestem” (10) wraca do kropki** — pinezka znowu w kropce, z GPS. Przybliżenie startowe z18, gesty planu jak w 2 | tryb mapy | panel 12a | **start (D32):** nowa pinezka — w kropce, gdy kropka jest w obrysie; inaczej w środku strefy kwatery grobu, a bez strefy — w środku kadru. Poprawa — w zapisanym miejscu (D35) | — | M6 · H3 · **decyzja autora** (SPIKE-004 D22) · D16 · D32–D36 |
| 12a | **Panel trybu D** na dole, na powierzchni, promień 16 dp u góry. Adres grobu ([[grob]] 4; 14 sp, tekst; bez adresu — „Bez adresu kwatery”), a pod nim **źródło, z którym pinezka się zapisze** (14 sp, tekst; ikona `place_outlined` w kolorze tekstu pomocniczego): „Pinezka: GPS ±5 m”, „Pinezka: postawiona na planie” albo „Pinezka: postawiona na zdjęciu z góry” (14, D33). **Poprawa przed zmianą:** „Teraz: GPS ±7 m · 12.10.2026”, a po zmianie „Po zapisie: postawiona na planie”. Przy złym sygnale niżej: `gps_not_fixed` w kolorze tekstu + „Słaby sygnał: ±25 m. Przesuń plan tak, żeby znicz stał na grobie.” (P2) albo „…Dotknij planu tam, gdzie jest grób.” (P1) — 14 sp, kolor tekstu, **bez akcentu i bez koloru błędu**, bo to nie błąd i nie działanie ([[style-b]] *Token roles*). Na dole „Anuluj” (tekstowy) i **„Zapisz pinezkę”** (wypełniony, na resztę szerokości) | panel + przycisk główny | „Zapisz pinezkę” → zapis pozycji, źródła, dokładności (tylko GPS) i daty → stan B z tym grobem (D36); „Anuluj” → *Navigation* | — | **słaby sygnał:** dokładność gorsza niż **15 m — próg tymczasowy** (decyzja autora 2026-10-12; ustawi go pomiar z `CURRENT_STATE.md` → *Parked*, D37); zapis możliwy, dokładność idzie do źródła. Poprawa bez zmiany → „Zapisz pinezkę” nieaktywny (D35). Błąd zapisu → nad przyciskami `error_outline` + „Nie udało się zapisać pinezki. Spróbuj jeszcze raz.” (kolor błędu), tryb zostaje | M6 · H3 · D33 · D35 · D37 |
| 13 | **Bez internetu (M7):** plan bez zmian; plakietka przy „Zdjęciu” — `wifi_off` „bez internetu”, a wybrane „Zdjęcie” pokazuje „Zdjęcie z góry potrzebuje internetu. Plan działa bez niego.” i „Wróć do planu” | stan | — | — | — | [[NFR-001-offline]] · [[ADR-003-map-source-offline]] pkt 2 |
| 14 | **Źródło pinezki w danych (v7, D33):** to, z czego wzięła się pozycja w chwili zapisu — **GPS** (pinezka w kropce, nieruszona; z dokładnością podaną przez telefon, w metrach) albo **ręcznie** na warstwie, na której pinezka stała: **plan** albo **zdjęcie z góry** (bez dokładności). Do tego **data zapisu**. Widać w [[grob]] (4) pod adresem: „Pinezka: GPS ±4 m · 12.10.2026”, „Pinezka: postawiona na planie · 12.10.2026”, „Pinezka: postawiona na zdjęciu z góry · 12.10.2026” (pinezka bez daty — bez „· data”). *(Do v6: „zaznaczona w domu” i link do [[FR-001-provenance]], wycofanego w SPIKE-004 D28. Źródło pinezki to nie źródło faktu o rodzinie.)* | dane | — | — | — | słowniczek → *pinezka* · [[data-model]] → Grave · [[EPIC-002-wizyta]] (każda pinezka ze źródłem i dokładnością) |
| 15 | **„Kwatery” (v6)** — pigułka na powierzchni, wys. 40 dp w polu dotyku 48 dp (całe pole reaguje; dla czytnika przycisk „Kwatery” — v6.1), `pentagon_outlined` w akcencie + „Kwatery” (14 sp, tekst), z lewej nad paskiem grobów (6), margines 12 dp — miejsce „Popraw pinezkę” (11), która jest tylko w B. Kadr planu (2) pigułki nie liczy, tak jak „gdzie jestem” (10) (v6.1; *obali:* strefa rodziny w lewym dolnym rogu cmentarza schowana pod pigułką). **Tylko w stanie A i tylko wtedy, gdy jest na czym rysować:** plan (2) albo „Zdjęcie” z siecią. Przy zaślepce 2a i przy „Zdjęciu” bez sieci (13) jej nie ma | przycisk | → tryb E (16) | — | — | [[ISSUE-028-cemetery-sectors]] *What to build* 1 · D24 |
| 16 | **Tryb E — „Kwatery” (v6):** pasek: `close` (`tooltip` „Zamknij kwatery”), „Kwatery” (18 sp, półgruby) i pod spodem nazwa cmentarza (13 sp, tekst pomocniczy). **Bez dolnego paska** ([[style-b]] reguła 12 — tryb). Plakietki i przełącznik Plan · Zdjęcie (3) zostają, bo kwaterę zaznacza się na planie albo na zdjęciu. Kadr: plan zostaje, jak był w A, gdy wszystkie strefy już są w wolnym miejscu nad arkuszem (margines 48 dp); inaczej przybliżenie maleje, aż się zmieszczą; bez stref — jak w A (v6.1). Znicze (5) widoczne w zwykłym wyglądzie i **nieaktywne** (jak [[cmentarze]] D21), żeby było widać, gdzie leżą znane groby | tryb mapy | strefa → 17b; gesty planu jak w 2 | lista (17a) | — | D24 |
| 17 | **Arkusz kwater (tryb E)** na powierzchni, z uchwytem. **(a) Lista:** karta na kwaterę — w kolorze tła na arkuszu, promień 14 dp, odstęp 8 dp, ≥ 56 dp: „Kwatera A” (16 sp, półgruby) i pod spodem „2 groby · na planie”, „2 groby · bez strefy — tylko w adresach” albo „bez grobów · na planie” (14 sp, kolor tekstu — W2), chevron „›”; kolejność naturalna po nazwie (2, 10, A, B — liczby jako liczby, cyfry przed literami, jak w całej aplikacji — v6.1). Pod listą **wypełniony „Zaznacz kwaterę”** (`add`, ≥ 52 dp, pełna szerokość). Lista dłuższa niż pół ekranu przewija się w arkuszu. **Bez kwater:** „Na tym cmentarzu nie ma jeszcze kwater. Zaznacz te, w których leży rodzina — według planu zarządcy.” (14 sp, tekst) i „Zaznacz kwaterę”. **(b) Kwatera wybrana:** ‹ (`tooltip` „Wszystkie kwatery”), „Kwatera B” (18 sp, półgruby), ✎ (`edit_outlined`, akcent, `tooltip` „Zmień nazwę kwatery”); pod spodem ta sama linia co w karcie; przycisk z obrysem **„Narysuj strefę”** (bez strefy) albo **„Narysuj strefę od nowa”** (`pentagon_outlined` w akcencie); gdy strefa jest — przycisk tekstowy **„Usuń z planu”** (`delete_outline`, kolor tekstu — [[style-b]] reguła 14). Plan przesuwa się płynnie tak, żeby strefa stała w środku wolnego miejsca nad arkuszem w obecnym przybliżeniu, a przybliżenie maleje tylko wtedy, gdy strefa się nie mieści (v6.1) | dolny arkusz | karta → (b); ✎ → 19b; „Narysuj…” → F; „Usuń z planu” → 19c; „Zaznacz kwaterę” → 19a | — | — | ISSUE-028 *What to build* 1, 3 · D25–D27 |
| 18 | **Tryb F — zaznaczanie strefy (v6):** pasek: `close`, „Kwatera D — strefa” (18 sp, półgruby) i pod spodem „Zaznacz rogi według planu zarządcy” albo przy rysowaniu od nowa „Stara strefa jest szara” (13 sp, tekst pomocniczy). Bez dolnego paska. **U góry karta** (jak 12) z `pentagon_outlined` w akcencie i instrukcją K1 (v6.1, dosłownie): „Przesuń plan tak, żeby celownik stał na rogu kwatery, i dotknij „Dodaj róg”. Możesz też dotknąć miejsca na planie — przesunie się pod celownik.” — zamiast plakietek; karta najwyżej ok. 22% wysokości mapy, przewijana z widocznym paskiem, a pod nią podpis źródła mapy jak w 3 („© OpenStreetMap” albo „Ortofotomapa: GUGiK”) (v6.1); warstwa (plan albo zdjęcie) zostaje z trybu E. Na planie: inne kwatery jak w 4, znicze przygaszone (krycie 55%) i nieaktywne, **stara strefa** (od nowa) przerywaną linią 2 dp w kolorze tekstu pomocniczego (5,01:1 na powierzchni, 1,62:1 wobec alejek — w kolorze obrysu znikała wzdłuż nich; v6.1). **Rogi:** koło 14 dp w akcencie z obwódką 2 dp w kolorze tła. **Boki:** 2,5 dp w akcencie na linii 5 dp w kolorze tła (widać je na planie i na zdjęciu), bok zamykający (ostatni → pierwszy róg) przerywany; od 3 rogów nazwa „Kwatera D” w akcencie jak w 4. **Dolny panel** na powierzchni: liczba rogów — „2 rogi — potrzebne co najmniej 3” / „4 rogi” (13 sp, tekst); przycisk z obrysem **„Cofnij”** (`undo` w akcencie), a przy tekście > 130% sama ikona `undo` 52 × 52 dp z `tooltip` „Cofnij” (v6.1); **wypełniony „Gotowe”** na pełną szerokość, nieaktywny poniżej 3 rogów | tryb mapy | „Cofnij” → bez ostatniego rogu (K3: bez ostatniej zmiany); „Gotowe” → zapis → E z tą kwaterą wybraną (17b); ✕/wstecz → *Navigation*. **Gesty — według kandydata:** **K1** celownik na środku wolnego miejsca (krzyż 28 dp i koło 18 dp, linia 1,6 dp w kolorze tekstu z obwódką w kolorze tła); przeciągnięcie przesuwa plan, **dotknięcie planu przesuwa to miejsce pod celownik** (ok. 220 ms — droga bez przeciągania, SC 2.5.7); przycisk z obrysem **„Dodaj róg”** (`add_circle_outline`) obok „Cofnij” stawia róg pod celownikiem. **K2** dotknięcie planu stawia róg, przeciągnięcie przesuwa plan; podwójne dotknięcie nie przybliża (stawiałoby rogi), więc przybliżanie dwoma palcami i **przyciskami „+ −”** (SC 2.5.1). **K3** na starcie prostokąt ok. 140 dp na środku wolnego miejsca; przeciągnięcie rogu go przesuwa, **dotknięcie rogu go wybiera** (pierścień 2 dp w akcencie), a dotknięcie planu przenosi wybrany róg (SC 2.5.7); „+” w połowie boku (koło 18 dp na powierzchni z obrysem, cel 48 dp) dodaje róg; przeciągnięcie poza rogiem przesuwa plan | — | boki, które się przecinają → pod liczbą rogów `error_outline` + „Boki strefy się przecinają — cofnij ostatni róg.” (kolor błędu; v6.1 — w K1 rogu nie da się przesunąć), „Gotowe” nieaktywne | ISSUE-028 *What to build* 1 · prior art (*Decisions* D30) · D26 |
| 19 | **Okna (v6),** według [[style-b]] reguły 1 (okno) i 10. **(a) „Nowa kwatera”:** pole z przedrostkiem „Kwatera ” (ramka w kolorze obrysu), fokus i klawiatura od razu, klawiatura tekstowa bez wymuszonych wielkich liter, `done` = „Dalej”; pod polem „Sama nazwa, jak na planie zarządcy, np. B albo 12.” (13 sp, tekst pomocniczy); „Anuluj” · **„Dalej”** (akcent). **(b) „Nazwa kwatery”** (✎): to samo pole z obecną nazwą; pod polem skutek dla adresów — W-a: „Adresy 2 grobów zmienią się na „Kwatera B1”.”; W-b: „Adresy grobów zostaną bez zmian: 2 groby z „Kwatera B” przestaną pasować do tej strefy.”; kwatera bez grobów — bez tej linii; „Anuluj” · **„Zapisz”**. **(c) „Usunąć kwaterę B z planu?”** — „Strefa zniknie z planu. Adresy grobów zostaną.”; „Usuń” (kolor tekstu) · **„Zostaw”** (akcent). **(d) „Porzucić zaznaczanie?”** — „Zaznaczone rogi przepadną.”; „Porzuć” (kolor tekstu) · **„Rysuj dalej”** (akcent) | okna dialogowe | (a) „Dalej” → F; (b) „Zapisz” → 17b z nową nazwą; (c) „Usuń” → 17a (kwatera bez grobów znika, z grobami zostaje „bez strefy”); (d) „Porzuć” → E | (a) pusto; (b) obecna nazwa | (a), (b): puste → „Podaj nazwę kwatery.”; ta sama nazwa na tym cmentarzu (bez wielkości liter, polskich znaków i słowa „Kwatera” na początku) → (a) „Kwatera B już jest na liście — wybierz ją tam.”, (b) „Kwatera B już jest na tym cmentarzu — wpisz inną nazwę.” (v6.1 — zmiana nazwy nie łączy kwater) (kolor błędu + `error_outline`), okno zostaje; wpisane „Kwatera B” zapisuje się jako „B”; spacje na brzegach obcięte | D25 · D27 · *Open* W-a/W-b |

Imię i nazwisko w liście osób: „Imiona Nazwisko” bez nazwiska rodowego — „z d.” jest w [[grob]]. Osoba bez
imion albo bez nazwiska: to, co jest. Spór źródeł o grób ([[ADR-006-claimed-value-separate-structures]] D2):
osoba z dwoma pochówkami stoi w obu grobach, jak w [[grob]].

## States
| Stan | Co widać |
|---|---|
| A — mapa | 1–6 |
| B — jeden grób | 1–5, 7; pasek grobów (6) schowany |
| C — lista | 1, 8, 9 |
| plan się pobiera (v5) | 1, 2a (a), przełącznik (3), pasek grobów (6) — lista działa |
| bez planu: bez internetu | 1, 2a (b), przełącznik (3), pasek grobów (6) — lista działa |
| bez planu: serwer nie odpowiada (v5) | 1, 2a (c), przełącznik (3), pasek grobów (6) |
| bez planu: brak obrysu w OSM (v5) | 1, 2a (d), przełącznik (3), pasek grobów (6) |
| bez punktu (v5) | 1, 2a (e), pasek grobów (6); bez przełącznika |
| bez pinezek (np. zaraz po przepisaniu) | 1–4 bez zniczy, pasek (6): „6 grobów bez pinezki — na liście” |
| bez grobów | 1–4, pasek (6): „Na tym cmentarzu nie ma jeszcze grobów.” (tekst pomocniczy) i „Dodaj grób” |
| błąd | „Nie udało się odczytać grobów.” (tekst pomocniczy) + „Spróbuj ponownie” (przycisk z obrysem); „Dodaj grób” nieaktywny, bo nie wiadomo, do czego dodaje |
| wczytywanie | wskaźnik postępu w środku (lokalna baza — zwykle niewidoczny) |
| grób bez osób | **v8: powstaje z okna „Nowy grób” (9a)** — do v7 tylko z innych danych. Karta z nazwą: tytuł — nazwa grobu, (b) „bez wpisanych osób” (14 sp, tekst pomocniczy); bez nazwy: tytuł karty „Grób bez wpisanych osób” w kolorze pomocniczym. Adres (c) i miniatura (d) bez zmian. Podsumowanie liczy taki grób („3 groby · 2 osoby”) |
| brak pliku zdjęcia | wpis zdjęcia jest, pliku nie ma: karta bez miniatury (o braku mówi [[grob]] → *States*) |
| A, B z lokalizacją (v7) | jak A, B + kropka, koło i „tu jesteś · ±5 m” (10); przycisk 10 w kolorze kropki |
| lokalizacja: poza cmentarzem · szukam pozycji · tylko przybliżona (v7) | jak A, B + 10a (a), (b) albo (c); plan się nie rusza |
| lokalizacja: brak zgody · wyłączona w telefonie (v7) | jak A, B + pasek komunikatu z 10 albo 10a; przycisk 10 wyłączony |
| D — z GPS (v7) | 12, 12a; znicz w kropce; karta: „**Stań przy grobie.** Pinezka stoi w niebieskiej kropce. Jeśli nie trafia w grób, dotknij planu tam, gdzie grób jest.” (P1) · „**Stań przy grobie.** Plan idzie za niebieską kropką, a znicz stoi w niej. Jeśli nie trafia w grób, przesuń plan albo dotknij miejsca grobu.” (P2); 12a: „Pinezka: GPS ±5 m” |
| D — ręcznie (v7) | 12, 12a; karta: „Dotknij planu tam, gdzie jest grób. ◎ postawi pinezkę w Twojej pozycji.” (P1) · „Przesuń plan tak, żeby znicz stał na grobie. Możesz też dotknąć miejsca na planie — przesunie się pod znicz. ◎ wraca do Twojej pozycji.” (P2), w miejscu ◎ ikona `my_location`; 12a: „Pinezka: postawiona na planie” (albo „na zdjęciu z góry”) |
| D — słaby sygnał (v7) | D z GPS + linia „Słaby sygnał: ±N m…” w 12a (próg tymczasowy 15 m, D37) |
| D — bez zgody · tylko przybliżona (v7) | D ręcznie; karta: „Bez zgody na lokalizację pinezkę postawisz ręcznie: …” (dalej tekst D ręcznie bez zdania o ◎) · „Telefon podaje tylko przybliżoną lokalizację — postaw pinezkę ręcznie. Dokładną włączysz w ustawieniach telefonu.” |
| D — szukam pozycji · poza cmentarzem (v7) | D ręcznie, pinezka w środku strefy kwatery grobu (D32). W 12a pod źródłem (14 sp, tekst pomocniczy): „Szukam pozycji…” albo „Jesteś poza cmentarzem (2,5 km).” — w trybie D plakietki 10a nie ma, bo jej miejsce zajmuje karta. Gdy pozycja przyjdzie w obrysie, a pinezki nikt nie ruszył, pinezka przeskakuje do kropki (z GPS) |
| D — poprawa przed zmianą (v7) | D ręcznie w zapisanym miejscu; 12a: „Teraz: …”, „Zapisz pinezkę” nieaktywny (D35) |
| błąd zapisu pinezki (v7) | D zostaje; w 12a nad przyciskami `error_outline` + „Nie udało się zapisać pinezki. Spróbuj jeszcze raz.” (kolor błędu) |
| bez internetu | 1–6, 13; „Kwatery” (15) tylko na planie |
| A z kwaterami (v6) | 1–6 ze strefami (4) i „Kwatery” (15) |
| E — lista kwater (v6) | 16, 2–5 (strefy, znicze nieaktywne), 17a |
| E — bez kwater (v6) | 16, 2, 3, 5, 17a: „Na tym cmentarzu nie ma jeszcze kwater…” i „Zaznacz kwaterę” |
| E — kwatera wybrana (v6) | 16, 4 (wybrana w akcencie), 17b |
| E — kwatera bez strefy wybrana (v6) | 16, 17b z „Narysuj strefę”, bez „Usuń z planu”; kadr bez zmian |
| F — zaznaczanie strefy (v6) | 18 (pasek, karta, rogi, boki, dolny panel); 2 z kwaterami i przygaszonymi zniczami |
| F — „Zdjęcie” bez sieci (v6) | 18 z 13 („Zdjęcie z góry potrzebuje internetu…”, „Wróć do planu”); rogi zostają |
| błąd zapisu kwatery (v6) | F albo okno 19 zostaje; pod „Gotowe” (albo pod polem) `error_outline` + „Nie udało się zapisać kwatery. Spróbuj jeszcze raz.” (kolor błędu); rogi i wpis zostają |
| błąd odczytu kwater (v6) | 17a: „Nie udało się odczytać kwater.” (tekst pomocniczy) + „Spróbuj ponownie” (przycisk z obrysem); „Zaznacz kwaterę” nieaktywny. Plan w A rysuje się bez stref |

## Sketch
v4 — stan A (mapa) i stan B (jeden grób):
```
┌──────────────────────────────────┐   ┌──────────────────────────────────┐
│ ←  Cmentarz parafialny w       ✎ │   │ ←  Cmentarz parafialny w       ✎ │
│    Wymyślonowie · Wymyślonów     │   │    Wymyślonowie · Wymyślonów     │
│ (✓ Plan offline)  [Plan|Zdjęcie] │   │ (✓ Plan offline)  [Plan|Zdjęcie] │
│ © OpenStreetMap                  │   │  ┌ ─ ─ ─ ─ ─┐┌ ─ ─ ─ ─ ─ ─┐      │
│                                  │   │  │  ⚱   ⚱   ││   ⚱    ⚱   │      │  ← plan nad arkuszem
│  ┌ ─ ─ ─ ─ ─┐┌ ─ ─ ─ ─ ─ ─┐      │   │  │Kwatera A ││ Kwatera B  │      │
│  │  ⚱   ⚱   ││   ⚱    ⚱   │      │   │  └ ─ ─ ─ ─ ─┘└ ─ ─ ─ ─ ─ ─┘      │
│  │Kwatera A ││ Kwatera B  │      │   │ ╭──────────────────────────────╮ │
│  └ ─ ─ ─ ─ ─┘└ ─ ─ ─ ─ ─ ─┘      │   │ │ ▓▓▓  Grób rodzinny Wymyślon… │ │
│      (alejki, obrys)             │   │ │ ▓▓▓  Kwatera A · Rząd 2 · M… │ │
│ ╭──────────────────────────────╮ │   │ │      👥 3 osoby               │ │
│ │ 6 grobów · 14 osób   ── uchwyt │ │   │ │ ╭──────────────────────────╮ │ │
│ │ 2 groby bez pinezki — na liście│ │   │ │ │     ⚱  Pokaż grób        │ │ │  ← wypełniony
│ │ ╭──────────────────────────╮ │ │   │ │ ╰──────────────────────────╯ │ │
│ │ │      +  Dodaj grób       │ │ │   │ ╰──────────────────────────────╯ │
│ │ ╰──────────────────────────╯ │ │   │  Mapa      Osoby      Drzewo     │
│ ╰──────────────────────────────╯ │   └──────────────────────────────────┘
│  Mapa      Osoby      Drzewo     │
└──────────────────────────────────┘
```
v5 — zaślepki planu 2a (a)–(e) i warianty W1/W2 z *Open*: makieta `issue-027-mapa-cmentarza.html` (katalog tymczasowy
sesji 2026-10-12). Zaślepka stoi w miejscu planu, nad paskiem grobów; przełącznik w prawym górnym rogu zostaje (poza (e)).

Stan C (lista) — karty jak w v3, na cały ekran pod paskiem (1), z wypełnionym „Dodaj grób” na dole. Szkice v2 i v3:
*Historia* w nagłówku i makiety z 2026-10-07.

v6 — tryb E (lista kwater) i tryb F (zaznaczanie strefy, kandydat K1); K2 i K3 — prototyp `issue-028-kwatery.html`:
```
┌──────────────────────────────────┐   ┌──────────────────────────────────┐
│ ✕  Kwatery                       │   │ ✕  Kwatera D — strefa            │
│    Cmentarz parafialny w Wymyś…  │   │    Zaznacz rogi według planu za… │
│ (✓ Plan offline)  [Plan|Zdjęcie] │   │ ╭──────────────────────────────╮ │
│  ┌ ─ ─ ─ ─ ─┐ ┌ ─ ─ ─ ─ ─┐       │   │ │⬠ Przesuń plan tak, żeby cel- │ │
│  │  ⚱   ⚱   │ │   ⚱      │       │   │ │  ownik stał na rogu kwatery… │ │
│  │Kwatera A │ │Kwatera B │       │   │ ╰──────────────────────────────╯ │
│  └ ─ ─ ─ ─ ─┘ └ ─ ─ ─ ─ ─┘       │   │  ┌ ─ ─ ─ ─┐ ┌ ─ ─ ─ ─┐          │
│ ╭──────────────────────────────╮ │   │  │Kwatera A│ │Kwatera B│         │
│ │ ╭──────────────────────────╮ │ │   │  ●━━━━━━━━●  ⊕ ← celownik       │
│ │ │ Kwatera A              › │ │ │   │  ┆         ┃                    │
│ │ │ 2 groby · na planie      │ │ │   │  ┆Kwatera D┃                    │
│ │ ╰──────────────────────────╯ │ │   │  ●━━━━━━━━●                     │
│ │ ╭──────────────────────────╮ │ │   │ ╭──────────────────────────────╮ │
│ │ │ Kwatera C              › │ │ │   │ │ 4 rogi                       │ │
│ │ │ 2 groby · bez strefy — … │ │ │   │ │ [↶ Cofnij] [⊕ Dodaj róg    ] │ │
│ │ ╰──────────────────────────╯ │ │   │ │ ╭──────────────────────────╮ │ │
│ │ ╭──────────────────────────╮ │ │   │ │ │         Gotowe           │ │ │
│ │ │    +  Zaznacz kwaterę    │ │ │   │ │ ╰──────────────────────────╯ │ │
│ ╰──────────────────────────────╯ │   │ ╰──────────────────────────────╯ │
└──────────────────────────────────┘   └──────────────────────────────────┘
```

v7 — stan B z lokalizacją i „Popraw pinezkę”; tryb D z GPS (kandydat P2). P1 — prototyp `issue-029-pinezka.html`:
```
┌──────────────────────────────────┐   ┌──────────────────────────────────┐
│ ←  Cmentarz parafialny w       ✎ │   │ ✕  Pinezka grobu                 │
│    Wymyślonowie · Wymyślonów     │   │    Grób rodzinny Zmyślonych      │
│ (✓ Plan offline)  [Plan|Zdjęcie] │   │ ╭──────────────────────────────╮ │
│ © OpenStreetMap                  │   │ │⌖ Stań przy grobie. Plan idzie│ │
│  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┐          │   │ │  za niebieską kropką, a znicz│ │
│  │  ⚱                 │          │   │ │  stoi w niej. Jeśli nie tra… │ │
│  │     ⚱wybrany  ●    │          │   │ ╰──────────────────────────────╯ │
│  │Kwatera B           │          │   │  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┐       │
│  └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┘          │   │  │   ⚱(przygaszony)     │       │
│ (⌖ Popraw pinezkę)          (◎)  │   │  │────────────────────  │       │
│ ╭──────────────────────────────╮ │   │  │        ⚲  ← znicz w   │       │
│ │ Grób rodzinny Zmyślonych     │ │   │  │        ●    obrysie,  │       │
│ │ Kwatera B · Rząd 4 · Miej… 12│ │   │  │Kwatera B   w kropce  │       │
│ │ 👥 2 osoby                    │ │   │  └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┘  (◉) │
│ │ ╭──────────────────────────╮ │ │   │ ╭──────────────────────────────╮ │
│ │ │     ⚱  Pokaż grób        │ │ │   │ │ Kwatera B · Rząd 4 · Miej… 12│ │
│ │ ╰──────────────────────────╯ │ │   │ │ ⌖ Pinezka: GPS ±5 m          │ │
│ ╰──────────────────────────────╯ │   │ │ Anuluj  ╭──────────────────╮ │ │
│  Mapa      Osoby      Drzewo     │   │ │         │  Zapisz pinezkę  │ │ │
└──────────────────────────────────┘   │ ╰─────────╰──────────────────╯─╯ │
                                       └──────────────────────────────────┘
```
● — kropka „tu jesteś” z kołem dokładności; w A i B obok niej plakietka „tu jesteś · ±5 m” (10). ◎ — „gdzie jestem”, ◉ — włączone,
plan na kropce.

## Tempo
Rekordem jest **grób**: ok. 50 na całe notatki (G6, [[NT-002-transcribe-the-notes]]).
- **Nowy grób** (v8): stan A → „Dodaj grób” → „Zapisz” w oknie 9a (nazwa opcjonalna) → w pustym grobie „Dodaj osobę” → „Nowa osoba” =
  **4 dotknięcia** do formularza pierwszej osoby (do v7 — 1). Na ok. 50 grobów to ok. 150 dotknięć więcej (D38). Imię pierwszej osoby wpisuje
  się już w szukaniu ([[grob]] 9), więc formularz go nie powtarza ([[wpis-osoby]] → *Tempo*).
- **Pierwszy grób na nowym cmentarzu:** znicz → „Otwórz cmentarz” → „Dodaj grób” = 3 dotknięcia (jak w v3).
- **Grób bez pinezki:** pasek → karta = **2 dotknięcia** (w v3 jedno). Przy przepisywaniu wszystkie groby są bez
  pinezki, ale przepisywanie prowadzi „Dodaj grób”, a do listy wraca się rzadziej.
- **Grób z pinezką:** znicz → „Pokaż grób” = 2 dotknięcia.
- **Nazwa grobu** nie kosztuje tu nic — nadaje się ją w [[grob]].
- **Kwatera (v6):** rekordem jest kwatera, w której leży rodzina — kilkanaście na całe notatki (11 cmentarzy, SPIKE-001), raz, w
  domu. „Kwatery” → „Zaznacz kwaterę” → nazwa (1–3 znaki) → „Dalej” → rogi → „Gotowe”. Rogi prostokątnej kwatery: **K1** 4 ×
  (przesunięcie albo dotknięcie planu + „Dodaj róg”) = 8 ruchów; **K2** 4 dotknięcia; **K3** 4 przeciągnięcia (albo 8 dotknięć).
  Razem 8–12 dotknięć na kwaterę. Wpis jest rzadki, więc tempo nie rozstrzyga między kandydatami — rozstrzyga, czy róg staje
  tam, gdzie autor celował, i ile pomyłek trzeba cofać.
- **Pinezka (v7):** rekordem jest grób na wizycie — ok. 50 na całe notatki, przy grobie, często w zimnie i jedną ręką. Z [[grob]]:
  „Postaw pinezkę” → (stoisz przy grobie) → „Zapisz pinezkę” = **2 dotknięcia**, pierwszy raz +1 na zgodę systemu. Z mapy, grób
  bez pinezki: pasek → karta → „Postaw pinezkę” → „Zapisz pinezkę” = 4. Ręczna poprawka: **P1** +1 dotknięcie, **P2** +1
  przeciągnięcie albo +1 dotknięcie. Tempo nie rozstrzyga między P1 a P2 — rozstrzyga, czy pinezka staje tam, gdzie autor
  celował (palec przy P1 zasłania przy z19 ok. 8–9 m planu, cel 48 dp — *Open*, znicze), i czy idąc z telefonem nie przestawi
  jej przypadkiem.

## Style B rules applied
- **Reguła 1:** jeden wypełniony przycisk w każdym stanie — A: „Dodaj grób”, B: „Pokaż grób”, C: „Dodaj grób”.
  Ten sam „Dodaj grób” w A i C (decyzja autora, D14).
- **Reguła 8:** „Pokaż grób” ze zniczem (prowadzi do miejsca pamięci), „Dodaj grób” bez znicza (działanie).
- **Reguły 2 i 11:** karty na powierzchni z chevronem, miniatura nagrobka z lewej, gdy zdjęcie jest.
- **Reguła 12:** pasek dolny we wszystkich stanach. **Reguła 15:** ✎ w pasku.
- **Reguła 13 (v1.14):** plan, kwatery autora, znicze; zieleń „Plan offline” tylko z ikoną i podpisem (SC 1.4.1).
- **Reguła 14:** miniatury bez filtrów i bez tekstu; zdjęcie z góry to treść z zewnątrz — na nim tylko znicze,
  nazwy kwater z obwódką i plakietki na powierzchni.
- **Reguły 4–7:** tytuły półgrube; margines 16 dp, 8 dp między kartami; adres pełnymi słowami, liczby odmienione;
  „bez pinezki” to fakt w tekście pomocniczym. **Reguła 7 (v5):** każdy brak planu ma fakt i drogę naprzód (2a, D17), ton
  spokojny, bez wykrzykników — także przy błędzie serwera.
- **Gesty (v5):** przeciągnięcie arkusza ma alternatywę w dotknięciu uchwytu (D21, SC 2.5.7).
- **Kwatery (v6):**
  - **reguła 1:** jeden wypełniony przycisk — E: „Zaznacz kwaterę”, F: „Gotowe”; w oknach przyciski tekstowe;
  - **reguła 12:** tryby E i F bez dolnego paska;
  - **reguła 13 (v1.22):** kwatera wybrana w akcencie, rysowana strefa w akcencie na linii w kolorze tła;
  - **reguła 14 (v1.22):** rysowanie na zdjęciu z góry to wyjątek jak ramka kadru — rogi, boki i celownik, bez tekstu poza nazwą
    kwatery; „Usuń z planu” bez koloru błędu, „Zostaw” w akcencie;
  - **reguła 10:** okno tylko przy porzuceniu rogów i przy usunięciu strefy;
  - **gesty:** K1 i K3 mają drogę bez przeciągania (SC 2.5.7); K2 wymaga przycisków „+ −” (SC 2.5.1).
- **Pinezka (v7):**
  - **reguła 1:** jeden wypełniony przycisk w D — „Zapisz pinezkę”; „Popraw pinezkę” to pigułka jak „Kwatery”;
  - **reguła 12:** tryb D bez dolnego paska, jak E i F;
  - **reguła 13:** znicz w obrysie = miejsce niezapisane; znicze innych grobów przygaszone; kropka „tu jesteś” w kolorze stanu
    (*State colours*), nigdy w akcencie;
  - **reguła 7 i *Token roles*:** słaby sygnał to fakt w kolorze tekstu, bez akcentu (akcent nie dla ostrzeżeń) i bez koloru błędu;
    każdy brak lokalizacji ma drogę naprzód — ręczne stawianie;
  - **gesty:** P2 ma drogę bez przeciągania (dotknięcie, jak F); P1 jej nie potrzebuje (SC 2.5.7).
- **Tokeny:** zieleń offline `stateOk` (w `theme.dart` od [[ISSUE-022-app-skeleton-tabs-people-settings]]); v5 i v6 bez nowych
  tokenów. **v7 — nowy token: kropka „tu jesteś”** (`#5EA2E6`, propozycja z [[style-b]] *State colours* v1.16; wpisze `dev` w
  `theme.dart`, np. `GrobingColors.here`). Pomiar ([[style-b]] v1.16): 6,99:1 na tle, 6,38:1 na powierzchni (SC 1.4.11 ≥ 3:1);
  znicz w obrysie (akcent) 8,04:1 na powierzchni; tekst 12a 10,02:1, ikona źródła (tekst pomocniczy) 5,01:1 na powierzchni.
  Koło dokładności (krycie 18%) nie niesie informacji samo — liczbę mówią plakietka i 12a (SC 1.4.1). **Pomiar v6** (wzór WCAG, 2026-10-12): linia kwatery (tekst 75%) 6,16:1 na powierzchni; nazwa kwatery 10,02:1; akcent
  (wybrana, rysowana) 8,04:1 na powierzchni; stara strefa (obrys) 3,10:1; akcent wobec linii kwatery tylko 1,31:1, więc wybór
  niesie też grubość (2,5 dp) i nazwa w arkuszu 17b (SC 1.4.1). Kontrast: tytuł karty 10,02:1, linie pomocnicze 5,01:1 na powierzchni (W2 z *Open*: 10,02:1), zieleń 8,19:1 na
  powierzchni, alejki (obrys) 3,10:1 na powierzchni (SC 1.4.11).

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-002 AC-1 | 8 → [[grob]] | karta grobu wymienia wszystkie wpisane osoby; po dotknięciu każda ma kartę w [[grob]] |
| US-002 AC-5 | 6, 8 (c), 9 | grób zapisany z samym cmentarzem i osobami ma kartę z „Bez adresu kwatery · bez pinezki”, a pasek liczy groby bez pinezki |
| ISSUE-012: „Otwórz cmentarz” otwiera ekran cmentarza | [[cmentarze]] element 7 → 1 | arkusz cmentarza na mapie → „Otwórz cmentarz” → pasek z nazwą tego cmentarza |
| decyzja autora 2026-10-06: nazwa grobu | 7, 8 (a) | grób z nazwą nadaną w [[grob]] ma ją jako tytuł karty i arkusza |
| ISSUE-012: styl B | całość | reguły wyżej; przegląd `ui` przed stopem #2 |
| US-005 AC-1 | 7, 8 (d) | grób ze zdjęciem dodanym w [[grob]] ma jego miniaturę w karcie i w arkuszu |
| US-007 AC-1 — plan offline | 2, 3 | cmentarz dodany z siecią, w trybie samolotowym: plan (obrys, alejki), „Plan offline” z ikoną, „© OpenStreetMap” |
| US-007 AC-2 — zdjęcie z góry online | 3, 13 | „Zdjęcie” z siecią: ortofotomapa i „Ortofotomapa: GUGiK”; bez sieci „bez internetu”, „Wróć do planu”, a plan działa; w pamięci telefonu nie przybywa plików |
| US-007 AC-3 — sama mapa, jeden grób, lista | 5, 6, 7, 8 · *Navigation* | na starcie plan i pasek z liczbą grobów bez pinezki; znicz → arkusz z „Pokaż grób”; pasek albo uchwyt → lista wszystkich grobów |
| US-007 AC-4 — kwatery autora | 4, 15–19 | kwatera zaznaczona w trybie „Kwatery” ma na planie (i na zdjęciu) przerywaną linię z „Kwatera B” w lewym dolnym rogu; kwatera tylko z adresu grobu jest na liście 17a jako „bez strefy — tylko w adresach”, a na planie jej nie ma |
| ISSUE-028 *What to build* 3 — poprawa i usunięcie | 17b, 18, 19b, 19c | ✎ zmienia nazwę (z linią o adresach), „Narysuj strefę od nowa” rysuje na starej strefie, „Usuń z planu” zdejmuje strefę, a adresy grobów zostają |
| ISSUE-028 — kwatera wraca po odtworzeniu z kopii | 4, 17a | po odtworzeniu ta sama lista kwater i te same strefy na planie — sprawdza `qa` (dane, nie ekran) |
| US-007 AC-5 — bez planu | 2a (b), 6 | cmentarz dodany bez sieci: „pobierze się, gdy będzie internet”, „Pobierz teraz”, a pasek prowadzi do listy |
| US-008 AC-1 — gdzie jestem | 10, 10a | ◎ → (pierwszy raz) pytanie systemu → niebieska kropka z kołem i „tu jesteś · ±5 m”, plan jedzie do kropki; „Nie zezwalaj” → „Bez zgody na lokalizację pinezki postawisz tylko ręcznie.”, a tryb D działa ręcznie |
| US-008 AC-2 — postaw pinezkę | [[grob]] 4 → 12, 12a, 14 | grób bez pinezki → „Postaw pinezkę” → znicz w obrysie w kropce; dotknięcie (P1) albo przesunięcie planu (P2) go przenosi; „Zapisz pinezkę” → stan B z nowym zniczem, a w [[grob]] „Pinezka: GPS ±5 m · 12.10.2026” albo „postawiona na planie · …” |
| US-008 AC-3 — popraw pinezkę | 11 → 12, 12a | grób z pinezką: znicz → B → „Popraw pinezkę” → ten sam tryb, start w zapisanym miejscu, „Teraz: …”; po zmianie „Zapisz pinezkę” zapisuje nowe miejsce |
| US-008 AC-4 — bez internetu | 10, 12, 13 | w trybie samolotowym: kropka, koło i tryb D działają na planie offline; „Zdjęcie” mówi „bez internetu” (13) |
| ISSUE-029 — pinezka z datą wraca po odtworzeniu | 5, 14 → [[grob]] 4 | po odtworzeniu ten sam znicz i ta sama linia „Pinezka: …” z datą — sprawdza `qa` (dane, nie ekran) |

## Decisions
- **D1 — „jak R2 bez satelity” = arkusz grobów na cały ekran, bez pola mapy.** *(Zastąpione w v4 przez D10–D11.)* Groby z notatek nie mają
  pinezek, a ISSUE-012 nie daje sposobu ich postawienia (pinezka → [[EPIC-002-wizyta]], M6). Pole mapy bez
  zdjęcia satelitarnego i bez ani jednej pinezki byłoby stale pustym prostokątem nad listą — na ekranie
  używanym ok. 50 razy. **Kierunek:** gdy [[SPIKE-001-map-source-offline]] da zdjęcie cmentarza, a groby
  dostaną pinezki, mapa staje nad listą, a lista zamienia się w dolny arkusz jak w R2 (makieta, ramka 8 —
  poglądowo, nie w ISSUE-012). Wtedy grób z pinezką ma znicz na mapie, a grób bez — tylko kartę w arkuszu.
  *Obali:* autor chce widzieć pole mapy już teraz (np. punkt cmentarza na mapie Polski) — wtedy pasek mapy
  nad arkuszem, z ryzykiem pustego miejsca.
- **D2 — „z pinezką i bez” to dopisek w karcie, nie dwie sekcje.** W ISSUE-012 żaden grób nie będzie miał
  pinezki, więc sekcja „z pinezką” byłaby zawsze pusta. Dopisek „· bez pinezki” niesie to samo w każdej
  karcie i zniknie sam, gdy pinezka powstanie.
- **D3 — karta bez przycisku „Pokaż grób” z R2.** *(W v4 „Pokaż grób” wraca w arkuszu grobu ze znicza — D11.)* R2 to arkusz jednego wybranego grobu, więc ma przycisk. Na
  liście cała karta prowadzi do grobu (reguła 11), a jeden wypełniony przycisk na ekranie należy do „Dodaj
  grób” (reguła 1). „Pokaż grób” ze zniczem wraca z arkuszem pod mapą (D1).
- **D4 — karta bez liczby osób** („3 osoby” z R2): *(w v4 „3 osoby” wraca w arkuszu grobu ze znicza — D11)* karta wymienia osoby z imienia, więc liczba byłaby
  powtórzeniem. Liczby zostają w podsumowaniu (2). *Obali:* arkusz pod mapą (D1), gdzie jest miejsce tylko na
  liczbę — tam wraca „3 osoby” jak w R2.
- **D5 — bez nazwy tytułem są osoby, a nie „Grób”.** Na liście pięciu kart „Grób” nie da się odróżnić, a
  osoby z notatek tak. Nazwy nie wyliczamy z nazwisk: odmiana w dopełniaczu liczby mnogiej (Wymyślony →
  Wymyślonych) bywa błędna, a błąd na grobie rodziny razi ([[grob]] → D1).
- **D6 — kolejność wpisania**, czyli kolejność z notatek: łatwo sprawdzić, gdzie się skończyło. *Obali:*
  autor szuka grobów po nazwisku — to wyszukiwanie osób (S5).
- **D7 — wstecz wraca na mapę z otwartym arkuszem tego cmentarza**, bo stamtąd się przyszło, a arkusz
  pokazuje nowe liczby — to potwierdzenie, że groby się zapisały.
- **D8 — [[NFR-004-czytelnosc-w-sloncu]] nie rozstrzyga się tutaj** (zmiana względem [[cmentarze]] D12, które
  wskazywało ten ekran). W ISSUE-012 cmentarz to ekran przepisywania w domu, a nie wizyty. Miara zapada przy
  pierwszym ekranie wizyty: mapie cmentarza z pinezkami (D1, [[EPIC-002-wizyta]]). Do tego czasu linie
  pomocnicze mają 5,01:1 (AA).
- **D9 — miniatura nagrobka w karcie** (v3). Autor chciał w arkuszu grobu „miejsca na zdjęcie” (ISSUE-012 →
  *Input from the author* 2), a R2 ma miniaturę nagrobka. Na liście ok. 50 grobów nagrobek rozpoznaje się
  szybciej niż listę imion. Kwadrat 56 dp, a nie okrąg jak przy osobie: nagrobek to przedmiot, okrąg zostaje dla
  ludzi (R3, R4). To decyzja projektowa spoza AC US-005 (AC-1 mówi „przy grobie”), widoczna na stopie #1.
  *Obali:* autor uznaje miniatury na liście za szum — wtedy zdjęcie tylko w [[grob]].
- **D10 — cmentarz to mapa: plan schematyczny + zdjęcie z góry** (v4, SPIKE-004 D8; [[ADR-003-map-source-offline]]).
  Plan to obrys i alejki z OSM w tokenach stylu B, pobrany przy dodaniu cmentarza. Ma plakietkę „Plan offline” (zieleń
  stanu z ikoną) i podpis „© OpenStreetMap”. Przełącznik **Plan / Zdjęcie** w prawym górnym rogu: zdjęcie to
  ortofotomapa GUGiK, tylko z internetem, z plakietką „tylko z internetem” i podpisem „Ortofotomapa: GUGiK”. Bez planu
  (przy dodaniu nie było sieci) jest zaślepka „Plan tego cmentarza pobierze się, gdy będzie internet.” i „Pobierz
  teraz”. Autor: *„Plan i zdjęcie ok, dodaj grób ok”*. **Zastępuje D1.**
- **D11 — na starcie sama mapa; jeden grób po zniczu; lista po przeciągnięciu, bez mapy** (v4, SPIKE-004 D9). Autor:
  *„list grobów nie chce aby była — dopiero po kliknięciu na pineske chciałbym aby ten jeden grób się pojawił”*.
  Znicz → arkusz grobu: miniatura nagrobka, tytuł, adres, „3 osoby” (wraca z R2, D4), **wypełniony „Pokaż grób” ze
  zniczem** (wraca z R2, D3). Arkusz przeciągnięty w górę → **lista grobów na cały ekran**, bez mapy, w kolejności
  wpisania (D6), z kartami jak w elemencie 3. Karta → [[grob]]. Na liście zaznaczony grób ma obrys w akcencie. Mapa
  wraca po przeciągnięciu listy w dół albo „wstecz”. *Obali:* autor przy wizycie chce widzieć listę i mapę naraz.
- **D12 — bez linku do Grobonetu i do wyszukiwarki zarządcy** (v4, SPIKE-004 D10). Autor: *„Nie wykorzystujemy tej
  funkcjonalności, z grobonetu chciałem tak naprawdę tylko te mapki”*. Planów zarządców nie wolno kopiować
  ([[ADR-003-map-source-offline]], W3), więc ich miejsce zajmuje plan schematyczny z kwaterami autora. Zmiana zakresu
  M3 ([[EPIC-002-wizyta]]).
- **D13 — kwatera to nazwana strefa z przerywaną linią** (v4, SPIKE-004 D11): linia w kolorze tekstu, krycie 75%,
  kreska 5/4; nazwa „Kwatera A” 12 sp, półgruba, z obwódką w kolorze tła planu, w dolnym lewym rogu strefy, żeby nie
  wchodziła pod znicze. Kwatera bez strefy żyje tylko w adresach grobów. Autor: *„ok”*.

- **D14 — pasek grobów w stanie mapy, z tym samym „Dodaj grób” co pod listą** (v4.1, SPIKE-004 D12). Groby bez
  pinezki nie mają znicza, a zaraz po przepisaniu notatek pinezki nie ma żaden grób. Bez paska lista byłaby więc
  nieosiągalna. Pasek liczy groby bez pinezki i prowadzi do listy. Autor przyjął pasek i poprosił, żeby „Dodaj grób”
  wyglądał jak pod listą: wypełniony, pełna szerokość. *Obali:* pasek zasłania południe planu na małym telefonie —
  wtedy „Dodaj grób” obok liczby, ale wciąż wypełniony.

- **D15 — „gdzie jestem” na żądanie, nie zawsze** (v4.2, SPIKE-004 D22). Lokalizacja tylko po dotknięciu: w domu nie jest
  potrzebna, a na cmentarzu jest jednym gestem. *Obali:* autor na miejscu zawsze ją włącza — wtedy włączona sama, gdy
  telefon jest w obrysie cmentarza.
- **D16 — pinezka z GPS z możliwością przesunięcia** (v4.2, D22; M6, H3). GPS przy grobie bywa niedokładny; przesunięcie
  dotknięciem planu poprawia go bez nowego trybu. Źródło i dokładność zapisują się z pinezką. *Obali:* pomiar na
  cmentarzu (*Parked*) pokaże dokładność gorszą niż szerokość alejki — wtedy pinezka zaczyna się od kwatery, nie od GPS.

- **D17 — sześć stanów planu zamiast dwóch** (v5, element 2a). Prototyp znał „jest” i „nie pobrany”, a każda przyczyna
  braku ma inną drogę naprzód: brak internetu (poczekać), serwer (spróbować później), brak obrysu w OSM (zdjęcie z góry),
  brak punktu (wskazać). Jedna zaślepka „pobierze się, gdy będzie internet” mówiłaby nieprawdę w trzech z nich ([[style-b]]
  reguła 7: brak opisany faktem i tym, kiedy się uzupełni). Tekst (b) zostaje z prototypu (autor: *„Plan i zdjęcie ok”*).
  *Obali:* na cmentarzach autora zdarza się tylko (b) — wtedy (c) i (d) zostają w kodzie bez dalszego projektu.
- **D18 — pobieranie rusza samo, „Pobierz teraz” to skrót.** Plan zaczyna się pobierać przy zapisie cmentarza z punktem
  (z bazy albo ręcznie), przy zmianie punktu w „Popraw cmentarz” i wtedy, gdy telefon odzyska internet. Tekst (b) to
  obietnica, więc mechanizm musi ją spełnić: wybiera go `planning`, np. zadanie w tle z warunkiem sieci, jak kopia. Zmiana
  punktu pobiera plan od nowa, bo obrys zależy od punktu. *Obali:* zadanie w tle kosztuje więcej niż reszta pozycji — wtedy
  (b) brzmi „Plan tego cmentarza pobierze się, gdy otworzysz go z internetem.”
- **D19 — brak obrysu w OSM: zaślepka i zdjęcie z góry, a nie kwadrat wokół punktu.** Kwadrat ±300 m (zapas z SPIKE-001)
  pokazałby drogi i domy wokół cmentarza: plan, który nie jest planem. Cmentarze z bazy ([[ISSUE-015-add-cemetery-from-database]])
  pochodzą z OSM, więc zwykle mają obrys, a ten stan dotyczy głównie cmentarzy dodanych ręcznie. *Obali:* autor ma taki
  cmentarz i bez zasięgu nie widzi na nim nic — wtedy same znicze na tle w kolorze powierzchni, z podziałką.
- **D20 — pobieranie niewidoczne na mapie Polski** ([[cmentarze]] D34). Po „Zapisz” mapa Polski wygląda jak dotąd, a plan
  widać w cmentarzu, gdzie jest potrzebny. Postęp w arkuszu cmentarza byłby szumem na ekranie, na którym wybiera się, dokąd
  jechać. *Obali:* autor dodaje cmentarz w drodze, bez zasięgu, i chce wiedzieć, czy plan już jest — wtedy w arkuszu linia
  „Plan offline” z ikoną.
- **D21 — uchwyt arkusza działa dotknięciem.** W prototypie z B do C prowadziło tylko przeciągnięcie. WCAG 2.2 SC 2.5.7
  Dragging Movements (AA): *„All functionality that uses a dragging movement for operation can be achieved by a single
  pointer without dragging, unless dragging is essential”* ([Understanding 2.5.7](https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements.html)).
  Uchwyt z celem 48 dp: w B prowadzi do C, w C wraca. Pasek w A działał dotknięciem już wcześniej (element 6).
- **D22 — plakietki przy dużym tekście.** Przełącznik zostaje w prawym górnym rogu, bo tam jest w R2 i w prototypie. „Plan
  offline” schodzi pod niego, gdy oba nie mieszczą się w rzędzie. Plakietki to kontrolki, a nie podpisy przypięte do punktu,
  więc nie obowiązuje ich granica 1,3× ([[style-b]] reguła 13).
- **D23 — z widoku osoby, gdy mapa już jest.** Grób z pinezką → stan B z tym grobem. Grób bez pinezki → stan C z
  zaznaczonym grobem, **bez komunikatu o pinezce aż do [[US-008-pinezka-na-miejscu]]**. [[osoba]] D17 trwa, bo mapa jest,
  ale pinezki nie da się jeszcze postawić, a komunikat mówiłby o działaniu, którego nie ma.
- **D24 — kwatery w osobnym trybie, z widocznym wejściem w stanie A** (v6). Zaznacza się je rzadko i w domu, a stan A służy też
  wizycie. Tryb zabiera dolny pasek i wyłącza dotyk zniczy, więc dotknięcie strefy nie konkuruje z dotknięciem znicza.
  Wejście jest pigułką na planie, a nie wierszem pod ✎: działanie, którego nie widać, dla autora nie istnieje (prototyp SPIKE-004).
  Pigułki nie ma, gdy nie ma na czym rysować (zaślepka 2a, „Zdjęcie” bez sieci). *Obali:* pigułka przeszkadza przy wizycie —
  wtedy „Kwatery” jako wiersz w oknie „Popraw cmentarz”.
- **D25 — nazwa przed rysowaniem** (v6), jak „Nowy cmentarz” → wskazanie na mapie ([[cmentarze]] 15 → 16). Instrukcja i podpis
  rysowanej strefy mówią „Kwatera D”, a podwójna nazwa zatrzymuje autora, zanim narysuje drugi raz tę samą kwaterę. Aplikacje
  terenowe robią odwrotnie (najpierw kształt, potem formularz — QField), bo tam pól jest wiele; tu jest jedna nazwa. *Obali:* na
  prototypie autor chce najpierw rysować.
- **D26 — poprawa strefy to narysowanie jej od nowa na starej, szarej strefie** (v6). Kwatera ma 4–6 rogów, więc przerysowanie to
  4–6 ruchów ze wzorem pod spodem. Edytor rogów (przesuń, usuń, wstaw — *Vertex Tool* w QField) to osobny tryb do zbudowania i do
  nauczenia. *Obali:* autor wiele razy poprawia jeden róg — wtedy edytor rogów (przy K3 to prawie ten sam tryb).
- **D27 — „Usuń z planu” zdejmuje tylko strefę** (v6). Adres zarządcy jest prawdą, a strefa pomocą ([[data-model]] → Grave), więc
  usunięcie strefy nie zmienia adresu żadnego grobu. Kwatera bez grobów i bez strefy znika z listy, a z grobami zostaje jako „bez
  strefy”. *Obali:* autor chce usunąć literówkę z adresów wielu grobów naraz — to zmiana nazwy (19b) przy W-a.
- **D28 — strefa bez wypełnienia; kwatera wybrana w akcencie** (v6). Wypełnienie byłoby dużą plamą (akcent nigdy jako plama — [[style-b]]
  *Token roles*), a szare wypełnienie zlewałoby się z alejkami. Wybór niesie akcent, grubość 2,5 dp i nazwa w arkuszu 17b, bo akcent
  i linia kwatery różnią się tylko o 1,31:1 (SC 1.4.1).
- **D29 — strefy nie reagują na dotyk w stanach A i B** (v6). Znicze leżą w strefach. Gdyby dotknięcie strefy coś otwierało, każde
  chybione dotknięcie znicza otwierałoby kwaterę. Kwaterami zarządza się w trybie E. *Obali:* autor na wizycie chce dotknąć kwatery,
  żeby zobaczyć jej groby — kandydat dla [[US-008-pinezka-na-miejscu]] (lista grobów kwatery, „Pokaż kwaterę” przy grobie bez pinezki).
- **D30 — prior art: jak aplikacje mapowe rysują obszar na telefonie** (v6, dla *Open* K1–K3). Kanonem są aplikacje do zbierania
  danych w terenie:
  - **QField:** celownik na środku i „+”: *„Tap the plus button (+) at the bottom right to place the first vertex”*, „−” usuwa
    ostatni róg, a wielokąt wymaga *„a minimum of 3 vertices”*. **Dotknięcie stawiające róg jest opcją, domyślnie wyłączoną:**
    *„Allow finger tap on canvas to add vertices”* ([QField — Digitize](https://docs.qfield.org/how-to/data-collection/digitize/));
  - **Google Earth na Androidzie:** *„move the map and tap Add point”*, „Undo”, *„connect to your first point and tap Close Shape”*
    ([Google Earth Help — Measure distances and areas](https://support.google.com/earth/answer/9010337));
  - **Mergin Maps** i **ArcGIS Earth:** też celownik
    ([Mergin Maps — mobile features](https://merginmaps.com/docs/field/mobile-features/),
    [ArcGIS Earth mobile — Create drawings](https://doc.arcgis.com/en/arcgis-earth/mobile/create-drawings.htm)).

  Dlaczego tak: palec zasłania miejsce, które wskazuje, a dotknięcie, które stawia róg, konkuruje z gestami mapy (przesunięcie,
  podwójne dotknięcie). W samej aplikacji obowiązuje jednak odwrotny wzorzec: wskazanie cmentarza ([[cmentarze]] 16) i pinezka (12)
  stawia się dotknięciem.
- **D31 — „gdzie jestem” ma trzy stany i jedzie planem do kropki** (v7, 10, 10a). Wyłączony → włącza i centruje; plan na kropce →
  wyłącza; plan odsunięty → wraca do kropki. Jedno miejsce na trzy potrzeby: włączyć, wrócić, wyłączyć. Kropka poza obrysem nie
  przesuwa planu, bo przesuwanie jest ograniczone do obrysu (2), a w domu plan zostałby pusty — plakietka mówi „poza cmentarzem”
  i jak daleko. Decyzja projektowa, bo SPIKE-004 pokazał tylko włącz/wyłącz. *Obali:* przy bramie autor chce widzieć cały
  cmentarz z kropką — wtedy pierwsze dotknięcie centruje bez przybliżania.
- **D32 — tryb D sam włącza lokalizację; bez kropki pinezka zaczyna w strefie kwatery grobu** (v7, 12). „Postaw pinezkę” przy
  grobie znaczy „tu jestem”, więc wejście do D to żądanie lokalizacji z D15, a nie wyjątek od niego. Pierwsze wejście pyta o zgodę.
  Bez kropki (w domu, bez zgody, bez sygnału) pinezka startuje w środku strefy kwatery z adresu grobu — tak wygląda kierunek
  autora ([[EPIC-002-wizyta]] → *Open questions*: adres → kwatera → pinezka). Bez strefy startuje w środku kadru. *Obali:* w domu
  pytanie o lokalizację przy stawianiu pinezki na zdjęciu z góry przeszkadza — wtedy lokalizacja w D dopiero po ◎.
- **D33 — źródło pinezki to to, z czego wzięła się pozycja, a nie to, gdzie był autor** (v7, 14, 12a; pytania (a) i (b) z
  [[ISSUE-029-pin-on-site-gps]]). Pinezka nieruszona w kropce to **GPS** z dokładnością. Pinezka przesunięta ręką — także o metr,
  także na cmentarzu — to **„postawiona na planie”** albo **„na zdjęciu z góry”** (warstwa, na której stała), **bez dokładności**,
  bo to miejsce wybrane przez autora, a nie pomiar. Kanon: słowniczek → *pinezka*: „postawiona przez autora na planie albo na
  ortofotomapie / GPS na miejscu”, czyli trzy źródła. „Zaznaczona w domu” z v4.2 odpada, bo ręczna poprawka przy grobie też jest
  ręczna. Data — przy każdym źródle. **Dla danych** (`planning`): enum `PositionSource` ma dziś `satellite` i `gps`, brakuje
  wartości „plan”, a daty pinezki nie ma w schemacie. *Obali:* autor chce odróżnić poprawkę przy grobie od poprawki w domu —
  wtedy dopisek „na miejscu”, gdy kropka była w obrysie.
- **D34 — gdzie się dotyka w trybie D: P1 albo P2 — decyzja autora na stopie #1** (v7, 12; retro: pokazać „gdzie się dotyka”, a nie
  tylko co widać — ISSUE-024). **Rekomendacja `ui`: P2** — ten sam ruch co rysowanie kwatery na tym samym planie (K1, wybór
  autora 2026-10-12): palec nie zasłania miejsca, idąc z telefonem nie przestawi się pinezki przypadkiem, a plan idący za kropką
  znamy z nawigacji. **P1** (prototyp SPIKE-004 i wskazanie cmentarza, [[cmentarze]] 16) daje jedno dotknięcie na poprawkę, ale
  opuszka przy z19 zasłania ok. 8–9 m planu, czyli tyle, ile sama poprawka GPS. *Obali P2:* na prototypie autor szuka pinezki, którą
  da się złapać palcem — wtedy P1.
- **D35 — poprawa zaczyna od zapisanej pinezki** (v7, 11, 12a). Zapisana pinezka mogła być postawiona starannie, a kropka ±15 m by
  ją zgubiła. ◎ przenosi ją do kropki jednym dotknięciem. „Zapisz pinezkę” nieaktywny, dopóki nic się nie zmieni, jak „Gotowe” w F
  przed trzecim rogiem. *Obali:* autor przy każdej poprawce najpierw dotyka ◎ — wtedy start w kropce.
- **D36 — tryb D jak tryb F; po zapisie mapa z grobem** (v7, 12; [[style-b]] reguła 12). Pasek z ✕, bez dolnego paska, warstwa z
  poprzedniego stanu bez przełącznika — ten sam wzorzec co F, więc drugi tryb na planie nie uczy nowego układu. „Zapisz pinezkę” →
  stan B z nowym zniczem także po wejściu z [[grob]] (D22 z SPIKE-004), bo nowy znicz na mapie jest potwierdzeniem zapisu. Wyjście
  bez zapisu nie pyta, bo jedna pinezka to mało pracy do stracenia (F pyta o rogi, 19d). *Obali:* autor po zapisie z grobu chce
  wrócić do grobu, np. żeby od razu zrobić zdjęcie nagrobka — wtedy powrót tam, skąd przyszedł.
- **D37 — słaby sygnał: próg tymczasowy 15 m** (v7, 12a; decyzja autora 2026-10-12 w `/pm`: budowa przed pomiarem, żeby jedna
  wizyta dała pomiar i sprawdzenie w terenie). Komunikat jest faktem w kolorze tekstu, a zapis zostaje możliwy, bo słaby sygnał
  przy grobie to wciąż lepiej niż brak pinezki, a dokładność idzie do źródła. Próg to jedna stała. *Obali:* pomiar przy 3 grobach
  (`CURRENT_STATE.md` → *Parked*) — próg ustawia się na zmierzoną wartość, a jeśli kropka nie trafia nawet w kwaterę (D16 →
  *Obali*), pinezka zaczyna od kwatery, nie od GPS.
- **D38 — „Dodaj grób” otwiera okno grobu, nie formularz osoby** (v8 — przyjęte na stopie #1 (autor: „Tak”, 2026-10-18), [[ISSUE-047-grave-first-then-people]]; autor
  2026-10-18: *„chciałbym dodać po prostu grób, a następnie osobę (lub osoby, które tam leżą)”*). Grób jest rekordem tego ekranu (*Tempo*), a
  osoby mają już wejście z widoku grobu — razem z wyborem osoby, która jest w aplikacji bez grobu ([[grob]] D22). Okno to „Popraw grób” w trybie
  nowego grobu, nie nowy ekran: te same pola, ta sama walidacja, jeden wzorzec do nauczenia ([[grob]] D2, D13). Przy grobie na cmentarzu
  autor może najpierw zrobić zdjęcie nagrobka i postawić pinezkę, a osoby dodać później. Koszt: 3 dotknięcia więcej na grób z notatek (ok. 150
  przy ok. 50 grobach). Pusty grób, z którego autor wyszedł, zostaje na liście — usuwania grobów, osób i pochówków nie ma ([[wpis-osoby]]
  *Decisions* → „Bez usuwania osoby”; brief G7/C5). D36 obowiązuje dalej: widok nowego grobu leży nad tym ekranem tak jak dotąd po formularzu.
  *Obali:* (1) przy przepisywaniu notatek trzy dotknięcia przeszkadzają — wtedy po „Zapisz” w oknie od razu wybór osoby ([[grob]] 8–12) nad pustym
  grobem; (2) puste groby z pomyłek zaśmiecają listę — wtedy „Usuń grób” tylko dla grobu bez osób, osobną pozycją.

## Open
- ✅ **Rozstrzygnięte 2026-10-12 na stopie #1 [[ISSUE-029-pin-on-site-gps]] (autor: „ok”): P2** — celownik, plan pod zniczem.
  Element 12 obowiązuje w wariancie P2, a teksty karty i 12a — w wariancie P2. Decyzje D31–D33, D35–D37 potwierdzone. Pierwotne
  pytanie: **gdzie się dotyka w trybie D** (D34). Klikalny prototyp `issue-029-pinezka.html`, panel 2:
  - **P1 — dotknięcie przesuwa znicz.** Koszt: palec zasłania miejsce (ok. 8–9 m planu przy z19); jedno dotknięcie na poprawkę.
    Tracimy spójność z rysowaniem kwatery (K1);
  - **P2 — celownik, plan pod zniczem** (rekomendacja). Koszt: przy dużej poprawce przesuwanie zamiast dotknięcia (albo dotknięcie,
    które przesuwa miejsce pod znicz). *Obali:* autor na prototypie szuka pinezki do złapania palcem.
- ✅ **Rozstrzygnięte 2026-10-12 na stopie #1 [[ISSUE-028-cemetery-sectors]] (autor: „tak”):** **K1** (celownik i „Dodaj róg”),
  **W-a** (odnośnik — [[ADR-016-sector-record-and-grave-link]]), **adres grobu w ISSUE-028** ([[grob]] v6). Element 18 obowiązuje w
  wariancie K1, a 19b — w wariancie W-a. Pierwotne opisy pytań:
- **K1, K2 czy K3: gdzie się dotyka przy zaznaczaniu strefy** (v6, element 18; klikalny prototyp `issue-028-kwatery.html`,
  panel 3):
  - **K1 — celownik i „Dodaj róg”** (kanon, D30): plan zachowuje się jak wszędzie (przesuwanie, dwa palce, podwójne dotknięcie),
    a róg nigdy nie stawia się przypadkiem; dotknięcie planu przesuwa miejsce pod celownik, więc nic nie wymaga przeciągania.
    Koszt: dwa ruchy na róg i nowe pojęcie w aplikacji (celownik);
  - **K2 — dotknięcie stawia róg**: jak wskazanie cmentarza i pinezka w tej aplikacji, najmniej ruchów. Koszt: palec zasłania róg,
    przypadkowe dotknięcie stawia róg („Cofnij”), a podwójne dotknięcie nie może przybliżać, więc dochodzą przyciski „+ −”;
  - **K3 — gotowy prostokąt do dopasowania**: większość kwater to prostokąty między alejkami. Koszt: małe uchwyty do przeciągania na
    telefonie, droga bez przeciągania („dotknij rogu, potem miejsca”) jest mniej oczywista.

  **Rekomendacja `ui`: K1.** Kanon wybiera celownik z powodów, które obowiązują także w domu: palec i gesty mapy. Plan nie dostaje
  nowych przycisków. *Co obali:* na prototypie K1 wyda się autorowi wolny albo obcy, a K2 trafi w róg za pierwszym razem — wtedy K2
  z „+ −”.
- **jak kwatera łączy się z adresem grobu** (v6; prototyp, panele 2 i 4; model należy do `planning` — ADR, „model kwatery”
  z [[ADR-003-map-source-offline]] → *Follow-ups*). Widoczny skutek:
  - **W-a — odnośnik:** w adresie grobu wybierasz kwaterę z kwater cmentarza albo wpisujesz nową, a „b” trafia w „B”. Zmiana nazwy
    kwatery poprawia adresy wszystkich jej grobów. Kwatera wpisana w adresie bez strefy jest na liście 17a jako „bez strefy”;
  - **W-b — tekst:** każdy adres jest osobnym tekstem. Zmiana nazwy strefy nie zmienia adresów, więc groby z „Kwatera B” przestają
    pasować do strefy „B1”, a „b” i „B” to dwie kwatery na liście.

  **Rekomendacja `ui`: W-a.** Dziś żaden grób w aplikacji autora nie ma adresu, bo żaden ekran go nie zapisuje (niżej), więc W-a nie
  przenosi żadnych prawdziwych danych. Po instalacji MVP przejście z W-b na W-a byłoby już migracją adresów rodziny. *Co obali:* autor
  chce wpisywać w adresie dowolny opis, np. „B, lewa strona od kaplicy” — wtedy W-b.
- **adresu grobu nie da się wpisać — luka poza tą specyfikacją** (znaleziona przy v6). Kolumny `sector`, `row`, `plot` są w
  schemacie od v1, ale żaden ekran ich nie zapisuje — tylko wymyślone dane w buildzie debug. [[grob]] mówi „Uzupełnisz przy wizycie.”,
  a [[US-008-pinezka-na-miejscu]] adresu nie obejmuje. Kierunek autora ([[EPIC-002-wizyta]] → *Open questions*, krok 1: adres z
  wyszukiwarki zarządcy) nie ma więc ekranu, choć M1 wymienia adres kwatery. Bez adresu kwatera na planie nie łączy się z żadnym
  grobem. **Propozycja: [[grob]] v6** — „Popraw grób” z polami Kwatera, Rząd i Miejsce oraz „Wpisz adres” pod brakiem adresu.
  **Rekomendacja `ui`:** w ISSUE-028, bo W-a/W-b ma sens tylko razem z polem adresu, a koszt to jedno okno. Inaczej — osobna pozycja
  przed instalacją MVP. To zmiana zakresu, więc decyduje autor.
- ✅ **Rozstrzygnięte 2026-10-12 — W2** (autor: „tak” na stopie #1 [[ISSUE-027-cemetery-map-plan-photo-states]], D1). Pierwotny
  opis pytania:
- **Miara [[NFR-004-czytelnosc-w-sloncu]] na tym ekranie.** To pierwszy ekran wizyty (D8 przesunęło miarę tutaj),
  a [[style-b]] trzyma 7:1 (SC 1.4.6, AAA) jako kandydata „do decyzji przy pierwszym ekranie wizyty”. Dwa warianty na
  makiecie (ramki B1 i B2):
  - **W1 — jak dziś:** adres, „3 osoby”, linia grobów bez pinezki i druga linia zaślepek w tekście pomocniczym (5,01:1 na
    powierzchni, AA);
  - **W2 — 7:1 dla tekstu potrzebnego na cmentarzu:** te same linie w kolorze tekstu (10,02:1 na powierzchni). W tekście
    pomocniczym zostaje tylko to, czego nie czyta się przy grobie: podpisy źródeł („© OpenStreetMap”, „Ortofotomapa:
    GUGiK”). Hierarchię niesie rozmiar i waga, a nie kolor.

  **Rekomendacja `ui`: W2** i test w słońcu na telefonie przy instalacji MVP (`DEFINITION_OF_DONE.md` → wyjątki).
  - **Koszt:** kilka linii zmienia rolę koloru, bez nowych tokenów.
  - **Co tracimy:** część spokojnej hierarchii z R2, w której linie pomocnicze są szare.
  - **Co obali:** test w słońcu pokaże, że W2 nie wystarcza → wariant wysokokontrastowy (NFR-004 → *Notes*).

  Decyzja autora trafi do NFR-004 (miara), [[style-b]] (*Thresholds*: z kandydata miara obowiązująca na ekranach wizyty) i
  [[grob]] (*Known gaps*: te same linie przy M4).
- ⚠️ OPEN — **dokładność GPS przy grobie** (ile metrów, czy kropka trafia w kwaterę) — mierzy wizyta na cmentarzu
  (`CURRENT_STATE.md` → *Parked*, SPIKE-001 D5). Od wyniku zależy próg „słaby sygnał” (element 12a) — [[US-008-pinezka-na-miejscu]].
  **Nie blokuje budowy (v7):** do pomiaru próg tymczasowy 15 m (D37, decyzja autora 2026-10-12).
- **Nie do `ui` — czy plan wchodzi do kopii** (`planning`, kandydat na ADR). Widoczny skutek: jeśli plan nie wchodzi do
  kopii, po odtworzeniu na nowym telefonie każdy cmentarz pokazuje (a) albo (b), aż telefon dostanie internet.
- **Znicze sąsiednich grobów nachodzą na siebie** (przegląd ISSUE-027, odstępstwo 4): przy z19 na 52° N 1 dp to ok. 0,18 m, więc
  cel 48 dp ma ok. 9 m, a znicz ok. 5 m — groby obok siebie zasłonią się nawet przy największym przybliżeniu, a łączenie w znicz
  z liczbą (jak na mapie Polski) ich nie rozdzieli. Kandydat dla [[US-008-pinezka-na-miejscu]]: znicz z liczbą otwiera arkusz z
  listą tych grobów. Do tego czasu wybór przez listę (C). **v7:** kandydat poza [[ISSUE-029-pin-on-site-gps]] →
  [[ISSUE-030-sector-on-a-visit]] (`draft`, razem z „Pokaż kwaterę” i listą grobów kwatery z D29).
- **Główne i boczne alejki według rodzaju z OSM** (przegląd ISSUE-027, pkt 9): na publicznym cmentarzu testowym prawie wszystkie
  alejki mają w OSM `footway`, więc rysują się jako boczne (2 dp), także te, które są główne na miejscu. Kandydat: grubość z
  `width`/`surface` albo jedna grubość dla wszystkich — decyzja, gdy autor zobaczy plany swoich cmentarzy.
- **Znana luka — przesuwanie przybliżonego planu tylko przeciągnięciem** (SC 2.5.7). Wszystkie znicze są w kadrze startowym,
  a lista (C) prowadzi do każdego grobu jednym dotknięciem, więc żadne działanie nie wymaga przeciągania. Kandydat:
  przycisk „cały cmentarz”, gdy autor zgubi się na przybliżonym planie.
