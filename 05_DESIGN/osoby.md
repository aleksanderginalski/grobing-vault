---
screen: "Osoby — zakładka: wszystkie osoby i wyszukiwanie; wybór „ja”"
items: ["[[SPIKE-004-mvp-flow-prototype]]", "[[ISSUE-022-app-skeleton-tabs-people-settings]]", "[[ISSUE-025-gender-kinship-together-since]]"]
us: "do rozpisania — S5/G5 (wyszukiwanie osób; brief §5a G5 — Should, przyjęte do MVP decyzją autora na prototypie: SPIKE-004 D1, D3, D19)"
journey-step: "n/a — wejście do widoku osoby (M5) spoza ścieżki wizyty"
mockup: "2026-10-08: grobing-prototyp.html (SPIKE-004, panel 5) — katalog tymczasowy sesji, ścieżka w SPIKE-004"
updated: 2026-10-08
---

# Osoby — specyfikacja

> Żywy plik: `ui` aktualizuje go przy każdej pozycji, która ten ekran zmienia. Prawdą o ekranie jest ten
> plik; szkic i makieta to podgląd. Wytyczne: [[style-b]] (v1.17) · referencja: [[references]] → **R1** (zakładka „Osoby”).
>
> **Wersja 1 — discovery na prototypie, panel 5 ([[SPIKE-004-mvp-flow-prototype]] D19, 2026-10-08).** Autor: *„tak jest
> dobrze, przy czym jeszcze chciałbym mieć ścieżkę (Osoby -> Wybrana osoba -> (w przypadku jeżeli zmarła) Miejsce
> pochówku -> I jestem kierowany na widok Cmentarza z zaznaczoną pinezką)”*. Ścieżkę niesie [[osoba]] element 9.
> **Zakres:** wyszukiwanie osób było w briefie w Should (G5). Zakładka Osoby z R1 i decyzje D1, D3 SPIKE-004 przenoszą je
> do MVP — to decyzja autora na prototypie, zapisana jako zmiana zakresu.
>
> **Wersja 2 — zbudowane w [[ISSUE-022-app-skeleton-tabs-people-settings]], przegląd `ui` (2026-10-08).** Decyzje ze
> stopu #1 (D2, D3) i odstępstwa `dev` przyjęte w przeglądzie (*Dev report → Deviations* 1, 2, 7):
> - „Ja” przed wyborem zaprasza do wyboru, a po wyborze pokazuje imię i nazwisko wybranej osoby (D4 → element 3);
> - kolejność i litera według nazwiska, a bez nazwiska — według nazwiska rodowego; „Bez nazwiska” na końcu (D5 →
>   element 4);
> - lata życia same lata według [[style-b]] reguły 6, a bez dat napis „bez dat” (element 4);
> - pole szukania z „Wyczyść”, przewinięcie listy chowa klawiaturę (element 2);
> - **nowa część: wybór „ja” — „Która osoba to Ty?”** (elementy 6–7, D6);
> - karta osoby otwiera „Poprawę wpisu”, dopóki nie ma widoku osoby (D7, *Navigation*).
>
> ~~**Wersja 2.1 — pokrewieństwo w liście.**~~ **Wycofana na stopie #1 [[ISSUE-025-gender-kinship-together-since]]
> (wersja 2.2, 2026-10-08, decyzja autora):** *„W osobach bym nie dodawał informacji kto jest kim dla kogo to jest funkcja
> łączenia osób w drzewie (przy wielu poziomach to by się strasznie rozrastało)”*. Lista pokazuje imię, nazwisko i lata
> życia, jak w v2. „Kim jest dla mnie” jest w widoku osoby ([[osoba]] element 7) i w łączeniu osób w drzewie ([[drzewo]]).
> D2 obalone, D8 i D9 wycofane.

