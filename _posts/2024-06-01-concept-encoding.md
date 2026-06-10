---
layout: post
title: Emergence and Effectiveness of Task Vectors in In-Context Learning
description: >
  Encoder-decoder analysis of compact task vectors that drive in-context predictions.
date: 2024-06-01
image:
  path: /assets/img/projects/concept_encoding.png
categories: [research]
tags: [icl, llm, mechanistic-interpretability]
---

![Task Vectors Overview](/assets/img/projects/concept_encoding.png){:.lead width="800" loading="lazy"}

Overview figure for the task-vector analysis in in-context learning.
{:.figcaption}

## Summary

**TL;DR:** We studied how transformers form compact task vectors during in-context learning and how those vectors drive predictions.

Why does in-context learning (ICL) succeed or fail depending on the task? We explored this through an encoder-decoder perspective: how a model encodes the task from context examples and decodes that task information into predictions.

## Task-Vector Formation

The paper analyzes task vectors as compact internal representations that emerge during pretraining and support in-context predictions.

## Key Findings

The main finding is that transformer models can form compact task vectors that causally contribute to in-context predictions.

### Causal Analysis

We performed intervention analyses supporting the claim that task-vector representations are not only correlated with ICL behavior, but help drive it.

- **Representation analysis**: Track compact task information in intermediate representations
- **Causal interventions**: Test whether modifying task-vector directions changes predictions
- **Encoder-decoder framing**: Separate task encoding from prediction decoding

## Citation

```bibtex
@article{song2024context,
  title={Emergence and Effectiveness of Task Vectors in In-Context Learning: An Encoder Decoder Perspective},
  author={Song, Jinyeop and Han, Seungwook and Agrawal, Pulkit and Gore, Jeffrey},
  journal={ICML 2025 (Spotlight)},
  year={2024}
}
```

**Paper:** [arXiv:2412.12276](https://arxiv.org/abs/2412.12276) - **ICML 2025 Spotlight**
