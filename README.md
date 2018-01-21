
## Projekt na egzamin z Zaawansowanych języków Programowania
### Anthill – Mrowisko
> Mateusz Breza, Oskar Marcinkiewicz, Bartosz Wiśniewski

Mrowisko to program generujący planszę o podanych wymiarach wraz z sprecyzowaną przez użytkownika ilośc mrówek. Następnie symuluje ich ruch po wyznaczonym obszarze.


## Opis głównych plików projektu

Anthill.rb - Główna klasa odpowiedzialna za czytanie danych z konsoli oraz wyowłyanie metod w innych klasach.
Ants.rb - Klasa odpowiedzialna za pojawienie się mrówek na planszy i wprawienie ich w ruch.
Board.rb - Klasa odpowiedzialna za utworzenie i wyświetlenie  planszy.

## Refaktoryzacja

Zanim rozpoczęliśmy refaktoryzację w naszym kodzie odnaleźliśmy 8 warningów następujących rodzajów:
- IrresponsibleModule
- TooManyInstanceVariables
- LongParameterList
- TooManyStatements
- NestedIterators
- UtilityFunction




## Opis procesu refaktoryzacji

### IrresponsibleModule

Do każdej klasy został dodany opis, precyzujący za co ona jest odpowiedzialna, ułatwi to w przyszłości zrozumienie kodu.

!['o' output](https://i.imgur.com/m1eYaEZ.png)
!['o' output](https://i.imgur.com/cQ0UTrD.png)
!['o' output](https://i.imgur.com/6bKRrl4.png)
!['o' output](https://i.imgur.com/qW5GEPh.png)

### LongParameterList

Metoda dodaj mrówki przyjmowała za dużo parametrów więc parametr wysokość i szerokość zostały zamienione na tablice wymiary.
Naprawiony został również błąd, który umożliwiał dodanie dwóch mrówek w tym samym miejscu co powodowało, że kóńcowa ilość mrówek mogła być mniejsza niż zakładaliśmy.

!['o' output](https://i.imgur.com/AtD5Jhg.png)
!['o' output](https://i.imgur.com/XBym7nV.png)


### TooManyStatements

Metoda mrówki się poruszają była zbyt rozbudowana dlatego została ona rozbita na mniejsze metody. Pozwoliło nam to usunąć smella oraz w przyszłości umożliwi łatwiejsze rozbudowywanie programu.

!['o' output](https://i.imgur.com/aJO9x78.png)
!['o' output](https://i.imgur.com/yJvETmE.png)
!['o' output](https://i.imgur.com/N9u2YrS.png)
!['o' output](https://i.imgur.com/t3iF9Ao.png)


### NestedIterators

Pierwotny sposób wypisywwania danych zawartych w  tablicy z mrówkami powodował smella. Został on zmodyfikowany żeby spełniać wymagania reeka. 
!['o' output](https://i.imgur.com/nQ4a9Ze.png)
!['o' output](https://i.imgur.com/tV9dgdS.png)
### UtilityFunction

Zadeklarowanowa lokalnie zmienna plansza została zmieniona na zmienną instancji. To poskutkowało usunięciem smella optymalizując jednocześnie otwartość programu.
!['o' output](https://i.imgur.com/nUDBCYF.png)
!['o' output](https://i.imgur.com/XohrsVE.png)

### TooManyInstanceVariables

Zmienne instancji wysokośc oraz szerokość zostały przeniesione do tablicy wymiary a zmienna mrówki została całkowicie usunięta. To pozwoliło nam na pozbycie się zbędnego kodu i usunięcie smella. 
!['o' output](https://i.imgur.com/pghsX4k.png)
!['o' output](https://i.imgur.com/eNeoeYF.png)
## Podsumowanie
Po skończonej refaktoryzacji otrzymaliśmy program nie posiadający smelli. Po każdej zmianie były uruchamiane testy kontrolujące poprawność działania programu.
!['o' output](https://i.imgur.com/IyxRwl0.png)

