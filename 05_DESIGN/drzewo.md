---
screen: "Drzewo — rodzina od osoby, poziomy połączeń, czas; połącz dwie osoby"
items: ["[[SPIKE-004-mvp-flow-prototype]]", "[[ISSUE-024-person-view]]", "[[SPIKE-002-tree-on-a-phone]]", "[[US-009-drzewo-od-osoby]]", "[[ISSUE-033-tree-from-a-person]]", "[[ISSUE-034-tree-presentation-mode]]", "[[ISSUE-035-tree-names-shrink-my-voice]]", "[[ISSUE-036-cast-from-the-app]]", "[[ISSUE-037-time-on-the-tree]]", "[[ISSUE-038-history-on-tv-and-tempo]]", "[[ISSUE-039-connect-two-people]]", "[[ISSUE-044-family-wreaths]]"]
us: "[[US-009-drzewo-od-osoby]] (M9) · [[US-010-czas-na-drzewie]] (M10) · [[US-011-polacz-dwie-osoby]] (M11) — [[EPIC-003-zrozumienie]]"
journey-step: "widok 5 (M9–M11, R3)"
mockup: "2026-10-14: drzewo-039.html (ISSUE-039: ikona w pasku, okno z kaflami „Od” i „Do”, lista wyboru, ścieżka na drzewie, baner; kandydaci A1–A4, W1–W2, F1–F2, O1–O3, Y1–Y2 na 106 wymyślonych osobach; zrzuty `shots-039\\`) — katalog tymczasowy sesji `0558e715-…\\scratchpad`; 2026-10-14: drzewo-038.html (ISSUE-038: tryb prezentacji poziomo z rokiem L1–L3, sterowaniem B1–B3, tempem V1–V3, wejściem Z1–Z2 i podglądem „z kanapy” 32–65″; zrzuty `shots-038\\`) — katalog tymczasowy sesji `baf00b7b-…\\scratchpad`; 2026-10-14: drzewo-037.html (ISSUE-037: suwak czasu, kandydaci N1–N3, C1–C2, T1–T2, E1–E3, R1–R2 na wymyślonej rodzinie z datami niepewnymi; zrzuty `shots-037\\`) — katalog tymczasowy sesji `555909c3-…\\scratchpad`; 2026-10-14: drzewo-036.html (ISSUE-036: kandydaci P1–P3 wejścia w przesyłanie, zrzuty z emulatora `shots-036\\`) — katalog tymczasowy sesji `fa865b36-…\\scratchpad`; 2026-10-13: drzewo-us009.html (US-009: imiona przy oddalaniu I1–I3, karta z nazwami pokrewieństwa, tekst 200%, tryb prezentacji, stany) — katalog tymczasowy sesji `c3868f5f-…\\scratchpad`; 2026-10-13: drzewo-spike002.html (SPIKE-002, kandydaci na 106 wymyślonych osobach) — `220a9b6c-…\\scratchpad`; wcześniej 2026-10-08: grobing-prototyp.html (SPIKE-004, panel 6, runda 2)"
updated: 2026-10-17
---

# Drzewo — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.31) · referencja: [[references]] → **R3**.
>
> **Wersja 1 — discovery na prototypie, panel 6 ([[SPIKE-004-mvp-flow-prototype]] D20, D21, 2026-10-08).** Kierunek
> autora: drzewo **od osoby** (kandydat „od osoby z rozwijaniem” ze [[SPIKE-002-tree-on-a-phone]]), z poziomami
> połączeń, kolorami linii według relacji, czasem, w którym ludzie pojawiają się przy narodzinach, a pary łączą przy
> związku, z dwoma trybami związku („razem”, „małżeństwo”) i animacją ścieżki między dwiema osobami. **Czy drzewo ok.
> 100 osób jest czytelne na telefonie — to dalej pytanie SPIKE-002 (H4)**, które prototyp z ok. 30 wymyślonymi osobami
> tylko przybliża.
>
> **Wersja 1.1 — ocena rundy 2 ([[SPIKE-004-mvp-flow-prototype]] D25, D26, 2026-10-08):**
> - poziomy, linie i czas przyjęte (*„tak to jest dokładnie to”*, *„linie są super”*, *„działa dobrze i jest tak jak
>   chciałem”*); **bez legendy**; **sterowanie poziomami do przeprojektowania** — obecne „− Poziom 2 +” jest nieestetyczne
>   (*Open* 1);
> - w produkcie: **przybliżanie i oddalanie** jak na mapie oraz **pokazanie drzewa na telewizorze** (*Open* 2);
> - **„Połącz dwie osoby” dzieje się na drzewie**, nie w osobnym trybie: ikona bez podpisu → okno z dwoma kaflami →
>   wybór osób → drzewo na właściwym poziomie, linia biegnie przez ścieżkę, reszta wyszarzona, na chwilę baner z opisem
>   pokrewieństwa. Elementy 1, 7–10 i D5, D6 przepisane.
>
> **Wersja 1.2 — kandydaci [[SPIKE-002-tree-on-a-phone]] (`ui` przed planem, 2026-10-13).** Makieta na wymyślonej rodzinie o
> kształcie prawdziwej (106 osób, 6 pokoleń, trzy osoby w dwóch związkach — wdowiec, wdowa, rozwód — dwie pary „razem”, rodzina
> żony z jej kuzynami) pokazuje: **K1 całe drzewo** obok **K2 od osoby** (D1 → *Obali*), **sterowanie poziomami S1 · S2 · S3**
> (*Open* 1), **ślad dalszej rodziny** (D9), **tryb prezentacji** (*Open* 2), zadanie na czas „kim jest X dla mnie” (kryterium
> spike'a: < 30 s) i pomiar każdego poziomu (*Candidates — SPIKE-002*). Prior art: D8. Imię pod węzłem 13 sp zamiast 12 sp (D10).
> Wybór — na stopie #1.
>
> **Wersja 1.3 — decyzje autora na stopie #1 SPIKE-002 (2026-10-13, *„Tak”*):** **K2 bez K1** w MVP (D1) · **S2** — oddalanie
> odsłania dalszą rodzinę, przyciski + / − w rogu jako dostęp jednym dotknięciem (SC 2.5.1), **4 progi** zamiast zakresu 1–5, bo poziomy
> rosną 6 → 20 → 66 → 99 → 106, a od 4 to prawie wszyscy (element 3) · **ślad dalszej rodziny — tak** (D9, element 4) · **telewizor
> (a) + (b)** — „Przesyłaj ekran” Androida i tryb prezentacji na poziomie 2; buduje pozycja drzewa, nie spike; bez Google Cast (D11).
>
> **Wersja 1.4 — wynik [[SPIKE-002-tree-on-a-phone]] (2026-10-13, przy zamknięciu):** *Open* 3 rozstrzygnięte (czytelnie od osoby, z
> przesuwaniem; własny układ zamiast `graphview`) z wejściami do pozycji drzewa; nowe *Open* 5 (imiona przy oddalaniu); *Style B rules
> applied* bez nieaktualnej legendy.
>
> **Wersja 1.5 — `ui` przed planem [[US-009-drzewo-od-osoby]] (2026-10-13).** Każdy element ma numer US, która go buduje: US-009 — 1 (bez
> „Połącz dwie osoby”), 3–5, 11; US-010 — 6; US-011 — 7–10. Doszły: wartości S2 z prototypu (element 3, D18), „ja” w drzewie (D14), tekst
> 200% i cel dotyku przy oddaleniu (element 4, D17, D20), karta ze słownikiem pokrewieństwa (element 5, D12, D13), „Pokaż w drzewie” (D15),
> tryb prezentacji (element 11, D16) oraz stany bez „ja” i pustej bazy (D19). **Na stop #1:** *Open* 5 (imiona przy oddalaniu — I1, I2, I3;
> rekomendacja I2) i *Open* 6 (kto mówi w karcie — rekomendacja „Twoja”). Makieta: `drzewo-us009.html`.
>
> **Wersja 1.6 — decyzje autora na stopie #1 [[ISSUE-033-tree-from-a-person]] (2026-10-13, *„Tak”*):** *Open* 5 → **I2** (imiona zostają
> czytelne, nakładające się chowają), *Open* 6 → **G1** („Twoja babcia”, „Siostra cioteczna babci Twojej żony”); D12–D20 przyjęte.
>
> **Wersja 1.7 — przegląd `ui` zbudowanego ekranu [[ISSUE-033-tree-from-a-person]] (2026-10-13), przyjęte odstępstwa `dev`** (*Dev report* →
> *Deviations*): imię na tabliczce w kolorze tła zamiast obwódki liter (1 → D23, [[style-b]] v1.26) · drzewo nie ucieka z kadru (2, 3 → D21) ·
> zmarły = zapisany zgon albo pochówek (4 → D22) · imię ucięte w miejscu osoby także przy 100% (5 → D24) · „Pokaż w drzewie” z widoku otwartego z
> drzewa zaczyna drzewo od nowa (6 → D15) · źródło form dopełniacza (7 → D12). Odstępstwo 8 (ustawienie emulatora) nie dotyczy ekranu.
>
> **Wersja 1.8 — przegląd `ui` zbudowanego trybu prezentacji [[ISSUE-034-tree-presentation-mode]] (2026-10-14), przyjęte odstępstwa `dev`**
> (*Dev report* → *Deviations*): dotknięcie osoby w środku dopasowuje poziom od nowa (1 → D25) · pasy przy krawędziach bez dotyku (2 → D25) ·
> „Zakończ prezentację” chowa podpowiedź (3 → D25) · podpowiedź na 4 s nad górnym rzędem (4 → D26) · tekst 200% w trybie zostaje do pozycji I1 (5
> → element 11, *Open* 5) · **podpowiedź bez nazwy kafelka** — na Pixelu po polsku kafelek to „Przesyłanie”, u Samsunga „Smart View”, więc tekst
> mówi o funkcji, a nie o nazwie (6 → element 11, D26). **Zmiana decyzji autora** na stopie #1 ISSUE-034 (2026-10-14): *Open* 5 → **I1**, *Open* 6
> → **G2** — buduje to osobna pozycja „drzewo: I1 i „Moja””; do tego czasu w kodzie są I2 i G1 (elementy 4, 5).
>
> **Wersja 1.9 — [[ISSUE-035-tree-names-shrink-my-voice]] (2026-10-14): G2 w elementach 4, 5; imiona zostają przy I2.** Na kartę, do czytnika i na
> baner 9 trafiają nazwy pokrewieństwa Twoim głosem: „Moja babcia”, „to ja”, „nie wiadomo jeszcze, kim jest dla mnie”. Zdania, w których mówi
> aplikacja, zostają w drugiej osobie, np. „Wybierz, która osoba to Ty” (D28; [[style-b]] reguła 7, v1.28). **Imiona przy oddalaniu:** `ui` rozpisał
> I1, ale na stopie #1 ISSUE-035 autor odpowiedział na sekcje makiety `drzewo-us009.html`: *„1 I2, 2 „moja babcia”, 3 100%, 4 ok, 5 ok, 6 ok”*. Zostaje
> więc I2, które już jest w kodzie (D27). Zapis I1 cofnięty przed budową.
>
> **Wersja 1.10 — `ui` przed planem [[ISSUE-036-cast-from-the-app]] (2026-10-14): wejście w przesyłanie z aplikacji.** Prior art i pomiar (D29): aplikacja
> bez Google Cast może tylko **otworzyć systemowy ekran przesyłania** — pełny ekran ustawień („Google Cast”, zrzut `01` w makiecie), a nie okienko z listą
> nad drzewem jak w Zdjęciach. Samo przesyłanie włącza system. Kandydaci wejścia P1–P3 (*Candidates — ISSUE-036*), **rekomendacja P2**: jedna ikona
> „Przesyłaj na telewizor” zamiast ikony telewizora, czyli ekran systemu, a po powrocie tryb prezentacji (elementy 1 i 11 zapisane według P2, *Open* 7 — na stop #1).
> Makieta: `drzewo-036.html`. **Decyzja autora na stopie #1 (2026-10-14, *„tak”*): P2** (D30).
>
> **Wersja 1.11 — przegląd `ui` zbudowanego wejścia [[ISSUE-036-cast-from-the-app]] (2026-10-14), przyjęte odstępstwa `dev`** (*Dev report* →
> *Deviations*): powrót z ekranu systemu rozpoznany po tym, że aplikacja znów ma fokus, a nie po tym, że była schowana — szybki wstecz jej nie chowa,
> a ekran przesyłania w oknie nad aplikacją też by jej nie schował (1 → *Navigation*, D30 a) · drugie dotknięcie ikony w trakcie otwierania nic nie
> robi, a ikona się nie zmienia — wyszarzenie mignęłoby tylko na ułamek sekundy (2 → element 1, D30 b).
>
> **Wersja 1.12 — `ui` przed planem [[ISSUE-037-time-on-the-tree]] ([[US-010-czas-na-drzewie]], 2026-10-14): czas na drzewie.** Element 6 rozpisany do końca:
> suwak w karcie, ▶ / ❚❚, rok, tekst 200%, czytnik. Prior art (D31): TimeNets szacuje brakujące daty z rodziny i pokazuje niepewność na rysunku, a liczby
> okna są z Gramps. **Kandydaci na stop #1** (*Candidates — ISSUE-037*, makieta `drzewo-037.html`): daty niepewne i brak daty **N1–N3** (rekomendacja **N3** —
> przerywany obrys, D32), osoba w środku przed narodzinami **C1–C2** (**C1** — pusty pierścień, D33), początek suwaka **T1–T2** (**T2**, D34), koniec związku
> **E1–E3** (**E3** — „//” na linii, D35, zmienia też drzewo na „dziś”), ograniczenie animacji **R1–R2** (**R2**, D36). Rok a nawigacja — D37. Elementy 4 i 6,
> *States*, *Sketch* i *AC → element* są zapisane według rekomendacji. Przy innym wyborze `ui` zmienia je przed planem (*Open* 8). **Decyzja autora na stopie #1
> (2026-10-14, *„tak”*): N3, C1, T2, E3, R2** — zapis bez zmian; [[style-b]] v1.29.
>
> **Wersja 1.13 — przegląd `ui` zbudowanego czasu [[ISSUE-037-time-on-the-tree]] (2026-10-14), przyjęte odstępstwa `dev`** (*Dev report* → *Deviations*): tempo ▶
> zmierzone ok. 19,7 lat/s (1 → *AC → element*, US-010 AC-3) · napis roku w stałym miejscu (2 → element 6) · przenikanie przerywane w trakcie ▶ (4 → element 6).
> Odstępstwo 3 (karta w osobnej warstwie) — techniczne, bez zapisu. Dwie usterki z przeglądu poprawione przed stopem #2 → D37: ślad w bok dopiero od początku związku,
> widok osoby zatrzymuje ▶.
>
> **Wersja 1.14 — `ui` przed planem [[ISSUE-038-history-on-tv-and-tempo]] (2026-10-14): historia na telewizorze i tempo lat.** Prośba autora ze stopu #2 ISSUE-037: *„a) Można
> było tą historie odtwarzać na telewizorze, b) dostosowanie prędkości tych lat”*, *„dla mnie za szybko”*. Prior art i pomiar (D38): telefon poziomo wypełnia szerokość
> telewizora 16:9, więc tekst z telefonu liczy się w kącie widzenia z kanapy. Rok w 36 sp ma z 3 m od 23′ (32″) do 46′ (65″), czyli powyżej minimum 16′ z ISO 9241. Imię w 13 sp
> ma 8–17′, więc od 55″ w dół jest poniżej minimum. **Kandydaci na stop #1** (*Candidates — ISSUE-038*, makieta `drzewo-038.html`):
> - rok na telewizorze **L1–L3** — rekomendacja **L1**, rok w rogu (D39);
> - sterowanie w prezentacji **B1–B3** — rekomendacja **B2**, listwa jak w odtwarzaczu (D40);
> - tempo **V1–V3** — rekomendacja **V2**: „Wolno” · „Średnio” · „Szybko”, 5 · 10 · 20 lat/s, domyślnie „Średnio” (D41);
> - wejście z roku Y **Z1–Z2** — rekomendacja **Z2**, rok przechodzi do trybu; to zmiana D37 (D42).
>
> Elementy 6 i 11, *Navigation*, *States*, *Sketch* i *AC → element* są zapisane według rekomendacji. Przy innym wyborze `ui` zmienia je przed planem (*Open* 9). **Decyzja
> autora na stopie #1 (2026-10-14, *„Ok”*): L1, B2, V2, Z2** — zapis bez zmian; tempo domyślne „Średnio” bez uwag.
>
> **Wersja 1.15 — przegląd `ui` zbudowanej historii na telewizorze [[ISSUE-038-history-on-tv-and-tempo]] (2026-10-14), przyjęte odstępstwa `dev`** (*Dev report* →
> *Deviations*): z czytnikiem ekranu sterowanie jest od wejścia w tryb i nie chowa się wcale, bo pustego miejsca czytnik nie dotknie (1 → element 11, *States*, D40) · górny
> rząd karty przy tekście ≥ 150% przenosi rok do następnej linii, zamiast go uciąć, gdy trzy elementy się nie mieszczą (2 → element 6) · przycisk tempa ma szerokość
> najszerszego słowa (3 → element 6; druga instancja po roku z v1.13, więc reguła — [[style-b]] reguła 5, v1.31).
>
> **Wersja 1.16 — `ui` przed planem [[ISSUE-039-connect-two-people]] ([[US-011-polacz-dwie-osoby]], 2026-10-14): „Połącz dwie osoby” na dzisiejszym drzewie.** Elementy 7–10
> były z v1.1 (prototyp z ok. 30 osobami), czyli sprzed poziomów S2, G2, czasu i trybu prezentacji. Prior art i pomiar (D43): FamilySearch pokazuje ścieżkę tylko od „mnie”;
> Snackbar Androida bierze czas z ustawienia „Czas na działanie”. Na makiecie ze 106 osobami ścieżka od „Ja” ma 1–5 kroków, a 10 ze 105 ścieżek nie mieści się na 360 dp nawet
> przy skali 0,4. **Kandydaci na stop #1** (*Candidates — ISSUE-039*, makieta `drzewo-039.html`):
> - ikona **A1–A4** — rekomendacja **A1**, `link_outlined` (D44; zamyka *Open* 1a);
> - kto staje w środku **W1–W2** — rekomendacja **W2**, „Do” (D45);
> - długa ścieżka **F1–F2** — rekomendacja **F2**, drzewo maleje, aż cała ścieżka się zmieści (D46);
> - baner, gdy „Od” to nie Ty, **O1–O3** — rekomendacja **O2**, dwie linie bez odmiany imion (D47);
> - rok inny niż „dziś” **Y1–Y2** — rekomendacja **Y1**, ścieżka przestawia na „dziś” (D48).
>
> Decyzje projektowe bez pytania — D49 (poziom, linia, baner, koniec podświetlenia, okno, tryb prezentacji). Elementy 1, 7–10, *Navigation*, *States*, *Sketch* i *AC → element*
> są zapisane według rekomendacji. Przy innym wyborze `ui` zmienia je przed planem (*Open* 10). **Decyzja autora na stopie #1 (2026-10-14, *„Tak”*): A1, W2, F2, O2, Y1** — zapis bez
> zmian; do tego z planu: bez „ja” ikony „Połącz dwie osoby” nie ma (element 1).
>
> **Wersja 1.17 — przegląd `ui` zbudowanego „Połącz dwie osoby” [[ISSUE-039-connect-two-people]] (2026-10-14), przyjęte odstępstwa `dev`** (*Dev report* → *Deviations*):
> baner dochodzi do czytnika jako region na żywo, jak pigułka poziomu, a nie osobnym ogłoszeniem — jego tekst jest na ekranie (1 → element 9, D43) · kadr krótkiej ścieżki na
> poziomie 1 w skali 1,3, bez przybliżania ponad próg poziomu (2 → element 8, D46) · zmiana danych drzewa w trakcie podświetlenia je kończy (3 → element 8, *Navigation*, D49) ·
> baner z jawną wysokością wiersza 1,3, żeby kadr liczył go tak, jak się rysuje (4 → element 9). Do tego dwa odstępstwa, których *Dev report* nie wymienia, a przegląd przyjmuje:
> w podświetleniu **wszystkie** linie rodziny i ślady są przy 30%, także osób ze ścieżki — jedna warstwa linii (plan D7), a drogę niesie linia w akcencie (5 → element 8, D49,
> *Style B rules applied*) · znak „Ja” w kaflu „Od” ma obrys w akcencie jak na liście [[osoby]], bo w oknie nie ma osoby w środku (6 → element 7). [[style-b]] bez zmian: żadne z
> sześciu nie zmienia reguły stylu.
>
> **Wersja 1.18 (2026-10-17, `ui` przed planem [[ISSUE-044-family-wreaths]], decyzja autora na prototypie — G2):** **wieniec rodu na węźle** (element 4; także w trybie
> prezentacji, 11) i **96 dp na osobę**, gdy ktoś w drzewie ma wieniec ([[wieniec]] D17; przy 80 dp wieńce par wchodziły na siebie). Ślad w bok zaczyna się za wieńcem.
> Karta (5) i kafle okna (7) bez wieńca. Szczegóły: [[wieniec]] D.
>
> **Wersja 1.19 (2026-10-17, przegląd `ui` zbudowanej [[ISSUE-044-family-wreaths]] — odstępstwa 1 i 5 `dev` przyjęte; [[wieniec]] v1.1):** 96 dp na osobę, gdy
> wieniec ma ktokolwiek **w rodzinie**, a nie tylko w pokazanym drzewie — miejsce nie zmienia się przy przestawieniu środka (1 → element 4, [[wieniec]] D17) ·
> **wieniec w węźle**, pod jego tabliczką i okręgiem, a nie na osobnej warstwie pod wszystkimi węzłami — gaśnie i wyszarza się razem z osobą (5 → element 4,
> [[wieniec]] D18). Doprecyzowane: ślad w bok zaczyna się 43 dp od środka tylko u osoby z wieńcem. [[style-b]] bez zmian.

## Purpose
Zobaczyć rodzinę wokół wybranej osoby i jak się łączy (M9), jak zmieniała się w czasie (M10) i jak dowolne dwie osoby
są spokrewnione (M11). Tak samo zbudowane jest mini-drzewo w [[osoba]] (element 6).

## Navigation
- **Zakładka „Drzewo”** w dolnym pasku. **Każde wejście z paska zaczyna od „Ja”** na poziomie 2, w skali 1 (AC-1). Drzewo nie pamięta
  poprzedniego środka (v1.5, D15).
- **„Pokaż w drzewie”** w [[osoba]] (element 6) → zakładka Drzewo z tą osobą w środku, na poziomie 2. Działa jak dotknięcie „Drzewo” w pasku
  ([[style-b]] reguła 12): stos widoku osoby znika, a wstecz z drzewa wraca na mapę (v1.5, D15). Także z widoku osoby otwartego z drzewa —
  drzewo zaczyna od nowa, z tą osobą w środku (v1.7, D15).
- **Dotknięcie osoby → ona staje w środku**; dotknięcie osoby w środku albo „Pokaż” w karcie → [[osoba]] (zakładka Drzewo
  zostaje aktywna). Wstecz z widoku osoby wraca do drzewa z tym samym środkiem i skalą.
