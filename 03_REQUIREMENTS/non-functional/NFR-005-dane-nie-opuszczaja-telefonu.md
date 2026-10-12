---
title: "NFR-005 — No family data leaves the phone except the encrypted backup and the export"
type: non-functional-requirement
status: draft
epic: ["[[EPIC-001-zabezpiecz-i-przepisz]]", "[[EPIC-002-wizyta]]", "[[EPIC-003-zrozumienie]]"]
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "PROJECT_BRIEF §Security (ASVS-lite translated, off-phone copy) · Step 0 (local-first: privacy) · §2 value ('private')"
created: 2026-10-05
updated: 2026-10-12
---

# NFR-005 — Dane nie opuszczają telefonu poza kopią

## Requirement
Dane rodziny opuszczają telefon **wyłącznie** jako:
1. **kopia zaszyfrowana w telefonie** (hasłem) przed wysłaniem do folderu w chmurze autora;
2. **okresowy eksport** czytelny bez aplikacji, przechowywany offline u rodziny (§Security: *„a periodic
   plain export kept offline by the family"*).

Nic więcej: **bez analityki, bez crash reportingu wysyłającego dane, bez danych rodziny w logach**, bez
SDK wysyłających dane z telefonu (np. Firebase).

| | |
|---|---|
| **Metric** | kanały wychodzące z telefonu, które niosą dane rodziny, poza dwoma powyższymi |
| **Target** | **zero** |
| **Method** | przegląd zależności przy każdej pozycji dokładającej pakiet (`qa`); przegląd logów pod kątem danych rodziny |
| **Verification trigger** | każda nowa zależność · [[ISSUE-002-bootstrap-code-repo]] (AC: brak Firebase) · pełny przegląd L1 przy [[DEF-002-full-l1-review]] |

## Notes
- **Wchodzi, nie wychodzi:** kafelki map są pobierane, nie wysyłane; link do Grobonetu otwiera się w
  zewnętrznej przeglądarce (bez WebView z danymi użytkownika).
- **Androidowa automatyczna kopia (`allowBackup`)** domyślnie kopiuje dane aplikacji na Dysk Google — to
  też kanał wychodzący. **Decyzja świadoma, nie dziedziczona** → [[ADR-004-backup-format-encryption-destination]].
  ✅ 2026-10-05: zamknięte w ADR-004 (pkt 4). `allowBackup="false"` **i** `dataExtractionRules`, bo samo
  `allowBackup="false"` nie zamyka transferu między urządzeniami (D2D). Zmierzone w
  [[SPIKE-003-backup-and-restore]], M7. ✅ 2026-10-06: zamknięte w kodzie ([[ISSUE-008-backup-write]]):
  `allowBackup="false"` + `dataExtractionRules` wykluczające wszystko; M7 powtórzone na buildzie release.
- **Kanał kopii (2026-10-06, [[ISSUE-008-backup-write]]):** aplikacja nie ma uprawnienia `INTERNET`
  (sprawdzone `aapt` na APK release) — plik kopii wysyła aplikacja Dysk. Nowe zależności `cryptography` i
  `pointycastle` przejrzane: czysty Dart, bez kodu sieciowego.
- **Kopia w tle (2026-10-06, [[ISSUE-010-background-backup]]):** nowa zależność `androidx.work` 2.11.2
  (Jetpack) przejrzana: dokłada `androidx.room`, `androidx.sqlite`, `androidx.startup` i uprawnienia
  `WAKE_LOCK`, `ACCESS_NETWORK_STATE`, `RECEIVE_BOOT_COMPLETED`, `FOREGROUND_SERVICE` — **bez `INTERNET`**
  (`aapt` na APK release), bez bibliotek sieciowych. Własna baza WorkManagera trzyma tylko listę zadań,
  bez danych rodziny.
- **Link do zdjęcia satelitarnego (2026-10-07, [[ISSUE-015-add-cemetery-from-database]]):** pierwsze wyjście z
  aplikacji, tylko po dotknięciu. Adres Map Google z punktem otwiera inna aplikacja (Mapy, a bez nich
  przeglądarka). Wychodzi punkt **publicznego** cmentarza z bazy OpenStreetMap, nie dane rodziny. Bez nowej
  zależności i bez `INTERNET` (`aapt` na APK release). **Granica:** gdyby ten sam link otwierał kiedyś
  cmentarz już zapisany w aplikacji, punkt mówiłby, gdzie leży rodzina autora — wtedy to osobna decyzja
  wobec tego NFR.
- **`INTERNET` dla mapy cmentarza (2026-10-08, [[ADR-003-map-source-offline]]):**
  - aplikacja dostanie to uprawnienie wraz z pozycją, która zbuduje mapę cmentarza, i **tylko po to**, żeby
    pobrać plan cmentarza z OSM przy jego dodaniu i wyświetlić ortofotomapę GUGiK online;
  - **od tej chwili tę własność pilnuje kod, a nie system:** aplikacja z `INTERNET` mogłaby wysłać cokolwiek.
    Dlatego pozycja, która je doda, ma w DoD: lista hostów w kodzie (OSM, GUGiK), tylko HTTPS, przegląd
    zależności i `aapt` na APK. `qa` sprawdza, że żadne inne wywołanie sieciowe nie powstało;
  - **co wychodzi:** z telefonu nie wychodzą dane rodziny. Wychodzą zapytania o **obszar cmentarza**, czyli
    ramka albo kafelki, z adresu IP telefonu. To ta sama granica, co przy linku do zdjęcia satelitarnego wyżej:
    serwery OSM i GUGiK mogłyby z tego wywnioskować, gdzie leży rodzina autora. Autor przyjął to, wybierając
    plan z pobraniem i zdjęcie online;
  - wcześniejszy pomysł „aplikacja bez `INTERNET`, plik z PC” (droga (b) w SPIKE-001) odrzucił autor.
- ✅ **`INTERNET` w aplikacji od 2026-10-12** ([[ISSUE-027-cemetery-map-plan-photo-states]]) — warunki z punktu wyżej spełnione i
  pilnowane testami:
  - **wszystkie adresy w `grobing-code/lib/net/hosts.dart`**, tylko `https` (test na źródłach: w `lib/` żaden adres w stringu poza tym
    plikiem; wyjątek — link do zdjęcia satelitarnego, który otwiera inna aplikacja); Overpass: `overpass-api.de`,
    `overpass.private.coffee` (bez `maps.mail.ru` — decyzja autora D4); GUGiK: `mapy.geoportal.gov.pl`; `User-Agent` nazywa
    aplikację, nie osobę; manifest bez ruchu jawnego (`usesCleartextTraffic="false"`);
  - **zdjęcie z góry nie zostaje w telefonie:** `flutter_map` 8.3.2 domyślnie zapisuje kafelki na dysk — wyłączone
    (`DisabledMapCachingProvider`), sprawdzone `run-as` (brak plików kafelków);
  - **bez adresów kafelków w logu systemu:** `flutter_map` przy nieudanym kafelku wypisywał jego adres (numery kafelków = miejsce,
    które oglądał telefon) także w release — wyciszone (`silenceExceptions`), na emulatorze 0 linii; pobieranie planu loguje sam
    rodzaj błędu, bez punktu;
  - `aapt` na APK release: z nowych uprawnień tylko `INTERNET`; bez nowych zależności (`pubspec.lock` bez zmian).

  **Czego to nie łapie:** wywołania sieciowego dodanego przez przyszłą zależność bez adresu w stringu — dlatego przegląd zależności i
  logcat przy każdej pozycji z siecią (`qa`).
- ✅ **Lokalizacja telefonu od 2026-10-12** ([[ISSUE-029-pin-on-site-gps]], [[ADR-017-location-from-gnss-only]]) — pozycja przy grobie
  to przy prawdziwym użyciu miejsce, gdzie leży rodzina:
  - **tylko satelity** (`LocationManager.GPS_PROVIDER`, własny kanał `HereLocation.kt`), bez Wi-Fi i masztów, **bez usług Google i bez
    nowej zależności** (`pubspec.lock` bez zmian); tylko gdy ekran cmentarza słucha, bez pracy w tle i bez `ACCESS_BACKGROUND_LOCATION`;
  - **żadnej pozycji w logu** — test na źródłach (`HereLocation.kt` bez `Log.`), logcat procesu aplikacji na emulatorze: 0 linii ze
    współrzędnymi; pozycja nie wychodzi z telefonu poza kopią (pinezka grobu jest w bazie jak każda inna dana);
  - `aapt` na APK release: z nowych uprawnień tylko `ACCESS_FINE_LOCATION` i `ACCESS_COARSE_LOCATION` (test na manifeście).

  **Czego to nie łapie:** ustawienia telefonu „Dokładność lokalizacji Google” — to sprawa systemu, nie aplikacji; aplikacja z niego
  nie korzysta.
- Eksport nie jest szyfrowany z założenia (czytelność jest jego celem) — dlatego żyje offline, nie w chmurze
  (§Security).
- Hipoteza prawna (wyłączenie domowe RODO) jest najmocniejsza, gdy chmura trzyma tylko szyfrogram →
  [[NT-003-verify-household-exemption]].
