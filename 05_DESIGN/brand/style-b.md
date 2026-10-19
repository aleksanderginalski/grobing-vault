---
title: "Style B — visual guidelines (v1.48)"
type: design-guidelines
status: active
owner: ui
source: "PROJECT_BRIEF §6a (Style B, chosen by the author 2026-10-05) · references.md (R1–R4, the kick-off images) · grobing-code/lib/app/theme.dart · WCAG 2.2 · Android accessibility"
non-tech-item: "[[NT-006-visual-guidelines]]"
created: 2026-10-06
updated: 2026-10-19
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
| akcent | `GrobingColors.amber` | **jeden kolor, wiele ról** (reguła 1): główne działanie (wypełnione), pinezki, znicz, aktywna zakładka i segment, zaznaczenie, fokus, ikony działań i nagłówków sekcji, wyróżnione imiona na ścieżce, link zewnętrzny, wskaźnik działania w toku (v1.8) | treść ciągła (akapity), duże dekoracyjne plamy, ostrzeżenia i błędy, numery listy i inne ozdobniki (v1.17) |
| obrys *(nowy — wchodzi z [[ISSUE-014-home-map-of-poland]], zaproponowany przy [[ISSUE-012-transcribe-grave-screen]])* | proponowany `GrobingColors.outline` | ramka pola wpisu, przycisk z obrysem, linia podziału, granica na mapie (reguła 13) | tekst |
| błąd *(nowy — wchodzi z ISSUE-014)* | proponowany `GrobingColors.error` | komunikat błędu pod polem, jego ikona, ramka pola z błędem | cokolwiek poza błędem |
| woda *(nowa, v1.13 — [[SPIKE-004-mvp-flow-prototype]] D6, [[cmentarze]] D29)* | `GrobingColors.water` (morze, jeziora) i `GrobingColors.waterLine` (rzeki) — w `theme.dart` od [[ISSUE-023-poland-map-r1-cemetery-photo]] (v1.20) | woda na mapie Polski jak w R1 | cokolwiek poza mapą; nośnik znaczenia (to dekoracja — brzeg niesie granica) |
| relacje w drzewie *(nowa, v1.16 — [[SPIKE-004-mvp-flow-prototype]] D20, [[drzewo]] D3)* | proponowane `GrobingColors.relParentChild` (`#8FB3C9`, rodzic–dziecko) i `GrobingColors.relPartners` (`#D39BB0`, partnerzy: ciągła — małżeństwo, przerywana — razem); **do `theme.dart` wchodzą z [[ISSUE-024-person-view]]** (mini-drzewo w [[osoba]] — pierwsze użycie, v1.18) | linie relacji w drzewie i mini-drzewie; **ślad dalszej rodziny** w drzewie — te same kolory przy kryciu 60%, kreska przerywana 3/3, 14 dp ([[drzewo]] D9, v1.24) | jedyny nośnik rodzaju relacji — kształt i styl linii niosą go też (SC 1.4.1); **bez legendy** (decyzja autora, SPIKE-004 D25); cokolwiek poza liniami relacji |
| kolory rodu *(nowe, v1.33 — [[wieniec]] D6, D15)* | proponowane, 12 wartości z [[wieniec]] → *Style B rules applied* (stare złoto, brąz, miedź, srebro, kość słoniowa, grafit, patyna, oliwka, błękit, lawenda, wrzos, rubin); **do `theme.dart` wchodzą z [[ISSUE-044-family-wreaths]]** | **wyłącznie wieniec rodu** — wzór w kolorze rodu z cieniowaniem C3 (najciemniej 80% koloru) i obwódką w kolorze tła, w widoku osoby, na drzewie, w znaku wieńca w formularzu, w kole wyboru koloru | działania, tekst, wybór i fokus (to akcent); jedyny nośnik rodu — niesie go wzór i podpis „Ród: …” (SC 1.4.1); kolor dowolny spoza palety |

### State colours — beyond the accent
Poza akcentem występują tylko **kolory stanu**. Każdy pojawia się zawsze razem z ikoną albo tekstem, nigdy
sam (SC 1.4.1):

| Stan | Skąd | Kiedy wchodzi |
|---|---|---|
| błąd | czerwień złagodzona (propozycja `#E07A6F`, pomiar niżej) | ISSUE-014 |
| bezpieczne i gotowe — kopia udana, „Offline ✓” | zieleń — R2; **`GrobingColors.stateOk`** (zaproponowana w v1.14, [[cmentarz]] D10; w `theme.dart` od [[ISSUE-022-app-skeleton-tabs-people-settings]], v1.17): 8,97:1 na tle, 8,19:1 na powierzchni. Zawsze z ikoną i podpisem: `cloud_done_outlined` + „Ostatnia udana kopia” ([[ustawienia]] element 2), `offline_pin` + „Plan offline” | **kopia — ISSUE-022**; plan offline — pierwszy ekran wizyty (M7, EPIC-002) |
| „tu jesteś” | niebieska kropka — konwencja map, R2; `GrobingColors.here` (`#5EA2E6`, v1.16, w `theme.dart` od v1.23, [[cmentarz]] element 10): 6,99:1 na tle, 6,38:1 na powierzchni, z obwódką w kolorze tła i kołem dokładności (krycie 18%). **Także:** „gdzie jestem” włączony i ikona plakietki stanu lokalizacji (10a) — v1.23 | mapa cmentarza (EPIC-002); nigdy w roli akcentu i nigdy jako ostrzeżenie |