- **Ikona „Przesyłaj na telewizor”** w pasku (v1.10, D30) → **systemowy ekran przesyłania** (ustawienia telefonu, nie ekran aplikacji) → po powrocie
  (wstecz albo wybór telewizora i wstecz) **tryb prezentacji** (element 11). Telefon bez tego ekranu → od razu tryb prezentacji z podpowiedzią (D26).
  Wstecz albo „Zakończ prezentację” wraca do drzewa (US-009). Do v1.9 ikona telewizora otwierała sam tryb prezentacji. **Powrót** to chwila, gdy
  aplikacja znów ma fokus po ekranie systemu, a nie gdy była schowana (v1.11, D30 a). Home z ekranu systemu i powrót do Grobinga pokazuje znowu
  ekran systemu (to samo zadanie); tryb włącza dopiero wstecz.
- **Ikona „Połącz dwie osoby”** w pasku → okno z dwoma kaflami (7) → kafel → lista „Od kogo?” / „Do kogo?” (tryb wyboru jak „Która osoba to Ty?”, bez
  dolnego paska — [[style-b]] reguła 12) → wybór „Od” wraca do okna, a wybór „Do” zamyka okno i wraca **na drzewo**, z animacją ścieżki (v1.1, D26). „Do” staje w
  środku (W2, D45). Podświetlenie kończy dotknięcie drzewa, wstecz, przybliżanie i oddalanie, ▶, suwak i „Przesyłaj na telewizor”; przeciąganie przesuwa i nie kończy
  (v1.16, D49). Kończy je też zmiana danych drzewa (v1.17, odstępstwo 3 ISSUE-039). Wstecz w oknie, „Anuluj” albo dotknięcie poza oknem zamyka okno bez zmian.
- **Rok na suwaku** (US-010, v1.12, D37): zostaje przy przestawieniu środka, zmianie poziomu i powrocie wstecz z widoku osoby; wejście z paska i „Pokaż w drzewie”
  pokazują „dziś”, a ścieżka „Połącz dwie osoby” przestawia na „dziś” i zatrzymuje ▶ (v1.16, Y1 — D48). **Tryb prezentacji** (v1.14, Z2 — D42): rok przechodzi do trybu i wraca z niego, tak jak osoba w środku; ▶ stoi, bo po drodze był ekran systemu. Do v1.13
  tryb zawsze pokazywał „dziś”.
- **Tempo** (v1.14, D41): wybrane tempo zostaje, dopóki aplikacja działa — w karcie i w trybie prezentacji to samo; po zamknięciu aplikacji wraca „Średnio”.
- **Bez „ja”:** „Wybierz, która osoba to Ty” → wybór „ja” ([[osoby]] 6–7) → po wyborze z powrotem na drzewie, z tą osobą w środku (D19).

