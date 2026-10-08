---
title: "ISSUE-022 — App skeleton: bottom bar Mapa · Osoby · Drzewo, the Osoby tab, settings under the gear"
type: issue
status: done
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: APPROVED
verdict-date: 2026-10-08
verdict-reviewer: self-check
source: "[[SPIKE-004-mvp-flow-prototype]] D1, D2, D3, D19, D23 (decyzje autora na prototypie, 2026-10-08)"
created: 2026-10-08
updated: 2026-10-08
---

# ISSUE-022 — Szkielet aplikacji: dolny pasek, zakładka Osoby, ustawienia

> Z zamknięcia [[SPIKE-004-mvp-flow-prototype]]. Pierwsza pozycja w drodze do instalacji MVP: na tym szkielecie stoją
> wszystkie ekrany, które przyjdą później.

## What to build
- **Dolny pasek Mapa · Osoby · Drzewo** ([[style-b]] reguła 12, v1.12; [[cmentarze]] element 18): widoczny na ekranach do
  oglądania, ukryty w formularzach, oknach, trybach wyboru i na zdjęciu na pełnym ekranie; zakładka, z której autor
  przyszedł, zostaje aktywna na całym stosie (SPIKE-004 D1, D2).
- **Zakładka Osoby** ([[osoby]] v1): wyszukiwarka osób, „Ja” na górze, lista A–Z po nazwisku. Pokrewieństwo pod imieniem
  przyjdzie z [[ISSUE-025-gender-kinship-together-since]] — do tego czasu sam rok życia (D19).
- **Koło zębate → ustawienia** ([[ustawienia]] v1, elementy 1–7): „Ja” (wybór osoby — ustawienie „ja” z [[data-model]]),
  kopia (dzisiejsze informacje i działania z „Stanu danych”), „Eksport dla rodziny” (ekran eksportu przyjdzie z
  [[US-006-eksport-dla-rodziny]]), notka przekazania, „Stan danych” o poziom niżej (D23).
- **Wyszukiwarka na mapie zostaje „Szukaj cmentarza”** (D3, [[cmentarze]] D27) — bez zmian w kodzie.

## Acceptance Criteria
- **AC-1** *Given* ekran główny *Then* na dole są zakładki Mapa · Osoby · Drzewo, aktywna Mapa; w formularzu osoby paska
  nie ma.
- **AC-2** *When* dotykam „Osoby” *Then* widzę „Ja” i wszystkie osoby A–Z po nazwisku; wpisanie „wymys” zostawia osoby
  o nazwisku Wymyślony/Wymyślona (bez polskich znaków, od początku słowa).
- **AC-3** *When* dotykam koło zębate *Then* widzę ustawienia; „Stan danych” otwiera dzisiejszy ekran.
- **AC-4** *When* wybieram w ustawieniach „Ja” *Then* wybrana osoba jest zapisana jako „ja” i stoi na górze zakładki Osoby.

## Notes
- **Zakładka Drzewo przed zbudowaniem drzewa** — do decyzji na stopie #1: zaślepka „Drzewo powstanie po SPIKE-002”
  albo dwie zakładki do czasu drzewa (reguła 12: pasek pojawia się przy dwóch celach).
- **Zmiana zakresu** zapisana w [[osoby]]: wyszukiwanie osób (brief §5a G5, Should) wchodzi do MVP decyzją autora.

## Implementation plan
> `planning`, 2026-10-08. Specyfikacje: [[osoby]] v1, [[ustawienia]] v1, [[cmentarze]] element 18, [[style-b]] reguły 11,
> 12, 15. Makieta: prototyp SPIKE-004, panele 5 i 9 (ścieżka w SPIKE-004), oraz warianty paska na stopie #1:
> `issue-022-pasek-warianty.html` w katalogu tymczasowym sesji (poza repo).

### Decisions for stop #1 (rekomendacja → „tak” przyjmuje wszystkie)
> **Stop #1, 2026-10-08: autor „Tak”** — D1 = A (trzy zakładki, zaślepki Drzewa i eksportu), D2–D4 jak niżej. AC-1 bez
> zmian (Mapa · Osoby · Drzewo).

