---
title: "Agentic Operating Model — What to Migrate First"
date: 2025-01-18
description: "Not all workflows are equal candidates for agent ownership. Select by observability, repeatability, and reversibility."
series: "Agentic Operating Model · Part 2"
tags: ["agentic-ai", "operations", "migration"]
---

In MIT NANDA’s The GenAI Divide: State of AI in Business 2025, only 5% of integrated AI pilots are extracting millions in value, while the vast majority remain stuck with no measurable P&L impact. When the conversion rate is that low, the first win has to be engineered: pick a workflow slice that is measurable, bounded, and easy to integrate, then earn autonomy with gates.

## What to migrate first

AI-owned workflows can plug into a human decision tree (human-in-the-loop approvals at key action points), or run as services inside orchestrated systems. In this series, the focus is mostly on human-owned → agent-owned workflow migration, because it forces the hardest requirements: explicit ownership, measurable outputs, guardrails, escalation paths, and rollback.

Large-scale operations pay a real coordination tax: humans become the glue between fragmented signals, decisions, and execution. [Dave Clark](https://www.linkedin.com/in/davehclark/?lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3BAoIJphxPSaO7O1c35xpYsg%3D%3D) frames the same idea as moving past the [Human API](https://www.linkedin.com/pulse/from-10-furniture-autonomous-operations-planetary-scale-dave-clark-aef1c/?lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3BAoIJphxPSaO7O1c35xpYsg%3D%3D) and toward configurable autonomy within guardrails, where coordination is pushed into the operating system instead of living in people’s heads and meeting queues. That maps to how agents need to be built in practice: explicit contracts (inputs, outputs, constraints), integrated tool access, orchestration where needed, and a trust layer (telemetry, escalation, rollback) that lets autonomy expand without losing control.

Start with a slice that is boring, measurable, and bounded:

*   **Boring:** repeatable work with stable inputs and a standard shape.
*   **Measurable:** clear output definitions and existing success metrics (time, cost, quality, throughput).
*   **Bounded:** hard constraints, a clean rollback path, and an explicit escalation owner.

## Start from current ops

Before scoring anything, write down how the workflow runs today:

*   **Frequency:** How many times per day/week is it executed?
*   **Trigger:** What event starts it (ticket, threshold breach, calendar cadence, leader ask)?
*   **Latency:** What is the SLA, and where does work wait (handoffs, approvals, missing data)?
*   **Expertise dependency:** Is it junior-executable with a checklist, or does it require 1–2 scarce SMEs?
*   **Data dependencies:** What inputs are required, how often are they wrong, and who owns definitions?
*   **Delivery mechanism:** Where does the output landing (dashboard, email, ticket, config change, PO)?
*   **Stakeholders:** Who consumes it, who approves it, who is on-call when it breaks?
*   **Business impact:** What happens if it is late or wrong (cost, CX, compliance, risk)?

## The scorecard

Score each dimension 0–2, then pick the smallest slice that scores high and can run behind gates.

<div class="table-caption">Table: Agent-Readiness Scorecard — 10 checks for your first agent-owned workflow slice</div>

| Dimension | 0 (Not a fit yet) | 1 (Possible) | 2 (Good first slice) |
| :--- | :--- | :--- | :--- |
| **Execution frequency** | Monthly or ad hoc | Weekly | Daily or many times per day |
| **Trigger clarity** | Human sensemaking | Mixed triggers | Clear trigger (event, threshold, schedule) |
| **Latency pressure** | No SLA | Soft SLA | Hard SLA or recurring bottleneck |
| **SME dependency** | Requires scarce experts | Some SME review | Mostly checklistable, SMEs only for exceptions |
| **Data readiness** | Inputs unclear, definitions disputed | Inputs exist but messy | Inputs reliable, definitions owned |
| **Tool / delivery path** | Output has nowhere to land | Manual copy/paste step | Clear landing zone (ticket, dashboard, PR, config, email) |
| **Stakeholders + ownership** | Many approvers, unclear RACI | Known owner, some ambiguity | Named DRI for output + escalation |
| **Impact of late or wrong** | Low consequence | Local cost | Material cost, CX, or compliance risk |
| **Boundedness** | Open-ended actions | Some limits | Hard constraints + permissions scoped |
| **Rollback + recovery** | Irreversible | Reversible but painful | Clean rollback and playbooked recovery | 

## Example: from “what” to “what next”

In large-scale operations, teams track network metrics sliced by geo and aggregation level, and the “what happened?” layer is often straightforward. Natural-language-to-SQL assistants can translate questions into queries and summarize results, which is useful but often equivalent to better self-serve BI when dashboards are already strong.

The “why did it happen?” layer is where agent ownership becomes interesting: root-cause analysis is contextual, changes over time, and leans heavily on SME heuristics plus iterative analysis. A good first agent-owned slice here is metrics anomaly triage, not autonomous remediation:

*   **Trigger:** anomaly detection flags a KPI deviation at a specific slice (region, node group, channel).
*   **Output:** a structured RCA pack – top drivers, the most likely hypotheses, the top follow-up cuts to confirm, and candidate remediations with constraints.
*   **Gate:** a named SME or ops owner approves the hypothesis before any corrective action runs, which is a standard human-in-the-loop pattern for tool execution.

Once “what” and “why” are reliable, add the third step: planning.

*   **Options:** enumerate feasible remediations based on policy constraints, tool permissions, and lead times.
*   **Simulation:** run what-if analysis through integrated planning tools (or standard notebooks) and score options against the KPIs you already operate to.
*   **Plan proposal:** output a recommended plan plus 1–2 fallback plans, with expected KPI deltas and risks.

Autonomy then grows in a sequence tied to blast radius:

1.  **Recommendation mode:** agent proposes, human executes.
2.  **Approval mode:** agent executes after explicit confirmation.
3.  **Constrained execution:** agent deploys changes autonomously inside hard limits, with rollback, once calibration thresholds are consistently met.

## Non-negotiable filters

*   If success cannot be measured weekly, it’s not ready.
*   If there is no rollback, it’s not an agent – it’s a bet.
*   If decision rights are unclear, the project turns into negotiation instead of shipping.

Everything above is a way to make the first agent migration boring on purpose: bounded scope, gated execution, and reversible actions. Then trust becomes operational – instrument the workflow end-to-end so every tool call, decision, and outcome is observable and debuggable, not tribal knowledge.

---

*This article was originally published on [LinkedIn.](https://www.linkedin.com/pulse/part-2-agentic-operating-model-what-migrate-first-vitaly-rodnenko-zmurc/)*
