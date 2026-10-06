---
screen: "Grób — wszyscy pochowani"
items: ["[[ISSUE-012-transcribe-grave-screen]]"]
us: "[[US-002-przepisanie-grobu]]"
journey-step: "n/a — M1; ten sam widok stanie się widokiem 3 (krok 4 UJ-001, M4, R4 lewy) — zdjęcia (US-005) i wizyta dojdą tutaj"
mockup: "katalog tymczasowy sesji 2026-10-06: makieta-przepisanie-grobu.html (ramka 7)"
updated: 2026-10-06
---

# Grób — specyfikacja

> ⚠️ **Do uzupełnienia — decyzja autora 2026-10-06.** Kierunek zgodny z R4. Dojdą: **nazwa grobu**
> (autor chce jej — *Open* 1 rozstrzygnięte w stronę pola w schemacie, w [[ISSUE-012-transcribe-grave-screen]]),
> zdjęcie grobu i portrety ([[US-005-zdjecia]]) oraz wejście w szczegóły osoby. `ui` uzupełni ten plik
> przed planem ISSUE-012.

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] · referencja: [[references]] → R4 (lewy ekran).

## Purpose
Wszyscy pochowani w jednym grobie, z datami z dopiskiem (US-002 AC-1, AC-3), i widoczny brak adresu
kwatery oraz pinezki (AC-5). Stąd dodaje się kolejną osobę, więc przy przepisywaniu to też potwierdzenie,
że wpis się zapisał. Układ to R4 bez zdjęć: zdjęcie nagrobka u góry i portrety w kartach dojdą z
[[US-005-zdjecia]].

## Navigation
- Z [[cmentarz]] (dotknięcie karty grobu) albo z [[wpis-osoby]] po zapisie. Formularz znika ze stosu, więc
  wstecz z grobu wraca do [[cmentarz]], nie do formularza.
- „Dodaj osobę” → [[wpis-osoby]] w trybie „kolejna osoba”.
- Dotknięcie karty osoby → [[wpis-osoby]] w trybie „poprawa” — **tylko jeśli poprawa wejdzie do
  ISSUE-012** ([[wpis-osoby]] → *Open* 1). Docelowo: widok osoby (M5, R4 prawy).
- Wstecz → [[cmentarz]].

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek: wstecz; podtytuł paska: nazwa cmentarza · miejscowość (tekst pomocniczy) | pasek | — | — | — | decyzja projektowa |
| 2 | **Tytuł:** „Grób” (półgruby, 24 sp, wyśrodkowany) — patrz *Open* 1 | tekst | — | — | — | R4 · decyzja projektowa |
| 3 | **Adres i pinezka** pod tytułem, wyśrodkowane: adres pełnymi słowami „Kwatera B · Rząd 4 · Miejsce 12” (tekst pomocniczy); bez adresu: ikona `place_outlined` + „Bez adresu kwatery · bez pinezki”, a pod spodem „Uzupełnisz przy wizycie.” (tekst pomocniczy) | tekst | — | — | — | AC-5 · R4 |
| 4 | **Karty osób** w kolejności wpisania. Karta: „Imiona Nazwisko z d. Rodowe” (tekst, 16 sp, półgruby, jedna linia, zawijana); lata życia (tekst pomocniczy): `1921–1987`, a z dopiskiem `ok. 1890 – 14.03.1951`; gdy jest data pochówku: `· poch. 18.03.1951`. Brak urodzenia: `zm. 1951`; brak zgonu: `ur. 1890`; brak dat: „bez dat”. Chevron „›”, jeśli karta prowadzi do poprawy | lista kart na powierzchni, karta ≥ 64 dp | dotknięcie → poprawa (*Open* 1 w [[wpis-osoby]]) | kolejność wpisania | — | AC-1 · AC-2 · AC-3 · R4 |
| 5 | **Rząd działań:** „Dodaj osobę” — przycisk z obrysem, ikona `person_add_alt_outlined` w akcencie, napis w kolorze tekstu. Miejsce obok zostaje na „Dodaj zdjęcie” ([[US-005-zdjecia]]) | rząd przycisków na dole | dotknięcie → [[wpis-osoby]] | — | — | *What to build* 3 · R4 |

**Gdy źródła się spierają** (dwie daty urodzenia albo dwa groby jednej osoby), widok pokazuje **pierwszą**
wartość — najniższe `id`, jak w GEDCOM 7 ([[ADR-006-claimed-value-separate-structures]] D3). Oznaczenie
sporu to [[US-004-fakt-od-babci]]. Osoba z dwoma pochówkami pojawia się w obu grobach (ADR-006,
*Consequences*).

## States
| Stan | Co widać |
|---|---|
| pusty | „W tym grobie nie ma jeszcze wpisanych osób.” + „Dodaj osobę” (z interfejsu nie powstaje — patrz [[cmentarz]]) |
| błąd | „Nie udało się odczytać grobu.” + „Spróbuj ponownie” (przycisk z obrysem) |
| wypełniony | jak wyżej |
| wczytywanie | wskaźnik postępu na środku (zwykle niewidoczny) |

