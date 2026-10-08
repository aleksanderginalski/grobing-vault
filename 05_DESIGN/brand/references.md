---
title: "Style B — visual references from the kick-off (prompts + what each image shows)"
type: design-references
status: active
owner: ui
source: "kick-off 2026-10-05 (PROJECT_BRIEF §6a: four image-generation prompts, Style B chosen by the author) · prompts and images re-supplied by the author 2026-10-06"
created: 2026-10-06
updated: 2026-10-08
---

# Styl B — referencje wizualne z kick-offu

> **Kanon wyglądu Grobing.** Brief zapisał styl B jednym zdaniem (§6a), a ten plik trzyma to, z czego to
> zdanie wybrano: cztery prompty i opis obrazów, które autor wybrał. [[style-b]] tłumaczy je na reguły i
> progi, a specyfikacje ekranów w `05_DESIGN/` muszą do nich prowadzić.
>
> **Obrazy nie leżą w vaulcie.** Strażnik danych rodziny blokuje `*.png` w trzech repo, a repo będą
> publiczne. Miejsce obrazów: *Where the images are* niżej.
>
> **Redakcja:** w promptach nazwa miejscowości jest zastąpiona `[miejscowość]`, bo to mogła być
> prawdziwa lokalizacja grobów rodziny (`family-data.md`). Nazwiska Nowak i Kowalska zostały: to
> najczęstsze polskie nazwiska, użyte jako przykład. Wszystkie osoby na obrazach wygenerowano, nikt nie
> jest prawdziwy.

## Shared style line (every prompt)
> *Style: modern, minimal, dark mode — near-black background, soft grey text, one accent colour: warm amber
> like candlelight. Thin line icons, clean sans-serif type, subtle depth, calm and dignified, nothing
> gloomy.*

## R1 — Mapa Polski (widok 1, M2)
**Prompt:**
> High-fidelity mobile app UI mockup. One smartphone screen, portrait, front view, phone floating on a plain
> light background, no hands, no extra props.
> App name in the top bar: "Grobing". Below it a search field: "Szukaj osoby lub cmentarza".
> Main area: a muted, light-coloured map of Poland (country outline, a few major cities, rivers subtle). 10
> small amber map pins mark cemeteries where family members are buried, spread across southern and central
> Poland.
> One pin is selected; a rounded card slides up from the bottom showing:
> - "Cmentarz parafialny w [miejscowość]"
> - "6 grobów · 14 osób"
> - a primary button "Otwórz cmentarz"
> Bottom navigation bar with 3 tabs and icons: "Mapa" (active), "Osoby", "Drzewo".

**Co pokazuje obraz:**
- pasek: **ikona znicza w bursztynie + „Grobing”** (półgruby krój), koło zębate po prawej;
- wyszukiwarka w kształcie pigułki na powierzchni, z ikoną lupy;
- ciemna mapa i bursztynowe pinezki z **ikoną znicza** w środku; wybrana pinezka większa, z poświatą;
- dolny arkusz (zaokrąglona karta na powierzchni): miniatura zdjęcia cmentarza, nazwa (półgruba), „6 grobów
  · 14 osób” (szary), **wypełniony bursztynowy przycisk z ikoną znicza** „Otwórz cmentarz” — zaokrąglony
  prostokąt z delikatną poświatą;
- dolna nawigacja: trzy zakładki z cienkimi ikonami; aktywna (Mapa) ma ikonę, podpis i podkreślenie w
  bursztynie.

## R2 — Mapa cmentarza (widok 2, M3 · M6 · M7)
**Prompt:**
> High-fidelity mobile app UI mockup. One smartphone screen, portrait, front view, plain light background,
> no hands.
> Header: back arrow and title "Cmentarz parafialny w [miejscowość]", with a small green badge on the right:
> "Offline ✓".
> Main area: a top-down satellite view of a small Polish village cemetery — rows of granite graves, gravel
> paths, a few tree canopies, a small chapel at the edge. 6 amber pins sit on individual graves. A blue
> pulsing dot shows "you are here" a few metres from one pin.
> Bottom sheet for the selected grave:
> - small thumbnail photo of a gravestone
> - title "Grób rodzinny Nowaków"
> - line "Kwatera B · Rząd 4 · Miejsce 12"
> - line "3 osoby"
> - primary button "Pokaż grób" and a small secondary text link "Grobonet ↗"
> A small floating round button above the sheet with a pin icon and label "Popraw pinezkę".

**Co pokazuje obraz:**
- **zielona plakietka „Offline ✓”** (kolor stanu) i **niebieska kropka „tu jesteś”** (konwencja map);
- pinezki ze zniczem na zdjęciu satelitarnym;
- przycisk „Popraw pinezkę” w kształcie pigułki na powierzchni, z bursztynową ikoną pinezki;
- okrągły przycisk lokalizacji na powierzchni;
- arkusz: miniatura nagrobka, tytuł „Grób rodzinny Nowaków”, adres pełnymi słowami, „3 osoby” z ikoną
  osób, wypełniony przycisk ze zniczem „Pokaż grób” i bursztynowy, podkreślony link „Grobonet ↗”.
- *Uwaga:* tytuł w pasku wyszedł krojem szeryfowym. To przypadek generatora, nie wybór: brief mówi
  „sans-serif”.

