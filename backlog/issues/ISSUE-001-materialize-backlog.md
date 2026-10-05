---
title: "ISSUE-001 — Materialize the rest of the backlog from PROJECT_BRIEF"
type: issue
status: done
priority: MUST
scope: docs
ideal_days: 1.0
created: 2026-10-05
updated: 2026-10-05
quality-verdict: APPROVED
verdict-date: 2026-10-05
verdict-reviewer: self-check
---

# ISSUE-001 — Materialize the rest of the backlog from PROJECT_BRIEF

> Jedyny meta-issue z kick-offu. Sesja postawiła minimalny start, mechanizmy jako pozycje i
> eksperymenty; to zadanie zamienia resztę `PROJECT_BRIEF.md` w pełny backlog. Wykonuje `docs`.
> Struktura wg hierarchii **COMPONENT** i reguły `doc-growth.md` — folder powstaje dopiero, gdy ma treść.

## Description

`00_START_HERE/kickoff/PROJECT_BRIEF.md` niesie każdą decyzję z kick-offu: wartość (§2), MoSCoW
M1-M11 (§5), personę (§4), ścieżkę wizyty (§4a), meta-decyzje, §Security i §Architecture (model
danych, ADR-y). To zadanie wyciąga je do osobnych artefaktów.

**Zakres:** wyłącznie dokumentacja. Bez kodu. Bez nowych decyzji produktowych — niejasność w briefie
→ `⚠️ OPEN` w wytworzonym pliku. **Bez danych rodziny.**

## Inputs (read first)

- `00_START_HERE/kickoff/PROJECT_BRIEF.md` — jedyne źródło
- `00_START_HERE/glossary.md` · `DEFINITION_OF_DONE.md` · `DOC_MAP.md` · `TRACEABILITY.md`
- `grobing-agents/.claude/rules/doc-growth.md` — który folder na jaki sygnał

### Correction from the author (2026-10-05) — the brief assumed otherwise

**Notatki nie zawierają adresów kwater** — są w nich adresy cmentarzy, pochowane osoby, informacje o
nich i ich powiązania. Brief zakładał adres kwatery z notatek: §1 („per cemetery plot"), §4a krok 2
(„each with its plot address") i gałąź *„Grave with no pin yet (only a plot address from the notes)"*.
Przy AC-3b: gałąź UJ-001 to **grób bez pinezki i bez adresu kwatery** — położenie i adres powstają
dopiero na miejscu (krok 6). Jeśli to wymaga zmiany kroku albo nowego EPIC-a/US → `## Open gaps`,
nie po cichu. Wpływ na SPIKE-001 krok 4 — oznaczony w samym spike'u.

## Acceptance Criteria

- [x] **AC-1 — Vision.** Brief §1-3 wystarcza jako wizja — zapisz to jednym zdaniem w DOC_MAP albo,
      jeśli rozwijasz, `02_PRODUCT/vision/`.
- [x] **AC-2 — Persona.** Brief §4 → `02_PRODUCT/personas/P1-zbierajacy.md` (Zbierający) + notka o
      babci jako **Źródle**, nie personie.
- [x] **AC-3 — EPICs.** Z MoSCoW i kanonu (etapy procesu genealoga) → `03_REQUIREMENTS/epics/`, po
      pliku na EPIC, cel w jednym zdaniu, `status: draft`. Proponowany podział do potwierdzenia z
      autorem: *Zabezpiecz i przepisz* (M1, M8) · *Wizyta* (M2-M7) · *Zrozumienie* (M9-M11).
      **Bez US** — rozpisanie na US to osobny krok.
- [x] **AC-3b — Journey coverage checked, not assumed.** Przejdź zasiane wiersze `TRACEABILITY.md` i
      przypisz każdy krok UJ-001 oraz każdy wiersz `n/a` do EPIC-a. **Krok bez EPIC-a trafia do
      `## Open gaps` z nazwy** — nie poszerzaj EPIC-a po cichu.
- [x] **AC-3c — FR and NFR.** Z briefu (Step 0, model danych, §Security, sufficiency A1/A2) →
      `03_REQUIREMENTS/`: FR provenance (źródło + status), FR rodzina jako rekord, FR wiele osób w
      grobie, FR data z dopiskiem, FR nazwisko rodowe · NFR offline (każdy krok UJ-001 w trybie
      samolotowym), NFR odtworzenie na nowym telefonie, NFR migracje schematu, NFR czytelność w słońcu,
      NFR brak danych opuszczających telefon poza kopią.
- [x] **AC-4 — ADRs.** Z §Architecture → `04_ARCHITECTURE/decisions/`: **ADR-001 local-first** i
      **ADR-002 Flutter z przypiętą wersją** jako `accepted` (decyzje zapadły w kick-offie, ≥3 opcje
      każda); ADR-003 (mapy) i ADR-004 (kopia) jako `proposed` — zamykają je SPIKE-001 i SPIKE-003;
      ADR-005 (dystrybucja) — przy NT-005. Model danych → `04_ARCHITECTURE/data-model.md` (diagram z
      briefu).
- [x] **AC-5 — Non-technical items.** Sprawdź, że każdy wiersz §6 (N1-N7) ma pozycję w
      `backlog/non-tech/` albo jawnie wskazany dom (N5 → SPIKE-001). Kick-off postawił je — tu tylko
      weryfikacja.
- [x] **AC-6 — Deferred requirements.** Sprawdź, że każdy wiersz §Security „Deferred" ma pozycję w
      `backlog/deferred/`. Kick-off postawił je — tu tylko weryfikacja.
- [x] **AC-7 — DOC_MAP.** Każdy folder utworzony w tym zadaniu ma wiersz.
- [x] **AC-8 — Closed.** `status: done`; `CURRENT_STATE.md` zaktualizowany.

## Manual Verification

```powershell
# w katalogu grobing-vault
Get-ChildItem 03_REQUIREMENTS/epics/*.md          # EPIC-i istnieją
Select-String -Path 00_START_HERE/TRACEABILITY.md -Pattern "^\| UJ-001" | Measure-Object   # 7 kroków ścieżki
Get-ChildItem 04_ARCHITECTURE/decisions/*.md      # ADR-001..004
```

## Implementation plan

> `planning`, 2026-10-05 · auto-flow · **wykonawca: `docs`** — pozycja bez kodu, `dev` nie bierze udziału.
> Wzorce z NPG (nie wymyślane od zera): `materialization-spec/templates/ADR.template.md` (≥3 opcje,
> append-only po akceptacji) · `knowledge-base/mature-documentation-reference.md` §Artefact catalogue
> (EPIC żyje w wymaganiach, nie w backlogu; FR ma jeden `epic:`, NFR ma listę `epic:` + miarę, cel,
> metodę i trigger weryfikacji; frontmatter z wikilinkami w górę i w dół).

### Route through the chain (docs-only item)

`planning` → stop #1 → **`docs` wykonuje AC-1…AC-7** → `qa` (AC + DoD w wersji bez kodu; komendy z
*Manual Verification* uruchamia sam; sekcja *Verification*) → **`docs` zamyka (AC-8)** → stop #3:
**jedna paczka** commita vaulta. Zamknięcie **przed** commitem, nie po — inaczej commit zostawiłby
pozycję `in-progress` i wymusił drugi.

- **Stop #2 (telefon): n/a** — nie ma czego klikać. `qa` zapisuje w *Verification* „n/a — pozycja bez
  kodu"; to nie jest „pomiń".
- W paczce stopu #3 jadą też 3 wcześniejsze niezacommitowane zmiany vaulta (`CURRENT_STATE.md`,
  SPIKE-001, `01_INBOX/2026-10-05-1-listopada-zbieranie.md`) — `CURRENT_STATE.md` i tak zmienia się w AC-8.

