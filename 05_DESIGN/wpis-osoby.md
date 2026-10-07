---
screen: "Wpis osoby w grobie — formularz"
items: ["[[ISSUE-012-transcribe-grave-screen]]"]
us: "[[US-002-przepisanie-grobu]]"
journey-step: "n/a — M1 (warunek kroku 1 UJ-001)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-cmentarz-grob-osoba.html (ramki 3–4)"
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

## Purpose
Wpisanie jednej osoby pochowanej w grobie, tak jak stoi w notatkach: imiona, nazwisko, nazwisko rodowe,
daty urodzenia, zgonu i pochówku z dopiskiem oraz **krótka biografia („kim była”)** z linią źródła. To
**najczęściej używany ekran przepisywania — ok. 100 razy** (G6), więc jego miarą jest koszt jednego wpisu.

## Navigation
- Z [[cmentarz]] → „Dodaj grób” → tryb **„nowy grób”**. Zapis tworzy grób i osobę razem.
- Z [[grob]] → „Dodaj osobę” → tryb **„kolejna osoba”**.
- Z [[grob]] → dotknięcie osoby → tryb **„poprawa”** (ISSUE-012, D1).
- **Zapis → [[grob]]**, który zastępuje formularz na stosie (wstecz z grobu wraca do cmentarza).
- **Wstecz z wpisanymi danymi** (przycisk albo gest) → okno „Odrzucić wpis?”. Bez wpisanych danych →
  od razu wstecz.

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek: „Osoba w grobie” (w poprawie: „Poprawa wpisu”); podtytuł (tekst pomocniczy, jedna linia): w trybie „nowy grób” — „Cmentarz Wymyślony · nowy grób”; w trybie „kolejna osoba” i w poprawie — nazwa grobu, a bez nazwy nazwa cmentarza, i „· w grobie: 2 osoby” | tytuł | — | — | — | decyzja projektowa · [[grob]] D1 |
| 2 | **Imiona** | pole tekstowe, wielka litera na początku słów | `next`; **fokus i klawiatura od razu po wejściu** w trybach „nowy grób” i „kolejna osoba”; w poprawie bez fokusu (v2.1) | pusto | imiona albo nazwisko, co najmniej jedno: „Podaj imiona albo nazwisko.” | AC-2 |
| 3 | **Nazwisko** | pole tekstowe, wielka litera na początku słów | `next` | w trybie „kolejna osoba”: nazwisko ostatnio wpisanej osoby w tym grobie, **zaznaczone** (pisanie je zastępuje) | jak 2 | AC-2 · decyzja (tempo) |
| 4 | **Nazwisko rodowe** — etykieta „Nazwisko rodowe (z domu)” | pole tekstowe, wielka litera na początku słów | `next` | pusto | — | AC-2 · [[FR-005-nazwisko-rodowe]] |
| 5 | **Urodzenie** | blok daty (niżej) | `next` | dopisek „dokładnie”, data pusta | blok daty | AC-3 · [[FR-004-data-z-dopiskiem]] |
| 6 | **Zgon** | blok daty | `next` | jak 5 | jak 5 | AC-3 |
| 7 | ~~**Pochówek** (data pochówku)~~ — **usunięte w v2.2** (decyzja autora, stop #2 ISSUE-012) | — | — | — | — | AC-3 (bez pochówku) |
| 8 | **Kim była** — krótka biografia. Pole wielowierszowe: **3 linie od startu**, rośnie do 6, potem przewija się w środku. Podpowiedź w pustym polu: „Krótka biografia — np. zawód, miejsce, co warto zapamiętać” (tekst pomocniczy, znika przy pisaniu) | pole wielowierszowe, wielka litera na początku zdania | Enter = nowa linia | pusto | — | AC-2 · uwaga autora 4 (biografia) · *Decisions* → „Biografia = „kim była”” |
| 9 | **Źródło „kim była”** — linia pod polem 8: „Źródło: notatki” (tekst pomocniczy) + „Zmień” | tekst + dotknięcie; „Zmień” odsłania jedno pole tekstowe w tym miejscu | dotknięcie | „notatki” | niepuste, gdy „kim była” jest wypełnione: „Podaj źródło — kto to powiedział albo skąd to wiesz.” | AC-4 · [[FR-001-provenance]] |
| 10 | **Źródło dat i pochówku** — stały tekst pomocniczy nad przyciskiem: „Daty i miejsce pochówku zapiszą się ze źródłem: notatki.” | tekst | — | źródło „notatki”, status `CLAIMED` (statusu nie pokazujemy) | — | AC-4 · FR-001 (decyzja kosztowa: bez pytania przy każdym polu) |
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

## States
| Stan | Co widać |
|---|---|
| pusty („nowy grób”, „kolejna osoba”) | fokus w „Imiona”, klawiatura otwarta. W „kolejnej osobie” nazwisko podpowiedziane i zaznaczone. Podglądy dat puste |
| błąd | komunikat pod polem w kolorze **błędu** z ikoną `error_outline`, a ramka pola też w kolorze błędu. Kolor nigdy sam: zawsze ikona i tekst (SC 1.4.1) |
| wypełniony | podgląd pod każdą wpisaną datą; przy „między” dwa pola daty |
| poprawa (D1) | wartości wpisane. Data, która ma więcej niż jedno twierdzenie (spór źródeł), jest tylko do odczytu, z dopiskiem „Kilka źródeł — tej daty tu nie poprawisz.” |
| zapisywanie | „Zapisz” nieaktywny przez chwilę zapisu (lokalnie — ułamek sekundy) |
| nieudany zapis (v2.1) | nad „Zapisz”: `error_outline` + „Nie udało się zapisać. Spróbuj jeszcze raz.” w kolorze błędu; wpis zostaje |
| okno „Odrzucić wpis?” | „Wpisane dane nie zostaną zapisane.” · **„Wróć do wpisu”** (akcent — bezpieczne działanie jest główne) · „Odrzuć” (kolor tekstu) |

## Sketch
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
| **Zdjęcie i relacje później** (v2) | brakowało ich autorowi, ale należą do [[US-005-zdjecia]] i [[US-003-przepisanie-rodziny]] (kolejność autora 2026-10-06). Miejsce, żeby kolejne pozycje nie przestawiały formularza: **portret na górze**, przed imionami (jak w R4 prawym) — dotknięcie dodaje zdjęcie, a pusty stan to ikona z podpisem, bez sylwetki; **„Rodzina” pod biografią**, przed linią źródła dat — chipy relacji jak w R4. Bez miejsc zastępczych w ISSUE-012 | US-003 wpisuje rodzinę naraz, w arkuszu rodziny (brief: *family group sheet*) — wtedy relacje nie trafiają do formularza osoby |

## Open
brak. Rozstrzygnięte w wersji 2.1:
1. **Poprawa wpisu** — wchodzi minimum (stop #1 ISSUE-012, D1): ten sam formularz w trybie „poprawa”, wartości
   poprawiane w miejscu, data z więcej niż jednym twierdzeniem tylko do odczytu.
2. **Klawiatura daty** — `TextInputType.datetime` (zmierzone na emulatorze, Gboard). `numberWithOptions(decimal:
   true)` odpada: przy polskim układzie dałby przecinek.

**Do odczucia na stopie #2** (*Decisions* → „Nazwisko podpowiedziane”): przy parach -ski/-ska i -ny/-na zaznaczona
podpowiedź wymaga przepisania całego nazwiska. Jeśli to przeszkadza — kursor na końcu zamiast zaznaczenia.