- **D1 — wejścia do ekranów, których jeszcze nie ma** (zakładka Drzewo, wiersz „Eksport dla rodziny”). Kandydaci na
  makiecie: **A — trzy zakładki, Drzewo i Eksport prowadzą do zaślepki** z tekstem, kiedy powstaną · B — dwie zakładki
  i bez wiersza eksportu, dopóki nie ma ich ekranów. **Rekomendacja: A.** Pasek ma od razu kształt, który autor
  zatwierdził na prototypie (SPIKE-004 D1). Material Design zaleca pasek dolny dla 3–5 celów, a przy mniej niż trzech
  każe „rozważyć zakładki” (m1.material.io → *Bottom navigation*). Reguła 12 dopuszcza oba warianty. Koszt A: dwa ekrany
  zaślepek do usunięcia razem z drzewem i eksportem. *Obali:* autor dotyka „Drzewo” i odbiera to jako pusty przycisk,
  a nie zapowiedź → B.
  Zaślepki: „Drzewo powstanie po SPIKE-002. Na razie rodzinę widać przy osobie.” · „Eksport powstanie z US-006.”
- **D2 — karta osoby w zakładce Osoby prowadzi do „Poprawy wpisu”**, dopóki nie ma widoku osoby
  ([[ISSUE-024-person-view]]). To ta sama droga co chip krewnego w sekcji „Rodzina” (`loadPersonForCorrection` →
  `Correction`). Działa też dla osoby bez grobu. ISSUE-024 przepnie kartę na widok osoby.
- **D3 — „Ja”.** Gdy osoby „ja” nie wybrano, karta „Ja” w zakładce Osoby i wiersz „Ja” w ustawieniach otwierają wybór
  osoby: tryb wyboru bez paska, tytuł „Która osoba to Ty?”, wyszukiwarka i lista A–Z jak w zakładce. Gdy „ja” jest
  wybrane, karta „Ja” otwiera tę osobę (D2), a wiersz w ustawieniach otwiera wybór, żeby ją zmienić. Osoba „ja” nie
  powtarza się w liście A–Z (jak w prototypie), ale wyszukiwanie ją znajduje. **Dopisek do specyfikacji:** pod „Ja”
  stoi imię i nazwisko wybranej osoby, bo inaczej nigdzie nie widać, kogo wybrano. Do specyfikacji ([[osoby]] el. 3,
  [[ustawienia]] el. 1) dopisze to `ui` w przeglądzie ekranu.
- **D4 — „Notka przekazania” to krótki ekran z listą tego, co ma być na kartce** ([[ustawienia]] el. 6, D3; prototyp
  pokazywał tylko komunikat). Treść ogólna, z [[NT-007-hand-over-note]], bez danych rodziny:
  - że kopia istnieje;
  - gdzie są plik kopii i plik klucza (folder i nazwy plików);
  - hasło, **nie w tej samej chmurze**;
  - jak otworzyć kopię bez Grobing: `age` → `tar` → SQLite;
  - gdzie leży eksport dla rodziny;
  - że po „Skonfiguruj kopię od nowa” notkę trzeba wymienić.

