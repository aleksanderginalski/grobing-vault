# Plany cmentarzy z kwaterami — trzecie źródło położenia grobu?

> ✅ **Rozstrzygnięte 2026-10-08 przez [[SPIKE-001-map-source-offline]] → [[ADR-003-map-source-offline]].**
> - Plany z kwaterami są w sieci dla 8 z 11 cmentarzy autora, a wyszukiwarkę grobów zarządcy ma 11 z 11. **Nie
>   wolno ich kopiować** i nie działają offline, więc **nie są źródłem położenia w aplikacji**.
> - Kwatery zaznacza autor według planu zarządcy, a pinezkę grobu stawia w kwaterze.
> - Siatkę kwater z pomysłu niżej zastępują kwatery autora.
> - Plan w aplikacji to schemat z OSM, a zdjęcie z góry jest tylko online.
>
> Wejście do pierwszej US mapy cmentarza: [[EPIC-002-wizyta]] → *Input from SPIKE-001*. Model danych i
> glosariusz są już zaktualizowane (*Sector*, *pinezka*, *plan cmentarza*). **Notatka zostaje w INBOX jako ślad,
> mimo zdania „znika z INBOX” niżej:** linkuje do niej 8 zamkniętych pozycji, a usunięcie urwałoby te odsyłacze
> (`docs`, 2026-10-08).

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

## Related idea — a cemetery database with map import (author, 2026-10-06)
Przy uwagach do makiety ([[ISSUE-012-transcribe-grave-screen]] → *Input from the author*) autor zapytał,
czy nowy cmentarz dałoby się *„znaleźć w bazie cmentarzy, żeby potem zaimportować jego mapę”*. To ta
sama rodzina pytań co plany z kwaterami: **skąd brać dane o cmentarzu (położenie, granice, mapę), zamiast
wpisywać je ręcznie.** Pytania do [[SPIKE-001-map-source-offline]]:
- czy istnieje źródło listy cmentarzy w Polsce z położeniem, którego warunki pozwalają użyć go offline
  przez jedną osobę (np. dane OpenStreetMap — licencja ODbL, do sprawdzenia, a nie z pamięci);
- czy „import mapy” cmentarza to po prostu obszar offline wybranego źródła satelitarnego, czyli
  dokładnie pytanie spike'a.

Do tego czasu [[ISSUE-014-home-map-of-poland]] dodaje cmentarz ręcznie: nazwa, miejscowość i punkt
dotknięciem na mapie.

> **2026-10-06 — baza cmentarzy wyszła z tej notatki do [[ISSUE-015-add-cemetery-from-database]]** (decyzja autora
> na stopie #1 ISSUE-014). Falsyfikator: wbudowany wyciąg OpenStreetMap (ODbL), 8 z 8 cmentarzy autora w bazie
> (ISSUE-014 → *Stop #1 — round 1*). **„Import mapy” cmentarza** (granice, zdjęcie satelitarne) i plany z
> kwaterami zostają tutaj i w [[SPIKE-001-map-source-offline]].

## Related idea — a grid of sectors to tap (author, 2026-10-07)
Na stopie #1 [[ISSUE-012-transcribe-grave-screen]] autor zapytał, czy oprócz „Dodaj grób” nie mogłaby być
**siatka kwater**: dotknięcie kwatery na planie cmentarza mówi, która to kwatera. Autor nie wiedział, jak takie plany
wyglądają, i odłożył to, jeśli to temat na osobną pozycję. Notatki nie mają adresów kwater, więc siatka pomoże na
cmentarzu, a nie przy przepisywaniu w domu. Stoi na tym samym falsyfikatorze co plany wyżej: **ile cmentarzy autora
ma plan z kwaterami** ([[SPIKE-001-map-source-offline]] krok 1). Kierunek ekranu po SPIKE-001: [[cmentarz]] → D1
(mapa nad arkuszem grobów).
