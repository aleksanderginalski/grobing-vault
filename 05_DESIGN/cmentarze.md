---
screen: "Ekran główny — mapa Polski z cmentarzami rodziny"
items: ["[[ISSUE-012-transcribe-grave-screen]]", "[[ISSUE-014-home-map-of-poland]]", "[[ISSUE-015-add-cemetery-from-database]]", "[[SPIKE-004-mvp-flow-prototype]]"]
us: "[[US-002-przepisanie-grobu]]"
journey-step: "UJ-001 · 1 (widok 1, M2) · warunek kroku 1: dodanie cmentarza (M1)"
mockup: "katalog tymczasowy sesji 2026-10-06: makieta-mapa-polski.html (ramki 1–10, wersja 2 po stopie #1) · 2026-10-08: grobing-prototyp.html (SPIKE-004, klikalny)"
updated: 2026-10-08
---

# Ekran główny — mapa Polski — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.5) · referencja: [[references]] → **R1**.
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
> Które elementy dowozi która pozycja, mówi plan (`planning`), a nie ten plik.

## Purpose
Zbierający otwiera aplikację i widzi, **na których cmentarzach w Polsce leży jego rodzina**, ze zniczem na
każdym. Wybiera, dokąd jechać albo który cmentarz przepisywać (UJ-001 krok 1, M2). Nowy cmentarz **wybiera
z bazy cmentarzy Polski**, żeby trafić we właściwy cmentarz we właściwym miejscu, a nie stawiać punkt na
oko (M1). Mapa i baza działają bez sieci od pierwszego uruchomienia: kontur, miasta i rzeki z Natural Earth,
a cmentarze z OpenStreetMap są wbudowane w aplikację.

## Navigation
- **Start aplikacji → ten ekran.** Ekran startowy z [[ISSUE-002-bootstrap-code-repo]] znika; natywny ekran
  uruchamiania (tło `grobing_background`) zostaje.
- **Koło zębate → „Stan danych”** (jedyne ustawienie; lista ustawień powstanie z drugą pozycją).
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
  i niżej, a wyszukiwanie, okno i tryb wskazania pasek chowają ([[style-b]] reguła 12). Do czasu zbudowania
  zakładek Osoby i Drzewo pasek czeka na drugi cel (reguła 12).

