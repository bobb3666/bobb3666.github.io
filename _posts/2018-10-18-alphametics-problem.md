---
layout: post
title: The Alphametics Problem
descriptions: Ruby track alphametics exercise solution
categories: [Exercism, Ruby]
image: http://www.mathmavericktutor.com/wp-content/uploads/2014/12/AlphameticsEx.png
---

![An alphametic](http://www.mathmavericktutor.com/wp-content/uploads/2014/12/AlphameticsEx.png)

I have recently begun working through challenges at both [exercism](http://exercism.io/) and [codewars](http://www.codewars.com/) to try and get some coding practice, develop my abilities and and get a better handle on ruby. Exercism allows you to view community answers to problems to better help your learning. One such example that struck me was the Alphametics challenge. I spent a good couple of hours trying to work through it and yet couldn't find a solution. Exercism allows you to post unfinished problems so you can check other user's solutions to better your own. I want to put one example here from user @gchan. I hope this doesn't break the rules.

## The problem:
Basically, you get a string that has words equated to each other like a typical maths equation - "I + BB = ILL". You need to find the numbers that correspond to the letters to solve the challenge. After about 50 lines of code I realised I didn't know what I was doing, so I went to the work of others to learn. 

I think I was breaking up the problem wrong, and didn't have the knowledge of tools available to me to better work through this. So I found @gchan's solution very useful and I want to work through it here. 

## The solution

Firstly, the answer should take the form of <code>Alphametics.solve(puzzle)</code> - where <code>Alphametics</code> is a class, and <code>solve</code> is a method of that class. This part is easy, and part of each challenge. 

~~~ruby
class Alphametics
  def self.solve(puzzle)
    #code goes here
  end
end
~~~

Sweet. So using @gchan's solution, lets see a clean way to work through the problem.

Firstly, ruby handles exponentials with the syntax <code> x**y </code> but the equations posted in the challenge use the <code>^</code> symbol. To fix this problem, you must first "globally substitute" every instance of <code>^</code> with <code>**</code>:

~~~ruby
# The exclaimation makes the function mutate the original variable
puzzle.gsub!('^', '**')
~~~

The next thing to do is create an array of unique letters in the puzzle, seeing that each letter only needs once solution, you really only need to create a copy of each unique letter.

~~~ruby
letters = puzzle.scan(/[[:alpha]]/).uniq
#This just uses a regex expression that finds alphanumerics in a given string
#and creates an array of the unique letters in it
~~~

Now for the meaty part. 

1. The next portion of code needs to create a permutation of all the possible answers to each letter (i.e. the digits 0 - 9) for the amount of unique letters in the equation (in the above example that is "I", "B", "L"). This was the part I really didn't know how to do. 

2. Then you want to create a hash (dictionary of sorts) of all possible combinations where these letters have a different solution (i.e. "I" => 1, "B" = > 2, etc for every combo). 

3. While iterating through each combination, create a string with the substituted "letter-answer" combinations. 

4. If the string evaluates true (i.e. tell ruby to process the string like it was made of integers), return it. 

That part of the code looks like:
~~~ruby
(0..9).to_a.permutation(letters.count).each do |digits|
      map = Hash[*(letters.zip(digits).flatten)]
      substituted = puzzle.gsub(/[A-Z]/, map)
      next if substituted.match(/(\s|\A)0/)
      return map if class_eval(substituted)
    end
~~~

Elegant. I was trying to achieve this same function in around 50 lines of code and getting no where. Boy do I feel silly?!?@#@?

Below is the fully implemented code from @gchan, which I have commented on to help me understan it. I'd say doing things this way is helpful when you have no idea what you're doing. I had to look up each method I didn't know about. Practice my regex. Learn some tricks. Great stuff. Thank's gchan.

~~~ruby
class Alphametics
  def self.solve(puzzle)
    # change math sign ^ to ** for ruby
    puzzle.gsub!('^', '**')
    # get the unique letters used in puzzle
    letters = puzzle.scan(/[[:alpha:]]/).uniq

    #create permutations of digits for amount of unique letters
    (0..9).to_a.permutation(letters.count).each do |digits|
      #create hash of letter digit combinations and flattens into one array
      map = Hash[*(letters.zip(digits).flatten)]

      #substitute the given map permutation into the puzzle
      substituted = puzzle.gsub(/[A-Z]/, map)

      #skips to next iteration of loop if substituted
      #puzzle has whitespace or A? followed by a 0
      next if substituted.match(/(\s|\A)0/)

      # returns the map if the evalution of the string is true
      return map if class_eval(substituted)
    end
  end
end
~~~

Byenow. 