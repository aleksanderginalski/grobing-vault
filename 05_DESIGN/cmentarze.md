---
screen: "Ekran główny — mapa Polski z cmentarzami rodziny"
items: ["[[ISSUE-012-transcribe-grave-screen]]", "[[ISSUE-014-home-map-of-poland]]"]
us: "[[US-002-przepisanie-grobu]]"
journey-step: "UJ-001 · 1 (widok 1, M2) · warunek kroku 1: dodanie cmentarza (M1)"
mockup: "katalog tymczasowy sesji 2026-10-06: makieta-mapa-polski.html (ramki 1–10, wersja 2 po stopie #1)"
updated: 2026-10-06
---

# Ekran główny — mapa Polski — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.4) · referencja: [[references]] → **R1**.
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
  - wynik „Z bazy cmentarzy” → **podgląd** (14) → „Dodaj ten cmentarz” → **okno** (15) → zapis → mapa z
    nowym zniczem i arkuszem;
  - „Nie ma go w bazie — dodaj ręcznie” → **okno** (15) → **tryb wskazania** (16–17) → zapis.
- **Ikonka edycji w arkuszu** → okno „Popraw cmentarz” (15) → tryb wskazania (16–17) z obecnym zniczem.
- **Wstecz:** z trybu wskazania → okno z wpisanymi wartościami; z okna → poprzedni widok bez zapisu; z
  podglądu → wyniki z tym samym tekstem; z wyszukiwania → mapa; z otwartego arkusza → zamyka arkusz; z
  mapy → wyjście z aplikacji.
- **Bez dolnej nawigacji** Mapa · Osoby · Drzewo — pojawi się z drugim celem ([[style-b]] reguła 12).

## Elements in order
**Mapa (ekran główny)**

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek: **ikona znicza (akcent) + „Grobing”** (półgruby, 22 sp); po prawej koło zębate (`settings_outlined`, tekst pomocniczy, `tooltip` „Ustawienia”) | pasek | koło → „Stan danych” | — | — | R1 · *What to build* 5 · [[style-b]] reguła 8 |
| 2 | **Wyszukiwarka:** pigułka na powierzchni, wys. 56 dp, margines 16 dp, ikona `search` (tekst pomocniczy), podpowiedź **„Szukaj cmentarza”** | pole (tylko wejście) | dotknięcie → tryb wyszukiwania (10) | pusto | — | R1 · *What to build* 3 · D2 |
| 3 | **Mapa Polski**: ląd w kolorze powierzchni, granica w kolorze obrysu (1,5 dp), rzeki jako dekoracja, **9 miast** (kropka 4 dp + podpis 13 sp, tekst pomocniczy, z obwódką 2–3 dp w kolorze lądu — [[style-b]] reguła 13): Szczecin, Gdańsk, Białystok, Poznań, Warszawa, Łódź, Wrocław, Lublin, Kraków | mapa | szczypanie, przeciąganie, podwójne dotknięcie; ruch ograniczony do Polski; najmniejsze przybliżenie = cała Polska z marginesem 16 dp, **a od dołu o wysokość arkusza (ok. 150 dp)**, żeby Polska stała pod wyszukiwarką, nad strefą arkusza (przegląd `ui`, 2026-10-06); bez obrotu; dotknięcie pustego miejsca zamyka arkusz | cała Polska, północ u góry | — | R1 · *What to build* 1 · D9, D14 |
| 4 | **Znicze cmentarzy** w punkcie cmentarza: pinezka w akcencie z sylwetką znicza w kolorze tła, 32 × 40 dp, **cel dotyku 48 × 48 dp**. Wybrany: 40 × 50 dp z poświatą. **Znicze, których cele nachodzą na siebie, łączą się w jeden znicz z liczbą** (plakietka: powierzchnia, obrys w akcencie, cyfra w kolorze tekstu). Znicz rysuje się nad podpisami miast | znaczniki | dotknięcie → arkusz (6) albo arkusz grupy (9); mapa przesuwa się tak, żeby znicz (także znicz z liczbą) nie stał pod arkuszem — według wysokości narysowanego arkusza | — | cmentarz bez punktu nie ma znicza | R1 · *What to build* 2 · AC-2 · D8 |
| 5 | **Stan pusty:** karta na powierzchni na dole: „Tu pojawią się cmentarze rodziny.” (tekst pomocniczy) + **wypełniony „Dodaj cmentarz”** (`add_location_alt_outlined`) | karta + przycisk główny | → tryb wyszukiwania (10) z podpowiedzią „Wpisz nazwę cmentarza albo miejscowość” | — | — | AC-1 · [[style-b]] reguła 9 · D16 |

