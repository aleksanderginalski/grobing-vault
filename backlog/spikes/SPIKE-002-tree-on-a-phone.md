---
title: "SPIKE-002 — Is a family tree with in-laws and remarriages readable on a phone?"
type: spike
status: done
priority: MUST
time-box: "1-2 days"
hypotheses: [H4]
blocks: "MVP done (view 5, M9-M11) — not the use of views 1-4"
quality-verdict: APPROVED
verdict-date: 2026-10-13
verdict-reviewer: self-check
created: 2026-10-05
updated: 2026-10-13
---

# SPIKE-002 — Tree on a phone (S-TREE)

## The question
**Czy graf rodziny ~100 osób z powinowatymi i powtórnymi małżeństwami da się czytelnie pokazać na
ekranie telefonu — i jakim układem?**

## Why it matters
To główne ryzyko budowy (H4) i jedyna rzecz, od której zależy **ogłoszenie gotowego MVP** (widok 5
trafił do Must z wyboru autora). Narzędzia genealogiczne pokazują zwykle przodków albo potomków, a nie
„wszystkich" — nie bez powodu.

## Steps
1. Wygeneruj **wymyślony** zbiór ~100 osób o strukturze podobnej do realnej (powinowaci, 2-3 powtórne
   małżeństwa, kilka pokoleń) — **żadnych prawdziwych danych**.
2. 2-3 podejścia: biblioteka układu grafu we Flutterze · widok wycinkowy (rodzina + 1 pokolenie w górę
   i w dół, przewijany) · widok „od osoby" z rozwijaniem.
3. Oceń na prawdziwym telefonie autora: czy da się odpowiedzieć na „kim jest X dla Y" w < 30 s.

## Input from SPIKE-004 (2026-10-08)
- **Kierunek autora na prototypie** ([[drzewo]] v1.1): drzewo **od osoby** z przestawianiem środka (kandydat 3 z kroku 2),
  poziomy połączeń, kolory linii rodzic–dziecko i partnerzy, czas (pojawianie przy narodzinach, łączenie przy związku),
  „Połącz dwie osoby” na drzewie z animacją. Spike sprawdza teraz **czytelność tego kierunku przy ok. 100 osobach**.
- **Do pokazania jako kandydaci** (retro 2, R6): sterowanie poziomami bez przycisków − / + (np. oddalanie odsłania dalszą
  rodzinę — [[drzewo]] *Open* 1) i tryb prezentacji na telewizor (*Open* 2).
- **Dane do spike'a:** wymyślona rodzina o kształcie prawdziwej (ok. 100 osób, powinowaci, związki „razem” i małżeństwa),
  zostaje w buildzie debug jako dane do oceny „feelingu” (propozycja z sesji `/pm` 2026-10-08).

## Input from ISSUE-024 (2026-10-12, `docs` przy zamknięciu)
- **Słownik nazw złożonych przechodzi do drzewa** (decyzja autora na stopie #1 [[ISSUE-024-person-view]], runda 1: *„przypadki np.
  Brat stryjeczny prababki lub podobne zrobimy w widoku drzewa przy łączeniu różnych osób”*). Kanon i tabela nazw —
  [[ISSUE-025-gender-kinship-together-since]] → *Prior art* i D2; widok osoby pokazuje tylko łańcuch z relacjami jednego kroku
  ([[osoba]] D13'). Pozycja drzewa dostaje **dawne AC-6 ISSUE-024**: *Given ścieżka Ja → rodzic (mężczyzna) → jego rodzic → jego
  córka Then nazwa to „ciotka”; brat ojca — „stryj”, brat matki — „wuj”; dziecko siostry ojca — „brat/siostra cioteczna”
  (słownik ze źródłem)* — w banerze „Połącz dwie osoby” ([[drzewo]] D6) i w karcie osoby w środku drzewa.
- **Ścieżka już jest:** `grobing-code/lib/data/kinship.dart` (`KinGraph.path` — najkrótsza, mniej „para”, niższe `id`) z testami.
- **Mini-drzewo w widoku osoby** (jeden poziom, `mini_tree.dart`) ma układ dla dwóch związków i przewijanie w bok ([[osoba]] D12)
  — do porównania z kierunkiem spike'a.
- „Pokaż w drzewie” w widoku osoby czeka na pozycję drzewa ([[osoba]] D11).

## Exit criterion
Wybrane podejście → notatka/ADR; albo „nie da się czytelnie" → decyzja autora (np. widok wycinkowy
zamiast pełnego drzewa).

## Definition of Done
- [x] Odpowiedź zapisana · kod eksperymentu usunięty · status H4 zaktualizowany.
      *(`docs`, 2026-10-13:*
      - *odpowiedź w *Findings* (własny układ, K2, S2, ślad; `graphview` odpada, więc bez ADR) i w [[drzewo]] v1.4 (*Open* 3);*
      - *H4 w *Findings*: częściowo potwierdzona — czytelnie od osoby z przesuwaniem, całości naraz nie; zadanie na czas < 30 s na telefonie →
        [[ISSUE-032-mvp-install]] → *Hand checks*;*
      - *prototyp `com.grobing.spike002` odinstalowany z `Medium_Phone`, `_throwaway/spike-002/` usunięty, skrypty i zrzuty ze scratchpada
        usunięte; makieta `drzewo-spike002.html` czeka na kosz autora (`CURRENT_STATE.md` → *Autor, poza sesją*);*
      - *EPIC-003 rozpisany na [[US-009-drzewo-od-osoby]], [[US-010-czas-na-drzewie]], [[US-011-polacz-dwie-osoby]].)*

