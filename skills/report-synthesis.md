---
type: skill
id: report-synthesis
title: Report Synthesis
description: "Combines status breakdown and velocity metrics into a stakeholder-ready sprint report"
tags: [Production, Project Management]
connections:
  - target: llm-service
    type: runs_on
context_params:
  voice_profile:
    label: "Voice Profile"
    description: "Your writing style for the report — tone, vocabulary, and formality"
    required: false
  audience_profile:
    label: "Audience Profile"
    description: "Who will read this report — adjusts detail level and jargon"
    required: false
  report_depth:
    label: "Report Depth"
    description: "How detailed the report should be — Executive, Standard, or Detailed"
    default: "Standard"
    required: false
---

## Capability

Merges the status categorisation and velocity analysis into a single, stakeholder-ready sprint report. Adapts tone and detail level to the target audience.

## When to Use

- After the parallel categorisation and velocity steps have completed
- As the main synthesis step in a sprint reporting pipeline

## What It Does

1. **Executive summary** — 2–3 sentence overview: what shipped, velocity, key risks
2. **Status breakdown** — grouped by the categorisation mode with summaries
3. **Velocity metrics** — points completed/planned, completion rate, trend
4. **Highlights** — notable achievements, completed epics, significant features
5. **Risks and blockers** — blocked tickets, at-risk items, dependencies
6. **Carry-over plan** — what moves to the next sprint and why

## Report Depth Levels

- **Executive** — summary + velocity + risks only. 200–400 words. For leadership.
- **Standard** — everything above plus status breakdown and highlights. 400–800 words. For team leads and stakeholders.
- **Detailed** — full report with per-ticket detail, assignee workloads, and trend charts. 800–1,500 words. For the team.

## Outputs

Formatted sprint report in markdown, ready to share with stakeholders.
