---
screen: "Drzewo — rodzina od osoby, poziomy połączeń, czas; połącz dwie osoby"
items: ["[[SPIKE-004-mvp-flow-prototype]]"]
us: "do rozpisania — M9, M10, M11 w [[EPIC-003-zrozumienie]]; czytelność na telefonie: [[SPIKE-002-tree-on-a-phone]] (H4)"
journey-step: "widok 5 (M9–M11, R3)"
mockup: "2026-10-08: grobing-prototyp.html (SPIKE-004, panel 6, runda 2) — katalog tymczasowy sesji, ścieżka w SPIKE-004"
updated: 2026-10-08
---

# Drzewo — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.16) · referencja: [[references]] → **R3**.
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

## Purpose
Zobaczyć rodzinę wokół wybranej osoby i jak się łączy (M9), jak zmieniała się w czasie (M10) i jak dowolne dwie osoby
są spokrewnione (M11). Tak samo zbudowane jest mini-drzewo w [[osoba]] (element 6).

## Navigation
- **Zakładka „Drzewo”** w dolnym pasku. Na starcie w środku jest „Ja”.
- **„Pokaż w drzewie”** w [[osoba]] → ta osoba w środku.
- **Dotknięcie osoby → ona staje w środku**; dotknięcie osoby w środku albo „Pokaż” w karcie → [[osoba]] (zakładka Drzewo
  zostaje aktywna).
- **Ikona „Połącz dwie osoby”** w pasku → okno z dwoma kaflami → po wybraniu drugiej osoby **z powrotem na drzewie**, z
  animacją ścieżki (v1.1, D26). Dotknięcie drzewa albo wstecz kończy podświetlenie.

## Elements in order
**Tryb „Drzewo”**

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek „Drzewo” i po prawej **ikona „Połącz dwie osoby”** (`conversion_path`, akcent, cel 48 dp, `tooltip` „Połącz dwie osoby”) — **bez podpisu** (v1.1) | pasek + przycisk-ikona | → okno wyboru (7) | — | — | R3 · **decyzja autora** (D26) |
| 2 | ~~Legenda linii~~ — **bez legendy** (v1.1, D25). Rodzaj linii niesie kształt i styl (łamana z góry — rodzic–dziecko; pozioma ciągła — małżeństwo; przerywana — razem), więc kolor nie jest jedynym nośnikiem (SC 1.4.1) | — | — | — | — | **decyzja autora** (D25) |
| 3 | **Poziom połączeń**: „−” · „Poziom 2” + „15 osób” · „+” na powierzchni, przyciski 36 dp w akcencie. **Poziom 1:** rodzice, partnerzy, dzieci. **Poziom k ≥ 2:** do tego rodzice, partnerzy, dzieci i **rodzeństwo** każdej osoby z poziomu k−1 (np. rodzeństwo, rodzeństwo partnerów, dziadkowie, teściowie, wnuki). Zakres 1–5 | przycisk-ikona ×2 | − / + | 2 | — | **decyzja autora** (D20) · D2 |
| 4 | **Drzewo**: rzędy według pokolenia (wyżej starsze), osoba w środku z pierścieniem w akcencie; rodzeństwo z boku osoby, po stronie dalszej od partnera; **rodzina partnera po prawej**, bez przeplatania z krewnymi. Węzeł 44 dp (profilowe albo inicjały), imię 12 sp półgrube; **zmarły ma znicz** w rogu węzła ([[style-b]] reguła 8, R3). Linie: **rodzic–dziecko** — kolor relacji rodzic–dziecko, łamana z góry w dół; **małżeństwo** — kolor partnerów, ciągła, pozioma; **razem (bez ślubu)** — kolor partnerów, przerywana 5/4. Przewijanie w obu osiach, środek ustawia się na osobie | drzewo | dotknięcie → osoba w środek; drugie → [[osoba]] | „Ja” | — | R3 · D1, D3, D4 |
| 5 | **Karta osoby w środku** (dolny arkusz): profilowe 40 dp, imię, lata · pokrewieństwo („1925–2004 · Twoja babcia”), przycisk tekstowy „Pokaż ›” (akcent) | karta | → [[osoba]] | — | — | D1 |
| 6 | **Czas (M10):** przycisk ▶ / ❚❚ (36 dp, akcent), „1880”, suwak (akcent), rok w akcencie („dziś” na końcu). **Rok Y:** osoba urodzona po Y znika (miejsce zostaje, żeby drzewo nie skakało); para łączy się linią „razem” od daty początku związku, a ciągłą od ślubu; zmarły do Y ma znicz. ▶ przechodzi od 1880 do dziś w ok. 7 s | suwak + przycisk | przeciągnięcie; ▶ | dziś | — | R3 (suwak) · **decyzja autora** (D20) · D4 |

