---
layout: page
title: Categories
---

<div class='list-group'>
  {% assign cats_list = site.categories %}

  {% if cats_list.first[0] == null %}
    {% for cat in cats_list %}
      <a href="/categories#{{ cat | slugify }}" class='list-group-item'>
        {{ category }} <span class='badge'>{{ site.categories[cat].size }}</span>
      </a>
    {% endfor %}
  {% else %}
    {% for cat in cats_list %}
      <a href="/categories#{{ cat[0] | slugify }}" class='list-group-item'>
        {{ cat[0] }} <span class='badge'>{{ cat[1].size }}</span>
      </a>
    {% endfor %}
  {% endif %}

  {% assign cats_list = nil %}
</div>

<hr>

{% for cat in site.categories %}
<div class="archive-group">
  <h2 class='tag-header' id="{{ cat[0] | slugify }}">{{ cat[0] }}</h2>
  <ul>
    {% assign pages_list = cat[1] %}

    {% for node in pages_list %}
      {% if node.title != null %}
        {% if group == null or group == node.group %}
          {% if page.url == node.url %}
          <li class="active"><a href="{{node.url}}" class="active">{{node.title}}</a></li>
          {% else %}
          <li><a href="{{node.url}}">{{node.title}}</a></li>
          {% endif %}
        {% endif %}
      {% endif %}
    {% endfor %}

    {% assign pages_list = nil %}
    {% assign group = nil %}
  </ul>
</div>
{% endfor %}

