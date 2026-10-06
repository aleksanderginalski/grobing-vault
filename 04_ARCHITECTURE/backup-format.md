---
title: "Backup file format v1"
type: architecture
status: active
source: "ADR-004 pkt 1-3 · ISSUE-008 D2 (format v1, 2026-10-06)"
created: 2026-10-06
updated: 2026-10-06
---

# Format kopii — v1

> **Kontrakt na dziesięciolecia.** Pierwsza prawdziwa kopia zamraża v1. Odtworzenie musi czytać
> **każdą** wersję formatu, która kiedykolwiek powstała, więc zmiana czegokolwiek poniżej oznacza nowy
> `format_version`, nigdy edycję v1. Decyzja: [[ADR-004-backup-format-encryption-destination]];
> przypięcie szczegółów: [[ISSUE-008-backup-write]] → *Decisions for stop #1*, D2.
>
> Ten plik ma też wystarczyć komuś, kto **nie ma Grobing**: notka przekazania
> ([[NT-007-hand-over-note]]) wskazuje tutaj.

## Three things open a backup
| Rzecz | Domyślna nazwa | Gdzie |
|---|---|---|
| plik kopii | `grobing-kopia.age` | Dysk autora, nadpisywany przy każdej kopii |
| plik klucza | `grobing-klucz.age` | obok kopii, zapisany raz przy konfiguracji |
| hasło | — | tylko na papierze, w notce przekazania (brief §Security) |

**Utrata hasła albo pliku klucza = utrata kopii.** Hasła nie da się odzyskać.

## Layers
1. **Plik kopii: [`age` v1](https://c2sp.org/age)**, binarny (bez ASCII armor), do jednego odbiorcy
   X25519. Klucz publiczny (`age1…`) jest w telefonie, więc kopia nie potrzebuje hasła.
2. **Plik klucza: `age` v1 do hasła** (scrypt, work factor 18 — domyślny w oficjalnym `age`). W środku
   plik tożsamości w formacie `age-keygen`: dwa komentarze (`# created:`, `# public key:`) i jedna linia
   `AGE-SECRET-KEY-1…`. Oficjalne `age -d -i` rozpoznaje taki plik i pyta o hasło.
3. **Wnętrze kopii: archiwum `tar` w formacie ustar** (POSIX `pax` → *ustar Interchange Format*):
   - tylko zwykłe pliki, tryb 0644, czas modyfikacji = `created_at`;
   - ścieżki ASCII: segmenty `[A-Za-z0-9._-]+` rozdzielone `/`, nigdy `.` ani `..`;
   - kolejność: `grobing.db` → `media/…` (po ścieżce) → **`manifest.json` na końcu**;
   - koniec archiwum: dwa bloki zer.

## Files inside
| Ścieżka | Co to jest |
|---|---|
| `grobing.db` | migawka bazy SQLite (`VACUUM INTO`) — schemat: `data-model.md`, wersja w `PRAGMA user_version` |
| `media/<ścieżka>` | każdy plik zdjęcia z prywatnego katalogu aplikacji, ścieżka względna jak w tabeli `media` |
| `manifest.json` | opis kopii (niżej) — ostatni, bo sumy liczone są w tym samym przebiegu, w którym plik trafia do archiwum |

## manifest.json
| Pole | Typ | Znaczenie |
|---|---|---|
| `format_version` | liczba | `1` |
| `created_at` | tekst, ISO 8601 UTC | kiedy powstała migawka |
| `schema_version` | liczba | `PRAGMA user_version` migawki; starszą odtworzenie migruje, nowszą odrzuca (ADR-004 pkt 5) |
| `record_counts` | obiekt: tabela → liczba | liczba wierszy każdej tabeli z `sqlite_master` (bez `sqlite_*`) |
| `data_fingerprint` | tekst, 64 znaki hex | odcisk danych z ekranu „Stan danych” (SHA-256 treści tabel i zdjęć) — definicja: README `grobing-code` → *Baza danych*. Odtworzenie sprawdza wynik tą jedną liczbą ([[NFR-002-odtworzenie-na-nowym-telefonie]]) |
| `files[]` | lista `{path, size, sha256}` | każdy plik archiwum poza samym manifestem; rozmiary pozwalają sprawdzić wolne miejsce przed rozpakowaniem |

Pola `created_at`, `data_fingerprint` i `size` doszły ponad listę z ADR-004 (ISSUE-008, D2) — wszystkie
trzy dla odtworzenia.

## Opening a backup without Grobing (PC)
Oficjalne [`age`](https://github.com/FiloSottile/age), zwykły `tar`, dowolny SQLite. **Poza każdym
repozytorium** — to dane rodziny; po obejrzeniu usuń.

```sh
age -d -i grobing-klucz.age grobing-kopia.age > kopia.tar   # age pyta o hasło do pliku klucza
mkdir kopia && tar -xf kopia.tar -C kopia                   # grobing.db, media/, manifest.json
sqlite3 kopia/grobing.db "PRAGMA integrity_check"           # albo dowolna przeglądarka SQLite
```

Z kodem Grobing pod ręką `dart run tool/fingerprint.dart kopia` liczy odcisk tą samą funkcją co ekran i
sprawdza manifest (rozmiary, SHA-256, liczby, odcisk).

## Known limits of v1
- Każda kopia to całość: Dysk w oknie zapisu pliku nie pozwala na kopię przyrostową (ADR-004, *Options*).
- „Ostatnia udana kopia” znaczy: Dysk w telefonie przyjął plik, a nie: plik jest już w chmurze.
- Migawka bazy i odczyt zdjęć nie są jedną transakcją — do rozstrzygnięcia przy
  [[US-005-zdjecia]], zanim zdjęcia będzie można usuwać.

## Evidence
Zgodność z oficjalnym CLI `age` v1.3.2 w obie strony, 92 oficjalne wektory testowe C2SP i plik kopii z
emulatora otwarty na PC z odciskiem zgodnym z ekranem: [[ISSUE-008-backup-write]] → *Verification*.
