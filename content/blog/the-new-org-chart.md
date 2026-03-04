---
title: "The New Org Chart: Why Your Next Hire Should Be an Agent"
date: 2025-01-08
description: "An agent is not 'AI in a feature.' It is execution capacity. The right starting point is the org chart, not the model."
series: "Agentic Operating Model · Part 1"
tags: ["agentic-ai", "product-leadership", "org-design"]
---

An agent is not "AI in a feature." It is execution capacity. It performs real work that either (a) wasn't done before, (b) was done by internal teams, or (c) was outsourced — and that work has performance expectations: cost, turnaround time, measurable quality, and volume limits.

I've seen a good amount of "agent" projects start model-first: pick a strong model, wrap it in a chat UI, and hope useful work falls out. That can produce impressive demos, but production value comes from systems people trust — because they're observable, auditable, and controllable.

<div class="pull-quote">
<p>The right starting point is not the model. It is the org chart.</p>
</div>

## From org chart to map

Take the functions that exist today, map the workflows they own, and make the work explicit: inputs, decisions, handoffs, outputs, and the metrics those workflows are already held to.

Put each workflow on one page — trigger, key decisions, system actions, handoffs, and what "good" looks like in cost, time, quality, and throughput. Then ask a concrete question: which workflows (or slices of workflows) can move under agent ownership without breaking safety, controllability, or accountability.

### The clean cut

The only question that matters: where is the clean cut between "agent-owned" and "human-owned." Not by job title, but by decision type. An agent can own the parts that are repeatable and testable. Humans keep ownership of policy changes, high-blast-radius decisions, and ambiguous exceptions.

Autonomy should ramp in levels, not as a switch flip. A practical sequence is:

- **Draft only** — human executes
- **Pre-fill with approval** — human confirms
- **Execute inside hard limits** — human handles exceptions
- **Broaden scope** — once the system proves stable

This progression forces discipline. Each step up requires evidence in metrics and clean rollback paths, not simply confidence in the underlying model.
