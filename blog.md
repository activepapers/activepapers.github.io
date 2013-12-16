---
layout: default
title: ActivePapers blog
---
<h1>{{ page.title }}</h1>
{% for post in site.posts %}
<div class="post">
<div class="date">
{{ post.date | date_to_string}}
</div>
<a href="{{ post.url }}">{{ post.title }}</a> by {{ post.author }}
</div>
{% endfor %}
