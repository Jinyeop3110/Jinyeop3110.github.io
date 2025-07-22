---
layout: default
permalink: /cv/
title: cv
nav: true
nav_order: 5
cv_pdf: CV-2025Jul21.pdf
description: This is my CV as of July 21, 2025.
---

<div class="post">
  <header class="post-header">
    <h1 class="post-title">{{ page.title }}</h1>
    {% if page.description %}
      <p class="post-description">{{ page.description }}</p>
    {% endif %}
  </header>

  <article>
    <div style="width: 100%; height: 800px;">
      <embed src="{{ page.cv_pdf | prepend: 'assets/pdf/' | relative_url }}" 
             type="application/pdf" 
             width="100%" 
             height="100%">
    </div>
    
    <div class="text-center mt-3">
      <a href="{{ page.cv_pdf | prepend: 'assets/pdf/' | relative_url }}" 
         target="_blank" 
         rel="noopener noreferrer" 
         class="btn btn-primary">
        <i class="fa-solid fa-download"></i> Download PDF
      </a>
    </div>
  </article>
</div>
