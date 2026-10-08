---
screen: "Rodzina — arkusz rodziny (A) i wybór osoby (B)"
items: ["[[ISSUE-019-family-relations]]"]
us: "[[US-003-przepisanie-rodziny]]"
journey-step: "n/a — M1 (warunek kroku 1 UJ-001)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-rodzina.html (ramki 3–6; ramki 1–2 to sekcja „Rodzina” w [[wpis-osoby]])"
updated: 2026-10-07
---

# Rodzina — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]].
>
> **Wersja 1 (2026-10-07, przed planem [[ISSUE-019-family-relations]]).** Kanon: brief → *Domain canon (Step 0)* —
> jednostką wpisywania jest *family group sheet* (para i jej dzieci), co jest też odpowiedzią na G6, i
> [[FR-002-rodzina-jako-rekord]] („całymi rodzinami, nie osoba po osobie”). Referencja: R4 prawy pokazuje
> rodzinę **przy osobie** (sekcja „Rodzina” z chipami, [[references]]). Arkusza nie ma w R1–R4, więc dziedziczy
> reguły stylu B i formę pól z [[wpis-osoby]]. Gdzie relacje widać przy osobie: [[wpis-osoby]] v5, element 9a.
> **Trzy rozwidlenia dla autora na stopie #1** są w *Open*. Specyfikacja jest napisana według rekomendacji.
>
> **Wersja 1.1 (2026-10-07, stop #1 [[ISSUE-019-family-relations]] — decyzje autora):**
> - **O1 „ok”** (arkusz do wpisywania, widok przy osobie). Uwaga autora: *„może być tak, że ktoś był z kimś w danym
>   okresie, a następnie się rozstali lub owdowieli i mieli nowe związki i dzieci”*. Model to obsługuje: każdy związek to
>   osobna rodzina z własnymi dziećmi, datą ślubu i datą końca (AC-2, AC-3). Zmieniają się słowa: **„związek”** zamiast
>   „małżeństwo” (nie każdy związek był małżeństwem). Linia przy końcu mówi o rozstaniu i owdowieniu (A6);
> - **O2 i płeć w schemacie — „nie czuję potrzeby”:** **bez płci.** Nazwy relacji są neutralne (*Role names*), a z
>   arkusza znika kolumna roli, bo sekcje „Para” i „Dzieci” mówią to samo;
> - **O3 — „na ten moment raczej nie trzeba”:** bez rodzeństwa przy osobie; pokażą je wizualizacje połączeń (EPIC-003);
> - **kolejność dzieci według daty urodzenia** (kanon GEDCOM 7: *„chronological by birth”*) zastępuje D10;
> - D1–D8 i D11 przyjęte („ok”), w tym „Usuń rodzinę” (D8).
>
> **Wersja 1.2 (2026-10-07, przegląd `ui` zbudowanego ekranu, ISSUE-019 → *Verification*):** błąd daty przewija cały
> blok z linią komunikatu nad „Zapisz” (*States* → „A — błąd”; blok wspólny z [[wpis-osoby]]); 24 dp przed „Dzieci”;
> „Dodaj koniec związku” i „Usuń rodzinę” na krawędzi treści (16 dp); „Nowa osoba” ma rolę przycisku dla czytnika; D7 ze
> słowami v1.1.
>
> **Wersja 1.3 — płeć wraca ([[SPIKE-004-mvp-flow-prototype]] D16, 2026-10-08):** warunek obalenia D9' się spełnił —
> ścieżka do „ja” w widoku osoby ([[osoba]] D4) potrzebuje nazw z płcią. Autor: *„W sumie faktycznie musi wrócić płeć -
> bo dzięki temu możemy powiedzieć babcia, dziadek, stryj, siostra cioteczna itd.”*. Chipy i wiersze dostają nazwy z
> płci: Ojciec/Matka, Mąż/Żona (bez ślubu: Partner/Partnerka), Syn/Córka; osoba bez wpisanej płci — nazwy neutralne
> jak w v1.1. Kolumna roli w arkuszu dalej niepotrzebna (sekcje „Para” i „Dzieci”). Szczegóły → pozycja, która zbuduje
> pole płci ([[wpis-osoby]] 4a).
>
> **Wersja 1.4 — dwa tryby związku ([[SPIKE-004-mvp-flow-prototype]] D20, 2026-10-08):** związek ma **dwie daty: „Razem od”
> (początek związku) i „Ślub”**, a do tego jak dotąd koniec związku. Autor: *„zrobiłbym dwa tryby połączenia (razem,
> małżeństwo - bo czasami ludzie nie są małżeństwem, mają dziecko, i dopiero biorą ślub)”*. Rozstrzyga to temat z
> `CURRENT_STATE.md` („data początku związku bez ślubu”, przegląd US-003 uwaga 4) wariantem **osobnego pola „Razem
> od”**, nie innego podpisu „Ślubu”. Związek bez ślubu ma samo „Razem od”; nazwy w chipach: Partner/Partnerka (bez ślubu)
> albo Mąż/Żona (po ślubie). W drzewie: linia przerywana od „Razem od”, ciągła od ślubu ([[drzewo]] D4). Zdarzenie
> początku związku to nowe zdarzenie rodziny z twierdzeniem (jak ślub, [[ADR-011-relation-claims-family-and-child-link]]) —
> szczegóły i ewentualna migracja → pozycja, która zbuduje pole.

## Purpose
Wpisanie jednej rodziny naraz — pary i jej dzieci — tak, jak stoi w notatkach, oraz poprawa rodziny. Wybór osoby
**najpierw szuka**, więc osoba już wpisana (np. przy grobie) nie powstaje drugi raz (US-003 AC-5).

## Navigation
- Z [[wpis-osoby]] w trybie „poprawa”, sekcja „Rodzina” (element 9a):
  - „Dodaj związek” (v1.1; było „Dodaj małżeństwo”) → A **„nowa rodzina”**, w parze ta osoba;
  - „Dodaj rodziców” → A **„nowa rodzina”**, w dzieciach ta osoba;
  - ✎ przy grupie (rodzice albo związek) → A **„poprawa”** tej rodziny.
- A → „Dodaj osobę do pary” albo „Dodaj dziecko” → B. **Dotknięcie osoby w B wraca do A** z tą osobą dodaną, a
  „Nowa osoba” wraca z nowym wierszem do wpisania. Wstecz z B → A bez zmian.
- **„Zapisz” w A → [[wpis-osoby]]**, który odświeża sekcję „Rodzina”. Rodzina zapisuje się od razu, własną
  transakcją, niezależnie od „Zapisz” formularza osoby (D1).
- Wstecz z A ze zmianami → okno „Odrzucić zmiany w rodzinie?”. Bez zmian → od razu.
- Osoba z arkusza ma swój wpis ([[wpis-osoby]], poprawa) dostępny przez chip w sekcji „Rodzina” każdego krewnego,
  także wtedy, gdy nie ma grobu. Wiersze arkusza nie prowadzą do wpisu (D11).

## Elements in order

### A — arkusz rodziny (pełny ekran)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| A1 | **Pasek:** wstecz; tytuł „Nowa rodzina”, w poprawie „Rodzina” (półgruby); podtytuł (14 sp, tekst pomocniczy, jedna linia, ucięty): imiona i nazwisko osoby, z której otwarto arkusz | pasek | wstecz → okno albo [[wpis-osoby]] | — | — | decyzja projektowa |
| A2 | Nagłówek **„Para”** (14 sp, półgruby, tekst pomocniczy — jak D4 w [[zdjecie]]) | tekst | — | — | — | AC-1 · FR-002 |
| A3 | **Wiersz osoby** (ten sam kształt w parze i w dzieciach), ≥ 56 dp. Imiona i nazwisko z „z d.” (16 sp, tekst, zawijane), pod nimi lata (14 sp, tekst pomocniczy, format jak w [[grob]]), a przy osobie, z której otwarto arkusz, „· ta osoba”. Z prawej `close` (tekst pomocniczy, cel 48 dp, `tooltip` „Usuń z rodziny”) — **oprócz „tej osoby”**. **Bez kolumny roli** (v1.1: bez płci rola powtarzałaby nagłówek sekcji) | wiersz | `close` usuwa osobę **z rodziny**, nie z aplikacji | — | — | AC-1 · AC-2 |
| A3' | **Wiersz nowej osoby** (z „Nowa osoba” w B): pola **„Imiona”** i pod nim **„Nazwisko”** (ramka w kolorze obrysu, 16 sp, wielka litera na początku słów); `close` usuwa wiersz | dwa pola tekstowe | **fokus i klawiatura od razu w „Imiona”**, kursor na końcu; „Imiona” `next` → „Nazwisko” `done` | imiona: tekst wpisany w B; nazwisko: **podpowiedziane i zaznaczone** — dziecko i druga osoba z pary dostają nazwisko pierwszej osoby z pary, a przy „Dodaj rodziców” nazwisko dziecka. Przy parach -ski/-ska zaznaczenie wymaga przepisania nazwiska, jak w [[wpis-osoby]] (*Open* → „Do odczucia”) | imiona albo nazwisko: „Podaj imiona albo nazwisko.” | AC-1 · [[wpis-osoby]] element 3 (podpowiedź) · D4 |
| A4 | **„Dodaj osobę do pary”** — przycisk z obrysem, `person_add_alt_outlined` w akcencie, napis w kolorze tekstu, ≥ 52 dp, szerokość treści, z lewej. Tylko gdy w parze jest mniej niż dwie osoby | przycisk | → B w trybie „para” | — | najwyżej dwie osoby w parze: przy dwóch przycisku nie ma | AC-1 · FR-002 (1–2 partnerów) |
| A5 | **„Ślub”** — blok daty z [[wpis-osoby]] (b dopisek · c data · d „do” przy „między” · e podgląd), etykieta „Ślub” | blok daty | dotknięcie pola; `next` z daty do daty | „dokładnie”, pusto | jak blok daty | AC-3 · [[FR-004-data-z-dopiskiem]] |
| A6 | **„Dodaj koniec związku”** — przycisk tekstowy w linii treści (akcent). Odsłania **A6'**: blok daty „Koniec związku” z linią pod etykietą „np. rozwód albo rozstanie. Owdowienie to zgon osoby — zapisuje się w jej wpisie.” (13 sp, tekst pomocniczy; v1.1 — uwaga autora o rozstaniu i owdowieniu). W poprawie rodziny z datą końca A6' widać od razu, bez przycisku | przycisk → blok daty | po odsłonięciu fokus w polu daty | schowany | jak blok daty | AC-3 · D7 |
| A7 | Nagłówek **„Dzieci”** (jak A2) | tekst | — | — | — | AC-1 |
| A8 | **Wiersze dzieci** (A3 / A3'). Przy otwarciu arkusza **według daty urodzenia** (pierwsza wartość), a bez daty na końcu, w kolejności zapisu (v1.1, kanon GEDCOM 7). Wiersz dodany w trakcie edycji zostaje tam, gdzie go dodano | wiersze | jak A3 | — | — | AC-1 · AC-2 |
| A9 | **„Dodaj dziecko”** — jak A4, zawsze | przycisk | → B w trybie „dziecko” | — | — | AC-1 |
| A10 | **Źródło** — stały tekst pomocniczy nad przyciskiem: „Rodzina i jej daty zapiszą się ze źródłem: notatki.” | tekst | — | źródło „notatki”, status `CLAIMED` (statusu nie pokazujemy) | — | AC-4 · [[FR-001-provenance]] (jak [[wpis-osoby]] element 10) |
| A11 | **„Usuń rodzinę”** — tylko w poprawie: przycisk tekstowy z `delete_outline`, w kolorze tekstu ([[style-b]] reguła 14, usuwanie bez koloru błędu) | przycisk | → okno „Usunąć rodzinę?” | — | — | **decyzja projektowa spoza AC** (D8) |
| A12 | **Zapisz** — przycisk wypełniony, przypięty na dole nad klawiaturą, ≥ 52 dp | przycisk | dotknięcie | — | rodzina ma osobę w parze i co najmniej dwie osoby. Bez pary: „Dodaj osobę do pary — rodzina to para i jej dzieci.” Z jedną osobą: „Dodaj drugą osobę do pary albo dziecko.” Komunikat nad „Zapisz” z `error_outline` w kolorze błędu. Do tego błędy pól jak w [[wpis-osoby]] | AC-1…AC-4 |

**Zapis jest całością** (ISSUE-019 AC): nowe osoby, przynależność do pary i dzieci (każda z twierdzeniem), daty
ślubu i końca (z twierdzeniami) zapisują się razem albo wcale. Usunięcie osoby z rodziny usuwa jej przynależność
razem z twierdzeniem. Osoba zostaje.

#### Role names
Rola mówi, kim **osoba z chipu** ([[wpis-osoby]] 9a) jest dla osoby, której wpis oglądamy. **v1.1: bez płci** (decyzja
autora), więc nazwy są neutralne:

| Relacja | Nazwa |
|---|---|
| rodzic | Rodzic |
| druga osoba ze związku | Partner |
| dziecko | Dziecko |

„Partner”, a nie „Małżonek”, bo związek nie musiał być małżeństwem (uwaga autora do O1). Arkusz ról nie pokazuje:
mówią je nagłówki „Para” i „Dzieci”. ~~Tabela z v1 (Mąż/Żona, Syn/Córka, Ojciec/Matka, Brat/Siostra) zależała od płci
— *Open* 2, odrzucone.~~

### B — wybór osoby (pełny ekran)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| B1 | **Pasek:** wstecz → A bez zmian; tytuł „Dodaj do pary” albo „Dodaj dziecko” (półgruby) | pasek | — | — | — | decyzja projektowa |
| B2 | **Pole „Szukaj osoby albo wpisz nową”** — ramka w kolorze obrysu, ikona `search` (tekst pomocniczy); filtruje B4 i B5 bez polskich znaków i końcówek (`matchesQuery`, jak D3 w [[zdjecie]]) | pole tekstowe | **fokus i klawiatura od wejścia** (inaczej niż D3); `done` chowa klawiaturę | pusto | — | AC-5 · D3 |
| B3 | **„Nowa osoba”** — pierwszy wiersz pod polem, zawsze widoczny: `person_add_alt_outlined` (akcent) i „Nowa osoba” (16 sp, tekst), a przy wpisanym tekście „Nowa osoba: „Anna””. ≥ 56 dp | wiersz-przycisk | → A z wierszem A3', imiona = tekst z B2 | — | — | AC-1 · D3 |
| B4 | **Sekcja „W tym grobie”** (nagłówek jak A2) — osoby z grobu osoby, z której otwarto arkusz (jej pierwszy pochówek, [[ADR-006-claimed-value-separate-structures]] D3), w kolejności wpisania. Osoba bez grobu — sekcji nie ma. **Wiersz:** imiona i nazwisko z „z d.” (16 sp, tekst), lata (14 sp, tekst pomocniczy), ≥ 56 dp, cały wiersz to jeden cel | lista | dotknięcie → A z tą osobą | — | — | AC-5 |
| B5 | **Sekcja „Inne osoby”** — pozostałe osoby, alfabetycznie po nazwisku, potem imionach (`polishCompare`). Druga linia: lata · nazwa grobu, a bez niej nazwa cmentarza (jedna linia, ucięta), jak D5 w [[zdjecie]]; osoba bez grobu — same lata, a bez lat „bez dat” | lista | jak B4 | — | — | AC-5 · AC-2 (osoba z innej rodziny jako druga para) |

**Wiersze nieaktywne** (B4, B5): tekst w kolorze pomocniczym, bez dotknięcia, dla czytnika „niedostępne”, a zamiast
lat **powód tekstem** (nie samym kolorem, SC 1.4.1):
- „już w tej rodzinie” — osoba jest już w A (także „ta osoba”);
- „ma już rodziców” — tylko w trybie „dziecko”, gdy osoba jest dzieckiem w innej rodzinie (D5).

**Pusty wynik filtra:** pod B3 „Nie ma osoby pasującej do „…”.” (14 sp, tekst pomocniczy). B3 zostaje, więc z
pustego wyniku jest jedno działanie ([[style-b]] reguła 9).

**Dane, których potrzebuje B** (dla `planning`):
- wszystkie osoby: imiona, nazwisko, nazwisko rodowe, lata;
- grób albo cmentarz pierwszego pochówku każdej osoby;
- kto jest dzieckiem w jakiejś rodzinie (w trybie „dziecko”);
- niezapisany skład A — wyklucza osoby, które już w nim są.

## States
| Stan | Co widać |
|---|---|
| A — nowa, „Dodaj związek” | w parze „ta osoba” (bez `close`) i A4; A5 pusty; A6 schowany; „Dzieci” bez wierszy, tylko A9. Bez fokusu i bez klawiatury |
| A — nowa, „Dodaj rodziców” | „Para” bez wierszy, tylko A4; w „Dzieci” „ta osoba” i A9 |
| A — poprawa | wiersze z bazy; A5 i A6' z datami, gdy są; A11 widoczny |
| A — nowa osoba dopisana | wiersz A3' z fokusem w „Imiona”, klawiatura otwarta, nazwisko podpowiedziane |
| A — błąd | komunikaty pól jak w [[wpis-osoby]] (`error_outline`, kolor błędu, ramka); komunikat składu nad „Zapisz”; fokus i przewinięcie do pierwszego błędu; nic się nie zapisuje |
| A — zapisywanie | „Zapisz” nieaktywny przez chwilę zapisu |
| A — nieudany zapis | nad „Zapisz”: `error_outline` + „Nie udało się zapisać. Spróbuj jeszcze raz.” (kolor błędu); arkusz zostaje |
| A — okno „Odrzucić zmiany w rodzinie?” | „Zmiany w tej rodzinie nie zostaną zapisane.” · **„Wróć do rodziny”** (akcent) · „Odrzuć” (kolor tekstu) |
| A — okno „Usunąć rodzinę?” | „Osoby zostają w aplikacji. Znikną tylko ich powiązania w tej rodzinie i daty ślubu i końca.” · **„Zostaw”** (akcent) · „Usuń” (kolor tekstu). „Usuń” usuwa od razu i wraca do [[wpis-osoby]]; błąd usunięcia pod treścią okna: `error_outline` + „Nie udało się usunąć rodziny. Spróbuj jeszcze raz.” |
| B — otwarty | fokus w B2, klawiatura otwarta; B3, a pod nim B4 (gdy jest grób) i B5 |
| B — filtr | sekcje pokazują pasujące wiersze; nagłówek sekcji bez pasujących znika; B3 z wpisanym tekstem |
| B — pusty wynik | B3 i „Nie ma osoby pasującej do „…”.” |
| B — wczytywanie | samo tło (odczyt trwa ułamek sekundy — jak [[zdjecie]] D) |

## Sketch
A — nowa rodzina z „Dodaj związek” (po dodaniu partnera, dziecka z grobu i nowego dziecka) i B — wybór dziecka.
**v1.1:** szkic jest z v1 — w arkuszu nie ma już kolumny roli („Żona”, „Mąż”, „Syn”, „Córka”); wiersze zaczynają się
od imion. Reszta bez zmian:
```
 A — nowa rodzina                      B — dodaj dziecko
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│ ←  Nowa rodzina                  │  │ ←  Dodaj dziecko                 │
│    Maria Wymyślona z d. Testowa  │  │ ┌──────────────────────────────┐ │
│  Para                            │  │ │ ⌕  An▌                       │ │
│  Żona   Maria Wymyślona          │  │ └──────────────────────────────┘ │
│         z d. Testowa             │  │  👤+ Nowa osoba: „An”            │
│         1925–2004 · ta osoba     │  │                                  │
│  Mąż    Jan Wymyślony         ✕  │  │  W tym grobie                    │
│         1921–1987                │  │  Anna Wymyślona                  │
│  Ślub                            │  │  już w tej rodzinie   (przygaszone)
│ ┌──────────┐ ┌─────────────────┐ │  │                                  │
│ │ około  ▾ │ │ 1948            │ │  │  Inne osoby                      │
│ └──────────┘ └─────────────────┘ │  │  Anna Testowa                    │
│  → ok. 1948                      │  │  ok. 1930 · Cmentarz Wymyślony   │
│  Dodaj koniec związku            │  │  Joanna Testowa                  │
│  Dzieci                          │  │  ma już rodziców      (przygaszone)
│  Syn    Stanisław Wymyślony   ✕  │  │                                  │
│         1950–1951                │  │                                  │
│  Córka ┌ Imiona ─────────────┐ ✕ │  │        [ klawiatura ]            │
│        │ Anna▌               │   │  │                                  │
│        └─────────────────────┘   │  └──────────────────────────────────┘
│        ┌ Nazwisko ───────────┐   │
│        │ ▒Wymyślony▒         │   │  ← podpowiedź zaznaczona
│        └─────────────────────┘   │
│ ┌────────────────┐               │
│ │ 👤+ Dodaj dziecko│              │
│ └────────────────┘               │
│  Rodzina i jej daty zapiszą się  │
│  ze źródłem: notatki.            │
│ ┌──────────────────────────────┐ │
│ │            Zapisz            │ │
│ └──────────────────────────────┘ │
└──────────────────────────────────┘
```

## Tempo
**Typowa rodzina z notatek:** para (ta osoba i mąż z tego samego grobu), rok ślubu z „około”, troje dzieci —
jedno pochowane w tym grobie, dwoje nowych (bez grobu w aplikacji).

| Krok | Akcje poza pisaniem |
|---|---|
| [[grob]] → karta osoby → [[wpis-osoby]] (poprawa), przewinięcie do „Rodzina” | 2 |
| „Dodaj związek” | 1 |
| „Dodaj osobę do pary” → mąż w „W tym grobie” | 2 |
| „Ślub”: dopisek „około” (menu, wybór) → rok → `done` | 3 |
| dziecko z grobu: „Dodaj dziecko” → wiersz | 2 |
| nowe dziecko: „Dodaj dziecko” → imię w B2 → „Nowa osoba: …” → `next` → nazwisko podpowiedziane → `done` | 4 |
| drugie nowe dziecko | 4 |
| „Zapisz” → [[wpis-osoby]] → wstecz do [[grob]] | 2 |
| **Razem** | **20 akcji na rodzinę 5 osób** (ok. 4 na osobę), 0 pytań o źródło |

- Na całe notatki (ok. 100 osób, przy ok. 30 rodzinach podobnej wielkości): **ok. 600 akcji** plus pisanie. Nowe osoby
  z arkusza nie mają dat: jeśli notatki je podają, każda to jeszcze chip + ok. 4 akcje w [[wpis-osoby]] (D4).
- **Co skraca:** wybór z „W tym grobie” bez pisania; nazwisko podpowiedziane; „Koniec związku” schowany (D7);
  źródło bez pytania; bez pola płci (v1.1).
- **Co wydłuża świadomie:** „najpierw szukaj” — +1 dotknięcie na każdą nową osobę („Nowa osoba”). To cena
  AC-5 (D3). Wejście przez formularz osoby w poprawie — +1 dotknięcie na rodzinę (D2).

## Style B rules applied
- **Reguła 1:** jedyny wypełniony przycisk to „Zapisz”. „Dodaj osobę do pary” i „Dodaj dziecko” mają obrys i ikonę
  w akcencie; „Dodaj koniec związku” to przycisk tekstowy w linii treści (akcent); „Usuń rodzinę” — tekstowy w
  kolorze tekstu; w oknach bezpieczne działanie w akcencie.
- **Reguła 3:** ikony `outlined` — `person_add_alt_outlined`, `delete_outline`, `search`, `close`, `error_outline`;
  `close` ma `tooltip`.
- **Reguła 5:** marginesy 16 dp; między grupami (para · ślub · dzieci) 24 dp; wiersze bez odstępu (lista).
- **Reguła 6:** lata i podgląd dat jak w [[grob]] i [[wpis-osoby]].
- **Reguła 7:** komunikaty składu mówią, czego brakuje, bez „błąd”; okno usunięcia mówi, co zostaje.
- **Reguła 8:** bez znicza — arkusz to działanie.
- **Reguła 10:** zapis wraca do formularza osoby, gdzie zmiana jest widoczna w sekcji „Rodzina”, bez okienka.
- **Reguła 11:** wiersze arkusza **nie są kartami** — nie prowadzą dalej (D11). Wiersze w B to lista wyboru, jak D
  w [[zdjecie]].
- *Thresholds:* cele ≥ 48 dp (`close` 48, wiersze 56); wiersz nieaktywny niesie powód tekstem (SC 1.4.1); przyciski
  i wiersze rosną z tekstem (SC 1.4.4).
- **Nowe tokeny:** brak. Pary: tekst pomocniczy na tle 5,50:1, obrys na tle 3,40:1 (pomiar [[style-b]] 2026-10-06).

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-003 AC-1 | A3–A4, A3', A8–A9, B3, A12 | w jednym arkuszu para i dzieci; „Nowa osoba” tworzy osobę przy zapisie rodziny; po „Zapisz” wszyscy są w sekcji „Rodzina” ([[wpis-osoby]] 9a) |
| US-003 AC-2 | A4 → B5; [[wpis-osoby]] 9a „Dodaj związek” | ta sama osoba w drugim arkuszu jako para; w jej sekcji „Rodzina” dwie grupy „Związek”, każda ze swoimi dziećmi — także po rozstaniu albo owdowieniu (uwaga autora do O1) |
| US-003 AC-3 | A5, A6' | pięć dopisków przy ślubie i końcu; podgląd przed zapisem, a po zapisie w etykiecie grupy („Związek · ślub ok. 1948 · koniec 1960”) |
| US-003 AC-4 | A10 | przynależność i daty zapisują się ze źródłem „notatki” i statusem `CLAIMED`, bez pytania |
| US-003 AC-5 | B2, B4, B5, B3 | osoba z grobu jest na liście, zanim da się utworzyć nową; wybór dodaje istniejącą osobę |
| ISSUE-019: najwyżej dwie osoby w parze | A4 | przy dwóch osobach w parze przycisku nie ma |
| ISSUE-019: zapis całością | A12 | po nieudanym zapisie nic z arkusza nie ma w bazie (test `qa`) |
| ISSUE-019: styl B | całość | reguły wyżej; przegląd `ui` |

## Decisions
| Decyzja | Dlaczego | Obali |
|---|---|---|
| **D1 — arkusz ma własne „Zapisz” i zapisuje się od razu**, nie z „Zapisz” formularza osoby | rodzina to osobny rekord, który dotyka kilku osób; arkusz ma własne pola. W aplikacji „Gotowe” wraca do formularza bez zapisu (zdjęcia, [[zdjecia-osoby]] D1), a „Zapisz” zapisuje (jak okno „Popraw grób”) — arkusz mówi „Zapisz” | autor oczekuje, że „Odrzuć” w formularzu osoby cofnie też rodzinę |
| **D2 — arkusz otwiera się z formularza osoby w poprawie**, nie przy nowej osobie | arkusz pokazuje „tę osobę”, więc musi ona już istnieć; formularz nowej osoby nie zapisuje się po cichu. Koszt: +1 dotknięcie (karta w [[grob]]) na rodzinę | autor przy przepisywaniu grobu chce dodać rodzinę od razu przy nowej osobie → „Zapisz i dodaj rodzinę” |
| **D3 — najpierw szukaj, potem twórz** (B: pole z fokusem, „Nowa osoba” nad listą) | AC-5: duplikat osoby rozbija rodziny i ścieżkę (dwie te same osoby w różnych rodzinach). Koszt: +1 dotknięcie na nową osobę | autor przy nowych osobach nie patrzy na listę → „Nowe dziecko” wprost w arkuszu, a duplikaty łapie dopiero ostrzeżenie |
| **D4 — nowa osoba w arkuszu to imiona i nazwisko**; daty i reszta w jej wpisie (chip) | arkusz to szybkość dla całej rodziny; pełny formularz w środku arkusza to zapis w zapisie. *Family group sheet* ma przy dziecku datę urodzenia, ale tu przy każdej osobie z notatek byłby to blok daty | przy przepisywaniu prawie każda nowa osoba ma w notatkach daty → rok urodzenia w wierszu A3' (+1 pole) |
| **D5 — dziecko ma jedną rodzinę rodziców**; osoba z rodzicami jest w B nieaktywna („ma już rodziców”) | druga rodzina rodziców to sprzeczne twierdzenie albo przysposobienie: pierwsze to [[US-004-fakt-od-babci]], drugie jest poza zakresem. Blokada chroni przed pomyłkowym podpięciem | w notatkach jest przysposobienie albo dwie wersje rodziców |
| **D6 — rodzina musi mieć osobę w parze** | [[FR-002-rodzina-jako-rekord]]: 1–2 partnerów i dzieci; AC-1 też mówi „1-2 partnerów” | notatki znają rodzeństwo bez imion rodziców → rodzina bez pary (schemat tego nie zabrania) |
| **D7 — „Koniec związku” schowany za przyciskiem**, z linią „np. rozwód albo rozstanie. Owdowienie to zgon osoby — zapisuje się w jej wpisie.” (v1.1) | w notatkach rzadki; schowany nie kosztuje `next` w każdej rodzinie. Linia zapobiega wpisaniu daty śmierci drugi raz | notatki często mają rozwody albo autor wpisuje tam daty zgonu |
| **D8 — „Usuń rodzinę” w poprawie, z oknem** — element spoza AC | bez niego pomyłkowo utworzona rodzina nie ma wyjścia (arkusz nie zapisze rodziny z jedną osobą). Osoby zostają, znikają tylko powiązania. Okno, więc to nie jest ciche usunięcie (brief G7/C5) | autor woli bez usuwania, jak przy osobie ([[wpis-osoby]] → „Bez usuwania osoby”) |
| ~~**D9 — rola w wierszu i w chipie z płci**~~ — **obalone na stopie #1** (autor: bez płci) → **D9' — nazwy neutralne, bez kolumny roli w arkuszu** (*Role names*) | odchodzi od R4 („Mąż: Jan”, „Córka: Anna”) świadomie: płci nie ma w danych, a zgadywanie z imienia autor odrzucił. Chip mówi „Rodzic”, „Partner”, „Dziecko” | nazwy relacji na ścieżce i w drzewie (EPIC-003, R3: „jej tata”, „jej mąż”) albo powinowactwo („teść”) okażą się potrzebne → płeć wraca jako pole osoby, wtedy z migracją |
| ~~**D10 — kolejność dzieci: dodania**~~ — **zastąpione na stopie #1** (decyzja autora D4) → **D10' — według daty urodzenia** (A8, [[wpis-osoby]] 9a) | kanon GEDCOM 7: *„The order of the CHIL (children) pointers … should be chronological by birth”*. Z D10 zostaje tylko to, że wiersz dodany w trakcie edycji nie skacze | — |
| **D11 — wiersze arkusza nie prowadzą do wpisu osoby** | arkusz nie jest bramą do kolejnych formularzy (zapis w zapisie, utrata zmian w arkuszu); osobę poprawia się przez chip w jej rodzinie | autor po zapisie rodziny od razu chce dopisać daty nowych dzieci i chip jest za daleko |

## Open
**Rozstrzygnięte na stopie #1 [[ISSUE-019-family-relations]] (2026-10-07):** 1 → **C**, z uwagą autora o rozstaniach,
owdowieniach i nowych związkach (v1.1: słowo „związek”); 2 → **bez płci** (P2); 3 → **bez rodzeństwa**. Treść pytań
zostaje niżej jako zapis tego, co rozważano.

1. ~~⚠️ OPEN~~ **— droga wejścia relacji** (US-003 → *Notes*; [[wpis-osoby]] → *Decisions* → „Zdjęcie i relacje później”).
   - **C (rekomendacja): relacje widać w formularzu osoby (9a, chipy jak R4), a wpisuje się je arkuszem** (ten
     plik), otwieranym z tej sekcji. Kanon briefu i FR-002 mówią „rodziną naraz”, R4 i uwaga autora — „przy osobie”.
     Warunek, który obalał kierunek z v2 („arkusz → relacje nie trafiają do formularza”), trafił częściowo:
     **wpisywanie** jest w arkuszu, **widok** w formularzu.
   - A: relacje po jednej z formularza osoby („Dodaj ojca”, „Dodaj męża”, „Dodaj dziecko”), a pod spodem dalej
     rodziny, które aplikacja dobiera sama. Bez nowego ekranu arkusza, ale sprzeczne z FR-002 (wpis osoba po osobie
     → zmiana FR), a przy powtórnym małżeństwie „Dodaj dziecko” musi pytać, z którą parą.
   - B: sam arkusz, wejście z [[grob]], bez sekcji w formularzu — nie odpowiada na uwagę autora (relacji nie widać
     przy osobie).
2. ~~⚠️ OPEN~~ **— płeć osoby** (wybrane P2; pomiar reguły z imienia — [[ISSUE-019-family-relations]] → *Prior art*). `Persons` nie ma płci, a od niej zależą nazwy relacji (*Role names*).
   - **P1 (rekomendacja): pole „Płeć” w formularzu osoby** ([[wpis-osoby]] 4a: Kobieta · Mężczyzna; bez wyboru =
     nieznana), **podpowiedziane z imienia** przy nowej osobie i w wierszu A3': pierwsze imię na „-a” → Kobieta,
     inne → Mężczyzna, bez imion — bez wyboru. Podpowiedź widać w polu i w nazwie roli, zmiana to jedno dotknięcie.
     +0 akcji przy trafnej podpowiedzi. Ryzyko: imiona męskie na „-a” (np. Kuba, Barnaba) dostaną złą podpowiedź
     — widoczną od razu. Poprawa wpisu nigdy nie zmienia płci sama. Schemat v6 dostaje kolumnę płci (w GEDCOM 7
     osoba ma `SEX` — `planning` cytuje specyfikację). Płeć bez źródła, jak imiona ([[FR-001-provenance]] →
     ziarnistość: twierdzenia na datach, relacjach i pochówku).
   - P1': to samo pole bez podpowiedzi — +1 dotknięcie na osobę (ok. 100 na całe notatki).
   - P2: bez płci — nazwy neutralne („Rodzic”, „Małżonek”, „Dziecko”), 0 akcji, osoba w schemacie bez zmian.
     Odchodzi od R4, a ścieżka z R3 („jej tata”, „jej mąż”) i powinowactwo z uwagi autora („teść”) będą potrzebować
     płci później — wtedy z migracją i uzupełnianiem ok. 100 osób.
3. ~~⚠️ OPEN~~ **— relacje dalsze w sekcji „Rodzina”** (wybrany wariant węższy) ([[wpis-osoby]] 9a).
   - **Rekomendacja: rodzeństwo tak** — to inne dzieci tej samej rodziny rodziców, bez nowych danych i bez nowego
     wpisywania (chipy „Brat: …”, „Siostra: …”). **Teściowie, dziadkowie i dalsi — nie:** to ścieżka przez dwie
     rodziny i więcej, czyli sekcja „Jak łączy się ze mną” z R4 prawego ([[EPIC-002-wizyta]], M5).
   - Wariant węższy: same rodziny osoby (rodzice, małżonkowie, dzieci).

**Poza zakresem tej wersji** (nazwane, żeby nie poszerzać po cichu): osoba żyjąca (`is_living` zostaje wartością
domyślną, czyli „nie żyje”, także dla żyjących osób dodanych arkuszem; ekran nie pokazuje tego nigdzie, a pole
przyjdzie z eksportem, który od niego zależy — [[US-006-eksport-dla-rodziny]]); kontrola, czy nikt nie jest swoim
przodkiem (poza blokadą w B); rodzaj więzi dziecka z rodzicami (przysposobienie — D5).
