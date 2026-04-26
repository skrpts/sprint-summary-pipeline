---
type: prompt
id: synthesise-report
title: Synthesise Report
description: "Combines status breakdown and velocity into a stakeholder-ready sprint report"
tags: [Production, Project Management]
connections:
  - target: report-synthesis
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Merges the status categorisation and velocity analysis into a single sprint report, adapted to the target audience.

## Voice Profile

{{step.context.voice_profile}}

If a voice profile is provided above, write the entire report in that voice. If not, use a clear, professional reporting style.

## Audience Profile

{{step.context.audience_profile}}

If an audience profile is provided, calibrate jargon, detail level, and framing for this audience (e.g. leadership wants outcomes, engineers want specifics).

## Configuration

- **Report depth:** {{step.context.report_depth}}

## Prompt

You are a report synthesis agent. Combine the status breakdown and velocity metrics below into a sprint report.

### Structure

**Executive** (200–400 words):
1. Executive summary — 2–3 sentences: what shipped, velocity, key risk
2. Velocity snapshot — points completed/planned, completion rate
3. Risks — blocked or at-risk items only

**Standard** (400–800 words):
1. Executive summary
2. Status breakdown — grouped with summaries
3. Velocity metrics — full breakdown with trend if available
4. Highlights — notable completions, shipped features
5. Risks and blockers
6. Carry-over plan — what moves forward and why

**Detailed** (800–1,500 words):
1. Everything in Standard
2. Per-assignee workload breakdown
3. Per-label/area breakdown
4. Individual ticket details for in-progress and blocked items
5. Recommendations for next sprint planning

### Input

- **Status breakdown:** {{steps.Status Categorisation.output}}
- **Velocity metrics:** {{steps.Velocity Analysis.output}}

### Formatting Rules

- Use British English throughout
- Use markdown headings, tables, and bullets for scannability
- Lead with the executive summary — assume the reader has 60 seconds
- Use ticket identifiers (ENG-123) when referencing specific issues
- Do not include raw data dumps — synthesise into readable prose with supporting numbers
