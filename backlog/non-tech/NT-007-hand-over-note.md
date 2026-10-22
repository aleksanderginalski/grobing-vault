---
title: "NT-007 — Hand-over note for the family (where the copy is, how to open it, the passphrase)"
type: non-code-item
status: open
category: stakeholder
priority: MUST
source: "PROJECT_BRIEF §5 M8 (G2), §Security"
wake-condition: "backup + export exist (SPIKE-003 → ADR-004; export = the backup since ADR-018 — ISSUE-040)"
created: 2026-10-05
updated: 2026-10-22
---

# NT-007 — Notka przekazania dla rodziny

## The question / task
Krótka, **papierowa** notka trzymana u rodziny: że kopia istnieje · gdzie jest · jak ją otworzyć ·
**gdzie jest hasło** (nie w tej samej chmurze) · gdzie leży eksport czytelny bez aplikacji.

## Why it matters
„Przetrwa mnie i aplikację" (§2) zawodzi po cichu, jeśli nikt nie wie, gdzie jest kopia. **Zgubione
hasło = utracona kopia** (§Security).

> Treść notki to dane rodziny i sekret — **nie w repo**. W vaulcie tylko fakt, że notka istnieje i
> kiedy była ostatnio sprawdzona.

## Input from SPIKE-003 (2026-10-05) — what the note must cover
Mechanizm: [[ADR-004-backup-format-encryption-destination]]. Do odtworzenia potrzebne są **trzy rzeczy**,
nie dwie:
1. **plik kopii** (w Dysku autora);
2. **plik klucza** (obok kopii; w środku klucz prywatny zaszyfrowany hasłem);
3. **hasło**.

Utrata pliku klucza = utracona kopia, nawet z hasłem. Dlatego notka (fizyczna, nie w tej samej chmurze)
powinna mieć **hasło i sam klucz prywatny** wydrukowany (ciąg `AGE-SECRET-KEY-1…`, 74 znaki; wygodniej
jako kod QR).

Notka powinna też powiedzieć:
- **Jak otworzyć kopię bez Grobing**, gdyby aplikacji już nie było: `age` (age-encryption.org) → `tar` →
  baza SQLite i zdjęcia.
- Że na świeżym telefonie folder Dysku w systemowym oknie wyboru bywa przez pierwsze minuty pusty, a pliki
  znajduje **wyszukiwarka** tego okna.

## Input from ISSUE-008 (2026-10-06) — the production backup exists
- Domyślne nazwy plików: `grobing-kopia.age` i `grobing-klucz.age`, w folderze Dysku wybranym przy
  konfiguracji (autor może je zmienić — notka podaje te, które naprawdę są).
- **Jak otworzyć kopię bez Grobing:** `04_ARCHITECTURE/backup-format.md` → *Opening a backup without
  Grobing* (trzy polecenia: `age`, `tar`, SQLite). Notka może przepisać je wprost, bo vault nie trafi do
  rodziny.
- Klucz prywatny do wydruku da się wyjąć na PC: `age -d grobing-klucz.age` (pyta o hasło) — aplikacja go
  nie pokazuje.
- **„Skonfiguruj kopię od nowa” w aplikacji tworzy nowy klucz:** po każdej ponownej konfiguracji notka
  jest nieaktualna i trzeba ją wymienić.
- Warunek obudzenia się przybliża: kopia działa (na przycisk), odtworzenie to [[ISSUE-009-restore]]
  (✅ 2026-10-06), eksport to [[US-006-eksport-dla-rodziny]].

## Input from ISSUE-009 (2026-10-06) — restore exists in the app
- **Odtworzenie w Grobing:** „Stan danych” → „Odtwórz z kopii” → plik kopii, plik klucza (systemowe okno
  wyboru pliku) → hasło. Zła kopia albo złe hasło niczego w telefonie nie zmienia.
- Na świeżym telefonie folder Dysku w oknie bywa przez kilka minut pusty — **lupa u góry okna, wpisać
  „grobing”**. Plików o tej samej nazwie może być kilka; aplikacja pokazuje po odtworzeniu datę kopii.
- **Najświeższej kopii może jeszcze nie być w chmurze:** Dysk wysyła plik z opóźnieniem (w teście:
  kilkanaście minut). Kopia sprzed chwili ze starego telefonu nie musi być tą, którą zobaczy nowy.
- **Po zmianie telefonu notka zostaje ważna:** odtworzona aplikacja robi dalej kopie tym samym kluczem do
  tego samego pliku (ISSUE-009, D3). Nieaktualna robi się dopiero po „Skonfiguruj kopię od nowa” (nowy
  klucz) — albo gdy Dysk nie pozwoli pisać do pliku (aplikacja mówi to wprost po odtworzeniu).
