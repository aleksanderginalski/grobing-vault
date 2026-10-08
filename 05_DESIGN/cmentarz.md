---
screen: "Cmentarz — groby na cmentarzu"
items: ["[[ISSUE-012-transcribe-grave-screen]]", "[[ISSUE-016-photos-grave-and-person]]", "[[SPIKE-004-mvp-flow-prototype]]"]
us: "[[US-002-przepisanie-grobu]] · [[US-005-zdjecia]]"
journey-step: "n/a — M1 (warunek kroku 1 UJ-001); docelowo mapa cmentarza z arkuszem grobu (R2, krok 2 UJ-001, M3)"
mockup: "katalog tymczasowy sesji 2026-10-07: makieta-cmentarz-grob-osoba.html (ramki 1–2, 8, ISSUE-012) · makieta-zdjecia.html (ramka 9, ISSUE-016) · 2026-10-08: grobing-prototyp.html (SPIKE-004, panel 2)"
updated: 2026-10-08
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
>
> **Wersja 4 — discovery na prototypie, panel 2 ([[SPIKE-004-mvp-flow-prototype]] D8–D11, 2026-10-08): cmentarz to
> mapa.** Kierunek z D1 („mapa nad listą, lista w dolnym arkuszu jak w R2”) autor zmienił na prototypie:
> - **na starcie sama mapa**: plan schematyczny z OSM (offline) albo zdjęcie z góry (online), kwatery, znicze grobów
>   z pinezką, bez listy (D10, D11);
> - **znicz → arkusz jednego grobu** z „Pokaż grób” (R2);
> - **arkusz przeciągnięty w górę → cała lista grobów bez mapy**, a karta na liście → [[grob]];
> - **bez linku do Grobonetu i do wyszukiwarki zarządcy** (D12);
> - kwatery jako nazwane strefy z przerywaną linią (D13).
>
>
> **Wersja 4.1 — panel 2, runda 2 (SPIKE-004 D12, 2026-10-08):** w stanie mapy pasek grobów na dole z liczbą grobów
> bez pinezki i **wypełnionym „Dodaj grób”, takim samym jak pod listą** (autor: *„1 ok, ale chciałbym aby wygląd
> przycisku »dodaj grób« był konsekwentny z tym co jest po rozwinięciu tego paska grobów”*; przepływ: *„2. tak”*).
> Purpose, Navigation, Elements, States, Sketch, Tempo i *Style B rules applied* przepisane na trzy stany ekranu
> (mapa · jeden grób · lista). **Zbudowany ekran (ISSUE-012/016) to dzisiejszy stan C bez planu i bez pasków.**
>
> **Wersja 4.2 — wizyta, panel 7 ([[SPIKE-004-mvp-flow-prototype]] D22, 2026-10-08):** autor: *„5. ok”*. Na planie
> przycisk **„gdzie jestem”** z niebieską kropką i kołem dokładności; w arkuszu grobu z pinezką **„Popraw pinezkę”** (R2);
> **tryb stawiania pinezki** (stan D) z GPS — pinezka w kropce, przesuwana dotknięciem planu, zapis ze źródłem „GPS ±N m,
> data”; **bez internetu** plan działa, a „Zdjęcie” mówi „bez internetu”. Wejście do trybu D także z [[grob]] („Postaw
> pinezkę”). Elementy 10–14, stan D i *States*.

## Purpose
Cmentarz rodziny **jako mapa** (UJ-001 krok 2, M3, M7): plan schematyczny bez sieci albo zdjęcie z góry z siecią,
kwatery zaznaczone przez autora i znicze grobów z pinezką. Stąd autor idzie do **jednego grobu** (znicz) albo do
**listy wszystkich grobów**, także bez pinezki, i dodaje kolejny grób z notatek (M1). Lista mówi, czy grób ma adres
kwatery i pinezkę (US-002 AC-5), i pokazuje, dokąd doszło przepisywanie.

## Navigation
- **Z [[cmentarze]]:** arkusz cmentarza → **„Otwórz cmentarz”** (element 7). Ekran otwiera się zawsze w stanie A.
  Także dla cmentarza bez grobów, bez planu i bez punktu na mapie.
