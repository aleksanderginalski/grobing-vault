---
screen: "Wieniec rodu — wieniec przy portrecie i na drzewie, wybór rodu w „Popraw wpis”, ród (nazwa, kolor, wzór)"
items: ["[[ISSUE-044-family-wreaths]]"]
us: "n/a — pozycja z pomysłu autora ([[2026-10-14-opowiesc-rodziny-i-wieniec]] → d), bez US"
journey-step: "UJ-001 · 5 (widok osoby, R4 prawy) · widok 5 (drzewo, tryb prezentacji)"
mockup: "2026-10-16: wience-044.html (ISSUE-044, discovery: panele 1–6 — kształt K0–K3, linie L1–L2, kobieta po ślubie Ś1–Ś2, wybór rodu i O1–O2, gdzie widać G1–G3, rysunek T1–T2; paleta kolorów rodu) — katalog tymczasowy sesji `2aa5d062-…\\scratchpad` · 2026-10-17: pilot-grid.png (laur i dąb z DALL-E w kolorach rodu wokół portretu 104 dp i 44 dp, w pikselach telefonu) i wience-044-b.html (panele 7–9: 19 wzorów we wspólnym kadrze, Ś1/Ś3, kolor C0–C3) — katalog tymczasowy sesji `3c71c787-…\\scratchpad`"
updated: 2026-10-17
---

