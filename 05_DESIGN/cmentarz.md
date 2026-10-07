---
screen: "Cmentarz — groby na cmentarzu"
items: ["[[ISSUE-012-transcribe-grave-screen]]", "[[ISSUE-016-photos-grave-and-person]]"]
us: "[[US-002-przepisanie-grobu]] · [[US-005-zdjecia]]"
journey-step: "n/a — M1 (warunek kroku 1 UJ-001); docelowo mapa cmentarza z arkuszem grobu (R2, krok 2 UJ-001, M3)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-cmentarz-grob-osoba.html (ramki 1–2, 8, ISSUE-012) · makieta-zdjecia.html (ramka 9, ISSUE-016)"
updated: 2026-10-07
---

# Cmentarz — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.8) · referencja: [[references]] → **R2**.
>
> **Wersja 2 (2026-10-07, przed planem ISSUE-012)** — przebudowa według decyzji autora z 2026-10-06
> ([[ISSUE-012-transcribe-grave-screen]] → *Input from the author*): **cmentarz jak R2, ale bez zdjęcia
> satelitarnego — arkusz z grobami, z pinezką i bez.** Wersja 1 była listą kart z „Grób nazwany osobami”;
> zmiany: układ R2 (nagłówek, arkusz grobów), **nazwa grobu** jako tytuł karty, wejście z „Otwórz cmentarz”
> ([[cmentarze]] element 7), kierunek po [[SPIKE-001-map-source-offline]] (D1).
>
> **Wersja 2.1 — przegląd `ui` zbudowanego ekranu (2026-10-07):** lista kończy się nad przypiętym „Dodaj grób”
> (zamiast przewijać się pod nim — skutek ten sam: ostatnia karta jest cała widoczna). Osoba bez imion i nazwiska
> (tylko z innych danych): „Osoba bez imienia”. Reszta zgodna ze zbudowanym ekranem.
>
> **Wersja 3 (2026-10-07, przed planem [[ISSUE-016-photos-grave-and-person]]):** karta grobu ze zdjęciem ma z
> lewej **miniaturę zdjęcia nagrobka** (element 3 (d)) — „miejsce na zdjęcie” z arkusza grobu, którego chciał
> autor (ISSUE-012 → *Input from the author* 2), i miniatura nagrobka z R2. Grób bez zdjęcia — karta bez zmian.

## Purpose
Groby przepisane na jednym cmentarzu i wejście do dodania kolejnego grobu z notatek. Każda karta grobu niesie
treść arkusza grobu z R2 — nazwę, adres, kto tam leży — i mówi, czy grób ma adres kwatery i pinezkę
(US-002 AC-5). Przy przepisywaniu to też miejsce, w którym widać, dokąd się doszło w notatkach.

## Navigation
- **Z [[cmentarze]]:** arkusz cmentarza → **„Otwórz cmentarz”** (element 7, przeniesiony z ISSUE-014, D5).
  Także dla cmentarza bez grobów i bez punktu na mapie.
- **Dotknięcie karty grobu → [[grob]].**
- **„Dodaj grób” → [[wpis-osoby]] w trybie „nowy grób”:** grób powstaje razem z pierwszą osobą, przy jej
  zapisie. Pustych grobów z interfejsu nie ma.
