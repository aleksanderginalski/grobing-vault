---
title: "ADR-022 — Deleting what was added: rows deleted with a snapshot, \"Cofnij\" for a few seconds, no bin"
type: adr
status: accepted
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-053-delete-cemetery-grave-person]]"
source: "plan `planning` (mechanizm H) i stop #1 runda 2 ISSUE-053 (autor: „tak K2 4s”, 2026-10-23) · brief §5 G7 → C5 (*„Undo / no silent deletion … or an architecture property (soft delete)”*) · zasada autora *„wszystko, co można dodać, można też usunąć”* ([[style-b]] reguła 16)"
created: 2026-10-23
updated: 2026-10-23
---

# ADR-022 — Usuwanie: wiersze usunięte z migawką, „Cofnij” przez kilka sekund, bez kosza

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-23: mechanizm H w planie [[ISSUE-053-delete-cemetery-grave-person]], stop #1 runda 2 — autor: *„tak K2 4s”* (pasek „Cofnij” przez 4 s).

## Context
Po instalacji MVP autor wpisuje prawdziwe dane i pyta, jak usunąć pomyłkę (`/pm` 2026-10-23). Do tej pory w aplikacji nie dało się usunąć cmentarza,
grobu, osoby, pochówku, pinezki ani rodu; brief odłożył to jako C5 (G7: *„a mis-tap at the cemetery must not erase a person”*, Could) i zostawił otwarte,
czy rozwiązać to oknem, czy własnością architektury (*soft delete*). Autor chce zasady *„wszystko, co można dodać, można też usunąć”* w całości przed
wyjazdem, a przy grobie i cmentarzu — żeby **osoby nie znikały**, tylko traciły grób. Dane są niezastąpione, a kopia w tle po ok. 10 min ciszy nadpisuje
plik na Dysku stanem już po usunięciu ([[ADR-004-backup-format-encryption-destination]], [[ADR-018-export-is-the-backup]]).

## Decision
1. **Usunięcie kasuje wiersze w jednej transakcji i zwraca migawkę** (`lib/data/deletion.dart`): każdy usunięty wiersz z jego `id` i każdy wiersz
   zmieniony w miejscu (pinezka, `persons.clan_id`, zdjęcie grobu, na którym ktoś jest). Bez zmiany schematu (v15).
2. **„Cofnij” wstawia migawkę z powrotem** w jednej transakcji, w kolejności kluczy obcych (rodzice przed dziećmi), z tymi samymi `id`, i zapisuje
   zmienione wiersze takimi, jakie były — przez drift, więc ekrany i kopia w tle widzą zmianę. Po „Cofnij” odcisk danych jest ten sam co przed usunięciem.
3. **Pasek „Cofnij” przez 4 s** (K2, decyzja autora), dłużej, gdy prosi o to „Czas na działanie”; przy czytniku ekranu nie znika sam (SC 2.2.1). Przed
   usunięciem okno mówi, co zniknie i co zostaje ([[style-b]] reguła 16).
4. **Osoby nigdy nie znikają z grobem ani z cmentarzem** — tracą pochówek (grob D28, cmentarze D40). Usunięcie osoby zabiera to, co jej: zdarzenia,
   pochówki, „źródła”, zamieszkania, łącza do zdjęć i zdjęcia, na których nie ma nikogo innego; związek, któremu brakuje partnera albo dwóch osób, znika
   cały (jak „Usuń związek”). „Ja” się nie usuwa.
5. **Pliki zdjęć zostają na dysku do najbliższego sprzątania** (przy kopii i przy starcie — `sweepOrphanMedia`), więc „Cofnij” znajduje je na miejscu.
6. **„Cofnij” odmawia, gdy osoba z migawki leży już w innym grobie** (`RestoreRefused`) — nikt nie leży w dwóch grobach ([[grob]] D23).

## Options considered
| Opcja | Co | Za | Przeciw |
|---|---|---|---|
| **N** — samo okno „Usunąć …?” (K1) | jak dziś „Usuń związek” | najprostsze | okno klika się z przyzwyczajenia; po pomyłce zostaje odtworzenie całej kopii, a kopia w tle po 10 min ma już stan po usunięciu |
| **H** — usunięcie + migawka + „Cofnij” ✅ | jak wyżej | bez zmiany schematu; każde zapytanie aplikacji zostaje, jakie było; pomyłkę naprawia jedno dotknięcie | odzysk tylko przez sekundy; dalej — kopia |
| **S** — kosz (*soft delete*, sugestia briefu C5) | `deleted_at` w sześciu tabelach, filtr w każdym zapytaniu, ekran kosza | odzysk po dniach | migracja przed wyjazdem; każde zapytanie, które zapomni filtra, pokaże usuniętą osobę na drzewie albo w nazwie pokrewieństwa; kopia niesie usunięte dane |
| **T** — tabela kosza (wiersze przenoszone do osobnej tabeli albo JSON) | odzysk po czasie bez filtrów | zapytania bez zmian | nowa tabela i format do kopii; „przywróć” musi znać kolejność kluczy, tak jak H, ale po dniach, gdy reszta danych mogła się zmienić |

## Consequences
- **Okno ryzyka:** „Zrób kopię teraz” w czasie paska sprząta pliki usuniętych zdjęć — „Cofnij” przywróci wtedy wiersze bez plików (README `grobing-code`
  → *Baza danych*).
- Flutter 3.41 trzyma pasek z akcją do dotknięcia (`SnackBar.persist` domyślnie `true`) — czas trzeba podać jawnie (*Dev report* ISSUE-053).
- Odzysk po upływie paska: tylko odtworzenie kopii z Dysku, zanim kopia w tle zapisze stan po usunięciu.

## Follow-ups
- *Obali:* autor chce odzyskać rzecz po dniu → kosz (S albo T), osobnym ADR.
- „Cofnij” dla usunięć sprzed tej decyzji („Usuń związek”) — kandydat na spójność (ISSUE-053 → *Out of scope*).
