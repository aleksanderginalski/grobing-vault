---
title: "US-005 — Attach photos to a grave and a person (zdjęcia)"
type: user-story
status: ready
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M1]
journey-steps: "n/a — poza ścieżką (M1)"
FR: []
NFR: ["[[NFR-002-odtworzenie-na-nowym-telefonie]]", "[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
issues: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §5 M1 (zdjęcie nagrobka, zdjęcie osoby) · §4 Pains („brak zdjęć") · data-model.md (Media)"
created: 2026-10-05
updated: 2026-10-05
---

# US-005 — Zdjęcia nagrobka i osoby

## Story
**Jako** Zbierający **chcę** dołączyć zdjęcie nagrobka do grobu i zdjęcie osoby do osoby, **żeby**
notatki bez zdjęć przestały być jedynym zapisem, a zdjęcia przeżyły telefon razem z danymi.

## Acceptance Criteria
- **AC-1 — zdjęcie przy grobie i osobie.** *When* wybieram zdjęcie z galerii albo robię je aparatem
  *Then* jest widoczne przy grobie albo przy osobie.
- **AC-2 — zdjęcie w prywatnym magazynie aplikacji.** *Then* aplikacja trzyma własną kopię pliku w
  prywatnym magazynie (data-model.md → *Media*) i nie zależy od tego, czy oryginał zostanie w galerii.
- **AC-3 — zdjęcie jest w kopii.** *Given* zdjęcie w aplikacji *When* powstaje kopia *Then* zdjęcie jest
  w niej i wraca po odtworzeniu (odcisk danych obejmuje zdjęcia —
  [[NFR-002-odtworzenie-na-nowym-telefonie]]).

## Out of scope
- Pinezka z lokalizacji zdjęcia → `TRACEABILITY.md` → *Open gaps* 2 (nieplanowane).
- Nowe zdjęcie robione na miejscu przy wizycie → [[EPIC-002-wizyta]] (M6).

## Notes
- **Rozdzielczość zdjęć w aplikacji** jest nierozstrzygnięta (poza zakresem [[SPIKE-003-backup-and-restore]]).
  Waży, bo każda kopia wysyła całość (ADR-004, *Consequences*). Decyzja przy planowaniu pierwszego ISSUE.
- **Kopia a zdjęcia (2026-10-06, [[ISSUE-008-backup-write]]):** migawka bazy (`VACUUM INTO`) i odczyt plików
  zdjęć nie są jedną transakcją. Dziś zdjęcia dodaje tylko przycisk debug. Gdy zdjęcie da się usunąć,
  usunięcie w trakcie kopii zostawi w kopii wpis bez pliku — do rozstrzygnięcia przy planowaniu
  (`04_ARCHITECTURE/backup-format.md` → *Known limits*).
- **Kopia w tle a zdjęcia (2026-10-06, [[ISSUE-010-background-backup]]):** kopia powstaje raz po sesji
  (10 min ciszy, najpóźniej 60 min od pierwszej zmiany) i zawsze wysyła całość. Przy pierwszych zdjęciach
  te dwie liczby wracają do decyzji razem z rozdzielczością. Do tego:
  - zadanie w tle ma ~10 min — kopia rzędu kilku GB wymagałaby zadania na pierwszym planie;
  - stempel zmian widzi zdjęcie po rozmiarze i czasie pliku, nie po treści — zdjęcie zmienione „w
    miejscu” (ten sam rozmiar, przywrócony czas) nie wyzwoli kopii. Dziś aplikacja zdjęć w miejscu nie
    edytuje.
- Kopię w Zdjęciach Google trzeba wstrzymać dla zdjęć nagrobków, bo wysłałaby je niezaszyfrowane
  (`TRACEABILITY.md` → *Open gaps* 2).
