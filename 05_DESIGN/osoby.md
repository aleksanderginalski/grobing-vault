---
screen: "Osoby — zakładka: wszystkie osoby i wyszukiwanie"
items: ["[[SPIKE-004-mvp-flow-prototype]]"]
us: "do rozpisania — S5/G5 (wyszukiwanie osób; brief §5a G5 — Should, przyjęte do MVP decyzją autora na prototypie: SPIKE-004 D1, D3, D19)"
journey-step: "n/a — wejście do widoku osoby (M5) spoza ścieżki wizyty"
mockup: "2026-10-08: grobing-prototyp.html (SPIKE-004, panel 5) — katalog tymczasowy sesji, ścieżka w SPIKE-004"
updated: 2026-10-08
---

# Osoby — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.16) · referencja: [[references]] → **R1** (zakładka „Osoby”).
>
> **Wersja 1 — discovery na prototypie, panel 5 ([[SPIKE-004-mvp-flow-prototype]] D19, 2026-10-08).** Autor: *„tak jest
> dobrze, przy czym jeszcze chciałbym mieć ścieżkę (Osoby -> Wybrana osoba -> (w przypadku jeżeli zmarła) Miejsce
> pochówku -> I jestem kierowany na widok Cmentarza z zaznaczoną pinezką)”*. Ścieżkę niesie [[osoba]] element 9.
> **Zakres:** wyszukiwanie osób było w briefie w Should (G5). Zakładka Osoby z R1 i decyzje D1, D3 SPIKE-004 przenoszą je
> do MVP — to decyzja autora na prototypie, zapisana jako zmiana zakresu.

## Purpose
Znaleźć osobę bez wiedzy, na którym cmentarzu leży: po nazwisku albo imieniu, a w liście — zobaczyć, kim jest dla
autora. Stąd idzie do widoku osoby ([[osoba]]), a z niego do pochówku na mapie cmentarza (D19).

## Navigation
- **Zakładka „Osoby”** w dolnym pasku ([[style-b]] reguła 12). Wyszukiwarka tej zakładki szuka tylko osób (SPIKE-004 D3).
- **Karta osoby → [[osoba]]** — zakładka Osoby zostaje aktywna na całym stosie: osoba → mapa cmentarza → grób.
- Wstecz z widoku osoby wraca tu, z tym samym tekstem w wyszukiwarce i tą samą pozycją listy.

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** „Osoby” (20 sp, półgruby) i po prawej liczba „34 osoby” (14 sp, tekst pomocniczy, odmiana) | pasek | — | — | — | R1 · [[style-b]] reguła 6 |
| 2 | **Wyszukiwarka** — pigułka jak na mapie ([[cmentarze]] element 2), podpowiedź „Szukaj osoby”. Dopasowanie bez polskich znaków i wielkości liter, od początku słowa imienia albo nazwiska (także nazwiska rodowego) | pole tekstowe | wielka litera wyłączona; `search` = zamknij klawiaturę | pusto | — | D3 (SPIKE-004) · jak [[cmentarze]] D3 |
| 3 | **„Ja”** — pierwsza karta, z obrysem: inicjały „Ja” w akcencie, „Ja” i „to Ty — od Ciebie liczą się łańcuchy”. Przy wpisanym tekście znika | karta | → [[osoba]] dla „ja” | — | — | M5 · [[data-model]] (ustawienie „ja”) |
| 4 | **Lista osób A–Z po nazwisku**, z nagłówkami liter (13 sp, tekst pomocniczy). Karta (reguła 11): profilowe 40 dp albo inicjały, „Imiona Nazwisko z d. Rodowe” (16 sp, półgruby), pod spodem lata życia i **kim osoba jest dla autora** („1925–2004 · babcia”, „ur. 1955 · ciotka (siostra taty)”) — 14 sp, tekst pomocniczy; chevron. Polskie sortowanie | lista kart | karta → [[osoba]] | po nazwisku, potem po imieniu | — | **decyzja autora** (D19) · [[osoba]] D4 (nazwy pokrewieństwa) |
| 5 | **Brak wyników:** „Nie ma osoby „<tekst>”.” (tekst pomocniczy) | tekst | — | — | — | [[style-b]] reguła 9 |

## States
| Stan | Co widać |
|---|---|
| pełny | 1–4 |
| szukanie | 1, 2, wyniki 4 bez nagłówków liter i bez „Ja” |
| brak wyników | 1, 2, 5 |
| pusta baza | 1, 2, „Tu pojawią się osoby z grobów i rodzin.” (reguła 9) |
| wczytywanie | wskaźnik postępu (lokalna baza — zwykle niewidoczny) |

## Sketch
```
┌──────────────────────────────────┐
│ Osoby                  34 osoby  │
│ ( 🔍  Szukaj osoby             ) │
│ ╭──────────────────────────────╮ │
│ │ (Ja) Ja                     ›│ │  ← obrys, „to Ty”
│ │      to Ty — od Ciebie liczą…│ │
│ ╰──────────────────────────────╯ │
│ P                                │
│ ╭──────────────────────────────╮ │
│ │ (◉) Alicja Przykładowa      ›│ │
│ │     1926–2010 · babcia       │ │
│ ╰──────────────────────────────╯ │
│ ╭──────────────────────────────╮ │
│ │ (EP) Ewa Przykładowa        ›│ │
│ │     ur. 1955 · ciotka (sios… │ │
│ ╰──────────────────────────────╯ │
│  Mapa      Osoby      Drzewo     │
└──────────────────────────────────┘
```

## Tempo
n/a — ekran do szukania i oglądania.

## Style B rules applied
- **Reguła 11:** karty z chevronem; profilowe — okrąg (reguła 14); bez zdjęcia — inicjały na powierzchni z obrysem
  (nie zastępczy obrazek — tekst).
- **Reguła 12:** zakładka Osoby aktywna; **każda zakładka szuka swojego**.
- **Reguła 6:** lata życia, „z d.”, odmiana liczby osób.
- **Tokeny:** bez nowych.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| SPIKE-004 D19 — Osoby → osoba → pochówek → mapa z pinezką | 4 → [[osoba]] 9 → [[cmentarz]] | „Maria” → „Pochówek” → mapa Wymyślonowa z zaznaczonym zniczem jej grobu |
| G5 — znaleźć osobę po nazwisku wśród ok. 100 | 2, 4 | „wymys” → osoby o nazwisku Wymyślony/Wymyślona |

## Decisions
- **D1 — sortowanie po nazwisku z literami** (D19: *„tak jest dobrze”*). Nazwisko grupuje rodziny. *Obali:* autor szuka
  częściej po pokoleniu albo bliskości — wtedy przełącznik sortowania.
- **D2 — pokrewieństwo w liście** zamiast miejsca pochówku: lista odpowiada na „kto to dla mnie”, a „gdzie leży” jest w
  widoku osoby. *Obali:* autor przed wizytą szuka po cmentarzu — wtedy filtr „na tym cmentarzu”.
- **D3 — „Ja” na górze** — kotwica łańcuchów; tu autor ją widzi i poprawia (ustawienie w [[ustawienia]]).

## Open
brak.
