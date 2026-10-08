---
screen: "Osoba — widok osoby (kim była, rodzina, jak łączy się ze mną, źródła)"
items: ["[[SPIKE-004-mvp-flow-prototype]]"]
us: "do rozpisania — M5 w [[EPIC-002-wizyta]] (widok 4); źródła przy faktach: [[US-004-fakt-od-babci]] AC-4"
journey-step: "UJ-001 · 5 (widok 4, M5, R4 prawy)"
mockup: "2026-10-08: grobing-prototyp.html (SPIKE-004, panel 4) — katalog tymczasowy sesji, ścieżka w SPIKE-004"
updated: 2026-10-08
---

# Osoba — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.16) · referencja: [[references]] → **R4 prawy**.
>
> **Wersja 1 — discovery na prototypie, panel 4 ([[SPIKE-004-mvp-flow-prototype]] D14–D17, 2026-10-08).** Ekranu nie
> ma w aplikacji: karta osoby w [[grob]] otwierała dotąd formularz poprawy ([[wpis-osoby]]). Autor o prototypie:
> *„jest super”*, z trzema zmianami:
> - **„Rodzina” to docelowo mini-drzewo** najbliższej rodziny z zakładki Drzewo: rodzice, dzieci, partnerzy (D5). Do
>   czasu projektu drzewa (panel 6) — chipy;
> - **płeć wraca**, żeby mówić „babcia”, „dziadek”, „stryj”, „siostra cioteczna” (D4);
> - **zdjęcie w tle jak na Facebooku** zamiast gałązek z R4 (D3).
>
> **Wersja 1.1 — runda po panelach 4–9 (SPIKE-004 D18, D19, 2026-10-08):** widok w wersji 2 przyjęty (*„1 jest
> dobrze”*): **„Rodzina” to mini-drzewo** (element 6). **Pochówek prowadzi na mapę cmentarza z zaznaczoną pinezką**
> (element 9; autor: *„Osoby -> Wybrana osoba -> Miejsce pochówku -> I jestem kierowany na widok Cmentarza z
> zaznaczoną pinezką”*). Pod „Daty i źródła” jest widoczne wejście „Dopisz, co mówi babcia” (element 8), bo samo
> dotknięcie daty było niewidoczne (autor o panelu 8: *„nie wiem jak wejść”*).
>
> **Wersja 1.2 — fakt od babci to zwykła poprawa ([[SPIKE-004-mvp-flow-prototype]] D27, 2026-10-08):** autor: *„Babcia to
> po prostu jedna z osób które dadzą mi wkład do tego co później wrzucę do notatek o danej osobie - nie ma potrzeby mieć
> tam źródła. Po rozmowie z babią normalnie wszedłbym na edycje danej osoby i dodał o niej informacje.”* Przycisk
> „Dopisz, co mówi babcia” i ekran źródeł faktu **wycofane** (element 8, D8). Czy źródło przy dacie zostaje na ekranie —
> *Open* 2.
>
> **Wersja 1.3 — bez źródeł ([[SPIKE-004-mvp-flow-prototype]] D28, 2026-10-08):** *„a to jakiś błąd się wkradł w takim razie - moje notatki to moje notatki, nie potrzeba żadnych potwierdzeń skąd pochodzą”*. Bez linii źródła przy „kim była” (5) i przy datach (8);
> D10.

## Purpose
Zbierający stoi przy grobie albo przegląda notatki i chce wiedzieć, **kim była ta osoba i jak łączy się z nim** (UJ-001
krok 5, M5). Widzi portret, „kim była”, najbliższą rodzinę, łańcuch od siebie do tej osoby i każdą datę ze źródłem
([[FR-001-provenance]], [[US-004-fakt-od-babci]] AC-4). Stąd idzie do grobu, do zdjęć, do krewnych i — pod ✎ — do
poprawy.

## Navigation
- **Wejście:** karta osoby w [[grob]] (v5) · chip albo węzeł łańcucha w innym widoku osoby · lista w zakładce Osoby
  (panel 5) · węzeł drzewa (panel 6).