## Elements in order
**Tryb „Drzewo”** — US-009, poza elementem 6 (US-010)

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek „Drzewo” (20 sp, półgruby), po prawej ikony **bez podpisu** (v1.1): **„Przesyłaj na telewizor”** (`cast_outlined`, akcent, cel 48 dp, `tooltip` „Przesyłaj na telewizor”, czytnik: „Przesyłaj na telewizor — w ustawieniach telefonu” — **US-009**, v1.10, [[ISSUE-036-cast-from-the-app]]; **zastępuje** `tv_outlined` „Tryb prezentacji” z v1.5 — D30; drugie dotknięcie, zanim otworzy się ekran systemu, nic nie robi, a ikona się nie zmienia — v1.11, D30 b) i na lewo od niej **„Połącz dwie osoby”** (`link_outlined` — A1, v1.16, D44; akcent, cel 48 dp, `tooltip` i czytnik „Połącz dwie osoby” — **US-011**). W stanach bez drzewa (bez „ja”, pusta baza) ikon nie ma; „Połącz dwie osoby” nie ma też na drzewie z „Pokaż w drzewie”, gdy „ja” nie jest wybrane — okno zaczyna od „Ja”, a baner mówi od „ja” (v1.16, D3 planu [[ISSUE-039-connect-two-people]], stop #1) | pasek + przyciski-ikony | → systemowy ekran przesyłania → po powrocie tryb prezentacji (11) · → okno wyboru (7) | — | — | R3 · **decyzja autora** (D26, D11; stop #2 ISSUE-034 — „jak w YouTube”) · AC-8 · D29 |
| 2 | ~~Legenda linii~~ — **bez legendy** (v1.1, D25). Rodzaj linii niesie kształt i styl (łamana z góry — rodzic–dziecko; pozioma ciągła — małżeństwo; przerywana — razem), więc kolor nie jest jedynym nośnikiem (SC 1.4.1) | — | — | — | — | **decyzja autora** (D25) |
| 3 | **Poziom połączeń — oddalanie odsłania dalszą rodzinę** (v1.3, S2): bez przycisków „−/Poziom 2/+” w pasku. Poziom zmienia oddalanie i przybliżanie, **próg za progiem**: oddalasz — dokłada się poziom, przybliżasz — dalsza rodzina znika. **4 progi** (poziomy 1–4; od 4 to prawie wszyscy). Przy zmianie na chwilę pigułka „Poziom 3 · 66 osób” (13 sp, powierzchnia). **Przyciski + / −** (cel 48 dp, powierzchnia z obrysem) w prawym dolnym rogu drzewa — alternatywa jednym dotknięciem (SC 2.5.1): + przybliża, − oddala. **Poziom 1:** rodzice, partnerzy, dzieci. **Poziom k ≥ 2:** do tego rodzice, partnerzy, dzieci i **rodzeństwo** każdej osoby z poziomu k−1 (np. rodzeństwo, rodzeństwo partnerów, dziadkowie, teściowie, wnuki). **Wartości** (v1.5, D18 — z prototypu SPIKE-002, do potwierdzenia w ręce): skala 0,4–2,0, start 1,0; **poziom 1** przy skali ≥ 1,3 · **2** — 0,85–1,3 · **3** — 0,55–0,85 · **4** — poniżej 0,55. + / − mnożą skalę przez 1,45 (mniej więcej poziom na dotknięcie); **podwójne dotknięcie pustego miejsca** przybliża tak samo (AC-3). Pigułka ok. 1,5 s; ten sam tekst ogłasza czytnik. Zmiana poziomu zostawia osobę w środku w tym samym miejscu ekranu | gest + przycisk-ikona ×2 + pigułka | dwa palce (oddal / przybliż) · + / − · podwójne dotknięcie | 2 | — | **decyzja autora** (stop #1 SPIKE-002) · D2 · D8 · AC-3 · D18 |
| 4 | **Drzewo**: rzędy według pokolenia (wyżej starsze), osoba w środku z pierścieniem w akcencie; rodzeństwo z boku osoby, po stronie dalszej od partnera; **rodzina partnera po prawej**, bez przeplatania z krewnymi. Węzeł 44 dp (profilowe albo inicjały), imię 13 sp półgrube (v1.2, D10); **zmarły ma znicz** w rogu węzła ([[style-b]] reguła 8, R3); zmarły = zapisany zgon albo pochówek, z datą albo bez (v1.7, D22). Linie: **rodzic–dziecko** — kolor relacji rodzic–dziecko, łamana z góry w dół; **małżeństwo** — kolor partnerów, ciągła, pozioma; **razem (bez ślubu)** — kolor partnerów, przerywana 5/4. **Koniec związku** (v1.12, E3 — D35): od roku końca dwie ukośne kreski „//” przez środek linii pary (kolor partnerów, 2 dp, ok. 12 × 12 dp), także na „dziś”; koniec bez daty — tylko na „dziś”; linia do dzieci zostaje. **Ślad dalszej rodziny** (v1.3, D9): osoba z rodziną poza widokiem dostaje krótką przerywaną kreskę 3/3, 14 dp, w kolorze relacji o kryciu 60% — w górę rodzice, w dół dzieci, w bok partner, **na zewnątrz od środka** (na lewo od osoby w środku — w lewo, na prawo i u niej samej — w prawo; v1.7, przegląd `ui` ISSUE-033: zawsze w prawo celował u osób po lewej w środek i mylił się z linią „razem”). Przewijanie w obu osiach, środek ustawia się na osobie. **Drzewo nie ucieka z kadru** (v1.7, D21): gdy w kadrze nie ma nikogo, widok wraca płynnie (ok. 0,35 s) do osoby w środku, a palec na ekranie przerywa powrót; nowy rozmiar obszaru drzewa przed pierwszym dotknięciem ustawia środek od nowa. **„Ja”** (v1.5, D14): okrąg ze znakiem „Ja” (inicjały „Ja” w akcencie, obrys w kolorze obrysu, także przy profilowym — jak [[osoby]] D4), podpis „Ja”; pierścień i poświatę w akcencie ma tylko osoba w środku. **Przestawienie środka** (AC-2, v1.5): węzły przesuwają się na nowe miejsca w ok. 0,45 s, nowe osoby się pojawiają, odchodzące gasną, a widok jedzie tak, że nowa osoba staje w środku (ok. 42% wysokości obszaru drzewa). Przy systemowym ograniczeniu animacji — od razu (SC 2.3.3, jak D5). **Imiona przy oddalaniu** (v1.6, I2 — decyzja autora; potwierdzona w v1.9, D27): przy skali < 1 imię nie maleje — na ekranie ma 13 sp × skala tekstu, na tabliczce w kolorze tła (zaokrąglona 4 dp, 3 dp z boków; v1.7, D23); gdy dwa imiona by się nałożyły, zostaje to bliżej osoby w środku (najpierw poziom z D2, potem odległość w poziomie), a reszta chowa się do przybliżenia. **Wieniec rodu** (v1.18, [[wieniec]] D): pod węzłem osoby z rodem — płótno 88 dp, węzeł w jego (0,50; 0,434), skaluje się z drzewem; rysowanie: linie → wieńce → węzły → znicz, a **wieniec należy do węzła** (v1.19): w węźle wieniec → tabliczka imienia → okrąg z pierścieniem, poświatą i zniczem, więc gaśnie i wyszarza się razem z osobą (element 8) bez osobnego krycia; poza czytnikiem. **Gdy ktoś w rodzinie ma wieniec** (całe drzewo w bazie, nie tylko pokazane — v1.19), **miejsce osoby ma 96 dp** zamiast 80 (`max(96, 80 × skala tekstu)`, najwyżej 160 dp), a **ślad w bok osoby z wieńcem zaczyna się za wieńcem**, 43 dp od środka węzła (osoby bez wieńca — przy okręgu). **Tekst systemu** (AC-7, v1.5): miejsce osoby 80 dp × skala tekstu, najwyżej 160 dp (jak mini-drzewo, [[osoba]] v2.2); rząd rośnie z podpisem (104 dp → 124 dp przy 200%); inicjały najwyżej 1,3×; imię w jednej linii, „…” dopiero poza miejscem osoby (przy 100% to ok. 10 liter, także przy oddaleniu — v1.7, D24). **Cel dotyku** = miejsce osoby × skala drzewa (D17). **Czytnik:** „Zofia Wymyślona, 1928–2010, Moja babcia — w środek” (v1.9, G2 — ten sam tekst co karta, D28), osoba w środku „… — otwórz”; kolejność rzędami, z góry i od lewej; linie i ślad poza czytnikiem | drzewo | dotknięcie → osoba w środek; drugie → [[osoba]] | „Ja” | — | R3 · D1, D3, D4, D9 · AC-1, AC-2, AC-4, AC-7 · D14, D17 |
| 5 | **Karta osoby w środku** (dolny arkusz, powierzchnia; v1.5): okrąg 40 dp z pierścieniem w akcencie (profilowe w kadrze albo inicjały; „ja” — znak „Ja”) · **imię i nazwisko** z „z d.” (16 sp, półgruby, tekst, do dwóch linii) · pod spodem **lata · kim jest dla mnie** (14 sp, tekst pomocniczy, **zawija się, bez ucinania**): nazwa ze słownika, z nawiasem tam, gdzie słownik go ma („1928–2010 · Moja babcia”, „ur. 1951 · Mój stryj (brat taty)”, „Moje rodzeństwo” przy osobie bez płci), a dalej opis z odcinków („1925–2010 · Siostra cioteczna mojego dziadka”, „Siostra cioteczna babci mojej żony”; D12, D13; **mówisz Ty — G2, v1.9, D28**). „Ja”: „ur. 1983 · to ja”. Bez ścieżki do „ja”: „… · nie wiadomo jeszcze, kim jest dla mnie”. Zaimek zawsze z małej litery w środku opisu („…babci mojej żony”), z wielkiej tylko na początku nazwy („Moja babcia”). Bez „ja” (wejście z „Pokaż w drzewie”): same lata. Po prawej przycisk tekstowy „Pokaż ›” (akcent, cel 48 dp); **przy tekście systemu ≥ 150% „Pokaż ›” przechodzi pod tekst, do prawej** (D20) | karta | „Pokaż” → [[osoba]] | — | — | D1 · AC-2, AC-5 · D12, D13, D20 |
| 6 | **US-010. Czas (M10; v1.12 — [[ISSUE-037-time-on-the-tree]]):** w karcie (5), pod imieniem i opisem, jeden rząd: **▶ / ❚❚** (okrąg 36 dp w akcencie, ikona `play_arrow` / `pause` w kolorze tła, cel 48 dp, `tooltip` „Odtwórz historię” / „Zatrzymaj”) · **rok początku** (13 sp, tekst pomocniczy) · **suwak** (`Slider`: aktywny tor i uchwyt w akcencie, tor nieaktywny w kolorze obrysu, wysokość 48 dp, krok 1 rok) · **rok** (16 sp, półgruby, akcent, cyfry o stałej szerokości; na końcu suwaka „dziś”) — w stałym miejscu na szerokość najszerszego z „dziś” i „8888”, żeby tor suwaka nie zmieniał długości pod palcem (v1.13, odstępstwo 2 ISSUE-037) · **tempo** (v1.14, V2 — D41): przycisk tekstowy z nazwą tempa, „Średnio” (14 sp, waga 500, kolor tekstu — stoi obok wypełnionego ▶, [[style-b]] reguła 1; cel 48 dp, `tooltip` i czytnik „Tempo historii: średnio — zmień”) — na szerokość najszerszego słowa („Średnio”), słowo na środku, żeby tor suwaka nie zmieniał długości przy przełączaniu (v1.15, odstępstwo 3 ISSUE-038; [[style-b]] reguła 5). Dotknięcie przełącza „Wolno” → „Średnio” → „Szybko” → „Wolno”; w trakcie ▶ odtwarzanie biegnie dalej od bieżącego roku w nowym tempie. Przy tekście 100% suwak jest przez to krótszy: 129–137 dp zamiast 193 dp (makieta, ekran 360 dp). **Domyślnie „dziś”** — drzewo jak w US-009: nic nie znika i nic nie jest przerywane. **Początek suwaka** (T2, D34): pełna dekada przed najwcześniejszą datą urodzenia w bazie, najpóźniej 1880. **Rok Y** (AC-1, AC-2): osoba, która w roku Y jeszcze się nie urodziła, znika razem ze swoimi liniami i imieniem, a jej miejsce zostaje (układ liczony jak na „dziś”, rok go nie zmienia); nie jest celem dotyku i nie ma jej w czytniku. Zmarły do Y ma znicz. Para: do początku związku bez linii, od początku przerywana „razem”, od ślubu ciągła; **związek bez daty** — od urodzenia najstarszego wspólnego dziecka, a bez dzieci — od 20. roku życia młodszego z pary (D31); koniec związku — „//” (element 4, E3). **Data niepewna i brak daty** (N3, D32): każda data ma okno [najwcześniej, na pewno]. Osoba pojawia się na początku okna urodzenia i do jego końca ma **przerywany obrys okręgu** (2 dp, kreska 4/3, kolor obrysu; u osoby w środku pierścień w akcencie przerywany). W oknie śmierci — ten sam obrys, a znicz dopiero na końcu okna. Okno: dokładnie Y — Y; „ok. Y” — Y−5 … Y+5; „między A a B” — A … B; „przed Y” — najwcześniej z rodziny … Y; „po Y” — Y … na pewno z rodziny; brak daty — oba końce z rodziny (D32). **Osoba w środku przed narodzinami** (C1, D33): pusty pierścień w akcencie w jej miejscu, bez okręgu, imienia i znicza; karta bez zmian. **▶** (AC-3): od początku suwaka (albo od bieżącego roku, gdy to nie „dziś”) do „dziś”, **w wybranym tempie** (v1.14, D41): „Wolno” 5, „Średnio” 10, „Szybko” 20 lat na sekundę, czyli od 1880 do dziś ok. 29 · 15 · 7 s (do v1.13 stale ok. 21 lat/s); osoby pojawiają się i gasną przenikaniem 150 ms — w trakcie ▶ najwyżej do następnego roku (przy „Wolno” pełne 150 ms, przy „Średnio” ok. 100 ms, przy „Szybko” ok. 50 ms), pełne 150 ms przy przesuwaniu suwaka palcem (v1.13, odstępstwo 4 ISSUE-037; *Obali:* autor widzi miganie osób przy ▶ — wtedy przenikanie od roku narodzin, bez przerywania); na „dziś” ▶ się zatrzymuje, a czytnik raz ogłasza rok („Rok 1923”, „dziś”) — także po ❚❚. ❚❚ zatrzymuje na bieżącym roku; przeciągnięcie suwaka też zatrzymuje. **Ograniczenie animacji** (R2, D36): ▶ przeskakuje o pełną dekadę, osoby pojawiają się od razu, bez przenikania; odstęp skoków daje tempo — co ok. 2 · 1 · 0,5 s (v1.14, D41). **Tekst ≥ 150%** (D20): rok początku i rok w rzędzie nad suwakiem (po lewej i po prawej), **tempo między nimi** (v1.14 — suwak bez zmian, 278 dp przy 200%), ▶ i suwak w rzędzie pod nimi. Gdy trzy się nie mieszczą (telefon węższy niż 360 dp albo szerszy krój), rok przechodzi do następnej linii, na lewo, zamiast się uciąć; na 360 dp przy 200% w Roboto stoją w jednej linii (v1.15, odstępstwo 2 ISSUE-038). **Czytnik:** ▶ „Odtwórz historię” / „Zatrzymaj”; suwak „Rok” z wartością „1923” albo „dziś”, zwiększanie i zmniejszanie o 10 lat (krok co rok to do 166 gestów); w trakcie ▶ rok nie jest ogłaszany co zmianę, po zatrzymaniu — tak. Osoba z przerywanym obrysem: do opisu z elementu 4 dochodzi „nie wiadomo, czy już żyje” (okno urodzenia) albo „nie wiadomo, czy jeszcze żyje” (okno śmierci); pusty pierścień: „… — przed narodzinami” | suwak + przycisk ×2 | przeciągnięcie · ▶ / ❚❚ · tempo | dziś · „Średnio” | — | R3 (suwak) · **decyzja autora** (D20) · D4 · AC-1–AC-3 · D31–D37 · D41 (ISSUE-038) |
| 11 | **Tryb prezentacji** (AC-8, D11; v1.5, D16): ekran poziomo, na pełnym ekranie (bez pasków systemu i aplikacji, bez karty i + / −), **poziom 2 dopasowany do ekranu** (w obszarze bezpiecznym, margines 24 dp) i wyśrodkowany. **Wejście (v1.10, P2):** po powrocie z systemowego ekranu przesyłania — **bez podpowiedzi** (przesyłanie właśnie wybrane, a podpowiedź trafiłaby na telewizor). **Tylko gdy telefon nie ma tego ekranu** (ISSUE-036 AC-2) tryb włącza się od razu i na ok. 4 s pokazuje pigułkę u góry, w miejscu pigułki poziomu: „Obraz na telewizor: przesyłanie ekranu w szybkich ustawieniach telefonu” (v1.8, D26 — funkcja, nie nazwa kafelka; twarda spacja po „w”, [[style-b]] reguła 6). Przez te 4 s może przykryć górny rząd, a dotyk przechodzi do osób pod nią (D26). **Dotknięcie osoby** → ona w środku, poziom 2 dopasowany na nowo — **także osoby, która już jest w środku**: po przeciągnięciu to droga z powrotem; jej widok się nie otwiera, a czytnik nie mówi „otwórz” (v1.8, D25). Przeciąganie przesuwa; **bez szczypania** — poziom stały. **Pasy 24 dp przy krawędziach, od których system wysuwa paski, nie przyjmują dotyku** (v1.8, D25). **Dotknięcie pustego miejsca** → **sterowanie** (v1.14, B2 — D40; do v1.13 sam przycisk na 3 s): w prawym górnym rogu przycisk „Zakończ prezentację” (`close` w akcencie + napis w kolorze tekstu, powierzchnia z obrysem, cel 48 dp), a na dole **listwa** na powierzchni (zaokrąglona 16 dp, 24 dp od krawędzi — nad pasami bez dotyku z D25): ▶ / ❚❚, rok początku, suwak i tempo, te same co w elemencie 6, ale bez roku na końcu, bo rok stoi w rogu. Sterowanie chowa się po 5 s od ostatniego dotyku albo po czasie z ustawienia systemu „Czas na działanie”, gdy jest dłuższy. Drugi pusty dotyk chowa je od razu. **Z czytnikiem ekranu** (TalkBack, a także Switch Access i Voice Access — wszystko, co ustawia `accessibleNavigation`) sterowanie jest **od wejścia w tryb i nie chowa się wcale**: pusty obszar nie ma węzła semantyki, więc czytnik nie umie go dotknąć, a schowane sterowanie byłoby nie do odzyskania; wyjście — „Zakończ prezentację” albo wstecz (v1.15, odstępstwo 1 ISSUE-038; D40). Podpowiedź, jeśli jeszcze jest, znika (v1.8, D25). Przeciągnięcie suwaka zatrzymuje ▶ (D37), a dotknięcie osoby nie zatrzymuje, tylko stawia ją w środku. Przez te 5 s listwa przykrywa dolny rząd drzewa — także na telewizorze. **Wstecz** też kończy. Po wyjściu — drzewo pionowo, ta sama osoba w środku, poziom 2, skala 1, **ten sam rok** (Z2 — D42). **Rok na telewizorze** (v1.14, L1 — D39): w lewym górnym rogu, 36 sp, półgruby, akcent, cyfry o stałej szerokości, na tabliczce w kolorze tła (zaokrąglona 8 dp, 6 dp z boków). Stoi **48 dp od lewej krawędzi** (5% szerokości — telewizor może przyciąć brzeg obrazu, D38) i 24 dp od góry. Widać go, gdy rok nie jest „dziś”, i zawsze, gdy widać sterowanie; gdy ▶ dojdzie do „dziś”, napis „dziś” zostaje jeszcze 3 s. Drzewo dopasowuje się tak samo jak bez roku — w makiecie rok nie przykrywa nikogo przy żadnym ze 106 środków na ekranie 914 dp, a na 360 dp przy jednym (*Candidates — ISSUE-038* → *Pomiar*). Rośnie z tekstem systemu najwyżej do 1,3× (47 sp; [[style-b]] *Thresholds*). Czytnik: „Rok 1950” albo „dziś”, w trakcie ▶ bez ogłaszania (jak element 6). **Wejście z roku Y** (Z2 — D42): tryb pokazuje rok z karty, ▶ stoi. **Tekst 200%** (v1.8, odstępstwo 5 ISSUE-034; v1.9 — I2 zostaje, D27): imiona jak w elemencie 4, więc na ekranie 360 dp imię ma 26 sp przy okręgu ok. 20 dp (skala ok. 0,45), widać 13 z 20 imion, a tabliczki zasłaniają linie między rzędami (zrzut `18b`). Przy I1 byłoby 20 z 20 imion, ok. 11,7 sp (przeliczenie `ui`, v1.9). Na ekranie 914 dp przy 200% widać 17 z 20 imion (makieta ISSUE-038), a przy 100% — 20 z 20 | tryb | dotknięcie osoby · pustego miejsca (sterowanie) · ▶ / ❚❚ · suwak · tempo · wstecz | poziom 2 · rok z karty | — | **decyzja autora** (D11) · AC-8 · D16 · D25, D26 · D38–D42 (ISSUE-038) |

**„Połącz dwie osoby” na drzewie (M11, v1.1)** — US-011

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 7 | **Okno „Połącz dwie osoby”** (v1.1; v1.16 — D49): okno na środku ekranu, na powierzchni, zaokrąglone 16 dp, tło pod nim przyciemnione; tytuł „Połącz dwie osoby” (18 sp, półgruby); **dwa kafle obok siebie**, między nimi strzałka `arrow_forward` (tekst pomocniczy) — „Od” i „Do”: obrys 1 dp w kolorze obrysu, zaokrąglone 12 dp, cel ≥ 48 dp. W kaflu podpis „Od” / „Do” (13 sp, tekst pomocniczy), okrąg 40 dp (profilowe w kadrze albo inicjały; „ja” — znak „Ja”, D14, z obrysem w akcencie jak na liście [[osoby]], bo w oknie nie ma osoby w środku, z którą by się pomylił — v1.17, przegląd ISSUE-039) i imię z nazwiskiem bez „z d.” (14 sp, zawija się na spacjach, nie w środku słowa). **Pusty kafel:** przerywany okrąg w akcencie z `add` i „Wybierz osobę” (akcent, waga 500 — główne działanie okna, [[style-b]] reguła 1). **Tekst ≥ 150%:** kafle jeden pod drugim, strzałka w dół; w kaflu podpis nad wierszem z okręgiem i imieniem. Na dole przycisk tekstowy „Anuluj” (kolor tekstu). **Każde otwarcie:** „Od” — „Ja”, „Do” — pusty. Kafel → **lista „Od kogo?” / „Do kogo?”** na cały ekran — ta sama lista co w [[osoby]] (wyszukiwarka „Szukaj osoby”, A–Z, karty z okręgiem, imieniem z „z d.” i latami; tryb wyboru jak „Która osoba to Ty?”, bez dolnego paska), **bez osoby z drugiego kafla**. Wybór „Od” wraca do okna; **wybór „Do” zamyka okno** i uruchamia 8 | okno z kaflami + lista wyboru | kafel → lista; wybór „Do” → 8; „Anuluj”, wstecz, dotknięcie poza oknem → zamknij bez zmian | Od: „Ja” | — | **decyzja autora** (D26) · R3 · [[osoby]] (lista) · D49 |
| 8 | **Ścieżka na drzewie** (v1.1; v1.16 — D45, D46, D48, D49): **„Do” staje w środku** (W2) — przestawienie środka jak po dotknięciu (element 4, ok. 0,45 s), karta (5) pokazuje „Do”. Drzewo przechodzi na **najniższy poziom, na którym widać całą ścieżkę**, licząc od osoby w środku; gdy ścieżka sięga dalej niż poziom 4 — poziom 4 i brakujące osoby ścieżki. **Kadr:** cała ścieżka na ekranie, 24 dp od krawędzi, pod banerem (jego wysokość przy danym tekście), w skali swojego poziomu (S2, element 3; **na poziomie 1 — 1,3**, dół zakresu, bez przybliżania ponad próg poziomu — v1.17, odstępstwo 2 ISSUE-039, D46); gdy się w niej nie mieści — **mniejsza skala, aż się zmieści** (F2; najmniej 0,15, a po końcu podświetlenia skala wraca do 0,4). Osoby spoza ścieżki — **30% krycia**; **linie rodziny i ślady — wszystkie przy 30%**, także osób ze ścieżki, jedną warstwą; drogę niesie linia w akcencie (v1.17, odstępstwo 5 z przeglądu ISSUE-039; do v1.16 „razem z ich liniami i śladami”). **Linia w akcencie** (3 dp, ta sama grubość przy każdej skali) biegnie po liniach rodziny — para: pozioma; rodzic–dziecko: przez kreskę do dzieci; rodzeństwo: przez kreskę rodziców — **od „Od” do „Do”, ok. 0,7 s na krok**; osoba, do której doszła, dostaje pierścień i poświatę w akcencie ([[style-b]] reguła 2). Imiona osób ze ścieżki mają pierwszeństwo przy chowaniu nakładających się (przed osobą w środku; I2, D27). **Ograniczenie animacji** — od razu cała ścieżka (D5). **Rok:** ścieżka przestawia suwak na „dziś” i zatrzymuje ▶ (Y1, D48). **Koniec podświetlenia** (D49): dotknięcie drzewa (także osoby — pierwsze dotknięcie tylko kończy), wstecz, przybliżanie i oddalanie (także + / −), ▶, suwak, „Przesyłaj na telewizor”, **zmiana danych drzewa** (v1.17, odstępstwo 3 ISSUE-039); przeciąganie przesuwa i nie kończy. Osoba w środku, poziom i skala zostają | animacja na drzewie | dotknięcie drzewa / wstecz → koniec podświetlenia | — | — | **decyzja autora** (D21, D26) · D5 · D45, D46, D48, D49 |
| 9 | **Baner** (v1.1; v1.16 — D43, D47) u góry drzewa, 12 dp od góry i 16 dp od boków, na powierzchni, zaokrąglony 12 dp, wyśrodkowany, zawija się; pojawia się, **gdy linia dojdzie do „Do”** (przy ograniczeniu animacji — od razu). **„Od” = „Ja”:** jedna linia — nazwa ze słownika Twoim głosem, ten sam tekst co w karcie (16 sp, półgruby, kolor tekstu), np. „Babcia mojej żony” (G2, D28). **„Od” to ktoś inny** (O2, D47): pierwsza linia „Piotr Przykładowy → Zofia Wymyślona” (13 sp, tekst pomocniczy; „Ja”, gdy jedną z osób jesteś Ty), druga — nazwa bez zaimka: „Wnuczka”, „Siostrzenica bratowej”. **Wysokość wiersza 1,3** w obu liniach, a nie 1,43 z motywu: kadr (8) mierzy baner tymi samymi stylami, którymi się rysuje, więc przy 200% nie zasłania góry ścieżki; przy 100% baner jest przez to o kilka dp niższy niż w makiecie (v1.17, odstępstwo 4 ISSUE-039). **Czas:** 4 s, dłużej, gdy zaleca ustawienie „Czas na działanie” (`getRecommendedTimeoutMillis` z flagami treści tekstowej, jak Snackbar Androida — D43). Czytnik ogłasza baner raz, bez przenoszenia fokusu (komunikat stanu, SC 4.1.3) — jako **region na żywo**, jak pigułka poziomu (element 3), a nie osobnym ogłoszeniem (v1.17, odstępstwo 1 ISSUE-039, D43). Bez zdania ścieżki i **bez „Odtwórz jeszcze raz”** (D26) | baner | znika sam; koniec podświetlenia też go chowa | — | — | **decyzja autora** (D26) · D6 · D43 · D47 |
| 10 | **Bez ścieżki:** baner jak 9, jedna linia: „Te osoby nie łączą się — w drzewie brakuje rodziny między nimi.”; drzewo bez zmian — środek, poziom i rok zostają | baner | — | — | — | reguła 9 |

## States
| Stan | Co widać |
|---|---|
| drzewo | 1, 3–5 (6 od US-010); na starcie „Ja” w środku, poziom 2 |
| oddalenie (poziom 3–4) | 1, 3–5; imiona według I2 — czytelne, nakładające się chowają (element 4, D27); na chwilę pigułka „Poziom 3 · 66 osób” |
| rok w przeszłości (US-010) | 4 bez osób nieurodzonych (miejsca zostają), linie par według dat związku, znicze zmarłych do tego roku, przerywany obrys przy osobach w oknie daty (N3); ślad dalszej rodziny i pigułka poziomu liczą tylko osoby, które w tym roku już są (D37); 5 bez zmian; 6 z rokiem (v1.12) |
| osoba w środku przed narodzinami (US-010) | 4: w jej miejscu pusty pierścień w akcencie (C1, D33); 5 bez zmian; czytnik „… — przed narodzinami” |
| odtwarzanie (US-010) | 6: ❚❚ zamiast ▶, rok biegnie w wybranym tempie (domyślnie „Średnio”, 10 lat na sekundę — v1.14, D41); dotknięcie osoby i oddalanie działają dalej (D37) |
| ograniczenie animacji (US-010) | jak odtwarzanie, ale rok skacze o dekadę co ok. 2 · 1 · 0,5 s według tempa, osoby pojawiają się od razu (R2, D36, D41) |
| połącz — wybór (US-011) | 1, okno 7 nad przyciemnionym drzewem; kafel → lista „Od kogo?” / „Do kogo?” na cały ekran, bez dolnego paska; wyszukiwanie bez wyniku — „Nie ma osoby „…”.” (jak [[osoby]]) |
| połącz — ścieżka (US-011) | 1, 3–6 („Do” w środku, karta „Do” z nazwą pokrewieństwa, suwak na „dziś”), 8 (reszta 30%), 9 od dojścia linii do „Do” przez ok. 4 s (v1.16) |
| połącz — ścieżka, tekst 200% (US-011) | jak wyżej; w oknie 7 kafle jeden pod drugim; baner do 4 linii przy „Od” innym niż Ty, kadr pod nim; skala zwykle poniżej 0,4 (F2), imię jednej z osób ścieżki może się schować (makieta: Ja → Wanda, 1 z 4) |
| bez ścieżki (US-011) | 1, 3–6 bez zmian, 10 przez ok. 4 s |
| osoba bez rodziny | 4: tylko ona, bez śladu; 5 („… · nie wiadomo jeszcze, kim jest dla mnie”, chyba że to „ja”) |
| osoba spoza rodziny „ja” | 4: jej rodzina; 5 z „nie wiadomo jeszcze, kim jest dla mnie” |
| „ja” niewybrane | 1 bez ikon; w miejscu drzewa, na środku: „Aplikacja nie wie jeszcze, która osoba to Ty.” (16 sp, tekst pomocniczy) i przycisk tekstowy w akcencie „Wybierz, która osoba to Ty” (jak [[osoba]] element 7); bez karty i + / −. Wejście z „Pokaż w drzewie” działa — wtedy 5 bez pokrewieństwa (D19) |
| pusta baza | 1 bez ikon; na środku „Tu pojawi się drzewo — osoby z grobów i ich rodziny.” (16 sp, tekst pomocniczy; jak „pusta baza” w [[osoby]]), bez działania (D19) |
| tekst 200% | 4 z szerszym miejscem osoby; 5 z „Pokaż ›” pod tekstem; + / − bez zmian, 48 dp (D20) |
| przesyłanie — ekran systemu (v1.10) | nie ekran aplikacji: ustawienia telefonu („Google Cast” na emulatorze z Androidem 16; jasny, w języku telefonu), lista telewizorów w tej samej sieci Wi-Fi albo „No nearby devices were found.” (zrzut `01`). Wstecz wraca do aplikacji |
| tryb prezentacji | 11 — po ekranie systemu bez podpowiedzi; rok z karty (Z2), w rogu, gdy nie jest „dziś” (L1) |
| tryb prezentacji — sterowanie (v1.14, ISSUE-038) | 11 + „Zakończ prezentację” u góry po prawej i listwa na dole (▶ / ❚❚, rok początku, suwak, tempo); rok w rogu także na „dziś”; 5 s od ostatniego dotyku (B2, D40); z czytnikiem ekranu od wejścia w tryb i bez chowania (v1.15) |
| tryb prezentacji — historia (v1.14, ISSUE-038) | 11 jak „rok w przeszłości” i „odtwarzanie”; rok w rogu zmienia się z ▶, sterowanie schowane; na „dziś” napis „dziś” jeszcze 3 s (L1, D39) |
| tryb prezentacji — telefon bez ekranu przesyłania (v1.10, ISSUE-036 AC-2) | 11 z podpowiedzią D26; aplikacja nie pada |
| błąd odczytu | „Nie udało się odczytać drzewa.” (tekst pomocniczy) i przycisk z obrysem „Spróbuj ponownie” (jak w [[osoby]]) |
| wczytywanie | wskaźnik postępu (lokalna baza — zwykle niewidoczny) |

## Sketch
```
┌──────────────────────────────────┐
│ Drzewo                    ↝  [⌔] │  ← [⌔] „Przesyłaj na telewizor” (US-009, v1.10 — P2) · ↝ „Połącz dwie osoby” (US-011)
│  (R)━(A)       (J)━(M)           │  ← ━ małżeństwo (róż), │ rodzic–dziecko (niebieski)
│    │             │               │
│ (E) (M)━━━━━(A)  (S)  (P)━(H)    │  ← rodzina partnera po prawej
│        │               │         │
│   (O) [JA]━━━━━(K)  (Mi)         │  ← [JA] znak „Ja”; pierścień — osoba w środku
│          │                   (+) │
│        (Z)                   (−) │  ← + / − (48 dp) w rogu drzewa: przybliż · oddal (S2)
│ ╭──────────────────────────────╮ │
│ │ (Ja) Mateusz Wymyślony       │ │
│ │      ur. 1983 · to ja Pokaż ›│ │
│ │(▶) 1860 ━━━━━●━━ 1984 Średnio│ │  ← suwak czasu — US-010 (v1.12): ▶ 36 dp, rok w akcencie, „dziś” na końcu; tempo (v1.14, V2)
│ ╰──────────────────────────────╯ │
│  Mapa      Osoby      Drzewo     │
└──────────────────────────────────┘
```

**Tryb prezentacji z historią** (v1.14 — ISSUE-038; poziomo, telefon 914 × 411 dp, obraz na telewizorze ten sam):
```
┌────────────────────────────────────────────────────────────────────────┐
│     ┌──────┐                                    ┌────────────────────┐ │
│     │ 1950 │  (J)━(Z)        (H) (K)            │ ✕ Zakończ prezent. │ │  ← rok L1: 36 sp, akcent, 48 dp od lewej · „Zakończ” tylko ze sterowaniem
│     └──────┘    │                               └────────────────────┘ │
│   (J)···                                                                │
│                         ◯                                               │  ← ◯ „Ja” przed narodzinami (C1)
│                                                                         │
│  ╭──────────────────────────────────────────────────────────────────╮  │
│  │ (▶) 1860 ━━━━━━━━━━━━━━━━━━━━━━━━━━●━━━━━━━━━━━━━━━━━━━━━  Średnio │  │  ← listwa B2: pusty dotyk → na 5 s; rok stoi w rogu, nie na końcu suwaka
│  ╰──────────────────────────────────────────────────────────────────╯  │
└────────────────────────────────────────────────────────────────────────┘
```

**„Połącz dwie osoby” — okno i ścieżka** (v1.16 — ISSUE-039; Ja → Wanda, W2; zrzuty `01`, `04` w `shots-039\`):
```
┌──────────────────────────────────┐   ┌──────────────────────────────────┐
│ Drzewo                    ⛓  [⌔] │   │ Drzewo                    ⛓  [⌔] │  ← ⛓ „Połącz dwie osoby” (A1)
│  ╭────────────────────────────╮  │   │       ╭───────────────────╮      │
│  │ Połącz dwie osoby          │  │   │       │ Babcia mojej żony │      │  ← baner 9, gdy linia dojdzie do „Do”
│  │ ┌──────────┐   ┌──────────┐│  │   │       ╰───────────────────╯      │
│  │ │Od        │ → │Do        ││  │   │  ·(LW) ·(CW)      ((WP))  ·(EP)  │  ← „Do” w środku (W2); · = 30% krycia
│  │ │   (Ja)   │   │  ( + )   ││  │   │                     ┃            │
│  │ │ Mateusz  │   │ Wybierz  ││  │   │  ·(RW) ·(AP)  ((PP))┛            │  ← linia w akcencie po liniach rodziny
│  │ │Wymyślony │   │  osobę   ││  │   │                 ┃                │
│  │ └──────────┘   └──────────┘│  │   │ ((Ja))━━((KW))━┛  ·(WP) ·(AP)    │  ← osoby ze ścieżki: pierścień i poświata
│  │                     Anuluj │  │   │ ╭──────────────────────────────╮ │
│  ╰────────────────────────────╯  │   │ │(WP) Wanda Przykładowa z d. … │ │
│                                  │   │ │ ur. 1934 · Babcia mojej żony │ │  ← karta „Do” trzyma nazwę po banerze
└──────────────────────────────────┘   └──────────────────────────────────┘
```

## Tempo
n/a — ekran do oglądania.

## Style B rules applied
- **Nowa rola — kolory relacji** ([[style-b]] v1.16): rodzic–dziecko i partnerzy, każda ≥ 3:1 na tle (SC 1.4.11). Między
  sobą różnią się tylko odcieniem (1,04:1), więc **rodzaj linii niesie też kształt i styl**: rodzic–dziecko łamana z góry
  w dół, para pozioma, „razem” przerywana (SC 1.4.1); bez legendy (v1.1, D25 — poprawione w v1.4).
- **Reguła 1 (akcent):** ścieżka „Połącz dwie osoby”, osoba w środku, aktywny segment i suwak — wybór i fokus, nie relacje.
- **Reguła 8:** znicz na węźle osoby zmarłej (R3); znicz na krążku w kolorze tła leży nad wieńcem rodu (v1.18).
- **Reguła 14:** węzły to okręgi profilowego w kadrze; bez zdjęcia — inicjały.
- **Reguła 2:** poświata tylko na osobie w środku i na zapalonych węzłach ścieżki.
- **Ślad dalszej rodziny (D9, v1.3):** kolory relacji przy kryciu 60% — 3,75:1 (rodzic–dziecko) i 3,66:1 (partnerzy) na tle, ≥ 3:1
  (SC 1.4.11); rola w [[style-b]] od v1.24.
- **Reguła 1 (v1.5):** znak „Ja” w akcencie (jak [[osoby]] D4) nie oznacza wyboru, więc węzeł „ja” ma obrys w kolorze obrysu. Pierścień i
  poświata w akcencie zostają dla osoby w środku (D14). Znak „Ja” na powierzchni 8,04:1, obrys na tle 3,40:1.
- **Imiona przy oddalaniu (I2, v1.6; v1.7 — D23; potwierdzone w v1.9 — D27):** tabliczka w kolorze tła (na jednolitym tle drzewa działa jak
  obwódka przy podpisach miast) i chowanie nakładających się ([[style-b]] reguła 13, v1.26), bo przy oddaleniu linie przechodzą pod podpisem; imię
  to tekst na tle, 10,98:1 (przeliczone z `theme.dart` 2026-10-14).
- **Reguła 7 — kto mówi (v1.9, D28; [[style-b]] v1.28):** nazwa pokrewieństwa Twoim głosem („Moja babcia”, „to ja”), zdania aplikacji do Ciebie
  („Wybierz, która osoba to Ty”).
- **Cel dotyku (v1.5):** na poziomie 4 poniżej 48 dp — wyjątek w [[style-b]] *Thresholds* (v1.24), D17.
- **Tryb prezentacji (v1.5):** „Zakończ prezentację” — powierzchnia z obrysem (3,40:1 na tle), `close` w akcencie (8,04:1 na powierzchni),
  napis w kolorze tekstu (10,02:1); pigułki na powierzchni w kolorze tekstu (10,02:1). Ikona telewizora w pasku — akcent na tle 8,81:1 (reguła 3:
  działanie). **v1.8:** zbudowane tak samo, pary przeliczone z `theme.dart` 2026-10-14 — wyniki te same.
- **Tokeny (v1.5):** bez nowych — tylko istniejące pary (przeliczone z `theme.dart` 2026-10-13).
- **„Przesyłaj na telewizor” (v1.10):** `cast_outlined` (istnieje we Flutterze 3.41.1 — `icons.dart`, sprawdzone w SDK 2026-10-14) w akcencie, jak ikona
  telewizora przed nią: działanie (reguła 3), 8,81:1 na tle; bez nowych tokenów. Ikona ma `tooltip` (reguła 3). Czytnik dostaje dopisek „w ustawieniach
  telefonu”, bo dotknięcie prowadzi poza aplikację, tak jak „w innej aplikacji” przy linku zewnętrznym (reguła 1). Ikona zostaje ta sama także w czasie
  przesyłania (`cast_connected` odpada — D29: aplikacja nie wie, czy przesyłanie trwa).
- **Czas (v1.12, element 6):** ▶ — okrąg w akcencie z ikoną w kolorze tła (główne działanie karty, reguła 1; akcent na powierzchni 8,04:1), rok w akcencie
  (wybór, reguła 1; 8,04:1), rok początku — tekst pomocniczy na powierzchni (5,01:1), tor nieaktywny — obrys na powierzchni (3,10:1, SC 1.4.11). **Niepewność
  niesie kształt, nie kolor** (N3, SC 1.4.1): przerywany obrys okręgu w kolorze obrysu ma ten sam kontrast co ciągły (3,40:1 na tle), a imię zostaje tekstem na tle
  10,98:1. Przenikanie (N2) odrzucone pomiarem: imię przy kryciu 30–50% ma 2,04–3,56:1, próg 4,5:1 osiąga dopiero przy 60% (*Candidates — ISSUE-037* → *Pomiar*).
  Pusty pierścień (C1) — akcent na tle 8,81:1. „//” (E3) — kolor partnerów, jak linia, którą przecina. Bez nowych tokenów (przeliczone z `theme.dart` 2026-10-14).
  **Tabliczka imienia (D23) bez zmian:** suwak jest w karcie, więc tło drzewa zostaje jednolite i warunek *Obali* z D23 nie zachodzi.
- **Historia na telewizorze (v1.14, ISSUE-038):** rok w rogu — akcent na tabliczce w kolorze tła, 8,81:1 (reguła 1: to wartość suwaka, jak rok w karcie). Tabliczka, a nie
  obwódka liter, bo tło drzewa jest jednolite (reguła 13, D23). L3 odpada pomiarem: rok w tle jako tekst o kryciu 10% ma 1,20:1, a próg dla dużego tekstu (SC 1.4.3) to 3:1;
  przy kryciu 40% wciąż ma tylko 2,70:1, a tabliczki imion odcinają się od niego jak prostokąty, czyli spełnia się *Obali* z D23. Listwa — powierzchnia; ▶ jak w karcie
  (akcent 8,04:1 na powierzchni); tempo — przycisk tekstowy w kolorze tekstu (10,02:1 na powierzchni), bo stoi obok wypełnionego ▶ (reguła 1); tor suwaka jak w karcie. **Tekst
  dla telewizora** ma osobny próg w [[style-b]] *Thresholds* (v1.30): co rodzina ma przeczytać z kanapy — co najmniej 36 sp i 48 dp od bocznych krawędzi. Bez nowych tokenów
  (przeliczone z `theme.dart` 2026-10-14).
- **Stała szerokość zmiennego napisu (v1.15, [[style-b]] reguła 5, v1.31):** rok w karcie (v1.13) i przycisk tempa (v1.15) mają szerokość najszerszej swojej wartości, więc tor suwaka
  obok nich ma stałą długość. Pary bez zmian (przeliczone z `theme.dart` 2026-10-14, przegląd `ui`): rok w rogu 8,81:1 na tabliczce · ▶ i aktywny tor 8,04:1 · ikona na ▶ 8,81:1 ·
  tempo i napis „Zakończ” 10,02:1 · rok początku 5,01:1 · tor nieaktywny 3,10:1 · obrys „Zakończ” 3,40:1 na tle.
- **„Połącz dwie osoby” (v1.16, ISSUE-039):** ikona `link_outlined` w akcencie (działanie, reguła 3; 8,81:1 na tle), ta sama co przy „Jak łączy się ze mną” w [[osoba]] 7. Linia ścieżki,
  pierścienie i poświata — akcent (wybór i fokus, reguły 1 i 2; 8,81:1 na tle). **Reszta drzewa przy 30% krycia — poniżej progów, celowo:** imię 2,04:1, obrys 1,34:1, linia rodzic–dziecko
  1,83:1. Na czas podświetlenia to tło bez działania (dotknięcie gdziekolwiek tylko kończy podświetlenie), a [WCAG 2.2](https://www.w3.org/TR/WCAG22/) SC 1.4.3 i 1.4.11 nie stawiają
  wymagań elementom nieaktywnym; informację niosą osoby ze ścieżki w pełnym kontraście, a kolor nie jest jedynym nośnikiem (pierścień i linia mają kształt — SC 1.4.1). Okno — powierzchnia;
  obrys kafla 3,10:1 na powierzchni (SC 1.4.11); „Wybierz osobę” — akcent 8,04:1; podpis „Od” / „Do” i pierwsza linia baneru — tekst pomocniczy 5,01:1; baner — tekst 10,02:1 na powierzchni.
  Bez nowych tokenów (przeliczone z `theme.dart` 2026-10-14). **v1.17** (przegląd `ui` zbudowanego ekranu, odstępstwa 5 i 6): przy 30% są wszystkie linie rodziny i ślady, także osób ze ścieżki
  (linia partnerów 1,78:1); linia w akcencie leży na nich z 4,81:1 wobec linii rodzic–dziecko przy 30%, więc droga odcina się od reszty kształtem i jasnością. Znak „Ja” w kaflu „Od” ma obrys
  w akcencie jak w [[osoby]] (D4), a nie w kolorze obrysu jak w drzewie (D14): w oknie nie ma osoby w środku, z którą pierścień mógłby się pomylić. Pary przeliczone z `theme.dart` 2026-10-14
  — wyniki jak wyżej.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| M9 — drzewo rodziny z powinowatymi i powtórnymi związkami | 3, 4 | poziom 2 od „Ja”: rodzice, dziadkowie, rodzeństwo, żona i jej rodzina po prawej |
| US-009 AC-1 — od „Ja” | 1, 3, 4, 5 | zakładka Drzewo: „Ja” w środku z pierścieniem, poziom 2 — rodzice, Kasia, dzieci, rodzeństwo, dziadkowie, rodzina Kasi po prawej |
| US-009 AC-2 — przestawianie środka | 4, 5 | dotknięcie Kasi → ona w środku z animacją, karta „ur. 1985 · Moja żona” (v1.9, G2); drugie dotknięcie albo „Pokaż” → widok Kasi |
| US-009 AC-3 — dalsza rodzina (S2) | 3 | − → „Poziom 3 · 66 osób”; + albo podwójne dotknięcie → „Poziom 2 · 20 osób” |
| US-009 AC-4 — ślad dalszej rodziny | 4 | na poziomie 2 osoba z rodziną poza widokiem ma bladą kreskę 3/3: w górę rodzice, w dół dzieci, w bok partner |
| US-009 AC-5 — nazwa pokrewieństwa w karcie | 5 | „Moja ciotka (siostra taty)” · „Mój stryj (brat taty)” · „Mój wuj (brat mamy)” · „Moja siostra cioteczna (córka siostry taty)” · „Siostra cioteczna mojego dziadka” · ścieżka Ja → żona → jej mama → jej mama → jej rodzic → jego rodzeństwo → jego dziecko: „Siostra cioteczna babci mojej żony” · mama taty: „Moja babcia” (v1.9, G2 — D28; makieta, sekcja 2; D12) |
| US-009 AC-6 — „Pokaż w drzewie” | [[osoba]] 6 → 4, 5 | w widoku Franciszka „Pokaż w drzewie” → zakładka Drzewo, Franciszek w środku, poziom 2 |
| US-009 AC-7 — tekst 200% na 360 dp | 4, 5 | miejsce osoby 160 dp, imię 26 sp bez ucięcia, inicjały 1,3× w okręgu; „Pokaż ›” pod tekstem karty |
| US-009 AC-8 — tryb prezentacji | 1, 11 | „Przesyłaj na telewizor” → ekran systemu → wstecz → poziomo, poziom 2 dopasowany, bez przycisków; dotknięcie pustego miejsca → „Zakończ prezentację” (v1.10; do v1.9 — ikona telewizora) |
| ISSUE-036 AC-1 — „Przesyłaj” otwiera systemową listę | 1 | dotknięcie `cast_outlined` → ekran ustawień „Google Cast” z listą urządzeń w pobliżu (emulator: pusta, zrzut `01`); po powrocie tryb prezentacji bez podpowiedzi |
| ISSUE-036 AC-2 — telefon bez listy | 1, 11 | brak ekranu przesyłania → aplikacja nie pada, tryb prezentacji z podpowiedzią „Obraz na telewizor: przesyłanie ekranu w szybkich ustawieniach telefonu” (D26) |
| M10 — suwak czasu: urodzenia, związki, zgony (US-010) | 6 | rok 1984: „Ja” jest, rodzice „razem” (przerywana), ślub 1985 — ciągła |
| US-010 AC-1 — rok na suwaku | 4, 6 | „Ja” w środku, rok 1950: na poziomie 2 jest 5 z 20 osób, w miejscu „Ja” pusty pierścień (C1); dziadkowie bez znicza; rok 2010: znicz u babci zmarłej w 2010 (makieta, wymyślona rodzina) |
| US-010 AC-2 — związki w czasie | 4, 6 | rodzice „Ja” (razem od 1982, ślub 1985): 1981 — bez linii, 1984 — przerywana, 1986 — ciągła; para bez daty ślubu — linia od urodzenia najstarszego dziecka |
| US-010 AC-3 — odtwarzanie | 6 | ▶ od 1860 → „dziś” w ok. 8 s (od 1880 — ok. 7 s; zmierzone na emulatorze: 8,4 s, ok. 19,7 lat/s — v1.13, odstępstwo 1 ISSUE-037), ❚❚ zatrzymuje; „Usuń animacje” w systemie → co ok. 1 s dekada, bez przenikania (R2) |
| ISSUE-037 — data niepewna i brak daty | 4, 6 | „ur. przed 1900” w roku 1890: osoba z przerywanym obrysem (N3); „zm., data nieznana” w roku 1960: przerywany obrys, znicz dopiero na końcu okna |
| ISSUE-037 — tekst 200% na 360 dp | 5, 6 | rok początku i rok nad suwakiem, ▶ (cel 48 × 48 dp) i suwak w rzędzie pod nimi; nic nie jest ucięte |
| ISSUE-037 — koniec związku (E3) | 4 | para rozstana w 1995: w 2000 i na „dziś” „//” na linii pary, linia do dzieci zostaje |
| ISSUE-038 — ▶ w prezentacji, rok na telewizorze | 11 | pusty dotyk → listwa; ▶ od 1860 do „dziś”, rok w rogu zmienia się z ▶, ❚❚ zatrzymuje; „dziś” zostaje 3 s; rok w 36 sp, 48 dp od lewej (L1, B2) |
| ISSUE-038 — tempo w karcie i w prezentacji | 6, 11 | „Średnio” → „Wolno”: od 1880 do dziś ok. 29 s zamiast ok. 15 s, „Szybko” — ok. 7 s; to samo tempo w karcie i w listwie (makieta, `#playtest`: po 3,5 s od 1860 rok 1877 · 1895 · 1930) (V2) |
| ISSUE-038 — ograniczenie animacji | 6 | „Usuń animacje”: dekada co ok. 2 · 1 · 0,5 s według tempa, bez przenikania (R2 zostaje) |
| ISSUE-038 — prezentacja z roku Y | 11 | karta na 1950 → „Przesyłaj na telewizor” → wstecz: tryb w roku 1950, ▶ stoi; „Zakończ prezentację” → karta w roku 1950 (Z2) |
| ISSUE-038 — tekst 200% | 6, 11 | tempo w górnym rzędzie karty, suwak 278 dp bez zmian; listwa w jednym rzędzie (suwak 614 dp na 914 dp); rok w rogu 47 sp |
| M11 — ścieżka między dowolnymi dwiema osobami (US-011) | 7–9 | „Ja” → „Wanda Przykładowa” (v1.2: przykład z wymyślonych rdzeni, retro 3 R7): Wanda w środku, poziom 3 (skala 0,85), linia przez Kasię i Piotra, reszta przy 30%, baner i karta „Babcia mojej żony” (v1.16 — W2; makieta, zrzut `04`) |
| US-011 AC-1 — wybór osób | 1, 7 | ikona `link_outlined` → okno: „Od” — „Ja” (Mateusz Wymyślony), „Do” — „Wybierz osobę”; „Do” → „Do kogo?” z wyszukiwarką i A–Z; wybór Wandy zamyka okno (zrzuty `01`, `02`) |
| US-011 AC-2 — ścieżka na drzewie | 4, 8 | jw.; „Usuń animacje” — cała ścieżka od razu; najszersza ścieżka od „Ja” (Zdzisław, „Stryj mojej mamy”) — skala 0,34, cała ścieżka na ekranie (F2, zrzut `11`) |
| US-011 AC-3 — baner z nazwą | 9 | „Babcia mojej żony” przez ok. 4 s po dojściu linii; „Od” = Piotr, „Do” = Zofia (ur. 2012): „Piotr Przykładowy → Zofia Wymyślona” / „Wnuczka” (O2, zrzut `06`) |
| US-011 AC-4 — bez ścieżki | 10 | „Ja” → „Teofil Przykładowski” (wymyślona osoba bez rodziny): baner „Te osoby nie łączą się — w drzewie brakuje rodziny między nimi.”, drzewo bez zmian (zrzut `08`) |
| ISSUE-039 — tekst 200% na 360 dp | 7, 9 | kafle jeden pod drugim, imię zawija się na spacji („Wanda / Przykładowa”), okno 328 × 458 dp; baner do 4 linii (zrzut `12`) |

## Candidates — SPIKE-002 (2026-10-13)
> Makieta `drzewo-spike002.html` (*mockup* we frontmatterze) pokazuje ton, układ i liczby. **Nie** pokazuje gestów ani płynności
> Fluttera, a czytelność na fizycznym ekranie telefonu sprawdzimy przed instalacją MVP ([[ISSUE-032-mvp-install]] → *Hand checks*;
> decyzja autora w `/pm` 2026-10-13). Układ liczy algorytm makiety: rzędy według pokolenia, para jako blok, kolejność w rzędzie według
> środków ciężkości z najmniejszą liczbą skrzyżowań i położenie w poziomie z regresji izotonicznej. W parze pierwszeństwo ma osoba
> bliższa środkowi, więc rodzina partnera wisi z boku (D8). Algorytm do Fluttera wybiera plan.

| # | Kandydat | Co widać | Gdzie się dotyka | Źródło |
|---|---|---|---|---|
| K1 | **Całe drzewo naraz** | wszyscy w rzędach według pokoleń; przesuwanie i przybliżanie jak na mapie | przeciągnięcie · dwa palce · przyciski + / − (48 dp) | kandydat 1 ze SPIKE-002 (biblioteka układu grafu) · D1 → *Obali* |
| K2 | **Od osoby, z poziomami** | osoba w środku i jej rodzina do poziomu z elementu 3 | dotknięcie osoby → ona w środku | D1 · kierunek autora (SPIKE-004 D20) |
| S1 | „− Poziom 2 · 20 osób +” | jak element 3 | przyciski 36 dp | v1 · autor: *„nie wygląda to estetycznie”* (D25) |
| S2 | **Oddalanie odsłania dalszą rodzinę** | jak na mapie: oddalasz, a dokłada się poziom; przybliżasz, a dalsza rodzina znika; na chwilę pigułka „Poziom 3 · 66 osób” | dwa palce · przyciski + / − w rogu (48 dp) jako dostęp jednym dotknięciem (SC 2.5.1, [[style-b]] *Thresholds* → gesty) | *Open* 1, kandydat a · DOI (D8) |
| S3 | **Suwak „Bliżej · Dalej”** | w dolnej karcie nad suwakiem czasu, pozycje 1–5 | przeciągnięcie albo dotknięcie suwaka | *Open* 1, kandydat b |
| — | **Ślad dalszej rodziny** | krótka, przerywana kreska przy osobie, która ma rodzinę poza widokiem: w górę — rodzice, w dół — dzieci, w bok — partner | bez akcji (podpowiedź) | D9 |
| — | **Tryb prezentacji** | poziomo, pełny ekran, bieżący poziom dopasowany do ekranu, bez przycisków; obraz na telewizor przez „Przesyłaj ekran” Androida | — | *Open* 2, kandydaci a + b |

**Pomiar** (makieta, od „Ja”; obszar drzewa 328 × 452 dp na ekranie 360 dp; miejsce osoby 80 dp, rząd 104 dp):

| Widok | Osób | Pokoleń | Szerokość | Skrzyżowania linii (przybliżenie) | Skala „zmieścić” | Imię przy tej skali | Miejsce osoby |
|---|---|---|---|---|---|---|---|
| K2 · poziom 1 | 6 | 3 | 212 dp | 0 | 1,00 | 13,0 sp ✅ | 80 dp ✅ |
| K2 · poziom 2 | 20 | 4 | 864 dp | 0 | 0,38 | 4,9 sp | 30 dp |
| K2 · poziom 3 | 66 | 5 | 1960 dp | 6 | 0,17 | 2,2 sp | 13 dp |
| K2 · poziom 4 | 99 | 6 | 2663 dp | 9 | 0,12 | 1,6 sp | 10 dp |
| K2 · poziom 5 | 106 | 6 | 2960 dp | 10 | 0,11 | 1,4 sp | 9 dp |
| K1 · wszyscy | 106 | 6 | 2960 dp | 10 | 0,11 | 1,4 sp | 9 dp |

Progi: tekst pomocniczy ≥ 13 sp ([[style-b]] *Thresholds*), cel dotyku ≥ 48 dp ([Android](https://developer.android.com/guide/topics/ui/accessibility/apps)).
Co z tego wynika dla ekranu:
- **bez przesuwania mieści się czytelnie tylko poziom 1.** Od poziomu 2 drzewo czyta się przez przesuwanie przy skali bliskiej 1,
  nie przez oglądanie całości. Pytanie spike'a dotyczy więc orientacji przy przesuwaniu, nie tego, czy całość się zmieści;
- **poziomy rosną skokami** 6 → 20 → 66 → 99 → 106. Od poziomu 4 to prawie cała rodzina, więc zakres 1–5 z elementu 3 jest dłuższy,
  niż trzeba (*Open* 1);
- **od poziomu 3 rodzina żony wisi na długich szynach** nad kuzynami ze strony mamy. To cecha kraty (D8), nie algorytmu: każda
  kolejność w rzędzie coś krzyżuje.

## Candidates — US-009 (2026-10-13)
> Makieta `drzewo-us009.html` (*mockup* we frontmatterze) ma tę samą wymyśloną rodzinę co SPIKE-002 (106 osób) i ten sam algorytm układu.
> Pokazuje *Open* 5 i 6, decyzje D12–D20 i stany. **Nie** pokazuje gestów ani płynności Fluttera, czytelności na fizycznym ekranie ani
> zdjęć w węzłach (tylko inicjały).

| # | Kandydat | Co widać | Gdzie się dotyka | Źródło |
|---|---|---|---|---|
| I1 | **Imiona maleją razem z drzewem** | jak w prototypie SPIKE-002: poziom 3 — ok. 9 sp, poziom 4 — ok. 6 sp | — | SPIKE-002 M4 |
| I2 | **Imiona zostają czytelne, a nakładające się chowają** | imię na ekranie ma zawsze co najmniej 13 sp (przy skali < 1 nie maleje), z obwódką w kolorze tła; gdy dwa by się nałożyły, zostaje to bliżej osoby w środku (najpierw poziom z D2, potem odległość w poziomie). Po przybliżeniu ukryte imiona wracają | przybliżenie: + albo dwa palce | podpisy na mapie ([[style-b]] reguła 13) · DOI (D8) |
| I3 | **Od poziomu 3 bez imion** | przy skali < 0,85 imię ma tylko osoba w środku, reszta to sam kształt rodziny | dotknięcie osoby → karta z imieniem | SPIKE-002 M4 („widać kształt rodziny”) |
| G1 | **„Twoja babcia” · „Siostra cioteczna babci Twojej żony”** | aplikacja mówi do Ciebie | — | [[osoby]] („Wybierz, która osoba to Ty”) · [[osoba]] 7 („…łączy się z Tobą”) |
| G2 | **„Moja babcia” · „Siostra cioteczna babci mojej żony”** | mówisz Ty | — | [[osoba]] 7 (nagłówek „Jak łączy się ze mną”) · US-009 AC-5 · D6 |

**Pomiar** (makieta, od „Ja”, ekran 360 dp, tekst 100%):

| Poziom · skala | Osób | I1 — imię | I2 — imion widać | I3 — imion widać | Miejsce osoby = cel dotyku |
|---|---|---|---|---|---|
| 2 · 1,00 | 20 | 13,0 sp | 20 z 20 | 20 z 20 | 80 dp ✅ |
| 3 · 0,69 | 66 | 9,0 sp | 62 z 66 | 1 z 66 | 55 dp ✅ |
| 4 · 0,48 | 99 | 6,2 sp | 63 z 99 | 1 z 99 | 38 dp (D17) |
| 4 · 0,40 (najmniejsza skala) | 99 | 5,2 sp | nie mierzone | 1 z 99 | 32 dp (D17) |

## Candidates — ISSUE-036 (2026-10-14)
> Makieta `drzewo-036.html` (*mockup* we frontmatterze) składa każdy wariant ze zrzutów z emulatora `Grobing_Restore` (Android 16, system po angielsku,
> wymyślona rodzina): drzewo, systemowy ekran przesyłania i tryb prezentacji. **Nie** pokazuje telewizora ani tego, co system pokaże po wyborze telewizora,
> bo emulator nie widzi żadnego (D29 → *Nie da*).

**Co naprawdę otwiera przycisk** (pomiar 2026-10-14, `am start -a android.settings.CAST_SETTINGS`): `com.android.settings/.Settings$WifiDisplaySettingsActivity` —
pełny, jasny ekran ustawień z tytułem „Google Cast”, ikoną przesyłania i listą urządzeń w pobliżu (na emulatorze „No nearby devices were found.”). Wstecz
wraca do aplikacji. **To nie jest okienko z listą nad treścią, jak „Przesyłaj” w Zdjęciach i YouTube** — tamto daje Google Cast SDK, którego tu nie ma (D11, D29).

| # | Kandydat | Co widać | Gdzie się dotyka | Dotknięć do obrazu na telewizorze |
|---|---|---|---|---|
| P1 | **Dwie ikony:** `cast_outlined` „Przesyłaj na telewizor” obok `tv_outlined` „Tryb prezentacji” | „Przesyłaj” → ekran systemu → po powrocie tryb prezentacji bez podpowiedzi; telewizor → tryb z podpowiedzią, jak dziś | ikona przesyłania · telewizor · wybór telewizora · wstecz | 3 (przesyłaj, telewizor na liście, wstecz) |
| P2 | **Jedna ikona `cast_outlined` zamiast telewizora** | ekran systemu → po powrocie tryb prezentacji bez podpowiedzi; telefon bez ekranu przesyłania → od razu tryb z podpowiedzią | ikona przesyłania · wybór telewizora · wstecz | 3; **sam tryb bez telewizora** — też 2 (ikona, wstecz) |
| P3 | **Przesyłanie z trybu prezentacji:** telewizor jak dziś, w trybie podpowiedź staje się przyciskiem „Przesyłaj ›” (4 s), a pusty dotyk pokazuje „Przesyłaj” obok „Zakończ prezentację” | tryb poziomo → ekran systemu (pionowo albo poziomo, zależnie od ustawienia obracania) → z powrotem tryb | telewizor · „Przesyłaj ›” · wybór telewizora · wstecz | 4, ekran obraca się w trakcie |

**Rekomendacja: P2.** Autor na stopie #2 ISSUE-034: *„chciałem aby ten tryb telewizora streamował obraz do smart TV … jak w YouTube”*, czyli przycisk telewizora
miał wysyłać obraz. P2 robi to jednym przyciskiem. Ma ikonę przesyłania, tę samą co ekran systemu, kafelek w szybkich ustawieniach i YouTube. Stoi tam, gdzie Google
każe stawiać przycisk przesyłania: *„In mobile apps, display the Cast button on the right side of the screen”*, a *„the Cast button is not specific to Google
Cast”* ([Google Cast Design Checklist → Cast button](https://developers.google.com/cast/docs/design_checklist/cast-button), odczyt 2026-10-14). P1 stawia obok
siebie dwie ikony o podobnym znaczeniu, a po US-011 w pasku byłyby trzy. P3 obraca ekran w trakcie i kosztuje dotknięcie więcej.
**Nie da (P2):** trybu prezentacji jednym dotknięciem bez telewizora (wchodzi się przez ekran systemu i wstecz).

## Candidates — ISSUE-037 (2026-10-14)
> Makieta `drzewo-037.html` (*mockup* we frontmatterze) to makieta US-009 (106 wymyślonych osób, ten sam układ) z suwakiem w karcie. W rodzinie są
> daty niepewne i brakujące, jakich można się spodziewać w notatkach: „ok.”, „między”, „przed”, „po”, osoby bez daty urodzenia, zmarły bez daty śmierci,
> trzy pary bez daty ślubu, rozstanie. Przełączniki w sekcjach 1–5, „Pokaż, gdzie się dotyka”, tekst 200%, self-test `#test=1` i `#playtest=1`. **Nie** pokazuje
> płynności Fluttera ani zdjęć w węzłach. Zrzuty `shots-037\`.

| # | Kandydat | Co widać | Gdzie się dotyka | Źródło |
|---|---|---|---|---|
| N1 | **Jeden rok z daty** | „ok. Y”, „przed Y”, „po Y” → rok Y; „między A a B” → środek; brak daty → środek okna z rodziny. Niepewności na drzewie nie widać — mówi o niej karta | suwak · ▶ | element 6 v1 („osoba urodzona po Y znika”) |
| N2 | **Osoba pojawia się stopniowo** | w oknie daty osoba blada (krycie 30% → 100%), znicz tak samo | suwak · ▶ | TimeNets: lifeline blednie gradientem przy niepewnej dacie (D31) |
| N3 | **Przerywany obrys: „nie wiadomo, czy w tym roku żyje”** | osoba od początku okna urodzenia, z przerywanym obrysem do jego końca; ten sam obrys w oknie śmierci, znicz na końcu okna | suwak · ▶ · dotknięcie osoby → karta z datą z dopiskiem | TimeNets (znacznik niepewności) + Priestley 1765 (kropki przy niepewnych datach, D31) |
| C1 | **Pusty pierścień** w miejscu osoby w środku przed jej narodzinami | pierścień w akcencie, bez okręgu i imienia; karta bez zmian | — | AC-1 („miejsce zostaje”) |
| C2 | **Osoba w środku zostaje, wyszarzona** | wyjątek od AC-1 dla osoby w środku | — | — |
| T1 | **Zawsze od 1880** | starsi od 1880 są na drzewie od początku suwaka | — | US-010 AC-3 |
| T2 | **Od pełnej dekady przed najwcześniejszą datą, najpóźniej 1880** | tu 1860; na początku drzewo jest puste | — | D4 (*„jeżeli ktoś się rodzi to dopiero ma się pojawić”*) |
| E1 | **Koniec związku bez zmian na drzewie** | linia pary zostaje | — | dziś w kodzie (ISSUE-033) |
| E2 | **Po końcu linia znika** | także na „dziś”; linia do dzieci wisi między rodzicami | — | — |
| E3 | **„//” na linii od roku końca** | dwie ukośne kreski przez linię pary, linia do dzieci zostaje; także na „dziś” | — | genogram (D35) |
| R1 | **Ograniczenie animacji: ▶ od razu na „dziś”** | jak D5 („od razu cała ścieżka”) | ▶ | D5 |
| R2 | **Ograniczenie animacji: dekadami co ok. 1 s** | rok skacze o 10 lat, osoby pojawiają się od razu | ▶ | WCAG 2.2 SC 2.3.3 (D36) |

**Pomiar** (kontrast według WCAG 2.2 z `theme.dart`, 2026-10-14; skrypt w katalogu sesji):

| Co | N2 krycie 30% | 40% | 50% | 60% | N3 (pełne krycie) | Próg |
|---|---|---|---|---|---|---|
| imię (tekst na tle) | 2,04 | 2,70 | 3,56 | 4,61 | 10,98 | 4,5 (SC 1.4.3) |
| obrys okręgu na tle | 1,34 | 1,52 | 1,72 | 1,97 | 3,40 (przerywany) | 3 (SC 1.4.11) |
| znicz (akcent) na tle | 1,85 | 2,38 | 3,05 | 3,84 | 8,81 | 3 (SC 1.4.11) |

Makieta, „Ja” w środku, poziom 2 (20 osób): rok 1900 — 0 osób na drzewie i pusty pierścień; 1950 — 5; 1984 — 14; „dziś” — 20. ▶ od 1860: po 3,5 s rok 1933, „dziś” po ok. 8 s;
przy ograniczeniu animacji po 3,5 s 1890, po 9 s 1950 (`#playtest=1`, Chrome bez okna). Tekst 200% na 360 dp: ▶ 48 × 48 dp, suwak 278 dp w drugim rzędzie (przy 100% — 194 dp
w jednym).

**Rekomendacja: N3, C1, T2, E3, R2.**
- **N3:** TimeNets: *„Without indications of uncertainty, visual analysis may lead to inaccurate conclusions”* (D31). N1 tych oznaczeń nie ma, a „przed 1900” pokazuje
  osobę dopiero w 1900, czyli za późno. N2 oznacza niepewność kryciem: imię ma mniej niż 4,5:1 aż do 60% krycia (*Pomiar*), a krycie ok. 30% to już „wyszarzenie”
  osób spoza ścieżki w US-011 (element 8). N3 niesie niepewność kształtem, imię zostaje czytelne, a znicz znaczy jedno: „na pewno nie żyje” (D22).
  **Nie da:** stopniowania — osoba z oknem 10 lat i 40 lat wygląda tak samo; ile wiadomo, mówi karta.
- **C1:** środek i drzewo się nie ruszają, a pierścień mówi, skąd czytasz. C2 łamie AC-1 dla jednej osoby. **Nie da:** twarzy osoby w środku w latach przed nią.
- **T2:** każdy pojawia się wtedy, gdy się rodzi, także najstarsi (D4). Prędkość jest stała, więc od 1880 nadal ok. 7 s. **Zmienia AC-3:** „od 1880” → „od początku suwaka
  (najpóźniej 1880)”. **Nie da:** stałego napisu „1880”.
- **E3:** suwak ma pokazać, *kto z kim był razem* (US-010), a E1 rysuje parę razem także po rozstaniu. E2 zostawia linię do dzieci w powietrzu. **E3 zmienia też drzewo na
  „dziś”** (element 4) — decyzja projektowa, nie z AC. **Nie da:** rozróżnienia rozwodu i rozstania (genogram ma na to „/” i „//”, a model ma jeden „koniec związku” —
  [[rodzina]] A6).
- **R2:** historia odtwarza się dalej, ale nic się nie przesuwa ani nie przenika. R1 zostawia ▶ bez działania. **Nie da:** płynnego biegu przy ograniczeniu animacji.

## Candidates — ISSUE-038 (2026-10-14)
> Makieta `drzewo-038.html` (*mockup* we frontmatterze) to makieta ISSUE-037 (106 wymyślonych osób, ten sam układ i te same daty niepewne) z **trybem prezentacji poziomo**
> (914 × 411 dp jak emulator `Medium_Phone`, przełącznik na 780 × 360 dp) i **podglądem „z kanapy”**: drzewo w wielkości, w jakiej widać telewizor 32–65″ z 3 m, gdy siedzi
> się ok. 60 cm od monitora. Przełączniki w sekcjach 1–4, „Pokaż, gdzie się dotyka”, tekst 200%, „Usuń animacje”, self-test `#test=1` i `#playtest=1`. **Nie** pokazuje
> płynności Fluttera, prawdziwego telewizora (proporcji obrazu po przesłaniu, opóźnienia) ani zdjęć w węzłach. Zrzuty `shots-038\`.

| # | Kandydat | Co widać | Gdzie się dotyka | Źródło |
|---|---|---|---|---|
| L1 | **Rok w lewym górnym rogu** | 36 sp w akcencie na tabliczce w kolorze tła, 48 dp od lewej i 24 dp od góry; drzewo tej samej wielkości co dziś | — | skala TV Androida (display small, „numerals”), margines 5% (D38) |
| L2 | **Pas u góry, rok na środku** | rok 36 sp na środku u góry; drzewo dopasowane od 75 dp od góry zamiast od 24 dp | — | — |
| L3 | **Wielki rok w tle, za drzewem** | ok. 220 sp, tekst o kryciu 10% | — | „watermark year” w Gapminder (D38) |
| B1 | **▶ i tempo obok „Zakończ prezentację”** | pusty dotyk: w prawym górnym rogu ▶ / ❚❚, tempo, „Zakończ prezentację”; bez suwaka | pusty dotyk · ▶ · tempo | dziś: „Zakończ prezentację” (D25) |
| B2 | **Listwa na dole, jak w odtwarzaczu** | pusty dotyk: na dole ▶ / ❚❚, rok początku, suwak, tempo; u góry „Zakończ prezentację”; 5 s | pusty dotyk · ▶ · suwak · tempo · drugi pusty dotyk chowa | Media3 `PlayerControlView` (D38) |
| B3 | **Gest dwoma palcami** | bez przycisków; dwa palce w poziomie zmieniają rok | dwa palce · pusty dotyk (wyjście) | — |
| V1 | **Dwa tempa: „Wolno” · „Szybko”** | 10 · 20 lat/s, domyślnie „Wolno” | przycisk tempa (przełącza) | autor: *„dla mnie za szybko”* |
| V2 | **Trzy tempa słowami: „Wolno” · „Średnio” · „Szybko”** | 5 · 10 · 20 lat/s, domyślnie „Średnio” | przycisk tempa (przełącza) | jw. |
| V3 | **Trzy tempa jak w odtwarzaczu: „0,5×” · „1×” · „2×”** | te same 5 · 10 · 20 lat/s, domyślnie „1×” | przycisk tempa (przełącza) | prędkości w Media3 (D38) |
| Z1 | **Prezentacja zawsze od „dziś”** | jak w D37 | — | D37 |
| Z2 | **Prezentacja z rokiem z karty** | rok przechodzi do trybu i wraca, jak osoba w środku | — | D37 (rok to stan widoku) |

**Pomiar** (makieta i skrypt `tv_legibility.py` w katalogu sesji, 2026-10-14):

| Wysokość cyfry z 3 m (telefon 914 dp wypełnia szerokość telewizora 16:9) | 32″ | 43″ | 55″ | 65″ | Próg (ISO 9241, D38) |
|---|---|---|---|---|---|
| imię w drzewie, 13 sp | 8′ | 11′ | 14′ | 17′ | min. 16′, zwykle 20–22′ |
| rok w karcie, 16 sp | 10′ | 14′ | 17′ | 21′ | jw. |
| 24 sp (TV „headline small”) | 15′ | 20′ | 26′ | 31′ | jw. |
| **rok L1 / L2, 36 sp** (TV „display small”) | **23′** | **31′** | **39′** | **46′** | jw. — z 3,5 m na 32″: 19,5′ |

| Co | L1 | L2 | L3 |
|---|---|---|---|
| środki (ze 106, poziom 2, „dziś”), przy których rok przykrywa okrąg · imię — 914 dp | 0 · 0 | 0 · 0 | — (za drzewem) |
| to samo — 780 × 360 dp | 1 · 1 | 0 · 0 | — |
| to samo — tekst 200%, 914 dp | 2 · 1 | 0 · 0 | — |
| wielkość drzewa wobec dzisiejszej (mediana) — 914 dp · 780 dp · 200% | 100% | 86% (86–91%) · 84% · 82% | 100% |
| kontrast roku na tle (próg dla dużego tekstu 3:1) | 8,81:1 | 8,81:1 | 1,20:1 przy kryciu 10% · 2,04 przy 30% · 2,70 przy 40% |

Tempo (makieta, `#playtest`, od 1860): po 3,5 s rok 1877 · 1895 · 1930, po 9 s 1905 · 1950 · „dziś” (5 · 10 · 20 lat/s); „Usuń animacje” przy „Średnio” — 1890 i 1950, przy „Wolno” — 1870 i
1900. Suwak w karcie na 360 dp: przy 100% 193 dp bez przycisku tempa, z przyciskiem 129–137 dp; przy 200% 278 dp w obu. Listwa B2: suwak 691 dp (100%) i 614 dp (200%), listwa
w jednym rzędzie. Tryb prezentacji od „Ja” na „dziś”: L1 i L2 — 20 z 20 imion (100%), L1 przy 200% — 17 z 20.

**Rekomendacja: L1, B2, V2, Z2.**
- **L1:** rok czytelny z kanapy na każdym telewizorze z tabeli (≥ 16′ także na 32″ z 3,5 m), stoi tam, gdzie liczbę na ekranie stawia telewizja, i w makiecie nie przykrył nikogo przy
  żadnym ze 106 środków (na 360 dp przy jednym). L2 zabiera drzewu 14% wielkości w każdym pokazie, także na „dziś”, za przypadek, który w L1 prawie się nie zdarza. L3 nie spełnia
  progu kontrastu dużego tekstu nawet przy kryciu 40% i odsłania tabliczki imion (D23 → *Obali*). **Nie da:** gwarancji, że rok nigdy nie przykryje osoby — przy innym kształcie
  rodziny w rogu może ktoś stać, a dotknięcie osoby obok przestawia drzewo.
- **B2:** jeden suwak i jedno ▶ w dwóch miejscach, układ jak w odtwarzaczach, które ludzie znają z telewizora (YouTube, Media3), i rok przewijany ręcznie bez wychodzenia z trybu.
  B1 nie ma suwaka, więc powrót do 1950 to wyjście z trybu. B3 nie ma alternatywy jednym palcem (SC 2.5.1), bo jeden palec przeciąga drzewo (D25), a ▶ i tak potrzebuje przycisku.
  **Nie da:** sterowania niewidocznego dla rodziny — listwa przez 5 s jest też na telewizorze i przykrywa dolny rząd.
- **V2:** autor uznał 20 lat/s za za szybkie, więc domyślne jest o połowę wolniejsze, a „Szybko” zostaje dla tego, kto chce dzisiejszego tempa. „Wolno” daje ok. 5 s na pokolenie na
  opowiadanie przy telewizorze. Słowa mówią, co się stanie; „1×” w V3 nie mówi, ile to lat, a „2×” to tempo, które było za szybkie. V1 nie ma tempa na opowiadanie. **Zmienia
  US-010 AC-3** („od 1880 w ok. 7 s” → „w wybranym tempie, domyślnie ok. 15 s od 1880”) i szkic AC z ISSUE-038 (14 · 7 · 4 s → ok. 29 · 15 · 7 s). **Nie da:** tempa dobranego co do
  roku, tempa zapamiętanego po zamknięciu aplikacji (D41) i dłuższego suwaka w karcie przy 100% (193 → ok. 133 dp).
- **Z2:** rok to stan widoku, jak środek (D37), a tryb już przenosi osobę w środku; opowieść przygotowana na telefonie (osoba, rok) zaczyna się na telewizorze od tego miejsca.
  **Zmienia D37.** **Nie da:** pewności, że tryb pokazuje całą rodzinę — kto zostawił suwak na 1950, zobaczy 1950 (rok widać w rogu).

**Zauważone przy pomiarze, poza pozycją:** imiona w trybie prezentacji mają 13 sp (I2, D27), czyli z 3 m na 55″ ok. 14′, poniżej minimum 16′ — na telewizorze imiona czyta się
z bliska, rok z kanapy. Wraca na [[ISSUE-032-mvp-install]] → *Hand checks* (telewizor autora) i jako wejście do [[2026-10-14-opowiesc-rodziny-i-wieniec]] (opowieść na telewizorze).

## Candidates — ISSUE-039 (2026-10-14)
> Makieta `drzewo-039.html` (*mockup* we frontmatterze) to makieta ISSUE-038 (106 wymyślonych osób, ten sam układ, czas i tryb prezentacji) z **ikoną w pasku, oknem z kaflami,
> listą wyboru, ścieżką na drzewie i banerem**. Przełączniki w sekcjach 1–5, przykłady u góry (Ja → Wanda, Ja → Ewelina, Ja → najdalsza osoba, Ja → najszersza ścieżka, Ja → Teofil bez
> rodziny, Piotr → Zofia, rok 1950), „Usuń animacje”, „Czas na działanie”, tekst 200%, „Pokaż, gdzie się dotyka”, self-test `#test=1`. **Nie** pokazuje płynności Fluttera, zdjęć w węzłach
> ani prawdziwego czytnika ekranu. Zrzuty `shots-039\`.

| # | Kandydat | Co widać | Gdzie się dotyka | Źródło |
|---|---|---|---|---|
| A1 | **Ogniwa łańcucha** (`link_outlined`) | ikona w akcencie na lewo od „Przesyłaj na telewizor” | ikona → okno 7 | ta sama ikona przy „Jak łączy się ze mną” ([[osoba]] 7) |
| A2 | **Trasa między punktami** (`route_outlined`) | jw. | jw. | — |
| A3 | **Punkty połączone linią** (`polyline_outlined`) | jw. | jw. | — |
| A4 | **Własna ikona: dwie kropki i kręta droga** | kształt `conversion_path` z Material Symbols, rysowany w aplikacji | jw. | zapis prototypu (*Open* 1a) |
| W1 | **„Od” w środku** | linia od środka na zewnątrz; karta „Od” (przy „Ja” — „to ja”) | — | D5 („ode mnie”) |
| W2 | **„Do” w środku** | „Do” w środku jak po dotknięciu; karta „Do” z nazwą pokrewieństwa | „Pokaż ›” w karcie → widok „Do” | element 4 (dotknięcie osoby) · D6 |
| F1 | **Widok jedzie za linią** | gdy ścieżka się nie mieści: skala poziomu, widok przesuwa się razem z linią i staje na „Do” | — | — |
| F2 | **Drzewo maleje, aż ścieżka się zmieści** | cała ścieżka naraz, reszta osób jako małe kropki | — | AC-2 („ustawia ścieżkę w kadrze”) |
| O1 | **„Od” zawsze Ty** | kafel „Od” bez wyboru | — | — |
| O2 | **Dwie linie, bez odmiany imion** | „Piotr Przykładowy → Zofia Wymyślona” / „Wnuczka” | — | imiona w mianowniku, jak w notatkach |
| O3 | **Jedno zdanie, imię w dopełniaczu** | „Wnuczka Piotra” | — | — |
| Y1 | **Ścieżka przestawia na „dziś”** | suwak „dziś”, ▶ stoi, cała ścieżka z imionami | — | — |
| Y2 | **Rok zostaje** | osoby ścieżki nieurodzone w tym roku — pusty pierścień (C1), bez imion; linia przez puste miejsca | — | C1 (D33) |

**Pomiar** (makieta, `#test=1`, ekran 360 dp, „Ja” = Mateusz, 2026-10-14):

| Co | Tekst 100% | Tekst 200% |
|---|---|---|
| ścieżka od „Ja” | do 105 osób rodziny; Teofil (osoba bez rodziny, dołożona w makiecie ISSUE-038) — bez ścieżki | jw. |
| kroki ścieżki | 1 — 7 · 2 — 17 · 3 — 41 · 4 — 33 · 5 — 7 (najdłuższa: 3,5 s linii) | jw. |
| poziom ścieżki — W2 | 1 — 5 · 2 — 13 · 3 — 39 · 4 — 39 · „4 + osoby ścieżki” — 9 | jw. |
| poziom ścieżki — W1 | 1 — 5 · 2 — 14 · 3 — 46 · 4 — 33 · „4 +” — 7 | jw. |
| ścieżka nie mieści się w skali swojego poziomu — W2 · W1 | 25 · 55 | 96 · 98 |
| … nawet przy najmniejszej skali 0,4 — W2 · W1 | 10 · 37 | 67 · 73 |
| F2: najmniejsza skala, przy której cała ścieżka się mieści (W2) | 0,34 (okrąg 15 dp) | 0,17 (okrąg 7 dp) |
| wszystkie pary ze 107 osób makiety (11 342): bez ścieżki · „4 +” przy W2 · najdłuższa | 212 (z Teofilem) · 6681 (60% par ze ścieżką) · 9 kroków | — |
| Ja → Wanda (W2): poziom · skala · imiona ścieżki schowane | 3 · 0,85 · 0 z 4 | 3 · 0,31 · 1 z 4 |
| okno 7 | 328 × 253 dp, kafle 132 × 131 dp | 328 × 458 dp, kafle jeden pod drugim (296 dp) |
| baner: „Od” = Ty · O2 · O3 · bez ścieżki (linie) | 1 · 2 · 1 · 2 | do 2 · do 4 · do 2 · 4 |

**Odmiana imion w O3** (proste reguły, jak musiałaby je mieć aplikacja): wszystkie imiona wymyślonej rodziny poprawnie, ale 5 z 10 trudnych źle — „Ania” → „Anii” (Ani), „Hania” → „Hanii” (Hani),
„Maciek” → „Macika” (Maćka), „Wiesiek” → „Wiesika” (Wieśka), „Lew” → „Lewa” (Lwa); dobrze: Aniela, Rozalia, Bartłomiej, Wincenty, Józefa. Zdrobnienia i rzadkie imiona to właśnie to, co
bywa w notatkach rodziny.

**Rekomendacja: A1, W2, F2, O2, Y1.**
- **A1:** ten sam znak dla tej samej rzeczy — w widoku osoby `link` stoi nad łańcuchem „Jak łączy się ze mną”, a ścieżka na drzewie to ten łańcuch narysowany; bez rysunku do utrzymania.
  A2 w aplikacji z mapą i pinezkami czyta się jak „trasa do grobu”, A3 to najmniej znany znak, A4 to własny rysunek. **Nie da:** znaku, którego nikt nie pomyli z „linkiem” z innych
  aplikacji — dlatego `tooltip` i czytnik mówią „Połącz dwie osoby”.
- **W2:** pytasz o „Do”, więc „Do” staje w środku jak po dotknięciu, karta trzyma nazwę po zniknięciu baneru, a „Pokaż ›” prowadzi do tej osoby. Przy W1 karta mówi „to ja”. W pomiarze przy
  W2 ścieżka nie mieści się w skali poziomu 25 razy, przy W1 — 55. **Nie da:** linii „od środka na zewnątrz” — biegnie do środka.
- **F2:** zostaje przy brzmieniu AC-2 („ustawia ścieżkę w kadrze”) — przy 100% najmniej 0,34, a imiona ze ścieżki są czytelne, bo przy oddalaniu nie maleją (I2). F1 pokazuje ścieżkę po
  kawałku i co 0,7 s przesuwa całe drzewo; zmienia AC-2. **Nie da:** czytelnych osób spoza ścieżki przy długiej ścieżce (kropki), a przy tekście 200% — każdego imienia ze ścieżki (1 z 4 w
  przykładzie). Po końcu podświetlenia skala wraca do 0,4.
- **O2:** imiona zostają w mianowniku, więc nic się nie odmienia. O3 wymaga odmiany, a proste reguły mylą się na zdrobnieniach (tabela wyżej) — błąd w imieniu babci zobaczy cała rodzina.
  O1 zmienia AC-1 i zabiera pytanie „kim jest X dla Y”, np. przy wnukach. **Nie da:** najkrótszego baneru — przy 200% do 4 linii.
- **Y1:** pokrewieństwo nie zależy od roku; przy Y2 linia biegnie przez puste pierścienie bez imion (zrzut `09`). **Zmienia D37** dla jednego wejścia (jak wejście z paska). **Nie da:**
  powrotu do roku sprzed ścieżki.

## Decisions
- **D1 — drzewo od osoby z przestawianiem środka** (SPIKE-004 D20; kandydat 3 ze SPIKE-002). Na telefonie całe drzewo
  ok. 100 osób jest za szerokie; od osoby widać to, o co się pyta. *Obali:* SPIKE-002 pokaże, że cały widok jest czytelny
  i potrzebny — wtedy dodatkowy tryb „całe drzewo”. **v1.3:** potwierdzone na stopie #1 SPIKE-002 (2026-10-13, *„Tak”*) — K1 nie
  wchodzi do MVP.
- **D2 — poziomy połączeń według „rodziny każdej osoby”** (D20). Autor: *„poziom 1 to nasi partnerzy, dzieci i
  rodzice, poziom 2 to rodzeństwo partnerów, nasze rodzeństwo, rodzice rodziców, itd”*. Reguła z elementu 3 daje
  dokładnie te osoby. *Obali:* autor chce rodzeństwo już na poziomie 1.
- **D3 — kolory linii według rodzaju relacji + styl** (D20). Autor: *„chciałbym aby linie były odpowiednich kolorów
  (dziecko-rodzic, partnerzy)”*. Trzeci rodzaj (rodzic przybrany / adopcja) — *Open*.
- **D4 — czas pokazuje narodziny i związki, nie tylko zgony** (D20). Autor: *„jeżeli ktoś się rodzi to dopiero ma się
  pojawić w tym drzewie, albo gdy jest ślub to się łączą”*. Związek ma dwie daty: początek („razem”) i ślub
  ([[rodzina]] v1.4) — *„czasami ludzie nie są małżeństwem, mają dziecko, i dopiero biorą ślub”*.
- **D5 — animacja ścieżki od osoby do osoby, na drzewie** (D21, D26). Autor: *„odemnie leci linia do żony, potem do jej
  mamy…”*. Rytm ok. 0,7 s na krok („powoli”); przy włączonym w systemie ograniczeniu animacji — od razu cała ścieżka
  (SC 2.3.3).

- **D6 — ścieżka na drzewie, opis pokrewieństwa w banerze** (v1.1, SPIKE-004 D26). Autor chce widzieć ścieżkę na tym
  samym drzewie, a nie w osobnym układzie, i jedną informację: kim ta osoba jest dla niego. **Opis składa się z
  odcinków** nazwanych pojedynczo i połączonych w dopełniaczu: „siostra cioteczna” · „babci” · „mojej żony” →
  „Siostra cioteczna babci mojej żony”. Pojedyncze nazwy (z płcią i stroną) daje [[osoba]] D4; formy dopełniacza i podział
  na odcinki — słownik w pozycji, która to zbuduje, ze źródłem (kanon polskiej terminologii pokrewieństwa).
  **Od 2026-10-09 słownik nazw złożonych żyje tutaj** (decyzja autora na stopie #1 [[ISSUE-024-person-view]]: *„przypadki np.
  Brat stryjeczny prababki lub podobne zrobimy w widoku drzewa przy łączeniu różnych osób”*): kanon i tabela nazw —
  [[ISSUE-025-gender-kinship-together-since]] → *Prior art* i D2 (ciotka, stryj, wuj, rodzeństwo cioteczne, stryjeczne i
  wujeczne, bratanek, siostrzeniec, teściowie, zięć, synowa, bratowa, szwagier, opis z odcinków, odcinki neutralne), a z nimi
  **dawne AC-6 ISSUE-024** (*Given ścieżka Ja → tata → jego rodzic → jego córka Then „ciotka”; brat ojca — „stryj”, brat matki
  — „wuj”; dziecko siostry ojca — „brat/siostra cioteczna”*). Widok osoby pokazuje łańcuch z relacjami jednego kroku
  ([[osoba]] D13'); ścieżkę (`kinship.dart`) buduje ISSUE-024 i drzewo jej użyje.
- **D7 — przybliżanie i oddalanie** (v1.1, D25). Gesty jak na mapie (szczypanie, przeciąganie, podwójne dotknięcie),
  z alternatywą jednym dotknięciem ([[style-b]] *Thresholds* → gesty).
- **D8 — prior art: rodzina to krata, a nie drzewo, więc pokazuje się wycinek według zainteresowania** (v1.2, SPIKE-002).
  TimeNets (Kim, Card, Heer, AVI 2010; [PDF](https://homes.cs.washington.edu/~jheer/files/genvis.pdf)): *„Families are lattices of
  relationships, not trees”*, a wykresy przodków, potomków i klepsydra *„assume a hierarchical structure that does not fit
  real-world families”*; *„Visualizing the whole lattice structure is not realistic; it is reasonable to instead find
  sub-structures”*. Ich odpowiedzią jest **stopień zainteresowania (DOI)**: wartość maleje z odległością od osoby w środku, przy czym
  *„across conjugal relations, DOI values decrease more slowly”*, a widać tylko osoby powyżej progu. To jest reguła poziomów z D2
  (partner już na poziomie 1). Ukryte zostawia ślad (*„information scent”*), stąd D9. Drzewa podwójne McGuffina i Balakrishnana
  (InfoVis 2005, [doi:10.1109/INFVIS.2005.1532124](https://doi.org/10.1109/INFVIS.2005.1532124); opis w TimeNets) uogólniają klepsydrę
  na dwie osoby, np. mnie i żonę, ale i tam *„only a limited number of nodes are shown”*, z rozwijaniem i zwijaniem. **Produkt
  mobilny:** w aplikacji FamilySearch jest wachlarz przodków, a widok poziomy i widok potomków są tylko na stronie
  ([pomoc FamilySearch](https://www.familysearch.org/en/help/helpcenter/article/what-are-the-different-pedigree-views-in-family-tree)).
  Ścieżka pokrewieństwa to tam wykres z nazwą u góry, np. „My Grandmother”
  ([pomoc](https://www.familysearch.org/en/help/helpcenter/article/what-is-view-my-relationship-in-family-tree)), tak jak baner D6.
  **Tło dla kryterium < 30 s:** w badaniu TimeNets pytania o strukturę rodziny 36 osób (obraz 600 × 600 px na komputerze) zajmowały
  na zwykłym drzewie medianę 17,1 s. *Obali:* źródło, które pokazuje pełny graf rodziny z powinowatymi czytelnie na małym ekranie.
- **D9 — ślad dalszej rodziny** (v1.2, przyjęta na stopie #1 SPIKE-002, 2026-10-13; D8 → *„information scent”*). Osoba, która ma
  rodzinę poza widokiem, dostaje krótką kreskę (14 dp, przerywana 3/3) w kolorze relacji o kryciu 60%: w górę — rodzice, w dół —
  dzieci, w bok — partner. Krycie 60% daje 3,75:1 (rodzic–dziecko; przeliczone 2026-10-13 z kolorem po zaokrągleniu kanałów, wcześniej 3,76:1) i 3,66:1 (partnerzy) na tle, czyli ≥ 3:1 (SC 1.4.11), a przerywany
  kształt odróżnia ślad od prawdziwej linii nie tylko kolorem (SC 1.4.1). Po co: widać, gdzie drzewo idzie dalej, zanim się tam dotknie.
  *Obali:* autor uzna kreski za szum albo pomyli je z linią „razem”.
- **D10 — imię pod węzłem 13 sp** (v1.2). Jak w mini-drzewie ([[osoba]] element 6), bo v1 miało 12 sp bez wyjątku w [[style-b]] (tekst
  pomocniczy ≥ 13 sp). Pomiar wyżej nie zależy od tej różnicy. *Obali:* wyjątek w [[style-b]] z powodem, jak przy podpisie zakładki.
- **D11 — tryb prezentacji na telewizor** (v1.3, decyzja autora na stopie #1 SPIKE-002, 2026-10-13: *„Tak”*; dawne *Open* 2).
  **(a)** systemowe „Przesyłaj ekran” Androida — obraz telefonu na telewizorze, bez kodu; **(b)** tryb prezentacji w aplikacji: poziomo,
  pełny ekran, bez przycisków, **poziom 2** dopasowany do ekranu (przy poziomie 3 osoby na ekranie 16:9 są za małe — makieta v1.2).
  **Bez Google Cast:** odbiornik na telewizorze to kod sieciowy i dane rodziny w sieci lokalnej ([[NFR-005-dane-nie-opuszczaja-telefonu]]).
  Buduje to pozycja drzewa, nie spike. **Nie da:** obrazu na telewizorze bez telefonu w ręce. *Obali:* „Przesyłaj ekran” nie działa z
  telewizorem autora.
- **D12 — opis z odcinków liczony od drugiej osoby** (v1.5, AC-5). [[ISSUE-025-gender-kinship-together-since]] D2 mówi: „najdłuższy znany
  odcinek od „ja”, potem następny”. Dla przykładu z AC-5 (żona → jej mama → jej mama → jej rodzic → jego rodzeństwo → jego dziecko) ta reguła
  daje „Siostrzenica babci Twojej teściowej”, bo „teściowa” zabiera pierwszy odcinek. **Odcinki od drugiej osoby:** najpierw najdłuższy znany
  odcinek, który kończy się na niej, potem następny w stronę „Ja”. Wychodzi „Siostra cioteczna babci Twojej żony”, tak jak w AC-5 i D6.
  Sprawdzone w makiecie na 22 osobach (sekcja 2), np. tata → dziadek → pradziadek → jego siostra → jej córka daje „Siostra cioteczna Twojego
  dziadka”. Słownik i nawiasy bez zmian (ISSUE-025 D2). Dopełniacz każdej nazwy — tabela w pozycji, z testami. *Obali:* opis, który autor
  mówi inaczej, np. „Wnuk Twojej ciotki” tam, gdzie powiedziałby „Syn Twojej siostry ciotecznej”. **v1.7:** rzadsze formy dopełniacza
  (szwagra, siostrzeńca, zięcia, teścia, wuja) sprawdzone w Wikisłowniku (tabele odmiany), a nie w SJP PWN, jak mówił plan — odstępstwo 7
  [[ISSUE-033-tree-from-a-person]]; formy zgodne z odmianą wzorcową, reszta to odmiana regularna z testami `qa`.
- **D13 — nawias w karcie** (v1.5). Przy pojedynczej nazwie karta pokazuje nawias ze słownika ([[ISSUE-025-gender-kinship-together-since]] D2,
  kolumna „Nawias w liście”): „Twoja ciotka (siostra taty)”, „Twój wuj (brat mamy)”. Lista osób nie pokazuje już pokrewieństwa ([[osoby]] v2.2),
  więc karta drzewa jest pierwszym miejscem, gdzie nawias jest potrzebny: „ciotka” i „wuj” nie mówią, z której strony (SJPD, za Szymczakiem —
  ISSUE-025 → *Prior art*). Opis z odcinków nie ma nawiasu, bo sam pokazuje drogę. *Obali:* autor uzna nawias za zbędny — wtedy sama nazwa
  (AC-5 mówi tylko „ciotka”).
- **D14 — „ja” w drzewie ze znakiem „Ja”** (v1.5). Jak w [[osoby]] D4 i w łańcuchu [[osoba]] 7: okrąg z „Ja” w akcencie (także przy profilowym)
  i podpis „Ja”. Obrys zostaje w kolorze obrysu, bo pierścień w akcencie znaczy „osoba w środku” — dwa bursztynowe pierścienie myliłyby, gdzie
  jest środek. Po co: po kilku przestawieniach widać, gdzie jesteś. *Obali:* autor woli w węźle swoje zdjęcie.
- **D15 — zakładka zawsze od „Ja”, a „Pokaż w drzewie” przełącza zakładkę** (v1.5, AC-1, AC-6). Wejście z paska zaczyna od „Ja” na poziomie 2.
  Drzewo nie pamięta poprzedniego środka, a wstecz nie cofa środka — działa jak w [[style-b]] reguła 12. „Pokaż w drzewie” przechodzi na
  zakładkę Drzewo (pasek pokazuje, gdzie jesteś), a nie kładzie drzewa na widoku osoby w innej zakładce. Do siebie wracasz przez węzeł „Ja”
  (D14) albo ponowne wejście w zakładkę. **Nie da:** powrotu wstecz do osoby, z której się przyszło. *Obali:* autor gubi się po kilku
  przestawieniach albo szuka drogi wstecz do osoby — wtedy wstecz cofa środek. **v1.7** (odstępstwo 6 [[ISSUE-033-tree-from-a-person]]):
  „Pokaż w drzewie” zaczyna drzewo od nowa także z widoku osoby otwartego z drzewa — stos drzewa znika. Wynik jest ten sam co powrót do
  drzewa i przestawienie środka (ta osoba w środku, poziom 2), a droga jedna zamiast dwóch.
- **D16 — tryb prezentacji: wejście, wyjście, stały poziom** (v1.5, AC-8, D11). Wejście — ikona telewizora w pasku (`tv_outlined`; istnieje we
  Flutterze 3.41.1, sprawdzone w SDK 2026-10-13). Na ekranie nie ma przycisków, więc wyjście daje dotknięcie pustego miejsca (na 3 s „Zakończ
  prezentację”) albo wstecz. **Poziom 2 stały:** oddalanie zmieniałoby skład osób na ekranie, który ogląda rodzina, a + / − tu nie ma.
  Dotknięcie osoby wystarczy, żeby przejść po rodzinie. Podpowiedź o „Przesyłaj ekran” pojawia się przy każdym wejściu, bo sam tryb niczego
  nie wysyła. Po co: rodzina patrzy na telewizor, a osoba z telefonem prowadzi. *Obali:* autor chce oddalać na telewizorze — wtedy szczypanie
  jak w drzewie. **v1.8** ([[ISSUE-034-tree-presentation-mode]]): podpowiedź mówi o funkcji, a nie o nazwie kafelka (D26). Przy pierwszym pełnym
  ekranie aplikacji system raz pokazuje własne okno o tym, jak wyjść z pełnego ekranu. To okno systemu, nie aplikacji. Jeśli przesyłanie już trwa,
  zobaczy je też telewizor, więc przed pierwszym pokazem warto raz wejść w tryb bez przesyłania. **v1.10** ([[ISSUE-036-cast-from-the-app]], D30):
  wejście przez ekran przesyłania systemu, a podpowiedź tylko na telefonie bez tego ekranu. Wejście bez przesyłania to ekran systemu i wstecz.
- **D17 — cel dotyku przy oddaleniu poniżej 48 dp** (v1.5). Cel to miejsce osoby × skala drzewa. Przy skali ≥ 0,6 ma ≥ 48 dp (prawie cały
  poziom 3; od 0,55 — 44 dp). Na poziomie 4 ma 38 dp przy 0,48 i 32 dp przy najmniejszej skali 0,4. Węzły nie mogą rosnąć, bo wtedy drzewo
  przestałoby być oddalone. Najmniejsza skala 0,4 trzyma cel ≥ 24 dp — [WCAG 2.2](https://www.w3.org/TR/WCAG22/) SC 2.5.8 Target Size
  (Minimum), AA: *„The size of the target for pointer inputs is at least 24 by 24 CSS pixels”*. Do tego przybliżenie (+) daje cel ≥ 48 dp
  jednym dotknięciem — wyjątek *Equivalent*: *„The function can be achieved through a different control on the same page that meets this
  criterion”*. Pomyłka kosztuje mało: dotknięcie złej osoby tylko przestawia środek. Wyjątek zapisany w [[style-b]] *Thresholds* (v1.24).
  *Obali:* na telefonie autor trafia w złą osobę na poziomie 4 — wtedy najmniejsza skala 0,6.
- **D18 — wartości S2 z prototypu** (v1.5). Progi 1,3 · 0,85 · 0,55 i krok 1,45 wybrał `dev` w prototypie SPIKE-002 (*Dev report* →
  *Deviations* 1). Autor przeszedł na nich oddalanie i powrót („ok” na stopie #2, krok 1). Zakres skali 0,4–2,0: dolna granica z D17, a górna
  daje imię 26 sp — większe nie pokazuje nic nowego. *Obali:* progi w ręce, przy szczypaniu na telefonie ([[ISSUE-032-mvp-install]] →
  *Hand checks*, wiersz ze SPIKE-002).
- **D19 — stany bez „ja” i pustej bazy** (v1.5). Drzewo zaczyna się od „Ja” (AC-1), więc bez „ja” nie ma od czego zacząć. Zdanie i działanie
  są jak w [[osoba]] element 7 („Aplikacja nie wie jeszcze, która osoba to Ty.” · „Wybierz, która osoba to Ty”), a po wyborze widać drzewo od
  tej osoby. Nie zaczynamy od przypadkowej osoby, bo karta nie umiałaby powiedzieć, kim ktoś jest dla Ciebie. Przy pustej bazie — zdanie jak w
  [[osoby]], bez działania, bo osoby dodaje się przy grobie (reguła 9: jedno działanie, gdy jest). *Obali:* autor chce drzewa bez wyboru „ja”
  — wtedy start od ostatnio oglądanej osoby.
- **D20 — tekst 200% w karcie** (v1.5, AC-7; SPIKE-002 M4: karta i pasek zajmowały pół ekranu). Przy tekście systemu ≥ 150% „Pokaż ›”
  przechodzi pod tekst, do prawej, więc imię i pokrewieństwo mają całą szerokość karty i się nie ucinają. Przy 200% karta i tak zajmuje ok.
  40% wysokości: treść jest ważniejsza niż kadr drzewa, a drzewo przesuwa się palcem. Przyciski + / − nie rosną (ikony, 48 dp) i mogą przykryć
  węzeł — przesunięcie go odsłania. *Obali:* przy 200% drzewo jest za niskie, żeby się po nim poruszać — wtedy karta zwija się do jednej linii.
- **D21 — drzewo nie ucieka z kadru** (v1.7, odstępstwa 2 i 3 `dev` w [[ISSUE-033-tree-from-a-person]], przyjęte w przeglądzie `ui`). Gdy po
  przesunięciu albo zmianie skali w kadrze nie ma nikogo, widok po chwili spokoju (ok. 0,4 s) wraca płynnie (0,35 s) do osoby w środku, przy
  tej samej skali i poziomie. Palec na ekranie przerywa powrót, a przy ograniczeniu animacji powrót jest od razu (SC 2.3.3). Nowy rozmiar
  obszaru drzewa **przed pierwszym dotknięciem** (klawiatura zamykana po wyborze „ja”, obrót) ustawia środek od nowa. Po co: wstecz nie cofa
  środka (D15), a zakładka na swoim ekranie nic nie robi ([[style-b]] reguła 12), więc bez tego drzewo dało się zgubić na emulatorze po kilku
  przesunięciach. **Nie da:** oglądania pustej płaszczyzny poza drzewem — nic tam nie ma. *Obali:* autor odczuje powrót jako szarpnięcie przy
  szybkim przesuwaniu — wtedy zamiast powrotu granica przesuwania wokół drzewa.
- **D22 — kto jest zmarły** (v1.7, odstępstwo 4). Znicz dostaje osoba z zapisanym **zgonem albo pochówkiem**, z datą albo bez. Element 4 mówił
  „zmarły ma znicz”, ale nie mówił, skąd to wiadomo, a pole `is_living` w bazie ma wartość domyślną i nic nie znaczy. Zdarzenie zgonu albo
  pochówku to fakt wpisany przez autora. Bez nich osoby nie oznaczamy, nawet urodzonej dawno: aplikacja nie zgaduje śmierci z wieku.
  *Obali:* autor chce znicza przy osobie bez wpisanego zgonu ani pochówku, o której wie, że nie żyje — wtedy osobne pole w formularzu osoby.
- **D23 — imię na tabliczce w kolorze tła** (v1.7, odstępstwo 1; [[style-b]] reguła 13, v1.26). I2 (v1.6) mówiło „obwódka w kolorze tła”, jak
  podpisy miast. Na emulatorze ok. 100 rozmytych cieni pod imionami w każdej klatce ruchu szarpało przejścia między poziomami na wątku
  rasteryzacji ([[ISSUE-033-tree-from-a-person]] → *Dev report* → *Found on the emulator*, a). **Tabliczka:** prostokąt w kolorze tła,
  zaokrąglony 4 dp, 3 dp z boków imienia. Tło drzewa jest jednolite, więc tabliczka wygląda jak obwódka i tak samo przerywa linie pod imieniem.
  Okrąg maluje się nad tabliczką, żeby nie ucinała poświaty osoby w środku. Imię na tabliczce to tekst na tle, 10,98:1. **Nie da:** obwódki
  dopasowanej do liter — linia jest przerwana na całej szerokości imienia. *Obali:* pod węzłami pojawi się tło niejednolite (zdjęcie, pasmo
  czasu z US-010) — tam tabliczka byłaby widoczna jako prostokąt; wtedy obwódka liter jak na mapie.
- **D24 — imię ucięte w miejscu osoby także przy 100%** (v1.7, odstępstwo 5). Element 4 od v1.5 mówi: „…” dopiero poza miejscem osoby. Przy
  tekście 100% to ok. 10 liter (np. „Bronisła…”), tak samo przy oddaleniu (I2: imię na ekranie ma tę samą szerokość co w skali 1) i w
  mini-drzewie ([[osoba]] v2.2). Pełne imię i nazwisko daje karta (5) i czytnik. Przy 200% miejsce osoby rośnie do 160 dp i imiona mieszczą się
  w całości (AC-7). *Obali:* autor myli osoby po uciętym imieniu (np. Bronisław i Bronisława) — wtedy przy skali < 1 imię może sięgać szerzej
  niż miejsce osoby, bo I2 i tak chowa nakładające się.
- **D25 — tryb prezentacji: dotyk** (v1.8, odstępstwa 1–3 `dev` w [[ISSUE-034-tree-presentation-mode]], przyjęte w przeglądzie `ui`).
  **(a) Osoba w środku:** dotknięcie dopasowuje poziom 2 od nowa, płynnie, jak powrót drzewa do kadru (D21). Plan ISSUE-034 (D5) mówił „nic”, ale
  element 11 mówi „dotknięcie osoby → … poziom 2 dopasowany na nowo”, a po przeciągnięciu to jedyna droga z powrotem bez wychodzenia z trybu.
  Widok osoby się nie otwiera, bo w pionie przerwałby pokaz, a czytnik nie mówi „otwórz”. **(b) Pasy przy krawędziach:** w trybie pełnego ekranu
  przeciągnięcie od krawędzi, które wysuwa paski systemu, trafia też do aplikacji i przesuwało drzewo (Flutter 3.41.1, `services/system_chrome.dart`,
  `SystemUiMode.immersiveSticky`: *„A swipe gesture from the edge of the screen displays overlays. In contrast to [SystemUiMode.immersive], this
  gesture is received by the application”* — sprawdzone w SDK 2026-10-14). Pas 24 dp przy takiej krawędzi nie przyjmuje dotyku. Dopasowany poziom
  i tak trzyma 24 dp od krawędzi (element 11). Zbudowane przy górze i dole; przy nawigacji trzema przyciskami pasek w poziomie stoi z boku — tam
  też (przegląd v1.8, do sprawdzenia na emulatorze).
  **(c) „Zakończ prezentację” chowa podpowiedź**, gdy pusty dotyk przyjdzie w ciągu jej 4 s: kto szuka wyjścia, podpowiedź już widział, a przy
  tekście 200% oba stałyby w tym samym miejscu. **Nie da:** dotknięcia osoby pod pasem po przeciągnięciu — trzeba ją odsunąć od krawędzi.
  *Obali:* autor na telefonie trafia w pas, chcąc dotknąć osoby — wtedy węższy pas albo pas tylko przy krawędzi paska nawigacji.
- **D26 — tryb prezentacji: podpowiedź** (v1.8, odstępstwa 4 i 6). **Tekst mówi o funkcji, a nie o nazwie kafelka:** „Obraz na telewizor:
  przesyłanie ekranu w szybkich ustawieniach telefonu”. Nazwa kafelka zależy od producenta: na Pixelu (Android 16, po polsku) to „Przesyłanie”
  (`quick_settings_cast_title` w zasobach SystemUI emulatora — *Dev report* ISSUE-034), u Samsunga „Smart View”, a v1.5 cytowała „Przesyłaj
  ekran”, którego nie ma na żadnym sprawdzonym telefonie. Nazwa w cudzysłowie obiecuje napis, którego użytkownik może nie znaleźć; opis funkcji
  pasuje do każdego. **Miejsce:** u góry, jak pigułka poziomu (element 3), na 4 s; może przykryć górny rząd (zrzut `02` ISSUE-034), ale nie
  przyjmuje dotyku, więc dotknięcie trafia w osobę pod nią. Komunikat na chwilę nad treścią to zwykła forma podpowiedzi, a stałe miejsce na nią
  pomniejszyłoby drzewo na cały pokaz. *Obali:* na telefonie autora kafelek ma inną nazwę i autor go nie znajduje — wtedy w podpowiedzi nazwa z
  jego telefonu, w cudzysłowie ([[ISSUE-032-mvp-install]] → *Hand checks*).
- **D27 — imiona przy oddalaniu: zostaje I2** (v1.9, [[ISSUE-035-tree-names-shrink-my-voice]]). Droga tej decyzji: **I2** na stopie #1
  [[ISSUE-033-tree-from-a-person]] (2026-10-13, „Tak” — najpewniej bez makiety) → **I1** na stopie #1 [[ISSUE-034-tree-presentation-mode]] (2026-10-14,
  *„1 — I1”*, pierwszy raz z makietą) → **I2** na stopie #1 ISSUE-035 (2026-10-14, *„1 I2”*). Przed tym stopem `ui` rozpisał I1 w elementach 4 i 11 i w
  [[style-b]] (wyjątek od 13 sp), a makieta i plan opisały koszt I1 wprost: *„na poziomie 4 widać tylko kreski”*. Autor wybrał I2 po obejrzeniu
  sekcji 1 makiety. Zapis I1 cofnięty przed budową, kod bez zmian. **Skutek, który zostaje:** w trybie prezentacji przy tekście 200% na 360 dp widać
  13 z 20 imion, a tabliczki zasłaniają linie między rzędami (element 11, zrzut `18b` ISSUE-034). Przy I1 byłoby 20 z 20. *Obali:* na telefonie albo
  na telewizorze autor chce widzieć wszystkie imiona przy oddaleniu ([[ISSUE-032-mvp-install]] → *Hand checks*). Wtedy I1 albo I1 + I2 od progu
  (dolna granica imienia z chowaniem poniżej niej).
- **D28 — kto mówi: nazwa pokrewieństwa Twoim głosem, zdania aplikacji do Ciebie (G2)** (v1.9, [[ISSUE-035-tree-names-shrink-my-voice]]; decyzja
  autora na stopie #1 [[ISSUE-034-tree-presentation-mode]], 2026-10-14: *„2 — Moja babcia”*). Zastępuje G1 z v1.6. **Reguła** ([[style-b]] reguła 7,
  v1.28): nazwa tego, kim ktoś jest dla mnie, to etykieta z mojego punktu widzenia, więc mówi „mój”: „Moja babcia”, „Siostra cioteczna babci mojej
  żony”, „to ja”, „nie wiadomo jeszcze, kim jest dla mnie”. Zdanie, w którym aplikacja coś mówi, o coś pyta albo do czegoś zaprasza, zostaje w
  drugiej osobie: „Wybierz, która osoba to Ty”, „Która osoba to Ty?”, „Aplikacja nie wie jeszcze, która osoba to Ty.”. Nagłówek „Jak łączy się ze mną”
  ([[osoba]] 7) to już pytanie zadane Twoim głosem, a odpowiedź aplikacji pod nim („Nie wiadomo jeszcze, jak łączy się z Tobą — …”) jest zdaniem do
  Ciebie. Obie zostają. **Prior art:** [Microsoft Writing Style Guide → Person](https://learn.microsoft.com/en-us/style-guide/grammar/person) (odczyt
  2026-10-14): *„In general, use second-person pronouns (you, your)”*, ale *„First-person singular pronouns can be used in product UI to show
  someone's control”* oraz *„it's OK to use "my" in navigation or filter labels if you need to distinguish a person's content”*. W genealogii
  FamilySearch nazywa pokrewieństwo w pierwszej osobie, np. „My Grandmother” (D8). **Zakres G2:** karta (5), opis dla czytnika (4) i baner „Połącz
  dwie osoby” (9, US-011; od v1.1 mówi „mojej żony”) — wszystkie biorą ten sam tekst nazwy. **Poza zakresem:** inne zdania aplikacji, np. „Twoje
  cmentarze” i „wraca do Twojej pozycji”, bo aplikacja mówi tam do Ciebie, oraz [[osoba]] (mini-drzewo i łańcuch 7 mówią relację jednego kroku bez zaimka do Ciebie, np. „Jej mama Maria” —
  D13'). Wielka litera tylko
  na początku nazwy („Moja babcia”), w środku opisu mała („…mojej żony”). Wielkie „Twoja” w G1 było grzecznościowe, a „mój” wielkiej litery nie bierze.
  Przykłady w D12, D13 i *Open* 6 są zapisane w G1, czyli sprzed v1.9, a dziś obowiązuje G2. Makieta pokazała autorowi G2 z „to ja” i „dla mnie”
  (`cardSub` w `drzewo-us009.html`), więc pytanie (a) z ISSUE-035 rozstrzyga sama makieta. **Nie da:** jednego głosu w całej aplikacji — są dwa, każdy
  ze swoją rolą. *Obali:* autor uzna, że zdania aplikacji obok „Moja babcia” brzmią obco (np. „Wybierz, która osoba to Ty” nad kartą „to ja”). Wtedy
  osobna pozycja na zdania aplikacji w pierwszej osobie („Wybierz, która osoba to ja”).
- **D29 — co aplikacja bez Google Cast może otworzyć** (v1.10, [[ISSUE-036-cast-from-the-app]]; prior art przed wyborem wejścia). **Źródła:**
  - `Settings.ACTION_CAST_SETTINGS` (źródła SDK Androida 36, `android/provider/Settings.java`, odczyt 2026-10-14): *„Activity Action: Show settings to allow
    configuration of cast endpoints. In some cases, a matching Activity may not exist, so ensure you safeguard against this.”* To jedyne publiczne wejście, stąd
    ISSUE-036 AC-2;
  - przesyłanie ekranu włącza system: typ trasy „remote display” w `android/media/MediaRouter.java` jest `@hide`, a stan przesyłania synchronizują *„System UI
    and Settings”* z uprawnieniem systemowym `CONFIGURE_WIFI_DISPLAY`. Aplikacja nie otworzy więc okienka z szybkich ustawień ani nie zacznie przesyłania sama;
  - [pomoc Google → Cast your Android screen](https://support.google.com/chromecast/answer/6059461) (odczyt 2026-10-14): przesyłanie ekranu na urządzenie Google
    Cast działa od Androida 8.0; druga droga to aplikacja Google Home („Cast my screen”, „Cast one app”);
  - Android 15 pozwala przesyłać jedną aplikację zamiast całego ekranu, a po wyjściu z niej telewizor jest czarny
    ([Android Authority](https://androidauthority.com/android-partial-screenshare-task-switcher-3488494)) — źródło wtórne.

  **Pomiar:** ekran z *Candidates — ISSUE-036*. **Wniosek:** przycisk otwiera ekran ustawień, a aplikacja **nie wie, czy przesyłanie ruszyło**. Dlatego po
  powrocie zawsze włącza tryb prezentacji (P2), a ikona nie zmienia się w `cast_connected`. **Nie da:** okienka z listą nad drzewem jak w Zdjęciach (to casting,
  po MVP — ISSUE-036 *Out of scope*) · pewności, że na telefonie autora po wyborze telewizora system nie zapyta jeszcze o zgodę albo o „cały ekran / jedna
  aplikacja” · pewności, że telefon innego producenta otworzy ekran z telewizorami Google Cast, a nie np. tylko Miracast. Wtedy podpowiedź się nie pokaże, bo
  ekran istnieje. Wszystkie trzy sprawdza telefon autora z jego telewizorem ([[ISSUE-032-mvp-install]] → *Hand checks*). *Obali:* na telefonie autora ekran
  systemu nie pokazuje jego telewizora, choć kafelek w szybkich ustawieniach go pokazuje. Wtedy przycisk otwiera tryb z podpowiedzią (stan z AC-2) zamiast
  ekranu systemu.
- **D30 — jedna ikona „Przesyłaj na telewizor” zamiast ikony telewizora (P2)** (v1.10, decyzja autora na stopie #1 [[ISSUE-036-cast-from-the-app]], 2026-10-14:
  *„tak”*; dawne *Open* 7). Ikona `cast_outlined` otwiera systemowy ekran przesyłania, a po powrocie włącza tryb prezentacji bez podpowiedzi. Telefon bez tego
  ekranu włącza od razu tryb z podpowiedzią D26. Powód: autor chciał, żeby przycisk telewizora wysyłał obraz (stop #2 [[ISSUE-034-tree-presentation-mode]]: *„jak
  w YouTube”*), a ikona przesyłania jest ta sama co w systemie i w YouTube (*Candidates — ISSUE-036*). **Nie da:** trybu bez telewizora jednym dotknięciem —
  ikona i wstecz. *Obali:* autor na telefonie często pokazuje drzewo poziomo bez telewizora — wtedy P1 (druga ikona `tv_outlined`).
  **v1.11** (przegląd `ui`, odstępstwa 1–2 `dev` w [[ISSUE-036-cast-from-the-app]]):
  **(a) Powrót = aplikacja znów ma fokus** (we Flutterze `inactive` → `resumed`), a nie „aplikacja była schowana” (`hidden` → `resumed`, plan D1). Pomiar `dev`
  na emulatorze: przy wstecz po ok. 1 s Android nie zdążył schować aplikacji, więc według planu tryb by się nie włączył. Flutter 3.41.1 (`dart:ui`,
  `AppLifecycleState.inactive`, odczyt 2026-10-14): na Androidzie aplikacja jest `inactive` m.in. *„when the app is partially obscured or another activity is
  focused, a app running in a split screen that isn't the current app”*. Ten sam sygnał obejmuje więc ekran przesyłania, który u innego producenta byłby oknem
  nad aplikacją i jej nie chował. **Skutki:** przy podzielonym ekranie tryb włączy się, gdy wrócisz palcem do Grobinga; Home z ekranu systemu i powrót do
  Grobinga pokazuje znowu ekran systemu (to samo zadanie), a tryb włącza dopiero wstecz, czyli „nie da” z planu D1 (z innej aplikacji prosto w tryb) jest
  łagodniejsze. **(b) Drugie dotknięcie** w czasie otwierania ekranu systemu nic nie robi, a ikona się nie zmienia. Wyszarzenie mignęłoby na ułamek sekundy,
  zanim ekran systemu przykryje drzewo, a po powrocie ikony i tak nie widać, bo jest tryb prezentacji. *Obali:* na telefonie autora ikona przestaje reagować,
  a tryb się nie włącza (czekanie bez końca) — wtedy koniec czekania po czasie i widoczny stan czekania.
- **D31 — prior art: brakujące daty szacuje się z rodziny, a niepewność się pokazuje** (v1.12, [[ISSUE-037-time-on-the-tree]]). TimeNets (Kim, Card, Heer, AVI 2010;
  [PDF](https://homes.cs.washington.edu/~jheer/files/genvis.pdf), odczyt 2026-10-14), *Missing Data Estimation*: *„We use a rule-based method to estimate missing
  dates”* — urodzenie z daty ślubu rodziców, średniej urodzeń rodzeństwa albo małżonka; ślub z urodzenia najstarszego dziecka; bez reguły — urodzenie przesunięte o ok. 20
  lat. *Uncertainty*: *„Without indications of uncertainty, visual analysis may lead to inaccurate conclusions”*; *„For uncertain birth and death dates, we fade lifelines
  using a gradient”*. Wcześniej Priestley (1765) oznaczał niepewne daty urodzenia i śmierci kropkami (opis w TimeNets). **Liczby okna z Gramps** (`gramps.gen.utils.alive`,
  [źródło](https://pythonhosted.org/Gramps/_modules/gramps/gen/utils/alive.html), odczyt 2026-10-14): średni odstęp pokoleń `AVG_GENERATION_GAP = 20`, różnica wieku
  rodzeństwa `MAX_SIB_AGE_DIFF = 20`, najwyższy wiek „prawdopodobnie żyje” `MAX_AGE_PROB_ALIVE = 110`. W Grobingu to tylko **granice okna**, w którym nie wiadomo, czy osoba
  żyje — śmierci z wieku aplikacja dalej nie zgaduje (D22: znicz tylko przy zapisanym zgonie albo pochówku). *Obali:* źródło z genealogii, które pokazuje daty niepewne
  na osi czasu inaczej i lepiej czytelnie na małym ekranie.
- **D32 — okno daty i przerywany obrys (N3)** (v1.12; *Candidates — ISSUE-037*; **rekomendacja — decyzja autora na stopie #1**). Każda data osoby ma okno
  [najwcześniej, na pewno]: dokładnie Y → [Y, Y]; „ok. Y” → [Y−5, Y+5] (±5 — decyzja projektowa: „ok.” w notatkach to zwykle zaokrąglenie); „między A a B” → [A, B];
  „przed Y” → [z rodziny, Y]; „po Y” → [Y, z rodziny]; brak → oba z rodziny. **Urodzenie z rodziny:** najwcześniej 20 lat po urodzeniu młodszego z rodziców, a bez rodziców
  — 20 lat przed najstarszym z partnerów i rodzeństwa, a bez nich — początek suwaka; na pewno — pierwsze datowane zdarzenie z własnego życia (związek, dziecko, śmierć,
  pochówek), a bez nich — 20 lat po najmłodszym z partnerów i rodzeństwa, a bez nich — „dziś”. **Śmierć bez daty** (jest zgon albo pochówek): od ostatniego datowanego
  zdarzenia z życia (urodzenie, związek, dziecko) do daty pochówku, a bez niej — do urodzenia + 110 lat (najpóźniej „dziś”). Związek bez daty — D31 (najstarsze dziecko). Na
  „dziś” okien nie ma: drzewo jest takie jak w US-009. *Obali:* na prawdziwych danych przerywanych obrysów jest tyle, że drzewo w przeszłości czyta się gorzej niż bez nich —
  wtedy węższe okno „ok.” albo N1.
- **D33 — osoba w środku przed narodzinami: pusty pierścień (C1)** (v1.12, rekomendacja). AC-1 mówi „miejsce zostaje, drzewo nie skacze”, więc środek się nie przestawia;
  pierścień mówi, od kogo czytasz drzewo. Karta zostaje (opisuje osobę, nie rok). Pierścień nie jest celem dotyku; „Pokaż ›” w karcie działa. *Obali:* autor szuka w latach
  przed sobą swojego okręgu i go nie znajduje — wtedy C2.
- **D34 — początek suwaka od najwcześniejszej daty (T2), stała prędkość** (v1.12, rekomendacja). Pełna dekada przed najwcześniejszą datą urodzenia w bazie (przy „ok.” —
  przed początkiem jej okna), najpóźniej 1880. ▶ biegnie stale ok. 21 lat na sekundę, czyli 1880 → dziś w ok. 7 s jak w AC-3. Przy T2 AC-3 brzmi „od początku suwaka”.
  *Obali:* najstarsza data w bazie to błąd wpisu (np. 1088) i suwak zaczyna się sto lat za wcześnie — wtedy dolna granica (np. 1800) albo T1.
- **D35 — koniec związku: „//” na linii pary (E3)** (v1.12, rekomendacja; **zmienia też drzewo na „dziś”**). Genogram: *„Marital separation is indicated by a single slash
  along the connecting line; a divorce is indicated by two slashes”* (ND CFS QA, *Case Review Genogram Resource*, rev. 11.22,
  [PDF](https://und.edu/cfstc/_files/docs/2023-qa-genogram-resource.pdf), odczyt 2026-10-14). Model ma jeden „koniec związku” (rozwód albo rozstanie — [[rodzina]] A6),
  więc jeden znak, ten od rozwodu. Owdowienie nie jest końcem związku (zgon osoby), więc linia wdowy zostaje bez kresek. *Obali:* „//” myli się z linią „razem” albo ze
  śladem dalszej rodziny przy oddaleniu — wtedy E1 i koniec tylko w widoku osoby.
- **D36 — ograniczenie animacji: dekadami co ok. 1 s (R2)** (v1.12, rekomendacja; AC-3). WCAG 2.2 SC 2.3.3 *Animation from Interactions* (poziom AAA, [w3.org](https://www.w3.org/TR/WCAG22/#animation-from-interactions),
  odczyt 2026-10-14) dotyczy animacji ruchu: *„Motion animation triggered by interaction can be disabled, unless the animation is essential to the functionality or the
  information being conveyed”*. Skok roku co sekundę i osoby pojawiające się od razu to zmiana stanu, nie ruch. Ten sam warunek
  wyłącza przenikanie osób (150 ms) i przesuwanie widoku przy zmianie środka (element 4). *Obali:* autor z włączonym „Usuń animacje” odbiera skoki jako miganie — wtedy R1.
- **D37 — rok a nawigacja** (v1.12, decyzje projektowe). Rok to stan widoku jak środek i skala: **zostaje** przy przestawieniu środka, zmianie poziomu i powrocie wstecz z
  widoku osoby; **„dziś”** przy każdym wejściu z paska i z „Pokaż w drzewie” (jak środek od „Ja”, D15) oraz w trybie prezentacji, który nie ma suwaka ani roku (element 11;
  suwak w trybie prezentacji — poza ISSUE-037). Dotknięcie osoby i oddalanie w czasie ▶ **nie zatrzymują** odtwarzania; przeciągnięcie suwaka — zatrzymuje. Pigułka poziomu
  i ślad dalszej rodziny liczą tylko osoby, które w tym roku już są — dziecko, które jeszcze się nie urodziło, nie jest „rodziną poza widokiem”. *Obali:* autor po powrocie z
  widoku osoby spodziewa się „dziś”. **v1.13** (przegląd `ui` ISSUE-037): ślad w bok dopiero od początku związku, tak jak linia pary (AC-2); otwarcie widoku osoby
  zatrzymuje ▶ na bieżącym roku. **v1.14** ([[ISSUE-038-history-on-tv-and-tempo]], Z2 — D42): tryb prezentacji ma już rok, więc rok przechodzi do trybu i z niego wraca, a nie
  zmienia się na „dziś”.
- **D38 — prior art: tekst na telewizorze liczy się w kącie widzenia, sterowanie odtwarzacza chowa się samo** (v1.14, [[ISSUE-038-history-on-tv-and-tempo]]). **Źródła**
  (odczyt 2026-10-14):
  - [Android TV → Typography](https://developer.android.com/design/ui/tv/guides/styles/typography): *„As television screens are typically viewed from a distance, interfaces
    that use larger typography are more legible and comfortable for users”*; style „display” są *„reserved for short, important text passages, or numerals”*. Wielkości ze
    źródeł biblioteki TV (`androidx/tv/material3/tokens/TypeScaleTokens.kt`): display small **36 sp**, medium 45, large 57; headline small 24;
  - [Android TV → Layouts](https://developer.android.com/design/ui/tv/guides/styles/layouts): ekran TV projektuje się jako **960 × 540 dp**; *„position the elements with a 5% margin
    of 48dp on the left and right sides, and 27dp on the top and bottom of a layout. This ensures that the layout's screen elements are within the overscan”*, z dopiskiem *„Most
    modern TVs no longer have overscan issues”*. Telefon 914 dp poziomo to prawie te same 960 dp (×1,05), a 780 dp — ×1,23, więc skala TV stosuje się do trybu prezentacji wprost.
    Telefon jest szerszy niż 16:9, więc jego obraz wypełnia **szerokość** telewizora i tylko boczne krawędzie mogą wpaść w przycięcie (u góry i u dołu są czarne pasy);
  - **czytelność z odległości:** ISO 9241-3xx podaje wysokość znaku w kącie widzenia: *„Usual LCG character heights are then 20′ to 22′ with a minimum of 16′”* — za
    [listą CSS W3C](https://lists.w3.org/Archives/Public/public-css-archive/2020Jun/0612.html); samej normy (płatnej) nie czytałem;
  - **odtwarzacz Androida** — Media3, `PlayerControlView.java` ([androidx/media](https://github.com/androidx/media), gałąź `release`): `DEFAULT_SHOW_TIMEOUT_MS = 5_000` —
    *„The time between the last user interaction and the controls being automatically hidden”*; prędkości `{0.25f, 0.5f, 0.75f, 1f, 1.25f, 1.5f, 2f}` w menu ustawień;
    `PlayerView`: `controllerHideOnTouch = true` (dotknięcie chowa sterowanie);
  - **czas dla sterowania:** `AccessibilityManager.getRecommendedTimeoutMillis` (źródła SDK Androida 36): *„Controls should remain on the screen for at least this long to give
    users time to react”* — ustawienie „Czas na działanie” w ułatwieniach dostępu, od Androida 10. We Flutterze 3.41.1 nie ma go wprost (kanał natywny, jak `openCastSettings`);
    `MediaQuery.accessibleNavigation` mówi, że działa czytnik ekranu;
  - **Gapminder:** rok jako duży napis w tle wykresu („watermark year”) — źródło wtórne,
    [omówienie grafiki Gapminder](https://lively-kernel.org/lively4/BP2019RH1/doc/research/styles/gapminder.md); animację prowadzą tam ▶ i suwak.

  **Pomiar:** *Candidates — ISSUE-038* → *Pomiar* (wysokość cyfry Roboto = wysokość wersalika, 1456/2048 em). *Obali:* na telefonie autora obraz na telewizorze nie wypełnia szerokości
  (np. system przesyła pion albo dokłada ramkę) — wtedy rok jest mniejszy, niż wynika z tabeli. Sprawdza to telewizor autora ([[ISSUE-032-mvp-install]] → *Hand checks*).
- **D39 — rok na telewizorze w lewym górnym rogu (L1)** (v1.14, **decyzja autora na stopie #1 — „Ok”, 2026-10-14**). 36 sp (display small, D38) w akcencie, jak rok w karcie, bo to ta sama
  wartość suwaka (reguła 1); na tabliczce w kolorze tła, bo przy oddaleniu linie przechodzą pod napisem (reguła 13, D23). 48 dp od lewej krawędzi (5% szerokości, D38), 24 dp od góry, jak
  dopasowany poziom (element 11). Widać go, gdy rok nie jest „dziś”, i zawsze ze sterowaniem; na „dziś” po ▶ — jeszcze 3 s, żeby rodzina zobaczyła, że historia doszła do dziś. Rośnie z
  tekstem najwyżej do 1,3× (47 sp): przy 2× miałby 72 sp i zasłaniał dwa rzędy, a już jest ponad dwa razy większy od roku w karcie ([[style-b]] *Thresholds*, wyjątek jak podpisy na
  mapie). *Obali:* na prawdziwej rodzinie rok w rogu często przykrywa osobę — wtedy L2.
- **D40 — sterowanie w prezentacji: listwa jak w odtwarzaczu (B2)** (v1.14, **decyzja autora na stopie #1 — „Ok”, 2026-10-14**). Pusty dotyk pokazuje listwę (▶ / ❚❚, rok początku, suwak,
  tempo) i „Zakończ prezentację”; drugi pusty dotyk chowa oba (Media3 `controllerHideOnTouch`). **Czas:** 5 s od ostatniego dotyku (Media3 `DEFAULT_SHOW_TIMEOUT_MS`) — dotyczy też
  „Zakończ prezentację”, które od ISSUE-034 było na 3 s (D25); z suwakiem 3 s to za mało. Dłużej, gdy ustawienie „Czas na działanie” zaleca więcej (`getRecommendedTimeoutMillis`); z
  czytnikiem ekranu sterowanie nie chowa się samo — znika po pustym dotyku (dwukrotnym w czytniku) albo po wyjściu. Czy „Czas na działanie” czytać przez kanał natywny, wybiera
  `planning` (koszt: jedna metoda w kanale, który już jest). Rok przy suwaku jest tylko w rogu (L1), nie drugi raz w listwie. Listwa stoi 24 dp nad dolną krawędzią, nad pasem bez dotyku
  (D25). *Obali:* rodzina przy telewizorze odbiera listwę jako zasłonę drzewa — wtedy B1. **v1.15** (przegląd `ui` [[ISSUE-038-history-on-tv-and-tempo]], odstępstwo 1 `dev`,
  2026-10-14): z czytnikiem sterowanie jest od wejścia w tryb i **nie znika wcale**, także po pustym dotyku. Zapis „znika po pustym dotyku (dwukrotnym w czytniku)” był błędny: pusty
  obszar nie ma węzła semantyki, więc TalkBack ani Switch Access nie mają go czym aktywować, a sterowanie schowane raz nie wróciłoby. Koszt: przy czytniku listwa stale przykrywa
  dolny rząd, także na telewizorze — osoba z czytnikiem prowadzi pokaz, więc sterowanie jest dla niej ważniejsze niż pełny dolny rząd.
- **D41 — tempo: trzy słowa, domyślnie „Średnio” (V2)** (v1.14, **decyzja autora na stopie #1 — „Ok”, 2026-10-14**). „Wolno” 5 · „Średnio” 10 · „Szybko” 20 lat na sekundę (od 1880 do dziś ok.
  29 · 15 · 7 s); „Szybko” to tempo z ISSUE-037 (ok. 21 lat/s, D34). **Przycisk przełącza** po kolei, a nie otwiera menu: trzy wartości mieszczą się w jednym dotknięciu, a menu w Media3
  jest dla siedmiu (D38). Tekst przycisku to nazwa bieżącego tempa, czytnik: „Tempo historii: średnio — zmień”. Zmiana w trakcie ▶ nie zatrzymuje odtwarzania. Przy „Usuń animacje”
  zostaje R2 (D36), a tempo zmienia tylko odstęp skoków o dekadę: co ok. 2 · 1 · 0,5 s. Pół sekundy to 2 zmiany na sekundę, poniżej progu 3 błysków ([WCAG 2.2](https://www.w3.org/TR/WCAG22/)
  SC 2.3.1). **Tempo pamięta aplikacja, dopóki działa:** w karcie i w trybie to samo, a po zamknięciu wraca „Średnio”. Zapamiętanie po zamknięciu to kolumna w tabeli `Settings`
  (jeden wiersz, dziś tylko osoba „ja” — `lib/data/database.dart`), czyli zmiana schematu z migracją, testem migracji i próbnym odtworzeniem kopii (DoD warstwy danych), albo nowa
  zależność (`pubspec.yaml` nie ma `shared_preferences`). Dla jednego przycisku to więcej, niż daje. **Zmienia US-010 AC-3**
  (tempo, domyślnie ok. 15 s od 1880). *Obali:* autor przy telewizorze za każdym razem przełącza na to samo tempo — wtedy zapamiętane tempo osobną pozycją; albo „Średnio” jest dla niego
  dalej za szybko — wtedy inne wartości (np. 3 · 6 · 12 lat/s).
- **D42 — tryb prezentacji z rokiem z karty (Z2)** (v1.14, **decyzja autora na stopie #1 — „Ok”, 2026-10-14**; zmienia D37). Rok przechodzi do trybu i z niego wraca, tak jak osoba w środku; ▶
  stoi, bo po drodze był ekran systemu (jak przy widoku osoby, D37 v1.13). Na „dziś” tryb wygląda jak w US-009. *Obali:* autor po wejściu w tryb oczekuje całej rodziny, a widzi
  rok sprzed lat (zostawiony na suwaku) — wtedy Z1.
- **D43 — prior art: ścieżka od „mnie”, czas baneru jak Snackbar, komunikat stanu** (v1.16, [[ISSUE-039-connect-two-people]]). **Źródła** (odczyt 2026-10-14):
  - FamilySearch pokazuje ścieżkę pokrewieństwa tylko od „mnie”, z nazwą u góry („My Grandmother”) — D8. Drzewo robi to samo na tym samym drzewie (D6); „Od” inne niż Ty to
    przypadek, którego tam nie ma — stąd D47;
  - **Snackbar** w Material Components Androida (`Snackbar.getDuration()`,
    [material-components-android](https://github.com/material-components/material-components-android/blob/master/lib/java/com/google/android/material/snackbar/Snackbar.java)): od
    Androida 10 *„accessibilityManager.getRecommendedTimeoutMillis(userSetDuration, controlsFlag | FLAG_CONTENT_ICONS | FLAG_CONTENT_TEXT)”*, a `FLAG_CONTENT_CONTROLS` tylko przy
    przycisku działania; na stałe zostaje tylko komunikat z działaniem przy czytniku (starsze Androidy). Baner nie ma działania, więc dostaje ten sam czas co Snackbar, a nie regułę
    sterowania z D40 (tam są przyciski);
  - **WCAG 2.2 SC 4.1.3 Status Messages** ([Understanding](https://www.w3.org/WAI/WCAG22/Understanding/status-messages.html)): komunikat o wyniku działania ma dać się przeczytać
    czytnikowi *„without receiving focus”* — baner to wynik wyboru „Do”.

  **Pomiar** — *Candidates — ISSUE-039* → *Pomiar*. *Obali:* na telefonie z czytnikiem baner znika, zanim czytnik skończy go czytać — wtedy baner do końca podświetlenia, jak D40.

  **v1.17** (przegląd `ui` [[ISSUE-039-connect-two-people]], odstępstwo 1 `dev`, 2026-10-14): czytnik dostaje baner jako **region na żywo** (`Semantics(liveRegion: true)`), a nie
  przez `SemanticsService` — tak jak pigułkę poziomu na tym samym ekranie (element 3). Tekst baneru jest na ekranie, więc czytnik czyta węzeł, który widać, a nie osobny komunikat
  bez miejsca; to webowy odpowiednik `role=status`, technika wystarczająca dla SC 4.1.3 (ARIA22 w [Understanding 4.1.3](https://www.w3.org/WAI/WCAG22/Understanding/status-messages.html)).
  Na emulatorze baner jest węzłem z tekstem (`uiautomator dump`); mowy TalkBack agent nie słyszy — odsłuch zostaje do [[ISSUE-032-mvp-install]] → *Hand checks*. *Obali:* TalkBack
  na telefonie nie czyta baneru, gdy się pojawia — wtedy ogłoszenie przez `SemanticsService`, jak rok w karcie.
- **D44 — ikona „Połącz dwie osoby”: `link_outlined` (A1)** (v1.16, **decyzja autora na stopie #1 — „Tak”, 2026-10-14**; zamyka *Open* 1a). Ta sama ikona stoi w [[osoba]] 7 nad łańcuchem „Jak
  łączy się ze mną”, a ścieżka na drzewie to ten łańcuch narysowany — jeden znak dla jednej rzeczy. Istnieje we Flutterze 3.41.1 (`icons.dart`, sprawdzone w SDK 2026-10-14; tak samo
  `route_outlined` i `polyline_outlined`, a `conversion_path` — nie). *Obali:* autor na makiecie albo emulatorze bierze ją za „udostępnij link”.
- **D45 — „Do” staje w środku (W2)** (v1.16, **decyzja autora na stopie #1 — „Tak”, 2026-10-14**). Przestawienie środka jak po dotknięciu (element 4), więc karta mówi, kim jest „Do” dla mnie, także po zniknięciu baneru, a
  „Pokaż ›” prowadzi do tej osoby. Poziom i kadr liczą się od „Do”; linia dalej biegnie od „Od” (D5). W pomiarze ścieżka przy W2 częściej mieści się w skali poziomu (25 razy nie, przy W1 —
  55). *Obali:* autor chce, żeby po końcu podświetlenia drzewo było przy „Od” — wtedy W1.
- **D46 — długa ścieżka: drzewo maleje, aż cała ścieżka się zmieści (F2)** (v1.16, **decyzja autora na stopie #1 — „Tak”, 2026-10-14**). Kadr najpierw w skali poziomu (S2); gdy ścieżka się w niej nie mieści — mniejsza
  skala, najmniej 0,15 (w makiecie najmniej 0,34 przy 100% i 0,17 przy 200%). Linia ma tę samą grubość przy każdej skali. Po końcu podświetlenia skala wraca do 0,4 (dół zakresu S2)
  z osobą w środku. Imiona ze ścieżki mają pierwszeństwo przy chowaniu nakładających się (I2). Kadr liczy skrajne osoby ścieżki z ich miejscem; `dev` sprawdza, czy imię na skraju nie
  wychodzi poza ekran (w makiecie przy 200% wyszło — imię rośnie o 1/skala). *Obali:* na prawdziwej rodzinie osoby spoza ścieżki jako kropki gubią kontekst — wtedy F1.
  **v1.17** (przegląd `ui` [[ISSUE-039-connect-two-people]], odstępstwo 2 `dev`, 2026-10-14): **na poziomie 1 kadr w skali 1,3**, czyli na dole zakresu poziomu, a nie „aż do 2,0”. Krótka
  ścieżka (Ja → córka) w skali 2,0 miałaby okręgi 88 dp i imiona 26 sp — większe niż w każdym innym widoku drzewa, które startuje w skali 1. Na pozostałych poziomach kadr bierze
  największą skalę poziomu, w której ścieżka się mieści. Tak było w makiecie; na emulatorze — zrzut `29` (Ja → Zofia).
- **D47 — baner, gdy „Od” to nie Ty: dwie linie bez odmiany imion (O2)** (v1.16, **decyzja autora na stopie #1 — „Tak”, 2026-10-14**). Pierwsza linia: „Imię Nazwisko → Imię Nazwisko” w mianowniku (bez „z d.”; „Ja”,
  gdy to Ty). Druga: nazwa z tych samych odcinków co w G2 (D6, D12), bez zaimka przy ostatnim odcinku — „Wnuczka”, „Siostrzenica bratowej”, „Ciotka (siostra taty)”. Słownik się nie
  zmienia; odpada tylko „mój / moja / mojej / mojego”. Gdy „Od” to Ty — jedna linia jak w AC-3. *Obali:* autor czyta drugą linię bez pierwszej i myli kierunek („Wnuczka” — czyja?)
  — wtedy O3 z tabelą odmiany imion i testami.
- **D48 — ścieżka przestawia rok na „dziś” (Y1)** (v1.16, **decyzja autora na stopie #1 — „Tak”, 2026-10-14**; **zmienia D37** dla jednego wejścia). Wybór „Do” zatrzymuje ▶ i ustawia suwak na „dziś”, jak wejście z paska.
  Pokrewieństwo nie zależy od roku, a w roku Y część ścieżki byłaby pustymi pierścieniami bez imion. *Obali:* autor przygotowuje opowieść w roku Y i chce w nim zostać — wtedy Y2.
- **D49 — „Połącz dwie osoby”: decyzje projektowe** (v1.16, bez pytania; „tak” na stopie #1 przyjmuje je z planem):
  - **poziom:** najniższy z całą ścieżką od osoby w środku; dalej niż poziom 4 — poziom 4 i brakujące osoby ścieżki (od „Ja” 9 ze 105; we wszystkich parach 60%, bo od osoby na brzegu
    rodziny poziomy są małe);
  - **linia po liniach rodziny**, a nie na skos: autor mówił *„powoli linie idą odemnie do kolejnych osób”* ([[SPIKE-004-mvp-flow-prototype]] D26), a skos przecinałby inne osoby;
  - **baner, gdy linia dojdzie do „Do”** — nazwa na końcu drogi, nie na początku; kadr zostawia mu miejsce u góry;
  - **koniec podświetlenia:** każde działanie, które zmienia drzewo (dotknięcie, wstecz, poziom, rok, ▶, przesyłanie). Przeciąganie nie kończy, żeby dało się obejrzeć ścieżkę. Pierwsze
    dotknięcie osoby tylko kończy podświetlenie, żeby przypadkowe dotknięcie nie przestawiło środka. **v1.17** (przegląd `ui` [[ISSUE-039-connect-two-people]], odstępstwo 3 `dev`): kończy je
    też **zmiana danych drzewa** — osoby ścieżki mogły zniknąć albo zmienić rodzinę, a linia biegłaby po starym układzie;
  - **wyszarzenie** (v1.17, odstępstwo 5 z przeglądu ISSUE-039 — w *Dev report* go nie ma): przy 30% są osoby spoza ścieżki i **wszystkie** linie rodziny ze śladami, także osób ze ścieżki.
    Linie to jedna warstwa (plan D7: wyszarzenie grupy jedną warstwą), a linia rodziny przy osobie ze ścieżki prowadzi albo do osoby wyszarzonej, albo leży pod linią w akcencie. Ślad
    dalszej rodziny przy osobie ze ścieżki w czasie podświetlenia niczego nie dodaje. *Obali:* autor na emulatorze gubi, gdzie osoba ze ścieżki ma dalszą rodzinę — wtedy linie i ślady osób
    ze ścieżki w pełnym kryciu, w osobnej warstwie;
  - **okno:** okno z dwoma kaflami, jak chciał autor (*„pojawia mi się pop-up z dwoma kaflami”*, SPIKE-004 D26). Lista — tryb wyboru jak „Która osoba to Ty?” (`MePickerScreen`,
    [[style-b]] reguła 12), bez osoby z drugiego kafla (ta sama osoba nie ma ścieżki). Każde otwarcie zaczyna od „Ja”;
  - **tryb prezentacji bez „Połącz dwie osoby”** w MVP — nie ma tam paska z ikonami, a „Przesyłaj na telewizor” kończy podświetlenie. Ścieżka na telewizorze to wejście do
    [[2026-10-14-opowiesc-rodziny-i-wieniec]];
  - **pigułka poziomu** nie pokazuje się przy przejściu do ścieżki — w tym miejscu stoi baner.

  *Obali:* autor na emulatorze chce kończyć podświetlenie tylko przez wstecz albo chce, żeby okno pamiętało ostatnie „Od”.

## Open
1. ~~⚠️ OPEN — sterowanie poziomami — nowy wygląd~~ — rozstrzygnięte 2026-10-13: S2 (element 3), 4 progi (autor na stopie #1
   SPIKE-002: *„Tak”*).
1a. ~~⚠️ OPEN — ikona „Połącz dwie osoby”~~ — **rozstrzygnięte 2026-10-14: A1** `link_outlined` (stop #1 [[ISSUE-039-connect-two-people]], *„Tak”*; D44). Zapis sprzed
   decyzji: (element 1) `conversion_path` **nie istnieje** w `Icons` Fluttera 3.41.1 (sprawdzone w SDK
   2026-10-09, przy [[osoba]] D18). Do wyboru przy pozycji drzewa: `link` (jak „Jak łączy się ze mną” w [[osoba]] — ta sama
   idea) albo własna ikona wektorowa. **v1.16:** kandydaci A1–A4 na makiecie `drzewo-039.html`, rekomendacja **A1** `link_outlined` (D44) — na stop #1
   [[ISSUE-039-connect-two-people]], razem z *Open* 10.
2. ~~⚠️ OPEN — pokazanie drzewa na telewizorze~~ — rozstrzygnięte 2026-10-13: D11.
2a. ~~⚠️ OPEN — trzeci rodzaj linii (adopcja)~~ — nie (autor: *„linie są super”*).
3. ~~⚠️ OPEN — czytelność ok. 100 osób na telefonie~~ — **rozstrzygnięte 2026-10-13 ([[SPIKE-002-tree-on-a-phone]] → *Findings*,
   v1.4):** czytelnie od osoby (K2) przy skali bliskiej 1, z przesuwaniem i przestawianiem środka; całości naraz — nie. Własny układ
   (port makiety) zamiast `graphview`. Zadanie na czas < 30 s i płynność na fizycznym telefonie → [[ISSUE-032-mvp-install]] → *Hand
   checks* (stop #2 SPIKE-002: zadanie „pomiń”). **Wejścia do pozycji drzewa z *Findings*:** przy tekście 200% miejsce osoby rośnie jak w
   mini-drzewie ([[osoba]] v2.2) i inicjały mają limit wielkości (M4); karta osoby w środku potrzebuje nazwy złożonej (D6); przejście
   między poziomami — optymalizacja rysowania (M3); skala S2 z osi x, nie `getMaxScaleOnAxis()`.
5. ~~⚠️ OPEN — imiona przy oddalaniu~~ — **rozstrzygnięte 2026-10-13: I2** (stop #1 [[ISSUE-033-tree-from-a-person]], *„Tak”*; element 4,
   [[style-b]] reguła 13 v1.25). Zapis sprzed decyzji (v1.4, SPIKE-002 *Findings* → M4): na poziomie 4 (skala ok. 0,48) imię ma ok. 6 sp i znika jako
   tekst. **Kandydaci na makiecie (v1.5, *Candidates — US-009*):** **I1** imiona maleją z drzewem · **I2** zostają czytelne, a nakładające się
   chowają · **I3** od poziomu 3 imię ma tylko osoba w środku. **Rekomendacja: I2.** Na poziomie 4 widać 63 z 99 imion w 13 sp, a nie 99
   nieczytelnych (I1) albo jedno (I3). Pierwszeństwo osób bliżej środka to ta sama reguła co poziomy (D2, D8), a mapa pokazuje podpisy
   tak samo, więc aplikacja wszędzie zachowuje się podobnie. **Nie da:** stałego zestawu imion — przy oddalaniu część imion znika i wraca.
   *Obali:* miganie imion przy szczypaniu przeszkadza — wtedy I3. **v1.8 — zmiana decyzji autora** (stop #1
   [[ISSUE-034-tree-presentation-mode]], 2026-10-14): **I1**, w osobnej pozycji „drzewo: I1 i „Moja””. Jej `ui` mierzy też tryb prezentacji przy
   tekście 200% na ekranie 360 dp (zrzut `18b` ISSUE-034, przy I2: skala 0,45, imiona 26 sp przy okręgach ok. 20 dp, 13 z 20 imion widać, a
   tabliczki zasłaniają linie między rzędami). **v1.9 — z powrotem I2** (stop #1 [[ISSUE-035-tree-names-shrink-my-voice]], 2026-10-14: *„1 I2”*):
   kod bez zmian (D27).
4. ~~⚠️ OPEN — całe drzewo (K1) jako dodatkowy tryb? i ślad dalszej rodziny (D9) — tak czy nie?~~ — rozstrzygnięte 2026-10-13: K2
   bez K1, ślad — tak.
6. ~~⚠️ OPEN — kto mówi w karcie~~ — **rozstrzygnięte 2026-10-13: G1** (stop #1 [[ISSUE-033-tree-from-a-person]], *„Tak”*; dotyczy też
   banera 9 w US-011). Zapis sprzed decyzji (v1.5, AC-5): **G1** „Twoja babcia”, „Siostra cioteczna babci Twojej żony” · **G2** „Moja babcia”,
   „Siostra cioteczna babci mojej żony”. **Rekomendacja: G1.** Aplikacja wszędzie mówi do Ciebie („Wybierz, która osoba to Ty”, „…łączy się
   z Tobą”), a nagłówek „Jak łączy się ze mną” to pytanie, które sam zadajesz. Wybór obowiązuje też baner „Połącz dwie osoby” (9, US-011):
   przy G1 przykład z D6 brzmi „Siostra cioteczna babci Twojej żony”, a przykład w AC-5 US-009 trzeba poprawić. **Nie da:** zdania Twoim
   głosem, jak w notatkach. *Obali:* „Twoja” brzmi obco w aplikacji o własnej rodzinie. **v1.8 — zmiana decyzji autora** (stop #1
   [[ISSUE-034-tree-presentation-mode]], 2026-10-14): **G2** („Moja babcia”), w tej samej osobnej pozycji co I1 (*Open* 5). **v1.9 — specyfikacja
   G2** (potwierdzone na stopie #1 ISSUE-035: *„2 „moja babcia””*): elementy 4, 5, 9, D28 (nazwa pokrewieństwa Twoim głosem, zdania aplikacji do Ciebie — [[style-b]] reguła 7 v1.28). Buduje
   [[ISSUE-035-tree-names-shrink-my-voice]].
7. ~~⚠️ OPEN — wejście w przesyłanie z aplikacji: P1, P2 czy P3?~~ — **rozstrzygnięte 2026-10-14: P2** (stop #1 [[ISSUE-036-cast-from-the-app]], *„tak”*; D30).
   Zapis sprzed decyzji: ([[ISSUE-036-cast-from-the-app]], v1.10; kandydaci i rekomendacja — *Candidates — ISSUE-036*,
   makieta `drzewo-036.html`.) **Rekomendacja: P2** — jedna ikona `cast_outlined` „Przesyłaj na telewizor” zamiast ikony telewizora; ekran systemu, a po powrocie
   tryb prezentacji. Elementy 1 i 11, *Navigation*, *States* i *AC → element* są zapisane według P2. Przy P1 albo P3 `ui` zmienia je przed planem. Na stop #1,
   razem z zrzutem tego, co przycisk naprawdę otwiera (D29).
8. ~~⚠️ OPEN — czas na drzewie: N, C, T, E, R~~ — **rozstrzygnięte 2026-10-14: N3, C1, T2, E3, R2** (stop #1 [[ISSUE-037-time-on-the-tree]], *„tak”*; D32–D36).
   Zapis sprzed decyzji: ([[ISSUE-037-time-on-the-tree]], v1.12; kandydaci, pomiar i rekomendacja — *Candidates — ISSUE-037*, makieta
   `drzewo-037.html`). **Rekomendacja: N3, C1, T2, E3, R2** (D32–D36). Elementy 4 i 6, *States*, *Sketch* i *AC → element* są zapisane według rekomendacji. Przy innym
   wyborze `ui` zmienia je przed planem. T2 zmienia brzmienie US-010 AC-3, a E3 — drzewo na „dziś” (element 4). Na stop #1.
9. ~~⚠️ OPEN — historia na telewizorze i tempo: L, B, V, Z~~ — **rozstrzygnięte 2026-10-14: L1, B2, V2, Z2** (stop #1 [[ISSUE-038-history-on-tv-and-tempo]], *„Ok”*; D39–D42).
   Zapis sprzed decyzji: ([[ISSUE-038-history-on-tv-and-tempo]], v1.14; kandydaci, pomiar i rekomendacja — *Candidates — ISSUE-038*, makieta
   `drzewo-038.html`). **Rekomendacja: L1, B2, V2, Z2** (D39–D42). Elementy 6 i 11, *Navigation*, *States*, *Sketch* i *AC → element* są zapisane według rekomendacji; przy innym
   wyborze `ui` zmienia je przed planem. V2 zmienia US-010 AC-3 (tempo zamiast „ok. 7 s”), a Z2 — D37. Na stop #1.
10. ~~⚠️ OPEN — „Połącz dwie osoby”: A, W, F, O, Y~~ — **rozstrzygnięte 2026-10-14: A1, W2, F2, O2, Y1** (stop #1 [[ISSUE-039-connect-two-people]], *„Tak”*; D44–D48).
   Zapis sprzed decyzji: ([[ISSUE-039-connect-two-people]], v1.16; kandydaci, pomiar i rekomendacja — *Candidates — ISSUE-039*, makieta
   `drzewo-039.html`). **Rekomendacja: A1, W2, F2, O2, Y1** (D44–D48), do tego decyzje projektowe D49. Elementy 1, 7–10, *Navigation*, *States*, *Sketch* i *AC → element* są
   zapisane według rekomendacji; przy innym wyborze `ui` zmienia je przed planem. Y1 zmienia D37 (ścieżka ustawia „dziś”), F1 zmieniłoby brzmienie US-011 AC-2. Na stop #1.
