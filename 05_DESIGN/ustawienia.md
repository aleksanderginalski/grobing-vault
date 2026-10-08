---
screen: "Ustawienia — ja, kopia, eksport dla rodziny, notka przekazania, stan danych"
items: ["[[SPIKE-004-mvp-flow-prototype]]"]
us: "[[US-006-eksport-dla-rodziny]] (eksport) · [[US-001-kopia-z-odtworzeniem]] (kopia, zbudowana) · ustawienie „ja” (M5, [[data-model]])"
journey-step: "n/a — M8 (przeżywa telefon i aplikację)"
mockup: "2026-10-08: grobing-prototyp.html (SPIKE-004, panel 9) — katalog tymczasowy sesji, ścieżka w SPIKE-004"
updated: 2026-10-08
---

# Ustawienia — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.16) · referencja: [[references]] → R1 (koło zębate).
>
> **Wersja 1 — discovery na prototypie, panel 9 ([[SPIKE-004-mvp-flow-prototype]] D23, 2026-10-08).** Autor: *„7. ok”*.
> Dziś koło zębate otwiera od razu „Stan danych” (ekran techniczny z ISSUE-007…010). Ustawienia stają przed nim jako
> lista, a „Stan danych” schodzi o poziom niżej. Ekran eksportu jest tu, bo prowadzi do niego tylko ta lista.

## Purpose
Jedno miejsce na to, co nie jest rodziną ani mapą: **kim jestem w drzewie** („ja”), **czy kopia działa**, **eksport i
notka dla rodziny** (M8: przeżywa telefon i aplikację) i dane techniczne.

## Navigation
- **Koło zębate na ekranie głównym** ([[cmentarze]] element 1) → ta lista. Bez dolnego paska — to nie jest zakładka
  ([[style-b]] reguła 12).
- „Odtwórz z kopii” i „Stan danych” → dzisiejszy ekran „Stan danych” (bez zmian).
- „Eksport dla rodziny” → ekran eksportu (elementy 8–11).
- Wstecz → ekran główny.

## Elements in order
**Lista ustawień** — sekcje z nagłówkiem (13 sp, tekst pomocniczy), wiersze ≥ 56 dp z linią podziału, ikona z lewej (akcent
— działanie; tekst pomocniczy — informacja), tytuł 16 sp półgruby, opis 13 sp tekst pomocniczy, chevron, gdy prowadzi dalej

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Ty w drzewie — „Ja”**: inicjały „Ja” w akcencie (albo profilowe tej osoby), „Od tej osoby liczą się łańcuchy i nazwy pokrewieństwa” | wiersz | → wybór osoby z listy (jak [[osoby]]) | brak — pierwszy start prosi o wybór przy pierwszym łańcuchu | — | M5 · [[data-model]] („ja”) |
| 2 | **Kopia — „Ostatnia udana kopia”**: `cloud_done` w zieleni stanu, „dziś, 11:42 (w tle) · Dysk Google” | wiersz (informacja) | — | — | — | US-001 (zbudowane: „Stan danych”) |
| 3 | **„Zrób kopię teraz”** (`backup`, akcent) | wiersz | zrób kopię | — | — | US-001 |
| 4 | **„Odtwórz z kopii”** (`settings_backup_restore`, akcent) — „Nowy telefon albo utracone dane” | wiersz | → „Stan danych” → odtworzenie (jak dziś) | — | — | US-001 · [[NFR-002-odtworzenie-na-nowym-telefonie]] |
| 5 | **Dla rodziny — „Eksport dla rodziny”** (`ios_share`, akcent) — „HTML i PDF — otworzą się bez Grobing” | wiersz | → eksport (8–11) | — | — | [[US-006-eksport-dla-rodziny]] |
| 6 | **„Notka przekazania”** (`description`, akcent) — „Gdzie jest kopia i jak ją otworzyć — na papierze, u rodziny” | wiersz | → opis tego, co ma być w notce ([[NT-007-hand-over-note]]); sama notka jest poza aplikacją | — | — | M8 · G2 · NT-007 |
| 7 | **Techniczne — „Stan danych”** (`database`, tekst pomocniczy) · **O aplikacji** — wersja i podpisy danych: „Mapy: © OpenStreetMap (ODbL) · Natural Earth · Ortofotomapa: GUGiK” | wiersze | „Stan danych” → dzisiejszy ekran | — | — | ISSUE-007 · licencje (ODbL) |