### DoR / DoD applied to a meta item

- **DoR ISSUE:** jasny zakres ✅ · powiązana US / krok ścieżki / `delivery-style` — **n/a**: to pozycja,
  która dopiero tworzy EPIC-i, więc nie ma nad sobą US.
- **DoD ISSUE:** obowiązują linie **„dokumentacja zaktualizowana (wiersz DOC_MAP)"** i **„zero danych
  rodziny w zmianach"**. Kod, test happy-path, telefon, odtworzenie z kopii — **n/a** (zakres: wyłącznie
  dokumentacja). Kontrakt DoD nie ma wiersza dla pozycji bez kodu → *Gaps noticed*.
- **Macierz — moje kolumny (Issue(s), Issue Status) bez zmian.** ISSUE-001 nie dowozi żadnego kroku
  ścieżki; wpisany jako Issue sprawiłby, że kroki **wyglądałyby na pokryte**.

### Files — all in `grobing-vault`

| Plik | AC | Źródło | Treść |
|---|---|---|---|
| `00_START_HERE/DOC_MAP.md` | AC-1, AC-7 | brief §1-3 | zdanie nad tabelą: *wizja = brief §1-3 (zdanie wartości §2); `02_PRODUCT/vision/` powstaje dopiero, gdy wizja wyjdzie poza brief* · **8 wierszy folderów** (niżej), kolumna *Added* = „ISSUE-001" |
| `02_PRODUCT/personas/P1-zbierajacy.md` | AC-2 | §4, glossary | rola · cele · bóle · kontekst techniczny — **tylko to, co zadeklarowane** · notka: babcia = **Źródło**, nie persona (dlaczego: liczy się dla przepływu wprowadzania, nie dla ekranu) |
| `03_REQUIREMENTS/epics/EPIC-001-zabezpiecz-i-przepisz.md` | AC-3 | §5 M1+M8, Step 0, MD2 | etap: zabezpiecz notatki → przepisz rodzinami → uzupełnij u babci · **kopia + odtwarzanie przed masowym przepisywaniem** (MD2) · powiązania: NT-001, NT-002, NT-007, SPIKE-003, ADR-004 |
| `03_REQUIREMENTS/epics/EPIC-002-wizyta.md` | AC-3 | §4a, §5 M2-M7 | etap: weryfikacja na miejscu · UJ-001 kroki 1-7 · powiązania: SPIKE-001, ADR-003, NT-004 · **⚠️ OPEN: gałąź „grób bez pinezki i bez adresu kwatery"** (korekta autora) |
| `03_REQUIREMENTS/epics/EPIC-003-zrozumienie.md` | AC-3 | §5 M9-M11, H4 | etap: wizualizacja — **ostatni w kolejności pracy** (kanon) · „MVP done" zależy od SPIKE-002 (H4) |
| `00_START_HERE/TRACEABILITY.md` | AC-3b | §4a | kolumna **EPIC** we wszystkich 13 wierszach (mapowanie niżej) · `## Open gaps` |
| `03_REQUIREMENTS/functional/FR-001…FR-005` | AC-3c | Step 0, model danych | niżej |
| `03_REQUIREMENTS/non-functional/NFR-001…NFR-005` | AC-3c | §Security, A1, A2, M7, M8 | niżej |
| `04_ARCHITECTURE/decisions/ADR-001…ADR-004` | AC-4 | §Architecture, §Security | niżej |
| `04_ARCHITECTURE/data-model.md` | AC-4 | §Architecture → Data model | diagram mermaid + tabela encji + ścieżka pokrewieństwa (liczona, nie zapisywana) + ziarnistość provenance · nota: **adres kwatery i pozycja grobu powstają na miejscu** (korekta autora), link do Open gaps |
| `backlog/non-tech/*`, `backlog/deferred/*` | AC-5, AC-6 | §6, §Security Deferred | **tylko odczyt** — wynik weryfikacji w *Verification* |
| ten plik + `CURRENT_STATE.md` | AC-8 | — | `status: done` · „w toku" / „ostatnio zrobione" · licznik retro → 1 |