### Scope — files (`{code}`)
| Plik | Co |
|---|---|
| `lib/app/tabs.dart` (nowy) | `AppTab` (map, people, tree); `GrobingTabBar` według [[cmentarze]] el. 18: 72 dp, powierzchnia, linia obrysu u góry, ikona nad podpisem 12 sp, aktywna w akcencie z podkreśleniem 2 dp, w semantyce stan „wybrana”. **Przełączenie:** mapa zawsze leży na dole stosu; zakładka zdejmuje stos do mapy i kładzie swój ekran główny bez wsuwania. Wstecz z ekranu głównego Osób wraca na mapę, a wstecz z mapy zamyka aplikację (Android, *Principles of navigation*: stały ekran startowy). „Stos zakładki od początku” jak w el. 18 |
| `lib/app/home/home_screen.dart` | pasek w `bottomNavigationBar` (arkusze stoją nad nim, el. 18); koło zębate → ustawienia zamiast „Stanu danych” |
| `lib/app/grave/cemetery_screen.dart`, `grave_screen.dart` | pasek z aktywną Mapą. Parametr zakładki dojdzie z ISSUE-024, gdy pojawi się druga droga do tych ekranów; bez niego teraz |
| `lib/data/people.dart` (nowy) | `watchPeople` (osoba, imiona, nazwisko, nazwisko rodowe, urodzenie, zgon, profilowe z kadrem) · `watchMe` / `setMe` — tabela `Settings` z v1 (`me_person_id`, wiersz `id = 1`, zapis jako upsert). **Bez zmiany schematu** |
| `lib/app/people/people_screen.dart` (nowy) | zakładka Osoby, elementy 1–5 i stany z [[osoby]]: liczba osób z odmianą, nagłówki liter, karta (reguła 11: profilowe 40 dp albo inicjały), pusto, brak wyników. Lata życia **same lata** („1926–2010”, „ur. 1955”, „ok. 1890–1951”), nowa funkcja obok `lifeLine` w `dates.dart` |
| `lib/app/people/me_picker_screen.dart` (nowy) | wybór „ja” (D3); lista wspólna z zakładką |
| `lib/app/polish.dart` | dopasowanie od początku słowa (imiona, nazwisko, nazwisko rodowe; bez polskich znaków i wielkości liter). To nie jest `matchesQuery`, bo ta funkcja obcina końcówki i szuka w środku słowa. Sortowanie po nazwisku, potem po imionach (`polishCompare`) |
| `lib/app/settings/settings_screen.dart` (nowy) | elementy 1–7 z [[ustawienia]]: sekcje, wiersze ≥ 56 dp; kopia (ostatnia udana, „Zrób kopię teraz”, stan nieskonfigurowany → „Skonfiguruj kopię”) przez istniejący `BackupService`. Opis ostatniej kopii z jednej wspólnej funkcji z „Stanem danych”, bez zmiany tamtego ekranu. „Odtwórz z kopii” i „Stan danych” → dzisiejszy ekran. Bez paska |
| `lib/app/settings/hand_over_note_screen.dart`, zaślepki D1 (nowe) | D4; zaślepka Drzewa (z paskiem, aktywne Drzewo) i eksportu (bez paska) |
| „O aplikacji” | wersja jako stała w kodzie, **bez nowej zależności**; test porównuje ją z `pubspec.yaml`. Podpisy: „Mapy: © autorzy OpenStreetMap (ODbL) · Natural Earth”. GUGiK dojdzie z ortofotomapą ([[US-007-mapa-cmentarza]]) |

Bez paska zostają: formularz osoby, arkusz rodziny, wybór osoby, wyszukiwarka cmentarzy, wskazanie punktu, zdjęcia
osoby, podgląd zdjęcia, kadr, ustawienia, „Stan danych”, odtworzenie, konfiguracja kopii (reguła 12). Wyszukiwarka na
mapie bez zmian (D3).

### AC → implementation → test (testy pisze `qa`)
| AC | Gdzie | Test happy-path |
|---|---|---|
| AC-1 (przy D1 = A: Mapa · Osoby · Drzewo; przy B: Mapa · Osoby) | `tabs.dart`, `home_screen.dart`, ekrany cmentarza i grobu | widżet: pasek na mapie z aktywną Mapą, na cmentarzu i grobie też; w formularzu osoby paska nie ma; Osoby → wstecz → mapa |
| AC-2 | `people_screen.dart`, `people.dart`, `polish.dart` | widżet: „Ja” na górze, kolejność A–Z z literami, „wymys” → tylko Wymyślony/Wymyślona; jednostkowe: dopasowanie od początku słowa (także nazwisko rodowe), polskie sortowanie |
| AC-3 | `settings_screen.dart` | widżet: koło zębate → ustawienia; „Stan danych” → dzisiejszy ekran |
| AC-4 | `me_picker_screen.dart`, `people.dart` | widżet: wybór → `settings.me_person_id`, osoba pod „Ja” w zakładce i znika z listy A–Z; danych: `setMe` / `watchMe` |
| D4, „O aplikacji” | ekrany ustawień | widżet: notka ma listę; wersja = `pubspec.yaml` |

### Data layer
- **Schemat bez zmian** (v6): tabela `Settings` jest od v1 i dopiero teraz ma pierwszy zapis. Migracji nie ma, więc
  testu migracji też nie.
- **Próbne odtworzenie:** test kopii i odtworzenia z ustawionym „ja” (ta sama osoba po odtworzeniu, odcisk zgodny). Na
  emulatorze: kopia z `Medium_Phone` z nowym hasłem testowym i odtworzenie na `Grobing_Restore` (agent).
- **Źródło i status faktu:** nie dotyczy, bo „ja” to ustawienie, a nie fakt o rodzinie (SPIKE-004 D28: aplikacja bez
  źródeł).
