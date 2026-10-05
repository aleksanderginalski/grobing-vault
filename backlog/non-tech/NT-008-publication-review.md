---
title: "NT-008 — Publication review before the first public push"
type: non-code-item
status: open
category: legal
priority: MUST
source: "materialization 4.6 — the author chose PUBLIC GitHub repos as a portfolio (2026-10-05)"
wake-condition: "before the first push of ANY Grobing repo to a public remote"
created: 2026-10-05
updated: 2026-10-05
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
- Otwarte: **wybór dla vaulta** · przed samym pushem przegląd `git log -p` (granica wyżej).

## Resolution (fill when done — this is the DoD)
[ISSUE-006 zamknięte · przegląd 2 i 3 zrobiony (co zmieniono — bez cytowania danych) · wybór dla vaulta ·
data] → dopiero wtedy budzi się [[DEF-005-push-gate]].