## Implementation plan
> `planning`, 2026-10-13. **DoR (SPIKE):** pytanie ✓ · limit czasu ✓ (1–2 dni) · warunek wyjścia ✓. **Specyfikacja:** [[drzewo]] v1.2
> (`ui`, 2026-10-13) — *Candidates — SPIKE-002*, D8–D10, *Open* 1–4. Makieta `drzewo-spike002.html` (ścieżka w [[drzewo]] → *mockup*).
> Spike **nie zmienia `grobing-code`** ani warstwy danych (D5, D6), więc test migracji i próbne odtworzenie nie mają zastosowania. Testów
> automatycznych nie ma, bo kod nie zostaje (DoD SPIKE). **Danych rodziny nie dotyka:** rodzina w makiecie i w prototypie jest wymyślona
> (106 osób, nazwiska z rdzeni z retro 3, R7).
>
> **Gdzie ocena — decyzja autora w `/pm` 2026-10-13:** na emulatorze, zgodnie z DoD. Krok 3 spike'a („na prawdziwym telefonie autora”)
> przechodzi na listę [[ISSUE-032-mvp-install]] → *Hand checks*: drzewo na telefonie, „kim jest X dla mnie” w mniej niż 30 s i płynność
> przesuwania przy ok. 100 osobach.

### Prior art (źródła, nie pamięć; odczyt 2026-10-13)
- **Kanon dziedziny** → [[drzewo]] D8: TimeNets, drzewa podwójne McGuffina i Balakrishnana, FamilySearch. Cytaty i linki są tam, tu bez
  kopii. W skrócie: rodzina to krata, całej się nie pokazuje, widać wycinek według stopnia zainteresowania, a to są poziomy z D2.
- **Biblioteka układu grafu we Flutterze** (kandydat 1 z *Steps*): [`graphview`](https://pub.dev/packages/graphview) 1.5.1 (MIT, wydana
  ok. 12 miesięcy temu):
  - `SugiyamaAlgorithm` (graf warstwowy) i `BuchheimWalkerAlgorithm` (drzewo, *„Family Tree, Hierarchy View”*);
  - węzły jako dowolne widżety, przesuwanie i przybliżanie przez `InteractiveViewer`;
  - o dużych grafach strona mówi tylko *„works excellent with small graphs”*;
  - zgodność z Flutterem 3.41.1 jest nieznana — sprawdzi to `pub get` w projekcie wyrzucanym (globalnego Fluttera nie ruszamy, ADR-002);
  - Sugiyama nie zna par ani zasady „rodzina partnera z boku”, więc partnerów trzeba sklejać węzłem związku.
