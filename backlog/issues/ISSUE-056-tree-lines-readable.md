---
title: "ISSUE-056 — Tree lines a large family can read: who is whose child at a glance, without parallel rails crossing other families"
type: issue
status: done
delivery-style: task-level
priority: SHOULD
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-009-drzewo-od-osoby]]"
depends-on: "[[ISSUE-033-tree-from-a-person]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-23
verdict-reviewer: self-check
source: "`/pm` 2026-10-22 — pierwsze użycie MVP z prawdziwą rodziną, uwaga autora *„linie się przecinają i nie wiem, kto jest synem kogo”* (`CURRENT_STATE.md` → *In progress*, pozycja 5 kolejki); `/pm` 2026-10-23 — pytanie o cel (retro 4, R1): **„całe drzewo”** + zrzut z telefonu; rozpisanie `docs` w auto-flow po `pm`, 2026-10-23"
created: 2026-10-23
updated: 2026-10-23
---

# ISSUE-056 — Linie drzewa czytelne przy dużej rodzinie

> Autor 2026-10-23 w `/pm`, na pytanie „przy całym drzewie czy przy jednej osobie?”: **„całe drzewo”** — *„nie podoba mi się to, że te niebieskie
> linie się przecinają, przez co łatwo się gubię, jak połączone są te osoby”*. Do tego zrzut z telefonu z **prawdziwą rodziną** — w vaulcie tylko
> struktura (*What the screenshot shows*), bez imion i zdjęć (`family-data.md` w `grobing-agents`).
>
> Rozpisanie przed `ui` (retro 4, R2). **Pozycja zmienia ekran drzewa → `ui` w trybie discovery, klikalny prototyp przed `planning`.** Prawdopodobnie
> bez zmiany bazy (v15) — aktualizacja ze sklepu przed wyjazdem na Wszystkie Święte (`CURRENT_STATE.md` → *In progress*, „Zasady terminu”).

## Why
Drzewo ma pokazać rodzinie przy telefonie i na telewizorze, kto jest czyim dzieckiem. Przy prawdziwej rodzinie, większej niż wymyślone dane w
emulatorze w miejscach, gdzie rodziny się przeplatają, linie rodzic–dziecko tego nie mówią: autor, który zna tę rodzinę, *„łatwo się gubi”*. Wybór
„całe drzewo” wyklucza odpowiedź „dotknij osoby, a podświetlą się jej linie” jako **główną** — obraz ma być czytelny bez dotykania, także na
telewizorze, gdzie nikt nie dotyka.

## What the screenshot shows (sama struktura)
Telefon autora w pionie, zakładka Drzewo, skala bliska 1, pięć rzędów pokoleń:
- **między rzędem rodziców a rzędem dzieci biegną cztery równoległe, poziome szyny rodzic–dziecko** w tym samym niebieskim kolorze, kilka dp od
  siebie, przez całą szerokość ekranu i dalej poza kadr;
- **dzieci dwóch–trzech rodzin stoją przemieszane w jednym rzędzie**: pionowa kreska dziecka schodzi z jednej szyny i przecina po drodze dwie–trzy
  szyny innych rodzin; z kadru nie da się odczytać, z której szyny schodzi;
- **para rodziców stoi daleko od swoich dzieci** — pionowa kreska od pary schodzi przy jej krawędzi kadru, a dzieci są po drugiej stronie;
- niżej to samo w mniejszej skali: szyna od jednej pary biegnie pod inną osobą i skręca w górę do pary obok;
- wieńce i profilowe działają; problem dotyczy tylko linii rodzic–dziecko (niebieskich). Linie par (różowe, ciągła i przerywana) są czytelne.

Zrzut leży poza repo, w katalogu tymczasowym sesji (*Notes*); do vaulta nie trafia.

## Where this comes from in the code (dla `ui` — mechanizm, nie rozwiązanie)
`grobing-code/lib/app/tree/tree_layout.dart`:
1. **Kolejność w rzędzie** — środki ciężkości (*barycentres*), 10 przejść w dół i w górę, wygrywa kolejność z najmniejszą liczbą skrzyżowań
   (`crossings()`); **położenie w rzędzie** — regresja izotoniczna (60 przejść). Algorytm z makiety SPIKE-002 ([[drzewo]] *Candidates — SPIKE-002*).