## R3 — Drzewo, ścieżka, suwak czasu (widok 5, M9–M11)
**Prompt:**
> High-fidelity mobile app UI mockup. One smartphone screen, portrait, front view, plain light background,
> no hands.
> Top: a segmented toggle "Drzewo | Połącz dwie osoby" with "Połącz dwie osoby" active.
> Main area: a family tree of about 15 people shown as small round portrait nodes with first names under
> them. Married couples are joined by a short horizontal line, children hang below them. One side of the tree
> (the in-law family) has a slightly different tint.
> An amber highlighted path runs through the tree connecting two nodes labelled "Ja" and "Józef". Above the
> tree a compact card spells the path out:
> "Ja → żona Kasia → jej tata Marek → jego siostra Ewa → jej mąż Józef"
> Bottom: a horizontal time slider with year labels "1880" on the left and "2025" on the right, the handle set
> at "1950". People not yet born by 1950 appear faded; people who had died by 1950 show a tiny candle icon on
> their node.

**Co pokazuje obraz:**
- przełącznik segmentowy: aktywny segment z bursztynowym obrysem i ikoną;
- karta ścieżki: **imiona w bursztynie**, relacje w szarym;
- węzły: okrągłe portrety w sepii; na ścieżce bursztynowy pierścień z poświatą, a osoby nieurodzone
  przygaszone;
- **mały znicz na węźle osoby zmarłej**;
- rodzina żony ma lekko cieplejsze tło;
- suwak czasu: bursztynowa część wypełniona, rok w okienku nad uchwytem.

## R4 — Grób i osoba (widoki 3 i 4, M4 · M5)
**Prompt:**
> High-fidelity mobile app UI mockup. Two smartphone screens side by side, portrait, front view, plain light
> background, no hands.
> LEFT screen — a family grave:
> - large photo at the top: a grey granite family gravestone with candles (znicze) in front of it
> - title "Grób rodzinny Nowaków", line below: "Kwatera B · Rząd 4 · Miejsce 12"
> - a list of 3 people as cards, each with a small old sepia portrait photo:
>   "Jan Nowak · 1921–1987"
>   "Maria Nowak z d. Kowalska · 1925–2004"
>   "Stanisław Nowak · 1950–1951"
> - small action row at the bottom: "Dodaj zdjęcie", "Dodaj osobę"
> RIGHT screen — one person:
> - round sepia portrait at the top, name "Maria Nowak z d. Kowalska", line "1925–2004"
> - a short 2-line bio: "Nauczycielka w [miejscowość]. Matka trojga dzieci."
> - section "Rodzina" with small chips: "Mąż: Jan", "Córka: Anna", "Syn: Stanisław"
> - section "Jak łączy się ze mną": a short vertical chain of 3 small round avatars joined by an amber line,
>   labelled "Ja", "Mama Anna", "Babcia Maria"

**Co pokazuje obraz:**
- **grób:**
  - duże zdjęcie nagrobka u góry (treść użytkownika: krzyż i znicze są na zdjęciu, nie w interfejsie);
  - tytuł półgruby wyśrodkowany, adres pełnymi słowami w szarym;
  - **osoby jako zaokrąglone karty** na powierzchni: miniatura portretu, imię i nazwisko z „z d.” w jednej
    linii, „1921–1987” w szarym, chevron „›”;
  - **rząd działań: dwa przyciski z obrysem i bursztynową ikoną** („Dodaj zdjęcie”, „Dodaj osobę”);
- **osoba:**
  - okrągły portret z bursztynowym pierścieniem i delikatnymi **gałązkami** w tle;
  - imię wyśrodkowane, półgrube; lata w szarym; „kim była” w dwóch liniach wyśrodkowanych;
  - sekcje z **bursztynową ikoną w nagłówku** („Rodzina”, „Jak łączy się ze mną”);
  - chipy relacji z bursztynową ikoną osoby;
  - łańcuch awatarów połączonych bursztynową linią.

## Target app structure (from R1–R4)
- **Ekran główny = mapa Polski** (R1) z wyszukiwarką (S5) i kołem zębatym (ustawienia, w tym „Stan
  danych”).
- **Dolna nawigacja: Mapa · Osoby · Drzewo.** Pojawia się, gdy istnieją co najmniej dwa z tych celów.
  Potwierdzone na prototypie ([[SPIKE-004-mvp-flow-prototype]] D1–D3, autor 2026-10-08): pasek na ekranach do
  oglądania, ukryty w formularzach i na zdjęciu na pełnym ekranie; **wyszukiwarka na mapie szuka tylko cmentarzy**
  (odstępstwo od R1 „Szukaj osoby lub cmentarza”), a osoby szuka zakładka Osoby.
- Cmentarz → mapa cmentarza z arkuszem grobu (R2) → widok grobu (R4 lewy) → osoba (R4 prawy) → drzewo i
  ścieżka (R3).
- **Mapa Polski jest ekranem głównym od startu** (decyzja autora 2026-10-06): kontur z wbudowanych danych,
  bez dostawcy kafelków ([[ISSUE-014-home-map-of-poland]], [[cmentarze]]). Na zdjęcie satelitarne czeka tylko
  mapa cmentarza (R2, [[SPIKE-001-map-source-offline]]).

## Where the images are
**`05_DESIGN/brand/references/`, lokalnie** (decyzja autora 2026-10-06: obrazy położył w
`01_INBOX/Inspiracje/`, a przy rozdzieleniu INBOX trafiły tutaj):
- `R1-mapa-polski.png`;
- `R2-mapa-cmentarza.png`;
- `R3-drzewo-sciezka-suwak.png`;
- `R4-grob-i-osoba.png`.

**Git ich nie widzi:** blok danych rodziny w `.gitignore` (`*.png`) ignoruje je po cichu, więc nie trafią
do publicznego repo ani do historii. To też znaczy, że **nie ma ich w kopii przez git**: na innej maszynie
folder będzie pusty. Trwałą kopię trzyma autor (np. na Dysku); ten plik zachowuje prompty i opisy.
