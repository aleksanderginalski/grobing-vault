---
screen: "Ustawienia — ja, kopia, eksport dla rodziny, notka przekazania, stan danych"
items: ["[[SPIKE-004-mvp-flow-prototype]]", "[[ISSUE-022-app-skeleton-tabs-people-settings]]"]
us: "[[US-006-eksport-dla-rodziny]] (eksport) · [[US-001-kopia-z-odtworzeniem]] (kopia, zbudowana) · ustawienie „ja” (M5, [[data-model]])"
journey-step: "n/a — M8 (przeżywa telefon i aplikację)"
mockup: "2026-10-08: grobing-prototyp.html (SPIKE-004, panel 9) — katalog tymczasowy sesji, ścieżka w SPIKE-004"
updated: 2026-10-08
---

# Ustawienia — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.17) · referencja: [[references]] → R1 (koło zębate).
>
> **Wersja 1 — discovery na prototypie, panel 9 ([[SPIKE-004-mvp-flow-prototype]] D23, 2026-10-08).** Autor: *„7. ok”*.
> Dziś koło zębate otwiera od razu „Stan danych” (ekran techniczny z ISSUE-007…010). Ustawienia stają przed nim jako
> lista, a „Stan danych” schodzi o poziom niżej. Ekran eksportu jest tu, bo prowadzi do niego tylko ta lista.
>
> **Wersja 2 — zbudowane w [[ISSUE-022-app-skeleton-tabs-people-settings]] (elementy 1–7), przegląd `ui` (2026-10-08).**
> Decyzje ze stopu #1 (D1 = A, D3, D4) i odstępstwa `dev` przyjęte albo poprawione w przeglądzie (*Dev report →
> Deviations* 1, 3–6, 8):
> - **„Odtwórz z kopii” otwiera od razu ekran odtworzenia**, a nie „Stan danych” (D4 → element 4, *Navigation*);
> - „Ja”: profilowe 40 dp albo „Ja”, imię i nazwisko wybranej osoby, a przed wyborem zaproszenie (D7 → element 1);
> - kopia: format czasu, miejsce od dostawcy pliku, stany „nieudana” i „w toku” (D5, D6 → elementy 2–3, *States*);
> - **ekran notki przekazania** (element 6a, D8); zaślepka eksportu do US-006 (element 5);
> - „Stan danych” z ikoną `storage_outlined`; osobna sekcja „O aplikacji” (element 7, D9);
> - margines boczny 16 dp, pole ikony 40 dp.

## Purpose
Jedno miejsce na to, co nie jest rodziną ani mapą: **kim jestem w drzewie** („ja”), **czy kopia działa**, **eksport i
notka dla rodziny** (M8: przeżywa telefon i aplikację) i dane techniczne.

## Navigation
- **Koło zębate na ekranie głównym** ([[cmentarze]] element 1) → ta lista. Bez dolnego paska — to nie jest zakładka
  ([[style-b]] reguła 12); ekrany pod nią (wybór „ja”, notka, eksport, odtworzenie, „Stan danych”) też go nie mają.
- „Ja” → **wybór „ja”** — „Która osoba to Ty?” ([[osoby]] elementy 6–7); wybór zapisuje i wraca tu.
- **„Odtwórz z kopii” → ekran odtworzenia wprost** (ten sam, co z „Stanu danych”, US-001; D4).
- „Stan danych” → dzisiejszy ekran „Stan danych” (bez zmian; tam też jest „Odtwórz z kopii”).
- „Kopia nie jest skonfigurowana” → „Skonfiguruj kopię” → dzisiejsza konfiguracja kopii.
- „Eksport dla rodziny” → ekran eksportu (elementy 8–11); **do [[US-006-eksport-dla-rodziny]] — zaślepka** (element 5).
- „Notka przekazania” → ekran notki (element 6a).
- Wstecz → ekran główny.

