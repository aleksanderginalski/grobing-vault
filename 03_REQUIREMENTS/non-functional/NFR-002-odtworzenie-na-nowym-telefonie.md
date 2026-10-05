---
title: "NFR-002 — A restore onto a new phone recovers everything"
type: non-functional-requirement
status: draft
epic: ["[[EPIC-001-zabezpiecz-i-przepisz]]"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §5 M8 · §5a G1 · MD2 (NFR example) · §Security (backup vs export)"
created: 2026-10-05
updated: 2026-10-05
---

# NFR-002 — Odtworzenie na nowym telefonie

## Requirement
Z kopii poza telefonem da się **odtworzyć wszystko** na nowym telefonie: osoby, rodziny, zdarzenia,
cmentarze, groby, pochówki, twierdzenia ze źródłami i zdjęcia. Kopia, której nikt nie odtworzył, nie jest
kopią (G1).

| | |
|---|---|
| **Metric** | kompletność danych po odtworzeniu na drugim urządzeniu względem źródła |
| **Target** | **wszystko** — brief: *„a restore onto a new phone recovers everything"* |
| **Method** | próbne odtworzenie z kopii na **drugim emulatorze `Grobing_Restore`** (stałe urządzenie do odtworzeń, z kontem Google autora; od [[SPIKE-003-backup-and-restore]]), na **wymyślonych** danych (DoD ISSUE). Plik kopii walidowany **przed** nadpisaniem czegokolwiek (§Security floor). Zgodność mierzona **odciskiem danych** (SHA-256 treści tabel i zdjęć) przed kopią i po odtworzeniu, czyli jedną liczbą zamiast porównywania rekordów |
| **Verification trigger** | każda pozycja dotykająca warstwy danych (DoD) · pytanie o fakty co 10 zamkniętych pozycji: *„czy ostatnie odtworzenie naprawdę zadziałało?"* |

## Notes
- Kopia ≠ eksport (`glossary.md`): kopia jest pełna, zaszyfrowana, do odtworzenia; eksport jest czytelny
  bez aplikacji, dla rodziny. To NFR dotyczy kopii.
- **Sama kopia Androida się nie liczy** — limit 25 MB na aplikację czyni ją cicho niepełną ze zdjęciami
  (§Security) → [[ADR-004-backup-format-encryption-destination]].
- Pierwsze prawdziwe odtworzenie: [[SPIKE-003-backup-and-restore]] — **przed masowym przepisywaniem** (MD2).
  ✅ 2026-10-05: wykonane przez Dysk na drugim emulatorze, odcisk danych zgodny. Mechanizm:
  [[ADR-004-backup-format-encryption-destination]]. Spike sprawdził mechanizm, a nie funkcję w aplikacji.
  NFR jest spełniona dopiero, gdy pozycja produkcyjna kopii przejdzie to samo odtworzenie.
