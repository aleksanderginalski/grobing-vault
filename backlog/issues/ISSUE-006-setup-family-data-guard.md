---
title: "ISSUE-006 — PreToolUse guard that refuses family-data files in any repo"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: 0.5
quality-verdict: APPROVED
verdict-date: 2026-10-05
verdict-reviewer: self-check
created: 2026-10-05
updated: 2026-10-05
---

# ISSUE-006 — Family-data guard (T-05: the only real veto)

> Meta-decyzja 3h. Uzasadnione, bo w tym projekcie jest **jedna nieodwracalna akcja: wypchnięcie danych
> rodziny** do repo, które może dostać remote. Do czasu zbudowania chronią: reguła `family-data.md`
> (ładowana) i `.gitignore` w trzech repo.

## What to build
Hook `PreToolUse` w `grobing-agents/.claude/settings.json`, który **odmawia** (`deny`) zapisu i
`git add` plików: `*.db`, `*.sqlite*`, kopii (`*.grobing-backup`), eksportów, zdjęć spoza zasobów UI —
w **każdym z trzech repo**, rozpoznając je po typie i lokalizacji.

**Czego NIE daje — powiedziane uczciwie:** rozpoznaje plik, **nie treść**. Prawdziwego nazwiska
wpisanego w kod albo dokumentację nie zauważy — tę połowę pilnuje krytyk (powód BLOCK „dane rodziny w
repo", [[ISSUE-003-setup-quality-critic]]).

## Acceptance Criteria
- [x] Skrypt istnieje; dopiero potem hook. Brak skryptu → `exit 2`, nigdy cisza.
- [x] Zero ścieżek absolutnych; repo rozpoznawane z `project-config.md`.
- [x] **Uruchomiony raz naprawdę:** próba zapisu `test.db` w `grobing-code` została odrzucona z
      czytelnym komunikatem.
- [x] Granica (plik, nie treść) zapisana w `family-data.md` — status mechanizmu z „plan" na „działa".

## Implementation plan
> `planning`, 2026-10-05. Pozycja nie dotyka warstwy danych aplikacji, więc test migracji, próbne
> odtworzenie z kopii i źródło faktu nie mają tu zastosowania. **DoR:** pozycja startowa z kick-offu
> (MD3h, T-05), bez kroku ścieżki i bez US, tak jak ISSUE-001 i ISSUE-002. Dlatego nie ma wiersza w
> `TRACEABILITY.md`. **Korekta opisu:** wzorzec `*.grobing-backup` z *What to build* jest sprzed
> [[ADR-004-backup-format-encryption-destination]]. Kopia i plik klucza to pliki `age`
> (SPIKE-003: `grobing-*.age`), wnętrze kopii to `tar`, a eksport to HTML + PDF.

### Prior art (sources, not memory)
- **Dokumentacja hooków Claude Code** ([hooks](https://code.claude.com/docs/en/hooks.md),
  [hooks-guide](https://code.claude.com/docs/en/hooks-guide.md)):
  - `PreToolUse`: `exit 2` blokuje, a stderr trafia do Claude'a;
  - **`exit 1` i inne kody nie blokują** (akcja przechodzi);
  - **brak skryptu = błąd „command not found”, nie blokada**;
  - `deny` działa także w trybie `bypassPermissions`;
  - `PowerShell` to osobna nazwa narzędzia w matcherze;
  - `$CLAUDE_PROJECT_DIR` wskazuje korzeń projektu;
  - zmiany hooków w `settings.json` w trakcie sesji „normalnie” działają od razu;
  - **nieudokumentowane:** czy hook działa dla plików w katalogach dodatkowych i dla subagentów → AC-3
    i krok `qa` sprawdzają to naprawdę.
- **NPG-Agents** `.claude/settings.json` (hook `check-wiring`): `"shell": "powershell"`,
  `$env:CLAUDE_PROJECT_DIR`, a gdy skryptu nie ma, `exit 2` z komunikatem. **To jest wzorzec AC-1**,
  przejęty 1:1.
- **CAMPUS** `tools/guard-branch.py`: strażnik `PreToolUse` dla `Write|Edit`. Docstring uczciwie mówi
  „czego nie złapie” (zapis przez powłokę), więc tak samo opisujemy granice tutaj.

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego |
|---|---|---|---|
| D1 | **Język skryptu** | **Windows PowerShell 5.1** (`"shell": "powershell"`), wzorzec NPG | **zmierzone 2026-10-05:** start ~190 ms przy każdym wywołaniu, Python ~95 ms. Python jest w `PATH` tylko z katalogu tej maszyny. Na innej maszynie samo `python` dałoby „command not found”, a to według dokumentacji **nie blokuje**, czyli strażnik przepuszczałby wszystko po cichu. PowerShell 5.1 jest w każdym Windowsie |
| D2 | **Co jest „plikiem danych rodziny”** (wspólna lista: hook + `.gitignore` w 3 repo) | **bazy:** `*.db`, `*.db-journal`, `*.db-wal`, `*.db-shm`, `*.sqlite`, `*.sqlite3`, `*.sqlite-*` · **kopia (ADR-004):** `*.age`, `*.tar` · **eksport (ADR-004):** `*.html`, `*.pdf` · **zdjęcia i filmy:** `*.jpg`, `*.jpeg`, `*.png`, `*.heic`, `*.heif`, `*.webp`, `*.gif`, `*.bmp`, `*.tif`, `*.tiff`, `*.dng`, `*.mp4`, `*.mov`; **jedyny wyjątek:** obrazy w `grobing-code/android/app/src/main/res/` (ikony) · **katalogi w korzeniu repo:** `/exports/`, `/backups/`, `/family-data/`, `/real-data/` | rozpoznanie po typie, a nie po nazwie, działa niezależnie od tego, jak produkcyjna kopia i eksport nazwą pliki. Dziś w trzech repo nie ma ani jednego takiego pliku poza 5 ikonami `ic_launcher.png` (sprawdzone `git ls-files`). Wyjątki tylko z instancji: `assets/` (grafiki UI we Flutterze) i `05_DESIGN/` w vaulcie dochodzą, gdy pojawi się pierwszy taki plik |
| D3 | **Jak łapać `git add` / `git commit`** (Bash i PowerShell) | Każda komenda z `git … add` albo `git … commit`: (a) `git add -f`/`--force` → **odmowa** (agent tego nie potrzebuje, autor może sam); (b) w każdym z 3 repo: pliki w indeksie (`git diff --cached --name-only`) + zmienione i nieśledzone, które nie są ignorowane (`git status --porcelain --untracked-files=all`) → którykolwiek pasuje do D2 → **odmowa z listą plików**. **Bez** pola `if` w hooku | nie parsujemy ścieżek (`.`, `-A`, `-u`, `-C`, `commit -am`), tylko patrzymy na to, co mogłoby trafić do commita. Koszt: ~60 ms × 3 (zmierzone). Łapie też pliki, które weszły do drzewa **inną drogą** niż `Write` (`cp`, `>`, `adb pull`, zdjęcie wklejone w Obsidianie). Pole `if` (`Bash(git *)`) skróciłoby czas, ale jego dopasowanie jest *best-effort*. Gdyby nie odpaliło się przy `cd x && git add .`, strażnik przepuściłby po cichu |
| D4 | **Gdy coś pójdzie nie tak** | **fail-closed:** każdy wyjątek w skrypcie, brak `project-config.md`, pusta albo nieistniejąca ścieżka repo → `exit 2` z komunikatem, co naprawić. Komendy powłoki, które nie są `git add`/`commit`, przechodzą od razu, bez czytania konfiguracji | `exit 1` nie blokuje (dokumentacja), więc nieobsłużony wyjątek PowerShella byłby cichym przepuszczeniem. Brak konfiguracji naprawia autor ręcznie (kopia `project-config.example.md`, jak mówi `CLAUDE.md`) |

### Scope diff vs the item (to accept at stop #1)
- **+ `.gitignore` w trzech repo:** ten sam blok danych rodziny według D2, zamiast dzisiejszych
  rozjechanych bloków. Powód: hook chroni tylko narzędzia Claude'a, a **commit autora z VS Code przechodzi
  wyłącznie przez `.gitignore`** (brief: „`.gitignore` + hook”). Dziś `.gitignore` nie zna ani `*.age`,
  ani zdjęć, ani HTML/PDF.
- **+ poprawka znaleziona przy okazji:** `backups/` i `exports/` w `.gitignore` nie mają kotwicy, więc
  pasują do katalogu o tej nazwie **na każdym poziomie**. Przyszły kod funkcji kopii w
  `lib/…/backups/` zostałby po cichu zignorowany. Wpisy dostają kotwicę `/backups/`, `/exports/` itd.
- **+ wyjątek dla ikon w `grobing-code`:** negacja **osobno dla każdego rozszerzenia obrazu**
  (`!/android/app/src/main/res/**/*.png` itd.), a nie dla całego katalogu, bo `!…/res/**` odblokowałoby
  też `*.db` w `res/`.
- **+ `*.grobing-backup` znika** z `.gitignore` i z `family-data.md`. To nazwa, której nic nie tworzy.

### Steps (dev)
1. **Skrypt najpierw** (AC-1): `grobing-agents/.claude/hooks/family-data-guard.ps1`.
   - Czyta JSON ze stdin: `tool_name`, `tool_input.file_path` / `notebook_path` / `command`, `cwd`.
   - Korzeń `grobing-agents` bierze z położenia skryptu, a vault i kod z
     `.claude/rules/project-config.md` (`vault_local_path`, `code_local_path`; odescapowane `\\`).
     Parametr `-ConfigPath` jest tylko dla testów.
   - Ścieżki normalizuje: wielkość liter, `\` → `/`, `/c/…` → `c:/…`, względne wobec `cwd`.
   - **Zapis** (`Write|Edit|MultiEdit|NotebookEdit`): plik w którymś z 3 repo pasuje do D2 → `exit 2`.
     Poza repo (scratchpad, `_throwaway/`) przepuszcza.
   - **Powłoka** (`Bash|PowerShell`): według D3. Inne komendy → `exit 0` od razu.
   - Całość w `try/catch` → `exit 2` (D4).
   - Komunikat po polsku: **co** zablokowano (ścieżka względna z nazwą repo), **dlaczego** (kategoria
     D2 + `family-data.md`), **co zrobić zamiast** (dane testowe: wymyślone osoby, baza w pamięci albo w
     katalogu tymczasowym poza repo).
   - Nagłówek skryptu: co łapie i **czego nie łapie** (wzorzec CAMPUS).
2. **Dopiero potem hook** w `grobing-agents/.claude/settings.json`: `PreToolUse`, matcher
   `Write|Edit|MultiEdit|NotebookEdit|Bash|PowerShell`, `"shell": "powershell"`, `timeout` 30. Komenda
   według wzorca NPG: `$env:CLAUDE_PROJECT_DIR` → `Test-Path` skryptu → brak = komunikat na stderr i
   `exit 2`; jest = uruchom i przekaż `$LASTEXITCODE`. **Zero ścieżek absolutnych** (AC-2).
3. `.gitignore` × 3 według *Scope diff*. Sprawdzenie `git check-ignore -v` na próbnych nazwach (bez
   tworzenia plików w repo) i na istniejących `ic_launcher.png`: **nie** są ignorowane.
4. `family-data.md` (AC-4), tabela *Mechanisms*:
   - `.gitignore` „w trzech repo, wzorce z ISSUE-006”;
   - hook: „**działa**” + czego nie łapie: treści (nazwisko w kodzie albo dokumencie → krytyk); zapisu
     komendą powłoki **w chwili zapisu** (złapie go dopiero przy `git add`/`commit`); commita autora z
     VS Code (tam działa tylko `.gitignore`); edycji samego skryptu albo `.gitignore` (widać ją w diffie
     na stopie #3);
   - wiersz „każdy” w tabeli agentów: `*.age` zamiast kopii bez typu.
5. `project-config.example.md`, ostatni akapit: z `project-config.md` czyta też hook strażnika.

### AC → evidence
| AC | Dowód |
|---|---|
| 1 skrypt, potem hook; brak skryptu → `exit 2` | **test:** dokładna komenda z `settings.json` uruchomiona z `CLAUDE_PROJECT_DIR` wskazującym katalog bez skryptu → `exit 2` + komunikat; kolejność kroków widać w diffie |
| 2 zero ścieżek absolutnych; repo z `project-config.md` | **test:** tymczasowe repo git w `%TEMP%` + tymczasowy config (`-ConfigPath`). Zapis `x.db` w środku → `exit 2`, poza → `exit 0`; brak configu → `exit 2`; grep `settings.json` i skryptu: brak `[A-Za-z]:[\\/]` |
| 3 uruchomiony raz naprawdę | `qa` w tej sesji: `Write` `grobing-code/test.db` → odmowa z komunikatem (to sprawdza też **katalog dodatkowy**, którego dokumentacja nie opisuje); to samo z subagenta; autor ocenia komunikat na stopie #2 |
| 4 granica w `family-data.md` | diff tabeli *Mechanisms* |
| D2/D3 (zakres) | **testy** tabelą przypadków: każda kategoria D2 → `exit 2`; `ic_launcher.png` w `res/` → `exit 0`; `lib/x.dart` → `exit 0`; `git add .`, `git -C … add -A`, `git commit -am` z plikiem `proba.age` nieśledzonym w repo testowym → `exit 2`; `git add -f` → `exit 2`; `git status` → `exit 0`; ścieżki `/c/…` i `C:\…` dają ten sam wynik. `git check-ignore -v` w 3 repo |

Test: `grobing-agents/.claude/hooks/tests/family-data-guard.tests.ps1`. Czysty PowerShell, bez Pestera
(w Windows jest tylko stary 3.4), osobny proces na każdy przypadek, wyłącznie wymyślone nazwy plików.

### Manual verification (stop #2, po polsku, według miejsca)
- **VS Code, panel Claude Code:** wpisz `/hooks` → `PreToolUse` z naszym matcherem, źródło
  *Project settings*. Jeśli go nie ma, zrestartuj sesję Claude Code i sprawdź ponownie.
- **Napisz tutaj:** „spróbuj zapisać pusty plik test.db w grobing-code” → Claude dostaje odmowę.
  **Czy z komunikatu od razu wiesz, co się stało i co zrobić?**
- **Eksplorator Windows:** skopiuj dowolny **nierodzinny** obraz (np. zrzut ekranu) jako
  `grobing-vault/01_INBOX/proba.jpg` i utwórz pusty `grobing-code/proba.age` → **VS Code, Source Control**:
  żaden z nich się nie pokazuje. Potem usuń oba.

### Out of Scope
- **Treść** (prawdziwe nazwisko wpisane w kod albo dokument) → [[ISSUE-003-setup-quality-critic]].
- Git `pre-commit` w trzech repo (łapałby też commit autora z GUI poza `.gitignore`). Bez sygnału, że
  `.gitignore` nie wystarcza; byłby osobną pozycją.
- Bramka na pushu → [[DEF-005-push-gate]]; przegląd historii przed pushem → [[NT-008-publication-review]].
- Wyjątki `assets/` i `05_DESIGN/` — dopisze je pozycja, przy której pojawi się pierwszy taki plik.

### Closing checklist (docs)
- [[NT-008-publication-review]] → *Progress*: punkt 1 zamknięty (data), otwarty zostaje tylko wybór dla
  vaulta.
- `CURRENT_STATE.md`: z warunków przed pierwszym pushem zostaje NT-008.
- Paczka na stop #3 obejmuje **trzy repo**: `grobing-agents` (skrypt, test, `settings.json`,
  `family-data.md`, `project-config.example.md`, `.gitignore`), `grobing-vault` (`.gitignore`, ta
  pozycja), `grobing-code` (`.gitignore`). **Bez pusha.**

## Verification
> `qa`, 2026-10-05. Rytuał WZ-024: format → analiza → testy → kroki ręczne → czekaj. Format i analiza
> Darta nie dotyczą tej pozycji (zmiany w PowerShellu, JSON-ie, `.gitignore` i Markdownie).

### Automated (done)
| Co | Jak | Wynik |
|---|---|---|
| **AC-3 naprawdę, w sesji** | `qa`: `Write` `grobing-code/test.db` | ✅ odmowa z pełnym komunikatem; plik nie powstał. Hook zadziałał **po edycji `settings.json` w trakcie sesji, bez restartu**, i w **katalogu dodatkowym** (dokumentacja tego nie opisuje) |
| AC-3 w subagencie | subagent: `Write` `grobing-code/probe-subagent.db` | ✅ odmowa, ten sam komunikat; plik nie powstał. **Hook działa też w subagentach** (nieudokumentowane) |
| AC-1, AC-2, D2–D4 | `grobing-agents/.claude/hooks/tests/family-data-guard.tests.ps1`: trzy tymczasowe repo w `%TEMP%`, kopia skryptu z własnym `project-config.md`, osobny proces na przypadek, wyłącznie wymyślone nazwy plików | ✅ **106/106** (43 s). Pokrywa: każdy typ z listy D2, katalogi w korzeniu, wyjątek ikon w `res/` (i jego brak dla `*.db`/filmów), `lib/…/backups/`, zapisy ścieżek (`/c/…`, wielkie litery, względna, `..`), `Edit`/`MultiEdit`/`NotebookEdit`, fail-closed (bez configu, pusta i błędna ścieżka, zły JSON, pusty stdin), `git add -f` w 4 zapisach, nieśledzony `proba.age` przy `add .`/`add -A`/`commit -am`/`add <inny plik>` (Bash i PowerShell), ten sam plik ukryty przez prawdziwy `.gitignore` → przechodzi, plik wciśnięty do indeksu → `commit` odrzucony; owijacz z `settings.json`: skrypt jest / brak / błąd składni / bez `exit` / wyjątek → zawsze `exit 2` |
| `.gitignore` = lista hooka | ten sam test, `git check-ignore --no-index` w **prawdziwych** trzech repo (tylko odczyt) | ✅ każdy typ z listy ignorowany w trzech repo; `lib/features/backups/` nie; ikony w `res/` nie; `*.db` i film w `res/` tak. **Rozjazd listy hooka i `.gitignore` wywali ten test** |
| Zero ścieżek absolutnych (AC-2) | grep `[A-Za-z]:[\\/]` w `settings.json` i skrypcie (część testu) | ✅ brak |
| Koszt (zmierzone, mediana z 3) | owijacz z `settings.json` | każda komenda powłoki **~320 ms**, każdy zapis **~390 ms**, `git add`/`commit` ze skanem trzech repo **~700 ms**. **Więcej niż ~190 ms z planu** (tam był sam start PowerShella) |
| Dane rodziny w zmianach | `git status --ignored` w 3 repo + przegląd diffów | ✅ zmienione tylko pliki tekstowe z planu; żadnych baz, kopii, zdjęć ani plików próbnych (smoke `dev` i sonda subagenta posprzątane). Ignorowane `android/gradlew` itp. pochodzą z `android/.gitignore` Fluttera, nie z tej zmiany. Brak imion i nazwisk w diffach |

### Notes (z uwagami)
1. **Komunikat w panelu:** Claude Code poprzedza stderr **pełną komendą owijacza**, a dopiero za nią jest
   komunikat strażnika. Na stopie #2 owijacz skrócony z ~600 do ~280 znaków (bez fallbacku na
   bieżący katalog: brak `CLAUDE_PROJECT_DIR` → brak skryptu → `exit 2`). Ochrona ta sama, testy 106/106
   po zmianie, odmowa `test.db` sprawdzona ponownie na żywo.
2. Komunikaty strażnika są **bez polskich znaków**, celowo: PowerShell 5.1 czyta `.ps1` bez BOM jako
   ANSI.
3. Kosmetyka na ścieżce błędu: polski komunikat .NET przy uszkodzonym JSON-ie ma krzaczki. Nadal
   `exit 2`.
4. Test tworzy tymczasowe repo `git init` w `%TEMP%`. Plan to przewidział (AC → evidence), a te repo
   nie są repozytoriami Grobing.

### Manual (stop #2) — autor oddał kroki agentowi („ty to zrób”, 2026-10-05)
| Krok | Wynik |
|---|---|
| 1 `/hooks` pokazuje hook | **pominięty** — komendy interfejsu agent nie uruchomi. Zastępczy dowód, mocniejszy: dwie odmowy na żywo (sesja + subagent) z hooka z *Project settings* |
| 2 czytelność komunikatu | **decyzja oddana agentowi** → owijacz skrócony (*Notes* 1). Ocena czytelności przez człowieka: **niewykonana** |
| 3–5 commit autora z VS Code nie widzi `proba.age` w kodzie i `proba.jpg` w `01_INBOX/` | **zastąpione** `git check-ignore -v --no-index` na tych nazwach w prawdziwych repo: `*.age` (kod) i `*.jpg` (vault) ignorowane. Plików agent **nie tworzył**: `Write` blokuje strażnik, a obejście przez powłokę byłoby tym, czego zabrania `family-data.md`. Panel *Source Control* korzysta z tych samych reguł gita, ale człowiek go nie oglądał |

### Verdict
**APPROVED (self-check, z uwagami)** — 2026-10-05. Wszystkie 4 AC mają dowód (AC-3 na żywo, AC-1/2 i
zakres D2–D4 w teście 106/106, AC-4 w diffie `family-data.md`). Uwagi:
- koszt ~320–390 ms na każde wywołanie narzędzia i ~700 ms na `git add`/`commit` jest wyższy niż w planie;
- stop #2 bez oczu człowieka (kroki oddane agentowi);
- *Notes* 2–4.

Brak wiersza w `TRACEABILITY.md`, więc kolumny Quality Verdict nie ma gdzie wpisać (pozycja startowa,
patrz nagłówek planu).

## Closure
`docs`, 2026-10-05. Commity: `grobing-agents` bf70669 · `grobing-vault` 0a319e3 · `grobing-code` 1a67014
+ commit zamknięcia w vaulcie. **Bez pusha** (warunek: [[NT-008-publication-review]]).

**Checklista zamknięcia (z planu):**
- ✅ [[NT-008-publication-review]] → *Progress*: punkt 1 zamknięty; otwarty zostaje wybór dla vaulta.
- ✅ `CURRENT_STATE.md`: z warunków przed pierwszym pushem zostaje NT-008.
- ✅ Paczka objęła trzy repo, bez pusha.

**DoD ISSUE (MVP):**
- testy dla każdego AC: 106/106;
- ręczna weryfikacja: kroki oddane agentowi; pominięcia i zastępcze dowody są zapisane w *Verification*,
  cisza nie została uznana za „pomiń”;
- zero danych rodziny w zmianach;
- nowych folderów w vaulcie brak (hook i test żyją w `grobing-agents`).

Warstwy danych aplikacji pozycja nie dotyka, więc odtworzenie z kopii i migracja nie mają zastosowania.
Opis w *What to build* (`*.grobing-backup`) zostaje jako zapis pierwotnej pozycji; obowiązującą listę
podają plan (D2) i `family-data.md`.
