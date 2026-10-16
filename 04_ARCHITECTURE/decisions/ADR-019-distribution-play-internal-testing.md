---
title: "ADR-019 — Distribution: Google Play internal testing with a Google-generated signing key; a database snapshot before every schema update"
type: adr
status: accepted
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-041-google-play-and-safe-update]]"
source: "decyzja autora 2026-10-16 w `/pm` („tak zróbmy to” — Google Play, testy wewnętrzne, klucz od Google, jak Friendsheet) i na stopie #1 ISSUE-041 („tak” — K3) · [[NT-005-distribution-decision]] · Android „Sign your app” · Play Console Help „Play App Signing”, „internal testing”"
created: 2026-10-16
updated: 2026-10-16
---

# ADR-019 — Dystrybucja: Google Play, testy wewnętrzne; migawka bazy przed aktualizacją schematu

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-16, decyzja autora w `/pm` (pytanie „czy nie stracę danych przy aktualizacji?”) i na stopie #1
[[ISSUE-041-google-play-and-safe-update]]. Zamyka [[NT-005-distribution-decision]]. Numer ADR-005, zarezerwowany na dystrybucję w briefie,
zajął wcześniej [[ADR-005-sqlite-package]].

## Context
Po instalacji MVP na telefonie autora są **prawdziwe dane rodziny**, a aplikacja będzie się dalej zmieniać (miejsca zamieszkania, wieńce,
mapa migracji — [[2026-10-16-retro-04]] → *Product decisions*). Android zachowuje dane przy aktualizacji tylko wtedy, gdy nowa wersja ma
**tę samą nazwę pakietu, ten sam klucz podpisu i wyższy numer wersji** — inaczej wymaga odinstalowania, a to kasuje bazę
([Sign your app](https://developer.android.com/studio/publish/app-signing): *„the signing key never changes during the lifetime of your app”*).
Pierwsza instalacja z danymi ustala więc kanał na stałe. Autor zna z Friendsheet aktualizację ze sklepu i chce jej tutaj; ma konto
deweloperskie Google Play.

Trzecie ryzyko to zła migracja w nowej wersji: przerwaną chroni jedna transakcja ([[NFR-003-migracje-schematu]]), ale start zamawia kopię zaraz
po migracji (retro 1, R6), a kopia nadpisuje **jedyny plik** (`backup-format.md` → *Known limits*) — po złej migracji dobra kopia znika.

## Decision
1. **Kanał: Google Play, ścieżka testów wewnętrznych**, autor jedynym testerem, konto to samo co przy Friendsheet. Aplikacja nie jest publiczna;
   wpis w sklepie jest tymczasowy. Na telefon **nic poza sklepem** — APK z tego repo ma inny podpis i numer wersji.
2. **Play App Signing z kluczem wygenerowanym przez Google.** Obecny klucz wydania (`release_keystore_dir`) zostaje **kluczem przesyłania** —
   zgubiony da się zresetować w Play Console bez zmiany podpisu aplikacji na telefonie.
3. **Numer wersji** rośnie przy każdej wysyłce (`pubspec.yaml`); nazwa `0.9.x` do instalacji z prawdziwymi danymi, `1.0.0` na instalację.
4. **Migawka bazy przed aktualizacją schematu** (K3): zanim nowa wersja przeniesie bazę na nowszy schemat, start zapisuje jej spójną kopię w
   starej wersji w prywatnym katalogu aplikacji (`pre-update/grobing-v<stara>.db`, 3 najnowsze; `lib/data/pre_update_snapshot.dart`). Droga
   powrotu przy złej migracji: wersja z poprawką wraca do migawki (README `grobing-code` → *Wydanie*).

## Options considered

| Option | Pros | Cons | Why (not) chosen |
|---|---|---|---|
| **Google Play, testy wewnętrzne, klucz Google** | aktualizacja jednym dotknięciem (jak Friendsheet); klucz podpisu przechowuje Google, klucz przesyłania da się zresetować; do 100 testerów, bez przeglądu, wersja w kilka minut; ścieżka zwolniona z sekcji „Bezpieczeństwo danych” ([Play Console Help](https://support.google.com/googleplay/android-developer/answer/9845334)) | APK zbudowany lokalnie nie zaktualizuje wersji ze sklepu (inny podpis — jak w Friendsheet, TASK-133); każda wysyłka to kilka kliknięć autora; Google wie, że aplikacja istnieje | **chosen** (decyzja autora) |
| Google Play z własnym kluczem (PEPK) | sklep i APK z PC aktualizują się nawzajem | klucz podpisu zostaje w rękach autora — zgubiony = koniec aktualizacji; więcej kroków przy zakładaniu | instalacja z PC nie jest potrzebna; zysk z klucza u Google przeważa |
| APK bezpośrednio (plik albo `adb install`) | zero konfiguracji, bez Google | bez przycisku „Aktualizuj”; klucz tylko u autora; pomyłka podpisu albo numeru wersji (`--split-per-abi` daje 2001) = odinstalowanie | autor chce aktualizacji ze sklepu |
| Kopia sprzed aktualizacji: historia wersji Dysku (K1) / drugi pełny plik w Pobranych (K2) | K1 bez kodu; K2 widoczny w „Odtwórz z kopii” | K1 niesprawdzone, ok. 30 dni, tylko przy Dysku; K2 — pełna kopia ze zdjęciami (rząd 0,2 GB) przy pierwszym starcie | K3: migawka samej bazy, bo migracje zmieniają wiersze, nie zdjęcia — kilka MB, ułamek sekundy, autor nic nie robi |

## Consequences
- **Positive:**
  - aktualizacja nie kasuje danych, o ile idzie ze sklepu; zła migracja ma drogę powrotu bez udziału autora;
  - pytanie o kopię klucza wydania (retro 1–3) traci wagę — to klucz przesyłania;
  - [[NFR-005-dane-nie-opuszczaja-telefonu]] bez zmian: sklep dostarcza kod i nie widzi bazy; migawka leży w prywatnym katalogu, poza kopią.
- **Negative / trade-offs:**
  - **żadnego APK na telefon** — także na próbę; buildy z PC tylko na emulatory;
  - zmiany wpisane po złej aktualizacji, a przed poprawką, giną przy powrocie do migawki — po aktualizacji ze zmianą schematu najpierw
    sprawdzić dane;
  - migawka nie chroni przed utratą telefonu w trakcie aktualizacji — to robi zwykła kopia;
  - [[DEF-002-full-l1-review]]: ścieżka wewnętrzna z jednym testerem to nie „druga osoba / sklep publiczny” — warunek obudzenia nie zachodzi.
- **Follow-ups:**
  - 2026-10-16 — część w sklepie (wpis w Play Console, instalacja z odtworzeniem wymyślonej rodziny, aktualizacja ze sklepu — AC-1
    ISSUE-041) przeniesiona decyzją autora do [[ISSUE-032-mvp-install]] → *Before install* 0: najpierw funkcje z kolejki, potem sklep. Nazwa
    pakietu `com.grobing.app` w sklepie — niesprawdzona do pierwszej wysyłki;
  - pierwsza prawdziwa migracja przez sklep — wiersz listy A w [[ISSUE-032-mvp-install]].
