---
screen: "Zdjęcia osoby — baza zdjęć jednej osoby"
items: ["[[ISSUE-017-person-photos]]"]
us: "[[US-005-zdjecia]]"
journey-step: "n/a — M1 (przepisywanie i zbieranie u babci); docelowo część widoku osoby (M5, R4 prawy)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-zdjecia-osoby.html (ramki 1–9)"
updated: 2026-10-07
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
  Docelowo także z widoku osoby (M5), ale tego widoku jeszcze nie ma.
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
| 2 | **Profilowe** — nagłówek wyśrodkowany: okrąg **96 dp** z profilowym (pierwsze łącze), przycięty ze środka; pod nim „Profilowe” (13 sp, tekst pomocniczy); odstęp 24 dp od paska i 24 dp do siatki. Opis dla czytnika: „Zdjęcie profilowe — otwórz” | obraz-przycisk (cel 96 dp) | dotknięcie → [[zdjecie]] B na tym zdjęciu | pierwsze zdjęcie osoby | — | ISSUE-017 AC 4 · R4 prawy · D2 |
| 3 | **Nagłówek sekcji:** „Wszystkie zdjęcia · 3” — ikona `photo_library_outlined` w akcencie (reguła 3: nagłówek sekcji), tekst 14 sp półgruby w kolorze tekstu; sama liczba po kropce, bez rzeczownika, więc bez odmiany | tekst | — | — | — | decyzja projektowa · R4 (nagłówki sekcji z ikoną) |
| 4 | **Siatka zdjęć** — 3 kolumny, kwadraty z zaokrągleniem 8 dp, odstęp 8 dp, marginesy 16 dp; zdjęcie przycięte ze środka. **Kolejność łączy:** profilowe pierwsze, dalej w kolejności dodania. Nic na zdjęciach (reguła 14) — profilowe w siatce nie ma znacznika, bo pokazuje je element 2. Opis każdej komórki dla czytnika: „Zdjęcie 2 z 3 — otwórz”, a przy pierwszym „Zdjęcie 1 z 3, profilowe — otwórz” | siatka obrazów-przycisków (komórka ok. 104 dp przy 360 dp szerokości, ok. 121 dp przy 411) | dotknięcie → [[zdjecie]] B na tym zdjęciu | — | — | ISSUE-017 AC 4 · US-005 AC-1 · D3 · [[style-b]] reguła 14 (v1.9) |
| 5 | **Kafelek „Dodaj zdjęcie”** — ostatnia komórka siatki, tej samej wielkości: obrys 1 dp w kolorze obrysu na tle (bez wypełnienia), zaokrąglenie 8 dp, w środku `add_a_photo_outlined` (28 dp, akcent) i pod nią „Dodaj zdjęcie” (14 sp, półgruby 500, kolor tekstu, do 2 linii). Opis dla czytnika „Dodaj zdjęcie osoby” | przycisk | → [[zdjecie]] A (galeria — kilka zdjęć, aparat — jedno) | — | — | US-005 AC-1 · D4 · D5 · [[grob]] D12 (działanie tam, gdzie pojawi się wynik) |
| 6 | **Linia zapisu** pod siatką: „Zmiany zdjęć zapiszą się razem z wpisem osoby.” (13 sp, tekst pomocniczy) — tylko gdy na tym ekranie albo w podglądzie coś zmieniono, a wpis nie jest jeszcze zapisany | tekst | — | ukryta | — | D1 · [[style-b]] reguła 7 |

**Dane, których ekran potrzebuje** (dla `planning`):
- zdjęcia osoby w kolejności łączy, czyli zapisane łącza plus zmiany z tej edycji formularza;
- profilowe, czyli pierwsze łącze;
- liczba zdjęć;
- plik każdego zdjęcia: z magazynu aplikacji albo, gdy zdjęcie jest dopiero wybrane, przygotowany plik z katalogu
  roboczego ([[ADR-008-photos-access-copy-and-backup-consistency]]: plik powstaje przed wierszem).

Miniatury dekodowane w rozmiarze komórki, jak w [[grob]].