- **Trzy stany ekranu** ([[SPIKE-004-mvp-flow-prototype]] D9, D12):
  - **A — mapa:** plan (2–5) i pasek grobów na dole (6). Znicz → B. Pasek (dotknięcie albo przeciągnięcie w górę)
    → C. „Dodaj grób” → [[wpis-osoby]] w trybie „nowy grób”: grób powstaje z pierwszą osobą, przy jej zapisie;
  - **B — jeden grób:** arkusz grobu (7), a plan przesuwa się płynnie nad arkusz. „Pokaż grób” → [[grob]]. Arkusz
    przeciągnięty w górę → C. Dotknięcie planu albo wstecz → A;
  - **C — lista:** wszystkie groby na cały ekran, bez planu (8–9). Karta → [[grob]]. Lista przeciągnięta w dół albo
    wstecz → stan, z którego przyszła (B albo A).
- **Wstecz w stanie A → [[cmentarze]]** z tym samym cmentarzem wybranym i jego arkuszem (D7). Z [[grob]] wstecz →
  stan, w którym autor ekran opuścił.
- **✎ w pasku → okno „Popraw cmentarz”** ([[cmentarze]] 15), według [[style-b]] reguły 15. Zaznaczanie kwater i
  stawianie pinezek to osobne działania: panel 7 (wizyta) i pierwsza US [[EPIC-002-wizyta]].