## Elements in order
**Lista ustawień** — sekcje z nagłówkiem (13 sp, tekst pomocniczy), wiersze ≥ 56 dp z linią podziału w kolorze obrysu,
**margines boczny 16 dp**, ikona z lewej w polu 40 dp (akcent — działanie; tekst pomocniczy — informacja), tytuł 16 sp
półgruby, opis 13 sp tekst pomocniczy, chevron, gdy prowadzi dalej. Wiersz z działaniem jest dla czytnika jednym
elementem (tytuł + opis).

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Ty w drzewie — „Ja”**. **Przed wyborem:** inicjały „Ja” w akcencie (40 dp), opis „Wybierz, która osoba to Ty”, a pod nim „Od tej osoby liczą się łańcuchy i nazwy pokrewieństwa”. **Po wyborze:** profilowe tej osoby (okrąg 40 dp, w kadrze łącza), a bez zdjęcia „Ja”; opis — imię i nazwisko („Ewa Wymyślona”), a pod nim to samo zdanie. Chevron | wiersz | → wybór „ja” ([[osoby]] 6–7) — także żeby zmienić osobę | brak — pierwszy start prosi o wybór przy pierwszym łańcuchu (poza ISSUE-022) | — | M5 · [[data-model]] („ja”) · ISSUE-022 D3, odstępstwo 1 · D7 |
| 2 | **Kopia — „Ostatnia udana kopia”**: `cloud_done_outlined` w zieleni stanu (`stateOk`), opis: **kiedy** („dziś, 11:42”, „wczoraj, 18:05”, „03.10.2026, 09:30” — czas telefonu), „ (w tle)”, gdy kopię zrobiło tło, i **gdzie** po „ · ”: „Dysk Google”, „Pobrane” albo „pamięć telefonu” — z dostawcy pliku wybranego w oknie zapisu; **nieznany dostawca → bez miejsca**. Kopii jeszcze nie było → `cloud_queue` (tekst pomocniczy), opis „jeszcze nie było”. Zmianę wiersza czytnik ogłasza sam | wiersz (informacja) | — | — | — | US-001 (zbudowane: „Stan danych”) · ISSUE-022 odstępstwa 3, 8 · D5 |
| 3 | **„Zrób kopię teraz”** (`backup_outlined`, akcent), bez chevronu. W trakcie: wskaźnik postępu zamiast ikony, „Robię kopię…”, wiersz nieaktywny; czytnik ogłasza zmianę | wiersz | zrób kopię | — | błąd → pasek komunikatu z treścią błędu; wiersz 2 pokazuje stan „nieudana” | US-001 · ISSUE-022 odstępstwo 4 · D6 |
| 4 | **„Odtwórz z kopii”** (`settings_backup_restore`, akcent) — „Nowy telefon albo utracone dane”, chevron. Podczas kopii nieaktywny i przygaszony (tytuł w kolorze tekstu pomocniczego) | wiersz | → **ekran odtworzenia wprost** (D4) | — | — | US-001 · [[NFR-002-odtworzenie-na-nowym-telefonie]] · przegląd `ui` |
| 5 | **Dla rodziny — „Eksport dla rodziny”** (`ios_share`, akcent) — „HTML i PDF — otworzą się bez Grobing”, chevron | wiersz | → eksport (8–11); **do US-006 zaślepka**: pasek wstecz + „Eksport dla rodziny” i tekst pomocniczy na środku „Eksport powstanie z US-006: jeden plik HTML i jeden PDF, które otworzą się bez Grobing.” | — | — | [[US-006-eksport-dla-rodziny]] · ISSUE-022 D1 = A |
| 6 | **„Notka przekazania”** (`description_outlined`, akcent) — „Gdzie jest kopia i jak ją otworzyć — na papierze, u rodziny”, chevron | wiersz | → ekran notki (6a); sama notka jest poza aplikacją | — | — | M8 · G2 · NT-007 |
| 7 | **Techniczne — „Stan danych”** (`storage_outlined`, tekst pomocniczy — w Material Icons Fluttera nie ma `database`) — „Wersja bazy, odcisk danych, liczby”, chevron; podczas kopii nieaktywny i przygaszony. **Sekcja „O aplikacji”**: `info_outline`, tytuł „Grobing <wersja>” (wersja z `pubspec.yaml`), opis „Mapy: © autorzy OpenStreetMap (ODbL) · Natural Earth”; „ · Ortofotomapa: GUGiK” dochodzi z [[US-007-mapa-cmentarza]]. Bez działania i bez chevronu | wiersze | „Stan danych” → dzisiejszy ekran | — | — | ISSUE-007 · licencje (ODbL) · ISSUE-022 odstępstwa 6, 9 · D9 |

