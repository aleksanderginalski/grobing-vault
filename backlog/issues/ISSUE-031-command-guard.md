---
title: "ISSUE-031 — Command guard: refuse a Python script read from stdin and the git commands the boundary forbids"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: 0.5
quality-verdict: APPROVED
verdict-date: 2026-10-13
verdict-reviewer: self-check
source: "[[2026-10-13-retro-03]] R1"
created: 2026-10-13
updated: 2026-10-13
---

# ISSUE-031 — Strażnik komend (mechanizm zamiast pamięci)

> Decyzja autora w [[2026-10-13-retro-03]] (R1). Pozycja startowa procesu, tak jak [[ISSUE-006-setup-family-data-guard]] i
> [[ISSUE-020-content-guard]]: bez kroku ścieżki i bez US, więc bez wiersza w `TRACEABILITY.md`.

## Problem
Dwie rzeczy wracają mimo zapisu w pamięci agenta i w regułach:
- **`python -` / `python -I -`** (skrypt czytany z wejścia) — **8 razy** od SPIKE-001, w czterech kolejnych pozycjach (ISSUE-025,
  023, 028, 029). W tym środowisku komenda wisi, aż ktoś ją zatrzyma. Pamięć mówi „nigdy”, a token wraca z nawyku: raz jako
  „szablon” komendy, raz doklejony do łańcucha. Bez szkody dla plików, ale za każdym razem tracona runda;
- **komendy git zmieniające indeks poza commitem `docs`** — `git rm --cached` w ISSUE-014 (retro 2, R2), `git add -N .` i `git reset -q`
  w ISSUE-028 („tylko do liczenia”). Reguła `git-autonomy-boundary.md` je zakazuje, a nic ich nie zatrzymuje.

Strażnik danych rodziny pokazał, że mechanizm działa tam, gdzie wola nie działa.

## What to build
Hook `PreToolUse` w `grobing-agents` (narzędzia `Bash` i `PowerShell`), który **odmawia** komendy z czytelnym powodem i
podpowiedzią:
- **Python ze skryptem z wejścia:** `python`, `python3`, `py` (także `.exe`) z argumentem `-` albo bez skryptu i bez `-c`/`-m`
  → odmowa z podpowiedzią „zapisz skrypt w katalogu tymczasowym sesji i uruchom plik”;
- **git z *Forbidden autonomously*** (`git-autonomy-boundary.md`): `reset`, `restore`, `stash`, `rm`, `checkout`, `switch`,
  `rebase`, `merge`, `pull`, `fetch`, `commit --amend`, `branch -D/-d`, `init`, `remote add/set-url/remove`, `push` inny niż
  `git push origin main` (`--force`, `-f`, `--force-with-lease`, inna gałąź, tagi), `add` z `-A`, `--all`, `.`, `-u`, `-N`,
  `--intent-to-add`, wzorcem katalogu, `--no-verify` przy każdej komendzie, `gh`;
- **przechodzi bez zmian:** komendy tylko do odczytu (`status`, `diff`, `log`, `branch -l`, `branch --show-current`,
  `remote get-url`, `check-ignore`, `show`, `rev-parse`), `git add -- <jawne pliki>`, `git commit` (bez `--amend`, bez
  `--no-verify`), `git push origin main`.

Strażnik danych rodziny dalej robi swoje przy `git add`/`commit` — ten hook go nie zastępuje.

## Czego NIE daje — powiedziane uczciwie
- Komendy złożonej w locie (`bash -c "$(…)"`, zmienna z nazwą komendy, alias), skryptu z pliku, który sam woła zakazaną komendę,
  i komend autora z VS Code.
- Pamięć agenta o komendach zostaje. Hook łapie nawyk przy próbie, ale nie usuwa go.
- Zmianę `.claude/settings.json` klasyfikator Claude Code może zablokować agentowi (tak było przy edycji reguł w ISSUE-020) — wtedy
  autor wpisuje podaną linię sam.