- **Pasek dolny** Mapa · Osoby · Drzewo jest widoczny we wszystkich stanach, a aktywna jest Mapa ([[style-b]] reguła
  12, SPIKE-004 D2).

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** wstecz + **nazwa cmentarza** (18 sp, półgruby, do 2 linii), pod nią miejscowość (13 sp, tekst pomocniczy; bez miejscowości brak linii); po prawej ✎ (`edit_outlined`, akcent, `tooltip` „Popraw cmentarz”) | pasek | wstecz (*Navigation*); ✎ → okno | — | — | R2 (nagłówek) · [[style-b]] reguła 15 |
| 2 | **Plan schematyczny** na całą szerokość pod paskiem, także pod arkuszami: obrys cmentarza i alejki z OSM, pobrane przy dodaniu cmentarza ([[style-b]] reguła 13: teren — powierzchnia z obrysem, alejki — obrys 4 i 2 dp). Wyśrodkowany w wolnym miejscu między plakietkami (3) a paskiem grobów (6); w stanie B przesuwa się płynnie nad arkusz (jak [[cmentarze]] D30). Podpis „© OpenStreetMap” (11 sp, tekst pomocniczy) pod plakietką. **Bez planu:** ikona `cloud_download`, „Plan tego cmentarza pobierze się, gdy będzie internet.”, „Groby są na liście — pasek na dole.” (14 sp, tekst pomocniczy) i przycisk tekstowy „Pobierz teraz” (akcent) | mapa | szczypanie, przeciąganie, podwójne dotknięcie; bez obrotu | cały cmentarz, północ u góry | — | [[ADR-003-map-source-offline]] pkt 1 · D10 |
| 3 | **Plakietki na planie**, na powierzchni, wys. 32 dp, margines 12 dp. Z lewej **„Plan offline”** z ikoną `offline_pin` w zieleni stanu (propozycja `#8CC084`, [[style-b]] *State colours*). Z prawej przełącznik segmentowy **Plan · Zdjęcie** (ikony `map_outlined`, `satellite_alt`; aktywny segment w akcencie). „Zdjęcie” to ortofotomapa GUGiK, tylko online, nic nie zapisuje w telefonie; plakietka zmienia się na „tylko z internetem” z ikoną `wifi` (tekst pomocniczy), a podpis na „Ortofotomapa: GUGiK”. Wygląd „Zdjęcia” bez sieci → panel 7 (wizyta, offline) | plakietka + przełącznik | segment → warstwa | Plan | — | [[ADR-003-map-source-offline]] pkt 2 · D10 |
| 4 | **Kwatery autora:** przerywana linia (tekst, krycie 75%, kreska 5/4) i nazwa „Kwatera A” (12 sp, półgruba, obwódka w kolorze tła planu) w dolnym lewym rogu strefy. Kwatera bez strefy jest tylko w adresach grobów | strefy | — | — | — | [[ADR-003-map-source-offline]] pkt 3 · D13 |
| 5 | **Znicze grobów z pinezką:** znicz-pinezka 28 × 35 dp, cel dotyku ≥ 48 dp; wybrany 38 × 47 dp z poświatą ([[style-b]] reguła 13). Grób bez pinezki nie ma znicza | znaczniki | dotknięcie → stan B | — | — | R2 · D11 |
| 6 | **Pasek grobów** (stan A): dolny arkusz na powierzchni, promień 16 dp u góry, uchwyt. „6 grobów · 14 osób” (14 sp, tekst), pod spodem „2 groby bez pinezki — na liście” albo „wszystkie groby mają pinezki” (13 sp, tekst pomocniczy). Pod nimi **wypełniony „Dodaj grób”** z ikoną `add`, ≥ 52 dp, na pełną szerokość — **ten sam przycisk co pod listą (9)** | dolny arkusz + przycisk główny | dotknięcie albo przeciągnięcie w górę → stan C; „Dodaj grób” → [[wpis-osoby]] „nowy grób” | — | — | **decyzja autora** (SPIKE-004 D12) · D14 |
| 7 | **Arkusz grobu** (stan B), na powierzchni, z uchwytem: miniatura nagrobka 72 dp (promień 12 dp; bez zdjęcia brak miniatury), tytuł (16 sp, półgruby — jak 8 (a)), adres (14 sp, tekst pomocniczy), ikona `group_outlined` + „3 osoby”, **wypełniony „Pokaż grób” ze zniczem** (kolor tła na akcencie) | dolny arkusz + przycisk główny | „Pokaż grób” → [[grob]]; przeciągnięcie w górę → stan C | — | — | R2 (arkusz grobu) · D11 |
| 8 | **Lista grobów** (stan C), pod paskiem (1), na powierzchni z uchwytem: podsumowanie „6 grobów · 14 osób” (14 sp, tekst pomocniczy, margines 16 dp) i karty (promień 16 dp, odstęp 8 dp, margines 16 dp) w kolejności wpisania. Karta, od góry: **(a) tytuł** — nazwa grobu (16 sp, półgruby, kolor tekstu, do 2 linii); bez nazwy tytułem są **osoby w grobie**: imiona i nazwiska po przecinku, ten sam krój, do 2 linii, potem „i jeszcze 2”. **(b) osoby** — tylko gdy tytułem jest nazwa: imiona i nazwiska po przecinku (14 sp, tekst pomocniczy, do 2 linii, potem „i jeszcze 2”). **(c) adres** (14 sp, tekst pomocniczy): „Kwatera B · Rząd 4 · Miejsce 12”, a bez pinezki dopisane „· bez pinezki”; bez adresu „Bez adresu kwatery · bez pinezki”. Chevron „›” po prawej. Karta ≥ 64 dp. **(d) miniatura** — tylko gdy grób ma zdjęcie: zdjęcie nagrobka ([[grob]] D9), kwadrat **56 dp** z zaokrągleniem 8 dp, przycięty ze środka, z lewej, wyśrodkowany w pionie, odstęp 12 dp do tekstu; poza czytnikiem. Bez zdjęcia bez miniatury i bez wcięcia ([[grob]] D11). **Grób wybrany w stanie B** ma obrys 1,5 dp w akcencie | lista kart | karta → [[grob]]; przeciągnięcie w dół → stan B albo A | kolejność wpisania | — | AC-1 · AC-5 · R2 · decyzja autora (nazwa grobu) · US-005 AC-1 · D6, D9, D11 |
| 9 | **„Dodaj grób”** pod listą — wypełniony, z ikoną `add`, ≥ 52 dp, przypięty na dole; lista przewija się nad nim, a ostatnia karta ma pod sobą odstęp na wysokość przycisku | przycisk główny | → [[wpis-osoby]] „nowy grób” | — | — | *What to build* 2 · D14 |
| 10 | **„Gdzie jestem”** — okrągły przycisk 48 dp na powierzchni (`my_location`), z prawej nad paskiem grobów albo arkuszem grobu (R2). Włączony: ikona w kolorze kropki „tu jesteś”, na planie **niebieska kropka** 16 dp z obwódką w kolorze tła i **kołem dokładności** (kolor kropki, krycie 18%), obok plakietka „tu jesteś · ±4 m” (12 sp) | przycisk-ikona | włącz / wyłącz lokalizację; pierwsze użycie → systemowe pytanie o uprawnienie lokalizacji | wyłączony | brak uprawnienia → „Bez zgody na lokalizację pinezki postawisz tylko ręcznie.” | R2 · [[style-b]] *State colours* · D15 |
| 11 | **„Popraw pinezkę”** (stan B, grób z pinezką) — pigułka na powierzchni z `edit_location_alt` w akcencie, z lewej nad arkuszem grobu (R2) | przycisk | → stan D dla tego grobu | — | — | R2 · M6 · D15 |
| 12 | **Stan D — stawianie pinezki:** zamiast plakietek u góry karta „**Stań przy grobie.** Pinezka stanie w niebieskiej kropce. Możesz ją przesunąć — dotknij planu.” (13 sp, `my_location` w akcencie); na planie kropka i **znicz w obrysie** (miejsce jeszcze niezapisane, [[style-b]] reguła 13) w kropce; dotknięcie planu przesuwa znicz. Na dole arkusz: tytuł grobu, „dokładność GPS ±4 m · źródło pinezki: GPS” i „Anuluj” (tekstowy) · **„Zapisz pinezkę”** (wypełniony) | tryb mapy | „Zapisz pinezkę” → zapis pinezki ze źródłem i dokładnością ([[FR-001-provenance]]) → stan B z tym grobem; „Anuluj”/wstecz → poprzedni stan | pinezka w kropce | dokładność gorsza niż 15 m → pod tekstem „Słaby sygnał — przesuń pinezkę ręcznie.” | M6 · H3 · **decyzja autora** (D22) · D16 |
| 13 | **Bez internetu (M7):** plan bez zmian; plakietka przy „Zdjęciu” — `wifi_off` „bez internetu”, a wybrane „Zdjęcie” pokazuje „Zdjęcie z góry potrzebuje internetu. Plan działa bez niego.” i „Wróć do planu” | stan | — | — | — | [[NFR-001-offline]] · [[ADR-003-map-source-offline]] pkt 2 |
| 14 | **Źródło pinezki w danych:** „GPS ±4 m · 08.10.2026” albo „zaznaczona w domu” (z planu lub zdjęcia z góry) — widać w [[grob]] pod adresem | dane | — | — | — | [[FR-001-provenance]] · [[EPIC-002-wizyta]] (każda pinezka ze źródłem i dokładnością) |

