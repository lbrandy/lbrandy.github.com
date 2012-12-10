---
layout: page
title: lbrandy.com
tagline: programming and the internets
---

{% for post in site.posts limit:3 %}
#  {{ post.title }}

{{ post.content }}

{% endfor %}
