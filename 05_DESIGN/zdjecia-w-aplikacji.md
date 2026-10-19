---
screen: "Zdjęcia w aplikacji — wybór zdjęć, które już są u innych osób"
items: ["[[ISSUE-048-portrait-photos]]"]
us: "[[US-005-zdjecia]] — [[ISSUE-048-portrait-photos]] AC-4, AC-5 (z [[ISSUE-026-link-existing-photo-to-person]] AC-1, AC-2)"
journey-step: "n/a — M1 (przepisywanie i zbieranie u babci: zdjęcie grupowe z albumu u kilku osób)"
mockup: "2026-10-19: makieta-048.html (klikalna; ekran 5 „Zdjęcia w aplikacji”, warianty P1 i P2 portretu) — katalog tymczasowy sesji, ścieżka w ISSUE-048 → Implementation plan"
updated: 2026-10-19
---

# Zdjęcia w aplikacji — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.43, reguła 14) · referencja: brak w [[references]] (R1–R4 nie
> pokazują wyboru zdjęć), więc ekran dziedziczy reguły stylu B i wzorce [[zdjecia-osoby]] (siatka) i [[zdjecie]] D (szukanie osób).
>
> **Wersja 1 (2026-10-19, `ui` przed planem [[ISSUE-048-portrait-photos]]).** Nowy ekran z [[ISSUE-026-link-existing-photo-to-person]], wchłoniętej
> przez ISSUE-048: autor przy pustej sekcji „Zdjęcia” — *„…abym wiedział że mogę tutaj je dodać na dole (lub połączyć z istniejącymi)”*.
> **Może wypaść z zakresu na stopie #1** (ISSUE-048 → *Notes*, termin instalacji 2026-10-29). Wtedy ISSUE-026 wraca do `ready`, a plik zostaje
> jako projekt na później. [[zdjecia-osoby]] D6 *Obali* trafione.
>
> **Wersja 1.1 (2026-10-19, przegląd `ui` zbudowanej [[ISSUE-048-portrait-photos]] — przyjęte odstępstwo 3 `dev`):** stan „plik bez odczytu” dzieli się na
> dwa: **pliku nie ma** — komórka nieaktywna, jak w v1; **plik jest, ale się nie dekoduje** — ta sama ikona, komórkę da się zaznaczyć (D9).
>
> **Wersja 1.2 (2026-10-19, przegląd `ui` [[ISSUE-048-portrait-photos]], znalezisko 5 — przyjęte odstępstwo 5 kodu):** „Dodaj” zamyka ekran zawsze, a zapisuje
> ten, kto go otworzył; błąd zapisu z widoku osoby to komunikat widoku albo linia „Zdjęcia profilowego”, a zaznaczenie przepada (D10). Do tego nagłówki
> sekcji i wiersze osób są nagłówkami dla czytnika (element 4–6), a w stałych tekstach stoją twarde spacje („w aplikacji”, „u innych osób”, „· 3 zdjęcia” —
> [[style-b]] reguła 6).

## Purpose
Dodać osobie zdjęcie, które **już jest w aplikacji u innej osoby**, np. zdjęcie grupowe z albumu u babci, bez drugiego pliku (AC-4). Przy
kilkuset zdjęciach autor znajduje je po imieniu osoby, która je ma, bez przewijania wszystkiego (AC-5). Dziś da się to zrobić tylko od strony
zdjęcia: u tamtej osoby pod ✎ → podgląd → „Na zdjęciu · Zmień” ([[zdjecie]] D).

**Model** ([[ADR-009-person-photos-record-and-link]]): wybór tworzy **łącze** tej osoby do istniejącego zdjęcia, na końcu jej kolejności. Plik i
łącza innych osób się nie zmieniają. Bez zmiany schematu.