- **Wydajność** ([Flutter — UI performance](https://docs.flutter.dev/perf/ui-performance)): *„each frame must render approximately every
  16ms to avoid jank”*, a *„running apps on simulators or emulators, is generally not indicative of the final behavior of release mode
  builds”*. Pomiar klatek na emulatorze jest więc tylko wskazówką. Pomiar na telefonie → ISSUE-032 *Hand checks*.
- **W tym repo:**
  - mini-drzewo jednego poziomu ([[osoba]] D12, `lib/app/person/mini_tree.dart`: miejsce 80 dp, węzeł 44 dp, imię 13 sp) — to istniejący
    kandydat 2 („wycinek”);
  - ścieżka `KinGraph.path` (`lib/data/kinship.dart`) wczytuje się tylko z bazy aplikacji, więc prototyp jej nie użyje (D5);
  - nazwy pokrewieństwa: `kinship_names.dart`, [[ISSUE-025-gender-kinship-together-since]] D2;
  - emulator `Medium_Phone`; kod AOT jest dopiero w buildzie profile albo release.

### Decisions for stop #1
**Najpierw kandydaci w makiecie, przed rekomendacją** (retro 2, R6). Rekomendacje niżej są wstępne: to, co autor zobaczy, może je odwrócić.

| # | Decyzja | Kandydaci (makieta) | Rekomendacja wstępna | Dlaczego / czego to nie da |
|---|---|---|---|---|
| D1 | **Co widać:** całe drzewo czy od osoby ([[drzewo]] D1 → *Obali*, *Open* 4) | K1 · K2 | **K2, bez K1 w MVP** | Całość mieści się na ekranie dopiero przy imieniu 1,4 sp i miejscu osoby 9 dp, a kanon (D8) nie pokazuje całej kraty na małym ekranie. **Nie da:** widoku „wszyscy naraz” na spotkaniu rodzinnym — to D4 |
| D2 | **Sterowanie poziomami i zakres** (*Open* 1) | S1 · S2 · S3 | **S2** (oddalanie odsłania dalszą rodzinę) z przyciskami + / − | Autor chciał drzewa „jak na mapie” (SPIKE-004 D25), a S2 to stopień zainteresowania z D8. Poziomy rosną skokami 6 → 20 → 66 → 99 → 106, więc S2 ma 4 progi, a 4 to prawie wszyscy. **Nie da:** stałej liczby osób na ekranie (pigułka pojawia się na chwilę). **Obali:** autor gubi się, gdy przy oddalaniu układ się zmienia |
| D3 | **Ślad dalszej rodziny** ([[drzewo]] D9) | wł. · wył. | **tak** | Tani i z kanonu (*information scent*), kontrast przy kryciu 60% ≥ 3:1. **Obali:** autor widzi szum albo myli ślad z linią „razem” |
| D4 | **Telewizor** (*Open* 2) | (a) + (b) w makiecie | **(a) + (b)**, tryb prezentacji na poziomie 2. Buduje to pozycja drzewa, nie spike | Bez kodu sieciowego ([[NFR-005-dane-nie-opuszczaja-telefonu]]). **Nie da:** obrazu na telewizorze bez telefonu w ręce |
| D5 | **Gdzie żyje prototyp** | (A) projekt wyrzucany poza repo · (B) ekran debug w `grobing-code`, usuwany przy zamknięciu | **(A)** `{code}/../_throwaway/spike-002/`, `applicationId` `com.grobing.spike002`, bez `INTERNET`, rodzina z makiety jako plik JSON | Jak SPIKE-001 D4: nic nie zostaje w repo, a liczby da się porównać z makietą, bo to ta sama rodzina. **Nie da:** sprawdzenia modelu danych aplikacji (rodziny, „razem od”) na 106 osobach — to pierwszy krok pozycji drzewa (D6). **Koszt:** logika ścieżki przeniesiona z makiety zamiast `KinGraph` |
| D6 | **Wymyślona rodzina 106 osób w buildzie debug** (`lib/dev/fictional_data.dart`; propozycja z `/pm` 2026-10-08) | teraz · w pozycji drzewa | **W pozycji drzewa**, jako jej pierwszy krok (kształt z *Findings*: liczby, bez nazwisk) | Spike zostaje bez kodu w `grobing-code` (DoD SPIKE), a dane wejdą tam, gdzie aplikacja pierwszy raz ich potrzebuje, razem z testami. **Nie da:** „feelingu” 106 osób w innych widokach (lista osób, widok osoby) przed pozycją drzewa. **Obali:** autor chce ich wcześniej — wtedy osobna mała pozycja |

**Stop #1 — odpowiedź autora (2026-10-13):** *„Tak”* — przyjęte wszystkie rekomendacje D1–D6 i zakres niżej: **K2 bez K1** ·
**S2** (oddalanie odsłania dalszą rodzinę, przyciski + / −, 4 progi) · **ślad dalszej rodziny — tak** · **telewizor (a) + (b)**, tryb
prezentacji na poziomie 2, w pozycji drzewa · **prototyp (A)** poza repo · **rodzina 106 osób w `lib/dev/` w pozycji drzewa**. Wyników
zadania na czas z makiety autor nie podał — M5 zbiera stop #2.

### Scope diff vs the item (to accept at stop #1)
- **Krok 3 „na prawdziwym telefonie autora” → emulator** (decyzja autora 2026-10-13), plus wpis na liście ISSUE-032 *Hand checks* (`docs` przy
  zamknięciu).
- **Krok 1** (wymyślony zbiór ok. 100 osób) jest zrobiony w makiecie `ui`: 106 osób, 6 pokoleń, 3 osoby w dwóch związkach, 2 pary „razem”,
  rodzina żony. Prototyp używa tej samej rodziny.
- **Krok 2** (2–3 podejścia):
  - kandydat 1 to K1 i `graphview`;
  - kandydat 2 („wycinek”) już istnieje jako mini-drzewo w [[osoba]] (D12), więc porównanie jest na zrzutach, bez nowego kodu;
  - kandydat 3 to K2, czyli kierunek autora.
- **+ pomiar w makiecie** (szerokość, skala, skrzyżowania na każdym poziomie — [[drzewo]] *Candidates*) i **+ zadanie na czas** jako miara
  kryterium < 30 s.
- **+ wydajność:** klatki przy przesuwaniu ok. 100 węzłów i czas przeliczenia układu. Emulator daje wskazówkę, telefon → ISSUE-032.
- **− Out of scope:**
  - pozycja drzewa w aplikacji (M9–M11): zakładka „Drzewo”, czas, „Połącz dwie osoby” z animacją, słownik nazw złożonych i dawne AC-6
    ISSUE-024, „Pokaż w drzewie” ([[osoba]] D11), tryb prezentacji. *Findings* proponuje podział EPIC-003 na US, a pozycje zakłada `docs`;
  - wymyślona rodzina w `lib/dev/` (D6);
  - zmiany w modelu danych, glosariuszu i [[style-b]] (rola śladu D9 wchodzi dopiero z pozycją drzewa, jeśli D3 = tak);
  - nowa zależność w `grobing-code` (`graphview` tylko w projekcie wyrzucanym);
  - pomiar na fizycznym telefonie (ISSUE-032).

### Steps (dev) — w kolejności falsyfikatora, z limitem czasu
**Krok 0 (`ui` jako subagent, zaraz po „tak”):** wybory autora D1–D4 w [[drzewo]] v1.3 (*Decisions*, *Open*), z datą i cytatem.

1. **Projekt wyrzucany (≤ 1 h).**
   - `flutter create` w `{code}/../_throwaway/spike-002/` (poza trzema repo), `com.grobing.spike002`, bez `INTERNET`; Flutter 3.41.1 bez
     zmian;
   - tokeny kolorów przepisane z `theme.dart` (projekt i tak znika);
   - rodzina z makiety jako `assets/family.json`. Wyciąga ją skrypt w scratchpadzie z `drzewo-spike002.html`.
2. **Układ w Dart (≤ 3 h). M1:**
   - port algorytmu makiety: rzędy według pokolenia, pary jako bloki, kolejność ze środków ciężkości z najmniejszą liczbą skrzyżowań,
     regresja izotoniczna, pierwszeństwo osoby bliższej środkowi;
   - na poziomach 1–5 i dla wszystkich od „Ja”: liczba osób, szerokość, skrzyżowania, **czas przeliczenia w ms (profile)**;
   - wynik musi zgadzać się z tabelą [[drzewo]] *Candidates* w granicach 5%. Inaczej to błąd portu, a nie wynik.
3. **`graphview` (≤ 1,5 h). M2:**
   - ta sama rodzina, `SugiyamaAlgorithm` z węzłem związku między partnerami;
   - te same liczby co w M1, a do tego: **ile par stoi obok siebie** i **czy rodzina partnera wisi z boku**;
   - **Bramka A:** jeśli `pub get` odmawia przy Flutterze 3.41.1 albo licencja nie jest MIT, zapisz to i pomiń krok. Bez obchodzenia, bez
     `dependency_overrides`.
4. **Ekran (≤ 3 h).** Kandydat wybrany na stopie #1 (D1–D3), z lepszym układem z M1 albo M2:
   - `InteractiveViewer`: przesuwanie, szczypanie, podwójne dotknięcie;
   - węzły jako widżety (okrąg 44 dp, imię 13 sp — D10), linie w `CustomPainter` (kolory relacji i styl par jak [[drzewo]] element 4);
   - dotknięcie osoby → ona w środku, z animacją ok. 0,45 s;
   - dolna karta z osobą i prostym suwakiem czasu, bez odtwarzania;
   - **tryb „Losuj osobę”** jak w makiecie: czas znalezienia, wybór ścieżki, wynik na ekranie.
5. **Pomiar na emulatorze (≤ 1 h).**
   - **M3:** build profile na `Medium_Phone`, przesuwanie i przybliżanie na poziomie 3 i przy „wszyscy”: `adb shell dumpsys gfxinfo
     com.grobing.spike002` (odsetek klatek > 16 ms, 90. percentyl); czas od dotknięcia osoby do końca animacji;
   - **M4:** zrzuty przy tekście systemowym 200% na 360 dp (czy ucięte imię nie myli osób) i porównanie z mini-drzewem w [[osoba]]
     (kandydat 2);
   - liczby to tylko wskazówka (*Prior art* → wydajność).
6. ***Findings* i sprzątanie.** W *Findings*:
   - tabela M1–M4 i M5 (wyniki zadania na czas autora ze stopu #2);
   - rekomendacja: układ (własny albo `graphview`), sterowanie, ślad, zakres poziomów. **ADR tylko wtedy, gdy rekomendacja dodaje
     zależność** (`graphview`); inaczej notatka w *Findings* i w [[drzewo]];
   - status H4;
   - propozycja podziału [[EPIC-003-zrozumienie]] na US (M9, M10, M11), z wejściami z ISSUE-024 i z D6;
   - kształt rodziny dla `lib/dev/` (same liczby, bez nazwisk) jako wejście do D6;
   - wpis dla ISSUE-032 *Hand checks*.

   Usuwane: `_throwaway/spike-002/`, aplikacja `com.grobing.spike002` z emulatora, JSON i zrzuty ze scratchpada. Makieta zostaje do zamknięcia,
   potem trafia na listę do kosza autora (`CURRENT_STATE` → *Autor, poza sesją*).

**Limit czasu:** 2 dni. Po ok. 1 dniu bez M1 i bez ekranu z kroku 4 → stop i raport, bez dociągania na siłę.
**Dane:** wyłącznie rodzina z makiety (rdzenie z R7). Przed `git add` dry-run strażnika treści na liście plików vaulta.

### Exit → evidence
| Warunek | Dowód |
|---|---|
| Wybrane podejście | decyzje D1–D4 ze stopu #1 i M1/M2 → rekomendacja w *Findings* |
| Czytelność ok. 100 osób | tabela [[drzewo]] *Candidates*, M4 (zrzuty, tekst 200%), M5 (zadanie na czas autora, < 30 s) |
| Płynność | M3 na emulatorze (wskazówka); telefon → ISSUE-032 |
| „Nie da się czytelnie” | M5 > 30 s na poziomie 2 i 3 → decyzja autora (*Exit criterion*, np. sam wycinek) |
| Status H4 | *Findings* |

### Manual verification (stop #2, po polsku, według miejsca)
**Agent na emulatorze — przed stopem, ze zrzutami:** instalacja buildu profile, zrzuty każdego poziomu i „wszyscy”, przesuwanie i przybliżanie
(M3), tekst 200% (M4), zadanie na czas jako sprawdzenie, że działa (bez mierzenia czasu człowieka).

**Autor: odczucie (najwyżej 3 kroki):**
- **Emulator `Medium_Phone`** (aplikację „spike 002” otworzy agent):
  1. Przesuwaj i przybliżaj drzewo wybranym sposobem (D2), aż zobaczysz dalszą rodzinę, a potem wróć do siebie. **Czy cały czas wiesz,
     gdzie jesteś?**
  2. Dotknij po kolei trzech osób, żeby każda stanęła w środku. **Czy animacja pozwala śledzić, co się przesunęło?**
  3. Naciśnij „Losuj osobę” trzy razy: na poziomie 2, 3 i najdalszym. **Zapisz czasy** — czy mieszczą się w 30 s?
- **Napisz tutaj:** „ok” · „pomiń” · opis tego, co nie gra · czasy z kroku 3.

### Closing checklist (docs)
- *Findings* i DoD spike'a (odpowiedź, kod usunięty, H4).
- [[drzewo]]: wynik spike'a w *Open* 3 i decyzje. Pisze `ui` (krok 0; zmiany po stopie #2 — `ui` przed zamknięciem).
- ADR tylko przy nowej zależności (krok 6).
- [[ISSUE-032-mvp-install]] → *Hand checks*: „Drzewo na telefonie — kim jest X dla mnie w mniej niż 30 s i płynność przesuwania przy ok.
  100 osobach (SPIKE-002, decyzja autora 2026-10-13)”.
- [[EPIC-003-zrozumienie]]: US z propozycji w *Findings* i pozycja drzewa, z D6 jako pierwszym krokiem i z wejściami z ISSUE-024. Pozycje
  zakłada `docs`.
- `TRACEABILITY.md`: wiersz M9 (Issue Status `done`); M10 i M11 — US z EPIC-003.
- `CURRENT_STATE.md`: następna pozycja; katalog z makietą na liście *Autor, poza sesją*.
- Sprzątanie z kroku 6 potwierdzone. Paczka: **vault** (i `grobing-agents`, jeśli coś się w nim zmieni), **bez `grobing-code`**.

## Findings
> `dev`, 2026-10-13. Prototyp w `{code}/../_throwaway/spike-002/` (`com.grobing.spike002`, build profile, `Medium_Phone`), rodzina z makiety
> (106 wymyślonych osób, 38 związków) w `assets/family.json`. Prototyp zostaje do stopu #2, bo autor ocenia na nim; usuwa go zamknięcie
> (krok 6 → sprzątanie).

### M1 — własny układ (port makiety), od „Ja”
| Widok | Osób | Pokoleń | Szerokość | Skrzyżowania | Skala „zmieścić” | Pary obok siebie | Rodzice nad „Ja” (miejsca) | Przeliczenie |
|---|---|---|---|---|---|---|---|---|
| K2 · poziom 1 | 6 | 3 | 212 dp | 0 | 1,00 | 2/2 | 0,0 | 1,5 ms |
| K2 · poziom 2 | 20 | 4 | 864 dp | 0 | 0,38 | 5/5 | 1,6 | 3,6 ms |
| K2 · poziom 3 | 66 | 5 | 1960 dp | 6 | 0,17 | 21/21 | 1,9 | 10,1 ms |
| K2 · poziom 4 | 99 | 6 | 2663 dp | 9 | 0,12 | 35/35 | 2,5 | 13,6 ms |
| K1 · wszyscy | 106 | 6 | 2960 dp | 10 | 0,11 | 38/38 | 2,2 | 15,4 ms |

Liczby osób, pokoleń, szerokości i skrzyżowań są **identyczne** z tabelą [[drzewo]] *Candidates*, więc port jest wierny. Przeliczenie (profile,
emulator) trwa do 15 ms przy 106 osobach — prawie cały budżet jednej klatki, na wątku głównym.

### M2 — `graphview` 1.5.1, Sugiyama z węzłem związku (warstwy *network simplex*)
**Bramka A przeszła:** licencja MIT, `pub get` z Flutterem 3.41.1 bez konfliktu. Katalog `familytree` w paczce jest pusty.

| Widok | Osób | Szerokość | Skrzyżowania | Pary obok siebie | Rodzice nad „Ja” | Krawędzie rodzic → dziecko o jedno pokolenie | Przeliczenie |
|---|---|---|---|---|---|---|---|
| K2 · poziom 2 | 20 | 1000 dp | 6 | 5/5 | 1,1 | 12/27 | 4,2 ms |
| K2 · poziom 3 | 66 | 2884 dp | 32 | 12/21 | 4,5 | 63/87 | 13,3 ms |
| K2 · poziom 4 | 99 | 5188 dp | 98 | 18/35 | 3,3 | 96/126 | 53,5 ms |
| K1 · wszyscy | 106 | 5244 dp | 88 | 24/38 | 1,8 | 102/134 | 40,4 ms |

Przy całej rodzinie `graphview` daje układ 1,8 raza szerszy, 88 skrzyżowań zamiast 10, tylko 24 z 38 par obok siebie, a 32 ze 134 krawędzi
rodzic–dziecko omija pokolenie. Na zrzucie z poziomu 2 „Ja” stoi na skraju warstwy, Kasia daleko od niego, linie partnerów idą ukośnie, a
węzły związków zajmują osobne rzędy. Sugiyama nie zna par ani zasady „rodzina partnera z boku” (*Prior art*). **Wniosek: własny układ;
`graphview` odpada, więc nie ma nowej zależności ani ADR.**

### M3 — klatki na emulatorze (wskazówka)
`dumpsys gfxinfo` nie widzi klatek Fluttera (0 klatek), więc pomiar idzie z silnika: `FrameTiming` (budowa i rasteryzacja każdej klatki), build
profile, `Medium_Phone`.

| Co | Klatek | > 16,7 ms | Budowa p50 / p90 / max | Raster p50 / p90 / max |
|---|---|---|---|---|
| oddalenie do poziomu 3 (przeliczenie + animacja) | 20 | 55% | 4,9 / 12,7 / 34,8 ms | 20,0 / 65,2 / 91,7 ms |
| przesuwanie, poziom 3 (66 osób) | 311 | 1,0% | 1,6 / 2,0 / 4,4 ms | 4,8 / 15,6 / 132 ms |
| oddalenie do poziomu 4 | 32 | 19% | 5,1 / 5,8 / 30,7 ms | 14,4 / 17,5 / 133 ms |
| przesuwanie, poziom 4 (99 osób) | 312 | 1,3% | 1,4 / 1,9 / 3,6 ms | 5,1 / 7,8 / 136 ms |
| przybliżenie do poziomu 3 · do poziomu 2 | 31 · 40 | 23% · 5% | ok. 3–5 ms | 14–15 / 17–20 ms |
| zmiana osoby w środku ×3 (poziom 2) | 68 | 2,9% | 2,4 / 3,4 / 10,0 ms | 9,1 / 16,0 / 110 ms |

- **Przesuwanie jest płynne** (≤ 1,3% wolnych klatek) także przy 99 osobach.
- **Przejście między poziomami szarpie:** przeliczenie i animacja 66–99 osób, z rasteryzacją jako wąskim gardłem (linie przerywane liczone co
  klatkę, cienie, wszystkie węzły na nowo). Wejście do pozycji drzewa: linie w `RepaintBoundary` albo z pamięci podręcznej w czasie animacji,
  przerywane bez `computeMetrics` w każdej klatce, mniej cieni, przeliczenie poza klatką animacji.
- Dokumentacja Fluttera: emulator *„generally not indicative”*. Pomiar na telefonie → ISSUE-032 *Hand checks*.

### M4 — zrzuty: poziomy, tekst 200%, wycinek
- **Poziom 2 przy skali 1:** czytelny (imię 13 sp), 20 osób; w bok trzeba przesuwać (864 dp).
- **Poziom 3 przy skali 0,69:** imię ok. 9 sp, czytelne z bliska. **Poziom 4 przy 0,48:** ok. 6 sp — widać kształt rodziny, ale imion nie.
  Pytanie do `ui` przy pozycji drzewa: czy imiona przy oddalaniu nie powinny maleć poniżej czytelnej wielkości (jak podpisy na mapie, z
  ukrywaniem nakładających się).
- **Tekst 200% na 360 dp:** imiona ucięte do 3–4 liter, inicjały wychodzą poza okrąg, karta i pasek zajmują pół ekranu, a przyciski + / −
  zasłaniają osobę. Pozycja drzewa bierze regułę mini-drzewa (miejsce osoby rośnie z tekstem, najwyżej 160 dp — [[osoba]] v2.2) i limit
  wielkości inicjałów.
- **Wycinek (kandydat 2) to mini-drzewo w [[osoba]]**: ten sam zbiór co K2 na poziomie 1 (6 osób). Zostaje w widoku osoby bez zmian.
- **Karta osoby w środku:** opis z łańcucha („Twoja żona → jej tata → je…”) nie mieści się w jednej linii, więc karta potrzebuje nazw złożonych
  ze słownika (dawne AC-6 ISSUE-024, [[drzewo]] D6) tak samo jak baner „Połącz dwie osoby”.

### M5 — zadanie na czas (autor, stop #2)
*Czeka na stop #2.* Zadanie działa od początku do końca (sprawdzone przez agenta: losowanie, dotknięcie, trzy odpowiedzi, wynik w logu i w
„Wynikach”); czasu agenta nie liczymy.

### H4 — status (wstępny, przed M5)
*„Graf ok. 100 osób z powinowatymi i powtórnymi małżeństwami da się czytelnie pokazać na ekranie telefonu”* → **częściowo potwierdzona:**
czytelnie przy skali bliskiej 1, z przesuwaniem i przestawianiem środka (K2), przy czym od poziomu 3 widać już prawie całą rodzinę. Całość naraz
(106 osób) — nie: tylko jako kształt. Ostateczny status po M5.

### Rekomendacja (do zamknięcia, po M5)
- **Układ:** własny (port makiety) w pozycji drzewa, z testami (`qa`). Bez nowej zależności, bez ADR.
- **Sterowanie:** S2 z 4 progami. Progi dev (1,3 · 0,85 · 0,55) — do potwierdzenia odczuciem na stopie #2 i na telefonie.
- **Ślad dalszej rodziny:** widoczny na zrzutach, nie myli się z linią „razem” (kreska 3/3 krótsza i bledsza).
- **Animacja przejścia:** optymalizacja z M3 w pozycji drzewa.
- **Podział [[EPIC-003-zrozumienie]] (propozycja dla `docs`):**
  1. **drzewo od osoby (M9):** układ, S2, ślad, karta z nazwą złożoną, „Pokaż w drzewie” ([[osoba]] D11), tekst 200%; **pierwszy krok —
     wymyślona rodzina w `lib/dev/`** (D6);
  2. **czas (M10):** suwak z odtwarzaniem, daty „razem od” i ślubu, znicze;
  3. **„Połącz dwie osoby” (M11):** okno z kaflami, animacja ścieżki, baner z nazwą złożoną ze słownika (dawne AC-6 ISSUE-024);
  4. **tryb prezentacji na telewizor** ([[drzewo]] D11) — w 1. albo osobno, gdy 1. urośnie.
- **Kształt rodziny dla `lib/dev/` (D6, same liczby):** 106 osób, 38 związków, 6 pokoleń (roczniki 1868–2019), 31 zmarłych i 75 żyjących,
  39 osób bez rodziców w danych (powinowaci i najstarsi), 3 osoby w dwóch związkach (wdowiec, wdowa, rozwód), 2 pary „razem” (jedna potem
  ze ślubem), rodzina żony w 3 pokoleniach z jej kuzynami. **Do potwierdzenia przez autora:** proporcja zmarłych do żyjących w prawdziwych
  notatkach (tylko liczby) — od niej zależy, ile zniczy widać na drzewie.
- **Dla ISSUE-032 *Hand checks*:** drzewo na telefonie — „kim jest X dla mnie” w mniej niż 30 s, płynność przesuwania i przejścia między
  poziomami przy ok. 100 osobach, progi S2 w ręce.

### Dev report
- **Zrobione:** kroki 1–5, krok 6 bez M5 (stop #2). Sprzątanie po stopie #2 — prototyp jest potrzebny autorowi.
- **Deviations:**
  1. progi S2 (1,3 · 0,85 · 0,55) wybrał `dev`, bo specyfikacja mówi „4 progi” bez wartości;
  2. karta zadania stoi na dole obszaru drzewa, nie u góry: u góry zasłaniała szukaną osobę (dziadkowie w górnym rzędzie);
  3. suwak czasu bez odtwarzania, „Połącz dwie osoby” i „Pokaż” jako zaślepki (zakres planu);
  4. znicz jako ikona Material (`local_fire_department`), nie znicz aplikacji;
  5. klatki mierzone przez `FrameTiming`, bo `gfxinfo` nie widzi Fluttera.
- **Błędy znalezione w przejściu na emulatorze, poprawione:** (a) przyciski + / − skalowały tylko osie x i y, a `getMaxScaleOnAxis()` bierze
  też oś z, więc poziom się nie zmieniał (pierwszy pomiar M3 dotyczył poziomu 2 — powtórzony); **wejście do pozycji drzewa:** skala z osi
  x, nie `getMaxScaleOnAxis()`; (b) pierwsza klatka na Androidzie ma rozmiar bliski zeru, więc ustawienie środka trafiało w róg — teraz czeka na
  prawdziwy rozmiar.
- **`flutter analyze`:** czysto (projekt wyrzucany). `grobing-code` bez zmian.

## Verification
> `qa`, 2026-10-13. **DoD SPIKE:** odpowiedź zapisana · kod eksperymentu usunięty · status hipotezy zaktualizowany. Testów automatycznych
> nie ma, bo kod nie zostaje. Dowodem są pomiary z logów emulatora, które `qa` czytał sam, a nie tylko tabele z raportu `dev`.
> **Przegląd `ui` pominięty świadomie:** to wyrzucany prototyp, a nie ekran produktu. Prawdą o ekranie jest [[drzewo]] v1.3, a przegląd
> zbudowanego ekranu przypada na pozycję drzewa. **Sieci w kodzie prototypu nie ma**, więc logcat pod kątem współrzędnych nie dotyczy (R7).

### Exit → evidence, sprawdzone przez `qa`
| Warunek | Sprawdzenie `qa` | Wynik |
|---|---|---|
| Wybrane podejście | stop #1 (*„Tak”*, D1–D6) + M1/M2 z logu `SPIKE002 M1/M2` (build z `MEASURE=true`) + zrzut porównawczy M2 | ✅ własny układ, K2, S2, ślad |
| Czytelność ok. 100 osób | M1 = tabela [[drzewo]] *Candidates* liczba w liczbę; zrzuty poziomów 2–4 i tekstu 200% (M4) obejrzane | ✅ z uwagami (poziom 4 i tekst 200% — M4) |
| Zadanie na czas < 30 s (M5) | brak wyniku autora w logu (`SPIKE002 M5` tylko z próby agenta sprzed restartu) | ⬜ **pomiń** → ISSUE-032 |
| Płynność | M3 z logu `FrameTiming` po poprawce osi z (pierwszy przebieg mierzył poziom 2 — odrzucony) | ✅ wskazówka; telefon → ISSUE-032 |
| Status H4 | *Findings* → *H4*: częściowo potwierdzona | ✅ (bez M5) |

### Dane rodziny
- Zmienione pliki vaulta: [[drzewo]], ta pozycja, `TRACEABILITY.md`. Przykłady to wyłącznie wymyślona rodzina z rdzeni z R7 (Wymyśl-, Zmyśl-,
  Testow-, Przykład-) i liczby. **Dry-run strażnika treści** na tych trzech plikach przeszedł.
- Prototyp, `family.json`, makieta i zrzuty leżą **poza repo** (projekt wyrzucany i scratchpad sesji). `grobing-code` i `grobing-agents` są
  czyste.
- **Odstępstwo od D5:** build profile ma uprawnienie `INTERNET` z manifestu `profile`, który Flutter dodaje dla narzędzi pomiaru. Główny
  manifest go nie ma, kod prototypu niczego nie wysyła, a dane są wymyślone.

### Stop #2 — odpowiedź autora (2026-10-13)
*„ok”*, bez czasów z kroku 3. **Sprawdzone na urządzeniu** (pamięć: „ok” sprawdzać na urządzeniu): po restarcie aplikacji o 16:15 w minucie
16:40 jest ok. 1050 klatek, osoba w środku zmieniła się na inną, a „Pokaż” zostawiło komunikat — **kroki 1 i 2 mają ślad**. Wyników zadania na
czas od autora nie ma — **krok 3 zapisany jako „pomiń”**.

- Krok 1 (orientacja przy oddalaniu i powrocie): **ok** (ślad na urządzeniu).
- Krok 2 (animacja przestawiania środka): **ok** (ślad na urządzeniu).
- Krok 3 (zadanie na czas, poziomy 2, 3, 4): **pomiń** — niewykonane.

### Na listę ISSUE-032 → *Hand checks* (po jednym w linii)
- „pomiń”: zadanie na czas „kim jest X dla mnie” < 30 s przy ok. 100 osobach (M5 — kryterium spike'a niezmierzone).
- „nieprzetestowane na żywo”: płynność przesuwania i przejścia między poziomami na fizycznym telefonie (M3 tylko emulator).
- „nieprzetestowane na żywo”: progi S2 (1,3 · 0,85 · 0,55) w ręce, przy szczypaniu palcami (na emulatorze tylko przyciski + / − i mysz).

### Werdykt `qa`: APPROVED (self-check, z uwagami)
Pytanie spike'a ma odpowiedź: **czytelnie od osoby (K2) przy skali bliskiej 1, z przesuwaniem i przestawianiem środka; całości naraz — nie**.
Podejście jest wybrane i zmierzone: własny układ wygrywa z `graphview` w każdej mierze (M2). Uwagi:
1. M5 (< 30 s) niezmierzone — przechodzi na telefon (ISSUE-032), zgodnie z decyzją autora z `/pm`;
2. przejście między poziomami szarpie na emulatorze (do 55% klatek) — optymalizacja w pozycji drzewa (*Findings* → M3);
3. tekst 200% i poziom 4 wymagają reguł z mini-drzewa i decyzji `ui` (*Findings* → M4);
4. w [[drzewo]] *Style B rules applied* zostało nieaktualne „i legenda (SC 1.4.1)” (zgłosił `ui` w kroku 0) — do poprawy przez `ui` przy
   pozycji drzewa.

**Czego szukałem i nie znalazłem:** rozjazdu M1 z makietą (0 różnic) · danych rodziny w zmianach (0) · zmian w `grobing-code` (0) · kodu
sieciowego w prototypie (0).

### Paczka dla `docs`
- **vault:** `05_DESIGN/drzewo.md` · `backlog/spikes/SPIKE-002-tree-on-a-phone.md` · `00_START_HERE/TRACEABILITY.md` + pliki zamknięcia
  `docs` (checklista w *Implementation plan*).
- **`grobing-code`, `grobing-agents`:** bez zmian.
- **Sprzątanie (krok 6) przed commitem:** odinstalować `com.grobing.spike002` z `Medium_Phone`, usunąć `{code}/../_throwaway/spike-002/`, ze
  scratchpada usunąć zrzuty i skrypty (makieta zostaje do kosza autora).