- **Krewny (chip albo węzeł łańcucha) → jego widok osoby**, na tym samym stosie: wstecz wraca do poprzedniej osoby.
- **Portret → baza zdjęć osoby** ([[zdjecia-osoby]]). **Zdjęcie w tle → podgląd** ([[zdjecie]]).
- **Pochówek → mapa cmentarza z zaznaczoną pinezką** ([[cmentarz]], stan B; bez pinezki — lista, stan C). Do grobu dalej
  prowadzi „Pokaż grób” (v1.1, D9).
- **✎ w pasku → [[wpis-osoby]] w trybie „poprawa”** ([[style-b]] reguła 15). Po zapisie wraca tutaj, z nowymi danymi.
- ~~Wiersz w „Daty i źródła” → wszystkie źródła faktu; „Dopisz, co mówi babcia”~~ — wycofane (v1.2, D27). Wiedzę od babci
  autor wpisuje przez ✎ (poprawa wpisu).
- **Dolny pasek** widoczny; aktywna zakładka, z której autor przyszedł ([[style-b]] reguła 12).

## Elements in order
| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** wstecz; po prawej ✎ (`edit_outlined`, akcent, `tooltip` „Popraw wpis”). Bez tytułu — imię niesie nagłówek (4) | pasek | wstecz; ✎ → [[wpis-osoby]] „poprawa” | — | — | R4 · [[style-b]] reguła 15 · D1 |
| 2 | **Zdjęcie w tle** na pełną szerokość, 140 dp, pod paskiem, przycięte ze środka. Wybrane przez autora z bazy zdjęć osoby („Ustaw jako tło” w podglądzie zdjęcia, obok „Ustaw jako profilowe”). **Bez tła:** pasmo w kolorze powierzchni z przyciskiem z obrysem „Dodaj zdjęcie w tle” (ikona `add_photo_alternate_outlined` w akcencie) w prawym dolnym rogu | zdjęcie / przycisk | zdjęcie → podgląd; przycisk → baza zdjęć osoby w trybie wyboru tła | bez tła | — | **decyzja autora** (SPIKE-004 D17) · D3 |
| 3 | **Portret:** okrąg 104 dp z pierścieniem 2 dp w akcencie i delikatną poświatą, wyśrodkowany, **nachodzi do połowy na dolną krawędź tła** (jak profilowe na Facebooku). Profilowe w kadrze łącza ([[kadr-profilowego]]). **Bez zdjęcia:** okrąg z obrysem, `add_a_photo_outlined` w akcencie i „Dodaj zdjęcie” (12 sp) | zdjęcie / przycisk | → [[zdjecia-osoby]] | — | — | R4 · **decyzja autora** (SPIKE-004 D14) · D2 |
| 4 | **Imię i nazwisko z „z d.”** (22 sp, półgruby, wyśrodkowane, do 2 linii) · **lata życia** (14 sp, tekst pomocniczy; formaty [[style-b]] reguła 6) | tekst | — | — | — | R4 |
| 5 | **„Kim była”** (15 sp, wyśrodkowane, do 4 linii). Bez „kim była” — nic. **Bez linii źródła** (v1.3, D10) | tekst | — | — | — | R4 |
| 6 | **Rodzina** — nagłówek sekcji z ikoną `diversity_3` w akcencie. **Mini-drzewo najbliższej rodziny** (v1.1, D5): rodzice w rzędzie nad osobą, osoba z pierścieniem w akcencie i partnerzy obok, dzieci w rzędzie pod; węzły 44 dp (profilowe albo inicjały), nad imieniem nazwa roli z płcią (10 sp, tekst pomocniczy: „Ojciec”, „Matka”, „Mąż”, „Żona”, „Syn”, „Córka”; bez płci — „Rodzic”, „Partner”, „Dziecko”), imię 12 sp półgrube; linie jak w [[drzewo]] (kolory relacji). Pod spodem przycisk tekstowy **„Pokaż w drzewie”** (`account_tree`, akcent). Bez rodziny: „Rodziny jeszcze nie ma. Dodasz ją pod ✎.” | mini-drzewo | węzeł → widok tej osoby; „Pokaż w drzewie” → [[drzewo]] z tą osobą w środku | — | — | R4 · **decyzja autora** (SPIKE-004 D15, D16, D18) · D4, D5 |
| 7 | **Jak łączy się ze mną** — nagłówek z ikoną `conversion_path` w akcencie. Pierwsza linia: **nazwa pokrewieństwa wobec „ja”** (14 sp, tekst): „Twoja babcia”, „Twój pradziadek”, „Twój wuj (brat mamy)”, „Twoja siostra cioteczna”. Pod nią **łańcuch od „Ja”**: węzły 36 dp (profilowe albo inicjały na powierzchni z obrysem; „Ja” z obrysem w akcencie) połączone pionową linią 2 dp w akcencie; podpis węzła „Mama Anna”, „Babcia Maria” (14 sp, półgruby). **Bez ścieżki:** „Nie wiadomo jeszcze, jak łączy się z Tobą. Połączy się, gdy dodasz rodzinę pod ✎.” **Bez ustawionego „ja”:** „Ustaw, kim jesteś w drzewie” → ustawienia (panel 9) | łańcuch | węzeł → widok tej osoby | najkrótsza ścieżka | — | R4 · M5 · [[data-model]] (ustawienie „ja”, ścieżka liczona, nie zapisywana) · D4, D6 |
| 8 | **Daty** — nagłówek z ikoną `event_note` w akcencie. Wiersze z linią podziału: etykieta (96 dp, tekst pomocniczy) · wartość. **Bez źródła i bez statusu** (v1.3, D10). Wartość pokazana to pierwsza ([[ADR-006-claimed-value-separate-structures]] D3) | lista wierszy | — (poprawa przez ✎) | urodzenie, zgon, nazwisko rodowe, gdy jest | — | **decyzja autora** (SPIKE-004 D27, D28) · D10 |
| 9 | **Pochówek** — ostatni wiersz sekcji 8: tytuł grobu, pod nim „Cmentarz … · notatki” (13 sp, tekst pomocniczy), chevron. Bez pochówku (osoba żyjąca albo nieznany grób) — brak wiersza | wiersz | → **mapa cmentarza** ([[cmentarz]]) **z zaznaczoną pinezką tego grobu** (stan B, arkusz grobu z „Pokaż grób”); grób bez pinezki → lista grobów (stan C) z zaznaczonym grobem i komunikatem „Ten grób nie ma jeszcze pinezki — jest zaznaczony na liście.” (v1.1, D9) | — | — | M4 · FR-003 · **decyzja autora** (SPIKE-004 D19) · D9 |
| 10 | **Zdjęcia · 3** — nagłówek z ikoną `photo_library` w akcencie; rząd do 4 miniatur 56 dp (kwadraty, promień 8 dp — [[style-b]] reguła 14) i chevron. Bez zdjęć — brak sekcji | rząd miniatur | → [[zdjecia-osoby]] | — | — | [[US-005-zdjecia]] · decyzja projektowa |

