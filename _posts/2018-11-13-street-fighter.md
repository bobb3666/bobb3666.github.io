---
layout: post
title: Street Fighter
description: Player selection - Ryu???
categories: [Ruby, Codewars]
image: https://i.ytimg.com/vi/IDvepzNWCJc/hqdefault.jpg
---
![Street Fighter](https://i.ytimg.com/vi/IDvepzNWCJc/hqdefault.jpg)

The following is from a [Codewars](https://www.codewars.com/) kata. 

> Some of you might remember spending afternoons playing Street Fighter 2 in some Arcade back in the 90s or emulating it nowadays with the numerous emulators for retro consoles. You'll have to simulate the video game's character selection screen behaviour, more specifically the selection grid
>Selection Grid Layout in text:
~~~
| Ryu  | E.Honda | Blanka  | Guile   | Balrog | Vega    |
| Ken  | Chun Li | Zangief | Dhalsim | Sagat  | M.Bison |
~~~

**Input**

    the list of game characters in a 2x6 grid;
    the initial position of the selection cursor (top-left is (0,0));
    a list of moves of the selection cursor (which are up, down, left, right);

**Output**

    the list of characters who have been hovered by the selection cursor after all the moves (ordered and with repetition, all the ones after a move, wether successful or not, see tests);

**Rules**

Selection cursor is circular horizontally but not vertically!

As you might remember from the game, the selection cursor rotates horizontally but not vertically; that means that if I'm in the leftmost and I try to go left again I'll get to the rightmost (examples: from Ryu to Vega, from Ken to M.Bison) and vice versa from rightmost to leftmost.

Instead, if I try to go further up from the upmost or further down from the downmost, I'll just stay where I am located (examples: you can't go lower than lowest row: Ken, Chun Li, Zangief, Dhalsim, Sagat and M.Bison in the above image; you can't go upper than highest row: Ryu, E.Honda, Blanka, Guile, Balrog and Vega in the above image).

### My problem

Again - verbosity is my issue here. Perhaps my lack of patience in refactoring is a key issue. My solution (which works) looked as follows:

~~~ruby
def streetFighterSelection(fighters, position, moves)
  
  hovered_chars = []
  position = position
  
  moves.each do |move|
    if move == "up"
      position[0] = 0
    elsif move == "down"
      position[0] = 1
    elsif move == "left"
      position[1] -= 1
      if position[1] < 0
        position[1] = 5
      end
    else
      position[1] += 1
      position[1] = 0 if position[1] > 5
    end
  hovered_chars.append(fighters[position[0]][position[1]])
  end
hovered_chars
end
~~~

### The solution

The solution, posted by user jaredk72, is more or less the same, but much more succint. It goes a lil like this:

~~~ruby
def streetFighterSelection(fighters, position, moves)
  x = position[0]; y = position[1]
    
  moves.map { |move| 
    case move 
      when "right" then fighters[x][y == 5 ? y = 0 : y += 1]        
      when "left" then fighters[x][y == 0 ? y = 5 : y -= 1]        
      when "down" then fighters[x == 1 ? 1 : x += 1][y]         
      when "up" then fighters[x == 0 ? 0 : x -= 1][y]      
    end
  }
end
~~~

I am not as familiar with <code>case</code> as I should be, and this is a good example of when to use it I think, so remember that shit. Good n proper. 

OUT!
