---
layout: default
title : Archives
description: An archive of this blog's post.
keywords: blog archive, archive
---

<div class="posts notes">
<div class="hrhead"></div>

  <h3>Archives</h3>
  {% for post in site.posts %}
  <div class="post-list">
      <div class="post-list-date"><small><li>{{ post.date | date: "%b %d, %Y" }} » </li></small></div>
	    <div class="text-truncate"><a href="{{ post.url }}">{{ post.title }}</a></div>
    </div>
  {% endfor %}
</div>