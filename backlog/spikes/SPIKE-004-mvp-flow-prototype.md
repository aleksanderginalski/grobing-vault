---
title: "SPIKE-004 — Is the full MVP flow what the author wants? (clickable prototype, one panel at a time)"
type: spike
status: done
priority: MUST
time-box: "2 sessions"
hypotheses: []
prototype: "grobing-prototyp.html — %TEMP%\\claude\\c--Programowanie-Grobing-grobing-agents\\e2987d63-950d-4e55-b9fb-24429bf1ed09\\scratchpad\\ (poza repo, wyłącznie wymyślone osoby)"
quality-verdict: APPROVED
verdict-date: 2026-10-08
verdict-reviewer: self-check
source: "Decyzja autora 2026-10-08 w /pm: discovery przed SPIKE-002 — „pełne MVP flow na podstawie naszych moodboardów, jeden panel na raz”"
created: 2026-10-08
updated: 2026-10-08
---

# SPIKE-004 — Pełny przepływ MVP na klikalnym prototypie (S-FLOW)

## The question
**Czy pełny przepływ MVP (widoki 1–5 i M1–M11 z briefu §5) to to, czego autor chce?** Sprawdzamy to na klikalnym
prototypie, zanim powstanie więcej kodu.

## Why it matters
- Autor wpisze prawdziwe dane dopiero po instalacji gotowego MVP na telefonie, a do tego czasu ocenia aplikację na
  wymyślonych danych (decyzja autora 2026-10-08, [[CURRENT_STATE]] uzupełni `docs` przy zamknięciu). „Feeling”
  zbudowanych ekranów pokazał dwie rozbieżności z oczekiwaniem:
  - **brak dolnych zakładek** jak w R1. [[style-b]] reguła 12 planuje pasek Mapa · Osoby · Drzewo dopiero przy
    dwóch celach, a dziś jest tylko Mapa;
  - **osoba z grobu otwiera się od razu w edycji.** [[grob]]: „Docelowo: widok osoby (M5, R4 prawy)”, a widok
    osoby jeszcze nie powstał.
- Obie dotyczą **architektury informacji**: cele najwyższego poziomu i zasady „widok → ✎ edycja”. Wygląd jednego
  ekranu to dopiero następna warstwa. Taka zmiana na makiecie kosztuje mniej niż w kodzie:
  [[2026-10-06-retro-01]] → *What worked* (makieta przed kodem) i [[2026-10-08-retro-02]] R6 („autor decyduje,
  patrząc”).

## Steps
1. **Panel po panelu** w jednym pliku HTML (rama telefonu, przełączanie ekranów, kolory z `theme.dart`, wyłącznie
   wymyślone osoby). Pod ramką etykieta: „jak dziś w aplikacji” · „zmiana względem aplikacji” · „nowe — nie
   zbudowane”.
2. Kolejność paneli to propozycja, a autor może przeskoczyć dalej przez „otwórz…”:
   - 0 szkielet (zakładki, koło zębate, „widok → ✎”);
   - 1 mapa Polski;
   - 2 cmentarz;
   - 3 grób;
   - 4 osoba;
   - 5 zakładka Osoby;
   - 6 zakładka Drzewo (kandydaci do [[SPIKE-002-tree-on-a-phone]], bez rozstrzygania H4);
   - 7 wizyta (pinezka, offline);
   - 8 fakt od babci ([[US-004-fakt-od-babci]]);
   - 9 ustawienia, kopia i eksport ([[US-006-eksport-dla-rodziny]]).
3. **Konsensus autora** → w tej samej turze wiersz w *Findings* i nowa wersja specyfikacji w `05_DESIGN/`
   (pisze `ui`). Zmiana zakresu MVP to decyzja autora, nazwana wprost.

## Exit criterion
Konsensus dla paneli 0–9 albo świadome „dalej nie teraz” autora. Każda decyzja ma specyfikację, a każda zmiana w
kodzie ma pozycję backlogu.

