---
screen: "Drzewo — rodzina od osoby, poziomy połączeń, czas; połącz dwie osoby"
items: ["[[SPIKE-004-mvp-flow-prototype]]", "[[ISSUE-024-person-view]]", "[[SPIKE-002-tree-on-a-phone]]", "[[US-009-drzewo-od-osoby]]", "[[ISSUE-033-tree-from-a-person]]", "[[ISSUE-034-tree-presentation-mode]]", "[[ISSUE-035-tree-names-shrink-my-voice]]", "[[ISSUE-036-cast-from-the-app]]", "[[ISSUE-037-time-on-the-tree]]"]
us: "[[US-009-drzewo-od-osoby]] (M9) · [[US-010-czas-na-drzewie]] (M10) · [[US-011-polacz-dwie-osoby]] (M11) — [[EPIC-003-zrozumienie]]"
journey-step: "widok 5 (M9–M11, R3)"
mockup: "2026-10-14: drzewo-037.html (ISSUE-037: suwak czasu, kandydaci N1–N3, C1–C2, T1–T2, E1–E3, R1–R2 na wymyślonej rodzinie z datami niepewnymi; zrzuty `shots-037\\`) — katalog tymczasowy sesji `555909c3-…\\scratchpad`; 2026-10-14: drzewo-036.html (ISSUE-036: kandydaci P1–P3 wejścia w przesyłanie, zrzuty z emulatora `shots-036\\`) — katalog tymczasowy sesji `fa865b36-…\\scratchpad`; 2026-10-13: drzewo-us009.html (US-009: imiona przy oddalaniu I1–I3, karta z nazwami pokrewieństwa, tekst 200%, tryb prezentacji, stany) — katalog tymczasowy sesji `c3868f5f-…\\scratchpad`; 2026-10-13: drzewo-spike002.html (SPIKE-002, kandydaci na 106 wymyślonych osobach) — `220a9b6c-…\\scratchpad`; wcześniej 2026-10-08: grobing-prototyp.html (SPIKE-004, panel 6, runda 2)"
updated: 2026-10-14
---

# Drzewo — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.29) · referencja: [[references]] → **R3**.
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
- **Ikona „Połącz dwie osoby”** w pasku → okno z dwoma kaflami → po wybraniu drugiej osoby **z powrotem na drzewie**, z
  animacją ścieżki (v1.1, D26). Dotknięcie drzewa albo wstecz kończy podświetlenie (US-011).
- **Rok na suwaku** (US-010, v1.12, D37): zostaje przy przestawieniu środka, zmianie poziomu i powrocie wstecz z widoku osoby; wejście z paska, „Pokaż w drzewie” i
  tryb prezentacji pokazują „dziś”.
- **Bez „ja”:** „Wybierz, która osoba to Ty” → wybór „ja” ([[osoby]] 6–7) → po wyborze z powrotem na drzewie, z tą osobą w środku (D19).

