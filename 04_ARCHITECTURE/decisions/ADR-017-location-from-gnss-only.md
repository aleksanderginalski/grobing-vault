---
title: "ADR-017 — The phone's position from the GNSS satellites alone, through the app's own channel (no Google services, no new dependency)"
type: adr
status: accepted
supersedes: []
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
decided-by: "[[ISSUE-029-pin-on-site-gps]]"
source: "ISSUE-029 → Implementation plan (Prior art: AOSP Location.getAccuracy(), LocationManager providers; Android runtime location permissions; pub.dev geolocator 14.1.1 and geolocator_android build.gradle; Google Location Accuracy help), D2; stop #1 („ok”: D2 = A); Verification · NFR-005 · ADR-002"
created: 2026-10-12
updated: 2026-10-12
---

# ADR-017 — Pozycja telefonu tylko z satelitów, własnym kanałem aplikacji

> Architecture Decision Record. **Append-only po akceptacji:** zmiana decyzji = nowy ADR. Dopisek w
> *Follow-ups* (datowany, bez zmiany decyzji) nie jest przepisaniem.

## Status
accepted — 2026-10-12 (stop #1 [[ISSUE-029-pin-on-site-gps]]: D2 = A — „ok”), wdrożone i sprawdzone w tej samej pozycji:
- na emulatorze: kropka, zgoda dokładna, odmowa, blokada po dwóch odmowach, zgoda przybliżona, tryb samolotowy;
- logcat procesu aplikacji bez współrzędnych; `aapt` na APK release — z nowych uprawnień tylko `ACCESS_FINE_LOCATION` i
  `ACCESS_COARSE_LOCATION`; `pubspec.lock` bez zmian;
- stop #2 „ok”.

**GPS w terenie jeszcze niesprawdzony** — wizyta na cmentarzu (`CURRENT_STATE.md` → *Parked*). Zamknięte 2026-10-12.

To nowa decyzja, **nie zastępuje żadnego ADR** — sygnał dla `architect` („pierwszy ADR zastąpiony po akceptacji”, retro 2, R7) się nie
zapala.

## Context
- **Pinezka na miejscu** ([[US-008-pinezka-na-miejscu]]) potrzebuje pozycji telefonu przy grobie: kropki „tu jesteś” z kołem dokładności
  i pinezki w kropce ([[cmentarz]] elementy 10–12).
- **[[NFR-005-dane-nie-opuszczaja-telefonu]]:** aplikacja nie ma żadnej zależności od usług Google („No Firebase, analytics…” w
  `pubspec.yaml`), a od `INTERNET` (ISSUE-027) tę własność pilnuje kod. Pozycja telefonu przy grobie to przy prawdziwym użyciu miejsce,
  gdzie leży rodzina — nie może trafić do logu ani wyjść z telefonu.
- **Przypięty Flutter 3.41.1** ([[ADR-002-flutter-pinned]]): każdy pakiet to przegląd zgodności i przypięcie.
- **Kanon** (cytaty w ISSUE-029 → *Prior art*):
  - `Location.getAccuracy()` — *„the estimated horizontal accuracy radius in meters of this location at the 68th percentile confidence
    level”*: koło dokładności to „zwykle”, nie „na pewno”;
  - `LocationManager.GPS_PROVIDER` — *„determines location using GNSS satellites”*; `NETWORK_PROVIDER` — *„based on nearby of cell tower
    and WiFi access points. Operation of this provider may require a data connection”*; `FUSED_PROVIDER` łączy kilka źródeł;
  - Android 12+: FINE i COARSE w jednym żądaniu, wybór „Precise” albo „Approximate” (ok. 3 km²); od Androida 11 druga odmowa wyłącza
    okno systemu;
  - `geolocator` 14.1.1 — *„FusedLocationProviderClient or if not available the LocationManager”*, opcja `forceLocationManager`;
    `geolocator_android` dokłada `com.google.android.gms:play-services-location:21.2.0` i sześć pakietów platform.

## Options
- **A — własny kanał na `LocationManager.GPS_PROVIDER`** (wybrane): sam GNSS, bez nowej zależności, bez usług Google, wzorzec
  istniejących kanałów (`ExternalLinks.kt`, `PhotoPreparation.kt`). Koszt: ok. 150–250 linii Kotlin i Dart — uprawnienia, strumień,
  ustawienia. W budynku pozycji zwykle nie ma.
- **B — `geolocator` z `forceLocationManager`:** mniej własnego kodu. Koszt: `play-services-location` w APK, sześć pakietów do przypięcia
  i przeglądu, zgodność z Flutterem 3.41.1 do sprawdzenia.
- **C — `geolocator` z Fused (usługi Google):** szybsza pierwsza pozycja (Wi-Fi, maszty). Koszt jak B, a pozycja zależy od usług Google
  i ich ustawienia „Dokładność lokalizacji”; na otwartym cmentarzu przewaga znika, bo i tak liczy GNSS.

## Decision
1. **Pozycję daje `HereLocation.kt`** — `LocationManager.GPS_PROVIDER`, `requestLocationUpdates` co ok. 1 s **tylko wtedy, gdy ekran
   słucha** (`EventChannel`), `removeUpdates` przy anulowaniu. Bez `NETWORK_PROVIDER`, bez Fused, bez usług Google.
2. **Uprawnienia:** `ACCESS_FINE_LOCATION` z `ACCESS_COARSE_LOCATION` w jednym żądaniu; „Przybliżona” = bez kropki, pinezka ręcznie; po
  odmowie bez uzasadnienia do pokazania — „zablokowana”, droga przez ustawienia aplikacji. `uses-feature gps` niewymagane. **Bez
  `ACCESS_BACKGROUND_LOCATION`**, bez pracy w tle.
3. **Żadnej pozycji w logu** — ani w Kotlinie, ani w Dart (test na źródłach: `HereLocation.kt` bez `Log.`).
4. **Nakładka w Dart** (`lib/app/grave/here_location.dart`): `HereLocation` za interfejsem (testy podmieniają ją przez `MapHereLocation`),
  jeden wspólny strumień — drugi `receiveBroadcastStream` anulowałby pierwszy po stronie natywnej.
5. **Próg „słaby sygnał”** to jedna stała (`weakSignalM`, 15 m) — **tymczasowa**, ustawi ją pomiar przy grobach ([[cmentarz]] D37).

## Consequences
- **Dobre:** nic poza satelitami; brak nowych pakietów i przeglądów zależności; NFR-005 pilnują testy na źródłach i na manifeście.
- **Złe:** w budynku i w mieście pierwsza pozycja bywa wolna albo jej nie ma („Szukam pozycji…”) — na cmentarzu bez znaczenia, w domu
  pinezkę stawia się ręcznie. Bez wspomagania z sieci zimny start GNSS trwa dłużej.
- **Emulator:** pozycję daje `adb emu geo fix <dł> <szer> <wysokość> <satelity>` — bez wysokości i satelitów zostawał domyślny punkt;
  dokładności ta komenda nie ustawia (słaby sygnał tylko w testach).

## Follow-ups
- Pomiar przy 3 grobach (*Parked*): dokładność kropki → wartość `weakSignalM`; jeśli kropka nie trafia nawet w kwaterę — pinezka zaczyna
  od kwatery ([[cmentarz]] D16 → *Obali*).
- Jeśli w terenie pierwsza pozycja będzie zbyt wolna — nowy ADR z wyborem między wspomaganiem z sieci a NFR-005, nie cicha zmiana dostawcy.
