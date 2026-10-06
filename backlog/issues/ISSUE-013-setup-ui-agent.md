---
title: "ISSUE-013 — Set up the screen designer agent (`ui`) and wire it into the chain"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: 1
quality-verdict: APPROVED
verdict-date: 2026-10-06
verdict-reviewer: self-check
source: "PROJECT_BRIEF §How we build → 3c (`ui` — first screen designed, early: Style B needs guidelines) · decyzja autora 2026-10-06"
blocks: "[[ISSUE-012-transcribe-grave-screen]]"
created: 2026-10-06
updated: 2026-10-06
---

# ISSUE-013 — Agent `ui` (projektant ekranów) w łańcuchu

> **Decyzja autora 2026-10-06 (w `/pm`):** *„zróbmy to prawidłowo — budujemy agenta `ui` i włączamy go w
> procesy”*, zanim ruszy [[ISSUE-012-transcribe-grave-screen]]. Wcześniej w tej samej sesji autor przyjął
> wariant „pierwszy ekran projektuje `planning`, `ui` przy drugim ekranie” i zmienił zdanie, zanim
> cokolwiek zapisano. Kick-off (brief → 3c) zakładał `ui` na sygnał *„first screen designed (early: Style
> B needs guidelines)”*. ISSUE-012, pierwszy ekran do wpisywania danych, jest tym sygnałem.

## What to build
1. **Skill `grobing-agents/.claude/skills/ui/SKILL.md`** w kształcie `SKILL.template.md` z NPG. Projektant
   ekranów Grobing:
   - pisze **specyfikację ekranu** w vaulcie dla pozycji, która dodaje albo zmienia ekran: cel, US i AC,
     pola i ich kolejność, klawiatura, wartości domyślne, stany (pusty / błąd / wypełniony), szkic,
     mapowanie AC → element;
   - jest **właścicielem wytycznych stylu B** ([[NT-006-visual-guidelines]]). Pierwsza wersja powstaje
     przy pierwszym prawdziwym uruchomieniu;
   - **nie pisze kodu** (tokeny w `theme.dart` wdraża `dev` według wytycznych), nie planuje pozycji i jej
     nie zamyka.
2. **Wpięcie w procesy** (`grobing-agents`):
   - `autonomous-flow.md` → *The chain*: miejsce `ui` w łańcuchu dla pozycji z ekranem. Lista punktów
     stopu zostaje zamknięta;
   - `CLAUDE.md` → *Agents*: `ui` w tabeli, usunięty z „Na sygnał”;
   - `pm` → *Routing*: wiersz „pierwszy ekran → zaproponuj agenta `ui`” zastąpiony routingiem do `ui`;
   - `vault-as-sot.md` → *Ownership*: kto pisze treść `05_DESIGN/`. Folder i wiersz w DOC_MAP nadal
     zakłada `docs` (`doc-growth.md`);
   - sąsiednie skille (`planning`, `dev`, `qa`) — tylko to, co muszą wiedzieć o specyfikacji.
3. **Pierwsze prawdziwe uruchomienie na [[ISSUE-012-transcribe-grave-screen]]**: specyfikacja tego ekranu
   i pierwsza wersja wytycznych stylu B w `05_DESIGN/`. Folder zakłada `docs` przy tym uruchomieniu, z
   wierszem w DOC_MAP.

## Acceptance Criteria
- [ ] `grobing-agents/.claude/skills/ui/SKILL.md` ma kształt `SKILL.template.md`: *Scope* z *Does NOT*,
      *On invocation*, *Output* z dokładnym miejscem zapisu, *Constraints* z hand-offem, *Conflict Check*,
      *Self-check*, `updated:`. Bez ścieżek absolutnych (`project-config.example.md`).
- [ ] `ui` jest w łańcuchu, a `autonomous-flow.md`, `CLAUDE.md` (*Agents*), routing `pm` i własność
      `05_DESIGN/` w `vault-as-sot.md` mówią to samo. **Żadnego nowego punktu stopu** poza zamkniętą
      listą, chyba że autor zdecyduje inaczej na stopie #1.
- [ ] **Uruchomiony raz naprawdę** na ISSUE-012: specyfikacja ekranu i wytyczne stylu B v1 leżą w
      `05_DESIGN/`, z wierszami w DOC_MAP. Każde AC ISSUE-012 ma element w specyfikacji. Czego
      specyfikacja nie rozstrzyga, jest oznaczone `⚠️ OPEN`, a nie zgadnięte.
- [ ] Wytyczne stylu B mają **sprawdzalne progi** (kontrast, cel dotyku) z cytowanym źródłem, a nie z
      pamięci, oraz zapisany pomiar obecnych kolorów z `grobing-code/lib/app/theme.dart`.
- [ ] Zero danych rodziny w specyfikacji, szkicach i przykładach — wyłącznie wymyślone osoby
      (`family-data.md`).

## Out of Scope
- Kod ekranu ISSUE-012 i zmiany w `theme.dart` → [[ISSUE-012-transcribe-grave-screen]] (`dev`).
- Czytelność w pełnym słońcu ([[NFR-004-czytelnosc-w-sloncu]]) — sprawdza ją tylko telefon w buildzie
  release (`DEFINITION_OF_DONE.md`). Wytyczne mogą zaproponować próg; decyzja zapada przy pierwszym
  ekranie wizyty.
- Krytyk jakości → [[ISSUE-003-setup-quality-critic]]. `ui` nie ocenia danych ani AC poza ekranem.
- Specyfikacje ekranów, których nie dotyka żadna pozycja (mapa, cmentarz, drzewo) — powstają razem ze
  swoimi pozycjami.

## Technical Notes
- **Prior art:**
  - `CreatiumTeamAgents/.claude/skills/ui`: składa US, FR, NFR i AC w jeden prompt do Claude Design
    (prototyp React + Tailwind, desktop-first), zapisuje go w `03_DRAFTS/ux-drafts/`, nie pisze kodu ani
    makiet, traktuje AC jako cel wizualny. **Do przeniesienia:** zbieranie wymagań, inwentarz widoków ze
    stanami, AC → element, granica „nie pisze kodu”. **Nie pasuje 1:1:** tamten celuje w web i desktop
    oraz w zespół z osobnym narzędziem projektowym, a Grobing to Flutter na Androida i autor solo.
  - NPG: `SKILL.template.md` (kształt skilla) i `npg-architect` → 3c (tabela trigger → agent: „ekran →
    `ui`”). Szablonu agenta `ui` NPG nie ma.
  - [[ISSUE-003-setup-quality-critic]]: wzorzec „uruchomiony raz naprawdę” (NPG `workflow-library.md`:
    agent zaprojektowany na papierze i nigdy nieuruchomiony to PHANTOM).