Imię i nazwisko w liście osób: „Imiona Nazwisko” bez nazwiska rodowego — „z d.” jest w [[grob]]. Osoba bez
imion albo bez nazwiska: to, co jest. Spór źródeł o grób ([[ADR-006-claimed-value-separate-structures]] D2):
osoba z dwoma pochówkami stoi w obu grobach, jak w [[grob]].

## States
| Stan | Co widać |
|---|---|
| A — mapa | 1–6 |
| B — jeden grób | 1–5, 7; pasek grobów (6) schowany |
| C — lista | 1, 8, 9 |
| bez planu | 1, zaślepka (2), pasek grobów (6) — lista działa |
| bez pinezek (np. zaraz po przepisaniu) | 1–4 bez zniczy, pasek (6): „6 grobów bez pinezki — na liście” |
| bez grobów | 1–4, pasek (6): „Na tym cmentarzu nie ma jeszcze grobów.” (tekst pomocniczy) i „Dodaj grób” |
| błąd | „Nie udało się odczytać grobów.” (tekst pomocniczy) + „Spróbuj ponownie” (przycisk z obrysem); „Dodaj grób” nieaktywny, bo nie wiadomo, do czego dodaje |
| wczytywanie | wskaźnik postępu w środku (lokalna baza — zwykle niewidoczny) |
| grób bez osób | może przyjść z innych danych (z interfejsu nie powstaje): tytuł karty „Grób bez wpisanych osób” w kolorze pomocniczym |
| brak pliku zdjęcia | wpis zdjęcia jest, pliku nie ma: karta bez miniatury (o braku mówi [[grob]] → *States*) |
| D — stawianie pinezki | 1, 2 (z kropką i zniczem w obrysie), 12 zamiast plakietek i arkuszy |
| bez internetu | 1–6, 13 |

