---
title: "Style B — visual guidelines (v1.8)"
type: design-guidelines
status: active
owner: ui
source: "PROJECT_BRIEF §6a (Style B, chosen by the author 2026-10-05) · references.md (R1–R4, the kick-off images) · grobing-code/lib/app/theme.dart · WCAG 2.2 · Android accessibility"
non-tech-item: "[[NT-006-visual-guidelines]]"
created: 2026-10-06
updated: 2026-10-07
---

# Styl B — wytyczne wizualne

> Właściciel: agent `ui`. Każdy ekran Grobing stoi na tym pliku; specyfikacje ekranów w `05_DESIGN/`
> mówią, które reguły stosują. **Kanonem wyglądu są obrazy z kick-offu — [[references]] (R1–R4)**; ten plik
> tłumaczy je na reguły, progi i pomiar. **Wartości kolorów mają jeden dom:
> `grobing-code/lib/app/theme.dart`.** Tu jest rola tokenu, reguła, próg i pomiar, a nie druga kopia wartości
> do utrzymania.

## Style — verbatim (brief §6a)
> *modern, minimal, dark mode — near-black background, soft grey text, one accent colour: warm amber like
> candlelight. Thin line icons, clean sans-serif type, subtle depth, calm and dignified, nothing gloomy.*

Trzy przymiotniki: **nowoczesny · minimalistyczny · godny**. Odrzucony styl A (jasny, ciepła biel) jest
zapisany w briefie jako świadomy wybór. **Odróżnia go od B jasność, nie znicz.** Obrazy B, które wybrał
autor, też używają znicza (reguła 8).

## Token roles
| Rola | Token w `theme.dart` | Do czego (według R1–R4) | Nigdy |
|---|---|---|---|
| tło | `GrobingColors.background` | tło każdego ekranu i paska aplikacji | — |
| powierzchnia | `GrobingColors.surface` | **karty** (osoba, grób, cmentarz), dolny arkusz, wyszukiwarka, okno, menu, chip, przycisk pływający | granica pola wpisu (tło–powierzchnia ma ok. 1,1:1, więc granicę niesie obrys) |
| tekst | `GrobingColors.text` | treść, wartości, imiona i nazwiska, tytuły | — |
| tekst pomocniczy | `GrobingColors.textMuted` | lata, adres, liczby („6 grobów · 14 osób”), etykiety, podpowiedzi, „bez adresu kwatery”, źródło, nieaktywne zakładki | jedyny nośnik ważnej informacji na ekranie wizyty (patrz *Thresholds*) |
| akcent | `GrobingColors.amber` | **jeden kolor, wiele ról** (reguła 1): główne działanie (wypełnione), pinezki, znicz, aktywna zakładka i segment, zaznaczenie, fokus, ikony działań i nagłówków sekcji, wyróżnione imiona na ścieżce, link zewnętrzny, wskaźnik działania w toku (v1.8) | treść ciągła (akapity), duże dekoracyjne plamy, ostrzeżenia i błędy |
| obrys *(nowy — wchodzi z [[ISSUE-014-home-map-of-poland]], zaproponowany przy [[ISSUE-012-transcribe-grave-screen]])* | proponowany `GrobingColors.outline` | ramka pola wpisu, przycisk z obrysem, linia podziału, granica na mapie (reguła 13) | tekst |
| błąd *(nowy — wchodzi z ISSUE-014)* | proponowany `GrobingColors.error` | komunikat błędu pod polem, jego ikona, ramka pola z błędem | cokolwiek poza błędem |

### State colours — beyond the accent
Poza akcentem występują tylko **kolory stanu**. Każdy pojawia się zawsze razem z ikoną albo tekstem, nigdy
sam (SC 1.4.1):

| Stan | Skąd | Kiedy wchodzi |
|---|---|---|
| błąd | czerwień złagodzona (propozycja `#E07A6F`, pomiar niżej) | ISSUE-014 |
| offline gotowy („Offline ✓”) | zieleń — R2 | pierwszy ekran wizyty (M7, EPIC-002): wartość i pomiar wtedy |
| „tu jesteś” | niebieska kropka — konwencja map, R2 | mapa cmentarza (EPIC-002) |

