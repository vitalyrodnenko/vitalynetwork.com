---
title: "Weekly Digest, Week 17, 2026"
date: 2026-04-26
description: "A 15M-parameter JEPA model plans 48x faster than foundation-model alternatives, Meta open-sources a brain activity predictor trained on 1,115 hours of fMRI, and a new RAG benchmark methodology makes data leakage a structural non-issue."
tags: ["weekly-digest", "ai", "research", "llm"]
keywords: ["weekly digest", "AI", "product management", "Vitaly Rodnenko"]
---

What caught my attention in W17.

## DRAGOn: Designing RAG On Periodically Updated Corpus

Standard RAG benchmarks break down in production because they are static. Once a dataset is public, models can overfit to it, and it does not reflect the knowledge drift happening in live corpora. DRAGOn, published at EACL 2026 by Chernogorskii et al., addresses this by building test sets from Russian news using auto-extracted knowledge graphs, then generating multi-hop QA pairs via LLM. To score well, a model has to connect facts across multiple documents; pattern-matching a retrieved chunk will not cut it. A judge model evaluates on completeness and factual accuracy, not token overlap. Fresh dataset versions get generated on schedule, so data leakage is structural rather than accidental.

The methodology can drop into internal tooling: benchmark your RAG pipeline against your own corpus before shipping. That is where the value is for analytics, document-heavy enterprise systems, or support workflows where a bad retrieval costs real money. <a href="https://arxiv.org/abs/2507.05713" rel="nofollow noindex">Source</a>

## LeWorldModel: Stable End-to-End JEPA from Pixels

LeCun's JEPA (Joint-Embedding Predictive Architecture) predicts abstract representations of what comes next, not the raw pixels or tokens. The argument is simple: pixel prediction forces a model to reconstruct every irrelevant surface detail to minimize loss. JEPA skips the surface and targets the structure. LeWorldModel (LeWM) is the first implementation that trains stably end-to-end from raw pixels without a pre-trained encoder, using only two loss terms: a next-embedding prediction loss and a Gaussian regularizer that prevents representation collapse. Prior end-to-end alternatives needed six tunable loss hyperparameters.

At 15M parameters, trainable on a single GPU in a few hours, LeWM plans 48x faster than foundation-model-based alternatives and stays competitive across 2D and 3D control tasks. Authors Maes, Le Lidec, Scieur, LeCun, and Balestriero show its latent space encodes physical structure and reliably flags physically implausible events without explicit supervision.

The performance-per-parameter number is the interesting part. 15M parameters matching foundation models on planning tasks. If JEPA's scaling properties hold, the architecture has room to run. <a href="https://arxiv.org/abs/2603.19312" rel="nofollow noindex">Source</a>

## Meta TRIBE v2: A Foundation Model for Brain Activity Prediction

Meta FAIR released TRIBE v2 on March 26, a trimodal foundation model (LLaMA 3.2 for text, V-JEPA2 for video, Wav2Vec-BERT for audio) that predicts fMRI brain responses across 20,484 cortical vertices. Trained on 1,115 hours of fMRI from over 720 subjects, it outputs a predicted BOLD signal at 1 Hz per cortical point given any combination of video, audio, or text input. Two results stand out.

Zero-shot predictions track group-averaged brain responses more closely than individual fMRI scans. Individual scans are noisy: heartbeats, motion artifacts, and individual variance. The model averages over 720 subjects and does not have that problem. Second, it follows log-linear scaling laws with no plateau, the same pattern as LLMs. The architecture is not exotic: frozen encoders plus a transformer integration layer plus subject-specific projection heads. The interesting part is the result, not the design. Notably, the model recovers known functional networks, including primary auditory, language, motion, default mode, and visual, without any fMRI data at inference time. Weights, code, and an interactive demo are open-sourced under CC BY-NC.

The practical frame: an API to a canonical human brain. Neuromarketing and UX research teams will use this before most neuroscientists do. <a href="https://aidemos.atmeta.com/tribev2/" rel="nofollow noindex">Source</a>
