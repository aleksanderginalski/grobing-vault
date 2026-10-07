---
screen: "Grób — wszyscy pochowani"
items: ["[[ISSUE-012-transcribe-grave-screen]]"]
us: "[[US-002-przepisanie-grobu]]"
journey-step: "n/a — M1; ten sam widok stanie się widokiem 3 (krok 4 UJ-001, M4, R4 lewy) — zdjęcia (US-005) i wizyta dojdą tutaj"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-cmentarz-grob-osoba.html (ramki 5–7)"
updated: 2026-10-07
---

# Grób — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.5) · referencja: [[references]] → **R4 (lewy
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

## Purpose
Wszyscy pochowani w jednym grobie, z datami z dopiskiem (US-002 AC-1, AC-3), nazwa grobu i widoczny brak
adresu kwatery oraz pinezki (AC-5). Stąd dodaje się kolejną osobę, więc przy przepisywaniu to też
potwierdzenie, że wpis się zapisał. Układ to R4 bez zdjęć: zdjęcie nagrobka u góry i portrety w kartach dojdą
z [[US-005-zdjecia]].

## Navigation
- Z [[cmentarz]] (dotknięcie karty grobu) albo z [[wpis-osoby]] po zapisie. Formularz znika ze stosu, więc
  wstecz z grobu wraca do [[cmentarz]], nie do formularza.
- **Ikonka edycji (3) → okno „Popraw grób”** nad widokiem grobu; „Zapisz” zamyka okno, a tytuł się zmienia.
- „Dodaj osobę” → [[wpis-osoby]] w trybie „kolejna osoba”.
- Dotknięcie karty osoby → [[wpis-osoby]] w trybie „poprawa” (ISSUE-012, D1). Docelowo: widok osoby (M5, R4
  prawy).
- Wstecz → [[cmentarz]].

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** wstecz; podtytuł paska: nazwa cmentarza · miejscowość (14 sp, tekst pomocniczy, jedna linia, ucięta) | pasek | wstecz → [[cmentarz]] | — | — | decyzja projektowa |
| 2 | **Tytuł:** nazwa grobu (24 sp, półgruby, wyśrodkowany, do 2 linii). **Bez nazwy: „Grób”** w tym samym kroju | tekst | — | — | — | R4 · decyzja autora (nazwa grobu) · D1 |
| 3 | **Ikonka edycji** w linii tytułu, z prawej: `edit_outlined` w akcencie, cel 48 × 48 dp, `tooltip` „Popraw grób”. Tytuł ma z lewej taki sam odstęp, więc zostaje wyśrodkowany | przycisk-ikona | → okno „Popraw grób” (3a) | — | — | decyzja projektowa (jak [[cmentarze]] element 8) · D2 |
| 3a | **Okno „Popraw grób”:** pole **„Nazwa grobu”** (ramka w kolorze obrysu, wielka litera na początku zdania, podpowiedź „np. Grób rodzinny Nowaków” — tekst z R4), pod polem „Zostaw puste, jeśli grób nie ma nazwy.” (13 sp, tekst pomocniczy). Przyciski „Anuluj” (kolor tekstu) · **„Zapisz”** (akcent) — jak okno cmentarza w `cemetery_form.dart` | okno dialogowe | fokus i klawiatura od razu, kursor na końcu obecnej nazwy; `done` = „Zapisz” | obecna nazwa albo pusto | puste = bez nazwy (tytuł „Grób”); spacje na brzegach obcięte. Błąd zapisu: pod polem `error_outline` + „Nie udało się zapisać. Spróbuj jeszcze raz.” (kolor błędu), okno zostaje | decyzja autora (nazwa grobu) · [[style-b]] reguła 1 (okno) |
| 4 | **Adres i pinezka** pod tytułem, wyśrodkowane: adres pełnymi słowami „Kwatera B · Rząd 4 · Miejsce 12” (14 sp, tekst pomocniczy). Bez adresu: ikona `place_outlined` + „Bez adresu kwatery · bez pinezki”, a pod spodem „Uzupełnisz przy wizycie.” (tekst pomocniczy). Z adresem, bez pinezki: adres + „· bez pinezki” | tekst | — | — | — | AC-5 · R4 |
| 5 | **Karty osób** w kolejności wpisania, odstęp 8 dp. Karta: „Imiona Nazwisko z d. Rodowe” (16 sp, półgruby, zawijane); lata życia (14 sp, tekst pomocniczy): `1921–1987`, a z dopiskiem `ok. 1890 – 14.03.1951`; gdy jest data pochówku: `· poch. 18.03.1951`. Brak urodzenia: `zm. 1951`; brak zgonu: `ur. 1890`; brak dat: „bez dat”. **Chevron „›” — karta prowadzi do poprawy (D1)** | lista kart na powierzchni, karta ≥ 64 dp | dotknięcie → poprawa ([[wpis-osoby]] → *Open* 1) | kolejność wpisania | — | AC-1 · AC-2 · AC-3 · R4 |
| 6 | **Rząd działań:** „Dodaj osobę” — przycisk z obrysem, ikona `person_add_alt_outlined` w akcencie, napis w kolorze tekstu, ≥ 52 dp. Miejsce obok zostaje na „Dodaj zdjęcie” ([[US-005-zdjecia]]) | rząd przycisków pod listą | dotknięcie → [[wpis-osoby]] „kolejna osoba” | — | — | *What to build* 3 · R4 |