## Sketch
v4 — stan A (mapa) i stan B (jeden grób):
```
┌──────────────────────────────────┐   ┌──────────────────────────────────┐
│ ←  Cmentarz parafialny w       ✎ │   │ ←  Cmentarz parafialny w       ✎ │
│    Wymyślonowie · Wymyślonów     │   │    Wymyślonowie · Wymyślonów     │
│ (✓ Plan offline)  [Plan|Zdjęcie] │   │ (✓ Plan offline)  [Plan|Zdjęcie] │
│ © OpenStreetMap                  │   │  ┌ ─ ─ ─ ─ ─┐┌ ─ ─ ─ ─ ─ ─┐      │
│                                  │   │  │  ⚱   ⚱   ││   ⚱    ⚱   │      │  ← plan nad arkuszem
│  ┌ ─ ─ ─ ─ ─┐┌ ─ ─ ─ ─ ─ ─┐      │   │  │Kwatera A ││ Kwatera B  │      │
│  │  ⚱   ⚱   ││   ⚱    ⚱   │      │   │  └ ─ ─ ─ ─ ─┘└ ─ ─ ─ ─ ─ ─┘      │
│  │Kwatera A ││ Kwatera B  │      │   │ ╭──────────────────────────────╮ │
│  └ ─ ─ ─ ─ ─┘└ ─ ─ ─ ─ ─ ─┘      │   │ │ ▓▓▓  Grób rodzinny Wymyślon… │ │
│      (alejki, obrys)             │   │ │ ▓▓▓  Kwatera A · Rząd 2 · M… │ │
│ ╭──────────────────────────────╮ │   │ │      👥 3 osoby               │ │
│ │ 6 grobów · 14 osób   ── uchwyt │ │   │ │ ╭──────────────────────────╮ │ │
│ │ 2 groby bez pinezki — na liście│ │   │ │ │     ⚱  Pokaż grób        │ │ │  ← wypełniony
│ │ ╭──────────────────────────╮ │ │   │ │ ╰──────────────────────────╯ │ │
│ │ │      +  Dodaj grób       │ │ │   │ ╰──────────────────────────────╯ │
│ │ ╰──────────────────────────╯ │ │   │  Mapa      Osoby      Drzewo     │
│ ╰──────────────────────────────╯ │   └──────────────────────────────────┘
│  Mapa      Osoby      Drzewo     │
└──────────────────────────────────┘
```
Stan C (lista) — karty jak w v3, na cały ekran pod paskiem (1), z wypełnionym „Dodaj grób” na dole. Szkice v2 i v3:
*Historia* w nagłówku i makiety z 2026-10-07.

## Tempo
Rekordem jest **grób**: ok. 50 na całe notatki (G6, [[NT-002-transcribe-the-notes]]).
- **Nowy grób:** stan A → „Dodaj grób” = **1 dotknięcie** (jak w v3), potem formularz pierwszej osoby ([[wpis-osoby]]
  → *Tempo*).
- **Pierwszy grób na nowym cmentarzu:** znicz → „Otwórz cmentarz” → „Dodaj grób” = 3 dotknięcia (jak w v3).
- **Grób bez pinezki:** pasek → karta = **2 dotknięcia** (w v3 jedno). Przy przepisywaniu wszystkie groby są bez
  pinezki, ale przepisywanie prowadzi „Dodaj grób”, a do listy wraca się rzadziej.
- **Grób z pinezką:** znicz → „Pokaż grób” = 2 dotknięcia.
- **Nazwa grobu** nie kosztuje tu nic — nadaje się ją w [[grob]].

## Style B rules applied
- **Reguła 1:** jeden wypełniony przycisk w każdym stanie — A: „Dodaj grób”, B: „Pokaż grób”, C: „Dodaj grób”.
  Ten sam „Dodaj grób” w A i C (decyzja autora, D14).