## Acceptance Criteria
- [ ] Każda zakazana forma z *What to build* w teście hooka → odmowa z powodem i podpowiedzią; **falsyfikator: test, w którym
      któraś z nich przechodzi**.
- [ ] Każda forma z listy „przechodzi” w teście → bez odmowy; komendy łączone (`&&`, `;`, `|`) sprawdzane w całości.
- [ ] Przy własnym błędzie albo braku skryptu hook **blokuje** (jak strażnik danych rodziny, ISSUE-006) i mówi dlaczego.
- [ ] Testy strażnika danych rodziny dalej zielone; koszt hooka na wywołanie zmierzony i zapisany.
- [ ] `git-autonomy-boundary.md` → *Forbidden autonomously* mówi, który mechanizm łapie te komendy, i czego nie łapie.

## Do decyzji na stopie #1
- Osobny skrypt (`command-guard.ps1`) czy gałąź istniejącego `family-data-guard.ps1`? Kandydat: osobny skrypt — inna
  odpowiedzialność, a strażnik danych rodziny ma już 635 linii i 150 testów.
- Czy `git fetch` (bez zapisu w gałęziach roboczych) ma przechodzić? Reguła mówi dziś „`git fetch` z zapisem”.

## Notes / references
- [[2026-10-13-retro-03]] R1 · `grobing-agents/.claude/rules/git-autonomy-boundary.md` → *Forbidden autonomously* ·
  `.claude/hooks/family-data-guard.ps1` (wzorzec: fail-closed, testy w `.claude/hooks/tests/`).

## Implementation plan
> `planning`, 2026-10-13. Pozycja procesu bez ekranu i bez warstwy danych aplikacji: test migracji i próbne odtworzenie
> nie mają tu zastosowania. **DoR:** zakres jasny, `delivery-style: task-level`; bez US i bez kroku ścieżki, jak
> [[ISSUE-020-content-guard]], więc bez wiersza w `TRACEABILITY.md`.

