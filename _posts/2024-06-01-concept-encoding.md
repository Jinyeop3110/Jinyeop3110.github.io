---
layout: post
title: Emergence and Effectiveness of Task Vectors in In-Context Learning
description: >
  Understanding why in-context learning succeeds or fails through the lens of concept encoding in intermediate representations.
date: 2024-06-01
image:
  path: /assets/img/projects/concept_encoding.png
categories: [research]
tags: [icl, llm, mechanistic-interpretability]
---

![Concept Encoding Overview](/assets/img/projects/concept_encoding.png){:.lead width="800" loading="lazy"}

Overview of the Concept Encoding phenomenon and Concept Decodability (CD)
{:.figcaption}

## Summary

**TL;DR:** We explored the mechanistic understanding of ICL success/failure modes through how well certain concepts are encoded in intermediate representations.

Why does in-context learning (ICL) succeed or fail depending on the task? We explored the mechanisms behind these success and failure modes and sought to quantify them.

## Concept Encoding Phenomena

We introduced the **Concept Encoding** phenomenon, which posits that representations are effectively distinguished by latent concepts. Our findings demonstrate that concept encoding occurs in the Llama 3 8B model, as evidenced by realistic latent concepts such as verbs and nouns in part-of-speech tagging, as well as logical operators like AND and OR in bitwise operations.

## Key Findings

We conjecture that concept decodability—specifically, how well a given concept is separated in intermediate representations—can predict in-context learning (ICL) performance. Our observations indicate that this holds true for both the part-of-speech (POS) task and bitwise operation tasks.

### Causal Analysis

We performed various interventions and causal experiments supporting the claim that concept encoding is indeed causally related to ICL performance:

- **Perturbation Analysis**: Perturbing concept representations affects ICL accuracy
- **Fine-tuning Experiments**: Fine-tuning improves both concept decodability and ICL performance
- **Prompting Studies**: Different prompting strategies affect concept encoding patterns

## Citation

```bibtex
@article{song2024context,
  title={Emergence and Effectiveness of Task Vectors in In-Context Learning: An Encoder Decoder Perspective},
  author={Han, Seungwook and Song, Jinyeop and Gore, Jeffrey and Agrawal, Pulkit},
  journal={ICML 2025 (Spotlight)},
  year={2024}
}
```

**Paper:** [arXiv:2412.12276](https://arxiv.org/abs/2412.12276) - **ICML 2025 Spotlight (Top 2.5%)**