- **Wstecz → [[cmentarze]]** z tym samym cmentarzem wybranym i jego arkuszem (liczby w arkuszu już nowe).

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** wstecz + **nazwa cmentarza** (20 sp, półgruby, do 2 linii), pod nią miejscowość (14 sp, tekst pomocniczy; bez miejscowości — brak linii) | pasek | wstecz → [[cmentarze]] | — | — | R2 (nagłówek) |
| 2 | **Podsumowanie:** „3 groby · 6 osób” (14 sp, tekst pomocniczy), margines 16 dp | tekst | — | — | — | decyzja projektowa (postęp przepisywania, NT-002) · [[cmentarze]] D13 (ta sama liczba osób co w arkuszu) |
| 3 | **Arkusz grobów** — karty na powierzchni (promień 16 dp, odstęp 8 dp, margines 16 dp) w kolejności wpisania. Karta, od góry: **(a) tytuł** — nazwa grobu (16 sp, półgruby, kolor tekstu, do 2 linii); bez nazwy tytułem są **osoby w grobie**: imiona i nazwiska po przecinku, ten sam krój, do 2 linii, potem „i jeszcze 2”. **(b) osoby** — tylko gdy tytułem jest nazwa: imiona i nazwiska po przecinku (14 sp, tekst pomocniczy, do 2 linii, potem „i jeszcze 2”). **(c) adres** (14 sp, tekst pomocniczy): „Kwatera B · Rząd 4 · Miejsce 12”, a bez pinezki dopisane „· bez pinezki”; bez adresu „Bez adresu kwatery · bez pinezki”. Chevron „›” po prawej. Karta ≥ 64 dp. **(d) miniatura (v3)** — tylko gdy grób ma zdjęcie: zdjęcie nagrobka (jedno — [[grob]] D9), kwadrat **56 dp** z zaokrągleniem 8 dp, przycięty ze środka, z lewej, wyśrodkowany w pionie, odstęp 12 dp do tekstu; poza czytnikiem (kartę opisuje tekst). Bez zdjęcia: bez miniatury i bez wcięcia ([[grob]] D11) | lista kart | dotknięcie → [[grob]] | kolejność wpisania | — | AC-1 · AC-5 · R2 (arkusz grobu) · decyzja autora (nazwa grobu) · US-005 AC-1 · uwaga autora 2 (ISSUE-012) |
| 4 | **„Dodaj grób”** — przycisk wypełniony (główne działanie), ≥ 52 dp, **przypięty na dole**, pełna szerokość minus marginesy, nad paskiem gestów; lista przewija się pod nim, a ostatnia karta ma pod sobą odstęp na wysokość przycisku | przycisk główny | dotknięcie → [[wpis-osoby]] „nowy grób” | — | — | *What to build* 2 |

Imię i nazwisko w liście osób: „Imiona Nazwisko” bez nazwiska rodowego — „z d.” jest w [[grob]]. Osoba bez
imion albo bez nazwiska: to, co jest. Spór źródeł o grób ([[ADR-006-claimed-value-separate-structures]] D2):
osoba z dwoma pochówkami stoi w obu grobach, jak w [[grob]].

## States
| Stan | Co widać |
|---|---|
| pusty | pasek (1), w środku „Na tym cmentarzu nie ma jeszcze grobów.” (16 sp, tekst pomocniczy), pod spodem „Dodaj grób” (4). Bez podsumowania (2) |
| wypełniony | 1–4 |
| błąd | „Nie udało się odczytać grobów.” (tekst pomocniczy) + „Spróbuj ponownie” (przycisk z obrysem); „Dodaj grób” nieaktywny, bo nie wiadomo, do czego dodaje |
| wczytywanie | wskaźnik postępu w środku (lokalna baza — zwykle niewidoczny) |
| grób bez osób | może przyjść z innych danych (z interfejsu nie powstaje): tytuł karty „Grób bez wpisanych osób” w kolorze pomocniczym |
| brak pliku zdjęcia (v3) | wpis zdjęcia jest, pliku nie ma: karta bez miniatury (o braku mówi [[grob]] → *States*) |

## Sketch
v3 — karta ze zdjęciem nagrobka (pierwsza) obok karty bez zdjęcia:
```
│ ╭──────────────────────────────╮ │
│ │ ▓▓▓▓  Grób rodzinny        › │ │  ← miniatura 56 dp
│ │ ▓▓▓▓  Wymyślonych            │ │
│ │       Jan Wymyślony, Anna    │ │
│ │       Wymyślona, Józef W…    │ │
│ ╰──────────────────────────────╯ │
│ ╭──────────────────────────────╮ │
│ │ Maria Próbna, Piotr Próbny › │ │  ← bez zdjęcia: jak v2
│ │ Kwatera B · Rząd 3 · …       │ │
│ ╰──────────────────────────────╯ │
```

