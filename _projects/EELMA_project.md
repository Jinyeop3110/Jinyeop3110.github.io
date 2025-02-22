---
layout: page
title: Scaling Empowerment Estimation of a Language Model Agent
description: MATS Program - Winter 2024-25 Cohort
img: assets/img/3.jpg
importance: 3
category: AI safety
---
## <mark>Summary</mark>  
We will propose a scalable method for quantifying the empowerment (i.e., one's control over the future state) of a Language Model agent. haha

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/publications/EELMA/Fig1.png" title="EELMA Figure 1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Figure 1. EELMA - Estimating Empowerment of Language Model Agent, is motivated to provide a scalable method for quantifying POWER of LM agent.

## <mark>Abstract</mark>  
As LLM agents become more intelligent and gain wider access to real-world tools, there is growing concern about them potentially developing power-seeking behavior. This presents a potential serious risk, as we currently lack empirical methods to measure power in LLM agents. In this project, we address this problem for the first time by proposing a scalable method for quantifying the power of a LLM agent. Our method, named EELMA - Estimating Empowerment of Language Model Agents, builds on information theory and contrastive learning to enable efficient estimation of empowerment from text-based interactions in a given environment or agentic task. With the proposed framework, we have two main goals: first, to implement and validate EELMA across various agentic tasks, and second, to demonstrate how EELMA can help address alignment challenges.

## <mark>Theory of Change</mark>

**Threat Model -** Power seeking LLM agents and methodological challenge.  
Power-seeking AIs are a significant threat. Power is vaguely defined as the ability to achieve a wide range of goals. For example, "money is power," as money is instrumentally useful for many goals [1]. Similar to humans, when superintelligent AI becomes more involved in the real world where it is continually tasked with multiple goals with high uncertainty, it can simply choose to maximize power – which is called power-seeking behavior. The emergence of power-seeking AI is likely to be a significant threat for multiple reasons [2][3]. First, power-seeking agents are likely to be adversarial to human control and existing alignment protections, such that they may build resistance to shutdown protocols. Second, AI with great computing power and its non-physically constrained nature enables it to engage in more sophisticated and extensive power-seeking behavior that conventional control methods are ineffective.  
LLM agents are potential power-seeking AI in the near future. Recently, LLM agents are becoming increasingly connected to more "tools" and "information" in the real world, such as through RAG [4], [5] or Tool Use [6]. This empowers agents with more options for interacting with the world. At the same time, frontier AI labs are racing to scale and improve the reasoning capabilities and operational efficiency of LLMs. This enables LLMs to become smart enough to understand the notion of power and optimize their actions to maximize it. Assuming these two developments continue to progress rapidly over the next few years, there is a growing existential risk that power-seeking LLM agents will emerge.  

**Lack of methods to quantify power.**  
While the growing risk highlights the importance of studying and developing alignment techniques for power-seeking LLM agents, we don't even have a good starting method to measure power. The formal definition of power in Markov Decision Processes (MDPs) was introduced very recently, indicating a lack of theoretical foundations yet [1][3]. Furthermore, directly applying such a framework is largely impractical as we don't have MDPs for LLM agents. Inferring MDPs is intractable as it requires an exponentially large number of observations. Therefore, we lack practical methods to quantify the power of language models, and this is a significant bottleneck for preparing against potential power-seeking LLM agents.

## <mark>Impact Analysis</mark>  
The core motivation of this project is to propose EELMA as an effective method to measure power and study the power-seeking behavior of LLM agents. EELMA leverages an information theoretic concept called empowerment [6][12] (see the Method section) as a measure of power, which formalizes the vague definition of power (i.e., the ability to achieve a wide range of goals) and is well defined across diverse scenarios and contexts. We expect the following impacts:
- Foundational methodology for studying the power of LM agents.
- Comparison with benchmark approach.
- Practical control system for power-seeking behavior.
- Integration with RL as an alignment objective.

## <mark>Risk Analysis</mark>  
Success/Failure chance: The project goal is fundamentally challenging because it involves developing novel methodologies. Nonetheless, we have evidences supporting its potential for success:
- Existence of prior models.
- Embedding models.
- Dual usage risk.
- Infohazard minimized.

## <mark>Method: EELMA</mark>  
EELMA quantifies power through Empowerment [6][12]—a measure of an agent's ability to control its environment through its actions. Empowerment shows how much influence an agent has over its future states, making it a useful metric for spotting when an agent is gaining unintended power or capabilities. By measuring how an agent's actions affect its future possibilities, empowerment offers a general way to detect power-seeking behavior without needing to define specific warning signs. For example, if an agent gains elevated system privileges, it will show increased empowerment because it can now affect more future states, even if we haven't labeled privilege escalation as a specific concern.

However, computing empowerment in Language Model Agents is challenging. The state and action spaces are high-dimensional, which makes traditional empowerment calculations computationally intractable. In addition, these environments are non-stationary—the available actions and their effects can change over time—making measurement even more complicated.

To tackle these issues, we will first develop state embedding models that effectively reduce the dimensionality of agent states while keeping the important information needed for analyzing power dynamics. We plan to fine-tune language embedding models to embed high-dimensional states (such as web browsing patterns or code modification histories) into a lower-dimensional space. Second, we will implement a critic model for efficient mutual information estimation between agent actions and future states using contrastive learning techniques. Specifically, we will apply noise-contrastive estimation to approximate mutual information by comparing actual state transitions caused by the agent with randomly sampled counterfactuals.

## <mark>Research Plan</mark>

**Phase 1 (MATS 7.0): EELMA Implementation and Evaluation**  
We start with developing the comprehensive pipeline to test and evaluate EELMA. Components include:
- Mutual Information estimation module using contrastive learning.
- LLM agents.
- Various agentic task benchmarks.
- Other non-text-based empowerment estimation methods.

**Week 1-5: Implementing EELMA**  
• Developed a parallel pipeline for generating Agent-World plays of LLM models  
• Implemented the noise contrastive component of EELMA  
• LLM agents - Vanilla, CoT, and ReACT agents  
• Established a 2D grid world environment  

**Week 6-10: Evaluating and optimizing EELMA**  
Evaluation will include:
• Accuracy  
• Efficiency  
• Generality  

**Phase 2 (Post-MATS): Power-Seeking Behavior Study**  
March-May: Model study of power-seeking behaviors  
May-Aug: Toward disempowered, helpful LLM agents  
• Employ RLHF techniques to optimize agents for reduced power-seeking behavior.  
• Submit findings to NeurIPS 2025 and post to LessWrong.

## <mark>References</mark>  
[1] A. M. Turner et al., “Optimal Policies Tend to Seek Power,” 2019.  
[2] J. Carlsmith, “Is Power-Seeking AI an Existential Risk?,” 2022.  
[3] A. M. Turner, “On Avoiding Power-Seeking by Artificial Intelligence,” 2022.  
[4] D. Rothman, RAG-Driven Generative AI, 2024.  
[5] A. Vemula, Retrieval-Augmented Generation using LLMs.  
[6] C. Qu et al., “Tool Learning with Large Language Models: A Survey,” 2024.  
[7] M. I. Belghazi et al., “MINE: Mutual Information Neural Estimation,” 2018.  
[8] A. van den Oord et al., “Representation Learning with Contrastive Predictive Coding,” 2018.  
[9] R. Zhao et al., “Mutual Information State Intrinsic Control,” 2021.  
[10] V. Myers et al., “Learning to Assist Humans without Inferring Rewards,” 2024.  
[11] L. Wang et al., “Improving Text Embeddings with Large Language Models,” 2023.  
[12] C. Salge et al., “Empowerment -- an Introduction,” 2013.  
[13] P. Czyż et al., “Beyond Normal: On the Evaluation of Mutual Information Estimators,” 2023.  
[14] B. Poole et al., “On Variational Bounds of Mutual Information,” 2019.
