---
title: "Agentic Operating Model — What to Migrate First"
date: 2025-01-18
description: "Not all workflows are equal candidates for agent ownership. Select by observability, repeatability, and reversibility."
series: "Agentic Operating Model · Part 2"
tags: ["agentic-ai", "operations", "migration"]
---

Not all workflows are equal candidates for agent ownership. The temptation is to start with the highest-value process, but that's usually also the highest-risk one. A better filter: start where you have the best **observability**, **repeatability**, and **reversibility**.

## Observability first

If you can't measure what a workflow does today, you can't tell whether an agent is doing it better or worse. Before migrating anything, instrument the current process. Know the baseline: volume, error rate, cycle time, cost per unit.

## Repeatability as a prerequisite

Agents excel at workflows that are structurally consistent. If every instance of a process looks different, you're not automating — you're improvising with a model. Look for workflows where 80%+ of instances follow the same decision tree.

## Reversibility as a safety net

The best first candidates are workflows where a bad agent decision can be caught and corrected before it causes real damage. Order routing? Reversible. Pricing changes pushed to 10M customers? Not reversible. Start with the former.
