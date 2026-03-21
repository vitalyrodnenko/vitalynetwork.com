---
title: "Who owns the agent?"
date: 2026-03-18
description: "Agentic Operating Model Part 6: agent ownership, decision rights, RBAC vs accountability, autonomy by action class, shadow mode to full autonomy, RACI, escalation paths, and stop signals."
slug: "who-owns-the-agent-decision-rights-accountability-rbac"
aliases: ["/blog/who-owns-the-agent/"]
series: "Agentic Operating Model · Part 6"
tags: ["agentic-ai", "org-design", "leadership", "product-leadership", "product-management", "governance"]
keywords: ["who owns the agent", "agent ownership", "agentic operating model", "decision rights", "RBAC", "accountability", "action classes", "autonomy zones", "human in the loop", "shadow mode", "agent governance", "multi-agent systems", "RACI", "escalation path", "stop signal", "production agents"]
---

The moment an agent is deployed, it has decision rights. The question is whether anyone designed them.

Every agent that goes into production carries a set of implicit decisions about authority — which actions it can take on its own, which require confirmation, who gets called when something falls outside what it knows. These decisions exist whether they were made deliberately or not.

## Two layers, one of which usually gets skipped

The natural starting point for agent permissions is what the agent is technically allowed to do. Engineers configure RBAC — which systems the agent can call, which tools it can invoke. That's a real and necessary layer.

But there's a second layer, and it answers a different question: who is accountable for the consequences if the result is wrong?

RBAC closes the first question. The second stays open by default.

The distinction matters because permission and accountability are not the same thing. An agent can be technically authorized to send a message to a customer, trigger a pricing update, or close a support case — and still have no human who owns the consequence of that action. When something goes wrong, the RBAC configuration won't tell you who to call. It was never designed to.

The accountability question becomes harder when a single agent handles actions with very different risk profiles.

## Action classes, not agents

There's a framing that I think creates problems.

The natural move is to assign an autonomy zone to the agent itself. This agent is supervised. That one is autonomous. The agent becomes the unit of control. And that creates a problem — because a single agent typically performs multiple types of actions with fundamentally different risk profiles.

I've seen this work well, in a team building a domain agent for operational planning. The agent handled three distinct classes of work, each with a different logic behind the access decision.

The first was metric analysis and bridging — read-only, exploratory, low cost of error. This was made available to everyone in the domain without restrictions.

The second was what-if simulations. These went further — they triggered real computational systems running actual calculations. The restriction here wasn't about data sensitivity. It was about compute cost. Running these simulations was expensive, and opening them to everyone would have been financially unjustifiable. Access was limited to a defined group.

The third was publishing changes to production. This was irreversible. The team didn't restrict it through a policy or a prompt instruction — the control was built directly around the tool. When the agent reached that step in a workflow, the system intercepted the call and required explicit confirmation from a human operator before anything continued. The agent physically could not publish without a person in the loop.

Three action classes. Three distinct rationales behind each decision. One agent.

Autonomy zones are assigned to action classes, not to agents as a whole. An agent can be fully autonomous in analysis and human-first in production actions.

The dangerous configuration is the one where the boundary between classes remains undefined. An agent diagnoses a problem, formulates a fix, and calls a production action — all inside one workflow, with no confirmation point between the diagnosis and the intervention. The transition from read to write happens invisibly. Nobody designed that boundary, because it seemed like an implementation detail.

In multi-agent chains, the risk compounds. The first agent does safe analysis. The second, acting on that analysis, affects production. Decision rights need to be designed at the chain level, not just at the level of each individual agent.

Escalation is part of this design too — not a separate mechanism bolted on, but a specified transition. The agent recognizes at runtime that a situation falls outside its zone, and hands control to a human. This path needs to exist before it's needed, not be discovered when something breaks.

## How autonomy actually gets assigned

In that operational planning project, the path to autonomous simulations was deliberate.

The customer would file a ticket. The team would run the simulation manually — and in parallel through the agent — then compare results. After a series of successful validations, the customer got access to the system directly, first with a shared session where the team could observe and co-review. Then, after a formal certification step, full autonomy.

Nobody declared the agent ready and moved on. Each transition was a decision. Someone looked at the data and said: we're ready.

![Each autonomy transition is a decision after reviewing data — from shadow mode to full autonomy](/images/who-owns-the-agent/transitions-readiness.svg)

1. **Shadow mode** comes first. The agent runs alongside the manual process. Outputs are compared. No action is taken by the agent. This phase tends to get cut. Without it, there's no baseline for calibration.
2. **Supervised** mode follows. The agent proposes; a human confirms before anything happens.
3. **Partial autonomy** comes next. The agent handles a portion of the traffic — by action type, by risk level, by scenario.
4. **Full autonomy** is when the agent acts independently, with humans on escalations.

Each step forward is a management decision, not a technical default. The owner looks at evals, quality metrics, escalation rates, and failure patterns — and makes a call.

The same logic runs in reverse. Autonomy earned can be pulled back. What returns an agent to the previous phase should be defined before it's needed. A stop signal is as important as a readiness criterion.

Which raises the question of who makes these calls.

## What it actually means to own an agent

In that project, the agent was owned by the product-engineering team — not the customers who used it, and not the operators who confirmed production changes. The operators are worth noting, though. They weren't a new group created for the agent. They were the same people who had always published production changes manually. The agent changed how the work got done. It didn't change who was trusted to authorize it. The confirmation step belongs to whoever already owned that action.

Owning the agent is different. The owner defines action class boundaries, reads telemetry, handles escalations, and carries the consequences. How accountability distributes depends on the action: fully autonomous actions sit entirely with the owner; supervised actions split responsibility between the owner and whoever confirmed; human-in-the-loop actions make the confirming person accountable for their authorization. The point isn't to distribute blame — it's to make accountability legible before anything goes wrong. A RACI matrix mapped to action classes is a practical way to do that explicitly.

## What this comes down to

Before any agent goes into production, four questions are worth settling: who owns this? Are action class boundaries defined? Is there an escalation path? Is there a stop signal?

These are management decisions. They don't get easier after launch.
