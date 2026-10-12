---
screen: "Cmentarz — groby na cmentarzu"
items: ["[[ISSUE-012-transcribe-grave-screen]]", "[[ISSUE-016-photos-grave-and-person]]", "[[SPIKE-004-mvp-flow-prototype]]", "[[ISSUE-024-person-view]]", "[[ISSUE-027-cemetery-map-plan-photo-states]]"]
us: "[[US-002-przepisanie-grobu]] · [[US-005-zdjecia]] · [[US-007-mapa-cmentarza]]"
journey-step: "n/a — M1 (warunek kroku 1 UJ-001); docelowo mapa cmentarza z arkuszem grobu (R2, krok 2 UJ-001, M3)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-cmentarz-grob-osoba.html (ramki 1–2, 8, ISSUE-012) · makieta-zdjecia.html (ramka 9, ISSUE-016) · 2026-10-08: grobing-prototyp.html (SPIKE-004, panel 2) · 2026-10-12: issue-027-mapa-cmentarza.html (stany planu, warianty NFR-004)"
updated: 2026-10-12
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
    → C. „Dodaj grób” → [[wpis-osoby]] w trybie „nowy grób”: grób powstaje z pierwszą osobą, przy jej zapisie;
  - **B — jeden grób:** arkusz grobu (7), a plan przesuwa się płynnie nad arkusz. „Pokaż grób” → [[grob]]. Arkusz
    przeciągnięty w górę albo **dotknięty uchwyt** → C (D21). Dotknięcie planu albo wstecz → A;
  - **C — lista:** wszystkie groby na cały ekran, bez planu (8–9). Karta → [[grob]]. Lista przeciągnięta w dół, **dotknięty
    uchwyt** albo wstecz → stan, z którego przyszła (B albo A).
- **Z [[osoba]] → „Pochówek”** (v5, D23): grób z pinezką → stan B z tym grobem; grób bez pinezki → stan C z zaznaczonym
  grobem, **bez komunikatu o pinezce aż do [[US-008-pinezka-na-miejscu]]** ([[osoba]] D17 trwa; komunikat z [[osoba]] D9
  wraca z US-008). Wstecz → widok osoby.
- **Wstecz w stanie A → [[cmentarze]]** z tym samym cmentarzem wybranym i jego arkuszem (D7). Z [[grob]] wstecz →
  stan, w którym autor ekran opuścił.
- **✎ w pasku → okno „Popraw cmentarz”** ([[cmentarze]] 15), według [[style-b]] reguły 15. Zaznaczanie kwater i
  stawianie pinezek to osobne działania: panel 7 (wizyta) i pierwsza US [[EPIC-002-wizyta]].
