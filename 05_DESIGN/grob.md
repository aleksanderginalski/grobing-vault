---
screen: "Grób — wszyscy pochowani"
items: ["[[ISSUE-012-transcribe-grave-screen]]", "[[ISSUE-016-photos-grave-and-person]]", "[[ISSUE-017-person-photos]]", "[[ISSUE-018-profile-photo-crop]]", "[[SPIKE-004-mvp-flow-prototype]]", "[[ISSUE-024-person-view]]", "[[ISSUE-028-cemetery-sectors]]", "[[ISSUE-029-pin-on-site-gps]]", "[[ISSUE-043-grave-paid-until]]", "[[ISSUE-047-grave-first-then-people]]"]
us: "[[US-002-przepisanie-grobu]] · [[US-005-zdjecia]] · [[US-008-pinezka-na-miejscu]] · brief §5 S4 (ISSUE-043, bez US)"
journey-step: "n/a — M1; ten sam widok stanie się widokiem 3 (krok 4 UJ-001, M4, R4 lewy) — wizyta dojdzie tutaj"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-cmentarz-grob-osoba.html (ramki 5–7, ISSUE-012) · makieta-zdjecia.html (ramki 1, 2, 4, ISSUE-016) · 2026-10-12: issue-028-kwatery.html (panel 4 — adres grobu, W-a/W-b) · 2026-10-12: issue-029-pinezka.html (panel 2 — „Postaw pinezkę”, linia źródła) · v8 (ISSUE-043): n/a — zmiana istniejącego ekranu, warianty W1/W2 w szkicu ASCII · 2026-10-18: makieta-047.html (ISSUE-047 — pusty grób, wybór osoby, ekrany 3–5)"
updated: 2026-10-18
---

