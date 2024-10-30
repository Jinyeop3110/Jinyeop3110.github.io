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

Therefore, our goal is to develop a foundation model(MethylGPT) specifically for human methylation data(DNAm), paving the way for future research. We curated about 300,000 DNAm data from public, deduplicate and curated them into 154,063 human DNAm. DNA methylation data have varying numbers of CpG entries depending on the array platform (Il-lumina 27k, Illumina 450k, and EPIC). To address these differences and ensure biological rele-vance, we focused on 49,156 CpG sites. So In total, 7.6 billion training tokens are used for pretraining.

Our model architecture and training is specialized for DNAm data. First, training loss : pretraining process includes the Masked Language modeling(MLM)-style approach and Autoregressive Generative -style approach. Both optimize the correct prediction of methylation value close to the original value under the information is blocked. Second, 



<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/methylGPT/Picture1.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/methylGPT/Picture2.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/methylGPT/Picture3.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/methylGPT/Picture4.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/methylGPT/Picture5.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

MethylGPT captures biologically meaningful sample-level features, such as tissue information, sex and disease tpyes compared than raw methylation data directly generated UMAP embeddings (Fig. 3d-f)


MethylGPT learns tissue-specific and sex-specific methylation patterns


. MethylGPT achieved superior accuracy( median absolute error (MedAE) of 4.45 ) in predicting biological age than other SOTA methods(ElasticNet [@zou2005], MLP (AltumAge) [@delimacamillo2022]).



Age-specific attention patterns reveal distinct methylation signatures by age groups(younger - elder).


Disease risk prediction and intervention analysis


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
