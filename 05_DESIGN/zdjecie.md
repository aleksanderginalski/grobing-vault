---
screen: "Zdjęcie — wybór źródła i podgląd na pełnym ekranie"
items: ["[[ISSUE-016-photos-grave-and-person]]", "[[ISSUE-017-person-photos]]", "[[ISSUE-018-profile-photo-crop]]"]
us: "[[US-005-zdjecia]]"
journey-step: "n/a — M1; docelowo krok 3 UJ-001 (porównanie zdjęcia nagrobka z tym, co przed tobą — brief §4a)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-zdjecia.html (ramki 3, 5, 6 — wersja przed stopem #1 ISSUE-016) · makieta-zdjecia-osoby.html (ramki 5–8 — tryb osoby, ISSUE-017) · makieta-kadr-profilowego.html (ramki 1, 4 — B4' z kadrem, ISSUE-018)"
updated: 2026-10-07
---

# Zdjęcie — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.9, reguła 14) · referencja: brak w
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
>
> **Wersja 1.3 (2026-10-07, przed planem [[ISSUE-017-person-photos]]) — tryb osoby.** Ten sam arkusz i podgląd służą
> bazie zdjęć osoby ([[zdjecia-osoby]]). Różnice w trybie osoby:
> - **A:** tytuł „Zdjęcia osoby”; galeria pozwala wybrać **kilka** zdjęć;
> - **B:** poprzednie i następne (B3); nowa linia „Na zdjęciu” z „Zmień” (B5); w działaniach „Ustaw jako profilowe”
>   i „Usuń z tej osoby” zamiast „Zmień zdjęcie” i „Usuń zdjęcie” (B4');
> - **C:** treść zależy od tego, czy zdjęcie ma jeszcze inne osoby;
> - **nowa część D:** „Kto jest na zdjęciu?”.
>
> Tryb grobu bez zmian. Zmiany w trybie osoby zapisują się z „Zapisz” formularza osoby ([[zdjecia-osoby]] D1).
>
> **Wersja 1.4 (2026-10-07, przed planem [[ISSUE-018-profile-photo-crop]]) — kadr profilowego.** Tylko tryb osoby, B:
> - **B4' „Ustaw jako profilowe”** otwiera [[kadr-profilowego]], a zdjęcie staje się profilowym dopiero po „Gotowe” —
>   razem z kadrem ([[kadr-profilowego]] D2);
> - **na profilowym** dolny pasek ma **„Popraw kadr”** w miejscu tekstu „✓ Profilowe”, a stan „profilowe” niesie
>   podtytuł paska B1: „Zdjęcie profilowe” zamiast „Zdjęcie osoby” ([[kadr-profilowego]] D8).
>
> Podgląd dalej pokazuje całe zdjęcie, bez kadru.

## Purpose
Dodanie zdjęcia nagrobka do grobu (US-005 AC-1) i obejrzenie go w całości, z przybliżeniem. Zdjęcie nagrobka ma
posłużyć do rozpoznania grobu na miejscu (brief §4a, krok 3), a napis na tablicy trzeba umieć przeczytać, więc
podgląd pokazuje cały kadr i pozwala przybliżyć.

**Tryb osoby (v1.3):** dodanie zdjęć do bazy zdjęć osoby, obejrzenie każdego w całości, wybór profilowego i
zaznaczenie, kto jeszcze jest na zdjęciu — jedno zdjęcie należy wtedy do kilku osób, a plik jest jeden (ISSUE-017).

## Navigation
- **A — arkusz źródła** otwiera się z pola „Dodaj zdjęcie nagrobka” w [[grob]] (element 1a, v3.2) albo z „Zmień zdjęcie” w podglądzie
  (B4). Wybór → systemowe okno wyboru zdjęć (jedno zdjęcie) albo systemowy aparat. Okno wyboru pokazuje wszystkie
  zdjęcia i albumy w telefonie, więc dawno zrobione zdjęcie (np. zdjęcie zdjęcia z albumu) da się znaleźć i dodać
  później (przypadek autora ze stopu #1). Anulowanie w systemowym oknie wraca bez zmian.
- **B — podgląd** otwiera się po dotknięciu zdjęcia nagrobka w [[grob]] (element 1a). Wstecz → [[grob]].
- **C — okno „Usunąć zdjęcie?”** z podglądu. Po usunięciu → [[grob]] bez zdjęcia, z polem „Dodaj zdjęcie nagrobka”.

**Tryb osoby (v1.3):**
- **A** otwiera się z elementu 1a w [[wpis-osoby]] (osoba bez zdjęć) albo z kafelka „Dodaj zdjęcie” w
  [[zdjecia-osoby]]. Po wyborze z galerii wraca tam, skąd się otworzył, i nowe zdjęcia się przygotowują.
- **B** otwiera się po dotknięciu zdjęcia albo profilowego w [[zdjecia-osoby]], na tym zdjęciu. Wstecz →
  [[zdjecia-osoby]].
- **C** otwiera się z „Usuń z tej osoby” (B4'). Po „Usuń” → [[zdjecia-osoby]] bez tego zdjęcia.
- **D — „Kto jest na zdjęciu?”** otwiera się z „Zmień” w linii „Na zdjęciu” (B5). „Gotowe” → B z nową linią „Na
  zdjęciu”. Wstecz → B bez zmian, bez okna: przepadają najwyżej zaznaczenia (reguła 10).

## Elements in order

### A — arkusz źródła (dolny arkusz na powierzchni)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| A1 | **Tytuł:** „Zdjęcie nagrobka” (16 sp, półgruby) | tekst | — | — | — | decyzja projektowa |
| A2 | **„Wybierz z galerii”** — wiersz ≥ 56 dp, ikona `photo_library_outlined` w akcencie, napis w kolorze tekstu (16 sp) | wiersz-przycisk | → systemowe okno wyboru zdjęć, **jedno zdjęcie** | — | — | US-005 AC-1 · D1 · D2 |
| A3 | **„Zrób zdjęcie”** — wiersz jak A2, ikona `photo_camera_outlined` | wiersz-przycisk | → systemowy aparat; jedno zdjęcie | — | — | US-005 AC-1 · D1 |

**Tryb osoby (v1.3):** A1 — „Zdjęcia osoby”; A2 — systemowe okno wyboru **kilku zdjęć** (bez sztucznego limitu;
każde przygotowuje się osobno, [[zdjecia-osoby]] → *States*); A3 bez zmian. Kolejność nowych zdjęć: tak, jak
zwróci je okno systemowe (D8).

### B — podgląd na pełnym ekranie
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| B1 | **Pasek** na tle (nie na zdjęciu): wstecz; tytuł — nazwa grobu (bez nazwy „Grób”), 16 sp, półgruby, jedna linia, ucięta; podtytuł „Zdjęcie nagrobka” (14 sp, tekst pomocniczy) | pasek | wstecz | — | — | decyzja projektowa · [[style-b]] reguła 14 (nic na zdjęciu) |
| B2 | **Zdjęcie w całości** na tle (dopasowane, bez przycinania). **Przybliżenie:** rozsunięcie dwoma palcami do 4×; **podwójne dotknięcie** przybliża 2,5× w miejscu dotknięcia, a kolejne oddala. Przybliżone przesuwa się palcem | obraz | gesty jak obok | całe zdjęcie, bez przybliżenia | — | brief §4a krok 3 · D3 · D4 (SC 2.5.1) |
| B3 | **Poprzednie / następne** (tryb osoby, v1.3; tylko gdy osoba ma więcej niż jedno zdjęcie) — rząd pod zdjęciem, wyśrodkowany: `chevron_left` · „2 z 5” (14 sp, tekst pomocniczy) · `chevron_right`; przyciski-ikony w kolorze tekstu, cel 48 × 48 dp, `tooltip` „Poprzednie zdjęcie” / „Następne zdjęcie”; na pierwszym i ostatnim zdjęciu odpowiedni przycisk nieaktywny. **Przesunięcie w bok** zmienia zdjęcie tylko bez przybliżenia (z przybliżeniem przesuwa zdjęcie). **W trybie grobu nie ma** — nagrobek ma jedno zdjęcie | przyciski-ikony + gest | dotknięcie · przesunięcie | zdjęcie, które dotknięto w [[zdjecia-osoby]] | — | WCAG 2.2 SC 2.5.1 · [[style-b]] reguła 14 (nic na zdjęciu) |
| B5 | **Na zdjęciu** (tryb osoby, v1.3) — pod zdjęciem, nad B3: „Na zdjęciu:” (14 sp, tekst pomocniczy) i imiona i nazwiska osób z łączem do tego zdjęcia, po przecinku, **ta osoba pierwsza** (14 sp, kolor tekstu, zawijane, bez „z d.”); na końcu przycisk tekstowy w linii treści **„Zmień”** (akcent, reguła 1 v1.6, cel ≥ 48 dp) | tekst + przycisk tekstowy | „Zmień” → D | — | — | ISSUE-017 AC 5 · D6 ([[zdjecia-osoby]]) |
| B4 | **Działania** w dolnym pasku: **„Zmień zdjęcie”** — przycisk tekstowy w akcencie, ikona `photo_library_outlined` → A; po wyborze nowe zdjęcie zastępuje stare i podgląd je pokazuje (D5). **„Usuń zdjęcie”** — przycisk tekstowy z ikoną `delete_outline`, oba w kolorze tekstu → C | przyciski tekstowe | dotknięcie | — | — | decyzja autora (stop #1 ISSUE-016) · D5 |
| B4' | **Działania w trybie osoby** (v1.3), dolny pasek: **„Ustaw jako profilowe”** — przycisk tekstowy w akcencie, ikona `account_circle_outlined`; po dotknięciu zdjęcie staje się pierwszym łączem tej osoby, a na miejscu przycisku pojawia się stan. **Stan, gdy to już profilowe:** „Profilowe” z ikoną `check` (14 sp, tekst pomocniczy) — tekst, nie przycisk, ten sam stan dla czytnika. **„Usuń z tej osoby”** — przycisk tekstowy z ikoną `delete_outline`, w kolorze tekstu → C. **Bez „Zmień zdjęcie”**: w bazie się dodaje i usuwa, a nie podmienia. **v1.4:** „Ustaw jako profilowe” → [[kadr-profilowego]]; zdjęcie staje się profilowym po „Gotowe”, z kadrem. **Na profilowym zamiast stanu „✓ Profilowe”: „Popraw kadr”** — przycisk tekstowy w akcencie, ikona `crop_outlined` → [[kadr-profilowego]]; stan niesie podtytuł B1 („Zdjęcie profilowe”) | przyciski tekstowe | dotknięcie | — | — | ISSUE-017 AC 4, 6 · GEDCOM 7 („the first is the most-preferred value”) · D9 · ISSUE-018 AC 1, 3 ([[kadr-profilowego]] D2, D8) |

**B1 w trybie osoby (v1.3):** tytuł — imiona i nazwisko osoby, której bazę oglądamy (bez imion i nazwiska: „Nowa
osoba”); podtytuł „Zdjęcie osoby”, **a na profilowym „Zdjęcie profilowe”** (v1.4). Kolejność pod zdjęciem: B5, B3, B4'.

### C — okno „Usunąć zdjęcie?”
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| C1 | Tytuł „Usunąć zdjęcie?”, treść (16 sp, kolor tekstu — jak w oknie „Odrzucić wpis?”): „Zdjęcia nie będzie w aplikacji ani w kolejnych kopiach. Jeśli jest w galerii telefonu, tam zostaje.” Przyciski: „Usuń” (kolor tekstu) · **„Zostaw”** (akcent — bezpieczne działanie jest główne) | okno dialogowe | „Zostaw” zamyka okno; „Usuń” usuwa i wraca do [[grob]] | — | — | [[style-b]] reguła 10 · wzorzec okna „Odrzucić wpis?” z [[wpis-osoby]] |
| C1' | **Tryb osoby (v1.3).** **Zdjęcie tylko tej osoby:** jak C1. **Zdjęcie ma też inne osoby:** tytuł „Usunąć zdjęcie z tej osoby?”, treść „Zdjęcie zostaje u: Jan Wymyślony.” (osoby po przecinku). **Gdy to profilowe**, w obu wariantach dochodzi zdanie: „Profilowym zostanie następne zdjęcie.” (albo, gdy to ostatnie zdjęcie osoby: „Osoba nie będzie miała zdjęcia.”). Przyciski jak C1. **Usunięcie działa z „Zapisz” formularza** ([[zdjecia-osoby]] D1), więc okno nie mówi „od razu” | okno dialogowe | „Usuń” usuwa łącze tej osoby → [[zdjecia-osoby]] | — | — | ISSUE-017 AC 6 · [[style-b]] reguły 7, 10, 14 |

### D — „Kto jest na zdjęciu?” (tryb osoby, v1.3; pełny ekran)
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| D1 | **Pasek:** wstecz (bez zmian); tytuł „Kto jest na zdjęciu?” (16 sp, półgruby) | pasek | wstecz → B bez zmian | — | — | decyzja projektowa |
| D2 | **Zdjęcie** na tle, w całości (dopasowane, bez przycinania), **wysokość 160 dp**, wyśrodkowane, bez przybliżenia — żeby widzieć twarze, wybierając imiona | obraz | — | — | — | [[style-b]] reguła 14 · decyzja projektowa |
| D3 | **Pole „Szukaj osoby”** — ramka w kolorze obrysu, ikona `search` (tekst pomocniczy), bez fokusu od wejścia; filtruje obie sekcje bez polskich znaków i końcówek (`matchesQuery` jak w wyszukiwarce cmentarzy); `done` chowa klawiaturę | pole tekstowe | `done` | pusto | — | D7 |
| D4 | **Sekcja „W tym grobie”** (nagłówek 14 sp, półgruby, tekst pomocniczy) — **pierwszy wiersz: ta osoba**, zaznaczona i nieaktywna, z drugą linią „ta osoba”. Dalej osoby z grobu, z którego otwarto formularz, w kolejności wpisania (jak w [[grob]]). **Wiersz:** pole wyboru z lewej, imiona i nazwisko z „z d.” (16 sp, kolor tekstu), lata życia (14 sp, tekst pomocniczy, format jak w [[grob]]); cały wiersz ≥ 56 dp to jeden cel dotyku. Zaznaczone pole: wypełnione akcentem z `check` w kolorze tła; puste: obrys w tekście pomocniczym | lista z polami wyboru | dotknięcie wiersza przełącza | zaznaczone osoby, które mają łącze do tego zdjęcia | — | ISSUE-017 AC 5 · [[style-b]] *Thresholds* (SC 1.4.1) |
| D5 | **Sekcja „Inne osoby”** (nagłówek jak D4) — wszystkie pozostałe osoby w aplikacji, alfabetycznie po nazwisku, potem imionach (`polishCompare`). Druga linia: lata życia · nazwa grobu, a bez niej nazwa cmentarza (jedna linia, ucięta) — odróżnia dwie osoby o tym samym imieniu i nazwisku; osoba bez pochówku — same lata. Wiersz jak D4 | lista z polami wyboru | jak D4 | jak D4 | — | ISSUE-017 AC 5 i AC „także później” · **D7 — przyjęte na stopie #1** |
| D6 | **„Gotowe”** — przycisk wypełniony (akcent), przypięty na dole, ≥ 52 dp, na pełną szerokość z marginesami 16 dp | przycisk | → B; linia B5 pokazuje nowy skład | — | — | [[style-b]] reguła 1 |

**Pusty wynik filtra:** w miejscu sekcji „Nie ma osoby pasującej do „…”.” (14 sp, tekst pomocniczy). **Nowa osoba**
(formularz w trybie „nowy grób”): sekcja D4 ma tylko tę osobę.

**Dane, których potrzebuje D** (dla `planning`):
- wszystkie osoby: imiona, nazwisko, nazwisko rodowe, lata;
- grób albo cmentarz pierwszego pochówku każdej osoby — pierwsza wartość według [[ADR-006-claimed-value-separate-structures]] D3;
- łącza tego zdjęcia.

Zaznaczenie osoby dodaje łącze **na końcu** jej kolejności. Gdy osoba nie miała zdjęć, to zdjęcie zostaje jej
profilowym. Odznaczenie usuwa łącze tej osoby, a gdy to było jej profilowe, profilowym zostaje jej następne zdjęcie.
Wszystko zapisuje się z „Zapisz” formularza ([[zdjecia-osoby]] D1).

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
| C — nieudane usunięcie | w oknie pod treścią: `error_outline` + „Nie udało się usunąć zdjęcia. Spróbuj jeszcze raz.” (kolor błędu); okno zostaje. **W trybie osoby nie występuje** — usunięcie łącza zapisuje się z „Zapisz” formularza, a jego błąd pokazuje formularz („nieudany zapis”) |
| B — tryb osoby, jedno zdjęcie | B1, B2, B5, B4' — bez B3 |
| B — tryb osoby, profilowe | v1.4: podtytuł B1 „Zdjęcie profilowe”; w B4' zamiast „Ustaw jako profilowe” przycisk „Popraw kadr” ([[kadr-profilowego]] D8). Do v1.3: stan „✓ Profilowe” (tekst pomocniczy) |
| B — tryb osoby, zdjęcie dopiero wybrane | jak wypełniony: plik przygotowany w katalogu roboczym, jeszcze nie w magazynie aplikacji ([[ADR-008-photos-access-copy-and-backup-consistency]]); dla autora bez różnicy |
| D — otwarte | D1–D6, klawiatura schowana; zaznaczone osoby, które mają łącze do zdjęcia |
| D — filtr | sekcje pokazują tylko pasujące wiersze; nagłówek sekcji bez pasujących wierszy znika; zaznaczenia ukrytych wierszy zostają |

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

**Tryb osoby (v1.3):**
```
 B — podgląd (osoba)                  D — kto jest na zdjęciu?
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│ ←  Anna Wymyślona                │  │ ←  Kto jest na zdjęciu?          │
│    Zdjęcie osoby                 │  │        ┌──────────────┐          │
│   ┌──────────────────────────┐   │  │        │ [zdjęcie w   │  160 dp  │
│   │                          │   │  │        │  całości]    │          │
│   │   [zdjęcie w całości,    │   │  │        └──────────────┘          │
│   │    bez przycinania]      │   │  │ ┌ 🔍 Szukaj osoby ─────────────┐ │
│   │                          │   │  │ └──────────────────────────────┘ │
│   └──────────────────────────┘   │  │  W tym grobie                    │
│  Na zdjęciu: Anna Wymyślona,     │  │  ☑ Anna Wymyślona  (nieaktywne)  │
│  Jan Wymyślony          Zmień    │  │    ta osoba                      │
│        ‹     2 z 3     ›         │  │  ☑ Jan Wymyślony                 │
│                                  │  │    ok. 1890 – 14.03.1951         │
│ ◉ Ustaw jako profilowe           │  │  Inne osoby                      │
│ 🗑 Usuń z tej osoby               │  │  ☐ Józef Wymyślony               │
└──────────────────────────────────┘  │    po 1920 – 1944 · Grób rodz…   │
                                      │  ☐ Maria Zmyślona                │
                                      │    1901–1979 · Cmentarz Testowy  │
                                      │ ┌──────────────────────────────┐ │
                                      │ │            Gotowe            │ │
                                      │ └──────────────────────────────┘ │
                                      └──────────────────────────────────┘
```

## Tempo
Rekordem jest **zdjęcie nagrobka**: ok. 50 grobów (G6, [[NT-002-transcribe-the-notes]]).
- **Z galerii:** pole „Dodaj zdjęcie nagrobka” → „Wybierz z galerii” → zdjęcie → „Gotowe” w systemowym oknie = **4 dotknięcia**
  (v1.2: zmierzone na Androidzie 16 — okno wymaga potwierdzenia także przy jednym zdjęciu, poza kontrolą
  aplikacji; na Androidzie 13–15 Photo Picker może wracać od razu, wtedy 3).
- **Aparatem:** „Dodaj zdjęcie” → „Zrób zdjęcie” → spust → zatwierdzenie w aplikacji aparatu = 4 dotknięcia.
- Na całość: ok. 50 × 4 = **ok. 200 dotknięć**.
- **Zmiana:** zdjęcie → „Zmień zdjęcie” → „Wybierz z galerii” → zdjęcie → „Gotowe” = 5 dotknięć.

**Tryb osoby (v1.3)** — rachunek na całą bazę: [[zdjecia-osoby]] → *Tempo*. Tutaj:
- **profilowe:** „Ustaw jako profilowe” = 1 dotknięcie w podglądzie; **v1.4:** + „Gotowe” w [[kadr-profilowego]] = 2 i gesty kadru;
- **osoba na zdjęciu z tego samego grobu:** „Zmień” → wiersz → „Gotowe” = 3 dotknięcia; z innego grobu — plus
  przewinięcie albo kilka liter w D3;
- **usunięcie z osoby:** „Usuń z tej osoby” → „Usuń” = 2.

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
- **Tryb osoby (v1.3):**
  - B3 i B5 stoją pod zdjęciem, nie na nim (reguła 14);
  - „Ustaw jako profilowe” w akcencie jako główne działanie podglądu, a „Usuń z tej osoby” w kolorze tekstu
    (reguła 1);
  - stan „Profilowe” ma ikonę `check` i tekst, a nie sam kolor (SC 1.4.1);
  - w D jedyny wypełniony przycisk to „Gotowe” (reguła 1);
  - pole wyboru zaznaczone niesie akcent i znak `check`, więc kolor nie jest jedynym nośnikiem (SC 1.4.1). Puste pole
    ma obrys w tekście pomocniczym (5,50:1 na tle, SC 1.4.11 ✅). Nieaktywne pole „ta osoba” jest zwolnione z SC
    1.4.11 (*inactive user interface components*), a stan niesie druga linia „ta osoba”.
- **Tokeny:** bez nowych.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-005 AC-1 (grób) | A2, A3 → [[grob]] 1a | zdjęcie wybrane z galerii albo zrobione aparatem pojawia się nad tytułem grobu |
| US-005 AC-2 | B2 | podgląd otwiera zdjęcie z magazynu aplikacji; po usunięciu oryginału z galerii dalej się otwiera |
| US-005 AC-3 | B2 | po odtworzeniu z kopii podgląd otwiera to samo zdjęcie (odcisk danych — `qa`) |
| ISSUE-016: zmiana i usunięcie (decyzja autora) | B4, C | „Zmień zdjęcie” → nowe zdjęcie; „Usuń zdjęcie” → okno → zdjęcia nie ma |
| ISSUE-016: styl B | całość | reguły wyżej; przegląd `ui` przed stopem #2 |
| US-005 AC-1 (osoba, v1.3) | A (tryb osoby) → [[zdjecia-osoby]] | zdjęcia z galerii (kilka) albo aparatu pojawiają się w bazie osoby |
| ISSUE-017: jedno zdjęcie profilowe | B4' | „Ustaw jako profilowe” → (v1.4: [[kadr-profilowego]] → „Gotowe”) → podtytuł „Zdjęcie profilowe”; profilowe w [[zdjecia-osoby]], [[wpis-osoby]] 1a i karcie w [[grob]] |
| ISSUE-018: kadr profilowego, poprawa kadru (v1.4) | B4' → [[kadr-profilowego]] | „Ustaw jako profilowe” i „Popraw kadr” otwierają kadr; po „Gotowe” okręgi profilowego pokazują wycinek |
| ISSUE-017: zdjęcie u kilku osób, jeden plik | B5 → D | zaznaczona osoba ma to zdjęcie w swojej bazie; plik w magazynie jeden |
| ISSUE-017: usunięcie u jednej osoby nie usuwa innym | B4' → C1' | treść okna mówi, u kogo zdjęcie zostaje; po zapisie zdjęcie jest dalej w bazie tamtej osoby |

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
- **D7 — kogo da się zaznaczyć na zdjęciu: wszystkie osoby, a ten grób na górze (v1.3; przyjęte przez autora na stopie
  #1 ISSUE-017: *„na 4-osobowym zdjęciu zaznaczę tylko dwie osoby, które znam, ale w przyszłości wrócę do tego zdjęcia
  i zaznaczę kolejną”* — nowo poznany krewny leży zwykle w innym grobie).** Główny przypadek zdjęcia dzielonego to zdjęcie grupowe z
  albumu u babci (brief §2 *Value & Scope*: *„capturing from grandmother (sitting with her, adding facts, photographing old
  photos, recording who-is-who)”*). Rodzice i dzieci leżą zwykle w
  różnych grobach, a osoby żyjące (z [[US-003-przepisanie-rodziny]]) w żadnym. Wybór tylko z tego grobu
  ([[ISSUE-017-person-photos]] → *Out of Scope*) obsłużyłby małżonków, a przy reszcie wymuszał drugi plik tego samego
  zdjęcia, czyli to, czego AC zabrania. **Koszt:** lista ok. 100 osób z polem filtra. Filtr to istniejące
  `matchesQuery` i `polishCompare` z wyszukiwarki cmentarzy, działa tylko w tym oknie i **nie jest wyszukiwaniem S5**
  (bez cmentarzy, bez wejścia z mapy). **Wariant tańszy:** sama sekcja D4 bez D3 i D5. Zdjęcie osoby z innego grobu
  dodaje się wtedy u niej osobno, jako drugi plik. *Obali:* autor na stopie #1 woli wariant tańszy albo przy
  pierwszych zdjęciach grupowych okazuje się, że osoby z innych grobów nie trafiają się na tych samych zdjęciach.
- **D8 — kolejność kilku nowych zdjęć: tak, jak zwróci je okno systemowe; pierwsze zostaje profilowym, jeśli osoba
  nie miała zdjęć.** Czy Photo Picker zwraca zdjęcia w kolejności zaznaczania — **nie sprawdzone** (falsyfikator dla
  `dev` na emulatorze). Gdy nie, profilowym zostaje „przypadkowe” z wybranych. Koszt poprawki: 2 dotknięcia
  („Ustaw jako profilowe”).
- **D9 — profilowe jest osobne dla każdej osoby.** To łącze, nie zdjęcie, ma kolejność. To samo zdjęcie ślubne może być
  profilowym żony i zwykłym zdjęciem męża (GEDCOM 7: kolejność `OBJE` w strukturze każdej osoby). „Ustaw jako
  profilowe” zmienia tylko osobę z paska B1.

## Open
brak. Usuwanie i zmiana zdjęcia nagrobka rozstrzygnięte na stopie #1 ISSUE-016 (wchodzą). Zdjęcia osób — tryb osoby
v1.3 i [[zdjecia-osoby]]. **Na stopie #1 ISSUE-017:** D7 (kogo da się zaznaczyć na zdjęciu) — rekomendacja w
*Decisions*, nie luka — **przyjęte na stopie #1** (wszystkie osoby z filtrem).
