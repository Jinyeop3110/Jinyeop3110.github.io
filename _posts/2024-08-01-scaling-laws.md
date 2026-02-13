---
layout: post
title: Neural Scaling Laws
description: >
  Diverse studies on emergent Neural Scaling Laws (NSL) of AI - reconciling different formulations and proposing theoretical models.
date: 2024-08-01
image:
  path: /assets/img/projects/reconcile_nsl.png
categories: [research]
tags: [scaling-laws, llm, theory]
---

![Scaling Laws Overview](/assets/img/projects/reconcile_nsl.png){:.lead width="800" loading="lazy"}

## Reconciling Kaplan and Chinchilla Scaling Laws

The Neural Scaling Law (NSL) refers to how language models scale with respect to key factors: model size, training data size, and computational resources. This scaling law is important to analyze since it enables predicting how much "performance gain" we can expect by scaling up AI models and data.

However, Kaplan et al. and Hoffmann et al. (Chinchilla) have empirically measured different scaling coefficients for large language models. In our TMLR paper ["Reconciling Kaplan and Chinchilla Scaling Laws"](https://arxiv.org/abs/2406.12907), we aim to identify the origin of such discrepancy through analytic methods and small language model training.

## Origin of Neural Scaling Laws: The Resource Model

On the other hand, it is unknown why such a law occurs and holds across various tasks, including language, vision, and even proteins. In our ICLR 2024 workshop paper ["A Resource Model for Neural Scaling Laws"](https://arxiv.org/abs/2402.05164), we propose the **"resource model"** as a phenomenological model to explain the scaling laws of large language models.

### Resource Model Hypotheses

The Resource Model hypothesizes that:

1. **Tasks are composed of subtasks** - Complex tasks can be decomposed into simpler components
2. **Resources are limited** - Model capacity acts as a limited resource distributed across subtasks
3. **Power-law emergence** - The combination of these factors leads to power-law scaling behavior

Based on these hypotheses, we derive a **-1 scaling law** for general composite tasks.

## Publications

- **Reconciling Kaplan and Chinchilla Scaling Laws**
  Tim Pearce, *Jinyeop Song*
  TMLR 2024 | [arXiv:2406.12907](https://arxiv.org/abs/2406.12907)

- **A Resource Model for Neural Scaling Law**
  *Jinyeop Song*, Ziming Liu, Max Tegmark, Jeff Gore
  ICLR 2024 BGPT Workshop | [arXiv:2402.05164](https://arxiv.org/abs/2402.05164)

## Citation

```bibtex
@article{pearce2024reconciling,
  title={Reconciling Kaplan and Chinchilla Scaling Laws},
  author={Pearce, Tim and Song, Jinyeop},
  journal={TMLR},
  year={2024}
}

@article{song2024resource,
  title={A resource model for neural scaling law},
  author={Song, Jinyeop and Liu, Ziming and Tegmark, Max and Gore, Jeff},
  journal={ICLR BGPT workshop},
  year={2024}
}
```
