---
title: "US-007 — Cemetery as a map: schematic plan offline, photo from above online, the author's quarters, candles (mapa cmentarza)"
type: user-story
status: done
epic: "[[EPIC-002-wizyta]]"
persona: "[[P1-zbierajacy]]"
moscow: [M3, M7]
journey-steps: "UJ-001 · 2, 7 (widok 2, R2)"
FR: []
NFR: ["[[NFR-001-offline]]", "[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
issues: ["[[ISSUE-027-cemetery-map-plan-photo-states]]", "[[ISSUE-028-cemetery-sectors]]"]
quality-verdict: APPROVED
verdict-date: 2026-10-12
verdict-reviewer: self-check
source: "[[SPIKE-004-mvp-flow-prototype]] D8–D12 · [[ADR-003-map-source-offline]] · [[cmentarz]] v4.1 · EPIC-002 → Input from SPIKE-001"
created: 2026-10-08
updated: 2026-10-12
---

# US-007 — Mapa cmentarza

## Story
**Jako** Zbierający **chcę** widzieć cmentarz jako plan z kwaterami i zniczami grobów, także bez zasięgu, **żeby** znaleźć
grób rodziny bez papierowych notatek i bez planu przy bramie.

## Acceptance Criteria
- **AC-1 — plan offline.** *Given* cmentarz dodany z siecią *When* otwieram go w trybie samolotowym *Then* widzę plan
  schematyczny (obrys, alejki z OSM) z „Plan offline” i „© OpenStreetMap” ([[ADR-003-map-source-offline]] pkt 1).
- **AC-2 — zdjęcie z góry online.** *When* przełączam na „Zdjęcie” z siecią *Then* widzę ortofotomapę GUGiK; bez sieci —
  „bez internetu”, a plan działa; nic nie zapisuje się w telefonie (pkt 2).
- **AC-3 — sama mapa, jeden grób, lista.** *Given* groby z pinezką i bez *Then* na starcie jest sama mapa i pasek grobów
  z liczbą grobów bez pinezki; znicz → arkusz grobu z „Pokaż grób”; przeciągnięcie → lista wszystkich grobów
  ([[cmentarz]] stany A, B, C; D11, D14).
- **AC-4 — kwatery autora.** *Given* kwatera zaznaczona przez autora *Then* plan pokazuje ją przerywaną linią z nazwą;
  kwatera bez strefy jest tylko w adresach ([[cmentarz]] D13).
- **AC-5 — bez planu.** *Given* cmentarz dodany bez sieci *Then* jest zaślepka „pobierze się, gdy będzie internet” i
  „Pobierz teraz”, a lista grobów działa.

## Out of scope
- Pinezka z GPS na miejscu, „gdzie jestem” → [[US-008-pinezka-na-miejscu]].
- Link do Grobonetu i wyszukiwarki zarządcy — wycofany (SPIKE-004 D10).

## Notes
- **Do zaprojektowania przed planem (`ui`):** jak autor **zaznacza kwaterę** na planie albo zdjęciu z góry — SPIKE-004
  tego nie pokazał ([[cmentarz]] → *Navigation*).
- **Uprawnienie `INTERNET`** wchodzi z tą US — tylko do pobrania planu i zdjęcia z góry ([[ADR-003-map-source-offline]]
  pkt 4).
- **Rozstrzygnięte w [[ISSUE-028-cemetery-sectors]] (stop #1, 2026-10-12):** zaznaczanie kwatery celownikiem (K1), kwatera jako rekord,
  na który wskazuje grób ([[ADR-016-sector-record-and-grave-link]]).
- **Poza AC tej US, przyjęte przez autora w ISSUE-028 (D3):** wpisanie **adresu zarządcy** grobu (kwatera, rząd, miejsce) w oknie
  „Popraw grób” ([[grob]] v6). To była luka M1 (brief §5 — „adres kwatery”): kolumny istniały od v1, ale żaden ekran ich nie
  zapisywał. Właścicielem tematu w wymaganiach jest [[US-002-przepisanie-grobu]] (AC-5 dopuszcza brak adresu) — tu zapisane, gdzie
  powstało.

## Verification (US)
> `qa`, 2026-10-12. Werdykt na poziomie US wystawił **niezależny przegląd**: subagent bez udziału w budowie, tylko odczyt plików i
> przebieg testów US (10 plików, **161/161**, dwa razy). Po przeglądzie `qa` dopisał asercję z uwagi 1 (linia przerywana 5/4).
> DoD US: każde AC z testem happy-path · pokazane w aplikacji na emulatorze · werdykt zapisany · wiersz w `TRACEABILITY.md`.

| AC | Test happy-path | Pokazane człowiekowi (emulator) |
|---|---|---|
| AC-1 plan offline | `cemetery_map_screen_test.dart` „AC-1 — a cemetery with its plan…” (plan z bazy, „Plan offline”, „© OpenStreetMap”, sieć niepytana) · `osm_plan_test.dart` · `overpass_plan_source_test.dart` · `cemetery_plans_test.dart` | **Autor** ([[ISSUE-027-cemetery-map-plan-photo-states]], stop #2): kroki 1–2 „ok”, ze śladem na urządzeniu. **Agent:** zimny start w trybie samolotowym |
| AC-2 zdjęcie z góry online, „bez internetu” | `cemetery_map_screen_test.dart` „AC-2 — "Zdjęcie" with a network…” · `hosts_test.dart` (kafelki nigdy nie zostają) | **Autor:** kroki 1–2 „ok”. **Agent:** brak kafelków w `cache`, 0 adresów GUGiK w logu |
| AC-3 mapa · jeden grób · lista | `cemetery_map_screen_test.dart` „AC-3 — at first only the map…”, „D23 — from a person's "Pochówek"…” | **Autor:** krok 3 „ok”, **bez śladu na urządzeniu**. **Agent:** przejście A → B → C → wstecz |
| AC-4 kwatery autora | `sectors_test.dart` „US-007 AC-4 — a sector with its zone and one only in an address…” · `sectors_screen_test.dart` „US-007 AC-4, What to build 3…”, „element 15, D24…” (strefa bez wypełnienia, **linia 5/4** — dopisane po przeglądzie, nazwa) | **Autor: nic** — stop #2 [[ISSUE-028-cemetery-sectors]] „pomiń” dla wszystkich kroków. **Agent:** strefa w A i E, na zdjęciu z góry, po odtworzeniu w trybie samolotowym |
| AC-5 bez planu | `cemetery_map_screen_test.dart` „AC-5 — a cemetery added without a network…”, „2a (a) and (c)…” | **Agent:** zaślepka → „Pobierz teraz” → pasek komunikatu → plan po powrocie sieci. Autor nie dostał tego kroku |

**Werdykt: APPROVED** z uwagami:
- **AC-4 nie przeszło przez ręce człowieka**, a AC-5 widział tylko agent. Wymóg „pokazane w aplikacji” spełnia przejście agenta. Krok 3
  autora przy AC-3 nie ma śladu na urządzeniu;
- zaślepki (c) i (d) mają tylko testy (Overpass był przeciążony). Koszt rysowania zmierzono na PC. TalkBack i test w słońcu — przy
  instalacji MVP;
- adres grobu wykracza poza AC (*Notes* wyżej) — zmiana zakresu przyjęta przez autora.

**Czego szukano i nie znaleziono:**
- AC bez testu, testy czerwone albo pominięte;
- naruszenia *Out of scope*: brak pakietu GPS i uprawnienia lokalizacji w `pubspec.yaml`, manifeście i `lib/`; brak Grobonetu w
  `lib/`;
- decyzja sprzeczna z AC: K1 i odnośnik (ADR-016) spełniają AC-4.
