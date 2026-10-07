---
title: "US-005 — Attach photos to a grave and a person (zdjęcia)"
type: user-story
status: done
epic: "[[EPIC-001-zabezpiecz-i-przepisz]]"
persona: "[[P1-zbierajacy]]"
moscow: [M1]
journey-steps: "n/a — poza ścieżką (M1)"
FR: []
NFR: ["[[NFR-002-odtworzenie-na-nowym-telefonie]]", "[[NFR-005-dane-nie-opuszczaja-telefonu]]"]
issues: ["[[ISSUE-016-photos-grave-and-person]]", "[[ISSUE-017-person-photos]]"]
quality-verdict: APPROVED
verdict-date: 2026-10-07
verdict-reviewer: self-check
source: "PROJECT_BRIEF §5 M1 (zdjęcie nagrobka, zdjęcie osoby) · §4 Pains („brak zdjęć") · data-model.md (Media)"
created: 2026-10-05
updated: 2026-10-07
---

# US-005 — Zdjęcia nagrobka i osoby

## Story
**Jako** Zbierający **chcę** dołączyć zdjęcie nagrobka do grobu i zdjęcie osoby do osoby, **żeby**
notatki bez zdjęć przestały być jedynym zapisem, a zdjęcia przeżyły telefon razem z danymi.

## Acceptance Criteria
- **AC-1 — zdjęcie przy grobie i osobie.** *When* wybieram zdjęcie z galerii albo robię je aparatem
  *Then* jest widoczne przy grobie albo przy osobie.
- **AC-2 — zdjęcie w prywatnym magazynie aplikacji.** *Then* aplikacja trzyma własną kopię pliku w
  prywatnym magazynie (data-model.md → *Media*) i nie zależy od tego, czy oryginał zostanie w galerii.
- **AC-3 — zdjęcie jest w kopii.** *Given* zdjęcie w aplikacji *When* powstaje kopia *Then* zdjęcie jest
  w niej i wraca po odtworzeniu (odcisk danych obejmuje zdjęcia —
  [[NFR-002-odtworzenie-na-nowym-telefonie]]).

## Out of scope
- Pinezka z lokalizacji zdjęcia → `TRACEABILITY.md` → *Open gaps* 2 (nieplanowane).
- Nowe zdjęcie robione na miejscu przy wizycie → [[EPIC-002-wizyta]] (M6).