- **Pasek dolny** Mapa · Osoby · Drzewo jest widoczny we wszystkich stanach, a aktywna jest Mapa ([[style-b]] reguła
  12, SPIKE-004 D2).

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** wstecz + **nazwa cmentarza** (18 sp, półgruby, do 2 linii), pod nią miejscowość (13 sp, tekst pomocniczy; bez miejscowości brak linii); po prawej ✎ (`edit_outlined`, akcent, `tooltip` „Popraw cmentarz”) | pasek | wstecz (*Navigation*); ✎ → okno | — | — | R2 (nagłówek) · [[style-b]] reguła 15 |
| 2 | **Plan schematyczny** na całą szerokość pod paskiem, także pod arkuszami: obrys cmentarza i alejki z OSM, pobrane przy dodaniu cmentarza ([[style-b]] reguła 13: teren — powierzchnia z obrysem, alejki — obrys 4 i 2 dp). Wyśrodkowany w wolnym miejscu między plakietkami (3) a paskiem grobów (6); w stanie B przesuwa się płynnie nad arkusz (jak [[cmentarze]] D30). Podpis „© OpenStreetMap” (11 sp, tekst pomocniczy) pod plakietką. **Kadr (v5):** na starcie cały obrys z marginesem 16 dp w wolnym miejscu; to też najmniejsze przybliżenie, a największe to z19 (granica zdjęcia z góry, [[ADR-003-map-source-offline]] pkt 2). Przesuwanie ograniczone do obrysu z marginesem, więc cmentarz nigdy nie znika z ekranu. Teren poza obrysem w kolorze tła. **Dla czytnika** plan to jeden węzeł „Plan cmentarza” (alejek nie czyta), a każdy znicz (5) to osobny przycisk. **Bez planu → 2a** | mapa | szczypanie, przeciąganie, podwójne dotknięcie; bez obrotu | cały cmentarz, północ u góry | — | [[ADR-003-map-source-offline]] pkt 1 · D10 |
| 2a | **Zaślepka planu (v5, D17)** w miejscu planu, wyśrodkowana w wolnym miejscu. Ikona 32 dp w kolorze tekstu pomocniczego, pod nią fakt i droga naprzód (oba 14 sp, kolor tekstu — W2, *Open*), niżej przycisk tekstowy w akcencie, cel ≥ 48 dp. Pięć wariantów: **(a) pobieranie** — wskaźnik postępu (kołowy, akcent) zamiast ikony, „Pobieram plan cmentarza…”, bez przycisku; **(b) bez internetu** — `cloud_download`, „Plan tego cmentarza pobierze się, gdy będzie internet.” · „Groby są na liście — pasek na dole.” · **„Pobierz teraz”**; **(c) serwer nie odpowiada** (po ponowieniach) — `cloud_off`, „Nie udało się pobrać planu — serwer map nie odpowiada.” · „Spróbuję znowu później. Groby są na liście.” · **„Pobierz teraz”**; **(d) brak obrysu w OSM** — `not_listed_location`, „W OpenStreetMap nie ma planu tego cmentarza.” · „Z internetem zobaczysz go na zdjęciu z góry.” · **„Pokaż zdjęcie z góry”** (tylko z siecią; bez sieci bez przycisku); **(e) bez punktu** — `location_off_outlined`, „Plan pobierze się, gdy wskażesz cmentarz na mapie.” · **„Wskaż na mapie”**. Plakietka „Plan offline” i podpis „© OpenStreetMap” znikają w każdym wariancie; przełącznik Plan · Zdjęcie (3) zostaje w (a)–(d), a w (e) znika, bo zdjęcie nie ma środka | stan planu | „Pobierz teraz” → (a); bez sieci zamiast tego pasek komunikatu „Bez internetu. Plan pobierze się, gdy będzie zasięg.” (zaślepka zostaje); „Pokaż zdjęcie z góry” → warstwa „Zdjęcie”, środek w punkcie cmentarza, z17; „Wskaż na mapie” → tryb wskazania ([[cmentarze]] 16) dla tego cmentarza; po „Zapisz” powrót tutaj w (a) | według stanu pobierania | — | [[ADR-003-map-source-offline]] pkt 1 („ponawianie i zaślepka są warunkiem”) · US-007 AC-5 · [[style-b]] reguła 7 · D17–D19 |
| 3 | **Plakietki na planie**, na powierzchni, wys. 32 dp, margines 12 dp. Z lewej **„Plan offline”** z ikoną `offline_pin` w zieleni stanu (propozycja `#8CC084`, [[style-b]] *State colours*). Z prawej przełącznik segmentowy **Plan · Zdjęcie** (ikony `map_outlined`, `satellite_alt`; aktywny segment w akcencie). „Zdjęcie” to ortofotomapa GUGiK, tylko online, nic nie zapisuje w telefonie; plakietka zmienia się na „tylko z internetem” z ikoną `wifi` (tekst pomocniczy), a podpis na „Ortofotomapa: GUGiK”. Kafelki zdjęcia ładują się na tle w kolorze powierzchni, bez wskaźnika; nic nie trafia do pamięci telefonu poza pamięcią podręczną w RAM (pkt 2). Wygląd „Zdjęcia” bez sieci → 13. **Duży tekst (v5, D22):** plakietki to kontrolki, więc rosną w pełni; gdy z przełącznikiem nie mieszczą się w jednym rzędzie, „Plan offline” schodzi pod przełącznik, z lewej. Przełącznik dla czytnika: dwa przyciski ze stanem „wybrany” | plakietka + przełącznik | segment → warstwa | Plan | — | [[ADR-003-map-source-offline]] pkt 2 · D10 |
| 4 | **Kwatery autora:** przerywana linia (tekst, krycie 75%, kreska 5/4) i nazwa „Kwatera A” (12 sp, półgruba, obwódka w kolorze tła planu) w dolnym lewym rogu strefy. Kwatera bez strefy jest tylko w adresach grobów. **Zaznaczanie i rysowanie → [[ISSUE-028-cemetery-sectors]]**; w ISSUE-027 plan jest bez kwater | strefy | — | — | — | [[ADR-003-map-source-offline]] pkt 3 · D13 |
| 5 | **Znicze grobów z pinezką:** znicz-pinezka 28 × 35 dp, cel dotyku ≥ 48 dp; wybrany 38 × 47 dp z poświatą ([[style-b]] reguła 13). Grób bez pinezki nie ma znicza | znaczniki | dotknięcie → stan B | — | — | R2 · D11 |
| 6 | **Pasek grobów** (stan A): dolny arkusz na powierzchni, promień 16 dp u góry, uchwyt. „6 grobów · 14 osób” (14 sp, tekst), pod spodem „2 groby bez pinezki — na liście” albo „wszystkie groby mają pinezki” (13 sp, kolor tekstu — W2). Pod nimi **wypełniony „Dodaj grób”** z ikoną `add`, ≥ 52 dp, na pełną szerokość — **ten sam przycisk co pod listą (9)** | dolny arkusz + przycisk główny | dotknięcie albo przeciągnięcie w górę → stan C; „Dodaj grób” → [[wpis-osoby]] „nowy grób” | — | — | **decyzja autora** (SPIKE-004 D12) · D14 |
| 7 | **Arkusz grobu** (stan B), na powierzchni, z uchwytem: miniatura nagrobka 72 dp (promień 12 dp; bez zdjęcia brak miniatury), tytuł (16 sp, półgruby — jak 8 (a)), adres i ikona `group_outlined` + „3 osoby” (14 sp, kolor tekstu — W2, *Open*), **wypełniony „Pokaż grób” ze zniczem** (kolor tła na akcencie) | dolny arkusz + przycisk główny | „Pokaż grób” → [[grob]]; przeciągnięcie w górę albo dotknięcie uchwytu (cel 48 dp, czytnik: „Pokaż listę grobów”) → stan C | — | — | R2 (arkusz grobu) · D11 · D21 |
| 8 | **Lista grobów** (stan C), pod paskiem (1), na powierzchni z uchwytem: podsumowanie „6 grobów · 14 osób” (14 sp, tekst pomocniczy, margines 16 dp) i karty (promień 16 dp, odstęp 8 dp, margines 16 dp) w kolejności wpisania. Karta, od góry: **(a) tytuł** — nazwa grobu (16 sp, półgruby, kolor tekstu, do 2 linii); bez nazwy tytułem są **osoby w grobie**: imiona i nazwiska po przecinku, ten sam krój, do 2 linii, potem „i jeszcze 2”. **(b) osoby** — tylko gdy tytułem jest nazwa: imiona i nazwiska po przecinku (14 sp, tekst pomocniczy, do 2 linii, potem „i jeszcze 2”). **(c) adres** (14 sp, kolor tekstu — W2, ten sam adres co w arkuszu 7): „Kwatera B · Rząd 4 · Miejsce 12”, a bez pinezki dopisane „· bez pinezki”; bez adresu „Bez adresu kwatery · bez pinezki”. Chevron „›” po prawej. Karta ≥ 64 dp. **(d) miniatura** — tylko gdy grób ma zdjęcie: zdjęcie nagrobka ([[grob]] D9), kwadrat **56 dp** z zaokrągleniem 8 dp, przycięty ze środka, z lewej, wyśrodkowany w pionie, odstęp 12 dp do tekstu; poza czytnikiem. Bez zdjęcia bez miniatury i bez wcięcia ([[grob]] D11). **Grób wybrany w stanie B** ma obrys 1,5 dp w akcencie | lista kart | karta → [[grob]]; przeciągnięcie w dół albo dotknięcie uchwytu (czytnik: „Pokaż mapę”) → stan B albo A | kolejność wpisania | — | AC-1 · AC-5 · R2 · decyzja autora (nazwa grobu) · US-005 AC-1 · D6, D9, D11 |
| 9 | **„Dodaj grób”** pod listą — wypełniony, z ikoną `add`, ≥ 52 dp, przypięty na dole; lista przewija się nad nim, a ostatnia karta ma pod sobą odstęp na wysokość przycisku | przycisk główny | → [[wpis-osoby]] „nowy grób” | — | — | *What to build* 2 · D14 |
| 10 | **„Gdzie jestem”** — okrągły przycisk 48 dp na powierzchni (`my_location`), z prawej nad paskiem grobów albo arkuszem grobu (R2). Włączony: ikona w kolorze kropki „tu jesteś”, na planie **niebieska kropka** 16 dp z obwódką w kolorze tła i **kołem dokładności** (kolor kropki, krycie 18%), obok plakietka „tu jesteś · ±4 m” (12 sp) | przycisk-ikona | włącz / wyłącz lokalizację; pierwsze użycie → systemowe pytanie o uprawnienie lokalizacji | wyłączony | brak uprawnienia → „Bez zgody na lokalizację pinezki postawisz tylko ręcznie.” | R2 · [[style-b]] *State colours* · D15 |
| 11 | **„Popraw pinezkę”** (stan B, grób z pinezką) — pigułka na powierzchni z `edit_location_alt` w akcencie, z lewej nad arkuszem grobu (R2) | przycisk | → stan D dla tego grobu | — | — | R2 · M6 · D15 |
| 12 | **Stan D — stawianie pinezki:** zamiast plakietek u góry karta „**Stań przy grobie.** Pinezka stanie w niebieskiej kropce. Możesz ją przesunąć — dotknij planu.” (13 sp, `my_location` w akcencie); na planie kropka i **znicz w obrysie** (miejsce jeszcze niezapisane, [[style-b]] reguła 13) w kropce; dotknięcie planu przesuwa znicz. Na dole arkusz: tytuł grobu, „dokładność GPS ±4 m · źródło pinezki: GPS” i „Anuluj” (tekstowy) · **„Zapisz pinezkę”** (wypełniony) | tryb mapy | „Zapisz pinezkę” → zapis pinezki ze źródłem i dokładnością ([[FR-001-provenance]]) → stan B z tym grobem; „Anuluj”/wstecz → poprzedni stan | pinezka w kropce | dokładność gorsza niż 15 m → pod tekstem „Słaby sygnał — przesuń pinezkę ręcznie.” | M6 · H3 · **decyzja autora** (D22) · D16 |
| 13 | **Bez internetu (M7):** plan bez zmian; plakietka przy „Zdjęciu” — `wifi_off` „bez internetu”, a wybrane „Zdjęcie” pokazuje „Zdjęcie z góry potrzebuje internetu. Plan działa bez niego.” i „Wróć do planu” | stan | — | — | — | [[NFR-001-offline]] · [[ADR-003-map-source-offline]] pkt 2 |
| 14 | **Źródło pinezki w danych:** „GPS ±4 m · 08.10.2026” albo „zaznaczona w domu” (z planu lub zdjęcia z góry) — widać w [[grob]] pod adresem | dane | — | — | — | [[FR-001-provenance]] · [[EPIC-002-wizyta]] (każda pinezka ze źródłem i dokładnością) |

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
| grób bez osób | może przyjść z innych danych (z interfejsu nie powstaje): tytuł karty „Grób bez wpisanych osób” w kolorze pomocniczym |
| brak pliku zdjęcia | wpis zdjęcia jest, pliku nie ma: karta bez miniatury (o braku mówi [[grob]] → *States*) |
| D — stawianie pinezki | 1, 2 (z kropką i zniczem w obrysie), 12 zamiast plakietek i arkuszy |
| bez internetu | 1–6, 13 |

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