## Navigation
- **Wejście:** wiersz **„Ze zdjęć w aplikacji”** w arkuszu źródła w trybie osoby ([[zdjecie]] A4, v1.7), czyli z każdego miejsca, które dodaje
  zdjęcia osobie:
  - z widoku osoby ([[osoba]] v2.9): portret → „Zdjęcie profilowe” → kafelek „Dodaj zdjęcia”, okrąg z inicjałami, „Dodaj zdjęcie” w pustej
    sekcji „Zdjęcia”;
  - z formularza ([[wpis-osoby]] 1a, kafelek w [[zdjecia-osoby]]).

  **Nie z „Zdjęcia w tle”** (D7). Wiersza nie ma, gdy w aplikacji nie ma zdjęć innych osób, których ta osoba jeszcze nie ma.
- **„Dodaj N zdjęć”** (7) → powrót tam, skąd otwarto arkusz:
  - **z widoku osoby — zapis od razu** ([[osoba]] D24): widok osoby z nową liczbą „Zdjęcia · N”, a gdy to pierwsze zdjęcia osoby — z portretem;
    z „Zdjęcia profilowe” — ten ekran z nowymi zdjęciami w siatce;
  - **z formularza — do zmian formularza**, zapis z „Zapisz” ([[zdjecia-osoby]] D1); baza zdjęć pokazuje linię zapisu (element 6).
- **Wstecz** → tam, skąd otwarto arkusz, bez zmian i bez okna. Przepada najwyżej zaznaczenie ([[style-b]] reguła 10).
- Dolnego paska nie ma — tryb wyboru ([[style-b]] reguła 12).

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** wstecz; tytuł „Zdjęcia w aplikacji” (16 sp, półgruby); podtytuł **„dla: Jan Wymyślony”** (14 sp, tekst pomocniczy, jedna linia, ucięta) — osoba, do której zdjęcia dołączą, bez „z d.” (jak [[zdjecie]] B1); z formularza bez imienia — „dla: Nowa osoba” | pasek | wstecz → bez zmian | — | — | decyzja projektowa · wzorzec [[zdjecie]] D1 |
| 2 | **Pole „Szukaj osoby”** jak [[zdjecie]] D3: ramka w kolorze obrysu, ikona `search` (tekst pomocniczy), **przypięte pod paskiem** (nie przewija się z listą), bez fokusu od wejścia; filtruje grupy po imionach, nazwisku i nazwisku rodowym osoby, bez polskich znaków i końcówek (`matchesQuery`); `done` chowa klawiaturę | pole tekstowe | `done` | pusto | — | AC-5 · [[zdjecie]] D7 |
| 3 | **Linia pod polem:** „Bez zdjęć, które Jan już ma. Dotknij zdjęć, które dodać.” (14 sp, tekst pomocniczy; imię osoby z paska) | tekst | — | — | — | D3 · [[style-b]] reguła 7 |
| 4 | **Sekcja „Najbliżsi”** (nagłówek 14 sp, półgruby, tekst pomocniczy, jak [[zdjecie]] D4): grupy osób z mini-drzewa tej osoby (rodzice, partnerzy, dzieci — [[osoba]] 6) i z jej grobu, alfabetycznie. Bez takich osób ze zdjęciami — sekcji nie ma | nagłówek + grupy | — | — | — | D4 |
| 5 | **Sekcja „Inne osoby”** (nagłówek jak 4): pozostałe osoby ze zdjęciami, alfabetycznie po nazwisku, potem imionach (`polishCompare`) | nagłówek + grupy | — | — | — | D4 · AC-5 |
| 6 | **Grupa osoby** — tylko osoba, która ma choć jedno zdjęcie, którego ta osoba nie ma; bez samej tej osoby. **Wiersz osoby** (nie przycisk; ≥ 56 dp): okrąg 40 dp (profilowe w kadrze łącza — [[kadr-profilowego]]; bez zdjęcia — inicjały na powierzchni z obrysem), obok imiona i nazwisko z „z d.” (16 sp, tekst) i pod nimi „1924–2001 · 3 zdjęcia” (14 sp, tekst pomocniczy; lata jak w [[grob]], liczba z odmianą). **Pod nim siatka** jak [[zdjecia-osoby]] 4: 3 kolumny, kwadraty z promieniem 8 dp, odstęp 8 dp, marginesy 16 dp, przycięte ze środka, w kolejności łączy tamtej osoby, **bez zdjęć, które ta osoba już ma** (D3). **Zdjęcie grupowe stoi pod każdą osobą, która je ma** (D2). **Dotknięcie przełącza zaznaczenie**; zaznaczone ma ramkę jak obecne tło w „Zdjęciu w tle” ([[zdjecia-osoby]] v1.4): 2 dp akcentu, 2 dp tła, zdjęcie mniejsze w środku z promieniem 4 dp. **Zaznaczenie należy do zdjęcia, nie do miejsca:** zdjęcie grupowe zaznaczone w jednej grupie ma ramkę we wszystkich. Opis komórki dla czytnika: „Anna Wymyślona, zdjęcie 2 z 3 — zaznacz”, zaznaczone: „…, zaznaczone — odznacz” | wiersz + siatka obrazów-przycisków (komórka ok. 104 dp przy 360 dp) | dotknięcie → zaznacz / odznacz | nic nie zaznaczone | — | AC-4 · AC-5 · D1 · D2 · [[style-b]] reguła 14 · SC 1.4.1 |
| 7 | **„Dodaj”** — przycisk wypełniony (akcent), przypięty na dole, ≥ 52 dp, pełna szerokość z marginesami 16 dp. Bez zaznaczenia nieaktywny, z napisem „Dodaj”; z zaznaczeniem **„Dodaj 1 zdjęcie” · „Dodaj 2 zdjęcia” · „Dodaj 5 zdjęć”** (D5). Zaznaczone zdjęcia dostają łącze do tej osoby **na końcu jej kolejności, w kolejności zaznaczania**; gdy osoba nie miała zdjęć, pierwsze zostaje profilowym ([[zdjecie]] D, [[kadr-profilowego]] D3 — bez kadru, ze środka) | przycisk | → *Navigation* | nieaktywny | ≥ 1 zaznaczone | AC-4 · [[style-b]] reguła 1 · D5 · D8 |

