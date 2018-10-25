---
layout: post
title: Bracket push
description: Make sure you open and close your brackets correctly
categories: [Exercism, Ruby]
image: http://static1.squarespace.com/static/52350939e4b0ca7875752c5f/533836a1e4b0954150ffdcf7/553c4653e4b0b45c0770d8e5/1519269331931/?format=1000w
---

![a bracket](http://static1.squarespace.com/static/52350939e4b0ca7875752c5f/533836a1e4b0954150ffdcf7/553c4653e4b0b45c0770d8e5/1519269331931/?format=1000w)

### The problem
Given a string containing brackets [], braces {}, parentheses (), or any combination thereof, verify that any and all pairs are matched and nested correctly.

### My problem
I was again, thinking about this all wrong. This problem is one of the 'unlockable side exercises', that always seem harder than the original hurdle problem. My mind went straight away to REGEX when I read about matching. That's not quite the right way to have thought about. Again, @gchan, fucking saving my learning abilities - writing such nice code. 

### The solution

Here's the way old mate put it, with some of my comments added in to help me:
~~~ruby
class Brackets
  #create hash of bracket pairs
  BRACKETS = {
    '(' => ')',
    '[' => ']',
    '{' => '}'
  }

  def self.paired?(string)
    #create tempory array to match pairs against
    temp = []

    #iterate over every character of string
    string.chars.each do |char|
      #do the keys of the BRACKETS has contain the character
      if BRACKETS.keys.include?(char)
        #if they do push them to the temporary array
        temp.push(char)
      # else, do the BRACKETVALUES include this character  
      elsif BRACKETS.values.include?(char)
        # pop the last item of temp array into the hash key, does it
        # equal the character? if it does, it should empty the array
        # again, otherwise, return false, the brackets are out of order
        # or some are missing
        return false unless BRACKETS[temp.pop] == char
      end
    end
    # returns true if the temp array is empty, i.e. all the 
    # inputed characters match
    temp.empty?
  end
end
~~~

Let's just walk through this a bit in irb. 

~~~
irb (main)

BRACKETS = { '(' => ')', '[' => ']', '{' => '}' }   #create your variables
=> {"("=>")", "["=>"]", "{"=>"}"}
temp = []
=> []
string = "[[]]"
=>"[[]]"

if BRACKETS.keys.include?('[')
temp.push('[')
end
=> ["["]
~~~

So that part is just checking if the hash has the open bracket, and pushes it to the temporary array. The same will happen for the next iteration of "string", if we pretend we are iterating through the characters of the string ("[[]]"). This means the array is now <code>["[", "["]</code>. That kinda looks confusing, because of the characters, but you'll get there, and I can't be bothered re-writing it. 

So, then we get to the next part of the loop, the <code>elsif</code> statement. 

~~~
BRACKETS.values.include?(']')
=> true
~~~

Now pay attentions, with the original code in mind (focus on the elsif statement still, which just evaluated true.

~~~
temp
=> ["[", "["]

BRACKETS[temp.pop] == ']'
=> true

# and if we check temp now
temp
=> ["["]
~~~

Repeating this again for the final iteration of the loop, "temp" will yield <code>[]</code>. The array is empty. Which means all the brackets matched. 

This fact is assured with the 
~~~
temp.empty?
=> true
~~~

Thus, the function returns true, when the temp array has become empty. And its empty because all the characters matched. If the most previous iteration of characters "popped" from the array had been a closing the bracket, the 'key' wouldn't be found in the "BRACKETS" hash, and the loop would have returned false. 

FUCKING. CLEVER.

How are you feeling?