## Notes
- ~~**Rozdzielczość zdjęć w aplikacji** jest nierozstrzygnięta~~ — **rozstrzygnięte 2026-10-07** (decyzja autora D2'
  na stopie #1 [[ISSUE-016-photos-grave-and-person]]): JPEG 2048 px, jakość 85, bez EXIF —
  [[ADR-008-photos-access-copy-and-backup-consistency]]. Spójność kopii przy usuwaniu: ADR-008 pkt 3. Liczby kopii w
  tle (10 min ciszy, najpóźniej 60 min) zostają — kopia ze zdjęciami mieści się w zadaniu w tle z dużym zapasem (F2).
- **Rozpisanie (2026-10-07):** [[ISSUE-016-photos-grave-and-person]] (zdjęcie nagrobka, fundament — `done`) i
  [[ISSUE-017-person-photos]] (baza zdjęć osoby, dzielona, „profilowe”, schemat v4). Werdykt US — po ISSUE-017
  (*Verification (US)* niżej). **Po werdykcie:** [[ISSUE-018-profile-photo-crop]] — kadr profilowego ze zdjęcia
  grupowego (decyzja autora na stopie #2 ISSUE-017), rozwinięcie poza AC tej US.
- **Kopia a zdjęcia (2026-10-06, [[ISSUE-008-backup-write]]):** migawka bazy (`VACUUM INTO`) i odczyt plików
  zdjęć nie są jedną transakcją. Dziś zdjęcia dodaje tylko przycisk debug. Gdy zdjęcie da się usunąć,
  usunięcie w trakcie kopii zostawi w kopii wpis bez pliku — do rozstrzygnięcia przy planowaniu
  (`04_ARCHITECTURE/backup-format.md` → *Known limits*).
- **Kopia w tle a zdjęcia (2026-10-06, [[ISSUE-010-background-backup]]):** kopia powstaje raz po sesji
  (10 min ciszy, najpóźniej 60 min od pierwszej zmiany) i zawsze wysyła całość. Przy pierwszych zdjęciach
  te dwie liczby wracają do decyzji razem z rozdzielczością. Do tego:
  - zadanie w tle ma ~10 min — kopia rzędu kilku GB wymagałaby zadania na pierwszym planie;
  - stempel zmian widzi zdjęcie po rozmiarze i czasie pliku, nie po treści — zdjęcie zmienione „w
    miejscu” (ten sam rozmiar, przywrócony czas) nie wyzwoli kopii. Dziś aplikacja zdjęć w miejscu nie
    edytuje.
- Kopię w Zdjęciach Google trzeba wstrzymać dla zdjęć nagrobków, bo wysłałaby je niezaszyfrowane
  (`TRACEABILITY.md` → *Open gaps* 2).

## Verification (US)
> `qa`, 2026-10-07. Werdykt na poziomie US wystawił **niezależny przegląd**: subagent bez udziału w budowie, tylko
> odczyt plików i jeden przebieg `flutter test` (**389/389**, ok. 50 s), na drzewie roboczym z paczką ISSUE-017. Po
> przeglądzie `qa` dopisał testy z uwag 1 i 2: **391/391**. DoD US: każde AC z testem happy-path · pokazane w aplikacji
> na emulatorze · werdykt zapisany · wiersz w `TRACEABILITY.md`.

| AC | Test happy-path | Pokazane człowiekowi (emulator) |
|---|---|---|
| AC-1 zdjęcie przy grobie | `grave_photo_screens_test.dart`: „US-005 AC-1, D12” (pole → arkusz → galeria → zdjęcie nad tytułem), „Zrób zdjęcie” (aparat, dopisany po przeglądzie), D9 (miniatura na cmentarzu) · `test/data/photos_test.dart` · `test/app/photo/photos_test.dart` | ISSUE-016 stop #2. **Autor:** kroki 1–6 „ok”; stan urządzenia potwierdzony; odczucie „jest dobrze”. Po zmianie D12 autor ocenił wygląd pola, a przejście wykonał **agent** |
| AC-1 zdjęcie przy osobie | `person_photos_screens_test.dart`: „US-005 AC-1 — element 1a” (2 zdjęcia z galerii → okrąg i „2 zdjęcia” → „Zapisz” → profilowe w karcie grobu), „Zrób zdjęcie” z bazy zdjęć osoby (dopisany po przeglądzie) · `person_photos_test.dart` | ISSUE-017 stop #2. **Autor:** 3 zdjęcia z galerii i zdjęcie wspólne z drugą osobą (stan urządzenia i logcat); „względnie ok”, prośba o kadr → [[ISSUE-018-profile-photo-crop]]. **Agent (`adb`):** osoba z innego grobu później, „Usuń z tej osoby”, „Odrzuć”, aparat |
| AC-2 własna kopia w prywatnym magazynie | `test/app/photo/photos_test.dart` · `test/data/photos_test.dart` · `person_photos_test.dart` i `person_photos_screens_test.dart` (pliki w `media/zdjecia/`, kopie z okna wyboru usunięte) · `person_photos_draft_test.dart` („Odrzuć” nie zostawia plików) | **Agent, nagrobek** (ISSUE-016): oryginał usunięty z galerii i MediaStore, zdjęcie dalej w grobie. Osoba — ta sama ścieżka `Photos`, sprawdzona testem |
| AC-3 zdjęcie nagrobka w kopii | `restore_service_test.dart` („ISSUE-016 AC-3”) · `backup_archive_test.dart` (zdjęcia z SHA-256; zdjęcie dodane albo usunięte w trakcie kopii — F4 i D3 z ISSUE-016) · `data_state_test.dart` | **Agent** (ISSUE-016): kopia z `Medium_Phone` → niezależny dekoder `age` na PC → odtworzenie na `Grobing_Restore`, odcisk zgodny |
| AC-3 zdjęcia osób i łącza w kopii | `restore_service_test.dart`: „ISSUE-017 F3” (kopia v3 → v4: łącza w kolejności `id`, pliki, `foreign_key_check`) i „end to end” (kopia v4 danych debug: odcisk i liczby zgodne, **po przeglądzie także łącza matki w kolejności i wspólny wiersz ojca odczytane wprost**) · `migration_test.dart` (F2) · `data_state_test.dart` | **Nie odtworzono na urządzeniu** (w sesji nie było hasła testowego z ISSUE-016). Agent sprawdził kopię w tle po migracji |

**Werdykt: APPROVED** z uwagami. Każde AC, w części o grobie i o osobie, ma test happy-path, który przechodzi. AC-1
autor widział na emulatorze w obu częściach. AC-2 i AC-3 sprawdził agent albo test odtworzenia na prawdziwym archiwum
z kodu produkcyjnego. Kadr profilowego to nowe oczekiwanie spoza AC — według decyzji autora trafia do
[[ISSUE-018-profile-photo-crop]].

**Czego szukano i nie znaleziono:**
- AC bez testu happy-path; testów pominiętych albo czerwonych;
- pliku w kopii, którego nie obejmuje odcisk;
- utraty łączy osób albo ich kolejności przy migracji i przy odtworzeniu kopii v3;
- zdjęcia zależnego po zapisie od pliku w galerii albo w cache okna wyboru;
- uprawnienia `INTERNET`;
- obrazów, baz, kopii i eksportów w repo — jedyne obrazy to ikony w `android/app/src/main/res/`;
- prawdziwych osób w testach i danych debug.

Granica: bez porównania z notatkami rodziny, bo `family_data_dir` nie był czytany.

**Uwagi, które nie blokują:**
1. ~~Aparat bez testu happy-path~~ — **poprawione w paczce ISSUE-017** (dwa testy widżetu: grób i baza zdjęć osoby).
2. **AC-3 dla osób bez próbnego odtworzenia na urządzeniu.** Brakowało hasła testowego z poprzedniej sesji, a nie
   sekretu autora. Test „end to end” sprawdza teraz łącza i profilowe wprost (poprawione w paczce). Odtworzenie na
   drugim emulatorze — przy następnej pozycji z kopią, z nowym hasłem testowym.
3. **Przy zdjęciach osób autor ocenił niewiele.** Nieocenione: „Ustaw jako profilowe”, odczucie siatki i okręgu,
   zapis przez „Zapisz” (D3) i lista „Kto jest na zdjęciu?”.
4. **Kadr profilowego** — [[ISSUE-018-profile-photo-crop]], następna pozycja (decyzja autora). Bez niej AC są
   spełnione, ale oczekiwanie autora wobec profilowego — nie.
5. **AC-2 dla osoby** sprawdzone tylko testem; na urządzeniu — przy nagrobku.
6. **Pole „Dodaj zdjęcie nagrobka”** nie ma akcji dla czytnika i sterowania przełącznikami (ten sam wzorzec, który
   przegląd `ui` w ISSUE-017 uznał za MAJOR). Kandydat na małą pozycję (`CURRENT_STATE.md`).
7. **Nie zmierzone na prawdziwym zdjęciu:**
   - HEIF;
   - rozmiar 0,4–0,7 MB (obrazy syntetyczne ok. 236 KB);
   - zmniejszanie w Kotlinie bez testu automatycznego (F1 na emulatorze);
   - kolejność zaznaczania tylko na Androidzie 16;
   - TalkBack i duża czcionka tylko z kodu.
8. Werdykt obowiązuje dla commita obejmującego całą paczkę ISSUE-017 (w tym ADR-009, [[zdjecia-osoby]] i ISSUE-018).
9. **Kopia w Zdjęciach Google dla zdjęć nagrobków** (*Notes*, `TRACEABILITY.md` → *Open gaps* 2) — ustawienie telefonu
   autora, przed MVP.