2. **`crossings()` liczy skrzyżowania prostych od środka rodziców do dziecka**, a ekran **rysuje coś innego**: każda para dostaje poziomą szynę od
   miejsca zejścia do najdalszego dziecka (`_lines`), a szyny, które by się nałożyły, dostają własną wysokość — do 4 poziomów co 7 dp. Skrzyżowanie
   „pionowa kreska dziecka × szyna innej rodziny” **nie wchodzi do liczby, którą algorytm zmniejsza** — może być ich dużo przy małym `crossings()`.
3. **Pomiar z makiety SPIKE-002** (od „Ja”, wymyślona rodzina 106 osób): skrzyżowania 0 / 0 / 6 / 9 / 10 na poziomach 1–5 — **ta sama miara co (2)**,
   więc nie mówi, ile przecięć widzi oko.

Wniosek do sprawdzenia przez `ui` (*Open* 1): część problemu może siedzieć w mierze, a nie w samym rysunku. Specyfikacja zapisała już granicę:
*„każda kolejność w rzędzie coś krzyżuje”* — to cecha kraty ([[drzewo]] D8), nie algorytmu. Przecięć może być mniej, ale nie zero.

## What to build (kierunek — szczegóły `ui`)
- **na pierwszy rzut oka widać, kto jest czyim dzieckiem** — przy całym widoku drzewa na telefonie i na telewizorze, bez dotykania;
- linie par (ciągła, przerywana, „//”), wieńce, ścieżka „Połącz dwie osoby” (D49, D79), ślad dalszej rodziny (D9), poziomy (D50), suwak czasu i
  „Następne” działają jak dziś — ścieżka biegnie po szynach (`pathRoute`), więc **każda zmiana szyn zmienia też jej trasę**;
- bez zmiany bazy (v15), wersja `1.0.4+7` — przed wyjazdem.

## Acceptance Criteria (runda 2 — `planning` po decyzji autora na prototypie, 2026-10-23)
- [ ] **AC-1 — miara, którą widzi oko** ([[drzewo]] D84). Na wymyślonej rodzinie (`lib/dev/fictional_family.dart`, od „Ja” = Mateusz) narysowane przecięcia
      linii rodzic–dziecko (pionowa kreska × szyna innej rodziny) na poziomach 1 / 2 / 3: **dziś 9 / 19 / 27 → po zmianie 9 / 17 / 22** (sonda na kodzie
      aplikacji), szyn jedna nad drugą w jednej przerwie najwyżej 4; **miejsca osób identyczne jak przed zmianą** (D86).
- [ ] **AC-2 — mostek łukiem** (D83). *Given* kreska dziecka (albo rodziców) przechodzi przez szynę innej rodziny *Then* przeskakuje ją łukiem w prawo, 4 dp
      szerokim, od 4 dp nad szyną do 4 dp pod nią, w kolorze i grubości kreski, a szyna zostaje ciągła; *Given* kreska przechodzi przez dwie szyny 7 dp od
      siebie *Then* jeden łuk nad obiema. Kreska, która nic nie przecina, zostaje prosta.
- [ ] **AC-3 — reszta drzewa bez zmian** (D83, D86). Linia ścieżki „Połącz dwie osoby” przez mostek idzie tym samym łukiem; ślad dalszej rodziny, linie par,
      „//”, wieńce, poziomy i tryb prezentacji jak dziś. **Suwak czasu:** piętro każdej szyny to samo w każdym roku (drzewo nie skacze — [[ISSUE-037-time-on-the-tree]]
      AC-1), a mostek jest tylko tam, gdzie w danym roku są obie linie.
- [ ] **AC-4 — płynność.** Klatki drzewa przy przesuwaniu, przestawieniu środka i ▶ nie gorsze od buildu odniesienia `1.0.3+6` (pomiar naprzemienny, retro 4 R3).
- [ ] Linie dalej poza czytnikiem; kolory bez zmian (D85). Tekst 200% — bez sprawdzania (decyzja autora 2026-10-23, [[style-b]] v1.53).

