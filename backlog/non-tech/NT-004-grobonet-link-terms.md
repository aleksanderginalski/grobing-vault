---
title: "NT-004 — Grobonet: may the app link to a grave's page? (link, never copy)"
type: non-code-item
status: done
category: legal
priority: SHOULD
source: "PROJECT_BRIEF §6 N4, MoSCoW W3"
created: 2026-10-05
updated: 2026-10-08
---

# NT-004 — Warunki linkowania do Grobonetu

## The question / task
Czy regulamin Grobonetu dopuszcza linkowanie do strony konkretnego grobu z prywatnej aplikacji?
Potwierdzić decyzję **tylko link, nigdy kopia** (brak publicznego API; prawa do bazy danych operatora
komercyjnego).

## Why it matters
Krok 2 ścieżki wizyty pokazuje link do Grobonetu tam, gdzie cmentarz jest pokryty (SPIKE-001 krok 1).

## Resolution (fill when done — this is the DoD)
**Regulamin nie zakazuje linku i zakazuje kopiowania. Decyzja „tylko link, nigdy kopia” jest potwierdzona.**
- [Regulamin Grobonetu](https://grobonet.com/index.php?page=regulamin), odczyt 2026-10-08 (bez daty i wersji;
  operator *„Firma Artlook Gallery s.c.”*), **nie ma zapisu o linkowaniu**: ani do serwisu, ani do konkretnych
  stron, ani o dostępie automatycznym;
- *„Dane zawarte w wyszukiwarce nie mogą być kopiowane lub wykorzystywane do celów innych niż informacji o osobach
  pochowanych”*;
- *„Właścicielami baz danych są urzędy miast, gmin i parafie”*.

Link otwiera się w zewnętrznej przeglądarce ([[NFR-005-dane-nie-opuszczaja-telefonu]]). Szukanie po nazwisku
robi autor we własnej przeglądarce, a aplikacja niczego nie pobiera. **Poza zakresem tej pozycji:** czy adres strony
grobu jest trwały. Sprawdzi się przy pierwszym prawdziwym linku. Źródło pomiaru: [[SPIKE-001-map-source-offline]]
→ *Findings* → M4 (`docs`, 2026-10-08).
