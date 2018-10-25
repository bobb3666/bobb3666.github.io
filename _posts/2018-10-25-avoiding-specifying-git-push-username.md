---
layout: post
title: The git push problem
description: Avoid specifying username and password when using "git push"
categories: [Bash, Git, Ubuntu]
image: https://cdn-images-1.medium.com/max/1600/1*Z65ZuqFrCa7aqZLD29HBkg.png
---

![git push](https://cdn-images-1.medium.com/max/1600/1*Z65ZuqFrCa7aqZLD29HBkg.png)

I was typing in my username and password everytime I wanted to commit a push to [GitHub](https://github.com/). Its probably good practice, I don't know, but for some projects it likely doesn't matter. So here is a workaround from [Stack Overflow](https://stackoverflow.com/questions/8588768/how-do-i-avoid-the-specification-of-the-username-and-password-at-every-git-push).

### If you haven't already, generate an SSH key

I've already done this, but the bash (ubuntu) is

~~~
cd ~                #Your home directory
ssh-keygen -t rsa   #Press enter for all values
~~~

### Associate the SSH key with remote setup

For me this just involves going to the GitHub repository, clicking settings, and 'add SSH key'. Then paste it in. 
These instructions are often posted in the GitHub repository anyway. 
The magic comes next.

### Set your remote URL to a form that supports SSH<sup>1</sup>

You want your repo to be in the form

~~~
git+ssh://git@github.com/username/repository.git
~~~

To check what its currently looking like:
~~~
git remote show origin
~~~

**And to change it**
~~~
git remote set-url origin git+ssh://git@github.com/username/repository.git
~~~

Handy stuff. Thanks to @First Zero

