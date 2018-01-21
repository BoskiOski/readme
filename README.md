
## Projekt na egzamin z Zaawansowanych języków Programowania
### Anthill – Mrowisko
> Mateusz Breza, Oskar Marcinkiewicz, Bartosz Wiśniewski

Mrowisko to program generujący planszę o podanych wymiarach wraz z sprecyzowaną przez użytkownika ilośc mrówek. Następnie symuluje ich ruch po wyznaczonym obszarze.


## Opis głównych plików projektu

- Anthill.rb - Główna klasa odpowiedzialna za czytanie danych z konsoli oraz wyowłyanie metod w innych klasach.
- Ants.rb - Klasa odpowiedzialna za pojawienie się mrówek na planszy i wprawienie ich w ruch.
- Board.rb - Klasa odpowiedzialna za utworzenie i wyświetlenie  planszy.

## Refaktoryzacje i dodane funkcjonalności

Po wstępnych refaktoryzacjach w naszym programie pozostała następująca ilość smelli:
```
Inspecting 3 file(s):
SSS

lib/anthill.rb -- 1 warning:
  [6]:TooManyInstanceVariables: AntHill has at least 5 instance variables [https://github.com/troessner/reek/blob/master/docs/Too-Many-Instance-Variables.md]
lib/ants.rb -- 1 warning:
  [27]:TooManyStatements: Ants#mrowki_sie_poruszaja has approx 8 statements [https://github.com/troessner/reek/blob/master/docs/Too-Many-Statements.md]
lib/board.rb -- 1 warning:
  [32]:NestedIterators: Board#rysuj_plansza contains iterators nested 2 deep [https://github.com/troessner/reek/blob/master/docs/Nested-Iterators.md]
3 total warnings
```
Postanowiliśmy dodać funkcjonalność 
Pierwszą funkcjonalnością którą postanowiliśmy zaimplementować jest pokolorowanie mrówek na różne barwy. Żeby otworzyć kod na taką modyfikację musieliśmy usunąć smella "NestedIterators".

Po zmianach kod wyglądał w następujący sposób:

#!/usr/bin/env ruby
require 'rainbow'

#Class responsible for creating and printing board.
class Board
   ```
    def initialize
        @plansza = Array.new()
    end
   
    def wypelnij_plansze(wymiary) 
        for i in 0..wymiary[0]-1
            @plansza[i] = Array.new()
            for j in 0..wymiary[1]-1
                @plansza[i][j] = " "
            end
        end
        return @plansza
    end
   
    def rysuj_ramka(szerokosc)
       ramka = "-" 
       for i in 0..szerokosc
            ramka = ramka + "-"
        end
        puts ramka
    end
   
    def rysuj_plansza(wymiary, plansza)      
        colors = [:red, :green, :yellow, :blue, :magenta, :cyan]
        rysuj_ramka(wymiary[1])
       
           for i in (0..wymiary[0]-1)
            print "|"
            for j in (0..wymiary[1]-1)
                print Rainbow(plansza[i][j]).chars.map { |char| Rainbow(char).color(colors.sample) }.join
            end
            print "|\n"
        end
       
        rysuj_ramka(wymiary[1])
    end
end
```

