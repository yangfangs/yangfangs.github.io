---
layout: page
title: Wiki
description: 收藏
keywords: 收藏, Wiki
comments: false
menu: 收藏
permalink: /wiki/
---

> 就像一本字典一样,收藏一些非常有用,需要查询的东西

<ul class="listing">
{% for wiki in site.wiki %}
{% if wiki.title != "Wiki Template" %}
<li class="listing-item"><a href="{{ wiki.url }}">{{ wiki.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
