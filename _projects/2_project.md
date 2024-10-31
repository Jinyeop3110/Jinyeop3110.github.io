---
layout: page
title: Neural Scaling Laws(NSL)
description: Diverse studies on emergent Neural Scaling Laws(NSL) of AI
img: assets/img/publication_preview/reconcile_nsl.png
importance: 2
category: Sceince of AI
giscus_comments: true
---

The Neural Scaling Law(NSL) [kaplan2020scaling, hoffmann2022training] refers to how language models scale with respect to key factors: model size, training data size, and computational resources. This scaling law is important to anlyze since it enable how "perofrmance gain" we can expect by scaling up the AI model and data.
However, [kaplan2020scaling, hoffmann2022training] has empricially measured different scaling coefficients for lage langague model. In paper (Under review in TMLR) <a href="https://arxiv.org/pdf/2406.12907">"Reconciling Kaplan and Chinchilla Scaling Laws"</a> , we aim to identify the origin of such discrepancy through analytic methods and small langauge model traning.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/reconcile_paperfig_01.pdf" title="Reconciling Kaplan and Chinchilla scaling laws" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

On the other hand, it is unknown why such a law occurs and holds across various tasks, including language, vision, and even proteins. Previously, in our workshop paper at ICLR 2024, <a href="https://arxiv.org/pdf/2402.05164">**"A RESOURCE MODEL FOR NEURAL SCALING LAWS"**</a>, we propose the **"resource model"** as a **phenomenological model** to explain the scaling laws of large language models (LLMs). Resource model hypotheses are as follows.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/ResourceModel/1.png" title="fig1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/ResourceModel/2.png" title="fig1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/ResourceModel/3.png" title="fig1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Based on the hypotheses of the Resource Model, we derive a \(-1\) scaling law for general composite tasks.

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/ResourceModel/4.png" title="fig1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/ResourceModel/fig1.png" title="fig1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
--
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/ResourceModel/fig2.png" title="fig2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
--
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/ResourceModel/fig3.png" title="fig3" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/ResourceModel/fig4.png" title="fig4" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
--
</div>