- Osoby nie da się usunąć w aplikacji, więc klucz obcy `me_person_id` nie ma osieroconego przypadku. Gdy usuwanie
  powstanie, ta pozycja jest prior artem.

### Manual verification
**Agent na emulatorze** (`Medium_Phone`, build release jako aktualizacja, wymyślone dane), zrzuty przed stopem #2:
1. Mapa: pasek, aktywna Mapa, arkusz cmentarza nad paskiem. Cmentarz i grób: pasek z aktywną Mapą. Formularz osoby,
   wyszukiwarka cmentarzy, wskazanie punktu: bez paska.
2. Osoby: „Ja”, litery, liczba; „wymys” → Wymyślony/Wymyślona; „xyz” → „Nie ma osoby „xyz”.”; karta → „Poprawa wpisu”;
   wstecz → ten sam tekst i to samo miejsce listy.
3. Przełączanie: Osoby → wstecz → mapa; „Mapa” z grobu → mapa Polski; zaślepki D1.
4. Koło zębate → ustawienia: kopia (stan, „Zrób kopię teraz”), „Stan danych”, „Odtwórz z kopii”, notka, „O aplikacji”.
5. „Ja” → wybór → zapisane (odczyt bazy: `settings.me_person_id`), na górze Osób z imieniem.
6. `uiautomator`: zakładki z nazwą, stanem „wybrana” i `clickable`; karty osób i wiersze ustawień `clickable`.
7. Próbne odtworzenie na `Grobing_Restore`: odcisk zgodny, „Ja” ta sama osoba.

**Autor: odczucie** (najwyżej 3):
1. Przełączanie Mapa ↔ Osoby i „wstecz”: czy zawsze wiesz, gdzie jesteś.
2. Znaleźć osobę kawałkiem nazwiska, otworzyć i wrócić: czy lista jest tam, gdzie ją zostawiłeś.
3. Koło zębate → „Ja” → wybierz siebie: czy ustawienia są tam, gdzie ich szukasz.

Przegląd ekranów `ui` (subagent `qa`) przed stopem #2; nowy ekran → `dev` przechodzi AC na emulatorze przed `qa`.

### Out of Scope
- Widok osoby i pochówek → mapa z pinezką ([[ISSUE-024-person-view]]); karta osoby do tego czasu → poprawa (D2).
- Pokrewieństwo w liście („babcia”) → [[ISSUE-025-gender-kinship-together-since]].
- Drzewo ([[SPIKE-002-tree-on-a-phone]]), ekran eksportu ([[US-006-eksport-dla-rodziny]]), podpis GUGiK ([[US-007-mapa-cmentarza]]).
- Pamięć osobnego stosu każdej zakładki (el. 18: stos od początku).
- Pierwszy start z prośbą o „ja” przy pierwszym łańcuchu ([[ustawienia]] el. 1) → z widokiem osoby albo drzewem.
- Mapa Polski jak R1 → [[ISSUE-023-poland-map-r1-cemetery-photo]].

## Dev report
> `dev`, 2026-10-08. Stop #1: „Tak” (D1 = A, D2–D4). Flutter 3.41.1 zgodny z przypiętym. `dart format` i `flutter analyze`:
> czyste. Schemat bez zmian (v6).

### What was built (`{code}`)
- **Pasek i zakładki:** `lib/app/tabs.dart` — `AppTab`, `openTab` (mapa zawsze pierwszą trasą; zakładka zdejmuje stos do
  mapy albo do swojego ekranu głównego i kładzie go bez wsuwania), `GrobingTabBar` (72 dp, linia obrysu u góry,
  aktywna w akcencie z podkreśleniem podpisu, `Semantics(selected)`). Pasek na mapie, cmentarzu i grobie (aktywna Mapa),
  w Osobach i na zaślepce Drzewa (`lib/app/tree/tree_placeholder_screen.dart`).
- **Osoby:** `lib/app/people/people_screen.dart` + `people_list.dart` (pole wyszukiwania, karta z profilowym albo
  inicjałami, polska kolejność po nazwisku, litery, „Nie ma osoby „…”.”), `me_picker_screen.dart` („Która osoba to Ty?”,
  wybrana z ✓ i `selected`). Dane: `lib/data/people.dart` (`loadPeople`/`watchPeople`, `watchMe`, `setMe` — upsert
  wiersza `settings.id = 1`). Lata życia: `lifeYears` w `dates.dart`; dopasowanie od początku słowa: `matchesWordStart`
  w `polish.dart` (dzieli też nazwiska z łącznikiem).
