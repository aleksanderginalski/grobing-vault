---
title: "Grobing — Data model"
type: data-model
status: active
source: "PROJECT_BRIEF §Architecture → Data model (accepted by the author, 2026-10-05)"
FR: ["[[FR-001-provenance]]", "[[FR-002-rodzina-jako-rekord]]", "[[FR-003-wiele-osob-w-grobie]]", "[[FR-004-data-z-dopiskiem]]", "[[FR-005-nazwisko-rodowe]]"]
ADR: ["[[ADR-001-local-first]]", "[[ADR-006-claimed-value-separate-structures]]"]
created: 2026-10-05
updated: 2026-10-06
---

# Grobing — Data model

> **Żywy dom modelu danych.** Brief (`kickoff/PROJECT_BRIEF.md` §Architecture → *Data model*) jest
> zamrożonym zapisem decyzji z kick-offu; zmiany modelu trafiają **tutaj** (a zmiana schematu w kodzie —
> z migracją, [[NFR-003-migracje-schematu]]).
>
> Zbudowany z kanonu (brief, Step 0): rodzina jako rekord, wiele osób w grobie, zdarzenia z niepewną
> datą, nazwiska rodowe, **źródło przy faktach**. Pojęcia mapują się jeden do jednego na GEDCOM
> (individual, family, event, source + quality) — **bez importu i eksportu GEDCOM**, więc eksport (C2)
> zostaje tani.

```mermaid
erDiagram
    PERSON ||--o{ FAMILY_PARTNER : "is partner in"
    FAMILY ||--o{ FAMILY_PARTNER : "has 1-2 partners"
    FAMILY ||--o{ FAMILY_CHILD : "has children"
    PERSON ||--o{ FAMILY_CHILD : "is child in"
    PERSON ||--o{ EVENT : "birth, death"
    FAMILY ||--o{ EVENT : "marriage, end"
    CEMETERY ||--o{ GRAVE : contains
    GRAVE ||--o{ BURIAL : "holds many"
    PERSON ||--o{ BURIAL : "buried in (one per claimed grave)"
    EVENT ||--|{ ASSERTION : "cited by"
    BURIAL ||--|{ ASSERTION : "cited by"
    FAMILY_PARTNER ||--|{ ASSERTION : "cited by (US-003)"
    FAMILY_CHILD ||--|{ ASSERTION : "cited by (US-003)"
    MEDIA }o--o| PERSON : shows
    MEDIA }o--o| GRAVE : shows
```

## Entities

| Entity | Carries | Why this shape |
|---|---|---|
| **Person** | imiona · nazwisko · **nazwisko rodowe** · kim była (tekst) · `is_living` | nazwisko rodowe — [[FR-005-nazwisko-rodowe]]; `is_living` steruje prywatnością w eksporcie |
| **Family** | 1-2 partnerów · dzieci · własne zdarzenia małżeństwa / końca | osoba może być partnerem w kilku rodzinach → powtórne małżeństwo działa z konstrukcji ([[FR-002-rodzina-jako-rekord]]) |
| **Event** | typ · **data + kwalifikator** (dokładnie / około / przed / po / między) · miejsce | „ok. 1890" i „przed 1920" to normalne dane ([[FR-004-data-z-dopiskiem]]). Typy: osoby — urodzenie, zgon, **pochówek** (`glossary.md` → *pochówek*: data pochówku to Event, nie cecha powiązania); rodziny — małżeństwo, koniec. Diagram z briefu wymienia tylko birth, death |
| **Cemetery** | nazwa · miejscowość · punkt środka · link do Grobonetu (jeśli pokryty) · status mapy offline | widok 1; dwa ostatnie pola wypełnia SPIKE-001 / [[ADR-003-map-source-offline]] |
| **Grave** | **kwatera / rząd / miejsce** (`sector` / `row` / `plot`) · pozycja + **jak ją uzyskano** (pinezka ze zdjęcia satelitarnego / GPS na miejscu) + dokładność · zdjęcia nagrobka · opłata ważna do (S4) | adres zarządcy jest prawdą, pinezka pomocą |
| **Burial** | grób ↔ osoba, wiele na grób; osoba ma osobny wiersz dla każdego grobu, który podaje dla niej jakieś źródło | grób rodzinny mieści kilka osób ([[FR-003-wiele-osob-w-grobie]]); człowiek leży w jednym miejscu, ale źródła mogą się różnić ([[ADR-006-claimed-value-separate-structures]] D2) |
| **Assertion** (provenance) | **źródło** (nagrobek / notatki / babcia / krewny / akt) + szczegół (kto, który akt) · **status** `CLAIMED / CONFIRMED / CONTRADICTED / UNKNOWN` · kiedy — **przy wierszu *Event* albo *Burial***, którego wartość potwierdza; wartość („co twierdzimy”) żyje w tym wierszu | cytowanie źródła jak w GEDCOM 7; **dwa sprzeczne twierdzenia współistnieją** jako dwa wiersze, każdy ze swoim twierdzeniem ([[FR-001-provenance]], [[ADR-006-claimed-value-separate-structures]]) |
| **Media** | pliki zdjęć w prywatnym magazynie aplikacji, powiązane z osobą albo grobem | — |
| **Setting: „ja"** | która osoba to autor | kotwica „jak łączą się ze mną" (M5) |

