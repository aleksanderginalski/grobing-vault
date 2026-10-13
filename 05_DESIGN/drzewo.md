---
screen: "Drzewo — rodzina od osoby, poziomy połączeń, czas; połącz dwie osoby"
items: ["[[SPIKE-004-mvp-flow-prototype]]", "[[ISSUE-024-person-view]]", "[[SPIKE-002-tree-on-a-phone]]", "[[US-009-drzewo-od-osoby]]", "[[ISSUE-033-tree-from-a-person]]"]
us: "[[US-009-drzewo-od-osoby]] (M9) · [[US-010-czas-na-drzewie]] (M10) · [[US-011-polacz-dwie-osoby]] (M11) — [[EPIC-003-zrozumienie]]"
journey-step: "widok 5 (M9–M11, R3)"
mockup: "2026-10-13: drzewo-us009.html (US-009: imiona przy oddalaniu I1–I3, karta z nazwami pokrewieństwa, tekst 200%, tryb prezentacji, stany) — katalog tymczasowy sesji `c3868f5f-…\\scratchpad`; 2026-10-13: drzewo-spike002.html (SPIKE-002, kandydaci na 106 wymyślonych osobach) — `220a9b6c-…\\scratchpad`; wcześniej 2026-10-08: grobing-prototyp.html (SPIKE-004, panel 6, runda 2)"
updated: 2026-10-13
---

# Drzewo — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.27) · referencja: [[references]] → **R3**.
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
- **Ikona „Tryb prezentacji”** w pasku → tryb prezentacji (element 11); wstecz albo „Zakończ prezentację” wraca do drzewa (US-009).
- **Ikona „Połącz dwie osoby”** w pasku → okno z dwoma kaflami → po wybraniu drugiej osoby **z powrotem na drzewie**, z
  animacją ścieżki (v1.1, D26). Dotknięcie drzewa albo wstecz kończy podświetlenie (US-011).
- **Bez „ja”:** „Wybierz, która osoba to Ty” → wybór „ja” ([[osoby]] 6–7) → po wyborze z powrotem na drzewie, z tą osobą w środku (D19).