**„Połącz dwie osoby” na drzewie (M11, v1.1)**

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 7 | **Okno „Połącz dwie osoby”** (v1.1): dwa kafle na powierzchni — „Od” i „Do” (podpis 13 sp, profilowe 40 dp albo „Wybierz osobę”). Kafel → lista osób jak [[osoby]] (wyszukiwarka i A–Z). „Od” domyślnie „Ja” | okno z kaflami | kafel → lista; **wybór drugiej osoby zamyka okno** i uruchamia 8 | Od: „Ja” | — | **decyzja autora** (D26) · R3 |
| 8 | **Ścieżka na drzewie** (v1.1): drzewo przechodzi na **najniższy poziom, na którym widać drugą osobę**, i ustawia się tak, żeby ścieżka była w kadrze; **osoby spoza ścieżki wyszarzone** (krycie ok. 30%), osoby ze ścieżki podświetlone; **linia w akcencie biegnie powoli ode mnie do kolejnych osób** (ok. 0,7 s na krok), każda osiągnięta osoba dostaje pierścień w akcencie | animacja na drzewie | dotknięcie drzewa / wstecz → koniec podświetlenia | — | — | **decyzja autora** (D21, D26) · D5 |
| 9 | **Baner na chwilę** (ok. 4 s) u góry drzewa, na powierzchni: **kim ta osoba jest dla mnie** — opis złożony z odcinków, np. „Siostra cioteczna babci mojej żony” (16 sp, półgruby); bez zdania ścieżki i **bez „Odtwórz jeszcze raz”** | baner | znika sam | — | — | **decyzja autora** (D26) · D6 |
| 10 | **Bez ścieżki:** baner „Te osoby nie łączą się — w drzewie brakuje rodziny między nimi.”, drzewo bez zmian | baner | — | — | — | reguła 9 |

## States
| Stan | Co widać |
|---|---|
| drzewo | 1–6 |
| rok w przeszłości | 4 bez osób nieurodzonych, linie par według dat związku, 6 z rokiem |
| połącz — wybór | 1, okno 7 nad drzewem |
| połącz — ścieżka | 1, 3–6, 8 (reszta wyszarzona), 9 przez ok. 4 s |
| bez ścieżki | 1, 3–6, 10 |
| osoba bez rodziny | 4: tylko ona; 5 |
| wczytywanie | wskaźnik postępu |

## Sketch
```
┌──────────────────────────────────┐
│ Drzewo                        ↝  │  ← ikona „Połącz dwie osoby”
│                     ( − Poziom 2 +)│  ← do przeprojektowania (Open 1)
│  (R)━(A)       (J)━(M)           │  ← ━ małżeństwo (róż), │ rodzic–dziecko (niebieski)
│    │             │               │
│ (E) (M)━━━━━(A)  (S)  (P)━(H)    │  ← rodzina partnera po prawej
│        │               │         │
│   (O) [JA]━━━━━(K)  (Mi)         │
│          │                       │
│        (Z)                       │
│ ╭──────────────────────────────╮ │
│ │ (Ja) Ja  ur. 1983    Pokaż › │ │
│ │ ▶ 1880 ━━━━━━━━━━━━━━●  dziś │ │
│ ╰──────────────────────────────╯ │
│  Mapa      Osoby      Drzewo     │
└──────────────────────────────────┘
```