## States
| Stan | Co widać |
|---|---|
| pełny | 1–10 |
| bez zdjęć | 2 jako pasmo z „Dodaj zdjęcie w tle”, 3 jako „Dodaj zdjęcie”, bez 10 |
| bez rodziny | 6: „Rodziny jeszcze nie ma. Dodasz ją pod ✎.”; 7: „Nie wiadomo jeszcze…” |
| bez „ja” | 7: „Ustaw, kim jesteś w drzewie” |
| osoba żyjąca | bez 9; lata „ur. 1952” |
| spór źródeł | 8 z ikoną `compare_arrows` i drugą wartością |
| wczytywanie | wskaźnik postępu (lokalna baza — zwykle niewidoczny) |
| błąd | „Nie udało się odczytać wpisu.” + „Spróbuj ponownie” |

## Sketch
```
┌──────────────────────────────────┐
│ ←                              ✎ │
│▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓│  ← zdjęcie w tle 140 dp
│▓▓▓▓▓▓▓▓▓▓▓▓▓▓╭──────╮▓▓▓▓▓▓▓▓▓▓▓▓│
│              │portret│             │  ← okrąg 104 dp, pierścień w akcencie
│              ╰──────╯             │
│   Maria Wymyślona z d. Testowa   │
│            1925–2004             │
│ Nauczycielka w szkole w Wymyślo… │
│         Źródło: notatki          │
│ 👪 Rodzina                        │  ← docelowo mini-drzewo (panel 6)
│ (Ojciec: Józef) (Matka: Anna)    │
│ (Mąż: Jan) (Syn: Stanisław) …    │
│ ↝ Jak łączy się ze mną           │
│ Twoja babcia                     │
│ (Ja) Ja                          │
│  │                               │
│ (AW) Mama Anna                   │
│  │                               │
│ (MW) Babcia Maria                │
│ ▤ Daty i źródła                  │
│ Urodzenie   12.03.1925 · notatki │
│ Zgon        04.11.2004 · notatki │
│ Pochówek    Grób rodzinny Wym… › │
│ ▣ Zdjęcia · 3                    │
│ ▓▓ ▓▓ ▓▓                       › │
│  Mapa      Osoby      Drzewo     │
└──────────────────────────────────┘
```

