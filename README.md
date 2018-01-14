
## Projekt na egzamin z Zaawansowanych języków Programowania
### Anthill – Mrowisko
> Mateusz Breza, Oskar Marcinkiewicz, Bartosz Wiśniewski

Tutaj będzie opis co robią mrówki 


## Opis głównych plików projektu

Tutaj krótki opis plików

może wyszczególnione ale chyba nie ma co


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
### TooManyInstanceVariables

### TooManyStatements

### NestedIterators

### UtilityFunction