**Notka przekazania** ([[ISSUE-022-app-skeleton-tabs-people-settings]] D4, [[NT-007-hand-over-note]]; bez paska dolnego)

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 6a | Pasek wstecz + „Notka przekazania”. **Wstęp** (16 sp, tekst): „Kartka u rodziny — poza telefonem i poza chmurą. Bez niej rodzina nie otworzy kopii. Na kartce:”. **Lista 1–5** (numery w kolorze tekstu pomocniczego, treść 16 sp, tekst): (1) że kopia istnieje — Grobing robi ją sam, kilka minut po zmianach; (2) gdzie leży kopia: folder i nazwy obu plików — kopii (np. `grobing-kopia.age`) i klucza (np. `grobing-klucz.age`); (3) hasło do pliku klucza — nigdy w tej samej chmurze co kopia; zgubione hasło albo plik klucza to utracona kopia; (4) jak otworzyć kopię bez Grobing: program `age` odszyfrowuje plik, w środku jest archiwum `tar` z bazą SQLite i zdjęciami; (5) gdzie leży eksport dla rodziny — otworzy się w zwykłej przeglądarce. **Przypis** (14 sp, tekst pomocniczy): „„Skonfiguruj kopię od nowa” tworzy nowy klucz — wtedy notkę trzeba wymienić. Zmiana telefonu jej nie zmienia.” Margines boczny 16 dp | tekst | — | — | — | ISSUE-022 D4 · NT-007 · D8 |

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
| „ja” niewybrane | 1 z „Ja” i opisem „Wybierz, która osoba to Ty” |
| kopia nieskonfigurowana | 2: `cloud_off_outlined` (tekst pomocniczy) „Kopia nie jest skonfigurowana”, opis „Do jej otwarcia będą potrzebne: plik kopii, plik klucza i hasło” + 3 jako „Skonfiguruj kopię” (`backup_outlined`, akcent, chevron) |
| kopii jeszcze nie było | 2: `cloud_queue` (tekst pomocniczy), „Ostatnia udana kopia” — „jeszcze nie było” |
| ostatnia kopia nieudana | 2: `sync_problem` w kolorze błędu, „Ostatnia kopia się nie udała”, opis „<kiedy> — <komunikat>” i w drugiej linii „Ostatnia udana: <kiedy · gdzie albo „jeszcze nie było”>”; 3 bez zmian (ponowienie) |
| kopia w toku | 3: wskaźnik postępu, „Robię kopię…”; 4 i 7 nieaktywne i przygaszone |
| błąd odczytu ustawień kopii | 2: `error_outline` w kolorze błędu, „Nie udało się odczytać ustawień kopii” |
| notka | 6a |
| eksport przed US-006 | zaślepka z elementu 5 |
| eksport | 8–11 |
| eksport w toku | 11: wskaźnik postępu w przycisku, przycisk nieaktywny |
| eksport gotowy | ciche potwierdzenie (reguła 10): „Zapisano: grobing-eksport-2026-10-08.html i .pdf” pod przyciskiem |

## Sketch
```
┌──────────────────────────────────┐   ┌──────────────────────────────────┐
│ ←  Ustawienia                    │   │ ←  Eksport dla rodziny           │
│ Ty w drzewie                     │   │ Czytelna kopia dla rodziny: HTML │
│ (◉) Ja                         › │   │ i PDF z osobami, rodzinami, …    │
│     Ewa Wymyślona                │   │ ▣ Zdjęcia                  [●━]  │
│     Od tej osoby liczą się …     │   │ ◯ Osoby żyjące             [━○]  │
│ Kopia                            │   │ Plik zapiszesz tam, gdzie …      │
│ ☁✓ Ostatnia udana kopia          │   │ ╭──────────────────────────────╮ │
│    dziś, 11:42 (w tle) · Dysk G… │   │ │      ⇪  Utwórz eksport       │ │
│ ⤒  Zrób kopię teraz              │   │ ╰──────────────────────────────╯ │
│ ↺  Odtwórz z kopii             › │   └──────────────────────────────────┘
│ Dla rodziny                      │   ┌──────────────────────────────────┐
│ ⇪  Eksport dla rodziny         › │   │ ←  Notka przekazania             │
│ ▤  Notka przekazania           › │   │ Kartka u rodziny — poza telefo-  │
│ Techniczne                       │   │ nem i poza chmurą. Bez niej …    │
│ ⛁  Stan danych                 › │   │ 1. Że kopia istnieje. …          │
│ O aplikacji                      │   │ 2. Gdzie leży kopia: folder …    │
│ ⓘ  Grobing 1.0.0                 │   │ …                                │
│    Mapy: © autorzy OpenStreet…   │   │ „Skonfiguruj kopię od nowa” …    │
└──────────────────────────────────┘   └──────────────────────────────────┘
```

