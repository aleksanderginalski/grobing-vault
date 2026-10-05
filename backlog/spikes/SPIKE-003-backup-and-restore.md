---
title: "SPIKE-003 — Encrypted backup to the author's cloud via the system picker, and a real restore"
type: spike
status: ready
priority: MUST
time-box: "1 day"
precedes: "mass transcription (NT-002) — backup + restore must exist first (MD2)"
created: 2026-10-05
updated: 2026-10-05
---

# SPIKE-003 — Backup + restore (S-BACKUP)

## The question
**Czy aplikacja może automatycznie zapisywać kopię zaszyfrowaną w telefonie (hasłem) do folderu w
chmurze autora, wskazanego w systemowym oknie wyboru — bez kluczy API i sekretów OAuth w aplikacji — i
czy z tej kopii da się naprawdę odtworzyć wszystko na drugim urządzeniu?**

## Why it matters
§Security: kopia (zaszyfrowana, automatyczna, sprawdzona odtworzeniem) i eksport (czytelny, u rodziny)
to dwie różne rzeczy. Od pierwszej przepisanej osoby telefon jest **jedyną** cyfrową kopią — więc ten
spike poprzedza masowe przepisywanie.

## Steps
1. Zapis pliku do folderu z chmury wybranego w systemowym oknie; trwałe uprawnienie do zapisu w tle.
2. Szyfrowanie po stronie telefonu (hasło → klucz); gdzie trzymać klucz do kopii automatycznej
   (kandydat: bezpieczny magazyn, sprawdzony we wcześniejszej aplikacji autora).
3. **Androidowa automatyczna kopia (`allowBackup`)** — decyzja świadoma: limit 25 MB na aplikację
   oznacza **cicho niepełną** kopię ze zdjęciami.
4. Odtworzenie na emulatorze/drugim urządzeniu z wymyślonymi danymi; walidacja pliku przed nadpisaniem
   czegokolwiek (floor: walidacja wejścia na granicy).

## Exit criterion
**ADR-004** (format, szyfrowanie, miejsce, `allowBackup`) `accepted`; albo „okno systemowe nie wystarcza"
→ decyzja autora o alternatywie.

## Definition of Done
- [ ] Odpowiedź zapisana · kod eksperymentu usunięty · **odtworzenie wykonane naprawdę**, nie tylko
      zaprojektowane.
