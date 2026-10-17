---
title: "ADR-021 — Family wreaths: a clans table and the choice at the person, the wreath worked out from the tree"
type: adr
status: accepted
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-044-family-wreaths]]"
source: "plan `planning` na stopie #1 ISSUE-044 (M1; autor: „tak”, 2026-10-17) · decyzje autora z discovery ([[wieniec]] D7, D9, D14, D15) i ze stopu #2 (D20) · droga obrazów R (stop #1) · [[ADR-018-export-is-the-backup]]"
created: 2026-10-17
updated: 2026-10-17
---

# ADR-021 — Wieńce rodów: tabela rodów i wybór przy osobie, wieniec liczony z drzewa

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-17: model M1 na stopie #1 [[ISSUE-044-family-wreaths]] („tak”), razem z drogą obrazów R; para wzór + kolor — decyzja autora na
stopie #2 ([[wieniec]] D20).

## Context
Autor chce przy portrecie **wieniec rodu**, z którego osoba się wywodzi, a domyślnie **dzieci przejmują go po ojcu** (`/pm` 2026-10-16). Po discovery
([[wieniec]] D7, D9, D14): cały wieniec po ojcu (linia ojca, nie matki), ród wybiera się raz u szczytu linii, a kobieta po ślubie ma pół wieńca rodu
własnego i pół rodu męża. Wieniec ma się zmieniać sam, gdy zmienia się drzewo (nowe dziecko, poprawiony ojciec), jak ścieżka „Jak łączy się ze mną”,
która też jest liczona, a nie zapisywana ([[data-model]] → *Rules that are not tables*). Kopia jest eksportem dla rodziny
([[ADR-018-export-is-the-backup]]), więc rody muszą się czytać z samej bazy.

## Decision
1. **Nowa tabela `clans`** (schemat v15): nazwa · **klucz wzoru** (jeden z 19 obrazów, np. `klosy`) · **klucz koloru** (jeden z 12 kolorów palety, np.
   `rubin`). Klucze, nie wartości: obraz i kolor mają dom w aplikacji (`assets/wreaths/`, `theme.dart`), a nieznany klucz z kopii nowszej aplikacji
   daje „bez wieńca” albo pierwszy kolor, nie błąd. **Nazwa unikalna bez wielkości liter i polskich znaków** — sprawdza kod (`fold`), bo `NOCASE`
   SQLite nie zna polskich liter.
2. **Przy osobie zapisany jest tylko wybór:** `persons.clan_id` (ród wybrany przy tej osobie, opcjonalny) i `persons.no_wreath` (wybrane „bez
   wieńca”). Nic nie wybrane = wieniec przychodzi po ojcu. Migracja v14→v15: `createTable` + dwa `addColumn`, bez zmiany wierszy.
3. **Wieniec każdej osoby liczy się przy odczycie** z drzewa i wyborów (`WreathGraph`, reguły [[wieniec]] B1–B7): ojciec = rodzic z płcią „mężczyzna”
   w pierwszej rodzinie, w której osoba jest dzieckiem; ród własny = wybór przy osobie, inaczej ród własny ojca; **kobieta po ślubie** — lewa połowa
   to ród własny, prawa to ród męża z **ostatniego małżeństwa** („razem” się nie liczy); brakująca połowa wypełnia całość; dzieci dziedziczą ród
   własny ojca; koniec związku i suwak czasu wieńca nie zmieniają; pętla w drzewie daje „bez wieńca” i nie zawiesza liczenia.
4. **Ród odróżnia para wzór + kolor** ([[wieniec]] D20): ostrzeżenie „też: …” przy wyborze wzoru tylko dla tej samej pary; tej samej pary baza nie
   blokuje.
5. **Obrazy wzorów w repo kodu** (droga R): 19 plików `assets/wreaths/wieniec-<klucz>.png`, szare z przezroczystością, 640 × 640 — wąski wyjątek w
   `.gitignore` i w strażniku danych rodziny, który sprawdza nagłówek każdego pliku (`grobing-agents/.claude/rules/family-data.md` → *Mechanisms*). Kolor i obwódkę dokłada
   aplikacja raz na parę wzór–kolor i rozmiar.

## Options considered
| Opcja | Za | Przeciw | Wynik |
|---|---|---|---|
| **M1 — `clans` + wybór przy osobie, wieniec liczony** | jeden zapis u szczytu linii; wieniec nadąża za drzewem bez migracji danych; kopia niesie tabelę sama | liczenie przy każdym odczycie drzewa (czysta funkcja, pamięć na osobę) | **wybrane** |
| M2 — ród przy rodzinie (`families`) | jeden zapis na związek | rodzina to związek, a wieniec dziedziczy się po osobie (ojcu); przy pół na pół jedna rodzina miałaby dwa rody | odrzucone |
| M3 — ród z nazwiska, bez zapisu | zero wpisywania | nazwisko zmienia się po ślubie, ma literówki, jedno nazwisko może mieć dwa rody | odrzucone |
| M4 — wieniec zapisany przy każdej osobie | odczyt bez liczenia | zmiana u szczytu linii to dziesiątki zapisów; po zmianie drzewa wieniec rozjeżdża się z rodziną | odrzucone |
| Obrazy poza repo (P) albo przerysowane na SVG (S) zamiast pkt 5 | ochrona danych rodziny bez wyjątku | P: build tylko z plikami autora; S: nowa biblioteka, cieniowanie w aplikacji, ok. 1–2 dni więcej przed instalacją | odrzucone (decyzja autora na stopie #1) |

## Consequences
- **Kopia v14** odtwarza się w v15 bez rodów — nikt nie ma wieńca, dopóki autor nie wybierze rodu u szczytu linii (test odtworzenia,
  `restore_service_test`).
- **Usuwania rodu nie ma** ([[wieniec]] D16) — ród bez osób zostaje w tabeli i w arkuszu wyboru.
- **Wzór spoza listy** (np. mak, D12) może dojść aktualizacją aplikacji: nowy obraz i klucz, bez zmiany schematu.
- **Mapa pól GEDCOM na później** (eksport GEDCOM poza MVP): GEDCOM 7 nie ma rodu z wieńcem; nazwa rodu najbliżej `NOTE` przy osobie u szczytu linii
  albo rozszerzenie `_CLAN` — decyzja przy eksporcie, nie teraz.
- Strażnik danych rodziny nie odróżni szarego zdjęcia z przezroczystością przyciętego do 640 × 640 i nazwanego jak wzór (`family-data.md` → *Czego NIE
  łapie*).

## Follow-ups
