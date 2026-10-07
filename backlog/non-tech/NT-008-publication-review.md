---
title: "NT-008 — Publication review before the first public push"
type: non-code-item
status: done
category: legal
priority: MUST
source: "materialization 4.6 — the author chose PUBLIC GitHub repos as a portfolio (2026-10-05)"
wake-condition: "before the first push of ANY Grobing repo to a public remote"
created: 2026-10-05
updated: 2026-10-07
---

# NT-008 — Przegląd przed pierwszym publicznym pushem

## The question / task
Autor chce trzech **publicznych** repo na GitHubie jako portfolio: kod i proces widoczne dla innych,
**dane rodziny wyłącznie jego**. Architektura już to zapewnia (dane żyją tylko w telefonie, w
zaszyfrowanej kopii i w eksporcie u rodziny). Ta pozycja zamyka trzy rzeczy, które architektura sama
nie załatwia — **przed pierwszym pushem, bo push do publicznego repo jest nieodwracalny** (historia
gita i indeksy wyszukiwarek zostają).

1. **Twarda blokada plików z danymi rodziny działa** — [[ISSUE-006-setup-family-data-guard]] zamknięte.
   ✅ 2026-10-05 (wcześniej chroniły tylko reguła i `.gitignore`).
2. **Zapis kick-offu nie mówi więcej o rodzinie, niż autor chce pokazać publicznie.** Przejrzyj
   `00_START_HERE/kickoff/PROJECT_BRIEF.md` i `SESSION_STATE.md`: cytaty o babci (w tym o tym, ile
   może jeszcze żyć), struktura rodziny, objętość notatek. Zostaw, przeredaguj albo przenieś — decyzja
   autora.
3. **Zapis kick-offu nie przenosi opisów innych przestrzeni autora z jego prywatnego rejestru**
   (zasada NPG: *rejestr wskazuje, nie cytuje poza tą maszyną*). Do sprawdzenia: brief §3a (opis innej
   aplikacji autora i jej historii), §Architecture → *Reuse of the author's existing tooling* (uwaga o
   lokalizacji klucza podpisywania innej, wydanej aplikacji — **ta jedna linia nie powinna trafić do
   publicznego repo w żadnej formie**), `PROFILE.md` (linie oznaczone *zmierzone*).

## Options for the vault (autor wybiera przy tej pozycji)
- **Wszystkie trzy publiczne** po przeglądzie 1-3 — portfolio pokazuje kod, agentów i proces decyzyjny.
- **`grobing-code` + `grobing-agents` publiczne, `grobing-vault` prywatne** — proces zostaje u autora.

## Why it matters
Prywatne repo wybacza pomyłkę; publiczne — nie. Klucz map (jeśli dostawca go wymaga) w publicznej
aplikacji musi być ograniczony do pakietu i certyfikatu podpisu (§Security).

## Progress
- **2026-10-05 — punkty 2 i 3 zrobione, przed pierwszym commitem** (decyzje autora): §2 briefu —
  okno czasowe źródła przeredagowane bez szacunku · §3a — odwołanie do prywatnego rejestru i
  niezwiązana przestrzeń usunięte · §Architecture → *Reuse* — szczegół konfiguracji podpisu innej
  aplikacji usunięty, razem z tym samym faktem w innej formie (brief + ISSUE-002, *Technical Notes*) ·
  reszta (babcia jako źródło, przykłady relacji, objętość, `PROFILE.md`) — zostaje. Ślad w nagłówku
  briefu. **Historia gita czysta**, bo przegląd poprzedził pierwszy commit.
- ⚠️ **Granica tego przeglądu:** obejmuje stan plików, nie historię. Treść tego typu dopisana **po**
  pierwszym commicie zostaje w historii nawet po usunięciu — przed pierwszym pushem przejrzyj też
  `git log -p`, nie tylko bieżące pliki.