## Definition of Done
- [ ] Dziennik decyzji w *Findings*: każdy D# ze specyfikacją (wersja) i z „zmiana w kodzie → pozycja” albo „brak”.
- [ ] Specyfikacje w `05_DESIGN/` zgodne z dziennikiem i ze sobą nawzajem.
- [ ] Zmiany w kodzie zamienione na pozycje albo dopisane do US/EPIC. Nowa kolejność do instalacji MVP w
      `CURRENT_STATE.md`.
- [ ] Prototyp poza repo. Zero danych rodziny.

## Implementation plan
> Zatwierdzony przez autora 2026-10-08 (tryb planu w sesji `/pm`, wybór: plik lokalny na PC).

- **Kto:** `ui` prowadzi panele w trybie krok po kroku, na wyraźne życzenie autora. To nie jest nowy punkt stopu w
  `autonomous-flow.md`. `docs` zakłada i zamyka pozycję.
- **Jawny wyjątek od własności:** sekcję *Findings* tego spike'a pisze `ui`, nie `dev` (w zwykłym spike'u produktem
  jest kod; tu decyzja na makiecie).
- **Skill `ui` bez zmian.** Proces „ekran po ekranie z zapisem decyzji” robimy pierwszy raz. Jeśli zadziała, retro
  zdecyduje, czy zostaje trybem `ui` (framework dopiero z 2 instancji).
- **Prototyp:** `grobing-prototyp.html` w scratchpadzie tej sesji (ścieżka we frontmatterze), otwierany w
  przeglądarce na PC. Nigdy w repo: `*.html` blokuje `.gitignore` i strażnik. Prawdą jest specyfikacja, nie plik.
- **Dane:** wymyślone, wzór `grobing-code/lib/dev/fictional_data.dart`: 2–3 cmentarze, kilka grobów, ok. 15–20 osób z
  powtórnym związkiem i powinowatymi. Bez złocenia.
- **Przy zamknięciu (`docs`):**
  - pozycje dla zmian w kodzie;
  - w `CURRENT_STATE` nowa kolejność do instalacji MVP i zasada autora „wymyślone dane do instalacji”, a także
    rozstrzygnięcie pytania o rozmowę z babcią: na kartce, wpis po instalacji;
  - wiersz w `TRACEABILITY.md`, licznik retro +1;
  - commit i push paczki. Jeśli pozycja przejdzie na drugą sesję, koniec pierwszej mówi wprost, które pliki czekają.

**Czego to nie da:** tempa wpisywania, pikseli ani gestów Fluttera. Nie da też czytelności drzewa ~100 osób na
telefonie (H4, [[SPIKE-002-tree-on-a-phone]]) ani słońca, GPS i offline na cmentarzu (wyjątki telefonu w
`DEFINITION_OF_DONE.md`).

## Findings
> Dziennik decyzji — pisze `ui` przy każdym konsensusie autora.
>
> **Stan (2026-10-08):** panele 0–3 ustalone, panel 4 ustalony z trzema zmianami (D15–D17), [[osoba]] v1 zapisana.
> Na prośbę autora (*„śmiało zrób więcej kroków do przodu”*) prototyp ma też **panele 5–9 do oceny**: widok osoby w
> wersji 2 (zdjęcie w tle, nazwy z płcią, mini-drzewo), zakładkę Osoby, Drzewo od osoby z suwakiem czasu i „Połącz dwie
> osoby”, pinezkę z GPS na miejscu i stan bez internetu, fakt od babci (wszystkie źródła jednego faktu) oraz ustawienia
> z eksportem. Specyfikacje paneli 5–9 powstaną po ocenie autora.

