---
screen: "Cmentarz — groby na cmentarzu"
items: ["[[ISSUE-012-transcribe-grave-screen]]"]
us: "[[US-002-przepisanie-grobu]]"
journey-step: "n/a — M1 (warunek kroku 1 UJ-001); docelowo mapa cmentarza z arkuszem grobu (R2, krok 2 UJ-001, M3)"
mockup: "katalog tymczasowy sesji 2026-10-06: makieta-przepisanie-grobu.html (ramka 4)"
updated: 2026-10-06
---

# Cmentarz — specyfikacja

> ⚠️ **Do przebudowy — decyzja autora 2026-10-06.** Cmentarz ma wyglądać jak R2: mapa z grobami
> zaznaczonymi zniczami, a po wybraniu znicza arkusz (miejsce na zdjęcie, lokalizacja, liczba osób, nazwa
> grobu, „Pokaż grób”). Do [[SPIKE-001-map-source-offline]] bez zdjęcia satelitarnego: arkusz z grobami, z
> pinezką i bez. `ui` przepisze ten plik przed planem [[ISSUE-012-transcribe-grave-screen]].

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] · referencja: [[references]] → R2 (treść karty
> grobu).

## Purpose
Groby przepisane na jednym cmentarzu i wejście do dodania kolejnego grobu z notatek. Karta grobu niesie tę
samą treść co arkusz grobu w R2: osoby, adres, liczbę osób. Widać, którym grobom brakuje adresu kwatery i
pinezki (US-002 AC-5); uzupełni się je przy wizycie. Docelowo (R2) ten ekran dostaje mapę cmentarza, a
karta staje się dolnym arkuszem.

## Navigation
- Z [[cmentarze]] (dotknięcie karty albo zaraz po dodaniu cmentarza).
- Dotknięcie karty grobu → [[grob]].
- **„Dodaj grób” → [[wpis-osoby]] w trybie „nowy grób”**: grób powstaje razem z pierwszą osobą, przy jej
  zapisie. Pustych grobów nie ma.
- Wstecz → [[cmentarze]].

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek: wstecz + **nazwa cmentarza** (półgruby, tytuł), miejscowość (podtytuł, tekst pomocniczy) | pasek | — | — | — | *What to build* 1 · R2 |
| 2 | Podsumowanie: „3 groby · 6 osób” | tekst pomocniczy | — | — | — | decyzja projektowa (postęp plastra, NT-002) |
| 3 | **Karty grobów** w kolejności wpisania. Karta: (a) **osoby w grobie** — imiona i nazwiska po przecinku (tekst, 16 sp, półgruby, najwyżej 2 linie, potem „i jeszcze 2”); (b) adres pełnymi słowami „Kwatera B · Rząd 3 · Miejsce 12” albo „Bez adresu kwatery”, i „· bez pinezki”, gdy grób nie ma pozycji (tekst pomocniczy); (c) ikona `people_outline` + „3 osoby” (tekst pomocniczy); chevron „›” | lista kart na powierzchni | dotknięcie → [[grob]] | kolejność wpisania | — | AC-1 · AC-5 · R2 |
| 4 | **„Dodaj grób”** | przycisk wypełniony (główne działanie), przypięty na dole, pełna szerokość | dotknięcie → [[wpis-osoby]] „nowy grób” | — | — | *What to build* 2 |

## States
| Stan | Co widać |
|---|---|
| pusty | „Na tym cmentarzu nie ma jeszcze grobów.” (tekst pomocniczy, środek) + „Dodaj grób” |
| błąd | „Nie udało się odczytać grobów.” + „Spróbuj ponownie” (przycisk z obrysem) |
| wypełniony | jak wyżej |
| wczytywanie | wskaźnik postępu na środku (zwykle niewidoczny) |

Grób bez wpisanych osób nie powstaje z interfejsu, ale może przyjść z innych danych. Wtedy karta pokazuje
„Grób bez wpisanych osób” w tekście pomocniczym.

## Sketch
```
┌──────────────────────────────────┐
│ ←  Cmentarz Wymyślony            │
│    Miejscowość Testowa           │
│  3 groby · 6 osób                │
│ ╭──────────────────────────────╮ │
│ │ Jan Wymyślony, Anna        › │ │
│ │ Wymyślona, Józef Wymyślony   │ │
│ │ Bez adresu kwatery · bez     │ │
│ │ pinezki                      │ │
│ │ 👥 3 osoby                   │ │
│ ╰──────────────────────────────╯ │
│ ╭──────────────────────────────╮ │
│ │ Maria Próbna               › │ │
│ │ Kwatera B · Rząd 3 ·         │ │
│ │ Miejsce 12 · bez pinezki     │ │
│ │ 👥 1 osoba                   │ │
│ ╰──────────────────────────────╯ │
│ ┌──────────────────────────────┐ │
│ │          Dodaj grób          │ │  ← wypełniony, akcent
│ └──────────────────────────────┘ │
└──────────────────────────────────┘
```

## Tempo
Na grób: **1 dotknięcie** („Dodaj grób” otwiera od razu formularz pierwszej osoby). Ok. 50 dotknięć na
całe notatki.

## Style B rules applied
- Reguła 1: jedyny wypełniony przycisk to „Dodaj grób”. W przepisywaniu to główna, powtarzana czynność
  tego ekranu.
- Reguła 2 i 11: karty na powierzchni z chevronem; bez miniatury, bo zdjęcia to US-005.
- Reguła 3: ikona osób w kolorze tekstu pomocniczego, bo opisuje, a nie działa.
- Reguła 6: adres pełnymi słowami, liczby odmienione.
- Reguła 7: „Bez adresu kwatery · bez pinezki” to fakt w tekście pomocniczym, nie ostrzeżenie.
- Reguła 9: pusty stan ma jedno działanie.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-002 AC-1 | 3 → [[grob]] | karta grobu nazwana wszystkimi osobami, z ich liczbą, a po dotknięciu pokazuje każdą |
| US-002 AC-5 | 3 (b), 4 | grób zapisany z samym cmentarzem i osobami ma kartę z „Bez adresu kwatery · bez pinezki” |
| ISSUE-012: styl B | całość | reguły wyżej; przegląd `ui` |

## Decisions
- **„Dodaj grób” otwiera od razu formularz pierwszej osoby**, a grób zapisuje się razem z nią. Grób z
  notatek to cmentarz i osoby (US-002, decyzja autora 2026-10-06), więc pusty grób nie ma po co istnieć.
  *Obali:* potrzeba zapisu grobu znanego z wizyty, którego osób jeszcze nie znam.
- **Karta grobu nazwana osobami**, a nie „Grób rodzinny X-ów” (R2): nazwa rodowa wymaga odmiany
  nazwiska ([[grob]] → *Open*). Osoby po przecinku niosą tę samą informację bez ryzyka złej odmiany.
- **Kolejność wpisania**, czyli kolejność z notatek. Ułatwia sprawdzenie, gdzie się skończyło. *Obali:*
  autor szuka grobów po nazwisku — to [[EPIC-002-wizyta]] albo wyszukiwanie (S5).

## Open
brak (nazwa grobu → [[grob]] → *Open*).
