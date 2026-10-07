---
screen: "Zdjęcie — wybór źródła i podgląd na pełnym ekranie"
items: ["[[ISSUE-016-photos-grave-and-person]]"]
us: "[[US-005-zdjecia]]"
journey-step: "n/a — M1; docelowo krok 3 UJ-001 (porównanie zdjęcia nagrobka z tym, co przed tobą — brief §4a)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-zdjecia.html (ramki 3, 5, 6 — wersja przed stopem #1: kilka zdjęć nagrobka; obowiązuje ta specyfikacja)"
updated: 2026-10-07
---

# Zdjęcie — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.8, reguła 14) · referencja: brak w
> [[references]] (R1–R4 pokazują zdjęcia w widokach, nie podgląd ani wybór źródła), więc ekran dziedziczy
> reguły stylu B.
>
> **Wersja 1.1 (2026-10-07, po stopie #1 ISSUE-016).** Trzy części: arkusz wyboru źródła (A), podgląd na pełnym
> ekranie (B), okno usunięcia (C). **Decyzje autora:** nagrobek ma **jedno** zdjęcie, które da się zmienić i
> usunąć; zdjęcia osób to baza zdjęć z „profilowym” — [[ISSUE-017-person-photos]]. Elementy oznaczone „kierunek dla
> ISSUE-017” nie wchodzą w ISSUE-016; ich ostateczny kształt ustala `ui` przed planem ISSUE-017.
>
> **Wersja 1.2 (2026-10-07, przegląd `ui` zbudowanego ekranu):** systemowe okno wyboru (Android 16) wymaga
> „Gotowe” także przy jednym zdjęciu — **4 dotknięcia z galerii** (*Tempo*, D2, D5). Zmierzone dwiema drogami:
> `ACTION_GET_CONTENT` i Android Photo Picker (`PICK_IMAGES`) — obie z „Gotowe”. „B — wczytywanie”: samo tło.
> Okno C: treść 16 sp w kolorze tekstu. „Zapisuję zdjęcie…” w B dopiero po wyborze (MAJOR poprawiony w kodzie).

## Purpose
Dodanie zdjęcia nagrobka do grobu (US-005 AC-1) i obejrzenie go w całości, z przybliżeniem. Zdjęcie nagrobka ma
posłużyć do rozpoznania grobu na miejscu (brief §4a, krok 3), a napis na tablicy trzeba umieć przeczytać, więc
podgląd pokazuje cały kadr i pozwala przybliżyć.

## Navigation
- **A — arkusz źródła** otwiera się z pola „Dodaj zdjęcie nagrobka” w [[grob]] (element 1a, v3.2) albo z „Zmień zdjęcie” w podglądzie
  (B4). Wybór → systemowe okno wyboru zdjęć (jedno zdjęcie) albo systemowy aparat. Okno wyboru pokazuje wszystkie
  zdjęcia i albumy w telefonie, więc dawno zrobione zdjęcie (np. zdjęcie zdjęcia z albumu) da się znaleźć i dodać
  później (przypadek autora ze stopu #1). Anulowanie w systemowym oknie wraca bez zmian.
- **B — podgląd** otwiera się po dotknięciu zdjęcia nagrobka w [[grob]] (element 1a). Wstecz → [[grob]].
- **C — okno „Usunąć zdjęcie?”** z podglądu. Po usunięciu → [[grob]] bez zdjęcia, z polem „Dodaj zdjęcie nagrobka”.

## Elements in order

### A — arkusz źródła (dolny arkusz na powierzchni)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| A1 | **Tytuł:** „Zdjęcie nagrobka” (16 sp, półgruby) | tekst | — | — | — | decyzja projektowa |
| A2 | **„Wybierz z galerii”** — wiersz ≥ 56 dp, ikona `photo_library_outlined` w akcencie, napis w kolorze tekstu (16 sp) | wiersz-przycisk | → systemowe okno wyboru zdjęć, **jedno zdjęcie** | — | — | US-005 AC-1 · D1 · D2 |
| A3 | **„Zrób zdjęcie”** — wiersz jak A2, ikona `photo_camera_outlined` | wiersz-przycisk | → systemowy aparat; jedno zdjęcie | — | — | US-005 AC-1 · D1 |

### B — podgląd na pełnym ekranie
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| B1 | **Pasek** na tle (nie na zdjęciu): wstecz; tytuł — nazwa grobu (bez nazwy „Grób”), 16 sp, półgruby, jedna linia, ucięta; podtytuł „Zdjęcie nagrobka” (14 sp, tekst pomocniczy) | pasek | wstecz | — | — | decyzja projektowa · [[style-b]] reguła 14 (nic na zdjęciu) |
| B2 | **Zdjęcie w całości** na tle (dopasowane, bez przycinania). **Przybliżenie:** rozsunięcie dwoma palcami do 4×; **podwójne dotknięcie** przybliża 2,5× w miejscu dotknięcia, a kolejne oddala. Przybliżone przesuwa się palcem | obraz | gesty jak obok | całe zdjęcie, bez przybliżenia | — | brief §4a krok 3 · D3 · D4 (SC 2.5.1) |
| B3 | **Poprzednie / następne** — *kierunek dla ISSUE-017* (baza zdjęć osoby): przyciski-ikony `chevron_left` / `chevron_right` (kolor tekstu, cel 48 × 48 dp, `tooltip`) jako alternatywa dla przesunięcia w bok. **W ISSUE-016 nie ma** — nagrobek ma jedno zdjęcie | — | — | — | — | WCAG 2.2 SC 2.5.1 |
| B4 | **Działania** w dolnym pasku: **„Zmień zdjęcie”** — przycisk tekstowy w akcencie, ikona `photo_library_outlined` → A; po wyborze nowe zdjęcie zastępuje stare i podgląd je pokazuje (D5). **„Usuń zdjęcie”** — przycisk tekstowy z ikoną `delete_outline`, oba w kolorze tekstu → C | przyciski tekstowe | dotknięcie | — | — | decyzja autora (stop #1 ISSUE-016) · D5 |

### C — okno „Usunąć zdjęcie?”
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| C1 | Tytuł „Usunąć zdjęcie?”, treść (16 sp, kolor tekstu — jak w oknie „Odrzucić wpis?”): „Zdjęcia nie będzie w aplikacji ani w kolejnych kopiach. Jeśli jest w galerii telefonu, tam zostaje.” Przyciski: „Usuń” (kolor tekstu) · **„Zostaw”** (akcent — bezpieczne działanie jest główne) | okno dialogowe | „Zostaw” zamyka okno; „Usuń” usuwa i wraca do [[grob]] | — | — | [[style-b]] reguła 10 · wzorzec okna „Odrzucić wpis?” z [[wpis-osoby]] |

## States
| Stan | Co widać |
|---|---|
| A — otwarty | A1–A3 nad przyciemnionym ekranem; dotknięcie poza arkuszem albo wstecz zamyka go bez zmian |
| B — wczytywanie | samo tło (v1.2: odczyt trwa ułamek sekundy, więc wskaźnik by tylko mignął) |
| B — wypełniony | B1, B2, B4 |
| B — zmiana w toku | **dopiero po wyborze** nowego zdjęcia (przy otwartym arkuszu i oknie systemowym widać obecne zdjęcie): wskaźnik postępu na środku i „Zapisuję zdjęcie…” (14 sp, tekst pomocniczy); B4 nieaktywne. Potem nowe zdjęcie |
| B — nieudana zmiana | pod zdjęciem: `error_outline` + „Nie udało się zapisać zdjęcia. Spróbuj jeszcze raz.” (kolor błędu); stare zdjęcie zostaje |
| B — błąd odczytu | na środku `broken_image_outlined` (tekst pomocniczy) i „Nie udało się otworzyć zdjęcia.” (14 sp, tekst pomocniczy). B4 zostaje — zdjęcie da się zmienić albo usunąć |
| C — otwarte | okno nad podglądem |
| C — nieudane usunięcie | w oknie pod treścią: `error_outline` + „Nie udało się usunąć zdjęcia. Spróbuj jeszcze raz.” (kolor błędu); okno zostaje |

## Sketch
```
 A — arkusz źródła                    B — podgląd
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│ ←  Cmentarz Wymyślony · Miejsco… │  │ ←  Grób rodzinny Wymyślonych     │
│      ░░░░░░░░░░░░░░░░░░░░░░░░    │  │    Zdjęcie nagrobka              │
│      ░░ (widok grobu,     ░░░    │  │                                  │
│      ░░  przyciemniony)   ░░░    │  │   ┌──────────────────────────┐   │
│      ░░░░░░░░░░░░░░░░░░░░░░░░    │  │   │                          │   │
│ ╭──────────────────────────────╮ │  │   │   [zdjęcie w całości,    │   │
│ │ Zdjęcie nagrobka             │ │  │   │    bez przycinania]      │   │
│ │                              │ │  │   │                          │   │
│ │ ▣  Wybierz z galerii         │ │  │   └──────────────────────────┘   │
│ │ ◎  Zrób zdjęcie              │ │  │                                  │
│ ╰──────────────────────────────╯ │  │  ▣ Zmień zdjęcie   🗑 Usuń zdjęcie │
└──────────────────────────────────┘  └──────────────────────────────────┘

 C — okno usunięcia
╭────────────────────────────────╮
│ Usunąć zdjęcie?                │
│ Zdjęcia nie będzie w aplikacji │
│ ani w kolejnych kopiach. Jeśli │
│ jest w galerii telefonu, tam   │
│ zostaje.                       │
│                 Usuń   Zostaw  │
╰────────────────────────────────╯
```

## Tempo
Rekordem jest **zdjęcie nagrobka**: ok. 50 grobów (G6, [[NT-002-transcribe-the-notes]]).
- **Z galerii:** pole „Dodaj zdjęcie nagrobka” → „Wybierz z galerii” → zdjęcie → „Gotowe” w systemowym oknie = **4 dotknięcia**
  (v1.2: zmierzone na Androidzie 16 — okno wymaga potwierdzenia także przy jednym zdjęciu, poza kontrolą
  aplikacji; na Androidzie 13–15 Photo Picker może wracać od razu, wtedy 3).
- **Aparatem:** „Dodaj zdjęcie” → „Zrób zdjęcie” → spust → zatwierdzenie w aplikacji aparatu = 4 dotknięcia.
- Na całość: ok. 50 × 4 = **ok. 200 dotknięć**.
- **Zmiana:** zdjęcie → „Zmień zdjęcie” → „Wybierz z galerii” → zdjęcie → „Gotowe” = 5 dotknięć.

## Style B rules applied
- **Reguła 14 (v1.7):** zdjęcie to treść użytkownika — bez filtrów i bez tekstu na zdjęciu; podgląd na tle; gesty
  mają alternatywę jednym dotknięciem (SC 2.5.1): podwójne dotknięcie zamiast rozsunięcia palców.
- **Reguła 1:** w podglądzie i arkuszu nie ma wypełnionego przycisku. „Zmień zdjęcie” w akcencie (główne działanie
  podglądu), „Usuń zdjęcie” w kolorze tekstu. W oknie C potwierdza bezpieczne „Zostaw” w akcencie.
- **Reguła 3:** ikony źródła w akcencie (działania); `delete_outline` w kolorze tekstu — usunięcie to działanie, ale
  nie zapraszamy do niego akcentem.
- **Reguła 7:** treść okna C mówi faktem, co przepadnie i co zostaje, bez straszenia.
- **Reguła 10:** dodanie i zmiana kończą się widokiem zdjęcia, bez okienka „Zapisano”.
- **Kolor błędu** tylko w komunikacie błędu, nigdy na „Usuń”.
- **Tokeny:** bez nowych.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-005 AC-1 (grób) | A2, A3 → [[grob]] 1a | zdjęcie wybrane z galerii albo zrobione aparatem pojawia się nad tytułem grobu |
| US-005 AC-2 | B2 | podgląd otwiera zdjęcie z magazynu aplikacji; po usunięciu oryginału z galerii dalej się otwiera |
| US-005 AC-3 | B2 | po odtworzeniu z kopii podgląd otwiera to samo zdjęcie (odcisk danych — `qa`) |
| ISSUE-016: zmiana i usunięcie (decyzja autora) | B4, C | „Zmień zdjęcie” → nowe zdjęcie; „Usuń zdjęcie” → okno → zdjęcia nie ma |
| ISSUE-016: styl B | całość | reguły wyżej; przegląd `ui` przed stopem #2 |

## Decisions
- **D1 — najpierw galeria, potem aparat.** Przepisywanie odbywa się w domu: zdjęcia nagrobków zrobione na
  cmentarzu i zdjęcia starych fotografii już są w galerii (także takie sprzed miesięcy — przypadek autora ze stopu
  #1). Aparat przydaje się przy babci i przy wizycie. *Obali:* autor częściej robi zdjęcie na bieżąco niż wybiera z
  galerii.
- **D2 — jedno zdjęcie z galerii** (v1.1, decyzja autora: jedno zdjęcie nagrobka). Systemowe okno wymaga
  potwierdzenia „Gotowe” (Android 16, zmierzone 2026-10-07) — poza kontrolą aplikacji (v1.2). Wybór kilku wraca w
  bazie zdjęć osoby ([[ISSUE-017-person-photos]]).
- **D3 — podgląd bez przycinania, z przybliżeniem.** Zdjęcie nagrobka służy do porównania z tym, co przed tobą
  (brief §4a krok 3), a napis na tablicy trzeba przeczytać. Przycięte jest tylko zdjęcie w widoku grobu
  ([[grob]] D8) i miniatura w [[cmentarz]]; tutaj widać całość. Przybliżenie ma sens do ok. 2× — zdjęcie w
  aplikacji ma 2048 px po dłuższym boku (decyzja autora D2', stop #1 ISSUE-016).
- **D4 — gesty mają alternatywę jednym dotknięciem** (WCAG 2.2 SC 2.5.1, poziom A: *„All functionality that
  uses multipoint or path-based gestures for operation can be operated with a single pointer without a
  path-based gesture”* — [Understanding 2.5.1](https://www.w3.org/WAI/WCAG22/Understanding/pointer-gestures.html)).
  Rozsunięcie palców → podwójne dotknięcie w wybranym miejscu, które jednocześnie wybiera, co przybliżyć.
- **D5 — „Zmień zdjęcie” bez okna potwierdzenia, „Usuń zdjęcie” z oknem.** Zmiana wymaga wybrania nowego zdjęcia
  (4 świadome dotknięcia, v1.2), więc nie dzieje się przypadkiem; usunięcie to jedno dotknięcie, a kopia jest jedna i
  nadpisywana ([[backup-format]] → *Known limits*) — po następnej kopii zdjęcia nie ma nigdzie poza galerią, stąd
  okno C (reguła 10). *Obali:* autor zmienia zdjęcie przez pomyłkę — wtedy okno także przy zmianie.
- **D6 — tekst nigdy na zdjęciu.** Kontrastu tekstu na zdjęciu nie da się zagwarantować (SC 1.4.3), a zdjęcie
  to treść użytkownika.

## Open
brak. Usuwanie i zmiana zdjęcia nagrobka rozstrzygnięte na stopie #1 ISSUE-016 (wchodzą). Zdjęcia osób →
[[ISSUE-017-person-photos]] (`ui` projektuje bazę zdjęć osoby przed planem).
