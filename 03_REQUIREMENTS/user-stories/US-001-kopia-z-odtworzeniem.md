---
title: "US-001 — Backup that restores (kopia z odtworzeniem)"
type: user-story
status: done
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M8]
journey-steps: "n/a — poza ścieżką (M8)"
FR: []
NFR: ["[[NFR-002-odtworzenie-na-nowym-telefonie]]", "[[NFR-003-migracje-schematu]]", "[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
ADR: ["[[ADR-004-backup-format-encryption-destination]]"]
issues: ["[[ISSUE-007-data-layer]]", "[[ISSUE-008-backup-write]]", "[[ISSUE-009-restore]]", "[[ISSUE-010-background-backup]]"]
quality-verdict: APPROVED
verdict-date: 2026-10-06
verdict-reviewer: self-check
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
  ✅ **2026-10-06:** obejrzane — [[ISSUE-009-restore]] zamknięte, stop #2 „ok”: kopia zapisana do Dysku na
  `Medium_Phone`, odtworzona z Dysku na `Grobing_Restore`, odcisk zgodny. **AC-3 i AC-4 tej US pokryte.**
  Zostało AC-1 (kopia sama, bez przycisku) → [[ISSUE-010-background-backup]].
  ✅ **2026-10-06:** [[ISSUE-010-background-backup]] zamknięte — kopia w tle po zmianie danych, jedna po
  sesji; kopię zrobioną w tle odtworzył człowiek. **Wszystkie cztery ISSUE przyjęte, US zamknięta**
  (*Verification* niżej).
- [[NT-003-verify-household-exemption]] (`open`) nie blokuje: ADR-004 wybrał wariant, w którym chmura
  trzyma tylko szyfrogram, a hipoteza prawna jest wtedy najmocniejsza.

## Verification (US)
> `qa`, 2026-10-06. Werdykt na poziomie US wystawił **niezależny przegląd** (subagent bez udziału w
> budowie, tylko odczyt plików i `flutter test`: 248/248), z uzupełnieniem `qa` (M7 powtórzone po
> ISSUE-010). DoD US: każde AC z testem happy-path · pokazane w aplikacji na emulatorze · werdykt zapisany ·
> wiersz w `TRACEABILITY.md`.

| AC | Test happy-path | Pokazane człowiekowi (emulator) |
|---|---|---|
| AC-1 kopia sama, czas ostatniej kopii | `background_backup_test.dart` (zmiana → kopia bez hasła, „w tle”; bez zmiany → nic), `backup_service_test.dart` (czas zapisany), `data_state_screen_test.dart` i `background_backup_screen_test.dart` (czas i „(w tle)” na ekranie, wyzwalacze) | ISSUE-010 stop #2 „ok” (zadanie przetrwało zamknięcie gestem; uruchomienie wymuszone `adb` po ciszy) · ISSUE-009 stop #2 „ok” („Zrób kopię teraz” do Dysku) |
| AC-2 czytelna bez Grobing | `backup_archive_test.dart` (sumy, liczby, odcisk, `integrity_check` — własnym czytnikiem tar), wektory C2SP (`age_testkit_test.dart`), round-trip (`age_test.dart`) | — (oficjalne `age` + `tar` + SQLite: bramka CLI `qa` w ISSUE-008, raz) |
| AC-3 odtworzenie na drugim telefonie | `restore_service_test.dart` → *end to end with the real setup* (odcisk i liczby = źródło) | ISSUE-009 stop #2 „ok”: Dysk → `Grobing_Restore`, release, odcisk zgodny · ISSUE-010: odtworzona kopia z tła |
| AC-4 zła kopia niczego nie psuje | `restore_service_test.dart`, grupa *refused* (złe hasło, bit, ucięcie, nowszy schemat, nowszy format; dane nietknięte) | złe hasło: smoke check `dev` na emulatorze (ISSUE-009); w stanie emulatora po stopie niewidoczne |
| AC-5 kopia Androida i D2D wyłączone | `repo_invariants_test.dart` (konfiguracja: manifest + reguły) | — (zachowanie: M7 w ISSUE-008 na release; **powtórzone 2026-10-06 po ISSUE-010** na bieżącym buildzie: chmura „Backup is not allowed”, D2D „Transport rejected package”, kontrola `com.android.providers.settings` „Success”; ustawienia emulatora przywrócone) |

**Werdykt: APPROVED** z uwagami.

**Czego szukano i nie znaleziono:** nieprzechodzącego testu; niezacommitowanych zmian; AC bez testu
happy-path; danych rodziny w zmianach.

**Uwagi, które nie blokują:**
1. **AC-2 nie ma stałego testu z oficjalnymi narzędziami** — oficjalne `age` i `tar` uruchomiono raz
   (bramka ISSUE-008); test automatyczny sprawdza własne moduły. Tani strażnik: test z `age`/`tar`,
   pomijany, gdy narzędzi nie ma w `PATH`. Kandydat na pozycję, nie poprawka tutaj.
2. **AC-5 sprawdza automatycznie tylko konfigurację**; zachowanie — ręcznie (M7), ostatnio po ISSUE-010.
3. **Interaktywnego `age -d -i grobing-klucz.age`** (droga z notki przekazania) nikt nie wykonał — bramka
   ISSUE-008 użyła `age-plugin-batchpass`. Do [[NT-007-hand-over-note]]: notkę sprawdzić tą drogą.
4. Kopii w tle, która ruszyła **sama przy martwym procesie**, nikt nie widział — JobScheduler trzymał gotowe
   zadanie > 3,5 min (ISSUE-010, uwaga 1). Funkcję wejścia z argumentem w AOT sprawdził build profile, nie
   release — do potwierdzenia przy pierwszym buildzie release.
5. „Zdjęcia” w testach to małe pliki tekstowe; mechanizm nie zależy od typu pliku.
6. Dwa stopy #2 w łańcuchu zostały pominięte (SPIKE-003, ISSUE-008); nadrobiły je ISSUE-009 i ISSUE-010.
