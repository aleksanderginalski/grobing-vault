---
screen: "Ekran główny — mapa Polski z cmentarzami rodziny"
items: ["[[ISSUE-012-transcribe-grave-screen]]", "[[ISSUE-014-home-map-of-poland]]", "[[ISSUE-015-add-cemetery-from-database]]", "[[SPIKE-004-mvp-flow-prototype]]", "[[ISSUE-022-app-skeleton-tabs-people-settings]]", "[[ISSUE-023-poland-map-r1-cemetery-photo]]", "[[ISSUE-027-cemetery-map-plan-photo-states]]", "[[ISSUE-052-cemetery-search-and-patient-plan]]"]
us: "[[US-002-przepisanie-grobu]]"
journey-step: "UJ-001 · 1 (widok 1, M2) · warunek kroku 1: dodanie cmentarza (M1)"
mockup: "katalog tymczasowy sesji 2026-10-06: makieta-mapa-polski.html (ramki 1–10, wersja 2 po stopie #1) · 2026-10-08: grobing-prototyp.html (SPIKE-004, klikalny)"
updated: 2026-10-23
---

# Ekran główny — mapa Polski — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.20) · referencja: [[references]] → **R1**.
>
> **Historia:** do ISSUE-014 plik opisywał listę cmentarzy jako ekran główny (pierwsza wersja `ui`). Autor
> zdecydował, że ekranem głównym jest od startu mapa Polski jak R1. Nazwa pliku zostaje, bo linkują do niej
> zamknięte pozycje.
>
> **Wersja 2 — stop #1 ISSUE-014, runda 1 (2026-10-06):**
> - cmentarz dodaje się **z bazy cmentarzy** (OpenStreetMap, wbudowana), a ręczne dodanie zostaje
>   zapasem. Uzasadnienie i pomiar: [[ISSUE-014-home-map-of-poland]] → *Stop #1 — round 1*;
> - poprawa to **ikonka edycji w prawym górnym rogu kafla cmentarza**, a nie przycisk „Popraw”.
>
> **Wersja 2.1 — stop #1 ISSUE-015 (2026-10-07):** poprawki zatwierdzone przez autora; uzasadnienia:
> [[ISSUE-015-add-cemetery-from-database]] → *Decisions for stop #1*.
> - link do zdjęcia satelitarnego otwiera adres Map Google z warstwą satelitarną zamiast `geo:` (D1 → element 14, D18);
> - brak aplikacji, która otworzy link → komunikat „Nie ma aplikacji, która to otworzy.” (D2 → element 14, *States*, D18);
> - podpis licencji „Dane: © autorzy OpenStreetMap (ODbL)” (D3 → element 12, D16, szkic);
> - miejscowość według D9 ISSUE-014, a nie z granic administracyjnych (D4 → element 12, D16);
> - *AC → element*: wiersze dla 7 AC ISSUE-015, z prefiksem „(ISSUE-015)”.
>
> **Wersja 2.2 — przegląd `ui` zbudowanego ekranu ISSUE-015 (2026-10-07):** poprawki z przeglądu, wprowadzone
> w kodzie przed stopem #2, i odstępstwa `dev` przyjęte w przeglądzie
> ([[ISSUE-015-add-cemetery-from-database]] → *Dev report → Deviations* 3, 5–7):
> - podgląd przybliża o 1,5 stopnia ponad całą Polskę, a nie o 3. Pomiar na wyciągu: miasto w kadrze przy
>   96% cmentarzy zamiast 29% (D22 → element 14);
> - okno z bazy otwiera się nad podglądem, a „Anuluj” wraca do podglądu. Błąd zapisu pokazuje się w karcie
>   podglądu, a okno wraca z wpisanymi wartościami (D23 → elementy 14 i 15, *Navigation*, *States*);
> - „Pokazuję 30 z N — dopisz miejscowość.” stoi pod nagłówkiem sekcji „Z bazy cmentarzy”, a nie pod
>   ostatnią kartą (D24 → element 12);
> - separator w linii miejscowości nie zostaje na końcu linii (D25 → element 12);
> - przy błędzie bazy cmentarzy jest przycisk „Dodaj ręcznie” (odstępstwo 5 → *States*);
> - w podglądzie mapa stoi nad kartą, a nie pod nią (odstępstwo 6 → element 14, szkic);
> - miejscowość w oknie z bazy jest bez dzielnicy (odstępstwo 7 → element 15);
> - strzałka linku to ikona `north_east` (odstępstwo 3 → [[style-b]] v1.5, reguła 1);
> - szkic: mapa nad kartą, bez pustego nagłówka „Twoje cmentarze”.
>
> **Wersja 2.3 — discovery na prototypie, panel 0+1 ([[SPIKE-004-mvp-flow-prototype]], 2026-10-08):**
> - **dolny pasek Mapa · Osoby · Drzewo na tym ekranie** (element 18), koło zębate zostaje (autor: *„1. tak”*,
>   *„2. tak zostaje”* — D26, [[style-b]] v1.12 reguła 12);
> - **wyszukiwarka zostaje „Szukaj cmentarza” na stałe**, a osób szuka zakładka Osoby (autor: *„Tylko cmentarze,
>   jeżeli ktoś będzie chciał poszukać osoby to wejdę w zakładkę osoby”* — D27, zmienia D2);
> - otwarte po rundzie 2: zdjęcie cmentarza w arkuszu i wygląd mapy jak R1 (*Open*).
>
> **Wersja 2.4 — discovery na prototypie, panel 1, runda 2 ([[SPIKE-004-mvp-flow-prototype]], 2026-10-08):**
> - **zdjęcie cmentarza w arkuszu** (element 6a): miniatura z lewej jak w R1, a bez zdjęcia pole „Dodaj zdjęcie”
>   (autor: *„1 tak”* — D28);
> - **mapa Polski jak R1** (element 3): sąsiedzi, Bałtyk, jeziora, rzeki w kolorze wody, „Polska”, 11 miast (autor:
>   *„Mapa Polski B - jest ok”* — D29, zastępuje D9);
> - **Polska wyśrodkowana bez arkusza**, a po otwarciu arkusza przesunięta nad niego (D30).
>
> **Wersja 2.5 — pasek dolny i koło zębate zbudowane ([[ISSUE-022-app-skeleton-tabs-people-settings]], przegląd `ui`,
> 2026-10-08):**
> - **koło zębate → [[ustawienia]]**, a „Stan danych” o poziom niżej (element 1, *Navigation*);
> - pasek dolny na mapie, cmentarzu i grobie; przełączanie zakładek, wstecz i zaślepka Drzewa (D31 → element 18,
>   *Navigation*);
> - element 18: semantyka zakładek, klawiatura zakrywa pasek, podpis 12 sp jako wyjątek w [[style-b]] v1.17.
>
> **Wersja 2.6 — przegląd `ui` zbudowanego ekranu [[ISSUE-023-poland-map-r1-cemetery-photo]] (2026-10-12):** odstępstwa `dev`
> przyjęte w przeglądzie i poprawki z przeglądu (*Dev report → Deviations* 1–7, *Found on the emulator* 4):
> - **falsyfikator D26 się zapalił** (360 × 640 dp: Polska ok. 145 dp, podpisy nachodzą). „Niższy arkusz” nie wystarcza, więc
>   najmniejsze przybliżenie nie zależy od arkusza (cała Polska na szerokość ekranu), a na krótkim ekranie przy arkuszu działa
>   reguła znicza (D26, D30);
> - arkusz stoi na pasku dolnym i **nie dokłada marginesu paska gestów** — ten trzyma pasek dolny (nagłówek arkusza, D30);
> - podpisy mapy rosną z tekstem najwyżej do 1,3×; „Polska” tylko przy najmniejszych przybliżeniach; brzegi sąsiadów bez
>   linii; progi jezior (D32 → element 3);
> - arkusz z miniaturą: nazwa przy górze miniatury, ✎ w linii pierwszej linii nazwy; stany miniatury (D33 → 6a, *States*);
> - *AC → element*: wiersze dla 4 AC ISSUE-023, szkic arkusza z miniaturą.
>
> Które elementy dowozi która pozycja, mówi plan (`planning`), a nie ten plik.
>
> **Wersja 2.7 (2026-10-12, przed planem [[ISSUE-027-cemetery-map-plan-photo-states]]):** zapis cmentarza z punktem (okno 15
> z bazy, „Zapisz” w trybie wskazania 17) i zmiana punktu przy poprawie **uruchamiają pobieranie planu cmentarza**
> ([[ADR-003-map-source-offline]] pkt 1). Na tym ekranie nic się nie zmienia: postęp i braki planu widać w [[cmentarz]] (element
> 2a), a nie w arkuszu (D34).
>
> **Wersja 2.8 (2026-10-22, przed planem [[ISSUE-052-cemetery-search-and-patient-plan]]) — pierwsze użycie z prawdziwymi cmentarzami.**
> Autor nie znalazł cmentarza parafialnego we wsi, który jest w bazie: OSM przypisał go do przysiółka, a nazwa wsi była tylko wśród
> okolicznych miejscowości (pomiar: pozycja → *Why*). Zmiany:
> - **karta wyniku z bazy mówi „przy: <miejscowość>”**, gdy słowo trafiło tylko w okoliczną miejscowość (element 12, D35);
> - **nowa kolejność wyników z bazy:** całe słowa przed rdzeniami, potem nazwa → miejscowość z karty → okolica → środek słowa, potem
>   mniej pól, potem alfabet (element 12, D36);
> - **stan planu w arkuszu i na liście „Twoje cmentarze”** — „Plan offline” albo brak z powodem; spełnia *Obali* D34 (element 6, 11, D37,
>   decyzja projektowa — autor: *„aby na 100% mieć je na wyjazd”*).
>
> **Wersja 2.9 (2026-10-23, przegląd `ui` zbudowanego ekranu [[ISSUE-052-cemetery-search-and-patient-plan]]):** przyjęte z budowy (D38):
> - **ikona linii planu w arkuszu 18 dp**, jak ikona linii liczb (element 6) — v2.8 mówiło naraz „jak linia liczb” i „20 dp” (odstępstwo 2
>   `dev`);
> - **„przy: <miejscowość>” to jedna całość** — twarda spacja po „przy:” i między słowami nazwy, żeby dwuczłonowa nazwa przy dużym tekście nie
>   czytała się jak dwie miejscowości (element 12; `dev` → *Found on the emulator*). Nazwa, która razem z „· przy:” nie mieści się w linii,
>   łamie się między swoimi słowami, nigdy w środku słowa.

