---
layout: page
title: Tags
---

<ul class="tags">
  {% assign tags_list = site.tags %}

  {% if tags_list.first[0] == null %}
    {% for tag in tags_list %}
    <li>
      <a href="/tags#{{ tag }}">
        {{ tag }} <span class='badge'>{{ site.tags[tag].size }}</span>
      </a>
    </li>
    {% endfor %}
  {% else %}
    {% for tag in tags_list %}
    <li>
      <a href="/tags#{{ tag[0] }}" class="tag">
        {{ tag[0] }} <span class='badge'>{{ tag[1].size }}</span>
      </a>
    </li>
    {% endfor %}
  {% endif %}

  {% assign tags_list = nil %}
</ul>


{% for tag in site.tags %}
  <h2 class='tag-header' id="{{ tag[0] }}">{{ tag[0] }}</h2>
  <ul class="tags">
    {% assign pages_list = tag[1] %}
    {% for node in pages_list %}
      {% if node.title != null %}
        {% if group == null or group == node.group %}
<li><a href="{{node.url}}">{{node.title}}</a></li>
        {% endif %}
      {% endif %}
    {% endfor %}

    {% assign pages_list = nil %}
    {% assign group = nil %}
  </ul>
{% endfor %}
