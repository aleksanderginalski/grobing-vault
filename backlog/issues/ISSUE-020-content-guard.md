---
title: "ISSUE-020 — Content guard: refuse staged lines that match the author's stem list"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: 0.5
quality-verdict: APPROVED
verdict-date: 2026-10-08
verdict-reviewer: self-check
source: "[[2026-10-08-retro-02]] R1"
created: 2026-10-08
updated: 2026-10-08
---

# ISSUE-020 — Strażnik treści (lista rdzeni autora)

> Decyzja autora w [[2026-10-08-retro-02]] (R1). Pozycja startowa procesu, tak jak
> [[ISSUE-006-setup-family-data-guard]]: bez kroku ścieżki i bez US, więc bez wiersza w `TRACEABILITY.md`.

## Problem
Od 2026-10-07 push idzie sam zaraz po commicie paczki, a repo są publiczne. Strażnik z ISSUE-006 rozpoznaje
**typ pliku, nie treść**: nazwisko wpisane w kod, test albo dokument przejdzie. Przegląd imion z
[[NT-008-publication-review]] objął historię do 2026-10-07, a przy następnych pushach treści pilnuje tylko uwaga
agenta. Agent nie może sam przeszukać zmian nazwami z notatek: odczytu `family_data_dir` klasyfikator Claude
Code nie przepuścił nawet za zgodą autora w sesji (pierwszy push, `CURRENT_STATE.md` → *Recently done*).

## What to build
Rozszerzenie `grobing-agents/.claude/hooks/family-data-guard.ps1` o **sprawdzenie treści** przy `git add` i
`git commit` w trzech repo:

- **lista rdzeni** w pliku w `family_data_dir` (nazwa ustalana w planie): nazwiska, nazwiska z domu, miejscowości,
  nazwy cmentarzy — po jednym w linii. **Pisze ją autor**, w Notatniku, poza VS Code. Agent jej nie tworzy, nie
  czyta i nie edytuje;
- czyta ją **wyłącznie skrypt strażnika** (uruchamiany przez harness, nie przez agenta);
- sprawdzane: **dodawane linie** w plikach, które mogą wejść do commita (ten sam zbiór co dziś przy typach plików),
  i **opis commita** z komendy;
- dopasowanie bez wielkości liter i bez polskich znaków, rdzeń jako początek słowa (np. rdzeń „Wymyslin” łapie
  „Wymyślina” i „WYMYSLINIE”);
- trafienie → **odmowa** z repo, plikiem i numerem linii, **bez trafionego słowa i bez treści linii** (komunikat
  strażnika trafia do kontekstu agenta, a stamtąd do zapisu sesji);
- zmiana w `family-data.md`: skrypt strażnika jako jedyny czytelnik listy; agenci dalej nie czytają
  `family_data_dir` bez prośby autora; nowy wiersz w tabeli *Mechanisms*.

## Czego NIE daje — powiedziane uczciwie
- **imion** — za częste, kolidowałyby z wymyślonymi danymi w testach; lista ma rdzenie rzadkie;
- **commitów autora z VS Code** — tam dalej chroni tylko `.gitignore`;
- **treści już wypchniętej** — historię do 2026-10-07 przejrzało NT-008, commity od tamtej pory nie były
  przeszukane nazwami z notatek;
- słowa z literówką albo odmienionego tak, że zmienia się rdzeń.

## Acceptance Criteria
- [ ] **AC-1 — odmowa bez echa.** *Given* na liście jest wymyślony rdzeń testowy *When* `git add` pliku, w którym
      to słowo stoi odmienione, wielkimi literami albo bez polskich znaków *Then* strażnik odmawia, a komunikat
      podaje repo, plik i linię i **nie zawiera** ani słowa, ani linii (test sprawdza stderr).
- [ ] **AC-2 — opis commita.** *Given* ten sam rdzeń *When* `git commit -m` z tym słowem w opisie *Then* odmowa
      bez słowa w komunikacie.
- [ ] **AC-3 — czysto przechodzi.** Zmiany bez trafień przechodzą; czas strażnika przy `git add`/`commit`
      zmierzony i zapisany (porównanie z pomiarem z ISSUE-006 → *Verification*).
- [ ] **AC-4 — uruchomiony raz naprawdę.** Autor wpisuje na listę wymyślony rdzeń testowy, agent dodaje w repo
      plik z tym słowem → odmowa; potem autor usuwa rdzeń, a agent plik.
