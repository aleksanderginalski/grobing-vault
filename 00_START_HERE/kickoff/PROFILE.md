---
title: "Grobing — Person Profile"
type: profile
status: approved
created: 2026-10-05
updated: 2026-10-05
---

# Grobing — Person Profile

> Zatwierdzony profil z fazy 0 kick-offu (2026-10-05). Agenci czytają go, żeby dobrać język,
> granulację, głębokość procesu i zasady gita. **Profil generuje rekomendacje, nigdy nie
> rozstrzyga** — każdy wybór należał do autora.
>
> **Ten plik jest domem profilu od materializacji.** `PROJECT_BRIEF.md` §Profile wskazuje tutaj
> i nie powtarza treści (jeden dom naraz, przekazany — nie dwie żywe kopie).
>
> Oznaczenia: *zmierzone* = widoczne na dysku · *zadeklarowane* = powiedziane przez autora ·
> *założone* = wniosek agenta, przedstawiony jako założenie i niepoprawiony na checkpoincie.

## Axis A — Technical level + command literacy
- Technical level: **doświadczony** (*zmierzone*: wydana na Google Play aplikacja Flutter, wiele
  przestrzeni z własnymi skryptami i matrycami własności).
- Command literacy: **zwięzłe komendy wystarczą**, bez tłumaczenia krok po kroku.
- Style: komendy i konkret; uzasadnienie tylko tam, gdzie zmienia decyzję.

## Axis B — Solo vs team + git rules
- Setup: **solo** (*założone*).
- Others run their own agents: **nie** (*założone*).
- Version rules needed: tylko `git-autonomy-boundary` — bez ceremonii branchy.

## Axis C — Working style with agents
- Issues per session: elastycznie; każda sesja coś **domyka**.
- Mindset: inżynierski (lista zadań), nie scrum-masterski.
- Slice size: **cienki plaster** (*zadeklarowane*). Rytuał zamknięcia sesji z ręczną weryfikacją po
  polsku przed commitem (*zmierzone*, wzorzec WZ-024 z wcześniejszej aplikacji autora).

## Axis D — Product goal + process appetite
- Goal: **prawdziwy, osobisty produkt na lata** (*założone*).
- Process: **ciężki / rygorystyczny** (*zadeklarowane* 2026-10-05; luźny jest wyłącznie termin, nie
  proces).
- Grant/tender: nie.

## Derived calibration (how this profile shaped the setup)
Solo · doświadczony · cienki plaster · rygor. Napięcie „cienki plaster vs rygor" rozstrzygnięto w
Meta-decyzji 2 tak, że **rygor siedzi w warstwach artefaktów** (FR, NFR, AC, ścieżka, macierz
powiązań, krytyk), a **cienkość w rozmiarze zadania** (COMPONENT + task-level). Doświadczenie →
auto-flow z trzema punktami stopu, numerowane foldery, zwięzła komunikacja agentów.
