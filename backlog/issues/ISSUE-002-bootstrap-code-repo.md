---
title: "ISSUE-002 — Bootstrap grobing-code (fresh Flutter project, pinned SDK, no Firebase)"
type: issue
status: in-progress
delivery-style: task-level
priority: MUST
ideal_days: 0.5
quality-verdict: APPROVED
verdict-date: 2026-10-05
verdict-reviewer: self-check
created: 2026-10-05
updated: 2026-10-05
---

# ISSUE-002 — Bootstrap grobing-code

## Scope
Świeży projekt Flutter w `grobing-code` na przypiętej wersji SDK, uruchamiający się na emulatorze i
telefonie autora jako pusty ekran startowy w stylu B — fundament pod wszystkie kolejne zadania.

## Acceptance Criteria
- [ ] `flutter create` w `grobing-code` (platforma: **android**), na wersji z
      `project-config.example.md` (`flutter_version_pinned`). **Globalny Flutter nie jest
      aktualizowany** — współdzieli go wydana aplikacja autora.
- [ ] Wersja przypięta per projekt (menedżer wersji albo zapis + sprawdzenie) — jeden sposób, opisany
      w README repo.
- [ ] Nazwa pakietu ustalona z autorem i wpisana **wyłącznie** w `project-config.example.md`
      (`android_package`).
- [ ] Domyślny `.gitignore` Fluttera **dołączony pod** istniejący blok (dane rodziny + sekrety
      zostają na górze).
- [ ] **Brak Firebase** i jakichkolwiek SDK wysyłających dane z telefonu.
- [ ] Lints/`analysis_options.yaml` jak we wcześniejszej aplikacji autora (wzorzec, nie kopia pliku).
- [ ] Własny keystore wydania **poza drzewem projektu**, ścieżka w lokalnym `project-config.md`
      (`release_keystore_dir`); w repo nic.
- [ ] `flutter analyze` i `flutter test` przechodzą; aplikacja startuje na telefonie z ciemnym ekranem
      startowym (styl B).

## Out of Scope
- Model danych, ekrany, mapy — kolejne zadania i spike'i.
- Wybór dostawcy map (SPIKE-001), mechanizmu kopii (SPIKE-003).

## Technical Notes
- **Nie kopiuj folderu innej aplikacji jako szablonu** — przeniósłby jej konfigurację; start od świeżego
  `flutter create`.
- Decyzja o sposobie przypięcia wersji → wpis do ADR-002 (ISSUE-001 AC-4).

## Implementation plan
> `planning`, 2026-10-05. Pozycja nie dotyka warstwy danych, więc test migracji, próbne odtworzenie z
> kopii i źródło faktu nie mają tu zastosowania. **DoR:** to pozycja startowa z kick-offu bez kroku
> ścieżki i bez US, tak jak ISSUE-001. Dlatego nie ma wiersza w `TRACEABILITY.md`; wpisanie jej do
> któregoś kroku byłoby zapychaniem luki.

