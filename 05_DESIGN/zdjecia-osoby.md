---
screen: "Zdjęcia osoby — baza zdjęć jednej osoby"
items: ["[[ISSUE-017-person-photos]]", "[[ISSUE-018-profile-photo-crop]]", "[[ISSUE-024-person-view]]", "[[ISSUE-048-portrait-photos]]"]
us: "[[US-005-zdjecia]]"
journey-step: "n/a — M1 (przepisywanie i zbieranie u babci); docelowo część widoku osoby (M5, R4 prawy)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-zdjecia-osoby.html (ramki 1–9) · 2026-10-19: makieta-048.html (ekran 2 „Zdjęcie profilowe”, ISSUE-048)"
updated: 2026-10-19
---

# Zdjęcia osoby — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.9, reguła 14) · referencja: [[references]] → **R4
> (prawy ekran)** — okrągły portret u góry. Bazy zdjęć osoby żadna referencja nie pokazuje, więc siatka dziedziczy
> reguły stylu B.
>
> **Wersja 1 (2026-10-07, przed planem [[ISSUE-017-person-photos]]).** Decyzja autora na stopie #1 ISSUE-016:
> *„osoby chciałbym, aby miały «swoją bazę zdjęć» (lub dzieloną, jeżeli na zdjęciu jest kilka osób) i możliwość
> wybierania z nich «profilowego»”*. Ten ekran to ta baza. Podgląd jednego zdjęcia i wybór osób na zdjęciu są w
> [[zdjecie]] (B w trybie osoby, D), a wejście z formularza w [[wpis-osoby]] v4 (element 1a).
>
> **Wersja 1.1 (2026-10-07, przed planem [[ISSUE-018-profile-photo-crop]]):** nagłówek (element 2) pokazuje profilowe
> **w kadrze** z [[kadr-profilowego]]; profilowe bez kadru — jak dotąd, ze środka. Kadr ustawia się z podglądu
> ([[zdjecie]] v1.4, B4'), a jego zmiana pokazuje linię zapisu (element 6). Siatka bez zmian.
>
> **Wersja 1.2 (2026-10-09, przed planem [[ISSUE-024-person-view]]):** wejście z widoku osoby ([[osoba]] element 10).
> **Tryb oglądania** (W2 — decyzja autora na stopie #1 ISSUE-024): bez kafelka „Dodaj zdjęcie” (5) i bez linii zapisu (6),
> podgląd bez działań ([[zdjecie]] v1.5). Zmiany zdjęć dalej tylko z formularza (D1). Tło osoby nie ma znacznika w siatce
> (reguła 14); mówi o nim opis komórki dla czytnika: „Zdjęcie 3 z 4, tło — otwórz”.
>
> **Wersja 1.3 (2026-10-09, przegląd `ui` ISSUE-024):** baza w trybie oglądania jest **bez dolnego paska**, jak ten sam ekran z
> formularza ([[style-b]] reguła 12 — ekran zdjęć jest piętrem pod widokiem, powrót daje „wstecz”).

> **Wersja 1.4 (2026-10-09, stop #2 [[ISSUE-024-person-view]], runda 1 — tryb „Zdjęcie w tle”, [[osoba]] D21):** z pasma tła w
> widoku osoby. Pasek: wstecz, tytuł „Zdjęcie w tle”, podtytuł — imię i nazwisko. Pod paskiem „Dotknij zdjęcia, które ma być w tle.”
> (14 sp, tekst pomocniczy; osoba bez zdjęć — „Ta osoba nie ma jeszcze zdjęć. Dodaj zdjęcie, które ma być w tle.”). **Siatka zdjęć tej osoby** jak element 4 (bez nagłówka profilowego); obecne tło ma **obrys 2 dp w
> akcencie** wokół komórki, pod nim 2 dp koloru tła, a zdjęcie w środku mniejsze, z promieniem 4 dp — jak ramka kadru (akcent/tło
> 8,81:1 na każdym zdjęciu, a zmiana obrysu zdjęcia mówi to bez koloru; przegląd `ui`) (zaznaczenie — reguła 1) i dla czytnika „…, tło, zaznaczone — wybierz”; pozostałe „Zdjęcie 2 z 4 —
> ustaw jako tło”. **Kafelek „Dodaj zdjęcie”** → arkusz źródła (tytuł „Zdjęcie w tle”; galeria — **jedno** zdjęcie, aparat — jedno).
> **Dotknięcie zdjęcia albo zdjęcie dodane → tło zapisuje się od razu** i ekran wraca do widoku osoby z tłem (reguła 10). Gdy tło
> jest: pod siatką przycisk tekstowy **„Bez zdjęcia w tle”** (`hide_image_outlined`, kolor tekstu) → tło zdjęte, zdjęcie zostaje,
> powrót do widoku. Wstecz — bez zmian. Zdjęcie dodane tutaj dołącza do zdjęć osoby (na końcu; osobie bez zdjęć — też profilowe).
>
> **Wersja 1.5 (2026-10-19, `ui` przed planem [[ISSUE-048-portrait-photos]] — tryb „Zdjęcie profilowe”, [[osoba]] D23):** z portretu w widoku
> osoby. Autor: *„gdy klikam na kogoś „zdjęcie profilowe”, chciałbym od razu widzieć tam możliwość jego zmiany (lub dodania dla tej osoby nowych
> zdjęć — podobnie jak działa zdjęcie w tle)”*. Ten sam ekran co tryb tła, z obecnym profilowym na górze i „Obejrzyj zdjęcie”. Dotknięcie zdjęcia
> → kadr → „Gotowe” → **zapis od razu** i powrót do widoku osoby. Kafelek **„Dodaj zdjęcia”** dodaje kilka naraz (także „Ze zdjęć w aplikacji” —
> [[zdjecia-w-aplikacji]]), **zapis od razu**, a ekran zostaje z nowymi zdjęciami w siatce. Elementy: *Tryb „Zdjęcie profilowe”* niżej. Wariant
> **P2** — przyjęty przez autora na stopie #1 (2026-10-19, *„tak”*); odrzucony P1 (arkusz z działaniami) — [[osoba]] *Open* 7.
> **D6 *Obali* trafione** — trzecie źródło w arkuszu: „Ze zdjęć w aplikacji” ([[zdjecie]] A4, v1.7).
>
> **Wersja 1.6 (2026-10-19, przegląd `ui` zbudowanej [[ISSUE-048-portrait-photos]] — przyjęte odstępstwo 2 `dev`):** nieudany zapis w trybie
> „Zdjęcie profilowe” cofa siatkę do zapisanego stanu, **także zdjęcia dodane kafelkiem w tej próbie** — trzeba je dodać jeszcze raz (D8). v1.5 mówiła
> tylko o profilowym.

## Purpose
Wszystkie zdjęcia jednej osoby w jednym miejscu: tu się je dodaje (z galerii kilka naraz albo aparatem), wybiera
**profilowe** i otwiera, żeby zaznaczyć, kto jeszcze jest na zdjęciu (US-005 AC-1, ISSUE-017 AC 4–6). Profilowe to
zdjęcie, które widać w formularzu osoby i w karcie osoby w [[grob]].

**Model w jednym zdaniu** (kanon: [GEDCOM 7.0](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html), cytaty
w [[ISSUE-016-photos-grave-and-person]] → *Stop #1 — round 1*): zdjęcie to osobny rekord, osoba ma do niego
**łącze** (`OBJE`), łącza osoby mają kolejność, a *„the first is the most-preferred value”*, więc **profilowe =
pierwsze łącze**. Jedno zdjęcie może mieć łącza od kilku osób, a każda z nich ma własne profilowe. Model danych
rozstrzyga ADR w `planning`. Ekran zakłada tylko te trzy rzeczy: łącze, kolejność i „pierwsze = profilowe”.

## Navigation
- **Wejście:** z [[wpis-osoby]] → element 1a, gdy osoba ma choć jedno zdjęcie (także dopiero wybrane, jeszcze
  niezapisane). Bez zdjęć element 1a otwiera od razu arkusz źródła ([[zdjecie]] A), bez pustej bazy.
  **Z widoku osoby** ([[osoba]] element 10, v1.2) — w trybie oglądania. Wstecz → widok osoby.
  **Z portretu w widoku osoby** ([[osoba]] element 3, v1.5) — w trybie „Zdjęcie profilowe” (*Tryb „Zdjęcie profilowe”* niżej). Wstecz → widok
  osoby; zdjęcia dodane kafelkiem są już zapisane.
- **Zdjęcie w siatce albo profilowe w nagłówku** → podgląd ([[zdjecie]] B, tryb osoby): przybliżenie, poprzednie i
  następne, „Na zdjęciu”, „Ustaw jako profilowe”, „Usuń z tej osoby”.
- **„Dodaj zdjęcie”** (kafelek w siatce) → arkusz źródła ([[zdjecie]] A, tytuł „Zdjęcia osoby”). Galeria pozwala
  wybrać kilka zdjęć, aparat robi jedno.
- **Wstecz** → [[wpis-osoby]], **ze zmianami zachowanymi w formularzu**, ale jeszcze niezapisanymi. Zapisuje je
  „Zapisz” formularza razem z wpisem osoby, a „Odrzuć” w oknie „Odrzucić wpis?” cofa je wszystkie (D1).
  Bez okna przy wyjściu z tego ekranu, bo nic tu nie przepada.

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** wstecz; tytuł „Zdjęcia” (16 sp, półgruby); podtytuł — imiona i nazwisko osoby jak w formularzu w tej chwili (14 sp, tekst pomocniczy, jedna linia, ucięta); bez imion i nazwiska: „Nowa osoba” | pasek | wstecz → [[wpis-osoby]] | — | — | decyzja projektowa |
| 2 | **Profilowe** — nagłówek wyśrodkowany: okrąg **96 dp** z profilowym (pierwsze łącze), w kadrze łącza ([[kadr-profilowego]], v1.1), a bez kadru przycięty ze środka; pod nim „Profilowe” (13 sp, tekst pomocniczy); odstęp 24 dp od paska i 24 dp do siatki. Opis dla czytnika: „Zdjęcie profilowe — otwórz” | obraz-przycisk (cel 96 dp) | dotknięcie → [[zdjecie]] B na tym zdjęciu | pierwsze zdjęcie osoby | — | ISSUE-017 AC 4 · R4 prawy · D2 |
| 3 | **Nagłówek sekcji:** „Wszystkie zdjęcia · 3” — ikona `photo_library_outlined` w akcencie (reguła 3: nagłówek sekcji), tekst 14 sp półgruby w kolorze tekstu; sama liczba po kropce, bez rzeczownika, więc bez odmiany | tekst | — | — | — | decyzja projektowa · R4 (nagłówki sekcji z ikoną) |
| 4 | **Siatka zdjęć** — 3 kolumny, kwadraty z zaokrągleniem 8 dp, odstęp 8 dp, marginesy 16 dp; zdjęcie przycięte ze środka. **Kolejność łączy:** profilowe pierwsze, dalej w kolejności dodania. Nic na zdjęciach (reguła 14) — profilowe w siatce nie ma znacznika, bo pokazuje je element 2. Opis każdej komórki dla czytnika: „Zdjęcie 2 z 3 — otwórz”, a przy pierwszym „Zdjęcie 1 z 3, profilowe — otwórz” | siatka obrazów-przycisków (komórka ok. 104 dp przy 360 dp szerokości, ok. 121 dp przy 411) | dotknięcie → [[zdjecie]] B na tym zdjęciu | — | — | ISSUE-017 AC 4 · US-005 AC-1 · D3 · [[style-b]] reguła 14 (v1.9) |
| 5 | **Kafelek „Dodaj zdjęcie”** — ostatnia komórka siatki, tej samej wielkości: obrys 1 dp w kolorze obrysu na tle (bez wypełnienia), zaokrąglenie 8 dp, w środku `add_a_photo_outlined` (28 dp, akcent) i pod nią „Dodaj zdjęcie” (14 sp, półgruby 500, kolor tekstu, do 2 linii). Opis dla czytnika „Dodaj zdjęcie osoby” | przycisk | → [[zdjecie]] A (galeria — kilka zdjęć, aparat — jedno) | — | — | US-005 AC-1 · D4 · D5 · [[grob]] D12 (działanie tam, gdzie pojawi się wynik) |
| 6 | **Linia zapisu** pod siatką: „Zmiany zdjęć zapiszą się razem z wpisem osoby.” (13 sp, tekst pomocniczy) — tylko gdy na tym ekranie, w podglądzie albo w kadrze coś zmieniono, a wpis nie jest jeszcze zapisany | tekst | — | ukryta | — | D1 · [[style-b]] reguła 7 |

**Dane, których ekran potrzebuje** (dla `planning`):
- zdjęcia osoby w kolejności łączy, czyli zapisane łącza plus zmiany z tej edycji formularza;
- profilowe, czyli pierwsze łącze;
- liczba zdjęć;
- plik każdego zdjęcia: z magazynu aplikacji albo, gdy zdjęcie jest dopiero wybrane, przygotowany plik z katalogu
  roboczego ([[ADR-008-photos-access-copy-and-backup-consistency]]: plik powstaje przed wierszem).

Miniatury dekodowane w rozmiarze komórki, jak w [[grob]].

### Tryb „Zdjęcie profilowe” (v1.5, [[ISSUE-048-portrait-photos]])
Z portretu w widoku osoby. Wzorem jest tryb „Zdjęcie w tle” (v1.4): siatka zdjęć tej osoby, obecny wybór w ramce, dotknięcie wybiera, zapis od
razu. Różnice:

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| P1 | **Pasek:** wstecz; tytuł „Zdjęcie profilowe” (16 sp, półgruby); podtytuł — imiona i nazwisko z „z d.” (14 sp, tekst pomocniczy, jedna linia, ucięta) | pasek | wstecz → widok osoby | — | — | wzorzec v1.4 |
| P2 | **Obecne profilowe** — jak element 2: okrąg 96 dp w kadrze łącza, wyśrodkowany, 24 dp pod paskiem; dotknięcie → podgląd. Pod nim zamiast podpisu „Profilowe” **przycisk tekstowy „Obejrzyj zdjęcie”** (akcent, 14 sp, waga 500, cel ≥ 48 dp) → [[zdjecie]] B w trybie oglądania na profilowym (jak dziś z portretu). Opis okręgu dla czytnika: „Zdjęcie profilowe — obejrzyj” | obraz-przycisk + przycisk tekstowy | → [[zdjecie]] B, tryb oglądania | — | — | AC-1 („obejrzyj”) · D2 |
| P3 | **Linia:** „Dotknij zdjęcia, które ma być profilowym.” (14 sp, tekst pomocniczy, 16 dp marginesu) — jak linia trybu tła | tekst | — | — | — | AC-1 („zmień profilowe”) · wzorzec v1.4 |
| P4 | **Nagłówek sekcji** — element 3 („Wszystkie zdjęcia · 3”) | tekst | — | — | — | element 3 |
| P5 | **Siatka** jak element 4. **Obecne profilowe** (pierwsza komórka) ma ramkę jak obecne tło w v1.4 (2 dp akcentu, 2 dp tła, zdjęcie mniejsze, promień 4 dp). **Dotknięcie zdjęcia → [[kadr-profilowego]]** z kadrem łącza albo domyślnym; „Gotowe” → zdjęcie staje się pierwszym łączem z tym kadrem, **zapis od razu**, powrót do widoku osoby z nowym portretem (reguła 10). Dotknięcie obecnego profilowego → kadr („Popraw kadr”), „Gotowe” → nowy kadr, zapis od razu, widok osoby. Opis komórki dla czytnika: „Zdjęcie 1 z 3, profilowe, zaznaczone — popraw kadr”; pozostałe „Zdjęcie 2 z 3 — ustaw jako profilowe” | siatka obrazów-przycisków | → [[kadr-profilowego]] → widok osoby | — | — | AC-2 · [[osoba]] D24 · [[kadr-profilowego]] v1.3 |
| P6 | **Kafelek „Dodaj zdjęcia”** — jak element 5, napis w liczbie mnogiej. → arkusz źródła ([[zdjecie]] A, tryb osoby, tytuł „Zdjęcia osoby”): galeria — **kilka**, aparat — jedno, **„Ze zdjęć w aplikacji”** — kilka ([[zdjecia-w-aplikacji]]). Nowe zdjęcia dołączają na końcu kolejności, **zapisują się od razu**, a ekran **zostaje** z nimi w siatce — jednym dotknięciem któreś zostaje profilowym. Profilowe się nie zmienia (osoba ma zdjęcia, więc pierwsze łącze zostaje). Przygotowanie i jego błąd — jak *States* („przygotowanie zdjęć”) | przycisk | → [[zdjecie]] A | — | — | AC-1 („dodaj zdjęcia”) · D7 |

**Bez linii zapisu** (6) — nic nie czeka na „Zapisz”. **Bez „Bez profilowego”** — profilowe to pierwsze zdjęcie osoby
([[ADR-009-person-photos-record-and-link]]); zdjęcia usuwa się dalej tylko pod ✎ (podgląd → „Usuń z tej osoby”).
**Zapis — błąd:** pod siatką `error_outline` + „Nie udało się zapisać zdjęć. Spróbuj jeszcze raz.” (kolor błędu, 14 sp); w kadrze „Gotowe”
wraca tu z tym komunikatem i starym profilowym. **v1.6:** siatka wraca do zapisanego stanu — zdjęcia dodane kafelkiem w tej próbie znikają z niej i
dodaje się je jeszcze raz (D8).

## States
| Stan | Co widać |
|---|---|
| wypełniony | 1–5; 6, gdy są niezapisane zmiany |
| jedno zdjęcie | nagłówek 2 i siatka z jednym zdjęciem i kafelkiem „Dodaj zdjęcie” |
| przygotowanie zdjęć | po powrocie z galerii albo aparatu: w miejscu każdego nowego zdjęcia komórka na powierzchni (zaokrąglenie 8 dp) ze wskaźnikiem postępu w środku; kafelek 5 nieaktywny. Zmniejszanie trwa chwilę na zdjęcie (ADR-008: 2048 px, JPEG 85). Nowe zdjęcia pojawiają się po kolei. **W „Zdjęciu profilowym” (v1.5, przegląd `ui` — MAJOR) czekają też zdjęcia siatki:** dotknięcie w trakcie przygotowania i zapisu nic nie robi — „Gotowe” w kadrze zamknęłoby ekran i szkic, a zdjęcia w przygotowaniu przepadłyby bez słowa |
| przygotowanie — błąd | pod siatką: `error_outline` + „Nie udało się wczytać 1 zdjęcia z 3. Spróbuj jeszcze raz.” (kolor błędu, 14 sp; liczby z odmianą). Udane zdjęcia zostają |
| pusty | osoba miała zdjęcia, a w tej edycji wszystkie usunięto: bez nagłówka 2; „Ta osoba nie ma zdjęć.” (14 sp, tekst pomocniczy) nad siatką z samym kafelkiem 5 (reguła 9) i linia 6. Bez zdjęć formularz tu nie prowadzi (*Navigation*) |
| brak pliku | łącze jest, pliku nie ma albo nie da się go odczytać: komórka na powierzchni z `broken_image_outlined` (tekst pomocniczy), bez tekstu; dotknięcie → podgląd ze stanem „B — błąd odczytu”, gdzie da się zdjęcie usunąć z osoby. W nagłówku 2 ta sama ikona w okręgu na powierzchni |
| wczytywanie | tło; siatka pojawia się, gdy lista łączy jest gotowa (ułamek sekundy, bez wskaźnika — jak [[zdjecie]] „B — wczytywanie”) |

## Sketch
```
┌──────────────────────────────────┐
│ ←  Zdjęcia                       │
│    Anna Wymyślona z d. Zmyślona  │
│                                  │
│             ╭──────╮             │
│             │▓▓▓▓▓▓│  ← profilowe│
│             │▓▓▓▓▓▓│    okrąg 96 │
│             ╰──────╯             │
│             Profilowe            │
│                                  │
│  ▣ Wszystkie zdjęcia · 3         │  ← ikona w akcencie
│ ╭────────╮ ╭────────╮ ╭────────╮ │
│ │▓▓▓▓▓▓▓▓│ │░░░░░░░░│ │▒▒▒▒▒▒▒▒│ │  ← kwadraty, przycięte
│ │▓▓▓▓▓▓▓▓│ │░░░░░░░░│ │▒▒▒▒▒▒▒▒│ │    ze środka
│ ╰────────╯ ╰────────╯ ╰────────╯ │
│ ╭────────╮                       │
│ │   📷+   │  ← kafelek z obrysem │
│ │  Dodaj  │                      │
│ │ zdjęcie │                      │
│ ╰────────╯                       │
│  Zmiany zdjęć zapiszą się razem  │
│  z wpisem osoby.                 │
└──────────────────────────────────┘
```

## Tempo
Rekordem jest **zdjęcie osoby**. Ile ich będzie, nie wiadomo: notatki nie mają zdjęć ([[NT-001-photograph-the-notes]]
to zdjęcia stron, nie osób), a zdjęcia osób przychodzą z albumów, od babci i z galerii. **Założenie do sprawdzenia:**
ok. 50 zdjęć osób w MVP.

| Działanie | Dotknięcia | Uwagi |
|---|---|---|
| **Pierwsze zdjęcie osoby** z formularza (1a puste → „Wybierz z galerii” → zdjęcie → „Gotowe”) | 4 | jak nagrobek; okno systemowe na Androidzie 16 wymaga „Gotowe” ([[zdjecie]] v1.2). Bez bazy po drodze |
| **Kilka zdjęć naraz** z galerii | 4 + 1 na każde kolejne | „Gotowe” i tak trzeba dotknąć, więc wybór kilku nic nie kosztuje (D4) |
| **Kolejne zdjęcie** osobie, która już ma zdjęcia (1a → kafelek 5 → galeria → zdjęcie → „Gotowe”) | 5 | — |
| **Profilowe** (zdjęcie w siatce → „Ustaw jako profilowe” → wstecz) | 3 | — |
| **Profilowe z widoku osoby** (v1.5: portret → zdjęcie → „Gotowe” w kadrze) | **3** | zapis od razu; przez ✎ było ✎ → 1a → zdjęcie → „Ustaw jako profilowe” → „Gotowe” → wstecz → wstecz → „Zapisz” = 8 |
| **Kolejne zdjęcia z widoku osoby** (v1.5: portret → „Dodaj zdjęcia” → „Wybierz z galerii” → zdjęcia → „Gotowe” → wstecz) | 6 + 1 na każde kolejne | zapis od razu |
| **Zdjęcie dzielone z osobą z tego grobu** (zdjęcie → „Zmień” przy „Na zdjęciu” → zaznaczenie → „Gotowe”) | 4 | [[zdjecie]] D |
| Zapis zmian | +1 („Zapisz” formularza) | D1. W nowej osobie „Zapisz” i tak jest, więc +0 |
| **Osoba bez zdjęć** | **+0** | element 1a stoi poza `next` ([[wpis-osoby]] → *Tempo*) |

Przy założonych ok. 50 zdjęciach: ok. 50 × 4–5 = **ok. 200–250 dotknięć**, plus dzielenie tam, gdzie zdjęcie jest
grupowe.

## Style B rules applied
- **Reguła 14 (v1.9):** w bazie zdjęcia są **kwadratami** (promień 8 dp), bo zdjęcia osób bywają grupowe, a okrąg
  ucinałby najwięcej. **Okrąg tylko dla profilowego** (nagłówek 96 dp, formularz 80 dp, karta 40 dp), bo profilowe
  oznacza osobę. Nic na zdjęciach. Profilowego nie oznaczamy w siatce znacznikiem na zdjęciu, tylko nagłówkiem 2 i
  opisem dla czytnika.
- **Reguła 1:** na ekranie nie ma wypełnionego przycisku: treścią są zdjęcia, a jedynym działaniem jest kafelek z
  obrysem i ikoną w akcencie.
- **Reguła 3:** `add_a_photo_outlined` i ikona nagłówka sekcji w akcencie; `broken_image_outlined` w tekście
  pomocniczym (opisuje).
- **Reguły 9 i 11:** pusty stan mówi faktem, co tu jest, i daje jedno działanie; bez zastępczych obrazków — kafelek
  „Dodaj zdjęcie” to przycisk, nie szary prostokąt.
- **Reguła 7:** linia 6 mówi, kiedy zmiany się zapiszą, bez ostrzeżenia.
- **Reguła 10:** dodanie kończy się zdjęciem w siatce, bez okienka.
- **Tokeny:** bez nowych. Obrys kafelka to para obrys/tło (3,40:1, SC 1.4.11 ✅).

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-005 AC-1 (osoba) | 5 → [[zdjecie]] A; 2, 4 | zdjęcie z galerii albo aparatu pojawia się w siatce, a pierwsze — w nagłówku, w formularzu i w karcie w [[grob]] |
| US-005 AC-2 | 4 | po zapisie zdjęcie otwiera się z magazynu aplikacji także po usunięciu oryginału z galerii |
| US-005 AC-3 | 2, 4 | po odtworzeniu z kopii te same zdjęcia w tej samej kolejności i to samo profilowe (odcisk danych — `qa`) |
| ISSUE-017: kilka zdjęć, jedno profilowe | 2, 3, 4 → [[zdjecie]] B4 | siatka z kilkoma zdjęciami; „Ustaw jako profilowe” przenosi zdjęcie na pierwsze miejsce, a nagłówek 2 się zmienia |
| ISSUE-017: jedno zdjęcie u kilku osób, jeden plik | 4 → [[zdjecie]] B5, D | zdjęcie zaznaczone u drugiej osoby pojawia się w jej bazie; plik jest jeden (sprawdza `qa` w magazynie aplikacji) |
| ISSUE-017: usunięcie u jednej osoby nie usuwa innym | 4 → [[zdjecie]] C (tryb osoby) | po „Usuń z tej osoby” zdjęcie znika z tej bazy, a w bazie drugiej osoby zostaje |
| ISSUE-017: styl B | całość | reguły wyżej; przegląd `ui` przed stopem #2 |
| ISSUE-048 AC-1 — z portretu widać: obejrzyj, zmień profilowe, dodaj zdjęcia (v1.5) | P2, P3, P6 | portret Jana → „Zdjęcie profilowe”: „Obejrzyj zdjęcie”, „Dotknij zdjęcia, które ma być profilowym.”, kafelek „Dodaj zdjęcia” — bez ✎ |
| ISSUE-048 AC-2 — profilowe z portretu zapisuje się od razu (v1.5) | P5 → [[kadr-profilowego]] | zdjęcie ślubne → „Gotowe” → widok Jana z nowym portretem; po wyjściu z aplikacji i powrocie — ten sam |
| ISSUE-017: migracja v3→v4, kopia v3 w v4, kopia zaraz po migracji | n/a — bez elementu ekranu | warstwa danych; sprawdza `qa`. Na ekranie: osoba ze zdjęciem z v3 ma po migracji to zdjęcie jako profilowe i jedyne w bazie |

## Decisions
| Decyzja | Dlaczego | Obali |
|---|---|---|
| **D1 — zmiany zdjęć zapisują się z „Zapisz” formularza**, nie od razu | „Zapis jest całością” ([[wpis-osoby]] v2, D-zdjęcie-2): osoba i jej zdjęcia powstają razem albo wcale, a „Odrzuć” cofa wszystko. Ten sam przepływ działa przy **nowej osobie**, której jeszcze nie ma w bazie. Inaczej niż przy nagrobku, który zapisuje się od razu, bo widok grobu nie ma formularza ([[grob]] → *Navigation*). Koszt: zmiana samych zdjęć istniejącej osoby to +1 dotknięcie („Zapisz”) | na stopie #2 autor czuje dwie zasady (nagrobek od razu, osoba z „Zapisz”) albo gubi zmiany → zapis od razu, a w nowej osobie zdjęcia dopiero po pierwszym zapisie |
| **D2 — profilowe w nagłówku jako okrąg** | autor widzi, jak profilowe wypadnie w okręgu karty i formularza (przycięte ze środka), zanim je ustawi. To ten sam portret co w R4 prawym, więc nagłówek przejdzie do widoku osoby (M5) | — |
| **D3 — siatka kwadratów, kolejność łączy** | zdjęcia osoby bywają grupowe, więc kwadrat ucina mniej niż okrąg. Całość jest o jedno dotknięcie dalej, w podglądzie. Kolejność łączy (profilowe pierwsze, dalej według dodania) to porządek GEDCOM. **Bez przestawiania** zdjęć poza profilowym, bo dziś kolejność niczego poza profilowym nie zmienia | autor chce porządkować zdjęcia (np. według lat) → przestawianie albo data zdjęcia, osobna pozycja |
| **D4 — kilka zdjęć naraz z galerii** | okno systemowe i tak wymaga „Gotowe” ([[zdjecie]] D2), więc wybór kilku nic nie kosztuje, a zdjęcia jednej osoby (np. z jednego albumu) przychodzą seriami. Obiecane w [[zdjecie]] D2 | — |
| **D5 — „Dodaj zdjęcie” jako ostatnia komórka siatki** | działanie stoi tam, gdzie pojawi się wynik, jak „Dodaj zdjęcie nagrobka” ([[grob]] D12, decyzja autora) | osoby mają po kilkanaście zdjęć i kafelek ucieka za ekran → rząd działań nad siatką |
| **D6 — dzielenie od strony zdjęcia** („Kto jest na zdjęciu?”, [[zdjecie]] D), a nie przez wybór „zdjęcia innej osoby” przy dodawaniu | zdjęcie grupowe zaznacza się raz, w jednym miejscu, i widać od razu wszystkich na nim. Druga droga (wybór spośród zdjęć w aplikacji) dawałaby to samo dwa razy. Dodanie zdjęcia jednej osoby kosztuje +0 | autor częściej szuka „tego zdjęcia ślubnego, które już jest u żony” niż otwiera zdjęcie → trzecia pozycja w arkuszu źródła: „Ze zdjęć w aplikacji”. **Trafione (v1.5, 2026-10-19):** autor przy ISSUE-024 i w przeglądzie 2026-10-18 — „lub połączyć z istniejącymi” → [[zdjecia-w-aplikacji]]; droga od strony zdjęcia zostaje |
| **D7 — tryb „Zdjęcie profilowe” zapisuje od razu, a kafelek dodaje kilka zdjęć i zostawia ekran** (v1.5) | zapis od razu to decyzja autora w pozycji (ISSUE-048 AC-2, „jak tło”), więc D1 ma dwa wyjątki, oba z widoku osoby: wybór tła i profilowego. W formularzu dalej „Zapisz”. Autor chce tu też „dodania dla tej osoby nowych zdjęć” — w liczbie mnogiej, więc kafelek nie kończy wyboru jak w trybie tła (tam jedno zdjęcie od razu staje się tłem): dodaje, zapisuje i zostawia siatkę, żeby nowe zdjęcie mogło zostać profilowym jednym dotknięciem | autor dodaje z portretu głównie po to, żeby zmienić profilowe → kafelek przy jednym zdjęciu od razu otwiera kadr |
| **D8 — nieudany zapis w „Zdjęciu profilowym” cofa siatkę do zapisanego stanu, także dodane zdjęcia** (v1.6; odstępstwo 2 `dev` w [[ISSUE-048-portrait-photos]], przyjęte w przeglądzie `ui` 2026-10-19) | ten tryb nie ma „Zapisz” (D7), więc zdjęcie, które zostałoby w siatce po nieudanym zapisie, wyglądałoby na zapisane, a po „wstecz” przepadłoby bez słowa (reguła 10: widać to, co zapisane). Linia błędu mówi, co zrobić. Zdjęcie z galerii albo z aplikacji wybiera się jeszcze raz, z aparatu — robi się jeszcze raz. Przypadek rzadki (zapis do bazy w telefonie) | autor po błędzie szuka dodanych zdjęć w siatce → zostają w siatce z linią „nie zapisane” i „Spróbuj jeszcze raz” |

## Open
brak. Zakres wyboru osób na zdjęciu — [[zdjecie]] D7, **przyjęte na stopie #1** (wszystkie osoby z filtrem; zaznaczenie
kolejnej osoby także później, z bazy każdej osoby już zaznaczonej na zdjęciu).
