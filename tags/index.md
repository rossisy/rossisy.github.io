---
title: tags
layout: default
---

<div id="tag_cloud">
  {% for tag in site.tags %}
    <a href="#{{ tag[0] }}" title="{{ tag[0] }}" rel="{{ tag[1].size }}">{{ tag[0] }}({{ tag[1].size }})</a>
  {% endfor %}
</div>

<ul class="listing">
  {% for tag in site.tags %}
    <li class="listing-seperator" id="{{ tag[0] }}">
      <h2>{{ tag[0] }}</h2>
    </li>
  {% for post in tag[1] %}
    <li class="listing-item">
      <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
      <time datetime="{{ post.date | date: site.date_format }}">{{ post.date | date: site.date_format }}</time>
    </li>
  {% endfor %}
    <br>
  {% endfor %}
