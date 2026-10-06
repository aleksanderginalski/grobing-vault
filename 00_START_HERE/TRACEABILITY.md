---
title: "Grobing — Requirements Traceability"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-06
---

# Grobing — Requirements Traceability

> Jedna macierz dla całego łańcucha: brief → EPIC → US → ISSUE. **Zasiana w dniu materializacji
> krokami ścieżki wizyty (UJ-001, brief §4a) z PUSTYMI kolumnami US i Issue** — US mają wynikać z
> kroków, więc krok bez US jest luką, którą WIDAĆ. Zasiane też: funkcje widoku 5 (zestaw funkcji, nie
> przepływ) i pozycje Must spoza ścieżki — żeby nic z Must nie było niewidoczne.

## Column ownership (so agents don't clobber each other's lanes)
> Kolumny edytuje wyłącznie ich właściciel.

| Columns | Owner |
|---|---|
| Journey step, Brief §, EPIC, US, Story Status | `docs` (strażnik vaulta; pierwsze EPIC/US wpisuje ISSUE-001, wykonywane przez `docs`) |
| Issue(s), Issue Status | `planning` |
| Quality Verdict | krytyk `quality`, gdy powstanie ([[ISSUE-003-setup-quality-critic]]); do tego czasu `qa` z `verdict-reviewer: self-check` |

## Matrix

