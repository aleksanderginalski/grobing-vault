---
screen: "Miejsca zamieszkania — sekcja w widoku osoby i w formularzu, okno „Miejsce zamieszkania”, wybór miejsca"
items: ["[[ISSUE-042-places-of-residence]]", "[[ISSUE-045-migration-map]]"]
us: "n/a — pozycja z refinementu 2026-10-16 ([[2026-10-16-retro-04]] → *Product decisions*), bez US; [[EPIC-003-zrozumienie]]"
journey-step: "n/a — widok osoby (M5) i wpis osoby (M1); dane dla [[ISSUE-045-migration-map]]"
mockup: "2026-10-16: makieta-042.html — katalog tymczasowy sesji b20ca21c-…\\scratchpad (ramki 1–5, kandydaci A i N); link w ISSUE-042 → Implementation plan"
updated: 2026-10-17
---

# Miejsca zamieszkania — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.32) · referencja: [[references]] → **R4 prawy** (sekcje widoku osoby).
>
> **Wersja 1 (2026-10-16, `ui` przed planem [[ISSUE-042-places-of-residence]]).** Autor w `/pm`: *„gdzie dana osoba mieszkała w którym momencie
> swojego życia, aby zrobić taką mapę, jak kto się przemieszczał po mapie świata”* i o dokładności: **od ogółu do szczegółu** — kraj
> (punkt w środku kraju) → miasto (środek miasta) → *„albo wręcz dokładną ulicę”*. Dwa wybory dla autora na makiecie: **A** (adres) i **N**
> (nazwa sprzed zmiany granic) — *Open*.
>
> **Wersja 1.1 (2026-10-16, przegląd `ui` zbudowanego ekranu — [[ISSUE-042-places-of-residence]] → *Dev report*).** A i N rozstrzygnięte na stopie #1:
> **A1** i **N2** (*Open*). Przyjęte odstępstwa `dev`: kolejność wyników i szukanie po innych nazwach (D-dev 1, 2 → D9), nazwy jednostek (D-dev 3 →
> element 19), wiersze i karty dla N2 z adresem i z krajem (D-dev 4 → D10), „Ostatnio wybrane” najpierw z kart formularza (D-dev 5 → D11), teksty okien,
> podpowiedź pola wyboru i opis ✕ (D-dev 6 → *Navigation*, 8, 17), dwa stany wyboru zbudowane poza specyfikacją (lista się otwiera, lista się nie
> otworzyła) i łamanie linii lat i miejsca (poprawki z przejścia `dev` → elementy 2, 6, 12, 19; [[style-b]] reguła 6, v1.32). **Zmiana z przeglądu:**
> od 3 liter kraj, którego nazwa zaczyna się od wpisanego tekstu, stoi nad miejscowościami (D8, element 20) — znalezisko `dev` „kraje pod 30
> miejscowościami”. Kod jeszcze tego nie robi: usterka z przeglądu do `dev` ([[ISSUE-042-places-of-residence]] → *Verification*).
>
> **Wersja 1.2 (2026-10-16, stop #2 [[ISSUE-042-places-of-residence]] — decyzja autora).** Autor na stopie #2, przy dwóch wpisanych miejscach „od 2024” i
> „od 2026”: *„czy system wie, że już nie mieszkam [w pierwszym], a [w drugim]? Czy myśli, że w dwóch miejscach mieszkam? Wolałbym, aby od razu zakładał,
> że jeżeli data jest nowsza, to poprzednia wtedy się kończyła”* → po rekomendacji *„tak”*:
> **pobyt bez „Do” kończy się początkiem następnego** — wyliczone przy odczycie, nie zapisane (D12; elementy 2, 6, 10).
>
> **Wersja 1.3 (2026-10-17, `ui` przed planem [[ISSUE-045-migration-map]]).** Pod wierszami w widoku osoby **„Pokaż na mapie”** (element 4a) →
> [[mapa-migracji]]. Mapa liczy koniec pobytu tak samo jak D12, a zamieszkanie bez lat nie stoi na osi czasu ([[mapa-migracji]] D4). *Open* 3 (miejsce
> urodzenia i zgonu) — przy projekcie mapy: **nie w ISSUE-045** ([[mapa-migracji]] D12).
>
> **Wersja 1.4 (2026-10-17, przegląd `ui` zbudowanej [[ISSUE-045-migration-map]]):** ikona „Pokaż na mapie” (4a) to `public_outlined` ([[style-b]] reguła 3;
> v1.3 podawała `public`).

## Purpose
Zbierający zapisuje, **gdzie i kiedy osoba mieszkała** — tak dokładnie, jak wie: sam kraj, miejscowość albo adres — i widzi to w widoku osoby.
Z tych zapisów mapa migracji ([[ISSUE-045-migration-map]]) rysuje, kto gdzie mieszkał w danym roku. Wiedza przychodzi z notatek i od babci, więc
wpis musi przyjąć niepewność: „ok. 1925”, „sam kraj”, bez lat.

## Prior art
- **Zamieszkanie to fakt z okresem i miejscem:** [GEDCOM 7 `INDI-RESI`](https://gedcom.io/terms/v7/INDI-RESI) (miejsce w `PLAC`/`ADDR`, data w
  `DATE`). **Okres zapisuje się `FROM … TO …`**, a `BET … AND …` to nieznana data jednego zdarzenia
  ([GEDCOM 7 — type Date](https://gedcom.io/terms/v7/type-Date); [specyfikacja, typy danych](https://github.com/FamilySearch/GEDCOM/blob/main/specification/gedcom-2-data-types.md)).
  Dzisiejsze „między” w aplikacji ([[wpis-osoby]] blok daty) to `BET` — do okresu się nie nadaje (D3).
- **Dwa miejsca przy zdarzeniu:** FamilySearch zaleca nazwę z czasu zdarzenia i łączy ją z miejscem według dzisiejszej listy, które daje
  punkt na mapie (*„FamilySearch recommends you use the name of the place at the time of the event”* —
  [Family Locket](https://familylocket.com/adding-historical-place-names-in-familysearch);
  [Genea-Musings](https://www.geneamusings.com/2016/01/standardized-historical-and-current.html)) → kandydat N2.
- **Lista miejsc bez sieci:** GeoNames — miejscowości z punktem, nazwy alternatywne według języka (polskie: kod `pl`), licencja CC BY 4.0 (podpis
  źródła w aplikacji) ([Creative Commons — GeoNames](https://wiki.creativecommons.org/wiki/GeoNames)); kraje i ich punkt etykiety — Natural Earth, już
  w aplikacji przy mapie Polski ([[ADR-007-poland-map-bundled-data]]). Zakres i rozmiar listy mierzy `planning`.

## Navigation
- **Widok osoby** ([[osoba]] element 9a, v2.5): sekcja tylko do oglądania; poprawa przez ✎ ([[style-b]] reguła 15). **Bez miejsc** — „Dodaj miejsce”
  otwiera [[wpis-osoby]] „poprawa” z otwartym od razu oknem (A), jak „Dodaj zdjęcie” (D20 w [[osoba]]).
- **Formularz** ([[wpis-osoby]] element 9b, v5.9): karta zamieszkania → ✎ → okno (A) z wpisanymi danymi; „Dodaj miejsce” → okno (A) puste.
  Sekcja jest **w każdym trybie** (także „nowy grób” i „kolejna osoba”), a zapis idzie **razem z „Zapisz”** formularza (D5).
- **Okno (A) „Miejsce zamieszkania”** — pełny ekran nad formularzem. Pole „Miejsce” → **wybór miejsca (B)**; wybór wraca do (A).
  „Gotowe” wraca do formularza i dokłada albo zmienia kartę (zapisu w bazie jeszcze nie ma). ✕ z wpisanymi zmianami → okno „Odrzucić zmiany?”
  — treść „Zmiany w tym miejscu nie zostaną zapisane.” (v1.1) — („Wróć” — akcent · „Odrzuć”), bez zmian — od razu wstecz.
- **Usunięcie:** w oknie (A) otwartym z karty, na dole przycisk tekstowy „Usuń to miejsce” → okno „Usunąć to miejsce zamieszkania?” — treść
  „Zniknie z wpisu po „Zapisz”.” (v1.1) — („Wróć” — akcent · „Usuń”) → karta znika z formularza; z bazy dopiero przy „Zapisz” (formularz da się
  jeszcze odrzucić).
- **Wybór miejsca (B)** — pełny ekran, pole wyszukiwania z fokusem i klawiaturą; wynik → wraca do (A). Wstecz — bez zmiany.

## Elements in order

### Widok osoby — sekcja „Miejsca zamieszkania” ([[osoba]] 9a)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Nagłówek** „Miejsca zamieszkania” (16 sp, półgruby) z ikoną `home_outlined` w akcencie — jak inne sekcje (R4) | tekst | — | — | — | R4 · D1 |
| 2 | **Wiersz zamieszkania** — jak wiersze „Daty” ([[osoba]] 8): linia podziału w kolorze obrysu, ≥ 48 dp; **lata** (lewa kolumna 112 dp, 14 sp, tekst pomocniczy; przy większym tekście nad wartością, jak v2.2 w [[osoba]]) · **miejsce** (16 sp, tekst): **adres** („ul. Przykładowa 3, Wymyślowo”, druga linia: kraj) · **miejscowość** („Wymyślowo, Polska”) · **kraj** („Ukraina”, druga linia „cały kraj — miejscowość nieznana”, 14 sp, tekst pomocniczy). Przy N2 z nazwą z tamtego czasu: ta nazwa w pierwszej linii, w drugiej „dziś: Zmyślin, Ukraina”; **adres + N2** — „ul. Przykładowa 3, Zmyślin, Polska” / „dziś: Zmyślin, Ukraina”; **kraj + N2** — „Zmyślin, Polska” / „dziś: Ukraina — cały kraj” (v1.1, D10). **Puste „Do” przed późniejszym miejscem** (v1.2, D12): lata kończą się początkiem następnego zamieszkania — „od 2024” i „od 2026” to wiersze „2024–2026” i „od 2026”; wpisane „Do” zawsze wygrywa. Lata według [[style-b]] reguła 6 i D3: `1946–1978`, `ok. 1925 – 1945`, `od 1946`, `do ok. 1925`; bez lat — kolumna pusta. **Łamanie linii** (v1.1, [[style-b]] reguła 6, v1.32): lata łamią się tylko za „–” — „ok.”, „od”, „do” trzymają się roku, a „–” poprzedniej części; „dziś:” trzyma się nazwy. Opis dla czytnika: „ok. 1925 – 1945: Zmyślin, Polska, dziś Zmyślin, Ukraina”. **Bez akcji** (wejście na mapę — [[ISSUE-045-migration-map]]) | lista wierszy | — | — | — | ISSUE-042 · D2, D3 |
| 3 | **Kolejność:** według początku („Od”), a bez „Od” — według końca; bez lat na końcu, w kolejności wpisania | — | — | — | — | D4 |
| 4 | **Bez miejsc:** „Nie ma jeszcze zapisanych miejsc.” (16 sp, tekst pomocniczy) i przycisk z obrysem **„Dodaj miejsce”** (`add_home_outlined` w akcencie, ≥ 48 dp, szerokość treści) | pusty stan + przycisk | → [[wpis-osoby]] „poprawa” z otwartym oknem (A) | — | — | [[style-b]] reguła 9 · D20 w [[osoba]] |
| 4a | **„Pokaż na mapie”** (v1.3) — pod ostatnim wierszem, do lewej: przycisk tekstowy w akcencie z ikoną `public_outlined` (v1.4), cel 48 dp, jak „Pokaż w drzewie” w [[osoba]] 6. Tylko przy co najmniej jednym zamieszkaniu; bez miejsc go nie ma (4) | przycisk tekstowy | → [[mapa-migracji]] z tą osobą w środku | — | — | [[ISSUE-045-migration-map]] · [[osoba]] D22 |

### Formularz — sekcja „Miejsca zamieszkania” ([[wpis-osoby]] 9b)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 5 | **Nagłówek** jak 1. Sekcja po „Kim była” (8) i po „Rodzinie” (9a), gdy ta jest; **poza `next`** | tekst | — | — | — | D5 |
| 6 | **Karta zamieszkania** (powierzchnia, promień 12 dp, ≥ 72 dp, jak karta partnera [[wpis-osoby]] 9a c): lata (16 sp, półgruby; bez lat — „Bez lat”; puste „Do” przed późniejszym miejscem — koniec z następnej karty, jak w 2, D12) · miejsce (14 sp, tekst pomocniczy, jedna albo dwie linie: „Zmyślin, Polska · dziś Ukraina”) · ✎ (48 dp, `tooltip` „Popraw miejsce”). Kolejność jak 3. **Linia miejsca** (v1.1, D10): miejscowość — „Wymyślowo, Polska”; adres — „ul. Przykładowa 3, Wymyślowo, Polska”; kraj — „Ukraina · cały kraj”; z nazwą z tamtego czasu — „{nazwa z tamtego czasu} · dziś {miejscowość}, {kraj}”, a **sam kraj („· dziś Ukraina”), gdy część nazwy z tamtego czasu przed pierwszym przecinkiem to dzisiejsza nazwa miejscowości** (porównanie całej części, bez polskich znaków i wielkości liter — nie początek: „Zmyślinek, Polska” przy dzisiejszym „Zmyślin” zostaje „· dziś Zmyślin, Ukraina”); adres + N2 — „{adres}, {nazwa z tamtego czasu} · dziś …” jak wyżej; kraj + N2 — „{nazwa z tamtego czasu} · dziś {kraj}”. Linia łamie się przed „·”, nigdy po nim, a „dziś” trzyma się nazwy ([[style-b]] reguła 6, v1.32) | karta | ✎ → okno (A) z danymi | — | — | D5 |
| 7 | **„Dodaj miejsce”** — przycisk z obrysem, `add_home_outlined` | przycisk | → okno (A) puste | — | — | D5 |

### Okno (A) „Miejsce zamieszkania”
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 8 | **Pasek:** ✕ (`tooltip` „Zamknij”, v1.1) · „Miejsce zamieszkania” | pasek | ✕ → *Navigation* | — | — | decyzja projektowa |
| 9 | **Od** — blok daty jak [[wpis-osoby]] (b, c, e), ale **dopisek tylko: dokładnie · około** (D3). **Fokus i klawiatura numeryczna od razu** przy pustym oknie | dopisek + pole daty | `next` → Do | „dokładnie”, pusto | jak blok daty: `rrrr` · `mm.rrrr` · `dd.mm.rrrr` | D3 · [[FR-004-data-z-dopiskiem]] |
| 10 | **Do** — jak 9; pod etykietą linia 13 sp, tekst pomocniczy: **„Puste — do początku następnego miejsca.”** (v1.2, D12) | dopisek + pole daty | `next` → Miejsce (otwiera B) | „dokładnie”, pusto | gdy oba: „Do” nie wcześniej niż „Od”: „Koniec nie może być przed początkiem.” | D3 |
| 11 | **Podgląd lat** pod „Do” (14 sp, tekst pomocniczy): „→ ok. 1925 – 1945”, „→ od 1946”, „→ bez lat” | tekst | — | — | — | jak blok daty |
| 12 | **Miejsce** — pole-przycisk (≥ 56 dp, obrys): `place_outlined` · wybrane miejsce („Zmyślin · Ukraina”, „Ukraina · cały kraj”; łamie się przed „·” — v1.1) albo podpowiedź „Wybierz kraj albo miejscowość” · chevron | pole-przycisk | → wybór (B) | pusto | **wymagane**: „Wybierz miejsce.” (bez miejsca nie ma czego zapisać) | ISSUE-042 AC-1, AC-2 |
| 13 | **Nazwa z tamtego czasu** — **N2, wybór autora na stopie #1** (*Open* 2): pole tekstowe, opcjonalne; podpowiedź „np. Zmyślin, Polska” | pole tekstowe, wielka litera na początku słów | `next` | pusto | — | N2 · FamilySearch |
| 14 | **Adres** — **A1, wybór autora na stopie #1** (*Open* 1): pole tekstowe, opcjonalne, **tylko gdy miejsce to miejscowość**; podpowiedź „np. ul. Przykładowa 3”. ~~*A2:* pod polem przycisk tekstowy „Popraw punkt na mapie” (gdy jest sieć)~~ — A2 nie wybrane | pole tekstowe | `done` | pusto | — | autor („wręcz dokładną ulicę”) · A1–A3 |
| 15 | **„Gotowe”** — przycisk wypełniony, przypięty na dole nad klawiaturą | przycisk | → formularz (*Navigation*) | — | błąd → komunikat przy polu, fokus na pierwszym | [[style-b]] reguła 1 |
| 16 | **„Usuń to miejsce”** — tylko z karty; przycisk tekstowy (kolor tekstu, nie akcent), nad „Gotowe” | przycisk tekstowy | → okno potwierdzenia | — | — | *Navigation* |

### Wybór miejsca (B)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 17 | **Pasek z polem wyszukiwania** (wstecz · pole z `search`, podpowiedź „Kraj albo miejscowość” — v1.1), fokus i klawiatura od razu | pole tekstowe | wpisywanie filtruje na bieżąco | pusto | — | decyzja projektowa |
| 18 | **Bez tekstu: „Ostatnio wybrane”** (nagłówek, 14 sp, tekst pomocniczy) — do 5 różnych miejsc: **najpierw z kart tego formularza (jeszcze niezapisanych), potem z zapisanych zamieszkań**, najnowsze najpierw (v1.1, D11); ikona `history` · nazwa · druga linia jak w 19 (jednostka · kraj) albo „cały kraj” | lista | dotknięcie → (A) | — | — | D6 (tempo) · D11 |
| 19 | **Wyniki — miejscowości:** ikona `location_city_outlined` · polska nazwa, jeśli lista ją ma (inaczej miejscowa) · druga linia: jednostka i kraj („woj. testowe · Polska”, „obw. przykładowy · Ukraina”) — rozróżnia tak samo nazwane wsie; łamie się przed „·” (v1.1). **Jednostka** (v1.1): polska nazwa z GeoNames ze skrótem „woj.”, „obw.”; w czterech krajach z pełną listą brakujące polskie nazwy uzupełnia narzędzie listy; poza nimi nazwa z listy (często angielska albo miejscowa). Dopasowanie od początku słów, bez polskich znaków i wielkości liter, jak wyszukiwanie cmentarzy ([[cmentarze]]), **także po innych nazwach miejscowości** (polskie nazwy historyczne i polskie zapisy w czterech krajach) — wiersz pokazuje nazwę z listy (v1.1, D9). **Kolejność** (v1.1, D9): dopasowanie od początku nazwy przed dopasowaniem dalszego słowa, potem liczba mieszkańców z wagą (Polska ×10; Ukraina, Białoruś, Litwa ×3), stolice i siedziby jednostek, alfabet; najwyżej 30 wierszy; wiersz ≥ 56 dp | lista | dotknięcie → (A) | — | — | GeoNames · D7 · D9 |
| 20 | **Wyniki — kraje:** `public` · nazwa kraju · „cały kraj”. **Od 3 liter kraj, którego nazwa zaczyna się od wpisanego tekstu, stoi na górze wyników, przed miejscowościami** — ten sam wiersz, bez nagłówka (rodzaj niosą ikona i „cały kraj”). Pozostałe pasujące kraje — dalszym słowem nazwy („Korea Południowa” na „połu”), a przy 1–2 literach wszystkie — **pod miejscowościami**, nagłówek „Kraje” (v1.1, D8; w v1 wszystkie kraje pod miejscowościami) | lista | dotknięcie → (A), poziom „kraj” | — | — | ISSUE-042 AC-1 · D8 |
| 22 | **Podpis źródła listy** na dole wyboru, pod wynikami: „Lista miejsc: GeoNames (CC BY 4.0) · Natural Earth” (13 sp, tekst pomocniczy) — licencja GeoNames wymaga podania źródła | tekst | — | — | — | CC BY 4.0 · jak „© OpenStreetMap” na mapie ([[style-b]] progi, wyjątek podpisu źródła) |
| 21 | **Brak wyników:** „Nie ma na liście? Wybierz kraj i wpisz nazwę w „Nazwa z tamtego czasu”.” (14 sp, tekst pomocniczy) — przy N1: „…wybierz kraj.” | tekst | — | — | — | D7 |

**Dane, których ekran potrzebuje** (dla `planning` — model danych i ADR należą do planu):
- zamieszkanie: osoba · **od** (data + dopisek dokładnie/około, pusta dozwolona) · **do** (jak od) · **miejsce** (poziom: kraj · miejscowość · adres;
  punkt; nazwa dziś; kraj dziś; jednostka) · **nazwa z tamtego czasu** (N2) · **adres** (tekst; A2 — też własny punkt);
- lista miejsc w aplikacji: kraje (nazwa polska, punkt etykiety) i miejscowości (nazwa polska albo miejscowa, jednostka, kraj, punkt) — zakres
  (Polska i sąsiedzi wszystkie miejscowości, świat — większe miasta?) i rozmiar mierzy `planning`;
- „ostatnio wybrane” — z zapisanych zamieszkań (bez nowej tabeli).

## States
| Stan | Co widać |
|---|---|
| widok — z miejscami | 1, 2 w kolejności 3 |
| widok — bez miejsc | 1 + 4 („Nie ma jeszcze zapisanych miejsc.” · „Dodaj miejsce”) |
| widok — samo zamieszkanie bez lat | wiersz z pustą lewą kolumną, na końcu listy |
| formularz — bez miejsc | 5 + 7 |
| formularz — z miejscami | 5, karty 6, 7 |
| okno — nowe | 9 z fokusem, reszta pusta; bez 16 |
| okno — z karty | wartości wpisane, 16 nad „Gotowe” |
| okno — błąd | „Wybierz miejsce.” przy 12 · „Koniec nie może być przed początkiem.” przy 10; kolor błędu z `error_outline` (SC 1.4.1) |
| okno — miejsce „kraj” | 14 (adres) schowane — adres wymaga miejscowości |
| wybór — pusty tekst | 18 („Ostatnio wybrane”), bez ostatnich — sama podpowiedź pola |
| wybór — wyniki | od 3 liter kraje pasujące od początku nazwy (20), potem 19, potem „Kraje” (20) — v1.1, D8; przy 1–2 literach 19, potem „Kraje” |
| wybór — brak wyników | 21 |
| wybór — lista się otwiera *(v1.1, zbudowane przez `dev`)* | wpisany tekst, zanim lista się otworzy: wskaźnik działania w toku (akcent, [[style-b]] v1.8) pod polem; bez tekstu — 18 |
| wybór — lista się nie otworzyła *(v1.1, zbudowane przez `dev`)* | „Nie udało się otworzyć listy miejsc.” (14 sp, tekst pomocniczy) i podpis źródła (22) |
| tekst 200% / 360 dp | lata w widoku nad miejscem (jak [[osoba]] v2.2); karty rosną; pola okna jedno pod drugim (dopisek nad datą, gdy obok się nie mieści) |

## Sketch
```
WIDOK OSOBY                         OKNO (A)
│ 🗓 Daty                       │    │ ✕  Miejsce zamieszkania        │
│ Urodzenie     ok. 1905        │    │ Od                             │
│ Zgon          14.03.1978      │    │ [około ▾] [1925            ]   │
│                               │    │ Do                             │
│ 🏠 Miejsca zamieszkania        │    │ [dokładnie ▾] [1945        ]   │
│ do ok. 1925   Ukraina         │    │ → ok. 1925 – 1945              │
│               cały kraj — …   │    │ Miejsce                        │
│ ok. 1925 –    Zmyślin, Polska │    │ [📍 Zmyślin · Ukraina       › ] │
│ 1945          dziś: Zmyślin,  │    │ Nazwa z tamtego czasu (N2)     │
│               Ukraina         │    │ [Zmyślin, Polska           ]   │
│ 1946–1978     ul. Przykładowa │    │ Adres (A1)                     │
│               3, Wymyślowo    │    │ [np. ul. Przykładowa 3     ]   │
│                               │    │ [         Gotowe           ]   │
│ 🖼 Zdjęcia · 2                 │
```

## Tempo
**Typowe zamieszkanie z notatek:** lata z „ok.” na początku, miejscowość z listy, bez adresu.

| Krok | Akcje poza pisaniem |
|---|---|
| „Dodaj miejsce” w formularzu | 1 |
| Od: dopisek „około” (menu, wybór) | 2 |
| Od: rok → `next` | 1 |
| Do: rok → `next` (otwiera wybór) | 1 |
| Wybór: kilka liter → dotknięcie wyniku | 1 |
| Gotowe | 1 |
| **Razem** | **7** (bez „około”: 5); miejscowość z „ostatnio wybranych”: −0 pisania |

- Zapis z resztą formularza („Zapisz”) — bez osobnego zapisu (D5).
- Na ok. 100 osób po 1–2 zamieszkania: rząd 700–1400 akcji — **sekcja jest opcjonalna**, a wiedza przychodzi głównie od babci, nie z notatek.
- **Co skraca:** fokus od razu w „Od”, `next` z „Do” otwiera wybór, „ostatnio wybrane”. **Co wydłuża świadomie:** dopisek przy każdej dacie
  (+2) — bez niego „ok.” nie da się zapisać.

## Style B rules applied
- **Reguła 15:** widok tylko pokazuje; poprawa przez ✎; „Dodaj miejsce” w pustym stanie otwiera formularz od razu (działanie „Dodaj …”).
- **Reguła 9:** pusty stan mówi, co tu będzie, i ma jedno działanie.
- **Reguła 1:** jedyny wypełniony przycisk w oknie — „Gotowe”; w formularzu — „Zapisz”. „Dodaj miejsce” z obrysem. „Usuń to miejsce” w kolorze
  tekstu, nie akcentu.
- **Reguła 3:** ikony `outlined`, nagłówek sekcji w akcencie (`home_outlined`).
- **Reguły 6–7:** lata w polskim formacie; „cały kraj — miejscowość nieznana” spokojnie, jako fakt.
- **Reguła 11:** karty w formularzu jak karta partnera; wiersze widoku bez chevronu (bez akcji).
- **Progi:** treść 16 sp, drobny tekst ≥ 13 sp; pola i wiersze ≥ 48 dp; błąd kolorem **i** ikoną z tekstem (SC 1.4.1).
- **Tokeny:** bez nowych — tło, powierzchnia, tekst, tekst pomocniczy, akcent, obrys, błąd z `theme.dart`.

## AC → element
| AC ([[ISSUE-042-places-of-residence]]) | Element(y) | Jak widać spełnienie |
|---|---|---|
| AC-1 — sam kraj i „ok. 1930 – ok. 1945” → poziom „kraj”, punkt w środku kraju | 9–12, 20, 2 | w oknie „około 1930”, „około 1945”, wybór „Ukraina · cały kraj” (po 3 literach na górze wyników — D8) → w widoku „ok. 1930 – ok. 1945 · Ukraina · cały kraj — miejscowość nieznana” |
| AC-2 — doprecyzowanie miasta, potem adresu → jedno zamieszkanie | 6 → ✎ → 12, 19, 14 | ✎ na karcie → Miejsce → „Zmyślin” → Adres „ul. Przykładowa 3” → Gotowe → jedna karta, widok z adresem |
| AC-3 — kraj i miasto bez sieci | 17–20 | wybór działa w trybie samolotowym (lista w aplikacji) |
| AC-4 — kopia sprzed pozycji odtwarza się w nowej | n/a — warstwa danych | test migracji i próbne odtworzenie (plan) |

## Decisions
- **D1 — sekcja w widoku po „Datach”, przed „Zdjęciami”**: fakty z życia razem (urodzenie, zgon, pochówek, gdzie mieszkał), zdjęcia na końcu jak
  dziś. Nazwa sekcji „Miejsca zamieszkania” — rzeczownik jak „Rodzina”, „Daty”, bez odmiany według płci. *Obali:* autor szuka miejsc przy rodzinie.
- **D2 — dokładność mówi sam wiersz** (kraj / miejscowość / adres), bez etykiety „dokładność”. *Obali:* autor myli „kraj” z miejscowością o tej
  samej nazwie.
- **D3 — okres „Od – Do” z dopiskiem tylko „dokładnie · około”** (GEDCOM 7: okres to `FROM … TO …`; „między” to nieznana data, nie okres). Puste
  „Od” albo „Do” albo oba — dozwolone. „Do dziś” nie ma osobnego znaku: puste „Do” u żyjącej osoby. *Obali:* autor chce „przed”/„po” albo „do dziś”.
- **D4 — kolejność według lat**, bez lat na końcu. *Obali:* autor chce kolejności ręcznej.
- **D5 — sekcja w formularzu w każdym trybie, zapis z „Zapisz”** (całość wpisu, [[wpis-osoby]] „Zapis jest całością”) — inaczej niż „Rodzina”, która
  potrzebuje zapisanej osoby. Przy przepisywaniu nowej osoby nie trzeba jej najpierw zapisać. *Obali:* zmiana w oknie ginie przy „Odrzuć wpis”, a
  autor oczekiwał, że zapisała się od razu.
- **D6 — „ostatnio wybrane”** zamiast pustej listy: rodzina zwykle mieszkała w kilku tych samych miejscowościach. *Obali:* lista ostatnich myli.
- **D7 — lista miejsc w aplikacji (bez sieci)** dla kraju i miejscowości; polskie nazwy, gdy lista je zna; jednostka i kraj w drugiej linii. Brak
  na liście → kraj + nazwa wpisana ręcznie (N2). *Obali:* zbyt wiele miejscowości z notatek nie ma na liście — wtedy pomiar zakresu w `planning`.
- **D8 — kraj pasujący od początku nazwy stoi nad miejscowościami, od 3 liter** (v1.1, przegląd `ui`; znalezisko `dev` w *Dev report* →
  *Found, outside the item*). W v1 kraje stały pod miejscowościami, a wyników jest do 30: pomiar na liście z 2026-10-16 — „ukr” pasuje do 77
  miejscowości, „pols” do 73, a **pełna nazwa „Polska” do 23**, więc kraj (droga AC-1, „sam kraj”) stał pod kilkunastoma wierszami, poza widokiem nad
  klawiaturą (zrzut: ok. 8 wierszy). Kraj to rzadki wybór na liście ok. 240 krajów i 188 tys. miejscowości, ale jedyna droga do „sam kraj”.
  **Dlaczego od 3 liter:** krajów o tym samym początku nazwy jest do 28 przy 1 literze („S”), do 12 przy 2 („Ma”), przy 3 — 1–3 dla czterech krajów z pełną listą
  (Polska, Ukraina, Białoruś, Litwa) i np. Niemiec czy Rosji, a najwyżej 10 dla „wys” („Wyspy …”); przy 1–2 literach kraje zepchnęłyby miejscowości z ekranu.
  Kraje pasujące dalszym słowem nazwy zostają w grupie „Kraje” pod miejscowościami (przy „pol” byłoby ich 7 nad miejscowościami). *Obali:* autor
  szuka miejscowości o początku nazwy kraju („Pol…”) i kraj na górze go myli — wtedy kraj na górze tylko przy pełnej nazwie kraju.
- **D9 — kolejność wyników i szukanie po innych nazwach** (v1.1, D-dev 1 i 2 przyjęte w przeglądzie `ui`). Specyfikacja nie mówiła o kolejności, a bez
  wagi kraju 3 litery dawały najpierw duże miasto dalekiego kraju, a potem polskie miasto o tym samym początku. Waga (Polska ×10; Ukraina, Białoruś,
  Litwa ×3) idzie za zakresem listy — cztery kraje w całości, granice sprzed 1945 ([[ISSUE-042-places-of-residence]] → *Implementation plan*). Inne nazwy (polskie nazwy historyczne,
  polskie zapisy w czterech krajach) służą tylko do szukania — kto szuka nazwy sprzed 1945, trafia na dzisiejszą miejscowość i starą nazwę wpisuje w
  „Nazwa z tamtego czasu” (N2). *Obali:* autor na stopie #2 nie rozpoznaje wyniku znalezionego po starej nazwie — wtedy ta nazwa w drugiej linii wiersza.
- **D10 — wiersze i karty dla N2 z adresem i z krajem** (v1.1, D-dev 4 przyjęte): połączenia, których v1 nie pokazywała, idą tym samym wzorem — pierwsza
  linia to to, co mówią notatki (nazwa z tamtego czasu, z adresem przed nią), druga „dziś: …” z dzisiejszej listy. Karta skraca „dziś …” do kraju, gdy
  nazwa się nie zmieniła (makieta: „Zmyślin, Polska · dziś Ukraina”) — porównanie całej części przed pierwszym przecinkiem, bo sam początek ukryłby
  zmienioną nazwę („Zmyślinek” przy „Zmyślin”). *Obali:* autor czyta „dziś: …” jako drugie zamieszkanie.
- **D11 — „Ostatnio wybrane” najpierw z kart formularza** (v1.1, D-dev 5 przyjęte): przy przepisywaniu kilku zamieszkań jednej osoby drugie ma pierwsze
  miejsce pod ręką, zanim cokolwiek się zapisze (D6 — tempo). *Obali:* autor szuka na górze miejsc z wcześniej zapisanych osób, a widzi tylko te z
  bieżącego wpisu (karty żyją tylko w otwartym formularzu, więc odrzucony wpis nie zostawia śladu w liście).
- **D12 — pobyt bez „Do” kończy się początkiem następnego** (v1.2, decyzja autora na stopie #2): autor zapisał „od 2024” i „od 2026” i chce, żeby
  aplikacja wiedziała, że to przeprowadzka, nie dwa domy naraz. **Wyliczone przy odczycie, nie zapisane** — w bazie zostaje to, co podało źródło
  (dowód oddzielony od wniosku); zapisany koniec byłby faktem, którego nikt nie podał, i zestarzałby się po dołożeniu pobytu pomiędzy. Reguła: zamieszkanie
  z „Od” i bez „Do” kończy się „Od” najbliższego zamieszkania o późniejszym początku (z jego dopiskiem i dokładnością); wpisane „Do” zawsze wygrywa; ten
  sam początek albo brak „Od” — bez wyliczenia. Widok (2) i karta (6) pokazują lata z tym końcem tym samym zapisem co wpisane; okno zostawia „Do”
  puste i mówi pod etykietą, co puste znaczy (10). Mapa migracji ([[ISSUE-045-migration-map]]) bierze ten sam koniec. **Koszt:** dwa domy naraz (np.
  studia w innym mieście) wymagają wpisanego „Do” przy jednym z nich. *Obali:* autor myli koniec wyliczony z wpisanym — wtedy wyliczony innym zapisem
  (np. „2024 – (2026)”).

## Open
> **v1.1 — rozstrzygnięte:** A1 i N2 (stop #1 2026-10-16, potwierdzone przez autora: *„Tak”* — [[ISSUE-042-places-of-residence]] → *Dev report*).
> Punkt 3 zostaje otwarty.

1. **~~⚠️ OPEN~~ A — adres → A1** (makieta, kandydaci A1–A3; decyzja autora na stopie #1):
   - **A1 (rekomendacja)** — adres jako tekst, punkt w środku miejscowości; bez sieci, bez nowej zależności; nie da kropki na domu;
   - **A2** — A1 + „Popraw punkt na mapie” przy sieci (mapa ulic, pinezka na dom); nowy ekran mapy;
   - **A3** — wyszukiwarka adresów w sieci; **wpisany adres wychodzi z telefonu** (dziś aplikacja nie wysyła żadnego wpisanego tekstu,
     [[NFR-005-dane-nie-opuszczaja-telefonu]]); stare adresy często się nie znajdą.
2. **~~⚠️ OPEN~~ N — nazwa sprzed zmiany granic → N2** (makieta; decyzja autora na stopie #1):
   - **N1** — tylko dzisiejsza nazwa i kraj z listy;
   - **N2 (rekomendacja, tak robi FamilySearch)** — miejsce z listy daje punkt, a opcjonalne pole „Nazwa z tamtego czasu” daje pierwszą linię
     wiersza („Zmyślin, Polska” · „dziś: Zmyślin, Ukraina”).
3. **Miejsce urodzenia i zgonu — nie w tej pozycji.** `events.place` jest w schemacie, a żaden ekran go nie zapisuje (audyt R9 w
   [[ISSUE-032-mvp-install]]). Ten sam wybór miejsca dałby mapie migracji punkt początku i końca — kandydat po [[ISSUE-045-migration-map]], decyzja
   autora przy jej projekcie. **v1.3:** przy projekcie mapy — **nie w ISSUE-045**, bo punkt wymaga zmiany bazy (`events.place` to sam tekst); kandydat po
   wyjeździe, widoczny na stopie #1 ([[mapa-migracji]] D12).