**Pusty wynik filtra:** w miejscu sekcji „Nie ma osoby ze zdjęciami pasującej do „…”.” (14 sp, tekst pomocniczy). Zaznaczenia w ukrytych
grupach zostają, a przycisk 7 dalej je liczy.

**Dane, których ekran potrzebuje** (dla `planning`):
- wszystkie łącza osoba–zdjęcie: osoba, zdjęcie, miejsce w kolejności, plik — **nowe zapytanie** obok `personPhotos` (dziś łącza czyta się
  osobno dla każdej osoby);
- osoby z łączami: imiona, nazwisko, nazwisko rodowe, lata, profilowe z kadrem (jak [[osoby]] i [[zdjecie]] D5);
- zdjęcia tej osoby: zapisane łącza i, z formularza, zmiany szkicu, żeby ukryć to, co już ma (D3);
- rodzina z mini-drzewa tej osoby i osoby z jej grobu (sekcja 4);
- **dołączenie istniejącego zdjęcia do szkicu zdjęć osoby** — `PersonPhotosDraft` umie dziś dodać tylko plik wybrany z galerii albo aparatu
  (`addPicked`). Łącze do zapisanego zdjęcia to `SavedPhoto` z `mediaId` innej osoby; zapis przez `applyPersonPhotoEdits` jak każda zmiana zdjęć
  osoby. Bez zmiany schematu (łącze istnieje od v4).

Miniatury dekodowane w rozmiarze komórki, jak w [[zdjecia-osoby]]. Siatka budowana leniwie przy kilkuset zdjęciach.

