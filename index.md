---
layout: page
title: Software, hardbody
tagline: my programming and self development blog
---
{% include JB/setup %}

## Recent Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## My projects

* [Moving Bro](http://www.movingbro.com)
* [Swelfie](http://swelfie.us)

