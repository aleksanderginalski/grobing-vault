---
title: "ISSUE-019 — Family relations: a couple and their children entered as one family, each membership with source and status (schema v6)"
type: issue
status: done
delivery-style: task-level
priority: MUST
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
user-story: "[[US-003-przepisanie-rodziny]]"
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-08
verdict-reviewer: self-check
source: "US-003 (AC-1…AC-5, Notes: uwaga autora 2026-10-06) · FR-002 · FR-001 (ziarnistość: twierdzenia na relacjach) · data-model.md (FAMILY_PARTNER / FAMILY_CHILD cited by ASSERTION) · wpis-osoby → Decisions → „Zdjęcie i relacje później”"
created: 2026-10-07
updated: 2026-10-08
---

# ISSUE-019 — Relacje w rodzinie

> Z rozpisania [[US-003-przepisanie-rodziny]] (`docs` w auto-flow, 2026-10-07, po `pm`): **jedna pozycja**, schemat
> i ekran razem, tak jak [[ISSUE-016-photos-grave-and-person]]…[[ISSUE-018-profile-photo-crop]]. Podział nie jest
> decyzją autora. Jeśli na stopie #1 pozycja okaże się za duża, autor może ją podzielić. Uwaga autora z 2026-10-06:
> w formularzu osoby brakuje mu informacji, *„z kim osoba jest związana (pokrewieństwo, powinowactwo)”*.

## What to build
1. **Rodzina naraz:** 1–2 partnerów i ich dzieci w jednym przebiegu. Nowe osoby powstają przy okazji (US-003 AC-1),
   a osobę, która już jest w aplikacji (np. wpisaną przy grobie), wskazuje się zamiast wpisywać ją drugi raz (AC-5).
2. **Powtórne małżeństwo:** osoba jest partnerem w kilku rodzinach, a dziecko należy do pary, nie do jednego
   rodzica (AC-2, [[FR-002-rodzina-jako-rekord]]).
3. **Małżeństwo i koniec rodziny** jako zdarzenia rodziny, z datą z dopiskiem i źródłem (AC-3,
   [[FR-004-data-z-dopiskiem]]).
4. **Źródło i status przy przynależności** partnera i dziecka, domyślnie „notatki” i `CLAIMED` (AC-4,
   [[FR-001-provenance]]). To jest **schemat v6** z migracją v5→v6.
5. **Relacje widać przy osobie.** Kierunek: sekcja „Rodzina” pod biografią w formularzu osoby, z chipami relacji
   jak w R4 ([[wpis-osoby]] → *Decisions* → „Zdjęcie i relacje później”).

**Droga wejścia do rozstrzygnięcia przez `ui` z autorem, przed planem** (US-003 → *Notes*): relacje z formularza
osoby, osobnym arkuszem rodziny (AC-1, *family group sheet* z briefu) czy na oba sposoby. Specyfikacja
[[wpis-osoby]] już nazywa warunek, który obala kierunek z pkt 5: *„US-003 wpisuje rodzinę naraz, w arkuszu
rodziny — wtedy relacje nie trafiają do formularza osoby”*.

## Acceptance Criteria
- [ ] US-003 AC-1: w jednym przebiegu podaję 1–2 partnerów i dzieci, a nowe osoby powstają przy okazji.
- [ ] US-003 AC-2: osoba już będąca partnerem w jednej rodzinie może być partnerem w drugiej. Obie rodziny istnieją,
      a dzieci należą do właściwej pary.
- [ ] US-003 AC-3: datę małżeństwa i końca rodziny wpisuję z każdym z pięciu dopisków.
- [ ] US-003 AC-4: przynależność partnerów i dzieci ma źródło (domyślnie „notatki”) i status.
- [ ] US-003 AC-5: osobę wpisaną przy grobie wskazuję w rodzinie zamiast tworzyć ją drugi raz.
- [ ] Rodzina ma najwyżej dwóch partnerów. Pilnuje tego wprowadzanie, nie baza (`database.dart` → `Families`).
- [ ] Rodzina zapisuje się w całości albo wcale.
- [ ] Migracja v5→v6 zachowuje wszystkie dane. Istniejące przynależności dostają źródło i status (jak dane z v1 w
      migracji v1→v2, [[ADR-006-claimed-value-separate-structures]] D5). Kopia v5 odtwarza się w aplikacji v6. Po
      migracji kopia w tle zamawia się od razu (retro 1, R6).
- [ ] Rodziny z twierdzeniami są w kopii i wracają po odtworzeniu, z odciskiem zgodnym.
- [ ] Ekran stosuje wytyczne stylu B ([[style-b]]).

## Out of Scope
- Widok drzewa i ścieżka „ja → …” → [[EPIC-003-zrozumienie]] ([[SPIKE-002-tree-on-a-phone]]) i [[EPIC-002-wizyta]]
  (M5). Ścieżkę się liczy, nigdy nie zapisuje ([[FR-002-rodzina-jako-rekord]]).
- Wskazanie „ja” → [[EPIC-002-wizyta]] (M5).
- Sprzeczne twierdzenia o relacji → [[US-004-fakt-od-babci]].
- **Relacje dalsze niż rodziny samej osoby** (rodzeństwo, dziadkowie, teściowie, czyli powinowactwo z uwagi autora)
  wynikają z dwóch rodzin albo więcej, więc liczy je ścieżka. To, czy sekcja „Rodzina” pokazuje któreś z nich, ustala
  `ui` z autorem na stopie #1. **Zakres nie poszerza się po cichu.**

## Technical Notes
- **Co już jest w schemacie:** `Families`, `FamilyPartners` i `FamilyChildren` od v1, z kluczem złożonym (rodzina,
  osoba) i bez `id`. Zdarzenia rodziny (małżeństwo, koniec) żyją w `Events` przez `family_id`, z twierdzeniami od
  v2, więc **AC-3 nie zmienia schematu**. `Assertions` cytuje dziś tylko `event_id` albo `burial_id`
  (`CHECK`), więc **AC-4 to schemat v6**. Model v6 rozstrzyga ADR (następny wolny numer) z ≥ 3 opcjami. Diagram w
  `data-model.md` już rysuje FAMILY_PARTNER i FAMILY_CHILD z twierdzeniami (US-003).
- **Kanon dla planu (cytat ze specyfikacji, nie z pamięci):** jak GEDCOM 7, ten sam kanon co ADR-006, ADR-009 i
  ADR-010, przypina źródło do rodziny i do przynależności (`FAM`, `HUSB`/`WIFE`/`CHIL`, `FAMC`/`FAMS`). Do tego
  jak robi to Gramps, z którego prior artu korzysta EPIC-003.
- **Płeć osoby — pytanie przed planem.** `Persons` nie ma płci. Bez niej chip relacji nie powie „ojciec”/„matka”,
  „mąż”/„żona”, „syn”/„córka”, tylko „rodzic”, „partner”, „dziecko”. Uwaga autora mówi o pokrewieństwie i
  powinowactwie, więc to pytanie do `ui` i autora na stopie #1. Nowe pole byłoby częścią v6 (w GEDCOM 7 osoba ma
  `SEX`; planning cytuje specyfikację). Podpowiedź z końcówki imienia byłaby zgadywaniem faktu o osobie
  ([[FR-001-provenance]]).
- **Wskazanie istniejącej osoby (AC-5):** wzorzec listy „Kto jest na zdjęciu?” z
  [[ISSUE-017-person-photos]]: wszystkie osoby, ten grób na górze, filtr.
- **Tempo przepisywania** to miara ekranu: ok. 100 osób z notatek ([[NT-002-transcribe-the-notes]], G6). Liczy się
  w akcjach na rekord, jak w [[wpis-osoby]]. Każde pytanie przy relacji mnoży się przez liczbę dzieci.
- **Transakcja:** zmiany zdjęć osoby zapisują się z „Zapisz” jej wpisu ([[ADR-009-person-photos-record-and-link]]).
  Jeśli relacje wchodzą z formularza osoby, plan mówi, czy idą tą samą transakcją.
