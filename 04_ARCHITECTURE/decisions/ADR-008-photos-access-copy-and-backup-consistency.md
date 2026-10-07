---
title: "ADR-008 — Photos in the app: a 2048 px JPEG access copy, and how photo files stay consistent with every backup"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-016-photos-grave-and-person]]"
source: "ISSUE-016 → Implementation plan (Prior art, Falsifier F1–F5, stop #1 rounds 1–2: D2', D3) · Library of Congress, Personal Archiving: Digital Photographs · image_picker 1.2.4 / image_picker_android 0.8.13+17 · ADR-004 (one encrypted file, whole copy each time) · backup-format.md → Known limits"
created: 2026-10-07
updated: 2026-10-07
---

# ADR-008 — Zdjęcia w aplikacji: kopia dostępowa i spójność kopii

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-07. Rozmiar wybrał autor na stopie #1 [[ISSUE-016-photos-grave-and-person]] (runda 2, D2':
*„to mają być raczej zdjęcia podglądowe”*), a spójność kopii (D3) przyjął w rundzie 1. Wdrożone i sprawdzone
(stop #2). Pomiary są w pozycji (*Falsifier*, *Dev report*, *Verification*) i tam zostają.

## Context
- Kopia to jeden plik `age` wysyłany w całości po każdej sesji ze zmianami
  ([[ADR-004-backup-format-encryption-destination]]); zadanie w tle ma ok. 10 min.
- Zdjęcia: ok. 50 nagrobków ([[ISSUE-016-photos-grave-and-person]]) i baza zdjęć osób
  ([[ISSUE-017-person-photos]]) — rząd 350 zdjęć. Oryginał z telefonu ma 3–5 MB (szacunek).
- Kanon archiwalny (Library of Congress, *Personal Archiving: Digital Photographs*): *„save the one with highest
  quality”*, *„Make at least two copies”*. Autor świadomie wybrał w aplikacji **kopię dostępową**, a oryginał zostaje
  w galerii albo na papierze.
- Kod przed tą decyzją miał lukę: odcisk danych i archiwum listowały pliki zdjęć **dwa razy**, więc zdjęcie dodane
  między listami dawało kopię, której żadne odtworzenie nie przyjmie (ISSUE-016 → *Prior art*, F4).

## Decision
1. **Kopia dostępowa:** aplikacja trzyma JPEG jakości 85, dłuższy bok najwyżej **2048 px** (mniejsze bez zmiany
   rozmiaru), z orientacją zapisaną w pikselach, **bez EXIF** (także bez lokalizacji). Robi ją kod natywny
   (`PhotoPreparation.kt`: `ImageDecoder` od Androida 9, `BitmapFactory` + `ExifInterface` na 7–8), bo
   `image_picker` nie zmniejsza HEIF.
2. **Wybór zdjęcia:** `image_picker` z włączonym Android Photo Picker (`useAndroidPhotoPicker`) — bez uprawnień do
   pamięci i aparatu.
3. **Spójność z kopią** (kolejność kroków):
   - **jedna lista plików** zdjęć dla odcisku danych i archiwum, robiona po migawce bazy;
   - **dodanie:** plik powstaje (w katalogu roboczym poza `media/`, potem przeniesienie) **przed** wierszem `media`;
   - **usunięcie i zmiana:** kasują tylko wiersz; plik bez wiersza usuwa **sprzątanie** pod zamkiem danych — przed
     znacznikiem i migawką każdej kopii oraz przy starcie — i tylko plik starszy niż 1 h.

   Każdy wiersz w migawce ma wtedy swój plik w kopii, a zdjęcie dodane albo usunięte w trakcie kopii jej nie psuje.
4. **Grób ma najwyżej jedno zdjęcie** (decyzja autora); bez zmiany schematu. Model zdjęć osób → ADR przy
   [[ISSUE-017-person-photos]].

## Options considered
| Option | For | Against | Status |
|---|---|---|---|
| Oryginał bajt w bajt (3–5 MB) | pełna jakość, EXIF z lokalizacją (przyszła pinezka ze zdjęcia); kanon archiwalny | kopia 1–1,75 GB wysyłana po każdej sesji; HEIF bez gwarancji dekodowania | rejected (autor: „podglądowe”) |
| 2560 px | duże przybliżenie | ok. 2× rozmiaru 2048 px przy małym zysku na ekranie ~1080 px | rejected |
| **2048 px, JPEG 85, bez EXIF** | ok. 2× przybliżenia (napis na tablicy, twarz z grupowego zdjęcia — przyszłe `CROP`); kopia ok. 0,15–0,25 GB przy 350 zdjęciach; jeden format dla każdego wejścia | oryginał nie trafia do aplikacji; brak EXIF z lokalizacją; kod natywny bez testu automatycznego | **chosen** |
| 1600 / 1280 px | najmniejsza kopia | przybliżenie miękkie albo bezużyteczne | rejected |
| Oryginał w aplikacji, zmniejszony tylko w kopii | pełna jakość w telefonie | kopia przestaje być wierna, odcisk danych się nie zgadza, odtworzenie oddaje inne zdjęcia | rejected |
| Spójność: usunięcie czeka na zamek kopii (bez sprzątania) | prostsze | usunięcie zdjęcia może czekać do ~1,5 min z „Usuwam…”; nie sprząta plików po przerwaniu | rejected |

## Consequences
- **Positive:** F1 na emulatorze — JPEG 2048 × 1536, orientacja z EXIF poprawna, bez EXIF; F2 na hoście — 205 MB
  zdjęć to kopia ok. 22 s; test F4 na starym kodzie czerwony, na nowym zielony; odtworzenie ze zdjęciem sprawdzone na
  drugim emulatorze. Brak nowych uprawnień.
- **Negative / trade-offs:**
  - zdjęcie w aplikacji nie zastąpi oryginału do druku albo dużego powiększenia;
  - pinezka ze zdjęcia (`TRACEABILITY.md` → *Open gaps* 2) musiałaby czytać lokalizację z oryginału w galerii;
  - przez godzinę po zmianie albo usunięciu zdjęcia „Stan danych” pokazuje więcej plików niż wpisów, a kopia te
    pliki zawiera (odcisk liczy je spójnie);
  - HEIF niesprawdzony (F3) — pierwsze prawdziwe zdjęcie z telefonu autora przy MVP.
- **Follow-ups:**
  - Okno wyboru na Androidzie 16 wymaga „Gotowe” także przy jednym zdjęciu (zmierzone dla `GET_CONTENT` i
    `PICK_IMAGES`) — poza kontrolą aplikacji.
  - Zmiana wersji `image_picker*` to przegląd, a nie `pub upgrade` (komentarz w `pubspec.yaml`).
  - Przy [[ISSUE-017-person-photos]]: odcisk danych liczy SHA-256 każdego zdjęcia, więc przy ~350 zdjęciach „Stan
    danych” na telefonie może liczyć kilka sekund (F2 na hoście: 4,9 s na 205 MB).
