---
layout: post
title: "Remapping Caps Lock in Multiple Operating Systems"
description: ""
category: Programming
tags: [keyboards, capslock]
---

A colleague of mine recently sold me an HHKB (["Happy Hacking Keyboard"](https://hhkeyboard.us/)).
It's a little different than most other keyboards I've used (and I'm a fan of
either 60% of 75% layouts). For example, the Backspace key is below the number
row, and the backslash key is in the number row. I found I was able to adjust to
this and back to the "Normal" positioning fairly quickly after some practice.
For example, if I needed to use my laptop keyboard for a while, readjusting my
fingers only took one or two mistakes. The brain's plasticity never ceases to
surprise me.

However, one other change on this layout was harder for me to adjust to.  In
particular, there is no left "Ctrl" key. Instead, you will find it where you
might normally find a Caps Lock key. This left me SHOUTING UNNECESSARILY when I
was using a more standard keyboard layout. I use the Ctrl key for navigating words,
particularly on the command line, and I kept tripping up on this change.

Since I try not to shout much on the internet, Caps Lock isn't super useful for
me.[^1] It makes sense to remap it to something more useful, like the Control
key, across all my keyboards. However, when I set out to do this I found that
there is a ton of out-dated information floating around (registry hacks,
anyone?). Hence, I hope it might be useful to see this in one place for others.
These tricks worked, at least, in September 2021.

* For **Ubuntu Linux** (20.04 or newer, but also probably older version as well),
  install the Gnome tweaks tool. You can do this by opening a
  terminal and running `sudo apt install gnome-tweaks`. From there, open up
  "Gnome Tweaks" and simply navigate to the keyboard preferences panel. From
  there you can easily map Caps Lock to Ctrl.
* For **Mac OS**, open up System Preferences and then "Keyboard." Click the
  "Modifier Keys" button. From here you can remap Caps Lock to Control. Note
  that if you use an external (USB) keyboard you will need to remap this for
  each keyboard.
* **Microsoft Windows**, use the [PowerToys](https://docs.microsoft.com/en-us/windows/powertoys/)
  utility. Once it's installed, open it and click "Keyboard Preferences." From
  there you can remap Caps Lock to Ctrl. This works on Windows 10 or Windows 11.

That covers all of the major operating systems. Happy keyboarding!

[^1]: I tried the [colemak](https://colemak.com/) layout for a year or so and one of the things I liked about it was that it remapped Caps Lock to backspace.  However, I found that my typing error rate never recovered so I eventually went back to Qwerty and continued to ignore the Caps Lock key.


