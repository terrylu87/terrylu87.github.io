---
layout: page
title: Hello Hackers
tagline: let's become top coders
---
{% include JB/setup %}

<div>Latest Posts:</div>
<ul class="posts">
{% for post in site.posts limit: 5 %}
  <div class="post_info">
    <li>
	    <a href="{{ post.url }}">{{ post.title }}</a>
	    <span>({{ post.date | date:"%Y-%m-%d" }})</span>
    </li>
    </br> <em>{{ post.excerpt }} </em>
    </div>
  {% endfor %}
</ul>

<div>All Posts:</div>
<ul>
  {% for post in site.posts %}
  <li>
    <a href="{{ post.url }}" title="{{ post.title }}">
      <span class="date">
        <span class="day">{{ post.date | date: '%d' }}</span>
        <span class="month"><abbr>{{ post.date | date: '%b' }}</abbr></span>
        <span class="year">{{ post.date | date: '%Y' }}</span>
      </span>
      <span class="title">{{ post.title }}</span>
    </a>
  </li>
  {% endfor %}
</ul>
