---
title: "ISSUE-002 — Bootstrap grobing-code (fresh Flutter project, pinned SDK, no Firebase)"
type: issue
status: ready
delivery-style: task-level
priority: MUST
ideal_days: 0.5
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
created: 2026-10-05
updated: 2026-10-05
---

# ISSUE-002 — Bootstrap grobing-code

## Scope
Świeży projekt Flutter w `grobing-code` na przypiętej wersji SDK, uruchamiający się na emulatorze i
telefonie autora jako pusty ekran startowy w stylu B — fundament pod wszystkie kolejne zadania.

## Acceptance Criteria
- [ ] `flutter create` w `grobing-code` (platforma: **android**), na wersji z
      `project-config.example.md` (`flutter_version_pinned`). **Globalny Flutter nie jest
      aktualizowany** — współdzieli go wydana aplikacja autora.
- [ ] Wersja przypięta per projekt (menedżer wersji albo zapis + sprawdzenie) — jeden sposób, opisany
      w README repo.
- [ ] Nazwa pakietu ustalona z autorem i wpisana **wyłącznie** w `project-config.example.md`
      (`android_package`).
- [ ] Domyślny `.gitignore` Fluttera **dołączony pod** istniejący blok (dane rodziny + sekrety
      zostają na górze).
- [ ] **Brak Firebase** i jakichkolwiek SDK wysyłających dane z telefonu.
- [ ] Lints/`analysis_options.yaml` jak we wcześniejszej aplikacji autora (wzorzec, nie kopia pliku).
- [ ] Własny keystore wydania **poza drzewem projektu**, ścieżka w lokalnym `project-config.md`
      (`release_keystore_dir`); w repo nic.
- [ ] `flutter analyze` i `flutter test` przechodzą; aplikacja startuje na telefonie z ciemnym ekranem
      startowym (styl B).

## Out of Scope
- Model danych, ekrany, mapy — kolejne zadania i spike'i.
- Wybór dostawcy map (SPIKE-001), mechanizmu kopii (SPIKE-003).

## Technical Notes
- **Nie kopiuj folderu innej aplikacji jako szablonu** — przeniósłby jej konfigurację; start od świeżego
  `flutter create`.
- Decyzja o sposobie przypięcia wersji → wpis do ADR-002 (ISSUE-001 AC-4).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| ADR-002 (Flutter, pinned) | technical | decyzja zapadła w kick-offie; plik powstaje w ISSUE-001 |

## Definition of Done
- [ ] DoD ISSUE (MVP) z `00_START_HERE/DEFINITION_OF_DONE.md`
- [ ] Ręczna weryfikacja w telefonie: aplikacja się instaluje i startuje
- [ ] **INVEST self-check**