## Tempo
Rekordem jest **grób**: ok. 50 na całe notatki (G6, [[NT-002-transcribe-the-notes]]).
- **Nowy grób:** stan A → „Dodaj grób” = **1 dotknięcie** (jak w v3), potem formularz pierwszej osoby ([[wpis-osoby]]
  → *Tempo*).
- **Pierwszy grób na nowym cmentarzu:** znicz → „Otwórz cmentarz” → „Dodaj grób” = 3 dotknięcia (jak w v3).
- **Grób bez pinezki:** pasek → karta = **2 dotknięcia** (w v3 jedno). Przy przepisywaniu wszystkie groby są bez
  pinezki, ale przepisywanie prowadzi „Dodaj grób”, a do listy wraca się rzadziej.
- **Grób z pinezką:** znicz → „Pokaż grób” = 2 dotknięcia.
- **Nazwa grobu** nie kosztuje tu nic — nadaje się ją w [[grob]].

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
- **Tokeny:** zieleń offline `stateOk` (w `theme.dart` od [[ISSUE-022-app-skeleton-tabs-people-settings]]); v5 bez nowych
  tokenów. Kontrast: tytuł karty 10,02:1, linie pomocnicze 5,01:1 na powierzchni (W2 z *Open*: 10,02:1), zieleń 8,19:1 na
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
| US-007 AC-4 — kwatery autora | 4 | → [[ISSUE-028-cemetery-sectors]] |
| US-007 AC-5 — bez planu | 2a (b), 6 | cmentarz dodany bez sieci: „pobierze się, gdy będzie internet”, „Pobierz teraz”, a pasek prowadzi do listy |

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

