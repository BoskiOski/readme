
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
Pierwszą funkcjonalnością którą postanowiliśmy zaimplementować jest pokolorowanie mrówek na różne barwy. Żeby otworzyć kod na taką modyfikację musieliśmy usunąć smella "NestedIterators".

Po zmianach kod wyglądał w następujący sposób:
```ruby
#!/usr/bin/env ruby
require 'rainbow'

#Class responsible for creating and printing board.
class Board
   
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
Po uruchomieniu reeka otrzymialiśmy następujący output.
```
lib/anthill.rb -- 1 warning:
  [6]:TooManyInstanceVariables: AntHill has at least 5 instance variables [https://github.com/troessner/reek/blob/master/docs/Too-Many-Instance-Variables.md]
lib/ants.rb -- 1 warning:
  [27]:TooManyStatements: Ants#mrowki_sie_poruszaja has approx 8 statements [https://github.com/troessner/reek/blob/master/docs/Too-Many-Statements.md]
lib/board.rb -- 1 warning:
  [29]:TooManyStatements: Board#rysuj_plansza has approx 7 statements [https://github.com/troessner/reek/blob/master/docs/Too-Many-Statements.md]
3 total warnings
```
Następną funkcjonalnością jest upewnienie się ,że mrówki nie znikają przy próbie wyjścia poza planszę i nie mają możliwośći zjadania się. Podczas wprowadzania tej funkcjonalności został usunięty smell "TooManyStatements".

 ```ruby
  def rusz_mrowka(wysokosc, szerokosc, plansza,i,j)
	ii = rand(i-1..i+1)
	jj = rand(j-1..j+1)                       
	if ii.between?(0, wysokosc-1) && jj.between?(0, szerokosc-1) && plansza[ii][jj] != "m"              
		plansza[i][j] = " "
		plansza[ii][jj] = "m"                        
	end   
  end
	  
 def mrowki_sie_poruszaja(wysokosc, szerokosc, plansza)
        sleep(0.1)
        system "clear"
        for i in 0..wysokosc-1
            for j in 0..szerokosc-1
                if plansza[i][j] == "m" then
                rusz_mrowka(wysokosc, szerokosc, plansza,i,j)
                end
            end
        end            
        return plansza
    end
                
   
end
 ```
 Po wprowadzeniu tych zmian, raport reeka wyglądał następująco:
 ```
 Inspecting 3 file(s):
SSS

lib/anthill.rb -- 1 warning:
  [6]:TooManyInstanceVariables: AntHill has at least 5 instance variables [https://github.com/troessner/reek/blob/master/docs/Too-Many-Instance-Variables.md]
lib/ants.rb -- 2 warnings:
  [33, 35, 36]:FeatureEnvy: Ants#rusz_mrowka refers to 'plansza' more than self (maybe move it to another class?) [https://github.com/troessner/reek/blob/master/docs/Feature-Envy.md]
  [26]:LongParameterList: Ants#rusz_mrowka has 5 parameters [https://github.com/troessner/reek/blob/master/docs/Long-Parameter-List.md]
lib/board.rb -- 1 warning:
  [29]:TooManyStatements: Board#rysuj_plansza has approx 7 statements [https://github.com/troessner/reek/blob/master/docs/Too-Many-Statements.md]
4 total warnings
```
 Ostatnią funkcjonalnością, która została wprowadzona jest weryfikacja danych wprowadzanych przez użytkownika programu. Sprawdzamy czy osoba obsługująca aplikację wprowadziła 3 parametry. W ramach działań prowadzonych w celu stworzenia tej funkcjonalności usunieliśmy smella "TooManyInstanceVariables"
 ```ruby
 #!/usr/bin/env ruby
require_relative 'board'
require_relative 'ants'

#Main class responsible for reading data from console, and calling methods contained in another classes.
class AntHill

    
    
	def initialize 
        @board = Board.new
        @ants = Ants.new
        @wymiary = Array.new()
        @mrowki = 0
	end	
    
    def weryfikacja    
        if ARGV.length != 3 then
            @wymiary = [50, 100]
            @mrowki = 50
        else
            @wymiary = [ARGV[0].to_i, ARGV[1].to_i]
            @mrowki = ARGV[2].to_i
        end  
    end
    
    def start
      plansza = @board.wypelnij_plansze(@wymiary)
      plansza = @ants.dodaj_mrowki(@wymiary, plansza, @mrowki)
      @board.rysuj_plansza(@wymiary, plansza) 
      while true do    
      plansza = @ants.mrowki_sie_poruszaja(@wymiary[0],@wymiary[1] , plansza)    
      @board.rysuj_plansza(@wymiary, plansza)  
      end    
    end
    
end
ah = AntHill.new
ah.weryfikacja
ah.start
```
       