- **Ustawienia:** `lib/app/settings/settings_screen.dart` (elementy 1–7), `hand_over_note_screen.dart` (D4),
  `export_placeholder_screen.dart` (D1). Koło zębate na mapie → ustawienia. Wspólny pasek „wstecz + tytuł”:
  `lib/app/widgets/title_bar.dart`.
- **D2:** `openPersonEntry` w `person_form_screen.dart` — jedna droga do „Poprawy wpisu” spoza grobu; chip krewnego w
  `family_section.dart` używa jej zamiast własnej kopii (zachowanie bez zmian).
- **Token:** `GrobingColors.stateOk` `#8CC084` (propozycja z [[style-b]] *State colours*, v1.14) — stan kopii.

### Deviations (dla przeglądu `ui`)
1. **„Ja” wybrane** — pod „Ja” imię i nazwisko zamiast „to Ty — …” (D3). W ustawieniach: imię, a pod nim opis; ikona to
   profilowe osoby, gdy ma zdjęcie. Specyfikacje [[osoby]] el. 3 i [[ustawienia]] el. 1 do dopisania przez `ui`.
2. **Osoby bez nazwiska** — na końcu listy pod nagłówkiem „Bez nazwiska” (specyfikacja nie mówi).
3. **Miejsce kopii** — z dostawcy pliku wybranego w oknie zapisu: „Dysk Google”, „Pobrane”, „pamięć telefonu”; nieznany
   dostawca → nic, zamiast stałego „Dysk Google” z el. 2 (na emulatorze kopia idzie do Pobranych — pokazane
   „Pobrane”). Rozpoznanie Dysku po `com.google.android.apps.docs…` — niesprawdzone na urządzeniu w tej pozycji.
4. **Nieudana ostatnia kopia** (stanu nie ma w specyfikacji) — wiersz „Ostatnia kopia się nie udała”, `sync_problem` w
   kolorze błędu, komunikat i „Ostatnia udana: …”. W trakcie „Zrób kopię teraz”: wskaźnik zamiast ikony i „Robię kopię…”.
5. **„Odtwórz z kopii” → „Stan danych”**, jak w el. 4 — tam jeszcze raz „Odtwórz z kopii”. Dwa dotknięcia tego samego
   napisu; kandydat dla `ui`: wiersz otwiera od razu ekran odtworzenia.
6. Ikona „Stanu danych”: `storage_outlined` (Flutter nie ma `database`). Linie podziału w kolorze obrysu (prototyp: 40%).
7. Pole „Szukaj osoby” ma „Wyczyść” (×) jak wyszukiwarka cmentarzy; wybór „ja” bez autofokusu pola.
8. Plan: „opis ostatniej kopii z jednej funkcji ze „Stanem danych”” — **nie zrobione**: ustawienia mówią „dziś, 11:42”,
   „Stan danych” zostaje techniczny (`2026-10-08 11:42`), bez zmiany tamtego ekranu.
9. Wersja: stała `appVersion = '1.0.0'` w `settings_screen.dart` — test z `pubspec.yaml` pisze `qa`.

### Emulator pass (R5) — `Medium_Phone`, build release wgrany na istniejące dane (`install -r`)
| AC | Wynik |
|---|---|
| AC-1 | mapa: pasek, Mapa `selected`; arkusz cmentarza nad paskiem; cmentarz i grób z paskiem; „Poprawa wpisu” bez paska; „Mapa” z grobu → mapa Polski; Osoby/Drzewo → wstecz → mapa; zaślepka Drzewa |
| AC-2 | „7 osób”, „Ja” na górze, W, „Bez nazwiska”; „wymys” → 6 osób Wymyslona/Wymyslony; „zmys” → osoba z d. Zmyslona; „xyz” → „Nie ma osoby „xyz”.”; klawiatura bez wielkiej litery, zakrywa pasek |
| AC-3 | koło zębate → ustawienia (bez paska); „Stan danych” → dzisiejszy ekran („Ustawienia 1” po wyborze „ja”); „Zrób kopię teraz” → „dziś, 16:46 · Pobrane”; notka, zaślepka eksportu |
| AC-4 | „Ja” → wybór → Ewa → wiersz z profilowym i imieniem; Osoby: „Ja / Ewa Wymyslona” na górze, Ewa nie powtarza się w A–Z; karta „Ja” → jej „Poprawa wpisu” |