### Prior art (sources, not memory)
- **Reguły `permissions.deny`** ([permissions](https://code.claude.com/docs/en/permissions) → *Compound commands*,
  *Wrappers*, *What a Bash rule doesn't match*): dzielą komendy złożone (`&&`, `;`, `|`, `$(…)`, ciała pętli) i zdejmują
  `time`, `nohup`, `xargs`… — ale dopasowują **tekst**: dokumentacja sama podaje, że `Bash(git push *)` nie łapie
  `git -C . push`, `git -c … push` ani `git 'push'`; Python ze skryptem z wejścia — tylko dokładny tekst. Wprost: reguła
  „covers the invocation Claude usually produces and isn't a security boundary”, a do sprawdzenia całej komendy własną
  logiką — hook `PreToolUse`.
- **Na Windowsie z Git Bash każda reguła `deny` dla Bash, także zawężona, wyłącza narzędzie PowerShell na całą sesję —
  bez ostrzeżenia** ([tools reference → PowerShell tool](https://code.claude.com/docs/en/tools-reference#powershell-tool)).
- **Hooki** ([hooks](https://code.claude.com/docs/en/hooks)): `exit 2` blokuje, stderr wraca do Claude'a; **wszystkie
  pasujące hooki biegną równolegle**, a odmowa wygrywa (deny > defer > ask > allow). **Hook, który przekroczy `timeout`,
  nie blokuje**, chyba że ma `"onFailure": "block"` (od 2.1.295). Sesje autora: rozszerzenie VS Code **2.1.296**;
  `claude` w `PATH` — 2.1.238 (nie zna tego klucza).
- **Strażnik danych rodziny** (ISSUE-006, ISSUE-020): wzorzec fail-closed, owijacz w `settings.json` („brak skryptu →
  `exit 2`”), testy jako osobny proces na przypadek; start PowerShell 5.1 ~190 ms (ISSUE-006 D1). Szuka `git … add|commit`
  w **całym tekście** komendy — tutaj tak nie można, bo `grep 'git reset'` i opis commita ze słowem „reset” dostałyby
  odmowę.

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego |
|---|---|---|---|
| D1 | **Mechanizm** | **hook-skrypt** `PreToolUse`, bez reguł `permissions.deny` | reguły nie łapią `-C`, `-c`, ścieżki do `git.exe`, `sh -c`; a każda reguła `deny` dla Bash po cichu wyłączyłaby PowerShell |
| D2 | **Gdzie** | **osobny skrypt** `command-guard.ps1` i **osobny wpis** w `settings.json` (matcher `Bash\|PowerShell`), obok strażnika danych rodziny | hooki biegną równolegle, więc czas ≈ wolniejszy z dwóch, a nie suma; inna odpowiedzialność; awaria jednego nie wyłącza drugiego. Strażnik ma 635 linii i 150 testów |
| D3 | **Git: lista dozwolonych, nie lista zakazanych** | przechodzi tylko: (a) **odczyt** — `status`, `diff`, `log`, `show`, `rev-parse`, `rev-list`, `ls-files`, `ls-tree`, `cat-file`, `check-ignore`, `blame`, `shortlog`, `describe`, `grep`, `merge-base`, `show-ref`, `for-each-ref`, `count-objects`, `version`, `help`, `var`; `branch` tylko jako lista (bez argumentów, `-l`, `--list`, `--show-current`, `-a`, `-r`, `-v`); `remote` tylko bez argumentów, `-v`, `get-url`; `config` tylko odczyt (`--get*`, `--list`/`-l`, sama nazwa klucza); `tag` tylko lista; (b) **`add`** jawnych plików — odmowa przy `-A`, `--all`, `.`, `:/`, `-u`, `-N`, `--intent-to-add`, `-f`, `-p`, `-i`, `-e`, znakach wzorca (`* ? [`), magii pathspec `:(` i ścieżce, która jest katalogiem; (c) **`commit`** — odmowa przy `--amend`, `-a`/`--all`, `-p`, `--interactive`; (d) **`push origin main`** (dopuszczalne `-q`, `--dry-run`). Opcje globalne `-C`, `-c`, `--no-pager`, `--git-dir`, `--work-tree` przechodzą. **`--no-verify`/`-n` przy commicie i pushu — zawsze odmowa.** `gh` — zawsze odmowa | nieznana komenda (`clean`, `mv`, `cherry-pick`, `revert`, `update-index`, `apply --index`) dostaje odmowę bez dopisywania; to dokładnie *Always allowed* + dwie sekcje *Allowed autonomously* z `git-autonomy-boundary.md` |
| D4 | **Python ze skryptem z wejścia** | `python`, `python3`, `python3.N`, `py` (także ze ścieżką i `.exe`): pierwszy argument, który nie jest opcją, to `-` → odmowa; **brak skryptu, `-c` i `-m`** (REPL) → odmowa. `-X`, `-W` biorą wartość; sklejone `-Iu` rozumiane. Podpowiedź: „zapisz skrypt w katalogu tymczasowym sesji i uruchom plik” | to forma, która wisiała 8 razy; `python -I plik.py` i `python -c "…"` przechodzą |
| D5 | **Parser komendy** (Bash i PowerShell) | treść **w cudzysłowach to tekst**, nie komenda (`echo "git reset"`, `grep 'git reset'`, opis w `-m` przechodzą); ciała heredoc (`<<EOF`, `<<'EOF'`, `<<-EOF`) i here-stringi PowerShell (`@'…'@`, `@"…"@`) wycinane — **ale** `-` po `python` przed heredociem zostaje w komendzie (D4). Podział na segmenty po `&&`, `\|\|`, `;`, `\|`, `&`, nowej linii, `( ) { }`, `$(`, odwróconym apostrofie; `$(…)` i `` `…` `` **w podwójnych cudzysłowach** parsowane osobno. Słowo komendy po: przypisaniach `X=1`, operatorze `&` PowerShella, nakładkach (`time`, `timeout N`, `nice`, `nohup`, `command`, `builtin`, `env`, `xargs`), słowach kluczowych (`if`, `then`, `do`, `else`, `elif`, `while`, `until`, `!`); nazwa bez ścieżki, `.exe` i wielkości liter. `bash`/`sh -c "…"` i `powershell`/`pwsh -Command "…"` → treść parsowana jeszcze raz (do głębokości 2) | fałszywa odmowa przy `grep` albo opisie commita to hook, który ktoś wyłączy. Ten sam podział co reguły `deny` w dokumentacji, plus formy, których one nie łapią |
| D6 | **Fail-closed i limit czasu** | owijacz jak przy strażniku (brak skryptu → `exit 2`), `timeout` 10 s, **`"onFailure": "block"` w obu wpisach** — także w istniejącym strażniku danych rodziny | **dziś strażnik danych rodziny przy przekroczeniu 30 s przepuszcza po cichu** — wbrew swojemu nagłówkowi „FAIL-CLOSED”. Klucz działa od 2.1.295; `claude` 2.1.238 w terminalu go nie zna |
| D7 | **Komendy „po go”** (`git init`, `git remote add/set-url`, ustawienia GitHuba przez `gh`) | hook odmawia **zawsze**; po „go” agent podaje dokładną komendę, a **autor wykonuje ją w terminalu VS Code** | rzadkie (raz na repo). Furtka, którą agent mógłby sam otworzyć (słowo w komendzie, zmienna), zjadłaby sens hooka |
| D8 | **`git fetch`** (pytanie z pozycji) | **odmowa** — także bez zapisu w gałęziach roboczych | zwykły `fetch` zapisuje `refs/remotes` (reguła: „`git fetch` z zapisem”); nikt w łańcuchu go nie potrzebuje — sygnałem jest odrzucony push |
| D9 | **`git revert`** | **odmowa** (lista dozwolonych) | to nowy commit spoza paczki. „Cofnięcie: `git revert <hash>`” w dzienniku łańcucha jest instrukcją dla autora albo dla agenta po „go” → wykonuje autor (D7) |

**Przed czym chronimy** (pytanie z retro 3, R7, zadane wprost): przed **nawykiem** agenta — komendą wpisaną z
przyzwyczajenia — a **nie** przed agentem, który chce regułę obejść. Hook to pas bezpieczeństwa, nie piaskownica
(dokumentacja: „isn't a security boundary”); granicą systemową byłby sandbox Claude Code — poza zakresem.

### Scope diff vs the item (to accept at stop #1)
- **lista dozwolonych zamiast zakazanych** (D3) — szerzej niż *What to build*: odmowę dostają też `clean`, `mv`,
  `cherry-pick`, `revert`, zapis `config` i `tag`, `update-index`;
- **dochodzi `"onFailure": "block"` w istniejącym strażniku danych rodziny** (D6) — luka znaleziona przy prior art, jedna
  linia w `settings.json`;
- doprecyzowanie: tekst w cudzysłowach, heredoc, `$(…)` w cudzysłowach i `bash -c` (D5);
- *Do decyzji na stopie #1* z pozycji → D2 (osobny skrypt), D8 (`fetch`).

### Steps (dev)
1. `grobing-agents/.claude/hooks/command-guard.ps1` (PowerShell 5.1, komunikaty ASCII jak w strażniku): stdin JSON →
   `tool_name` spoza `Bash`/`PowerShell` → `exit 0`; parser (D5) → dla każdego segmentu: git (D3, D8, D9), `gh`, Python
   (D4). Odmowa: `exit 2`, stderr — co, dlaczego (reguła), co zamiast. Każdy wyjątek → `exit 2`. Nagłówek *WHAT IT
   DOES / WHAT IT DOES NOT CATCH* (z *Czego NIE daje* tej pozycji i przecieków parsera).
2. `.claude/settings.json`: drugi wpis `PreToolUse` (matcher `Bash|PowerShell`, owijacz jak przy strażniku, `timeout`
   10) i `"onFailure": "block"` w obu wpisach (D6). Klasyfikator może zablokować zmianę własnych uprawnień — wtedy
   `dev` podaje autorowi dokładny tekst do wklejenia w edytorze.
3. `.claude/rules/git-autonomy-boundary.md` → *Forbidden autonomously*: akapit — `command-guard.ps1` (ISSUE-031) łapie
   te komendy przy próbie; czego nie łapie; komendy „po go” wykonuje autor (D7). (AC-5)
4. Pomiar kosztu wywołania (mediana z 3, jak ISSUE-006): sam skrypt na zwykłej komendzie i na komendzie złożonej.
5. Sprawdzenie na żywo w sesji (po przeładowaniu ustawień, jeśli harness ich nie podejmie od razu), **w tej
   kolejności**: najpierw `git -C <katalog tymczasowy, nie repo> reset` → odmowa (bez hooka git tylko odpowie „not a git
   repository” — bez skutku); dopiero po potwierdzonej odmowie `timeout 5 python -I - </dev/null` → odmowa (gdyby hook
   przepuścił, wejście jest puste, a `timeout` i tak przerwie — nic nie zawiśnie); `git status` → przechodzi;
   `grep -n 'git reset'` w regułach → przechodzi. Wynik w *Dev report*.

### Files likely touched
- `grobing-agents/.claude/hooks/command-guard.ps1` — `dev`;
- `grobing-agents/.claude/hooks/tests/command-guard.tests.ps1` — `qa`;
- `grobing-agents/.claude/settings.json`, `.claude/rules/git-autonomy-boundary.md` — `dev` (kroki 2–3);
- ta pozycja — `planning` (plan), `dev` (*Dev report*), `qa` (*Verification*); `CURRENT_STATE.md` — `docs`.

### AC → verification
| AC | Jak sprawdzone |
|---|---|
| 1 zakazane formy → odmowa | `qa`: tabela przypadków, osobny proces na przypadek, Bash i PowerShell — każda forma z D3/D4/D7–D9, także z `-C`, `-c`, ścieżką do `git.exe`, w `&&`/`;`/`\|`, w `$(…)`, w `bash -c "…"`, `git add <katalog>` (katalog tymczasowy) · `dev`: na żywo (krok 5) |
| 2 dozwolone formy → przechodzą | `qa`: każda forma z D3 (a)–(d); `echo`/`grep`/opis commita ze słowami zakazanych komend; heredoc z takim tekstem; komenda dzisiejszego commita `docs` (`git add -- <pliki>`, `git commit -q -F "<plik>"`, `git push origin main`) |
| 3 fail-closed | `qa`: zły JSON, pusty stdin, owijacz z `settings.json` bez skryptu → `exit 2`; `"onFailure": "block"` w obu wpisach — sprawdzenie pliku (zachowanie przy przekroczeniu czasu tylko według dokumentacji, nazwane wprost) |
| 4 strażnik danych rodziny zielony; koszt | `qa`: `family-data-guard.tests.ps1` bez regresji · `dev`: pomiar (krok 4) |
| 5 reguła mówi, co łapie | diff `git-autonomy-boundary.md` |

### Manual verification (stop #2)
- **Agent (przed stopem, bez emulatora):** testy obu hooków; krok 5 na żywo; pomiar. Zapis w *Verification* jako „kroki
  oddane agentowi” (pozycja bez ekranu — `DEFINITION_OF_DONE.md` → *Kto sprawdza*).
- **Autor: odczucie** — brak (pozycja bez ekranu). Jedyna możliwa rzecz dla autora: wkleić tekst do `settings.json`, jeśli
  klasyfikator zablokuje zmianę agentowi.

### Out of scope
- komendy złożone w locie (`eval`, nazwa komendy w zmiennej, alias), skrypt z pliku, który sam woła zakazaną komendę,
  `cmd /c …`, komendy autora z VS Code;
- reguły `permissions.deny` (D1) i sandbox Claude Code;
- zmiana pamięci agenta o `python -` — zostaje; hook ją uzupełnia.

## Dev report
> `dev`, 2026-10-13. Plan zatwierdzony na stopie #1 („tak”, 2026-10-13): lista dozwolonych, `onFailure` także w strażniku
> danych rodziny.

### Done
1. **`.claude/hooks/command-guard.ps1`** (PowerShell 5.1, komunikaty ASCII): parser komendy Bash i PowerShell (D5),
   lista dozwolonych gita (D3, D8, D9), `gh` zawsze odmowa, Python ze skryptem z wejścia i bez skryptu (D4). Każdy wyjątek
   → `exit 2`. Nagłówek *WHAT IT DOES / WHAT IT DOES NOT CATCH*. Odmowa podaje komendę (do 100 znaków), powód z regułą i
   co zrobić zamiast; najwyżej 3 odmowy w jednym komunikacie.
2. **`.claude/settings.json`**: drugi wpis `PreToolUse` (`Bash|PowerShell`, owijacz jak przy strażniku, `timeout` 10,
   `"onFailure": "block"`) i `"onFailure": "block"` w istniejącym wpisie strażnika danych rodziny (D6). Klasyfikator nie
   zablokował zmiany.
3. **`git-autonomy-boundary.md`** → *Forbidden autonomously*: akapit „Co to łapie” — mechanizm, granice, komendy „po go”
   wykonuje autor (AC-5).
4. **Pomiar** (osobny proces na wywołanie, mediana z 3): zwykła komenda **423 ms**; komenda złożona z pętlą i heredociem
   400 linii **543 ms**. Hooki biegną równolegle ze strażnikiem danych rodziny (dokumentacja), więc czas się nie sumuje.
5. **Na żywo w tej sesji** (harness podjął zmianę `settings.json` bez restartu — dokumentacja: „file watcher”), w
   kolejności z planu: `git -C <katalog tymczasowy> reset` → odmowa; `timeout 5 python -I - </dev/null` → odmowa (nic nie
   zawisło); `git status --short` i `grep -n 'git reset' …` (Bash) → przeszły; `git log` i `Select-String` (PowerShell)
   → przeszły.

**Test dymny `dev`** (poza repo, katalog tymczasowy sesji — testy w repo pisze `qa`): 72 przypadki, 0 rozjazdów — m.in.
`echo "git reset"`, `grep 'git reset'`, opis commita zaczynający się od „-a”, heredoc z tekstem „git reset” i „python -”,
here-string PowerShella → przechodzą; `cd x && git -C y reset`, `/usr/bin/git stash`, `git.exe checkout`, `echo
"$(git reset)"`, `` echo `git clean -fd` ``, `bash -c 'git fetch'`, `powershell -Command "git reset"`, `& '…\git.exe'
stash`, `if (…) { git checkout }`, `ForEach-Object { git rm }`, `git commit --amen` (skrót opcji), `git add -- <katalog>`
→ odmowa. Zły JSON, pusty stdin, brak `tool_input.command` → `exit 2`.

### Deviations
- **Głębokość parsowania 3, nie 2** (D5): `bash -c "…"` z `$(…)` w środku to już głębokość 2; przy 3 łapie jeszcze jedno
  zagnieżdżenie. Koszt pomijalny.
- **`-EncodedCommand` PowerShella dekodowany** (base64) i parsowany — poza planem, kilka linii; zamyka oczywistą furtkę.
- **`cd <katalog>` wcześniej w tej samej komendzie** przesuwa bazę dla sprawdzenia „`git add` katalogu” (D3 mówi tylko o
  `-C` i `cwd`) — bez tego `cd repo && git add sub` sprawdzałby katalog w złym miejscu.
- **Jedna linia w `family-data-guard.ps1`**: podpowiedź w odmowie „`git restore --staged` … agent najpierw pyta autora” →
  „wykonuje ją autor w terminalu VS Code (command-guard, ISSUE-031)” — po tej pozycji agent tej komendy nie wykona nawet
  po zgodzie. Testy strażnika tego tekstu nie sprawdzają.

### Found
- **`onFailure` według dokumentacji** ([hooks → *Block the action when a hook fails*](https://code.claude.com/docs/en/hooks)):
  pole obiektu hooka (obok `type`, `command`), wartości `continue` (domyślna) i `block`; blokuje przy hooku, który się nie
  uruchomi, przekroczy `timeout`, wyjdzie kodem innym niż 0 i 2 albo zwróci niepoprawny JSON. Zachowanie starszej wersji
  (`claude` 2.1.238 w terminalu) wobec nieznanego klucza — nieopisane.
- **Zmiany hooków w `settings.json`** podejmuje obserwator plików bez restartu sesji (dokumentacja + sprawdzone wyżej).

### For `qa`
- `grobing-agents/.claude/hooks/tests/command-guard.tests.ps1` — wzorem `family-data-guard.tests.ps1` (osobny proces na
  przypadek, JSON jak z harnessu): tabela AC-1 i AC-2 dla Bash i PowerShell (przypadki wyżej + każda pozycja listy
  dozwolonych z D3 i każda zakazana forma z D3/D4/D7–D9), `git add` z katalogiem w katalogu tymczasowym (także po `cd` i z
  `-C`), fail-closed (AC-3) i **owijacz z `settings.json`** (brak skryptu → `exit 2`), `onFailure: block` w obu wpisach
  (odczyt pliku); `family-data-guard.tests.ps1` bez regresji (AC-4).
- Kroki autora: brak (pozycja bez ekranu). Sprawdzenie na żywo zrobione wyżej — `qa` może je powtórzyć.

## Verification
> `qa`, 2026-10-13. Werdykt: **APPROVED** (self-check, z uwagami). Pozycja bez ekranu i bez warstwy danych aplikacji: przegląd
> `ui`, test migracji i próbne odtworzenie nie dotyczą; stop #2 — **kroki oddane agentowi** (`DEFINITION_OF_DONE.md` → *Kto
> sprawdza*).

| AC | Dowód | Wynik |
|---|---|---|
| 1 zakazane formy → odmowa | `.claude/hooks/tests/command-guard.tests.ps1`, osobny proces na przypadek: git spoza listy (32), `git add` bez jawnej listy — także katalog przez `cwd`, `-C` (Bash i Windows) i po `cd` (29), `commit`/`push`/`branch`/`tag`/`config` (41), ten sam czasownik w innych kształtach — `-C`, `-c`, `/usr/bin/git`, `git.exe`, ścieżka w cudzysłowie, `\git`, `'git'`, `&&`/`;`/`\|\|`/`\|`/nowa linia, `( )`, `{ }`, `$( )` także w cudzysłowie, odwrócony apostrof, `<( )`, `bash -c` (też dwa poziomy), `sh -lc`, `powershell -Command`, `pwsh -c`, słowa kluczowe, nakładki `time`/`timeout -s`/`nice -n`/`env`/`sudo`/`xargs -n` (55), PowerShell — w tym `& '…\git.exe'`, `{ }`, `$( )`, `@( )`, `-EncodedCommand` (19), `gh` (4), Python ze skryptem z wejścia albo bez skryptu — `python3.12`, `py -3`, `-X`/`-W` z wartością, `--`, heredoc, `winpty`, potok (29) | ✅ |
| 2 dozwolone formy → przechodzą | odczyt gita (58), `add`/`commit`/`push` w kształcie paczki `docs` — także komendy z dzisiejszego commita retro 3 i suchy przebieg `echo dry-run: git add -- …` (24), zakazane słowa jako **tekst** — `echo`, `grep`, `printf`, komentarze, heredoc (`<<'EOF'`, `<<EOF`, `<<-EOF` z tabulatorami), opis commita, `$(git status)`, `bash -c 'git status'`, Python ze skryptem, `-c`, `-m`, `--version`, `py --list`, `gitk`, `gh-pages-helper` (57), PowerShell — here-stringi, komentarze `#` i `<# #>`, `2>$null` (18) | ✅ |
| 3 fail-closed | zły JSON, pusty stdin, brak `tool_input.command`, heredoc bez znacznika → `exit 2`; brak `cwd` → dalej odmawia; owijacz z `settings.json` (`-EncodedCommand`, jak harness): skrypt jest → odmowa / przejście; brak skryptu → `exit 2` „BRAK SKRYPTU”; skrypt z błędem składni, bez `exit`, z wyjątkiem → `exit 2`; `settings.json` bez ścieżki absolutnej; **`"onFailure": "block"` w obu wpisach** (odczyt pliku) | ✅ |
| 4 strażnik danych rodziny zielony; koszt | `family-data-guard.tests.ps1`: **150/150** (80 s) — ten sam wynik co przy ISSUE-020; test strażnika bierze pierwszy wpis `PreToolUse`, a nowy wpis jest drugi. Koszt (pomiar `dev`): 423 ms zwykła komenda, 543 ms komenda złożona z heredociem 400 linii; hooki równolegle | ✅ |
| 5 reguła mówi, co łapie | `git-autonomy-boundary.md` → *Forbidden autonomously* → „Co to łapie — hook `command-guard.ps1`”: lista dozwolonych, kształty, granice, „po go” wykonuje autor | ✅ |

**Testy:** `command-guard.tests.ps1` **369/369** (200 s) — w tym komunikaty (komenda, reguła, kto wykonuje; skrót długiej
komendy; „i jeszcze N”) i **znane luki jako przypadki, które dziś przechodzą** (`eval`, `"$GIT"`, `bash script.sh`, `cmd /c`,
pętla w `git add`) — zmiana zachowania wyjdzie w teście. Pierwszy przebieg: 366/369 — trzy porażki w samym teście (odwrócony
apostrof jest znakiem ucieczki we wzorcach `-like`), poprawione na `.Contains`.

**Na żywo w tej sesji:** `dev` — Bash: `git -C <katalog tymczasowy> reset` → odmowa, `timeout 5 python -I - </dev/null` →
odmowa, `git status` i `grep 'git reset'` → przechodzą; PowerShell: `git log`, `Select-String` → przechodzą. `qa` — PowerShell:
`git -C <katalog tymczasowy> stash` → odmowa z pełnym komunikatem.

**Dane rodziny:** w zmianach brak plików z listy typów i brak nazwisk — przykłady w testach to ścieżki i słowa techniczne;
suchy przebieg strażnika treści na plikach paczki `grobing-agents` przeszedł.

**Uwagi (nie blokują):**
- `onFailure: block` przy przekroczeniu czasu — tylko według dokumentacji; harnessu nie da się tu zmusić do przekroczenia
  `timeout` bez spowalniania sesji;
- `claude` 2.1.238 w terminalu nie zna `onFailure` — w sesji z terminala zachowanie nieopisane (sesje autora idą przez
  rozszerzenie 2.1.296);
- skrypt nie przeszedł analizy statycznej PowerShella (PSScriptAnalyzer nie jest zainstalowany) — pokrycie dają testy;
- świadome luki z nagłówka skryptu (komenda złożona w locie, skrypt z pliku, `cmd /c`, pętla w `git add`) — test pilnuje, że są
  takie, jak opisane.

**Nieprzetestowane na żywo** (dla listy w [[ISSUE-032-mvp-install]] — tu nic: pozycja procesu, nie aplikacji):
- brak.

### Package for `docs`
- `grobing-agents`: `.claude/hooks/command-guard.ps1` (nowy) · `.claude/hooks/tests/command-guard.tests.ps1` (nowy) ·
  `.claude/hooks/family-data-guard.ps1` (jedna linia komunikatu) · `.claude/settings.json` · `.claude/rules/git-autonomy-boundary.md`;
- `grobing-vault`: `backlog/issues/ISSUE-031-command-guard.md` (plan, *Dev report*, *Verification*; zamknięcie — `docs`) ·
  `00_START_HERE/CURRENT_STATE.md` (zamknięcie — `docs`).
