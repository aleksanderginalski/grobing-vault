# 1 listopada — zbieranie danych bez aplikacji czy z kawałkiem aplikacji?

> Otwarte pytanie do autora, z sesji `pm` 2026-10-05. **Wraca przed [[ISSUE-002-bootstrap-code-repo]]** —
> od odpowiedzi zależy tempo budowy, nie kolejność pierwszych kroków.

## Context
- Notatki **nie mają adresów kwater** (korekta autora — [[ISSUE-001-materialize-backlog]]), więc
  położenie grobu powstaje dopiero na miejscu. 1 listopada pozycje się **zbiera**, nie sprawdza.
- Na nagrobkach są daty urodzin i śmierci — to, co autor chce uzupełniać (daty ślubów zwykle nie;
  ich źródłem jest babcia).

## Options
1. **(rekomendacja `pm`) Zbieraj aparatem telefonu z włączoną lokalizacją; budowa bez terminu.** Każde
   zdjęcie nagrobka niesie GPS w Exif; do aplikacji trafi, gdy będzie gotowa. Koszt: zero budowy pod
   datę. Tracimy: 1 listopada nic w aplikacji. Zgodne z modelem danych (Assertion ze źródłem
   „nagrobek", Media przy grobie, pozycja „GPS na miejscu" z dokładnością).
2. **Cienki kawałek aplikacji do 1 listopada** — projekt + baza + ekran „grób: zdjęcie + pinezka z GPS"
   + kopia. Szacunkowo 4-5 dni pracy w 4 tygodnie; budowa pod datę, ryzyko, że kopia nie zdąży przed
   pierwszymi danymi (MD2).

## Consequences to decide with it
- Opcja 1 dokłada funkcję spoza M1: **„grób ze zdjęcia z galerii — pinezka z lokalizacji zdjęcia"**.
  To zmiana zakresu — decyzja autora, nie dopisek po cichu.
- ⚠️ W obu opcjach: kopia w Zdjęciach Google wysłałaby zdjęcia nagrobków i ich położenia
  **niezaszyfrowane** — wbrew decyzji z briefu (§Security, kopia szyfrowana po stronie telefonu).
  Wstrzymać na ten dzień.

## Where it goes when answered
Decyzja → `planning` przy ISSUE-002 (i ewentualnie nowa pozycja dla importu ze zdjęcia); ta notatka
znika z INBOX.
