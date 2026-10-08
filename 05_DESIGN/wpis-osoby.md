---
screen: "Wpis osoby w grobie — formularz"
items: ["[[ISSUE-012-transcribe-grave-screen]]", "[[ISSUE-017-person-photos]]", "[[ISSUE-018-profile-photo-crop]]", "[[ISSUE-019-family-relations]]"]
us: "[[US-002-przepisanie-grobu]] · [[US-005-zdjecia]] · [[US-003-przepisanie-rodziny]]"
journey-step: "n/a — M1 (warunek kroku 1 UJ-001)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-cmentarz-grob-osoba.html (ramki 3–4, ISSUE-012) · makieta-zdjecia.html (ramki 7–8 — kierunek sprzed stopu #1 ISSUE-016) · makieta-zdjecia-osoby.html (ramki 1–2, ISSUE-017) · makieta-rodzina.html (ramki 1–2, ISSUE-019)"
updated: 2026-10-07
---

# Wpis osoby — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]]. Referencja: formularza nie ma w [[references]]
> (R1–R4), więc ekran dziedziczy reguły stylu B i formę kart i przycisków z R4.
>
> **Wersja 2 (2026-10-07, przed planem ISSUE-012)** — według uwag autora z 2026-10-06
> ([[ISSUE-012-transcribe-grave-screen]] → *Input from the author* 4 i decyzja o kolejności): **„kim była” to
> krótka biografia** z linią źródła (element 8: podpowiedź, większe pole). Zdjęcie i relacje, których brakowało
> autorowi, dochodzą z [[US-005-zdjecia]] i [[US-003-przepisanie-rodziny]] — ich miejsce w formularzu: *Decisions* → „Zdjęcie i relacje później”.
> Podtytuł paska z nazwą grobu (element 1). Reszta bez zmian.
>
> **Wersja 2.1 — przegląd `ui` zbudowanego ekranu (2026-10-07, ISSUE-012):** *Open* 1 i 2 rozstrzygnięte;
> poprawki z przeglądu wprowadzone w kodzie przed stopem #2; odstępstwa `dev` przyjęte
> ([[ISSUE-012-transcribe-grave-screen]] → *Dev report → Deviations*, *Verification*):
> - **poprawa wpisu wchodzi** (stop #1, D1) → *Navigation*, *States*;
> - **klawiatura daty:** `TextInputType.datetime` (Gboard: cyfry, `.`, `-`, `/`, „dalej”), filtr znaków `[0-9./-]`,
>   najwyżej 10 znaków → element c;
> - **fokus od wejścia tylko przy nowej osobie** — w poprawie bez fokusu, bo poprawę najpierw się czyta → element 2;
> - **blok daty:** podpowiedzi „rok albo dd.mm.rrrr”, a przy „między” — „od” i „do”; „Podaj pierwszą datę.” /
>   „Podaj drugą datę.”, gdy przy „między” brakuje jednej z dat; komunikat pod całym blokiem, ramka błędu na złym
>   polu; **otwarcie menu chowa klawiaturę** (zasłaniała dolne pozycje); **wybrany dopisek z ikoną ✓**, nie tylko w
>   akcencie (SC 1.4.1); **przycisk dopisku ma rozmiar najmniejszy 116 × 56 dp i rośnie z tekstem**, bez ucinania
>   (SC 1.4.4) → elementy b–e;
> - **element 9:** „Zmień” to przycisk tekstowy w akcencie;
> - **element 10:** na końcu przewijanej treści, nad „Zapisz” (nie przypięty — pas nad klawiaturą najniższy). W
>   poprawie: „Poprawa nie zmienia źródła dat. Nowa data zapisze się ze źródłem: notatki.”;
> - **odstęp pasek → pierwsze pole:** 24 dp;
> - **formularz zbudowany w całości** (nie leniwie), żeby pole poza ekranem było w kolejności `next`;
> - *States* → „nieudany zapis”.
>
> **Wersja 2.2 — stop #2 ISSUE-012 (2026-10-07, decyzja autora):** **bez pola „Pochówek”** (element 7).
> Autor: *„pochówek jest informacją zbędną (imo to jest to samo co zgon)”*. Każde pole mnoży się przez ok. 100
> wpisów. **Czy notatki podają daty pochówku — niesprawdzone.** *Obali:* pierwszy wpis z datą pochówku przy
> przepisywaniu ([[NT-002-transcribe-the-notes]]) — wtedy pole wraca, bo inaczej data trafi do „kim była”, bez
> dopisku i bez twierdzenia. Model danych ją zachowuje (w GEDCOM `BURI` to osobne zdarzenie obok `DEAT`; w starszych księgach parafii
> bywa jedyną datą), więc pole może wrócić bez migracji — np. ze źródłem innym niż notatki ([[US-004-fakt-od-babci]]).
> Poprawa wpisu nie rusza daty pochówku, którą osoba już ma. Tempo: 7 akcji na osobę zamiast 8.
>
> **Wersja 3 — KIERUNEK dla [[ISSUE-017-person-photos]], nie obowiązuje w ISSUE-016** (2026-10-07): zdjęcie osoby
> na górze formularza, przed imionami (element 1a), w miejscu wskazanym w v2 (*Decisions* → „Zdjęcie i relacje
> później”); poza kolejnością `next` i bez fokusu, więc wpis bez zdjęcia kosztuje tyle co dotąd. **Na stopie #1
> ISSUE-016 autor zdecydował inaczej niż v3:** osoba ma **bazę zdjęć** (dzieloną z innymi osobami, gdy na zdjęciu
> jest kilka osób) i wybrane **„profilowe”**. Element 1a pokaże więc profilowe, a D-zdjęcie-1 („jedno zdjęcie na
> osobę”) jest nieaktualne. `ui` przeprojektuje to przed planem ISSUE-017. **Formularz w ISSUE-016 się nie zmienia.**
>
> **Wersja 4 (2026-10-07, przed planem [[ISSUE-017-person-photos]]) — baza zdjęć osoby.** Element 1a zostaje na
> swoim miejscu i dalej stoi poza `next`. Zmienia się to, co pokazuje i dokąd prowadzi:
> - **bez zdjęć:** jak v3 — „Dodaj zdjęcie” otwiera arkusz źródła, a galeria pozwala wybrać kilka zdjęć;
> - **ze zdjęciami:** okrąg pokazuje **profilowe** (pierwsze łącze), a pod nim liczbę zdjęć. Dotknięcie otwiera bazę
>   zdjęć osoby ([[zdjecia-osoby]]), nie podgląd.
>
> Wszystkie zmiany zdjęć (dodanie, profilowe, osoby na zdjęciu, usunięcie z osoby) zapisują się z „Zapisz”, razem
> z wpisem (D-zdjęcie-2, rozszerzone). D-zdjęcie-1 zastępuje D-zdjęcie-4.
>
> **Wersja 4.1 (2026-10-07, przed planem [[ISSUE-018-profile-photo-crop]]):** okrąg 1a pokazuje profilowe **w kadrze**
> z [[kadr-profilowego]]; bez kadru — jak dotąd, ze środka. D-zdjęcie-3 („bez kadrowania”) obalone na stopie #2
> ISSUE-017. Formularz poza tym bez zmian; kadr zapisuje się z „Zapisz”, jak pozostałe zmiany zdjęć.
>
> **Wersja 5 (2026-10-07, przed planem [[ISSUE-019-family-relations]]) — relacje.** Uwaga autora z 2026-10-06: w
> formularzu brakuje, *„z kim osoba jest związana (pokrewieństwo, powinowactwo)”*. Według rekomendacji z
> [[rodzina]] → *Open* (decyzja autora na stopie #1):
> - **9a „Rodzina”** pod biografią, w miejscu wskazanym w v2: chipy relacji jak w R4 prawym, które prowadzą do wpisu
>   krewnego, i wejścia do arkusza rodziny ([[rodzina]]). **Tylko w poprawie** — arkusz potrzebuje zapisanej osoby;
> - **4a „Płeć”** (Kobieta · Mężczyzna), podpowiedziana z imienia — od niej zależą nazwy relacji ([[rodzina]] →
>   *Open* 2). Poza `next`;
> - **poprawa osoby bez grobu** — wpis otwarty z chipu krewnego, który nie ma pochówku (np. dziecko dodane
>   arkuszem). Zapis wraca tam, skąd go otwarto.
>
> Kierunek z v2 („relacje w formularzu”) i jego warunek obalający („arkusz → relacje nie trafiają do formularza”)
> godzi podział: **wpisywanie w arkuszu, widok w formularzu** (*Decisions* → „Zdjęcie i relacje później”).
>
> **Wersja 5.1 (2026-10-07, stop #1 ISSUE-019 — decyzje autora):** **bez płci** — elementu 4a nie ma, a chipy mają
> nazwy neutralne („Rodzic”, „Partner”, „Dziecko”, [[rodzina]] → *Role names*); **bez rodzeństwa** (9a c); **„Związek”**
> zamiast „Małżeństwo” i **„Dodaj związek”** (uwaga autora: rozstania, owdowienia, nowe związki); dzieci w 9a
> **według daty urodzenia**.
>
> **Wersja 5.2 (2026-10-07, przegląd `ui` ISSUE-019):** blok daty z błędem przewija się cały, z linią komunikatu nad
> przypiętym „Zapisz” — dotyczy też „Urodzenie” i „Zgon” (wspólny `DateBlock`); *Navigation* bez słów sprzed v5.1; chip
> „co najmniej 32 dp”.
>
> **Wersja 5.3 — płeć wraca, formularz to poprawa z widoku osoby ([[SPIKE-004-mvp-flow-prototype]] D4, D13, D16,
> 2026-10-08):**
> - **4a „Płeć” wraca** w kształcie z v5 (Kobieta · Mężczyzna, podpowiedziana z imienia, poza `next`), bo nazwy
>   pokrewieństwa w widoku osoby jej potrzebują ([[osoba]] D4). Autor: *„musi wrócić płeć”*. Wiersz 4a i *D-płeć*
>   niżej są przekreślone z v5.1 — odkreśli je pozycja, która pole zbuduje (z migracją schematu);
> - **tryb „poprawa” otwiera się z ✎ w widoku osoby** ([[osoba]]), a nie z karty osoby w [[grob]] ani z chipu krewnego —
>   te prowadzą do widoku osoby ([[style-b]] reguła 15). Po zapisie poprawy formularz wraca do widoku osoby.
>
> **Wersja 5.4 — bez źródeł ([[SPIKE-004-mvp-flow-prototype]] D28, 2026-10-08):** autor: *„a to jakiś błąd się wkradł w takim razie - moje notatki to moje notatki, nie potrzeba żadnych potwierdzeń skąd pochodzą”*. Elementy 9 („Źródło: notatki · Zmień” przy „kim
> była”) i 10 (tekst o źródle dat i pochówku) **znikają**. Schemat dalej dostaje domyślne źródło, po cichu. Wiedza od
> babci wchodzi tą samą poprawą (✎ w [[osoba]]), bez osobnej drogi (SPIKE-004 D27).

## Purpose
Wpisanie jednej osoby pochowanej w grobie, tak jak stoi w notatkach: zdjęcie (gdy jest), imiona, nazwisko,
nazwisko rodowe, daty urodzenia i zgonu z dopiskiem oraz **krótka biografia („kim była”)** z linią źródła. To
**najczęściej używany ekran przepisywania — ok. 100 razy** (G6), więc jego miarą jest koszt jednego wpisu.

## Navigation
- Z [[cmentarz]] → „Dodaj grób” → tryb **„nowy grób”**. Zapis tworzy grób i osobę razem.
- Z [[grob]] → „Dodaj osobę” → tryb **„kolejna osoba”**.
- Z [[grob]] → dotknięcie osoby → tryb **„poprawa”** (ISSUE-012, D1).
- **Zapis → [[grob]]**, który zastępuje formularz na stosie (wstecz z grobu wraca do cmentarza).
- **Wstecz z wpisanymi danymi** (przycisk albo gest) → okno „Odrzucić wpis?”. Bez wpisanych danych →
  od razu wstecz. **Wybrane albo zmienione zdjęcie to też wpisane dane** (v3).
- **Zdjęcia (1a, v4):** bez zdjęć → arkusz źródła ([[zdjecie]] A w trybie osoby: galeria — kilka zdjęć, aparat —
  jedno); ze zdjęciami → baza zdjęć osoby ([[zdjecia-osoby]]), a z niej podgląd ([[zdjecie]] B w trybie osoby).
  Powrót z arkusza, systemowego okna albo bazy wraca do formularza z wpisanymi danymi, bez zmiany fokusu na pole.
- **Okno „Odrzucić wpis?” przy zmianach zdjęć (v4):** treść „Wpisane dane i zmiany zdjęć nie zostaną zapisane.”, gdy
  w tej edycji zmieniono zdjęcia (także gdy pól nie ruszano). Bez zmian zdjęć treść jak dotąd.
- **Rodzina (9a, v5):**
  - chip krewnego → [[wpis-osoby]] w trybie „poprawa” **tej osoby**, położony na obecny formularz, który zostaje pod
    spodem z wpisanymi danymi. **Zapis albo wstecz wraca do formularza pod spodem**, a ten odświeża sekcję
    „Rodzina” (krewny mógł zmienić imię);
  - ✎ przy grupie, „Dodaj rodziców”, „Dodaj związek” → [[rodzina]] A. Arkusz zapisuje się sam ([[rodzina]] D1),
    a po powrocie sekcja się odświeża. Niezapisane pola formularza zostają.
- **Poprawa osoby bez grobu (v5):** podtytuł paska „bez grobu w aplikacji”; „Zapisz” wraca tam, skąd otwarto wpis
  (nie do [[grob]]). W „Kto jest na zdjęciu?” ([[zdjecie]] D4) sekcja „W tym grobie” ma tylko tę osobę.
- **Zapis wpisu otwartego z chipu** (z grobem albo bez) też wraca tam, skąd go otwarto, a nie do [[grob]].

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek: „Osoba w grobie” (w poprawie: „Poprawa wpisu”); podtytuł (tekst pomocniczy, jedna linia): w trybie „nowy grób” — „Cmentarz Wymyślony · nowy grób”; w trybie „kolejna osoba” i w poprawie — nazwa grobu, a bez nazwy nazwa cmentarza, i „· w grobie: 2 osoby” | tytuł | — | — | — | decyzja projektowa · [[grob]] D1 |
| 1a | **Zdjęcia osoby** (v4) — wyśrodkowane, okrąg **80 dp**, odstęp 24 dp do „Imiona”. **Bez zdjęć:** jak v3 — okrąg z obrysem 1 dp (kolor obrysu), w środku `add_a_photo_outlined` (28 dp, akcent), pod okręgiem „Dodaj zdjęcie” (14 sp, kolor tekstu); opis dla czytnika „Dodaj zdjęcie osoby”. **Ze zdjęciami:** **profilowe** (pierwsze łącze) w kadrze łącza ([[kadr-profilowego]], v4.1), a bez kadru przycięte do okręgu ze środka; pod okręgiem liczba zdjęć z odmianą — „1 zdjęcie” · „3 zdjęcia” · „5 zdjęć” (14 sp, tekst pomocniczy, `plural`); opis „Zdjęcia osoby: 3 — otwórz”. W obu stanach cała grupa (okrąg z podpisem) to jeden przycisk | przycisk (cel ≥ 80 dp) | dotknięcie → [[zdjecie]] A w trybie osoby (bez zdjęć) albo [[zdjecia-osoby]] (ze zdjęciami). **Poza kolejnością `next`, nie bierze fokusu** | bez zdjęć; w poprawie — profilowe i liczba zdjęć osoby | — | US-005 AC-1 · ISSUE-017 AC 4 · R4 prawy · D-zdjęcie-2…4 |
| 2 | **Imiona** | pole tekstowe, wielka litera na początku słów | `next`; **fokus i klawiatura od razu po wejściu** w trybach „nowy grób” i „kolejna osoba”; w poprawie bez fokusu (v2.1) | pusto | imiona albo nazwisko, co najmniej jedno: „Podaj imiona albo nazwisko.” | AC-2 |
| 3 | **Nazwisko** | pole tekstowe, wielka litera na początku słów | `next` | w trybie „kolejna osoba”: nazwisko ostatnio wpisanej osoby w tym grobie, **zaznaczone** (pisanie je zastępuje) | jak 2 | AC-2 · decyzja (tempo) |
| 4 | **Nazwisko rodowe** — etykieta „Nazwisko rodowe (z domu)” | pole tekstowe, wielka litera na początku słów | `next` | pusto | — | AC-2 · [[FR-005-nazwisko-rodowe]] |
| ~~4a~~ | ~~**Płeć**~~ — **nie wchodzi** (v5.1, decyzja autora na stopie #1 ISSUE-019: *„nie czuję potrzeby dawania płci”*). W v5 był tu segment „Kobieta · Mężczyzna” podpowiadany z imienia | — | — | — | — | [[rodzina]] → *Open* 2 |
| 5 | **Urodzenie** | blok daty (niżej) | `next` | dopisek „dokładnie”, data pusta | blok daty | AC-3 · [[FR-004-data-z-dopiskiem]] |
| 6 | **Zgon** | blok daty | `next` | jak 5 | jak 5 | AC-3 |
| 7 | ~~**Pochówek** (data pochówku)~~ — **usunięte w v2.2** (decyzja autora, stop #2 ISSUE-012) | — | — | — | — | AC-3 (bez pochówku) |
| 8 | **Kim była** — krótka biografia. Pole wielowierszowe: **3 linie od startu**, rośnie do 6, potem przewija się w środku. Podpowiedź w pustym polu: „Krótka biografia — np. zawód, miejsce, co warto zapamiętać” (tekst pomocniczy, znika przy pisaniu) | pole wielowierszowe, wielka litera na początku zdania | Enter = nowa linia | pusto | — | AC-2 · uwaga autora 4 (biografia) · *Decisions* → „Biografia = „kim była”” |
| ~~9~~ | ~~**Źródło „kim była”**~~ — **usunięte** (v5.4, [[SPIKE-004-mvp-flow-prototype]] D28: bez źródeł w aplikacji) | — | — | — | — | — |
| 9a | **Rodzina** (v5) — **tylko w poprawie**; elementy niżej (*Sekcja „Rodzina”*). Odstęp 24 dp od 9 | sekcja | chip → wpis krewnego; ✎ i przyciski → [[rodzina]] A. **Poza `next`** | — | — | US-003 AC-1, AC-2 · R4 prawy · uwaga autora 2026-10-06 |
| ~~10~~ | ~~**Źródło dat i pochówku**~~ — **usunięte** (v5.4, [[SPIKE-004-mvp-flow-prototype]] D28) | — | — | — | — | — |
| 11 | **Zapisz** | przycisk wypełniony (zaokrąglony prostokąt, ≥ 52 dp), **przypięty na dole, nad klawiaturą**; bez znicza ([[style-b]] reguła 8) | dotknięcie | — | błąd → komunikaty przy polach, fokus i przewinięcie do pierwszego błędu, nic się nie zapisuje | AC-1…AC-4 |

### Blok daty (pola 5, 6, 7)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja |
|---|---|---|---|---|---|
| a | Etykieta: Urodzenie / Zgon / Pochówek | tekst pomocniczy | — | — | — |
| b | **Dopisek** — przycisk z menu: dokładnie · około · przed · po · między. Pokazuje bieżący wybór („dokładnie ▾”); cel dotyku ≥ 48 dp | przycisk + menu | dotknięcie → menu; po wyborze fokus przechodzi do pola daty. **Poza kolejnością `next`**, żeby `next` skakało z daty do daty | „dokładnie” | — |
| c | **Data** | pole tekstowe, **klawiatura numeryczna z separatorem** | `next` | pusto | przyjmuje `rrrr` · `mm.rrrr` · `dd.mm.rrrr`, separatory `.` `-` `/`; rok od 1500 do bieżącego; dzień zgodny z miesiącem. Inaczej: „Nie rozumiem tej daty — wpisz rok, mm.rrrr albo dd.mm.rrrr.” |
| d | **Do** — tylko przy „między”, pojawia się obok pola c | pole jak c | `next` | pusto | wymagane przy „między”; późniejsze niż c: „Druga data musi być późniejsza od pierwszej.” |
| e | **Podgląd** — tekst pomocniczy pod polem: dokładnie tak, jak data pokaże się w [[grob]] (format: [[style-b]] reguła 6): „→ ok. 1890”, „→ między 1893 a 1895”, „→ 14.03.1951” | tekst | — | pusty, gdy nie ma daty | — |

**Pusta data** nie zapisuje nic (brak zdarzenia), a dopisek bez daty jest ignorowany. Zapis „wiem, że nie
wiem” (`UNKNOWN`) to [[US-004-fakt-od-babci]].

**Zapis jest całością:** osoba, pochówek (z twierdzeniem) i każda wpisana data (z twierdzeniem) zapisują
się razem albo wcale. Po błędzie nie zostaje „pół osoby”.

### Sekcja „Rodzina” (9a, v5)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja |
|---|---|---|---|---|---|
| a | **Nagłówek:** `people_outline` (20 dp, akcent) + „Rodzina” (16 sp, półgruby, kolor tekstu) — jak sekcje R4 prawego ([[style-b]] reguła 3: ikona nagłówka sekcji w akcencie) | tekst | — | — | — |
| b | **Grupa „Rodzice”** — gdy osoba jest dzieckiem w jakiejś rodzinie: etykieta „Rodzice” (14 sp, tekst pomocniczy), z prawej ✎ (`edit_outlined`, akcent, cel 48 dp, `tooltip` „Popraw rodzinę”); pod nią chipy rodziców („Rodzic: Józef” · „Rodzic: Zofia”) | grupa | ✎ → [[rodzina]] A, poprawa tej rodziny | — | — |
| ~~c~~ | ~~**Grupa „Rodzeństwo”**~~ — **nie wchodzi** (v5.1, decyzja autora: rodzeństwo pokażą wizualizacje połączeń, EPIC-003) | — | — | — | — |
| d | **Grupa za każdy związek** (osoba w parze), według daty ślubu, a bez daty na końcu, w kolejności zapisu. Etykieta „Związek”, a z datami „Związek · ślub ok. 1948” i „· koniec 1960” (format: [[style-b]] reguła 6); ✎ jak w b. Chipy: druga osoba z pary („Partner: Jan”), potem dzieci tej pary („Dziecko: Stanisław”, „Dziecko: Anna”) **według daty urodzenia**, a bez daty na końcu (v5.1, kanon GEDCOM 7) | grupa | jak b | — | — |
| e | **Chip** — powierzchnia, obrys 1 dp w kolorze obrysu, promień 8 dp, wysokość co najmniej 32 dp — gęstość Material 3 daje ok. 37 dp (cel dotyku 48 dp; przegląd `ui`, v5.2); `person_outline` (18 dp, akcent); napis „Rola: Imię” (14 sp, tekst) — rola z [[rodzina]] → *Role names* (neutralna, v5.1), imię to pierwsze z imion, a bez imion nazwisko. Opis dla czytnika: „Partner: Jan Wymyślony — otwórz wpis”. Chipy zawijają się do kolejnych linii i rosną z tekstem (SC 1.4.4) | chip-przycisk | dotknięcie → wpis tej osoby (poprawa) | — | — |
| f | **Rząd działań:** „Dodaj rodziców” (`group_add_outlined`) — tylko gdy osoba nie ma rodziców; **„Dodaj związek”** (`person_add_alt_outlined`) — zawsze, bo każdy kolejny związek (po rozstaniu albo owdowieniu) to osobna rodzina ze swoimi dziećmi (AC-2). Przyciski z obrysem ([[style-b]] reguła 1), ≥ 52 dp, szerokość treści; gdy dwa nie mieszczą się w linii, drugi schodzi niżej | przyciski | → [[rodzina]] A „nowa rodzina” | — | — |

**Bez rodziny:** sam nagłówek (a) i rząd działań (f). Pusty stan nie potrzebuje zdania: dwa przyciski mówią, co tu
będzie ([[style-b]] reguła 9).

## States
| Stan | Co widać |
|---|---|
| pusty („nowy grób”, „kolejna osoba”) | fokus w „Imiona”, klawiatura otwarta. W „kolejnej osobie” nazwisko podpowiedziane i zaznaczone. Podglądy dat puste |
| błąd | komunikat pod polem w kolorze **błędu** z ikoną `error_outline`, a ramka pola też w kolorze błędu. Kolor nigdy sam: zawsze ikona i tekst (SC 1.4.1) |
| wypełniony | podgląd pod każdą wpisaną datą; przy „między” dwa pola daty |
| poprawa (D1) | wartości wpisane. Data, która ma więcej niż jedno twierdzenie (spór źródeł), jest tylko do odczytu, z dopiskiem „Kilka źródeł — tej daty tu nie poprawisz.” |
| zapisywanie | „Zapisz” nieaktywny przez chwilę zapisu (lokalnie — ułamek sekundy; **z nowymi zdjęciami** dłużej, bo pliki trafiają do magazynu aplikacji — wskaźnik postępu w przycisku zamiast napisu, v3) |
| zdjęcia wybrane (v4) | element 1a pokazuje profilowe i liczbę zdjęć od razu, zanim wpis się zapisze — także po zmianach w [[zdjecia-osoby]]. Pozostałe pola i fokus bez zmian |
| zdjęcia — przygotowanie (v4) | między powrotem z galerii albo aparatu (z 1a bez zdjęć) a pokazaniem: okrąg 1a z obrysem i wskaźnikiem postępu w środku. Przy kilku zdjęciach okrąg pokazuje pierwsze gotowe, a liczba rośnie |
| zdjęcia — błąd (v4) | pod okręgiem 1a zamiast podpisu: `error_outline` + „Nie udało się wczytać zdjęcia. Spróbuj jeszcze raz.” (kolor błędu, 14 sp); przy kilku: „Nie udało się wczytać 1 zdjęcia z 3. Spróbuj jeszcze raz.” — udane zostają. Bez żadnego udanego okrąg wraca do stanu bez zdjęć. Wpis bez zdjęcia da się zapisać |
| nieudany zapis (v2.1) | nad „Zapisz”: `error_outline` + „Nie udało się zapisać. Spróbuj jeszcze raz.” w kolorze błędu; wpis zostaje |
| okno „Odrzucić wpis?” | „Wpisane dane nie zostaną zapisane.” · **„Wróć do wpisu”** (akcent — bezpieczne działanie jest główne) · „Odrzuć” (kolor tekstu) |
| rodzina — brak (v5, poprawa) | 9a: nagłówek i „Dodaj rodziców” · „Dodaj związek” |
| rodzina — wypełniona (v5, poprawa) | 9a: grupy b–d z chipami; „Dodaj rodziców” tylko bez rodziców |
| nowa osoba (v5) | 9a nie ma — sekcja pojawia się w poprawie (arkusz potrzebuje zapisanej osoby, [[rodzina]] D2) |
| poprawa osoby bez grobu (v5) | podtytuł paska „bez grobu w aplikacji”; reszta jak poprawa |

## Sketch
v5.1: „Rodzina” (9a) pod biografią — poprawa osoby z rodzicami i jednym związkiem (bez płci, bez rodzeństwa):
```
│  Źródło: notatki         Zmień   │
│                                  │
│  👥 Rodzina                       │  ← ikona w akcencie
│  Rodzice                      ✎  │
│  (👤 Rodzic: Józef) (👤 Rodzic: Zofia)
│  Związek · ślub ok. 1948      ✎  │
│  (👤 Partner: Jan)                │
│  (👤 Dziecko: Stanisław) (👤 Dziecko: Anna)
│ ┌────────────────────────┐       │
│ │ 👤+ Dodaj związek       │       │  ← „Dodaj rodziców” znika, gdy są
│ └────────────────────────┘       │
│  Daty i miejsce pochówku zapiszą │
│  się ze źródłem: notatki.        │
```

v4: zdjęcia (1a) nad imionami — bez zdjęć po lewej, ze zdjęciami po prawej (profilowe i liczba). Reszta formularza
bez zmian (niżej, z v2).
```
 bez zdjęć                             ze zdjęciami (poprawa)
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│ ←  Osoba w grobie                │  │ ←  Poprawa wpisu                 │
│    Cmentarz Wymyślony · nowy grób│  │    Grób rodzinny Wymyślonych · … │
│              ╭────╮              │  │              ╭────╮              │
│              │ 📷 │              │  │              │▓▓▓▓│ ← profilowe  │
│              ╰────╯              │  │              ╰────╯              │
│          Dodaj zdjęcie           │  │            3 zdjęcia  ← do bazy  │
│ ┌ Imiona ──────────────────────┐ │  │ ┌ Imiona ──────────────────────┐ │
│ │ ▌                            │ │  │ │ Anna                         │ │
```

v2 (bez zdjęcia):
```
┌──────────────────────────────────┐
│ ←  Osoba w grobie                │
│    Cmentarz Wymyślony · nowy grób│
│                                  │
│ ┌ Imiona ──────────────────────┐ │
│ │ Jan▌                         │ │  ← fokus: ramka w akcencie
│ └──────────────────────────────┘ │
│ ┌ Nazwisko ────────────────────┐ │
│ │ Wymyślony                    │ │
│ └──────────────────────────────┘ │
│ ┌ Nazwisko rodowe (z domu) ────┐ │
│ └──────────────────────────────┘ │
│  Urodzenie                       │
│ ┌──────────┐ ┌─────────────────┐ │
│ │ około  ▾ │ │ 1890            │ │
│ └──────────┘ └─────────────────┘ │
│  → ok. 1890                      │
│  Zgon                            │
│ ┌──────────┐ ┌─────────────────┐ │
│ │dokładnie▾│ │ 14.03.1951      │ │
│ └──────────┘ └─────────────────┘ │
│  → 14.03.1951                    │
│  Pochówek                        │
│ ┌──────────┐ ┌──────┐ ┌───────┐  │
│ │ między ▾ │ │ 1951 │ │ do …  │  │  ← „między”: drugie pole
│ └──────────┘ └──────┘ └───────┘  │
│ ┌ Kim była ────────────────────┐ │
│ │ Kowal, prowadził kuźnię przy │ │  ← 3 linie od startu,
│ │ drodze do Miejscowości       │ │    rośnie do 6
│ │ Testowej.                    │ │
│ └──────────────────────────────┘ │
│  Źródło: notatki         Zmień   │
│                                  │
│  Daty i miejsce pochówku zapiszą │
│  się ze źródłem: notatki.        │
│ ┌──────────────────────────────┐ │
│ │            Zapisz            │ │  ← akcent, nad klawiaturą
│ └──────────────────────────────┘ │
└──────────────────────────────────┘
```

## Tempo
**Typowa osoba z notatek:** imię, nazwisko jak u poprzedniej osoby w grobie, rok urodzenia, pełna data
zgonu, bez daty pochówku, krótkie „kim była”.

| Krok | Akcje poza pisaniem |
|---|---|
| „Dodaj osobę” w [[grob]] (pierwsza osoba: „Dodaj grób” w [[cmentarz]]) | 1 dotknięcie |
| Imiona → `next` | 1 |
| Nazwisko (podpowiedziane) → `next` | 1 |
| Nazwisko rodowe (puste) → `next` | 1 |
| Urodzenie: rok → `next` (klawiatura numeryczna sama) | 1 |
| Zgon: data → `next` (do „Kim była”, klawiatura tekstowa sama) | 1 |
| Kim była | 0 |
| Zapisz | 1 |
| **Razem** | **7 akcji, 0 ręcznych zmian klawiatury, 0 pytań o źródło** (v2.2; było 8 z „Pochówkiem”) |

- Dopisek inny niż „dokładnie”: **+2 dotknięcia** (menu, wybór). „Między”: +2 i drugie pole.
- Na całe notatki (ok. 100 osób): **ok. 700 akcji** plus pisanie.
- **Zdjęcia osoby (v4): +4 dotknięcia** przy pierwszym zdjęciu (1a, „Wybierz z galerii”, wybór, „Gotowe” — okno
  systemowe na Androidzie 16, [[zdjecie]] v1.2), +1 na każde kolejne wybrane naraz; dalsze działania na bazie —
  [[zdjecia-osoby]] → *Tempo*. Tylko gdy osoba ma zdjęcie. Bez zdjęcia **+0**: element 1a stoi poza `next`, a fokus od wejścia dalej trafia w „Imiona”. Koszt v3 bez zdjęcia
  to tylko ok. 128 dp wysokości nad polami (okrąg 80, podpis, odstęp 24). Na emulatorze `Medium_Phone` przy otwartej
  klawiaturze „Imiona” i „Nazwisko” dalej widać, a pole w fokusie i tak przewija się do widoku (sprawdza przegląd
  `ui` przed stopem #2).
- **Rodzina (9a, v5): +0 w formularzu** — sekcji nie ma przy nowej osobie, a w poprawie stoi poza `next`. Koszt
  rodziny liczy [[rodzina]] → *Tempo*.
- **Co skraca:** podpowiedziane nazwisko, klawiatura dobrana do pola, źródło domyślne bez pytania, brak
  wyboru statusu, przycisk „Zapisz” zawsze nad klawiaturą.
- **Co wydłuża świadomie:** `next` przez puste „Nazwisko rodowe”. Pole wymaga FR-005; zwijanie pustych pól
  kosztowałoby jego odkrywanie. „Pochówek” usunięty w v2.2 (decyzja autora).

## Style B rules applied
- Reguła 1: jedyny wypełniony przycisk to „Zapisz”. Fokus pola i zaznaczony dopisek w menu są w akcencie,
  bo to stan. Przycisk dopisku ma obrys.
- Reguła 4: tytuł paska półgruby.
- Reguła 8: znicza tu nie ma — formularz to działanie, nie miejsce pamięci.
- Reguła 3: ikona błędu `error_outline`.
- Reguła 6: formaty dat w podglądzie są takie same jak w [[grob]].
- Reguła 7: komunikaty spokojne i rzeczowe; okno odrzucenia bez straszenia.
- Reguła 10: zapis kończy się widokiem grobu, bez okienka „Zapisano”.
- Tekst wpisywany ≥ 16 sp.
- **Reguły 11 i 14 (v3, v4):** profilowe w okręgu (osoba), liczba zdjęć pod nim w tekście pomocniczym, nie na
  zdjęciu. Puste zdjęcie to przycisk (obrys 3,40:1 na tle — SC 1.4.11 ✅, ikona w akcencie,
  podpis), a nie zastępczy obrazek ani sylwetka. Bez bursztynowego pierścienia z R4 prawego: tam to widok osoby
  (M5), a tu formularz; pierścień w akcencie byłby dekoracją (reguła 1).
- **Rodzina (v5, [[style-b]] v1.11):**
  - nagłówek sekcji z ikoną w akcencie (reguła 3, R4);
  - chipy relacji prowadzą do wpisu krewnego **bez chevronu** — wyjątek od reguły 11 z R4 prawego;
  - ✎ jak w [[grob]] element 3.
  
  Tokeny bez zmian: obrys chipu na tle 3,40:1, napis na powierzchni 10,02:1, akcent na tle 8,81:1.
- **Nowe tokeny** (proponowane; `dev` wpisuje je do `theme.dart` w ISSUE-012, a [[style-b]] ma już ich role):

  | Rola | Proponowana wartość | Pomiar (tło / powierzchnia) | Próg |
  |---|---|---|---|
  | `outline` — ramka pola w spoczynku, linia podziału | `#6B6862` | 3,40 / 3,10 | ≥ 3 (SC 1.4.11) ✅ |
  | `error` — komunikat błędu, jego ikona i ramka pola z błędem | `#E07A6F` | 6,45 / 5,89 | ≥ 4,5 (SC 1.4.3) ✅ |

  Pola mają ramkę (`outlined`) na tle, bez wypełnienia: różnica tło–powierzchnia ma ok. 1,1:1, więc granicę
  pola musi nieść ramka.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-002 AC-1 | 11 → [[grob]]; tryb „kolejna osoba” | każda zapisana osoba wraca w widoku grobu obok poprzednich |
| US-002 AC-2 | 2, 3, 4, 8 | imiona, nazwisko, osobno nazwisko rodowe i „kim była” do wpisania; po zapisie imiona, nazwisko i „z d.” w [[grob]] |
| US-002 AC-3 | 5–7 (b, c, d, e) | pięć dopisków do wyboru; podgląd pokazuje datę z dopiskiem przed zapisem, [[grob]] po zapisie |
| US-002 AC-4 | 9, 10 | daty i pochówek zapisują się ze źródłem „notatki” i statusem `CLAIMED` bez pytania; „kim była” ma linię źródła, domyślnie „notatki” |
| ISSUE-012: styl B | całość | reguły i nowe tokeny wyżej; przegląd `ui` |
| US-005 AC-1 (v3) | 1a → [[zdjecie]] A | zdjęcie z galerii albo aparatu widać w okręgu, a po „Zapisz” — w karcie osoby w [[grob]] |
| US-005 AC-2 (v3) | 1a | w poprawie zdjęcie widać dalej po usunięciu oryginału z galerii |
| ISSUE-016: styl B | 1a | reguły 11 i 14; przegląd `ui` |
| ISSUE-017: kilka zdjęć, profilowe (v4) | 1a → [[zdjecia-osoby]] | okrąg pokazuje profilowe, podpis — liczbę zdjęć; po „Ustaw jako profilowe” i powrocie okrąg się zmienia |
| ISSUE-017: zapis zdjęć z wpisem (v4) | 1a, 11 | zmiany zdjęć widać w 1a przed zapisem; po „Zapisz” są w [[grob]] (miniatura), po „Odrzuć” — nie ma ich |
| US-003 AC-1 (v5) | 9a f → [[rodzina]] | po zapisie arkusza para i dzieci są w sekcji jako chipy |
| US-003 AC-2 (v5) | 9a d, f | „Dodaj związek” przy osobie, która ma już związek; dwie grupy „Związek”, każda ze swoimi dziećmi |
| US-003 AC-3 (v5) | 9a d | data ślubu i końca z dopiskiem w etykiecie grupy |
| US-003: relacje przy osobie (v5.1) | 9a e | chipy „Rodzic”, „Partner”, „Dziecko”; po zmianie imienia krewnego w jego wpisie chip pokazuje nowe imię |
| ISSUE-012: zapis zamawia kopię w tle | 11 | n/a dla wyglądu. Zapis idzie przez API danych (`claims.dart`, drift), więc kopię zamawia sam `grobing_app.dart` (`watchChanges`). Sprawdza `qa` ISSUE-012 |

## Decisions
| Decyzja | Dlaczego | Obali |
|---|---|---|
| **Grób powstaje z pierwszą osobą** | grób z notatek = cmentarz + osoby (US-002); pusty grób nie ma po co istnieć | potrzeba grobu bez osób ([[cmentarz]] → *Decisions*) |
| **Po zapisie zawsze widok grobu**, bez przycisku „Zapisz i dodaj następną” | widać, co się zapisało, i łatwo porównać z notatką; mniej przycisków. Koszt: +1 dotknięcie na osobę poza pierwszą, ok. 50 na całe notatki (ok. 2 osoby na grób) | autor na stopie #2 czuje, że powrót do grobu spowalnia → drugi przycisk |
| **Nazwisko podpowiedziane i zaznaczone** | w grobie rodzinnym nazwisko zwykle się powtarza; zaznaczenie sprawia, że inne nazwisko po prostu się wpisuje, bez kasowania | podpowiedź myli (np. groby kilku rodzin) |
| **Dopisek jako przycisk z menu**, nie pięć przycisków w rzędzie | trzy rzędy po pięć przycisków to szum na ekranie, który ma być minimalny. Koszt: 2 dotknięcia zamiast 1, tylko przy dacie innej niż „dokładnie” | w notatkach przeważają daty przybliżone → segmenty albo rozpoznanie „ok.” wpisanego w polu |
| **Jedno pole daty z klawiaturą numeryczną**, nie kalendarz ani trzy pola | kalendarz nie umie „ok. 1890”, a trzy pola to trzy `next`. Kanon: GEDCOM 7 §2.4 — data ma modyfikator (`ABT` · `BEF` · `AFT` · `BET … AND`) i dokładność od roku do dnia (cytowane w [[ISSUE-011-schema-v2-assertions]] → *Prior art*) | — |
| **Podgląd pod datą** | dopisek i format widać przed zapisem, więc literówka w roku wychodzi od razu | — |
| **Źródło pokazane, nie pytane** | FR-001, decyzja kosztowa: źródło przy każdym polu spowolniłoby ok. 100 wpisów | — |
| **Statusu twierdzenia nie pokazujemy** | przy przepisywaniu zawsze `CLAIMED` z notatek; słowo nic tu nie daje. Status zobaczy się przy sporze (US-004) | — |
| **Rok od 1500 do bieżącego** | łapie literówkę typu „190” zamiast „1890”; dolna granica z zapasem | wpis sprzed 1500 (przy grobach nieprawdopodobny) |
| **Bez usuwania osoby** | brief G7/C5 („Undo / no silent deletion”, Could) czeka na osobną decyzję; dane są niezastąpione | — |
| **Biografia = „kim była”** (v2) | autor chciał krótkiej biografii i zgodził się, że to dzisiejsze „kim była” z linią źródła (decyzja 2026-10-06). Etykieta zostaje słowem z US-002 AC-2, a podpowiedź mówi, że to biografia. Większe pole (3 linie) zaprasza do dwóch-trzech zdań, jak w R4 prawym. Jedna linia źródła na cały tekst (FR-001, decyzja kosztowa). Biografię pokaże widok osoby (M5); do tego czasu widać ją w poprawie wpisu albo w karcie grobu ([[grob]] D3) | autor chce osobnych pól (zawód, miejsce) — wtedy to osobna pozycja ze zmianą schematu |
| **Zdjęcie i relacje później** (v2) | brakowało ich autorowi, ale należą do [[US-005-zdjecia]] i [[US-003-przepisanie-rodziny]] (kolejność autora 2026-10-06). Miejsce, żeby kolejne pozycje nie przestawiały formularza: **portret na górze**, przed imionami (jak w R4 prawym) — dotknięcie dodaje zdjęcie, a pusty stan to ikona z podpisem, bez sylwetki; **„Rodzina” pod biografią**, przed linią źródła dat — chipy relacji jak w R4. Bez miejsc zastępczych w ISSUE-012. **v5:** relacje wpisuje się arkuszem ([[rodzina]]), a w formularzu je widać (9a) — warunek obalający trafił w połowie: do formularza nie trafia **wpisywanie**, trafia **widok** | US-003 wpisuje rodzinę naraz, w arkuszu rodziny (brief: *family group sheet*) — wtedy relacje nie trafiają do formularza osoby |
| **D-rodzina-1 — „Rodzina” tylko w poprawie** (v5) | arkusz zapisuje się sam i wskazuje „tę osobę”, więc osoba musi być zapisana; nowa osoba nie ma jeszcze relacji do pokazania ([[rodzina]] D2) | autor chce dodać rodzinę zaraz przy nowej osobie → „Zapisz i dodaj rodzinę” |
| **D-rodzina-2 — chip prowadzi do wpisu krewnego**, nie do arkusza (v5) | osoba dodana arkuszem bez grobu nie ma innego wejścia do swojego wpisu (daty, zdjęcia); rodzinę poprawia ✎ przy grupie. Formularz pod spodem zostaje z danymi, więc chip nie wymaga okna „Odrzucić wpis?” | autor gubi się w wpisach położonych jeden na drugim (wstecz przez kilka osób) |
| ~~**D-płeć — segment pod nazwiskiem rodowym, poza `next`, podpowiedziany z imienia** (v5)~~ — **odrzucone na stopie #1** (v5.1: bez płci) | nazwy relacji jak w R4 bez dodatkowej akcji przy trafnej podpowiedzi; poza `next`, więc tempo wpisu bez zmian; podpowiedź widać przed zapisem. Poprawa nie podpowiada, bo poprawa nie zmienia niczego sama | autor wybiera na stopie #1 wariant P1' albo P2 ([[rodzina]] → *Open* 2) albo złe podpowiedzi zdarzają się częściej niż przy imionach męskich na „-a” |
| ~~**D-zdjęcie-1 — jedno zdjęcie na osobę** (v3)~~ — **nieaktualne:** decyzja autora na stopie #1 ISSUE-016 — baza zdjęć osoby z „profilowym” ([[ISSUE-017-person-photos]]) | R4 prawy pokazuje jeden portret, a karta w [[grob]] ma miejsce na jedną miniaturę. Kilka zdjęć osoby (np. z różnych lat) to treść widoku osoby (M5), którego jeszcze nie ma | autor przy przepisywaniu chce dołączyć do osoby kilka zdjęć — wtedy galeria w widoku osoby (M5), nie w formularzu |
| **D-zdjęcie-2 — zdjęcia zapisują się z „Zapisz”**, a nie od razu (v3; **v4: wszystkie zmiany bazy zdjęć**) | „zapis jest całością” (v2): osoba i jej zdjęcia powstają razem albo wcale, a „Odrzuć” cofa także zdjęcia. v4: to samo dotyczy zmian w [[zdjecia-osoby]] i [[zdjecie]] (tryb osoby) — dodania, profilowego, osób na zdjęciu (także łączy **innych** osób) i usunięcia z osoby; ten sam przepływ działa przy nowej osobie, której jeszcze nie ma w bazie ([[zdjecia-osoby]] D1). Inaczej niż w [[grob]], gdzie zdjęcie nagrobka zapisuje się od razu — tam nie ma formularza, który by je zatwierdził | autor gubi zmiany zdjęć albo czuje dwie zasady (nagrobek od razu, osoba z „Zapisz”) — [[zdjecia-osoby]] D1 |
| **D-zdjęcie-4 — baza zdjęć na osobnym ekranie, wejście z 1a** (v4) | formularz to ok. 100 wpisów, a większość osób z notatek zdjęć nie ma: galeria w formularzu zabierałaby miejsce przy każdym wpisie. Okrąg z profilowym i liczbą mówi, że zdjęcia są i ile; siatka potrzebuje szerokości ekranu. Ten sam ekran przyjmie widok osoby (M5) | autor przy poprawie chce widzieć wszystkie zdjęcia w formularzu → pasek miniatur pod 1a |
| ~~**D-zdjęcie-3 — bez kadrowania** (v3)~~ — **obalone** na stopie #2 ISSUE-017 (uwaga autora o zdjęciu grupowym) → [[kadr-profilowego]], [[ISSUE-018-profile-photo-crop]] | wybrane zdjęcie przycina się do okręgu ze środka; całość widać w podglądzie. Twarz ze zdjęcia grupowego wymagałaby kadrowania, które jest poza zakresem ([[ISSUE-016-photos-grave-and-person]] → *Out of Scope*) | na stopie #2 środek zdjęcia nie trafia w twarz na typowych starych zdjęciach — wtedy kadrowanie jako osobna pozycja |

## Open
**v5 — trzy pytania na stopie #1 [[ISSUE-019-family-relations]] — rozstrzygnięte 2026-10-07** ([[rodzina]] → *Open*):
1. droga wejścia relacji → **C** (widok w 9a, wpisywanie arkuszem);
2. płeć osoby → **bez płci** (4a nie wchodzi);
3. rodzeństwo w 9a → **nie**.

v3: zdjęcie osoby — **przeprojektowane w v4** (baza zdjęć: [[zdjecia-osoby]]; dzielenie i profilowe: [[zdjecie]] v1.3).
Na stopie #1 ISSUE-017: [[zdjecie]] D7 (kogo da się zaznaczyć na zdjęciu) — rekomendacja, nie luka.

Rozstrzygnięte w wersji 2.1:
1. **Poprawa wpisu** — wchodzi minimum (stop #1 ISSUE-012, D1): ten sam formularz w trybie „poprawa”, wartości
   poprawiane w miejscu, data z więcej niż jednym twierdzeniem tylko do odczytu.
2. **Klawiatura daty** — `TextInputType.datetime` (zmierzone na emulatorze, Gboard). `numberWithOptions(decimal:
   true)` odpada: przy polskim układzie dałby przecinek.

**Do odczucia na stopie #2** (*Decisions* → „Nazwisko podpowiedziane”): przy parach -ski/-ska i -ny/-na zaznaczona
podpowiedź wymaga przepisania całego nazwiska. Jeśli to przeszkadza — kursor na końcu zamiast zaznaczenia.
