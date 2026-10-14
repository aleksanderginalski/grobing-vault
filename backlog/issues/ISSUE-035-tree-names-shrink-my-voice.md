---
title: "ISSUE-035 — Tree: the card speaks in my voice („Moja babcia”, G2); names when zooming out stay I2 (I1 withdrawn at stop #1)"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-003-zrozumienie]]"
user-story: "[[US-009-drzewo-od-osoby]]"
depends-on: "[[ISSUE-034-tree-presentation-mode]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-14
verdict-reviewer: self-check
source: "decyzja autora na stopie #1 [[ISSUE-034-tree-presentation-mode]] (2026-10-14: „1 — I1, 2 — Moja babcia”, potem „tak” dla osobnej pozycji) · [[drzewo]] v1.8 *Open* 5 i 6 · *Candidates — US-009* (I1, G2)"
created: 2026-10-14
updated: 2026-10-14
---

# ISSUE-035 — Drzewo: „Moja” (I1 wycofane)

> Z zamknięcia [[ISSUE-034-tree-presentation-mode]] (`docs`, 2026-10-14). Autor pierwszy raz otworzył makietę `drzewo-us009.html` na stopie #1
> ISSUE-034 (adres `file:///`) i wybrał inaczej niż na stopie #1 [[ISSUE-033-tree-from-a-person]], gdzie „Tak” przyjęło rekomendacje I2 i G1.
> W kodzie są dziś I2 i G1. **Pozycja zmienia ekran → `ui` przed `planning`.**
>
> **Zamknięta 2026-10-14 (`docs`):** na stopie #1 tej pozycji autor wybrał **I2** (*„1 I2”*), więc zbudowane jest samo **G2**. Punkt 1 *What to
> build* i AC-1 wycofane decyzją autora (*Implementation plan* → *Stop #1*, [[drzewo]] D27).

## What to build
1. ~~**I1 — imiona maleją razem z drzewem** ([[drzewo]] *Candidates — US-009*, I1): przy oddalaniu imię ma wielkość skali drzewa (poziom 3 ok.
   9 sp, poziom 4 ok. 6 sp), zamiast stałych 13 sp z chowaniem nakładających się (I2).~~ — wycofane na stopie #1 (autor: „1 I2”).
2. **G2 — karta mówi Twoim głosem:** „Moja babcia”, „Siostra cioteczna babci mojej żony” (zamiast „Twoja babcia”, „…Twojej żony”).

## Acceptance Criteria
- ~~**US-009 AC-3 / [[drzewo]] *Open* 5 — I1.** *When* oddalam drzewo do poziomu 3 i 4 *Then* imiona maleją razem z drzewem i żadne się nie
      chowa.~~ — wycofane decyzją autora na stopie #1 (zostaje I2).
- [x] **US-009 AC-5 — G2.** *Given* ścieżka Ja → żona → jej mama → jej mama → jej rodzic → jego rodzeństwo → jego dziecko *Then* karta mówi
      „Siostra cioteczna babci mojej żony”; *Given* mama taty *Then* „Moja babcia”.
- [x] Przykład w US-009 AC-5 i w [[drzewo]] wraca do „mojej żony”.

## Out of scope
- Mini-drzewo w [[osoba]] (nie ma oddalania).
- Inne miejsca aplikacji, które mówią do Ciebie („Wybierz, która osoba to Ty”, „…łączy się z Tobą”) — czy też się zmieniają, rozstrzyga `ui`
  (pytania niżej); bez decyzji `ui` nic poza kartą drzewa.

## Notes
- **Pytania dla `ui` przed planem:** (a) co zamiast „to Ty” na karcie „ja” i zamiast „nie wiadomo jeszcze, kim jest dla Ciebie”; (b) czy G2 obejmuje
  baner „Połącz dwie osoby” ([[drzewo]] element 9, US-011) i opisy dla czytnika; (c) odstępstwo od progu 13 sp w [[style-b]] reguła 13 przy I1;
  (d) pomiar trybu prezentacji przy tekście 200% na 360 dp (zrzut `18b` ISSUE-034 — [[drzewo]] *Open* 5, v1.8).
- Makieta z kandydatami I1–I3 i G1–G2: `drzewo-us009.html` w katalogu tymczasowym sesji `c3868f5f-…\scratchpad` — podawać autorowi jako
  adres `file:///C:/Users/user/AppData/Local/Temp/claude/c--Programowanie-Grobing-grobing-agents/c3868f5f-084e-4101-9b20-5d98d098ca56/scratchpad/drzewo-us009.html`.
- Kod: `lib/app/tree/tree_labels.dart`, `tree_screen.dart` (`_labelScale`, `_visibleNames`), `lib/app/person/kinship_names.dart` (zaimek).

## Implementation plan
> `planning`, 2026-10-14. Specyfikacja: [[drzewo]] **v1.9** — element 4 (czytnik), element 5 (karta), *States*, D27 (imiona: zostaje I2), D28 (G2,
> kto mówi); [[style-b]] **v1.28** — reguła 7 (kto mówi). `ui` odpowiedział na pytania (a)–(d) z *Notes* w specyfikacji. Nowej makiety nie ma: I1/I2
> i G1/G2 to kandydaci z `drzewo-us009.html`.

### Stop #1 (2026-10-14) — autor odpowiedział na sekcje makiety: zostaje I2, budujemy samo G2
Autor napisał: *„1 I2, 2 „moja babcia”, 3 100%, 4 ok, 5 ok, 6 ok”*. Liczby to sekcje makiety `drzewo-us009.html`.
- **1 — I2.** Zamiast I1 ze stopu #1 [[ISSUE-034-tree-presentation-mode]] zostaje I2, które już jest w kodzie. **AC-1 tej pozycji (I1) wycofane
  decyzją autora.** Zapis I1 w [[drzewo]] i [[style-b]] `ui` cofnął przed budową ([[drzewo]] D27). Skutek, który zostaje: tryb prezentacji przy
  tekście 200% na 360 dp pokazuje 13 z 20 imion (element 11, zrzut `18b` ISSUE-034).
- **2 — „Moja babcia”** (G2): budujemy według [[drzewo]] D28, razem z decyzją projektową `ui`, którą plan pokazał na stopie (dwa głosy: nazwa
  pokrewieństwa „mój”, zdania aplikacji „Ty”). Autor nie zgłosił do niej uwag.
- **3 — „100%”:** sekcja 3 makiety („Tekst systemu”, AC-7) nie ma nic do wybrania, przełącza tylko podgląd 100% / 130% / 200%. Czytam to jako
  obejrzane bez uwag. AC-7 jest zbudowane ([[ISSUE-033-tree-from-a-person]]) i zostaje bez zmian.
- **4, 5, 6 — ok:** „Pokaż w drzewie”, tryb prezentacji i stany, wszystkie zbudowane w ISSUE-033 i ISSUE-034, bez zmian.

### Prior art (źródła, nie pamięć)
- **Kto mówi** ([[drzewo]] D28, [[style-b]] reguła 7): [Microsoft Writing Style Guide → Person](https://learn.microsoft.com/en-us/style-guide/grammar/person)
  — w interfejsie zwykle druga osoba, a „my” wolno w etykiecie, która pokazuje rzecz z punktu widzenia użytkownika. FamilySearch nazywa pokrewieństwo
  „My Grandmother” ([[drzewo]] D8).
- **Z kodu** ([[ISSUE-033-tree-from-a-person]]): nazwy pokrewieństwa daje jedna funkcja `kinshipName` (`lib/app/person/kinship_names.dart`), z zaimkiem
  w dwóch miejscach (pojedyncza nazwa i opis z odcinków). „to Ty” i „…dla Ciebie” są w `_kinOf` (`lib/app/tree/tree_screen.dart`). Karta i opis dla
  czytnika biorą ten sam tekst (`_kin`), więc zmiana w dwóch miejscach obejmuje oba.

### Decisions (przyjęte na stopie #1)
- **D28 `ui` — dwa głosy:** karta drzewa mówi „nie wiadomo jeszcze, kim jest dla mnie”, a widok osoby zostaje przy „Nie wiadomo jeszcze, jak łączy się z
  Tobą — …” pod nagłówkiem „Jak łączy się ze mną”. Zdania aplikacji („Wybierz, która osoba to Ty”, „Twoje cmentarze”) bez zmian.
- **P1 — dla `docs` przy zamknięciu** (zapisy poza kodem): skreślić AC-1 (I1) i poprawić tytuł oraz *What to build* tej pozycji (zostaje G2); przykład w
  US-009 AC-5 → „…babci mojej żony” (AC-3); przykład opisu czytnika w [[ISSUE-032-mvp-install]] → *Hand checks* → „…, Moja babcia, w środek”.

### Scope — files (`{code}`)
| Plik | Zmiana |
|---|---|
| `lib/app/person/kinship_names.dart` | zaimek G2: pojedyncza nazwa „Moja” / „Mój” / „Moje” (według rodzaju słowa, jak dziś), w opisie z odcinków „mojej” / „mojego” małą literą; wielka litera tylko na początku całego tekstu (jak dziś). Komentarze G1 → G2 (D28) |
| `lib/app/tree/tree_screen.dart` | w `_kinOf`: „to ja” i „nie wiadomo jeszcze, kim jest dla mnie”. Komentarze, które cytują G1 („Twoja babcia”, „kim jest dla Ciebie”), → G2 |

Imiona przy oddalaniu (`tree_labels.dart`, `_labelScale`, `_visibleNames`) — **bez zmian**. Testy (pisze `qa`): `test/app/person/kinship_names_test.dart`,
`test/app/tree/tree_screen_test.dart` (teksty G1 → G2), `test/app/person/person_screen_test.dart` (patrz niżej).

### AC → implementation → test (testy pisze `qa`)
| AC | Implementacja | Test happy-path |
|---|---|---|
| ~~AC-1 — I1~~ | **wycofane** (stop #1, autor: „1 I2”) | — I2 pokrywają testy ISSUE-033 (`tree_labels_test`), bez zmian |
| AC-2 — G2 | `kinshipName`, `_kinOf` | `kinship_names_test`: mama taty → „Moja babcia”; brat taty → „Mój stryj (brat taty)”; dziecko bez płci → „Moje dziecko”; ścieżka z AC-2 → „Siostra cioteczna babci mojej żony”; „Siostra cioteczna mojego dziadka”. `tree_screen_test`: karta „ur. 1983 · to ja”, po dotknięciu żony „ur. 1985 · Moja żona”, opis dla czytnika „…, Moja żona”; osoba bez rodziny „bez dat · nie wiadomo jeszcze, kim jest dla mnie”. W drzewie nie ma „Twoj” ani „Twój” |
| AC-3 — przykład w US-009 i [[drzewo]] | [[drzewo]] v1.9 (`ui`, zrobione); US-009 AC-5 — `docs` (P1) | — (zapis w vaulcie) |

Przy okazji `qa`: `person_screen_test` sprawdza dziś, że w widoku osoby nie ma „Twoja”. Przy G2 ten test nic nie pilnuje, więc niech sprawdza też
brak „Moja” (D13' — widok osoby nie podaje nazwy pokrewieństwa).

### Data layer
- **Bez zmian:** ekran tylko czyta, schemat v12 zostaje. Nie ma migracji ani próbnego odtworzenia z kopii.
- Bez sieci i bez nowych uprawnień. `AndroidManifest.xml` i `pubspec.yaml` zostają bez zmian.

### Manual verification
**Agent na emulatorze** — przed stopem #2, ze zrzutami (`Grobing_Restore`, build profile, wymyślona rodzina — 106 osób):
1. Karta: „Ja” → „to ja”; żona → „Moja żona”; mama taty → „Moja babcia”; ktoś z rodziny żony z opisem z odcinków („…mojej żony”); ktoś ze słownika z
   nawiasem („Mój stryj (brat taty)” albo „Moja ciotka (siostra taty)”).
2. `uiautomator dump`: opisy węzłów z „Moja …” / „Mój …”, bez „Twoja” i „Twój”.
3. Tekst 200% na 360 dp: dłuższy opis („Siostra cioteczna babci mojej żony”) zawija się w karcie bez ucięcia (element 5).

**Autor: odczucie** (najwyżej 3 kroki, emulator `Grobing_Restore`):
1. Dotknij kilka osób: babcię, żonę, kogoś z rodziny żony i siebie. Czy karta („Moja babcia”, „…babci mojej żony”, „to ja”) mówi tak, jak Ty mówisz o
   rodzinie?

### Out of Scope
- **I1** — wycofane przez autora na stopie #1 (D27); imiona przy oddalaniu i tryb prezentacji przy 200% zostają jak w ISSUE-033 i ISSUE-034.
- Mini-drzewo i łańcuch „Jak łączy się ze mną” w [[osoba]] (relacja jednego kroku, bez zaimka — D13').
- Zdania aplikacji w drugiej osobie: „Wybierz, która osoba to Ty”, „Która osoba to Ty?”, „Ty w drzewie”, „Twoje cmentarze”, „wraca do Twojej pozycji”,
  „…jak łączy się z Tobą” ([[drzewo]] D28).
- Baner „Połącz dwie osoby” buduje [[US-011-polacz-dwie-osoby]]. Weźmie tę samą funkcję, więc już mówi G2.
- „Przesyłaj” z aplikacji → [[ISSUE-036-cast-from-the-app]].

## Dev report
> `dev`, 2026-10-14. Flutter 3.41.1 (zgodny z przypiętym). `dart format` bez zmian, `flutter analyze` — *No issues found*.

### What was built (`{code}`)
- `lib/app/person/kinship_names.dart` — `kinshipName`: zaimek G2. Pojedyncza nazwa „moja” / „mój” / „moje” według rodzaju słowa, z wielką literą przez
  istniejące `text[0].toUpperCase()` („Moja babcia”). Opis z odcinków „mojej” / „mojego” małą literą („Dziadek mojej żony”). Komentarze → v1.9, D28.
- `lib/app/tree/tree_screen.dart` — `_kinOf`: „to ja”, „nie wiadomo jeszcze, kim jest dla mnie”; komentarz `_TreeCard` → D28.
- Imiona przy oddalaniu (I2) bez zmian, zgodnie z planem.

### Deviations (do przeglądu `ui`)
- Brak. Komentarz w `lib/data/family_tree.dart:80` („kim jest dla Ciebie”) zostaje, bo plik jest poza planem i to tylko opis pola w komentarzu, nie tekst na ekranie.

### Przejście AC na emulatorze (`Grobing_Restore`, build profile, wymyślona rodzina — 106 osób; zrzuty w `shots-035\` katalogu tymczasowego sesji)
- **Karta „ja”:** „ur. 1983 · to ja” (zrzut `01-ja`).
- **Słownik i nawiasy** (`uiautomator dump`, opisy węzłów od „Ja”): „Mój dziadek”, „Moja babcia”, „Mój tata”, „Moja mama”, „Mój wuj (brat mamy)”, „Moja ciotka
  (siostra mamy)”, „Mój teść (tata żony)”, „Moja siostra”, „Mój brat”, „Moja żona”, „Moja córka”, „Mój syn”; dalej „Mój brat stryjeczny (syn brata taty)”,
  „Moja teściowa (mama żony)”, „Mój szwagier (brat żony)”.
- **Opis z odcinków, małe „mojej” / „mojego”:** „Babcia mojej żony”, „Ciotka mojej żony”, „Wuj mojej żony”, „Brat wujeczny mojej żony”, „Siostra cioteczna mojej
  żony”, „Bratanica mojej żony”, „Wuj mojego taty”, „Stryj mojej mamy”, „Brat wujeczny mojego taty”. Karta po dotknięciu żony: „ur. 1985 · Moja żona”
  (zrzut `02-zona`); dalszy krewny: „ur. 1958 · Brat wujeczny mojego taty” (zrzut `04-dalszy`).
- **Ani jednego „Twoja” / „Twój”** w opisach węzłów na poziomach 2–4 od „Ja”, od żony, od jej babci i od taty (`dump` z filtrem).
- **Tekst 200% na 360 dp** (`font_scale 2.0`, `wm density 480`): „ur. 1958 · Brat wujeczny mojego taty” zawija się w dwie linie bez ucięcia, „Pokaż ›” pod
  tekstem (D20; zrzut `05-200proc`). Ustawienia emulatora przywrócone (`font_scale 1.0`, `wm density reset`).
- **Nie sprawdzone na emulatorze:**
  - stan „osoba bez rodziny” („nie wiadomo jeszcze, kim jest dla mnie”) — w bazie testowej nie ma osoby bez rodziny (zapytanie na kopii bazy w katalogu
    tymczasowym: 0). Tekst to jeden literał w `_kinOf`, więc pokrywa go test widgetu („States — a person without a family”) po zmianie przez `qa`;
  - ścieżka z AC-2 („Siostra cioteczna babci mojej żony”) — na emulatorze jej nie znalazłem: babcia żony po stronie mamy nie ma w wymyślonej rodzinie
    rodziców, a po stronie taty nie szukałem dalej. Na emulatorze widać opisy z dwóch odcinków („Brat wujeczny mojego taty”); trzy odcinki pokrywa test `kinship_names_test`.
- Pomiar klatki niepotrzebny — rysowanie bez zmian (zmienił się tylko tekst).

### For `qa`
- Teksty G1 w testach do zmiany na G2: `test/app/tree/tree_screen_test.dart` (13 miejsc: „to Ty”, „Twoja żona”, „Ciotka Twojej żony”, „Twój dziadek”, „…dla
  Ciebie”), `test/app/person/kinship_names_test.dart` (19 miejsc), `person_screen_test.dart:297` — dziś pilnuje braku „Twoja”, przy G2 niech pilnuje też braku
  „Moja” (plan → *AC → test*). Zdania aplikacji w drugiej osobie w testach („Wybierz, która osoba to Ty”, „Twoje cmentarze”) zostają.
- Kopia bazy testowej `test-035.db` w katalogu tymczasowym sesji (wymyślone dane) — do kosza po pozycji.

## Verification
> `qa`, 2026-10-14. Rytuał WZ-024: `dart format` (189 plików, 0 zmian) → `flutter analyze` (*No issues found*) → `flutter test` (**727/727**) → kroki
> ręczne → stop #2.

### Tests (happy path per AC, `{code}/test/`)
| AC | Test |
|---|---|
| ~~AC-1 — I1~~ | wycofane na stopie #1 (autor: „1 I2”); I2 pokrywają testy ISSUE-033 bez zmian (`tree_labels_test`) |
| AC-2 — G2 | `kinship_names_test` → *kinshipName — the tree's card*: mama taty → „Moja babcia”; „Mój stryj (brat taty)”, „Moja ciotka (siostra taty)”, „Mój wuj (brat mamy)”, „Moja siostra cioteczna (córka siostry taty)”, „Mój teść (tata żony)”, „Moja żona”; ścieżka z AC-2 (żona → jej mama → jej mama → jej rodzic → jego rodzeństwo → jego dziecko) → „Siostra cioteczna babci mojej żony”; „Babcia mojej żony”, „Ciotka babci mojej żony”; słowa neutralne „Moje dziecko”, „Partnerka mojego brata”, „Rodzic mojej mamy”. `tree_screen_test`: AC-1 — karta „ur. 1983 · to ja”, opis dla czytnika „…, to ja” i „…, Moja żona”, **w drzewie nie ma „Twoj”/„Twój” ani w tekście, ani w opisach dla czytnika** (nowa asercja); AC-2 — „ur. 1985 · Moja żona”; AC-5 — „ur. 1961 · Ciotka mojej żony”; AC-6 — „1925–2004 · Mój dziadek”; *States* — „bez dat · nie wiadomo jeszcze, kim jest dla mnie”; testy dostępności dotyku (`androidTapTargetGuideline`, `labeledTapTargetGuideline`, każdy przycisk ma akcję dotknięcia) bez zmian, zielone |
| AC-3 — przykład w US-009 i [[drzewo]] | [[drzewo]] v1.9 (zrobione); US-009 AC-5 — `docs` przy zamknięciu (plan → P1) |

Przy okazji: `person_screen_test` (D13') pilnuje teraz też braku „Moja” w widoku osoby. Zdania aplikacji w drugiej osobie („Wybierz, która osoba to Ty”,
„Aplikacja nie wie jeszcze, która osoba to Ty.”, „Twoje cmentarze”) — testy bez zmian, zielone.

### Agent na emulatorze (przed stopem #2)
Kroki 1–3 z planu zrobił `dev` przy przejściu AC (*Dev report*, zrzuty `01`–`05` w `shots-035\`), a `qa` je przejrzał i przyjął: karta „to ja”, „Moja żona”,
„Brat wujeczny mojego taty”; w `uiautomator dump` od „Ja”, żony, jej babci i taty nie ma „Twoja” ani „Twój”; przy 200% na 360 dp karta zawija się bez ucięcia.
Build profile z tą zmianą został na `Grobing_Restore`.

### UI review (`ui`, subagent bez historii) — 0 BLOCKER, 0 MAJOR, 1 MINOR spoza pozycji
- **Zgodne:** G2 w karcie i w opisach dla czytnika (wielka litera tylko na początku, „mojej” / „mojego” małą, nawiasy ze słownika); reguła 7 — żadne zdanie
  aplikacji nie przeszło na pierwszą osobę; karta przy 200% (zawijanie, „Pokaż ›” pod tekstem, ok. 24% wysokości < 40% z D20); imiona przy oddalaniu bez
  zmian (I2). Kontrast z `theme.dart`: linia karty 5,01:1, imię w karcie 10,02:1, „Pokaż” 8,04:1, imiona pod węzłami 10,98:1, ikona telewizora 8,81:1,
  obrys + / − 3,40:1.
- **MINOR (od ISSUE-033, nie z tej zmiany):** przy skali < 1 tabliczka imienia (I2 rośnie o 1/skala) zasłania kreskę śladu w dół („dzieci poza widokiem”,
  D9). Przy 100% kreska znika cała od skali ok. 0,48, przy 200% od ok. 0,65; na poziomie 2 (AC-4) zostaje. Poprawka: kreska w dół od dolnej krawędzi
  tabliczki na ekranie. **Nie wchodzi do tej paczki** — kandydat na małą pozycję (`docs` → `CURRENT_STATE.md` *Poza tą kolejnością*).
- **Znana luka, nie znalezisko:** „z d.” bez twardej spacji zostaje samo na końcu linii w karcie (zrzut `02`) — [[style-b]] reguła 6, kandydat już zapisany
  (przegląd ISSUE-022, B5).

### Dane rodziny
- Pliki paczki (lista niżej): bez baz, kopii, eksportów i zdjęć. Nazwiska w testach i w vaulcie tylko z wymyślonych rdzeni (Wymyśl-, Zmyśl-, Przykład-,
  Testow-). Strażnik treści przepuścił próbne `git add` obu paczek (2026-10-14).
- Kopia bazy testowej `test-035.db` (wymyślone dane) leży w katalogu tymczasowym sesji, poza repo — do kosza po pozycji.

### Not verified here (po jednym w linii — dla [[ISSUE-032-mvp-install]] → *Hand checks*)
- stan „osoba bez rodziny” („nie wiadomo jeszcze, kim jest dla mnie”) — tylko test widżetu; w bazie testowej nie ma takiej osoby
- opis z trzech odcinków („Siostra cioteczna babci mojej żony”) — tylko test jednostkowy; na emulatorze widać opisy z dwóch odcinków
- TalkBack na żywo czyta „…, Moja babcia, w środek” — tylko `uiautomator` i testy

### Stop #2 (2026-10-14) — autor: „ok”, bez śladu na urządzeniu
- Krok 1 (karta „Moja babcia”, „Babcia mojej żony”, „to ja” — odczucie): **„ok”**. Sprawdzenie na urządzeniu: od ustawienia drzewa na „Ja” (11:17 czasu
  emulatora) do odpowiedzi aplikacja nie narysowała ani jednej klatki (`GROBING_FRAME` w logcat), a karta dalej mówiła „to ja”, więc kroku nikt nie
  wykonał na emulatorze. Autor, zapytany, wybrał: **„zapisz bez śladu”**. Ton G2 autor wybrał sam na makiecie (stop #1 ISSUE-034 i ISSUE-035).

### Na listę ISSUE-032 → *Hand checks* (po jednym w linii)
- karta drzewa w G2 („Moja babcia”, „…babci mojej żony”, „to ja”) — „ok” autora bez śladu na urządzeniu (ISSUE-035, stop #2)
- stan „osoba bez rodziny” („nie wiadomo jeszcze, kim jest dla mnie”) — tylko test widżetu
- opis z trzech odcinków („Siostra cioteczna babci mojej żony”) — tylko test jednostkowy
- TalkBack na żywo czyta „…, Moja babcia, w środek” (zamiast przykładu „Twoja babcia” w istniejącym wierszu TalkBack) — tylko `uiautomator` i testy

### Werdykt `qa`: APPROVED (self-check, z uwagami)
- **Dowody:** AC-2 — testy jednostkowe i widżetu (727/727), przejście na emulatorze ze zrzutami (`dev`), przegląd `ui` 0 BLOCKER / 0 MAJOR; AC-3 —
  [[drzewo]] v1.9 zrobione, US-009 AC-5 przy zamknięciu (`docs`); AC-1 wycofane decyzją autora na stopie #1.
- **Uwagi:** stop #2 „ok” bez śladu (wyżej); MINOR spoza pozycji (tabliczka zasłania kreskę śladu w dół przy oddaleniu, od ISSUE-033) → kandydat dla
  `docs`; „z d.” bez twardej spacji — znany kandydat.
- **Szukałem i nie znalazłem:** „Twoj” / „Twój” / „Ciebie” w tekstach drzewa (kod, testy, `uiautomator`); nazwy pokrewieństwa w drugiej osobie albo zdań
  aplikacji w pierwszej (przegląd `ui`, reguła 7); zmian w imionach przy oddalaniu (diff, zrzuty poziomu 3); ucięcia karty przy 200%; danych rodziny w paczce
  (strażnik treści, rdzenie w przykładach); zmian w schemacie, `AndroidManifest.xml` i `pubspec.yaml`.

### Paczka dla `docs` (jedna pozycja = jeden commit na repo)
- **`grobing-code`:** `lib/app/person/kinship_names.dart` · `lib/app/tree/tree_screen.dart` · `test/app/person/kinship_names_test.dart` ·
  `test/app/person/person_screen_test.dart` · `test/app/tree/tree_screen_test.dart`.
- **`grobing-vault`:** `05_DESIGN/drzewo.md` · `05_DESIGN/brand/style-b.md` · `backlog/issues/ISSUE-035-tree-names-shrink-my-voice.md` ·
  `00_START_HERE/TRACEABILITY.md` — plus zapisy zamknięcia `docs` (plan → P1: AC-1 skreślone, tytuł i *What to build*; US-009 AC-5; [[ISSUE-032-mvp-install]]
  → *Hand checks*; `CURRENT_STATE.md` z kandydatem MINOR).
- **`grobing-agents`:** nic.
