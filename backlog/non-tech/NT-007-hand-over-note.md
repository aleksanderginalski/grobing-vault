---
title: "NT-007 — Hand-over note for the family (where the copy is, how to open it, the passphrase)"
type: non-code-item
status: open
category: stakeholder
priority: MUST
source: "PROJECT_BRIEF §5 M8 (G2), §Security"
wake-condition: "backup + export exist (SPIKE-003 → ADR-004, export US)"
created: 2026-10-05
updated: 2026-10-06
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
- Warunek obudzenia się przybliża: kopia działa (na przycisk), odtworzenie to [[ISSUE-009-restore]],
  eksport to [[US-006-eksport-dla-rodziny]].

## Resolution (fill when done — this is the DoD)
[notka przekazana (komu — rola, nie nazwisko) · data · data ostatniego sprawdzenia]