- **2026-10-05 — punkt 1 zrobiony:** [[ISSUE-006-setup-family-data-guard]] zamknięte. Hook `PreToolUse`
  w `grobing-agents` odmawia zapisu i `git add`/`commit` baz, kopii `age`/`tar`, eksportów HTML/PDF,
  zdjęć i filmów; ten sam blok jest w `.gitignore` trzech repo. Granice (treść, commit autora z VS Code)
  są w `family-data.md`.
- **2026-10-07 — przegląd historii zrobiony** (`/pm`, za zgodą autora w sesji). Agent przeczytał
  `family_data_dir` (33 zdjęcia notatek i listę cmentarzy) i przeszukał tym `git log --all -p` trzech repo,
  razem z opisami commitów: 41 commitów (`grobing-agents` 9, `grobing-vault` 23, `grobing-code` 9). Imiona,
  nazwiska i miejsca zostały w odpowiedzi agenta; **tutaj tylko liczby**:

  | Czego szukano | Trafienia | Ocena |
  |---|---|---|
  | nazwiska z notatek, z wariantami odmiany i pisowni | 0 | — |
  | miejsca z notatek i z listy cmentarzy | 9 | wszystkie w publicznych danych mapy Polski (Natural Earth) i jej testach — nie dane rodziny |
  | imiona z notatek | 17 | 16: wymyślone osoby (`Wymyślony`, `Próbna`, `Testowy`, `Nowak`/`Kowalska`) albo zwykłe słowa; 1 linia (prompt R3 w `05_DESIGN/brand/references.md`, ścieżka relacji) sprawdzona z autorem — **wymyślona, zostaje** |
  | fakty z notatek bez imion (lata, zawody, miejsca pracy, wydarzenia) | 0 | — |
  | adresy, kody pocztowe, numery PESEL, współrzędne | 0 | — |
  | numery kwater | kilka | tylko wymyślony przykład ze specyfikacji |
  | sekrety | 3 klucze `age` | publiczne wektory testowe C2SP i przykład ze specyfikacji `age` |
  | klucz podpisu innej aplikacji autora (pkt 3) | 0 | redakcja z 2026-10-05 trzyma |
  | prawdziwa miejscowość w promptach z kick-offu | 0 | od pierwszego commita w historii jest tylko `[miejscowość]` |
  | pliki z danymi (bazy, kopie, zdjęcia, keystore, `key.properties`, folder notatek) | 0 | w historii są tylko ikony aplikacji w `res/` |

  Drobiazg bez zmiany: [[ISSUE-002-bootstrap-code-repo]] → D3 podaje katalog klucza wydania Grobing na PC
  autora — bez klucza i haseł, więc nie sekret.

  **Granica przeglądu:** nazwiska trudne do odczytania z pisma sprawdzone w kilku wariantach; zdrobnień
  spoza notatek nic nie łapie; przegląd obejmuje historię do 2026-10-07, nie kolejne pushe (temat do retro
  w `CURRENT_STATE.md`).
- **2026-10-07 — wybór dla vaulta (autor):** **wszystkie trzy repo publiczne.**

## Resolution (fill when done — this is the DoD)
- [[ISSUE-006-setup-family-data-guard]] zamknięte — 2026-10-05.
- Przegląd 2 i 3 (zapis kick-offu) — 2026-10-05, przed pierwszym commitem: okno czasowe źródła bez
  szacunku, odwołanie do prywatnego rejestru i niezwiązana przestrzeń usunięte, szczegół podpisu innej
  aplikacji usunięty (w dwóch miejscach).
- Przegląd historii `git log -p` — 2026-10-07: zero danych rodziny w historii trzech repo (tabela wyżej).
- Wybór dla vaulta — 2026-10-07: wszystkie trzy repo publiczne.

**Zamknięte 2026-10-07.** Warunek pierwszego pushu z `family-data.md` jest spełniony. Push dalej tylko po
„go” (stop #3). Przy pierwszym pushu budzi się [[DEF-005-push-gate]].
