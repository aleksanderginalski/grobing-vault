---
screen: "Rodzina — arkusz rodziny (A) i wybór osoby (B)"
items: ["[[ISSUE-019-family-relations]]", "[[ISSUE-025-gender-kinship-together-since]]"]
us: "[[US-003-przepisanie-rodziny]]"
journey-step: "n/a — M1 (warunek kroku 1 UJ-001)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-rodzina.html (ramki 3–6; ramki 1–2 to sekcja „Rodzina” w [[wpis-osoby]]) · 2026-10-08: issue-025-prototyp.html (v2 — kreator, karta partnera, warianty C i P; ścieżka w ISSUE-025)"
updated: 2026-10-08
---

# Rodzina — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]].
>
> **Wersja 1 (2026-10-07, przed planem [[ISSUE-019-family-relations]]).** Kanon: brief → *Domain canon (Step 0)* —
> jednostką wpisywania jest *family group sheet* (para i jej dzieci), co jest też odpowiedzią na G6, i
> [[FR-002-rodzina-jako-rekord]] („całymi rodzinami, nie osoba po osobie”). Referencja: R4 prawy pokazuje
> rodzinę **przy osobie** (sekcja „Rodzina” z chipami, [[references]]). Arkusza nie ma w R1–R4, więc dziedziczy
> reguły stylu B i formę pól z [[wpis-osoby]]. Gdzie relacje widać przy osobie: [[wpis-osoby]] v5, element 9a.
> **Trzy rozwidlenia dla autora na stopie #1** są w *Open*. Specyfikacja jest napisana według rekomendacji.
>
> **Wersja 1.1 (2026-10-07, stop #1 [[ISSUE-019-family-relations]] — decyzje autora):**
> - **O1 „ok”** (arkusz do wpisywania, widok przy osobie). Uwaga autora: *„może być tak, że ktoś był z kimś w danym
>   okresie, a następnie się rozstali lub owdowieli i mieli nowe związki i dzieci”*. Model to obsługuje: każdy związek to
>   osobna rodzina z własnymi dziećmi, datą ślubu i datą końca (AC-2, AC-3). Zmieniają się słowa: **„związek”** zamiast
>   „małżeństwo” (nie każdy związek był małżeństwem). Linia przy końcu mówi o rozstaniu i owdowieniu (A6);
> - **O2 i płeć w schemacie — „nie czuję potrzeby”:** **bez płci.** Nazwy relacji są neutralne (*Role names*), a z
>   arkusza znika kolumna roli, bo sekcje „Para” i „Dzieci” mówią to samo;
> - **O3 — „na ten moment raczej nie trzeba”:** bez rodzeństwa przy osobie; pokażą je wizualizacje połączeń (EPIC-003);
> - **kolejność dzieci według daty urodzenia** (kanon GEDCOM 7: *„chronological by birth”*) zastępuje D10;
> - D1–D8 i D11 przyjęte („ok”), w tym „Usuń rodzinę” (D8).
>
> **Wersja 1.2 (2026-10-07, przegląd `ui` zbudowanego ekranu, ISSUE-019 → *Verification*):** błąd daty przewija cały
> blok z linią komunikatu nad „Zapisz” (*States* → „A — błąd”; blok wspólny z [[wpis-osoby]]); 24 dp przed „Dzieci”;
> „Dodaj koniec związku” i „Usuń rodzinę” na krawędzi treści (16 dp); „Nowa osoba” ma rolę przycisku dla czytnika; D7 ze
> słowami v1.1.
>
> **Wersja 1.3 — płeć wraca ([[SPIKE-004-mvp-flow-prototype]] D16, 2026-10-08):** warunek obalenia D9' się spełnił —
> ścieżka do „ja” w widoku osoby ([[osoba]] D4) potrzebuje nazw z płcią. Autor: *„W sumie faktycznie musi wrócić płeć -
> bo dzięki temu możemy powiedzieć babcia, dziadek, stryj, siostra cioteczna itd.”*. Chipy i wiersze dostają nazwy z
> płci: Ojciec/Matka, Mąż/Żona (bez ślubu: Partner/Partnerka), Syn/Córka; osoba bez wpisanej płci — nazwy neutralne
> jak w v1.1. Kolumna roli w arkuszu dalej niepotrzebna (sekcje „Para” i „Dzieci”). Szczegóły → pozycja, która zbuduje
> pole płci ([[wpis-osoby]] 4a).
>
> **Wersja 1.4 — dwa tryby związku ([[SPIKE-004-mvp-flow-prototype]] D20, 2026-10-08):** związek ma **dwie daty: „Razem od”
> (początek związku) i „Ślub”**, a do tego jak dotąd koniec związku. Autor: *„zrobiłbym dwa tryby połączenia (razem,
> małżeństwo - bo czasami ludzie nie są małżeństwem, mają dziecko, i dopiero biorą ślub)”*. Rozstrzyga to temat z
> `CURRENT_STATE.md` („data początku związku bez ślubu”, przegląd US-003 uwaga 4) wariantem **osobnego pola „Razem
> od”**, nie innego podpisu „Ślubu”. Związek bez ślubu ma samo „Razem od”; nazwy w chipach: Partner/Partnerka (bez ślubu)
> albo Mąż/Żona (po ślubie). W drzewie: linia przerywana od „Razem od”, ciągła od ślubu ([[drzewo]] D4). Zdarzenie
> początku związku to nowe zdarzenie rodziny z twierdzeniem (jak ślub, [[ADR-011-relation-claims-family-and-child-link]]) —
> szczegóły i ewentualna migracja → pozycja, która zbuduje pole.
>
> **Wersja 1.5 (2026-10-08, przed planem [[ISSUE-025-gender-kinship-together-since]]):** v1.3 i v1.4 rozpisane na elementy.
> Trzy luki, które wyszły przy rozpisaniu:
> - **płeć osoby nowej w arkuszu** (A3'): osoby z arkusza (rodzice, dzieci bez grobu) to duża część osób, a bez płci rodzica
>   nie da się odróżnić stryja od wuja. Wiersz A3' dostaje segment płci podpowiadany z imienia — tak jak w P1 z v1
>   (*Open* 2: „podpowiedziane z imienia przy nowej osobie i w wierszu A3'”) i w [[wpis-osoby]] 4a (D14);
> - **małżeństwo bez daty ślubu**: w v1.4 o „Mąż/Żona” decydowała data ślubu, a notatki często mówią „żona Jana” bez
>   daty. **Rekomendacja: segment „Małżeństwo · Razem”** (A5, dosłownie „dwa tryby” autora z D20), a daty pod nim
>   opcjonalne (D12) → *Open* 4 na stopie #1;
> - **A10 (źródło) znika** — SPIKE-004 D28 („bez źródeł w aplikacji”) dotyczy też arkusza; schemat dostaje domyślne
>   źródło po cichu, jak w [[wpis-osoby]] v5.4.
>
> *Role names* z płci i rodzaju związku (tabela niżej); po końcu związku nazwy się nie zmieniają (D13).
>
> **Wersja 2 (2026-10-08, stop #1 ISSUE-025, runda 1 — uwagi autora) — związek jako oś czasu, kreator zamiast arkusza.**
> Autor: *„związek może »ewoluować« w małżeństwo […] Podczas tworzenia chciałbym wybrać daną osobę i dobrać jej parę i na
> »pop-upie« zostać zapytany o szczegóły (pojedynczo, najpierw do wyboru osoba, potem czy razem/małżeństwo, potem opcja
> zakończenia lub »ewolucji« relacji z razem na małżeństwo/koniec związku itd.) Po dodaniu miałbym widok tylko informacje
> o partnerze z datami i opcje edycji tego partnera oraz możliwość dodania kolejnego.”*
> - **C — kreator związku** w arkuszu od dołu, jedno pytanie na krok: z kim → razem czy małżeństwo (z datą) → co było
>   dalej (ślub · koniec · nic więcej). Ten sam kreator dodaje rodziców (P1 — wybór autora, runda 2);
> - **D — podsumowanie związku** (✎ na karcie): każdy wiersz osi czasu zmienia się osobno, bez przechodzenia kreatora;
> - **E — dodaj dziecko** z karty związku (C1 — wybór autora, runda 2);
> - **A (pełny arkusz pary i dzieci) zastąpiony** przez C–E; **B (wybór osoby) zostaje** jako krok „z kim” kreatora;
> - v1.5 rozpisane na nowo: segment A5 i D12 obalone (*Open* 4 rozstrzygnięte trzecim kształtem), płeć nowej osoby
>   ikonami ♀ ♂ ([[wpis-osoby]] 4a v5.6), *Role names* bez zmian, A10 dalej usunięte.
>
> Karta i sekcja w formularzu: [[wpis-osoby]] 9a v5.6. Prototyp: `issue-025-prototyp.html` (katalog tymczasowy sesji).
>
> **Wersja 2.1 (2026-10-08, przegląd `ui` zbudowanego ekranu i stop #2 ISSUE-025):**
> - **arkusz zawsze tej samej wysokości** (ok. 92% ekranu), bez uchwytu i przeciągania; klawiatura zmniejsza treść, a nie
>   przesuwa arkusza, a przyciski kroku stoją nad nią. Autor na stopie #2: *„chciałbym aby ten pop-up był mniej więcej w tym
>   samym miejscu - aby po otwarciu się klawiatury ten pop-up nie przesuwał się stale góra-dół”* (C0);
> - „←” także na pierwszym kroku (zamyka); tytuł „Kolejny partner”, gdy osoba ma już związek;
> - C1 „Z kim w związku?”; „Nie znam daty” w **kolorze tekstu** (reguła 1 — akcent tylko dla „Dalej”); po wejściu w krok daty
>   kursor w polu, a klawisz „gotowe” robi przycisk kroku; błąd kolejności barwi ramkę pola;
> - C-r1 „Nie wiem — przejdź do taty”, a wtedy wybór taty zapisuje od razu („krok 2 z 2”, jak C-r2); C3b „Nie znam daty” =
>   koniec bez daty; karty-opcje nieaktywne w trakcie zapisu; ikony: Razem `favorite_border`, Małżeństwo i „Wzięli ślub”
>   `diamond_outlined`, koniec `call_split_outlined`, zapis `check`, „Nie wiem” `help_outline`;
> - D: „Rodzic” przy nieznanej płci, „Dzieci” przy związku rodziców, „Usuń” zamiast „Nie znam daty” przy „Razem od”, stopka
>   zawija się przy dużym tekście; E: „Dziecko tej pary”, para pod pytaniem (bez odmiany imion — [[grob]] D1).
> Dane bez zmian wobec planu ISSUE-025 (zdarzenia `together`, `marriage` — także bez daty — i `end`, `persons.sex`).

## Purpose
Wpisanie jednej rodziny naraz — pary i jej dzieci — tak, jak stoi w notatkach, oraz poprawa rodziny. Wybór osoby
**najpierw szuka**, więc osoba już wpisana (np. przy grobie) nie powstaje drugi raz (US-003 AC-5).

## Navigation
- Z [[wpis-osoby]] w trybie „poprawa”, sekcja „Rodzina” (element 9a):
  - „Dodaj związek” (v1.1; było „Dodaj małżeństwo”) → A **„nowa rodzina”**, w parze ta osoba;
  - „Dodaj rodziców” → A **„nowa rodzina”**, w dzieciach ta osoba;
  - ✎ przy grupie (rodzice albo związek) → A **„poprawa”** tej rodziny.
- A → „Dodaj osobę do pary” albo „Dodaj dziecko” → B. **Dotknięcie osoby w B wraca do A** z tą osobą dodaną, a
  „Nowa osoba” wraca z nowym wierszem do wpisania. Wstecz z B → A bez zmian.
- **„Zapisz” w A → [[wpis-osoby]]**, który odświeża sekcję „Rodzina”. Rodzina zapisuje się od razu, własną
  transakcją, niezależnie od „Zapisz” formularza osoby (D1).
- Wstecz z A ze zmianami → okno „Odrzucić zmiany w rodzinie?”. Bez zmian → od razu.
- Osoba z arkusza ma swój wpis ([[wpis-osoby]], poprawa) dostępny przez chip w sekcji „Rodzina” każdego krewnego,
  także wtedy, gdy nie ma grobu. Wiersze arkusza nie prowadzą do wpisu (D11).

## Elements in order

### A — arkusz rodziny (pełny ekran) — **zastąpiony w v2 przez C–E**
Tabela zostaje jako zapis tego, co zbudowało ISSUE-019, aż ISSUE-025 usunie ekran. Reguły, które przechodzą dalej: skład
rodziny (1–2 osoby w parze, nikt dwa razy, dziecko w jednej rodzinie rodziców — D5, D6), podpowiedź nazwiska (A3'), linia
przy końcu związku (A6, D7), „Usuń rodzinę” z oknem (A11, D8 → D „Usuń związek”).

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| A1 | **Pasek:** wstecz; tytuł „Nowa rodzina”, w poprawie „Rodzina” (półgruby); podtytuł (14 sp, tekst pomocniczy, jedna linia, ucięty): imiona i nazwisko osoby, z której otwarto arkusz | pasek | wstecz → okno albo [[wpis-osoby]] | — | — | decyzja projektowa |
| A2 | Nagłówek **„Para”** (14 sp, półgruby, tekst pomocniczy — jak D4 w [[zdjecie]]) | tekst | — | — | — | AC-1 · FR-002 |
| A3 | **Wiersz osoby** (ten sam kształt w parze i w dzieciach), ≥ 56 dp. Imiona i nazwisko z „z d.” (16 sp, tekst, zawijane), pod nimi lata (14 sp, tekst pomocniczy, format jak w [[grob]]), a przy osobie, z której otwarto arkusz, „· ta osoba”. Z prawej `close` (tekst pomocniczy, cel 48 dp, `tooltip` „Usuń z rodziny”) — **oprócz „tej osoby”**. **Bez kolumny roli** (v1.1: bez płci rola powtarzałaby nagłówek sekcji) | wiersz | `close` usuwa osobę **z rodziny**, nie z aplikacji | — | — | AC-1 · AC-2 |
| A3' | **Wiersz nowej osoby** (z „Nowa osoba” w B): pola **„Imiona”** i pod nim **„Nazwisko”** (ramka w kolorze obrysu, 16 sp, wielka litera na początku słów); `close` usuwa wiersz | dwa pola tekstowe | **fokus i klawiatura od razu w „Imiona”**, kursor na końcu; „Imiona” `next` → „Nazwisko” `done` | imiona: tekst wpisany w B; nazwisko: **podpowiedziane i zaznaczone** — dziecko i druga osoba z pary dostają nazwisko pierwszej osoby z pary, a przy „Dodaj rodziców” nazwisko dziecka. Przy parach -ski/-ska zaznaczenie wymaga przepisania nazwiska, jak w [[wpis-osoby]] (*Open* → „Do odczucia”) | imiona albo nazwisko: „Podaj imiona albo nazwisko.” | AC-1 · [[wpis-osoby]] element 3 (podpowiedź) · D4 |
| A3'a | **Płeć nowej osoby** (v1.5) — pod polem „Nazwisko” w wierszu A3', ten sam przycisk segmentowy co [[wpis-osoby]] 4a („Kobieta” · „Mężczyzna”, 48 dp, pusty dozwolony, ✓ i napis w akcencie przy wybranym), bez etykiety „Płeć” — dla czytnika „Płeć, Kobieta, zaznaczone” | przycisk segmentowy | dotknięcie; **poza `next`** — „Nazwisko” `done` dalej zamyka klawiaturę | podpowiedź z pierwszego imienia na bieżąco przy pisaniu „Imiona”, dopóki autor nie dotknie segmentu (reguła: [[wpis-osoby]] *D-płeć*); bez imion — nic | — | ISSUE-025 · *Open* 2 P1 (v1) · D14 |
| A4 | **„Dodaj osobę do pary”** — przycisk z obrysem, `person_add_alt_outlined` w akcencie, napis w kolorze tekstu, ≥ 52 dp, szerokość treści, z lewej. Tylko gdy w parze jest mniej niż dwie osoby | przycisk | → B w trybie „para” | — | najwyżej dwie osoby w parze: przy dwóch przycisku nie ma | AC-1 · FR-002 (1–2 partnerów) |
| A5 | **Rodzaj związku** (v1.5, rekomendacja — *Open* 4) — etykieta „Związek” (14 sp, tekst pomocniczy), pod nią przycisk segmentowy jak [[wpis-osoby]] 4a: **„Małżeństwo” · „Razem”**, bez pustego wyboru. Pod segmentem, gdy wybrane „Razem”, a pole „Ślub” ma datę: „Data ślubu nie zapisze się w związku bez ślubu.” (13 sp, tekst pomocniczy) — przełączenie z powrotem ją przywraca | przycisk segmentowy | dotknięcie; poza `next` | **nowa rodzina: „Małżeństwo”** (w notatkach rodziny przeważają małżeństwa); poprawa: „Małżeństwo”, gdy rodzina ma ślub (także bez daty), inaczej „Razem” — więc rodziny sprzed migracji bez daty ślubu pokazują „Razem”, czyli ten sam chip „Partner” co dziś | — | SPIKE-004 D20 („dwa tryby połączenia”) · ISSUE-025 AC-3 · D12 |
| A5' | **„Razem od”** (v1.5) — blok daty z [[wpis-osoby]], etykieta „Razem od”. Przy „Razem” widoczny od razu. Przy „Małżeństwo” schowany za przyciskiem tekstowym **„Dodaj „Razem od””** (akcent, w linii treści, jak A6), z linią pod etykietą „np. gdy byli razem przed ślubem.” (13 sp, tekst pomocniczy); w poprawie z datą widoczny od razu | blok daty / przycisk → blok daty | po odsłonięciu fokus w polu daty; `next` z daty do daty | „dokładnie”, pusto | jak blok daty; przy obu datach „Razem od” nie później niż ślub: „Ślub nie może być przed „Razem od”.” | ISSUE-025 AC-3 · [[rodzina]] v1.4 · D12 |
| A5'' | **„Ślub”** — blok daty z [[wpis-osoby]] (b dopisek · c data · d „do” przy „między” · e podgląd), etykieta „Ślub”. **Tylko przy „Małżeństwo”** (v1.5). Pusta data przy „Małżeństwo” = ślub był, daty nie znamy (D12) | blok daty | dotknięcie pola; `next` z daty do daty | „dokładnie”, pusto | jak blok daty | AC-3 · [[FR-004-data-z-dopiskiem]] |
| A6 | **„Dodaj koniec związku”** — przycisk tekstowy w linii treści (akcent). Odsłania **A6'**: blok daty „Koniec związku” z linią pod etykietą „np. rozwód albo rozstanie. Owdowienie to zgon osoby — zapisuje się w jej wpisie.” (13 sp, tekst pomocniczy; v1.1 — uwaga autora o rozstaniu i owdowieniu). W poprawie rodziny z datą końca A6' widać od razu, bez przycisku | przycisk → blok daty | po odsłonięciu fokus w polu daty | schowany | jak blok daty | AC-3 · D7 |
| A7 | Nagłówek **„Dzieci”** (jak A2) | tekst | — | — | — | AC-1 |
| A8 | **Wiersze dzieci** (A3 / A3'). Przy otwarciu arkusza **według daty urodzenia** (pierwsza wartość), a bez daty na końcu, w kolejności zapisu (v1.1, kanon GEDCOM 7). Wiersz dodany w trakcie edycji zostaje tam, gdzie go dodano | wiersze | jak A3 | — | — | AC-1 · AC-2 |
| A9 | **„Dodaj dziecko”** — jak A4, zawsze | przycisk | → B w trybie „dziecko” | — | — | AC-1 |
| ~~A10~~ | ~~**Źródło** — „Rodzina i jej daty zapiszą się ze źródłem: notatki.”~~ — **usunięte w v1.5** (SPIKE-004 D28, jak [[wpis-osoby]] element 10). Zapis dalej dostaje źródło „notatki” i status `CLAIMED`, po cichu | — | — | — | — | — |
| A11 | **„Usuń rodzinę”** — tylko w poprawie: przycisk tekstowy z `delete_outline`, w kolorze tekstu ([[style-b]] reguła 14, usuwanie bez koloru błędu) | przycisk | → okno „Usunąć rodzinę?” | — | — | **decyzja projektowa spoza AC** (D8) |
| A12 | **Zapisz** — przycisk wypełniony, przypięty na dole nad klawiaturą, ≥ 52 dp | przycisk | dotknięcie | — | rodzina ma osobę w parze i co najmniej dwie osoby. Bez pary: „Dodaj osobę do pary — rodzina to para i jej dzieci.” Z jedną osobą: „Dodaj drugą osobę do pary albo dziecko.” Komunikat nad „Zapisz” z `error_outline` w kolorze błędu. Do tego błędy pól jak w [[wpis-osoby]] | AC-1…AC-4 |

**Zapis jest całością** (ISSUE-019 AC): nowe osoby (v1.5: z płcią z A3'a), przynależność do pary i dzieci (każda z
twierdzeniem), daty „Razem od”, ślubu i końca (z twierdzeniami) oraz rodzaj związku zapisują się razem albo wcale. Usunięcie osoby z rodziny usuwa jej przynależność
razem z twierdzeniem. Osoba zostaje.

#### Role names
Rola mówi, kim **osoba z chipu** ([[wpis-osoby]] 9a) jest dla osoby, której wpis oglądamy. **v1.5: z płci osoby z chipu
i z rodzaju związku** (v1.3, v1.4; SPIKE-004 D16, D20). Osoba bez płci — nazwa neutralna jak w v1.1:

| Relacja | Kobieta | Mężczyzna | Płeć nieznana |
|---|---|---|---|
| rodzic | Matka | Ojciec | Rodzic |
| druga osoba ze związku — „Małżeństwo” | Żona | Mąż | Małżonek |
| druga osoba ze związku — „Razem” | Partnerka | Partner | Partner |
| dziecko | Córka | Syn | Dziecko |

Formy pełne („Matka”, nie „Mama”), bo chip mówi o relacji między dwiema osobami z notatek, a nie o autorze. Nazwy wobec
autora („mama”, „babcia”, „stryj”) są w [[osoby]] element 4 i w [[osoba]] element 7. Po końcu związku nazwa się nie
zmienia (D13). Arkusz ról nie pokazuje: mówią je nagłówki „Para” i „Dzieci”. Nazwy z v1.1 zostają dla osób bez płci.

### B — wybór osoby (pełny ekran)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| B1 | **Pasek:** wstecz → A bez zmian; tytuł „Dodaj do pary” albo „Dodaj dziecko” (półgruby) | pasek | — | — | — | decyzja projektowa |
| B2 | **Pole „Szukaj osoby albo wpisz nową”** — ramka w kolorze obrysu, ikona `search` (tekst pomocniczy); filtruje B4 i B5 bez polskich znaków i końcówek (`matchesQuery`, jak D3 w [[zdjecie]]) | pole tekstowe | **fokus i klawiatura od wejścia** (inaczej niż D3); `done` chowa klawiaturę | pusto | — | AC-5 · D3 |
| B3 | **„Nowa osoba”** — pierwszy wiersz pod polem, zawsze widoczny: `person_add_alt_outlined` (akcent) i „Nowa osoba” (16 sp, tekst), a przy wpisanym tekście „Nowa osoba: „Anna””. ≥ 56 dp | wiersz-przycisk | → A z wierszem A3', imiona = tekst z B2 | — | — | AC-1 · D3 |
| B4 | **Sekcja „W tym grobie”** (nagłówek jak A2) — osoby z grobu osoby, z której otwarto arkusz (jej pierwszy pochówek, [[ADR-006-claimed-value-separate-structures]] D3), w kolejności wpisania. Osoba bez grobu — sekcji nie ma. **Wiersz:** imiona i nazwisko z „z d.” (16 sp, tekst), lata (14 sp, tekst pomocniczy), ≥ 56 dp, cały wiersz to jeden cel | lista | dotknięcie → A z tą osobą | — | — | AC-5 |
| B5 | **Sekcja „Inne osoby”** — pozostałe osoby, alfabetycznie po nazwisku, potem imionach (`polishCompare`). Druga linia: lata · nazwa grobu, a bez niej nazwa cmentarza (jedna linia, ucięta), jak D5 w [[zdjecie]]; osoba bez grobu — same lata, a bez lat „bez dat” | lista | jak B4 | — | — | AC-5 · AC-2 (osoba z innej rodziny jako druga para) |

**Wiersze nieaktywne** (B4, B5): tekst w kolorze pomocniczym, bez dotknięcia, dla czytnika „niedostępne”, a zamiast
lat **powód tekstem** (nie samym kolorem, SC 1.4.1):
- „już w tej rodzinie” — osoba jest już w A (także „ta osoba”);
- „ma już rodziców” — tylko w trybie „dziecko”, gdy osoba jest dzieckiem w innej rodzinie (D5).

**Pusty wynik filtra:** pod B3 „Nie ma osoby pasującej do „…”.” (14 sp, tekst pomocniczy). B3 zostaje, więc z
pustego wyniku jest jedno działanie ([[style-b]] reguła 9).

**Dane, których potrzebuje B** (dla `planning`):
- wszystkie osoby: imiona, nazwisko, nazwisko rodowe, lata;
- grób albo cmentarz pierwszego pochówku każdej osoby;
- kto jest dzieckiem w jakiejś rodzinie (w trybie „dziecko”);
- niezapisany skład A — wyklucza osoby, które już w nim są.

### C — kreator związku (arkusz od dołu, v2)
Arkusz modalny na powierzchni, **zawsze tej samej wysokości (ok. 92% ekranu)**, bez uchwytu i przeciągania (v2.1):
nagłówek u góry, treść kroku przewijana pod nim, przyciski kroku przypięte na dole — klawiatura zmniejsza treść, a arkusz
stoi w miejscu. **Jedno pytanie na krok.** Nad pytaniem rośnie **oś czasu** tego związku („Maria i Jan · razem od 1946”).
Tryby: **„partner”** (z „Dodaj partnera” / „Dodaj kolejnego partnera”, 3 kroki) i **„rodzice”** (z „Dodaj rodziców”, P1,
4 kroki). Zapis następuje na ostatnim kroku, jedną transakcją: rodzina, para, zdarzenia, twierdzenia (po cichu —
„notatki”, `CLAIMED`).

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| C0 | **Nagłówek arkusza:** ← (krok wstecz; na pierwszym kroku zamyka — v2.1), „Dodaj partnera · krok 1 z 3” albo „Kolejny partner · …”, gdy osoba ma już związek (13 sp, tekst pomocniczy), ✕ (zamknij). Zamknięcie po pierwszym kroku → okno „Przerwać dodawanie?” · „Wróć” (akcent) · „Przerwij”; nic się nie zapisuje | nagłówek | ← · ✕ | — | — | decyzja projektowa |
| C1 | **„Z kim w związku?”** (v2.1) — pytanie (20 sp, półgruby), pod nim imię i nazwisko osoby z wpisu; treść = wybór osoby **B2–B5** (szukaj, „Nowa osoba”, „W tym grobie”, „Inne osoby”; wiersze nieaktywne z powodem, np. „już partner tej osoby”) | wybór osoby | dotknięcie osoby → C2; „Nowa osoba” → C1' | — | jak B | AC-1 · AC-5 (najpierw szukaj, D3) · autor (v2) |
| C1' | **Nowa osoba:** „Imiona” z ♀ ♂ po prawej ([[wpis-osoby]] 4a v5.6, podpowiedź z imienia), „Nazwisko” podpowiedziane i zaznaczone (nazwisko osoby z wpisu, jak A3'), „Dalej” (wypełniony) | pola + ikony | fokus w „Imiona”; „Imiona” `next` → „Nazwisko” `done`; „Dalej” → C2 | imiona: tekst z B2 | imiona albo nazwisko | A3' · D14 |
| C2 | **„Jaki to był związek?”** — dwie karty-opcje (≥ 56 dp, obrys 1 dp; wybrana obrys 2 dp w akcencie): **„Razem”** („bez ślubu — ślub możesz dodać w następnym kroku”) · **„Małżeństwo”** („od ślubu”). Po wyborze pod nimi **blok daty** z [[wpis-osoby]]: „Razem od” albo „Ślub”, i przyciski **„Nie znam daty”** (tekstowy, **kolor tekstu** — v2.1) · **„Dalej”** (wypełniony) | opcje + blok daty | wybór → fokus w polu daty; „Dalej” → C3 | nic nie wybrane | blok daty | autor (v2) · SPIKE-004 D20 · GEDCOM `MARR Y` (ślub bez daty) |
| C3 | **„Co było dalej?”** — opcje-karty: **„Wzięli ślub”** (tylko gdy związek nie jest jeszcze małżeństwem) → C3a · **„Związek się zakończył”** (tylko bez końca) → C3b · **„Nic więcej — zapisz”** → zapis, arkusz się zamyka, w 9a pojawia się karta. Krok wraca po C3a, aż autor wybierze koniec albo zapis | opcje | dotknięcie | — | — | autor („ewolucja” związku) |
| C3a | **„Kiedy był ślub?”** — blok daty „Ślub”, „Nie znam daty” · „Dalej” → C3 | blok daty | kursor w dacie po wejściu; `done` = „Dalej” (v2.1) | „dokładnie”, pusto | jak blok daty; ślub nie przed „Razem od”: „Ślub nie może być przed „Razem od”.” | AC-3 |
| C3b | **„Kiedy związek się zakończył?”** — blok daty „Koniec związku” z linią D7 („np. rozwód albo rozstanie. Owdowienie to zgon osoby — zapisuje się w jej wpisie.”), „Nie znam daty” (koniec bez daty — v2.1) · **„Zapisz”** | blok daty | kursor w dacie; `done` = „Zapisz” → zapis | — | koniec nie przed początkiem | A6 · D7 |
| C-r1 | **Tryb „rodzice” (P1), krok 1: „Kto jest mamą?”** — opcja-karta **„Nie wiem”** („przejdź do taty” — v2.1) nad wyborem jak C1; nowa osoba dostaje płeć „kobieta” bez pytania (ikony pokazane jako wybrane, do zmiany) | wybór osoby | → C-r2; po „Nie wiem” wybór taty zapisuje od razu (bez pary nie ma związku do opisania; „krok 2 z 2”) | — | osoba z rodzicami nieaktywna, gdy to „ta osoba” (cykl) | D14 · P1 |
| C-r2 | **„Kto jest tatą?”** — opcja-karta **„Nie wiem”** („dodasz go później przez ✎”) nad wyborem jak C1; nowa osoba — „mężczyzna” | wybór osoby | osoba → C2 (dla pary rodziców), potem C3; **„Nie wiem” → zapis od razu** (bez pary nie ma związku do opisania; „krok 2 z 2”) | — | — | P1 · D6 (rodzina z jedną osobą w parze i dzieckiem) |

### D — podsumowanie związku (✎ na karcie albo przy „Rodzice”, v2)
Arkusz od dołu: tytuł „Maria i Jan” (20 sp, półgruby). **Wiersze ≥ 56 dp** z linią podziału: etykieta (96 dp, tekst
pomocniczy) · wartość · chevron — **Partner** (albo **Mama**, **Tata**) · **Razem od** · **Ślub** · **Koniec**. Pusty
wiersz ma w wartości „Dodaj” (akcent). Dotknięcie wiersza otwiera **jeden krok** kreatora (C1, blok daty z C2, C3a, C3b) z
obecną wartością; „Dalej”/„Zapisz” w tym kroku zapisuje zmianę i wraca do D. W kroku „Ślub” jest dodatkowo przycisk
tekstowy **„To nie było małżeństwo”** (usuwa ślub; związek wraca do „Razem”). Przy wariancie C1 niżej **„Dzieci z tego
związku”** — wiersze z `close` („Usuń z tej rodziny”, `tooltip`). Na dole: **„Usuń związek”** (tekstowy, `delete_outline`,
kolor tekstu — reguła 14) → okno jak A11 („Osoby zostają w aplikacji. Znikną tylko ich powiązania w tej rodzinie i daty
związku.” · **„Zostaw”** · „Usuń”) i **„Gotowe”** (wypełniony, zamyka).

### E — dodaj dziecko (z karty związku, C1, v2)
Arkusz od dołu, jeden krok: „Dziecko Marii i Jana” (20 sp) i wybór osoby B w trybie „dziecko” (nieaktywne „ma już
rodziców”); „Nowa osoba” → pola jak C1' z **„Dodaj”** zamiast „Dalej”. Nazwisko podpowiedziane jak dziś (pierwsza osoba z
pary). Zapis od razu, z twierdzeniem przy łączu dziecka ([[ADR-011-relation-claims-family-and-child-link]]). **Wariant C2**
(osobna sekcja „Dzieci”): przed wyborem dodatkowy krok **„Z kim <osoba> ma to dziecko?”** — karty partnerów i „Nie
wiadomo”; przy jednym partnerze krok też jest, bo dziecko mogło być spoza związku.

## States
| Stan | Co widać |
|---|---|
| A — nowa, „Dodaj związek” | w parze „ta osoba” (bez `close`) i A4; A5 „Małżeństwo”, A5' schowany za „Dodaj „Razem od””, A5'' pusty; A6 schowany; „Dzieci” bez wierszy, tylko A9. Bez fokusu i bez klawiatury |
| A — nowa, „Dodaj rodziców” | „Para” bez wierszy, tylko A4; w „Dzieci” „ta osoba” i A9 |
| A — poprawa | wiersze z bazy; A5 według zapisanego ślubu (v1.5); A5', A5'' i A6' z datami, gdy są; A11 widoczny |
| A — „Razem” (v1.5) | A5 „Razem”, A5' widoczny, A5'' schowany; przy wpisanej wcześniej dacie ślubu linia „Data ślubu nie zapisze się…” |
| A — nowa osoba dopisana | wiersz A3' z fokusem w „Imiona”, klawiatura otwarta, nazwisko podpowiedziane; A3'a z płcią podpowiedzianą z imienia z B2 (v1.5) |
| A — błąd | komunikaty pól jak w [[wpis-osoby]] (`error_outline`, kolor błędu, ramka); komunikat składu nad „Zapisz”; fokus i przewinięcie do pierwszego błędu; nic się nie zapisuje |
| A — zapisywanie | „Zapisz” nieaktywny przez chwilę zapisu |
| A — nieudany zapis | nad „Zapisz”: `error_outline` + „Nie udało się zapisać. Spróbuj jeszcze raz.” (kolor błędu); arkusz zostaje |
| A — okno „Odrzucić zmiany w rodzinie?” | „Zmiany w tej rodzinie nie zostaną zapisane.” · **„Wróć do rodziny”** (akcent) · „Odrzuć” (kolor tekstu) |
| A — okno „Usunąć rodzinę?” | „Osoby zostają w aplikacji. Znikną tylko ich powiązania w tej rodzinie i daty związku.” (v1.5: daty to teraz także „Razem od”) · **„Zostaw”** (akcent) · „Usuń” (kolor tekstu). „Usuń” usuwa od razu i wraca do [[wpis-osoby]]; błąd usunięcia pod treścią okna: `error_outline` + „Nie udało się usunąć rodziny. Spróbuj jeszcze raz.” |
| B — otwarty | fokus w B2, klawiatura otwarta; B3, a pod nim B4 (gdy jest grób) i B5 |
| B — filtr | sekcje pokazują pasujące wiersze; nagłówek sekcji bez pasujących znika; B3 z wpisanym tekstem |
| B — pusty wynik | B3 i „Nie ma osoby pasującej do „…”.” |
| B — wczytywanie | samo tło (odczyt trwa ułamek sekundy — jak [[zdjecie]] D) |
| **C — krok 1** (v2) | arkusz wysoki, fokus w B2, klawiatura otwarta, „krok 1 z 3” |
| C — nowa osoba | C1' z fokusem w „Imiona”, płeć podpowiedziana, nazwisko zaznaczone |
| C — krok 2 przed wyborem | dwie karty, bez bloku daty i bez „Dalej” |
| C — krok 2 po wyborze | wybrana karta z obrysem 2 dp, blok daty z fokusem, „Nie znam daty” · „Dalej” |
| C — krok 3 | oś czasu nad pytaniem; opcje bez tych, które już padły (po ślubie nie ma „Wzięli ślub”) |
| C — zapisywanie | ostatni przycisk nieaktywny przez chwilę zapisu; po zapisie arkusz się zamyka, karta jest w 9a (reguła 10) |
| C — nieudany zapis | nad przyciskiem `error_outline` + „Nie udało się zapisać. Spróbuj jeszcze raz.”; kroki zostają |
| C — okno „Przerwać dodawanie?” | „To, co podałeś, nie zapisze się.” · **„Wróć”** (akcent) · „Przerwij” |
| D — podsumowanie | wiersze z wartościami albo „Dodaj”; dzieci (C1); „Usuń związek”, „Gotowe” |
| E — dziecko | arkusz wysoki, wybór osoby w trybie „dziecko” |

## Sketch
v2 — kreator partnera (C), krok 2 i krok 3, oraz podsumowanie (D):
```
 C2 — jaki związek                    C3 — co dalej                       D — podsumowanie
┌──────────────────────────────┐  ┌──────────────────────────────┐  ┌──────────────────────────────┐
│ ← Dodaj partnera · krok 2 z 3 ✕│ │ ← Dodaj partnera · krok 3 z 3 ✕│ │ Związek                     ✕│
│ Jaki to był związek?          │  │ Co było dalej?               │  │ Maria i Jan                  │
│ Maria i Jan                   │  │ Maria i Jan · razem od 1946  │  │ Partner   Jan Wymyślony     ›│
│ ╔════════════════════════════╗│  │ ┌──────────────────────────┐ │  │ Razem od  1946              ›│
│ ║ ∞ Razem                    ║│  │ │ ⚭ Wzięli ślub            │ │  │ Ślub      ok. 1948          ›│
│ ║   bez ślubu — ślub możesz… ║│  │ └──────────────────────────┘ │  │ Koniec    Dodaj             ›│
│ ╚════════════════════════════╝│  │ ┌──────────────────────────┐ │  │ Dzieci z tego związku        │
│ ┌────────────────────────────┐│  │ │ ⊘ Związek się zakończył  │ │  │ Stanisław Wymyślony        ✕ │
│ │ ⚭ Małżeństwo               ││  │ └──────────────────────────┘ │  │ Anna Wymyślona             ✕ │
│ └────────────────────────────┘│  │ ┌──────────────────────────┐ │  │ 🗑 Usuń związek     [Gotowe] │
│ Razem od                      │  │ │ ✓ Nic więcej — zapisz    │ │  └──────────────────────────────┘
│ [dokładnie ▾] [1946        ]  │  │ └──────────────────────────┘ │
│        Nie znam daty  [Dalej] │  └──────────────────────────────┘
└──────────────────────────────┘
```
Karta w formularzu po zapisie: [[wpis-osoby]] *Sketch* v5.6.

v1.5 (segment w arkuszu A) i v1 — zastąpione przez v2; szkice zostają jako zapis.
v1.5 — A, część „Para” i związek przy „Małżeństwo”, z nowym dzieckiem (A3'a) i bez linii źródła:
```
│  Para                            │
│  Maria Wymyślona z d. Testowa    │
│  1925–2004 · ta osoba            │
│  Jan Wymyślony                ✕  │
│  1921–1987                       │
│  Związek                         │
│ ┌───────────────┬──────────────┐ │
│ │ ✓ Małżeństwo  │    Razem     │ │  ← A5; ✓ i napis w akcencie
│ └───────────────┴──────────────┘ │
│  Dodaj „Razem od”                │  ← A5' schowany (akcent)
│  Ślub                            │
│ ┌──────────┐ ┌─────────────────┐ │
│ │ około  ▾ │ │ 1948            │ │  ← pusto = ślub był, daty nie znamy
│ └──────────┘ └─────────────────┘ │
│  → ok. 1948                      │
│  Dodaj koniec związku            │
│  Dzieci                          │
│  Stanisław Wymyślony          ✕  │
│  1950–1951                       │
│ ┌ Imiona ─────────────────────┐ ✕│
│ │ Anna▌                       │  │
│ └─────────────────────────────┘  │
│ ┌ Nazwisko ───────────────────┐  │
│ │ ▒Wymyślony▒                 │  │
│ └─────────────────────────────┘  │
│ ┌──────────────┬──────────────┐  │
│ │ ✓ Kobieta    │  Mężczyzna   │  │  ← A3'a: z „Anna”, na bieżąco
│ └──────────────┴──────────────┘  │
│ ┌────────────────┐               │
│ │ 👤+ Dodaj dziecko│              │
│ └────────────────┘               │
│ ┌──────────────────────────────┐ │
│ │            Zapisz            │ │
│ └──────────────────────────────┘ │
```

v1 — A — nowa rodzina z „Dodaj związek” (po dodaniu partnera, dziecka z grobu i nowego dziecka) i B — wybór dziecka.
**v1.1:** szkic jest z v1 — w arkuszu nie ma już kolumny roli („Żona”, „Mąż”, „Syn”, „Córka”); wiersze zaczynają się
od imion. **v1.5:** bez linii źródła (A10), z segmentami A5 i A3'a (szkic wyżej). Reszta bez zmian:
```
 A — nowa rodzina                      B — dodaj dziecko
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│ ←  Nowa rodzina                  │  │ ←  Dodaj dziecko                 │
│    Maria Wymyślona z d. Testowa  │  │ ┌──────────────────────────────┐ │
│  Para                            │  │ │ ⌕  An▌                       │ │
│  Żona   Maria Wymyślona          │  │ └──────────────────────────────┘ │
│         z d. Testowa             │  │  👤+ Nowa osoba: „An”            │
│         1925–2004 · ta osoba     │  │                                  │
│  Mąż    Jan Wymyślony         ✕  │  │  W tym grobie                    │
│         1921–1987                │  │  Anna Wymyślona                  │
│  Ślub                            │  │  już w tej rodzinie   (przygaszone)
│ ┌──────────┐ ┌─────────────────┐ │  │                                  │
│ │ około  ▾ │ │ 1948            │ │  │  Inne osoby                      │
│ └──────────┘ └─────────────────┘ │  │  Anna Testowa                    │
│  → ok. 1948                      │  │  ok. 1930 · Cmentarz Wymyślony   │
│  Dodaj koniec związku            │  │  Joanna Testowa                  │
│  Dzieci                          │  │  ma już rodziców      (przygaszone)
│  Syn    Stanisław Wymyślony   ✕  │  │                                  │
│         1950–1951                │  │                                  │
│  Córka ┌ Imiona ─────────────┐ ✕ │  │        [ klawiatura ]            │
│        │ Anna▌               │   │  │                                  │
│        └─────────────────────┘   │  └──────────────────────────────────┘
│        ┌ Nazwisko ───────────┐   │
│        │ ▒Wymyślony▒         │   │  ← podpowiedź zaznaczona
│        └─────────────────────┘   │
│ ┌────────────────┐               │
│ │ 👤+ Dodaj dziecko│              │
│ └────────────────┘               │
│  Rodzina i jej daty zapiszą się  │
│  ze źródłem: notatki.            │
│ ┌──────────────────────────────┐ │
│ │            Zapisz            │ │
│ └──────────────────────────────┘ │
└──────────────────────────────────┘
```

## Tempo
**v2 — ta sama typowa rodzina** (para małżeńska z grobu, ślub „około”, troje dzieci: jedno z grobu, dwoje nowych), C1:

| Krok | Akcje poza pisaniem |
|---|---|
| [[grob]] → osoba → poprawa, przewinięcie do „Rodzina” | 2 |
| „Dodaj partnera” → Jan z „W tym grobie” | 2 |
| „Małżeństwo” → dopisek „około” (menu, wybór) → rok → „Dalej” | 4 |
| „Nic więcej — zapisz” | 1 |
| dziecko z grobu: „Dodaj dziecko” → wiersz | 2 |
| nowe dziecko: „Dodaj dziecko” → imię → „Nowa osoba” → `next` → nazwisko podpowiedziane → „Dodaj” (płeć z imienia) | 4 |
| drugie nowe dziecko | 4 |
| wstecz do [[grob]] | 1 |
| **Razem** | **20 akcji na rodzinę 5 osób** — tyle co v1, przy jednym pytaniu na ekranie |

- **Para „razem”, potem ślub:** +2 („Wzięli ślub”, „Dalej”) i druga data. **Koniec:** +1 i data.
- **Rodzice (P1), oboje nowi:** „Dodaj rodziców” 1 + mama (imię, „Nowa osoba”, `next`, „Dalej” — 3) + tata (3) +
  „Małżeństwo” 1 + „Nie znam daty” 1 + „Nic więcej” 1 = **10**; płci nie trzeba wybierać, bo wynika z pytania.
- **C2 zamiast C1:** +1 na każde dziecko („Z kim?”) — przy ok. 60 dzieciach z notatek ok. 60 akcji.
- **Co skraca:** wybór z „W tym grobie”; podpowiedzi nazwiska i płci; „Nie znam daty” bez pustego pola; dzieci od razu
  przy właściwej parze (C1).
- **Co wydłuża świadomie:** krok „Co było dalej?” przy każdym związku (+1) — cena osi czasu, o którą prosił autor.

**v1 — typowa rodzina z notatek:** para (ta osoba i mąż z tego samego grobu), rok ślubu z „około”, troje dzieci —
jedno pochowane w tym grobie, dwoje nowych (bez grobu w aplikacji).

| Krok | Akcje poza pisaniem |
|---|---|
| [[grob]] → karta osoby → [[wpis-osoby]] (poprawa), przewinięcie do „Rodzina” | 2 |
| „Dodaj związek” | 1 |
| „Dodaj osobę do pary” → mąż w „W tym grobie” | 2 |
| „Ślub”: dopisek „około” (menu, wybór) → rok → `done` | 3 |
| dziecko z grobu: „Dodaj dziecko” → wiersz | 2 |
| nowe dziecko: „Dodaj dziecko” → imię w B2 → „Nowa osoba: …” → `next` → nazwisko podpowiedziane → `done` | 4 |
| drugie nowe dziecko | 4 |
| „Zapisz” → [[wpis-osoby]] → wstecz do [[grob]] | 2 |
| **Razem** | **20 akcji na rodzinę 5 osób** (ok. 4 na osobę), 0 pytań o źródło |

- Na całe notatki (ok. 100 osób, przy ok. 30 rodzinach podobnej wielkości): **ok. 600 akcji** plus pisanie. Nowe osoby
  z arkusza nie mają dat: jeśli notatki je podają, każda to jeszcze chip + ok. 4 akcje w [[wpis-osoby]] (D4).
- **v1.5: +0 w typowej rodzinie** — „Małżeństwo” domyślnie, płeć nowych osób podpowiedziana z imienia (segmenty poza
  `next`). Zła podpowiedź płci: +1. Związek bez ślubu: +1 („Razem”), a jego data — pisanie. Para razem przed ślubem: +1
  („Dodaj „Razem od””) i data.
- **Co skraca:** wybór z „W tym grobie” bez pisania; nazwisko podpowiedziane; płeć podpowiedziana (v1.5); „Razem od” i
  „Koniec związku” schowane (D7, D12); źródło bez pytania.
- **Co wydłuża świadomie:** „najpierw szukaj” — +1 dotknięcie na każdą nową osobę („Nowa osoba”). To cena
  AC-5 (D3). Wejście przez formularz osoby w poprawie — +1 dotknięcie na rodzinę (D2).

## Style B rules applied
- **Reguła 1:** jedyny wypełniony przycisk to „Zapisz”. „Dodaj osobę do pary” i „Dodaj dziecko” mają obrys i ikonę
  w akcencie; „Dodaj koniec związku” to przycisk tekstowy w linii treści (akcent); „Usuń rodzinę” — tekstowy w
  kolorze tekstu; w oknach bezpieczne działanie w akcencie.
- **Reguła 3:** ikony `outlined` — `person_add_alt_outlined`, `delete_outline`, `search`, `close`, `error_outline`;
  `close` ma `tooltip`.
- **Reguła 5:** marginesy 16 dp; między grupami (para · ślub · dzieci) 24 dp; wiersze bez odstępu (lista).
- **Reguła 6:** lata i podgląd dat jak w [[grob]] i [[wpis-osoby]].
- **Reguła 7:** komunikaty składu mówią, czego brakuje, bez „błąd”; okno usunięcia mówi, co zostaje.
- **Reguła 8:** bez znicza — arkusz to działanie.
- **Reguła 10:** zapis wraca do formularza osoby, gdzie zmiana jest widoczna w sekcji „Rodzina”, bez okienka.
- **Reguła 11:** wiersze arkusza **nie są kartami** — nie prowadzą dalej (D11). Wiersze w B to lista wyboru, jak D
  w [[zdjecie]].
- *Thresholds:* cele ≥ 48 dp (`close` 48, wiersze 56); wiersz nieaktywny niesie powód tekstem (SC 1.4.1); przyciski
  i wiersze rosną z tekstem (SC 1.4.4).
- **Kreator i podsumowanie (v2, C–E):** arkusz od dołu na powierzchni (jak arkusz cmentarza, [[cmentarze]]); jeden
  wypełniony przycisk na krok („Dalej” / „Zapisz” / „Dodaj” / „Gotowe”, reguła 1), „Nie znam daty” — tekstowy. Karty-opcje
  z ikoną w akcencie (warianty `outlined`, reguła 3; konkretne ikony wybiera przegląd `ui` zbudowanego ekranu); wybrana karta: obrys 2 dp w akcencie i stan „zaznaczone” dla czytnika (SC 1.4.1). Karta partnera w
  9a — reguła 11 (karta prowadzi do wpisu), ✎ jak w [[grob]] element 3. Tokeny bez zmian.
- **Segmenty (v1.5, A5, A3'a) — zastąpione w v2:** wybrany segment w akcencie z ✓ ([[style-b]] *Token roles* — „aktywny segment”;
  kolor nie sam, SC 1.4.1); obrys segmentu na tle 3,40:1 (SC 1.4.11 ✅), napis w akcencie na powierzchni 8,04:1.
- **Nowe tokeny:** brak. Pary: tekst pomocniczy na tle 5,50:1, obrys na tle 3,40:1 (pomiar [[style-b]] 2026-10-06).

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-003 AC-1 | A3–A4, A3', A8–A9, B3, A12 | w jednym arkuszu para i dzieci; „Nowa osoba” tworzy osobę przy zapisie rodziny; po „Zapisz” wszyscy są w sekcji „Rodzina” ([[wpis-osoby]] 9a) |
| US-003 AC-2 | A4 → B5; [[wpis-osoby]] 9a „Dodaj związek” | ta sama osoba w drugim arkuszu jako para; w jej sekcji „Rodzina” dwie grupy „Związek”, każda ze swoimi dziećmi — także po rozstaniu albo owdowieniu (uwaga autora do O1) |
| US-003 AC-3 | A5, A6' | pięć dopisków przy ślubie i końcu; podgląd przed zapisem, a po zapisie w etykiecie grupy („Związek · ślub ok. 1948 · koniec 1960”) |
| US-003 AC-4 | — (v1.5) | przynależność i daty dalej zapisują się ze źródłem „notatki” i statusem `CLAIMED`, bez pytania i **bez tekstu na ekranie** (SPIKE-004 D28) |
| ISSUE-025 AC-3 (v2) | C1 → C2 → C3 → C3a → C3 · D | Jan → „Razem” 1980 → „Wzięli ślub” 1985 → „Nic więcej — zapisz” → karta „razem od 1980 · ślub 1985”, rola „Mąż”/„Żona”; w D obie daty |
| ISSUE-025: związek bez ślubu (v2) | C2 „Razem”, C3 „Nic więcej” | karta „razem od 1980”, rola „Partner” / „Partnerka” |
| ISSUE-025: ślub bez daty (v2) | C2 „Małżeństwo” → „Nie znam daty” | karta „Małżeństwo”, rola „Mąż”/„Żona”; po zmianie innego wiersza w D ślub zostaje |
| ISSUE-025: płeć nowej osoby (v2) | C1', E | „Anna” → ♀ zaznaczona; po zapisie chip „Córka: Anna” |
| ISSUE-025 AC-4 (v2) | D (poprawa starej rodziny) | rodzina z kopii sprzed migracji: „Razem od” — „Dodaj”; bez ślubu → rola „Partner”, ze ślubem → „Mąż”/„Żona” z jego datą |
| US-003 AC-5 | B2, B4, B5, B3 | osoba z grobu jest na liście, zanim da się utworzyć nową; wybór dodaje istniejącą osobę |
| ISSUE-019: najwyżej dwie osoby w parze | A4 | przy dwóch osobach w parze przycisku nie ma |
| ISSUE-019: zapis całością | A12 | po nieudanym zapisie nic z arkusza nie ma w bazie (test `qa`) |
| ISSUE-019: styl B | całość | reguły wyżej; przegląd `ui` |

## Decisions
| Decyzja | Dlaczego | Obali |
|---|---|---|
| **D1 — arkusz ma własne „Zapisz” i zapisuje się od razu**, nie z „Zapisz” formularza osoby | rodzina to osobny rekord, który dotyka kilku osób; arkusz ma własne pola. W aplikacji „Gotowe” wraca do formularza bez zapisu (zdjęcia, [[zdjecia-osoby]] D1), a „Zapisz” zapisuje (jak okno „Popraw grób”) — arkusz mówi „Zapisz” | autor oczekuje, że „Odrzuć” w formularzu osoby cofnie też rodzinę |
| **D2 — arkusz otwiera się z formularza osoby w poprawie**, nie przy nowej osobie | arkusz pokazuje „tę osobę”, więc musi ona już istnieć; formularz nowej osoby nie zapisuje się po cichu. Koszt: +1 dotknięcie (karta w [[grob]]) na rodzinę | autor przy przepisywaniu grobu chce dodać rodzinę od razu przy nowej osobie → „Zapisz i dodaj rodzinę” |
| **D3 — najpierw szukaj, potem twórz** (B: pole z fokusem, „Nowa osoba” nad listą) | AC-5: duplikat osoby rozbija rodziny i ścieżkę (dwie te same osoby w różnych rodzinach). Koszt: +1 dotknięcie na nową osobę | autor przy nowych osobach nie patrzy na listę → „Nowe dziecko” wprost w arkuszu, a duplikaty łapie dopiero ostrzeżenie |
| **D4 — nowa osoba w arkuszu to imiona i nazwisko**; daty i reszta w jej wpisie (chip) | arkusz to szybkość dla całej rodziny; pełny formularz w środku arkusza to zapis w zapisie. *Family group sheet* ma przy dziecku datę urodzenia, ale tu przy każdej osobie z notatek byłby to blok daty | przy przepisywaniu prawie każda nowa osoba ma w notatkach daty → rok urodzenia w wierszu A3' (+1 pole) |
| **D5 — dziecko ma jedną rodzinę rodziców**; osoba z rodzicami jest w B nieaktywna („ma już rodziców”) | druga rodzina rodziców to sprzeczne twierdzenie albo przysposobienie: pierwsze to [[US-004-fakt-od-babci]], drugie jest poza zakresem. Blokada chroni przed pomyłkowym podpięciem | w notatkach jest przysposobienie albo dwie wersje rodziców |
| **D6 — rodzina musi mieć osobę w parze** | [[FR-002-rodzina-jako-rekord]]: 1–2 partnerów i dzieci; AC-1 też mówi „1-2 partnerów” | notatki znają rodzeństwo bez imion rodziców → rodzina bez pary (schemat tego nie zabrania) |
| **D7 — „Koniec związku” schowany za przyciskiem**, z linią „np. rozwód albo rozstanie. Owdowienie to zgon osoby — zapisuje się w jej wpisie.” (v1.1) | w notatkach rzadki; schowany nie kosztuje `next` w każdej rodzinie. Linia zapobiega wpisaniu daty śmierci drugi raz | notatki często mają rozwody albo autor wpisuje tam daty zgonu |
| **D8 — „Usuń rodzinę” w poprawie, z oknem** — element spoza AC | bez niego pomyłkowo utworzona rodzina nie ma wyjścia (arkusz nie zapisze rodziny z jedną osobą). Osoby zostają, znikają tylko powiązania. Okno, więc to nie jest ciche usunięcie (brief G7/C5) | autor woli bez usuwania, jak przy osobie ([[wpis-osoby]] → „Bez usuwania osoby”) |
| ~~**D9 — rola w wierszu i w chipie z płci**~~ — **obalone na stopie #1** (autor: bez płci) → **D9' — nazwy neutralne, bez kolumny roli w arkuszu** (*Role names*) | odchodzi od R4 („Mąż: Jan”, „Córka: Anna”) świadomie: płci nie ma w danych, a zgadywanie z imienia autor odrzucił. Chip mówi „Rodzic”, „Partner”, „Dziecko” | nazwy relacji na ścieżce i w drzewie (EPIC-003, R3: „jej tata”, „jej mąż”) albo powinowactwo („teść”) okażą się potrzebne → płeć wraca jako pole osoby, wtedy z migracją |
| ~~**D10 — kolejność dzieci: dodania**~~ — **zastąpione na stopie #1** (decyzja autora D4) → **D10' — według daty urodzenia** (A8, [[wpis-osoby]] 9a) | kanon GEDCOM 7: *„The order of the CHIL (children) pointers … should be chronological by birth”*. Z D10 zostaje tylko to, że wiersz dodany w trakcie edycji nie skacze | — |
| **D11 — wiersze arkusza nie prowadzą do wpisu osoby** | arkusz nie jest bramą do kolejnych formularzy (zapis w zapisie, utrata zmian w arkuszu); osobę poprawia się przez chip w jej rodzinie | autor po zapisie rodziny od razu chce dopisać daty nowych dzieci i chip jest za daleko |
| **D15 — związek to oś czasu w kreatorze** (v2, autor na stopie #1 ISSUE-025): razem od → ślub → koniec, krok po kroku, jedno pytanie na ekranie; po zapisie karta partnera, ✎ → podsumowanie | autor chce widzieć „ewolucję” związku i dodawać ją pojedynczo; ta sama oś trafi do drzewa (linia przerywana od „Razem od”, ciągła od ślubu — [[drzewo]] D4). Kanon: kreator z krokiem przeglądu (D) — zmiana jednej daty bez przechodzenia wszystkiego. Dane jak w D12: ślub bez daty to zdarzenie bez daty (GEDCOM `MARR Y`) | przy przepisywaniu ok. 30 rodzin kreator męczy bardziej niż jeden arkusz — wtedy tryb „wszystko na jednym ekranie” dla kolejnych rodzin |
| **D16 — ✎ otwiera podsumowanie, nie kreator od początku** (v2) | zmiana jednej daty przez trzy kroki kosztowałaby 3–4 dotknięcia zamiast 1–2; podsumowanie to krok przeglądu, który kreatory pokazują na końcu | autor wybiera ✎ i oczekuje kreatora od początku (np. żeby przejść oś jeszcze raz) |
| **D17 — „Dodaj rodziców” przez ten sam kreator, z pytaniami „Kto jest mamą?” i „Kto jest tatą?”** (v2, P1 — rekomendacja, *Open* 6) | przepisywanie idzie od grobu w górę: rodzice to najczęstsza rodzina dodawana z wpisu dziecka. Pytanie „mama/tata” od razu daje płeć nowej osoby. „Nie wiem” przy tacie, bo notatki często znają tylko matkę | autor dodaje rodziców zawsze od strony rodzica (P2) |
| **D18 — dzieci pod kartą związku** (v2, C1 — rekomendacja, *Open* 5) | dziecko należy do pary (FR-002, GEDCOM `FAM`); miejsce dodania mówi, z którego związku, więc bez pytania „Z kim?” (−1 akcja na dziecko wobec C2) | autor chce jednej listy dzieci osoby według urodzenia — C2 |
| ~~**D12 — rodzaj związku to wybór, a nie wniosek z dat** (v1.5, rekomendacja — *Open* 4): segment „Małżeństwo · Razem”, „Razem od” i „Ślub” pod nim opcjonalne~~ — **zastąpione przez D15** (autor: oś czasu w kreatorze; dane z D12 zostają) | notatki często mówią „żona Jana” bez daty ślubu — przy nazwach z samej daty (v1.4) taka para dostałaby „Partner/Partnerka”, czyli nieprawdę. Kanon: GEDCOM 7 pozwala zapisać zdarzenie bez daty (`1 MARR Y` — „zdarzenie zaszło, szczegółów brak”; `planning` cytuje specyfikację), więc „Małżeństwo” z pustą datą = ślub bez daty. Segment to dosłownie „dwa tryby połączenia (razem, małżeństwo)” z D20. „Małżeństwo” domyślnie, bo w notatkach przeważa; „Razem od” przy małżeństwie schowane, bo rzadkie (para razem przed ślubem, przykład autora z D20) | autor na stopie #1 woli same daty (v1.4) i godzi się, że ślub bez daty to „Partner” — albo przy przepisywaniu prawie każda para ma datę ślubu, więc segment nic nie wnosi |
| **D13 — nazwa partnera nie zmienia się po końcu związku** („Mąż”, nie „Były mąż”) (v1.5) | koniec związku widać w etykiecie grupy („· koniec 1960”, [[wpis-osoby]] 9a d); chip mówi, kim osoby były dla siebie, a notatki opisują przeszłość. Jedna nazwa mniej w słowniku | autor czyta „Mąż” przy rozwiedzionej parze jako błąd — wtedy „Były mąż” / „Była partnerka” przy rodzinie z końcem |
| **D14 — płeć nowej osoby w arkuszu** (A3'a, v1.5) | osoby z arkusza to rodzice i dzieci bez grobu, czyli duża część osób, a ich płeć decyduje o stronie (stryj czy wuj, [[osoba]] D4). Bez A3'a każda taka osoba wymagałaby osobnej poprawy przez chip (+ok. 4 akcje). Podpowiedź z imienia jak w [[wpis-osoby]] *D-płeć*, więc +0 przy trafnej | wiersz A3' z segmentem jest za wysoki przy kilku nowych dzieciach — wtedy płeć tylko w formularzu, a w arkuszu cicha podpowiedź pokazana w chipie po zapisie |

## Open
**Rozstrzygnięte na stopie #1 [[ISSUE-019-family-relations]] (2026-10-07):** 1 → **C**, z uwagą autora o rozstaniach,
owdowieniach i nowych związkach (v1.1: słowo „związek”); 2 → **bez płci** (P2); 3 → **bez rodzeństwa**. Treść pytań
zostaje niżej jako zapis tego, co rozważano.

1. ~~⚠️ OPEN~~ **— droga wejścia relacji** (US-003 → *Notes*; [[wpis-osoby]] → *Decisions* → „Zdjęcie i relacje później”).
   - **C (rekomendacja): relacje widać w formularzu osoby (9a, chipy jak R4), a wpisuje się je arkuszem** (ten
     plik), otwieranym z tej sekcji. Kanon briefu i FR-002 mówią „rodziną naraz”, R4 i uwaga autora — „przy osobie”.
     Warunek, który obalał kierunek z v2 („arkusz → relacje nie trafiają do formularza”), trafił częściowo:
     **wpisywanie** jest w arkuszu, **widok** w formularzu.
   - A: relacje po jednej z formularza osoby („Dodaj ojca”, „Dodaj męża”, „Dodaj dziecko”), a pod spodem dalej
     rodziny, które aplikacja dobiera sama. Bez nowego ekranu arkusza, ale sprzeczne z FR-002 (wpis osoba po osobie
     → zmiana FR), a przy powtórnym małżeństwie „Dodaj dziecko” musi pytać, z którą parą.
   - B: sam arkusz, wejście z [[grob]], bez sekcji w formularzu — nie odpowiada na uwagę autora (relacji nie widać
     przy osobie).
2. ~~⚠️ OPEN~~ **— płeć osoby** (wybrane P2; pomiar reguły z imienia — [[ISSUE-019-family-relations]] → *Prior art*). `Persons` nie ma płci, a od niej zależą nazwy relacji (*Role names*).
   - **P1 (rekomendacja): pole „Płeć” w formularzu osoby** ([[wpis-osoby]] 4a: Kobieta · Mężczyzna; bez wyboru =
     nieznana), **podpowiedziane z imienia** przy nowej osobie i w wierszu A3': pierwsze imię na „-a” → Kobieta,
     inne → Mężczyzna, bez imion — bez wyboru. Podpowiedź widać w polu i w nazwie roli, zmiana to jedno dotknięcie.
     +0 akcji przy trafnej podpowiedzi. Ryzyko: imiona męskie na „-a” (np. Kuba, Barnaba) dostaną złą podpowiedź
     — widoczną od razu. Poprawa wpisu nigdy nie zmienia płci sama. Schemat v6 dostaje kolumnę płci (w GEDCOM 7
     osoba ma `SEX` — `planning` cytuje specyfikację). Płeć bez źródła, jak imiona ([[FR-001-provenance]] →
     ziarnistość: twierdzenia na datach, relacjach i pochówku).
   - P1': to samo pole bez podpowiedzi — +1 dotknięcie na osobę (ok. 100 na całe notatki).
   - P2: bez płci — nazwy neutralne („Rodzic”, „Małżonek”, „Dziecko”), 0 akcji, osoba w schemacie bez zmian.
     Odchodzi od R4, a ścieżka z R3 („jej tata”, „jej mąż”) i powinowactwo z uwagi autora („teść”) będą potrzebować
     płci później — wtedy z migracją i uzupełnianiem ok. 100 osób.
3. ~~⚠️ OPEN~~ **— relacje dalsze w sekcji „Rodzina”** (wybrany wariant węższy) ([[wpis-osoby]] 9a).
   - **Rekomendacja: rodzeństwo tak** — to inne dzieci tej samej rodziny rodziców, bez nowych danych i bez nowego
     wpisywania (chipy „Brat: …”, „Siostra: …”). **Teściowie, dziadkowie i dalsi — nie:** to ścieżka przez dwie
     rodziny i więcej, czyli sekcja „Jak łączy się ze mną” z R4 prawego ([[EPIC-002-wizyta]], M5).
   - Wariant węższy: same rodziny osoby (rodzice, małżonkowie, dzieci).

**Rozstrzygnięte na stopie #1 ISSUE-025, runda 2 (2026-10-08, autor: „C1 / P1 / Jest dobrze”):** 5 → **C1**, 6 → **P1**.
Treść pytań zostaje jako zapis tego, co rozważano.

5. ~~⚠️ OPEN~~ — **dzieci przy nowym kształcie** (v2, stop #1 ISSUE-025, runda 2; prototyp, panel 4).
   - **C1 (rekomendacja):** pod kartą związku, „Dodaj dziecko” na karcie (D18, E);
   - **C2:** osobna sekcja „Dzieci” w 9a, według daty urodzenia; „Dodaj dziecko” pyta „Z kim?” (+1 na dziecko).
6. ~~⚠️ OPEN~~ — **rodzice przy nowym kształcie** (v2; prototyp, panel 5).
   - **P1 (rekomendacja):** „Dodaj rodziców” → kreator: mama → tata (albo „Nie wiem”) → związek → co dalej (D17);
   - **P2:** bez „Dodaj rodziców” — rodziców dodaje się we wpisie rodzica (partner, potem dziecko).

4. ~~⚠️ OPEN~~ **— rodzaj związku: wybór czy daty** — **rozstrzygnięte na stopie #1 ISSUE-025, runda 1:** ani R, ani V —
   autor opisał oś czasu w kreatorze (v2, D15). Zapis rozważanych wariantów:
   - **R (rekomendacja): segment „Małżeństwo · Razem”** (A5, D12) — ślub bez daty to dalej „Mąż/Żona”; +0 w typowej
     rodzinie, +1 przy związku bez ślubu. Schemat musi umieć ślub bez daty (`planning` sprawdza zdarzenie bez daty);
   - **V (v1.4 dosłownie): same daty** — „Mąż/Żona” tylko przy wpisanej dacie ślubu, bez segmentu. Mniej na ekranie, ale
     para z notatek bez daty ślubu dostaje „Partner/Partnerka”.

**Poza zakresem tej wersji** (nazwane, żeby nie poszerzać po cichu): osoba żyjąca (`is_living` zostaje wartością
domyślną, czyli „nie żyje”, także dla żyjących osób dodanych arkuszem; ekran nie pokazuje tego nigdzie, a pole
przyjdzie z eksportem, który od niego zależy — [[US-006-eksport-dla-rodziny]]); kontrola, czy nikt nie jest swoim
przodkiem (poza blokadą w B); rodzaj więzi dziecka z rodzicami (przysposobienie — D5).
