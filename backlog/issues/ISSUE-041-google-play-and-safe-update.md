---
title: "ISSUE-041 — Google Play internal testing and a safe update path (store, signing, version code, backup before update)"
type: issue
status: ready
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "`/pm` 2026-10-16 — pytanie autora „czy nie stracę swoich danych przy aktualizacji?” i decyzja „tak zróbmy to” (Google Play, testy wewnętrzne, klucz od Google) · [[NT-005-distribution-decision]] · [[2026-10-16-retro-04]] → *Product decisions*"
created: 2026-10-16
updated: 2026-10-16
---

# ISSUE-041 — Google Play i bezpieczna aktualizacja

> Autor w `/pm`: *„Będę je chciał wprowadzić do mojej istniejącej na telefonie aplikacji — jak to zadziała? Czy nie stracę swoich danych?
> (…) We Friendsheet podoba mi się to, że mogę po prostu zaktualizować to z poziomu sklepu”*. Decyzja: **Google Play, ścieżka testów
> wewnętrznych, autor jedynym testerem, klucz podpisu generuje Google** — jak w Friendsheet. **Pierwsza pozycja kolejki** przed instalacją
> (najpóźniej 2026-10-29): każda następna funkcja przyjdzie na telefon tą drogą.

## Why
Android zachowuje dane przy aktualizacji, gdy zgadzają się trzy rzeczy: **nazwa pakietu** (`com.grobing.app`, niezmienna —
`project-config.example.md`), **klucz podpisu** i **wyższy numer wersji** (`versionCode`). Pierwsza instalacja z prawdziwymi danymi ustala
je na stałe; zmiana kanału po fakcie = odinstalowanie, czyli skasowana baza i odtworzenie z kopii. Trzecie ryzyko to zła migracja — przed
nią chronią testy (NFR-003) i kopia, która dziś jest **jedna i nadpisywana** (`backup-format.md` → *Known limits*).

## What to build
1. **Wpis aplikacji w Play Console** (konto autora, to samo co Friendsheet), ścieżka testów wewnętrznych, autor jedynym testerem. **Play App
   Signing z kluczem wygenerowanym przez Google**; obecny klucz wydania (`release_keystore_dir`) zostaje **kluczem przesyłania**. Czynności w
   konsoli wykonuje **autor** — agent podaje kroki, nie klika w zewnętrznych serwisach. Formularze konsoli (np. bezpieczeństwo danych, polityka
   prywatności) — sprawdzić przy planie, co wymaga ścieżka testów wewnętrznych.
2. **Paczka `flutter build appbundle`** zamiast APK `--split-per-abi` i **numeracja wersji**: `version` w `pubspec.yaml` rośnie przy każdym
   wydaniu. Pułapka: APK `--split-per-abi` dostaje na arm64 numer 2001 (na emulatorze x86_64 widać 4001), paczka sklepu 1, 2, 3… — **kanałów
   się nie miesza**.
3. **Kopia sprzed aktualizacji.** Najpierw najtańszy sprawdzian: czy Dysk trzyma poprzednią wersję nadpisanego pliku (`backup-format.md` →
   *Known limits*, „niesprawdzone”). Jeśli nie — mechanizm, który przy pierwszym starcie nowej wersji, przed migracją, zachowuje kopię
   poprzedniej (kształt do decyzji przy planie; odtworzenie musi ją przyjąć — ADR-004 pkt 5).
4. **Opis wydania w README `grobing-code`** (jedno miejsce): podbicie numeru → paczka → sprawdzenie w „Stanie danych”, że kopia jest świeża →
   wysyłka przez autora w Play Console → po aktualizacji: migracja, kopia.
5. **Próba generalna na telefonie autora** (Motorola moto g82 5G, Android 13 — [[2026-10-16-retro-04]] → fakt 1): wersja N ze sklepu na
   **wymyślonych** danych → wersja N+1 ze sklepu → dane i kopia bez zmian. To pierwszy wiersz listy A w [[ISSUE-032-mvp-install]] →
   *Hand checks*.
6. **ADR-019 — dystrybucja** (≥3 opcje: sklep + klucz Google · sklep + własny klucz przez PEPK · APK bezpośrednio) — zamyka
   [[NT-005-distribution-decision]]. Pisze łańcuch `planning` → `docs` (`CLAUDE.md` → *Na sygnał*).

## Acceptance Criteria
- **AC-1** *Given* aplikacja zainstalowana ze sklepu z wymyślonymi danymi *When* autor instaluje ze sklepu nowszą wersję *Then* dane są
  nienaruszone (liczby wierszy i odcisk kopii jak przed aktualizacją), a kopia w tle przechodzi.
- **AC-2** *Given* nowa wersja zmienia schemat *When* migracja zepsuje dane albo aktualizacja się przerwie *Then* istnieje kopia sprzed
  aktualizacji i odtworzenie ją przyjmuje.
- **AC-3** *Given* README `grobing-code` *When* agent przygotowuje wydanie *Then* wszystkie kroki (numer, paczka, kopia, wysyłka, sprawdzenie
  po aktualizacji) są w jednym miejscu, a te w Play Console są opisane jako kroki autora.

## Notes
- Prior art: [Sign your app](https://developer.android.com/studio/publish/app-signing) — klucz podpisu nie zmienia się przez całe życie
  aplikacji; [Play App Signing](https://support.google.com/googleplay/android-developer/answer/9842756) — klucz od Google albo własny; Friendsheet
  (`Friendsheet-App/docs/BACKLOG.md`): Play App Signing, reset klucza przesyłania 2026-03-18, a APK zbudowany lokalnie ma inny podpis niż wersja
  ze sklepu (TASK-133). Limity testów wewnętrznych (do 100 testerów, bez przeglądu) — ze źródeł pobocznych, sprawdzić w Play Console.
- **Skutek dla [[ISSUE-032-mvp-install]]:** instalacja **ze sklepu**, nie `adb install`; pytanie o klucz wydania z retro 1–3 traci wagę
  (klucz przesyłania da się zresetować).
- **Dane rodziny:** sklep dostarcza kod, bazy nie widzi; [[NFR-005-dane-nie-opuszczaja-telefonu]] bez zmian.
- W trakcie wyjazdu na Wszystkie Święte **żadnych aktualizacji** ([[2026-10-16-retro-04]] → *Product decisions*).