**Arkusz cmentarza** — dolny arkusz na powierzchni do krawędzi ekranu (treść nad paskiem gestów), promień 16 dp, uchwyt: przeciągnięcie w dół zamyka arkusz jak dotknięcie mapy; mapa pod nim działa

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 6 | **Nazwa** (tekst, 18 sp, półgruby, do 2 linii) · **miejscowość** (tekst pomocniczy, 14 sp) · ikona `people_outline` + **„6 grobów · 14 osób”** (tekst pomocniczy, odmiana — [[style-b]] reguła 6). Bez punktu: ikona `location_off_outlined` + „Bez punktu na mapie” | tekst | — | — | — | R1 · *What to build* 4 · AC-4 · D13 |
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
| 12 | **Wyniki (od 2 znaków)** w dwóch sekcjach. **„Twoje cmentarze”** — karty jak w 11, które pasują. **„Z bazy cmentarzy”** — karty: **nazwa** (16 sp, półgruby; brak nazwy → „Cmentarz bez nazwy” w kolorze pomocniczym) · **„Miejscowość · woj. mazowieckie”**, w mieście z dzielnicą w nawiasie, i „· rzymskokatolicki”, gdy baza zna wyznanie (tekst pomocniczy) · chevron. Cmentarz z bazy, który już jest u Ciebie (punkt bliżej niż 100 m), ma zamiast chevronu „Dodany” (tekst pomocniczy) i prowadzi do jego arkusza. Najwyżej 30 wyników z bazy; więcej → „Pokazuję 30 z 214 — dopisz miejscowość.” Pod sekcją: „Dane: © współtwórcy OpenStreetMap (ODbL)” (13 sp, tekst pomocniczy). Na końcu przycisk tekstowy **„Nie ma go w bazie — dodaj ręcznie”** | dwie listy kart + przycisk tekstowy | karta z bazy → podgląd (14); „dodaj ręcznie” → okno (15) z nazwą = tekst | twoje alfabetycznie; z bazy: najpierw trafienia w nazwie, potem w miejscowości, w grupie alfabetycznie | — | AC-3 · D3, D16, D17 |
| 13 | **Brak wyników w obu sekcjach:** „Nie ma cmentarza „<tekst>” ani u Ciebie, ani w bazie.” (tekst pomocniczy) + **wypełniony „Dodaj ręcznie”** | tekst + przycisk główny | → okno (15) z nazwą = tekst | — | — | AC-3 |

**Podgląd cmentarza z bazy** — przed dodaniem

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 14 | Pasek: wstecz + „Cmentarz z bazy”. **Mapa przybliżona do punktu** z **zniczem w obrysie** (niezapisany, [[style-b]] reguła 13) i zapisanymi zniczami w okolicy. Karta na dole: nazwa (18 sp, półgruby), „Miejscowość · woj. …”, wyznanie, jeśli jest. Link **„Zobacz zdjęcie satelitarne ↗”** (akcent, podkreślony) i **wypełniony „Dodaj ten cmentarz”** | mapa + karta | link → zewnętrzna aplikacja map w tym punkcie (`geo:`), tylko po dotknięciu; „Dodaj…” → okno (15) z danymi z bazy | — | — | **decyzja autora** (pewność miejsca) · D18, D19 |

