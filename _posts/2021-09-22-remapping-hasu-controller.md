---
layout: post
title: "Adjusting the HHKB HASU (mod) Controller Layout"
description: ""
category: Programming
tags: [keyboards]
---

I recently acquired an HHKB Professional 2 with the HASU bluetooth controller
mod. I did not find documentation for remapping the keys using tmk or qmk in
one place, but I did cobble the information together and figured I would write
it up here. It's more for my own reference than anything else, but perhaps it
will be useful to someone else!

This is assuming that you're using a Mac. You'll need homebrew installed and
you'll need to use your laptop keyboard (or another spare) to flash the changes
to the HHKB.

Install `dfu-programmer`.

```
brew install dfu-programmer
```

Go to the [TMK keymap editor for the HHKB Pro1/Pro2 Controller Bluetooth](http://www.tmk-kbd.com/tmk_keyboard/editor/unimap/?hhkb_rn42)
and make your changes and download the hex file.

Put your keyboard into flashing mode by either pushing the red button on the
back or pressing the combination `Left Shift` + `Right Shift` + `Fn` + `P`.
After doing this the keyboard should not respond to further key presses, so
continue using another keyboard but do not disconnect it.

Run the following command in Terminal, and you should see similar output.

```
$ dfu-programmer atmega32u4 erase
Checking memory from 0x0 to 0x6FFF...  Not blank at 0x1.
Erasing flash...  Success
Checking memory from 0x0 to 0x6FFF...  Empty.
```

Next, apply the hex file you downloaded earlier from the keymap editor.

```
$ dfu-programmer atmega32u4 flash <path_to_.hex>
Checking memory from 0x0 to 0x6FFF...  Empty.
0%                            100%  Programming 0x7000 bytes...
[>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]  Success
0%                            100%  Reading 0x7000 bytes...
[>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]  Success
```

Lastly, run this:

```
dfu-programmer atmega32u4 reset
```

Your changes should now be ready to use!
