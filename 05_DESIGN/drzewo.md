---
screen: "Drzewo — rodzina od osoby, poziomy połączeń, czas; połącz dwie osoby"
items: ["[[SPIKE-004-mvp-flow-prototype]]", "[[ISSUE-024-person-view]]", "[[SPIKE-002-tree-on-a-phone]]", "[[US-009-drzewo-od-osoby]]", "[[ISSUE-033-tree-from-a-person]]", "[[ISSUE-034-tree-presentation-mode]]", "[[ISSUE-035-tree-names-shrink-my-voice]]", "[[ISSUE-036-cast-from-the-app]]", "[[ISSUE-037-time-on-the-tree]]", "[[ISSUE-038-history-on-tv-and-tempo]]", "[[ISSUE-039-connect-two-people]]", "[[ISSUE-044-family-wreaths]]", "[[ISSUE-045-migration-map]]", "[[ISSUE-049-tree-levels-and-zoom]]", "[[ISSUE-050-next-event]]", "[[ISSUE-055-connect-from-the-tree-and-rotate]]", "[[ISSUE-056-tree-lines-readable]]"]
us: "[[US-009-drzewo-od-osoby]] (M9) · [[US-010-czas-na-drzewie]] (M10) · [[US-011-polacz-dwie-osoby]] (M11) — [[EPIC-003-zrozumienie]]"
journey-step: "widok 5 (M9–M11, R3)"
mockup: "2026-10-23: prototyp-056.html (ISSUE-056: linie przy dużej rodzinie — dziś, piętra szyn + mostki, kolor rodziny, nowa kolejność, telefon i telewizor; geometria z sondy na tree_layout.dart, 116 wymyślonych osób; zrzuty `shots056\\`) — katalog tymczasowy sesji `6d4e489c-…\\scratchpad`; 2026-10-23: prototyp-055.html (ISSUE-055: „Od” z drzewa, ścieżka do wstecz z banerem, układ poziomy L1–L4 z podglądem telewizora 16:9; 16 wymyślonych osób; zrzuty `shots055\\`) — katalog tymczasowy sesji `8d325e2e-…\\scratchpad`; 2026-10-19: drzewo-050.html (ISSUE-050: ⏭ „Następne” w karcie i na listwie, podpis roku na telefonie i telewizorze; kandydaci K1–K2, N1–N2, F1–F2, Z1–Z2, V1–V2, P1–P2, U1–U3 na 117 wymyślonych osobach z makiety ISSUE-049, podgląd „z kanapy” 32–65″, autotest `#test50=1`; obok mapa-050.html — M1–M2 na rodzinie z makiety mapy; zrzuty `shots050\\`) — katalog tymczasowy sesji `ef3f4405-…\\scratchpad`; 2026-10-19: drzewo-049.html (ISSUE-049: reguła poziomów M1–M2, przełącznik P1–P3, nazwy N1–N2, skala po zmianie poziomu K1–K2, poziom na telewizorze T1–T2, przybliżanie do całego drzewa, tryb prezentacji z gestami; 117 wymyślonych osób — 107 z makiet drzewa i 10 do AC-2, AC-3; zrzuty `shots049\\`, autotest `#test49=1`) — katalog tymczasowy sesji `92dbd968-…\\scratchpad`; 2026-10-14: drzewo-039.html (ISSUE-039: ikona w pasku, okno z kaflami „Od” i „Do”, lista wyboru, ścieżka na drzewie, baner; kandydaci A1–A4, W1–W2, F1–F2, O1–O3, Y1–Y2 na 106 wymyślonych osobach; zrzuty `shots-039\\`) — katalog tymczasowy sesji `0558e715-…\\scratchpad`; 2026-10-14: drzewo-038.html (ISSUE-038: tryb prezentacji poziomo z rokiem L1–L3, sterowaniem B1–B3, tempem V1–V3, wejściem Z1–Z2 i podglądem „z kanapy” 32–65″; zrzuty `shots-038\\`) — katalog tymczasowy sesji `baf00b7b-…\\scratchpad`; 2026-10-14: drzewo-037.html (ISSUE-037: suwak czasu, kandydaci N1–N3, C1–C2, T1–T2, E1–E3, R1–R2 na wymyślonej rodzinie z datami niepewnymi; zrzuty `shots-037\\`) — katalog tymczasowy sesji `555909c3-…\\scratchpad`; 2026-10-14: drzewo-036.html (ISSUE-036: kandydaci P1–P3 wejścia w przesyłanie, zrzuty z emulatora `shots-036\\`) — katalog tymczasowy sesji `fa865b36-…\\scratchpad`; 2026-10-13: drzewo-us009.html (US-009: imiona przy oddalaniu I1–I3, karta z nazwami pokrewieństwa, tekst 200%, tryb prezentacji, stany) — katalog tymczasowy sesji `c3868f5f-…\\scratchpad`; 2026-10-13: drzewo-spike002.html (SPIKE-002, kandydaci na 106 wymyślonych osobach) — `220a9b6c-…\\scratchpad`; wcześniej 2026-10-08: grobing-prototyp.html (SPIKE-004, panel 6, runda 2)"
updated: 2026-10-23
---