**Okno i tryb wskazania**

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 15 | **Okno** „Nowy cmentarz” / „Popraw cmentarz”: **Nazwa** (wielka litera na początku słów, `next`), **Miejscowość** (opcjonalna, `done`). Przyciski: z bazy „Anuluj” · **„Zapisz”** (punkt jest z bazy); ręcznie i przy poprawie „Anuluj” · **„Dalej”** → wskazanie. Fokus w pierwszym pustym polu | okno dialogowe, pola z ramką w kolorze obrysu | „Zapisz” → zapis → mapa z nowym zniczem i arkuszem; „Dalej” → 16 | **z bazy:** nazwa i miejscowość z bazy; cmentarz bez nazwy → pusta nazwa z podpowiedzią „np. Cmentarz parafialny”. **Ręcznie:** nazwa z wyszukiwarki (wielka litera na początku słów). **Poprawa:** obecne wartości | nazwa wymagana: „Podaj nazwę cmentarza.” (kolor błędu + `error_outline`), okno zostaje | *What to build* 3 · D6, D20 |
| 16 | **Tryb wskazania:** pasek „Wskaż cmentarz na mapie” z `close` (→ okno 15); u góry karta: „Dotknij miejsca, gdzie leży <nazwa>. Mapę możesz przybliżyć.” (tekst pomocniczy). **Dotknięcie mapy stawia znicz w stylu wybranego, kolejne go przesuwa.** **Zapisane znicze są widoczne w zwykłym wyglądzie i nieaktywne**, żeby dało się postawić cmentarz obok innego (D21; przegląd `ui`, 2026-10-06). Wyszukiwarki nie ma | mapa w trybie wyboru | gesty jak 3 | przy poprawie: obecny znicz | — | *What to build* 3 |
| 17 | Dół, na powierzchni: **„Zapisz bez punktu”** (tekstowy) · **„Zapisz”** (wypełniony; aktywny po postawieniu znicza, przy poprawie z punktem od razu). Przy poprawie „Zapisz bez punktu” zdejmuje znicz z mapy | przyciski | zapis przez API danych → mapa z wybranym zniczem (bez punktu: sam arkusz) | — | błąd zapisu: „Nie udało się zapisać. Spróbuj jeszcze raz.” (kolor błędu + ikona); tryb zostaje | DoD (kopia w tle) · [[style-b]] reguła 10 |

Liczby odmieniają się po polsku: 1 grób · 2–4 groby · 5+ grobów (też 12–14 grobów, 22–24 groby) · 0
grobów; tak samo osoba / osoby / osób i cmentarz / cmentarze / cmentarzy.

## States
| Stan | Co widać |
|---|---|
| pusty | pasek, wyszukiwarka, **cała mapa Polski** (także w trybie samolotowym, AC-1) i karta z elementu 5 |
| wczytywanie | kontur rysuje się od razu z danych w aplikacji; znicze pojawiają się po odczycie bazy. Bazę cmentarzy Polski aplikacja wczytuje przy pierwszym wejściu w wyszukiwarkę, bez wskaźnika, chyba że trwa dłużej niż ok. 0,3 s — wtedy cienki pasek postępu pod polem |
| błąd | **odczyt bazy danych:** mapa zostaje, na dole karta „Nie udało się odczytać cmentarzy.” + „Spróbuj ponownie” (z obrysem). **Dane wbudowane** (mapa, baza cmentarzy; błąd = usterka aplikacji): w miejscu mapy „Nie udało się narysować mapy.”, a w wyszukiwarce sekcja z bazy zastąpiona tekstem „Baza cmentarzy jest niedostępna — dodaj ręcznie.” Wyszukiwanie wśród twoich i dodanie ręczne działają. **Zapis:** element 17. **Okno:** element 15 |
| wypełniony | znicze bez arkusza; nic nie jest wybrane |
| wybrany | znicz powiększony z poświatą, arkusz cmentarza (6–8) |
| grupa | znicz z liczbą powiększony, arkusz grupy (9) |
| wyszukiwanie | pusty tekst (11) · wyniki (12) · brak wyników (13) |
| podgląd | element 14 |
| wskazywanie | elementy 16–17 |

