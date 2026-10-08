---
title: "ISSUE-025 — Gender back in the person form, Polish kinship names, union 'together since', no sources in the form"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-08
verdict-reviewer: self-check
source: "[[SPIKE-004-mvp-flow-prototype]] D16, D20, D28 (decyzje autora na prototypie, 2026-10-08)"
created: 2026-10-08
updated: 2026-10-08
---

# ISSUE-025 — Płeć, nazwy pokrewieństwa, „Razem od”, formularz bez źródeł

> Z zamknięcia [[SPIKE-004-mvp-flow-prototype]]. Jedna zmiana schematu dla trzech rzeczy w danych osoby i rodziny.
> Specyfikacja: [[wpis-osoby]] v5.4 (4a; elementy 9–10 bez źródła), [[rodzina]] v1.4, [[osoba]] D4, [[drzewo]] D4, D6.

## What to build
- **Płeć** (D16): pole „Płeć” (Kobieta · Mężczyzna) w formularzu osoby, podpowiadane z imienia, poza `next`
  ([[wpis-osoby]] 4a, kształt z v5). **Zmiana schematu:** kolumna płci, migracja z testem (bez wartości dla istniejących
  osób; formularz podpowie przy pierwszej poprawie).
- **Nazwy pokrewieństwa po polsku** (D16): z płci i strony ścieżki do „ja” — mama/tata, babcia/dziadek, stryj/wuj/ciotka,
  rodzeństwo stryjeczne/wujeczne/cioteczne, teść/teściowa, szwagier/szwagierka… oraz **opis złożony z odcinków** w
  dopełniaczu („siostra cioteczna babci mojej żony”, [[drzewo]] D6). **Słownik ze źródłem** (kanon polskiej terminologii
  pokrewieństwa), nie z pamięci; test na tabeli przypadków. Chipy i role w arkuszu rodziny z płci ([[rodzina]] v1.3).
- **„Razem od”** (D20, [[rodzina]] v1.4): w arkuszu rodziny obok „Ślubu” data początku związku; zdarzenie rodziny jak
  ślub. Związek bez ślubu: „Partner/Partnerka”.
- **Formularz bez źródeł** (D28): bez linii „Źródło: notatki · Zmień” przy „kim była” i bez tekstu „Daty i miejsce
  pochówku zapiszą się ze źródłem: notatki”. Dane dalej zapisują się z domyślnym źródłem w schemacie — bez migracji.

## Acceptance Criteria
- **AC-1** *Given* osoba „Maria” *When* otwieram formularz *Then* „Płeć” jest podpowiedziana jako Kobieta; zapis ją
  utrwala.
- **AC-2** *Given* ścieżka Ja → rodzic (mężczyzna) → jego rodzic → jego córka *Then* nazwa to „ciotka”; brat ojca —
  „stryj”, brat matki — „wuj”; dziecko siostry ojca — „brat/siostra cioteczna”.
- **AC-3** *Given* para z „Razem od” 1980 i „Ślubem” 1985 *Then* obie daty są zapisane, a chip po ślubie mówi „Mąż/Żona”.
- **AC-4** *Given* kopia sprzed migracji *When* odtwarzam ją *Then* dane są pełne, osoby bez płci, związki bez „Razem od”.
- **AC-5** formularz nie pokazuje źródła ani przy „kim była”, ani przy datach.

## Implementation plan
> `planning`, 2026-10-08. Specyfikacje (`ui`, przed planem): [[wpis-osoby]] v5.5 (4a), [[rodzina]] v1.5 (A3'a, A5–A5'',
> *Role names*, D12–D14, *Open* 4), [[osoby]] v2.1 (*Pokrewieństwo w liście*, D8, D9), [[style-b]] bez zmian. Makieta
> kandydatów *Open* 4 (R6) i podglądu reszty: `issue-025-warianty.html` w katalogu tymczasowym sesji (poza repo).

