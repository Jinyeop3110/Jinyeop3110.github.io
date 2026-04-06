---
layout: post
title: "Protein LLM: Teaching Language Models to Understand Proteins"
description: >
  A living overview of the Protein LLM project — bridging ESM-3 protein embeddings with
  large language models through supervised fine-tuning and reinforcement learning.
  This post summarizes the full journey and links to detailed deep dives.
date: 2026-03-20
categories: [research]
tags: [llm, protein, multimodal, esm3, series-overview]
---

<div class="central-thesis">
  <div class="thesis-label">The Project</div>
  <p class="thesis-text">Can we teach a language model to effectively leverage protein structural embeddings — going beyond raw amino acid sequences to reason about structure, function, and evolutionary relationships — by bridging a protein encoder with an LLM?</p>
</div>

This is a living summary of the Protein LLM project. Each section captures a phase of the work and links to the full write-up. New entries will be added as the project progresses.

---

## The Architecture

We connect two worlds: **ESM-3**, a protein foundation model that encodes structural and evolutionary knowledge into 1536-dimensional embeddings, and **Qwen3-8B-Instruct**, a general-purpose LLM. A learnable bridge (pooling + projector) translates between them. ESM-3 stays frozen; the LLM adapts via LoRA.

To isolate what each component contributes, we designed a **four-way comparison**:

| Approach | How protein enters the LLM | Trainable params |
|----------|---------------------------|-----------------|
| **Text** | Raw sequence as `<protein>MKTL...</protein>` tokens | ~2M (LoRA only) |
| **MLP** | ESM-3 → AttentionPooling (32 tokens) → MLP projector | ~32.5M |
| **Perceiver** | ESM-3 → Perceiver Resampler (cross-attention) | ~31.4M |
| **Flamingo** | ESM-3 → Perceiver → Gated cross-attention at LLM layers | ~120-150M |

We also explored the full training pipeline: **SSL** (continued pre-training on biology literature) → **SFT** (instruction fine-tuning on protein tasks) → **GRPO** (reinforcement learning with verifiable rewards).

**Read the full story:** [Part 1 — Building a Protein-Understanding LLM](/research/2026-02-25-protein-llm-journey/)

---

## Scaling Data: 50K → 4.9 Million Samples

Our first 50K-sample run proved the architecture converges. But one data source wasn't enough — the model learned one annotation style and struggled to generalize. We assembled **4.89 million instruction pairs** from six sources: Mol-Instructions, Swiss-Prot, ProteinLMDataset, SwissProtCLAP, ProtDescribe, and Protein2Text-QA.

The result was substantial (note: these numbers are from the original 4.89M dataset, before curation to 1.82M — see caveat below):

| Metric | 50K / Qwen3-4B | 4.89M / Qwen3-8B | Change |
|--------|----------------|-------------------|--------|
| eval_loss | 3.64 | **0.361** | -90.1%* |
| BLEU (best, step 9250) | — | 0.315 | first measurement |
| ROUGE-L (best, step 9250) | — | 0.515 | first measurement |

*\*This comparison spans both a model change (4B→8B) and data change (50K→4.89M). On the same 8B model, data scaling alone gave an 81% reduction (1.91→0.361).*

The key observation: **data diversity and scale together produced the largest gains**, substantially exceeding the effect of model scaling alone. 72% of proteins appear across multiple sources but described differently each time — function annotations, structural domains, QA pairs, long-form paragraphs. We hypothesize that multiple annotation perspectives help generalization, though disentangling diversity from scale requires further experiments.

**Important:** The 4.89M dataset was later refined to **1.82M samples** after discovering protein overlap between train and evaluation splits. The eval_loss numbers above may be inflated by this leakage. Re-evaluation on the curated dataset is planned.

**Read the full story:** [Part 2 — Scaling to 4.9 Million Samples](/research/2026-03-07-protein-llm-scaling/)

---

## Reinforcement Learning: The Gradient Routing Problem

With a strong SFT checkpoint in hand, we applied **GRPO** (Group Relative Policy Optimization) using verifiable rewards — no reward model needed, just computed metrics like pLDDT structural quality scores.

Then came the surprise. The rankings **completely inverted**:

| Model | SFT eval_loss | GRPO Reward (best) |
|-------|--------------|-------------|
| ESM3+MLP | **0.361** (better) | 0.780 (worse) |
| Text-only | 1.207 (worse) | **0.832** (better) |