## Elements in order
**Tryb „Drzewo”** — US-009, poza elementem 6 (US-010)

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek „Drzewo” (20 sp, półgruby), po prawej ikony **bez podpisu** (v1.1): **„Przesyłaj na telewizor”** (`cast_outlined`, akcent, cel 48 dp, `tooltip` „Przesyłaj na telewizor”, czytnik: „Przesyłaj na telewizor — w ustawieniach telefonu” — **US-009**, v1.10, [[ISSUE-036-cast-from-the-app]]; **zastępuje** `tv_outlined` „Tryb prezentacji” z v1.5 — D30; drugie dotknięcie, zanim otworzy się ekran systemu, nic nie robi, a ikona się nie zmienia — v1.11, D30 b) i na lewo od niej **„Połącz dwie osoby”** (akcent, cel 48 dp, `tooltip` „Połącz dwie osoby” — **US-011**; ikona — *Open* 1a). W stanach bez drzewa (bez „ja”, pusta baza) ikon nie ma | pasek + przyciski-ikony | → systemowy ekran przesyłania → po powrocie tryb prezentacji (11) · → okno wyboru (7) | — | — | R3 · **decyzja autora** (D26, D11; stop #2 ISSUE-034 — „jak w YouTube”) · AC-8 · D29 |
| 2 | ~~Legenda linii~~ — **bez legendy** (v1.1, D25). Rodzaj linii niesie kształt i styl (łamana z góry — rodzic–dziecko; pozioma ciągła — małżeństwo; przerywana — razem), więc kolor nie jest jedynym nośnikiem (SC 1.4.1) | — | — | — | — | **decyzja autora** (D25) |
| 3 | **Poziom połączeń — oddalanie odsłania dalszą rodzinę** (v1.3, S2): bez przycisków „−/Poziom 2/+” w pasku. Poziom zmienia oddalanie i przybliżanie, **próg za progiem**: oddalasz — dokłada się poziom, przybliżasz — dalsza rodzina znika. **4 progi** (poziomy 1–4; od 4 to prawie wszyscy). Przy zmianie na chwilę pigułka „Poziom 3 · 66 osób” (13 sp, powierzchnia). **Przyciski + / −** (cel 48 dp, powierzchnia z obrysem) w prawym dolnym rogu drzewa — alternatywa jednym dotknięciem (SC 2.5.1): + przybliża, − oddala. **Poziom 1:** rodzice, partnerzy, dzieci. **Poziom k ≥ 2:** do tego rodzice, partnerzy, dzieci i **rodzeństwo** każdej osoby z poziomu k−1 (np. rodzeństwo, rodzeństwo partnerów, dziadkowie, teściowie, wnuki). **Wartości** (v1.5, D18 — z prototypu SPIKE-002, do potwierdzenia w ręce): skala 0,4–2,0, start 1,0; **poziom 1** przy skali ≥ 1,3 · **2** — 0,85–1,3 · **3** — 0,55–0,85 · **4** — poniżej 0,55. + / − mnożą skalę przez 1,45 (mniej więcej poziom na dotknięcie); **podwójne dotknięcie pustego miejsca** przybliża tak samo (AC-3). Pigułka ok. 1,5 s; ten sam tekst ogłasza czytnik. Zmiana poziomu zostawia osobę w środku w tym samym miejscu ekranu | gest + przycisk-ikona ×2 + pigułka | dwa palce (oddal / przybliż) · + / − · podwójne dotknięcie | 2 | — | **decyzja autora** (stop #1 SPIKE-002) · D2 · D8 · AC-3 · D18 |
| 4 | **Drzewo**: rzędy według pokolenia (wyżej starsze), osoba w środku z pierścieniem w akcencie; rodzeństwo z boku osoby, po stronie dalszej od partnera; **rodzina partnera po prawej**, bez przeplatania z krewnymi. Węzeł 44 dp (profilowe albo inicjały), imię 13 sp półgrube (v1.2, D10); **zmarły ma znicz** w rogu węzła ([[style-b]] reguła 8, R3); zmarły = zapisany zgon albo pochówek, z datą albo bez (v1.7, D22). Linie: **rodzic–dziecko** — kolor relacji rodzic–dziecko, łamana z góry w dół; **małżeństwo** — kolor partnerów, ciągła, pozioma; **razem (bez ślubu)** — kolor partnerów, przerywana 5/4. **Koniec związku** (v1.12, E3 — D35): od roku końca dwie ukośne kreski „//” przez środek linii pary (kolor partnerów, 2 dp, ok. 12 × 12 dp), także na „dziś”; koniec bez daty — tylko na „dziś”; linia do dzieci zostaje. **Ślad dalszej rodziny** (v1.3, D9): osoba z rodziną poza widokiem dostaje krótką przerywaną kreskę 3/3, 14 dp, w kolorze relacji o kryciu 60% — w górę rodzice, w dół dzieci, w bok partner, **na zewnątrz od środka** (na lewo od osoby w środku — w lewo, na prawo i u niej samej — w prawo; v1.7, przegląd `ui` ISSUE-033: zawsze w prawo celował u osób po lewej w środek i mylił się z linią „razem”). Przewijanie w obu osiach, środek ustawia się na osobie. **Drzewo nie ucieka z kadru** (v1.7, D21): gdy w kadrze nie ma nikogo, widok wraca płynnie (ok. 0,35 s) do osoby w środku, a palec na ekranie przerywa powrót; nowy rozmiar obszaru drzewa przed pierwszym dotknięciem ustawia środek od nowa. **„Ja”** (v1.5, D14): okrąg ze znakiem „Ja” (inicjały „Ja” w akcencie, obrys w kolorze obrysu, także przy profilowym — jak [[osoby]] D4), podpis „Ja”; pierścień i poświatę w akcencie ma tylko osoba w środku. **Przestawienie środka** (AC-2, v1.5): węzły przesuwają się na nowe miejsca w ok. 0,45 s, nowe osoby się pojawiają, odchodzące gasną, a widok jedzie tak, że nowa osoba staje w środku (ok. 42% wysokości obszaru drzewa). Przy systemowym ograniczeniu animacji — od razu (SC 2.3.3, jak D5). **Imiona przy oddalaniu** (v1.6, I2 — decyzja autora; potwierdzona w v1.9, D27): przy skali < 1 imię nie maleje — na ekranie ma 13 sp × skala tekstu, na tabliczce w kolorze tła (zaokrąglona 4 dp, 3 dp z boków; v1.7, D23); gdy dwa imiona by się nałożyły, zostaje to bliżej osoby w środku (najpierw poziom z D2, potem odległość w poziomie), a reszta chowa się do przybliżenia. **Tekst systemu** (AC-7, v1.5): miejsce osoby 80 dp × skala tekstu, najwyżej 160 dp (jak mini-drzewo, [[osoba]] v2.2); rząd rośnie z podpisem (104 dp → 124 dp przy 200%); inicjały najwyżej 1,3×; imię w jednej linii, „…” dopiero poza miejscem osoby (przy 100% to ok. 10 liter, także przy oddaleniu — v1.7, D24). **Cel dotyku** = miejsce osoby × skala drzewa (D17). **Czytnik:** „Zofia Wymyślona, 1928–2010, Moja babcia — w środek” (v1.9, G2 — ten sam tekst co karta, D28), osoba w środku „… — otwórz”; kolejność rzędami, z góry i od lewej; linie i ślad poza czytnikiem | drzewo | dotknięcie → osoba w środek; drugie → [[osoba]] | „Ja” | — | R3 · D1, D3, D4, D9 · AC-1, AC-2, AC-4, AC-7 · D14, D17 |
| 5 | **Karta osoby w środku** (dolny arkusz, powierzchnia; v1.5): okrąg 40 dp z pierścieniem w akcencie (profilowe w kadrze albo inicjały; „ja” — znak „Ja”) · **imię i nazwisko** z „z d.” (16 sp, półgruby, tekst, do dwóch linii) · pod spodem **lata · kim jest dla mnie** (14 sp, tekst pomocniczy, **zawija się, bez ucinania**): nazwa ze słownika, z nawiasem tam, gdzie słownik go ma („1928–2010 · Moja babcia”, „ur. 1951 · Mój stryj (brat taty)”, „Moje rodzeństwo” przy osobie bez płci), a dalej opis z odcinków („1925–2010 · Siostra cioteczna mojego dziadka”, „Siostra cioteczna babci mojej żony”; D12, D13; **mówisz Ty — G2, v1.9, D28**). „Ja”: „ur. 1983 · to ja”. Bez ścieżki do „ja”: „… · nie wiadomo jeszcze, kim jest dla mnie”. Zaimek zawsze z małej litery w środku opisu („…babci mojej żony”), z wielkiej tylko na początku nazwy („Moja babcia”). Bez „ja” (wejście z „Pokaż w drzewie”): same lata. Po prawej przycisk tekstowy „Pokaż ›” (akcent, cel 48 dp); **przy tekście systemu ≥ 150% „Pokaż ›” przechodzi pod tekst, do prawej** (D20) | karta | „Pokaż” → [[osoba]] | — | — | D1 · AC-2, AC-5 · D12, D13, D20 |
| 6 | **US-010. Czas (M10; v1.12 — [[ISSUE-037-time-on-the-tree]]):** w karcie (5), pod imieniem i opisem, jeden rząd: **▶ / ❚❚** (okrąg 36 dp w akcencie, ikona `play_arrow` / `pause` w kolorze tła, cel 48 dp, `tooltip` „Odtwórz historię” / „Zatrzymaj”) · **rok początku** (13 sp, tekst pomocniczy) · **suwak** (`Slider`: aktywny tor i uchwyt w akcencie, tor nieaktywny w kolorze obrysu, wysokość 48 dp, krok 1 rok) · **rok** (16 sp, półgruby, akcent, cyfry o stałej szerokości; na końcu suwaka „dziś”) — w stałym miejscu na szerokość najszerszego z „dziś” i „8888”, żeby tor suwaka nie zmieniał długości pod palcem (v1.13, odstępstwo 2 ISSUE-037). **Domyślnie „dziś”** — drzewo jak w US-009: nic nie znika i nic nie jest przerywane. **Początek suwaka** (T2, D34): pełna dekada przed najwcześniejszą datą urodzenia w bazie, najpóźniej 1880. **Rok Y** (AC-1, AC-2): osoba, która w roku Y jeszcze się nie urodziła, znika razem ze swoimi liniami i imieniem, a jej miejsce zostaje (układ liczony jak na „dziś”, rok go nie zmienia); nie jest celem dotyku i nie ma jej w czytniku. Zmarły do Y ma znicz. Para: do początku związku bez linii, od początku przerywana „razem”, od ślubu ciągła; **związek bez daty** — od urodzenia najstarszego wspólnego dziecka, a bez dzieci — od 20. roku życia młodszego z pary (D31); koniec związku — „//” (element 4, E3). **Data niepewna i brak daty** (N3, D32): każda data ma okno [najwcześniej, na pewno]. Osoba pojawia się na początku okna urodzenia i do jego końca ma **przerywany obrys okręgu** (2 dp, kreska 4/3, kolor obrysu; u osoby w środku pierścień w akcencie przerywany). W oknie śmierci — ten sam obrys, a znicz dopiero na końcu okna. Okno: dokładnie Y — Y; „ok. Y” — Y−5 … Y+5; „między A a B” — A … B; „przed Y” — najwcześniej z rodziny … Y; „po Y” — Y … na pewno z rodziny; brak daty — oba końce z rodziny (D32). **Osoba w środku przed narodzinami** (C1, D33): pusty pierścień w akcencie w jej miejscu, bez okręgu, imienia i znicza; karta bez zmian. **▶** (AC-3): od początku suwaka (albo od bieżącego roku, gdy to nie „dziś”) do „dziś”, stale ok. 21 lat na sekundę (1880 → dziś w ok. 7 s); osoby pojawiają się i gasną przenikaniem 150 ms — w trakcie ▶ najwyżej do następnego roku (ok. 50 ms), pełne 150 ms przy przesuwaniu suwaka palcem (v1.13, odstępstwo 4 ISSUE-037; *Obali:* autor widzi miganie osób przy ▶ — wtedy przenikanie od roku narodzin, bez przerywania); na „dziś” ▶ się zatrzymuje, a czytnik raz ogłasza rok („Rok 1923”, „dziś”) — także po ❚❚. ❚❚ zatrzymuje na bieżącym roku; przeciągnięcie suwaka też zatrzymuje. **Ograniczenie animacji** (R2, D36): ▶ przeskakuje o pełną dekadę co ok. 1 s, osoby pojawiają się od razu, bez przenikania. **Tekst ≥ 150%** (D20): rok początku i rok w rzędzie nad suwakiem (po lewej i po prawej), ▶ i suwak w rzędzie pod nimi. **Czytnik:** ▶ „Odtwórz historię” / „Zatrzymaj”; suwak „Rok” z wartością „1923” albo „dziś”, zwiększanie i zmniejszanie o 10 lat (krok co rok to do 166 gestów); w trakcie ▶ rok nie jest ogłaszany co zmianę, po zatrzymaniu — tak. Osoba z przerywanym obrysem: do opisu z elementu 4 dochodzi „nie wiadomo, czy już żyje” (okno urodzenia) albo „nie wiadomo, czy jeszcze żyje” (okno śmierci); pusty pierścień: „… — przed narodzinami” | suwak + przycisk | przeciągnięcie · ▶ / ❚❚ | dziś | — | R3 (suwak) · **decyzja autora** (D20) · D4 · AC-1–AC-3 · D31–D37 |
| 11 | **Tryb prezentacji** (AC-8, D11; v1.5, D16): ekran poziomo, na pełnym ekranie (bez pasków systemu i aplikacji, bez karty i + / −), **poziom 2 dopasowany do ekranu** (w obszarze bezpiecznym, margines 24 dp) i wyśrodkowany. **Wejście (v1.10, P2):** po powrocie z systemowego ekranu przesyłania — **bez podpowiedzi** (przesyłanie właśnie wybrane, a podpowiedź trafiłaby na telewizor). **Tylko gdy telefon nie ma tego ekranu** (ISSUE-036 AC-2) tryb włącza się od razu i na ok. 4 s pokazuje pigułkę u góry, w miejscu pigułki poziomu: „Obraz na telewizor: przesyłanie ekranu w szybkich ustawieniach telefonu” (v1.8, D26 — funkcja, nie nazwa kafelka; twarda spacja po „w”, [[style-b]] reguła 6). Przez te 4 s może przykryć górny rząd, a dotyk przechodzi do osób pod nią (D26). **Dotknięcie osoby** → ona w środku, poziom 2 dopasowany na nowo — **także osoby, która już jest w środku**: po przeciągnięciu to droga z powrotem; jej widok się nie otwiera, a czytnik nie mówi „otwórz” (v1.8, D25). Przeciąganie przesuwa; **bez szczypania** — poziom stały. **Pasy 24 dp przy krawędziach, od których system wysuwa paski, nie przyjmują dotyku** (v1.8, D25). **Dotknięcie pustego miejsca** → na 3 s przycisk „Zakończ prezentację” w prawym górnym rogu (`close` w akcencie + napis w kolorze tekstu, powierzchnia z obrysem, cel 48 dp); podpowiedź, jeśli jeszcze jest, znika (v1.8, D25); **wstecz** też kończy. Po wyjściu — drzewo pionowo, ta sama osoba w środku, poziom 2, skala 1. **Tekst 200%** (v1.8, odstępstwo 5 ISSUE-034; v1.9 — I2 zostaje, D27): imiona jak w elemencie 4, więc na ekranie 360 dp imię ma 26 sp przy okręgu ok. 20 dp (skala ok. 0,45), widać 13 z 20 imion, a tabliczki zasłaniają linie między rzędami (zrzut `18b`). Przy I1 byłoby 20 z 20 imion, ok. 11,7 sp (przeliczenie `ui`, v1.9) | tryb | dotknięcie osoby · pustego miejsca · wstecz | poziom 2 | — | **decyzja autora** (D11) · AC-8 · D16 · D25, D26 |

**„Połącz dwie osoby” na drzewie (M11, v1.1)** — US-011

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 7 | **Okno „Połącz dwie osoby”** (v1.1): dwa kafle na powierzchni — „Od” i „Do” (podpis 13 sp, profilowe 40 dp albo „Wybierz osobę”). Kafel → lista osób jak [[osoby]] (wyszukiwarka i A–Z). „Od” domyślnie „Ja” | okno z kaflami | kafel → lista; **wybór drugiej osoby zamyka okno** i uruchamia 8 | Od: „Ja” | — | **decyzja autora** (D26) · R3 |
| 8 | **Ścieżka na drzewie** (v1.1): drzewo przechodzi na **najniższy poziom, na którym widać drugą osobę**, i ustawia się tak, żeby ścieżka była w kadrze; **osoby spoza ścieżki wyszarzone** (krycie ok. 30%), osoby ze ścieżki podświetlone; **linia w akcencie biegnie powoli ode mnie do kolejnych osób** (ok. 0,7 s na krok), każda osiągnięta osoba dostaje pierścień w akcencie | animacja na drzewie | dotknięcie drzewa / wstecz → koniec podświetlenia | — | — | **decyzja autora** (D21, D26) · D5 |
| 9 | **Baner na chwilę** (ok. 4 s) u góry drzewa, na powierzchni: **kim ta osoba jest dla mnie** — opis złożony z odcinków, np. „Siostra cioteczna babci mojej żony” (16 sp, półgruby); bez zdania ścieżki i **bez „Odtwórz jeszcze raz”** | baner | znika sam | — | — | **decyzja autora** (D26) · D6 |
| 10 | **Bez ścieżki:** baner „Te osoby nie łączą się — w drzewie brakuje rodziny między nimi.”, drzewo bez zmian | baner | — | — | — | reguła 9 |

## States
| Stan | Co widać |
|---|---|
| drzewo | 1, 3–5 (6 od US-010); na starcie „Ja” w środku, poziom 2 |
| oddalenie (poziom 3–4) | 1, 3–5; imiona według I2 — czytelne, nakładające się chowają (element 4, D27); na chwilę pigułka „Poziom 3 · 66 osób” |
| rok w przeszłości (US-010) | 4 bez osób nieurodzonych (miejsca zostają), linie par według dat związku, znicze zmarłych do tego roku, przerywany obrys przy osobach w oknie daty (N3); ślad dalszej rodziny i pigułka poziomu liczą tylko osoby, które w tym roku już są (D37); 5 bez zmian; 6 z rokiem (v1.12) |
| osoba w środku przed narodzinami (US-010) | 4: w jej miejscu pusty pierścień w akcencie (C1, D33); 5 bez zmian; czytnik „… — przed narodzinami” |
| odtwarzanie (US-010) | 6: ❚❚ zamiast ▶, rok biegnie ok. 21 lat na sekundę; dotknięcie osoby i oddalanie działają dalej (D37) |
| ograniczenie animacji (US-010) | jak odtwarzanie, ale rok skacze o dekadę co ok. 1 s, osoby pojawiają się od razu (R2, D36) |
| połącz — wybór (US-011) | 1, okno 7 nad drzewem |
| połącz — ścieżka (US-011) | 1, 3–6, 8 (reszta wyszarzona), 9 przez ok. 4 s |
| bez ścieżki (US-011) | 1, 3–6, 10 |
| osoba bez rodziny | 4: tylko ona, bez śladu; 5 („… · nie wiadomo jeszcze, kim jest dla mnie”, chyba że to „ja”) |
| osoba spoza rodziny „ja” | 4: jej rodzina; 5 z „nie wiadomo jeszcze, kim jest dla mnie” |
| „ja” niewybrane | 1 bez ikon; w miejscu drzewa, na środku: „Aplikacja nie wie jeszcze, która osoba to Ty.” (16 sp, tekst pomocniczy) i przycisk tekstowy w akcencie „Wybierz, która osoba to Ty” (jak [[osoba]] element 7); bez karty i + / −. Wejście z „Pokaż w drzewie” działa — wtedy 5 bez pokrewieństwa (D19) |
| pusta baza | 1 bez ikon; na środku „Tu pojawi się drzewo — osoby z grobów i ich rodziny.” (16 sp, tekst pomocniczy; jak „pusta baza” w [[osoby]]), bez działania (D19) |
| tekst 200% | 4 z szerszym miejscem osoby; 5 z „Pokaż ›” pod tekstem; + / − bez zmian, 48 dp (D20) |
| przesyłanie — ekran systemu (v1.10) | nie ekran aplikacji: ustawienia telefonu („Google Cast” na emulatorze z Androidem 16; jasny, w języku telefonu), lista telewizorów w tej samej sieci Wi-Fi albo „No nearby devices were found.” (zrzut `01`). Wstecz wraca do aplikacji |
| tryb prezentacji | 11 — po ekranie systemu bez podpowiedzi |
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
│ │ (▶) 1860 ━━━━━━━━━━●━━━  1984 │ │  ← suwak czasu — US-010 (v1.12): ▶ 36 dp, rok w akcencie, „dziś” na końcu
│ ╰──────────────────────────────╯ │
│  Mapa      Osoby      Drzewo     │
└──────────────────────────────────┘
```

## Tempo
n/a — ekran do oglądania.

## Style B rules applied
- **Nowa rola — kolory relacji** ([[style-b]] v1.16): rodzic–dziecko i partnerzy, każda ≥ 3:1 na tle (SC 1.4.11). Między
  sobą różnią się tylko odcieniem (1,04:1), więc **rodzaj linii niesie też kształt i styl**: rodzic–dziecko łamana z góry
  w dół, para pozioma, „razem” przerywana (SC 1.4.1); bez legendy (v1.1, D25 — poprawione w v1.4).
- **Reguła 1 (akcent):** ścieżka „Połącz dwie osoby”, osoba w środku, aktywny segment i suwak — wybór i fokus, nie relacje.
- **Reguła 8:** znicz na węźle osoby zmarłej (R3).
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
| M11 — ścieżka między dowolnymi dwiema osobami (US-011) | 7–9 | „Ja” → „Wanda Przykładowa” (v1.2: przykład z wymyślonych rdzeni, retro 3 R7): drzewo na poziomie 3, linia biegnie przez Kasię i Piotra, reszta wyszarzona, baner „Babcia mojej żony” |

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
  zatrzymuje ▶ na bieżącym roku.

## Open
1. ~~⚠️ OPEN — sterowanie poziomami — nowy wygląd~~ — rozstrzygnięte 2026-10-13: S2 (element 3), 4 progi (autor na stopie #1
   SPIKE-002: *„Tak”*).
1a. **Ikona „Połącz dwie osoby”** (element 1): `conversion_path` **nie istnieje** w `Icons` Fluttera 3.41.1 (sprawdzone w SDK
   2026-10-09, przy [[osoba]] D18). Do wyboru przy pozycji drzewa: `link` (jak „Jak łączy się ze mną” w [[osoba]] — ta sama
   idea) albo własna ikona wektorowa.
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