- **Reguła 8:** „Pokaż grób” ze zniczem (prowadzi do miejsca pamięci), „Dodaj grób” bez znicza (działanie).
- **Reguły 2 i 11:** karty na powierzchni z chevronem, miniatura nagrobka z lewej, gdy zdjęcie jest.
- **Reguła 12:** pasek dolny we wszystkich stanach. **Reguła 15:** ✎ w pasku.
- **Reguła 13 (v1.14):** plan, kwatery autora, znicze; zieleń „Plan offline” tylko z ikoną i podpisem (SC 1.4.1).
- **Reguła 14:** miniatury bez filtrów i bez tekstu; zdjęcie z góry to treść z zewnątrz — na nim tylko znicze,
  nazwy kwater z obwódką i plakietki na powierzchni.
- **Reguły 4–7:** tytuły półgrube; margines 16 dp, 8 dp między kartami; adres pełnymi słowami, liczby odmienione;
  „bez pinezki” to fakt w tekście pomocniczym.
- **Tokeny:** zieleń offline (propozycja, [[style-b]] *State colours*); reszta bez zmian. Kontrast: tytuł karty
  10,02:1, linie pomocnicze 5,01:1 na powierzchni, zieleń 8,19:1 na powierzchni.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| US-002 AC-1 | 8 → [[grob]] | karta grobu wymienia wszystkie wpisane osoby; po dotknięciu każda ma kartę w [[grob]] |
| US-002 AC-5 | 6, 8 (c), 9 | grób zapisany z samym cmentarzem i osobami ma kartę z „Bez adresu kwatery · bez pinezki”, a pasek liczy groby bez pinezki |
| ISSUE-012: „Otwórz cmentarz” otwiera ekran cmentarza | [[cmentarze]] element 7 → 1 | arkusz cmentarza na mapie → „Otwórz cmentarz” → pasek z nazwą tego cmentarza |
| decyzja autora 2026-10-06: nazwa grobu | 7, 8 (a) | grób z nazwą nadaną w [[grob]] ma ją jako tytuł karty i arkusza |
| ISSUE-012: styl B | całość | reguły wyżej; przegląd `ui` przed stopem #2 |
| US-005 AC-1 | 7, 8 (d) | grób ze zdjęciem dodanym w [[grob]] ma jego miniaturę w karcie i w arkuszu |
| M3 / [[ADR-003-map-source-offline]] (EPIC-002, pozycja do rozpisania) | 2–5, 7 | plan offline z kwaterami i zniczami; zdjęcie z góry online; znicz → arkusz grobu → „Pokaż grób” |

## Decisions
- **D1 — „jak R2 bez satelity” = arkusz grobów na cały ekran, bez pola mapy.** *(Zastąpione w v4 przez D10–D11.)* Groby z notatek nie mają
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
- **D3 — karta bez przycisku „Pokaż grób” z R2.** *(W v4 „Pokaż grób” wraca w arkuszu grobu ze znicza — D11.)* R2 to arkusz jednego wybranego grobu, więc ma przycisk. Na
  liście cała karta prowadzi do grobu (reguła 11), a jeden wypełniony przycisk na ekranie należy do „Dodaj
  grób” (reguła 1). „Pokaż grób” ze zniczem wraca z arkuszem pod mapą (D1).
- **D4 — karta bez liczby osób** („3 osoby” z R2): *(w v4 „3 osoby” wraca w arkuszu grobu ze znicza — D11)* karta wymienia osoby z imienia, więc liczba byłaby
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
- **D10 — cmentarz to mapa: plan schematyczny + zdjęcie z góry** (v4, SPIKE-004 D8; [[ADR-003-map-source-offline]]).
  Plan to obrys i alejki z OSM w tokenach stylu B, pobrany przy dodaniu cmentarza. Ma plakietkę „Plan offline” (zieleń
  stanu z ikoną) i podpis „© OpenStreetMap”. Przełącznik **Plan / Zdjęcie** w prawym górnym rogu: zdjęcie to
  ortofotomapa GUGiK, tylko z internetem, z plakietką „tylko z internetem” i podpisem „Ortofotomapa: GUGiK”. Bez planu
  (przy dodaniu nie było sieci) jest zaślepka „Plan tego cmentarza pobierze się, gdy będzie internet.” i „Pobierz
  teraz”. Autor: *„Plan i zdjęcie ok, dodaj grób ok”*. **Zastępuje D1.**