## Purpose
Zbierający otwiera aplikację i widzi, **na których cmentarzach w Polsce leży jego rodzina**, ze zniczem na
każdym. Wybiera, dokąd jechać albo który cmentarz przepisywać (UJ-001 krok 1, M2). Nowy cmentarz **wybiera
z bazy cmentarzy Polski**, żeby trafić we właściwy cmentarz we właściwym miejscu, a nie stawiać punkt na
oko (M1). Mapa i baza działają bez sieci od pierwszego uruchomienia: kontur, miasta i rzeki z Natural Earth,
a cmentarze z OpenStreetMap są wbudowane w aplikację.

## Navigation
- **Start aplikacji → ten ekran.** Ekran startowy z [[ISSUE-002-bootstrap-code-repo]] znika; natywny ekran
  uruchamiania (tło `grobing_background`) zostaje.
- **Koło zębate → [[ustawienia]]** (od [[ISSUE-022-app-skeleton-tabs-people-settings]]; „Stan danych” jest tam o poziom
  niżej — [[ustawienia]] D1). Do ISSUE-022 koło otwierało od razu „Stan danych”.
- **Znicz → arkusz cmentarza** (6–8); **znicz z liczbą → arkusz grupy** (9) → wiersz → arkusz cmentarza.
- **„Otwórz cmentarz” → [[cmentarz]]** — dochodzi z [[ISSUE-012-transcribe-grave-screen]] (decyzja autora:
  ISSUE-014 → *Decisions for stop #1* D5).
- **Wyszukiwarka → tryb wyszukiwania** (10–13):
  - karta „Twoje cmentarze” → mapa z wybranym zniczem i arkuszem;
  - wynik „Z bazy cmentarzy” → **podgląd** (14) → „Dodaj ten cmentarz” → **okno** (15) **nad podglądem** →
    zapis → mapa z nowym zniczem i arkuszem (D23);
  - „Nie ma go w bazie — dodaj ręcznie” → **okno** (15) → **tryb wskazania** (16–17) → zapis.
- **Ikonka edycji w arkuszu** → okno „Popraw cmentarz” (15) → tryb wskazania (16–17) z obecnym zniczem.
- **Wstecz:** z trybu wskazania → okno z wpisanymi wartościami; z okna („Anuluj”) → widok pod oknem bez
  zapisu: przy cmentarzu z bazy podgląd (D23), przy ręcznym dodaniu i poprawie mapa; z podglądu → wyniki z
  tym samym tekstem; z wyszukiwania → mapa; z otwartego arkusza → zamyka arkusz; z mapy → wyjście z
  aplikacji.
- **Dolny pasek Mapa · Osoby · Drzewo** (element 18, D26). Mapa jest zakładką aktywną także na [[cmentarz]]
  i niżej, a wyszukiwanie, okno i tryb wskazania pasek chowają ([[style-b]] reguła 12). **Zbudowany w
  [[ISSUE-022-app-skeleton-tabs-people-settings]]** (D31): mapa zawsze leży na dole stosu; „Osoby” i „Drzewo” kładą
  swój ekran nad mapą bez wsuwania, a wstecz z nich wraca na mapę; „Mapa” z cmentarza albo grobu wraca na mapę Polski.
  **Drzewo prowadzi do zaślepki** „Drzewo powstanie po SPIKE-002. Na razie rodzinę widać przy osobie.” (z paskiem,
  aktywne Drzewo), dopóki nie ma [[drzewo]] (ISSUE-022 D1 = A).

## Elements in order
**Mapa (ekran główny)**

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek: **ikona znicza (akcent) + „Grobing”** (półgruby, 22 sp); po prawej koło zębate (`settings_outlined`, tekst pomocniczy, `tooltip` „Ustawienia”) | pasek | koło → [[ustawienia]] (od ISSUE-022; wcześniej „Stan danych”) | — | — | R1 · *What to build* 5 · [[style-b]] reguła 8 · ISSUE-022 |
| 2 | **Wyszukiwarka:** pigułka na powierzchni, wys. 56 dp, margines 16 dp, ikona `search` (tekst pomocniczy), podpowiedź **„Szukaj cmentarza”** | pole (tylko wejście) | dotknięcie → tryb wyszukiwania (10) | pusto | — | R1 · *What to build* 3 · D2 |
| 3 | **Mapa Polski jak R1 (v2.4, D29)** na całą szerokość pod wyszukiwarką: **Polska** — ląd w kolorze powierzchni, granica w kolorze **tekstu pomocniczego** (1,4 dp; 5,01:1 na lądzie, 5,04:1 na wodzie, 5,50:1 na tle); **sąsiednie kraje** w kolorze tła z granicami w kolorze obrysu (0,7 dp, krycie 45%, dekoracja); **Bałtyk i jeziora** w kolorze **wody** (nowa rola, token `water`, od ISSUE-023 w `theme.dart`); **rzeki** linią wody (1 dp, token `waterLine`, dekoracja); napis **„Polska”** (22 sp, półgruby, odstęp liter 2, tekst pomocniczy, krycie 85%) w wolnym miejscu północnej części kraju; **11 miast** (kropka 4 dp + podpis 13 sp, tekst pomocniczy, z obwódką 2–3 dp w kolorze lądu — [[style-b]] reguła 13): Szczecin, Gdańsk, Bydgoszcz, Białystok, Poznań, Warszawa, Łódź, Wrocław, Katowice, Lublin, Kraków. Dane: Natural Earth 1:10m (siedem warstw od ISSUE-023). Bez faktury terenu. **Podpisy mapy** (miasta i „Polska”) rosną z tekstem systemu najwyżej do 1,3×; „Polska” stoi tylko do +2 kroków przybliżenia (v2.6, D32) | mapa | szczypanie, przeciąganie, podwójne dotknięcie; ruch ograniczony do Polski; najmniejsze przybliżenie = cała Polska z marginesem 16 dp, **wyśrodkowana w pionie w obszarze mapy, gdy arkusz jest zamknięty; po otwarciu arkusza mapa przesuwa się płynnie w górę, tak że Polska stoi nad arkuszem** (v2.4, D30). **Na krótkim ekranie** Polska zostaje na całą szerokość, a przy otwartym arkuszu działa reguła znicza z elementu 4 (v2.6, D26); bez obrotu; dotknięcie pustego miejsca zamyka arkusz | cała Polska, północ u góry | — | R1 · *What to build* 1 · D14, D29, D30 |
| 4 | **Znicze cmentarzy** w punkcie cmentarza: pinezka w akcencie z sylwetką znicza w kolorze tła, 32 × 40 dp, **cel dotyku 48 × 48 dp**. Wybrany: 40 × 50 dp z poświatą. **Znicze, których cele nachodzą na siebie, łączą się w jeden znicz z liczbą** (plakietka: powierzchnia, obrys w akcencie, cyfra w kolorze tekstu). Znicz rysuje się nad podpisami miast | znaczniki | dotknięcie → arkusz (6) albo arkusz grupy (9); mapa przesuwa się tak, żeby znicz (także znicz z liczbą) nie stał pod arkuszem — według wysokości narysowanego arkusza | — | cmentarz bez punktu nie ma znicza | R1 · *What to build* 2 · AC-2 · D8 |
| 5 | **Stan pusty:** karta na powierzchni na dole: „Tu pojawią się cmentarze rodziny.” (tekst pomocniczy) + **wypełniony „Dodaj cmentarz”** (`add_location_alt_outlined`) | karta + przycisk główny | → tryb wyszukiwania (10) z podpowiedzią „Wpisz nazwę cmentarza albo miejscowość” | — | — | AC-1 · [[style-b]] reguła 9 · D16 |

**Arkusz cmentarza** — dolny arkusz na powierzchni, promień 16 dp, uchwyt: przeciągnięcie w dół zamyka arkusz jak dotknięcie mapy; mapa pod nim działa. **Stoi na pasku dolnym (18)**, a dół treści ma 20 dp. Margines paska gestów trzyma pasek dolny, więc arkusz go nie dokłada; to samo dotyczy karty pustego stanu (5). Do ISSUE-022 arkusz sięgał krawędzi ekranu i sam trzymał treść nad paskiem gestów (v2.6)

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 6 | **Nazwa** (tekst, 18 sp, półgruby, do 2 linii) · **miejscowość** (tekst pomocniczy, 14 sp) · ikona `people_outline` + **„6 grobów · 14 osób”** (tekst pomocniczy, odmiana — [[style-b]] reguła 6). Bez punktu: ikona `location_off_outlined` + „Bez punktu na mapie”. **Pod liczbami linia planu (v2.8, D37)**, jak linia liczb: 14 sp, tekst pomocniczy, ikona 18 dp jak przy liczbach, rosnąca z tekstem (v2.9, D38): plan zapisany → `offline_pin_outlined` + **„Plan offline”** (te same słowa co plakietka w [[cmentarz]]); pobieranie trwa → `cloud_download_outlined` + „Pobieram plan…”; bez internetu → `cloud_download_outlined` + „Plan pobierze się, gdy będzie internet.”; serwer nie odpowiedział albo nic jeszcze nie próbowało → `cloud_off_outlined` + „Bez planu — pobierze się sam.”; brak obrysu w OSM → `not_listed_location_outlined` + „W OpenStreetMap nie ma planu.”. Bez punktu linii planu nie ma (jest „Bez punktu na mapie”) | tekst | — | — | — | R1 · *What to build* 4 · AC-4 · D13 · D37 |
| 6a | **Zdjęcie cmentarza (v2.4, D28)** z lewej, przed nazwą: zaokrąglony prostokąt **96 × 80 dp**, promień 12 dp, przycięty ze środka ([[style-b]] reguła 14). Nazwa, miejscowość i liczby stoją obok: **nazwa zaczyna się przy górze miniatury, a ✎ (8) stoi w prawym górnym rogu, w linii pierwszej linii nazwy** (v2.6, D33). Opis dla czytnika: „Zdjęcie cmentarza — otwórz”. **Bez zdjęcia:** w tym samym miejscu pole **„Dodaj zdjęcie”** — obrys, ikona `add_a_photo_outlined` w akcencie, podpis 12 sp półgruby (wyjątek w [[style-b]] *Thresholds*, v1.20; reguła 14: puste miejsce tylko jako przycisk); z dużym tekstem pole rośnie (podpis w dwóch liniach). Dla czytnika pole i miniatura to osobne przyciski z akcją dotknięcia, a nie część arkusza. Zdjęcie robi autor; to treść użytkownika, bez filtrów | zdjęcie / przycisk | zdjęcie → zdjęcie cmentarza na pełnym ekranie ze „Zmień zdjęcie” i „Usuń zdjęcie”, jak [[zdjecie]] przy nagrobku (tryb cmentarza, v1.6); „Dodaj zdjęcie” → wybór źródła „Zdjęcie cmentarza”: „Wybierz z galerii” · „Zrób zdjęcie” ([[zdjecie]] A) → zapis od razu → zdjęcie w arkuszu. **Zapis:** w miejscu pola wskaźnik postępu bez słów (nie mieszczą się w 96 × 80), a czytnik słyszy „Zapisuję zdjęcie…”. **Błąd zapisu:** pod wierszem `error_outline` + „Nie udało się zapisać zdjęcia. Spróbuj jeszcze raz.” (kolor błędu, jak w [[grob]]); pole zostaje | brak zdjęcia | — | R1 (miniatura w arkuszu) · **decyzja autora** (SPIKE-004 D5) · D28 · ISSUE-023 D3 · D33 |
| 7 | **„Otwórz cmentarz”** — wypełniony, pełna szerokość karty, z ikoną znicza (kolor tła), ≥ 52 dp | przycisk główny | → [[cmentarz]] | — | — | R1 · ISSUE-012 (D5) |
| 8 | **Ikonka edycji** w prawym górnym rogu arkusza, w linii nazwy: `edit_outlined` w akcencie, cel 48 × 48 dp, `tooltip` „Popraw cmentarz”. Nazwa zawija się przed ikonką | przycisk-ikona | → okno „Popraw cmentarz” (15) | — | — | **decyzja autora** (stop #1, runda 1) · D7 |

**Arkusz grupy** (znicz z liczbą)

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 9 | Nagłówek „4 cmentarze w tym miejscu” (tekst pomocniczy, 13 sp) + **wiersze cmentarzy**: nazwa (16 sp, półgruby) · „Miejscowość · 3 groby · 6 osób” (tekst pomocniczy) · chevron „›”; wiersz ≥ 64 dp, bez własnego tła (arkusz już jest powierzchnią), linia podziału w kolorze obrysu | lista | wiersz → arkusz cmentarza (6–8), jego znicz wybrany | alfabetycznie po nazwie | — | [[style-b]] reguła 11 · D8, D21 |

**Tryb wyszukiwania** — pełny ekran nad mapą

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 10 | Pasek: wstecz + **pole wyszukiwania** z fokusem i klawiaturą od razu; `close` czyści tekst | pole tekstowe, bez wielkiej litery | `search` = zamknij klawiaturę | pusto | — | *What to build* 3 |
| 11 | **Pusty tekst:** sekcja **„Twoje cmentarze”** — wszystkie zapisane jako karty (nazwa 16 sp półgruby · „Miejscowość · 3 groby · 6 osób”, a bez punktu „· bez punktu na mapie” · chevron). **Cmentarz z punktem bez zapisanego planu ma „· bez planu”**, a z zapisanym „brak obrysu w OSM” — „· bez planu w OSM” (v2.8, D37); z planem nic nie dochodzi, więc lista przed wyjazdem pokazuje braki bez otwierania każdego arkusza. Bez zapisanych cmentarzy: „Wpisz nazwę cmentarza albo miejscowość.” (tekst pomocniczy) | lista kart | karta → mapa: wyjście z wyszukiwania, przybliżenie do znicza, arkusz otwarty | alfabetycznie, polskie sortowanie | — | AC-2 · D4 |
| 12 | **Wyniki (od 2 znaków)** w dwóch sekcjach. **„Twoje cmentarze”** — karty jak w 11, które pasują; bez trafień tej sekcji nie ma, także nagłówka. **„Z bazy cmentarzy”** — karty: **nazwa** (16 sp, półgruby; brak nazwy → „Cmentarz bez nazwy” w kolorze pomocniczym) · **„Miejscowość · woj. mazowieckie”**, w mieście albo miasteczku z dzielnicą w nawiasie (D16), i „· rzymskokatolicki”, gdy baza zna wyznanie (tekst pomocniczy) · chevron. **„· przy: Wymyślów” (v2.8, D35)** — zaraz za miejscowością (i dzielnicą), przed województwem — gdy któreś słowo nie zaczyna żadnego słowa nazwy, miejscowości ani dzielnicy karty, a zaczyna słowo okolicznej miejscowości: pokazana jest ta okoliczna miejscowość, w którą trafia najwięcej takich słów (przy remisie pierwsza z listy bazy), jedna, w mianowniku z bazy; „przy:” i nazwa to jedna całość (twarde spacje), a nazwa dłuższa niż linia łamie się tylko między swoimi słowami (v2.9, D38). Części linii łączy „ · ” ze spacją twardą po kropce, więc zawinięta linia zaczyna się od „·” i żadna nie kończy się kropką (D25). Cmentarz z bazy, który już jest u Ciebie (punkt bliżej niż 100 m), ma zamiast chevronu „Dodany” (tekst pomocniczy, wyrównany do kolumny chevronów) i prowadzi do jego arkusza. Najwyżej 30 wyników z bazy; przy większej liczbie **pod nagłówkiem sekcji, nad pierwszą kartą**, stoi „Pokazuję 30 z 214 — dopisz miejscowość.” (14 sp, tekst pomocniczy, D24). Pod sekcją: „Dane: © autorzy OpenStreetMap (ODbL)” (13 sp, tekst pomocniczy). Na końcu przycisk tekstowy **„Nie ma go w bazie — dodaj ręcznie”**. Między sekcjami 24 dp ([[style-b]] reguła 5) | dwie listy kart + przycisk tekstowy | karta z bazy → podgląd (14); „dodaj ręcznie” → okno (15) z nazwą = tekst | twoje alfabetycznie; **z bazy (v2.8, D36), po kolei:** (1) więcej słów wpisanych w całości (bez obcięcia końcówki) jako całe słowo w nazwie, miejscowości, dzielnicy albo okolicy; (2) najdalsze miejsce, którego wymaga któreś słowo: nazwa → miejscowość i dzielnica karty → okolica → tylko w środku słowa; (3) mniej pól, które razem mieszczą wszystkie słowa (cała nazwa miejscowości w jednym polu przed słowami rozrzuconymi); (4) alfabetycznie jak dotąd. Zbiór wyników się nie zmienia — tylko kolejność (D3 zostaje) | — | AC-3 · D3, D16, D17, D24, D25, D35, D36, D38 |
| 13 | **Brak wyników w obu sekcjach:** „Nie ma cmentarza „<tekst>” ani u Ciebie, ani w bazie.” (tekst pomocniczy) + **wypełniony „Dodaj ręcznie”** | tekst + przycisk główny | → okno (15) z nazwą = tekst | — | — | AC-3 |

**Podgląd cmentarza z bazy** — przed dodaniem

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 14 | Pasek: wstecz + „Cmentarz z bazy” (20 sp, półgruby, jak tytuł trybu wskazania). **Mapa przybliżona do punktu o 1,5 stopnia ponad całą Polskę** (ok. 2,8×, ok. 240 km szerokości; przy 96% cmentarzy z bazy w kadrze jest co najmniej jedno z 9 miast — D22). **Znicz w obrysie** stoi w środku kadru (niezapisany, [[style-b]] reguła 13), a zapisane znicze w okolicy są widoczne i nieaktywne. **Pod mapą karta na dole**: mapa i karta stoją jedna pod drugą, więc karta nigdy nie zasłania znicza. Karta: nazwa (18 sp, półgruby), „Miejscowość · woj. …”, wyznanie w osobnej linii, jeśli jest. Link **„Zobacz zdjęcie satelitarne ↗”**: akcent, podkreślony, strzałka jako ikona `north_east` ([[style-b]] reguła 1); cel ≥ 48 dp, rośnie i zawija się z dużą czcionką. Pod linkiem **wypełniony „Dodaj ten cmentarz”** | mapa + karta | link → **Mapy Google z warstwą satelitarną** w tym punkcie (adres Map Google z `zoom=17` i `basemap=satellite`, D18), a bez aplikacji Mapy — przeglądarka; tylko po dotknięciu. **Brak aplikacji, która otworzy adres** → pasek komunikatu na dole „Nie ma aplikacji, która to otworzy.” (sam tekst), podgląd zostaje. „Dodaj…” → okno (15) z danymi z bazy, **otwarte nad podglądem**; „Anuluj” wraca do podglądu. **Błąd zapisu** → w karcie, nad „Dodaj ten cmentarz”: `error_outline` + „Nie udało się zapisać. Spróbuj jeszcze raz.” (kolor błędu, 14 sp). Podgląd zostaje, a ponowne „Dodaj ten cmentarz” otwiera okno z wpisanymi wartościami (D23) | — | — | **decyzja autora** (pewność miejsca) · D18, D19, D22, D23 · ISSUE-015 D1, D2 |

**Okno i tryb wskazania**

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 15 | **Okno** „Nowy cmentarz” / „Popraw cmentarz”, z bazy nad podglądem (14), ręcznie i przy poprawie nad mapą: **Nazwa** (wielka litera na początku słów, `next`), **Miejscowość** (opcjonalna, `done`). Przyciski: z bazy „Anuluj” · **„Zapisz”** (punkt jest z bazy); ręcznie i przy poprawie „Anuluj” · **„Dalej”** → wskazanie. Fokus w pierwszym pustym polu, a gdy oba są wypełnione — w nazwie | okno dialogowe, pola z ramką w kolorze obrysu | „Zapisz” → zapis → mapa z nowym zniczem i arkuszem; błąd zapisu z bazy → podgląd (14) z komunikatem, a okno wraca z wpisanymi wartościami (D23); „Dalej” → 16; „Anuluj” → widok pod oknem (*Navigation*) | **z bazy:** nazwa i miejscowość z bazy, miejscowość **bez dzielnicy** („Warszawa”, a nie „Warszawa (Żoliborz)”: dzielnica rozróżnia wyniki, a w oknie jest Twój zapis); cmentarz bez nazwy → pusta nazwa z podpowiedzią „np. Cmentarz parafialny”. **Ręcznie:** nazwa z wyszukiwarki (wielka litera na początku słów). **Poprawa:** obecne wartości | nazwa wymagana: „Podaj nazwę cmentarza.” (kolor błędu + `error_outline`), okno zostaje | *What to build* 3 · D6, D20, D23 |
| 16 | **Tryb wskazania:** pasek „Wskaż cmentarz na mapie” z `close` (→ okno 15); u góry karta: „Dotknij miejsca, gdzie leży <nazwa>. Mapę możesz przybliżyć.” (tekst pomocniczy). **Dotknięcie mapy stawia znicz w stylu wybranego, kolejne go przesuwa.** **Zapisane znicze są widoczne w zwykłym wyglądzie i nieaktywne**, żeby dało się postawić cmentarz obok innego (D21; przegląd `ui`, 2026-10-06). Wyszukiwarki nie ma | mapa w trybie wyboru | gesty jak 3 | przy poprawie: obecny znicz | — | *What to build* 3 |
| 17 | Dół, na powierzchni: **„Zapisz bez punktu”** (tekstowy) · **„Zapisz”** (wypełniony; aktywny po postawieniu znicza, przy poprawie z punktem od razu). Przy poprawie „Zapisz bez punktu” zdejmuje znicz z mapy | przyciski | zapis przez API danych → mapa z wybranym zniczem (bez punktu: sam arkusz) | — | błąd zapisu: „Nie udało się zapisać. Spróbuj jeszcze raz.” (kolor błędu + ikona); tryb zostaje | DoD (kopia w tle) · [[style-b]] reguła 10 |

**Pasek dolny** (v2.3, [[SPIKE-004-mvp-flow-prototype]])

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 18 | **Pasek dolny** na powierzchni, wys. 72 dp (plus dolny margines systemu), linia podziału u góry w kolorze obrysu: trzy zakładki **Mapa** (`map_outlined`) · **Osoby** (`group_outlined`) · **Drzewo** (`account_tree_outlined`), każda na 1/3 szerokości, ikona nad podpisem (12 sp, półgruby — wyjątek od 13 sp, [[style-b]] *Thresholds*, v1.17). Aktywna: ikona, podpis i podkreślenie podpisu 2 dp w akcencie; nieaktywne w kolorze tekstu pomocniczego. Dla czytnika każda zakładka to przycisk z nazwą, a aktywna ma stan „wybrana”. Arkusz cmentarza (6–8) i arkusz grupy (9) stoją **nad** paskiem; **otwarta klawiatura zakrywa pasek** | nawigacja | zakładka → jej ekran główny, stos zakładki od początku, **bez wsuwania**; zakładka na swoim ekranie głównym nic nie robi; mapa zawsze na dole stosu (D31) | Mapa | — | R1 · [[style-b]] reguła 12 · D26 · D31 |

Liczby odmieniają się po polsku: 1 grób · 2–4 groby · 5+ grobów (też 12–14 grobów, 22–24 groby) · 0
grobów; tak samo osoba / osoby / osób i cmentarz / cmentarze / cmentarzy.

## States
| Stan | Co widać |
|---|---|
| pusty | pasek, wyszukiwarka, **cała mapa Polski** (także w trybie samolotowym, AC-1) i karta z elementu 5 |
| wczytywanie | kontur rysuje się od razu z danych w aplikacji; znicze pojawiają się po odczycie bazy. Bazę cmentarzy Polski aplikacja wczytuje przy pierwszym wejściu w wyszukiwarkę, bez wskaźnika, chyba że trwa dłużej niż ok. 0,3 s — wtedy cienki pasek postępu pod polem |
| błąd | **odczyt bazy danych:** mapa zostaje, na dole karta „Nie udało się odczytać cmentarzy.” + „Spróbuj ponownie” (z obrysem). **Dane wbudowane** (mapa, baza cmentarzy; błąd = usterka aplikacji): w miejscu mapy „Nie udało się narysować mapy.” (także w podglądzie 14; karta działa). W wyszukiwarce sekcję z bazy zastępuje tekst „Baza cmentarzy jest niedostępna — dodaj ręcznie.” (tekst pomocniczy, bez koloru błędu) i przycisk **„Dodaj ręcznie”** → okno (15) z nazwą = tekst. Bez twoich trafień przycisk jest wypełniony (jedyne działanie), a pod twoimi trafieniami tekstowy w akcencie ([[style-b]] reguła 1). Wyszukiwanie wśród twoich i dodanie ręczne działają. **Zapis:** element 17; z bazy — element 14 (D23). **Okno:** element 15 |
| wypełniony | znicze bez arkusza; nic nie jest wybrane |
| wybrany | znicz powiększony z poświatą, arkusz cmentarza (6–8) |
| wybrany — zdjęcie cmentarza (6a, v2.6, D33) | **wczytywanie miniatury:** miejsce 96 × 80 w kolorze tła, bez wskaźnika (na telefonie trwa ułamek sekundy, jak „B — wczytywanie” w [[zdjecie]]); to chwila przed obrazem, a nie zastępczy obrazek z reguły 14. **Błąd odczytu miniatury:** w tym miejscu `broken_image_outlined` (tekst pomocniczy, 5,50:1 na tle); dotknięcie otwiera podgląd z „Nie udało się otworzyć zdjęcia.”, gdzie da się zdjęcie zmienić albo usunąć. **Zapis** i **błąd zapisu:** element 6a |
| grupa | znicz z liczbą powiększony, arkusz grupy (9) |
| wyszukiwanie | pusty tekst (11) · wyniki (12) · brak wyników (13) |
| podgląd | element 14. **Brak aplikacji, która otworzy link:** pasek komunikatu na dole „Nie ma aplikacji, która to otworzy.” — sam tekst, bez ikony i bez koloru błędu (D18); podgląd zostaje, „Dodaj ten cmentarz” działa. **Okno nad podglądem:** element 15 (D23). **Błąd zapisu:** w karcie `error_outline` + „Nie udało się zapisać. Spróbuj jeszcze raz.” w kolorze błędu; ponowne „Dodaj ten cmentarz” otwiera okno z wpisanymi wartościami (D23) |
| wskazywanie | elementy 16–17 |

## Sketch
```
 wyszukiwanie: wyniki (ponad 30)      podgląd cmentarza z bazy (mapa nad kartą)
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│ ←  parafialny                  ✕ │  │ ←  Cmentarz z bazy               │
│  Z bazy cmentarzy                │  ├──────────────────────────────────┤
│  Pokazuję 30 z 214 — dopisz      │  │   ·Łódź                          │
│  miejscowość.                    │  │                                  │
│ ╭──────────────────────────────╮ │  │              ◌  ← znicz w obrysie│
│ │ Cmentarz parafialny        › │ │  │                       ·Warszawa  │
│ │ Wymyślin · woj. mazowieckie  │ │  ├──────────────────────────────────┤
│ │ · rzymskokatolicki           │ │  │ ╭──────────────────────────────╮ │
│ ╰──────────────────────────────╯ │  │ │ Cmentarz parafialny          │ │
│ ╭──────────────────────────────╮ │  │ │ Wymyślin · woj. mazowieckie  │ │
│ │ Cmentarz parafialny        › │ │  │ │ rzymskokatolicki             │ │
│ │ Wymyślin Mały · woj. łódzkie │ │  │ │ Zobacz zdjęcie satelitarne ↗ │ │
│ ╰──────────────────────────────╯ │  │ │ ╭──────────────────────────╮ │ │
│  …                               │  │ │ │    Dodaj ten cmentarz    │ │ │
│  Dane: © autorzy OSM (ODbL)      │  │ │ ╰──────────────────────────╯ │ │
│ Nie ma go w bazie — dodaj ręcznie│  │ ╰──────────────────────────────╯ │
└──────────────────────────────────┘  └──────────────────────────────────┘
 arkusz cmentarza (v2.6: miniatura z lewej, ✎ w linii nazwy)   bez zdjęcia
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│               ═══                │  │               ═══                │
│ ╭────────╮ Cmentarz Wymyślony  ✎ │  │ ┌────────┐ Cmentarz Wymyślony  ✎ │
│ │[zdjęcie│ Miejscowość Testowa   │  │ │  [+📷] │ Miejscowość Testowa   │
│ │ 96×80] │ 👥 2 groby · 3 osoby  │  │ │ Dodaj  │ 👥 2 groby · 3 osoby  │
│ ╰────────╯                       │  │ │zdjęcie │                       │
│ ╭──────────────────────────────╮ │  │ └────────┘                       │
│ │      Otwórz cmentarz         │ │  │ ╭──────────────────────────────╮ │
│ ╰──────────────────────────────╯ │  │ │      Otwórz cmentarz         │ │
├──────────────────────────────────┤  │ ╰──────────────────────────────╯ │
│  Mapa      Osoby      Drzewo     │  ├──────────────────────────────────┤
└──────────────────────────────────┘  └──────────────────────────────────┘
```
v2.8 — wynik przez okoliczną miejscowość (D35) i linia planu w arkuszu (D37):
```
 „wymyslow” — karta z bazy                arkusz: plan zapisany · plan jeszcze nie
╭──────────────────────────────────╮  │ Cmentarz Wymyślony             ✎ │
│ Cmentarz parafialny            › │  │ Zmyślonka                        │
│ Zmyślonka · przy: Wymyślów       │  │ 👥 2 groby · 3 osoby             │
│ · woj. małopolskie               │  │ ⊙ Plan offline                   │
│ · rzymskokatolicki               │  │   (albo: ☁ Bez planu — pobierze  │
╰──────────────────────────────────╯  │    się sam.)                     │
```
Czego szkic nie pokazuje:
- „Cmentarz bez nazwy” w kolorze pomocniczym i „Dodany” zamiast chevronu (element 12);
- brak sekcji „Twoje cmentarze”, gdy nic u Ciebie nie pasuje: bez nagłówka i bez „(brak)”;
- okno nad podglądem i błąd zapisu w karcie podglądu (elementy 14 i 15, D23).

Szkic pokazuje „↗” jako znak; w aplikacji to ikona `north_east` ([[style-b]] reguła 1).

## Tempo
Ekran do wybierania; wpisywanie jest rzadkie. Rekordem jest **cmentarz**: ok. 10 na całe notatki.
- **Otwarcie cmentarza:** znicz → „Otwórz cmentarz” = **2 dotknięcia** (przy zniczu z liczbą 3).
- **Nowy cmentarz z bazy:** wyszukiwarka + 1–2 słowa → wynik → (podgląd) „Dodaj ten cmentarz” → (okno)
  „Zapisz” = **4 dotknięcia** poza pisaniem. Nic nie trzeba przepisywać ani wskazywać.
- **Ręcznie (zapas):** jak wcześniej, ok. 7 akcji poza pisaniem.

## Style B rules applied
- **Reguła 1:** jeden wypełniony przycisk w danym stanie: „Dodaj cmentarz” (pusty), „Otwórz cmentarz”
  (arkusz), „Dodaj ten cmentarz” (podgląd), „Dodaj ręcznie” (brak wyników; błąd bazy cmentarzy bez twoich
  trafień), „Zapisz” (wskazanie). Link „Zobacz zdjęcie satelitarne ↗” ma formę linku zewnętrznego, a
  strzałka to ikona `north_east` (v1.5).
- **Reguła 2:** arkusz, karty i karta podglądu na powierzchni, promień 16 dp. Poświata tylko przy wybranym
  zniczu i głównym przycisku.
- **Reguła 3:** ikony `outlined`; w akcencie przy działaniach (ikonka edycji, „Dodaj cmentarz”).
- **Reguła 4:** „Grobing”, tytuły pasków („Cmentarz z bazy”, „Wskaż cmentarz na mapie”) i nazwy cmentarzy
  półgrube.
- **Reguła 5:** 24 dp między sekcjami „Twoje cmentarze” i „Z bazy cmentarzy”, 8 dp między kartami.
- **Reguła 6:** liczby odmienione po polsku.
- **Reguła 7:** brak opisany faktem („Bez punktu na mapie”, „Cmentarz bez nazwy”, „Nie ma aplikacji, która to
  otworzy.”), bez ostrzeżenia.
- **Reguła 8:** znicz w logo, w pinezce i na „Otwórz cmentarz”. „Dodaj”, ikonka edycji i „Zapisz” go nie
  mają.
- **Reguły 9 i 10:** pusty stan z jednym działaniem. Po zapisie widać zapisany znicz i jego arkusz.
- **Reguła 11:** karty z chevronem w wyszukiwarce, wiersze w arkuszu grupy; bez miniatur.
- **Reguła 12:** koło zębate → [[ustawienia]]; dolny pasek Mapa · Osoby · Drzewo na mapie, cmentarzu i grobie (od
  ISSUE-022), ukryty w wyszukiwaniu, oknie i trybie wskazania.
- **Reguła 13 (mapy):** role kolorów na mapie, znicz-pinezka i **znicz w obrysie dla cmentarza jeszcze nie
  dodanego** (podgląd). Od v1.13: woda, sąsiedzi, granica Polski w kolorze tekstu pomocniczego; od v1.20 podpisy mapy rosną
  z tekstem najwyżej do 1,3× (D32).
- **Reguła 14 (zdjęcia):** miniatura cmentarza 96 × 80 dp, promień 12, przycięta ze środka; bez zdjęcia pole „Dodaj
  zdjęcie” jako przycisk (obrys 3,10:1 na powierzchni, ikona w akcencie 8,04:1, podpis 10,02:1), nigdy zastępczy obrazek.
- **Tokeny wchodzące tą pozycją** (zmierzone w [[style-b]] → *Measurement*; do `theme.dart` wpisuje je
  `dev`): **obrys** `#6B6862` (3,40:1 na tle, 3,10:1 na powierzchni) i **błąd** `#E07A6F` (6,45:1 i
  5,89:1, zawsze z ikoną). Błąd zapisu w karcie podglądu stoi na powierzchni, więc ma 5,89:1 (D23).
- **Ikona znicza**, jedna na całą aplikację:
  - **sylwetka:** szklany znicz (prostokąt lekko zwężony ku dołowi, z kołnierzem u góry) i płomień w kształcie
    kropli nad nim;
  - **wersja liniowa** (logo, ikona przycisku): kreska 1,5 dp w siatce 24 dp, jak ikony `outlined`;
  - **wersja wypełniona** (wnętrze pinezki): sylwetka w kolorze tła na bursztynowej pinezce.

## AC → element
| AC (bez prefiksu — ISSUE-014) | Element(y) | Jak widać spełnienie |
|---|---|---|
| Po starcie bez sieci widać mapę Polski, także pustą | 3, 5 · stan „pusty” | tryb samolotowy → start → kontur, miasta i rzeki; karta „Tu pojawią się cmentarze rodziny.” |
| Cmentarz z punktem jest zniczem; cmentarz bez punktu znajduje wyszukiwarka | 4 · 11 | zapis z punktem (z bazy albo wskazany) → znicz; zapis bez punktu → brak znicza, karta w 11 z „· bez punktu na mapie” |
| Wyszukiwarka znajduje po nazwie albo miejscowości; brak wyników → „Dodaj cmentarz” | 12, 13 | tekst z nazwy i z miejscowości daje karty w obu sekcjach; tekst bez trafień daje 13 |
| Arkusz pokazuje liczbę grobów i osób | 6 | „2 groby · 3 osoby” zgodne z danymi. Otwarcie ekranu cmentarza → ISSUE-012 (D5) |
| „Stan danych” pod kołem zębatym; ekranu startowego nie ma | 1 · *Navigation* | start → od razu mapa; koło → „Stan danych” (od ISSUE-022: koło → ustawienia → „Stan danych”) |
| Ekran według specyfikacji `ui` i wytycznych stylu B | całość | *Style B rules applied*; przegląd `ui` przed stopem #2 |
| US-002 AC-1, *Given* „cmentarz w aplikacji” | 12, 14, 15 | cmentarz dodany z bazy istnieje i ma arkusz |
| **Uwaga autora: właściwy cmentarz we właściwym miejscu** | 12, 14 | wynik z województwem i dzielnicą; podgląd na mapie i zdjęcie satelitarne przed dodaniem |
| (ISSUE-015) Bez sieci baza znajduje cmentarz po nazwie, nazwie dodatkowej i miejscowości; polskie znaki i końcówki odmiany niepotrzebne | 12 · D3 | tryb samolotowy → „powazki” → Cmentarz Powązkowski w sekcji „Z bazy cmentarzy”; „stare powazki” → ten sam przez nazwę dodatkową; „krakow rakowicki” → Cmentarz Rakowicki |
| (ISSUE-015) Wynik z bazy pokazuje miejscowość i województwo; ta sama nazwa w dwóch województwach to dwa rozróżnialne wyniki | 12 · D16 | każda karta z bazy ma „Miejscowość · woj. …” (w mieście z dzielnicą w nawiasie); „powazkowski” → dwie karty różniące się województwem |
| (ISSUE-015) Podgląd pokazuje cmentarz na mapie przed dodaniem; link otwiera zewnętrzną aplikację map w tym punkcie; bez dotknięcia nic nie wychodzi | 14 · D18, D19, D22 | karta z bazy → mapa przybliżona (w kadrze miasto, np. Wrocław przy Powązkowskim w Marczowie), znicz w obrysie, karta; „Zobacz zdjęcie satelitarne ↗” → Mapy Google (albo przeglądarka) w widoku satelitarnym w tym punkcie; bez aplikacji → „Nie ma aplikacji, która to otworzy.” Brak wysyłania przed dotknięciem nie jest widoczny na ekranie — sprawdza test |
| (ISSUE-015) Dodanie z bazy zapisuje nazwę (poprawioną albo z bazy), miejscowość i punkt z bazy; znicz na mapie; „Dodany” w wynikach | 14, 15 · 4, 6 · 12 · D23 | „Dodaj ten cmentarz” → okno nad podglądem z nazwą i miejscowością z bazy → zmiana nazwy (np. „Cmentarz na Górce”) → „Zapisz” → mapa z nowym zniczem i arkuszem z tą nazwą; ponowne wyszukanie → „Dodany” zamiast chevronu, dotknięcie → jego arkusz |
| (ISSUE-015) Podpis ODbL przy wynikach z bazy; wyciąg w repo z licencją i pochodzeniem | 12 · D16 | „Dane: © autorzy OpenStreetMap (ODbL)” pod sekcją „Z bazy cmentarzy”. Licencja i pochodzenie wyciągu: n/a dla ekranu (README i nagłówek zasobu w repo) |
| (ISSUE-015) APK release bez uprawnienia `INTERNET` | n/a — mechanizm, nie element | na ekranie tego nie widać: link wychodzi przez inną aplikację (D18), a nie przez sieć Grobing. Sprawdza `aapt` na APK release |
| (ISSUE-015) Ekran według specyfikacji `ui` i wytycznych stylu B | całość (12–15) | *Style B rules applied*; przegląd `ui` przed stopem #2 |
| (ISSUE-022) AC-1 — na dole Mapa · Osoby · Drzewo, aktywna Mapa; w formularzu osoby paska nie ma | 18 · *Navigation* | start → pasek z aktywną Mapą; arkusz nad paskiem; cmentarz i grób — pasek z aktywną Mapą; „Poprawa wpisu” bez paska; Osoby → wstecz → mapa |
| (ISSUE-022) AC-3 — koło zębate → ustawienia | 1 | koło → „Ustawienia” ([[ustawienia]]) |
| (ISSUE-023) AC-1 — sąsiednie kraje, Bałtyk, jeziora, „Polska” i 11 miast, bez sieci | 3 · D29, D32 | start → sąsiedzi w kolorze tła z cienkimi granicami, morze i jeziora w kolorze wody, rzeki, „Polska” na Mazurach, 11 podpisów bez nachodzenia (także 360 dp i tekst 200%) |
| (ISSUE-023) AC-2 — mapa jedzie nad arkusz i wraca na środek | 3, 4 · D26, D30 | bez arkusza środek Polski w środku obszaru mapy; znicz → płynna jazda, Polska nad arkuszem (na krótkim ekranie: wybrany znicz nad arkuszem); dotknięcie mapy, przeciągnięcie, wstecz → środek |
| (ISSUE-023) AC-3 — miniatura, podgląd ze zmianą i usunięciem | 6a · [[zdjecie]] (tryb cmentarza) · D33 | „Dodaj zdjęcie” → galeria → miniatura 96 × 80; miniatura → podgląd „Zdjęcie cmentarza” → „Zmień zdjęcie” → nowa; „Usuń zdjęcie” → okno C1 → arkusz z „Dodaj zdjęcie” |
| (ISSUE-023) AC-4 — kopia sprzed zmiany schematu: dane pełne, cmentarze bez zdjęć | 6a · stan „wybrany” | po odtworzeniu kopii v8 każdy arkusz ma pole „Dodaj zdjęcie”; liczby i dane bez zmian sprawdza test |
| (ISSUE-052) AC-1 — wynik przez okoliczną miejscowość mówi „przy: …” i stoi pod trafieniami w miejscowość karty | 12 · D35, D36 | „wymyslow” → karta „Cmentarz parafialny · Zmyślonka · przy: Wymyślów…”; cmentarze z miejscowością „Wymyślów” nad nią; „Wymyślów” wpisane w całości stawia całe słowo przed rdzeniem („Wymyślowice”) |
| (ISSUE-052, decyzja projektowa) — przed wyjazdem widać, które cmentarze mają plan w telefonie | 6, 11 · D37 | wyszukiwarka z pustym tekstem → karty bez planu mają „· bez planu”; arkusz → „Plan offline” albo linia z powodem braku |

## Decisions
- **D1 — plik przepisany w miejscu**, nazwa zostaje (linki w zamkniętych pozycjach).
- **D2 — podpowiedź „Szukaj cmentarza”** zamiast „Szukaj osoby lub cmentarza” z R1, bo pole nie szuka osób
  (decyzja autora: wyszukiwanie osób nie w ISSUE-014). ~~Tekst z R1 wraca z wyszukiwaniem osób.~~ Zmienione przez
  D27: tekst zostaje na stałe.
- **D3 — szukanie bez wielkości liter i polskich znaków, a słowa od 5 liter bez dwóch ostatnich**
  („powazki” → „Powązkach”, „Powązkowski”). Zmierzone na wyciągu: polska odmiana i potoczne nazwy psują
  dopasowanie całych słów. Szukanie obejmuje też nazwy dodatkowe z bazy (potoczne, oficjalne). *Obali:*
  zbyt wiele fałszywych trafień przy krótkich słowach — wtedy próg 6 liter.
- **D4 — pusty tekst pokazuje wszystkie twoje cmentarze**, także bez punktu (jedyna droga do nich, AC-2).
- **D6 — ręczne dodanie jest zapasem**, a nie główną drogą: okno + wskazanie z „Zapisz bez punktu”. Na
  wypadek cmentarza, którego nie ma w bazie, i nowych cmentarzy (baza to stan na dzień wyciągu).
- **D7 — poprawa przez ikonkę edycji w prawym górnym rogu arkusza** (decyzja autora). Tylko w arkuszu, a nie
  na kartach wyszukiwarki: karta prowadzi do arkusza, więc jedna droga wystarcza. Poprawia nazwę,
  miejscowość i punkt. Bez tego źle wybrany cmentarz albo literówka zostają na zawsze (usuwania nie będzie,
  brief G7/C5).
- **D8 — znicze, które na siebie nachodzą, łączą się w jeden znicz z liczbą.** Cała Polska to ok. 700 km na
  ok. 330 dp, więc cel 48 dp to ok. 100 km. Arkusz grupy działa także wtedy, gdy cmentarze leżą obok siebie
  i nie rozdzieli ich żadne przybliżenie (D21).
- ~~**D9 — tylko Polska:** bez sąsiednich krajów, 9 miast wojewódzkich, rzeki jako dekoracja. *Obali:*
  cmentarz za granicą.~~ Zastąpione przez D29 (v2.4): autor wybrał na prototypie mapę jak R1.
- **D10 — bez „tu jesteś” i bez uprawnienia lokalizacji** na tym ekranie.
- **D11 — po zapisie mapa z nowym zniczem i arkuszem**, a nie od razu ekran cmentarza. Widać, gdzie
  cmentarz stanął.
- **D12 — [[NFR-004-czytelnosc-w-sloncu]] nie rozstrzyga się tutaj.** Mapę Polski czyta się przy wyborze,
  dokąd jechać. Nazwa ma kolor tekstu (10,0:1), miejscowość i liczby — pomocniczy (5,0:1, AA). Miara zapada
  przy pierwszym ekranie wizyty — mapie cmentarza z pinezkami ([[EPIC-002-wizyta]]), a nie przy [[cmentarz]]
  w ISSUE-012, który jest ekranem przepisywania w domu ([[cmentarz]] D8, 2026-10-07).
- **D13 — liczba osób w arkuszu = różne osoby z pochówkiem w grobach tego cmentarza** (osoba z dwoma
  sprzecznymi pochówkami na tym cmentarzu liczy się raz).
- **D14 — odwzorowanie Merkatora, północ u góry, bez obrotu.**
- **D15 — dla planu:** wymyślone dane w buildzie debug dostają wymyślone punkty w Polsce, w tym dwa w jednym
  miejscu i jeden bez punktu.
- **D16 — baza cmentarzy Polski z OpenStreetMap, wbudowana w aplikację** (decyzja autora po falsyfikatorze:
  8 z 8 cmentarzy autora jest w bazie). Działa bez sieci, a aplikacja dalej nie ma uprawnienia `INTERNET`.
  Licencja ODbL wymaga podpisu i wyraźnego oznaczenia licencji, więc pod sekcją wyników jest „Dane: © autorzy
  OpenStreetMap (ODbL)”, brzmienie z [polskiej strony praw autorskich OSM](https://www.openstreetmap.org/copyright/pl)
  (ISSUE-015 → D3). **Miejscowość według D9 [[ISSUE-014-home-map-of-poland]]**, bez granic administracyjnych
  (ISSUE-015 → D4):
  - do wyświetlenia **najbliższa z uwzględnieniem rangi** (zasięg: miasto 12 km, miasteczko 5 km, wieś 2,5 km,
    przysiółek 1,5 km);
  - **dzielnica w nawiasie**, gdy miejscowość to miasto albo miasteczko, a dzielnica leży bliżej niż 2,5 km;
  - do szukania **wszystkie miejscowości w zasięgu**;
  - województwo z Natural Earth.
  
  Zmierzone na 8 cmentarzach autora: sama najbliższa miejscowość była zła w 3 z 8, a z rangą jest dobra w
  **7 z 8 do wyświetlenia** (odstępstwo: dzielnica miasta zapisana w OSM jako wieś), **8 z 8 do znalezienia** i
  **8 z 8 województw**. Granice gmin to ciężkie dane bez zysku w pomiarze. *Obali:* baza nie znajduje
  cmentarzy z kolejnych notatek — wtedy ręczne dodanie przestaje być zapasem; kolejne cmentarze z miejscowością,
  której nie da się znaleźć — wtedy wraca pytanie o granice gmin.
- **D17 — dwie sekcje wyników: najpierw „Twoje cmentarze”, potem „Z bazy”.** Wyszukiwarka służy też do
  otwierania zapisanych, a te są ważniejsze od 16 tys. obcych. Cmentarz z bazy, który już masz, jest oznaczony
  „Dodany”, żeby nie dodać go dwa razy.
- **D18 — podgląd przed dodaniem i link „Zobacz zdjęcie satelitarne ↗” do Map Google.** W bazie są błędy
  (zmierzone: cmentarz o nazwie warszawskiego cmentarza przy wsi w innym województwie), a nazwy miejscowości się
  powtarzają (zmierzone: jedna z miejscowości cmentarzy autora występuje w Polsce 5 razy), więc wybór z samej
  nazwy nie daje pewności. Kontur kraju nie pokaże cmentarza z bliska. Pokaże go zdjęcie satelitarne poza
  aplikacją, tak jak link do Grobonetu (brief §Security: strona zewnętrzna w przeglądarce).
  - **Adres** (decyzja autora, stop #1 [[ISSUE-015-add-cemetery-from-database]] → D1):
    `https://www.google.com/maps/@?api=1&map_action=map&center=<lat>,<lon>&zoom=17&basemap=satellite`. Otwiera
    Mapy Google w widoku satelitarnym, a bez nich przeglądarkę ([Google Maps URLs](https://developers.google.com/maps/documentation/urls/get-started):
    `basemap=satellite`). Intencja `geo:` z wersji 2 odpada: nie ma parametru warstwy ([Android — intencje Map
    Google](https://developer.android.com/guide/components/google-maps-intents): tylko `z` i `q`), więc podpis
    obiecywałby coś, czego link nie daje.
  - **Koszt prywatności bez zmian:** dotknięcie wysyła do Google punkt publicznego cmentarza z bazy, a nie dane
    rodziny — tylko wtedy, gdy dotkniesz. Nowy koszt: link zależy od jednego dostawcy.
  - **Brak aplikacji, która otworzy adres** (ISSUE-015 → D2): pasek komunikatu na dole „Nie ma aplikacji,
    która to otworzy.”, podgląd zostaje. **Sam tekst, bez ikony:** to fakt o telefonie, a nie błąd (reguła 7),
    kolor błędu należy tylko do błędu pola ([[style-b]] → *Token roles*), a informację niesie tekst, nie kolor
    (SC 1.4.1). Pasek ma domyślne kolory motywu, jak w „Stan danych”: tło w kolorze tekstu, napis w kolorze
    powierzchni (10,02:1).
  - *Obali:* autor nie chce linku do Google — wtedy intencja `geo:` z podpisem „Pokaż w aplikacji map ↗”
    (warstwę przełącza się w aplikacji map). Autor nie chce żadnego wyjścia z aplikacji — wtedy link znika, a
    zostaje województwo, dzielnica i wyznanie.
- **D19 — znicz w obrysie** w podglądzie: cmentarz jeszcze nie jest twój, więc nie wygląda jak zapisany.
- **D20 — nazwa z bazy do poprawy przed zapisem.** Baza często ma tylko „Cmentarz parafialny”. Nazwę, której
  używasz (np. „Cmentarz na Górce”), wpisujesz w oknie. Cmentarz bez nazwy dostaje puste pole z podpowiedzią.
- **D21 — zespół cmentarzy to kilka cmentarzy w aplikacji.** Baza ma osobne cmentarze różnych wyznań przy
  jednej ulicy (zmierzone: jeden wpis notatek = 4 obiekty). Grób należy do konkretnego cmentarza, a blisko
  położone połączą się na mapie w znicz z liczbą (D8). *Obali:* autor chce jednego cmentarza „zespół przy
  ul. X” — wtedy dodaje go ręcznie albo z jednego obiektu i poprawia nazwę.
- **D22 — podgląd przybliża o 1,5 stopnia ponad całą Polskę** (ok. 2,8×, ok. 240 km szerokości kadru), a nie
  o 3 jak wybór własnego cmentarza z wyszukiwarki. Mapa podglądu ma powiedzieć, **gdzie w Polsce** leży
  cmentarz: z bliska pokaże go dopiero zdjęcie satelitarne (D18). Mapa zna tylko 9 miast, więc miarą jest
  odsetek cmentarzy z bazy, przy których w kadrze stoi co najmniej jedno miasto. Zmierzone na wyciągu
  (16 040 cmentarzy, kadr podglądu na `Medium_Phone`, przegląd `ui` 2026-10-07):

  | Przybliżenie ponad całą Polskę | Szerokość kadru | Miasto w kadrze |
  |---|---|---|
  | +3 (wersja 2.1) | ok. 84 km | 29% |
  | +2,5 | ok. 120 km | 50% |
  | +2 | ok. 170 km | 78% |
  | **+1,5** | **ok. 240 km** | **96%** |
  | +1 | ok. 340 km | 100% |

  Przy +3 drugi Cmentarz Powązkowski, ten przy Marczowie w woj. dolnośląskim (błąd w bazie z D18), był
  samotnym zniczem na gładkim lądzie. Przy +1,5 w kadrze są Wrocław i Poznań, więc od razu widać, że to nie
  Warszawa. Wybór własnego cmentarza zostaje przy +3, bo swoje cmentarze znasz. *Obali:* na telefonie o innym
  kadrze miasto przestaje się mieścić — wtedy przybliżenie liczone tak, żeby w kadrze stało najbliższe z 9
  miast.
- **D23 — okno z bazy nad podglądem; błąd zapisu w karcie podglądu** (przegląd `ui`, 2026-10-07). W wersji
  2.1 „Dodaj ten cmentarz” zamykało wyszukiwarkę i podgląd, a okno stawało nad mapą całej Polski. „Anuluj”
  kasował wtedy wyniki, a błąd zapisu kasował poprawioną nazwę. Teraz:
  - okno stoi nad podglądem, czyli nad tym cmentarzem, a „Anuluj” wraca do podglądu, a stamtąd do wyników z
    tym samym tekstem;
  - błąd zapisu wygląda jak w trybie wskazania (element 17): `error_outline` i tekst w kolorze błędu, w karcie
    nad „Dodaj ten cmentarz”;
  - tryb zostaje: ponowne „Dodaj ten cmentarz” otwiera okno z wpisanymi wartościami;
  - zapis prowadzi do mapy z nowym zniczem i arkuszem, jak wcześniej (D11).

  Ręczne dodanie i poprawa bez zmian: okno nad mapą.
- **D24 — podpowiedź o limicie nad wynikami.** „Pokazuję 30 z N — dopisz miejscowość.” stoi pod nagłówkiem
  „Z bazy cmentarzy”, nad pierwszą kartą. Pod 30. kartą widać ją było dopiero po ok. 5 ekranach przewijania,
  a to ona mówi, jak zawęzić wyniki (zrzut z przeglądu: „parafialny” → 30 z 3740). Podpis ODbL i „Nie ma go
  w bazie — dodaj ręcznie” zostają pod sekcją.
- **D25 — separator nie kończy linii.** Linia „Miejscowość · woj. … · wyznanie” łączy części przez „ · ” ze
  spacją twardą po kropce. Przy zawinięciu nowa linia zaczyna się od „· rzymskokatolicki”, jak w szkicu, a
  poprzednia nie kończy się wiszącą kropką. W podglądzie (14) wyznanie stoi w osobnej linii, bez kropki.
- **D26 — dolny pasek na ekranie głównym** (v2.3, [[SPIKE-004-mvp-flow-prototype]] D1–D2). Autor potwierdził na
  prototypie zakładki z R1 i koło zębate dla ustawień. Pasek zostaje na ekranach do oglądania, więc arkusz cmentarza
  stoi nad nim. *Obali:* arkusz nad paskiem zasłania południe Polski na małym telefonie — wtedy arkusz niższy
  (miniatura obok nazwy już oszczędza linię).

  **Falsyfikator się zapalił** (przegląd `ui` [[ISSUE-023-poland-map-r1-cemetery-photo]], 2026-10-12, zrzuty build release):
  - **360 × 640 dp:** obszar mapy ok. 388 dp, arkusz ok. 235 dp (nazwa w dwóch liniach). Zapas na arkusz w najmniejszym
    przybliżeniu zmniejszył Polskę do ok. 145 dp szerokości, a podpisy nachodzą (Bydgoszcz na Białystok, „Polska” na Gdańsk);
  - **„niższy arkusz” tego nie naprawi:** Polska na całą szerokość (328 dp) ma ok. 312 dp wysokości, więc z marginesami
    zostaje ok. 44 dp na arkusz. Najniższy możliwy arkusz (uchwyt, wiersz z miniaturą 80 dp, „Otwórz cmentarz” 52 dp) ma ok.
    190 dp.

  **Reguła (v2.6): najmniejsze przybliżenie nie zależy od arkusza** — cała Polska z marginesem 16 dp (na pionowym ekranie
  wyznacza je szerokość), na środku obszaru mapy. Arkusz zmienia tylko położenie mapy, nigdy jej przybliżenie.
  - **411 × 914:** Polska mieści się nad arkuszem, a mapa jedzie tak jak w D30.
  - **360 × 780 i 360 × 640:** Polska ma całą szerokość i stoi na środku. Po otwarciu arkusza mapa podnosi Polskę najwyżej
    tak, by jej góra stała 16 dp pod wyszukiwarką. Gdy wybrany znicz dalej byłby pod arkuszem, działa reguła znicza z
    elementu 4: znicz staje na środku miejsca nad arkuszem, także w poziomie, i bez jazdy, jak przy przybliżonej mapie.
    Południe może zostać pod arkuszem — tak samo jak przy tekście 200% na każdym telefonie.
  - Prostokąt danych mapy liczono dla tego przybliżenia, więc przy przeciąganiu brzeg danych nie wychodzi.

  Zbudowane w ISSUE-023 i sprawdzone na zrzutach przeglądu: Polska ma 328 dp na 360 × 640, podpisy się nie nakładają, a znicz
  stoi nad arkuszem. Pierwsza wersja tej reguły mówiła o „zapasie z górną granicą”; daje on to samo przybliżenie, więc
  zostało prostsze brzmienie.

  *Obali:* na krótkim telefonie nie da się wybrać cmentarza, bo arkusz zasłania za dużo — wtedy na krótkim ekranie arkusz
  zwinięty do nazwy i „Otwórz cmentarz”, a miniatura po rozwinięciu.
- **D27 — wyszukiwarka na mapie szuka tylko cmentarzy, na stałe** (v2.3, [[SPIKE-004-mvp-flow-prototype]] D3). D2
  zakładało, że tekst z R1 wróci z wyszukiwaniem osób. Autor wybrał podział: każda zakładka szuka swojego, a osoby
  szuka zakładka Osoby.

- **D28 — zdjęcie cmentarza w arkuszu** (v2.4, [[SPIKE-004-mvp-flow-prototype]] D5). Autor chce w arkuszu własne
  zdjęcie cmentarza, a bez niego zaproszenie „Dodaj zdjęcie”. Miniatura jest jak w R1, a pole na wzór „Dodaj zdjęcie
  nagrobka” ([[grob]] D12). **Zmiana zakresu:** brief M1 ma zdjęcie nagrobka, a nie cmentarza, więc to decyzja
  autora i nowe pole w danych cmentarza. *Obali:* na liście cmentarzy w wyszukiwaniu autor też chce miniatur —
  wtedy reguła 11 jak w kartach grobów.
- **D29 — mapa Polski jak R1** (v2.4, [[SPIKE-004-mvp-flow-prototype]] D6, zastępuje D9). Autor porównał na
  prototypie wariant A (sama Polska) i B (sąsiedzi, Bałtyk, jeziora, rzeki w kolorze wody, „Polska”, 11 miast) i
  wybrał B: *„jest ok”*. Te same dane Natural Earth, bez sieci (ADR-007 bez zmian). Woda to nowa rola koloru
  ([[style-b]] v1.13). Granica Polski w kolorze tekstu pomocniczego, bo na wodzie obrys ma tylko 3,11:1. **Bez faktury
  terenu z R1** (lasy, rzeźba): ta wymaga danych rastrowych (ok. 1–3 MB, szacunek) i sprawdzenia czytelności
  zniczy i podpisów, a autor jej nie zażądał. *Obali:* po zbudowaniu B autorowi brakuje faktury — wtedy wariant C
  na prototypie.
- **D30 — Polska na środku bez arkusza, nad arkuszem z arkuszem** (v2.4, [[SPIKE-004-mvp-flow-prototype]] D7).
  Autor: *„powinna być bardziej wycentrowana (ale na widoku z otworzonym cmentarzem jest idealnie)”*. Margines dołu
  na wysokość arkusza (przegląd `ui` 2026-10-06) działa więc tylko przy otwartym arkuszu, a mapa przesuwa się do niego
  płynnie (ok. 300 ms).

  **Zbudowane w [[ISSUE-023-poland-map-r1-cemetery-photo]] (v2.6, przegląd `ui`):**
  - najmniejsze przybliżenie to cała Polska z marginesem 16 dp, takie samo z arkuszem i bez (D26);
  - jazda trwa 300 ms i zwalnia na końcu. Liczy ją **zmierzony arkusz** i kończy się, gdy dół Polski stoi 16 dp nad arkuszem,
    a gdy Polska się nie mieści — gdy jej góra stoi 16 dp pod wyszukiwarką (dalej D26);
  - palec na mapie zatrzymuje jazdę, „Usuń animacje” w systemie daje skok, a przy przybliżeniu działa reguła znicza (D2 planu).

  **Arkusz nie dokłada marginesu paska gestów** (stoi na pasku dolnym, który już ten margines trzyma). W pierwszej wersji
  ISSUE-023 pod „Otwórz cmentarz” było 44 dp zamiast 20, arkusz z miniaturą miał 214 dp zamiast 190, a stały zapas 214 dp w
  przybliżeniu zmniejszał Polskę na 360 × 780 do 298 dp zamiast 328 dp. Po poprawce arkusz ma 190 dp, dół 20 dp, a Polska na
  411 × 914 stoi 17 dp nad arkuszem (zrzuty przeglądu).
- **D31 — jak pasek przełącza zakładki** (v2.5, [[ISSUE-022-app-skeleton-tabs-people-settings]], przegląd `ui`).
  **Mapa zawsze leży na dole stosu** — to stały ekran startowy Androida (developer.android.com → *Principles of
  navigation*: *fixed start destination*), więc wstecz z Osób albo Drzewa wraca na mapę, a z mapy zamyka aplikację.
  Zakładka zdejmuje stos do mapy i kładzie swój ekran główny **bez wsuwania**, bo przełączenie zakładki nie jest krokiem
  w głąb. Zakładka na swoim ekranie głównym nic nie robi. **Zakładka bez gotowego ekranu prowadzi do zaślepki** z
  tekstem, kiedy powstanie (Drzewo → SPIKE-002; decyzja autora na stopie #1 ISSUE-022, D1 = A): pasek od razu ma
  kształt zatwierdzony na prototypie. Pamięć osobnego stosu każdej zakładki jest poza zakresem (stos od początku).
  *Obali:* autor wraca do Osób i oczekuje osoby, którą zostawił — wtedy osobny stos na zakładkę.
- **D32 — podpisy mapy i szczegóły R1** (v2.6, przegląd `ui` ISSUE-023, odstępstwa `dev` 1–4):
  - **podpisy mapy (miasta i „Polska”) rosną z tekstem systemu najwyżej do 1,3×** (miasto 17 sp), a znacznik podpisu rośnie
    razem z nimi. Od ISSUE-014 miał stałe 24 dp i przy 200% ucinał litery. Podpis jest przypięty do miasta i nie może się
    odsunąć, więc przy 200% podpisy zachodziły na siebie (Bydgoszcz na Białystok). Nazwy cmentarzy, czyli treść, która coś
    znaczy, rosną w pełni w arkuszu i wyszukiwarce ([[style-b]] reguła 13, v1.20);
  - **„Polska” stoi w punkcie 53,85° N, 21,0° E** (Mazury, między podpisami Gdańska, Bydgoszczy, Warszawy i Białegostoku) i
    **znika powyżej +2 kroków przybliżenia**. Nazwa kraju należy do najmniejszych przybliżeń (konwencja kartograficzna), a
    bliżej leżałaby na jednym regionie. Przy przybliżeniu stoi na jeziorach mazurskich bez obwódki i dalej jest czytelna:
    3,98:1 na lądzie i 4,02:1 na wodzie, duży tekst, próg 3:1;
  - **strony podpisów:** Katowice po lewej (podpis po prawej wchodziłby na kropkę Krakowa), **Białystok i Lublin pod
    kropką**, reszta po prawej. Białystok po lewej przy 360 dp i tekście 200% stał 4 dp od „Bydgoszcz” w tej samej linii
    i obie nazwy czytały się jak jeden napis (zrzut po poprawkach przeglądu). Pod kropką przy 100% na 411 dp wchodzi na
    kilka dp za wschodnią granicę; obwódka w kolorze lądu ma tam 1,10:1 do tła, więc tego prawie nie widać;
  - **brzegi morza u sąsiadów i brzegi jezior są bez linii.** Wodę od lądu odróżnia odcień, bo to dekoracja, a brzeg Polski
    niesie jej granica ([[style-b]] reguła 13);
  - **progi jezior:** w Polsce od 8 km², za granicą od 40 km². Mniejsze przy całej Polsce mają poniżej 2 dp.

  *Obali:* ktoś z dużym tekstem nie odczyta podpisów w 1,3× — wtedy 1,5× i mniej miast na wąskim ekranie. Autor nie widzi
  jezior przy całej Polsce (krok odczucia 1; woda i ląd mają 1,00:1, różni je tylko odcień, jak na prototypie) — wtedy woda
  jaśniejsza od lądu i nowy pomiar granicy Polski na wodzie.
- **D33 — arkusz z miniaturą** (v2.6, przegląd `ui` ISSUE-023, odstępstwa `dev` 5–6):
  - **nazwa zaczyna się przy górze miniatury** (2 dp od góry wiersza), bo górne krawędzie tekstu i obrazu tworzą jedną
    linię. Bez magazynu zdjęć zostaje 12 dp, jak dotąd;
  - **✎ ma środek ikony w linii pierwszej linii nazwy** (element 8), a cel zostaje 48 × 48 dp. W zbudowanej wersji przeglądu
    ikona stała ok. 10 dp niżej, bo nazwa podjechała, a ✎ nie (do poprawki);
  - **zapis bez słów:** w miejscu pola wskaźnik, a „Zapisuję zdjęcie…” słyszy czytnik. W [[zdjecie]] B tekst stoi, bo tam
    jest na niego miejsce;
  - **wczytywanie miniatury to samo tło, bez wskaźnika** (jak [[zdjecie]] v1.2). Na wolnym emulatorze po odtworzeniu kopii
    widać było przez chwilę pusty prostokąt; na telefonie miniatura dekoduje się w ułamku sekundy. *Obali:* na telefonie
    autora prostokąt miga — wtedy miniatura pojawia się łagodnie (ok. 150 ms), dalej bez wskaźnika;
  - **miniatura dekoduje się jak inne miniatury przycięte ze środka:** do dwukrotności szerokości pola. Zdjęcia cmentarzy są
    zwykle poziome, a pole 96 × 80 ma proporcje 1,2:1, więc zdjęcie dekodowane tylko na szerokość pola byłoby powiększane i
    rozmyte.
- **D34 — pobieranie planu bez śladu na mapie Polski** (v2.7, [[cmentarz]] D18, D20). Zapis cmentarza z punktem albo zmiana
  punktu uruchamia pobieranie planu, ale arkusz i znicz wyglądają jak dotąd. Mapa Polski służy do wyboru, dokąd jechać, a
  plan jest potrzebny dopiero w cmentarzu, gdzie [[cmentarz]] 2a mówi, co się z nim dzieje. *Obali:* autor dodaje cmentarz
  bez zasięgu i chce wiedzieć, czy plan już jest — wtedy w arkuszu linia „Plan offline” z ikoną. **Obalone 2026-10-22 → D37.**
- **D35 — „przy: …”, gdy słowo trafiło tylko w okolicę** (v2.8, [[ISSUE-052-cemetery-search-and-patient-plan]]; propozycja `ui` z
  [[ISSUE-015-add-cemetery-from-database]] → *Notes*). OSM przypisuje cmentarz do najbliższego miejsca według rangi (ISSUE-014 D9), więc
  cmentarz parafialny we wsi miał na karcie nazwę przysiółka, a wsi, którą autor wpisał, nie było nigdzie na ekranie — przy 51 wynikach
  nie dało się go rozpoznać. Pokazana jest **jedna** miejscowość, ta, w którą trafia najwięcej słów spoza karty: pierwsza wersja pomiaru
  brała pierwszą z listy z jednym trafionym słowem i pokazała sąsiednią wieś o podobnym początku zamiast tej wpisanej. Mianownik z bazy i
  dwukropek, bo „przy” z nazwą wymagałoby odmiany. *Obali:* autor czyta „przy:” jako „obok cmentarza stoi miejscowość X” i myli się co do
  miejsca — wtedy „okolica: …”.
- **D36 — kolejność wyników: całe słowa, potem bliskość pola, potem zwartość** (v2.8). Zbiór wyników bez zmian (D3), zmienia się kolejność.
  Kanon wyszukiwania: dokładne trafienie przed prefiksem, prefiks przed środkiem słowa, trafienie w jednym polu przed rozrzuconym (tak
  punktuje wyszukiwanie pełnotekstowe — dopasowanie frazy wyżej niż pojedyncze słowa). Pomiar na wbudowanej bazie 2026-10-22, pozycja
  przed → po (w 30 pokazanych?):

  | Zapytanie (opis — nazwy cmentarzy autora nie trafiają do vaulta) | Wyników | Przed | Po |
  |---|---|---|---|
  | wieś autora w mianowniku (cmentarz przypisany do przysiółka) | 51 | 25 | **2** |
  | ta sama wieś w miejscowniku, jak w nazwie parafii | 855 | 402 (nie) | **27** |
  | „parafialny” + wieś w miejscowniku | 339 | 86 (nie) | **13** |
  | „parafialny” + wieś w mianowniku | 22 | 4 | **1** |
  | wieś, której nazwa po obcięciu końcówki daje 3 litery | 186 | 102 (nie) | **4** |
  | miasto wojewódzkie, cmentarz z ulicą w nazwie, samo miasto | 60 | 47 (nie) | **14** |
  | ten cmentarz, sama ulica w mianowniku | 88 | 3 | 24 |
  | 8 cmentarzy autora, najprostsze słowo dla każdego | — | 6 z 8 w 30 | **8 z 8** |
  | regresja: „krakow” — cmentarze Krakowa przed „…Krakowcu” | 111 | — | Kraków pierwszy |
  | regresja: „powazki” | 5 | — | Powązkowski w Warszawie przed tym w Marczowie (dotąd odwrotnie) |
  | regresja: „parafialny” | 3740 | — | bez zmiany pierwszego wyniku |

  Koszt: ulica wpisana w mianowniku, a w nazwie odmieniona („przy ul. …ej”), spada z 3. na 24. miejsce, bo całe słowo trafia w wieś o tej
  nazwie; z nazwą miasta albo w miejscowniku jest pierwsza. *Obali:* przy prawdziwym cmentarzu wynik znów jest poza 30 — wtedy odmiana nazw
  miejscowości w bazie (miejscownik z wyciągu), osobną pozycją.
- **D37 — stan planu widać przed wejściem w cmentarz** (v2.8, decyzja projektowa w [[ISSUE-052-cemetery-search-and-patient-plan]]; spełnia
  *Obali* D34). Autor chce *„na 100% mieć je na wyjazd”*, a dziś sprawdziłby to tylko, otwierając każdy cmentarz. Arkusz mówi „Plan offline”
  albo powód braku tymi samymi słowami co [[cmentarz]] 2a; lista „Twoje cmentarze” mówi tylko o braku („· bez planu”), jak „· bez punktu na
  mapie” — lista ma pokazywać, co zostało do zrobienia. Stan „pobieram” i „bez internetu” są w pamięci aplikacji, więc po ponownym starcie
  arkusz bez zapisanego planu mówi „Bez planu — pobierze się sam.”, dopóki pobieranie nie ruszy. *Obali:* linia w arkuszu przeszkadza przy
  wyborze cmentarza, gdy wszystkie mają plan — wtedy w arkuszu tylko brak, jak na liście.
- **D38 — szczegóły z budowy [[ISSUE-052-cemetery-search-and-patient-plan]]** (v2.9, przegląd `ui` 2026-10-23):
  - **ikona linii planu 18 dp** (odstępstwo 2 `dev`). Linia planu stoi pod linią liczb i ma wyglądać jak ona, a ikona liczb ma 18 dp — v2.8
    podało przy tym 20 dp, czyli samo sobie przeczyło. Dwie ikony różnej wielkości jedna pod drugą wyglądałyby jak pomyłka; obie rosną z
    tekstem ([[style-b]] reguła 3);
  - **„przy: <miejscowość>” trzyma się razem** (`dev` → *Found on the emulator*: przy 200% dwuczłonowa nazwa łamała się w środku, a
    „przy: Wymyślona⏎Wola” czyta się jak dwie miejscowości). Twarda spacja po „przy:” trzyma dopisek przy nazwie ([[style-b]] reguła 6,
    v1.32), a twarde spacje między słowami — nazwę w jednej linii. **Granica:** napis bez miejsca na złamanie, dłuższy niż linia, Flutter łamie
    w środku słowa. Przy 200% na 360 dp w linii karty mieści się ok. 20 znaków (zrzut przeglądu), a ok. jedna czwarta z 29 164 nazw okolicznych
    miejscowości w bazie ma ponad 12 znaków (pomiar przeglądu na wbudowanej bazie). Dlatego nazwa, która razem z „· przy:” nie mieści się w
    linii, łamie się między swoimi słowami — nigdy w środku słowa. *Obali:* autor przy dużym tekście nie łączy nazwy złamanej między słowami z
    „przy:” — wtedy „przy: …” w osobnej linii karty.

## Open
brak. Rundy prototypu ([[SPIKE-004-mvp-flow-prototype]]) rozstrzygnęły zdjęcie w arkuszu (D28) i mapę (D29, D30).

Pytania z pierwszej wersji (wyszukiwanie osób, „Otwórz cmentarz” przed ekranem cmentarza) autor rozstrzygnął na
stopie #1 (*„teoretycznie jest ok”* — rekomendacje D4 i D5 planu).