# Wieniec rodu — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która zmienia wieniec. Prawdą jest ten plik; prototyp i obrazy z DALL-E to
> podgląd. Wytyczne: [[style-b]] (v1.33) · referencja: [[references]] → **R4 prawy** (gałązki wokół portretu).
>
> **v1.2 (2026-10-17, stop #2 [[ISSUE-044-family-wreaths]] — decyzja autora D20):** ród odróżnia **para wzór + kolor**, nie sam wzór. „też: …” na kaflu
> wzoru (F4) tylko wtedy, gdy inny ród ma ten wzór **w wybranym kolorze**; domyślny wzór nowego rodu, gdy każdy wzór ma już ród — pierwszy, którego nikt nie ma
> w wybranym kolorze.
>
> **v1.1 (2026-10-17, przegląd `ui` zbudowanej [[ISSUE-044-family-wreaths]] — pięć odstępstw z *Dev report* przyjętych):** 96 dp na osobę, gdy wieniec ma
> ktokolwiek w rodzinie, a nie tylko w pokazanym drzewie (1 → D2, D17) · układ wiersza, arkusza i kafli przy tekście ≥ 150% (2 → E1, E2, F4, D19) · obwódka A5
> dokładana przez aplikację przy barwieniu, nie w pliku wzoru (3 → A5) · jasne miejsca C3 jako mnożnik koloru z obcięciem do bieli (4 → A4) · wieniec w węźle
> drzewa, nie na osobnej warstwie pod wszystkimi węzłami (5 → D1, D18). Do tego odstępstwa, których *Deviations* nie wymienia, a przegląd przyjmuje: wiersz E1
> to dla czytnika dwa węzły — słowa i „Zmień” osobno (*Znalezione* 1 w *Dev report*; inaczej przycisk tracił 48 dp) · znak bez wieńca w E1 to przerywany okrąg
> 28 dp w miejscu portretu znaku 56 dp, a nie 40 dp — oba stany znaku mają ten sam okrąg · przy B5 (ona bez rodu, mąż z rodem) linia „Po ślubie wieniec męża: …”
> zamiast „prawa połowa”, bo wieniec jest cały · „Bez wieńca” w arkuszu ma `check`, gdy jest wybrane · kafel wzoru ma wysokość z treści, rząd jak najwyższy
> kafel (*Znalezione* 3 — ok. 100 dp bez „też”, a nie ≥ 120 dp). Doprecyzowane przy okazji: ślad w bok zaczyna się 43 dp od środka **tylko u osoby z
> wieńcem** (D3). [[style-b]] bez zmian: cieniowanie zostaje wpieczone w plik wzoru, a obwódka i kolor powstają raz na parę wzór–kolor i rozmiar, nie w
> klatce (reguła 2); kontrast bez zmian, bo najciemniejsze miejsca to dalej 80% koloru (brąz 3,10:1, przeliczone z `theme.dart`).
>
> **v1.0 (2026-10-17) — pełna specyfikacja, idzie do planu.** Decyzje autora D14 (Ś3 — pół panieński, pół po mężu) i D15 (kolor C3 —
> tłoczenie i przejście tonu): *„jest super idźmy zgodnie z twoją rekomendacją”*. Zmienione razem z tym plikiem: [[osoba]] v2.6 (D3 — wieniec
> zamiast „bez gałązek”), [[wpis-osoby]] v5.10 (wiersz „Wieniec rodu”), [[drzewo]] v1.18 (wieniec na węźle, 96 dp na osobę), [[style-b]] v1.33
> (reguły 1, 2, 8, 14, kolory rodu).
>
> v0.3 (2026-10-17) — 19 wzorów, wspólny kadr (D13), pytania Ś3 i kolor. v0.2 (2026-10-17) — decyzje z prototypu (D5–D11), pilot.
> v0.1 (2026-10-16) — discovery: D1–D4, prompty 20 wzorów.

## Purpose
Wieniec przy portrecie mówi, z jakiego rodu osoba się wywodzi. Domyślnie dzieci przejmują go po ojcu (definicja autora z `/pm`
2026-10-16, [[2026-10-16-retro-04]] → *Product decisions*). Ród wybiera się raz, u osoby na szczycie linii, a reszta liczy się z drzewa.
Kobieta po ślubie nosi pół wieńca swojego rodu i pół rodu męża (D14).

## Navigation
- **Widok osoby** ([[osoba]] 3, 4a) i **drzewo** ([[drzewo]] 4, 11) tylko pokazują wieniec — bez akcji ([[style-b]] reguła 15).
- **[[wpis-osoby]] „poprawa” (✎) → wiersz „Wieniec rodu”** (wpis-osoby 4b, tylko w poprawie, D9):
  - „Wybierz ród” / „Zmień” → **arkusz „Wieniec rodu”** (E);
  - w arkuszu: ród → wybór zapisuje się od razu i arkusz się zamyka (D16); „Nowy ród” → **ekran „Nowy ród”** (F); ✎ przy rodzie → **ekran
    „Ród”** (F, poprawa rodu); „Bez wieńca” → zapis od razu, arkusz się zamyka;
  - „Zapisz ród” na ekranie „Nowy ród” → ród powstaje, ta osoba go dostaje, powrót do formularza (arkusz zamknięty); „Zapisz” na ekranie „Ród” →
    powrót do arkusza;
  - „Wróć do wieńca po ojcu” (w wierszu) → zapis od razu.
- Wstecz z arkusza i z ekranów F — bez zmian.

## Elements in order

### A. Wieniec — jeden element dla wszystkich miejsc
| # | Element | Szczegóły | Źródło |
|---|---|---|---|
| A1 | **Wzór** | jeden z 19 obrazów od autora (*Prompts* → lista, bez maku), jednobarwny; klucz wzoru w danych (A6) | D1, D2, D12 |
| A2 | **Kadr** | płótno kwadratowe = **2 × średnica portretu**; portret ma środek w (0,50; 0,434) płótna. Wieniec leży **pod** portretem: liście, które wchodzą pod okrąg, chowają się za nim (najwięcej lipa, 3,7% liści). Wymiary: portret 104 dp → płótno 208 dp (wieniec ok. 200 dp szeroki, 65 dp nad środkiem portretu, 99 dp pod nim); 44 dp → 88 dp (ok. 85 dp, 28 dp nad, 42 dp pod) | D13 |
| A3 | **Kolor** | kolor rodu z palety 12 (A6) | D3, D6 |
| A4 | **Cieniowanie C3** | przejście tonu (u końców gałązek jaśniej o 10%, przy węźle ciemniej o 16%) i tłoczenie (jasna krawędź liścia od lewej u góry, cień z drugiej strony, ±22%); **nigdy ciemniej niż 80% koloru rodu**. Liczone raz przy budowie z obrazu wzoru, nie przy każdej klatce ([[style-b]] reguła 2). **Barwienie (v1.1, odstępstwo 4):** plik niesie szarość, w której 50% to sam kolor rodu; aplikacja mnoży każdy kanał koloru przez jasność pliku i obcina do bieli (jeden filtr koloru, raz na parę wzór–kolor i rozmiar), zamiast przesuwać jasne miejsca „w stronę bieli” jak skrypt z discovery. Najciemniejsze miejsca bez zmian (80%), więc pomiar w *Style B rules applied* obowiązuje | D15 |
| A5 | **Obwódka w kolorze tła** | wokół każdego liścia, 0,75% płótna (1,5 dp przy 208 dp, 0,7 dp przy 88 dp) — **zawsze**, nie tylko na zdjęciu. Dzięki temu liść ma obok siebie kolor tła na zdjęciu, na paśmie bez zdjęcia (powierzchnia) i na drzewie, a kontrast liczy się wobec tła ([[style-b]] reguła 14). **Skąd (v1.1, odstępstwo 3):** obwódki nie ma w pliku wzoru — dokłada ją aplikacja przy barwieniu, kształtem liści w kolorze tła odsuniętym w 12 kierunkach, raz na parę i rozmiar. Plik zostaje szary (wyjątek strażnika — droga R planu przepuszcza tylko szare obrazy), kolor tła ma jeden dom w `theme.dart`, a grubość to zawsze 0,75% płótna na ekranie | prototyp panel 1 · D15 |
| A6 | **Pół na pół (Ś3)** | lewa połowa płótna (x < 0,5) z wieńca jednego rodu, prawa z drugiego, każda we wzorze i kolorze swojego rodu; łączą się na pionowej osi, w węźle | D14 |

**Klucze w danych** (wartości kolorów — w `theme.dart`, pisze `dev`; tu rola i pomiar w *Style B rules applied*):
- wzory: `laur` · `dab` · `klosy` · `jarzebina` · `lipa` · `brzoza` · `klon` · `kasztanowiec` · `bluszcz` · `dzika_roza` · `chaber` · `rumianek` ·
  `konwalia` · `wrzos` · `paproc` · `kalina` · `leszczyna` · `chmiel` · `jablon`;
- kolory: `stare_zloto` · `braz` · `miedz` · `srebro` · `kosc_sloniowa` · `grafit` · `patyna` · `oliwka` · `blekit` · `lawenda` · `wrzos` · `rubin`.

Nazwy po polsku na ekranie: jak w tabelach *Prompts* i *Style B rules applied*.

### B. Liczenie wieńca — reguły (z drzewa, przy otwarciu, nic poza wyborem nie jest zapisane)
| # | Reguła | Źródło |
|---|---|---|
| B1 | **Ojciec** = rodzic z płcią „mężczyzna” w rodzinie, w której osoba jest dzieckiem. Rodzic bez płci nie jest ojcem. Dziecko w kilku rodzinach — pierwsza zapisana | D7 |
| B2 | **Ród własny** osoby: wybrany przy niej ród → ten ród; wybrane „bez wieńca” → brak; nic nie wybrane → ród własny ojca; bez ojca → brak (**O1**). Pętla w drzewie (aplikacja dziś ich nie blokuje — CURRENT_STATE → *Poza tą kolejnością*) → brak, liczenie się nie zawiesza | D7, D9 |
| B3 | **Lewa połowa** = ród własny | D14 |
| B4 | **Prawa połowa:** osoba z płcią „kobieta”, która ma **małżeństwo** (nie „razem”) z mężczyzną → ród własny męża z **ostatniego** małżeństwa (późniejsza pierwsza data związku; bez dat — później zapisane, jak [[osoba]] 6). Inaczej prawa = lewa | D14 |
| B5 | **Brakująca połowa** → wieniec cały z drugiej. Obie brak → bez wieńca | D14 |
| B6 | **Dzieci dziedziczą ród własny ojca** (lewą część), nigdy połowy po mężu — ojciec jest mężczyzną, więc B4 go nie dotyczy | D7, D14 |
| B7 | Koniec związku („//”) i suwak czasu **nie zmieniają** wieńca: liczy się ostatnie małżeństwo z drzewa | D14 |

### C. Widok osoby ([[osoba]] v2.6)
| # | Element | Szczegóły |
|---|---|---|
| C1 | **Wieniec wokół portretu** (osoba 3) | płótno 208 dp, wyśrodkowane na portrecie 104 dp; górą wchodzi na pasmo tła (zdjęcie albo powierzchnia) — liście ma obwódka A5. Portret, jego pierścień i poświata leżą nad wieńcem; cel dotyku portretu bez zmian (104 dp). Wieniec nie przyjmuje dotyku (dotknięcie liścia nad pasmem to dotknięcie pasma). Portret bez zdjęcia (inicjały) — wieniec tak samo. **Poza czytnikiem** — ród czyta C2 |
| C2 | **Podpis rodu** (osoba 4a) | pod latami, 4 dp odstępu: „Ród: Wymyślscy” (14 sp, tekst pomocniczy, wyśrodkowany, zawija się); przy Ś3 „Ród: Zmyśleńscy · po mężu Wymyślscy” (twarda spacja U+00A0 po „·” — [[style-b]] reguła 6). Bez wieńca — bez podpisu |
| C3 | **Odstęp imienia** | z wieńcem imię zaczyna się **8 dp pod dolną krawędzią wieńca** (99 dp pod środkiem portretu; bez wieńca — jak dziś, 12 dp pod portretem). Treść zjeżdża o ok. 43 dp |

### D. Drzewo i tryb prezentacji ([[drzewo]] v1.19)
| # | Element | Szczegóły |
|---|---|---|
| D1 | **Wieniec na węźle** | płótno 88 dp na węźle 44 dp (A2); skaluje się z drzewem jak węzeł. Kolejność rysowania: linie → **wieńce** → węzły → znicz. **W węźle, nie na osobnej warstwie** (v1.1, odstępstwo 5, D18): każdy węzeł rysuje swój wieniec, na nim tabliczkę imienia, a na niej okrąg z pierścieniem, poświatą, przerywanym obrysem i zniczem na krążku 18 dp w kolorze tła (tabliczka pod okręgiem — jak od [[ISSUE-033-tree-from-a-person]]). Znicz i tabliczka leżą więc nad liśćmi, a wieniec gaśnie i wyszarza się razem z osobą (D4). Wieńce sąsiadów się nie nakładają: połowa wieńca 43 dp < połowa miejsca 48 dp |
| D2 | **Miejsce osoby z wieńcami** | **96 dp** zamiast 80 dp, gdy choć jedna osoba **w rodzinie** (całe drzewo w bazie, nie tylko pokazane) ma wieniec — v1.1, odstępstwo 1: miejsce nie zmienia się przy przestawieniu środka, więc drzewo nie skacze; bez rodów w bazie 80 dp jak dotąd. Z tekstem systemu `max(96, 80 × skala tekstu)`, najwyżej 160 dp. Rząd 104 dp bez zmian (wieniec sięga 6 dp nad węzeł i 20 dp pod niego, w pas imienia) |
| D3 | **Linie przy wieńcach** | linia pary widoczna w przerwie między wieńcami (ok. 11 dp przy 96 dp), „//” wypada w tej przerwie; linia rodzic–dziecko wchodzi w węzeł od góry przez otwarcie K2. **Ślad w bok** (partner poza widokiem) **osoby z wieńcem** zaczyna się **za wieńcem**, 43 dp od środka węzła, i ma 14 dp — inaczej leżałby pod liśćmi; osoby bez wieńca — przy okręgu, jak bez rodów (doprecyzowane w v1.1) |
| D4 | **Wyszarzenie i czas** | osoba poza ścieżką (krycie 30%) — wieniec razem z nią; osoba nieurodzona w roku suwaka — bez wieńca (nie ma węzła); pusty pierścień (C1 drzewa) — bez wieńca |
| D5 | **Gdzie nie ma wieńca** | karta osoby w środku (okrąg 40 dp), kafle „Połącz dwie osoby”, mini-drzewo w widoku osoby, łańcuch, lista osób, karta grobu (D10) |
| D6 | **Czytnik** | opis węzła bez zmian — ród czyta widok osoby (C2) |

### E. Formularz — wiersz „Wieniec rodu” ([[wpis-osoby]] 4b) i arkusz
| # | Element | Typ | Akcja | Szczegóły |
|---|---|---|---|---|
| E1 | **Wiersz „Wieniec rodu”** — etykieta „Wieniec rodu” (14 sp, tekst pomocniczy) nad ramką (obrys 1 dp, promień 8 dp, ≥ 64 dp, jak karta zamieszkania); w ramce: **znak wieńca 56 dp** (A, płótno 56 dp, w środku okrąg 28 dp z obrysem 1 dp — miejsce portretu) · dwie linie: nazwa rodu (16 sp, tekst) i wyjaśnienie (13 sp, tekst pomocniczy, zawija się) · **„Zmień”** (przycisk tekstowy w akcencie, ≥ 48 dp). Stany — tabela niżej. **Tekst ≥ 150%** (v1.1, odstępstwo 2, D19): znak i „Zmień” w rzędzie u góry ramki, linie pod nimi na całą szerokość | wiersz | „Zmień” / „Wybierz ród” → E2 | **tylko w poprawie**, poza `next`, po „Nazwisku rodowym” (4); zapis od razu, nie z „Zapisz” (D16) |
| E1a | **„Wróć do wieńca po ojcu”** — przycisk tekstowy w akcencie z `undo` pod ramką, gdy przy osobie jest wyjątek albo „bez wieńca”, a ojciec ma ród | przycisk | zapis od razu: wybór usunięty | AC-2 |
| E2 | **Arkusz „Wieniec rodu — Jan”** (dolny arkusz na powierzchni, tytuł 18 sp półgruby): **wiersz za każdy ród** (≥ 64 dp, A–Z): znak 56 dp · nazwa (16 sp) · „Dąb · Stare złoto · 7 osób” (13 sp, tekst pomocniczy; ród ojca — dopisek „· po ojcu”) · ✎ (`edit_outlined`, akcent, 48 dp, `tooltip` „Popraw ród”). Ród tej osoby ma `check` w akcencie przed ✎ i stan „zaznaczone” dla czytnika. Pod rodami: **„Nowy ród”** (`add`, akcent) i **„Bez wieńca”** (`block`, tekst pomocniczy) — ten tylko wtedy, gdy osoba ma albo dostałaby wieniec; wybrane — `check` w akcencie i stan „zaznaczone” (v1.1). Bez rodów: „Rodów jeszcze nie ma.” (16 sp, tekst pomocniczy) i „Nowy ród”. **Tekst ≥ 150%** (v1.1, odstępstwo 2, D19): w wierszu rodu znak, `check` i ✎ w rzędzie u góry, nazwa i opis pod nimi na całą szerokość | arkusz | ród → wybór, zapis, zamknięcie; ród ojca → usuwa wyjątek; ✎ → F (poprawa); „Nowy ród” → F; „Bez wieńca” → zapis, zamknięcie | D9, D16 |

**Stany wiersza E1** (imiona i nazwiska bez odmiany — dwukropek):

| Stan | Znak | Linia 1 | Linia 2 | Działania |
|---|---|---|---|---|
| bez ojca, nic nie wybrane (O1) | okrąg 28 dp w miejscu portretu znaku 56 dp, obrys przerywany 4/3 (v1.1; było 40 dp) | „Brak” | „Ojca nie ma w drzewie, więc wieniec nie ma po kim przyjść.” | przycisk z obrysem **„Wybierz ród”** (`add`, akcent) pod linią 2, zamiast „Zmień” |
| ojciec bez rodu, nic nie wybrane | jak wyżej | „Brak” | „Ojciec: Józef Wymyślski — bez wieńca.” | „Wybierz ród” |
| po ojcu | wieniec | „Wymyślscy” | „Po ojcu: Józef Wymyślski.” | „Zmień” |
| wybrany tutaj (szczyt linii) | wieniec | „Wymyślscy” | „Wybrane tutaj. Po tej osobie wieniec mają: Jan, Maria, Kasia i 3 inne osoby.” (do 3 imion, potem liczba; bez potomków — samo „Wybrane tutaj.”) | „Zmień” |
| wyjątek | wieniec | „Przykładowscy” | „Wybrane tutaj. Po ojcu byłoby: Wymyślscy.” | „Zmień” · E1a |
| bez wieńca (wybrane) | okrąg przerywany | „Bez wieńca” | „Wybrane tutaj. Po ojcu byłoby: Wymyślscy.” | „Zmień” · E1a |
| kobieta po ślubie (Ś3) | wieniec pół na pół | ród własny, jak wyżej | linia jak wyżej + „Po ślubie prawa połowa: Wymyślscy (mąż: Józef Wymyślski).” | jak wyżej — „Zmień” zmienia jej ród, czyli lewą połowę (B3) |
| ona bez rodu, mąż z rodem (B5; v1.1) | cały wieniec męża | „Brak” | linia jej stanu („Ojca nie ma w drzewie…”) + „Po ślubie wieniec męża: Wymyślscy (mąż: Józef Wymyślski).” | „Wybierz ród” |

Opis wiersza dla czytnika (v1.1): **dwa węzły** — słowa („Wieniec rodu”, nazwa, linie) i osobno przycisk „Zmień wieniec rodu” / „Wybierz ród”. W jednym
węźle przycisk scalał się z tekstem i tracił cel 48 dp (*Dev report* → *Znalezione* 1; było: „Wieniec rodu: Wymyślscy, po ojcu — zmień”).

### F. Ekran „Nowy ród” / „Ród” (poprawa rodu)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja |
|---|---|---|---|---|---|
| F1 | **Pasek:** ← i tytuł „Nowy ród” / „Ród” | pasek | wstecz → bez zmian | — | — |
| F2 | **Nazwa** — podpowiedź „np. Wymyślscy” | pole tekstowe, wielka litera na początku słów | `done` | pusto (poprawa — nazwa) | wymagana: „Wpisz nazwę rodu.”; inna niż istniejące, bez wielkości liter: „Taki ród już jest — wybierz go z listy.” (poprawa — poza nim samym) |
| F3 | **Kolor** — etykieta „Kolor” (14 sp, tekst pomocniczy); **12 kół 36 dp** w celach 48 dp, 6 w rzędzie, w kolejności palety; wybrane: pierścień 2 dp w akcencie z odstępem 2 dp w kolorze tła i `check` w kolorze tła w kole; pod kołami „Kolor: Stare złoto” (13 sp, tekst pomocniczy). Opis koła dla czytnika: nazwa koloru, stan „zaznaczone” | wybór jednokrotny | dotknięcie → wybór; siatka F4 przyjmuje ten kolor | **pierwszy kolor palety, którego nie ma żaden ród** (wszystkie zajęte — pierwszy) | — |
| F4 | **Wzór** — etykieta „Wzór”; **siatka 3 kolumn**, 19 kafli (obrys 1 dp, promień 12 dp, ≥ 104 dp szerokie; wysokość z treści, rząd tak wysoki jak najwyższy kafel — v1.1, ok. 100 dp bez „też”; **tekst ≥ 150% — 2 kolumny**, nazwa wzoru i każda nazwa rodu w „też” w jednej linii, raczej trochę mniejsza niż złamana w środku słowa — v1.1, odstępstwo 2, D19); treść kafla wyśrodkowana: znak wieńca 72 dp w wybranym kolorze (A, z C3) · nazwa wzoru (13 sp, tekst) · „też: Zmyśleńscy” (13 sp, tekst pomocniczy), gdy inny ród ma ten wzór **w wybranym kolorze** (v1.2, D20; zmiana koloru w F3 przelicza „też”). Wybrany: obrys 2 dp w akcencie i `check` w akcencie w rogu, stan „zaznaczone” | wybór jednokrotny | dotknięcie → wybór | **pierwszy wzór, którego nie ma żaden ród**; gdy każdy wzór ma już ród — pierwszy, którego żaden ród nie ma w kolorze z F3 (v1.2, D20) | — |
| F5 | **Kogo dotyczy** (14 sp, tekst pomocniczy): nowy — „Wieniec dostanie Jan Wymyślski, a po nim, po linii ojca, 4 osoby: Maria, Kasia, Tomek i Zosia.” (do 4 imion, potem „i N innych”; bez potomków — samo „Wieniec dostanie Jan Wymyślski.”); poprawa — „Zmiana dotyczy 7 osób.” (osoby z tym rodem w wieńcu, także w połowie) | tekst | — | — | — |
| F6 | **„Zapisz ród”** (nowy) / **„Zapisz”** (poprawa) — przycisk wypełniony, przypięty na dole nad klawiaturą | przycisk | zapis od razu (ród, a przy nowym — także wybór dla tej osoby), powrót (*Navigation*) | — | błąd F2 → komunikat pod polem, fokus |

**Usuwania rodu nie ma** (D16). Błąd zapisu (E, F): komunikat u dołu ekranu „Nie udało się zapisać wieńca. Spróbuj jeszcze raz.”, nic się nie zmienia.

**Dane, których ekrany potrzebują** (dla `planning`):
- **ród:** nazwa, klucz wzoru, klucz koloru — nowa tabela (zmiana schematu, test migracji; kopia i eksport ją niosą — AC-3,
  [[ADR-018-export-is-the-backup]]);
- **osoba:** wybór rodu — nic (dziedziczy) · ród · „bez wieńca”;
- do liczenia (B): rodziny (rodzice z płcią, dzieci), związki (rodzaj: małżeństwo albo razem, pierwsza data, kolejność zapisu);
- **obrazy 19 wzorów** z cieniowaniem C3 — w aplikacji (droga: *Open* → *Dla `planning`*); wartości 12 kolorów — `theme.dart`.

## States
| Stan | Widok osoby | Drzewo | Formularz (E1) |
|---|---|---|---|
| bez rodów w bazie (dziś) | portret jak dziś, bez podpisu | 80 dp na osobę, bez wieńców | „Brak” + „Wybierz ród” |
| ród po ojcu | wieniec, „Ród: X” | wieniec | „Po ojcu: …” |
| ród wybrany przy osobie | wieniec, „Ród: X” | wieniec | „Wybrane tutaj. Po tej osobie …” |
| wyjątek / bez wieńca | wieniec wybranego rodu / portret jak dziś | tak samo | + „Wróć do wieńca po ojcu” |
| kobieta po ślubie (Ś3) | pół na pół, „Ród: X · po mężu Y” | pół na pół | + linia „Po ślubie prawa połowa: …” |
| mąż bez rodu / ona bez rodu (B5) | cały wieniec z drugiej połowy; podpis: „Ród: X” albo „Ród: po mężu Y” | tak samo | jak stan jej rodu |
| portret bez zdjęcia | wieniec wokół okręgu z inicjałami | — | — |
| zapis wyboru (E, F) | — | — | od razu; wiersz pokazuje nowy stan |
| błąd zapisu | — | — | „Nie udało się zapisać wieńca. Spróbuj jeszcze raz.”, bez zmian |
| obraz wzoru bez odczytu | portret bez wieńca (nic na jego miejscu) | węzeł bez wieńca | znak: okrąg z obrysem |

## Sketch
```
Widok osoby (C)                          Formularz — poprawa (E1)
┌──────────────────────────────────┐     ┌──────────────────────────────────┐
│ ←                              ✎ │     │ ✕  Poprawa wpisu          Zapisz │
│▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓│     │            ( zdjęcie )            │
│▓▓▓▓▓\\▓▓▓▓▓╭────────╮▓▓▓▓▓//▓▓▓▓│     │ Imiona                     ♀  ♂  │
│    \\\     │ portret│     ///     │     │ Nazwisko                          │
│     \\\    ╰────────╯    ///      │     │ Nazwisko rodowe (z domu)          │
│       \\\\\    ⌒⌒    /////        │     │ Wieniec rodu                      │
│            \\\\ ⋈ ////            │     │ ┌──────────────────────────────┐ │
│   Anna Wymyślska z d. Zmyśleńska │     │ │ (w) Zmyśleńscy        Zmień  │ │
│            1903–1980             │     │ │     Po ojcu: Jan Zmyśleński. │ │
│ Ród: Zmyśleńscy · po mężu Wymyśl.│     │ │     Po ślubie prawa połowa:  │ │
│  (lewa gałązka — laur, patyna;   │     │ │     Wymyślscy (mąż: Józef …) │ │
│   prawa — dąb, stare złoto)      │     │ └──────────────────────────────┘ │
└──────────────────────────────────┘     │ Urodzenie …                       │

Arkusz „Wieniec rodu — Jan” (E2)         Nowy ród (F)
┌──────────────────────────────────┐     ┌──────────────────────────────────┐
│              ────                │     │ ←  Nowy ród                       │
│ Wieniec rodu — Jan               │     │ Nazwa  [ np. Wymyślscy          ]│
│ (w) Przykładowscy             ✎  │     │ Kolor                             │
│     Jarzębina · Lawenda · 3 osoby│     │ ● ● ● ● ● ●                       │
│ (w) Wymyślscy              ✓  ✎  │     │ ● ● ● ● ● ●   Kolor: Stare złoto  │
│     Dąb · Stare złoto · 7 · po o.│     │ Wzór                              │
│ +   Nowy ród                     │     │ [laur][dąb ✓][kłosy]              │
│ ⊘   Bez wieńca                   │     │ [jarz.][lipa][brzoza] …           │
└──────────────────────────────────┘     │ Wieniec dostanie Jan Wymyślski, a │
                                          │ po nim … 4 osoby: …               │
Drzewo (D), 96 dp na osobę                │ [        Zapisz ród             ] │
   \(Jó)/ ━━━ \(An)/                      └──────────────────────────────────┘
   Józef        Anna
```

## Tempo
Wybór rodu jest **raz na linię**, a nie raz na osobę (D9). Akcje:
- **szczyt linii, nowy ród:** ✎ w widoku (1) · „Wybierz ród” (1) · „Nowy ród” (1) · nazwa (ok. 10 znaków, jedna klawiatura) · kolor i wzór (0, gdy
  domyślne — pierwsze wolne; inaczej 2) · „Zapisz ród” (1) · wstecz z formularza bez „Zapisz” (1) — **5–7 dotknięć i nazwa**;
- **szczyt linii, ród już jest:** ✎ · „Wybierz ród” · ród · wstecz — **4 dotknięcia**;
- dzieci, wnuki i kobiety po ślubie — **0** (liczone z drzewa).

Przy ok. 100 osobach i ok. 10–15 liniach to ok. 60–100 dotknięć na całą rodzinę, a nie na osobę. Formularz nowej osoby („nowy grób”,
„kolejna osoba”) nie ma wiersza — tempo przepisywania (G6) bez zmian.

## Style B rules applied
- **Reguła 1 (jeden akcent) — wyjątek (D3, D6).** Wieniec ma kolor rodu z palety 12 kolorów, a nie akcent. Bursztyn zostaje dla działań, fokusu i
  wyboru: pierścień portretu, „Zmień”, `check` i obrys wybranego kafla w F. Na ekranie F jedyny wypełniony przycisk to „Zapisz ród”.
- **Reguła 2 (głębia subtelna).** Cieniowanie C3 jest częścią obrazu wzoru, liczone raz przy budowie — nie gradient tła i nie rozmyty cień w
  klatce (przy ok. 100 węzłach rozmyte cienie szarpały ruch — [[drzewo]] D23).
- **Reguła 8 (bez symboli religijnych).** Motywy to rośliny bez znaczenia religijnego. Poza zestawem są: palma i cierń (symbole religijne),
  lilia (symbol maryjny), oliwka (gałązka z gołębicą) i winorośl. Nie ma też gałązek iglastych (świerk, jodła, tuja), bo to materiał
  wieńców pogrzebowych, a styl B jest „bez ponurości”. **Wieniec zastępuje „bez gałązek”** ([[osoba]] D3, v2.6).
- **Reguła 14 (nic na zdjęciu).** Liście nad pasmem tła mają obwódkę w kolorze tła (A5), tak jak ramka kadru.
- **Reguła 15.** Widok i drzewo tylko pokazują; wybór — pod ✎.
- **Reguła 6.** „Ród: X · po mężu Y” — twarda spacja (U+00A0) po „·”.
- **Kontrast (SC 1.4.11).** Każdy kolor rodu ma ≥ 3:1 na tle także w najciemniejszych 5% liści po cieniowaniu C3; obwódka A5 sprawia, że liść
  zawsze sąsiaduje z kolorem tła (na powierzchni bez obwódki brąz miałby w cieniu ok. 2,8:1). Ród rozpoznaje się po wzorze i podpisie C2, a
  kolor go wspiera (SC 1.4.1). Obok akcentu każdy kolor ma < 3:1 — wieniec i pierścień rozdziela obwódka A5.

**Paleta kolorów rodu (D6) i C3 (D15), wzór WCAG, 2026-10-17** (płaski kolor; po C3 — liście lauru, dębu, lipy i kasztanowca w pikselach):

| Kolor | Wartość | płaski na tle | płaski na powierzchni | obok akcentu | C3: najciemniejsze 5% / mediana na tle |
|---|---|---|---|---|---|
| Stare złoto | `#A88B57` | 5,83:1 | 5,32:1 | 1,51:1 | 3,93 / 5,32 |
| Brąz | `#A0714F` | 4,46:1 | 4,07:1 | 1,97:1 | **3,10** / 4,08 |
| Miedź | `#C07A55` | 5,53:1 | 5,05:1 | 1,59:1 | 3,73 / 5,06 |
| Srebro | `#A9ACAF` | 8,27:1 | 7,55:1 | 1,07:1 | 5,38 / 7,53 |
| Kość słoniowa | `#D8CFB8` | 12,16:1 | 11,09:1 | 1,38:1 | 7,69 / 10,98 |
| Grafit | `#8E8A84` | 5,50:1 | 5,01:1 | 1,60:1 | 3,72 / 5,01 |
| Patyna | `#6FA08C` | 6,36:1 | 5,80:1 | 1,38:1 | 4,25 / 5,78 |
| Oliwka | `#8E9A5A` | 6,22:1 | 5,67:1 | 1,42:1 | 4,16 / 5,63 |
| Błękit | `#7FA3C7` | 7,15:1 | 6,53:1 | 1,23:1 | 4,71 / 6,50 |
| Lawenda | `#A08CC0` | 6,29:1 | 5,74:1 | 1,40:1 | 4,22 / 5,72 |
| Wrzos | `#C28BA0` | 6,73:1 | 6,14:1 | 1,31:1 | 4,47 / 6,12 |
| Rubin | `#C0707A` | 5,25:1 | 4,79:1 | 1,68:1 | 3,55 / 4,78 |

Wartości trafiają do `theme.dart` (pisze `dev`), a do [[style-b]] — rola i ten pomiar.

## AC → element
AC-1…AC-3 z [[ISSUE-044-family-wreaths]]; AC-4…AC-6 — **propozycje `ui` z discovery** (D14, D10, D3) do przyjęcia przez `planning` na stopie #1.

| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| AC-1 — ojciec z wieńcem, dziecko dostaje go bez kroku | B2 · C1 · D1 · E1 „po ojcu” | Józef ma ród Wymyślscy (wybrany u niego); dodaję mu syna Jana → widok Jana: dąb w starym złocie, „Ród: Wymyślscy”; w poprawie Jana „Po ojcu: Józef Wymyślski.” |
| AC-2 — zmiana ręczna dotyczy tej osoby, reszta rodu zostaje | E1 wyjątek · E1a · E2 · B2 | u Jana „Zmień” → Przykładowscy: Jan i jego dzieci mają jarzębinę, Józef i siostra Maria — dąb; „Wróć do wieńca po ojcu” przywraca dąb u Jana i jego dzieci |
| AC-3 — kopia sprzed pozycji odtwarza się kompletna | dane (*Elements* → *Dane*) | test migracji i próbne odtworzenie: kopia sprzed pozycji → wszystko jest, rodów brak, wieńców brak |
| AC-4 *(propozycja)* — kobieta po ślubie: pół panieński, pół po mężu | B4–B6 · A6 · C2 | Anna z d. Zmyśleńska, ślub z Józefem: lewa połowa laur w patynie, prawa dąb w starym złocie, „Ród: Zmyśleńscy · po mężu Wymyślscy”; jej syn Jan — cały dąb |
| AC-5 *(propozycja)* — wieńce na drzewie i w trybie prezentacji, pary się nie nakładają | D1–D3 | drzewo z wieńcami: 96 dp na osobę, linia pary widoczna między wieńcami; tryb prezentacji — te same wieńce |
| AC-6 *(propozycja)* — zmiana koloru albo wzoru rodu zmienia go u wszystkich | F (poprawa) · E2 ✎ | ✎ przy Wymyślscy → kolor Miedź → „Zmiana dotyczy 7 osób.” → u Józefa, Jana i połowie Anny dąb w miedzi |

## Decisions
- **D1 — rysunki wieńców z DALL-E** (2026-10-16, decyzja autora; było już w [[ISSUE-044-family-wreaths]] → *What to build*). Autor: *„to ma
  być prompty do wygenerowania w DALLe”*. `ui` pisze prompty (*Prompts*), autor generuje i odsyła. *Obali:* obrazy nie trzymają wspólnego kadru
  albo nie dają się zamienić na jednobarwne — pilot i pomiar 19 pokazały, że trzymają (D12, D13).
- **D2 — ok. 20 wzorów do wyboru dla rodu** (2026-10-16, decyzja autora): *„około 20 różnych wieńców do zaznaczenia rodziny”*. Jeden wzór może
  mieć kilka rodów, bo w polskiej heraldyce jeden herb nosiło wiele rodzin
  ([MyHeritage — Polish nobility surnames](https://www.myheritage.com/wiki/Polish_nobility_surnames)). Wybór pokazuje, kto już go używa (F4) — od v1.2
  w tym samym kolorze (D20).
- **D3 — kolor wieńca do zmiany** (2026-10-16, decyzja autora): *„które dodatkowo można modyfikować kolorystycznie”*. Każdy wzór jest
  jednobarwny, a kolor nakłada aplikacja; kolor i wzór rodu zmienia ekran „Ród” (F, AC-6).
- ~~**D4 — kadr wspólny przez puste koło 56%**~~ (2026-10-16) — **zastąpione przez D13**: DALL-E nie trzyma wielkości pustego koła (43–58%).
- **D5 — kształt K2:** wieniec otwarty u góry, dwie gałązki złączone na dole (2026-10-17, decyzja autora — rekomendacje prototypu przyjęte w
  całości: *„ok akceptuję prototyp”*).
- **D6 — kolor rodu z palety 12 kolorów**, a nie dowolny (j.w.). Dowolny kolor mógłby zniknąć na tle.
- **D7 — L1: cały wieniec po ojcu**, jeden ród własny na osobę (j.w.). L2 (linia matki w drugiej połowie) liczyłby się z tych samych zapisów, ale
  D14 zajął prawą połowę inaczej.
- ~~**D8 — Ś1: kobieta po ślubie zostaje przy wieńcu rodu ojca**~~ (2026-10-17) — **zastąpione przez D14**.
- **D9 — ród wybiera się raz, u osoby na szczycie linii, w „Popraw wpis” (✎)**; wyjątek przy jednej osobie, jej dzieci dziedziczą wyjątek. **O1:**
  osoba bez ojca w drzewie nie ma wieńca, dopóki ktoś go nie wybierze (j.w.).
- **D10 — G2: wieniec w widoku osoby i na drzewie, także w trybie prezentacji** (j.w.). Nie ma go w okręgach 40 dp i mniejszych (D5 w *Elements* D).
- **D11 — podpis „Ród: …” pod latami** (decyzja projektowa z prototypu, przyjęta). Niesie ród dla czytnika (SC 1.4.1).
- **D12 — pilot przyjęty, 19 z 20 wzorów** (2026-10-17, decyzja autora): po `pilot-grid.png` autor wygenerował resztę tym samym promptem.
  **Bez maku (11)** — 19 mieści się w D2; mak może dojść aktualizacją ze sklepu (nowy obraz i klucz, bez zmiany schematu).
- **D13 — wspólny kadr bez skalowania pojedynczych wzorów** (2026-10-17, decyzja projektowa `ui` po pomiarze 19). Puste koło waha się 43–58% i
  „pływa” w pionie przy kształcie U, ale **zewnętrzny kadr trzyma się we wszystkich 19**: boki 1,3–4,2% od brzegu, góra 12–23%, węzeł 89–91%
  wysokości. Portret 50% płótna w (0,50; 0,434), liście pod portretem chowają się za nim (najwięcej lipa 3,7%). Jedno miejsce w układzie dla
  wszystkich wzorów, wymiana wzoru nie przesuwa ekranu. *Obali:* wzór dodany później z węzłem poza 89–91% albo krawędzią bliżej niż 1% od brzegu
  — idzie do ponownego wygenerowania.
- **D14 — Ś3: kobieta po ślubie nosi pół wieńca panieńskiego i pół rodu męża** (2026-10-17, **pomysł i decyzja autora**: *„jeżeli kobieta wychodzi
  za mąż to połowa jej wieńca zmienia się na mężowy a połowa zostaje z części panieńskiej”*; po panelu 8 — *„jest super idźmy zgodnie z twoją
  rekomendacją”*). Lewa — skąd przyszła, prawa — do jakiej rodziny weszła. K2 dzieli się na dwie gałązki bez sztuczek. Zasady B4–B7 to
  decyzje projektowe `ui`, przyjęte z rekomendacją. Bazy nie zmienia. *Obali:* przy rodzinie z powtórnymi ślubami autor chce widzieć wszystkich
  mężów — wtedy prawa połowa nie wystarczy.
- **D15 — kolor C3: tłoczenie i przejście tonu** (2026-10-17, **decyzja autora**: *„chciałbym żeby ten kolor był mniej płaski”*, po panelu 9 —
  rekomendacja przyjęta). Kanon: gałązki w R4 mają przejście tonu; [[style-b]] reguła 2 zabrania tylko gradientów tła i rozmytych cieni w klatce.
  Cieniowanie wpieczone w obraz wzoru (A4), najciemniej 80% koloru — wszystkie 12 kolorów ≥ 3,10:1. *Obali:* na telefonie w słońcu wieniec C3
  czyta się gorzej niż płaski — wtedy C1 (mniej cienia).
- **D16 — wybór rodu i ród zapisują się od razu, bez „Zapisz” formularza** (2026-10-17, decyzja projektowa `ui`). Tak samo działa sekcja „Rodzina”
  w tym samym formularzu ([[rodzina]] D1: kreator zapisuje własną transakcją): wieniec, jak rodzina, dotyczy innych osób — dzieci, wnuków, żon.
  Ród utworzony na ekranie F od razu dostaje ta osoba, więc nie zostają rody, których nikt nie użył. **Usuwania rodu nie ma** w tej pozycji: ród
  da się poprawić (nazwa, kolor, wzór), a osoba może mieć „Bez wieńca”. *Obali:* autor tworzy ród przez pomyłkę i chce go usunąć — wtedy „Usuń
  ród” na ekranie F, gdy nikt go nie ma.
- **D17 — drzewo z wieńcami: 96 dp na osobę zamiast 80** (2026-10-17, decyzja projektowa `ui`, pokazana autorowi na panelu 8). Przy 80 dp wieńce par
  wchodzą na siebie i zasłaniają linię pary; przy 96 dp zostaje ok. 11 dp przerwy. Koszt: drzewo o 20% szersze — tylko wtedy, gdy ktoś w drzewie
  ma wieniec (D2 w *Elements* D; **v1.1, odstępstwo 1 `dev`: ktoś w całej rodzinie**, nie w pokazanym kawałku — inaczej miejsce zmieniałoby się przy
  przestawieniu środka i drzewo by skakało; koszt: rodzina z jednym rodem ma drzewo o 20% szersze wszędzie). *Obali:* przy 106 osobach na poziomie 4 drzewo przestaje mieścić rodzinę w kadrze trybu prezentacji — wtedy
  wieniec na drzewie mniejszy niż kadr A2 (liście głębiej pod węzłem).
- **D18 — wieniec w węźle drzewa, nie na osobnej warstwie** (2026-10-17, v1.1, odstępstwo 5 `dev` przyjęte w przeglądzie `ui`). Węzeł rysuje swój
  wieniec pod tabliczką imienia i okręgiem, więc wieniec gaśnie przy przestawieniu środka i wyszarza się na ścieżce razem z osobą (D4) bez osobnego
  krycia dla każdego wieńca — przenikanie grupy zostaje jedną warstwą (retro 4, R3). Wieńce sąsiadów się nie stykają (43 dp < 48 dp), a pomiar klatek
  `dev` (naprzemiennie z buildem odniesienia) nie pokazał straty. Cena: wieniec węzła rysowanego później leży nad tabliczką węzła rysowanego wcześniej,
  gdy tabliczka wyjdzie poza swoje miejsce. *Obali:* zrzut, na którym przy oddaleniu (imię nie maleje, I2) liście sąsiada leżą na literach imienia —
  wtedy wszystkie wieńce na jednej warstwie pod węzłami, z kryciem grupy jak linie (jedna warstwa).
- **D19 — duży tekst w wierszu, arkuszu i kaflach** (2026-10-17, v1.1, odstępstwo 2 `dev` przyjęte w przeglądzie `ui`). Przy tekście ≥ 150% (ten sam próg
  co „Pokaż ›” w karcie drzewa, [[drzewo]] D20) znak i przyciski idą w rząd nad tekstem, a tekst bierze całą szerokość; wzory w 2 kolumnach, nazwa
  wzoru i nazwy rodów w jednej linii, a gdy się nie mieszczą — trochę mniejsze. Na 360 dp przy 200% nazwy łamały się w środku słowa („Wymyslono / wie”,
  „Kasztan / owiec”; zrzuty 23, 24, 27, 28 przejścia `dev`), a [[osoba]] v2.2 zabrania łamania słów. Zmniejszenie dotyczy jednego słowa w kaflu, nie
  treści ciągłej. *Obali:* nazwa rodu tak długa, że w jednej linii przy 200% jest mniejsza niż przy 100% — wtedy w kaflu przy dużym tekście sama liczba
  („też: 2 rody”), a nazwy czyta się w arkuszu E2.
- **D20 — ród odróżnia para wzór + kolor** (2026-10-17, v1.2, decyzja autora na stopie #2 [[ISSUE-044-family-wreaths]]). Autor, po założeniu rodu z
  kłosami w innym kolorze niż ród, który już miał kłosy: *„każdy kolor chciałbym traktować osobno (np. nie ma znaczenia, że ktoś ma kłosy, tak długo jak nie
  dzielą tego samego koloru)”*. „też: …” na kaflu (F4) ostrzega więc tylko przed tą samą parą — dwa rody z kłosami w różnych kolorach to dwa różne wieńce, tak
  jak w heraldyce jeden herb różnych rodzin (D2). Domyślny wybór nowego rodu dalej zaczyna od koloru i wzoru, których nie ma nikt (więcej różnorodności na
  drzewie); dopiero gdy wzory się skończą, bierze pierwszy wolny w danym kolorze. Tej samej pary aplikacja nie blokuje — „też” zostaje ostrzeżeniem, jak
  w D2. *Obali:* dwa rody z tym samym wzorem w podobnych kolorach (np. brąz i miedź) mylą się na drzewie — wtedy „też” także przy kolorze sąsiednim.

## Open
**Pytań do autora o ekran — brak.** Punkty dla `planning` niżej — **wszystkie rozstrzygnięte** (v1.2, [[ISSUE-044-family-wreaths]]): obrazy — droga R
na stopie #1 (wyjątek dla szarych `wieniec-*.png`, [[ADR-021-clans-choice-at-the-person]]); klatki — z wieńcami nie gorsze od buildu odniesienia (*Dev
report* → *Emulator pass*); pętle — test `wreaths_test` (brak wieńca, bez zawieszenia).
- ~~**Obrazy wzorów w aplikacji — decyzja autora przez `planning`:**~~ `grobing-code/.gitignore` i strażnik danych rodziny nie przepuszczają `*.png`
  poza `android/app/src/main/res/`. Drogi: (a) obrys wektorowy jednobarwnych obrazów — bez plików graficznych; cieniowanie C3 aplikacja liczy
  wtedy raz na wzór i zapamiętuje obraz (nie w każdej klatce); (b) wyjątek w `.gitignore` i w strażniku dla jednego katalogu wieńców — obrazy
  z cieniowaniem gotowe przy budowie. Wyjątek zmienia ochronę danych rodziny, więc decyduje autor.
- ~~**Klatki drzewa:**~~ do ok. 100 wieńców na klatkę — z gotowych obrazów (jeden na ród albo parę rodów i wielkość), bez rozmycia i bez warstwy
  krycia na węzeł; pomiar naprzemiennie z buildem odniesienia (retro 4, R3).
- ~~**Pętle w drzewie**~~ (B2): liczenie po ojcach z pamięcią odwiedzonych.

## Prompts
**Jak generować:**
1. **Pilot — laur i dąb, potem reszta.** Zrobione 2026-10-17 (D12, D13): prompt bez zmian. Wzór idzie do ponownego wygenerowania, gdy ma kolor
   (nasycenie piksela > 25; wszystkie 19 mają ≤ 14), węzeł poza 89–91% wysokości, krawędź bliżej niż 1% od brzegu albo zamkniętą górę.
2. Wszystkie wzory **w jednej rozmowie z ChatGPT**. Przy kolejnych możesz dopisać: *„Same style, same size and composition as the previous
   wreath”*.
3. Zapis: PNG, **poza trzema repo** — np. w Pobranych. Nazwa z ChatGPT wystarczy, bo `ui` rozpozna wzór po obrazie. W czacie wystarczy
   napisać, że są.

**Baza promptu** (po angielsku, bo DALL-E lepiej trzyma wtedy szczegóły kadru). `[WZÓR]` zastępuje opis z listy niżej.

```
Flat emblem artwork on a 1024x1024 square canvas with a solid pure black #000000 background filling the whole square. In the centre, a botanical wreath shaped as a ring that is open at the top: two curved branches start together at the bottom centre, where their stems cross and are tied with a small simple knot, then rise along the left and right sides of an empty central circle and end a little above its middle height, so the top third of the ring stays open. The empty central circle is about 56% of the canvas width (about 575 px across) and must stay completely empty and black — a portrait photo will be placed there. The whole wreath fits inside a centred circle about 94% of the canvas width, with a clear margin on every side. The wreath is made of: [WZÓR]. Pure white #FFFFFF flat silhouette, one colour only: no grey, no gradient, no shading, no glow, no texture, no 3D, no photorealism. Leaf veins and small details as thin black cut-outs inside the white shapes. Shapes bold and simple enough to stay recognisable when the whole wreath is only 70 px wide. The left and right branches mirror each other. No text, no letters, no ribbons with writing, no animals, no people, no candles, no crosses, no religious symbols of any kind. Elegant, calm, modern, minimal and dignified; nothing gloomy.
```

**Wzory (20; 19 od autora — bez maku):**

| Nr | Wzór | Klucz | `[WZÓR]` |
|---|---|---|---|
| 01 | Laur | `laur` | slender pointed laurel leaves arranged in pairs along each branch, with a few small round berries |
| 02 | Dąb | `dab` | lobed oak leaves with wavy rounded edges and a few acorns with textured caps |
| 03 | Kłosy | `klosy` | ears of wheat with plump grains and fine straight awns, with a few long narrow blades of grass-like leaves |
| 04 | Jarzębina | `jarzebina` | rowan: feather-like compound leaves made of small narrow leaflets, with clusters of small round berries |
| 05 | Lipa | `lipa` | linden: heart-shaped leaves with finely toothed edges, with small hanging clusters of linden blossoms on narrow wing-like bracts |
| 06 | Brzoza | `brzoza` | birch: small diamond-shaped leaves with toothed edges on thin drooping twigs, with a few slender catkins |
| 07 | Klon | `klon` | five-pointed maple leaves and a few pairs of winged maple seeds |
| 08 | Kasztanowiec | `kasztanowiec` | horse chestnut: palm-shaped leaves made of five to seven long leaflets, with a few spiky round husks, one split open showing a smooth nut |
| 09 | Bluszcz | `bluszcz` | a winding ivy vine with three- and five-lobed ivy leaves of different sizes |
| 10 | Dzika róża | `dzika_roza` | simple five-petal wild rose flowers, small serrated leaves and oval rose hips |
| ~~11~~ | ~~Mak~~ | — | open poppy flowers with four rounded petals, round seed capsules with a crown on top, and deeply cut leaves — **nie wygenerowany** (D12) |
| 12 | Chaber | `chaber` | cornflower blossoms with ragged fringed petals, slim closed buds and narrow leaves |
| 13 | Rumianek | `rumianek` | small daisy-like chamomile flowers with many thin rays around a round centre, and fine feathery leaves |
| 14 | Konwalia | `konwalia` | lily of the valley: arching stems with rows of small bell-shaped flowers and broad smooth pointed leaves |
| 15 | Wrzos | `wrzos` | dense sprigs of heather covered with tiny bell-like flowers |
| 16 | Paproć | `paproc` | curved fern fronds with many small leaflets and a few young curled fiddleheads |
| 17 | Kalina | `kalina` | guelder rose: three-lobed maple-like leaves with hanging clusters of round berries |
| 18 | Leszczyna | `leszczyna` | hazel: rounded leaves with pointed tips and toothed edges, with hazelnuts in frilly husks |
| 19 | Chmiel | `chmiel` | a twining hop vine with three-lobed leaves and pine-cone-like hop cones |
| 20 | Jabłoń | `jablon` | apple twigs with five-petal blossoms, round buds, oval leaves and a few small apples |

**Obrazy autora** (poza repo, Pobrane, 2026-10-17 15:07–15:34): kolejność zapisu = kolejność wzorów 01–20 bez 11. Do budowy kopiuje je `dev` według
drogi z *Open*; pomiar: skrypty `measure_all.py` i `frame_all.py` w katalogu tymczasowym sesji `3c71c787-…\\scratchpad`.
