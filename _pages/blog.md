---
title: 'Blog'
description: "Discover Ilya Suchkov's articles and notes or search for particular one."
og-type: website
permalink: /blog
nav: custom
custom-nav: 
    - '<a style="cursor: pointer;" onclick="toggleSearchBar()" title="Search" >Search</a>&nbsp;|&nbsp;'
    - '<a href="/blog/topics" title="Topics of articles">Topics</a>&nbsp;|&nbsp;'
    - '<a href="/notes" title="Last 15 notes">Notes</a>&nbsp;|&nbsp;'
    - '<a href="/404" title="Random">Random</a>'
---


<div id="search-bar" style="display: none;">
{%- include search.html -%}
</div>

{% for post in site.categories.articles %}
{%- unless post.categories contains "rss-club" or 
post.categories contains "now"-%}
{% include blog-listing.html %}
{% endunless %}
{% endfor %}


<script>

let searchBarStatus = sessionStorage.getItem("searchBarStatus");

if (!searchBarStatus) {
    sessionStorage.setItem("searchBarStatus", "False");
    }
    else if (searchBarStatus === "True") {
    document.getElementById("search-bar").setAttribute("style", "display: block");
    }

function toggleSearchBar() {
    
    let searchBarStatus = sessionStorage.getItem("searchBarStatus");

    if (searchBarStatus === "False") {
        document.getElementById("search-bar").setAttribute("style", "display: block");
        sessionStorage.setItem("searchBarStatus", "True");
    } else if (searchBarStatus === "True") {
        document.getElementById("search-bar").setAttribute("style", "display: none");
        sessionStorage.setItem("searchBarStatus", "False");
    }    
}

</script>