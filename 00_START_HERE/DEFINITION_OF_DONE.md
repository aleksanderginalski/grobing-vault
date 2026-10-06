---
title: "Grobing — Definition of Ready / Done"
type: contract
status: active
created: 2026-10-05
updated: 2026-10-06
---

# Grobing — Definition of Ready / Done

> Kontrakt egzekwowany przez agentów (Meta-decyzja 6). DoR = kiedy pozycja może ruszyć; DoD =
> kiedy jest skończona. **Wartości z `dor-dod-defaults.md` (kolumna MVP), świadomie dostrojone w
> kick-offie 2026-10-05** do warstw z MD2, krytyka (3d), punktów stopu (3f) i kanonu genealogii.

## Per artefact type

| Type | DoR (ready to start) | DoD (done) |
|---|---|---|
| EPIC | cel · persona · zakres in/out · **któremu etapowi procesu genealoga służy** | wszystkie US zamknięte albo świadomie odłożone · **każde FR EPIC-a pokryte ≥1 zamkniętą US** (macierz bez luki) · jego NFR zweryfikowane |
| US | persona · wartość · ≥1 sprawdzalne AC · **kroki ścieżki, które pokrywa** (albo „funkcja widoku 5") | wszystkie AC spełnione, **każde z testem happy-path** · pokazane w aplikacji (do MVP na emulatorze — patrz niżej) · werdykt jakości zapisany · wiersz w `TRACEABILITY.md` zaktualizowany |
| ISSUE | jasny zakres · powiązana US · krok ścieżki / funkcja widoku 5 · `delivery-style: task-level` | kod + test happy-path dla każdego AC, którego dotyka · **ręczna weryfikacja — do MVP na emulatorze** (patrz niżej; kroki po polsku; `ok` / `pomiń` zapisane / opis błędu — **cisza ≠ pomiń**) · dokumentacja zaktualizowana (wiersz DOC_MAP, jeśli powstał folder) · **zapisuje fakt o rodzinie → źródło + status zapisane** (FR provenance) · **dotyka warstwy danych → próbne odtworzenie z kopii przechodzi; zmiana schematu ma test migracji z poprzedniej wersji** · **zero danych rodziny w zmianach** |
| SPIKE | pytanie · limit czasu · warunek wyjścia | odpowiedź zapisana (ADR albo notatka) · kod z eksperymentu usunięty · status hipotezy zaktualizowany |
| Bug | kroki odtworzenia · waga | poprawka + test regresji · dokumentacja zaktualizowana |
| Non-code (NT, także zaparkowane) | jasne pytanie · **warunek obudzenia będący zdarzeniem**, jeśli zaparkowane | odpowiedź zapisana — ⚠️ **fakty o rodzinie trafiają do aplikacji ze źródłem i statusem, nigdy do vaulta**; vault zapisuje tylko, że pozycja się zamknęła |
| **PRODUCT (v1 = MVP)** | ✅ spełnione w kick-offie — wartość ma trzy części, Must ją dowozi | **sygnał „3 miesiące" z `PROJECT_BRIEF.md` §2 jest prawdziwy:** ~100 osób i ~50 grobów z notatek jest w aplikacji · do papieru się nie zagląda · co najmniej jedna rozmowa z babcią dodała fakty spoza notatek. **Skalowane do MVP:** ścieżka wizyty przechodzi na prawdziwym cmentarzu **bez notatek**. |

> **DoD produktu to NIE „wszystkie EPIC-i zamknięte".** „M1-M11 dowiezione" to burndown, śledzony w
> backlogu. Produkt jest skończony, gdy sygnał jest prawdziwy — te dwie rzeczy potrafią się rozjechać
> w obie strony.

> **Gdzie ręczna weryfikacja — decyzja autora 2026-10-05 (stop #2 w [[ISSUE-002-bootstrap-code-repo]]).**
> Do MVP aplikację budujemy i sprawdzamy na **emulatorze**, najlepiej w buildzie release. Na prawdziwy
> telefon trafi dopiero MVP, wyłącznie jako build release: telefon z danymi nie może dostać buildu
> podpisanego innym kluczem, bo zmiana podpisu wymaga odinstalowania, a ono kasuje bazę. **Wyjątki,
> które sprawdzi tylko prawdziwy telefon w prawdziwym miejscu:** GPS na miejscu, czytelność w pełnym
> słońcu ([[NFR-004-czytelnosc-w-sloncu]]), offline na cmentarzu ([[NFR-001-offline]]). Pozycje, które
> ich dotyczą, mają w planie krok na telefonie i jasno mówią, że wymaga on buildu release.
>
> **Kto sprawdza — decyzja autora 2026-10-06 (stop #2 w [[ISSUE-011-schema-v2-assertions]]).** Kroki
> dla autora dotyczą **UI/UX: przepływu, który użytkownik czuje** (ekrany, dotknięcia, czytelność). Gdy
> pozycja nie ma nowego ekranu (schemat, migracja, mechanizm kopii), ręczną weryfikację na emulatorze
> robi **agent** (`adb`: instalacja, dotknięcia, zrzut ekranu, odczyt bazy) i zapisuje ją w
> *Verification* jako „kroki oddane agentowi”, a nie jako „ok” autora. Krok, którego agent nie może
> wykonać, bo wymaga sekretu autora (hasło), pokrywa test automatyczny, nazwany wprost.

## DoD scaling by maturity stage (current: MVP)

| Stage | ISSUE-DoD |
|---|---|
| PROTOTYP | works + manual verify (no test requirement) |
| **MVP** ← | **+ happy-path test for each AC** (plus the Grobing-specific lines above) |
| PRODUKCJA | + coverage threshold + docs updated |
| SCALING | + performance NFR check + observability hook |