- [ ] **AC-5 — reguła.** `family-data.md`: kto czyta listę, czego mechanizm nie łapie, status „działa”.

## Do decyzji na stopie #1
- brak pliku listy: blokada (jak brak `project-config.md`, fail-closed) czy ostrzeżenie;
- które linie sprawdzać przy `git add` pliku nieśledzonego (cały plik) i śledzonego (diff wobec `HEAD`);
- czy lista ma też kody i liczby (np. numery kwater), czy tylko słowa.

## Notes / references
- Wzorzec dziedziny: skaner przed commitem z listą zakazanych wzorców trzymaną **poza treścią repo** (np.
  git-secrets: wzorce w lokalnym `git config`). Źródło do sprawdzenia w planie, nie z pamięci.
- Edycje reguł i skryptu strażnika klasyfikator może zablokować jako zmianę własnych uprawnień agenta. Takie linie
  agent podaje autorowi do wpisania, nie obchodzi blokady.
- Lista leży w `family_data_dir`, poza trzema repo i workspace'em, jak inne robocze notatki rodziny
  (`family-data.md` → *Family data on this PC*).

## Implementation plan
> `planning`, 2026-10-08. Pozycja procesu bez ekranu i bez warstwy danych aplikacji: test migracji, próbne
> odtworzenie i źródło faktu nie mają tu zastosowania. **DoR:** zakres jasny, `delivery-style: task-level`;
> bez US i bez kroku ścieżki, jak [[ISSUE-006-setup-family-data-guard]], więc bez wiersza w `TRACEABILITY.md`.