## Tempo
n/a — ekran do oglądania.

## Style B rules applied
- **Nowa rola — kolory relacji** ([[style-b]] v1.16): rodzic–dziecko i partnerzy, każda ≥ 3:1 na tle (SC 1.4.11). Między
  sobą różnią się tylko odcieniem (1,04:1), więc **rodzaj linii niesie też kształt i styl**: rodzic–dziecko łamana z góry
  w dół, para pozioma, „razem” przerywana — i legenda (SC 1.4.1).
- **Reguła 1 (akcent):** ścieżka „Połącz dwie osoby”, osoba w środku, aktywny segment i suwak — wybór i fokus, nie relacje.
- **Reguła 8:** znicz na węźle osoby zmarłej (R3).
- **Reguła 14:** węzły to okręgi profilowego w kadrze; bez zdjęcia — inicjały.
- **Reguła 2:** poświata tylko na osobie w środku i na zapalonych węzłach ścieżki.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| M9 — drzewo rodziny z powinowatymi i powtórnymi związkami | 3, 4 | poziom 2 od „Ja”: rodzice, dziadkowie, rodzeństwo, żona i jej rodzina po prawej |
| M10 — suwak czasu: urodzenia, związki, zgony | 6 | rok 1984: „Ja” jest, rodzice „razem” (przerywana), ślub 1985 — ciągła |
| M11 — ścieżka między dowolnymi dwiema osobami | 7–9 | „Ja” → „Zofia Próbna”: drzewo na poziomie 3, linia biegnie przez Kasię i Piotra, reszta wyszarzona, baner „Babcia mojej żony” |

## Decisions
- **D1 — drzewo od osoby z przestawianiem środka** (SPIKE-004 D20; kandydat 3 ze SPIKE-002). Na telefonie całe drzewo
  ok. 100 osób jest za szerokie; od osoby widać to, o co się pyta. *Obali:* SPIKE-002 pokaże, że cały widok jest czytelny
  i potrzebny — wtedy dodatkowy tryb „całe drzewo”.
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
- **D7 — przybliżanie i oddalanie** (v1.1, D25). Gesty jak na mapie (szczypanie, przeciąganie, podwójne dotknięcie),
  z alternatywą jednym dotknięciem ([[style-b]] *Thresholds* → gesty).

## Open
1. ⚠️ OPEN — **sterowanie poziomami — nowy wygląd** (D25: *„nie wygląda to estetycznie”*). Kandydat do pokazania przy
   pozycji: **oddalanie odsłania kolejne poziomy** (przybliżenie semantyczne — oddalasz, a drzewo dokłada dalszą
   rodzinę), bez osobnych przycisków; drugi — suwak „bliżej · dalej” w dolnej karcie. Makieta albo emulator przed planem
   (retro 2, R6).
2. ⚠️ OPEN — **pokazanie drzewa na telewizorze** (D25). Kandydaci: (a) **systemowe przesyłanie ekranu Androida**
   („Przesyłaj ekran” / Smart View) — działa z każdą aplikacją, bez kodu; (b) do tego **tryb prezentacji** w aplikacji:
   poziomo, pełny ekran, większe węzły, bez przycisków; (c) Google Cast z odbiornikiem na telewizorze — dużo pracy, sieć
   i dane rodziny przez sieć lokalną ([[NFR-005-dane-nie-opuszczaja-telefonu]]). Rekomendacja `ui`: (a) + (b). Decyzja
   przy pozycji drzewa.
2a. ~~⚠️ OPEN — trzeci rodzaj linii (adopcja)~~ — nie (autor: *„linie są super”*).
3. ⚠️ OPEN — **czytelność ok. 100 osób na telefonie** — [[SPIKE-002-tree-on-a-phone]] (H4), na danych o kształcie
   prawdziwej rodziny.
