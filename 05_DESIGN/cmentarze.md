---
screen: "Cmentarze — ekran główny (do czasu mapy)"
items: ["[[ISSUE-012-transcribe-grave-screen]]"]
us: "[[US-002-przepisanie-grobu]]"
journey-step: "n/a — M1 (warunek kroku 1 UJ-001); forma przejściowa widoku 1 (R1) do czasu mapy Polski (M2)"
mockup: "katalog tymczasowy sesji 2026-10-06: makieta-przepisanie-grobu.html (ramki 1–3)"
updated: 2026-10-06
---

# Cmentarze — specyfikacja

> ⚠️ **Do przebudowy — decyzja autora 2026-10-06.** Ekranem głównym jest mapa Polski ze zniczami
> cmentarzy ([[ISSUE-014-home-map-of-poland]], R1), a nie ta lista. `ui` przepisze ten plik (albo zastąpi
> go specyfikacją mapy) przed planem ISSUE-014. Treść niżej to pierwsza wersja (ISSUE-013), zostawiona
> jako punkt wyjścia: karty cmentarzy wracają w wynikach wyszukiwarki i w arkuszu.

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] · referencja: [[references]] → R1.

## Purpose
**Ekran główny aplikacji** do czasu mapy Polski. Pokazuje cmentarze, na których leżą groby rodziny, i
prowadzi do przepisywania z notatek. Notatki przepisuje się cmentarz po cmentarzu, jako 10 plasterków
([[NT-002-transcribe-the-notes]]), więc postęp plastra widać w karcie: „6 grobów · 14 osób”. Docelowo
(R1) ten sam wybór cmentarza robi mapa z pinezkami, a karta cmentarza staje się dolnym arkuszem.

## Navigation
- **Ekran główny:** aplikacja otwiera się od razu tutaj. **Ekran startowy z ISSUE-002 znika**, a z nim
  bursztynowa kreska pod nazwą: znakiem marki jest znicz + „Grobing” w pasku (R1, [[style-b]] reguła 8).
  Natywny ekran uruchamiania (tło `grobing_background`) zostaje.
- Koło zębate w pasku → ustawienia. Dziś jedyną pozycją jest **„Stan danych”** (ISSUE-007), więc koło
  otwiera go od razu. Lista ustawień powstanie, gdy dojdzie druga pozycja.
- Dotknięcie karty cmentarza → [[cmentarz]].
- „Dodaj cmentarz” → okno dialogowe (nazwa, miejscowość) → po dodaniu od razu [[cmentarz]] nowego
  cmentarza.
- Wstecz → wyjście z aplikacji (ekran główny).
- **Docelowo** ([[references]] → *Target app structure*): zakładki Mapa · Osoby · Drzewo i wyszukiwarka
  (S5). W tej pozycji ich nie ma — powstają z pierwszym celem drugiej zakładki ([[style-b]] reguła 12).

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | Pasek: **ikona znicza (akcent) + „Grobing”** (półgruby, 22 sp); po prawej koło zębate (`settings_outlined`, tekst pomocniczy, `tooltip` „Ustawienia”) | pasek | koło → „Stan danych” | — | — | R1 · decyzja projektowa |
| 2 | Nagłówek sekcji: „Cmentarze” (tekst pomocniczy, 13 sp) | tekst | — | — | — | decyzja projektowa |
| 3 | **Karty cmentarzy:** nazwa (tekst, 16 sp, półgruby) + druga linia „Miejscowość · 6 grobów · 14 osób” (tekst pomocniczy) + chevron „›” | lista kart na powierzchni, karta ≥ 64 dp | dotknięcie → [[cmentarz]] | alfabetycznie po nazwie, z polskimi literami | — | ISSUE-012 *What to build* 1 · R1 |
| 4 | „Dodaj cmentarz” | przy niepustej liście **przycisk z obrysem** z ikoną `add_location_alt_outlined` w akcencie; przy pustej **wypełniony** (główne działanie) | dotknięcie → okno 5–7 | — | — | *What to build* 1 · [[style-b]] reguła 1 |
| 5 | Okno: **Nazwa** | pole tekstowe, wielka litera na początku słów | `next`; po otwarciu okna fokus i klawiatura od razu | pusto | wymagana: „Podaj nazwę cmentarza.” | *What to build* 1 |
| 6 | Okno: **Miejscowość** | pole tekstowe, wielka litera na początku słów | `done` = „Dodaj” | pusto | opcjonalna | *What to build* 1 |
| 7 | Okno: „Anuluj” · **„Dodaj”** | przyciski tekstowe; „Dodaj” w akcencie | dotknięcie | — | pusta nazwa → komunikat przy polu 5, okno zostaje | *What to build* 1 |

