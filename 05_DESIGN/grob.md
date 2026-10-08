---
screen: "Grób — wszyscy pochowani"
items: ["[[ISSUE-012-transcribe-grave-screen]]", "[[ISSUE-016-photos-grave-and-person]]", "[[ISSUE-017-person-photos]]", "[[ISSUE-018-profile-photo-crop]]", "[[SPIKE-004-mvp-flow-prototype]]"]
us: "[[US-002-przepisanie-grobu]] · [[US-005-zdjecia]]"
journey-step: "n/a — M1; ten sam widok stanie się widokiem 3 (krok 4 UJ-001, M4, R4 lewy) — wizyta dojdzie tutaj"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-cmentarz-grob-osoba.html (ramki 5–7, ISSUE-012) · makieta-zdjecia.html (ramki 1, 2, 4, ISSUE-016)"
updated: 2026-10-08
---

# Grób — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.9) · referencja: [[references]] → **R4 (lewy
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
>
> **Wersja 3 (2026-10-07, [[ISSUE-016-photos-grave-and-person]]) — zdjęcie nagrobka, jak w R4:** **jedno**
> zdjęcie nad tytułem (element 1a), „Dodaj zdjęcie” obok „Dodaj osobę”, dopóki grób nie ma zdjęcia (element 6);
> zmiana i usunięcie w podglądzie. Wybór źródła i podgląd: [[zdjecie]]. **Decyzje autora na stopie #1** (rundy 1–2):
> *„nagrobek — wystarczy mi jedno zdjęcie”*, a zdjęcia osób jako baza zdjęć z „profilowym” — to
> [[ISSUE-017-person-photos]]. **Miniatury osób w kartach (element 5) to kierunek dla ISSUE-017**, nie wchodzą w
> ISSUE-016.
>
> **Wersja 3.1 (2026-10-07, przegląd `ui` zbudowanego ekranu):** stan „wczytywanie zdjęcia” (pole 4:3 bez
> wskaźnika — tytuł i osoby nie zjeżdżają, gdy zdjęcie się pojawi); zdjęcie z galerii to 4 dotknięcia (okno
> systemowe wymaga „Gotowe”); zmierzone, ile osób mieści się nad zgięciem (*Tempo*, D8).
>
> **Wersja 3.2 (2026-10-07, stop #2 ISSUE-016 — decyzja autora):** *„dodaj zdjęcie powinno być domyślnie na polu
> przeznaczonym dla zdjęcia”*. Grób bez zdjęcia ma nad tytułem **pole „Dodaj zdjęcie nagrobka”** (element 1a, D12),
> a rząd działań ma już tylko „Dodaj osobę”.
>
> **Wersja 4 (2026-10-07, przed planem [[ISSUE-017-person-photos]]) — miniatury osób.** Kierunek z v3 (element 5, D11)
> wchodzi bez zmian kształtu. Miniatura w karcie to **profilowe** osoby, czyli pierwsze łącze
> ([[zdjecia-osoby]]). Zdjęcia osoby dodaje się i zmienia w formularzu osoby ([[wpis-osoby]] v4, element 1a), a nie
> tutaj, więc widok grobu nie dostaje nowych działań.
>
> **Wersja 4.1 (2026-10-07, przed planem [[ISSUE-018-profile-photo-crop]]):** miniatura w karcie (element 5) pokazuje
> profilowe **w kadrze** z [[kadr-profilowego]]; bez kadru — jak dotąd, ze środka. Bez nowych działań.
>
> **Wersja 5 — discovery na prototypie, panel 3 ([[SPIKE-004-mvp-flow-prototype]] D13, 2026-10-08):** widok grobu
> zostaje jak zbudowany (autor: *„1 ok”*). Zmieniają się dwie rzeczy:
> - **karta osoby otwiera widok osoby** ([[osoba]], panel 4), a nie formularz poprawy ([[style-b]] reguła 15,
>   SPIKE-004 D4; autor: *„2 ok”*). Poprawa jest pod ✎ w widoku osoby;
> - **dolny pasek** Mapa · Osoby · Drzewo jest widoczny, a aktywna jest zakładka, z której przyszedł autor
>   ([[style-b]] reguła 12).
>
> **Wersja 5.1 — wizyta ([[SPIKE-004-mvp-flow-prototype]] D22, 2026-10-08):** grób bez pinezki ma pod adresem przycisk z
> obrysem **„Postaw pinezkę”** (`add_location_alt` w akcencie) → mapa cmentarza w trybie stawiania pinezki ([[cmentarz]]
> element 12). Grób z pinezką ma pod adresem jej źródło: „Pinezka: GPS ±4 m · 08.10.2026” (13 sp, tekst pomocniczy).
>   ([[style-b]] reguła 12).

## Purpose
Wszyscy pochowani w jednym grobie, z datami z dopiskiem (US-002 AC-1, AC-3), nazwa grobu i widoczny brak
adresu kwatery oraz pinezki (AC-5). Stąd dodaje się kolejną osobę, więc przy przepisywaniu to też
potwierdzenie, że wpis się zapisał. Układ to R4: zdjęcie nagrobka u góry (US-005 AC-1), a zdjęcia osób w kartach
dojdą z [[ISSUE-017-person-photos]]. Zdjęcie nagrobka posłuży kiedyś do rozpoznania grobu na miejscu (brief §4a,
krok 3).

## Navigation
- Z [[cmentarz]] (dotknięcie karty grobu) albo z [[wpis-osoby]] po zapisie. Formularz znika ze stosu, więc
  wstecz z grobu wraca do [[cmentarz]], nie do formularza.
- **Ikonka edycji (3) → okno „Popraw grób”** nad widokiem grobu; „Zapisz” zamyka okno, a tytuł się zmienia.
- „Dodaj osobę” → [[wpis-osoby]] w trybie „kolejna osoba”.
- **„Dodaj zdjęcie” → arkusz źródła** ([[zdjecie]] A) → systemowe okno wyboru (jedno zdjęcie) albo aparat → z
  powrotem tutaj, a zdjęcie zapisuje się od razu, bez formularza (v3).
- **Dotknięcie zdjęcia nagrobka → podgląd** ([[zdjecie]] B): tam „Zmień zdjęcie” i „Usuń zdjęcie” (v3).
- Dotknięcie karty osoby → **widok osoby** ([[osoba]], M5, R4 prawy; v5, SPIKE-004 D13). Do v4.1 prowadziło do
  [[wpis-osoby]] w trybie „poprawa” (ISSUE-012, D1), bo widoku osoby nie było.
- **Dolny pasek** Mapa · Osoby · Drzewo widoczny (v5, [[style-b]] reguła 12).
- Wstecz → [[cmentarz]].

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** wstecz; podtytuł paska: nazwa cmentarza · miejscowość (14 sp, tekst pomocniczy, jedna linia, ucięta) | pasek | wstecz → [[cmentarz]] | — | — | decyzja projektowa |
| 1a | **Zdjęcie nagrobka** (v3). **Bez zdjęcia (v3.2, D12): pole „Dodaj zdjęcie nagrobka”** w tym samym miejscu — szerokość treści, **wysokość 120 dp**, zaokrąglenie 16 dp, obrys 1 dp w kolorze obrysu na tle (bez wypełnienia), w środku `add_a_photo_outlined` (32 dp, akcent) i pod nią „Dodaj zdjęcie nagrobka” (16 sp, półgruby 500, kolor tekstu); całe pole to jeden przycisk, opis dla czytnika „Dodaj zdjęcie nagrobka”; dotknięcie → [[zdjecie]] A. **Ze zdjęciem:** szerokość treści (marginesy 16 dp), zaokrąglenie 16 dp; proporcja zdjęcia, ale **nie wyżej niż szerokość** — wyższe (pionowy nagrobek) przycięte do kwadratu ze środka (D8). **Jedno zdjęcie na grób** (D9). Opis dla czytnika: „Zdjęcie nagrobka — otwórz”. Odstęp do tytułu 16 dp | obraz-przycisk | dotknięcie → [[zdjecie]] B | — | — | US-005 AC-1 · R4 · [[style-b]] reguła 14 · decyzja autora (jedno zdjęcie) |
| 2 | **Tytuł:** nazwa grobu (24 sp, półgruby, wyśrodkowany, do 2 linii). **Bez nazwy: „Grób”** w tym samym kroju | tekst | — | — | — | R4 · decyzja autora (nazwa grobu) · D1 |
| 3 | **Ikonka edycji** w linii tytułu, z prawej: `edit_outlined` w akcencie, cel 48 × 48 dp, `tooltip` „Popraw grób”. Tytuł ma z lewej taki sam odstęp, więc zostaje wyśrodkowany | przycisk-ikona | → okno „Popraw grób” (3a) | — | — | decyzja projektowa (jak [[cmentarze]] element 8) · D2 |
| 3a | **Okno „Popraw grób”:** pole **„Nazwa grobu”** (ramka w kolorze obrysu, wielka litera na początku zdania, podpowiedź „np. Grób rodzinny Nowaków” — tekst z R4), pod polem „Zostaw puste, jeśli grób nie ma nazwy.” (13 sp, tekst pomocniczy). Przyciski „Anuluj” (kolor tekstu) · **„Zapisz”** (akcent) — jak okno cmentarza w `cemetery_form.dart` | okno dialogowe | fokus i klawiatura od razu, kursor na końcu obecnej nazwy; `done` = „Zapisz” | obecna nazwa albo pusto | puste = bez nazwy (tytuł „Grób”); spacje na brzegach obcięte. Błąd zapisu: pod polem `error_outline` + „Nie udało się zapisać. Spróbuj jeszcze raz.” (kolor błędu), okno zostaje | decyzja autora (nazwa grobu) · [[style-b]] reguła 1 (okno) |
| 4 | **Adres i pinezka** pod tytułem, wyśrodkowane: adres pełnymi słowami „Kwatera B · Rząd 4 · Miejsce 12” (14 sp, tekst pomocniczy). Bez adresu: ikona `place_outlined` + „Bez adresu kwatery · bez pinezki”, a pod spodem „Uzupełnisz przy wizycie.” (tekst pomocniczy). Z adresem, bez pinezki: adres + „· bez pinezki” | tekst | — | — | — | AC-5 · R4 |
| 5 | **Karty osób** w kolejności wpisania, odstęp 8 dp. Karta: „Imiona Nazwisko z d. Rodowe” (16 sp, półgruby, zawijane); lata życia (14 sp, tekst pomocniczy): `1921–1987`, a z dopiskiem `ok. 1890 – 14.03.1951`; gdy jest data pochówku: `· poch. 18.03.1951`. Brak urodzenia: `zm. 1951`; brak zgonu: `ur. 1890`; brak dat: „bez dat”. **Chevron „›” — karta prowadzi do widoku osoby** ([[osoba]], v5; do v4.1 do poprawy). **Profilowe osoby (v4, [[ISSUE-017-person-photos]]):** okrąg 40 dp z lewej, wyśrodkowany w pionie, odstęp 12 dp do tekstu, w kadrze łącza ([[kadr-profilowego]], v4.1), a bez kadru przycięty ze środka, poza czytnikiem (kartę opisuje jej tekst); osoba bez zdjęcia — bez miniatury i bez wcięcia (D11). Plik bez odczytu: okrąg na tle z `broken_image_outlined` (20 dp, tekst pomocniczy) | lista kart na powierzchni, karta ≥ 64 dp | dotknięcie → widok osoby ([[osoba]], v5) | kolejność wpisania | — | AC-1 · AC-2 · AC-3 · R4 · ISSUE-017 AC 4 |
| 6 | **Rząd działań:** „Dodaj osobę” — przycisk z obrysem, ikona `person_add_alt_outlined` w akcencie, napis w kolorze tekstu, ≥ 52 dp, szerokość treści, z lewej. „Dodaj zdjęcie” jest w polu 1a (v3.2, D12), nie tutaj | rząd przycisków pod listą | „Dodaj osobę” → [[wpis-osoby]] „kolejna osoba” | — | — | *What to build* 3 · R4 |

**Gdy źródła się spierają** (dwie daty urodzenia albo dwa groby jednej osoby), widok pokazuje **pierwszą**
wartość — najniższe `id`, jak w GEDCOM 7 ([[ADR-006-claimed-value-separate-structures]] D3; `claims.dart` →
`firstEvent`). Oznaczenie sporu to [[US-004-fakt-od-babci]]. Osoba z dwoma pochówkami pojawia się w obu
grobach (ADR-006, *Consequences*).

**Dane, których ekran potrzebuje** (dla `planning`): nowe, opcjonalne pole **nazwa grobu** w tabeli grobów —
zmiana schematu, migracja v2→v3 z testem ([[NFR-003-migracje-schematu]]) i kopia zaraz po migracji (retro 1,
R6). Zapis nazwy zamawia kopię w tle jak każdy zapis.

**Dane, których ekran potrzebuje od v3** (dla `planning`, [[ISSUE-016-photos-grave-and-person]]): zdjęcie grobu
(najwyżej jeden wiersz `Media` z `grave_id`), więc **wygląd nie wymaga zmiany schematu**. Miniatura (56 dp w
[[cmentarz]]) i zdjęcie w widoku grobu dekodowane w rozmiarze, w jakim się wyświetlają. Dodanie, zmiana i usunięcie
zdjęcia zamawiają kopię w tle jak każdy zapis.

**Dane, których ekran potrzebuje od v4** (dla `planning`, [[ISSUE-017-person-photos]]): dla każdej osoby w grobie
ścieżka jej **profilowego**, czyli pliku z pierwszego łącza osoby, albo nic. **Od v4.1:** także kadr tego łącza (albo
brak kadru — wtedy środek). Miniatura dekodowana w rozmiarze 40 dp ×
gęstość ekranu, jak miniatury nagrobków.

## States
| Stan | Co widać |
|---|---|
| wypełniony | 1–6 (1a tylko, gdy grób ma zdjęcie; wtedy w 6 tylko „Dodaj osobę”) |
| bez zdjęcia (v3.2) | nad tytułem pole „Dodaj zdjęcie nagrobka” (1a, 120 dp); rząd działań — tylko „Dodaj osobę” |
| wczytywanie zdjęcia (v3.1) | do pierwszej klatki obrazu: w miejscu 1a puste pole w proporcji 4:3 (bez wskaźnika — zwykle ułamek sekundy), żeby tytuł i osoby nie przeskakiwały o wysokość zdjęcia |
| zapisywanie zdjęcia (v3) | w miejscu 1a pole na powierzchni (proporcja 4:3, zaokrąglenie 16 dp) ze wskaźnikiem postępu i „Zapisuję zdjęcie…” (14 sp, tekst pomocniczy) — zamiast pola „Dodaj zdjęcie nagrobka”. Zmniejszanie zdjęcia trwa chwilę (do zmierzenia). Po zapisie widać **dodane zdjęcie** — to potwierdzenie (reguła 10) |
| nieudany zapis zdjęcia (v3.2) | **pod polem 1a**, przy miejscu, którego dotyczy: `error_outline` + „Nie udało się zapisać zdjęcia. Spróbuj jeszcze raz.” (kolor błędu, 14 sp); pole „Dodaj zdjęcie nagrobka” zostaje. Komunikat znika przy następnym dodaniu |
| brak pliku zdjęcia (v3) | wpis zdjęcia jest, pliku nie ma albo nie da się go odczytać: w miejscu zdjęcia pole na powierzchni z `broken_image_outlined` i „Nie udało się otworzyć zdjęcia.” (tekst pomocniczy); dotknięcie → podgląd, gdzie można zdjęcie zmienić albo usunąć |
| bez nazwy | tytuł „Grób” + ikonka edycji; reszta bez zmian |
| pusty | „W tym grobie nie ma jeszcze wpisanych osób.” + „Dodaj osobę” (z interfejsu nie powstaje — patrz [[cmentarz]]) |
| okno „Popraw grób” | element 3a nad widokiem grobu |
| błąd | „Nie udało się odczytać grobu.” + „Spróbuj ponownie” (przycisk z obrysem) |
| wczytywanie | wskaźnik postępu w środku (zwykle niewidoczny) |

## Sketch
**v3 — ze zdjęciem nagrobka** (ISSUE-016; miniatury osób dojdą z ISSUE-017):
```
┌──────────────────────────────────┐
│ ←  Cmentarz Wymyślony · Miejsco… │
│ ╭──────────────────────────────╮ │
│ │                              │ │
│ │      [zdjęcie nagrobka —     │ │  ← dotknięcie: podgląd
│ │       wymyślone]             │ │    (zmień · usuń)
│ │                              │ │
│ ╰──────────────────────────────╯ │
│      Grób rodzinny          ✎   │
│      Wymyślonych                 │
│  ⌖ Bez adresu kwatery · bez      │
│    pinezki                       │
│ ╭──────────────────────────────╮ │
│ │ Jan Wymyślony              › │ │
│ │ ok. 1890 – 14.03.1951        │ │
│ ╰──────────────────────────────╯ │
│ ╭──────────────────────────────╮ │
│ │ Anna Wymyślona z d. Zmyślona›│ │
│ │ 1893–1960                    │ │
│ ╰──────────────────────────────╯ │
│ ╭─────────────────╮              │  ← zdjęcie jest: tylko
│ │ 👤+ Dodaj osobę  │              │    „Dodaj osobę”
│ ╰─────────────────╯              │
└──────────────────────────────────┘
```

**v3.2 — bez zdjęcia** (D12): w miejscu zdjęcia pole z obrysem, wysokość 120 dp:
```
│ ╭──────────────────────────────╮ │
│ │            📷+               │ │  ← add_a_photo_outlined, akcent
│ │    Dodaj zdjęcie nagrobka    │ │
│ ╰──────────────────────────────╯ │
│      Grób rodzinny          ✎   │
│      Wymyślonych                 │
```
Niżej szkic v2 — układ reszty widoku bez zmian; rząd działań ma tylko „Dodaj osobę”:
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
- **zdjęcie nagrobka (v3.1): 4 dotknięcia** z galerii („Dodaj zdjęcie”, „Wybierz z galerii”, zdjęcie, „Gotowe” —
  okno systemowe na Androidzie 16 wymaga potwierdzenia, [[zdjecie]] → *Tempo*). Na ok. 50 grobów: ok. 200 dotknięć.
  Też bez szukania grobu — widok jest na ekranie po zapisie osoby.
- **koszt zdjęcia nagrobka dla „Dodaj osobę” (v3):** zdjęcie (do kwadratu szerokości, ok. 330 dp) przesuwa rząd
  działań w dół. **Zmierzone (przegląd `ui`, `Medium_Phone` 411 × 914 dp):** bez przewijania „Dodaj osobę” mieści się
  przy zdjęciu poziomym (4:3) do **4 osób**, przy pionowym (kwadrat) do **3 osób**; od 5 (poziome) albo 4 (pionowe)
  trzeba przewinąć. Średnio ok. 2 osoby na grób (G6), więc przy przepisywaniu zwykle mieści się bez przewijania;
  przy dużych grobach taniej dodać zdjęcie **po** osobach z notatek. *Obali D8:* przewijanie przeszkadza na stopie
  #2 — wtedy zdjęcie niższe (np. do 200 dp) albo rząd działań przypięty na dole.

## Style B rules applied
- **Reguła 1:** brak wypełnionego przycisku — jak w R4, treścią są osoby. „Dodaj osobę” ma obrys i ikonę w
  akcencie. W oknie „Zapisz” jest przyciskiem tekstowym w akcencie.
- **Reguły 2 i 11:** karty osób na powierzchni z chevronem; bez zastępczych obrazków (miniatury osób —
  [[ISSUE-017-person-photos]]).
- **Reguła 14 (v1.7):** zdjęcie nagrobka bez filtrów i bez tekstu na nim; bez zdjęcia nie ma pola.
- **Reguła 3:** `place_outlined` w kolorze pomocniczym (opisuje), `person_add_alt_outlined`, `add_a_photo_outlined`
  i `edit_outlined` w akcencie (działania).
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
| US-005 AC-1 (v3.2, grób) | 1a → [[zdjecie]] A | pole „Dodaj zdjęcie nagrobka” → wybór → zdjęcie w tym samym miejscu, nad tytułem |
| US-005 AC-2 (v3) | 1a | zdjęcie dalej widać po usunięciu oryginału z galerii emulatora |
| US-005 AC-3 (v3) | 1a | po odtworzeniu z kopii to samo zdjęcie (odcisk danych — `qa`) |
| ISSUE-016: zmiana i usunięcie (decyzja autora, stop #1) | 1a → [[zdjecie]] B4, C | podgląd → „Zmień zdjęcie” → nowe zdjęcie; „Usuń zdjęcie” → okno → zdjęcia nie ma, „Dodaj zdjęcie” wraca |
| ISSUE-016: styl B | 1a, 6 | reguły 11 i 14 (puste miejsce na zdjęcie tylko jako przycisk); przegląd `ui` przed stopem #2 |
| ISSUE-017: profilowe osoby (v4) | 5 | karta osoby ze zdjęciem ma z lewej okrąg z profilowym; po „Ustaw jako profilowe” i „Zapisz” w formularzu okrąg pokazuje nowe; osoba bez zdjęć — karta bez wcięcia |
| ISSUE-017: zdjęcie dzielone (v4) | 5 | po zaznaczeniu drugiej osoby z grobu na zdjęciu, które dla niej jest pierwsze, jej karta też pokazuje to zdjęcie |

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
  **Wykonane w v3** — zdjęcie nagrobka i „Dodaj zdjęcie” w [[ISSUE-016-photos-grave-and-person]] (1a, 6, D8–D10);
  portrety w kartach w [[ISSUE-017-person-photos]] (5, D11).
- **D5 — kolejność wpisania**, nie chronologiczna: zgadza się z notatkami, więc łatwo porównać. *Obali:* autor
  na stopie #2 chce widzieć najpierw najstarszych.
- **D6 — daty z dokładnością taką, jak wpisano** (`ok. 1890 – 14.03.1951`), a nie same lata jak w R4: dopisek i
  dokładność to dana (FR-004), a nie szum. Same lata zostają, gdy wpisano same lata.
- **D7 — spór źródeł niewidoczny** — pokazuje się pierwsza wartość; oznaczenie to US-004.
- **D8 — zdjęcie nagrobka w proporcji zdjęcia, nie wyżej niż szerokość** (v3). Stała proporcja 4:3 ucinałaby
  pionowy nagrobek z góry i z dołu, a to on ma posłużyć do rozpoznania grobu (brief §4a krok 3). Zdjęcie
  poziome i kwadratowe widać więc w całości, a dopiero wyższe od kwadratu jest przycięte ze środka, żeby imiona
  osób nie zjechały za ekran. Całość jest zawsze o jedno dotknięcie dalej, w podglądzie. *Obali:* na stopie #2
  przycięcie pionowych zdjęć zabiera napis z tablicy — wtedy całe zdjęcie z pasami po bokach na powierzchni.
- **D9 — jedno zdjęcie nagrobka** (decyzja autora, stop #1 ISSUE-016: *„nagrobek — wystarczy mi jedno
  zdjęcie”*). Zmiana zastępuje zdjęcie, a „Dodaj zdjęcie” widać tylko bez zdjęcia. Wersja z kilkoma zdjęciami
  (przesuwanie, licznik „1 / 3”) odpada; przesuwanie i przyciski ‹ › wracają w bazie zdjęć osoby
  ([[ISSUE-017-person-photos]]).
- **D10 — „Dodaj osobę” zostaje z lewej** (z ISSUE-012). ~~„Dodaj zdjęcie” obok~~ — zastąpione przez D12 (v3.2).
- **D12 — „Dodaj zdjęcie” w miejscu zdjęcia** (v3.2, decyzja autora na stopie #2 ISSUE-016). Działanie stoi tam, gdzie
  pojawi się jego wynik, więc nie trzeba go szukać w rzędzie przycisków. To przycisk z obrysem, ikoną w akcencie i
  podpisem, a nie zastępczy obrazek ([[style-b]] reguły 11 i 14 — tak samo jak puste zdjęcie osoby w [[wpis-osoby]]
  v3). **Wysokość 120 dp, nie 4:3:** ok. 50 grobów zaczyna bez zdjęcia, a pole wielkości zdjęcia (ok. 250 dp)
  spychałoby osoby i „Dodaj osobę” na każdym z nich; 120 dp wystarcza, żeby czytało się jako „tu będzie zdjęcie”.
  *Obali:* autor chce pola wielkości zdjęcia — wtedy 4:3 i bez przeskoku po dodaniu.
- **D11 — karta osoby bez zdjęcia nie ma wcięcia** (kierunek z v3, wchodzi w [[ISSUE-017-person-photos]], v4). Reguła 11 zabrania zastępczych obrazków, a puste wcięcie
  wyglądałoby jak brakujące zdjęcie. Koszt: w grobie, gdzie część osób ma zdjęcie, imiona nie stoją w jednej linii.
  *Obali:* na stopie #2 karty mieszane wyglądają nierówno — wtedy wcięcie 52 dp bez obrazka u wszystkich, gdy
  choć jedna osoba w grobie ma zdjęcie.

## Open
brak. Usuwanie i zmiana zdjęcia nagrobka rozstrzygnięte na stopie #1 ISSUE-016 (wchodzą — [[zdjecie]] B4, C).
Poprawa wpisu rozstrzygnięta na stopie #1 ISSUE-012 (D1 — wchodzi).