## Purpose
Znaleźć osobę bez wiedzy, na którym cmentarzu leży: po nazwisku albo imieniu, a w liście — zobaczyć, kim jest dla
autora. Stąd idzie do widoku osoby ([[osoba]]), a z niego do pochówku na mapie cmentarza (D19). Tu też autor wskazuje,
która osoba to on („ja”) — od niej liczą się łańcuchy i nazwy pokrewieństwa.

## Navigation
- **Zakładka „Osoby”** w dolnym pasku ([[style-b]] reguła 12, [[cmentarze]] element 18). Wyszukiwarka tej zakładki szuka
  tylko osób (SPIKE-004 D3). Zakładka otwiera ekran od razu, bez wsuwania; **wstecz z tego ekranu wraca na mapę**.
- **Karta osoby → [[osoba]]** — zakładka Osoby zostaje aktywna na całym stosie: osoba → mapa cmentarza → grób. **Do czasu
  [[ISSUE-024-person-view]] karta otwiera „Poprawę wpisu”** ([[wpis-osoby]]) tą samą drogą co chip krewnego (D7).
- **Karta „Ja”:** przed wyborem → **wybór „ja”** (elementy 6–7); po wyborze → ta osoba (jak karta osoby).
- Wstecz z osoby wraca tu, z tym samym tekstem w wyszukiwarce, tą samą pozycją listy i **bez klawiatury** (pole oddaje
  fokus przed otwarciem osoby — błąd znaleziony na emulatorze w ISSUE-022).
- **Wybór „ja”** otwiera się też z wiersza „Ja” w [[ustawienia]] (element 1) — tam zawsze, także żeby zmienić wybraną
  osobę. Wybór zapisuje i wraca tam, skąd przyszedłeś; wstecz bez wyboru niczego nie zmienia.

## Elements in order
**Zakładka Osoby**

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 1 | **Pasek:** „Osoby” (20 sp, półgruby) i po prawej liczba „34 osoby” (14 sp, tekst pomocniczy, odmiana) — wszystkie osoby, także podczas szukania | pasek | — | — | — | R1 · [[style-b]] reguła 6 |
| 2 | **Wyszukiwarka** — pigułka jak na mapie ([[cmentarze]] element 2), podpowiedź „Szukaj osoby”, a z wpisanym tekstem **× „Wyczyść”** (cel 48 dp) jak w wyszukiwarce cmentarzy. Dopasowanie bez polskich znaków i wielkości liter, od początku słowa imienia albo nazwiska (także nazwiska rodowego); nazwisko z łącznikiem to dwa słowa | pole tekstowe | wielka litera wyłączona; `search` = zamknij klawiaturę; **przewinięcie listy chowa klawiaturę** | pusto | — | D3 (SPIKE-004) · jak [[cmentarze]] D3 · ISSUE-022 odstępstwo 7 |
| 3 | **„Ja”** — pierwsza karta, z obrysem: inicjały „Ja” w akcencie (40 dp; **zawsze znak „Ja”, także gdy osoba ma profilowe** — D4), „Ja” (16 sp, półgruby), pod spodem jedna linia (14 sp, tekst pomocniczy): **przed wyborem** „Wybierz, która osoba to Ty”, **po wyborze** imię i nazwisko tej osoby („Ewa Wymyślona”, z „z d. …”, jeśli jest). Chevron. Przy wpisanym tekście znika | karta | przed wyborem → wybór „ja” (6–7); po wyborze → [[osoba]] dla „ja” (do ISSUE-024 — „Poprawa wpisu”) | — | — | M5 · [[data-model]] (ustawienie „ja”) · ISSUE-022 D3 · przegląd `ui` (D4) |
| 4 | **Lista osób A–Z po nazwisku**, z nagłówkami liter (13 sp, tekst pomocniczy). Karta (reguła 11, ≥ 64 dp): profilowe 40 dp albo inicjały, „Imiona Nazwisko z d. Rodowe” (16 sp, półgruby), pod spodem **lata życia** — 14 sp, tekst pomocniczy (v2.2: bez pokrewieństwa — D2 obalone); chevron. **Lata — same lata** według reguły 6: „1926–2010”, „ur. 1955”, „zm. 1951”, „ok. 1890 – 1951”, „między 1893 a 1895 – 1960”, a bez dat „bez dat”. Pokrewieństwa w liście nie ma (v2.2, decyzja autora). **Polskie sortowanie: po nazwisku, a gdy go brak — po nazwisku rodowym** (tego samego klucza używa nagłówek litery), potem po imionach. Osoby bez nazwiska i bez nazwiska rodowego — **na końcu, pod nagłówkiem „Bez nazwiska”**. Osoba „ja” nie powtarza się na liście (stoi w 3), ale wyszukiwanie ją znajduje | lista kart | karta → [[osoba]] (do ISSUE-024 — „Poprawa wpisu”, D7) | po nazwisku, potem po imieniu | — | **decyzja autora** (D19) · [[osoba]] D4 (nazwy pokrewieństwa) · ISSUE-022 D3, odstępstwo 2 (D5) |
| 5 | **Brak wyników:** „Nie ma osoby „<tekst>”.” (tekst pomocniczy) | tekst | — | — | — | [[style-b]] reguła 9 |