## States
| Stan | Co widać |
|---|---|
| wczytywanie | tło z paskiem i polem; grupy, gdy lista łączy jest gotowa (lokalna baza — ułamek sekundy, bez wskaźnika, jak [[zdjecie]] „B — wczytywanie”) |
| wypełniony | 1–7, „Dodaj” nieaktywny |
| zaznaczone | ramki na zaznaczonych zdjęciach (we wszystkich grupach); „Dodaj 2 zdjęcia” aktywny |
| filtr | tylko grupy pasujących osób; nagłówek sekcji bez grup znika; zaznaczenia ukrytych zostają |
| pusty wynik filtra | „Nie ma osoby ze zdjęciami pasującej do „…”.” |
| brak zdjęć do wyboru | nie występuje — bez zdjęć innych osób wiersz „Ze zdjęć w aplikacji” w arkuszu jest ukryty ([[zdjecie]] A4) |
| plik bez odczytu | **pliku nie ma** (sprawdzenie przy wczytaniu ekranu): komórka na powierzchni z `broken_image_outlined` (tekst pomocniczy), **nieaktywna** (opis „…, nie da się otworzyć zdjęcia”) — łącze do pliku, którego nie ma, nic by nie dało. **Plik jest, ale się nie dekoduje** (v1.1, D9): ta sama ikona, komórka **da się zaznaczyć**, opis jak każdej komórki |
| zapis — błąd (z widoku osoby) | ~~ekran zostaje z zaznaczeniem; komunikat „Nie udało się dodać zdjęć…”~~ **v1.2 (D10):** ekran jest już zamknięty — zapisuje ten, kto go otworzył: widok osoby pokazuje u dołu „Nie udało się zapisać zdjęć. Spróbuj jeszcze raz.”, a „Zdjęcie profilowe” linię błędu pod siatką; zaznaczenie przepada, osoba bez zmian |

## Sketch
```
┌──────────────────────────────────┐
│ ←  Zdjęcia w aplikacji           │
│    dla: Jan Wymyślony            │
│ ┌ 🔍 Szukaj osoby ─────────────┐ │  przypięte
│ └──────────────────────────────┘ │
│ Bez zdjęć, które Jan już ma.     │
│ Dotknij zdjęć, które dodać.      │
│ Najbliżsi                        │
│ (AW) Anna Wymyślona z d. Zmyślona│
│      1924–2001 · 3 zdjęcia       │
│ ╭──────╮ ┏━━━━━━┓ ╭──────╮       │
│ │ ▓▓▓▓ │ ┃╭────╮┃ │ ░░░░ │       │  ┏┓ zaznaczone: ramka wokół,
│ │ ▓▓▓▓ │ ┃│▒▒▒▒│┃ │ ░░░░ │       │     nic na zdjęciu
│ ╰──────╯ ┗━━━━━━┛ ╰──────╯       │
│ (PW) Piotr Wymyślony             │
│      ur. 1950 · 2 zdjęcia        │
│ ╭──────╮ ╭──────╮                │
│ Inne osoby                       │
│ (HP) Helena Przykładowa          │
│      1899–1975 · 4 zdjęcia       │
│ ╭──────╮ ╭──────╮ ┏━━━━━━┓       │  to samo zdjęcie grupowe
│ ...                              │  zaznaczone też u Stefana
│ ┌──────────────────────────────┐ │
│ │       Dodaj 2 zdjęcia        │ │  przypięty
│ └──────────────────────────────┘ │
└──────────────────────────────────┘
```

## Tempo
Rekordem jest **zdjęcie dzielone** (grupowe, u kilku osób). Ile ich będzie, nie wiadomo — założenie z [[zdjecia-osoby]] → *Tempo*: ok. 50
zdjęć osób w MVP; dzielonych niewiele, ale każde to kilka osób.

| Działanie | Dotknięcia | Uwagi |
|---|---|---|
| **Zdjęcie grupowe Anny dla Jana, z widoku Jana** (portret → kafelek „Dodaj zdjęcia” → „Ze zdjęć w aplikacji” → zdjęcie → „Dodaj 1 zdjęcie”) | **5** | zapis od razu; Anna w „Najbliższych”, więc bez szukania |
| to samo dla osoby spoza najbliższych | 5 + 2–4 litery | szukanie po imieniu (AC-5) |
| to samo przez okrąg z inicjałami (osoba bez zdjęć) | **4** | okrąg → „Ze zdjęć w aplikacji” → zdjęcie → „Dodaj” |
| dziś, od strony zdjęcia (✎ u Anny → 1a → zdjęcie → „Zmień” → litery → wiersz Jana → „Gotowe” → wstecz → „Zapisz”) | 8 + litery | droga zostaje ([[zdjecie]] D) — lepsza, gdy na zdjęciu jest kilka osób naraz |

