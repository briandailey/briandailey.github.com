---
layout: page
title: Hi.
tagline: 
---
{% include JB/setup %}

<div class="pull-right"><img alt="Pete the pug and Brian at the tip of Long Island, Montauk, NY." src="https://si0.twimg.com/profile_images/2504804310/0tp8veb5lge1ze599zso.jpeg" /></div>

My name is Brian. I am a web developer. As of 2013, I am busy in Nashville with [Stratasan](http://stratasan.com), a company I co-founded in 2010. I also occasionally do freelance work under the business name [Realm3](http://realm3.com).

My current language of choice is Python. You can see some of my projects on [GitHub](http://github.com/briandailey). If you would like to find out more about projects I've worked on in the past, see the [Projects](/projects.html) page.

Occasionally, I blog here. My latest ramblings are:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

If you want to get in touch with me, you can reach me at [@byeliad](http://twitter.com/byeliad) on Twitter. You can also find me on Freenode on #pynash, #nashdl, and elsewhere. If you must, you can also connect with me on [LinkedIn](http://www.linkedin.com/in/briandailey).