## Tempo
n/a — ekran do oglądania. Poprawa idzie przez [[wpis-osoby]] (✎).

## Style B rules applied
- **Reguła 15:** widok przed poprawą; ✎ w pasku.
- **Reguła 14:** portret — okrąg w kadrze łącza; zdjęcie w tle — prostokąt na pełną szerokość, przycięty ze środka, nic
  na nim (pasek z ikonami stoi nad nim na tle); puste miejsca tylko jako przyciski („Dodaj zdjęcie”, „Dodaj zdjęcie w
  tle”).
- **Reguła 8:** **bez gałązek** wokół portretu (rozstrzygnięte, D3 — zamiast nich zdjęcie w tle).
- **Reguła 3:** ikony nagłówków sekcji w akcencie (R4).
- **Reguła 11:** chipy relacji (wyjątek od karty); w łańcuchu węzły bez chevronu, cel dotyku ≥ 48 dp na cały wiersz.
- **Reguła 1:** bez wypełnionego przycisku — to ekran do oglądania.
- **Reguły 4–7:** imię półgrube; formaty dat i „z d.”; spokojne „nie wiadomo” i „sprzeczne” jako fakt z ikoną, nie
  ostrzeżenie (SC 1.4.1 — status nigdy samym kolorem).
- **Tokeny:** bez nowych. Pierścień portretu — para akcent/tło 8,81:1.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| M5 — kim była, relacje, łańcuch do „ja” | 4–7 | widok Marii: „kim była”, rodzina, „Twoja babcia” i łańcuch Ja → Mama Anna → Babcia Maria |
| ~~[[US-004-fakt-od-babci]] AC-4~~ | — | wycofane (SPIKE-004 D28) |
| ~~[[US-004-fakt-od-babci]] AC-1, AC-3~~ | — | wycofane (SPIKE-004 D28) |
| [[US-005-zdjecia]] — profilowe i baza zdjęć | 3, 10 | portret w kadrze; rząd miniatur prowadzi do bazy zdjęć |

## Decisions
- **D1 — widok przed poprawą** ([[style-b]] reguła 15, SPIKE-004 D4). Do formularza prowadzi tylko ✎. *Obali:* autor
  przy przepisywaniu częściej poprawia, niż ogląda — wtedy szybka ścieżka do poprawy z [[grob]].
- **D2 — portret u góry** (SPIKE-004 D14; R4). Autor: *„chciałbym mieć tam również ich portret”*.
- **D3 — zdjęcie w tle jak na Facebooku, bez gałązek** (SPIKE-004 D17). Autor: *„Tutaj bym zrobił »tło zdjęcia« tak jak
  na facebooku”*. Tło wybiera autor z bazy zdjęć osoby (np. dom, wieś, zdjęcie grupowe), więc **w danych potrzebne
  jest wskazanie tła** — jak profilowe, przy łączu osoba–zdjęcie ([[ADR-009-person-photos-record-and-link]]) — i działanie
  „Ustaw jako tło” w podglądzie zdjęcia. *Obali:* większość osób nie ma żadnego zdjęcia poza portretem — wtedy pasmo
  „Dodaj zdjęcie w tle” stoi pusto na większości ekranów i warto je schować.