Liczby odmieniają się po polsku: 1 grób · 2–4 groby · 5+ grobów (też 12–14 grobów, 22–24 groby) · 0
grobów; tak samo osoba / osoby / osób.

**Dlaczego główne działanie zmienia formę:** przy niepustej liście główną czynnością jest otwarcie
cmentarza (dotknięcie karty, jak „Otwórz cmentarz” w R1). Dodanie nowego cmentarza zdarza się ok. 10 razy
na całe notatki, więc jest drugorzędne. Przy pustej liście nie ma czego otworzyć i dodanie staje się
głównym działaniem.

## States
| Stan | Co widać |
|---|---|
| pusty | „Nie ma jeszcze żadnego cmentarza.” (tekst pomocniczy, środek) + wypełnione „Dodaj cmentarz” |
| błąd | odczyt bazy się nie udał: „Nie udało się odczytać cmentarzy.” + „Spróbuj ponownie” (przycisk z obrysem). W oknie dodawania: komunikat przy polu nazwy w kolorze błędu, z ikoną |
| wypełniony | pasek, nagłówek i karty jak wyżej, „Dodaj cmentarz” z obrysem na dole |
| wczytywanie | wskaźnik postępu na środku (baza lokalna, zwykle niewidoczny) |

## Sketch
```
┌──────────────────────────────────┐
│ 🕯 Grobing                     ⚙ │  ← znicz w akcencie
│                                  │
│  Cmentarze                       │
│ ╭──────────────────────────────╮ │
│ │ Cmentarz Próbny            › │ │
│ │ Wieś Przykładowa · 0 grobów  │ │
│ ╰──────────────────────────────╯ │
│ ╭──────────────────────────────╮ │
│ │ Cmentarz Wymyślony         › │ │
│ │ Miejscowość Testowa ·        │ │
│ │ 3 groby · 6 osób             │ │
│ ╰──────────────────────────────╯ │
│                                  │
│ ╭──────────────────────────────╮ │
│ │  ⊕ Dodaj cmentarz            │ │  ← obrys, ikona w akcencie
│ ╰──────────────────────────────╯ │
└──────────────────────────────────┘
```

## Tempo
Raz na plaster, nie na rekord: otwarcie aplikacji → karta cmentarza = **1 dotknięcie** na sesję
przepisywania (wcześniej 2, przez ekran startowy). Nowy cmentarz: „Dodaj cmentarz” + nazwa + `next` +
miejscowość + `done` = **3 akcje** poza pisaniem, ok. 10 razy na całe notatki.

## Style B rules applied
- Reguła 1: wypełniony przycisk tylko w stanie pustym; przy liście „Dodaj cmentarz” z obrysem i ikoną w
  akcencie.
- Reguła 2: karty na powierzchni, promień 16 dp.
- Reguła 4: „Grobing” i nazwy cmentarzy półgrube.
- Reguła 6: liczby odmienione po polsku.
- Reguła 8: znicz w logo.
- Reguły 9, 11 i 12: pusty stan z jednym działaniem; karty z chevronem; koło zębate → ustawienia.
- Pola w oknie: ramka w roli **obrysu**, komunikat w roli **błędu** ([[wpis-osoby]] → *Style B rules
  applied*).

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-002 AC-1, *Given* „cmentarz w aplikacji” | 4–7, 3 | cmentarz dodany oknem jest w kartach i otwiera [[cmentarz]] |
| ISSUE-012: ekran stosuje wytyczne stylu B | całość | reguły wyżej; przegląd `ui` przed stopem #2 |

## Decisions
- **Lista cmentarzy jako ekran główny, ekran startowy znika.** Bliżej docelowego układu z R1 (ekran główny =
  cmentarze, dziś jako karty, docelowo na mapie) i o jedno dotknięcie szybciej na każdą sesję. *Obali:*
  autor chce ekranu powitalnego z samą nazwą.
- **„Stan danych” pod kołem zębatym** (R1): to narzędzie kontroli, nie praca.
- **Po dodaniu cmentarza od razu jego ekran:** cmentarz dodaje się po to, żeby na nim przepisywać.
  *Obali:* autor dodaje kilka cmentarzy naraz przed przepisywaniem.
- **Okno dialogowe zamiast osobnego ekranu:** dwa pola nie potrzebują ekranu.
- **Te same nazwy są dozwolone** (dwa „Cmentarz Parafialny” w różnych miejscowościach), a rozróżnia je
  miejscowość.
- **Bez miniatury zdjęcia** w karcie: cmentarze nie mają zdjęć w modelu danych. Miniatura (R1) dojdzie, gdy
  pojawi się zdjęcie cmentarza.

## Open
brak.