### Decisions for stop #1
| # | Decyzja | Rekomendacja | Dlaczego |
|---|---|---|---|
| D1 | **Nazwa pakietu** (`applicationId`) — **nieodwracalna**: inna nazwa albo inny klucz to dla Androida inna aplikacja, aktualizacja się nie zainstaluje, a baza lokalna nie przejdzie ([Sign your app](https://developer.android.com/studio/publish/app-signing)) | ✅ **`com.grobing.app`** — decyzja autora na stopie #1 (2026-10-05); wzorzec Friendsheet (`com.friendsheet.app`). Rekomendacją było `io.github.aleksanderginalski.grobing` | odrzucona alternatywa: domena, którą autor kontroluje, wykluczałaby kolizję w Play. Autor wybrał własny wzorzec; ryzyko kolizji istnieje tylko przy publikacji w Play (NT-005 otwarte) |
| D2 | **Przypięcie wersji Fluttera** | `pubspec.yaml` → `environment: flutter: 3.41.1` (dokładna wersja). Zapis wartości zostaje w `project-config.example.md`, a sprawdza ją `pubspec` | **zmierzone 2026-10-05** (próba w scratchpadzie): `pub get` przechodzi na 3.41.1 i **odmawia** na `3.42.0` oraz na `>=3.40.0 <3.41.0`. Każde `run`/`test`/`build` sprawdza wersję bez nowego narzędzia i bez drugiej kopii SDK. **Czego nie da:** dwóch wersji obok siebie. Gdy Friendsheet będzie potrzebował nowszego Fluttera, Grobing przestanie się budować i wtedy trzeba będzie albo podbić wersję (nowa linia w ADR-002), albo dołożyć FVM. Generalizujemy z przypadku, nie przed nim |
| D3 | **Miejsce keystore wydania** | `C:\Users\user\.keystores\grobing\` (poza `C:\Programowanie`, gdzie leżą wszystkie drzewa projektów); ścieżka w lokalnym `project-config.md` → `release_keystore_dir` | Klucz tworzy **autor sam** (`keytool` pyta o hasła), żeby hasła nigdy nie przeszły przez sesję. **Plus:** kopia keystore w zaszyfrowanym miejscu autora (tak jak NT-001), bo utrata klucza oznacza, że aktualizacja nie wejdzie na telefon bez odinstalowania, a odinstalowanie kasuje bazę |

### Scope diff vs the item (to accept at stop #1)
- **+ podpis wydania w Gradle** z `android/key.properties` (gitignorowany, leży już w bloku sekretów).
  Build `release` **bez** tego pliku kończy się głośnym błędem i **nie** przechodzi po cichu na klucz
  debug. Wynika z AC-7.
- **+ ciemne tło natywnego ekranu startu** (`launch_background`, `styles` w `values`/`values-night`),
  żeby przed pierwszą klatką Fluttera nie mignęła biel. Wynika z AC-8 „ciemny ekran startowy".
- **+ reguła w README:** na telefonie z prawdziwymi danymi instalujemy **tylko build release**. Zmiana
  podpisu z debug na release wymaga odinstalowania, a ono kasuje bazę.
- **+ `root_widget: GrobingApp`** w *Product invariants* `project-config.example.md` (wzorzec
  „Project Identity" z briefu → *Reuse*, obok `android_package`).
- **+ ręczna kopia keystore** (autor, poza sesją; zapis w README bez ścieżki).

### Steps (dev)
1. W `grobing-code`: `flutter create --project-name grobing --org com.grobing --platforms android .`.
   **Zmierzone:** `create` pomija istniejące `README.md` i `.gitignore`, więc oba zostają nietknięte.
   `create` składa identyfikator jako `<org>.<project-name>`, więc daje `com.grobing.grobing`. Dlatego
   `namespace` i `applicationId` w `build.gradle.kts` trzeba ustawić na **`com.grobing.app`**
   (D1), a `MainActivity.kt` przenieść do `kotlin/com/grobing/app/`. Nazwa pakietu Darta zostaje
   `grobing`.
2. Domyślny `.gitignore` Fluttera wygeneruj w katalogu tymczasowym (poza repo) i **dołącz pod**
   istniejące bloki. Usuń duplikaty z bloku „Flutter / Android build output"; blok danych rodziny i
   sekretów zostaje na górze bez zmian.
3. `pubspec.yaml`: `environment.flutter: 3.41.1` (D2), opis aplikacji, **zero zależności poza
   szablonem** (bez Firebase i bez SDK analityki czy raportowania błędów).
4. `analysis_options.yaml` według **wzorca** Friendsheet, nie kopii: `flutter_lints` z szablonu, do tego
   `strict-casts` i `strict-raw-types`, wykluczenia plików generowanych, reguły pojedynczych
   cudzysłowów, `final`/`const`, `directives_ordering`, `prefer_relative_imports`,
   `always_declare_return_types`, `cancel_subscriptions`, `close_sinks` i `avoid_print`. Bez reguł,
   które `flutter_lints` już zawiera.
5. `lib/`: `main.dart` uruchamia `GrobingApp`; motyw ciemny z tokenami stylu B z briefu §6a (prawie
   czarne tło, miękki szary tekst, jeden akcent: ciepły bursztyn jak światło znicza); ekran startowy z
   nazwą aplikacji. **Nie projektujemy ekranu**: wytyczne wizualne to NT-006, a agent `ui` pojawi się
   na sygnał.
6. Android: `android:label="Grobing"`; ciemne tło startu (pkt „Scope diff"); `build.gradle.kts` z
   konfiguracją podpisu `release` z `key.properties` (głośny błąd bez pliku).
7. `README.md`: jak przypięta jest wersja (D2) i co zrobić przy aktualizacji; jak autor tworzy klucz
   (`keytool` z flagami z dokumentacji Fluttera, ścieżka z `project-config.md`) i wypełnia
   `key.properties`; reguła „tylko release na telefonie z danymi"; kopia klucza.
8. `grobing-agents`: `android_package` i `root_widget` w `project-config.example.md`;
   `release_keystore_dir` w lokalnym `project-config.md`.

### AC → evidence
| AC | Dowód |
|---|---|
| 1 create / android / 3.41.1, globalny nietknięty | `flutter --version` przed i po bez zmian; w repo tylko `android/` jako platforma |
| 2 przypięcie | `environment.flutter: 3.41.1` + README; `flutter pub get` przechodzi |
| 3 pakiet | wartość w `project-config.example.md`; poza kodem Androida nie pojawia się w żadnym dokumencie |
| 4 `.gitignore` | diff: istniejące bloki na górze bez zmian, domyślne wpisy Fluttera pod nimi |
| 5 bez Firebase | **test** `test/no_cloud_sdk_test.dart`: `pubspec.lock` nie zawiera pakietów Firebase ani SDK analityki czy raportowania błędów |
| 6 linty | `flutter analyze`: 0 problemów |
| 7 keystore | w drzewie repo nie ma `*.jks`/`*.keystore`; ścieżka tylko w lokalnym `project-config.md`; build release podpisany (stop #2) |
| 8 analyze/test/telefon | **test widgetu** `test/app_start_test.dart`: `GrobingApp` startuje, motyw jest ciemny, nazwa jest widoczna; telefon na stopie #2 |

### Manual verification (stop #2, po polsku)
0. **Przed:** utwórz klucz komendą z README (hasła wpisujesz sam) i wypełnij `android/key.properties`.
1. Podłącz telefon z debugowaniem USB; `flutter devices` go widzi.
2. `flutter run --release`: instalacja przechodzi bez błędu podpisu.
3. Ikona „Grobing" jest w szufladzie aplikacji. Po uruchomieniu **od pierwszej chwili ciemne tło**, bez
   białego błysku; nazwa w szarym, akcent w bursztynie.
4. Zamknij aplikację, otwórz ponownie: to samo.
5. Ustawienia → Aplikacje → Grobing → Uprawnienia: **brak uprawnień**.

### Closing checklist (docs)
- [[ADR-002-flutter-pinned]] → *Follow-ups*: datowane linie o mechanizmie (D2) i nazwie pakietu (D1);
  zdjąć oba `⚠️ OPEN`.
- Paczka na stop #3 obejmuje **trzy repo**: kod (`grobing-code`), vault, agenci
  (`project-config.example.md`). **Bez pusha** do zamknięcia [[ISSUE-006-setup-family-data-guard]] i
  [[NT-008-publication-review]].

## Verification
> `qa`, 2026-10-05. Rytuał WZ-024: format → analiza → testy → kroki ręczne → czekaj.

### Automated (done)
| AC | Dowód | Wynik |
|---|---|---|
| 1 | `flutter --version` = 3.41.1 przed i po; `test/repo_invariants_test.dart`: w repo tylko `android/` | ✅ |
| 2 | `environment.flutter: 3.41.1`; test sprawdza pin; próba z planu: 3.42.0 i zakres poniżej 3.41.1 są odrzucane | ✅ |
| 3 | `com.grobing.app` w `namespace`/`applicationId` (test) i w APK (`aapt`: `package: name='com.grobing.app'`, etykieta `Grobing`); wartość w `project-config.example.md` | ✅ |
| 4 | test: blok danych rodziny i sekretów zaczyna plik, wpisy domyślne pod nim; odporny na CRLF (sprawdzone) | ✅ |
| 5 | `test/no_cloud_sdk_test.dart`: w `pubspec.lock` nie ma Firebase ani SDK analityki, raportowania błędów i reklam | ✅ |
| 6 | `flutter analyze`: **No issues found**; `dart format` stabilny | ✅ |
| 7 | test: brak `*.jks`/`*.keystore` w drzewie; `release_keystore_dir` tylko w lokalnym `project-config.md`; release **bez** `key.properties` kończy się `GradleException` (zmierzone) | ✅ (podpis — krok ręczny) |
| 8 | `test/app_start_test.dart`: `GrobingApp` startuje, motyw ciemny, tło i akcent stylu B; `flutter test` **7/7**; `flutter build apk --debug` OK | ✅ (telefon — krok ręczny) |

Dane rodziny w zmianach: brak (żadnych `*.db`, `*.sqlite*`, kopii, eksportów ani zdjęć; PNG to domyślne
ikony szablonu Fluttera). Sekrety: brak (`key.properties` i klucz poza repo).

### Manual (stop #2)
> **Decyzja autora (2026-10-05, na stopie #2):** do MVP budujemy i sprawdzamy na **wirtualnym telefonie**
> (emulator Android Studio). Na prawdziwy telefon trafi dopiero MVP, jako build release. Zgodne z
> regułą z README: telefon z danymi dostaje tylko release, więc nie ma pułapki podpisu debug → release.
> **Do `docs` przy zamknięciu:** ta decyzja zmienia kontrakt. Do poprawienia: `DEFINITION_OF_DONE.md`
> (ISSUE-DoD „ręczna weryfikacja w telefonie”), `grobing-agents/.claude/rules/autonomous-flow.md`
> (stop #2) i skill `qa`, z wyjątkiem tego, co sprawdzi tylko prawdziwy telefon: GPS na miejscu,
> czytelność w słońcu (NFR-004), offline na cmentarzu.

- Krok 0 (klucz + `key.properties`): ✅ autor. `flutter build apk --release` przeszedł; `apksigner`:
  podpis `CN=Unknown` (klucz Grobing, **nie** `CN=Android Debug`); `aapt`: `com.grobing.app`, etykieta
  `Grobing`, brak uprawnień widocznych dla użytkownika.
- [x] Kroki 1-5 na emulatorze `Medium Phone API 36.1` (Android 16, x86_64): `flutter install --release`
  przeszedł, `am start`: `Status: ok`; zrzut ekranu: ciemne tło, szary napis, bursztynowa kreska;
  `dumpsys package`: brak uprawnień widocznych dla użytkownika. **Autor: „ok”** (2026-10-05), w tym brak
  białego błysku przy starcie.

### Verdict (self-check)
**APPROVED** — wszystkie 8 AC z dowodem; rytuał WZ-024 przeszedł (format → analiza → testy 7/7 → kroki
ręczne → „ok”).

**Czego szukałem i nie znalazłem:** danych rodziny w zmianach (plików bazy, kopii, eksportów, zdjęć,
nazwisk); sekretów (haseł, `key.properties`, `*.jks` w drzewie; `git check-ignore` potwierdza
wykluczenie); SDK Firebase, analityki i raportowania błędów (test na `pubspec.lock`); uprawnienia
INTERNET w buildzie release (jest tylko w debug/profile, z szablonu, dla hot reload); podpisu release
kluczem debug.

**Uwagi, które nie blokują:**
- `version: 1.0.0+1` zostało z szablonu; `cupertino_icons` też z szablonu, na razie nieużywane.
- Kopia klucza (`.jks` + hasła) w zaszyfrowanym miejscu: **do zrobienia przez autora** przed
  pierwszymi prawdziwymi danymi.
- Hasło magazynu przeszło przez sesję: harness pokazał zmianę w `key.properties`, który utworzył agent.
  Ryzyko małe, bo trzeba mieć też plik klucza. Zmiana hasła po sesji (`keytool -storepasswd` /
  `-keypasswd`) to opcja autora. Lekcja zapisana w pamięci agenta: nie tworzyć za autora plików z
  sekretami.
- Trzy linki w zamkniętym ISSUE-001 wskazują na usuniętą notatkę z INBOX; to zapis historyczny.

## Dependencies
| Dependency | Type | Status |
|---|---|---|
| ADR-002 (Flutter, pinned) | technical | decyzja zapadła w kick-offie; plik powstaje w ISSUE-001 |

## Definition of Done
- [ ] DoD ISSUE (MVP) z `00_START_HERE/DEFINITION_OF_DONE.md`
- [ ] Ręczna weryfikacja w telefonie: aplikacja się instaluje i startuje
- [ ] **INVEST self-check**
