---
title: "Weekly Digest, Week 15, 2026"
date: 2026-04-11
description: "Reasoning models like DeepSeek-R1 don't think longer. They simulate internal multi-agent debate, which explains the accuracy gap."
tags: ["weekly-digest", "ai", "llm", "research"]
keywords: ["weekly digest", "AI", "LLM", "reasoning models", "Vitaly Rodnenko"]
---

What caught my attention in W15.

## Reasoning Models Generate Societies of Thought

Research from Kim, Lai, Scherrer, Agüera y Arcas, and Evans shows that reasoning models like DeepSeek-R1 and QwQ-32B don't just think longer than instruction-tuned models. They simulate multi-agent debate internally. Mechanistic interpretability of reasoning traces reveals they activate a much broader diversity of personality- and expertise-related features during reasoning, shifting perspectives and reconciling conflicting views the way a group discussion would. The accuracy difference is concrete: models using this "society of thought" structure hit about 55% on complex tasks; suppress the mechanism and accuracy falls to around 24%. RL experiments confirm that base models develop these conversational behaviors when rewarded purely for reasoning accuracy. <a href="https://arxiv.org/abs/2601.10825" rel="nofollow noindex">Source</a>

Chain of thought isn't a longer monologue. It's an internal debate.

## The Adolescence of Technology

Dario Amodei's January 2026 essay maps the AI risk picture without sliding into doomerism. He defines "powerful AI" precisely: smarter than a Nobel laureate across biology, math, engineering, and coding; capable of autonomous multi-week tasks; running as millions of simultaneous instances by around 2027. He puts that level of capability at 1 to 2 years out. Current models already show manipulative, sycophantic, and deceptive behaviors in controlled testing. His core argument: stopping AI is not realistic given the momentum behind it, so the only viable path is building interpretability tools and introducing surgical regulation. The rules need to be specific enough to reduce concrete dangers without destroying progress. <a href="https://www.darioamodei.com/essay/the-adolescence-of-technology" rel="nofollow noindex">Source</a>

The adolescence framing holds up. We're being handed unprecedented power before the institutions that govern it have matured. Whether regulation can move fast enough is the open question.

## International AI Safety Report 2026

Compiled by more than 100 researchers, this report covers where AI risk actually sits right now. The boom isn't about to collapse. Compute, capital, and algorithmic progress keep driving things forward. The specific near-term concern isn't autonomous runaway systems; it's AI lowering the barrier to dangerous biological and chemical knowledge. On employment: no evidence of mass unemployment yet, but early pressure on junior roles and demand increasingly concentrated at the top. The sharpest observation is also the most mundane: heavy AI reliance could slowly erode human skills, critical thinking, and personal accountability, without anyone noticing until the damage is done. <a href="https://internationalaisafetyreport.org/sites/default/files/2026-02/ai-safety-report-2026-extended-summary-for-policymakers.pdf" rel="nofollow noindex">Source</a>

## Frontier Model Training Methodologies

Alex Wa's post breaks down training methodology across seven open-weight frontier models: SmolLM3, Intellect-3, Hermes 4, gpt-oss-120b, Kimi K2, DeepSeek-R1, and Arcee Trinity. Covers architecture choices (GQA, gated attention, MoE, hybrid designs), stability techniques (z-loss, QK-norm, RMSNorm, logit softcapping), tokenization, all three training phases (pre-, mid-, and post-training), and RL alignment. Not introductory material. If you want a practical reference for how frontier models are built, this is one of the more thorough ones available. <a href="https://djdumpling.github.io/2026/01/31/frontier_training.html" rel="nofollow noindex">Source</a>

## Karpathy's Autoresearch

Karpathy released autoresearch, a self-running research loop on a single GPU. Three files: prepare.py handles fixed data prep and evaluation utilities (never touched by the agent), train.py is what the agent iterates on (full GPT model, Muon+AdamW optimizer, training loop; everything is fair game), and program.md is where you write the agent's operating instructions. The agent modifies train.py, runs a fixed 5-minute training budget, checks val_bpb (validation bits per byte; lower is better, vocab-size-independent), keeps or discards the change, and repeats. You configure what to optimize, which hyperparameters to explore, how aggressive the search should be. Wake up to a log of experiments and a better model. <a href="https://github.com/karpathy/autoresearch" rel="nofollow noindex">Source</a>

## Attention Residuals

A proposal from the Kimi Team at Moonshot AI for rethinking how information flows through transformers. Standard residual connections accumulate all layer outputs with equal fixed weights, which causes uncontrolled hidden-state growth as depth increases and dilutes each layer's contribution more with each added layer. Attention Residuals (AttnRes) replaces this with softmax attention over all preceding layer outputs. Each layer learns which earlier representations matter most for the current token. More selective internal memory, more stable activations, useful early signals staying visible in deeper networks. Block AttnRes groups layers into blocks to make this practical at scale with lower memory and communication cost. <a href="https://arxiv.org/abs/2603.15031" rel="nofollow noindex">Source</a>

## Cloudflare's /crawl Endpoint

Cloudflare launched a /crawl endpoint that parses an entire website and returns the content as HTML, Markdown, or JSON. Primary use cases: powering RAG pipelines, building knowledge bases with current web content, monitoring content across multiple pages. Same vendor, two roles: Cloudflare is the stack that helps you keep bots and scrapers off your properties, and it is also the one giving you a first-party endpoint to crawl and parse whole sites on demand. <a href="https://developers.cloudflare.com/browser-rendering/quick-actions/crawl-endpoint/" rel="nofollow noindex">Source</a>