- **D4 — płeć wraca; nazwy pokrewieństwa po polsku** (SPIKE-004 D16; [[rodzina]] D9' obalone). Autor: *„W sumie
  faktycznie musi wrócić płeć - bo dzięki temu możemy powiedzieć babcia, dziadek, stryj, siostra cioteczna itd.”*.
  Nazwy zależą od płci **i od strony** (stryj — brat ojca, wuj — brat matki; rodzeństwo stryjeczne, wujeczne,
  cioteczne), więc liczy je ścieżka do „ja”, a nie sama relacja. Pole „Płeć” wraca do [[wpis-osoby]] (4a) z
  podpowiedzią z imienia ([[ISSUE-019-family-relations]] → *Prior art*: 0,066% pomyłek wśród zmarłych w rejestrze
  PESEL), a schemat dostaje kolumnę płci z migracją. Słownik nazw ustala pozycja, która to zbuduje, ze źródłem
  (kanon polskiej terminologii pokrewieństwa), nie z pamięci.
- **D5 — „Rodzina” jako mini-drzewo z zakładki Drzewo** (SPIKE-004 D15). Autor: *„ta część rodzina możemy zrobić na
  razie jako placeholder bo tutaj bym wykorzystał funkcjonalność z »drzewo« gdzie widzielibyśmy najbliższą rodzinę
  danej osoby (rodzice, dzieci, partner/partnerzy)”*. Wygląd mini-drzewa wynika z panelu 6; do tego czasu chipy (6).
- **D6 — kolejność sekcji: kim była → Rodzina → Jak łączy się ze mną → Daty i źródła → Zdjęcia.** Autor: *„jest
  super”*. Najpierw to, kim była i z kim, potem jak łączy się ze mną, a źródła na końcu — to sprawdzanie, nie czytanie.
- **D7 — źródło przy każdej dacie, status tylko przy sporze, potwierdzeniu albo „nie wiadomo”** ([[US-004-fakt-od-babci]]
  AC-4). Pojedyncze źródło bez statusu, żeby nie zaśmiecać ok. 100 widoków słowem „jedno źródło”.

- ~~**D8 — widoczne wejście do źródeł: „Dopisz, co mówi babcia”** (v1.1).~~ **Obalone w v1.2** (SPIKE-004 D27): autor nie chce
  osobnej drogi dla wiedzy od babci. Samo dotknięcie wiersza daty było dla autora
  niewidoczne (*„nie wiem jak wejść i co opisujesz”*). Przycisk mówi wprost, co robi, a podpis nad wierszami mówi, że
  daty da się dotknąć. *Obali:* w rundzie 2 autor dalej nie wie, po co ten panel — wtedy fakt od babci jako osobny
  tryb „Rozmowa z babcią”.
- **D9 — pochówek prowadzi na mapę, nie do grobu** (v1.1, SPIKE-004 D19). Autor szuka, gdzie leży osoba: mapa z
  zaznaczoną pinezką odpowiada na to od razu, a „Pokaż grób” jest o jedno dotknięcie dalej. *Obali:* przy przepisywaniu
  autor częściej chce do grobu niż na mapę — wtedy dwa wiersze: „Grób” i „Na mapie”.

- **D10 — bez źródeł i statusów** (v1.3, [[SPIKE-004-mvp-flow-prototype]] D28). Autor: *„a to jakiś błąd się wkradł w takim razie - moje notatki to moje notatki, nie potrzeba żadnych potwierdzeń skąd pochodzą”*. Ekran pokazuje fakty, a nie ich pochodzenie.
  *Obali:* rodzina po autorze pyta, skąd jest data — wtedy źródło wraca najpierw do eksportu (dane i tak je mają).

## Open
1. ~~⚠️ OPEN — mini-drzewo w sekcji „Rodzina”~~ — rozstrzygnięte w v1.1 (element 6, D18).
2. ~~⚠️ OPEN — źródło przy dacie na ekranie~~ — rozstrzygnięte w v1.3: **bez źródeł** (D10, [[SPIKE-004-mvp-flow-prototype]] D28).
3. ⚠️ OPEN — **źródło przy relacjach** (US-004 AC-4 mówi „przy datach, relacjach i miejscu pochówku”): model ma
   twierdzenia przy rodzinie i łączu dziecka ([[ADR-011-relation-claims-family-and-child-link]]), a widok jeszcze
   ich nie pokazuje — razem z mini-drzewem.
4. ⚠️ OPEN — **ustawienie „ja”** (kim jest autor w drzewie) — panel 9 (ustawienia).