**Błąd znaleziony na emulatorze i poprawiony:** po powrocie z wpisu osoby wracała klawiatura — pole wyszukiwania
odzyskiwało fokus, bo zakres trasy pamięta ostatnie pole (`FocusScope.unfocus()` tego nie czyści). Teraz przed
otwarciem osoby odfokusowane jest samo pole, a przewinięcie listy chowa klawiaturę. Sprawdzone: po powrocie klawiatury
nie ma, tekst „zof” zostaje, lista w tym samym miejscu (te same współrzędne kart).

### For `qa`
- **4 istniejące testy padają z powodu zmiany drogi** (zamierzonej, AC-3): `home_screen_test.dart` „AC-5 … the gear opens
  „Stan danych”” i trzy w `restore_screen_test.dart` (`pumpApp`: koło zębate → „Odtwórz z kopii” czeka na
  `RestoreScreen`, a teraz trafia do ustawień → „Stan danych”). Reszta: 458 zielonych (przebieg przed poprawką fokusu).
- Kroki ręczne: *Implementation plan* → *Manual verification* (agent: 1–7, autor: 3 kroki odczucia). Kroki 1–6 przeszły
  w tym przejściu; krok 7 (próbne odtworzenie na `Grobing_Restore`) zostaje dla `qa`.
- Zrzuty: katalog tymczasowy sesji, `shots/` (poza repo).

## Verification
> `qa`, 2026-10-08. Rytuał WZ-024: `dart format` → `flutter analyze` (czysto) → `flutter test` (**481 zielonych**) → kroki
> agenta na emulatorze → przegląd `ui` → poprawki → stop #2.

### Tests (happy path per AC)
| AC | Test |
|---|---|
| AC-1 | `test/app/skeleton_test.dart` → *AC-1*: pasek na mapie z aktywną Mapą (`isSemantics(isSelected, isButton, hasTapAction)`), Osoby i Drzewo otwierają swoje ekrany, wstecz → mapa, „Mapa” z cmentarza → mapa Polski; widok grobu z paskiem, „Poprawa wpisu” bez paska |
| AC-2 | *AC-2*: „Ja” na górze, A–Z po nazwisku w polskiej kolejności (L przed Ł, nazwisko rodowe zamiast braku nazwiska, „Bez nazwiska” na końcu), liczba osób, „wymys”, „LIS” (także z d.), „xyz” → „Nie ma osoby „xyz”.”; D2 — karta → „Poprawa wpisu”, wstecz z tym samym tekstem; pusta baza. Jednostkowe: `matchesWordStart` (`polish_test.dart`), `lifeYears` (`dates_test.dart`), `loadPeople`/`watchPeople` (`test/data/people_test.dart`) |
| AC-3 | *AC-3*: sekcje i wiersze ustawień, notka (D4), zaślepka eksportu (D1), „Stan danych”; kopia ustawiona (zieleń stanu, „dziś, … (w tle) · Dysk Google”) i nieudana (ikona błędu, „ — komunikat”, „Ostatnia udana: …”); `home_screen_test.dart` AC-5: koło zębate → ustawienia → „Stan danych”; `restore_screen_test.dart`: ustawienia → „Odtwórz z kopii” → ekran odtworzenia; `settings_words_test.dart`: `backupWhen`, `backupPlace`, wersja = `pubspec.yaml` |
| AC-4 | *AC-4*: ustawienia → „Ja” → wybór → zapis w `settings`, imię w wierszu i w karcie „Ja”, osoba nie powtarza się w A–Z, wyszukiwanie ją znajduje, w wyborze ✓ bez chevronów; „Ja” niewybrane w Osobach otwiera wybór. Danych: `setMe`/`watchMe` (jeden wiersz `id = 1`, zmiana, klucz obcy) |

### Data layer
- **Schemat bez zmian (v6)** — migracji nie ma, testu migracji też nie (DoD: tylko przy zmianie schematu).
- **Próbne odtworzenie — przeszło** (agent, kroki 7 z planu):
  - test: `restore_service_test.dart` → end to end — źródło z wybranym „ja”, po odtworzeniu ta sama osoba;
  - emulator: na `Medium_Phone` „Skonfiguruj kopię od nowa” z **nowym hasłem testowym**, kopia do Pobranych (`grobing-klucz-022.age`, `grobing-kopia-022.age`, wymyślone dane), odcisk źródła `96cf576af7e2ee9d`; pliki przeniesione `adb` na `Grobing_Restore`, tam z ustawień „Odtwórz z kopii” → „Zastąp dane” → **odcisk `96cf576af7e2ee9d` — zgodny**, w Osobach „Ja / Ewa Wymyslona”.