## Elements in order
**Tryb „Drzewo”** — US-009, poza elementem 6 (US-010)

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek „Drzewo” (20 sp, półgruby), po prawej ikony **bez podpisu** (v1.1): **„Tryb prezentacji”** (`tv_outlined`, akcent, cel 48 dp, `tooltip` „Tryb prezentacji” — **US-009**, v1.5) i na lewo od niej **„Połącz dwie osoby”** (akcent, cel 48 dp, `tooltip` „Połącz dwie osoby” — **US-011**; ikona — *Open* 1a). W stanach bez drzewa (bez „ja”, pusta baza) ikon nie ma | pasek + przyciski-ikony | → tryb prezentacji (11) · → okno wyboru (7) | — | — | R3 · **decyzja autora** (D26, D11) · AC-8 |
| 2 | ~~Legenda linii~~ — **bez legendy** (v1.1, D25). Rodzaj linii niesie kształt i styl (łamana z góry — rodzic–dziecko; pozioma ciągła — małżeństwo; przerywana — razem), więc kolor nie jest jedynym nośnikiem (SC 1.4.1) | — | — | — | — | **decyzja autora** (D25) |
| 3 | **Poziom połączeń — oddalanie odsłania dalszą rodzinę** (v1.3, S2): bez przycisków „−/Poziom 2/+” w pasku. Poziom zmienia oddalanie i przybliżanie, **próg za progiem**: oddalasz — dokłada się poziom, przybliżasz — dalsza rodzina znika. **4 progi** (poziomy 1–4; od 4 to prawie wszyscy). Przy zmianie na chwilę pigułka „Poziom 3 · 66 osób” (13 sp, powierzchnia). **Przyciski + / −** (cel 48 dp, powierzchnia z obrysem) w prawym dolnym rogu drzewa — alternatywa jednym dotknięciem (SC 2.5.1): + przybliża, − oddala. **Poziom 1:** rodzice, partnerzy, dzieci. **Poziom k ≥ 2:** do tego rodzice, partnerzy, dzieci i **rodzeństwo** każdej osoby z poziomu k−1 (np. rodzeństwo, rodzeństwo partnerów, dziadkowie, teściowie, wnuki). **Wartości** (v1.5, D18 — z prototypu SPIKE-002, do potwierdzenia w ręce): skala 0,4–2,0, start 1,0; **poziom 1** przy skali ≥ 1,3 · **2** — 0,85–1,3 · **3** — 0,55–0,85 · **4** — poniżej 0,55. + / − mnożą skalę przez 1,45 (mniej więcej poziom na dotknięcie); **podwójne dotknięcie pustego miejsca** przybliża tak samo (AC-3). Pigułka ok. 1,5 s; ten sam tekst ogłasza czytnik. Zmiana poziomu zostawia osobę w środku w tym samym miejscu ekranu | gest + przycisk-ikona ×2 + pigułka | dwa palce (oddal / przybliż) · + / − · podwójne dotknięcie | 2 | — | **decyzja autora** (stop #1 SPIKE-002) · D2 · D8 · AC-3 · D18 |
| 4 | **Drzewo**: rzędy według pokolenia (wyżej starsze), osoba w środku z pierścieniem w akcencie; rodzeństwo z boku osoby, po stronie dalszej od partnera; **rodzina partnera po prawej**, bez przeplatania z krewnymi. Węzeł 44 dp (profilowe albo inicjały), imię 13 sp półgrube (v1.2, D10); **zmarły ma znicz** w rogu węzła ([[style-b]] reguła 8, R3); zmarły = zapisany zgon albo pochówek, z datą albo bez (v1.7, D22). Linie: **rodzic–dziecko** — kolor relacji rodzic–dziecko, łamana z góry w dół; **małżeństwo** — kolor partnerów, ciągła, pozioma; **razem (bez ślubu)** — kolor partnerów, przerywana 5/4. **Ślad dalszej rodziny** (v1.3, D9): osoba z rodziną poza widokiem dostaje krótką przerywaną kreskę 3/3, 14 dp, w kolorze relacji o kryciu 60% — w górę rodzice, w dół dzieci, w bok partner, **na zewnątrz od środka** (na lewo od osoby w środku — w lewo, na prawo i u niej samej — w prawo; v1.7, przegląd `ui` ISSUE-033: zawsze w prawo celował u osób po lewej w środek i mylił się z linią „razem”). Przewijanie w obu osiach, środek ustawia się na osobie. **Drzewo nie ucieka z kadru** (v1.7, D21): gdy w kadrze nie ma nikogo, widok wraca płynnie (ok. 0,35 s) do osoby w środku, a palec na ekranie przerywa powrót; nowy rozmiar obszaru drzewa przed pierwszym dotknięciem ustawia środek od nowa. **„Ja”** (v1.5, D14): okrąg ze znakiem „Ja” (inicjały „Ja” w akcencie, obrys w kolorze obrysu, także przy profilowym — jak [[osoby]] D4), podpis „Ja”; pierścień i poświatę w akcencie ma tylko osoba w środku. **Przestawienie środka** (AC-2, v1.5): węzły przesuwają się na nowe miejsca w ok. 0,45 s, nowe osoby się pojawiają, odchodzące gasną, a widok jedzie tak, że nowa osoba staje w środku (ok. 42% wysokości obszaru drzewa). Przy systemowym ograniczeniu animacji — od razu (SC 2.3.3, jak D5). **Imiona przy oddalaniu** (v1.6, I2 — decyzja autora): przy skali < 1 imię nie maleje — na ekranie ma 13 sp × skala tekstu, na tabliczce w kolorze tła (zaokrąglona 4 dp, 3 dp z boków; v1.7, D23); gdy dwa imiona by się nałożyły, zostaje to bliżej osoby w środku (najpierw poziom z D2, potem odległość w poziomie), a reszta chowa się do przybliżenia. **Tekst systemu** (AC-7, v1.5): miejsce osoby 80 dp × skala tekstu, najwyżej 160 dp (jak mini-drzewo, [[osoba]] v2.2); rząd rośnie z podpisem (104 dp → 124 dp przy 200%); inicjały najwyżej 1,3×; imię w jednej linii, „…” dopiero poza miejscem osoby (przy 100% to ok. 10 liter, także przy oddaleniu — v1.7, D24). **Cel dotyku** = miejsce osoby × skala drzewa (D17). **Czytnik:** „Zofia Wymyślona, 1928–2010, Twoja babcia — w środek”, osoba w środku „… — otwórz”; kolejność rzędami, z góry i od lewej; linie i ślad poza czytnikiem | drzewo | dotknięcie → osoba w środek; drugie → [[osoba]] | „Ja” | — | R3 · D1, D3, D4, D9 · AC-1, AC-2, AC-4, AC-7 · D14, D17 |
| 5 | **Karta osoby w środku** (dolny arkusz, powierzchnia; v1.5): okrąg 40 dp z pierścieniem w akcencie (profilowe w kadrze albo inicjały; „ja” — znak „Ja”) · **imię i nazwisko** z „z d.” (16 sp, półgruby, tekst, do dwóch linii) · pod spodem **lata · kim jest dla Ciebie** (14 sp, tekst pomocniczy, **zawija się, bez ucinania**): nazwa ze słownika, z nawiasem tam, gdzie słownik go ma („1928–2010 · Twoja babcia”, „ur. 1951 · Twój stryj (brat taty)”), a dalej opis z odcinków („1925–2010 · Siostra cioteczna Twojego dziadka”; D12, D13; aplikacja mówi do Ciebie — G1, v1.6). „Ja”: „ur. 1983 · to Ty”. Bez ścieżki do „ja”: „… · nie wiadomo jeszcze, kim jest dla Ciebie”. Bez „ja” (wejście z „Pokaż w drzewie”): same lata. Po prawej przycisk tekstowy „Pokaż ›” (akcent, cel 48 dp); **przy tekście systemu ≥ 150% „Pokaż ›” przechodzi pod tekst, do prawej** (D20) | karta | „Pokaż” → [[osoba]] | — | — | D1 · AC-2, AC-5 · D12, D13, D20 |
| 6 | **US-010. Czas (M10):** przycisk ▶ / ❚❚ (36 dp, akcent), „1880”, suwak (akcent), rok w akcencie („dziś” na końcu). **Rok Y:** osoba urodzona po Y znika (miejsce zostaje, żeby drzewo nie skakało); para łączy się linią „razem” od daty początku związku, a ciągłą od ślubu; zmarły do Y ma znicz. ▶ przechodzi od 1880 do dziś w ok. 7 s | suwak + przycisk | przeciągnięcie; ▶ | dziś | — | R3 (suwak) · **decyzja autora** (D20) · D4 |
| 11 | **Tryb prezentacji** (AC-8, D11; v1.5, D16): ekran poziomo, na pełnym ekranie (bez pasków systemu i aplikacji, bez karty i + / −), **poziom 2 dopasowany do ekranu** i wyśrodkowany. Przy wejściu na ok. 4 s pigułka „Obraz na telewizor: „Przesyłaj ekran” w szybkich ustawieniach Androida”. **Dotknięcie osoby** → ona w środku, poziom 2 dopasowany na nowo. Przeciąganie przesuwa; **bez szczypania** — poziom stały. **Dotknięcie pustego miejsca** → na 3 s przycisk „Zakończ prezentację” w prawym górnym rogu (`close` w akcencie + napis w kolorze tekstu, powierzchnia z obrysem, cel 48 dp); **wstecz** też kończy. Po wyjściu — drzewo pionowo, ta sama osoba w środku, poziom 2 | tryb | dotknięcie osoby · pustego miejsca · wstecz | poziom 2 | — | **decyzja autora** (D11) · AC-8 · D16 |

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
| oddalenie (poziom 3–4) | 1, 3–5; imiona według *Open* 5; na chwilę pigułka „Poziom 3 · 66 osób” |
| rok w przeszłości (US-010) | 4 bez osób nieurodzonych, linie par według dat związku, 6 z rokiem |
| połącz — wybór (US-011) | 1, okno 7 nad drzewem |
| połącz — ścieżka (US-011) | 1, 3–6, 8 (reszta wyszarzona), 9 przez ok. 4 s |
| bez ścieżki (US-011) | 1, 3–6, 10 |
| osoba bez rodziny | 4: tylko ona, bez śladu; 5 („… · nie wiadomo jeszcze, kim jest dla Ciebie”, chyba że to „ja”) |
| osoba spoza rodziny „ja” | 4: jej rodzina; 5 z „nie wiadomo jeszcze, kim jest dla Ciebie” |
| „ja” niewybrane | 1 bez ikon; w miejscu drzewa, na środku: „Aplikacja nie wie jeszcze, która osoba to Ty.” (16 sp, tekst pomocniczy) i przycisk tekstowy w akcencie „Wybierz, która osoba to Ty” (jak [[osoba]] element 7); bez karty i + / −. Wejście z „Pokaż w drzewie” działa — wtedy 5 bez pokrewieństwa (D19) |
| pusta baza | 1 bez ikon; na środku „Tu pojawi się drzewo — osoby z grobów i ich rodziny.” (16 sp, tekst pomocniczy; jak „pusta baza” w [[osoby]]), bez działania (D19) |
| tekst 200% | 4 z szerszym miejscem osoby; 5 z „Pokaż ›” pod tekstem; + / − bez zmian, 48 dp (D20) |
| tryb prezentacji | 11 |
| błąd odczytu | „Nie udało się odczytać drzewa.” (tekst pomocniczy) i przycisk z obrysem „Spróbuj ponownie” (jak w [[osoby]]) |
| wczytywanie | wskaźnik postępu (lokalna baza — zwykle niewidoczny) |

## Sketch
```
┌──────────────────────────────────┐
│ Drzewo                    ↝  [▭] │  ← [▭] „Tryb prezentacji” (US-009) · ↝ „Połącz dwie osoby” (US-011)
│  (R)━(A)       (J)━(M)           │  ← ━ małżeństwo (róż), │ rodzic–dziecko (niebieski)
│    │             │               │
│ (E) (M)━━━━━(A)  (S)  (P)━(H)    │  ← rodzina partnera po prawej
│        │               │         │
│   (O) [JA]━━━━━(K)  (Mi)         │  ← [JA] znak „Ja”; pierścień — osoba w środku
│          │                   (+) │
│        (Z)                   (−) │  ← + / − (48 dp) w rogu drzewa: przybliż · oddal (S2)
│ ╭──────────────────────────────╮ │
│ │ (Ja) Mateusz Wymyślony       │ │
│ │      ur. 1983 · to Ty Pokaż ›│ │
│ │ ▶ 1880 ━━━━━━━━━━━━━━●  dziś │ │  ← suwak czasu — US-010
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
- **Imiona przy oddalaniu (I2, v1.6; v1.7 — D23):** tabliczka w kolorze tła (na jednolitym tle drzewa działa jak obwódka przy podpisach
  miast) i chowanie nakładających się ([[style-b]] reguła 13, v1.26), bo przy oddaleniu linie przechodzą pod podpisem; imię to tekst na tle,
  10,98:1.
- **Cel dotyku (v1.5):** na poziomie 4 poniżej 48 dp — wyjątek w [[style-b]] *Thresholds* (v1.24), D17.
- **Tryb prezentacji (v1.5):** „Zakończ prezentację” — powierzchnia z obrysem (3,40:1 na tle), `close` w akcencie (8,04:1 na powierzchni),
  napis w kolorze tekstu (10,02:1); pigułki na powierzchni w kolorze tekstu (10,02:1).
- **Tokeny (v1.5):** bez nowych — tylko istniejące pary (przeliczone z `theme.dart` 2026-10-13).

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| M9 — drzewo rodziny z powinowatymi i powtórnymi związkami | 3, 4 | poziom 2 od „Ja”: rodzice, dziadkowie, rodzeństwo, żona i jej rodzina po prawej |
| US-009 AC-1 — od „Ja” | 1, 3, 4, 5 | zakładka Drzewo: „Ja” w środku z pierścieniem, poziom 2 — rodzice, Kasia, dzieci, rodzeństwo, dziadkowie, rodzina Kasi po prawej |
| US-009 AC-2 — przestawianie środka | 4, 5 | dotknięcie Kasi → ona w środku z animacją, karta „ur. 1985 · Twoja żona”; drugie dotknięcie albo „Pokaż” → widok Kasi |
| US-009 AC-3 — dalsza rodzina (S2) | 3 | − → „Poziom 3 · 66 osób”; + albo podwójne dotknięcie → „Poziom 2 · 20 osób” |
| US-009 AC-4 — ślad dalszej rodziny | 4 | na poziomie 2 osoba z rodziną poza widokiem ma bladą kreskę 3/3: w górę rodzice, w dół dzieci, w bok partner |
| US-009 AC-5 — nazwa pokrewieństwa w karcie | 5 | „Twoja ciotka (siostra taty)” · „Twój stryj (brat taty)” · „Twój wuj (brat mamy)” · „Twoja siostra cioteczna (córka siostry taty)” · „Siostra cioteczna Twojego dziadka” (makieta, sekcja 2; D12) |
| US-009 AC-6 — „Pokaż w drzewie” | [[osoba]] 6 → 4, 5 | w widoku Franciszka „Pokaż w drzewie” → zakładka Drzewo, Franciszek w środku, poziom 2 |
| US-009 AC-7 — tekst 200% na 360 dp | 4, 5 | miejsce osoby 160 dp, imię 26 sp bez ucięcia, inicjały 1,3× w okręgu; „Pokaż ›” pod tekstem karty |
| US-009 AC-8 — tryb prezentacji | 1, 11 | ikona telewizora → poziomo, poziom 2 dopasowany, bez przycisków; dotknięcie pustego miejsca → „Zakończ prezentację” |
| M10 — suwak czasu: urodzenia, związki, zgony (US-010) | 6 | rok 1984: „Ja” jest, rodzice „razem” (przerywana), ślub 1985 — ciągła |
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
  jak w drzewie.
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
   *Obali:* miganie imion przy szczypaniu przeszkadza — wtedy I3.
4. ~~⚠️ OPEN — całe drzewo (K1) jako dodatkowy tryb? i ślad dalszej rodziny (D9) — tak czy nie?~~ — rozstrzygnięte 2026-10-13: K2
   bez K1, ślad — tak.
6. ~~⚠️ OPEN — kto mówi w karcie~~ — **rozstrzygnięte 2026-10-13: G1** (stop #1 [[ISSUE-033-tree-from-a-person]], *„Tak”*; dotyczy też
   banera 9 w US-011). Zapis sprzed decyzji (v1.5, AC-5): **G1** „Twoja babcia”, „Siostra cioteczna babci Twojej żony” · **G2** „Moja babcia”,
   „Siostra cioteczna babci mojej żony”. **Rekomendacja: G1.** Aplikacja wszędzie mówi do Ciebie („Wybierz, która osoba to Ty”, „…łączy się
   z Tobą”), a nagłówek „Jak łączy się ze mną” to pytanie, które sam zadajesz. Wybór obowiązuje też baner „Połącz dwie osoby” (9, US-011):
   przy G1 przykład z D6 brzmi „Siostra cioteczna babci Twojej żony”, a przykład w AC-5 US-009 trzeba poprawić. **Nie da:** zdania Twoim
   głosem, jak w notatkach. *Obali:* „Twoja” brzmi obco w aplikacji o własnej rodzinie.