## Thresholds — with source
| Próg | Wartość | Źródło |
|---|---|---|
| kontrast tekstu | **≥ 4,5:1** | [WCAG 2.2](https://www.w3.org/TR/WCAG22/) SC 1.4.3 Contrast (Minimum), AA: *„text … has a contrast ratio of at least 4.5:1”* |
| kontrast elementów interfejsu (ramka pola, obrys przycisku, ikona, która coś znaczy) | **≥ 3:1** wobec sąsiedniego koloru | WCAG 2.2 SC 1.4.11 Non-text Contrast, AA |
| kolor jako nośnik | **nigdy jedyny**: błąd, brak, wybór i stan mają też tekst albo ikonę. Pozycja wybrana w menu ma ikonę `check` i stan „zaznaczone” dla czytnika, nie tylko akcent (v1.6) | WCAG 2.2 SC 1.4.1 Use of Color, A |
| rozmiar kontrolki z tekstem | **najmniejszy, nie stały**: przycisk, link i pole rosną z systemowym rozmiarem tekstu, zamiast ucinać napis (v1.6 — druga instancja po linku z v1.5) | WCAG 2.2 SC 1.4.4 Resize Text, AA |
| gesty | **przesunięcie i gest kilkoma palcami mają alternatywę jednym dotknięciem** (przyciski poprzednie/następne, podwójne dotknięcie zamiast rozsunięcia palców) (v1.7) | WCAG 2.2 SC 2.5.1 Pointer Gestures, A: *„All functionality that uses multipoint or path-based gestures for operation can be operated with a single pointer without a path-based gesture”* ([Understanding 2.5.1](https://www.w3.org/WAI/WCAG22/Understanding/pointer-gestures.html)) |
| cel dotyku | **≥ 48 × 48 dp** | [Android — Make apps more accessible](https://developer.android.com/guide/topics/ui/accessibility/apps) → *Use large, simple controls*: *„at least 48dp×48dp”* |
| rozmiary tekstu | treść i tekst wpisywany **≥ 16 sp**; drobny tekst pomocniczy ≥ 13 sp; etykieta przycisku 14–16 sp, waga 500 | decyzja projektowa (nie norma) — dane wpisuje się szybko i trzeba je odczytać bez mrużenia oczu |
| **kandydat** dla ekranów wizyty | **≥ 7:1** dla tekstu | WCAG 2.2 SC 1.4.6 Contrast (Enhanced), AAA. **Nie obowiązuje jeszcze:** propozycja miary dla [[NFR-004-czytelnosc-w-sloncu]] (`⚠️ OPEN` tam), decyzja przy pierwszym ekranie wizyty |

## Measurement — 2026-10-06
Kontrast według wzoru WCAG (luminancja względna), wartości z `theme.dart` w dniu pomiaru. Pomiar
pochodzi z [[ISSUE-013-setup-ui-agent]] → *Technical Notes*; kandydaci na nowe tokeny zmierzeni tym samym
wzorem. **Przelicz przy każdej zmianie tokenów.**

| Para | Na tle | Na powierzchni | Próg | Wynik |
|---|---|---|---|---|
| tekst | 10,98 | 10,02 | 4,5 (AA) · 7 (AAA) | ✅ AA · ✅ AAA |
| tekst pomocniczy | 5,50 | 5,01 | 4,5 (AA) · 7 (AAA) | ✅ AA · ❌ AAA |
| akcent jako tekst, ikona albo ramka | 8,81 | 8,04 | 4,5 / 3 | ✅ |
| tło na akcencie (napis na przycisku głównym) | 8,81 | — | 4,5 | ✅ |
| obrys *(kandydat `6B6862`)* | 3,40 | 3,10 | 3 (SC 1.4.11) | ✅ |
| błąd *(kandydat `E07A6F`)* | 6,45 | 5,89 | 4,5 | ✅ |
| tekst na zaznaczeniu tekstu (domyślne zaznaczenie Fluttera: akcent 40% na tle ≈ `#664D26`) *(v1.6)* | 4,60 | — | 4,5 | ✅ — tuż nad progiem: **nie zwiększać krycia zaznaczenia** |

**Wniosek:** wszystkie pary spełniają AA, a tekst pomocniczy nie spełnia kandydata 7:1. Jeśli ekrany
wizyty przyjmą 7:1, informacja potrzebna na cmentarzu (adres kwatery, lata) nie może być w kolorze
pomocniczym albo ten token trzeba rozjaśnić. Do rozstrzygnięcia przy pierwszym ekranie wizyty.

## Rules
1. **Jeden kolor akcentu, jedno główne działanie.** Bursztyn to jedyny kolor akcentu, ale ma wiele ról
   (*Token roles*, jak w R1–R4). Na ekranie jest **najwyżej jeden wypełniony bursztynowy przycisk**, czyli
   główne działanie. Forma działań:
   - **główne:** przycisk wypełniony (tło w akcencie, napis w kolorze tła, 8,81:1) w kształcie
     zaokrąglonego prostokąta (promień 12–16 dp), wysokość ≥ 52 dp. Delikatna poświata dozwolona (reguła 2).
     Na liście albo formularzu jest przypięty na dole na pełną szerokość, a na karcie albo arkuszu stoi w
     karcie (R1, R2);
   - **drugorzędne:** przycisk z obrysem (obrys, promień 12 dp), z **ikoną w akcencie** i napisem w kolorze
     tekstu, np. „Dodaj zdjęcie”, „Dodaj osobę” (R4). Kilka obok siebie tworzy rząd działań;
   - **w oknie dialogowym:** przyciski tekstowe, a potwierdzające w akcencie (wzorzec okien Material);
   - **przycisk tekstowy poza oknem** (v1.4): w akcencie, gdy jest jedynym działaniem dalej (np. „Dodaj
     ręcznie” pod wynikami); w kolorze tekstu, gdy stoi obok wypełnionego (np. „Zapisz bez punktu” obok
     „Zapisz”), żeby akcent miało tylko główne działanie. **Przycisk tekstowy w linii treści** (np. „Zmień”
     przy źródle biografii) jest w akcencie (v1.6);
   - **link zewnętrzny:** tekst w akcencie, podkreślony, ze strzałką „↗” (np. „Grobonet ↗”, R2). Szczegóły
     (v1.5, [[ISSUE-015-add-cemetery-from-database]]):
     - **strzałka to ikona `north_east`** w akcencie, a nie znak U+2197, bo Android rysuje ten znak jako
       kolorowe emoji (zobaczone na emulatorze). Byłby to drugi kolor obok akcentu;
     - ikona rośnie z systemowym rozmiarem tekstu (16 dp × skala tekstu);
     - podkreślenie obejmuje sam tekst;
     - cel dotyku ma ≥ 48 dp wysokości i rośnie, a tekst zawija się przy dużej czcionce zamiast się uciąć;
     - czytnik ekranu czyta link z dopiskiem „w innej aplikacji”.
2. **Głębia subtelna:** tło → powierzchnia (zaokrąglone karty, promień 12–16 dp, i dolny arkusz). Głównemu
   przyciskowi i zaznaczonemu elementowi (wybrana pinezka, węzeł na ścieżce) wolno mieć **delikatną
   bursztynową poświatę**. Bez twardych cieni i bez gradientów tła.
3. **Ikony cienkie:** warianty `outlined` z Material Icons. Ikona jest w kolorze tekstu pomocniczego, a
   **w akcencie wtedy, gdy oznacza działanie albo nagłówek sekcji** (R4: „Rodzina”, „Dodaj osobę”). Ikona,
   która niesie znaczenie, ma podpis albo `tooltip`.
4. **Krój:** systemowy bezszeryfowy (Roboto na Androidzie), bez własnych fontów w aplikacji. **Tytuły i
   imiona półgrube (waga 500–600)**, jak w R1–R4. Treść ma wagę regularną. Krój szeryfowy z R2 był
   przypadkiem generatora i nie obowiązuje.
5. **Odstępy:** siatka 8 dp. Na ekranach z listą albo formularzem margines boczny 16 dp, odstęp między
   grupami 24 dp, wewnątrz grupy 8–12 dp, a między kartami 8 dp. Kompozycje wyśrodkowane (pusty stan,
   nagłówek osoby z R4) biorą większe odstępy z tej samej siatki.
6. **Formaty po polsku:**
   - lata życia: `1921–1987`, a z dopiskiem `ok. 1890 – 14.03.1951` (spacje wokół kreski, gdy którakolwiek
     strona ma więcej niż sam rok);
   - daty: `14.03.1951`, `03.1951`, `1890`; dopiski: `ok. 1890`, `przed 1920`, `po 1945`, `między 1893 a 1895`;
   - nazwisko rodowe w tej samej linii co nazwisko: `Maria Nowak z d. Kowalska`;
   - adres pełnymi słowami: `Kwatera B · Rząd 4 · Miejsce 12`; liczby: `6 grobów · 14 osób`, `3 osoby`
     (z odmianą).
7. **Ton tekstów:** spokojny i rzeczowy. Bez wykrzykników, bez „Sukces!”, bez emotikonów. Brak czegoś
   opisujemy faktem i tym, kiedy się uzupełni („Bez adresu kwatery · uzupełnisz przy wizycie”), a nie
   ostrzeżeniem.
8. **Znicz to znak aplikacji** (R1–R3). Występuje w logo (znicz + „Grobing”), w pinezce (znicz w kształcie
   pinezki), na głównym działaniu prowadzącym do miejsca pamięci („Otwórz cmentarz”, „Pokaż grób”) i jako
   znacznik osoby zmarłej (węzeł drzewa, R3). **Znicz oznacza miejsce i pamięć**, a nie zwykłe działania:
   „Zapisz” i „Dodaj” go nie mają. **Krzyż ani inne symbole religijne nie pojawiają się w interfejsie** —
   są tylko na zdjęciach, czyli w treści użytkownika (R4). Gałązki wokół portretu (R4, osoba) to opcja
   widoku osoby, rozstrzygana przy tym ekranie.
9. **Puste stany** mówią, co tu będzie, i dają jedno działanie. Bez ilustracji.
10. **Potwierdzenia ciche:** zapis kończy się widokiem tego, co zapisano, a nie komunikatem w okienku.
    Okno dialogowe tylko wtedy, gdy coś może przepaść (niezapisany wpis).
11. **Listy jako karty:** element, który prowadzi dalej (osoba, grób, cmentarz), to karta na powierzchni z
    chevronem „›”. Miniatura zdjęcia z lewej, gdy zdjęcie jest ([[US-005-zdjecia]]). **Bez zastępczych
    obrazków**: brak zdjęcia oznacza brak miniatury.
12. **Nawigacja docelowa** ([[references]] → *Target app structure*): dolny pasek Mapa · Osoby · Drzewo
    (aktywna zakładka ma ikonę, podpis i podkreślenie w akcencie). Pojawia się, gdy istnieją co najmniej dwa
    z tych celów. Ustawienia, w tym „Stan danych”, są pod kołem zębatym w pasku ekranu głównego.
13. **Mapy** (R1, R2; pierwsza: [[cmentarze]]). Mapa nie ma własnej palety, tylko tokeny i kolory stanu:
    - **ląd** — powierzchnia; **poza krajem** — tło; **granica** — obrys, bo kształt kraju niesie położenie
      zniczy (≥ 3:1, SC 1.4.11);
    - **rzeki** i inne tło mapy — cienki obrys z przezroczystością. To dekoracja, a SC 1.4.11 obejmuje tylko
      grafikę potrzebną do zrozumienia treści. Nic, co coś znaczy, nie może mieć formy dekoracji;
    - **podpisy miast** — tekst pomocniczy ≥ 13 sp na lądzie (5,01:1), **z obwódką 2–3 dp w kolorze lądu**, żeby granica, wybrzeże i rzeki nie przecinały liter (standard kartograficzny, v1.4);
    - **znicz-pinezka** — bursztyn z sylwetką znicza w kolorze tła (8,81:1), cel dotyku ≥ 48 dp. Wybrany jest
      większy, z poświatą (reguła 2). Znicze, których cele nachodzą na siebie, łączą się w znicz z liczbą.
      **Cyfra plakietki ≥ 11 sp** i rośnie z systemowym rozmiarem tekstu — wyjątek od 13 sp, jak plakietka
      (Badge) w Material 3, bo plakietka to liczba, a nie tekst do czytania (v1.4).
      **Znicz w obrysie** (bursztynowy kontur, wnętrze w kolorze lądu) oznacza miejsce jeszcze nie zapisane,
      np. podgląd cmentarza z bazy przed dodaniem;
    - **kolory stanu** tylko z *State colours* (zieleń offline, niebieska kropka „tu jesteś” — mapa cmentarza).
14. **Zdjęcia to treść użytkownika** (v1.7, R2, R4; pierwsze: [[grob]], [[wpis-osoby]], [[cmentarz]], [[zdjecie]]):
    - **bez filtrów i tonowania** — sepia z R4 jest w samych starych zdjęciach, a nie w aplikacji. Krzyż, znicze
      i napisy na nagrobku to treść zdjęcia (reguła 8);
    - **nic na zdjęciu:** licznik, podpis i przyciski stoją obok zdjęcia, nie na nim — kontrastu tekstu na zdjęciu
      nie da się zagwarantować (SC 1.4.3);
    - **kształt mówi, co to jest:** ludzie — okrąg (miniatura w karcie 40 dp, zdjęcie w formularzu 80 dp; R3, R4);
      nagrobek — zaokrąglony prostokąt (duże zdjęcie: promień 16 dp; miniatura w karcie: kwadrat 56 dp, promień 8 dp;
      R2, R4);
    - **przycięcie tylko w miniaturze i na liście**, ze środka; całe zdjęcie, bez przycinania i z przybliżeniem —
      w podglądzie na tle;
    - **puste miejsce na zdjęcie istnieje tylko jako przycisk** (obrys, ikona w akcencie, podpis — np. „Dodaj
      zdjęcie” w formularzu osoby), nigdy jako szary prostokąt ani sylwetka (reguła 11);
    - duże zdjęcie i zdjęcie osoby w formularzu mają opis dla czytnika; miniatura w karcie nie ma, bo kartę opisuje
      jej tekst;
    - gesty na zdjęciu mają alternatywę jednym dotknięciem (*Thresholds* → gesty);
    - **usuwanie zdjęcia bez koloru błędu:** przycisk tekstowy z ikoną `delete_outline` w kolorze tekstu, a gdy
      usunięcie działa od razu — okno z bezpiecznym działaniem w akcencie (reguła 10).

## Sunlight — [[NFR-004-czytelnosc-w-sloncu]]
**Nie sprawdzone.** Test wymaga prawdziwego telefonu, buildu release i pełnego słońca
(`DEFINITION_OF_DONE.md` → wyjątki). Gdy wypadnie źle, zgodnie z NFR-004 powstaje wariant
wysokokontrastowy, bez rezygnacji ze stylu B. Wynik i data trafiają tutaj i do
[[NT-006-visual-guidelines]] → *Resolution*.

## Known gaps
- **Widoczność fokusu przycisku** (klawiatura fizyczna, sterowanie przełącznikami): domyślna nakładka
  Material 3 daje ok. 1,17:1 wobec tła, poniżej 3:1 (SC 1.4.11). Przy dotyku i TalkBacku (własna ramka)
  bez znaczenia. Wraca, gdy pojawi się taki sposób sterowania (zmierzone w pierwszym przeglądzie,
  2026-10-06).
- **Cel dotyku 48 dp przycisków** zapewnia domyślne `MaterialTapTargetSize.padded` motywu na Androidzie
  (widoczny przycisk tekstowy ma 40 dp). `shrinkWrap` obniżyłby cel do 40 dp, więc ekrany go nie używają.
- ~~**Nazwa grobu**~~ — rozstrzygnięte 2026-10-07: opcjonalne pole w schemacie, wpisywane ręcznie, bez
  wyliczania z nazwisk (decyzja autora, [[ISSUE-012-transcribe-grave-screen]]; [[grob]] D1). Bez nazwy grób
  ma tytuł „Grób”, a na liście [[cmentarz]] tytułem są osoby.
- **Ikona znicza** nie istnieje w Material Icons. Własna ikona wektorowa, jedna na całą aplikację (wersja
  liniowa i wypełniona), powstaje z [[ISSUE-014-home-map-of-poland]]; sylwetka i wersje: [[cmentarze]] →
  *Style B rules applied*.

## Changelog
- 2026-10-06 — v1 (`ui`, pierwsze uruchomienie, [[ISSUE-013-setup-ui-agent]] przy
  [[ISSUE-012-transcribe-grave-screen]]): role tokenów, progi ze źródłem, pomiar, reguły 1–10. Nowe tokeny
  obrysu i błędu zaproponowane w specyfikacji [[wpis-osoby]].
- 2026-10-06 — v1.1, po pierwszym przeglądzie `ui` (ekran startowy): forma głównego działania, etykieta
  przycisku, odstępy kompozycji wyśrodkowanych, *Known gaps*.
- 2026-10-06 — **v1.2, wyrównanie do referencji z kick-offu** ([[references]], dostarczone przez autora po
  stopie #2). v1 powstała z samego zdania briefu, bez obrazów, i rozjechała się z nimi w pięciu miejscach.
  Poprawki:
  - reguła 8 **odwrócona**: znicz to znak aplikacji, a nie symbol zakazany;
  - reguła 1: jeden *kolor* akcentu o wielu rolach zamiast „jednego bursztynowego elementu”, plus forma
    przycisków drugorzędnych i linku;
  - reguła 2: karty i delikatna poświata;
  - reguła 4: tytuły półgrube zamiast wagi 300;
  - reguła 6: lata życia i adres pełnymi słowami;
  - nowe reguły 11 (karty) i 12 (nawigacja docelowa);
  - kolory stanu (zieleń offline, niebieska kropka).
  
  Wyjątek „kreska pod nazwą jako znak marki” z v1.1 jest **zastąpiony**: znakiem marki jest znicz +
  „Grobing” (R1), a kreska znika razem z ekranem startowym ([[cmentarze]] → *Navigation*).
- 2026-10-06 — **v1.3, mapa Polski** ([[ISSUE-014-home-map-of-poland]], `ui`):
  - nowa reguła 13 (mapy): role kolorów na mapie, znicz-pinezka i znicz w obrysie (miejsce jeszcze nie
    zapisane — podgląd cmentarza z bazy, po stopie #1);
  - obrys i błąd wchodzą z ISSUE-014, która idzie przed ISSUE-012;
  - ikona znicza ma sylwetkę i dwie wersje.
- 2026-10-06 — **v1.4, po pierwszym przeglądzie mapy** (`ui` jako subagent `qa`, [[ISSUE-014-home-map-of-poland]]):
  - reguła 1: przycisk tekstowy poza oknem (akcent albo kolor tekstu);
  - reguła 13: obwódka podpisów miast; cyfra plakietki ≥ 11 sp jako wyjątek.
- 2026-10-07 — **v1.5, po przeglądzie ekranu z bazy cmentarzy** (`ui` jako subagent `qa`,
  [[ISSUE-015-add-cemetery-from-database]]): reguła 1, link zewnętrzny — strzałka „↗” to ikona `north_east`
  (znak U+2197 Android rysuje jako kolorowe emoji), ikona rośnie z tekstem, cel ≥ 48 dp rośnie, a tekst się
  zawija. Tokeny bez zmian, więc pomiar z 2026-10-06 obowiązuje (przeliczony z `theme.dart` 2026-10-07,
  wyniki te same).
- 2026-10-07 — **v1.6, po przeglądzie ekranów przepisywania** (`ui` jako subagent `qa`,
  [[ISSUE-012-transcribe-grave-screen]]): kontrolka z tekstem ma rozmiar najmniejszy i rośnie z tekstem (SC 1.4.4);
  pozycja wybrana w menu ma ikonę `check` (SC 1.4.1); przycisk tekstowy w linii treści w akcencie; nowa para w
  pomiarze — tekst na zaznaczeniu 4,60:1. Tokeny bez zmian.
- 2026-10-07 — *Known gaps*: nazwa grobu rozstrzygnięta (`ui` przed planem [[ISSUE-012-transcribe-grave-screen]]).
  Reguły i tokeny bez zmian, więc wersja zostaje v1.5.
- 2026-10-07 — **v1.7, zdjęcia** (`ui` przed planem [[ISSUE-016-photos-grave-and-person]]): nowa reguła 14 (zdjęcia
  jako treść użytkownika — bez filtrów, nic na zdjęciu, kształt według tego, co na zdjęciu, puste miejsce tylko jako
  przycisk, usuwanie bez koloru błędu) z czterech instancji naraz (zdjęcie nagrobka, miniatura w karcie osoby i grobu,
  zdjęcie w formularzu, podgląd). Nowy próg: gesty z alternatywą jednym dotknięciem (SC 2.5.1). Tokeny bez zmian,
  więc pomiar z 2026-10-06 obowiązuje; obrys pustego zdjęcia osoby to istniejąca para obrys/tło (3,40:1).
- 2026-10-07 — **v1.8, po przeglądzie ekranów zdjęcia nagrobka** (`ui` jako subagent `qa`,
  [[ISSUE-016-photos-grave-and-person]]): rola akcentu obejmuje wskaźnik działania w toku (`CircularProgressIndicator`
  dziedziczy akcent na każdym ekranie — było spójne, brakowało zapisu). Tokeny bez zmian.
