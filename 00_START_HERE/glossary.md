---
title: "Grobing — Glossary"
type: meta
status: active
created: 2026-10-05
updated: 2026-10-08
---

# Grobing — Glossary

> Wspólne definicje dla TEGO produktu — chronią przed rozjazdem pojęć. Treść po polsku, nazwy pól
> i nagłówki po angielsku (Meta-decyzja 1).

## Work-item hierarchy (Meta-decision 2)

| Term | Definition in this product |
|---|---|
| EPIC | Jeden etap procesu genealoga z własną wartością (np. *Zabezpiecz i przepisz*, *Wizyta*, *Zrozumienie*). Dokument wymagań, nie wielka karta backlogu. |
| US (User Story) | Jedna rzecz, którą Zbierający robi od początku do końca, wyprowadzona z 1-3 kolejnych kroków ścieżki wizyty (UJ-001) — albo z jednej funkcji widoku 5. |
| ISSUE | Jeden komponent US, **do kliknięcia w aplikacji** (do MVP na emulatorze — `DEFINITION_OF_DONE.md`), ~0,5-1 dnia (`delivery-style: task-level`). |
| SPIKE | Pytanie z limitem czasu i warunkiem wyjścia; kod z eksperymentu **nie zostaje**. |
| NT (non-tech item) | Sprawa poza kodem: prawna, koszt, przekazanie rodzinie, przepisywanie notatek. |
| DEF (deferred item) | Wymóg odłożony z **triggerem-zdarzeniem**, nie datą. |
| FR · NFR · AC | Wymaganie funkcjonalne (trwałe, przeżywa każdą US) · niefunkcjonalne (z miarą i sposobem sprawdzenia) · kryterium akceptacji (Given/When/Then, jedno na US). |

> Hierarchy chosen: **COMPONENT**. Delivery style: **task-level**. Numeracja osobna per prefiks;
> **nigdy nie zgaduj numeru — znajdź najwyższy istniejący** (wzorzec z wcześniejszej aplikacji autora).

## Domain terms