- **Wejście do wytycznych:** brief §6a (styl B dosłownie) · `grobing-code/lib/app/theme.dart` (tokeny) ·
  [[NFR-004-czytelnosc-w-sloncu]] (miara `⚠️ OPEN`) · [[NT-006-visual-guidelines]].
- **Pomiar wstępny (2026-10-06, z przerwanego planu ISSUE-012; wejście dla `ui`, nie decyzja).** Kontrast
  według wzoru WCAG, kolory z `theme.dart`:

  | Para | Kontrast |
  |---|---|
  | tekst `C9C5BF` na tle `121110` / na powierzchni `1C1B19` | 10,98 / 10,02 |
  | szary pomocniczy `8E8A84` na tle / na powierzchni | 5,50 / 5,01 |
  | bursztyn `E3A646` na tle / na powierzchni | 8,81 / 8,04 |
  | tło na bursztynie (tekst przycisku) | 8,81 |

  Wszystkie pary mają ≥ 4,5:1, czyli próg AA dla tekstu. Szary pomocniczy jest poniżej 7:1, progu AAA,
  który ma znaczenie dla ekranów wizyty. Źródła progów:
  - [WCAG 2.2](https://www.w3.org/TR/WCAG22/) (W3C Recommendation, 12.12.2024): SC 1.4.3 — 4,5:1 dla
    tekstu (AA); SC 1.4.6 — 7:1 (AAA); SC 1.4.11 — 3:1 dla elementów interfejsu; SC 1.4.1 — kolor nie
    może być jedynym nośnikiem informacji;
  - [Android — Make apps more accessible](https://developer.android.com/guide/topics/ui/accessibility/apps)
    → *Use large, simple controls*: cel dotyku co najmniej 48 dp × 48 dp.
- **Do rozstrzygnięcia na stopie #1** (`planning`, nie tutaj):
  - gdzie w łańcuchu działa `ui`: przed `planning` czy jako bramka-subagent w `planning`;
  - czy przegląd zbudowanego ekranu względem specyfikacji (np. przed stopem #2) wchodzi teraz;
  - w jakiej formie autor widzi ekran przed kodem: szkic w specyfikacji, makieta czy prompt do narzędzia
    projektowego.
- Zamknięcie tej pozycji uruchamia retro przed ISSUE-012 (licznik: `CURRENT_STATE.md`).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[NT-006-visual-guidelines]] (wytyczne stylu B) | design | `open`. Ta pozycja daje wytyczne v1; test w słońcu zostaje na telefon, więc NT-006 może zostać otwarte |
| [[ISSUE-012-transcribe-grave-screen]] | pierwsze prawdziwe uruchomienie | `ready`, czeka na tę pozycję |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP), przełożone na pozycję setup tak jak w
[[ISSUE-006-setup-family-data-guard]]:
- skill i reguły w `grobing-agents`;
- uruchomiony raz naprawdę (AC wyżej);
- vault zaktualizowany: wiersz w DOC_MAP przy nowym folderze `05_DESIGN/`;
- zero danych rodziny w zmianach;
- ręczna weryfikacja: specyfikacja i wytyczne to decyzje o wyglądzie i przepływie, czyli UI/UX, więc
  ocenia je autor (`DEFINITION_OF_DONE.md` → *Kto sprawdza*). Formę kroków ustala `planning`.

## Implementation plan
> `planning`, 2026-10-06. **DoR:** pozycja setup z kick-offu (3c) i z decyzji autora, bez kroku ścieżki i
> bez US, tak jak [[ISSUE-003-setup-quality-critic]] i [[ISSUE-006-setup-family-data-guard]]. Dlatego nie
> ma wiersza w `TRACEABILITY.md` (kolumny Issue(s)/Issue Status: n/a) ✅ · jasny zakres ✅ · `task-level`
> ✅. **Warstwa danych aplikacji:** nie dotyka (zero zmian w `grobing-code`), więc test migracji, próbne
> odtworzenie i źródło faktu nie mają tu zastosowania.

### Prior art (sources, not memory)
Zebrane w pozycji (*Technical Notes*). Z `CreatiumTeamAgents/.claude/skills/ui` przejmujemy:
- kolejność zbierania wejścia (`references/aggregation-checklist.md`): US → AC dosłownie → FR → NFR →
  system wizualny → istniejące specyfikacje;
- **inwentarz widoku ze stanami** (pusty / błąd / wypełniony);
- **AC jako cel wizualny** z zastrzeżeniem, że to cel, a nie weryfikacja;
- granicę „nie pisze kodu i nie commituje”.

Nie przejmujemy:
- promptu do Claude Design jako jedynego wyjścia;
- limitu 500 linii;
- trybów full-build / incremental (jeden autor, jedna aplikacja: specyfikacja ekranu to żywy plik
  aktualizowany przy każdej zmianie ekranu);
- folderów `03_DRAFTS/` i `06_DESIGN/ui-specs/` (Grobing ma już `05_DESIGN/` w `doc-growth.md`).

Z NPG `SKILL.template.md`: kształt sekcji, `updated:` bez `version:`, *Conflict Check* (agent konsumuje
cudzy artefakt) i *Self-check* (agent pisze na dysk).

### Decisions for stop #1
**Problem:** ISSUE-012 potrzebuje decyzji, których dziś nikt nie ma prawa podjąć:
- kolejność pól i wartości domyślne przy ok. 100 osobach;
- wpisywanie daty z dopiskiem;
- stany ekranu;
- ton i wytyczne stylu B.

`05_DESIGN/` nie ma właściciela. Każdy następny ekran (mapa, cmentarz, grób, osoba, drzewo) stanie na
tym, co ustalimy tutaj.

| # | Decyzja | Rekomendacja | Dlaczego · koszt |
|---|---|---|---|
| D1 | **Miejsce w łańcuchu** | **Osobny krok przed `planning`:** `pm` → `ui` (gdy pozycja dodaje albo zmienia ekran) → `planning` → `dev` → `qa` → `docs`. `ui` jest skillem, nie subagentem: jego praca jest widoczna w dzienniku łańcucha. **Bez nowego punktu stopu:** specyfikacja idzie na stop #1 razem z planem | Plan (pliki, kroki, testy) wynika z projektu ekranu, więc projekt musi być pierwszy. **Odrzucone:** `ui` jako bramka-subagent w `planning` — jego wynik ginie w wyniku narzędzia, a sam projekt bez planu (np. poprawka wyglądu) nie miałby wejścia; `ui` po `planning` — plan powstawałby przed projektem. **Koszt:** stop #1 przy pozycjach z ekranem jest cięższy (plan + specyfikacja) |
| D2 | **Co `ui` pisze** | (a) **specyfikację ekranu**, jeden żywy plik na ekran: `{vault}/05_DESIGN/<ekran>.md`, aktualizowany przy każdej pozycji, która ten ekran zmienia; (b) **wytyczne stylu B**: `{vault}/05_DESIGN/brand/style-b.md`. Oba foldery są już w `doc-growth.md`, więc reguła się nie zmienia. `ui` nie pisze kodu ani `theme.dart`, nie rusza pozycji ani DOC_MAP | **Wartości kolorów mają jeden dom: `theme.dart`.** Wytyczne mówią: rola tokenu, reguła, próg, pomiar. Nowy token `ui` proponuje w specyfikacji razem z pomiarem kontrastu, a `dev` go wpisuje. Dwa domy jednej wartości koloru rozjechałyby się przy pierwszej poprawce. Folder `05_DESIGN/` powstaje przy pierwszym zapisie `ui`. Wiersze DOC_MAP dopisuje `docs` w tej samej paczce (`doc-growth.md` reguła 5: punkt checklisty zamknięcia, nie po cichu) |
| D3 | **Podgląd ekranu przed kodem** — ❓ **pytanie do autora** | **Szkic ASCII w specyfikacji zawsze, a przy nowym ekranie także statyczna makieta HTML w stylu B** (kolory z `theme.dart`, wymyślone dane). Makieta jest jednorazowa, leży w katalogu tymczasowym sesji, poza repo. Strażnik danych rodziny i tak blokuje `*.html` w trzech repo. Autor ogląda ją na stopie #1, a prawdą zostaje specyfikacja | Ton (godny, spokojny, „nic ponurego”) da się ocenić tylko okiem, a przy pierwszym ekranie produktu o zmarłych to największe ryzyko. Makieta kosztuje minuty, a przeróbka ekranu we Flutterze po stopie #2 — pół sesji. **Czego makieta nie pokaże:** tempa wpisywania (klawiatura, przejścia między polami) i pikseli Fluttera (kroje, widgety Material). Tempo sprawdza dopiero stop #2 na emulatorze. **Odrzucone:** sam szkic ASCII (ton dopiero po kodzie); prompt do Claude Design jak w Creatium (autor sam wkleja go do zewnętrznego narzędzia i dostaje prototyp React pod przeglądarkę) |
| D4 | **Przegląd zbudowanego ekranu** | **Teraz, w małej skali:** drugi tryb tego samego skilla. `qa` przed stopem #2 woła `ui` jako **subagenta bez historii** ze zrzutami z emulatora (`adb`, katalog tymczasowy, nigdy repo). `ui` porównuje je ze specyfikacją i wytycznymi i zwraca tabelę `Miejsce · Problem · Reguła · Poprawka`. Wpisuje ją `qa` w *Verification*, a `ui` nie pisze nic. Usterki wracają do `dev`, zanim autor dostanie kroki | Domyka pętlę „projekt → budowa → sprawdzenie”, którą autor nazwał „włączeniem w procesy”. Autor nie dostaje na stopie #2 rzeczy, które da się złapać mechanicznie (kontrast, cel dotyku, brak elementu). **Granica:** to nie jest krytyk z [[ISSUE-003-setup-quality-critic]] — nie blokuje i nie ocenia danych ani AC |

### Scope diff vs the item (to accept at stop #1)
- **+ tryb przeglądu** (D4) i jego **jedno prawdziwe uruchomienie** już w tej pozycji. ISSUE-012 nie ma
  jeszcze zbudowanego ekranu, więc przegląd idzie na istniejącym ekranie startowym (dziś jedyny ekran
  produktu) względem wytycznych v1. Znaleziska się zapisuje, ale nie poprawia. Poprawka to osobna
  decyzja.
- **+ szablon specyfikacji** jako plik skilla: `.claude/skills/ui/references/screen-spec.md`. Szablon
  żyje przy agencie, który go wypełnia, tak jak w Creatium.
- **+ makieta HTML** (D3, jeśli autor ją przyjmie).
- **− zmiany w `docs`**: `doc-growth.md` już zna `05_DESIGN/` i `05_DESIGN/brand/`, więc skill `docs` i
  reguła zostają bez zmian.
- **− zmiany w `grobing-code`**: zero.

### Steps (dev)
1. **`grobing-agents/.claude/skills/ui/SKILL.md`** (nowy), sekcje według `SKILL.template.md`:
   - `description`: co robi + kiedy („/ui”, „zaprojektuj ekran”, „specyfikacja ekranu”, „wytyczne stylu”,
     „przejrzyj ekran”), oba tryby;
   - **Scope:** specyfikacja ekranu · wytyczne stylu B · przegląd zbudowanego ekranu. **Does NOT:** kod,
     `theme.dart`, testy, plan, `status:`, foldery i DOC_MAP, commit;
   - **On invocation — tryb „specyfikacja” (domyślny):**
     - czyta: pozycję · US z AC (dosłownie) · powiązane FR i NFR · `glossary.md` · DoD · brief §6a (styl
       B) i §4a (krok ścieżki, jeśli to ekran wizyty) · `05_DESIGN/brand/style-b.md` · istniejące
       specyfikacje w `05_DESIGN/` · obecne ekrany w `{code}/lib/app/` i `theme.dart`;
     - **brak wytycznych = pierwsze uruchomienie:** pisze v1 z briefu §6a, tokenów `theme.dart` i progów
       z cytowanym źródłem (pomiar w tej pozycji), z miejscem na wynik testu w słońcu (telefon, release);
     - wypełnia szablon specyfikacji. Ekran do wpisywania danych dostaje **liczbę akcji na jeden rekord**
       (pole, dotknięcie, zmiana klawiatury), bo tempo przy ok. 100 osobach to miara ekranu (G6);
     - przy nowym ekranie: makieta HTML (D3) w katalogu tymczasowym sesji, wymyślone dane, nigdy w repo;
   - **On invocation — tryb „przegląd”** (subagent `qa`): wejście = pozycja + specyfikacja + wytyczne +
     ścieżki zrzutów. Sprawdza elementy i ich kolejność, stany, role kolorów i pary kontrastu według
     tokenów, cel dotyku 48 dp oraz to, że kolor nie jest jedynym nośnikiem informacji. Wyjście: tabela
     `Miejsce · Problem · Reguła · Poprawka` jako wynik narzędzia; bez zapisu na dysk. Gdy nie ma
     specyfikacji, przegląd idzie tylko według wytycznych i wynik mówi to wprost;
   - **Output:** `{vault}/05_DESIGN/<ekran>.md` · `{vault}/05_DESIGN/brand/style-b.md` · makieta
     (katalog tymczasowy). Dla `docs`: lista nowych folderów do DOC_MAP;
   - **Constraints:** zero danych rodziny (przykłady, makiety, zrzuty tylko z wymyślonymi osobami) ·
     jeden dom wartości koloru (`theme.dart`) · progi z cytowanym źródłem · `⚠️ OPEN` zamiast zgadywania
     decyzji produktowej · bez nowego punktu stopu · hand-off: tryb specyfikacji → `planning` (auto-flow)
     albo „Następny: uruchom /planning”; tryb przeglądu → wynik wraca do `qa`;
   - **Conflict Check:**
     - pozycja vs AC w US;
     - specyfikacja vs istniejące ekrany i nawigacja w kodzie;
     - wytyczne vs brief §6a;
     - `⚠️ OPEN` w US albo NFR, które ekran dziedziczy (np. miara [[NFR-004-czytelnosc-w-sloncu]]);
   - **Self-check:**
     - każdy element ekranu wynika z AC albo FR, a jeśli nie, jest nazwany decyzją projektową;
     - każde pole na rekord jest uzasadnione (tempo);
     - zero danych rodziny;
     - zmieniał tylko `05_DESIGN/`.
2. **`.claude/skills/ui/references/screen-spec.md`** (nowy) — szablon specyfikacji:
   - frontmatter: `screen`, `items` (pozycje, które go zmieniały), `updated`;
   - **Purpose** (US, krok ścieżki albo M1);
   - **Navigation** (skąd się wchodzi, dokąd prowadzi);
   - **Elements in order:** element · typ · klawiatura · wartość domyślna · walidacja · źródło (AC/FR
     albo „decyzja projektowa”);
   - **States** (pusty / błąd / wypełniony / wczytywanie, jeśli dotyczy);
   - **Sketch** (ASCII);
   - **Tempo** (akcje na rekord — tylko ekrany do wpisywania);
   - **Style B rules applied** (+ nowe tokeny z pomiarem);
   - **AC → element**;
   - **Open** (`⚠️ OPEN`).
3. **Wpięcie** — tylko zdania, które zmieniają zachowanie, plus `updated:` w każdym ruszonym skillu:
   - `.claude/rules/autonomous-flow.md` → *The chain*:
     `pm` → (`ui`, gdy pozycja dodaje albo zmienia ekran) → `planning` → `dev` → `qa` (+ przegląd `ui`
     jako subagent przed stopem #2) → `docs`. Przy stopie #1: „pozycja z ekranem — także specyfikacja
     i makieta”. **Lista stopów bez zmian;**
   - `CLAUDE.md` → *Agents*: wiersz `/ui`; z „Na sygnał” usunięte `ui`;
   - `.claude/rules/vault-as-sot.md` → *Ownership*: `05_DESIGN/` (specyfikacje ekranów, wytyczne stylu
     B) → `ui`; folder i wiersz DOC_MAP → `docs`;
   - `pm/SKILL.md`: `description` (łańcuch od `ui` przy ekranie) · *Routing*: wiersz „pierwszy ekran →
     zaproponuj `ui`” zastąpiony wierszem „pozycja dodaje albo zmienia ekran → `ui` (auto-flow: dalej
     cały łańcuch)” · hand-off;
   - `planning/SKILL.md`:
     - *On invocation*: pozycja z ekranem → przeczytaj specyfikację i wytyczne, a plan je linkuje;
     - *Conflict Check* 3: **pozycja z ekranem bez specyfikacji → STOP, wróć do `ui`**. To mechaniczna
       straż kolejności;
     - stop #1 pokazuje link do specyfikacji i makiety;
   - `dev/SKILL.md`:
     - czyta specyfikację i wytyczne;
     - kolory tylko przez `theme.dart`, bez literałów `Color(0x…)` w ekranach;
     - odstępstwo od specyfikacji idzie do *Dev report* → *Deviations*, nie po cichu;
   - `qa/SKILL.md`:
     - krok 4: przy pozycji z ekranem, przed stopem #2, przegląd `ui` jako subagent ze zrzutami z `adb`
       (katalog tymczasowy). Usterki wracają do `dev`;
     - kroki dla autora wynikają ze specyfikacji (UI/UX).

### Files likely touched
- `grobing-agents`:
  - nowe: `.claude/skills/ui/SKILL.md`, `.claude/skills/ui/references/screen-spec.md`;
  - zmienione: `CLAUDE.md`, `.claude/rules/autonomous-flow.md`, `.claude/rules/vault-as-sot.md`,
    `.claude/skills/{pm,planning,dev,qa}/SKILL.md`.
- `grobing-vault`:
  - ta pozycja;
  - przy pierwszym prawdziwym uruchomieniu (`qa`, przez `/ui`): `05_DESIGN/<ekran ISSUE-012>.md`,
    `05_DESIGN/brand/style-b.md`;
  - przy zamknięciu (`docs`): DOC_MAP (2 wiersze), `CURRENT_STATE.md`, [[NT-006-visual-guidelines]] →
    *Resolution* (częściowe: wytyczne v1, test w słońcu otwarty).
- `grobing-code`: nic.

### AC → checks (`qa`)
Pozycja nie ma kodu, więc nie ma testów `flutter`. `qa` sprawdza dowodami, jak przy ISSUE-006:

| AC | Sprawdzenie |
|---|---|
| AC-1 kształt skilla | sekcje `SKILL.md` porównane z `SKILL.template.md`; brak ścieżek absolutnych (grep `C:\\`, `/c/`) |
| AC-2 łańcuch spójny | 5 plików (`autonomous-flow.md`, `CLAUDE.md`, `vault-as-sot.md`, `pm`, `planning`) czytane obok siebie: ta sama kolejność i ten sam warunek („dodaje albo zmienia ekran”); lista stopów w `autonomous-flow.md` bez zmian (`git diff`) |
| AC-3 uruchomiony raz naprawdę | **specyfikacja:** `/ui` na ISSUE-012. Pliki w `05_DESIGN/`; każde AC ISSUE-012 (US-002 AC-1…5, styl B, kopia przy zapisie) ma wiersz w *AC → element*; niewiadome są `⚠️ OPEN`. **Przegląd:** subagent `ui` bez historii na zrzucie ekranu startowego z emulatora, według wytycznych v1. Tabela znalezisk trafia do *Verification* |
| AC-4 progi ze źródłem | `style-b.md` cytuje WCAG 2.2 i Androida z linkiem; tabela pomiaru kolorów `theme.dart` jest w pliku |
| AC-5 zero danych rodziny | grep specyfikacji i makiety: tylko wymyślone osoby; zrzuty i makieta poza repo (`git status` trzech repo) |

### Manual verification (stop #2) — kroki według miejsca
Przegląd, ton i progi to UI/UX, więc kroki są dla autora. Spójność plików sprawdza agent (wyżej).
- **Plik w edytorze** — `grobing-vault/05_DESIGN/<ekran ISSUE-012>.md`: czy kolejność pól, wartości
  domyślne i wpisywanie daty z dopiskiem pasują do tego, jak wyglądają notatki? Czy liczba akcji na
  osobę jest do przyjęcia przy ok. 100 osobach?
- **Przeglądarka na PC** (link poda agent) — makieta HTML: czy ton jest godny i spokojny, bez
  ponurości, i czy bursztyn pojawia się tylko tam, gdzie prowadzi do działania?
- **Plik w edytorze** — `grobing-vault/05_DESIGN/brand/style-b.md`: czy progi i reguły są tym, czego
  chcesz pilnować na każdym następnym ekranie?
- **Napisz tutaj:** „ok” · „pomiń” · uwagi. Uwagi do specyfikacji wracają do `ui` przed zamknięciem.

### Out of Scope (this plan)
- Kod ekranu ISSUE-012 i zmiany w `theme.dart` (także nowe tokeny proponowane w specyfikacji) →
  [[ISSUE-012-transcribe-grave-screen]].
- Poprawki istniejących ekranów po przeglądzie ekranu startowego → osobna decyzja autora.
- Miara [[NFR-004-czytelnosc-w-sloncu]] → wytyczne mogą zaproponować próg (np. 7:1 dla ekranów wizyty),
  a decyzja zapada przy pierwszym ekranie wizyty, na telefonie.
- Krytyk jakości → [[ISSUE-003-setup-quality-critic]].

### Falsifier — what will show this shape is wrong
- *Dev report* ISSUE-012 wymienia decyzje projektowe, które `dev` musiał podjąć sam, bo specyfikacja ich
  nie rozstrzygała → szablonowi brakuje sekcji.
- Na stopie #2 ISSUE-012 autor znajduje problem z tonem albo układem, który makieta powinna była pokazać
  → zły poziom makiety.
- Przegląd `ui` nie znajduje nic, a autor znajduje usterki wizualne → przegląd jest dekoracją.

Wszystkie trzy wypadają przy ISSUE-012, tuż po retro (licznik: `CURRENT_STATE.md`).

### Self-check (planning) — said out loud
- **Kompletność:** zakres, pliki, AC → sprawdzenia, kroki ręczne i *Out of Scope* są.
- **Niezmierzone:** czy skill utworzony w trakcie sesji jest od razu widoczny jako `/ui`. Jeśli nie, `qa`
  uruchamia go jako subagenta z treścią `SKILL.md` i zapisuje to w *Verification*. Brak możliwości
  uruchomienia nie jest powodem, żeby go nie uruchomić.
- **D4 to generalizacja przed instancją ekranu z danymi.** Uzasadnienie: autor poprosił o włączenie w
  procesy, koszt to jedna sekcja skilla, a prawdziwe uruchomienie jest na ekranie startowym. Jeśli przy
  ISSUE-012 przegląd okaże się szumem, wypada (falsyfikator 3).
- **Własność:** pisałem tylko swoją sekcję i `status: in-progress`. Kolumn macierzy nie ruszałem
  (pozycja setup, n/a).

## Dev report
> `dev`, 2026-10-06.
> - **Stop #1:** autor odpowiedział: *„Róbmy zgodnie z twoją rekomendacją i dobrymi praktykami”*, czyli
>   „tak”. D1–D4 według rekomendacji, a D3 to szkic ASCII zawsze i makieta HTML przy nowym ekranie.
> - Zmiany są wyłącznie w `grobing-agents`. Wersja Fluttera i `flutter analyze` nie dotyczą tej pozycji
>   (zero zmian w `grobing-code`).

### What was built
- **`.claude/skills/ui/SKILL.md`** (nowy), sekcje według `SKILL.template.md`:
  - *Modes* (specyfikacja / przegląd), *Scope* z *Does NOT*;
  - *On invocation* osobno dla obu trybów;
  - *Style B guidelines* (co plik `05_DESIGN/brand/style-b.md` musi mieć: progi z linkami do WCAG 2.2 i
    Androida, jeden dom wartości koloru);
  - *Mockup* (katalog tymczasowy sesji, wymyślone dane, czego makieta nie pokazuje);
  - *Output*, *Constraints* z hand-offem, *Conflict Check*, *Self-check*;
  - `updated: 2026-10-06`, bez `version:`. Ścieżek absolutnych brak (grep).
- **`.claude/skills/ui/references/screen-spec.md`** (nowy) — szablon specyfikacji: frontmatter (`screen`,
  `items`, `us`, `journey-step`, `mockup`, `updated`), *Purpose*, *Navigation*, *Elements in order*,
  *States*, *Sketch*, *Tempo*, *Style B rules applied*, *AC → element*, *Decisions*, *Open*.
- **Wpięcie:**

  | Plik | Zmiana |
  |---|---|
  | `.claude/rules/autonomous-flow.md` | *The chain*: `ui` przed `planning`, gdy pozycja dodaje albo zmienia ekran; przegląd `ui` jako subagent w `qa` przed stopem #2. Stop #1: przy pozycji z ekranem także specyfikacja i makieta. **Lista stopów: nadal trzy** |
  | `.claude/rules/vault-as-sot.md` | *Ownership*: treść `05_DESIGN/` → `ui`; folder i DOC_MAP → `docs`; wartości kolorów → `theme.dart` (`dev`) |
  | `CLAUDE.md` | *Agents*: wiersz `/ui`; `ui` usunięty z „Na sygnał” |
  | `.claude/skills/pm/SKILL.md` | `description` (łańcuch od `ui` przy ekranie); *Routing*: „Start pozycji, która dodaje albo zmienia ekran → `ui` → `planning`” i „zmiana wyglądu bez pozycji → `ui`”, zamiast „pierwszy ekran → zaproponuj `ui`”; hand-off |
  | `.claude/skills/planning/SKILL.md` | *On invocation* 1: przy ekranie czyta specyfikację i wytyczne, nie projektuje od nowa; 4: stop #1 z linkami; *Conflict Check* 3: **brak specyfikacji → STOP, wróć do `ui`** |
  | `.claude/skills/dev/SKILL.md` | czyta specyfikację i wytyczne; kolory tylko przez tokeny `theme.dart`; odstępstwo albo nierozstrzygnięta decyzja projektowa → *Deviations* |
  | `.claude/skills/qa/SKILL.md` | krok 3a: zrzuty z `adb` do katalogu tymczasowego, przegląd `ui` jako subagent bez historii, wynik w *Verification*, usterki → `dev` |

  W każdym ruszonym skillu `updated: 2026-10-06`. `git diff --stat`: 7 plików, +40 / −13, plus nowy
  katalog `.claude/skills/ui/`.

### Measured on the way
- **Skill utworzony w trakcie sesji jest od razu widoczny:** zaraz po zapisie `ui` pojawił się na liście
  skilli sesji. Punkt „niezmierzone” z *Self-check (planning)* jest rozstrzygnięty, więc `qa` może
  wywołać `/ui` normalnie.

### Deviations from the plan
- **Brak `references/` poza szablonem.** Plan nie przewidywał innych plików. Wzorce Creatium
  (agregacja, inwentarz stanów) weszły do *On invocation* i szablonu, a nie do osobnych plików.
- **Numeracja w `qa`:** nowy krok ma numer 3a, żeby nie przesuwać numerów, do których odwołują się inne
  pozycje („krok 4 = stop #2”).
- **`docs` bez zmian** — zgodnie z planem (`doc-growth.md` już zna `05_DESIGN/` i `05_DESIGN/brand/`).

### For qa
- **AC-3 — pierwsze prawdziwe uruchomienie:**
  1. **Specyfikacja:** `/ui` na [[ISSUE-012-transcribe-grave-screen]]. To pierwsze uruchomienie, więc
     najpierw powstaje `05_DESIGN/brand/style-b.md`, potem specyfikacja ekranu, a przy nowym ekranie
     makieta HTML w katalogu tymczasowym sesji. Hand-off `ui` → `planning` **w tym przebiegu wstrzymaj**:
     ISSUE-012 planujemy po retro, a nie w ISSUE-013.
  2. **Przegląd:** zrzut ekranu startowego z emulatora (`adb exec-out screencap -p` do katalogu
     tymczasowego), potem `ui` w trybie przeglądu jako subagent bez historii, tylko według wytycznych
     (ekran sprzed `ui`). Znaleziska do *Verification*, bez poprawiania.
- **AC-2:** pięć plików do przeczytania obok siebie — tabela wyżej. W `git diff` pliku
  `autonomous-flow.md` lista stopów ma nadal 3 pozycje (zmienił się opis stopu #1, nie ich liczba).
- **Paczka na stop #3:** `grobing-agents` (7 zmienionych plików + `.claude/skills/ui/`) oraz
  `grobing-vault` (ta pozycja, ISSUE-012, `CURRENT_STATE.md`, `05_DESIGN/` z AC-3, DOC_MAP od `docs`).
  Git ostrzega o zmianie LF → CRLF w ruszonych plikach (`core.autocrlf`); to mechaniczne, treść diffu
  tego nie obejmuje.

### Manual verification (stop #2) — kroki według miejsca
Bez zmian względem planu (*Manual verification (stop #2)* wyżej): plik specyfikacji i `style-b.md` w
edytorze, makieta w przeglądarce na PC, odpowiedź tutaj.

## Verification
> `qa`, 2026-10-06. Pozycja bez kodu aplikacji, więc nie ma testów `flutter`. Weryfikacja idzie dowodami,
> jak przy [[ISSUE-006-setup-family-data-guard]].

### AC-1 — kształt skilla: ✅
`ui/SKILL.md` ma wszystkie sekcje `SKILL.template.md`: *Scope* z *Does NOT*, *On invocation* (osobno dla
obu trybów), *Output*, *Constraints* z hand-offem, *Conflict Check*, *Self-check*. Ma też `updated:`, a nie
ma `version:`. Sekcje dodatkowe (*Modes*, *Style B guidelines*, *Mockup*) szablonu nie łamią. Ścieżek
absolutnych brak (grep `C:\`, `/c/`, `Programowanie`).

### AC-2 — łańcuch spójny: ✅
- `autonomous-flow.md`, `CLAUDE.md`, `vault-as-sot.md`, `pm` i `planning` mówią to samo: `ui` przed
  `planning`, „gdy pozycja dodaje albo zmienia ekran”; przegląd jako subagent `qa` przed stopem #2;
  `05_DESIGN/` należy do `ui`, a folder i DOC_MAP do `docs`.
- **Lista stopów w `autonomous-flow.md`: nadal 3** (`git diff`: zmienił się opis stopu #1, nie liczba).
- Skill był widoczny w sesji zaraz po utworzeniu i przy `/ui` uruchomił się normalnie.

### AC-3 — uruchomiony raz naprawdę: ✅ (oba tryby)
**Tryb specyfikacji** — `/ui` na [[ISSUE-012-transcribe-grave-screen]], pierwsze uruchomienie. Hand-off
do `planning` wstrzymany zgodnie z planem.
- Wynik: `05_DESIGN/brand/style-b.md` (v1) i cztery specyfikacje: [[cmentarze]], [[cmentarz]],
  [[wpis-osoby]], [[grob]]. Przepływ ISSUE-012 to cztery ekrany, a skill każe pisać jeden żywy plik na
  ekran.
- Do tego makieta `makieta-przepisanie-grobu.html` (9 ramek) w katalogu tymczasowym sesji.
- **Każde AC ISSUE-012 ma wiersz w *AC → element*:**
  - US-002 AC-1 → [[cmentarz]], [[grob]], [[wpis-osoby]];
  - AC-2 → [[wpis-osoby]], [[grob]];
  - AC-3 → [[wpis-osoby]], [[grob]];
  - AC-4 → [[wpis-osoby]];
  - AC-5 → [[cmentarz]], [[grob]];
  - styl B → wszystkie;
  - kopia przy zapisie → [[wpis-osoby]] (n/a dla wyglądu, nazwane wprost).
- **Niewiadome oznaczone, nie zgadnięte:**
  - ⚠️ OPEN „poprawa wpisu” (decyzja na stopie #1 ISSUE-012) z rekomendacją;
  - pomiar typu klawiatury dla `dev`.
- Specyfikacja liczy tempo: **8 akcji na typową osobę, 0 ręcznych zmian klawiatury, 0 pytań o źródło**.

**Tryb przeglądu** — subagent `ui` bez historii (narzędzie Agent), zrzut ekranu startowego z `Medium_Phone`
(build debug z ISSUE-011; kod ekranu startowego bez zmian od ISSUE-002). Zrzut leżał w katalogu
tymczasowym sesji. Przegląd szedł bez specyfikacji, tylko według wytycznych, i powiedział to w pierwszym
zdaniu. Subagent niczego nie zapisał.

| # | Miejsce | Problem | Reguła | Co dalej |
|---|---|---|---|---|
| 1 | `start_screen.dart:44–48`, bursztynowa kreska 32 × 2 dp pod tytułem | akcent użyty jako ozdoba: dwa bursztynowe elementy przy jednym działaniu | *Token roles* → akcent „nigdy dekoracja”; reguła 1 | **usterka ekranu albo wyjątek znaku marki.** `ui` dopisał wyjątek do `style-b.md` v1.1 **do potwierdzenia przez autora (stop #2)**. Bez potwierdzenia kreska przechodzi na tekst pomocniczy (poprawka w ISSUE-012, które i tak zmienia ekran startowy) |
| 2 | odstępy 16 i 48 dp na starcie | poza wartościami reguły 5 (8–12 / 24 dp) | reguła 5 | **luka w wytycznych** → reguła 5 dostała kompozycje wyśrodkowane (v1.1) |
| 3 | etykieta „Stan danych”, 14 sp / 500 | wytyczne nie przypisywały etykiet przycisków do żadnego progu | *Thresholds* | **luka** → etykieta przycisku 14 sp / 500 dopisana (v1.1) |
| 4 | główne działanie jako `TextButton` | wytyczne nie mówiły, jaką formę ma główne działanie — ważne przed „Zapisz” w ISSUE-012 | reguła 1 | **luka** → wypełniony na listach i formularzach, tekstowy na ekranie startowym i w oknach (v1.1) |
| 5 | fokus przycisku | nakładka M3 ok. 1,17:1, poniżej 3:1 | SC 1.4.11 | **znana luka, niski priorytet** → *Known gaps* (tylko klawiatura fizyczna albo przełączniki) |

**Zgodne według przeglądu:**
- kolory wyłącznie z tokenów;
- kontrast: tytuł 10,98:1, etykieta 8,81:1, wciśnięta 7,52:1;
- cel dotyku 48 dp (z `MaterialTapTargetSize.padded`, sprawdzone w źródle Fluttera 3.41.1);
- krój systemowy, waga 300 w tytule;
- brak cieni i gradientów, ton, brak symboli;
- brak danych osób.

**Falsyfikator 3 („przegląd to dekoracja”): przy pierwszym uruchomieniu nie zachodzi.** Przegląd znalazł 1
możliwą usterkę i 4 luki, z których 2 (forma działania, rozmiar etykiet) dotyczą wprost ISSUE-012.
Sprawdzian na ekranie z danymi przyjdzie przy ISSUE-012.

### AC-4 — progi ze źródłem: ✅
`style-b.md` → *Thresholds* cytuje WCAG 2.2 (SC 1.4.3, 1.4.11, 1.4.1, 1.4.6 jako kandydat) i Androida
(48 dp), z linkami, a decyzje projektowe nazywa decyzjami (np. 16 sp). *Measurement* ma tabelę par z
`theme.dart` i z kandydatami na nowe tokeny. Liczba „tło–powierzchnia 1,1:1” użyta w wytycznych i
specyfikacji jest przeliczona (1,10).

### AC-5 — zero danych rodziny: ✅
- Osoby w `05_DESIGN/` i w makiecie: Jan, Anna i Józef Wymyślony/-a, Maria Próbna, Stefan i Zofia
  Przykładowy/-a, z d. Zmyślona. Wszystkie wymyślone.
- Zrzut i makieta leżą poza repo. W zmianach trzech repo nie ma `png`, `jpg`, `html`, `pdf`, `db`, `age`
  ani `tar` (`git status --untracked-files=all`).

### For docs (closure checklist)
- DOC_MAP: wiersze `05_DESIGN/` (specyfikacje ekranów, właściciel `ui`) i `05_DESIGN/brand/` (wytyczne
  stylu B), sygnał: ISSUE-013 (pierwsze uruchomienie `ui` na ISSUE-012).
- [[NT-006-visual-guidelines]] → *Resolution*, częściowo: link do `style-b.md`. Test w słońcu nie zrobiony
  (telefon, release), więc NT-006 zostaje `open`.
- ISSUE-012: link do czterech specyfikacji. Jego plan zaczyna się od specyfikacji, a stop #1 ISSUE-012
  rozstrzyga ⚠️ OPEN „poprawa wpisu”.
- `CURRENT_STATE.md`: licznik retro +1 → 10 → retro przed ISSUE-012.

### Manual (stop #2) — **„ok”** (autor, 2026-10-06)
- Odpowiedź autora: *„wygląda dobrze”*, po pytaniu „co teraz?”, w którym agent przypomniał minimum
  (pytanie 7) i makietę.
- **Pytanie 7 (znak marki):** autor nie odpowiedział osobno. Makieta, którą ocenił, pokazuje kreskę w
  akcencie na ekranie startowym (ramka 1), więc wyjątek z `style-b.md` reguła 1 zapisany jako
  **potwierdzony pośrednio**, z prośbą o korektę na stopie #3, gdyby to nie było zamierzone.
- Uwagi do specyfikacji: brak.

### Stop #2, runda 2 — referencje z kick-offu (autor, 2026-10-06)
- **Co się stało:** po „ok” autor przerwał zamknięcie i przysłał cztery obrazy stylu B z kick-offu (R1–R4)
  z promptami, z pytaniem, czy projekt jest z nimi spójny. **Obrazy i prompty nie były nigdzie zapisane**:
  brief §6a ma o nich jedno zdanie, więc `ui` pisał v1 z tego zdania.
- **Rozjazdy v1.1 względem obrazów (wykrył `ui` w porównaniu, nie przegląd):**
  1. reguła 8 zakazywała znicza, a obrazy B używają go jako znaku aplikacji;
  2. reguła 1 była za surowa wobec wielu ról bursztynu;
  3. reguła 2 nie pozwalała na karty ani poświatę;
  4. tytuły miały wagę 300 zamiast półgrubej;
  5. struktura i widok grobu odbiegały od R1 i R4.
- **Poprawione (rola `ui`):**
  - nowy plik `05_DESIGN/brand/references.md`: prompty dosłownie (nazwa miejscowości zastąpiona
    `[miejscowość]` — mogła być prawdziwa), opis obrazów, docelowa struktura aplikacji;
  - `style-b.md` → v1.2 (*Changelog*);
  - specyfikacje: [[cmentarze]] staje się ekranem głównym (znicz + „Grobing”, koło zębate → „Stan danych”,
    karty), ekran startowy znika; [[cmentarz]] dostaje karty z treścią arkusza R2; [[grob]] dostaje układ
    R4 i *Open* 1 o nazwie grobu; [[wpis-osoby]] dostaje formę „Zapisz” i odwołania do reguł;
  - makieta v1.2 z obrazami R1, R2 i R4 obok do porównania;
  - **skill `ui`**: `references.md` to obowiązkowe wejście, a reguły wyprowadza się z obrazów
    (`grobing-agents/.claude/skills/ui/SKILL.md`).
- **Znak marki:** wyjątek „kreska pod nazwą” z v1.1 jest zastąpiony zniczem + „Grobing” (R1). Pytanie 7
  z rundy 1 przestaje istnieć.
- **Gdzie trzymać obrazy (decyzja autora)** — opcje:
  - (a) folder poza repo, obok nich, z kopią na Dysku autora;
  - (b) w vaulcie, z wyjątkiem w `.gitignore` i w strażniku danych rodziny dla `05_DESIGN/brand/` — obrazy
    trafiłyby do publicznego repo, a wyjątek na obrazy w vaulcie osłabia strażnika dokładnie tam, gdzie
    kiedyś może trafić prawdziwe zdjęcie nagrobka.
  
  **Rekomendacja: (a).** **Decyzja autora:** obrazy położył w vaulcie (`01_INBOX/Inspiracje/`) i pozwolił
  je przenieść. Leżą w `05_DESIGN/brand/references/` jako R1–R4. Ich `*.png` jest ignorowane przez
  `.gitignore` (blok danych rodziny), więc nie trafią do repo, a strażnik zostaje bez wyjątku
  (sprawdzone `git check-ignore`). Trwała kopia → autor.
- **Uwagi autora do ekranów (runda 2):** dotyczą zakresu i kolejności ISSUE-012, nie agenta. Zapisane w
  [[ISSUE-012-transcribe-grave-screen]] → *Input from the author (2026-10-06)*.
- **Runda 2 — ocena autora (2026-10-06):** autor ocenił makietę v1.2 ramka po ramce (1–3, 4, 5–6, 7).
  Wygląd przyjął, a zmienił **strukturę i zakres**: mapa Polski od startu, cmentarz jak R2, grób jak R4,
  w formularzu zdjęcie i relacje. Zaakceptował plan kolejności (*„ok plan brzmi dobrze”*), zapisany w
  ISSUE-012 → *Input from the author* i w [[ISSUE-014-home-map-of-poland]]. To uwagi do ekranów, a nie do
  agenta: wracają do `ui` przed planem każdej z tych pozycji.

### Verdict (self-check)
**APPROVED, z uwagami** (`verdict-reviewer: self-check` — krytyk z ISSUE-003 jeszcze nie istnieje).

**Uwagi (nie blokują):**
1. Przegląd ekranu startowego zrobił subagent bez historii. Specyfikację i jej ocenę pisał jednak ten sam
   łańcuch, który zbudował agenta, więc AC-3 w trybie specyfikacji ma ślepą plamkę self-checku. Prawdziwy
   sprawdzian to falsyfikatory przy ISSUE-012: decyzje projektowe w *Dev report*, ton na stopie #2 i
   przegląd ekranu z danymi.
2. Wyjątek znaku marki z rundy 1 jest nieaktualny — w v1.2 znakiem jest znicz + „Grobing” (R1).
2a. **Falsyfikator 2 („zły poziom makiety”) zadziałał przed kodem:** makieta pozwoliła autorowi zmienić
    strukturę ekranów, zanim powstała linijka kodu. Agent spełnia swoją rolę; zawiodło wejście (referencje
    nie były zapisane), więc skill czyta je teraz obowiązkowo.
3. Stop #1 przy pozycjach z ekranem będzie cięższy (plan + specyfikacja + makieta). Do retro: czy nadal
   „lekko”?

**Czego szukałem i nie znalazłem:**
- nowego punktu stopu poza zamkniętą listą;
- ścieżek absolutnych w skillu;
- drugiego pisarza `05_DESIGN/`;
- danych rodziny i plików binarnych w trzech repo;
- AC ISSUE-012 bez elementu w specyfikacji;
- progu bez źródła;
- drugiej kopii wartości kolorów poza `theme.dart`. Wytyczne podają role i pomiar; wartości kandydatów
  `#6B6862` i `#E07A6F` są tylko w specyfikacji jako propozycja do wpisania przez `dev`.

## Closure
> `docs`, 2026-10-06. Zamknięcie **przed** commitem: folder `05_DESIGN/` wchodzi do paczki razem z
> wierszami DOC_MAP (`doc-growth.md` reguła 1).
- `status: done`, `ideal_days: 1`; werdykt `qa`: APPROVED (self-check, z uwagami).
- DOC_MAP: `05_DESIGN/` i `05_DESIGN/brand/` (z uwagą, że obrazy w `references/` są tylko lokalne).
- [[NT-006-visual-guidelines]] → *Resolution* częściowe: wytyczne v1.2 są, test w słońcu nie. Pozycja
  zostaje `open`.
- Uwagi autora do ekranów i kolejność → [[ISSUE-012-transcribe-grave-screen]] → *Input from the author*;
  nowa pozycja [[ISSUE-014-home-map-of-poland]]; [[US-002-przepisanie-grobu]] → `issues`;
  [[US-003-przepisanie-rodziny]] → *Notes*; pomysł „baza cmentarzy z importem mapy” →
  `01_INBOX/2026-10-05-plany-cmentarzy.md`.
- Brak wiersza w `TRACEABILITY.md` — pozycja setup, jak ISSUE-003 i ISSUE-006.
- Licznik retro +1 → retro przed następną pozycją (`CURRENT_STATE.md`).