~~**Pokrewieństwo w liście (element 4, v2.1)**~~ — wycofane w v2.2 (decyzja autora, wyżej). Reguły nazw (słownik ze
źródłem, nawias ze ścieżką, opis z odcinków, odcinki neutralne bez płci) przechodzą do widoku osoby
([[ISSUE-024-person-view]], [[osoba]] element 7) — zapis kanonu w [[ISSUE-025-gender-kinship-together-since]] → *Prior art*.

**Wybór „ja” — „Która osoba to Ty?”** ([[ISSUE-022-app-skeleton-tabs-people-settings]] D3; tryb wyboru, bez dolnego paska)

| # | Element | Typ | Klawiatura / akcja | Domyślnie | Walidacja | Źródło |
|---|---|---|---|---|---|---|
| 6 | **Pasek:** wstecz + „Która osoba to Ty?” (20 sp, półgruby) · **wyszukiwarka** jak 2, **bez automatycznego fokusu** (najpierw widać listę) · **lista** jak 4: litery, A–Z, „Bez nazwiska”, brak wyników jak 5. Osoba „ja” stoi na swoim miejscu w liście | pasek, pole, lista | wstecz → bez zmiany | — | — | ISSUE-022 D3 · odstępstwo 7 · D6 |
| 7 | **Karta osoby w trybie wyboru:** jak w 4, ale **bez chevronu** — dotknięcie wybiera, a nie prowadzi dalej. Wybrana osoba: ikona `check` w akcencie zamiast chevronu i stan „zaznaczone” dla czytnika ([[style-b]] *Thresholds* → kolor jako nośnik, v1.6) | karta | dotknięcie → zapis „ja” → powrót tam, skąd przyszedłeś (reguła 10: widać wybraną osobę pod „Ja”) | obecna „ja” z ✓ | błąd zapisu → pasek komunikatu „Nie udało się zapisać. Spróbuj jeszcze raz.”, wybór zostaje otwarty | ISSUE-022 D3 · przegląd `ui` (D6) |

## States
| Stan | Co widać |
|---|---|
| pełny | 1–4 |
| „ja” niewybrane | 3 z linią „Wybierz, która osoba to Ty” |
| szukanie | 1, 2, wyniki 4 bez nagłówków liter i bez „Ja”; osoba „ja” jest w wynikach, jeśli pasuje |
| brak wyników | 1, 2, 5 |
| pusta baza | 1, 2, „Tu pojawią się osoby z grobów i rodzin.” (reguła 9); w wyborze „ja” — to samo zdanie |
| błąd odczytu | „Nie udało się odczytać osób.” (tekst pomocniczy) i przycisk z obrysem „Spróbuj ponownie” |
| wczytywanie | wskaźnik postępu (lokalna baza — zwykle niewidoczny) |
| wybór „ja” | 6–7; szukanie, brak wyników i pusta baza jak w zakładce |