- Stary telefon po zmianie: wyłączyć mu kopię, inaczej dwa telefony nadpisują jeden plik
  (`04_ARCHITECTURE/backup-format.md` → *Known limits*).

## Input from US-001 closure (2026-10-06)
- Drogi z notki — **`age -d -i grobing-klucz.age grobing-kopia.age`, z hasłem wpisanym w terminalu** —
  nikt jeszcze nie wykonał w tej postaci (bramka ISSUE-008 otworzyła plik klucza przez
  `age-plugin-batchpass`). Przy pisaniu notki przejść ją raz, na wymyślonych danych.
- Kopia robi się sama ok. 10 min po ostatniej zmianie ([[ISSUE-010-background-backup]]); dla rodziny nic
  się przez to nie zmienia — odtworzenie nadal = plik kopii + plik klucza + hasło.

## Input from ISSUE-040 (2026-10-16) — the export is the backup
- **Osobnego eksportu dla rodziny nie ma** (decyzja autora, [[ADR-018-export-is-the-backup]]): punkt „gdzie leży eksport czytelny bez aplikacji”
  wypada z notki i z ekranu notki w aplikacji. Dane poza aplikacją = kopia otwarta drogą z notki (plik kopii + plik klucza + hasło + `age`).
- Warunek obudzenia („backup + export exist”) jest spełniony, gdy zamknie się [[ISSUE-040-export-is-the-backup]].
- Skutek dla rodziny: bez autora dane czyta ktoś, kto przejdzie `age` → `tar` → SQLite. Notka powinna więc mówić te trzy kroki wprost (już mówi:
  *Input from ISSUE-008*).

## Input from ISSUE-032 (2026-10-22) — the production backup on the phone
- **Kopia docelowa skonfigurowana 2026-10-22 13:31** na telefonie autora (Grobing 1.0.0 ze sklepu), na **Dysku Google**, domyślne nazwy
  `grobing-kopia.age` i `grobing-klucz.age`. To **nowy klucz** — notka musi powstać z tej konfiguracji; każda następna „Skonfiguruj kopię od nowa”
  ją unieważnia.
- **Droga z notki niesprawdzona na tej kopii — decyzja autora** (*„na razie nie chcę tego robić — tamte działały”*): mechanizm `age` → `tar` → odcisk
  przeszedł 2026-10-21 na kopii próbnej z emulatora ([[ISSUE-032-mvp-install]] → *Dev report*, *Step 7*), a odtworzenie na telefonie tą samą drogą.
  **Niesprawdzone zostaje:** czy hasło zapisane do notki jest tym, które wpisano w telefonie, i czy oba pliki są na Dysku. Do czasu sprawdzenia
  pomyłka w haśle = kopia, której nie da się otworzyć.
- **Sprawdzenie przy pisaniu notki** (autor, terminal VS Code, PowerShell; hasło wpisuje autor — agent go nie widzi). `age` v1.3.2 czeka w
  `C:\Programowanie\Grobing\_notka\` (poza repo):
  1. oba pliki z Dysku do `C:\Programowanie\Grobing\_notka\`;
  2. `.\age.exe -d -i grobing-klucz.age -o kopia.tar grobing-kopia.age` → `mkdir kopia; tar -xf kopia.tar -C kopia` (w PowerShellu `-o`, nie `>`);
  3. w `grobing-code`: `dart run tool/fingerprint.dart C:\Programowanie\Grobing\_notka\kopia` → odcisk równy „Stanowi danych” w telefonie
     (przy pustej bazie z 13:31: `dff49ae6db482714`; po pierwszych wpisach — ten, który pokazuje telefon);
  4. `.\age.exe -d grobing-klucz.age` → klucz prywatny `AGE-SECRET-KEY-1…` na papier (albo kod QR); nie do czatu;
  5. `Remove-Item -Recurse kopia, kopia.tar, grobing-*.age`.
  Najtańsza wersja bez PC (sprawdza tylko hasło i pliki, nie drogę bez aplikacji): w Grobing „Odtwórz z kopii” z plikami z Dysku i hasłem z kartki —
  **tylko przy pustej bazie albo zaraz po kopii**, bo odtworzenie zastępuje dane w telefonie.
- Czytający bazę bez aplikacji pomija `persons.is_living` (zawsze 0) — `backup-format.md` → *Opening a backup without Grobing*.

## Resolution (fill when done — this is the DoD)
[notka przekazana (komu — rola, nie nazwisko) · data · data ostatniego sprawdzenia]