- **Dane debug** (`grobing-code/lib/dev/fictional_data.dart`) mają już wymyślone rodziny. Wszyscy wymyśleni noszą
  nazwisko „Wymyślona” (`CURRENT_STATE.md` → *Do retro*), a z relacjami na ekranie widać to wyraźniej.
- Dane do testów i weryfikacji wyłącznie wymyślone (`family-data.md`).

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| [[ISSUE-012-transcribe-grave-screen]] (osoba przy grobie, formularz osoby) | technical | `done` |
| [[ISSUE-017-person-photos]] (lista wszystkich osób z filtrem) | technical | `done` |
| specyfikacja `ui`: droga wejścia relacji, sekcja „Rodzina” w [[wpis-osoby]], makieta przy nowym ekranie | design | do zrobienia przed planem |
| [[SPIKE-002-tree-on-a-phone]] | — | nie blokuje: drzewo jest poza zakresem |

## Definition of Done
Według `DEFINITION_OF_DONE.md` → *ISSUE* (MVP):
- test happy-path dla każdego AC;
- ręczna weryfikacja na emulatorze;
- fakt o rodzinie → źródło i status zapisane;
- zmiana schematu, więc test migracji v5→v6;
- próbne odtworzenie z kopii przechodzi;
- zero danych rodziny w zmianach.

Po przyjęciu tego ISSUE US-003 idzie do werdyktu US.

