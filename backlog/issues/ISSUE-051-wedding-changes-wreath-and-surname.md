---
title: "ISSUE-051 — A wedding and the end of a union change the wreath and the surname in that year"
type: issue
status: draft
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "`/pm` 2026-10-19 — dwa pomysły autora w jednej wiadomości (wieniec po ślubie i po rozwodzie · „aktualizacja nazwisk”), połączone przez `pm` w jedną pozycję; autor: *„w ramach tej sesji chciałbym tylko, abyś stworzył to zadanie”*"
created: 2026-10-19
updated: 2026-10-19
---

# ISSUE-051 — Ślub i koniec związku zmieniają wieniec i nazwisko

> Autor 2026-10-19 w `/pm`: *„chciałbym, aby kobieta, która dopiero się rodzi, miała swój »rodowy wieniec«, natomiast dopiero po ślubie dostała
> »dzielony«; dodatkowo po rozwodzie wróciłaby do swojego pierwotnego wieńca”* oraz *„jeżeli kobieta wychodzi za mąż, jej nazwisko się zmienia
> (domyślnie na męża, ale nie zawsze) — dla osób, które są już zmarłe, to nie będzie problem. Ale dla osób nowych, które planują się pobrać za kilka
> lat, chciałbym mieć to zaopiekowane w funkcjonalnościach”*.

## Why one item, not two
Oba pomysły to ta sama rzecz piętro niżej: **ślub i koniec związku zmieniają, kim osoba jest w danym roku** — jaki ma wieniec i jakie nazwisko. Te
same zdarzenia, to samo okno ([[rodzina]]: „Ślub”, „Koniec związku”), ten sam suwak czasu ([[drzewo]]). Widać to już w [[ISSUE-050-next-event]]:
podpis „Urodziła się …” bierze dzisiejsze nazwisko (`tree_events.dart` → `surname`), więc w roku urodzin kobieta ma nazwisko po mężu, a jej wieniec
na suwaku jest pół na pół od urodzenia.

## Decisions this changes — on purpose
1. **[[wieniec]] B7** — „koniec związku („//”) i suwak czasu nie zmieniają wieńca: liczy się ostatnie małżeństwo z drzewa” (zasada `ui` przyjęta z
   rekomendacją w [[ISSUE-044-family-wreaths]]). Autor ją odwraca.
2. **[[wieniec]] B4** — „ród męża z **ostatniego** małżeństwa” → z małżeństwa trwającego w danym roku (`ui` sprawdza brzmienie).

## What to build
### 1. Wieniec w danym roku
- przed ślubem — wieniec swojego rodu (B3 na całość);
- od roku ślubu — pół na pół ([[wieniec]] D14, Ś3);
- po końcu związku (rozwód, rozstanie) — znowu swój;
- **owdowienie zostawia pół na pół**: w modelu to zgon męża, nie koniec związku ([[rodzina]] D7);
- powtórny ślub — prawa połowa z rodu drugiego męża;
- „rok” to na drzewie i w trybie prezentacji rok suwaka; bez suwaka (portret w [[osoba]], węzły na „dziś”) — stan dzisiejszy, czyli rozwiedziona ma
  swój wieniec;
- liczone z dat związku, **bez zapisu**. Ślub bez daty i koniec bez daty — do `ui` (dziś B4 bierze „później zapisane”).