## Open
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
  (`CURRENT_STATE.md` → *Parked*, SPIKE-001 D5). Od wyniku zależy próg „słaby sygnał” (element 12) — [[US-008-pinezka-na-miejscu]].
- **Nie do `ui` — czy plan wchodzi do kopii** (`planning`, kandydat na ADR). Widoczny skutek: jeśli plan nie wchodzi do
  kopii, po odtworzeniu na nowym telefonie każdy cmentarz pokazuje (a) albo (b), aż telefon dostanie internet.
- **Znicze sąsiednich grobów nachodzą na siebie** (przegląd ISSUE-027, odstępstwo 4): przy z19 na 52° N 1 dp to ok. 0,18 m, więc
  cel 48 dp ma ok. 9 m, a znicz ok. 5 m — groby obok siebie zasłonią się nawet przy największym przybliżeniu, a łączenie w znicz
  z liczbą (jak na mapie Polski) ich nie rozdzieli. Kandydat dla [[US-008-pinezka-na-miejscu]]: znicz z liczbą otwiera arkusz z
  listą tych grobów. Do tego czasu wybór przez listę (C).
- **Główne i boczne alejki według rodzaju z OSM** (przegląd ISSUE-027, pkt 9): na publicznym cmentarzu testowym prawie wszystkie
  alejki mają w OSM `footway`, więc rysują się jako boczne (2 dp), także te, które są główne na miejscu. Kandydat: grubość z
  `width`/`surface` albo jedna grubość dla wszystkich — decyzja, gdy autor zobaczy plany swoich cmentarzy.
- **Znana luka — przesuwanie przybliżonego planu tylko przeciągnięciem** (SC 2.5.7). Wszystkie znicze są w kadrze startowym,
  a lista (C) prowadzi do każdego grobu jednym dotknięciem, więc żadne działanie nie wymaga przeciągania. Kandydat:
  przycisk „cały cmentarz”, gdy autor zgubi się na przybliżonym planie.