## Implementation plan
> `planning`, 2026-10-07. **DoR:**
> - jasny zakres ✅;
> - US: [[US-003-przepisanie-rodziny]] ✅;
> - krok ścieżki: n/a — M1 ✅;
> - `task-level` ✅.
>
> **Ekrany** — specyfikacje `ui` z 2026-10-07:
> - [[rodzina]] v1 — **nowe ekrany:** A (arkusz rodziny), B (wybór osoby); decyzje D1–D11, trzy `⚠️ OPEN`;
> - [[wpis-osoby]] v5.1 — 9a „Rodzina” (tylko w poprawie), poprawa osoby bez grobu (4a „Płeć” odrzucone na stopie #1);
> - wytyczne [[style-b]] v1.11 (chip relacji z R4, przycisk segmentowy z R3).
>
> **Makieta:** `makieta-rodzina.html` w katalogu tymczasowym sesji, ramki 1–6. Obowiązują specyfikacje.
>
> **Warstwa danych:**
> - zmiana schematu v5→v6 (`addColumn` i przebudowa dwóch tabel) z testem migracji;
> - odtworzenie kopii v5 w aplikacji v6;
> - kopia z rodzinami odtworzona z odciskiem zgodnym, w teście i na drugim emulatorze;
> - kopia w tle zaraz po migracji (R6).
>
> **Źródło faktu:** relacja to fakt o rodzinie, więc twierdzenie „notatki”, `CLAIMED` (AC-4, [[FR-001-provenance]]).
> Płci w aplikacji nie ma (decyzja autora na stopie #1).

### Prior art (sources, not memory)
- **[GEDCOM 7.0.18](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html)**, odczyt 2026-10-07:
  - `FAMILY_RECORD`: pod `HUSB`, `WIFE` i `CHIL` stoi tylko `+2 PHRASE`, **bez cytowania źródła**. Cytowanie
    (`+1 <<SOURCE_CITATION>> {0:M}`) stoi przy całym rekordzie `FAM`;
  - pod `FAMC` i `FAMS` osoby też nie ma `SOUR`. `FAMC` ma `STAT`: *„assessing of the state or condition of a researcher's
    belief in a family connection”* (`CHALLENGED` · `DISPROVEN` · `PROVEN`) i `PEDI` (`BIRTH` · `ADOPTED` · `FOSTER` ·
    `SEALING` · `OTHER`);
  - *„Source citations and notes related to the start of a specific child relationship should be placed under the child's
    BIRT, CHR, or ADOP event, rather than under the FAM record”*;
  - *„The order of the CHIL (children) pointers within a FAM (family) structure should be chronological by birth”* oraz
    *„A FAM record should not have multiple CHIL substructures pointing to the same INDI”*;
  - *„Sex, gender, titles, and roles of partners should not be inferred based on the partner that the HUSB or WIFE
    structure points to”*;
  - `SEX`: `M` · `F` · `X` (*„Does not fit the typical definition of only Male or only Female”*) · `U` (*„Cannot be
    determined from available sources”*);
  - sama specyfikacja: *„The structures for representing the strength of and confidence in various claims are known to be
    inadequate and are likely to change in a future version”* i *„The FAM record will be revised in a future version”*.
- **Gramps** (kod źródłowy `gramps-project/gramps`, gałąź `master` 6.1.0-dev, odczyt 2026-10-07; wiki i dokumentacja
  zwróciły 403):
  - `ChildRef(…, CitationBase, NoteBase, RefBase)` — *„A class for tracking information about how a child relates to their
    parents”*: **łącze dziecka ma własne cytowania** i osobny rodzaj relacji do ojca i do matki (`BIRTH` domyślnie,
    `ADOPTED`, `STEPCHILD`, `FOSTER`…);
  - `Family(CitationBase, …)` — cytowania przy rodzinie; partnerzy to `father_handle` i `mother_handle`, bez własnych
    cytowań;
  - płeć osoby: `FEMALE` · `MALE` · `UNKNOWN` (domyślna) · `OTHER`.
- **Kod `grobing-code`**, odczyt 2026-10-07:
  - `restore_service.dart:254-264` — po migracji **liczba wierszy każdej tabeli z manifestu musi być równa** (`count !=
    table.value` → odmowa). Migracja może przebudować tabelę, ale nie może dodać do niej wierszy;
  - `data_state.dart:54-69` — odcisk danych czyta tabele z `sqlite_master` i kolumny z `PRAGMA table_info`, więc nowe
    kolumny wchodzą do odcisku bez zmian w kodzie;
  - `database.dart:153` — `assertions` ma `CHECK` na dwóch kolumnach, więc nowy cel twierdzenia to przebudowa tabeli
    (wzorzec `TableMigration` z v3→v4);
  - **wiersze `families` pisze dziś tylko `lib/dev/fictional_data.dart`** (dane debug). Formularza rodziny nie było, więc w
    buildzie release przed v6 rodzin nie ma;
  - `graves.dart:563-607` — `loadPersonChoices` (lista osób z grobem albo cmentarzem dla „Kto jest na zdjęciu?”);
    `graves.dart:421` — `AlsoWrite` dołącza zapis do transakcji wpisu;
  - `person_form_screen.dart:818-899` — `_DateInput` i `_DateBlock` są prywatne w formularzu osoby; arkusz potrzebuje
    tego samego bloku.
- **Pomiar podpowiedzi płci** (dla `⚠️ OPEN` 2) — lista imion PESEL, dane.gov.pl, stan na 20.01.2026 (zbiór 1667 — osoby
  żyjące; zbiór 1501 — żyjące i zmarłe; zmarłe = różnica). Reguła „pierwsze imię na „-a” → kobieta, inne → mężczyzna”:
  - **osoby zmarłe: 0,066%** pomyłek (10 168 z 15,45 mln). Mężczyźni wzięci za kobiety: Kuba, Bonawentura, Dyzma,
    Kosma, Jarema, Kuźma, Barnaba. Kobiety wzięte za mężczyzn to głównie imiona niemieckie (Margot, Irmgard, Ingrid,
    Ruth, Hildegard);
  - osoby żyjące: 0,97% — głównie imiona napływowe (Mykola, Illia, Nikita) i Kuba;
  - **granice:** rejestr PESEL ma mało osób zmarłych przed jego powstaniem (niesprawdzone na stronie zbioru), więc
    najstarsze groby są niedoreprezentowane; imion występujących raz w zbiorach nie ma. Pliki i skrypt leżą w katalogu
    tymczasowym sesji, poza repo.

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego · co ją obali |
|---|---|---|---|
| **O1** | **Droga wejścia relacji** ([[rodzina]] → *Open* 1) | **C: widok w formularzu osoby (9a), wpisywanie arkuszem rodziny** | kanon briefu (*family group sheet*) i [[FR-002-rodzina-jako-rekord]] mówią „rodziną naraz”, a R4 i twoja uwaga — „przy osobie”. **A** (relacje po jednej z formularza osoby) wymaga zmiany FR-002 i pytania „z którą parą?” przy powtórnym małżeństwie. **B** (sam arkusz z widoku grobu) nie pokazuje relacji przy osobie. *Obali:* arkusz na stopie #2 wydaje się wolniejszy niż relacje po jednej |
| **O2** | **Płeć osoby** ([[rodzina]] → *Open* 2) | **P1: pole „Płeć” (4a), podpowiedziane z imienia, z krótką listą wyjątków z pomiaru** (Kuba, Bonawentura, Dyzma, Kosma, Jarema, Kuźma, Barnaba → mężczyzna) | nazwy relacji jak w R4 („Mąż: Jan”, „Córka: Anna”) i jak ścieżka z R3. **Pomiar:** wśród zmarłych reguła myli się u 0,066% osób, czyli przy ok. 100 osobach z notatek najpewniej ani razu, a zła podpowiedź jest widoczna od razu. **P1'** (bez podpowiedzi): +1 dotknięcie na osobę. **P2** (bez płci): nazwy neutralne („Rodzic”, „Małżonek”), a płeć i tak wróci z drzewem i ścieżką (EPIC-003, M5), wtedy z migracją i uzupełnianiem ok. 100 osób. *Obali:* w notatkach są imiona spoza reguły częściej niż raz na sto |
| **O3** | **Rodzeństwo w 9a** ([[rodzina]] → *Open* 3) | **tak**; teściowie, dziadkowie i dalsi — nie (to ścieżka M5) | rodzeństwo to inne dzieci tej samej rodziny rodziców: bez nowych danych i bez wpisywania. *Obali:* sekcja z rodzeństwem robi się za długa przy dużych rodzinach |
| **D1** | **Gdzie stoi twierdzenie o relacji, schemat v6** (→ ADR-011) | **(a) przy rodzinie (związek pary) i przy każdym łączu dziecka**: `assertions.family_id` i `assertions.family_child_id`; `family_children` dostaje `id` | Łączy oba kanony: GEDCOM cytuje przy `FAM` (para), a Gramps przy łączu dziecka (`ChildRef`). GEDCOM ma też `FAMC.STAT` (`PROVEN`/`DISPROVEN`), czyli status relacji jednego dziecka. Spór „to nie było ich dziecko” ([[US-004-fakt-od-babci]]) dotyczy jednego dziecka, a nie całej rodziny. Inny partner to inna rodzina (osobny wiersz, [[ADR-006-claimed-value-separate-structures]] D1). *Obali:* przypadek, w którym źródło potwierdza jednego partnera, a drugiemu przeczy, w tej samej rodzinie |
| | opcja (b) | twierdzenie przy **każdym** łączu: partnera i dziecka (`family_partners` też dostaje `id`) | dosłownie [[ADR-006-claimed-value-separate-structures]] D6. Para to jednak jeden fakt („byli parą”), a nie dwa, i żaden kanon nie cytuje przy samym partnerze. Druga przebudowa tabeli bez zysku. Zostaje, gdyby D1 (a) obalił przypadek wyżej |
| | opcja (c) | tylko przy rodzinie (GEDCOM 1:1) | najprostsza, ale nie umie zakwestionować jednego dziecka (US-004) — **odrzucona** |
| | opcja (d) | dziecko przez zdarzenie urodzenia z `FAMC` (zalecenie GEDCOM) | miesza źródło daty urodzenia ze źródłem rodziców; dziecko bez daty potrzebowałoby pustego zdarzenia; `events` ma `CHECK` „osoba albo rodzina” — **odrzucona** |
| | opcja (e) | jedna tabela `family_members` zamiast dwóch | migracja usuwa tabele, a odtworzenie kopii v5 liczy wiersze każdej tabeli z manifestu ([[NFR-003-migracje-schematu]]) — **odrzucona** |
| **D2** | **Płeć w schemacie** (przy O2 = P1) | `persons.sex` — tekst `female` / `male`, **pusty = nieznana** (`U` w GEDCOM) | jak inne pola osoby: puste znaczy „nie wiem”. `X` z GEDCOM nie ma przypadku w notatkach, a wartość tekstową da się dodać bez migracji. Płeć stoi przy osobie, a nie przy miejscu w parze, zgodnie z GEDCOM („should not be inferred based on … HUSB or WIFE”) |
| **D3** | **Relacje sprzed v6: migracja nie dopisuje im twierdzeń** | tak | Dopisanie wierszy do `assertions` złamałoby odtworzenie każdej kopii v5 z rodzinami (`restore_service.dart:254-264`). Rodziny przed v6 powstawały tylko z danych debug, więc w buildzie release ich nie ma. Twierdzenie dostaje relacja przy pierwszym zapisie w arkuszu. Inaczej niż v1→v2 ([[ADR-006-claimed-value-separate-structures]] D5): tam `assertions` była nową tabelą. *Obali:* rodzina w buildzie release v5 (nie ma drogi, która by ją zapisała) |
| **D4** | **Kolejność dzieci** — zmiana [[rodzina]] D10 według kanonu | w 9a i przy otwarciu arkusza **według urodzenia**, a bez daty na końcu, w kolejności dodania. Podczas edycji arkusza nowy wiersz zostaje tam, gdzie go dodano | GEDCOM: *„chronological by birth”*. D10 bronił tylko tego, żeby wiersze nie skakały w trakcie wpisywania, i to zostaje. Po „tak” `ui` poprawia D10 w specyfikacji |
| **D5** | **Pozostałe decyzje projektowe `ui`** (pakiet) | przyjąć | arkusz zapisuje się sam (D1) · otwiera się z formularza w poprawie (D2) · najpierw szukaj, potem twórz, +1 dotknięcie na nową osobę (D3) · nowa osoba w arkuszu to imiona i nazwisko (D4) · dziecko ma jedną rodzinę rodziców (D5) · rodzina potrzebuje osoby w parze (D6) · „Koniec związku” schowany (D7) · wiersze arkusza nie prowadzą do wpisu (D11) · chip prowadzi do wpisu krewnego ([[wpis-osoby]] D-rodzina-2) |
| **D6** | **„Usuń rodzinę”** ([[rodzina]] D8) — **spoza AC** | tak, z oknem | bez tego pomyłkowo utworzonej rodziny nie da się usunąć. Osoby zostają, znikają tylko powiązania i daty ślubu i końca. *Obali:* wolisz bez usuwania, jak przy osobie (brief G7/C5) |
| **D7** | **Wielkość pozycji** | **jedna**, jak ISSUE-016…018 | Alternatywa jak przy US-002: ISSUE-019 to schemat v6 i warstwa danych (sprawdza agent), a ISSUE-020 to ekrany. Dwa commity i dwa razy stop #2, ale mniejsze paczki. *Obali:* wolisz mniejsze paczki |

### Stop #1 — odpowiedź autora (2026-10-07)
- **O1:** „ok”, z uwagą: *„może być tak, że ktoś był z kimś w danym okresie, a następnie się rozstali lub owdowieli i
  mieli nowe związki i dzieci”*. Model to obsługuje z konstrukcji: każdy związek to osobna rodzina z własnymi dziećmi,
  datą ślubu i datą końca (AC-2, AC-3), a owdowienie to zgon partnera. Skutek dla ekranu (`ui`, [[rodzina]] v1.1,
  [[wpis-osoby]] v5.1): **„Związek”** i **„Dodaj związek”** zamiast „Małżeństwo”, chip „Partner”, a linia przy końcu
  mówi o rozwodzie, rozstaniu i owdowieniu.
- **O2:** *„nie czuję potrzeby”* i **D2:** *„nie czuję potrzeby dawania płci”* → **bez płci**: bez pola 4a, bez kolumny
  w schemacie, nazwy relacji neutralne („Rodzic”, „Partner”, „Dziecko”). Pomiar PESEL zostaje w *Prior art* na wypadek,
  gdyby płeć wróciła z drzewem i ścieżką (EPIC-003).
- **O3:** *„na ten moment raczej nie trzeba — w wizualizacjach połączeń rodziny będziemy to mieli”* → **bez rodzeństwa**
  w 9a.
- **D1:** „ok” — twierdzenie przy rodzinie i przy łączu dziecka.
- **D3:** *„na razie to dummy data, więc nic się nie dzieje”* — migracja nie dopisuje twierdzeń.
- **D4:** „według daty urodzenia”.
- **D5, D6, D7:** „ok” — pakiet decyzji `ui`, „Usuń rodzinę”, jedna pozycja.

### Falsifier — what is measured and what is not
| # | Pytanie | Wynik |
|---|---|---|
| F1 | Czy migracja v5→v6 zachowuje wszystkie dane? | **Zmierzy** test: wymyślona baza v5 z dwiema rodzinami (jedna osoba w obu — powtórne małżeństwo), ślubem z twierdzeniem, zdjęciami i kadrem → v6: te same wiersze i `id` we wszystkich tabelach, `family_children.id` nadane, twierdzenia bez zmian, `PRAGMA foreign_key_check` pusty |
| F2 | Czy kopia v5 z rodzinami odtwarza się w v6? | **Zmierzy** test odtworzenia na kopii v5 zrobionej kodem testowym (wzorzec F3 z ISSUE-018). To ten test pilnuje D3 |
| F3 | Czy rodziny z twierdzeniami są w kopii i wracają z odciskiem zgodnym? | **Zmierzy** test (kopia v6 → odtworzenie → równe wiersze i odcisk) i **agent** na emulatorach: nowe hasło testowe, kopia z `Medium_Phone` → odtworzenie na `Grobing_Restore` |
| F4 | Czy zapis rodziny jest całością? | **Zmierzy** test: błąd wstrzyknięty po zapisie nowej osoby, a przed zapisem łącza → w bazie nic z arkusza |
| F5 | Czy niezmienniki trzyma warstwa danych, nie tylko ekran? | **Zmierzy** test danych: odmowa przy trzech osobach w parze, rodzinie bez pary, jednej osobie, tej samej osobie dwa razy w rodzinie, dziecku z drugą rodziną rodziców |
| F6 | Czy podpowiedź płci trafia? | ✅ **zmierzone** na liście PESEL (*Prior art*): 0,066% pomyłek wśród zmarłych. **Nieużyte** — autor wybrał wariant bez płci (O2) |
| F7 | Czy przed v6 jakaś droga w buildzie release zapisuje rodziny (D3)? | ✅ **z kodu:** zapis do `families`, `family_partners` i `family_children` jest tylko w `lib/dev/fictional_data.dart` |
| F8 | Odczucie: arkusz, wybór osoby z klawiaturą od wejścia, chipy z nazwami neutralnymi | **Nie zmierzone** — autor na stopie #2 |
| F9 | Tempo rodziny (ok. 20 akcji na 5 osób, [[rodzina]] → *Tempo*) | **Nie zmierzone** — liczone ze specyfikacji; prawdziwe tempo pokaże przepisywanie ([[NT-002-transcribe-the-notes]]) |

### Scope diff vs the item
- **zakres według pozycji:** AC-1…AC-5, schemat v6, zapis całością, najwyżej dwie osoby w parze — bez zmian.
- ~~**+ płeć osoby** (O2)~~ i ~~**+ rodzeństwo w 9a** (O3)~~ — **odrzucone na stopie #1**, nie wchodzą.
- **+ „Usuń rodzinę”** (D6) — spoza AC, przyjęte na stopie #1.
- **± słowo „związek”** zamiast „małżeństwo” — z uwagi autora do O1, bez zmiany zakresu.
- **+ poprawa osoby bez grobu** — wynika z AC-1: osoba dodana arkuszem nie ma grobu, a musi mieć wejście do wpisu.
- **± kolejność dzieci według urodzenia** (D4) — kanon zamiast D10 `ui`.
- **+ wspólny blok daty** — wyjęty z formularza osoby, bo arkusz potrzebuje tego samego.
- **bez zmian:** widok grobu, zdjęcia, kopia, brak `INTERNET`, styl B.

### Steps (dev)
0. **Przed zmianą:** na `Medium_Phone` jest build release v5 z wymyślonymi osobami i zdjęciami (stan po ISSUE-018).
   **Nie odinstalowuj** — aktualizacja na tych danych to sprawdzenie migracji na urządzeniu (`qa`).
1. **Schemat v6** — `lib/data/database.dart`:
   - a. ~~płeć osoby~~ — **nie wchodzi** (stop #1: bez płci);
   - b. `FamilyChildren`: `id` autoincrement i UNIQUE (`familyId`, `personId`) w miejsce klucza złożonego;
   - c. `Assertions`: `familyId` i `familyChildId` (opcjonalne klucze obce); `CHECK` — dokładnie jedno z czterech:
     `event_id`, `burial_id`, `family_id`, `family_child_id`. Komentarz: D1 i cytaty GEDCOM i Gramps;
   - d. `currentSchemaVersion = 6`, `dart run drift_dev make-migrations`;
   - e. `_from5To6`: `TableMigration` dla `family_children` (te same wiersze, `id` w kolejności `rowid`) i dla
     `assertions` (te same wiersze i `id`); na końcu `PRAGMA foreign_key_check`. **Bez wstawiania
     wierszy** (D3) — komentarz z powodem (`restore_service.dart`);
   - f. `build_runner build`.
2. **Twierdzenia** — `lib/data/claims.dart`: `addFamilyClaim` (para) i `addChildLinkWithClaim` (łącze dziecka i
   twierdzenie w jednej transakcji). Pierwsze twierdzenie i pierwsza wartość jak dotąd (ADR-006 D3).
3. **Rodziny** — nowy `lib/data/families.dart`:
   - odczyt dla 9a: `watchRelations(personId)` — rodzina rodziców (rodzice), związki osoby (druga osoba, dzieci, ślub i
     koniec jako pierwsza wartość z twierdzeniem), związki według daty ślubu. Dzieci według urodzenia (D4);
   - odczyt dla A: `loadFamily(id)` (dzieci według urodzenia); dla B: `loadPersonChoices` (`graves.dart`) dostaje
     informację „jest dzieckiem w rodzinie”;
   - zapis: `saveFamily(draft)` w **jednej transakcji** — nowe osoby (imiona, nazwisko), rodzina,
     łącza pary, twierdzenie przy rodzinie (nowa rodzina), łącza dzieci z twierdzeniami, usunięcie łączy (z ich
     twierdzeniami), ślub i koniec: nowe z twierdzeniem albo poprawione w miejscu, gdy mają jedno twierdzenie (jak
     `updatePersonEntry`, [[wpis-osoby]] → poprawa D1);
   - **niezmienniki w jednym miejscu** (F5): 1–2 osoby w parze, co najmniej dwie osoby, nikt dwa razy, dziecko w jednej
     rodzinie rodziców;
   - `deleteFamily(id)`: łącza, ich twierdzenia, ślub i koniec z twierdzeniami, twierdzenia rodziny, wiersz rodziny —
     jedna transakcja; osoby zostają.
4. **Osoba** — `lib/data/graves.dart`: nowy odczyt wpisu osoby bez pochówku do poprawy (`BuriedPerson` bez grobu).
5. ~~**Nazwy i podpowiedź płci**~~ — **nie wchodzi** (stop #1). Nazwy ról są stałe („Rodzic”, „Partner”, „Dziecko”,
   [[rodzina]] → *Role names*) i żyją w widżecie sekcji 9a.
6. **Wspólny blok daty** — `_DateInput` i `_DateBlock` z `person_form_screen.dart` do `lib/app/widgets/date_block.dart`,
   bez zmiany wyglądu i zachowania (testy formularza dalej zielone).
7. **Formularz osoby** — `person_form_screen.dart` ([[wpis-osoby]] v5.1):
   - 9a (tylko poprawa): grupy b, d, e, f („Rodzice”, „Związek”, chipy, „Dodaj rodziców” · „Dodaj związek”), chipy →
     `PersonFormScreen` w poprawie krewnego (`push`), po powrocie odświeżenie; ✎ i przyciski → arkusz;
   - `Correction` bez grobu: podtytuł „bez grobu w aplikacji”, „Zapisz” wraca przez `pop` (jak dziś poprawa); w „Kto
     jest na zdjęciu?” sekcja grobu ma tylko tę osobę.
8. **Arkusz i wybór osoby** — nowe `lib/app/family/family_sheet_screen.dart` (A) i `person_picker_screen.dart` (B),
   [[rodzina]] *Elements*, *States*, okna; filtr przez `matchesQuery`, porządek przez `polishCompare`.
9. **Dane debug** — `lib/dev/fictional_data.dart`: rodziny zapisane przez `saveFamily` (z twierdzeniami); drugi związek
   po rozstaniu albo owdowieniu z własnym dzieckiem (uwaga autora do O1); dziecko bez grobu.
10. **README** → *Baza danych*: akapit „Rodzina (schemat v6)”: twierdzenie przy rodzinie i przy łączu dziecka (D1),
    relacje sprzed v6 bez twierdzeń i dlaczego (D3), kolejność dzieci (D4), płci w modelu nie ma (decyzja autora).
11. `dart format` · `flutter analyze` · `flutter test`. Build release i instalacja **na** build v5 z kroku 0, bez
    odinstalowania.

### Files likely touched
- **Kod danych:**
  - `lib/data/database.dart`, `database.g.dart`, `database.steps.dart`, `drift_schemas/grobing/drift_schema_v6.json`;
  - `lib/data/claims.dart`, `lib/data/graves.dart`, nowy `lib/data/families.dart`.
- **Kod ekranów:**
  - nowe: `lib/app/family/family_sheet_screen.dart`, `person_picker_screen.dart`, `family_section.dart` (9a),
    `lib/app/widgets/date_block.dart`;
  - `lib/app/grave/person_form_screen.dart`, `lib/app/grave/grave_screen.dart` (przekazanie trybu),
    `lib/app/photo/photo_people_screen.dart` (osoba bez grobu).
- **Debug i dokumentacja:** `lib/dev/fictional_data.dart`, `README.md`.
- **Testy (`qa`):**
  - `test/drift/grobing/migration_test.dart` i `generated/` (v6); `test/data/database_test.dart` (lista tabel, `user_version`);
  - `test/data/claims_test.dart`, `graves_test.dart`, `data_state_test.dart`; nowe `test/data/families_test.dart`;
  - `test/backup/restore_service_test.dart` (F2, F3);
  - nowe `test/app/family/family_screens_test.dart`; `test/app/grave/grave_screens_test.dart`.

### AC → tests (`qa`)
| AC | Test |
|---|---|
| AC-1 — rodzina jednym formularzem, nowe osoby przy okazji | widget: poprawa osoby → „Dodaj związek” → B → osoba z grobu → „Dodaj dziecko” → „Nowa osoba: …” → imiona → „Zapisz” → 9a ma chipy „Partner” i „Dziecko”; dane: nowa osoba istnieje, łącza są |
| AC-2 — kolejny związek (po rozstaniu albo owdowieniu) | dane i widget: osoba w dwóch rodzinach jako para, każda ze swoimi dziećmi; 9a pokazuje dwie grupy „Związek” według daty ślubu |
| AC-3 — ślub i koniec z dopiskiem | widget: ślub „około 1948”, koniec „przed 1960” → etykieta grupy; dane: zdarzenia rodziny z dopiskiem i twierdzeniem |
| AC-4 — źródło i status | dane: nowa rodzina ma twierdzenie „notatki”, `CLAIMED`; każde łącze dziecka ma twierdzenie; po usunięciu dziecka z rodziny jego twierdzenia nie ma |
| AC-5 — osoba z grobu zamiast drugiej | widget: B pokazuje osobę z grobu w „W tym grobie”; po wyborze liczba osób w bazie bez zmian |
| najwyżej dwie osoby w parze; zapis całością; niezmienniki | F4, F5; widget: przy dwóch osobach w parze nie ma „Dodaj osobę do pary”, komunikaty składu |
| migracja v5→v6; kopia v5 w v6; kopia po migracji | F1 + wygenerowane testy schematu; F2; istniejący test startu (R6) dalej zielony |
| kopia z rodzinami | F3; `data_state_test`: zmiana łącza dziecka albo twierdzenia rodziny zmienia odcisk |
| kolejność dzieci (D4) | dane i widget: dzieci dodane w kolejności 1950, bez daty, 1945 → w 9a i po ponownym otwarciu arkusza: 1945, 1950, bez daty |
| chip i osoba bez grobu | widget: chip dziecka bez grobu → wpis z podtytułem „bez grobu w aplikacji” → „Zapisz” → powrót do wpisu rodzica, chip z nowym imieniem |
| „Usuń rodzinę” | widget i dane: okno → „Usuń” → osoby zostają, łączy, zdarzeń rodziny i ich twierdzeń nie ma |
| styl B | przegląd `ui` (subagent) ze zrzutów: chipy, segment, arkusz, B, okna |

### Manual verification (stop #2) — kroki według miejsca
**Emulator `Medium_Phone`, build release (ty — UI/UX).** Wymyślone osoby i groby są na emulatorze od ISSUE-018.
Trzy kroki, a resztę sprawdza agent (wniosek z *Do retro* w `CURRENT_STATE.md`):
1. Grób z wymyślonymi osobami → dotknij osoby → przewiń do **„Rodzina”** → **„Dodaj związek”** → „Dodaj osobę do
   pary” → wybierz osobę z „W tym grobie” → „Ślub”: „około”, rok → „Dodaj dziecko” → wpisz nowe imię → „Nowa osoba: …”
   → „Zapisz”. W „Rodzina” są chipy „Partner: …” i „Dziecko: …”.
2. Dotknij **chipu nowego dziecka** → wpis „bez grobu w aplikacji” → dopisz rok urodzenia → „Zapisz” → wracasz do
   pierwszej osoby.
3. **Odczucie** (napisz tutaj): arkusz zamiast relacji po jednej (O1), klawiatura od razu w wyborze osoby (D3), chipy
   z nazwami neutralnymi i ✎.

**Agent (bez ciebie):**
- aktualizacja na buildzie v5 z kroku 0: liczby wierszy bez zmian, `family_children.id` nadane, kopia zamówiona po
  starcie;
- „Dodaj rodziców”, drugi związek z datą końca i własnym dzieckiem, kolejność dzieci według urodzenia, „Usuń
  rodzinę”, komunikaty składu, wstecz z arkusza ze zmianami;
- **F3 na urządzeniu:** nowa konfiguracja kopii z nowym hasłem testowym (wymyślone dane), kopia do Pobranych →
  odtworzenie na `Grobing_Restore` → odcisk zgodny, rodziny i twierdzenia w bazie równe;
- „Stan danych” bez błędów po migracji.

### Out of Scope (this plan)
- Drzewo, ścieżka „ja → …”, rodzeństwo, teściowie i dalsi krewni (EPIC-003, EPIC-002 M5) — rodzeństwo z decyzji
  autora na stopie #1 (O3).
- **Płeć osoby** (decyzja autora, O2/D2). Wraca jako pole osoby z migracją, jeśli nazwy na ścieżce albo w drzewie
  („jej tata”, „teść”) okażą się potrzebne.
- Rodzaj więzi dziecka (`PEDI`: przysposobienie, rodzina zastępcza) i druga rodzina rodziców — [[rodzina]] D5,
  [[US-004-fakt-od-babci]].
- Źródło inne niż „notatki” i sprzeczne twierdzenia o relacji — US-004.
- Rodzina bez pary (rodzeństwo bez znanych rodziców) — [[rodzina]] D6.
- Osoba żyjąca (`is_living`) — [[US-006-eksport-dla-rodziny]].
- Semantyka starszych ekranów i polskie `MaterialLocalizations` (kandydaci w `CURRENT_STATE.md`).

### For docs at closure
- **ADR-011 — twierdzenie o relacji przy rodzinie i przy łączu dziecka (schemat v6)** z D1 i D3: opcje (a)–(e),
  cytaty GEDCOM 7.0.18 i Gramps (*Prior art*), D3 (dlaczego migracja nie dopisuje twierdzeń). W *Context*: płci w modelu
  nie ma (decyzja autora), a GEDCOM i tak nie wyprowadza jej z miejsca w parze.
- [[ADR-006-claimed-value-separate-structures]] → *Follow-ups*: datowany dopisek „D6 doprecyzowany w ADR-011 — para:
  twierdzenie przy rodzinie”.
- `04_ARCHITECTURE/data-model.md`: diagram (ASSERTION przy FAMILY i FAMILY_CHILD), *Family* — związek (nie tylko
  małżeństwo) i kolejność dzieci; *In code* — schemat v6.
- `04_ARCHITECTURE/backup-format.md`: bez zmiany formatu; rodziny z twierdzeniami w bazie i w odcisku.
- `glossary.md`: **arkusz rodziny**; przy **rodzina** — „związek, nie tylko małżeństwo” (uwaga autora do O1).
- [[FR-002-rodzina-jako-rekord]]: wpisywanie arkuszem, widok w formularzu osoby; [[NFR-003-migracje-schematu]]: piąta
  migracja i D3.

### Self-check (planning) — said out loud
1. **Kompletność:** zakres, decyzje, falsyfikatory, kroki, pliki, AC → testy, kroki ręczne według miejsca, *Out of
   Scope* ✅.
2. **Spójność:** plan idzie za specyfikacjami `ui` z 2026-10-07. Trzy `⚠️ OPEN`, zmiana D10 (D4) i elementy spoza AC
   (płeć, „Usuń rodzinę”, rodzeństwo) poszły na stop #1 jawnie. Po stopie: płeć i rodzeństwo odpadły, „Usuń rodzinę”
   weszło, specyfikacje `ui` są w wersjach v1.1 i v5.1.
3. **Własność:** ta sekcja, `status: in-progress`, kolumny Issue(s) i Issue Status w `TRACEABILITY.md`. ADR-011 pisze
   `docs` przy zamknięciu. Specyfikacje zmieniał `ui`.
4. **Warstwa danych:**
   - test migracji v5→v6 z danymi (F1) ✅;
   - odtworzenie kopii v5 w v6 (F2) i kopii z rodzinami (F3), także na urządzeniu ✅;
   - kopia po migracji (R6) ✅;
   - źródło faktu o relacji: twierdzenie „notatki”, `CLAIMED` (AC-4) ✅.
5. **Wystarczalność — czego plan nie ma:**
   - **prawdziwego tempa** — 20 akcji na rodzinę to liczba ze specyfikacji, a nie pomiar (F9);
   - **imion z notatek** — pomiar PESEL to rejestr, a nie notatki; najstarsze pokolenia mogą mieć imiona spoza
     listy;
   - **relacji sprzed v6 bez twierdzeń** (D3) — w release ich nie ma; mają je tylko bazy buildu debug z danymi
     wymyślonymi sprzed v6, dopóki rodzina nie zostanie zapisana w arkuszu. Ekran pokazuje je jak każde inne;
   - **nazw relacji z płcią** — chipy mówią „Rodzic”, „Partner”, „Dziecko”. Jeśli ścieżka albo drzewo (EPIC-003) będą
     potrzebować „jej tata” czy „teść”, płeć wraca jako pole osoby z migracją (pomiar PESEL jest gotowy);
   - **pozycja jest duża:** dwa nowe ekrany, zmiana formularza, schemat. Stąd D7.

## Dev report
> `dev`, 2026-10-07. Flutter 3.41.1 (przypięty) ✅. Kod w `grobing-code`, bez testów (to `qa`).

### What was built
- **Schemat v6** (`lib/data/database.dart`, ADR-011 do napisania przez `docs`):
  - `family_children` dostaje `id` (stary `rowid`) i UNIQUE (rodzina, osoba);
  - `assertions` cytuje dokładnie jedno z czterech: zdarzenie, pochówek, rodzinę (`family_id`) albo łącze dziecka
    (`family_child_id`) — nowy `CHECK`;
  - `_from5To6`: dwie przebudowy (`TableMigration`), `PRAGMA foreign_key_check`, **bez wstawiania wierszy** (D3);
  - `drift_schemas/grobing/drift_schema_v6.json` i wygenerowane `test/drift/grobing/generated/schema_v6.dart`,
    `schema.dart` (`make-migrations` — kod wygenerowany, nie testy pisane ręcznie).
- **Dane:**
  - `lib/data/claims.dart`: `addFamilyClaim`, `addChildLinkWithClaim`;
  - nowy `lib/data/families.dart`: `watchRelations` i `loadRelations` (9a; związki według ślubu, dzieci według
    urodzenia — D4), `loadFamily`, `loadFamilyMember`, `peopleWithParents`, **`saveFamily`** (jedna transakcja,
    niezmienniki F5, twierdzenie dla rodziny i łączy sprzed v6 przy pierwszym zapisie), **`deleteFamily`**;
  - `lib/data/graves.dart`: `loadPersonForCorrection` (wpis z chipu, także bez grobu), wspólna budowa `BuriedPerson`,
    publiczne `qualifiedDateValues` i `blankToNull` (używa ich `families.dart`), `watchTables` (Deviations 1).
- **Ekrany:**
  - nowe `lib/app/family/family_section.dart` (9a), `family_sheet_screen.dart` (A), `person_picker_screen.dart` (B);
  - `lib/app/widgets/date_block.dart` — `DateInput`, `DateBlock`, `ErrorLine`, `inputTextStyle` wyjęte z formularza
    osoby bez zmiany zachowania; `DateBlock` dostał opcjonalną linię pod etykietą (A6');
  - `person_form_screen.dart`: 9a w poprawie, `Correction.graveTitle` może być puste → podtytuł „bez grobu w
    aplikacji”;
  - `photo_people_screen.dart`: nagłówek sekcji publiczny (`PeopleSectionHeader`), wspólny z arkuszem i wyborem.
- **Dane debug** (`lib/dev/fictional_data.dart`): rodziny przez `saveFamily` (z twierdzeniami); drugi związek ojca po
  rozstaniu z partnerką i dzieckiem bez grobu (rok urodzenia 1927).
- **README** → *Baza danych*: akapit „Rodzina (schemat v6)”.

### Checks (dev, host Windows + emulator `Medium_Phone_API_36.1`, build release)
- `dart format` ✅ · `flutter analyze`: czyste.
- `flutter test`: **424 ✅, 5 ❌** — wszystkie pięć oczekuje starego stanu, nie błędu kodu (do poprawy przez `qa`):
  - `test/data/database_test.dart` „fresh database … user_version 5 … exactly the v5 tables” — teraz 6;
  - `test/data/data_state_test.dart` „empty database: schema 5” — teraz 6;
  - `test/data/data_state_test.dart` „row counts follow the data” — dane debug mają teraz 5 osób zamiast 3;
  - `test/app/data_state_screen_test.dart` „shows schema version … debug button adds made-up data” — liczby osób
    i rodzin w danych debug;
  - `test/app/restore_screen_test.dart` „phone with data: … dialog with the counts” — te same liczby.
  
  Testy migracji (pętla wszystkich par, także do v6) przechodzą.
- **Aktualizacja v5 → v6 na `Medium_Phone`** (build release wgrany na v5, bez odinstalowania), „Stan danych” przed i po:

  | | v5 | v6 |
  |---|---|---|
  | wersja schematu | 5 | 6 |
  | osoby · rodziny · partnerzy · dzieci | 5 · 0 · 0 · 0 | 5 · 0 · 0 · 0 |
  | zdarzenia · cmentarze · groby · pochówki | 4 · 1 · 2 · 5 | 4 · 1 · 2 · 5 |
  | twierdzenia · zdjęcia · łącza · ustawienia · pliki | 9 · 13 · 15 · 0 · 13 | 9 · 13 · 15 · 0 · 13 |
  | odcisk danych | `079e3bf6f6b74a32` | `168d42128e1c5aaa` |

  Odcisk zmienił się, bo zmieniły się kolumny (`family_children.id`, dwie kolumny `assertions`) — jak przy każdej
  zmianie schematu. **Rodzin w buildzie release przed v6: 0** — potwierdza D3 na urządzeniu.
- **Na emulatorze (wymyślone osoby):**
  - 9a pusta: nagłówek, „Dodaj rodziców”, „Dodaj związek”;
  - „Dodaj związek” → A: „ta osoba” bez ✕, „Koniec związku” schowany, linia źródła;
  - B: klawiatura od wejścia, „Nowa osoba” na górze, „W tym grobie”, „już w tej rodzinie” przy tej osobie;
  - wybór partnera z grobu → „Dodaj osobę do pary” znika przy dwóch;
  - ✎ → A w poprawie z „Usuń rodzinę”; nowe dziecko „Stefan” → „dalej” do „Nazwisko” (podpowiedź zaznaczona) →
    „Zapisz” → 9a od razu: „Partner: Jan”, „Dziecko: Stefan”;
  - chip „Dziecko: Stefan” → wpis z podtytułem „bez grobu w aplikacji”, 9a: „Rodzic: Anna”, „Rodzic: Jan”, tylko
    „Dodaj związek”.

### Deviations from the plan
1. **`watchTables` w `graves.dart` — poprawka poza planem, zgłoszona.** drift współdzieli strumień między
   obserwatorami tego samego SQL i zmiennych (`StreamKey` = SQL + zmienne, bez `readsFrom`), a wspólny strumień ma
   `readsFrom` tego, kto otworzył go pierwszy. Wszystkie widoki obserwowały `SELECT 1`, więc widok grobu otwarty z
   listy cmentarza słuchał tylko tabel listy (bez `events`, `assertions`, `person_media`), a sekcja 9a — tak samo.
   **Na emulatorze:** zapis rodziny bez nowej osoby nie odświeżył 9a (widać było dopiero po ponownym otwarciu).
   Poprawka: każdy obserwator ma własny klucz (`SELECT 1 AS grave`, `cemetery_graves`, `family_relations`). W
   widoku grobu błąd był uśpiony (każdy zapis z formularza zmienia też `persons`), więc dotąd go nie widać.
2. **`watchRelations` słucha też `assertions`** — poprawa rodziny sprzed v6 może zapisać samo twierdzenie.
3. **„dalej” z „Imiona” wskazuje „Nazwisko” wprost** (`onEditingComplete`) w nowym wierszu arkusza. Na emulatorze
   kolejność czytania prowadziła z „Imiona” do ✕ obok (kolejny Enter usunął wiersz), a po wyłączeniu ✕ — do „Zapisz”,
   nigdy do „Nazwisko” pod spodem. ✕ zostaje w zwykłej kolejności fokusu (klawiatura fizyczna).
4. **Podpowiedź nazwiska nowego dziecka** to nazwisko pierwszej osoby z pary; gdy „tą osobą” jest matka, syn dostaje
   „Wymyślona” (zaznaczone, pisanie zastępuje). To znana uwaga z formularza osoby (-ski/-ska), [[rodzina]] A3' ją
   wymienia.
5. Pliki wygenerowane w `test/drift/grobing/generated/` (v6) — wynik `make-migrations`, jak przy v5.

### For qa
- **Pięć czerwonych testów** wyżej: oczekiwania v5 i liczby danych debug.
- **Testy do napisania** według *AC → tests* i F1–F5. Sekcja 9a i B czytają strumień drift: wzorzec `leaveScreen` z
  `test/app/grave/grave_screens_test.dart` (zakleszczenie na blokadzie bazy, `CURRENT_STATE.md` → *Do retro*).
- **Stan emulatora `Medium_Phone`** (release v6, wymyślone dane): rodzina Anna + Jan z dzieckiem „Stefan Wymyslona”
  bez grobu (zapisana w arkuszu). Stan v5 przed aktualizacją jest w tabeli wyżej.
- **F3 na urządzeniu** (kopia z rodzinami → odtworzenie na `Grobing_Restore`) — nie zrobione przez `dev`.
- Przegląd `ui` (subagent) ze zrzutów: 9a, A (nowa, poprawa, okna), B.

## Verification
> `qa`, 2026-10-07/08. Werdykt po stopie #2.

### Automated — `flutter test`: 458 ✅ (było 429; 457 przed przeglądem US, +1 test z jego uwagi 1 — dopiski ślubu i końca wpisane w arkuszu) · `flutter analyze`: czyste · `dart format`: ✅
- **Poprawione oczekiwania** (5 czerwonych z *Dev report*): `database_test` (v6, tabele, kolumny `family_children.id`,
  `assertions.family_id`, `family_child_id`), `data_state_test` (schemat 6, liczby danych debug v6),
  `data_state_screen_test`, `restore_screen_test` (liczby dwóch partii danych debug).
- **Nowe (28):**
  - **F1** — `migration_test`: v5→v6 z danymi (ojciec w dwóch związkach, ślub z twierdzeniem, pochówek, łącze z kadrem):
    te same wiersze i `id`, łącza dzieci dostają `id` z `rowid` w kolejności, twierdzenia bez zmian i bez celu w
    rodzinie, **żadna tabela nie zyskuje ani nie traci wierszy**, `foreign_key_check` pusty; plus 5 wygenerowanych par
    v1…v5→v6;
  - **F2** — `restore_service_test`: kopia v5 z rodzinami (bez twierdzeń) odtwarza się w v6 — liczby wierszy z
    manifestu równe, relacje ojca czytane jak przed migracją, łącza z `id` 1 i 2;
  - **F3** — test „end to end” (prawdziwy `BackupService`, dane debug v6): po odtworzeniu dwa związki ojca z dziećmi i
    4 twierdzenia relacji, odcisk równy;
  - `families_test` (15): AC-1, AC-4, AC-5 · AC-2 (dwa związki według ślubu, rodzice dziecka) · AC-3 (poprawa w miejscu,
    data z dwoma twierdzeniami nietknięta) · AC-4 (usunięte dziecko zabiera twierdzenia łącza; rodzina i łącza sprzed v6
    dostają twierdzenia przy pierwszym zapisie) · **F5** (trzy osoby w parze, bez pary, jedna osoba, ta sama osoba dwa
    razy, dziecko z rodzicami gdzie indziej — odmowa i nic nie zapisane) · **F4** (nowy partner zapisany, potem dziecko
    bez imienia → partnera też nie ma) · D4 (dzieci według urodzenia, bez daty na końcu) · D8 („Usuń rodzinę”) ·
    `CHECK` twierdzenia (dwa cele albo żaden → odmowa) · wpis z chipu (bez grobu / z grobem) · **regresja *Dev report*
    → Deviations 1** (przy otwartej liście cmentarza sekcja i widok grobu słyszą swoje tabele) — **sprawdzone, że test
    pada bez poprawki `watchTables`**;
  - `family_screens_test` (5): AC-1 i AC-5 przez formularz → „Dodaj związek” → B → osoba z grobu → „Dodaj dziecko” →
    „Nowa osoba: „Anna”” → `next` do „Nazwisko” → „Zapisz” → chipy w 9a · AC-2, AC-3, D4 (etykiety związków, chip dziecka
    → wpis bez grobu z rodzicami → powrót) · reguły arkusza (komunikat bez pary, okno odrzucenia, „Usuń rodzinę”) · B
    („ma już rodziców”, pusty wynik z „Nowa osoba”) · nowa osoba bez 9a;
  - `data_state_test`: zmiana twierdzenia łącza dziecka zmienia odcisk.

### Agent checks on the emulators (release, wymyślone dane)
- **Aktualizacja v5→v6** na `Medium_Phone` i na `Grobing_Restore` (build wgrany na v5, bez odinstalowania): liczby
  wierszy bez zmian (tabela w *Dev report*), rodzin przed v6: 0 na obu.
- **Kopia w tle po zapisie rodziny** przeszła sama (21:48, `Medium_Phone`).
- **F3 na urządzeniu:** nowa konfiguracja kopii z nowym hasłem testowym → `grobing-klucz-019.age`,
  `grobing-kopia-019.age` (Pobrane `Medium_Phone`, 21:53) → przeniesione przez `adb` → odtworzenie na
  `Grobing_Restore`: **odcisk `8d637712f2ac7532` — ten sam co źródło**; osoby 6, rodziny 1, partnerzy 2, dzieci 1,
  twierdzenia 11, zdjęcia 13, łącza 15, pliki 13 — równe.
- Przepływy z *Dev report* → *Checks* plus: „Koniec związku” odsłonięty z linią v1.1 i klawiaturą numeryczną; okna
  „Usunąć rodzinę?” i „Odrzucić zmiany w rodzinie?” z tekstami ze specyfikacji; błąd daty.

### ui review (subagent bez historii, ze zrzutów emulatora i kodu)
0 BLOCKER, **1 MAJOR**, 4 MINOR:
- **MAJOR** — linia błędu daty chowała się pod przypiętym „Zapisz” przy otwartej klawiaturze (wspólny `DateBlock`, więc
  też „Urodzenie” i „Zgon” w formularzu osoby). Poprawione: blok z błędem przewija się cały (`Scrollable.ensureVisible`,
  `keepVisibleAtEnd`), pola dat mają `scrollPadding` z miejscem na komunikat. **Sprawdzone na emulatorze:** komunikat
  widoczny nad „Zapisz” z otwartą klawiaturą.
- MINOR, poprawione: 24 dp przed „Dzieci” (było 32) · „Dodaj koniec związku” i „Usuń rodzinę” na krawędzi treści ·
  „Nowa osoba” z rolą przycisku dla czytnika · zaległe słowa w specyfikacjach (`ui`: [[rodzina]] v1.2,
  [[wpis-osoby]] v5.2).
- Zgodne (lista przeglądu): elementy i kolejność A, B, 9a; stany; jeden wypełniony przycisk; kontrast z `theme.dart`
  (bez nowych tokenów); cele ≥ 48 dp; kolor nigdy sam; chip według reguły 11 v1.11; ton i formaty; osoby wymyślone.
- Do odczucia autora: podpowiedź nazwiska syna „Wymyslona” po matce (A3', -ski/-ska) — bez płci lepiej się nie da.

### Family data
- W zmianach nie ma baz, kopii, eksportów ani zdjęć (lista plików `git status`, strażnik przy `git add`).
- Osoby w kodzie, testach, specyfikacjach i na zrzutach — wymyślone; `family_data_dir` w tej sesji nie był czytany.
- Pliki kopii F3 i zrzuty leżą w katalogu tymczasowym sesji, poza repo.

### State left on the emulators (dla autora)
- `Medium_Phone` (release v6): rodzina Anna + Jan z dzieckiem „Stefan Wymyslona” bez grobu; kopia skonfigurowana od
  nowa z hasłem testowym do Pobranych (`grobing-klucz-019.age`, `grobing-kopia-019.age`, wymyślone dane).
- `Grobing_Restore` (release v6): dane z kopii 019 (odcisk `8d637712f2ac7532`).

### Manual (stop #2) — autor i agent, emulator `Medium_Phone`, 2026-10-08
Odpowiedź autora: **„ok”**. Stan urządzenia sprawdzony przez agenta po odpowiedzi:
1. **Wykonany, z nadmiarem.** U Ewy Wymyslonej autor zapisał związek z Janem z datami (`Związek · ślub ok. 1993 ·
   koniec 1995` — dopisek „około” i odsłonięty koniec związku) i nowym dzieckiem „Dziecko Jana” (bez grobu), a do tego
   **„Dodaj rodziców”** (Stefan i Anna). Chipy „Rodzic:”, „Partner:”, „Dziecko:” i ✎ przy obu grupach są na miejscu.
2. **Pomiń** — wpis nowego dziecka nie ma roku urodzenia, więc kroku z chipem nikt nie domknął zapisem. Tę drogę (chip →
   „bez grobu w aplikacji” → zapis → powrót) sprawdził agent na emulatorze (*Dev report* → *Checks*) i pokrywa ją test
   `family_screens_test` (AC-2…).
3. **Odczucie:** „ok” bez uwag.

**Obserwacja z danych autora (nie błąd tej pozycji):** rodzicami Ewy są Anna i Stefan, a Stefan jest dzieckiem Anny —
aplikacja pozwala, by osoba była w parze ze swoim dzieckiem. Kontrola „nikt nie jest swoim przodkiem” jest w
[[rodzina]] → *Poza zakresem tej wersji*. Kandydat na małą pozycję, gdy pojawi się przy prawdziwym przepisywaniu.

### Verdict — APPROVED (self-check, z uwagami)
- **AC-1…AC-5** mają testy danych i ekranu; F1–F5 zmierzone (migracja, kopia v5 w v6, kopia z rodzinami w teście i na
  urządzeniu, zapis całością, reguły w warstwie danych); F6 zmierzone i nieużyte (bez płci); F7 z kodu i z urządzenia
  (rodzin w release przed v6: 0 na dwóch emulatorach).
- **Uwagi:**
  - tempo (F9) — wyliczenie ze specyfikacji, nie pomiar; prawdziwe pokaże przepisywanie notatek;
  - kontrola cykli w rodzinie poza zakresem (obserwacja wyżej);
  - **przegląd US-003** (niezależny, subagent): APPROVED z uwagami — [[US-003-przepisanie-rodziny]] → *Verification (US)*; z
    uwag: data początku związku bez ślubu (kandydat), twierdzenie o parze przy rodzinie (ADR-011);
  - poprawka strumieni drift (*Dev report* → Deviations 1) wyszła poza plan i objęła widok grobu — z testem regresji;
  - relacje sprzed v6 nie mają twierdzeń, dopóki rodzina nie zostanie zapisana w arkuszu (D3) — w release ich nie ma.
- **Czego szukałem i nie znalazłem:** zgubionych wierszy po migracji (F1, oba emulatory), twierdzenia bez celu albo z
  dwoma (test `CHECK`, `foreign_key_check`), osoby wpisanej dwa razy przy wyborze z grobu (AC-5), rozjazdu odcisku po
  odtworzeniu (F3 ×2), danych rodziny w zmianach.

### Package list for docs
**`grobing-code`:**
- `README.md`;
- `lib/data/database.dart`, `database.g.dart`, `database.steps.dart`, `claims.dart`, `graves.dart`, `families.dart` (nowy);
- `lib/app/family/family_section.dart`, `family_sheet_screen.dart`, `person_picker_screen.dart` (nowe);
- `lib/app/widgets/date_block.dart` (nowy), `lib/app/grave/person_form_screen.dart`, `lib/app/photo/photo_people_screen.dart`;
- `lib/dev/fictional_data.dart`;
- `drift_schemas/grobing/drift_schema_v6.json` (nowy);
- `test/drift/grobing/migration_test.dart`, `generated/schema.dart`, `generated/schema_v6.dart` (nowy);
- `test/data/database_test.dart`, `data_state_test.dart`, `families_test.dart` (nowy);
- `test/backup/restore_service_test.dart`;
- `test/app/data_state_screen_test.dart`, `restore_screen_test.dart`, `family/family_screens_test.dart` (nowy).

**`grobing-vault`:**
- `backlog/issues/ISSUE-019-family-relations.md` (nowy);
- `03_REQUIREMENTS/user-stories/US-003-przepisanie-rodziny.md`;
- `05_DESIGN/rodzina.md` (nowy), `05_DESIGN/wpis-osoby.md`, `05_DESIGN/brand/style-b.md`;
- `00_START_HERE/CURRENT_STATE.md`, `00_START_HERE/TRACEABILITY.md`;
- pliki zamknięcia `docs` (*For docs at closure*).

**`grobing-agents`:** brak zmian.