- **Źródło i status faktu:** nie dotyczy — „ja” to ustawienie (SPIKE-004 D28).

### Family data
- W zmianach nie ma baz, kopii, eksportów ani zdjęć: kopie `*-022.age` leżą w katalogu tymczasowym sesji i w Pobranych emulatorów, poza repo.
- **Strażnik treści odmówił na suchym przebiegu** (`polish.dart:84`, `polish_test.dart:115`, linia 18 listy): przykładowe nazwiska w komentarzu i teście dopasowania. Zastąpione wymyślonymi („Zmyślonek”, „Przezmyślonek”, „Testowski”), drugi suchy przebieg po 26 plikach kodu: przepuszcza. Dane testowe: Wymyślona/Wymyślony, Testowa, Lis, Łukasik, Nowak, Zmyślona — wymyślone.

### Agent on the emulator (`Medium_Phone`, build release jako aktualizacja) — kroki 1–7 z planu
Zrzuty: katalog tymczasowy sesji, `shots/01…25` (poza repo).
1. ✅ Pasek na mapie, cmentarzu i grobie (Mapa `selected`); arkusz nad paskiem; formularz osoby, ustawienia, wybór „ja”, notka bez paska.
2. ✅ Osoby: „7 osób”, „Ja”, litery; „wymys”, „zmys”, „xyz”; karta → „Poprawa wpisu”; wstecz — ten sam tekst i to samo miejsce listy, **bez klawiatury** (błąd znaleziony przez `dev` na emulatorze i poprawiony — *Dev report*).
3. ✅ Osoby/Drzewo → wstecz → mapa; „Mapa” z grobu → mapa Polski; zaślepka Drzewa.
4. ✅ Ustawienia: „Zrób kopię teraz” → „dziś, 16:46 · Pobrane”; notka; zaślepka eksportu; „Stan danych”; po przeglądzie: „Odtwórz z kopii” → od razu ekran odtworzenia.
5. ✅ „Ja” → Ewa → wiersz z profilowym i imieniem, karta „Ja / Ewa Wymyslona”, „Ustawienia 1” w „Stanie danych”.
6. ✅ `uiautomator`: zakładki `clickable` + `selected`; karty osób i wiersze ustawień `clickable`.
7. ✅ Próbne odtworzenie na `Grobing_Restore` — wyżej.

### ui review (subagent, przed stopem #2)
0 BLOCKER · **1 MAJOR** · 13 MINOR (9 odstępstw z *Dev report* + B1–B10).
- **MAJOR (odstępstwo 5)** — „Odtwórz z kopii” prowadziło przez „Stan danych” do drugiego „Odtwórz z kopii” pod „Skonfiguruj kopię od nowa” → **poprawione**: wiersz otwiera od razu ekran odtworzenia.
- **Poprawione przed stopem:** profilowe w wierszu „Ja” 40 dp (1) · kolejność i litera po nazwisku rodowym, gdy nie ma nazwiska (2) · „dziś, 11:42 — komunikat” i przygaszone wiersze w trakcie kopii (4) · przed wyborem „Wybierz, która osoba to Ty” (B1) · wybór bez chevronów (B2) · numery notki w kolorze tekstu pomocniczego (B3) · „Bez niej rodzina nie otworzy kopii.” (B4) · margines 16 dp (B7) · `liveRegion` stanu kopii (B8).
- **Przyjęte:** 3, 6, 7, 8, 9; B9 (zaślepki tymczasowe), B10 (podpis zakładki 12 sp jak w Material 3 — wyjątek do wytycznych).
- **Nie w tej pozycji:** B5 — twarde spacje po jednoliterowych słowach i w „z d.” w całej aplikacji (`personName`) → kandydat na osobną drobną pozycję; B6 — „Stan danych” mówi „Zapisana w Dysku na telefonie” także przy Pobranych (poza zakresem: tamten ekran bez zmian).
- **Specyfikacje zaktualizowane przez `ui`** (w tej paczce, według stanu kodu po poprawkach): [[osoby]] v2 (el. 2–4,
  nowe el. 6–7 „Która osoba to Ty?”, D4–D7) · [[ustawienia]] v2 („Odtwórz z kopii” od razu do odtworzenia, stany kopii,
  el. 6a notka, D4–D9) · [[cmentarze]] v2.5 (el. 18 zbudowany, koło zębate → ustawienia, D31) · [[style-b]] v1.17
  (`stateOk` w kodzie, wyjątek 12 sp, akcent nigdy jako numer listy, reguła 6 — twarda spacja z adnotacją „kod jeszcze
  nie stosuje”). Bez nowych plików i folderów — DOC_MAP bez zmian.