| Journey step | Brief § | EPIC | US | Issue(s) | Story Status | Issue Status | Quality Verdict |
|---|---|---|---|---|---|---|---|
| UJ-001 · 1 — mapa Polski z cmentarzami rodziny; wybór, dokąd jechać | §4a · §5 M2 | [[EPIC-002-wizyta]] | | | | | |
| UJ-001 · 2 — na miejscu: mapa cmentarza, pinezki, adres zarządcy, link do Grobonetu | §4a · §5 M3 | [[EPIC-002-wizyta]] | | | | | |
| UJ-001 · 3 — dojście do pinezki; porównanie ze zdjęciem nagrobka | §4a · §5 M3/M4 | [[EPIC-002-wizyta]] | | | | | |
| UJ-001 · 4 — grób: wszyscy pochowani, zdjęcie + imię | §4a · §5 M4 | [[EPIC-002-wizyta]] | | | | | |
| UJ-001 · 5 — osoba: kim była, pokrewieństwa, ścieżka do „ja" | §4a · §5 M5 | [[EPIC-002-wizyta]] | | | | | |
| UJ-001 · 6 — poprawa na miejscu: pinezka, nowe zdjęcie, imię z tablicy | §4a · §5 M6 | [[EPIC-002-wizyta]] | | | | | |
| UJ-001 · 7 — powrót na mapę cmentarza → następny grób | §4a · §5 M3 | [[EPIC-002-wizyta]] | | | | | |
| n/a — widok 5 (zestaw funkcji): drzewo | §5 M9 | [[EPIC-003-zrozumienie]] | | | | | |
| n/a — widok 5: suwak czasu | §5 M10 | [[EPIC-003-zrozumienie]] | | | | | |
| n/a — widok 5: ścieżka między dowolnymi dwiema osobami | §5 M11 | [[EPIC-003-zrozumienie]] | | | | | |
| n/a — poza ścieżką (warunek kroku 1): przepisanie grobu z osobami | §5 M1 | [[EPIC-001-zabezpiecz-i-przepisz]] | [[US-002-przepisanie-grobu]] | | draft (⚠️ OPEN — Open gaps 1) | | |
| n/a — poza ścieżką (warunek kroku 1): wprowadzanie całymi rodzinami | §5 M1 · G6 | [[EPIC-001-zabezpiecz-i-przepisz]] | [[US-003-przepisanie-rodziny]] | | ready | | |
| n/a — poza ścieżką (warunek kroku 1): fakty od babci obok notatek | §2 · §5 M1 | [[EPIC-001-zabezpiecz-i-przepisz]] | [[US-004-fakt-od-babci]] | | ready | | |
| n/a — poza ścieżką (warunek kroku 1): zdjęcia nagrobka i osoby | §5 M1 | [[EPIC-001-zabezpiecz-i-przepisz]] | [[US-005-zdjecia]] | | ready | | |
| n/a — poza ścieżką (NFR): działa bez zasięgu | §5 M7 | [[EPIC-002-wizyta]] ([[NFR-001-offline]]) | | | | | |
| n/a — poza ścieżką: kopia z odtworzeniem | §5 M8 · G1 | [[EPIC-001-zabezpiecz-i-przepisz]] | [[US-001-kopia-z-odtworzeniem]] | [[SPIKE-003-backup-and-restore]] (spike: mechanizm kopii → [[ADR-004-backup-format-encryption-destination]]) · [[ISSUE-007-data-layer]] · [[ISSUE-008-backup-write]] · [[ISSUE-009-restore]] · [[ISSUE-010-background-backup]] | in-progress | SPIKE-003 done · ISSUE-007 done · ISSUE-008 done · ISSUE-009 done · ISSUE-010 in-progress | SPIKE-003: APPROVED (self-check, 2026-10-05; stop #2 pominięty) · ISSUE-007: APPROVED (self-check, 2026-10-05; stop #2 ok) · ISSUE-008: APPROVED (self-check, 2026-10-06, z uwagami; stop #2 pominięty — Dysk z kodem produkcyjnym niesprawdzony) · ISSUE-009: APPROVED (self-check, 2026-10-06, z uwagami; stop #2 ok — odtworzenie przez Dysk na drugim emulatorze) · ISSUE-010: APPROVED (self-check, 2026-10-06, z uwagami; stop #2 ok w podejściu 2 — kopia w tle po zamknięciu gestem, odtworzona z odciskiem zgodnym) |
| n/a — poza ścieżką: eksport czytelny bez aplikacji (+ notka przekazania [[NT-007-hand-over-note]], poza kodem) | §5 M8 · G2 · A4 | [[EPIC-001-zabezpiecz-i-przepisz]] | [[US-006-eksport-dla-rodziny]] | | ready | | |

> Jedna US może pokrywać 1-3 kolejne kroki — wpisz ją raz i zaznacz zakres. Każda US musi mieć brief §
> w górę i ≥1 issue w dół. Pusta komórka „Brief §" albo „Issue(s)" to luka.

## Open gaps
- **Kolumny US i Issue są puste — tak ma być** do rozpisania EPIC-ów na US.
  [[ISSUE-001-materialize-backlog]] AC-3b (2026-10-05): **każdy wiersz ma EPIC; żaden krok nie został bez <!-- placeholder-ok: real wikilink -->
  EPIC-a.** Gdyby został — trafiłby tutaj z nazwy.
  - ✅ 2026-10-05: [[EPIC-001-zabezpiecz-i-przepisz]] rozpisany. Wiersze M1 i M8 podzielone na jeden wiersz
    na US. **Kolumna Issue(s) w wierszach EPIC-001 czeka na `planning`**: ISSUE-007…009 pod US-001 już
    istnieją w `backlog/issues/`, a wpisuje je `planning` przy planowaniu każdego z nich. EPIC-002 i
    EPIC-003 bez US.
- **1 — ⚠️ OPEN: gałąź UJ-001 „grób bez pinezki" po korekcie autora** (2026-10-05, [[EPIC-002-wizyta]]).
  Brief §4a zakłada adres kwatery z notatek; **notatki go nie mają**. Przy pierwszej wizycie taki grób nie
  ma ani pinezki, ani adresu, ani zdjęcia nagrobka — krok 2 może pokazać co najwyżej link do Grobonetu
  (jeśli cmentarz jest pokryty), a krok 3 nie ma z czym porównać. **Jak Zbierający znajduje go na miejscu?** Dotyka też M1 („grób: adres kwatery, zdjęcie,
  pinezka" — przy przepisywaniu nie ma żadnego z trzech, [[EPIC-001-zabezpiecz-i-przepisz]]) i `glossary.md`
  → *pinezka* („prawdą o położeniu jest adres zarządcy" — dla takiego grobu pinezka jest jedynym
  wskaźnikiem). **Decyzja autora**; nie zmienia przypisania kroków do EPIC-ów.
- **2 — nierozstrzygnięte: grób ze zdjęcia z galerii** (pinezka z lokalizacji zdjęcia) — funkcja spoza M1.
  **Decyzja autora (2026-10-05): budowa bez terminu**, 1 listopada niczego nie wyznacza. Przy wizytach
  autor robi zdjęcia nagrobków aparatem z włączoną lokalizacją, co nie wymaga żadnej budowy. Kopię w
  Zdjęciach Google trzeba wtedy wstrzymać, bo wysłałaby zdjęcia i położenia **niezaszyfrowane**
  (brief §Security). Sama funkcja **nie jest planowana teraz** i zależy od tego, które źródła położenia
  wybierze [[SPIKE-001-map-source-offline]] (patrz `01_INBOX/2026-10-05-plany-cmentarzy.md`).
  *Nota techniczna:* systemowy picker zdjęć Androida domyślnie usuwa lokalizację. Odczyt wymaga
  `ACCESS_MEDIA_LOCATION` i poproszenia o oryginał pliku albo nowego API pickera (mainline 08.2026), w
  którym użytkownik sam zgadza się przekazać lokalizację. Poza EPIC-ami do decyzji.
