---
title: "ISSUE-008 — Production backup: encrypted on the phone, one age file in the author's Drive"
type: issue
status: ready
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-001-kopia-z-odtworzeniem]]"
ideal_days: 1
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
created: 2026-10-05
updated: 2026-10-05
---

# ISSUE-008 — Kopia: zapis

> Mechanizm jest rozstrzygnięty w [[ADR-004-backup-format-encryption-destination]] (pkt 1-4) i zmierzony w
> [[SPIKE-003-backup-and-restore]] → *Findings*. Kod spike'a został usunięty, więc to jest budowa od
> nowa, na pomiarach. Musi działać **przed pierwszymi prawdziwymi danymi** (ADR-004 → *Follow-ups*).

## What to build
1. **Konfiguracja kopii (raz):**
   - tożsamość X25519 i plik tożsamości zaszyfrowany hasłem (scrypt, work factor 18), zapisany przez
     systemowe okno zapisu pliku;
   - w aplikacji zostaje tylko klucz publiczny;
   - plik kopii w Dysku wskazany oknem zapisu pliku (`ACTION_CREATE_DOCUMENT`) z trwałym uprawnieniem
     do odczytu i zapisu.

   Hasło autor wpisuje w aplikacji. Żaden plik z hasłem nie powstaje.
2. **Format (ADR-004 pkt 2):** własny moduł `age` v1 na `cryptography` i `pointycastle`; `tar` z
   `manifest.json` (`format_version`, `schema_version`, liczby rekordów, SHA-256 każdego pliku),
   migawką `VACUUM INTO` i `media/*`.
3. **Zapis:** nadpisanie pliku kopii w trybie `"wt"`. „Zrób kopię teraz" oraz kopia w tle bez hasła.
   Kiedy kopia w tle się uruchamia, wybiera `planning`; termin wykonania wyznacza Android.
4. **„Ostatnia udana kopia: kiedy"** na ekranie „Stan danych" (uwaga `qa` ze SPIKE-003). Uczciwie:
   aplikacja wie, że Dysk przyjął plik, nie że go wysłał (ADR-004, *Consequences*).
5. **`allowBackup="false"` i `dataExtractionRules`** wykluczające wszystko w `<cloud-backup>` i
   `<device-transfer>` (ADR-004 pkt 4).

## Acceptance Criteria
- [ ] Po jednorazowej konfiguracji „Zrób kopię teraz" zapisuje w Dysku jeden plik `age`, a ekran
      „Stan danych" pokazuje czas ostatniej udanej kopii.
- [ ] Kopia w tle powstaje po zmianie danych bez pytania o hasło (zmierzone na emulatorze; termin
      zapisany, nie obiecany).
- [ ] **Bramka zgodności (`qa`):** plik kopii + plik klucza + hasło otwierają się na PC oficjalnym
      `age` (`age -d`, potem `age -d -i`) i zwykłym `tar`. Wszystkie SHA-256 zgadzają się z manifestem,
      `integrity_check` = `ok`, a odcisk danych zgadza się z ekranem „Stan danych".
- [ ] Kopia Androida i transfer D2D nie obejmują danych `com.grobing.app`, sprawdzone tak samo jak M7
      w spike'u.
- [ ] Bez kluczy API, sekretów OAuth i uprawnienia `INTERNET` dla kopii; nowe zależności przejrzane
      ([[NFR-005-dane-nie-opuszczaja-telefonu]]).

## Out of Scope
- Odtworzenie w aplikacji → [[ISSUE-009-restore]].
- Eksport HTML + PDF → [[US-006-eksport-dla-rodziny]].
- Treść notki przekazania (hasło, miejsce pliku klucza) → [[NT-007-hand-over-note]].
- Kopia przyrostowa (ADR-004, *Options*: niewykonalna przez okno systemowe).

## Technical Notes
- Pomiary do wykorzystania (SPIKE-003 → *Findings*): czyste szyfrowanie w Darcie ~8 MB/s
  (`cryptography_flutter` jako opcja); scrypt tylko przy konfiguracji i odtworzeniu, nigdy przy kopii w
  tle; Dysk w oknie zapisu pliku działa w tle i przeżywa restart; termin kopii w tle od ~1 min do > 44 min.
- Próbne odtworzenie z DoD, zanim powstanie [[ISSUE-009-restore]]: oficjalne CLI na PC (bramka zgodności
  wyżej), tak jak M5 w spike'u.
- Dane do pokazania: wymyślone, mechanizmem z [[ISSUE-007-data-layer]] (nigdy w buildzie release).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-007-data-layer]] | technical | `ready` |
| [[ADR-004-backup-format-encryption-destination]] | technical | `accepted` |
| emulator `Grobing_Restore` z kontem Google autora | technical | istnieje (SPIKE-003) |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP): test happy-path dla każdego AC · ręczna weryfikacja na
emulatorze · próbne odtworzenie (tu: oficjalnym CLI) · zero danych rodziny w zmianach (pliki `*.age` w
żadnym repo — strażnik [[ISSUE-006-setup-family-data-guard]]) · INVEST self-check.
