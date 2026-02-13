---
layout: post
title: Concept Encoding in In-Context Learning
description: >
  Understanding why in-context learning succeeds or fails through the lens of concept encoding in intermediate representations.
date: 2024-06-01
image:
  path: /assets/img/projects/concept_encoding.png
categories: [research]
tags: [icl, llm, mechanistic-interpretability]
---

![Concept Encoding Overview](/assets/img/projects/concept_encoding.png){:.lead width="800" loading="lazy"}

Overview of Concept Encoding phenomena and Concept Decodability (CD)
{:.figcaption}

## Summary

**TLDR:** We explored the mechanistic understanding of ICL success/failure modes through how well certain concepts are encoded in intermediate representations.

Why does in-context learning (ICL) succeed or fail depending on the task? We explored the mechanisms behind these success and failure modes and sought to quantify them.

## Concept Encoding Phenomena

We introduced the concept of **Concept Encoding** phenomena, which posits that representations are effectively distinguished by latent concepts. Our findings demonstrate that concept encoding occurs in the LLAMA3 8B model, as evidenced by realistic latent concepts such as verbs and nouns in part-of-speech tagging, as well as logical operators like AND and OR in bitwise operations.

## Key Findings

We conjecture that concept decodability—specifically, how well a given concept is separated in intermediate representations—can predict in-context learning (ICL) performance. Our observations indicate that this holds true for both the part-of-speech (POS) task and bitwise operation tasks.

### Causal Analysis

We performed various interventions and causal relation experiments supporting that concept encoding phenomena is indeed causally related with the ICL performance:

- **Perturbation Analysis**: Perturbing concept representations affects ICL accuracy
- **Fine-tuning Experiments**: Fine-tuning improves both concept decodability and ICL performance
- **Prompting Studies**: Different prompting strategies affect concept encoding patterns

## Citation

```bibtex
@article{song2024context,
  title={Context to Concept: Concept Encoding in In-context Learning},
  author={Song, Jinyeop and Han, Sumin and Argawal, P. and Gore, Jeffrey},
  journal={ICML 2025 (Spotlight)},
  year={2024}
}
```

**Paper:** [arXiv:2412.12276](https://arxiv.org/abs/2412.12276) - **ICML 2025 Spotlight (Top 2.5%)**
