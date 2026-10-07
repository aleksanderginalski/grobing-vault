---
title: "ADR-010 — Profile photo crop: GEDCOM CROP in pixels of the access copy, on the person's link (schema v5)"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-018-profile-photo-crop]]"
source: "ISSUE-018 → Implementation plan (Prior art, D1, F1–F6), stop #1 (author: „D1 — ok”) · GEDCOM 7.0 (MULTIMEDIA_LINK → CROP) · Gramps MediaRef region (forum threads) · grobing-code PhotoPreparation.kt (EXIF applied before saving) · ADR-008 · ADR-009"
created: 2026-10-07
updated: 2026-10-07
---

# ADR-010 — Kadr profilowego: `CROP` z GEDCOM w pikselach kopii dostępowej, przy łączu osoby

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-07. Autor przyjął D1 na stopie #1 [[ISSUE-018-profile-photo-crop]] („D1 — ok”). Wdrożone i sprawdzone
w tej samej pozycji: test migracji v4→v5 z danymi (F2), odtworzenie kopii v4 w v5 (F3), kopia z kadrami odtworzona na
drugim emulatorze z odciskiem zgodnym (F4), kadr zachowany przy późniejszej edycji zdjęć (F1).

## Context
- **Decyzja autora (stop #2 [[ISSUE-017-person-photos]]):** profilowe ze zdjęcia grupowego ma pokazywać tę osobę, a nie
  środek zdjęcia — kadr z liniami pomocniczymi ([[kadr-profilowego]]).
- **Kanon — [GEDCOM 7.0](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html)** (odczyt 2026-10-07): `CROP` stoi
  przy łączu `OBJE` (`MULTIMEDIA_LINK`); `TOP` i `LEFT` to *„a number of pixels to not display from the top/left side of
  the image”*, `HEIGHT` i `WIDTH` to rozmiar w pikselach; wycinek poza obrazem jest błędem.
- **Gramps:** region przy `MediaRef` to narożniki w **procentach** obrazu, liczby całkowite (źródła w
  [[kadr-profilowego]] → *Prior art*).
- **Z kodu:** kopia dostępowa (2048 px, JPEG 85, [[ADR-008-photos-access-copy-and-backup-consistency]]) jest obracana według
  EXIF **przed** zapisem i nie ma EXIF (`PhotoPreparation.kt`), a zdjęcia osoby nie podmienia się w miejscu — plik łącza
  się nie zmienia. Łącze to `person_media` ([[ADR-009-person-photos-record-and-link]]).

## Decision
1. **Kadr to cztery kolumny `person_media`:** `crop_left`, `crop_top`, `crop_width`, `crop_height` — liczby całkowite,
   **piksele pliku zdjęcia** (kopii dostępowej), opcjonalne. Wszystkie puste = bez kadru: okrąg pokazuje największy
   kwadrat ze środka, jak przed v5. Niepełny albo z rozmiarem ≤ 0 czyta się jako brak.
2. **Kadr należy do łącza**, więc każda osoba na zdjęciu grupowym ma własny, a plik zdjęcia się nie zmienia.
3. **Ekran zapisuje kwadrat w obrębie obrazu** (okrąg wpisany w kwadrat); model przyjmie prostokąt jak GEDCOM, a okrąg
   bierze z niego kwadrat ze środka. Granicę obrazu pilnuje ekran i rysowanie, bo wymiarów zdjęcia nie ma w bazie.
4. **Kadr przeżywa każdą edycję zdjęć osoby:** zapis przepisuje łącza osoby od nowa, więc najpierw czyta ich kadry i
   zapisuje je z powrotem, chyba że edycja ustawiła nowy (F1).
5. **Migracja v4→v5:** cztery `addColumn` — bez zmiany wierszy i bez przebudowy tabeli.
6. **Kadr bez źródła i statusu** — mówi, gdzie na zdjęciu jest twarz, a nie podaje daty, relacji ani pochówku
   ([[FR-001-provenance]]); łącze w GEDCOM 7 nie ma `SOUR`.

## Options considered
| Option | For | Against | Status |
|---|---|---|---|
| **(a) piksele kopii dostępowej, cztery kolumny jak GEDCOM `CROP`** | plik łącza się nie zmienia i jest wyprostowany, więc piksele są stabilne; eksport do GEDCOM 1:1; liczby całkowite w odcisku danych | wymiary zdjęcia do rysowania trzeba czytać z nagłówka pliku (każda opcja poza (e) i tak ich potrzebuje) | **chosen** |
| (b) ułamki boków (`REAL` 0…1) | niezależne od rozdzielczości | plik się nie zmienia, więc nic nie zyskujemy; kwadrat w pikselach wymaga zaokrągleń; eksport i tak liczy piksele | rejected |
| (c) środek i promień okręgu w ułamkach | prosto odwzorowuje okrąg | GEDCOM i każdy przyszły kadr prostokątny potrzebują prostokąta | rejected |
| (d) procenty całkowite jak region w Gramps | zgodne z Gramps | za grube: 1 % to ok. 20 px zdjęcia 2048 px, a przy najmniejszym kadrze (128 px) krok to ok. 16 % kadru | rejected |
| (e) osobny plik wycinka przy każdym łączu | najprostsze rysowanie | dodatkowe pliki w kopii i w sprzątaniu (ADR-008 pkt 3); każda poprawka kadru to nowy plik | rejected — wraca tylko, gdyby okręgi z małym kadrem zabrakły pamięci (F6) |

## Consequences
- **Positive:**
  - dwie osoby na jednym zdjęciu mają różne kadry, plik jeden i niezmieniony (test i emulator);
  - łącza z v4 po migracji wyglądają jak przed nią (bez kadru = środek);
  - kadr jest w kopii i w odcisku danych; kopia z kadrami odtworzona na drugim emulatorze z odciskiem zgodnym (F4);
  - kopia v4 odtwarza się w aplikacji v5 (F3).
- **Negative / trade-offs:**
  - okrąg z małym kadrem dekoduje prawie całe zdjęcie (do 2048 px, ok. 12 MB na plik) — pomiar na emulatorze to tylko
    sygnał, bo emulator nie pokazuje pamięci grafiki (F6, [[ISSUE-018-profile-photo-crop]] → *Dev report*);
  - okrąg z kadrem jest pusty, dopóki nie przeczyta wymiarów z nagłówka pliku (chwila przy pierwszym pokazaniu);
  - odciski sprzed v5 i po v5 nie są porównywalne, jak przy każdej zmianie schematu.
- **Follow-ups:**
  - pomiar pamięci okręgów z małym kadrem na telefonie autora przy MVP; źle → dekodowanie z limitem 1× dla okręgów ≤ 40 dp,
    potem opcja (e);
  - kadr z oryginału w wyższej rozdzielczości — poza zakresem (oryginał zostaje w galerii, ADR-008); gdyby kopia dostępowa
    łącza kiedyś zmieniła rozdzielczość, migracja przelicza kadr proporcjonalnie.