## Style B rules applied
- **Reguła 14:** zdjęcia to kwadraty w siatce, przycięte ze środka; **nic na zdjęciu** — zaznaczenie to ramka wokół (v1.19), a zdjęć, które ta osoba
  już ma, nie wyszarzamy na zdjęciu, tylko ich nie ma (D3); okrąg tylko dla profilowego w wierszu osoby.
- **Reguła 1:** jeden wypełniony przycisk — „Dodaj”; nieaktywny jest zwolniony z SC 1.4.11 (*inactive user interface components*), a stan niesie
  napis bez liczby.
- **Reguła 3:** `search` w tekście pomocniczym (opisuje pole); bez innych ikon.
- **Reguła 7:** linia 3 mówi, czego tu nie ma i co zrobić, bez ostrzeżenia.
- **Reguła 10:** „Dodaj” kończy się widokiem dodanych zdjęć tam, skąd przyszedłeś, bez okienka.
- **Reguła 12:** bez dolnego paska — tryb wyboru.
- **Progi:** komórka ok. 104 dp ≥ 48 dp; treść 16 sp, drobny tekst 14 sp; zaznaczenie niesie zmiana kształtu (ramka, mniejsze zdjęcie) i stan dla
  czytnika, nie tylko akcent (SC 1.4.1); ramka akcent–tło 8,81:1 na każdym zdjęciu (SC 1.4.11).
- **Tokeny:** bez nowych.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| ISSUE-048 AC-4 (ISSUE-026 AC-1) — zdjęcie grupowe Marii u Jana, plik jeden | [[zdjecie]] A4 → 6, 7 | u Jana „Ze zdjęć w aplikacji” → grupa Marii → zdjęcie grupowe → „Dodaj 1 zdjęcie”; zdjęcie jest w „Zdjęciach” Jana i dalej u Marii, „Na zdjęciu: Jan Wymyślony, Maria Zmyślona”; w magazynie aplikacji jeden plik (`qa`) |
| ISSUE-048 AC-5 (ISSUE-026 AC-2) — przy kilkuset zdjęciach bez przewijania wszystkiego | 2, 4, 5, 6 | „mar” w polu → tylko grupy osób o pasującym imieniu albo nazwisku; najbliżsi bez szukania na górze |

## Decisions
- **D1 — zdjęcia pogrupowane według osób, nie jedna siatka wszystkich.** Autor szuka zdjęcia, „które już jest u innej osoby” (ISSUE-026), więc
  szuka po osobie. Jedna siatka kilkuset zdjęć bez porządku to przewijanie wszystkiego (AC-5); grupy z polem szukania prowadzą do osoby w kilku
  literach. *Obali:* autor szuka po wydarzeniu („to ślubne”), nie po osobie → opis albo data zdjęcia, osobna pozycja.
- **D2 — zdjęcie grupowe pod każdą osobą, która je ma; zaznaczenie wszędzie.** Autor nie wie, u kogo zdjęcie zapisał najpierw, i szuka go u
  osoby, którą na nim widzi. Zaznaczenie należy do pliku, więc ramka jest we wszystkich grupach, a przycisk 7 liczy zdjęcia, nie ramki. *Obali:*
  powtórzenia wydłużają listę tak, że przewijanie przeszkadza → zdjęcie tylko przy pierwszej osobie.
- **D3 — zdjęć, które ta osoba już ma, nie ma na liście** (zamiast wyszarzenia). Wyszarzenie byłoby filtrem na zdjęciu (reguła 14), a znak „już
  jest” — znakiem na zdjęciu. Linia 3 mówi, że ich tu nie ma. *Obali:* autor szuka zdjęcia, którego „nie ma”, a ono już jest u tej osoby → wiersz
  osoby z dopiskiem „i 2 zdjęcia, które Jan już ma”.
- **D4 — „Najbliżsi” na górze** (rodzina z mini-drzewa i ten grób). Zdjęcie grupowe z albumu to najczęściej zdjęcie rodzinne ([[zdjecie]] D7:
  zbieranie u babci), więc zwykle jest u żony, rodzica albo dziecka. Ten sam wzorzec co „W tym grobie” na górze „Kto jest na zdjęciu?”.
  **Wariant tańszy dla `planning`:** wszystkie grupy alfabetycznie, bez sekcji (szukanie i tak działa).
  *Obali:* zdjęcia dzielone są głównie z dalszą rodziną → bez sekcji.
