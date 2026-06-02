---
layout: minimal
title: Posts
description: >
  Blog posts and project pages.
hide_description: true
---

# Posts

## Projects

<ul class="project-list">
  <li>
    <a href="/protein-llm.html">Protein LLM Series</a>
    <span>Bridging ESM-3 protein embeddings with LLMs: architecture, scaling, and reinforcement learning.</span>
  </li>
  <li>
    <a href="/autoresearch-denovo.html">Autoresearch De Novo</a>
    <span>De novo protein binder design with Proteina-Complexa: beam search, config diversity, and sequence analysis.</span>
  </li>
</ul>

## Blog posts

{% assign posts_by_year = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
{% for year in posts_by_year %}
### {{ year.name }}

<ul class="post-list">
{% for post in year.items %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <span>{{ post.date | date: "%d %b" }}</span>
  </li>
{% endfor %}
</ul>
{% endfor %}
