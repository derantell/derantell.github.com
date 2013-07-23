---
layout: post
title: "Why I switched from a Swedish to a US keyboard"
date: 2013-07-23 23:30
comments: true
categories: Productivity
---

Over the years I have noticed that the more experienced I get, the lazier I get when it comes to interacting with a computer. Reaching for the mouse becomes more and more awkward. The more you can do with your hands on the keyboard the better, right?

<!-- more -->

Most the time I spend in front of a keyboard---about 80%---I either code or write English text. I only use Swedish in mail conversations and some client focused documentation. 

That is why I have become more and more frustrated by the layout of the Swedish keyboard. The main pain points are

* `[]`, `{}`, `$`, `|` and `\` are _third level_ (i.e. accessed via `AltGr` or `Ctrl`+`Alt`)
* `^`, `~` and <code>`</code> are [dead keys][1]
* `<>` are on the same key (minor inconvenience perhaps, but my brain has never learned which one is shifted.)
* Most keyboard shortcut schemes of tools and well designed web applications are made with the US keyboard layout in mind.

{% img center /images/KB_Sweden.png 'Swedish keyboard layout' 'Swedish keyboard layout' %}

The reason the Swedish keyboard looks the way it does is because of the three extra vowels Å, Ä and Ö that had to be first level characters on the keyboard. 

After having said to myself for years: "Man, I wish I had a US keyboard", the tipping point finally came when I decided to learn vim commands in [Sublime Text's Vintage mode][2]. Some useful commands just did not work or were very awkward to type. 

Rewiring the brain
------------------
So I ordered the US version of the keyboard I use, the [Microsoft Natural Ergonomic Keyboard 4000][3].

Since I have been [touch typing][4] for the last ten years and are quickly approaching 40, I was worried that it was too late for me to learn a new keyboard layout. However, it was surprisingly easy! The first few weeks there were a lot of mistyping, but after about a month the new layout had settled. 

The hardest part was to relearn the new positions of Å, Ä and Ö when writing Swedish. 

Layouts
-------
To be able to type European letters on a US keyboard, the [US International keyboard][5] should be set as the input keyboard layout. Here are instructions for how to change keyboard layouts on [Windows 7][6], [Windows 8][7], and [Mac][8]. In this layout Å, Ä and Ö are on the third level of `W`, `Q` and `P`, respectively.

{% img center /images/KB_US-International.png 'US International keyboard layout' 'US International keyboard layout' %}

An alternative keyboard layout is the [EurKEY layout][9] by Steffen Brüntjen, which is based on the US layout, but adds a lot of accented characters used in European languages. It also adds Greek letters and mathematical symbols which are available after pressing a dead key. E.g. the `Alt Gr`+`m` dead key toggles the Greek alphabet, hence `Alt Gr`+`m` followed by `p` produces π. 

Conclusion
----------
I have now been using EurKEY on a US keyboard for six months. On the positive side

* coding feels much more natural than before
* keyboard shortcuts work as expected in all tools and apps

However, there are some issues

* my current work laptop has a Swedish keyboard, I usually switch back to the Swedish layout when undocking it
* remoting into servers that does not have a US layout activated causes me trouble sometimes
* pair programming when you don't have two keyboards and are pairing with a programmer that uses a Swedish keyboard 

All in all, I will stick to the US keyboard as long as I primarily use it to write code and English text. And I encourage other programmers/power users to try the switch if they are in a similar situation as myself.

[1]: http://en.wikipedia.org/wiki/Dead_key
[2]: http://www.sublimetext.com/docs/2/vintage.html
[3]: http://www.microsoft.com/hardware/en-us/p/natural-ergonomic-keyboard-4000
[4]: https://en.wikipedia.org/wiki/Touch_typing
[5]: http://commons.wikimedia.org/wiki/File:KB_US-International.svg
[6]: http://support.microsoft.com/kb/258824
[7]: http://www.howtogeek.com/121169/how-to-change-your-keyboard-layout-in-windows-8/
[8]: http://www.wikihow.com/Change-the-Keyboard-Language-of-a-Mac
[9]: http://eurkey.steffen.bruentjen.eu/start.html