- **D5 — zaznaczenie kilku i liczba na przycisku** (ISSUE-026: „zaznaczenie kilku, „Gotowe””). Zaznaczenia w innych grupach mogą być poza ekranem,
  a po szukaniu — w ukrytych grupach, więc przycisk mówi, ile zdjęć dołączy. „Dodaj”, a nie „Gotowe”: przycisk mówi, co się stanie.
- **D6 — bez podglądu na pełnym ekranie z tego ekranu.** Dotknięcie zaznacza, bo to jedyne zadanie ekranu, a całe zdjęcie da się obejrzeć po
  dodaniu, w „Zdjęciach” osoby. *Obali:* autor nie rozpoznaje zdjęć grupowych w miniaturze 104 dp → przytrzymanie otwiera podgląd.
- **D7 — nie w „Zdjęciu w tle”** (ISSUE-026: „także w wyborze tła — do decyzji przy projekcie”). Tło to zwykle widok albo dom, a „Zdjęcie w tle”
  wybiera **jedno** zdjęcie od razu; wybór kilku z liczbą na przycisku tam nie pasuje, a tryb jednego zdjęcia to drugi tryb tego ekranu. Zdjęcie
  innej osoby jako tło: portret → „Dodaj zdjęcia” → „Ze zdjęć w aplikacji”, potem pasmo → zdjęcie (ok. +4 dotknięcia). *Obali:* autor szuka go w
  „Zdjęciu w tle”.
- **D8 — zapis zależy od wejścia.** Z widoku osoby od razu, jak każda zmiana zdjęć z widoku ([[osoba]] D24); z formularza — z „Zapisz”, jak reszta
  formularza ([[zdjecia-osoby]] D1). Ekran ten sam, zmienia się tylko to, kto zapisuje.
- **D9 — plik, który jest, ale się nie dekoduje, da się zaznaczyć** (v1.1; odstępstwo 3 `dev` w [[ISSUE-048-portrait-photos]], przyjęte w przeglądzie `ui`
  2026-10-19). Brak pliku ekran rozpoznaje jednym sprawdzeniem pliku przy wczytaniu. Uszkodzenie wyszłoby dopiero z dekodowania każdego zdjęcia przed
  pokazaniem ekranu, a przy kilkuset zdjęciach to czas wejścia (AC-5). Przypadek rzadki, a łącze wskazuje ten sam plik, który ma tamta osoba: niczego nie
  psuje i naprawia się razem z nim. Czytnik nie słyszy, że zdjęcie jest uszkodzone — ekran dowiaduje się o tym dopiero przy rysowaniu komórki.
  *Obali:* uszkodzone pliki zdarzają się po odtworzeniu kopii albo przeniesieniu na nowy telefon → sprawdzenie dekodowania w tle i komórka nieaktywna,
  gdy wynik przyjdzie.
- **D10 — „Dodaj” zawsze zamyka ekran, a zapisuje wołający** (v1.2; przegląd `ui` [[ISSUE-048-portrait-photos]], znalezisko 5 — kod tak działa od
  początku). Ekran wyboru oddaje zaznaczone zdjęcia, a zapis od razu z widoku (D8, [[osoba]] D24) robi jedna funkcja dla wszystkich dodawanych zdjęć —
  z galerii, aparatu i z aplikacji — z jednym komunikatem błędu. Zatrzymanie ekranu przy błędzie wymagałoby tu drugiej drogi zapisu. Koszt: po błędzie
  zaznaczenie trzeba powtórzyć (błąd zapisu lokalnej bazy jest rzadki). *Obali:* błędy zapisu zdarzają się na telefonie (np. pełna pamięć) i autor
  traci duże zaznaczenia → ekran zostaje otwarty do zapisu.

## Open
brak. Zakres (AC-4, AC-5 w tej pozycji czy później) — pytanie `planning` na stopie #1 (ISSUE-048 → *Notes*), nie luka projektu.