## Elements in order
**Mapa (ekran główny)**

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek: **ikona znicza (akcent) + „Grobing”** (półgruby, 22 sp); po prawej koło zębate (`settings_outlined`, tekst pomocniczy, `tooltip` „Ustawienia”) | pasek | koło → „Stan danych” | — | — | R1 · *What to build* 5 · [[style-b]] reguła 8 |
| 2 | **Wyszukiwarka:** pigułka na powierzchni, wys. 56 dp, margines 16 dp, ikona `search` (tekst pomocniczy), podpowiedź **„Szukaj cmentarza”** | pole (tylko wejście) | dotknięcie → tryb wyszukiwania (10) | pusto | — | R1 · *What to build* 3 · D2 |
| 3 | **Mapa Polski jak R1 (v2.4, D29)** na całą szerokość pod wyszukiwarką: **Polska** — ląd w kolorze powierzchni, granica w kolorze **tekstu pomocniczego** (1,4 dp; 5,01:1 na lądzie, 5,04:1 na wodzie, 5,50:1 na tle); **sąsiednie kraje** w kolorze tła z granicami w kolorze obrysu (0,7 dp, krycie 45%, dekoracja); **Bałtyk i jeziora** w kolorze **wody** (nowa rola, proponowany token `water` `#101C25`); **rzeki** linią wody (1 dp, proponowany token `waterLine` `#3A5E74`, dekoracja); napis **„Polska”** (22 sp, półgruby, odstęp liter 2, tekst pomocniczy, krycie 85%) w wolnym miejscu północnej części kraju; **11 miast** (kropka 4 dp + podpis 13 sp, tekst pomocniczy, z obwódką 2–3 dp w kolorze lądu — [[style-b]] reguła 13): Szczecin, Gdańsk, Bydgoszcz, Białystok, Poznań, Warszawa, Łódź, Wrocław, Katowice, Lublin, Kraków. Dane: Natural Earth 1:10m, te same co dziś. Bez faktury terenu | mapa | szczypanie, przeciąganie, podwójne dotknięcie; ruch ograniczony do Polski; najmniejsze przybliżenie = cała Polska z marginesem 16 dp, **wyśrodkowana w pionie w obszarze mapy, gdy arkusz jest zamknięty; po otwarciu arkusza mapa przesuwa się płynnie w górę, tak że Polska stoi nad arkuszem** (v2.4, D30); bez obrotu; dotknięcie pustego miejsca zamyka arkusz | cała Polska, północ u góry | — | R1 · *What to build* 1 · D14, D29, D30 |
| 4 | **Znicze cmentarzy** w punkcie cmentarza: pinezka w akcencie z sylwetką znicza w kolorze tła, 32 × 40 dp, **cel dotyku 48 × 48 dp**. Wybrany: 40 × 50 dp z poświatą. **Znicze, których cele nachodzą na siebie, łączą się w jeden znicz z liczbą** (plakietka: powierzchnia, obrys w akcencie, cyfra w kolorze tekstu). Znicz rysuje się nad podpisami miast | znaczniki | dotknięcie → arkusz (6) albo arkusz grupy (9); mapa przesuwa się tak, żeby znicz (także znicz z liczbą) nie stał pod arkuszem — według wysokości narysowanego arkusza | — | cmentarz bez punktu nie ma znicza | R1 · *What to build* 2 · AC-2 · D8 |
| 5 | **Stan pusty:** karta na powierzchni na dole: „Tu pojawią się cmentarze rodziny.” (tekst pomocniczy) + **wypełniony „Dodaj cmentarz”** (`add_location_alt_outlined`) | karta + przycisk główny | → tryb wyszukiwania (10) z podpowiedzią „Wpisz nazwę cmentarza albo miejscowość” | — | — | AC-1 · [[style-b]] reguła 9 · D16 |

