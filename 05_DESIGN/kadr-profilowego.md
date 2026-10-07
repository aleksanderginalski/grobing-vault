---
screen: "Kadr profilowego — wycinek zdjęcia w okręgu profilowego"
items: ["[[ISSUE-018-profile-photo-crop]]"]
us: "[[US-005-zdjecia]] (rozwinięcie po jej werdykcie — AC US-005 spełnione bez tego ekranu)"
journey-step: "n/a — M1 (przepisywanie i zbieranie u babci); docelowo profilowe w widoku osoby (M5, R4 prawy) i w węzłach drzewa (R3)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-kadr-profilowego.html (ramki 1–6)"
updated: 2026-10-07
---

# Kadr profilowego — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.10, reguła 14) · referencja: [[references]] → **R4
> (prawy ekran)** i **R3** — okrągły portret osoby. Ekranu kadrowania żadna referencja nie pokazuje, więc dziedziczy
> reguły stylu B.
>
> **Wersja 1 (2026-10-07, przed planem [[ISSUE-018-profile-photo-crop]]).** Uwaga autora na stopie #2
> [[ISSUE-017-person-photos]]: *„zakładałem, że gdy wybieram dane zdjęcie, to mogę ustalić jego «kadr» z liniami
> pomocniczymi, aby na profilowym była właśnie ta osoba, a nie całe zdjęcie”*. Ten ekran to ten kadr. Wejścia są w
> [[zdjecie]] v1.4 (B4'), a okręgi, które pokazują kadr, w [[wpis-osoby]] (1a), [[grob]] (5) i [[zdjecia-osoby]] (2).
>
> **Wersja 1.1 (2026-10-07, przegląd `ui` zbudowanego ekranu, 0 BLOCKER / 0 MAJOR / 6 MINOR):**
> - cień linii trójpodziału ma krycie 50 % (K2);
> - „Pomniejsz” i „Powiększ” przesuwają płynnie, 250 ms, jak dotknięcie (K4);
> - okrąg z kadrem jest pusty, dopóki nie zna wymiarów zdjęcia (*Gdzie kadr widać*);
> - przesuwanie zdjęcia czytnikiem ekranu to nazwana luka (K2);
> - dotknięcie w trakcie „Powiększ” zachowuje cały krok, a plik, którego nie da się zdekodować, daje „błąd odczytu” —
>   poprawki w kodzie, zgodne z v1.
>
> **Wersja 1.2 (2026-10-07, stop #2 — decyzja autora):** *„nie czuję, że potrzebowałbym tych lup — cała reszta działa
> wystarczająco dobrze”* (zrzut ekranu z przekreśloną podpowiedzią i lupami). Wybór autora — opcja A:
> - **bez podpowiedzi K3 i bez lup K4** — pod zdjęciem zostaje tylko „Gotowe”;
> - **podwójne dotknięcie przybliża ×2 w miejscu dotknięcia**, a po największym przybliżeniu wraca do całości — to
>   zastępstwo rozsunięcia palców jednym palcem (SC 2.5.1, D7'), ten sam gest co w podglądzie [[zdjecie]] B2;
> - pojedyncze dotknięcie dalej przenosi punkt na środek, ale czeka ok. 0,3 s, czy nie przyjdzie drugie.

## Purpose
Wybór wycinka zdjęcia, który pokazuje okrąg profilowego jednej osoby — twarz tej osoby ze zdjęcia grupowego, a nie
środek zdjęcia (ISSUE-018 AC 1–3). Kadr należy do **łącza osoba–zdjęcie**, nie do zdjęcia: na jednym zdjęciu każda
osoba ma własny kadr, a plik się nie zmienia.

**Model w jednym zdaniu** (kanon: [GEDCOM 7.0](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html) →
`CROP`, przy `MULTIMEDIA_LINK`): kadr to prostokąt w obrazie — `LEFT` i `TOP` to *„a number of pixels to not display
from the left/top side of the image”*, `WIDTH` i `HEIGHT` to jego rozmiar, a wycinek wychodzący poza obraz jest
błędem. Okrąg profilowego to okrąg wpisany w **kwadratowy** kadr. Jednostkę zapisu (piksele jak GEDCOM albo ułamki
boków jak region w Gramps — *Prior art* niżej) rozstrzyga ADR w `planning`. Ekran zakłada tylko kwadrat w obrębie
zdjęcia.

## Prior art
- **GEDCOM 7.0 `CROP`** (cytat wyżej): kadr przy łączu, w pikselach, wewnątrz obrazu; bez `CROP` — całe zdjęcie.
- **Gramps** (program genealogiczny z *Prior art* [[EPIC-003-zrozumienie]]): region przy odwołaniu osoby do zdjęcia
  (`MediaRef`) to prostokąt zaznaczany na całym zdjęciu, a jego narożniki są zapisane **w procentach** obrazu, np.
  `<region corner1_x="51" corner1_y="19" corner2_x="59" corner2_y="33"/>`. Miniatura osoby pokazuje ten wycinek, nie
  całe zdjęcie. Źródło: forum Gramps — [Clarifying some Gramps Data model detail](https://gramps.discourse.group/t/clarifying-some-gramps-data-model-detail/8986),
  [Which software to import Gramps media's information into XMP](https://gramps.discourse.group/t/which-software-to-import-gramps-medias-information-into-xmp-pictures-tags/1529)
  (wiki Gramps zwróciło 403, więc źródłem są wątki forum, nie podręcznik).
- **Telefony** (systemowe Kontakty, komunikatory): zdjęcie profilowe ustawia się przesuwaniem i przybliżaniem zdjęcia
  pod nieruchomym okręgiem. To konwencja z doświadczenia, a nie norma z cytatu — falsyfikatorem jest makieta na stopie
  #1 (D1).

## Navigation
- **Wejście** — z podglądu zdjęcia osoby ([[zdjecie]] B4', v1.4):
  - **„Ustaw jako profilowe”** (zdjęcie, które nie jest profilowym) → K z kadrem domyślnym albo z kadrem, który to
    łącze już ma (np. zdjęcie było kiedyś profilowym). „Gotowe” → zdjęcie staje się profilowym tej osoby, z tym kadrem
    (D2);
  - **„Popraw kadr”** (profilowe) → K z obecnym kadrem albo, bez kadru, z domyślnym. „Gotowe” → nowy kadr.
- **„Gotowe”** → [[zdjecie]] B na tym zdjęciu, które jest teraz pierwsze (profilowe): podtytuł „Zdjęcie profilowe”, a w
  dolnym pasku „Popraw kadr”.
- **Wstecz** → [[zdjecie]] B bez zmian, bez okna — przepada najwyżej ustawienie okręgu ([[style-b]] reguła 10; D9).
- **Zapis:** kadr i profilowe trafiają do zmian formularza osoby i zapisują się z jego „Zapisz”, a „Odrzuć” je cofa
  ([[zdjecia-osoby]] D1). W [[zdjecia-osoby]] zmiana kadru pokazuje linię zapisu (element 6).

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| K1 | **Pasek** na tle: wstecz; tytuł „Kadr profilowego” (16 sp, półgruby); podtytuł — imiona i nazwisko osoby jak w formularzu w tej chwili (14 sp, tekst pomocniczy, jedna linia, ucięta); bez imion i nazwiska: „Nowa osoba” | pasek | wstecz → [[zdjecie]] B bez zmian | — | — | decyzja projektowa · wzorzec B1 i D1 z [[zdjecie]] |
| K2 | **Obszar kadru** — całe miejsce między paskiem a K5 (v1.2: bez K3 i K4). **Okrąg nieruchomy**, wyśrodkowany, średnica = szerokość obszaru − 2 × 24 dp (312 dp przy 360 dp szerokości), ale nie więcej niż wysokość obszaru − 48 dp. **Pod okręgiem zdjęcie**, które się przesuwa i przybliża (D1). Poza okręgiem zdjęcie przyciemnione kolorem tła (krycie 72%), żeby widać było resztę zdjęcia i inne twarze. **Pierścień:** 2 dp w akcencie, z obu stron linia 1 dp w kolorze tła (D10). **Linie pomocnicze:** podział na trzy w kwadracie okręgu, przycięty do okręgu — dwie pionowe i dwie poziome, 1 dp w kolorze tekstu (krycie 60%) z cieniem 1 dp w kolorze tła (krycie 50 %, v1.1), zawsze widoczne (D6). **Bez tekstu na zdjęciu.** Opis dla czytnika: „Kadr profilowego — zdjęcie w okręgu”, bez działania dla czytnika (v1.1): jego „podwójne dotknięcie” trafiałoby w środek, czyli niczego nie przesuwa. **Luka nazwana:** czytnikiem ekranu nie da się ani przesunąć, ani przybliżyć zdjęcia (v1.2: bez lup K4) — „Gotowe” zapisuje kadr, który jest | obraz z gestami | **przesunięcie palcem** — przesuwa zdjęcie; **rozsunięcie palców** — przybliża; **dotknięcie** punktu — przesuwa ten punkt na środek okręgu (animacja 250 ms, po ok. 0,3 s oczekiwania na drugie dotknięcie) — alternatywa przesunięcia jednym dotknięciem; **podwójne dotknięcie** (v1.2) — przybliża ×2 i stawia ten punkt na środku, a przy największym przybliżeniu wraca do całości (okrąg obejmuje krótszy bok) wokół tego punktu — alternatywa rozsunięcia palców (D7') | kadr łącza; bez kadru — największy kwadrat ze środka (D3) | zdjęcie zatrzymuje się na krawędzi: **okrąg zawsze cały na zdjęciu** (D4); przybliżenie od „okrąg obejmuje krótszy bok” do „okrąg obejmuje 128 px zdjęcia” (D5) | ISSUE-018 *What to build* 1 · AC 1 · GEDCOM 7 `CROP` · [[style-b]] reguła 14 (v1.10) |
| ~~K3~~ | ~~Podpowiedź „Przesuń zdjęcie palcem albo dotknij twarzy.”~~ — **usunięta w v1.2** (decyzja autora na stopie #2) | — | — | — | — | — |
| ~~K4~~ | ~~„Pomniejsz” / „Powiększ”~~ — **usunięte w v1.2** (decyzja autora na stopie #2); zastępstwo rozsunięcia palców to podwójne dotknięcie w K2 (D7') | — | — | — | — | — |
| K5 | **„Gotowe”** — przycisk wypełniony (akcent), przypięty na dole, ≥ 52 dp, na pełną szerokość z marginesami 16 dp | przycisk | → [[zdjecie]] B; wycinek w okręgu staje się kadrem łącza tej osoby, a przy wejściu z „Ustaw jako profilowe” zdjęcie staje się profilowym | — | — | [[style-b]] reguła 1 · AC 1, 3 |

**Co zapisuje „Gotowe”:** kwadrat w obrazie, który widać w okręgu — zawsze jawnie, także gdy nikt nie przesunął
zdjęcia. Profilowe bez kadru zostaje tylko tam, gdzie nikt nie otworzył K (D3).

**Dane, których ekran potrzebuje** (dla `planning`):
- plik zdjęcia: z magazynu aplikacji albo, gdy zdjęcie jest dopiero wybrane, przygotowany plik z katalogu roboczego
  ([[ADR-008-photos-access-copy-and-backup-consistency]]) — ten sam, który pokazuje [[zdjecie]] B;
- wymiary zdjęcia w pikselach (granice D4, D5);
- kadr łącza tej osoby z tym zdjęciem: ze zmian formularza albo zapisany; brak = środek (D3);
- imiona i nazwisko osoby jak w formularzu (K1).

**Gdzie kadr widać** (te ekrany zmieniają tylko to, co pokazuje okrąg):
- [[wpis-osoby]] → 1a (okrąg 80 dp);
- [[grob]] → 5 (miniatura w karcie, 40 dp);
- [[zdjecia-osoby]] → 2 (nagłówek, 96 dp).

Każdy z tych okręgów pokazuje kadr łącza, a bez kadru — największy kwadrat ze środka, jak dziś. **Okrąg z kadrem jest
pusty, dopóki nie przeczyta wymiarów zdjęcia** (chwila przy pierwszym pokazaniu w danym uruchomieniu; v1.1): środek
zdjęcia grupowego mógłby na moment pokazać kogoś innego. Siatka w
[[zdjecia-osoby]] (element 4) i podgląd [[zdjecie]] B się nie zmieniają: siatka zostaje przycięta ze środka
(ISSUE-018 → *Out of Scope*), a podgląd pokazuje całe zdjęcie. Okrąg dekoduje wycinek w rozmiarze co najmniej
2 × pole, jak dziś całe zdjęcie (`coverDecodeWidth`).

## States
| Stan | Co widać |
|---|---|
| wczytywanie | samo tło (odczyt trwa ułamek sekundy, jak [[zdjecie]] „B — wczytywanie”) |
| otwarty — kadr domyślny | K1, K2, K5; zdjęcie tak przybliżone, że okrąg obejmuje krótszy bok, i wyśrodkowane — dokładnie to, co dziś pokazuje okrąg profilowego |
| otwarty — kadr łącza | K1, K2, K5; zdjęcie ustawione tak, że okrąg pokazuje zapisany kadr (albo kadr z tej edycji formularza) |
| przy granicy | zdjęcie nie przesuwa się dalej niż krawędź (okrąg cały na zdjęciu, bez odbicia); rozsunięcie palców nie przybliża dalej niż do 128 px, a podwójne dotknięcie przy największym przybliżeniu wraca do całości. Małe zdjęcie, którego krótszy bok ma ≤ 128 px: bez przybliżenia, przesunięcie możliwe tylko wzdłuż dłuższego boku |
| błąd odczytu | na środku obszaru `broken_image_outlined` (tekst pomocniczy) i „Nie udało się otworzyć zdjęcia.” (14 sp, tekst pomocniczy); bez okręgu, K5 nieaktywne; wstecz wraca do B |

## Sketch
```
 K — kadr profilowego                  B — podgląd profilowego (v1.4)
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│ ←  Kadr profilowego              │  │ ←  Anna Wymyślona                │
│    Anna Wymyślona                │  │    Zdjęcie profilowe             │
│ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │  │   ┌──────────────────────────┐   │
│ ░░░░░░░░╭──────────────╮░░░░░░░░ │  │   │                          │   │
│ ░░░░░░╭─┼────┼────┼────┼─╮░░░░░░ │  │   │   [zdjęcie w całości,    │   │
│ ░░░░░│  │    │    │    │  │░░░░░ │  │   │    bez przycinania]      │   │
│ ░░░░░├──┼────┼────┼────┼──┤░░░░░ │  │   │                          │   │
│ ░░░░░│  │   [twarz]    │  │░░░░░ │  │   └──────────────────────────┘   │
│ ░░░░░├──┼────┼────┼────┼──┤░░░░░ │  │  Na zdjęciu: Anna Wymyślona,     │
│ ░░░░░│  │    │    │    │  │░░░░░ │  │  Jan Wymyślony          Zmień    │
│ ░░░░░░╰─┼────┼────┼────┼─╯░░░░░░ │  │        ‹     1 z 3     ›         │
│ ░░░░░░░░╰──────────────╯░░░░░░░░ │  │                                  │
│ ░░ (reszta zdjęcia przyciemniona)│  │  ⌗ Popraw kadr  🗑 Usuń z tej osoby│
│ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │  └──────────────────────────────────┘
│                                  │   ░ — zdjęcie poza okręgiem, przyciemnione
│ ┌──────────────────────────────┐ │   ─┼─ — linie pomocnicze (trójpodział)
│ │            Gotowe            │ │
│ └──────────────────────────────┘ │
└──────────────────────────────────┘
```

## Tempo
Rekordem jest **profilowe osoby**. Założenie z [[zdjecia-osoby]] → *Tempo*: ok. 50 zdjęć osób w MVP. Ile z nich to
zdjęcia grupowe, na których środek nie trafia w twarz, **nie wiadomo** — założenie do sprawdzenia: ok. 20 profilowych
wymaga kadru.

| Działanie | Dotknięcia | Uwagi |
|---|---|---|
| **Profilowe z kadrem** (podgląd → „Ustaw jako profilowe” → przesunięcie albo dotknięcie twarzy, przybliżenie → „Gotowe”) | 2 + 1–3 gesty | było 1 (bez kadru) — D2 |
| **Poprawa kadru profilowego z formularza** (1a → nagłówek profilowego → „Popraw kadr” → gesty → „Gotowe” → wstecz → „Zapisz”) | 6 + 1–3 gesty | główny przypadek: pierwsze zdjęcie osoby to zdjęcie grupowe i zostało profilowym ze środka (D3) |
| **Zdjęcie grupowe, każda z 4 osób z własnym kadrem** | 4 × 6 + gesty | kadr należy do łącza, więc ustawia się go w formularzu każdej osoby osobno (AC 2) |
| Osoba, której profilowe wypada dobrze ze środka | **+0** | K się nie otwiera (D3) |

Przy ok. 20 kadrach: ok. 20 × 6 = **ok. 120 dotknięć** plus gesty, w zamian za twarz zamiast środka zdjęcia grupowego w
każdym okręgu osoby.

## Style B rules applied
- **Reguła 14 (v1.10):**
  - **ramka kadru to jedyny element na zdjęciu** — ten ekran wybiera część zdjęcia, więc okrąg musi na nim leżeć. Bez
    tekstu i przycisków na zdjęciu: „Gotowe” stoi pod nim (v1.2: bez podpowiedzi i lup);
  - okrąg, bo to profilowe osoby (okrąg tylko dla profilowego);
  - bez filtrów: przyciemnienie poza okręgiem to warstwa interfejsu wokół kadru, nie zmiana zdjęcia — w okręgu zdjęcie
    jest takie, jak w profilowym;
  - gesty z alternatywą jednym dotknięciem (*Thresholds* → gesty, D7).
- **Reguła 1:** jeden wypełniony przycisk — „Gotowe” — i jedyny przycisk ekranu (v1.2).
- **Reguła 2:** bez poświaty na okręgu — kontrast niesie pierścień (D10).
- **Reguła 3:** `broken_image_outlined` w tekście pomocniczym.
- **Reguła 10:** „Gotowe” kończy się widokiem zdjęcia z nowym stanem („Zdjęcie profilowe”), bez okienka; wstecz bez okna.
- **Kontrast** (tokeny z `theme.dart`, wzór WCAG): pierścień w akcencie wobec linii w kolorze tła — **8,81:1** (SC 1.4.11 ✅)
  na każdym zdjęciu, bo linie tła oddzielają pierścień od zdjęcia z obu stron. Sam akcent na białym fragmencie zdjęcia
  miałby ok. 2,1:1 — stąd linie (D10). Linie pomocnicze to pomoc, a nie informacja potrzebna do zrozumienia treści ani
  stan kontrolki, więc SC 1.4.11 ich nie obejmuje. Cień w kolorze tła trzyma je widoczne na jasnym zdjęciu.
- **Tokeny:** bez nowych.

## AC → element
| AC (ISSUE-018) | Element(y) | Jak widać spełnienie |
|---|---|---|
| Na zdjęciu grupowym kadr profilowego jednej osoby; okrąg pokazuje ten kadr w formularzu, w karcie grobu i w nagłówku zdjęć osoby | [[zdjecie]] B4' „Ustaw jako profilowe” → K2, K5 → [[wpis-osoby]] 1a, [[grob]] 5, [[zdjecia-osoby]] 2 | twarz wybrana w okręgu K2 jest po „Gotowe” w nagłówku bazy zdjęć, w okręgu formularza, a po „Zapisz” w karcie osoby w widoku grobu |
| Dwie osoby na tym samym zdjęciu mają różne kadry; plik jest jeden i się nie zmienia | K (w formularzu każdej osoby osobno) | okrąg pierwszej osoby pokazuje jej twarz, drugiej — jej twarz; w magazynie aplikacji jeden plik, bajt w bajt ten sam przed kadrem i po nim (`qa`) |
| Kadr da się poprawić | [[zdjecie]] B4' „Popraw kadr” → K (stan „kadr łącza”) | K otwiera się na zapisanym kadrze; po zmianie i „Zapisz” okręgi pokazują nowy |
| Kadr jest w kopii i wraca po odtworzeniu, z odciskiem zgodnym | n/a — bez elementu ekranu | warstwa danych, sprawdza `qa`; na ekranie: po odtworzeniu okręgi pokazują te same kadry |
| Migracja v4→v5; kopia v4 w v5; kopia w tle po migracji | n/a — bez elementu ekranu | warstwa danych, sprawdza `qa`; na ekranie: po migracji okręgi pokazują środek, jak przed nią (łącza bez kadru — D3) |
| Styl B (reguła 14; gesty z alternatywą jednym dotknięciem — SC 2.5.1) | K2 | reguły wyżej; dotknięcie twarzy zastępuje przesunięcie, a podwójne dotknięcie rozsunięcie palców (v1.2); przegląd `ui` przed stopem #2 |

## Decisions
| Decyzja | Dlaczego | Obali |
|---|---|---|
| **D1 — nieruchomy okrąg, pod nim przesuwa się i przybliża zdjęcie** (a nie okrąg przesuwany i powiększany na całym zdjęciu, jak w opisie pozycji i jak region w Gramps) | twarz na starym zdjęciu grupowym jest mała: przy 2048 px pokazanych na ok. 360 dp twarz osoby z dziesięciu w rzędzie ma ok. 20 dp, więc okrąg tej wielkości trudno ustawić palcem i ocenić. Pod nieruchomym okręgiem twarz przybliża się do ok. 300 dp, a okrąg pokazuje dokładnie to, co profilowe, zawsze w tej samej wielkości. Gramps zaznacza region myszą na komputerze; na telefonie zdjęcie profilowe ustawia się przesuwaniem i przybliżaniem zdjęcia pod okręgiem (*Prior art*). Zapis jest ten sam (kwadrat w obrazie), więc wybór dotyczy tylko gestów | autor na makiecie (stop #1) albo na stopie #2 woli widzieć całe zdjęcie i przesuwać okrąg → okrąg ruchomy z przybliżaniem widoku; zapis kadru bez zmian |
| **D2 — „Ustaw jako profilowe” prowadzi przez kadr** | profilowe to okrąg, więc autor widzi wycinek, zanim zdjęcie zostanie profilowym (*„gdy wybieram dane zdjęcie, to mogę ustalić jego kadr”*). Koszt: +1 dotknięcie („Gotowe”), gdy środek wystarcza | autor ustawia profilowe głównie z portretów, gdzie środek wystarcza, i „Gotowe” go spowalnia → „Ustaw jako profilowe” od razu, kadr tylko przez „Popraw kadr” |
| **D3 — bez kadru = największy kwadrat ze środka; K nie otwiera się sam** | tak działa dziś każdy okrąg, więc łącza z v4 po migracji wyglądają jak przed nią. Pierwsze zdjęcie osoby zostaje profilowym samo ([[zdjecia-osoby]]), także zdjęcie zaznaczone u osoby bez zdjęć w „Kto jest na zdjęciu?” ([[zdjecie]] D). W obu przypadkach K się nie otwiera — portret pojedynczej osoby zwykle wypada dobrze ze środka, a kadr poprawia się w 6 dotknięciach (*Tempo*) | przy przepisywaniu większość pierwszych zdjęć osób to zdjęcia grupowe i autor poprawia kadr prawie każdemu → K otwiera się sam po dodaniu pierwszego zdjęcia osobie bez zdjęć |
| **D4 — okrąg zawsze cały na zdjęciu** | wycinek poza obrazem to w GEDCOM 7 błąd (`LEFT + WIDTH` nie może przekroczyć szerokości obrazu), więc taki kadr nie przeżyłby eksportu. Koszt: twarz przy samej krawędzi zdjęcia nie stanie na środku okręgu | autor chce twarz z krawędzi zdjęcia na środku profilowego → tło poza zdjęciem w okręgu, z zapisem innym niż `CROP` |
| **D5 — największe przybliżenie: okrąg obejmuje 128 px zdjęcia** (ok. 1/12 krótszego boku zdjęcia 2048 × 1536) | mniejszy wycinek byłby w nagłówku 96 dp (ok. 250 px ekranu przy gęstości 2,6) rozmyty ponad dwukrotnie. Szczegół i tak ogranicza kopia dostępowa 2048 px ([[ADR-008-photos-access-copy-and-backup-consistency]]), a oryginał zostaje w galerii | twarze na zdjęciach, które autor dodaje (np. klasowych), są mniejsze niż 128 px → niższy limit albo kadr z oryginału (osobna pozycja) |
| **D6 — linie pomocnicze: trójpodział, zawsze widoczne** | o linie prosił autor. Trójpodział zna z siatki aparatu w telefonie: oczy na górnej linii, twarz między pionowymi. Zawsze widoczne, bo ekran istnieje tylko po to, żeby ustawić kadr | linie przeszkadzają ocenić twarz → widoczne tylko w trakcie przesuwania |
| ~~**D7 — gesty z alternatywą: dotknięcie i lupy**~~ — **zastąpione przez D7'** (stop #2) | przesunięcie palcem → dotknięcie twarzy; rozsunięcie palców → „Pomniejsz”/„Powiększ” z krokiem 1,5× | autor nie potrzebuje lup — obalone na stopie #2 |
| **D7' — gesty z alternatywą jednym dotknięciem, bez widocznych przycisków** (v1.2, decyzja autora — opcja A; WCAG 2.2 SC 2.5.1, poziom A: *„All functionality that uses multipoint or path-based gestures for operation can be operated with a single pointer without a path-based gesture”*) | przesunięcie palcem → **dotknięcie twarzy** przenosi ją na środek okręgu; rozsunięcie palców → **podwójne dotknięcie** przybliża ×2 w tym miejscu (od całości do 128 px: 4 podwójne dotknięcia), a przy największym wraca do całości — jak w [[zdjecie]] B2, który autor zna. Działa jedną ręką, gdy w drugiej jest album. Koszt: pojedyncze dotknięcie czeka ok. 0,3 s, czy nie przyjdzie drugie | pojedyncze dotknięcie wydaje się ospałe → dotknięcie bez czekania, a przybliżenie tylko dwoma palcami (nazwana luka SC 2.5.1) |
| **D8 — w podglądzie stan „profilowe” przechodzi do podtytułu paska, a na jego miejscu staje „Popraw kadr”** ([[zdjecie]] v1.4) | „Kadr da się poprawić” (AC 3) potrzebuje działania przy profilowym. Dolny pasek ma dwa stałe miejsca, żeby „Usuń z tej osoby” nie skakało pod palcem (przegląd `ui` ISSUE-017), więc „Popraw kadr” zajmuje miejsce tekstu „✓ Profilowe”, a stan niesie tekst w pasku „Zdjęcie profilowe” — tekst, nie kolor (SC 1.4.1) | autor na stopie #2 nie widzi, które zdjęcie jest profilowe → stan wraca do dolnego paska, a „Popraw kadr” obok |
| **D9 — wstecz bez okna** | przepada najwyżej ustawienie okręgu, które odtwarza się w kilka sekund ([[style-b]] reguła 10), jak wstecz w [[zdjecie]] D | — |
| **D10 — pierścień w akcencie z liniami w kolorze tła z obu stron** | kontrastu z dowolnym zdjęciem nie da się zagwarantować (sam akcent na białym niebie: ok. 2,1:1). Linie tła oddzielają pierścień od zdjęcia, więc pierścień ma 8,81:1 wobec sąsiedniego koloru na każdym zdjęciu. Akcent, bo okrąg to zaznaczenie ([[style-b]] → *Token roles*) | — |

## Open
brak. **Na stopie #1:** D1 (nieruchomy okrąg zamiast ruchomego z opisu pozycji) i D2 (+1 dotknięcie przy „Ustaw jako
profilowe”) — rekomendacje w *Decisions*, nie luki. Jednostka zapisu kadru (piksele albo ułamki) — ADR w `planning`.