The model with lower SFT loss learned *worse* from RL. Why?

**The gradient routing problem.** During GRPO, gradients flow predominantly to either the projector OR the LoRA adapters — not both effectively. One pathway captures most of the signal, starving the other. SFT doesn't have this issue because its dense per-token loss flows naturally through the entire graph. GRPO's sparse scalar reward creates a competition.

In the worst case (standard configuration with gradient-starved LoRA), MLP reward was only 0.582. The partial fix: **freeze the projector** during GRPO, forcing all signal through LoRA. This raised MLP reward to **0.774**. A separate MLP run with different hyperparameters reached 0.780 — but text-only still leads at 0.832.

This SFT→RL inversion is the central open question of the project.

**Read the full story:** [Part 3 — The Gradient Routing Problem](/research/2026-03-13-protein-llm-grpo-gradient-routing/)

---

## What's Next

These are the active and planned directions. New posts will be added here as they're written.

### SSL: Domain Pre-Training
Continued pre-training on 50GB of biology literature (PMC papers, PubMed abstracts, protein sequences in context) using Qwen3.5-4B BASE with LoRA. The goal: inject biological domain knowledge *before* instruction tuning, creating a stronger foundation for both SFT and GRPO.

### Perceiver & Flamingo at Scale
Both architectures are implemented and validated on small data but untested at 4.89M scale. The Perceiver uses cross-attention instead of concatenation — it may exhibit different gradient routing during GRPO. Flamingo inserts protein information via gated cross-attention at every 4th LLM layer, a fundamentally different integration strategy.

### Resolving the Gradient Routing Problem
Three approaches under investigation:
1. **Two-stage GRPO** — freeze projector first (teach format), then unfreeze (structural refinement)
2. **Gradient balancing** — GradNorm or PCGrad to prevent winner-take-all dynamics
3. **Architectural solutions** — Perceiver/Flamingo may route gradients differently

### Downstream Evaluation
GO term prediction (F1), protein stability prediction (MAE), structure quality assessment — task-specific benchmarks that measure whether lower loss translates to genuine scientific utility.

---

## Timeline

| Date | Phase | Key Result |
|------|-------|------------|
| Feb 2026 | Architecture & first training | ESM3+MLP converges; 50K SFT eval_loss=3.64 |
| Mar 7 | Data scaling | 4.89M samples; eval_loss **0.361** (-90.1%) |
| Mar 13 | GRPO reinforcement learning | Gradient routing problem discovered; text 0.832 vs MLP 0.582 |
| Mar 16 | SSL pipeline & curated data | 50GB SSL corpus + 1.82M curated SFT dataset prepared |
| TBD | SSL pre-training | Qwen3.5-4B continued pre-training on biology literature |
| TBD | Four-way comparison | Text vs MLP vs Perceiver vs Flamingo at scale |
| TBD | Gradient routing fix | Two-stage GRPO / gradient balancing |

---

<div class="conclusion">

## The Story So Far

We set out to bridge protein language models with LLMs. The architecture works — ESM-3 embeddings show a large eval_loss advantage over raw text during supervised learning on the 4.89M dataset (0.361 vs 1.207, though these numbers are pre-curation). Scaling data from diverse sources produced the largest SFT gains. But reinforcement learning revealed an unexpected tension: the multimodal pathway that excels at SFT struggles with sparse reward optimization.

The gradient routing problem — observed so far on the structure quality GRPO task — may be relevant to other multimodal RL settings where an encoder bridge and LLM adapters compete for gradient signal. Whether it generalizes beyond our specific setup remains an open question.

</div>

## Resources

**Project Repository:** [Post_Training_Protein_LLM](https://github.com/Jinyeop3110/Post_Training_Protein_LLM)

**Detailed Posts:**
- [Part 1: Building a Protein-Understanding LLM](/research/2026-02-25-protein-llm-journey/) — Architecture, first training, debugging
- [Part 2: Scaling to 4.9 Million Samples](/research/2026-03-07-protein-llm-scaling/) — Data diversity, loss curves, generation quality
- [Part 3: The Gradient Routing Problem](/research/2026-03-13-protein-llm-grpo-gradient-routing/) — GRPO RL, SFT→RL inversion, gradient analysis

**Key References:**
- [ESM-3: Protein Language Model](https://github.com/facebookresearch/esm)
- [Mol-Instructions Dataset (ICLR 2024)](https://arxiv.org/abs/2306.08018)