## Open for `ui` (przed planem; kandydaci na prototypie — retro 2, R6)
> **Rozstrzygnięte 2026-10-23** przez `ui` z autorem na prototypie `prototyp-056.html` — [[drzewo]] v1.31 (*Candidates — ISSUE-056*, D83–D86), [[style-b]] v1.55.
> Open 1: wymyślona rodzina odtwarza obraz ze zrzutu (4 szyny w przerwie na poziomie 3), algorytm liczy 3 przecięcia tam, gdzie ekran rysuje 9.

1. **Najtańszy falsyfikator najpierw.** Zanim powstanie prototyp: policzyć na wymyślonej rodzinie, ile jest dziś skrzyżowań **rysowanych** linii i
   równoległych szyn (AC-1) i czy wymyślona rodzina w ogóle odtwarza obraz ze zrzutu (dzieci kilku rodzin przemieszane w rzędzie, cztery szyny). Jeśli
   nie odtwarza — dołożyć do prototypu wymyśloną gałąź, która go odtwarza (powtórne związki, kuzyni po obu stronach), zanim kandydaci zostaną ocenieni.
2. **Kandydaci** (z `/pm` 2026-10-22, do sprawdzenia i uzupełnienia o prior art):
   - **kolejność według rysowanych linii** — algorytm zmniejsza skrzyżowania szyn, nie prostych; dzieci jednej pary obok siebie i pod nią;
   - **krótsze szyny** — szyna tylko nad własnymi dziećmi, zejście od pary przesunięte; przy dalekiej parze łamana zamiast szyny przez cały rząd;
   - **mostki** — w miejscu skrzyżowania kreska dziecka przeskakuje nad cudzą szyną (łuk albo przerwa), jak na schematach elektrycznych;
   - **kolor linii na parę rodziców** — szyny sąsiednich rodzin w różnych odcieniach (ile odcieni przy 3:1 na tle i bez kolizji z kolorem par i akcentem);
   - **więcej miejsca między szynami** — dziś 7 dp, przy oddaleniu jeszcze mniej na ekranie;
   - podświetlenie linii dotkniętej osoby — **tylko jako dodatek**: autor wybrał „całe drzewo” (*Why*).
3. **Prior art** — co robią drzewa genealogiczne i genogramy przy przeplatających się rodzinach (np. programy genealogiczne z układem warstwowym,
   rysowanie grafów warstwowych — Sugiyama i miary skrzyżowań linii łamanych), z cytatem źródła ([[drzewo]] D8 — TimeNets już jest).
4. **Koszt kandydata w kodzie** — który z nich zmienia tylko rysowanie (`_lines`), a który kolejność i położenie (`tree_layout`), a więc też miejsca
   osób, które autor już zna na pamięć. Wybór opisany tym, co autor zobaczy (pamięć: nazwa opcji po źródle).
