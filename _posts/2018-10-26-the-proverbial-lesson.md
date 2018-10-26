---
layout: post
title: The Proverbial Lesson
description: Exercism Proverb problem, and the lessons learned
categories: [Ruby, Exercism]
image: https://i.redditmedia.com/rnjtwPzextCF-zt6sz-x-RA8JYpaWdmgffW8GJ_0b8U.jpg?w=960&s=e60cade597206687ab75789b9e7ea1c6
---

![A proverb](https://i.redditmedia.com/rnjtwPzextCF-zt6sz-x-RA8JYpaWdmgffW8GJ_0b8U.jpg?w=960&s=e60cade597206687ab75789b9e7ea1c6)

### The problem

From Exercism.io

For want of a horseshoe nail, a kingdom was lost, or so the saying goes.

Given a list of inputs, generate the relevant proverb. For example, given the list ["nail", "shoe", "horse", "rider", "message", "battle", "kingdom"], you will output the full text of this proverbial rhyme:

> * For want of a nail the shoe was lost.
> * For want of a shoe the horse was lost.
> * For want of a horse the rider was lost.
> * For want of a rider the message was lost.
> * For want of a message the battle was lost.
> * For want of a battle the kingdom was lost.
> * And all for the want of a nail.

Note that the list of inputs may vary; your solution should be able to handle lists of arbitrary length and content. No line of the output text should be a static, unchanging string; all should vary according to the input given.

### My problem

My problem here was pretty straightforward, I just didn't know the appropriate syntax for taking multiple arguments. But I learned it. It goes something like this:

~~~ruby
def initialize (*words)
  @words = words
end
~~~

That's pretty simple. 

I also learned a neat trick in iterating through a list, 2 at a time. I think that's what this is for. 

~~~ruby
@words.each_cons(2) do |word1, word2|
  puts "#{word1} and then #{word2}"
end
~~~

Also useful. 

### The solution

Final workthrough with comments:

~~~ruby
class Proverb

  #initialize class, with multiple inputs, and a qualifier
  #which is default set to nil (doesn't exist)
  def initialize(*words, qualifier: nil)
    @words = words
    @qualifier = qualifier
  end

  def to_s
    str = ""
    #iterate through the words list, pulling out 2 at a time
    #until there are none left
    @words.each_cons(2) do |i1, i2|
      #build string
      str += "For want of a #{i1} the #{i2} was lost.\n"
    end
    #build qualifier for end of string
    first_item = [@qualifier, @words.first].compact.join(" ")
    #serve up the proverb
    str += "And all for the want of a #{first_item}."
  end
end
~~~

I got a lot of that from you know who (gchan).

Thanks berdy. 

OUT.