### 2. Nazwisko po ślubie i po końcu związku
- **Przy dodaniu ślubu** ([[rodzina]] — kreator i poprawa) pytanie o nazwisko po ślubie, **dla obojga**. Prawo daje więcej niż „męża albo swoje”
  ([art. 25 KRO](https://e-prawnik.pl/artykuly/czy-moge-zmienic-nazwisko-po-slubie-opinia-prawna.html)): małżonkowie mogą przyjąć wspólne nazwisko
  jednego z nich (także żony), zachować swoje albo połączyć je z nazwiskiem drugiego (najwyżej dwa człony); bez oświadczenia każde zostaje przy swoim.
  Podpowiedź domyślna według autora: kobieta przyjmuje nazwisko męża.
- **Przy końcu związku** pytanie, czy osoba wraca do nazwiska sprzed ślubu
  ([art. 59 KRO](https://czasopismo.legeartis.org/2015/12/powrot-do-poprzedniego-nazwiska-po-rozwodzie/)): wrócić może tylko ten, kto zmienił nazwisko,
  w 3 miesiące od uprawomocnienia rozwodu, i nie musi.
- **Na suwaku i w podpisach ⏭** ([[ISSUE-050-next-event]]): przed ślubem nazwisko rodowe, po — obecne.
- Dla kogo: **żyjące osoby, które pobiorą się za kilka lat**. U zmarłych nazwisko i „z d.” są wpisane i nic się nie zmienia (autor).

## Recommendation from `pm` (2026-10-19, bez decyzji autora)
- **Bez zmiany bazy:** wybór przy ślubie zapisuje się w obecnym `surname`, `birth_surname` zostaje ([[FR-005-nazwisko-rodowe]] — dwa pola: rodowe i
  obecne). Bez migracji, bez zmiany kopii.
- **Kolejka: po instalacji, jako pierwsza aktualizacja ze sklepu** — pozycja nie zmienia bazy, więc według zasady terminu może przyjść później
  (`CURRENT_STATE.md` → *In progress*, „Zasady terminu”); śluby, o których myśli autor, są za kilka lat; do 2026-10-29 są jeszcze
  [[ISSUE-050-next-event]], retro 5, [[NT-007-hand-over-note]] i [[ISSUE-032-mvp-install]].
- ⚠️ OPEN — **miejsce w kolejce:** autor nie odpowiedział na pytanie `pm` *„na wyjeździe czy pierwszą aktualizacją po instalacji?”* (2026-10-19 —
  w tej sesji tylko zapis pozycji). `pm` pyta przy starcie pozycji, zanim ruszy `ui`.
- Koszt: ok. 1–1,5 dnia łańcucha (`ui` → `planning` → `dev` → `qa`).

## What this will not give
- **Jeśli pozycja przyjdzie po instalacji:** na wyjeździe ⏭ i suwak dalej pokażą nazwisko po mężu i wieniec pół na pół już w roku urodzin — jak
  dziś w [[ISSUE-050-next-event]]. Przy opowiadaniu rodzinie na telewizorze może to zostać wyłapane.
- **Nazwiska z pierwszego małżeństwa** kobiety, która brała ślub dwa razy: dwa pola trzymają tylko początek (rodowe) i koniec (obecne).
  *Obali:* w notatkach jest taka kobieta i jej środkowe nazwisko jest dla autora ważne → nazwisko przy każdym ślubie (np. w rodzinie) — **zmiana
  bazy**, a według zasady terminu ta idzie przed instalację; pozycja wraca wtedy do `pm` przed [[ISSUE-032-mvp-install]]. Pytanie do autora, nie do
  notatek (agenci nie czytają `family_data_dir` bez prośby).

## Prior art
- **[GEDCOM 7](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html):** osoba ma dowolnie wiele nazwisk (`PERSONAL_NAME_STRUCTURE {0:M}`,
  pierwsze — preferowane), każde z typem: `BIRTH` („nadane przy urodzeniu lub blisko niego”), `MAIDEN` („nazwisko przed pierwszym ślubem”),
  `MARRIED` („przyjęte przy ślubie”). **Nazwisko nie ma daty** (`PERSONAL_NAME_STRUCTURE` bez `DATE`) — datę daje zdarzenie. Dwa pola Grobing to
  `BIRTH`/`MAIDEN` i ostatnie `MARRIED`, więc eksport GEDCOM (C2) zostaje tani ([[FR-005-nazwisko-rodowe]] → *Why durable*).
- **Prawo polskie** — KRO art. 25 i 59 (wyżej): wybór przy ślubie dotyczy obojga, powrót po rozwodzie jest dobrowolny.
- **Rama:** genealogia oddziela osobę od jej nazwisk — zapisy z różnych lat znają tę samą kobietę pod różnymi nazwiskami, a nazwisko nadpisane „na
  dziś” to gubi.

## Acceptance Criteria (propozycja `pm` — do potwierdzenia przez `ui` i `planning`)
- **AC-1** *Given* Anna Zmyślona, ślub z Józefem Wymyślskim w 1952 *When* suwak stoi na 1940 *Then* wieniec Anny jest cały w jej rodzie; *When*
  suwak stoi na 1960 *Then* pół na pół.
- **AC-2** *Given* to małżeństwo z końcem w 1970 *When* suwak stoi na 1975 albo otwieram widok Anny *Then* jej wieniec znowu jest cały w jej rodzie;
  *Given* zamiast końca zgon Józefa w 1970 *Then* zostaje pół na pół.
- **AC-3** *Given* żyjąca Ewa Testowa *When* dodaję jej ślub z Piotrem Przykładowskim *Then* aplikacja pyta o nazwisko po ślubie obojga, z podpowiedzią,
  że Ewa przyjmuje nazwisko męża; po wyborze jej nazwisko to „Przykładowska”, a nazwisko rodowe „Testowa”.
- **AC-4** *Given* osoba, która zmieniła nazwisko przy ślubie *When* dodaję koniec związku *Then* pytanie, czy wraca do nazwiska sprzed ślubu;
  „nie” zostawia obecne.
- **AC-5** *Given* suwak przed rokiem ślubu Anny *When* ⏭ pokazuje rok jej urodzin *Then* podpis brzmi „Urodziła się Anna Zmyślona”; po roku ślubu
  osoba ma nazwisko obecne.

## Notes
- **Ekrany (`ui` → `planning`):** [[wieniec]] (B4, B7, *States*), [[rodzina]] (pytanie przy ślubie i przy końcu związku), [[drzewo]] (wieniec i podpis
  w roku suwaka), [[wpis-osoby]] (pola „Nazwisko” i „Nazwisko rodowe (z domu)”), [[osoba]] (portret „dziś”), [[mapa-migracji]] — jeśli pokazuje
  nazwiska.
- **Nazwisko nie zmienia rodu:** ród jest wybrany przy osobie, a nie liczony z nazwiska ([[ADR-021-clans-choice-at-the-person]] — M3 „ród z nazwiska”
  odrzucone). Mąż, który przyjmie nazwisko żony, zostaje w swoim rodzie, a jego dzieci dziedziczą jego ród (B6).
- **Forma żeńska nazwiska męża:** -ski → -ska, -cki → -cka, -dzki → -dzka; nazwisko bez formy żeńskiej („Wymyślak”) bez zmiany. Do `ui`: aplikacja
  odmienia sama czy podpowiada formę do poprawy.
- **„Razem” (bez ślubu)** nie zmienia ani wieńca, ani nazwiska — jak dziś B4 (tylko małżeństwo). `ui` potwierdza.
- **Nazwisko w roku przy dwóch zmianach** (ślub, rozwód z powrotem, drugi ślub) — z dwóch pól da się wyliczyć tylko „przed pierwszym ślubem” i „po
  ostatniej zmianie”; środek do decyzji `ui` (np. obecne od pierwszego ślubu).
- **`TRACEABILITY.md`** — wiersz przy starcie pozycji (`planning`). 2026-10-19 plik był w edycji sesji [[ISSUE-050-next-event]], więc ta pozycja go nie
  dotknęła.
