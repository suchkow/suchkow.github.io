---
title: Notes
layout: page
nav: custom
custom-nav: 
    - '<a href="/blog" title="blog">Blog</a>' ## &nbsp;|&nbsp;
permalink: /notes
---


<div class="callout" markdown="1">

## What are notes?

This is a place for shorter thoughts, interesting links and shaping ideas before they become full posts.

</div>


{% for post in site.categories.notes limit: 15 %}
<section class="note-entry" markdown="1">
<h1><a href="{{post.url}}" style="text-decoration: none;">{{post.title}}</a></h1>

{{post.content}}

<p class="note-date-line"><time datetime="{{ post.date | date: '%Y-%m-%d' }}">{{ post.date | date: "%B %d, %Y" }}</time></p>
</section>
{% endfor %}


<div class="callout" markdown="1">

## You’ve reached the end, kind of

There is a limit of 15 last notes.
#### Older notes are still accessible via their respective link.

</div>
