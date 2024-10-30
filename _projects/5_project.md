---
layout: page
title: MethylGPT
description: a project with a background image
img: assets/img/1.jpg
importance: 3
category: AI for science
---

{% raw %}

```html

MethylGPT: a foundation model for the DNA methylome
Kejun Ying1,2,†,*,, Jinyeop Song3,†, Haotian Cui4,5,6,†, Yikun Zhang1,†, Siyuan Li1, Xingyu Chen5,6, Hanna Liu1, Alec Eames1, Daniel L McCartney7, Riccardo E. Marioni7, Jesse R. Poganik1, Mahdi Moqri1,*, Bo Wang5,6,*, Vadim N. Gladyshev1,*
```html

{% endraw %}

**TLDR:** We are building a foundation model for processing natural language representations of human methylation profiles, advancing research in biological aging and medicine.

Human DNA methylation data (methylome) is an important biomarker for aging and chronic diseases. Despite its significance, a unified and adaptable framework has yet to emerge, largely due to the absence of a "foundation model." Foundation models have already proven essential for understanding the complexities of biology. For instance, in proteomics, models like ESM-2/ESM-3 and AlphaFold2/AlphaFold3 have achieved unprecedented accuracy in structure prediction and function annotation. In genomics, Enformer and Evo have demonstrated their ability to predict gene regulation and variant effects. Similarly, in single-cell biology, models such as Geneformer, scGPT, and scFoundation have enabled zero-shot cell-type classification and in-silico perturbation.

Therefore, our goal is to develop a foundation model specifically for human methylation data, paving the way for future research. We curated fro

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