## Sketch
```
 wyszukiwanie: wyniki                 podgląd cmentarza z bazy
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│ ←  parafialny wymys            ✕ │  │ ←  Cmentarz z bazy               │
│  Twoje cmentarze                 │  │                                  │
│  (brak)                          │  │        ·Wymyślin                 │
│  Z bazy cmentarzy                │  │              ◌  ← znicz w obrysie│
│ ╭──────────────────────────────╮ │  │                                  │
│ │ Cmentarz parafialny        › │ │  │ ╭──────────────────────────────╮ │
│ │ Wymyślin · woj. mazowieckie  │ │  │ │ Cmentarz parafialny          │ │
│ │ · rzymskokatolicki           │ │  │ │ Wymyślin · woj. mazowieckie  │ │
│ ╰──────────────────────────────╯ │  │ │ rzymskokatolicki             │ │
│ ╭──────────────────────────────╮ │  │ │ Zobacz zdjęcie satelitarne ↗ │ │
│ │ Cmentarz bez nazwy         › │ │  │ │ ╭──────────────────────────╮ │ │
│ │ Wymyślin Mały · woj. mazow.  │ │  │ │ │    Dodaj ten cmentarz     │ │ │
│ ╰──────────────────────────────╯ │  │ │ ╰──────────────────────────╯ │ │
│  Dane: © współtwórcy OSM (ODbL)  │  │ ╰──────────────────────────────╯ │
│  Nie ma go w bazie — dodaj ręcznie│ └──────────────────────────────────┘
└──────────────────────────────────┘
 arkusz cmentarza (ikonka edycji w prawym górnym rogu)
┌──────────────────────────────────┐
│ ═══                              │
│ Cmentarz Wymyślony 1          ✎ │
│ Miejscowość Testowa              │
│ 👥 2 groby · 3 osoby             │
└──────────────────────────────────┘
```

## Tempo
Ekran do wybierania; wpisywanie jest rzadkie. Rekordem jest **cmentarz**: ok. 10 na całe notatki.
- **Otwarcie cmentarza:** znicz → „Otwórz cmentarz” = **2 dotknięcia** (przy zniczu z liczbą 3).
- **Nowy cmentarz z bazy:** wyszukiwarka + 1–2 słowa → wynik → (podgląd) „Dodaj ten cmentarz” → (okno)
  „Zapisz” = **4 dotknięcia** poza pisaniem. Nic nie trzeba przepisywać ani wskazywać.
- **Ręcznie (zapas):** jak wcześniej, ok. 7 akcji poza pisaniem.

## Style B rules applied
- **Reguła 1:** jeden wypełniony przycisk w danym stanie: „Dodaj cmentarz” (pusty), „Otwórz cmentarz”
  (arkusz), „Dodaj ten cmentarz” (podgląd), „Dodaj ręcznie” (brak wyników), „Zapisz” (wskazanie). Link
  „Zobacz zdjęcie satelitarne ↗” ma formę linku zewnętrznego.
- **Reguła 2:** arkusz, karty i karta podglądu na powierzchni, promień 16 dp. Poświata tylko przy wybranym
  zniczu i głównym przycisku.
- **Reguła 3:** ikony `outlined`; w akcencie przy działaniach (ikonka edycji, „Dodaj cmentarz”).
- **Reguła 4:** „Grobing” i nazwy cmentarzy półgrube.
- **Reguła 6:** liczby odmienione po polsku.
- **Reguła 7:** brak opisany faktem („Bez punktu na mapie”, „Cmentarz bez nazwy”), bez ostrzeżenia.
- **Reguła 8:** znicz w logo, w pinezce i na „Otwórz cmentarz”. „Dodaj”, ikonka edycji i „Zapisz” go nie
  mają.