**Arkusz cmentarza** — dolny arkusz na powierzchni do krawędzi ekranu (treść nad paskiem gestów), promień 16 dp, uchwyt: przeciągnięcie w dół zamyka arkusz jak dotknięcie mapy; mapa pod nim działa

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 6 | **Nazwa** (tekst, 18 sp, półgruby, do 2 linii) · **miejscowość** (tekst pomocniczy, 14 sp) · ikona `people_outline` + **„6 grobów · 14 osób”** (tekst pomocniczy, odmiana — [[style-b]] reguła 6). Bez punktu: ikona `location_off_outlined` + „Bez punktu na mapie” | tekst | — | — | — | R1 · *What to build* 4 · AC-4 · D13 |
| 6a | **Zdjęcie cmentarza (v2.4, D28)** z lewej, przed nazwą: zaokrąglony prostokąt **96 × 80 dp**, promień 12 dp, przycięty ze środka ([[style-b]] reguła 14). Nazwa, miejscowość i liczby stoją obok, a ✎ (8) zostaje w prawym górnym rogu. **Bez zdjęcia:** w tym samym miejscu pole **„Dodaj zdjęcie”** — obrys, ikona `add_a_photo_outlined` w akcencie, podpis 12 sp półgruby ([[style-b]] reguła 14: puste miejsce tylko jako przycisk). Zdjęcie robi autor; to treść użytkownika, bez filtrów | zdjęcie / przycisk | zdjęcie → zdjęcie cmentarza na pełnym ekranie ze „Zmień zdjęcie” i „Usuń zdjęcie”, jak [[zdjecie]] przy nagrobku; „Dodaj zdjęcie” → wybór źródła „Wybierz z galerii” · „Zrób zdjęcie” ([[zdjecie]]) → zdjęcie w arkuszu | brak zdjęcia | — | R1 (miniatura w arkuszu) · **decyzja autora** (SPIKE-004 D5) · D28 |
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
| 11 | **Pusty tekst:** sekcja **„Twoje cmentarze”** — wszystkie zapisane jako karty (nazwa 16 sp półgruby · „Miejscowość · 3 groby · 6 osób”, a bez punktu „· bez punktu na mapie” · chevron). Bez zapisanych cmentarzy: „Wpisz nazwę cmentarza albo miejscowość.” (tekst pomocniczy) | lista kart | karta → mapa: wyjście z wyszukiwania, przybliżenie do znicza, arkusz otwarty | alfabetycznie, polskie sortowanie | — | AC-2 · D4 |
| 12 | **Wyniki (od 2 znaków)** w dwóch sekcjach. **„Twoje cmentarze”** — karty jak w 11, które pasują; bez trafień tej sekcji nie ma, także nagłówka. **„Z bazy cmentarzy”** — karty: **nazwa** (16 sp, półgruby; brak nazwy → „Cmentarz bez nazwy” w kolorze pomocniczym) · **„Miejscowość · woj. mazowieckie”**, w mieście albo miasteczku z dzielnicą w nawiasie (D16), i „· rzymskokatolicki”, gdy baza zna wyznanie (tekst pomocniczy) · chevron. Części linii łączy „ · ” ze spacją twardą po kropce, więc zawinięta linia zaczyna się od „·” i żadna nie kończy się kropką (D25). Cmentarz z bazy, który już jest u Ciebie (punkt bliżej niż 100 m), ma zamiast chevronu „Dodany” (tekst pomocniczy, wyrównany do kolumny chevronów) i prowadzi do jego arkusza. Najwyżej 30 wyników z bazy; przy większej liczbie **pod nagłówkiem sekcji, nad pierwszą kartą**, stoi „Pokazuję 30 z 214 — dopisz miejscowość.” (14 sp, tekst pomocniczy, D24). Pod sekcją: „Dane: © autorzy OpenStreetMap (ODbL)” (13 sp, tekst pomocniczy). Na końcu przycisk tekstowy **„Nie ma go w bazie — dodaj ręcznie”**. Między sekcjami 24 dp ([[style-b]] reguła 5) | dwie listy kart + przycisk tekstowy | karta z bazy → podgląd (14); „dodaj ręcznie” → okno (15) z nazwą = tekst | twoje alfabetycznie; z bazy: najpierw trafienia w nazwie, potem w miejscowości, w grupie alfabetycznie | — | AC-3 · D3, D16, D17, D24, D25 |
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
| 18 | **Pasek dolny** na powierzchni, wys. 72 dp, linia podziału u góry w kolorze obrysu: trzy zakładki **Mapa** (`map_outlined`) · **Osoby** (`group_outlined`) · **Drzewo** (`account_tree_outlined`), ikona nad podpisem (12 sp, półgruby). Aktywna: ikona, podpis i podkreślenie 2 dp w akcencie; nieaktywne w kolorze tekstu pomocniczego. Arkusz cmentarza (6–8) i arkusz grupy (9) stoją **nad** paskiem | nawigacja | zakładka → jej ekran główny, stos zakładki od początku | Mapa | — | R1 · [[style-b]] reguła 12 · D26 |

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
 arkusz cmentarza (ikonka edycji w prawym górnym rogu)
┌──────────────────────────────────┐
│ ═══                              │
│ Cmentarz Wymyślony 1          ✎ │
│ Miejscowość Testowa              │
│ 👥 2 groby · 3 osoby             │
└──────────────────────────────────┘
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
- **Reguła 12:** koło zębate → „Stan danych”; bez dolnej nawigacji.
- **Reguła 13 (mapy):** role kolorów na mapie, znicz-pinezka i **znicz w obrysie dla cmentarza jeszcze nie
  dodanego** (podgląd).
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
| „Stan danych” pod kołem zębatym; ekranu startowego nie ma | 1 · *Navigation* | start → od razu mapa; koło → „Stan danych” |
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

## Open
brak. Rundy prototypu ([[SPIKE-004-mvp-flow-prototype]]) rozstrzygnęły zdjęcie w arkuszu (D28) i mapę (D29, D30).

Pytania z pierwszej wersji (wyszukiwanie osób, „Otwórz cmentarz” przed ekranem cmentarza) autor rozstrzygnął na
stopie #1 (*„teoretycznie jest ok”* — rekomendacje D4 i D5 planu).
