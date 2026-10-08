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
  - ✅ **2026-10-05 — mechanizm przypięcia** ([[ISSUE-002-bootstrap-code-repo]]): zapisana wersja +
    sprawdzenie. Wersję deklaruje `project-config.example.md`, a sprawdza ją
    `grobing-code/pubspec.yaml` → `environment.flutter: 3.41.1`. **Zmierzone:** `pub get` odmawia
    każdej innej wersji, łącznie z górną granicą zakresu. FVM odłożony do pierwszego konfliktu wersji z
    drugą aplikacją. Opis jest w README `grobing-code`. Zmiana wersji to obie linie w jednej paczce plus
    nowa linia tutaj.
  - ✅ **2026-10-05 — nazwa pakietu: `com.grobing.app`** (decyzja autora, ISSUE-002; wzorzec jego
    wcześniejszej aplikacji). Wartość jest wpisana wyłącznie w `project-config.example.md`.
    **Nieodwracalna:** inna nazwa albo inny klucz podpisu to dla Androida inna aplikacja, która nie widzi
    bazy z telefonu. Klucz wydania leży poza drzewem projektu (`release_keystore_dir` w lokalnym
    `project-config.md`).
  - **2026-10-05 — przypięcie ogranicza paczki** ([[ISSUE-007-data-layer]], [[ADR-005-sqlite-package]]).
    Przypięty SDK trzyma `analyzer` na 10.x, więc `drift` i `drift_dev` są przypięte parą na 2.34.0, a
    `sqlite3` stoi na 3.5.x. **Zmiana wersji Fluttera rusza też tę parę**, potem `drift_dev schema dump`
    i pełne testy. Wcześniej to samo ograniczenie odrzuciło `dartage` ([[SPIKE-003-backup-and-restore]]).
  - **2026-10-08 — `flutter_localizations` wiąże `intl` z SDK** ([[ISSUE-021-small-fixes-after-retro-2]]). Polskie
    teksty widżetów Fluttera biorą pakiet z SDK, który wymaga dokładnie `intl` 0.20.2, więc `intl` (wcześniej tylko
    przez `latlong2`) cofnął się z 0.20.3 — decyzja autora; Grobing sam `intl` nie używa. **Zmiana wersji Fluttera
    rusza też `intl`.**