5. **Prototyp** — klikalny, `file:///`, na wymyślonej rodzinie, ekran telefonu i podgląd telewizora obok (*Do retro* ISSUE-050); przy każdym kandydacie
   liczby z AC-1. Kandydaci na emulatorze albo makiecie **przed rekomendacją** (`autonomous-flow.md` → stop #1).

## Out of scope
- tabliczka imienia zasłaniająca ślad dalszej rodziny (MINOR z [[ISSUE-035-tree-names-shrink-my-voice]]) — *Poza tą kolejnością*; chyba że kandydat
  i tak przesuwa szyny i ślad — wtedy decyzja na stopie #1;
- rodzeństwo przyrodnie w słowniku — *Poza tą kolejnością*;
- mapa migracji, animacje opowieści — pozycja 6 kolejki ([[2026-10-14-opowiesc-rodziny-i-wieniec]]);
- tekst 200% (decyzja autora 2026-10-23).

## What this will not give
- **Zera przecięć** — rodzina to krata ([[drzewo]] D8): przy powtórnych związkach i kuzynach po obu stronach każda kolejność coś krzyżuje.
- Zmiana kolejności w rzędzie przestawi osoby, które autor już zna z telefonu — koszt do pokazania na stopie #1, nie do odkrycia po aktualizacji.

## Notes
- Kod: `lib/app/tree/tree_layout.dart` — `crossings()`, kolejność i położenie w rzędzie, `_lines` (szyny, `byGap`, wysokości `ty − 9 − k × 7`),
  `_rails` i `pathRoute` (ścieżka po szynach); rysowanie — `tree_painter.dart`.
- **Dane rodziny:** zrzut autora z prawdziwą rodziną jest w katalogu tymczasowym sesji
  `%TEMP%\claude\c--Programowanie-Grobing-grobing-agents\6d4e489c-…\images\` — poza repo, do kosza po pozycji (`CURRENT_STATE.md` → *Autor, poza
  sesją*). Przed `git add` skan zmian po imionach ze zrzutu (pamięć: skan po odczycie danych rodziny), przykłady w prototypie i testach tylko z
  wymyślonych rdzeni.

## Stop #1 (2026-10-23) — ✅ „tak”
Prototyp `prototyp-056.html` (wybór autora na panelu 2: *„wybrałbym opcje mostków - łuk, bez osobnych kolorów dla rodzin”* — D83, D85) i plan niżej z decyzjami
projektowymi (piętra raz na drzewo, jeden łuk nad sąsiednimi szynami, ścieżka tym samym łukiem, **kolejność w rzędzie bez zmian** — D84, D86) — autor: *„tak”*.

## Implementation plan (`planning`, 2026-10-23)
> Specyfikacje: [[drzewo]] v1.31 (elementy 4 i 8; D83–D86; *Candidates — ISSUE-056*) · [[style-b]] v1.55 (rola linii relacji — mostek). Prototyp — wybór autora to
> panel 2: `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/6d4e489c-bbef-43af-b3d5-51de0077d68d/scratchpad/prototyp-056.html#p2`.
> **Bez zmiany schematu** (v15) — migracji nie ma, kopia i odtworzenie bez zmian. Wersja **`1.0.4+7`**.

### Scope diff
1. **Piętra szyn według przecięć (D84)** — `tree_layout.dart`, `_lines`: po przydziale z lewej krawędzi (dziś) wybór piętra, które daje najmniej przecięć: dla
   dwóch zachodzących szyn „a nad b” kosztuje kreska rodziców b, gdy przechodzi przez a, plus każde dziecko a, które stoi nad b; poprawianie po jednej szynie i
   zamianą pięter dwóch szyn, dopóki koszt spada; najwyżej 4 piętra co 7 dp (jak dziś). Wzór: sonda `_optimizeTracks` w
   `C:\Users\user\AppData\Local\Temp\claude\c--Programowanie-Grobing-grobing-agents\6d4e489c-bbef-43af-b3d5-51de0077d68d\scratchpad\probe056\make_copy.py`
   (dała 9 / 17 / 22). **Piętra liczone raz dla drzewa na „dziś”** (jak `_rails`) i **te same w każdym roku suwaka** — w roku szyna jest krótsza albo jej nie ma,
   więc piętra się nie zderzają, a drzewo nie skacze przy ▶ (decyzja projektowa).
2. **Mostek (D83)** — w `_lines` (i w `linesAt` dla roku): przecięcia pionowej kreski (od rodziców do szyny, od szyny do dziecka) z szyną **innej** rodziny, bez
   końców (złącza); kolejne przecięcia na jednej kresce bliżej niż 8 dp → jeden łuk. Łuk: półelipsa w prawo, 4 dp szeroka, od 4 dp nad pierwszą szyną do 4 dp pod
   ostatnią — **zapisany jako krótkie odcinki w tych samych punktach `parentChild`** (np. 12 na łuk), więc `TreeLinesPainter` zostaje bez zmian. Liczone dla
   linii danego roku (mostek tylko tam, gdzie są obie linie).
3. **Ścieżka przez mostek** — `pathRoute` / `_down` / rodzeństwo przez szynę rodziców: pionowe odcinki trasy dostają te same łuki co linia pod nimi (trasa na
   „dziś”, D48), więc `PathLinePainter` (rysuje po długości) też zostaje bez zmian.
4. **Miara do testów (AC-1)** — publiczna liczba narysowanych przecięć układu (np. `TreeLayout.drawnCrossings`, liczona z prostej geometrii szyn, przed łukami),
   obok dzisiejszego `crossings`.
5. **Wersja** `1.0.4+7` (`pubspec.yaml`).

### Files (likely)
| Plik | Zmiana |
|---|---|
| `lib/app/tree/tree_layout.dart` | piętra według przecięć raz na układ; mostki w `_lines`; łuki w trasie ścieżki; `drawnCrossings` |
| `lib/app/tree/tree_painter.dart` | prawdopodobnie bez zmian (łuk = odcinki); zmiana tylko, gdyby odcinki nie wyglądały gładko przy skali 2,5 |
| `pubspec.yaml` | `1.0.4+7` |
| `test/app/tree/tree_layout_test.dart` (`qa`) | AC-1–AC-3 |

### AC → test / check
| AC | Test (`qa`) | Na emulatorze (`dev` przed `qa`) |
|---|---|---|
| AC-1 | `tree_layout_test`: na wymyślonej rodzinie `drawnCrossings` 9 / 17 / 22 na poziomach 1–3; `positions` identyczne jak przed zmianą (lista miejsc z `1.0.3+6` w teście); najwyżej 4 piętra w przerwie | — |
| AC-2 | geometria: mała wymyślona rodzina z dwiema zachodzącymi szynami — łuk 4 dp w prawo, ±4 dp wokół szyny; dwie szyny co 7 dp — jeden łuk; szyna bez przerwy; kreska bez przecięcia prosta | zrzut „Przez 2 związki” w miejscu z 4 szynami, przybliżony |
| AC-3 | trasa ścieżki przez mostek ma ten sam łuk; `linesAt` w kilku latach — `ry` każdej szyny jak na „dziś”; mostek znika, gdy w roku nie ma jednej z linii; ślad, pary, „//” bez zmian | ścieżka „Połącz dwie osoby” przez mostek; ▶ — szyny nie skaczą |
| AC-4 | — | klatki przesuwania, przestawienia środka i ▶ naprzemiennie z buildem `1.0.3+6` (`FRAME_LOG`); czas `layoutTree` + `linesAt` przed i po |

### Manual verification (stop #2)
**Agent na emulatorze** (`Grobing_Restore` — demo zapisane przed pozycją i wgrane z powrotem po niej, stan sprzed demo z `_pokaz`; pamięć o emulatorze):
1. drzewo od „Ja” na trzech poziomach, miejsce z 4 szynami — zrzuty przed (`1.0.3+6`) i po; łuki gładkie przy przybliżeniu;
2. „Połącz dwie osoby” przez mostek — zrzut w trakcie i na końcu animacji;
3. suwak czasu i ▶ — kilka lat, szyny na tych samych piętrach; tryb prezentacji — cały poziom;
4. klatki (AC-4) i czas układu.

**Autor: odczucie** (emulator, najwyżej 3):
1. Drzewo → „Przez 2 związki” → miejsce z kilkoma szynami: czy z łukami od razu widać, która kreska do której rodziny należy?

**Lista B** w [[ISSUE-032-mvp-install]] → *Hand checks* (telefon, prawdziwa rodzina — nie na stop #2): miejsce ze zrzutu z 2026-10-23 po aktualizacji
`1.0.4+7` — czy z mostkami wiesz, kto jest czyim dzieckiem.

### Decisions for stop #1 (projektowe — „tak” przyjmuje je z planem)
- **piętra szyn raz na drzewo, te same w każdym roku** — drzewo nie skacze przy ▶;
- **jeden łuk nad sąsiednimi szynami** (D83) — w prototypie dwa łuki zachodziły na siebie;
- **linia ścieżki przechodzi tym samym łukiem** (D83);
- **kolejność w rzędzie bez zmian** (D86) — panel 4 bez wyboru: nikt się nie przesuwa, a „Linia krwi” zostaje z 9 przecięciami, tylko z łukami.

### Out of scope
- nowa kolejność w rzędzie (kandydat D, D86) i kolor rodziny (D85);
- więcej niż 4 zachodzące szyny nad jednym miejscem — dziś piąta i dalsze dzielą 4. piętro (`math.min(k, 3)`); bez zmian, na wymyślonej rodzinie najwyżej 4;
- tabliczka imienia zasłaniająca ślad (ISSUE-035 MINOR), rodzeństwo przyrodnie, tekst 200%;
- mostki w mini-drzewie widoku osoby ([[osoba]]) — tam rysuje inny kod i nie ma szyn kilku rodzin.

### Known edges
- przy całym poziomie (telewizor, oddalenie) łuk ma ok. 1 px — przecięcie wygląda jak dziś (D83 *Nie da*);
- piętra wybrane na „dziś” w roku, w którym części szyn nie ma, mogą być wyżej, niż trzeba — cena tego, że drzewo nie skacze.

## Dev report (`dev`, 2026-10-23)
Flutter 3.41.1 (przypięty). `flutter analyze` — czysto; `dart format` — sformatowane. Bez zmiany schematu (v15). Wersja `1.0.4+7`. Zmienione: `lib/app/tree/tree_layout.dart`,
`pubspec.yaml`.

### Built
1. **Piętra szyn według przecięć (D84)** — `_lines`: lewa krawędź jak dotąd (najmniej pięter), potem `_fewestCrossings` wybiera piętro każdej szyny spośród tych pięter (po
   jednej szynie i zamianą dwóch, póki przecięć ubywa — wzór z sondy `ui`). Piętra liczone **raz dla drzewa na „dziś”** (`_RailsToday`, w miejsce `_rails`) i podawane
   do `linesAt` każdego roku (`floors:`).
2. **Mostek (D83)** — w `_lines` przecięcia kreski rodziców i kreski dziecka z szyną innej rodziny (bez końców); `_jumps` łączy przecięcia bliżej niż 8 dp w jeden łuk;
   `_drop` rysuje kreskę z półelipsą 4 dp w prawo (12 odcinków) — w tych samych punktach `parentChild`, więc `TreeLinesPainter` bez zmian. Kreska bez przecięcia daje
   te same punkty co przed zmianą.
3. **Ścieżka przez mostek** — `_down` i rodzeństwo przez szynę rodziców biegną przez `_drop` z łukami z „dziś”; bez przecięć punkty trasy są te same co przed zmianą
   (przyrodnie rodzeństwo z innej szyny — bez łuków drugiej kreski). `PathLinePainter` bez zmian.
4. **`TreeLayout.drawnCrossings`** — narysowane przecięcia na „dziś” (AC-1), obok `crossings`.
5. `pubspec.yaml` → `1.0.4+7`.

### Measurements
- **Sonda na kodzie po zmianie** (wymyślona rodzina, od „Ja”, poziomy 1 / 2 / 3; `scratchpad\emu056\check_test.dart`): `drawnCrossings` **9 / 17 / 22** (sonda `ui`: 9 / 17 / 22),
  `crossings` 3 / 14 / 26 bez zmian, **miejsca osób: 0 przesuniętych** względem eksportu sondy z `1.0.3+6`, łuków 9 / 15 / 22 (na poziomie 2 sąsiednie szyny pod jednym łukiem),
  `linesAt` ok. 1 ms (PC, JIT).
- **Klatki na emulatorze** (`Grobing_Restore`, profile z `FRAME_LOG`, ten sam przebieg: drzewo na najwyższym poziomie, 6 wolnych przeciągnięć; naprzemiennie B1, A1, B2, A2):
  | Build | Klatek | Wolne (> 16,7 ms) | build p50 / p90 µs | raster p50 / p90 µs |
  |---|---|---|---|---|
  | `1.0.3+6` A1 / A2 | 362 / 363 | 43,4% / 42,7% | 2162 / 4647 · 1768 / 4366 | 15477 / 24118 · 15247 / 24563 |
  | `1.0.4+7` B1 / B2 | 370 / 367 | **41,1% / 40,9%** | 1880 / 4011 · 1822 / 4665 | 15452 / 24915 · 15271 / 23560 |

  Bez regresji (AC-4). Wysoki raster jest w obu buildach — drzewo z wieńcami na najwyższym poziomie na tym emulatorze; to nie ta zmiana.

### Emulator pass (`Grobing_Restore`, 1080 × 2400 przy 420 dpi = 411 × 914 dp; stan sprzed demo z `_pokaz`, zrzuty `scratchpad\emu056\shots\`)
1. Drzewo od „Ja”, ten sam przebieg na obu buildach (`A1-*`, `B1-*`, wycinki `band-0`, `band-r1`): **łuk widać przy skali 1** — kreska przeskakuje dłuższą szynę, w miejscu z
   kilkoma szynami każde przecięcie ma swój łuk; miejsca osób te same.
2. „Połącz dwie osoby” „Ja” → brat stryjeczny mamy (`11-path-mid`, `12-path-end`, `12-crop`): linia w akcencie przechodzi tym samym łukiem.
3. Suwak czasu: 1973 vs „dziś” (`cmp-year`) — szyny na tych samych piętrach, mostek tam, gdzie w 1973 są obie linie; osób nienarodzonych nie ma (jak dotąd).
4. Klatki — wyżej.

### Found
- **Łuk w linii ścieżki przy małej skali** (`12-crop`): linia w akcencie ma 3 dp na ekranie przy każdej skali (element 8), a łuk 4 dp w jednostkach drzewa — przy skali ścieżki ok.
  0,75 łuk to małe wcięcie „>” w grubej linii. Zgodne ze specyfikacją (ścieżka tym samym łukiem), do oceny w przeglądzie `ui`.

- **Wersja w dwóch miejscach** (złapał test `qa` `settings_words_test`): `appVersion` w `lib/app/settings/settings_screen.dart` („O aplikacji”) został na `1.0.3` —
  poprawione na `1.0.4` (mechaniczne, bez stopu).

### Deviations (do przeglądu `ui`)
- Brak odstępstw od [[drzewo]] v1.31.

### Known edges
- jak w planie: łuk ok. 1 px przy całym poziomie (telewizor); powyżej 4 zachodzących szyn piąta dzieli 4. piętro (bez zmian).

### For `qa`
- **Test trasy ścieżki** (`tree_layout_test`: *„Never at a slant: every segment level or upright”*) przechodzi, bo ścieżka do Wandy nie trafia na mostek; trasa przez mostek ma
  odcinki łuku z założenia (D83) — test AC-3 musi je dopuszczać (np. „poziomo, pionowo albo w łuku przy przecięciu”).
- `tree_time_test` porównuje `linesAt(time, null)` z `lines` — zielone (piętra z „dziś”). Wszystkie testy `test/app/tree/` — 135 zielonych.
- **Emulator:** na `Grobing_Restore` jest **stan sprzed demo** z `_pokaz` i build profile `1.0.4+7` z `FRAME_LOG`; demo zapisane przed pozycją w
  `scratchpad\emu056\stan-demo-przed-056.tar` + `.apk` (i w `_pokaz`) — **wgrać z powrotem po stopie #2**. Zrzut `10-list.png` ma na liście osób wpis autora z emulatora (imię i
  nazwisko) — do kosza razem z katalogiem sesji.

## Verification (`qa`, 2026-10-23)
### Tests — 1055 zielonych, `flutter analyze` i `dart format` czyste
Nowy plik `test/app/tree/tree_lines_test.dart` (4 testy, wymyślona rodzina z `lib/dev`):
| AC | Test |
|---|---|
| AC-1 | od „Ja”, poziomy 1–3: `drawnCrossings` **9 / 17 / 22**, `crossings` 3 / 14 / 26, **odcisk wszystkich miejsc** = odcisk eksportu `1.0.3+6` z sondy `ui` (sprawdzony sondą `qa`: 0 przesuniętych); najwyżej 4 piętra w przerwie |
| AC-2 | poziom 2: każdy łuk wraca na swoją kreskę, 12 odcinków, wybrzuszenie dokładnie 4 dp w prawo, od 4 dp nad pierwszą do 4 dp pod ostatnią przeciętą szyną; szyny pod łukiem są całymi odcinkami przez x (bez przerwy); sąsiednie szyny < 8 dp pod jednym łukiem (jest co najmniej jeden taki); przecięcia pod łukami = `drawnCrossings`; poza łukami żadnych skosów |
| AC-3 | „Ja” → Jan (poziom 1): każdy odcinek skośny trasy leży na narysowanym łuku; trasa od osoby do osoby. Suwak (poziom 3; 1930, 1950, 1973, 1990, 2010): każda szyna roku leży na szynie „dziś” (te same piętra), każdy łuk roku jest łukiem „dziś”, wcześniej mniej łuków |

Pełny przebieg: pierwszy raz 1054 + 1 czerwony — `settings_words_test` (wersja w „O aplikacji” ≠ `pubspec.yaml`) → `dev` poprawił `appVersion` (*Dev report*); drugi raz
**1055 zielonych**. Istniejący test trasy (*„Never at a slant”*) zostaje — ścieżka do Wandy nie trafia na mostek; trasę przez mostek sprawdza nowy test AC-3.

### ui review (subagent bez historii, 2026-10-23) — 0 BLOCKER / 0 MAJOR / 2 MINOR
1. **MINOR — łuk w linii ścieżki przy małej skali** (element 8, `12-crop`): linia w akcencie 3 dp na ekranie, łuk 4 dp w jednostkach drzewa — przy skali ścieżki ok. 0,73 łuk
   wybrzusza się o ok. 2,9 dp i zamyka w „>”; litera D83 spełniona, cel przy małej skali nie. **Przyjęte bez zmiany kodu** (rekomendacja `ui`): drogę niosą pierścienie, animacja i
   baner, a linie pod ścieżką są przy 30%. Zapisane w [[drzewo]] D83 *Nie da*. Gdyby przeszkadzało: łuk ścieżki `max(4, 5 / skala)` w `PathLinePainter`.
2. **MINOR — brak zrzutu w przybliżeniu i w miejscu z 4 szynami** → zrobione przed stopem: `20-four-rails` (poziom 3, miejsce 815 dp w prawo od „Ja” — sonda: 4 szyny nad
   jednym miejscem; łuki nad 2–3 szynami naraz), `21-zoom` i `21-crop` (podwójne dotknięcie, skala ok. 1,5): łuk gładki, na stykach z kreską ząbek ok. 1 px widoczny dopiero
   przy powiększeniu pikseli — bez poprawki.

Zgodne (z przeglądu): wymiary łuku na `band-0` 3,8 × 8 dp; kreska bez przecięcia prosta; D86 — przy tych samych przesunięciach zrzuty różnią się tylko łukami; łuk nie trafia w
węzły, wieńce ani imiona; ścieżka tym samym łukiem; suwak — te same piętra; kolory bez zmian (rodzic–dziecko 8,50:1, partnerzy 8,16:1, akcent 8,81:1 na tle); SC 1.4.1 —
przecięcie od połączenia odróżnia kształt. Poza zakresem: ślad dalszej rodziny (3/3) nie przeskakuje szyn — zgodnie z D83 (tylko kreski rodzic–dziecko).

### Emulator, klatki i dane
- Przejście `dev` (*Dev report* → *Emulator pass*) i klatki naprzemiennie z `1.0.3+6`: 41,1% / 40,9% wolnych wobec 43,4% / 42,7% — bez regresji (AC-4).
- **Bez zmiany schematu** (v15): migracji i odtworzenia z kopii pozycja nie dotyka (DoD — warstwa danych nie zmieniona).
- **Dane rodziny:** zmiany w `grobing-code` (3 pliki + 1 nowy test) — tylko wymyślone rdzenie („Wymyślony”); skan po imionach ze zrzutu autora i po jego nazwisku — 0 trafień;
  vault — sama struktura zrzutu, bez imion. Zrzuty emulatora poza repo; `10-list.png` z wpisem autora — do kosza.

### Stop #2 (2026-10-23) — autor: *„tak widać”*
Krok 1 (emulator, poziom 3, miejsce z kilkoma szynami — `22-for-author`): *„czy z łukami od razu widać, która kreska należy do której rodziny?”* — **„tak widać”**, **ze śladem**:
15 klatek w logcat (`GROBING_FRAME`) po przygotowaniu widoku i drzewo przesunięte (`23-after-author` ≠ `22-for-author`).

### For ISSUE-032 → Hand checks
- **B** — telefon, prawdziwa rodzina, po aktualizacji `1.0.4+7`: miejsce ze zrzutu autora z 2026-10-23 (*„niebieskie linie się przecinają”*) — czy z mostkami wiesz, kto jest czyim
  dzieckiem (ISSUE-056, D83).
