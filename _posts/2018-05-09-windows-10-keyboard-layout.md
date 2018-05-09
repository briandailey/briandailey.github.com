---
layout: post
title: "Help! My Keyboard Layout Keeps Switching in Windows 10"
description: ""
category: windows
tags: [windows, colemak]
---
I use the Colemak layout on Windows 10 version 1803 (April 2018). I'm aware that I can switch back to a Qwerty
layout by hitting Windows + Space, but occasionally my layout would switch anyway
and I knew I wasn't hitting this shortcut. It turns out that there's another keyboard
shortcut that does the same thing - either _Alt+Left Shift_ or _Ctrl+Left Shift_. In
my case, it was the latter. Here's how to fix this.

First, open settings. Choose _Time & Language_ and then _Region and Language_.
Next, click _Advanced Keyboard Settings_ below "Related Settings." Then click
"Languag bar options" below "Switching input methods." This opens a dialog box,
choose the "Advanced Key Settings" tab. You should see something like
this:

![keyboard layout shortcuts](/img/2018-05-09-windows-layout.png)

Click "Change Key Sequence" and then choose "Not assigned" for both "Switch
Keyboard Layout" and "Switch Input Language."

Hit "Ok."

Now you should be less prone to accidentally change your layout in the middle
of trying to get things done!