**Gdy źródła się spierają** (dwie daty urodzenia albo dwa groby jednej osoby), widok pokazuje **pierwszą**
wartość — najniższe `id`, jak w GEDCOM 7 ([[ADR-006-claimed-value-separate-structures]] D3; `claims.dart` →
`firstEvent`). Oznaczenie sporu to [[US-004-fakt-od-babci]]. Osoba z dwoma pochówkami pojawia się w obu
grobach (ADR-006, *Consequences*).

**Dane, których ekran potrzebuje** (dla `planning`): nowe, opcjonalne pole **nazwa grobu** w tabeli grobów —
zmiana schematu, migracja v2→v3 z testem ([[NFR-003-migracje-schematu]]) i kopia zaraz po migracji (retro 1,
R6). Zapis nazwy zamawia kopię w tle jak każdy zapis.

## States
| Stan | Co widać |
|---|---|
| wypełniony | 1–6 |
| bez nazwy | tytuł „Grób” + ikonka edycji; reszta bez zmian |
| pusty | „W tym grobie nie ma jeszcze wpisanych osób.” + „Dodaj osobę” (z interfejsu nie powstaje — patrz [[cmentarz]]) |
| okno „Popraw grób” | element 3a nad widokiem grobu |
| błąd | „Nie udało się odczytać grobu.” + „Spróbuj ponownie” (przycisk z obrysem) |
| wczytywanie | wskaźnik postępu w środku (zwykle niewidoczny) |

## Sketch
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

## Tempo
Widok do oglądania. Jako krok przepisywania:
- **1 dotknięcie** („Dodaj osobę”) na każdą osobę poza pierwszą w grobie;
- **nazwa grobu: 2 dotknięcia** (ikonka, „Zapisz”) i pisanie — tylko dla grobów, które mają nazwę. Zaraz po
  zapisie pierwszej osoby ten widok jest na ekranie, więc nazwę nadaje się bez szukania grobu.

## Style B rules applied
- **Reguła 1:** brak wypełnionego przycisku — jak w R4, treścią są osoby. „Dodaj osobę” ma obrys i ikonę w
  akcencie. W oknie „Zapisz” jest przyciskiem tekstowym w akcencie.
- **Reguły 2 i 11:** karty osób na powierzchni z chevronem; bez miniatur do US-005, bez zastępczych obrazków.
- **Reguła 3:** `place_outlined` w kolorze pomocniczym (opisuje), `person_add_alt_outlined` i `edit_outlined`
  w akcencie (działania).
- **Reguła 4:** tytuł i imiona półgrube.
- **Reguła 6:** lata życia, „z d.” w tej samej linii, adres pełnymi słowami.
- **Reguła 7:** brak adresu opisany faktem i tym, kiedy się uzupełni; „Zostaw puste, jeśli grób nie ma
  nazwy.” zamiast oznaczenia pola jako opcjonalnego.
- **Reguła 10:** zapis z [[wpis-osoby]] kończy się tym widokiem, bez okienka „Zapisano”; zapis nazwy kończy
  się nowym tytułem.
- **Tokeny:** bez nowych.
- **Uwaga na ekrany wizyty:** lata i adres są tu w tekście pomocniczym (5,50:1 na tle). Gdy ten widok stanie
  się widokiem wizyty (M4), a [[NFR-004-czytelnosc-w-sloncu]] przyjmie 7:1, te linie przejdą na kolor tekstu
  ([[style-b]] → *Measurement*).

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-002 AC-1 | 5 | każda osoba wpisana do grobu ma kartę |
| US-002 AC-2 | 5 | imiona, nazwisko i osobno „z d. Rodowe”; „kim była” — patrz D3 |
| US-002 AC-3 | 5 (lata życia, data pochówku) | każdy z pięciu dopisków widać w zapisie: „1890”, „ok. 1890”, „przed 1920”, „po 1945”, „między 1893 a 1895” |
| US-002 AC-5 | 4 | grób bez adresu i pinezki zapisany i widoczny z „Bez adresu kwatery · bez pinezki” |
| decyzja autora 2026-10-06: grób jak R4 z nazwą grobu | 2, 3, 3a | ikonka → „Grób rodzinny Wymyślonych” → „Zapisz” → tytuł widoku i tytuł karty w [[cmentarz]] |
| ISSUE-012: styl B | całość | reguły wyżej; przegląd `ui` przed stopem #2 |

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
- **D5 — kolejność wpisania**, nie chronologiczna: zgadza się z notatkami, więc łatwo porównać. *Obali:* autor
  na stopie #2 chce widzieć najpierw najstarszych.
- **D6 — daty z dokładnością taką, jak wpisano** (`ok. 1890 – 14.03.1951`), a nie same lata jak w R4: dopisek i
  dokładność to dana (FR-004), a nie szum. Same lata zostają, gdy wpisano same lata.
- **D7 — spór źródeł niewidoczny** — pokazuje się pierwsza wartość; oznaczenie to US-004.

## Open
brak. Poprawa wpisu rozstrzygnięta na stopie #1 ISSUE-012 (D1 — wchodzi).
