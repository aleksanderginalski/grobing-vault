---
screen: "Wpis osoby w grobie — formularz"
items: ["[[ISSUE-012-transcribe-grave-screen]]"]
us: "[[US-002-przepisanie-grobu]]"
journey-step: "n/a — M1 (warunek kroku 1 UJ-001)"
mockup: "katalog tymczasowy sesji 2026-10-06: makieta-przepisanie-grobu.html (ramki 5, 6, 8)"
updated: 2026-10-06
---

# Wpis osoby — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]]. Referencja: formularza nie ma w [[references]]
> (R1–R4), więc ekran dziedziczy reguły stylu B i formę kart i przycisków z R4.

## Purpose
Wpisanie jednej osoby pochowanej w grobie, tak jak stoi w notatkach: imiona, nazwisko, nazwisko rodowe,
daty urodzenia, zgonu i pochówku z dopiskiem oraz „kim była” z linią źródła. To **najczęściej używany ekran
przepisywania — ok. 100 razy** (G6), więc jego miarą jest koszt jednego wpisu.

## Navigation
- Z [[cmentarz]] → „Dodaj grób” → tryb **„nowy grób”**. Zapis tworzy grób i osobę razem.
- Z [[grob]] → „Dodaj osobę” → tryb **„kolejna osoba”**.
- Z [[grob]] → dotknięcie osoby → tryb **„poprawa”** — tylko jeśli wejdzie (*Open* 1).
- **Zapis → [[grob]]**, który zastępuje formularz na stosie (wstecz z grobu wraca do cmentarza).
- **Wstecz z wpisanymi danymi** (przycisk albo gest) → okno „Odrzucić wpis?”. Bez wpisanych danych →
  od razu wstecz.

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek: „Osoba w grobie” (w poprawie: „Poprawa wpisu”); podtytuł: „Cmentarz Wymyślony · nowy grób” albo „· w grobie: 2 osoby” | tytuł | — | — | — | decyzja projektowa |
| 2 | **Imiona** | pole tekstowe, wielka litera na początku słów | `next`; **fokus i klawiatura od razu po wejściu** | pusto | imiona albo nazwisko, co najmniej jedno: „Podaj imiona albo nazwisko.” | AC-2 |
| 3 | **Nazwisko** | pole tekstowe, wielka litera na początku słów | `next` | w trybie „kolejna osoba”: nazwisko ostatnio wpisanej osoby w tym grobie, **zaznaczone** (pisanie je zastępuje) | jak 2 | AC-2 · decyzja (tempo) |
| 4 | **Nazwisko rodowe** — etykieta „Nazwisko rodowe (z domu)” | pole tekstowe, wielka litera na początku słów | `next` | pusto | — | AC-2 · [[FR-005-nazwisko-rodowe]] |
| 5 | **Urodzenie** | blok daty (niżej) | `next` | dopisek „dokładnie”, data pusta | blok daty | AC-3 · [[FR-004-data-z-dopiskiem]] |
| 6 | **Zgon** | blok daty | `next` | jak 5 | jak 5 | AC-3 |
| 7 | **Pochówek** (data pochówku) | blok daty | `next` | jak 5 | jak 5 | AC-3 |
| 8 | **Kim była** | pole wielowierszowe, wielka litera na początku zdania | Enter = nowa linia | pusto | — | AC-2 |
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
| poprawa (*Open* 1) | wartości wpisane. Data, która ma więcej niż jedno twierdzenie (spór źródeł), jest tylko do odczytu, z dopiskiem „Kilka źródeł — tej daty tu nie poprawisz.” |
| zapisywanie | „Zapisz” nieaktywny przez chwilę zapisu (lokalnie — ułamek sekundy) |
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
│ │ Kowal, prowadził kuźnię…     │ │
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
| Zgon: data → `next` | 1 |
| Pochówek (pusty) → `next` (klawiatura tekstowa sama) | 1 |
| Kim była | 0 |
| Zapisz | 1 |
| **Razem** | **8 akcji, 0 ręcznych zmian klawiatury, 0 pytań o źródło** |

- Dopisek inny niż „dokładnie”: **+2 dotknięcia** (menu, wybór). „Między”: +2 i drugie pole.
- Na całe notatki (ok. 100 osób): **ok. 800 akcji** plus pisanie.
- **Co skraca:** podpowiedziane nazwisko, klawiatura dobrana do pola, źródło domyślne bez pytania, brak
  wyboru statusu, przycisk „Zapisz” zawsze nad klawiaturą.
- **Co wydłuża świadomie:** `next` przez puste „Nazwisko rodowe” i „Pochówek”. Te pola wymagają FR-005 i
  AC-3; zwijanie pustych pól kosztowałoby ich odkrywanie.

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

## Open
1. ⚠️ **OPEN — poprawa wpisu** (ISSUE-012 → *Out of Scope*: decyduje `planning` na stopie #1 ISSUE-012).
   - **Rekomendacja `ui`: wchodzi minimum.** Ten sam formularz w trybie „poprawa”, po dotknięciu osoby w
     [[grob]]. Zmiana poprawia wartość w miejscu: literówka przy przepisywaniu to błąd tego samego źródła,
     a nie drugie źródło (ADR-006 rozdziela wartości z **różnych** źródeł). Data z więcej niż jednym
     twierdzeniem jest tylko do odczytu.
   - **Dlaczego:** przy ok. 100 wpisach literówka jest pewna, a bez poprawy zostaje w niezastąpionych
     danych na zawsze.
   - **Jeśli nie wejdzie:** znika tryb „poprawa” i dotknięcie osoby w [[grob]], a [[grob]] pokazuje
     pierwszą linijkę „kim była” (inaczej nie byłoby jej nigdzie widać).
2. **Do zmierzenia przez `dev`** (technika, nie decyzja produktowa): który typ klawiatury Androida daje
   cyfry i separator bez przełączania (`TextInputType.datetime` albo `numberWithOptions(decimal: true)`).
   Wynik trafia do *Dev report*, a jeśli zmienia kształt pola, wraca tutaj. Parser i tak przyjmuje `.`,
   `-` i `/`.
