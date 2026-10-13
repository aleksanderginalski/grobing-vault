---
screen: "Osoba — widok osoby (kim była, rodzina, jak łączy się ze mną, daty, pochówek, zdjęcia)"
items: ["[[SPIKE-004-mvp-flow-prototype]]", "[[ISSUE-024-person-view]]", "[[ISSUE-027-cemetery-map-plan-photo-states]]", "[[US-009-drzewo-od-osoby]]"]
us: "M5 (brief §5, widok 4) — [[ISSUE-024-person-view]] AC-1…AC-5 (AC-6 → drzewo, v2.1)"
journey-step: "UJ-001 · 5 (widok 4, M5, R4 prawy)"
mockup: "2026-10-09: issue-024-widok-osoby.html (ISSUE-024; runda 1 stopu #1 — W2, łańcuch po imionach, pusta sekcja „Zdjęcia”) — katalog tymczasowy sesji, ścieżka w ISSUE-024 → Implementation plan · 2026-10-08: grobing-prototyp.html (SPIKE-004, panel 4)"
updated: 2026-10-12
---

# Osoba — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.18) · referencja: [[references]] → **R4 prawy**.
>
> **Wersje 1–1.3 — discovery na prototypie ([[SPIKE-004-mvp-flow-prototype]] D4, D13–D19, D27, D28, 2026-10-08).** Autor
> o panelu 4: *„jest super”*. Z prototypu: zdjęcie w tle jak na Facebooku zamiast gałązek (D3), płeć wraca dla nazw
> pokrewieństwa (D4), „Rodzina” to mini-drzewo (D5), pochówek prowadzi na mapę cmentarza (D9), a **bez źródeł i statusów**
> (D10 — *„moje notatki to moje notatki, nie potrzeba żadnych potwierdzeń skąd pochodzą”*).
>
> **Wersja 2 (2026-10-09, `ui` przed planem [[ISSUE-024-person-view]]):**
> - **sprzątanie:** *Open* 3 i 4 z v1.3 rozstrzygnięte (źródła przy relacjach — D10; ustawienie „ja” — [[ISSUE-022-app-skeleton-tabs-people-settings]]);
>   z sekcji 8 wypada wiersz „Nazwisko rodowe” (jest w imieniu, 4) i stan „spór źródeł” (D10);
> - **⚠️ OPEN 1 — zdjęcia w widoku: edycja (W1) czy tylko oglądanie (W2)**. Uwaga autora ze stopu #2 ISSUE-025 — *„aby
>   oglądanie danej osoby nie mieszało się z edycją tej osoby”* — przeczy przyciskom „Dodaj zdjęcie w tle” i „Dodaj
>   zdjęcie” z v1. Oba warianty na makiecie, rekomendacja W2;
> - **pochówek do czasu mapy cmentarza** prowadzi do listy grobów z zaznaczonym grobem (D17); mapa i pinezki to
>   [[US-007-mapa-cmentarza]] i [[US-008-pinezka-na-miejscu]];
> - **„Pokaż w drzewie” ukryte**, dopóki zakładka Drzewo jest zaślepką (D11);
> - **mini-drzewo dla kilku związków i wielu dzieci** (D12), **pierwsza linia „Jak łączy się ze mną”** z zaimkiem przy
>   właściwym odcinku (D13), **wejścia z formularza** (D14), **jedna poprawa osoby naraz** (D15);
> - **rozmiary tekstu według progów** [[style-b]] (D19): v1.3 miała 10, 12, 14 i 15 sp tam, gdzie próg mówi 13 albo 16 sp.
>
> **Wersja 2.1 (2026-10-09, stop #1 [[ISSUE-024-person-view]], runda 1 — decyzje autora):**
> - **W2** (*Open* 1): *„W2 jest dobry”* — widok tylko pokazuje zdjęcia; warianty W1 usunięte z elementów;
> - **„Jak łączy się ze mną” — same imiona i relacja każdego kroku** (D13'): *„łączenie ze sobą tylko po imionach oraz relacje
>   miedzy tymi osobami (mama, córka, brat, mąż itd - przypadki np. Brat stryjeczny prababki lub podobne zrobimy w widoku drzewa
>   przy łączeniu różnych osób)”*. Bez pierwszej linii „Twoja babcia”; słownik nazw złożonych i AC-6 → [[drzewo]] (D6);
> - **sekcja „Zdjęcia” także bez zdjęć** (element 10, D20): *„chciałbym mieć dla osoby bez zdjęć również miejsce na »zdjęcia«
>   abym wiedział że mogę tutaj je dodać na dole (lub połączyć z istniejącymi)”*. „Dodaj zdjęcie” otwiera poprawę z arkuszem
>   źródła — zapis dalej jeden, z „Zapisz” (W2). **„Połączyć z istniejącymi”** to nowy ekran — *Open* 6.

>
> **Wersja 2.2 (2026-10-09, po przeglądzie `ui` zbudowanego ekranu, [[ISSUE-024-person-view]]):**
> - **pierścień w akcencie rysuje się nad zdjęciem** (portret, osoba w środku mini-drzewa, okręgi łańcucha) — pod nim
>   zakrywał go nieprzezroczysty okrąg (MAJOR);
> - **tekst 200% (SC 1.4.4):** miejsce węzła mini-drzewa rośnie ze skalą tekstu, do dwóch razy (rola nie jest ucinana, imię
>   może — „…”); etykieta w „Daty” idzie nad wartość, gdy nie mieści się w 96 dp (słowa nie łamią się w środku); inicjały w
>   okręgach rosną najwyżej 1,3× (MAJOR, MINOR);
> - **łańcuch:** wiersz ≥ 48 dp (próg Androida; było ≥ 56), linia przechodzi przez okręgi bez przerw (MINOR);
> - **„małżonek”** w łańcuchu przy małżeństwie bez płci — jak „Małżonek” w mini-drzewie ([[rodzina]] *Role names*); element 6
>   wymieniał błędnie „Partner” (MINOR).

>
> **Wersja 2.3 (2026-10-09, stop #2 [[ISSUE-024-person-view]], runda 1 — decyzja autora, D21):** *„chciałbym móc kliknąć w ten
> obszar i od razu być przekierwany do listy zdjęć (domyślnie jest tam zwykłe tło) z tą osobą z możliwośią dodania zdjęcia
> powiązanego z tą osobą (aparatem lub z galerii) i po wybraniu ustawia się to tło”*. **Pasmo tła jest zawsze**; bez zdjęcia — zwykłe
> tło. **Dotknięcie pasma → wybór tła** ([[zdjecia-osoby]] v1.4): zdjęcia osoby i „Dodaj zdjęcie”; wybór zapisuje tło od razu.
> Jedyne wejście do zmiany w widoku poza ✎ i „Dodaj zdjęcie” (W2 dla reszty zdjęć zostaje).
>
> **Wersja 2.4 (2026-10-13, `ui` przed planem [[US-009-drzewo-od-osoby]], AC-6):** **„Pokaż w drzewie” wraca** (D11): przycisk tekstowy pod
> mini-drzewem, gdy osoba ma rodzinę. Prowadzi na zakładkę Drzewo z tą osobą w środku ([[drzewo]] D15). Do widoku osoby prowadzi też osoba w
> środku drzewa i „Pokaż” w jego karcie.

## Purpose
Zbierający stoi przy grobie albo przegląda notatki i chce wiedzieć, **kim była ta osoba i jak łączy się z nim** (UJ-001
krok 5, M5). Widzi zdjęcie w tle, portret, „kim była”, najbliższą rodzinę, łańcuch od siebie do tej osoby, daty i miejsce
pochówku. Stąd idzie do krewnych, na cmentarz, do zdjęć i — pod ✎ — do poprawy. **Ekran do oglądania:** poprawa ma jedno
wejście, ✎ ([[style-b]] reguła 15).

## Navigation
- **Wejście** (D14):
  - karta osoby w [[grob]];
  - karta osoby w [[osoby]]; karta „Ja” po wyborze „ja” → widok tej osoby;
  - **chip krewnego i karta partnera w sekcji „Rodzina” formularza** ([[wpis-osoby]] 9a) — widok kładzie się nad
    formularzem, który zostaje pod spodem z wpisanymi danymi; wstecz wraca do formularza;
  - węzeł mini-drzewa (6) i węzeł łańcucha (7) w innym widoku osoby;
  - osoba w środku drzewa albo „Pokaż” w karcie drzewa ([[drzewo]] 4, 5; v2.4) — zakładka Drzewo zostaje aktywna, wstecz wraca do drzewa.
- **Krewny → jego widok osoby**, na tym samym stosie: wstecz wraca do poprzedniej osoby.
- **✎ w pasku → [[wpis-osoby]] w trybie „poprawa”.** Po zapisie wraca tutaj, a widok pokazuje nowe dane (reguła 10).
  **Jeśli poprawa tej osoby już leży niżej w stosie** (np. formularz → chip męża → jego mini-drzewo → ta sama osoba),
  ✎ wraca do tamtej poprawy zamiast otwierać drugą (D15).
- **Pochówek (9) → [[cmentarz]] z zaznaczonym grobem.** Do czasu [[US-007-mapa-cmentarza]] to lista grobów (dziś
  zbudowany stan C), przewinięta do grobu tej osoby (D17). Z mapą: grób z pinezką — stan B, bez pinezki — stan C z
  komunikatem (D9). Wstecz z cmentarza wraca tutaj.
- **Zdjęcia (3, 10) — tylko do oglądania (W2, decyzja autora):** portret → podgląd profilowego w trybie oglądania, z poprzednim i następnym zdjęciem osoby;
  „Zdjęcia · N” → baza zdjęć osoby ([[zdjecia-osoby]]) w trybie oglądania. Profilowe i kolejne zdjęcia — przez ✎ → formularz →
  zdjęcia. **Pasmo tła → wybór tła** ([[zdjecia-osoby]] v1.4, D21): zdjęcie z siatki albo nowe (aparat, galeria) zapisuje się jako tło
  od razu i ekran wraca do widoku z tłem; „Bez zdjęcia w tle” zdejmuje tło. Zdjęcie tła na pełnym ekranie — z „Zdjęcia”. **Osoba bez zdjęć:** „Dodaj zdjęcie” w sekcji 10 → [[wpis-osoby]] „poprawa” z otwartym od razu
  arkuszem źródła ([[zdjecie]] A, tryb osoby) — po wyborze formularz z nowym zdjęciem, „Zapisz” → tutaj (D20; [[style-b]]
  reguła 15: formularz otwiera się od razu przy działaniu „Dodaj …”).
- **Bez ustawionego „ja”** — „Wybierz, która osoba to Ty” (7) → wybór „ja” ([[osoby]] elementy 6–7) → powrót tutaj z
  policzonym łańcuchem.
- **Dolny pasek** widoczny; aktywna zakładka, z której autor przyszedł ([[style-b]] reguła 12), także gdy widok otwarto
  z formularza.

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek** na tle: wstecz; po prawej ✎ (`edit_outlined`, akcent, cel 48 dp, `tooltip` „Popraw wpis”). Bez tytułu — imię niesie nagłówek (4) | pasek | wstecz; ✎ → [[wpis-osoby]] „poprawa” (D15) | — | — | R4 · [[style-b]] reguła 15 · D1 |
| 2 | **Pasmo tła — zawsze** (v2.3, D21) pod paskiem, na pełną szerokość, 140 dp, bez zaokrąglenia. **Z tłem:** zdjęcie przycięte ze środka, nic na nim (reguła 14). **Bez tła:** zwykłe tło — pasmo w kolorze powierzchni, w prawym dolnym rogu (12 dp od krawędzi) ikona `add_photo_alternate_outlined` w akcencie (24 dp) jako znak, że pasmo da się dotknąć (reguła 14: puste miejsce na zdjęcie tylko jako przycisk). Całe pasmo to jeden cel, a ikona ma `tooltip` „Zdjęcie w tle”. Opis dla czytnika: „Zdjęcie w tle — wybierz”, bez tła — „Zdjęcie w tle: brak — wybierz” | pasmo-przycisk | → wybór tła ([[zdjecia-osoby]] v1.4) | bez tła | — | **decyzja autora** (SPIKE-004 D17; stop #2, D21) · D3 |
| 3 | **Portret:** okrąg 104 dp z pierścieniem 2 dp w akcencie i delikatną poświatą, wyśrodkowany; **z tłem nachodzi do połowy na jego dolną krawędź**. Profilowe w kadrze łącza ([[kadr-profilowego]]), bez kadru — ze środka. Opis dla czytnika: „Zdjęcie profilowe — otwórz”. **Portret zawsze nachodzi na dolną krawędź pasma** (v2.3). **Bez zdjęcia:** okrąg 104 dp na powierzchni z obrysem 2 dp (obrys, nie akcent: to nie zdjęcie) i inicjałami (34 sp, półgrube, tekst pomocniczy), **bez akcji** i poza czytnikiem — jak węzeł bez zdjęcia w mini-drzewie (6); miejsce na dodanie zdjęć jest na dole (10) | zdjęcie / inicjały | zdjęcie → podgląd profilowego w trybie oglądania | — | — | R4 · **decyzja autora** (SPIKE-004 D14; W2 na stopie #1) · D2 |
| 4 | **Imię i nazwisko z „z d.”** (22 sp, półgruby, tekst, wyśrodkowane, zawijane bez ucinania) · **lata życia** (16 sp, tekst pomocniczy; [[style-b]] reguła 6: `1925–2004`, `ok. 1890 – 14.03.1951`, `ur. 1952`, `zm. 1951`, bez dat — nic). Odstęp 12 dp od portretu | tekst | — | — | — | R4 |
| 5 | **„Kim była”** w całości (16 sp, tekst, wyśrodkowane, odstęp 12 dp). Bez „kim była” — nic. **Bez linii źródła** (D10) | tekst | — | — | — | R4 · D16 |
| 6 | **Rodzina** — nagłówek sekcji (16 sp, półgruby) z ikoną `people_outline` w akcencie, jak w formularzu ([[wpis-osoby]] 9a). **Mini-drzewo jednego poziomu** (D5, D12): rząd rodziców nad osobą; w środku **osoba** z pierścieniem 2 dp w akcencie i poświatą, obok partnerzy (jeden — po prawej; dwa — wcześniejszy związek po lewej, późniejszy po prawej; kolejność pierwszej daty związku, bez dat — kolejność wpisania; trzeci i dalsi — dalej po prawej); **dzieci pod swoim związkiem** według daty urodzenia (rodzina jednego rodzica — pod osobą); przy dwóch związkach z dziećmi dzieci lewego kończą się przed osobą, a prawego zaczynają za nią, więc ich szyny się nie stykają. **Węzeł** (miejsce 80 dp, przy większym tekście systemowym szersze w tej samej proporcji, najwyżej 160 dp — v2.2): okrąg 44 dp (profilowe w kadrze albo inicjały na powierzchni z obrysem), pod nim **rola** (13 sp, tekst pomocniczy: „Matka”, „Ojciec”, „Mąż”, „Żona”, „Partner”, „Partnerka”, „Syn”, „Córka”; bez płci — „Rodzic”, „Małżonek” (małżeństwo), „Partner” („razem”), „Dziecko” — [[rodzina]] *Role names*; v2.2) i **imię** (13 sp, półgruby, tekst, jedna linia, ucięte „…”). **Linie jak w [[drzewo]]:** para — pozioma, kolor partnerów, ciągła przy małżeństwie, przerywana 5/4 przy „razem”; rodzic–dziecko — kolor relacji rodzic–dziecko, z połowy linii pary w dół, poziomą szyną do każdego dziecka. Bez zniczy (mini-drzewo nie ma czasu). **Szersze niż ekran → przewija się w poziomie**, na starcie osoba na środku, a ucięty węzeł przy krawędzi mówi, że jest dalej. Opis węzła dla czytnika: „Matka: Anna Wymyślona, 1897–1970 — otwórz”; linie poza czytnikiem. **„Pokaż w drzewie”** (v2.4, D11): pod mini-drzewem, do lewej, przycisk tekstowy w akcencie z ikoną `account_tree_outlined` (jedyne działanie dalej w sekcji — [[style-b]] reguła 1), cel 48 dp. Jest tylko wtedy, gdy osoba ma rodzinę — bez rodziny drzewo pokazałoby ją samą. Prowadzi na zakładkę Drzewo z tą osobą w środku, na poziomie 2 ([[drzewo]] D15). **Bez rodziny:** „Rodziny jeszcze nie ma. Dodasz ją pod ✎.” (16 sp, tekst pomocniczy) | mini-drzewo + przycisk tekstowy | węzeł krewnego → jego widok; węzeł osoby — bez akcji; „Pokaż w drzewie” → [[drzewo]] | — | — | R4 · **decyzja autora** (SPIKE-004 D15, D16, D18) · AC-2 · D4, D5, D12 |
| 7 | **Jak łączy się ze mną** — nagłówek (16 sp, półgruby) z ikoną `link` w akcencie (R4; D18). **Łańcuch od „Ja” — same imiona i relacja każdego kroku** (v2.1, D13'): wiersze ≥ 48 dp (v2.2) — okrąg 40 dp z pierścieniem 2 dp w akcencie nad zdjęciem (profilowe albo inicjały; **„Ja” zawsze jako znak „Ja”** w akcencie, jak w [[osoby]] D4) i podpis (16 sp, półgruby): **relacja do poprzedniej osoby i imię**, jak karta ścieżki w R3 — „Ja” · „Mama Anna” · „Jej mama Maria”; „Ja” · „Żona Kasia” · „Jej tata Marek” · „Jego siostra Ewa”. Relacje jednego kroku z płci osoby w wierszu: mama / tata, córka / syn, siostra / brat, żona / mąż (małżeństwo), partnerka / partner („razem”); bez płci — rodzic, dziecko, rodzeństwo, małżonek (małżeństwo) albo partner („razem”; v2.2). Zaimek „jej” / „jego” według rodzaju gramatycznego relacji w wierszu wyżej — mama, córka, siostra, żona, partnerka → „jej”; tata, syn, brat, mąż, partner, a także neutralne rodzic, dziecko, rodzeństwo → „jego” (rodzaj słowa, nie płeć osoby); pierwszy krok, po „Ja” — bez zaimka. **Bez nazw złożonych** („babcia”, „stryj”, „siostra cioteczna”) — te są w [[drzewo]] przy łączeniu dwóch osób (D6). Okręgi połączone pionową linią 2 dp w akcencie, bez przerw między okręgami (v2.2). Wiersze krewnych prowadzą do ich widoków; ostatni wiersz to ta osoba — bez akcji. Ścieżka: najkrótsza w grafie osoba–rodzina (krawędzie: rodzic, dziecko, rodzeństwo — dzieci tej samej rodziny, para); przy równej — mniej krawędzi „para”; dalej stała kolejność `id` (ISSUE-025 D2); liczona przy otwarciu, nie zapisywana ([[data-model]]). **Bez ścieżki:** „Nie wiadomo jeszcze, jak łączy się z Tobą — w drzewie brakuje rodziny między wami.” (16 sp, tekst pomocniczy). **Bez „ja”:** „Aplikacja nie wie jeszcze, która osoba to Ty.” i przycisk tekstowy w akcencie „Wybierz, która osoba to Ty”. **To „ja”** — sekcji nie ma | łańcuch | wiersz krewnego → jego widok; „Wybierz…” → wybór „ja” | najkrótsza ścieżka | — | R4 · R3 (karta ścieżki) · M5 · AC-3 · **decyzja autora** (stop #1) · D6, D13' |
| 8 | **Daty** — nagłówek (16 sp, półgruby) z ikoną `event_note_outlined` w akcencie. Wiersze z linią podziału w kolorze obrysu, ≥ 48 dp: etykieta (96 dp, 14 sp, tekst pomocniczy; gdy przy większym tekście się nie mieści — nad wartością, v2.2) · wartość (16 sp, tekst, reguła 6, z dopiskiem: „ok. 1890”, „między 1893 a 1895”). Wiersze: **Urodzenie**, **Zgon** (gdy są). Bez źródła i statusu (D10); wartość to pierwsza ([[ADR-006-claimed-value-separate-structures]] D3). Bez dat i bez pochówku — sekcji nie ma | lista wierszy | — (poprawa przez ✎) | — | — | **decyzja autora** (SPIKE-004 D27, D28) · D10 |
| 9 | **Pochówek** — ostatni wiersz sekcji 8, ≥ 64 dp: etykieta „Pochówek” · tytuł grobu (16 sp, tekst; bez nazwy — „Grób”, [[grob]] D1), pod nim nazwa cmentarza (14 sp, tekst pomocniczy) i adres kwatery, gdy jest („Kwatera B · Rząd 4 · Miejsce 12”, 14 sp, tekst pomocniczy); chevron. Opis dla czytnika: „Pochówek: Grób rodzinny Wymyślonych, Cmentarz parafialny w Wymyślonowie — pokaż na cmentarzu”. Bez pochówku (osoba żyjąca, osoba bez grobu w aplikacji) — brak wiersza | wiersz | → [[cmentarz]] z zaznaczonym grobem (D17) | — | — | M4 · FR-003 · AC-4 · **decyzja autora** (SPIKE-004 D19) · D9, D17 |
| 10 | **Zdjęcia · 4** — nagłówek (16 sp, półgruby) z ikoną `photo_library_outlined` w akcencie; rząd do 4 miniatur 56 dp (kwadraty, promień 8 dp, ze środka — reguła 14) i chevron; cały wiersz to jeden cel. Opis dla czytnika: „Zdjęcia osoby, 4 — otwórz”. **Bez zdjęć (v2.1, D20) — sekcja zostaje:** nagłówek „Zdjęcia”, pod nim „Ta osoba nie ma jeszcze zdjęć.” (16 sp, tekst pomocniczy) i przycisk z obrysem **„Dodaj zdjęcie”** (`add_a_photo_outlined` w akcencie, ≥ 48 dp, szerokość treści — reguły 1, 9) | rząd miniatur / pusty stan z przyciskiem | miniatury → [[zdjecia-osoby]] w trybie oglądania; „Dodaj zdjęcie” → poprawa z arkuszem źródła (*Navigation*) | — | — | [[US-005-zdjecia]] · **decyzja autora** (stop #1, D20) |

Odstępy ([[style-b]] reguła 5): margines boczny 16 dp, między sekcjami 24 dp, nagłówek sekcji → treść 8 dp.

**Dane, których ekran potrzebuje** (dla `planning`):
- osoba: imiona, nazwisko, rodowe, płeć, „kim była”, żyjąca; urodzenie i zgon (pierwsza wartość, z dopiskiem);
- profilowe z kadrem łącza; **tło — nowe wskazanie przy łączu osoba–zdjęcie** (AC-5, D3; zmiana schematu z migracją);
  liczba zdjęć i pierwsze 4;
- rodzina jednego poziomu: rodzice (z płcią i rodzajem ich związku), każdy związek osoby (partner, rodzaj — małżeństwo
  albo razem, pierwsza data — do kolejności i stylu linii), dzieci związku z datą urodzenia;
- „ja” (`Settings.mePersonId`) i **graf całej rodziny** (rodziny, partnerzy, dzieci, płeć) do ścieżki;
- pochówek: grób (tytuł, kwatera, rząd, miejsce) i cmentarz (nazwa).

## States
| Stan | Co widać |
|---|---|
| pełny | 1–10 |
| bez tła, z portretem | 1, pasmo w kolorze powierzchni z ikoną, portret na jego krawędzi, 4–10 |
| bez zdjęć | pasmo jak wyżej, okrąg z inicjałami na jego krawędzi; 10: „Ta osoba nie ma jeszcze zdjęć.” + „Dodaj zdjęcie” |
| bez rodziny | 6: „Rodziny jeszcze nie ma. Dodasz ją pod ✎.”; 7: bez ścieżki |
| bez ścieżki | 7: „Nie wiadomo jeszcze, jak łączy się z Tobą — w drzewie brakuje rodziny między wami.” |
| osoba bez płci w łańcuchu | jej wiersz z relacją neutralną („Jego rodzic Aleksander”); następny — „jego …” („Jego córka Zofia”) |
| bez „ja” | 7: „Aplikacja nie wie jeszcze, która osoba to Ty.” + „Wybierz, która osoba to Ty” |
| to „ja” | bez 7 |
| osoba żyjąca | lata „ur. 1952”; bez „Zgon” i bez 9 |
| bez dat i pochówku | bez 8 i 9 |
| mini-drzewo szersze niż ekran | 6 przewija się w poziomie, osoba na środku, ucięty węzeł przy krawędzi |
| wczytywanie | tło (lokalna baza — ułamek sekundy, bez wskaźnika, jak [[zdjecie]] „B — wczytywanie”) |
| błąd odczytu | „Nie udało się odczytać wpisu.” (16 sp, tekst pomocniczy) + przycisk tekstowy w akcencie „Spróbuj ponownie” |
| zapis tła — błąd (v2.3) | komunikat u dołu ekranu „Nie udało się zapisać zdjęcia w tle. Spróbuj jeszcze raz.” (jak wybór „ja”); tło bez zmian |
| plik zdjęcia bez odczytu | portret, tło albo miniatura: okrąg / pasmo / kwadrat na tle z `broken_image_outlined` (tekst pomocniczy), jak w [[grob]] |

## Sketch
```
┌──────────────────────────────────┐
│ ←                              ✎ │  pasek na tle
│▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓│  zdjęcie w tle 140 dp
│▓▓▓▓▓▓▓▓▓▓▓▓▓╭────────╮▓▓▓▓▓▓▓▓▓▓▓│
│             │ portret│            │  okrąg 104 dp, pierścień w akcencie
│             ╰────────╯            │
│   Maria Wymyślona z d. Testowa   │  22 sp
│            1925–2004             │
│  Nauczycielka w Wymyślonowie.    │  „kim była”, całość
│      Matka trojga dzieci.        │
│                                  │
│ 👥 Rodzina                        │
│      (Jó)━━━━━━(An)               │  rodzice — ━ małżeństwo (róż)
│      Ojciec      Matka            │
│           ┃                      │  ┃ rodzic–dziecko (niebieski)
│        [Maria]━━━━(JW)           │  osoba z pierścieniem, mąż po prawej
│                Mąż Jan           │
│           ┌─────┼─────┐          │
│         (An)  (St)  (Ze)          │  dzieci pod związkiem
│        Córka  Syn   Syn          │
│                                  │
│ 🔗 Jak łączy się ze mną           │
│ (Ja)  Ja                         │
│  │                               │  linia 2 dp w akcencie
│ (AW)  Mama Anna                  │
│  │                               │
│ (MW)  Jej mama Maria             │
│                                  │
│ 🗓 Daty                           │
│ Urodzenie      12.03.1925        │
│ Zgon           04.11.2004        │
│ Pochówek       Grób rodzinny W… ›│
│                Cmentarz paraf…   │
│                Kwatera B · Rząd 4│
│                                  │
│ 🖼 Zdjęcia · 4                    │
│ ▓▓  ▓▓  ▓▓  ▓▓                 › │
│  Mapa      Osoby      Drzewo     │
└──────────────────────────────────┘
```

## Tempo
n/a — ekran do oglądania. Poprawa idzie przez [[wpis-osoby]] (✎).

## Style B rules applied
- **Reguła 15:** widok przed poprawą; ✎ w pasku; zdjęcia tylko do oglądania (W2); „Dodaj zdjęcie” (10) otwiera formularz
  od razu, bo to działanie „Dodaj …”.
- **Reguła 14:** portret — okrąg w kadrze łącza; tło — prostokąt na pełną szerokość, przycięty ze środka, nic na nim;
  miniatury — kwadraty 56 dp, promień 8 dp. Okrąg z inicjałami bez zdjęcia nie jest pustym miejscem na zdjęcie (bez akcji,
  jak węzeł drzewa), więc nie łamie „puste miejsce tylko jako przycisk”; miejsce na zdjęcia to przycisk w sekcji 10.
- **Reguła 8:** bez gałązek (D3); bez zniczy w mini-drzewie (D12).
- **Reguła 3:** ikony nagłówków sekcji w akcencie (R4).
- **Reguła 11:** łańcuch i mini-drzewo to węzły bez chevronu; cel dotyku ≥ 48 dp (węzeł z podpisem, wiersz łańcucha).
  Wiersze z chevronem (9, 10) prowadzą dalej jak karty.
- **Reguła 1:** bez wypełnionego przycisku — ekran do oglądania; przyciski tekstowe w akcencie: „Wybierz, która osoba to Ty”
  (jedyne działanie dalej) i „Spróbuj ponownie”; „Dodaj zdjęcie” — drugorzędny z obrysem (reguła 9: pusty stan z jednym
  działaniem).
- **Reguła 2:** poświata tylko na portrecie i na osobie w środku mini-drzewa.
- **Reguły 6–7:** formaty dat i „z d.”; spokojne „Nie wiadomo jeszcze…”, bez ostrzeżeń.
- **Progi:** treść 16 sp, drobny tekst ≥ 13 sp (etykiety węzłów 13 sp — D19); kolor relacji nie jest jedynym nośnikiem
  rodzaju linii — niesie go też kształt i styl (SC 1.4.1).
- **Tokeny:** **wchodzą do `theme.dart` dwa zaproponowane w [[style-b]] v1.16** — `relParentChild` i `relPartners`
  (pierwsze użycie: mini-drzewo). Pomiar z v1.16: rodzic–dziecko 8,50:1 na tle, partnerzy 8,16:1 na tle (SC 1.4.11 ✅).
  Pierścień portretu i łańcucha — akcent/tło 8,81:1; obrys okręgu z inicjałami — obrys/tło 3,40:1; inicjały — tekst
  pomocniczy na powierzchni 5,01:1.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| AC-1 — osoba w grobie otwiera widok, ✎ poprawę | *Navigation*, 1 | karta Marii w grobie → widok Marii; ✎ → „Poprawa wpisu” |
| AC-2 — mini-drzewo z nazwami, dotknięcie → krewny | 6 | nad Marią „Ojciec Józef”, „Matka Anna”; obok „Mąż Jan”; pod nimi „Córka Anna”, „Syn Stanisław”; „Mąż Jan” → widok Jana |
| AC-3 (v2.1) — łańcuch po imionach z relacją kroku | 7 | Ja → Mama Anna → Jej mama Maria; `docs` przepisuje AC-3 przy zamknięciu (decyzja autora na stopie #1) |
| AC-4 — pochówek → cmentarz z zaznaczonym grobem | 9 | „Pochówek” → lista grobów Cmentarza parafialnego w Wymyślonowie przewinięta do „Grób rodzinny Wymyślonych” z obrysem w akcencie. **Do czasu [[US-007-mapa-cmentarza]] bez mapy i pinezki** (D17) — `planning` przepisuje AC-4 |
| AC-5 — tło nad portretem; stara kopia bez tła | 2, 3 · [[zdjecia-osoby]] v1.4 · [[zdjecie]] B4'' | pasmo → „Zdjęcie w tle” → zdjęcie (albo nowe z aparatu, galerii) → widok z tłem od razu (D21); druga droga: ✎ → zdjęcia → podgląd → „Ustaw jako tło” → „Zapisz” |
| ~~AC-6 — słownik: ciotka, stryj, wuj, siostra cioteczna~~ | — | **→ [[drzewo]]** (v2.1, decyzja autora: nazwy złożone przy łączeniu dwóch osób) |
| [[US-009-drzewo-od-osoby]] AC-6 — „Pokaż w drzewie” (v2.4) | 6 → [[drzewo]] 4, 5 | w widoku Franciszka pod mini-drzewem „Pokaż w drzewie” → zakładka Drzewo, Franciszek w środku, poziom 2; u osoby bez rodziny przycisku nie ma |
| D20 — miejsce na zdjęcia bez zdjęć | 10 | Józef bez zdjęć: „Ta osoba nie ma jeszcze zdjęć.” + „Dodaj zdjęcie” → poprawa z arkuszem źródła → zdjęcie → „Zapisz” → widok z portretem |
| *Input from ISSUE-025* — chipy i karta partnera → widok osoby | *Navigation* · [[wpis-osoby]] 9a v5.8 | w formularzu Marii chip „Syn: Stanisław” → widok Stanisława; wstecz → formularz z wpisanymi danymi |
| M5 — kim była, relacje, łańcuch do „ja” | 4–7 | jak wyżej |

## Decisions
- **D1 — widok przed poprawą** ([[style-b]] reguła 15, SPIKE-004 D4). Do formularza prowadzi tylko ✎. *Obali:* autor
  przy przepisywaniu częściej poprawia, niż ogląda — wtedy szybka ścieżka do poprawy z [[grob]].
- **D2 — portret u góry** (SPIKE-004 D14; R4). Autor: *„chciałbym mieć tam również ich portret”*.
- **D3 — zdjęcie w tle jak na Facebooku, bez gałązek** (SPIKE-004 D17). Autor: *„Tutaj bym zrobił »tło zdjęcia« tak jak
  na facebooku”*. Tło wybiera autor z bazy zdjęć osoby, więc **w danych potrzebne jest wskazanie tła** przy łączu
  osoba–zdjęcie ([[ADR-009-person-photos-record-and-link]]) i działanie „Ustaw jako tło” w podglądzie ([[zdjecie]] v1.5).
  *Obali:* większość osób nie ma żadnego zdjęcia poza portretem — wtedy pasmo „Dodaj zdjęcie w tle” stoi pusto na
  większości ekranów (to jeden z powodów rekomendacji W2, *Open* 1).
- **D4 — płeć; nazwy pokrewieństwa po polsku** (SPIKE-004 D16). Zbudowane w ISSUE-025 (płeć, role); słownik i ścieżka —
  ISSUE-024 (D13).
- **D5 — „Rodzina” jako mini-drzewo** (SPIKE-004 D15, D18). Autor: *„widzielibyśmy najbliższą rodzinę danej osoby (rodzice,
  dzieci, partner/partnerzy)”*.
- **D6 — kolejność sekcji: kim była → Rodzina → Jak łączy się ze mną → Daty → Zdjęcia.** Autor: *„jest super”*.
- ~~**D7 — źródło przy każdej dacie**~~ — obalone przez D10.
- ~~**D8 — „Dopisz, co mówi babcia”**~~ — obalone (SPIKE-004 D27).
- **D9 — pochówek prowadzi na mapę, nie do grobu** (v1.1, SPIKE-004 D19). Autor: *„Osoby -> Wybrana osoba -> Miejsce
  pochówku -> I jestem kierowany na widok Cmentarza z zaznaczoną pinezką”*. Grób bez pinezki → lista z zaznaczonym grobem i
  komunikatem „Ten grób nie ma jeszcze pinezki — jest zaznaczony na liście.” Do czasu mapy — D17. *Obali:* przy
  przepisywaniu autor częściej chce do grobu niż na mapę — wtedy dwa wiersze: „Grób” i „Na mapie”.
- **D10 — bez źródeł i statusów** (v1.3, SPIKE-004 D28). *Obali:* rodzina po autorze pyta, skąd jest data — wtedy źródło
  wraca najpierw do eksportu (dane i tak je mają).
- **D11 — „Pokaż w drzewie” ukryte, dopóki Drzewo jest zaślepką** (v2). Przycisk z treści, który prowadzi do „Drzewo
  powstanie…”, obiecuje coś, czego nie ma; zaślepka jest tymczasowa i nie jest celem nawigacji ([[style-b]] reguła 12).
  Przycisk dochodzi z pozycją drzewa ([[SPIKE-002-tree-on-a-phone]] → drzewo). *Obali:* autor chce widzieć na stopie #1,
  gdzie drzewo się pojawi — wtedy przycisk z zaślepką. **v2.4:** zaślepka znika z [[US-009-drzewo-od-osoby]], więc przycisk wraca
  (element 6). To przejście na zakładkę Drzewo, a nie drzewo na stosie widoku osoby ([[drzewo]] D15).
- **D12 — mini-drzewo dla prawdziwych rodzin** (v2). Prototyp miał jeden związek i do trzech dzieci; notatki starszych
  pokoleń mają po 6–10 dzieci i powtórne związki. Dwa związki — po obu stronach osoby (układ znany z drzew
  genealogicznych: pierwszy mąż · ona · drugi mąż), dzieci pod swoim związkiem, a szersze niż ekran przewija się w
  poziomie z osobą na środku, a ucięty przy krawędzi węzeł mówi, że rząd jest dłuższy (bez dodatkowego znaku). Etykiety 13 sp
  zamiast 10/12 sp z prototypu (D19), więc miejsce na węzeł 80 dp — 4 węzły w rzędzie przy 360 dp. Bez zniczy: prototyp
  pokazywał je tylko z suwakiem czasu, a mini-drzewo czasu nie ma. *Obali:* przy rodzinie z 8 dziećmi autor nie zauważa,
  że rząd się przewija — wtedy dzieci zawijane w kolejne rzędy.
- ~~**D13 — pierwsza linia „Jak łączy się ze mną”: zaimek przy odcinku najbliższym „ja”** (v2).~~ **Zastąpione w v2.1 przez
  D13'.** Zapis v2: „Twoja żona taty” znaczy
  coś innego niż „Żona Twojego taty” — zaimek należy do odcinka, który łączy się ze mną, więc w opisie stoi w dopełniaczu
  przy ostatnim odcinku („…babci Twojej żony”). Nazwa ze słownika dostaje zaimek z przodu („Twoja babcia”). Nawias i opis
  neutralny — z tabeli D2 ISSUE-025 (dawne [[osoby]] D8, D9). Łańcuch pod spodem mówi to samo krok po kroku, więc nawias
  zostaje tylko tam, gdzie słownik go podaje. *Obali:* autor uzna nawias za zbędny przy łańcuchu tuż pod nim.
- **D13' — łańcuch po imionach z relacją jednego kroku** (v2.1, decyzja autora na stopie #1). Autor: *„łączenie ze sobą tylko
  po imionach oraz relacje miedzy tymi osobami (mama, córka, brat, mąż itd …)”*; nazwy złożone — w drzewie przy łączeniu
  dwóch osób ([[drzewo]] D6). Forma podpisu z karty ścieżki R3 (*„Ja → żona Kasia → jej tata Marek → jego siostra Ewa → jej mąż
  Józef”*): relacja do poprzedniej osoby i imię, zaimek z rodzaju słowa w wierszu wyżej (dzięki temu działa też przy osobie bez płci: „Jego rodzic Aleksander” → „Jego córka Zofia”). Widok osoby potrzebuje więc tylko
  czterech relacji z płcią, a nie słownika. *Obali:* przy długich łańcuchach (5+ kroków) autor gubi, kim osoba jest dla
  niego — wtedy wraca jedna linia z nazwą ze słownika, gdy drzewo go zbuduje.
- **D14 — każde dotknięcie osoby prowadzi do widoku, także w formularzu** (v2; uwaga autora ze stopu #2 ISSUE-025: *„po
  wybraniu osoby najpierw wejść w jej »profil« z najważniejszymi informacjami a dopiero potem w edycję”*). Chip krewnego
  i karta partnera w formularzu otwierają widok nad formularzem; formularz czeka pod spodem z wpisanymi danymi.
- **D15 — jedna poprawa osoby naraz** (v2). Widok otwierany z formularza pozwala dojść do tej samej osoby drugi raz (żona →
  mąż → jego mini-drzewo → żona) i otworzyć drugą poprawę tej samej osoby nad pierwszą, niezapisaną. Zapis drugiej, a
  potem pierwszej nadpisałby nowsze dane starszymi. ✎ dla osoby, której poprawa leży już w stosie, wraca do niej.
  *Obali:* nic — to ochrona danych, nie wygląd.
- **D16 — „kim była” w całości, wyśrodkowane** (v2). Pole w formularzu nie ma limitu, a ekran jest po to, żeby to
  przeczytać; ucinanie po 4 liniach z „więcej” to dodatkowe dotknięcie przy każdej dłuższej biografii. *Obali:* biografie
  z notatek mają po kilkanaście linii — wtedy dłuższy tekst do lewej (wyśrodkowane długie akapity czyta się gorzej).
- **D17 — pochówek do czasu mapy: lista grobów z zaznaczonym grobem, bez komunikatu o pinezce** (v2). Dziś zbudowany
  cmentarz to sama lista (stan C), a pinezek nie da się jeszcze postawić. Komunikat „Ten grób nie ma jeszcze pinezki”
  mówiłby o czymś, czego w aplikacji nie ma; wraca z mapą (D9). Lista przewija się do grobu, a karta ma obrys w akcencie
  ([[cmentarz]] D11) i stan „zaznaczony” dla czytnika. *Obali:* autor woli od razu grób (jedno dotknięcie mniej) — wtedy
  do czasu mapy pochówek → [[grob]].
  **v2.4 (2026-10-12, [[ISSUE-027-cemetery-map-plan-photo-states]], [[cmentarz]] D23):** mapa przychodzi przed pinezkami, więc
  D17 trwa aż do [[US-008-pinezka-na-miejscu]]. Grób z pinezką (na razie tylko w danych testowych) → mapa w stanie B z tym
  grobem, a grób bez pinezki → lista jak wyżej, bez komunikatu. Komunikat z D9 wraca z US-008.
- **D18 — ikony nagłówków.** „Rodzina” — `people_outline`, jak w formularzu (ta sama sekcja, ta sama ikona; R4 ma dwie
  postacie). „Jak łączy się ze mną” — `link` (ogniwo z R4): `conversion_path` z v1 **nie istnieje** w `Icons` Fluttera
  3.41.1 (sprawdzone w SDK 2026-10-09).
- **D20 — sekcja „Zdjęcia” także bez zdjęć** (v2.1, decyzja autora na stopie #1). Autor chce wiedzieć, że tu dodaje zdjęcia.
  Pusty stan z jednym działaniem (reguła 9); „Dodaj zdjęcie” otwiera poprawę z arkuszem źródła, więc zapis zdjęć zostaje
  jeden — „Zapisz” w formularzu (W2). Okrąg portretu bez zdjęcia zostaje bez akcji: jedno miejsce na dodanie, na dole.
  *Obali:* autor szuka dodania zdjęcia w okręgu portretu — wtedy okrąg z inicjałami też prowadzi do tego samego działania.
- **D21 — pasmo tła zawsze, dotknięcie → wybór tła, zapis od razu** (v2.3, decyzja autora na stopie #2, runda 1). Autor chce
  ustawić tło jednym dotknięciem miejsca, gdzie tło stoi, a nie przez ✎ i podgląd (6 dotknięć z W2). Wybór tła zapisuje się od
  razu, jak zdjęcie nagrobka w [[grob]]: to wybór obrazu, nie wpis do poprawy. Bez tła pasmo ma małą ikonę w akcencie (inaczej
  dotykalne miejsce byłoby niewidoczne — reguła 14). Zdjęcie dodane osobie bez zdjęć staje się też jej profilowym: pierwsze zdjęcie
  osoby jest profilowym ([[ADR-009-person-photos-record-and-link]]); profilowe zmienia się pod ✎. *Obali:* autor chce z pasma też
  obejrzeć zdjęcie tła na pełnym ekranie — wtedy w wyborze tła przycisk „Pokaż”.
- **D19 — rozmiary tekstu według progów** (v2). v1.3 (z prototypu) miała rolę 10 sp, imię w węźle 12 sp, „kim była” 15 sp,
  łańcuch i daty 14 sp. Progi [[style-b]]: treść ≥ 16 sp, drobny tekst ≥ 13 sp. Treść (imię, „kim była”, daty, łańcuch)
  — 16 sp; etykiety węzłów mini-drzewa — 13 sp (krótka etykieta pod okręgiem, jak podpis zakładki — ale bez wyjątku od
  13 sp, bo mieści się).

## Open
1. ~~⚠️ OPEN — zdjęcia w widoku: edycja (W1) czy tylko oglądanie (W2)~~ — **W2** (decyzja autora na stopie #1: *„W2 jest
   dobry”*). Zapis kandydatów:
   - **W2 (rekomendacja):** widok tylko pokazuje zdjęcia. Bez tła — bez pasma; bez zdjęcia — okrąg z inicjałami; tło,
     portret i „Zdjęcia” otwierają podgląd i bazę **bez działań**. Dodanie zdjęcia, profilowe i tło — przez ✎ (formularz
     → zdjęcia, jak dziś), zapis z „Zapisz”. Za: uwaga autora o oddzieleniu oglądania od edycji; jeden sposób zapisu
     zdjęć osoby (z formularzem, [[zdjecia-osoby]] D1); bez pustych pasm na większości z ok. 100 widoków (D3). Koszt: tryb
     oglądania w bazie i podglądzie (ukryte działania). Przeciw: tło to 6 dotknięć (✎, okrąg zdjęć, zdjęcie, „Ustaw jako
     tło”, wstecz, „Zapisz”);
   - **W1 (jak v1, prototyp):** „Dodaj zdjęcie w tle” i „Dodaj zdjęcie” w widoku, zmiany zdjęć z widoku zapisują się od
     razu. Za: tło w 3 dotknięciach, wygląd z prototypu (*„jest super”*). Przeciw: edycja w widoku i **dwa sposoby zapisu**
     tej samej bazy zdjęć — z formularza przez „Zapisz”, z widoku od razu.
2. ~~⚠️ OPEN — mini-drzewo~~ — rozstrzygnięte w v1.1 (D5, D18 SPIKE-004).
3. ~~⚠️ OPEN — źródło przy dacie na ekranie~~ — bez źródeł (D10).
4. ~~⚠️ OPEN — źródło przy relacjach~~ — bez źródeł na ekranie (D10, SPIKE-004 D28); twierdzenia zostają w danych
   ([[ADR-011-relation-claims-family-and-child-link]]).
5. ~~⚠️ OPEN — ustawienie „ja”~~ — zbudowane w [[ISSUE-022-app-skeleton-tabs-people-settings]] ([[ustawienia]] element 1,
   [[osoby]] 6–7).
6. ~~⚠️ OPEN — „połączyć z istniejącymi”~~ — **osobna pozycja po ISSUE-024** (decyzja autora na stopie #1, runda 2: *„jest
   dobrze”*). Zapis (v2.1, uwaga autora przy D20): dodać osobie zdjęcie, które już jest w aplikacji
   (np. zdjęcie grupowe z bazy innej osoby). Dziś da się to zrobić od strony zdjęcia: w podglądzie zdjęcia innej osoby „Na
   zdjęciu · Zmień” → zaznaczyć tę osobę ([[zdjecie]] D). Od strony osoby potrzeba nowego źródła w arkuszu („Ze zdjęć w
   aplikacji”) i **nowego ekranu wyboru** spośród wszystkich zdjęć osób (jak znaleźć jedno wśród kilkuset — siatka według
   osób, wyszukiwarka). Rekomendacja `ui`: osobna pozycja po ISSUE-024 — nowy ekran ze specyfikacją i makietą, a ISSUE-024
   już jest duża.