### Stop #2 — autor
**„ok” (autor, 2026-10-08)** — kroki 1–3 odczucia (przełączanie zakładek, szukanie z powrotem do listy, ustawienia i
„Ja”). Sprawdzone na urządzeniu: „Ja” zmienione przez autora z Ewy na „Jozef z d. Testowy”, Ewa wróciła do listy A–Z —
krok 3 wykonany. Kroki 1–2 nie zostawiają śladu.

### Verdict
**APPROVED** (self-check, z uwagami). Każde AC ma test happy-path i przeszło na emulatorze; warstwa danych: schemat bez
zmian, próbne odtworzenie zgodne; dane rodziny: strażnik treści przepuszcza paczkę kodu po poprawce przykładów.
Uwagi:
- rozpoznanie „Dysk Google” w wierszu kopii (`backupPlace`) sprawdzone tylko testem — na emulatorach kopia idzie do
  Pobranych; pierwszy prawdziwy telefon przy MVP;
- B5 (twarde spacje w całej aplikacji) i B6 („Stan danych” o Dysku przy Pobranych) — poza tą pozycją;
- zaślepki Drzewa i eksportu (D1 = A) do usunięcia z SPIKE-002 i US-006;
- self-check `qa` ma tę samą ślepą plamkę co `dev`: werdykt opiera się na testach, przeglądzie `ui` i trzech krokach
  autora; czego nikt nie sprawdził — TalkBack na żywo (sprawdzone `uiautomator` i testy semantyki), duże powiększenie
  tekstu na ekranach Osób i ustawień.

### Package for `docs` (lista jawna, R1)
- **grobing-code** (26): `lib/app/dates.dart` · `lib/app/family/family_section.dart` · `lib/app/grave/cemetery_screen.dart` ·
  `lib/app/grave/grave_screen.dart` · `lib/app/grave/person_form_screen.dart` · `lib/app/home/home_screen.dart` ·
  `lib/app/polish.dart` · `lib/app/theme.dart` · `lib/app/tabs.dart` · `lib/app/people/me_picker_screen.dart` ·
  `lib/app/people/people_list.dart` · `lib/app/people/people_screen.dart` · `lib/app/settings/export_placeholder_screen.dart` ·
  `lib/app/settings/hand_over_note_screen.dart` · `lib/app/settings/settings_screen.dart` ·
  `lib/app/tree/tree_placeholder_screen.dart` · `lib/app/widgets/title_bar.dart` · `lib/data/people.dart` ·
  `test/app/dates_test.dart` · `test/app/home/home_screen_test.dart` · `test/app/polish_test.dart` ·
  `test/app/restore_screen_test.dart` · `test/app/settings/settings_words_test.dart` · `test/app/skeleton_test.dart` ·
  `test/backup/restore_service_test.dart` · `test/data/people_test.dart`
- **grobing-vault**: `backlog/issues/ISSUE-022-app-skeleton-tabs-people-settings.md` · `00_START_HERE/TRACEABILITY.md` ·
  `05_DESIGN/osoby.md` · `05_DESIGN/ustawienia.md` · `05_DESIGN/cmentarze.md` · `05_DESIGN/brand/style-b.md` + zamknięcie
  `docs` (`CURRENT_STATE.md`).
- **grobing-agents**: nic.
- Poza repo (nie wchodzi): zrzuty `shots/`, makieta wariantów paska, kopie `*-022.age` w katalogu tymczasowym sesji i w
  Pobranych obu emulatorów.

**Dla autora (do zamknięcia):** na `Medium_Phone` kopia jest skonfigurowana od nowa — hasło testowe, Pobrane
(`grobing-klucz-022.age`, `grobing-kopia-022.age`, wymyślone dane); `Grobing_Restore` ma dane z tej kopii.