## Tempo
n/a — ekran ustawień.

## Style B rules applied
- **Reguła 12:** bez dolnego paska — ustawienia są pod kołem zębatym, nie zakładką; ekrany pod nimi też bez paska.
- **Reguła 1:** jeden wypełniony przycisk („Utwórz eksport”); wiersze bez wypełnienia.
- **Reguła 3 i kolory stanu:** ikony działań w akcencie, informacji w tekście pomocniczym. Stan kopii w zieleni stanu
  (`stateOk`, 8,97:1 na tle — wiersz stoi na tle) i błąd (6,45:1) — zawsze z ikoną i tekstem, nigdy sam kolor.
- **Role tokenów:** numery listy w notce w kolorze tekstu pomocniczego — akcent nie jest ozdobnikiem.
- **Reguła 5:** margines boczny 16 dp w liście i w notce.
- **Reguła 7:** ton notki spokojny i rzeczowy: „Bez niej rodzina nie otworzy kopii.”
- **Reguła 10:** eksport kończy się cichym potwierdzeniem, nie oknem; wybór „ja” — widokiem wybranej osoby w wierszu 1.
- **Reguła 14:** profilowe w wierszu 1 — okrąg 40 dp, ten sam rozmiar co miniatura osoby w karcie.
- **Tokeny:** `stateOk` wpisany do `theme.dart` w ISSUE-022 ([[style-b]] v1.17 → *State colours*); przełącznik — akcent
  (włączony) i obrys (wyłączony): istniejące pary.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-006 AC-1 — HTML i PDF bez aplikacji | 8, 11 | opis i przycisk; zapis dwóch plików |
| US-006 AC-3 — eksport nie idzie do chmury sam | 11 | systemowe okno zapisu; podpis „Grobing nigdzie go nie wysyła” |
| M8 / G2 — rodzina wie, że kopia istnieje | 6, 6a | wiersz notki przekazania i ekran z listą tego, co ma być na kartce |
| (ISSUE-022) AC-3 — koło zębate → ustawienia; „Stan danych” otwiera dzisiejszy ekran | lista · 7 | koło → „Ustawienia”; „Stan danych” → ekran z wersją schematu i odciskiem |
| (ISSUE-022) AC-4 — wybór „ja” zapisany i na górze Osób | 1 · [[osoby]] 3, 6–7 | „Ja” → „Która osoba to Ty?” → Ewa → w wierszu jej profilowe i „Ewa Wymyślona”; w Osobach pod „Ja” |
| (ISSUE-022) D4 — notka z listą tego, co ma być na kartce | 6a | sześć rzeczy z D4: pięć punktów i przypis o nowym kluczu |

## Decisions
- **D1 — koło zębate → lista ustawień, „Stan danych” niżej** (D23). Kopia, eksport i „ja” to sprawy użytkownika, a
  „Stan danych” to diagnostyka. *Obali:* autor używa „Stanu danych” codziennie — wtedy wiersz na górze.
- **D2 — eksport domyślnie bez osób żyjących** (D23: *„7. ok”* na pytanie wprost). Eksport ma trafić do rodziny i może
  pójść dalej; dane żyjących chroni brief §6 N3. *Obali:* rodzina chce kompletnego drzewa z żyjącymi — przełącznik już
  jest.
- **D3 — notka przekazania jako opis, nie generator** — notka to kartka u rodziny (NT-007), poza aplikacją; aplikacja
  przypomina, co ma w niej być.
