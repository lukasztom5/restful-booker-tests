# Restful Booker API tests (Postman + Newman)

This repository shows example requests, a collection and an environment for Postman and a REST API.

The collection is run in two ways: run A tests a single booking (Setup, Negative, CRUD folders), run B runs data-driven tests using a CSV file (Setup, Data-driven folders).

This repository is a learning project. The API under test is Restful Booker.

Expected results: run A: 38 assertions, 0 failures; run B: 33 assertions, 0 failures.

*Polish version below.*

To repozytorium przedstawia przykładowe działania żądań, kolekcji i środowiska dla Postman i interfejsu REST API.

A to testy jednej rezerwacji (Setup, Negatywne, CRUD), B to testy sterowane danymi z plików csv (Setup, Data-driven)

To repozytorium jest przykładem nauki, a API - Restful Booker

Do zainstalowania:
- Node LTS - najnowsza wersja LTS. CI używa wersji z pliku newman.yml (obecnie 24)
- okno terminala w Linuxie lub Windowsie
- Newman - npm install -g newman
  
Dane użytkownika i hasła z publicznej dokumentacji API. - https://restful-booker.herokuapp.com/apidoc/#api-Auth-CreateToken - Auth - CreateToken
`<UŻYTKOWNIK>` i `<HASŁO>` trzeba zastąpić, razem z ostrymi nawiasami - najlepiej dać w cudzysłowach.

## Uruchomienie polecenia A

```
newman run "Restful Booker.postman_collection.json" -e "Rb - dev.postman_environment.json" --env-var username=<UŻYTKOWNIK> --env-var password=<HASŁO> --folder Setup --folder Negatywne --folder CRUD --reporters cli,junit --reporter-junit-export raport_1.xml
```

## Uruchomienie polecenia B

```
newman run "Restful Booker.postman_collection.json" -e "Rb - dev.postman_environment.json" --env-var username=<UŻYTKOWNIK> --env-var password=<HASŁO> --folder Setup --folder Data-driven --reporters cli,junit --reporter-junit-export raport_2.xml -d rezerwacje_Postman.csv
```

Wyniki prawidłowe:
- A 38 asercji, 0 faili
- B 33 asercje, 0 faili

missing_id jest w środowisku i oznacza id rezerwacji, która nie istnieje, więc oczekiwane statusy to 404 i 405.

Kilka testów celowo sprawdza zachowania z błędem i dlatego są zielone np. Booking - depositpaid null [POST] i Booking - missing fields [POST]

Raporty `raport_1.xml` i `raport_2.xml` powstają lokalnie i są w pliku .gitignore

Przebieg uruchamia się po dokonaniu pusha na main. Przebieg można uruchomić ręcznie z zakładki Actions. Do uruchomienia są potrzebne sekrety RB_USERNAME i RB_PASSWORD. Po przebiegu raporty `raport_1.xml` i `raport_2.xml` zapisują się jako artefakty do pobrania.
Osoba, która skopiuje repozytorium, musi dodać sekrety w ustawieniach (wartości z dokumentacji API, a nie ze swojego konta), a missing_id jest w CI jawnie podawany.