## Sketch
```
 zakładka Osoby                       wybór „ja”
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│ Osoby                  34 osoby  │  │ ←  Która osoba to Ty?            │
│ ( 🔍  Szukaj osoby             ) │  │ ( 🔍  Szukaj osoby             ) │
│ ╭──────────────────────────────╮ │  │ P                                │
│ │ (Ja) Ja                     ›│ │  │ ╭──────────────────────────────╮ │
│ │      Ewa Wymyślona           │ │  │ │ (◉) Alicja Przykładowa       │ │
│ ╰──────────────────────────────╯ │  │ │     1926–2010                │ │
│ P                                │  │ ╰──────────────────────────────╯ │
│ ╭──────────────────────────────╮ │  │ W                                │
│ │ (◉) Alicja Przykładowa      ›│ │  │ ╭──────────────────────────────╮ │
│ │     1926–2010                │ │  │ │ (◉) Ewa Wymyślona           ✓│ │
│ ╰──────────────────────────────╯ │  │ │     ur. 1958                 │ │
│ ╭──────────────────────────────╮ │  │ ╰──────────────────────────────╯ │
│ │ (EP) Ewa Przykładowa        ›│ │  │ Bez nazwiska                     │
│ │     ur. 1955                 │ │  │ ╭──────────────────────────────╮ │
│ ╰──────────────────────────────╯ │  │ │ (J)  Józef                   │ │
│  Mapa      Osoby      Drzewo     │  │ │     bez dat                  │ │
└──────────────────────────────────┘  └──────────────────────────────────┘
```
Przed wyborem karta „Ja” ma w drugiej linii „Wybierz, która osoba to Ty”. Pokrewieństwa w liście nie ma (v2.2).

## Tempo
n/a — ekran do szukania i oglądania.

## Style B rules applied
- **Reguła 6:** lata życia (same lata, spacje wokół kreski, gdy strona ma więcej niż rok), „z d.”, odmiana liczby osób.
- **Reguła 9:** „Ja” przed wyborem mówi, co zrobić („Wybierz, która osoba to Ty”), a nie tylko, czym jest.
- **Reguła 10:** wybór „ja” kończy się widokiem wybranej osoby pod „Ja”, bez komunikatu.
- **Reguła 11:** karty z chevronem; profilowe — okrąg (reguła 14); bez zdjęcia — inicjały na powierzchni z obrysem
  (nie zastępczy obrazek — tekst). **W trybie wyboru bez chevronu**, wybrana z ✓ i stanem „zaznaczone”.
- **Reguła 12:** zakładka Osoby aktywna; **każda zakładka szuka swojego**; wybór „ja” to tryb wyboru — bez paska.
- **Reguła 14:** profilowe 40 dp w karcie, w kadrze łącza.
- **Tokeny:** bez nowych. „Ja” w akcencie (8,04:1 na powierzchni), obrys karty „Ja” 3,40:1 na tle.

## AC → element
| AC | Element(y) | Jak widać spełnienie |
|---|---|---|
| SPIKE-004 D19 — Osoby → osoba → pochówek → mapa z pinezką | 4 → [[osoba]] 9 → [[cmentarz]] | „Maria” → „Pochówek” → mapa Wymyślonowa z zaznaczonym zniczem jej grobu (po [[ISSUE-024-person-view]]) |
| G5 — znaleźć osobę po nazwisku wśród ok. 100 | 2, 4 | „wymys” → osoby o nazwisku Wymyślony/Wymyślona |
| (ISSUE-022) AC-2 — „Ja” i wszystkie osoby A–Z; „wymys” zostawia Wymyślony/Wymyślona | 1–5 | „Osoby” → „Ja” na górze, litery, liczba; „wymys” → tylko te osoby, bez liter i bez „Ja”; „zmys” → osoba z d. Zmyślona |
| (ISSUE-022) AC-4 — wybrana w ustawieniach osoba jest „ja” i stoi na górze | 3, 6–7 · [[ustawienia]] 1 | wybór Ewy → pod „Ja” „Ewa Wymyślona”, Ewa nie powtarza się w A–Z |
| (ISSUE-025) — lista bez pokrewieństwa (v2.2) | 4 | karta: imię i nazwisko, pod spodem same lata |

