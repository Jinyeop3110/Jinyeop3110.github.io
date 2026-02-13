---
layout: post
title: MethylGPT
description: >
  A foundation model approach to understanding human methylation patterns - under review at Nature Methods.
date: 2024-09-01
image:
  path: /assets/img/projects/methylgpt.png
categories: [research]
tags: [foundation-models, biology, methylation]
---

![MethylGPT Overview](/assets/img/projects/methylgpt.png){:.lead width="800" loading="lazy"}

## Overview

MethylGPT is a foundational GPT-like model designed for human methylation data, applying transformer architectures to biological sequence analysis.

## Background

DNA methylation is an epigenetic modification that plays a crucial role in gene regulation, development, and disease. Traditional analysis methods are often limited in their ability to capture complex patterns across the methylome.

## Approach

MethylGPT applies the foundation model paradigm—successful in natural language processing—to methylation data:

- **Pre-training** on large-scale methylation datasets
- **Transfer learning** to downstream tasks
- **Interpretable representations** of methylation patterns

## Key Contributions

1. **Scalable Architecture**: GPT-style transformer adapted for methylation arrays
2. **Pre-trained Foundation Model**: Can be fine-tuned for various downstream tasks
3. **Biological Insights**: Learned representations capture meaningful biological signals

## Status

Currently under review at **Nature Methods**.

## Citation

```bibtex
@article{ying2024methylgpt,
  title={MethylGPT: Foundational GPT-like Model for Human Methylation Data},
  author={Ying, Alex and Song, Jinyeop and Cui, Haoran and others},
  journal={bioRxiv},
  year={2024}
}
```

**Preprint:** [bioRxiv](https://www.biorxiv.org/content/10.1101/2024.10.30.621013v2)
