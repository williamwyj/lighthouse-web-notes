# W8D5 Ruby

- Intro to Ruby on Rails
- Intro to the Ruby Language
- Demo - basketball one-on-one

## Intro Roby and Rails

  - Ruby was created 1995 Yukihiro Matsumoto(Matz)
  - Designed for developer happiness and productivity
  - Really took off with the release of Rails (2005), 
  - David Eninemier Henson from Basecamp
  
  With Ruby on Rails
  - Very legible code, almost english like
  - Rapid Development
  - Rich set of tools and libraries out of the box
  - Very good database functionality (Active Record)
  - Lots of abstraction
  - very opinionated (lots of convention)

## JS vs NodeJS/Express

- JS Async / Ruby Sync
- JS Multi-paradigm / Ruby mostly OOP
- JS primitive types, obj types / Ruby all are objects

## Why Rails?

- OOP
- Learn about new patterns MVC
- Learning a new framework

## Intro to the Ruby Languange

- Ruby Hash = JS Object
- symbol - :text, its like the stripped down version of the string object
- string injection only work with double quote, not single quote eg, puts "Hello #{name}" where name is a variable
- ! operator for array.shuffle! changes the original array where as only shuffle does not.
- snake_case convention

- iterators
  - hash are iterable
```ruby
names = ['name1','name2']
names.each do |name|
  puts "hello #{name}"
end


(1..5).each do |num|
  puts num
end


5.times do |num|
  puts num
end

(1..100).steps(10) do |num|
  puts num
end

famous_painter = {
  first_name:"Pablo"
  last_name:"Picasso",
}



```

- block
  2 ways
    - do end - typically for multi line
    - {} - typically for single line, is a shorthand
```ruby
(1..5).each do |num|
  puts num
end

(1..5).each {|num| puts num}
```

- function
```ruby
def multiple(val)
    multipleArr=[]
    1.upto(val) do |num|
      multipleArr.push yield num # yield return the {|n| n*5} where n = num
    end
    multipleArr # last line is implicity return
end

result = multiple(5) {|n| n*5}

puts result.inspect

#old syntax, result in same thing as above
def multiple(val, &block)
    multipleArr=[]
    1.upto(val) do |num|
      multipleArr.push block.call num # yield return the {|n| n*5} where n = num
    end
    multipleArr # last line is implicity return
end

result = multiple(5) {|n| n*5}

puts result.inspect
```

### Ruby class
```game.rb
require_relative './player'

class Game

  def initialize
    
    @player1 = Player.new('LeBron')
    @player2 = Player.new('Kevin') #the @ declare variable as global variable in the class, without it the var is local to the initialize function
    @players = [@player1, @player2].shuffle
    @round1 = 1
    
  end
  
  def displayer_scoreboard
  
  # display scoreboard
      puts "------- Scoreboard --------"
      puts "Name: #{@player1.name} Points: #{@player1.score}"
      puts "Name: #{@player2.name} Points: #{@player2.score}"
  
  end
  
  def next_round
  
      # display the round
      puts " ------- Round #{@round} ------- "
  
      # switch the player and do it again
      @round += 1
      @players.rotate!
  end
  
  def game_over?
    @player1.score.winner? && @player2.score.winner?
  end
  
  def winner
    @player1.winner? ? @player1.name : @player2.name
  end
  
  def display_winner
    puts "The winner is #{winner}"
  end
  
  def play
  
    until (game_over?) do
      
      next_round

      # attacking player - player object
      attack_player = @players.first

      # defense player - player object
      defence_player = @players.last

      
      attack_player.shoots
      
      
      displayer_scoreboard
      
      sleep 0.7
    end
    
    display_winner
    
  end
end

# game1 = Game.new

# game1.play # print the 2 player names
```
```player.rb
class Player
  
  #getters
  attr_reader :name #, :score
  
  #setters
  # attr_writer :score
  
  #both getter and setter
  attr_accessor :score
  
  def initialize(name)
    @name = name # these are private variables and are only retreieved and manipulated thru in class functions
    @score = 0
  end
  
  def shoots
    # attack player is going to score
    score = rand(1..2)

    puts "Score: #{score}"
    
    # increase the score of that player
    self.score += score
    
    puts "#{self.name} shoots and score #{score} points!"
  end
  
  def winner?
    score > 11
  end
  
  # getter
  #def score
  #  @score
  #end
  
  #setter
  #def score=(points)
  #  @score=points
  #end
end
```
```main.rb
require_relative './game'

game1 = Game.new
game1.play

```