- **D11 — na starcie sama mapa; jeden grób po zniczu; lista po przeciągnięciu, bez mapy** (v4, SPIKE-004 D9). Autor:
  *„list grobów nie chce aby była — dopiero po kliknięciu na pineske chciałbym aby ten jeden grób się pojawił”*.
  Znicz → arkusz grobu: miniatura nagrobka, tytuł, adres, „3 osoby” (wraca z R2, D4), **wypełniony „Pokaż grób” ze
  zniczem** (wraca z R2, D3). Arkusz przeciągnięty w górę → **lista grobów na cały ekran**, bez mapy, w kolejności
  wpisania (D6), z kartami jak w elemencie 3. Karta → [[grob]]. Na liście zaznaczony grób ma obrys w akcencie. Mapa
  wraca po przeciągnięciu listy w dół albo „wstecz”. *Obali:* autor przy wizycie chce widzieć listę i mapę naraz.
- **D12 — bez linku do Grobonetu i do wyszukiwarki zarządcy** (v4, SPIKE-004 D10). Autor: *„Nie wykorzystujemy tej
  funkcjonalności, z grobonetu chciałem tak naprawdę tylko te mapki”*. Planów zarządców nie wolno kopiować
  ([[ADR-003-map-source-offline]], W3), więc ich miejsce zajmuje plan schematyczny z kwaterami autora. Zmiana zakresu
  M3 ([[EPIC-002-wizyta]]).
- **D13 — kwatera to nazwana strefa z przerywaną linią** (v4, SPIKE-004 D11): linia w kolorze tekstu, krycie 75%,
  kreska 5/4; nazwa „Kwatera A” 12 sp, półgruba, z obwódką w kolorze tła planu, w dolnym lewym rogu strefy, żeby nie
  wchodziła pod znicze. Kwatera bez strefy żyje tylko w adresach grobów. Autor: *„ok”*.

- **D14 — pasek grobów w stanie mapy, z tym samym „Dodaj grób” co pod listą** (v4.1, SPIKE-004 D12). Groby bez
  pinezki nie mają znicza, a zaraz po przepisaniu notatek pinezki nie ma żaden grób. Bez paska lista byłaby więc
  nieosiągalna. Pasek liczy groby bez pinezki i prowadzi do listy. Autor przyjął pasek i poprosił, żeby „Dodaj grób”
  wyglądał jak pod listą: wypełniony, pełna szerokość. *Obali:* pasek zasłania południe planu na małym telefonie —
  wtedy „Dodaj grób” obok liczby, ale wciąż wypełniony.

- **D15 — „gdzie jestem” na żądanie, nie zawsze** (v4.2, SPIKE-004 D22). Lokalizacja tylko po dotknięciu: w domu nie jest
  potrzebna, a na cmentarzu jest jednym gestem. *Obali:* autor na miejscu zawsze ją włącza — wtedy włączona sama, gdy
  telefon jest w obrysie cmentarza.
- **D16 — pinezka z GPS z możliwością przesunięcia** (v4.2, D22; M6, H3). GPS przy grobie bywa niedokładny; przesunięcie
  dotknięciem planu poprawia go bez nowego trybu. Źródło i dokładność zapisują się z pinezką. *Obali:* pomiar na
  cmentarzu (*Parked*) pokaże dokładność gorszą niż szerokość alejki — wtedy pinezka zaczyna się od kwatery, nie od GPS.

## Open
brak. Wejście do listy na cmentarzu bez pinezek rozstrzygnął pasek grobów (D14).
- ⚠️ OPEN — **dokładność GPS przy grobie** (ile metrów, czy kropka trafia w kwaterę) — mierzy wizyta na cmentarzu
  (`CURRENT_STATE.md` → *Parked*, SPIKE-001 D5). Od wyniku zależy próg „słaby sygnał” (element 12).
