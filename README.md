
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
!['o' output](https://i.imgur.com/LwzJk19.jpg)



## Opis procesu refaktoryzacji

### IrresponsibleModule
2  lib/anthill.rb
 @@ -15,7 +15,7 @@ def initialize
      
      def start
        plansza = @board.wypelnij_plansze(@wysokosc, @szerokosc)
 -      plansza = @ants.dodaj_mrowki(@wysokosc, @szerokosc, plansza, @mrowki)
 +      plansza = @ants.dodaj_mrowki(@szerokosc, plansza, @mrowki)
        
        while true do    
        plansza = @ants.mrowki_sie_poruszaja(@wysokosc, @szerokosc, plansza)    
View  
4  lib/ants.rb

### TooManyInstanceVariables

### LongParameterList

### TooManyStatements

### NestedIterators

### UtilityFunction