## States
| Stan | Co widać |
|---|---|
| wypełniony | 1–5; 6, gdy są niezapisane zmiany |
| jedno zdjęcie | nagłówek 2 i siatka z jednym zdjęciem i kafelkiem „Dodaj zdjęcie” |
| przygotowanie zdjęć | po powrocie z galerii albo aparatu: w miejscu każdego nowego zdjęcia komórka na powierzchni (zaokrąglenie 8 dp) ze wskaźnikiem postępu w środku; kafelek 5 nieaktywny. Zmniejszanie trwa chwilę na zdjęcie (ADR-008: 2048 px, JPEG 85). Nowe zdjęcia pojawiają się po kolei |
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
| ISSUE-017: migracja v3→v4, kopia v3 w v4, kopia zaraz po migracji | n/a — bez elementu ekranu | warstwa danych; sprawdza `qa`. Na ekranie: osoba ze zdjęciem z v3 ma po migracji to zdjęcie jako profilowe i jedyne w bazie |

## Decisions
| Decyzja | Dlaczego | Obali |
|---|---|---|
| **D1 — zmiany zdjęć zapisują się z „Zapisz” formularza**, nie od razu | „Zapis jest całością” ([[wpis-osoby]] v2, D-zdjęcie-2): osoba i jej zdjęcia powstają razem albo wcale, a „Odrzuć” cofa wszystko. Ten sam przepływ działa przy **nowej osobie**, której jeszcze nie ma w bazie. Inaczej niż przy nagrobku, który zapisuje się od razu, bo widok grobu nie ma formularza ([[grob]] → *Navigation*). Koszt: zmiana samych zdjęć istniejącej osoby to +1 dotknięcie („Zapisz”) | na stopie #2 autor czuje dwie zasady (nagrobek od razu, osoba z „Zapisz”) albo gubi zmiany → zapis od razu, a w nowej osobie zdjęcia dopiero po pierwszym zapisie |
| **D2 — profilowe w nagłówku jako okrąg** | autor widzi, jak profilowe wypadnie w okręgu karty i formularza (przycięte ze środka), zanim je ustawi. To ten sam portret co w R4 prawym, więc nagłówek przejdzie do widoku osoby (M5) | — |
| **D3 — siatka kwadratów, kolejność łączy** | zdjęcia osoby bywają grupowe, więc kwadrat ucina mniej niż okrąg. Całość jest o jedno dotknięcie dalej, w podglądzie. Kolejność łączy (profilowe pierwsze, dalej według dodania) to porządek GEDCOM. **Bez przestawiania** zdjęć poza profilowym, bo dziś kolejność niczego poza profilowym nie zmienia | autor chce porządkować zdjęcia (np. według lat) → przestawianie albo data zdjęcia, osobna pozycja |
| **D4 — kilka zdjęć naraz z galerii** | okno systemowe i tak wymaga „Gotowe” ([[zdjecie]] D2), więc wybór kilku nic nie kosztuje, a zdjęcia jednej osoby (np. z jednego albumu) przychodzą seriami. Obiecane w [[zdjecie]] D2 | — |
| **D5 — „Dodaj zdjęcie” jako ostatnia komórka siatki** | działanie stoi tam, gdzie pojawi się wynik, jak „Dodaj zdjęcie nagrobka” ([[grob]] D12, decyzja autora) | osoby mają po kilkanaście zdjęć i kafelek ucieka za ekran → rząd działań nad siatką |
| **D6 — dzielenie od strony zdjęcia** („Kto jest na zdjęciu?”, [[zdjecie]] D), a nie przez wybór „zdjęcia innej osoby” przy dodawaniu | zdjęcie grupowe zaznacza się raz, w jednym miejscu, i widać od razu wszystkich na nim. Druga droga (wybór spośród zdjęć w aplikacji) dawałaby to samo dwa razy. Dodanie zdjęcia jednej osoby kosztuje +0 | autor częściej szuka „tego zdjęcia ślubnego, które już jest u żony” niż otwiera zdjęcie → trzecia pozycja w arkuszu źródła: „Ze zdjęć w aplikacji” |

## Open
brak. Zakres wyboru osób na zdjęciu — [[zdjecie]] D7, **przyjęte na stopie #1** (wszystkie osoby z filtrem; zaznaczenie
kolejnej osoby także później, z bazy każdej osoby już zaznaczonej na zdjęciu).
