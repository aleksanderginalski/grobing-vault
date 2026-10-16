---
title: "ISSUE-044 — Family wreaths at the portrait: the families a person comes from, inherited from the father by default"
type: issue
status: ready
delivery-style: task-level
priority: SHOULD
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[2026-10-14-opowiesc-rodziny-i-wieniec]] → d) · `/pm` 2026-10-16: autor przenosi wieńce przed instalację („tak róbmy to”) i podaje definicję · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-16
---

# ISSUE-044 — Wieńce rodzin przy portrecie

> Autor 2026-10-14 (stop #2 ISSUE-037): *„chciałbym móc w wyborze portretu dla niej customowy wieniec, który byłby związany z danym
> nazwiskiem”*. 2026-10-16 w `/pm`: wieńce **symbolizujące rodziny, z których wywodzi się dana osoba (domyślnie dzieci przejmują po ojcu)** —
> i *„tak róbmy to”*: teraz, a nie po instalacji MVP.

## Two earlier decisions this changes — on purpose
1. **[[style-b]] reguła 8 i [[osoba]] D3 — „bez gałązek” wokół portretu** (choć referencja R4 je miała). Wraca do decyzji na prototypie.
2. **Kolejność z 2026-10-14** („c) i d) po instalacji MVP”) — d) idzie teraz; c) (opowieść na drzewie) zostaje po instalacji.

## What to build
1. **Najpierw `ui` w trybie discovery** — klikalny prototyp panel po panelu (retro 3, R4), link `file:///` (retro 4, R1). Pytania (z INBOX d i
   z nowej definicji):
   - czym jest wieniec (gałązki jak w R4, liście, ramka z motywem) i czy jest symbolem religijnym (reguła 8);
   - **jedna linia czy obie** — „rodziny, z których się wywodzi” może znaczyć linię ojca i matki;
   - kobieta z nazwiskiem rodowym („z d.”, [[FR-005-nazwisko-rodowe]]): wieniec rodu ojca, czy po ślubie inny;
   - wyjątek ręczny: kiedy dziecko nie przejmuje po ojcu (np. ojciec nieznany);
   - gdzie widać: portret w widoku osoby, węzły drzewa, karta, tryb prezentacji;
   - grafika: `ui` pisze prompty do DALL-E, autor generuje i odsyła (jak przy [[ISSUE-046-icons]]) — motywy wieńców to nie dane rodziny.
2. Potem plan i budowa: **wieniec wyliczany z drzewa po linii ojca**, zapisane tylko: wieńce rodów (nazwa, motyw) i wyjątki przy osobie — nowa
   tabela, zmiana schematu (test migracji, kopia ją niesie).

## Acceptance Criteria (do potwierdzenia po discovery)
- **AC-1** *Given* ojciec z wieńcem rodu *When* dodaję mu dziecko *Then* dziecko ma ten wieniec bez dodatkowego kroku.
- **AC-2** *Given* osoba z wieńcem po ojcu *When* zmieniam jej wieniec ręcznie *Then* zmiana dotyczy tej osoby, a reszta rodu zostaje.
- **AC-3** *Given* kopia z wersji sprzed tej pozycji *When* odtwarzam ją w nowej *Then* dane są kompletne (test migracji, próbne odtworzenie).

## Notes
- Prototyp to tylko decyzje autora, więc może iść równolegle z budową [[ISSUE-041-google-play-and-safe-update]]…[[ISSUE-043-grave-paid-until]];
  budowa przed instalacją, jeśli zmieści się w terminie — inaczej po wyjeździe (zmiana bazy na prawdziwych danych, z testem migracji).
