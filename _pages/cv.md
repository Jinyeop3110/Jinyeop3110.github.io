---
layout: default
permalink: /cv/
title: cv
nav: true
nav_order: 5
description: My resumes tailored for different research directions.
---

<div class="post">
  <header class="post-header">
    <h1 class="post-title">{{ page.title }}</h1>
    {% if page.description %}
      <p class="post-description">{{ page.description }}</p>
    {% endif %}
  </header>

  <article>
    <!-- Tab Navigation -->
    <ul class="nav nav-tabs" id="cvTabs" role="tablist">
      <li class="nav-item" role="presentation">
        <button class="nav-link active" id="coreai-tab" data-bs-toggle="tab" data-bs-target="#coreai" type="button" role="tab" aria-controls="coreai" aria-selected="true">
          <i class="fa-solid fa-brain"></i> Core AI Research
        </button>
      </li>
      <li class="nav-item" role="presentation">
        <button class="nav-link" id="ai4science-tab" data-bs-toggle="tab" data-bs-target="#ai4science" type="button" role="tab" aria-controls="ai4science" aria-selected="false">
          <i class="fa-solid fa-flask"></i> AI for Science
        </button>
      </li>
    </ul>

    <!-- Tab Content -->
    <div class="tab-content" id="cvTabsContent">
      <!-- Core AI Tab -->
      <div class="tab-pane fade show active" id="coreai" role="tabpanel" aria-labelledby="coreai-tab">
        <p class="mt-3 text-muted"><em>Focus: Multi-LLM Agent RL, LLM Agent Foundations, Tool-augmented Reasoning</em></p>
        <div style="width: 100%; height: 800px;">
          <embed src="{{ 'assets/pdf/Resume_coreAI.pdf' | relative_url }}"
                 type="application/pdf"
                 width="100%"
                 height="100%">
        </div>
        <div class="text-center mt-3">
          <a href="{{ 'assets/pdf/Resume_coreAI.pdf' | relative_url }}"
             target="_blank"
             rel="noopener noreferrer"
             class="btn btn-primary">
            <i class="fa-solid fa-download"></i> Download Core AI Resume
          </a>
        </div>
      </div>

      <!-- AI for Science Tab -->
      <div class="tab-pane fade" id="ai4science" role="tabpanel" aria-labelledby="ai4science-tab">
        <p class="mt-3 text-muted"><em>Focus: LLM-agent Systems for Science, Biological Foundation Models, Scientific Benchmarks</em></p>
        <div style="width: 100%; height: 800px;">
          <embed src="{{ 'assets/pdf/Resume_AI4Science.pdf' | relative_url }}"
                 type="application/pdf"
                 width="100%"
                 height="100%">
        </div>
        <div class="text-center mt-3">
          <a href="{{ 'assets/pdf/Resume_AI4Science.pdf' | relative_url }}"
             target="_blank"
             rel="noopener noreferrer"
             class="btn btn-primary">
            <i class="fa-solid fa-download"></i> Download AI for Science Resume
          </a>
        </div>
      </div>
    </div>
  </article>
</div>