### Prior art
- **Słownik pokrewieństwa — kanon, nie pamięć.** M. Frąckiewicz, *Stopnie pokrewieństwa i powinowactwa rodzinnego w
  języku młodzieży (cz. III). Nazwy członków dalszej rodziny w linii bocznej*, „Studia nad Rodziną” 17/2 (33), 2013,
  s. 113–126 ([bazhum](https://bazhum.muzhp.pl/media/texts/studia-nad-rodzina/2013-tom-17-numer-2-33/studia_nad_rodzina-r2013-t17-n2_33-s113-126.pdf),
  odczyt 2026-10-08). Artykuł cytuje definicje ze *Słownika języka polskiego* pod red. W. Doroszewskiego (SJPD, 1967) z
  tomem i stroną:
  - stryj — „brat ojca” (t. VIII, s. 842); stryjenka — „żona stryja” (tamże);
  - wuj — „brata matki lub męża ciotki, dalszego krewnego ze strony matki” (t. IX, s. 1382); wujenka — „żona wuja”;
  - ciotka — „siostra lub kuzynka matki lub ojca” (t. III, s. 1010), a za Szymczakiem: *„nie ma w języku polskim odróżnienia
    nazwowego między siostrą matki i siostrą ojca”* — **stąd nawias „(siostra taty)” w liście** ([[osoby]] D8);
  - brat cioteczny — „syn ciotki” (t. III, s. 1012); siostra cioteczna — „córka ciotki”; brat stryjeczny — „syn stryja”
    (t. VIII, s. 237);
  - bratanek — „syn brata”, bratanica — „córka brata” (t. III, s. 649); siostrzeniec — „syn siostry”, siostrzenica —
    „córka siostry” (t. VIII, s. 237);
  - teściowa — „matka żony lub męża” (t. IX, s. 127); teściowie — „rodzice żony albo męża; teść i teściowa”; zięć —
    „mąż córki” (t. X, s. 1109); synowa — „żona syna” (t. VIII, s. 977); bratowa — „żona brata” (t. I, s. 651);
  - szwagier — „mąż siostry albo brat żony lub męża…” (t. VIII); szwagierka — „siostra męża lub żony albo żona szwagra”,
    przy czym *„w tym znaczeniu [żona brata] zdecydowanie częściej pojawia się wyraz bratowa”*.

  Monografia, na której stoi artykuł: M. Szymczak, *Nazwy stopni pokrewieństwa i powinowactwa rodzinnego w historii i
  dialektach języka polskiego*, Warszawa 1966 (nieczytana — cytowana za artykułem). Uzupełnienie z [SJP PWN](https://sjp.pwn.pl)
  (odczyt 2026-10-08): wujeczny — „spokrewniony przez wujka”, brat wujeczny — „syn wujka”; pradziadek — „ojciec dziadka
  albo babci”.
- **[GEDCOM 7.0](https://gedcom.io/specifications/FamilySearchGEDCOMv7.html)** (odczyt 2026-10-08):
  - `SEX` — *„the sex of the individual at birth”*, wartości `M` „Male”, `F` „Female”, `X` „Does not fit the typical
    definition of only Male or only Female”, `U` „Cannot be determined from available sources”. Pusta kolumna = `U`
    (ISSUE-019 D2); `X` bez przypadku w notatkach — dojdzie bez migracji (enum jako tekst);
  - `MARR` — *„A legal, common-law, or customary event such as a wedding or marriage ceremony that joins 2 partners…”*;
    payload `Y` — *„the event is known to have occurred without providing any additional information about it”* → **ślub
    bez daty to zdarzenie bez daty** (D1 = R);
  - `FAM` *„may also be used for cultural parallels to this, including nuclear families, marriage, cohabitation…”*; tagu
    na początek związku bez ślubu nie ma — `EVEN` *„must be classified by a subordinate use of the TYPE tag”* → „Razem
    od” to zdarzenie rodziny eksportowane kiedyś jako `EVEN` + `TYPE`.
- **Podpowiedź płci z imienia:** pomiar na rejestrze PESEL, 0,066% pomyłek wśród zmarłych, z listą wyjątków —
  [[ISSUE-019-family-relations]] → *Prior art* (reguła w [[wpis-osoby]] *D-płeć*).
- **Z kodu** (ankieta 2026-10-08): ścieżki ani grafu między osobami nie ma (drzewo to zaślepka). `textEnum` nie dodaje
  `CHECK`, a `CHECK` na `events` traktuje każdy typ spoza osoby jako zdarzenie rodziny — **nowy typ bez przebudowy
  tabeli**. Ślubu bez daty **dziś nie da się zapisać**: `saveFamily` pomija pustą datę, a przy następnym zapisie kasuje
  zdarzenie (`families.dart` 339–361), `QualifiedDate.ofEvent` daje `null` przy braku roku.

### Stop #1, runda 1 (2026-10-08) — uwagi autora, plan wraca do `ui`
Autor nie wybrał ani R, ani V — opisał trzeci kształt:
1. **Związek „ewoluuje”:** *„związek może »ewoluować« w małżeństwo (wiem że to do drzewa ale też można te linie inaczej
   zaznaczać). Podczas tworzenia chciałbym wybrać daną osobę i dobrać jej parę i na »pop-upie« zostać zapytany o
   szczegóły (pojedynczo, najpierw do wyboru osoba, potem czy razem/małżeństwo, potem opcja zakończenia lub »ewolucji«
   relacji z razem na małżeństwo/koniec związku itd.) Po dodaniu miałbym widok tylko informacje o partnerze z datami i
   opcje edycji tego partnera oraz możliwość dodania kolejnego.”* → związek to **oś czasu**: razem od → ślub → koniec.
   Dane z planu pasują bez zmian (zdarzenia `together`, `marriage` — także bez daty — i `end`); zmienia się ekran:
   kreator krok po kroku zamiast przełącznika w arkuszu (D1 zastąpione).
2. **Płeć ikonami:** *„Płeć natomiast myślałem zaznaczać ikonką męską i damską (nie wiem jakie są standardy teraz)”*.
   Standard: GEDCOM zapisuje `M`/`F`, a ekranu nie narzuca; Material ma symbole ♀ ♂ (`Icons.female_outlined`,
   `Icons.male_outlined` — są we Flutterze 3.41.1). Ikona bez napisu potrzebuje nazwy dla czytnika (WCAG 2.2 SC 1.1.1,
   4.1.2) — „Kobieta”, „Mężczyzna”.
3. **Bez pokrewieństwa w zakładce Osoby:** *„W osobach bym nie dodawał informacji kto jest kim dla kogo to jest funkcja
   łączenia osób w drzewie (przy wielu poziomach to by się strasznie rozrastało)”* → [[osoby]] D2 i v2.1 wycofane. Słownik
   i ścieżka nie mają w tej pozycji widocznego użytkownika — **rekomendacja: przenieść je do [[ISSUE-024-person-view]]**
   („Jak łączy się ze mną”), razem z *Prior art* (kanon zostaje zapisany tutaj). AC-2 idzie za nimi.

Dalej: `ui` projektuje kreator partnera, widok partnera i ikony płci na klikalnym prototypie (nowa interakcja → makieta,
R5, R6), a z nim kandydatów na miejsce dzieci; potem plan wraca na stop #1.

### Decisions for stop #1 — runda 2 (rekomendacja → „tak” przyjmuje wszystkie)
> **Stop #1, runda 2, 2026-10-08 — autor: „C1 / P1 / Jest dobrze”.** R2-D1 = **C1** z nowym brzmieniem
> [[FR-002-rodzina-jako-rekord]] i [[US-003-przepisanie-rodziny]] AC-1 („rodzina to jeden rekord: para i jej dzieci; dzieci
> dodaje się przy parze” — zapisuje `docs` przy zamknięciu); R2-D2 = **P1**; R2-D3 (AC-2 i słownik → ISSUE-024) i R2-D4
> (jedna pozycja) przyjęte; z rundy 0 obowiązują D3 i D4.

> Specyfikacje po rundzie 1: [[rodzina]] v2 (C kreator, D podsumowanie, E dziecko; A zastąpiony), [[wpis-osoby]] v5.6 (4a
> ikony, 9a karty), [[osoby]] v2.2 (bez pokrewieństwa). Prototyp: `issue-025-prototyp.html` w katalogu tymczasowym sesji
> (6 paneli, warianty C i P do przełączania).

- **R2-D1 — dzieci: C1, C2 czy C1+** ([[rodzina]] *Open* 5; prototyp, panel 4). **C1 (rekomendacja):** dzieci pod kartą
  związku, „Dodaj dziecko” na karcie — bez pytania „Z kim?”. **C2:** osobna sekcja „Dzieci”, +1 akcja na dziecko.
  **Konflikt z wymaganiem:** [[US-003-przepisanie-rodziny]] AC-1 („rodzina jednym formularzem… w jednym przebiegu”) i
  [[FR-002-rodzina-jako-rekord]] („para + dzieci naraz”) — w C1 i C2 para i dzieci to dwa przebiegi. Tempo bez zmian
  (20 akcji na rodzinę 5 osób, [[rodzina]] *Tempo* v2), a rodzina dalej jest jednym rekordem (para i jej dzieci).
  Rekomendacja: **C1 i nowe brzmienie FR-002 / US-003 AC-1** — „rodzina to jeden rekord: para i jej dzieci; dzieci dodaje
  się przy parze” (`docs` przy zamknięciu, decyzja autora w tym stopie). **C1+**, gdy „jednym przebiegiem” ma zostać: krok 4
  kreatora „Dzieci tej pary” (kilka naraz, „Bez dzieci — zapisz”) — +1 krok w każdym związku, także bez dzieci.
- **R2-D2 — rodzice: P1 czy P2** ([[rodzina]] *Open* 6; prototyp, panel 5). **P1 (rekomendacja):** „Dodaj rodziców” →
  kreator: mama → tata (albo „Nie wiem”) → związek → co dalej; płeć nowych rodziców wynika z pytania. **P2:** rodziców
  dodaje się tylko we wpisie rodzica.
- **R2-D3 — słownik i ścieżka do [[ISSUE-024-person-view]]** (rekomendacja). Bez pokrewieństwa w liście (decyzja autora)
  ta pozycja nie ma ekranu, który by je pokazał, a ISSUE-024 ma: „Jak łączy się ze mną”. **AC-2 przechodzi do ISSUE-024**
  razem z tabelą z rundy 0 (D2) i kanonem z *Prior art* — zapisuje `docs` przy zamknięciu. Tu zostają nazwy ról z płci w
  chipach i na karcie (Matka, Ojciec, Mąż, Żona, Partner, Partnerka, Syn, Córka).
- **R2-D4 — pozycja rośnie.** Kreator, podsumowanie i dodawanie dziecka zastępują arkusz rodziny A z ISSUE-019 (B zostaje
  jako krok „Z kim?”). Rekomendacja: **jedna pozycja** — jedna zmiana schematu i ekran, który na niej stoi; podział
  dałby ekran z ISSUE-019 na danych v7 bez sposobu wpisania „Razem od”. *Obali:* plan nie mieści się w jednej sesji `dev`
  — wtedy kreator i karty jako ISSUE-026, a tu tylko schemat, płeć i formularz.
- **Z rundy 0 obowiązują:** D3 (płci nie zgadujemy przy migracji) i D4 (ADR-012, nie zastąpienie ADR-011 — sygnał dla
  `architect` się nie zapala).

### Decisions for stop #1 — runda 0 (zapis; D1 zastąpione osią czasu, D2 → ISSUE-024, D3 i D4 obowiązują)
- **D1 — rodzaj związku: R czy V** ([[rodzina]] *Open* 4; makieta, rząd 1). **R (rekomendacja):** przełącznik
  „Małżeństwo · Razem”, ślub bez daty zostaje małżeństwem („Mąż/Żona”), „Razem od” schowane przy małżeństwie. **V:** same
  daty — „Mąż/Żona” tylko z datą ślubu; para „żona Jana” bez daty z notatek dostaje „Partner/Partnerka”. Kanon za R:
  GEDCOM `MARR Y`. Koszt R: flaga małżeństwa w warstwie danych (niżej). *Obali:* przy przepisywaniu prawie każda para ma
  datę ślubu — wtedy przełącznik jest zbędny.
- **D2 — słownik nazw: zakres i reguły** (wszystkie ze źródłem z *Prior art*; ścieżka od „ja”: R = rodzic, D = dziecko,
  B = rodzeństwo, czyli dzieci tej samej rodziny, P = para; płeć ostatniej osoby wybiera formę):

  | Ścieżka | Nazwa (K / M) | Nawias w liście ([[osoby]] D8) |
  |---|---|---|
  | R · R R · R×n | mama / tata · babcia / dziadek · pra…babcia / pra…dziadek | — |
  | D · D D · D×n | córka / syn · wnuczka / wnuk · pra…wnuczka / pra…wnuk | — |
  | B | siostra / brat | — |
  | P (małżeństwo · razem) | żona / mąż · partnerka / partner | — |
  | R(M) B | ciotka / stryj | (siostra taty) / (brat taty) |
  | R(K) B | ciotka / wuj | (siostra mamy) / (brat mamy) |
  | R B(M) P — małżeństwo | stryjenka (R = tata) · wujenka (R = mama) | (żona brata taty) · (żona brata mamy) |
  | R B(K) P — małżeństwo | wuj (SJPD: „mąż ciotki”) | (mąż siostry taty) · (mąż siostry mamy) |
  | R B(M) D, R = tata | siostra / brat stryjeczny | (córka brata taty) |
  | R B(M) D, R = mama | siostra / brat wujeczny | (syn brata mamy) |
  | R B(K) D | siostra / brat cioteczny | (córka siostry taty) |
  | B(M) D · B(K) D | bratanica / bratanek · siostrzenica / siostrzeniec | (córka brata) · (syn siostry) |
  | P R — małżeństwo | teściowa / teść | (mama żony) |
  | D P — małżeństwo | synowa / zięć | (żona syna) |
  | B(M) P — małżeństwo | bratowa | (żona brata) |
  | B(K) P — małżeństwo · P B — małżeństwo | szwagier · szwagierka / szwagier | (mąż siostry) · (siostra żony) |

  **Poza tabelą — opis z odcinków w dopełniaczu**, np. „żona taty”, „syn taty” (rodzeństwo przyrodnie), „tata partnerki”,
  „siostra cioteczna babci żony”: najdłuższy znany odcinek od „ja”, potem następny ([[drzewo]] D6). Ojczym, pasierb,
  rodzeństwo przyrodnie i „dziadek stryjeczny” zostają opisem — słownik da się poszerzyć później bez zmiany danych.
  **Brak płci osoby, od której zależy słowo** → odcinki neutralne („rodzic taty”, „dziecko brata”, [[osoby]] D9).
  **Kilka ścieżek:** najkrótsza w grafie osoba–rodzina; przy równej — mniej krawędzi „para”; dalej stała kolejność `id`.
- **D3 — płci nie zgadujemy przy migracji.** Kolumna przychodzi pusta; formularz podpowiada przy pierwszej poprawie
  ([[wpis-osoby]] *D-płeć*), lista daje opis neutralny (D9). Do instalacji MVP bez płci są tylko wymyślone osoby z testów.
- **D4 — ADR-012 „Płeć osoby i rodzaj związku (schemat v7)”**, pisany przez łańcuch (`docs` przy zamknięciu). To **nie
  jest zastąpienie** [[ADR-011-relation-claims-family-and-child-link]]: jego decyzja (gdzie stoją twierdzenia o relacji)
  zostaje, a pkt 5 („płci w modelu nie ma”) sam przewidział powrót płci w *Follow-ups* — ADR-011 dostaje datowany dopisek.
  Dlatego **sygnał dla `architect`** („pierwszy ADR zastąpiony po akceptacji”, retro 2, R7) **się nie zapala**. Jeśli
  uznasz to za zastąpienie — powiedz, a `pm` zaproponuje `architect`.
- **Decyzje projektowe ze specyfikacji** (do potwierdzenia tym samym „tak”):
  - płeć nowej osoby w arkuszu ([[rodzina]] D14, A3'a) — bez niej osoby z arkusza psułyby stryja i wuja;
  - z arkusza znika „Rodzina i jej daty zapiszą się ze źródłem: notatki.” (SPIKE-004 D28 obejmuje całą aplikację);
  - po końcu związku chip zostaje „Mąż”, nie „Były mąż” ([[rodzina]] D13);
  - w liście nawias ze ścieżką przy krewnych bocznych i powinowatych, bez nawiasu w linii prostej ([[osoby]] D8);
  - powinowactwo przez „Razem” to opis („tata partnerki”), bo „teść” znaczy rodzica małżonka (SJPD).

### Scope — files (`{code}`) — runda 2
| Plik | Co |
|---|---|
| `lib/data/database.dart` | `enum Sex { female, male }`; `Persons.sex` — `textEnum<Sex>().nullable()` (pusto = nieznana, `U`); `EventType.together` („Razem od”, eksport `EVEN`+`TYPE`) dopisany **na końcu** enuma; komentarz nagłówka bez „No sex”. **Schemat v7**, krok `_from6To7`: `m.addColumn(schema.persons, schema.persons.sex)` — żadnego wiersza nie dodaje (odtworzenie liczy wiersze, `restore_service.dart` → `_migrate`) |
| `drift_schemas/grobing/drift_schema_v7.json`, `database.steps.dart`, `test/drift/grobing/generated/*` | `dart run drift_dev make-migrations` (README → *Baza danych*, podbicie wersji) |
| `lib/data/graves.dart` | `PersonEntry.sex`, `BuriedPerson.sex` (i `entry`), `_buried` czyta `sex`, zapis w obu `PersonsCompanion`; `PersonChoice.sex` (lista wyboru osoby — płeć istniejącej osoby do nazwy roli). `bioSource` w danych bez zmian: nowa osoba — `defaultBioSource`, poprawa — wartość z bazy |
| `lib/data/families.dart` | **jedna droga zapisu zostaje: `saveFamily`** — kreator, podsumowanie i „Dodaj dziecko” budują `FamilyDraft` z `loadFamily` i jednej zmiany. Dochodzi: `FamilyMember.sex`; `PersonUnion` i `FamilyDetail`: `married` (jest zdarzenie `marriage`, także bez daty) i `together`; `FamilyDraft`: `married`, `together`; `NewMember.sex` → `_addPerson`. Pętla dat (339–361): para `(EventType.together, draft.together)`; **ślub przy `married` zapisuje się także bez daty** (zdarzenie z twierdzeniem) i nie jest kasowany; `married = false` kasuje ślub z twierdzeniami. Związki w `loadRelations` według pierwszej daty związku (razem od, a bez niej ślub). Reguły składu bez zmian (para z jedną osobą i dzieckiem — „Nie wiem” przy tacie — przechodzi już dziś, D6) |
| `lib/app/family/union_wizard.dart` (nowy) | [[rodzina]] C: arkusz modalny od dołu, kroki C0–C3b i tryb „rodzice” (C-r1, C-r2 przy P1); oś czasu nad pytaniem; „Nie znam daty”; okno „Przerwać dodawanie?”; zapis na ostatnim kroku przez `saveFamily` |
| `lib/app/family/person_choice_list.dart` (nowy, z `person_picker_screen.dart`) | lista B (B2–B5, wiersze nieaktywne z powodem) jako widżet do arkusza, bo krok „Z kim?” i E jej używają; ekran B jako osobna trasa znika razem z arkuszem A |
| `lib/app/family/union_summary_sheet.dart` (nowy) | [[rodzina]] D: wiersze Partner/Mama/Tata · Razem od · Ślub · Koniec → jeden krok kreatora z obecną wartością; „To nie było małżeństwo”; dzieci z `close` (C1); „Usuń związek” → `deleteFamily` z oknem; „Gotowe” |
| `lib/app/family/add_child_sheet.dart` (nowy) | [[rodzina]] E: „Dziecko Marii i Jana”, lista B w trybie „dziecko”, nowa osoba z ♀ ♂ i „Dodaj”; przy C2 — krok „Z kim?” |
| `lib/app/family/family_section.dart` | [[wpis-osoby]] 9a v5.6: „Rodzice · oś czasu” z ✎ i chipami „Matka”/„Ojciec” albo „Dodaj rodziców” (P1); „Partnerzy” — karta na związek (profilowe, imię, „lata · rola”, oś czasu, ✎), dzieci pod kartą z „Dodaj dziecko” (C1); „Dodaj partnera” / „Dodaj kolejnego partnera”. Nazwy ról z płci i `married` ([[rodzina]] *Role names*) — mała funkcja w tym pliku |
| `lib/app/family/family_sheet_screen.dart`, `person_picker_screen.dart` | **usunięte** (zwykłe skasowanie pliku i `git add -- <ścieżka>` w paczce — nie `git rm`, `git-autonomy-boundary.md`) |
| `lib/app/widgets/sex_toggle.dart` (nowy) | [[wpis-osoby]] 4a v5.6: ♀ `female_outlined`, ♂ `male_outlined`, 48 × 56 dp, pusty wybór dozwolony, wybrana — powierzchnia, obrys 2 dp i ikona w akcencie, `tooltip` i semantyka „Kobieta”/„Mężczyzna”, „zaznaczone”; **poza kolejnością `next`** (jak `qualifierNode` w `DateBlock`) |
| `lib/app/polish.dart` | `suggestSex(givenNames)`: pierwsze imię na „-a” → kobieta, inaczej mężczyzna; wyjątki → mężczyzna (Kuba, Bonawentura, Dyzma, Kosma, Jarema, Kuźma, Barnaba); bez imion — `null` |
| `lib/app/grave/person_form_screen.dart` | 4a w wierszu „Imiona” (pole węższe); podpowiedź na bieżąco z „Imiona”, dopóki autor nie dotknie ikony; w poprawie zapisana płeć, a bez niej podpowiedź **jako wartość początkowa** (snapshot), żeby „wstecz” bez zmian nie pytało „Odrzucić wpis?”. **Usunąć** `_sourceLine` (element 9 z „Zmień” i walidacją „Podaj źródło…”) i tekst elementu 10 |
| `lib/dev/fictional_data.dart` | płeć wymyślonych osób (ojciec M, matka i partnerka K, jedno dziecko bez płci); jeden związek „razem od” przed ślubem — liczniki w `data_state_test.dart` i `data_state_screen_test.dart` poprawić o nowe zdarzenie i twierdzenie |
| `README.md` (`grobing-code`) | *Baza danych*: wpis v7 (płeć, „Razem od”, ślub bez daty); wpis v6 bez „Płci w modelu nie ma” |

Bez zmian w tej pozycji: zakładka Osoby (lista bez pokrewieństwa — jak dziś), `people.dart`, `theme.dart` (tokeny
wystarczą).

### AC → implementation → test (testy pisze `qa`) — runda 2
| AC | Gdzie | Test happy-path |
|---|---|---|
| AC-1 | `polish.dart`, `sex_toggle.dart`, `person_form_screen.dart`, `graves.dart` | jednostkowy: `suggestSex` („Maria” → K, „Jan” → M, „Kuba” → M, pusto → `null`); widżet: „Maria” → ♀ zaznaczona, „Zapisz” → `persons.sex = female`, poprawa pokazuje ♀; 5× `next` przechodzi przez te same pola co dziś (ikony poza kolejnością) |
| ~~AC-2~~ → [[ISSUE-024-person-view]] (R2-D3) | — | — |
| AC-3 | `union_wizard.dart`, `families.dart`, `family_section.dart`, `union_summary_sheet.dart` | danych: „Razem od” 1980 + ślub 1985 → dwa zdarzenia z twierdzeniami, odczyt oba; ślub bez daty przeżywa kolejny zapis; „To nie było małżeństwo” kasuje ślub; widżet: kreator Jan → „Razem” 1980 → „Wzięli ślub” 1985 → „Nic więcej — zapisz” → karta „razem od 1980 · ślub 1985”, rola „Mąż”; „Małżeństwo” + „Nie znam daty” → karta „Małżeństwo”, „Mąż”; „Razem” bez ślubu → „Partner” |
| AC-4 | `database.dart` (v7), `restore_service.dart` (bez zmian) | migracja v6→v7 z danymi (`testWithDataIntegrity`): wiersze i `id` bez zmian, `sex` pusta; odtworzenie kopii v6 w v7: liczniki zgodne, osoby bez płci, związki bez „Razem od”, rodzina ze ślubem — „Mąż/Żona”, bez — „Partner”; `user_version` 7, „Wersja schematu” 7 |
| AC-5 | `person_form_screen.dart`, kreator i arkusze | widżet: w nowej osobie i w poprawie brak tekstów „Źródło”, „Zmień”, „zapiszą się ze źródłem”, „Poprawa nie zmienia źródła”; w kreatorze i arkuszach rodziny też |
| P1 (R2-D2) | `union_wizard.dart` | widżet: „Dodaj rodziców” → nowa „Zofia” jako mama (♀ bez wyboru) → „Nie wiem” przy tacie → zapis od razu ([[rodzina]] C-r2) → chip „Matka: Zofia”, rodzina z jedną osobą w parze i dzieckiem; drugi przebieg z tatą → „Małżeństwo” → „Rodzice · ślub …” |
| C1 (R2-D1) | `add_child_sheet.dart`, `family_section.dart` | widżet: „Dodaj dziecko” na karcie → nowa „Anna” (♀) → chip „Córka: Anna” pod tą kartą; dziecko z grobu → chip; ✕ w podsumowaniu usuwa łącze, osoba zostaje |

Testy do przepisania: `test/app/family/family_screens_test.dart` (arkusz A i ekran B znikają — scenariusze US-003 AC-1,
AC-2, AC-3, AC-5 przechodzą na kreator, kartę i E; muszą zostać zielone, bo US-003 jest zamknięta); `grave_screens_test.dart`
251, 253 (źródło); `database_test.dart`, `data_state_screen_test.dart` (wersja 6 → 7).

### Data layer
- **Schemat v7** z testem migracji v6→v7 na danych (NFR-003); nowy plik schematu i helpery testów z `make-migrations`.
- **Próbne odtworzenie:** test kopii v6 → v7 (AC-4) i kopii v7 z płcią, „Razem od” i ślubem bez daty (odcisk zgodny). Na
  emulatorze: kopia z `Medium_Phone` z nowym hasłem testowym → `Grobing_Restore` (agent).
- **Źródło i status faktu:** „Razem od”, ślub (także bez daty), koniec, para i łącze dziecka zapisują się z twierdzeniem
  „notatki”, `CLAIMED` (po cichu, SPIKE-004 D28) — ta sama droga co dziś (`saveFamily`). Płeć bez twierdzenia, jak imiona
  ([[FR-001-provenance]]: twierdzenia na datach, relacjach, pochówku).
- **ADR-012** (D4) i wpis v7 w [[data-model]] → `docs` przy zamknięciu; dopisek w *Follow-ups* ADR-011. Przy C1 także nowe
  brzmienie [[FR-002-rodzina-jako-rekord]] i [[US-003-przepisanie-rodziny]] AC-1 (R2-D1) i AC-2 w [[ISSUE-024-person-view]] (R2-D3).

### Manual verification — runda 2
**Agent na emulatorze** (`Medium_Phone`, build release jako aktualizacja na danych testowych v6), zrzuty przed stopem #2:
1. Po aktualizacji: dane całe, `user_version` 7, `persons.sex` puste; rodziny z ISSUE-019 jako karty (ze ślubem — „Mąż”/„Żona”,
   bez — „Partner”).
2. Formularz: „Maria” → ♀, „Kuba” → ♂, ręczny wybór wygrywa z dalszym pisaniem, drugie dotknięcie zdejmuje wybór; `next` z
   „Imiona” idzie do „Nazwisko”; zapis → `sex` w bazie; poprawa starej osoby pokazuje podpowiedź, a „wstecz” bez zmian nie pyta.
3. Kreator partnera: „Razem” 1946 → „Wzięli ślub” ok. 1948 → „Związek się zakończył” 1960 → karta z osią czasu; drugi
   partner „Małżeństwo” + „Nie znam daty”; „wstecz” w krokach i „Przerwać dodawanie?”.
4. Podsumowanie: dodanie „Razem od” do starej rodziny, „To nie było małżeństwo”, ✕ dziecka, „Usuń związek” z oknem.
5. Dzieci (C1) i rodzice (P1): dziecko z grobu i nowe „Anna” → „Córka: Anna”; rodzice — mama nowa, tata „Nie wiem”.
6. Nigdzie tekstu o źródle; `uiautomator`: ikony płci z nazwą, `checked` i `clickable`; karty-opcje i karta partnera
   `clickable`.
7. Próbne odtworzenie na `Grobing_Restore`: odcisk zgodny; płeć, „Razem od” i ślub bez daty te same.

**Autor: odczucie** (najwyżej 3):
1. Dodaj partnera kreatorem, z ewolucją „razem → ślub”: czy kolejność pytań jest naturalna.
2. Popraw jedną datę na karcie przez ✎: czy jest tam, gdzie jej szukasz.
3. Wpisz dwie osoby: czy podpowiedź ♀ ♂ widać i czy nie spowalnia wpisu.

Przegląd ekranów `ui` (subagent `qa`) przed stopem #2; zmienione ekrany → `dev` przechodzi AC na emulatorze przed `qa`.

### Out of Scope
- **Słownik pokrewieństwa, ścieżka do „ja” i AC-2** → [[ISSUE-024-person-view]] (R2-D3); kanon zostaje w *Prior art*, tabela
  w rundzie 0 (D2).
- Pokrewieństwo w zakładce Osoby — **nie będzie** (decyzja autora, [[osoby]] v2.2).
- Drzewo z linią przerywaną od „Razem od” i ciągłą od ślubu ([[drzewo]] D4) → [[SPIKE-002-tree-on-a-phone]].
- „Były mąż” po końcu związku ([[rodzina]] D13); płeć `X`.
- Kontrola cykli w rodzinie (poza blokadą „ta osoba” w kroku „Kto jest mamą?”); twarde spacje w nazwach ([[style-b]]
  reguła 6 — osobna drobna pozycja).
- Eksport GEDCOM (`EVEN`+`TYPE` dla „Razem od”, `MARR Y`) → [[US-006-eksport-dla-rodziny]].

## Dev report
> `dev`, 2026-10-08. Stop #1, runda 2: „C1 / P1 / Jest dobrze”. Flutter 3.41.1 zgodny z przypiętym. `dart format` i
> `flutter analyze lib`: czyste. Schemat v7. Testy w `test/` (poza wygenerowanymi helperami migracji) należą do `qa`.

### What was built (`{code}`)
- **Schemat v7** (`lib/data/database.dart`): `enum Sex { female, male }`, `persons.sex` (pusta = nieznana), `EventType.together`
  na końcu enuma; krok `_from6To7` = `addColumn(persons.sex)`, bez nowych wierszy. `drift_schema_v7.json`,
  `database.steps.dart` i helpery `test/drift/grobing/generated/` z `make-migrations`.
- **Dane** (`lib/data/families.dart`, `graves.dart`): płeć w `PersonEntry`, `BuriedPerson`, `PersonChoice`, `FamilyMember`,
  `NewMember`; `FamilyDraft` ma `together`, `married`, `ended` (bez flag decyduje sama data — stare wywołania działają jak
  przed v7); ślub albo koniec bez daty to zdarzenie bez daty z twierdzeniem „notatki”, `CLAIMED`; `married`/`ended` =
  false kasuje zdarzenie z twierdzeniami. `PersonUnion`/`FamilyDetail` niosą oś czasu; `PersonRelations.parentsUnion` —
  oś czasu związku rodziców. Związki według pierwszej daty (razem od, a bez niej ślub). Jedna droga zapisu: `saveFamily`.
- **Formularz osoby** (`person_form_screen.dart`): ♀ ♂ w wierszu „Imiona” (`lib/app/widgets/sex_toggle.dart`), podpowiedź z
  `suggestSex` (`polish.dart`, wyjątki z pomiaru PESEL) na bieżąco, dopóki autor nie dotknie ikony; w poprawie bez płci
  podpowiedź jest wartością początkową (snapshot). Element 9 (źródło „kim była”, „Zmień”, „Podaj źródło…”) i tekst
  elementu 10 usunięte; `bioSource` w danych: poprawa zostawia zapisany, nowa osoba — „notatki”.
- **Kreator związku** (`lib/app/family/union_wizard.dart`, rodzina.md C): arkusz od dołu, kroki „Z kim?” → (nowa osoba z ♀ ♂)
  → „Jaki to był związek?” (Razem / Małżeństwo + data albo „Nie znam daty”) → „Co było dalej?” (Wzięli ślub · Związek
  się zakończył · Nic więcej — zapisz); tryb rodziców P1: „Kto jest mamą?” → „Kto jest tatą?” („Nie wiem — zapisz”) →
  związek; walidacja kolejności („Ślub nie może być przed „Razem od”.”, „Koniec nie może być przed początkiem związku.”);
  „Przerwać dodawanie?”.
- **Podsumowanie związku** (`union_summary_sheet.dart`, rodzina.md D): wiersze Partner/Mama/Tata/Rodzic · Razem od · Ślub ·
  Koniec, każdy jednym krokiem; „To nie było małżeństwo”, „Usuń koniec”, „Usuń” przy „Razem od”; dzieci z ✕ („ta
  osoba” bez ✕); „Usuń związek” z oknem; „Gotowe”.
- **Dodaj dziecko** (`add_child_sheet.dart`, rodzina.md E, C1) i lista osób jako widżet arkusza (`person_choice_list.dart`,
  dawny ekran B).
- **Sekcja „Rodzina”** (`family_section.dart`, wpis-osoby.md 9a v5.6): „Rodzice · <oś czasu>” z ✎ i chipami z płci albo
  „Dodaj rodziców”; „Partnerzy” — karta na związek (inicjały, imię i nazwisko, „lata · rola”, oś czasu, ✎), pod nią „Dzieci
  z tego związku” i „Dodaj dziecko”; „Dodaj partnera” / „Dodaj kolejnego partnera”. Nazwy ról z płci i ślubu.
- **Usunięte:** `family_sheet_screen.dart` (arkusz A) i `person_picker_screen.dart` (ekran B jako trasa) — do paczki przez
  `git add -- <ścieżka>` skasowanego pliku, nie `git rm`.
- **Wymyślone dane** (`lib/dev/fictional_data.dart`): płeć ojca, matki i partnerki; drugi związek z „Razem od” ok. 1922 przed
  ślubem 1925 (+1 zdarzenie, +1 twierdzenie — liczniki testów `data_state` do poprawy przez `qa`).
- **README** → *Baza danych*: wpis v7; wpis v6 bez „Płci w modelu nie ma”.

### Deviations (do przeglądu `ui`)
1. **Karta partnera — same inicjały**, bez profilowego (spec: „profilowe albo inicjały”): `FamilyMember` nie niesie zdjęcia, a
   dociągnięcie profilowych to osobny odczyt. Kandydat na ISSUE-024 (widok osoby i tak czyta zdjęcia).
2. **„Kto jest mamą?” ma też „Nie wiem — przejdź do taty”** (spec C-r1 go nie ma): notatki bywają tylko z ojcem; bez tego
   rodziców z samym ojcem nie dałoby się dodać kreatorem.
3. **E bez odmiany imion:** „Dziecko tej pary” + „Ewa i Kuba” zamiast „Dziecko Marii i Jana” — zła odmiana imienia razi
   ([[grob]] D1), a aplikacja nie ma słownika odmian. Tak samo krok C1: „Z kim w związku?” + imię i nazwisko pod spodem.
4. **„Nie znam daty” przy końcu związku** zapisuje koniec bez daty (flaga `ended`, jak `married`) — plan wymieniał tylko
   `married`; bez tego przycisk z C3b nie miałby czego zapisać.
5. **„Razem od” w podsumowaniu ma „Usuń”, nie „Nie znam daty”:** „razem” bez daty to po prostu związek bez ślubu.
6. **Istniejąca osoba wybrana jako „tata” bez płci zostaje bez płci** (wiersz „Rodzic”, chip „Rodzic”) — płci nie zgadujemy
   (D3); nowa osoba w kroku „mama”/„tata” dostaje płeć z pytania, jak w spec.
7. **Ikony kart-opcji** (spec: „wybiera przegląd `ui`”): Razem `favorite_border`, Małżeństwo i „Wzięli ślub”
   `diamond_outlined`, koniec `heart_broken_outlined`, zapis `check`, „Nie wiem” `help_outline`.
8. **Arkusze nie zamykają się przeciągnięciem ani dotknięciem tła** — tylko ✕ i „wstecz” (C0: zamknięcie z oknem
   „Przerwać dodawanie?”).

### Found on the emulator (AC przed `qa`, R5)
`Medium_Phone`, build release jako aktualizacja na danych testowych v6 (zrzuty w katalogu tymczasowym sesji, `shots/`):
- migracja: aplikacja wstała, „Stan danych” — wersja schematu 7, dane całe; osoby sprzed v7 bez płci;
- formularz Ewy: ♀ podpowiedziana z imienia (`checked`), bez linii źródła; „wstecz” bez zmian — bez okna;
- podsumowanie związku Ewy i Jana: „Razem od” 1990 → zapis; ślub „Nie znam daty” → „bez daty”; „To nie było małżeństwo” →
  karta „Partner · razem od 1990 · koniec 1995”;
- kreator „Kolejny partner”: „Kuba” → ♂ (wyjątek), „Razem” 2000 → ślub 1999 odrzucony („Ślub nie może być przed „Razem
  od”.”) → 2002 → „Nic więcej — zapisz” → karta „Kuba Testowy · bez dat · Mąż · razem od 2000 · ślub 2002”;
- „Dodaj dziecko” na karcie Kuby: nowa „Anna” → ♀ → chip „Córka: Anna” pod tą kartą;
- rodzice Kuby (P1): nowa „Zofia” jako mama (♀ bez wyboru) → „Nie wiem — zapisz” → „Rodzice”, „Matka: Zofia”; potem w
  podsumowaniu tata z listy i ślub bez daty → „Rodzice · Małżeństwo”;
- **błąd znaleziony i poprawiony:** w kroku „Jaki to był związek?” pod pytaniem stało „Ewa i Kuba · Razem”, zanim
  cokolwiek podano — oś czasu pokazuje się teraz od kroku „Co było dalej?”. Poprawka po przejściu: do sprawdzenia na
  nowym buildzie przez `qa`.
- przy okazji (poza zakresem): podpowiedziane nazwisko nowej mamy to forma syna („Testowy”) — znany punkt „do odczucia”
  ([[wpis-osoby]] *Open*), i lista „Dziecko tej pary” pozwala wybrać byłego partnera tej osoby (kontrola cykli — *Out of
  Scope*).

### For `qa` — kroki ręczne
Według *Manual verification — runda 2* wyżej; dodatkowo: przepisać `test/app/family/family_screens_test.dart` (arkusz A i
ekran B nie istnieją — scenariusze US-003 przez kreator, podsumowanie i E), poprawić liczniki `data_state` (wymyślone dane
+1 zdarzenie, +1 twierdzenie), wersję 6 → 7 w testach, teksty źródła w `grave_screens_test.dart`.

## Verification
> `qa`, 2026-10-08. Rytuał WZ-024: `dart format` (0 zmian) → `flutter analyze` (czysto) → `flutter test` (**503**, zielone) →
> kroki agenta na emulatorze → przegląd `ui` → poprawki `dev` → stop #2.

### Tests (happy path per AC)
| AC | Test |
|---|---|
| AC-1 | `polish_test.dart` „ISSUE-025 AC-1 — suggestSex…” (Maria, Anna Zofia → K; Jan, Józef Maria, Kuba, Barnaba → M; puste → brak) · `grave_screens_test.dart` „AC-1…AC-4” (Jan → ♂ `checked`, Anna → ♀, w bazie `male`, `female`) i „ISSUE-025 AC-1, D-płeć…” (poprawa bez płci zaczyna od podpowiedzi, „wstecz” bez zmian nie pyta; zapisanej płci imię nie zmienia) · `family_screens_test.dart` C1' (Kuba → ♂) i P1 (mama ♀ z pytania) |
| ~~AC-2~~ | przeniesione do [[ISSUE-024-person-view]] (stop #1, R2-D3) |
| AC-3 | `families_test.dart` „ISSUE-025 AC-3 — "Razem od" 1980 and the wedding 1985…”, ślub bez daty (`MARR Y`) przeżywa zapis, „To nie było małżeństwo”, koniec bez daty, data dla ślubu, którego nie było — odmowa, płeć nowej osoby, kolejność związków · `family_screens_test.dart` „US-003 AC-3 / ISSUE-025 AC-3” (kreator: Razem 1980 → ślub 1975 odrzucony → 1985 → karta „razem od 1980 · ślub 1985”, „Mąż”), ślub bez daty → „Małżeństwo”, podsumowanie D |
| AC-4 | `migration_test.dart` „ISSUE-025 AC-4 — v6 to v7…” (`testWithDataIntegrity`: wiersze i `id` bez zmian, `sex` puste) · `restore_service_test.dart` „ISSUE-025 AC-4 — a v6 backup restores into the v7 app…” (liczniki zgodne, bez płci, bez „Razem od”, ślub → `married`) · pełna kopia → odtworzenie z płcią i „Razem od” (odcisk zgodny) · `database_test.dart` (v7, kolumna `sex`) |
| AC-5 | `grave_screens_test.dart`: nowa osoba i poprawa bez „Źródło”, „Zmień”, „ze źródłem”, „Poprawa nie zmienia źródła”; kreator, D i E nie mają tekstu źródła (przegląd `ui`, kod) |
| US-003 (zamknięta) | `family_screens_test.dart` — scenariusze AC-1, AC-2, AC-3, AC-5 przepisane na kreator, kartę i E (12 testów, zielone) |

Testy przepisał subagent (ekrany rodziny) i `qa` (dane, migracja, kopia, formularz). Wymyślone osoby: Wymyślony, Testowa,
Zmyślona, Przykładowe; imiona Jan, Maria, Anna, Kuba, Zofia.

### Agent na emulatorze (przed stopem #2)
Build release jako aktualizacja na danych testowych v6 (`Medium_Phone`), potem nowy build po poprawkach (`Grobing_Restore`);
zrzuty w katalogu tymczasowym sesji (`shots/`), wymyślone osoby:
1. ✅ Aktualizacja: „Stan danych” — schemat 7, dane całe; osoby sprzed v7 bez płci, w formularzu podpowiedź z imienia.
2. ✅ Formularz: „Ewa” → ♀, „Kuba” → ♂ (wyjątek); ręczny wybór wygrywa; „wstecz” bez zmian — bez okna; bez linii źródła.
3. ✅ Kreator partnera: „Razem” 2000 → ślub 1999 odrzucony (czerwona ramka i komunikat) → 2002 → karta „Mąż · razem od
   2000 · ślub 2002”; kursor sam w dacie, klawisz „gotowe” robi „Dalej”; „Przerwać dodawanie?” — „Przerwij” nic nie zapisuje.
4. ✅ Podsumowanie: „Razem od” 1990, ślub „Nie znam daty” → „bez daty”, „To nie było małżeństwo” → „Partner”.
5. ✅ Dzieci (C1) i rodzice (P1): nowa „Anna” → „Córka: Anna” pod kartą; nowa mama „Zofia” (♀ z pytania) → „Nie wiem — zapisz”;
   tata z listy i ślub bez daty → „Rodzice · Małżeństwo”.
6. ✅ `uiautomator`: ♀/♂ — `clickable` i `checked`; karty-opcje i karta partnera `clickable`; karta czyta „otwórz wpis”.
7. ✅ **Próbne odtworzenie:** na `Medium_Phone` „Skonfiguruj kopię od nowa” z nowym hasłem testowym, kopia do Pobranych
   (`grobing-klucz-025.age`, `grobing-kopia-025.age`, wymyślone dane), odcisk źródła `9344e604acc5c681`; pliki przeniesione `adb`
   na `Grobing_Restore`, tam „Odtwórz z kopii” → „Zastąp dane” → **odcisk `9344e604acc5c681` — zgodny**, schemat 7; na ekranie
   wróciły płeć, „razem od”, ślub i „Córka: Anna”.

### `ui` review (subagent, bez historii)
0 BLOCKER, 2 MAJOR, 7 MINOR; odstępstwa `dev` 1–7 przyjęte, 8 (ikona końca) do zmiany. **Wszystkie poprawione przed stopem #2**
(`dev`), sprawdzone na nowym buildzie:
- MAJOR: „Nie znam daty” w kolorze tekstu, nie w akcencie (reguła 1; błąd był w specyfikacji C2);
- MAJOR: „Nie wiem” przy mamie → wybór taty zapisuje od razu („krok 2 z 2”), bez pytania o związek jednej osoby (+ test);
- MINOR: kursor w dacie po wejściu w krok i klawisz „gotowe” = przycisk kroku (`DateBlock.onDone`); błąd kolejności barwi ramkę
  pola (`DateBlock.error`); „←” także na kroku 1 (zamyka); karta partnera — opis „otwórz wpis”; karta bez partnera i bez dat — bez
  „Razem”; ikona końca `call_split_outlined` zamiast złamanego serca; karty-opcje nieaktywne w trakcie zapisu.

Znaleziska z testów (subagent): dolny wiersz podsumowania zawija się (`Wrap`) przy dużym tekście; tytuł „Kolejny partner”, gdy
osoba ma jakikolwiek związek — poprawione.

**Do specyfikacji (`ui`, przed commitem paczki):** [[rodzina]] v2.1 — C0 bez uchwytu i przeciągania, C1 „Z kim w związku?”, C2
„Nie znam daty” w kolorze tekstu, C-r1 „Nie wiem — przejdź do taty” i zapis od razu, C3b koniec bez daty, D („Rodzic”, „Dzieci”,
„Usuń” przy „Razem od”), E „Dziecko tej pary”, ikony kart-opcji; [[wpis-osoby]] 9a — „Rodzice · Małżeństwo”, karta bez
partnera, opis karty dla czytnika.

### Family data
Paczka kodu (31 plików) i vaulta: suchy przebieg strażnika (`git add -- <lista>`) — przechodzi; bez baz, kopii, eksportów i
zdjęć; w testach, zrzutach i danych emulatora wyłącznie wymyślone osoby. Pliki kopii `-025` leżą tylko na emulatorach i w
katalogu tymczasowym sesji.

### Not covered (named)
- Na żywo przez nikogo: TalkBack i powiększenie tekstu 200% w kreatorze (wiersz podsumowania zawija się — test).
- Testem: zastąpienie partnera z wiersza D, „Usuń koniec”, daty z kilku źródeł w D, komunikaty nieudanego zapisu, menu dopisku
  w kreatorze.
- Znane, poza zakresem: podpowiadane nazwisko w formie osoby z wpisu (mama „Testowy”) — [[wpis-osoby]] *Open*; lista „Dziecko
  tej pary” pozwala wybrać byłego partnera (kontrola cykli).

### Stop #2 — runda 1 (2026-10-08)
- Kroki 1–3 (kreator z „ewolucją”, ✎ jednej daty, ♀ ♂ przy nowych osobach): **„ok”** — *„1-2-3 UX jest dobrze”*, z uwagą:
  *„chciałbym aby ten pop-up był mniej więcej w tym samym miejscu - aby po otwarciu się klawiatury ten pop-up nie przesuwał
  się stale góra-dół”* → `dev`: arkusze kreatora, podsumowania i dziecka mają **stałą wysokość** (ok. 92% ekranu), klawiatura
  zmniejsza treść, przyciski kroku przypięte nad nią (`SheetPage`); test „C0 — the sheet stands in one place…” (górna
  krawędź ta sama na każdym kroku i przy klawiaturze, „Dalej” nad klawiaturą); na emulatorze nagłówek arkusza na tej samej
  wysokości w krokach 1–2, z klawiaturą i bez. [[rodzina]] v2.1 (C0). Testy: **504**.
- Uwaga autora: *„po wybraniu osoby najpierw wejść w jej »profil« z najważniejszymi informacjami a dopiero potem w edycję
  (aby oglądanie danej osoby nie mieszało się z edycją tej osoby) (chyba że to inne zadanie)”* → **to [[ISSUE-024-person-view]]**
  (widok osoby, [[osoba]] D1, [[style-b]] reguła 15); karty i chipy otwierają poprawę tymczasowo, do niego. Bez zmiany zakresu
  tutaj — `docs` dopisze uwagę jako wejście ISSUE-024.
- Pytanie o płeć z odpowiedzi „mama/tata” dla osoby bez płci: **bez odpowiedzi** — zachowanie bez zmian (D3), pytanie
  powtórzone w rundzie 2.

### Stop #2 — runda 2 (2026-10-08)
- Krok 1 (arkusz przy klawiaturze): **„ok”**. Sprawdzone na urządzeniu (`Grobing_Restore`): autor przy okazji usunął oba
  związki Ewy („Usuń związek”, *„Ja usunąłem ich przed chwilą”*) — „Stan danych”: rodziny 5 → 3, dzieci w rodzinach 6 → 4,
  zdarzenia 11 → 7, twierdzenia 27 → 19, osoby bez zmian (10): usunięcie zabrało powiązania i daty związku, osoby zostały
  (rodzina.md D8).
- Pytanie o płeć z odpowiedzi „mama/tata”: **bez odpowiedzi „tak/nie”** — zostaje D3 (płci nie wpisujemy bez wyboru
  ikony); sprawa dla autora przy zamknięciu.

**Werdykt `qa`: APPROVED (self-check, z uwagami)** — każde AC (bez AC-2, przeniesionego do ISSUE-024) ma test i przejście na
emulatorze; migracja v6→v7 i odtworzenie kopii v6 w v7 przechodzą; próbne odtworzenie na drugim emulatorze — odcisk zgodny;
przegląd `ui` rozliczony; stop #2 „ok”. Uwagi: TalkBack i tekst 200% nie sprawdzone na żywo; podpowiadane nazwisko w formie
osoby z wpisu; kontrola cykli poza zakresem.