- **Reguły 9 i 10:** pusty stan z jednym działaniem. Po zapisie widać zapisany znicz i jego arkusz.
- **Reguła 11:** karty z chevronem w wyszukiwarce, wiersze w arkuszu grupy; bez miniatur.
- **Reguła 12:** koło zębate → „Stan danych”; bez dolnej nawigacji.
- **Reguła 13 (mapy):** role kolorów na mapie, znicz-pinezka i **znicz w obrysie dla cmentarza jeszcze nie
  dodanego** (podgląd).
- **Tokeny wchodzące tą pozycją** (zmierzone w [[style-b]] → *Measurement*; do `theme.dart` wpisuje je
  `dev`): **obrys** `#6B6862` (3,40:1 na tle, 3,10:1 na powierzchni) i **błąd** `#E07A6F` (6,45:1 i
  5,89:1, zawsze z ikoną).
- **Ikona znicza**, jedna na całą aplikację:
  - **sylwetka:** szklany znicz (prostokąt lekko zwężony ku dołowi, z kołnierzem u góry) i płomień w kształcie
    kropli nad nim;
  - **wersja liniowa** (logo, ikona przycisku): kreska 1,5 dp w siatce 24 dp, jak ikony `outlined`;
  - **wersja wypełniona** (wnętrze pinezki): sylwetka w kolorze tła na bursztynowej pinezce.

## AC → element
| AC (ISSUE-014) | Element(y) | Jak widać spełnienie |
|---|---|---|
| Po starcie bez sieci widać mapę Polski, także pustą | 3, 5 · stan „pusty” | tryb samolotowy → start → kontur, miasta i rzeki; karta „Tu pojawią się cmentarze rodziny.” |
| Cmentarz z punktem jest zniczem; cmentarz bez punktu znajduje wyszukiwarka | 4 · 11 | zapis z punktem (z bazy albo wskazany) → znicz; zapis bez punktu → brak znicza, karta w 11 z „· bez punktu na mapie” |
| Wyszukiwarka znajduje po nazwie albo miejscowości; brak wyników → „Dodaj cmentarz” | 12, 13 | tekst z nazwy i z miejscowości daje karty w obu sekcjach; tekst bez trafień daje 13 |
| Arkusz pokazuje liczbę grobów i osób | 6 | „2 groby · 3 osoby” zgodne z danymi. Otwarcie ekranu cmentarza → ISSUE-012 (D5) |
| „Stan danych” pod kołem zębatym; ekranu startowego nie ma | 1 · *Navigation* | start → od razu mapa; koło → „Stan danych” |
| Ekran według specyfikacji `ui` i wytycznych stylu B | całość | *Style B rules applied*; przegląd `ui` przed stopem #2 |
| US-002 AC-1, *Given* „cmentarz w aplikacji” | 12, 14, 15 | cmentarz dodany z bazy istnieje i ma arkusz |
| **Uwaga autora: właściwy cmentarz we właściwym miejscu** | 12, 14 | wynik z województwem i dzielnicą; podgląd na mapie i zdjęcie satelitarne przed dodaniem |

## Decisions
- **D1 — plik przepisany w miejscu**, nazwa zostaje (linki w zamkniętych pozycjach).
- **D2 — podpowiedź „Szukaj cmentarza”** zamiast „Szukaj osoby lub cmentarza” z R1, bo pole nie szuka osób
  (decyzja autora: wyszukiwanie osób nie w ISSUE-014). Tekst z R1 wraca z wyszukiwaniem osób.
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
- **D9 — tylko Polska:** bez sąsiednich krajów, 9 miast wojewódzkich, rzeki jako dekoracja. *Obali:*
  cmentarz za granicą.
- **D10 — bez „tu jesteś” i bez uprawnienia lokalizacji** na tym ekranie.
- **D11 — po zapisie mapa z nowym zniczem i arkuszem**, a nie od razu ekran cmentarza. Widać, gdzie
  cmentarz stanął.