## Thresholds — with source
| Próg | Wartość | Źródło |
|---|---|---|
| kontrast tekstu | **≥ 4,5:1** | [WCAG 2.2](https://www.w3.org/TR/WCAG22/) SC 1.4.3 Contrast (Minimum), AA: *„text … has a contrast ratio of at least 4.5:1”* |
| kontrast elementów interfejsu (ramka pola, obrys przycisku, ikona, która coś znaczy) | **≥ 3:1** wobec sąsiedniego koloru | WCAG 2.2 SC 1.4.11 Non-text Contrast, AA |
| kolor jako nośnik | **nigdy jedyny**: błąd, brak, wybór i stan mają też tekst albo ikonę. Pozycja wybrana w menu ma ikonę `check` i stan „zaznaczone” dla czytnika, nie tylko akcent (v1.6) | WCAG 2.2 SC 1.4.1 Use of Color, A |
| rozmiar kontrolki z tekstem | **najmniejszy, nie stały**: przycisk, link i pole rosną z systemowym rozmiarem tekstu, zamiast ucinać napis (v1.6 — druga instancja po linku z v1.5). **Wyjątek — podpisy na mapie** (miasta, nazwa kraju): rosną z tekstem systemu najwyżej do 1,3× (v1.20, reguła 13) | WCAG 2.2 SC 1.4.4 Resize Text, AA |
| gesty | **przesunięcie i gest kilkoma palcami mają alternatywę jednym dotknięciem** (przyciski poprzednie/następne, podwójne dotknięcie zamiast rozsunięcia palców) (v1.7). **Wyjątek — oddalanie drzewa** (v1.46, [[drzewo]] D58, decyzja autora na stopie #2 [[ISSUE-049-tree-levels-and-zoom]]: *„wystarczy funkcja ręcznego zoom-in/out”*): przyciski + / − w rogu drzewa zmieniają poziom, więc drzewo oddalają tylko dwa palce; przybliżanie ma alternatywę (podwójne dotknięcie, dotknięcie małego drzewa — D52). Koszt: z czytnikiem ekranu albo Switch Access drzewa nie da się oddalić. Aplikacja jest prywatna, dla autora i rodziny — WCAG jest tu miarą, nie wymogiem. *Obali:* ktoś z rodziny nie umie oddalić dwoma palcami — wtedy oddalanie jednym dotknięciem wraca | WCAG 2.2 SC 2.5.1 Pointer Gestures, A: *„All functionality that uses multipoint or path-based gestures for operation can be operated with a single pointer without a path-based gesture”* ([Understanding 2.5.1](https://www.w3.org/WAI/WCAG22/Understanding/pointer-gestures.html)) |
| cel dotyku | **≥ 48 × 48 dp**. **Wyjątek — węzeł drzewa przy oddaleniu** (v1.24, [[drzewo]] D17; **v1.44, D52**): cel to miejsce osoby × skala drzewa — przy skali poniżej 0,6 mniej niż 48 dp. Od v1.44 oddalanie sięga całego drzewa (skala do ok. 0,1, cel ok. 8 dp), więc **poniżej 24 dp dotknięcie nie wybiera osoby, tylko przybliża w to miejsce** (do skali 0,45) — wybór osoby ma zawsze cel ≥ 24 dp (do v1.43: najmniejsza skala 0,4 trzymała cel ≥ 24 dp); dotknięcie małego drzewa przybliża do 0,45 (cel 36 dp, z wieńcem 43 dp), a podwójne dotknięcie dalej, do ≥ 48 dp (v1.46: + w rogu drzewa zmienia już poziom, [[drzewo]] D58). Węzły nie mogą rosnąć, bo drzewo przestałoby być oddalone, a pomyłka tylko przestawia środek | [Android — Make apps more accessible](https://developer.android.com/guide/topics/ui/accessibility/apps) → *Use large, simple controls*: *„at least 48dp×48dp”*. Wyjątek: [WCAG 2.2](https://www.w3.org/TR/WCAG22/) SC 2.5.8 Target Size (Minimum), AA: *„The size of the target for pointer inputs is at least 24 by 24 CSS pixels”*, z wyjątkiem *Equivalent*: *„The function can be achieved through a different control on the same page that meets this criterion”* (odczyt 2026-10-13) |
| rozmiary tekstu | treść i tekst wpisywany **≥ 16 sp**; drobny tekst pomocniczy ≥ 13 sp; etykieta przycisku 14–16 sp, waga 500. **Wyjątek — podpis zakładki w dolnym pasku: 12 sp, półgruby** (v1.17, [[cmentarze]] element 18), bo to krótka etykieta pod ikoną, a nie tekst do czytania; rośnie z systemowym rozmiarem tekstu (przy 200% mieści się w pasku 72 dp). **Wyjątek — podpis pola „Dodaj zdjęcie” w miejscu miniatury cmentarza 96 × 80 dp: 12 sp, półgruby** (v1.20, [[cmentarze]] 6a). To krótka etykieta pod ikoną w polu, które ma rozmiar miniatury, a przy 14 sp podpis nie mieści się w jednej linii. Rośnie z tekstem: przy 200% pole rośnie, a podpis przechodzi do dwóch linii. **Wyjątek — podpis źródła mapy („© OpenStreetMap”, „Ortofotomapa: GUGiK”): 11 sp, tekst pomocniczy, na małej plakietce w kolorze powierzchni** (v1.21, [[cmentarz]] v5.1). To wymagany podpis licencji, a nie treść do czytania przy grobie; rośnie z tekstem systemu | decyzja projektowa (nie norma) — dane wpisuje się szybko i trzeba je odczytać bez mrużenia oczu. Wyjątek: podpis zakładki w pasku nawigacji Material 3 to *label medium*, 12 sp (Flutter 3.41.1, `material/navigation_bar.dart` → `_NavigationBarDefaultsM3` używa `labelMedium`; `material/typography.dart` → `_M3Typography`: `labelMedium` 12.0, w500 — sprawdzone w SDK 2026-10-08) |
| **tekst dla telewizora** (tryb prezentacji, od v1.30) | to, co rodzina ma przeczytać z kanapy (rok historii): **≥ 36 sp** i **≥ 48 dp od bocznych krawędzi**; rośnie z tekstem systemu najwyżej do 1,3× (jak podpisy na mapie, reguła 13 — napis już jest duży i stoi na drzewie). Pomiar: telefon poziomo wypełnia szerokość telewizora 16:9, więc 36 sp ma z 3 m 23′ (32″) – 46′ (65″), a 13 sp tylko 8–17′ ([[drzewo]] *Candidates — ISSUE-038*). **Zdania** (v1.47 — podpis roku po ⏭, [[drzewo]] 6a): **≥ 28 sp** (M3 *headline medium*), tak samo najwyżej 1,3× z tekstem systemu i 48 dp od bocznych krawędzi — z 3 m 18′ (32″) – 36′ (65″); 24 sp (*headline small*) ma na 32″ tylko 15′, a 36 sp zostaje dla liczb i krótkich napisów, bo kilka linii zdań w 36 sp zakryłoby pół telewizora ([[drzewo]] *Candidates — ISSUE-050*). **v1.48: próg dla zdań nie ma dziś instancji** — podpis roku zszedł na listwę jako linia 14 sp czytana z telefonu ([[drzewo]] D72). Sterowanie dla osoby z telefonem (listwa, „Zakończ prezentację”) — progi telefonu | czytelność: ISO 9241-3xx, wysokość znaku zwykle 20–22′, min. 16′ (za [listą CSS W3C](https://lists.w3.org/Archives/Public/public-css-archive/2020Jun/0612.html)); skala: [Android TV → Typography](https://developer.android.com/design/ui/tv/guides/styles/typography) (display small 36 sp — *„reserved for short, important text passages, or numerals”*); margines: [Android TV → Layouts](https://developer.android.com/design/ui/tv/guides/styles/layouts) — *„a 5% margin of 48dp on the left and right sides”* (odczyt 2026-10-14; [[drzewo]] D38); zdania: skala M3 we Flutterze 3.41.1 — `material/typography.dart` → `_M3Typography`: `headlineMedium` 28.0, `headlineSmall` 24.0, `displaySmall` 36.0 (sprawdzone w SDK 2026-10-19) |
| **ekrany wizyty** (od v1.21) | **≥ 7:1** dla tekstu czytanego przy grobie (adres, liczby, stan planu); w tekście pomocniczym tylko to, czego nie czyta się przy grobie | WCAG 2.2 SC 1.4.6 Contrast (Enhanced), AAA. **Miara [[NFR-004-czytelnosc-w-sloncu]]** — decyzja autora 2026-10-12 (W2, stop #1 [[ISSUE-027-cemetery-map-plan-photo-states]]); pierwszy ekran: [[cmentarz]] v5. Test w słońcu — przy instalacji MVP |

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
| zieleń stanu `stateOk` jako ikona albo tekst *(v1.17, 2026-10-08)* | 8,97 | 8,19 | 3 (ikona) · 4,5 (tekst) | ✅ |
| napis „Polska” — tekst pomocniczy, krycie 85%, 22 sp półgruby *(v1.20, 2026-10-12)* | — | 3,98 na lądzie · 4,02 na wodzie | 3 (duży tekst, SC 1.4.3) | ✅ |
| granica sąsiada — obrys, krycie 45% *(v1.20)* | 1,61 · na wodzie 1,59 | — | dekoracja (poza SC 1.4.11) | — |
| linia kwatery — tekst, krycie 75% *(v1.22, 2026-10-12)* | 6,56 | 6,16 | 3 (SC 1.4.11) | ✅ |
| kwatera wybrana (akcent) wobec linii kwatery *(v1.22)* | — | 1,31 (między sobą) | — | wybór niesie też grubość i nazwa (SC 1.4.1) |
| ślad dalszej rodziny — rodzic–dziecko · partnerzy, krycie 60% *(v1.24, 2026-10-13)* | 3,75 · 3,66 | — | 3 (SC 1.4.11) | ✅ — kształt (przerywana 3/3, krótka) odróżnia ślad od linii, nie tylko kolor (SC 1.4.1) |
| przerywany obrys węzła — data niepewna na suwaku czasu, obrys *(v1.29, 2026-10-14, [[drzewo]] D32)* | 3,40 | — | 3 (SC 1.4.11) | ✅ — niepewność niesie kształt (kreska 4/3), nie krycie: imię zostaje tekstem na tle 10,98:1 |
| kolory rodu — wieniec, najsłabszy z 12 (brąz): płaski · C3, najciemniejsze 5% liści *(v1.33, 2026-10-17, [[wieniec]] D15)* | 4,46 · 3,10 | 4,07 · — | 3 (SC 1.4.11) | ✅ — obwódka w kolorze tła sprawia, że liść zawsze sąsiaduje z tłem, także na powierzchni i na zdjęciu; pełna tabela: [[wieniec]] |

**Wniosek:** wszystkie pary spełniają AA, a tekst pomocniczy nie spełnia 7:1. **Ekrany wizyty przyjęły 7:1** (v1.21, W2,
2026-10-12): informacja potrzebna na cmentarzu (adres kwatery, liczby, stan planu) jest w kolorze tekstu, a token pomocniczy
zostaje bez zmian.

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

   **Wyjątek — wieniec rodu** (v1.33, [[wieniec]] D6): wieniec ma kolor rodu z palety 12 kolorów (*Token roles*), a nie akcent. To drugi kolor
   obok akcentu, ale tylko w tej jednej roli; pierścień portretu, wybór i działania przy wieńcu zostają w akcencie.
2. **Głębia subtelna:** tło → powierzchnia (zaokrąglone karty, promień 12–16 dp, i dolny arkusz). Głównemu
   przyciskowi i zaznaczonemu elementowi (wybrana pinezka, węzeł na ścieżce) wolno mieć **delikatną
   bursztynową poświatę**. Bez twardych cieni i bez gradientów tła. **Poświata leży pod okręgiem, nie na nim** — nad
   okręgiem leży tylko pierścień (v1.27): poświata nad okręgiem zabarwiała go (znak „Ja” spadał poniżej 4,5:1, zdjęcie dostawało
   odcień — reguła 14). Trzy instancje: osoba w środku drzewa, w mini-drzewie i portret osoby (przegląd `ui` [[ISSUE-033-tree-from-a-person]]).
   **Wieniec rodu ma głębię wpieczoną w obraz** (v1.33, [[wieniec]] D15): przejście tonu jak gałązki w R4 i tłoczenie liści, liczone raz przy
   budowie z obrazu wzoru. To nie gradient tła i nie rozmyty cień rysowany w każdej klatce — tych przy ok. 100 węzłach drzewa nadal nie ma.
   **Osoby z podpisu roku po ⏭ świecą** (v1.48, [[drzewo]] D73, [[mapa-migracji]] D30 — prośba autora na stopie #2 [[ISSUE-050-next-event]]): pierścień w akcencie i
   poświata pod okręgiem, a przy wieńcu rodu pod wieńcem; przy ślubie i „razem” także linia pary w akcencie. Jedyna **pulsująca** poświata: trzy pulsy po 1,2 s (krycie 0,30 → 0,65),
   potem stała 0,30 — ruch kończy się przed 5 s ([SC 2.2.2](https://www.w3.org/TR/WCAG22/#pause-stop-hide)), poniżej 3 zmian na sekundę
   ([SC 2.3.1](https://www.w3.org/TR/WCAG22/#three-flashes-or-below-threshold)), przy ograniczeniu animacji od razu stała (SC 2.3.3). Poświata leży pod osobami na **jednej warstwie**
   (kilka osób naraz, nie cień w każdym węźle) i przy oddaleniu ma na ekranie stałą wielkość, jak imię.
3. **Ikony cienkie, w dwóch tonach** (v1.38, [[ISSUE-046-icons]] decyzje 1–3 autora, 2026-10-18 — kierunek z arkusza DALL-E: *„to jest kierunek, w
   który chcę iść”*): **Material Symbols, końce zaokrąglone (Rounded), grubość 300**, i **wypełnienie 25%** — ten sam glif wypełniony, w kolorze ikony przy
   kryciu 25%, pod glifem z kreską (`GrobingIcon`). Wypełnienie jest dekoracją: znaczenie i kontrast ≥ 3:1 niesie kreska. Metafory z arkusza tam, gdzie mówią
   więcej niż ogólny kształt: poprawa to **pióro** (`ink_pen`), dodanie zdjęcia to **zdjęcie z krajobrazem** (`add_photo_alternate`), drzewo to **drzewo
   liściaste** (`nature`) — nie schemat i nie iglaste (reguła 8). Ikona jest w kolorze tekstu pomocniczego, a **w akcencie wtedy, gdy oznacza działanie albo
   nagłówek sekcji** (R4: „Rodzina”, „Dodaj osobę”). Ikona, która niesie znaczenie, ma podpis albo `tooltip`. **Ikona obok tekstu rośnie z tekstem** (przyciski,
   nagłówki sekcji, wiersze); pasek ekranu i dolne zakładki zostają 24 dp (decyzja 2). **Stałe 24 dp są też** (v1.39, przegląd `ui`, odstępstwo 3 `dev`):
   przełącznik widoku „Drzewo | Mapa” (stoi w pasku jak zakładki, a przy dużym tekście zostają w nim same ikony), przyciski z samą ikoną (`IconButton`,
   okrągłe przyciski mapy i drzewa) i ikony w pudełkach o stałym rozmiarze (miniatura, portret, miejsce na zdjęcie, kafelek dodawania). Znicz
   (`CandleIcon`) zostaje własną ikoną, z kreską 1,5.
   **Skąd glify** (v1.39, odstępstwa 1 i 2 `dev`): własny font ikon `grobing-symbols.ttf`, wycięty z Material Symbols Rounded razem z podmianami osi FILL — pakiet
   `material_symbols_icons` po wycinaniu ikon przez Fluttera gubił część glifów (`group`, `settings` puste). Grubość 300 to jedna stała `GrobingIcon.weight`,
   więc zmiana na 400 (*Obali* w *Candidates — ISSUE-046*, słońce) to jedna linia.
   **Dziewięć ikon z arkusza autora** (v1.40, [[ISSUE-046-icons]] decyzja 1' na stopie #2 — *„chciałem te »odpicowane«”*): zakładki Mapa, Osoby, Drzewo,
   lupa, ustawienia, dodaj zdjęcie, pinezka ze zniczem, pióro, telewizor to rysunki z arkusza DALL-E autora (mapa z trasą, rodzina z dzieckiem, drzewo z kropkami,
   zdjęcie z krajobrazem, pinezka ze zniczem, stalówka, telewizor z drzewem) — przerysowane do wektora w tym samym foncie (linie i wypełnienie jako dwa glify),
   w tych samych rolach kolorów i rozmiarach. Pozostałe ikony (strzałki, ✕, ✓, „›”, kalendarz, nagłówki sekcji spoza arkusza…) zostają z Material Symbols.
   Autor zna koszt: przy 24 dp najdrobniejsze detale rysunków się zlewają. Nowa ikona „ważna” (zakładka, główne działanie) — najpierw arkusz w tym stylu.
   **Grubość linii arkusza** (v1.41, przegląd `ui` rundy 4): przy 24 dp rysunek miał 0,6–0,75 dp kreski wobec 1,5 dp Material przy 300 — linie są poszerzone
   o ≈ 0,3 dp (`THICKEN` w `tool/icons/build_symbols.py`; więcej zlewa koronę drzewa). Glify z arkusza są statyczne — `GrobingIcon.weight` ich nie zmienia,
   więc w słońcu (NFR-004) dźwignią jest `THICKEN` i przebudowa fontu. Pinezki informacyjne (adres grobu, poprawa pinezki, brak lokalizacji) zostają z Material.
   ~~Warianty `outlined` z Material Icons~~ (do v1.37).
4. **Krój:** systemowy bezszeryfowy (Roboto na Androidzie), bez własnych krojów tekstu w aplikacji (font ikon z reguły 3 to ikony, nie krój —
   v1.39). **Tytuły i
   imiona półgrube (waga 500–600)**, jak w R1–R4. Treść ma wagę regularną. Krój szeryfowy z R2 był
   przypadkiem generatora i nie obowiązuje.
5. **Odstępy:** siatka 8 dp. Na ekranach z listą albo formularzem margines boczny 16 dp, odstęp między
   grupami 24 dp, wewnątrz grupy 8–12 dp, a między kartami 8 dp. Kompozycje wyśrodkowane (pusty stan,
   nagłówek osoby z R4) biorą większe odstępy z tej samej siatki.
   **Stała szerokość zmiennego napisu** (v1.31): napis, którego wartość się zmienia, a obok stoi kontrolka do przeciągania
   (rok przy suwaku, nazwa tempa), ma szerokość najszerszej ze swoich wartości w tym samym kroju i skali tekstu. Inaczej
   suwak zmienia długość przy każdej zmianie napisu, a uchwyt ucieka spod palca. Dwie instancje: rok w karcie drzewa (v1.13,
   znalezione na emulatorze w [[ISSUE-037-time-on-the-tree]]) i przycisk tempa ([[ISSUE-038-history-on-tv-and-tempo]]; [[drzewo]]
   element 6).
6. **Formaty po polsku:**
   - lata życia: `1921–1987`, a z dopiskiem `ok. 1890 – 14.03.1951` (spacje wokół kreski, gdy którakolwiek
     strona ma więcej niż sam rok);
   - daty: `14.03.1951`, `03.1951`, `1890`; dopiski: `ok. 1890`, `przed 1920`, `po 1945`, `między 1893 a 1895`;
   - nazwisko rodowe w tej samej linii co nazwisko: `Maria Nowak z d. Kowalska`;
   - adres pełnymi słowami: `Kwatera B · Rząd 4 · Miejsce 12`; liczby: `6 grobów · 14 osób`, `3 osoby`
     (z odmianą);
   - **twarda spacja (U+00A0) po jednoliterowych słowach** (a, i, o, u, w, z) w stałych tekstach aplikacji i w „z d.”
     w nazwie osoby (`z d. Rodowe`), żeby słowo nie zostało samo na końcu linii (polska zasada składu)
     (v1.17; instancje z przeglądu [[ISSUE-022-app-skeleton-tabs-people-settings]]: „…na papierze, u⏎rodziny” w
     ustawieniach, „Na⏎kartce”, „w⏎środku”, „i⏎zdjęciami” w notce przekazania). **Kod jeszcze tej reguły nie
     stosuje** — obejmuje całą aplikację i `personName`, więc wejdzie osobną drobną pozycją, a nie w ISSUE-022.
     **Nowe stałe teksty stosują ją od razu** (przegląd [[ISSUE-039-connect-two-people]] i [[ISSUE-042-places-of-residence]]);
   - **linia nie kończy się separatorem ani dopiskiem** (v1.32): po „·” w linii złożonej z części stoi twarda spacja, więc linia
     łamie się **przed** „·” („Wymyślowo⏎· woj. testowe”), nigdy po nim; dopisek przed rokiem albo nazwą („ok.”, „od”, „do”,
     „dziś”) trzyma się następnego słowa, a lata okresu łamią się tylko za „–” („ok. 1930 –⏎ok. 1945”). Dwie instancje: linia
     miejscowości w bazie cmentarzy ([[cmentarze]] D25) i lata oraz linie miejsca zamieszkania ([[zamieszkanie]] v1.1 — zobaczone na
     emulatorze w [[ISSUE-042-places-of-residence]]: „ok.” na końcu linii w kolumnie 112 dp, „·” na końcu linii przy tekście 200%).
7. **Ton tekstów:** spokojny i rzeczowy. Bez wykrzykników, bez „Sukces!”, bez emotikonów. Brak czegoś
   opisujemy faktem i tym, kiedy się uzupełni („Bez adresu kwatery · uzupełnisz przy wizycie”), a nie
   ostrzeżeniem.
   **Kto mówi** (v1.28, [[drzewo]] D28 — G2, decyzja autora 2026-10-14). Aplikacja zwraca się do Ciebie: pyta, zaprasza, wyjaśnia („Wybierz, która
   osoba to Ty”, „Nie wiadomo jeszcze, jak łączy się z Tobą — …”). **Nazwa pokrewieństwa** jest etykietą z Twojego punktu widzenia, więc mówi Twoim
   głosem: „Moja babcia”, „Siostra cioteczna babci mojej żony”, „to ja”, „nie wiadomo jeszcze, kim jest dla mnie”. Tak samo pytanie zadawane przez
   Ciebie, np. nagłówek „Jak łączy się ze mną”. W jednym miejscu jeden głos: linia pod imieniem w karcie drzewa jest cała w pierwszej osobie.
   „Mój” piszemy małą literą, chyba że zaczyna nazwę. Źródło: [Microsoft Writing Style Guide → Person](https://learn.microsoft.com/en-us/style-guide/grammar/person)
   (odczyt 2026-10-14): *„In general, use second-person pronouns (you, your)”*; *„First-person singular pronouns can be used in product UI to show
   someone's control”*; *„it's OK to use "my" in navigation or filter labels if you need to distinguish a person's content”*. W genealogii FamilySearch
   pisze „My Grandmother” ([[drzewo]] D8).
8. **Znicz to znak aplikacji** (R1–R3). **Rysunek znicza** (v1.42, [[ISSUE-046-icons]], stop #2 — autor: *„te trzy … dlaczego nie zmieniłeś”*): znicz autora
   z DALL-E, ten sam znak co ikona aplikacji L1 — w dwóch tonach w logo i na przyciskach, pełny z wyciętymi detalami w pinezce (kropla z kodu, czubek co do
   piksela) i w znaczniku zmarłych w drzewie; przerysowany do fontu ikon (`Glyphs.candle`, `Glyphs.candleSolid`). **Pinezka ze zniczem z arkusza autora** (v1.41) to pinezka aplikacji — także na przyciskach, które stawiają nową
   pinezkę („Dodaj cmentarz”, „Dodaj ten cmentarz”, „Dodaj ręcznie”, „Postaw pinezkę”); „Zapisz” i inne „Dodaj” dalej znicza nie mają. Występuje w **ikonie aplikacji** (v1.38, [[ISSUE-046-icons]] decyzja 4 autora: znicz L1 z DALL-E w dwóch tonach,
   akcent na tle `grobing_background`, warstwa jednobarwna z samych linii), w logo (znicz + „Grobing”), w pinezce (znicz w kształcie
   pinezki), na głównym działaniu prowadzącym do miejsca pamięci („Otwórz cmentarz”, „Pokaż grób”) i jako
   znacznik osoby zmarłej (węzeł drzewa, R3). **Znicz oznacza miejsce i pamięć**, a nie zwykłe działania:
   „Zapisz” i „Dodaj” go nie mają. **Krzyż ani inne symbole religijne nie pojawiają się w interfejsie** —
   są tylko na zdjęciach, czyli w treści użytkownika (R4). ~~Gałązki wokół portretu (R4, osoba) to opcja
   widoku osoby, rozstrzygana przy tym ekranie.~~ ~~**Rozstrzygnięte (v1.15, [[osoba]] D3): bez gałązek**~~ — zamiast nich
   zdjęcie w tle, jak na Facebooku (decyzja autora, [[SPIKE-004-mvp-flow-prototype]] D17). **v1.33 (decyzja autora na prototypie,
   [[wieniec]] D5): gałązki wracają jako wieniec rodu** wokół portretu i na węźle drzewa, obok zdjęcia w tle. Wzory to rośliny bez
   znaczenia religijnego: bez palmy, ciernia, lilii, oliwki i winorośli, bez gałązek iglastych (materiał wieńców pogrzebowych — „bez ponurości”).
9. **Puste stany** mówią, co tu będzie, i dają jedno działanie. Bez ilustracji.
10. **Potwierdzenia ciche:** zapis kończy się widokiem tego, co zapisano, a nie komunikatem w okienku.
    Okno dialogowe tylko wtedy, gdy coś może przepaść (niezapisany wpis).
11. **Listy jako karty:** element, który prowadzi dalej (osoba, grób, cmentarz), to karta na powierzchni z
    chevronem „›”. Miniatura zdjęcia z lewej, gdy zdjęcie jest ([[US-005-zdjecia]]). **Bez zastępczych
    obrazków**: brak zdjęcia oznacza brak miniatury. **Wyjątek — chip relacji** (v1.11, R4 prawy, [[wpis-osoby]]
    9a): osoba w sekcji „Rodzina” to chip „Partner: Jan” z ikoną osoby w akcencie, bez chevronu. Prowadzi do **widoku**
    tej osoby (reguła 15; do v1.17 — do jej wpisu), więc ma obrys (granica na tle 3,40:1), cel dotyku 48 dp i opis dla
    czytnika kończący się „— otwórz” (v1.18).
    Chip stoi tylko tam, gdzie osób jest kilka obok siebie; lista osób dalej składa się z kart.
12. **Nawigacja docelowa** ([[references]] → *Target app structure*): dolny pasek Mapa · Osoby · Drzewo
    (aktywna zakładka ma ikonę, podpis i podkreślenie w akcencie). Pojawia się, gdy istnieją co najmniej dwa
    z tych celów. Ustawienia, w tym „Stan danych”, są pod kołem zębatym w pasku ekranu głównego.
    **Potwierdzone na prototypie (v1.12, [[SPIKE-004-mvp-flow-prototype]] D1–D2, autor 2026-10-08):**
    - zakładki i koło zębate zostają jak w R1;
    - **pasek jest widoczny na ekranach do oglądania** (mapa Polski, cmentarz, grób, osoba, listy, drzewo), a ekran
      otwarty z zakładki zostawia ją aktywną (cmentarz → Mapa);
    - **pasek jest ukryty w formularzach, oknach i trybach wyboru** (wpis osoby, arkusz rodziny, wyszukiwanie,
      wskazanie punktu) **i na zdjęciu na pełnym ekranie** (podgląd, kadr). Tam liczy się jedno zadanie, a powrót
      daje „wstecz”;
    - **każda zakładka szuka swojego** (D3): wyszukiwarka na mapie szuka tylko cmentarzy, a osób — zakładka Osoby.
      To odstępstwo od R1 („Szukaj osoby lub cmentarza”).

    **Zbudowane w [[ISSUE-022-app-skeleton-tabs-people-settings]] (v1.17):**
    - **ustawienia nie są zakładką**, więc lista ustawień i wszystkie ekrany pod nią (wybór „ja”, notka, eksport,
      odtworzenie, „Stan danych”) są bez paska;
    - **mapa zawsze leży na dole stosu** (stały ekran startowy Androida): wstecz z ekranu głównego innej zakładki wraca
      na mapę, a z mapy zamyka aplikację; zakładka kładzie swój ekran bez wsuwania; zakładka na swoim ekranie nic nie
      robi; otwarta klawiatura zakrywa pasek ([[cmentarze]] D31);
    - **zakładka, której ekranu jeszcze nie ma, prowadzi do zaślepki** z tekstem, kiedy ekran powstanie (Drzewo do
      SPIKE-002; decyzja autora, ISSUE-022 D1 = A). Zaślepka jest tymczasowa i **nie jest wzorem pustego stanu**: duża
      ikona w kolorze obrysu i numer pozycji w tekście łamią reguły 3 i 9, a przyjęto je tylko dlatego, że zaślepka
      znika razem z prawdziwym ekranem.
13. **Mapy** (R1, R2; pierwsza: [[cmentarze]]). Mapa nie ma własnej palety, tylko tokeny i kolory stanu:
    - **ląd** — powierzchnia; **poza krajem** — tło; **granica** — obrys, bo kształt kraju niesie położenie
      zniczy (≥ 3:1, SC 1.4.11);
    - **mapa Polski jak R1** (v1.13, [[cmentarze]] D29): **sąsiednie kraje** w kolorze tła z granicami w kolorze obrysu
      (krycie 45%, dekoracja); **morze i jeziora** — woda; **rzeki** — linia wody. **Granica Polski** w kolorze tekstu
      pomocniczego, bo obrys ma na wodzie tylko 3,11:1, a tekst pomocniczy 5,04:1 (na tle 5,50:1, na lądzie 5,01:1).
      Woda i ląd mają tę samą jasność (1,00:1), więc brzeg niesie granica, a nie kolor (SC 1.4.1). Napis kraju —
      tekst pomocniczy, 22 sp, półgruby, odstęp liter 2, **tylko przy najmniejszych przybliżeniach** (v1.20: do +2 kroków;
      nazwa kraju nazywa całość). **Brzegi morza u sąsiadów i brzegi jezior bez linii** — to dekoracja, a znaczenie niesie
      tylko granica Polski (v1.20, [[cmentarze]] D32);
    - **podpisy na mapie rosną z tekstem systemu najwyżej do 1,3×** (v1.20, [[cmentarze]] D32; miasto przy 200% = 17 sp).
      Podpis jest przypięty do punktu na mapie i nie może się odsunąć, więc w 200% podpisy zachodziłyby na siebie i na
      znicze — to też utrata treści (SC 1.4.4). Treść, która coś znaczy (nazwy cmentarzy), rośnie w pełni w arkuszu i w
      wyszukiwarce. Znacznik podpisu ma wysokość podpisu w tej skali, żeby nie ucinał liter;
    - **imiona w drzewie przy oddaleniu** (v1.25, [[drzewo]] v1.6 — I2, decyzja autora na stopie #1 [[ISSUE-033-tree-from-a-person]]; potwierdzona
      na stopie #1 [[ISSUE-035-tree-names-shrink-my-voice]], 2026-10-14 — [[drzewo]] D27):
      ta sama zasada co podpisy na mapie. Imię nie maleje z drzewem poniżej 13 sp × skala tekstu, stoi na **tabliczce w kolorze tła**
      (zaokrąglona 4 dp, 3 dp z boków — v1.26), a z nakładających się zostaje to bliżej osoby w środku; reszta wraca po przybliżeniu. Mniej
      imion, ale każde czytelne. **Tabliczka zamiast obwódki liter tylko na jednolitym tle** (v1.26, [[drzewo]] D23): na tle drzewa wygląda tak
      samo i tak samo przerywa linie, a rysuje się bez rozmytych cieni, które przy ok. 100 imionach szarpały ruch. Na mapie tło się zmienia
      (ląd, woda, granica, zdjęcie z góry), więc tam obwódka zostaje wokół liter. **Osoba z widocznym imieniem leży nad sąsiadami** (v1.45, [[drzewo]]
      v1.24 — odstępstwo 2 [[ISSUE-049-tree-levels-and-zoom]]): przy całym drzewie imię jest szersze niż kilka okręgów, więc tabliczka zakrywa okręgi
      pod sobą, a nie okręgi — litery imienia (na emulatorze cięły „Wiktoria”, „Stanisław”). Podpis jest ważniejszy niż to, co pod nim, jak na mapie;
    - **plan cmentarza** (v1.14, [[cmentarz]] D10, D13): teren cmentarza — powierzchnia z obrysem; alejki — obrys
      (główne 4 dp, boczne 2 dp); **kwatera autora** — przerywana linia w kolorze tekstu (krycie 75%) z nazwą 12 sp,
      półgrubą, z obwódką w kolorze tła planu. Linia kwatery to granica zaznaczona przez autora, więc niesie znaczenie:
      tekst na powierzchni 10,02:1. Zdjęcie z góry to treść z zewnątrz (reguła 14 — nic na nim poza zniczami, nazwami
      kwater z obwódką i plakietkami na powierzchni);
    - **kwatera wybrana i rysowana** (v1.22, [[cmentarz]] v6, D28): strefa **bez wypełnienia** (akcent nigdy jako plama).
      Wybrana — linia 2,5 dp i nazwa w akcencie; wybór niesie też grubość i nazwa w arkuszu, bo akcent i linia kwatery różnią
      się tylko o 1,31:1 (SC 1.4.1). Rysowana — rogi (koło 14 dp w akcencie z obwódką 2 dp w kolorze tła) i boki (2,5 dp w
      akcencie na linii 5 dp w kolorze tła), bok zamykający przerywany. Linia pod spodem w kolorze tła daje 8,81:1 na każdym
      tle, także na zdjęciu (jak pierścień kadru, reguła 14). Stara strefa przy rysowaniu od nowa — przerywana linia w kolorze
      tekstu pomocniczego (w kolorze obrysu znikała wzdłuż alejek — przegląd ISSUE-028). **Strefy na zdjęciu z góry** leżą na linii
      w kolorze tła (3,5 dp, pod wybraną 5 dp), tak jak rysowana strefa. **Celownik** (K1 — wybór autora na stopie #1 [[ISSUE-028-cemetery-sectors]]): krzyż i koło w kolorze tekstu, 1,6 dp, z obwódką w
      kolorze tła;
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
    - **mapa świata** (v1.34, [[mapa-migracji]], decyzje autora na stopie #1 [[ISSUE-045-migration-map]]): **ląd** — powierzchnia, **morze** — woda, **granice
      i brzegi** — obrys przy kryciu 70% (2,17:1, dekoracja: ląd i woda mają tę samą jasność, a znaczenie niosą osoby). **Bez podpisów miejsc i bez nazw
      krajów** (v1.35, decyzja autora 2026-10-17, [[mapa-migracji]] D18: *„wystarczą awatary i kontury krajów”*): kraj rozpoznaje się po konturze, a gdzie kto
      jest, mówi słowami karta osoby w środku i czytnik ekranu. Z tekstu na mapie zostają liczby („+N”, pigułka). **Osoba to okrąg** (profilowe albo inicjały,
      32 dp, obrys), a nie pinezka: znicz zostaje znakiem grobu na mapie Polski i cmentarza, a na mapie świata grobów nie ma (K2). **Stosy osób, które leżałyby na
      sobie, łączą się w jeden stos z „+N”**, a dotknięcie przybliża do ich miejsc (v1.35, [[mapa-migracji]] D19) — jak znicze z liczbą wyżej. **Miejsce znane
      tylko do kraju** stoi w punkcie nazwy kraju, bez obszaru i bez zaznaczonej granicy — niepewność mówi słowo „cały kraj” w karcie i w czytniku (O3). **Ruch**
      (przeprowadzka) — sam przejazd okręgu, **bez śladu i bez innego efektu** (v1.36, decyzja autora 2026-10-17, [[mapa-migracji]] D25).
      Przerywany obrys okręgu znaczy tylko niepewną datę, jak w drzewie.
14. **Zdjęcia to treść użytkownika** (v1.7, R2, R4; pierwsze: [[grob]], [[wpis-osoby]], [[cmentarz]], [[zdjecie]]):
    - **bez filtrów i tonowania** — sepia z R4 jest w samych starych zdjęciach, a nie w aplikacji. Krzyż, znicze
      i napisy na nagrobku to treść zdjęcia (reguła 8);
    - **nic na zdjęciu:** licznik, podpis i przyciski stoją obok zdjęcia, nie na nim — kontrastu tekstu na zdjęciu
      nie da się zagwarantować (SC 1.4.3). **Jedyny wyjątek: ramka kadru** (v1.10, [[kadr-profilowego]]), bo ekran
      kadru wybiera część zdjęcia. Ramka nie ma tekstu: pierścień 2 dp w akcencie, z obu stron linia 1 dp w kolorze tła
      (akcent–tło 8,81:1 na każdym zdjęciu; sam akcent na białym ok. 2,1:1), poza okręgiem zdjęcie przyciemnione kolorem
      tła (krycie 72%), linie pomocnicze w kolorze tekstu (krycie 60%) z cieniem w kolorze tła (krycie 50 %). **Drugi wyjątek
      — zaznaczanie kwatery na zdjęciu z góry** (v1.22, [[cmentarz]] 18): rogi, boki i celownik, bo ten tryb też wybiera
      część zdjęcia. Tekstu nie ma, poza nazwą kwatery z obwódką. Każda linia leży na linii w kolorze tła (reguła 13);
    - **kształt mówi, co to jest:** osoba — okrąg, i to tylko jej **profilowe** (miniatura w karcie i w wierszu ustawień
      40 dp — v1.17, [[ustawienia]] element 1; zdjęcie w formularzu 80 dp, nagłówek bazy zdjęć 96 dp; R3, R4); nagrobek — zaokrąglony prostokąt (duże zdjęcie: promień
      16 dp; miniatura w karcie: kwadrat 56 dp, promień 8 dp; R2, R4); **cmentarz** — zaokrąglony prostokąt
      (miniatura w arkuszu cmentarza 96 × 80 dp, promień 12 dp; R1; v1.13, [[cmentarze]] D28); **zdjęcie w tle osoby** —
      prostokąt na pełną szerokość, 140 dp, bez zaokrąglenia, przycięty ze środka, a portret nachodzi na jego dolną
      krawędź (v1.15, [[osoba]] D3); **zdjęcia w bazie zdjęć osoby** — kwadraty w
      siatce, promień 8 dp, bo bywają grupowe, a okrąg ucina najwięcej (v1.9, [[zdjecia-osoby]]);
    - **przycięcie tylko w miniaturze, na liście i w siatce**, ze środka; całe zdjęcie, bez przycinania i z
      przybliżeniem — w podglądzie na tle. **Okrąg profilowego pokazuje kadr łącza osoba–zdjęcie** (v1.10,
      [[kadr-profilowego]]), a bez kadru — największy kwadrat ze środka. Każdy przyszły okrąg profilowego (widok osoby
      R4, węzeł drzewa R3) też;
    - **stan zdjęcia (np. „profilowe”) nie jest znacznikiem na zdjęciu:** niesie go miejsce (nagłówek, pierwsza
      pozycja), tekst obok albo opis dla czytnika (v1.9);
    - **puste miejsce na zdjęcie istnieje tylko jako przycisk** (obrys, ikona w akcencie, podpis — np. „Dodaj
      zdjęcie” w formularzu osoby), nigdy jako szary prostokąt ani sylwetka (reguła 11);
    - duże zdjęcie i zdjęcie osoby w formularzu mają opis dla czytnika; miniatura w karcie nie ma, bo kartę opisuje
      jej tekst;
    - gesty na zdjęciu mają alternatywę jednym dotknięciem (*Thresholds* → gesty);
    - **tło osoby wybiera się z pasma w widoku osoby** („Zdjęcie w tle”, [[zdjecia-osoby]] v1.4) albo w podglądzie („Ustaw jako
      tło”, [[zdjecie]] v1.5); jego stan niesie podtytuł podglądu („Zdjęcie w tle”) — jak profilowe, bez znacznika na zdjęciu
      (v1.18). **Zaznaczone zdjęcie w siatce** ma ramkę wokół, nie na zdjęciu: 2 dp akcentu, 2 dp tła, zdjęcie mniejsze w środku
      (v1.19). **Profilowe wybiera się z portretu** w widoku osoby („Zdjęcie profilowe”, [[zdjecia-osoby]] v1.5, v1.43) tym samym wzorcem: siatka,
      obecny wybór w ramce, dotknięcie wybiera; ta sama ramka zaznacza kilka zdjęć naraz w [[zdjecia-w-aplikacji]];
    - **wyjątek — pasmo tła bez zdjęcia** ([[osoba]] D21, decyzja autora: „zwykłe tło”): powierzchnia z samą ikoną w akcencie
      (z `tooltip`), bez obrysu i podpisu — całe pasmo jest przyciskiem (v1.19). **Ten sam wyjątek — okrąg z inicjałami w widoku osoby**
      (v1.43, [[osoba]] v2.9): okrąg z obrysem i plakietką 32 dp z ikoną dodawania w akcencie, z `tooltip`, bez podpisu — cały okrąg jest
      przyciskiem; na portrecie ze zdjęciem plakietki nie ma (nic na zdjęciu);
    - **wieniec rodu nad zdjęciem w tle** (v1.33, [[wieniec]] A5): górne liście wchodzą na pasmo, więc każdy liść ma obwódkę w kolorze tła
      (0,75% płótna, 1,5 dp w widoku osoby) — jak ramka kadru. Tekstu na zdjęciu dalej nie ma;
    - **usuwanie zdjęcia bez koloru błędu:** przycisk tekstowy z ikoną `delete_outline` w kolorze tekstu, a gdy
      usunięcie działa od razu — okno z bezpiecznym działaniem w akcencie (reguła 10).
15. **Widok przed poprawą** (v1.12, [[SPIKE-004-mvp-flow-prototype]] D4, autor 2026-10-08: *„ok”*). Dotknięcie
    cmentarza, grobu albo osoby **otwiera widok**, a poprawa jest pod ✎ (`edit_outlined` w akcencie, `tooltip`
    „Popraw …”), jak w arkuszu cmentarza ([[cmentarze]] element 8) i w tytule grobu ([[grob]]). Formularz otwiera się
    od razu tylko przy działaniu „Dodaj …”. ~~Dziś regułę łamie karta osoby w grobie~~ — **[[ISSUE-024-person-view]] kończy
    te wyjątki** (v1.18): karta osoby w [[grob]] i w [[osoby]] oraz chipy i karta partnera w formularzu prowadzą do widoku
    osoby ([[osoba]] D14). **Poprawa ma jedno wejście — ✎ w widoku**, a ✎ dla osoby, której poprawa już leży w stosie,
    wraca do niej zamiast otwierać drugą ([[osoba]] D15).
    **Wyjątek — wybór zdjęć w widoku** (v1.43, [[ISSUE-048-portrait-photos]]; pierwszy raz w v1.18 przy tle): w widoku osoby pasmo tła wybiera tło,
    a portret i okrąg z inicjałami — profilowe i nowe zdjęcia ([[osoba]] D21, D23, D24). To wybór i dodanie obrazu, nie poprawa wpisu, więc
    **zapisuje się od razu**, jak zdjęcie nagrobka. Usuwanie zdjęć i „Kto jest na zdjęciu?” zostają pod ✎, bo mogą coś odebrać. Gdy poprawa tej
    osoby leży w stosie, te wejścia wracają do niej, jak ✎ ([[osoba]] D25).

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
- **Ikona znicza** nie istnieje w Material Icons. Własna ikona, jedna na całą aplikację (wersja w dwóch tonach i pełna) —
  ~~sylwetka z [[ISSUE-014-home-map-of-poland]] ([[cmentarze]] → *Style B rules applied*)~~; od v1.42 rysunek autora z DALL-E w foncie ikon
  (reguła 8, [[ISSUE-046-icons]]).

## Candidates — ISSUE-046 (2026-10-18)
> Kandydaci do [[ISSUE-046-icons]], **bez zmiany reguł**: reguła 3 i ikona aplikacji zmieniają się dopiero po wyborze autora na stopie #1
> (retro 4, R1 — zmiana decyzji najpierw na makiecie). Makieta `ikony-046.html` w katalogu tymczasowym sesji `1f978d57-…\scratchpad\makieta-046\`
> (poza repo; fonty z tego samego źródła co w aplikacji). **Nie pokazuje** pikseli Fluttera, słońca ([[NFR-004-czytelnosc-w-sloncu]]) ani opcji C —
> ta czeka na obrazy autora (prompty: katalog tymczasowy `b20ca21c-…\scratchpad\dalle-prompts-046.md`; decyzja autora w `/pm` 2026-10-18: wybór przy komplecie).

**Stan dziś:** 77 różnych ikon `Icons.*` w ok. 180 miejscach (`grep` w `lib/`), font Material Icons z Fluttera 3.41.1 — jedna grubość (kreska ok. 2 dp), końce
kanciaste. Z tekstem rosną tylko strzałka linku (`north_east`, reguła 1) i ikona w podglądzie z bazy; reszta ma stałe 16–24 dp. Znicz (`candle.dart`) ma kreskę
1,5 w siatce 24, czyli jest cieńszy od reszty. Kanon: brief §6a *„Thin line icons”*; R1 i R4 mają ikony cienkie, z zaokrąglonymi końcami, a „Drzewo” w R1 to
gałązka drzewa liściastego, nie schemat.

| # | Kandydat | Co widać | Koszt | Źródło |
|---|---|---|---|---|
| A | Material Icons `outlined` (dziś) | kreska ok. 2 dp, końce kanciaste; grubsze niż znicz i niż R1/R4 | 0 | `flutter/bin/cache/artifacts/material_fonts/materialicons-regular.otf` |
| B | Material Symbols — pakiet `material_symbols_icons` 4.2960.0 (Apache-2.0, fonty zmienne Outlined · Rounded · Sharp, osie FILL, GRAD, `opsz` 20–48, `wght` 100–700) | grubość i końce (zaokrąglone · kanciaste) jednym ustawieniem motywu; przy 300 kreska zbliża się do znicza | nowa zależność; ok. 180 odwołań `Icons.*` do podmiany (mechanicznie); ok. 0,2 MB w APK | [pub.dev](https://pub.dev/packages/material_symbols_icons) (odczyt 2026-10-18); fonty z [google/material-design-icons](https://github.com/google/material-design-icons/tree/master/variablefont) |
| C | arkusz 9 ikon z DALL-E | czeka na obrazy | raster przy 24 dp, kolor nie zmienia się ze stanem bez przerysowania do wektora; 68 ikon spoza arkusza zostaje z A albo B | prompty z 2026-10-16 |

**Pomiar i sonda (2026-10-18):**
- **Odpowiedniki:** 77 z 77 ikon jest w Material Symbols — zwykle ta sama nazwa bez przyrostka `_outlined`/`_outline`; `people_outline` → `group`, `favorite_border`
  → `favorite`.
- **Wycinanie ikon przy buildzie release nie gubi grubości:** `font-subset` z Fluttera 3.41.1 (ten sam, który wycina nieużywane ikony) zostawił tabele `fvar`, `gvar`,
  `avar`, `HVAR` i cztery osie. 9 ikon Rounded: 36 KB z 15,2 MB; 75 ikon Rounded: 227 KB (A dziś: 11 KB). Czy silnik rysuje wybraną grubość na telefonie, potwierdzi
  build release w `dev` (zrzut 300 obok 400).
- **Kontrast** (wzór WCAG z `theme.dart`): ikona w tekście pomocniczym 5,50 na tle / 5,01 na powierzchni, w akcencie 8,81 / 8,04 — wszystkie ≥ 3:1 (SC 1.4.11) przy
  każdej opcji. Próg liczy kolor, nie grubość kreski, więc cienka kreska w słońcu to pytanie do NFR-004, nie do SC 1.4.11.
- **Dla planu (fakty, nie decyzje):** wbudowane widżety Fluttera (np. „wstecz”, „zamknij” w pasku) rysują własne `Icons.*` — przy B trzeba je podmienić w motywie
  (`ActionIconThemeData` → `backButtonIconBuilder`, `closeButtonIconBuilder`), inaczej zostaną grubsze. `opticalSize` = rozmiar ikony. Pakiet zależy tylko od `flutter`,
  fonty są w pakiecie, nic nie idzie do sieci — do potwierdzenia przy planie ([[NFR-005-dane-nie-opuszczaja-telefonu]]).

**Ikona aplikacji:** dziś domyślna ikona Fluttera — tylko `mipmap-*/ic_launcher.png`, bez ikony adaptacyjnej i bez jednobarwnej (motywy Androida 13+ jej nie
przekolorują). Kandydaci: **V — znicz z aplikacji** (decyzja projektowa `ui`, bez DALL-E): sylwetka z `candle.dart` jako wektor, płomień wypełniony, kreska
grubsza (1,9 w siatce 24), w strefie bezpiecznej 66 z 108 dp; wersja jednobarwna to ta sama ścieżka · **L1–L3** z promptów DALL-E (znicz · płomień z drzewem
rodziny · ścieżka „jak łączy się ze mną”) — czekają.

✅ **Rozstrzygnięte na stopie #1 (autor, 2026-10-18)** — 1: **B w kierunku arkusza** (zaokrąglone, 300, wypełnienie 25%, pióro, zdjęcie z krajobrazem) ·
2: **rośnie obok tekstu** · 3: **`nature`** · 4: **L1**. Reguły 3 i 8 przepisane w v1.38; zapis decyzji — [[ISSUE-046-icons]] → *Implementation plan*.
~~⚠️ **OPEN — na stop #1**~~ (po kolei, jedno pytanie na raz — `autonomous-flow.md`):
1. **Ikony w aplikacji:** A · B (końce, grubość) · C.
2. **AC-2 „rosną z tekstem”** — dziś nie rosną. Kandydaci: **stała 24 dp** (jak Android: rozmiar czcionki zmienia `sp`, a ikony w `dp` rosną tylko z „rozmiarem
   wyświetlania”; Flutter `IconThemeData.applyTextScaling` domyślnie `false`) · **rośnie obok tekstu** (przyciski, nagłówki sekcji, wiersze; pasek ekranu i
   zakładki stałe). Przy 200% ikona obok tekstu ma 48 dp — na makiecie to widać.
3. **Zakładka „Drzewo”** (przy B): `account_tree` (schemat, dziś) · `family_history` (drzewo rodziny: osoby jako kółka) · `nature` (drzewo liściaste, jak gałązka
   w R1). `park` odpada — drzewo iglaste, a iglaste to materiał wieńców pogrzebowych (reguła 8).
4. **Ikona aplikacji:** V · L1 · L2 · L3.

**Arkusz C od autora (2026-10-18, `_ikony-dalle\C-arkusz-bursztyn.png`, poza repo) — kierunek wybrany przez autora: bursztyn, dwa tony, charakter**
([[ISSUE-046-icons]] → *Implementation plan*). Na makiecie 9 ikon arkusza jako maski (kolor ze stanu działa — ta sama technika co wieniec, [[wieniec]]):
przy 96 px cały charakter; **przy 24 dp — rozmiar w aplikacji — detale znikają**: drzewo to rozmyta kula, trasa i poziomice mapy to szum, twarze rodziny to plamy,
stalówka to słaba kreska; czytelne zostają lupa, koło zębate i pinezka ze zniczem. Arkusz ma 9 z 77 ikon, reszta zostałaby z B. Na makiecie dodane dwa
przełączniki B, które przenoszą kierunek na wektor: **wypełnienie 25%** (glif wypełniony pod glifem z kreską — ten sam kształt, więc się pokrywają) i
**metafory z arkusza** (`ink_pen` zamiast ołówka, `add_photo_alternate` — zdjęcie z krajobrazem). `family_restroom` odrzucone — pełne postacie jak znak
toalety, nie pasuje do „godny”.

**Ikona aplikacji od autora (2026-10-18):** L1 — znicz z perforowaną pokrywką, L2 — drzewo z kropkami i płomieniem (`_ikony-dalle`, poza repo); L3 nie
powstała. Na makiecie jako maski: tło `grobing_background` i akcent z aplikacji, a nie z obrazu; warstwa jednobarwna = same linie (alfa > 0,55), wyprowadzona z
kolorowej. Obie czytelne przy 56 px na ekranie głównym i w motywie Androida 13. Przy wyborze L ikona powstaje tak samo jak wieńce: obraz → maska → PNG na
gęstość w `res/mipmap-*` (wyjątek strażnika już obejmuje `res/`).

**AC → element:** AC-1 → ikona aplikacji (V albo L) jako adaptacyjna z warstwą jednobarwną, w miejsce `mipmap-*/ic_launcher.png`. AC-2 → jedna rodzina (OPEN 1),
kontrast — pomiar wyżej, rośnięcie z tekstem — OPEN 2, cele dotyku — zmiana ikon nie zmienia przycisków (≥ 48 dp, *Known gaps*); przy „rośnie obok tekstu” przycisk
z podpisem rośnie razem z tekstem, a ikona mieści się w jego wysokości.

**Rekomendacja `ui`** (po kandydatach): **B, końce zaokrąglone, grubość 300** — najbliżej R1/R4 i *„Thin line icons”*, jedna grubość ze zniczem; **rośnie obok
tekstu** (AC-2 tak, jak je zapisano, bez ruszania pasków); **`family_history`** — mówi „rodzina”, a nie „schemat”; **V**, chyba że któraś L wyraźnie wygra —
V jest wektorem z tej samej ścieżki co znicz w aplikacji, więc nic nie trzeba przerysowywać. **Nie da:** wyglądu 1:1 z R1 — ikony R1 przypominają inną rodzinę
(cienkie, z zaokrąglonymi końcami, w stylu Lucide), której makieta nie pokazuje. *Obali:* kreska 300 w tekście pomocniczym słabo widoczna w słońcu (NFR-004,
telefon) → grubość 400 z zaokrąglonymi końcami, jednym parametrem.

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
- 2026-10-07 — **v1.9, baza zdjęć osoby** (`ui` przed planem [[ISSUE-017-person-photos]], [[zdjecia-osoby]]): reguła
  14 — okrąg tylko dla profilowego osoby (także nagłówek bazy, 96 dp), zdjęcia w bazie jako kwadraty w siatce
  (bywają grupowe), stan zdjęcia nie jest znacznikiem na zdjęciu. Tokeny bez zmian, więc pomiar z 2026-10-06
  obowiązuje; obrys pustego pola wyboru to tekst pomocniczy na tle (5,50:1, SC 1.4.11 ✅).
- 2026-10-07 — **v1.10, kadr profilowego** (`ui` przed planem [[ISSUE-018-profile-photo-crop]], [[kadr-profilowego]]):
  reguła 14 — okrąg profilowego pokazuje kadr łącza (bez kadru: środek); ramka kadru to jedyny wyjątek od „nic na
  zdjęciu”, bez tekstu, z pierścieniem w akcencie między liniami w kolorze tła. Tokeny bez zmian, więc pomiar z
  2026-10-06 obowiązuje; pierścień to istniejąca para akcent/tło (8,81:1).
- 2026-10-07 — **v1.11, rodzina** (`ui` przed planem [[ISSUE-019-family-relations]], [[rodzina]], [[wpis-osoby]] v5):
  reguła 11 — chip relacji z R4 prawego jako wyjątek od „karta z chevronem”. Tokeny bez zmian, więc pomiar z 2026-10-06
  obowiązuje: obrys chipu na tle 3,40:1, napis chipu na powierzchni 10,02:1. Przycisk segmentowy dla pola płci wypadł
  razem z polem na stopie #1 (decyzja autora: bez płci), więc reguły dla niego nie ma — bez instancji byłaby na zapas.
- 2026-10-08 — **v1.12, szkielet aplikacji z prototypu** (`ui`, [[SPIKE-004-mvp-flow-prototype]] panel 0, decyzje
  autora D1–D4):
  - reguła 12: pasek dolny i koło zębate potwierdzone; widoczny na ekranach do oglądania, ukryty w formularzach,
    trybach wyboru i na zdjęciu na pełnym ekranie; każda zakładka szuka swojego;
  - nowa reguła 15: widok przed poprawą.

  Tokeny bez zmian, więc pomiar z 2026-10-06 obowiązuje. Pasek to istniejące pary: powierzchnia z tekstem
  pomocniczym, a aktywna zakładka w akcencie.
- 2026-10-08 — **v1.13, mapa Polski jak R1 i zdjęcie cmentarza** (`ui`, [[SPIKE-004-mvp-flow-prototype]] panel 1,
  decyzje autora D5–D6):
  - nowa rola: woda (`water`, `waterLine` — wartości proponuje [[cmentarze]] element 3, a do `theme.dart` wpisze je
    `dev`);
  - reguła 13: sąsiedzi, morze, jeziora, rzeki; granica Polski w kolorze tekstu pomocniczego;
  - reguła 14: kształt zdjęcia cmentarza.

  Pomiar nowych par (wzór WCAG, 2026-10-08): tekst pomocniczy/woda 5,04:1 · obrys/woda 3,11:1 · akcent/woda 8,07:1 ·
  woda/ląd 1,00:1 · linia wody/ląd 2,49:1 (dekoracja).
- 2026-10-08 — **v1.14, plan cmentarza** (`ui`, [[SPIKE-004-mvp-flow-prototype]] panel 2, decyzje autora D8, D11):
  reguła 13 — plan schematyczny i kwatery autora; *State colours* — propozycja zieleni „Plan offline” `#8CC084`
  (8,19:1 na powierzchni, z ikoną i podpisem).
- 2026-10-08 — **v1.15, widok osoby** (`ui`, [[SPIKE-004-mvp-flow-prototype]] panel 4, [[osoba]]): reguła 8 — bez
  gałązek wokół portretu (rozstrzygnięte); reguła 14 — kształt zdjęcia w tle osoby. Tokeny bez zmian.
- 2026-10-08 — **v1.16, drzewo i wizyta** (`ui`, [[SPIKE-004-mvp-flow-prototype]] D20, D22; [[drzewo]], [[cmentarz]] v4.2):
  - nowa rola — kolory relacji (rodzic–dziecko, partnerzy) z kształtem i legendą;
  - *State colours* — wartość niebieskiej kropki „tu jesteś”.

  Pomiar (wzór WCAG, 2026-10-08): rodzic–dziecko 8,50:1 na tle, 7,75:1 na powierzchni · partnerzy 8,16:1 i 7,45:1 ·
  między sobą 1,04:1 (dlatego kształt i legenda) · kropka 6,99:1 i 6,38:1.
- 2026-10-08 — **v1.17, po przeglądzie szkieletu aplikacji** (`ui` jako subagent `qa`,
  [[ISSUE-022-app-skeleton-tabs-people-settings]]; [[osoby]] v2, [[ustawienia]] v2, [[cmentarze]] v2.5):
  - *State colours* — zieleń stanu weszła do `theme.dart` jako `GrobingColors.stateOk`; rola „bezpieczne i gotowe”
    obejmuje kopię udaną (ustawienia), a nie tylko „Plan offline”;
  - *Thresholds* — wyjątek: podpis zakładki 12 sp, półgruby (jak w pasku nawigacji Material 3);
  - akcent — nigdy numery listy ani inne ozdobniki (notka przekazania);
  - reguła 6 — twarda spacja po jednoliterowych słowach i w „z d.”; **kod jeszcze jej nie stosuje** (osobna drobna
    pozycja);
  - reguła 12 — ustawienia i ekrany pod nimi bez paska; mapa na dole stosu; zaślepka zakładki bez ekranu, tymczasowa i
    nie jako wzór pustego stanu;
  - reguła 14 — profilowe 40 dp także w wierszu ustawień.

  Pomiar (wzór WCAG z wartości w `theme.dart`, 2026-10-08): `stateOk` 8,97:1 na tle, 8,19:1 na powierzchni. Pozostałe
  tokeny bez zmian (przeliczone tego dnia: akcent 8,81 / 8,04, tekst pomocniczy 5,50 / 5,01, błąd 6,45 / 5,89, obrys
  3,40 / 3,10 — wyniki te same).
- 2026-10-09 — **v1.18, widok osoby** (`ui` przed planem [[ISSUE-024-person-view]], [[osoba]] v2):
  - reguła 15 — wyjątki (karta w grobie, w Osobach, chipy w formularzu) kończy ISSUE-024; poprawa ma jedno wejście (✎),
    a druga poprawa tej samej osoby w stosie się nie otwiera;
  - reguła 11 — chip relacji prowadzi do widoku osoby, opis dla czytnika „— otwórz”;
  - reguła 14 — tło osoby wybiera się w podglądzie, stan niesie podtytuł;
  - role — kolory relacji wchodzą do `theme.dart` z ISSUE-024 (mini-drzewo).

  Tokeny bez nowych wartości, więc pomiar z v1.16 i v1.17 obowiązuje (rodzic–dziecko 8,50:1 na tle, partnerzy 8,16:1 na tle;
  okrąg z inicjałami — obrys/tło 3,40:1, inicjały — tekst pomocniczy na powierzchni 5,01:1).
- 2026-10-09 — **v1.19, pasmo tła** (`ui`, stop #2 [[ISSUE-024-person-view]], runda 1; [[osoba]] v2.3, [[zdjecia-osoby]] v1.4): reguła 14
  — tło wybiera się też z pasma w widoku osoby; zaznaczone zdjęcie w siatce ma ramkę wokół, nie na zdjęciu; pasmo bez tła jako
  wyjątek od „obrys, ikona, podpis”. Tokeny bez zmian (ikona — akcent/powierzchnia 8,04:1; ramka — akcent/tło 8,81:1).
- 2026-10-12 — **v1.20, po przeglądzie mapy jak R1 i zdjęcia cmentarza** (`ui` jako subagent `qa`,
  [[ISSUE-023-poland-map-r1-cemetery-photo]]; [[cmentarze]] v2.6):
  - reguła 13 — podpisy na mapie rosną z tekstem najwyżej do 1,3×; „Polska” tylko przy najmniejszych przybliżeniach;
    brzegi morza u sąsiadów i brzegi jezior bez linii;
  - *Thresholds* — dwa wyjątki: podpisy mapy (SC 1.4.4, 1,3×) i podpis pola „Dodaj zdjęcie” w miejscu miniatury cmentarza
    (12 sp, półgruby).

  Pomiar (wzór WCAG z wartości w `theme.dart`, 2026-10-12): `water` i `waterLine` weszły do `theme.dart` z wartościami z
  v1.13, więc pary z v1.13 obowiązują (przeliczone: tekst pomocniczy/woda 5,04, woda/ląd 1,00, linia wody/ląd 2,49). Nowe
  pary: „Polska” (tekst pomocniczy 85%) 3,98:1 na lądzie i 4,02:1 na wodzie — duży tekst, próg 3:1; granica sąsiada (obrys
  45%) 1,61:1 — dekoracja. Pole „Dodaj zdjęcie” na powierzchni: obrys 3,10, ikona 8,04, podpis 10,02.
- 2026-10-12 — **v1.21, ekrany wizyty i podpis źródła mapy** (decyzja autora W2 na stopie #1 i przegląd `ui`
  [[ISSUE-027-cemetery-map-plan-photo-states]]; [[cmentarz]] v5, v5.1). *Wpis uzupełniony w v1.22 — wersja v1.21 zmieniła
  tytuł i progi, a tego wiersza zabrakło.*
  - *Thresholds* — ekrany wizyty: ≥ 7:1 dla tekstu czytanego przy grobie (miara NFR-004);
  - wyjątek: podpis źródła mapy 11 sp na plakietce.
- 2026-10-12 — **v1.22, kwatery autora** (`ui` przed planem [[ISSUE-028-cemetery-sectors]], [[cmentarz]] v6):
  - reguła 13 — kwatera wybrana i rysowana (bez wypełnienia, akcent na linii w kolorze tła); celownik (K1 — wybór autora); po
    przeglądzie ISSUE-028: stara strefa w kolorze tekstu pomocniczego, strefy na zdjęciu na linii w kolorze tła;
  - reguła 14 — drugi wyjątek od „nic na zdjęciu”: zaznaczanie kwatery na zdjęciu z góry.

  Tokeny bez zmian. Pomiar (wzór WCAG z wartości w `theme.dart`, 2026-10-12): linia kwatery (tekst 75%) 6,16:1 na powierzchni i
  6,56:1 na tle; akcent na powierzchni 8,04:1; akcent wobec linii kwatery 1,31:1; stara strefa (tekst pomocniczy) 5,01:1 na
  powierzchni i 1,62:1 wobec alejki (obrys).
- 2026-10-12 — v1.23 (`ui`, [[ISSUE-029-pin-on-site-gps]], przegląd zbudowanego ekranu): *State colours* — „tu jesteś” w `theme.dart`
  (`GrobingColors.here`), rola obejmuje też włączony „gdzie jestem” i ikonę plakietki 10a; nigdy akcent, nigdy ostrzeżenie. Słaby
  sygnał w trybie pinezki to fakt w kolorze tekstu (reguła 7, *Token roles*: akcent nie dla ostrzeżeń). Pomiar bez zmian
  (kropka 6,99:1 na tle, 6,38:1 na powierzchni).
- 2026-10-13 — **v1.24, drzewo od osoby** (`ui` przed planem [[US-009-drzewo-od-osoby]], [[drzewo]] v1.5):
  - role — kolory relacji obejmują ślad dalszej rodziny (krycie 60%, przerywana 3/3);
  - *Thresholds* — wyjątek od celu dotyku 48 dp dla węzła drzewa przy oddaleniu, nigdy poniżej 24 dp (WCAG 2.2 SC 2.5.8, wyjątek
    *Equivalent* — przybliżenie).

  Tokeny bez zmian. Pomiar (wzór WCAG z wartości w `theme.dart`, 2026-10-13): ślad 3,75:1 (rodzic–dziecko) i 3,66:1 (partnerzy) na tle;
  znak „Ja” w akcencie na powierzchni 8,04:1; imię na tle 10,98:1. Reguła dla imion przy oddalaniu czeka na decyzję autora ([[drzewo]]
  *Open* 5) — przy I2 dojdzie do reguły 13 jako druga instancja podpisów z obwódką i chowaniem.
- 2026-10-13 — **v1.25** (decyzja autora na stopie #1 [[ISSUE-033-tree-from-a-person]], I2): reguła 13 — imiona w drzewie przy oddaleniu jak
  podpisy na mapie (nie maleją poniżej 13 sp, obwódka w kolorze tła, chowanie nakładających się z pierwszeństwem bliższych środka). Tokeny i
  pomiar bez zmian.
- 2026-10-13 — **v1.26, po przeglądzie drzewa** (`ui` jako subagent `qa`, [[ISSUE-033-tree-from-a-person]]; [[drzewo]] v1.7, D23): reguła 13 —
  imię w drzewie stoi na tabliczce w kolorze tła (zaokrąglona 4 dp, 3 dp z boków) zamiast obwódki liter; tabliczka tylko na jednolitym tle,
  na mapie obwódka zostaje. Powód: ok. 100 rozmytych cieni w klatce szarpało przejścia między poziomami (pomiar `dev` na emulatorze). Tokeny i
  pomiar bez zmian (imię na tabliczce = tekst na tle, 10,98:1; przeliczone z `theme.dart` 2026-10-13).
- 2026-10-13 — **v1.27** (przegląd `ui` [[ISSUE-033-tree-from-a-person]], MAJOR; poprawka w drzewie, mini-drzewie i portrecie — autor: „ok” na
  stopie #2): reguła 2 — poświata pod okręgiem, nad nim tylko pierścień. Pomiar: wnętrze okręgu „Ja” na zrzucie `#1C1B19` (= powierzchnia), przed
  poprawką `#594626`; znak „Ja” 8,04:1. Tokeny bez zmian.
- 2026-10-14 — **v1.28** ([[ISSUE-035-tree-names-shrink-my-voice]]; G2 — decyzja autora na stopie #1 [[ISSUE-034-tree-presentation-mode]],
  potwierdzona na stopie #1 ISSUE-035; [[drzewo]] v1.9, D28):
  - reguła 7 — **kto mówi**: nazwa pokrewieństwa Twoim głosem („Moja babcia”), zdania aplikacji do Ciebie („Wybierz, która osoba to Ty”); źródło
    Microsoft Writing Style Guide → Person;
  - reguła 13 — imiona w drzewie zostają przy I2: na stopie #1 ISSUE-035 autor wybrał I2, a nie I1 ze stopu #1 ISSUE-034 ([[drzewo]] D27). Wyjątek od
    13 sp, który `ui` dopisał dla I1, wycofany przed planem.

  Tokeny bez zmian. Pomiar (wzór WCAG z wartości w `theme.dart`, 2026-10-14): linia karty (tekst pomocniczy na powierzchni) 5,01:1, imię na tle
  10,98:1.
- 2026-10-14 — **v1.29** ([[ISSUE-037-time-on-the-tree]]; decyzja autora na stopie #1, *„tak”*; [[drzewo]] v1.12, D32, D35):
  - **niepewność niesie kształt, nie krycie** — na suwaku czasu osoba z datą niepewną ma przerywany obrys okręgu (kolor obrysu, kreska 4/3), a nie bladość.
    Przenikanie odrzucone pomiarem: imię przy kryciu 30–50% ma 2,04–3,56:1, 4,5:1 dopiero przy 60%. Krycie ok. 30% zostaje dla „wyszarzenia” w US-011;
  - reguła 8 — znicz na węźle znaczy „na pewno nie żyje”: w oknie niepewnej śmierci jest przerywany obrys, a znicz dopiero na końcu okna;
  - koniec związku — „//” w kolorze partnerów przez linię pary (genogram), jak linia, którą przecina.

  Tokeny bez zmian.
- 2026-10-14 — **v1.30** (`ui` przed planem [[ISSUE-038-history-on-tv-and-tempo]]; [[drzewo]] v1.14, D38, D39): *Thresholds* — **tekst dla telewizora**: co rodzina czyta z kanapy, ma
  ≥ 36 sp i stoi ≥ 48 dp od bocznych krawędzi, a z tekstem systemu rośnie najwyżej do 1,3×. Pierwsza instancja: rok historii w trybie prezentacji. Próg stoi niezależnie od wyboru
  miejsca roku na stopie #1 (L1–L3). Tokeny bez zmian. Pomiar (wzór WCAG z wartości w `theme.dart`, 2026-10-14): rok w akcencie na tle 8,81:1; tekst o kryciu 10% na tle (kandydat L3)
  1,20:1, przy 40% — 2,70:1, poniżej 3:1 dla dużego tekstu.
- 2026-10-14 — **v1.31** (przegląd `ui` zbudowanej [[ISSUE-038-history-on-tv-and-tempo]], odstępstwo 3 `dev` przyjęte; [[drzewo]] v1.15): reguła 5 — **stała szerokość
  zmiennego napisu** obok kontrolki do przeciągania (szerokość najszerszej wartości). Reguła, bo to druga instancja: rok w karcie (v1.13) i przycisk tempa. Tokeny bez zmian.
  Pomiar (wzór WCAG z wartości w `theme.dart`, 2026-10-14): tempo w kolorze tekstu na powierzchni 10,02:1; rok w rogu na tabliczce w kolorze tła 8,81:1.
- 2026-10-16 — **v1.32** (przegląd `ui` zbudowanej [[ISSUE-042-places-of-residence]]; [[zamieszkanie]] v1.1): reguła 6 — **linia nie kończy się separatorem
  ani dopiskiem** (twarda spacja po „·” i po „ok.”, „od”, „do”, „dziś”; lata okresu łamią się za „–”). Reguła, bo to druga instancja: linia miejscowości w bazie
  cmentarzy ([[cmentarze]] D25) i linie zamieszkania. Twarda spacja po jednoliterowych słowach — w nowych stałych tekstach od razu. Tokeny bez zmian. Pomiar
  (wzór WCAG z wartości w `theme.dart`, 2026-10-16; wyniki te same): tekst 10,98 / 10,02 · tekst pomocniczy 5,50 / 5,01 · akcent 8,81 / 8,04 · obrys 3,40 / 3,10 ·
  błąd 6,45 / 5,89 (na tle / na powierzchni) · tło na akcencie 8,81.
- 2026-10-17 — **v1.33** (`ui` przed planem [[ISSUE-044-family-wreaths]]; decyzje autora na prototypie — wieniec K2, paleta, Ś3, C3: [[wieniec]] D5, D6, D14, D15):
  - reguła 8 — **gałązki wracają jako wieniec rodu** (zmienia v1.15 „bez gałązek”, [[osoba]] D3 v2.6); wzory to rośliny bez znaczenia religijnego, bez iglastych;
  - reguła 1 — wyjątek: **kolor rodu** z palety 12 kolorów, tylko dla wieńca;
  - reguła 2 — głębia wieńca (przejście tonu i tłoczenie) **wpieczona w obraz przy budowie**, a nie gradient tła ani rozmyty cień w klatce;
  - reguła 14 — liście nad zdjęciem w tle z obwódką w kolorze tła.

  Nowa rola tokenów: kolory rodu (do `theme.dart` z ISSUE-044). Pomiar (wzór WCAG, 2026-10-17): 12 kolorów płasko 4,46–12,16:1 na tle, 4,07–11,09:1 na
  powierzchni; po cieniowaniu C3 najciemniejsze 5% liści ≥ 3,10:1 na tle (brąz) — tabela w [[wieniec]]. Pozostałe tokeny bez zmian.
- 2026-10-17 — **v1.34** (`ui` po stopie #1 [[ISSUE-045-migration-map]]; decyzje autora W2, K2, O3, D2, R4 — [[mapa-migracji]] v1.1): reguła 13 — punkt **mapa
  świata** (ląd, morze, granice jako dekoracja, osoba jako okrąg, „cały kraj” w punkcie nazwy kraju bez obszaru, ślad ruchu). Tokeny bez zmian; pary zmierzone
  wzorem WCAG z `theme.dart` 2026-10-17 (tabela w [[mapa-migracji]]).
- 2026-10-17 — **v1.35** (przegląd `ui` zbudowanej [[ISSUE-045-migration-map]]; decyzja autora w trakcie przeglądu — [[mapa-migracji]] v1.2, D18, D19): reguła 13,
  punkt **mapa świata** — **bez podpisów miejsc i nazw krajów** (zdanie o nazwach krajów 13 sp usunięte; „cały kraj” mówi karta i czytnik); stosy, które leżałyby
  na sobie, łączą się w jeden stos z „+N” i dotknięcie przybliża (druga instancja łączenia po zniczach z liczbą na mapie Polski); ślad osoby w środku — akcent przy
  kryciu 90%. Tokeny bez zmian. Pomiar (wzór WCAG z wartości w `theme.dart`, 2026-10-17): ślad — tekst 50% 3,48:1 na lądzie, 3,46:1 na wodzie (v1.34 podawała 3,49
  — zaokrąglenie); akcent 90% 6,74:1 na lądzie, 6,75:1 na wodzie; pozostałe pary bez zmian (tekst 10,98 / 10,02 · tekst pomocniczy 5,50 / 5,01 · akcent 8,81 /
  8,04 · obrys 3,40 / 3,10, na wodzie 3,11 — na tle / na powierzchni).
- 2026-10-17 — **v1.36** (stop #2 [[ISSUE-045-migration-map]] — decyzja autora, [[mapa-migracji]] v1.4, D25): reguła 13, punkt **mapa świata** —
  przeprowadzka to sam przejazd okręgu, **bez śladu** (*„bez tych linii szarych (nie ma potrzeby żadnego dodatkowego efektu)”*). Pary śladu z v1.35 (3,48 i
  6,74:1) nieaktualne. Tokeny bez zmian.
- 2026-10-18 — **v1.37** (`ui` przed planem [[ISSUE-046-icons]]): sekcja *Candidates — ISSUE-046* — opcje A i B na makiecie (C czeka na obrazy autora), ikona
  aplikacji V, sonda wycinania fontu zmiennego, 4 pytania na stop #1. **Reguły bez zmian** do wyboru autora. Tokeny bez zmian; pary ikon (wzór WCAG z
  `theme.dart`, 2026-10-18): tekst pomocniczy 5,50 / 5,01 · akcent 8,81 / 8,04 (na tle / na powierzchni).
- 2026-10-18 — **v1.38** (stop #1 [[ISSUE-046-icons]], decyzje 1–4 autora): reguła 3 — **Material Symbols, zaokrąglone, grubość 300, wypełnienie 25%**
  (dekoracja; znaczenie i ≥ 3:1 niesie kreska), metafory z arkusza (pióro, zdjęcie z krajobrazem, drzewo liściaste), ikona obok tekstu rośnie z tekstem, pasek i
  zakładki 24 dp; reguła 8 — znicz L1 to ikona aplikacji. Tokeny bez zmian; pary bez zmian (tekst pomocniczy 5,50 / 5,01 · akcent 8,81 / 8,04).
- 2026-10-18 — **v1.39** (przegląd `ui` zbudowanej [[ISSUE-046-icons]] — przyjęte odstępstwa `dev` 1–3): reguła 3 — stałe 24 dp także przełącznik „Drzewo | Mapa”,
  przyciski z samą ikoną i ikony w pudełkach o stałym rozmiarze (odstępstwo 3; reguła mówiła tylko o pasku i zakładkach); glify z własnego wyciętego fontu
  zamiast pakietu (odstępstwo 1 — sonda: wycinanie Fluttera gubiło glify), grubość jedną stałą w widżecie (odstępstwo 2); reguła 4 — „bez własnych krojów
  tekstu”, bo font ikon nie jest krojem. Odstępstwo 4 (ta sama ikona dla obu „dodaj zdjęcie”) to już reguła 3 — bez zmiany. Tokeny bez zmian. Pary ikon (wzór
  WCAG z `theme.dart`, 2026-10-18): kreska na tle / powierzchni — tekst pomocniczy 5,50 / 5,01, tekst 10,98 / 10,02, akcent 8,81 / 8,04, `stateOk` 8,97 / 8,19,
  błąd 6,45 / 5,89, `here` 6,99 / 6,38, tło na akcencie 8,81; **kreska wobec własnego wypełnienia 25%** (szczegół wewnątrz ikony) — najsłabsza para: tekst
  pomocniczy na powierzchni 3,47:1, akcent 4,81, tło na akcencie 5,41 — wszystkie ≥ 3:1 (SC 1.4.11); wypełnienie wobec tła 1,41–1,77:1 — dekoracja.
- 2026-10-18 — **v1.40** (stop #2 [[ISSUE-046-icons]], decyzja 1' autora): reguła 3 — **dziewięć ikon z arkusza DALL-E autora** (zakładki, lupa, ustawienia,
  dodaj zdjęcie, pinezka, pióro, telewizor) przerysowane do wektora w foncie ikon; reszta z Material Symbols. Na stopie #2 autor zobaczył B (ikony Google w jego
  kolorach) i wskazał, że chciał swoje rysunki — opis opcji B na stopie #1 był myląco nazwany kierunkiem. Tokeny bez zmian.
- 2026-10-18 — **v1.41** (przegląd `ui` rundy 4 [[ISSUE-046-icons]]): reguła 3 — linie z arkusza poszerzone o ≈ 0,3 dp (`THICKEN`), dźwignia na słońce dla
  glifów z arkusza, pinezki informacyjne zostają z Material; reguła 8 — pinezka ze zniczem także na przyciskach, które stawiają nową pinezkę. Tokeny bez zmian.
- 2026-10-18 — **v1.42** (stop #2 [[ISSUE-046-icons]], prośba autora): reguła 8 — znicz aplikacji to rysunek autora z DALL-E (ten sam znak co ikona L1): dwa
  tony w logo i na przyciskach, pełny w pinezce i w znaczniku zmarłych; *Known gaps* — stara sylwetka zastąpiona. Tokeny bez zmian.
- 2026-10-19 — **v1.43** (`ui` przed planem [[ISSUE-048-portrait-photos]]): reguła 15 — wyjątek „wybór zdjęć w widoku” nazwany wprost (tło od v1.18,
  teraz profilowe i dodawanie zdjęć z portretu i okręgu z inicjałami, zapis od razu; usuwanie zostaje pod ✎); reguła 14 — profilowe wybierane z
  portretu wzorcem „Zdjęcia w tle”, ramka zaznaczenia także przy wyborze kilku zdjęć ([[zdjecia-w-aplikacji]]), okrąg z inicjałami jako przycisk z
  plakietką (ten sam wyjątek co pasmo bez zdjęcia). Tokeny bez zmian.
- 2026-10-19 — **v1.44** (`ui` przed planem [[ISSUE-049-tree-levels-and-zoom]], propozycja na stop #1): *Thresholds* → cel dotyku — wyjątek węzła drzewa przy
  oddaleniu przepisany ([[drzewo]] D52): oddalanie sięga całego drzewa, a poniżej 24 dp dotknięcie przybliża zamiast wybierać osobę. Tokeny bez zmian; pary
  etykiety i listy poziomów przeliczone z `theme.dart` 2026-10-19: obrys na tle 3,40, tekst na powierzchni 10,02, tekst pomocniczy 5,01, akcent 8,04.
- 2026-10-19 — **v1.45** (przegląd `ui` zbudowanej [[ISSUE-049-tree-levels-and-zoom]], odstępstwo 2 `dev` przyjęte): reguła 13, imiona w drzewie — osoba z widocznym imieniem
  leży nad sąsiadami, więc tabliczka zakrywa okręgi pod sobą, a nie okręgi litery ([[drzewo]] v1.24). Tokeny bez zmian; pary przeliczone z `theme.dart` 2026-10-19: tekst
  10,98 / 10,02, tekst pomocniczy 5,50 / 5,01, akcent 8,81 / 8,04, obrys 3,40 / 3,10 (na tle / na powierzchni).
- 2026-10-19 — **v1.46** (stop #2 [[ISSUE-049-tree-levels-and-zoom]], decyzja autora — [[drzewo]] D58): *Thresholds* → gesty — wyjątek „oddalanie drzewa”: + / − w rogu drzewa i na
  listwie trybu prezentacji zmieniają poziom, a przyciski przybliżania odpadły, więc oddalają tylko dwa palce (przybliżanie ma podwójne dotknięcie i dotknięcie małego drzewa).
  Nieaktywny + / − na krańcach poziomów — bez obrysu, ikona w kolorze tekstu pomocniczego (rola z *Token roles*: „nieaktywne”); sam kolor ikony dawał 2,00:1 między
  stanami, więc stan niesie też kształt (SC 1.4.1, przegląd `ui`). *Thresholds* → cel dotyku: zdanie o „+” przepisane — przybliża dotknięcie małego drzewa i podwójne
  dotknięcie. Tokeny bez zmian.
- 2026-10-19 — **v1.47** (`ui` przed planem [[ISSUE-050-next-event]], propozycja na stop #1): *Thresholds* → tekst dla telewizora — próg dla **zdań** (podpis roku po ⏭, [[drzewo]] 6a):
  ≥ 28 sp (M3 *headline medium*, z 3 m na 32″ ok. 18′), najwyżej 1,3× z tekstem systemu; 36 sp zostaje dla liczb i krótkich napisów. Trzecia instancja reguły 6 „linia nie kończy się
  separatorem”: imię z nazwiskiem, dopisek daty i strzałka w podpisie trzymają się razem ([[mapa-migracji]] 15). Tokeny bez zmian; pary przeliczone z `theme.dart` 2026-10-19: tekst
  10,98 / 10,02, tekst pomocniczy 5,50 / 5,01, akcent 8,81 / 8,04 (na tle / na powierzchni).
- 2026-10-19 — **v1.48** (stop #2 [[ISSUE-050-next-event]], runda 1 — prośba autora i decyzja *„B”*): reguła 2 — czwarta instancja poświaty: osoby z podpisu roku po ⏭ na drzewie i
  przeprowadzający się na mapie świecą (pierścień, poświata pod okręgiem i wieńcem, linia pary), jedyna pulsująca — trzy pulsy, potem stała (SC 2.2.2, SC 2.3.1, SC 2.3.3). *Thresholds* →
  tekst dla telewizora bez zmian, ale podpis roku na telewizorze odpadł ([[drzewo]] D72 — linia 14 sp na listwie czytana z telefonu), więc próg 28 sp dla zdań nie ma dziś instancji. Tokeny bez
  zmian; pary przeliczone z `theme.dart` 2026-10-19: akcent 8,81 / 8,04, tekst 10,98 / 10,02, tekst pomocniczy 5,50 / 5,01 (na tle / na powierzchni).
