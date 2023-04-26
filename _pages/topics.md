---
title: "Topics"
description: "Ech of my articles has one or more topic."
permalink: /blog/topics
---

{% include search.html %}

<h2 id="categories">Categories</h2>
<div class="tag-list">
<a href="/blog">Articles ({{ site.categories.articles | size }})</a>
<a href="/blog/now">Now ({{ site.categories.now | size }})</a>
<a href="/notes">Recent notes</a>
</div>

<h2 id="topics">Topics</h2>

{% assign sortedTags = site.tags | sort %}

<div class="tag-list">
{% for tag in sortedTags %}
	<a href="#{{tag[0]}}">{{ tag[0] }}&nbsp;({{ tag[1] | size }})</a>
{% endfor %}
</div>

{% for tag in sortedTags %}

<section class="posts-by-tag">

<h2 id="{{ tag[0] }}">{{ tag[0] }}</h2>

{% for post in tag[1] %}
	{% include blog-listing.html %}
{% endfor %}

<p><a href="#" class="internal-link">All Topics &#8593;</a></p>

{% endfor %}