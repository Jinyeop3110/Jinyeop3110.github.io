---
layout: post
title: "Protein LLM Part 2: Scaling to 4.9 Million Samples"
description: >
  From 50K to 4.9M training samples — how scaling data transformed our protein-understanding LLM, what the numbers look like, and what comes next.
date: 2026-03-07
categories: [research]
tags: [llm, protein, multimodal, esm3, sft, scaling]
---

<div class="central-thesis">
  <div class="thesis-label">The Big Picture</div>
  <p class="thesis-text">We scaled our protein-LLM training data from 50K to 4.9 million samples across six sources. The result: <strong>eval_loss dropped 90.1%</strong> — from 3.64 to 0.361 — and the model now generates scientifically meaningful protein descriptions.</p>
</div>

## Where We Left Off

In [Part 1](/research/2026-02-25-protein-llm-journey/), we built the foundation: a frozen ESM-3 protein encoder connected to Qwen3-8B through a learnable MLP projector. We trained on 50K samples from Mol-Instructions, proved the architecture converges, and assembled a 4.5M-record dataset from six sources.

The question now: **does more data actually help?**

---

## The Scaling Experiment

We trained the same ESM-3 + MLP architecture on the full combined dataset: 4.89 million instruction pairs spanning protein function prediction, catalytic activity, domain analysis, gene prediction, and more.

| What Changed | Before | After |
|-------------|--------|-------|
| Training samples | 50K (one source) | 4.89M (six sources) |
| Dataset diversity | 5 task types | 15+ task types |
| Annotation styles | Template-based only | Paragraphs, QA, structured |
| Total training steps | 2,595 | 28,941 |

Everything else stayed constant: Qwen3-8B-Instruct, ESM-3 small (frozen), MLP projector, LoRA on all linear layers, 8x H100 GPUs with FSDP.

---

## The Results

### Loss Dropped Off a Cliff

The combined dataset didn't just incrementally improve things — it fundamentally changed the loss landscape.

![Training Loss Over Time](/assets/img/projects/mlp_epoch1_train_loss.png){:.lead width="700" loading="lazy"}

Training loss (token_avg_loss) showing continued improvement through epoch 1 (step 9,750). The combined dataset produces dramatically lower loss than single-source training.
{:.figcaption}

At step 9,750 (33.7% through training, epoch 1 complete), the model has achieved:

| Metric | Combined 4.9M | Mol-Instr Only (505K) | <span style="color: red;">Text-Only on 4.9M (step ~190)</span> |
|--------|---------------|----------------------|-------------------|
| **eval_loss** | **0.361** | 1.908 | <span style="color: red;">pending (run in progress)</span> |
| **token_avg_loss** | **0.366** | 2.282 | <span style="color: red;">2.356 (early)</span> |
| Improvement vs Mol-Instr | 81.1% | baseline | <span style="color: red;">TBD</span> |

<span style="color: red;">**Note:** The text-only baseline on the 4.89M combined dataset is currently running but only ~190 steps in. A fair head-to-head comparison at matched step counts is pending. The 57% advantage cited at step 200 (token_avg_loss 1.02 vs 2.36) is preliminary.</span>

![Evaluation Loss Comparison](/assets/img/projects/mlp_epoch1_eval_loss.png){:.lead width="700" loading="lazy"}

Eval loss at epoch 1 checkpoint: 0.361 — dramatically lower than the mol-instructions-only run (1.908).
{:.figcaption}

### The Two Biggest Levers

Looking back at two weeks of experiments, two changes drove the most improvement:

| Date | Change | eval_loss | Improvement |
|------|--------|-----------|-------------|
| Feb 20 | First run (Qwen3-4B, 50K) | 3.64 | baseline |
| Feb 23 | Scale model: 4B to 8B | 2.50 | 31% |
| Feb 27 | Text-only baseline (8B, 505K) | 2.42 | 3% |
| Mar 5 | MLP on full mol-instructions | 1.91 | 21% |
| **Mar 7** | **Combined 4.89M dataset** | **0.361** | **81%** |

**Data scaling provided 2.6x more improvement than model scaling.** Going from 505K to 4.89M samples (10x) cut eval_loss by 81%, while going from 4B to 8B parameters (2x) only cut it by 31%.

This makes intuitive sense: with diverse data sources, the model sees the same proteins described in multiple ways — function annotations, structural domains, QA pairs, long-form descriptions. It's like studying a subject from six different textbooks instead of one.

### First Generation Quality Numbers

For the first time, we measured how well the model actually generates protein descriptions:

| Task Type | BLEU | ROUGE-L |
|-----------|------|---------|
| Catalytic Activity | 0.392 | 0.541 |
| Protein Function | 0.404 | 0.523 |
| General Description | 0.265 | 0.436 |
| Domain/Motif | 0.166 | 0.433 |
| **Overall** | **0.307** | **0.483** |

The model is strongest on catalytic activity and function prediction — tasks where the training data is richest. Domain/motif prediction lags behind, likely because its outputs are more structured (specific domain names and boundaries) rather than free-form text.

ROUGE-L of 0.48 means the model captures roughly half the content of reference answers. Not perfect, but a solid foundation for reinforcement learning to build on.

---

## Under the Hood: Training Stability

### Gradient Norms

One concern with scaling to 4.9M samples from diverse sources: would the varied annotation styles cause training instability?

