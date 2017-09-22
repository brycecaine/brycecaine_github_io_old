---
layout: single
title: Archive
permalink: /archive/
---

<div>
    {% for post in site.posts %}
        {% assign currentdate = post.date | date: "%Y" %}
        {% if currentdate != date %}
            <h2 id="y{{currentdate}}">{{ currentdate }}</h2>
            {% assign date = currentdate %} 
        {% endif %}
        <p><a href="{{ post.url }}">{{ post.title }}</a></p>
    {% endfor %}
</div>
