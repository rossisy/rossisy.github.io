---
title: Categories
layout: default
---

<div>
  {% for cat in site.categories %}
  <a href="#{{ cat[0] }}" title="{{ cat[0] }}" rel="{{ cat[1].size }}">{{ cat[0] }}({{ cat[1].size }})</a>
  {% endfor %}
</div>

<ul class="listing">
  {% for cat in site.categories %}
    <li class="listing-seperator" id="{{ cat[0] }}">
      <h2>{{ cat[0] }}</h2>
    </li>
  {% for post in cat[1] %}
    <li class="listing-item">
      <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
      <time datetime="{{ post.date | date: site.date_format }}">{{ post.date | date: site.date_format }}</time>
    </li>
  {% endfor %}
    <br>
  {% endfor %}
</ul>