**Eksport dla rodziny** ([[US-006-eksport-dla-rodziny]])

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 8 | Pasek wstecz + „Eksport dla rodziny”; **opis**: „Czytelna kopia dla rodziny: jeden plik HTML i jeden PDF z osobami, rodzinami, grobami i datami. Otworzy się w zwykłej przeglądarce, bez Grobing.” (14 sp) | tekst | — | — | — | US-006 AC-1 |
| 9 | **„Zdjęcia”** — przełącznik (akcent, gdy włączony): „Portrety i nagrobki w pliku” | przełącznik | dotknięcie | włączony | — | decyzja projektowa (rozmiar pliku) |
| 10 | **„Osoby żyjące”** — przełącznik: „Domyślnie bez — eksport może trafić do innych” | przełącznik | dotknięcie | **wyłączony** | — | **decyzja autora** (D23) · brief §6 N3 (RODO, żyjący) |
| 11 | „Plik zapiszesz tam, gdzie wskażesz. Grobing nigdzie go nie wysyła.” (13 sp, tekst pomocniczy) i **wypełniony „Utwórz eksport”** (`ios_share`) | tekst + przycisk główny | → systemowe okno zapisu pliku → HTML i PDF | — | brak miejsca / błąd zapisu: komunikat z ikoną błędu nad przyciskiem | US-006 AC-3 · [[NFR-005-dane-nie-opuszczaja-telefonu]] |

## States
| Stan | Co widać |
|---|---|
| lista | 1–7 |
| kopia nieskonfigurowana | 2: `cloud_off` (tekst pomocniczy) „Kopia nie jest skonfigurowana” + 3 jako „Skonfiguruj kopię” |
| eksport | 8–11 |
| eksport w toku | 11: wskaźnik postępu w przycisku, przycisk nieaktywny |
| eksport gotowy | ciche potwierdzenie (reguła 10): „Zapisano: grobing-eksport-2026-10-08.html i .pdf” pod przyciskiem |

## Sketch
```
┌──────────────────────────────────┐   ┌──────────────────────────────────┐
│ ←  Ustawienia                    │   │ ←  Eksport dla rodziny           │
│ Ty w drzewie                     │   │ Czytelna kopia dla rodziny: HTML │
│ (Ja) Ja                        › │   │ i PDF z osobami, rodzinami, …    │
│ Kopia                            │   │ ▣ Zdjęcia                  [●━]  │
│ ☁✓ Ostatnia udana kopia          │   │ ◯ Osoby żyjące             [━○]  │
│ ⤒  Zrób kopię teraz              │   │ Plik zapiszesz tam, gdzie …      │
│ ↺  Odtwórz z kopii             › │   │ ╭──────────────────────────────╮ │
│ Dla rodziny                      │   │ │      ⇪  Utwórz eksport       │ │
│ ⇪  Eksport dla rodziny         › │   │ ╰──────────────────────────────╯ │
│ ▤  Notka przekazania           › │   └──────────────────────────────────┘
│ Techniczne                       │
│ ⛁  Stan danych                 › │
└──────────────────────────────────┘
```

## Tempo
n/a — ekran ustawień.

## Style B rules applied
- **Reguła 12:** bez dolnego paska — ustawienia są pod kołem zębatym, nie zakładką.
- **Reguła 1:** jeden wypełniony przycisk („Utwórz eksport”); wiersze bez wypełnienia.
- **Reguła 3:** ikony działań w akcencie, informacji w tekście pomocniczym; stan kopii w zieleni stanu tylko z ikoną i
  tekstem.
- **Reguła 10:** eksport kończy się cichym potwierdzeniem, nie oknem.
- **Tokeny:** przełącznik — akcent (włączony) i obrys (wyłączony): istniejące pary.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-006 AC-1 — HTML i PDF bez aplikacji | 8, 11 | opis i przycisk; zapis dwóch plików |
| US-006 AC-3 — eksport nie idzie do chmury sam | 11 | systemowe okno zapisu; podpis „Grobing nigdzie go nie wysyła” |
| M8 / G2 — rodzina wie, że kopia istnieje | 6 | wiersz notki przekazania |

## Decisions
- **D1 — koło zębate → lista ustawień, „Stan danych” niżej** (D23). Kopia, eksport i „ja” to sprawy użytkownika, a
  „Stan danych” to diagnostyka. *Obali:* autor używa „Stanu danych” codziennie — wtedy wiersz na górze.
- **D2 — eksport domyślnie bez osób żyjących** (D23: *„7. ok”* na pytanie wprost). Eksport ma trafić do rodziny i może
  pójść dalej; dane żyjących chroni brief §6 N3. *Obali:* rodzina chce kompletnego drzewa z żyjącymi — przełącznik już
  jest.
- **D3 — notka przekazania jako opis, nie generator** — notka to kartka u rodziny (NT-007), poza aplikacją; aplikacja
  przypomina, co ma w niej być.

## Open
brak.