| Term | Czym jest | Czym NIE jest |
|---|---|---|
| **kwatera** | **sektor cmentarza** w adresie zarządcy (kilkanaście–kilkadziesiąt grobów, często więcej); na mapie cmentarza — nazwana strefa, którą **zaznacza autor** według planu zarządcy ([[ADR-003-map-source-offline]]) | pojedynczym grobem ani miejscem jednego grobowca — tak rozumiał to słowo autor do 2026-10-08 (SPIKE-001); w danych to pole `sector` |
| **rząd · miejsce** | dalsza część adresu zarządcy: kwatera → rząd → miejsce | współrzędnymi GPS |
| **grób** (Grave) | miejsce na cmentarzu z adresem, pinezką i zdjęciami nagrobka | osobą — w grobie rodzinnym leży kilka osób |
| **nazwa grobu** | opcjonalny tytuł grobu nadany przez autora, np. „Grób rodzinny Nowaków” ([[ISSUE-012-transcribe-grave-screen]], schemat v3) | nazwiskiem osób — aplikacja nie wylicza jej z nazwisk, bo odmiana bywa błędna; bez nazwy grób ma tytuł „Grób” |
| **pochówek** (Burial) | powiązanie osoba ↔ grób (wiele na jeden grób) | zdarzeniem z datą (data pochówku to Event) |
| **pinezka** | pozycja grobu na mapie **ze źródłem** (postawiona przez autora na planie albo na ortofotomapie / GPS na miejscu) i dokładnością | prawdą o położeniu — prawdą jest adres zarządcy; ani pozycją przejętą z map zarządców (tych nie kopiujemy — [[ADR-003-map-source-offline]]) |
| **plan cmentarza** | schematyczna mapa cmentarza w aplikacji: obrys i alejki z OSM (offline) + kwatery i pinezki autora ([[ADR-003-map-source-offline]]) | planem zarządcy (Grobonet, tablica przy bramie) — ten jest tylko odnośnikiem dla autora |
| **rodzina** (Family) | rekord: **związek** (małżeństwo albo nie) 1-2 partnerów + dzieci; osoba może być partnerem w kilku rodzinach — kolejny związek po rozstaniu albo owdowieniu to kolejna rodzina ([[ISSUE-019-family-relations]]) | „krawędzią" między dwiema osobami — to psuje się przy pierwszym powtórnym małżeństwie |
| **arkusz rodziny** | ekran, na którym wpisuje się jedną rodzinę naraz: parę, dzieci, ślub i koniec związku ([[rodzina]] A; kanon: *family group sheet*). Otwiera się z sekcji „Rodzina” formularza osoby, zapisuje się sam | formularzem osoby — relacji nie wpisuje się po jednej przy osobie, tylko widać je tam jako chipy |
| **nazwisko rodowe** | nazwisko z urodzenia (panieńskie) | nazwiskiem po ślubie |
| **data z dopiskiem** | data + kwalifikator: dokładnie / około / przed / po / między | błędem — „ok. 1890" to normalna dana |
| **twierdzenie** (Assertion) | fakt **ze źródłem** (nagrobek / notatki / babcia / krewny / akt) i statusem | gołą wartością pola |
| **status twierdzenia** | `CLAIMED` (jedno źródło) · `CONFIRMED` (drugie, niezależne) · `CONTRADICTED` (źródła się różnią — **zostaje**, to wynik) · `UNKNOWN` (wiem, że nie wiem) | oceną prawdziwości — status mówi, jak mocne jest twierdzenie, nie czy jest prawdziwe **Od 2026-10-08 niewidoczny i niezbierany w aplikacji** ([[SPIKE-004-mvp-flow-prototype]] D28); kolumny w schemacie zostają. |
| **„ja"** | wskazanie, która osoba w danych to autor — kotwica ścieżki pokrewieństwa | kontem użytkownika (kont nie ma) |
| **ścieżka pokrewieństwa** | najkrótsza droga po rodzinach między dwiema osobami, wyliczana na bieżąco | czymś zapisanym w bazie |
| **kopia** (backup) | pełna, **zaszyfrowana w telefonie**, automatyczna, sprawdzona odtworzeniem — do przywrócenia na nowym telefonie | eksportem |
| **eksport** | **czytelny bez aplikacji** (HTML + PDF), dla rodziny, przechowywany offline | kopią — nie da się go zaszyfrować, bo czytelność jest jego celem |
| **dane rodziny** | cokolwiek o prawdziwych osobach: imiona, daty, zdjęcia, pozycje grobów, pliki bazy, eksporty | dokumentacją, kodem albo danymi testowymi z **wymyślonymi** osobami |
| **zaparkowane** | sprawa czekająca na kogoś spoza sesji (babcia, cmentarz) z **warunkiem obudzenia** | blokadą łańcucha |
| **Zbierający** | jedyny użytkownik — autor (persona P1) | rodziną, która dziedziczy dane |
| **Źródło (osoba)** | babcia — najważniejsze żywe źródło faktów, z ograniczonym czasem | użytkowniczką aplikacji |
| **łącze zdjęcia** | powiązanie osoba ↔ zdjęcie z miejscem w kolejności zdjęć tej osoby (jak `OBJE` w GEDCOM 7; [[ADR-009-person-photos-record-and-link]]). Jedno zdjęcie może mieć łącza od kilku osób | kopią pliku — plik jest jeden; usunięcie zdjęcia z osoby usuwa łącze, nie zdjęcie |
| **profilowe** | pierwsze zdjęcie osoby (pierwsze łącze) — okrąg w formularzu, w karcie grobu i w nagłówku jej zdjęć; **osobne dla każdej osoby** | cechą zdjęcia — to samo zdjęcie grupowe może być profilowym jednej osoby i zwykłym zdjęciem drugiej |
| **kadr profilowego** | wycinek zdjęcia, który pokazuje okrąg profilowego — kwadrat w pikselach pliku, zapisany przy łączu osoby (`CROP` w GEDCOM 7; [[ADR-010-profile-photo-crop-pixels]]); bez kadru okrąg pokazuje środek zdjęcia | zmianą pliku — zdjęcie się nie zmienia, a każda osoba na zdjęciu grupowym ma własny kadr |