**Nowe foldery (8, każdy z wierszem DOC_MAP):** `02_PRODUCT/` · `02_PRODUCT/personas/` ·
`03_REQUIREMENTS/` · `03_REQUIREMENTS/epics/` · `03_REQUIREMENTS/functional/` ·
`03_REQUIREMENTS/non-functional/` · `04_ARCHITECTURE/` · `04_ARCHITECTURE/decisions/`.
Podfoldery FR/NFR, bo w `03_REQUIREMENTS/` dojdą jeszcze US i AC — bez nich korzeń zmiesza cztery typy.

**EPIC — szkielet** (tak, żeby spełniał DoR EPIC-a przy późniejszym rozpisaniu): frontmatter
`type: epic` · `status: draft` · `moscow: [...]` · `persona: "[[P1-zbierajacy]]"` · `FR: [...]` ·
`NFR: [...]` · `quality-verdict: pending` → sekcje *Goal* (1 zdanie) · *Stage of the genealogist's
process* · *In scope* (M-y) · *Out of scope* (S/C/W numerami) · *Dependencies* · *Open questions*.
**Bez US.**

**Dlaczego 3 EPIC-i, nie ~4** (brief MD2 mówi „~4 EPICs"): „uzupełnij u babci" to ta sama funkcja M1
ze źródłem „babcia" — osobny EPIC nie miałby własnej pozycji Must. Zapisane w EPIC-001, nie po cichu.

**AC-3b — mapowanie kroków:**

| Wiersz macierzy | EPIC |
|---|---|
| UJ-001 · 1-7 (M2-M6) | EPIC-002 |
| n/a — M9 · M10 · M11 (widok 5) | EPIC-003 |
| n/a — M1 (wprowadzanie rodzinami) | EPIC-001 |
| n/a — M7 (bez zasięgu) | EPIC-002 (NFR-001) |
| n/a — M8 (kopia + eksport + notka) | EPIC-001 |

Żaden krok nie zostaje bez EPIC-a. **`## Open gaps`** dostaje:
1. **Gałąź UJ-001 po korekcie autora** — grób **bez pinezki i bez adresu kwatery**: krok 2 nie ma czego
   pokazać poza linkiem do Grobonetu (gdy cmentarz jest pokryty). Jak Zbierający znajduje taki grób przy
   pierwszej wizycie? Dotyka też M1 („grób: adres kwatery, zdjęcie, pinezka" — przy przepisywaniu żadnego
   z trzech nie ma). **Decyzja autora** — nie zmienia EPIC-a.
2. **Nierozstrzygnięte:** grób ze zdjęcia z galerii (pinezka z lokalizacji zdjęcia) →
   `01_INBOX/2026-10-05-1-listopada-zbieranie.md`. Poza EPIC-ami do decyzji.

**FR** (`type: functional-requirement`, `status: draft`, jeden `epic:`; w treści „używane też przez"):

| FR | Reguła (z briefu) | `epic:` |
|---|---|---|
| FR-001 provenance | twierdzenie o **datach, relacjach i miejscu pochówku** ma źródło + status (`CLAIMED / CONFIRMED / CONTRADICTED / UNKNOWN`) + kiedy + kto; sprzeczne współistnieją; „kim był" — jedna linia źródła | EPIC-001 (też EPIC-002, M6) |
| FR-002 rodzina jako rekord | 1-2 partnerów + dzieci; osoba partnerem w wielu rodzinach; wprowadzanie rodziną (G6) | EPIC-001 (też EPIC-003) |
| FR-003 wiele osób w grobie | pochówek = osoba ↔ grób, wiele na grób | EPIC-001 (też EPIC-002, M4) |
| FR-004 data z dopiskiem | dokładnie / około / przed / po / między | EPIC-001 (też EPIC-003, M10) |
| FR-005 nazwisko rodowe | nazwisko z urodzenia obok nazwiska po ślubie | EPIC-001 |

**NFR** (`type: non-functional-requirement`, `status: draft`, `epic:` jako lista; sekcje *Metric · Target ·
Method · Verification trigger*). **Bez wymyślonych liczb** — brak miary w briefie → `⚠️ OPEN` w pliku.

| NFR | Z briefu | `epic:` |
|---|---|---|
| NFR-001 offline | każdy krok UJ-001 w trybie samolotowym (M7, H9) | [EPIC-002] |
| NFR-002 odtworzenie na nowym telefonie | kopia odtwarza wszystko — osoby, rodziny, groby, zdjęcia (M8, G1) | [EPIC-001] |
| NFR-003 migracje schematu | zmiana schematu = migracja testowana z poprzedniej wersji (A1) | [EPIC-001, EPIC-002, EPIC-003] |
| NFR-004 czytelność w słońcu | ekrany wizyty czytelne w pełnym słońcu; wariant kontrastowy, jeśli nie (A2) | [EPIC-002] |
| NFR-005 dane nie opuszczają telefonu poza kopią | bez analityki, crash reportingu, danych rodziny w logach; wychodzi tylko zaszyfrowana kopia i eksport na żądanie (§Security) | [EPIC-001, EPIC-002, EPIC-003] |

**ADR** (szablon NPG; `quality-verdict: pending`; opcje **wyłącznie z briefu**):

| ADR | Status | Opcje (≥3) |
|---|---|---|
| ADR-001 local-first | `accepted` | baza w telefonie = SoT + zaszyfrowana kopia + czytelny eksport (**wybrana**) · backend w chmurze jako SoT (model Friendsheet) · lokalna baza jako lustro bazy w chmurze · hostowany serwis genealogiczny (MyHeritage / FamilySearch — test zastępowalności) |
| ADR-002 Flutter z przypiętą wersją | `accepted` | Flutter, wersja przypięta per projekt (3.41.1), globalny SDK nietykany (**wybrana**) · Kotlin + Jetpack Compose · Flutter na współdzielonym globalnym SDK bez przypięcia (psuje wydaną aplikację) · *Follow-ups:* mechanizm przypięcia `⚠️ OPEN` → ISSUE-002 |
| ADR-003 źródło map offline | `proposed` | `flutter_map` + cache kafelków (uwaga: wtyczka bulk-download GPL, warunki dostawców) · regiony offline MapLibre · własne kafelki · mapy tylko online (łamie M7) — zamyka SPIKE-001 |
| ADR-004 kopia: format, szyfrowanie, miejsce | `proposed` | automatyczna kopia szyfrowana w telefonie → folder w chmurze autora przez systemowe okno wyboru + czytelny eksport offline (**kierunek wybrany przez autora**, §Security) · tylko eksport kopiowany ręcznie · sama kopia Androida (limit 25 MB → cicho niepełna) — mechanizm zamyka SPIKE-003 |

ADR-005 (dystrybucja) **nie powstaje** — przy NT-005.

### Out of Scope

- **US i AC** — rozpisanie EPIC-ów to osobny krok (*Next steps* 1).
- **UJ-001 jako osobny plik** w `03_REQUIREMENTS/` — ścieżka żyje w briefie §4a + macierzy. Poprawka
  gałęzi idzie do Open gaps i EPIC-002, **nie do briefu** (`kickoff/` = zapis decyzji autora).
- `02_PRODUCT/vision/` — AC-1 w wariancie „jedno zdanie w DOC_MAP"; trigger z `doc-growth.md` nie odpalił.
- Should / Could / Won't jako EPIC-i — wymienione numerami w *Out of scope* EPIC-ów.
- ADR-005; `06_NON_TECH/` (powstaje przy SPIKE-001 / koszcie).
- Zmiany w briefie, `glossary.md`, `DEFINITION_OF_DONE.md` — także tam, gdzie korekta autora je
  dezaktualizuje → *Gaps noticed*.
- Import grobu ze zdjęcia z galerii.
- **Nazwy cmentarzy i jakiekolwiek dane rodziny** — repo publiczne (decyzja 2026-10-05).

### Gaps noticed (sufficiency — said out loud, not fixed here)

1. **DoD nie ma wiersza dla pozycji bez kodu** — dotyczy ISSUE-001, a w części ISSUE-003…006 (repo
   agentów, bez telefonu). Tu stosujemy linie dokumentacyjne; uzupełnienie kontraktu = decyzja autora /
   temat na retro.
2. **ADR append-only vs ISSUE-002** („sposób przypięcia → wpis do ADR-002"): ADR-002 przyjmuje decyzję,
   mechanizm zostaje w *Follow-ups* jako `⚠️ OPEN`; ISSUE-002 **dopisuje** datowaną linię (dopisek, nie
   przepisanie decyzji).
3. **`glossary.md` — „pinezka: prawdą o położeniu jest adres zarządcy"** — dla grobu bez adresu kwatery
   pinezka jest jedynym wskaźnikiem. Razem z Open gap 1.

### Acceptance scenario

Otwieram vault i widzę:
- 3 EPIC-i w `03_REQUIREMENTS/epics/`, każdy z celem, etapem procesu, M-ami i FR/NFR;
- 13 wierszy macierzy, każdy z EPIC-iem; Open gaps nazywa gałąź bez adresu kwatery;
- 5 FR i 5 NFR; ADR-001 i 002 `accepted`, 003 i 004 `proposed`; `data-model.md`;
- DOC_MAP z 8 nowymi wierszami (każdy ma folder na dysku, każdy folder ma wiersz) i zdaniem o wizji;
- ISSUE-001 `done`, `CURRENT_STATE.md` zaktualizowany, licznik retro = 1;
- w zmianach zero danych rodziny.

### Verification for `qa`

```powershell
# w katalogu grobing-vault
(Get-ChildItem 03_REQUIREMENTS/epics/*.md).Count                                   # 3
(Get-ChildItem 03_REQUIREMENTS/functional/*.md, 03_REQUIREMENTS/non-functional/*.md).Count   # 10
Get-ChildItem 04_ARCHITECTURE/decisions/*.md                                       # ADR-001..004
Select-String -Path 00_START_HERE/TRACEABILITY.md -Pattern "^\| (UJ-001|n/a)" |
  Where-Object { $_.Line -notmatch "EPIC-00\d" }                                   # pusto = każdy wiersz ma EPIC
Get-ChildItem -Directory -Recurse 02_PRODUCT, 03_REQUIREMENTS, 04_ARCHITECTURE |
  ForEach-Object { $rel = ($_.FullName.Substring((Get-Location).Path.Length + 1) -replace '\\','/') + '/'
    if (-not (Select-String -Path 00_START_HERE/DOC_MAP.md -SimpleMatch "``$rel``" -Quiet)) { "brak wiersza: $rel" } }
git status --short                                                                 # tylko *.md, żadnych zdjęć/baz/eksportów
```
Plus przegląd diffu pod kątem danych rodziny (imiona, daty, **nazwy cmentarzy**, miejscowości).

## Verification

> `qa`, 2026-10-05. Uruchomiony jako subagent bez historii rozmowy, więc niezależny od sesji wykonawcy
> `docs`. To jednak ta sama rola `qa`, nie krytyk, stąd `verdict-reviewer: self-check` (krytyk
> `quality` powstaje w ISSUE-003). Zakres: AC-1…AC-7 oraz DoD ISSUE w wersji bez kodu, czyli linie
> „dokumentacja zaktualizowana (wiersz DOC_MAP)” i „zero danych rodziny w zmianach”. AC-8 robi `docs`
> po `qa`, więc nie jest tu oceniane.

**Werdykt: CONDITIONAL.** AC-1…AC-7 są spełnione. Żaden powód BLOCK nie zachodzi: zero danych rodziny,
w zmianach wyłącznie pliki `*.md`. Trzy miejsca mówią jednak coś, czego brief nie niesie, albo przeczą
innemu plikowi (F-1…F-3). `docs` poprawia je **przed zamknięciem (AC-8)**. F-4…F-7 to zalecenia, nie
warunki.

### Acceptance criteria

| AC | Wynik | Dowód |
|---|---|---|
| AC-1 Vision | ✅ | `DOC_MAP.md:21-23`: zdanie „Wizja = brief §1-3”. `02_PRODUCT/vision/` nie istnieje, bo trigger z `doc-growth.md` nie odpalił |
| AC-2 Persona | ✅ | `P1-zbierajacy.md:16-34`: rola, cele, bóle i kontekst techniczny 1:1 z briefu §4, bez wieku, zawodu i nawyków. `:36-40`: babcia jako **Źródło**, nie persona, z powodem z §4 |
| AC-3 EPICs | ✅ | 3 pliki ze `status: draft` i celem w jednym zdaniu (EPIC-001:21-22 · EPIC-002:22-24 · EPIC-003:22-23). Podział M1+M8 / M2-M7 / M9-M11 jak w propozycji AC. `user-stories: []`, czyli bez US. Odejście od „~4 EPICs” (MD2) jest uzasadnione w EPIC-001:29-31. DoR EPIC-a (cel · persona · in/out · etap procesu) spełniony w każdym z trzech |
| AC-3b Journey coverage | ✅ | `TRACEABILITY.md:29-41`: 13 z 13 wierszy ma EPIC, zgodnie z mapowaniem z planu. `:46-58` *Open gaps* nazywa gałąź „grób bez pinezki i bez adresu kwatery” (korekta autora) oraz grób ze zdjęcia z galerii |
| AC-3c FR and NFR | ✅ (uwagi F-1, F-2) | FR-001…005 i NFR-001…005 to dokładnie lista z AC. Każdy FR ma jeden `epic:`. Każdy NFR ma `epic:` jako listę oraz sekcje Metric · Target · Method · Verification trigger. Tam, gdzie brief nie podaje miary, stoi `⚠️ OPEN` (NFR-004:23-24) |
| AC-4 ADRs | ✅ | ADR-001 `accepted`, 4 opcje · ADR-002 `accepted`, 3 opcje · ADR-003 `proposed`, 4 opcje, `decided-by: SPIKE-001` · ADR-004 `proposed`, 3 opcje, `decided-by: SPIKE-003`. ADR-005 słusznie nie powstał (przy NT-005). `data-model.md` ma diagram mermaid identyczny z briefem, tabelę encji, ścieżkę pokrewieństwa, ziarnistość źródeł i notę o korekcie autora |
| AC-5 Non-technical | ✅ | N1→NT-001 · N2→NT-002 · N3→NT-003 · N4→NT-004 · N5→SPIKE-001 (`covers-non-tech: [N5]`) · N6→NT-005 · N7→NT-006. Ponad to NT-007 (G2) i NT-008 |
| AC-6 Deferred | ✅ | In-app lock→DEF-001 · pełny przegląd L1→DEF-002 · SCA→DEF-003 · logowanie zdarzeń bezpieczeństwa→DEF-004. Wiersz ASVS L2 brief oznacza jako „n/a”, nie „deferred”, więc pozycji nie wymaga. DEF-005 pochodzi z triggera push z 3g |
| AC-7 DOC_MAP | ✅ | `DOC_MAP.md:31-38`: 8 wierszy. Komenda nr 5 zwraca pusto. Każdy z 17 wierszy DOC_MAP ma folder albo plik na dysku |
| AC-8 Closed | — | poza zakresem `qa`; robi `docs` po tej sekcji |

### Command results

Komendy z *Verification for `qa`* i *Manual Verification*, uruchomione w PowerShell w `grobing-vault`
2026-10-05:

| Komenda | Oczekiwane | Wynik |
|---|---|---|
| `(Get-ChildItem 03_REQUIREMENTS/epics/*.md).Count` | 3 | **3** ✅ |
| `(Get-ChildItem …functional/*.md, …non-functional/*.md).Count` | 10 | **10** ✅ |
| `Get-ChildItem 04_ARCHITECTURE/decisions/*.md` | ADR-001..004 | `ADR-001-local-first` · `ADR-002-flutter-pinned` · `ADR-003-map-source-offline` · `ADR-004-backup-format-encryption-destination` ✅ |
| wiersze `UJ-001` / `n/a` bez `EPIC-00\d` | pusto | **pusto**: 13 wierszy, każdy z EPIC-iem ✅ |
| foldery bez wiersza w DOC_MAP | pusto | **pusto** ✅. Uwaga: `-Recurse` nie zwraca samych korzeni, więc `02_PRODUCT/`, `03_REQUIREMENTS/` i `04_ARCHITECTURE/` sprawdziłem osobno; wszystkie trzy mają wiersz |
| `git status --short` | tylko `*.md` | 5 zmienionych i 21 nowych plików, **wszystkie `*.md`** ✅ |
| *Manual Verification*: liczba wierszy `^\| UJ-001` | 7 | **7** ✅ |

Ponad listę:
- **Wikilinki:** 34 różne wikilinki w nowych i zmienionych plikach, **0 martwych**.
- **Ścieżki w backtickach:** wszystkie istnieją poza `06_NON_TECH/external-costs.md` (ADR-003:35).
  Ta jest jawnie opisana jako „folder na sygnał”, zgodnie z `doc-growth.md`.

### Family-data scan

- **Typy plików:** wyłącznie `*.md`. Zero `*.db`, `*.sqlite*`, zdjęć, eksportów i kopii.
- **Co przejrzałem:** cały `git diff`, 21 nowych plików i 3 zmiany z wcześniejszej sesji
  (`CURRENT_STATE.md`, SPIKE-001, `01_INBOX/2026-10-05-1-listopada-zbieranie.md`).
- **Lata w treści:** 1890 i 1920 (przykłady „ok. 1890”, „przed 1920” z briefu), 1918 (granica A6),
  2019 (cytowanie Ink & Switch), 2026 (daty dokumentów). Żadne nie dotyczy prawdziwej osoby.
- **Słowa z wielkiej litery,** przejrzane ręcznie z pełnej listy: brak imion i nazwisk, nazw cmentarzy,
  parafii i miejscowości. Jedyna nazwa geograficzna to „Polska”. Łańcuch „ja → żona → jej ojciec” jest
  ogólnym przykładem z briefu.
- **Grep na końcówki nazwisk** (-ski, -cka, -wicz…) **i znaczniki miejsca** (parafia, ul., gmina,
  „cmentarz X”): zero trafień o osobach albo miejscach.
- SPIKE-001:27-29 trzyma nazwy cmentarzy poza vaultem do czasu decyzji w NT-008. To prawidłowe.
- **Wynik: zero danych rodziny w zmianach.**

### Ownership

- `kickoff/` bez zmian: `git diff -- 00_START_HERE/kickoff` jest puste ✅
- `TRACEABILITY.md`: zmieniona tylko kolumna EPIC i `## Open gaps`. Kolumny Issue(s), Issue Status i
  Quality Verdict są puste, tak jak przed zmianą ✅
- *Implementation plan*: brak śladów edycji przez `docs`. Odstępstwa `docs` od planu widać w plikach,
  nie w planie (np. F-3) ✅
- `status: in-progress` nieruszony ✅

### Stop #2

Stop #2 (telefon): n/a — pozycja bez kodu (to nie jest „pomiń”)

### Findings

| # | Gdzie | Problem | Waga | Poprawka (`docs`) |
|---|---|---|---|---|
| F-1 | `03_REQUIREMENTS/functional/FR-001-provenance.md:31-32` | Zdanie „stąd okresowe pytanie o nośne fakty co 10 zamkniętych pozycji” łączy dwie rzeczy, których brief nie łączy. Granica WZ-036 (Step 0) wymaga okresowego „czy to nadal prawda?” dla **twierdzeń w aplikacji**. Pytanie z 3g dotyczy faktów o **projekcie** zapisanych w vaulcie (przykłady z briefu: ostatnie odtworzenie, osoby w aplikacji vs w notatkach, cmentarze bez pinezek), a twierdzeń o rodzinie w vaulcie być nie może. Plik przedstawia lukę jako pokrytą. | **warunek** | zastąpić `⚠️ OPEN`: brief nie mówi, kiedy i jak przegląda się statusy twierdzeń w aplikacji |
| F-2 | `03_REQUIREMENTS/non-functional/NFR-005-dane-nie-opuszczaja-telefonu.md:19` | Eksport jest tu „tworzony **na żądanie**”. Brief §Security mówi „a **periodic** plain export”, a ADR-004:36 poprawnie pisze „okresowy”. Dwa pliki mówią co innego, a „na żądanie” to nowa decyzja o mechanizmie. | **warunek** | „okresowy eksport (mechanizm: ADR-004)” |
| F-3 | `03_REQUIREMENTS/functional/FR-002-rodzina-jako-rekord.md:6` ↔ `03_REQUIREMENTS/epics/EPIC-002-wizyta.md:8` | FR-002 wymienia EPIC-002 w `used-by`, ale lista `FR:` w EPIC-002 nie ma FR-002 (plan mówił tylko „też EPIC-003”). DoD EPIC-a („każde FR EPIC-a pokryte ≥1 zamkniętą US”) czyta listę z EPIC-a, więc to powiązanie działa tylko w jedną stronę. | **warunek** | dopisać FR-002 do `FR:` w EPIC-002 (M5: ścieżka liczona po rodzinach) albo usunąć EPIC-002 z `used-by` |
| F-4 | `03_REQUIREMENTS/non-functional/NFR-001-offline.md:23` ↔ `04_ARCHITECTURE/decisions/ADR-003-map-source-offline.md:2, 33-35` | Cel „wszystkie kroki UJ-001” (MD2 + AC-3c) obejmuje też krok 1, czyli **mapę Polski offline**. ADR-003 i SPIKE-001 pytają tylko o ~10 obszarów wielkości cmentarza (gałąź w briefie §4a: kroki 2-7). Ten rozjazd nie jest nigdzie zaznaczony. | zalecenie | `⚠️ OPEN` w NFR-001 albo w *Context* ADR-003: czy krok 1 offline wymaga warstwy mapy dla całej Polski? Pytanie dla SPIKE-001 |
| F-5 | `04_ARCHITECTURE/data-model.md:29, 47` ↔ `FR-003-wiele-osob-w-grobie.md:26`, `FR-004-data-z-dopiskiem.md:20` | FR-003 i FR-004 traktują **pochówek jako zdarzenie z datą** (źródło: `glossary.md:36`). „Żywy dom modelu” ma za to zdarzenia osoby tylko „birth, death”, tak jak brief. Dev czytający model nie zobaczy typu „pochówek”. | zalecenie | jedna linia w wierszu *Event* albo `⚠️ OPEN`: typ „pochówek” pochodzi z `glossary.md` i nie ma go na diagramie briefu |
| F-6 | `03_REQUIREMENTS/epics/EPIC-002-wizyta.md:66-67` | „Brief to przewidział” nie do końca się zgadza. Brief §1 mówi, że notatki nie mają zdjęć, ale gałąź §4a dla pierwszej wizyty mówi tylko o brakującej pinezce. Przy pierwszej wizycie krok 3 nie ma czym porównać. | zalecenie | dopisać brak zdjęcia do *Open gaps* 1 (pierwsza wizyta: bez pinezki, bez adresu **i bez zdjęcia**), zamiast uznawać za przewidziane |
| F-7 | `backlog/deferred/DEF-001-in-app-lock.md` (poza zmianami ISSUE-001) | Pozycja ma `deferred-until: MVP`, a brief §Security mówi „MVP+ (optional)”. Pokrycia AC-6 to nie zmienia. | obserwacja | poprawić przy okazji (pozycja z kick-offu) |

### Re-check

> `qa`, 2026-10-05, po poprawkach `docs`. **Werdykt zmieniony: CONDITIONAL → APPROVED.** Warunki F-1…F-3
> są spełnione, a zalecenia F-4…F-6 też wdrożone.

| # | Wynik | Dowód |
|---|---|---|
| F-1 | ✅ | FR-001 *Rules*: zdanie „stąd…” zastąpione `⚠️ OPEN` („kto, kiedy i jak przegląda statusy twierdzeń w aplikacji”), z wyjaśnieniem, że pytanie z 3g tej luki nie pokrywa. „Okresowy przegląd” ma pokrycie w briefie (Step 0, WZ-036: *„a periodic 'are these still true?' pass”*) |
| F-2 | ✅ | NFR-005 pkt 2: „okresowy eksport” z cytatem z §Security zgodnym co do słowa z briefem. Teraz spójne z ADR-004:36 |
| F-3 | ✅ | `FR:` w EPIC-002 ma FR-002. Powiązanie działa w obie strony z `used-by` w FR-002 |
| F-4 | ✅ (uwaga N-1) | `⚠️ OPEN` dodane w NFR-001 *Notes* i w ADR-003 *Follow-ups*. ADR-003 jest `proposed`, więc dopisek nie łamie zasady append-only |
| F-5 | ✅ | `data-model.md`, wiersz *Event*: typy osoby (urodzenie, zgon, pochówek, ze wskazaniem `glossary.md`) i rodziny (małżeństwo, koniec), plus nota, że diagram briefu wymienia tylko birth, death. Diagram bez zmian. Zgodne z listą typów w FR-004 |
| F-6 | ✅ | EPIC-002 *Open questions*: zdanie „brief to przewidział” usunięte, krok 3 włączony do *Open gaps* 1. `TRACEABILITY.md` *Open gaps* 1 dopisuje brak zdjęcia nagrobka i krok 3 |
| F-7 | — | poza zakresem ISSUE-001; `docs` przekazał autorowi. Nie wpływa na werdykt |

**Sprawdzone ponownie:**
- Wikilinki we wszystkich nowych i zmienionych plikach: 0 martwych.
- W zmianach nadal tylko `*.md`.
- `kickoff/` bez zmian.
- W poprawionych fragmentach zero danych rodziny (jedyne lata to przykłady „ok. 1890” i „przed 1920” z briefu).
- `status:` bez zmian.

**Nowe znaleziska:**
- **N-1 (obserwacja, nie blokuje)** — `NFR-001-offline.md`, *Notes*, punkt `⚠️ OPEN`: dopisek „(wybór, dokąd
  jechać, **zwykle w domu**)”. Brief §4a mówi tylko „around 1 November, deciding where to go”, a nie, gdzie
  się to dzieje. To przesłanka bez źródła, choć stoi wewnątrz pytania otwartego i niczego nie rozstrzyga.
  Można ją usunąć przy okazji.
- **N-2 (moja poprawka we własnym tekście)** — w *Command results* zapis wikilinka z wielokropkiem w
  środku (w backtickach) zamieniłem na słowo „wikilinki”. Prosty checker linków (np. przyszła bramka z ISSUE-004) czytałby go
  jako martwy link. Treść znalezisk bez zmian.

### Checked and found correct

- **Opcje ADR — każda ma źródło w briefie:**
  - ADR-001: wybrana · backend w chmurze (§3a) · lokalna baza jako lustro chmury (Step 0) ·
    MyHeritage / FamilySearch (test zastępowalności, §2).
  - ADR-002: Flutter z przypiętą wersją · Kotlin + Compose (tabela *Stack*) · Flutter bez przypięcia
    (ryzyko opisane w *Reuse*: „upgrading Flutter for Grobing upgrades it for Friendsheet too”).
  - ADR-003: `flutter_map` i MapLibre (tabela *Stack*) · własne kafelki (N5) · tylko online
    (odrzucone przez M7).
  - ADR-004: opcja wybrana, (b) i (c) dosłownie z §Security.
- **Każde `⚠️ OPEN` w nowych plikach to prawdziwa luka briefu; brief żadnego nie rozstrzyga:**
  - grób bez adresu kwatery (EPIC-001:60 · EPIC-002:60 · data-model:70) — korekta autora;
  - kopia sprzed migracji (NFR-003:30 · ADR-004:61) — brief milczy;
  - miara czytelności w słońcu (NFR-004:23-24) — A2 nie podaje progu;
  - mechanizm przypięcia i nazwa pakietu (ADR-002:53-56) — brief podaje dwie drogi i nie wybiera.
- **Liczby:** żadnej wymyślonej. „Zero” w NFR-003 i NFR-005 to przeformułowanie reguł A1 i §Security.
  25 MB, 3.41.1, Dart 3.11.0, ~100 / ~50 / 10 pochodzą z briefu.
- **Znaczenia spoza briefu mają źródło w `glossary.md`** (kontrakcie z kick-offu), więc nie są
  wymyślone: znaczenia statusów (`CLAIMED` = jedno źródło itd.), pinezka „ze źródłem i dokładnością”,
  data pochówku jako Event.
- **Spójność `epic:`** w NFR z listami `NFR:` w EPIC-ach: zgodna we wszystkich 5 NFR.
- **Persona:** bez wieku, zawodu i nawyków. Cele i bóle mają pokrycie w §4 i §2.

## Next steps after this closes

1. Rozpisanie EPIC-a *Zabezpiecz i przepisz* na US (z kroków / funkcji) — najpierw kopia i odtwarzanie.
2. Normalny łańcuch: `pm` → `planning` → `dev` → `qa` → `docs`.
