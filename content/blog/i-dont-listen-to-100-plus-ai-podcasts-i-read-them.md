---
title: "I Don't Listen to 100+ AI Podcasts a Week. I Read Them."
date: 2026-04-25
draft: false
description: "How a local weekly pipeline turns 100+ AI podcast feeds into transcripts, two-pass LLM notes, a searchable vault, and a short Top N list you can actually read."
tags: ["productivity", "knowledge-base", "ai"]
---

If I tried to listen to every AI podcast I track, I'd need a sixty-hour week with no other inputs. The list sits at over a hundred shows: founders, investors, infra engineers, policy people, the occasional weird outlier. A lot of them publish weekly. Some twice. The queue outruns any realistic listening budget.

So I stopped being a human in that loop.

What I want is to know what the people building this technology are saying right now: what they think is hard, what they think is solved, who they're hiring against, where they think the field lands in six months. Audio is the format that information happens to ship in. Format is a delivery problem. The value is the signal underneath. The pipeline I run separates those two.

<!-- static/images/podcast-pipeline/production.svg -->
![The production line. Each stage runs locally on the same box.](/images/podcast-pipeline/production.svg)

Every show on my list lives in a registry with metadata: tags, tier, enabled/disabled. T1 is people I'd reorganize my week around if they said something specific. T6 is shows I keep enabled for exposure: background most weeks, there when I want the option. Tiers exist so the downstream curation step has a useful prior.

Once a week, the pipeline checks every enabled feed for new episodes in the window, downloads the audio, and pushes it through speech-to-text on a local box: 2×RTX 4090, 64GB RAM, Whisper on GPU. Local matters at this volume for two reasons. Cost first: cloud transcription on 100+ hours of audio every week is a real budget line. Turnaround second: the local stack finishes overnight, reliably, every time.

<!-- static/images/podcast-pipeline/workstation.jpeg -->
![The same workstation: dual RTX 4090, 64GB RAM. Overnight ingest, Whisper, and both LLM passes.](/images/podcast-pipeline/workstation.jpeg)

Transcripts are raw. They feed the next step; the note is the deliverable, raw text stays upstream.

The next step is a two-pass LLM summarization, Qwen3.6 at 128k context, also local. Pass one takes the full transcript plus metadata and writes a structured note: positioning of the show, who's on it, the actual claims being made, the bets, the contradictions, the open questions. Pass two is faithfulness. It goes back to the transcript and tightens any place pass one overstated, generalized, or rounded off an interesting edge. Models love to flatten. They round "I think this might be true in narrow cases" into "experts say." For knowledge work, that flattening is the whole problem. The second pass is cheap, runs locally, and is what makes the summary trustworthy.

Every episode moves through tracked states: new, downloaded, transcribed, summarized, failed. State tracking is boring infrastructure that pays off the first time something breaks at hour seven of a weekend run. I can resume, retry the failures, and re-run one show while leaving the other ninety-nine untouched.

The pipeline produces one Obsidian-ready note per episode, with frontmatter, consistent sections, and a link back to the source transcript. That's still a hundred-plus notes a week, which is too much to read. So a layer on top scores every note against my profile: agentic AI and automation patterns, AI product leadership, what AI-native organizations are doing with their structure and staff, where the field is heading next. It also checks against my recent vault history, so repeat themes surface at most once in a week. The output is a weekly Top N, usually 8 to 12 entries, each with a one-line "why this matters for you right now." That's the artifact I actually consume.

<!-- static/images/podcast-pipeline/curation.svg -->
![What I read versus what I keep. The ninety I skip that week stay in the corpus for search.](/images/podcast-pipeline/curation.svg)

The other 90 notes stay in the vault for when I search. When I need to know who's said what about agent evals over the last three months, the vault answers in seconds because the notes are already there. The pipeline gives me a corpus that is mine, structured, and refreshed every Monday. Before that, I only had a browser tab and hope.

Before this existed, my AI-podcast diet was three or four shows a week, mostly in the gym, mostly the obvious ones. I was sampling the top of the distribution. Now the distribution is the whole field, weighted by my own priors. The change shows up in the questions I can answer from my own knowledge base. "Who's actually building agent trajectory replay tooling?" "What did founders publicly say about agent eval at the last Sequoia summit?" I can answer both in seconds.

The pipeline itself is unremarkable as engineering. Feed reader, downloader, Whisper, two LLM passes, file writer, scoring layer. The subtle part is treating personal information consumption as a system with an SLA.

Next I'm thinking about graph RAG on the vault. I'll need to figure out how to connect that stack to Obsidian so the vault stays the single place I edit and the graph piece stays something I can actually run and maintain.
