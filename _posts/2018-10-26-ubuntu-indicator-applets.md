---
layout: post
title: Ubuntu indicator apps
description: Be indicators
categories: Ubuntu
image: https://cdn.arstechnica.net/wp-content/uploads/2018/05/ubuntu1804-files-640x360.jpeg
---

![Ubuntu](https://cdn.arstechnica.net/wp-content/uploads/2018/05/ubuntu1804-files-640x360.jpeg)

I needed an indicator app that let me know when I pressed my keylocks (capslock, numlock), and came across a good article from [It's FOSS](https://itsfoss.com/best-indicator-applets-ubuntu/). I found that the linked indicator was good, and was thinking of adding a few more...


### Keylock indicator

![Keylock indicator](https://4bds6hergc-flywheel.netdna-ssl.com/wp-content/uploads/2017/01/key-lock-best-indicator-applets-e1483992179368.jpg)

Let's you know when you've capslocked.

Here's how to get it going:

~~~
sudo add-apt-repository ppa:tsbarnes/indicator-keylock

sudo apt-get update

sudo apt-get install indicator-keylock
~~~

Nice. 

### Caffeine indicator

Stop your screen turning off. Its annoying. Set it easily to on or off. 

~~~
sudo add-apt-repository ppa:caffeine-developers/ppa

sudo apt-get update

sudo apt-get install caffeine
~~~

### Netspeed Unity - Check yo speed

~~~
sudo apt-add-repository ppa:fixnix/netspeed

sudo apt-get update

sudo apt-get install indicator-netspeed-unity
~~~

### Simple weather indicator

Check the weather fool.

~~~
sudo add-apt-repository ppa:kasra-mp/ubuntu-indicator-weather

sudo apt update

sudo apt install indicator-weather
~~~

### System load: Indicate it

See how you're running.

![System indicator](https://4bds6hergc-flywheel.netdna-ssl.com/wp-content/uploads/2017/01/system-load-monitor-best-indicator-applets-e1483990514733.jpg)

~~~
sudo apt-get install indicator-multiload
~~~


#### That's it for now folks

END.

