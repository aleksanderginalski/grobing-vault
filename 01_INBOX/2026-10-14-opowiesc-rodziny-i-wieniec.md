# Opowieść rodziny na drzewie i wieniec przy portrecie według nazwiska

> Pomysły autora ze stopu #2 [[ISSUE-037-time-on-the-tree]] (2026-10-14), punkty c) i d) tej samej prośby co [[ISSUE-038-history-on-tv-and-tempo]] (a, b).
> W INBOX, bo każdy ma więcej niewiadomych niż jedna pozycja: najpierw **prototyp `ui` w trybie discovery** (panel po panelu — tak autor decyduje najlepiej,
> SPIKE-004), potem pozycje backlogu. Bez danych rodziny.

## c) Animowane połączenia i zbliżenia na zdarzenia
Słowa autora: *„Animowanie tych połączeń (np. aby te linie były bardziej wizualnie atrakcyjne, gdy dwójka ludzi się poznaje jest jeden efekt, a gdy zostaje małżeństwem to
inny, „zbliżenia” na momenty w których zawierane są małżeństwa, rodzą się dzieci, umierają osoby)”*.

**Gdzie to siedzi:** element 6 i 11 [[drzewo]] (czas, prezentacja); linie i ich rysowanie — `tree_layout.dart`, `tree_painter.dart`.

**Pytania na prototyp (do autora, nie do zgadywania):**
1. **Które zdarzenia dostają zbliżenie?** W wymyślonej rodzinie to ok. 175 zdarzeń (106 urodzeń, 31 zgonów, 38 związków) — przy ▶ w 8 s nie da się zbliżyć każdego.
   Kandydaci: tylko rodzina osoby w środku (poziom 1–2) · tylko przodkowie „Ja” · wszystkie, ale ▶ zwalnia przy zdarzeniu.
2. **Jak różnią się efekty:** poznanie („razem”), ślub, narodziny, śmierć — i jak ma się to do stylu B (*nowoczesny · minimalistyczny · godny*, bez ponurości; znicz to znak
   aplikacji — reguła 8).
3. **Daty niepewne** (N3, [[drzewo]] D32): czy zbliżać zdarzenie „ok. 1890” i jak je pokazać.
4. **Ograniczenie animacji** (WCAG SC 2.3.3, D36): co zostaje, gdy system wyłącza animacje — zbliżenia to ruch.
5. **Płynność:** zbliżenia i efekty to więcej pracy rastra niż dziś (▶: 7–9% wolnych klatek na emulatorze) — pomiar na prototypie we Flutterze, nie tylko w HTML.
6. **Imiona na telewizorze** (wejście z [[ISSUE-038-history-on-tv-and-tempo]], 2026-10-14): w trybie prezentacji imię ma 13 sp, czyli z 3 m na 55″ ok. 14′ — poniżej minimum 16′
   (ISO 9241, [[drzewo]] D38, *Candidates — ISSUE-038* → *Zauważone*). Rok w rogu czyta się z kanapy, imiona tylko z bliska. Opowieść na telewizorze może potrzebować większych imion
   osób, o których akurat mowa — dziś to I2 ([[drzewo]] D27).

## d) Wieniec przy portrecie związany z nazwiskiem
Słowa autora: *„Chciałbym móc w wyborze portretu dla niej customowy wieniec który byłby związany z danym nazwiskiem”*.

**Gdzie to siedzi:** portret w widoku osoby ([[osoba]]), wybór portretu ([[kadr-profilowego]]), być może węzły drzewa i karta.

**Uwaga — wcześniejsza decyzja:** [[style-b]] reguła 8 (v1.15, [[osoba]] D3) rozstrzygnęła **„bez gałązek”** wokół portretu, choć referencja R4 je miała
([[references]]). Wieniec według nazwiska to zmiana tej decyzji — do potwierdzenia na prototypie.

**Pytania na prototyp:**
1. **Czym jest wieniec:** gałązki jak w R4, wieniec z liści, ramka z motywem — i czy wolno go pokazywać na nagrobku-zdjęciu (reguła 8: bez symboli religijnych w
   interfejsie).
2. **„Związany z nazwiskiem”:** z nazwiskiem rodowym czy obecnym (kobieta ma dwa — „z d.”, [[FR-005-nazwisko-rodowe]]); jeden wieniec na rodzinę nazwiska, wybierany
   raz i dziedziczony przez wszystkich o tym nazwisku?
3. **Kto go tworzy:** wybór z gotowego zestawu, kolor i motyw do wyboru, czy własny rysunek.
4. **Gdzie widać:** tylko widok osoby, czy też węzły drzewa, karta, eksport dla rodziny ([[US-006-eksport-dla-rodziny]]).
5. **Dane:** ustawienie „nazwisko → wieniec” to nowa tabela — **zmiana schematu** (migracja i test migracji), a kopia i eksport muszą ją nieść (próbne odtworzenie).

## Kolejność — decyzja autora 2026-10-14 (*„ok”*)
Propozycja łańcucha, przyjęta: [[ISSUE-038-history-on-tv-and-tempo]] zaraz po [[ISSUE-037-time-on-the-tree]]; c) i d) — po instalacji MVP ([[ISSUE-032-mvp-install]]),
bo prawdziwe dane czekają na instalację, a wartość z briefu §2 to notatki *„uzupełniane, póki babcia może opowiedzieć”*.

## Zmiana 2026-10-16 — d) przeniesione do backlogu (decyzja autora w `/pm`)
**d) jest teraz [[ISSUE-044-family-wreaths]]** — przed instalacją, nie po niej (*„tak róbmy to”*, [[2026-10-16-retro-04]] → *Product decisions*). Autor
doprecyzował definicję: wieńce **symbolizujące rodziny, z których wywodzi się osoba, domyślnie dzieci przejmują po ojcu** (zamiast „według nazwiska”).
Pytania 1–5 z d) przeszły do pozycji. **c) zostaje tutaj** — po instalacji MVP, jak w decyzji z 2026-10-14.
