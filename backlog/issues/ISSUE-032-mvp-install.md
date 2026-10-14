---
title: "ISSUE-032 — MVP install on the author's phone: data-model audit, hand checks, conditions before the first real data"
type: issue
status: draft
delivery-style: task-level
priority: MUST
ideal_days: null
quality-verdict: pending
verdict-date: null
verdict-reviewer: null
source: "[[2026-10-13-retro-03]] R8, R9 · `CURRENT_STATE.md` → *Droga do instalacji MVP* (ostatni krok bez pozycji)"
created: 2026-10-13
updated: 2026-10-14
---

# ISSUE-032 — Instalacja MVP na telefonie autora

> **`draft`: dom dla dwóch decyzji retro 3, a nie plan.** Droga do instalacji MVP kończyła się krokiem bez pozycji; retro 3
> dało mu dwie rzeczy — audyt (R9) i jedną listę rzeczy niesprawdzonych w ręce (R8). Plan pisze `planning`, gdy droga dojdzie
> do tego kroku (po [[US-006-eksport-dla-rodziny]] i [[NT-007-hand-over-note]]).

## Why
Po instalacji na telefon trafiają **prawdziwe dane rodziny** (decyzja autora 2026-10-08) — od tej chwili błąd kosztuje dane, a nie
rundę. Wszystko, co do tej pory sprawdzał tylko emulator, test albo nikt, ma być sprawdzone albo świadomie przyjęte przed
pierwszym prawdziwym wpisem.

## Before install
Warunki — każdy ma swój dom, tutaj tylko lista:
1. **Audyt pól modelu ↔ ekrany** (retro 3, R9): każde pole [[data-model]] ma ekran, który je zapisuje, albo jawne „nie zapisuje go
   żaden ekran, bo…”. Powód: adres kwatery (M1) miał kolumny od v1, a ekran dopiero w [[ISSUE-028-cemetery-sectors]]. Robi agent;
   wynik to tabela w tej pozycji;
2. **klucz wydania** (`.jks` i oba hasła) w zaszyfrowanym miejscu — autor (`CURRENT_STATE.md` → *Autor, poza sesją*; pytanie z retro
   1, 2 i 3 bez odpowiedzi);
3. **notka przekazania** sprawdzona jej własną drogą — [[NT-007-hand-over-note]];
4. **dane aplikacji wyczyszczone** po buildzie z wizyty (wymyślone dane) — `CURRENT_STATE.md` → *Autor, poza sesją*;
5. kandydaci na małe pozycje „przed instalacją MVP” — `CURRENT_STATE.md` → *Poza tą kolejnością* (np. mapa cmentarza przy
   tekście 200%);
6. *kandydat, nie decyzja retro:* testy dostępności dotyku z R2 (`meetsGuideline`) na ekranach zbudowanych przed retro 3 — decyzja
   przy planowaniu.

## Hand checks — rzeczy niesprawdzone w ręce
> **Jedna lista** (retro 3, R8). Pisze `docs` przy zamknięciu każdej pozycji: każde „pomiń”, „ok” bez śladu na urządzeniu i
> „nieprzetestowane na żywo” z *Verification* → jeden wiersz ze źródłem. Na telefonie z buildem release, na wymyślonych danych,
> **przed** pierwszymi prawdziwymi. Krok w terenie (GPS przy grobach, słońce, tryb samolotowy) jest w `CURRENT_STATE.md` →
> *Parked*, nie tutaj.

**Kopia**
- po zmianie danych pojawia się „(w tle)” — w AOT sprawdzał to tylko build profile ([[ISSUE-010-background-backup]]);
- rozpoznanie „Dysk Google” w wierszu kopii — tylko test ([[ISSUE-022-app-skeleton-tabs-people-settings]]).

**Zdjęcia**
- zdjęcie HEIF z telefonu — emulator ich nie robi ([[ISSUE-016-photos-grave-and-person]]);
- okno wyboru oddaje zdjęcia w kolejności zaznaczania — sprawdzone tylko na Androidzie 16 ([[ISSUE-017-person-photos]]);
- nieocenione w ręce: „Ustaw jako profilowe”, siatka i okrąg, zapis zdjęć przez „Zapisz”, lista „Kto jest na zdjęciu?”
  ([[ISSUE-017-person-photos]]);
- kadr profilowego: podwójne dotknięcie i ok. 0,3 s czekania przy pojedynczym; pamięć okręgów z małym kadrem
  ([[ISSUE-018-profile-photo-crop]], [[ADR-010-profile-photo-crop-pixels]] → *Follow-ups*).

**Osoby i rodzina**
- tło z pasma w widoku osoby — „pomiń” ([[ISSUE-024-person-view]], krok 3 rundy 2); TalkBack w widoku osoby, ekran 360 dp;
- TalkBack i tekst 200% w kreatorze związku ([[ISSUE-025-gender-kinship-together-since]]);
- TalkBack i duże powiększenie tekstu na Osobach i w ustawieniach ([[ISSUE-022-app-skeleton-tabs-people-settings]]).

