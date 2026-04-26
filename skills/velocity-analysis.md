---
type: skill
id: velocity-analysis
title: Velocity Analysis
description: "Computes sprint velocity — points completed vs planned, completion rate, and trends"
tags: [Production, Project Management]
connections:
  - target: llm-service
    type: runs_on
context_params:
  velocity_context:
    label: "Velocity Context"
    description: "Previous sprint data for trend comparison (optional — paste prior sprint stats)"
    required: false
---

## Capability

Analyses the ticket set to compute sprint velocity metrics: points completed, points planned, completion rate, and (if previous data is provided) trend comparison.

## When to Use

- As a parallel analysis step after ticket fetching
- When stakeholders need quantitative sprint metrics

## What It Does

1. **Points completed** — sums point estimates for all Done tickets
2. **Points planned** — sums point estimates for all tickets that started in the sprint (excluding carry-overs added mid-sprint)
3. **Completion rate** — percentage of planned points delivered
4. **Carry-over load** — points carried from the previous sprint, and how many of those were completed
5. **Trend comparison** (if velocity_context provided) — compares current velocity to previous sprints, notes acceleration or deceleration
6. **Risk flags** — highlights tickets still in progress with high point values, or blocked tickets that may slip

## Outputs

Structured velocity report: points completed, points planned, completion percentage, carry-over stats, trend data (if available), and risk flags.