| D# | Panel | Decyzja | Autor (cytat, data) | Specyfikacja (wersja) | Zmiana w kodzie → pozycja |
|---|---|---|---|---|---|
| D1 | 0 | Dolny pasek Mapa · Osoby · Drzewo jak w R1; ustawienia pod kołem zębatym na mapie | *„1. tak”* (2026-10-08) | [[style-b]] v1.12 reguła 12 · [[cmentarze]] v2.3 element 18, D26 · [[references]] | **tak** — pasek dolny i zakładki → pozycja przy zamknięciu |
| D2 | 0 | Pasek widoczny na ekranach do oglądania (mapa, cmentarz, grób, osoba, listy, drzewo), ukryty w formularzach, oknach, trybach wyboru i na zdjęciu na pełnym ekranie | *„2. tak zostaje”* (2026-10-08) | [[style-b]] v1.12 reguła 12 | **tak** — razem z D1 |
| D3 | 1 | Wyszukiwarka na mapie szuka tylko cmentarzy, na stałe; osoby szuka zakładka Osoby | *„3. Tylko cmentarze, jeżeli ktoś będzie chciał poszukać osoby to wejdę w zakładkę osoby”* (2026-10-08) | [[cmentarze]] v2.3 D27 (zmienia D2) · [[style-b]] reguła 12 · [[references]] | brak (dziś już tak) |
| D4 | 0 | Dotknięcie cmentarza, grobu i osoby otwiera widok, a poprawa jest pod ✎, w całej aplikacji | *„4. ok”* (2026-10-08) | [[style-b]] v1.12 reguła 15 | **tak** — karta osoby w grobie i chipy rodziny prowadzą do widoku osoby → razem z widokiem osoby (panel 4) |
| D5 | 1 | Arkusz cmentarza ma zdjęcie cmentarza zrobione przez autora: miniatura z lewej (R1); bez zdjęcia pole „Dodaj zdjęcie”; miniatura → zdjęcie na pełnym ekranie ze „Zmień” i „Usuń” | *„Arkusz cmentarza chciałbym aby miał zdjęcie tego cmentarza (zrobione przezemnie lub informacje »dodaj zdjęcie«)”* · *„1 tak”* (2026-10-08) | [[cmentarze]] v2.4 element 6a, D28 · [[style-b]] v1.13 reguła 14 | **tak** — zdjęcie cmentarza to nowe pole w danych (zmiana zakresu względem M1: brief ma zdjęcie nagrobka) → pozycja |
| D6 | 1 | Mapa Polski jak R1 (wariant B): sąsiedzi, Bałtyk i jeziora, rzeki w kolorze wody, granica Polski w kolorze tekstu pomocniczego, „Polska”, 11 miast; bez faktury terenu | *„Mapa Polski B - jest ok”* (2026-10-08) | [[cmentarze]] v2.4 element 3, D29 · [[style-b]] v1.13 (rola wody, reguła 13) | **tak** — `tool/map/extract_poland.dart`, `assets/map/poland.json`, tokeny wody w `theme.dart` → pozycja |
| D7 | 1 | Bez arkusza Polska wyśrodkowana w obszarze mapy; po otwarciu arkusza mapa płynnie przesuwa się nad arkusz | *„powinna być bardziej wycentrowana (ale na widoku z otworzonym cmentarzem jest idealnie)”* (2026-10-08) | [[cmentarze]] v2.4 element 3, D30 | **tak** — razem z D6 |
| D8 | 2 | Cmentarz to mapa: plan schematyczny OSM z plakietką „Plan offline” i przełącznikiem Plan / Zdjęcie (ortofotomapa GUGiK tylko online); „Dodaj grób” zostaje | *„Plan i zdjęcie ok, dodaj grób ok”* (2026-10-08) | [[cmentarz]] v4 D10 · [[style-b]] v1.14 (reguła 13, zieleń offline) | **tak** — mapa cmentarza (M3, [[ADR-003-map-source-offline]]) → pierwsza US [[EPIC-002-wizyta]] |
| D9 | 2 | Na starcie sama mapa, bez listy grobów. Znicz → arkusz **jednego** grobu z „Pokaż grób”. Przeciągnięcie arkusza w górę → cała lista grobów **bez mapy**, a z listy → grób | *„list grobów nie chce aby była - dopiero po kliknięciu na pineske chciałbym aby ten jeden grób się pojawił. Dopiero gdy mamy jeden grób zaznaczony i przeciągamy ten pasek (zrzut) to widzimy całą liste (ale wtedy nie widzimy mapy cmentarza)”* (2026-10-08) | [[cmentarz]] v4 D11 (zastępuje D1, D3, D4) | **tak** — razem z D8 |
| D10 | 2 | **Bez linku do Grobonetu i do wyszukiwarki zarządcy** w aplikacji. Z Grobonetu autor chciał tylko plany cmentarzy, a te daje plan schematyczny z kwaterami. **Zmiana zakresu:** brief M3 ma „link do Grobonetu” | *„Nie wykorzystujemy tej funkcjonalności, z grobonetu chciałem tak naprawdę tylko te mapki”* (2026-10-08) | [[cmentarz]] v4 D12 | brak (nie zbudowane); [[EPIC-002-wizyta]] → M3 i pole linku poprawi `docs` przy zamknięciu |
| D11 | 2 | Kwatery to strefy z nazwą, zaznaczone przerywaną linią; kwatera bez strefy żyje tylko w adresach | *„4) ok”* (2026-10-08) | [[cmentarz]] v4 D13 · [[style-b]] v1.14 reguła 13 | **tak** — razem z D8 |
| D12 | 2 | W stanie mapy pasek grobów na dole: liczba grobów i grobów bez pinezki, dotknięcie albo przeciągnięcie → lista; **„Dodaj grób” wypełniony, taki sam jak pod listą**. Przepływ znicz → jeden grób → lista → grób potwierdzony | *„1 ok, ale chciałbym aby wygląd przycisku »dodaj grób« był konsekwentny z tym co jest po rozwinięciu tego paska grobów”* · *„2. tak”* (2026-10-08) | [[cmentarz]] v4.1 elementy 1–9, D14 (specyfikacja przepisana na trzy stany) | **tak** — razem z D8 |
| D13 | 3 | Widok grobu zostaje jak zbudowany; karta osoby → widok osoby, poprawa pod ✎ w widoku osoby; dolny pasek widoczny | *„1 ok”* · *„2 ok przy czym chciałbym mieć tam również ich portret”* (2026-10-08) | [[grob]] v5 | **tak** — karta osoby → widok osoby (razem z D4) |
| D14 | 4 (wejście) | Widok osoby zaczyna się od **portretu** osoby (profilowe, R4 prawy) | *„chciałbym mieć tam również ich portret”* (2026-10-08) | [[osoba]] v1 D2 | razem z widokiem osoby |
| D15 | 4 | Widok osoby jak w prototypie (*„jest super”*); **„Rodzina” to docelowo mini-drzewo najbliższej rodziny** (rodzice, dzieci, partnerzy) z zakładki Drzewo, do tego czasu zaślepka | *„ta część rodzina możemy zrobić na razie jako placeholder bo tutaj bym wykorzystał funkcjonalność z »drzewo« gdzie widzielibyśmy najbliższą rodzinę danej osoby”* (2026-10-08) | [[osoba]] v1 D5, D6 | **tak** — widok osoby (M5, nowy ekran) → US w [[EPIC-002-wizyta]] |
| D16 | 4 | **Płeć wraca** (odwraca decyzję z ISSUE-019): nazwy pokrewieństwa po polsku — babcia, dziadek, stryj, wuj, siostra cioteczna — z płci i strony ścieżki do „ja” | *„W sumie faktycznie musi wrócić płeć - bo dzięki temu możemy powiedzieć babcia, dziadek, stryj, siostra cioteczna itd.”* (2026-10-08) | [[osoba]] v1 D4 · [[rodzina]] v1.3 · [[wpis-osoby]] v5.3 (4a wraca) | **tak** — pole płci w formularzu, kolumna płci w schemacie z migracją, słownik nazw pokrewieństwa → pozycja |
| D17 | 4 | **Zdjęcie w tle jak na Facebooku** zamiast gałązek; portret nachodzi na jego dolną krawędź; tło wybiera autor z bazy zdjęć osoby | *„Tutaj bym zrobił »tło zdjęcia« tak jak na facebooku”* (2026-10-08) | [[osoba]] v1 D3 · [[style-b]] v1.15 reguły 8, 14 | **tak** — wskazanie tła przy łączu osoba–zdjęcie (zmiana schematu) i „Ustaw jako tło” w podglądzie → razem z widokiem osoby |
| D18 | 4 | Widok osoby w wersji 2 (zdjęcie w tle, nazwy z płcią, **„Rodzina” jako mini-drzewo**: rodzice nad osobą, partnerzy obok, dzieci pod) | *„1 jest dobrze”* (2026-10-08) | [[osoba]] v1.1 element 6 | razem z widokiem osoby |
| D19 | 5 | Zakładka Osoby: „Ja” na górze, A–Z po nazwisku, pod imieniem pokrewieństwo; **ścieżka Osoby → osoba → Pochówek → mapa cmentarza z zaznaczoną pinezką** (bez pinezki — lista z zaznaczonym grobem) | *„tak jest dobrze, przy czym jeszcze chciałbym mieć ścieżkę (Osoby -> Wybrana osoba -> (w przypadku jeżeli zmarła) Miejsce pochówku -> I jestem kierowany na widok Cmentarza z zaznaczoną pinezką)”* (2026-10-08) | [[osoby]] v1 · [[osoba]] v1.1 element 9 | **tak** — zakładka Osoby (nowy ekran) i przejście pochówek → mapa → pozycja |
| D20 | 6 | Drzewo od osoby; **poziomy połączeń** (1: rodzice, partnerzy, dzieci; 2: do tego ich rodzina — rodzeństwo, rodzeństwo partnerów, dziadkowie…); **kolory linii** rodzic–dziecko i partnerzy; **czas**: osoba pojawia się przy narodzinach, para łączy się przy związku; **dwa tryby związku: „razem” i „małżeństwo”** | *„chciałbym mieć tutaj możliwość zwiększania »ilości połączeń«… chciałbym aby linie były odpowiednich kolorów… jeżeli ktoś się rodzi to dopiero ma się pojawić w tym drzewie, albo gdy jest ślub to się łączą (… dwa tryby połączenia (razem, małżeństwo - bo czasami ludzie nie są małżeństwem, mają dziecko, i dopiero biorą ślub)”* (2026-10-08) | [[drzewo]] v1 · [[rodzina]] v1.4 · [[style-b]] v1.16 (kolory relacji) | **tak** — widok drzewa (M9, M10) po [[SPIKE-002-tree-on-a-phone]]; data „razem od” przy rodzinie (zmiana schematu) → pozycja |
| D21 | 6 | „Połącz dwie osoby”: **animacja — linia biegnie od osoby do osoby** (ode mnie do żony, do jej mamy…), zdanie dopisuje się w tym rytmie | *„będzie się generowała taka animacja że odemnie leci linia do żony, potem do jej mamy, jej mamy, córki mamy, jej męża, jej syna”* (2026-10-08) | [[drzewo]] v1 (tryb „Połącz dwie osoby”) | **tak** — M11 → razem z drzewem |
| D22 | 7 | Wizyta: „gdzie jestem” na planie, „Postaw pinezkę” w grobie bez pinezki, „Popraw pinezkę” w arkuszu grobu, pinezka z GPS (źródło i dokładność), plan działa bez internetu, zdjęcie z góry nie | *„5. ok”* (2026-10-08) | [[cmentarz]] v4.2 · [[grob]] v5.1 · [[style-b]] v1.16 (niebieska kropka) | **tak** — M6, M7, uprawnienie lokalizacji → US [[EPIC-002-wizyta]]; pomiar GPS na miejscu czeka w *Parked* |
| D23 | 9 | Koło zębate → ustawienia (Ja, kopia, eksport, notka przekazania, „Stan danych”); **eksport domyślnie bez osób żyjących** | *„7. ok”* (2026-10-08) | [[ustawienia]] v1 | **tak** — ekran ustawień, wybór „ja”, eksport ([[US-006-eksport-dla-rodziny]]) → pozycje |

> **Panel 8 (fakt od babci) — runda 2.** Autor: *„a to nie wiem jak wejść i co opisujesz”*. Ukryte wejście (dotknięcie
> wiersza daty) nie zadziałało. W rundzie 2 jest widoczny przycisk „Dopisz, co mówi babcia” w widoku osoby i opis „po
> co” prostymi słowami.

| D# | Panel | Decyzja | Autor (cytat, data) | Specyfikacja (wersja) | Zmiana w kodzie → pozycja |
|---|---|---|---|---|---|
| D24 | 5 | Ścieżka Osoby → osoba → pochówek → mapa z zaznaczoną pinezką potwierdzona na prototypie | *„1 tak to jest to o co mi chodziło”* (2026-10-08) | [[osoba]] v1.1 element 9 · [[osoby]] v1 | razem z D19 |
| D25 | 6 | Poziomy, linie i czas — jak w rundzie 2. Do tego w produkcie: **przybliżanie i oddalanie drzewa** (jak mapa) i **pokazanie drzewa na telewizorze** na spotkaniu rodzinnym. **Bez legendy.** **Sterowanie poziomami do przeprojektowania** (estetyka). Bez trzeciego rodzaju linii | *„tak to jest dokładnie to przy czym w finalnym projekcie chciałbym aby można to było powiększać, pomniejszać (jak na mapie) oraz aby była możliwość połączenia się ze smart-TV… Legenda jest niepotrzebna, natomiast poziomy bym jakoś inaczej stworzył bo nie wygląda to moim zdaniem teraz estetycznie”* · *„3 linie są super”* · *„4 też działa dobrze i jest tak jak chciałem”* (2026-10-08) | [[drzewo]] v1.1 | **tak** — z drzewem (M9, M10); telewizor → decyzja przy pozycji ([[drzewo]] *Open*) |
| D26 | 6 | **„Połącz dwie osoby” na drzewie, nie osobny widok:** ikona bez podpisu → okno z dwoma kaflami (Od, Do) → lista osób; po wyborze drugiej osoby powrót do drzewa na poziomie, na którym ją widać; linia biegnie powoli ode mnie przez kolejne osoby; osoby ze ścieżki podświetlone, reszta wyszarzona; bez zdania i bez „Odtwórz jeszcze raz”; na chwilę baner z opisem pokrewieństwa („Siostra cioteczna babci mojej żony”) | *„… zaznaczając »połącz dwie osoby« (aczkolwiek zrobiłbym tylko tą ikonkę bez podpisu) pojawia mi się pop-up z dwoma kaflami … po wybraniu drugiej osoby od razu wracamy do widoku drzewa … powoli linie idą odemnie do kolejnych osób … tylko osoby w tych liniach są podświetlone a reszta jest wyszarzona. Nie ma podpisu, wyświetla się tylko na chwilę baner kim ta osoba dla mnie jest np. Siostra cioteczna babci mojej żony. Bez przycisku odtwórz jeszcze raz”* (2026-10-08; autor wpisał to jako punkt 5–6, odpowiedź na pytanie 5) | [[drzewo]] v1.1 elementy 7–10, D5, D6 | **tak** — M11 z drzewem; opisowe nazwy pokrewieństwa składane z odcinków |
| D27 | 8 | **Fakt od babci nie jest osobnym działaniem.** Babcia to jedna z osób, od których autor zbiera wiedzę; po rozmowie poprawia wpis osoby zwykłą edycją. Przycisk „Dopisz, co mówi babcia” i ekran źródeł faktu wycofane. **Źródła na ekranach i los [[US-004-fakt-od-babci]] / [[FR-001-provenance]] — pytanie do autora** (zmiana względem kick-offu, G3) | *„Nie, to źle Ci to wytłumaczyłem, Babcia to po prostu jedna z osób które dadzą mi wkład do tego co później wrzucę do notatek o danej osobie - nie ma potrzeby mieć tam źródła. Po rozmowie z babią normalnie wszedłbym na edycje danej osoby i dodał o niej informacje.”* (2026-10-08) | [[osoba]] v1.2 (element 8, D8 wycofane) | do ustalenia po odpowiedzi autora |

| D28 | 8 | **Bez źródeł w aplikacji** — ani na ekranach, ani w formularzu, ani w eksporcie. [[FR-001-provenance]] i [[US-004-fakt-od-babci]] wycofane (zmiana względem kick-offu, brief §5a G3); **schemat zostaje** (twierdzenia z v2 i v6 uśpione, formularz wpisuje domyślne źródło po cichu — bez migracji, odwracalne) | *„a to jakiś błąd się wkradł w takim razie - moje notatki to moje notatki, nie potrzeba żadnych potwierdzeń skąd pochodzą”* (2026-10-08) | [[osoba]] v1.3 D10 · [[wpis-osoby]] v5.4 (bez elementów 9–10) · [[ustawienia]] · [[US-006-eksport-dla-rodziny]] AC-1 · [[ADR-006-claimed-value-separate-structures]] *Follow-ups* · `DEFINITION_OF_DONE.md` · glossary · data-model · skill `qa` | **tak** — formularz bez linii źródła → [[ISSUE-025-gender-kinship-together-since]] |

> **Koniec rund prototypu (2026-10-08).** Autor: *„Jeżeli nie masz pytań to nie generowałbym nowych widoków - mam wrażenie
> że mamy dokładnie to czego potrzebowałem”*. Ostatnie pytanie (źródła) rozstrzygnął D28; pozycja zamknięta (`docs`).

## Verification
> Self-check przy zamknięciu (`docs` + `qa`, 2026-10-08). Werdykt: **APPROVED (self-check)** — granica jak zawsze: dziennik
> pisany przez agenta zapisuje to, co agent zrozumiał (D27 pokazał, że raz zrozumiał źle — złapał to autor).

- **Każda decyzja ma specyfikację:** D1–D28 → [[style-b]] v1.16 · [[references]] · [[cmentarze]] v2.4 · [[cmentarz]] v4.2 ·
  [[grob]] v5.1 · [[osoba]] v1.3 · [[osoby]] v1 · [[drzewo]] v1.1 · [[ustawienia]] v1 · [[rodzina]] v1.4 · [[wpis-osoby]]
  v5.4. Nowe specyfikacje: osoba, osoby, drzewo, ustawienia (folder `05_DESIGN/` istnieje — bez nowego wiersza DOC_MAP).
- **Każda zmiana w kodzie ma pozycję:** [[ISSUE-022-app-skeleton-tabs-people-settings]] (D1–D3, D19, D23) ·
  [[ISSUE-023-poland-map-r1-cemetery-photo]] (D5–D7) · [[ISSUE-024-person-view]] (D4, D13–D18, D24, D27) ·
  [[ISSUE-025-gender-kinship-together-since]] (D16, D20, D28) · [[US-007-mapa-cmentarza]] (D8–D12) ·
  [[US-008-pinezka-na-miejscu]] (D22) · drzewo (D20, D21, D25, D26) → [[SPIKE-002-tree-on-a-phone]] → *Input from
  SPIKE-004*, potem US w [[EPIC-003-zrozumienie]] · eksport (D23) → [[US-006-eksport-dla-rodziny]].
- **Zmiany zakresu nazwane:** zdjęcie cmentarza (D5), bez linku do Grobonetu (D10), wyszukiwanie osób do MVP (D19), płeć
  wraca (D16), drzewo na telewizorze (D25, do decyzji przy pozycji), bez źródeł (D28).
- **Zero danych rodziny:** prototyp i specyfikacje używają wyłącznie wymyślonych osób i miejsc (Wymyślonów, Testowo,
  Przykładowo, Zmyślin). Nazwa miejscowości z obrazu R1, którą autor wkleił do rozmowy, nie trafiła do żadnego pliku.
  Strażnik treści sprawdzi zmiany przy `git add`.
- **Prototyp poza repo:** `%TEMP%\claude\c--Programowanie-Grobing-grobing-agents\e2987d63-950d-4e55-b9fb-24429bf1ed09\scratchpad\grobing-prototyp.html` (ok. 320 KB, jeden plik HTML) — do wyrzucenia; prawdą są specyfikacje.
- **Time-box:** 1 sesja (zakładane 2).
- **Czego prototyp nie dał:** tempa wpisywania, pikseli i gestów Fluttera, czytelności drzewa ok. 100 osób (SPIKE-002),
  słońca, GPS i offline na cmentarzu (wyjątki telefonu w DoD).
