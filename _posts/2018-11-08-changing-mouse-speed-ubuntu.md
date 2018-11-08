---
layout: post
title: Configuring mouse speed in Ubuntu
description: How to alter that mouse speed
categories: [Ubuntu]
image: https://cdn.renodepot.com/images/13095109_L.jpg
---

![A mouse trap](https://cdn.renodepot.com/images/13095109_L.jpg)

I recently installed [touchpad indicator](http://ubuntuhandbook.org/index.php/2018/04/install-touchpad-indicator-ubuntu-18-04-lts/) for Ubuntu, so I would stop moving teh mouse around when typing. It seems to be working pretty good so far. However, upon doing so, alterations I had made to my touchpad to slow the pointer speed down seems to have reverted (It was initially pretty fast). 

So to fix it, here's what can be done:

Find the device:
```
xinput --list --short
```

That shows up this:
```
⎡ Virtual core pointer                      id=2  [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4  [slave  pointer  (2)]
⎜   ↳ SYNA7DB5:01 06CB:7DB7 Touchpad            id=12 [slave  pointer  (2)]
⎣ Virtual core keyboard                     id=3  [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5  [slave  keyboard (3)]
    ↳ Power Button 
```

My device is <code>"SYNA7DB5:01 06CB:7DB7 Touchpad"</code>. To get the device properties:
```
xinput --list-props "SYNA7DB5:01 06CB:7DB7 Touchpad"
```

The speed properties is this one:
```
Device Accel Constant Deceleration (275): 1.000000
```

So to slow it down, you put a bigger number I think. Type:
```
xinput --set-prop "SYNA7DB5:01 06CB:7DB7 Touchpad" "Device Accel Constant Deceleration" 1.5
```

That should fix it. Nice one. 

[Answer found here](https://askubuntu.com/questions/205676/how-to-change-mouse-speed-sensitivity)