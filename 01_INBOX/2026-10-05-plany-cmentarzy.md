# Plany cmentarzy z kwaterami — trzecie źródło położenia grobu?

> Pomysł autora z sesji `pm` 2026-10-05, **bez preferencji** względem zdjęć z GPS. Decyzja odłożona do
> [[SPIKE-001-map-source-offline]], bo rozstrzygają ją dane, nie gust.

## The idea
Mieć plany cmentarzy z podziałem na kwatery, zaznaczać na nich kwatery grobów, a potem dołączać do
nich zdjęcia nagrobków.

## Where it fits
- **Model danych już to przewiduje:** `Grave` ma adres zarządcy (`sector` / `row` / `plot`) jako
  prawdę o położeniu, a pozycję zapisuje razem ze **źródłem** i dokładnością (`04_ARCHITECTURE/data-model.md`).
  Plan zarządcy byłby **trzecim źródłem** pozycji obok zdjęcia satelitarnego i GPS na miejscu. To
  rozszerzenie, które niczego nie psuje. Jeśli pomysł wejdzie, zmiana trafi do modelu danych i do
  `glossary.md` → *pinezka*.
- **To kandydat na lukę 1** (`TRACEABILITY.md` → *Open gaps* 1, grób bez pinezki). Zdjęcie z GPS
  pomaga dopiero wtedy, gdy grób jest już znaleziony. Plan razem z adresem kwatery z zarządu
  cmentarza albo z Grobonetu pozwala go znaleźć **za pierwszym razem**.
- **Zdjęcia z GPS i plany się nie wykluczają.** Zdjęcie nagrobka jest potrzebne w obu podejściach.

## Cheapest falsifier
Przy [[SPIKE-001-map-source-offline]] krok 1 policzyć, **ile z 10 cmentarzy autora ma plan z
kwaterami** (Grobonet, strona zarządcy, tablica przy bramie). W vaulcie zapisać tylko liczbę, bez nazw
cmentarzy (patrz ostrzeżenie w SPIKE-001 krok 1).

## Where it goes when answered
Wynik SPIKE-001 trafia do [[ADR-003-map-source-offline]] razem z decyzją autora o źródłach położenia.
Potem idzie do modelu danych i glosariusza, a ta notatka znika z INBOX.
