---
layout: post
title: "Mac OS X Mavericks and Android File Transfer"
description: ""
category: random
tags: [android, mac, os x]
---
If you have recently upgraded to Mac OS X Mavericks and you discover that you can no longer detect your Android phone with Android File Transfer, this should fix it for you.

* Open up Settings.
* Choose Storage.
* On the top right is an option dropdown, hit that and hit "USB computer connection."
* If MTP is unchecked (as mine was), AFT won't detect your device. Enable it.
* Reconnect and everything should work properly.

I haven't messed with this setting in the past so I don't know why it was unchecked, but apparently something in the Mavericks upgrade affected the ability of AFT to detect the phone without MTP enabled.

Hopefully this will help out other frustrated hybrid Mac OS X and Android users.