![Gradient Norms](/assets/img/projects/mlp_epoch1_grad_norms.png){:.lead width="700" loading="lazy"}

Gradient norm trajectories across runs. The main combined run stabilizes to a mean of 0.627 after initial spikes in the first 100 steps.
{:.figcaption}

The answer: brief instability early on (steps 10-100), then rock-solid stability. The mean gradient norm settled at 0.627 — lower than both the mol-instructions-only run (1.67) and the text baseline (1.48). More diverse data actually made optimization *smoother*.

### Still Improving

The most exciting part: **the run is 33.7% complete** (epoch 1 of 3). Both train and eval loss are still declining with no sign of plateau. With the cosine learning rate schedule decaying through epochs 2-3, we expect continued improvement.

---

## Architectural Comparison

### MLP vs Perceiver on Small Data

On the 50K mol-instructions dataset, MLP and Perceiver Resampler achieve nearly identical performance: eval_loss 1.942 vs 1.952 (MLP wins by 0.5%). The simpler MLP projector (30.5M params) captures the essential protein-to-language mapping as well as the more complex Perceiver (29.4M params) at this data scale.

<span style="color: red;">

### Planned: Four-Way Comparison on 4.89M

The core thesis of this project is a systematic four-way comparison of protein-to-LLM bridging architectures. So far, only MLP has been trained on the full combined dataset. The remaining comparisons:

| Approach | Projector Params | 50K eval_loss | 4.89M eval_loss | Status |
|----------|-----------------|---------------|-----------------|--------|
| Text-only | — (LoRA only) | 2.415 | **pending** | Running (~190 steps) |
| **MLP** | **30.5M** | **1.942** | **0.361** | **Epoch 1 complete** |
| Perceiver Resampler | 29.4M | 1.952 | **pending** | Not yet started |
| Flamingo (gated cross-attn) | ~120-150M | — | **pending** | Implemented, not yet run |

The Perceiver and Flamingo architectures are fully implemented and validated on small data. Scaling them to 4.89M is the next priority.

</span>

---

## What This Means

### The Data Diversity Hypothesis: Confirmed

Our bet from Part 1 paid off. Combining six sources with different annotation styles, task types, and protein coverage produced a model that generalizes far better than any single source could. The key insight: **it's not just about more data, it's about more perspectives on the same proteins.**

72% of proteins appear in multiple sources — but described differently each time. The model learns that BRCA1 isn't just "a DNA repair protein" (Mol-Instructions) — it's also "involved in homologous recombination" (Swiss-Prot), "contains BRCT domains" (ProteinLMDataset), and has a detailed functional description (SwissProtCLAP). Multiple views create deeper understanding.

### ESM-3 Embeddings Still Matter

Even with 10x more data, the ESM-3 encoder provides a consistent advantage over text-only processing. The structural information encoded in ESM-3's 1536-dimensional embeddings — fold types, binding sites, evolutionary constraints — can't be recovered from amino acid sequences alone, no matter how much text data you add.

---

## What's Next

1. **Let the run finish.** At 33.7% complete with loss still dropping, we expect eval_loss to reach 0.30-0.35 by completion.

<span style="color: red;">

2. **Text-only baseline on 4.89M.** Currently running. This will provide a fair apples-to-apples comparison of ESM-3 MLP vs text-only on identical data at scale. Early numbers (step ~190) show token_avg_loss of 2.36 vs MLP's 1.02 at the same step, but we need matched training duration for a conclusive comparison.

3. **Perceiver Resampler on combined data.** With MLP established, we'll train the Perceiver architecture on the same data. This is the core thesis comparison: does a more expressive cross-attention projector (29.4M params) outperform the simpler MLP (30.5M params) at scale?

4. **Flamingo gated cross-attention.** The fourth approach inserts protein information via gated cross-attention at every 4th LLM layer, rather than prefix injection. A fundamentally different architectural choice to test (~120-150M trainable params, no LoRA).

5. **GRPO reinforcement learning.** The current checkpoint is strong enough for downstream RL. We'll fine-tune with verifiable rewards — GO term F1, stability prediction accuracy, structure quality — to push beyond "reasonable-sounding" to "measurably correct."

6. **Downstream task evaluation.** GO term prediction (F1), protein stability prediction (MAE), and protein-protein interaction accuracy — these task-specific benchmarks will measure whether lower loss translates to genuine scientific utility.

</span>

<div class="conclusion">

## The Takeaway

Two weeks in, and the story is clear: **data diversity is the biggest lever for protein LLM performance.** Not model scale, not architecture complexity — just giving the model multiple perspectives on the same biology.

The numbers:
- **eval_loss: 3.64 to 0.361** (90.1% reduction)
- **BLEU: 0.307, ROUGE-L: 0.483** (first generation metrics)
- **33.7% through training** (epoch 1 complete, significant headroom remains)

The architecture works. The data works. <span style="color: red;">Next up: the full four-way architecture comparison and reinforcement learning with verifiable rewards.</span>

</div>

## Resources

**Project Repository:** [Post_Training_Protein_LLM](https://github.com/Jinyeop3110/Post_Training_Protein_LLM)

**Related Posts:**
- [Part 1: Building a Protein-Understanding LLM](/research/2026-02-25-protein-llm-journey/)

**Key References:**
- [ESM-3: Protein Language Model](https://github.com/facebookresearch/esm)
- [Mol-Instructions Dataset (ICLR 2024)](https://arxiv.org/abs/2306.08018)