- **D12 — [[NFR-004-czytelnosc-w-sloncu]] nie rozstrzyga się tutaj.** Mapę Polski czyta się przy wyborze,
  dokąd jechać. Nazwa ma kolor tekstu (10,0:1), miejscowość i liczby — pomocniczy (5,0:1, AA). Miara zapada
  przy [[cmentarz]] (ISSUE-012).
- **D13 — liczba osób w arkuszu = różne osoby z pochówkiem w grobach tego cmentarza** (osoba z dwoma
  sprzecznymi pochówkami na tym cmentarzu liczy się raz).
- **D14 — odwzorowanie Merkatora, północ u góry, bez obrotu.**
- **D15 — dla planu:** wymyślone dane w buildzie debug dostają wymyślone punkty w Polsce, w tym dwa w jednym
  miejscu i jeden bez punktu.
- **D16 — baza cmentarzy Polski z OpenStreetMap, wbudowana w aplikację** (decyzja autora po falsyfikatorze:
  8 z 8 cmentarzy autora jest w bazie). Działa bez sieci, a aplikacja dalej nie ma uprawnienia `INTERNET`.
  Licencja ODbL wymaga podpisu, więc pod sekcją wyników jest „© współtwórcy OpenStreetMap (ODbL)”.
  **Miejscowość z granic administracyjnych** (miasto albo gmina), bo z najbliższego punktu była zła w 3 z 8.
  *Obali:* baza nie znajduje cmentarzy z kolejnych notatek — wtedy ręczne dodanie przestaje być zapasem.
- **D17 — dwie sekcje wyników: najpierw „Twoje cmentarze”, potem „Z bazy”.** Wyszukiwarka służy też do
  otwierania zapisanych, a te są ważniejsze od 16 tys. obcych. Cmentarz z bazy, który już masz, jest oznaczony
  „Dodany”, żeby nie dodać go dwa razy.
- **D18 — podgląd przed dodaniem i link „Zobacz zdjęcie satelitarne ↗”.** W bazie są błędy (zmierzone:
  cmentarz o nazwie warszawskiego cmentarza przy wsi w innym województwie), a nazwy miejscowości się
  powtarzają (zmierzone: jedna z miejscowości cmentarzy autora występuje w Polsce 5 razy), więc wybór z samej nazwy nie daje pewności. Kontur kraju nie pokaże
  cmentarza z bliska. Pokaże go zdjęcie satelitarne w zewnętrznej aplikacji map (`geo:`), tak jak link do
  Grobonetu (brief §Security: strona zewnętrzna w przeglądarce). **Koszt prywatności:** dotknięcie wysyła
  punkt do dostawcy map — tylko wtedy, gdy dotkniesz. *Obali:* autor nie chce żadnego wyjścia z aplikacji —
  wtedy link znika, a zostaje województwo, dzielnica i wyznanie.
- **D19 — znicz w obrysie** w podglądzie: cmentarz jeszcze nie jest twój, więc nie wygląda jak zapisany.
- **D20 — nazwa z bazy do poprawy przed zapisem.** Baza często ma tylko „Cmentarz parafialny”. Nazwę, której
  używasz (np. „Cmentarz na Górce”), wpisujesz w oknie. Cmentarz bez nazwy dostaje puste pole z podpowiedzią.
- **D21 — zespół cmentarzy to kilka cmentarzy w aplikacji.** Baza ma osobne cmentarze różnych wyznań przy
  jednej ulicy (zmierzone: jeden wpis notatek = 4 obiekty). Grób należy do konkretnego cmentarza, a blisko
  położone połączą się na mapie w znicz z liczbą (D8). *Obali:* autor chce jednego cmentarza „zespół przy
  ul. X” — wtedy dodaje go ręcznie albo z jednego obiektu i poprawia nazwę.

## Open
brak. Pytania z pierwszej wersji (wyszukiwanie osób, „Otwórz cmentarz” przed ekranem cmentarza) autor
rozstrzygnął na stopie #1 (*„teoretycznie jest ok”* — rekomendacje D4 i D5 planu).
