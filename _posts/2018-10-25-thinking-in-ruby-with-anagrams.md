---
layout: post
title: Thinking in Ruby (with Anagrams!)
description: Working around the anagram problem
categories: [Exercism, Ruby]
image: https://wordsmith.org/anagram/images/anagram-listen-silent.png
---

![An anagram](https://wordsmith.org/anagram/images/anagram-listen-silent.png)

## The problem

Given a word and a list of potential anagrams of that word, return a list of correct anagrams

## My problem

I was thinking about it wrong. I wanted to iterate over each letter of each word of each word in the list and of each letter of the given word. Its too much iteration, and likely involves far too many nested loops. Instead, consider our trusty anonymous github user, who may surely shut me down, @gchan.

## The solution

Instead of iterating over each letter of each word to check for anagrams, think more abstractly, and more like a programmer. Just turn the words into arrays of characters, and then sort the arrays. In this way, if 2 words are anagrams, when viewed as sorted arrays, they will be equal. 

Example

~~~
irb(main)

word_one = "Listen"
=> "Listen"
word_two = "silent"
=> "silent"
word_one.downcase.chars.sort
=> ["e", "i", "l", "n", "s", "t"]
word_two.downcase.chars.sort
=> ["e", "i", "l", "n", "s", "t"]
word_one == word_two
=> false
word_one.downcase.chars.sort == word_two.downcase.chars.sort
=> true

~~~

So, to solve the puzzle for [Exercism](https://exercism.io), @gchan, and now me, used this:

~~~ruby
class Anagram
  def initialize(word)
    @word = word
  end

  def match(word_list)
    #create array and sort it, of the characters that make up the given word
    sorted_chars = @word.downcase.chars.sort

    #select conditions that are "true" from iterating over the word_list
    word_list.select do |candidate|
      #make sure that the words are anagrams and not simply equal
      candidate.downcase != @word.downcase &&
      candidate.downcase.chars.sort == sorted_chars
    end
  end
end
~~~

Freaking learning all the time. Feels good in the brain balls. 

End.