# Drzewo — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.54) · referencja: [[references]] → **R3**.
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
>
> **Wersja 1.20 (2026-10-17, stop #1 [[ISSUE-045-migration-map]] — decyzja autora W2):** zakładka Drzewo ma **dwie części: „Drzewo” i „Mapa”** — przełącznik
> segmentowy zamiast tytułu w pasku (element 1) i w sterowaniu trybu prezentacji (element 11). Osoba w środku, karta, rok, tempo i ▶ są wspólne; „Połącz dwie
> osoby” zostaje przy drzewie. Część „Mapa” — [[mapa-migracji]]. Drzewo samo w sobie bez zmian.
>
> **Wersja 1.21 (2026-10-17, przegląd `ui` zbudowanej [[ISSUE-045-migration-map]]):** w przełączniku (element 1) ikona części „Mapa” to `public_outlined`
> ([[style-b]] reguła 3 — cienkie ikony; v1.20 podawała `public`), a napisy albo same ikony liczone są względem miejsca w części „Drzewo”, więc przełącznik ma
> ten sam kształt w obu częściach ([[mapa-migracji]] v1.2, D20).
>
> **Wersja 1.22 (2026-10-17, ponowny przegląd `ui` zbudowanej [[ISSUE-045-migration-map]] — odstępstwo 9 `dev` przyjęte):** w sterowaniu trybu prezentacji
> (element 11) przełącznik „Drzewo · Mapa” stoi **na środku miejsca między rokiem w rogu a „Zakończ prezentację”**, a nie na środku ekranu; gdy napisy się tam
> nie mieszczą — same ikony. Przy tekście 200% przełącznik na środku ekranu wchodził pod „Zakończ” ([[mapa-migracji]] v1.3, D24). [[style-b]] bez zmian.
>
> **Wersja 1.23 (2026-10-19, `ui` przed planem [[ISSUE-049-tree-levels-and-zoom]]; decyzja autora na stopie #1 tego dnia — *„tak”*: M2, P2, N2, K1, T2, zapis bez zmian):** **poziomy i przybliżanie rozdzielone**, jak chciał autor
> (*„niezależne względem siebie funkcjonalności”*). **Poziom = 1 + liczba związków na drodze od osoby w środku** — krew nic nie kosztuje (D50, zastępuje D2); wybiera go
> osobny przełącznik (element 3, D53), a **przybliżanie i oddalanie zmienia tylko widok**, aż do całego drzewa (element 3a, D51; zastępuje S2 i D18). Tryb prezentacji
> dostaje dwa palce, − / + i przełącznik poziomu (element 11, D56; zmienia D16 i D25 a). Prior art i pomiar — *Candidates — ISSUE-049*. **Na stop #1** (*Open* 11, makieta
> `drzewo-049.html`): **M2** (mąż, żona i partner krewnego na poziomie 1, ich rodziny wyżej), **P2** (etykieta „Linia krwi ▾” i lista), **N2** (nazwy „Linia krwi”, „Przez 1
> związek”…), **K1** (skala zostaje po zmianie poziomu), **T2** (poziom także na telewizorze). Elementy 3, 3a, 4, 8, 11, *Navigation*, *States*, *Sketch* i *AC → element* są
> zapisane według rekomendacji; przy innym wyborze `ui` zmienia je przed planem. Pomiary z elementu 11 sprzed v1.23 (skala 0,45 przy 200%, rok w rogu) dotyczą
> dopasowanego poziomu 2. [[style-b]] v1.44 — wyjątek celu dotyku (D52).
>
> **Wersja 1.24 (2026-10-19, przegląd `ui` zbudowanej [[ISSUE-049-tree-levels-and-zoom]] — odstępstwa 1–3 `dev` i dwie poprawki z testów `qa` przyjęte):**
> oddalenie do końca stawia **cały poziom na środku** obszaru drzewa — przy −, po geście dwóch palców po 0,4 s spokoju i gdy skala rośnie do nowej granicy (1 → element 3a,
> 11, D51; − od „Ja” zostawiało drzewo w bok, z osobą uciętą przy krawędzi) · osoba z widocznym imieniem leży **nad sąsiadami**, więc tabliczka zakrywa okręgi, a nie okręgi
> litery (2 → element 4; [[style-b]] reguła 13, v1.45) · **w trybie prezentacji bez pigułki** po zmianie poziomu — u góry stoi sterowanie, a nazwę mówi etykieta na listwie (3 →
> elementy 3, 11, D57) · **listwa:** etykieta poziomu najwyżej 30% szerokości listwy (nazwa ucina się „…”), etykieta i − / + dopiero na listwie od 560 dp — z czytnikiem
> ekranu sterowanie przychodzi, zanim telefon się obróci, a listwa 302 dp przepełniała się o 6,5 dp (test `qa` → element 11, D56) · **kadr ścieżki** może zejść poniżej
> granicy całego poziomu, do 0,08: granica liczy miejsca osób, a imiona przy oddalaniu nie maleją (I2) — test ISSUE-039 (MAJOR przeglądu: imiona ścieżki w całości na
> ekranie) złapał 0,4 dp za marginesem (test `qa` → element 8, D57). Doprecyzowane z emulatora: etykieta przy tekście 200% ma ok. 140–235 dp („Linia krwi” – „Przez 3
> związki”), a nie ok. 170 dp z makiety (element 3, *States*). Odstępstwa 4 (narzędzie wymyślonej rodziny) i 5 (liczba osób w makiecie) nie dotyczą ekranu.
>
> **Wersja 1.25 (2026-10-19, stop #2 [[ISSUE-049-tree-levels-and-zoom]] — decyzja autora, D58):** *„jednak zamiast "kogo pokazać na drzewie" chciałbym mieć prosty "+"
> "-"”* · *„Obecny "+" "-" można zastąpić/usunąć bo wystarczy funkcja ręcznego zoom-in/out”* · *„Te komentarze odnoszą się tak samo do widoku w aplikacji i na
> telewizorze”*. **+ / − w prawym dolnym rogu zmieniają poziom** — + dalsza rodzina, − bliższa, na krańcach nieaktywne; etykieta „Linia krwi ▾” i lista „Kogo pokazać na
> drzewie” odpadają (element 3; zastępuje P2 z D53). **Przycisków przybliżania nie ma** — przybliżają dwa palce, podwójne dotknięcie i dotknięcie małego drzewa, **oddalają
> tylko dwa palce** (element 3a; [[style-b]] v1.46 — wyjątek od SC 2.5.1). **Tryb prezentacji:** na listwie − / + poziomu zamiast etykiety i przybliżania, a **pigułka poziomu
> jest także na telewizorze**, pod górnym rzędem sterowania — bez etykiety tylko ona mówi, który poziom widać (element 11; cofa odstępstwo 3 z v1.24). Pomiar z emulatora —
> element 11, *States*.
>
> **Wersja 1.26 (2026-10-19, `ui` przed planem [[ISSUE-050-next-event]]; decyzja autora na stopie #1 tego dnia — *„tak”*: K1, N1, F1, Z1, V2, P1, U3, mapa M2, zapis bez zmian).** Cel autora — odpowiedź na pytanie „po co dziś” (retro 4, R1) w `/pm`
> 2026-10-19: **(a) opowiadanie rodzinie przy telewizorze** — autor dotyka, rodzina czyta rok i podpis z kanapy; projekt zaczyna od trybu prezentacji, telefon jest drugi.
> **⏭ „Następne” zaraz za ▶** w karcie (element 6) i na listwie (element 11): suwak przeskakuje do najbliższego późniejszego roku ze zdarzeniem, a **podpis roku** (nowy
> element 6a) mówi, co się w nim stało — na telewizorze pod rokiem w rogu, 28 sp. Na stop #1 (*Open* 12, makiety `drzewo-050.html` i `mapa-050.html`): **K1** (zdarzenia osób z
> wybranego poziomu), **N1** (data niepewna w roku zapisanym, z dopiskiem), **F1** (czasownik według płci), **Z1** (⏭ zatrzymuje ▶), **V2** (drzewo podjeżdża do osób z podpisu, gdy są
> poza ekranem), **P1** (podpis pod rokiem w rogu), **U3** (w karcie bez roku początku); mapa — **M2** ([[mapa-migracji]] v1.5). Elementy 6, 6a, 11, *Navigation*, *States*,
> *Sketch* i *AC → element* są zapisane według rekomendacji; przy innym wyborze `ui` zmienia je przed planem. Prior art, kandydaci i pomiar — *Candidates — ISSUE-050*.
> [[style-b]] v1.47 — próg „tekst dla telewizora” dla zdań (28 sp).
>
> **Wersja 1.27 (2026-10-19, przegląd `ui` zbudowanej [[ISSUE-050-next-event]] — odstępstwa 1–3 `dev` przyjęte):** **podpis na telewizorze** — tabliczka 48 dp od lewej, jak
> tabliczka roku, z tym samym wcięciem 6 dp, więc tekst zaczyna się 54 dp od lewej, równo z cyframi roku (1 → elementy 6a, 11, D64; v1.26: „tekst 48 dp od lewej”) · **V2 — grupa
> 8 dp pod podpisem, a nie na środku obszaru**: w poziomie na środku, za szeroka — pierwsza osoba i tak w obszarze, na + / − w rogu telefonu — grupa w lewo, za wysoka — rząd
> pierwszej osoby u góry (2 → element 6a, *States*, D63; przy tekście 200% na 360 dp środek obszaru wypadał na wysokości + / −, a „Tomasz” stał pod „+”) · **„Urodził się”,
> „Urodziła się” z twardą spacją przed „się”** — linia nie zaczyna się od „się Jan…” (3 → element 6a, D61; jedna instancja — do [[style-b]] reguły 6 przy drugiej). Pomiar z
> emulatora (411 × 914 dp, [[ISSUE-050-next-event]] → *Dev report* → *Measurements*): suwak w karcie przy 100% z ⏭ i bez roku początku — 189 dp (tor ok. 141 dp; liczby z elementu 6
> są z makiety 360 dp); po ⏭ od „Ja” w skali 1 za każdym razem co najmniej jedna osoba z podpisu na ekranie, razem 123 ze 178 (69%); podpis 4 zdarzeń na telewizorze — 447 × 146 dp
> (49% szerokości), dół ok. 221 dp z 411. [[style-b]] i [[mapa-migracji]] bez zmian (mapa bierze podpis na telewizorze z D64).
>
> **Wersja 1.28 (2026-10-19, stop #2 [[ISSUE-050-next-event]], runda 1 — prośba autora i decyzja *„B”*):** autor na emulatorze: *„dobrze by było gdyby rzeczy które się dzieją były
> podświetlone na telewizorze (obwódka wokół osoby i/lub podświetlona relacja) natomiast sama informacja kto się urodził itd. niech zostanie na telefonie (aby nie przysłaniała drzewa na
> telewizorze)”* · *„chciałbym aby ich obwódka / laur "lśniały"”*. Telewizor dostaje kopię ekranu telefonu (przesyłanie ekranu — D11, D29), więc napisu „tylko na telefonie” w trybie
> prezentacji być nie może; z dwóch wariantów (A — w trybie prezentacji bez podpisu, B — linia na listwie) autor wybrał **B**: **podpis w trybie prezentacji to drobna linia na listwie** nad
> rzędem ▶ ⏭, znika z listwą po 5 s (D72 — zastępuje P1, D64); **osoby z podpisu świecą** — pierścień w akcencie i poświata pod okręgiem i pod wieńcem, trzy łagodne pulsy, potem stała
> poświata, dopóki stoi podpis; przy ślubie i „razem” także linia pary w akcencie (D73 — zastępuje D70); na telefonie i w trybie prezentacji tak samo (D74), przy ograniczeniu animacji bez
> pulsu (D75). Poza trybem prezentacji dymek bez zmian. Zmienione: elementy 6a i 11, *States*, *Sketch*, *Style B rules applied*, *AC → element*, D63, D64, D70. Makiety tej zmiany nie ma:
> autor zgłosił ją na zbudowanym ekranie i sprawdza ją na emulatorze w rundzie 2 stopu #2. [[style-b]] v1.48 — reguła 2, poświata osób z podpisu; [[mapa-migracji]] v1.6 — linia na listwie
> i świecące awatary.

> **Wersja 1.29 (2026-10-23, `ui` przed planem [[ISSUE-055-connect-from-the-tree-and-rotate]]; decyzje autora na prototypie `prototyp-055.html` tego dnia).** Uwagi
> autora po pierwszym pokazie drzewa rodzinie (`/pm` 2026-10-22) i pięć paneli: **„Od” = osoba w środku** (D78 — panel 1, *„tak”*); **ścieżka zostaje do gestu wstecz,
> bez „×”** (D79 — *„w sumie nie chcę, aby był »x«, wystarczy mi gest wstecz”*); **w trakcie ścieżki samo drzewo i baner do końca** (D80 — *„B1”*); **po wyjściu rok sprzed
> ścieżki, „Od” w środku** (D81 — *„tak”*); **przycisk „Obróć” i układ poziomy L4 „bez zakładek”** dla drzewa i części „Mapa” (D76 — cel z pytania `ui`: w trybie prezentacji
> nie ma ścieżki, a przesyłanie z szybkich ustawień zostawia pion; D77 — *„L4”* po odrzuceniu L1: *„więcej miejsca na drzewo a mniej na »interface«”*; mapa — panel 5,
> *„tak”*). Zastąpione: D45; w D48 rok po wyjściu; w D49 „każde otwarcie od „Ja””, koniec podświetlenia i brak ikony bez „ja”; w elemencie 9 czas baneru (D43). Zmienione:
> elementy 1, 7, 8, 9, 10, nowy 12 (układ poziomy), *Navigation*, *States*, *Sketch*, *AC → element*. Decyzja projektowa D82 (przycisk „Obróć”). [[style-b]] v1.54 — reguła 12
> (dolny pasek ukryty w poziomie na drzewie i mapie); [[mapa-migracji]] v1.7.
>
> **Wersja 1.30 (2026-10-23, przegląd `ui` zbudowanej [[ISSUE-055-connect-from-the-tree-and-rotate]] — odstępstwa 1–2 `dev` przyjęte):** **lista „Od kogo?” / „Do kogo?” w
> poziomie zostaje pozioma**, a klawiatura zakrywa wtedy wyniki — pokazuje je klawisz szukania na klawiaturze albo jej schowanie (1 → element 7, D77) · **dolny pasek w części
> „Mapa” ma ok. 79 dp** — linia „gdzie” to trzecia linia tekstu (2 → element 12, D77). Pomiar z emulatora (914 × 411 dp): pasek w części „Drzewo” 64 dp, w części „Mapa” 79 dp.
> [[style-b]] i [[mapa-migracji]] bez zmian (mapa bierze pasek z elementu 12).
>
> **Wersja 1.31 (2026-10-23, `ui` przed planem [[ISSUE-056-tree-lines-readable]]; decyzja autora na prototypie `prototyp-056.html` tego dnia).** Cel z `/pm`:
> **„całe drzewo”** — *„te niebieskie linie się przecinają, przez co łatwo się gubię”*. Sonda na kodzie aplikacji: algorytm liczy 3 / 14 / 26 przecięć, a ekran rysuje
> 9 / 19 / 27 (*Candidates — ISSUE-056*). Autor na panelu 2: *„wybrałbym opcje mostków - łuk, bez osobnych kolorów dla rodzin”* — **mostek łukiem w każdym przecięciu**
> (D83), **piętra szyn według przecięć** (D84 — część tego kandydata), **bez koloru rodziny** (D85), **kolejność w rzędzie bez zmian** (D86 — do potwierdzenia na stopie #1).
> Zmienione: elementy 4 i 8, *AC → element*. [[style-b]] v1.55 (rola linii relacji — mostek).

## Purpose
Zobaczyć rodzinę wokół wybranej osoby i jak się łączy (M9), jak zmieniała się w czasie (M10) i jak dowolne dwie osoby
są spokrewnione (M11). Tak samo zbudowane jest mini-drzewo w [[osoba]] (element 6).

## Navigation
- **Zakładka „Drzewo”** w dolnym pasku. **Każde wejście z paska zaczyna od „Ja”** w skali 1 (AC-1), **na wybranym poziomie** — przy pierwszym
  uruchomieniu aplikacji poziom 1 („Linia krwi”), potem ten, który wybrałeś, dopóki aplikacja działa, jak tempo (v1.23, D57; do v1.22 — zawsze poziom 2).
  Drzewo nie pamięta poprzedniego środka (v1.5, D15). Wejście z paska otwiera część „Drzewo”; **„Pokaż na mapie”** w [[osoba]] 9a — część „Mapa” z tą osobą w środku (v1.20,
  [[mapa-migracji]] *Navigation*). Przełącznik w pasku zmienia część bez zmiany osoby w środku, roku, tempa i ▶ (v1.20).
- **„Pokaż w drzewie”** w [[osoba]] (element 6) → zakładka Drzewo z tą osobą w środku, na wybranym poziomie, w skali 1 (v1.23; do v1.22 — poziom 2). Działa jak dotknięcie „Drzewo” w pasku
  ([[style-b]] reguła 12): stos widoku osoby znika, a wstecz z drzewa wraca na mapę (v1.5, D15). Także z widoku osoby otwartego z drzewa —
  drzewo zaczyna od nowa, z tą osobą w środku (v1.7, D15).
- **Dotknięcie osoby → ona staje w środku**; dotknięcie osoby w środku albo „Pokaż” w karcie → [[osoba]] (zakładka Drzewo
  zostaje aktywna). Wstecz z widoku osoby wraca do drzewa z tym samym środkiem, poziomem i skalą.
- **Ikona „Przesyłaj na telewizor”** w pasku (v1.10, D30) → **systemowy ekran przesyłania** (ustawienia telefonu, nie ekran aplikacji) → po powrocie
  (wstecz albo wybór telewizora i wstecz) **tryb prezentacji** (element 11). Telefon bez tego ekranu → od razu tryb prezentacji z podpowiedzią (D26).
  Wstecz albo „Zakończ prezentację” wraca do drzewa (US-009). Do v1.9 ikona telewizora otwierała sam tryb prezentacji. **Powrót** to chwila, gdy
  aplikacja znów ma fokus po ekranie systemu, a nie gdy była schowana (v1.11, D30 a). Home z ekranu systemu i powrót do Grobinga pokazuje znowu
  ekran systemu (to samo zadanie); tryb włącza dopiero wstecz.
- **Ikona „Połącz dwie osoby”** w pasku → okno z dwoma kaflami (7) → kafel → lista „Od kogo?” / „Do kogo?” (tryb wyboru jak „Która osoba to Ty?”, bez
  dolnego paska — [[style-b]] reguła 12) → wybór „Od” wraca do okna, a wybór „Do” zamyka okno i wraca **na drzewo**, z animacją ścieżki (v1.1, D26). **„Od” to osoba w
  środku i w nim zostaje** (v1.29, D78, D81; do v1.28 „Od” — „Ja”, a „Do” stawał w środku — D45). Ścieżkę kończy **wstecz**, przełącznik „Drzewo · Mapa”, „Przesyłaj na
  telewizor”, nowe „Do” i zmiana danych drzewa; dwa palce, przeciąganie i podwójne dotknięcie zmieniają tylko widok, a dotknięcie osoby nic nie robi (v1.29, D79; do v1.28
  kończyło ją każde działanie na drzewie — D49). Po wyjściu suwak wraca na rok sprzed ścieżki (D81). Wstecz w oknie, „Anuluj” albo dotknięcie poza oknem zamyka okno bez zmian.
- **Poziom i skala** (v1.23, D51, D55, D57): zostają przy przestawieniu środka, powrocie wstecz z widoku osoby i przejściu do trybu prezentacji i z powrotem. Zmienia je
  tylko + / − poziomu (3; do v1.24 przełącznik z listą), gesty (3a) oraz ścieżka „Połącz dwie osoby” (8 — poziom tylko w górę).
- **Rok na suwaku** (US-010, v1.12, D37): zostaje przy przestawieniu środka, zmianie poziomu i powrocie wstecz z widoku osoby; wejście z paska i „Pokaż w drzewie”
  pokazują „dziś”, a ścieżka „Połącz dwie osoby” przestawia na „dziś” i zatrzymuje ▶ (v1.16, Y1 — D48), a po wyjściu z niej wraca rok sprzed ścieżki (v1.29, D81). **Tryb prezentacji** (v1.14, Z2 — D42): rok przechodzi do trybu i wraca z niego, tak jak osoba w środku; ▶ stoi, bo po drodze był ekran systemu. Do v1.13
  tryb zawsze pokazywał „dziś”.
- **Tempo** (v1.14, D41): wybrane tempo zostaje, dopóki aplikacja działa — w karcie i w trybie prezentacji to samo; po zamknięciu aplikacji wraca „Średnio”.
- **⏭ „Następne”** (v1.26, ISSUE-050 — element 6a): z „dziś” prowadzi do pierwszego zdarzenia (jak ▶ z „dziś” zaczyna od początku suwaka — D34), dalej do najbliższego
  późniejszego roku ze zdarzeniem; po ostatnim — „dziś” z podpisem końca, a następne dotknięcie zaczyna od początku (D67). Zatrzymuje ▶ (Z1 — D62) i kończy podświetlenie
  „Połącz dwie osoby”, jak suwak (D49). **Podpis roku** zostaje, dopóki rok stoi; znika przy zmianie roku (suwak, ▶), poziomu i części („Drzewo” · „Mapa”) oraz przy ścieżce
  „Połącz dwie osoby” (rok „dziś” — D48); dotknięcie osoby, przybliżanie i przesuwanie go nie zabierają; przechodzi z rokiem do trybu prezentacji i z niego wraca (jak rok — Z2,
  D42; D69).
- **„Obróć”** (v1.29, D82) w pasku drzewa i mapy → ekran poziomo, w układzie 12; w poziomie → pionowo. Wybór trzyma, dopóki jesteś w zakładce Drzewo (obie części; tryb
  prezentacji po wyjściu wraca do niego); widok osoby, inne zakładki i wyjście z drzewa idą za ustawieniem obracania w telefonie, a powrót do drzewa — znowu za wyborem.
  Po zamknięciu aplikacji wyboru nie ma. Ścieżki nie kończy.
- **Bez „ja”:** „Wybierz, która osoba to Ty” → wybór „ja” ([[osoby]] 6–7) → po wyborze z powrotem na drzewie, z tą osobą w środku (D19).

## Elements in order
**Tryb „Drzewo”** — US-009, poza elementem 6 (US-010)

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Od v1.20 (W2, [[ISSUE-045-migration-map]]): zamiast tytułu przełącznik segmentowy „Drzewo” · „Mapa”** (`account_tree_outlined` · `public_outlined` — v1.21, wysokość 40 dp, cel 48 dp, aktywna część z obrysem 2 dp i ikoną w akcencie jak segment z R3; czytnik „Drzewo, zaznaczone” / „Mapa”; przy tekście ≥ 150% same ikony z `tooltip`, gdy napisy nie mieszczą się w pasku części „Drzewo” — ten sam kształt w obu częściach, v1.21) — szczegóły i część „Mapa”: [[mapa-migracji]] 1. Do v1.19: pasek „Drzewo” (20 sp, półgruby). Po prawej ikony **bez podpisu** (v1.1): **„Przesyłaj na telewizor”** (`cast_outlined`, akcent, cel 48 dp, `tooltip` „Przesyłaj na telewizor”, czytnik: „Przesyłaj na telewizor — w ustawieniach telefonu” — **US-009**, v1.10, [[ISSUE-036-cast-from-the-app]]; **zastępuje** `tv_outlined` „Tryb prezentacji” z v1.5 — D30; drugie dotknięcie, zanim otworzy się ekran systemu, nic nie robi, a ikona się nie zmienia — v1.11, D30 b) i na lewo od niej **„Połącz dwie osoby”** (`link_outlined` — A1, v1.16, D44; akcent, cel 48 dp, `tooltip` i czytnik „Połącz dwie osoby” — **US-011**). W stanach bez drzewa (bez „ja”, pusta baza) ikon nie ma; ~~„Połącz dwie osoby” nie ma też na drzewie z „Pokaż w drzewie”, gdy „ja” nie jest wybrane~~ (v1.16, D3 planu [[ISSUE-039-connect-two-people]]) — **od v1.29 jest przy każdym drzewie** (D78: okno zaczyna od osoby w środku, baner bez „ja” ma dwie linie — D47). **Od v1.29 (D82):** na lewo od „Połącz dwie osoby” — **„Obróć”** (`screen_rotation`, akcent, cel 48 dp, `tooltip` i czytnik „Obróć poziomo” / „Obróć pionowo”), także w części „Mapa”. Z trzema ikonami przełącznik może stracić napisy na wąskim ekranie przy tekście 100% — reguła z [[mapa-migracji]] 1 (same ikony, gdy napisy się nie mieszczą); `dev` mierzy na 360 dp, telefon autora ma 412 dp. **W poziomie** ikony i przełącznik stoją w górnym rzędzie nad drzewem (12, D77) | pasek + przyciski-ikony | → systemowy ekran przesyłania → po powrocie tryb prezentacji (11) · → okno wyboru (7) · „Obróć” → poziomo (12) / pionowo | — | — | R3 · **decyzja autora** (D26, D11; stop #2 ISSUE-034 — „jak w YouTube”) · AC-8 · D29 |
| 2 | ~~Legenda linii~~ — **bez legendy** (v1.1, D25). Rodzaj linii niesie kształt i styl (łamana z góry — rodzic–dziecko; pozioma ciągła — małżeństwo; przerywana — razem), więc kolor nie jest jedynym nośnikiem (SC 1.4.1) | — | — | — | — | **decyzja autora** (D25) |
| 3 | **Poziom — kogo pokazać** (v1.23, D50, D53; zastępuje S2 i D2 — do v1.22 poziom zmieniało oddalanie, próg za progiem, a poziom 1 to byli rodzice, partnerzy i dzieci): **poziom = 1 + liczba związków na drodze od osoby w środku** — krew nic nie kosztuje, każdy związek (małżeństwo albo „razem”) to poziom wyżej. **Poziom 1 „Linia krwi”** — krewni osoby w środku (przodkowie i wszyscy ich potomkowie: rodzeństwo, kuzyni, ich dzieci — wspólny przodek, jak w KRO art. 617) **z mężami, żonami i partnerami** każdego z nich, bez ich rodzin (M2). **Poziom k + 1** — dla każdego męża, żony i partnera spoza krwi z poziomu k: jego krewni z ich mężami, żonami i partnerami. Np. od „Ja”: poziom 1 — brat Michał, jego partnerka Natalia i syn Leon; 2 — rodzice i siostra Natalii z mężem Konradem; 3 — rodzice Konrada. Liczba poziomów zależy od osoby w środku (od „Ja” w makiecie trzy: 91 → 113 → 116 osób). **Przełącznik (v1.25, D58; do v1.24 — etykieta „Linia krwi ▾” z listą „Kogo pokazać na drzewie”, P2 — D53):** **+ / −** w prawym dolnym rogu drzewa, 12 dp od krawędzi, + nad −, 8 dp odstępu — tam, gdzie do v1.24 stały + / − przybliżania (48 dp, powierzchnia z obrysem, ikona w kolorze tekstu, nie rośnie z tekstem): **+** — następny poziom (dalsza rodzina), **−** — poprzedni (bliższa); jedno dotknięcie = jeden poziom. **Na krańcach nieaktywne:** − na „Linii krwi”, + na najwyższym poziomie osoby w środku — **bez obrysu**, ikona w kolorze tekstu pomocniczego (rola „nieaktywne”, [[style-b]] *Token roles*; kształt, nie sam kolor — SC 1.4.1, przegląd `ui` rundy 2), dotknięcie nic nie robi, czytnik mówi „niedostępne”. Bez napisu między przyciskami (stare „− Poziom 2 +” autor uznał za nieestetyczne — [[SPIKE-004-mvp-flow-prototype]] D25): nazwę poziomu mówi pigułka po każdej zmianie. `tooltip` „Dalsza rodzina” / „Bliższa rodzina”. **Nazwy (N2, D54):** „Linia krwi” · „Przez 1 związek” · „Przez 2 związki” · „Przez 5 związków” (odmiana liczby jak [[style-b]] reguła 6). **Po zmianie (K1, D55):** skala bez zmian, osoba w środku w tym samym miejscu ekranu; dochodzące osoby się pojawiają, odchodzące gasną (jak przestawienie środka, element 4); **pigułka** u góry drzewa na ok. 1,8 s: „Przez 1 związek · 113 osób (+22)” (13 sp, powierzchnia; czytnik czyta ją jako region na żywo; liczba jak D37 — osoby, które w roku suwaka już są); **w trybie prezentacji także** (v1.25, D58; w v1.24 bez pigułki) — pod górnym rzędem sterowania, 68 dp od góry, bo bez etykiety tylko pigułka mówi, który poziom widać (element 11). Pigułka w dwóch liniach jest szeroka jak dłuższa linia, a nie jak cały rząd (przegląd `ui` rundy 2). **Osoba w środku ma mniej poziomów** niż wybrany (np. osoba bez rodziny): drzewo pokazuje jej najwyższy, a + jest nieaktywne (przy jednym poziomie oba); wybór wraca przy osobie, która go ma (D57). Czytnik: „Dalsza rodzina”, „Bliższa rodzina” — przyciski, na krańcach „niedostępne”; po zmianie czyta pigułkę (region na żywo) | przycisk-ikona ×2 + pigułka | + / − | 1 przy pierwszym uruchomieniu, potem wybrany (D57) | — | **decyzja autora** ([[ISSUE-049-tree-levels-and-zoom]]: *„niezależne względem siebie funkcjonalności”*) · AC-2, AC-3 (ISSUE-049) · D50, D53–D55, D57 · **D58 — decyzja autora na stopie #2** |
| 3a | **Przybliżanie i oddalanie — sam widok** (v1.23, D51; zastępuje S2): **dwa palce** (przybliżają i oddalają) i **podwójne dotknięcie pustego miejsca** (przybliża ×1,45) zmieniają tylko skalę; **przycisków przybliżania nie ma** (v1.25, D58 — decyzja autora; do v1.24 + / − w prawym dolnym rogu, ×1,45 — dziś zmieniają poziom, element 3), więc **oddalają tylko dwa palce** ([[style-b]] v1.46 — wyjątek od SC 2.5.1) — **skład osób się nie zmienia**. **Zakres:** od skali, w której **cały pokazany poziom mieści się w obszarze drzewa** (24 dp marginesu; dolna granica najwyżej 0,4 i najmniej 0,08 — od „Ja” na poziomie 1 ok. 0,12), do 2,0. Gdy po zmianie poziomu albo osoby w środku dolna granica wypada nad bieżącą skalą, skala rośnie do niej. **Na dolnej granicy cały poziom stoi na środku obszaru drzewa** (v1.24, odstępstwo 1 ISSUE-049): po geście dwóch palców po 0,4 s spokoju (jak powrót z D21), a także gdy skala rośnie do nowej granicy po zmianie poziomu, osoby w środku albo obszaru (np. wejście w tryb prezentacji) — wtedy osoba w środku nie zostaje w swoim miejscu ekranu, bo widać cały poziom (K1 dotyczy skali nad granicą). Ze ścieżką „Połącz dwie osoby” bez centrowania — kadr ścieżki (8). Do v1.23 granica nie mówiła, gdzie stoi drzewo: − od „Ja” zostawiało je w bok, z osobą uciętą przy krawędzi (89 z 91 na ekranie). **Dotknięcie przy małym drzewie** (D52): gdy miejsce osoby na ekranie (miejsce × skala) ma mniej niż 24 dp, dotknięcie drzewa — osoby albo pustego miejsca — **przybliża w to miejsce do skali 0,45** (ok. 0,35 s, przy ograniczeniu animacji od razu) i nikogo nie stawia w środku; od 24 dp — jak w elemencie 4. Czytnik: węzeł osoby przy celu < 24 dp ma działanie „przybliż” zamiast „w środek” | gest | dwa palce · podwójne dotknięcie · dotknięcie przy małym drzewie | skala 1 | — | **decyzja autora** (ISSUE-049) · AC-1 (ISSUE-049) · D7 · D51, D52, D58 |
| 4 | **Drzewo**: rzędy według pokolenia (wyżej starsze), osoba w środku z pierścieniem w akcencie; rodzeństwo z boku osoby, po stronie dalszej od partnera; **rodzina partnera po prawej**, bez przeplatania z krewnymi. Węzeł 44 dp (profilowe albo inicjały), imię 13 sp półgrube (v1.2, D10); **zmarły ma znicz** w rogu węzła ([[style-b]] reguła 8, R3); zmarły = zapisany zgon albo pochówek, z datą albo bez (v1.7, D22). Linie: **rodzic–dziecko** — kolor relacji rodzic–dziecko, łamana z góry w dół; **małżeństwo** — kolor partnerów, ciągła, pozioma; **razem (bez ślubu)** — kolor partnerów, przerywana 5/4. **Koniec związku** (v1.12, E3 — D35): od roku końca dwie ukośne kreski „//” przez środek linii pary (kolor partnerów, 2 dp, ok. 12 × 12 dp), także na „dziś”; koniec bez daty — tylko na „dziś”; linia do dzieci zostaje. **Szyny rodzic–dziecko** (v1.31, D84): od pary (albo spod samotnego rodzica) kreska w dół do poziomej szyny nad dziećmi i z niej do każdego dziecka; szyny, które zachodzą na siebie w jednej przerwie między rzędami, stoją na osobnych piętrach co 7 dp (najwyżej 4), a **piętro wybiera najmniejsza liczba przecięć**. **Mostek** (v1.31, D83): gdzie pionowa kreska jednej rodziny przechodzi przez szynę innej, kreska przeskakuje ją łukiem — półelipsa 4 dp w prawo, 4 dp nad i pod szyną, w kolorze i grubości kreski; szyna zostaje ciągła; kolejne przecięcia bliżej niż 8 dp — jeden łuk nad wszystkimi. **Ślad dalszej rodziny** (v1.3, D9): osoba z rodziną poza widokiem (v1.23: poza wybranym poziomem, np. rodzice Natalii na poziomie 1) dostaje krótką przerywaną kreskę 3/3, 14 dp, w kolorze relacji o kryciu 60% — w górę rodzice, w dół dzieci, w bok partner, **na zewnątrz od środka** (na lewo od osoby w środku — w lewo, na prawo i u niej samej — w prawo; v1.7, przegląd `ui` ISSUE-033: zawsze w prawo celował u osób po lewej w środek i mylił się z linią „razem”). Przewijanie w obu osiach, środek ustawia się na osobie. **Drzewo nie ucieka z kadru** (v1.7, D21): gdy w kadrze nie ma nikogo, widok wraca płynnie (ok. 0,35 s) do osoby w środku, a palec na ekranie przerywa powrót; nowy rozmiar obszaru drzewa przed pierwszym dotknięciem ustawia środek od nowa. **„Ja”** (v1.5, D14): okrąg ze znakiem „Ja” (inicjały „Ja” w akcencie, obrys w kolorze obrysu, także przy profilowym — jak [[osoby]] D4), podpis „Ja”; pierścień i poświatę w akcencie ma tylko osoba w środku. **Przestawienie środka** (AC-2, v1.5): węzły przesuwają się na nowe miejsca w ok. 0,45 s, nowe osoby się pojawiają, odchodzące gasną, a widok jedzie tak, że nowa osoba staje w środku (ok. 42% wysokości obszaru drzewa). Przy systemowym ograniczeniu animacji — od razu (SC 2.3.3, jak D5). **Imiona przy oddalaniu** (v1.6, I2 — decyzja autora; potwierdzona w v1.9, D27): przy skali < 1 imię nie maleje — na ekranie ma 13 sp × skala tekstu, na tabliczce w kolorze tła (zaokrąglona 4 dp, 3 dp z boków; v1.7, D23); gdy dwa imiona by się nałożyły, zostaje to bliżej osoby w środku (najpierw liczba kroków w rodzinie od osoby w środku — rodzic, partner, dziecko, rodzeństwo, czyli dawne poziomy D2; potem odległość w poziomie — v1.23, D57: poziom o tym nie decyduje, bo na poziomie 1 bywa 91 osób), a reszta chowa się do przybliżenia. **Osoba z widocznym imieniem leży nad sąsiadami** (v1.24, odstępstwo 2 ISSUE-049; [[style-b]] reguła 13, v1.45): przy oddaleniu imię 13 sp jest szersze niż kilka okręgów, a okręgi rysowane po nim cięły litery („Wiktoria”, „Stanisław”) — teraz tabliczka zakrywa okręgi pod sobą. **Wieniec rodu** (v1.18, [[wieniec]] D): pod węzłem osoby z rodem — płótno 88 dp, węzeł w jego (0,50; 0,434), skaluje się z drzewem; rysowanie: linie → wieńce → węzły → znicz, a **wieniec należy do węzła** (v1.19): w węźle wieniec → tabliczka imienia → okrąg z pierścieniem, poświatą i zniczem, więc gaśnie i wyszarza się razem z osobą (element 8) bez osobnego krycia; poza czytnikiem. **Gdy ktoś w rodzinie ma wieniec** (całe drzewo w bazie, nie tylko pokazane — v1.19), **miejsce osoby ma 96 dp** zamiast 80 (`max(96, 80 × skala tekstu)`, najwyżej 160 dp), a **ślad w bok osoby z wieńcem zaczyna się za wieńcem**, 43 dp od środka węzła (osoby bez wieńca — przy okręgu). **Tekst systemu** (AC-7, v1.5): miejsce osoby 80 dp × skala tekstu, najwyżej 160 dp (jak mini-drzewo, [[osoba]] v2.2); rząd rośnie z podpisem (104 dp → 124 dp przy 200%); inicjały najwyżej 1,3×; imię w jednej linii, „…” dopiero poza miejscem osoby (przy 100% to ok. 10 liter, także przy oddaleniu — v1.7, D24). **Cel dotyku** = miejsce osoby × skala drzewa (D17); poniżej 24 dp dotknięcie przybliża (element 3a, v1.23, D52). **Czytnik:** „Zofia Wymyślona, 1928–2010, Moja babcia — w środek” (v1.9, G2 — ten sam tekst co karta, D28), osoba w środku „… — otwórz”; kolejność rzędami, z góry i od lewej; linie i ślad poza czytnikiem | drzewo | dotknięcie → osoba w środek; drugie → [[osoba]] | „Ja” | — | R3 · D1, D3, D4, D9 · AC-1, AC-2, AC-4, AC-7 · D14, D17 |
| 5 | **Karta osoby w środku** (dolny arkusz, powierzchnia; v1.5): okrąg 40 dp z pierścieniem w akcencie (profilowe w kadrze albo inicjały; „ja” — znak „Ja”) · **imię i nazwisko** z „z d.” (16 sp, półgruby, tekst, do dwóch linii) · pod spodem **lata · kim jest dla mnie** (14 sp, tekst pomocniczy, **zawija się, bez ucinania**): nazwa ze słownika, z nawiasem tam, gdzie słownik go ma („1928–2010 · Moja babcia”, „ur. 1951 · Mój stryj (brat taty)”, „Moje rodzeństwo” przy osobie bez płci), a dalej opis z odcinków („1925–2010 · Siostra cioteczna mojego dziadka”, „Siostra cioteczna babci mojej żony”; D12, D13; **mówisz Ty — G2, v1.9, D28**). „Ja”: „ur. 1983 · to ja”. Bez ścieżki do „ja”: „… · nie wiadomo jeszcze, kim jest dla mnie”. Zaimek zawsze z małej litery w środku opisu („…babci mojej żony”), z wielkiej tylko na początku nazwy („Moja babcia”). Bez „ja” (wejście z „Pokaż w drzewie”): same lata. Po prawej przycisk tekstowy „Pokaż ›” (akcent, cel 48 dp); **przy tekście systemu ≥ 150% „Pokaż ›” przechodzi pod tekst, do prawej** (D20) | karta | „Pokaż” → [[osoba]] | — | — | D1 · AC-2, AC-5 · D12, D13, D20 |
| 6 | **US-010. Czas (M10; v1.12 — [[ISSUE-037-time-on-the-tree]]):** w karcie (5), pod imieniem i opisem, jeden rząd: **▶ / ❚❚** (okrąg 36 dp w akcencie, ikona `play_arrow` / `pause` w kolorze tła, cel 48 dp, `tooltip` „Odtwórz historię” / „Zatrzymaj”) · **⏭ „Następne”** (v1.26, ISSUE-050 — element 6a: `skip_next` w akcencie, bez wypełnienia, cel 48 dp, zaraz za ▶) · **rok początku** (13 sp, tekst pomocniczy; **v1.26, U3 — tylko przy tekście ≥ 150%**: przy mniejszym w karcie go nie ma, zostaje na listwie trybu prezentacji i w czytniku — D65) · **suwak** (`Slider`: aktywny tor i uchwyt w akcencie, tor nieaktywny w kolorze obrysu, wysokość 48 dp, krok 1 rok) · **rok** (16 sp, półgruby, akcent, cyfry o stałej szerokości; na końcu suwaka „dziś”) — w stałym miejscu na szerokość najszerszego z „dziś” i „8888”, żeby tor suwaka nie zmieniał długości pod palcem (v1.13, odstępstwo 2 ISSUE-037) · **tempo** (v1.14, V2 — D41): przycisk tekstowy z nazwą tempa, „Średnio” (14 sp, waga 500, kolor tekstu — stoi obok wypełnionego ▶, [[style-b]] reguła 1; cel 48 dp, `tooltip` i czytnik „Tempo historii: średnio — zmień”) — na szerokość najszerszego słowa („Średnio”), słowo na środku, żeby tor suwaka nie zmieniał długości przy przełączaniu (v1.15, odstępstwo 3 ISSUE-038; [[style-b]] reguła 5). Dotknięcie przełącza „Wolno” → „Średnio” → „Szybko” → „Wolno”; w trakcie ▶ odtwarzanie biegnie dalej od bieżącego roku w nowym tempie. Przy tekście 100% suwak jest przez to krótszy: 129–137 dp zamiast 193 dp (makieta, ekran 360 dp). **v1.26 (U3):** z ⏭ i bez roku początku — ok. 110 dp, tor Fluttera ok. 62 dp (D65). **Domyślnie „dziś”** — drzewo jak w US-009: nic nie znika i nic nie jest przerywane. **Początek suwaka** (T2, D34): pełna dekada przed najwcześniejszą datą urodzenia w bazie, najpóźniej 1880. **Rok Y** (AC-1, AC-2): osoba, która w roku Y jeszcze się nie urodziła, znika razem ze swoimi liniami i imieniem, a jej miejsce zostaje (układ liczony jak na „dziś”, rok go nie zmienia); nie jest celem dotyku i nie ma jej w czytniku. Zmarły do Y ma znicz. Para: do początku związku bez linii, od początku przerywana „razem”, od ślubu ciągła; **związek bez daty** — od urodzenia najstarszego wspólnego dziecka, a bez dzieci — od 20. roku życia młodszego z pary (D31); koniec związku — „//” (element 4, E3). **Data niepewna i brak daty** (N3, D32): każda data ma okno [najwcześniej, na pewno]. Osoba pojawia się na początku okna urodzenia i do jego końca ma **przerywany obrys okręgu** (2 dp, kreska 4/3, kolor obrysu; u osoby w środku pierścień w akcencie przerywany). W oknie śmierci — ten sam obrys, a znicz dopiero na końcu okna. Okno: dokładnie Y — Y; „ok. Y” — Y−5 … Y+5; „między A a B” — A … B; „przed Y” — najwcześniej z rodziny … Y; „po Y” — Y … na pewno z rodziny; brak daty — oba końce z rodziny (D32). **Osoba w środku przed narodzinami** (C1, D33): pusty pierścień w akcencie w jej miejscu, bez okręgu, imienia i znicza; karta bez zmian. **▶** (AC-3): od początku suwaka (albo od bieżącego roku, gdy to nie „dziś”) do „dziś”, **w wybranym tempie** (v1.14, D41): „Wolno” 5, „Średnio” 10, „Szybko” 20 lat na sekundę, czyli od 1880 do dziś ok. 29 · 15 · 7 s (do v1.13 stale ok. 21 lat/s); osoby pojawiają się i gasną przenikaniem 150 ms — w trakcie ▶ najwyżej do następnego roku (przy „Wolno” pełne 150 ms, przy „Średnio” ok. 100 ms, przy „Szybko” ok. 50 ms), pełne 150 ms przy przesuwaniu suwaka palcem (v1.13, odstępstwo 4 ISSUE-037; *Obali:* autor widzi miganie osób przy ▶ — wtedy przenikanie od roku narodzin, bez przerywania); na „dziś” ▶ się zatrzymuje, a czytnik raz ogłasza rok („Rok 1923”, „dziś”) — także po ❚❚. ❚❚ zatrzymuje na bieżącym roku; przeciągnięcie suwaka też zatrzymuje. **Ograniczenie animacji** (R2, D36): ▶ przeskakuje o pełną dekadę, osoby pojawiają się od razu, bez przenikania; odstęp skoków daje tempo — co ok. 2 · 1 · 0,5 s (v1.14, D41). **Tekst ≥ 150%** (D20): rok początku i rok w rzędzie nad suwakiem (po lewej i po prawej), **tempo między nimi** (v1.14 — suwak bez zmian, 278 dp przy 200%; v1.26 — 222 dp z ⏭), ▶, ⏭ (v1.26) i suwak w rzędzie pod nimi. Gdy trzy się nie mieszczą (telefon węższy niż 360 dp albo szerszy krój), rok przechodzi do następnej linii, na lewo, zamiast się uciąć; na 360 dp przy 200% w Roboto stoją w jednej linii (v1.15, odstępstwo 2 ISSUE-038). **Czytnik:** ▶ „Odtwórz historię” / „Zatrzymaj”; suwak „Rok” z wartością „1923” albo „dziś”, zwiększanie i zmniejszanie o 10 lat (krok co rok to do 166 gestów); w trakcie ▶ rok nie jest ogłaszany co zmianę, po zatrzymaniu — tak. Osoba z przerywanym obrysem: do opisu z elementu 4 dochodzi „nie wiadomo, czy już żyje” (okno urodzenia) albo „nie wiadomo, czy jeszcze żyje” (okno śmierci); pusty pierścień: „… — przed narodzinami” | suwak + przycisk ×2 | przeciągnięcie · ▶ / ❚❚ · tempo | dziś · „Średnio” | — | R3 (suwak) · **decyzja autora** (D20) · D4 · AC-1–AC-3 · D31–D37 · D41 (ISSUE-038) |
| 6a | **ISSUE-050. „Następne” i podpis roku (v1.26):** **⏭** w rzędzie czasu karty (6) i na listwie trybu prezentacji (11), w obu zaraz za ▶: ikona `skip_next` (Material Symbols Rounded — do dodania do fontu ikon aplikacji, [[style-b]] reguła 3; przycisk z samą ikoną, 24 dp) w akcencie, **bez wypełnienia** — ▶ zostaje jedynym wypełnionym ([[style-b]] reguła 1); cel 48 dp, `tooltip` i czytnik „Następne zdarzenie” (D71). **Dotknięcie:** suwak przeskakuje do najbliższego **późniejszego** roku ze zdarzeniem — z „dziś” do pierwszego zdarzenia, jak ▶ z „dziś” (D34, D67); ▶, jeśli biegło, staje (Z1 — D62). **Zdarzenia (K1, N1 — D59, D60, D68):** osób z **wybranego poziomu** (3) — narodziny, śmierć, „razem” (początek związku bez ślubu albo przed ślubem) i ślub, w roku zapisanym w dacie; związek tylko, gdy obie osoby są na poziomie. „ok. 1870” w 1870, „między 1895 a 1900” w 1895, „przed 1900” i „po 1945” w roku z daty. **Data bez roku nie jest zdarzeniem** — okna z D31, D32 służą tylko obrysowi, aplikacja dat nie zgaduje. Koniec związku nie jest zdarzeniem w podpisie (D68). **Podpis roku — telefon:** dymek u góry obszaru drzewa, 10 dp od góry i 16 dp od boków (miejsce pigułki poziomu i baneru), powierzchnia, zaokrąglony 12 dp: nagłówek „W 1952” (13 sp, półgruby, tekst pomocniczy; przy dwóch stronach „W 1955 · 1 z 2”), pod nim zdarzenia (14 sp, tekst, imiona półgrube); zawija się. **Podpis roku — tryb prezentacji (v1.28, B — D72; v1.26–v1.27 pod rokiem w rogu, 28 sp — D64):** **drobna linia na listwie** (11), nad rzędem ▶ ⏭, od lewej krawędzi ▶, na całą szerokość listwy: nagłówek „W 1955 · 1 z 2” (13 sp, półgruby, tekst pomocniczy), 12 dp odstępu, zdarzenia strony w jednym akapicie, rozdzielone „ · ” (14 sp, tekst, imiona półgrube; twarda spacja po „·” — [[style-b]] reguła 6), na końcu „ · Jeszcze 2 w tym roku” (tekst pomocniczy); zawija się, bez ucinania. Na końcu historii: „Dziś”, odstęp, „To wszystkie zdarzenia z datą.”. Listwa jest po ⏭ 5 s, jak po każdym dotknięciu (D40), i znika razem z linią; pusty dotyk pokazuje ją znowu z tą samą linią, dopóki stoi podpis (D69). Linię czyta autor z telefonu w ręce; rodzina z kanapy widzi rok w rogu i świecące osoby (D73). Pod rokiem nic nie stoi. Rok w rogu jest widoczny, dopóki stoi podpis — także „dziś” na końcu. **Linia zdarzenia (F1 — D61):** „Urodził się **Jan Wymyślony**” · „Urodziła się **Maria Zmyślona**” · osoba bez płci „Urodził(a) się …” · „Zmarł …” / „Zmarła …” / „Zmarł(a) …” · „Ślub: **Maria Zmyślona** i **Piotr Wymyślony**” · „Razem: … i …”; data niepewna — dopisek na końcu: „(ok. 1870)”, „(między 1895 a 1900)”. Imię i nazwisko jak w karcie, **bez „z d.”**; w parze kobieta pierwsza (jak w AC-1), poza tym kolejność zapisu. Imię z nazwiskiem i dopisek trzymają się razem (twarde spacje), więc linia łamie się przed „ i ” i przed dopiskiem ([[style-b]] reguła 6). **Czasownik trzyma „się”** (v1.27, odstępstwo 3 ISSUE-050): „Urodził się”, „Urodziła się”, „Urodził(a) się” z twardą spacją przed „się”, więc linia nie zaczyna się od „się Jan…”. **Kolejność w roku:** śluby i „razem”, narodziny, śmierć; w grupie według daty, potem imienia. **Najwyżej 4 zdarzenia naraz** (D66): gdy w roku jest więcej, ostatnia linia mówi „Jeszcze 3 w tym roku” (tekst pomocniczy), a następne ⏭ pokazuje dalszy ciąg **tego samego roku**. **Po ostatnim zdarzeniu** ⏭ → „dziś” i podpis „To wszystkie zdarzenia z datą.” (na telefonie nagłówek „Dziś”); następne ⏭ zaczyna od pierwszego (AC-4, D67). **Widok (V2 — D63):** gdy ktoś z podpisu (z bieżącej strony) jest poza obszarem drzewa, który zostaje bez podpisu, widok jedzie tak, że cała grupa stoi **8 dp pod podpisem** (w trybie prezentacji — pod tabliczką roku, nad listwą z linią podpisu; v1.28), w poziomie na środku tego obszaru (v1.27, odstępstwo 2 ISSUE-050; v1.26: „na środku tego obszaru”), ok. 0,45 s, jak przestawienie środka (element 4; przy ograniczeniu animacji — od razu). Grupa za szeroka — pierwsza osoba i tak w obszarze; ktoś stanąłby na + / − w rogu (telefon) — grupa przesuwa się w lewo, dopóki pierwsza osoba się mieści; grupa za wysoka — rząd pierwszej osoby u góry obszaru; **skala i osoba w środku się nie zmieniają**; gdy wszyscy są na ekranie, nic się nie rusza. **Trwanie (D69):** podpis zostaje, dopóki rok stoi, bez odliczania czasu; znika przy zmianie roku (suwak, ▶), poziomu (3), części (1) i przy ścieżce „Połącz dwie osoby” (8 — rok „dziś”); dotknięcie osoby, przybliżanie i przesuwanie go nie zabierają; przechodzi z rokiem do trybu prezentacji i z niego wraca — wtedy widok podjeżdża do osób z podpisu jak po ⏭ (V2; v1.28 — przejście `dev`: w trybie prezentacji był tylko pusty pierścień „Ja”, a świecące osoby poza ekranem). **Osoby z podpisu świecą** (v1.28, D73–D75; v1.26–v1.27 bez wyróżniania — D70): osoby ze zdarzeń bieżącej strony, które są na drzewie, dostają **pierścień w akcencie** (2 dp, jak węzły ścieżki — 8) i **poświatę pod okręgiem, a przy wieńcu rodu — pod wieńcem**, więc laur świeci na jej tle ([[style-b]] reguła 2); przy ślubie i „razem” świecą obie osoby i **linia pary w akcencie** (3 dp na ekranie, jak linia ścieżki), która rośnie od pierwszej osoby do drugiej w ok. 0,45 s. **Puls:** trzy łagodne pulsy poświaty po 1,2 s (krycie 0,30 → 0,65 → 0,30), potem stała poświata 0,30, dopóki stoi podpis (D69); następna strona albo następny rok — puls od nowa, na nowych osobach. Przy oddaleniu (skala < 1) poświata ma na ekranie tę samą wielkość — sięga co najmniej 12 dp poza okrąg — jak imię (I2), więc z kanapy widać, gdzie są osoby z podpisu, także przy całym poziomie; pierścień maleje z okręgiem. Osoba urodzona w tym roku dochodzi przenikaniem jak przy suwaku (6) i świeci razem z nim. Osoba w środku zostaje z pierścieniem; gdy jest w podpisie, pulsuje jak inni. Przy ograniczeniu animacji — od razu stała poświata i cała linia pary, bez pulsu (D75). Na telefonie i w trybie prezentacji tak samo (D74). **Brak zdarzeń z datą** na wybranym poziomie — ⏭ nie ma (D71). **Czytnik:** podpis jest regionem na żywo, jak pigułka poziomu — po ⏭ słychać „W 1952: Urodził się Jan Wymyślony. Ślub: …” zamiast osobnego „Rok 1952” | przycisk-ikona + podpis | ⏭ → następny rok ze zdarzeniem (albo dalszy ciąg roku) | — | — | **decyzja autora** (ISSUE-050: *„data i co się w tym roku stało”*, „Następne” obok ▶; cel (a) — 2026-10-19) · AC-1–AC-4 (ISSUE-050) · D59–D71 |
| 11 | **Tryb prezentacji** (AC-8, D11; v1.5, D16): ekran poziomo, na pełnym ekranie (bez pasków systemu i aplikacji, bez karty i + / − poziomu w rogu), **poziom i skala z telefonu, osoba w środku na środku ekranu** (v1.23, D56; do v1.22 — poziom 2 dopasowany do ekranu w obszarze bezpiecznym, margines 24 dp). Skala z telefonu poniżej granicy ekranu poziomego (3a) rośnie do niej, a wtedy na środku stoi cały poziom, nie osoba (v1.24, odstępstwo 1 ISSUE-049). **Wejście (v1.10, P2):** po powrocie z systemowego ekranu przesyłania — **bez podpowiedzi** (przesyłanie właśnie wybrane, a podpowiedź trafiłaby na telewizor). **Tylko gdy telefon nie ma tego ekranu** (ISSUE-036 AC-2) tryb włącza się od razu i na ok. 4 s pokazuje pigułkę u góry, w miejscu pigułki poziomu: „Obraz na telewizor: przesyłanie ekranu w szybkich ustawieniach telefonu” (v1.8, D26 — funkcja, nie nazwa kafelka; twarda spacja po „w”, [[style-b]] reguła 6). Przez te 4 s może przykryć górny rząd, a dotyk przechodzi do osób pod nią (D26). **Dotknięcie osoby** → ona w środku, skala zostaje — **także osoby, która już jest w środku**: widok jedzie do niej, po przeciągnięciu to droga z powrotem; jej widok się nie otwiera, a czytnik nie mówi „otwórz” (v1.8, D25; v1.23 — bez dopasowania poziomu 2). Przy celu < 24 dp dotknięcie przybliża (3a, D52). Przeciąganie przesuwa, **dwa palce przybliżają i oddalają** (AC-4 ISSUE-049, v1.23, D56; do v1.22 bez szczypania, poziom stały — D16); bez podwójnego dotknięcia, bo pusty dotyk pokazuje sterowanie. **Pasy 24 dp przy krawędziach, od których system wysuwa paski, nie przyjmują dotyku** (v1.8, D25). **Dotknięcie pustego miejsca** → **sterowanie** (v1.14, B2 — D40; do v1.13 sam przycisk na 3 s): **u góry przełącznik „Drzewo · Mapa”** na powierzchni (v1.20, W2 — przełączenie zostawia rok, ▶ i tempo, a sterowanie zostaje na 5 s; [[mapa-migracji]] 13) — **na środku miejsca między rokiem a „Zakończ prezentację”**, liczonego od roku w najszerszym zapisie, a gdy napisy się tam nie mieszczą, same ikony (v1.22; [[mapa-migracji]] D24; do v1.21 — na środku ekranu), w prawym górnym rogu przycisk „Zakończ prezentację” (`close` w akcencie + napis w kolorze tekstu, powierzchnia z obrysem, cel 48 dp), a na dole **listwa** na powierzchni (zaokrąglona 16 dp, 24 dp od krawędzi — nad pasami bez dotyku z D25): ▶ / ❚❚, **⏭ „Następne”** (v1.26 — element 6a; po ⏭ nad tym rzędem linia podpisu — v1.28, D72), rok początku, suwak i tempo, te same co w elemencie 6, ale bez roku na końcu, bo rok stoi w rogu; za tempem **− / + poziomu** (T2, v1.23, D56; **v1.25, D58** — te same co w rogu drzewa, element 3; do v1.24 etykieta z listą i − / + przybliżania): 44 dp w celu 48 dp — dotyk przyjmuje cały cel, także 2 dp wokół koła (przegląd `ui` rundy 2) — w kolorze tła z obrysem (listwa jest powierzchnią), na krańcach nieaktywne, bez obrysu. − / + są **tylko na listwie od 560 dp szerokości**, czyli przy telefonie poziomo (v1.24, test `qa` ISSUE-049): z czytnikiem ekranu sterowanie przychodzi od wejścia, zanim telefon się obróci, a na listwie 302 dp rząd czasu z etykietą i − / + przepełniał się o 6,5 dp — do obrotu listwa ma sam czas. Po zmianie poziomu z listwy **pigułka** (v1.25, D58; w v1.24 bez niej): na środku, **pod górnym rzędem sterowania** (68 dp od góry — rząd ma 48 dp także przy 200%), ok. 1,8 s; **z obu stron wcięta jak przełącznik „Drzewo · Mapa”** — o szerokość roku w rogu i 12 dp, więc nie zachodzi na rok także na wąskim telefonie (przegląd `ui` rundy 2: od ok. 720 dp w dół długa pigułka sięgała pod rok). Emulator przy 200%: ekran 914 dp — pigułka od ok. 267 dp, tabliczka roku do ok. 142 dp; ekran 640 dp — pigułka w dwóch liniach od ok. 220 dp, rok do ok. 140 dp (zrzut 33). Sterowanie chowa się po 5 s od ostatniego dotyku albo po czasie z ustawienia systemu „Czas na działanie”, gdy jest dłuższy. Drugi pusty dotyk chowa je od razu. **Z czytnikiem ekranu** (TalkBack, a także Switch Access i Voice Access — wszystko, co ustawia `accessibleNavigation`) sterowanie jest **od wejścia w tryb i nie chowa się wcale**: pusty obszar nie ma węzła semantyki, więc czytnik nie umie go dotknąć, a schowane sterowanie byłoby nie do odzyskania; wyjście — „Zakończ prezentację” albo wstecz (v1.15, odstępstwo 1 ISSUE-038; D40). Podpowiedź, jeśli jeszcze jest, znika (v1.8, D25). Przeciągnięcie suwaka zatrzymuje ▶ (D37), a dotknięcie osoby nie zatrzymuje, tylko stawia ją w środku. Przez te 5 s listwa przykrywa dolny rząd drzewa — także na telewizorze. **Wstecz** też kończy. Po wyjściu — drzewo pionowo, ta sama osoba w środku, **ten sam poziom i skala** (v1.23, D56; do v1.22 — poziom 2, skala 1), **ten sam rok** (Z2 — D42). **Rok na telewizorze** (v1.14, L1 — D39): w lewym górnym rogu, 36 sp, półgruby, akcent, cyfry o stałej szerokości, na tabliczce w kolorze tła (zaokrąglona 8 dp, 6 dp z boków). Stoi **48 dp od lewej krawędzi** (5% szerokości — telewizor może przyciąć brzeg obrazu, D38) i 24 dp od góry. Widać go, gdy rok nie jest „dziś”, zawsze, gdy widać sterowanie, i dopóki stoi podpis roku (v1.26 — element 6a); gdy ▶ dojdzie do „dziś”, napis „dziś” zostaje jeszcze 3 s. Drzewo dopasowuje się tak samo jak bez roku — w makiecie rok nie przykrywa nikogo przy żadnym ze 106 środków na ekranie 914 dp, a na 360 dp przy jednym (*Candidates — ISSUE-038* → *Pomiar*). Rośnie z tekstem systemu najwyżej do 1,3× (47 sp; [[style-b]] *Thresholds*). Czytnik: „Rok 1950” albo „dziś”, w trakcie ▶ bez ogłaszania (jak element 6). **Podpis roku po ⏭ — na listwie** (v1.28, B — element 6a, D72; v1.26–v1.27 pod rokiem w rogu, 28 sp — D64): drobna linia nad rzędem ▶ ⏭, znika z listwą po 5 s; pod rokiem nic nie stoi, a osoby z podpisu świecą (D73). **Wejście z roku Y** (Z2 — D42): tryb pokazuje rok z karty, ▶ stoi. **Tekst 200%** (v1.8, odstępstwo 5 ISSUE-034; v1.9 — I2 zostaje, D27): imiona jak w elemencie 4, więc na ekranie 360 dp imię ma 26 sp przy okręgu ok. 20 dp (skala ok. 0,45), widać 13 z 20 imion, a tabliczki zasłaniają linie między rzędami (zrzut `18b`). Przy I1 byłoby 20 z 20 imion, ok. 11,7 sp (przeliczenie `ui`, v1.9). Na ekranie 914 dp przy 200% widać 17 z 20 imion (makieta ISSUE-038), a przy 100% — 20 z 20 | tryb | dotknięcie osoby · pustego miejsca (sterowanie) · dwa palce · ▶ / ❚❚ · suwak · tempo · − / + poziomu · wstecz | poziom i skala z telefonu · rok z karty | — | **decyzja autora** (D11) · AC-8 · D16 · D25, D26 · D38–D42 (ISSUE-038) · AC-4 (ISSUE-049), D56, D58 |

**„Połącz dwie osoby” na drzewie (M11, v1.1)** — US-011

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 7 | **Okno „Połącz dwie osoby”** (v1.1; v1.16 — D49): okno na środku ekranu, na powierzchni, zaokrąglone 16 dp, tło pod nim przyciemnione; tytuł „Połącz dwie osoby” (18 sp, półgruby); **dwa kafle obok siebie**, między nimi strzałka `arrow_forward` (tekst pomocniczy) — „Od” i „Do”: obrys 1 dp w kolorze obrysu, zaokrąglone 12 dp, cel ≥ 48 dp. W kaflu podpis „Od” / „Do” (13 sp, tekst pomocniczy), okrąg 40 dp (profilowe w kadrze albo inicjały; „ja” — znak „Ja”, D14, z obrysem w akcencie jak na liście [[osoby]], bo w oknie nie ma osoby w środku, z którą by się pomylił — v1.17, przegląd ISSUE-039) i imię z nazwiskiem bez „z d.” (14 sp, zawija się na spacjach, nie w środku słowa). **Pusty kafel:** przerywany okrąg w akcencie z `add` i „Wybierz osobę” (akcent, waga 500 — główne działanie okna, [[style-b]] reguła 1). **Tekst ≥ 150%:** kafle jeden pod drugim, strzałka w dół; w kaflu podpis nad wierszem z okręgiem i imieniem. Na dole przycisk tekstowy „Anuluj” (kolor tekstu). **Każde otwarcie:** „Od” — **osoba w środku drzewa** („Ja”, gdy w środku jesteś Ty; v1.29, D78 — do v1.28 zawsze „Ja”), „Do” — pusty. Kafel → **lista „Od kogo?” / „Do kogo?”** na cały ekran — ta sama lista co w [[osoby]] (wyszukiwarka „Szukaj osoby”, A–Z, karty z okręgiem, imieniem z „z d.” i latami; tryb wyboru jak „Która osoba to Ty?”, bez dolnego paska), **bez osoby z drugiego kafla**. **W poziomie** (12) lista zostaje pozioma, jak wybór „Obróć” — to tryb wyboru z drzewa; otwiera się bez kursora w polu, więc A–Z widać od razu, a przy pisaniu klawiatura zakrywa wyniki: pokazuje je klawisz szukania na klawiaturze albo jej schowanie (v1.30, odstępstwo 1 ISSUE-055, D77). Wybór „Od” wraca do okna; **wybór „Do” zamyka okno** i uruchamia 8 | okno z kaflami + lista wyboru | kafel → lista; wybór „Do” → 8; „Anuluj”, wstecz, dotknięcie poza oknem → zamknij bez zmian | Od: osoba w środku (D78) | — | **decyzja autora** (D26, D78) · R3 · [[osoby]] (lista) · D49 |
| 8 | **Ścieżka na drzewie** (v1.1; v1.16 — D45, D46, D48, D49): **„Od” zostaje w środku** (v1.29, D81; do v1.28 „Do” stawał w środku — W2, D45); gdy kafel „Od” zmieniono w oknie na kogoś innego, ta osoba staje w środku przy starcie ścieżki (przestawienie jak po dotknięciu, element 4, ok. 0,45 s). **Samo drzewo** (v1.29, D80): od wyboru „Do” znikają karta (5) z rzędem czasu (6) i + / − poziomu (3), a drzewo zajmuje ich miejsce; pasek u góry zostaje (w poziomie — górny rząd, 12). Drzewo przechodzi na **najniższy poziom, na którym widać całą ścieżkę**, licząc od osoby w środku — **tylko w górę**: gdy wybrany poziom ją pokazuje, zostaje (v1.23, D57; każda połączona osoba ma poziom, więc „poziom 4 i brakujące osoby ścieżki” z v1.16 odpada). **Kadr:** cała ścieżka na ekranie, 24 dp od krawędzi, pod banerem (jego wysokość przy danym tekście), w największej skali, w której się mieści, **najwyżej 1,3** (v1.17, D46), a **najmniej 0,08 — także poniżej granicy całego poziomu z 3a** (v1.24, test `qa` ISSUE-049): granica liczy miejsca osób, a imiona przy oddalaniu nie maleją (I2), więc ścieżka od skrajnej do skrajnej osoby poziomu potrzebuje odrobinę mniej, żeby imiona końców zostały na ekranie (test ISSUE-039 — MAJOR przeglądu: imiona ścieżki w całości — złapał 0,4 dp za marginesem; v1.23 mówiła „najmniej przy dolnej granicy 3a”). Skala pod granicą zostaje po końcu podświetlenia; pierwszy gest dwóch palców wraca do granicy (v1.25 — − przybliżania już nie ma) (F2; v1.23: skala nie zależy już od poziomu, **po końcu podświetlenia skala i poziom zostają** — do v1.22 skala wracała do 0,4). Osoby spoza ścieżki — **30% krycia**; **linie rodziny i ślady — wszystkie przy 30%**, także osób ze ścieżki, jedną warstwą; drogę niesie linia w akcencie (v1.17, odstępstwo 5 z przeglądu ISSUE-039; do v1.16 „razem z ich liniami i śladami”). **Linia w akcencie** (3 dp, ta sama grubość przy każdej skali) biegnie po liniach rodziny — para: pozioma; rodzic–dziecko: przez kreskę do dzieci; rodzeństwo: przez kreskę rodziców; przez mostki — tym samym łukiem (v1.31, D83) — **od „Od” do „Do”, ok. 0,7 s na krok**; osoba, do której doszła, dostaje pierścień i poświatę w akcencie ([[style-b]] reguła 2). Imiona osób ze ścieżki mają pierwszeństwo przy chowaniu nakładających się (przed osobą w środku; I2, D27). **Ograniczenie animacji** — od razu cała ścieżka (D5). **Rok:** ścieżka przestawia suwak na „dziś” i zatrzymuje ▶ (Y1, D48); **po wyjściu wraca rok sprzed ścieżki** (v1.29, D81). **Koniec ścieżki** (v1.29, D79; do v1.28 — D49: także dotknięcie drzewa, przybliżanie i oddalanie, poziom, ▶, suwak): **wstecz** (gest, przycisk nawigacji, „wstecz” czytnika ekranu), a poza tym przełącznik „Drzewo · Mapa”, „Przesyłaj na telewizor”, wybór nowego „Do” w oknie (nowa ścieżka zastępuje starą) i **zmiana danych drzewa** (v1.17, odstępstwo 3 ISSUE-039). **W trakcie:** dwa palce, przeciąganie i podwójne dotknięcie zmieniają tylko widok; dotknięcie osoby nic nie robi; „Obróć” zostawia ścieżkę, a kadr liczy się od nowa w nowym rozmiarze (12). Po wyjściu wracają karta, suwak (na roku sprzed ścieżki) i + / −; „Od” w środku, poziom i skala zostają (D81) | animacja na drzewie | wstecz → koniec ścieżki · dwa palce, przeciąganie → tylko widok · dotknięcie osoby → nic (D79) | — | — | **decyzja autora** (D21, D26, D79–D81) · D5 · D46, D48, D49 |
| 9 | **Baner** (v1.1; v1.16 — D43, D47) u góry drzewa, 12 dp od góry i 16 dp od boków, na powierzchni, zaokrąglony 12 dp, wyśrodkowany, zawija się; pojawia się, **gdy linia dojdzie do „Do”** (przy ograniczeniu animacji — od razu). **„Od” = „Ja”:** jedna linia — nazwa ze słownika Twoim głosem, ten sam tekst co w karcie (16 sp, półgruby, kolor tekstu), np. „Babcia mojej żony” (G2, D28). **„Od” to ktoś inny** (O2, D47): pierwsza linia „Piotr Przykładowy → Zofia Wymyślona” (13 sp, tekst pomocniczy; „Ja”, gdy jedną z osób jesteś Ty), druga — nazwa bez zaimka: „Wnuczka”, „Siostrzenica bratowej”. **Wysokość wiersza 1,3** w obu liniach, a nie 1,43 z motywu: kadr (8) mierzy baner tymi samymi stylami, którymi się rysuje, więc przy 200% nie zasłania góry ścieżki; przy 100% baner jest przez to o kilka dp niższy niż w makiecie (v1.17, odstępstwo 4 ISSUE-039). **Czas (v1.29, D80):** baner stoi przez całą ścieżkę, do wyjścia, bez „×” (D79); do v1.28 — 4 s, dłużej według „Czas na działanie” (D43). **W poziomie** baner stoi w górnym rzędzie między przełącznikiem a ikonami (12). Czytnik ogłasza baner raz, bez przenoszenia fokusu (komunikat stanu, SC 4.1.3) — jako **region na żywo**, jak pigułka poziomu (element 3), a nie osobnym ogłoszeniem (v1.17, odstępstwo 1 ISSUE-039, D43). Bez zdania ścieżki i **bez „Odtwórz jeszcze raz”** (D26) | baner | znika z końcem ścieżki (v1.29) | — | — | **decyzja autora** (D26) · D6 · D43 · D47 |
| 10 | **Bez ścieżki:** baner jak 9, ale na 4 s — dłużej, gdy zaleca ustawienie „Czas na działanie” (D43; v1.29 bez zmian), jedna linia: „Te osoby nie łączą się — w drzewie brakuje rodziny między nimi.”; drzewo bez zmian — środek, poziom i rok zostają | baner | — | — | — | reguła 9 |
| 12 | **Układ poziomy — drzewo i część „Mapa”** (v1.29, L4 — D77; prototyp ISSUE-055, panele 4–6): gdy ekran stoi poziomo — z „Obróć” (D82) albo z obracania telefonu — **bez dolnego paska zakładek** ([[style-b]] reguła 12, v1.54). **Górny rząd nad drzewem** (64 dp; drzewo rysuje się też pod nim): z lewej przełącznik „Drzewo · Mapa” (jak 1, 12 dp od lewej i od góry), z prawej ikony „Obróć”, „Połącz dwie osoby” (tylko część „Drzewo”) i „Przesyłaj na telewizor” w jednej pigułce (zaokrąglenie 28 dp), 8 dp od prawej i od góry — oba na powierzchni z obrysem 1 dp. **Dolny pasek** na powierzchni z obrysem u góry, 64 dp, rośnie, gdy tekst się zawija (bez ucinania — jak 5); w części „Mapa” linia „gdzie” to trzecia linia tekstu, więc pasek ma ok. 79 dp, a mapa jest o tyle niższa (v1.30, odstępstwo 2 ISSUE-055): karta osoby w środku w jednym rzędzie — okrąg 40 dp, imię z „z d.” (15 sp, półgruby) i „lata · kim jest dla mnie” (13 sp, tekst pomocniczy; w części „Mapa” pod nim linia „gdzie”, 13 sp — [[mapa-migracji]] 12), tekst do 300 dp szerokości; dalej rząd czasu (6: ▶, ⏭, suwak na resztę szerokości, rok, tempo) i „Pokaż ›”. **+ / − poziomu** (3) w prawym dolnym rogu drzewa, nad paskiem. **Kadr:** start i przestawienie środka jak w pionie — osoba na środku obszaru drzewa; ścieżka (8) mieści się pod górnym rzędem. **W trakcie ścieżki** (D80): dolny pasek i + / − znikają, drzewo sięga dolnej krawędzi; baner (9) stoi w górnym rzędzie między przełącznikiem a ikonami, wyśrodkowany. Telefon autora (915 × 412 dp): drzewo 915 × 308 dp, w trakcie ścieżki 915 × 372; ścieżka przez 4 pokolenia w skali ok. 0,55 (prototyp). Do innych zakładek — „Obróć” albo wstecz | układ | „Obróć” → pion · wstecz → jak w pionie | pion; poziomo z „Obróć” albo obracania telefonu | — | **decyzja autora** (D76, D77) · panel 5 („tak” — mapa) · D80, D82 |

## States
| Stan | Co widać |
|---|---|
| drzewo | 1, 3–5 (6 od US-010); na starcie „Ja” w środku, skala 1, wybrany poziom — przy pierwszym uruchomieniu „Linia krwi” (v1.23) |
| oddalenie (v1.23) | 1, 3–5, skład bez zmian; imiona według I2 — czytelne, nakładające się chowają (element 4, D27); przy całym poziomie 1 od „Ja” skala ok. 0,12, okręgi ok. 5 dp, widać ok. 10 z 91 imion; miejsce osoby < 24 dp → dotknięcie przybliża (3a) |
| pierwszy i ostatni poziom (v1.25) | 3: na „Linii krwi” − nieaktywne, na najwyższym poziomie osoby w środku + nieaktywne (bez obrysu, ikona w kolorze tekstu pomocniczego); osoba z jednym poziomem — oba. Do v1.24 w tym wierszu była lista poziomów — usunięta (D58) |
| zmiana poziomu (v1.23) | 4 — dochodzący się pojawiają, odchodzący gasną, skala i środek bez zmian (K1); pigułka „Przez 1 związek · 113 osób (+22)” ok. 1,8 s — w trybie prezentacji pod górnym rzędem sterowania (v1.25, D58; w v1.24 bez pigułki), przy 200% w dwóch liniach, szeroka jak dłuższa linia (ok. 214 dp na ekranie 360 dp — zrzut 31); na dolnej granicy skala rośnie do nowej, a cały poziom staje na środku (v1.24, 3a) |
| rok w przeszłości (US-010) | 4 bez osób nieurodzonych (miejsca zostają), linie par według dat związku, znicze zmarłych do tego roku, przerywany obrys przy osobach w oknie daty (N3); ślad dalszej rodziny i pigułka poziomu liczą tylko osoby, które w tym roku już są (D37); 5 bez zmian; 6 z rokiem (v1.12) |
| osoba w środku przed narodzinami (US-010) | 4: w jej miejscu pusty pierścień w akcencie (C1, D33); 5 bez zmian; czytnik „… — przed narodzinami” |
| odtwarzanie (US-010) | 6: ❚❚ zamiast ▶, rok biegnie w wybranym tempie (domyślnie „Średnio”, 10 lat na sekundę — v1.14, D41); dotknięcie osoby i oddalanie działają dalej (D37) |
| ograniczenie animacji (US-010) | jak odtwarzanie, ale rok skacze o dekadę co ok. 2 · 1 · 0,5 s według tempa, osoby pojawiają się od razu (R2, D36, D41) |
| następne — podpis roku (ISSUE-050, v1.26) | 6: suwak na roku zdarzenia, ⏭ zaraz za ▶; 6a: dymek u góry drzewa „W 1893 / Urodził się Ignacy Zmyślicki”; osoba z podpisu była poza ekranem — widok podjechał tak, że grupa stoi 8 dp pod dymkiem (V2; v1.27), skala i osoba w środku bez zmian; **osoby z podpisu świecą** — pierścień, poświata pod okręgiem i wieńcem, trzy pulsy, potem stała (D73; v1.28); przy ograniczeniu animacji suwak i widok przeskakują, osoby pojawiają się od razu, poświata stała bez pulsu (D36, D75) |
| następne — ślub albo „razem” (ISSUE-050, v1.28) | 6a: „Ślub: Krystyna Zmyślona i Henryk Zmyślony”; obie osoby świecą, a linia pary w akcencie rośnie od pierwszej do drugiej (ok. 0,45 s) i zostaje, dopóki stoi podpis (D73) |
| następne — rok z więcej niż 4 zdarzeniami (ISSUE-050) | 6a: 4 zdarzenia i „Jeszcze 2 w tym roku”, nagłówek „W 1955 · 1 z 2”; ⏭ → dalszy ciąg 1955, następne ⏭ → następny rok (makieta, cała rodzina: 1955) |
| następne — koniec (ISSUE-050, AC-4) | po ostatnim zdarzeniu ⏭ → suwak na „dziś”, dymek „Dziś / To wszystkie zdarzenia z datą.”, w trybie prezentacji „dziś” w rogu i „Dziś  To wszystkie zdarzenia z datą.” na listwie (v1.28, D72); nikt nie świeci; ⏭ jeszcze raz → pierwsze zdarzenie (w makiecie 1868) |
| następne — brak zdarzeń z datą (ISSUE-050) | ⏭ nie ma — rząd czasu jak przed v1.26 (D71) |
| tryb prezentacji — podpis roku (ISSUE-050, v1.28) | 11: rok w rogu, pod nim nic; na listwie nad rzędem ▶ ⏭ linia podpisu 14 sp (B — D72), 5 s jak po każdym dotknięciu (D40), znika z listwą, a pusty dotyk pokazuje ją znowu; osoby z podpisu świecą (D73); widok podjeżdża do nich pod rokiem, nad listwą (V2). Do v1.27 — podpis 28 sp pod rokiem (P1, D64) |
| połącz — wybór (US-011) | 1, okno 7 nad przyciemnionym drzewem; kafel → lista „Od kogo?” / „Do kogo?” na cały ekran, bez dolnego paska; wyszukiwanie bez wyniku — „Nie ma osoby „…”.” (jak [[osoby]]) |
| połącz — ścieżka (US-011, v1.29) | 1, 4 („Od” w środku), 8 (reszta 30%), 9 od dojścia linii do „Do” aż do wstecz; bez 3, 5 i 6 — samo drzewo (D79–D81; do v1.28 „Do” w środku z kartą i suwakiem, baner 4 s) |
| połącz — ścieżka, tekst 200% (US-011) | jak wyżej; w oknie 7 kafle jeden pod drugim; baner do 4 linii przy „Od” innym niż Ty, kadr pod nim; skala zwykle poniżej 0,4 (F2), imię jednej z osób ścieżki może się schować (makieta: Ja → Wanda, 1 z 4) |
| bez ścieżki (US-011) | 1, 3–6 bez zmian, 10 przez ok. 4 s |
| połącz — po wyjściu (v1.29) | 1, 3–6 jak przed ścieżką: suwak na roku sprzed ścieżki, „Od” w środku, poziom i skala ze ścieżki (D81) |
| poziomo (v1.29, L4) | 12: górny rząd nad drzewem (przełącznik, „Obróć”, „Połącz dwie osoby”, „Przesyłaj”), dolny pasek z kartą i czasem, + / − nad paskiem, bez zakładek (D77) |
| poziomo — ścieżka (v1.29) | 12 bez dolnego paska i + / −; baner (9) w górnym rzędzie; drzewo do dolnej krawędzi (D80) |
| poziomo — część „Mapa” (v1.29) | jak „poziomo”, w miejscu drzewa mapa, w karcie linia „gdzie” ([[mapa-migracji]] 12, D31); bez „Połącz dwie osoby” |
| osoba bez rodziny | 4: tylko ona, bez śladu; 5 („… · nie wiadomo jeszcze, kim jest dla mnie”, chyba że to „ja”) |
| osoba spoza rodziny „ja” | 4: jej rodzina; 5 z „nie wiadomo jeszcze, kim jest dla mnie” |
| „ja” niewybrane | 1 bez ikon; w miejscu drzewa, na środku: „Aplikacja nie wie jeszcze, która osoba to Ty.” (16 sp, tekst pomocniczy) i przycisk tekstowy w akcencie „Wybierz, która osoba to Ty” (jak [[osoba]] element 7); bez karty i + / −. Wejście z „Pokaż w drzewie” działa — wtedy 5 bez pokrewieństwa (D19) |
| pusta baza | 1 bez ikon; na środku „Tu pojawi się drzewo — osoby z grobów i ich rodziny.” (16 sp, tekst pomocniczy; jak „pusta baza” w [[osoby]]), bez działania (D19) |
| tekst 200% | 4 z szerszym miejscem osoby; 5 z „Pokaż ›” pod tekstem; 6 — ⏭ w dolnym rzędzie obok ▶, suwak 222 dp (v1.26); 6a — dymek zawija się, imię z nazwiskiem w jednej linii; w trybie prezentacji linia podpisu na listwie zawija się w kilka wierszy (v1.28); + / − poziomu bez zmian, 48 dp (D20); pigułka poziomu w dwóch liniach, ok. 214 dp szerokości (v1.25, emulator 360 × 640 dp, zrzut 31; do v1.24 tu była etykieta poziomu ok. 140–235 × 48 dp) |
| przesyłanie — ekran systemu (v1.10) | nie ekran aplikacji: ustawienia telefonu („Google Cast” na emulatorze z Androidem 16; jasny, w języku telefonu), lista telewizorów w tej samej sieci Wi-Fi albo „No nearby devices were found.” (zrzut `01`). Wstecz wraca do aplikacji |
| tryb prezentacji | 11 — po ekranie systemu bez podpowiedzi; rok z karty (Z2), w rogu, gdy nie jest „dziś” (L1); poziom i skala z telefonu, osoba w środku na środku (v1.23) |
| tryb prezentacji — sterowanie (v1.14, ISSUE-038) | 11 + „Zakończ prezentację” u góry po prawej i listwa na dole (▶ / ❚❚, rok początku, suwak, tempo, − / + poziomu — v1.25; na listwie od 560 dp — v1.24); po zmianie poziomu pigułka pod górnym rzędem (v1.25); rok w rogu także na „dziś”; 5 s od ostatniego dotyku (B2, D40); z czytnikiem ekranu od wejścia w tryb i bez chowania (v1.15) |
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
│                 (Z)          (−) │  ← v1.25 (D58): + / − zmieniają poziom; przybliżanie — dwa palce, podwójne dotknięcie
│ ╭──────────────────────────────╮ │
│ │ (Ja) Mateusz Wymyślony       │ │
│ │      ur. 1983 · to ja Pokaż ›│ │
│ │(▶)(⏭) ━━━━━●━━ 1984 Średnio│ │  ← suwak czasu — US-010 (v1.12): ▶ 36 dp, rok w akcencie, „dziś” na końcu; tempo (v1.14, V2); v1.26: ⏭ za ▶, rok początku tylko przy ≥ 150% (U3)
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
│  │ (▶) 1860 ━━━━━━━━━━━━━●━━━━━━━━━━━  Średnio                 (−)(+) │  │  ← listwa B2: pusty dotyk → na 5 s; rok stoi w rogu; v1.25: − / + poziomu (D58)
│  ╰──────────────────────────────────────────────────────────────────╯  │
└────────────────────────────────────────────────────────────────────────┘
```

**„Następne” — telefon i telewizor** (v1.28 — ISSUE-050; K1, F1, V2, U3, na telewizorze B — D72, świecenie — D73; do v1.27 na telewizorze podpis pod rokiem, P1, zrzuty `01`, `11` w `shots050\`):
```
┌──────────────────────────────────┐   ┌────────────────────────────────────────────────────────────────────────┐
│ Drzewo                    ⛓  [⌔] │   │ ┌────┐                                                                 │
│  ╭ W 1893 ─────────────────╮     │   │ │1955│  ← rok L1, 36 sp; pod nim nic (v1.28)                           │
│  │ Urodził się Ignacy      │     │   │ └────┘                                                                 │
│  │ Zmyślicki               │     │   │                                                                        │
│  ╰─────────────────────────╯     │   │    (CZ)━(TZ)  ⟨(HZ)⟩━━⟨(KZ)⟩   ⟨(WP)⟩━━⟨(EP)⟩   ⟨(GT)⟩  ⟨(MW)⟩   (ZZ)  │
│           ⟨(IZ)⟩           (A)   │   │               ⟨ ⟩ świecą: pierścień, poświata pod okręgiem i wieńcem,  │
│           Ignacy                 │   │               trzy pulsy, potem stała (D73); ━━ linia pary w akcencie  │
│   ⟨ ⟩ świeci; widok podjechał    │   │                                                                        │
│                             (+)  │   │                                                                        │
│                             (−)  │   │ ╭──────────────────────────────────────────────────────────────────╮   │
│ ╭──────────────────────────────╮ │   │ │ W 1955 · 1 z 2  Ślub: Krystyna Zmyślona i Henryk Zmyślony · Ślub:│   │
│ │ (Ja) Mateusz Wymyślony Pokaż›│ │   │ │ Wanda Przykładowa i Edmund Przykładowy · Urodziła się Grażyna …  │   │
│ │      ur. 1983 · to ja        │ │   │ │ (▶)(⏭) 1860 ━━━━━━━━━━━━━━━━━━━━━━━━●━━━━━━━━━━  Średnio   (−)(+) │  │
│ │(▶)(⏭) ━━●━━━━━ 1893 Średnio │ │   │ ╰──────────────────────────────────────────────────────────────────╯   │
│ ╰──────────────────────────────╯ │   └────────────────────────────────────────────────────────────────────────┘
└──────────────────────────────────┘      linia podpisu 14 sp na listwie (D72) — 5 s po ⏭, potem znika z listwą;
                                          rok w rogu i świecące osoby zostają, dopóki stoi podpis
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

**Poziomo — L4 „bez zakładek”** (v1.29 — ISSUE-055, D77; telefon autora 915 × 412 dp; prototyp, zrzuty `11`–`15` w `shots055\`):
```
┌────────────────────────────────────────────────────────────────────────────┐
│ ╭─────────────────╮                                       ╭─────────────╮ │
│ │ Drzewo │ Mapa   │         (P)━(A)        (E)━(M)        │ ⟲   ⛓  [⌔] │ │  ← górny rząd nad drzewem; ⟲ „Obróć” (D82)
│ ╰─────────────────╯            │              │           ╰─────────────╯ │
│                   ((Ja))━(N)   (K)━(P)        (I)                         │
│                      │           │                                   (+)  │
│                     (L)         (O)                                  (−)  │
│ ┌────────────────────────────────────────────────────────────────────────┐ │
│ │(Ja) Mateusz Wymyślony    (▶)(⏭) ━━━━━━━━━━━━━━━━━━━●━━ dziś  1×  Pokaż ›│ │  ← dolny pasek 64 dp: karta + czas
│ │     ur. 1983 · to ja                                                   │ │
│ └────────────────────────────────────────────────────────────────────────┘ │
└────────────────────────────────────────────────────────────────────────────┘
  w trakcie ścieżki: dolny pasek i + / − znikają, baner (9) staje w górnym rzędzie między przełącznikiem a ikonami (D80)
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
- **Reguła 2:** poświata tylko na osobie w środku, na zapalonych węzłach ścieżki i na osobach z podpisu roku po ⏭ (v1.28, D73 — trzy pulsy, potem stała; [[style-b]] v1.48).
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

- **Poziom i przybliżanie (v1.23, ISSUE-049):** etykieta poziomu — powierzchnia z obrysem (obrys na tle 3,40:1, SC 1.4.11), nazwa w kolorze tekstu (10,02:1 na powierzchni),
  `arrow_drop_down` w akcencie (8,04:1; reguła 1 — działanie, jak „Pokaż ›”). Lista — dolny arkusz na powierzchni ([[style-b]] reguła 2), nazwa — tekst 10,02:1, opis — tekst pomocniczy
  5,01:1, wybór — `check` w akcencie 8,04:1 i stan „zaznaczone” (kolor nie jest jedynym nośnikiem — SC 1.4.1). Pigułka bez zmian. − / + na listwie trybu prezentacji — tło z obrysem jak
  + / − w drzewie. Cel dotyku osoby: wyjątek w [[style-b]] *Thresholds* zmieniony w v1.44 (D52). Bez nowych tokenów (przeliczone z `theme.dart` 2026-10-19).
  **v1.24** (przegląd `ui` zbudowanego ekranu): etykieta na listwie trybu prezentacji — tło z obrysem jak − / + (obrys na powierzchni listwy 3,10:1, nazwa — tekst na tle 10,98:1,
  `arrow_drop_down` — akcent na tle 8,81:1); tabliczka imienia leży nad okręgami sąsiadów ([[style-b]] reguła 13, v1.45 — odstępstwo 2). Pary przeliczone z `theme.dart` 2026-10-19:
  tekst 10,98 / 10,02 · tekst pomocniczy 5,01 na powierzchni · akcent 8,81 / 8,04 · obrys 3,40 / 3,10 (na tle / na powierzchni).
  **v1.25** (D58): etykiety i listy nie ma. + / − poziomu — jak dawne + / − przybliżania: powierzchnia z obrysem 3,40:1 na tle, ikona w kolorze tekstu 10,02:1; na listwie tło z
  obrysem 3,10:1 na powierzchni, ikona 10,98:1. Nieaktywny — bez obrysu, ikona w kolorze tekstu pomocniczego (5,01 na powierzchni, 5,50 na tle; rola „nieaktywne zakładki”, [[style-b]]
  *Token roles*) — kształt, nie sam kolor: między ikoną aktywną a nieaktywną jest tylko 2,00:1 (SC 1.4.1, przegląd `ui` rundy 2); czytnik „niedostępne”; nieaktywny element nie musi spełniać SC 1.4.11, a ma i tak 5:1. Oddalanie tylko gestem — wyjątek [[style-b]] *Thresholds* → gesty (v1.46).
- **„Następne” i podpis roku (v1.26, ISSUE-050):** ⏭ — `skip_next` w akcencie, bez wypełnienia (działanie, reguła 3; 8,04:1 na powierzchni karty i listwy); ▶ zostaje jedynym wypełnionym
  (reguła 1). Nieaktywnego ⏭ nie ma: ikona w kolorze tekstu pomocniczego różniłaby się od aktywnej tylko kolorem (1,60:1 — SC 1.4.1), więc przy braku zdarzeń przycisk znika (D71).
  Dymek — powierzchnia; nagłówek i „Jeszcze 3 w tym roku” — tekst pomocniczy 5,01:1, zdarzenia — tekst 10,02:1. Linia podpisu na listwie (v1.28, D72) — zdarzenia: tekst na powierzchni 10,02:1, nagłówek i
  „Jeszcze …” — tekst pomocniczy 5,01:1, 14 sp jak dymek; próg 28 sp dla zdań na telewizorze ([[style-b]] v1.47) jej nie dotyczy — czyta ją autor z telefonu, rodzina czyta rok w rogu (36 sp).
  Świecenie (D73): pierścień i linia pary w akcencie 8,81:1 na tle (SC 1.4.11 ≥ 3:1); puls kończy się przed 5 s ([SC 2.2.2](https://www.w3.org/TR/WCAG22/#pause-stop-hide)) i ma mniej niż
  3 zmiany na sekundę — 0,83 Hz, łagodna zmiana krycia na małej powierzchni ([SC 2.3.1](https://www.w3.org/TR/WCAG22/#three-flashes-or-below-threshold)); przy ograniczeniu animacji bez pulsu (SC 2.3.3, D75). Linia nie kończy się separatorem ani dopiskiem: imię z nazwiskiem i dopisek trzymają się razem
  (reguła 6). Bez nowych tokenów (przeliczone z `theme.dart` 2026-10-19: tekst 10,98 / 10,02, tekst pomocniczy 5,50 / 5,01, akcent 8,81 / 8,04 — na tle / na powierzchni).

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| M9 — drzewo rodziny z powinowatymi i powtórnymi związkami | 3, 4 | „Przez 1 związek” od „Ja” (v1.23): linia krwi z mężami i żonami, żona i jej rodzina po prawej, rodziny mężów i żon rodzeństwa |
| US-009 AC-1 — od „Ja” | 1, 3, 4, 5 | zakładka Drzewo: „Ja” w środku z pierścieniem, skala 1; od v1.23 na wybranym poziomie (pierwszy raz „Linia krwi”: rodzice, dziadkowie, rodzeństwo z partnerami, Kasia, dzieci; rodzina Kasi — „Przez 1 związek”) |
| US-009 AC-2 — przestawianie środka | 4, 5 | dotknięcie Kasi → ona w środku z animacją, karta „ur. 1985 · Moja żona” (v1.9, G2); drugie dotknięcie albo „Pokaż” → widok Kasi |
| ~~US-009 AC-3 — dalsza rodzina (S2)~~ | 3, 3a | **zastąpione przez ISSUE-049 AC-1–AC-3 (v1.23):** dalszą rodzinę dokłada przełącznik poziomu, a nie oddalanie (do v1.22: − → „Poziom 3 · 66 osób”) |
| US-009 AC-4 — ślad dalszej rodziny | 4 | na poziomie 2 osoba z rodziną poza widokiem ma bladą kreskę 3/3: w górę rodzice, w dół dzieci, w bok partner |
| US-009 AC-5 — nazwa pokrewieństwa w karcie | 5 | „Moja ciotka (siostra taty)” · „Mój stryj (brat taty)” · „Mój wuj (brat mamy)” · „Moja siostra cioteczna (córka siostry taty)” · „Siostra cioteczna mojego dziadka” · ścieżka Ja → żona → jej mama → jej mama → jej rodzic → jego rodzeństwo → jego dziecko: „Siostra cioteczna babci mojej żony” · mama taty: „Moja babcia” (v1.9, G2 — D28; makieta, sekcja 2; D12) |
| US-009 AC-6 — „Pokaż w drzewie” | [[osoba]] 6 → 4, 5 | w widoku Franciszka „Pokaż w drzewie” → zakładka Drzewo, Franciszek w środku, wybrany poziom, skala 1 (v1.23; do v1.22 — poziom 2) |
| US-009 AC-7 — tekst 200% na 360 dp | 4, 5 | miejsce osoby 160 dp, imię 26 sp bez ucięcia, inicjały 1,3× w okręgu; „Pokaż ›” pod tekstem karty |
| US-009 AC-8 — tryb prezentacji | 1, 11 | „Przesyłaj na telewizor” → ekran systemu → wstecz → poziomo, poziom i skala z telefonu (v1.23; do v1.22 — poziom 2 dopasowany), bez przycisków; dotknięcie pustego miejsca → „Zakończ prezentację” (v1.10; do v1.9 — ikona telewizora) |
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
| ISSUE-055 AC-1 — „Od” z drzewa | 1, 7 | w środku Zofia → ⛓ → kafel „Od”: Zofia, „Do” pusty (prototyp, panel 1; D78) |
| ISSUE-055 AC-2 — dwa palce nie kończą | 8 | ścieżka Zofia → Leon; przybliżanie i oddalanie — wyszarzenie, linia i pierścienie zostają (panel 2; D79) |
| ISSUE-055 AC-3 — koniec przez wstecz (bez „×” — decyzja autora) | 8, 5, 6 | wstecz → karta i suwak wracają, suwak na roku sprzed ścieżki (1950), Zofia w środku (panel 3; D79, D81) |
| ISSUE-055 AC-4 — samo drzewo | 8, 9 | w trakcie ścieżki bez karty, suwaka i + / −; baner „Prawnuk” stoi do wstecz (panel 2; D80) |
| ISSUE-055 AC-5 — pion / poziom | 1, 12 | „Obróć” → poziomo L4 (drzewo i „Mapa”), drugie dotknięcie → pion; także przy zablokowanym obracaniu (panele 4–6; D76, D77, D82) |
| ISSUE-056 AC-1 — miara narysowanych przecięć | 4 | sonda na kodzie aplikacji, wymyślona rodzina: 9 / 19 / 27 → 9 / 17 / 22 (poziomy 1–3); szyn jedna nad drugą najwyżej 4 (D84) |
| ISSUE-056 AC-2 — kto jest czyim dzieckiem | 4 | łuk w każdym przecięciu kreski z cudzą szyną, jeden łuk nad sąsiednimi szynami (prototyp, panel 2; D83) |
| ISSUE-056 AC-3 — reszta drzewa bez zmian | 4, 8 | miejsca osób te same (D86); linia ścieżki w akcencie przez mostki tym samym łukiem; ślad, linie par, „//” bez zmian (D83) |
| ISSUE-049 AC-1 — przybliżanie to sam widok | 3a | „Ja”, „Linia krwi”: dwa palce i podwójne dotknięcie (v1.25 — bez + / − przybliżania, D58) od skali 1 do całego poziomu (ok. 0,12) i z powrotem do 1,38 — cały czas 91 osób (makieta, `#test49=1`) |
| ISSUE-049 AC-2 — poziom 1 i 2 | 3 | „Ja”: na „Linii krwi” brat Michał, jego syn Leon i partnerka Natalia (M2), rodziców Natalii nie ma — nad Natalią ślad (D9); + → „Przez 1 związek” (v1.25) — rodzice Natalii, jej siostra Patrycja z mężem Konradem |
| ISSUE-049 AC-3 — poziom 3 | 3 | + → „Przez 2 związki” — dochodzą rodzice Konrada (Ryszard, Dorota) i jego brat; pigułka „Przez 2 związki · 116 osób (+3)” (przy M1 sam Konrad dochodzi dopiero tu) |
| ISSUE-049 AC-4 — przybliżanie na telewizorze | 11 | tryb prezentacji: dwa palce na telefonie — skala 1 → 0,48, cały czas 91 osób; + poziomu na listwie — „Przez 1 związek”, 113 osób, pigułka pod sterowaniem (T2; v1.25, D58) |
| ISSUE-049 AC-5 — ścieżka dalej cała (US-011) | 8 | „Ja” → Ryszard (teść siostry partnerki brata): poziom 3, skala 0,27, wszystkie 6 osób ścieżki na ekranie, baner „Teść siostry partnerki mojego brata”; po końcu skala i poziom zostają |
| ISSUE-039 — tekst 200% na 360 dp | 7, 9 | kafle jeden pod drugim, imię zawija się na spacji („Wanda / Przykładowa”), okno 328 × 458 dp; baner do 4 linii (zrzut `12`) |
| ISSUE-050 AC-1 — ⏭ na drzewie, rok i co się stało | 6, 6a | „Ja”, „Linia krwi”, suwak na 1940 → ⏭ → 1944: „Zmarł Leon Wymyślony (ok. 1944)”; ⏭ → 1946: „Ślub: Helena Wymyślona i Józef Wymyślony” (makieta, `#test50=1`). Przy F1 linie zaczynają się wielką literą — `planning` poprawia przykład w AC-1 („Urodził się Jan Wymyślony”, „Ślub: Maria Zmyślona i Piotr Wymyślony”) |
| ISSUE-050 AC-2 — ⏭ na mapie | [[mapa-migracji]] 15 | rok z przeprowadzką i podpis, kto się przeprowadził (M2: skąd i dokąd) |
| ISSUE-050 AC-3 — to samo na telewizorze, czytelne z kanapy | 6a, 11 | tryb prezentacji, ⏭ na listwie → 1895: rok 36 sp w rogu (z 3 m na 32″ ok. 23′ — D38), Franciszek i Tadeusz świecą na drzewie (D73), a linia „Urodził się Franciszek Wymyślony · Urodził się Tadeusz Wymyślewicz (między 1895 a 1900)” stoi na listwie 5 s — dla autora z telefonu (v1.28, B — D72). Z kanapy czyta się rok i widać, kogo dotyczy; słowa mówi autor. v1.26–v1.27: podpis 28 sp pod rokiem (P1, zrzut `03`) |
| ISSUE-050 AC-4 — po ostatnim zdarzeniu | 6a | po 2019 (ostatnie zdarzenie na „Linii krwi”) ⏭ → „dziś” i „To wszystkie zdarzenia z datą.”; ⏭ jeszcze raz → 1868, bez błędu (zrzut `09`) |

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

## Candidates — ISSUE-049 (2026-10-19)
> Makieta `drzewo-049.html` (*mockup* we frontmatterze) to makieta ISSUE-039 z nową regułą poziomów, przybliżaniem odpiętym od poziomu i przełącznikami wariantów.
> Rodzina: 107 osób z makiet drzewa (106 i Teofil bez rodziny) i 10 wymyślonych do AC-2 i AC-3 — rodzice i siostra Natalii (partnerki brata Michała), mąż siostry Konrad z rodzicami i bratem,
> rodzice Bartosza (męża siostry Joanny). Na starcie włączone rekomendacje; autotest `#test49=1` sprawdza AC-1–AC-5. **Nie** pokazuje płynności Fluttera, wieńców, zdjęć
> w węzłach, ikon z fontu aplikacji ani czytnika ekranu.

**Prior art.**
- **Prawo rodzinne** — granica, którą autor narysował, jest w kodeksie: pokrewieństwo to pochodzenie jednej osoby od drugiej albo od wspólnego przodka (KRO art. 617), a
  *„z małżeństwa wynika powinowactwo między jednym małżonkiem a krewnymi drugiego małżonka”* (KRO art. 618, [lexlege.pl](https://lexlege.pl/krio/art-61-8/), odczyt
  2026-10-19). Reguła autora idzie dalej niż prawo: rodzina żony brata nie jest dla mnie powinowatą (powinowactwo nie rodzi powinowactwa), a w drzewie to poziom 2. Prawo liczy
  obowiązki, drzewo — opowieść, więc to nie błąd, tylko inny cel; „Linia krwi” jest za to prawnie dokładna.
- **TimeNets** (D8) — wycinek rodziny według stopnia zainteresowania (DOI) zostaje, tylko z innymi wagami: krok po krwi 0, krok przez związek 1. U TimeNets było odwrotnie
  (*„across conjugal relations, DOI values decrease more slowly”*) — tam partner był bliżej, tu dalej, bo autor chce najpierw swojej krwi.
- **Programy genealogiczne** trzymają przy krewnych ich małżonków jako jeden zbiór: Gramps ma regułę *„Descendant family members of <person>”* — *„Matches people that are
  descendants or the spouse of a descendant of a specified person”* — obok osobnej „Descendants of” ([kod źródłowy Gramps 5.2](https://github.com/gramps-project/gramps/blob/maintenance/gramps52/gramps/gen/filters/rules/person/_isdescendantfamilyof.py),
  odczyt 2026-10-19). To M2 dla potomków; M1 to „Descendants of”.
- **Mapa migracji** — autor wybrał kadr tylko z własnych gestów (R4, [[mapa-migracji]] 10), więc K1 trzyma tę samą zasadę na drzewie.

| # | Kandydat | Co widać | Gdzie się dotyka | Źródło |
|---|---|---|---|---|
| M1 | **Na poziomie 1 tylko krew** | mąż, żona i partner krewnego dochodzą na 2 razem ze swoją rodziną; na 1 linia do dzieci brata wychodzi od niego samego | — | zdanie autora dosłownie · Gramps „Descendants of” |
| M2 | **Krew z mężami, żonami i partnerami; ich rodziny poziom wyżej** | na 1 pary są całe, nad partnerem spoza krwi ślad (D9); jego rodzina na 2 | — | Gramps „Descendant family members of” · przykłady autora (rodzina żony brata — 2, rodzina męża siostry żony brata — 3) |
| P1 | **Przyciski z numerami u góry drzewa** | „1 · 2 · 3” na tle z obrysem, wybrany w akcencie na tle akcentu 16% (6,66:1); nazwa tylko w pigułce po zmianie | jeden dotyk | segmentowy przełącznik Material |
| P2 | **Etykieta z nazwą + lista** | „Linia krwi ▾” w lewym dolnym rogu; lista z opisem i liczbą osób | etykieta → wiersz | arkusz rodów ([[wieniec]] E2) |
| P3 | **Przycisk nad + / −** | okrągły przycisk z plakietką numeru; każdy dotyk to następny poziom, po ostatnim — 1 | jeden dotyk na krok | — (ikona do dorysowania w foncie aplikacji) |
| N1 | **„Poziom 1, 2, 3”** | numer na etykiecie i w pigułce, opis tylko na liście | — | dziś („Poziom 3 · 66 osób”) |
| N2 | **„Linia krwi” · „Przez 1 związek” · „Przez 2 związki”** | pierwsza nazwa słowami autora, kolejne mówią regułę | — | zdanie autora · [[rodzina]] (związek: małżeństwo albo „razem”) |
| K1 | **Skala i środek zostają** | dochodzący pojawiają się wokół, pigułka „(+22)”; część może być poza ekranem | — | R4 ([[mapa-migracji]]) |
| K2 | **Dopasowanie do ekranu** | po każdej zmianie cały poziom; przy 91 osobach skala ok. 0,12 | — | — |
| T1 | **Poziom tylko przed wejściem w tryb** | listwa bez przełącznika | — | D16 (dziś poziom stały) |
| T2 | **Przełącznik poziomu na listwie** | ta sama etykieta (albo P1, P3) za tempem, przed − / + | listwa → etykieta → lista | B2 (D40) |

**Pomiar** (makieta, ekran 360 dp, obszar drzewa 360 × 510 dp, tekst 100%; „skala całości” — cały poziom na ekranie z 24 dp marginesu; „dotknięć −” — od skali 1, po ×1,45):

| W środku · reguła | Osób na poziomach | Skala całości | Okrąg (dp) | Imion widać | Dotknięć − |
|---|---|---|---|---|---|
| Ja · M1 | 67 → 109 → 116 | 0,17 · 0,10 · 0,09 | 7 · 5 · 4 | 9 · 11 · 9 | 5 · 7 · 7 |
| **Ja · M2** | **91 → 113 → 116** | 0,12 · 0,10 · 0,09 | 5 · 4 · 4 | 10 · 10 · 9 | 6 · 7 · 7 |
| Natalia (partnerka brata) · M1 | 6 → 76 → 113 → 116 | 1,00 · 0,14 · 0,10 · 0,09 | 44 · 6 · 4 · 4 | 6 · 11 · 12 · 10 | 0 · 6 · 7 · 7 |
| Natalia · M2 | 8 → 99 → 116 | 0,91 · 0,11 · 0,09 | 40 · 5 · 4 | 8 · 10 · 10 | 1 · 6 · 7 |
| Kasia (żona) · M1 | 15 → 83 → 112 → 116 | 0,80 · 0,13 · 0,10 · 0,10 | 35 · 6 · 4 · 4 | 15 · 10 · 12 · 12 | 1 · 6 · 7 · 7 |
| Kasia · M2 | 19 → 106 → 113 → 116 | 0,57 · 0,11 · 0,10 · 0,10 | 25 · 5 · 4 · 4 | 13 · 11 · 11 · 12 | 2 · 7 · 7 · 7 |

Dziś (D2) od „Ja” w tej samej rodzinie: 6 → 20 → 66 → 104 → 113 → 116 osób na poziomach 1–6, przełączane czterema progami skali; oddalanie kończy się na 0,4.
**Cały obraz na telewizorze** (tryb prezentacji, 914 × 411 dp, „Ja”, M2): poziom 1 — skala 0,34, okrąg 15 dp, 43 z 91 imion; „Przez 1 związek” — 0,27, 12 dp, 46 ze 113;
„Przez 2 związki” — 0,26, 11 dp, 44 ze 116. Co z tego wynika:
- **„Linia krwi” od „Ja” to większość rodziny** (91 ze 117 przy M2, 67 przy M1): krewni z krwi to potomkowie wszystkich ośmiu pradziadków. Poziomy nie są już kolejnymi
  pierścieniami wokół osoby, tylko „czyją rodzinę dołączam”. Na prawdziwych danych autora proporcja będzie podobna — notatki idą po liniach pradziadków;
- **cały obraz na telefonie pionowo to pasek**: poziom 1 jest ok. 4 razy szerszy niż wysoki, okręgi mają ok. 5 dp, widać ok. 10 imion. Czytelny cały obraz daje telewizor
  (okręgi 15 dp, ok. połowa imion). Na telefonie oddalanie służy orientacji — „gdzie jestem w całości” — a czyta się przy skali bliskiej 1;
- **przy 200%** obszar drzewa ma 360 × 305 dp, a etykieta poziomu ok. 170 × 48 dp — mieści się obok + / − bez nakładania (makieta).

## Candidates — ISSUE-050 (2026-10-19)
> Makieta `drzewo-050.html` (*mockup* we frontmatterze) to makieta ISSUE-049 (117 wymyślonych osób, poziomy M2, + / − poziomu po D58) z ⏭ w karcie i na listwie, podpisem roku na
> telefonie i telewizorze, podglądem „z kanapy” 32–65″ i autotestem `#test50=1`. Olaf ma w makiecie wyczyszczoną płeć (przypadek „bez płci”). Obok `mapa-050.html` — mapa z makiety
> ISSUE-045 w stanie po [[mapa-migracji]] v1.4 (bez nazw, bez śladu, K2, kadr z gestów) z ⏭ i podpisem przeprowadzki (M1–M2). **Nie** pokazuje płynności Fluttera, zdjęć w węzłach,
> wieńców, ikon z fontu aplikacji ani czytnika ekranu.

**Cel autora** (R1, `/pm` 2026-10-19): **(a) opowiadanie rodzinie przy telewizorze** — telewizor pierwszy, telefon drugi.

**Prior art** (odczyt 2026-10-19):
- **„Następny” w odtwarzaczu** — Media3 `PlayerControlView` ([androidx/media](https://github.com/androidx/media), gałąź `release`): atrybut `show_next_button` — *„Whether the next
  button is shown.”* (domyślnie tak), obok ▶; dotknięcie woła `player.seekToNext()`. Zamiar odtwarzania zmieniają tylko ▶ / ❚❚ (`Player`: *„Indicates the user intention to play. It can
  be set with play or pause.”*), więc w odtwarzaczu „następny” nie zatrzymuje — to Z2. Znak `skip_next` jest w Material Symbols.
- **Zdanie o zdarzeniu z płcią** — Gramps, `gramps/plugins/lib/libnarrate.py` ([gałąź maintenance/gramps52](https://github.com/gramps-project/gramps/blob/maintenance/gramps52/gramps/plugins/lib/libnarrate.py)):
  każde zdanie ma trzy wersje — *„%(male_name)s was born on %(birth_date)s in %(birth_place)s.”*, *„%(female_name)s was born on …”*, *„%(unknown_gender_name)s was born on …”*, tak samo
  *„died on”*. Po polsku płeć zmienia czasownik („urodził się” / „urodziła się”), więc trzecia wersja to „urodził(a) się” — F1; albo rzeczownik bez płci — F2.
- **Tekst na telewizorze** — napisy: *„All subtitles should be center justified and placed at either the top or bottom of the screen”*, *„2 lines maximum”*, *„Maximum duration: 7 seconds
  per subtitle event”* ([Netflix — Timed Text Style Guide: General Requirements](https://partnerhelp.netflixstudios.com/hc/en-us/articles/215758617-Timed-Text-Style-Guide-General-Requirements)) —
  P2 jest tym wzorcem. Podpis roku nie jest napisem dialogu: tempo nadaje autor, a lista bywa dłuższa niż 2 linie — stąd P1 i strony po 4 zdarzenia (D66). Wielkość — skala TV Androida (D38) i
  M3: *headline medium* 28 sp (Flutter 3.41.1, `material/typography.dart` → `_M3Typography`: `headlineMedium` 28.0, `headlineSmall` 24.0, `displaySmall` 36.0 — sprawdzone w SDK).
- **Suwak Fluttera** — tor jest krótszy od suwaka o 2 × 24 dp: `RoundSliderOverlayShape({this.overlayRadius = 24.0})` (`material/slider_value_indicator_shape.dart`) i
  `offset.dx + math.max(overlayWidth / 2, thumbWidth / 2)` (`material/slider_parts.dart`; Flutter 3.41.1, sprawdzone w SDK).
- **Własne konwencje:** ▶ z „dziś” zaczyna od początku suwaka (D34); widok po zmianie poziomu zmienia tylko autor (K1 — D55), na mapie kadr z gestów (R4 — [[mapa-migracji]] D6); aplikacja
  nie zgaduje dat (D22, D31).

| # | Kandydat | Co widać | Gdzie się dotyka | Źródło |
|---|---|---|---|---|
| K1 | **Zdarzenia osób z wybranego poziomu** | na „Linii krwi” od „Ja” — zdarzenia 91 osób; + dokłada rodziny razem z ich zdarzeniami | ⏭ · + / − poziomu | poziomy (D50) |
| K2 | **Zdarzenia całej rodziny** | podpis mówi też o osobach, których na drzewie nie ma | ⏭ | — |
| N1 | **Data niepewna w roku zapisanym, z dopiskiem** | „Urodziła się Marianna Wymyślona (ok. 1870)” w 1870; osoba z przerywanym obrysem | — | D32 |
| N2 | **Tylko daty pewne** | ⏭ pomija „ok.”, „przed”, „po”, „między” | — | — |
| F1 | **Czasownik według płci** | „Urodził się / Urodziła się / Urodził(a) się …”, „Zmarł / Zmarła …”, „Ślub: …”, „Razem: …” | — | słowa autora · Gramps |
| F2 | **Rzeczownik** | „Narodziny: …”, „Śmierć: …”, „Ślub: …”, „Razem: …” | — | — |
| Z1 | **⏭ zatrzymuje ▶** | podpis stoi, ▶ potem jedzie dalej od tego roku | ⏭ | — |
| Z2 | **⏭ jak w odtwarzaczu** | ▶ biegnie dalej, podpis znika z następnym rokiem (przy „Średnio” po 0,1 s) | ⏭ | Media3 |
| V1 | **Widok stoi** | osoby z podpisu często poza ekranem | — | K1 (D55), R4 |
| V2 | **Widok podjeżdża do osób z podpisu** | przesunięcie bez zmiany skali, tylko gdy kogoś nie widać | — | przestawienie środka (element 4) |
| P1 | **Podpis pod rokiem w rogu** | rok i zdarzenia w jednym miejscu, lewy górny róg | — | L1 (D39) |
| P2 | **Podpis na dole na środku** | jak napisy; przez 5 s po ⏭ nad listwą, potem zjeżdża | — | Netflix |
| U1 | **Karta: jeden rząd, wszystko** | ▶ ⏭ 1860 ━ 1893 Średnio | ⏭ | — |
| U2 | **Karta: dwa rzędy** | rok początku, tempo i rok nad ▶ ⏭ i suwakiem | ⏭ | układ ≥ 150% (D20) |
| U3 | **Karta: jeden rząd bez roku początku** | ▶ ⏭ ━━ 1893 Średnio | ⏭ | — |

**Pomiar** (makieta, `#test50=1`, ekran 360 dp, tekst 100%, 2026-10-19):

| W środku · poziom (K1, N1) | Zdarzeń | Lat ze zdarzeniem | Dotknięć ⏭ do „dziś” | Najwięcej w roku | Lat z > 4 |
|---|---|---|---|---|---|
| Ja · Linia krwi | 147 | 79 | 85 | 5 | 5 |
| Ja · Przez 1 związek | 180 | 84 | 92 | 8 | 7 |
| Ja · Przez 2 związki | 184 | 85 | 93 | 8 | 7 |
| Kasia (żona) · Linia krwi | 28 | 23 | 24 | 3 | 0 |

K2 (cała rodzina): 186 zdarzeń w 86 latach. N2 zamiast N1: 141 zamiast 147 na „Linii krwi” od „Ja”. Bez roku — nie są zdarzeniem — 3 śluby, 2 urodzenia i 1 śmierć.
**Widok:** pierwsze 12 dotknięć ⏭ od „Ja” w skali 1 — osoby z podpisu na ekranie: **V1 — 0 z 16**, **V2 — 14 z 16** (2 — para szersza niż ekran, środek na pierwszej osobie).

| Karta, 360 dp | Suwak 100% | Tor Fluttera (− 48 dp) | Karta | Suwak 200% |
|---|---|---|---|---|
| dziś (bez ⏭) | 129–137 dp | ok. 81–89 dp | 114 dp | 278 dp (makieta ISSUE-038) |
| U1 | 73 dp | ok. 25 dp | 114 dp | 222 dp |
| U2 | 222 dp | ok. 174 dp | 162 dp (obszar drzewa 510 → 462 dp) | 222 dp |
| U3 | 110 dp | ok. 62 dp | 114 dp | 222 dp |

**Telewizor** — wysokość cyfry z 3 m, telefon wypełnia szerokość (32″ · 43″ · 55″ · 65″; metoda z *Candidates — ISSUE-038*): podpis **28 sp — 18 · 24 · 30 · 36′**; 24 sp — 15 · 21 · 26 · 31′
(na 32″ poniżej 16′); rok 36 sp — 23 · 31 · 39 · 46′. Z 3,5 m na 32″ podpis 28 sp ma ok. 15′. Podpis 4 zdarzeń na 914 × 411 dp ma ok. 140 dp wysokości, razem z rokiem ok. 190 dp.
**Mapa** (`mapa-050.html`, 16 osób): 19 przeprowadzek w 13 latach (14 dotknięć do „dziś”), najwięcej 5 osób w jednym roku — 1946: czterech jedną drogą i jedna z Litwy, w M2 dwie linie.

**Rekomendacja: K1, N1, F1, Z1, V2, P1, U3** (mapa — M2, [[mapa-migracji]] D27):
- **K1:** podpis mówi o ludziach, których drzewo pokazuje, a + dokłada ich zdarzenia razem z nimi — ta sama zasada co pigułka poziomu (D37). K2 opowiada o osobach spoza drzewa. **Nie
  da:** zdarzeń rodziny, której poziom nie jest wybrany.
- **N1:** rok na ekranie to rok z notatek, a niepewność mówią dopisek i przerywany obrys (D32) — nic nie ginie. N2 wycina 6 ze 147 zdarzeń w makiecie, w prawdziwych notatkach u najstarszych
  pokoleń więcej. **Nie da:** „przed 1900” stoi w 1900, choć mogło być wcześniej.
- **F1:** słowa autora (*„ktoś się urodził, ktoś się ożenił, ktoś zmarł”*) i zdanie, które czyta się na głos; trzy wersje jak w Gramps. F2 nie potrzebuje płci, ale brzmi jak rubryka, a
  „Śmierć” dużymi literami jest cięższa ([[style-b]] reguła 7: bez ponurości). **Nie da:** ładnej formy u osoby bez płci — „(a)” wygląda urzędowo; w danych to wyjątek (płeć ustawia formularz
  osoby — [[ISSUE-025-gender-kinship-together-since]]).
- **Z1:** cel (a) to opowiadanie — podpis musi stać, dopóki autor mówi; przy Z2 i „Średnio” znika po 0,1 s. **Nie da:** zachowania znanego z odtwarzaczy (Media3: „następny” nie zatrzymuje).
- **V2:** przy V1 żadna z 16 osób z pierwszych 12 podpisów nie była na ekranie — rodzina czyta o kimś, kogo nie widzi, a od „Ja” w skali 1 telewizor pokazuje przez pierwsze dekady
  pusty pierścień. V2 przesuwa tylko widok, bez skali, i tylko gdy trzeba. Na mapie zostaje R4: tam osoba poza kadrem wlatuje zza krawędzi, a na drzewie osoby poza ekranem po prostu nie
  widać. **Nie da:** zasady „widok zmieniasz tylko Ty” z K1 — ⏭ ją łamie.
- **P1:** rok i jego zdarzenia w jednym miejscu, a listwa (5 s po każdym ⏭) niczego nie przesuwa. P2 to wzorzec napisów, ale po każdym ⏭ wskakuje nad listwę i po 5 s zjeżdża — ruch na
  telewizorze — a rok i zdarzenia są w dwóch miejscach ekranu. **Nie da:** wolnego lewego górnego rogu — podpis 4 zdarzeń z rokiem zajmuje ok. 190 dp z 411 dp wysokości.
- **U3:** karta tej samej wysokości, suwak krótszy o 19 dp zamiast o 56 dp (U1); rok początku zostaje na listwie i w czytniku. U2 daje najdłuższy suwak, ale zabiera drzewu 48 dp
  (510 → 462 dp). **Nie da:** w karcie roku, od którego zaczyna się historia.

## Candidates — ISSUE-055 (2026-10-23)
> Prototyp `prototyp-055.html` w katalogu tymczasowym sesji `8d325e2e-…\scratchpad` (6 paneli, wymyślona rodzina 16 osób, telefon 412 × 915 dp jak telefon autora
> i podgląd telewizora 16:9 obok; zrzuty `shots055\`). Kierunek z uwag autora po pierwszym pokazie rodzinie ([[ISSUE-055-connect-from-the-tree-and-rotate]]) i z D76.
> Po odpowiedziach autora `ui` przepisuje elementy 1, 4–9, *Navigation*, *States*, *Sketch*, *AC → element* oraz D45, D48, D49 — **dopiero po potwierdzeniu na prototypie**
> (retro 4, R1).

| Panel | Pytanie | Kandydaci | Rekomendacja `ui` |
|---|---|---|---|
| 1 | Skąd „Od” | „Od” = osoba w środku drzewa; kafel „Od” dalej da się zmienić na liście | **autor: „tak”** (D78) |
| 2 | Gdzie „×” | **B1** — baner z nazwą zostaje przez całą ścieżkę, „×” na jego końcu · **B2** — baner 4 s jak dziś, „×” w rogu drzewa | **autor: bez „×”, koniec gestem wstecz** (D79) · **baner: B1** (D80) |
| 2 | Co w trakcie ścieżki | samo drzewo — bez karty z suwakiem i bez + / − poziomu; pasek i zakładki zostają. Dwa palce, przeciąganie, podwójne dotknięcie — ścieżka zostaje; dotknięcie osoby — nic; „Drzewo · Mapa” i „Przesyłaj na telewizor” kończą ją (tam ścieżki nie ma); „Obróć” nie kończy; zmiana danych drzewa kończy (v1.17) | decyzja projektowa |
| 3 | Po wyjściu (wstecz) | suwak wraca na rok sprzed ścieżki; **„Od” zostaje w środku** (zastępuje D45), więc następne „Połącz” zaczyna od tej samej osoby; skala i poziom zostają | **autor: „tak”** (D81) |
| 4–6 | Układ poziomy | **L1 „karta z boku”** — kolumna 352 dp po prawej: pasek, karta, suwak, zakładki; drzewo 563 × 372 dp; baner ścieżki z „×” w kolumnie, w miejscu karty · **L2 „pasek na dole”** — pasek 56 dp u góry, karta w jednym rzędzie z suwakiem na dole (64 dp), bez zakładek; drzewo 915 × 252 dp (w trakcie ścieżki 316 dp minus baner) | ~~**L1**~~ (odrzucony w rundzie 2): drzewo rośnie w dół, a L1 daje mu o 120 dp więcej wysokości; ścieżka Zofia → Leon (4 pokolenia) w L1 w skali ok. 0,68, w L2 ok. 0,43; zakładki zostają |
| 4–6, runda 2 | Układ poziomy po uwadze autora | **L1 odrzucony** — autor na panelu 6: *„gdy telefon jest poziomo chciałbym aby było więcej miejsca na drzewo a mniej na »interface« (…) to z »mapą/osobami/drzewo«”* (kolumna z zakładkami). Interfejs na brzegi: przełącznik „Drzewo · Mapa” i ikony **nad drzewem** w górnym rzędzie (na powierzchni, z obrysem), karta z suwakiem — pasek 64 dp na dole; w trakcie ścieżki pasek znika, a baner z „×” staje w górnym rzędzie między przełącznikiem a ikonami. **L3 „wąska szyna z lewej”** — zakładki Mapa · Osoby · Drzewo w pionowym pasku 72 dp (*navigation rail* — w Androidzie wybór aplikacji, domyślnie na niskim ekranie zostaje dolny pasek, D76); drzewo 843 × 308 dp, w trakcie ścieżki 843 × 372 · **L4 „bez zakładek”** — do innych zakładek przez „Obróć” albo wstecz; drzewo 915 × 308, w trakcie ścieżki 915 × 372 | **autor: L4** (D77); ścieżka 4 pokoleń w L3 i L4 w skali ok. 0,55 (górny rząd 64 dp nad drzewem) — mniej niż L1 w pionie, więcej osób obok siebie |

**Pomiar (prototyp, 412 × 915 dp):** obraz telefonu na telewizorze 16:9 zajmuje pionowo ok. 24% ekranu, poziomo ok. 84%. W poziomie w skali 1 widać 2–3 pokolenia
zamiast 5 — więcej osób obok siebie, mniej w dół. **Przycisk „Obróć”** w pasku obu części (`screen_rotation` — glif do dołożenia do fontu ikon, README `grobing-code` →
*Ikony*): z trzema ikonami w pasku części „Drzewo” przełącznik „Drzewo · Mapa” może stracić napisy na wąskim ekranie przy tekście 100% (reguła z
[[mapa-migracji]] 1 — same ikony, gdy napisy się nie mieszczą) — `dev` mierzy na 360 dp; telefon autora ma 412 dp.

## Candidates — ISSUE-056 (2026-10-23)
> Prototyp `prototyp-056.html` w katalogu tymczasowym sesji `6d4e489c-…\scratchpad` (5 paneli; geometria z sondy na `tree_layout.dart` — kopia algorytmu
> poza repo, `probe056\`; wymyślona rodzina z `lib/dev/fictional_family.dart`, od „Ja” 91 / 113 / 116 osób na poziomach 1–3; zrzuty `shots056\`). Cel autora:
> **„całe drzewo”** — obraz czytelny bez dotykania ([[ISSUE-056-tree-lines-readable]]). Zrzut autora z prawdziwą rodziną — w pozycji tylko struktura.
> Elementy 4, 8 i D-y przepisuje `ui` **dopiero po decyzjach autora na prototypie** (retro 4, R1).

**Pomiar — najtańszy falsyfikator (sonda na kodzie aplikacji, ten sam układ co na telefonie; miejsce osoby 80 dp):**

| Poziom | Osób | Skrzyżowania wg algorytmu (`crossings()`) | Skrzyżowania **narysowane** (kreska × cudza szyna) | Szyn jedna nad drugą (max w przerwie) | Długość szyn |
|---|---|---|---|---|---|
| 1 „Linia krwi” | 91 | 3 | **9** | 2 | 5899 dp |
| 2 „Przez 1 związek” | 113 | 14 | **19** | 3 | 8858 dp |
| 3 „Przez 2 związki” | 116 | 26 | **27** | **4** | 9427 dp |

- **wymyślona rodzina odtwarza obraz ze zrzutu**: na poziomie 3 w jednej przerwie 4 szyny co 7 dp, jedna przez całą szerokość (panel 1);
- **algorytm zmniejsza nie tę liczbę, którą widzi oko**: `crossings()` liczy proste od środka rodziców do dziecka, a ekran rysuje szyny (`_lines`) —
  na poziomie 1 narysowanych przecięć jest 3 razy więcej, niż algorytm „widzi”;
- **wysokości szyn to algorytm lewej krawędzi** (Hashimoto i Stevens 1971, trasowanie kanałów w układach scalonych): najmniej pięter, ale bez patrzenia na
  przecięcia — piętro można wybrać tak, żeby kreski krzyżowały mniej szyn.

**Prior art:**
- **rysowanie rodowodów** (Tores, Barillot, *Optimizing Pedigree Drawing Using Interval Graph Theory*, RECOMB 2000,
  [PDF](https://recomb.org/recomb2000/Posters/pdf/96.pdf)): *„(c) Sibs must be adjacent, but orphan spouses may be inserted within a sibship. (d) Parents are above
  their child sibship. (e) There are no link crossing”*; rodowód z powtórnymi związkami i kilkoma rodzinami często nie da się narysować bez przecięć, a metody
  dokładne *„have been shown to be NP-hard, even in simplest cases”* — stąd heurystyki;
- **liczenie przecięć przy liniach z szynami** (Spönemann, Schulze, Rüegg, von Hanxleden, *Counting Crossings for Layered Hypergraphs*, 2014,
  [raport](https://rtsys.informatik.uni-kiel.de/~biblio/downloads/papers/report-1404.pdf) — **pełnego tekstu nie udało się pobrać; teza z opisu w wyszukiwarce**): przy
  liniach prowadzonych pod kątem prostym przez wspólne odcinki liczba przecięć prostych źle przewiduje przecięcia narysowane — proponują osobne liczenie;
  nasz pomiar to samo zjawisko (3 vs 9);
- **mostki** (*line jumps*) — [draw.io](https://drawio-app.com/blog/draw-io-now-supports-line-jumps/), [Visio](https://support.microsoft.com/en-US/Visio/add-or-remove-connector-line-jumps):
  łuk albo przerwa w miejscu przecięcia mówi, że linie się nie łączą (opis z wyników wyszukiwania; strony nie dało się pobrać w całości);
- [[drzewo]] D8 — rodzina to krata (TimeNets); przecięć może być mniej, nie zero.

| Panel | Pytanie | Kandydat | Liczby (poziom 1 / 2 / 3; narysowane przecięcia, dziś 9 / 19 / 27) | Koszt |
|---|---|---|---|---|
| 1 | Czy wymyślona rodzina pokazuje ten sam kłopot | — dziś | 9 / 19 / 27; 4 szyny w jednej przerwie | — |
| 2 | Czy mostki wystarczą | **B** — piętra szyn wybrane tak, żeby przecięć było najmniej + **mostek** w każdym przecięciu (łuk albo przerwa); nikt się nie przesuwa | 9 / 17 / 22 | tylko rysowanie (`_lines`, malarz); trasa ścieżki idzie po szynach (`pathRoute`) |
| 3 | Czy kolor rodziny pomaga | **E** — linie dzieci każdej pary w jednym z 4 odcieni, sąsiednie szyny nigdy w tym samym; linie par zostają różowe | jak B | rysowanie + zmiana roli koloru: dziś kolor = rodzaj relacji ([[style-b]] *Token roles*), tu 4 odcienie dla rodzic–dziecko; kontrast każdego ≥ 8:1 na tle |
| 4 | Czy nowa kolejność jest warta przesunięć | **D** — kolejność w rzędzie wybrana według narysowanych przecięć i długości szyn (rodzeństwo obok siebie, rodzice nad dziećmi) + B | **4** / 13 / 18; szyny na poziomie 1 krótsze (5388 dp); przesunięte osoby 12 / 35 / 15 | nowy algorytm kolejności; sonda na PC liczy 9–34 s — do wydania potrzebny szybszy; osoby, które autor zna z telefonu, stają gdzie indziej |
| 5 | Które połączenie | B / E / D z mostkami lub bez, telefon i telewizor (obraz telefonu poziomo, cały poziom) | — | na telewizorze przy całym poziomie mostki są za małe, żeby je zobaczyć; kolor zostaje widoczny |

**Decyzja autora (2026-10-23):** *„wybrałbym opcje mostków - łuk, bez osobnych kolorów dla rodzin”* — **B + łuk** (D83, D84), bez E (D85); D bez wyboru → kolejność bez
zmian (D86, potwierdzenie na stopie #1). Panel 1 (czy to ten sam kłopot) — autor przeszedł od razu do wyboru rozwiązania.

## Decisions
- **D1 — drzewo od osoby z przestawianiem środka** (SPIKE-004 D20; kandydat 3 ze SPIKE-002). Na telefonie całe drzewo
  ok. 100 osób jest za szerokie; od osoby widać to, o co się pyta. *Obali:* SPIKE-002 pokaże, że cały widok jest czytelny
  i potrzebny — wtedy dodatkowy tryb „całe drzewo”. **v1.3:** potwierdzone na stopie #1 SPIKE-002 (2026-10-13, *„Tak”*) — K1 nie
  wchodzi do MVP.
- **D2 — poziomy połączeń według „rodziny każdej osoby”** (D20). Autor: *„poziom 1 to nasi partnerzy, dzieci i
  rodzice, poziom 2 to rodzeństwo partnerów, nasze rodzeństwo, rodzice rodziców, itd”*. Reguła z elementu 3 daje
  dokładnie te osoby. *Obali:* autor chce rodzeństwo już na poziomie 1. **v1.23 — zastąpione przez D50** (nowa reguła autora: krew, potem każdy związek).
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
  jak w drzewie (**trafione 2026-10-18 — v1.23, D56**). **v1.8** ([[ISSUE-034-tree-presentation-mode]]): podpowiedź mówi o funkcji, a nie o nazwie kafelka (D26). Przy pierwszym pełnym
  ekranie aplikacji system raz pokazuje własne okno o tym, jak wyjść z pełnego ekranu. To okno systemu, nie aplikacji. Jeśli przesyłanie już trwa,
  zobaczy je też telewizor, więc przed pierwszym pokazem warto raz wejść w tryb bez przesyłania. **v1.10** ([[ISSUE-036-cast-from-the-app]], D30):
  wejście przez ekran przesyłania systemu, a podpowiedź tylko na telefonie bez tego ekranu. Wejście bez przesyłania to ekran systemu i wstecz.
- **D17 — cel dotyku przy oddaleniu poniżej 48 dp** (v1.5). Cel to miejsce osoby × skala drzewa. Przy skali ≥ 0,6 ma ≥ 48 dp (prawie cały
  poziom 3; od 0,55 — 44 dp). Na poziomie 4 ma 38 dp przy 0,48 i 32 dp przy najmniejszej skali 0,4. Węzły nie mogą rosnąć, bo wtedy drzewo
  przestałoby być oddalone. Najmniejsza skala 0,4 trzyma cel ≥ 24 dp — [WCAG 2.2](https://www.w3.org/TR/WCAG22/) SC 2.5.8 Target Size
  (Minimum), AA: *„The size of the target for pointer inputs is at least 24 by 24 CSS pixels”*. Do tego przybliżenie (+) daje cel ≥ 48 dp
  jednym dotknięciem — wyjątek *Equivalent*: *„The function can be achieved through a different control on the same page that meets this
  criterion”*. Pomyłka kosztuje mało: dotknięcie złej osoby tylko przestawia środek. Wyjątek zapisany w [[style-b]] *Thresholds* (v1.24).
  *Obali:* na telefonie autor trafia w złą osobę na poziomie 4 — wtedy najmniejsza skala 0,6. **v1.23 — zmienione przez D52** (skala schodzi niżej, poniżej 24 dp dotknięcie przybliża).
- **D18 — wartości S2 z prototypu** (v1.5). Progi 1,3 · 0,85 · 0,55 i krok 1,45 wybrał `dev` w prototypie SPIKE-002 (*Dev report* →
  *Deviations* 1). Autor przeszedł na nich oddalanie i powrót („ok” na stopie #2, krok 1). Zakres skali 0,4–2,0: dolna granica z D17, a górna
  daje imię 26 sp — większe nie pokazuje nic nowego. *Obali:* progi w ręce, przy szczypaniu na telefonie ([[ISSUE-032-mvp-install]] →
  *Hand checks*, wiersz ze SPIKE-002). **v1.23 — progi zastąpione przez D51** (skala nie zmienia poziomu); krok ×1,45 i górna granica 2,0 zostają.
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
  **(a) Osoba w środku:** dotknięcie dopasowuje poziom 2 od nowa, płynnie, jak powrót drzewa do kadru (D21) (**v1.23 — zmienione przez D56:** przesuwa ją na środek bez zmiany skali i poziomu). Plan ISSUE-034 (D5) mówił „nic”, ale
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
- **D43 — prior art: ścieżka od „mnie”, czas baneru jak Snackbar, komunikat stanu** (**v1.29:** czas baneru ścieżki zastąpiony przez D80 — do wyjścia; „bez ścieżki” — 4 s bez zmian) (v1.16, [[ISSUE-039-connect-two-people]]). **Źródła** (odczyt 2026-10-14):
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
- **D45 — „Do” staje w środku (W2)** — **v1.29: zastąpione przez D81** („Od” zostaje w środku) (v1.16, **decyzja autora na stopie #1 — „Tak”, 2026-10-14**). Przestawienie środka jak po dotknięciu (element 4), więc karta mówi, kim jest „Do” dla mnie, także po zniknięciu baneru, a
  „Pokaż ›” prowadzi do tej osoby. Poziom i kadr liczą się od „Do”; linia dalej biegnie od „Od” (D5). W pomiarze ścieżka przy W2 częściej mieści się w skali poziomu (25 razy nie, przy W1 —
  55). *Obali:* autor chce, żeby po końcu podświetlenia drzewo było przy „Od” — wtedy W1.
- **D46 — długa ścieżka: drzewo maleje, aż cała ścieżka się zmieści (F2)** (v1.16, **decyzja autora na stopie #1 — „Tak”, 2026-10-14**). Kadr najpierw w skali poziomu (S2); gdy ścieżka się w niej nie mieści — mniejsza
  skala, najmniej 0,15 (w makiecie najmniej 0,34 przy 100% i 0,17 przy 200%). Linia ma tę samą grubość przy każdej skali. Po końcu podświetlenia skala wraca do 0,4 (dół zakresu S2)
  z osobą w środku (**v1.23 — zmienione przez D57:** skala i poziom zostają, bo skala nie jest już związana z poziomem). Imiona ze ścieżki mają pierwszeństwo przy chowaniu nakładających się (I2). Kadr liczy skrajne osoby ścieżki z ich miejscem; `dev` sprawdza, czy imię na skraju nie
  wychodzi poza ekran (w makiecie przy 200% wyszło — imię rośnie o 1/skala). *Obali:* na prawdziwej rodzinie osoby spoza ścieżki jako kropki gubią kontekst — wtedy F1.
  **v1.17** (przegląd `ui` [[ISSUE-039-connect-two-people]], odstępstwo 2 `dev`, 2026-10-14): **na poziomie 1 kadr w skali 1,3**, czyli na dole zakresu poziomu, a nie „aż do 2,0”. Krótka
  ścieżka (Ja → córka) w skali 2,0 miałaby okręgi 88 dp i imiona 26 sp — większe niż w każdym innym widoku drzewa, które startuje w skali 1. Na pozostałych poziomach kadr bierze
  największą skalę poziomu, w której ścieżka się mieści. Tak było w makiecie; na emulatorze — zrzut `29` (Ja → Zofia).
- **D47 — baner, gdy „Od” to nie Ty: dwie linie bez odmiany imion (O2)** (v1.16, **decyzja autora na stopie #1 — „Tak”, 2026-10-14**). Pierwsza linia: „Imię Nazwisko → Imię Nazwisko” w mianowniku (bez „z d.”; „Ja”,
  gdy to Ty). Druga: nazwa z tych samych odcinków co w G2 (D6, D12), bez zaimka przy ostatnim odcinku — „Wnuczka”, „Siostrzenica bratowej”, „Ciotka (siostra taty)”. Słownik się nie
  zmienia; odpada tylko „mój / moja / mojej / mojego”. Gdy „Od” to Ty — jedna linia jak w AC-3. *Obali:* autor czyta drugą linię bez pierwszej i myli kierunek („Wnuczka” — czyja?)
  — wtedy O3 z tabelą odmiany imion i testami.
- **D48 — ścieżka przestawia rok na „dziś” (Y1)** — **v1.29: po wyjściu wraca rok sprzed ścieżki (D81)** (v1.16, **decyzja autora na stopie #1 — „Tak”, 2026-10-14**; **zmienia D37** dla jednego wejścia). Wybór „Do” zatrzymuje ▶ i ustawia suwak na „dziś”, jak wejście z paska.
  Pokrewieństwo nie zależy od roku, a w roku Y część ścieżki byłaby pustymi pierścieniami bez imion. *Obali:* autor przygotowuje opowieść w roku Y i chce w nim zostać — wtedy Y2.
- **D49 — „Połącz dwie osoby”: decyzje projektowe** (v1.16, bez pytania; „tak” na stopie #1 przyjmuje je z planem):
  - **poziom:** najniższy z całą ścieżką od osoby w środku (**v1.23, D57:** tylko w górę — wybrany poziom nie maleje; każda połączona osoba ma poziom, więc „poziom 4 i brakujące osoby” odpada); dalej niż poziom 4 — poziom 4 i brakujące osoby ścieżki (od „Ja” 9 ze 105; we wszystkich parach 60%, bo od osoby na brzegu
    rodziny poziomy są małe);
  - **linia po liniach rodziny**, a nie na skos: autor mówił *„powoli linie idą odemnie do kolejnych osób”* ([[SPIKE-004-mvp-flow-prototype]] D26), a skos przecinałby inne osoby;
  - **baner, gdy linia dojdzie do „Do”** — nazwa na końcu drogi, nie na początku; kadr zostawia mu miejsce u góry;
  - **koniec podświetlenia** (**v1.29: zastąpione przez D79** — tylko wstecz i działania bez miejsca na ścieżkę)**:** każde działanie, które zmienia drzewo (dotknięcie, wstecz, poziom, rok, ▶, przesyłanie). Przeciąganie nie kończy, żeby dało się obejrzeć ścieżkę. Pierwsze
    dotknięcie osoby tylko kończy podświetlenie, żeby przypadkowe dotknięcie nie przestawiło środka. **v1.17** (przegląd `ui` [[ISSUE-039-connect-two-people]], odstępstwo 3 `dev`): kończy je
    też **zmiana danych drzewa** — osoby ścieżki mogły zniknąć albo zmienić rodzinę, a linia biegłaby po starym układzie;
  - **wyszarzenie** (v1.17, odstępstwo 5 z przeglądu ISSUE-039 — w *Dev report* go nie ma): przy 30% są osoby spoza ścieżki i **wszystkie** linie rodziny ze śladami, także osób ze ścieżki.
    Linie to jedna warstwa (plan D7: wyszarzenie grupy jedną warstwą), a linia rodziny przy osobie ze ścieżki prowadzi albo do osoby wyszarzonej, albo leży pod linią w akcencie. Ślad
    dalszej rodziny przy osobie ze ścieżki w czasie podświetlenia niczego nie dodaje. *Obali:* autor na emulatorze gubi, gdzie osoba ze ścieżki ma dalszą rodzinę — wtedy linie i ślady osób
    ze ścieżki w pełnym kryciu, w osobnej warstwie;
  - **okno:** okno z dwoma kaflami, jak chciał autor (*„pojawia mi się pop-up z dwoma kaflami”*, SPIKE-004 D26). Lista — tryb wyboru jak „Która osoba to Ty?” (`MePickerScreen`,
    [[style-b]] reguła 12), bez osoby z drugiego kafla (ta sama osoba nie ma ścieżki). Każde otwarcie zaczyna od „Ja” (**v1.29: zastąpione przez D78** — od osoby w środku);
  - **tryb prezentacji bez „Połącz dwie osoby”** w MVP — nie ma tam paska z ikonami, a „Przesyłaj na telewizor” kończy podświetlenie. Ścieżka na telewizorze to wejście do
    [[2026-10-14-opowiesc-rodziny-i-wieniec]];
  - **pigułka poziomu** nie pokazuje się przy przejściu do ścieżki — w tym miejscu stoi baner.

  *Obali:* autor na emulatorze chce kończyć podświetlenie tylko przez wstecz albo chce, żeby okno pamiętało ostatnie „Od”.

- **D50 — poziomy według związków (M2)** (v1.23, [[ISSUE-049-tree-levels-and-zoom]]; **zastępuje D2**; *Open* 11a; **decyzja autora na stopie #1 — „tak”, 2026-10-19**). Autor: *„poziom pierwszy to tylko „nasza linia krwi”,
  a w kolejnych poziomach dodawana jest np. rodzina żony brata itd., na jeszcze kolejnym rodzina męża siostry żony brata”*. **Reguła:** poziom 1 — krewni osoby w środku (wspólny przodek,
  KRO art. 617) z ich mężami, żonami i partnerami; poziom k + 1 — krewni każdego męża, żony i partnera spoza krwi z poziomu k, z ich mężami, żonami i partnerami. „Związek” to oba tryby
  z [[rodzina]] (małżeństwo i „razem”), także zakończony — rozstanie nie odcina dzieci. Liczone z relacji przy otwarciu, bez zmiany bazy. **Dlaczego M2, a nie M1:** przy M1 na poziomie 1
  linia do dzieci brata wychodzi od niego samego, Twoje dzieci są bez Kasi, a przykłady autora (rodzina żony brata — 2, rodzina męża siostry żony brata — 3) trafiają tylko przy M2;
  Gramps trzyma potomków z małżonkami jako jeden zbiór (*Candidates — ISSUE-049* → *Prior art*). **Nie da:** poziomu 1 jako samej krwi — 91 zamiast 67 osób od „Ja”. *Obali:* autor na
  makiecie albo emulatorze chce na poziomie 1 widzieć tylko krew — wtedy M1.
- **D51 — przybliżanie i oddalanie to sam widok** (v1.23; **zastępuje S2 i D18**, rozszerza D7). Gesty, + / − i podwójne dotknięcie zmieniają tylko skalę. **Zakres:** od całego
  pokazanego poziomu na ekranie (24 dp marginesu; najwyżej 0,4, najmniej 0,08) do 2,0 — autor chce *„widzieć „big picture” i przybliżać sobie szczegóły bez znikania członków mojej
  rodziny”*. Krok ×1,45 zostaje z D18 (od skali 1 do całości 6–7 dotknięć). **Nie da:** czytelnego całego obrazu na telefonie pionowo — przy 91 osobach okręgi ok. 5 dp i ok. 10 imion;
  czytelny jest na telewizorze (*Candidates — ISSUE-049* → *Pomiar*). *Obali:* na telefonie autor nie oddala do całości, bo nic tam nie widzi — wtedy dolna granica wyżej (np. 0,2) i cały
  obraz tylko w trybie prezentacji. **v1.24** (odstępstwo 1 `dev`, przegląd `ui`): na dolnej granicy cały poziom stoi na środku obszaru drzewa — po −, po geście dwóch palców
  po 0,4 s spokoju i gdy skala rośnie do nowej granicy; „cały obraz” znaczy cały, a nie przesunięty w bok z osobą uciętą przy krawędzi. Ze ścieżką — jej kadr.
  **v1.25 (D58):** + / − przybliżania usunięte decyzją autora — zostają dwa palce, podwójne dotknięcie i dotknięcie małego drzewa (D52); oddalają tylko dwa palce.
- **D52 — przy celu poniżej 24 dp dotknięcie przybliża** (v1.23; **zmienia D17**). Do v1.22 najmniejsza skala 0,4 trzymała cel ≥ 24 dp ([WCAG 2.2](https://www.w3.org/TR/WCAG22/) SC 2.5.8).
  Teraz skala schodzi do ok. 0,1, a cel do ok. 8 dp — dotknięcie trafiałoby w sąsiada. Gdy miejsce osoby × skala < 24 dp, dotknięcie drzewa przybliża w to miejsce do 0,45 (cel 36 dp
  przy miejscu 80 dp, 43 dp przy 96 dp), a dopiero tam dotknięcie osoby stawia ją w środku — jak skupienie na mapie migracji ([[mapa-migracji]] 4a: dotknięcie przybliża). Wybór osoby
  ma więc zawsze cel ≥ 24 dp; [[style-b]] *Thresholds* v1.44. *Obali:* autor chce z całego obrazu dotknąć osoby i od razu mieć ją w środku — wtedy dotknięcie wybiera najbliższą osobę
  w promieniu 24 dp, a pomyłkę naprawia karta.
- **D53 — przełącznik poziomu: etykieta z nazwą i lista (P2)** (v1.23; *Open* 11b; **decyzja autora na stopie #1 — „tak”, 2026-10-19**). Stare „− Poziom 2 +” autor uznał za nieestetyczne ([[SPIKE-004-mvp-flow-prototype]] D25, v1.1). Etykieta w lewym dolnym rogu
  stoi naprzeciw + / −, więc góra drzewa zostaje dla pigułki i baneru „Połącz dwie osoby”, a nazwa mówi, co pokazuje drzewo, bez dotykania. Lista to ten sam wzorzec co arkusz rodów
  ([[wieniec]] E2: wiersz, `check` w akcencie). Koszt: dwa dotknięcia na zmianę — poziom zmienia się rzadko, a przybliżanie (częste) jest jednym gestem. Ikona `arrow_drop_down` jest w
  foncie aplikacji (`Glyphs.arrowDropDown`). *Obali:* autor przełącza poziomy często i liczy dotknięcia — wtedy P1. **v1.25 — zastąpione przez D58:** na stopie #2 autor
  zamienił etykietę i listę na proste + / − (bliżej P3 niż P1: jeden dotyk na krok, ale dwa przyciski, bez numerów).
- **D54 — nazwy poziomów (N2)** (v1.23; *Open* 11c; **decyzja autora na stopie #1 — „tak”, 2026-10-19**). „Linia krwi” to słowa autora; „Przez 1 związek”, „Przez 2 związki” mówią regułę i działają dla dowolnej liczby poziomów
  (od Kasi w makiecie są cztery). „Związek”, bo tak aplikacja nazywa oba tryby ([[rodzina]]); „małżeństwo” myliłoby przy parach „razem”. **Nie da:** nazw, które same opowiadają, kto
  dochodzi — to robi opis na liście („do tego rodziny mężów, żon i partnerów, np. rodzina żony brata”). *Obali:* autor poda własne słowa (np. „Z rodzinami małżonków”) — wtedy jego.
- **D55 — po zmianie poziomu skala i środek zostają (K1)** (v1.23; *Open* 11d; **decyzja autora na stopie #1 — „tak”, 2026-10-19**). Ta sama zasada co R4 na mapie migracji: widok zmieniasz Ty. Pigułka mówi, ile osób doszło albo
  ubyło, więc nowe osoby poza ekranem nie giną bez śladu. Gdy po zmianie nikt nie jest w kadrze, działa D21 (powrót do osoby w środku). **Nie da:** całego nowego poziomu bez oddalania.
  *Obali:* autor po każdej zmianie poziomu od razu oddala — wtedy K2.
- **D56 — tryb prezentacji: gesty, poziom i skala z telefonu (T2)** (v1.23, AC-4; **zmienia D16 i D25 a**; *Open* 11e; **decyzja autora na stopie #1 — „tak”, 2026-10-19**). D16 miało *Obali:* „autor chce oddalać na telewizorze” —
  trafione. Dwa palce na telefonie przybliżają i oddalają, na listwie są − / + (SC 2.5.1) i przełącznik poziomu; podwójnego dotknięcia nie ma, bo pusty dotyk pokazuje sterowanie. Wejście
  bierze poziom i skalę z telefonu (jak rok — Z2, D42), z osobą w środku na środku ekranu; wyjście oddaje je z powrotem. Dotknięcie osoby w środku przesuwa ją na środek bez zmiany skali
  (D25 a dopasowywało poziom 2 — po przeciągnięciu to dalej droga z powrotem). Po co T2: autor opowiada rodzinie od linii krwi i dokłada rodziny bez wychodzenia z pokazu — przy T1 każda
  zmiana to wyjście i ponowne wejście przez ekran przesyłania (D30). **Nie da:** schowania listy przed telewizorem — przy przesyłaniu ekranu rodzina widzi ją przez chwilę.
  **v1.24** (testy `qa`, przegląd `ui`): etykieta i − / + tylko na listwie od 560 dp (telefon poziomo), etykieta najwyżej 30% listwy z „…” — z czytnikiem ekranu sterowanie
  przychodzi przed obrotem telefonu, a w pionie rząd czasu nie mieści obu; po zmianie poziomu w trybie bez pigułki (odstępstwo 3 `dev`). **v1.25 (D58):** na listwie − / + poziomu zamiast etykiety i przybliżania;
  pigułka jest także tu, pod górnym rzędem sterowania.
- **D57 — decyzje projektowe bez pytania** (v1.23; „tak” na stopie #1 przyjmuje je z planem):
  - **start:** wejście z paska i „Pokaż w drzewie” — skala 1; poziom przy pierwszym uruchomieniu 1, potem wybrany, dopóki aplikacja działa (jak tempo, D41). Autor zaczyna od swojej krwi,
    a raz wybranego poziomu nie ustawia przy każdym wejściu. *Obali:* autor co wejście przełącza na 2 — wtedy start na 2;
  - **osoba w środku z mniejszą liczbą poziomów:** drzewo pokazuje jej najwyższy, etykieta i lista — jej poziomy (v1.25, D58: + nieaktywne); wybór wraca przy osobie, która go ma;
  - **pigułka po zmianie:** nazwa, liczba osób w roku suwaka (D37) i ile doszło albo ubyło, ok. 1,8 s; w trybie prezentacji jej nie ma — u góry stoi sterowanie, a nazwę mówi
    etykieta na listwie (v1.24, odstępstwo 3 `dev`). **v1.25 (D58):** jest także w trybie prezentacji, pod górnym rzędem sterowania — etykiety już nie ma;
  - **imiona przy oddalaniu (I2, D27):** pierwszeństwo według kroków w rodzinie od osoby w środku (dawne poziomy D2), nie według nowego poziomu — na poziomie 1 bywa 91 osób, a imię
    brata ma być ważniejsze niż imię kuzyna dziadka;
  - **„Połącz dwie osoby” (zmienia D46 v1.17 i D49 „poziom”):** poziom rośnie do najniższego z całą ścieżką, ale nie maleje — wybór autora zostaje; kadr bez zmian w zasadzie (F2, skala
    najwyżej 1,3); po końcu podświetlenia skala i poziom zostają, bo skala nie jest już związana z poziomem. **v1.24** (test `qa`): kadr może zejść poniżej granicy
    całego poziomu, do 0,08 — granica liczy miejsca osób, a imiona ścieżki (I2) muszą zostać na ekranie w całości;
  - **ślad dalszej rodziny (D9):** bez zmian w kształcie; „poza widokiem” znaczy teraz „poza wybranym poziomem”.
- **D58 — poziom zmieniają + / −, przybliżania nie ma na przyciskach** (v1.25, stop #2 [[ISSUE-049-tree-levels-and-zoom]]; **zastępuje P2 z D53**, zmienia D51, D56 i odstępstwo 3
  z v1.24; **decyzja autora, 2026-10-19**). Autor na emulatorze: *„jednak zamiast "kogo pokazać na drzewie" chciałbym mieć prosty "+" "-"”* · *„Obecny "+" "-" można
  zastąpić/usunąć bo wystarczy funkcja ręcznego zoom-in/out”* · *„Te komentarze odnoszą się tak samo do widoku w aplikacji i na telewizorze”*. Wynik: + / − w prawym dolnym
  rogu (miejsce dawnych + / − przybliżania) i na listwie trybu prezentacji zmieniają poziom o jeden, na krańcach są nieaktywne. Bez napisu między przyciskami — nazwę mówi
  pigułka, więc pigułka jest też na telewizorze, pod górnym rzędem sterowania (w v1.24 jej tam nie było, bo nazwę mówiła etykieta). Przybliżają dwa palce, podwójne dotknięcie
  i dotknięcie małego drzewa (D52); **oddalają tylko dwa palce**. **Nie da:** (a) nazwy poziomu na stałe — po 1,8 s pigułki o poziomie mówi tylko to, które z + / − jest
  aktywne; (b) opisu, kto dochodzi (był na liście: „do tego rodziny mężów, żon i partnerów…”); (c) oddalania jednym dotknięciem — [[style-b]] v1.46, wyjątek od SC 2.5.1:
  z czytnikiem ekranu albo Switch Access drzewa nie da się oddalić. *Obali:* (a) autor albo rodzina pytają „który to poziom?” — wtedy nazwa przy + / − (np. mała etykieta nad +);
  (c) ktoś z rodziny nie umie oddalić dwoma palcami albo autor trzyma telefon jedną ręką — wtedy wraca oddalanie jednym dotknięciem (np. przycisk „cały poziom” albo podwójne
  dotknięcie przy największej skali).
- **D59 — zdarzenia osób z wybranego poziomu (K1)** (v1.26, [[ISSUE-050-next-event]]; *Open* 12; **decyzja autora na stopie #1 — „tak”, 2026-10-19**). ⏭ i podpis biorą narodziny i śmierć
  osób z bieżącego poziomu (3), a związki — gdy obie osoby są na poziomie. Dlaczego: podpis ma mówić o ludziach, których rodzina widzi na drzewie; + dokłada rodzinę razem z jej zdarzeniami,
  jak pigułka poziomu liczy tylko pokazane osoby (D37). Odrzucone: zdarzenia osób w kadrze — podpis zmieniałby się od samego przesunięcia palcem. **Nie da:** zdarzeń rodziny poza
  wybranym poziomem. *Obali:* autor przy telewizorze dokłada poziom tylko po to, żeby pojawiło się jedno zdarzenie — wtedy K2.
- **D60 — data niepewna w roku zapisanym, z dopiskiem (N1); bez roku — nie ma zdarzenia** (v1.26; *Open* 12; **decyzja autora na stopie #1 — „tak”, 2026-10-19**). Zdarzenie stoi w roku z daty: „ok. 1870” w 1870,
  „między 1895 a 1900” w 1895, „przed 1900” i „po 1945” w roku z daty; podpis kończy dopisek w nawiasie, a na drzewie osoba ma w tym roku przerywany obrys (D32). Data bez roku nie jest
  zdarzeniem — okna z D31, D32 służą tylko obrysowi (aplikacja nie zgaduje dat — D22). Dlaczego: rok na ekranie to rok z notatek, a niepewność mówią dopisek i kształt. **Nie da:**
  „przed 1900” stoi w 1900, choć mogło być wcześniej. *Obali:* rodzina przy telewizorze czyta „(ok. 1870)” jako pewną datę — wtedy N2 albo „około” pełnym słowem.
- **D61 — linia zdarzenia: czasownik według płci (F1)** (v1.26; *Open* 12; **decyzja autora na stopie #1 — „tak”, 2026-10-19**). „Urodził się / Urodziła się / Urodził(a) się”, „Zmarł / Zmarła / Zmarł(a)”, „Ślub: … i …”,
  „Razem: … i …” — trzy wersje jak w Gramps (*Candidates — ISSUE-050*). Decyzje projektowe w tej samej linii: imię i nazwisko jak w karcie, bez „z d.” (krócej na telewizorze, a rodzina zna
  osobę pod tym nazwiskiem); w parze kobieta pierwsza, jak w AC-1; imię z nazwiskiem i dopisek trzymają się razem, linia łamie się przed „ i ” ([[style-b]] reguła 6). **Nie da:** ładnej formy u
  osoby bez płci. *Obali:* (a) „(a)” razi autora — wtedy przy osobie bez płci rzeczownik („Narodziny: …”); (b) rodzina myli kobietę po ślubie przy jej narodzinach — wtedy przy narodzinach
  nazwisko rodowe. **v1.27 (odstępstwo 3 `dev`, przegląd `ui` [[ISSUE-050-next-event]]):** „Urodził się”, „Urodziła się”, „Urodził(a) się” z twardą spacją przed „się” — linia nie zaczyna się od
  „się Jan…”, a łamie się dopiero przed imieniem. To poza [[style-b]] regułą 6 (słowa jednoliterowe, separatory, dopiski): jedna instancja — do reguły przy drugiej.
- **D62 — ⏭ zatrzymuje ▶ (Z1)** (v1.26; *Open* 12; **decyzja autora na stopie #1 — „tak”, 2026-10-19**). Gdy historia biegnie, ⏭ zatrzymuje ją na najbliższym zdarzeniu; ▶ potem jedzie dalej od tego roku (element 6:
  ▶ z roku innego niż „dziś”). Dlaczego: cel (a) — podpis ma stać, dopóki autor opowiada; przy biegnącej historii („Średnio” — 0,1 s na rok) nie da się go przeczytać. Media3 robi inaczej
  (*Candidates — ISSUE-050*), ale tam „następny” prowadzi do rozdziału filmu, który dalej gra. **Nie da:** ⏭ jako przyspieszenia biegnącej historii. *Obali:* autor przy telewizorze po ⏭
  zawsze od razu dotyka ▶ — wtedy Z2.
- **D63 — drzewo podjeżdża do osób z podpisu (V2)** (v1.26; *Open* 12; **decyzja autora na stopie #1 — „tak”, 2026-10-19**; **zmienia zasadę K1 — D55 — dla jednego wejścia**). Gdy ktoś z podpisu (z bieżącej strony) jest
  poza obszarem drzewa, który zostaje bez podpisu, widok jedzie tak, że grupa stoi na środku tego obszaru (ok. 0,45 s; przy ograniczeniu animacji od razu — D36), a gdy się nie mieści — na
  pierwszej osobie; skala i osoba w środku zostają. Dlaczego: pomiar — przy V1 od „Ja” w skali 1 żadna z 16 osób z pierwszych 12 podpisów nie była na ekranie (V2: 14 z 16), a telewizor
  pokazywał pusty pierścień „Ja” sprzed narodzin. Mapa zostaje przy R4 ([[mapa-migracji]] D29): tam osoba poza kadrem wlatuje zza krawędzi, a na drzewie osoby poza ekranem nie widać. **Nie
  da:** widoku, który zmienia tylko autor. *Obali:* autor ustawia drzewo przed opowieścią (np. cały poziom na telewizorze), a ⏭ mu je przestawia — wtedy V1 albo podjazd tylko przy skali
  powyżej całego poziomu. **v1.27 (odstępstwo 2 `dev`, przegląd `ui` [[ISSUE-050-next-event]]): grupa 8 dp pod podpisem**, w poziomie na środku obszaru; za szeroka — pierwsza osoba i tak
  w obszarze; ktoś na + / − w rogu telefonu — grupa w lewo, dopóki pierwsza osoba się mieści; za wysoka — rząd pierwszej osoby u góry. Dlaczego: na emulatorze przy tekście 200% na 360 dp
  środek obszaru wypadał na wysokości + / − poziomu i „Tomasz” stał pod „+”, a obszar bez całej kolumny przycisków był za wąski na parę; pod podpisem ludzie stoją przy słowach o nich, na
  telefonie i na telewizorze tak samo. Pomiar od „Ja” w skali 1: po każdym ⏭ co najmniej jedna osoba z podpisu na ekranie, razem 123 ze 178 (69% — reszta to grupy szersze niż ekran, np.
  ślub i trzy narodziny w różnych gałęziach). **Nie da:** rzędu nad grupą — rodzice nowo narodzonych bywają pod dymkiem albo za górną krawędzią (zrzuty 1955 i 2010). *Obali:* autor albo
  rodzina pytają przy telewizorze „czyje to dziecko?”, bo rodziców zasłania podpis — wtedy grupa niżej, z rzędem rodziców nad nią (np. środek obszaru bez pasa + / − u dołu). **v1.28 (D72):** w trybie prezentacji pod rokiem nie ma podpisu — obszar zaczyna się 12 dp pod tabliczką roku i kończy 24 dp nad listwą z linią podpisu.
- **D64 — podpis na telewizorze pod rokiem w rogu (P1), 28 sp** (v1.26; *Open* 12; **decyzja autora na stopie #1 — „tak”, 2026-10-19**). Tekst 48 dp od lewej (margines z D38), 8 dp pod tabliczką roku, najwyżej 62%
  szerokości, na tabliczce w kolorze tła (linie drzewa pod napisem, D23); 28 sp — M3 *headline medium*, z 3 m na 32″ ok. 18′ (minimum 16′ — D38; [[style-b]] v1.47), najwyżej 1,3× z tekstem
  systemu. Dlaczego: rok i jego zdarzenia w jednym miejscu, a listwa (5 s po każdym ⏭) niczego nie przesuwa; P2 (napisy na dole) po każdym ⏭ wskakuje nad listwę i zjeżdża po 5 s. **Nie
  da:** wolnego lewego górnego rogu (4 zdarzenia z rokiem — ok. 190 dp z 411 dp). *Obali:* na prawdziwej rodzinie podpis zasłania osobę, o której mówi — wtedy P2 albo podpis po
  przeciwnej stronie osób z podpisu. **v1.27 (odstępstwo 1 `dev`, przegląd `ui` [[ISSUE-050-next-event]]):** tabliczka podpisu stoi 48 dp od lewej, jak tabliczka roku, z tym samym wcięciem
  6 dp, więc tekst zaczyna się 54 dp od lewej, równo z cyframi roku (v1.26: „tekst 48 dp od lewej”). Rok i jego zdarzenia mają jedną lewą krawędź (zrzut `tv03`); margines z D38 (≥ 48 dp)
  zostaje — liczony od tabliczki, jak przy roku. Emulator: 4 zdarzenia — 447 × 146 dp (49% szerokości), dół ok. 221 dp. **v1.28 — zastąpione przez D72** (stop #2 [[ISSUE-050-next-event]], runda 1, decyzja autora *„B”*): podpis pod rokiem zasłaniał drzewo na telewizorze (*„niech zostanie na telefonie (aby nie przysłaniała drzewa na telewizorze)”*).
- **D65 — ⏭ w karcie: jeden rząd bez roku początku (U3)** (v1.26; *Open* 12; **decyzja autora na stopie #1 — „tak”, 2026-10-19**; **zmienia element 6**). Przy tekście poniżej 150% rok początku znika z karty (zostaje na listwie
  trybu prezentacji i w czytniku — suwak mówi „Rok” z wartością); przy ≥ 150% układ dwóch rzędów jak dotąd, z ⏭ obok ▶. Dlaczego: ⏭ zabiera 48 dp — U1 skraca tor do ok. 25 dp (przeciąganie
  prawie po omacku), U2 zabiera drzewu 48 dp wysokości; U3 skraca suwak o 19 dp (tor ok. 62 zamiast 81–89 dp), a rok początku to najmniej potrzebna informacja w karcie — początek widać
  pod palcem. **Nie da:** w karcie roku, od którego zaczyna się historia. *Obali:* autor szuka w karcie roku początku albo ma kłopot z przeciąganiem na krótszym suwaku — wtedy U2.
- **D66 — najwyżej 4 zdarzenia naraz, dalszy ciąg tym samym ⏭** (v1.26, decyzja projektowa; „tak” na stopie #1 przyjmuje ją z planem). Gdy w roku jest więcej zdarzeń, ostatnia linia
  mówi „Jeszcze 3 w tym roku”, a ⏭ pokazuje dalszy ciąg tego roku, zanim przejdzie dalej. Dlaczego: pomiar — na „Linii krwi” od „Ja” 5 lat ma więcej niż 4 zdarzenia, na dalszych
  poziomach do 8 w jednym roku; 8 linii po 28 sp zakryłoby telewizor, a „i jeszcze N” schowałoby część historii przed rodziną. Każde dotknięcie to porcja do opowiedzenia. **Nie da:**
  całego roku naraz. *Obali:* autor gubi się, że ⏭ nie zmieniło roku — wtedy wszystkie zdarzenia roku na raz, w dwóch kolumnach.
- **D67 — z „dziś” od pierwszego zdarzenia, po ostatnim „dziś” i od nowa** (v1.26, decyzja projektowa; AC-4). ⏭ z „dziś” prowadzi do pierwszego zdarzenia (jak ▶ z „dziś” zaczyna od
  początku — D34), po ostatnim — „dziś” z podpisem „To wszystkie zdarzenia z datą.”, a następne dotknięcie zaczyna od początku. Dlaczego: „dziś” to domyślny rok drzewa, więc ⏭ nie może tam
  być martwe; podpis końca mówi, że dalej nic nie ma (AC-4), bez błędu i bez nieaktywnego przycisku. **Nie da:** zatrzymania na końcu — kolejne dotknięcie cofa do 1868. *Obali:* autor przy
  telewizorze przypadkiem zaczyna od nowa — wtedy na „dziś” po końcu ⏭ nieaktywne do zmiany roku.
- **D68 — które zdarzenia** (v1.26, decyzja projektowa). Narodziny, śmierć, „razem” (gdy jest datą przed ślubem albo bez ślubu) i ślub — lista autora (*„ktoś się urodził, ktoś się ożenił,
  ktoś zmarł”*) i dwa tryby związku aplikacji ([[rodzina]]). Koniec związku nie jest zdarzeniem w podpisie — nie było go na liście, a rozwód czytany rodzinie z kanapy to temat do
  opowiedzenia, nie do podpisu; na drzewie „//” jest dalej (E3 — D35). Pochówek bez daty śmierci też nie. **Nie da:** rozstań w historii. *Obali:* autor pyta o rozstania — wtedy
  „Rozstanie: … i …”.
- **D69 — podpis bez odliczania, zostaje, dopóki rok stoi** (v1.26, decyzja projektowa). Znika przy zmianie roku (suwak, ▶), poziomu, części i przy ścieżce „Połącz dwie osoby”; dotknięcie
  osoby, przybliżanie i przesuwanie go nie zabierają; przechodzi z rokiem do trybu prezentacji i z niego wraca (Z2 — D42). Dlaczego: tempo opowieści jest autora — napisy mają najwyżej 7 s
  (*Candidates — ISSUE-050*), ale tam tempo nadaje film. **Nie da:** drzewa bez podpisu, póki stoi rok — trzeba ruszyć suwak. *Obali:* autor chce pokazać drzewo w tym roku bez podpisu —
  wtedy pusty dotyk chowa podpis razem ze sterowaniem.
- **D70 — bez wyróżniania osób z podpisu na drzewie** (v1.26, decyzja projektowa). Osoby dochodzą przenikaniem jak przy suwaku (element 6); pierścień i poświata zostają dla osoby w
  środku i ścieżki ([[style-b]] reguła 2). Zbliżenia i efekty na zdarzeniach zostają w INBOX, po instalacji ([[2026-10-14-opowiesc-rodziny-i-wieniec]] c). **Nie da:** odpowiedzi „który to?”
  na telewizorze — imię 13 sp czyta się z bliska (D38). *Obali:* rodzina przy telewizorze pyta, która osoba to ta z podpisu — wtedy krótka poświata na osobach z podpisu. **v1.28 — zastąpione przez D73** (stop #2 [[ISSUE-050-next-event]], runda 1): autor na zbudowanym ekranie poprosił wprost — *„obwódka wokół osoby i/lub podświetlona relacja”*, *„obwódka / laur "lśniały"”*.
- **D71 — ⏭: znak, forma, czytnik** (v1.26, decyzja projektowa). `skip_next` — znak „następny” z odtwarzaczy (Media3), w akcencie bez wypełnienia, bo ▶ jest jedynym wypełnionym (reguła 1);
  cel 48 dp, `tooltip` i czytnik „Następne zdarzenie”; podpis jest regionem na żywo (jak pigułka poziomu, D43), więc po ⏭ czytnik czyta rok i zdarzenia zamiast osobnego „Rok 1952”. Na
  poziomie bez żadnego zdarzenia z datą ⏭ **nie ma**: nieaktywna ikona różniłaby się od aktywnej tylko kolorem (1,60:1 — SC 1.4.1), a taki poziom to wyjątek (osoba bez dat i rodziny).
  Glif trzeba dodać do fontu ikon aplikacji (`tool/icons/build_symbols.py` — [[style-b]] reguła 3). **Nie da:** ⏭ zawsze w tym samym miejscu — przy takim poziomie rząd wraca do układu
  sprzed v1.26. *Obali:* autor szuka ⏭ przy osobie bez dat — wtedy nieaktywne z przekreśleniem.
- **D72 — podpis w trybie prezentacji: linia na listwie (B)** (v1.28; stop #2 [[ISSUE-050-next-event]], runda 1; **decyzja autora — *„B”*, 2026-10-19**; zastępuje D64). Po ⏭ nad rzędem
  ▶ ⏭ listwy stoi drobna linia: nagłówek „W 1955 · 1 z 2” (13 sp, tekst pomocniczy), zdarzenia strony rozdzielone „ · ” (14 sp, imiona półgrube), „Jeszcze 2 w tym roku”; znika z
  listwą po 5 s (D40), pusty dotyk pokazuje ją znowu, dopóki stoi podpis (D69); z czytnikiem ekranu listwa się nie chowa (v1.15), a linia jest regionem na żywo (D71). Pod rokiem w rogu
  nic nie stoi, a V2 (D63) liczy obszar od tabliczki roku do listwy. Dlaczego: autor — *„sama informacja kto się urodził itd. niech zostanie na telefonie (aby nie przysłaniała drzewa na
  telewizorze)”*; telewizor dostaje kopię ekranu telefonu (przesyłanie ekranu — D11, D29), więc „tylko na telefonie” w trybie prezentacji nie istnieje. A — w trybie prezentacji bez
  podpisu — zostawiało autora bez słów w ręce; B daje mu ściągę na 5 s w miejscu, które i tak pojawia się po każdym dotknięciu. 14 sp, nie 28: linię czyta autor z ręki, nie rodzina z
  kanapy — rodzina ma rok (36 sp) i świecące osoby (D73). **Nie da:** słów na telewizorze dla rodziny — kto się urodził, mówi autor; przy tekście 200% na telefonie 360 dp strona 4 zdarzeń (1955) ma 4 wiersze, a listwa zajmuje ok. połowy wysokości ekranu na 5 s (przejście `dev`, emulator); przy 100% na 411 dp — 1–2 wiersze. *Obali:* rodzina przy telewizorze pyta „co to za
  rok, co się stało?”, a autor zerka po słowa i ich nie ma, bo listwa zniknęła — wtedy linia zostaje, dopóki stoi podpis (listwa bez reszty sterowania).
- **D73 — osoby z podpisu świecą; przy związku także linia pary** (v1.28; stop #2 [[ISSUE-050-next-event]], runda 1; **prośba autora** — *„obwódka wokół osoby i/lub podświetlona
  relacja”*, *„obwódka / laur "lśniały"”*; **decyzja *„B”***; zastępuje D70). Osoby ze zdarzeń bieżącej strony: pierścień w akcencie 2 dp (jak węzły ścieżki — 8) i poświata pod okręgiem,
  a przy wieńcu rodu pod wieńcem; przy ślubie i „razem” obie osoby i linia pary w akcencie (3 dp na ekranie, jak linia ścieżki — po prostej między okręgami, nad linią rodziny, pod osobami),
  która rośnie od pierwszej do drugiej w ok. 0,45 s. Trzy pulsy po 1,2 s (krycie 0,30 → 0,65 → 0,30), potem stała poświata 0,30, dopóki stoi podpis; przy oddaleniu poświata ma na ekranie
  stałą wielkość (co najmniej 12 dp poza okręgiem), jak imię (I2). Dlaczego: z kanapy imienia 13 sp nie widać (D38), a światło widać — rodzina wie, o kim autor mówi; laur świeci na tle
  poświaty, więc wieniec rodu (ISSUE-044) też „lśni”. Puls zamiast stałej: przyciąga oko w chwili ⏭, a stała poświata potem nie męczy; puls kończy się przed 5 s, bo ruch dłuższy niż 5 s
  bez sposobu na zatrzymanie łamie [SC 2.2.2](https://www.w3.org/TR/WCAG22/#pause-stop-hide), a podpis stoi bez końca (D69); 0,83 Hz — poniżej 3 zmian na sekundę
  ([SC 2.3.1](https://www.w3.org/TR/WCAG22/#three-flashes-or-below-threshold)). Linia pary — prostą między okręgami, jak krok „partner” ścieżki (element 8), bo para stoi obok siebie
  w jednym rzędzie. Narodziny i śmierć — sama osoba: linia do rodziców to już ścieżka, nie zdarzenie. **Nie da:** rozróżnienia rodzaju zdarzenia światłem — narodziny, ślub i śmierć
  świecą tak samo, rodzaj mówi linia podpisu i znicz. *Obali:* (a) poświata przy prawdziwej rodzinie zakrywa sąsiadów przy całym poziomie — wtedy przy skali < 1 mniejsza; (b) puls
  rozprasza autora w trakcie opowieści — wtedy jeden puls.
- **D74 — świecenie na telefonie i w trybie prezentacji tak samo** (v1.28, decyzja projektowa; „B” mówi o drzewie i mapie, nie o trybie). Dlaczego: ten sam ⏭ i ten sam podpis w obu
  miejscach (6a), a telefon bywa przesyłany na telewizor także poza trybem prezentacji; jedna reguła — mniej do zapamiętania. **Nie da:** spokojnego drzewa na telefonie po ⏭. *Obali:*
  autor na telefonie wyłącza świecenie wzrokiem (ma dymek) i mówi, że przeszkadza — wtedy świecenie tylko w trybie prezentacji.
- **D75 — przy ograniczeniu animacji bez pulsu** (v1.28, decyzja projektowa; [SC 2.3.3](https://www.w3.org/TR/WCAG22/#animation-from-interactions), jak D5, D36). Systemowe
  ograniczenie animacji → od razu stała poświata 0,30 i cała linia pary; wyróżnienie zostaje, ruch odpada. **Nie da:** przyciągnięcia oka pulsem przy wyłączonych animacjach.
  *Obali:* przy wyłączonych animacjach rodzina nie zauważa, kto świeci — wtedy mocniejsza stała poświata.
- **D76 — obrót: zwykły widok drzewa i mapy poziomo, z kartą, suwakiem i ikonami** (2026-10-23, [[ISSUE-055-connect-from-the-tree-and-rotate]] *Open* 4; **decyzja autora**
  w odpowiedzi na pytanie `ui` przed prototypem). Pytanie: po co przycisk pion/poziom, skoro tryb prezentacji stawia drzewo poziomo. Autor zaznaczył: *„w trybie prezentacji brak
  ścieżki — wychodziłem z niego, a drzewo wracało do pionu”* · *„przesyłanie włączyłem z szybkich ustawień telefonu, aplikacja została w pionie”* · *„chcę drzewo i mapę poziomo
  razem z kartą, suwakiem i ikonami — tryb prezentacji chowa za dużo”*; nie zaznaczył *„cała aplikacja poziomo”*. Więc: **drzewo i część „Mapa” w poziomie ze ścieżką, kartą,
  suwakiem i ikonami**; tryb prezentacji (11) i inne ekrany bez zmian. **Prior art:** Android 9+ przy zablokowanym obracaniu sam pokazuje przycisk obrotu na pasku nawigacji,
  gdy telefon się przekręci ([Rotate suggestions, AOSP](https://source.android.com/docs/core/display/rotate-suggestions)), a aplikacja poza trybem prezentacji nie blokuje
  orientacji — obrócić się da już dziś. Tyle że w poziomie na drzewo zostaje ok. 80 dp wysokości (pasek 64, karta z suwakiem ok. 120, zakładki 72 na 412 dp), więc
  **rzecz jest w układzie poziomym, a przycisk to dostęp do niego** bez obracania telefonu, który leży przy telewizorze. Na niskim ekranie Android domyślnie zostawia dolny
  pasek nawigacji ([Build adaptive navigation](https://developer.android.com/develop/adaptive-apps/guides/build-adaptive-navigation)). Układ — *Candidates — ISSUE-055*.
  **Nie da:** czystego telewizora — telewizor dostaje kopię ekranu z paskiem i kartą (D29); czysty obraz to tryb prezentacji. *Obali:* przy telewizorze autor i tak zostawia
  telefon w pionie albo wybiera tryb prezentacji — wtedy zamiast układu poziomego ścieżka w trybie prezentacji ([[2026-10-14-opowiesc-rodziny-i-wieniec]]).
- **D77 — układ poziomy L4 „bez zakładek”** (2026-10-23, [[ISSUE-055-connect-from-the-tree-and-rotate]]; **decyzja autora na prototypie — *„L4”***, runda 2 po
  uwadze do L1: *„więcej miejsca na drzewo a mniej na »interface«”*). Drzewo i część „Mapa” w poziomie — z przycisku „Obróć” albo z obracania telefonu: **bez dolnego paska
  zakładek**; **górny rząd 64 dp nad drzewem** — przełącznik „Drzewo · Mapa” z lewej, ikony „Obróć”, „Połącz dwie osoby”, „Przesyłaj na telewizor” z prawej, oba na
  powierzchni z obrysem; **karta osoby w środku z rzędem czasu — jeden pasek 64 dp na dole**; + / − poziomu w prawym dolnym rogu drzewa, nad paskiem. Na 915 × 412 dp
  drzewo ma 915 × 308 dp, w trakcie ścieżki 915 × 372 (pasek znika, baner z „×” staje w górnym rzędzie między przełącznikiem a ikonami). Do innych zakładek — „Obróć”
  albo wstecz. **Nie da:** zakładek w poziomie; ścieżka przez 4 pokolenia w skali ok. 0,55 (w L1 ok. 0,68) — za to więcej osób obok siebie. *Obali:* autor w poziomie szuka
  zakładek, żeby przejść do Osób — wtedy L3 (szyna 72 dp z lewej, *Candidates — ISSUE-055*).
  **v1.30 (przegląd `ui` zbudowanej [[ISSUE-055-connect-from-the-tree-and-rotate]], odstępstwa `dev` przyjęte):** (1) **lista „Od kogo?” / „Do kogo?” w poziomie zostaje
  pozioma** (element 7). Kandydaci `dev`: zostawić · lista w pionie jak widok osoby · wyniki nad polem. Przyjęte „zostawić”: lista otwiera się bez kursora w polu, więc A–Z
  widać od razu i wybór bez szukania działa; klawisz szukania na klawiaturze chowa ją sam (Flutter 3.41.1, `widgets/editable_text.dart`: `TextInputAction.search` →
  `_finalizeEditing(…, shouldUnfocus: true)`), a pole listy ma `TextInputAction.search`. Lista w pionie to dwa obroty obrazu na telewizorze przy jednym wyborze, a wyniki nad
  polem — osobny układ listy dla rzadkiego przypadku. **Nie da:** podglądu wyników w trakcie pisania w poziomie. *Obali:* autor w poziomie pisze imię i nie wie, gdzie są
  wyniki — wtedy wyniki nad polem. (2) **dolny pasek w części „Mapa” ok. 79 dp** zamiast 64 (element 12): linia „gdzie” to jedyne miejsce, które mówi słowami, gdzie osoba
  jest ([[mapa-migracji]] D18), więc nie znika ani nie ucina się; „rośnie, gdy tekst się zawija” nie przewidziało trzeciej linii. **Nie da:** 15 dp wysokości mapy.
- **D78 — „Od” = osoba w środku drzewa** (2026-10-23, [[ISSUE-055-connect-from-the-tree-and-rotate]]; prośba autora po pierwszym pokazie rodzinie, **potwierdzona na
  prototypie, panel 1 — *„tak”***; **zastępuje** w D49 „każde otwarcie zaczyna od „Ja””). Okno „Połącz dwie osoby” (7) otwiera się z osobą ze środka drzewa w kaflu „Od”
  („Ja”, gdy w środku jesteś Ty); kafel dalej prowadzi do listy „Od kogo?”. Po co: pokazać rodzinie, jak ktoś łączy się z tą osobą, nie tylko ze mną. **Decyzja projektowa
  z tego wynikająca:** ikona „Połącz dwie osoby” jest przy każdym drzewie, także z „Pokaż w drzewie”, gdy „ja” nie jest wybrane — powód jej braku (okno od „Ja”, baner
  od „ja”, v1.16 D3 planu ISSUE-039) znika; baner bez „ja” ma dwie linie (D47). *Obali:* autor na emulatorze zaczyna od „Ja” częściej niż od kogoś innego i za każdym razem
  zmienia kafel — wtedy „Od” zapamiętane z ostatniego razu albo „Ja” z szybką zamianą.
- **D79 — ścieżka zostaje do gestu wstecz, bez „×”** (2026-10-23, [[ISSUE-055-connect-from-the-tree-and-rotate]]; **decyzja autora na prototypie, panel 2 — *„w sumie nie
  chcę, aby był »x«, wystarczy mi gest wstecz”***; **zastępuje** w D49 „koniec podświetlenia: każde działanie, które zmienia drzewo” i w pozycji „do „×” albo gestu
  wstecz”). W trakcie ścieżki: dwa palce, przeciąganie i podwójne dotknięcie zmieniają tylko widok, a ścieżka zostaje; dotknięcie osoby nic nie robi. Kończy ją **wstecz**
  (gest, przycisk nawigacji trzema przyciskami, „wstecz” czytnika ekranu). **Decyzje projektowe:** kończą ją też działania, po których ścieżki nie ma gdzie pokazać —
  przełącznik „Drzewo · Mapa”, „Przesyłaj na telewizor” (tryb prezentacji bez ścieżki, D49), wybór nowego „Do” w oknie (nowa ścieżka zastępuje starą) i zmiana danych
  drzewa (v1.17); „Obróć” jej nie kończy. **Nie da:** widocznego wyjścia na ekranie — kto nie zna gestu wstecz, nie wie, jak wyjść. *Obali:* ktoś z rodziny trzyma
  telefon i nie umie wrócić do zwykłego drzewa — wtedy „Zakończ” na banerze.
- **D80 — w trakcie ścieżki samo drzewo i baner, który zostaje (B1)** (2026-10-23, [[ISSUE-055-connect-from-the-tree-and-rotate]]; „samo drzewo, bez suwaka czasu” —
  prośba autora po pokazie rodzinie; **baner — decyzja autora na prototypie, panel 2 — *„B1”***; **zastępuje** w elemencie 9 „4 s, dłużej według »Czas na działanie«”
  i w D45 powód „karta mówi, kim jest „Do”, także po zniknięciu baneru”). Od wyboru „Do” do wyjścia: **karta osoby w środku z rzędem czasu i + / − poziomu znikają**
  (decyzja projektowa: + / − zmieniałyby poziom pod ścieżką), drzewo dostaje ich miejsce; **baner z nazwą stoi przez całą ścieżkę**, bez „×” (D79) — pojawia się, gdy
  linia dojdzie do „Do” (D49), i znika z wyjściem. Pasek u góry zostaje (w poziomie górny rząd, D77). Po co: karta jest schowana, więc baner to jedyne miejsce, które
  mówi słowami, kim jest „Do” — rodzina przy telewizorze widzi to cały czas. Czytnik ogłasza baner raz (region na żywo, element 9). **Nie da:** górnych ~60 dp drzewa
  przez całą ścieżkę — kadr (8) zostawia miejsce pod banerem. *Obali:* przy długiej rozmowie baner przeszkadza rodzinie w oglądaniu góry drzewa — wtedy B2 (4 s).
- **D81 — po wyjściu ze ścieżki: rok sprzed ścieżki, „Od” w środku** (2026-10-23, [[ISSUE-055-connect-from-the-tree-and-rotate]]; **decyzja autora na prototypie, panel 3 —
  *„tak”***; **zastępuje D45** „„Do” staje w środku” i w D48 „ustawia suwak na „dziś”” — od wyjścia). Ścieżka dalej liczy się i rysuje na „dziś” (D48: pokrewieństwo nie
  zależy od roku), ale **wstecz przywraca rok, który był przed wyborem „Do”** (▶ stoi). **„Od” zostaje w środku** przez całą ścieżkę i po niej, więc następne „Połącz” zaczyna
  od tej samej osoby (D78); poziom liczony od „Od” (element 8 — „od osoby w środku”). **Skala i poziom po wyjściu zostają** (jak v1.23). Kafel „Od” zmieniony w oknie na
  kogoś innego przestawia środek na tę osobę przy starcie ścieżki — ścieżka zawsze zaczyna się w środku. Po co: powrót do opowieści dokładnie tam, gdzie była przerwana.
  *Obali:* autor po wyjściu chce od razu oglądać „Do” (karta) — wtedy dotknięcie „Do” po wyjściu, bez zmiany zasady.
- **D82 — przycisk „Obróć”: decyzje projektowe** (v1.29, [[ISSUE-055-connect-from-the-tree-and-rotate]], bez pytania; „tak” na stopie #1 przyjmuje je z planem):
  - **glif** `screen_rotation` z Material Symbols Rounded 300 — do dołożenia do fontu ikon (`tool/icons/build_symbols.py`, README `grobing-code` → *Ikony*); akcent, cel 48 dp,
    `tooltip` i czytnik „Obróć poziomo” / „Obróć pionowo” — nazwa mówi, co się stanie;
  - **miejsce:** w pasku na lewo od „Połącz dwie osoby” (w części „Mapa” — na lewo od „Przesyłaj na telewizor”); w poziomie pierwsza ikona górnego rzędu (12);
  - **działanie:** w pionie ustawia ekran poziomo (oba boki — telefon można obrócić), w poziomie pionowo; wybór trzyma także przy włączonym obracaniu w telefonie, dopóki
    jesteś w zakładce Drzewo (obie części; tryb prezentacji po wyjściu wraca do tego wyboru, a nie do ustawienia telefonu). Widok osoby, inne zakładki i wyjście z drzewa
    idą za ustawieniem telefonu (jak dziś — aplikacja poza drzewem nie ma układu poziomego), powrót do drzewa — znowu za wyborem. Po zamknięciu aplikacji wyboru nie ma
    (jak tempo — D41);
  - **inne ekrany bez zmian** — autor nie wybrał „cała aplikacja poziomo” (D76);
  - **ścieżki nie kończy** (D79): kadr ścieżki liczy się od nowa w nowym rozmiarze.

  **Nie da:** poziomu na widoku osoby, grobu i cmentarzy — przy telewizorze wyjście z drzewa obraca obraz do pionu. *Obali:* autor przy telewizorze chodzi z drzewa do osoby i z
  powrotem, a podwójny obrót przeszkadza — wtedy wybór na całą aplikację (inne ekrany potrzebują wtedy układu poziomego).
- **D83 — mostek łukiem w każdym przecięciu linii rodzic–dziecko** (2026-10-23, [[ISSUE-056-tree-lines-readable]]; **decyzja autora na prototypie, panel 2 — *„wybrałbym
  opcje mostków - łuk, bez osobnych kolorów dla rodzin”***). Gdzie pionowa kreska jednej rodziny (od rodziców do szyny albo od szyny do dziecka) przechodzi przez szynę innej
  rodziny, **kreska przeskakuje szynę łukiem**: półelipsa 4 dp w prawo, od 4 dp nad szyną do 4 dp pod nią, w kolorze i grubości kreski; szyna zostaje ciągła. **Kolejne
  przecięcia bliżej niż 8 dp** (szyny stoją co 7 dp) — **jeden łuk nad wszystkimi**, od 4 dp nad pierwszą do 4 dp pod ostatnią (decyzja projektowa: w prototypie dwa łuki
  zachodziły na siebie). Łuk jest w jednostkach drzewa — przy oddalaniu maleje z linią, jak jej grubość. **Linia w akcencie ścieżki** (8) biegnie tą samą drogą, łącznie z
  łukiem (decyzja projektowa — „tak” na stopie #1 ją przyjmuje). Prior art: *line jumps* w [draw.io](https://drawio-app.com/blog/draw-io-now-supports-line-jumps/) i
  [Visio](https://support.microsoft.com/en-US/Visio/add-or-remove-connector-line-jumps) — łuk mówi, że linie się nie łączą. Kandydaci odrzuceni: przerwa w szynie (panel 2),
  kolor rodziny (D85). **Nie da:** mostków na telewizorze przy całym poziomie (skala ok. 0,26 — łuk ok. 1 px); **mniej przecięć** — przecięcie zostaje, tylko widać, że to nie
  połączenie; **łuku w linii ścieżki przy skali poniżej ok. 1** (przegląd `ui` ISSUE-056, MINOR przyjęty) — linia w akcencie ma 3 dp na ekranie, łuk 4 dp w jednostkach drzewa,
  więc przy kadrze ścieżki 0,5–0,9 łuk zamyka się w „>”; drogę niosą pierścienie, animacja i baner. Gdyby przeszkadzało: łuk ścieżki `max(4, 5 / skala)` dp. *Obali:* autor po aktualizacji dalej gubi się przy przecięciach na telefonie → kolejność w rzędzie (D86) albo kolor rodziny (D85) wracają jako kandydaci.
- **D84 — piętra szyn według przecięć** (v1.31, [[ISSUE-056-tree-lines-readable]]; część kandydata „Piętra szyn + mostki” z panelu 2, który autor wybrał). Szyny, które
  zachodzą na siebie w jednej przerwie między rzędami, dalej stoją na osobnych piętrach co 7 dp (najwyżej 4, jak dziś), ale **piętro wybiera najmniejsza liczba
  przecięć**, a nie kolejność od lewej (algorytm lewej krawędzi — Hashimoto i Stevens 1971, trasowanie kanałów; daje najmniej pięter, przecięć nie liczy). Szyna wyżej
  znaczy: jej dzieci przecinają szyny niżej, a kreska rodziców szyny niżej przecina ją. **Nikt nie zmienia miejsca.** Pomiar na wymyślonej rodzinie (sonda na kodzie
  aplikacji): przecięcia narysowane 9 / 19 / 27 → 9 / 17 / 22 na poziomach 1–3. **Nie da:** mniej przecięć na „Linii krwi” (9 zostaje) — tam pomaga dopiero mostek.
- **D85 — bez koloru rodziny** (2026-10-23, [[ISSUE-056-tree-lines-readable]]; **decyzja autora na panelu 3** — *„bez osobnych kolorów dla rodzin”*). Linie rodzic–dziecko
  zostają w jednym kolorze; kolor dalej niesie rodzaj relacji ([[style-b]] *Token roles*), a nie rodzinę. *Obali* — jak D83.
- **D86 — kolejność w rzędzie bez zmian** (v1.31, [[ISSUE-056-tree-lines-readable]]; panel 4 bez wyboru — autor wybrał kandydata z panelu 2, „nikt się nie przesuwa”;
  **do potwierdzenia na stopie #1**). Kandydat D — kolejność według narysowanych przecięć i długości szyn, zasada rodowodów *„Sibs must be adjacent… Parents are above
  their child sibship”* (Tores, Barillot, RECOMB 2000) — dawał 9 → 4 na „Linii krwi” (13 i 18 na poziomach 2–3), ale przestawiał 12 / 35 / 15 osób, a sonda liczyła go
  9–34 s na PC: przed wyjazdem potrzebny byłby nowy, szybszy algorytm, a osoby znane autorowi z telefonu stanęłyby gdzie indziej. Miara narysowanych przecięć zostaje w
  testach `tree_layout` (AC-1) — gdy D wróci, jest od czego liczyć. *Obali* — jak D83.

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
11. ~~⚠️ OPEN — poziomy i przybliżanie: M, P, N, K, T~~ — **rozstrzygnięte 2026-10-19: M2, P2, N2, K1, T2** (stop #1 [[ISSUE-049-tree-levels-and-zoom]], *„tak”*; D50, D53–D56).
   Zapis sprzed decyzji: ([[ISSUE-049-tree-levels-and-zoom]], v1.23; kandydaci, prior art i pomiar — *Candidates — ISSUE-049*, makieta `drzewo-049.html`).
   **Rekomendacja: M2, P2, N2, K1, T2** (D50, D53–D56), do tego decyzje projektowe D51, D52, D57. Pytania z pozycji (*Notes* → `⚠️ OPEN` 1–4): (a) mąż, żona i partner krewnego na
   poziomie 1 czy 2 — **M1 / M2**; (b) wygląd przełącznika — **P1 / P2 / P3**; (c) nazwy — **N1 / N2** albo słowa autora; (d) skala po zmianie poziomu — **K1 / K2**; (e) przełącznik w trybie
   prezentacji — **T1 / T2**. Elementy 3, 3a, 4, 8, 11, *Navigation*, *States*, *Sketch* i *AC → element* są zapisane według rekomendacji; przy innym wyborze `ui` zmienia je przed planem.
   AC-3 ISSUE-049 brzmi dziś według M1 („mąż siostry Ewy i jego rodzice” na 3); przy M2 sam mąż jest już na 2, a na 3 dochodzą jego rodzice — `planning` poprawia przykład w AC-3. Na stop #1.
12. ~~⚠️ OPEN — „Następne”: K, N, F, Z, V, P, U (i M na mapie)~~ — **rozstrzygnięte 2026-10-19: K1, N1, F1, Z1, V2, P1, U3, mapa M2** (stop #1 [[ISSUE-050-next-event]], *„tak”*;
   D59–D65, [[mapa-migracji]] D27). Zapis sprzed decyzji: na stop #1 [[ISSUE-050-next-event]] (v1.26; kandydaci, prior art i pomiar — *Candidates — ISSUE-050*, makiety
   `drzewo-050.html` i `mapa-050.html`). **Rekomendacja: K1, N1, F1, Z1, V2, P1, U3** (D59–D65), mapa **M2** ([[mapa-migracji]] D27), do tego decyzje projektowe D66–D71. Pytania z pozycji
   (*Notes* → `⚠️ OPEN` 1–5): (1) czyje zdarzenia — **K1 / K2**; (2) daty niepewne — **N1 / N2**; (3) forma podpisu — **F1 / F2**; (4) nazwa miejsca w podpisie mapy — **M1 / M2**; (5) ▶ po
   „Następne” — **Z1 / Z2**. Nowe z makiety: (6) czy drzewo podjeżdża do osób z podpisu — **V1 / V2** (V2 zmienia zasadę K1 dla ⏭); (7) gdzie podpis na telewizorze — **P1 / P2**; (8) ⏭ w
   karcie telefonu — **U1 / U2 / U3** (U3 zmienia element 6: rok początku tylko przy ≥ 150%). Elementy 6, 6a, 11, *Navigation*, *States*, *Sketch* i *AC → element* są zapisane według
   rekomendacji; przy innym wyborze `ui` zmienia je przed planem. Przy F1 `planning` poprawia przykład w AC-1 (linie wielką literą). Na stop #1.