## Rules that are not tables

- **Ścieżka między dwiema osobami** = najkrótsza droga po krawędziach osoba–rodzina (partner, dziecko),
  pokazywana jako łańcuch („ja → żona → jej ojciec → …"). **Liczona, nigdy zapisywana.**
- **Ziarnistość źródeł (decyzja kosztowa z kick-offu):** twierdzenia na **datach, relacjach i miejscu
  pochówku** — to, o co się spiera; „kim była" niesie jedną linię źródła. Źródło na każdym polu
  spowolniłoby przepisywanie ~100 osób (G6).
- **Gdzie żyje:** lokalny SQLite + zdjęcia w prywatnym magazynie aplikacji ([[ADR-001-local-first]]);
  kopia i eksport — [[ADR-004-backup-format-encryption-destination]].

## In code

- **2026-10-05 — schemat v1** ([[ISSUE-007-data-layer]], [[ADR-005-sqlite-package]]):
  `grobing-code/lib/data/database.dart`. Są w nim wszystkie encje z tabeli wyżej **oprócz *Assertion***,
  a także bez opłaty za grób (S4, poza Must) i statusu mapy offline cmentarza ([[SPIKE-001-map-source-offline]]).
  Powód: model nie mówi, gdzie żyje wartość spornej daty, w *Event* czy w *Assertion*. *Assertion*
  przyjdzie jako v2 przy [[US-002-przepisanie-grobu]], z pierwszym prawdziwym testem migracji. Ta tabela
  się nie zmienia; to stan wdrożenia, nie korekta modelu.
- **2026-10-06 — schemat v2** ([[ISSUE-011-schema-v2-assertions]]). Odpowiedź na pytanie z v1: **wartość
  żyje w *Event* (data z dopiskiem) i w *Burial* (grób), a *Assertion* jest cytowaniem przy wierszu**, jak
  w GEDCOM 7. Sprzeczna wartość to osobny wiersz, a pokazuje się pierwszy
  ([[ADR-006-claimed-value-separate-structures]]). Tabela `assertions`; `burials` z `id`, bez UNIQUE na
  osobie, z UNIQUE (osoba, grób). Zapis faktów przez `grobing-code/lib/data/claims.dart`. Wiersze z v1
  dostały twierdzenie „notatki, przeniesione z v1”. Diagram i wiersze *Burial* / *Assertion* wyżej
  poprawione według ADR-006, więc to **korekta modelu**, nie tylko stan wdrożenia. Twierdzenia przy
  relacjach (diagram: „US-003”) jeszcze nie są w kodzie.

## Known consequence — not a model change

**Korekta autora (2026-10-05): notatki nie zawierają adresów kwater.** Grób przepisany z notatek ma
więc cmentarz i osoby, ale **ani adresu kwatery, ani pozycji** — oba powstają dopiero na miejscu (krok 6
UJ-001). Pola modelu zostają; nie mogą być wymagane przy wprowadzaniu. Jak taki grób znaleźć przy
pierwszej wizycie — ⚠️ **OPEN**, decyzja autora: `00_START_HERE/TRACEABILITY.md` → *Open gaps* 1.

**Decyzja autora (2026-10-06):** jeden wpis w notatkach = jeden nagrobek i osoby w nim, więc **Burial →
Grave zostaje wymagane** — model bez zmian. Gdyby przy przepisywaniu pojawił się wpis bez grobu, wraca
opcja „pochówek = osoba + cmentarz, grób opcjonalny” ([[US-002-przepisanie-grobu]] → *Open questions*).