## Sketch
```
┌──────────────────────────────────┐
│ ←  Cmentarz Wymyślony · Miejsco… │
│                                  │
│               Grób               │
│   ⌖ Bez adresu kwatery · bez     │
│     pinezki                      │
│     Uzupełnisz przy wizycie.     │
│ ╭──────────────────────────────╮ │
│ │ Jan Wymyślony              › │ │
│ │ ok. 1890 – 14.03.1951 ·      │ │
│ │ poch. 18.03.1951             │ │
│ ╰──────────────────────────────╯ │
│ ╭──────────────────────────────╮ │
│ │ Anna Wymyślona z d. Zmyślona›│ │
│ │ między 1893 a 1895 – przed   │ │
│ │ 1960                         │ │
│ ╰──────────────────────────────╯ │
│ ╭──────────────────────────────╮ │
│ │ Józef Wymyślony            › │ │
│ │ po 1920 – 1944               │ │
│ ╰──────────────────────────────╯ │
│ ╭─────────────────╮              │
│ │ 👤+ Dodaj osobę  │              │  ← obrys, ikona w akcencie
│ ╰─────────────────╯              │
└──────────────────────────────────┘
```

## Tempo
n/a — widok do oglądania. Jako krok przepisywania: **1 dotknięcie** („Dodaj osobę”) na każdą osobę poza
pierwszą.

## Style B rules applied
- Reguła 1: brak wypełnionego przycisku. Jak w R4, działania w tym widoku są drugorzędne, a treścią są
  osoby. „Dodaj osobę” ma obrys i ikonę w akcencie.
- Reguła 2 i 11: karty osób na powierzchni z chevronem; bez miniatur do US-005.
- Reguła 3: `place_outlined` w kolorze pomocniczym (opisuje), `person_add_alt_outlined` w akcencie
  (działanie).
- Reguła 4: tytuł i imiona półgrube.
- Reguła 6: lata życia, „z d.” w tej samej linii, adres pełnymi słowami.
- Reguła 7: brak adresu opisany faktem i tym, kiedy się uzupełni.
- Reguła 10: zapis z [[wpis-osoby]] kończy się tym widokiem, bez okienka „Zapisano”.
- **Uwaga na ekrany wizyty:** lata i adres są tu w tekście pomocniczym (5,50:1). Gdy ten widok stanie się
  widokiem wizyty (M4), a [[NFR-004-czytelnosc-w-sloncu]] przyjmie 7:1, te linie przejdą na kolor tekstu
  ([[style-b]] → *Measurement*).

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-002 AC-1 | 4 | każda osoba wpisana do grobu ma kartę |
| US-002 AC-2 | 4 | imiona, nazwisko i osobno „z d. Rodowe”; „kim była” — patrz *Decisions* |
| US-002 AC-3 | 4 (lata życia, data pochówku) | każdy z pięciu dopisków widać w zapisie: „1890”, „ok. 1890”, „przed 1920”, „po 1945”, „między 1893 a 1895” |
| US-002 AC-5 | 3 | grób bez adresu i pinezki zapisany i widoczny z „Bez adresu kwatery · bez pinezki” |
| ISSUE-012: styl B | całość | reguły wyżej; przegląd `ui` |

## Decisions
- **Kolejność wpisania**, nie chronologiczna: zgadza się z notatkami, więc łatwo porównać. *Obali:* autor
  na stopie #2 chce widzieć najpierw najstarszych.
- **Daty z dokładnością taką, jak wpisano** (`ok. 1890 – 14.03.1951`), a nie same lata jak w R4: dopisek i
  dokładność to dana (FR-004), a nie szum. Same lata zostają, gdy wpisano same lata.
- **„Kim była” nie stoi w karcie.** Lista ma być spokojna, a „kim była” to treść widoku osoby (R4 prawy,
  M5). **Wyjątek:** jeśli poprawa nie wejdzie do ISSUE-012 ([[wpis-osoby]] → *Open* 1), „kim była” nie
  byłoby nigdzie widać. Wtedy karta dostaje trzecią linię: pierwsza linijka „kim była”, w tekście
  pomocniczym, ucięta.
- **Spór źródeł niewidoczny** — pokazuje się pierwsza wartość; oznaczenie to US-004.

## Open
1. **Nazwa grobu** („Grób rodzinny Nowaków”, R2 i R4) — do decyzji przy widoku grobu dla wizyty (M4), nie
   blokuje ISSUE-012. Opcje:
   - (a) wyliczać z nazwisk pochowanych. Wymaga poprawnej odmiany w dopełniaczu liczby mnogiej (Nowak →
     Nowaków, Kowalski → Kowalskich, Wymyślony → Wymyślonych), a błąd odmiany na grobie rodziny razi;
   - (b) opcjonalne pole „nazwa grobu” w schemacie (migracja);
   - (c) zostać przy „Grób” i osobach.
   
   **Rekomendacja `ui`: (c) teraz, (b) przy M4**, jeśli autor chce nazw jak w R4. Nazwę wpisaną ręcznie da
   się sprawdzić, a wyliczonej nie.

Poprawa wpisu → [[wpis-osoby]] → *Open* 1.
