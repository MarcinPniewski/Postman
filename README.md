# Postman – testy API

## Opis

Projekt zawiera testy API przygotowane w narzędziu Postman.  
Testy można uruchamiać zarówno w środowisku graficznymjak i z linii komend z użyciem `Newman` (CLI Postmana).

W projekcie zdefiniowano Test Steps symulujące odpowiedzi GET przykładowej aplikacji testowej na metodę `statusZadania`.  
Dla każdego testu przekazywany jest parametr `kod` identyfikujący zadanie (`zadanie_1`, `zadanie_2`, `zadanie_3`).  
Każde żądanie jest automatycznie walidowane pod kątem poprawności struktury odpowiedzi, obecności nagłówków, statusów i sygnatur błędów (`FAILED`, `Failures`, itp.).

W przypadku uruchomienia w środowisku graficznym log znajduje się w konsoli.

W przypadku uruchomienia z linii komend logi z przebiegu zostają umieszczone w katalogu `reports`.

## Struktura projektu
- `project/` - pliki projektów Postman (.json)
 - `Testy aplikacji testowej.postman_collection.json` – definicja kolekcji Postman zawierająca zapytania i testy
 - `Testy aplikacji testowej.postman_environment.json` – środowisko zdefiniowane na potrzeby testów (zmienna `BaseURL`)
- `reports/` - raporty z wykonanych testów CLI

## Wymagania
- Postman 11.x
- Newman (do uruchamiania testów z lini komend)
- reporter newman-reporter-htmlextra (do szczegółowego raportu z testów z lini komend)
- system MacOS/Linux/Windows
- uruchomiona zaślepka przykładowej aplikacji testowej ([MockService](https://github.com/MarcinPniewski/MockService)) pod adresem zdefiniowanym w zmiennej BaseURL (domyślnie http://localhost:8089)

## Uruchamianie testów w Postman GUI
- zaimportować:
 - kolekcję: _Testy aplikacji testowej.postman_collection.json_
 - środowisko: _Testy aplikacji testowej.postman_environment.json_
- wybrać środowisko _Testy aplikacji testowej_ z listy Environment.
- uruchomić całą kolekcję `Testy aplikacji testowej`
- przejrzeć logi w “Console”

## Uruchamianie testów z CLI (Newman)
  ```bash
newman run project/"Testy aplikacji testowej.postman_collection.json" \
  --environment project/"Testy aplikacji testowej.postman_environment.json" \
  --reporters cli,htmlextra \
  --reporter-htmlextra-export reports/postman_detailed_report.html
  ```
Wynik testów pojawi się w terminalu oraz w raportach w katalogu `reports`.

## Licencja
To repozytorium udostępniane jest wyłącznie do celów testowych i edukacyjnych.  
Wszelkie inne formy użycia (modyfikacja, komercja, publikacja) są zabronione.  
Szczegóły w pliku [LICENSE.txt](./LICENSE.txt).
