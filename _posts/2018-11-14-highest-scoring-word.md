---
layout: post
titie: Highest Scoring Word
description: A codewars example
categories: [Ruby, Codewars]
image: https://phillipwright.files.wordpress.com/2018/05/scrabble-word.jpg?w=540&h=360
---

![Word Scores](https://phillipwright.files.wordpress.com/2018/05/scrabble-word.jpg?w=540&h=360)

So this is another codewars example. The problem is, given a string of words, find the highest scoring word of that string, using the scoring method: 

~~~
'a' => 1, 'b' => 2, 'c' => 3      # etc. up to 'z' => 26
~~~

### My solution

First thing to do is create a hash for the scoring system. This isn't perhaps the best way to approach it, but here's how I did that...

~~~ruby
SCORES = Hash[('a'..'z').zip(1..26)]
~~~

Next thing we need is a method to look up that score for a word
~~~ruby
def get_score(word)
  word.chars.sum {  |x| SCORES[x] }
end
~~~

Finally, a method to get the highgest score, using this new method I didn't know about <code>max_by</code> - which returns the maximum value for a given block.

~~~ruby
def highest_word(string)
  string.scan(/\w+/).max_by { |word| get_score(word) }
end
~~~

That's it. Pretty easy. took some refactoring. GOTS IT dOnE.

#### Final code

~~~ruby

SCORES = Hash[('a'..'z').zip(1..26)]

def highest_word(string)
  string.scan(/\w+/).max_by { |word| get_score(word) }
end

def get_score(word)
  word.chars.sum {  |x| SCORES[x] }
end

~~~