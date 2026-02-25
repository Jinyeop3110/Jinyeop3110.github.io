---
layout: post
title: "A Systems Biology Approach to Multi-LLM Agent Systems"
description: >
  Research proposal on applying systems biology principles to understand and stabilize multi-agent LLM training dynamics.
date: 2025-02-01
categories: [research]
tags: [llm-agents, multi-agent, systems-biology, rl]
---

<div class="central-thesis">
  <div class="thesis-label">Central Thesis</div>
  <p class="thesis-text">Systems Biology offers a productive lens for understanding multi-LLM agent dynamics—treating agents as nodes in regulatory networks enables principled approaches to stability and optimization.</p>
</div>

## The Challenge: Training Multi-Agent Systems

Multi-LLM agent systems excel in real-world tasks—solver–refiner pipelines for math reasoning and coding, multi-agent retrieval-augmented generation (RAG), and collaborative scientific tools. In these systems, role-specialized agents tackle partial subtasks and, through orchestration, collectively solve the end task.

<div class="callout">
  <div class="callout-label">Key Problem</div>
  <p>Current implementations rely heavily on large foundation models and static prompts, leading to cost inefficiency and prompt-dependent capabilities that limit practical, scalable deployment.</p>
</div>

A natural alternative is multi-agent systems built with cost-efficient models, with each agent fine-tuned via SFT or RL for their roles. However, when we jointly train the network of agents for end-to-end performance, the agents' learning becomes **coupled and non-stationary**, creating multi-body dynamics that make optimization challenging.

## Why Systems Biology?

Systems Biology studies how interacting components—genes, neurons, or species—give rise to stable, functional behavior at the system level. I believe that knowledge and ideas in systems biology can transfer to multi-LLM-agent systems to address these challenges.

<div class="pillars">
  <div class="pillar">
    <div class="pillar-title">Project 1</div>
    <p>Network Motifs: Applying regulatory network theory to predict and control stability in multi-agent systems.</p>
  </div>
  <div class="pillar">
    <div class="pillar-title">Project 2</div>
    <p>Pool-of-Agents: A population-based training methodology inspired by evolutionary dynamics.</p>
  </div>
</div>

## Project 1: Network Motifs for Multi-Agent Dynamics

### Feed-Forward Loops in Biology

Feed-forward loops (FFLs) are recurring three-node regulatory patterns found throughout biological transcription networks. In an FFL, three nodes—X, Y, and Z—form two paths: X directly regulates both Y and Z, and Y also regulates Z.

- **Coherent FFLs** (same sign on both paths): Enable persistence detection and signal stabilization
- **Incoherent FFLs** (opposite signs): Generate pulse responses and adaptation

### Mapping to Multi-Agent Systems

We can treat each agent as a node whose "expression level" is its **task competence** A<sub>i</sub>(t)—the agent's learned performance at training step t. Edges represent learning influences:

- **Positive edge (X → Y)**: Improving agent X accelerates Y's learning (e.g., better retriever → sharper reasoner signal)
- **Negative edge (X ⊣ Y)**: Improving X throttles Y's updates (e.g., stricter critic → reduced solver exploration)

<div class="callout">
  <div class="callout-label">Hypothesis</div>
  <p>C1-FFLs stabilize training by filtering spurious reward signals, whereas I1-FFLs accelerate early exploration via rapid transient responses—though with higher risk of oscillatory behavior.</p>
</div>

## Project 2: Pool-of-Agents Training

### The Instability Problem

One major challenge of current RL-based LLM finetuning (PPO, GRPO) is inherent instability. In multi-agent setups, this compounds dramatically—each agent's policy updates simultaneously affect the training signals of all other agents, creating cascading failures.

### Inspiration from Population Genetics

In large populations, selection is more efficient and genetic drift (stochastic noise) is weaker, producing more reproducible evolutionary dynamics. Adopting this principle, we propose maintaining a **Pool-of-Agents** for each role:

1. Pool members perform identical roles but are initialized with slightly different policies
2. During each rollout, sample one member from each pool
3. Update using standard gradient-based methods or evolution strategies

<div class="callout">
  <div class="callout-label">Expected Benefits</div>
  <p><strong>Reduced variance</strong> through ensemble averaging, <strong>robust exploration</strong> of the strategy space, and <strong>resistance to cascading failures</strong> from individual agent updates.</p>
</div>

<div class="conclusion">

## Looking Forward

The goal is to establish principled methods for stable multi-LLM-agent optimization, deriving design principles that enable architects to predict and control learning dynamics across different topologies and hyperparameters.

This research bridges my background in systems biology with my current focus on LLM agents—applying ecological and evolutionary thinking to one of the most pressing challenges in AI systems design.

</div>

## Resources

**Full Proposal:** [Research Statement (PDF)](/assets/pdf/Research_Statement_multiagent.pdf)

**Related Work:**
- [EELMA: Estimating Empowerment of LLM Agents](/research/2025-01-01-eelma/)
- [Neural Scaling Laws (ICML Spotlight)](/research/2025-05-01-icml-spotlight/)
