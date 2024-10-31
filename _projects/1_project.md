---
layout: page
title: Concept encoding in in-context learning of LLMs
description: Study about concept encoding phenomena in in-context learning of LLMs and how to interpret ICL sucess and failure modes.
img: assets/img/publication_preview/concept_encoding.png
importance: 1
category: Sceince of AI
related_publications: true
---

Paper (soon to be archived) : <a href="https://drive.google.com/file/d/14e3DBsKpuRdav9lA_Wkfg8FI1mi5iMZn/view?usp=sharing">"Concept to Context : Concept Encoding in In-Context Learning of LLMs"</a>


**TLDR:** We explored the mechanistic understanding of ICL success/failure modes through how well certain concepts are encoded in intermediate reprsentatoions


Why does in-context learning (ICL) succeed or fail depending on the task? We explored the mechanisms behind these success and failure modes and sought to quantify them. To this end, we introduced the concept of **Concept Encoding** phenomena, which posits that representations are effectively distinguished by latent concepts. Our findings demonstrate that concept encoding occurs in the LLAMA3 8B model, as evidenced by realistic latent concepts such as verbs and nouns in part-of-speech tagging, as well as logical operators like AND and OR in bitwise operations.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/reconcile_paperfig_01.pdf" title="Reconciling Kaplan and Chinchilla scaling laws" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Concept Encoding phenomena and Concept Decodability(CD) as predictive of ICL performance
</div>

<div class="row">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/publication_preview/publications/rep_umap_keys_Representations at Layer 15 - Part-Of-Speach Tagging.pdf" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/publication_preview/publications/rep_umap_keys_Representations at Layer 13 - Bitwise Operations.pdf" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


TO be updated