v2:
```
┌──────────────────────────────────┐
│ ←  Cmentarz Wymyślony            │
│    Miejscowość Testowa           │
│                                  │
│  3 groby · 6 osób                │
│ ╭──────────────────────────────╮ │
│ │ Grób rodzinny Wymyślonych  › │ │  ← nazwa grobu
│ │ Jan Wymyślony, Anna          │ │  ← osoby, pomocniczy
│ │ Wymyślona, Józef Wymyślony   │ │
│ │ Bez adresu kwatery · bez     │ │
│ │ pinezki                      │ │
│ ╰──────────────────────────────╯ │
│ ╭──────────────────────────────╮ │
│ │ Maria Próbna, Piotr Próbny › │ │  ← bez nazwy: tytułem osoby
│ │ Kwatera B · Rząd 3 ·         │ │
│ │ Miejsce 12 · bez pinezki     │ │
│ ╰──────────────────────────────╯ │
│ ╭──────────────────────────────╮ │
│ │ Ewa Testowa                › │ │
│ │ Bez adresu kwatery · bez     │ │
│ │ pinezki                      │ │
│ ╰──────────────────────────────╯ │
│                                  │
│ ╭──────────────────────────────╮ │
│ │          Dodaj grób          │ │  ← wypełniony, akcent, przypięty
│ ╰──────────────────────────────╯ │
└──────────────────────────────────┘
```

## Tempo
Rekordem jest **grób**: ok. 50 na całe notatki (G6, [[NT-002-transcribe-the-notes]]).
- **Nowy grób:** „Dodaj grób” = **1 dotknięcie**, potem formularz pierwszej osoby ([[wpis-osoby]] → *Tempo*).
- **Pierwszy grób na nowym cmentarzu:** znicz → „Otwórz cmentarz” → „Dodaj grób” = 3 dotknięcia.
- **Nazwa grobu** nie kosztuje tu nic — nadaje się ją w [[grob]] (2 dotknięcia i pisanie, tylko dla grobów,
  które mają nazwę).

## Style B rules applied
- **Reguła 1:** jedyny wypełniony przycisk to „Dodaj grób” — w przepisywaniu to powtarzana czynność tego
  ekranu. Bez znicza (reguła 8: „Dodaj” to działanie, nie miejsce pamięci).
- **Reguły 2 i 11:** karty na powierzchni z chevronem. **Miniatura zdjęcia nagrobka z lewej, gdy zdjęcie jest**
  (v3), bez zastępczego obrazka.
- **Reguła 14 (v1.7):** miniatura bez filtrów i bez tekstu na niej.
- **Reguła 4:** tytuł paska i tytuły kart półgrube.
- **Reguła 5:** margines 16 dp, 8 dp między kartami, 24 dp między podsumowaniem a paskiem.
- **Reguła 6:** adres pełnymi słowami, liczby odmienione (`polish.dart` → `gravesLabel`, `peopleLabel`).
- **Reguła 7:** „Bez adresu kwatery · bez pinezki” to fakt w tekście pomocniczym, nie ostrzeżenie.
- **Reguła 9:** pusty stan mówi, co tu będzie, i ma jedno działanie.
- **Tokeny:** bez nowych. Kontrast: tytuł karty 10,02:1, linie pomocnicze 5,01:1 na powierzchni
  ([[style-b]] → *Measurement*).

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-002 AC-1 | 3 → [[grob]] | karta grobu wymienia wszystkie wpisane osoby; po dotknięciu każda ma kartę w [[grob]] |
| US-002 AC-5 | 3 (c), 4 | grób zapisany z samym cmentarzem i osobami ma kartę z „Bez adresu kwatery · bez pinezki” |
| ISSUE-012: „Otwórz cmentarz” otwiera ekran cmentarza | [[cmentarze]] element 7 → 1 | arkusz cmentarza na mapie → „Otwórz cmentarz” → pasek z nazwą tego cmentarza |
| decyzja autora 2026-10-06: nazwa grobu | 3 (a) | grób z nazwą nadaną w [[grob]] ma ją jako tytuł karty |
| ISSUE-012: styl B | całość | reguły wyżej; przegląd `ui` przed stopem #2 |
| US-005 AC-1 (v3) | 3 (d) | grób ze zdjęciem dodanym w [[grob]] ma jego miniaturę w karcie |