### Prior art (sources, not memory)
- **git-secrets** ([README](https://github.com/awslabs/git-secrets)): wzorce w `git config` repo albo globalnym
  (`secrets.patterns`), poza treścią repo; `--add-provider` bierze wzorce z zewnętrznego programu; trzy hooki —
  `pre-commit` (zmienione pliki), `commit-msg` (opis commita), `prepare-commit-msg`. **Przy trafieniu drukuje
  „plik:linia:treść linii”** — tu świadomie odwrotnie, bo stderr strażnika trafia do rozmowy z agentem.
- **gitleaks** ([README](https://github.com/gitleaks/gitleaks)): `--redact` — „redact secrets from logs and stdout”
  (domyślnie 100%). To wzorzec komunikatu bez trafionego słowa.
- **Hooki Claude Code** ([hooks](https://code.claude.com/docs/en/hooks.md)): `PreToolUse` z `exit 2` blokuje
  wywołanie, a stderr zostaje w rozmowie, więc Claude go widzi. Strażnik działa poza klasyfikatorem uprawnień,
  bo uruchamia go harness, a nie agent.
- **ISSUE-006** → *Verification*: `git add`/`commit` ze skanem trzech repo kosztuje dziś ~700 ms (mediana z 3).

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego |
|---|---|---|---|
| D1 | **Gdzie lista** | `{family_data_dir}/rdzenie-straznika.txt`, ścieżka z `family_data_dir` w `project-config.md` (jest od retro 1). Jeden rdzeń w linii, `#` = komentarz, puste linie pomijane. Odczyt jako UTF-8, a gdy bajty nie są poprawnym UTF-8 — Windows-1250 (Notatnik zapisany „ANSI”) | bez nowego klucza konfiguracji; testy podstawiają własny `family_data_dir` w swoim `project-config.md`, jak dziś ścieżki repo |
| D2 | **Brak listy albo lista bez rdzeni** | **blokada** `git add`/`commit` z komunikatem „utwórz listę” (fail-closed, jak brak `project-config.md` w ISSUE-006). Zapis plików narzędziami Claude'a — bez zmian | ryzyko jest nieodwracalne. Cichy brak listy wyglądałby jak ochrona, której nie ma |
| D3 | **Co sprawdza** (w trzech repo, jak dziś typy plików) | (a) linie dodane w `git diff --cached` (indeks wobec `HEAD`) i w `git diff` (drzewo wobec indeksu), `-U0 --no-renames --no-color --no-ext-diff`; (b) cała treść plików nieśledzonych i nieignorowanych; (c) **ścieżki** tych plików; (d) **cały tekst komendy** z `git add`/`commit` (łapie `-m` i heredoc w `-F -`), a przy `-F <plik>` także ten plik. Pliki binarne (bajt 0 w pierwszych 8 KB, „Binary files … differ”) pomijane — zdjęcia i bazy łapie lista typów | to samo podejście co ISSUE-006 D3: patrzymy na wszystko, co mogłoby wejść do commita, zamiast parsować pathspecy. Nazwa pliku też jest treścią |
| D4 | **Dopasowanie** | obie strony bez polskich znaków (ą ć ę ł ń ó ś ź ż → a c e l n o s z z, reszta przez NFD) i bez wielkości liter. Rdzeń na **początku słowa**: przed nim nie-litera albo przejście małej litery w wielką (`testZmyslonowski`). Rdzeń krótszy niż 3 litery → blokada „popraw linię k listy” | „Zmyslonowsk” łapie „Zmyślonowska”, „ZMYSLONOWSKIEGO”, `zmyslonowski_test` i `testZmyslonowski`. Dopasowanie w środku słowa dawałoby fałszywe trafienia w zwykłych słowach |
| D5 | **Komunikat** | `ODMOWA` + repo, plik, **numer linii pliku** i **numer linii listy** (autor widzi go w Notatniku); nigdy słowo ani treść linii. Ścieżka, w której jest trafienie, drukowana z gwiazdkami w miejscu trafionego słowa | agent wie, co poprawić, bo sam napisał tę linię, a lista nie trafia do rozmowy. Ścieżka bez maskowania zdradziłaby słowo |
| D6 | **Fałszywe trafienie** (np. miejscowość z listy w publicznych danych OSM) | **bez listy wyjątków w v1.** Agent zgłasza autorowi „plik:linia, linia k listy”, autor zawęża rdzeń. Druga taka sytuacja → lista wyjątków jako osobna pozycja | reguła „nie generalizuj przed 2 instancjami”. Podpowiedź dla autora: na liście rzadkie rzeczy (nazwiska, nazwiska z domu, małe miejscowości), duże miasta nie |
| D7 | **Jednorazowy skan treści `HEAD` trzech repo** (tryb skryptu `-ScanTracked`) | **tak** — ten sam dopasowywacz na wszystkich śledzonych plikach. Wynik: liczba trafień i `repo/plik:linia, linia k listy`, bez słów | commity od 2026-10-07 (po przeglądzie [[NT-008-publication-review]]) nie były przeszukane nazwami z notatek, a są publiczne. Skan `HEAD` zamyka to tanio. Trafienie = incydent → STOP i zgłoszenie autorowi. **Nie obejmuje** linii usuniętych we wcześniejszych commitach |

### Scope diff vs the item (to accept at stop #1)
- **dochodzi D7** (skan `HEAD`) — poza *What to build*, ten sam kod, nowy tryb wywołania;
- dochodzi maskowanie ścieżek (D5) i rozpoznanie camelCase (D4) — doprecyzowanie „bez echa” i „początku słowa”;
- *Do decyzji na stopie #1* z pozycji → D2 (brak listy), D3 (które linie); kody i numery na liście: **nie** w v1
  (lista to słowa; numery kwater i kody pocztowe sprawdza skan wzorców w `qa`).

### Steps (dev)
1. `family-data-guard.ps1`: odczyt `family_data_dir` z konfiguracji; `Get-Stems` (D1, D2, D4: walidacja ≥3 litery,
   numer linii listy przy każdym rdzeniu). Wyjątek albo nieczytelna lista → `exit 2` (fail-closed, jak dziś).
2. `ConvertTo-Folded` (D4) i jeden połączony wzorzec dla wszystkich rdzeni.
3. `Get-AddedLines` (D3a–c): dwa wywołania `git diff` na repo z `-c core.quotepath=off -c color.ui=never`, parser
   nagłówków `diff --git`, `+++ b/…` i `@@ … +c,d @@` (numery linii nowej wersji); pliki nieśledzone z
   `Get-CommitCandidates` czytane bezpośrednio; binarne pomijane.
4. Gałąź `Bash|PowerShell` po sprawdzeniu typów: treść komendy (D3d) + dodane linie + ścieżki → trafienia →
   `Stop-Refuse` z komunikatem D5. Typy plików sprawdzane **przed** treścią.
5. Tryb `-ScanTracked` (D7): `git ls-files -z` w trzech repo, ten sam dopasowywacz, wynik na stdout, `exit 1`
   przy trafieniach.
6. Nagłówek skryptu (*WHAT IT DOES / DOES NOT CATCH*): treść z listy autora; granice z pozycji.
7. `family-data.md`: (a) *Family data on this PC* — skrypt strażnika jako jedyny czytelnik `rdzenie-straznika.txt`;
   agent go nie otwiera, nie tworzy i nie edytuje; (b) tabela *Mechanisms* — nowy wiersz z granicami.
   `project-config.example.md` → komentarz przy `family_data_dir`.
8. Pomiar czasu `git add`/`commit` (mediana z 3, jak ISSUE-006) z listą ~30 wymyślonych rdzeni.

Edycje skryptu strażnika i reguł klasyfikator może zablokować jako zmianę własnych uprawnień → `dev` podaje
autorowi dokładne linie.

### Files likely touched
- `grobing-agents/.claude/hooks/family-data-guard.ps1` — `dev`;
- `grobing-agents/.claude/hooks/tests/family-data-guard.tests.ps1` — `qa`;
- `grobing-agents/.claude/rules/family-data.md`, `.claude/rules/project-config.example.md` — `dev` (krok 7);
- ta pozycja — `planning` (plan), `dev` (*Dev report*), `qa` (*Verification*); `CURRENT_STATE.md` — `docs`.

`.claude/settings.json` zostaje (limit 30 s), chyba że pomiar z kroku 8 pokaże coś blisko limitu.

### AC → checks (`qa`)
| AC | Sprawdzenie |
|---|---|
| AC-1 | test w kopii repo w `%TEMP%`: lista z wymyślonymi rdzeniami; plik ze słowem odmienionym, wielkimi literami, bez polskich znaków i w camelCase → `exit 2`; stderr zawiera plik i linię, **nie zawiera** rdzenia, słowa ani linii (także w postaci bez polskich znaków) |
| AC-2 | `git commit -m` i heredoc `-F -` ze słowem → `exit 2` bez słowa; `-F <plik>` też |
| AC-3 | czyste zmiany przechodzą; pomiar z kroku 8 zapisany obok ~700 ms z ISSUE-006 |
| AC-4 | prawdziwe uruchomienie z prawdziwą listą (kroki niżej) |
| AC-5 | `family-data.md` po zmianie: czytelnik listy, granice, status „działa” |
| D2 | brak listy, pusta lista, rdzeń 2-literowy → `exit 2` z komunikatem bez treści listy |
| D5 | ścieżka z rdzeniem w nazwie → odmowa ze ścieżką zamaskowaną |
| D7 | `-ScanTracked` w kopii testowej: trafienie i brak trafienia |

### Manual verification (stop #2) — kroki według miejsca
**Autor — przed uruchomieniem naprawdę** (to nie odczucie, tylko lista, której agent nie może napisać):
- *Notatnik, poza VS Code:* utwórz `rdzenie-straznika.txt` w `family_data_dir`: nazwiska, nazwiska z domu, małe
  miejscowości i nazwy cmentarzy z notatek, jeden rdzeń w linii, plus wymyślony rdzeń testowy **`Zmyslonowsk`**.
  Agent tego pliku nie otworzy.

**Agent — w repo, przed stopem #2 (R4):**
1. plik próbny w `grobing-agents` ze słowem „Zmyślonowska” → `git add` → odmowa bez słowa; plik usunięty;
2. `git add` paczki tej pozycji z prawdziwą listą → przechodzi (zero fałszywych trafień w zmianach tej pozycji);
3. `-ScanTracked` na trzech repo → liczba trafień w *Verification*. Trafienie → STOP i zgłoszenie autorowi. Jeśli
   klasyfikator zablokuje agentowi uruchomienie skryptu, który czyta listę, krok 3 robi autor w terminalu VS Code
   i wkleja samą liczbę.

**Autor — odczucie:** brak (pozycja bez ekranu).

### Out of Scope (this plan)
- sprawdzanie treści przy `Write`/`Edit` (R1: kontrola przed `git add`);
- lista wyjątków dla fałszywych trafień (D6);
- historia sprzed `HEAD` (linie usunięte w starszych commitach);
- imiona, kody i numery na liście;
- commity autora z VS Code (tam dalej `.gitignore`).

### Falsifier — what will show this shape is wrong
- skan `HEAD` (D7) albo pierwsze tygodnie dają **fałszywe trafienia częściej niż raz na pozycję** → rdzenie na
  początku słowa są za szerokie dla miejscowości; wtedy lista wyjątków albo same nazwiska;
- koszt `git add`/`commit` rośnie powyżej ~1,5 s → skan trzech repo przy każdym wywołaniu trzeba zawęzić;
- komunikat strażnika kiedykolwiek zawiera słowo z listy → konstrukcja „bez echa” nie działa; test AC-1 ma to
  złapać przed użyciem.

### Self-check (planning) — said out loud
- **Wystarczalność:** strażnik dalej nie widzi treści zapisanej poleceniem powłoki aż do `git add` (ta sama
  granica co ISSUE-006) ani treści w commitach autora z VS Code.
- **Ryzyko pozycji:** pierwsze uruchomienie z prawdziwą listą jest jedynym miejscem, gdzie skrypt czyta prawdziwe
  rdzenie. Testy używają wyłącznie wymyślonych (`Zmyslonowsk`, `Wymyslin`).
- **Własność:** `planning` napisał tę sekcję i `status: in-progress`; wiersza macierzy nie ma (pozycja procesu).

## Dev report
> `dev`, 2026-10-08. Stop #1: „tak” (D1–D7 z rekomendacjami).

### What was built
- `family-data-guard.ps1` (kroki 1–6 planu): lista rdzeni z `family_data_dir` (D1, UTF-8 / UTF-16 / Windows-1250);
  blokada przy braku listy, pustej liście i rdzeniu krótszym niż 3 znaki (D2); dodane linie z `git diff --cached`
  i `git diff`, pliki nieśledzone, ścieżki, tekst komendy i plik `-F` (D3); jeden wzorzec z klasami znaków
  zamiast zamiany tekstu — każda litera rdzenia dopasowuje swoje warianty z diakrytykami i obie wielkości, a
  początek słowa to „brak litery przed” albo przejście mała → wielka (D4); komunikat z plikiem, linią i numerem
  linii listy, ścieżki z `***` w miejscu trafionego słowa, najwyżej 20 trafień w komunikacie (D5); tryb
  `-ScanTracked` (D7). Skrypt zostaje w ASCII: mapa liter z diakrytykami powstaje z punktów kodowych
  U+00C0…U+017F (NFD) plus ł, đ, ø.
- `family-data.md`: lista rdzeni w *Family data on this PC*, nowy wiersz w *Mechanisms*, wiersz hooka odsyła do niego.
  `project-config.example.md`: komentarz przy `family_data_dir`.

### Measured on the way (dev smoke, scratchpad, wymyślone rdzenie `Zmyslonowsk`, `Wymyslin`)
- **14 z 14 przypadków** zgodnych z planem, w żadnym komunikacie nie ma rdzenia ani słowa: brak listy, czysto,
  plik nieśledzony z polskimi literami (linia 2), zmiana w indeksie wielkimi literami, zmiana w drzewie w camelCase
  (linia 3), rdzeń w środku słowa (przechodzi), `-m`, heredoc `-F -`, ścieżka (zamaskowana), `-F` brak pliku, `-F`
  plik ze słowem, lista w Windows-1250, rdzeń 2-literowy, lista bez rdzeni. `-ScanTracked`: 1 trafienie, `exit 1`.
- **Czas `git add`** (3 repo, jedna zmiana, 30 rdzeni, mediana z 3, ten sam układ): **~1145 ms**; strażnik sprzed
  tej pozycji w tym samym układzie **~953 ms**. Dokłada ~0,2–0,3 s, poniżej progu ~1,5 s z falsyfikatora. (ISSUE-006
  mierzył ~700 ms na prawdziwych repo przez owijacz z `settings.json` — inny układ, liczby nieporównywalne 1:1.)

### Deviations
1. **`Invoke-Git` czyta stderr w tle** (poza planem): `git diff` wypisuje ostrzeżenia CRLF dla każdego pliku. Przy
   wielu plikach pełny potok stderr mógłby zawiesić git, a strażnik czekał na stdout — do limitu 30 s. Dodatkowo
   `-c core.safecrlf=false` przy diffach.
2. **`Get-CommitCandidates` parsuje `git status` ściśle**: nieznany wpis → wyjątek → blokada (fail-closed); ścieżka
   źródłowa przy rename/copy brana z następnego pola, a nie zgadywana z wyglądu wpisu (wcześniej porównanie było bez
   wielkości liter, więc ścieżka „ma c.txt” mogła udawać wpis statusu).
3. **`-F <plik>`, którego strażnik nie znajdzie → odmowa** z podpowiedzią `-m` albo `-F -`. Plan nie mówił, co wtedy;
   wybrane fail-closed jak reszta.
4. **Plik większy niż 20 MB → trafienie** („treści nie sprawdzono”), fail-closed. Największy plik tekstowy w repo
   to dziś ok. 1,9 MB (`assets/cemeteries/poland_cemeteries.json`).
5. **`-ScanTracked` czyta pliki z drzewa roboczego**, nie `git show HEAD:`. Przy czystych repo to ta sama treść.

### For `qa`
- **Testy z ISSUE-006 nie przejdą bez zmiany:** `Write-TestConfig` nie zapisuje `family_data_dir`, więc każdy
  przypadek z `git add`/`commit` dostanie teraz „brak listy rdzeni” (D2). Konfiguracja testowa potrzebuje
  `family_data_dir` z wymyśloną listą.
- **Prawdziwy hook działa od zapisu skryptu:** do czasu, aż autor utworzy listę, każde `git add`/`commit` w tej sesji
  jest zablokowane (D2, zgodnie z planem).
- Kroki ręczne: *Implementation plan* → *Manual verification* (bez zmian).

## Verification
> `qa`, 2026-10-08.

### Automated (`powershell -NoProfile -File .claude/hooks/tests/family-data-guard.tests.ps1`)
**150 z 150.** Testy ISSUE-006 przechodzą po dodaniu `family_data_dir` z wymyśloną listą do konfiguracji testowej.
Nowe przypadki (kopia trzech repo w `%TEMP%`, wyłącznie wymyślone rdzenie):
- **AC-1:** plik nieśledzony z polskimi literami (linia 2) · zmiana w indeksie wielkimi literami bez polskich znaków ·
  zmiana w drzewie wobec indeksu w camelCase (linia 3) · `snake_case` · rdzeń dwuwyrazowy ze spacjami i tabulatorem ·
  rdzeń w środku słowa przechodzi · `Write` ze słowem w treści przechodzi (treść sprawdza `git add`, R1);
- **AC-2:** `-m`, heredoc `-F -`, `-F <plik>` ze słowem → odmowa; `-F <brak pliku>` → odmowa; `-F <czysty plik>` →
  przechodzi;
- **D1** lista w Windows-1250, UTF-8 z BOM, UTF-16 z BOM i CRLF · **D2** brak listy (zapis plików i inne komendy
  przechodzą), lista bez rdzeni, rdzeń 2-literowy (numer linii listy), brak `family_data_dir` · **D3** plik binarny
  nieczytany · **D5** ścieżka z `***` · **D7** `-ScanTracked` bez trafień (`exit 0`) i z trafieniem (`exit 1`,
  plik:linia i linia listy) · owijacz z `settings.json` z komendą `git add` → odmowa;
- **każda odmowa treści i wynik skanu** sprawdzone wzorcem: ani rdzeń, ani słowo, ani znacznik z treści linii nie
  pojawia się w komunikacie.

**AC-3 (koszt):** `git add`, 3 repo, jedna zmiana, 30 rdzeni — mediana **958 ms** w testach (repo bez commitów);
w smoke `dev` 1145 ms wobec 953 ms strażnika sprzed pozycji. Poniżej ~1,5 s z falsyfikatora.

**AC-5:** `family-data.md` po zmianie: czytelnik listy (*Family data on this PC*), wiersz w *Mechanisms* z granicami,
status „działa”.

### Family data in the changes
Wzorce (kody pocztowe, PESEL, współrzędne, adresy, numery kwater): 0. Nazwy własne w zmianach: tylko wymyślone
rdzenie testów i przykład z opisu (`Zmyslonowsk…`, `Wymyslin`, „Stare Wymyślone”). Notatek rodziny `qa` nie
czytał.

### Deviation from the plan — test stem for AC-4
Rdzeń `Zmyslonowsk` z planu stoi w testach i w tekście tej pozycji. Na prawdziwej liście zablokowałby commit paczki,
więc autor musiałby go usuwać przed commitem. **Rdzeń testowy dla AC-4 podaje czat, a nie żaden plik w repo**, i
może zostać na liście na stałe. Ma ł i ź, więc sprawdza też odczyt polskich liter z pliku autora.

### Decision at stop #2 — who writes the list (author, 2026-10-08)
Autor: *„To jest ok że nazwiska będą tutaj (to nie są aż tak wrażliwe dane) — zależało mi najbardziej na tym żeby
takie informacje nie trafiały na githuba aby ktoś z zewnątrz sprawdzając moje repo zobaczył gdzie kto jest pochowany
z mojej rodziny”*. Zagrożenie to **publikacja na GitHubie, nie rozmowa z agentem**. Skutek:
- listę spisał agent z notatek w `family_data_dir`, na prośbę autora (odczyt zdjęć notatek klasyfikator tym razem
  przepuścił);
- zapis „agent tego pliku nie tworzy, także za zgodą” z *What to build* i z kroku 7 planu przestaje obowiązywać.
  Skrypt strażnika (nagłówek, komunikat) już to mówi; **`family-data.md` poprawia autor** — tę edycję klasyfikator
  zablokował agentowi jako zmianę własnych reguł;
- komunikat bez słowa (D5) zostaje: nic nie kosztuje i trzyma nazwiska poza logami narzędzi.

### AC-4 — real run (2026-10-08)
Lista: **28 rdzeni** — 13 nazwisk, 4 nazwiska z niepewnym odczytem pisma (oznaczone na liście do sprawdzenia przez
autora), 10 rdzeni miejscowości i cmentarzy, 1 rdzeń testowy (wymyślony, z ł i ź, nie stoi w żadnym repo).
1. **Plik próbny** w `grobing-agents` z rdzeniem testowym, `git add --dry-run` → **odmowa**: plik:linia i numer linii
   listy, bez słowa; polskie litery z pliku listy odczytane dobrze. Ta sama próba przejrzała wszystkie zmiany tej
   pozycji w trzech repo — **0 innych trafień**. Plik próbny usunięty.
2. **`-ScanTracked`** (360 śledzonych plików w trzech repo):
   - przebieg 1 (29 rdzeni): 353 trafienia, wszystkie w danych publicznych — wyciąg OSM
     `assets/cemeteries/poland_cemeteries.json` oraz jedno duże miasto z 9 miast mapy Polski (kod, testy, specyfikacja
     mapy, Natural Earth). **Ten rdzeń usunięty z listy** (D6, pierwsze fałszywe trafienie: miasto samo nie wskazuje
     grobu);
   - przebieg 2 (28 rdzeni): 293 trafienia, **wszystkie w `poland_cemeteries.json`**; przeszukanie trzech repo tymi
     samymi rdzeniami także w środku słów, poza tym plikiem: **0**.

**Incydentów: 0** — w treści `HEAD` trzech repo nie ma żadnego nazwiska z notatek. Granica: linie usunięte w starszych
commitach nie były przeszukane.

**Znany skutek na przyszłość:** wyciąg OSM to jeden wiersz JSON. Odświeżenie bazy cmentarzy (README `grobing-code`)
doda ten wiersz od nowa i strażnik go odrzuci przez rdzenie miejscowości. Wtedy wyjątek dla ścieżki tego pliku —
osobna pozycja, decyzja autora (D6: lista wyjątków przy drugim fałszywym trafieniu).

**Po odczycie notatek:** przeszukanie wszystkich zmian tej sesji w trzech repo rdzeniami z listy — 0 trafień (pamięć
agenta: grep po czytaniu `family_data_dir`); w vaulcie są tylko liczby.

**Testy po zmianie komunikatu:** 150 z 150; mediana `git add` 1110 ms (30 rdzeni, kopia w `%TEMP%`).

### Verdict
**APPROVED (self-check, z uwagami):** wszystkie AC sprawdzone, AC-4 na prawdziwej liście. Uwagi: (1) linia w
`family-data.md` czeka na autora — bez niej reguła mówi co innego niż praktyka, więc `docs` nie commituje przed nią;
(2) 4 niepewne odczyty nazwisk na liście; (3) przyszłe odświeżenie wyciągu OSM zostanie odrzucone. Czego szukałem i nie
znalazłem: przecieku słowa w komunikatach (wzorzec w każdym teście treści), trafień nazwisk w `HEAD`, danych rodziny w
zmianach tej pozycji.