# Grób — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.32) · referencja: [[references]] → **R4 (lewy
> ekran)**.
>
> **Wersja 2 (2026-10-07, przed planem ISSUE-012)** — według decyzji autora z 2026-10-06
> ([[ISSUE-012-transcribe-grave-screen]] → *Input from the author*): **grób jak R4 z nazwą grobu.** Zmiany
> względem wersji 1: tytułem jest **nazwa grobu** (nowe pole, migracja v2→v3), ikonka edycji z oknem „Popraw
> grób” (element 3), miejsca na zdjęcie i portrety opisane jako kierunek [[US-005-zdjecia]] (D4). Dawne *Open*
> 1 rozstrzygnięte (D1).
>
> **Wersja 2.1 — przegląd `ui` zbudowanego ekranu (2026-10-07):** poprawa wpisu wchodzi (stop #1 ISSUE-012, D1),
> więc karta osoby zawsze ma chevron i prowadzi do poprawy, a wyjątek z D3 nie zachodzi (biografię widać w
> poprawie). „Dodaj osobę” ma szerokość treści i stoi z lewej (element 6). Odstęp nagłówek → lista: 24 dp. Osoba
> bez imion i nazwiska (tylko z innych danych): „Osoba bez imienia”. **Data pochówku** (`· poch. …`) pokazuje się
> tylko wtedy, gdy przyszła z innych danych: od stopu #2 formularz jej nie wpisuje ([[wpis-osoby]] v2.2).
>
> **Wersja 3 (2026-10-07, [[ISSUE-016-photos-grave-and-person]]) — zdjęcie nagrobka, jak w R4:** **jedno**
> zdjęcie nad tytułem (element 1a), „Dodaj zdjęcie” obok „Dodaj osobę”, dopóki grób nie ma zdjęcia (element 6);
> zmiana i usunięcie w podglądzie. Wybór źródła i podgląd: [[zdjecie]]. **Decyzje autora na stopie #1** (rundy 1–2):
> *„nagrobek — wystarczy mi jedno zdjęcie”*, a zdjęcia osób jako baza zdjęć z „profilowym” — to
> [[ISSUE-017-person-photos]]. **Miniatury osób w kartach (element 5) to kierunek dla ISSUE-017**, nie wchodzą w
> ISSUE-016.
>
> **Wersja 3.1 (2026-10-07, przegląd `ui` zbudowanego ekranu):** stan „wczytywanie zdjęcia” (pole 4:3 bez
> wskaźnika — tytuł i osoby nie zjeżdżają, gdy zdjęcie się pojawi); zdjęcie z galerii to 4 dotknięcia (okno
> systemowe wymaga „Gotowe”); zmierzone, ile osób mieści się nad zgięciem (*Tempo*, D8).
>
> **Wersja 3.2 (2026-10-07, stop #2 ISSUE-016 — decyzja autora):** *„dodaj zdjęcie powinno być domyślnie na polu
> przeznaczonym dla zdjęcia”*. Grób bez zdjęcia ma nad tytułem **pole „Dodaj zdjęcie nagrobka”** (element 1a, D12),
> a rząd działań ma już tylko „Dodaj osobę”.
>
> **Wersja 4 (2026-10-07, przed planem [[ISSUE-017-person-photos]]) — miniatury osób.** Kierunek z v3 (element 5, D11)
> wchodzi bez zmian kształtu. Miniatura w karcie to **profilowe** osoby, czyli pierwsze łącze
> ([[zdjecia-osoby]]). Zdjęcia osoby dodaje się i zmienia w formularzu osoby ([[wpis-osoby]] v4, element 1a), a nie
> tutaj, więc widok grobu nie dostaje nowych działań.
>
> **Wersja 4.1 (2026-10-07, przed planem [[ISSUE-018-profile-photo-crop]]):** miniatura w karcie (element 5) pokazuje
> profilowe **w kadrze** z [[kadr-profilowego]]; bez kadru — jak dotąd, ze środka. Bez nowych działań.
>
> **Wersja 5 — discovery na prototypie, panel 3 ([[SPIKE-004-mvp-flow-prototype]] D13, 2026-10-08):** widok grobu
> zostaje jak zbudowany (autor: *„1 ok”*). Zmieniają się dwie rzeczy:
> - **karta osoby otwiera widok osoby** ([[osoba]], panel 4), a nie formularz poprawy ([[style-b]] reguła 15,
>   SPIKE-004 D4; autor: *„2 ok”*). Poprawa jest pod ✎ w widoku osoby;
> - **dolny pasek** Mapa · Osoby · Drzewo jest widoczny, a aktywna jest zakładka, z której przyszedł autor
>   ([[style-b]] reguła 12).
>
> **Wersja 5.1 — wizyta ([[SPIKE-004-mvp-flow-prototype]] D22, 2026-10-08):** grób bez pinezki ma pod adresem przycisk z
> obrysem **„Postaw pinezkę”** (`add_location_alt` w akcencie) → mapa cmentarza w trybie stawiania pinezki ([[cmentarz]]
> element 12). Grób z pinezką ma pod adresem jej źródło: „Pinezka: GPS ±4 m · 08.10.2026” (13 sp, tekst pomocniczy).
>   ([[style-b]] reguła 12).
>
> **Wersja 6 — przyjęta na stopie #1 [[ISSUE-028-cemetery-sectors]] (2026-10-12, autor: „tak”; pole „Kwatera” w wariancie W-a).**
> Poniżej pierwotny opis propozycji. Dopiski „propozycja” w elementach 3b, 4 i D13 są nieaktualne — v6 obowiązuje. Adres zarządcy w oknie „Popraw
> grób”. Kolumny kwatery, rzędu i miejsca są w schemacie od v1, ale **żaden ekran ich nie zapisuje**, więc „Uzupełnisz przy
> wizycie” obiecuje coś, czego aplikacja nie umie ([[cmentarz]] → *Open*). Zmiany: okno 3a z polami Kwatera · Rząd · Miejsce,
> element 4 z „Wpisz adres”, D13. Pole kwatery zależy od decyzji W-a/W-b ([[cmentarz]] → *Open*). Gdy autor zdecyduje, że adres
> idzie osobną pozycją, ta wersja przechodzi do niej bez zmian.
>
> **Wersja 7 (2026-10-12, przed planem [[ISSUE-029-pin-on-site-gps]]) — pinezka.** Element 4 z v5.1 wchodzi do kodu:
> - grób bez pinezki ma pod adresem (i pod „Wpisz adres”, gdy adresu nie ma) **„Postaw pinezkę”** → tryb D [[cmentarz]] (12);
> - grób z pinezką ma pod adresem **źródło i datę**: „Pinezka: GPS ±4 m · 12.10.2026”, „Pinezka: postawiona na planie · …” albo
>   „Pinezka: postawiona na zdjęciu z góry · …” ([[cmentarz]] 14, D33 — źródło to to, z czego wzięła się pozycja).
>
> Poprawa pinezki jest tylko na mapie ([[cmentarz]] 11) — tu bez drugiego wejścia (D14).
>
> **Wersja 8 (2026-10-16, przed planem [[ISSUE-043-grave-paid-until]]) — „Opłacone do”.** Zakres według decyzji autora w `/pm`
> (wariant B): **sama data**, bez „kto płaci” i bez przypomnienia. Przypomnienie przyjdzie później aktualizacją ze sklepu, bo bazy nie
> zmienia. Zmiany:
> - **na samym dole widoku, pod „Dodaj osobę”, jest wiersz „Opłacone do”** (element 7, D15). Autor: *„można dodać na samym dole profilu grobu”*;
> - **grób bez daty** ma w tym wierszu „nie wiadomo” i przycisk „Wpisz” (W1, D16). **Przyjęte na stopie #1 (autor: „Tak”, 2026-10-16)**;
>   wariant bez wiersza (W2) został w szkicu jako odrzucony;
> - **okno „Popraw grób”** ma na końcu pole „Opłacone do” (3c). Pole przyjmuje lata z przyszłości (D18);
> - **bez stanu „bez terminu” i bez oznaczenia opłaty, która minęła** (D19).
>
> **Wersja 8.1 (2026-10-16, przegląd `ui` zbudowanego ekranu [[ISSUE-043-grave-paid-until]]) — dwa odstępstwa `dev` przyjęte:**
> - **okno samo przewija się do 3c** (D20). Przy fokusie w „Opłacone do”, przy zmianie wysokości klawiatury i przy błędzie pole z etykietą staje
>   u góry widocznej części okna, 16 dp pod jej krawędzią. Specyfikacja mówiła tylko „okno przewija się do pola nad klawiaturą”, a przy tekście 200%
>   z klawiaturą pole zostawało pod krawędzią okna — to był falsyfikator z planu;
> - **podpowiedź pod 3c ma tyle linii, ile trzeba, i nigdy nie jest ucięta** (D21). Tekst się nie zmienia. „Do 2 linii” z v8 było niezmierzone: przy
>   100% podpowiedź ma 3 linie (411 i 360 dp), a przy 200% na 360 dp — 5. Krótszy tekst zaproponowany przez `dev` nie daje 2 linii na 360 dp.
>
> **Wersja 9 (2026-10-18, przed planem [[ISSUE-047-grave-first-then-people]]) — przyjęte na stopie #1 (autor: „Tak”, 2026-10-18): najpierw grób, potem osoby.** Autor:
> *„gdy na grobie klikam „Dodaj osobę”, powinienem móc albo wybrać z istniejącej listy, albo dodać nową osobę do rodziny”*. Zmiany:
> - **grób może być pusty** — powstaje z okna „Nowy grób” ([[cmentarz]] 9a, v8), czyli z okna 3a–3c w trybie nowego grobu. Stan „pusty” już był
>   opisany; teraz to zwykły stan po dodaniu grobu (*States*);
> - **„Dodaj osobę” (6) → wybór osoby „Kto leży w tym grobie?”** (8–12): najpierw szukasz; osoby **bez grobu** wybierasz jednym dotknięciem i
>   wracasz do grobu z ich kartą; osoby, które mają grób, widać wyszarzone z powodem; „Nowa osoba” → [[wpis-osoby]] „kolejna osoba” z imionami
>   z szukania (D22–D24). Wzór: wybór osoby z [[rodzina]] B (US-003 AC-5 — tu w drugą stronę: osoba z rodziny w grobie);
> - makieta: `makieta-047.html`, ekrany 3–5.
>
> **Wersja 9.1 (2026-10-18, przegląd `ui` zbudowanego ekranu [[ISSUE-047-grave-first-then-people]]):**
> - **nagłówki sekcji 11 i 12 — 14 sp, półgrube**, jak [[rodzina]] A2 i B4 (ten sam widżet `PersonChoiceList`); „13 sp” w v9 było błędem tej
>   specyfikacji (D25). Pole 9 zostaje z ramką w kolorze obrysu — tak jak zbudowany wybór w arkuszu rodziny;
> - **stan „pusty”: zdanie 40 dp pod 4** (24 dp odstępu grupy + 16 dp wokół zdania), 24 dp nad „Dodaj osobę” (D26).

## Purpose
Wszyscy pochowani w jednym grobie, z datami z dopiskiem (US-002 AC-1, AC-3), nazwa grobu i widoczny brak
adresu kwatery oraz pinezki (AC-5). Stąd dodaje się kolejną osobę, więc przy przepisywaniu to też
potwierdzenie, że wpis się zapisał. Układ to R4: zdjęcie nagrobka u góry (US-005 AC-1), a zdjęcia osób w kartach
dojdą z [[ISSUE-017-person-photos]]. Zdjęcie nagrobka posłuży kiedyś do rozpoznania grobu na miejscu (brief §4a,
krok 3). **Na dole jest data, do której grób jest opłacony** (v8, brief §5 S4). Grób ziemny bez odnowionej opłaty zarządca może
zlikwidować, a to jedyny sposób, żeby stracić sam grób, a nie wiedzę o nim. Wiersz pokazuje też, przy których grobach daty
jeszcze nie ma. Daty wpisuje się na Wszystkich Świętych, z naklejek na grobach albo w biurze zarządcy.

## Navigation
- Z [[cmentarz]] (dotknięcie karty grobu), **z okna „Nowy grób” po zapisie** ([[cmentarz]] 9a, v9 — grób pusty) albo z [[wpis-osoby]] po
  zapisie. Formularz znika ze stosu, więc wstecz z grobu wraca do [[cmentarz]], nie do formularza.
- **Ikonka edycji (3) → okno „Popraw grób”** nad widokiem grobu; „Zapisz” zamyka okno, a tytuł się zmienia.
- **„Wpisz adres” (element 4, v6 — propozycja) → to samo okno** z fokusem w polu „Kwatera”; „Zapisz” zamyka okno, a adres
  pojawia się pod tytułem.
- **„Wpisz” w wierszu „Opłacone do” (element 7, v8) → to samo okno** z fokusem w polu „Opłacone do” (3c). Okno przewija się tak, że pole z
  etykietą stoi u góry widocznej części okna, nad klawiaturą (v8.1, D20). „Zapisz” zamyka okno, a data pojawia się w wierszu. Grób z datą nie ma
  „Wpisz”, datę poprawia się pod ✎ (D17).
- **„Dodaj osobę” → wybór osoby „Kto leży w tym grobie?”** (8–12, v9; do v8.1 — od razu [[wpis-osoby]] „kolejna osoba”):
  - osoba z „Bez grobu” (11) → pochówek w tym grobie zapisuje się od razu → **z powrotem tutaj**, jej karta na końcu listy (5); bez okna
    „Zapisano” ([[style-b]] reguła 10);
  - „Nowa osoba” (10) → [[wpis-osoby]] „kolejna osoba”, imiona = tekst z szukania; zapis → tutaj, jak dotąd (formularz i wybór znikają ze stosu);
  - wstecz → tutaj bez zmian.
- **„Dodaj zdjęcie” → arkusz źródła** ([[zdjecie]] A) → systemowe okno wyboru (jedno zdjęcie) albo aparat → z
  powrotem tutaj, a zdjęcie zapisuje się od razu, bez formularza (v3).
- **Dotknięcie zdjęcia nagrobka → podgląd** ([[zdjecie]] B): tam „Zmień zdjęcie” i „Usuń zdjęcie” (v3).
- Dotknięcie karty osoby → **widok osoby** ([[osoba]], M5, R4 prawy; v5, SPIKE-004 D13). Do v4.1 prowadziło do
  [[wpis-osoby]] w trybie „poprawa” (ISSUE-012, D1), bo widoku osoby nie było.
- **Dolny pasek** Mapa · Osoby · Drzewo widoczny (v5, [[style-b]] reguła 12).
- Wstecz → [[cmentarz]].

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** wstecz; podtytuł paska: nazwa cmentarza · miejscowość (14 sp, tekst pomocniczy, jedna linia, ucięta) | pasek | wstecz → [[cmentarz]] | — | — | decyzja projektowa |
| 1a | **Zdjęcie nagrobka** (v3). **Bez zdjęcia (v3.2, D12): pole „Dodaj zdjęcie nagrobka”** w tym samym miejscu — szerokość treści, **wysokość 120 dp**, zaokrąglenie 16 dp, obrys 1 dp w kolorze obrysu na tle (bez wypełnienia), w środku `add_a_photo_outlined` (32 dp, akcent) i pod nią „Dodaj zdjęcie nagrobka” (16 sp, półgruby 500, kolor tekstu); całe pole to jeden przycisk, opis dla czytnika „Dodaj zdjęcie nagrobka”; dotknięcie → [[zdjecie]] A. **Ze zdjęciem:** szerokość treści (marginesy 16 dp), zaokrąglenie 16 dp; proporcja zdjęcia, ale **nie wyżej niż szerokość** — wyższe (pionowy nagrobek) przycięte do kwadratu ze środka (D8). **Jedno zdjęcie na grób** (D9). Opis dla czytnika: „Zdjęcie nagrobka — otwórz”. Odstęp do tytułu 16 dp | obraz-przycisk | dotknięcie → [[zdjecie]] B | — | — | US-005 AC-1 · R4 · [[style-b]] reguła 14 · decyzja autora (jedno zdjęcie) |
| 2 | **Tytuł:** nazwa grobu (24 sp, półgruby, wyśrodkowany, do 2 linii). **Bez nazwy: „Grób”** w tym samym kroju | tekst | — | — | — | R4 · decyzja autora (nazwa grobu) · D1 |
| 3 | **Ikonka edycji** w linii tytułu, z prawej: `edit_outlined` w akcencie, cel 48 × 48 dp, `tooltip` „Popraw grób”. Tytuł ma z lewej taki sam odstęp, więc zostaje wyśrodkowany | przycisk-ikona | → okno „Popraw grób” (3a) | — | — | decyzja projektowa (jak [[cmentarze]] element 8) · D2 |
| 3a | **Okno „Popraw grób”:** pole **„Nazwa grobu”** (ramka w kolorze obrysu, wielka litera na początku zdania, podpowiedź „np. Grób rodzinny Nowaków” — tekst z R4), pod polem „Zostaw puste, jeśli grób nie ma nazwy.” (13 sp, tekst pomocniczy). Przyciski „Anuluj” (kolor tekstu) · **„Zapisz”** (akcent) — jak okno cmentarza w `cemetery_form.dart` | okno dialogowe | fokus i klawiatura od razu, kursor na końcu obecnej nazwy; `done` = „Zapisz” | obecna nazwa albo pusto | puste = bez nazwy (tytuł „Grób”); spacje na brzegach obcięte. Błąd zapisu: pod polem `error_outline` + „Nie udało się zapisać. Spróbuj jeszcze raz.” (kolor błędu), okno zostaje | decyzja autora (nazwa grobu) · [[style-b]] reguła 1 (okno) |
| 3b | **Adres w oknie „Popraw grób” (v6 — propozycja, stop #1 ISSUE-028).** Pod „Nazwą grobu” podpis grupy „Adres zarządcy” (13 sp, tekst pomocniczy, odstęp 16 dp) i pola z ramką w kolorze obrysu: **„Kwatera”**, a pod nim **„Rząd”** i **„Miejsce”** obok siebie (po połowie szerokości; przy tekście 200% jedno pod drugim). Pod polami: „Z wyszukiwarki zarządcy. Zostaw puste, czego nie wiesz.” (13 sp, tekst pomocniczy). **„Kwatera” — według decyzji W-a/W-b** ([[cmentarz]] → *Open*): **W-a** — pod polem chipy kwater tego cmentarza (kolejność naturalna, jak [[cmentarz]] 17a; [[style-b]] reguła 11 — chip z obrysem, cel 48 dp); dotknięcie chipu wpisuje jego nazwę; wpis równy kwaterze (bez wielkości liter, polskich znaków i słowa „Kwatera” na początku) zaznacza jej chip (`check`, obrys i napis w akcencie, stan „zaznaczone” dla czytnika); wpis bez odpowiednika → pod chipami „Nowa kwatera „D” — powstanie bez strefy; zaznaczysz ją w „Kwaterach”.” (13 sp, tekst pomocniczy). Bez kwater na cmentarzu — bez chipów. **W-b** — zwykłe pole tekstowe | pola tekstowe (+ chipy przy W-a) | klawiatura tekstowa (bywa „12a”, „IV”, „B”) bez wymuszonych wielkich liter; Nazwa `next` → Kwatera `next` → Rząd `next` → Miejsce `done` = „Zapisz”; okno przewija się nad klawiaturą. **Od v8: Miejsce `next` → Opłacone do (3c)** | obecne wartości albo pusto | wszystko opcjonalne; spacje na brzegach obcięte; słowo pola na początku wpisu („Kwatera B”, „Rząd 4”, „Miejsce 12”) usunięte, żeby adres nie mówił „Kwatera Kwatera B” | **luka M1** · [[EPIC-002-wizyta]] → *Open questions* (krok 1) · [[cmentarz]] *Open* · D13 |
| 3c | **„Opłacone do” w oknie „Popraw grób”** (v8). Ostatnie pole okna, 16 dp pod podpisem adresu, bez podpisu grupy (etykieta mówi, co to). Pole z ramką w kolorze obrysu, etykieta **„Opłacone do”**, podpowiedź „np. 2031”, pod polem tekst pomocniczy, 13 sp, ~~do 2 linii~~ **w tylu liniach, ile trzeba, nigdy ucięty** (v8.1, D21 — przy 100% 3 linie, przy 200% na 360 dp 5): „Rok albo data z naklejki na grobie lub z pokwitowania. Zostaw puste, jeśli nie wiesz.” (twarda spacja po „z”, [[style-b]] reguła 6) | pole daty | **klawiatura numeryczna z kropką**, jak pole daty w [[wpis-osoby]] (c). `done` = „Zapisz”. Przy wejściu z „Wpisz” (7): fokus i klawiatura od razu, kursor na końcu. **Przewijanie (v8.1, D20):** przy fokusie w 3c (z „Wpisz”, z `next` w „Miejsce”, po dotknięciu pola), przy zmianie wysokości klawiatury i przy błędzie okno stawia pole u góry widocznej części, 16 dp pod jej krawędzią, żeby etykieta nad ramką nie była ucięta. Gdy treść okna kończy się wcześniej, okno pokazuje swój koniec | obecna data (`2031`, `03.2031`, `31.12.2031`) albo pusto | puste = bez daty („nie wiadomo”). **`rrrr` · `mm.rrrr` · `dd.mm.rrrr`, bez dopisku** (D18). **Lata od 1500 do bieżącego roku + 50**, a przyszłość jest dozwolona (pole daty osoby jej nie przyjmuje). Zły zapis → pod polem `error_outline` i „Nie rozumiem tej daty — wpisz rok, mm.rrrr albo dd.mm.rrrr.” (ten sam tekst co w bloku daty). Rok dalej niż za 50 lat → „Tak odległa data to raczej pomyłka — sprawdź rok.” Przy błędzie okno zostaje i **nie zapisuje się nic** (ani nazwa, ani adres). Błąd zapisu — jak 3a | brief §5 S4 · ISSUE-043 AC-1 · D18 |
| 4 | **Adres i pinezka** pod tytułem, wyśrodkowane: adres pełnymi słowami „Kwatera B · Rząd 4 · Miejsce 12” (14 sp, tekst pomocniczy). Bez adresu: ikona `place_outlined` + „Bez adresu kwatery · bez pinezki”, a pod spodem ~~„Uzupełnisz przy wizycie.” (tekst pomocniczy)~~ **(v6 — propozycja) przycisk tekstowy w linii treści „Wpisz adres”** (akcent, [[style-b]] reguła 1, cel 48 dp), bo adres przepisuje się w domu z wyszukiwarki zarządcy, a nie przy wizycie. Z adresem, bez pinezki: adres + „· bez pinezki”. **Pinezka (v7):** grób bez pinezki — pod adresem (i pod „Wpisz adres”) **przycisk z obrysem „Postaw pinezkę”** (`add_location_alt` w akcencie, napis w kolorze tekstu, wys. 48 dp, wyśrodkowany, odstęp 8 dp); grób z pinezką — zamiast „· bez pinezki” druga linia **„Pinezka: GPS ±4 m · 12.10.2026”** (13 sp, tekst pomocniczy; teksty źródła — [[cmentarz]] 14), bez daty, gdy pinezka jej nie ma | tekst (+ przycisk tekstowy, + przycisk z obrysem) | „Wpisz adres” → okno 3a z fokusem w „Kwatera”; „Postaw pinezkę” → tryb D [[cmentarz]] (12) dla tego grobu | — | — | AC-5 · R4 · D13 · US-008 AC-2 · D14 |
| 5 | **Karty osób** w kolejności wpisania, odstęp 8 dp. Karta: „Imiona Nazwisko z d. Rodowe” (16 sp, półgruby, zawijane); lata życia (14 sp, tekst pomocniczy): `1921–1987`, a z dopiskiem `ok. 1890 – 14.03.1951`; gdy jest data pochówku: `· poch. 18.03.1951`. Brak urodzenia: `zm. 1951`; brak zgonu: `ur. 1890`; brak dat: „bez dat”. **Chevron „›” — karta prowadzi do widoku osoby** ([[osoba]], v5; do v4.1 do poprawy). **Profilowe osoby (v4, [[ISSUE-017-person-photos]]):** okrąg 40 dp z lewej, wyśrodkowany w pionie, odstęp 12 dp do tekstu, w kadrze łącza ([[kadr-profilowego]], v4.1), a bez kadru przycięty ze środka, poza czytnikiem (kartę opisuje jej tekst); osoba bez zdjęcia — bez miniatury i bez wcięcia (D11). Plik bez odczytu: okrąg na tle z `broken_image_outlined` (20 dp, tekst pomocniczy) | lista kart na powierzchni, karta ≥ 64 dp | dotknięcie → widok osoby ([[osoba]], v5) | kolejność wpisania | — | AC-1 · AC-2 · AC-3 · R4 · ISSUE-017 AC 4 |
| 6 | **Rząd działań:** „Dodaj osobę” — przycisk z obrysem, ikona `person_add_alt_outlined` w akcencie, napis w kolorze tekstu, ≥ 52 dp, szerokość treści, z lewej. „Dodaj zdjęcie” jest w polu 1a (v3.2, D12), nie tutaj | rząd przycisków pod listą | „Dodaj osobę” → wybór osoby (8–12, v9; do v8.1 — [[wpis-osoby]] „kolejna osoba”) | — | — | *What to build* 3 · R4 · ISSUE-047 AC-2, AC-3 |
| 7 | **„Opłacone do” — ostatni element widoku** (v8, D15). 24 dp pod „Dodaj osobę” ([[style-b]] reguła 5). U góry linia podziału 1 dp w kolorze obrysu, wiersz ≥ 48 dp, taki sam jak wiersze „Daty” w [[osoba]] (8). **Etykieta** „Opłacone do” (kolumna 96 dp, 14 sp, tekst pomocniczy; przy większym tekście, gdy się nie mieści, nad wartością, jak [[osoba]] v2.2). **Wartość**: **z datą** — data jak wpisana ([[style-b]] reguła 6: `2031`, `03.2031`, `31.12.2031`; 16 sp, kolor tekstu), także data, która już minęła (D19); **bez daty (W1, D16)** — „nie wiadomo” (16 sp, tekst pomocniczy), a na końcu wiersza przycisk tekstowy **„Wpisz”** (akcent, 14 sp, półgruby 600, cel 48 dp — jak „Wpisz adres”). Gdy wartość i „Wpisz” nie mieszczą się w jednej linii (tekst 200% na 360 dp), „Wpisz” przechodzi pod wartość, z lewej. **Opis dla czytnika**: wiersz — „Opłacone do 2031” albo „Opłacone do: nie wiadomo”; przycisk — „Wpisz datę opłaty” (zawiera widoczne „Wpisz”, SC 2.5.3). **Wiersz to fakt, nie przycisk** (D17) | wiersz faktu (+ przycisk tekstowy) | „Wpisz” → okno 3a z fokusem w 3c | „nie wiadomo” | — | brief §5 S4 · ISSUE-043 AC-1, AC-2 · decyzja autora („na samym dole profilu grobu”) · D15–D17 |

**Wybór osoby — „Kto leży w tym grobie?”** (v9, [[ISSUE-047-grave-first-then-people]]; pełny ekran, tryb wyboru — bez dolnego paska, [[style-b]]
reguła 12). **Ten sam wybór co w [[rodzina]] B** (`PersonChoiceList`: pole z fokusem, „Nowa osoba” nad listą, wiersze nieaktywne z powodem
tekstem), z innymi sekcjami:

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 8 | **Pasek:** wstecz + „Kto leży w tym grobie?” (20 sp, półgruby); bez podtytułu — grób widać pod spodem po powrocie | pasek | wstecz → widok grobu bez zmian | — | — | decyzja projektowa |
| 9 | **Pole „Szukaj osoby albo wpisz nową”** — jak [[rodzina]] B2: ramka w kolorze obrysu, `search` w tekście pomocniczym, filtruje 11 i 12 bez polskich znaków i wielkości liter, od początku słowa imienia, nazwiska albo nazwiska rodowego (`matchesQuery`) | pole tekstowe | **fokus i klawiatura od wejścia** (najczęściej wpisujesz imię z notatki); wielka litera na początku słów; `done` chowa klawiaturę; przewinięcie listy chowa klawiaturę | pusto | — | ISSUE-047 AC-2 · [[rodzina]] D3 |
| 10 | **„Nowa osoba”** — pierwszy wiersz pod polem, zawsze widoczny: `person_add_alt_outlined` (akcent) i „Nowa osoba”, a przy wpisanym tekście „Nowa osoba: „Jan”” (16 sp, tekst), ≥ 56 dp — jak [[rodzina]] B3 | wiersz-przycisk | → [[wpis-osoby]] „kolejna osoba”, **imiona = tekst z 9** (spacje na brzegach obcięte), nazwisko podpowiedziane jak dotąd (z poprzedniej osoby w grobie; w pustym grobie — puste) | — | — | ISSUE-047 AC-3 |
| 11 | **Sekcja „Bez grobu”** (nagłówek ~~13 sp~~ **14 sp, półgruby** (v9.1), tekst pomocniczy, jak [[rodzina]] B4 i A2) — osoby bez żadnego pochówku: dodane w drzewie albo arkuszem rodziny, z zakładki Osoby, także żyjące. Kolejność po nazwisku, potem imionach (`polishCompare`). **Wiersz** jak [[rodzina]] B5: imiona i nazwisko z „z d.” (16 sp, tekst), lata według [[style-b]] reguły 6, a bez dat „bez dat” (14 sp, tekst pomocniczy), ≥ 56 dp, cały wiersz to jeden cel. Bez osób bez grobu — sekcji nie ma | lista | dotknięcie → **pochówek tej osoby w tym grobie zapisuje się od razu** (ze źródłem domyślnym po cichu, jak każdy pochówek — [[wpis-osoby]] v5.4) → widok grobu z jej kartą. Błąd zapisu → pasek komunikatu „Nie udało się zapisać. Spróbuj jeszcze raz.”, wybór zostaje otwarty | — | — | ISSUE-047 AC-2 · D22 |
| 12 | **Sekcja „W grobach”** — osoby, które mają pochówek, w tej samej kolejności. **Wszystkie nieaktywne** (D23): tekst w kolorze pomocniczym, bez dotknięcia, dla czytnika „niedostępne”, a **zamiast lat powód tekstem** (SC 1.4.1): „już w tym grobie” albo „w grobie: Grób rodzinny Zmyślonych” (nazwa grobu, a bez niej nazwa cmentarza; jedna linia, ucięta) | lista | — | — | — | D23 · [[rodzina]] *Wiersze nieaktywne* |

**Stany wyboru:** pusta baza → tylko 9 i 10 · szukanie bez wyników → 9 i 10 z tekstem („Nowa osoba: „Jan””), bez sekcji · błąd odczytu → „Nie udało się
odczytać osób.” (tekst pomocniczy) pod 10 — „Nowa osoba” działa dalej.

**Dane, których ekran potrzebuje od v9** (dla `planning`, [[ISSUE-047-grave-first-then-people]]): **bez zmiany schematu** — `burials` to osobna tabela
osoba ↔ grób ([[data-model]]), więc grób bez osób i pochówek osoby, która już jest w aplikacji, to zwykłe wiersze. Potrzebne: utworzenie grobu bez
osoby (nazwa, adres, opłata — jedna transakcja jak „Zapisz” w 3a–3c) i dodanie pochówku istniejącej osoby (`addBurialWithClaim` w `claims.dart`); dla
wyboru — lista osób z informacją, czy i gdzie mają pochówek (jak `loadPersonChoices`). Oba zapisy zamawiają kopię w tle jak każdy zapis.

**Gdy źródła się spierają** (dwie daty urodzenia albo dwa groby jednej osoby), widok pokazuje **pierwszą**
wartość — najniższe `id`, jak w GEDCOM 7 ([[ADR-006-claimed-value-separate-structures]] D3; `claims.dart` →
`firstEvent`). Oznaczenie sporu to [[US-004-fakt-od-babci]]. Osoba z dwoma pochówkami pojawia się w obu
grobach (ADR-006, *Consequences*).

**Dane, których ekran potrzebuje** (dla `planning`): nowe, opcjonalne pole **nazwa grobu** w tabeli grobów —
zmiana schematu, migracja v2→v3 z testem ([[NFR-003-migracje-schematu]]) i kopia zaraz po migracji (retro 1,
R6). Zapis nazwy zamawia kopię w tle jak każdy zapis.

**Dane, których ekran potrzebuje od v3** (dla `planning`, [[ISSUE-016-photos-grave-and-person]]): zdjęcie grobu
(najwyżej jeden wiersz `Media` z `grave_id`), więc **wygląd nie wymaga zmiany schematu**. Miniatura (56 dp w
[[cmentarz]]) i zdjęcie w widoku grobu dekodowane w rozmiarze, w jakim się wyświetlają. Dodanie, zmiana i usunięcie
zdjęcia zamawiają kopię w tle jak każdy zapis.

**Dane, których ekran potrzebuje od v4** (dla `planning`, [[ISSUE-017-person-photos]]): dla każdej osoby w grobie
ścieżka jej **profilowego**, czyli pliku z pierwszego łącza osoby, albo nic. **Od v4.1:** także kadr tego łącza (albo
brak kadru — wtedy środek). Miniatura dekodowana w rozmiarze 40 dp ×
gęstość ekranu, jak miniatury nagrobków.

**Dane, których ekran potrzebuje od v8** (dla `planning`, [[ISSUE-043-grave-paid-until]]): opcjonalna data **„opłacone do”** przy grobie.
Dokładność to rok, miesiąc albo dzień (jak `PartialDate`), bez dopisku. Zapis **w postaci, z której da się wyliczyć najwcześniejszą datę**,
a nie wolnym tekstem, bo z tej daty przypomnienie wyliczy później termin ([[data-model]] → *Grave*: „opłata ważna do (S4)”). To nowa kolumna
w `graves`, więc zmiana schematu: migracja v13 → v14 z testem ([[NFR-003-migracje-schematu]]) i migawką sprzed migracji
([[ISSUE-041-google-play-and-safe-update]]). Kopię niesie razem z całą bazą. „Zapisz” w oknie zapisuje nazwę, adres i datę razem i zamawia
kopię w tle, jak każdy zapis. **Walidacja dat osoby się nie zmienia**: lata z przyszłości przyjmuje tylko to pole (D18).

## States
| Stan | Co widać |
|---|---|
| wypełniony | 1–6 (1a tylko, gdy grób ma zdjęcie; wtedy w 6 tylko „Dodaj osobę”) |
| bez zdjęcia (v3.2) | nad tytułem pole „Dodaj zdjęcie nagrobka” (1a, 120 dp); rząd działań — tylko „Dodaj osobę” |
| wczytywanie zdjęcia (v3.1) | do pierwszej klatki obrazu: w miejscu 1a puste pole w proporcji 4:3 (bez wskaźnika — zwykle ułamek sekundy), żeby tytuł i osoby nie przeskakiwały o wysokość zdjęcia |
| zapisywanie zdjęcia (v3) | w miejscu 1a pole na powierzchni (proporcja 4:3, zaokrąglenie 16 dp) ze wskaźnikiem postępu i „Zapisuję zdjęcie…” (14 sp, tekst pomocniczy) — zamiast pola „Dodaj zdjęcie nagrobka”. Zmniejszanie zdjęcia trwa chwilę (do zmierzenia). Po zapisie widać **dodane zdjęcie** — to potwierdzenie (reguła 10) |
| nieudany zapis zdjęcia (v3.2) | **pod polem 1a**, przy miejscu, którego dotyczy: `error_outline` + „Nie udało się zapisać zdjęcia. Spróbuj jeszcze raz.” (kolor błędu, 14 sp); pole „Dodaj zdjęcie nagrobka” zostaje. Komunikat znika przy następnym dodaniu |
| brak pliku zdjęcia (v3) | wpis zdjęcia jest, pliku nie ma albo nie da się go odczytać: w miejscu zdjęcia pole na powierzchni z `broken_image_outlined` i „Nie udało się otworzyć zdjęcia.” (tekst pomocniczy); dotknięcie → podgląd, gdzie można zdjęcie zmienić albo usunąć |
| bez nazwy | tytuł „Grób” + ikonka edycji; reszta bez zmian |
| bez pinezki (v7) | 4: adres (albo „Bez adresu kwatery · bez pinezki” i „Wpisz adres”), pod nim „Postaw pinezkę” |
| z pinezką (v7) | 4: adres, pod nim „Pinezka: GPS ±4 m · 12.10.2026” (albo inne źródło — [[cmentarz]] 14); bez „Postaw pinezkę” |
| z datą opłaty (v8) | 7: „Opłacone do” · „2031” (data jak wpisana, także miniona); bez „Wpisz” |
| bez daty opłaty (v8, W1) | 7: „Opłacone do” · „nie wiadomo” · „Wpisz” |
| pusty | **v9: zwykły stan po „Nowy grób”** ([[cmentarz]] 9a; do v8.1 z interfejsu nie powstawał). 1a (pole „Dodaj zdjęcie nagrobka”), 2–4 (tytuł, adres, „Wpisz adres”, „Postaw pinezkę”), w miejscu kart „W tym grobie nie ma jeszcze wpisanych osób.” (16 sp, tekst pomocniczy, wyśrodkowane, ~~24 dp~~ **40 dp pod 4** (v9.1, D26) — [[style-b]] reguła 9), pod nim, 24 dp niżej, „Dodaj osobę” (6), na dole 7 |
| okno „Popraw grób” | element 3a nad widokiem grobu |
| okno „Popraw grób” z „Wpisz” (v8) | 3a przewinięte do 3c, fokus w „Opłacone do”, klawiatura numeryczna. **v8.1:** pole z etykietą u góry widocznej części okna (D20); przy 100% widać całe pole z podpowiedzią, przy 200% z klawiaturą — pole i początek podpowiedzi, a resztę po przewinięciu |
| zła data w oknie (v8) | pod 3c `error_outline` + komunikat (D18) zamiast podpowiedzi, ramka i etykieta w kolorze błędu, okno zostaje i przewija pole z komunikatem na górę (v8.1), nic się nie zapisuje |
| błąd | „Nie udało się odczytać grobu.” + „Spróbuj ponownie” (przycisk z obrysem) |
| wczytywanie | wskaźnik postępu w środku (zwykle niewidoczny) |

## Sketch
**v3 — ze zdjęciem nagrobka** (ISSUE-016; miniatury osób dojdą z ISSUE-017):
```
┌──────────────────────────────────┐
│ ←  Cmentarz Wymyślony · Miejsco… │
│ ╭──────────────────────────────╮ │
│ │                              │ │
│ │      [zdjęcie nagrobka —     │ │  ← dotknięcie: podgląd
│ │       wymyślone]             │ │    (zmień · usuń)
│ │                              │ │
│ ╰──────────────────────────────╯ │
│      Grób rodzinny          ✎   │
│      Wymyślonych                 │
│  ⌖ Bez adresu kwatery · bez      │
│    pinezki                       │
│ ╭──────────────────────────────╮ │
│ │ Jan Wymyślony              › │ │
│ │ ok. 1890 – 14.03.1951        │ │
│ ╰──────────────────────────────╯ │
│ ╭──────────────────────────────╮ │
│ │ Anna Wymyślona z d. Zmyślona›│ │
│ │ 1893–1960                    │ │
│ ╰──────────────────────────────╯ │
│ ╭─────────────────╮              │  ← zdjęcie jest: tylko
│ │ 👤+ Dodaj osobę  │              │    „Dodaj osobę”
│ ╰─────────────────╯              │
└──────────────────────────────────┘
```

**v3.2 — bez zdjęcia** (D12): w miejscu zdjęcia pole z obrysem, wysokość 120 dp:
```
│ ╭──────────────────────────────╮ │
│ │            📷+               │ │  ← add_a_photo_outlined, akcent
│ │    Dodaj zdjęcie nagrobka    │ │
│ ╰──────────────────────────────╯ │
│      Grób rodzinny          ✎   │
│      Wymyślonych                 │
```
Niżej szkic v2 — układ reszty widoku bez zmian; rząd działań ma tylko „Dodaj osobę”:
```
 grób z nazwą                          okno „Popraw grób”
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│ ←  Cmentarz Wymyślony · Miejsco… │  │ ←  Cmentarz Wymyślony · Miejsco… │
│                                  │  │  ╭────────────────────────────╮  │
│      Grób rodzinny          ✎   │  │  │ Popraw grób                │  │
│      Wymyślonych                 │  │  │ ┌ Nazwa grobu ───────────┐ │  │
│  ⌖ Bez adresu kwatery · bez      │  │  │ │ Grób rodzinny Wymyślo▌ │ │  │
│    pinezki                       │  │  │ └────────────────────────┘ │  │
│    Uzupełnisz przy wizycie.      │  │  │ Zostaw puste, jeśli grób   │  │
│ ╭──────────────────────────────╮ │  │  │ nie ma nazwy.              │  │
│ │ Jan Wymyślony              › │ │  │  │          Anuluj   Zapisz   │  │
│ │ ok. 1890 – 14.03.1951 ·      │ │  │  ╰────────────────────────────╯  │
│ │ poch. 18.03.1951             │ │  │                                  │
│ ╰──────────────────────────────╯ │  │                                  │
│ ╭──────────────────────────────╮ │  │                                  │
│ │ Anna Wymyślona z d. Zmyślona›│ │  │                                  │
│ │ między 1893 a 1895 – przed   │ │  │                                  │
│ │ 1960                         │ │  │                                  │
│ ╰──────────────────────────────╯ │  │                                  │
│ ╭──────────────────────────────╮ │  │                                  │
│ │ Józef Wymyślony            › │ │  │                                  │
│ │ po 1920 – 1944               │ │  │                                  │
│ ╰──────────────────────────────╯ │  │                                  │
│ ╭─────────────────╮              │  │                                  │
│ │ 👤+ Dodaj osobę  │              │  │                                  │
│ ╰─────────────────╯              │  │                                  │
└──────────────────────────────────┘  └──────────────────────────────────┘
```

**v8 — dół widoku: „Opłacone do”** (ISSUE-043). Na stopie #1 do wyboru **W1** (rekomendacja, D16) albo **W2**:
```
 W1 — wiersz zawsze                    W2 — wiersz tylko z datą
 z datą:                               z datą: jak W1
│ ╭─────────────────╮              │  │ ╭─────────────────╮              │
│ │ 👤+ Dodaj osobę  │              │  │ │ 👤+ Dodaj osobę  │              │
│ ╰─────────────────╯              │  │ ╰─────────────────╯              │
│                                  │  │                                  │  ← 24 dp
│ ──────────────────────────────── │  │ ──────────────────────────────── │  ← linia podziału (obrys)
│ Opłacone do   2031               │  │ Opłacone do   2031               │
└──────────────────────────────────┘  └──────────────────────────────────┘
 bez daty:                             bez daty:
│ ╭─────────────────╮              │  │ ╭─────────────────╮              │
│ │ 👤+ Dodaj osobę  │              │  │ │ 👤+ Dodaj osobę  │              │
│ ╰─────────────────╯              │  │ ╰─────────────────╯              │
│                                  │  └──────────────────────────────────┘
│ ──────────────────────────────── │   nic nie mówi, że daty brak;
│ Opłacone do   nie wiadomo  Wpisz │   wpis tylko pod ✎ przy tytule
└──────────────────────────────────┘
       „Wpisz” (akcent) → okno, fokus w „Opłacone do”
```
Okno „Popraw grób” — koniec okna (3c), po wejściu z „Wpisz”:
```
│  │ Z wyszukiwarki zarządcy. Zostaw  │  │
│  │ puste, czego nie wiesz.          │  │
│  │ ┌ Opłacone do ─────────────────┐ │  │
│  │ │ ▌                            │ │  │  ← fokus, klawiatura numeryczna
│  │ └──────────────────────────────┘ │  │
│  │ Rok albo data z naklejki na      │  │
│  │ grobie lub z pokwitowania.       │  │
│  │ Zostaw puste, jeśli nie wiesz.   │  │
│  │                Anuluj   Zapisz   │  │
```

## Tempo
Widok do oglądania. Jako krok przepisywania:
- ~~**1 dotknięcie** („Dodaj osobę”) na każdą osobę poza pierwszą w grobie~~ **v9: 2 dotknięcia na nową osobę** („Dodaj osobę”, „Nowa osoba” po
  wpisaniu imienia w 9 — imię nie powtarza się w formularzu, więc tempo formularza bez zmian), **także dla pierwszej osoby w grobie** (grób powstaje
  oknem — [[cmentarz]] *Tempo*). Ok. 100 osób → ok. 100 dotknięć więcej niż w v8.1, w zamian każde imię przed wpisaniem pokazuje, czy ta osoba
  już jest (D22);
- **osoba, która już jest w aplikacji bez grobu** (v9): „Dodaj osobę”, kilka liter, wiersz = **2 dotknięcia** — do v8.1 tylko jako druga, nowa osoba;
- **nazwa grobu: 2 dotknięcia** (ikonka, „Zapisz”) i pisanie — tylko dla grobów, które mają nazwę. Zaraz po
  zapisie pierwszej osoby ten widok jest na ekranie, więc nazwę nadaje się bez szukania grobu.
- **adres zarządcy (v6 — propozycja): ok. 4 dotknięcia** („Wpisz adres”, chip kwatery albo 1–2 znaki, „dalej” do rzędu i miejsca,
  „Zapisz”) i 2–6 znaków na grób; ok. 50 grobów. Adres przepisuje się z wyszukiwarki zarządcy, więc autor przełącza się między
  przeglądarką a aplikacją — dlatego jedno okno na cały adres, a nie trzy.
- **zdjęcie nagrobka (v3.1): 4 dotknięcia** z galerii („Dodaj zdjęcie”, „Wybierz z galerii”, zdjęcie, „Gotowe” —
  okno systemowe na Androidzie 16 wymaga potwierdzenia, [[zdjecie]] → *Tempo*). Na ok. 50 grobów: ok. 200 dotknięć.
  Też bez szukania grobu — widok jest na ekranie po zapisie osoby.
- **koszt zdjęcia nagrobka dla „Dodaj osobę” (v3):** zdjęcie (do kwadratu szerokości, ok. 330 dp) przesuwa rząd
  działań w dół. **Zmierzone (przegląd `ui`, `Medium_Phone` 411 × 914 dp):** bez przewijania „Dodaj osobę” mieści się
  przy zdjęciu poziomym (4:3) do **4 osób**, przy pionowym (kwadrat) do **3 osób**; od 5 (poziome) albo 4 (pionowe)
  trzeba przewinąć. Średnio ok. 2 osoby na grób (G6), więc przy przepisywaniu zwykle mieści się bez przewijania;
  przy dużych grobach taniej dodać zdjęcie **po** osobach z notatek. *Obali D8:* przewijanie przeszkadza na stopie
  #2 — wtedy zdjęcie niższe (np. do 200 dp) albo rząd działań przypięty na dole.
- **„Opłacone do” (v8): 2 dotknięcia i ok. 4 cyfry na grób** („Wpisz”, cyfry na klawiaturze numerycznej, `done` = „Zapisz”), czasem jedno
  przewinięcie do dołu. Przy ok. 50 grobach to ok. 100 dotknięć. Dane przychodzą seriami: naklejki przy grobach na Wszystkich Świętych
  albo lista z biura zarządcy. Przez ✎ to samo kosztuje 3 dotknięcia (✎, pole, „Zapisz”), dlatego przy braku daty jest skrót „Wpisz” (D16).
  Daty nie da się nadać od razu po zapisie osoby tak jak nazwy grobu, bo przy przepisywaniu notatek zwykle jej nie ma.

## Style B rules applied
- **Reguła 1:** brak wypełnionego przycisku — jak w R4, treścią są osoby. „Dodaj osobę” ma obrys i ikonę w
  akcencie. W oknie „Zapisz” jest przyciskiem tekstowym w akcencie.
- **Reguły 2 i 11:** karty osób na powierzchni z chevronem; bez zastępczych obrazków (miniatury osób —
  [[ISSUE-017-person-photos]]).
- **Reguła 14 (v1.7):** zdjęcie nagrobka bez filtrów i bez tekstu na nim; bez zdjęcia nie ma pola.
- **Reguła 3:** `place_outlined` w kolorze pomocniczym (opisuje), `person_add_alt_outlined`, `add_a_photo_outlined`
  i `edit_outlined` w akcencie (działania). **v7:** `add_location_alt` w akcencie przy „Postaw pinezkę” (przycisk z obrysem — reguła 1:
  dalej bez wypełnionego przycisku); linia źródła pinezki to fakt w tekście pomocniczym.
- **Reguła 4:** tytuł i imiona półgrube.
- **Reguła 6:** lata życia, „z d.” w tej samej linii, adres pełnymi słowami.
- **Reguła 7:** brak adresu opisany faktem i tym, kiedy się uzupełni; „Zostaw puste, jeśli grób nie ma
  nazwy.” zamiast oznaczenia pola jako opcjonalnego.
- **Reguła 10:** zapis z [[wpis-osoby]] kończy się tym widokiem, bez okienka „Zapisano”; zapis nazwy kończy
  się nowym tytułem.
- **v8 — „Opłacone do”:**
  - wiersz faktu jak „Daty” w [[osoba]] (8): linia podziału w obrysie, etykieta w tekście pomocniczym, wartość w kolorze tekstu. Bez nowego wzorca;
  - reguła 1 — „Wpisz” to przycisk tekstowy w linii treści, w akcencie (v1.6), jak „Wpisz adres”;
  - reguła 5 — 24 dp między grupami;
  - reguła 6 — format daty, a w nowych tekstach twarda spacja po „z” („z naklejki”, „z pokwitowania”);
  - reguła 7 — brak opisany faktem: „nie wiadomo” i „Zostaw puste, jeśli nie wiesz.”, bez ostrzeżenia. Data, która minęła, też jest faktem, bez czerwieni (D19);
  - reguła 15 — poprawa ma jedno wejście, ✎ (D17);
  - SC 1.4.1 — błąd w oknie ma ikonę i tekst.
- **Tokeny:** bez nowych.
- **Uwaga na ekrany wizyty:** lata i adres są tu w tekście pomocniczym (5,50:1 na tle). [[NFR-004-czytelnosc-w-sloncu]]
  przyjęła 7:1 (W2, 2026-10-12, [[ISSUE-027-cemetery-map-plan-photo-states]]) — gdy ten widok stanie się widokiem wizyty (M4), te
  linie przejdą na kolor tekstu ([[style-b]] → *Thresholds*).

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-002 AC-1 | 5 | każda osoba wpisana do grobu ma kartę |
| US-002 AC-2 | 5 | imiona, nazwisko i osobno „z d. Rodowe”; „kim była” — patrz D3 |
| US-002 AC-3 | 5 (lata życia, data pochówku) | każdy z pięciu dopisków widać w zapisie: „1890”, „ok. 1890”, „przed 1920”, „po 1945”, „między 1893 a 1895” |
| US-002 AC-5 | 4 | grób bez adresu i pinezki zapisany i widoczny z „Bez adresu kwatery · bez pinezki” |
| v6 — propozycja (stop #1 ISSUE-028): adres zarządcy | 3b, 4 | „Wpisz adres” → „B”, „4”, „12” → „Zapisz” → pod tytułem „Kwatera B · Rząd 4 · Miejsce 12 · bez pinezki”, a karta w [[cmentarz]] ma ten sam adres |
| decyzja autora 2026-10-06: grób jak R4 z nazwą grobu | 2, 3, 3a | ikonka → „Grób rodzinny Wymyślonych” → „Zapisz” → tytuł widoku i tytuł karty w [[cmentarz]] |
| ISSUE-012: styl B | całość | reguły wyżej; przegląd `ui` przed stopem #2 |
| US-005 AC-1 (v3.2, grób) | 1a → [[zdjecie]] A | pole „Dodaj zdjęcie nagrobka” → wybór → zdjęcie w tym samym miejscu, nad tytułem |
| US-005 AC-2 (v3) | 1a | zdjęcie dalej widać po usunięciu oryginału z galerii emulatora |
| US-005 AC-3 (v3) | 1a | po odtworzeniu z kopii to samo zdjęcie (odcisk danych — `qa`) |
| ISSUE-016: zmiana i usunięcie (decyzja autora, stop #1) | 1a → [[zdjecie]] B4, C | podgląd → „Zmień zdjęcie” → nowe zdjęcie; „Usuń zdjęcie” → okno → zdjęcia nie ma, „Dodaj zdjęcie” wraca |
| ISSUE-016: styl B | 1a, 6 | reguły 11 i 14 (puste miejsce na zdjęcie tylko jako przycisk); przegląd `ui` przed stopem #2 |
| ISSUE-017: profilowe osoby (v4) | 5 | karta osoby ze zdjęciem ma z lewej okrąg z profilowym; po „Ustaw jako profilowe” i „Zapisz” w formularzu okrąg pokazuje nowe; osoba bez zdjęć — karta bez wcięcia |
| ISSUE-017: zdjęcie dzielone (v4) | 5 | po zaznaczeniu drugiej osoby z grobu na zdjęciu, które dla niej jest pierwsze, jej karta też pokazuje to zdjęcie |
| US-008 AC-2 — postaw pinezkę (v7) | 4 → [[cmentarz]] 12 | grób bez pinezki → „Postaw pinezkę” → tryb D → „Zapisz pinezkę” → mapa z nowym zniczem; po powrocie do grobu „Pinezka: GPS ±5 m · 12.10.2026” zamiast „· bez pinezki” |
| ISSUE-043 AC-1 (v8) | 7 → 3c | grób bez daty → „Wpisz” → „2031” → `done` → na dole „Opłacone do” · „2031”, bez „Wpisz”; ✎ → pole ma „2031” → „03.2031” → „Zapisz” → „03.2031” |
| ISSUE-043 AC-2 (v8) | 7 | grób bez wpisu: „Opłacone do” · „nie wiadomo” (W1) albo brak wiersza (W2); nigdzie daty, której nie wpisano |
| ISSUE-043 AC-3 (v8) | 7 | po odtworzeniu kopii z wersji sprzed pozycji wiersz pokazuje „nie wiadomo”, a reszta grobu jest bez zmian. Po odtworzeniu kopii z datą — ta sama data (`qa`, migracja i próbne odtworzenie) |
| D18 — przyszłość i literówka (v8) | 3c | „2031” zapisuje się; „2301” → „Tak odległa data to raczej pomyłka — sprawdź rok.”; „13.2031” → „Nie rozumiem tej daty…”; okno zostaje, nazwa i adres też się nie zapisują |
| ISSUE-047 AC-1 (v9) | [[cmentarz]] 9a → stan „pusty” | „Dodaj grób” → „Grób rodzinny Wymyślonych” → „Zapisz” → ten widok: tytuł, „W tym grobie nie ma jeszcze wpisanych osób.”, „Dodaj osobę”; formularz osoby się nie otwiera |
| ISSUE-047 AC-2 (v9) | 6 → 8–11 → 5 | „Dodaj osobę” → „Jan” → w „Bez grobu” Jan Wymyślony (dodany w drzewie jako rodzic) → z powrotem tu, karta „Jan Wymyślony”; w zakładce Osoby nadal jeden Jan, jego daty, zdjęcia i rodzina bez zmian |
| ISSUE-047 AC-3 (v9) | 6 → 10 → [[wpis-osoby]] | „Dodaj osobę” → „Anna” → „Nowa osoba: „Anna”” → formularz „Osoba w grobie” z „Anna” w Imionach, nazwisko podpowiedziane z poprzedniej osoby |
| ISSUE-047 — osoba z grobem (v9, D23) | 12 | Jan Zmyślony z innego grobu: wyszarzony, „w grobie: Grób rodzinny Zmyślonych”, dotknięcie nic nie robi; osoba z tego grobu — „już w tym grobie” |

## Decisions
- **D1 — nazwa grobu wpisywana ręcznie, opcjonalna** (decyzja autora 2026-10-06: opcja (b) z wersji 1). Nie
  wyliczamy jej z nazwisk: „Grób rodzinny Nowaków” wymaga odmiany w dopełniaczu liczby mnogiej (Nowak →
  Nowaków, Kowalski → Kowalskich), a zła odmiana na grobie rodziny razi. Wpisaną nazwę autor widzi i
  poprawia. **Bez nazwy tytułem jest „Grób”**, bo pod nim od razu stoją osoby.
- **D2 — nazwa w oknie z ikonki edycji, a nie w formularzu osoby.** Formularz osoby to ok. 100 wpisów
  (G6): pole nazwy kosztowałoby `next` przy każdym nowym grobie i mieszało grób z osobą. Ikonka edycji to ten
  sam wzorzec co poprawa cmentarza ([[cmentarze]] element 8, decyzja autora). Później to samo okno przyjmie
  adres kwatery (wizyta, [[EPIC-002-wizyta]]). *Obali:* autor na stopie #2 nadaje nazwę prawie każdemu
  grobowi i czuje, że okno spowalnia — wtedy pole „Nazwa grobu” w trybie „nowy grób” formularza.
- **D3 — „kim była” nie stoi w karcie.** Lista ma być spokojna jak w R4, a „kim była” (krótka biografia) to
  treść widoku osoby (R4 prawy, M5). **Wyjątek:** jeśli poprawa nie wejdzie do ISSUE-012 ([[wpis-osoby]] →
  *Open* 1), biografii nie byłoby nigdzie widać. Wtedy karta dostaje trzecią linię: początek „kim była” w
  tekście pomocniczym, jedna linia, ucięta.
- **D4 — zdjęcia później, bez miejsc zastępczych.** Z R4 brakuje zdjęcia nagrobka u góry, portretów w kartach
  i „Dodaj zdjęcie” w rzędzie działań. Wszystko to [[US-005-zdjecia]]: zdjęcie stanie nad tytułem, portret z
  lewej w karcie, „Dodaj zdjęcie” obok „Dodaj osobę”. Do tego czasu nie ma szarych prostokątów (reguła 11).
  **Wykonane w v3** — zdjęcie nagrobka i „Dodaj zdjęcie” w [[ISSUE-016-photos-grave-and-person]] (1a, 6, D8–D10);
  portrety w kartach w [[ISSUE-017-person-photos]] (5, D11).
- **D5 — kolejność wpisania**, nie chronologiczna: zgadza się z notatkami, więc łatwo porównać. *Obali:* autor
  na stopie #2 chce widzieć najpierw najstarszych.
- **D6 — daty z dokładnością taką, jak wpisano** (`ok. 1890 – 14.03.1951`), a nie same lata jak w R4: dopisek i
  dokładność to dana (FR-004), a nie szum. Same lata zostają, gdy wpisano same lata.
- **D7 — spór źródeł niewidoczny** — pokazuje się pierwsza wartość; oznaczenie to US-004.
- **D8 — zdjęcie nagrobka w proporcji zdjęcia, nie wyżej niż szerokość** (v3). Stała proporcja 4:3 ucinałaby
  pionowy nagrobek z góry i z dołu, a to on ma posłużyć do rozpoznania grobu (brief §4a krok 3). Zdjęcie
  poziome i kwadratowe widać więc w całości, a dopiero wyższe od kwadratu jest przycięte ze środka, żeby imiona
  osób nie zjechały za ekran. Całość jest zawsze o jedno dotknięcie dalej, w podglądzie. *Obali:* na stopie #2
  przycięcie pionowych zdjęć zabiera napis z tablicy — wtedy całe zdjęcie z pasami po bokach na powierzchni.
- **D9 — jedno zdjęcie nagrobka** (decyzja autora, stop #1 ISSUE-016: *„nagrobek — wystarczy mi jedno
  zdjęcie”*). Zmiana zastępuje zdjęcie, a „Dodaj zdjęcie” widać tylko bez zdjęcia. Wersja z kilkoma zdjęciami
  (przesuwanie, licznik „1 / 3”) odpada; przesuwanie i przyciski ‹ › wracają w bazie zdjęć osoby
  ([[ISSUE-017-person-photos]]).
- **D10 — „Dodaj osobę” zostaje z lewej** (z ISSUE-012). ~~„Dodaj zdjęcie” obok~~ — zastąpione przez D12 (v3.2).
- **D12 — „Dodaj zdjęcie” w miejscu zdjęcia** (v3.2, decyzja autora na stopie #2 ISSUE-016). Działanie stoi tam, gdzie
  pojawi się jego wynik, więc nie trzeba go szukać w rzędzie przycisków. To przycisk z obrysem, ikoną w akcencie i
  podpisem, a nie zastępczy obrazek ([[style-b]] reguły 11 i 14 — tak samo jak puste zdjęcie osoby w [[wpis-osoby]]
  v3). **Wysokość 120 dp, nie 4:3:** ok. 50 grobów zaczyna bez zdjęcia, a pole wielkości zdjęcia (ok. 250 dp)
  spychałoby osoby i „Dodaj osobę” na każdym z nich; 120 dp wystarcza, żeby czytało się jako „tu będzie zdjęcie”.
  *Obali:* autor chce pola wielkości zdjęcia — wtedy 4:3 i bez przeskoku po dodaniu.
- **D11 — karta osoby bez zdjęcia nie ma wcięcia** (kierunek z v3, wchodzi w [[ISSUE-017-person-photos]], v4). Reguła 11 zabrania zastępczych obrazków, a puste wcięcie
  wyglądałoby jak brakujące zdjęcie. Koszt: w grobie, gdzie część osób ma zdjęcie, imiona nie stoją w jednej linii.
  *Obali:* na stopie #2 karty mieszane wyglądają nierówno — wtedy wcięcie 52 dp bez obrazka u wszystkich, gdy
  choć jedna osoba w grobie ma zdjęcie.
- **D13 — adres zarządcy w oknie „Popraw grób”, z widocznym „Wpisz adres”** (v6 — propozycja na stop #1
  [[ISSUE-028-cemetery-sectors]]). Nazwa i adres to dane grobu, a poprawa ma jedno wejście — ✎ ([[style-b]] reguła 15), więc nie
  ma drugiego okna. „Wpisz adres” przy braku adresu jest skrótem do tego samego okna, bo ✎ przy tytule nie mówi, że tam jest
  adres. Rząd i miejsce to tekst, nie liczby, bo zarządcy piszą „12a” i „IV”. *Obali:* autor wpisuje adresy seriami (wiele grobów
  pod rząd z jednej wyszukiwarki) — wtedy adres w karcie listy [[cmentarz]] C bez wchodzenia w grób.
- **D14 — pinezka w widoku grobu: „Postaw” tak, „Popraw” nie** (v7, [[ISSUE-029-pin-on-site-gps]]). Grób bez pinezki nie ma
  znicza na mapie, więc jedyną drogą do trybu D jest ten widok (do niego prowadzi lista [[cmentarz]] C). Grób z pinezką ma znicz, a
  „Popraw pinezkę” stoi przy nim na mapie ([[cmentarz]] 11) — tam widać, gdzie pinezka jest teraz. Drugie wejście tutaj dublowałoby
  działanie. Linia źródła to fakt, nie przycisk. *Obali:* przy wizycie autor, patrząc na grób z pinezką w tym widoku, szuka, jak ją
  poprawić — wtedy linia źródła staje się przyciskiem do trybu D.
- **D15 — „Opłacone do” na samym dole, pod „Dodaj osobę”** (v8, decyzja autora 2026-10-16: *„można dodać na samym dole profilu grobu”*).
  Górę widoku zajmuje to, po czym rozpoznaje się grób (zdjęcie, nazwa, adres, pinezka), a środek osoby. Opłatę sprawdza się rzadko, więc
  nie spycha osób ani „Dodaj osobę”. *Obali:* przy wpisywaniu z naklejek autor przewija przy każdym grobie i to przeszkadza — wtedy wiersz
  pod adresem (element 4).
- **D16 — grób bez daty ma wiersz „nie wiadomo” z „Wpisz” (W1), a nie brak wiersza (W2)** (v8, AC-2). Wiersz pokazuje, przy których grobach
  daty jeszcze nie ma, a o to chodzi na Wszystkich Świętych. Bez wiersza nic nie mówi, że grób ma takie pole, a ✎ przy tytule nie mówi, że
  tam jest opłata, tak jak nie mówił o adresie (D13). Koszt: do czasu wpisania jedna linia w tekście pomocniczym na ok. 50 grobach.
  *Obali:* na stopie #1 albo #2 wiersz przy każdym grobie wygląda jak upominanie — wtedy W2, czyli wiersz tylko z datą i wpis pod ✎.
- **D17 — wiersz to fakt, nie przycisk; poprawa pod ✎** (v8, [[style-b]] reguła 15). „Wpisz” jest skrótem tylko przy braku daty, jak „Wpisz
  adres” (D13). Grób z datą ma jedno wejście do poprawy, tak jak linia źródła pinezki (D14). *Obali:* autor przy poprawie dotyka daty i szuka,
  gdzie ją zmienić — wtedy cały wiersz otwiera okno z fokusem w 3c.
- **D18 — sama data, bez dopisku, z przyszłością** (v8). Termin opłaty to fakt z dokumentu (naklejka, pokwitowanie), a przypomnienie
  potrzebuje jednej daty, więc pole nie ma „ok.”, „przed”, „po” ani „między”. Zapis jak przy innych datach: `rrrr` · `mm.rrrr` · `dd.mm.rrrr`.
  Opłata jest zwykle na przyszłość (co 20 lat), a pole daty osoby nie przyjmuje lat późniejszych niż bieżący. To pole przyjmuje je
  **do bieżącego roku + 50**: literówka „2301” zamiast „2031” dostaje komunikat, a prawdziwe opłaty na 20–25 lat się mieszczą.
  *Obali:* autor zna termin tylko z pamięci („chyba do 2030”) — wtedy dopisek „ok.”. Albo zarządca daje opłatę dłuższą niż 50 lat — wtedy
  wyższy próg.
- **D19 — bez stanu „bez terminu” i bez oznaczenia opłaty, która minęła** (v8, zakres B — decyzja autora w `/pm` 2026-10-16: sama data, bez
  przypomnienia). Data, która minęła, wyświetla się jak każda („Opłacone do” · „2019”), bez koloru i bez dopisku: fakt mówi sam za siebie.
  Wyróżnianie takich grobów to część przypomnienia, które przyjdzie później aktualizacją ze sklepu, przed najwcześniejszą zapisaną datą.
  „Bez terminu” (grób, za który nie płaci się okresowo) nie występuje w briefie: S4 i G4 mówią o 20-letniej opłacie za grób ziemny. Pusta
  data znaczy więc „nie wiadomo”. *Obali:* przy wpisywaniu w trakcie wyjazdu część grobów okazuje się bez terminu, a „Wpisz” przy nich
  przeszkadza — wtedy wybór „bez terminu” w oknie: nowa kolumna i migracja na prawdziwych danych, z migawką
  ([[ISSUE-041-google-play-and-safe-update]]).
- **D20 — okno samo przewija się do 3c** (v8.1, odstępstwo `dev` przyjęte w przeglądzie `ui` 2026-10-16). Pole opłaty jest ostatnie w długim oknie,
  a własne przewijanie pola tekstowego go nie wyciągało: przy tekście 200% z klawiaturą „Wpisz” dawało fokus i klawiaturę numeryczną, ale widać było
  „Rząd” i „Miejsce”, a nie pole. Dlatego przy fokusie w 3c, przy zmianie wysokości klawiatury i przy błędzie okno stawia pole u góry widocznej części.
  Bez 16 dp nad polem etykieta nad ramką była ucięta do połowy. Pierwszeństwo ma pole z etykietą, a nie koniec podpowiedzi: przy 200% z klawiaturą
  „Zostaw puste, jeśli nie wiesz.” jest pod krawędzią i widać je po przewinięciu (SC 1.4.10). Do tego zachowania nie ma reguły w [[style-b]], bo to
  jedna instancja. Gdy to samo okaże się potrzebne w drugim oknie (np. „Popraw cmentarz”, *Open* — luka v6.1), powstanie reguła.
  *Obali:* na stopie #2 przeskok okna przy otwieraniu klawiatury przeszkadza — wtedy przewinięcie raz, po ustaleniu się klawiatury.
- **D21 — podpowiedź pod 3c bez limitu linii, tekst bez zmian** (v8.1, odstępstwo `dev` przyjęte w przeglądzie `ui` 2026-10-16). Pomiar (Roboto z
  emulatora, 13 sp, łamanie jak we Flutterze, sprawdzone na zrzutach przy 100% i 200%): obecny tekst ma 3 linie przy 100% na 411 i 360 dp i 5 przy 200%
  na 360 dp. Propozycja `dev` („Rok albo data z naklejki lub pokwitowania. Puste — nie wiadomo.”) ma 2 linie tylko na 411 dp. Na 360 dp ma 3, z
  samym „wiadomo.” w ostatniej linii, a przy 200% — 5, z „Puste — nie⏎wiadomo.”. Zmienia też głos: obie podpowiedzi w tym oknie mówią „Zostaw puste…”
  ([[style-b]] reguła 7 — aplikacja zwraca się do Ciebie). Szkic v8 i tak miał 3 linie. Koszt: jedna linia (ok. 16 dp) więcej w oknie, które się
  przewija. *Obali:* autor na stopie #2 uznaje podpowiedź za za długą — wtedy „Rok albo data z naklejki na grobie. Zostaw puste, jeśli nie wiesz.”
  (2 linie na 411 dp, 4 przy 200%; bez pokwitowania).
- **D22 — „Dodaj osobę” najpierw szuka** (v9 — przyjęte na stopie #1 (autor: „Tak”, 2026-10-18), [[ISSUE-047-grave-first-then-people]]; autor 2026-10-18: *„powinienem móc albo
  wybrać z istniejącej listy, albo dodać nową osobę do rodziny”*). Osoby trafiają do aplikacji dwiema drogami — z grobu i z drzewa (arkusz rodziny,
  rodzice i dzieci bez grobu) — a do v8.1 nie było drogi, by osobę z drzewa przypiąć do grobu znalezionego później: zostawało wpisać ją drugi raz.
  Duplikat w danych genealogicznych to najdroższa poprawka, a scalania osób nie ma. Wzór „najpierw szukaj, potem nowa” już działa w [[rodzina]] (D3,
  US-003 AC-5 — osoba z grobu w rodzinie); tu ten sam wybór w drugą stronę, ten sam kod (`PersonChoiceList`). **„Bez grobu” na górze**, bo to
  jedyne osoby, które da się tu wybrać. Wybór zapisuje od razu, bez formularza i bez „Zapisz”: to wskazanie, a nie wpis do poprawy (jak tło w
  [[osoba]] D21 i zdjęcie nagrobka). Koszt: 1 dotknięcie więcej na każdą nową osobę (*Tempo*). *Obali:* przy przepisywaniu notatek prawie każda
  osoba jest nowa i wybór spowalnia — wtedy „Dodaj osobę” prosto do formularza, a wybór pod osobnym „Wybierz z aplikacji”.
- **D23 — osoba, która ma już grób, jest nieaktywna z powodem** (v9). Model umie zapisać dwa groby jednej osoby ([[ADR-006-claimed-value-separate-structures]]
  — pokazuje się w obu), ale **w aplikacji nie ma usuwania pochówku** ([[wpis-osoby]] *Decisions* → „Bez usuwania osoby”, brief G7/C5), więc
  dotknięcie złego „Jana” zostawiłoby go w dwóch grobach na zawsze. Wiersz zostaje widoczny, bo bez niego autor szukający Jana, który już leży w
  tym albo innym grobie, nic by nie znalazł i wpisałby go jako nową osobę — czyli duplikat. Powód tekstem mówi, gdzie ta osoba jest. *Obali:* w
  notatkach ktoś jest na dwóch nagrobkach (np. napis symboliczny na grobie rodzinnym) — wtedy wiersz aktywny z oknem „Dodać także do tego grobu?”
  albo usuwanie pochówku, osobną pozycją.
- **D24 — pusty grób to zwykły stan, bez usuwania** (v9). Autor chce dodać grób, a osoby potem — przy wizycie najpierw zdjęcie i pinezka, osoby w domu
  z notatek. Pusty grób, z którego autor wyszedł, zostaje na liście cmentarza („bez wpisanych osób”, [[cmentarz]] *States*) i nie znika sam: grób
  ma nazwę, adres, pinezkę i opłatę, które mogą być prawdziwe. Usuwania nie ma tak samo jak dla osób. *Obali:* jak [[cmentarz]] D38 (2).
- **D25 — wybór osoby wygląda jak zbudowany wybór w arkuszu rodziny** (v9.1, przegląd `ui` 2026-10-18). To ten sam widżet (`PersonChoiceList`), więc
  dwa wybory osoby w aplikacji mają wyglądać tak samo: pole z ramką w kolorze obrysu ([[rodzina]] B2), nagłówki sekcji 14 sp półgrube ([[rodzina]] A2).
  „13 sp” w v9 było błędem przepisania. *Obali:* nagłówki sekcji przy wierszach 16 sp wyglądają na stopie #2 jak druga lista — wtedy zmiana w obu
  wyborach naraz.
- **D26 — pusty grób: zdanie 40 dp pod adresem** (v9.1, przegląd `ui` 2026-10-18 — tak zbudowane, przyjęte). Pusty stan to kompozycja wyśrodkowana, a
  takie biorą większy odstęp z tej samej siatki ([[style-b]] reguła 5); zdanie odsuwa się od przycisku „Postaw pinezkę” nad nim i stoi bliżej „Dodaj
  osobę”, do którego prowadzi. *Obali:* na stopie #2 zdanie wygląda na zawieszone w pustce, a nie na miejsce, gdzie staną osoby — wtedy 24 dp.

## Open
- ✅ **Rozstrzygnięte 2026-10-12 na stopie #1 [[ISSUE-028-cemetery-sectors]] (autor: „tak”):** adres zarządcy wchodzi do ISSUE-028, a
  pole „Kwatera” działa w wariancie **W-a** (chipy kwater cmentarza, odnośnik — [[ADR-016-sector-record-and-grave-link]]). v6 obowiązuje.
- **Znana luka (przegląd `ui` ISSUE-028, v6.1):** przy 360 × 640 dp, tekście 200% i otwartej klawiaturze okno „Popraw grób” pokazuje na
  raz ok. dwie linie, resztę przewijaniem — wszystkie pola są osiągalne (SC 1.4.10). Okno na cały ekran przy dużym tekście dotyczy też
  „Popraw cmentarz”, więc o wzorcu decyduje się przy drugim oknie z tym problemem. Kolejność chipów — [[cmentarz]] 17a.

- **v8 ([[ISSUE-043-grave-paid-until]]):** nowych `⚠️ OPEN` nie ma. Oba pytania z pozycji (przypomnienie, „kto płaci”) rozstrzygnął autor
  w `/pm` 2026-10-16 (wariant B). ✅ **W1 przyjęte na stopie #1** (autor: „Tak”, 2026-10-16; D16).
- **Znana luka v8:** pole 3c wydłuża okno „Popraw grób”. Przy tekście 200% z otwartą klawiaturą okno jest jeszcze dłuższe (luka v6.1 wyżej).
  ~~„Wpisz” przewija okno do pola, ale wejście przez ✎ wymaga przewinięcia do końca.~~ **v8.1 (D20):** okno przewija się do 3c przy każdym fokusie
  w tym polu, także z `next` w „Miejsce”. Przez ✎ fokus jest w nazwie, więc do 3c prowadzą cztery `next` albo przewinięcie i dotknięcie pola. Przy
  200% z klawiaturą koniec podpowiedzi 3c widać dopiero po przewinięciu.

- **v9 ([[ISSUE-047-grave-first-then-people]]):** oba `⚠️ OPEN` z pozycji rozstrzygnięte projektem — osoba z grobem: D23; porzucony pusty grób:
  D24, [[cmentarz]] D38. ✅ Przyjęte na stopie #1 razem z makietą (autor: „Tak”, 2026-10-18).

Usuwanie i zmiana zdjęcia nagrobka rozstrzygnięte na stopie #1 ISSUE-016 (wchodzą — [[zdjecie]] B4, C). Poprawa wpisu
rozstrzygnięta na stopie #1 ISSUE-012 (D1 — wchodzi).
