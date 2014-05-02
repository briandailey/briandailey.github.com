---
layout: post
title: Know Thy Code
category: Random
---
When I first started programming in Java for a medical company (I was 17 at the time) I had very little training and unfortunately I learned a lot of bad habits that have taken a lot of study to identify and squelch.

Even what I learned in school, as others have often experienced, was far less useful than on-the-job experience and learning from other talented developers.

I once worked with another talented developer that didn't use many of the tools that I've come to rely on: debugging aids, unit testing, high error/warning levels, etc. Yet this developer seemed to be able to catch nearly all bugs without any of these tools. At first I thought it was simply inhuman. How could someone catch everything on the first pass without any debugging tools or even compiler notices turned on? It wasn't until I asked to sit down and have this developer walk me through his entire debugging process that light began to dawn upon why he seemed to be so thorough in reviewing his own code.

The primary difference was that I programmed with a web browser open while my colleague did not. My usual approach was to code a little bit, view the changes in the browser, make sure the incremental changes that I made worked (if unit testing is available, I'd run that, too) and then move on to the next incremental change. My colleague, on the other hand, would work on much larger incremental changes; he also spent much more time in the code itself checking for problems. By the time he was ready to fire up the browser (or in my case, a unit test) he was already confident that the code would work exactly as he expected it to.

I have recently been reading the book "[Code Complete](http://www.amazon.com/Code-Complete-Practical-Handbook-Construction/dp/0735619670/)" by Steve McConnell on the advice of the programmer/blogger [Jeff Atwood](http://www.codinghorror.com/blog/). I have found it to be very useful and I have learned a lot from it, even though I'm only halfway through the book. One snippet from the book is quite relevant to this phenomenon that I witnessed.

> _After_ reviewing the routine, compile it. It might seem inefficient to wait this long to compile since the code was completed several pages ago. Admittedly, you might have saved some work by compiling the routine earlier and letting the computer check for undeclared variagles, [etc]. The main reason [for compiling later] is that when you compile new code, an internal stopwatch starts ticking. After the first compile, you step up the pressure. 'I'll get it right with just one more compile.' The 'Just One More Compile' syndrome leads to hasty, error-prone changes that take more time in the long run. Avoid the rush to completion by not compiling until you've convinced yourself that the routine is right." (Emphasis mine.)

If you replace "compile" with "refresh the browser" you can apply the same idea to web application development. I realized after reading this that my colleague didn't have superhuman powers: he had simply taught himself to thoroughly _know his own code_ before loading it up and viewing it in a browser. I realized that I was guilty of "Just one more refresh" syndrome. I'm not discounting the power of unit testing or turning on all compiler warnings on a development machine. I still believe that's vital to development in any environment. But change a line, refresh, fix the error that you saw, change another line... that's a horrible way to develop software.

There are still many times in web development when firing up a web browser is still absolutely necessary, but I do believe that far too many web developers do not put enough emphasis on knowing and understanding the code before attempting to run it.

Here are some ideas that have helped me with knowing my code and catching problems before they ever appear in the browser.

- Close the browser. If possible, don't open it until you have completely reviewed the code.
- Review each routine (function) or class call and make sure it's doing what you think it's doing.
- When you near finishing the feature, review the code and see if it can be refactored to make it more clear what is the code is doing (I'm a big believer in maximum code-clarity).
- What does the code modify (for example, in the database)? How does it modify it?

Of course there are many, many other things you can review (read Section 9.3 in "Code Complete" for some ideas) but the idea is to review, review, review, _before_ opening the browser. After adopting this up-front investment in the code I have found that the number of errors in my code are much fewer and far between than they were.

__Edit:__ Hey, thanks for all the constructive criticism! One thing I should probably clarify. I never said that this idea applies to web _design_. Web design is (at least as I see it) defined differently from web (or software) development. Web design, as in HTML layout, CSS, images, what-have-you, _does_ require that you view it in a browser early and often. It's the nature of the game. What I'm referring to is completely on the backend (where, as some of you pointing out my "horrible font choices" probably already know, I spend 99.9% of my time). By the way, I will definitely take the recommendations on the serif font seriously.

