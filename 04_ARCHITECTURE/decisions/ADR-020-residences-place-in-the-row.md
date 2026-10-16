---
title: "ADR-020 — Places of residence: one table, the place in words in the row, the end worked out from the next residence"
type: adr
status: accepted
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-042-places-of-residence]]"
source: "plan `planning` przy stopie #1 ISSUE-042 (R1, G1; autor: „jest ok”, potwierdzone w `/pm` 2026-10-16 — A1, N2) · decyzja autora na stopie #2 („tak, zróbmy to jak rekomendujesz” — D12) · GEDCOM 7 `INDI-RESI`, typ Date (`FROM`/`TO`) · GeoNames (CC BY 4.0) · [[zamieszkanie]] v1.2"
created: 2026-10-16
updated: 2026-10-16
---

# ADR-020 — Miejsca zamieszkania: jedna tabela, miejsce słowami w wierszu, koniec z następnego zamieszkania

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-16: model na stopie #1 [[ISSUE-042-places-of-residence]] (plan `planning`, R1 i G1; A1 i N2 potwierdzone przez autora w `/pm`),
koniec wyliczany — decyzja autora na stopie #2 (D12 w [[zamieszkanie]] v1.2).

## Context
Autor chce zapisywać, **gdzie i kiedy osoba mieszkała** — od samego kraju, przez miejscowość, po adres — żeby mapa migracji
([[ISSUE-045-migration-map]]) pokazała, kto gdzie był w danym roku. Kanon genealogii ma na to fakt zamieszkania z okresem i miejscem
([GEDCOM 7 `INDI-RESI`](https://gedcom.io/terms/v7/INDI-RESI)); okres zapisuje się `FROM … TO …`, a `BET … AND …` to nieznana data jednego zdarzenia
([GEDCOM 7 — type Date](https://gedcom.io/terms/v7/type-Date)). `events` ma jeden dopisek na parę dat i miejsce tylko jako tekst — punktu na mapie z
niego nie ma. Kopia jest eksportem dla rodziny ([[ADR-018-export-is-the-backup]]): musi się czytać bez aplikacji.

## Decision
1. **Jedna nowa tabela `residences`** (schemat v13, migracja `createTable` + indeks — kopie v12 odtwarzają się z osobami bez zamieszkań): osoba ·
   **od** i **do** — każde z dopiskiem `exact`/`about` i rokiem/miesiącem/dniem, każde może być puste · **poziom** `country` · `locality` · `address` ·
   **miejsce w wierszu, słowami**: nazwa dziś, jednostka 1. rzędu, kraj (kod i nazwa polska), punkt, id GeoNames · **nazwa z tamtego czasu** (N2) ·
   **adres** jako tekst, punkt zostaje w środku miejscowości (A1). Dwa `CHECK`: adres ⇔ poziom `address`; kraj ⇔ brak id GeoNames. Bez twierdzeń (D28).
2. **Zapis z „Zapisz” wpisu osoby, w jego transakcji** (`AlsoWrite`, jak zdjęcia) — nieudany zapis nie zostawia ani osoby, ani zamieszkań.
3. **Koniec bez „Do” wyliczany przy odczycie** (D12): zamieszkanie z „Od” i bez „Do” kończy się „Od” najbliższego o późniejszym początku; wpisane „Do”
   wygrywa. **Nie zapisuje się go** — w bazie zostaje to, co podało źródło; widok, karta i mapa liczą ten sam koniec (`impliedEnds`).
4. **Lista miejsc** (kraje i miejscowości z punktami — GeoNames CC BY 4.0, Natural Earth) jest **assetem aplikacji budowanym na PC i trzymanym poza
   gitem** (`*.db` z bloku danych rodziny, G1); w aplikacji kopiowana do `places/` obok danych, **poza kopią zapasową**.

## Options considered
| Opcja | Za | Przeciw | Wynik |
|---|---|---|---|
| **R1 — `residences`, miejsce w wierszu** | jedna tabela, jedno miejsce zapisu; kopia czyta się bez listy (nazwy słowami); okres `FROM/TO` z dopiskiem przy każdym końcu | nazwy powtórzone przy każdym zamieszkaniu tego samego miejsca | **wybrane** |
| R2 — `residences` + współdzielona tabela `places` | jedno miejsce na wiele zamieszkań; gotowe dla miejsca urodzenia i zgonu | generalizacja przy jednej instancji użycia (reguła: nie przed drugą); kopia potrzebuje złączenia | odrzucone — wraca przy miejscu urodzenia i zgonu ([[zamieszkanie]] *Open* 3) |
| R3 — `events` z typem `residence` | bez nowej tabeli; typ na końcu enumu bez migracji | jeden dopisek na parę dat, a „między” = `BET`, nie okres; miejsce tylko tekstem — zmiana `events` i tak potrzebna | odrzucone |
| Koniec zapisany przy „Zapisz” (zamiast pkt 3) | koniec widoczny w bazie wprost | fakt, którego nikt nie podał; nieaktualny po dołożeniu zamieszkania pomiędzy | odrzucone (decyzja autora na stopie #2) |
| Lista w repo + wyjątek strażnika (zamiast pkt 4, G2) | build z czystego klonu bez kroku | nazwy wszystkich miejscowości, także z listy rdzeni, w publicznym repo; dziura w jedynej ochronie publikacji | odrzucone |

## Consequences
- **Na czystym klonie** przed pierwszym `flutter test`/`build` trzeba zbudować listę (`tool/places/build_places.dart`, README → *Lista miejsc*).
- **Dwa domy naraz** (np. studia w innym mieście) wymagają wpisanego „Do” przy jednym z nich — inaczej pierwszy kończy się początkiem drugiego.
- **Mapa pól GEDCOM na później** (eksport GEDCOM poza MVP): zamieszkanie → `RESI` z `DATE FROM … TO …` (`ABT` przy „około”); miejsce → `PLAC` (nazwa,
  jednostka, kraj) + `MAP` (`LATI`/`LONG` z punktu); nazwa z tamtego czasu → `PLAC` z czasu zdarzenia, dzisiejsza w notatce albo `PLAC.FORM`; adres →
  `ADDR`; koniec wyliczony (pkt 3) nie trafia do eksportu — eksportuje się to, co zapisane.
- Nowa wersja listy (nowy zrzut GeoNames) = nowa wersja aplikacji; zapisane zamieszkania się nie zmieniają, bo mają miejsce słowami.

## Follow-ups
