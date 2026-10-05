---
title: "ADR-002 — Flutter, with the SDK version pinned per project"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §Architecture → Stack · Reuse of the author's existing tooling"
created: 2026-10-05
updated: 2026-10-05
---

# ADR-002 — Flutter z przypiętą wersją

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-05 (decyzja autora w kick-offie; rekomendacją był Flutter).

## Context
- Typ A: aplikacja na Androida z bazą; autor pracuje sam i jest doświadczony.
- **Dowód zmierzony, nie zadeklarowany:** autor wydał aplikację we Flutterze w Google Play.
- iPhone: Won't (now), W5 — z warunkiem powrotu; ten sam kod ułatwiłby powrót.
- **SDK jest współdzielone z wydaną aplikacją autora** (zainstalowane: Flutter 3.41.1 stable, Dart
  3.11.0): aktualizacja Fluttera dla Grobing aktualizuje go też tam i może zepsuć jej build.
- Prawdziwym ograniczeniem nie jest framework, tylko źródło map ([[ADR-003-map-source-offline]]).

## Decision
**Flutter, na wersji przypiętej per projekt** — wartość żyje wyłącznie w
`grobing-agents/.claude/rules/project-config.example.md` → `flutter_version_pinned` (w dniu decyzji:
wersja zainstalowana, patrz *Context*). **Globalny Flutter nie jest aktualizowany bez decyzji.** Start od świeżego `flutter create` (nie kopia folderu innej aplikacji); bez Firebase; relacyjny
SQLite, nie magazyn klucz-wartość; własny klucz podpisu poza każdym drzewem projektu.

## Options considered

| Option | Pros | Cons | Why (not) chosen |
|---|---|---|---|
| **Flutter, wersja przypięta per projekt, globalny SDK nietykany** | dowód autora (wydana aplikacja); jeden kod pod iPhone'a później; wtyczki z regionami offline | wymaga mechanizmu przypięcia; uwaga na licencje wtyczek map (popularna wtyczka bulk-download do `flutter_map` jest GPL) | **chosen** |
| Kotlin + Jetpack Compose | kanon Androida wprost (Room + WorkManager) | brak dowodu u autora; druga platforma = druga aplikacja | rejected |
| Flutter na współdzielonym globalnym SDK, bez przypięcia | zero konfiguracji | aktualizacja dla Grobing aktualizuje wydaną aplikację — może zepsuć jej build | rejected — ryzyko dla żywej aplikacji |

## Consequences
- **Positive:** reuse stosu i rytuału zamknięcia (WZ-024) z wcześniejszej aplikacji; ścieżka do
  iPhone'a otwarta bez przepisywania.
- **Negative / trade-offs:** zależność od wtyczek Fluttera dla map offline i bezpiecznego magazynu;
  przypięta wersja wymaga świadomych aktualizacji.
- **Reuse — co tak, co nie** (brief): SDK Androida, edytor, obrazy emulatora — tak, wspólne z założenia ·
  `analysis_options.yaml` / `flutter_lints`, rytuał zamknięcia, sekcja „Project Identity" — jako wzorce,
  nie pliki · Firebase, klucz podpisu innej aplikacji, Hive, kopia folderu innej aplikacji — **nie**.
- **Follow-ups:**
  - ⚠️ **OPEN — mechanizm przypięcia** (menedżer wersji albo zapisana wersja + sprawdzenie) →
    [[ISSUE-002-bootstrap-code-repo]] wybiera jeden, opisuje w README `grobing-code` i **dopisuje tu
    datowaną linię**.
  - ⚠️ **OPEN — nazwa pakietu Androida** → ISSUE-002, wpis wyłącznie w `project-config.example.md`.