**Mapa Polski**
- znicz z liczbą i cmentarz bez punktu — kroki pominięte, pokryte testami i agentem ([[ISSUE-014-home-map-of-poland]]);
- wydajność na słabym telefonie, TalkBack w arkuszu, telefon trzymany poziomo ([[ISSUE-023-poland-map-r1-cemetery-photo]]).

**Mapa cmentarza i pinezka**
- znicz → arkusz → uchwyt → lista → wstecz — „ok” bez śladu ([[ISSUE-027-cemetery-map-plan-photo-states]], krok 3); stan „brak w
  OSM”, koszt rysowania, TalkBack na planie;
- rysowanie kwatery celownikiem (K1), zmiana nazwy i „Usuń z planu”, „Wpisz adres” — „pomiń” ([[ISSUE-028-cemetery-sectors]]);
  okno „Popraw grób” przy tekście 200% z otwartą klawiaturą ([[grob]] → *Open*);
- trzy stany ◎ — „ok” bez śladu ([[ISSUE-029-pin-on-site-gps]], krok 2); słaby sygnał i „Włącz” tylko w testach; TalkBack.

**Drzewo** (decyzja autora w `/pm` 2026-10-13: ocena na emulatorze, telefon tutaj)
- zadanie na czas „kim jest X dla mnie” < 30 s przy ok. 100 osobach — „pomiń” na stopie #2 ([[SPIKE-002-tree-on-a-phone]], krok 3; kryterium
  spike'a niezmierzone);
- płynność przesuwania i przejścia między poziomami na fizycznym telefonie — nieprzetestowane na żywo, emulator to tylko wskazówka
  ([[SPIKE-002-tree-on-a-phone]] → *Findings* M3);
- progi S2 (oddalanie odsłania dalszą rodzinę) przy szczypaniu palcami — nieprzetestowane na żywo, na emulatorze tylko przyciski i mysz
  ([[SPIKE-002-tree-on-a-phone]]);
- „Pokaż w drzewie” z widoku osoby otwiera drzewo tam, gdzie się go spodziewasz — „ok” bez śladu ([[ISSUE-033-tree-from-a-person]], krok 3);
- TalkBack na drzewie: opisy węzłów („…, Moja babcia, w środek” — od [[ISSUE-035-tree-names-shrink-my-voice]], wcześniej „Twoja”) i pigułka poziomu —
  nieprzetestowane na żywo, tylko `uiautomator` i testy ([[ISSUE-033-tree-from-a-person]]).

**Drzewo — tryb prezentacji** ([[ISSUE-034-tree-presentation-mode]] → *Verification*)
- przesyłanie ekranu z trybu prezentacji na telewizor autora z kafelka szybkich ustawień — nieprzetestowane na żywo (emulator nie przesyła;
  telewizor autora jest odbiornikiem Google Cast — zrzut autora z Zdjęć);
- nazwa kafelka przesyłania ekranu na telefonie autora — podpowiedź mówi o funkcji ([[drzewo]] D26);
- paski, obrót i przeciągnięcie od krawędzi na fizycznym telefonie, przy nawigacji, której używa autor — nieprzetestowane na żywo;
- systemowe okno „pełny ekran” przy pierwszym wejściu — przed pierwszym pokazem wejść w tryb raz bez przesyłania;
- TalkBack w trybie prezentacji — nieprzetestowane na żywo;
- wyjście z trybu przyciskiem Wstecz — „ok” bez śladu (stop #2, krok 2; sprawdzone przez agenta i w teście).

**Drzewo — karta Twoim głosem** ([[ISSUE-035-tree-names-shrink-my-voice]] → *Verification*)
- karta w G2 („Moja babcia”, „…babci mojej żony”, „to ja”) brzmi tak, jak autor mówi o rodzinie — „ok” bez śladu na urządzeniu (stop #2, krok 1; autor:
  „zapisz bez śladu”);
- stan „osoba bez rodziny” („nie wiadomo jeszcze, kim jest dla mnie”) — tylko test widżetu, w bazie testowej nie ma takiej osoby;
- opis z trzech odcinków („Siostra cioteczna babci mojej żony”) — tylko test jednostkowy, na emulatorze widać opisy z dwóch odcinków.

**Do decyzji autora, gdy zobaczy swoje cmentarze** (nie sprawdzenie, tylko wybór): grubość alejek i znicze, które nachodzą na
siebie ([[cmentarz]] → *Open*, [[ISSUE-030-sector-on-a-visit]]).

## Notes / references
- [[2026-10-13-retro-03]] R8, R9 · `DEFINITION_OF_DONE.md` → *Kto sprawdza* · wyjątki „na telefonie” w DoD (GPS, słońce,
  offline — build release).