## Decisions
- **D1 — „jak R2 bez satelity” = arkusz grobów na cały ekran, bez pola mapy.** Groby z notatek nie mają
  pinezek, a ISSUE-012 nie daje sposobu ich postawienia (pinezka → [[EPIC-002-wizyta]], M6). Pole mapy bez
  zdjęcia satelitarnego i bez ani jednej pinezki byłoby stale pustym prostokątem nad listą — na ekranie
  używanym ok. 50 razy. **Kierunek:** gdy [[SPIKE-001-map-source-offline]] da zdjęcie cmentarza, a groby
  dostaną pinezki, mapa staje nad listą, a lista zamienia się w dolny arkusz jak w R2 (makieta, ramka 8 —
  poglądowo, nie w ISSUE-012). Wtedy grób z pinezką ma znicz na mapie, a grób bez — tylko kartę w arkuszu.
  *Obali:* autor chce widzieć pole mapy już teraz (np. punkt cmentarza na mapie Polski) — wtedy pasek mapy
  nad arkuszem, z ryzykiem pustego miejsca.
- **D2 — „z pinezką i bez” to dopisek w karcie, nie dwie sekcje.** W ISSUE-012 żaden grób nie będzie miał
  pinezki, więc sekcja „z pinezką” byłaby zawsze pusta. Dopisek „· bez pinezki” niesie to samo w każdej
  karcie i zniknie sam, gdy pinezka powstanie.
- **D3 — karta bez przycisku „Pokaż grób” z R2.** R2 to arkusz jednego wybranego grobu, więc ma przycisk. Na
  liście cała karta prowadzi do grobu (reguła 11), a jeden wypełniony przycisk na ekranie należy do „Dodaj
  grób” (reguła 1). „Pokaż grób” ze zniczem wraca z arkuszem pod mapą (D1).
- **D4 — karta bez liczby osób** („3 osoby” z R2): karta wymienia osoby z imienia, więc liczba byłaby
  powtórzeniem. Liczby zostają w podsumowaniu (2). *Obali:* arkusz pod mapą (D1), gdzie jest miejsce tylko na
  liczbę — tam wraca „3 osoby” jak w R2.
- **D5 — bez nazwy tytułem są osoby, a nie „Grób”.** Na liście pięciu kart „Grób” nie da się odróżnić, a
  osoby z notatek tak. Nazwy nie wyliczamy z nazwisk: odmiana w dopełniaczu liczby mnogiej (Wymyślony →
  Wymyślonych) bywa błędna, a błąd na grobie rodziny razi ([[grob]] → D1).
- **D6 — kolejność wpisania**, czyli kolejność z notatek: łatwo sprawdzić, gdzie się skończyło. *Obali:*
  autor szuka grobów po nazwisku — to wyszukiwanie osób (S5).
- **D7 — wstecz wraca na mapę z otwartym arkuszem tego cmentarza**, bo stamtąd się przyszło, a arkusz
  pokazuje nowe liczby — to potwierdzenie, że groby się zapisały.
- **D8 — [[NFR-004-czytelnosc-w-sloncu]] nie rozstrzyga się tutaj** (zmiana względem [[cmentarze]] D12, które
  wskazywało ten ekran). W ISSUE-012 cmentarz to ekran przepisywania w domu, a nie wizyty. Miara zapada przy
  pierwszym ekranie wizyty: mapie cmentarza z pinezkami (D1, [[EPIC-002-wizyta]]). Do tego czasu linie
  pomocnicze mają 5,01:1 (AA).
- **D9 — miniatura nagrobka w karcie** (v3). Autor chciał w arkuszu grobu „miejsca na zdjęcie” (ISSUE-012 →
  *Input from the author* 2), a R2 ma miniaturę nagrobka. Na liście ok. 50 grobów nagrobek rozpoznaje się
  szybciej niż listę imion. Kwadrat 56 dp, a nie okrąg jak przy osobie: nagrobek to przedmiot, okrąg zostaje dla
  ludzi (R3, R4). To decyzja projektowa spoza AC US-005 (AC-1 mówi „przy grobie”), widoczna na stopie #1.
  *Obali:* autor uznaje miniatury na liście za szum — wtedy zdjęcie tylko w [[grob]].

## Open
brak.