## Decisions
- **D1 — sortowanie po nazwisku z literami** (D19: *„tak jest dobrze”*). Nazwisko grupuje rodziny. *Obali:* autor szuka
  częściej po pokoleniu albo bliskości — wtedy przełącznik sortowania.
- ~~**D2 — pokrewieństwo w liście** zamiast miejsca pochówku~~ — **obalone na stopie #1 ISSUE-025** (v2.2): „kto to dla
  mnie” to funkcja łączenia osób w drzewie, a przy wielu poziomach linia by się rozrastała. Lista: imię, nazwisko, lata.
  Miejsca pochówku też nie ma — „gdzie leży” jest w widoku osoby.
- **D3 — „Ja” na górze** — kotwica łańcuchów; tu autor ją widzi i poprawia (ustawienie w [[ustawienia]]).
- **D4 — „Ja” zaprasza przed wyborem i nazywa wybraną osobę po wyborze** (v2; ISSUE-022 D3 i odstępstwo 1, przegląd
  `ui`). Tekst z v1 („to Ty — od Ciebie liczą się łańcuchy”) nie mówił, że nikogo nie wybrano ani co zrobić (reguła 9),
  a po wyborze nigdzie nie było widać, kogo wybrano. Znak „Ja” w akcencie zostaje także przy wybranej osobie ze
  zdjęciem: ta karta jest kotwicą, a kogo wybrano, mówi linia pod spodem. W wierszu ustawień jest profilowe
  ([[ustawienia]] D7). *Obali:* autor szuka siebie po twarzy i nie rozpoznaje karty „Ja” — wtedy profilowe także tutaj.
- **D5 — bez nazwiska: nazwisko rodowe, a potem „Bez nazwiska”** (v2; ISSUE-022 odstępstwo 2, przegląd `ui`). Osoba,
  której znane jest tylko nazwisko rodowe („Maria z d. Wymyślona”), stoi pod jego literą: to jej rodzina (D1), a
  nagłówek „Bez nazwiska” nad kartą z „z d. …” przeczyłby sam sobie. Osoby bez obu nazwisk — na końcu, pod „Bez
  nazwiska”. *Obali:* autor szuka takich osób po nazwisku męża — wtedy pole nazwiska, a nie sortowanie.
- **D6 — wybór „ja” jako tryb wyboru** (v2; ISSUE-022 D3, odstępstwo 7, przegląd `ui`). Ta sama lista co w zakładce,
  żeby nie uczyć się drugiej; bez paska (reguła 12), bez chevronu (reguła 11 — chevron znaczy „prowadzi dalej”), ✓ przy
  obecnej osobie; bez automatycznego fokusu pola, bo wybór robi się raz, a lista ok. 100 osób przewija się szybciej, niż
  się pisze przy klawiaturze zakrywającej połowę ekranu. *Obali:* autor przy pierwszym wyborze zawsze wpisuje nazwisko —
  wtedy fokus od razu.
- **D7 — karta osoby → „Poprawa wpisu” do czasu widoku osoby** (v2; ISSUE-022 D2). Tymczasowe złamanie reguły 15 (widok
  przed poprawą), opisane w [[style-b]] reguła 15. [[ISSUE-024-person-view]] przepina kartę na [[osoba]].

- ~~**D8, D9** (v2.1 — nawias ze ścieżką, opis neutralny bez płci)~~ — wycofane z listą (v2.2); obie reguły przechodzą do
  widoku osoby ([[ISSUE-024-person-view]]).

## Open
brak.