- **D4 — „Odtwórz z kopii” otwiera odtworzenie wprost** (v2; przegląd `ui` ISSUE-022, odstępstwo 5; zmienia
  *Navigation* v1). W v1 wiersz prowadził do „Stanu danych”, gdzie trzeba było znaleźć drugi raz „Odtwórz z kopii” —
  poniżej krawędzi ekranu, pod „Skonfiguruj kopię od nowa” w tej samej formie przycisku tekstowego. To najrzadsza i
  najważniejsza droga (nowy telefon, często ktoś z rodziny, NFR-002), więc nie może prowadzić przez ekran diagnostyczny.
  Przycisk w „Stanie danych” zostaje. *Obali:* ktoś trafia w odtworzenie, chcąc tylko zobaczyć stan kopii — wtedy
  ekran odtworzenia zaczyna się od opisu tego, co zastąpi (już tak jest: ostrzeżenie przy danych w telefonie, ISSUE-009 D4).
- **D5 — miejsce kopii od dostawcy pliku, bez zgadywania** (v2; ISSUE-022 odstępstwo 3). Przykład z v1 („· Dysk Google”)
  zakładał jedną chmurę. Miejsce bierze się z dostawcy pliku wybranego w oknie zapisu; nieznany dostawca nie dostaje
  nazwy, bo zła nazwa jest gorsza niż żadna. Rozpoznanie Dysku Google trzeba potwierdzić na telefonie. *Obali:* u autora
  dostawca zawsze jest nieznany — wtedy nazwa folderu z okna zapisu.
- **D6 — stany kopii nieudanej i w toku** (v2; ISSUE-022 odstępstwo 4, przegląd `ui`). Nieudana kopia to ryzyko utraty
  danych, więc ma kolor błędu — zawsze z ikoną `sync_problem` i tekstem, z datą ostatniej udanej; ponowieniem jest
  „Zrób kopię teraz” tuż pod spodem. W trakcie kopii wiersze, które otwierają odtworzenie albo „Stan danych”, są
  nieaktywne i **wyglądają na nieaktywne** (przygaszony tytuł). Zmiany stanu kopii czytnik ogłasza sam (WCAG 2.2
  SC 4.1.3). *Obali:* kopia w toku trwa tak krótko, że przygaszenie miga — wtedy wiersze zostają aktywne, a ekran
  odtworzenia czeka na koniec kopii.
- **D7 — „Ja” w wierszu: profilowe, imię i nazwisko, a przed wyborem zaproszenie** (v2; ISSUE-022 D3, odstępstwo 1,
  przegląd `ui`). Bez nazwy wybranej osoby nigdzie nie widać, kogo wybrano. W wierszu ustawień jest profilowe, a w
  zakładce Osoby znak „Ja” ([[osoby]] D4) — tu wiersz mówi „kto”, tam karta jest kotwicą listy. *Obali:* autor myli
  się, bo w dwóch miejscach są różne znaki — wtedy jeden znak w obu.
- **D8 — notka: lista i spokojny ton** (v2; ISSUE-022 D4, przegląd `ui`). Treść ogólna, bez danych: aplikacja nie zna
  hasła ani miejsca kartki i nigdy nie pokazuje klucza. Wstęp mówi, po co jest kartka („Bez niej rodzina nie otworzy
  kopii.”), a nie straszy (reguła 7). *Obali:* rodzina nie umie otworzyć kopii z tej listy — wtedy krok po kroku w
  [[NT-007-hand-over-note]], a tu link do niego.
- **D9 — „O aplikacji” jako osobna sekcja; czas ludzki tu, techniczny w „Stanie danych”** (v2; ISSUE-022 odstępstwa 6, 8).
  Wersja i podpisy danych to nie diagnostyka, więc mają własny nagłówek. „Stan danych” zostaje techniczny
  (`2026-10-08 11:42`). **Znana rozbieżność, poza zakresem ISSUE-022:** „Stan danych” mówi „Zapisana w Dysku na
  telefonie…”, także gdy kopia leży w „Pobranych” — poprawka przy następnej zmianie tamtego ekranu (to samo
  rozpoznanie miejsca co w elemencie 2).

## Open
brak.
