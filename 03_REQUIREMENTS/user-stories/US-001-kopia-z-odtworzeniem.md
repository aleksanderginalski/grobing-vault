---
title: "US-001 — Backup that restores (kopia z odtworzeniem)"
type: user-story
status: in-progress
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M8]
journey-steps: "n/a — poza ścieżką (M8)"
FR: []
NFR: ["[[NFR-002-odtworzenie-na-nowym-telefonie]]", "[[NFR-003-migracje-schematu]]", "[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
ADR: ["[[ADR-004-backup-format-encryption-destination]]"]
issues: ["[[ISSUE-007-data-layer]]", "[[ISSUE-008-backup-write]]", "[[ISSUE-009-restore]]", "[[ISSUE-010-background-backup]]"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §5 M8 · §5a G1 · ADR-004 · MD2 (kopia przed masowym przepisywaniem)"
created: 2026-10-05
updated: 2026-10-06
---

# US-001 — Kopia z odtworzeniem

## Story
**Jako** Zbierający **chcę**, żeby dane z aplikacji same trafiały, zaszyfrowane w telefonie, do mojego
Dysku i dały się odtworzyć na nowym telefonie, **żeby** utrata telefonu nie była utratą tego, co
przepisałem i usłyszałem od babci.

**Dlaczego pierwsza w EPIC-u (MD2):** od pierwszej przepisanej osoby telefon byłby jedyną cyfrową kopią,
czyli problemem papieru od nowa. Mechanizm jest rozstrzygnięty w
[[ADR-004-backup-format-encryption-destination]].

## Acceptance Criteria
- **AC-1 — kopia powstaje sama.** *Given* kopia jest skonfigurowana raz (hasło, plik klucza, plik kopii
  w Dysku) *When* dane w aplikacji się zmieniają *Then* w Dysku jest jeden zaszyfrowany plik kopii z
  aktualnymi danymi, bez wpisywania hasła, a aplikacja pokazuje, kiedy była ostatnia udana kopia.
- **AC-2 — kopia jest czytelna bez Grobing.** *Given* plik kopii, plik klucza i hasło *When* otwieram je
  na PC oficjalnym `age`, zwykłym `tar` i dowolnym SQLite *Then* widzę bazę i zdjęcia, a sumy kontrolne
  zgadzają się z manifestem.
- **AC-3 — odtworzenie na drugim telefonie.** *Given* kopia w Dysku, plik klucza i hasło *When* odtwarzam
  je na drugim urządzeniu (`Grobing_Restore`) *Then* odcisk danych jest identyczny ze źródłem
  ([[NFR-002-odtworzenie-na-nowym-telefonie]] → *Method*).
- **AC-4 — zła kopia niczego nie psuje.** *Given* złe hasło, uszkodzony plik albo kopia z nowszej wersji
  aplikacji *When* próbuję odtworzyć *Then* aplikacja odmawia z czytelnym komunikatem, a dane w telefonie
  zostają nietknięte.
- **AC-5 — jedyna droga danych z telefonu.** *Given* zainstalowana aplikacja *Then* kopia Androida w
  chmurze i transfer na nowe urządzenie (D2D) nie obejmują danych Grobing
  ([[NFR-005-dane-nie-opuszczaja-telefonu]], ADR-004 pkt 4).

## Issues (in order)
| # | Issue | Co daje do kliknięcia |
|---|---|---|
| 1 | [[ISSUE-007-data-layer]] | baza ze schematem v1 i ekran „Stan danych" (wersja schematu, liczby rekordów, odcisk danych) |
| 2 | [[ISSUE-008-backup-write]] | konfiguracja kopii, „Zrób kopię teraz", „ostatnia udana kopia" |
| 3 | [[ISSUE-009-restore]] | odtworzenie z pliku kopii na świeżej instalacji |
| 4 | [[ISSUE-010-background-backup]] | kopia w tle po zmianie danych, bez hasła |

> **Podział na trzy, nie dwa (docs, 2026-10-05).** Autor zatwierdził „najpierw baza, potem kopia". Kopia
> razem z odtworzeniem to ADR-004 pkt 1-6 i cztery uwagi `qa` ze spike'a, czyli więcej niż jedno ISSUE
> (~0,5-1 dnia, `glossary.md`). Zakres się nie zmienił, tylko podzielił.
>
> **Na cztery (decyzja autora na stopie #1 ISSUE-008, 2026-10-06, D1).** Kopia w tle ma własną niewiadomą
> i własną decyzję (kiedy się uruchamia), więc wyszła do ISSUE-010. Idzie po odtworzeniu: najpierw
> domknięta pętla „kopia → odtworzenie”, potem automatyzacja. AC-1 tej US jest spełnione dopiero z ISSUE-010.

## Out of scope
- Eksport czytelny bez aplikacji → [[US-006-eksport-dla-rodziny]].
- Notka przekazania z hasłem i miejscem pliku klucza → [[NT-007-hand-over-note]] (poza kodem).
- Kopia przyrostowa: Dysk nie działa w oknie wyboru folderu (ADR-004, *Options*).

## Notes
- US jest `done` dopiero, gdy wszystkie cztery ISSUE są przyjęte, a odtworzenie obejrzał człowiek. W
  [[SPIKE-003-backup-and-restore]] stop #2 został pominięty; uwaga `qa`: pierwsze odtworzenie, które
  obejrzy człowiek, wypada tutaj ([[ISSUE-009-restore]]).
- [[NT-003-verify-household-exemption]] (`open`) nie blokuje: ADR-004 wybrał wariant, w którym chmura
  trzyma tylko szyfrogram, a hipoteza prawna jest wtedy najmocniejsza.
